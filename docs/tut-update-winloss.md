# Update your team's `winLossRatio`

In this tutorial:

- You will learn how to update the `winLossRatio` field after a game is completed, using both
curl and Postman Desktop
- You will be introduced to some common errors and troubleshooting tips

## Table of Contents
- [Prerequisites](#1)
- [Update the `winLossRatio` using curl](#2)
- [Update the `winLossRatio` using Postman Desktop](#3)
- [Errors & Troubleshooting](#4)
- [Related Topics](#5)
- [Back to Main Menu](nav.md)

<a id="1"></a>
## Prerequisties

- Make sure your system is running the API server. See [Test your set up](test-system.md) if you need help with this.
- Make sure you've already added your team details into the Rec Hockey Service. See [Create an entry for your team](tut-create-team.md) for assistance.

<a id="2"></a>
## Update the `winLossRatio` using curl

1. Start with a `GET` call to the `teams` resource to retrieve your teams details, or review our [teams resource](res-teams.md) doc to find the required fields.

2. Let's assume you are updating the `winLossRatio` for the Seattle Kraken (team `id` = 5) after losing their second game against the Calgary Flames (They won their first game). After updating the `winLossRatio` field, send the following `PATCH` call:

```shell
curl -X PATCH http://localhost:3000/teams/5 \
-H "Content-Type: application/json" \
-d '{
  "id": 5,
  "teamName": "Seattle Kraken",
  "headquarters": "Seattle, WA",
  "mascot": "Buoy the Troll",
  "winLossRatio": "1-1-0",
  "coach": "Dave Hakstol",
  "numberOfPlayers": 23
}'
```

The output should look like:

```shell
{
  "id": 5,
  "teamName": "Seattle Kraken",
  "headquarters": "Seattle, WA",
  "mascot": "Buoy the Troll",
  "winLossRatio": "1-1-0",
  "coach": "Dave Hakstol",
  "numberOfPlayers": 23
}
```

3. When patching multiple fields, we recommend doing a final `GET` call to ensure the data has been properly propagated to the database.

4. **NOTE** While it may seem cumbersome to download all resource data and return it just to updata a single field, please review the [Limitations of our `json-server`](xtra-limitations.md) doc to understand and potentially troubleshoot this issue.

5. As the season progresses, you may want to retrieve the `winLossRatio`s for all teams in the league to calculate standings. To do this, refer to our [Retrieve the league's win/loss records](tut-retrieve-wlr.md) tutorial.

<a id="3"></a>
## Update the score using Postman Desktop

1. Start with a `GET` call to the `teams` resource to retrieve your teams details, or review our [teams resource](res-teams.md) doc to find the required fields.

2. Let's assume you are updating the `winLossRatio` for the New Jersey (team `id` = 6) after losing their second game against the New York Rangers (They won their first game). After updating the `winLossRatio` field, send the following `PATCH` call:

    * **METHOD**: PATCH
    * **URL**: `{{base_url}}/teams/6`
    * **Headers**:
        * `Content-Type: application/json`
    * **Request body**:
        You can change the values of each property as needed.

```json
{
  "id": 6,
  "teamName": "New Jersey Devils",
  "headquarters": "Newark, NJ",
  "mascot": "NJ Devil",
  "winLossRatio": "1-1-0",
  "coach": "Lindy Ruff",
  "numberOfPlayers": 23
}
```

The response should look like:

```js
{
    "id": 6,
    "teamName": "New Jersey Devils",
    "headquarters": "Newark, NJ",
    "mascot": "NJ Devil",
    "winLossRatio": "1-1-0",
    "coach": "Lindy Ruff",
    "numberOfPlayers": 23
}
```

3. When patching multiple fields, we recommend doing a final `GET` call to ensure the data has been properly propagated to the database.

4. **NOTE** While it may seem cumbersome to download all resource data and return it just to updata a single field, please review the [Limitations of our `json-server`](xtra-limitations.md) doc to understand and potentially troubleshoot this issue.

5. As the season progresses, you may want to retrieve the `winLossRatio`s for all teams in the league to calculate standings. To do this, refer to our [Retrieve the league's win/loss records](tut-retrieve-wlr.md) tutorial.

<a id="4"></a>
### Errors & Troubleshooting

1. Errors often occur because of a mistyped command, including:
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
3. [Retrieve the league's win/loss records](tut-retrieve-wlr.md)

### [Back to Main Menu](nav.md)
