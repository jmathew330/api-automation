# 🧪 DummyJSON Users API - Postman Testing Suite

This project is a comprehensive API testing suite for the [DummyJSON Users API](https://dummyjson.com/users), built using **Postman**. It includes tests for:

- Getting all users
- Getting a single user by ID
- Adding a new user

The suite covers **status checks**, **response structure**, **data validation**, **schema validation**, **field presence**, **performance**, and **uniqueness**.

---

## 📂 Project Structure

- `GET /users` – Retrieve all users
- `GET /users/:id` – Retrieve a single user by ID
- `POST /users/add` – Add a new user

---

## ✅ Test Coverage

### 1. Status & Performance

- ✅ Status code is as expected (`200`, `201`)
- ⚡ Response time is under `500ms`

### 2. Response Structure Validation

- 📦 Top-level response type checks (`object`, `array`)
- 🏗️ Nested field presence checks (e.g., `hair.color`, `address.coordinates.lat`)
- 🧩 Data types are asserted using Postman's `chai` assertions

### 3. Field Value Integrity

- 🚫 Fields are **not null or undefined**
- 🔁 Unique values test (e.g., `user.id` is unique across the array)

### 4. Schema Validation

- 📜 JSON Schema-based validation using `pm.response.to.have.jsonSchema()`

### 5. Dynamic Data Validation (Single User)

- Ensures `user.id` in response matches the requested ID

---

## 📥 How to Use

### Prerequisites

- [Postman](https://www.postman.com/downloads/)
- Internet connection (API is publicly available)

### Steps

1. Import the **Postman collection** (you can create a `.json` file with the test scripts provided).
2. Set up your environment (if using variables).
3. Run the requests:
   - `GET https://dummyjson.com/users`
   - `GET https://dummyjson.com/users/:id`
   - `POST https://dummyjson.com/users/add`
4. View the **Test Results** tab to see passed/failed assertions.

---

## 🔍 Example: GET `/users` Test Breakdown

javascript
// ✅ STATUS & PERFORMANCE TESTS
pm.test("Response code is 200", () => {
    pm.response.to.have.status(200);
});
pm.test("Response time is under 500ms", () => {
    pm.expect(pm.response.responseTime).to.be.below(500);
});

// 📦 PARSE RESPONSE
const jsonData = pm.response.json();
const users = jsonData.users;

// 🏗️ STRUCTURE TESTS
pm.test("Response is an object", () => {
    pm.expect(jsonData).to.be.an("object");
});
pm.test("Users is an array", () => {
    pm.expect(users).to.be.an("array");
});

// 🧩 FIELD VALIDATION (TRUNCATED EXAMPLE)
users.forEach(user => {
    pm.expect(user).to.have.property("id");
    pm.expect(user.firstName).to.be.a("string");
    pm.expect(user.hair.color).to.not.be.oneOf([null, undefined]);
    pm.expect(user.address.coordinates.lat).to.be.a("number");
});
---

## 👤 Example: GET `/users/:id` Test Highlights

This test suite focuses on validating the structure and integrity of a single user object returned by the `GET /users/:id` endpoint.

**Validations performed:**

- ✅ Asserts that the response is a valid JSON object
- 📌 Verifies the presence of all required top-level fields
- 🧩 Validates correct data types for each field
- 🏗️ Checks the structure of nested objects (e.g., `address`, `hair`, `bank`, `company`, `crypto`)
- 🔁 Ensures the returned user ID matches the requested ID

---

## ➕ Example: POST `/users/add` Test Highlights

This test ensures that a new user can be added correctly using the `POST /users/add` endpoint.

**Validations performed:**

- ✅ Confirms a `201 Created` status code is returned
- 📦 Parses the returned object to validate successful creation
- 📌 Asserts that all critical fields are returned in the response
- 🧩 Validates nested structures such as:
  - `company.address.coordinates`
  - `hair`, `bank`, `crypto`

---

## 📚 Technologies Used

- 🧰 **Postman** – for writing and running API tests
- 🔍 **Chai.js** – Postman's built-in assertion library for writing expressive test cases
- 🔗 **[DummyJSON API](https://dummyjson.com/users/)** – a fake API for prototyping and testing

---

## 🧠 Notes

- The DummyJSON API serves **mock data** only and does **not** persist changes.
- This project is ideal for practicing and demonstrating API testing strategies.
- For production-ready testing and automation:
  - 🔁 Integrate these tests into **CI/CD pipelines** using tools like **Newman**

---

## 🚀 Running Tests via CLI (Optional)

To run the Postman test collection using Newman (Postman's CLI companion):

```bash
npm install -g newman
newman run path/to/your_collection.json
