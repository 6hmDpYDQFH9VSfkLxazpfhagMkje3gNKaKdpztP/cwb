+++
title = "Game Modding"
description = "Citra has a powerful modding framework allowing for multiple formats of patches and flexibility in distribution."
+++

Citra has a powerful modding framework allowing for multiple formats of patches and flexibility in distribution.

### Directory Structure

The following is an example of a mod in Citra.<br>
Each title has its own Mods directory that can be opened by right-clicking on the game in Citra (alternatively `load/mods/<Title ID>` in the User Directory)
```
load/mods/<Title ID>
  - exefs
  - romfs
  - romfs_ext
  - exheader.bin
```
Note that everything demonstrated above is optional. It is possible that a mod contains only some of these files.

#### ExeFS
The ExeFS directory contains replacements or patches for the game's executable.
These types of mods typically alter game behavior or logic.
Currently you can put a replacement file, or apply two types of patches: `IPS` and `BPS`.

To use a replacement file for the game code, put a file named `code.bin` in the ExeFS directory.

To use an `IPS` patch, put a file named `code.ips` in the ExeFS directory.
More details on the `IPS` format can be found on [ZeroSoft](https://zerosoft.zophar.net/ips.php) and [SMWiki](http://old.smwiki.net/wiki/IPS_file_format).

To use a `BPS` patch, put a file named `code.bps` in the ExeFS directory.
More details on the `BPS` format can be found on [byuu](https://byuu.org/projects/beat#bps).

*Note: For compatiblity with Luma3DS, you can also put these ExeFS replacements/patches directly in the mods folder instead of the `exefs` subfolder.*

#### RomFS
The RomFS directory contains replacements for the game's assets and general files.
These types of mods typically alter a game's textures, text, fonts, sounds, or other graphical assets.
If this directory is not empty, Citra will combine the contents of it with the base game with files from this directory taking precedence over the base.
This technique is called LayeredFS.
```
It is important to note that for this to work properly, the directory structure of the game has to be mirrored in this directory.
```

It is much easier to get started with a RomFS mod than an ExeFS mod.
To dump a game's RomFS, right-click on the game and select `Dump RomFS`.
The dumped directory will be opened after the dump was completed, and can be found at `dump/romfs/<Title ID>` in the User Directory.

#### RomFS Extension (romfs_ext)
The RomFS Extension directory contains patches and stubs for RomFS files.
This allows modders to delete files within the RomFS if a file of the same name but the extension `.stub` is found at the same directory within `romfs_ext`.
Similarly, if a file with the same name but with extension `.ips` or `.bps` is found at the same directory within `romfs_ext`, the base game file will be patched with it.
```
It is important to note that currently patches require loading the entire file into the RAM.
Please do not use too many patches at the same time. This will likely be improved in the future.
```

#### ExHeader
The `exheader.bin` overrides the game's ExHeader, which specifies information like codeset info and system mode. By overriding the ExHeader, modders can allow more code to be added or more RAM to be used.

### Example
For example, let's examine Pokemon Ultra Sun, a popular game for modding.

Since its Title ID is `00040000001B5000`, our mods for this game will go in `load/mods/00040000001B5000` in the User Directory. 

Within this folder, there are `exefs`, `romfs`, and `romfs_ext` directories and the `exheader.bin` file provided by the author.
It is okay to omit one (or more) of them if the mod does not need to replace those files. Additionally, if a folder is empty Citra will ignore it.

### Using Mods Intended for Luma3DS
Citra's game modding framework offers drop-in compatibility with Luma3DS mods.

Just put a Luma3DS mod (usually structured like the following example) into Citra's mod folder for the title, and it should directly work.
```
luma/titles/<Title ID>
  - romfs
    - other files and folders
  - code.bin / code.ips
  - exheader.bin
```
Note that everything demonstrated above is optional. It is possible that a mod contains only some of these files.

### Using 3GX plugins
Citra can use 3GX plugins by using the same format that the Luma3DS 3GX plugin loader uses. Plugins can be placed in 2 locations:
```
- sdmc/luma/plugins/<TITLEID>/<filename>.3gx 
To set a plugin for a specified game (higher priority).

- sdmc/luma/plugins/default.3gx 
To set a plugin which would be loaded for all games (lower priority).
```
You can find the `sdmc` folder in Citra's [User Directory](https://citra-emu.org/wiki/user-directory/).
After placing your plugin in the correct location, you'll need to check the 3GX plugin `Enable 3GX plugin loader` option in Citra's System settings. The plugin(s) should now apply the next time you run your game.

### Conclusion
If you are a modder looking to distribute mods for Citra and have further questions or doubts, feel free to ask in our Discord.

If you are a user trying to install a mod for Citra and are having issues with it, first try asking the mod author for help. If it still doesn't work, feel free to ask in our Discord.
