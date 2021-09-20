# Access Token Control​
## Problems with token storage​

### When store in cookie
* Proned to [CSRF](https://en.wikipedia.org/wiki/Cross-site_request_forgery) attacks​

### When store in localstorage
* Proned to [XSS](https://en.wikipedia.org/wiki/Cross-site_scripting) attacks​

### What if we store it in memory
#### Advantages
* Hard to be stolen
* Won't be persisted

#### Disadvantages
* The users session won't be persisted

## Proposal
Access token + refresh token

### Specification
#### Access token
* Used for validating users
* Stored in memory
* Low life span

#### Refresh token
* Used to extend the Access token lifespan
* Stored in cookie(**[HttpOnly](https://owasp.org/www-community/HttpOnly)**)​

#### Advantages
* The users session will be persited​
* Access token is short-live so even if it get stolen, it will not be as damaging​
* Because refresh token is in HttpOnly cookie, the client can't programmatically read it​
* Even if CSRF attack happens, the Access token can't not be obtain.

### Diagram Flow​
![Diagram](./Token%20Control.jpg)