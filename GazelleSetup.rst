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
* installed Gnome 3 Tweaks via Pop Shop
  * set Caps Lock to Ctrl
  * enabled week numbers in calendar
* added Git PPA to software sources
* cloned dotfiles repo from GitHub
  * created pop_os/khawla/ by copying from ubuntu/kudu/ and editing:
  
    * .ssh/config
    * .gitconfig
    * .profile

  * TODO:

    * set up symlinks
      ln -s ~/dotfiles/pop_os/khawla/.ssh/config ~/.ssh/config
      ln -s ~/dotfiles/pop_os/khawla/.gitconfig ~/.gitconfig
      ln -sf ~/dotfiles/pop_os/khawla/.profile ~/.profile

      .bash_aliases
      .condarc
      .cookiecutterrc
      githooks: rescuetime
      vscode settings.json
      
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

* downloaded Toolbox app tarball from jetbrains.com
* unpacked tarball into ~/bin/
* ran the contained app to launch Toolbox and install it as a startup app
* 

MOAD Repos
^^^^^^^^^^

43ravens Repos
^^^^^^^^^^^^^^

borg Backups
^^^^^^^^^^^^

Darktable & Photos
^^^^^^^^^^^^^^^^^^

* installed Darktable 3.6.1 flatpak from Pop Shop
* TODO:
  * migrate config
  * migrate images
  * Rapid Photo Downloader
  * dotfiles backup-photos.sh


Gnucash
^^^^^^^

* installed Gnucash 4.8a+ flatpak from Pop Shop
* TODO:
  * migrate files
  * migrate reports

Other Applications
^^^^^^^^^^^^^^^^^^

flatpaks are generally newer versions than .deb (when both are available)

From Pop Shop:

* GIMP 2.10.28 flatpak
* Inkscape 1.1.1 flatpak
* Remmina 1.4.21 flatpak
* Skype flatpak
* Slack flatpak
* Thunderbird flatpak
* VirtualBox deb
* Zoom flatpak
* Xournal++ flatpak
  * TODO: migrate signature file

Others:

* Microsoft Teams .deb from microsoft.com
  * that adds packages.microsoft.com/repos/ms-teams to software sources
* Rescuetime .deb from rescuetime.com and Firefox add-on
  * made it an auto-start app by creating ~/.config/autostart/rescuetime.desktop containing:

      [Desktop Entry]
      Type=Application
      Exec=/usr/bin/rescuetime
      Hidden=false
      NoDisplay=false
      X-GNOME-Autostart-enabled=true
      Name[en_CA]=RescueTime
      Name=Rescuetime
      Comment[en_CA]=RescueTime monitoring app
      Comment=Rescuetime monitoring app

Chromium for CubedHost
eFunds from my portfolio repo
