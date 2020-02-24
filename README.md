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
- bottomstack
- noborder
- pertag
- restartsig
- statusallmons
- titlecolor

**Patching guide**
refer to [here](https://github.com/qguv/dwm) for an example
- Add a patch:
    - branch off of develop
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
