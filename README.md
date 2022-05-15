# Spotify Polybar

Module for polybar to display spotify song status using playerctl

Inspired by [PrayagS polybar-spotify module](https://github.com/PrayagS/polybar-spotify)
## Dependencies
- Music player supported by [Playerctl](https://github.com/altdesktop/playerctl/#selecting-players-to-control)
- [Zscroll](https://github.com/noctuid/zscroll)

## Configuration

You can modify some variable in `spotify.sh`

```sh
# Set the source audio player here.
# Examples: spotify, vlc, chrome, mpv and others.
# See more here: https://github.com/altdesktop/playerctl/#selecting-players-to-control
readonly PLAYER="spotifyd"

# Delay (in seconds) for scrolling update
# lower this for faster scrolling
readonly ZSCROLL_DELAY="0.1"

# Time in seconds to wait in between running update checking commands
# Make also a "pause" in scroll but its just due by playerctl hang time to get informations
readonly ZSCROLL_UPDATE_DELAY="2"

# if display text lenght > number the text is going to scroll
readonly ZSCROLL_LENGTH="20"
```

## Usage

The script expects parameters :
 - `--get-infos` : Get the song name if playing or return No playing song / Paused
 - `--get-status` : Get the current status of player like Playing | Stopped | Paused but return icon
 - `--scroll` : Display the song metadata with zscroll to get scrolling text
 - `--play-pause` : Execute play or pause command (depend on playerctl status)
 - `--next` : Execute next command
 - `--previous` : Execute previous command


Example module for polybar

```ini
[module/spotify-title]
type = custom/script
tail = true
format-prefix = " "
format-prefix-font = 5
interval = 2
exec = ~/.config/polybar/scripts/spotify.sh --scroll
click-left = kitty spt
click-right = playerctl --player=spotifyd metadata --format "{{ xesam:url }}" | xclip -selection clipboard

[module/spotify-prev]
type = custom/text
content = ""
content-padding = 0
content-spacing = 0
content-margin = 0
click-left = ~/.config/polybar/scripts/spotify.sh --previous


[module/spotify-next]
type = custom/text
content = ""
content-padding = 0
content-spacing = 0
content-margin = 0
click-left = ~/.config/polybar/scripts/spotify.sh --next


[module/spotify-playpause]
type = custom/text
content = ""
content-padding = 0
content-spacing = 0
content-margin = 0
click-left = ~/.config/polybar/scripts/spotify.sh --play-pause
```

## Demo
![Demo gif](./.assets/demo.gif)