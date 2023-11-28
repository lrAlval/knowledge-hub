## Middleware Ordering
- When a request is received by .NET Core web API, it goes through a chain of middleware's. 
- Every middleware add some feature in the request pipeline on top of previous middleware. 
- In addition to middleware there are also filters which are executed during request processing.

## Middleware order
1. Exception Handler
2. HSTS - enforce Strict transport security.
3. HTTPs Redirection
4. Static Files (MVC)
5. Routing
6. CORS
7. Authentication
8. Authorization
9. Custom Middleware's
10. Endpoint Middleware

![[Pasted image 20231126170712.png]]

## Endpoint Middleware

![[Pasted image 20231126172839.png]]

## Reference
- [ASP.NET Middleware overview](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/middleware/?view=aspnetcore-8.0)