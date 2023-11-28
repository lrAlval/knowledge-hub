>The API relies on the client to use user-level or admin-level/privileged APIs as **appropriate**. Attackers figure out the “hidden” admin API methods and invoke them directly.


## Use case

- Some **administrative** **functions** are exposed as APIs.
- Sensitive operations should **only be available internally** (for example deleting a resource)
- Non-privileged users can access these functions without authorization if they know how.
- Can be a matter of knowing the URL, or using a different verb or a parameter:
    - `/api/users/v1/user/myinfo`
    - `/api/admins/v1/users/all`

## How to prevent

- - Do not rely on the client to **enforce admin access**.
    - Apply `deny all` access by default.

- Only **allow operations** to users belonging to the **appropriate** **group or role**.
- Implement properly designed and **tested authorization**.