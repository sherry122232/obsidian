```
import { Component, OnInit, NgZone, inject } from '@angular/core';
import { Functions, httpsCallable } from '@angular/fire/functions';
import { Router } from '@angular/router';
import { BehaviorSubject, switchMap, tap } from 'rxjs';
import { Project } from '../projectService/project.model';
import { ProjectService } from '../projectService/project.service';

@Component({
    selector: 'sd-projects',
    templateUrl: './projects.component.html',
    styleUrls: ['./projects.component.scss'],
})
export class ProjectsComponent implements OnInit {
    private projectService: ProjectService = inject(ProjectService);
    private router: Router = inject(Router);
    private zone: NgZone = inject(NgZone);
    private functions: Functions = inject(Functions);

    favoriteTotalAmounts: number = 0;
    ownedTotalAmounts: number = 0;
    pageProjects: any = [];
    favoriteProjectList: any;
    docOwnedSnap: any;

    ownOrAll: BehaviorSubject<string> = new BehaviorSubject<string>('own');

    constructor() {
        this.projectService.favoriteProjects.subscribe((projects: Project[]) => {
            this.zone.run(() => {
                this.favoriteTotalAmounts = projects.length;
                this.favoriteProjectList = projects;
                console.log('triggered favoriteProjectList', this.favoriteProjectList);
            });
        });

        this.ownOrAll
            .pipe(
                tap(() => {
                    console.log('tap 1');
                }),
                switchMap((isOwn: string) => {
                    this.pageProjects = [];
                    this.projectService.showMoreProjects.next(null);
                    if (isOwn == 'own') {
                        return this.projectService.ownedProjects;
                    } else {
                        return this.projectService.allOtherProjects;
                    }
                }),
            )
            // .subscribe((projects: Project[]) => {
            //     if (projects.length > 0) {
            //         this.docOwnedSnap = projects[projects.length - 1];
            //     }
            //     this.zone.run(() => {
            //     this.totalAmounts = projects.length;
            //     this.pageProjects.push(...projects);
            //         console.log('triggered own/all projects', this.pageProjects);
            //     });
            // });
            .subscribe((projects: Project[]) => {
                
                for (const project of projects) {
                    if (!this.pageProjects.some((p: { projectId: string }) => p.projectId === project.projectId)) {
                        this.pageProjects.push(project);
                    }
                }

                // need to optimize - Update isFavorite for Pageprojects, if the updated one isn't one of the subscribed projects
                for (const project of this.pageProjects) {
                    if (!this.favoriteProjectList) project.isFavorite = false;
                    else project.isFavorite = this.favoriteProjectList.some((p: { projectId: string }) => p.projectId === project.projectId);
                }

                if (projects.length > 0) {
                    this.docOwnedSnap = projects[projects.length - 1];
                }

                this.zone.run(() => {
                    console.log('triggered own/all projects', this.pageProjects);
                });
            });
    }

    ngOnInit(): void {}

    subscribeToShowMore() {
        this.projectService.showMoreProjects.next(this.docOwnedSnap.snapshot);
    }

    createProject() {
        this.router.navigate(['/labs', ':lab', 'create-project']);
    }

    /**
     * remove favorite project from favoriteProjectss for the provided project
     * @param project object
     */
    removeFavorite(projectId: any) {
        // httpsCallable<any, any>(this.functions, 'api/removeFavorite')(projectId);
        console.log('Removing project: ', projectId, 'from favorite');
        httpsCallable<any, any>(this.functions, 'api/toggleFavorite')({ projectId: projectId, isFavorite: false });
    }

    /**
     * remove favorite project from favoriteProjectss for the provided project
     * @param project object
     */
    toggleFavorite(projectId: any) {
        if (this.favoriteProjectList && this.favoriteProjectList.map((project: { projectId: any }) => project.projectId).includes(projectId)) {
            console.log('Removing project: ', projectId, 'to favorite');
            httpsCallable<any, any>(this.functions, 'api/toggleFavorite')({ projectId: projectId, isFavorite: false });
        } else {
            console.log('Add project: ', projectId, 'from favorite');
            httpsCallable<any, any>(this.functions, 'api/toggleFavorite')({ projectId: projectId, isFavorite: true });
        }
    }
}
```





## projects
```

import { inject, Injectable } from '@angular/core';
import { Firestore, collection, query, orderBy, documentId, where, limit, startAfter } from '@angular/fire/firestore';
import { collection as collect } from 'rxfire/firestore';
import { Observable, mergeMap, shareReplay, map, filter, mergeAll, tap, distinctUntilChanged, takeLast, skipUntil, skipWhile, takeWhile, take, skip, BehaviorSubject, defaultIfEmpty } from 'rxjs';
import { ScidapService } from '../../services/scidap.service';
@Injectable({
    providedIn: 'root',
})
export class ProjectService {
    private firestore: Firestore = inject(Firestore);
    private scidapService: ScidapService = inject(ScidapService);

    public favoriteProjects: Observable<any>; // declare variable, not assignement
    public ownedProjects: Observable<any>;
    public allOtherProjects: Observable<any>;
    pageSize = 5;
    pageFavoriteSize= 100;
    laboratoryId$: Observable<any>;

    docOwnedSnap: any;
    docAllOtherSnap: any;
    docFavoriteSnap: any;

    favoriteQueryCollectionDocs$: Observable<any>;
    readonly showMoreProjects: BehaviorSubject<any> = new BehaviorSubject<any>(null);
    
    constructor() {
        this.laboratoryId$ = this.scidapService.userProfile$.pipe(
            tap(() => {
                console.log('LaboratoryId Executed');
            }),
            mergeMap(({ user }) => {
                const q: any = query(collection(this.firestore, 'laboratories'), where('ownerUID', '==', user.uid));
                return collect(q).pipe(
                    map((doc: any) => {
                        if (doc && doc.length > 0) return { laboratoryId: doc[0].id, user };
                        return { laboratoryId: null, user };
                    }),
                );
            }),
            shareReplay(1),
        );

        this.favoriteQueryCollectionDocs$ = this.laboratoryId$.pipe(
            tap(() => {
                console.log('Favorite Query Collection Executed');
            }),
            mergeMap(({ laboratoryId, user }) => {
                // console.log('in get fave coll. user: ', JSON.stringify(u.user));
                //TODO: check how changes in user (tokens, passwords) would retrigger
                const q: any = query(collection(this.firestore, 'favorite'), where('type', '==', 'projects'), where('userId', '==', user.uid));
                //we got a reactive variable that changes all the time there is a change in database
                return collect(q).pipe(
                    map((doc: any) => {
                        if (doc && doc.length > 0) return { favoriteProjects: doc[0].data()['projects'], laboratoryId, user };
                        return { favoriteProjects: [], laboratoryId, user };
                    }),
                );
            }),
            shareReplay(1), // we replay last recived data when new subscribe called. subscribe happening somewhere in our code async...
        );

        this.favoriteProjects = this.favoriteQueryCollectionDocs$.pipe(
            tap(({ favoriteProjects, laboratoryId, user }) => {
                console.log('Favorite Projects Executed');
            }),
            filter(({ favoriteProjects }) => favoriteProjects.length),
            mergeMap(({ favoriteProjects }) => {
                const q: any = query(collection(this.firestore, 'projects'), where(documentId(), 'in', favoriteProjects), orderBy('laboratoryId'), limit(this.pageFavoriteSize));
                //we got a reactive variable that changes all the time there is a change in database
                return collect(q).pipe(
                    tap(()=>{console.log("tap 4")}),
                    map((projectList) => {
                        return projectList.map((project) => ({ ...project.data(), projectId: project.id, isFavorite: true }));
                    }),
                );
            }),
        );

        // get owned projects
        this.ownedProjects = this.favoriteQueryCollectionDocs$.pipe(
            mergeMap(({ favoriteProjects, laboratoryId, user })=> {
                return this.showMoreProjects.pipe(
                    map((snapshot)=>{
                        return {snapshot, favoriteProjects, laboratoryId, user}
                    })
                )
            }),
            tap(({ favoriteProjects, laboratoryId, user }) => {
                console.log('Owned Projects Executed');
            }),
            mergeMap(({ snapshot, favoriteProjects, laboratoryId, user }) => {
                const q: any = query(collection(this.firestore, 'projects'), where('ownerUID', '==', user.uid), orderBy('laboratoryId'), startAfter(snapshot), limit(this.pageSize));
                return collect(q).pipe(
                    tap(()=>{console.log("tap 3")}),
                    map((projectList) => {
                        return projectList.map((project) => ({ ...project.data(), projectId: project.id, isFavorite: favoriteProjects.includes(project.id), snapshot: project}));
                    }),
                );
            }),
            
        );

        // get all other projects
        this.allOtherProjects = this.favoriteQueryCollectionDocs$.pipe(
            mergeMap(({ favoriteProjects, laboratoryId, user })=> {
                return this.showMoreProjects.pipe(
                    map((snapshot)=>{
                        return {snapshot, favoriteProjects, laboratoryId, user}
                    })
                )
            }),
            tap(() => {
                console.log('All Other Projects Executed');
            }),
            mergeMap(({ snapshot, favoriteProjects, laboratoryId, user }) => {
                const queryRef: any = query(collection(this.firestore, 'projects'), where('laboratoryId', '==', laboratoryId), orderBy('laboratoryId'), startAfter(snapshot), limit(this.pageSize));
                return collect(queryRef).pipe(
                    map((projectList) => {
                        return projectList.map((project) => ({ ...project.data(), projectId: project.id, isFavorite: favoriteProjects.includes(project.id), snapshot: project}));
                    }),
                );
            }),
        );
    }

    updateLocalOwnDoc(newValue: any): void {
        this.docOwnedSnap = newValue;
    }

    updateLocalAllOtherDoc(newValue: any): void {
        this.docAllOtherSnap = newValue;
    }
}
```

