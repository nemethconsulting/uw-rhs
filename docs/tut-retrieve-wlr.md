<div style="display: flex; align-items: center; justify-content: space-between;">
  <h1>Retrieve win/loss ratios across the league</h1>
  <img src="rhs-logo_4x4.jpeg" alt="Rec Hockey League Logo" style="width: 100px; height: 100px; margin-left: 20px;">
</div>

In this tutorial:

- You will learn how to retrieve the `winLossRatio` for the entire league.
- You will be introduced to some common errors and troubleshooting tips

## Table of contents
1. [Prerequisites](#1)
2. [Retrieve all win/loss records for the league using curl](#2)
3. [Retrieve all win/loss records for the league using Postman Desktop](#3)
4. [Errors & troubleshooting](#4)
5. [Related topics](#5)
6. [Back to main menu](nav.md)

<a id="1"></a>
## Prerequisites

- Make sure your system is running the API server. See [Test your set up](test-system.md) if you need help with this.
- Make sure you've already added all team details into the Rec Hockey Service API. See [Create an entry for your team](tut-create-team.md) for assistance.

<a id="2"></a>
## Retrieve all win/loss records for the league using curl

1. Retrieve all teams' records at any point during the season to calculate standings. You can do this using a simple `GET` call.

```bash
curl -X GET {base_url}/teams \
-H "Content-Type: application/json"
```

The response should look like:

```bash
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

2. Since our `json-server` doesn't support returning specific fields, you'll need to retrieve the entire teams resource and filter the response on the client side. See our doc for more on the [Limitations](xtra-limitations.md) of our server.

3. For more details on our API, see our [`teams`](res-teams.md) and [`games`](res-games.md) reference docs.

<a id="3"></a>
## Retrieve all win/loss records for the league using Postman Desktop

1. Retrieve all teams' records at any point during the season to calculate standings. You can do this using a simple `GET` call.

    * **METHOD**: GET
    * **URL**: `{base_url}/teams`
    * **Headers**:
        * `Content-Type: application/json'

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

2. Since our `json-server` doesn't support returning specific fields, you'll need to retrieve the entire teams resource and filter the response on the client side. See our doc for more on the [Limitations](xtra-limitations.md) of our server.

3. For more details on our API, see our [`teams`](res-teams.md) and [`games`](res-games.md) reference docs.

<a id="4"></a>
### Errors & troubleshooting

1. Errors often occur because of a mistyped command, including:
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
