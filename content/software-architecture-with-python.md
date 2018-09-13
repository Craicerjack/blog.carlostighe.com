---
title: Software Architecture With Python
image: 
imageMeta:
  attribution:
  attributionLink:
featured: true
author: carlos
date: Tue Sep 11 2018 13:07:06 GMT+0100 (IST)
tags:
  - programming
  - python
  - architecture
  - packt books
---

# Software Architecture With Python
Notes from the book of the above name by Anand Balachandran Pillai  

## Principles of Software Architecture  

##### Defining Software Architecture
> Software Architecture is a description if the subsystmes or components of a software system, and the relationships between them.  

##### Software Architecture vs Design
> Software Architecture is about the design of the entire system whereas, software design is mostly about the details, typically at the implementation level.  
Not sure I agree with the above.... but...
The distinction that the former is at a much higher abstraction and at a larger scope than the latter.  

##### Aspects of Software Architecture

 * System: a collection of components organised in specific ways to achieve functionality  
 * Structure: set of elements grouped by a principle. 
 * Environment: Context in which a software system is built  
 * Stakeholder: someone who has an interest int he system

##### Characteristics of Software Architecture

 * Defines a structure. 
 * A well defined architecture clearly captures only the core set of structural elements required to build the core functionality of the system 
 * An architecture captures early design decisions  
 * An architecture manages stakeholder requirements  
 * An architecture influences the organisational structure  
 * An architecture is influenced by its environment.  
 * An architecture documents the system  
 * An architecture often conforms to a pattern

##### Why is Software Architecture important?
**Architecture:**  
 * selects quality attributes to be optimised for a system  
     * aspects such as scalability, availabilit, modifiability, security, depend on early decisons.  
     * Early decisions on how to tackle requirements will decide design decisions  
 * facilitates early prototyping  
     * defining how to build a system at the start will speed up the building of that system or parts of that system for protyping.  
 * Architecture allows a system to be built component wise
 * Architecture helps to manages changes to the system  

##### Architectural quality attributes
> "A quality attribute is a measurable and testable property of a system which can
be used to evaluate the performance of a system within its prescribed environment
with respect to its non-functional aspects"  

**QUALITY ATTRIBUTES:**  
 * Modifiability  
     * The ease with which changes can be made  
     * Difficulty - how difficult to make changes  
     * Cost - in terms of time and resources to make the changes  
     * Risks - The risks associated with changing the system  
     * 3 levels of changes - local, non-local, global  
     * Other factors: size of a module, size of team working on it, dependencies
 * Testability  
     * How amenable system is to demonstrating its faults through testing.  
 * Scalability and performance  
     * capacity of a system to increase its workload while keeping performance  
     * Horizontal and Vertical scaling  
     * Performance - response time, latency (how much time it takes to get a request and respond), and Throughput (rate at which a system processes its information)  
 * Availability  
     * property of readiness of a system to carry out its operations when the need arises.  
     * availability closley related to reliability.  
     * RECOVERY - ability to recover from faults  
     * (Mean Time Between Failures) MTBF/ (MTBF + MTTR) (Mean Time To Repair)
     * The above is often called the mission capable rate  
     * fault detection, recovery, and prevention.  
 * Security  
     * users, accounts, access control, and authorization.  
     * Integrity, Origin, Authenticity  
 * Deployability  
     * Module Structures, production vs development environments, ecosystem supoprt, standardized configuration, standardized infrastructure, use of containers.

## Writing Modifiable and Readable Code  

##### Moifiability  
> Modifiability is the degree of ease at which changes can be made to a system, and the flexibility with which the system adpats to such changes.  

 * __Readability__: the ease with which a programs logic can be followed and understood. System should be well-written, well-documented, and well-formatted  
     * __antipatterns__: very few comments or breaking best practices of the language, mixed indentation, mixed string literal types, overuse of functional constructs  
     * __Techniques for readability__:
         * document your code: inline, external docs, and user manuals    
         * function doc strings  
         * Class docstrings  
         * Module docstrings  
         * Use guidelines; PEP8  
         * review and refactor code  
         * Use comments that are helpful, not just repeating the obvious. Avoid inline comments  
 * __Modularity__: written in well encapsualted modules, which do very specific well documented functions  
 * __Reusability__: measures the number of parts of a software system that can be reused in other parts of the system with zero or little modification  
 * __Maintainability__: ease with which the system can be updated and kept working in a useful state  

###### Cohesion & Coupling  
Cohesion - refers to how tightly the responsibilities of a module are related to each other. 
Coupling - how related modules are to each other  
Aim is for high cohesion and low coupling  

__Provide Explicit Interfaces__: 
 * a modules should mark a set of functions as the interface it provides to external code  
 * Methods or fuctions which are internal to it, do not make up its API, should be explicitly made __private__ or should be documented as such   
 * reduce two way dependencies  
 * abstract common services  
 * Using inheritance techniques  
 * Use late binding techniques: plugin mechanisms (setting things at runtime rather than statically), registry lookup services, nontification service, deployment time binding, using creational patterns  

 __TOOLS FOR STATIC ANALYSIS__:  
  * Pylint  
  * Pyflakes  
  * McCabe  
  * Pycodestyle  
  * Flake8  


## Testability Writing Testable Code  

