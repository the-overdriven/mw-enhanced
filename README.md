# Morrowind issues and how to fix them
Morrowind is a great game, but can be made even greater (and less clunky) by customizing it with the 20+ years of its wonderous modding heritage. While some of these solutions might work on OpenMW these docs focus exclusively on Morrowind.exe and modern Windows systems. Most of this is perceived as obvious common knowledge, but human memory can be fleeting.

## How do I actually run a modded game?
Forget about Morrowind Launcher. Use a mod organizer, such as [Wrye Mash](https://www.nexusmods.com/morrowind/mods/45439). It includes the most important shortcuts, allows to reorder .esp plugins load order and fix various issues.

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

## I get low FPS in cities (i.e. Vivec exteriors)
Install [Morrowind Code Patch](https://www.nexusmods.com/morrowind/mods/19510), [Morrowind Optimization Patch](https://www.nexusmods.com/morrowind/mods/45384) and [Project Atlas](https://www.nexusmods.com/morrowind/mods/45399)

In MGE XE settings, disable Dynamic ripples and some water reflections. Decrease Draw Distance. Regenerate Distant Land with lower settings. Disable Grass.

In MGE XE settings, go to In-Game tab and click on Macro Editor. You can add a hotkey here for toggling distant land and shaders (i.e. `-` and `*` on numberical keyboard). Then when you're in a taxing location just press these keys to disable distant land and shaders, it should restore up to 10 fps.  
![image](https://github.com/the-overdriven/morrowind-issues-and-fixes/assets/100090726/7c588307-33d5-4999-aea8-cc0fb3f53604)

You can also try to run the shortcut to Morrowind with `/High` priority but from my experience it doesn't change much.

## How to fix errors "One of the files that "(mod name).ESP" is dependent on has changed since the last save."
Install [Wrye Mash](https://www.nexusmods.com/morrowind/mods/45439?tab=docs). Follow [this guide](https://danaeplays.thenet.sk/wrye-mash/).  
TL;DR: for me selecting the problematic esp in the Mods tab and right-clicking on its masters on right side to update them fixes it. Moving the esp in the modlist helps too.

## I would like to know what is my current modlist
Install [Mod List](https://www.nexusmods.com/morrowind/mods/50214), find the mod in the Mod Config list and click on it. Copy+paste to any text editor.

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
  <summary>My custom GMST variables corresponding to walk/run speed</summary>

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

## Fights are too quick and chaotic 
Install [Time Shift](https://www.nexusmods.com/morrowind/mods/49646), in its main.lua comment out the line:  
```
-- mp.fatigue.current = mp.fatigue.current - dt * cf.sc
```
Set the time scaling value to 45, it seems to be most optimal for combat, as lower values might make animations too slow.

## How to cast spells on key press, to not switch between weapon and magic all the time?
Install [Morrowind Code Patch](https://www.nexusmods.com/morrowind/mods/19510), run it, check "Swift Casting" and apply  
![image](https://github.com/the-overdriven/morrowind-issues-and-fixes/assets/100090726/5fc22441-abae-4a39-be5d-c6616f665cd8)

## How do I use Quick Keys in Morrowind?
Press F1

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

## I want to adjust the camera with a mouse scroll, just like in OpenMW
Install [Zoom](https://www.nexusmods.com/morrowind/mods/53474)  
Compatibility patch for Zoom and QuickLoot: [patch](https://github.com/the-overdriven/morrowind-zoom-and-quickloot-compatibility)  
It's even better than in OpenMW, because it allows zooming in also in first-person view. For even better camera experience install [Steadicam](https://www.nexusmods.com/morrowind/mods/52225). But personally I don't find the default settings too playable and recommend only a slight first-person steadicam, to disable it in third-person set third-person values to lowest possible.

## Very few dialogues are voiced
Install AI-generated [Kezyma's Voices of Vvardenfell](https://www.nexusmods.com/morrowind/mods/52279)  
Other, AI-generated voices:  
[Ashlander Voices](https://www.nexusmods.com/morrowind/mods/53863)  
[Vivec](https://www.nexusmods.com/morrowind/mods/52333)  
[Yagrum Bagarn](https://www.nexusmods.com/morrowind/mods/52344)  
[Davyth Fyr](https://www.nexusmods.com/morrowind/mods/52343)  
[The Wisest Women](https://www.nexusmods.com/morrowind/mods/52353)  
[Nordic Banter](https://www.nexusmods.com/morrowind/mods/53715)  
[Friends Reunited](https://www.nexusmods.com/morrowind/mods/53601)  
[Quest Voice Greetings](https://www.nexusmods.com/morrowind/mods/52273)  
[Great Service](https://www.nexusmods.com/morrowind/mods/47767)  
[Idle Talk](https://www.nexusmods.com/morrowind/mods/46948)  
[Its a Deal](https://www.nexusmods.com/morrowind/mods/47968)  

## Dialogues with NPCs are too repeatable
Install [UI Expansion](https://www.nexusmods.com/morrowind/mods/46071) and [Dialogues Decluttered](https://www.nexusmods.com/morrowind/mods/48301)

## City guards and faction members are not helping me when I'm being attacked
Install [More Attentive Guards](https://www.nexusmods.com/morrowind/mods/48622)
Caution, has a bug: "Every time I attack in self defense, I get reported and attacked"

## There is no hotkey for Quests
After installing [Hot Quests](https://www.nexusmods.com/morrowind/mods/48976) the hotkey is "U"

## Can I make Quests screen more usable (i.e. bigger)?
Yes. With [Smart Journal](https://www.nexusmods.com/morrowind/mods/47492):  
![image](https://github.com/the-overdriven/morrowind-issues-and-fixes/assets/100090726/3a18f6a4-1676-4e76-9bcd-c908e3b167be)

## Can I write in my journal?
Yes, with [Journal Search and Edit](https://www.nexusmods.com/morrowind/mods/46756)

## Different potions in inventory are not easy to tell apart
Install [Colored Potions](https://www.nexusmods.com/morrowind/mods/48999)

## All merchants are broke
Install [More Barter Gold](https://www.nexusmods.com/morrowind/mods/40053) and [Merchant Gold Resets Instantly](https://www.nexusmods.com/morrowind/mods/43764)

## Is there a way to stop friendly-fire?
Yes, install [No More Friendly Fire](https://www.nexusmods.com/morrowind/mods/48801)
