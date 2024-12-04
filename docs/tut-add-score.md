<div style="display: flex; align-items: center; justify-content: space-between;">
  <h1>Update the score of a completed game</h1>
  <img src="rhs-logo_4x4.jpeg" alt="Rec Hockey League Logo" style="width: 100px; height: 100px; margin-left: 20px;">
</div>

In this tutorial:

- You will learn how to update the `finalScore` field after a game is completed, using both
curl and Postman Desktop
- You will be introduced to some common errors and troubleshooting tips

## Table of contents
1. [Prerequisites](#1)
2. [Update the score using curl](#2)
3. [Update the score using Postman Desktop](#3)
4. [Errors & troubleshooting](#4)
5. [Related topics](#5)
6. [Back to main menu](nav.md)

<a id="1"></a>
## Prerequisites

- Make sure your system is running the API server. See [Test your set up](test-system.md) if you need help with this.
- Make sure you've already added your team's schedule into the Rec Hockey Service API. See [Add games to your team's calendar](tut-add-games.md) for assistance.

<a id="2"></a>
## Update the score using curl

1. Start with a `GET` call to see the list of current games in the database. Export this to an external editor, update the relevant `finalScore` fields, and return the entire JSON payload using a command like the one in step 2.

2. Let's assume you are updating the score for the Seattle Kraken (team `id` = 5) after their first game against the Vegas Golden Knights. You have a total of two season games in the API at the moment, so you would download all data, update the `finalScore` field under `gameNumber`:1 and send the entire dataset back in a `PATCH` call as follows:

```bash
curl -X PATCH {base_url}/games/5 \
-H "Content-Type: application/json" \
-d '{
  "id": 5,
  "teamName": "Seattle Kraken",
  "season": "2024-2025",
  "seasonGames": [
    {
      "gameNumber": 1,
      "date": "2024-10-03T19:00:00-08:00",
      "homeGame": true,
      "opposingTeam": "Vegas Golden Knights",
      "locationName": "Climate Pledge Arena",
      "locationAddress": "334 1st Ave N, Seattle, WA 98109",
      "finalScore": "4-2"
    },
    {
          "gameNumber": 2,
          "date": "2024-10-10T19:30:00-06:00",
          "homeGame": false,
          "opposingTeam": "Detroit Red Wings",
          "locationName": "Little Caesars Arena",
          "locationAddress": "2645 Woodward Avenue, Detroit, MI 48201",
          "finalScore": "TBD"
    }
  ]
}'

```

The response should look like:

```bash
{
  "id": 5,
  "teamName": "Seattle Kraken",
  "season": "2024-2025",
  "seasonGames": [
    {
      "gameNumber": 1,
      "date": "2024-10-03T19:00:00-08:00",
      "homeGame": true,
      "opposingTeam": "Vegas Golden Knights",
      "locationName": "Climate Pledge Arena",
      "locationAddress": "334 1st Ave N, Seattle, WA 98109",
      "finalScore": "4-2"
    },
    {
      "gameNumber": 2,
      "date": "2024-10-10T19:30:00-06:00",
      "homeGame": false,
      "opposingTeam": "Detroit Red Wings",
      "locationName": "Little Caesars Arena",
      "locationAddress": "2645 Woodward Avenue, Detroit, MI 48201",
      "finalScore": "TBD"
    }
  ]
}
```

3. When patching multiple fields, we recommend doing a final `GET` call to ensure the data has been properly propagated to the database.

4. **NOTE** While it may seem cumbersome to download all resource data and return it just to update a single field, please review the [Limitations of our `json-server`](xtra-limitations.md) doc to understand and potentially troubleshoot this issue.

5. If you want to update your `winLossRatio` to coincide with the recently completed game, you can do so using the [Update your team's win/loss record](tut-update-winloss.md) tutorial.

<a id="3"></a>
## Update the score using Postman Desktop

1. Start with a `GET` call to see the list of current games in the database. Export this to an external editor, update the relevant `finalScore` fields and return the entire JSON payload using a command like the one in step 2.

2. Let's assume you are updating the score for the New Jersey Devils (team `id` = 6) after their first game against the Philadelphia Flyers. You have a total of two season games in the API at the moment, so you would download all data, update the `finalScore` field under `gameNumber`:1 and send the entire dataset back in a `PATCH` call as follows:

    * **METHOD**: PATCH
    * **URL**: `{base_url}/teams/6`
    * **Headers**:
        * `Content-Type: application/json`
    * **Request body**:
        You can change the values of each property as needed.

```json
{
      "id": 6,
      "teamName": "New Jersey Devils",
      "season": "2024-2025",
      "seasonGames": [
        {
          "gameNumber": 1,
          "date": "2024-10-04T19:00:00-05:00",
          "homeGame": true,
          "opposingTeam": "Philadelphia Flyers",
          "locationName": "Prudential Center",
          "locationAddress": "25 Lafayette St, Newark, NJ 07102",
          "finalScore": "5-3"
        },
        {
          "gameNumber": 2,
          "date": "2024-10-08T19:00:00-05:00",
          "homeGame": false,
          "opposingTeam": "New York Rangers",
          "locationName": "Madison Square Garden",
          "locationAddress": "4 Pennsylvania Plaza, New York, NY 10001",
          "finalScore": "TBD"
        }
```

The response should look like:

```js
{
    "id": 6,
    "teamName": "New Jersey Devils",
    "season": "2024-2025",
    "seasonGames": [
        {
            "gameNumber": 1,
            "date": "2024-10-04T19:00:00-05:00",
            "homeGame": true,
            "opposingTeam": "Philadelphia Flyers",
            "locationName": "Prudential Center",
            "locationAddress": "25 Lafayette St, Newark, NJ 07102",
            "finalScore": "5-2"
        },
        {
            "gameNumber": 2,
            "date": "2024-10-08T19:00:00-05:00",
            "homeGame": false,
            "opposingTeam": "New York Rangers",
            "locationName": "Madison Square Garden",
            "locationAddress": "4 Pennsylvania Plaza, New York, NY 10001",
            "finalScore": "TBD"
        }
    ]
}
```

3. When patching multiple fields, we recommend making a final `GET` request to ensure the data has been properly propagated to the database.

4. **NOTE** While it may seem cumbersome to download all resource data and return it just to update a single field, please review the [Limitations of our `json-server`](xtra-limitations.md) doc to understand and potentially troubleshoot this issue.

5. If you want to update your `winLossRatio` to coincide with the recently completed game, you can do so using the [Update your team's win/loss record](tut-update-winloss.md) tutorial.

<a id="4"></a>
### Errors & troubleshooting

1. **Note** on proper data entry the `finalScore` field:
Ensure that the `homeGame` property aligns with the score order:

  - If "homeGame": true, the first score in "finalScore" belongs to the team in the teamName field (e.g., Seattle Kraken).
  - If "homeGame": false, the first score belongs to the opposingTeam.

2. Other errors often occur because of a mistyped command, including:
    - Forgetting to put a backslash after one of your lines of code in curl
    - Using single quotes instead of backticks when delivering your json data
    - Mistyping the URL
    - Forgetting a comma after a field entry in your JSON data
    - Other misc mis-formatting of commands and json payloads

**To troubleshoot:** Recheck your command closely and look for these potential errors.

<a id="5"></a>
## Related topics

Here are related tutorials you may want to look at:

1. [Create an entry for your team](tut-create-team.md)
2. [Add games to your team's calendar](tut-add-games.md)
3. [Update your team's win/loss record](tut-update-winloss.md)

### [Back to main menu](nav.md)
