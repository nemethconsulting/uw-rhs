# Test your development system

1. Create and checkout a branch of your clone of the rec-hockey-service repo. Your `GitHub repo workspace` is the directory that contains your clone of the `uw-rhs` repo.

    ```shell
    cd <your GitHub repo workspace>
    ls
    # (see the uw-rhs directory in the list)
    cd uw-rhs
    git checkout -b -<the branch you want to test>
    cd api
    sh start-server.sh
    ```

    If your development system is installed correctly, you should see
    the service start and display the URL of the service: `http://localhost:3000`.

2. Make a test call to the service.

    ```shell
    curl http://localhost:3000/teams
    ```

3. If the service is running correctly, you should see a list of teams from the service, such as in this example.

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

If you don't see the list of teams, or receive an error in any step
of the procedure, investigate and correct the error before continuing.
Some common situations that cause errors include:

1. You mistyped a command.
2. You aren't in the correct directory.
3. A required software component didn't install correctly.
4. A required software component isn't up-to-date.

If you see the list of teams from the service, you're ready for the [Quick Start](quick-start.md).