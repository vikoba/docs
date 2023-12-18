# Kikoba Update API

This API allows users to perform CRUD operations on a Kikoba entity. Users can create a new Kikoba, update an existing one, retrieve details of a Kikoba, or delete a Kikoba.

## Endpoint

- `api/kikoba/update/`

## Authentication

- Requires authentication using a valid token.

## Methods

### 1. Create a new Kikoba

- **Method:** POST
- **Endpoint:** `api/kikoba/update/`
- **Parameters:**
  - `kikoba_name` (string, required): The name of the Kikoba.
  - `location` (string, required): The location of the Kikoba.
- **Response:**
  - Status Code: 201 Created
  - Body: `{ "message": "Kikoba created successfully" }`
  - Possible Errors:
    - 400 Bad Request: Invalid input or duplicate Kikoba name.
    - 401 Unauthorized: Authentication failed.

### 2. Delete a Kikoba

- **Method:** DELETE
- **Endpoint:** `api/kikoba/update/`
- **Parameters:**
  - `kikoba_id` (string, required): The ID of the Kikoba to be deleted.
- **Response:**
  - Status Code: 200 OK
  - Body: `{ "detail": "Deleted successfully" }`
  - Possible Errors:
    - 400 Bad Request: Invalid input or user not authorized to delete.
    - 401 Unauthorized: Authentication failed.
    - 404 Not Found: Kikoba with the provided ID does not exist.

### 3. Update a Kikoba

- **Method:** PATCH
- **Endpoint:** `api/kikoba/update/`
- **Parameters:**
  - `kikoba_id` (string, required): The ID of the Kikoba to be updated.
  - Additional parameters for updating specific fields (e.g., `kikoba_name`, `location`).
- **Response:**
  - Status Code: 200 OK
  - Body: `{ "detail": "Updated successfully" }`
  - Possible Errors:
    - 400 Bad Request: Invalid input or user not authorized to update.
    - 401 Unauthorized: Authentication failed.
    - 404 Not Found: Kikoba with the provided ID does not exist.

### 4. Retrieve details of a Kikoba

- **Method:** GET
- **Endpoint:** `api/kikoba/update/`
- **Parameters:**
  - `kikoba_id` (string, required): The ID of the Kikoba to retrieve details.
- **Response:**
  - Status Code: 200 OK
  - Body: JSON object containing details of the Kikoba.
  - Possible Errors:
    - 400 Bad Request: Invalid input or user not authorized to retrieve details.
    - 401 Unauthorized: Authentication failed.
    - 404 Not Found: Kikoba with the provided ID does not exist.

### 5. Invalid Request Method

- **Method:** Any method other than POST, DELETE, PATCH, or GET
- **Endpoint:** `api/kikoba/update/`
- **Response:**
  - Status Code: 400 Bad Request
  - Body: `{ "detail": "Invalid request method" }`

## Code Implementation Notes

- Ensure the user is authenticated using a valid token before making requests.
- Use appropriate request methods and parameters as described in the documentation.
- Handle possible errors such as authentication failure, invalid input, user not authorized, or resource not found.
