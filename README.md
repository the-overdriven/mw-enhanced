# Morrowind issues and how to fix them
Morrowind is a great game, but can be made even greater (and less clunky) by customizing it with the 20+ years of its wonderous modding heritage. While some of these solutions might work on OpenMW these docs focus exclusively on Morrowind.exe and modern Windows systems. Most of this is perceived as obvious common knowledge, but human memory can be fleeting.

What these docs are not:
- not a guide you have to read from cover to cover, you can solve each issue separately, in any order  
- not a modlist, it expands from the context of specific issues and sometimes a possible solution is installing a mod, but not always  
- doesn't cover all QoL mods, as those less essential, that are nice-to-have will be listed in a separate modlist repository  
- doesn't mention any shaders and mesh/texture replacers for purely aesthethic experience, there will be a separate repository for that
- doesn't mention any content and overhaul mods

Think of it rather as "Morrowind power user FAQ"

## How to get the best bug-free experience?
Install [Patch for Purists](https://www.nexusmods.com/morrowind/mods/45096)

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

## I get low FPS (i.e. in cities, Vivec exteriors)
<details>
  <summary>(click to expand)</summary>

Morrowind, as many old games, is a CPU hog. Doesn't make use of multithreading and GPU. Not much can be done about it.

Install [Morrowind Code Patch](https://www.nexusmods.com/morrowind/mods/19510), [Morrowind Optimization Patch](https://www.nexusmods.com/morrowind/mods/45384) and [Project Atlas](https://www.nexusmods.com/morrowind/mods/45399)

In MGE XE settings, disable Dynamic ripples and some water reflections. Decrease Draw Distance. Regenerate Distant Land with lower settings. Disable Grass.

In MGE XE settings, go to In-Game tab and click on Macro Editor. You can add a hotkey here for toggling distant land and shaders (i.e. `-` and `*` on numberical keyboard). Then when you're in a taxing location just press these keys to disable distant land and shaders, it should restore up to 10 fps.  
![image](https://github.com/the-overdriven/morrowind-issues-and-fixes/assets/100090726/7c588307-33d5-4999-aea8-cc0fb3f53604)

You can also try to run the shortcut to Morrowind with `/High` priority but from my experience it doesn't change much.  

Decreasing view distance does make a big difference but comes at a price of causing a Fata Morgana effect (objects disappear or change when coming closer).

[Memory Monitor](https://www.nexusmods.com/morrowind/mods/45696) can be used to keep track of performance improvements.

Optional: 
- [Ocean Light Remover](https://www.nexusmods.com/morrowind/mods/53847)
- [Turn Normal Grass and Kelp into Groundcover](https://www.nexusmods.com/morrowind/mods/52010)
- [I Lava Good Mesh Replacer](https://www.nexusmods.com/morrowind/mods/49605)
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

## How to fix seams on models?
[Correct Meshes](https://www.nexusmods.com/morrowind/mods/39348)

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

<details>
  <summary>(click to expand)</summary>

Install [Time Shift](https://www.nexusmods.com/morrowind/mods/49646), in its main.lua comment out the line:  
```
-- mp.fatigue.current = mp.fatigue.current - dt * cf.sc
```
Set the time scaling value to 45, it seems to be most optimal for combat, as lower values might make animations too slow.
</details>

## How to cast spells on key press, to not switch between weapon and magic all the time?

<details>
  <summary>(click to expand)</summary>

Install [Morrowind Code Patch](https://www.nexusmods.com/morrowind/mods/19510), run it, check "Swift Casting" and apply  
![image](https://github.com/the-overdriven/morrowind-issues-and-fixes/assets/100090726/5fc22441-abae-4a39-be5d-c6616f665cd8)

</details>

## How do I use Quick Keys in Morrowind?
Press F1. You can install [Quickkeys Hotbar](https://www.nexusmods.com/morrowind/mods/51192) to see all your hotkeys in the HUD.

## Are there hotkeys to save and load?
F5 to save, F9 to load

## When quick-saving will it save on multiple slots?
No. You'd have install [Sophisticated Save System](https://www.nexusmods.com/morrowind/mods/45608) for that. It adds autosave as well (including save every x minutes)

## Being able to chug multiple potions at the same time is too OP. Alchemy is too OP, in general.
Install [Controlled Consumption](https://www.nexusmods.com/morrowind/mods/45624) or [Alchemical Hustle](https://www.nexusmods.com/morrowind/mods/51050)

## Killed enemies respawn like in some kind of MMO
Install [No Respawns](https://www.nexusmods.com/morrowind/mods/53853)

## Difficulty (some enemies) scale with level, I want more challenges early game
Install [OperatorJack's Deleveler](https://www.nexusmods.com/morrowind/mods/47897)  

## Looting is clunky, too much clicking
Install [QuickLoot](https://www.nexusmods.com/morrowind/mods/46283). Recommended to use with [Morrowind Containers Animated - Edited for Quickloot](https://www.nexusmods.com/morrowind/mods/49297).

## Pickpocketing is useless
Install [Pickpocket](https://www.nexusmods.com/morrowind/mods/47581)

## Sneaking is useless
Install [Stealth Improved](https://www.nexusmods.com/morrowind/mods/49614)

## When leveling, HP gain is not retroactive, which incentivizes focusing on Endurance early game. Excess progress and multiplier bonus are also sometimes wasted.
Install [Improved Vanilla Leveling](https://www.nexusmods.com/morrowind/mods/48065) (fixes retroactive health, multipliers and how XP carry-over contributes to attributes)  
XP carry-over fix (unrelated to attribute gain): [Experience Carryover](https://www.nexusmods.com/morrowind/mods/53972)  
Also: [Quest Skill Reward Fix](https://www.nexusmods.com/morrowind/mods/48269) - applies skill rewards from quests more optimally.

## Progresion is too quick/easy
Install [Proportional Progression](https://www.nexusmods.com/morrowind/mods/45697) or [Proportional Progression Expanded](https://www.nexusmods.com/morrowind/mods/53782)  
TODO

## It is too easy to get rich
TODO

## There are too many (low tier) items in game
TODO

## Outside of cities, everything that moves wants to kill me
Install [Non-Homicidal Ecosystem](https://www.nexusmods.com/morrowind/mods/42327)  
Could be even better if these attacks were based on player's level or health (weak monsters should be afraid to attack strong player)

## I'm lost in Vivec, every canton looks the same
Install [Colorful Vivec](https://www.nexusmods.com/morrowind/mods/53806) and [Vivec Cantons Reconnected](https://www.nexusmods.com/morrowind/mods/48081)

## How can I toggle the map mode?

<details>
  <summary>(click to expand)</summary>
	
Install [UI Expansion](https://www.nexusmods.com/morrowind/mods/46071), the hotkey is configurable in the mod settings. There is also a possibility to automatically change map mode on cell change.  
There is one small bug with the map mode toggle hotkey, though. It stops working after opening and closing the inventory, but can be fixed. Find `local function onKeyInput()` in `MenuMap.lua` and change:
```
 if (not common.isTextInputActive() and common.complexKeybindTest(common.config.keybindMapSwitch)) then
```
to
```
 if (common.complexKeybindTest(common.config.keybindMapSwitch)) then
```
It comes with a catch: the hotkey should not type anything (i.e. F3), otherwise you might change your map mode when typing in the inventory filters.
</details>

## I'm pestered by dark assassins from Tribunal content early game
Install [Tribunal Delayed](https://www.nexusmods.com/morrowind/mods/33973/) or [Expansion Delay](https://www.nexusmods.com/morrowind/mods/47588)

## I'm encumbered all the time
Install [Encumberance increaser](https://www.nexusmods.com/morrowind/mods/28213)

## I want to have a stash for items but can't put much in containers
Install [ContainerWeightMaxed](https://www.nexusmods.com/morrowind/mods/45698)  
~~Even if using QuickLoot, [inom - Inventory mouse wheel](https://www.nexusmods.com/morrowind/mods/46847) might still be helpful here for moving items from/to container quicker.~~  
Actually, UI Expansion has an option to move items from/to container on left click.

## I want to adjust the camera with a mouse scroll, just like in OpenMW
<details>
  <summary>(click to expand)</summary>

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
</details>

## Very few dialogues are voiced

<details>
  <summary>(click to expand)</summary>

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
</details>

## Dialogues with NPCs are too repeatable
Install [UI Expansion](https://www.nexusmods.com/morrowind/mods/46071) and [Dialogues Decluttered](https://www.nexusmods.com/morrowind/mods/48301)

## How to break from endless dialogue choices loop?
Install [Force Close Dialogue Menu](https://www.nexusmods.com/morrowind/mods/52553)

## Passing by NPCs makes them too reactive
Install [Shut Up](https://www.nexusmods.com/morrowind/mods/43310), NPCs will notice you only when you look at them.

## Companions, city guards and faction members are not helping me when I'm attacked
Install [More Attentive Guards](https://www.nexusmods.com/morrowind/mods/48622). Caution, has a bug: "Every time I attack in self defense, I get reported and attacked"

For companions: install [Diligent Defenders](https://www.nexusmods.com/morrowind/mods/45717)  

How to tell my followers (companions and summons) who to attack? You can do on hotkey when you install [Kill Command](https://www.nexusmods.com/morrowind/mods/46723)

How to see my followers' stats? Install [More Detailed Companion HealthBars MWSE Lua Script](https://www.nexusmods.com/morrowind/mods/51389)

## Companions get lost occasionally
Install [Easy Escort](https://www.nexusmods.com/morrowind/mods/45712)

## There is no hotkey for Quests
After installing [Hot Quests](https://www.nexusmods.com/morrowind/mods/48976) the hotkey is "U"

## Can I make Quests screen more usable (i.e. bigger)?

<details>
  <summary>(click to expand)</summary>
	
Yes. With [Smart Journal](https://www.nexusmods.com/morrowind/mods/47492):  
![image](https://github.com/the-overdriven/morrowind-issues-and-fixes/assets/100090726/3a18f6a4-1676-4e76-9bcd-c908e3b167be)

Highlighting and hiding quests is doable with [Better Questlist](https://www.nexusmods.com/morrowind/mods/48272)
</details>

## Can I write in my journal?
Yes, with [Journal Search and Edit](https://www.nexusmods.com/morrowind/mods/46756)

## Different potions in inventory are not easy to tell apart
Install [Colored Potions](https://www.nexusmods.com/morrowind/mods/48999)

## All merchants are broke
Install [More Barter Gold](https://www.nexusmods.com/morrowind/mods/40053) and [Merchant Gold Resets Instantly](https://www.nexusmods.com/morrowind/mods/43764)

## Race and birthsign spells are ~~cringe~~ useless and unbalanced
Install [Balanced Passive Races and Birthsigns](https://www.nexusmods.com/morrowind/mods/47782), it will replace spells (that no one uses anyway) with permanent bonuses.

## Using shrines is clunky
[Shrine Tooltips](https://www.nexusmods.com/morrowind/mods/48275) adds tooltips that tells you what each option actually does. [No Thank You](https://www.nexusmods.com/morrowind/mods/49681) adds a cancel option.

## Movement when swimming and levitating is clunky
Install [Better Buoyancy](https://www.nexusmods.com/morrowind/mods/48929), adds jump key to float upwards, and the sneak key to sink downwards.

## How can I see HP values of enemies?

<details>
  <summary>(click to expand)</summary>
	
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
</details>

## Is there a way to stop friendly-fire?
Yes, install [No More Friendly Fire](https://www.nexusmods.com/morrowind/mods/48801)

## How to tell if I've already read a given book? Also: books are increasing full skill points, which incentives postponing the bonus. And not sure which book actually gives the bonus.
If reading a book bumps a skill to next round integer value then it would pay off better to read them when our skills are high enough and expensive to train. And also ideally when have just advanced recently. A more fair solution would be to make books increase xp of skill, rather than bump the skill to the next round value. Then it wouldn't matter when we receive the bonus.  
Luckily [Reading is Good](https://www.nexusmods.com/morrowind/mods/51705) and [Book Worm](https://www.nexusmods.com/morrowind/mods/46851) should fix that.  
Additionally, [Skill Name Skill Books](https://www.nexusmods.com/morrowind/mods/51510) will show which skill does a given book increase.

## Is there an easier way to drop items?
[Caps Click to Drop](https://www.nexusmods.com/morrowind/mods/52518) and [Just Drop It](https://www.nexusmods.com/morrowind/mods/49557) for better dropping experience (corpses fall according to the terrain!)

## How to fix silent NPC groans?
Some mods break it (Character Sound Overhaul and Impact Sounds - I'm looking at you). Install [Deathrattle Sounds](https://www.nexusmods.com/morrowind/mods/53938), it doesn't restore groans on hit, but it does restore groans on death. And adds some extra. It fixes NPCs blabbering after death as well.  
Recommended together with [Small Quality of Life Improvements - MWSE](https://www.nexusmods.com/morrowind/mods/53905), which includes a component preventing repeating same combat voice-overs repeatedly.

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

## How to remove learned spells?
Install [Spellscribe](https://www.nexusmods.com/morrowind/mods/52809). Use paper on yourself to scribe the spell for backup. Remove the spell with Shift+Click.

## Why do I have to read a blank piece of paper before I pick it up?
Install [Plain Paper Fix](https://www.nexusmods.com/morrowind/mods/47735)

## How to disable the cheesy shiny glow?
Install [Assetless No Glow](https://www.nexusmods.com/morrowind/mods/47925)  
To change glass weapons and armor: [Dim Glass - Less Irritating Glass Armor and Weapon](https://www.nexusmods.com/morrowind/mods/51544)

## How to change the cheesy shiny background behind magical items in invetory?
Install [Seph's Inventory Decorators](https://www.nexusmods.com/morrowind/mods/50582)

## How to install animations (i.e. xbase_anim.1st.kf)?
Copy to Meshes. Some require [LizTail Animation Kit](https://www.nexusmods.com/morrowind/mods/43606/)

## How to show 1-st person swimming annimation?
Install [MCAR](https://www.nexusmods.com/morrowind/mods/48628)

## How to track mod updates on Nexus?

<details>
  <summary>(click to expand)</summary>

Go to [Tracking Centre](https://www.nexusmods.com/mods/trackingcentre). The problem with this view is that it's not very useful. In the tracking centre we are only interested in mods that we already downloaded but in the meantime they got an update. Unfortunately, Nexus doesn't provide a filter for mods you haven't downloaded yet. And, most importantly, you cannot filter out mods that didn't have new updates since last time you've downloaded them.

Here comes the power of CSS and JS magic.

The first time you open the page, open the console with F12 and run the following code:

```
function filterMods() {
	document.querySelectorAll('.mod-tracking-table tbody tr').forEach(function(tr) {
		const tdDownloaded = tr.querySelector('td.table-download');
		const tdUpdated = tr.querySelector('td.table-update');
		const updatedDateGreaterThanDownloadedDate = new Date(tdUpdated.innerHTML).getTime() > new Date(tdDownloaded.innerHTML).getTime();

		if (tdDownloaded.innerHTML.includes('--') || !updatedDateGreaterThanDownloadedDate) {
			tdDownloaded.innerHTML = '';
			// tr.remove(); // uncomment this, if you don't want to use Stylus/CSS
		}
	})
}


(function() {
    filterMods()
    var origOpen = XMLHttpRequest.prototype.open;
    XMLHttpRequest.prototype.open = function() {
        console.log('request started!');
        this.addEventListener('load', function() {
            console.log('request completed!');
            setTimeout(filterMods, 50)
        });
        origOpen.apply(this, arguments);
    };
})();
```

You can use [an addon](https://chromewebstore.google.com/detail/custom-javascript-for-web/ddbjnfjiigjmcpcpkmhogomapikjbjdk) to not have to copy-paste this code every single time.

Thanks to this JS code every time we change the page the "Last download" cell of mods that are of no interest to us here will be cleared. Now we can use the CSS to hide whole rows. Install [Stylus](https://chromewebstore.google.com/detail/stylus/clngdbkpkpeebahjckkjfobafhncgmne) and add a style for Nexus tracking centre page with following CSS code: `tr:has(.table-download:empty) { display:none }`. Once you save it filtering should start working. Of course, the same can be achieved with JS only, without using any CSS (albeit, JS-free, CSS-only solution is probably not possible in this case). Sometimes you do need both and processing CSS has a minimal performance impact, so it doesn't hurt to install Stylus, you might need it for a different issue, in the future.
</details>

## How to change screenshot path when using ReShade?
When in game, press Home and look for the path in Settings

## How to view meshes with textures?
Install [NifSkope 2.0 Dev 7](https://github.com/niftools/nifskope/releases). Set path to Morrowind Data Files in Options: Options > Settings > Resources > Add Folder.  
From my experience version Dev 9 doesn't load textures.
