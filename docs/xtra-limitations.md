## Our API does not dynamically update fields
...

## `PATCH' calls
Need all fields so as not to overwrite the data
...

## Nested Arrays w/ Top-Level Fields
Won't update across resources
Yes, what you're observing is indeed a limitation of json-server due to its behavior when handling nested resources (like seasonGames). When you use PATCH to update a nested field (seasonGames), json-server will replace the entire array and may not update sibling fields like winLossRatio correctly within the same PATCH request. This is because json-server treats each field in the resource independently, and it doesn't automatically merge changes between top-level fields and nested arrays.

While it may seem easier to target only the relevant fields with a `PATCH` call like the one below, the `json-server` used with the API does not natively handle deep merging of objects or arrays. You need to send all fields of data in your request, or use middleware such as `mergePatch.js` to merge arrays and nested objects properly. 

```shell
curl -X PATCH http://localhost:3000/games/5 \
-H "Content-Type: application/json" \
-d '{
  "id": 5,
  "teamName": "Seattle Kraken",
  "season": "2024-2025",
  "winLossRatio": "0-1-0",
  "seasonGames": [
    {
      "gameNumber": 1,
      "date": "2024-10-03T19:00:00-08:00",
      "homeGame": true,
      "opposingTeam": "Vegas Golden Knights",
      "locationName": "Climate Pledge Arena",
      "locationAddress": "334 1st Ave N, Seattle, WA 98109",
      "finalScore": "4-2"
    }
  ]
}'
```

## Targeting retrieval of specific fields
Since our `json-server` doesn't support returning specific fields, you'll need to retrieve the entire teams resource and filter the response on the client side.
You can then process this JSON data (e.g., with jq in a shell script) to extract only the teamName and winLossRatio.
curl -X GET http://localhost:3000/teams \
-H "Content-Type: application/json" | jq '[.[] | {teamName: .teamName, winLossRatio: .winLossRatio}]'



# Limitations of json-server and Troubleshooting Approaches

## 1. PATCH Replaces Entire Nested Arrays
- **Limitation**: When updating a nested array (e.g., `seasonGames`) via a `PATCH` call, json-server replaces the entire array instead of merging changes with existing fields.
- **Workaround**:
  - Always include the full array in the `PATCH` request to avoid overwriting data.
  - Example:
    ```bash
    curl -X PATCH http://localhost:3000/games/5 \
    -H "Content-Type: application/json" \
    -d '{
      "seasonGames": [
        {
          "gameNumber": 1,
          "finalScore": "4-2"
        },
        {
          "gameNumber": 2,
          "finalScore": "TBD"
        }
      ]
    }'
    ```

## 2. PATCH Cannot Update Multiple Resources Simultaneously
- **Limitation**: json-server does not support updating two different resources (e.g., `games` and `teams`) in the same `PATCH` call.
- **Workaround**:
  - Make separate `PATCH` calls for each resource.
  - Example:
    ```bash
    # Update game score
    curl -X PATCH http://localhost:3000/games/5 \
    -H "Content-Type: application/json" \
    -d '{ "seasonGames": [{ "gameNumber": 1, "finalScore": "4-2" }] }'

    # Update winLossRatio
    curl -X PATCH http://localhost:3000/teams/5 \
    -H "Content-Type: application/json" \
    -d '{ "winLossRatio": "1-1-0" }'
    ```

## 3. json-server Cannot Return Specific Fields
- **Limitation**: json-server does not support querying specific fields (e.g., `teamName` and `winLossRatio`) in a single call.
- **Workaround**:
  - Retrieve all data and filter the results client-side.
  - Example using `jq`:
    ```bash
    curl -X GET http://localhost:3000/teams | jq '[.[] | {teamName, winLossRatio}]'
    ```

## 4. Static Server Does Not Dynamically Update Fields
- **Limitation**: json-server does not support dynamic updates (e.g., recalculating `winLossRatio` based on game results).
- **Workaround**:
  - Perform calculations client-side and send updated values back via a `PATCH` or `PUT` call.
  - Example:
    ```bash
    # Calculate winLossRatio locally and update
    curl -X PATCH http://localhost:3000/teams/5 \
    -H "Content-Type: application/json" \
    -d '{ "winLossRatio": "2-1-0" }'
    ```

## 5. No Validation for Unique or Consistent Fields
- **Limitation**: json-server does not enforce uniqueness (e.g., duplicate `id` values) or consistency (e.g., valid `finalScore` formats).
- **Workaround**:
  - Add middleware to validate requests before they are processed.
  - Example Middleware:
    ```javascript
    module.exports = (req, res, next) => {
      const db = require('./db.json');
      if (req.method === 'POST' && db.teams.some(team => team.id === req.body.id)) {
        return res.status(400).json({ error: "Duplicate id detected" });
      }
      next();
    };
    ```

## 6. Limited Support for Advanced Queries
- **Limitation**: json-server cannot handle complex queries (e.g., filtering nested fields or advanced search).
- **Workaround**:
  - Use client-side filtering or extend json-server with custom middleware.
  - Example Middleware for Specific Fields:
    ```javascript
    module.exports = (req, res, next) => {
      if (req.method === 'GET' && req.path === '/teams') {
        const fields = req.query._fields?.split(',') || [];
        const db = require('./db.json');
        const result = db.teams.map(team =>
          fields.reduce((acc, field) => ({ ...acc, [field]: team[field] }), {})
        );
        res.json(result);
      } else {
        next();
      }
    };
    ```
