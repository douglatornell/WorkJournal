Gazelle Setup
=============

Delivered: 29-Nov-2021
Name: khawla

Specs
-----

* 15.6" Matte Full HD 1080p (144 Hz) display
* 4 GB RTX 3050 w/ 2048 CUDA Cores
* 4.6 GHz i7-11800H - up to 4.6 GHz - 24MB Cache - 8 Cores - 16 Threads)
* 64 GB Dual Channel DDR4 at 3200 MHz (2x 32GB)
* 1 TB NVMe Seq Read: 7,000 MB/s, Seq Write: 5,000 MB/s
* 2 TB NVMe Seq Read: 3,500 MB/s, Seq Write: 3,300 MB/s


Setup
-----

Basics
^^^^^^

* encrypted boot drive
* installed LaserJet-3052 printer as pencil
* copied ssh keys from kudu via USB key
  * had to fix permissions on private keys to 600
* used disks utility to rename file system on 2Tb drive to warehouse and set
  it to mount on boot
* added Git PPA to software sources
* cloned dotfiles repo from GitHub
  * created pop_os/khawla/.ssh/config by coping from ubuntu/kudu/.ssh/config
  * TODO:

    * set up symlinks
      ln -s ~/dotfiles/pop_os/khawla/.ssh/config ~/.ssh/config
* TODO:
  * remap Caps Lock key to Ctrl; need gnome-tweaks

Firefox
^^^^^^^

* signed into Firefox to sync extensions
  * created extra tab containers

VSCode
^^^^^^

* installed VSCode via .deb download from code.visualstudiocode.com
  * that adds packages.microsoft.com/repos/code to software sources
  * TODO install extensions

Minecraft
^^^^^^^^^

* installed Minecraft via .deb download from minecraft.net
  * TODO install mods, datapacks, etc.

PyCharm
^^^^^^^

MOAD Repos
^^^^^^^^^^

43ravens Repos
^^^^^^^^^^^^^^

borg Backups
^^^^^^^^^^^^

Darktable & Photos
^^^^^^^^^^^^^^^^^^
