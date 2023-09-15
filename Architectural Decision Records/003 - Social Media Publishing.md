##  	Social Media Publishing	## Ref 003
### Status
Pending

### Context
Users should also be able to share their trip information by interfacing with standard social media sites. We will need to limit the number of API's that we support.

### Decision
We will utilise X, Meta and LinkedIn API's in order to support publishing to Facebook, Instragram, X and LinkedIn.

### Consequences
There may be some users which use less common social media sites which will not be able to use the functionality however by consuming these API's we hope to cover the majority.
Simplicity and Maintainability, In order to avoid having to maintain and provide storage for the configuration details for a user to allow us access a social media provider and also maintain and develop a component to interface with either meta/ X API's which may have provided a more seamless integration. In making this decision we do not believe usability will be effected as many sites allow users to share information by just redirecting them to add the post to their social media provider in the suggested manner