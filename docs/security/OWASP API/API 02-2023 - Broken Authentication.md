> Poorly implemented API authentication allows attackers to assume other users’ identities, or access resources without any authentication at all.


## Use case
- **Unprotected** **APIs** thar are considered "**internal**".
- Weak authentication that does not follow industry best practices.
- Weak **API** **keys** that are **not** **rotated**.
- Passwords that are weak, plain text, encrypted, poorly hashed, shared or default passwords.
- Authentication susceptible to brute force attacks and credential stuffing.
- **Credentials** and keys **included** in **URLs**.
- **Lack** of access **token** **validation** (including JWT validation).
- Unsigned or weakly signed **non-expiring JWTs**.

## How to prevent

- Check all possible ways to authenticate to all APIs.
- APIs for password reset and one-time links also allow users to authenticate, and should be protected just as rigorously.
- Use standard authentication:
	- token generation.
	- password storage.
	- multi-factor authentication (MFA).
- Use **short**-lived **access** tokens.
- **Authenticate** your apps (so you know who is talking to you).
- Use **stricter rate-limiting** for **authentication**.
	- implement **lockout policies** and **weak password checks**.