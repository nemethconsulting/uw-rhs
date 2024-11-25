# Add games to your team's schedule

In this tutorial:

- You will learn how to add games to your team's schedule using both
curl and Postman Desktop
- You will be introduced to some common errors and troubleshooting tips

## Table of Contents
- [Prerequisites](#1)
- [Add your games using curl](#2)
- [Add your games using Postman Desktop](#3)
- [Errors & Troubleshooting](#4)
- [Related Topics](#5)
- [Back to Main Menu](nav.md)

<a id="1"></a>
## Prerequisties

- Make sure your system is running the API server. See [Test your set up](test-system.md) if you need help with this.
- Make sure you've first created a team entry in the Rec Hockey Service. See [Create an entry for your team](tut-create-team.md) for assistance.

<a id="2"></a>
## Add your games using curl

1. Start by gathering the necessary data about your games. See our [games resource](res-games.md) guide for the necessary fields to make your call. If you don't have all data on hand, review our [Note on null or empty fields](tut-null-fields.md).

2. Assume your team is assigned `id`=5 in the db (The new entry for the Seattle Kraken) and you want to add the first two season games to the schedule. Make the following `POST`.

```shell
curl -X POST http://localhost:3000/games \
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
      "finalScore": "TBD"
    },
    {
      "gameNumber": 2,
      "date": "2024-10-07T19:00:00-08:00",
      "homeGame": false,
      "opposingTeam": "Calgary Flames",
      "locationName": "Scotiabank Saddledome",
      "locationAddress": "555 Saddledome Rise SE, Calgary, AB T2G 2W1",
      "finalScore": "TBD"
    }
  ]
}'
```

The output should look like:

```shell
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
      "finalScore": "TBD"
    },
    {
      "gameNumber": 2,
      "date": "2024-10-07T19:00:00-08:00",
      "homeGame": false,
      "opposingTeam": "Calgary Flames",
      "locationName": "Scotiabank Saddledome",
      "locationAddress": "555 Saddledome Rise SE, Calgary, AB T2G 2W1",
      "finalScore": "TBD"
    }
  ]
}
```

3. Use this method to add any additional games to the team's schedule. When a game is complete, use our [Update the score of a completed game](tut-add-score.md) tutorial to update the db.

<a id="3"></a>
## Add your games using Postman Desktop

1. Start by gathering the necessary data about your games. See our [games resource](res-games.md) guide for the necessary fields to make your call. If you don't have all data on hand, review our [Note on null or empty fields](tut-null-fields.md).

2. Assume your team is assigned `id`=6 in the db (The new entry for the New Jersey Devils) and you want to add the first two season games to the schedule. Make the following `POST`. 

    * **METHOD**: POST
    * **URL**: `{{base_url}}/games`
    * **Headers**:
        * `Content-Type: application/json`
    * **Request body**:
        You can change the values of each property as needed.

```js
{
  "id": 6,
  "teamName": "New Jersey Devils",
  "headquarters": "Newark, NJ",
  "mascot": "NJ Devil",
  "winLossRatio": "0-0-0",
  "coach": "Lindy Ruff",
  "numberOfPlayers": 23,
  "seasonGames": [
    {
      "gameNumber": 1,
      "date": "2024-10-04T19:00:00-05:00",
      "homeGame": true,
      "opposingTeam": "Philadelphia Flyers",
      "locationName": "Prudential Center",
      "locationAddress": "25 Lafayette St, Newark, NJ 07102",
      "finalScore": "TBD"
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

The response should look like:

```js
{
    "id": 6,
    "teamName": "New Jersey Devils",
    "headquarters": "Newark, NJ",
    "mascot": "NJ Devil",
    "winLossRatio": "0-0-0",
    "coach": "Lindy Ruff",
    "numberOfPlayers": 23,
    "seasonGames": [
        {
            "gameNumber": 1,
            "date": "2024-10-04T19:00:00-05:00",
            "homeGame": true,
            "opposingTeam": "Philadelphia Flyers",
            "locationName": "Prudential Center",
            "locationAddress": "25 Lafayette St, Newark, NJ 07102",
            "finalScore": "TBD"
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

3. Use this method to add any additional games to the team's schedule. When a game is complete, use our [Update the score of a completed game](tut-add-score.md) tutorial to update the db.

<a id="4"></a>
### Errors & Troubleshooting

1. One error you may encounter is:

```shell
Error: Insert failed, duplicate id
```
Both curl and Postman Desktop will throw this error when you try to `POST` using a  `gameNumber` that already exists. 

**To troubleshoot:** If you receieve this error, do a `GET` call for your team's games and adjust your `gameNumber` for the new game accordingly.

2. Other errors in curl often occur because of a mistyped command, including:
    - Forgetting to put a backslash after one of your lines of code in curl
    - Using single quotes instead of backticks when delivering your json data
    - Mistyping the URL
    - Forgetting a comma after a field entry in your JSON data
    - Other misc mis-formatting of commands and json payloads

**To troubleshoot:** Recheck your command closely and look for these potential errors.


<a id="5"></a>
## Related Topics

Here are related tutorials you may want to look at:

1. [Create an entry for your team](tut-create-team.md)
2. [Update the final score of a game](tut-add-score.md)
3. [Retrieve the league's win/loss records](tut-get-wins.md)

### [Back to Main Menu](nav.md)
