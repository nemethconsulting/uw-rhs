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
