# Morrowind issues and how to fix them
While some of the fixes might work on OpenMW these docs focus exclusively on Morrowind.exe and Windows ystem.

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

## On multiple screens setup, moving mouse in game moves cursor on second screen
Install and run [FullscreenLock](https://github.com/blaberry/FullscreenLock) every time you run the game (the script above runs it automatically)
