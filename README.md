# NFSWorldSplitsHud
A set of GFX files to display splits during a race (sprint and circuit)

## Installation

Download the [latest release](https://github.com/Randhomme/NFSWorldSplitsHud/releases/latest) for the server you want. Then drop the files in the `GFX` folder when your game is already running.

Remember to install it again after a game restart, because the modded files will probably be restored to the original ones.

Currently available on :
- FreeroamSparkServer
- NightRiderz (as server mod)
- Overdrive
- UndergroundStage
- Vanilla
- WorldEvolved
- WorldUnited

## How does it work ?

### Things you probably don't need to know

- I had to move the ranking indicators (sprint and circuit) to `CommonHUD.gfx`. Technically speaking, `CommonHUD` now imports both ranking indicators to display them when needed. The reason is both `SprintRankingIndicator` and `CircuitRankingIndicator` can't use the global api commands (don't ask me why). And to load and save the splits outside the game, we need to use a command named `SetPersistentValue`. This command saves values to `UserSettings.xml`, under the `PersistentValue` tag.

- I also had to modify `RaceGadget.gfx` to retreive the correct event id and use it in the splits hud, since the `GetEventId` command gets the last lobby and not the race itself (it sounds confusing, but you can start a race from a completely different lobby, think about randomizer on WUGG or time attack mode on NR)

### Things you need to know

- Splits are saved in `UserSettings.xml` under `PersistentValue` > `ServerName` (the name of the server used in the settings, see below for more information) > `EventId_PersonalBest` and `EventId_ComparisonRun` (for exemple `Event1234_PersonalBest` for the event with 1234 as `Id`)

- During the race, the current splits are saved in the game (litteraly in the session) using the command `SetSessionValue`. A comparison to the personal best / comparison run is made each percent of the race. And if you finish the run ahead of your PB, the current splits are saved over your previous PB

- Since you will probably not play on only one server, you can change the server you are currently playing on by pressing the `Settings` button during a race (the button is below the comparison run field), then choose the server in the drop down menu. This allows you to save a PB and a comparison run for each race on every server instead of mixing stuff (event ids might overlap on different servers)

- A warning is displayed top right of the screen when you enter freeroam for the first time in your session. It's a reminder to set the server (see the point above). It will be shown only once during your session. You can click on the close button to close it. And you can chose to not see this warning anymore by unchecking the check box in the `Settings` menu of the splits mod

- Last but not least : you can import a run of your choice to use it as a comparison run during a race. To do so, open `ComparisonRun.txt` (you need to move this file to the `GFX` folder of your game). The file needs to start by `comparisonRun=`, paste your run after the `=`, then click the `Import` button to load the pasted run

### Exemple run

Here is how a run looks like (it's a 5:56.527 on Highway 142) :
```
1393;2143;2d72;3b87;47f1;53be;5f14;6aca;7600;8029;8925;9286;9c4c;a7a3;b3cb;b4f7;c627;d43a;e0b5;ed38;fcd6;10708;11629;124b2;13585;152d9;163b4;1777e;18278;190e2;19fcb;1b47d;1c39b;1d145;1e162;1ef5a;1ff0d;20e56;2217e;23034;23f82;2524a;265bc;274a5;282b4;28f3c;29a74;2a690;2b568;2bf2e;2ceba;2da71;2e6f0;2f443;300bd;30c77;317cd;32321;32edf;3385a;34141;34ac0;354ca;3601c;36b5d;36e1a;37fd06;38dbd;39984;3a6ce;3b670;3bfcf;3ce45;3ddde;3ef34;40c04;41cce;42cce;437be;44569;4543b;46900;477ce;48589;4957f;4a3f3;4b2d3;4c2ca;4d538;4e400;4f3a4;5072a;518bd;526d1;5347a;540e3;54cbe;55857;56751;570af
```
Format is `split1;...;split100`, with all the values in milliseconds written in hexadecimal.
You can import this run as a comparison run by pasting it in `ComparisonRun.txt` and clicking the `Import` button, as written above

## The features
- Current split and segment displayed during the race (for each percent)
- Delta with PB or a comparison run of your choice (use the buttons to switch between PB and comparison run)
- Server drop down menu to have splits for each server (in the settings menu of the splits mod)
- Personal best and comparison run saved in `UserSettings.xml` (will be updated only after game close)
- As a bonus, a restart race button (top bar, nfs world logo, a little bit alone, you can't miss it)

## Known bugs and issues
- If `ComparisonRun.txt` is empty, clicking `Import` button crashes the game
- Personal best and comparison run will be updated in `UserSettings.xml` only after closing the game

You found a bug, or you have an idea for an improvement ? Contact me on Discord !

## How does it look ?

It looks like this :

![Screenshot of the splits hud in action, on Highway 142, the best race ever](/nfsw001.png)
