# Retrieve Win/Loss Ratios across the league

In this tutorial:

- You learn how to retrieve  `winLossRatio`s for the entire league.
- You will be introduced to some common errors and troubleshooting tips

## Table of Contents
- [Prerequisites](#1)
- [Retrieve all win/loss records for the league using curl](#2)
- [Retrieve all win/loss records for the league using Postman Desktop](#3)
- [Errors & Troubleshooting](#4)
- [Related Topics](#5)
- [Back to Main Menu](nav.md)

<a id="1"></a>
## Prerequisties

- Make sure your system is running the API server. See [Test your set up](test-system.md) if you need help with this.
- Make sure you've already added all team details into the Rec Hockey Service. See [Create an entry for your team](tut-create-team.md) for assistance.

<a id="2"></a>
## Retrieve all win/loss records for the league

1. At various points in the season, you will want to see all teams' records to calculate standings. You can do this using a simple `GET` call.

```shell
curl -X GET http://localhost:3000/teams \
-H "Content-Type: application/json"
```

The output should look like:

```shell
[
  {
    "id": 1,
    "teamName": "Pittsburgh Penguins",
    "headquarters": "Pittsburgh, PA",
    "mascot": "Iceburgh",
    "winLossRatio": "2-0-0",
    "coach": "Mike Sullivan",
    "numberOfPlayers": 17
  },
  {
    "id": 2,
    "teamName": "New York Rangers",
    "headquarters": "New York, NY",
    "mascot": "None",
    "winLossRatio": "1-0-1",
    "coach": "Peter Philip Laviolette Jr.",
    "numberOfPlayers": 16
  },
  ...
]

```

2. Since our `json-server` doesn't support returning specific fields, you'll need to retrieve the entire teams resource and filter the response on the client side. See our doc for more on the [Limitations](xtra-limitations.md).

3. For more details on our API, see our [`teams`](res-teams.md) and []`games`](res-games.md) docs.

<a id="3"></a>
## Retrieve all win/loss records for the league using Postman Desktop

1. At various points in the season, you will want to see all teams' records to calculate standings. You can do this using a simple `GET` call.

    * **METHOD**: GET
    * **URL**: `{{base_url}}/teams`
    * **Headers**:
        * `Content-Type: application/json

The response should look like:

```json
[
    {
        "id": 1,
        "teamName": "Pittsburgh Penguins",
        "headquarters": "Pittsburgh, PA",
        "mascot": "Iceburgh",
        "winLossRatio": "2-0-0",
        "coach": "Mike Sullivan",
        "numberOfPlayers": 17
    },
    {
        "id": 2,
        "teamName": "New York Rangers",
        "headquarters": "New York, NY",
        "mascot": "None",
        "winLossRatio": "1-0-1",
        "coach": "Peter Philip Laviolette Jr.",
        "numberOfPlayers": 16
    },
    ...
]
```

2. Since our `json-server` doesn't support returning specific fields, you'll need to retrieve the entire teams resource and filter the response on the client side. See our doc for more on the [Limitations](xtra-limitations.md).

3. For more details on our API, see our [`teams`](res-teams.md) and []`games`](res-games.md) docs.

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
3. [Update your team's win/loss record](tut-update-winloss.md)

### [Back to Main Menu](nav.md)
