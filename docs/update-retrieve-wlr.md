# Update the score of a completed game

In this tutorial:

- You will learn how to update the `finalScore` field after a game is completed, using both
curl and Postman Desktop
- You will also learn how to both update and retrieve your team's `winLossRatio`
- You will be introduced to some common errors and troubleshooting tips

## Table of Contents
- [Prerequisites](#1)
- [Update the score using curl](#2)
- [Update the score using Postman Desktop](#3)
- [Errors & Troubleshooting](#4)
- [Related Topics](#5)
- [Back to Main Menu](nav.md)

<a id="1"></a>
## Prerequisties

- Make sure your system is running the API server. See [Test your set up](test-system.md) if you need help with this.
- Make sure you've already added your team's schedule into the Rec Hockey Service. See [Add games to your team's calendar](tut-add-games.md) for assistance.

<a id="2"></a>
## Update the score using curl

1. You will need the `gameNumber` to make this `PATCH`. If you don't have it on hand, you can make a `GET` call to the games resource to find it.

2. Let's assume you are updating the score for the Seattle Kraken (team `id` = 5) after their first game against the Vegas Golden Knights. Using the appropriate game id (in this case, `gameNumber`:1), make the following call in curl:

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

The output should look like:

```shell
{
  "id": 5,
  "teamName": "Seattle Kraken",
  "season": "2024-2025",
  "seasonGames": [
    {
      "gameNumber": 1,
      "finalScore": "4-2"
    }
  ]
}
```


4. Our API does not dynamically update fields, so if you wanted to simultaneously update your team's `winLossRatio` in the same call as updating your game score, you could do so using the following command (for this example, we will update `gameNumber`: 2 along with the cumulative `winLossRatio' for the Seattle Kraken):

```shell
curl -X PATCH http://localhost:3000/games/5 \
-H "Content-Type: application/json" \
-d '{
  "winLossRatio": "1-1-0",
  "seasonGames": [
    {
      "gameNumber": 2,
      "finalScore": "1-3"
    }
  ]
}'
```

The response should look like: 

```shell
{
  "id": 5,
  "teamName": "Seattle Kraken",
  "season": "2024-2025",
  "seasonGames": [
    {
      "gameNumber": 2,
      "finalScore": "1-3"
    }
  ],
  "winLossRatio": "1-1-0"
}
```

3. When patching multiple fields, we recommend doing a final `GET` call to ensure the data has been properly propagated to the database.

4. As the season goes on, if you are looking to retrieve `winLossRatio`'s across the league, see our [Retrieve the league's win/loss records](tut-get-wins.md) tutorial.

<a id="3"></a>
## Update the score using Postman Desktop

1. Start with a `GET` call to see the list of current teams in the league database.

    * **METHOD**: POST
    * **URL**: `{{base_url}}/teams`
    * **Headers**:
        * `Content-Type: application/json`

The response should look like:

```js
[
    {
        "id": 1,
        "teamName": "Pittsburgh Penguins",
        "headquarters": "Pittsburgh, PA",
        "mascot": "Iceburgh",
        "winLossRatio": "0-0-0",
        "coach": "Mike Sullivan",
        "numberOfPlayers": "17"
    },
  ...
```

2. Note the required fields and make sure you have the appropriate data for entry. If you do not have all the data, see [Note on null or empty fields](tut-null-fields.md) to help guide your data entry.

3. Review the list of teams and take note of the highest team `id`. Your input for this field will the highest team `id` +1. (In the example below, there are already 8 teams in the database, so a new team would take the `id` of 9)

4. With your data on hand, make the following `POST`.

* **METHOD**: POST
    * **URL**: `{{base_url}}/teams`
    * **Headers**:
        * `Content-Type: application/json`
    * **Request body**:
        You can change the values of each property as you'd like.

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

1. Double-Check Your Game Data
Ensure that the homeGame property aligns with the score order:

If "homeGame": true, the first score in "finalScore" belongs to the team in the teamName field (e.g., Seattle Kraken).
If "homeGame": false, the first score belongs to the opposingTeam.

2. While it may seem easier to target only the relevant fields with a `PATCH` call like the one below, the `json-server` used with the API does not natively handle deep merging of objects or arrays. You need to send all fields of data in your request, or use middleware such as `mergePatch.js` to merge arrays and nested objects properly. 

```shell
curl -X PATCH http://localhost:3000/games/5 \
-H "Content-Type: application/json" \
-d '{
  "seasonGames": [
    {
      "gameNumber": 1,
      "finalScore": "4-2"
    }
  ]
}'
```

3. One error you may encounter in curl is:

```shell
Error: Insert failed, duplicate id
```
This error occurs when you try to `POST` using a team `id` that already exists in the database.
curl will not overwrite the existing entry.

**To troubleshoot:** Review the list of teams in the database (do another `GET` call if needed) and find an `id` that is not already being used, preferably being the highest existing `id` +1.

<span style="color:red">NOTE OF CAUTION:</span> This same error will not occur in Postman Desktop. Instead,
if you post with a team `id` that is already in the database, it will overwrite the existing team's data. Doublecheck that you
have a unique team `id` before creating your team.

4. Other errors in curl often occur because of a mistyped command, including:
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
2. [Add games to your team's calendar](tut-add-games.md)
3. [Retrieve the league's win/loss records](tut-get-wins.md)

### [Back to Main Menu](nav.md)
