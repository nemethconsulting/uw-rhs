<div style="display: flex; align-items: center; justify-content: space-between;">
  <h1>Teams resource</h1>
  <img src="rhs-logo_4x4.jpeg" alt="Rec Hockey League Logo" style="width: 100px; height: 100px; margin-left: 20px;">
</div>

## Overview

The `teams` resource manages information about hockey teams, including their names, mascots, and win/loss records.

## Table of contents
1. [Base URL](#1)
2. [Resource properties](#2)
3. [Operations](#3)
    - [GET](#4)
    - [POST](#5)
    - [PATCH](#6)
    - [DELETE](#7)
4. [Error codes](#8)
5. [Back to main menu](nav.md)

<a id="1"></a>
## Base URL

`/teams`

<a id="2"></a>
## Resource properties

Sample `teams` resource

```json
{
  "id": 5,
  "teamName": "Seattle Kraken",
  "headquarters": "Seattle, WA",
  "mascot": "Buoy the Troll",
  "winLossRatio": "3-1-0",
  "coach": "Dan Bylsma",
  "numberOfPlayers": 23
}
```

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

#### Example request

```bash
curl -X GET {base_url}/teams
```

#### Example response

```json
[
  {
    "id": 1,
    "teamName": "Pittsburgh Penguins",
    "headquarters": "Pittsburgh, PA",
    "mascot": "Iceburgh",
    "winLossRatio": "0-0-0",
    "coach": "Mike Sullivan",
    "numberOfPlayers": 20
  },
  {
    "id": 2,
    "teamName": "New York Rangers",
    "headquarters": "New York, NY",
    "mascot": "None",
    "winLossRatio": "0-0-0",
    "coach": "Peter Laviolette",
    "numberOfPlayers": 22
  },
  ...
]
```

<a id="5"></a>
### POST `/teams`

Add a new team

#### Example request

**Note** When you set the `id` to null, the server will generate a unique identifier for the new team.

```bash
curl -X POST {base_url}/teams \
-H "Content-Type: application/json" \
-d '{
  "id": null,
  "teamName": "Los Angeles Kings",
  "headquarters": "Los Angeles, CA",
  "mascot": "Bailey the Lion",
  "winLossRatio": "0-0-0",
  "coach": "Todd McLellan",
  "numberOfPlayers": 23
}'
```

#### Example response

```json
{
  "id": 10,
  "teamName": "Los Angeles Kings",
  "headquarters": "Los Angeles, CA",
  "mascot": "Bailey the Lion",
  "winLossRatio": "0-0-0",
  "coach": "Todd McLellan",
  "numberOfPlayers": 23
}
```

<a id="6"></a>
### PATCH `/teams/{id}`

Update the details of an existing team. Since the server does not support partial updates, the full team resource must be included in the request.

#### Example request

```bash
curl -X PATCH {base_url}/teams/5 \
-H "Content-Type: application/json" \
-d '{
  "id": 5,
  "teamName": "Seattle Kraken",
  "headquarters": "Seattle, WA",
  "mascot": "Buoy the Troll",
  "winLossRatio": "3-1-0",
  "coach": "Dan Bylsma",
  "numberOfPlayers": 23
}'
```

#### Example response

```json
{
  "id": 5,
  "teamName": "Seattle Kraken",
  "headquarters": "Seattle, WA",
  "mascot": "Buoy the Troll",
  "winLossRatio": "3-1-0",
  "coach": "Dan Bylsma",
  "numberOfPlayers": 23
}
```

<a id="7"></a>
### DELETE `/teams/{id}`

This operation will permanently remove the team and its associated data from the API.

#### Example request

```bash
curl -X DELETE {base_url}/teams/7
```

#### Example response

```json
{}
```

<a id="8"></a>
## Error codes 

See our [Error codes](xtra-errors.md) doc for guidance and troubleshooting

### [Back to main menu](nav.md)
