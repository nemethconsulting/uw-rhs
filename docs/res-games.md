Understanding the games resource in the Hockey League API

_Coming Soon_

This page is still under construction, but the table below provides details for making a call to our games resource:

### **Season Game Object Fields**

| **Field Name**    | **Type**  | **Description**                                                                |
|--------------------|-----------|--------------------------------------------------------------------------------|
| `gameNumber`       | Integer   | The sequential number of the game in the season.                               |
| `date`             | String    | Date and time of the game in ISO 8601 format (e.g., `2024-10-15T19:00:00Z`).   |
| `homeGame`         | Boolean   | Indicates whether the team is playing at home (`true`) or away (`false`).      |
| `opposingTeam`     | String    | Name of the opposing team.                                                     |
| `locationName`     | String    | Name of the location/arena where the game is played.                           |
| `locationAddress`  | String    | Physical address of the game location.                                         |
| `finalScore`       | String    | Final score of the game in the format `teamScore-opponentScore` or `TBD`.      |

