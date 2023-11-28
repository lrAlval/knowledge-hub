>API endpoints can be vulnerable to attacks based on their data: either they may **expose more data** than is required for their business purposes (excessive **information exposure**), or they may inadvertently **accept** and process **more data** than they should (**mass assignment**).


## Use case

- The **API returns** **full** data **objects** **as** they are **stored** in the **backend database**.
- The **client application filters** the **responses** and only shows the data that the **users** **really need to see**.
- Attackers call the **API directly** and retrieve sensitive data that the UI would filter out.
- The **API** works with the data structures without **proper filtering**.
- **Received payload** is **blindly** transformed into an **object** and **stored.**
    - NodeJS:  
        var user = new User(req.body);  
        user.save();
    - Rails:  
        @user = User.new(params[:user])
- Attackers can guess the fields by looking at the GET request data.

## How to prevent

**Requests**

- Do not **automatically** **bind** incoming data to internal **objects**.
- **Explicitly define** all the parameters and **payloads** you are **expecting**.
- Use the **readOnly** property set to true in object schemas for all **properties** that can be retrieved through APIs but **should** **never be modified.**
- Precisely **define** the **schemas**, types, and patterns you will accept in requests **at design time** and **enforce** them at **runtime**.

**Responses**

- **Never** rely on the **client** to **filter data**!
- **Review** all **API responses** and adapt them to match what the API **consumers really need**.
- Carefully **define schemas** for all the **API responses**.
- Do not forget about **error responses**, **define** proper **schemas** as well.
- **Identify** all the **sensitive data** or Personally Identifiable Information (**PII**), and justify its use using a robust **data governance process**.

