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
* Cameras - Documentation - GTAForums 
    * https://gtaforums.com/topic/793247-cameras/


Problem specified links:
* openCamera for Grand Theft Auto V - Scripts & Plugins - GTAForums (Recording limit)
    * https://gtaforums.com/topic/815220-opencamera-for-grand-theft-auto-v/

Tools:
* Visual Studio
* ScriptHookV
* wxWidgets / Qt
* FiveM
* OpenIV
* .NET Reflector

Modules:
* MODE:
    * Play, Edit, Spawn, Record, Render, Preview
* OBJECT:
        Ped, Vehicle, Camera, Event, Misc
    PROPERTIES:
        Ped:





Todo list:
* remove the restrictions of rockstar recording duration
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
* keyframes
* support mouse click
* support autocomplete drop-down list
* timeline
* 

Questions:
* Pure native functions or using Qt?


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

    Timeline


