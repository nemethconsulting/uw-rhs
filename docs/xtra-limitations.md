
Yes, what you're observing is indeed a limitation of json-server due to its behavior when handling nested resources (like seasonGames). When you use PATCH to update a nested field (seasonGames), json-server will replace the entire array and may not update sibling fields like winLossRatio correctly within the same PATCH request. This is because json-server treats each field in the resource independently, and it doesn't automatically merge changes between top-level fields and nested arrays.

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