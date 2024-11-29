<div style="display: flex; align-items: center; justify-content: space-between;">
  <h1>Error Codes and Troubleshooting Steps for the Recreational Hockey League API
</h1>
  <img src="rhs-logo_4x4.jpeg" alt="Rec Hockey League Logo" style="width: 100px; height: 100px; margin-left: 20px;">
</div>

Review this page to see causes and fixes for common error codes.

## Table of Contents
1. [400: Bad Request](#1)
2. [404: Not Found](#2)
3. [405: Method Not Allowed](#3)
4. [409: Conflict](#4)
5. [500: Internal Server Error](#5)
6. [422: Unprocessable Entity](#6)
7. [401: Unauthorized](#7)
8. [403: Forbidden](#8)
9. [413: Payload Too Large](#9)
10. [Back to Main Menu](nav.md)

<a id="1"></a>
## 400: Bad Request
- **What It Means**: The request is malformed (e.g., missing required fields, invalid JSON syntax).
- **Example**: Posting a team without a required `id` field.
- **Troubleshooting**: 
  - Check the JSON structure and ensure all required fields are present.
  - Validate with an online JSON validator.

<a id="2"></a>
## 404: Not Found
- **What It Means**: The requested resource does not exist (e.g., querying `/games/999` when `id=999` does not exist).
- **Example**: Attempting to `PATCH` a team or game with an incorrect `id`.
- **Troubleshooting**: 
  - Verify the endpoint URL and `id` values in the request.
  - Use a `GET` request to check the resource exists before making updates.

<a id="3"></a>
## 405: Method Not Allowed
- **What It Means**: The HTTP method used is not supported by the endpoint (e.g., `POST` on a non-modifiable endpoint).
- **Example**: Using `DELETE` on `/teams` when the server does not allow deletions.
- **Troubleshooting**: 
  - Confirm the method is supported for the endpoint.
  - Review the API documentation for allowed methods.

<a id="4"></a>
## 409: Conflict
- **What It Means**: The request conflicts with the current state of the resource (e.g., duplicate `id` values).
- **Example**: Attempting to add a new team with an existing `id`.
- **Troubleshooting**: 
  - Check for existing resources with the same `id` using a `GET` request.
  - Ensure new resources have unique identifiers.

<a id="5"></a>
## 500: Internal Server Error
- **What It Means**: An unexpected error occurred on the server (e.g., malformed middleware or database file corruption).
- **Example**: Middleware attempting to process invalid data causes a server crash.
- **Troubleshooting**: 
  - Check the server logs for more details on the error.
  - Validate the integrity of `db.json` and ensure no malformed data.

<a id="6"></a>
## 422: Unprocessable Entity
- **What It Means**: The server understands the request but cannot process the contained instructions (e.g., invalid `finalScore` format).
- **Example**: Sending `"winLossRatio": "invalid-format"` when the server expects `"X-Y-Z"`.
- **Troubleshooting**: 
  - Confirm the field formats and data types match the API's expected structure.
  - Adjust the request payload to conform to the schema.

<a id="7"></a>
## 401: Unauthorized
- **What It Means**: The request is missing or contains an invalid authentication token.
- **Example**: Attempting to modify a game without a valid token.
- **Troubleshooting**: 
  - Ensure a valid JSON Web Token (JWT) is included in the `Authorization` header.
  - Check if the token has expired or lacks the required permissions.

<a id="8"></a>
## 403: Forbidden
- **What It Means**: The client is authenticated but does not have permission to perform the action.
- **Example**: A user with read-only access trying to `POST` or `PATCH` resources.
- **Troubleshooting**: 
  - Verify the user's permissions for the requested operation.
  - Contact the API administrator to adjust access levels if needed.

<a id="9"></a>
## 413: Payload Too Large
- **What It Means**: The request body exceeds the server's maximum allowed size.
- **Example**: Sending an excessively large nested array of games.
- **Troubleshooting**: 
  - Reduce the size of the payload by batching the data into smaller requests.
  - Check the server's payload size limits and adjust configuration if possible.

## [Back to Main Menu](nav.md)