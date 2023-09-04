---
description: '- yabai & skhd -'
---

# window management & simple hotkey daemon

## Brew install

```bash
brew install koekeishiya/formulae/skhd
brew install koekeishiya/formulae/yabai
```

## Config files

```bash
~/.config/yabai/yabairc
~/.config/skhd/skhdrc
```

### yabairc

{% code lineNumbers="true" %}
```bash
#!/usr/bin/env sh

# global settings
yabai -m config mouse_follows_focus          on
yabai -m config focus_follows_mouse          off
yabai -m config window_origin_display        default
yabai -m config window_placement             second_child
yabai -m config window_topmost               off
yabai -m config window_shadow                on
yabai -m config window_opacity               off
yabai -m config window_opacity_duration      0.0
yabai -m config active_window_opacity        1.0
yabai -m config normal_window_opacity        0.90
yabai -m config window_border                on
yabai -m config window_border_width          2
# https://convertingcolors.com/hex-color-FF00FF.html?search=Hex(FF00FF)
yabai -m config active_window_border_color   0xFF39FF14
#yabai -m config active_window_border_color   0xFF91BAF8
yabai -m config normal_window_border_color   0xff555555
yabai -m config insert_feedback_color        0xffd75f5f
yabai -m config split_ratio                  0.50
yabai -m config auto_balance                 off
yabai -m config mouse_modifier               fn
yabai -m config mouse_action1                move
yabai -m config mouse_action2                resize
yabai -m config mouse_drop_action            swap

# general space settings
yabai -m config layout                       bsp
yabai -m config top_padding                  15
yabai -m config bottom_padding               15
yabai -m config left_padding                 15
# NOTE: for OBS floating head
# yabai -m config left_padding                 450
yabai -m config right_padding                15
yabai -m config window_gap                   15

# apps to not manage (ignore)
yabai -m rule --add app="^Finder$" manage=off
yabai -m rule --add app="^System Settings$" manage=off
yabai -m rule --add app="^Archive Utility$" manage=off
yabai -m rule --add app="^Logi Options$" manage=off
yabai -m rule --add app="Raycast" manage=off
yabai -m rule --add app="^Music$" manage=off
yabai -m rule --add app="^IntelliJ IDEA$" manage=off
yabai -m rule --add app="Toolbox$" manage=off
yabai -m rule --add app="Android Studio$" manage=off
yabai -m rule --add app="^1Password 7$" manage=off
yabai -m rule --add app="^Messages$" manage=off
yabai -m rule --add app="^Finder$" manage=off

echo "yabai configuration loaded.."
```
{% endcode %}



### skhdrc

#### Launch Commands

{% code fullWidth="false" %}
```bash
# === Launch Commands ===
# Start IntelliJ IDEA Ultimate
cmd + shift - i : osascript -e "tell application \"/Users/$USER/Applications/IntelliJ IDEA Ultimate.app\" to activate"
# Start Safari
cmd + shift - s : osascript -e "tell application \"Safari\" to activate"
# Start Warp
cmd + shift - w : osascript -e "tell application \"Warp\" to activate"
```
{% endcode %}

#### Navigation

{% code fullWidth="false" %}
```bash
# === Navigation ===
# move window to space #
ctrl + alt - 1 : yabai -m window --space 1
ctrl + alt - 2 : yabai -m window --space 2
ctrl + alt - 3 : yabai -m window --space 3
ctrl + alt - 4 : yabai -m window --space 4
ctrl + alt - 5 : yabai -m window --space 5
ctrl + alt - 6 : yabai -m window --space 6
ctrl + alt - 7 : yabai -m window --space 7
ctrl + alt - 8 : yabai -m window --space 8
ctrl + alt - 9 : yabai -m window --space 9
ctrl + alt - 0 : yabai -m window --space 10
# move window to prev and next space
ctrl + alt - p : yabai -m window --space prev;
ctrl + alt - n : yabai -m window --space next;

# change window focus within space
cmd - h : yabai -m window --focus west
cmd - j : yabai -m window --focus south
cmd - k : yabai -m window --focus north
cmd - l : yabai -m window --focus east
# support also arrows
cmd - left : yabai -m window --focus west
cmd - down : yabai -m window --focus south
cmd - up : yabai -m window --focus north
cmd - right : yabai -m window --focus east



```
{% endcode %}

#### Moving Windows Around

{% code fullWidth="false" %}
```bash
# -- Moving Windows Around --
# swap windows
shift + cmd - j : yabai -m window --swap south
shift + cmd - k : yabai -m window --swap north
shift + cmd - h : yabai -m window --swap west
shift + cmd - l : yabai -m window --swap east

# move window and split
ctrl + cmd - j : yabai -m window --warp south
ctrl + cmd - k : yabai -m window --warp north
ctrl + cmd - h : yabai -m window --warp west
ctrl + cmd - l : yabai -m window --warp east
```
{% endcode %}

#### Modifying  Window

{% code fullWidth="false" %}
```bash
# -- Modifying the Layout --
# rotate windows clockwise / anticlockwise
alt - r         : yabai -m space --rotate 270
shift + alt - r : yabai -m space --rotate 90

# rotate on X and Y axis
alt - x : yabai -m space --mirror x-axis
alt - y : yabai -m space --mirror y-axis

# toggle window float
alt - t : yabai -m window --toggle float --grid 4:4:1:1:20:20

# toggle padding and gap
alt - g : yabai -m space --toggle padding; yabai -m space --toggle gap

# maximize a window
alt - m : yabai -m window --toggle zoom-fullscreen

# balance out tree of windows (resize to occupy same area)
alt - b : yabai -m space --balance

# balance out tree of windows (resize to occupy same area)
alt - b : yabai -m space --balance 

# set insertion point for focused container
shift + ctrl + alt - h : yabai -m window --insert west
shift + ctrl + alt - j : yabai -m window --insert south
shift + ctrl + alt - k : yabai -m window --insert north
shift + ctrl + alt - l : yabai -m window --insert east

# change window sizes and border color
# define border color 
:: resize @ : yabai -m config active_window_border_color 0xFFFF00FF
#:: default : yabai -m config active_window_border_color 0xFF91BAF8
:: default : yabai -m config active_window_border_color  0xFF39FF14
# toggle mode 
resize < hyper - r ; default
default < hyper - r ; resize
# change wind:w
# ow size
resize < h : yabai -m window --resize left:-50:0; yabai -m window --resize right:-50:0
resize < j : yabai -m window --resize bottom:0:50; yabai -m window --resize top:0:50
resize < k   : yabai -m window --resize top:0:-50; yabai -m window --resize bottom:0:-50
resize < l : yabai -m window --resize right:50:0; yabai -m window --resize left:50:0
# support also arrows
resize < left : yabai -m window --resize left:-50:0; yabai -m window --resize right:-50:0
resize < down : yabai -m window --resize bottom:0:50; yabai -m window --resize top:0:50
resize < up   : yabai -m window --resize top:0:-50; yabai -m window --resize bottom:0:-50
resize < right : yabai -m window --resize right:50:0; yabai -m window --resize left:50:0
```
{% endcode %}

#### Manage yabai & skhd

{% code fullWidth="false" %}
```bash
# -- Manage yabai and skhd --
# stop/start/restart yabai
ctrl + alt - q : yabai --stop-service
ctrl + alt - s : yabai --start-service
ctrl + alt - r : yabai --restart-service
# Reload skhd configuration
shift + cmd - r : skhd --reload

```
{% endcode %}

#### Disable OSX built-in mappings

{% code fullWidth="false" %}
```bash
# -- disable some OSX built-in key mappings --
# disable osx hide window
cmd - h : :
# disable osx minimize window
alt + cmd - m : :
cmd - m : :
```
{% endcode %}

