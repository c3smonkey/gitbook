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

<pre class="language-bash" data-line-numbers><code class="lang-bash"><strong># global settings
</strong>yabai -m config mouse_follows_focus          off
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
yabai -m rule --add app="Raycast" manage=off
yabai -m rule --add app="^Music$" manage=off
#yabai -m rule --add app="^IntelliJ IDEA$" manage=off
yabai -m rule --add app="Toolbox$" manage=off
#yabai -m rule --add app="Android Studio$" manage=off
yabai -m rule --add app="^1Password 7$" manage=off

echo "yabai configuration loaded.."


</code></pre>



### skhdrc

#### Change Focus

{% code fullWidth="false" %}
```bash
~/.config/skhd/skhdrc

# -- Changing Window Focus --
# change window focus within space
alt - j : yabai -m window --focus south
alt - k : yabai -m window --focus north
alt - h : yabai -m window --focus west
alt - l : yabai -m window --focus east

# change window focus cycle forwards
ctrl + alt - n : yabai -m window --focus next || yabai -m window --focus first
# change window focus cycle backwards
shift + ctrl + alt - n : yabai -m window --focus prev || yabai -m window --focus last
```
{% endcode %}

#### Change Layout

{% code fullWidth="false" %}
```bash
~/.config/skhd/skhdrc

# -- Modifying the Layout --
# rotate windows clockwise / anticlockwise
alt - r         : yabai -m space --rotate 270
shift + alt - r : yabai -m space --rotate 90

# flip along y-axis
alt - y : yabai -m space --mirror y-axis

# flip along x-axis
alt - x : yabai -m space --mirror x-axis

# toggle window float
alt - t : yabai -m window --toggle float --grid 4:4:1:1:20:20

# toggle padding and gap
alt - g : yabai -m space --toggle padding; yabai -m space --toggle gap

# maximize a window
alt - m : yabai -m window --toggle zoom-fullscreen

# balance out tree of windows (resize to occupy same area)
 alt - b : yabai -m space --balance
```
{% endcode %}

#### Change Size

{% code fullWidth="false" %}
```bash
~/.config/skhd/skhdrc

# -- Modifying Window Size --
# change window sizes
shift + ctrl + alt - h : yabai -m window --resize left:-20:0 ; yabai -m window --resize right:-20:0
shift + ctrl + alt - j : yabai -m window --resize bottom:0:20 ; yabai -m window --resize top:0:20
shift + ctrl + alt - k : yabai -m window --resize top:0:-20 ; yabai -m window --resize bottom:0:-20
shift + ctrl + alt - l : yabai -m window --resize right:20:0 ; yabai -m window --resize left:20:0

```
{% endcode %}

#### Move Window

{% code fullWidth="false" %}
```bash
~/.config/skhd/skhdrc

# -- Moving Windows Around --
# swap windows
shift + alt - j : yabai -m window --swap south
shift + alt - k : yabai -m window --swap north
shift + alt - h : yabai -m window --swap west
shift + alt - l : yabai -m window --swap east

# move window and split
ctrl + alt - j : yabai -m window --warp south
ctrl + alt - k : yabai -m window --warp north
ctrl + alt - h : yabai -m window --warp west
ctrl + alt - l : yabai -m window --warp east

# move window to prev and next space
shift + alt - p : yabai -m window --space prev;
shift + alt - n : yabai -m window --space next;

# move window to space #
shift + alt - 1 : yabai -m window --space 1;
shift + alt - 2 : yabai -m window --space 2;
shift + alt - 3 : yabai -m window --space 3;
shift + alt - 4 : yabai -m window --space 4;
shift + alt - 5 : yabai -m window --space 5;
shift + alt - 6 : yabai -m window --space 6;
shift + alt - 7 : yabai -m window --space 7;

# swap managed window
shift + alt - j : yabai -m window --swap south
shift + alt - k : yabai -m window --swap north
shift + alt - h : yabai -m window --swap west
shift + alt - l : yabai -m window --swap east

# move window to display left and right
shift + alt - s : yabai -m window --display west; yabai -m display --focus west;
shift + alt - g : yabai -m window --display east; yabai -m display --focus east;

```
{% endcode %}

#### Start- Stop and Restart yabai

{% code fullWidth="false" %}
```bash
~/.config/skhd/skhdrc

# -- Starting/Stopping/Restarting Yabai --
# stop/start/restart yabai
ctrl + alt - q : yabai --stop-service
ctrl + alt - s : yabai --start-service
ctrl + alt - r : yabai --restart-service
```
{% endcode %}

#### OSX Hacks

<pre class="language-bash" data-full-width="false"><code class="lang-bash"><strong>~/.config/skhd/skhdrc
</strong><strong>
</strong><strong># -- osx hacks --
</strong># disable osx hide window
cmd - h : :
# disable osx minimize window
alt + cmd - m : :
cmd - m : :
</code></pre>
