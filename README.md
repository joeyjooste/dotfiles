# My dotfiles

This is a repo containing all of my dotfiles (Files in linux that start with a . such as .zshrc).

These files are usually configuration files for my applications and system.

## Requirements

Ensure you have the following installed on your system

### Git

```
pacman -S git
```

### Stow

```
pacman -S stow
```

### Zellij

``` 
pacman -S zellij
```

### Zsh

```
pacman -S zsh
```

## Installation

Step 1 is to add the dotfiles repo to your $HOME directory 

```
$ git clone git@github.com/FrikkyWasTaken/dotfiles.git
$ cd dotfiles
```

Then use GNU Stow to create symlinks

```
$ stow .
```

## Adding your own Dot files to the repo

### Fork the repo on github

Fork the Repo by clicking the fork button on github

Now follow the [Installation](##Installation) but change the git URL to that of your own repo

### Add your own dotfiles

Keep the directory structure the same and move your dotfiles into the ~/dotfiles directory

Now push it to your git repo

In your ~/dotfiles directory run:

```
$ git add .
$ git commit -m "Added X dotfiles"
$ git push origin main
```

Now add the sym links to your dotfiles (CAREFUL)

```
stow --override .
```

NOTE: This command overwrites the existing dotfiles on your system, use with caution.


## How to setup your own dotfiles repo

[Setup GNU Stow and your very own dotfiles Repo](https://youtu.be/y6XCebnB9gs?si=k3jpqGTt3HtZgFtv)


# Trassition to Void
I'm moving my dotfiles across to a suckless and linux void setup, below is documentation that I'm finding along the way.

### Sym linking flatpaks
This allows them to be opened by dmenu
```
sudo ln -s /var/lib/flatpak/exports/bin/chat.rocket.RocketChat /usr/bin/rocket-chat
```

### Dependancys for picom (FT labs fork)
```
sudo xbps-install -S meson ninja cmake libev-devel xcb-util-renderutil-devel xcb-util-image-devel pixman-devel pkgconf-devel uthash pcre-devel dbus-devel glu-devel libconfig-devel
```

### Install from scratch
Install using void-installer
Confirm network is working (WPA supplicant for wifi and dhcpcd for ethernet)

- Update your system to mirror 
```
sudo xbps-install -Su
```
- Install basic packages
```
sudo xbps-install -S helix xorg xinit git make base-devel libX11-devel libXft-devel libXinerama-devel freetype-devel fontconfig-devel firefox
```
- Make directories for suckless
```
mkdir .config
```
```
cd .config
```
```
mkdir suckless
```
```
cd suckless
```
- Clone my/your DWM repo
```
git clone https://github.com/joeyjooste/dwm
```
- The same for ST, dmenu, and slstatus
```
git clone https://github.com/joeyjooste/dmenu
```
```
git clone https://github.com/joeyjooste/slstatus
```
- ST carries a dependancy of harfbuzz-devel
```
sudo xbps-install -S harfbuzz-devel
```
```
git clone https://github.com/joeyjooste/st
```
- Now compile them all
```
cd dwm 
```
```
sudo make clean install
```
- Repeat for all other suckless software
- Now start dwm
```
startx /usr/local/bin/dwm
```
Press mod+shift+enter to open a terminal (mod is alt by default, it is windows key in my config)
- Launch firefox with the following command
```
firefox
```
Head to [Nerd Fonts](https://www.nerdfonts.com/font-downloads)
Download a nerdfont of your choice (I use jetbrainsmono)

- Inside of your downloads folder run the following
```
sudo mv JetBrainsMono.zip /usr/share/fonts/TTF
```
Use tab to complete the name of your zip.

- Then cd into the TTF folder
```
cd /usr/share/fonts/TTF
```
```
sudo unzip JetBrainsMono.zip
```
Now reload DWM to see it apply, (make sure the font is correctly enabled inside of your dwm config) I have reload bound to Mod+crtl+shift+q if you are using my dwm config.
