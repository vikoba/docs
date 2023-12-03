# API Documentation: Verify OTP and Generate Token

## Overview

This API endpoint is designed to verify the OTP (One-Time Password) provided by the user, and upon successful verification, it generates a JWT (JSON Web Token) for authentication. The JWT includes a refresh token and an access token. Additionally, it provides information about whether the user is a new member.

## Endpoint

- **URL:** `/api/account/verify-otp-and-generate-token/`
- **Method:** POST

## Request

### Body

- **phone_number** (required): User's phone number. Should be a valid phone number.
- **otp** (required): OTP received by the user. Should be a 6-character string.

Example:

```json
{
  "phone_number": "+255679190720",
  "otp": "123456"
}
```

## Errors

### 1. Invalid OTP Length

- **Status Code:** 400 Bad Request
- **Response:**
  ```json
  {
    "otp": [
      "Ensure this field has no more than 6 characters."
    ]
  }
  ```

### 2. Invalid Phone Number Format

- **Status Code:** 400 Bad Request
- **Response:**
  ```json
  {
    "phone_number": [
      "Enter a valid phone number."
    ]
  }
  ```

### 3. Invalid OTP

- **Status Code:** 400 Bad Request
- **Response:**
  ```json
  {
    "detail": "Invalid OTP"
  }
  ```

## Success

- **Status Code:** 200 OK
- **Response:**
  ```json
  {
    "refresh": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
    "access": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
    "new_member": false
  }
  ```

## User Flow

1. User makes a POST request to the `/api/account/verify-otp-and-generate-token/` endpoint with their phone number and OTP in the request body.
2. The API validates the OTP and phone number.
    - If the OTP is not in a valid format, it responds with an error message.
    - If the phone number is not in a valid format, it responds with an error message.
3. If the OTP and phone number are valid, the API checks if the OTP matches the stored OTP for the user.
    - If the OTP is valid, the user's OTP is cleared, and a JWT token is generated.
    - If the OTP is invalid, it responds with an error message.
4. The API responds with the generated JWT token and indicates whether the user is a new member.

## Example Usage (cURL)

```bash
curl -X POST \
  -H "Content-Type: application/json" \
  -d '{"phone_number": "+255679190720", "otp": "123456"}' \
  http://example.com/api/account/verify-otp-and-generate-token/
```

## Example Usage (Python - requests library)

```python
import requests

url = "http://example.com/api/account/verify-otp-and-generate-token/"
data = {"phone_number": "+255679190720", "otp": "123456"}

response = requests.post(url, json=data)
print(response.json())
```

## Possible Improvements

- Include detailed error messages for specific validation failures.
- Implement rate limiting or CAPTCHA to prevent abuse of the verification endpoint.
- Provide additional information in the JWT payload based on your application requirements.
