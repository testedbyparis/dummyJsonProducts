# 🌐 API Testing Portfolio: Dummy JSON Products

## 🚀 Project Overview

This project showcases a robust **API testing strategy** applied to the public [Dummy JSON Products API](https://dummyjson.com/docs/products). It demonstrates proficiency in multiple testing types, including **End-to-End (E2E) flows, Functional Validation, Contract Testing, Negative Testing, and Schema Validation.**

The entire test suite is implemented using Postman and its native JavaScript testing framework.

## 🛠️ Testing Methodology & Coverage

The tests are organized to reflect a comprehensive approach to quality assurance (QA), covering the full scope of a modern REST API.

| Category | Description | Key Techniques Demonstrated |
| --- | --- | --- |
| **End-to-End (E2E) Flows** | Simulates multi-step user journeys by chaining API calls and validating data consistency across requests. | Dynamic variable handling (pm.environment.set), data extraction, multi-step assertions. |
| **Functional / Contract Testing (CRUD Simulation)** | Verifies the expected behavior and response contract for core Create, Update, and Delete operations. | POST, PUT, DELETE requests, validating that the response body accurately reflects the data sent. |
| **Negative Testing** | Ensures the API fails gracefully and predictably when given invalid input or routes. | Asserting 404 Not Found status codes and specific error messages. |
| **Schema Validation** | Asserting 404 Not Found status codes and specific error messages. | Using Postman's tv4 library and a predefined JSON Schema. |  

## 🧪 Test Scenarios Implemented

The suite covers the following 12 key requests, grouped by function:

1.  **End-to-End Flows (E2E)**  

These scenarios validate data integrity across multiple endpoints.  

- **E2E Search and Details:** Verifies that a product found in the main search (GET /products or GET /search?q=...) has matching data when requested individually (GET /products/:id).

- **E2E Data Filtering and Validation:** Searches for a specific category (GET /products/category/smartphones) and iterates through the entire response list, asserting that every item correctly contains the specified category field.

2.  **Functional and Contract Tests (CRUD)**  

These scenarios confirm the expected immediate response for state-changing operations (simulated by Dummy JSON).  

- **Functional Test: Simulate Creation (POST):** Sends a new product payload and confirms the API returns a 200/201 status and reflects the sent data and a new simulated id in the response.  

- **Functional Test: Simulate Edition (PUT):** Sends a partial update payload (PUT /products/1) and confirms the response body contains the updated title/price.  

- **Functional Test: Simulate Deletion (DELETE):** Executes the DELETE /products/1 endpoint and verifies the 200 status, along with confirmation fields like isDeleted: true in the response payload.  

3.  **Validation and Negative Tests**  

These ensure robust data handling and error control.  

- **Schema Validation:** Ensures the GET /products/1 response strictly adheres to the predefined JSON schema (fields, types, and required properties).  

- **Get All Categories Validation:** Validates that the list of categories (GET /products/categories) is returned as an array and contains required structural elements (e.g., objects with a slug property).  

- **Negative Test: Non-Existent ID:** Checks that requesting a non-existent product ID (GET /products/9999) results in a predictable 404 Not Found status.  

- **Negative Test: Invalid Route:** Ensures that accessing an invalid path (GET /nonexistent-route) results in a 404 Not Found status.  

## 🚀 Automation & CI/CD Readiness (New!)

This project is configured for seamless automation, emphasizing a shift-left QA approach:

1.  **Newman Integration:** The entire collection is executable via the command line using **Newman**.
2.  **HTML Reporting:** Generates detailed HTML reports using `newman-reporter-htmlextra` for easy failure analysis.
3.  **CI/CD Pipeline:** **A GitHub Actions workflow is fully implemented** to automatically run the complete test suite on every code push, establishing an automated quality gate for the API contract.

## 📋 Getting Started

### Prerequisites  

* **[Postman](https://www.postman.com/downloads/)** installed.
* **[Node.js](https://nodejs.org/en)** installed (required for Newman).

#### Installation and Setup

1.  **Clone the Repository:** Download the project files (including the Collection and Environment JSON files) from GitHub.
2.  **Import to Postman:** In Postman, click **Import** and select the Collection JSON file.
3.  **Setup Environment:**
    * Ensure an environment named `"dummyJsonEnv"` is active.
    * The base URL variable (`{{baseUrl}}`) must be set to `https://dummyjson.com`.
4.  **Install Newman (Command Line Runner):** Install Newman and the HTML EXTRA reporter globally via npm:

    ```bash
    npm install -g newman newman-reporter-htmlextra
    ```

#### Running Tests & Reviewing Reports

You can execute the test suite in two ways:

##### A. Via Postman GUI (Manual Execution)

Select the imported Collection, click **Run** (or `...` $\to$ **Run collection**), and execute the entire test suite.

##### B. Via Newman (Automated Execution)

Run the tests from your terminal (ensure you are in the directory containing your collection/environment files):

```bash
# Replace 'Collection.json' and 'Environment.json' with your actual filenames
newman run <Collection_File.json> -e <Environment_File.json> --reporters cli,htmlextra --reporter-htmlextra-export newman/newman-report.html
```

##### Viewing the Report  
After execution, a folder named newman will be created in your project root, containing a detailed HTML report file (newman-report.html). Open this file in any web browser to view the structured results, including pass/fail status for every test and assertion.