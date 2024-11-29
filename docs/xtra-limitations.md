<div style="display: flex; align-items: center; justify-content: space-between;">
  <h1>Limitations of json-server and Troubleshooting Approaches</h1>
  <img src="rhs-logo_4x4.jpeg" alt="Rec Hockey League Logo" style="width: 100px; height: 100px; margin-left: 20px;">
</div>

There are some limitations to the `json-server` used with this mock API. Review the details below to understnd the call and responses available in working with it.

## Table of Contents
1. [PATCH Replaces Entire Nested Arrays](#1)
2. [PATCH Cannot Update Multiple Resources Simultaneously](#2)
3. [json-server Cannot Return Specific Fields](3)
4. [Static Server Does Not Dynamically Update Fields](#4)
5. [Limited Support for Advanced Queries](#5)
6. [Git Bash Issues with Multi-line JSON Payloads](#6)
7. [Back to Main Menu](nav.md)

<a id="1"></a>
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

<a id="2"></a>
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

<a id="3"></a>
## 3. json-server Cannot Return Specific Fields
- **Limitation**: json-server does not support querying specific fields (e.g., `teamName` and `winLossRatio`) in a single call.
- **Workaround**:
  - Retrieve all data and filter the results client-side.
  - Example using `jq`:
    ```bash
    curl -X GET http://localhost:3000/teams | jq '[.[] | {teamName, winLossRatio}]'
    ```

<a id="4"></a>
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

<a id="5"></a>
## 5. Limited Support for Advanced Queries
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

<a id="6"></a>
## 6. Git Bash Issues with Multi-line JSON Payloads

- **Limitation**: Git Bash sometimes struggles with multi-line JSON payloads, causing parsing errors when copying and pasting the `curl` command.
- **Workaround**:
  - Condense the JSON payload into a single line to avoid issues with line breaks.
  - Example: 
    ```bash
    curl -X PATCH http://localhost:3000/games/5 \
    -H "Content-Type: application/json" \
    -d '{"id": 5, "teamName": "Seattle Kraken", "season": "2024-2025", "seasonGames": [{"gameNumber": 1, "date": "2024-10-03T19:00:00-08:00", "homeGame": true, "opposingTeam": "Vegas Golden Knights", "locationName": "Climate Pledge Arena", "locationAddress": "334 1st Ave N, Seattle, WA 98109", "finalScore": "5-3"}, {"gameNumber": 2, "date": "2024-10-07T19:00:00-08:00", "homeGame": false, "opposingTeam": "Calgary Flames", "locationName": "Scotiabank Saddledome", "locationAddress": "555 Saddledome Rise SE, Calgary, AB T2G 2W1", "finalScore": "2-1"}, {"gameNumber": null, "date": null, "homeGame": null, "opposingTeam": null, "locationName": null, "locationAddress": null, "finalScore": null}]}'
    ```
  - This ensures the entire JSON body is correctly interpreted by Git Bash and sent successfully to the server.

## [Back to Main Menu](nav.md)