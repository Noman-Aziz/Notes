# Cross-origin resource sharing (CORS)

### Introduction

* Cross-origin resource sharing (CORS) is a browser mechanism which enables controlled access to resources located outside of a given domain.
* It extends and adds flexibility to the same-origin policy (SOP).
* It also provides potential for cross-domain attacks, if a website's CORS policy is poorly configured and implemented.
* **CORS is not a protection against cross-origin attacks such as cross-site request forgery (CSRF)**

### Same-origin policy

* The same-origin policy is a restrictive cross-origin specification that limits the ability for a website to interact with resources outside of the source domain.
* It generally allows a domain to issue requests to other domains, but not to access the responses.

#### Why is the same-origin policy necessary?

When a browser sends an HTTP request from one origin to another, any cookies, including authentication session cookies, relevant to the other domain are also sent as part of the request.

#### Relaxation of the same-origin policy

The same-origin policy is very restrictive and consequently various approaches have been devised to circumvent the constraints. Many websites interact with subdomains or third-party sites in a way that requires full cross-origin access. **A controlled relaxation of the same-origin policy is possible using cross-origin resource sharing (CORS)**.
