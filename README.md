# Morrowind issues and how to fix them
While some of the fixes might work on OpenMW these docs focus exclusively on Morrowind.exe and modern Windows systems.

## Alt+Tab doesn't work or is clunky
1. Install [MGE XE](https://www.nexusmods.com/morrowind/mods/41102)
2. Open MGE XE settings (MGEXEgui.exe in main game folder)
3. Check "Windowed mode" and "Borderless window" in MGE XE settings:
![image](https://github.com/the-overdriven/morrowind-issues-and-fixes/assets/100090726/5e8f8763-8f46-4b04-bda4-b56161d81953)

## But I want to play in lower resolution and fullscreen
If your game's resolution doesn't match system screen resolution running the game in borderless window mode won't look like fullscreen.
Unfortunately in this case system's screen resolution has to be adjusted to be the same as game's resolution, so it imitates fullscreen.
But to not change the resolution manually every time you run the game you can create a simple .bat file that automates the following: 
1. Decreases the resolution, i.e. to 720p
2. Runs the game.
3. Increases the resolution (back to 1080p) after the game is closed.

```
start /b FullscreenLock
start /b /WAIT SetResolution 720 -noprompt
start /d "<path to game folder>" /WAIT Morrowind.exe
start /b /WAIT SetResolution 1080 -noprompt
taskkill /IM FullscreenLock.exe /F
```

Save it as .bat file, i.e. res_720_MW.bat. Create a shortcut, open its properties and in the Target field enter:
`C:\Windows\System32\cmd.exe /C "<path to the script>\res_720_MW.bat"`

## On multiple screens setup, moving mouse in game moves cursor on the second screen
Install [FullscreenLock](https://github.com/blaberry/FullscreenLock) and run it every time you run the game (the script above runs it automatically). The .exe file can be downloaded from the [Releases](https://github.com/blaberry/FullscreenLock/releases/tag/1.1) page. [Mirror](https://github.com/the-overdriven/FullscreenLock/releases/tag/1.1).

## Everything in game is too small. Fonts, UI, etc.
Open MGE XE settings and adjust the Menu UI scaling to your liking. Depending on game's resolution I find 1.20 - 1.50 values most optimal.

## I move like in slow motion, I want to run faster
For this purpose I find being able to edit GMST variables during game runtime the best solution, because you can adjust it to your liking every time instantly.
1. Install [GMST Menu](https://www.nexusmods.com/morrowind/mods/46428)
2. Run the game
3. Open Mod Configuration
4. Search for "GMST Menu", click it
5. You should see this screen:  
![image](https://github.com/the-overdriven/morrowind-issues-and-fixes/assets/100090726/2b28765a-13a1-4575-9caa-e090b31f2041)
6. Go to Floats tab
7. Search for "walk" or "run"
8. I like to have everyone walk slowly, but run quickly, so I find these values most optimal:
<details>
  <summary>My custom GMST variables</summary>

```
fFatigueSwimWalkBase = 2.5
fFatigueSwimWalkMult = 0
fMaxWalkSpeed = 80
fMinWalkSpeed = 20
fMinWalkSpeedCreature = 5
fStromWalkMult = 0.25
fSwimWalkAthleticsMult = 0.02
fSwimWalkBase = 0.5

fAthleticsRunBonus = 1
fBaseRunMultiplier = 5
fFatigueRunBase = 5
fFatigueRunMult = 2
fFatigueSwimRunBase = 7
fJumpRunMultiplier = 1
fSwimRunAthleticsMult = 0.1
fSwimRunBase = 0.5
fWereWolfRunMult = 1.5
```
</details>

## All my hits are missing
Dice-roll combat working as intended. But on a serious note, you can make the combat more dynamic by installing mods that make all swings have 100% chance to hit. I find [Better Balanced Combat](https://www.nexusmods.com/morrowind/mods/46596) to address this issue most tactfully, without breaking the balance too much, by taking side effects into consideration: i.e. fatigue is still important as the lower it is the higher is the chance to be knocked down, weapon skills also do not become meaningless but add a bonus to strength instead (which, rightfully, excludes the capacity bonus). Unfortunately, the mod also affects the regen rate, running speed and makes "You have failed casting the spell" popups disappear, which I'd personally prefer to leave as it is.

