# DreamcastCdiTool

![dreamon1](https://cloud.githubusercontent.com/assets/8145834/8882599/e246bdfa-3250-11e5-91a4-7724e474077b.png)

To make Dreamcast read any game from CD-R backup flawlessly it worth to convert CDI file from Audio/Data to Data/Data format. Also it’s possible to create a compilation disc containing multiple games to preserve CD-R discs. In order to be able to create compilation disc initial CDIs must be in Audio-Data format.

This tool was created to automate convertion process as well as to make it easy to crete compilation discs containing several games.


# Usage

Just launch launcher.bat script file under Windows to start the process. It will ask to pick CDI files to process.


# Creating a multi game compilation disc 

To create compilation disc launch the script and just pick several CDI files from the dialog using CTRL/Shift buttons.

Almost done. 

While processing the CDI files the script will ask to enter a display name for every game selected (or just press Enter to use CDI file's name) as well as a cover image to display in selection menu (or use "-silet" flag to skip both inputs)

All the games will be presented withing DreamOn Collection menu by default with the names and the images picked previously. It's possible to use a simple DP3 menu which sometimes works better for some games. Use -dp3 launch flag for this.

# Multi game compilation disc loading issue

If some games doesn't boot within DreamOn boot menu (always check it on emulator before burning to CD-R) but still they loads fine as standalone game (converted to Data/Data) the following should do the trick:

Launch launcher.bat with -relocate flag:

> launcher -relocate

And answer yes (y) for evetry game which doesn't boot when prompted with a question like "Put !gameName! to the root?". 
Answer No (n) for games which boots fine within DreamOn boot menu.

Loading issues happens because while creating multi game disk every game is placed to its own folder so no files with the same name overlaps. However some games requires to be in the root to load properly (for example all WinCE games). -relocate flag gives a way to cheoose for every specific game if it should be placed in separate folder or in the root.

WARNING: while placing several games in the root some files may overlap - they will be displayed in the scrip's output window. Test such games carefully on emulator. Consider using differnet set of games if files overlapped and any of the game doesn't boot.

# Burning

Note. Test the final CDI image with Dreamcast emulator. If it can't boot a game (or ony game from multi game disc) it's very likely that the game won't boot with you Dreamcast as well unless emulator couldn't play the original CDI.

Alcohol 120 works smooth to burn Data-Data CDI images for furhter use with Dreamcast console.

After selecting a CDI image Alcohol will show sessions and tracks from the image. If it's in Data/Data it should contain only 2 sessions with 1 track each - "session 1 track 1" is a big one (actual game data) and "session 2 track 2" - a small one.

Alcohol Settings for burning a dics:

1. Write Speed - minimal possible (in my case 10x was fine)
2. Write mode: RAW DAO. Hardware dependent. If you can't set this mode you should find another CD/DVD drive to burn a CD-R backup.
3. Remove tick from "Enable Buffer Underrun Technology" option


# Additional flags

Main launcher.bat script accepts the next launch flags:

<b>-dest</b>       Choose destination folder for extracting and creating final CDI image.

<b>-modify</b>     Allows modification of extracted folder before creating final CDI image. Useful if the original image contains dummy files to preserve space.

<b>-silent</b>     Used in compilation disc image only. Flag for skipping custom display name for games and image cover dialog.

<b>-keep</b>      Flag for preserving all intermediate files.

<b>-dp3</b>       Use DP3 menu as boot menu instead of DreamOn Collection boot menu. Sometimes DreamOn boot menu can't load a game properly. Sometimes DP3 boot menu can help in these cases.


# Important

Make sure you Dreamcas can run CD-R. Mine is HKT-3030 which is able to read CD-R discs. In The bottom of the same sticker there is rounded 1 PAL/E which also could matter. Also Goolge if your model can run CD-R’s.

In my experience CD-R brand really matters. Try different ones if you Dreamcast can’t boot one. In My case SmartTrack discs worked all the time, while it failed to load with Verbatim and Mirex. Google for the best CD-R.


# Additional notes

During convertation to Data-Data format it's reauired for script to updated boot file. Usually it's name is 1ST_READ.BIN or 0WINCEOS.BIN. In that cases script will locate them automatically. Some CDI archives has differnet name for that file and script will ask to locate it manually. You should locate and pick one in order for script to be able to create bootable CDI image.

If the initially provided image is in Data-Data format it will be skipped. Also it's not possible to use such CDI for multiple game images due t otechnical restrictions. If anyone kow a way haw to create using extracted Data-Data folder a bootable CDI image I'll be glad to add that functionality to script as weel.

# Inspired 

by all the information I was able to find on the web regarding creating backups CD-Rs for Dreamcast. Just wanted to gather everything in one place and to provide an easy and user-friendly way for using the tools.

# Tools Used

cdirip - ftp://ftp.cs.tu-berlin.de/pub/aminet/disk/cdrom/cdirip-0.6.3.readme

isofix - https://github.com/DeadlySystem/isofix

7z - http://www.7-zip.org/

binhack32 - http://sourceforge.net/projects/binhack32/

mkisofs - https://en.wikipedia.org/wiki/Cdrtools

cdi4dc - https://github.com/DC-SWAT/DreamShell/tree/master/sdk/bin/src/img4dc/cdi4dc
