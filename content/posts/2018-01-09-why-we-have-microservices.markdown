---
layout: post
title:  "Why we have micro-services"
date:   2018-01-09
categories: Microservice 
description: Yes, micro-services
tags: [microservice]
---

Traditionally, software developers created large, monolithic applications which will encompass all the business activities. As the requirements of the application grew, so did the monolith.

#### Problem 1: Hard to maintain and scale.
In this model, implementing an improved piece of business functionality required developers to make changes within the single application, often with many other developers attempting to make changes to the same single application at the same time. In that environment, developers could easily step on each other’s toes and make conflicting changes that resulted in problems and outages.

Dealing with monolithic applications often caused development organizations to get stuck in the muck, resulting in slower, less-reliable applications and longer and longer development schedules. The companies who create those applications, as a result, end up losing customers and money.

#### Problem 2: Hard for troubleshooting
Codebases grow as we write code to add new features. Over time, it can be difficult to know where a change needs to be made because the codebase is so large. Despite a drive for clear, modular monolithic codebases, all too often these arbitrary in-process boundaries break down. Code related to similar functions starts to become spread all over, making fixing bugs or implementations more difficult.

#### Problem 3: Hard to update/adopting to some new technology.
One of the biggest barriers to trying out and adopting new technology is the risks associated with it. With a monolithic application, if you want to try a new programming language, database, library or framework, any change will impact a large amount of your system.

The muck is not inevitable. You can rebuild and re-architect your applications to scale with your company’s needs, not against it. Using a microservice-based application architecture is an increasingly popular technique for building applications that can scale without miring your organization in the monolithic muck.


------
  
## The benefit of microservices

#### 1. Small, and Focused on Doing One Thing Well 
As the Single Responsibility Principle — “Gather together those things that change for thesame reason, and separate those things that change for different reasons.” Microservices take this approach to independent services. Microservices focus on boundaries on business boundaries, making it obvious where code lives for a given piece of functionality. And by keeping this service focused on an explicit boundary, we avoid the temptation for it grow too large.

#### 2. Autonomous  
All the services are separate entities. They might be deployed as an isolated services on a platform as a service (PAAS), or it might be its own operating system process. These services are (or need to be) able to change independently of each other, and be deployed by themselves without requiring consumers to change.

The golden rule: can you make achange to a service and deploy it by itself without changing anything else? If the answer isno, then many of the advantages we discuss throughout this book will be hard for you toachieve.

#### 3. Technology Heterogeneity  
Can use different technologies in different services which are better to achieve the performance levels required.

#### 4. Resilience
A key concept in resilience engineering is the bulkhead. If one component of a systemfails, but that failure doesn’t cascade, you can isolate the problem and the rest of thesystem can carry on working. Service boundaries become your obvious bulkheads. In amonolithic service, if the service fails, everything stops working. With a monolithicsystem, we can run on multiple machines to reduce our chance of failure, but withmicroservices, we can build systems that handle the total failure of services and degradefunctionality accordingly.

#### 5. Scaling
With a large, monolithic service, we have to scale everything together. One small part ofour overall system is constrained in performance, but if that behavior is locked up in agiant monolithic application, we have to handle scaling everything as a piece. Withsmaller services, we can just scale those services that need scaling, allowing us to runother parts of the system on smaller, less powerful hardware

#### 6. Ease of Deployment
A one-line change to a million-line-long monolithic application requires the wholeapplication to be deployed in order to release the change. That could be a large-impact,high-risk deployment. In practice, large-impact, high-risk deployments end up happeninginfrequently due to understandable fear. Unfortunately, this means that our changes buildup and build up between releases, until the new version of our application hittingproduction has masses of changes. And the bigger the delta between releases, the higherthe risk that we’ll get something wrong!

With microservices, we can make a change to a single service and deploy it independently of the rest of the system. This allows us to get our code deployed faster. If a problem does occur, it can be isolated quickly to an individual service, making fast rollback easy to achieve. It also means we can get our new functionality out to customers faster. This isone of the main reasons why organizations like Amazon and Netflix use thesearchitectures — to ensure they remove as many impediments as possible to getting software out the door.

#### 7. Organizational Alignment
Many of us have experienced the problems associated with large teams and largecodebases. These problems can be exacerbated when the team is distributed. We alsoknow that smaller teams working on smaller codebases tend to be more productive.
Microservices allow us to better align our architecture to our organization, helping usminimize the number of people working on any one codebase to hit the sweet spot of teamsize and productivity. We can also shift ownership of services between teams to try to keeppeople working on one service colocated. 

#### 8. Composability
One of the key promises of distributed systems and service-oriented architectures is thatwe open up opportunities for reuse of functionality. With microservices, we allow for ourfunctionality to be consumed in different ways for different purposes. This can beespecially important when we think about how our consumers use our software. Gone isthe time when we could think narrowly about either our desktop website or mobileapplication. Now we need to think of the myriad ways that we might want to weavetogether capabilities for the Web, native application, mobile web, tablet app, or wearabledevice. As organizations move away from thinking in terms of narrow channels to moreholistic concepts of customer engagement, we need architectures that can keep up.

With microservices, think of us opening up seams in our system that are addressable byoutside parties. As circumstances change, we can build things in different ways. With amonolithic application, I often have one coarse-grained seam that can be used from theoutside. If I want to break that up to get something more useful, I’ll need a hammer!

#### 9. Optimizing for Replaceability
If you work at a medium-size or bigger organization, chances are you are aware of somebig, nasty legacy system sitting in the corner. The one no one wants to touch. The one thatis vital to how your company runs, but that happens to be written in some odd Fortranvariant and runs only on hardware that reached end of life 25 years ago. Why hasn’t itbeen replaced? You know why: it’s too big and risky a job.

With our individual services being small in size, the cost to replace them with a betterimplementation, or even delete them altogether, is much easier to manage. How often haveyou deleted more than a hundred lines of code in a single day and not worried too muchabout it? With microservices often being of similar size, the barriers to rewriting orremoving services entirely are very low.
