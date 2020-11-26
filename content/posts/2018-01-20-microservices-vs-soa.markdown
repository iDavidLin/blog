---
layout: post
title: "Microservices VS SOA: What's the difference"
date: 2018-01-20
categories: [Miscroservices]
description: Micro-service and SOA
tags: [Microservices, architecture]
---
Lately I am reading the book [\<Building Microservices: Designing Fine-Grained Systems 1st Edition
\>](https://www.amazon.com/Building-Microservices-Designing-Fine-Grained-Systems/dp/1491950358), wondering what's the difference between SOA and Microservices.

## 1.SOA

A Service Oriented Architecture is a software architecture pattern, which application components provide services to other components via a communications protocol over a network. The communication can involve either simple data passing or it could involve two or more services coordinating connecting services to each other. Services (such as RESTful Web services) carry out some small functions, such as validating an order, activating account, or providing shopping cart services.

There are 2 main roles in SOA, a service provider and a service consumer. A software agent may play both roles. The Consumer Layer is the point where consumers (human users, other services or third parties) interact with the SOA and Provider Layer consists of all the services defined within the SOA. The following figure shows a quick view of an SOA architecture.

![SOA architecture](/image/SOA-architecture.png){:width="600px"}

Enterprise Service Bus (ESB) is a style of the integration architecture that allows communication via a common communication bus that consists of a variety of point-to-point connections between providers and consumers . In addition to above, the data storage is shared within all services in SOA.

## 2.Microservices

Microservices is a software architecture pattern in which complex applications are composed of small, independent processes communicating with each other using language-agnostic APIs. 

Microservices must be a real need in the system architecture as it could be designed wrongly. It means a service should be independently deployable, or be able to shut-down a service when is not required in the system and that should not have any impact on other services. The following figure shows a quick view of a Microservices architecture.

![Micro-service-architecture](/image/Microservices-architecture.png)

## 3. Differences between SOA and Microservices
<table>
<thead>
<tr>
<th>SOA</th>
<th>Microservices</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align: left;">Built on the idea of “share-as-much-as-possible” architecture approach</td>
<td style="text-align: left;">Built on the idea of “share-as-little-as-possible” architecture approach</td>
</tr>
<tr>
<td style="text-align: left;">More importance on business functionality reuse</td>
<td style="text-align: left;">More importance on the concept of “bounded context”</td>
</tr>
<tr>
<td style="text-align: left;">Common governance and standards</td>
<td style="text-align: left;">Relaxed governance, with more focus on people collaboration and freedom of choice</td>
</tr>
<tr>
<td style="text-align: left;">Uses enterprise service bus (ESB) for communication</td>
<td style="text-align: left;">Uses less elaborate and simple messaging system</td>
</tr>
<tr>
<td style="text-align: left;">Supports multiple message protocols</td>
<td style="text-align: left;">Uses lightweight protocols such as HTTP/REST &amp; AMQP</td>
</tr>
<tr>
<td style="text-align: left;">Common platform for all services deployed to it</td>
<td style="text-align: left;">Application Servers not really used. Platforms such as Node.JS could be used</td>
</tr>
<tr>
<td style="text-align: left;">Multi-threaded with more overheads to handle I/O</td>
<td style="text-align: left;">Single-threaded usually with use of Event Loop features for non-locking I/O handling</td>
</tr>
<tr>
<td style="text-align: left;">Use of containers (Dockers, Linux Containers) less popular</td>
<td style="text-align: left;">Containers work very well in MSA</td>
</tr>
<tr>
<td style="text-align: left;">Maximizes application service reusability</td>
<td style="text-align: left;">More focused on decoupling</td>
</tr>
<tr>
<td style="text-align: left;">Uses traditional relational databases more often</td>
<td style="text-align: left;">Uses modern, non-relational databases</td>
</tr>
<tr>
<td style="text-align: left;">A systematic change requires modifying the monolith</td>
<td style="text-align: left;">A systematic change is to create a new service</td>
</tr>
<tr>
<td style="text-align: left;">DevOps / Continuous Delivery is becoming popular, but not yet mainstream</td>
<td style="text-align: left;">Strong focus on DevOps / Continuous Delivery</td>
</tr>
</tbody>
</table>
<br>  
  
## 4.The differences in more detail:
* Coordination: In SOA, you need to coordinate with multiple groups to create business requests. But there is little or no coordination among services in MSA. If coordination is needed among service owners, it is done through small application development teams, and services can be quickly developed, tested and deployed.
  
* Service granularity: The prefix “micro” in Microservices refers to the granularity of the internal components. Service components within MSA are generally single purpose services that do one thing really well. Services usually include much more business functionality in SOA, and they are often implemented as complete subsystems.

* Component sharing: SOA enhances component sharing, whereas MSA tries to minimize on sharing through “bounded context.” A bounded context refers to the coupling of a component and its data as a single unit with minimal dependencies. As SOA relies on multiple services to fulfill a business request, systems built on SOA are likely to be slower than MSA.

* Middleware vs API layer: The messaging middleware in SOA offers a host of additional capabilities not found in MSA, including mediation and routing, message enhancement, message and protocol transformation. MSA has an API layer between services and service consumers.

* Remote services: SOA architectures rely on messaging (AMQP, MSMQ) and SOAP as primary remote access protocols. Most MSAs rely on two protocols – REST and simple messaging (JMS, MSMQ), and the protocol found in MSA is usually homogeneous.

* Heterogeneous interoperability: SOA promotes the propagation of multiple heterogeneous protocols through its messaging middleware component. MSA attempts to simplify the architecture pattern by reducing the number of choices for integration. If you would like to integrate several systems using different protocols in heterogeneous environment, you need to consider SOA. If all your services could be exposed and accessed through the same remote access protocol, then MSA is a better option.

* Contract decoupling: Contract decoupling is the holy grail of abstraction. It offers the greatest degree of decoupling between services and consumers. It is one of the fundamental capabilities offered within SOA. But MSA doesn’t support contract decoupling.
   
  
Microservices are not invented. Enterprises such as Amazon, Netflix, and eBay used the divide and conquer strategy to functionally partition their monolithic applications into smaller units, and resolved many issues. Following the success of these companies, many other companies started adopting this as a common pattern to refactor their applications. Eventually the pattern was termed as Microservices Architecture. Nothing radically new has been introduced in MSA. MSA is the logical evolution of SOA and supports modern business use cases.


SOA is better suited for large and complex business application environments that require integration with many heterogeneous applications. However, workflow based applications that have a well defined processing flow are a bit difficult to implement using SOA patterns. Small applications are also not a good fit for SOA as they don’t need messaging middleware component. The MSA pattern is well suited for smaller and well partitioned web based systems. The lack of messaging middleware is one of the factors that makes it unfit for complex environments.

If you are developing an application, then Microservices Architecture gives you greater control as a developer. If you are trying to orchestrate a number of business processes, SOA probably provides a better set of tools.

Also in the early stages of your business, you might find that MSA is a good choice. As the business grows, you may need capabilities such as complex request transformation and heterogeneous systems integration. In such situations, you may likely turn to SOA pattern to replace MSA.

Both SOA and MSA are the same set of standards used at different layers of an enterprise. The existence of MSA comes down to the success of SOA pattern. Hence, MSA pattern is a subset of SOA. Here the main focus is on the runtime autonomy of each service.


Reference Links  
<https://www.bmc.com/blogs/microservices-vs-soa-whats-difference/>  
<https://dzone.com/articles/how-containers-microservices-and-devops-are-revolu-1>


Other Resources:  
[Microservices Resource Guide](https://martinfowler.com/microservices/)
