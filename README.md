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

## Flush Cache & Clear DNS
* `sudo dscacheutil -flushcache`
* `sudo killall -HUP mDNSResponder`

## Reset Audio
* `sudo killall coreaudiod`
