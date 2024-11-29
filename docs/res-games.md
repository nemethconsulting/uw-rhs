<div style="display: flex; align-items: center; justify-content: space-between;">
  <h1>Games Resource</h1>
  <img src="rhs-logo_4x4.jpeg" alt="Rec Hockey League Logo" style="width: 100px; height: 100px; margin-left: 20px;">
</div>

## Overview
The `games` resource manages information about your team's hockey schedule, including dates, locations, and final scores.

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
`/games`

<a id="2"></a>
## Fields

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
| `finalScore`    | String   | No       | Final score of the game in `X-Y` format or `"TBD"`. | `"4-2"`                     |

<a id="3"></a>
## Operations

<a id="4"></a>
### GET `/games/{id}`
Retrieve a team's schedule (or all teams' schedules if an `id` is not specified).

#### Example Request
```bash
curl -X GET http://localhost:3000/games
```

#### Example Response

```shell
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
#### Example Request

```
curl -X POST http://localhost:3000/games \
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

#### Example Response

```
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
Replaces the entire schedule for the team specified by id. Partial updates to the seasonGames array are not supported.

#### Example Request

```
curl -X PATCH http://localhost:3000/games/5 \
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
    },
    {
      "gameNumber": 3,
      "date": "2024-10-15T19:00:00-08:00",
      "homeGame": true,
      "opposingTeam": "Edmonton Oilers",
      "locationName": "Climate Pledge Arena",
      "locationAddress": "334 1st Ave N, Seattle, WA 98109",
      "finalScore": "TBD"
    }
  ]
}'
```

#### Example Response

```
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
    },
    {
      "gameNumber": 3,
      "date": "2024-10-15T19:00:00-08:00",
      "homeGame": true,
      "opposingTeam": "Edmonton Oilers",
      "locationName": "Climate Pledge Arena",
      "locationAddress": "334 1st Ave N, Seattle, WA 98109",
      "finalScore": "TBD"
    }
  ]
}
```

<a id="7"></a>
### DELETE `/games/{id}`
Remove the entire schedule for a team
Deletes the schedule for the specified team, including all nested seasonGames.

#### Example Request

```
curl -X DELETE http://localhost:3000/games/5
```

#### Example Response

```
{}
```

<a id="8"></a>
## Error Codes 
See our [Error Codes](xtra-errors.md) doc for guidance and troubleshooting

## [Back to Main Menu](nav.md)