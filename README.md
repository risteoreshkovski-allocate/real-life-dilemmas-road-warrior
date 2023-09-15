
# Real Life Dilemmas - Road Warrior Travel Architecture

**Team Members: Riste Oreshkovski; Andrej Manev; Jovan Nikoloski; Elena Aleksovska; Sarah Webb**
## Table of Contents
<img align="right" width="210" height="368" src="Images/confused.jpg">
- [Requirements](#requirements)  
    - [Introduction](#introduction)
    
    - [Business Requirements](#business-requirements)
    - [Functional Requirements](#functional-requirements)
    - [Architecture Characteristics Requirements](#architecture-characteristics-requirements)
    - [Constraints](#constraints)
    - [Assumptions](#assumptions)
- [Baseline Architecture](#baseline-architecture)  
- [Target Architecture](#target-architecture)  
    - [Use Case Model](#use-case-model)  
    - [System Context](#system-context)  
    - [Containers](#containers)  
    - [Process Views](#process-views)  
    - [Deployment](#deployment)  
- [Transition Architecture](#transition-architecture)
- [Architecture Decision Records](#architecture-decision-records)


## Requirements

### Business Requirements
** Introduction**
A new startup "Road Warrior" wants to build the next generation online trip management dashboard to allow travelers to see all of their existing reservations organized by trip either online (web) or through their mobile device
-   users quarter million active users/week
-   total users: 15 million (user accounts)

**Requirements**
-   Poll email looking for travel-related emails
-   Filter and whitelist certain emails
-   The system must interface with the agency’s existing airline, hotel, and car rental interface system to update travel details (delays, cancellations, updates, gate changes, etc.). Updates must be in the app within 5 minutes of an update (better than the competition)
-   Customers should be able to add, update, or delete existing reservations manually as well
-   Items in the dashboard should be able to be grouped by trip, and once the trip is complete, the items should automatically be removed from the dashboard.
-   Users should also be able to share their trip information by interfacing with standard social media sites or allowing targeted people to view your trip.
-   Richest user interface possible across all deployment platforms
-   Provide end-of-year summary reports for users with a wide range of metrics about their travel usage
-   Road Warrior gathers analytical data from users trips for various purposes - travel trends, locations, airline and hotel vendor preferences, cancellation and update frequency, and so on.

#### Additional context
-   Must integrate seamlessly with existing travel systems (i.e, SABRE, APOLLO)
-   Must integrate with preferred travel agency for quick problem resolution (help me!)
-   Must work international

#### Technical requirements
-   Users must be able to access the system at all times (max 5 minutes per month of unplanned downtime)
-   Travel updates must be presented in the app within 5 minutes of generation by the source
-   Response time from web (800ms) and mobile (First-contentful paint of under 1.4 sec)

### Stakeholders

This section describes key stakeholders of the system and their architectural concerns.

* **SH-1**: **Traveller** (availability, performance, scalability, fault tolerant, usability and secure)
	- Must be able to see all of their existing reservations organized by trip.
    - Should be able to add, update, or delete existing reservations manually.
	- Should be able to share their trip information by interfacing with standard social media sites or allowing targeted people to view their trip.

* **SH-2**: **Data analyst** (performance, scalability, fault tolerant, Secure)
	- Must be able to derive a given set of metrics from the data (trends, preferences, locations, hotels) 
	- Provide end of year summary report template which can be displayed for each user

* **SH-3**: **External Systems** (fault tolerant, secure)
	- Existing agency and travel APIs must remain stable and accessible in line with our agreed levels of service.

### Functional Requirements

#### Use Cases are defined below for the Traveller:

* **UC-1**: **Traveller registration**:
    - Traveller register their profile through external identity provider (SH-1);
	
* **UC-2**: **Traveller Login**:
	- Traveller login to the Road Warrior through external identity provider (SH-1);

* **UC-3**: **View Dashboard**:
	- Traveller views their existing reservations organised by trip (SH-1);
	
* **UC-4**: **Search for a reservation item**:
	- Traveller searchs for reservation item (airline, car rental or hotel) using search criteria (SH-1);

* **UC-5**: **Edit Trip information**:
	- Traveller is able to add, update, or delete existing reservations manually (SH-1);
	
* **UC-6**: **Share Trip information to Social Media**:
	- Traveller shares their trip information by interfacing with standard social media sites (SH-1);

* **UC-7**: **Views Summary Report**:
	- Traveller view summary of key metrics for the year via email (SH-1);


#### Use Cases are defined below for the External Systems

	
* **UC-8**: **Refresh Trip information **:
	- Trip information should be updated as soon as possible when we are notified by an external systems that a change has occured. (SH-3);
	


### Architecture Characteristics

#### Implicit Characteristics
There are the architectural properties that we believe all applications must have by design, due to this fact they have not been specifically rated.

**Security**(Use Cases X)
     - Store personal information and information provided by integrated systems securely. 
     - Must meet General Data Protection regulations or equivalent standard as a minimum.
     - Ensure only specified individuals can view trips and edit trip information.
      - Ensure only identified users can access the system.

**Maintainability**
    - Implemented with a clean architecture style and adheres to agreed coding standards to ensure that the code can be easily maintained and extended.

**Testability**
    - We can use contract based testing to ensure we have a stable product and would be immediatley informed if there are any changes in the agreed api's. 
    - We will cover integration, manual and unit tests as a minimum.
    - We will also more generally test security and performance.

**Deployability**
    - We need to ensure we can achieve continuous deployment and testing as a minimum for our product. 
    - Can deploy new versions in a controlled manner to ensure stability before we deploy to all regions.

**Accessibility**
    - Application must be usable by a wide range of individuals with possible visual, hearing and congnitive, speach and mobility and meet all stands. https://www.gov.uk/guidance/accessibility-requirements-for-public-sector-websites-and-apps

#### Driving Characteristics
These are the characteristics that we consider important to the development of this specific system based on careful analysis of the business requirements. The rating is from 1 - 5 where 5 is considered the most desirable characteristic and 1 the least.

**Interoperability | Rating: 5 STARS**
- Information from external systems needs to be displayed as part of the trip information. This may include car rentals , airlines, hotels and travel details. The interfaces must be able to meaningfully exchange and interpret information from external systems.
- User should be able to interface with standard social media sites and share with other targeted people (manager, travelling companion)
- Integrates with existing travel systems such as Sabre and Apollo

** Availability | Rating: 5 STARS**
- The system must be highly available with users able to always access the system. 
- It must also be available internationally. 
- There should be a maximum of 5 minutes per month of unplanned downtime.

** Usability | Rating: 4 STARS**
- Customers must be able to easily add, update and delete reservations manually in addition to the automated means of doing so.
- Grouping should be used to show trip information and archived once the trip is over to make it easier to see current tips. 
- We should endeavour to provide the richest user interface possible. 
- We need to make it easy to share with social media sites. 
- Make Available for mobile and web to allow users to access the site from from a laptop or phone.

** Fault Tolerance | Rating: 4 STARS**
- If one of the applications we interface with is inaccessible it should not affect the overall operations of the system and the user should be made aware that information from this source is currently unavailable. 
- Reliability is encompassed under this characteristic as without Fault Tolerance it would not be so.

** Scalability | Rating: 4 STARS**
- We need to be able to scale to support quarter million active users/week. 
- We can use auto scaling in scenarios, where we may need to support more bookings on a monday than a friday or such like.

** Responsiveness | Rating: 3 STARS**
- All updates from external systems must be in the application within 5 minutes to beat the competition.
- Response time from web (800ms) and mobile (First-contentful paint of under 1.4 sec)

** Elasticity | Rating: 2 STARS**
As there are 15 million use account we should be prepared to support higher number of users than quarter million on certain occasions (sudden bursts) however it is not predicted this should happen in the near future. 

** Extensibility | Rating: 2 STARS**
- can scan new email providers
- can interface with new travel systems

** Performance | Rating: 2 STARS**
- Travel updates must be presented in the app within 5 minutes of generation by the source

** Configurability | Rating: 2 Stars**
- Shall allow the user to set pefered agency and mail providers. 
- There is now major requirement to store any other user preferences or settings. 

#### Other Characteristics Considered
We considered the characteristics below but they were not relevant enough to rate or covered under anotherother characteristic umbrella.

Reliability, Agility, Abstraction, Cost, Domain Partitioning, Work Flow, Integration, Evolvability, Simplicity, Feasability

### Constraints
- The business is a startup so there may be a limited budget. 
- The maturity and capability of the development teams will be low, so limited knowledge of the travel domain.

### Assumptions
* **Support for Travel Types-1**: We are not expected to support other forms of travel such as buses or trains for the MVP.
* **Support for Payments-2**: The system will not be required to store any customer credit card information locally or maintain any payment details.
* **Time to Market-3**: No deadline for time to market has been given so we can define an appropriate timeline for the architecture we choose.
* **Storage Personal Identifiable Information-4**: This will not be stored directly in our system and OKTA(Auth0) used for authentication purposes


## Architecture
This section describes the target software architecture.

Please note that all views are documented in [C4 model](https://c4model.com) style, although only System Context, Container and dynamic views are presented. The most diagrams use informal notation style. All diagrams are supplied with a key explaining meaning of each shape on the diagram.

### Use Case Model

The following diagram shows mapping of architecture characteristics requirements on the key use cases based on discovered [requirements](Requirements.md):

![Use Case Model](images/use-case-model.jpg "Use Case Model")


### System Context

The system context diagram below depicted key users of the system and its external dependencies:

![System Context](images/system-context.jpg "System Context")

### Containers

The containers diagram that follows shows the high-level shape of the software architecture and how responsibilities are distributed across containers. It also shows the major technology choices and how the containers communicate with one another.

The architecture is build around four main domains that have been discovered during the problem analysis:
 - customer-facing services, such as ticket submission, customer profiles, survey submission etc;
 - expert services, such as ticket acceptance and knowledge base search;
 - administration services, such as reporting, survey analysis, ticket tracking etc;
 - billing service, which require high attention to security.

The architectural style used here as the bases is Service-based architecture (see [ADR-1](ADR/ADR-1-service-based.md) for details).

![Containers](images/containers.jpg "Containers")

### Process Views

This section explains some key use cases to demonstrate how corresponding workflows pass through containers.

#### UC-2: Customer registration
The following sequence diagram highlights some key requests that the customer performs during registration in the system.
One worth paying attention is registration of a credit card. In the customer database we store only some minimal credit card data to let the customer possibility identify which card do they have already registered. All the details of the credit card are encrypted and securely passed to the billing system (see [ADR-4](ADR/ADR-4-extract-billing-quanta.md)).

![UC-2: Customer registration](images/customer-registration.jpg "Customer Registration")

#### UC-3: Ticket submission
The following diagram illustrates the process of a ticket registration by the customer.

![UC-3: Ticket submission](images/ticket-submission.jpg "Ticket Submission")

Important thing to note is that the requests succeeds after the ticket is saved in the customer database and the corresponding event is fired for the ticket processing area. This way the customer will be able to see the new ticket immediately after the page refresh and will not have to wait on any further actions on the ticket.

#### UC-3: Ticket assignment
The diagram below explains how the system processes a new ticket and assigns it an expert.

![UC-3: Ticket Created](images/ticket-assignment.jpg)

Since Ticket Process is a job that runs periodically, tickets that cannot be assigned at the given moment will never be lost, they we bill processed next time the job will run.

Also, notice that an assignment is a separate entity. This way we can store a history of assignments.

#### UC-3: Ticket acceptance
This diagram continues the ticket workflow and shows how the Ticket Assigned event is processed by the Sysops Expert user.

![UC-3: Ticket Assigned](images/ticket-acceptance.jpg)

The experts operation succeeds as soon as the ticket status is saved in the database. And in case of acceptance the corresponding even is fired to the customer area.

#### UC-3: Ticket in-progress
This diagram demonstrates how the customer is notified when the Sysops Expert accepted the ticket.

![UC-3: Ticket In-Progress](images/ticket-inprogress.jpg)

Important to notice that the ticket is saved in the customer database prior to the notification event so that the customer will see the actual ticket status upon the notification receive.

#### UC-3: Ticket completion
This diagram explains the process when the Sysops Expert solved the problem and marks the ticket as completed.

![UC-3: Ticket Completed](images/ticket-completion.jpg)

#### UC-3: Ticket Resolved
This diagram illustrates how the customer receives a notification about the ticket resolution and link to the survey form.

![UC-3: Ticket Resolved](images/ticket-resolved.jpg)

First, the ticket status has to be updated in the customer database, so that upon receiving any notifications the customer will see the actual ticket status on the Customer Portal.

#### UC-4: Survey Submission

And finally the last step in the ticket resolution flow is survey submission by the customer.

![UC-4: Survey Submission](images/survey-submission.jpg)

From the customer perspective this is a fire-and-forget even so the operation succeeds as soon as the "Submit" button is clicked.

Analytics API can perform some preliminary processing of the survey if necessary or simply store it in the database for the reporting.

#### UC-7: Monthly billing
The diagram illustrates the monthly billing workflow.

![UC-7: Monthly billing](images/billing-sequence.jpg "Monthly Billing")

### Deployment

The deployment diagram illustrates how the system containers are mapped to the infrastructure:

![Deployment](images/deployment.jpg "Deployment")
Note the colors have not special meaning, they are just to distinguish thing from one another.

The deployment strategy here is cloud-agnostic, assuming you can use any cloud provider of your choice or stay totally on-prem. An exception is the billing stuff, which is recommended to remain on-prem anyway for security considerations.

## Transition Architecture

The solution proposed in the [Target Architecture](#containers) section is the final ambition that solves most of the problems and risks, but can require significant development efforts because of the database split required. Thus we can divide the whole work into two phases:

1. Solve critical problems an stick with a monolithic database until it becomes a bottleneck.
2. Migrate further to the target architecture to deal with all remaining risks.

Here is the transitional architecture proposal that solves critical problems but leaves some risks (analysis follows).
Note that we still leverage asynchronous messaging for ticket processing here to enable independent scalability and availability for different parts of the system. In this case, messages can contain mach less information because all the details can be taken by the receiver from the database.

![Transition Architecture](images/transition.jpg)

Since we have a single monolithic database we can save some efforts on additional messaging and replication.

### Risk Analysis
These are the possible high risks of the transition architecture.

#### Performance
Because this is a monolithic database it can become a performance bottleneck. The same concern regarding the single API Gateway - if not scaled properly may also become a bottleneck.

#### Availability
A single API Gateway may introduce a single point of failure for the whole system (see [ADR-12](ADR/ADR-12-gateways.md)).

#### Security
There is a risk that admin staff can get access to the customer credit card data. We certainly want to prevent that by extracting billing into a separate architectural quantum (see [ADR-4](ADR/ADR-4-extract-billing-quanta.md)) and isolating it in a separate network zone with strict access permissions.

The same concern is regarding the customer services - we don't want to allow an attacker to get access to the reset of the system. A significant security improvement would be to migrate customer services and data in a separate quantum in isolate it in a separate network zone (see [ADR-5](ADR/ADR-5-extract-customer-quantum.md)).

#### Other
Additional concerns regarding the ?

## Architecture Decision Records

> *Why is more important than how.  
Second Law of Software Architecture*

 - [ADR-1](ADR/ADR-1-service-based.md) Use Service-based architectural style as the basic style.

