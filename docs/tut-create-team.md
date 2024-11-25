# Create an entry for your team

In this tutorial:

- You will learn how to add a team to the Rec Hockey Service using both
curl and Postman Desktop
- You will be introduced to some common errors and troubleshooting tips

## Table of Contents
- [Prerequisites](#1)
- [Add your team using curl](#2)
- [Add your team using Postman Desktop](#3)
- [Errors & Troubleshooting](#4)
- [Related Topics](#5)
- [Back to Main Menu](nav.md)

<a id="1"></a>
## Prerequisties

- Make sure your system is running the API server. See [Test your set up](test-system.md) if you need help with this.

<a id="2"></a>
## Add your team using curl

1. Start with a `GET` call to see the list of current teams in the league database.

```shell
curl http://{base_url}/teams
```

The output should look like:

```shell
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

3. Review the list of teams and take note of the final team `id`. Your input for this field will be the highest team `id` +1. (In the example below, there are already 4 teams in the database, so a new team would take the `id` of 5).

4. With your data on hand, make the following `POST` to the API.

```shell
curl -X POST http://localhost:3000/teams \
-H "Content-Type: application/json" \
-d '{
  "id": 5,
  "teamName": "Seattle Kraken",
  "headquarters": "Seattle, WA",
  "mascot": "Buoy the Troll",
  "winLossRatio": "0-0-0",
  "coach": "Dave Hakstol",
  "numberOfPlayers": 23
}'
```

A successful response will look like this:
```shell
{
      "id": 5,
      "teamName": "Seattle Kraken",
      "headquarters": "Seattle, WA",
      "mascot": "Buoy the Troll",
      "winLossRatio": "0-0-0",
      "coach": "Dave Hakstol",
      "numberOfPlayers": 23
}
```

5. With your team created, you can go ahead and start adding your [team's schedule](tut-add-games.md).

<a id="3"></a>
## Add your team using Postman Desktop

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

3. Review the list of teams and take note of the highest team `id`. Your input for this field will the highest team `id` +1. (In the example below, there are already 5 teams in the database, so a new team would take the `id` of 6)

4. With your data on hand, make the following `POST`.

* **METHOD**: POST
    * **URL**: `{{base_url}}/teams`
    * **Headers**:
        * `Content-Type: application/json`
    * **Request body**:
        You can change the values of each property as you'd like.

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

5. With your team created, you can go ahead and start adding your [team's schedule](tut-add-games.md).

<a id="4"></a>
### Errors & Troubleshooting

1. One error you may encounter is: `Error: Insert failed, duplicate id'

This error occurs when you try to `POST` using a team `id` that already exists in the database.

**To troubleshoot:** Review the list of teams in the database (do another `GET` call if needed) and find an `id` that is not already being used, preferably being the highest existing `id` +1.

2. Other errors in curl often occur because of a mistyped command, including:
    - Forgetting to put a backslash after one of your lines of code
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
