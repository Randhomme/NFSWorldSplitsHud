# NFSWorldSplitsHud
A set of GFX files to display splits during a race (sprint and circuit)

## Installation

Download the [latest release](https://github.com/Randhomme/NFSWorldSplitsHud/releases/latest) for the server you want. Then drop the files in the `GFX` folder when your game is already running.

Currently available on :
- WorldUnited

## How does it work ?

### Things you probably don't need to know

- I had to move the ranking indicators (sprint and circuit) to `CommonHUD.gfx`. Technically speaking, `CommonHUD` now imports both ranking indicators to display them when needed. The reason is both `SprintRankingIndicator` and `CircuitRankingIndicator` can't use the global api commands (don't ask me why). And to load and save the splits outside the game, we need to use a command named `SetPersistentValue`. This command saves values to `UserSettings.xml`, under the `PersistentValue` tag. Splits are saved under `PersistentValue` > `ServerName` (the name of the server used in the settings, see below for more information) > `EventId_PersonalBest` and `EventId_ComparisonRun`

- I also had to modify `RaceGadget.gfx` to retreive the correct event id and use it in the splits hud, since the `GetEventId` command gets the last lobby and not the race itself (it sounds confusing, but you can start a race from a completely different lobby, think about randomizer on WUGG or time attack mode on NR)

### Things you need to know

- During the race, the current splits are saved in the game (litteraly in the session) using the command `SetSessionValue`. A comparison to the personal best / comparison run is made each percent of the race. And if you finish the run ahead of your PB, the current splits are saved over your previous PB

- Since you will probably not play on only one server, you can change the server you are currently playing on by pressing the `Settings` button during a race (the button is below the comparison run field), then choose the server in the drop down menu. This allows you to save a PB and a comparison run for each race on every server instead of mixing stuff (event ids might overlap on different servers)

- A warning is displayed top right of the screen when you enter freeroam for the first time in your session. It's a reminder to set the server (see the point above). It will be shown only once during your session. You can click on the close button to close it. And you can chose to not see this warning anymore by unchecking the check box in the `Settings` menu of the splits mod

- Last but not least : you can import a run of your choice to use it as a comparison run during a race. To do so, open `ComparisonRun.txt` (you need to move this file to the `GFX` folder of your game). The file needs to start by `comparisonRun=`, paste your run after the `=`, then click the `Import` button to load the pasted run

## The features
- Current split and segment displayed during the race (for each percent)
- Delta with PB or a comparison run of your choice (use the buttons to swith between PB and comparison run)
- Server drop down menu to have splits for each server (in the settings menu of the splits mod)
- As a bonus, a restart race button (top bar, nfs world logo, a little bit alone, you can't miss it)

## How does it look ?

I don't know, maybe it's not that bad ?

![Screenshot of the splits hud in action, on Highway 142, the best race ever](/nfsw001.png)
