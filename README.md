# Mac Useful Commands

AA collection of little code snippets or tutorials to get the most out of your mac or out of a certain situation.

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

## Flush Cache & Clear DNS
* `sudo dscacheutil -flushcache`
* `sudo killall -HUP mDNSResponder`

## Reset Audio
* `sudo killall coreaudiod`

## Disable Gatekeeper
* `sudo spctl --master-disable`
* `sudo defaults write /Library/Preferences/com.apple.security GKAutoRearm -bool NO`

## Show/Hide Hidden Files
* `defaults write com.apple.finder AppleShowAllFiles NO`
* `defaults write com.apple.finder AppleShowAllFiles YES`
* `killall Finder`

---

## Homebrew Services

Integrates Homebrew formulae with macOS's `launchctl` manager.

By default, plists are installed to `~/Library/LaunchAgents/` and run as the
current user upon login.  When `brew services` is run as the root user, plists
are installed to `/Library/LaunchDaemons/`, and run as the root user on boot.

## Installation ##
`brew tap homebrew/services`

### List all services managed by `brew services` ###
`$ brew services list`

### Run/start/stop/restart all available services ###
`$ brew services run|start|stop|restart --all`

---

# Toggle MacOS X Notification Center on or off

[This gist](https://gist.github.com/mikermcneil/10005651) is to remind me (and anyone else who it helps) how to quickly disable and re-enable Notification Center.

## Set Up Bash Aliases

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
Disable MacOS X's Notification Center entirely.  But make it easy to turn it back on and disable again as needed.

#### Reasoning
I'm tired of seeing notifications that I can't dismiss, and there's no easy way to do this selectively (e.g. MacOS notifications always come through)

#### How this disables __Notification Center__

```sh
launchctl unload -w /System/Library/LaunchAgents/com.apple.notificationcenterui.plist
killall NotificationCenter

```

#### How this re-enables __Notification Center__

```sh 
launchctl load -w /System/Library/LaunchAgents/com.apple.notificationcenterui.plist
open /System/Library/CoreServices/NotificationCenter.app/

```

## Bibliography
This approach is a command-line-only version of the solution proposed in [a great article](http://osxdaily.com/2012/08/06/disable-notification-center-remove-menu-bar-icon-os-x/) on osxdaily.com.
