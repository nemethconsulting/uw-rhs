<div style="display: flex; align-items: center; justify-content: space-between;">
  <h1>Create an entry for your team</h1>
  <img src="rhs-logo_4x4.jpeg" alt="Rec Hockey League Logo" style="width: 100px; height: 100px; margin-left: 20px;">
</div>

In this tutorial:

- You will learn how to add a team to the Rec Hockey Service API using both
curl and Postman Desktop
- You will be introduced to some common errors and troubleshooting tips

## Table of Contents
1. [Prerequisites](#1)
2. [Add your team using curl](#2)
3. [Add your team using Postman Desktop](#3)
4. [Errors & Troubleshooting](#4)
5. [Related Topics](#5)
6. [Back to Main Menu](nav.md)

<a id="1"></a>
## Prerequisties

- Make sure your system is running the API server. See [Test your set up](test-system.md) if you need help with this.

<a id="2"></a>
## Add your team using curl

1. Refer to the [teams resource](res-teams.md) doc for fields and values specific to this resource.

2. Format your `POST` call as follows. By making the `id` field `null`, the API will assign your new team the next highest `id` in the database.

```bash
curl -X POST {base_url}/teams \
-H "Content-Type: application/json" \
-d '{
  "id": null,
  "teamName": "Seattle Kraken",
  "headquarters": "Seattle, WA",
  "mascot": "Buoy the Troll",
  "winLossRatio": "0-0-0",
  "coach": "Dan Bylsma",
  "numberOfPlayers": 23
}'
```

The response should look like:
```bash
{
      "id": 5,
      "teamName": "Seattle Kraken",
      "headquarters": "Seattle, WA",
      "mascot": "Buoy the Troll",
      "winLossRatio": "0-0-0",
      "coach": "Dan Bylsma",
      "numberOfPlayers": 23
}
```

3. With your team created, you can go ahead and start adding your [team's schedule](tut-add-games.md).

<a id="3"></a>
## Add your team using Postman Desktop

1. Refer to the [teams resource](res-teams.md) doc for fields and values specific to this resource.

2. Format your `POST` call as follows. By making the `id` field `null`, the API will assign your new team the next highest `id` in the database.

* **METHOD**: POST
    * **URL**: `{{base_url}}/teams`
    * **Headers**:
        * `Content-Type: application/json`
    * **Request body**:
        You can change the values of each property as needed.

```js
{
  "id": null,
  "teamName": "New Jersey Devils",
  "headquarters": "Newark, NJ",
  "mascot": "NJ Devil",
  "winLossRatio": "0-0-0",
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
    "winLossRatio": "0-0-0",
    "coach": "Lindy Ruff",
    "numberOfPlayers": 23
}
```

3. With your team created, you can go ahead and start adding your [team's schedule](tut-add-games.md).

<a id="4"></a>
### Errors & Troubleshooting

1. One error you may encounter is:

```bash
Error: Insert failed, duplicate id
```
Both curl and Postman Desktop will throw this error when you try to `POST` using a team `id` that already exists in the database.

**To troubleshoot:** Do a `GET` call to review all teams in the db and find an `id` that is not already being used, preferably being the highest existing `id` +1. Or set your `id` field to `null` and the API will assign an `id` for you.

2. Other errors often occur because of a mistyped command, including:
    - Forgetting to put a backslash after one of your lines of code in curl
    - Using single quotes instead of backticks when delivering your json data
    - Mistyping the URL
    - Forgetting a comma after a field entry in your JSON data
    - Other misc mis-formatting of commands and json payloads
    
**To troubleshoot:** Recheck your command closely and look for potential errors.


<a id="5"></a>
## Related Topics

Here are related tutorials you may want to look at:

1. [Add games to your team's calendar](tut-add-games.md)
2. [Update the final score of a game](tut-add-score.md)
3. [Retrieve the league's win/loss records](tut-get-wins.md)

### [Back to Main Menu](nav.md)
