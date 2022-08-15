![](screenshots/bar-only.png)
# Mokujin Polybar Theme
A theme for [Polybar](https://github.com/polybar/polybar) based on the Mokujin colorway

![](https://img.shields.io/badge/Version-0.97-green) ![](https://img.shields.io/badge/License-GPLv3-yellowgreen) ![](https://img.shields.io/badge/Polybar-3.6.3%2B-blue)

## Features
- Pleasant, earthy, minimalist design
- Single ini file using inline shell scripts
- User configuration section
- Day/Night weather conditions & current temp
- OpenHAB weather integration support
- Japanese day of the week
- Package manager update notification (pacman and apt)
- Bluetooth power button and management
- Wireless gamepad battery indicator
- System battery indicator
- Volume control
- Screen brightness control
- CPU & RAM utilization indicators
- MPD control + current track
- Workspace control
- Error notifications (via libnotify)

## Screenshots
![](screenshots/screenshot-2.png)<sub>wallpaper credit: Dani Pendergast (www.danipendergast.com)</sub>
![](screenshots/screenshot-1.png)<sub>wallpaper credit: OpenAI DALL-E 2</sub>


## Requirements
Requirements have been kept as minimal as possible.  Mostly they are pretty standard utilities, even for minimalist desktop systems.  Shell scripting is bash, but hopefully works for other shells.  All script utilities and fonts are free and available in Arch repos and AUR.

- **Polybar 3.6.3+** 
- **Noto CJK fonts**
- **mononoki Nerd Fonts** or **Nerd Fonts Complete**
- **pulseaudio** or **pipewire-pulse**
- **bash** (or compatible)
- **date**
- **bc**
- **curl** (weather)
- **jq** (weather)
- **checkupdates** (Arch / pacman-based distros) (optional)
- **apt-get** (Debian / apt-based distros - see notes)  (optional)
- **bluetoothctl** (optional)
- **notify-send** (optional)
- **mpd** (optional)
- Gamepad driver that creates a sysfs node for capacity in percentage
- OpenWeatherMap API key (free) or OpenHAB server configured to provide OWM data.

## Installation
### Fonts
For arch users the noto fonts can be found in **extra** and the Nerd Fonts can be found in **aur**.

```
pacman -S noto-fonts-cjk
yay -S nerd-fonts-complete
```

### Theme file
The theme is contained in a single file, so you can just drop mokujin.ini where you want and tell polybar to use it.

### Other dependencies
Assuming you already have a basic running system with audio and optionally MPD set up, you *might* need one or more of these packages installed.

Arch users
```
pacman -S bc curl jq pacman-contrib bluez-utils 
```

## Configuration
You're going to need to configure a few things first.  I've created a section at the top of the ini file for user configuration so you shouldn't have to hunt throught the rest of it to get going.

The user configuration is friendly and well documented inside the mokujin.ini file and should hopefully make everything pretty clear.

For polybar options like MPD configuration, you can find the documentation [here](https://github.com/polybar/polybar/wiki)

You're also going to want to use the weather modules, in which case you need an API key.  You can get a **free** OpenWeatherMap API key [here](https://openweathermap.org/appid). 

Side note:  I'm a big privacy advocate, so I want to mention that I've never given OWM any data other than a junk email address and I've never been contacted in any way other than to email me the API key.  I've had my key for *years* and no one has ever bugged me and I've never had to log into the website, even for API documentation.


## Troubleshooting
If you're experiencing text rendering issues, make sure the necessary font packages in the requirements section are installed and update your font cache with `fc-cache -f`.  You will probably need to restart polybar afterwards.


## Note for Debain / apt distro users
Unfortunately there is no equivalent of the pacman **checkupdates** utility for **apt**.  Simply, **apt** will not allow you to compare or even read the package lists as a non-root user, which means we cannot use it to check the repos for package changes.

This script does, however, rootlessly do a *dry run* on an **apt-get upgrade** to see if anything *would* be upgraded.  Which, of course, doesn't do much by itself if the local package lists are not up-to-date with the repos.

To make this work, you can create a **cron job** which will run `apt-get update` once a day as root.  This will not upgrade anything, but will keep the local package list more or less synced and up-to-date with the repos.  With that in place, the script can check the local package lists for upgradable packages and provide a notification if there are any.


## Contributing
If you find a bug, or would like to see a feature implemented, please create an issue and I'll take a look.  Or, if you prefer to just submit a PR, thats fine too.  

I need users to provide sysfs device paths for whatever gamepads they may have which create a directory in `/sys/class/power_supply/`.  I'm looking for files within these paths which provide battery levels.  Open a support issue if you'd like to help with information about your gamepad.

As always, you can buy me a coffee if you find this software useful and want to say thanks ;)


## License
This software is licensed under the GNU Affero General Public License v3+

