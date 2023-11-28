>Poor configuration of the API servers allows attackers to exploit them.

## Use case

- Unpatched systems
- Unprotected files and directories
- Unhardened images
- Missing, outdated, or misconfigured TLS
- Exposed storage or server management panels
- Missing CORS policy or security headers
- Error messages with stack traces
- Unnecessary features enabled

## How to prevent

- Automate the hardening and patching processes of the full API stack (code, libraries, containers)
- Automate test to API endpoints for misconfiguration (TLS version, cyphers, bad verbs)
- Disable unnecessary features.
- Restrict administrative access.
- Define and enforce all outputs, including errors.