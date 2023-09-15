
# Real Life Dilemmas - Road Warrior Travel Architecture

**Team Members: Riste Oreshkovski; Andrej Manev; Jovan Nikoloski; Elena Aleksovska; Sarah Webb**

## Table of Contents

## Contents
<img align="right" width="210" height="368" src="Images/confused.jpg"/>
- [Requirements](#requirements)  
    - [Introduction](#introduction)
    - [Business Requirements](#business-requirements)
    - [Functional Requirements](#functional-requirements)
    - [Architecture Characteristics](#architecture-characteristics)
    - [Constraints](#constraints)
    - [Assumptions](#assumptions)
- [Architecture](#architecture)  
    - [Use Case Model](#use-case-model)  
    - [System Context](#system-context)  
    - [Containers](#containers)  
    - [Process Views](#process-views)  
    - [Deployment](#deployment)  
- [Architecture Decision Records](#architecture-decision-records)

## Requirements

### Business Requirements
** Introduction**
A new startup "Road Warrior" wants to build the next-generation online trip management dashboard to allow travelers to see all of their existing reservations organized by trip either online (web) or through their mobile device
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
-   Road Warrior gathers analytical data from user's trips for various purposes - travel trends, locations, airline and hotel vendor preferences, cancellation and update frequency, and so on.

#### Additional context
-   Must integrate seamlessly with existing travel systems (i.e., SABRE, APOLLO)
-   Must integrate with a preferred travel agency for quick problem resolution (help me!)
-   Must work internationally

#### Technical requirements
-   Users must be able to access the system at all times (max 5 minutes per month of unplanned downtime)
-   Travel updates must be presented in the app within 5 minutes of generation by the source
-   Response time from web (800ms) and mobile (First-contentful paint of under 1.4 sec)

### Stakeholders

This section describes key stakeholders of the system and their architectural concerns.

* **SH-1**: **Traveller** (availability, performance, scalability, fault-tolerant, usability and security)
	- Must be able to see all of their existing reservations organized by trip.
    - Should be able to add, update, or delete existing reservations manually.
	- Should be able to share their trip information by interfacing with standard social media sites or allowing targeted people to view their trip.

* **SH-2**: **Data analyst** (performance, scalability, fault-tolerant, Secure)
	- Must be able to derive a given set of metrics from the data (trends, preferences, locations, hotels) 
	- Provide an end-of-year summary report template which can be displayed for each user

* **SH-3**: **External Systems** (fault-tolerant, secure)
	- Existing agency and travel APIs must remain stable and accessible in line with our agreed levels of service.

### Functional Requirements

#### Use Cases are defined below for the Traveller:
* **UC-1**: **Traveller registration**:
    - Traveller register their profile through an external identity provider (SH-1)
![UC-1: Traveller registration](Images/Sequence%20diagrams%20-%20Sequence-Registration.png "Traveller registration")
* **UC-2**: **Traveller Login**:
	- Traveller login to the Road Warrior through an external identity provider (SH-1)
![UC-1: Traveller Login](Images/Sequence%20diagrams%20-%20Sequence-Login.png "Traveller Login")
* **UC-3**: **View Dashboard**:
	- Traveller views their existing reservations organised by trip (SH-1)
 ![UC-1: View Dashboard](Images/Sequence%20diagrams%20-%20Sequence-ViewDashboard.png "View Dashboard")
* **UC-4**: **Search for a reservation item**:
	- Traveller searches for a reservation item (airline, car rental or hotel) using search criteria (SH-1)
![UC-1: Search for a reservation item](Images/Sequence%20diagrams%20-%20Sequence-SearchReservationItem.png "Search for a reservation item")
* **UC-5**: **Edit Trip Information**:
	- Traveller is able to add, update, or delete existing reservations manually (SH-1)
![UC-1: Edit Trip Information](Images/Sequence%20diagrams%20-%20Sequence-TravellerEditTrip.png "Edit Trip Information")
* **UC-6**: **Share Trip information to Social Media**:
	- Traveller shares their trip information by interfacing with standard social media sites (SH-1)
![UC-1: Share Trip information to Social Media](Images/Sequence%20diagrams%20-%20Sequence-TravellerEditTrip.png "Share Trip information to Social Media")
* **UC-7**: **Views Summary Report**:
	- Traveller view summary of key metrics for the year via email (SH-1)

#### Use Cases are defined below for the External Systems
* **UC-8**: **Refresh Trip Information**:
	- Trip information should be updated as soon as possible when we are notified by an external system that a change has occurred. (SH-3)
![UC-1: Refresh Trip Information](Images/Sequence%20diagrams%20-%20Sequence-TravellerEditTrip.png "Refresh Trip Information")
### Architecture Characteristics

#### Implicit Characteristics
There are architectural properties that we believe all applications must have by design, due to the fact they have not been specifically rated.

**Security**
     - Store personal information and information provided by integrated systems securely. 
     - Must meet General Data Protection regulations or equivalent standards as a minimum.
     - Ensure only specified individuals can view trips and edit trip information.
      - Ensure only identified users can access the system.

**Maintainability**
    - Implemented with a clean architecture style and adhered to agreed coding standards to ensure that the code can be easily maintained and extended.

**Testability**
    - We can use contract-based testing to ensure we have a stable product and would be immediately informed if there are any changes in the agreed APIs. 
    - We will cover integration, manual and unit tests at a minimum.
    - We will also more generally test security and performance.

**Observability**
    - We plan to collect telemetry data (metrics, logs and traces) using the Open Telemetry standards for the purposes of monitoring the performance, application usage and error logging.

**Deployability**
    - We need to ensure we can achieve continuous deployment and testing as a minimum for our product. 
    - Can deploy new versions in a controlled manner to ensure stability before we deploy to all regions.

**Accessibility**
    - Application must be usable by a wide range of individuals with possible visual, hearing cognitive, speech and mobility and meet all standards. https://www.gov.uk/guidance/accessibility-requirements-for-public-sector-websites-and-apps

#### Driving Characteristics
These are the characteristics that we consider important to the development of this specific system based on careful analysis of the business requirements. The rating is from 1 - 5 where 5 is considered the most desirable characteristic and 1 the least.

**Interoperability | Rating: 5 STARS**
- Information from external systems needs to be displayed as part of the trip information. This may include car rentals , airlines, hotels and travel details. The interfaces must be able to meaningfully exchange and interpret information from external systems.
- User should be able to interface with standard social media sites and share with other targeted people (manager, travelling companion)
- Integrates with existing travel systems such as Sabre and Apollo

**Availability | Rating: 5 STARS**
- The system must be highly available with users able to always access the system. 
- It must also be available internationally. 
- There should be a maximum of 5 minutes per month of unplanned downtime.

**Usability | Rating: 4 STARS**
- Customers must be able to easily add, update and delete reservations manually in addition to the automated means of doing so.
- Grouping should be used to show trip information and archived once the trip is over to make it easier to see current tips. 
- We should endeavour to provide the richest user interface possible. 
- We need to make it easy to share with social media sites. 
- Make Available for mobile and web to allow users to access the site from from a laptop or phone.

**Fault Tolerance | Rating: 4 STARS**
- If one of the applications we interface with is inaccessible it should not affect the overall operations of the system and the user should be made aware that information from this source is currently unavailable. 
- Reliability is encompassed under this characteristic as without Fault Tolerance it would not be so.

**Scalability | Rating: 4 STARS**
- We need to be able to scale to support a quarter million active users/week. 
- We can use auto-scaling in scenarios, where we may need to support more bookings on a Monday than a Friday or such.

**Responsiveness | Rating: 3 STARS**
- All updates from external systems must be in the application within 5 minutes to beat the competition.
- Response time from web (800ms) and mobile (First-contentful paint of under 1.4 sec)

**Elasticity | Rating: 2 STARS**
As there are 15 million user accounts we should be prepared to support a higher number of users than a quarter million on certain occasions (sudden bursts) however it is not predicted this should happen in the near future. 

**Extensibility | Rating: 2 STARS**
- can scan new email providers
- can interface with new travel systems

**Performance | Rating: 2 STARS**
- Travel updates must be presented in the app within 5 minutes of generation by the source

**Configurability | Rating: 2 Stars**
- Shall allow the user to set preferred agency and mail providers. 
- There is not a major requirement to store any other user preferences or settings. 

#### Other Characteristics Considered
We considered the characteristics below but they were not relevant enough to rate or covered under another characteristic umbrella.

Reliability, Agility, Abstraction, Cost, Domain Partitioning, Work Flow, Integration, Evolvability, Simplicity, Feasibility

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

Please note that all views are documented in [C4 model](https://c4model.com) style, although only System Context, Container and dynamic views are presented. Most diagrams use an informal notation style. All diagrams are supplied with a key explaining the meaning of each shape on the diagram.

### Use Case Model

The following diagram shows the mapping of architecture characteristics requirements on the key use cases based on discovered [requirements](Requirements.md):

![Use Case Model](images/use-case-model.jpg "Use Case Model")


### System Context

The system context diagram below depicts key users of the system and its external dependencies:

![System Context](images/system-context.jpg "System Context") ADD DIAGRAM HERE

### Containers

The containers diagram that follows shows the high-level shape of the software architecture and how responsibilities are distributed across containers. It also shows the major technology choices and how the containers communicate with one another.

The architecture is built around two main domains that have been discovered during the problem analysis:
 - traveler-facing services, such as trip viewing and amending reservations;
 - data analytics, provision of data for reporting and defining metrics;


![Containers](images/containers.jpg "Containers")

## Architecture Decision Records

> *Why is more important than how.  
Second Law of Software Architecture*

 - [ADR-001](https://github.com/risteoreshkovski-allocate/real-life-dilemmas-road-warrior/ArchitecturalDecisionRecords/001 - Analysis And Reporting.md) Analysis And Reporting.
 - [ADR-002](https://github.com/risteoreshkovski-allocate/real-life-dilemmas-road-warrior/ArchitecturalDecisionRecords/002 - Traveller Search.md) Traveller Search.
 - [ADR-003](https://github.com/risteoreshkovski-allocate/real-life-dilemmas-road-warrior/ArchitecturalDecisionRecords/003 - Social Media Publishing.md) Social Media Publishing.
 - [ADR-004](https://github.com/risteoreshkovski-allocate/real-life-dilemmas-road-warrior/ArchitecturalDecisionRecords/004 - Supported Email Protocols.md) Supported Email Protocols.
 - [ADR-005](https://github.com/risteoreshkovski-allocate/real-life-dilemmas-road-warrior/ArchitecturalDecisionRecords/005 - Email Analyser.md) Email Analyser.
 - [ADR-006](https://github.com/risteoreshkovski-allocate/real-life-dilemmas-road-warrior/ArchitecturalDecisionRecords/006 - IdentityProvider.md) Identity Provider.

