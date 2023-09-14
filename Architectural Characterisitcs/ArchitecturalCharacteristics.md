## Architectural Characteristics

### Implicit Characteristics

#### Security

 - Store personal information and information provided by integrated systems securely. 
 - Must meet General Data Protection regulations or equivalent standard as a minimum.
 - Ensure only specified individuals can view trips and edit trip information.
 - Ensure only identified users can access the system.

#### Maintainability

 - Implemented with a clean architecture style and adheres to agreed coding standards to ensure that the code can be easily maintained and extended.

#### Testability

- We can use contract based testing to ensure we have a stable product and would be immediatley informed if there are any changes in the agreed api's. 
- We will cover integration, manual and unit tests as a minimum.
- We will also more generally test security and performance.

#### Deployability

- We need to ensure we can achieve continuous deployment and testing as a minimum for our product. 
- Can deploy new versions in a controlled manner to ensure stability before we deploy to all regions.

#### Accessibility
- Application must be usable by a wide range of users with possible visual, hearing and congnitive, speach and mobility and meet all stands. https://www.gov.uk/guidance/accessibility-requirements-for-public-sector-websites-and-apps


### Driving Characteristics

#### Reliability
?
#### Performance

- Travel updates must be presented in the app within 5 minutes of generation by the source

#### Scalability
- We need to be able to scale to support quarter million active users/week. 
- We can use auto scaling in this scenario, ie we may need to support more booking on a monday than a friday or such like.

#### Elasticity
As there are 15 million use account we should be prepared to support higher number of users than quarter million on certain occasions (sudden bursts). 

#### Extensibility
- can scan new email providers
- can interface with new travel systems

#### Usability

- Customers must be able to add, update and delete reservations manually in addition to the automated means of doing so. 
- Grouping should be used to show trip information and archived once the trip is over to make it easier to see current tips. 
- We should endeavour to provide the richest user interface possible. 
- Sharing with social media sites. 
- Available for mobile and web

#### Availability

- The system must be highly available with users able to always access the system. 
- It must also be available internationally. 
- There should be a maximum of 5 minutes per month of unplanned downtime.

#### Responsiveness

- All updates from external systems must be in the application within 5 minutes to beat the competition.
- Response time from web (800ms) and mobile (First-contentful paint of under 1.4 sec)

#### Fault Tolerance
- If one of the applications we interface with is inaccessible it should not affect the overall operations of the system and the user should be made aware that information from this source is currently unavailable. 

#### Interoperability

- Information from external systems needs to be displayed as part of the trip information. This may include car rentals , airlines, hotels and travel details. The interfaces must be able to meaningfully exchange and interpret information from external systems.
- User should be able to interface with standard social media sites and share with other targeted people (manager, travelling companion)
- Integrates with existing travel systems such as Sabre and Apollo

#### Evolvability


### Others Considered
#### Simplicity

- Easily usable interface modules that can be extended for use with many airlines, hotels and car rentals, travel systems and email providers. 
- We should be easily able to support other forms of travel.

#### Feasibility
- Minimum Viable Product should be available as soon as possible so we are not restricted to any specific deadline by the business.
- May be limited budget as this is a startup
- Limited development capacity as this is a startup