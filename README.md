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

## How to setup your own dotfiles repo

https://youtu.be/y6XCebnB9gs?si=k3jpqGTt3HtZgFtv
