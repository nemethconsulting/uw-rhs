<div style="display: flex; align-items: center; justify-content: space-between;">
  <h1>Games resource</h1>
  <img src="rhs-logo_4x4.jpeg" alt="Rec Hockey League Logo" style="width: 100px; height: 100px; margin-left: 20px;">
</div>

## Overview
The `games` resource manages information about your team's hockey schedule, including dates, locations, and final scores.

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
`/games`

<a id="2"></a>
## Resource properties

Sample `games` resource

```json
{
  "id": 6,
  "teamName": "New Jersey Devils",
  "season": "2024-2025",
  "seasonGames": [
    {
      "gameNumber": 1,
      "date": "2024-10-04T19:00:00-05:00",
      "homeGame": true,
      "opposingTeam": "Philadelphia Flyers",
      "locationName": "Prudential Center",
      "locationAddress": "25 Lafayette St, Newark, NJ 07102",
      "finalScore": "TBD"
    },
    {
      "gameNumber": 2,
      "date": "2024-10-08T19:00:00-05:00",
      "homeGame": false,
      "opposingTeam": "New York Rangers",
      "locationName": "Madison Square Garden",
      "locationAddress": "4 Pennsylvania Plaza, New York, NY 10001",
      "finalScore": "TBD"
    }
  ]
}
```

| Field Name      | Type     | Required | Description                                         | Example Value               |
|------------------|----------|----------|-----------------------------------------------------|-----------------------------|
| `id`            | Integer  | Yes      | Unique identifier for the game resource.           | `5`                         |
| `teamName`      | String   | Yes      | Name of the team playing the game.                 | `"Seattle Kraken"`          |
| `season`        | String   | Yes      | The season for which the game is scheduled.         | `"2024-2025"`               |
| `seasonGames`   | Array    | Yes      | List of games scheduled for the season.            | `[ ... ]`                   |
| `gameNumber`    | Integer  | Yes      | Sequence number of the game in the season schedule.| `1`                         |
| `date`          | String   | Yes      | Date and time the game is scheduled (ISO 8601).    | `"2024-10-03T19:00:00-08:00"`|
| `homeGame`      | Boolean  | Yes      | Indicates if the team is playing at home.          | `true`                      |
| `opposingTeam`  | String   | Yes      | Name of the opposing team.                         | `"Vegas Golden Knights"`    |
| `locationName`  | String   | Yes      | Name of the venue where the game is held.          | `"Climate Pledge Arena"`    |
| `locationAddress`| String  | Yes      | Address of the venue.                              | `"334 1st Ave N, Seattle, WA 98109"`|
| `finalScore`    | String   | No       | Final score of the game in `X-Y` format.           | `"4-2"`                     |

<a id="3"></a>
## Operations

<a id="4"></a>
### GET `/games/{id}`

Retrieve a team's schedule (or all teams' schedules if an `id` is not specified).

#### Example request

```bash
curl -X GET {base_url}/games/5
```

#### Example response

```json
[
  {
    "id": 5,
    "teamName": "Seattle Kraken",
    "season": "2024-2025",
    "seasonGames": [
      {
        "gameNumber": 1,
        "date": "2024-10-03T19:00:00-08:00",
        "homeGame": true,
        "opposingTeam": "Vegas Golden Knights",
        "locationName": "Climate Pledge Arena",
        "locationAddress": "334 1st Ave N, Seattle, WA 98109",
        "finalScore": "TBD"
      },
      {
        "gameNumber": 2,
        "date": "2024-10-07T19:00:00-08:00",
        "homeGame": false,
        "opposingTeam": "Calgary Flames",
        "locationName": "Scotiabank Saddledome",
        "locationAddress": "555 Saddledome Rise SE, Calgary, AB T2G 2W1",
        "finalScore": "TBD"
      }
    ]
  }
]
```

### POST '/games/{id}`

Add a new team's schedule

<a id="5"></a>
#### Example request

```bash
curl -X POST {base_url}/games \
-H "Content-Type: application/json" \
-d '{
  "id": 6,
  "teamName": "New Jersey Devils",
  "season": "2024-2025",
  "seasonGames": [
    {
      "gameNumber": 1,
      "date": "2024-10-04T19:00:00-05:00",
      "homeGame": true,
      "opposingTeam": "Philadelphia Flyers",
      "locationName": "Prudential Center",
      "locationAddress": "25 Lafayette St, Newark, NJ 07102",
      "finalScore": "TBD"
    },
    {
      "gameNumber": 2,
      "date": "2024-10-08T19:00:00-05:00",
      "homeGame": false,
      "opposingTeam": "New York Rangers",
      "locationName": "Madison Square Garden",
      "locationAddress": "4 Pennsylvania Plaza, New York, NY 10001",
      "finalScore": "TBD"
    }
  ]
}'
```

#### Example response

```json
{
  "id": 6,
  "teamName": "New Jersey Devils",
  "season": "2024-2025",
  "seasonGames": [
    {
      "gameNumber": 1,
      "date": "2024-10-04T19:00:00-05:00",
      "homeGame": true,
      "opposingTeam": "Philadelphia Flyers",
      "locationName": "Prudential Center",
      "locationAddress": "25 Lafayette St, Newark, NJ 07102",
      "finalScore": "TBD"
    },
    {
      "gameNumber": 2,
      "date": "2024-10-08T19:00:00-05:00",
      "homeGame": false,
      "opposingTeam": "New York Rangers",
      "locationName": "Madison Square Garden",
      "locationAddress": "4 Pennsylvania Plaza, New York, NY 10001",
      "finalScore": "TBD"
    }
  ]
}
```

<a id="6"></a>
### PATCH `/games`

Update specific fields in a team's game schedule.

This operation replaces the entire schedule for the specified team. Partial updates to the `seasonGames` array are not supported.

#### Example request

```bash
curl -X PATCH {base_url}/games/5 \
-H "Content-Type: application/json" \
-d '{
  "id": 5,
  "teamName": "Seattle Kraken",
  "season": "2024-2025",
  "seasonGames": [
    {
      "gameNumber": 1,
      "date": "2024-10-03T19:00:00-08:00",
      "homeGame": true,
      "opposingTeam": "Vegas Golden Knights",
      "locationName": "Climate Pledge Arena",
      "locationAddress": "334 1st Ave N, Seattle, WA 98109",
      "finalScore": "4-2"
    },
    {
      "gameNumber": 2,
      "date": "2024-10-07T19:00:00-08:00",
      "homeGame": false,
      "opposingTeam": "Calgary Flames",
      "locationName": "Scotiabank Saddledome",
      "locationAddress": "555 Saddledome Rise SE, Calgary, AB T2G 2W1",
      "finalScore": "TBD"
    }
  ]
}'
```

#### Example response

```json
{
  "id": 5,
  "teamName": "Seattle Kraken",
  "season": "2024-2025",
  "seasonGames": [
    {
      "gameNumber": 1,
      "date": "2024-10-03T19:00:00-08:00",
      "homeGame": true,
      "opposingTeam": "Vegas Golden Knights",
      "locationName": "Climate Pledge Arena",
      "locationAddress": "334 1st Ave N, Seattle, WA 98109",
      "finalScore": "4-2"
    },
    {
      "gameNumber": 2,
      "date": "2024-10-07T19:00:00-08:00",
      "homeGame": false,
      "opposingTeam": "Calgary Flames",
      "locationName": "Scotiabank Saddledome",
      "locationAddress": "555 Saddledome Rise SE, Calgary, AB T2G 2W1",
      "finalScore": "TBD"
    }
  ]
}
```

<a id="7"></a>
### DELETE `/games/{id}`

Remove the entire schedule for a team.

Deletes the schedule for the specified team, including all nested seasonGames.

#### Example request

```bash
curl -X DELETE {base_url}/games/5
```

#### Example response

```json
{}
```

<a id="8"></a>
## Error codes 

See our [Error Codes](xtra-errors.md) doc for guidance and troubleshooting

### [Back to main menu](nav.md)