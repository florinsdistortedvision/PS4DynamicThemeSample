# PS4DynamicSample

# Requirements/Tools needed:
- Your source video must be in a format that can be split into a sequence of frames (recommended: .mp4 for videos or .gif).
- Free Video to JPG Converter by dvdvideosoft (freeware, other program can be used) for converting your source video/gif to frames.
- TGA-PNG-JPG-TO DDS by Backporter (https://github.com/Backporter/TGA-PNG-JPG-TO-DDS). Note!: You must download and install Nvidia GameWorks Legacy Texture Tool:DDS Utilities (https://developer.nvidia.com/legacy-texture-tools) for the program to work!
- A random content ID generator such as Random-Content-ID by Backporter (https://github.com/Backporter/Random-Content-ID).
- orbis-pub-sfo and orbis-pub-gen from FPKG Tools.
- Dynamic Custom Theme sample discovered by yy oossk and merged/edited by me: clone this repo :)


# 1. Converting source video to frames usable by PS4

Note!: Keep in mind that dynamic themes have a limit of 16MB of video/frames files, so to insure the theme can be applied, video must be 1280x720, otherwise the theme will give a error when trying to apply!

- Open Free Video to JPG Converter and add your source, in Extract section select Total of 34 frames from video (Note! You can select more, as long as you also modify the .xml file with the new frames).
- Your source will now be in 34 .jpg files. It is advised that you rename them now from 00.jpg to 33.jpg.
- The PS4 theme system uses a sequence of .dds pictures that are controlled by a .xml file, so we need to convert our .jpg files to .dds. Open TGA-PNG-JPG-TO DDS, add all your frames, leave default dxt1a, and click start.
- We should now have files from 00.dds to 33.dds, ready for PS4 to read.
- Replace all the .dds files with the ones included in the sample archive in scene/background.raf/.

# 2. Customizing the speed of frames

- A crucial step is figuring out the right speed of the frames, unfortunately this will most likely be needed as I noticed.
- Open scene/background.raf/index.xml and look for lines that contain : <case wait="2">. The default value is 2, tinker with the values until your frames are played correctly. Note!: You must change all of them!
- At this point, if you had more frames converted in step 1, you can add the additional lines, following the same structure as the other ones.
- Save the file.

# 3. Other modifications

Here are all the other things you can change:

- sce_sys/icon0.png. Dimensions must be : 512x512, file must be png! This is the icon of the theme seen in Settings-Theme.
- sound/bgm_home.at9 and all the .vag files. bgm_home is the background music, a .wav can be converted via at9tool. The .vag files are the sound effects, .wav can be easily converted via MFAudiov11. Note!: Files must be at 48000Hz.
- texture/content_icon and texture/function_icon is where all the icons are. Content_Icon files must be .png at 512x512. Function_Icon files must be .png at 128x128.
- texture/preview.png is the preview file for the theme (just before applying the theme in Settings). Must be .png at 1920x1080.
- /theme.xml. Here you can change the colors of the font and what color the theme will use for menus like Settings, etc. 

Example of things you can change:
- < themecolor >0< /themecolor > holds the color for the menus. A description is present inside the .xml file telling which color is which number (ex: 1=pink, 2=red, etc)
- < fontcolor >#FF4F7ECE< /fontcolor > holds the text color. Value is hexadecimal.
- < fontshadowcolor >#00000000< /fontshadowcolor > holds the shadow font color. Value is hexadecimal.
- < focuscolor >#FF00BAFF< /focuscolor > holds the focus color of the font. Value is hexadecimal.
- < homebgm-enable >True< /homebgm-enable > specifies whether the theme should use your custom background music or the default one. True=custom, False=default.

# 4. Editing Param.sfo

- Open sce_sys/param.sfo using orbis-pub-sfo.
- Make sure Category is PS4 System SoftwareTheme, input your Content-ID using Random-Content-ID by Backporter.
- In Title Text section, you can input the Theme Title and the Theme Provider (your name). These will be seen in Settings-Theme in Theme Information settings.
- Optionally you can input a Theme Version such as 01.12 in Theme Settings section and add other languages in Add/Delete Languages section.
- Save the file.

# 5. Building the theme as a fpkg

- Open orbis-pub-gen
- File - New Project - System Software Theme Package
- Double click Image0
- Drag and drop all the folders and files into the File Name section. Note!: Do not drag a single folder containing all the files, the structure should be: sce_sys folder, scene folder, sound folder, texture folder and theme.xml (no other folders)!
- Close the window
- Command - Project Settings - Package tab
- Input the same Content-ID as made in the param.sfo file. Passcode can be all 0's. Select Ok.
- Select Build. Select your output path. Select Build!
- Install the pkg theme via debug settings or your preffered method and apply the theme!
- Done!

Congrats! You now have a fully customized dynamic theme!

# End Notes!:
- As this is a fpkg theme, this cannot be made permanent/persistent after reboot!
- If the source files are playing too fast/slow, you must edit the <case wait="2"> file again. NOTE!: If any edits are made, you have to also make a new Content-ID in param.sfo and the project settings when building pkg, otherwise it will cause issues such as the theme not applying!
