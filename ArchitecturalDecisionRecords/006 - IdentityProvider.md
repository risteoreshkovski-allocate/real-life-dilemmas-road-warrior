##  	Identity Provider	## Ref 006
### Status
Pending

### Context
User must securley authenticate in order to use Road Travel Warrior

### Decision
We are going to use OKTA (Aoth0) as our chosen Identity Provider, this will be used to federate to Google, or other customer specific identity providers. Auth0 supports the following enterprise providers :
Active Directory/LDAP, ADFS, Azure Active Directory Native, Google Workspace, OpenID Connect, Okta, PingFederate, SAML and Azure Active Directory. It is very easy to integrate into and to adapt.

### Consequences
This is to ensure that the user profile information is stored securley in one place, however we a relient on the continuity of business of our chosen identity provider. We will incure a cost for using the service, however it will be cheaper and more maintainable than providing support to integrate with multiple identity providers. It helps us maximise security and protect against the latest threats.

