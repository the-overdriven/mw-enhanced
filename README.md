# Morrowind issues and how to fix them
Morrowind is a great game, but can be made even greater (and less clunky) by customizing it with the 20+ years of its wonderous modding heritage. While some of these solutions might work on OpenMW these docs focus exclusively on Morrowind.exe and modern Windows systems. Most of this is perceived as obvious common knowledge, but human memory can be fleeting.

What these docs are not:
- not a guide you have to read from cover to cover, you can solve each issue separately, in any order  
- not a modlist, it expands from the context of specific issues and sometimes a possible solution is installing a mod, but not always  
- doesn't cover all QoL mods, as those less essential, that are nice-to-have will be listed in a separate modlist repository  
- doesn't mention any shaders and mesh/texture replacers for purely aesthethic experience, there will be a separate repository for that
- doesn't mention any content and overhaul mods

Think of it rather as "Morrowind power user FAQ"

## How do I actually run a modded game?
Forget about Morrowind Launcher. Use a mod organizer, such as [Wrye Mash](https://www.nexusmods.com/morrowind/mods/45439). It includes the most important shortcuts, allows to reorder .esp plugins load order and fix various issues.

## Alt+Tab doesn't work or is clunky
1. Install [MGE XE](https://www.nexusmods.com/morrowind/mods/41102)
2. Open MGE XE settings (MGEXEgui.exe in main game folder)
3. Check "Windowed mode" and "Borderless window" in MGE XE settings:
![image](https://github.com/the-overdriven/morrowind-issues-and-fixes/assets/100090726/5e8f8763-8f46-4b04-bda4-b56161d81953)

## But I want to play in lower resolution and fullscreen
<details>
  <summary>(click to expand)</summary>
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
</details>

## On multiple screens setup, moving mouse in game moves cursor on the second screen
Install [FullscreenLock](https://github.com/blaberry/FullscreenLock) and run it every time you run the game (the script above runs it automatically). The .exe file can be downloaded from the [Releases](https://github.com/blaberry/FullscreenLock/releases/tag/1.1) page. [Mirror](https://github.com/the-overdriven/FullscreenLock/releases/tag/1.1).

## Game hangs when closing it
Install [Expeditious Exit](https://www.nexusmods.com/morrowind/mods/45634)

## Everything in game is too small. Fonts, UI, etc.
Open MGE XE settings and adjust the Menu UI scaling to your liking. Depending on game's resolution I find 1.20 - 1.50 values most optimal.

## I get low FPS in cities (i.e. Vivec exteriors)
<details>
  <summary>(click to expand)</summary>

Install [Morrowind Code Patch](https://www.nexusmods.com/morrowind/mods/19510), [Morrowind Optimization Patch](https://www.nexusmods.com/morrowind/mods/45384) and [Project Atlas](https://www.nexusmods.com/morrowind/mods/45399)

In MGE XE settings, disable Dynamic ripples and some water reflections. Decrease Draw Distance. Regenerate Distant Land with lower settings. Disable Grass.

In MGE XE settings, go to In-Game tab and click on Macro Editor. You can add a hotkey here for toggling distant land and shaders (i.e. `-` and `*` on numberical keyboard). Then when you're in a taxing location just press these keys to disable distant land and shaders, it should restore up to 10 fps.  
![image](https://github.com/the-overdriven/morrowind-issues-and-fixes/assets/100090726/7c588307-33d5-4999-aea8-cc0fb3f53604)

You can also try to run the shortcut to Morrowind with `/High` priority but from my experience it doesn't change much.  

Might want to install [Memory Monitor](https://www.nexusmods.com/morrowind/mods/45696) to keep track of performance improvements.

Optional: [Ocean Light Remover](https://www.nexusmods.com/morrowind/mods/53847)
</details>

## I see jagged flickering lines at night
Turn OFF anti-aliasing in MGE XE settings.

## How to fix frequent "Initializing data" screens when changing exterior cells? (OpenMW only)
Recreate navigation mesh cache. It's under Data Files tab.

## How to fix incorrect map?
Wrye Mash has the utility to reset save state map.

## How to fix errors "One of the files that "(mod name).ESP" is dependent on has changed since the last save."
Install [Wrye Mash](https://www.nexusmods.com/morrowind/mods/45439?tab=docs). Follow [this guide](https://danaeplays.thenet.sk/wrye-mash/).  
TL;DR: for me selecting the problematic esp in the Mods tab and right-clicking on its masters on right side to update them fixes it. Moving the esp in the modlist helps too.

## I would like to know what is my current modlist
Install [Mod List](https://www.nexusmods.com/morrowind/mods/50214), find the mod in the Mod Config list and click on it. Copy+paste to any text editor.

## The game is too dark
Install [Gamma](https://www.nexusmods.com/morrowind/mods/53829). Don't forget to add 📄 Gamma.fx to MGE XE shaders and activate it.  
Then in Mod Config menu find Gamma and decrease Gamma or increase Luminance. You can increase color saturation as well.

## It's still too dark at night
If we adjust the luminance to be sufficiently bright in dark caves then it might turn out that we overdid it and now it's too bright outside.  
Can't make it perfect, can we? Actually we can if we take the current cell and daytime into account. This [fork of Gamma](https://github.com/the-overdriven/morrowind-bright-nights-and-caves/blob/main/main.lua) will decrease luminance in exteriors during the day and increase luminance in interiors, or when it is night time.

## How to fix seams on land textures?
Install [Texture Fix 2.0](https://www.nexusmods.com/morrowind/mods/53593) and [Texture Fix - Extended](https://www.nexusmods.com/morrowind/mods/46018)

## How to hide HUD?
It's `tm` command in console, but it's a bit clunky to deactivate.
Better solution might be to use [HUD Hider](https://www.nexusmods.com/morrowind/mods/46642) which adds a toggable hotkey.

## I move like in slow motion, I want to run faster

<details>
  <summary>(click to expand)</summary>

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
</details>

## I use up all my fatigue for moving around, so I have none left for fighting

<details>
  <summary>(click to expand)</summary>
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
</details>

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

## Are there hotkeys to save and load?
F5 to save, F9 to load

## When quick-saving will it save on multiple slots?
No. You'd have install [Sophisticated Save System](https://www.nexusmods.com/morrowind/mods/45608) for that. It adds autosave as well (including save every x minutes)

## Being able to chug multiple potions at the same time is too OP
Install [Controlled Consumption](https://www.nexusmods.com/morrowind/mods/45624)

## Killed enemies respawn like in some kind of MMO
Install [No Respawns](https://www.nexusmods.com/morrowind/mods/53853)

## Difficulty (some enemies) scale with level, I want more challenges early game
Install [OperatorJack's Deleveler](https://www.nexusmods.com/morrowind/mods/47897)

## Looting is clunky, too much clicking
Install [QuickLoot](https://www.nexusmods.com/morrowind/mods/46283). Recommended to use with [Morrowind Containers Animated - Edited for Quickloot](https://www.nexusmods.com/morrowind/mods/49297).

## Outside of cities, everything that moves wants to kill me
Install [Non-Homicidal Ecosystem](https://www.nexusmods.com/morrowind/mods/42327)  
Could be even better if these attacks were based on player's level or health (weak monsters should be afraid to attack strong player)

## I'm lost in Vivec, every canton looks the same
Install [Colorful Vivec](https://www.nexusmods.com/morrowind/mods/53806)

## How can I toggle the map mode?
Install [UI Expansion](https://www.nexusmods.com/morrowind/mods/46071), the hotkey is configurable in the mod settings. There is also a possibility to automatically change map mode on cell change.

## I'm pestered by dark assassins from Tribunal content early game
Install [Tribunal Delayed](https://www.nexusmods.com/morrowind/mods/33973/)

## I'm encumbered all the time
Install [Encumberance increaser](https://www.nexusmods.com/morrowind/mods/28213)

## I want to have a stash for items but can't put much in containers
Install [ContainerWeightMaxed](https://www.nexusmods.com/morrowind/mods/45698)  
~~Even if using QuickLoot, [inom - Inventory mouse wheel](https://www.nexusmods.com/morrowind/mods/46847) might still be helpful here for moving items from/to container quicker.~~  
Actually, UI Expansion has an option to move items from/to container on left click.

## I want to adjust the camera with a mouse scroll, just like in OpenMW
Install [Zoom](https://www.nexusmods.com/morrowind/mods/53474)  
Compatibility patch for Zoom and QuickLoot: [patch](https://github.com/the-overdriven/morrowind-zoom-and-quickloot-compatibility)  
It's even better than in OpenMW, because it allows zooming in also in first-person view. For even better camera experience install [Steadicam](https://www.nexusmods.com/morrowind/mods/52225). But personally I don't find the default settings too playable and recommend only a slight first-person steadicam, to disable it in third-person set third-person values to lowest possible.  
Despite the visual improvements it brings, Steadicam does cause some issues. One is that it smooth camera makes aiming enemies harder, it can be mitigated by adding to the beginning of steadicam function:
```
if tes3.player.mobile.inCombat then
  return
end
```
Other issue is that it makes targeting small items harder. An easy fix is too turn off the smooth camera on zoom:
```
if mge.camera.zoom > 3 then
  return
end
```

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

## City guards and faction members are not helping me when I'm attacked
Install [More Attentive Guards](https://www.nexusmods.com/morrowind/mods/48622)
Caution, has a bug: "Every time I attack in self defense, I get reported and attacked"

## There is no hotkey for Quests
After installing [Hot Quests](https://www.nexusmods.com/morrowind/mods/48976) the hotkey is "U"

## Can I make Quests screen more usable (i.e. bigger)?
Yes. With [Smart Journal](https://www.nexusmods.com/morrowind/mods/47492):  
![image](https://github.com/the-overdriven/morrowind-issues-and-fixes/assets/100090726/3a18f6a4-1676-4e76-9bcd-c908e3b167be)

Highlighting and hiding quests is doable with [Better Questlist](https://www.nexusmods.com/morrowind/mods/48272)

## Can I write in my journal?
Yes, with [Journal Search and Edit](https://www.nexusmods.com/morrowind/mods/46756)

## Different potions in inventory are not easy to tell apart
Install [Colored Potions](https://www.nexusmods.com/morrowind/mods/48999)

## All merchants are broke
Install [More Barter Gold](https://www.nexusmods.com/morrowind/mods/40053) and [Merchant Gold Resets Instantly](https://www.nexusmods.com/morrowind/mods/43764)

## How can I see HP values of enemies?
With [Seph's Enemy Bars](https://www.nexusmods.com/morrowind/mods/50577). There is one problem with this mod, though. It hides the default yellow bar and the new one is not displayed when attacking enemies from distance. In order to at least restore the vanilla yellow bar in bottom left corner edit this mod's main.lua file and remove or comment out following lines:
```
-- if npcHealthBar then
		-- 	-- Just yeet that yellow bar somewhere so it never shows its ugly face again.
		-- 	npcHealthBar.absolutePosAlignX = 10.0
		-- 	npcHealthBar.absolutePosAlignY = 10.0
		-- 	npcHealthBar.visible = false
		-- 	npcHealthBar.disabled = true
		-- end
```

## Is there a way to stop friendly-fire?
Yes, install [No More Friendly Fire](https://www.nexusmods.com/morrowind/mods/48801)

## How to tell if I've already read a given book? Also: books are increasing full skill points, which incentives postponing the bonus. And not sure which book actually gives the bonus.
If reading a book bumps a skill to next round integer value then it would pay off better to read them when our skills are high enough and expensive to train. And also ideally when have just advanced recently. A more fair solution would be to make books increase xp of skill, rather than bump the skill to the next round value. Then it wouldn't matter when we receive the bonus.  
Luckily [Reading is Good](https://www.nexusmods.com/morrowind/mods/51705) and [Book Worm](https://www.nexusmods.com/morrowind/mods/46851) should fix that.  
Additionally, [Skill Name Skill Books](https://www.nexusmods.com/morrowind/mods/51510) will show which skill does a given book increase.

## Is there an easier way to drop items?
[Caps Click to Drop](https://www.nexusmods.com/morrowind/mods/52518) and [Just Drop It](https://www.nexusmods.com/morrowind/mods/49557) for better dropping experience (corpses fall according to the terrain!)

## How to fix silent death sounds?
Install [Deathrattle Sounds](https://www.nexusmods.com/morrowind/mods/53938), it fixes NPCs blabbering after death as well.
Recommended together with [Small Quality of Life Improvements - MWSE](https://www.nexusmods.com/morrowind/mods/53905), which includes a component preventing repeating same voice-over repeatedly.

## How to disable vanity camera? (the one that turns on after 30 seconds) 
Install [No Auto Vanity Camera](https://www.nexusmods.com/morrowind/mods/48933)

## Game doesn't notify me explicitly enough that I started or finished a quest.
Install [Skyrim Style Quest Notifications](https://www.nexusmods.com/morrowind/mods/53175) and [Skyrim Style Quest Notifications - Legendary Edition](https://www.nexusmods.com/morrowind/mods/53712)

## Where is the medium armor trainer?
There is none, Bethesda forgot to add it. Install [Cinia](https://www.nexusmods.com/morrowind/mods/47153)

## I can sleep in owned beds, doesn't make much sense
Arguably it does make sense (especially if the house is abandoned), but if you like to limit yourself: install [Bed Buddies](https://www.nexusmods.com/morrowind/mods/46632). 

## Magicka (mana) doesn't regenerate
Most advanced and configurable mod for this appears to be [Magicka Regeneration Suite](https://www.nexusmods.com/morrowind/mods/49153)

## How to see how much longer a spell will last?
Install [Effect Timers](https://www.nexusmods.com/morrowind/mods/51787) or [Buff Bars](https://www.nexusmods.com/morrowind/mods/51924). Arguably Buff Bars are better, as they cover more spells, but they don't show time values.

## How to disable the cheesy shiny glow?
Install [Assetless No Glow](https://www.nexusmods.com/morrowind/mods/47925)

## How to install animations (i.e. xbase_anim.1st.kf)?
Copy to Meshes. Some require [LizTail Animation Kit](https://www.nexusmods.com/morrowind/mods/43606/)

## How to show 1-st person swimming annimation?
Install [MCAR](https://www.nexusmods.com/morrowind/mods/48628)

## How to change screenshot path when using ReShade?
When in game, press Home and look for the path in Settings

## How to view meshes with textures?
Install [NifSkope 2.0 Dev 7](https://github.com/niftools/nifskope/releases). Set path to Morrowind Data Files in Options: Options > Settings > Resources > Add Folder.  
From my experience version Dev 9 doesn't load textures.
