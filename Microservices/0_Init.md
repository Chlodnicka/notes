# Init

## Sources

1. https://martinfowler.com/microservices/
2. https://microservices.io/index.html

Plan:

1. Cutting and team sociology:
    * https://event-driven.io/en/sociological_aspects_of_microservices/ (Conway law)
    * https://event-driven.io/en/how_to_cut_microservices/
    * https://www.youtube.com/watch?v=haejb5rzKsM
2. Fowler thoughts: https://martinfowler.com/microservices/
   * Definition - https://martinfowler.com/articles/microservices.html
   * Trade-Offs - https://martinfowler.com/articles/microservice-trade-offs.html#boundaries
   * When to do? Monolith first? vs Dont start with monolith 
   * Prerequisites & first law of distributed objects
   * Testing
   * Breaking monolith (https://martinfowler.com/tags/legacy%20rehab.html)
   * Frontend
   * InfrastructureAsCode, DevOps
3. Patterns: https://microservices.io/patterns/index.html
    * Application architecture patterns
        * Monolithic architecture - https://microservices.io/patterns/monolithic.html
        * Microservice architecture - https://microservices.io/patterns/microservices.html
    * Decomposition
    * Refactoring to microservices
    * Data management
        * Transactional messaging
    * Testing
    * Deployment patterns
    * Cross-cutting concerns
    * Communication patterns
        * Style
        * Service discovery
        * Reliability
    * Security
    * Observability
    * UI patterns
4. Refactoring
    * https://microservices.io/refactoring/index.html
5. Microservices adoption anti-patterns: 
    * http://chrisrichardson.net/post/antipatterns/2019/01/28/melbourne-microservices.html
    * https://microservices.io/microservices/antipatterns/-/the/series/2019/06/18/microservices-adoption-antipatterns.html

   
1.2
When worth having more than one deployment unit in application?
Difference in trafic and workload in indivicual parts of app. Increasing throughput (BF), multi tenancy, multiregion
Not? 100% availability, microservice per storage type xD

1.3
Team cognitive load - how well do you understad system you work with? Missing skills or capabilites?
Team Interaction patters - collaboration, x as a service, facilitating? How would teams react?
Is your Platform well defined? 
Team Topologies (book)

Additional
https://martinfowler.com/bliki/SacrificialArchitecture.html
https://martinfowler.com/bliki/ServiceOrientedAmbiguity.html
