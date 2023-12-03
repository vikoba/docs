# API Documentation: Update User Profile

## Overview

This API endpoint allows authenticated users to update their profile information. Users can make a PATCH request to update specific fields in their profile. The endpoint requires authentication, ensuring that only authenticated users can modify their profiles.

## Endpoint

- **URL:** `/api/profile/update/`
- **Method:** PATCH
- **Authentication:** Bearer Token

## Request

### Body

The request body should contain the fields that the user wants to update.

Example:

```json
{
  "first_name": "John",
  "last_name": "Doe",
  "gender": 1,
  "avatar": (binary file),
  "marital_status": 2,
  "street": "123 Main Street"
  // Include other fields as needed
}
```

### Fields
- **first_name, middle_name, last_name:** User's names.
- **phone_number:** User's phone number.
- **nida_number:** User's National Identification Number.
- **birth_date:** User's date of birth (string representing a date).
- **marital_status:** User's marital status (integer).
- **gender:** User's gender (integer).
- **job:** User's job.
- **region:** User's region.
- **street:** User's street address.
- **house:** User's house number.
- **avatar:** User's avatar image (binary file).
- **national_identification:** User's national identification document (binary file).
- **letter:** User's letter document (binary file).

## Errors

### 1. Field Validation Errors

- **Status Code:** 400 Bad Request
- **Response:**
  ```json
  {
    "field_name": ["Error message 1", "Error message 2", ...]
  }
  ```

### 2. File Type Validation Error

- **Status Code:** 400 Bad Request
- **Response:**
  ```json
  {
    "field_name": ["Invalid file type. Allowed types are JPEG and PNG."]
  }
  ```

### 3. File Size Validation Error

- **Status Code:** 400 Bad Request
- **Response:**
  ```json
  {
    "field_name": ["File size exceeds the maximum allowed size (5 MB)."]
  }
  ```

### 4. Null Field Validation Error

- **Status Code:** 400 Bad Request
- **Response:**
  ```json
  {
    "field_name": ["Field cannot be null."]
  }
  ```

## Success

- **Status Code:** 200 OK
- **Response:**
  ```json
  {
    "message": "Profile updated successfully"
  }
  ```

## User Flow

1. Authenticated user makes a PATCH request to the `/api/profile/update/` endpoint with the desired fields in the request body.
2. The API validates the fields based on their types and specific rules.
    - If there are validation errors, the API responds with detailed error messages.
3. If the validation is successful, the API updates the user's profile information.
4. The API responds with a success message indicating that the profile has been updated successfully.

## Example Usage (cURL)

```bash
curl -X PATCH \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer YOUR_ACCESS_TOKEN" \
  -d '{"first_name": "John", "last_name": "Doe", "gender": 1, "avatar": (binary file), "marital_status": 2, "street": "123 Main Street"}' \
  http://example.com/api/profile/update/
```

## Example Usage (Python - requests library)

```python
import requests

url = "http://example.com/api/profile/update/"
headers = {
    "Content-Type": "application/json",
    "Authorization": "Bearer YOUR_ACCESS_TOKEN"
}
data = {
    "first_name": "John",
    "last_name": "Doe",
    "gender": 1,
    "avatar": (binary file),
    "marital_status": 2,
    "street": "123 Main Street"
}
response = requests.patch(url, headers=headers, json=data)
print(response.json())
```

## Possible Improvements

- Provide more detailed error messages for specific validation failures.
- Implement additional file type checks or validations for uploaded documents.
- Include documentation for additional fields if necessary.
