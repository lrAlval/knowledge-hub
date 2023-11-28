>Server-Side Request Forgery (SSRF) can occur when an API fetches a remote resource without validating the user-supplied URL. This enables an attacker to coerce the application to send a crafted request to an unexpected destination, even when protected by a firewall or a VPN.
## Use case

- An API accepts a URL as a parameter for a redirection, and an attacker finds that they can use this to redirect the response to a rogue site which is able to steal sensitive API data.
- An attacker can force an API to load resources from a server under their control; this is the basis of a key injection attack in JWTs.
- An API allows access to the local host allowing an attacker to use malform requests to access local resources.

## How to prevent

- Precisely define the schemas, types, and patterns you will accept in requests at design time and enforce them at runtime.
- Prevent your API server from following HTTP redirections.
- Use an `allow list` of permitted redirects or accesses. 
- Restrict the range of allowed URL schemes and ports allowed.
- Use a standard implementation for the library responsible for loading resources making sure it cannot access the local host, and uses sanitized URLs from a safe URL parser.