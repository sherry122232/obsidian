
```
import { Component, OnInit, NgZone, inject } from '@angular/core';

import { Router } from '@angular/router';

import { getAuth, onAuthStateChanged } from 'firebase/auth';

import { DocumentSnapshot } from 'firebase/firestore';

import { Observable, of } from 'rxjs';

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

private ngZone: NgZone = inject(NgZone);

  
  

totalAmounts: number = 0;

favoriteTotalAmounts: number = 0;

ownedTotalAmounts: number = 0;

  

currentPage: number = 1;

favoriteCurrentPage: number = 1;

ownedCurrentPage: number = 1;

  

amountPerPage: number = 1;

favoriteAmountPerPage: number = 10;

ownedAmountPerPage: number = 1;

  

pageProject: any;

pageOwnedProject: any;

  

totalPages: number = 0;

ownedTotalPages: number = 0;

favoriteTotalPages: number = 0;

  

  

goalPage = 1;

  

labId = '';

projects: Project[] = [];

userId = '';

  

// favoriteProjects: Observable<Project[]>; // = of([]);

favoriteProjectList:any;

  
  

constructor() {

this.getOwnedProjectsAmount().subscribe((value) => {

this.ownedTotalAmounts = value;

});

  

this.getTotalProjectsAmount().subscribe((value) => {

this.totalAmounts = value;

});

  

// this.favoriteProjects = this.projectService.favorites;

// this.favoriteProjects

this.projectService.favorites.subscribe((projects: Project[]) => {

this.favoriteTotalAmounts = projects.length;

this.favoriteProjectList = projects;

});

  

this.projectService.getPageProjects(1, this.ownedAmountPerPage, this.ownedTotalAmounts, this.ownedTotalPages, this.ownedCurrentPage).subscribe((projects: Project[]) => {

this.pageOwnedProject = projects;

})

  

const auth = getAuth();

onAuthStateChanged(auth, (user) => {

if (user) {

this.findLabId(user.uid);

} else {

console.log('You are not an authenticated user');

}

});

}

  

ngOnInit(): void {}

  

// getFavorite() {

// return this.projectService.getFavoritesProjects();

// }

  

// getFavoriteProjectsAmount(): Observable<number> {

// return this.projectService.getFavoriteProjectsDocumentCount();

// }

  

getOwnedProjectsAmount(): Observable<number> {

return this.projectService.getOwnedProjectsDocumentCount();

}

  

getTotalProjectsAmount(): Observable<number> {

return this.projectService.getOtherProjectsDocumentCount();

}

  

findLabId(userId: string) {

this.projectService

.getLabId(userId)

.then((labId) => {

if (labId) {

this.labId = labId;

this.projectService.getPageProjects(1, this.amountPerPage, this.totalAmounts, this.totalPages, this.currentPage).subscribe((projects: Project[]) => {

this.pageProject = projects;

})

// this.getTotalProjectsAmount(this.labId, 'other');

} else {

}

})

.catch((error) => {

console.error('Error retrieving lab ID:', error);

});

}

  

onTotalPagesChange(totalPages: number) {

this.totalPages = totalPages;

}

  

createProject() {

this.router.navigate(['/labs', ':lab', 'create-project']);

}

  

onCurrentPageChange(page: number, name: string) {

this.onPageChanged(page, name);

if (name === 'other') this.currentPage = page;

else if (name === 'favorite') this.favoriteCurrentPage = page;

else this.ownedCurrentPage = page;

}

  

onPageChanged(goalPage: number, name: string) {

if (name == 'other') {

this.projectService.getPageProjects(goalPage, this.amountPerPage, this.totalAmounts, this.totalPages, this.currentPage).subscribe((projects: Project[]) => {

this.pageProject = projects;

})

} else if (name == 'owned') {

this.projectService.getOwned(goalPage, this.ownedAmountPerPage, this.ownedTotalAmounts, this.ownedTotalPages, this.ownedCurrentPage).subscribe((projects: Project[]) => {

this.pageOwnedProject = projects;

})

}

}

  

/**

* Get projects for all other projects, needs to refactored

* @param goalPage

*/

  

}
```

```
import { inject, Injectable } from '@angular/core';

import { Firestore, collection, query, orderBy, startAfter, limit, where, getDocs, DocumentSnapshot, DocumentData, documentId, QueryDocumentSnapshot, QuerySnapshot, Query } from '@angular/fire/firestore';

import { collection as collect } from 'rxfire/firestore';

import { from, Observable, of, switchMap, mergeMap, shareReplay, map, catchError, filter, tap } from 'rxjs';

  

import { Project } from './project.model';

import { ScidapService } from '../../services/scidap.service';

@Injectable({

providedIn: 'root',

})

export class ProjectService {

private first: any = undefined;

private firestore: Firestore = inject(Firestore);

private scidapService: ScidapService = inject(ScidapService);

  

public favorites: Observable<any>; // declare variable, not assignement

public owned: Observable<any> = of([]);

public allOther: Observable<any> = of([]);

favoriteQueryCollectionDocs$: Observable<any>;

  

ownedDocumentSnap: any;

ownedhashmap: { [key: number]: Observable<Project[]> } = {};

ownedhashmap2: { [key: number]: Observable<DocumentSnapshot> } = {};

  

documentSnap: any;

hashmap: { [key: number]: Observable<Project[]> } = {};

hashmap2: { [key: number]: Observable<DocumentSnapshot> } = {};

  

constructor() {

this.favoriteQueryCollectionDocs$ = this.scidapService.userProfile$.pipe(

mergeMap(({user}) => {

// console.log('in get fave coll. user: ', JSON.stringify(u.user));

//TODO: check how changes in user (tokens, passwords) would retrigger

const q = query(collection(this.firestore, 'favorite'), where('type', '==', 'projects'), where('userId', '==', user.uid));

//we got a reactive variable that changes all the time there is a change in database

return collect(q);

}),

shareReplay(1) // we replay last recived data when new subscribe called. subscribe happening somewhere in our code async...

);

  

this.favorites = this.favoriteQueryCollectionDocs$.pipe(

filter(d=>d.length && d[0].data()['projects'].length),

mergeMap((doc) => {

const q = query(collection(this.firestore, 'projects'), where(documentId(), 'in', doc[0].data()['projects']));

//we got a reactive variable that changes all the time there is a change in database

return collect(q);

}),

map((projectList) => projectList.map((project) => ({ ...project.data(), _id: project.id })))

);

}

  

// isFavoriteOrNot(projectId: string): Observable<any> {

// return this.favoriteQueryCollectionDocs$.pipe(

// map((doc) => {

// if (!doc || doc.length === 0 || doc[0].data()['projects'].length === 0 || !(projectId in doc[0].data()['projects'])) {

// return false;

// } else {

// return true;

// }

// }),

// );

// }

  

async getLabId(userId: string): Promise<string | null> {

const labCollection = collection(this.firestore, 'laboratories');

const labQuery = query(labCollection, where('ownerUID', '==', userId));

  

const querySnapshot = await getDocs(labQuery);

if (!querySnapshot.empty) {

const document = querySnapshot.docs[0]; // Assuming there is only one matching document

const documentId = document.id;

return documentId;

}

return null; // No matching document found

}

  

updateFavoriteStatus(pageProject: Project[]): Observable<Project[]> {

return this.scidapService.userProfile$.pipe(

switchMap((u) => {

const favoriteCollection = collection(this.firestore, 'favorite');

const favoriteQuery = query(favoriteCollection, where('userId', '==', u.user.uid), where('type', '==', 'projects'));

  

return from(getDocs(favoriteQuery)).pipe(

switchMap((querySnapshot: QuerySnapshot<DocumentData>) => {

const favoriteProjects: string[] = [];

  

querySnapshot.forEach((doc: QueryDocumentSnapshot<DocumentData>) => {

const favoriteData = doc.data();

const favoriteProjectIds = favoriteData?.['projects'] || [];

favoriteProjects.push(...favoriteProjectIds);

});

  

pageProject.forEach((project: Project) => {

if (favoriteProjects.includes(project._id)) {

project.isFavorite = true;

}

});

  

return of(pageProject);

}),

);

}),

);

}

  

getPageProjects(goalPage: number, AmountPerPage: number, TotalAmounts: number, TotalPages: number, currentPage: number): Observable<Project[]> {

if (this.hashmap.hasOwnProperty(goalPage)) {

this.documentSnap = this.hashmap2[goalPage];

return this.hashmap[goalPage];

}

return of([]);

// else {

// return this.getcollectionRef(this.documentSnap=undefined,"", currentPage, goalPage, AmountPerPage=10).pipe(

// mergeMap((projects) => {

// let last;

// if (TotalPages > 1 && goalPage == TotalPages && TotalAmounts % AmountPerPage != 0) {

// last = -TotalAmounts % AmountPerPage;

// } else {

// last = -AmountPerPage;

// }

// this.allOther = this.updateFavoriteStatus(

// projects

// .map((project) => {

// const projectData = project.data() as Project;

// projectData._id = project.id;

// return projectData;

// })

// .slice(last),

// );

// this.documentSnap = projects[projects.length - 1];

// this.hashmap[goalPage] = this.allOther;

// this.hashmap2[goalPage] = this.documentSnap;

// return this.hashmap[goalPage];

// }),

// );

// }

}

  

getOwned(goalPage: number, ownedAmountPerPage: number, ownedTotalAmounts: number, ownedTotalPages: number, currentPage: number): Observable<Project[]> {

if (this.ownedhashmap.hasOwnProperty(goalPage)) {

this.ownedDocumentSnap = this.ownedhashmap2[goalPage];

return this.ownedhashmap[goalPage];

} else {

return this.getOwnedcollectionRef(this.ownedDocumentSnap=undefined, currentPage, goalPage, ownedAmountPerPage=10).pipe(

mergeMap((projects) => {

let last;

if (ownedTotalPages > 1 && goalPage == ownedTotalPages && ownedTotalAmounts % ownedAmountPerPage != 0) {

last = -ownedTotalAmounts % ownedAmountPerPage;

} else {

last = -ownedAmountPerPage;

}

this.owned = this.updateFavoriteStatus(

projects

.map((project) => {

const projectData = project.data() as Project;

projectData._id = project.id;

return projectData;

})

.slice(last),

);

this.ownedDocumentSnap = projects[projects.length - 1];

this.ownedhashmap[goalPage] = this.owned;

this.ownedhashmap2[goalPage] = this.ownedDocumentSnap;

return this.ownedhashmap[goalPage];

}),

);

}

}

  

getcollectionRef(lastsnapshot: any, laboratoryId: any, currentPage: any, goalPage: any, amountPerPage: any) {

if (lastsnapshot === undefined) {

this.first = query(query(collection(this.firestore, 'projects'), where('laboratoryId', '==', laboratoryId)), orderBy('laboratoryId'), limit(amountPerPage));

} else {

if (goalPage === currentPage + 1) {

this.first = query(query(collection(this.firestore, 'projects'), where('laboratoryId', '==', laboratoryId)), orderBy('laboratoryId'), startAfter(lastsnapshot), limit(amountPerPage));

} else {

this.getcollectionRef(undefined, laboratoryId, currentPage, goalPage, amountPerPage * goalPage);

}

}

const documentSnapshots = collect(this.first);

return documentSnapshots;

}

  

/**

*

* @param lastsnapshot

* @param currentPage

* @param goalPage

* @param amountPerPage

* @returns

*/

getOwnedcollectionRef(lastsnapshot: any, currentPage: any, goalPage: any, amountPerPage: any): Observable<DocumentSnapshot[]> {

return this.scidapService.userProfile$.pipe(

mergeMap((u) => {

let queryRef;

if (lastsnapshot === undefined) {

queryRef = query(collection(this.firestore, 'projects'), where('ownerUID', '==', u.user.uid), orderBy('laboratoryId'), limit(amountPerPage));

} else {

if (goalPage === currentPage + 1) {

queryRef = query(collection(this.firestore, 'projects'), where('ownerUID', '==', u.user.uid), orderBy('laboratoryId'), startAfter(lastsnapshot), limit(amountPerPage));

} else {

return this.getOwnedcollectionRef(undefined, currentPage, goalPage, amountPerPage * goalPage);

}

}

return collect(queryRef);

}),

);

}

  

getOwnedProjectsDocumentCount(): Observable<number> {

return this.scidapService.userProfile$.pipe(

mergeMap((u) => {

const q = query(collection(this.firestore, 'projects'), where('ownerUID', '==', u.user.uid));

return collect(q).pipe(

shareReplay(1),

mergeMap((doc) => {

if (!doc || doc.length === 0) {

return of(0);

}

return of(doc.length);

}),

);

}),

);

}

  

getOtherProjectsDocumentCount(): Observable<number> {

return this.scidapService.userProfile$.pipe(

switchMap((u) => {

const q = query(collection(this.firestore, 'laboratories'), where('ownerUID', '==', u.user.uid));

return from(getDocs(q)).pipe(

switchMap((querySnapshot) => {

const documents = querySnapshot.docs;

if (documents.length > 0) {

const labId = documents[0].id;

const q = query(collection(this.firestore, 'projects'), where('laboratoryId', '==', labId));

return from(getDocs(q)).pipe(

map((querySnapshot) => querySnapshot.size),

catchError(() => of(0)), // Handle any error and return 0

);

} else {

return of(0); // No matching document found

}

}),

);

}),

shareReplay(1),

);

}

}

  

// /**

// * Gets observable of favorites

// */

// private getFavoriteCollection(): Observable<any> { // Favorites collection

// return this.scidapService.userProfile$.pipe(

// mergeMap((u) => {

// // console.log('in get fave coll. user: ', JSON.stringify(u.user));

// //TODO: check how changes in user (tokens, passwords) would retrigger

// const q = query(

// collection(this.firestore, 'favorite'),

// where('type', '==', 'projects'),

// where('userId', '==', u.user.uid)

// );

// //we got a reactive variable that changes all the time there is a change in database

// return collect(q);

// }),

// shareReplay(1) // will work when it's not a function but variable

// )

// }

  

// /**

// * Should get array of favorites from favorite collection with type project

// * Then select those favorites from project collection

// * Should return observable reactive to changes in favorite record

// * @return Observable ...

// */

// getFavoritesProjects(): Observable<any> {

// return this.getFavoriteCollection().pipe(

// mergeMap((doc) => {

// console.log('in getFaveProject. favoriteDoc: ', doc);

// const q = query(

// collection(this.firestore, 'projects'),

// where(documentId(), 'in', doc[0].data()['projects']),

// );

// //we got a reactive variable that changes all the time there is a change in database

// return collect(q);

// })

// )

// }

  

// async getFavocriteProjectsDocumentCount(userId:string) {

// const q = query(

// collection(this.firestore, 'favorite'),

// where('type', '==', 'projects'),

// where('userId', '==', userId)

// );

  

// const querySnapshot = await getDocs(q);

// const documents = querySnapshot.docs;

  

// if (documents.length > 0) {

// const projectsArray = documents[0].data()['projects'];

// const projectsArrayLength = projectsArray.length;

// return projectsArrayLength;

// } else {

// return 0;

// }

// }
```

### 3.2
```
subscribeToShowMore(isOwn: string) {

this.projectService.showMoreProjects.next(this.docOwnedSnap.snapshot);

  

// .pipe(

// mergeMap(() => {

// if (isOwn === 'own') {

// return this.projectService.ownedProjects;

// } else {

// return this.projectService.allOtherProjects;

// }

// }),

// // take(1)

// )

// .subscribe((projects: Project[]) => {

// this.zone.run(() => {

// this.totalAmounts = projects.length;

// this.pageProjects = this.pageProjects.concat(projects);

// console.log('trigged show more own/all', projects);

// });

// });

}
```