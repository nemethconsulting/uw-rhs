# Error Codes and Troubleshooting Steps for the Recreational Hockey League API

## 400: Bad Request
- **What It Means**: The request is malformed (e.g., missing required fields, invalid JSON syntax).
- **Example**: Posting a team without a required `id` field.
- **Troubleshooting**: 
  - Check the JSON structure and ensure all required fields are present.
  - Validate with an online JSON validator.

## 404: Not Found
- **What It Means**: The requested resource does not exist (e.g., querying `/games/999` when `id=999` does not exist).
- **Example**: Attempting to `PATCH` a team or game with an incorrect `id`.
- **Troubleshooting**: 
  - Verify the endpoint URL and `id` values in the request.
  - Use a `GET` request to check the resource exists before making updates.

## 405: Method Not Allowed
- **What It Means**: The HTTP method used is not supported by the endpoint (e.g., `POST` on a non-modifiable endpoint).
- **Example**: Using `DELETE` on `/teams` when the server does not allow deletions.
- **Troubleshooting**: 
  - Confirm the method is supported for the endpoint.
  - Review the API documentation for allowed methods.

## 409: Conflict
- **What It Means**: The request conflicts with the current state of the resource (e.g., duplicate `id` values).
- **Example**: Attempting to add a new team with an existing `id`.
- **Troubleshooting**: 
  - Check for existing resources with the same `id` using a `GET` request.
  - Ensure new resources have unique identifiers.

## 500: Internal Server Error
- **What It Means**: An unexpected error occurred on the server (e.g., malformed middleware or database file corruption).
- **Example**: Middleware attempting to process invalid data causes a server crash.
- **Troubleshooting**: 
  - Check the server logs for more details on the error.
  - Validate the integrity of `db.json` and ensure no malformed data.

## 422: Unprocessable Entity
- **What It Means**: The server understands the request but cannot process the contained instructions (e.g., invalid `finalScore` format).
- **Example**: Sending `"winLossRatio": "invalid-format"` when the server expects `"X-Y-Z"`.
- **Troubleshooting**: 
  - Confirm the field formats and data types match the API's expected structure.
  - Adjust the request payload to conform to the schema.

## 401: Unauthorized
- **What It Means**: The request is missing or contains an invalid authentication token.
- **Example**: Attempting to modify a game without a valid token.
- **Troubleshooting**: 
  - Ensure a valid JSON Web Token (JWT) is included in the `Authorization` header.
  - Check if the token has expired or lacks the required permissions.

## 403: Forbidden
- **What It Means**: The client is authenticated but does not have permission to perform the action.
- **Example**: A user with read-only access trying to `POST` or `PATCH` resources.
- **Troubleshooting**: 
  - Verify the user's permissions for the requested operation.
  - Contact the API administrator to adjust access levels if needed.

## 413: Payload Too Large
- **What It Means**: The request body exceeds the server's maximum allowed size.
- **Example**: Sending an excessively large nested array of games.
- **Troubleshooting**: 
  - Reduce the size of the payload by batching the data into smaller requests.
  - Check the server's payload size limits and adjust configuration if possible.

