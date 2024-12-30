# Morrowind issues and how to fix them

Morrowind stands as a masterpiece of gaming, its enduring legacy enriched by over two decades of remarkable modding innovation. While some of these enhancements may be compatible with OpenMW, the guidance provided here focuses exclusively on Morrowind.exe within the context of modern Windows systems. Much of what follows may be regarded as conventional wisdom among the community, yet the passage of time often renders even the obvious worth revisiting.

What these docs are not:
- not a guide you have to read from cover to cover, you can solve each issue separately, in any order  
- not a modlist, it expands from the context of specific issues and sometimes a possible solution is installing a mod, but not always  
- doesn't mention any shaders and mesh/texture replacers for purely aesthethic experience, there will be a separate repository for that
- doesn't mention any content and overhaul mods

Most importantly, it provides *options* in an effort to avoid being overly opinionated. Think of it rather as "Morrowind power user FAQ".

[Open](https://github.dev/the-overdriven/mw-enhanced/blob/main/README.md) this .md file in a side-by-side editor.

## How to get the best bug-free experience?
Install [Morrowind Code Patch](https://www.nexusmods.com/morrowind/mods/19510) and [Patch for Purists](https://www.nexusmods.com/morrowind/mods/45096)  
For official plugins: [Unofficial Morrowind Official Plugins Patched](https://www.nexusmods.com/morrowind/mods/43931) and [Bethesda Official Plugins Naturalized](https://www.nexusmods.com/morrowind/mods/51107)  
More: [Doors Anti Stuck](https://www.nexusmods.com/morrowind/mods/50931), [Improved Temple Experience](https://www.nexusmods.com/morrowind/mods/49373), [The Publicans](https://www.nexusmods.com/morrowind/mods/45410), [Under Construction](https://www.nexusmods.com/morrowind/mods/50285), [Creature VFX Restoration](https://www.nexusmods.com/morrowind/mods/46194), [Correct UV Mudcrabs](https://www.nexusmods.com/morrowind/mods/42130), [Better Scamps](https://www.nexusmods.com/morrowind/mods/48008), [Jammings Off](https://www.nexusmods.com/morrowind/mods/44523), [Dubdilla Location Fix](https://www.nexusmods.com/morrowind/mods/46720)

## How do I actually run a modded game?
Forget about Morrowind Launcher. Use a mod organizer, such as [Wrye Mash](https://www.nexusmods.com/morrowind/mods/45439). It includes the most important shortcuts, allows to reorder .esp plugins load order, solve conflicts and includes other tools that can fix various issues:
<details>
  <summary>(click to expand)</summary>
	
* tes3merge - produces the Morrowind equivalent of a bashed patch
* merged lands - can fix a lot of landscape issues from mods with minor landscape conflicts
* mlox - can give advice on mod load order, or sort it for you
* tes3cmd - a cleaning tool, very very useful but a bit more advanced and less immediately necessary for you

</details>

## Are there any other mod managers, more modern and robust than Wrye Mash?
[MO2](https://github.com/ModOrganizer2/modorganizer), Morrowind Mod Organizer  
Not recommended: Vortex, Wabbajack

## How to make a copy of the game from MO2 and run that copy from MO2?
To copy only the changed files (including files from MO's virtual file system) and run the copy of the game from MO2 (but detached from MO2):  
<details>
  <summary>(click to expand)</summary>
	
Add exectuable to Binary "C:\Windows\System32\cmd.exe" with Arguments:  
```batch
/c "cd /d "(game dir)" && xcopy .\* "(game dir copy)" /D /E /H /Y && cd /d "(game dir copy)" && start explorer.exe ""(link to Morrowind.exe in copied game dir)"" && exit"
```
This way clicking on "Run" copies (with xcopy) only the changed files from the virtual file system managed by MO2 (compared against copy of the game dir) and runs the copied game detached from MO2 (by running it with explorer), all in one command. Alternatively, one can run Morrowind.exe manually after copying of all the files is finished.

Why make a copy? Backup (in case something goes wrong with the game), performance (MO's VFS adds an additional layer), and control: you can see exactly which files have been added since the last mod installation, and having access to physical files allows to open the mods' assets and set physical paths to them in Nifskope/Blender. Some mods might also not work correctly when running the game via MO2.

</details>

## Any modern tools for solving mod conflicts?
[Conflict Viewer](https://www.nexusmods.com/morrowind/mods/54108), a successor of [TES3View/xEdit](https://www.nexusmods.com/morrowind/mods/54508)

## How to remove records from esp plugin (to i.e. make it compatible with other plugin)?
With [Tesame](https://www.nexusmods.com/morrowind/mods/50810)  

## Are there any tools for automated .esp plugin load ordering?
mlox, included in Wrye Mash.  
Alternative: [plox](https://www.nexusmods.com/morrowind/mods/54262) - a rust re-write of MLOX  
Alternative: [LOOT](https://loot.github.io/) - Load Order Optimisation Tool 

## Where can I find game logs?
Warnings.txt, MWSE.log and mgeXE.log

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
Install [FullscreenLock](https://github.com/blaberry/FullscreenLock) and run it every time you run the game (the script above runs it automatically). The .exe file can be downloaded from the [Releases](https://github.com/blaberry/FullscreenLock/releases/tag/1.1) page. [Mirror](https://github.com/the-overdriven/FullscreenLock/releases/tag/1.1). Alternative: Borderless Gaming.

If you use Lossless Scaling, it also has this feature, it's called "Cursor Lock".

## Game hangs when closing it
Install [Expeditious Exit](https://www.nexusmods.com/morrowind/mods/45634)

## Everything in game is too small. Fonts, UI, etc.
Open MGE XE settings and adjust the Menu UI scaling to your liking. Depending on game's resolution I find 1.20 - 1.50 values most optimal.

## Any way I can change the game's font?
TODO  
For now use [Beauty Font](https://www.nexusmods.com/morrowind/mods/49201)

## I get low FPS (i.e. in cities, Vivec exteriors)
<details>
  <summary>(click to expand)</summary>

Morrowind, as many old games, is a CPU hog. Doesn't make use of multithreading and GPU. Not much can be done about it.

Install [Morrowind Code Patch](https://www.nexusmods.com/morrowind/mods/19510), [Morrowind Optimization Patch](https://www.nexusmods.com/morrowind/mods/45384) and [Project Atlas](https://www.nexusmods.com/morrowind/mods/45399)

Grab [Vulkan's dll](https://www.nexusmods.com/morrowind/mods/53685), you can gain up to 10-15fps. If you use ReShade you might have to re-run the installation.  

In MGE XE settings, disable Dynamic ripples and some water reflections. Decrease Draw Distance. Regenerate Distant Land with lower settings. Disable Grass.

In MGE XE settings, go to In-Game tab and click on Macro Editor. You can add a hotkey here for toggling distant land and shaders (i.e. `-` and `*` on numberical keyboard). Then when you're in a taxing location just press these keys to disable distant land and shaders, it should restore few fps.  
![image](https://github.com/the-overdriven/morrowind-issues-and-fixes/assets/100090726/7c588307-33d5-4999-aea8-cc0fb3f53604)  
Decreasing view distance does make a big difference but comes at a price of causing mirages (objects disappear or change when coming closer).
There's a mod to automate it: [Simple FPS Optimizer](https://www.nexusmods.com/morrowind/mods/53982)  
You can set hotkeys in MGE XE Macro Editors for increasing and decreasing "View Range" as well.

[Lossless Scaling](https://store.steampowered.com/app/993090/Lossless_Scaling/) - provides frame generation, which enhances low frame rates by interpolating additional frames between existing ones, creating smoother motion. It leverages techniques like frame duplication or AI-driven interpolation to maintain responsiveness while improving the visual fluidity of gameplay.

You can also try to run the shortcut to Morrowind with `/High` priority but from my experience it doesn't change much.  

Morrowind.exe is also notorious for memory leaks. [Memory Monitor](https://www.nexusmods.com/morrowind/mods/45696) can be used to keep track of performance improvements (it will show a bar once the memory starts running out).

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

## The map is not very useful
Install [Map Icons - MWSE](https://www.nexusmods.com/morrowind/mods/53966).  
Nice to have: [Detect Map Icons](https://www.nexusmods.com/morrowind/mods/54285)

## How to fix errors "One of the files that "(mod name).ESP" is dependent on has changed since the last save."
Install [Wrye Mash](https://www.nexusmods.com/morrowind/mods/45439?tab=docs). Follow [this guide](https://danaeplays.thenet.sk/wrye-mash/).  
TL;DR: for me selecting the problematic esp in the Mods tab and right-clicking on its masters on right side to update them fixes it. Moving the esp in the modlist helps too.

## What does updating the master list actually do?
<details>
  <summary>(click to expand)</summary>
	
"In practice it only updates the master sizes in the mod header so the message does not appear any more, so yes, you could just ignore it and keep playing with the same result in practice. The big BUT is:
often times having different master sizes means also that master references changed, and in that case you could have broken references you should fix to the best of your ability (e.g. applying Mash updaters procedure). If you keep playing ignoring masters size change warnings you will never check for this kind of problems hence you could have usual references problems (doors/other objects disappearing/not changing when they should etc.)" - abot

</details>

## I would like to know what is my current modlist
Install [Mod List](https://www.nexusmods.com/morrowind/mods/50214), find the mod in the Mod Config list and click on it. Copy+paste to any text editor.  
Unfortunately, it doesn't list pluginless mods.

[Mod Organizer 2](https://github.com/ModOrganizer2/modorganizer) should have this feature: 
1. Right-click anywhere in the mod list (left pane).
1. Choose "Export to CSV" or "Export Mod List" (depending on your version of MO2).
1. Save the exported file in your preferred location.

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

## How can I customize my HUD?
Install [Seph's HUD Customizer](https://www.nexusmods.com/morrowind/mods/50588)

What it allows:

<details>
  <summary>(click to expand)</summary>
	
You can have numbers inside your health/magicka/fatigue bars.  
You can change the visibility, position, size and color of the health, magicka and fatigue bars.  
You can change the visibility, position and size of the enemy health bar.  
You can change the visibility and position of your equipped weapon and magic indicators.  
You can change the visibility and position of the message that occurs when you swap weapons or magic.  
You can change the visibility, position and layout of the currently active magic effect icons.  
You can change the visibility and position of the sneak indicator.  
You can change the visibility, position and size of the minimap.  
You can change the visibility and position of the message that occurs when you enter a new area/cell.  
You can change the visibility and position of the breath meter.  
You can change the visibility, position and layout of generic messages.  

</details>

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

## Movement is weird: you move backwards as fast as forwards and diagonal movement increases your speed
Install [Realistic Movement Speeds](https://www.nexusmods.com/morrowind/mods/46248) (for backwards movement)  
For diagonal movement: [IMMERSIVE RUN FIX](https://www.nexusmods.com/morrowind/mods/45947)

## [Balance] All my hits are missing
Dice-roll combat working as intended. But on a serious note, you can make the combat more dynamic by installing mods that make all swings have 100% chance to hit. I find [Better Balanced Combat](https://www.nexusmods.com/morrowind/mods/46596) to address this issue most tactfully, without breaking the balance too much, by taking side effects into consideration: i.e. fatigue is still important as the lower it is the higher is the chance to be knocked down, weapon skills also do not become meaningless but add a bonus to strength instead (which, rightfully, excludes the encumbrance bonus). Unfortunately, the mod also affects the regen rate, running speed and makes "You have failed casting the spell" popups disappear, which I'd personally prefer to leave as it is.

Alternative: [Next Generation Combat](https://www.nexusmods.com/morrowind/mods/46993)

## Fights are too quick and chaotic 

<details>
  <summary>(click to expand)</summary>

Install [Time Shift](https://www.nexusmods.com/morrowind/mods/49646), in its main.lua comment out the line:  
```
-- mp.fatigue.current = mp.fatigue.current - dt * cf.sc
```
Set the time scaling value to 45, it seems to be most optimal for combat, as lower values might make animations too slow.
</details>

## It's too easy to start new game by misclicking
Install [New Game Confirmation](https://www.nexusmods.com/morrowind/mods/47693)

## How to cast spells on key press, to not switch between weapon and magic all the time?

<details>
  <summary>(click to expand)</summary>

Install [Morrowind Code Patch](https://www.nexusmods.com/morrowind/mods/19510), run it, check "Swift Casting" and apply  
![image](https://github.com/the-overdriven/morrowind-issues-and-fixes/assets/100090726/5fc22441-abae-4a39-be5d-c6616f665cd8)

</details>

## Closing menus is tedious
Install [Right Click Menu Exit](https://www.nexusmods.com/morrowind/mods/48458)  
To close books and scrolls without closing the inventory, [Morrowind Code Patch](https://www.nexusmods.com/morrowind/mods/19510) has a fix called "Shortcut key improvements", which allows using space bar to close them.

## Any chargen mods to speed up or diversify character creation process?
[Quick Character Creation](https://www.nexusmods.com/morrowind/mods/50381) - same as in vanilla but with tedious parts skipped  
[Skip Tutorial (2009)](https://www.nexusmods.com/morrowind/mods/27266)  
[Chargen Revamped - Expanded Lands Complete - 2024](https://www.nexusmods.com/morrowind/mods/54646)  
[An Unexpected Start](https://www.nexusmods.com/morrowind/mods/53514)  
[Quick Char (Necro Edit)](https://www.nexusmods.com/morrowind/mods/47706)  
[Morrowind - The Roleplaying Mod (New Starts. Play as a Non Nerevarine. and others)](https://www.nexusmods.com/morrowind/mods/49389)  

## During chargen when selecting the race it's unclear what will be my starting attributes
Install [What Are My Attributes](https://www.nexusmods.com/morrowind/mods/49912)

## How do I use Quick Keys in Morrowind?
Press F1. You can install [QuickKeys Hotbar](https://www.nexusmods.com/morrowind/mods/51192) to see all your hotkeys in the HUD.  
For quicker hotkey assignment: [QuickKey Outlander - MWSE](https://www.nexusmods.com/morrowind/mods/50997)  
If you need more hotkeys: [Hotkeys Extended](https://www.nexusmods.com/morrowind/mods/48055)  
Many items on one hotkey: [Quick Loadouts](https://www.nexusmods.com/morrowind/mods/46708)

## Are there hotkeys to save and load?
F5 to save, F9 to load

## Will quick-saving save on multiple slots?
No. You'd have to install [Sophisticated Save System](https://www.nexusmods.com/morrowind/mods/45608) for that. It adds autosave as well (including automatic save every x minutes). Other auto save mod: [Simple Auto Save Modified](https://www.nexusmods.com/morrowind/mods/53794)

## The game doesn't show sheated weapons
Install [Weapon Sheating](https://www.nexusmods.com/morrowind/mods/46069)

## [Balance] Being able to chug multiple potions at the same time is too OP. Alchemy is too OP, in general.
Install [Controlled Consumption](https://www.nexusmods.com/morrowind/mods/45624) or [Alchemical Hustle](https://www.nexusmods.com/morrowind/mods/51050). Also [Better Balanced Booze](https://www.nexusmods.com/morrowind/mods/45844)

## Good alchemy mod? To enable filtering by effect, rather than by ingredient
~~[mwse Alchemy Filter](https://www.nexusmods.com/morrowind/mods/44808). The hotkey is right ctrl. After applying filter click on ingredients as you would normally and it will show only those that can cause the desired effect.~~  

More modern alternative: [Alchemical Knowledge](https://www.nexusmods.com/morrowind/mods/49036)  
Cooking multiple potions at once: [Alchemy Cauldron - Multiple Potions at Once - MWSE](https://www.nexusmods.com/morrowind/mods/51461)  
[Visible Alchemy Success Chance](https://www.nexusmods.com/morrowind/mods/48608)

## Traders don't want to trade with me, because I have illegal goods (i.e. skooma)
Install [Lore-friendly Trade Restrictions](https://www.nexusmods.com/morrowind/mods/50112) aka ketsTrade

## How to tell how much in the end a given potion or spell will restore points?
TODO

## After using a grass mod, I end up with mispositioned, clipping grass
Install [The LawnMower for Morrowind](https://www.nexusmods.com/morrowind/mods/53034)

## How to install grass mods (and distant land)?
TODO

## Is there a mod to unlock more faces and hair styles?
[Freedom of Aesthetics](https://www.nexusmods.com/morrowind/mods/31167)

## Is there a mod to share hair styles between mer races?
[Hair Expander](https://www.nexusmods.com/morrowind/mods/52922)

## Why I cannot rest in cities?
Install [Actual Illegal Resting](https://www.nexusmods.com/morrowind/mods/51804)

## Why I cannot travel from Balmora to Maar Gan with silt strider directly? It's the same travel network
Install [All Silt Strider Ports](https://www.nexusmods.com/morrowind/mods/43796)  
Similar mod for boats: [All Boat Ports Plugin](https://www.nexusmods.com/morrowind/mods/946)

## Killed enemies respawn like in some kind of MMO
Install [No Respawns](https://www.nexusmods.com/morrowind/mods/53853)

## How can I adjust the respawn rate of plants
In [GMST Menu](https://www.nexusmods.com/morrowind/mods/46428) set `iMonthsToRespawn`  

## [Balance] Difficulty (some enemies) scale with level, I want more challenges early game
[No Respawns](https://www.nexusmods.com/morrowind/mods/53853) provides this option as well.  
[OperatorJack's Deleveler](https://www.nexusmods.com/morrowind/mods/47897) will also delevel item lists.

## [Balance] Enemies react too late and they stand still when fighting
Install [PvP](https://www.nexusmods.com/morrowind/mods/51034)

## How to tell blighted creatures from non-blighted?
Install [Blighted Animals Retextured](https://www.nexusmods.com/morrowind/mods/42245)  
If you want something opposite, that is remove "blighted" adjectives and "diseased" adjectives from their names, install [No Disease Labels](https://www.nexusmods.com/morrowind/mods/48295)

## How to tell filled soul gems from empty soul gems?
Install [Visually Filled Soul Gems](https://www.nexusmods.com/morrowind/mods/46709)

## Is there a way to control the weather?
Install [Weather Chances Adjuster](https://www.nexusmods.com/morrowind/mods/48335)

## I've installed a lot of face and hair mods, what would be the easiest way to test them?
Install [Barbershop aka FaceRecustom](https://www.nexusmods.com/morrowind/mods/52359) (hotkey to rotate between faces: alt + p)

## Wearing pauldrons under robe looks ridiculous
Install [Hidden Robe Armor](https://www.nexusmods.com/morrowind/mods/48425)

## Tombs entrances don't look like tombs
Install [Know Thy Ancestors](https://www.nexusmods.com/morrowind/mods/49678)

## Looting is clunky, too much clicking
Install [QuickLoot](https://www.nexusmods.com/morrowind/mods/46283). Recommended to use with [Morrowind Containers Animated - Edited for Quickloot](https://www.nexusmods.com/morrowind/mods/49297).  
QuickLoot successor: [More QuickLoot](https://www.nexusmods.com/morrowind/mods/53809) (allows skipping junk, includes weight and value in the popup)

## I'm annoyed by all the game popups
Install [Auto Yes to All](https://www.nexusmods.com/morrowind/mods/48863)

## Is there an auto-load mod?
Yes, install [Instant Load](https://www.nexusmods.com/morrowind/mods/48907)

## Is there any way to mark visited locations?
Install [Been There Done That](https://www.nexusmods.com/morrowind/mods/52807) and/or [Chalk](https://www.nexusmods.com/morrowind/mods/54043)

## [Balance] Bounty on your head should be gone when you kill all witnesses
Install [The Last Witness](https://www.nexusmods.com/morrowind/mods/46684)  
Alternative: [No Witness - No Bounty aka NWNC](https://www.nexusmods.com/morrowind/mods/53384)

## When sneaking in first-person view it doesn't feel like crouching
Install [Pluginless and Adjustable Lower First Person Sneak](https://www.nexusmods.com/morrowind/mods/48642)

## How do I know what are my chances of picking up lock or disarming a trap?
Install [Security Adjuster (MWSE)](https://www.nexusmods.com/morrowind/mods/47914)
Some QoL tweak for lockpicking: [Quick Security](https://www.nexusmods.com/morrowind/mods/52918) - allows you to select lockpicks or probes from a selection menu instead of having to search in your inventory to select it and equip it manually  
For greater immersion: [Visually Trapped](https://www.nexusmods.com/morrowind/mods/48936)

## Isn't it a bit cheaty that I know about all traps?
Install [Locks and Traps Detection](https://www.nexusmods.com/morrowind/mods/48528) - detection will depend on your Security skill and some RNG

## Pickpocketing is useless
Install [Pickpocket](https://www.nexusmods.com/morrowind/mods/47581)  
Alternative: [Pickpocket Minigame](https://www.nexusmods.com/morrowind/mods/52793)

## Sneaking is useless
Install [Stealth Improved aka stealth](https://www.nexusmods.com/morrowind/mods/49614)  
Install [Sneaky Snatcher](https://www.nexusmods.com/morrowind/mods/55369)  
Also: [Skillful Sneaking](https://www.nexusmods.com/morrowind/mods/52410) - the more skilled you are, the faster you move when sneaking, can jump too

## Sneaky strike doesn't take weapon type into account
Install [Sneaky Strike](https://www.nexusmods.com/morrowind/mods/48317)

## The right column of the charsheet is too long compared to the left one
Install [Tidy Charsheet](https://www.nexusmods.com/morrowind/mods/52776)

## [Balance] When leveling, HP gain is not retroactive, which incentivizes focusing on Endurance early game. Excess progress and multiplier bonus are also sometimes wasted.
Install [Improved Vanilla Leveling](https://www.nexusmods.com/morrowind/mods/48065) (fixes retroactive health, multipliers and how XP carry-over contributes to attributes)  
XP carry-over fix (unrelated to attribute gain): [Experience Carryover](https://www.nexusmods.com/morrowind/mods/53972)  
Also: [Quest Skill Reward Fix](https://www.nexusmods.com/morrowind/mods/48269) - applies skill rewards from quests more optimally.

Alternative for Improved Vanilla Leveling: [Madd Leveler](https://www.nexusmods.com/morrowind/mods/45865)  
Another alternative: [MULE - Mort's Ultimate Leveling Experience](https://www.nexusmods.com/morrowind/mods/47452)

## Sometimes when I go through a door and want to go back it's locked again
Install [Loading Doors Lock Tune](https://www.nexusmods.com/morrowind/mods/46094)

## Persuasion is kind of obscure, how do I know what are my chances? how to make it more fun?
Install [Visible Persuasion Chance](https://www.nexusmods.com/morrowind/mods/48634)  
Install [Silver Tongue](https://www.nexusmods.com/morrowind/mods/49086) (you can see NPC Fight and Alarm levels and lower Alarm, makes conversation with hostile NPC possible if they are not currently attacking, this makes Intimidation more useful)

## [Balance] Training armor skill is tedious
Install [Armor Training](https://www.nexusmods.com/morrowind/mods/51741)

## [Balance] Training magic is unbalanced, it should depend on amount of Magicka spent, rather than number of spells cast
Install [Magicka Based Skill Progression -- MWSE-Lua Edition](https://www.nexusmods.com/morrowind/mods/48330)

## [Balance] In general, shouldn't failed tries train the skills as well?
With [OEA's Practice Makes Perfect](https://www.nexusmods.com/morrowind/mods/49142) it will

## How can I pick up books without reading them?
Install [Book Pickup](https://www.nexusmods.com/morrowind/mods/46625)  
Alternative: [activate key takes open books](https://www.nexusmods.com/morrowind/mods/54181)  
The book pickup mod lets you skip the reading part when taking books; the second mod makes it easier to take the book once you've started reading it.

## Is there a way to compare my current gear with new gear?
Install [MWSE Compare Tooltips](https://www.nexusmods.com/morrowind/mods/51087), default hotkey: alt

## Keys make a mess in my inventory
Install [Consistent Keys](https://www.nexusmods.com/morrowind/mods/47954), it renames keys so they have a consistent naming scheme

## Potions make a mess in my inventory
Install [Potion Renamer](https://www.nexusmods.com/morrowind/mods/49853), it sorts them first by effect and then by quality

## Soulgems make a mess in my inventory
Install [Soulgem Renamer](https://www.nexusmods.com/morrowind/mods/49861)

## Other items still make a mess in my inventory
Install [Rational Names Lite](https://www.nexusmods.com/morrowind/mods/51241).  
Nice to have: [Inventory Sorter](https://www.nexusmods.com/morrowind/mods/54637?tab=posts) (not possible to save the sorting, though)

## Every key looks the same
Install [Key Replacer](https://www.nexusmods.com/morrowind/mods/1207)

## I've got rid of an important item
Install [Keepers](https://www.nexusmods.com/morrowind/mods/51821) to prevent it in the future (suffixes quest items with "!")  

## [Balance] The game is too easy, how to make it harder?
* Controlled Consumption: [click](https://github.com/the-overdriven/morrowind-issues-and-fixes/tree/main#being-able-to-chug-multiple-potions-at-the-same-time-is-too-op-alchemy-is-too-op-in-general)
* No enemy (and item) scaling: [click](https://github.com/the-overdriven/morrowind-issues-and-fixes/tree/main#difficulty-some-enemies-scale-with-level-i-want-more-challenges-early-game)
* Adjust progress: [click](https://github.com/the-overdriven/morrowind-issues-and-fixes/tree/main?tab=readme-ov-file#progresion-is-too-quickeasy)
* Better economy: [click](https://github.com/the-overdriven/morrowind-issues-and-fixes/tree/main?tab=readme-ov-file#it-is-too-easy-to-get-rich)
* MXPS - Morrowind Experience Point System (MWSE): [click](https://www.nexusmods.com/morrowind/mods/53870), alternative: MULE, or CCCP
* [BTB's Game Improvements (Necro Edit) Tweaked](https://www.nexusmods.com/morrowind/mods/50308) - BTB's Game Improvements with Necrolesian's and Sigourn's edits. A lot of tweaks: rebalances races, birthsigns, ingredients, magic (some effects disabled to prevent exploits), NPCs have new spells, lowered value of overpriced items, overhauled enchantments (i.e. it's no longer possible to self-enchant items, or to make custom constant effect enchantments), overhauled skill progression
* Recommended with BTBGI: [Fortify MAX](https://www.nexusmods.com/morrowind/mods/49825), [Economy Adjuster: Crime](https://www.nexusmods.com/morrowind/mods/47130), [Enhanced Detection Lite](https://www.nexusmods.com/morrowind/mods/48471), [Nimble Armor](https://www.nexusmods.com/morrowind/mods/48251), [Lua Lockbashing](https://www.nexusmods.com/morrowind/mods/48544), [Hold Your Breath](https://www.nexusmods.com/morrowind/mods/48872)
* Limited Resting, Waiting and Regen - [click](https://www.nexusmods.com/morrowind/mods/49191) or [No Rest Without Beds](https://www.nexusmods.com/morrowind/mods/46724), also: [Find Shelter MWSE](https://www.nexusmods.com/morrowind/mods/48583)  
* Intruder - No Trespassing Mod - [click](https://www.nexusmods.com/morrowind/mods/55223)  

Enemies  
* Make enemy react quicker and fight better: [click](https://github.com/the-overdriven/mw-enhanced/tree/main?tab=readme-ov-file#balance-enemies-react-too-late-and-they-stand-still-when-fighting)
* More Deadly Morrowind Denizens: [click](https://www.nexusmods.com/morrowind/mods/48745)
* Vanilla friendly creatures and undeads expansion: [click](https://www.nexusmods.com/morrowind/mods/48818)
* OAAB - Tombs and Towers: [click](https://www.nexusmods.com/morrowind/mods/49131)
* Mines and Caverns: [click](https://www.nexusmods.com/morrowind/mods/44893)

## [Balance] Progression is too quick/easy
* Install [Proportional Progression](https://www.nexusmods.com/morrowind/mods/45697) or [Proportional Progression Expanded](https://www.nexusmods.com/morrowind/mods/53782)  
* also [Fixed level multipliers](https://www.nexusmods.com/morrowind/mods/45064) - have your level multipliers be constant (only on attributes whose skills you leveled up)

## [Balance] It is too easy to get rich
* [Commonly Used Containers Nerfed](https://www.nexusmods.com/morrowind/mods/47068?tab=files) - nerfs barrel, boxes, etc. (included in [Morrowind Anti-Cheese](https://www.nexusmods.com/morrowind/mods/47305))
* [Realistic Repair](https://www.nexusmods.com/morrowind/mods/46673) - you need a forge to repair gear, gear of killed NPC is damaged
* [There Can Be Only One](https://www.nexusmods.com/morrowind/mods/47766) - makes daedric items unique
* [Morrowind Anti-Cheese](https://www.nexusmods.com/morrowind/mods/47305) includes nerfed Containers mod, Container Ownership and Rarer Scrap Metal mods, makes stealing known expensive items harder or replaced with cheaper equivalents, buffs some NPCs and enemies, creeper and mudcrab have less gold, increased blind effect on Boots of Blinding Speed, nerfed items (Ebony Mail, Wraithguard, Kagrenac's Tools, Helm of Oreyn Bearclaw, Silver Staff, Water Spear, Ancient Silver Daggers, Black Hands Dagger, Ebony Arrows of Slaying, and many more), Gedna Relvel was nerfed, some items devalued (ingredients)
* [Smarter Harder Barter](https://www.nexusmods.com/morrowind/mods/50883) - among many other things, removes randomness from haggling
* [The Morrowind Randomizer](https://www.nexusmods.com/morrowind/mods/44989) - randomizes the locations of 49 legendary items
* [Economy Adjuster Adjustments](https://www.nexusmods.com/morrowind/mods/47130) - increase the mercantile and speechcraft skills of service providers

## [Balance] There are too many (low tier) items in game
* [Commonly Used Containers Nerfed](https://www.nexusmods.com/morrowind/mods/47068?tab=files) - nerfs barrel, boxes, etc. (included in [Morrowind Anti-Cheese](https://www.nexusmods.com/morrowind/mods/47305))
* TODO

## [Balance] Trainers are broken
(idea) One way to fix it, could be to make all trainers still able to teach skills but not more than 1-5 levels (per each trainer), so visiting them would still be worthwile.

## NPC are too repeatable
Install [NPC Clothes Randomizer - MWSE](https://www.nexusmods.com/morrowind/mods/54064)  
Install [More Heads and Diversity](https://www.nexusmods.com/morrowind/mods/47213) and [More Heads and Diversity MWSE](https://www.nexusmods.com/morrowind/mods/48429)

## How can I soul trap NPCs?
Install [Seph's NPC Soul Trapping](https://www.nexusmods.com/morrowind/mods/50744)

## Animations are janky
Install [Animation Blending](https://www.nexusmods.com/morrowind/mods/53779)

## I forget where everyone is, especially trainers
Install [Trainer Log](https://www.nexusmods.com/morrowind/mods/38391) (has to be cleaned with [tes3cmd](https://github.com/john-moonsugar/tes3cmd))  
For all NPCS: [Who's Where](https://www.nexusmods.com/morrowind/mods/48843)

## Outside of cities, everything that moves wants to kill me
Install [Non-Homicidal Ecosystem](https://www.nexusmods.com/morrowind/mods/42327)  
Could be even better if these attacks were based on player's level or health (weak monsters should be afraid to attack strong player), something like [Improved Cliff Racer AI](https://www.nexusmods.com/morrowind/mods/44712)  
Alternative: [Less Aggressive Creatures](https://www.nexusmods.com/morrowind/mods/48292)  
Or: [Passive Healthy Wildlife (2016)](https://www.nexusmods.com/morrowind/mods/44675)  
Fun way to exterminate a selected type of creatures: [Animal Extinction - MWSE](https://www.nexusmods.com/morrowind/mods/51137)

## I'm lost in Vivec, every canton looks the same
Install [Colorful Vivec](https://www.nexusmods.com/morrowind/mods/53806) and [Vivec Cantons Reconnected](https://www.nexusmods.com/morrowind/mods/48081)  

Alternative: [Vivec City of Swords](https://www.nexusmods.com/morrowind/mods/54054). Incompatibilities:
* grass mods
* lanterns
* Silt Strider

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
Install [Encumberance increaser](https://www.nexusmods.com/morrowind/mods/28213) and/or [Bag of Holding](https://www.nexusmods.com/morrowind/mods/47778).  
Nice to have to monitor encumbrance: [HUD Encumbrance Bar](https://www.nexusmods.com/morrowind/mods/49608)  
Other: [Units and Vagueness](https://www.nexusmods.com/morrowind/mods/49046)  
Alternative: [Weight of the World](https://www.nexusmods.com/morrowind/mods/51195)  

## NPCs are shouting when I'm stealing but do nothing
Install [No NPC Shouting at 0 Alarm](https://www.nexusmods.com/morrowind/mods/53837)

## NPCs are commenting my outfit ALL THE TIME
Install [Outfit Greetings Tweaked](https://www.nexusmods.com/morrowind/mods/46066)

## NPCs are too boring/static
Install 
* [Small Talk](https://www.nexusmods.com/morrowind/mods/54810)  
* [Immersive Morrowind](https://www.nexusmods.com/morrowind/mods/54513)  
* [NPC Schedule](https://www.nexusmods.com/morrowind/mods/45525) or [Lightweight Lua Scheduling](https://www.nexusmods.com/morrowind/mods/48584)  
* [Lightweight Lua Scheduling](https://www.nexusmods.com/morrowind/mods/48584)
* [Living CIties of Vvardenfell (Reupload)](https://www.nexusmods.com/morrowind/mods/54662)

## Once NPC attacks it's impossible to calm them (permanently)
Install [Permanent Calm - Pacifist Option Apologize Befriend Bandit and Beasts Calm Down](https://www.nexusmods.com/morrowind/mods/51737)  

## I'm blocked by NPC standing in the way
Install [Just Move](https://www.nexusmods.com/morrowind/mods/53340)  

## I want to have a stash for items but can't put much in containers
Install [ContainerWeightMaxed](https://www.nexusmods.com/morrowind/mods/45698) (DELETED! TODO: add mirror)   
~~Even if using QuickLoot, [inom - Inventory mouse wheel](https://www.nexusmods.com/morrowind/mods/46847) might still be helpful here for moving items from/to container quicker.~~  
Actually, UI Expansion has an option to move items from/to container on left click.  
Portable alternatives: [Bag of Holding](https://www.nexusmods.com/morrowind/mods/47778), [MWSE Containers Extended](https://www.nexusmods.com/morrowind/mods/54120)  

## Is there a quicker way for looting items?
Install [More QuickLoot](https://www.nexusmods.com/morrowind/mods/53809)

## How do I know which item is owned or important?
Install [Essential Indicators](https://www.nexusmods.com/morrowind/mods/48267)

## How can I focus on creature from a distance?
Install [Hostility Indicator](https://www.nexusmods.com/morrowind/mods/49030) (default Left Shift)

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

## How can I disenchant enchanted items?
Install [Disenchant](https://www.nexusmods.com/morrowind/mods/48111)

## Very few dialogues are voiced

<details>
  <summary>(click to expand)</summary>

Install AI-generated [Kezyma's Voices of Vvardenfell](https://www.nexusmods.com/morrowind/mods/52279)  
Other, AI-generated voices:  
[Ashlander Voices](https://www.nexusmods.com/morrowind/mods/53863)  
[Vivec](https://www.nexusmods.com/morrowind/mods/52333)  
[Yagrum Bagarn](https://www.nexusmods.com/morrowind/mods/52344)
[Voiced Vivec and Yakety Yagrum - Merged and Improved](https://www.nexusmods.com/morrowind/mods/53098) (not AI)  
[Voices of Vvardenfell Unofficial Addon - Talkative Telvanni](https://www.nexusmods.com/morrowind/mods/52343)  
[The Wisest Women](https://www.nexusmods.com/morrowind/mods/52353)  
[Nordic Banter](https://www.nexusmods.com/morrowind/mods/53715)  
[Friends Reunited](https://www.nexusmods.com/morrowind/mods/53601)  
[Quest Voice Greetings](https://www.nexusmods.com/morrowind/mods/52273)  
[Great Service](https://www.nexusmods.com/morrowind/mods/47767) (unused, not AI)  
[Idle Talk](https://www.nexusmods.com/morrowind/mods/46948)  
[Its a Deal](https://www.nexusmods.com/morrowind/mods/47968)  
[Real Disposition](https://www.nexusmods.com/morrowind/mods/51427)  
[So. You're the Nerevarine.](https://www.nexusmods.com/morrowind/mods/46896) (unused, not AI)  
[FMBP - Greet Service](https://www.nexusmods.com/morrowind/mods/50937) (unused, not AI)
[Nordic Banter](https://www.nexusmods.com/morrowind/mods/53715)  
[Sermons and Preachers Vanilla edit](https://www.nexusmods.com/morrowind/mods/53294)  

more:  
[Voice Overhaul](https://www.nexusmods.com/morrowind/mods/51215)  
</details>

## Dialogues with NPCs are too repeatable
Install [UI Expansion](https://www.nexusmods.com/morrowind/mods/46071) and [Dialogues Decluttered](https://www.nexusmods.com/morrowind/mods/48301)

## How to break from endless dialogue choices loop?
Install [Force Close Dialogue Menu aka shiftGoodbye](https://www.nexusmods.com/morrowind/mods/52553)

## Passing by NPCs makes them too reactive
Install [Shut Up](https://www.nexusmods.com/morrowind/mods/43310), NPCs will notice you only when you look at them.

## NPC don't look at me when I talk to them
Install [Small Quality of Life Improvements - MWSE](https://www.nexusmods.com/morrowind/mods/53905) (Face Me component)

## It's unrealistic that I can join two factions that don't like each other
Install [More Exclusive Factions](https://www.nexusmods.com/morrowind/mods/49618)

## Companions, city guards and faction members are not helping me when I'm attacked
Install [More Attentive Guards](https://www.nexusmods.com/morrowind/mods/48622). Caution, has a bug: "Every time I attack in self defense, I get reported and attacked"

For companions: install [Diligent Defenders](https://www.nexusmods.com/morrowind/mods/45717)  
Deleted [Supreme Follower System](https://www.nexusmods.com/morrowind/mods/45599?tab=files&file_id=1000030142) (direct file link)  
Other companion mods: [article by Danae](https://danaeplays.thenet.sk/companion-modsi/)

## How to tell my followers (companions and summons) who to attack? 
You can do on hotkey when you install [Kill Command](https://www.nexusmods.com/morrowind/mods/46723)

## How to see my followers' stats? 
Install [More Detailed Companion HealthBars MWSE Lua Script](https://www.nexusmods.com/morrowind/mods/51389)  
Or [Companion Health Bars MWSE Lua Script](https://www.nexusmods.com/morrowind/mods/46136)

## How to share equipment with followers?
[NPC Functionality (2008)](https://www.nexusmods.com/morrowind/mods/49563)  
[Open Inventories (2009)](https://www.nexusmods.com/morrowind/mods/23197)  
[Smart Companions](https://www.nexusmods.com/morrowind/mods/49848)

## Companions get lost occasionally
Install [Easy Escort](https://www.nexusmods.com/morrowind/mods/45712)

## There is no hotkey for Map
After installing [Small Quality of Life Improvements - MWSE](https://www.nexusmods.com/morrowind/mods/53905) the hotkey is "M"

## There is no hotkey for torches
After installing [Torch Hotkey](https://www.nexusmods.com/morrowind/mods/45747) the hotkey is "C"

## There is no hotkey for Quests
After installing [Hot Quests](https://www.nexusmods.com/morrowind/mods/48976) the hotkey is "U"

## Is there a mod that allows mouse control?
Yes, [Morrowind Mouse Control](https://www.nexusmods.com/morrowind/mods/48254)

## Can I make Quests screen more usable (i.e. bigger)?

<details>
  <summary>(click to expand)</summary>
	
Yes. With [Smart Journal](https://www.nexusmods.com/morrowind/mods/47492):  
![image](https://github.com/the-overdriven/morrowind-issues-and-fixes/assets/100090726/3a18f6a4-1676-4e76-9bcd-c908e3b167be)

Highlighting and hiding quests is doable with [Better Questlist](https://www.nexusmods.com/morrowind/mods/48272)  
Bigger Quest Log: [Quest Log Menu](https://www.nexusmods.com/morrowind/mods/54203)
</details>

## Can I write in my journal or search through it?
Yes, with [Journal Search and Edit aka journal](https://www.nexusmods.com/morrowind/mods/46756) or [Writing and Journal Enhanced](https://www.nexusmods.com/morrowind/mods/48002)

## Information in Journal is too vague or not very helpful
Install [Improved Journal Entries](https://www.nexusmods.com/morrowind/mods/48105)

## How to tell different potions in inventory apart?
Install [Colored Potions](https://www.nexusmods.com/morrowind/mods/48999)

## How to tell different scrolls in inventory apart?
Install [MWSE Scroll Icons](https://www.nexusmods.com/morrowind/mods/54006)

## All merchants are broke
Install [More Barter Gold](https://www.nexusmods.com/morrowind/mods/40053) and [Merchant Gold Resets Instantly](https://www.nexusmods.com/morrowind/mods/43764)

## Race and birthsign spells are ~~cringe~~ useless and unbalanced
Install [Balanced Passive Races and Birthsigns](https://www.nexusmods.com/morrowind/mods/47782), it will replace spells (that no one uses anyway) with permanent bonuses. [BTB's Game Improvements (Necro Edit) Tweaked](https://www.nexusmods.com/morrowind/mods/50308) also rebalances races and birthsigns.

## Using shrines is clunky
[Shrine Tooltips](https://www.nexusmods.com/morrowind/mods/48275) adds tooltips that tells you what each option actually does. [No Thank You](https://www.nexusmods.com/morrowind/mods/49681) adds a cancel option.

## Movement when swimming and levitating is clunky
Install [Better Buoyancy](https://www.nexusmods.com/morrowind/mods/48929), adds jump key to float upwards, and the sneak key to sink downwards.

## How to tell which texture a mesh is using?
Install [Selection Details](https://www.nexusmods.com/morrowind/mods/51095)

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

## Game sounds are limited and weird
Install [Impact Sounds](https://www.nexusmods.com/morrowind/mods/52747)

## How to fix silent NPC groans?
Some mods break it (Character Sound Overhaul and Impact Sounds - I'm looking at you). Install [Deathrattle Sounds](https://www.nexusmods.com/morrowind/mods/53938), it doesn't restore groans on hit, but it does restore groans on death. And adds some extra. It fixes NPCs blabbering after death as well.  
Recommended together with [Small Quality of Life Improvements - MWSE](https://www.nexusmods.com/morrowind/mods/53905), which includes a component preventing repeating same combat voice-overs repeatedly (I Heard You The First Time!)

## How to silence your character's groans?
No mod that mutes that at the moment, but [Hit Sound Overhaul](https://www.nexusmods.com/morrowind/mods/55049) can help with misplaced groans. Also: [Voice Overhaul](https://www.nexusmods.com/morrowind/mods/51215)  
Related: [Mute High-Pitched Hit Sounds](https://www.nexusmods.com/morrowind/mods/53764)  

## How to disable vanity camera? (the one that turns on after 30 seconds) 
Install [No Auto Vanity Camera aka NoAutoVanityCam](https://www.nexusmods.com/morrowind/mods/48933)

## Game doesn't notify me explicitly enough that I started or finished a quest
Install [Skyrim Style Quest Notifications aka SSQN](https://www.nexusmods.com/morrowind/mods/53175), [Skyrim Style Quest Notifications - Legendary Edition](https://www.nexusmods.com/morrowind/mods/53712) and [Skyrim Style Quest Notifications Great Patch Hub](https://www.nexusmods.com/morrowind/mods/55480)

## Game doesn't notify me that someone died
Install [Notifications](https://www.nexusmods.com/morrowind/mods/48600)  

## Where is the medium armor trainer?
There is none, Bethesda forgot to add it. Install [Cinia](https://www.nexusmods.com/morrowind/mods/47153)

## I can sleep in owned beds, doesn't make much sense
Arguably it does make sense (especially if the house is abandoned), but if you like to limit yourself: install [Bed Buddies](https://www.nexusmods.com/morrowind/mods/46632). 

## Magicka (mana) doesn't regenerate
Most advanced and configurable mod for this appears to be [Magicka Regeneration Suite](https://www.nexusmods.com/morrowind/mods/49153)  
Alternative: [Puristy Friendly Magicka Regen](https://www.nexusmods.com/morrowind/mods/45636)

## How to rename a spell or enchanted item?
Install [Player Made Magic Rename](https://www.nexusmods.com/morrowind/mods/51484)

## How to see how much longer a spell will last?
Install [Effect Timers](https://www.nexusmods.com/morrowind/mods/51787) or [Buff Bars](https://www.nexusmods.com/morrowind/mods/51924). Arguably Buff Bars are better, as they cover more spells (and take less screen space), but they don't show time values.

## How to remove learned spells?
Install [Spellscribe aka rev_SPEL](https://www.nexusmods.com/morrowind/mods/52809). Use paper on yourself to scribe the spell for backup. Remove the spell with Shift+Click.

## Why do I have to read a blank piece of paper before I pick it up?
Install [Plain Paper Fix](https://www.nexusmods.com/morrowind/mods/47735)

## How to tell if I picked up an ingredient?
Install [Graphic Herbalism - MWSE and OpenMW Edition](https://www.nexusmods.com/morrowind/mods/46599) + [Graphic Herbalism Lighting](https://www.nexusmods.com/morrowind/mods/47864)

## How to prevent starting new game accidentally?
Install [New Game Confirmation](https://www.nexusmods.com/morrowind/mods/47693)

## How do I know what music track is currently playing?
Install [Now Playing](https://www.nexusmods.com/morrowind/mods/53091)  
[HeartStrings](https://www.nexusmods.com/morrowind/mods/52965) also has this feature (but only when a track starts).

## How do I know where the Intervention spell would teleport me?
Install [Smart Intervention](https://www.nexusmods.com/morrowind/mods/50752)

## Is there a way to make the console (`) more usable?
Install [Blue - Smart Console](https://www.nexusmods.com/morrowind/mods/53427)  
Also: [More Console Commands](https://www.nexusmods.com/morrowind/mods/52500)

## I don't know what time it is
Install [Clocks](https://www.nexusmods.com/morrowind/mods/50840)

## The game doesn't notify me when it's the time to rank up
Install [Rank Up - Advancement Notifications 2](https://www.nexusmods.com/morrowind/mods/54140)

## The game doesn't notify me when can I level up
Install [Level Up Indicator - MWSE](https://www.nexusmods.com/morrowind/mods/51376). Depending on used leveling mod, level up screen might not be needed at all!

## How to disable the cheesy shiny glow?
Install [Assetless No Glow aka NoGlow](https://www.nexusmods.com/morrowind/mods/47925)  
To change glass weapons and armor: [Dim Glass - Less Irritating Glass Armor and Weapon](https://www.nexusmods.com/morrowind/mods/51544)

## How to change the cheesy shiny background behind magical items in inventory?
Install [Seph's Inventory Decorators](https://www.nexusmods.com/morrowind/mods/50582)

## How to install animations (i.e. xbase_anim.1st.kf)?
Copy to Meshes. Some require [LizTail Animation Kit](https://www.nexusmods.com/morrowind/mods/43606/)

## How to show 1-st person swimming animation?
Install [MCAR](https://www.nexusmods.com/morrowind/mods/48628)

## How to add custom music to the game?
Contrary to common belief, .mp3 files don't need to be in constant 128kbps bitrate. The most important thing is to remove padding from tags. One can do that with [Foobar](https://www.foobar2000.org/): right click on the selected track(s), go to Properties, Tools and click on Optimize Size. The music files should be placed in Data Files/Music. Cover art has to be removed as well, can be done with [Mp3tag](https://www.mp3tag.de/en/).

Recommended music system: [MUSE aka MWSE/mods/music](https://www.nexusmods.com/morrowind/mods/46200)  
Or: [HeartStrings](https://www.nexusmods.com/morrowind/mods/52965). Or: [my fork](https://github.com/the-overdriven/mw-HeartStrings).

## Is there a music mod that resumes the previous track when transitioning the theme? For example: switching from a wilderness theme to a battle theme and then back to the wilderness theme would play the same track, as it played before the transition (instead of moving on to next track)

Now there [is](https://www.nexusmods.com/morrowind/mods/55543). I [forked](https://github.com/the-overdriven/mw-HeartStrings) Heartstrings and added this feature. It also prevents repeating the same track.

## How to track mod updates on Nexus?

<details>
  <summary>(click to expand)</summary>

Go to [Tracking Centre](https://www.nexusmods.com/mods/trackingcentre). The problem with this view is that it's not very useful. In the tracking centre we are only interested in mods that we already downloaded but in the meantime they got an update. Unfortunately, Nexus doesn't provide a filter for mods you haven't downloaded yet. And, most importantly, you cannot filter out mods that didn't have new updates since last time you've downloaded them.

Here comes the power of CSS and JS magic.

The first time you open the page, open the console with F12 and run the following code:

```javascript
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

## Nice to have mods
Not necessarily essential and fixing any glaring issues, but can improve the gameplay.
* [Animated Pickup](https://www.nexusmods.com/morrowind/mods/54532)
* [Adventurer's Backpacks](https://www.nexusmods.com/morrowind/mods/43213)
* [It's a deal aka Fairwell Customer](https://www.nexusmods.com/morrowind/mods/47968)
* [Give a Gift](https://www.nexusmods.com/morrowind/mods/46661) (bribe with items)
* [Glow in the Dahrk](https://www.nexusmods.com/morrowind/mods/45886) (windows glow in the dark)
* [Inspect It](https://www.nexusmods.com/morrowind/mods/54636) (inspecting items)
* [Caps Click to Drop](https://www.nexusmods.com/morrowind/mods/52518)
* [Morrowind Containers Animated aka MWCA](https://www.nexusmods.com/morrowind/mods/42238)
* [Mage Robes](https://www.nexusmods.com/morrowind/mods/45739)
* [Menus Hider on Item Select - MWSE](https://www.nexusmods.com/morrowind/mods/50974) (other mod allows throwing out items with CapsLock + click)
* [Morrowind World Randomizer](https://www.nexusmods.com/morrowind/mods/52534) (warning, it's cursed)
* Fashionwind: [glasses and goggles](https://www.nexusmods.com/morrowind/mods/50448), [masks and facewraps](https://www.nexusmods.com/morrowind/mods/51610), [scarves](https://www.nexusmods.com/morrowind/mods/52540)
* [MM - Enhanced Invisibility](https://www.nexusmods.com/morrowind/mods/47565)
* [MM - Enhanced Telekinesis](https://www.nexusmods.com/morrowind/mods/47534)
* [Rag n'wahs](https://www.nexusmods.com/morrowind/mods/54574)
* [Combat Enhanced MWSE](https://www.nexusmods.com/morrowind/mods/51414)
* [Spells Reforged (only visuals)](https://www.nexusmods.com/morrowind/mods/52263)
* [HUD Weapon Charge](https://www.nexusmods.com/morrowind/mods/47962)
* [Hide Grass](https://www.nexusmods.com/morrowind/mods/52764) (makes grass be rendered by MGEXE)
* [Water Sounds](https://www.nexusmods.com/morrowind/mods/47794)
* [Animated Arrow Denocker](https://www.nexusmods.com/morrowind/mods/52418)
* [Perfect Placement](https://www.nexusmods.com/morrowind/mods/46562)
* [Pincushion](https://www.nexusmods.com/morrowind/mods/46862)
* [Steadicam](https://www.nexusmods.com/morrowind/mods/52225)
* [Transporter Lights aka lightguideus](https://www.nexusmods.com/morrowind/mods/48050)
* [The Midnight Oil - Lighting Overhaul](https://www.nexusmods.com/morrowind/mods/48293) (toggle lights on and off, town lights go off during the day)
* [Quick Equip aka shiftEquip](https://www.nexusmods.com/morrowind/mods/48341) (left shift + click to equip items)
* [Bomberman](https://www.nexusmods.com/morrowind/mods/49667) (elemental blasts knock enemies back)
* [Tamrielic Lore Tooltips](https://www.nexusmods.com/morrowind/mods/45954)
* [Enlightened Flames aka erect/flames](https://www.nexusmods.com/morrowind/mods/48816)
* [Wading in Water MW](https://www.nexusmods.com/morrowind/mods/48783)
* [Cave Drips](https://www.nexusmods.com/morrowind/mods/43488)
* [Correct Iron Warhammer](https://www.nexusmods.com/morrowind/mods/43576)
* [Audiobooks of Morrowind](https://www.nexusmods.com/morrowind/mods/52458)
* [Travel Tooltips - A Travel UI Mod](https://www.nexusmods.com/morrowind/mods/48306)
* [Vapourmist - A Cloud and Mist Mod](https://www.nexusmods.com/morrowind/mods/50517)
* [UI Expansion Better Training Icons](https://www.nexusmods.com/morrowind/mods/51190)
* [AURA](https://www.nexusmods.com/morrowind/mods/48255) (adds ambient sounds)
* [Watch the Skies - Dynamic Weather and Sky Effects](https://www.nexusmods.com/morrowind/mods/48636)
* [Magican't](https://www.nexusmods.com/morrowind/mods/50990) 
