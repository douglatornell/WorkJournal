*****************
2022 Work Journal
*****************

This is my public work journal.
This journal is about:

* my work as a Research Software Engineer with Dr. Susan Allen in the Department of Earth, Ocean and Atmospheric Sciences at the University of British Columbia
* my freelance work via my consulting business,
  43ravens
* my open-source activities
* occasional notes about life in general


January
=======

Week 0
------

Sat 1-Jan-2022
^^^^^^^^^^^^^^

8 spills that are repeats of failed spills start on line 9849 of csv
50-55 queued
(MIDOSS)

Initialized balances and securities prices into 2022 accounts.


Sun 2-Jan-2022
^^^^^^^^^^^^^^

collect_weather 06 did not finish; investigation:
* re-tried download failures and queue 404 in log
* 445 of 576 files downloaded
* missing files in hours 7-8; no files in hours 9-18
* recovery at ~10:15:
    pkill collect_weather 06
    collect_weather 18 2.5km &
    rm -rf /results/forcing/atmospheric/GEM2.5/GRIB/20220102/06
    download_weather 06 2.5km
    wait for forecast2 runs to finish
    download_weather 12 2.5km
(SalishSeaCast)


Week 1
------

Mon 3-Jan-2022
^^^^^^^^^^^^^^

**Statutory Holiday** - New Years Day lieu day

upload_forcing arbutus forecast2 failed due to connection time-out
upload_forcing arbutus nowcast+ failed due to connection time-out
investigation:
* nowcast0 shut down with no explanation at 3-Jan 12:25 UTC == 16:25 Pacific;
* 02jan/forecast-x2 interrupted
* no 02jan/nowcast-r12
* no 03jan/forecast2 runs
* recovery started at ~09:25
  * restarted nowcast0 from web dashboard at 17:26 UTC == 09:26 Pacific
      sudo apt update
      # all packages are up to date
      sudo mount /dev/vdc /nemoShare
      ll /nemoShare/MEOPAR/  # to confirm mount
      sudo mount --bind /nemoShare/MEOPAR /export/MEOPAR
      ll /export/MEOPAR  # to confirm mount
      sudo systemctl start nfs-kernel-server.service
      sudo exportfs -f  # to reset NFS handles for compute nodes
      # confirm compute nodes have /nemoShare/MEOPAR/ mounted:
      for n in {1..9}; do   echo nowcast${n};   ssh nowcast${n} "mountpoint /nemoShare/MEOPAR"; done
      for n in {1..9}; do   echo nowcast${n};   ssh nowcast${n} "ls -C /nemoShare/MEOPAR"; done
      for n in {0..6}; do   echo fvcom${n};   ssh fvcom${n} "mountpoint /nemoShare/MEOPAR"; done
      for n in {0..6}; do   echo fvcom${n};   ssh fvcom${n} "ls -C /nemoShare/MEOPAR"; done
    * cleaned up stale tmp run dirs in runs/, fvcom-runs/ & wwatch3-runs/
  * on skookum:
    * confirmed that there are no stale workers
    * restarted log_aggregator
    * decided to skip forecast2 runs
    * recovery started at ~09:38:
        upload_forcing arbutus nowcast+
        wait for forecast-x2 then nowcast-r12 to fail at ~13:00
        launch_remote_worker arbutus make_fvcom_boundary arbutus x2 forecast 2022-01-02
        02jan22/forecast-x2 failed, but then automation started 02jan22/nowcast-r12
        wait for nowcast-r12 to finish at ~20:45
        launch_remote_worker arbutus make_fvcom_boundary arbutus r12 nowcast 2022-01-03
Continued copying GEMLAM from /opp to graham:nearline/ in 3-mo tarballs: 2012-q3 & q4
(SalishSeaCast)

Checked minecraft mods status:
* MaLILib - no changes
* Litematica - no changes
* MiniHUD - no 1.18 release
* Iris - no change
* Complementary shaders - new 4.3.3 release
* sodium - no changes
* lithium - new 1.18.1 release
* phosphur - new 1.18.x release
* hydrogen - no changes

Added khawla to borg-backup framework on smelt:
* created borg repo for khawla
    borg init --encryption=repokey-blake2 /backup/borg/khawla
* created borg-bkup/khawla-smelt.sh script and used it for 1st khawla backup to smelt

Group mtg; see whiteboard.
(MOAD)

Dug deeper into repo inherited from Phil, trying to understand automation.
(Numeric Course)


Tue 4-Jan-2022
^^^^^^^^^^^^^^

Continued copying GEMLAM from /opp to graham:nearline/ in 3-mo tarballs: 2013-q1 & q2
(SalishSeaCast)

Group mtg to plan mtgs for term.
(OceanParcels)

Decided to prototype new workflows in a test repo: douglatornell/numeric-refactor:
* created douglatornell/numeric-refactor oh GitHub
* see commits history
* successfully used Mambaforge-pypy3 in sphinx to gh-pages workflow :-)
* trashed getting notebooks included properly due to having .ipynb in source suffixes list
(Numeric Course)


Wed 5-Jan-2022
^^^^^^^^^^^^^^

Sentry is terminating Slack integration for free Developer plans on 10-Jan; US$312/yr to upgrade to Team plan.
04jan22/nowcast-x2 failed, and no subsequent runs; investigation:
* nowcast6 node stopped 3jan22 20:29 UTC == 12:29 Pacific
* missing runs:
  * 03jan22/nowcast-x2 forecast-x2
  * 04jan22/nowcast-x2 forecast-x2 nowcast-r12
* recovery started at ~10:00
  * restarted nowcast6 from dashboard 5jan22 18:03 UTC == 10:03 Pacific
      sudo mount -t nfs -o proto=tcp,port=2049 192.168.238.14:/MEOPAR /nemoShare/MEOPAR
    launch_remote_worker arbutus make_fvcom_boundary arbutus x2 nowcast 2022-01-03
    wait for 03jan22/forecast-x2 to start at ~12:45; kill it
    launch_remote_worker arbutus make_fvcom_boundary arbutus x2 nowcast 2022-01-04
    wait for 04jan22/forecast-x2 to start at ~15:15; kill it
    launch_remote_worker arbutus make_fvcom_boundary arbutus x2 nowcast 2022-01-05
    wait for 05jan22/nowcast-r12 to fail at ~21:15
    launch_remote_worker arbutus make_fvcom_boundary arbutus r12 nowcast 2022-01-04
Continued copying GEMLAM from /opp to graham:nearline/ in 3-mo tarballs: 2013-q3 & q4
(SalishSeaCast)

Renamed docs/ to website/ in numeric-refactor because it makes more sense.
Added lab1 in notebooks/ and numlabs/ w/ symlink to notebooks/ in website/,
and it all just works :-)
Created GitHub project to communicate and track tasks
(Numeric Course)


Thu 6-Jan-2022
^^^^^^^^^^^^^^

1st on-boarding session w/ Armaan:
* Windows user
download_live_ocean delayed ~2h
upload_forcing orcinus failed; I dropped the ball and didn't investigate
Backfill nowcast-r12:
  wait for 06jan22/nowcast-r12 to fail at ~16:45
  launch_remote_worker arbutus make_fvcom_boundary arbutus r12 nowcast 2022-01-05
(SalishSeaCast)

Got news that M has tested +ve for COVID-19; J in isolation pending PCR test.

Started migrating website content from numeric_2022 to numeric-refactor; see issue #8.
(Numeric Course)

COVID-19 vaccine dose #3.


Fri 7-Jan-2022
^^^^^^^^^^^^^^

upload_forcing orcinus failed; ssh connections failing; send email to Mark; power outage yesterday took orcinus down.
Backfill nowcast-r12:
  wait for 07jan22/nowcast-r12 to fail at ~15:00
  launch_remote_worker arbutus make_fvcom_boundary arbutus r12 nowcast 2022-01-06
  wait for 06jan22/nowcast-r12 to finish at ~22:00
  launch_remote_worker arbutus make_fvcom_boundary arbutus r12 nowcast 2022-01-07
Continued copying GEMLAM from /opp to graham:nearline/ in 3-mo tarballs: 2014-q1
(SalishSeaCast)

Continued migrating website content from numeric_2022 to numeric-refactor; see issues #8 & #9.
Transferred numeric-refactor to rhwhite.
(Numeric Course)

Put in ticket to get permissions and user id of /home/arandhawa fixed and /ocean/arandhawa created.
(MOAD)

Restored default terminal super+t keybinding to stop fullscreen on 35" monitor; special binding was:
  /usr/bin/gnome-terminal --window --maximize
Changed khawla terminal profile size to 284x100; might need to do special binding to get position I prefer:
  /usr/bin/gnome-terminal --geometry=284x100+0+0
  

Sat 8-Jan-2022
^^^^^^^^^^^^^^

Backfill nowcast-agrif:
  upload_forcing orcinus nowcast+ --run-date 2022-01-06
  upload_forcing orcinus turbidity --run-date 2022-01-06
  wait for 06jan22 run to complete
Continued copying GEMLAM from /opp to graham:nearline/ in 3-mo tarballs: 2014-q2 & q3
/results filled during make_plots; recovery:
* deleted nowcast-dev.201905/*20/ dirs
* re-ran make_plots:
    make_plots wwatch3 forecast publish
    make_plots fvcom nowcast-x2 publish 2022-01-06
    make_plots fvcom nowcast-x2 publish 2022-01-08
    make_plots nemo nowcast-green research 2022-01-08
(SalishSeaCast)

Changed website theme to Mozilla Sandstone theme; closed issue #6.

Continued migrating website content from numeric_2022 to numeric-refactor; see issues #8 & #9.
(Numeric Course)
  

Sun 9-Jan-2022
^^^^^^^^^^^^^^

Backfill nowcast-agrif:
  upload_forcing orcinus nowcast+ --run-date 2022-01-07
  upload_forcing orcinus turbidity --run-date 2022-01-07
  wait for 07jan22 run to complete
  upload_forcing orcinus nowcast+ --run-date 2022-01-08
  upload_forcing orcinus turbidity --run-date 2022-01-08
  wait for 08jan22 run to complete
  upload_forcing orcinus nowcast+ --run-date 2022-01-09
  upload_forcing orcinus turbidity --run-date 2022-01-09
Finished copying GEMLAM from /opp to graham:nearline/ in 3-mo tarballs: 2014-q4
(SalishSeaCast)

Susan got her COVID-19 vaccine dose #3.


Week 2
------

Mon 10-Jan-2022
^^^^^^^^^^^^^^^

Weekly group mtg; see whiteboard
Toured repos w/ GHA sphinx-linkcheck workflows to re-enable those that have not had recent activity.
(MOAD)

SalishSeaCast/docs updates:
* VSCode build task
* update .gitignore; drop .hgignore
* update copyright year range
  * NOTE: there are no copyright notice comments blocks at tops of files
* redirect Anaconda Python section to MOAD/docs conda section
* update version control section re: change to Git
(SalishSeaCast)

Transformed note on whiteboard about addition of fisheries harvest params option to AtlantisCmd into issue #3.
(Atlantis)


Tue 11-Jan-2022
^^^^^^^^^^^^^^^

Worked at ESB while Rita was at home.

SalishSeaCast/docs updates:

* update intro to Python section to use Tomas Beuzen's book and move section to MOAD docs
(MOAD)

Group mtg; Raisha talked about oil evaporation via exponential decay in a kernel;
so much for my "particle motion kernel" terminology
(OceanParcels)

Continued on-boarding w/ Armaan:
* install OpenSSH for Windows then work through Secure Remote Access setup; success
* left Armaan to work through Secure Remote Access and onward by himself; issues:
  * notepad created .ssh\config.txt; had to rename in .ssh\
  * Windows doesn't have ssh-copy-id; had to copy/paste via black box in top of cmd window
  * had to use admin mode Anaconda shell to start ssh-agent with:
      Set-Service ssh-agent -StartupType Automatic
      Start-Service ssh-agent
      Get-Service ssh-agent
      # from https://code.visualstudio.com/docs/remote/troubleshooting#_setting-up-the-ssh-agent
(SalishSeaCast)


Wed 12-Jan-2022
^^^^^^^^^^^^^^^

SHARCNET webinar:
* Armin Sobhani, OntarioTech U
* Remote Dev on Clusters w/ VSCode
* vcpkg - c/c++ pkg mgr
* GitHub sharcnet/vscode-hpc
* moduled have to be loaded via ~/.bashrc; e.g.
    module load cmake cuda scipy-stack/2020a ipykernel
* demo of local Code on windows
* cmake:
  * tight integration w/ VSCode for Intellisense, linting for compiled languages
  * "not your grandmother's make"
* Windows Terminal will replace cmd/powershell in Windows 11; preview release available now
* recommends ed25519 encryption for ssh keys
* CCDB installation of ssh public keys

HRDPS 12 delayed until ~11:15
(SalishSeaCast)

Helped Susan install VSCode and selected extensions.

Updated khawla to Pop_OS 21.10.

Disabled IntelliJ keymap extension in VSCode on khawla.

Changed MOAD/docs sphinx linkcheck workflow to use Mambaforge-pypy3; created #repos-maint post with 
task list to similarly update all repos where we use GHA. 
Updated nbviewer URL in MOAD/docs and cookiecutter-analysis-repo; probably a lot more instances in 
other repos.
Tried to use cs.github.com to help with above; appears that not all of our org repos are indexed 
yet.
Updated other redirected URLs in MOAD/docs.
Added pre-commit hooks to MOAD/docs.
(MOAD)

Generated new ed25519 ssh key pair on khawla and made it my default:
* copied public key to ocean machines and removed 2014 vintage 2048 bit rsa key
* replaced public key on GitHub
* replaced public key on computecanada CCDB


Thu 13-Jan-2022
^^^^^^^^^^^^^^^

Updated kudu to Pop_OS 21.10; had to fix full boot volume on the way:
* clean up /var/cache/apt/archives/ with:
  sudo apt autoclean
* flatpak cleanup:
    flatpak update --appstream
    flatpak update
    flatpak uninstall --unused
* deleted a bunch of old kernels with guidance from askubuntu (https://askubuntu.com/questions/345588/what-is-the-safest-way-to-clean-up-boot-partition)
  uname -r  # in-use kernel - **don't delete**
  dpkg --list 'linux-image*' | grep ^ii  # installed kernels
  sudo apt remove linux-image-VERSION  # remove all but in-use and previous kernels
  sudo apt autoremove  # remove pkgs associated w/ removed kernels
  # recovered 362 Mb == 55% of /boot

Squash-merged dependabot PRs re: pillow:
* SalishSeaNowcast
* SalishSeaTools
* SOG-Bloomcast-Ensemble
* analysis-doug/melanie-geotiff
* analysis-doug/dask-expts
* moad_tools
Helped Armaan on slack re: .bash_profile & .bashrc already existing in his ocean account;
.bash_profile is good, add aliases, etc. to end of .bashrc
(SalishSeaCast)

Pullled lab3 from 2020 repo and cleaned up markup.
Started work on issue #16 re: schedule and rubric PDFs giving 404s on github.io site;
root cause is GHA workflow doesn't do ``make html``;
workable resolution is to keep PDFs in _static/ tree that does get deployed;
concern is that makes location of PDFs non-obvious. 
(Numeric)

Added new 1.81.1 releases of lithium and phosphur to Minecraft client mods.
Changed Nodecraft server to run fabric via 1-click installer and archiving files to old_files/;
Restored world files and successfully tested world, then installed lithium and phosphur mods
and restarted world.


Fri 14-Jan-2022
^^^^^^^^^^^^^^^

upload_forcing graham nowcast+ failed w/ permission error; no obvious explanation;
re-ran successfully in debug mode at 10:48.
(SalishSeaCast)

Submitted renewal application for UBC Card.

Started work on diatoms nudging fields extraction in analysis-doug/dask-expts/
(Atlantis)


Sat 15-Jan-2022
^^^^^^^^^^^^^^^

Goofed off.


Sun 16-Jan-2022
^^^^^^^^^^^^^^^

Continued work on pkg PR#1
(MoaceanParcels)








(/SalishSeaCast/nowcast-env) ~$ python3 -m nowcast.workers.make_plots $NOWCAST_YAML wwatch3 forecast publish
/SalishSeaCast/nowcast-env/lib/python3.9/site-packages/pandas/io/parsers.py:3339: FutureWarning: 
        Use pd.to_datetime instead.

  return generic_parser(date_parser, *date_cols)
/SalishSeaCast/nowcast-env/lib/python3.9/site-packages/pandas/io/parsers.py:3339: FutureWarning: 
        Use pd.to_datetime instead.

  return generic_parser(date_parser, *date_cols)



TODO:
* for MoaceanParcels
  * add disappeared particle kernel w/ Birgit's notebook as docs
  * add docs re: adding pkgs to env
  * add docs re: adding kernels to pkg
  * add GHA CodeQL workflow
  * add pre-commit hooks:
    * pyupgrade

OceanParcels:
* Explore VisibleDeprecationWarning re: constructing ndarrays from lists of ndarrays; parcels/field.py:241 & 243 and commits f8faf9 & ffb6223; do timestamps & datafiles need to be ndarrays, or can they be lists?


TODO:
* Move entry points from setup.py to setup.cfg
  * SalishSeaCmd - done
  * NEMO-Cmd - done
  * MOHID-Cmd - done
  * moad_tools - done
  * Make-MIDOSS-Forcing
  * WWatch3-Cmd
  * also replace setup.py with pyproject.toml ??
    * AtlantisCmd
    * FVCOM-Cmd
    * salishsea-site
    * moad-app-dev
    * rpn-to-gemlam
    * SOG-Bloomcast
    * SOG-Bloomcast-Ensemble
    * SOG-forcing
    * SOG
* add pre-commit hooks:
  * blacken-docs
  * pyupgrade


TODO:
* Python packaging docs and pkg cookiecutters updates:
  * add docs re: pre-commit



TODO:
MIDOSS:
* figure out how to merge/cherrypick relevant changes from Rachael's add_terminal branch in moad_tools

Fix ariane docs:
* maybe re:  adding a bin-like directory to prefix gets rid of errors from doc/ and examples/ that confused Becca ???
 versions re: .bashrc



Update ONC URLs to https://data.oceannetworks.ca/

jupyter kernelspec uninstall unwanted-kernel



TODO:

https://linuxize.com/post/getting-started-with-tmux/

update deployment docs re: spinning up a new compute node


OPPTools PRs:
  add numpy-indexed dependency
  fix pyproj.Proj() initializations
  fix nctime().strftime in OPPTools.utils.fvcom_postprocess.vertical_transect_snap()


15jun20: check mitigation of "index exceeds dimension bounds" IndexError in make_plots fvcom forecast-x2 research

Add VCS revision recording to run_fvcom

Update SalishSeaNowcast fig-dev docs

fix SalishSeaTools unit tests

fix old colander dependency in SOG


Stack:
* create NEMO_Nowcast.workers.spotter to monitor and optionally kill workers that tend to get stuck; initial use cases: collect_weather, make_ww3_wind_file
* wwatch3 run success confirmation
* fix warnings in figure modules
* fix get_vfpa_hadcp MMSI AttributeError issue
* debug gemlam interpolation
Done:
*
