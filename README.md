# usm
[unix sample manager] search TERABYTES of samples across different (network) disks in few seconds (+offline)

# Usage

[](demo.gif)

# The problem 

> How to quickly search thru terabytes of samples across different harddrives/clouddrives? And what if they're offline?

This is a problem scientists, audiodesigners and videoartists face.

> solution: the good old unix tool *locate*

# Installation

> now lets create indexes

    $ sudo apt-get install mlocate dialog
    $ mkdir ~/.mlocate 
    $ updatedb --output ~/.mlocate/myusbdiskA --root /mnt/myusbdiskA/samples
    $ updatedb --output ~/.mlocate/myusbdiskB --root /mnt/myusbdiskB/projects
    $ echo 'export LOCATE_PATH=~/.mlocate' >> ~/.bashrc

> NOTE: `updatedb` takes a while (depending on the size of your hd)

    $ wget

# Unix ninja's

USM is just a wrapper for the `locate` tool. You can use also without USM:

    $ locate -r 'kick.*\.wav' -l10     # show first 10 regex matches

Also, USM's default preview-action is to play it as audio.
This can be overruled by running USM like so:

    $ ACTION=~/bin/myviewer usm

> This will simply open the selected file with `~/bin/myviewer`

# Background 

The author struggled for years with a proper solution.
Searching thru network drives (sshfs / nfs / samba) is too slow in many cases.
