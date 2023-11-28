>A set of APIs exposes a business flow and an attacker abuses these APIs using automated methods to achieve a malicious intent, such as exfiltrating data or manipulating market or price data.

## Use case

- An attacker discovers an API to buy a product online and uses automation to bulk purchase all items of a newly released product which they later re-sell. 
- Real-estate website’s price information can be scraped over time to predict house price trends in an area.
- Attackers can use automation to perform actions faster than a human user and gain an unfair advantage on auction sites, or similar.

## How to prevent

- Understand business flows that could be sensitive to abuse and add extra layers of protection to these and ensure authentication is required, using recommended OAuth flows, like authorization_code.
- Ensure that APIs are fully protected with robust rate-limiting in front of the API.
- Monitor API access and restrict clients using either suspicious devices or originating from risky IP addresses. 
- Identify non-human usage patterns such as impossibly quick transactions, and insert Captcha or other human detection controls.