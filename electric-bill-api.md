
## TransBnk Electricity Bill API  
**Version:** 1.0  
**Release Date:** 13-May-2024  

---

## 2. Overview

### Brief Description of What the API Does
The **TransBnk Electricity Bill API** provides functionality for retrieving electricity bill details for customers. It includes two main components:

1. **Operator Code Fetch API**
   - Retrieves operator codes corresponding to states.
   - These codes are required to identify the correct electricity provider before fetching bill details.

2. **Electricity Bill API**
   - Fetches detailed electricity bill information such as:
     - Customer Name
     - State
     - Address
     - Mobile
     - Email
     - Bill Amount
     - Bill Number
     - Document Link
   - Requires the customer’s **CA number** and **operator code** as input.

---

### Use Cases and Benefits

#### Use Cases
- **Utility Bill Payment Platforms**: Automate bill fetching for payment processing.
- **Banking Applications**: Allow customers to view and pay electricity bills directly.
- **Fintech Solutions**: Aggregate bills from multiple states and operators.
- **Customer Service Portals**: Enable support teams to verify and assist with bill details.

#### Benefits
- **Automation**: Reduces manual entry and errors.
- **Real-Time Data**: Ensures up-to-date bill information for faster processing.
- **Scalability**: Supports multiple states and operators for nationwide coverage.
- **Security**: API key authentication and IP whitelisting for secure access.
- **Enhanced Customer Experience**: Simplifies bill payment workflows through integration.

---

## 3. Base URLs

### UAT / Sandbox Environment
- **Operator Code Fetch API**:  
  `https://sandbox-api.trusthub.in/electricity-operator-code`

- **Electricity Bill API**:  
  `https://sandbox-api.trusthub.in/electricity-bill`

---

### Production Environment
- **Operator Code Fetch API**:  
  `https://api.trusthub.in/electricity-operator-code`

- **Electricity Bill API**:  
  `https://api.trusthub.in/electricity-bill`

---

## 4. Authentication & Security

### API Key Details
- **Authentication Method**: API Key
- **Header Parameter**:  
  `x-api-key: [API key provided by TransBnk after activation and IP whitelisting]`

---

### Required Headers
- `Authorization`: API Key in header (`x-api-key`)
- `Content-Type`:  
  `application/json; charset=utf-8`

---

### Security Measures
- **IP Whitelisting**:  
  Access to the API is restricted to whitelisted IP addresses only.
- **API Key Validation**:  
  Requests without a valid API key will return:  
  ```json
  { "message": "Forbidden" }


  

## 5. Rate Limits & Quotas

### Requests per Minute/Hour
- **Not specified in the current API documentation.**

### Throttling Behavior
- **Not mentioned in the provided specification.**
- It is recommended to confirm with TransBnk support for any applicable rate limits or throttling policies.

---

## 6. Request Structure

### HTTP Methods
- **Operator Code Fetch API**: `GET`
- **Electricity Bill API**: `POST`

---

### Endpoint URLs
#### UAT / Sandbox:
- **Operator Code Fetch**:  
  `https://sandbox-api.trusthub.in/electricity-operator-code`
- **Electricity Bill**:  
  `https://sandbox-api.trusthub.in/electricity-bill`

#### Production:
- **Operator Code Fetch**:  
  `https://api.trusthub.in/electricity-operator-code`
- **Electricity Bill**:  
  `https://api.trusthub.in/electricity-bill`

---

### Required Headers
- `x-api-key: [API key provided by TransBnk after activation and IP whitelisting]`
- `Content-Type: application/json; charset=utf-8`

---

### Request Body Format (for Electricity Bill API)
```json
{
  "id_number": "String",        // CA number (Required)
  "operator_code": "String"     // Operator code (Required)
}

```
--- 

### Request Body Parameters

| Field Name     | Required | Type   | Description    |
|---------------|----------|--------|---------------|
| id_number     | Yes      | String | CA number     |
| operator_code | Yes      | String | Operator code |

---

## 7. Response Structure

### Response Format
- **Format**: JSON

---

### Field Descriptions

| Field Name      | Type    | Description                          |
|-----------------|---------|--------------------------------------|
| client_id       | String  | Client ID                           |
| customer_id     | String  | Customer ID                         |
| operator_code   | String  | Operator code fetched from API      |
| state           | String  | State                               |
| full_name       | String  | Customer's full name                |
| address         | String  | Customer's address                  |
| mobile          | String  | Mobile number                       |
| user_email      | String  | Email address                       |
| bill_amount     | String  | Bill amount                         |
| bill_number     | String  | Bill number                         |
| document_link   | String  | Link to user document               |
| status_code     | Number  | HTTP status code                    |
| success         | Boolean | Indicates success or failure        |
| message         | String  | Response message                    |
| message_code    | String  | Message code                        |

---

### Example Response
```json
{
  "data": {
    "client_id": "electricity_jBxiqjAGXuymlqlbrOOb",
    "customer_id": "17000346322745",
    "operator_code": "MH",
    "state": "maharashtra",
    "full_name": "SUKHWANI",
    "address": "COLONY SOLAPUR ROAD NR LAD GIRNI SHEWALWADI 412307",
    "mobile": null,
    "user_email": null,
    "bill_amount": "1,280.00",
    "bill_number": null,
    "document_link": null
  },
  "status_code": 200,
  "success": true,
  "message": "Success",
  "message_code": "success"
}

```
---
## 8. Error Handling

### Common Error Codes and Messages

| HTTP Status Code | Message                                      | Description                                      |
|------------------|---------------------------------------------|--------------------------------------------------|
| 403              | {"message": "Forbidden"}                  | Missing or incorrect API key, or wrong HTTP method |
| 400              | {"message": "Invalid request body"}       | Empty or incorrect request body sent            |
| 401              | {"Message": "User: anonymous is not authorized to perform: execute-api:Invoke on resource…"} | IP not whitelisted                              |
| 504              | {"message": "Endpoint request timed out"} | Upstream service provider endpoint not responding |

---

### Example Error Responses

**Missing or Incorrect API Key / Wrong Method**
```json
{
  "message": "Forbidden"
}
```
**Invalid Request Body**

```json

{
  "message": "Invalid request body"
}

```
**IP Not Whitelisted**

```json


{
  "Message": "User: anonymous is not authorized to perform: execute-api:Invoke on resource…"
}
```
**Timeout**

```json


{
  "message": "Endpoint request timed out"
}
```
---
## 9. Integration Flow Diagram 
(Can be added)

---
## 10. Pagination & Filtering

### Handling Large Datasets
- **Not applicable** for this API as per the current specification.
- The API endpoints are designed to:
  - Fetch operator codes for states (small static dataset).
  - Retrieve a single electricity bill based on CA number and operator code.
- **Pagination and filtering are not supported** in the current version.

### Recommendation
If future versions include bulk bill retrieval or large datasets:
- Implement query parameters such as:
  - `page` (for page number)
  - `limit` (for number of records per page)
  - `filter` (for filtering by state, operator, etc.)
- Ensure proper response metadata:
  - `total_records`
  - `current_page`
  - `total_pages`

---

## 11. Versioning & Changelog

### Current Version
- **Version:** V1.0
- **Release Date:** 13-May-2024

---

### Changes from Previous Versions
- **First Release**
  - Initial version of the TransBnk Electricity Bill API.
  - Features included:
    - **Operator Code Fetch API** (GET): Retrieve operator codes for states.
    - **Electricity Bill API** (POST): Fetch electricity bill details using CA number and operator code.
  - Security:
    - API Key-based authentication.
    - IP whitelisting.
  - Response format: JSON.
  - Error handling for invalid API key, request body, IP restrictions, and timeout.

---

### Notes
- No previous versions exist; this is the first official release.

---


## 12. Best Practices

### Retry Logic
- Implement **exponential backoff** for retries in case of transient errors (e.g., network issues or timeout).
- Avoid infinite retry loops; set a maximum retry limit (e.g., 3 attempts).
- Do not retry on client-side errors (4xx status codes like `403 Forbidden` or `400 Invalid request body`).

---

### Timeout Handling
- Set a reasonable timeout for API requests (e.g., 30 seconds).
- Handle `504 Gateway Timeout` gracefully by:
  - Logging the error.
  - Informing the user about the delay.
  - Retrying after a short interval if appropriate.

---

### Security Recommendations
- **API Key Management**:
  - Keep your API key confidential; never expose it in client-side code.
  - Rotate API keys periodically.
- **IP Whitelisting**:
  - Ensure requests originate only from whitelisted IP addresses.
- **Use HTTPS**:
  - All API calls should use secure HTTPS endpoints.
- **Validate Inputs**:
  - Sanitize and validate CA numbers and operator codes before sending requests.
- **Error Logging**:
  - Log errors securely without exposing sensitive data.

---

### Additional Tips
- Monitor API usage and set alerts for unusual activity.
- Implement rate limiting on your side to avoid overwhelming the API.

---


## 13. Support & Contact

### UAT / PROD Portal Links
- **UAT / Sandbox API Portal**:  
  https://sandbox-api.trusthub.in
- **Production API Portal**:  
  https://api.trusthub.in

---

### Support Contact
- **Email**: support@trusthub.in
- **Escalation Matrix**:
  1. **Level 1**: API Integration Support Team  
     Email: support@trusthub.in
  2. **Level 2**: Technical Escalation  
     Email: techlead@trusthub.in
  3. **Level 3**: Account Manager  
     Contact via official TransBnk representative.

---

### Additional Resources
- API Documentation: Available on request from TransBnk.
- SLA & Response Times: Contact support for details.
---


## 13. Support & Contact

### UAT / PROD Portal Links
- **UAT / Sandbox API Portal**:  
  https://sandbox-api.trusthub.in
- **Production API Portal**:  
  https://api.trusthub.in

---

### Support Contact
- **Email**: support@trusthub.in
- **Escalation Matrix**:
  1. **Level 1**: API Integration Support Team  
     Email: support@trusthub.in
  2. **Level 2**: Technical Escalation  
     Email: techlead@trusthub.in
  3. **Level 3**: Account Manager  
     Contact via official TransBnk representative.

---

### Additional Resources
- API Documentation: Available on request from TransBnk.
- SLA & Response Times: Contact support for details.



