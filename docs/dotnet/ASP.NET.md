
## Middleware / Request processing order
1. Routing middleware 
	- set up routes
2. Controller middleware
	- set up http handlers and controller factories.
3. Action Middleware
	- set up action invoker
	- set up model binders
		- data type conversion
		- data validation
	- set up authentication Filter
		- validate identity.
	- set up Authorization Filter
		- validate permissions or role.
	- execute action filters
		- before action is executed - OnActionExecuting
		- after action is executed - OnActionExecuted
4. execute action results
	- Action Result can be:
		- ViewResult
			- ViewResult
			- PartialViewResult
		- NonViewResult
			- RedirectToRouteResult
			- RedirectResult
			- ContectResult
			- JsonResult
			- FileResult
			- EmptyResult


## Reference
- [dotnettricks](https://www.dotnettricks.com/learn/mvc/detailed-aspnet-mvc-pipeline)
