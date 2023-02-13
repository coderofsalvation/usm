# usm
[unix sample manager] search TERABYTES of samples across different (network) disks in few seconds (+offline)

> UPDATE 19-02-2023: usm now automatically symlinks the searchresults to a folder (which you can open in your daw/app etc) ❤

# Usage

<img src="demo.gif" width="100%"/>

# The problem 

> How to quickly search thru terabytes of samples across different harddrives/clouddrives? And what if they're offline?

This is a problem scientists, audiodesigners and videoartists sometimes face.

> solution: the good old `locate` unix tool

# Installation

> lets index some huge folders 

    $ sudo apt-get install mlocate dialog
    $ mkdir ~/.mlocate 
    $ updatedb --output ~/.mlocate/samples    --root /home/myusername/samples 
    $ updatedb --output ~/.mlocate/myusbdiskB --root /mnt/myusbdiskB/projects
    $ updatedb --output ~/.mlocate/dropbox    --root /mnt/Dropbox/audio
    $ updatedb --output ~/.mlocate/gdrive     --root /mnt/Gdrive/myrockband

> depending on your mlocate version, use one of these:

    $ echo "export LOCATE_PATH=/var/lib/mlocate/mlocate.db:$(find ~/.mlocate/* | sed 'N;s|\n|:|g')" >> ~/.bashrc
    $ echo "export LOCATE_PATH=~/.mlocate" >> ~/.bashrc

> now lets install usm 

    $ wget "https://raw.githubusercontent.com/coderofsalvation/usm/master/usm"
    $ chmod 755 usm
    $ sudo cp usm /usr/local/bin/.

> optional: install `rclone` to easily mount clouddrives to local folders (great for small harddrives)

# Unix ninja's

USM is just a wrapper for the `locate` tool. You can also search indexes without USM:

    $ locate -r 'kick.*\.wav' -l10     # show first 10 regex matches

Also, USM's default preview-action is to play it as audio.
This can be overruled by running USM like so:

    $ ACTION=~/bin/myviewer usm

> This will simply open the selected file with `~/bin/myviewer`

# Background 

The author struggled for years with a proper solution.
As a sounddesigner his audio / instrument library kept growing and growing.
Searching thru network drives (sshfs / nfs / samba) is too slow in many cases, and not possible offline.
USM only touches a networkdrive when preview or saving a file.
