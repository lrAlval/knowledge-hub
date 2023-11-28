>Modern API-based systems tend to be highly interconnected, frequently consuming upstream APIs. Unfortunately, these upstream APIs may themselves be vulnerable and put their consumers at risk.
## Use case

- An upstream API may inadvertently store data provided to it by a consumer, thereby violating the data governance regulations of the consumer.
- An upstream API provider may be attacked and compromised and then pass malicious data to its consumers due to insufficient internal controls. A typical example is an SQL injection attack.

## How to prevent

- Just like the case with user input, do not trust upstream API data. 
- Filter and sanitize any input data regardless of origin, particularly against injection attacks.
- Ensure that upstream API providers specify their API contract, and use runtime mechanisms to enforce this contract.
- Assume upstream API providers are part of your supply chain and verify their internal development processes. 
- Use a secure communication channel at all times.