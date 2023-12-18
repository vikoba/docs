# Kikoba Post API

This API allows users to perform operations related to Kikoba posts. Users can create a new post within a Kikoba, retrieve posts, or delete a post.

## Endpoint

- `api/kikoba/post/`

## Authentication

- Requires authentication using a valid token.

## Methods

### 1. Create a new Kikoba Post

- **Method:** POST
- **Endpoint:** `api/kikoba/post/`
- **Parameters:**
  - `kikoba_id` (string, required): The ID of the Kikoba where the post will be created.
  - `title` (string, required): The title of the post.
  - `body` (string, required): The body content of the post.
- **Response:**
  - Status Code: 201 Created
  - Body: `{ "detail": "Created successfully" }`
  - Possible Errors:
    - 400 Bad Request: Invalid input, user not authorized, or resource not found.
    - 401 Unauthorized: Authentication failed.
    - 404 Not Found: Kikoba with the provided ID does not exist.

### 2. Retrieve Kikoba Posts

- **Method:** GET
- **Endpoint:** `api/kikoba/post/`
- **Parameters:**
  - `kikoba_id` (string, required): The ID of the Kikoba to retrieve posts.
- **Response:**
  - Status Code: 200 OK
  - Body: JSON array containing details of Kikoba posts.
  - Possible Errors:
    - 400 Bad Request: Invalid input or resource not found.
    - 401 Unauthorized: Authentication failed.
    - 404 Not Found: Kikoba with the provided ID does not exist.

### 3. Delete a Kikoba Post

- **Method:** DELETE
- **Endpoint:** `api/kikoba/post/`
- **Parameters:**
  - `kikoba_id` (string, required): The ID of the Kikoba where the post will be deleted.
  - `post_id` (string, required): The ID of the post to be deleted.
- **Response:**
  - Status Code: 200 OK
  - Body: `{ "detail": "Deleted successfully" }`
  - Possible Errors:
    - 400 Bad Request: Invalid input, user not authorized, or resource not found.
    - 401 Unauthorized: Authentication failed.
    - 404 Not Found: Kikoba with the provided ID or post with the provided ID does not exist.

## Code Implementation Notes

- Ensure the user is authenticated using a valid token before making requests.
- Use appropriate request methods and parameters as described in the documentation.
- Handle possible errors such as authentication failure, invalid input, user not authorized, or resource not found.
