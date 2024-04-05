
https://notes.dizy.cc/v/devops/

# Devops - 1
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
# DevOps - 2

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


# DevOps - 3 
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


# DevOps - 4

## RESTful API

#### HyperText Transfer Protocol(HTTP)

- URL
- Header
- Body

### what is an API

- **A**pplication **P**rogramming **I**nterface
- A documented way to interact with a program or service
- Defines the **requests** that you can make of the service
- Defines the **data** that you can interchange with the service
- Defines the **results** that will be returned by the service

### What is REST?

- **RE**presentational **S**tate **T**ransfer
    
    - A REST API describes a set of resources
    - A simple way to transfer and manipulate the state of a resource

- A service based on REST is called a RESTful service
- A RESTful service is exposed through a Uniform Resource Locator (URL)
- A client would issue a Hypertext Transfer Protocol (HTTP) request to manipulate it

REST is not a Remote Procedure Call (RPC) or just a bunch of verbs as URI's.

### ==**REST Architecture**==


- REST is a **client-server** architecture: The client and the server provide a separation of concerns which allows both the client and the server to evolve independently as it only requires that the interface stays the same
    
- REST is **stateless**: The communication between the client and the server always contains all the information needed to perform the request. There is no session state in the server.
    
- REST is **cacheable**: The client, the server can cache resources in order to improve performance

- REST provides a **uniform interface** between components: All components follow the same rules to speak to one another

- REST is a **layered system**: Individual components cannot see beyond the immediate layer with which they are interacting
    

### What Does It Mean to Be RESTful?

- Everything is represented as a Resource
- Resource identification through URI (Uniform Resource Identifier), e.g., GET http://myservice.com/users/123
- Uniform interface (I should be able to guess the interface given a resource name)
- Self-descriptive messages are used to represent Resources (usually XML or JSON)
- Stateful interactions through hyperlinks
- A service based on REST is called a RESTful service
    

### What is a Resource?

- The fundamental concept in any RESTful API is the resource
- A resource is an object with a type, associated data, relationships to other resources, and a set of methods that operate on it    
- Only a few standard methods are defined for the resource corresponding to the standard HTTP GET, POST, PUT and DELETE methods
    

### What Does Resource-Based Mean?

- Things vs Actions
- Nouns vs Verbs
- Not a Remote Procedure Call mechanism
- Everything is Identified by URI’s: Multiple URI’s can manipulate the same Resource using different HTTP Verbs
    

### REST Provides a Uniform Interface

- Simplifies and decouples the architecture
- Fundamental to RESTful design is an interface that almost be guessed: Perform CRUD on Resources
- Uses HTTP verbs (POST, GET, PUT, DELETE)
- Uses URL’s to address resources
- Uses HTTP Response (status, body)
    

### Stateless Applications

- Server maintains no client state
- Each request contains enough context to process the message
- Any application state must be held on the client side
- Allows easy horizontal scaling of application services
    

### REST API Conventions
- Use REST API conventions to provide a consistent and easy to use interface for
- REST API conventions define specific behavior for each type of HTTP method. Use the following guidelines as a starting point for designing your API.
    
    - **GET** (read) operations only query data. A GET request should never modify data.
    - **POST** (create) operations create new resource but do not modify existing resources.    
    - **PUT** and **PATCH** (update) operations modify existing resources. (PUT is more common)
    - **DELETE** (delete) operations destroy resources    

**PUT** and **DELETE** operations are idempotent（幂等）, which means they have no further effect when performed multiple times after the first time.

# DevOps - 5
### Cloud Native 云原生 and Microservices

#### Agility: The Three Pillars
DevOps:
- Cultural Change
- Automated Pipeline
- Everything as Code
- Immutable Infrastructure

Microservices:
- Loose Coupling/Binding
- RESTful APIs
- Designed to resist failures
- Test by break / fail fast

Containers:
- Portability
- Developer Centric
- Ecosystem enabler
- Fast startup

## What is Cloud Native?

**Cloud-native is an approach to building and running applications that exploits the advantages of the cloud computing delivery model that are built using multiple, independent microservices.**

DevOps drives the patterns of high performing organizations delivering software faster, consistently and reliably at scale

Leveraging automation to improve human performance in a high trust culture, moving faster and safer with confidence and operational excellence

### Cloud Native Applications

- **The Twelve-Factor App** describes patterns for cloudnative architectures which leverage microservices.
- Applications are designed as a collection of stateless microservices.
- State is maintained in separate databases and persistent object stores.
- Resilience and horizontal scaling is achieved through deploying multiple instances.
- Failing instances are killed and re-spawned, not debugged and patched.
- DevOps pipelines help manage continuous delivery of services
### What are Microservices?

"…the microservice architectural style is an approach to developing a single application as a **suite of small services**, each **running in its own process** and communicating with lightweight mechanisms, often an HTTP resource API. These services are **built around business capabilities** and **independently deployable** by fully automated deployment machinery."

by Martin Fowler and James Lewis

### Microservice Architecture

An architecture style aimed to achieve flexibility, resiliency and control, based on the following principles:

- **Single purpose Loose Coupling bounded context**
- Independent life cycle: developed, deployed and scaled... and hopefully, fail independently
- Design for resiliency and owns it’s own data
- Polyglot — independent code base
- Built by autonomous teams with end-to-end responsibility, doing Continuous Delivery
- Communicates with other services over a well defined API
    

### Advantages of Microservices

- Developed by a single team
- Developed independently
- Developed on its own timetable
- Each can be developed in a different language
- Manages its own data
- Scales and fails independently
    

### Microservice Challenges

- Developers must have significant operational and development skills (DevOps / Multiple languages)
- Service interfaces and versions
- Duplication of effort across service implementations
- Extra complexity of creating a distributed system with these issues, among others:
    - Network latency
    - Fault tolerance
    - Serialization
- Designing decoupled non transactional systems is difficult
- Avoiding latency of large numbers of small service invocations
- Locating service instances
- Maintaining availability and consistency with partitioned data
- End-to-end automated testing
    

## Monolithic vs Microservice

### Monolithic Application Deployment

- Loosely coupled
- Minimal responsibility per service
- Small Deployment units
- Easy to Scale
- Short release cycles
- Fast on-boarding for new developers
- Develop quickly with fast feedback
### Microservice Application Deployment

- Cloud Native Model
    - Multiple microservices
    - Configuration: Automated and consistent
    - Changes: Performed in DevOps Pipeline
    - Deployment: Only what changes

- Advantages for operations
    - Resiliency through redundant services
    - Consistent configuration
    - Automated massive deployment
    
### ==Example Microservice Stereotypes==

- **Data services**: Responsible solely for the storage and retrieval of data associated with a single microservice
    
- **Orchestration services**: Communicate with multiple data services, either to store data associated with multiple microservice, or to read that data back and compose it into larger data structures

- **Backends-for-frontends** (**API Gateway**): Single entry point for all clients. May simply proxy/route to the appropriate service, or fan out to multiple services

- **Message bus consumers**: Consume and process messages from message buses such as Kafka

###  Microservice Design Enables Horizontal Scaling

**Vertical Scaling**: Get bigger servers

**Horizontal Scaling**: Get bigger servers

### Monolithic vs Microservices Architectures

|Category|Monolithic Architecture|Microservices architecture|
|---|---|---|
|Architecture|Built as a single logical executable|Built as a suite of small services|
|Modularity|Based on language features|Based on business capabilities|
|Agility|Changes to the system involve building and deploying a new version of the entire application|Changes can be applied to each service independently|
|Scaling|Entire application scaled when only one part is the bottleneck|Each service scaled independently when needed|
|Implementation|Typically entirely developed in one programming language|Each service can be developed in a different programming language|
|Maintainability|Large code base is intimidating to new developers|Smaller code bases easier to manage|
|Deployment|Complex deployments with maintenance windows and scheduled downtimes|Simple deployment as each service can be deployed individually, with minimal if not zero downtime|

## What Does A Microservice Should Have?

- **High Cohesion** (Bounded Context around a Business Domain): Does stuff that needs to change together occur together?
- **Low Coupling** (Shared Nothing with Technology Agnostic API): Do you avoid making otherwise independent concerns dependent?
- **Low Time to Comprehension** (Small and Single Responsibility): Small enough for one person to understand quickly
    

## What Does A GOOD Microservice Should Have?

- Microservices should have minimal outside dependancies
- Business Domains usually have well established boundaries
- Microservices should be broken up by Business Domains
    - With well defined interface
    - Limiting dependancies as much as possible

## Domain Driven Design

- DDD is about designing software based on models of the underlying domain
- ==**Bounded Context** is a central pattern in Domain-Driven Design==
- DDD deals with large models by dividing them into different Bounded Contexts and being explicit about their interrelationships.
    

## Microservice Designs Must:

- Design for failure
- Move from:
    - How to avoid —> How to identify & what to do about it
    - Pure operational concern —> developer concern
- Plan to be throttled
- Plan to retry (with exponential backoff)
- Degrade gracefully
- Cache when appropriate

### Retry Pattern

- Enable an application to handle transient failures when it tries to connect to a service or network resource, by transparently retrying a failed operation.
    

- **Exponentially back-off** delaying longer with each retry
    

### Circuit Breaker Pattern

- You wrap a protected function call in a circuit breaker object, which monitors for failures.
    

- Once the failures reach a certain threshold, the circuit breaker trips, and all further calls to the circuit breaker return with an error, without the protected call being made at all.
    

- Usually you'll also want some kind of monitor alert if the circuit breaker trips.
    

### Bulkhead Pattern 

- Isolates consumers and services from cascading failures: An issue affecting a consumer or service can be isolated within its own bulkhead, preventing the entire solution from failing.

- This pattern is named Bulkhead because it resembles the sectioned partitions of a ship’s hull: If the hull of a ship is compromised, only the damaged section fills with water, which prevents the ship from sinking.
    
- Allows you to preserve some functionality in the event of a service failure. Other services and features of the application will continue to work.

舱壁图案
- 将消费者和服务与级联故障隔离：影响消费者或服务的问题可以隔离在其自己的舱壁内，从而防止整个解决方案失败。
- 这种模式被称为舱壁，因为它类似于船体的分段隔板：如果船体受到损害，只有损坏的部分充满水，从而防止船沉没。
- 允许您在服务发生故障时保留某些功能。该应用程序的其他服务和功能将继续有效

## Canary Testing 金丝雀测试

- Mitigates the risks of changes to applications in production 
    
- **Features are activated only for a small percentage of users,** and the application performance and adoption results are measured
    
    - If those results indicate that the change is good, then it is ramped up to the rest of the user population
    - If the change is not good, it is rolled back
        

## ==A/B Testing==

- Some set of users are directed to one implementation of a feature, let’s call it the A version, while a different set of users are directed to a different implementation of the feature, let’s call that the B version

- This allows DevOps teams to evaluate different implementation options for a feature, and pick the one that works the best in the field, by measuring actual usage
    
- The data from usage analytics is then used to influence the priorities of the remaining stories in the backlog.
    

## Feature Flags

- With Continuous Delivery, code can be tested and delivered into production with “Feature Flags” around the new code
    
- Using these techniques, those features can be made visible to specific audiences to allow testing of those features in a production environment
    
- The act of going Live can happen via a Release Event on a later date when the Feature Flags are turned on in a coordinated way across multiple components, and the new feature is made publicly visible.
    

## The Twelve-Factor App


The twelve-factor app is a methodology for building software-as-a-service apps that:

- Use **declarative** formats for setup automation, to minimize time and cost for new developers joining the project;
    

- Have a **clean contract** with the underlying operating system, offering **maximum portability** between execution environments;
    

- Are suitable for **deployment** on modern **cloud platforms**, obviating the need for servers and systems administration;
    

- **Minimize divergence** between development and production, enabling **continuous** deployment for maximum agility;
    

- And can **scale up** without significant changes to tooling, architecture, or development practices
    

### I. Codebase

One codebase tracked in revision control, many deploys

- There is always a one-to-one correlation between the codebase and the app
    

- If there are multiple codebases, it’s not an app – it’s a distributed system: Each component in a distributed system is an app, and each can individually comply with twelvefactor.
    

- Multiple apps sharing the same code is a violation of twelve-factor: The solution here is to factor shared code into libraries which can be included through the dependency manager.
    

### II. Dependencies

Explicitly declare and isolate dependencies

- Most programming languages offer a packaging system for distributing support libraries, such as Rubygems for Ruby, or PyPi for Python, or Maven for Java: Libraries installed through a packaging system can be installed system-wide (known as “site packages”) or scoped into the directory containing the app (known as “vendoring” or “bundling”)
    

- **A twelve-factor app never relies on implicit existence of system-wide packages**
    
    - It declares all dependencies, completely and exactly, via a dependency declaration manifest
        
    
    - Furthermore, it uses a dependency isolation tool during execution to ensure that no implicit dependencies “leak in” from the surrounding system. The full and explicit dependency specification is applied uniformly to both production and development
        
    

### III. Config Store config in the environment


- An app’s config is everything that is likely to vary between deploys (staging, production, developer environments, etc). This includes:
    
    - Resource handles to the database, Memcached, and other backing services
        
    
    - Credentials to external services such as Amazon S3 or Twitter
        
    
    - Per-deploy values such as the canonical hostname for the deploy
        
- Apps sometimes store config as constants in the code. This is a violation of twelve-factor, which **requires strict separation of config from code**. Config varies substantially across deploys, code does not.
    

### IV. Backing services

[](https://notes.dizy.cc/v/devops/cloud-native-and-microservices#iv.-backing-services)

Treat backing services as attached resources

- A backing service is any service the app consumes over the network as part of its normal operation
    

- **The code for a twelve-factor app makes no distinction between local and third party services**
    
    - To the app, both are attached resources, accessed via a URL or other locator/credentials stored in the config
        
    
    - A deploy of the twelve-factor app should be able to swap out a local MySQL database with one managed by a third party (such as Amazon RDS) without any changes to the app’s code
        
    

### V. Build, release, run

Strictly separate build and run stages A codebase is transformed into a (non-development) deploy through three stages:

- The **build** stage is a transform which converts a code repo into an executable bundle known as a build.
    

- The **release** stage takes the build produced by the build stage and combines it with the deploy’s current config.
    

- The **run** stage (also known as “runtime”) runs the app in the execution environment, by launching some set of the app’s processes against a selected release
    

The twelve-factor app uses strict separation between the build, release, and run stages: For example, it is impossible to make changes to the code at runtime, since there is no way to propagate those changes back to the build stage.

### VI. Processes


Execute the app as one or more stateless processes

- The app is executed in the execution environment as one or more processes
    

- In the simplest case, the code is a stand-alone script, the execution environment is a developer’s local laptop with an installed language runtime, and the process is launched via the command line (for example, python my_script.py)
    

- On the other end of the spectrum, a production deploy of a sophisticated app may use many process types, instantiated into zero or more running processes
    

- **Twelve-factor processes are stateless and share-nothing**: Any data that needs to persist must be stored in a stateful backing service, typically a database
    

### VII. Port binding

Export services via port binding

- **The twelve-factor app is completely self-contained** and does not rely on runtime injection of a webserver into the execution environment to create a web-facing service
    

- The web app **exports HTTP as a service by binding to a port**, and listening to requests coming in on that port.
    

- In a local development environment, the developer visits a service URL like http:// localhost:5000/ to access the service exported by their app
    

- In deployment, a routing layer handles routing requests from a public-facing hostname to the port-bound web processes.
    

###  VIII. Concurrency


Scale out via the process model

- **In the twelve-factor app, processes are a first class citizen**
    

- Processes in the twelve-factor app take strong cues from the unix process model for running service daemons
    

- Using this model, the developer can architect their app to handle diverse workloads by assigning each type of work to a process type: For example, HTTP requests may be handled by a web process, and long-running background tasks handled by a worker process
    

### IX. Disposability

Maximize robustness with fast startup and graceful shutdown

- **The twelve-factor app’s processes are disposable, meaning they can be started or stopped at a moment’s notice**
    

- This facilitates fast elastic scaling, rapid deployment of code or config changes, and robustness of production deploys
    
    - Processes should strive to minimize startup time
        
    
    - Ideally, a process takes a few seconds from the time the launch command is executed until the process is up and ready to receive requests or jobs
        
    

- Processes shut down gracefully when they receive a SIGTERM signal from the process manager.
    
    - For a web process, graceful shutdown is achieved by ceasing to listen on the service port (thereby refusing any new requests), allowing any current requests to finish, and then exiting.
        
    

### X. Dev/prod parity

Keep development, staging, and production as similar as possible

Historically, there have been substantial gaps between development (a developer making live edits to a local deploy of the app) and production (a running deploy of the app accessed by end users). These gaps manifest in three areas:

- The **time gap**: A developer may work on code that takes days, weeks, or even months to go into production.
    

- The **personnel gap**: Developers write code, ops engineers deploy it.
    

- The **tools gap**: Developers may be using a stack like Nginx, SQLite, and OS X, while the production deploy uses Apache, MySQL, and Linux.
    

The twelve-factor app is designed for continuous deployment by keeping the gap between development and production small. Looking at the three gaps described on the previous chart:

- Make the **time gap** small: a developer may write code and have it deployed hours or even just minutes later.
    

- Make the **personnel gap** small: developers who wrote code are closely involved in deploying it and watching its behavior in production.
    

- Make the **tools gap** small: keep development and production as similar as possible
    

### XI. Logs

Treat logs as event streams

Logs provide visibility into the behavior of a running app. In server-based environments they are commonly written to a file on disk (a “logfile”); but this is only an output format.

**A twelve-factor app never concerns itself with routing or storage of its output stream**

- It should not attempt to write to or manage logfiles

- Instead, each running process writes its event stream, unbuffered, to stdout
    

- During local development, the developer will view this stream in the foreground of their terminal to observe the app’s behavior
    

### XII. Admin processes

Run admin/management tasks as one-off processes

**One-off admin processes should be run in an identical environment as the regular long-running processes of the app**, such as:

- Running database migrations (e.g. manage.py migrate in Django, rake db:migrate in Rails).
    

- Running a console (also known as a REPL shell) to run arbitrary code or inspect the app’s models against the live database.
    

- Running one-time scripts committed into the app’s repo (e.g. php scripts/ fix_bad_records.php)
    

They run against a release, using the same codebase and config as any process run against that release. Admin code must ship with application code to avoid synchronization issues

[

Previous

RESTful APIs



](https://notes.dizy.cc/v/devops/restful-apis)[

Next

Test Driven Development

](https://notes.dizy.cc/v/devops/test-driven-development)

Last modified 2yr ago

WAS THIS PAGE HELPFUL?

![](chrome-extension://ofpnmcalabcbjgholdjcjblkibolbppb/static/global/src/static/monicaLogo.png)⌘M


# DevOps 6
## Test driven development

If it's worth building, it's worth testing
## Software Testing Levels
### Acceptance Testing
A level of the software testing process where a system is tested for acceptability. The purpose of this test is to evaluate the system’s compliance with the business requirements and assess whether it is acceptable for delivery.

### System Testing
A level of the software testing process where a complete, integrated system/software is tested. The purpose of this test is to evaluate the system’s compliance with the specified requirements.

### Integration Testing
A level of the software testing process where individual units are combined and tested as a group. The purpose of this level of testing is to expose faults in the interaction between integrated units.
### Unit Testing
A level of the software testing process where individual units/ components of a software/system are tested. The purpose is to validate that each unit of the software performs as designed.

## DBB & TDD

Behavior-Driven Development (BDD)

- Describes the behavior of the system from the outside in
- Used for Integration / Acceptance Testing
    

Test Driven Development (TDD)

- Tests the functions of the system from the inside out
- Used for unit testing
    

### TDD Workflow

Cycle: ... -> RED -> GREEN -> REFACTOR -> ...

- Write a test case and watch it FAIL
- Write the code to make it PASS
- REFACTOR the code to make it great knowing that the test case will let you know if you broke anything
    

### BDD & TDD Cycle

![](https://209070276-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FIHriSm1GS8HhlboZIaAd%2Fuploads%2Fgit-blob-537a2b5e71e8ea50a23de4fbdcc997b85a9b3e0c%2Ftdd-bdd.png?alt=media)

BDD & TDD

"BDD is building the right thing, and TDD is building the thing right."

## What is TDD?

- Test Driven Development means that your test cases drive the design and development of your code
    
- You write the tests first for the code you wish you had, then you write the code to make the test pass

- This keeps you focused on the purpose of the code (i.e., what is it supposed to do)
    

### Why is automated Testing Important to DevOps?


- First and foremost it saves time when developing!
- It allows you to run faster because you are more confident
- It insures that your code is working as you expected
- It insures that future changes don’t break your code
- In order to use a DevOps Pipeline, all testing must be automated
### Kent Beck says Good Unit tests...

- Run fast (they have short setups, run times, and break downs).
- Run in isolation (you should be able to reorder them).
- Use data that makes them easy to read and to understand.
- Use real data (e.g. copies of production data) when they need to.
- Represent one step towards your overall goal.
    

### The Basic TDD Workflow

- Write a failing unit test for the code you wish you had
- Write just enough code to make the unit test pass
- Refactor the code and repeat
    
## Test Fixtures

A test fixture is a fixed state of a set of objects used as a baseline for running tests.

The purpose of a test fixture is to ensure that there is a well known and fixed environment in which tests are run so that results are repeatable.

Examples of fixtures:

- Preparation of input data and setup/creation of fake or mock objects
- Loading a database with a specific, known set of data
- Copying a specific known set of files creating a test fixture will create a set of objects initialized to certain states.
    

### Unittest Fixtures
```
def setUpModule(): # runs once before any tests

pass

def tearDownModule(): # runs once after all tests

pass

​

class MyTestCases(TestCase):

@classmethod

def setUpClass(cls): # runs once before test class

pass

​

@classmethod

def tearDownClass(cls): # runs once after test class

pass

​

def setUp(self): #runs before each tests

pass

​

def tearDown(self): # runs after each tests

pass

```

``
## 

Mocking

[](https://notes.dizy.cc/v/devops/test-driven-development#mocking)

- Mocking creates fake objects that behave like the real thing
    

- Any external service that is not under test should be Mocked
    

- Sometimes you need to change the behavior of a dependent system under test
    

- Maybe you don’t have a remote connection to another component
    

- Or you want to isolate your tests from a remote component
    

### Methods of Mocking


- **Patch** This patches a function call allowing you to change it’s behavior
- **MagicMock**: This mocks an entire object changing it’s behavior. Usually used as a return value
    

## Factories and Fakes

Sometimes you will need fake data to test against, sometimes you will want an entire class to be fake data, Factories and Fakes make this possible. We will use Factory Boy in Python for this.


# DevOps 7 - Platform as a Service