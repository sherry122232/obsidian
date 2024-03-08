
https://notes.dizy.cc/v/devops/

## Devops - 1
### DevOps Thinking / Tenets

- Social Coding
- Behavior and Test Driven Development
- Working in small batches
- Build **Minimum Viable Products** for gaining insights
- Failure leads to understanding

### Think Cloud Native

- The Twelve-Factor App describes patterns for cloud-native architectures which leverage microservices
- Applications are design as a collection of stateless microservices
- State is maintained in separate databases and persistent object stores
- Resilience and horizontal scaling is achieved through deploying multiple instances
- Failing instances are killed and re-spawned, not debugged and patched (cattle not pets)
- DevOps pipelines help manage continuous delivery of services

###  Design for Failure

- Embrace failures: they will happen! Move from "How to avoid" —> "How to identify & what to do about it". Move from "Pure operational concern" —> "developer concern".
- External calls to other services that you don’t control are especially prone to problems:
    - Use separate thread pools
    - Time out quickly
- Circuit breaker pattern: identify problem and do something about it to avoid cascading failures
- Bulkhead pattern: Isolation from start to limit scope of failure (separate thread pools)
- Monkey testing: test by breaking (yes, on purpose! see: Netflix Chaos Monkey and Simian Army)

### Working DevOps

- Facilitate a culture of **teaming and collaboration**
- Establish **agile development** as a shared discipline
- **Automate relentlessly** to enable rapid DevOps response
- Push **smaller releases faster**, measure and remediate impact

### Immutable Delivery

- Applications are packaged in containers
- Same container that developer runs on their laptop runs in production
- Rolling updates with immediate roll-back
- No variance limits side-effects
- Dependencies are contained

### Zero-Downtime Deployment

- Blue-green deployment is a zero-downtime deployment technique that consists of two nearly identical production environments, called Blue and Green.
    

- They differ by the artifacts that the developer has intentionally changed, typically by the version of the application. At any given time, at least one of the environments is active.
    

- Using the blue-green deployment technique, you can realize the following benefits:
    
    - Take software quickly from the final stage of testing to live production.
    - Deploy a new version of an application without disrupting traffic to the application.
    - Rollback rapidly. If there is something wrong with one of your environments, you can quickly switch to the other environment.

### DevOps Measurement / Metrics


DevOps changes the objective of the measurement from Mean Time To Failure (MTTF, make sure you never go down) -> Mean Time To Recovery (MTTR, you will go down, make sure you can recover quickly)

Metrics:

- A **BASELINE** provides a concrete number for comparison as you implement your DevOps changes:
    
    - It currently requires six team members 10 hours to deploy a new release of our product.
    - This costs us $X for every release

- Metric **GOALS** allow you to reason about these numbers and judge the success of your transition process:
    
    - Reduce deployment time from 10 hours to 2 hours.
    - Increase percentage of defects detected in testing from 25% to 50%

Top 4 actionable metric:
	- mean lead time
	- release frequency
	- change failure rate
	- mean time to recovery
## DevOps - 2

Source code management - SCM
Version Control Systems (VCS)

Git： Decentralized SCM system
![[Pasted image 20240306223509.png]]
### Detailed Feature Branch Workflow

- CLONE a Repository (FORK first if not part of Dev Team)
- Assign the ISSUE for your work to yourself and place it in working status
- Create a BRANCH to work on an ISSUE
- Run the Test suite to make sure you can run the code
- Make changes to code and test cases and COMMIT to local BRANCH
- Run the Test suite early and often to make sure you didn’t break anything
- PUSH changes to remote BRANCH
- Did we mention testing the code early and often?
- Create PULL REQUEST when all tests pass and code is ready for review / MERGE
    

### Why is Testing So Important?

- Automated testing must pass before your Pull Request will be accepted
- Automated testing is your guarantee that you didn’t break anything
- Without automated testing you cannot fully automate the DevOps pipeline

### Branches
- Branching is a core concept in Git: Branching is a core concept in Git
- The only rule: Anything in the **master**/**main** branch must always be deployable
- It's extremely important that your new branch is created off of master when working on a feature or a fix


### Fetch vs Pull

- ==Fetch== will bring down all of the changes from the remote repository

- ==Pull== will merge the changes from the current branch with your local workspace

Note: Pull does a fetch so if you just want to pull there is no need to fetch.


### Merge vs Rebase

**==Merge==** joins two branches together, usually your branch and master but it can be any two branches only changing the checked out branch. If there are no conflicts and the current HEAD is an ancestor of the merge branch, git will fast-forward the merge by moving the pointer forward. Merge retains all the history as it happened chronologically

**==Rebase==** will replay your changes on top of the current version of master. It will look as if your branch was created from the current state of master. It will look as if your branch was created from the current state of master. You can optionally do this before pushing/creating to remote branch otherwise use merge. ==**Never rebase once you have pushed to a remote**.== It will mess everyone else up because it changes history in a way that is incompatible.


### Reset vs Revert

if you haven't push ->
To get rid of the last two commits
` git reset --soft HEAD~2`
` git reset --hard master@{1}`

- `--soft` will undo the commit history and leave the files staged
- `--mixed` will undo the history and the staging so the files are untracked (default)
- `--hard` will undo and **delete** your files!

if you have pushed, you want to undo it.
` git revert <sha1>`

Revert is the only **safe** undo for a commit that has a remote push.
Note: revert will not remove files that are pushed remotely.

### Comparison

**Reset** will alter history as if it never existed. This will confuse remote repos so once you push a commit you should not reset it.

**Revert** will undo history by adding a commit that reverses the changes. This is remote repo friendly.

### Merge Conflicts


Git cannot merge code that has the **same line** of code changed in two **different branches**. This requires **manual intervention** and probably collaboration with the developer who made the other changes.

#### Resolution

For pull requests, you should merge from the master branch first. If there were conflicts, they would appear in the current branch.

- Edit the file in conflict and commit. (If is during a rebase, you should `git rebase --continue`).
    
git commit -am "Fix: Resolve conflicts"

- Then you can proceed to merge the pull requests into the master branch.
    

### Abort a Merge or Rebase


Never leave a merge or rebase in an unfinished state!

- For merge, you can abort it with: `git merge --abort`
- For rebase, you can abort it with: `git rebase --abort`


## DevOps - 3 
### Agile Planning

Agile and Scrum

**Scrum** is the most popular Agile development **framework**.

- **Agile** is a PHILOSOPHY for doing work, not prescriptive.
- **Scrum** is a METHODOLOGY for doing work that adds PROCESS to Agile thinking


### Organization of Scrum Teams
- Small team (7 ± 2)
- Dedicated
- Co-located
- Cross-functional
- Self managing

### Bad Formulas Leading to Failure

- Product Manager becomes Product Owner
- Project Manager becomes Scrum Master
- Developers become Scrum Team

### Agile Tenets

Agile takes ideas from Lean Manufacturing and Extreme Programming (XP)

- Working in Small Batches
- Creating Minimum Viable Products (MVP)
- Using Behavior Driven Design (BDD) to make sure that you are building the right
- Practicing Test Driven Development (TDD) to make sure that you are building the thing right
- Pair Programming to improve code quality and knowledge saturation
    

### Minimum Viable Product

- MVP is NOT the result of "Phase 1" of a project
- It IS the cheapest/easiest thing you can build to start testing your **value hypothesis** and **learning**
- The former focuses on delivery, while the latter focuses on learning
- At the end of each MVP you decide whether to pivot or persevere


### Actionable Metric Examples

- Reduce time-to-market for new features.
- Increase overall availability of the product.
- Reduce the time it takes to deploy a software release.
- Increase the percentage of defects detected in testing before production release.
- Make more efficient use of hardware infrastructure.
- Provide performance and user feedback to the product manager in a more timely manner.

![[Pasted image 20240307224911.png]]
![[Pasted image 20240307224933.png]]
### Grooming the Backlog

- Make sure that all Issues are groomed and stories are complete
- Keep the Backlog ranked by priority so that the important Issues are always on top: The priority is determined by the "**So that**" benefit statement
- Size the Issues if possible or leave to Sprint Planning


### Hypothesis Driven Development

Hypotheses pair a statement that asserts or predicts value with a testable condition that can be measured.

The typical form is as follows  : 

`we believe that function
`will lead to outcome`
`and this will be proven when <measureable condition>`


### Story Driven Development

- User Stories document a persona requesting a function to achieve a goal
- The typical form is as follows:

`As a <some role>`

`I need <some function>`

`So that <I get some benefit>

- User Stories can be entered into GitHub as **Issues**