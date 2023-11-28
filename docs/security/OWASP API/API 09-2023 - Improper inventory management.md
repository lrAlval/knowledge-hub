>Attackers find **non-production** versions of the API (**for** example, staging, testing, beta, or earlier versions) that are not as well protected as the production API, and use those to launch their attacks.

## Use case

- DevOps, the cloud, containers, and Kubernetes make having multiple deployments easy (for example, dev, test, branches, staging, and old versions).
- Desire to maintain backward compatibility forces to leave old APIs running.
- Old or non-production versions are not properly maintained, but these endpoints still have access to production data.
- Once authenticated with one endpoint, attackers may switch to the other, production one.
## How to prevent

- Keep an up-to-date inventory of all API hosts.
- Limit access to anything that should not be public.
- Limit access to production data, and segregate access to production and non-production data.
- Implement additional external controls, such as API firewalls.
- Properly retire old versions of APIs or backport security fixes to them.
- Implement strict authentication, redirects, CORS, and so forth.