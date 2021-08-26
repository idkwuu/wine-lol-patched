# How to install League of Legends from scratch (in Lutris)

### Prerequisites

- Make sure you have your graphics drivers installed! (follow Lutris' guide on [installing drivers](https://github.com/lutris/docs/blob/master/InstallingDrivers.md))
- Make sure you have Wine install, and all of its dependencies (follow Lutris' guide on [installing Wine's dependencies](https://github.com/lutris/docs/blob/master/WineDependencies.md))
- And ofc, [Lutris](https://lutris.net)

### Instructions

- Extract your preferred build of Wine to `~/.local/share/lutris/runners/wine/`
- Download the League of Legends installer [here](https://lol.secure.dyn.riotcdn.net/channels/public/x/installer/current/live.na.exe)
- Download the launch helper and syscall checker scripts
    - [launchhelper.sh](https://lutris.nyc3.digitaloceanspaces.com/games/league-of-legend/launchhelper.sh)
    - [syscall_checker.sh](https://lutris.nyc3.digitaloceanspaces.com/games/league-of-legend/syscall_check.sh)
- Mark the launch helper and syscall checker scripts as executables (this is important, otherwise, you won't be able to launch LoL)
    - `chmod +x launchhelper.sh`
    - `chmod +x syscall_checker.sh` 
- Create a folder where you'll have your Wine prefix (**don't use an already existing Wine prefix. Create a _new_ empty folder**).  By default Lutris creates the Wine prefix in ~/Games/league-of-legends
    - If you have a Wine prefix that already has the game, you can avoid redownloading the entire game by moving/copying the `Riot Games` folder located in `(Wine prefix folder)/drive_c/Riot Games`.
- Move the two scripts to that empty folder. Your folder structure is like this:

```
- league-of-legends (or the folder that you created)
     - launchhelper.sh
     - syscall_checker.sh
```

- Go to Lutris, add a new game (top left corner) and set it up with the following details. After setting everything up, save the configuration

```
- Game info
    - Name: (whatever you want to call it)
    - Runner: Wine (Runs Windows games)
- Game options
    - Wine prefix: (path to your new folder)
    - Prefix architecture: 32-bit
- Runner options
    - Wine version: (choose the build of Wine that you installed. If you use the one I build, it's wine-615-lol)
    - Enable DXVK/VKD3D: enable it if your GPU supports it! (this requires that your GPU supports Vulkan. Lutris automatically enables it. **If you had it enabled before or never changed it, then enable it**)
    - Enable Esync: if you need it, enable it. In my case I don't need it.
    - Enable Fsync: if the Wine build that you're using and your kernel supports it, you can enable it. In my case I don't need it.
- System options
    - Enable Feral GameMode: enable it if you want
    - Enable NVIDIA Prime Render Offload: enable if if you want/need
    - Environment variables:
    While these are not strictly necessary, these are the ones that are automatically set up by the Lutris installer, so lets set them just in case
        - DXVK_LOG_LEVEL               | none
        - DXVK_STATE_CACHE_PATH        | (path to your new folder)
        - STAGING_SHARED_MEMORY        | 1
        - WINE_LARGE_ADDRESS_AWARE     | 1
        - __GL_SHADER_DISK_CACHE       | 1
        - __GL_SHADER_DISK_CACHE_PATH  | (path to your new folder)
    - Pre-launch script: (path to your new folder)/launchhelper.sh
        - You need to enable "Show advanced options" to see this
        - Example: /home/idkwuu/Games/league-of-legends/launchscript.sh
```

- Now select the game in Lutris. On the bottom of the window, there should be a Wine logo, and to the right of it, a menu. Open it and click on Run EXE inside Wine prefix. Select the League of Legends installer
- Wait a white for it to open. If it asks you to install Mono or Gecko, click Install. 
    - If the installer never opens, try this step again. 
- Now you should see the installer. 
    - If you backed up your Riot Games folder, now it's the time to copy it back. Copy the Riot Games folder to `(path to your new folder)/drive_c` 
- Click Install. Wait for it to installl/"repair". When the launcher opens, **DON'T LOG IN**: Just let it download the client/verify the files. 
- Once that is over, close the launcher. Open the menu next to the Wine logo again and click on Kill all Wine processes (to make sure the launcher is closed)
- Open the game through Lutris (click play or double click the game)
    - If you don't see the dialog about the abi.vsyscall32=0 sysctl config you either:
          - Set your system to always use that config. You can check if you have set it up by running `sysctl -n abi.vsyscall32` in the terminal. 
              - If if outputs 1, then you didn't set the script as executable, didn't add it to the config as the pre-launch script or set the path incorrectly there.
              - If it outputs 0, then you're good to go.
          - Didn't set the script as executable, didn't add it to the config as the pre-launch script or set the path incorrectly there.
- Now you can log in with your Riot account and open the game.

And we're done! We now should be able to play the game again.

If the game doesn't open, make sure (again) that you have your graphics drivers installed and that you had set everything up correctly. Also, make sure to check the [3a. Common issues](https://old.reddit.com/r/leagueoflinux/wiki/index#wiki_3a_-_common_issues) section in the r/leagueoflinux wiki.
