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
* installed Mercurial distro pkg via apt
* overrode super+T keyboard shortcut to launch terminal with `/usr/bin/gnome-terminal --window --maximize`
* cloned dotfiles repo from GitHub
  * created pop_os/khawla/ by copying from ubuntu/kudu/ and editing:
  
    * .ssh/config
    * .gitconfig
    * .profile
    * githooks/rescuetime_commit_highlight.sh
    * .bash_aliases
    * .condarc
    * .cookiecutterrc

  * TODO:

    * set up symlinks
      ln -s ~/dotfiles/pop_os/khawla/.ssh/config ~/.ssh/config
      ln -s ~/dotfiles/pop_os/khawla/.gitconfig ~/.gitconfig
      ln -sf ~/dotfiles/pop_os/khawla/.profile ~/.profile
      ln -sf ~/dotfiles/pop_os/khawla/.bash_aliases ~/.bash_aliases
      ln -sf ~/dotfiles/pop_os/khawla/.condarc ~/.condarc
      ln -sf ~/dotfiles/pop_os/khawla/.cookiecutterrc ~/.cookiecutterrc

      vscode settings.json
      
* installed Mambaforge-pypy3 (like miniconda, but with conda-forge as default and only channel, mamba in place of conda, and PyPy 3.7 in base env) from https://github.com/conda-forge/miniforge
    cd ~/Downloads/
    curl -L -O https://github.com/conda-forge/miniforge/releases/latest/download/Mambaforge-pypy3-$(uname)-$(uname -m).sh
    cd ~
    bash ~/Downloads/Mambaforge-pypy3-$(uname)-$(uname -m).sh
* created ~/conda_envs/ for storage of conda envs on fastest storage (now that it is big); 1st env creation for NEMO-Cmd was blazingly fast :-)
* thrashed getting camera to work until I looked at System76 troubleshooting page and realized that it was disabled by the Fn+F10 hardware switch
* rsync-ed ~/Documents/ and /media/doug/warehouse/Documents from kudu into ~/Documents/


Firefox
^^^^^^^

* signed into Firefox to sync extensions
  * created extra tab containers


VSCode
^^^^^^

* installed VSCode via .deb download from code.visualstudiocode.com
  * that adds packages.microsoft.com/repos/code to software sources
  * installed extensions:
    * IntelliJ IDEA Keybindings
    * Python
    * GitLens
    * Remote - SSH
    * GitHub Pull Requests and Issues
    * Clipboard
    * Code Spell Checker
    * Mako
    * Modern fortran
    * pre-commit-vscode
    * Extension Pack for reStructuredText


Minecraft
^^^^^^^^^

* installed Minecraft via .deb download from minecraft.net
  * TODO install mods, datapacks, etc.
* Checked status of Minecraft mods on 4-Dec-21:
  * MaLiLib has a 1.18 release
  * Litematica has a 1.18 beta release (1.17 was never beyond beta)
  * MiniHUD has no 1.18
  * Sodium has a 1.18 alpha release
  * Lithium has no 1.18
  * Phosphur has no 1.18
  * Hydrogen has no 1.18
  * Iris has a 1.18 release
  * Complementary shaders has a 1.18 release
  * VanillaTweaks as a 1.18 release
* Downloaded Iris universal installer from irisshaders.net; installed it w/ the Fabric option and
  got Fabric, Sodium and Iris; in-game CPU usage dropped to ~40$ and ~150 fps (capped) was solid


PyCharm
^^^^^^^

* downloaded Toolbox app tarball from jetbrains.com
* unpacked tarball into ~/bin/
* ran the contained app to launch Toolbox and install it as a startup app
* installed PyCharm via Toolbox
* exported settings.zip from PyCharm on kudu; rsynced to khawla; imported
* installed plugins:
  * .ignore
  * Nyan Progress Bar
  * requirements
  * updated Datalore
  * skipped Key Promoter X for now


MOAD Repos
^^^^^^^^^^

MEOPAR
""""""

* created /media/doug/warehouse/MEOPAR/ and cloned SalishSeaCast org repos into it:

  * NEMO-Cmd
  * SalishSeaNowcast
  * tools
  * SalishSeaCmd
  * FVCOM-Cmd
  * OPPTools from GitLab
  * analysis-doug
  * docs
* TODO:
  * rsync .idea/workspace.xml and .idea/vcs.xml files from kudu projects to get project level configs
  * re-create PyCharm project structures



MIDOSS
""""""

* created /media/doug/warehouse/MIDOSS/ and cloned MIDOSS org repos into it:

  * MOHID-Cmd
  * MIDOSS-MOHID-config
  * Make-MIDOSS-Forcing
  * docs
  * MIDOSS-MOHID-CODE
  * WWatch3-Cmd
  * MIDOSS-MOHID-grid
* rsync-ed .idea/workspace.xml and .idea/vcs.xml files from kudu projects to get project level 
    configs
* TODO:
  * re-create PyCharm project structures


MOAD
""""

* created /media/doug/warehouse/MOAD/ and cloned UBC-MOAD org repos into it:

  * MoaceanParcels
  * moad_tools
  * cookiecutter-MOAD-pypkg
  * cookiecutter-analysis-repo
  * docs
  * PythonNotes
* rsync-ed .idea/workspace.xml and .idea/vcs.xml files from kudu projects to get project level configs
* TODO:
  * re-create PyCharm project structures


Atlantis
""""""""

* created /media/doug/warehouse/Atlantis/ and cloned SS-Atlantis org repos into it:

  * AtlantisCmd
* rsync-ed .idea/workspace.xml and .idea/vcs.xml files from kudu projects to get project level configs
* TODO:
  * re-create PyCharm project structures
  * svn checkouts from CSIRO Bitbucket server


43ravens Repos
^^^^^^^^^^^^^^

* personal/Workjournal
* 43ravens/43ravens.ca
* 43ravens/biz-journal
* 43ravens/domains-maint
  * rsync -av kudu.local:/media/doug/warehouse/43ravnes/domains-maint/db-backups domains-maint/
  * rsync -av /media/doug/warehouse/43ravens/domains-maint/phpgedview-svn-r7320-trunk-phpGedView.zip domains-maint/
* 43ravens/NEMO_Nowcast -> projects/NEMO_Nowcast
  * added to SalishSeaCast group in PyCharm project mgr
* 43ravens/client-UBC-SCARP -> clients/UBC-SCARP
* rsync -av kudu.local:/media/doug/warehouse/43ravens/financial 43ravens/

* TODO: rsync .idea/workspace.xml files from kudu projects to get project level configs


borg Backups
^^^^^^^^^^^^

* installed borgbackup system pkg via apt
* Cloned douglatornell/borg-bkup
* created borg repo w/ encryption and auto compression using zstd for khawla on lizzy
    borg init --encryption=repokey /backup/borg/khawla
* created and tuned borg-bkup/khawla-lizzy.sh
* added khawla to borg-backup framework on smelt:
* created borg repo for khawla
    borg init --encryption=repokey-blake2 /backup/borg/khawla
* created borg-bkup/khawla-smelt.sh script and used it for 1st khawla backup to smelt


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
* migrate files as part of rsync ~/Documents/ and /media/doug/warehouse/Documents from kudu into 
  ~/Documents/
* manually migrated preferences by comparison w/ Gnucash running on kudu becayse they are stored in dconf; minimal work
* migrated reports by rsync-ing kudu:.local/share/gnucash/saved-reports-2.8 to 
  .var/app/org.gnucash.GnuCash/data/gnucash/saved-reports-2.8


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

After a lot of searching, learned that I could xfer Thunderbird profile from kudu into
~/.var/app/org.mozilla.Thunderbird/.thunderbird/ to get my address book, feeds, etc.
Also learned that to run a flatpak app from the command line one uses something like
``flatpak run org.mozilla.Thunderbird``
Discovered that filters aren't recognized when they are symlinked from 
/home/doug/dotfiles/thunderbird/profile.default/ImapMail/mail.eoas.ubc.ca/msgFilterRules.dat
so copied that file to
.var/app/org.mozilla.Thunderbird/.thunderbird/24otlwll.default/ImapMail/mail.eoas.ubc.ca/msgFilterRules.dat

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

eFunds from my portfolio repo
