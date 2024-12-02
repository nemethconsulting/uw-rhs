<div style="display: flex; align-items: center; justify-content: space-between;">
  <h1>Rec Hockey League API Quick Start</h1>
  <img src="rhs-logo_4x4.jpeg" alt="Rec Hockey League Logo" style="width: 100px; height: 100px; margin-left: 20px;">
</div>

Find your team and get their schedule!

Once your system is [set up](prerequisites.md) and [tested](test-system.md), jump in and get started using our API.

## Table of Contents
2. Using curl
    - [Find your team](#1)
    - [Get your team's schedule](#2)
3. Using Postman Desktop
    - [Find your team](#3)
    - [Get your team's schedule](#4)
4. [Next steps](#5)
5. [Back to Main Menu](nav.md)

## Using curl

<a id="1"></a>
### Find your team

1. Locate your team with a simple `GET` call to the `teams` resource.

```bash
curl {base_url}/teams"
```
2. The response should look like:

```bash
[
  {
    "teamId": 1,
    "teamName": "Pittsburgh Penguins",
    "headquarters": "Pittsburgh, PA",
    "mascot": "Iceburgh",
    "winLossRatio": "0-0-0",
    "coach": "Mike Sullivan",
    "numberOfPlayers": 17
  },
  {
    "teamId": 2,
    "teamName": "New York Rangers",
    "headquarters": "New York, NY",
    "mascot": "None",
    "winLossRatio": "0-0-0",
    "coach": "Peter Philip Laviolette Jr.",
    "numberOfPlayers": 16
  },
  ...
```

3. Scan the returned list and find your team. Note their team `id` for next steps.

<a id="2"></a>
### Get your team's schedule

1. Use another `GET` call to pull your team's schedule from the `games` resource.

```bash
$ curl {base_url}/games/{id}
```
2. The response should look like:

```bash
[
  {
    "teamId": 4,
    "teamName": "Washington Capitals",
    "season": "2024-2025",
    "seasonGames": [
      {
        "gameNumber": 1,
        "date": "2024-10-08T19:30:00-05:00",
        "homeGame": true,
        "opposingTeam": "New Jersey Devils",
        "locationName": "Capital One Arena",
        "locationAddress": "601 F St NW, Washington, DC 20004",
        "finalScore": "TBD"
      },
      {
        "gameNumber": 2,
        "date": "2024-10-11T19:30:00-05:00",
        "homeGame": true,
        "opposingTeam": "Las Vegas Golden Knights",
        "locationName": "Capital One Arena",
        "locationAddress": "601 F St NW, Washington, DC 20004",
        "finalScore": "TBD"
      }
    ]
  }
]
```

## Using Postman Desktop

<a id="3"></a>
### Find your team

1. In the Postman app, create a new request with these values:
    * **METHOD**: GET
    * **URL**: `{base_url}/teams`
    * **Headers**:
        * `Content-Type: application/json`
    * **Request body**:
        You can change the values of each property as needed.

2. Click **Send** to make the request.

3. The response should look like:

```js
    [
    {
        "teamId": 1,
        "teamName": "Pittsburgh Penguins",
        "headquarters": "Pittsburgh, PA",
        "mascot": "Iceburgh",
        "winLossRatio": "0-0-0",
        "coach": "Mike Sullivan",
        "numberOfPlayers": 17
    },
    {
        "teamId": 2,
        "teamName": "New York Rangers",
        "headquarters": "New York, NY",
        "mascot": "None",
        "winLossRatio": "0-0-0",
        "coach": "Peter Philip Laviolette Jr.",
        "numberOfPlayers": 16
    },
    ...
```
4. Scan the returned list and find your team. Note their team `id` for next steps.

<a id="4"></a>
### Get your team's schedule

1. In the Postman app, create a new request with these values:
    * **METHOD**: GET
    * **URL**: `{base_url}/games/{id}`
    * **Headers**:
        * `Content-Type: application/json`
    * **Request body**:
        You can change the values of each property as needed.

2. Click **Send** to make the request.

3. The response should look like:

```js
[
    {
        "teamId": 4,
        "teamName": "Washington Capitals",
        "season": "2024-2025",
        "seasonGames": [
            {
                "gameNumber": 1,
                "date": "2024-10-08T19:30:00-05:00",
                "homeGame": true,
                "opposingTeam": "New Jersey Devils",
                "locationName": "Capital One Arena",
                "locationAddress": "601 F St NW, Washington, DC 20004",
                "finalScore": "TBD"
            },
            {
                "gameNumber": 2,
                "date": "2024-10-11T19:30:00-05:00",
                "homeGame": true,
                "opposingTeam": "Las Vegas Golden Knights",
                "locationName": "Capital One Arena",
                "locationAddress": "601 F St NW, Washington, DC 20004",
                "finalScore": "TBD"
            }
...
```

<a id="5"></a>
## Next steps

You've successfully started using the Rec Hockey League API! View the rest of our [docs](nav.md) to dive in deeper.

## [Back to Main Menu](nav.md)