
# ![image](img/logo-sway.png) Sway 

## First steps

### Sway config file

``` bash
# Move sway template to $XDG_CONFIG_DIR/sway/config
cp -r /etc/sway/config ~/.config/sway/config
```

**Fix resolution and display configuration**

[how-to-setup-multiple-monitors-in-sway:](https://fedoramagazine.org/how-to-setup-multiple-monitors-in-sway/)

``` bash
# Get available displays 
swaymsg -t get_outputs

# Configures display 1 (HDMI-A-1) with a width of 1920 pixels to be on the left of display 2 (eDP-2)
# $XDG_CONFIG_DIR/sway/config:
# (...)
output HDMI-A-1 pos 0,0
output eDP-2 pos 1920 0
# (...)
```

**Fix keyboard layout:**

```bash
# documentation on how to configure inputs
man 5 sway-input

# get list of available inputs
swaymsg -t get_inputs

# modify sway config to change input behavior
vi ~/.config/sway/config

# enables us and de keyboard layouts, configures SUPER + Space as layout toggle
input "2821:6582:Asus_Keyboard" {
    xkb_layout us,de
    xkb_options grp:win_space_toggle
}
```

## Important keybindings

* https://depau.github.io/sway-cheatsheet/
* https://wiki.garudalinux.org/en/sway-cheatsheet

| Keybinding | Effect |
| ---------- | ------ |
| SUPER + SHIFT + c | Reload configuration |
| SUPER + SHIFT + q | Close current window |
| SUPER + d | Open [Rofi](https://github.com/davatorium/rofi) |

## Rofi

Rofi is fedora-sway-atomics version of the Gnome super key menu.

## Foot: Wayland Terminal Emulator

Copy foot.ini to $XDG_CONFIG_DIR:

``` bash
mkdir -p $HOME/.config/foot/
cp /etc/xdg/foot/foot.ini $HOME/.config/foot/ 
```

Change font size:

``` ini
# Uncomment and adjust
font=monospace:size=10
```

## zsh

oh-my-zsh:

``` bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
# in .config/foot/foot.ini:
shell=zsh
```

Powerlevel10k:

``` bash
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
echo 'source /var/home/niule/.oh-my-zsh/custom/themes/powerlevel10k/powerlevel10k.zsh-theme' >> .zshrc
```

Install font files:

``` bash
curl -Lo meslo_regular.ttf https://github.com/romkatv/powerlevel10k-media/raw/master/MesloLGS%20NF%20Regular.ttf
curl -Lo meslo_bold.ttf https://github.com/romkatv/powerlevel10k-media/raw/master/MesloLGS%20NF%20Bold.ttf
curl -Lo meslo_italic.ttf https://github.com/romkatv/powerlevel10k-media/raw/master/MesloLGS%20NF%20Italic.ttf
curl -Lo meslo_bold_italic.ttf https://github.com/romkatv/powerlevel10k-media/raw/master/MesloLGS%20NF%20Bold%20Italic.ttf

# https://docs.fedoraproject.org/en-US/quick-docs/fonts/#unpackaged
sudo mkdir /usr/local/share/fonts/meslo_nf
sudo mv meslo* /usr/local/share/fonts/meslo_nf
sudo chmod 644 /usr/local/share/fonts/meslo_nf/*
sudo chown -R root: /usr/local/share/fonts/meslo_nf
sudo restorecon -vFr /usr/local/share/fonts/meslo_nf
sudo fc-cache -v
```
