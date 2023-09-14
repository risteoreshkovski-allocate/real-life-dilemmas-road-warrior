##  	Email Analyser	## Ref 005
### Status
Pending

### Context
We need to Filter and whitelist certain emails that are related to trips. We need a means to indentify these and once found decide whether to store or search for the emails live time.

### Decision
Relevant emails can be identified by looking at the domains that the emails are from. We can also check for specific booking references in the email by examining the content. We will save the search results in a cost effective storage location for review by the user when they login to the system. The analyser will attempt to allocate the email to the correct trip using either the booking reference or other unique identifier, the user will need to confirm that the adding of the email to the trip is correct via the user interface.

### Consequences
There may be a risk that the algorythms used may either incorrectly pick up a email that are not related to a trip or may attribute it to the wrong trip or accidentally ignore a relevant email due to there being insufficient criteria to identify the information.

