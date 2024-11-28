# Rec Hockey League API Quick Start

Find your favorite team and get their schedule!

Once your system is [Set up](prerequisites.md), jump in and get started using our API.

## Table of Contents
1. [Before you start](#1)
2. Using Curl
    - [Find your team](#2)
    - [Get your team's schedule](#3)
3. Using Postman Desktop
    - [Find your team](#4)
    - [Get your team's schedule](#5)
4. [Next steps](#6)
5. [Back to Main Menu](nav.md)

<a id="1"></a>
## Before you start

Make sure the server is running on your local machine. If you need assistance with this, review our [Set up your system](prerequisites.md) and [Test your set up](test-system.md) docs.

## Using curl

<a id="2"></a>
### Find your team

1. Locate your team with a simple GET call to the `teams` resource.

```shell
curl "http://localhost:3000/teams"
```
2. The returned data should look like:
```shell
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

3. Scan the returned list and find your team. Note their `teamId` for next steps.

<a id="3"></a>
### Get your team's schedule
1. Use another GET call to pull your team's schedule from the `games` resource.

```shell
$ curl "http://localhost:3000/games?{teamId=}"
```
2. The returned data should look like:

```shell
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

<a id="4"></a>
### Find your team

1. In the Postman app, create a new request with these values:
    * **METHOD**: GET
    * **URL**: `http://localhost:3000/teams`
    * **Headers**:
        * `Content-Type: application/json`
    * **Request body**:
        You can change the values of each property as you'd like.
2. Choose **Send** to make the request.
3. Watch for the response body, which should look something like this. 

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
4. Scan the returned list and find your team. Note their `teamId` for next steps.

<a id="5"></a>
### Get your team's schedule

1. In the Postman app, create a new request with these values:
    * **METHOD**: GET
    * **URL**: `http://localhost:3000/games?teamId={teamId}
    * **Headers**:
        * `Content-Type: application/json`
    * **Request body**:
        You can change the values of each property as you'd like.
2. Choose **Send** to make the request.
3. Watch for the response body, which should look something like this. 
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

<a id="6"></a>
## Next steps

You've successfully started using our API! View the rest of our [docs](nav.md) to dive in deeper.

## [Back to Main Menu](nav.md)