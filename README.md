## My Mac Setup

This repo contains info on all the apps / tools / settings I use on my Mac.

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

- [What MacBook do I have?](#what-macbook-do-i-have)
- [Homebrew](#homebrew)
  - [Install Everything with Brewfile](#install-everything-with-brewfile)
- [Github](#github)
  - [Github SSH Setup](#github-ssh-setup)
- [OS Settings](#os-settings)
  - [Dock](#dock)
  - [Desktop & Stage Manager](#desktop--stage-manager)
  - [Widgets & Windows](#widgets--windows)
  - [Finder](#finder)
  - [Trackpad](#trackpad)
  - [Menu Bar](#menu-bar)
  - [Other System Settings (Manual)](#other-system-settings-manual)
- [Quick Launching](#quick-launching)
  - [RayCast](#raycast)
    - [RayCast Plugins](#raycast-plugins)
- [App Switching](#app-switching)
- [Menu Bar Utilities](#menu-bar-utilities)
  - [Hidden Bar](#hidden-bar)
- [Web Browsers](#web-browsers)
  - [Safari](#safari)
  - [Google Chrome](#google-chrome)
- [Apps I Use](#apps-i-use)
  - [Mac App Store Apps](#mac-app-store-apps)
- [Command Line Tools](#command-line-tools)
- [Fonts](#fonts)
- [Terminal](#terminal)
  - [Shell](#shell)
    - [Load dotfiles](#load-dotfiles)
- [Node.js](#nodejs)
  - [Global Modules](#global-modules)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## What MacBook do I have?

I am using a 2021 16" MacBook Pro

The specs:

- Apple M1 Max
- 64GB RAM
- 2TB SSD

Read more about my MacBook [here](https://everymac.com/systems/apple/macbook_pro/specs/macbook-pro-m1-max-10-core-cpu-24-core-gpu-16-2021-specs.html).

## Homebrew

[Homebrew](https://brew.sh/) allows us to install tools and apps from the command line.

To install it, open up the built in `Terminal` app and run this command:

```sh
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

This will also install the xcode build tools which is needed by many other developer tools.

### Install Everything with Brewfile

This repo includes a `Brewfile` that contains all CLI tools, GUI apps, fonts, and Mac App Store apps. Install everything in one command:

```sh
brew bundle --file=Brewfile
```

This replaces the need to install apps individually. See the [Brewfile](./Brewfile) for the full list.

> **Note:** Mac App Store apps require the `mas` CLI (included in the Brewfile) and you must be signed into the App Store first.

## Github

I like to setup github at this point so I can clone this repo to access the `Brewfile` for easy batch installs.

### Github SSH Setup

- Follow [this guide](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent) to setup an ssh key for github
- Follow [this guide](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account) to add the ssh key to your github account
- Follow [this guide](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/testing-your-ssh-connection) to test the ssh connection

## OS Settings

These are my preferred settings for `Desktop`, the `Dock` and `Finder`.

Most of these can be applied via `defaults write` commands instead of clicking through System Settings.

### Dock

I don't use the Dock at all. It takes up screen space, and I can use RayCast to launch apps and AltTab to switch between apps. I make the dock as small as possible and auto hide it.

```sh
# Small dock size
defaults write com.apple.dock tilesize -int 36
# Magnification off
defaults write com.apple.dock magnification -bool false
# Minimize windows into application icon
defaults write com.apple.dock minimize-to-application -bool true
# Auto-hide the Dock
defaults write com.apple.dock autohide -bool true
# Don't show suggested and recent apps
defaults write com.apple.dock show-recents -bool false
# Restart Dock to apply changes
killall Dock
```

### Desktop & Stage Manager

I don't like the new Desktop, Stage Manager or Widget features in Tahoe, so I disable them.

```sh
# Disable Stage Manager
defaults write com.apple.WindowManager GloballyEnabled -bool false
# Show Desktop -> only in Stage Manager on click
defaults write com.apple.WindowManager EnableStandardClickToShowDesktop -bool false
# Show windows from an application -> All at Once
defaults write com.apple.WindowManager AppWindowGroupingBehavior -bool true
```

### Widgets & Windows

```sh
# Show Widgets -> in Stage Manager only (not on Desktop)
defaults write com.apple.WindowManager StandardHideWidgets -bool true
```

### Finder

```sh
# Show all filename extensions
defaults write NSGlobalDomain AppleShowAllExtensions -bool true
# Disable warning before changing an extension
defaults write com.apple.finder FXEnableExtensionChangeWarning -bool false
# Search the current folder by default
defaults write com.apple.finder FXDefaultSearchScope -string "SCcf"
# New Finder windows show home folder
defaults write com.apple.finder NewWindowTarget -string "PfHm"
# Show path bar
defaults write com.apple.finder ShowPathbar -bool true
# Show status bar
defaults write com.apple.finder ShowStatusBar -bool true
# Show tab bar
defaults write com.apple.finder ShowTabView -bool true
# Hide all desktop icons
defaults write com.apple.finder ShowExternalHardDrivesOnDesktop -bool false
defaults write com.apple.finder ShowHardDrivesOnDesktop -bool false
defaults write com.apple.finder ShowMountedServersOnDesktop -bool false
defaults write com.apple.finder ShowRemovableMediaOnDesktop -bool false
# Restart Finder to apply changes
killall Finder
```

### Trackpad

```sh
# Disable natural scrolling
defaults write NSGlobalDomain com.apple.swipescrolldirection -bool false
```

### Menu Bar

```sh
# Show date always, hide day of week, show seconds
defaults write com.apple.menuextra.clock ShowDate -int 1
defaults write com.apple.menuextra.clock ShowDayOfWeek -bool false
defaults write com.apple.menuextra.clock ShowSeconds -bool true
defaults write com.apple.menuextra.clock FlashDateSeparators -bool false
killall SystemUIServer
```

### Other System Settings (Manual)

These settings don't have reliable `defaults write` equivalents:

- System Settings -> General -> AutoFill & Passwords -> AutoFill Passwords and Passkeys -> uncheck
- System Settings -> Control Center -> Spotlight -> Don't show in Menu Bar
- System Settings -> Control Center -> Siri -> Don't show in Menu Bar

## Quick Launching

### RayCast

The built in spotlight search is a bit slow for me and usually has web search results as the default instead of apps or folders on my machine.

I use [RayCast](https://www.raycast.com/) (included in Brewfile).

#### RayCast Plugins

- [1Password](https://www.raycast.com/khasbilegt/1password)
- [iMessage 2FA](https://www.raycast.com/yuercl/imessage-2fa)
- [RayCast Homebrew Plugin](https://www.raycast.com/nhojb/brew) so we can easily install formulae and casks directly from RayCast.

## App Switching

The built in App switcher only shows application icons, and only shows 1 icon per app regardless of how many windows you have open in that app.

I use an app switcher called [AltTab](https://alt-tab-macos.netlify.app/) (included in Brewfile). It shows full window previews, and has an option to show a preview for every open window in all applications (even minimized ones).

I replace the built-in `CMD+TAB` shortcut with AltTab.

## Menu Bar Utilities

### Hidden Bar

If you have several apps running that have menu bar icons, [Hidden Bar](https://github.com/dwarvesf/hidden) (included in Brewfile) will let you choose which ones should be hidden. This cleans things up if you have a ton of background apps running.

## Web Browsers

### Safari

I use safari for my everyday browsing life.

### Google Chrome

I use Google Chrome for my work and local development previews.

## Apps I Use

All of the following are installed via the `Brewfile` with `brew bundle`:

- [1password-cli](https://1password.com/) - 1Password command-line tool
- [claude-code](https://claude.ai/code) - AI coding assistant
- [cleanshot](https://cleanshot.com/) - Screenshot tool
- [finetune](https://finetune.dev/) - Claude Code desktop client
- [discord](https://discord.com/) - Messaging / Community
- [karabiner-elements](https://karabiner-elements.pqrs.org/) - Keyboard customization
- [launchos](https://launchos.app/) - macOS setup automation
- [notion](https://www.notion.so/) - Notes / Project management
- [obs](https://obsproject.com/) - Streaming / Recording
- [obsidian](https://obsidian.md/) - Note taking
- [pearcleaner](https://itsalin.com/appInfo/?id=pearcleaner) - App uninstaller
- [screen-studio](https://www.screen.studio/) - Screen recording
- [slack](https://slack.com/) - Messaging
- [spotify](https://www.spotify.com/) - Music streaming
- [visual-studio-code](https://code.visualstudio.com/) - Code Editor
- [wispr-flow](https://wispr.com/) - Voice-to-text dictation
- [zoom](https://zoom.us/) - Video conferencing

### Mac App Store Apps

These are installed via `mas` in the Brewfile:

- 1Password for Safari
- Final Cut Pro
- Keynote
- Numbers
- Pixelmator Pro
- Speedtest

## Command Line Tools

All installed via the `Brewfile`:

- [eza](https://eza.rocks/) - Modern replacement for `ls`
- [gh](https://cli.github.com/) - GitHub CLI
- [lazygit](https://github.com/jesseduffield/lazygit) - Terminal UI for git
- [mole](https://github.com/nicnocquee/mole) - Local dev environment manager
- [rulesync](https://github.com/nicnocquee/rulesync) - Sync AI coding rules across projects
- [pnpm](https://pnpm.io/) - Fast package manager
- [starship](https://starship.rs/) - Cross-shell prompt
- [stow](https://www.gnu.org/software/stow/) - Symlink manager for dotfiles
- [thefuck](https://github.com/nvbn/thefuck) - Corrects previous console command
- [zoxide](https://github.com/ajeetdsouza/zoxide) - Smarter `cd` command
- [zsh-autosuggestions](https://github.com/zsh-users/zsh-autosuggestions) - Fish-like suggestions for zsh
- [zsh-syntax-highlighting](https://github.com/zsh-users/zsh-syntax-highlighting) - Syntax highlighting for zsh

## Fonts

Installed via the `Brewfile`:

- [Anonymous Pro](https://www.marksimonson.com/fonts/view/anonymous-pro)
- [Geist](https://vercel.com/font) - Vercel's sans-serif font
- [Geist Mono](https://vercel.com/font) - Vercel's monospace font
- [Meslo LG Nerd Font](https://github.com/ryanoasis/nerd-fonts/tree/master/patched-fonts/Meslo)
- [Reenie Beanie](https://fonts.google.com/specimen/Reenie+Beanie) - Handwritten font

## Terminal

I prefer [Ghostty](https://ghostty.org/) (included in Brewfile).

### Shell

#### Load dotfiles

All my dotfiles are stored on [github](https://github.com/chris-nowicki/dotfiles).

I clone this repo to my machine and copy the files into my home directory.

## Node.js

I use nvm to manage the installed versions of Node.js on my machine. This allows me to easily switch between Node.js versions depending on the project I'm working in.

See installation instructions [here](https://github.com/nvm-sh/nvm#installing-and-updating).

OR run this command:

```sh
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash
```

Now that nvm is installed, you can install a specific version of node.js and use it:

```sh
nvm install 20
nvm use 20
node --version
```

### Global Modules

There are a few global node modules I use a lot:

- [npm-check-updates](https://www.npmjs.com/package/npm-check-updates)

```sh
npm install -g npm-check-updates
```
