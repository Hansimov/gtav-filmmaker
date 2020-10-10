References:
* Grand Theft Auto V Native DB (More info than give-two)
    * https://alloc8or.re/gta5/nativedb/
* FiveM native reference 
    * https://runtime.fivem.net/doc/natives/
* GTA5 - NativeDatabase 
    * https://give-two.github.io/
* citizenfx/natives: native documentation 
    * https://github.com/citizenfx/natives
* GTAV original files (open with OpenIV)
    * *\GTAV\update\update.rpf\x64\levels\gta5\script\script_rel.rpf\*
* njames93/GTA-V-Script-Decompiler: decompile the script resources (xsc,csc,ysc) files
    * https://github.com/njames93/GTA-V-Script-Decompiler
* root-cause/v-decompiled-scripts: Decompiled scripts of GTA V version 1868. 
    * https://github.com/root-cause/v-decompiled-scripts
* ali-alidoust/gta5-extended-video-export: GTA V Video Export Enhancement 
    * https://github.com/ali-alidoust/gta5-extended-video-export


Problem specified links:
* openCamera for Grand Theft Auto V - Scripts & Plugins - GTAForums (Recording limit)
    * https://gtaforums.com/topic/815220-opencamera-for-grand-theft-auto-v/
* Cameras - Documentation - GTAForums 
    * https://gtaforums.com/topic/793247-cameras/
* Take a screen shot from command line in Windows - Super User 
    * https://superuser.com/questions/75614/take-a-screen-shot-from-command-line-in-windows
* batch.scripts/screenCapture.bat at master · npocmaka/batch.scripts 
    * https://github.com/npocmaka/batch.scripts/blob/master/hybrids/.net/c/screenCapture.bat
* c++ - How can I take a screenshot in a windows application? - Stack Overflow 
    * https://stackoverflow.com/questions/3291167/how-can-i-take-a-screenshot-in-a-windows-application


Film making tools comparison:
* Unreal Engine, C4D / Maya
    * Advantages:
        * High capabilities to customize resources and timeline
        * Support real-time playing and high-quality rendering simultaneously
        * Great combination with programming and art
    * Disadvantages:
        * Need to create most of the assets and interactions from the beginning, which might be the most time-consuming part
            * can be solved with external free resources and reuse existent resources
            * can use procedural generation techniques
        * Not easy to use, cooperate and distribute
            * not a problem for an experienced single creator
* GTA5 + mods
    * Advantages:
        * Large number of preseted resources, including buildings, environments, peds, vehicles, weathers, animations, interactions, audios and so on
        * Support real time playing
        * Large community with lots of mods and many users
    * Disadvantages:
        * Lack of cababiliies to edit and arrange the scenes
            * can be solved with Filmmaker mod (under my development)
        * Low quality of rendering frames
            * can be partly solved with graphics related mods, such as NaturalVision and "Extended Video Export" (with the drawbacks of Rockstar Editor)
            * for a story-dominant film, the quality of frames might not be an important issue
        * Cannot record long-time clips with Rockstar Editor
            * can be solved with real-time or in-game recording system (under my development)
        * Lack of customized resources
            * can be solved with external resources and OpenIV
            * can use green screen and After Effects

In short, the key issue of choosing UE or GTA5 is:
    * UE's high customizability, with high time cost
    * GTA5's high integration, with low customizability and weird working flow
Thus for a one-person creator like myself, use GTA5 might be better.
But in the long term, UE is more valuable.

Maybe we can use GTA5 for lively city and streets scenes, UE for customized cameras and character animations, and After Effects to combine them.

Develop tools:

* Visual Studio
* ScriptHookV
* wxWidgets / Qt
* FiveM
* OpenIV
* .NET Reflector

Assitant softwares:

* Unreal Engine
* Cinema 4D
* CityEngine
* After Effects
* Houdini

Assitant mods:
* Menyoo PC
* Simple Trainer
* Scene Director
* NaturalVision


Todo list:

* [optional] remove the restrictions of rockstar recording duration
    * Or just DEPRECATE the rockstar editor completely, and use Windows video and audio api to record them, which is a more feasible solution
    * the time limit of recording seems to be hard-coded in the GTA5.exe file, but there are still some possible methods to walk around. The time limit seems to depend on the number of events and business of environments.
        * Hack the GTA5.exe and modify the parameter which sets the limit
            * Hard but not impossible I guess, since the hex format of the .exe file still reveals some infos according to my simple diving
        * Use two threads, when t1 is going to exceed the limit, start t2 recording, save t1 as clip, and when t2 is going to exceed the limit, start t1 recording, save t2 to clip, ... Then combine these clips.
            * Midium but still lots of problems to encounter
        * Create a brand new record system
            * the most feasible solution
            * write a screenshot mod (inspired by the Ingame Screenshot mod)
            * use a third party screen shot software, send an event to it everytime (per frame) when the rendering process is done

* free control camera, peds (enhanced menyoo spooner mode)
* keyframes, auto add key when recording
* support mouse click / toggle focus on Play and Edit UI
* support autocomplete drop-down list
* timeline
* ...


Modules:
* Mode:
    * Play, Edit, Spawn, Record, Preview, Render
* Object:
    Ped, Vehicle, Camera, Light, Event, Misc
* Properties:
    * ALL: name, type, visible, pos, rot, scale
    * Ped:
        * animation, carry, waypoint, speek, control
    * Vehicle:
        * waypoint, control
    * Camera:
        * FOV, interp, 
    * Event (including Weather):
        * 
    * Misc

Questions:
* Pure native functions or using Qt?
    * Qt is better. Although it might be complicated to communicate and combine the native functions and Qt modules when developping the MOD, it is easier to design the GUI.
* Since rendering images can be done with screenshot per frame, how to add sound effects?
    * M1: Detect and store the sound effects id called during playing, extract, export and compose them to .wav formats.
        * Maybe not realistic, since there are many other factors to affect the final sound effects besides the original audio file
    * M2: Real-time screen recording, both images and audios.
        * How to ensure the smooth playing (rendering) of the scenes?
    * M3: Use Rockstar Editor 
        * Time limit restrictions of recording
        * Information loss of cameras

Implementations:
    Mode:
    * Edit mode
        * edit records, clips
        * select and search peds, vehicles, maps, animations, 
        * apply effects
        * choose events, paths, keyframes, ...
    * Play mode
    * Record mode?
    * Preview mode?

    Timeline:
    * Event-Driven, instead of  Data-Driven which is the common way of doing things in 3d softwares
        * 3d and editing softwares can control each frame of video, but it is not practical to apply this kind of method on the game playing, since game is real-time and event-driven
        * One idea is that we can apply a continuous control or event sequence to the obeject through the Timeline
            * Cons: cannot control the states of cars and peds accurately
        * Another idea is that we can use reverse events, for example, we set the start and end position of a car in the Timeline first, and then calculate its speed at each time point, and then determine the operations which the cars should take, like speed-up or slow-down
            * cons: hard to implement
        * Or we can combine the two ideas?
        * Some other techniques are:
            * recording events, just like what Scene Director does



