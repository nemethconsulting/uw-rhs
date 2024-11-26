# Teams Resource

## Overview
The `teams` resource manages information about hockey teams, including their names, mascots, and statistics.

## Table of Contents
1. [Base URL](#1)
2. [Fields](#2)
3. [Operations](#3)
    - [GET](#4)
    - [POST](#5)
    - [PATCH](#6)
    - [DELETE](#7)
4. [Error Codes](#8)
5. [Back to Main Menu](nav.md)

<a id="1"></a>
## Base URL
`/teams`

<a id="2"></a>
## Fields

| Field Name      | Type     | Required | Description                           | Example Value       |
|------------------|----------|----------|---------------------------------------|---------------------|
| `id`            | Integer  | Yes      | Unique identifier for the team.       | `5`                 |
| `teamName`      | String   | Yes      | Name of the team.                     | `"Seattle Kraken"`  |
| `headquarters`  | String   | No       | Location of the team headquarters.    | `"Seattle, WA"`     |
| `mascot`        | String   | No       | Name of the team's mascot.            | `"Buoy the Troll"`  |
| `winLossRatio`  | String   | No       | Format: `Wins-Losses-Overtime Losses` | `"2-1-0"`           |
| `coach`         | String   | No       | Name of the team's coach.             | `"Dave Hakstol"`    |
| `numberOfPlayers`| Integer | No       | Number of players on the team.        | `23`                |

<a id="3"></a>
## Operations

<a id="4"></a>
### GET `/teams`
Retrieve all teams.

#### Example Request
```shell
curl -X GET http://localhost:3000/teams
```

#### Example Response

```shell
[
  {
    "id": 5,
    "teamName": "Seattle Kraken",
    "headquarters": "Seattle, WA",
    "mascot": "Buoy the Troll",
    "winLossRatio": "2-1-0",
    "coach": "Dave Hakstol",
    "numberOfPlayers": 23
  },
  {
    "id": 6,
    "teamName": "New Jersey Devils",
    "headquarters": "Newark, NJ",
    "mascot": "NJ Devil",
    "winLossRatio": "3-0-0",
    "coach": "Lindy Ruff",
    "numberOfPlayers": 22
  },
  ...
]
```

<a id="5"></a>
### POST `/teams`
Add a new team

#### Example Request

```shell
curl -X POST http://localhost:3000/teams \
-H "Content-Type: application/json" \
-d '{
  "teamName": "Pittsburgh Penguins",
  "headquarters": "Pittsburgh, PA",
  "mascot": "Iceburgh",
  "winLossRatio": "0-0-0",
  "coach": "Mike Sullivan",
  "numberOfPlayers": 21
}'
```

#### Example Response

```shell
{
  "id": 7,
  "teamName": "Pittsburgh Penguins",
  "headquarters": "Pittsburgh, PA",
  "mascot": "Iceburgh",
  "winLossRatio": "0-0-0",
  "coach": "Mike Sullivan",
  "numberOfPlayers": 21
}
```

<a id="6"></a>
### PATCH `/teams`
Update specific fields of an existing team.

#### Example Request

```shell
curl -X PATCH http://localhost:3000/teams/5 \
-H "Content-Type: application/json" \
-d '{
  "winLossRatio": "3-1-0",
  "coach": "New Coach Name"
}'
```

#### Example Response

```shell
{
  "id": 5,
  "teamName": "Seattle Kraken",
  "headquarters": "Seattle, WA",
  "mascot": "Buoy the Troll",
  "winLossRatio": "3-1-0",
  "coach": "New Coach Name",
  "numberOfPlayers": 23
}
```

<a id="7"></a>
### DELETE `/teams/{id}`
Remove an existing team.

#### Example Request

```
curl -X DELETE http://localhost:3000/teams/7
```

#### Example Response

```
{}
```

<a id="8"></a>
## Error Codes 
See our [Error Codes](xtra-errors.md) doc for guidance and troubleshooting

## [Back to Main Menu](nav.md)
