# Building Microservices - Desinging Fine-Grained Systems - 2nd edition

## Chapter 1 - What are Microservices 

### Key takeaways 

#### **Microservices**

Microservices are small independatly deployable pieces of software centered around a business domain. It's like a black box that handles a single piece of functionality. 

Repeated mentions of information hiding, (hiding as much information as possible and exposing as little via external interfaces p4). The benefit being the internal implementation is more free to change as long as the exposed interfaces don't change in a backwards incompatible way. 

Question - In Asynchronous communication methods the idea is generally to share all information and allow consumers to decide what they need, are these two ideas exclusive? 

Core things all microservices should do/have:
- Independant deployability
- Modelled around a business domain
- Owning their own state
- Size (as small an interface as possible? p9)
- Flexible to change
- Alignment of architecture and organization (temas should be vertical instead of horizontal i.e. own the entire stack of their domain)

Great quote from Conways law- "Organizations which design systems are constrained to produce designs which are copies of the communication structure within an organization" 

#### **The Monolith**

Single process monolith

- Code is deployed as a single process, usually one database the classic monolith.

Modular Monolith

- Code within this single process monolith is divided into modules 
- Challenges is that databases/tables lack the decomposition found at the code level causing issues if you want to pull it apart in the future

Distributed Monolith

- A system which comprises of multiple services but it must all be deployed together

Advantages of a monolithic architecture
- Simpler workflows, deployment, monitoring and troubleshooting your concern is only one service
- Quicker to get started
- Easier to build when service boundaries and ownership isn't clear (think startup)

Advantages of a microservices architecture
- Technology heterogeneity - (use the best tool for the specific job, not really practiced or needed in most places)
- Robustness - A single failure doesn't (shouldn't) cascade
- Scaling - You can scale specific services which need resources rather than scaling an entire monolith because of one hungry package
- Ease of deployment - Changing are smaller one line code changes aren't as scary since you're not redploying the entire service
- Organizational Alignment - Ownership can change as the business organization shifts, smaller teams on smaller codebases tend to be more productive
- Composibility - Opens the door for reuse of functionality in different ways for different consumers (think of seams that can be addressed individually rather than one big stream)

Disadvantages of a microservices architecture
- DevEx can suffer - can you run 20 microservices in one machine? Probably not, would you need to? Probably not.
- Technology overload - the choice now sits with the team (or should) on what tool to use, the burden of choice can mean we end up choosing technology we're comfortable with rather than what best fits the need and vice versa; we might introduce new technology because we think we need to. Do you need a K8 cluster for 2 services?
- Cost - Microservices cost more and slow teams down in the short term, the benefit is in being able to go to market quicker with new revenue generating features. A company focussed on saving costs probably won't benefit from transitioning architectures. 
- Reporting - Before we had a single database and can just join accross the tables for the data we need, now we need a way to injest the data from sometimes 100s of services, usually achieved using streaming technologies. 
- Monitoring and troubleshooting - Every new service needs to be monitored and production ready, now it can take multiple people with domain expertise to troubleshoot an issue which could have been done by one person in a monolithic architecture. 
- Security - How are you keeping track of calls to external APIs the licences all your services use with everything flowing over the network MITM attacks can become a bigger concern. 
- Testing - E2E testing has diminshing returns yet is still regularly employed as a way to test microservices, the education on testing microservices isn't where it was for the very well understood monolith. The idea of testing and deployment requires a different mindset for microservices.
- Latency - With communication all being over network now you're introducing network complexity, in reality if everything is deployed in the same k8 cluster there shouldn't be noticible latency 
- Data consistency - Multiple services own and maintain their own data so reasoning about the overall state becomes more of a challenge. You can use techniques like Sagas or eventual consistency to get past this. 

Should I use Microservices? 

- Probably not if you're a small company/startup focus on your proof of concept, microservices shine when you want more developers to work together without getting in eachothers way. Here is where microservices shine, going from a start-up to a scale-up. Ensure the increase in complexity is warranted. 
