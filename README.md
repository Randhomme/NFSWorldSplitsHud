# NFSWorldSplitsHud
A set of GFX files to display splits during a race (sprint and circuit)

## Installation

Download the [latest release](https://github.com/Randhomme/NFSWorldSplitsHud/releases/latest) for the server you want. Then drop the files in the `GFX` folder when your game is already running.

Currently available on :
- FreeroamSparkServer
- NightRiderz (will be included as a server mod directly)*
- Overdrive
- UndergroundStage
- Vanilla
- WorldEvolved
- WorldUnited

*there won't be any download link for NR since it will be already included in the server mods

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
1393,1393;2143,db0;2d72,c2f;3b87,e15;47f1,c6a;53be,bcd;5f14,b56;6aca,bb6;7600,b36;8029,a29;8925,8fc;9286,961;9c4c,9c6;a7a3,b57;b3cb,c28;b4f7,12c;c627,1130;d43a,e13;e0b5,c7b;ed38,c83;fcd6,f9e;10708,a32;11629,f21;124b2,e89;13585,10d3;152d9,1d54;163b4,10db;1777e,13ca;18278,afa;190e2,e6a;19fcb,ee9;1b47d,14b2;1c39b,f1e;1d145,daa;1e162,101d;1ef5a,df8;1ff0d,fb3;20e56,f49;2217e,1328;23034,eb6;23f82,f4e;2524a,12c8;265bc,1372;274a5,ee9;282b4,e0f;28f3c,c88;29a74,b38;2a690,c1c;2b568,ed8;2bf2e,9c6;2ceba,f8c;2da71,bb7;2e6f0,c7f;2f443,d53;300bd,c7a;30c77,bba;317cd,b56;32321,b54;32edf,bbe;3385a,97b;34141,8e7;34ac0,97f;354ca,a0a;3601c,b52;36b5d,b41;36e1a,2bd;37fd0,11b6;38dbd,ded;39984,bc7;3a6ce,d4a;3b670,fa2;3bfcf,95f;3ce45,e76;3ddde,f99;3ef34,1156;40c04,1cd0;41cce,10ca;42cce,1000;437be,af0;44569,dab;4543b,ed2;46900,14c5;477ce,ece;48589,dbb;4957f,ff6;4a3f3,e74;4b2d3,ee0;4c2ca,ff7;4d538,126e;4e400,ec8;4f3a4,fa4;5072a,1386;518bd,1193;526d1,e14;5347a,da9;540e3,c69;54cbe,bdb;55857,b99;56751,efa;570af,95e
```
Format is `Split1,Segment1;...;Split100,Segment100`, with all the values in milliseconds written in hexadecimal.
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
