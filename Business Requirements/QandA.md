### 2023 O’Reilly Kata Challenge Questions and Answers

## We have worked with the katas hosts to provide answers to your questions as appropriate. Our goal was to provide guidance on the problem without providing information that we want you to figure out as part of the challenge. This mimics what is seen in real life when stakeholders are not sure of what their final vision is or how it will evolve in the future. A key part of the challenge is making your decisions on the right solution for the kata; everyone will solve the problem differently.


# Is the road warrior dashboard built by a new startup not affiliated with any particular travel agency(e.g. Expedia, Thomas Cook etc. )?

Correct - this is a separate independent startup company. 

# The system must interface with the agency’s existing airline, hotel, and car rental interface system to update travel details (delays, cancellations, updates, gate changes, etc.).Updates must be in the app within 5 minutes of an update (better than the competition). What is referred to as “Agency” in this requirement ? Is Expedia an example of an agency ?

Agency in this case means the airline, hotel, and car rental. All of these have a standard API, so you don’t have to worry about those details. For example, you might have a component in your architecture that says “Airline Interface” that interfaces or polls the airline exchange. 

# Is the scope limited to Airline, Hotel and Car Rental only ? Do we need to include other items like bus booking, train booking, attraction tickets etc. ? 

Right now it’s only airline, hotel, and car rental, but you should anticipate other interfaces to things like train, bus lines, and so on

# Why do we need to integrate with Apollo, Sabre if the agencies like Expedia are already integrated with them, can’t we use agency’s APIs ?  

In addition to the standard airline exchanges, Sabre and Apollo are other optional feeds to the Road Warrior system for bookings, updates, and cancelations. Through a SABRE or APOLLO API, Road Warrior can listen for bookings and other updates given a confirmation ID.

# Why do we need to poll email if we are already integrated with travel systems ?  


This is another optional feed. Users can choose NOT to have Road Warrior scan their email, in which case they can fall back to the exchanges or SABRE/APOLLO interfaces

# Do we need to provide technical architecture & tech stack as well ?  


Technical architecture should only include user interfaces, databases, services, and the like, but you so not need to include specific products, platforms, and languages.

# Why would another agency solve the problem for a booking done by 3rd party ? E.g if I have done the booking via Expedia why would Thomas Cook solve my problem ? (referring to this requirement -  “Must integrate with preferred travel agency for quick problem resolution (help me!)”. 

The end user can specify which travel agency (if any) they want to contact through the app. If a booking WAS made by a travel agent, the app should already know that information on the Help! Button for that particular registration.

# For the max. 5 minutes downtime per month requirement, is the to provide the infrastructure component along with CSP(Cloud Service Provider) details like AWS Lambda, Azure Functions, AWS Aurora etc. ?

You do not need to specify the actual cloud provider if you are choosing a cloud deployment. It is assumed that the infrastructure (on-prem or cloud-based) would support these requirements. It is up to you to create an *architecture* to support these (for example, would a monolithic system easily scale to 1 million users?)

# What is the source for the travel updates ? Referring to the requirement. - "Travel updates must be presented in the app within 5 minutes of generation by the source".  

“Source” in this case can come from one of the following places (configurable by the user):
1. Email scan
2. Airline, hotel, and rental car company exchanges (API)
3. SABRE/APOLLO API interfaces

# Does polling emails necessarily mean, that we have to follow Millions of user's emails, or could it also mean, that users forward us anything, that is travel relevant?

This can mean that the user either allows Road Warrior to "listen " to their email via a standard sharing interface and parse travel-related emails (and ignore others) OR the user can manually (or via a filter) forward emails to Road Warrior.

# What exactly is a preferred agency and who prefers it?

This is the users preferred travel agent or similar facilitator.

# We shall integrate with huge reservations APIs, like Sabre or Apollo. Do we need to integrate with both of them or one or a bigger number or can we assume a standardized interface?

You can assume a standard interface; we're not testing knowledge of travel agent integration details.
You write that updates must be visible in the app within 5 minutes after creation by the source. Does that include possible delayed emails or is that only the time, after WE have received an email?

This requirement means that there must be a 5 min turnaround after Road Warrior receives the update; we aren't measuring possible latency because of email providers. Once Road Warrior receives the email, that's when the clock starts.

# Do we need to evaluate emails from the ~2Mio active users or from the 15 Mio total users all the time?

Any of the 15 million users can become active at any time.

# Can you please explain or give examples to this requirement: "Richest user interface possible across all deployment platforms", e.g. what platforms?

The platforms are mobile device (smart phone) and web-based interface. "Richest possible" means that the preference is that the application can utilize features like GPS on mobile devices that don't exist within a browser.

Customers should be able to add, update, or delete existing reservations manually as well. Is this updating our view of customers reservations only (adding customer bookings that do not have an email etc.)? Or do we need to allow customers a way of add/edit/delete their bookings from our platform? 

This only applies to Road Warrior; the user will have to manually interact with the individual service to make changes or cancelations.

# Must integrate with preferred travel agency for quick problem resolution. Do we direct customers back to the original booking supplier (via deep link etc)? Or have a partnership for a travel agency to help with various other suppliers' bookings?

We allow the user to specify a preferred travel agent, and that's where we redirect them. If the user hasn't specified a travel agent, then this facility isn't available (we aren't in the business of brokering for travel agents.

# What timeline do we have to get the product to market?
MVP as soon as possible.

# What budget do we have?
This is a start up; use your best judgment re: budget.

# What’s the maturity and capability of the development teams?
This is a start up; use your best judgment re: budget.

# In the event of a disaster what is an acceptable data loss in terms of minutes?
Use your best judgment.

# When making changes within the app, should those updates reflect immediately, or only when confirmed by email?
Immediately.

# Can it be agreed that to increase speed to market of basic functionality with other extensions agreed to be delivered at a later point?
Use your best judgment.

# Are they happy to invest in cloud infrastructure and existing managed services on aws / azure?
If it works for the solution.

# Should we consider the environmental implications of the architecture we implement, i.e. is the funding for the startup agreed based on meeting certain targets?
This is up to you if it works for your solution.

# Where does the 15 Mio user base comes from for a start-up?
This should not impact your solution.

# What is the benefit for the users/ travelers and who is behind the start-up (for instance an existing travel agency or is it a complete business model) Assumption: start-up has knowledge in business domain, but needs support on technical level.
This is a good assumption to work from.

# What is the MVP?
Minimum viable product

ADDITIONAL QUESTIONS TO BE ANSWERED

# How does Road Warrior generate revenue?  Do users pay a subscription fee, are the data analytics and insights sold to companies in the travel sector, etc.?  We feel that a better understanding of the business model will help us decide which architecture characteristics to focus on in our solution.
TBD

# What is the financial situation and when are you expecting the first revenue?
This is a startup, use your best judgment


