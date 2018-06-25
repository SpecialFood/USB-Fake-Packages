# USB Fake Packages
USB Fake Packages is a tool I've made for the PS4 Jailbreak, based on versions 4.55 and 5.05.

The tool would probably not work on 4.05 so I wouldn't suggest trying.

There are 2 versions of the tool, 1.0c for version 4.55 and 1.1b for version 5.05.

The tool searches the console for fake packages based on the routes given by the user and links them with the USB fake packages based on the conditions the user have entered (whether it's linking with existent USB fake packages or copying from the console to the USB and then linking, in some cases an operation might fail due to the entered conditions, for example if a fake package already exists in the destination and it's not matching the console fake package (or not checking for a match in the conditions) so it won't delete the fake package in the destination for safety, and skip that console package file, another example is a copy attempt failing because of USB drive lack of space).

A processed USB fake package will be named with the extension of ".sym.pkg" instead of ".pkg", so that a difference will be noticed.

Make sure your USB drive is formatted as exFAT (recommended) or as FAT32 (not recommended).

Based on the pkg2usb by SiSTRO and AppToUsb by stooged, much different in my opinion however, changing from AppToUsb to this tool won't be a problem, but already symlinked fake packages won't be reprocessed, only ones that are not will be processed, keep that in mind.

I've based the tools on 10 partial systems, which are :

1. Variable Tools :

The work with variables inside the program, whether allocating space, rellocating, freeing, clearing, etc.

2. Text Tools :

The work with texts, whether to get inner texts or to combine ones.

3. Decimal Tools :

The work with numbers, to calculate logs and powers.

4. Convertion Tools :

The work with conversions, when needed to conver between bases (base 10 to 2 or 10 to 16 etc.).

5. Text Score Tools :

The work with visual texts, I've made a text scoring system that scores letters width and lines width and then trying to fit a text inside a certain line based on the score of the text and the score of the line (so a text "abcdefghijklmn" might become "abc...lmn" for example), this way I can control how texts are visually seen.

I've used this system for the PS4 messages sending.

6. File Tools :

The work with files, whether it's to open/close/read/write/copy etc.

7. Folder Tools :

The work with folders, the same idea as the work with files.

8. CFG File Tools :

The work with CFG files, I've written by myself, in order to receive info by the user, the rules are simple.

A CFG file is consisted of sections, inside them are fields, which each have keys and values for each key.

A section is written as [*Section Name*]

A field is written as *Key Name* = *Value1*, *Value2*... *Value13*;

In order to name a key or a value with a name that might confuse the reader (for example key = "tre=rt", there's "=" in it and the reader will look for a value, but it's just the key name) a one can use quote marks for the name.

Spaces and new lines are ignored when they should be, and comments are written as "//" without the quote marks.

An example for a valid CFG file :

{

  [   SectionA   ]  //some note
  
  // some empty line  
  
"ABRR==T"   = "34;24;",    Tg;//some note

["Section B"]

arr=3,5;

}

9. SFO File Tools :

The work with SFO files, wrote a code that reads a SFO file, and returns the values it has.

This current tool uses it for a naming element for the USB fake package files.

10. PS4 Tools :

The work with basic PS4 Jailbreak tools, based on tools to create a symlink between files or to initialize the PS4 system, send a PS4 message in the notification bar, etc.

# Instructions for the USB CFG file :
I edit the CFG file in notepad, I assume all of you can do the same, make sure the cfg file is in the root of the USB drive with the name of USBFakePackages.cfg.

Make sure that "/" slashes are used in routes, and not "\\" slashes.

The CFG file is consisted of 3 sections, the order of them or their keys is less important and shouldn't affect the tool working operation.

Section 1, "Options" :

The section has 4 keys, the section decides all the basic options required for the tool to function properly.

Section 1, Key 1, "CheckUSBConsoleRoot" :

This key is for the folder path that the console will use in the USB as a working space, the key has 2 values.

Section 1, Key 1, Value 1, "CheckUSBConsoleRootFolder" :

This value is for mentioning the folder path that the console will use in the USB as a working space.

The value can be set as "false" or a location, while false means that one won't transfer files there, copy conditions will be off and it'll only match package files with the USB routes and won't transfer them afterwards (means that the TransferPackageFile condition in the USB routes is off).

A location goes for the working space.

Section 1, Key 1, Value 2, "CheckUSBConsoleRootPackageFile" :

Check if the package file already exists in the working space, true goes for check if it's and false goes for don't.

If a match has been found then linking with the correct match.

note : if the first value of this key is set as false then the key should only have 1 value which is the first.

(CheckUSBConsoleRoot = false;)

Section 1, Key 2, "USBPackageFileNameElements" :

The elements that the USB package file name is consisted of, check the file USBPackageFileNameElements.txt file in the root folder of this project for all the possible values.

Each element takes a place in 1 value, and the key supports unlimited values.

Set as false for no elements, in case of only linking with existing files found in USB routes.

Section 1, Key 3, "CopySourceFile" :

The conditions of whether or not to copy console package files, the key has 2 values.

Section 1, Key 3, Value 1, "CopyConsolePackageFile" :

Copy console package file if needed, true goes for copy, false goes for don't.

Section 1, Key 3, Value 2, "MaxProcessSystemMessagesAmount" :

The amount of messages that will be shown during the copy process at max, for example, if it's set as 5 then 0-20% will be shown, as well as 20-40%, 40-60%, 60-80%, 80-100%, a possible routine might be 13% completed, 27%, 53%, 68%, 88%, 5 is max but not necessarily will happen every time, 33%, 84% is also a possible routine, most likely for a small fake package file.

There is also a time limit between messages, it's not up to the user as of now and set for 10 seconds (means that messages during the copy process won't be seen without a 10 seconds time space between them).

note : if the first value of this key is set as false then the key should only have 1 value which is the first.

(CopySourceFile = false;)

Section 1, Key 4, "CheckSymlinkExistenceShowSystemMessages" :

Show a message if a console package file already has a symlink, saying that the certain console package file already has a symlink, true goes for show, false goes for don't.

In my opinion if one a packages collector this option might get annoying, when seeing the message "the package file *X* already has a symlink" 7357 times in a row, but for a small packages amount it's quite nicely.

Section 2, "ConsoleRoutes" :

There are no keys required in this section, but that they're all optional.

Section 2, A key :

*ConsoleRoute* = *MaxConsoleSubFolderLevels*, *ConsoleDeniedFolderPaths*;

ConsoleRoute :

The route to search in the console, written as "Console/X" or just "Console" if one wants to search the whole console.

MaxConsoleSubFolderLevels :

The max dive into the route sub folders, 1 goes for 1 max dive, 0 goes for none, "Infinite" goes for infinite, etc.

ConsoleDeniedFolderPath_X :

The console folder paths to avoid searching, if one want to make the process go faster or dont want certain console folders to be searched he can add them here, written as "Console/a/b", this value is optional.

Section 3, "USBRoutes" :

There are no keys required in this section, but that they're all optional.

Section 3, A key :

*USBRoute* = *TransferPackageFile*, *ChangePackageFileName*, *MaxUSBSubFolderLevels*, *USBDeniedFolderPaths*;

USBRoute :

The route to search in the USB, written as "USB/X" or just "USB" if one wants to search the whole USB drive.

TransferPackageFile :

If a match has been found whether to move it to the USB Console working space or not, true goes for moving, false goes for not.

ChangePackageFileName :

If a match has been found whether to change the name of the USB fake package file based on the USB package file name elements or not, true goes for changing, false goes for not.

MaxUSBSubFolderLevels :

The max dive into the route sub folders, 1 goes for 1 max dive, 0 goes for none, "Infinite" goes for infinite, etc.

USBDeniedFolderPath_X :

The USB folder paths to avoid searching, if one want to make the process go faster or dont want certain USB folders to be searched he can add them here, written as "USB/a/b", this value is optional.
