# Mac Useful Commands

A collection of little code snippets or tutorials to get the most out of your mac or out of a certain situation.

## How to enable the root user on your Mac

1. Choose Apple menu () > System Preferences, then click Users & Groups (or Accounts).
2. Click <img src="https://support.apple.com/library/content/dam/edam/applecare/images/en_US/il/elcapitan-lock-inline.png" width="14">, then enter an administrator name and password.
3. Click Login Options.
4. Click Join (or Edit).
5. Click Open Directory Utility.
6. Click <img src="https://support.apple.com/library/content/dam/edam/applecare/images/en_US/il/elcapitan-lock-inline.png" width="14"> in the Directory Utility window, then enter an administrator name and password.
7. From the menu bar in Directory Utility:
   - Choose Edit > Enable Root User, then enter the password that you want to use for the root user.
   - Or choose Edit > Disable Root User.

With pictures: https://coolestguidesontheplanet.com/enable-root-user-macos-sierra

---

## Random Stuff

### Flush Cache & Clear DNS

- `sudo killall -HUP mDNSResponder`

### Reset Audio

- `sudo killall coreaudiod`

### Disable Gatekeeper

- `sudo spctl --master-disable`
- `sudo defaults write /Library/Preferences/com.apple.security GKAutoRearm -bool NO`

## Show/Hide Hidden Files

- `defaults write com.apple.finder AppleShowAllFiles NO`
- `defaults write com.apple.finder AppleShowAllFiles YES`
- `killall Finder`

### Remove .DS_Store files recursively from terminal

`find . -name ‘*.DS_Store’ -type f -delete`

---

### Disable macOS user interface Animations

1. Disable animations when opening and closing windows.
2. Disable animations when opening a Quick Look window.
3. Accelerated playback when adjusting the window size (Cocoa applications).
4. Disable animation when opening the Info window in Finder (cmd⌘ + i).
5. Disable animations when you open an application from the Dock.
6. Make all animations faster that are used by Mission Control.
7. Disable the delay when you hide the Dock.

```
defaults write NSGlobalDomain NSAutomaticWindowAnimationsEnabled -bool false
defaults write -g QLPanelAnimationDuration -float 0
defaults write NSGlobalDomain NSWindowResizeTime -float 0.001
defaults write com.apple.finder DisableAllAnimations -bool true
defaults write com.apple.dock launchanim -bool false
defaults write com.apple.dock expose-animation-duration -float 0.1
defaults write com.apple.Dock autohide-delay -float 0
```

### Disable opening and closing window animations
`defaults write NSGlobalDomain NSAutomaticWindowAnimationsEnabled -bool false`
`killall SystemUIServer`

### Expand save panel by default
`defaults write NSGlobalDomain NSNavPanelExpandedStateForSaveMode -bool true`

### Expand print panel by default
`defaults write NSGlobalDomain PMPrintingExpandedStateForPrint -bool true`

### Save to disk (not to iCloud) by default
`defaults write NSGlobalDomain NSDocumentSaveNewDocumentsToCloud -bool true`

### Automatically quit printer app once the print jobs complete
`defaults write com.apple.print.PrintingPrefs "Quit When Finished" -bool true`

### Disable the “Are you sure you want to open this application?” dialog
`defaults write com.apple.LaunchServices LSQuarantine -bool false`

### Disable Resume system-wide
`defaults write NSGlobalDomain NSQuitAlwaysKeepsWindows -bool false`

### Check for software updates daily, not just once per week
`defaults write com.apple.SoftwareUpdate ScheduleFrequency -int 1`

### Increase sound quality for Bluetooth headphones/headsets
`defaults write com.apple.BluetoothAudioAgent "Apple Bitpool Min (editable)" -int 40`

### Enable subpixel font rendering on non-Apple LCDs
### https://www.unixinfo.nl/osx-change-font-smoothing
`defaults write NSGlobalDomain AppleFontSmoothing -int 2`

## Maybe better mojave font rendering and on a per-app basis
```
defaults write -g CGFontRenderingFontSmoothingDisabled -bool NO

defaults write com.microsoft.VSCode CGFontRenderingFontSmoothingDisabled 0
defaults write com.microsoft.VSCode.helper CGFontRenderingFontSmoothingDisabled 0
defaults write com.microsoft.VSCode.helper.EH CGFontRenderingFontSmoothingDisabled 0
defaults write com.microsoft.VSCode.helper.NP CGFontRenderingFontSmoothingDisabled 0
```

### Finder: disable window animations and Get Info animations
```
defaults delete com.apple.dock expose-animation-duration
defaults write com.apple.dock springboard-show-duration -int 0
defaults write com.apple.dock springboard-hide-duration -int 0
killall Dock
defaults write com.apple.finder DisableAllAnimations -boolean true
killall Finder
defaults write -g NSInitialToolTipDelay -integer 100
defaults write -g NSWindowResizeTime 0.1
```

### Check spelling as you type 
`defaults write -g CheckSpellingWhileTyping -boolean false`

### Enable continuous spell checking everywhere (don't know what it means)
`defaults write -g WebContinuousSpellCheckingEnabled -boolean false`

### Disable smart quotes:
`defaults write NSGlobalDomain NSAutomaticQuoteSubstitutionEnabled -bool false`

### Disable smart dashes:
`defaults write NSGlobalDomain NSAutomaticDashSubstitutionEnabled -bool false`

### Disable smart quotes for TextEdit:
`defaults write com.apple.TextEdit SmartQuotes -bool false`

### Disable smart dashes for TextEdit:
`defaults write com.apple.TextEdit SmartDashes -bool false`

### Disable the “Are you sure you want to open this application?” dialog
`defaults write com.apple.LaunchServices LSQuarantine -bool false`

### Disable Resume system-wide
`defaults write com.apple.systempreferences NSQuitAlwaysKeepsWindows -bool false`

### Disable the crash reporter
`defaults write com.apple.CrashReporter DialogType -string "none"`

### Enable spring loading for directories
`defaults write NSGlobalDomain com.apple.springing.enabled -bool true`

### Remove the spring loading delay for directories
`defaults write NSGlobalDomain com.apple.springing.delay -float 0`

---

### List All Hardware Ports

`networksetup -listallhardwareports`

### Disable Internet/Networking

```
sudo ifconfig en0 down
sudo ifconfig en0 up
```

### Compare Files

`opendiff index1.html index2.html`

---

## Managing Mac Fonts

The power of three You can find system fonts in three main locations:

**`/System/Library/Fonts/`**

Holds fonts that are available for all Mac OS user accounts; Mac OS needs many of these fonts to operate normally.

**`/Library/Fonts/`**

Holds fonts that are available for all Mac OS user accounts, including fonts installed by applications.

**`~/Library/Fonts/`**

Holds fonts that are available only for the current Mac OS user; each user account has it own Fonts folder For a more detailed explanation of where Mac OS keeps its fonts, see Mac OS X: Font locations and their purposes.

[Read More](https://support.apple.com/en-us/HT201722)

---

## Homebrew Services

Integrates Homebrew formulae with macOS's `launchctl` manager.

By default, plists are installed to `~/Library/LaunchAgents/` and run as the
current user upon login. When `brew services` is run as the root user, plists
are installed to `/Library/LaunchDaemons/`, and run as the root user on boot.

## Installation

`brew tap homebrew/services`

### List all services managed by `brew services`

`$ brew services list`

### Run/start/stop/restart all available services

`$ brew services run|start|stop|restart --all`

---

## Toggle MacOS X Notification Center on or off

[This gist](https://gist.github.com/mikermcneil/10005651) is to remind me (and anyone else who it helps) how to quickly disable and re-enable Notification Center.

#### Installation

1. Open your terminal (<⌘ + ␣ (spacebar)>, then type "terminal", then press <↩ (enter)>).

2. Paste and run the following command:

```sh
echo >> ~/.profile && echo >> ~/.profile && echo '# Disable/enable notification center' >> ~/.profile && echo 'alias disableNotificationCenter="launchctl unload -w /System/Library/LaunchAgents/com.apple.notificationcenterui.plist && killall NotificationCenter"' >> ~/.profile && echo 'alias enableNotificationCenter="launchctl load -w /System/Library/LaunchAgents/com.apple.notificationcenterui.plist && open /System/Library/CoreServices/NotificationCenter.app/"' >> ~/.profile && source ~/.profile
```

#### Usage

**To disable notification center:**

```sh
disableNotificationCenter
```

**To re-enable notification center:**

```sh
enableNotificationCenter
```

## How it works / background

#### Goal

Disable MacOS X's Notification Center entirely. But make it easy to turn it back on and disable again as needed.

#### Reasoning

I'm tired of seeing notifications that I can't dismiss, and there's no easy way to do this selectively (e.g. MacOS notifications always come through)

#### How this disables **Notification Center**

```sh
launchctl unload -w /System/Library/LaunchAgents/com.apple.notificationcenterui.plist
killall NotificationCenter

```

#### How this re-enables **Notification Center**

```sh
launchctl load -w /System/Library/LaunchAgents/com.apple.notificationcenterui.plist
open /System/Library/CoreServices/NotificationCenter.app/

```

---

## Setting up a Brand New Mac for Development (not complete)

#### Show Library folder

`chflags nohidden ~/Library`

#### Mac Store CLI

```
brew install mas
mas signin email@email.com
```

---

### System Integrity Protection in macOS

[What is SIP – System Integrity Protection in macOS](https://coolestguidesontheplanet.com/what-is-sip-in-osx-10-11-el-capitan)

Reboot your Mac into Recovery Mode by rebooting and holding down ‘command’ + ‘r’.

Launch a Terminal session and enter `csrutil disable`

then once logged back in, re-open terminal and enter: `sudo spctl --master-disable`

---

### Update and clean homebrew in one command

```
cd ~
sudo nano .bash_profile
```

Add the next line:

`alias brewup='brew update; brew upgrade; brew prune; brew cleanup; brew doctor'`

Then `CTRL+O` to save, press enter, `CTRL+X` to close

---

## NPM

#### Manually change npm’s default directory

`mkdir ~/.npm-global`
`npm config set prefix '~/.npm-global'`
`export PATH=~/.npm-global/bin:$PATH`
`source ~/.bash_profile`

To test your new configuration, install a package without using sudo:
`npm install -g jshint`

#### Install some NPM packages

npm install -g prettier jshint jsonlint eslint tslint typescript csslint ternjs bower

## Git

`export PATH="/usr/local/bin:/usr/bin/git:/usr/bin:/usr/local/sbin:$PATH"`

---

## Node

It is cleaner not to use sudo when installing npm packages there are a couple of options here on how this is done.
`sudo chown -R $(whoami) $(npm config get prefix)/{lib/node_modules,bin,share}`

If all else fails:

## Fix NPM

`sudo chown -R $(whoami) /usr/local/lib/node_modules`
`sudo chown -R $(whoami) /usr/local/bin`
`sudo chown -R $(whoami) /usr/local/share`

---

## Generate SSH Private and Public Keys in macOS

#### Create a .ssh Directory

`cd ~/`

#### Create a SSH directory name .ssh and move into it

`mkdir .ssh ; cd .ssh`

#### Make sure that the file permissions are set to read/write/execute only for the user

`chmod go-rwx .ssh`

#### Create your private and public key, the blank quotes at the end of the command gives the private key no password, so allowing for passwordless logins!

`ssh-keygen -b 1024 -t rsa -f id_rsa -P ""`

#### Change into the .ssh directory and list the contents of that .ssh directory

`cd .ssh ; ls`

## References

[OSX Daily](https://osxdaily.com/2012/08/06/disable-notification-center-remove-menu-bar-icon-os-x/) | [Coolest Guides on the Planet](https:/coolestguidesontheplanet.com)
