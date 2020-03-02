My personal build of dwm (based on 6.2)
=======================================
DWM is an extremely fast, small, and dynamic window manager for X.

Requirements
------------
In order to build dwm you need the Xlib header files.

Installation
------------
Edit config.mk to match your local setup (dwm is installed into
the /usr/local namespace by default).

Afterwards enter the following command to build and install dwm (if
necessary as root):

`sudo make clean install`

Patches
--------
_All patches are added via branches. Source: [here](https://dwm.suckless.org/patches/)_
- [attachaside](https://dwm.suckless.org/patches/attachaside/)
- [bottomstack](https://dwm.suckless.org/patches/bottomstack)
- [mastermonitor](https://github.com/flaport/dwm/commit/55a46c0f808d01b0450eed748e49bfa9d278e317)
    - The master monitor is the only monitor with tags. All other monitors will
    have no tags.  The tags from the master can be accessed
    (enabled/disabled/send to) with the normal keybindings from any monitor.
    This makes the tag system a lot less confusing in a multi monitor setup.
    - This patch has been modified for my personal use
        - Removed Ctrl-n/Ctrl-Shift-n bindings for switching to monitor
        - Added statusallmons patch to display status bar on all monitors
- [noborder](https://dwm.suckless.org/patches/noborder/)
- [restartsig](https://dwm.suckless.org/patches/restartsig/)
- [tilegap](https://dwm.suckless.org/patches/tilegap/)
- [titlecolor](https://dwm.suckless.org/patches/titlecolor/)

**Patching guide**
refer to [here](https://github.com/qguv/dwm) for an example
- Reset develop branch:
    - `rm -rf config.h && sudo make clean`
    - `git reset --hard origin/develop`
- Add a patch:
    - branch off of clean develop branch
    - apply patch
    - move all config.def.h changes to config branch
    - commit branch `git commit -m <branchname>`
- Delete a patch:
    - Delete branch locally
        `git branch -D <branchname>`
    - Delete branch remotely
        `git push origin --delete <branchname>`
- Merge to develop (in order to build):
    - Reset develop branch
        `rm -rf config.h && sudo make clean`
    - Merge all branches
        `git merge <branchname> m <branchname>`
- Build

Running dwm
-----------
Add the following line to your .xinitrc to start dwm using startx:

`exec dwm`

In order to display status info in the bar, you can do something
like this in your .xinitrc:
```bash
while xsetroot -name "`date` `uptime | sed 's/.*,//'`"
do
  sleep 1
done &
exec dwm
```
