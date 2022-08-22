# MiSTer BGM

Background music player for the [MiSTer](https://github.com/MiSTer-devel/Main_MiSTer/wiki) menu.

![Control GUI](https://github.com/wizzomafizzo/MiSTer_BGM/raw/main/images/gui.png)

This script works well with the [Favorites](https://github.com/wizzomafizzo/MiSTer_Favorites) and [Games Menu](https://github.com/wizzomafizzo/MiSTer_GamesMenu) scripts.

## Features

* Play music in the main MiSTer menu, automatically stop and start music when a core is running.
* Play sounds when MiSTer first boots and when cores are launched.
* Support for most common music file formats including internet radio streams.
* Organise tracks into separate playlists.
* Multiple styles of playback and single track configuration.
* Play music while a core is running.
* Compatible with [MiSTer SAM](https://github.com/mrchrisster/MiSTer_SAM).

## Installation

1. Download and copy [bgm.sh](https://github.com/wizzomafizzo/MiSTer_BGM/raw/main/bgm.sh) to the `Scripts` folder on your SD card.
2. Run `bgm` from the `Scripts` section of the MiSTer menu.
3. Copy your music files to the newly created `music` folder on your SD card. *You can do this in advance by creating the music folder yourself.*
4. Reboot your MiSTer or re-run `bgm`.

### Updates

BGM can be automatically updated with the MiSTer downloader script (and update_all). Add the following text to the `downloader.ini` file on your SD card:

```
[bgm]
db_url = 'https://raw.githubusercontent.com/wizzomafizzo/MiSTer_BGM/main/bgm.json'
```

## Usage

Once installed, BGM will automatically start on MiSTer boot and randomly play any tracks in the `music` folder.

BGM will stop playing when a core is launched, and resume playing when you get back to the menu.

Launch `bgm` from the scripts menu to show the control GUI.

## Supported files

BGM supports playback of .mp3, .ogg, .wav, .mid and .vgm/.vgz files. These files can be used interchangeably in any playlist.

### Internet radio

Internet radio stations can be played using .pls files. The best way to manage these is by creating a new playlist folder, placing a single .pls file in that folder and playing it via the new playlist.

Multiple .pls files can be placed in a playlist (along with any other file), but they'll need to be manually skipped to move onto the next one.

## Controls

When the BGM service is running, launch the `bgm` script from the MiSTer Scripts menu to launch the control GUI. This GUI will give you basic playback functions, configuration options and the current playback status.

Changes made in the control GUI will also be written to the `bgm.ini` file and remembered between MiSTer boots.

## Playback types

Playback types can be configured in the control GUI or in the `bgm.ini` file.

By default, BGM will play the `random` playback type, which repeatedly picks a track at random to play.

An alternate playback type called `loop` can be used, which picks a random track to start, and then plays that same track on repeat until a reboot or core change.

The `disabled` playback type will stop tracks from playing completely, except for boot sounds.

## Playlists

Music files can be separated into playlists. Create a subfolder in the `music` directory and fill it with music files, it will now show up in the control GUI as a playlist. Playlists can contain any number and depth of subfolders if you want to organise tracks.

You can switch between playlists in the control GUI. As you switch, the current playlist will also be written to `bgm.ini`, so it will be started automatically next boot. Boot sounds are also taken from the current playlist.

The `none` playlist (the default) can be used to only use files from the top level of the `music` folder. Music files in the top level of the `music` folder and playlist subfolders will not conflict with each other.

The `all` playlist will play all files from every folder in the `music` folder.


## Boot sounds

Marking a music file as a boot sound will make BGM play it once when MiSTer starts up. This is intended for very short sound clips, like what you'd hear when booting up *\<your favourite console\>*.

Rename a music file with a `_` in front to make BGM play this file first on MiSTer start up (e.g. `_My File.mp3`). This can be done with multiple files to have it pick a random one each time. Boot sounds are picked from the active playlist and will be excluded from normal play.

### Global boot sounds

Boot sounds can be set to play no matter which playlist is active. To do this, create a new folder called `boot` in your `music` folder, and add your tracks here as normal.

These files will be included in the list of possible tracks selected to play on boot, as well as any boot sounds marked in your active playlist.

Global boot sounds do not need to be prefixed with a `_` character.

### Core boot sounds

Boot sounds can also be added which will play when a specific core is launched. Create a subfolder in the `boot` folder with its name matching the core and add your tracks here as normal.

When the core is launched, BGM will select a track from this folder to play once as the core is starting. For example, to play a boot sound when the SNES core is launched, create a folder called `SNES` in the `music/boot` folder and copy your tracks into it.

Core boot sounds do not need to be prefixed with a `_` character and are independent of all other boot sounds. **Note that core boot sounds will also trigger on .mgl file launches, as BGM cannot distinguish between those and a standalone core launch.**

A delay can be set before these boot sounds are triggered, to account for the time it takes for your monitor or TV to sync over HDMI. You can do this by adding the following line to your `bgm.ini` file:
```
corebootdelay = 0
```
And changing `0` to the number of seconds you want to delay the sound playing. This can be in increments of less than a second, just use a decimal number instead. Whenever you change this number in your ini file, you'll also have to either reboot your MiSTer or restart the BGM service before it takes effect.

## Per track looping

Individual music files can be configured to loop a certain number of times. If you have a short piece of background music from a game that you'd like to run longer, you can set it so that when that track starts playing it will loop a certain number of times before continuing to the next track.

You can do this be renaming the music file so it has `X##_` in front of the filename where `##` is the number of times it should loop with a leading zero. For example: `X05_My File.mp3` would loop it 5 times, while `X23_My File.mp3` would loop it 23 times.