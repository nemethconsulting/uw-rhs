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
  "teamId": 5,
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
  "teamId": 5,
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
  ],
  "id": 5
}
```

3. Use this method to add any additional games to the team's schedule. When a game is complete, use our [Update the score of a completed game](tut-add-score.md) tutorial to update the db.

<a id="3"></a>
## Add your games using Postman Desktop

1. Start by gathering the necessary data about your games. See our [games resource](res-games.md) guide for the necessary fields to make your call. If you don't have all data on hand, review our [Note on null or empty fields](tut-null-fields.md).

2. Assume your team is assigned `id`=5 in the db (The new entry for the Seattle Kraken) and you want to add the first two season games to the schedule. Make the following `POST`. 

    * **METHOD**: POST
    * **URL**: `{{base_url}}/games`
    * **Headers**:
        * `Content-Type: application/json`
    * **Request body**:
        You can change the values of each property as needed.

```js

```

The response should look like:

```js

```

2. Note the required fields and make sure you have the appropriate data for entry. If you do not have all the data, see [Note on null or empty 

```js
[
    {
        "id": 9,
        "teamName": "your team name",
        "headquarters": "your city and state",
        "mascot": "the name of your mascot",
        "winLossRatio": "0-0-0",
        "coach": "your team's coach",
        "numberOfPlayers": 0
    }
]
```

The response should look like:

```js
[
    {
        "id": 9,
        "teamName": "your team name",
        "headquarters": "your city and state",
        "mascot": "the name of your mascot",
        "winLossRatio": "0-0-0",
        "coach": "your team's coach",
        "numberOfPlayers": 0
    }
]
```

5. With your team created, you can go ahead and start adding your [team's schedule](tut-add-games.md).

<a id="4"></a>
### Errors & Troubleshooting

1. One error you may encounter in curl is:

```shell
Error: Insert failed, duplicate id
```
This error occurs when you try to `POST` using a team `id` that already exists in the database.
curl will not overwrite the existing entry.

*To troubleshoot:* Review the list of teams in the database (do another `GET` call if needed) and find an `id` that is not already being used, preferably being the highest existing `id` +1.

<span style="color:red">NOTE OF CAUTION:</span> This same error will not occur in Postman Desktop. Instead,
if you post with a team `id` that is already in the database, it will overwrite the existing team's data. Doublecheck that you
have a unique team `id` before creating your team.

2. Other errors in curl often occur because of a mistyped command, including:
  - Forgetting to put a backslash after one of your lines of code
  - Using single quotes instead of backticks when delivering your json data
  - Mistyping the URL
  - Forgetting a comma after a field entry in your JSON data

*To troubleshoot:* Recheck your entered command closely and look for these potential errors.


<a id="5"></a>
## Related Topics

Here are related tutorials you may want to look at:

1. [Create an entry for your team](tut-create-team.md)
2. [Update the final score of a game](tut-add-score.md)
3. [Retrieve the league's win/loss records](tut-get-wins.md)

### [Back to Main Menu](nav.md)
