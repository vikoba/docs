# API Documentation: User Registration

## Overview

This API endpoint is designed to handle user registration by sending an OTP (One-Time Password) to the provided phone number. The user enters their phone number, and upon successful validation, an OTP is generated, sent to the user, and saved in the database.

## Endpoint

- **URL:** `/api/account/user-registration/`
- **Method:** POST

## Request

### Body

- **phone_number** (required): User's phone number. Should be a valid phone number starting with the country code.

Example:

```json
{
  "phone_number": "+1234567890"
}
```

## Errors

### 1. Missing Phone Number

- **Status Code:** 400 Bad Request
- **Response:**
  ```json
  {
    "phone_number": [
      "This field is required."
    ]
  }
  ```

### 2. Blank Phone Number

- **Status Code:** 400 Bad Request
- **Response:**
  ```json
  {
    "phone_number": [
      "This field may not be blank."
    ]
  }
  ```

### 3. Invalid Phone Number Format

- **Status Code:** 400 Bad Request
- **Response:**
  ```json
  {
    "phone_number": [
      "Enter a valid phone number."
    ]
  }
  ```

## Success

- **Status Code:** 200 OK
- **Response:**
  ```json
  {
    "detail": "OTP sent successfully"
  }
  ```

## User Flow

1. User makes a POST request to the `/api/account/user-registration/` endpoint with their phone number in the request body.
2. The API validates the phone number.
    - If the phone number is missing or blank, it responds with an appropriate error message.
    - If the phone number is not in a valid format, it responds with an error message.
3. If the phone number is valid, an OTP is generated and sent to the user.
4. The OTP is saved to the user model in the database.
5. The API responds with a success message indicating that the OTP has been sent successfully.

## Example Usage (cURL)

```bash
curl -X POST \
  -H "Content-Type: application/json" \
  -d '{"phone_number": "+1234567890"}' \
  http://example.com/api/account/user-registration/
```

## Example Usage (Python - requests library)

```python
import requests

url = "http://example.com/api/account/user-registration/"
data = {"phone_number": "+1234567890"}

response = requests.post(url, json=data)
print(response.json())
```

## Possible Improvements

- Implement additional validation for phone numbers to ensure correct formatting.
- Provide more detailed error messages for specific validation failures.
- Implement rate limiting or CAPTCHA to prevent abuse of the registration endpoint.
- Include documentation for handling OTP verification in subsequent steps.
