>The API is **not protected** against an **excessive** amount of calls or **payload sizes**. Attackers can use this for **Denial of Service** (DoS) and authentication flaws like **brute force attacks**.

## Use case

- Attackers **overload** the **API** by sending more requests than they can handle.
- Attackers send requests at a rate exceeding the API’s processing speed, clogging it up.
- The **size** of the **requests** or some fields in them exceeds what the API can process.
- An attacker submits requests with **excessively** **large payloads** or complex queries causing the **API** to hit a **bottleneck** and **drop** **requests**.

## How to prevent

- Apply **rate limiting** policies to **all endpoints**.
- Pay special attention to endpoints related to **authentication** which are a **prime target for hackers**.
- **Tailor rate limiting** to match what API methods, **clients**, or addresses need or **should be allowed to retrieve**.
- IPs can easily be forged, whenever possible, **configure** rate **limiting** **on** different keys, such as **fingerprints**, or **tokens**. 
- **Limit** payload sizes, and query complexity.
- Define **CPU/memory limits** for **container** and **compute resources**.
- **Limit** the **complexity** of queries (especially in **GraphQL**) to prevent **excessive** computation on the **server**.
- **Limit** the **amount** of **data** that can be retrieved by a **query** by imposing limits on the **pagination size**, or **page counts**.
- **Leverage** **DDoS protections** from your **cloud provider**.