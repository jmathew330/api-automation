# 🏨 RESTful Booker API - Postman Collection

This Postman collection provides **automated API tests** for managing **Booking** resources, covering creating, updating, partially updating, and deleting bookings. It validates API functionality, response correctness, authentication, and performance.

---

## 🚀 Endpoints Covered

| Endpoint                    | HTTP Method | Description                          |
|-----------------------------|-------------|------------------------------------|
| `/booking`                  | POST        | ➕ Create a new booking             |
| `/booking/{{bookingId}}`    | GET         | 🔍 Retrieve booking details by ID  |
| `/booking/{{bookingId}}`    | PUT         | 🔄 Full update of an existing booking |
| `/booking/{{bookingId}}`    | PATCH       | ✏️ Partial update of booking fields |
| `/booking/{{bookingId}}`    | DELETE      | 🗑️ Delete a booking                |

---

## 📝 Requests and Tests

### 1. Create Booking (POST `/booking`)

- 🆕 Creates a new booking with full details.
- ✅ Tests include:
  - Status code is 200 (or 201).
  - ⏱️ Response time under 500ms.
  - 🔍 Response contains booking details and booking ID.
  - 📊 Validates required fields and data types.
- 🔧 Sets environment variables (`bookingId`, `firstName`, `lastName`, etc.) for later use.

---

### 2. Get Booking (GET `/booking/{{bookingId}}`)

- 📖 Retrieves booking details by ID.
- ✅ Tests include:
  - Status code 200.
  - ⏱️ Response time under 500ms.
  - 🔍 Verifies all expected fields exist.
  - 📐 Validates data types and content.

---

### 3. Full Update Booking (PUT `/booking/{{bookingId}}`)

- 🔄 Fully updates a booking with all fields.
- 🔐 Requires authentication token in cookie header.
- ✅ Tests validate status, fields, and updated values.

---

### 4. Partial Update Booking (PATCH `/booking/{{bookingId}}`)

- ✏️ Partially updates fields like `firstname` and `lastname`.
- 🧠 Uses pre-request scripts to extract updated values.
- ✅ Tests include:
  - Status code 200.
  - ⏱️ Response time under 500ms.
  - 🔍 All expected fields are present and not null.
  - 📐 Data types validated.
  - ✅ Updated values match the request.
  - 🔐 Negative test: PATCH without token returns 403 Forbidden.

---

### 5. Delete Booking (DELETE `/booking/{{bookingId}}`)

- 🗑️ Deletes the specified booking.
- ✅ Tests include:
  - Status code 201 (or per API spec).
  - ⏱️ Response time under 500ms.
  - 🧹 Confirms booking is deleted by GET returning 404.
  - 🔐 Negative test: DELETE without token returns 403 Forbidden.
  - 🧼 Cleans up all related environment variables after deletion.

---

## 🌍 Environment Variables

- `baseUrl`: 🌐 Base URL of the API.
- `token`: 🔑 Authentication token (sent in cookie header).
- `bookingId`: 🆔 ID of the current booking.
- Other temp variables: `firstName`, `lastName`, `updatedFirstName`, etc., for validation.

## 📊 Execution Summary

<img width="800" alt="Screen Shot 2025-09-30 at 3 16 51 PM" src="https://github.com/user-attachments/assets/dcff25fa-9ad1-4620-ad03-4f4ae99b5c5e" />

<img width="800" alt="Screen Shot 2025-09-30 at 3 17 10 PM" src="https://github.com/user-attachments/assets/746206fb-82e6-4bcf-a776-9da952b87fc2" />

---

## ⚙️ How to Use

1. **Setup Environment:**  
   Create/import a Postman environment and define:
   - `baseUrl`
   - `token`  
   (Note: `bookingId` is set dynamically after creating a booking.)

2. **Run Requests in Order:**  
   1️⃣ Create Booking  
   2️⃣ Get Booking  
   3️⃣ PUT Booking (full update)  
   4️⃣ PATCH Booking (partial update)  
   5️⃣ DELETE Booking (clean up)

3. **Review Tests:**  
   Check the **Tests** tab after each request to see validation results.

---

## 💡 Notes

- Authentication uses a `token` in the Cookie header for secured endpoints.
- Performance validated to ensure response times < 500ms.
- Negative tests ensure proper handling of unauthenticated requests.
- Environment variables are cleaned up after deletion to avoid clutter.
- Modify `baseUrl` and token values per your setup.


