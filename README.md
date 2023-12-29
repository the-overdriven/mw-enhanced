# Morrowind issues and how to fix them
Morrowind is a great game, but can be made ever greater (and less clunky) thanks to 20 years of modding wonders. While some of the fixes might work on OpenMW these docs focus exclusively on Morrowind.exe and modern Windows systems.

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

## Game hangs when closing it
Install [Expeditious Exit](https://www.nexusmods.com/morrowind/mods/45634)

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
fMaxWalkSpeed = 80
fMinWalkSpeed = 20
fMinWalkSpeedCreature = 5
fStromWalkMult = 0.25
fSwimWalkAthleticsMult = 0.02
fSwimWalkBase = 0.5

fAthleticsRunBonus = 1
fBaseRunMultiplier = 5
fJumpRunMultiplier = 1
fSwimRunAthleticsMult = 0.1
fSwimRunBase = 0.5
fWereWolfRunMult = 1.5
```
</details>

GMST Menu also removes the necessity of juggling around with .esp plugins whose only purpose is to modify these variables.

## I use up all my fatigue for moving around, so I have none left for fighting

Use the forementioned GMST Menu to halve the fatigue corresponding variables:

```
fFatigueRunBase = 5 to 2.5
fFatigueRunMult = 2 to 1
fFatigueSneakBase = 1.5 to 0.75
fFatigueSneakMult = 1.5 to 0.75
fFatigueSwimRunBase = 7 to 3.5
fFatigueSwimWalkBase = 2.5 to 1.25
```

To offset movement fatigue being halved one can double fatigue costs of jumping, attacking and blocking:
```
fFatigueAttackBase = 2 to 4
fFatigueBlockBase = 4 to 8
fFatigueJumpBase = 2 to 4
```

These especially make sense to cost more fatigue when using hit-chance simplifying mods (such as Better Balanced Combat), which make the combat last shorter.

## All my hits are missing
Dice-roll combat working as intended. But on a serious note, you can make the combat more dynamic by installing mods that make all swings have 100% chance to hit. I find [Better Balanced Combat](https://www.nexusmods.com/morrowind/mods/46596) to address this issue most tactfully, without breaking the balance too much, by taking side effects into consideration: i.e. fatigue is still important as the lower it is the higher is the chance to be knocked down, weapon skills also do not become meaningless but add a bonus to strength instead (which, rightfully, excludes the encumbrance bonus). Unfortunately, the mod also affects the regen rate, running speed and makes "You have failed casting the spell" popups disappear, which I'd personally prefer to leave as it is.

## Killed enemies respawn like in some kind of MMO
Install [No Respawns](https://www.nexusmods.com/morrowind/mods/53853)

## Difficulty (some enemies) scale with level, I want more challenges early game
Install [OperatorJack's Deleveler](https://www.nexusmods.com/morrowind/mods/47897)

## Looting is clunky, too much clicking
Install [QuickLoot](https://www.nexusmods.com/morrowind/mods/46283)

## Outside of cities, everything that moves wants to kill me
Install [Non-Homicidal Ecosystem](https://www.nexusmods.com/morrowind/mods/42327)  
Could be even better if these attacks were based on player's level or health (weak monsters should be afraid to attack strong player)

## I'm lost in Vivec, every canton looks the same
Install [Colorful Vivec](https://www.nexusmods.com/morrowind/mods/53806)

## I'm pestered by dark assassins from Tribunal content early game
Install [Tribunal Delayed](https://www.nexusmods.com/morrowind/mods/33973/)

## I'm encumbered all the time
Install [Encumberance increaser](https://www.nexusmods.com/morrowind/mods/28213)

## I want to have a stash for items but can't put much in containers
Install [ContainerWeightMaxed](https://www.nexusmods.com/morrowind/mods/45698)  
Even if using QuickLoot, [inom - Inventory mouse wheel](https://www.nexusmods.com/morrowind/mods/46847) might still be helpful here for moving items from/to container quicker.

## Very few dialogues are voiced
Install AI-generated [Kezyma's Voices of Vvardenfell](https://www.nexusmods.com/morrowind/mods/52279)

## Dialogues with NPCs are too repeatable
Install [UI Expansion](https://www.nexusmods.com/morrowind/mods/46071) and [Dialogues Decluttered](https://www.nexusmods.com/morrowind/mods/48301)
