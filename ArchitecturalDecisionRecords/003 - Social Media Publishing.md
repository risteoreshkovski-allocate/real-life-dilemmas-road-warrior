##  	Social Media Publishing	## Ref 003
### Status
Pending

### Context
Users should also be able to share their trip information by interfacing with standard social media sites. 

### Decision
 - We will support publishing to Facebook, Instagram, X and LinkedIn.
 - We will not be exposing links publicly.
 - We will prepare the content at a point in time and provide a link that navigates the traveller to the selected Social Media site.
 - The traveller can then post the prepared content directly on the selected Social Media site.

### Consequences
Because we are not sharing a direct link to the traveller's trip, the information in the Social Media post can become outdated in case of changes on the trip afterwards.
There may be some users which use less common social media sites which will not be able to use the functionality however by consuming these API's we hope to cover the majority.
Simplicity and Maintainability, In order to avoid having to maintain and provide storage for the configuration details for a user to allow us access a social media provider and also maintain and develop a component to interface with either meta/ X API's which may have provided a more seamless integration. In making this decision we do not believe usability will be effected as many sites allow users to share information by just redirecting them to add the post to their social media provider in the suggested manner