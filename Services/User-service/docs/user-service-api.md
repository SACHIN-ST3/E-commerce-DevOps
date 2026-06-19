# User Service API Design

## Authentication APIs

### Register User

POST /api/auth/register

Purpose:
Create a new customer account.

Request:

{
"fullName": "Stephen",
"email": "[stephen@example.com](mailto:stephen@example.com)",
"password": "Password123",
"phone": "9876543210"
}

Response:

{
"message": "User registered successfully"
}

---

### Login User

POST /api/auth/login

Purpose:
Authenticate user and return JWT token.

Request:

{
"email": "[stephen@example.com](mailto:stephen@example.com)",
"password": "Password123"
}

Response:

{
"token": "jwt-token"
}

---

## User APIs

### Get Profile

GET /api/users/profile

Purpose:
Return current logged-in user's profile.

---

### Update Profile

PUT /api/users/profile

Purpose:
Update customer profile information.

---

## Address APIs

### Get Addresses

GET /api/users/addresses

Purpose:
Get all addresses for current user.

---

### Add Address

POST /api/users/addresses

Purpose:
Create a new delivery address.

---

### Update Address

PUT /api/users/addresses/{id}

Purpose:
Update existing address.

---

### Delete Address

DELETE /api/users/addresses/{id}

Purpose:
Remove address.
