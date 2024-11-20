# Create an entry for your team

In this tutorial:

- You will learn how to add a team to the Rec Hockey Service
- You will learn how to do this using both curl and Postman Desktop
- You will gain an understanding of how this API deals with Null values

## Table of Contents
- [Prerequisites](#1)
- [Add your team using curl](#2)
- [Add your team using Postman Desktop](#3)
- [Note on Null fields](#4)
- [Related Topics](#5)
- [Back to Main Menu](nav.md)

<a id="1"></a>
## Prerequisties

- Make sure your system is running the API server. See [Test your set up](test-system.md) if you need help with this.

<a id="2"></a>
## Add your team using curl

1. Start with `GET` call to see the list of current teams in the league database.

```shell
curl http://{base_url}/teams
```

The output should look like:

```shell
[
  {
    "teamId": 1,
    "teamName": "Pittsburgh Penguins",
    "headquarters": "Pittsburgh, PA",
    "mascot": "Iceburgh",
    "winLossRatio": "0-0-0",
    "coach": "Mike Sullivan",
    "numberOfPlayers": "17"
  },
  ...
  ```

2. Note the required fields and make sure you have the appropriate data for entry. If you do not have all the data, see [Note on Null fields](#4) below.

3. Review the list of teams and notes the final `teamId`. Your input for this field will the highest `teamId` +1. (In the example below, there are already 4 teams in the database, so a new team would take the Id of 5)

4. With your data on hand, make the following `POST` to the API.

```shell
curl -X POST http://localhost:3000/teams \
-H "Content-Type: application/json" \
-d '{
        "id": 5,
        "teamName": "your team name",
        "headquarters": "your city and state",
        "mascot": "the name of your mascot",
        "winLossRatio": "win-loss-OT loss",
        "coach": "name of your coach",
        "numberOfPlayers": 0
        }'
```

A successful response will look like this:
```shell
{
  "id": 5,
  "teamName": "your team name",
  "headquarters": "your city and state",
  "mascot": "the name of your mascot",
  "winLossRatio": "win-loss-OT loss",
  "coach": "name of your coach",
  "numberOfPlayers": 0
}
```

5. With your team created, you can go ahead and start adding your [team's schedule](tut-add-games.md).

<a id="3"></a>
## Add your team using Postman Desktop

...

<a id="4"></a>
## Note on Null Fields

...

<a id="5"></a>
## Related Topics

...

### [Back to Main Menu](nav.md)
