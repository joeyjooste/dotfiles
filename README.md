# My dotfiles

This is a repo containing all of my dotfiles (Files in linux that start with a . such as .zshrc).

These files are usually configuration files for my applications and system.

## The Stack
- Distro: Void
- WM: [DWM](https://github.com/joeyjooste/dwm)
- Term: [ST](https://github.com/joeyjooste/st)
- Launcher: [DMENU](https://github.com/joeyjooste/dmenu)
- Bar: [slstatus](https://github.com/joeyjooste/slstatus)
- Apps: Flatpak


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


# Noob install guide (for me)
I'm moving my dotfiles across to a suckless and linux void setup, below is documentation that I'm finding along the way.


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
sudo xbps-install -S helix xorg xinit git make base-devel libX11-devel libXft-devel libXinerama-devel freetype-devel fontconfig-devel firefox neofetch zellij stow zsh starship yazi xwallpaper
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

- Create xinitrc file
```
hx .xinitrc
```
- Now inside of that file add these lines
```
slstatus &
xwallpaper --zoom ~/Wallpaper/gruvboxLady.png &
exec dbus-run-session dwm
```
- Install flatpak to manage proprietary applications
https://flatpak.org/setup/Void%20Linux

Note: Run the last command that ads the origin, which sudo otherwise it gives a system bus error

For every installed flatpak application, run this command to allow dmenu to open it through a symlink
```
sudo ln -s /var/lib/flatpak/exports/bin/chat.rocket.RocketChat /usr/bin/rocket-chat
```

- Theme firefox with your desired theme, I use the theme below
https://github.com/vinceliuice/WhiteSur-firefox-theme.git

- Change default terminal to zsh
```
chsh -s /usr/bin/zsh
```
restart your system to enable the new shell

- Now clone this dotfiles repo
```
git clone https://github.com/joeyjooste/dotfiles
```
```
stow .
```
If you have any existing config files that are conflicting, just go through and remove them and run "stow ." again.
- Firefox MP4
I needed the ffmpeg-devel package to enable mp4 in firefox videos.

- Install pulseaudio
```
sudo xbps-install -S pulseaudio
```
```
sudo xbps-install -S pasystray
```
- Install npm and node
```
sudo xbps-install -S nodejs
```
- Helix Language Servers
These are for my config, adjust as needed based on your config.
```
cargo install --git https://github.com/estin/simple-completion-language-server.git
```
```
npm i -g typescript-language-server typescript @tailwindcss/language-server prettier vscode-langservers-extracted
```


### Tweaks
- Disable Mouse Acceleration
https://wiki.archlinux.org/title/Mouse_acceleration
- Enable Rich Presence in flatpak version of discord
https://github.com/flathub/com.discordapp.Discord/wiki/Rich-Precense-(discord-rpc)
- Setup github SSH key and config flags
  Generate Key, Set key in SSH file, copy pub key to github, Create SSH config file that points to key, change any git url's to use SSH

### Todo
Auto Startx
Fix colours on bar
Add screenshot tool + keybinds
