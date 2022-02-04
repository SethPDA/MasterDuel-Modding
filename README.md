# Yu-Gi-Oh! Master Duel Modding

This Guide will go through the process of creating a music mod for Yu-Gi-Oh! Master Duel, but it can do any type of mod, though it wasn't tested for other types of files yet. 

I will not take any responsability if someone uses this guide for nefarious purposes like cheating or gaining advantage over others. Just keep in mind that if you have this kind of intention, I would like to kindly ask you to leave, because you may be ruining the modding scene for this game (Konami might update the game so it will check for modified files on every startup, then bye bye modding).

---

Guide maintained by these people: [SethPDA](https://discord.com/users/SethPDA#1193)

Guide last updated: **2021-Feb-04**

Works with Game Version:  **1.0.1**

Tested on following platforms: **Steam**

---

## Required tools:

**Asset Studio** *v0.16.21* (https://github.com/Perfare/AssetStudio)

**Unity Assets Advanced Editor** *v1.2 - called Second Release* or the latest *Build* (https://github.com/Igor55x/UAAE)

**Unity Engine 2020.3.18f1** (currently, this is the Unity version of which the game is built with. It may be required in the future to update Unity in order to meet the version of the game's Unity version). (https://unity3d.com/get-unity/download?thank-you=update&download_nid=65149&os=Win)

---

### First things first. ###

So the Steam version of the game is structured as follows: 
```
\Yu-Gi-Oh!  Master Duel\LocalData
\Yu-Gi-Oh!  Master Duel\LocalSave
\Yu-Gi-Oh!  Master Duel\masterduel_Data
```
The `masterduel_Data` folder contains music, graphics and code related to the title screen of the game. This sorta works like a launcher for the game (especially on the mobile version). All the cards and other graphics, music, core gameplay is located in `LocalData`. This is what you need to work with. This is also the folder which gets updated when the game tells you that it needs to download some files. If Steam tells you it has an update, it most likely will update the `masterduel_Data` folder. But for this tutorial, let's concentrate on `LocalData` folder.

So for the sake of this guide, I'm going to mod the game with a custom music, but you can mod it with literally anything since it's all made in Unity.



## Steps: ##

0. First of all, extract every tool (**Asset Studio** and **UAAE**) and install **Unity** before proceeding. For Unity install, you need to check the Windows Build platform/environment. Unity will also not run without having Unity Hub installed because it needs to check for a license. A free personal license is enough for this guide. You might also need stuff like .Net framework and so on, which I will not go through in this guide. There is plenty of info about that.
1. Open **Asset Studio**
2. You need to select the `LocalData` folder of the game
	>File-> Extract Folder-> `X:SteamLibrary\steamapps\common\Yu-Gi-Oh!  Master Duel\LocalData`
3. Select a folder where to extract. Mine will be at: `X:\SteamLibrary\steamapps\common\MasterDuelMod\GameExtract`
Let it do it's thing, it will take a while to decompress the game. The whole thing is about 10GB uncompressed.
I suggest you don't even move the Asset Studio window while it's doing its thing. For me, it froze all the time like that. If it still freezes for you, try again by re-opening it. If it still freezes, then you don't have enough RAM in your PC.
4. When it's finished, go back to **Asset Studio**, and then 
	>File-> Load Folder-> **Select the folder you just extracted.** In my case it's `X:\SteamLibrary\steamapps\common\MasterDuelMod\GameExtract`
5. In **Asset Studio** switch from `Scene Hierarchy` tab to `Asset List` tab. Find the thing you want to mod. In my case, I would like to change the music which appears on the `Deck edit` screen.

      At the top of the window, click on:
      >Filter Type-> Audio Clip

      to see only the audio files in the whole game.
You can sort them by name as well and you can further filter them. I'm just going to sort it by name and look for an asset called **`BGM_MENU_02`**.
If you click on an asset, you can preview it in the preview pane. In the case of music, you can listen to it.
6. Now open **Unity** and create a new project with the empty template called `3d core`then open it.
7. Go back to **Asset Studio** and take a look at the line of the **`BGM_MENU_02`** item. In the second column called `Container`, it shows where the engine is looking for the files. In my case this is the following text: `assets/resourcesassetbundle/sound/audioclip/bgm/bgm_menu_02.wav` . Take note of this, as you'll need this folder structure in the next step.
8. Go back to **Unity**, and create this folder structure. At first you'll have only an `Assets` folder which is perfect for us but we need the folders further down the tree. So create a folder in `Assets` called `resourcesassetbundle`. Then create another folder inside `resourcesassetbundle` called `sound` and so on.
9. When you reached the folder called `bgm`, drag and drop the file you're going to want in the game. In my case, I would like to change the `Deck Edit` music, to the deck music from **Yu-Gi-Oh! Power Of Chaos Joey The Passion**. In the case of music or sound effects, be sure to make them **`.wav`**
10. Drag and drop the `joeydeck.wav` into the `bgm` folder of the project then click on it.
11. In the right side of the screen, in the **Inspector** panel, some value changes will be needed so that the game properly plays it. In the case of music, these are the followiing: 
	>**Load type:** Streaming
	>
	>**Compression format:** Vorbis
	>
	>**Sample Rate Setting:** Override Sample Rate
	>
	>**Sampple Rate:** 48000Hz
	>
	>Press Apply.
12. Now rename your asset from `joeydeck` to **`BGM_MENU_02`** . This is the name of the Asset in game, which we noted in step 5.
13. In order for **Unity** to properly build the assets, drag and drop your music file into the **Unity** scene and just save it. It doesn't matter if it has a camera or light in the scene, we won't be using that anyway, we just need to make sure so that **Unity** builds our mod files.
14. Go to 
	>File -> Build settings -> 
	>
	>Platform: PC
	>
	>Target Platform: Windows
	>
	>Architecture: x86_64
	>
	>Compression method: LZ4

         Leave everything else untouched. 

Press **Build** and choose a folder where to build the files. 
In my case it's `X:\SteamLibrary\steamapps\common\MasterDuelMod\MyModProjectBuild`
Please note that at this point you might encounter building errors. I will not include fixes for those errors in my guide since there are plenty of tutorial out there for that kind of thing anyway.

If you would like to check if it has been built correctly, follow along but if you're confident that your build was successful, jump to **Step 18**.

15. When the build is finished, open up **Unity Assets Advanced Editor** or **UAAE** for short.
16. Open your now built mod's **Data** folder. In my case it's: `X:\SteamLibrary\steamapps\common\MasterDuelMod\MyModProjectBuild\TestYugioh_Data` and open the file called `data.unity3d` with **UAAE**
	>File -> Open -> 
	>
	>`X:\SteamLibrary\steamapps\common\MasterDuelMod\MyModProjectBuild\TestYugioh_Data\data.unity3d`

      It will ask you to decompress the bundle. Just decompress it into the memory since we have only one single music in it right now. 
      But if you're going to work on a large mod, you may be needed to decompress it normally. 
      For now, select Memory in the bundle decompression window. Then press the big LOAD button.
17. Take a look and see if all of your files are there. (We can see the **`BGM_MENU_02`** in the list) If everything's okay, then proceed. Close **UAAE** for now.

18. Now we have our music in the `sharedassets0.resource` file in the project build folder. We need to replace the correct resource file in order for the game to play it. But first, we need to identify which file do we need. Go back to **Asset Studio** and right click on the file you wanted to mod. In my case it's still **`BGM_MENU_02`** and click `Show original file`. This will open a window where it will show you where these files are located in the game.

    For this example, it will show this folder: `X:\SteamLibrary\steamapps\common\MasterDuelMod\GameExtract\f7efe7a2\0000\23\230d3279_unpacked`

	>23\230d3279_unpacked

    Take note of the numbered folders in which it is located because that is how we're going to trace it back.

19. In the folder above, you'll see two files. One without any extension, this is the meta file which contains information about the music asset, and the other one is literally the music file with the `.resource` extension. This means that this is the file we need to replace in the game itself. Copy the **NAME** of the `.resource` file. The name not the file itself. In my case it's : `CAB-788321b1ede439deac3186a7331dc35e.resource` and go back to your **build** folder:
    
    `X:\SteamLibrary\steamapps\common\MasterDuelMod\MyModProjectBuild\TestYugioh_Data`
    
    and then rename your `sharedassets0.resource` file to the filename you just copied.

20. Open up **UAAE** and navigate to the game's directory structure: 

    `X:\SteamLibrary\steamapps\common\Yu-Gi-Oh!  Master Duel\LocalData\f7efe7a2\0000`
    
    Here you see a bunch of numbered folders. Now go into the same folder as I mentioned above for you to take note of.
    That folder structure was in the **`GameExtract`** part but this time, we enter the same folder structure, but in the game itself.
    In my case it's :
    `X:\SteamLibrary\steamapps\common\Yu-Gi-Oh!  Master Duel\LocalData\f7efe7a2\0000\23`
    Right now I will have to look for a file called **`230d3279`** which was also noted above. (**230d3279_unpacked**)

21. Open the found file in **UAAE**
    It will ask you to decompress the bundle. Just decompress it into the memory since we have only one single music in it right now. But if you're going to work on a large mod, you may be needed to decompress it normally. For now, select Memory in the bundle decompression window. Then press the big LOAD button.

22. At this point we have two items in the dropdown (two only because we are changing a music only in the game. You might have more if you change other things).

23. Select the long numbered item with the `.resource` extension.

24. It's very important to do the following, else it won't work. Go back to your built mod's project data folder where you already renamed your `sharedassets0.resource`. In my case, it's already called `CAB-788321b1ede439deac3186a7331dc35e.resource` which I chose from the dropdown as well. Now copy this file into the **UAAE**'s main folder where the main exe is located. For me it's `X:\UAAE-new`. This is crucial because **UAAE** will not read files from other directories only in it's root directory. It may read from other directories when Run as Admin but I didn't test that.

25. Press on *Import* and select the freshly copied file. Now you'll see if you click on the dropdown, the `.resource` file has an asterisk alongside it's name, meaning it was modified. Click on it. 

26. Now go to 
	>File -> Save 

	    Be careful! The name of this file MUST BE the name of the file we opened in UAAE !!!
	    It is that numbered folder. In my case it's `230d3279`.
	    Be sure to NOT give any extension to the file because it might be difficult to remove it later on.
	    It should be JUST the numbered name then SAVE.

27. Now depending on where you saved this, go to that folder, in my case it's: `X:\SteamLibrary\steamapps\common\MasterDuelMod\230d3279`

    Copy that file to the game's data folder where we first found that. If you've closed **Asset Studio** along the way, just open it back, load the extracted game's folder, search for your item (**`BGM_MENU_02`**) and then right click to `Show original file`. This will show you the path where you need to copy the file, but instead of copying it in the extraced mod folder, do it into the game's `LocalData` folder. In my case it's: `X:\SteamLibrary\steamapps\common\Yu-Gi-Oh!  Master Duel\LocalData\f7efe7a2\0000\23`
and overwrite the file. Of course before copying, you can backup the file just in case.

28. Congratulations on your first **Master Duel MOD!** Now open the game, and check it out! Have fun!

# Here is a video link of the MOD in action!

# https://streamable.com/cawjso
