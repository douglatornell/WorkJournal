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
* modules have to be loaded via ~/.bashrc; e.g.
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

-merged dependabot PRs re: pillow:
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
(Numeric Course)

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


Week 3
------

Mon 17-Jan-2022
^^^^^^^^^^^^^^^

upload_forcing arbutus forecast2 failed due to NoValisConnectionError
upload_forcing arbutus nowcast+ failed due to NoValisConnectionError
investigation:
* nowcast0 shut down with no explanation at 16-Jan 22:16 UTC == 14:16 Pacific;
* 16jan/forecast-x2 interrupted
* no 16jan/nowcast-r12
* no 17jan/forecast2 runs
* recovery started at ~10:05
  * restarted nowcast0 from web dashboard at 18:05 UTC == 10:05 Pacific
      sudo apt update
      sudo apt upgrade
      # no need to reboot
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
    * cleaned up stale tmp run dirs in fvcom-runs/ & wwatch3-runs/
  * on skookum:
    * confirmed that there are no stale workers
    * restarted log_aggregator
    * decided to skip forecast2 runs
    * recovery started at ~10:30:
        upload_forcing arbutus nowcast+
        wait for nowcast-r12 to fail at ~17:00
        launch_remote_worker arbutus make_fvcom_boundary arbutus r12 nowcast 2022-01-16
Added uptimerobot ping monitor for arbutus ip (206.12.90.239).
(SalishSeaCast)

UBC-DFO modelling collaboration mtg; discussion of sinking & reflection in SMELT re: adding
sedimentation

Finished work on pkg PR#1; changed it from draft status to ready to review/merge.
(MoaceanParcels)


Tue 18-Jan-2022
^^^^^^^^^^^^^^^

Merged PR#1.
Group mtg:
* presented MoaceanParcels
* feedback:
  * add convention of prefixing kernel func local vars; Jose has had trouble w/ kernel local vars of the same name colliding and crashing pset.execute()
(MoaceanParcels)

Discussed running Olive (java viz app) and using sshfs on Mac w/ Raisha.
Continued work on diatoms nudging fields extraction in analysis-doug/dask-expts/; found weird -1 values in land areas of nav_lon/nav_lat fields in ptrc_T.nc file.
(Atlantis)

* nowcast0 and nowcast6 shut down with no explanation at 18-Jan 21:31 UTC == 13:21 Pacific
* 18jan/forecast-x2 interrupted
* recovery started at ~14:20
  * restarted nowcast0 & nowcast6 from web dashboard at 22:21 UTC == 14:21 Pacific
  * nowcast0
      sudo apt update
      sudo apt upgrade
      sudo shudown -r now
      sudo mount /dev/vdc /nemoShare
      ll /nemoShare/MEOPAR/  # to confirm mount
      sudo mount --bind /nemoShare/MEOPAR /export/MEOPAR
      ll /export/MEOPAR  # to confirm mount
      sudo systemctl start nfs-kernel-server.service
      sudo exportfs -f  # to reset NFS handles for compute nodes
    * nowcast6
        sudo mount -t nfs -o proto=tcp,port=2049 192.168.238.14:/MEOPAR /nemoShare/MEOPAR
    * nowcast0
      # confirm compute nodes have /nemoShare/MEOPAR/ mounted:
      for n in {1..9}; do   echo nowcast${n};   ssh nowcast${n} "mountpoint /nemoShare/MEOPAR"; done
      for n in {1..9}; do   echo nowcast${n};   ssh nowcast${n} "ls -C /nemoShare/MEOPAR"; done
      for n in {0..6}; do   echo fvcom${n};   ssh fvcom${n} "mountpoint /nemoShare/MEOPAR"; done
      for n in {0..6}; do   echo fvcom${n};   ssh fvcom${n} "ls -C /nemoShare/MEOPAR"; done
    * cleaned up stale tmp run dirs in fvcom-runs/
  * on skookum:
    * confirmed that there are no stale workers
    * restarted log_aggregator
    * decided to skip forecast-x2 run
    * recovery started at ~14:45:
        launch_remote_worker arbutus make_fvcom_boundary arbutus r12 nowcast 2022-01-17
        wait for nowcast-r12 to fail at ~21:45
        launch_remote_worker arbutus make_fvcom_boundary arbutus r12 nowcast 2022-01-18
(SalishSeaCast)


Wed 19-Jan-2022
^^^^^^^^^^^^^^^

Continued work on diatoms nudging fields extraction in analysis-doug/dask-expts/:
* changed to use bathymetry dataset to get lon/lat fields
* hit KeyError: 0 issue that Becca hit in mid-Dec;
  debugged and realized that chunksizes has to be list of ints in encoding for to_netcdf() in 
  contrast to dict for open_[mg]dataset()
* started scaling to multiple days using dask.distributed cluster and refactoring code into 
  functions
(Atlantis)

Helped Armaan w/ scikit-learn installtion; confusing because imports are from sklearn.
(SalishSeaCast)

Jose added Stoke's drift kernel to MoaceanParcels :-)
Discussed fieldset code for parcels w/ Jose; agreed to thing about a namespace separate from 
kernels.
(MoaceanParcels)


Thu 20-Jan-2022
^^^^^^^^^^^^^^^

Pullled lab4 from 2020 repo and cleaned up markup.
Created issue #17 re: links to phaustin/numeric
Created issue #18 re: links to specific version(s) of Python docs
Created PR#19 re: updating project info in conf.py; waiting for initial course year from Susan
(Numeric Course)

Phys Ocgy seminar: Acacia Markov, UOttawa: Nature-based solutions for coastal erosion protection
* coastal marsh low plant species diversity

Continued work on diatoms nudging fields extraction in analysis-doug/dask-expts/:
* ran 10d extraction in ~3s on khawla w/ sshfs mount of /results2
* 31d took ~10s, and 265d took ~2m :-)
* files are big due to netCDF classic w/ no deflation; 1.7G for 31d, 4.8G for 365d
* all done in notebook
* uploaded 10d & 31d to /ocean/dlatorne/Atlantis/day-avg-diatoms/ for Raisha
* uploads took longer than extraction :-)
(Atlantis)


Fri 21-Jan-2022
^^^^^^^^^^^^^^^

Answered questions from Jose about MoaceanParcels docs updating.

Cloased PR#19 re: updating project info in conf.py; Susan says initial course yearwas 1995
(Numeric Course)

IOS seminar: Andrea Hilborn, BIO & IOS, remote sensing
Ecosystem monitoring w/ satelite ocean colour and temperature
* Easter Beaufort sub-regions
* Near realtime SST monitoring w/ Charles Hannah
  * R and GitHub Actions:

Continued work on diatoms nudging fields extraction in analysis-doug/dask-expts/:
* extracted code from notebook to module; no significant change in execution time on khawla
* test on salish & tyee; all slower than khawla; spinning disk vs. NVME?
(Atlantis)

Squash-merged dependabot PRs re: numpy, ipython & pillow:
* analysis-doug/melanie-geotiff
* analysis-doug/dask-expts
* SOG-Bloomcast
* tools
* docs
* SOG-Bloomcast-Ensemble
* ECget
(SalishSeaCast)


Sat 22-Jan-2022
^^^^^^^^^^^^^^^

Goofed off!


Sun 23-Jan-2022
^^^^^^^^^^^^^^^

Goofed off!


Week 4
------

Mon 24-Jan-2022
^^^^^^^^^^^^^^^

Investigated make_plots failures:
* wwatch3 forecast publish:
  * dataset not found on /tmp/
      make_plots wwatch3 forecast publish 2022-01-23 --debug worked fine ???
* nowcast-green research:
  * too many indices; file not found
  * possibly related: ERDDAP dataset load failures
      make_plots nemo nowcast-green research 2022-01-23 --debug worked fine ???
HRDPS 12 delayed; started at 07:38, still collecting at 10:10, order looks more random than usual; 
sent email to Sandrine; missing files:
  018:
  CMC_hrdps_west_TMP_TGL_2_ps2.5km_2022012412_P018-00.grib2
  CMC_hrdps_west_PRATE_SFC_0_ps2.5km_2022012412_P018-00.grib2
  032:
  CMC_hrdps_west_DLWRF_SFC_0_ps2.5km_2022012412_P032-00.grib2
  033:
  CMC_hrdps_west_RH_TGL_2_ps2.5km_2022012412_P033-00.grib2
  041:
  CMC_hrdps_west_DLWRF_SFC_0_ps2.5km_2022012412_P041-00.grib2
  043:
  CMC_hrdps_west_PRATE_SFC_0_ps2.5km_2022012412_P043-00.grib2
  044:
  CMC_hrdps_west_TMP_TGL_2_ps2.5km_2022012412_P044-00.grib2
  045:
  CMC_hrdps_west_TMP_TGL_2_ps2.5km_2022012412_P045-00.grib2
  CMC_hrdps_west_RH_TGL_2_ps2.5km_2022012412_P045-00.grib2
  046:
  CMC_hrdps_west_UGRD_TGL_10_ps2.5km_2022012412_P046-00.grib2
  CMC_hrdps_west_UGRD_TGL_10_ps2.5km_2022012412_P046-00.grib2
  048:
  CMC_hrdps_west_APCP_SFC_0_ps2.5km_2022012412_P048-00.grib2
Started collect_weather 18 so that we don't miss more forecast files when/if they appear.
Sandrine confirmed that the issue was known; due to storage and network stability problems; missing 
files landed at ~15:12
(SalishSeaCast)

Restarted ERDDAP server process to try to mitigate large number of recent out of memory errors loading random nowcast-green files:
  sudo /opt/tomcat/bin/shutdown.sh
  wait for uptimerobot notification
  sudo /opt/tomcat/bin/startup.sh
More memory errors on restart
Also, "time_counter are different" errors in month-avg files:
  ERROR in Test.ensureEqual(Strings) line=1 col=25 ''!=' [end]':
  For /results/SalishSea/month-avg.201905/SalishSea_1m_202012_202012_grid_T.nc, the observed and expected values of units for sourceName=time_counter are different.
  Specifically:
  s1 line=1: seconds since 1900-01-01[end]
  s2 line=1: seconds since 1900-01-01 00:00:00[end]
(ERDDAP)

Updated cookiecutter-MOAD-pypkg:
* move .coveragerc contents to pyproject.toml
* add envs/environment-test.yaml template file
(MOAD)


Tue 25-Jan-2022
^^^^^^^^^^^^^^^

collect_weather got messed up due to yesterday shinnanigans;
* one instance of 18 succeeded, but didnt' notify manager, so 00 didn't launch
* another instance of 18 was still running this morning; 
* recovery started at ~10:25:
    download_weather 00 2.5km
    download_weather 06 2.5km
    collect_weather 18 2.5 &
    download_weather 00 1km --yesterday --debug  # failed due to no files on server
    download_weather 12 1km --yesterday --debug
    wait for forecast2 runs to finish
    download_weather 12 2.5km
(SalishSeaCast)

Picked up new UBC Card and sent 

Reviewed blurb about extraction of model variable time series from model product files that I wrote
for Susan's grant from Amber & Michael
(https://docs.google.com/document/d/1JbK14cVIRmQ27hCePCJQf1a_4Jm6obTGBh67tYRy2oo).
Created UBC-MOAD/Reshapr repo on GitHub.
Created Reshapr repo via cookiecutter-MOAD-pypkg on khawla and pushed to GitHub.
Set up Reshapr project on readthedocs and installed integration webhook on GitHub.
(Reshapr)


Wed 26-Jan-2022
^^^^^^^^^^^^^^^

Email from readthedocs re: ecosystem news; stuff I need to look at:
* :external: role for intersphinx
* autosummary extension
* pydata-sphinx-theme: better depth control of left sidebar
* sphinx-codeautolink: gives documented code elements hovers and links to their docs,
  including intersphinx
* sphinxcontrib-constdata
* MyST-Parser=0.17 will provide direct integration with Jupyter; i.e. MyST instead of markdown
  in notebook cells

Deleted /results/SalishSea/nowcast-agrif.201702/01oct21 to 24jan22
* Susan archived them yesterday to archive drives #9 and #10
Discussed w/ Susan moving nowcast-green.201812 to graham:nearline/
* cc wiki was updated 24nov21 to say that nearline now does compression on the way to tape
* tested tarballs built on salish:
  * oct15, no compression: 190G
  * oct15, gzip compression: 174G 136min
  * oct15, bzip2 compression: 177G 615min
(SalishSeaCast)

Slack call w/ Armaan re:
* install SalishSeaTools
* use pathlib
* use VSCode Remote SSH

Pullled lab5 from 2020 repo and cleaned up markup.
(Numeric Course)


Thu 27-Jan-2022
^^^^^^^^^^^^^^^

Email to Peter, Duncan & Maryse re: Economical demutualization pay out.

FAL estate work:
* email to Cameron re: tax return

Coffee w/ Karyn.

Added deisgn & implementation notes docs section; motivation, history
(Reshapr)

Updated khawla OS re: CVE-2021-4034 PwnKit vulnerability.

See work journal.
(Resilient-C)

Phys Ocgy seminar: Connor re: GEOMETRIC eddy parameterization.

Weekly group mtg.
(Atlantis)

EOAS colloquium: Cathie Hickson re: geothermal energy

Updated arbutus.cloud OS re: CVE-2021-4034 PwnKit vulnerability:
* nowcast0
    sudo apt update
    sudo apt upgrade
(SalishSeaCast)


Fri 28-Jan-2022
^^^^^^^^^^^^^^^

Wrote more design & implementation docs; history, Atlantis diatom nudging use case.
(Reshapr)

Helped Karyn try to figure out why evaltools.displayStats() is not applying decimal precision
formatting that is hard-coded in it.
(SalishSeaCast)

Answered Rachael's Slack question re: listing contributors for MIDOSS.
(MIDOSS)


Sat 29-Jan-2022
^^^^^^^^^^^^^^^

Added CLI based on Click using group feature to separate sub-command CLIs into modules; PR#2.
(Reshapr)


Sun 30-Jan-2022
^^^^^^^^^^^^^^^

Added logging framework based on structlog; PR #2.
Started adding extract sub-command; PR #2.
(Reshapr)

download_results nowcast-green to /result2 failed; investigation shows messed up ownership & 
permissions; opened hepdesk ticket
Also noticed a directory called fraser_tars/ ???
(SalishSeaCast)


February
========

Week 5
------

Mon 31-Jan-2022
^^^^^^^^^^^^^^^

Merged PR#2 re: inital dev of extract sub-command.
Started work on dask cluster setup and/or connection; PR#3.
(Reshapr)

Msg from Charles that salish has multiple disk failures.
(SalishSeaCast)

Group mtg; see whiteboard.
(MOAD)


Tue 1-Feb-2022
^^^^^^^^^^^^^^

Learned from Charles that /results2 suffered a 2nd disk failure while RAID was being rebuilt after 1st failure; almost certain total data loss:
* nowcast-green.201905 gone
* nowcast-green.201812 01jul19 to 15feb20 gone; but found those in borg backup on /backup2
* Vicky's MIDOSS gone; inconsequential ???
* yuetal gone; importance ???
* fraser_tars gone; what even was it ???
Discovered that salish does have zstd installed
* ran another nowcast-green.201812/*oct15 tarball test with:
    time tar cvv -I"zstd" -f /ocean/dlatorne/nowcast-green.201812-oct15.tar.zstd \
      nowcast-green.201812/*oct15 | tee /ocean/dlatorne/nowcast-green.201812-oct15.index
  got 177G (same as bzip2) in 38m21s (way faster than gzip or bzip2 or uncompressed)
* repeated uncompressed test with timing: 190G 52m33s !!!
Noted that borg backup of /opp on /backup is incomplete and 31May2020 workjournal provides no explanation of why:
* ran /etc/cron.daily/daily-opp-backup.sh to update backup of /opp/observations/ and 
  /opp/wwatch3/nowcast/
* df -h /backup:
    Filesystem      Size  Used Avail Use% Mounted on
    /dev/sdi1        17T  752G   15T   5% /backup
* added /opp/fvcom/nowcast/ to /etc/cron.daily/daily-opp-backup.sh and ran
* df -h /backup:

* added /opp/fvcom/nowcast-x2/ to /etc/cron.daily/daily-opp-backup.sh and ran
* df -h /backup:
* added /opp/fvcom/nowcast-r12/ to /etc/cron.daily/daily-opp-backup.sh and ran
* df -h /backup:
Created tarball of /results/SalishSea/month-avg.201905/ and uploaded it to graham-dtn:/nearline/SalishSea/nowcast-green.201905/
  time tar cvvf /ocean/dlatorne/nowcast-green.201905-month_avg-jan07-dec20.tar \
    month-avg.201905/* | tee /ocean/dlatorne/nowcast-green.201905-month_avg-jan07-dec20.index
  time rsync -rtlv --partial-dir=/scratch/dlatorne/MEOPAR/SalishSea/rsync-partial -P \
    /ocean/dlatorne/nowcast-green.201905-month_avg-jan07-dec20.* \
    graham-dtn:/nearline/rrg-allen/SalishSea/nowcast-green.201905/
Started build & upload to graham-dtn:/nearline/SalishSea/nowcast-green.201812/ of 1-mo tarballs in tmux session (201812-graham) on chum:
* jan15 uncompressed: tar: 94m rsync: 149m :-(
(SalishSeaCast)


Wed 2-Feb-2022
^^^^^^^^^^^^^^

Helped Susan and Armaan sort out divergence in analysis-armaan between his laptop and chum.
After disappointing performance on chum; started build & upload to graham-dtn:/nearline/SalishSea/nowcast-green.201812/ of 1-mo tarballs in tmux session (201812-graham) on salish:
* feb15 uncompressed: tar: 44m 173G rsync: 102m
* mar15 zstd 1 core: tar: 45m 182G rsync: 114m
* apr15 zstd 2 cores: tar: 40m 181G rsync: 114m
* may15 uncompressed: tar: 52m 202G rsync: 119m
* jun15 uncompressed: tar: 50m 191G rsync: 114m
(SalishSeaCast)

Reviewed Raisha's contaminant-dispersal/SSAM-parse-tracks notebook:
* bare except in cell 67, but is os.remove() even needed with clobber=True in netCDF4.Dataset()?
* I had forgotten how low level working with Dataset() feels compared to using xarray
* ``times.units = "seconds since 1950-01-01 00:00:00 +10"``; does +10 timezone offset matter? 
  why not UTC?
Slack call w/ Raisha; dove down pandas dataframes hole.
(Atlantis)

Created PR#92 from hindcast-log branch on kudu and merged it now that it has been tested in 
production.
Updated GHA workflows to use mambafogrge-pypy3.
Changed optimum-hindcast scratch dir in config re: 201905 re-run.
Deployed above to production.
(SalishSeaNowcast)


Thu 3-Feb-2022
^^^^^^^^^^^^^^

Continued building & uploading to graham-dtn:/nearline/SalishSea/nowcast-green.201812/ 
1-mo tarballs in tmux session (201812-graham) on salish:
* jul15 uncompressed: tar: 49m 203G rsync: 128m
* aug15 uncompressed: tar: 49m 201G rsync: 129m
* ...
**Don't forget about fixtmuxssh bash function to reconnect to ssh agent in new session on salish**
(SalishSeaCast)

FAL estate work:
* compiled info for estate trust 11nov21 income tax return and emailed to Cameron


Fri 4-Feb-2022
^^^^^^^^^^^^^^

Continued building & uploading to graham-dtn:/nearline/SalishSea/nowcast-green.201812/ 
1-mo tarballs in tmux session (201812-graham) on salish: 2016
(SalishSeaCast)

Merged PR#2 re: inital dev of extract sub-command.
Finished work on dask cluster setup and/or connection; merged PR#3.
Did some test framework cleanup; merged PR#4.
(Reshapr)



Sat 5-Feb-2022
^^^^^^^^^^^^^^

PyCascades
* PSF S&I workgroup:
  * awareness survey
  https://docs.google.com/forms/d/e/1FAIpQLSc8957QqYuPDF2qL8Q2ctFzBH_mPMi0yxSQ2oqOACTU9jIVDg/viewform
* Joined PSF as basic member
* PDX GDC and George Floyd protests
  * GDC == General Defense Committee; existed long before 2020 to support arrested labour 
    protesters
  * app mostly scrapes data from various court & govt sites that have no APIs
* Python's tale of concurrency, Pradhvan Bisht
  * concurrency is different from parallelism
  * concurrency: threads or asyncio
  * asyncio event loop pkg uvloop - pluggable, uses cython
  * use tasks to await on multiple coroutines, then gather tasks
  * concurrency is hard! don't undeestimate its complexity
  * resources:
    * Lukasz Langa import asyncio video series
    * Lynn Root blog posts (what we did wrong)
* Buiklding Elegant API Contracts, Neeraj Pandey
  * tools for REST APIs:
    * API blueprint, MSON, Apiary
    * something YAML-based
    * swagger aka openapi - OpenAPI specs
* Cyber Security Investigations w/ Jupyter Notebooks, Ian Hellen
  * MSTICPy pkg by Microsoft 
  * https://github.com/ianhelle/pycascades2022
* How (Not) to Start a Python User Group, Joseph Riddle, Spokane
* Invisible Walls: Isolating Your Python, Jeremiah Paige
  * interpreter isolation: venv, and others
  * userspace isolation: state, conda, containers
    * state looks like an ActiveState "version" of conda
* Literature Text Translation and Audio Synthesis using AI Services, Vivek Raja P S
  * Literature Love project
  * Azure Cognitive Service
* Tests as Classifiers, Moshe Zadka
  * F beta score; harmonic mean to balance precision and recall metrics
  * need to decide on beta; typical range is 0.5 to 2
  * need to collect data about test suite performance; tricky, I think
  * F score is a lagging guide

* nowcast0 shut down with no explanation at 5-Feb 19:10 UTC == 11:10 Pacific; 
  got uptimerobot notification at 11:18
* 5feb/wwatch3-forecast interrupted
* 5feb/forecast-x2 interrupted
* recovery started at ~11:40
  * restarted nowcast0 from web dashboard at 19:40 UTC == 11:40 Pacific
  * nowcast0
      sudo apt update
      # just git 2.35.1
      sudo apt upgrade
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
    * cleaned up stale tmp run dirs in [*]runs/; just wwatch3-forecast
  * on skookum:
    * killed stale workers
    * restarted log_aggregator
    * decided to skip wwatch3-forecast run
    * recovery started at ~11:58:
        launch_remote_worker arbutus make_fvcom_boundary arbutus x2 forecast 2022-02-05
Continued building & uploading to graham-dtn:/nearline/SalishSea/nowcast-green.201812/ 
1-mo tarballs in tmux session (201812-graham) on salish: 2016
* rsync failed for may16
(SalishSeaCast)

Started work on model profile concept and YAML file loader; PR#5.
(Reshapr)


Sun 6-Feb-2022
^^^^^^^^^^^^^^

PyCascades
* Fifty Shades of sign; Rodrigo Girão Serrão, Lisbon
  * @mathsppblog
  * mathspp.com
* Microsoft booth; Python in VSCode; Luciana Abud
  * activate env in terminal has to be configured in settings due to preformance concerns
      settings: activate environment
  * select linter -> flake8
  * format document -> black
  * refactoring via PyLance
  * jump to cursor in debugger lets you jump to code that wouldn't be executed due to condition,
    or jump to a earlier point in execution
  * run/debug config like PyCharm; flask, etc.
    * live reloading
    * justMyCode setting in run/debug config defaults to true; se to false to debug into libraries
  * testing config
    * similar to PyCharm
  * Council Data Project: Infrastructure-as-code for civic transparency and accessibility, Isaac Na
  * Security considerations in Python Packaging, Gajendra Deshpande
    * bandit pkg; checks for security issues via AST

upload_forcing turbidity failed due to too many chained symlinks; resolved by manually symlinking 06feb22 to 27dec21 (last good obs)
nowcast6 node stopped 6feb22 19:27 UTC == 11:27 Pacific
* missing run:
  * 06feb22/forecast-x2
* recovery started at ~17:20
  * restarted nowcast6 from dashboard 7feb22 01:20 UTC == 17:20 Pacific
      sudo mount -t nfs -o proto=tcp,port=2049 192.168.238.14:/MEOPAR /nemoShare/MEOPAR
  * skipped forecast-x2 run
Continued building & uploading to graham-dtn:/nearline/SalishSea/nowcast-green.201812/ 
1-mo tarballs in tmux session (201812-graham) on salish: 2016
* re-did may16; very slow
(SalishSeaCast)

Finished work on model profile YAML file loader; merged PR#5.
Started improving dask cluster loading w/ search pattern from model profile loading; PR#6.
(Reshapr)


Week 6
------

Mon 7-Feb-2022
^^^^^^^^^^^^^^

FAL estate work: reviewed and signed tax return.

More khawla setup work; see notes.

Continued building & uploading to graham-dtn:/nearline/SalishSea/nowcast-green.201812/ 
1-mo tarballs in tmux session (201812-graham) on salish: 2017
(SalishSeaCast)

Finished improving dask cluster loading w/ search pattern from model profile loading; merged PR#6.
Started adding dataset metadata loading; PR#7.
(Reshapr)


Tue 8-Feb-2022
^^^^^^^^^^^^^^

Worked at UBC while Rita was at home.

Continued building & uploading to graham-dtn:/nearline/SalishSea/nowcast-green.201812/ 
1-mo tarballs in tmux session (201812-graham) on salish: finished 2017, started 2018
(SalishSeaCast)

Finished adding dataset metadata loading; merged PR#7.
Enabled dependabot alerts and PRs on GitHub; addressed alert re: pillow<9.0.0; PR#8.
Added CodeQL analysis workflow; PR#9
Started work on extracted variable(s) dataset creation; PR#10.
(Reshapr)


Wed 9-Feb-2022
^^^^^^^^^^^^^^

Continued building & uploading to graham-dtn:/nearline/SalishSea/nowcast-green.201812/ 
1-mo tarballs in tmux session (201812-graham) on salish: finished 2018
(SalishSeaCast)

Finished work on extracted variable(s) dataset creation; PR#10.
(Reshapr)


Thu 10-Feb-2022
^^^^^^^^^^^^^^^

Continued building & uploading to graham-dtn:/nearline/SalishSea/nowcast-green.201812/ 
1-mo tarballs in tmux session (201812-graham) on salish: started 2019; finished to end of jun
(end of what it stored on /results).
collect_river_date failed; 
  KeyError exceptions, 164436480000000000 -> Timestamp("2022-02-09 00:00:00") ->  2022-02-09; investigation:
  * csv files from datamart stopped updating around 07:50 on 8feb
  * sarracenia client log shows connection timeout, then stream of broken pipe errors
* recovery started at ~09:20:
  * restarted sr_subscribe-hydrometric via supervisorctl
  * waited for csv files to update
  * csv files updated at 09:40
  * re-ran workers:
      collect_river_date Capilano 2022-02-09
      collect_river_date ChilliwackVedder 2022-02-09
      collect_river_date ClowhomClowhomLake 2022-02-09
      collect_river_date Englishman 2022-02-09
      collect_river_date HomathkoMouth 2022-02-09
      collect_river_date SalmonSayward 2022-02-09
      collect_river_date SanJuanPortRenfrew 2022-02-09
      collect_river_date SquamishBrackendale 2022-02-09
      collect_river_date TheodosiaScotty 2022-02-09
      collect_river_date TheodosiaBypass 2022-02-09
      collect_river_date TheodosiaDiversion 2022-02-09
      collect_river_date Fraser 2022-02-09
      upload_forcing arbutus nowcast+
      upload_forcing orcinus nowcast+
      upload_forcing optimum nowcast+
      upload_forcing graham-dtn nowcast+
  * nowcast runs started at 10:24
(SalishSeaCast)

FAL estate work: called AST for update and left msg.

Finished work on extracted variable(s) dataset creation; merged PR#10.
Added write to netCDF file; merged PR#11.
Started adding variable groups to 201812 profile; PR#12
(Reshapr)

Weekly mtg.
MEOPAR response workshop on 17-Mar; Raisha & Sara.
(Atlantis)


Fri 11-Feb-2022
^^^^^^^^^^^^^^^

Continued building & uploading to graham-dtn:/nearline/SalishSea/nowcast-green.201812/ 
1-mo tarballs in tmux session (201812-graham) on salish:
* 01jul19 to 15feb20 are in borg archive on /backup2
* can't use * wildcard to tar files from borg mount; resolved by using --from-file to read dirs
  from text file
    jul19
    aug19
Did easy 2022 rollover updates.
(SalishSeaCast)

Finished easy 2022 rollover updates.
(MOAD)

Did easy 2022 rollover updates.
(MIDOSS)

Ran tests on 1h files in analysis-foug/notebooks/dask-expts/atlantis_nudge_diatoms.ipynb to investigate the effect of increasing chunk size by increasing number of hours per chunk:
  1 hr: 54.54 MiB chunks; 240 chunks; 490 tasks; 42.5s
  6 hr: 327.21 MiB chunks; 40 chunks; 90 tasks; 26.4s
  8 hr: 436.28 MiB chunks; 30 chunks; 70 tasks; 27.3s
  12 hr: 654.43 MiB chunks; 20 chunks; 50 tasks; 26.5s
  repeat 1 hr: 54.54 MiB chunks; 240 chunks; 490 tasks; 26.5s !!!
Then 3x all chunk dims:
  163.61 MiB chunks; 80 chunks; 170 tasks; 26.3s
Speed governed by disk and network i/o rates???
(Reshapr)


Sat 12-Feb-2022
^^^^^^^^^^^^^^^

Continued building & uploading to graham-dtn:/nearline/SalishSea/nowcast-green.201812/ 
1-mo tarballs in tmux session (201812-graham) on salish:
* 01jul19 to 15feb20 are in borg archive on /backup2
* can't use * wildcard to tar files from borg mount; resolved by using --from-file to read dirs
  from text file
    sep19
(SalishSeaCast)

Drove to White Rock for Susan to visit J&M; traffic was stupid; waslked in Ruth Johnson Park.


Sun 13-Feb-2022
^^^^^^^^^^^^^^^

Pullled lab7 from 2020 repo and cleaned up markup.
(Numeric Course)

Helped Susan use Reshapr to extract files for Prodigy course; gathered user feedback:
* should there be environment-user.yaml (or some other name)?
Fixed issue #13 that Susan found re: config yaml passed through CLI as str instead Path; PR#14 
(Prodigy Course)


Week 7
------

Mon 14-Feb-2022
^^^^^^^^^^^^^^^

Continued building & uploading to graham-dtn:/nearline/SalishSea/nowcast-green.201812/ 
1-mo tarballs in tmux session (201812-graham) on salish:
* 01jul19 to 15feb20 are in borg archive on /backup2
* can't use * wildcard to tar files from borg mount; resolved by using --from-file to read dirs
  from text file
    oct19
    nov19
    dec19 tarball
nowcast-agrif failed
(SalishSeaCast)

Finished cleanup of lab7.
Fixed phaustin links in lab2 except one I can't resolve; created issue #20 for Susan & Rachel.
(Numeric Course)

Finsiehd adding variable groups to 201812 profile based on feedback from Susan; merged PR#12.
Test suite improvements, including a test for the config yaml type issue #13; merged PR#15.
Added user environment and installation docs; merged PR#16.
Made unused variables list global for model profiles; merged PR#17.
Started work on subset selection for extracted dataset; added time selection; discussed design w/ Susan.
(Reshapr)


Tue 15-Feb-2022
^^^^^^^^^^^^^^^

Investigated nowcast-agrif/14feb failure:
* 13feb also failed
* 12feb timed out
  * looks like upload_forcing failed; confirmed:
    * PasswordRequiredException: Private key file is encrypted
* backfilling:
    upload_forcing orcinus nowcast+ 2022-02-12
    make_forcing_links orcinus nowcast-agrif 2022-02-12
    make_forcing_links orcinus nowcast-agrif 2022-02-13
    make_forcing_links orcinus nowcast-agrif 2022-02-14
    make_forcing_links orcinus nowcast-agrif 2022-02-15
Finished building & uploading to graham-dtn:/nearline/SalishSea/nowcast-green.201812/ 
1-mo tarballs in tmux session (201812-graham) on salish:
* 01jul19 to 15feb20 are in borg archive on /backup2
* can't use * wildcard to tar files from borg mount; resolved by using --from-file to read dirs
  from text file
    dec19 upload
    jan20
    feb20
(SalishSeaCast)

UBC-DFO modeling mtg; Krysten Rutherford, new IOS post-doc, Ph.D. research

Finished work on time selection for extracted dataset; merged PR#18
Added yx grid selection for extracted dataset; merged PR#19
Added execution section to Atlantis use case; added PRODIGY course use case; PR#20
(Reshapr)


Wed 16-Feb-2022
^^^^^^^^^^^^^^^

Verified 1-mo tarballs graham-dtn:/nearline/SalishSea/nowcast-green.201812/.
(SalishSeaCast)

Merged PR#20 re: use case docs.
Added depth selection for extracted dataset; merged PR#21.
Changed to get coordinate names from model profile for source dataset in calc_output_coords(); 
merged PR#22
Installed Reshapr in /ocean/dlatorne/MOAD/ and set up user env; tests:
* set up 8 worker, 10 threads/worker cluster
  * 10d hourly diatoms, 1hr chunks, 1st run: 264s
  * 10d hourly diatoms, 1hr chunks, 2nd run: 267s
  * 10d hourly diatoms, 12hr chunks: 225s
  * 10d hourly diatoms, 24hr chunks: 218s
* changed cluster to 16 workers, 2 threads/worker
  * 10d hourly diatoms, 24hr chunks: 229s
  * 10d hourly diatoms, 4hr chunks: 221s
* changed cluster to 8 workers, 4 threads/worker
  * 10d hourly diatoms, 4hr chunks: 236s
  * 10d hourly diatoms, 4hr chunks, parallel=False in open_mfdataset(): 228s
  * 10d hourly diatoms, 1hr chunks: 242s
* changed cluster to 4 workers, 8 threads/worker
  * 10d hourly diatoms, 1hr chunks: 276s
* changed cluster to 16 workers, 2 threads/worker
  * 10d hourly diatoms, 1hr chunks: 242s
  * 10d hourly diatoms, 24hr chunks: 236s
* changed cluster to 8 workers, 2 threads/worker
  * 10d hourly diatoms, 24hr chunks: 230s
* changed to use engine="h5netcdf" and restarted 8-2 cluster
  * 10d hourly diatoms, 24hr chunks: 221s
  * 31d hourly diatoms, 24hr chunks: 665s
* changed to use engine="netcdf4"
  * 31d hourly diatoms, 24hr chunks: 690s
* can't use h5netcdf in .to_netcdf() due to chunksizes not tuples
(Reshapr)

Pullled lab6 from 2020 repo and cleaned up markup.
(Numeric Course)


Thu 17-Feb-2022
^^^^^^^^^^^^^^^

Debugged gh-pages build failure; ipython 8.0.x depends on black, supposed to be optional,
but it isn't; see https://ubc-eoas.slack.com/archives/C02S3CNV6C9/p1645071587534949
(Numeric Course)

Experimented w/ h5netcdf:
* changed chunksizes to tuples so that h5netcdf can be used by .to_netCDF()
* small test on khawla is inconclusive, or perhaps favours netCDF4 (as I usually find)
    netCDF4: 10.8, 10.2, 9.8, 10.1
    h5netcdf: 11.3, 10.7, 10.9, 10.5, 11.1
* test on salish using 8 worker, 2 threads/worker cluster
  * 31d hourly diatoms, 24hr chunks, w/ nowcast-dev running: 603s, 588s, 598s
* uninstalled netCDF4 from env on salish because it was still showing up in the 
  dask profile flame chart; actually, it wasn't, I mistook xarray/backends/netCDF4.py for it
  * 31d hourly diatoms, 24hr chunks, w/ nowcast-dev running: 600s
* re-created reshapr user env on salish
  * 31d hourly diatoms, 24hr chunks, w/ nowcast-dev finishing: 582s
  * 31d hourly diatoms, 24hr chunks, after nowcast-dev: 642s
* changed cluster to 8 workers, 10 threads/worker
  * 31d hourly diatoms, 24hr chunks, after nowcast-dev: 658s
* changed cluster to 8 workers, 1 threads/worker
  * 31d hourly diatoms, 24hr chunks, after nowcast-dev: 603s
  * 31d hourly diatoms, 24hr chunks, after nowcast-dev: 616s
* added args to open_mfdataset(); 
  concat_dim="time_counter", combine="nested", data_vars="minimal", coords="minimal", 
  compat="override",
  * 31d hourly diatoms, 24hr chunks, after nowcast-dev: 590s
* changed args to open_mfdataset(); 
  data_vars="minimal", coords="minimal", compat="override",
  * 31d hourly diatoms, 24hr chunks, after nowcast-dev: 602s
* changed cluster to 16 workers, 2 threads/worker
  * 31d hourly diatoms, 24hr chunks, after nowcast-dev: 665s
(Reshapr)

See work journal.
Set up warehouse/43ravens/projects/resilient-c/ dir on khawla; see setup notes.
(Resilient-C)

Weekly project mtg.
(Atlantis)

Did ramp test on Zwift; some calf cramping during ride.


Fri 18-Feb-2022
^^^^^^^^^^^^^^^

Pullled lab8 from 2020 repo and cleaned up markup.
(Numeric Course)

Sore calves during and after climby Zwift ride.


Sat 19-Feb-2022
^^^^^^^^^^^^^^^

Downloaded 1.18.1 versions of MaLiLib, MiniHUD & Litematica (beta) 
from curseforge.com and installed them.

Calves sore again after easy Zwift ride.


Sun 20-Feb-2022
^^^^^^^^^^^^^^^

Goofed off!

Walked to English Bay overlook then looped home via Cypress and bank;
calves a little sore, legs tired. No Zwift ride.


Week 8
------

Mon 21-Feb-2022
^^^^^^^^^^^^^^^

**Statutory Holiday** - Family Day

manager restarted overnight due to name resolution errors during nowcast-r12 run;
interupted hindcast runs; no log messages from watch_fvcom; restarted log_aggregator at ~19:40
(SalishSeaCast)

Started updating transactions for 2021 tax returns.

More khawla setup work; see notes.


Tue 22-Feb-2022
^^^^^^^^^^^^^^^

Worked at ESB while Rita was at home.

Group mtg:
* Birgit presented on her attempt to use parcels to back track Mn tracer;
  problem with time origin type in field set the combines velocity components
  and Mn field; consensus was to put Mn field in a separate fieldset
(Ocean Parcels)

Read xarray code to confirm that open_mfdataset() args:
  data_vars="minimal", coords="minimal", compat="override",
that are sufficient for `reshapr extract` do actually reduce the checks and work
done in the concatenate/merge functions. So, it is reasonable to expect that
they provide a small performance win.
Finished change from netCDF4 to h5netcdf engine for xarray; merged PR#23.
Discovered that ncdump is installed with netCDF4, so missing now from 
reshapr-dev env.
Also discovered that ncdump -t doesn't convert times to strings for 
netCDF4 files written by h5netcdf.
Without netcdf4 in reshapr, need pydap to access SSC ERDDAP geo ref dataset.
(Reshapr)


Wed 23-Feb-2022
^^^^^^^^^^^^^^^

Looked at lab9 and lab10 but they are both not in the same pattern as earlier labs;
need to consult w/ Susan.
(Numeric Course)

Reverted change from netCDF4 to h5netcdf; merged PR#24.
Started adding handling of surface variables that don't have a depth coordinate; PR#25
(Reshapr)

* nowcast0 shut down with no explanation at 23-Feb 21:07 UTC == 13:07 Pacific; 
  got uptimerobot notification at 13:13
* 23feb/forecast-x2 interrupted
* recovery started at ~13:30
  * restarted nowcast0 from web dashboard at 21:31 UTC == 13:31 Pacific
  * nowcast0
      sudo apt update
      sudo apt upgrade
      sudo mount /dev/vdc /nemoShare
      ll /nemoShare/MEOPAR/  # to confirm mount
      sudo mount --bind /nemoShare/MEOPAR /export/MEOPAR
      ll /export/MEOPAR  # to confirm mount
      sudo systemctl start nfs-kernel-server.service
      sudo exportfs -f  # to reset NFS handles for compute nodes
      # confirm compute nodes have /nemoShare/MEOPAR/ mounted:
      for n in {1..9}; do   echo nowcast${n};   ssh nowcast${n} "mountpoint /nemoShare/MEOPAR"; done
      for n in {1..9}; do   echo nowcast${n};   ssh nowcast${n} "ls -CF /nemoShare/MEOPAR"; done
      for n in {0..6}; do   echo fvcom${n};   ssh fvcom${n} "mountpoint /nemoShare/MEOPAR"; done
      for n in {0..6}; do   echo fvcom${n};   ssh fvcom${n} "ls -CF /nemoShare/MEOPAR"; done
    * cleaned up stale tmp run dirs in [*]runs/; just fvcom-forecast-x2
  * on skookum:
    * killed stale workers
    * restarted log_aggregator
    * decided to skip fvcom-forecast-x2 run
    * recovery started at ~14:01:
        launch_remote_worker arbutus make_fvcom_boundary "arbutus r12 nowcast 2022-02-23"
(SalishSeaCast)


Thu 24-Feb-2022
^^^^^^^^^^^^^^^

collect_weather 12 had not completed at 09:45; investigation:
* no errors in sarracenia log
* 493 of 576 files downloaded
* missing files in almomst all hours
* moved 12/ aside and tried to start recovery with download_weather, but it failed too
* moved 12.aside/ back so that collect_weather can finish its job, I hope
* sent email to Sandrine
* collect_weather 12 finished at ~11:51
(SalishSeaCast)

Discussed w/ Raisha in Slack Atlantis executable name item in YAML
and new -m flag for migration files:
* created issue #4 re: -m flag
* created issue #5 re: Atlantis executable name
Did year rollover code maint; merged PR#6.
Changed to Python 3.10 for dev; merged PR#7.
Changed GHA linkcheck & CI workflows to use mambafogrge-pypy3;
also changed all GHA worksflows to only run on-push, not on-pull-request; merged PR#8.
Did pre-commit autoupdate.
Started to scope adding Atlantis executable name to YAML file re: issue #5
Weekly mtg:
* Beth confirmed that -m is new required flag for migration params file that she has split
  out to handle things like salmon migration
(Atlantis)

Finished adding handling of surface variables that don't have a depth coordinate; mergd PR#25.
Started adding HRDPS model profiles.
(Reshapr)


Fri 25-Feb-2022
^^^^^^^^^^^^^^^

Added Atlantis executable name to YAML file re: issue #5; merged PR#9.
(Atlantis)

Slack call w/ Armaan re: memory use and jupyter lab variable inspector.

* nowcast0 shut down with no explanation at 25-Feb 20:31 UTC == 12:31 Pacific; 
  got uptimerobot notification at 12:45
* 25feb/forecast-x2 interrupted
* recovery started at ~14:50
  * restarted nowcast0 from web dashboard at 22:52 UTC == 14:52 Pacific
  * nowcast0
      sudo apt update  # all up to date
      sudo mount /dev/vdc /nemoShare
      ll /nemoShare/MEOPAR/  # to confirm mount
      sudo mount --bind /nemoShare/MEOPAR /export/MEOPAR
      ll /export/MEOPAR  # to confirm mount
      sudo systemctl start nfs-kernel-server.service
      sudo exportfs -f  # to reset NFS handles for compute nodes
      # confirm compute nodes have /nemoShare/MEOPAR/ mounted:
      for n in {1..9}; do   echo nowcast${n};   ssh nowcast${n} "mountpoint /nemoShare/MEOPAR"; done
      for n in {1..9}; do   echo nowcast${n};   ssh nowcast${n} "ls -CF /nemoShare/MEOPAR"; done
      for n in {0..6}; do   echo fvcom${n};   ssh fvcom${n} "mountpoint /nemoShare/MEOPAR"; done
      for n in {0..6}; do   echo fvcom${n};   ssh fvcom${n} "ls -CF /nemoShare/MEOPAR"; done
    * cleaned up stale tmp run dirs in [*]runs/; just fvcom-forecast-x2
  * on skookum:
    * killed stale workers
    * restarted log_aggregator
    * decided to skip fvcom-forecast-x2 run
    * recovery started at ~15:00:
        launch_remote_worker arbutus make_fvcom_boundary "arbutus r12 nowcast 2022-02-25"
(SalishSeaCast)


Sat 26-Feb-2022
^^^^^^^^^^^^^^^

Drove to White Rock for Susan to visit J&M; walked in Ruth Johnson Park.


Sun 27-Feb-2022
^^^^^^^^^^^^^^^

nowcast6 node stopped 27feb22 10:14 UTC == 02:14 Pacific
* no missing runs
* recovery started at ~12:10
  * restarted nowcast6 from dashboard 27feb22 20:09 UTC == 12:09 Pacific
      sudo mount -t nfs -o proto=tcp,port=2049 192.168.238.14:/MEOPAR /nemoShare/MEOPAR
  * skookum:
      launch_remote_worker arbutus make_fvcom_boundary "arbutus x2 nowcast 2022-02-27"
(SalishSeaCast)


March
=====

Week 9
------

Mon 28-Feb-2022
^^^^^^^^^^^^^^^

Group mtg; see whiteboard.
(MOAD)

Added Atlantis -m flag for migrations .csv re: issue #4; merged PR#11.
(Atlantis)

Started work on adding HRDPS model profiles for extractions.
(Reshapr)


Tue 1-Mar-2022
^^^^^^^^^^^^^^

Continued work on adding HRDPS model profiles for extractions.
(Reshapr)

salishsea-site went down at 16:36; investigation:
* /SalishSeaCast report i/o error
* opened helpdesk ticket
(SalishSeaCast)


Wed 2-Mar-2022
^^^^^^^^^^^^^^

SalishSeaCast status:
* processes on skookum:
    pgrep -af nowcast
    4597 /SalishSeaCast/nowcast-env/bin/python /SalishSeaCast/nowcast-env/bin/supervisord -c /SalishSeaCast/SalishSeaNowcast/config/supervisord.ini
    10192 /SalishSeaCast/nowcast-env/bin/python3 -m nowcast.workers.collect_weather /SalishSeaCast/SalishSeaNowcast/config/nowcast.yaml 00 2.5km
    21787 /SalishSeaCast/nowcast-env/bin/python3 -m nowcast.workers.make_surface_current_tiles /SalishSeaCast/SalishSeaNowcast/config/nowcast.yaml forecast2 --run-date 2022-02-28
    27796 /SalishSeaCast/nowcast-env/bin/python3 -m nowcast.workers.make_surface_current_tiles /SalishSeaCast/SalishSeaNowcast/config/nowcast.yaml forecast2 --run-date 2022-02-28
    29500 /SalishSeaCast/nowcast-env/bin/python -m nemo_nowcast.message_broker /SalishSeaCast/SalishSeaNowcast/config/nowcast.yaml
    * nothing useful; kill them all
* interrupted runs:
  * NONE!!!
  * nowcast-r12/01mar22 needs to be downloaded
* last weather download:
  * /results/forcing/atmospheric/GEM2.5/GRIB/20220301/18
* processes on arbutus:
    pgrep -af nowcast
    6316 bash -c source /nemoShare/MEOPAR/nowcast-sys/nowcast-env/etc/conda/activate.d/envvars.sh ; /nemoShare/MEOPAR/nowcast-sys/nowcast-env/bin/python3 -m nowcast.workers.watch_fvcom /nemoShare/MEOPAR/nowcast-sys/SalishSeaNowcast/config/nowcast.yaml arbutus.cloud-nowcast r12 nowcast
    6317 /nemoShare/MEOPAR/nowcast-sys/nowcast-env/bin/python3 -m nowcast.workers.watch_fvcom /nemoShare/MEOPAR/nowcast-sys/SalishSeaNowcast/config/nowcast.yaml arbutus.cloud-nowcast r12 nowcast

Plan for temporary replacement of /SalishSeaCast:
* replace miniconda3 with mambafogrge-pypy3
* build new deployment in /data/SalishSeaCast/
Deployment:
  on salish:
    sudo mkdir -m 755 /data/SalishSeaCast
    sudo chown dlatorne:sallen /data/SalishSeaCast
  on skookum:
    cd ~
    curl -L -O https://github.com/conda-forge/miniforge/releases/latest/download/Mambaforge-pypy3-$(uname)-$(uname -m).sh
    bash ~/Mambaforge-pypy3-$(uname)-$(uname -m).sh
    # allowed installer to run conda init
    # new shell
    conda config --set auto_activate_base false
    # edit .condarc
      channels:
        - conda-forge
        - nodefaults

      show_channel_urls: true

      envs_dirs:
        - /home/dlatorne/conda_envs

      auto_activate_base: false
    # new shell
    rm Miniconda3-latest-Linux-x86_64.sh
    rm -rf miniconda3/
    # follow deployment docs w/ exceptions noted here; 
    # see also Wed 7-Apr-2021 notes from last deployment update
    cd /data/SalishSeaCast/
    # clone repos
    # change SalishSeaNowcast/envs/environment-prod.yaml to use Python 3.10
    # create nowcast-env
    # install pkgs
    # change SalishSeaNowcast/envs/environment-sarracenia.yaml to use Python 3.10
    # create sarracenia-env
    # change salishsea-site/envs/environment-prod.yaml to use Python 3.10
    # create salishsea-site-env
    # installed pkg
    # set up envvars in 3 envs
    # set up runs/ dir
    # set up datamart/ dirs
    # set up logs/ dirs
    # restore large uncommitted tidal_predictions/ files:
      cp --preserve=timestamps /home/sallen/MEOPAR/ANALYSIS/analysis-storm-surges/notebooks/tide_analysis_scripts/*2030.csv SalishSeaNowcast/tidal_predictions/
    # changed links in /results/nowcast-sys/figures/salishsea-site/static/img/index_page

    # sort out OPPTools issues; see git diff on arbutus & Wed 7-Apr-2021 notes
    # build XIOS
    # build NEMO SalishSeaCast_blue for nowcast-dev

* fix docs
  * re: creating runs/ dir
  * re: namelist.time_nowcast_template
      maybe ../SS-run-sets/SalishSea/nemo3.6/nowcast/namelist.time_nowcast_template ???
  * path typos in cold start
  * add 00/ 06/ 12/ 18/ to datamart/hrdps-west/

Automation recovery:
* started automation at 12:51
* recovery:
    rmdir /results/forcing/atmospheric/GEM2.5/GRIB/20220302/00
    download_weather 00 2.5km
    download_weather 06 2.5km
* notifications going to my DMs on Slack, not ssc-daily-progress
  * fixed webhook URL envvar
  * stopped and re-started everything
* collect_river_data failed due to no hydrometric .csv files
* collect_river_data failed due to /SalishSeaCast path for .csv files
* grib_to_netcdf failed due to /SalishSeaCast path for wgrib2
* make_ssh_files failed due to /SalishSeaCast path for tidal_predictions
* get_onc_ctd failed due to invalid netcdf backend; might be due to another /SalishSeaCast path
* editted nowcast.yaml to change /SalishSeaCast to /data/SalishSeaCast

* recovery cont'd:
  # wait for sarracenia to grab hydrometric .csv files
    rm -rf /results/forcing/atmospheric/GEM2.5/GRIB/20220302/06
    download_weather 06 2.5km
  # collect_river_data succeeded
  # collect_NeahBay_ssh succeeded
  # forecast2 run failed; maybe wrong date; don't really care
    download_weather 12 2.5km
  # nowcast-blue running !!
    download_fvcom_results r12 nowcast 2022-03-01
    collect_weather 00 2.5km &
    rm -rf datamart/hrdps-west/18/*
    download_weather 18 2.5km
    download_weather 00 1km
    download_weather 12 1km
  # make_turbidity_file failed due to
  # pandas._config.config.OptionError: Pattern matched multiple keys (below)
    ln -s /results/forcing/rivers/river_turb/riverTurbDaily2_y2022m03d01.nc riverTurbDaily2_y2022m03d02.nc
    upload_forcing arbutus turbidity
    upload_forcing optimum turbidity  # failed: PasswordRequiredException: Private key file is encrypted
    upload_forcing orcinus turbidity  # failed: PasswordRequiredException: Private key file is encrypted
    upload_forcing graham turbidity  # hung

Lots of:
  2022-03-02 14:42:20,471 ERROR [make_plots] unexpected TypeError in make_figure:
  Traceback (most recent call last):
    File "/data/SalishSeaCast/SalishSeaNowcast/nowcast/workers/make_plots.py", line 1102, in _calc_figure
      fig = fig_func(*args, **kwargs)
    File "/data/SalishSeaCast/SalishSeaNowcast/nowcast/figures/fvcom/research/thalweg_transect.py", line 63, in make_figure
      plot_data = _prep_plot_data(place, fvcom_results_dataset, time_index, varname)
    File "/data/SalishSeaCast/SalishSeaNowcast/nowcast/figures/fvcom/research/thalweg_transect.py", line 125, in _prep_plot_data
      xx, zz, vi, _, __, ___ = fpp.vertical_transect_snap(
    File "/data/SalishSeaCast/OPPTools/OPPTools/utils/fvcom_postprocess.py", line 843, in vertical_transect_snap
      timestr = datetime.strftime(nctime(f,ktime), ' %Y-%m-%d %H:%M UTC')
  TypeError: descriptor 'strftime' for 'datetime.date' objects doesn't apply to a 'cftime._cftime.DatetimeGregorian' object

This looks like a new one:
  2022-03-02 15:32:01,643 CRITICAL [make_turbidity_file] unhandled exception:
  Traceback (most recent call last):
    File "/data/SalishSeaCast/NEMO_Nowcast/nemo_nowcast/worker.py", line 391, in _do_work
      checklist = self.worker_func(
    File "/data/SalishSeaCast/SalishSeaNowcast/nowcast/workers/make_turbidity_file.py", line 111, in make_turbidity_file
      itdf = _interpTurb(tdf, idateDD, mthresh)
    File "/data/SalishSeaCast/SalishSeaNowcast/nowcast/workers/make_turbidity_file.py", line 164, in _interpTurb
      pd.set_option("precision", 9)
    File "/data/SalishSeaCast/nowcast-env/lib/python3.10/site-packages/pandas/_config/config.py", line 256, in __call__
      return self.__func__(*args, **kwds)
    File "/data/SalishSeaCast/nowcast-env/lib/python3.10/site-packages/pandas/_config/config.py", line 149, in _set_option
      key = _get_single_key(k, silent)
    File "/data/SalishSeaCast/nowcast-env/lib/python3.10/site-packages/pandas/_config/config.py", line 116, in _get_single_key
      raise OptionError("Pattern matched multiple keys")
  pandas._config.config.OptionError: Pattern matched multiple keys

Also couple of new?:
  2022-03-02 17:21:13,598 ERROR [make_plots] unexpected TypeError in make_figure:
  Traceback (most recent call last):
    File "/data/SalishSeaCast/SalishSeaNowcast/nowcast/workers/make_plots.py", line 1102, in _calc_figure
      fig = fig_func(*args, **kwargs)
    File "/data/SalishSeaCast/SalishSeaNowcast/nowcast/figures/fvcom/publish/second_narrows_current.py", line 68, in make_figure
      plot_data = _prep_plot_data(place, fvcom_stns_datasets, obs_dataset)
    File "/data/SalishSeaCast/SalishSeaNowcast/nowcast/figures/fvcom/publish/second_narrows_current.py", line 123, in _prep_plot_data
      obs = xarray.Dataset(
    File "/data/SalishSeaCast/nowcast-env/lib/python3.10/site-packages/xarray/core/dataset.py", line 749, in __init__
      variables, coord_names, dims, indexes, _ = merge_data_and_coords(
    File "/data/SalishSeaCast/nowcast-env/lib/python3.10/site-packages/xarray/core/merge.py", line 483, in merge_data_and_coords
      return merge_core(
    File "/data/SalishSeaCast/nowcast-env/lib/python3.10/site-packages/xarray/core/merge.py", line 632, in merge_core
      collected = collect_variables_and_indexes(aligned)
    File "/data/SalishSeaCast/nowcast-env/lib/python3.10/site-packages/xarray/core/merge.py", line 291, in collect_variables_and_indexes
      variable = as_variable(variable, name=name)
    File "/data/SalishSeaCast/nowcast-env/lib/python3.10/site-packages/xarray/core/variable.py", line 110, in as_variable
      raise TypeError(
  TypeError: Using a DataArray object to construct a variable is ambiguous, please extract the data using the .data property.

  2022-03-02 18:56:26,443 ERROR [make_plots] unexpected KeyError in make_figure:
  Traceback (most recent call last):
    File "/data/SalishSeaCast/SalishSeaNowcast/nowcast/workers/make_plots.py", line 1102, in _calc_figure
      fig = fig_func(*args, **kwargs)
    File "/data/SalishSeaCast/SalishSeaNowcast/nowcast/figures/wwatch3/wave_height_period.py", line 66, in make_figure
      plot_data = _prep_plot_data(buoy, wwatch3_dataset_url)
    File "/data/SalishSeaCast/SalishSeaNowcast/nowcast/figures/wwatch3/wave_height_period.py", line 95, in _prep_plot_data
      obs = moad_tools.observations.get_ndbc_buoy(buoy)
    File "/data/SalishSeaCast/moad_tools/moad_tools/observations.py", line 108, in get_ndbc_buoy
      df = df.rename(index=str, columns=columns).set_index("time").sort_index()
    File "/data/SalishSeaCast/nowcast-env/lib/python3.10/site-packages/pandas/util/_decorators.py", line 311, in wrapper
      return func(*args, **kwargs)
    File "/data/SalishSeaCast/nowcast-env/lib/python3.10/site-packages/pandas/core/frame.py", line 5488, in set_index
      raise KeyError(f"None of {missing} are in the columns")
  KeyError: "None of ['time'] are in the columns"

Website recovery:
* changed log path in production.ini to /data/SalishSeaCast/...
(SalishSeaCast)


Thu 3-Mar-2022
^^^^^^^^^^^^^^

Merged main into py310 branch of SalishSeaNowcast; built new dev env
SalishSeaCast ops mgmt:
* make_turbidity_file failed due to pandas OptionError; persist:
    ln -s /results/forcing/rivers/river_turb/riverTurbDaily2_y2022m03d02.nc riverTurbDaily2_y2022m03d03.nc
    upload_forcing arbutus turbidity
* upload_forcing to graham-dtn is working today
Finished update of SalishSeaNowcast to Python 3.10 for dev & prod; merged PR#93.
Created issue #94 re: pandas OptionError in make_turbidity_file; root cause is unnecessary 
setting of display precision for pandas that was not robust for future changes; deleted; PR#95
Pulled PR#95 branch on to skookum for production testing tomorrow.
(SalishSeaCast)

Henryk power cycled salish at ~15:45.


Fri 4-Mar-2022
^^^^^^^^^^^^^^

Test of PR#95 branch re: re: pandas OptionError in make_turbidity_file in produciton succeded; 
merged PR#95 and updated skookum.
/results2 is back; 90Tb !!
  * created /result2/SalishSea/nowcast-green.201905
/SalishSeaCast is back; not corrupted?
(SalishSeaCast)

Cleaned up labs 9 and 10.
(Numeric Course)

Started work on setting up 2022 bloomcast:
* see khawla setup notes
* khawla:
  * cloned SOG-Bloomcast-Ensemble
  * cloned SOG
  * changed colander=1.5.1 dependency to install via pip
    * not available from conda-forge
    * can get from defaults, but that forces env to use Python 3.7
  * editable installs of SOG & SOG-Bloomcast-Ensemble
  * SOG-Bloomcast-Ensemble test suite ran successfully
  * mkdir run/2021
  * cp run/2021_bloomcast_inifile.yaml run/2022_bloomcast_infile.yaml
  * mv run/2021_bloomcast_inifile.yaml run/2021/
  * committed archive of 2021 SOG YAML infile
  * edit run/2022_bloomcast_infile.yaml
  * edit run/config/yaml
    * have to continue to use Nanaimo River at Cassidy as estimate of Englishman at Parksville
      because the Englishman data stream did not resume until 30-Apr-2021
  * tested run prep w/ SOG runs and publish to web disabled
  * committed run/2022_bloomcast_infile.yaml and run/config.yaml
* salish:ount
  * created new bloomcast env
  * runs dir: /data/dlatorne/SOG-projects/SOG-Bloomcast-Ensemble/run
  * archived 2021_bloomcast* files in run/2021/
  * archived Englishman_flow Fraser_flow Sandheads_wind in run/2021/
  * archived YVR_* in run/2021/
  * ran test w/ push to web disabled:
      INFO:bloomcast.ensemble:Predicted earliest bloom date is 2022-03-10
      INFO:bloomcast.ensemble:Earliest bloom date is based on forcing from 1983/1984
      INFO:bloomcast.ensemble:Predicted early bound bloom date is 2022-03-13
      INFO:bloomcast.ensemble:Early bound bloom date is based on forcing from 1991/1992
      INFO:bloomcast.ensemble:Predicted median bloom date is 2022-03-20
      INFO:bloomcast.ensemble:Median bloom date is based on forcing from 1999/2000
      INFO:bloomcast.ensemble:Predicted late bound bloom date is 2022-04-06
      INFO:bloomcast.ensemble:Late bound bloom date is based on forcing from 1998/1999
      INFO:bloomcast.ensemble:Predicted latest bloom date is 2022-04-07
      INFO:bloomcast.ensemble:Latest bloom date is based on forcing from 2008/2009
  * enabled cron job41
(Bloomcast)

Added SOG-projects/ to khawla; see setup notes.


Sat 5-Mar-2022
^^^^^^^^^^^^^^

Fixed conda bin path in cron job script; ran bloomcast via cron job script.
(Bloomcast)

Fiddled around with NFS mounts on skookum until I was able to get /SalishSeaCast and /results2
mounted:
* exportfs -f on salish didn't do the job for skookum, but may have to chum, tyee & lox
* needed to do umount -f on skookum, but that fails until all refs to fd have been eliminated
* found fs refs via ls -l /proc/*/fd/
* lots of hung refs to /SalishSeaCast, but /results2 was easier
Downloaded jan22 results from arbutus via bash loop.
(SalishSeaCast)


Sun 6-Mar-2022
^^^^^^^^^^^^^^

First automated run of bloomcast.
Looking at predictions and weather forecast, my guess is 17-Mar.
(Bloomcast)

Downloaded feb22 results from arbutus via bash loop.
Started building 1-mo tarballs of nowcast-green.2019105 in tmux session on chum 
and uploading to graham-dtn:/nearline; jan22
(SalishSeaCast)

Rode Zwift Gran Fondo ~25 min faster than on 31-Dec.


Week 10
-------

Mon 7-Mar-2022
^^^^^^^^^^^^^^

Group mtg; see whiteboard.
(MOAD)

Continued building 1-mo tarballs of nowcast-green.2019105 in tmux session on chum 
and uploading to graham-dtn:/nearline:
* jan22 rsync failed due to typos in command chain; re-ran
Downloaded 01-04mar22 results from arbutus via bash loop; re-enabled nowcast-green >30d old 
results purge cron task on arbutus
Restored /SalishSeaCast is not the one that disappeared last week; restored one has hg clones ???
Hacked OPPTools changes to avoid ~1000 error/day into /data/SalishSeaCast/OPPTools/
from khawal clone:
* OPPTools/fvcomToolbox/fvcomToolbox.py re: pyproj.Proj() arg
* OPPTools/utils/fvcom_postprocess.py re: nctime() call
* OPPTools/utils/__init__.py import that leads to ttide was commented out by Maxim in aa98ada
Created issue #96 re: upload_forcing to orcinus and optimum fails w/ "Private key file is encrypted"
* root cause is that orcinus and optimum ssh servers are too old to send server-sig-algs
  and paramiko>2.9 defaults to using rsa-sha2-512 which they don't seem to support
* optimum has openssh=5.3
* orcinus has openssh=6.0
(SalishSeaCast)


Tue 8-Mar-2022
^^^^^^^^^^^^^^

SoPO day 1:
* Farron:
  * normally warm year despite summer heat
  * failed La Niña in spring
  * very wet autumn
* Tetania:
  * freshening in NE Pacific over past 5 yrs

* TODO:
  * Look at CIOOS as data source; e.g. Halibut Bank per Andrea Hilborn

Finished work on issue #96 re: upload_forcing to orcinus and optimum fails with
"Private key file is encrypted"; created PR#97
* pull branch on skookum to test in production
Backfilled upload_forcing to orcinus and optimum.
Started backfilling nowcast-agrif runs:
  make_forcing_links orcinus nowcast-agrif 2022-03-02
  make_forcing_links orcinus nowcast-agrif 2022-03-03
  make_forcing_links orcinus nowcast-agrif 2022-03-04
  make_forcing_links orcinus nowcast-agrif 2022-03-05
  make_forcing_links orcinus nowcast-agrif 2022-03-06
  make_forcing_links orcinus nowcast-agrif 2022-03-07
  make_forcing_links orcinus nowcast-agrif 2022-03-08
(SalishSeaCast)

EOAS mail migration to mail.ubc.ca


Wed 9-Mar-2022
^^^^^^^^^^^^^^

Started using mail.ubc.ca web mail instead of Thunderbird on khawla.

SoPO day 2

Merged PR#91 re: issue #96 - upload_forcing to orcinus and optimum fails with
"Private key file is encrypted"; finalized deployment ot production.
Helped Susan update config to download 201905 re-run on optimum to nowcast-green.201905.
Started backfilling nowcast-dev runs:
  built XIOS-2
  built NEMO SalishSeaCast_Blue config
(SalishSeaCast)

Susan traced problem re-starting hindcast.201905 on optimum to needing omega login node that 
Henryk told us to use integrated into SalishSeaCmd; did so.
optimum's ancient ssh client doesn't like my new ed25519 key, causing it to be unable to interact
with GitHub; resolved by adding salishsea-nowcast-deployment_id_rsa deployment key to SalishSeaCmd
on GitHub.
(SalishSeaCmd)


Thu 10-Mar-2022
^^^^^^^^^^^^^^^

SoPO day 3

Created nowcast-dev/09mar22/ directory containing namelist_cfg and restart.nc from nowcast-green.201905/09mar22/ so that nowcast-dev can start
  make_forcing_links salish nowcast+ --shared-storage --run-date 2022-03-10
(SalishSeaCast)


Fri 11-Mar-2022
^^^^^^^^^^^^^^^

FAL estate work:
* updated distribution spreadsheet
* tried to figure out how to use DRS statement to get BCE shares into DI account;
  phone fail - bounced to estate dept.; Monica is no longer at TD branch

Year rollover codebase maintenance; PR#14; merged
* bump version to 22.1.dev0
* update copyright year range
* change copyright holder to SalishSeaCast Project Contributors
* add SPDX short-form license identifiers
* rename to .readthedocs.yaml
* change to new readthedocs build spec API & mambaforge-4.10
Improve GHA workflows; PR#15
* change to run GHA workflows on push to any branch
* drop pkg caching from GHA linkcheck & CI workflows
* chg GHA linkcheck & CI workflows to use mambaforge
Change to Python 3.10 for pkg dev; PR#
* add 3.10 to GHA pytest-coverage workflow
* change to 3.10 in GHA linkcheck workflow
* change to Python 3.10 for pkg dev
* update pkgs & versions used in revent dev env
Released SalishSeaCmd v22.1 re: Compute Canada StdEnv/2020, omega node on optimum, etc.;
also a test of auto-generated release notes on GitHub; I was correct in my expectation that
release notes come from PRs not commits; contributors list & change log link are nice too.
(SalishSeaCmd)


Sat 12-Mar-2022
^^^^^^^^^^^^^^^

Drove to White Rock for Susan to visit J&M; walked in Ruth Johnson Park.

Dinner from La Quercia deli.


Sun 13-Mar-2022
^^^^^^^^^^^^^^^

Squash-merged dependabot PRs re: pillow:
* moad_tools
* tools
* analysis-doug/melanie-geotiff
* analysis-doug/dask-expts
(SalishSeaCast)


Week 11
-------

Mon 14-Mar-2022
^^^^^^^^^^^^^^^

Resolved nvidia driver update problem on khawla thanks to apt & dpkg dance on 
https://support.system76.com/articles/package-manager-pop/

Got my phone connected to new FASMail EOAS mail account w/ extra long PIN for UBC.

Group mtg; first hybrid; see whiteboard.
(MOAD)

Dug up docs re: creating atmospheric forcing interpolation weights for NEMO re:
GEMLAM and downscaling; see https://salishseacast.slack.com/archives/C02TDP862N6/p1647290291220139
Wave plots failed due to change to DST

nowcast0 shut down with no explanation at 14-Mar 20:44 UTC == 13:44 Pacific; 
got uptimerobot notification at 13:49
* 14mar/forecast-x2 interrupted
* recovery started at ~15:10
  * restarted nowcast0 from web dashboard at 22:13 UTC == 15:13 Pacific
  * nowcast0
      sudo apt update
      sudo apt upgrade  # 2 pkgs
      sudo mount /dev/vdc /nemoShare
      ll /nemoShare/MEOPAR/  # to confirm mount
      sudo mount --bind /nemoShare/MEOPAR /export/MEOPAR
      ll /export/MEOPAR  # to confirm mount
      sudo systemctl start nfs-kernel-server.service
      sudo exportfs -f  # to reset NFS handles for compute nodes
      # confirm compute nodes have /nemoShare/MEOPAR/ mounted:
      for n in {1..9}; do   echo nowcast${n};   ssh nowcast${n} "mountpoint /nemoShare/MEOPAR"; done
      for n in {1..9}; do   echo nowcast${n};   ssh nowcast${n} "ls -CF /nemoShare/MEOPAR"; done
      for n in {0..6}; do   echo fvcom${n};   ssh fvcom${n} "mountpoint /nemoShare/MEOPAR"; done
      for n in {0..6}; do   echo fvcom${n};   ssh fvcom${n} "ls -CF /nemoShare/MEOPAR"; done
    * cleaned up stale tmp run dirs in [*]runs/; just fvcom-forecast-x2
  * on skookum:
    * no stale workers
    * restarted log_aggregator
    * decided to skip fvcom-forecast-x2 run
    * recovery started at ~15:30:
        launch_remote_worker arbutus make_fvcom_boundary "arbutus r12 nowcast 2022-03-14"
(SalishSeaCast)


Tue 15-Mar-2022
^^^^^^^^^^^^^^^

cron run failed due to "Wind data date 2022-03-14 is unchanged since last run"; re-ran manually repeatedly with no luck
(Bloomcast)

See work journal.
(Resilient-C)


Wed 16-Mar-2022
^^^^^^^^^^^^^^^

nowcast0 shut down with no explanation at 16-Mar 10:45 UTC == 03:45 Pacific; 
got uptimerobot notification at 03:53
* 15mar/forecast2 interrupted
* recovery started at ~09:20
  * restarted nowcast0 from web dashboard at 16:22 UTC == 09:22 Pacific
  * nowcast0
      sudo apt update
      sudo apt upgrade  # 4 pkgs; security
      cat /var/run/reboot-required*  # check for reboot required
      sudo shutdown -r now  # reboot for security updates
      sudo mount /dev/vdc /nemoShare
      ll /nemoShare/MEOPAR/  # to confirm mount
      sudo mount --bind /nemoShare/MEOPAR /export/MEOPAR
      ll /export/MEOPAR  # to confirm mount
      sudo systemctl start nfs-kernel-server.service
      sudo exportfs -f  # to reset NFS handles for compute nodes
      # confirm compute nodes have /nemoShare/MEOPAR/ mounted:
      for n in {1..9}; do   echo nowcast${n};   ssh nowcast${n} "mountpoint /nemoShare/MEOPAR"; done
      for n in {1..9}; do   echo nowcast${n};   ssh nowcast${n} "ls -CF /nemoShare/MEOPAR"; done
      for n in {0..6}; do   echo fvcom${n};   ssh fvcom${n} "mountpoint /nemoShare/MEOPAR"; done
      for n in {0..6}; do   echo fvcom${n};   ssh fvcom${n} "ls -CF /nemoShare/MEOPAR"; done
    * cleaned up stale tmp run dirs in [*]runs/; just forecast2
  * on skookum:
    * no stale workers
    * restarted log_aggregator
    * decided to skip forecast2 & wwatch3-forecast2 runs
    * collect_weather 12 2.5km still waiting for files
nowcast6 node stopped 16-Mar 18:13 UTC == 11:13 Pacific
* 16mar/nowcast-x2 interrupted
* recovery started at ~12:00
  * restarted nowcast6 from dashboard at 19:03 UTC == 12:03 Pacific
      sudo mount -t nfs -o proto=tcp,port=2049 192.168.238.14:/MEOPAR /nemoShare/MEOPAR
  * skookum:
      launch_remote_worker arbutus make_fvcom_boundary "arbutus x2 nowcast 2022-03-16"
(SalishSeaCast)

Added new unrecognized weather descriptions to cloud fraction mapping.
cron run failed due to "Wind data date 2022-03-15 is unchanged since last run"; investigating:
* reproduced issue on khawla
* trigger is ValueError from get_forcing_data(); presumably not from wind data processing
* HTML table we scrape to get the Fraser River discharge values appears to have changed 
  from 2 to 4 columns on 14-Mar
(Bloomcast)


Thu 17-Mar-2022
^^^^^^^^^^^^^^^

Installed Gparted on khawla.

Spun up the GEM2.5-2007-2009 and GEMLAM-2012-2014 external drives; 
note that they use different power supplied 3V for the 2007-2009, 1.5V for the 2012-2014;
also they are far from full.
Used Gparted to repurpose one of Elise's external drives (elise1) to hold GEMLAM 2010-2011:
* reformatted as ext4 to wipe contents
* set label to GEMLAM-2010-2011
* mount
* sudo mkdir gemlam
* sudo chmod 777 gemlam/
Started rsync-ing /opp/GEMLAM/2010/ from salish to GEMLAM-2010-2011 drive

Discovered that GEMLAM-2012-2014 starts on 2012-04-28;
it ends on 2014-11-18 (but I more or less knew that); months between look complete
it also has all the files stored in a (redundantly named) GEMLAM-2012-2014/ directory.
Checkeed GEM2.5-2007-2009:
* has year directory structure:
    gemlam/2007
    gemlam/2008
    gemlam/2009
* missing 2007-02-01; also missing on /opp
* missing hours on 2007-12-11 and 28
* 2008 is complete
* missing hours on 2009-10-11
(SalishSeaCast)

Phys Ocgy seminar; Tara Howatt re: gliders and zooplankton

See work journal.
(Resilient-C)

Sushi dinner at ESB w/ Raisha, Keiran & Sara.


Fri 18-Mar-2022
^^^^^^^^^^^^^^^

rsync-ing /opp/GEMLAM/2010/ from salish to GEMLAM-2010-2011 drive finished overnight
Started rsync-ing /opp/GEMLAM/2011/ from salish to GEMLAM-2010-2011 drive
Worked on making OPPTools usable in SalishSeaCast production without patches:
* installed djl_ed25519.pub key on GitLab
* confirmed that OPPTools clone on khawla is from my fork
* set upstream remote in khawla clone to point to Michael's repo
* pulled updates from upstream and pushed to fork
* confirmed that commit aa98ada45 comments out import of transit_window_analysis 
  that brings in problematic ttide package
* created SalishSeaCast-prod branch on khawla and added 3 commits:
  * fixed pyproj.Proj init re: axis order chgs in PROJ6+;
      See https://pyproj4.github.io/pyproj/stable/gotchas.html#init-auth-auth-code-should-be-replaced-with-auth-auth-code
  * fixed string formatting of netCDF date/times re: change in cftime pkg API.
    I think the relevant change is in the cftime=1.1.0 released on 13-Feb-2020:
      > * make only_use_cftime_datetimes=True by default, so cftime datetime
      >   instances are returned by default by num2date (instead of returning python
      >   datetime instances where possible). Issue #136, PR #135.
  * trailing whitespace cleanups
* pushed SalishSeaCast-prod branch to my fork on GitLab
* on skookum:
  * changed clone to have Michael's repo as upstream and my fork as origin
  * reverted uncommited changes that are now in my fork
  * pulled from new origin/master
  * pulled from origin/SalishSeaCast-prod
  * git switch SalishSeaCast-prod
  * updated SalishSeaNowcast deployment docs; PR#98
Started work on NEMO weights file for pre-22Sep2011 GEMLAM forcing:
* ref: https://salishsea-meopar-docs.readthedocs.io/en/latest/code-notes/salishsea-nemo/nemo-forcing/atmospheric.html#creating-new-weights-files
* cloned https://github.com/SalishSeaCast/NEMO-EastCoast/ into /ocean/dlatorne/MEOPAR/
* edit NEMO_Preparation/4_weights_ATMOS/make.sh to enable salish commands
* ./make.sh
(SalishSeaCast)

FAL estate work:
* MFC liquidation cheque arrived
* updated distribution spreadsheet

See work journal.
(Resilient-C)


Sat 19-Mar-2022
^^^^^^^^^^^^^^^

rsync-ing /opp/GEMLAM/2011/ from salish to GEMLAM-2010-2011 finished overnight
Started rsync-ing /opp/GEMLAM/2012/20120[1-4]* from salish to GEMLAM-2012-2014 drive
manager crashed early because the log rotation happened while update_forecast_datasets for wwatch3-forecast2 was in progress.
(SalishSeaCast)


Sun 20-Mar-2022
^^^^^^^^^^^^^^^

Refreshed my memory of where I was at on adding HRDPS model profile before SalishSeaCast disk crash.Discussed storage of HRDPS grid x & y w/ Susan; they are metres from SW corner of grid, stored as floats; decided that extraction can cast them to ints and should identify them well in metadata.
(Reshapr)

Rode ToW stage 3 Fire and Ice route; 1st ascent of Alpe de Zwift: 1h40m24s


Week 12
-------

Mon 21-Mar-2022
^^^^^^^^^^^^^^^

Discussed w/ Rachael on Slack files from near-BP_spill-hr Monte Carlo runs that have been 
purged from /scratch.
(MIDOSS)

Continued work on NEMO weights file for pre-22Sep2011 GEMLAM forcing:
* ref: https://salishsea-meopar-docs.readthedocs.io/en/latest/code-notes/salishsea-nemo/nemo-forcing/atmospheric.html#creating-new-weights-files
* cloned https://github.com/SalishSeaCast/NEMO-EastCoast/ into /ocean/dlatorne/MEOPAR/
* editted NEMO_Preparation/4_weights_ATMOS/make.sh to enable salish commands
* ./make.sh
* pushd /data/dlatorne/MEOPAR/grid/
* updated default branch name from master to main
    git branch -m master main
    git fetch origin
    git branch -u origin/main main
    git remote set-head origin -a
    git pull
* created symlinks in grid/ required to run get_weight_nemo:
    ln -s namelist.get_weight_nemo.gem2.5-ops namelist
    ln -s bathymetry_201702.nc bathy_meter.nc
    ln -s /results/forcing/atmospheric/GEM2.5/gemlam/gemlam_y2007m01d03.nc atmos.nc
* generated weights file:
    /ocean/dlatorne/MEOPAR/NEMO-EastCoast/NEMO_Preparation/4_weights_ATMOS/get_weight_nemo 
* improved weights file with tools/I_ForcingFiles/Atmos/ImproveWeightsFile.ipynb
* committed new weights file as grid/weights-gem2.5-gemlam_201702_pre22sep11.nc
* renamed grid/weights-gem2.5-gemlam_201702.nc to grid/weights-gem2.5-gemlam_201702_22sep11onward.nc
(SalishSeaCast)

Group mtg; see whiteboard.
(MOAD)

Continued work on adding HRDPS model profiles for extractions; created PR#27.
(Reshapr)


Tue 22-Mar-2022
^^^^^^^^^^^^^^^

Worked at UBC while Rita is at home.

See work journal.
(Resilient-C)

HRDPS 12Z forecast was very slow; collection finished at 11:55.
(SalishSeaCast)

Started setting up try3 runs:
Prepared and queued 5 x 200 spill runs: [1-5]-200.
  for grp in {1..5}; do head -1 SalishSea_oil_spills_try3.csv > SalishSea_oil_spills_near_BP_try3-${grp}-200.csv; done
  starts=( $(seq 2 2 10) ); grps=( $(seq 1 5) ); for i in "${!grps[@]}"; do head -${starts[$i]}01 SalishSea_oil_spills_try3.csv | tail -200 >>SalishSea_oil_spills_near_BP_try3-${grps[$i]}-200.csv; done
  for grp in {1..5}; do sed -i "s/job id: .*-200_near-BP_try3/job id: ${grp}-200_near-BP_try3/" near-BP.yaml && mohid monte-carlo --debug near-BP.yaml SalishSea_oil_spills_near_BP_try3-${grp}-200.csv; done
(MIDOSS)

Continued work on adding HRDPS model profiles for extractions:
* added HRDPS-2.5km-operational.yaml
* found and fixed more places where model profile coordinate attributes are used
  that I missed in 473bbda6
* fixed a bug in calc of dataset chunk size dict for loading that was corrupting the 
  chunk size dict in the model profile
(Reshapr)


Wed 23-Mar-2022
^^^^^^^^^^^^^^^

try3 runs [2-3]-200 finished, but incomplete; Susan is investigating.
(MIDOSS)

See work journal.
(Resilient-C)

Finished adding HRDPS model profiles for extractions; merged PR#27:
* added lon/lat var names for geo ref dataset to model profiles to handle HRDPS GEMLAM
  datasets where we use a dataset file instead of an ERDDAP geo ref dataset
* added HRDPS-2.5km-GEMLAM-pre22sep11.yaml
* added HRDPS-2.5km-GEMLAM-22sep11onward.yaml
(Reshapr)


Thu 24-Mar-2022
^^^^^^^^^^^^^^^

cron run failed w/ no new wind message after major river data download;
suspect another scraping issue
* reproduced on khawla
* server side problem; 
  https://wateroffice.ec.gc.ca:443/report/real_time_e.html?type=realTime&mode=Table&prm1=47&prm2=-1&stn=08MF005&startDate=2021-01-01&endDate=2022-03-24
  says "No data available"
(Bloomcast)

nowcast-x2 finished too quickly:
* no restart file
* 23mar22/nowcast-x2 never started; tried re-run:
    launch_remote_worker arbutus make_fvcom_boundary "arbutus x2 nowcast 2022-03-23"
(SalishSeaCast)

See work journal.
(Resilient-C)

Cycled to UBC w/ Susan because it was a nice afternoon and she had a thesis to pick up;
LSD ride, except for climb up Salish trail because Spanish Bank hill is closed for what
looks like storm sewer replacement.

Susan figured out that failed try3 runs wer due to spill volumes of zero in .csv file;
she and Rachael fixed that.
(MIDOSS)


Fri 25-Mar-2022
^^^^^^^^^^^^^^^

See work journal.
(Resilient-C)

Explored how best to get snippets for reStructuredText in PyCharm and VSCode;
looks like VSCode wins with TextMate style like Sublime Text had, and easy integration
in the setting system.

Retarted try3 runs:
* [1-5]-200 queued
(MIDOSS)

fvcom backfilling:
  # wait for nowcast-x2 to fail ~10:30
  launch_remote_worker arbutus make_fvcom_boundary "arbutus x2 nowcast 2022-03-24"
  # wait for 24mar22/nowcast-x2 to finish ~12:30
  # kill 24mar22/forecast-x2
  launch_remote_worker arbutus make_fvcom_boundary "arbutus r12 nowcast 2022-03-24"
  # wait for 24mar22/nowcast-r12 to finish ~21:15
  launch_remote_worker arbutus make_fvcom_boundary "arbutus x2 nowcast 2022-03-25"
DM to Michael on Slack asking if we still need to run daily forecast-x2;
he says we can stop running forecast2.
(SalishSeaCast)

Set up VSCode for reStructuredText editing of docs.
* Used https://github.com/ammaraskar/sphinx-problem-matcher to add a VSCode problem-matcher
  to sphinx build task.
* Started writting a collection of reStructuredText snippets in
  ~/.config/Code/User/snippets/restructuredtext.json;
  needs to move to my dofiles repo
Started writing model profiles section of docs.
(Reshapr)


Sat 26-Mar-2022
^^^^^^^^^^^^^^^

Drove to White Rock for Susan to visit J&M; walked in Ruth Johnson Park.

try3 runs:
* [1-5]-200 finished
* backfilled hdf5-to-netcdf4 for [1-2]-200
(MIDOSS)


Sun 27-Mar-2022
^^^^^^^^^^^^^^^

try3 runs:
* [6-10]-200 queued
* on hold until 29-Mar due to graham maintenance
(MIDOSS)

nowcast-agrif failed; maybe related to yesterday's upload_forcing failure?
(SalishSeaCast)


Week 13
-------

Mon 28-Mar-2022
^^^^^^^^^^^^^^^

See work journal.
(Resilient-C)

Group mtg; see whiteboard.
(MOAD)

Haircut.


Tue 29-Mar-2022
^^^^^^^^^^^^^^^

try3 runs:
* [6-10]-200 finsihed
(MIDOSS)

EOAS mail stored messages appeared in Outlook; spent some time sorting mail since migration
started on 8-Mar.

Backfilling nowcast-agrif:
  wait for 29mar22 run to fail
  upload_forcing orcinus nowcast+ --run-date 2022-03-26
  upload_forcing orcinus turbidity --run-date 2022-03-26
  wait for 26mar22 run to complete
  upload_forcing orcinus nowcast+ --run-date 2022-03-27
  upload_forcing orcinus turbidity --run-date 2022-03-27
  wait for 27mar22 run to complete
  upload_forcing orcinus nowcast+ --run-date 2022-03-28
  upload_forcing orcinus turbidity --run-date 2022-03-28
  wait for 28mar22 run to complete
  upload_forcing orcinus nowcast+ --run-date 2022-03-29
  upload_forcing orcinus turbidity --run-date 2022-03-29
graham is back after maintenance.
Started building 1-mo tarballs of nowcast-green.2019105 re-run in tmux session on chum 
and uploading to graham-dtn:/nearline; jan13, feb13
(SalishSeaCast)

See work journal.
(Resilient-C)

Farewell lunch for Rachael.


Wed 30-Mar-2022
^^^^^^^^^^^^^^^

Continued building 1-mo tarballs of nowcast-green.2019105 re-run in tmux session on chum 
and uploading to graham-dtn:/nearline; mar13
(SalishSeaCast)

try3 runs:
* [11-15]-200 finished
(MIDOSS)

Squash-merged dependabot PRs re: jupyter-server:
* SalishSeaTools
* SOG-Bloomcast-Ensemble
* analysis-doug/dask-expts
(MOAD)

See work journal.
(Resilient-C)

Coffee on Slack w/ Becca.


Thu 31-Mar-2022
^^^^^^^^^^^^^^^

Continued building 1-mo tarballs of nowcast-green.2019105 re-run in tmux session on chum 
and uploading to graham-dtn:/nearline; apr13, may13
UBC-DFO modeling mtg; Ben presented on wave paramaterization
(SalishSeaCast)

try3 runs:
* [16-20]-200 queued
* realized that I messed up .csv rows selection for 11-15
* 18-20 stopped due to node failure
* 17-18 failed due to /scratch issue
* 19-20 succeeded
(MIDOSS)

See work journal.
(Resilient-C)

Weekly project mtg.
(Atlantis)

April
=====

Fri 1-Apr-2022
^^^^^^^^^^^^^^

try3 runs:
* [11-15,16-18,21-25]-200 running
(MIDOSS)

Updated sentry-sdk (and certifi & openssl as deps) in prod env on skookum.
Updated paramiko in prod env on skookum re: dependabot PR; quash-merged PR.
Started removing forecast-x2 from automation.
Continued building 1-mo tarballs of nowcast-green.2019105 re-run in tmux session on chum 
and uploading to graham-dtn:/nearline; jun13, jul13, aug13
(SalishSeaCast)


Sat 2-Apr-2022
^^^^^^^^^^^^^^

try3 runs:
* [11-15,16-18,21-25]-200 probably all failed due to /scratch instability; tonnes of core dumps
(MIDOSS)

Continued building 1-mo tarballs of nowcast-green.2019105 re-run in tmux session on chum 
and uploading to graham-dtn:/nearline; sep13, oct13, nov13
nowcast0 shut down with no explanation at 2-Apr 20:12 UTC == 13:12 Pacific; 
got uptimerobot notification at 13:20
* 2apr/forecast-x2 interrupted
* 2apr/wwatch3-forecast interrupted
* recovery started at ~15:00
  * restarted nowcast0 from web dashboard at 21:59 UTC == 14:59 Pacific
  * nowcast0
      sudo apt update
      sudo apt upgrade  # 5 pkgs
      cat /var/run/reboot-required*  # check for reboot required
      sudo mount /dev/vdc /nemoShare
      ll /nemoShare/MEOPAR/  # to confirm mount
      sudo mount --bind /nemoShare/MEOPAR /export/MEOPAR
      ll /export/MEOPAR  # to confirm mount
      sudo systemctl start nfs-kernel-server.service
      sudo exportfs -f  # to reset NFS handles for compute nodes
      # confirm compute nodes have /nemoShare/MEOPAR/ mounted:
      for n in {1..9}; do   echo nowcast${n};   ssh nowcast${n} "mountpoint /nemoShare/MEOPAR"; done
      for n in {1..9}; do   echo nowcast${n};   ssh nowcast${n} "ls -CF /nemoShare/MEOPAR"; done
      for n in {0..6}; do   echo fvcom${n};   ssh fvcom${n} "mountpoint /nemoShare/MEOPAR"; done
      for n in {0..6}; do   echo fvcom${n};   ssh fvcom${n} "ls -CF /nemoShare/MEOPAR"; done
    * cleaned up stale tmp run dirs in [*]runs/; forecast-x2 & wwatch3-forecast
  * on skookum:
    * killed stale workers
    * restarted log_aggregator
    * decided to skip forecast2 & wwatch3-forecast2 runs
      launch_remote_worker arbutus make_fvcom_boundary "arbutus r12 nowcast 2022-04-02"
(SalishSeaCast)

First race on Zwift: HERD Summer Series, Figure 8 points race


Sun 3-Apr-2022
^^^^^^^^^^^^^^

try3 runs:
* confirmed that [11-18,21-25]-200 all failed
* cleaned up
* [11-13]-200 running
* [14-18]-200 queued
(MIDOSS)

Continued building 1-mo tarballs of nowcast-green.2019105 re-run in tmux session on chum 
and uploading to graham-dtn:/nearline; dec13, jan14
(SalishSeaCast)


Week 14
-------

Mon 4-Apr-2022
^^^^^^^^^^^^^^

nowcast0 shut down with no explanation at 4-Apr 10:41 UTC == 03:41 Pacific; 
got uptimerobot notification at 03:50
* 4apr/forecast2 interrupted
* 4apr/wwatch3-forecast missed
* recovery started at ~09:35:00
  * restarted nowcast0 from web dashboard at 16:36 UTC == 09:36 Pacific
  * nowcast0
      sudo apt update
      sudo apt upgrade  # 1 pkg
      cat /var/run/reboot-required*  # check for reboot required
      sudo mount /dev/vdc /nemoShare
      ll /nemoShare/MEOPAR/  # to confirm mount
      sudo mount --bind /nemoShare/MEOPAR /export/MEOPAR
      ll /export/MEOPAR  # to confirm mount
      sudo systemctl start nfs-kernel-server.service
      sudo exportfs -f  # to reset NFS handles for compute nodes
      # confirm compute nodes have /nemoShare/MEOPAR/ mounted:
      for n in {1..9}; do   echo nowcast${n};   ssh nowcast${n} "mountpoint /nemoShare/MEOPAR"; done
      for n in {1..9}; do   echo nowcast${n};   ssh nowcast${n} "ls -CF /nemoShare/MEOPAR"; done
      for n in {0..6}; do   echo fvcom${n};   ssh fvcom${n} "mountpoint /nemoShare/MEOPAR"; done
      for n in {0..6}; do   echo fvcom${n};   ssh fvcom${n} "ls -CF /nemoShare/MEOPAR"; done
    * cleaned up stale tmp run dirs in [*]runs/; forecast2
  * on skookum:
    * no stale workers
    * restarted log_aggregator
    * decided to skip forecast2 & wwatch3-forecast2 runs
Continued building 1-mo tarballs of nowcast-green.2019105 re-run in tmux session on chum 
and uploading to graham-dtn:/nearline; feb14, mar22, mar14, apr14
(SalishSeaCast)

try3 runs:
* [11-18]-200 finished successfully
* [21-25]-200 running
(MIDOSS)

Group mtg; see whiteboard.
(MOAD)


Tue 5-Apr-2022
^^^^^^^^^^^^^^

Email conversation w/ Luke Whittington of cloud support:
* nowcast0 and nowcast6 are on the same hypervisor
* nowcast0 stops were due to hypervisor os out of memory
* plan is to reboot the host at ~14:00
* rebooted, but no route to host, and Luke went silent
Continued building 1-mo tarballs of nowcast-green.2019105 re-run in tmux session on chum 
and uploading to graham-dtn:/nearline; may14, jun14, jul14
(SalishSeaCast)

try3 runs:
* [21-24]-200 finished successfully
* [25-30]-200 running
* [31-35]-200 queued
(MIDOSS)

Unpinned jinja2 in envs re: new release of nbconvert=6.4.5 that fixes the import issue that 
broke the website build.
(Numeric Course)

Auto-update pre-commit re: 2.18.1 release:
* UBC-MOAD/cookiecutter-MOAD-pypkg
* UBC-MOAD/MoaceanParcels
* UBC-MOAD/docs
* SS-Atlantis/AtlantisCmd
* MIDOSS/MOHID-Cmd

* SalishSeaCast/SalishSeaNowcast
* UBC-MOAD/Reshapr
(MOAD)

See work journal.
(Resilient-C)


Wed 6-Apr-2022
^^^^^^^^^^^^^^

Poked Luke re: connection to nowcast0 still down:
* he got the interfaces up somehow
* I dissociated the IP address and it was returned to the pool
* allocated a new IP and associated it, but still no route to host
Continued building 1-mo tarballs of nowcast-green.2019105 re-run in tmux session on chum 
and uploading to graham-dtn:/nearline; aug14, sep14, oct14
(SalishSeaCast)

SHARCNET webinar: Apptainer
* Paul Preney, U Windsor
* Apptainer was formerly known as Singularity; name change went with xfer from corp to 
  Linux Foundation
* originally developed by LBNL
* portability, reproducibility, long term perservation of software envs & configs
* specifically designed for HPC, in contrast to docker
* virtualizes OS; isolated from module system (CVMFS); module load apptainer
* comes from a module being installed on Linux VM
* all stuff must be compiled inside container, especially MPI
  * load MPI>=3 outside container, regardless of version of MPI used in container
* use srun apptainer, never mpirun or mpiexec, in slurm scripts
* most common starting point is to grab an image from Docker Hub; other ways are possible
  * see apptainer "build a container" docs
* apptainer image format (.sif) is different to docker image format
  * apptainer flattens all layers in contrast to docker format
* building large images is very disk intensive, use local drive if possible;
  don't use network file systems at risk of inexplicable failures
  * best to build images on a local system, not cluster
* build image using sudo because pkg mgr inside container needs root access
* for apptainer run, shell, instance, or exec, always use -C, -c, or -e
    * -C hides external file system, PID, IPC & env
    * -c hides less
    * -e hides even less
  * always -W w/ real empty dir that you have write access to; use $SLURM_TMPDIR
    in sbatch scripts; -W sets tmp dir envvars
  * bind mount home, project & scratch w/ -B /home -B /project -B /scratch
* RAPIDS example:
  * some nvidia cuda thing
  * use a new home on -W file system inside container 
* can install conda in container and build envs on -W dir
* test in interactive session, then build sbatch script
* can install spack in container via an overlay to install os-ish pkgs; e.g. nano
* super important to new home on -W or overlay

Learned in SHARCNET webinar chat that quotas are not enforced on SLURM_TMPDIR

try3 runs:
* [26-28,30]-200 finished successfully
* 29-200 had 1 failed spill w/ no .nc, .sro, .hdf5
* [31-35]-200 running
(MIDOSS)

See work journal.
(Resilient-C)


Thu 7-Apr-2022
^^^^^^^^^^^^^^

try3 runs:
* [32-35]-200 finished successfully
* 29-200 had 1 failed spill w/ no .nc, .sro, .hdf5
* 31-200 has 4 spills w/ no .nc, but .hdf5 and .sro; need to backfill
* pausing runs so that Ben gets some priority
(MIDOSS)

See work journal.
(Resilient-C)

Continued building 1-mo tarballs of nowcast-green.2019105 re-run in tmux session on chum 
and uploading to graham-dtn:/nearline; nov14, dec14, jan15
arbutus.cloud saga continued:
* Susan poked Luke
* Luke says that network card on the hypervisor is failed; need to migrate VMs
  to a different hypervisor
* Luke started migrations at ~13:55
* nowcast0 migration had trouble, but finished ~17:00
* nowcast6 migration happened later
nowcast system recovery:
  * nowcast0
      sudo apt update
      sudo apt upgrade  # 3 pkgs
      cat /var/run/reboot-required*  # check for reboot required
      sudo mount /dev/vdc /nemoShare
      ll /nemoShare/MEOPAR/  # to confirm mount
      sudo mount --bind /nemoShare/MEOPAR /export/MEOPAR
      ll /export/MEOPAR  # to confirm mount
      sudo systemctl start nfs-kernel-server.service
      sudo exportfs -f  # to reset NFS handles for compute nodes
      # confirm compute nodes have /nemoShare/MEOPAR/ mounted:
      for n in {1..9}; do   echo nowcast${n};   ssh nowcast${n} "mountpoint /nemoShare/MEOPAR"; done
      for n in {1..9}; do   echo nowcast${n};   ssh nowcast${n} "ls -CF /nemoShare/MEOPAR"; done
      for n in {0..6}; do   echo fvcom${n};   ssh fvcom${n} "mountpoint /nemoShare/MEOPAR"; done
      for n in {0..6}; do   echo fvcom${n};   ssh fvcom${n} "ls -CF /nemoShare/MEOPAR"; done
Realized that the EOAS firewall rules need to be changed to allow comms between skookum and new
nowcast0 IP address; created helpdesk ticket
(SalishSeaCast)

Phys Ocgy seminar; Ryan Osman of Water First in Ontario; photography, engineering & water resources
management.

Squash-merged dependabot PRs re: notebook leaking auth cookies & headers to server logs:
* 43ravens/ECget
* SalishSeaCast/SOG-Bloomcast-Ensemble
* SalishSeaCast/tools
* SalishSeaCast/analysis-doug/melanie-geotiff
* SalishSeaCast/analysis-doug/dask-expts
(MOAD)


Fri 8-Apr-2022
^^^^^^^^^^^^^^

Continued building 1-mo tarballs of nowcast-green.2019105 re-run in tmux session on chum 
and uploading to graham-dtn:/nearline; feb15, mar15, apr15, may15
Henryk adjusted EOAS firewall rules.
Continued nowcast system recovery:
* nowcast6:
    sudo mount -t nfs -o proto=tcp,port=2049 192.168.238.14:/MEOPAR /nemoShare/MEOPAR
* nowcast0
    # confirm compute nodes have /nemoShare/MEOPAR/ mounted:
    for n in {1..9}; do   echo nowcast${n};   ssh nowcast${n} "mountpoint /nemoShare/MEOPAR"; done
    for n in {1..9}; do   echo nowcast${n};   ssh nowcast${n} "ls -CF /nemoShare/MEOPAR"; done
* wait for nowcast-blue run launch to fail at ~09:45
* on skookum:
    stop log_aggregator
    stop manager
    stop message_broker
    start message_broker
    start manager
    start log_aggregator
    nemo_nowcast.workers.clear_checklist  # to also rotate logs
    upload_forcing arbutus nowcast+ 2022-04-06 --debug
    upload_forcing arbutus nowcast+ 2022-04-07 --debug
    make_turbidity_file 2022-04-06 --debug
    make_turbidity_file 2022-04-07 --debug
    make_turbidity_file 2022-04-08 --debug
  zmq messages not flowing; added to helpdesk ticket; Henryk fixed rules; he had updated salish
  but not skookum
  backfill nowcast-green
    upload_forcing arbutus turbidity 2022-04-06
    wait for run to finish
    download_results arbutus nowcast-green 2022-04-06
    upload_forcing arbutus turbidity 2022-04-07
    wait for run to finish
    download_results arbutus nowcast-green 2022-04-07
    upload_forcing arbutus turbidity 2022-04-08
    wait for run to finish
    download_results arbutus nowcast-green 2022-04-08
  backfill nowcast-agrif
    upload_forcing orcinus turbidity 2022-04-06
    wait for run to finish
    upload_forcing orcinus turbidity 2022-04-07
    wait for run to finish
    upload_forcing orcinus turbidity 2022-04-08
  backfill VHFR
    launch_remote_worker arbutus make_fvcom_boundary "arbutus r12 nowcast 2022-04-05"
    make_fvcom_rivers_forcing arbutus r12 nowcast 2022-04-05  # on arbutus
    make_fvcom_atmos_forcing r12 nowcast 2022-04-05  # on skookum
    wait for run to finish
    download_fvcom_results arbutus r12 nowcast 2022-04-05
  backfill nowcast-blue and forecast for wwatch3
    make_forcing_links arbutus nowcast+ 2022-04-06
    kill nowcast-green run when it starts
  backfill wwatch3
    launch_remote_worker arbutus make_ww3_wind_file "arbutus forecast 2022-04-06"
    launch_remote_worker arbutus make_ww3_current_file "arbutus forecast 2022-04-06"
  backfill nowcast-dev
    make_forcing_links salish nowcast+ --shared-storage 2022-04-06
(SalishSeaCast)


Sat 9-Apr-2022
^^^^^^^^^^^^^^

Continued nowcast system recovery:
* clear_checklist to rotate logs
* backfill nowcast-blue and forecast for wwatch3
    make_forcing_links arbutus nowcast+ 2022-04-07
    kill nowcast-green run when it starts
    make_forcing_links arbutus nowcast+ 2022-04-08
    kill nowcast-green run when it starts
    make_forcing_links arbutus nowcast+ 2022-04-09
* backfill wwatch3
    launch_remote_worker arbutus make_ww3_wind_file "arbutus forecast 2022-04-07"
    launch_remote_worker arbutus make_ww3_current_file "arbutus forecast 2022-04-07"
    launch_remote_worker arbutus make_ww3_wind_file "arbutus forecast 2022-04-08"
    launch_remote_worker arbutus make_ww3_current_file "arbutus forecast 2022-04-08"
* manager was restarted due to name resolution failure around 17:00; processing ended with
  forecast run completed but not downloaded, and nowcast-green run not started;
  resolved by manually doing download and make_forcing_links at ~20:00
Continued building 1-mo tarballs of nowcast-green.2019105 re-run in tmux session on chum 
and uploading to graham-dtn:/nearline; jun15, jul15, aug15
(SalishSeaCast)


Sun 10-Apr-2022
^^^^^^^^^^^^^^^

Name resolution problem continues; appears to be limited to UDC machines, no ESB workstations.
* no weather downloads yet today
* killed collect_weather 00
* pinged EOAS-IT slack and Henryk changed resolver and added failbacks
* recovery started at ~09:25:
    download_weather 00 2.5km
    download_weather 06 2.5km
    forecast2 runs didn't start ???
    launch_remote_worker arbutus make_ww3_wind_file "arbutus forecast 2022-04-09"
    launch_remote_worker arbutus make_ww3_current_file "arbutus forecast 2022-04-09"
    wait for wwatch3 backfill runs to finish
    collect_weather 18 2.5km
    download_weather 12 2.5km
      missing files on datamart; emailed Sandrine; file downloads finished at ~13:50
    collect_weather didn't finish but Susan determined that all the files that grib_to_netcdf needs are there, so started collect_weather 00
* backfill VHFR
    launch_remote_worker arbutus make_fvcom_boundary "arbutus r12 nowcast 2022-04-06"
* backfill nowcast-dev
    make_forcing_links salish nowcast+ --shared-storage 2022-04-07
Continued building 1-mo tarballs of nowcast-green.2019105 re-run in tmux session on chum 
and uploading to graham-dtn:/nearline; sep15, oct15, nov15, dec15
(SalishSeaCast)


Week 15
-------

Mon 11-Apr-2022
^^^^^^^^^^^^^^^

Continued building 1-mo tarballs of nowcast-green.2019105 re-run in tmux session on chum 
and uploading to graham-dtn:/nearline; jan16, feb16, mar16, apr16, may16
Continued nowcast system recovery:
* collect_weather 00 didn't finish; killed it and successfully ran download_weather 00
* catch-up:
    download_weather 06 2.5km
    collect_weather 18 2.5km
    wait for forecast2 runs to finish
    download_weather 12 2.5km
* backfill VHFR
    wait for nowcast-x2, then forecast-x2 to fail
    launch_remote_worker arbutus make_fvcom_boundary "arbutus x2 nowcast 2022-04-06"
    kill 06apr22/forecast-x2
    wait for nowcast-x2, then forecast-x2 from nowcast etc. re-run to fail
    launch_remote_worker arbutus make_fvcom_boundary "arbutus x2 nowcast 2022-04-07"
    kill 07apr22/forecast-x2
    launch_remote_worker arbutus make_fvcom_boundary "arbutus r12 nowcast 2022-04-07"
* backfill nowcast-dev
    wait for nowcast-dev run to fail
    make_forcing_links salish nowcast+ --shared-storage 2022-04-08
    make_forcing_links salish nowcast+ --shared-storage 2022-04-09
    make_forcing_links salish nowcast+ --shared-storage 2022-04-10
* ran download_weather 18 as a just-in-case, and it succeedded!!
Email from Parker saying that LiveOcean ran w/ incorrect atmos forcing today; has been corrected;
recovery:
  wait for 06apr22/nowcast-x2 to fail
  download_live_ocean
Started restoring nowcast-env on /SalishSeaCast file system:
* Charles recovered /SalishSeaCast to something from 2019/2020 full of mercurial repos
* checked repo clones for uncommitted changes, then deleted hg repos, and cloned git repos:
  * grid
  * moad_tools
  * NEMO-Cmd
  * NEMO_Nowcast
  * private-tools
  * rivers-climatology
  * SalishSeaCmd
  * SalishSeaNowcast
  * salishsea-site
  * SS-run-sets
  * tides
  * tools
  * tracers
  * NEMO-3.6-code
  * XIOS-ARCH
* GitLab repos  
  * FVCOM-VHFR-config
    * confirmed up to date
  * OPPTools
    * clone my fork
    * switch to SalishSeaCast-prod branch
* copy wgrib2 executable
* created nowcast-env env
* installed nowcast-env pkgs
* updated sarracenia-env env YAML
* created sarracenia-env
* set up envvars
* confirmed datamart dirs
* cleared logs dirs

TODO:
* build XIOS-2
* build SalishSeaCast_Blue
(SalishSeaCast)

Changed default branch of private-tools repo from master to main.
Group mtg; see whiteboard.
(MOAD)

Read and commented on draft of Raisha & Sara's data ranking paper.
(Atlantis)


Tue 12-Apr-2022
^^^^^^^^^^^^^^^

Continued building 1-mo tarballs of nowcast-green.2019105 re-run in tmux session on chum 
and uploading to graham-dtn:/nearline; jun16, jul16, aug16, oct16
Continued nowcast system recovery:
* automation was successful overnight :-)
* backfill nowcast-dev
    wait for nowcast-dev run to fail
    make_forcing_links salish nowcast+ --shared-storage 2022-04-11
    make_forcing_links salish nowcast+ --shared-storage 2022-04-12
* backfill VHFR
    wait for nowcast-x2, then forecast-x2 to fail
    launch_remote_worker arbutus make_fvcom_boundary "arbutus x2 nowcast 2022-04-08"
    kill 08apr22/forecast-x2 at ~13:30
    launch_remote_worker arbutus make_fvcom_boundary "arbutus x2 nowcast 2022-04-09"
    kill 09apr22/forecast-x2 at ~16:15
    launch_remote_worker arbutus make_fvcom_boundary "arbutus r12 nowcast 2022-04-08"
Got arbutus VMs to hosts mapping from Luke; stored on khawla desktop;
only 2 overlaps, one between x2 and r12, the other between nemo and r12; 
adjusted NEMO mpi_hosts to remove nowcast8 overlap with fvcom2;
left fvcom1 (x2) and fvcom5 (r12) overlap; also note that fvcom0 is used by both x2 and r12
(SalishSeaCast)

See work journal.
(Resilient-C)


Wed 13-Apr-2022
^^^^^^^^^^^^^^^

Continued building 1-mo tarballs of nowcast-green.2019105 re-run in tmux session on chum 
and uploading to graham-dtn:/nearline; oct16, nov16, dec16, jan17
Changed automation to run from new /SalishSeaCast env instead of temporary /data/SalishSeaCast/:
* stopped watch_NEMO_hindcast while 16dec07hindcast was in progress
* stopped collect_weather 12 2.5km
* supervisorctl shutdown in old env
* supervisord in new env
* rsync SalishSeaNowcast/tidal_predictions/ from old to new env
* start automation in new env:
    supervisorctl stop sr_subscribe-hrdps-west
    rm -rf /results/forcing/atmospheric/GEM2.5/GRIB/20220413/12
    collect_weather 18 2.5km
    download_weather 12 2.5km
Restored salishsea-site-env on /SalishSeaCast file system:
* created salishsea-site-env env
* installed salishsea-site-env pkgs
* set up envvars
* checked and updated paths
* supervisorctl shutdown in old env
* supervisord in new env
* on salish:
  * build XIOS-2
  * build NEMO SalishSeaCast_Blue config
  * build REBUILD_NEMO
Continued nowcast system recovery:
* backfill VHFR
    wait for nowcast-x2, then forecast-x2 to fail
    launch_remote_worker arbutus make_fvcom_boundary "arbutus x2 nowcast 2022-04-10"
    kill 10apr22/forecast-x2 at ~14:00
    launch_remote_worker arbutus make_fvcom_boundary "arbutus x2 nowcast 2022-04-11"
    kill 11apr22/forecast-x2 at ~17:45
    launch_remote_worker arbutus make_fvcom_boundary "arbutus x2 nowcast 2022-04-12"
    kill 12apr22/forecast-x2 at ~21:15
    launch_remote_worker arbutus make_fvcom_boundary "arbutus x2 nowcast 2022-04-13"
(SalishSeaCast)

Squash-merged dependabot PR in salishsea-site re: waitress.
Tracked recent linkcheck GHA failures to https://github.com/sphinx-doc/sphinx/issues/10343
and https://github.com/github/docs/issues/17042;
work-around is to spoof a user agent (see 1st link); that might also resolved the MOAD/docs
failure re: https://www.baeldung.com/cs/ssh-intro, a partial user-agent string of "Mozilla"
for in curl for that URL
(MOAD)

Added salishsea-site/ to khawla; see setup notes.

See work journal.
(Resilient-C)


Thu 14-Apr-2022
^^^^^^^^^^^^^^^

Continued building 1-mo tarballs of nowcast-green.2019105 re-run in tmux session on chum 
and uploading to graham-dtn:/nearline; feb17, mar17, apr17, may17, jun17
Created and squash-merged PR#100 to drop VHFR forecast runs; deployed to production.
Forgot to restart sr_subscribe-hrdps-west yesterday so no 18, 00, 06 or 12 HRDPS forecasts
collected; recovery:
  supervisorctl start sr_subscribe-hrdps-west
  download_weather 18 2.5km
  download_weather 00 2.5km
  download_weather 06 2.5km
  collect_weather 18 2.5km
  download_weather 00 1km --yesterday  # failed; too late
  download_weather 12 1km --yesterday
  wait for forecast2 runs to finish
  download_weather 12 2.5km
Continued nowcast system recovery:
* backfill VHFR
    wait for nowcast-r12 to fail at ~15:15
    launch_remote_worker arbutus make_fvcom_boundary "arbutus r12 nowcast 2022-04-09"
    wait for 09apr22/nowcast-r12 to finish at ~22:00
    launch_remote_worker arbutus make_fvcom_boundary "arbutus r12 nowcast 2022-04-10"
Started to explore how to move SalishSeaNowcast/tidal_predictions/ to somewhere other than 
uncommited file in production clone:
* 1.4G total
* 16 x 65M files for 30dec06 to 31dec30 .csv files
* lots of old files that cover sub-range of above time range
* copied files to /SalishSeaCast/tidal-predictions/ dir and changed nowcast.yaml to test
  * TODO: update lots of paths in SalishSeaNowcast notebooks & tests
/results is full :-(
  * deleted nowcast-dev.201905/jan-mar21
(SalishSeaCast)

Coffee w/ Karyn.

Phys Ocgy seminar; cop student presentations.

See work journal.
(Resilient-C)


Fri 15-Apr-2022
^^^^^^^^^^^^^^^

**Statutory Holiday** - Good Friday

Continued building 1-mo tarballs of nowcast-green.2019105 re-run in tmux session on chum 
and uploading to graham-dtn:/nearline; jul17, aug17
Bug re: log rotation during download_wwatch3_results forecast2 recurred.
Continued nowcast system recovery:
* backfill VHFR
    wait for nowcast-r12 to fail at ~12:45
    launch_remote_worker arbutus make_fvcom_boundary "arbutus r12 nowcast 2022-04-11"
    wait for nowcast-r12 to finish at ~20:00
    launch_remote_worker arbutus make_fvcom_boundary "arbutus r12 nowcast 2022-04-12"
(SalishSeaCast)

See work journal.
(Resilient-C)


Sat 16-Apr-2022
^^^^^^^^^^^^^^^

Continued building 1-mo tarballs of nowcast-green.2019105 re-run in tmux session on chum 
and uploading to graham-dtn:/nearline; sep17, oct17
collect_weather 00 failed, probably due to network issues; recovery:
  kill collect_weather 00 2.5km
  collect_weather 18 2.5km
  download_weather 00 2.5km
  download_weather 06 2.5km
  kill NEMO forecast2
  download_weather 12 2.5km
Continued nowcast system recovery:
* backfill VHFR
    wait for nowcast-r12 to fail 
    launch_remote_worker arbutus make_fvcom_boundary "arbutus r12 nowcast 2022-04-13"
(SalishSeaCast)

Cycled to Maquabeak Park under Port Mann Bridge; access to Colony Farm under Mary Hill is *still* 
closed due to TMX work.


Sun 17-Apr-2022
^^^^^^^^^^^^^^^

Continued building 1-mo tarballs of nowcast-green.2019105 re-run in tmux session on chum 
and uploading to graham-dtn:/nearline; nov17, dec17, jan18, feb18
Continued nowcast system recovery:
* backfill VHFR
    wait for nowcast-r12 to fail at ~12:45
    launch_remote_worker arbutus make_fvcom_boundary "arbutus r12 nowcast 2022-04-14"
    wait for nowcast-r12 to finish at ~21:15
    launch_remote_worker arbutus make_fvcom_boundary "arbutus r12 nowcast 2022-04-15"
(SalishSeaCast)

Created "Viewy Phantom" backup on Nodecraft before update to 1.18.2.
Changed Nodecraft server to run minecracft=1.18.2 and fabric=1.18.2-0.13.3 
via 1-click installer and archiving files to _old_files/;
Restored world files by copying from _old_files/:
  1_18-1/ (world)
  banned-ips.json
  banned-players.json
  ops.json
  server.properties
  whitelist.json
Successfully tested world, then installed 1.18.2 version of lithium and 
1.18.x version of phosphur mods and restarted world.
Cleared client mods/ dir and installed new 1.18.2 versions:
  iris-sodium-fabric via iris-installer=2.0.3
  lithium
  phosphur
  malilib
  minihud
  litematica
Cleared client shaderpacks/ dir and installed new 4.4 version of Complementary;
had to move 4.3.2 back to get shaders to work; maybe temporary?


Week 16
-------

Mon 18-Apr-2022
^^^^^^^^^^^^^^^

**Statutory Holiday** - Easter Monday

Continued building 1-mo tarballs of nowcast-green.2019105 re-run in tmux session on chum 
and uploading to graham-dtn:/nearline; mar18, apr18
Continued nowcast system recovery:
* backfill VHFR
    wait for nowcast-r12 to fail at ~12:45
    launch_remote_worker arbutus make_fvcom_boundary "arbutus r12 nowcast 2022-04-16"
    wait for nowcast-r12 to finish at ~21:00
    launch_remote_worker arbutus make_fvcom_boundary "arbutus r12 nowcast 2022-04-17"
(SalishSeaCast)

Started work on 2021 income tax returns:
* matisse runs 10.13.6


Tue 19-Apr-2022
^^^^^^^^^^^^^^^

Worked at ESB while Rita was at home.

collect_NeahBay_ssh failed for both forecast2 runs and nowcast; Susan tracked the issue down to a
planned outage; mitigation:
* symlinks:
    ln -s /results/forcing/sshNeahBay/fcst/ssh_y2022m04d18.nc /results/forcing/sshNeahBay/obs/ssh_y2022m04d18.nc
    ln -s /results/forcing/sshNeahBay/fcst/ssh_y2022m04d21.nc /results/forcing/sshNeahBay/fcst/ssh_y2022m04d22.nc
* kill collect_NeahBay_ssh 06
* restart automation:
    upload_forcing arbutus nowcast+
    upload_forcing orcinus nowcast+
    upload_forcing optimum nowcast+
    upload_forcing graham nowcast+
Continued building 1-mo tarballs of nowcast-green.2019105 re-run in tmux session on chum 
and uploading to graham-dtn:/nearline; may18, jun18
Continued nowcast system recovery:
* backfill VHFR
    wait for nowcast-r12 to fail at ~13:30
    launch_remote_worker arbutus make_fvcom_boundary "arbutus r12 nowcast 2022-04-18"
    wait for nowcast-r12 to finish at ~20:30
    launch_remote_worker arbutus make_fvcom_boundary "arbutus r12 nowcast 2022-04-19"
Continued work to move SalishSeaNowcast/tidal_predictions/ to somewhere other than 
uncommited file in production clone:
* renamed prod SalishSeaNowcast/tidal_predictions/ to SalishSeaNowcast/tidal_predictions.aside/
  to confirm success of config change
* rsync-ed skookum:/SalishSeaCast/tidal-predictions/ to khawla to create git repo
* created git repo on khawla
* started writing README; passed it to Susan for elaboration
* created private repo on GitHub; set origin remote in repo on khawla


* 1.4G total
* 16 x 65M files for 30dec06 to 31dec30 .csv files
* lots of old files that cover sub-ranges of above time range
* copied files to /SalishSeaCast/tidal-predictions/ dir and changed nowcast.yaml to test
  * TODO: update lots of paths in SalishSeaNowcast notebooks & tests
(SalishSeaCast)

Restarted try3 Monte Carlo runs:
* deleted all project SalishSea_oil_spills_near_BP_try3-*.csv files
* cleaned up scratch 
* built new MOHID at commit a31b4ce712
* [1-5]-200 queued
(MIDOSS)

Renewed PyCharm license.

Code maintenance:
* updated copyright year range
* updated nbviewer.jupyter.org domain in links
(SalishSeaNowcast)


Wed 20-Apr-2022
^^^^^^^^^^^^^^^

NOAA outage extended, so collect_NeahBay_ssh failed again for forecast2 and nowcast runs;
mitigation:
* wait for make_live_ocean_files and grib_to_netcdf to finish; automation is blocked then because
  collect_NeahBay_ssh is in race condition workers set
* kill collect_NeahBay_ssh 06
* symlinks:
    ln -s /results/forcing/sshNeahBay/fcst/ssh_y2022m04d19.nc /results/forcing/sshNeahBay/obs/ssh_y2022m04d19.nc
    ln -s /results/forcing/sshNeahBay/fcst/ssh_y2022m04d22.nc /results/forcing/sshNeahBay/fcst/ssh_y2022m04d23.nc
* restart automation:
    upload_forcing arbutus nowcast+
    upload_forcing orcinus nowcast+
    upload_forcing optimum nowcast+
    upload_forcing graham nowcast+
Continued building 1-mo tarballs of nowcast-green.2019105 re-run in tmux session on chum 
and uploading to graham-dtn:/nearline; jul18, aug18
(SalishSeaCast)

try3 runs:
* [1-5]-200 running
(MIDOSS)

FAL estate work:
* LOD for 2021 estate expenses payment
* TD branch visit to deposit cheques & make expenses transfer
* updated accounts & distribution spreadsheet


Thu 21-Apr-2022
^^^^^^^^^^^^^^^

NeahBay ssh outage ended; automation was smooth overnight
Continued building 1-mo tarballs of nowcast-green.2019105 re-run in tmux session on chum 
and uploading to graham-dtn:/nearline; sep18, oct18, nov18
(SalishSeaCast)

try3 runs:
* [1-5]-200 finished
* [9-10]-200 running
* []-200 queued
(MIDOSS)

See work journal.
(Resilient-C)

Phys Ocgy seminar; Cole Lord-May re: merging differential equation models w/ neural networks
for glacier melt modeling.


Fri 22-Apr-2022
^^^^^^^^^^^^^^^

Continued building 1-mo tarballs of nowcast-green.2019105 re-run in tmux session on chum 
and uploading to graham-dtn:/nearline; dec18, jan19, feb19
(SalishSeaCast)

try3 runs:
* [1-9]-200 finished
* [10-15]-200 running
(MIDOSS)

Code maintenance:
* updated `Salish Sea MEOPAR` to `SalishSeaCast`
* updated email addreses to eoas.ubc.ca
* added SPDX short-form license identifiers
Squash-merged dependabot re: pypdf2
(SalishSeaNowcast)

Mtg w/ Jose:
* checkpoint/restart
* tmux
* python3 -m
* if __name__ == "__main__":
* YAML files for config
* maybe a distinct conda env
* click if a cli is really needed
(MOAD)

Reviewed Raisha's video talk for Atlantis Summit.
(Atlantis)


Sat 23-Apr-2022
^^^^^^^^^^^^^^^

Continued building 1-mo tarballs of nowcast-green.2019105 re-run in tmux session on chum 
and uploading to graham-dtn:/nearline; mar19
(SalishSeaCast)

try3 runs:
* [1-15]-200 finished
* [16-20]-200 queued
(MIDOSS)

Visited J&M in White Rock and did their tax returns.


Sun 24-Apr-2022
^^^^^^^^^^^^^^^

Big monitor started flashing on and off when I reconnected khawla after yesterday's trip
to White Rock; appears to the be associated with Nvidia card or drivers; started after update
to 510.54 driver; system is stable on integrated graphics; reverted to 470.86; integerated graphics started to flicker too; unplugged & replugged HDMI cable from monitor; switched to port that had
matisse on it; stable; switched back to HDMI port 1 on monitor; stable; unplugged matisse from 
monitor.

Continued building 1-mo tarballs of nowcast-green.2019105 re-run in tmux session on chum 
and uploading to graham-dtn:/nearline; apr19
(SalishSeaCast)

try3 runs:
* [1-16]-200 finished
* 16-20 has 2 hdf5-to-netcdf4 failures; backfill job queued
* [17-18]-200 running
* [19-25]-200 queued, then cancelled to give Birgit priority
* cleaned up empty-ish duplicated run dirs to [1a-15]-200
(MIDOSS)

Rode ANZAC Classic long route on Zwift in NZ group; it was billed as a fondo, but recorded as a
race on ZwiftPower; buried 5 Oz riders on the final climb.


Week 17
-------

Mon 25-Apr-2022
^^^^^^^^^^^^^^^

Continued building 1-mo tarballs of nowcast-green.2019105 re-run in tmux session on chum 
and uploading to graham-dtn:/nearline; may19, jun19, jul19
Backfill nowcast-agrif since ssh banner issue on 23-Apr:
  upload_forcing orcinus nowcast+ 2022-04-23
  upload_forcing orcinus turbidity 2022-04-23
  wait for run to finish
  upload_forcing orcinus nowcast+ 2022-04-24
  upload_forcing orcinus turbidity 2022-04-24
  wait for run to finish
  upload_forcing orcinus nowcast+ 2022-04-25
  upload_forcing orcinus turbidity 2022-04-25
Continued work to move SalishSeaNowcast/tidal_predictions/ to somewhere other than 
uncommited file in production clone:
* finshed writing README; with Susan's commentary
* moved files and notebooks from Nancy's analysis for 2016 paper into analysis/
* committed 2007-2030 files individually and pushed them in batches to keep git and GitHub happy
* moved 2013-2020 and 2015-2020 files into archival dir on khawla; not pushed to GitHub
* .git/ is 358M on khawla
(SalishSeaCast)

try3 runs:
* [1-20]-200 finished
* [21-25]-200 ready to be queued
(MIDOSS)

Group mtg; see whiteboard.
(MOAD)

Updated skookum-salish deploy docs re: tidal-predictions repo; merged PR#102.
Cloned tidal-predictions repo on skookum in place of earlier created tidal-predictions/ dir.
Pulled updates on skookum
(SalishSeaNowcast)


Tue 26-Apr-2022
^^^^^^^^^^^^^^^

Continued building 1-mo tarballs of nowcast-green.2019105 re-run in tmux session on chum 
and uploading to graham-dtn:/nearline; aug19, sep19
Weird network problems started at ~10:10;
* investigation:
  * uptimerobot reported erddap and site down; apparently a DNS nameserver issue
  * msg gaps in log
  * restarted log_aggregator
* recovery started at ~11:45:
  * uptimerobot reported erddap and site back up
  * manager got start msg from watch_NEMO nowcast
  * restarted automation:
      make_forcing_links arbutus ssh
      launch_remote_worker arbutus make_fvcom_boundary "arbutus x2 nowcast"
      download_results arbutus nowcast
(SalishSeaCast)

See work journal.
(Resilient-C)

Call from Doug Milne & Kile Landrigan of TD Wealth Mgmt; will connect us to someone in estate planning.

GitHub InFocus keynote:
* Thomas Dohmke, CEO
  * developer cloud; code spaces
  * AI: copilot
  * open source community: 
  * security: codeql, dependabot
* Matthew McCullough; SVP of product
* Kevin Alwell; enterprise solutions engineer
  * code to cloud demo
  * valet to analyze GHA workflows?
  * codespace; pre-built VMs
  * copilot; stats say it generates 35% of code in projects where it is used
  * projects
    * spreadsheet or kanban
    * task hierarchy
    * group by labels
  * code-search
  * push protection prevents pushing credentials, API tokens, etc.
* Eirini K; researcher
 * productivity
 * SPACE metrics; multi-dimensional
 * developer velocity website
 * The Good Day project; GitHub blog
   * devs distrust productivity tools
   * 3 mtgs/day == 60% drop in progress
   * 2 minute daily reflection

Started work to fix wwatch3 fig bug:
  2022-04-25 13:18:17,244 ERROR [make_plots] unexpected KeyError in make_figure:
  Traceback (most recent call last):
    File "/SalishSeaCast/SalishSeaNowcast/nowcast/workers/make_plots.py", line 1102, in _calc_figure
      fig = fig_func(*args, **kwargs)
    File "/SalishSeaCast/SalishSeaNowcast/nowcast/figures/wwatch3/wave_height_period.py", line 66, in make_figure
      plot_data = _prep_plot_data(buoy, wwatch3_dataset_url)
    File "/SalishSeaCast/SalishSeaNowcast/nowcast/figures/wwatch3/wave_height_period.py", line 95, in _prep_plot_data
      obs = moad_tools.observations.get_ndbc_buoy(buoy)
    File "/SalishSeaCast/moad_tools/moad_tools/observations.py", line 108, in get_ndbc_buoy
      df = df.rename(index=str, columns=columns).set_index("time").sort_index()
    File "/SalishSeaCast/nowcast-env/lib/python3.10/site-packages/pandas/util/_decorators.py", line 311, in wrapper
      return func(*args, **kwargs)
    File "/SalishSeaCast/nowcast-env/lib/python3.10/site-packages/pandas/core/frame.py", line 5494, in set_index
      raise KeyError(f"None of {missing} are in the columns")
  KeyError: "None of ['time'] are in the columns"
* Set up nowcast-fig-dev env on khawla.
* Resolved `FutureWarning: Use pd.to_datetime instead.` by changing from date_parser() 
  internal function to:
    date_parser=lambda x: pandas.to_datetime(x, format="%Y %m %d %H %M")
  arg in pandas.read_csv() in moad_tools.observations.get_ndbc_buoy().
* Struggled with renaming date/time column in get_ndbc_buoy().
(SalishSeaNowcast)


Wed 27-Apr-2022
^^^^^^^^^^^^^^^

Continued building 1-mo tarballs of nowcast-green.2019105 re-run in tmux session on chum 
and uploading to graham-dtn:/nearline; oct19, nov19
(SalishSeaCast)

Finished work to fix wwatch3 fig bug:
* Resolved renaming of date/time column and making it the index in get_ndbc_buoy():
    df.set_index(df.columns[0], inplace=True)
    df.index.rename("time", inplace=True)
    df.sort_index(inplace=True)
* Fixed pandas.DataFrame.loc() calls re: buoy obs column names in wave_height_period.py
* Improved wave_height_period.py with elimination of OpenDAP issue work-around that downloads 
  fields from ERDDAP instead of accessing them lazily via xarray.open_dataset()
* created, merged & deployed PR#103.
(SalishSeaNowcast)

Did year roll-over and other code maint on moad_tools pkg before committing wwatch3 fig fixes;
used SalishSeaCmd repo for guidance.
* PR#15:
  * bump version to 22.1.dev0
  * change copyright year range to end with `– present`
  * add SPDX short-form license identifiers
* PR#16:
  * change to run GHA workflows on push to any branch
  * drop pkg caching from GHA workflows
  * change GHA workflows to use mambaforge
* PR#17:
  * Add GHA CodeQL scanning workflow
  * Add CodeQL analysis badges to README & pkg dev docs
* PR#18:
  * add Python 3.10 to GHA pytest-coverage workflow
  * Change GHA linkcheck workflow to Python 3.10
  * Change to Python 3.10 for pkg dev
  * Update pkgs & versions used in recent dev env
Cleaned up stale local and remote branches.
Updated get_ndbc_buoy() re: wwatch3 fig bug(s) and other things; PR#19 - merged.
Created 22.1 release on GitHub; deployed it to skookum.
(MOAD)


Thu 28-Apr-2022
^^^^^^^^^^^^^^^

Continued building 1-mo tarballs of nowcast-green.2019105 re-run in tmux session on chum 
and uploading to graham-dtn:/nearline; dec19, jan20, feb20
(SalishSeaCast)

See work journal.
(Resilient-C)

Worked on income tax returns.


Fri 29-Apr-2022
^^^^^^^^^^^^^^^

Continued building 1-mo tarballs of nowcast-green.2019105 re-run in tmux session on chum 
and uploading to graham-dtn:/nearline; mar20, apr20, may20
(SalishSeaCast)

See work journal.
(Resilient-C)

AAPS spring general mtg.


Sat 30-Apr-2022
^^^^^^^^^^^^^^^

Continued building 1-mo tarballs of nowcast-green.2019105 re-run in tmux session on chum 
and uploading to graham-dtn:/nearline; jun20
upload_forcing orcinus nowcast+ failed; investigation:
* $HOME file system is read-only
(SalishSeaCast)

See work journal.
(Resilient-C)

Disabled cronjob for 2022.
(Bloomcast)


May
===

Sun 1-May-2022
^^^^^^^^^^^^^^

Continued building 1-mo tarballs of nowcast-green.2019105 re-run in tmux session on chum 
and uploading to graham-dtn:/nearline; jul20
(SalishSeaCast)

Reviewed income tax returns.


Week 18
-------

Mon 2-May-2022
^^^^^^^^^^^^^^

Paid income tax balances owing.

Continued building 1-mo tarballs of nowcast-green.2019105 re-run in tmux session on chum 
and uploading to graham-dtn:/nearline; apr22, aug20, sep20, oct20
Backfill nowcast-agrif since ssh issue on 30-Apr:
  wait for 02may run to fail
  upload_forcing orcinus nowcast+ 2022-04-30
  upload_forcing orcinus turbidity 2022-04-30
  wait for run to finish
  upload_forcing orcinus nowcast+ 2022-05-01
  upload_forcing orcinus turbidity 2022-05-01
  wait for run to finish
  upload_forcing orcinus nowcast+ 2022-05-02
  upload_forcing orcinus turbidity 2022-05-02
(SalishSeaCast)

Added Sphinx config to ignore private tidal-predictions repo so that GHA linkcheck workflow
stops failing.
(SalishSeaNowcast)

Group mtg; see whiteboard.
(MOAD)

Did year roll-over and other code maint on NEMO-Cmd pkg;
used moad_tools & SalishSeaCmd repos for guidance.
* PR#33:
  * bump version to 22.1.dev0
  * change copyright year range to end with `– present`
  * add SPDX short-form license identifiers
* PR#34:
  * change to run GHA workflows on push to any branch
  * drop pkg caching from GHA workflows
  * change GHA workflows to use mambaforge
  * add name to Slack channel notification step
  * drop MIDOSS slack notification step
* PR#135:
  * Add GHA CodeQL scanning workflow
  * Add CodeQL analysis badges to README & pkg dev docs
* PR#36:
  * add Python 3.10 to GHA pytest-coverage workflow
  * Change GHA linkcheck workflow to Python 3.10
  * Change to Python 3.10 for pkg dev
  * Rename readthedocs.yml to .readthedocs.yaml
  * Move requirements.txt to envs/
  * Update pkgs & versions used in recent dev env
Cleaned up stale local and remote branches.
Created 22.1 release on GitHub; deployed it to skookum.
Bumped version to 22.2.dev0.
(MOAD)

Added 2 new descriptions to cloud fraction mapping.
(Bloomcast)


Tue 3-May-2022
^^^^^^^^^^^^^^

Worked at ESB while Rita was at home.

Continued building 1-mo tarballs of nowcast-green.2019105 re-run in tmux session on chum 
and uploading to graham-dtn:/nearline; nov20, dec20, jan21, feb21, mar21
(SalishSeaCast)

Started work on archive_tarball worker:
* stdlib tarfile module should work:
  * with tarfile.open() as tar: tar.add()  # recursive dir/file additions
  * probably iterate over getmembers() to generate .index file
* sysrsync pkg (PyPI, not conda-forge) could be used for rsync to graham-dtn
  * thin wrapper around subprocess.run() on system-installed rsync
  * ubc GitHub org is listed in Used-by, for what that's worth
* possible command-lines:
    archive-tarball run-type yyyy-mmm dest-host
      e.g. archive-tarball nowcast-green 2022-may graham-dtn
  * NEMO only, always upload to remote storage
  * get source dir from config["results archive"][run-type]
  * split yyyy-mmm to get wildcard dirs; i.e. *mmmyy/
  * compose tarball name from last segment of source dir path and mmmyy
  * get dest-host directory from new config["results archive"]["remote"][dest-host]
  * compose remote storage path from dest-host
* started implementation in archive-tarbasll branch
(SalishSeaNowcast)

CIOPS went live on datamart; east/2km, west/2km, salishsea/500m; 4 x 48h runs per day.


Wed 4-May-2022
^^^^^^^^^^^^^^

uptimerobot reported ~3 min of downtime for arbutus at ~05:45; no evident affect.
Continued building 1-mo tarballs of nowcast-green.2019105 re-run in tmux session on chum 
and uploading to graham-dtn:/nearline; apr21, may21
/results filled during nowcast-x2 prep and stopped automation; recovery:
  rm -rf /results/nowcast-dev.201905/*21/
  launch_remote_worker arbutus make_fvcom_boundary "arbutus x2 nowcast"
  make_turbidity_file
  download_results arbutus forecast
(SalishSeaCast)

See work journal.
(Resilient-C)


Thu 5-May-2022
^^^^^^^^^^^^^^

Continued building 1-mo tarballs of nowcast-green.2019105 re-run in tmux session on chum 
and uploading to graham-dtn:/nearline; jun21, jul21, aug21, sep21
Forgot to deal with collect_weather in yesterday's failure; recovery:
  kill collect_weather 18 2.5km
  rm -rf /results/forcing/atmospheric/GEM2.5/GRIB/20220504/18
  download_weather 18 2.5km
  download_weather 00 2.5km
  download_weather 06 2.5km
  download_weather 12 1km --yesterday
  collect_weather 18 2.5km &&
  wait for forecast2 runs to finish
  download_weather 12 2.5km
(SalishSeaCast)

See work journal.
(Resilient-C)


Fri 6-May-2022
^^^^^^^^^^^^^^

Continued building 1-mo tarballs of nowcast-green.2019105 re-run in tmux session on chum 
and uploading to graham-dtn:/nearline; oct21, nov21, dec21
(SalishSeaCast)

Continued work on archive_tarball worker.
(SalishSeaNowcast)

Revised and re-printed J&M income tax returns.


Sat 7-May-2022
^^^^^^^^^^^^^^

Drove to White Rock to visit J&M


Sun 8-May-2022
^^^^^^^^^^^^^^

Goofed off and washed Cannondales.


Week 19
-------

Mon 9-May-2022
^^^^^^^^^^^^^^

Filed income tax returns.

Created notebook in analysis-doug re: accessing SalishSeaCast NEMO datasets via from 
ERDDAP via xarray for Prodigy field school.
(EOAS Teaching)

MOAD group mtg.
(MOAD)

Debi arrived to stay overnight prior to Tereza's defense; 
1st visitor since start of COVID in Mar-20


Tue 10-May-2022
^^^^^^^^^^^^^^^

See work journal.
(Resilient-C)

FAL estate work: deposit MFC & BCE dividend cheques.

Tereza's defense.


Wed 11-May-2022
^^^^^^^^^^^^^^^

Vancouver to Dove Creek Farm


Thu 12-May-2022
^^^^^^^^^^^^^^^

Dove Creek Farm

try3 runs:
* [1-20]-200 finished
* [21-25]-200 queued
(MIDOSS)

Tried to cycle to Comox Lake but turned back at private raod logging closure on 
Duncan Bay Mainline Rd. Cut ride short due to increasing rainfall rate.


Fri 13-May-2022
^^^^^^^^^^^^^^^

Dove Creek Farm

try3 runs:
* [1-25]-200 finished
* had to backfill hdf5-to-netcdf4 for 2 spills in 25-200
(MIDOSS)

See work journal.
(Resilient-C)

Cycled to Campbell River w/ Susan and back alone, via backroads where possible;
on hwy 19a from north of Merville to south of Shelter Point. 
(100 km)


Sat 14-May-2022
^^^^^^^^^^^^^^^

Dove Creek Farm

Paid 2021 income tax installment interest owing.

Goofed off.

Cycled a loop through Courtenay and Comox; up Vanier Dr. hill, back along Back Rd.
(27 km)


Sun 15-May-2022
^^^^^^^^^^^^^^^

Dove Creek Farm

try3 runs:
* [1-25]-200 finished
* [26-30]-200 queued
(MIDOSS)

Network failed in afternoon; lots of time w/ host & Telus support getting it restored.

Didn't cycle due to heavy-ish rain.


Week 20
-------

Mon 16-May-2022
^^^^^^^^^^^^^^^

Dove Creek Farm

Cycled back roads route to Campbel River as far at Howard Rd & Hwy 19A to meet Susan,
Becca & Birgit.
(34.5 km)

try3 runs:
* [1-25]-200 finished
* [26-30]-200 running
(MIDOSS)


Tue 17-May-2022
^^^^^^^^^^^^^^^

Dove Creek Farm

try3 runs:
* [1-27]-200 finished
* [28-30]-200 failed, probably due to file system issues; re-queued
(MIDOSS)

Cycled to Cumberland, Bevan and twice to Comox Lake.
(55 km)


Wed 18-May-2022
^^^^^^^^^^^^^^^

Dove Creek Farm

try3 runs:
* [1-30]-200 finished
* [31-35]-200 queued
(MIDOSS)

See work journal.
(Resilient-C)

Rest day from cycling; planned due to storm warming, though storm passed mostly overnight.


Thu 19-May-2022
^^^^^^^^^^^^^^^

Dove Creek Farm

try3 runs:
* [1-30]-200 finished
* [31-34]-200 failed, lots of core dumps
* 35-200 running
(MIDOSS)

Cycled loop through Comox to Point Holme, Kye Bay, Heritage Aircraft Park, Merville, Headquarters,
Tsolumn River Rd.
(65 km)


Fri 20-May-2022
^^^^^^^^^^^^^^^

Dove Creek Farm to Parksville

try3 runs:
* [1-30,35]-200 finished
* [32,34]-200 failed, lots of core dumps; re-queued
* [31-34]-200 running
* [31,33]-200 failed due to bogus disk quota exceeded on /scratch; re-queued
(MIDOSS)


Sat 21-May-2022
^^^^^^^^^^^^^^^

Parksville to Vancouver

try3 runs:
* [1-30,32,34-35]-200 finished
* [31,33]-200 running
* [36-30]-200 queued
(MIDOSS)


Sun 22-May-2022
^^^^^^^^^^^^^^^

try3 runs:
* [1-30,32-40]-200 finished
* 31-200 had 8 hdf5-to-netcdf4 failures; backfill job running
* [41-44]-200 running
* 45-200 queued
(MIDOSS)

Cycled to Iona and home via Canada Line bridge & Heather.
(40 km)


Week 21
-------

Mon 23-May-2022
^^^^^^^^^^^^^^^

**Statutory Holiday** - Victoria Day

try3 runs:
* [1-45,50]-200 finished
* 50-200 is short - 33 spills
(MIDOSS)

Installed new smoke alarms.

Prepped excess bikes for donation.


Tue 24-May-2022
^^^^^^^^^^^^^^^

try3 runs:
* [1-50]-200 finished
* 50-200 is short - 33 spills
* 67 of 10_000 spills w/ volume of <3 litres not run through MOHID
(MIDOSS)

Updated PyCharm to 2022.1.1.

Continued dev of archive_tarball worker:
* created PR#104
* tested tarball & index creation for 2007-jan on skookum in archive_tarball tmux session
  * takes 1m16s per results day to add to tarball; 35-40m per month
* rsync upload speed from skookum is quite irratic
* updated /SalishSeaCast/nowcast-env prod env on skookum to add sysrsync pkg; got other pkg updates
* tested tarball & rsync functionality for 2007-feb on skookum in archive_tarball tmux session
* added archive_tarball to next_workers to run for nowcast-green results after last run of the month
(SalishSeaNowcast)

collect_river_data failure that started on 18-May is for San Juan River at Port Renfrew;
"cableway is currently out of service".
(SalishSeaCast)

Group mtg:
* planning;
  * present pub, or show work
  * lots of pubs on OP site
  * I present on 19-Jul
(Ocean Parcels)

Learned that sshfs -o nonempty is now default behaviour and nonempty option has been removed
in version of libfuse installed with 22.04.


Wed 25-May-2022
^^^^^^^^^^^^^^^

See work journal.
(Resilient-C)

upload_forcing to graham failed due to maintenance there
(SalishSeaCast)

Continued dev of archive_tarball worker:
* deployed next_workers update to skookum for testing in automation tomorrow;
  restarted manager
Fixed redirected links in docs.
(SalishSeaNowcast)

FAL estate work:
* appt w/ Sahi at TD branch to deposit DRS shares to my direct account; fail


Thu 26-May-2022
^^^^^^^^^^^^^^^

Telcon w/ Andres @ TD re: BCE DRS and estate planning.
FAL estate work: emailed DRS & cover letter to Andres.

graham-dtn ssh key auth failing; sent email to support; no response, but auth
started to work a couple of hours later.
backfill upload_forcing graham:
  upload_forcing graham nowcast+ 2022-05-25
  upload_forcing graham turbidity 2022-05-25
  upload_forcing graham nowcast+ 2022-05-26
  upload_forcing graham turbidity 2022-05-26
Transfer speed to graham-dtn was terrible: ~500 kB/s compared to ~30 MB/s before
shutdown; did mar07 tarball rsync from chum to graham-hindcast at ~35 MB/s.
Helped Karyn get plots of NPGO from .csv via pandas and overlay monthly phyto/zoo averages.
(SalishSeaCast)

Squash-merged dependabot PR in UBC-MOAD/docs re: ujson.
(MOAD)

PyCharm Functools Webinar:
* Mike Driscoll
* caching decorators:
  * cache 3.9
    * lru_cache(maxsize=None)
  * cache_property 3.8
  * lru_cache
* total_ordering
  * class decorators
  * infers comparison methods from __lt__ and __eq__
* partial
  * GUI programming use case; tkinter, wxPython
  * Mouse vs Python article
  * alternative to lambda
* reduce
  * Real Python article
  * replacement for former builtin
  * alternative to lambda
* singledispatch
  * function overloading decorator
  * dispatches based on type for 1st arg
  * multiple dispatch options; pkgs:
    * Plum
    * MultipledDspatch
* wraps 
  * for custom decorators
  * cleans up passing through decorated function name & docstring
  * Real Python article

Phys Ocgy seminar: Greg Crawford re: tsunami measurements at Humboldt CA re:
Honga Tonga erruption and other signals

Team mtg.
(Atlantis)


Fri 27-May-2022
^^^^^^^^^^^^^^^

Continued dev of archive_tarball worker:
* added deletion of tarball and index after successful rsync
* improved test coverage
(SalishSeaNowcast)

HRDPS 12 was late: ~11:00
(SalishSeaCast)

UBC-DFO modeling mtg:
* Laura re: new bathymetry in fjords

Finished writing model profile file docs.
(Reshapr)


Sat 28-May-2022
^^^^^^^^^^^^^^^

Drove to White Rock to visit J&M.


Sun 29-May-2022
^^^^^^^^^^^^^^^

Bike work:
* prepped Gunnar & Pico for fast road rides:
  * mud guards off
  * Garmin mount & cadence sensor on Gunnar
* checked clearance w/o mudgaurds for wider tires; 28 okay, 30 might be tight


Week 22
-------

Mon 30-May-2022
^^^^^^^^^^^^^^^

Emailed support re: slow graham-dtn transfers.
/results filled during nowcast-blue download; recover:
  rm -rf nowcast-dev.201905/23apr21.aside*
  rm -rf nowcast-blue.201905/*21
  make_turbidity_file
  make_fvcom_atmos_forcing
  download_results nowcast
  download_results forecast
  find nowcast-dev.201905/ -type d -name "*jan22" | xargs rm -rf
  find nowcast-dev.201905/ -type d -name "*feb22" | xargs rm -rf
  find nowcast-dev.201905/ -type d -name "*mar22" | xargs rm -rf
  find forecast2.201905/ -type d -name "*jan22" | xargs rm -rf
  find forecast2.201905/ -type d -name "*feb22" | xargs rm -rf
  find forecast2.201905/ -type d -name "*mar22" | xargs rm -rf
(SalishSeaCast)

Group mtg; see whiteboard.
(MOAD)

Started adding SalishSeaCast.201905 model profile
(Reshapr)


Tue 31-May-2022
^^^^^^^^^^^^^^^

Dentist appt.

Worked at ESB while Rita was at home.
Did extended commute ride as a sub for FTP builder Week 5 Day 2 foundation training
because the weather was nice, and it is Bike to Work Week.

Finished adding SalishSeaCast.201905 model profile; PR#29 merged.
(Reshapr)

archive_tarball for may was launched successfully by automation and successfully
created tarball and index; rsync to graham-dtn is slow but proceeding.
(SalishSeaCast)


June
====

Wed 1-Jun-2022
^^^^^^^^^^^^^^

SHARCNET Python & Numba:
* Pawel Pomorski, Waterloo
* @numba.jit(nopython=True) or @numba.njit
  * fail if code is not numba-compilable
* pre-compile mode not covered
* numba does type inferral, but can be explicit too; inferral is generally good enough
* contrived example: 
  * Euler proejct problem 39; integral length right triangles
  * 273 x speed-up
* numba does not not know about pandas
* numba does know about numpy
* contrived example: 2D diffusion equation with 2 for loops:
  * 309 x speed-up
  * for comparison, numpy vectorized version of code has 157 x speed-up
  * note though that running vectorized code w/ numba is 1.4x slower probably due to compilation
    of already compiled code
  * numba implementation is probably more readable
* numba supports only a subset of Python
  * refactor code into jit-able functions for the hot loops
  * numba has trouble with complex list data structures; replace with numpy arrays and operations;
    limited to homogenous type lists
  * copy.deepcopy() doesn't work with numba;
    * convert list to numpy array, use numpy.copy(), convert back to list
  * filtering list of lists via filter(lambda ...):
    * convert list to numpy array, use numpy logical ops for comparison, convert back to list
* parallel numba
  * @njit(parallel=True), but it's complicated
  * compilation for GPU is also possible

FAL estate work:
* Andres advised me to call estates to arrange how to handle DRS
* Estates agent (no name) says that an agent named James is working with TD Direct on a solution;
  will contact me later today or tomorrow
* emailed CRA notice of assessment to Cameron w/ update re: BCE & MFC shares
* emailed Sahi w/ update re: BCE shares

Squash-merged dependabot PR in docs repo re:ujson.
Squash-merged PR#104 re: archive_tarball worker and deployed main to production.
Automation archive_tarball may22 is still rsync-ing slowly to graham-dtn.
rsync-ed jun07 tarball to graham-hindcast in reaonable time.
Changed production config to use graham-hindcast for archive_tarball backfilling;
* started jul07; xfer was slow, so stopped it and tried explicit rsync; fast
* poked around and found that fast rsync is going to gra-login2
Explored how to rotate hindcast log files:
* nemo_nowcast.workers.rotate_logs is no config-driven enough
* options:
  * add maxBytes to config to rotate on size; unpredictable rotation timing
  * change to TimedRotatingFileHandler; might replace backup log files with empty files over time
  * improve nemo_nowcast.workers.rotate_logs; default rotation would be daily
* discussed w/ Susan who came up with the idea of a manually launched 
  SalishSeaNowcast.workers.rotate_hindcast_logs worker
(SalishSeaCast)

Toured repos w/ GHA workflows to re-enable any scheduled workflows that have been automatically
disabled due to inactivity.
(MOAD)


Thu 2-Jun-2022
^^^^^^^^^^^^^^

Squash-merged dependabot PR in moad_tools re: Pillow.
(MOAD)

archive_tarball sep07 to gra-login2 failed waiting for known hosts key acceptance;
started rsync; archive_tarball oct07 was successful to gra-login2 start to finish;
started loop for nov07-dec07; success; started loop for 2008.
may22 rsync is still going...
Continued work on rotate_hindcast_logs; PR#105.
(SalishSeaCast)

Team mtg
(Atlantis)

Did outdoor ride as a sub for FTP builder Week 5 Day 4 foundation training
to pick up cables from West Point, and it is Bike to Work Week; middle velcro closure
on workhorse Sidi shoes blew up.


Fri 3-Jun-2022
^^^^^^^^^^^^^^

archive_tarball loop for 2008 working well
may22 rsync is still going...
(SalishSeaCast)

Installed Vittoria Corsa 28mm tires w/ Champion latex tubes on Gunnars.
Installed chain and new rear brake cable w/o coupler on Impe.


Sat 4-Jun-2022
^^^^^^^^^^^^^^

Rode a loop of west side bike routes between rain systems; 10th, Ontario, Ridgeway, Trafalgar,
29th, Imperial, Discovery, Off-Broadway.
(20.5 km)

NEMO forecast failed on 1st time step due to high current near west boundary;
that caused forcing prep for wwatch3 to fail
recovery:
  Susan smoothed nowcast-blue restart file
  wait for nowcast-green to finish
  rsync restart to arbutus
  make_forcing_links ssh forecast
  kill watch_NEMO
  wait for forecast runs to finish
  download_results arbutus forecast
  launch_remote_worker make_ww3_wind_file arbutus "arbutus forecast"
  launch_remote_worker make_ww3_current_file arbutus "arbutus forecast"
Helped Susan do prod test of rotate_hindcast_logs; worked but unregistered worker error because
manager had not been restarted; that make me realize that I didn't write the after_ function
for it or for archive_tarball.
Investigated how to write a test to confirm that all modules in nowcast.workers have a
corresponding after_ function in next_workers; 2 possibilities:
* inspect.getmembers(next_workers, inspect.ifucntion)
* ast.parse() and isinstance(func, ast.FunctionDef)  # does not require import of next_workers
collect_weather 18 finished after 17:08, so download_weather 1km 00 failed
may22 rsync is still going...
archive_tarball loop for 2009 started
(SalishSeaCast)


Sun 5-Jun-2022
^^^^^^^^^^^^^^

uptimerobot reported web site down for 18 minutes overnight starting at 2022-06-04 22:24:42.
Tried to backfill yesterday's 1km 00 weather forecast, but files were gone.
nowcast-blue failed due to high velocity at west boundary; recovery:
  Susan smoothed nowcast-green/04jun22 restart file
  rsync restart to arbutus
  make_forcing_links arbutus nowcast+
may22 rsync finished!!!
archive_tarball loop for 2009 finished and 2010 started
(SalishSeaCast)

Researched password managers:
* https://www.wired.com/story/best-password-managers/
* LastPass is the one that fell into disrepute (bait & switch) in 1-Feb-2022
  by reducing free tier support and charging separately for mobile & desktop
* 1Password is highly rated, Canadian, and has a family mgmt plan for 5 users;
  also has auth app functionality for 2fa

Moved failed MIDOSS runs to borked dir
Ran 51-10 make-up runs that Susan created .csv file for.
(MIDOSS)


Week 23
-------

Mon 6-Jun-2022
^^^^^^^^^^^^^^

archive_tarball 2010-jun failed with broken pipe error
(SalishSeaCast)

Added after_rotate_hindcast_logs(); merged PR#105
Started work on adding TestAfterWorkerFunctions.
Discussed w/ Susan deleting old upload_all_files worker; she agreed.
(SalishSeaNowcast)

Group mtg.
(MOAD)

Haircut.


Tue 7-Jun-2022
^^^^^^^^^^^^^^

Disconnected all bluetooth devices (mouse & headphones) from khawla.
Confirmed that sleep works via keyboard, though there is still a syslog msg too fast to read.
Re-connected mouse; sleep fails, and failed during re-start; had to cycle power. Scary.

archive_tarball loop for 2010 finished
2010-jun tarball & index rsync-ed manually to gra-login2
Email conversation w/ Kaizaad Bilimorya @Guelph re: graham xfer rates;
confirmed my obs re: login2 vs. dtn, login1 & login3; says problem is resolved.
Tested graham dtn, login1 & login3 rates:
  tar cvvf /ocean/dlatorne/nowcast-green.201905-jan11.tar \
    /results2/SalishSea/nowcast-green.201905/*jan11 \
    | tee /ocean/dlatorne/nowcast-green.201905-jan11.index
  rsync -tv --progress /ocean/dlatorne/nowcast-green.201905-jan11.* \
    graham-dtn:/nearline/rrg-allen/SalishSea/nowcast-green.201905/
  * jan11 to graham-dtn: back-ish to pre-25-may transfer rate
  * feb11 to gra-login1: back-ish to pre-25-may transfer rate
  * mar11 to gra-login3: back-ish to pre-25-may transfer rate
(SalishSeaCast)

Deleted upload_all_files worker; PR#106; merged.
Added TestAfterWorkerFunctions class and after_archive_tarball(); PR#107; merged.
Reverted temporary change from graham-dtn as file transfer destination because it is working
at normal speed again.
Pulled updates into production; restarted manager.
(SalishSeaNowcast)

Group mtg: Jose presented Fischer, et al (2021) paper:
* Modeling submerged biofouled microplastics and their vertical trajectories
  links in Slack channel
* Jose's M.Sc. colleague
* will do future PO seminar
* diatoms dominate for 1st week, but bacterial take over
(OceanParcels)

UBC Alumni Fire & Floods Panel:
* last miunte change to just wildfires
* Intro: Rob Kozak
* Moderator: Johanna Wagstaffe
* Speaker: Lori Daniels, tree-ring lab
  * almost everything about forest mgmt since late-1800s has been wrong (my words, not her's)
    especially 100% goal for fire suppression
  * learn to live with fire
  * ground burns instead of crown burns
  * controlled burns in spring (not sure if she said autumn too)

Checked status of mods & resource packs for 1.19:
* updated:
  * sodium
  * iris-2.0.4
  * vanilla tweaks:
    * data packs:
      * 2x shulker shells v1.3.3 to server
      * coordinates HUD v1.2.3 - to server
    * resource packs:
      * Lower Shield
      * Redstone Devices:
        * Sticky Piston Sides
        * Directional Hoppers
        * Directional Dispensers & Droppers
        * Directional Observers
        * Groovy Levers
        * RedstoneWireFix      
      * Borderless Stained Glass
      * Clearer Water

      * Colourful Enchanting Table Particles
      * Flint Tipped Arrows
      * Accurate Spyglass
      * Fancy Sunflowers
      * SlimeParticleFix
      * Block Sides:
        * Grass Sides
        * Mycelium Sides
        * Grass Path Sides
        * Podzol Sides
        * Snow Sides
        * Crimson Nylium Sides
        * Warped Nylium Sides
* not updated yet:
  * lithium
  * phosphor
  * malilib
  * minihud
  * litematica
Created "Uncharmed Link" backup on Nodecraft; downloaded it to play with MCASelector.
Installed MCASelector in ~/MCASelector/ and explored world map.
Changed Nodecraft server to run minecracft=1.19 and fabric=1.19-0.14.6
via 1-click installer and archiving files to _old_files/;
Restored world files by copying from _old_files/:
  1_18-1/ (world)
  banned-ips.json
  banned-players.json
  ops.json
  server.properties
  whitelist.json
Successfully tested world w/ 1.19 client.
Downloaded VanillaTweak double_shulker_shells-v1.3.3, stopped server, uploaded it to replace
v1.3.2, and restarted server.
Downloaded VanillaTweak coordinatesHUD-v1.2.3, stopped server, uploaded until MiniHUD
gets updated, and restarted server.


Wed 8-Jun-2022
^^^^^^^^^^^^^^

archive_tarball loop for 2011 started w/ apr after manual tests for Kaizaad.
(SalishSeaCast)


Thu 9-Jun-2022
^^^^^^^^^^^^^^

upload_forcing orcinus turbidity failed; orcinus refusing network connections
archive_tarball loop for 2011 finished
archive_tarball loop for 2012 started
(SalishSeaCast)

Phys Ocgy seminar: Becca

ATSC seminar: Susan

Team mtg
(Atlantis)


Fri 10-Jun-2022
^^^^^^^^^^^^^^^

SMS to Paul Kim re: plumbing repairs.

Squash-merged dependabot pull requests re: cookiecutter:
* AtlantisCmd
* MOHID-Cmd
* WWatch3-Cmd
* cookiecutter-analysis-repo
* cookiecutter-MOAD-pypkg
* cookiecutter-djl-pypkg
(MOAD)

orcinus is back after file system maintenance; recovery:
  with for nowcast-agrif run to fail
  upload_forcing orcinus turbidity 2022-06-09
  upload_forcing orcinus turbidity 2022-06-10
* host key algorithm mismatch on connections from khawla, but okay from skookum
  * this appears to be an issue of OpenSSH_8.9p1 on khawla not wanting to use the ssh-rsa
    host key algorithm offered by OpenSSH_6.4p1-hpn14v1 on orcinus;
    kwala wants diffie-hellman-group-exchange-sha256
  * similar issue with public key signature algorithm
  * resolution:
      add 2 lines of ssh config for orcinus host aliases on khawla:
        HostKeyAlgorithms=+ssh-rsa
        PubkeyAcceptedKeyTypes=+ssh-rsa
  * sent FYO email to Mark
* same story between khawla and optimum; sent FYI Slack msg to Henryk
archive_tarball loop for 2012 failed because I didn't change gra-login2 to graham-dtn :-(
started rsync-ing 2012 tarballs & indexes
(SalishSeaCast)

Started work on time-averaging (aka resampling):
* resampling is a special case of xarray/pandas group-by functionality that is specific to
  time coordinates
* pandas/xarray refer to time intervals/frequencies for resampling as "offsets"
* pandas docs list of "offset aliases":
    https://pandas.pydata.org/docs/user_guide/timeseries.html#offset-aliases
* challenges:
  * due to flexibility of pandas/xarray offset aliases mini-language:
    * choice of time_offset and time_example in calc_output_coords()
    * choice of quanta and time_offset in calc_coord_encoding()
  * file names:
    * we have used NEMO convention: e.g. SalishSea_1m_202012_202012_ptrc_T.nc
      but reshapr convention is to provide file name stem to which date range and extension
      are appended; e.g. SalishSeaCast_1m_ptrc_T_202012_202012.nc
* proof of concept test of resampling added to extract sub-command worked
(Reshapr)


Sat 11-Jun-2022
^^^^^^^^^^^^^^^

Cycled to/from White Rock to visit J&M.
105 km


Sun 12-Jun-2022
^^^^^^^^^^^^^^^

upload_forcing orcinus failed for forecast2, nowcast+ & turbidity
(SalishSeaCast)


Week 24
-------

Mon 13-Jun-2022
^^^^^^^^^^^^^^^

orcinus network was disconnected Sat night due to fibre cut; restored Sun night; recovery:
  with for nowcast-agrif run to fail
  upload_forcing orcinus nowcast+ 2022-06-12
  upload_forcing orcinus turbidity 2022-06-12
  upload_forcing orcinus turbidity 2022-06-13
Email conversation w/ Jenn at ECCC re: Fraser buoy; she suspects impact damage to sensor due
to river debris.
(SalishSeaCast)

Continued work on resampling.
(Reshapr)

Group mtg.
(MOAD)


Tue 14-Jun-2022
^^^^^^^^^^^^^^^

Worked at ESB while Rita was at home.

Continued work on resampling:
* reviewed resampling implementation
(Reshapr)

Picked Susan up from skin surgery.

Deleted nested world saves from running world on nodecraft; 
reduced backup size from 8.8Gb to 2.4Gb

Set up family account trial on 1password.ca.


Wed 15-Jun-2022
^^^^^^^^^^^^^^^

Explored 1password more; helped Susan get set up.

Continued work on resampling:
* pushed resampling code; PR#30
* add CLI override for config file start/end dates to make month-average resampling
  easier to automate
(Reshapr)


Thu 16-Jun-2022
^^^^^^^^^^^^^^^

Tested resampling on salish to produce month-averaged files from 201905 re-run:
* worked in /results2/SalishSea/month-avg.201905/
* biology variables to ptrc_T: okay
* physics tracer variables to grid_T: okay
* lots of variables in day-avg files lack standard_name attrs:
  * carp_T:
    * PAR
  * dia2_T:
    * all variables
  * prod_T:
    * all variables except co2_flux_mmol_m2_s
* decided w/ Susan to not produce grid_[UVW] datasets because they would have to come from
  hour-averaged
* successfully ran bash loop to produce 2007 jan-mar physics & biology files
  on a 4 worker x 4 threads stand-alone cluster in tmux on salish
Started writing docs about dask cluster mgmt because I need to re-learn how to 
manage a stand-alone cluster on salish that I can run a resampling loop against.
(Reshapr)

Team mtg.
(Atlantis)


Fri 17-Jun-2022
^^^^^^^^^^^^^^^

Continued writing docs about dask cluster mgmt.
Successfully ran bash loop to produce 201905 re-run 2007 month-averaged apr-dec 
physics & biology files on a 4 worker x 4 threads stand-alone cluster in tmux on salish: 8m3.7s.
Added analysis-doug/notebooks/CompareReshapr-ncraMonthAvgs.ipynb.
(Reshapr)

Ran bash loop to produce 201905 re-run month-averaged physics & biology files
on a 4 worker x 4 threads stand-alone cluster in tmux on salish 
in /results2/SalishSea/month-avg.201905/:
2008: 12m58.7s
2009: 12m7.5s
2010: 12m3.8s
2011: 10m20.2s  after nowcast-dev finished
2012: 10m24.4s
(SalishSeaCast)

Squash-merged dependabot PRs re: token brute-forcing CVE in notebook:
* analysis-doug/melanie-geotiff
* analysis-doug/dask-expts
(MOAD)

(See work journal.
(Resilient-C))

Cleared leaves and other decayed stuff from patio and scrubbed it with bleach solution.
Cleaned grill cover with bleach solution.
Strained back.


Sat 18-Jun-2022
^^^^^^^^^^^^^^^

Ran bash loop to produce 201905 re-run month-averaged physics & biology files
on a 4 worker x 4 threads stand-alone cluster in tmux on salish
in /results2/SalishSea/month-avg.201905/:
2013: 10m2.6s
2014: 10m8.8s
2015: 10m6.2s
2016: 10m11.1s
2017: 10m17.0s
2018: 9m55.0s
(SalishSeaCast)


Sun 19-Jun-2022
^^^^^^^^^^^^^^^

Ran bash loop to produce 201905 re-run physics & biology files
on a 4 worker x 4 threads stand-alone cluster in tmux on salish
in /results2/SalishSea/month-avg.201905/:
2019: 10m18.7s
2020: 11m40.5s
2021: 12m29.1s
2022: 5m44.7s
(SalishSeaCast)


Week 25
-------

Mon 20-Jun-2022
^^^^^^^^^^^^^^^

Squash-merged dependabot PR re: old Numpy 1.8.0 in SOG-bloomcast.
(SOG)

Merged PR#30 re: resampling implementation.
Changed salish cluster description to 4 workers w/ 4 threads each based on last week's
month-avg work.
Add docs re: using a persistent cluster; PR#31
Set up VSCode for reStructuredText editing of docs.
* Used https://github.com/ammaraskar/sphinx-problem-matcher to add a VSCode problem-matcher
  to sphinx build task.
(Reshapr)

Group mtg.
(MOAD)


Tue 21-Jun-2022
^^^^^^^^^^^^^^^

PyCharm webinar about pandas:
* Matt Harrison, Trainer, Consultant, Author of Effective Pandas
* Jodie Burchell, Dev Advocate, Data Science, JetBrains
* Matt:
  * DataSpell product: fancy Jupyter
  * modin: alt to pandas for scaling, related to ponder start-up
  * ensure types are correct after loading data
    * pandas is in-memory, and greedy
    * over-eager: ints default to int64
    * autos[cols].dtypes
      * int64 can't have missing values; if missing values ints are coerced to float64
        that can have missing
      * Int64 also exists; it supprts missing data; Matt doesn't like
      * new pandas string type supports missing data
    * often missing data tells a story
    * autos[cols].memory_usage(deep=True).sum()
      * deep digs into Python objects in numpy arrays (e.g. strings)
  * data cleaning should be in code, not spreadsheet to that there is reasoning
    and a trail
  * autos[cols].select_dtypes(int).describe()
    * write code using chaining:
        (autos
            [cols]
            .select_dtypes(int)
            .describe()
        )
  * numpy.iiinfo(numpy.int)
  * convert types using astype()
  * count in describe() result is number of non-missing values, not numner of rows
  * autos[cols].query("cylinders.isnan()")
  * assign() method very valuable for chaining
  * object columns:
    * value_counts(dropna=False)
    * look for opportunities to convert to categorical type to save memory
    * str.extract() to split data like tranmission type
  * chaining is a constraint that can lead to better code
    * use .pipe() if you can't chain
      * pass in an arbitrary function to operate; 
        e.g. extract intermediate data frame for debugging
  * Matt tweeted notebook
  * .sample() to get a portion of data to speed up dev of chain
* Jodie:
  * DataSpell demo
    * interactive frames
    * deep auto-completion
    * in-built pandas docs
  * DataSpell is bundled in PyCharm as the Jupyter plugin

Birgit presenting paper:
* Kehl, C., Fischer, R. P. B., & Sebille, E. V. (2021). 
  Practices, pitfalls and guidelines in visualising lagrangian ocean analyses. 
  ISPRS Annals of the Photogrammetry, Remote Sensing 
  and Spatial Information Sciences, 217-224.
(OceanParcels)

Worked on EGBC CE program requirements:
* Regulatory Learning module
  * annual
  * indigenous people and practice at least 1 in 3 years
  * Professional Goverance Act (PGA)
    * applies to multiple self-regulating professions
    * Office of Superintendent of Professional Goverance in Ministry of Attorney General
    * engineers, geoscientists, foresters, argologists, applied biologists, app sci techs, 
      architects
  * Code of Ethics changes
    * 12 standardized principles; 1 extra for EGBC
      * Act in the Public interest
      * Know your limits
      * Follow the Law
      * Follow govt & EGBC standards
      * Maintain Competence
      * State Qualifications Accurately
      * Distinguish Facts from Assumptions
      * No Conflicts of interest
      * Duty to report
      * Stand Your ground
      * Each Professional is Responsible
      * Work Diligently & Follow Standars of Documentation
      * Do Unto Others
    * CE program
      * 60 hr per 3 yr period, or 20 hrs per yr average
      * reporting year starts 19-Jul
      * 1st 3 yr period started 1-Jul-2021
      * 4 areas of learning:
        * Ethics
          * EDI
          * 1 hr required per year
        * Regulatory
          * quality mgmt
          * 1 hr required per year; annual module
        * Technical
          * climate change
        * Comms & Leadership
      * CE plan:
        * annual
      * verification:
        * annual reporting 
        * audit
          * random selection
        * practice review
          * response to issue arising
    * Regulation of Firms
      * ethics, CE, quality mgmt
      * 8 hr self-paced training module <-*
      * Professional Practice Mgmt Plan
      * audit requirements
    * Audit & Practice Reviews
      * at least 1% selection annually
      * questionnaire and possible interview
    * Quality Mgmt requirements:
      * review guidelines & advisories <-*

Tried to add model profile for month-avg 201905 dataset; extract fails because it looks 
for day-by-day files; created issue #32.
Started work on info sub-command; created PR #33.
(Reshapr)


Wed 22-Jun-2022
^^^^^^^^^^^^^^^

Squash-merged dependabot PRs re: numpy string comparisons
* MOHID-Cmd
* Make-MIDOSS-Forcing
(MIDOSS)

Dropped SalishSeaTools editable install from rpn-to-gemlam requirements.txt
to enable dependabot to generat PRs.
Squash-merged 6 dependabot PRs in rpn-to-gemlam re: numpy, py, pygments, urllib3,
babel, jinja2, and cryptography.
(SalishSeaCast)

Started niko and wifi adapter is working again!
Updated niko from 21.04 to 21.10 to 22.04.

Worked on EGBC CE program requirements:
* Land Acknowledgements for Engineers and Geoscientists
  * doc on Engineers Canada website
  * panel
    * Matthew Dunn
    * Nalaine Morin
    * Chief Leah George-Wilson
      * land acknowledgements are part of 1st nations law
      * land acks are 1st step in reconciliation
      * no "tooth" at the end of Tsleil-Waututh
    * Linda Murphy
      * Manitoba
      * land acks are a good start; learn about history of people
      * be respectful, have humility
      * geoscience scales are not dissimilar to 1st nations scales
  * discussion questions:
    * how do you respond to people who want to improve land acks?
      * Chief Leah George-Wilson
        * learn the name of the people
      * Linda Murphy
        * do some research about people; listen
      * Nalaine Morin
        * not about checking a box; about understanding values
    * how can land acks impact decolonization?
      * Nalaine Morin
        * recognize that 1st nation people live on the land and have since forever
      * Linda Murphy
        * science can be informed by 1st nations ways of knowing
      * Chief Leah George-Wilson
        * step 1
        * step 2: learn more
        * indigenous knowledge *is* science
    * what suggestions do you have to make land aks non-tokenistic?
      * Nalaine Morin
        * understand why land ack
      * Chief Leah George-Wilson
        * indigineous people are all about protocol & ceremony
      * Linda Murphy
        * be open ot being corrected
        * don't appropriate - not settlers place to educate about 1st nations

Explored the idea of having `reshapr info` show the installed location of the package;
doesn't seem possible in an unhacky way, probably due to editable install.
(Reshapr)


Thu 23-Jun-2022
^^^^^^^^^^^^^^^

graham down for a week-long maintenance; upload_forcing failed

Created NEMO weights file for HRDPS ops dataset in SSC double resolution expt:
* ref: https://salishsea-meopar-docs.readthedocs.io/en/latest/code-notes/salishsea-nemo/nemo-forcing/atmospheric.html#creating-new-weights-files
* tool: /ocean/dlatorne/MEOPAR/NEMO-EastCoast/NEMO_Preparation/4_weights_ATMOS/get_weight_nemo 
* confirmed no repo updates since last build on 21mar22
* pushd /data/dlatorne/MEOPAR/grid/
* pulled changes from GitHub: Michael's ice_if PR
* created symlinks in grid/ required to run get_weight_nemo:
    ln -s namelist.get_weight_nemo.gem2.5-ops namelist
    ln -s /results/forcing/atmospheric/GEM2.5/operational/ops_y2017m01d01.nc atmos.nc
    ln -s /home/sallen/MEOPAR/grid/bathymetry_double_202206.nc bathy_meter.nc
* generated weights file:
    /ocean/dlatorne/MEOPAR/NEMO-EastCoast/NEMO_Preparation/4_weights_ATMOS/get_weight_nemo 
* improved weights file with tools/I_ForcingFiles/Atmos/ImproveWeightsFile.ipynb
* stored new, uncommitted weights file as grid/weights-gem2.5-ops_double_202206.nc
Email from arbutus support saying that fvcom3 VM was restarted due to a cloud hardware issue;
investigation:
* restart happened at 08:34 PDT
* confirmed reboot on VM and that it did not have /nemeShare/MEOPAR/ mounted
* no impact because fvcom3 is used for r12 run that hasn't started yet
* mounted /nemeShare/MEOPAR/
(SalishSeaCast)

Updated kudu from 21.10 to 22.04.

UBC-IOS modeling mtg: model evaluation discussion.

Continued work on info sub-command; learned how to use rich to style console output; PR#33.
Added test suite for dask cluster config YAML files; PR#33.
(Reshapr)


Fri 24-Jun-2022
^^^^^^^^^^^^^^^

Noticed that ERDDAP daily report emails stopped on 9-Mar; investigation:
* my email address was dlatorne@eos that didn't survive the move to FASMail; updated
* pulled change on skookum and restarted ERDDAP:
  sudo /opt/tomcat/bin/shutdown.sh
  wait for uptimerobot notification
  sudo /opt/tomcat/bin/startup.sh
(ERDDAP)

Continued work on info sub-command.
(Reshapr)


Sat 25-Jun-2022
^^^^^^^^^^^^^^^

Drove to White Rock to visit J&M.


Sun 26-Jun-2022
^^^^^^^^^^^^^^^

Goofed off.

Washed cycling shoes.


Week 26
-------

Mon 27-Jun-2022
^^^^^^^^^^^^^^^

Continued work on info sub-command.
(Reshapr)

Helped Susan prepare for double resolution experiment on sockeye:
* tested adding `--mca mpi_cuda_support 0` as mpirun option to suppress stderr
  messages re: CUDA unavailable libraries
* investigated run /scratch/st-sallen1-1/sallen1/DOUBLE_202111/tester71/
  * use `module load netcdf-fortran/4.4.5` to get ncdump
  * 1 core dump file (some other runs have 2 or 3)
  * msgs in stderr:
    * Error in `./nemo.exe`: corrupted size vs. prev_size: 0x00000000056de090 
        backtrace is mostly in libhdf5
    * Segmentation fault - invalid memory reference
        backtrace re: illegal attempt to fork in xios::CClient::finalize()
(DoubleRezSSC)

Group mtg.
(MOAD)

While debugging getting connected to sockeye from khawla as Susan,
learned about ProxyJump as clean alternative to ProxyCommand,
and `IdentitiesOnly yes` to avoid "too many auth errors" issue when I need to 
use a specific identity file.
Updated kahwla .ssh/config.


Tue 28-Jun-2022
^^^^^^^^^^^^^^^

Worked at ESB while Rita was at home.

Finished EGBC CE plan and submitted it.
Started adding CE activities for 1jan21 to 30jun22.


Wed 29-Jun-2022
^^^^^^^^^^^^^^^

FAL estate work: called TSX Trust re: DRS statement; rep thinks that back office made a mistake
in registration; should be me instead of me as estate executor; opened escallation request.

MOAD group coffee on zoom.

Finished adding CE activities for 1jan21 to 30jun22 to EGBC system.

Continued work on info sub-command; added model profile output.
(Reshapr)

Got outdated? dependabot alerts jupyter-server token bruteforcing; no PRs due to 
"jupyter-server no longer vulnerable"; weird.
Squash-merged dependabot PRs re: token brute-forcing CVE in notebook:
* SOG-Bloomcast-Ensemble
Squash-merged dependabot PRs re: numpy string comparisons
* analysis-doug/melanie-geotiff
Squash-merged dependabot re: both of above:
* SalishSeaTools
Updated sentry-sdk in prod env on skookum from 1.5.8 to 1.6.0; that triggered updates of
ca-certificates, certifi, libgcc-ng, libgomp, and openssl.
(SalishSeaCast)

Evaluated sphinx-hoverxref extension and discussed it w/ Susan; agreed that it is not 
what we want for links in general in our docs; maybe for API links in some cases.


Thu 30-Jun-2022
^^^^^^^^^^^^^^^

download_live_ocean was slow; after waiting 5h I found that liveocean.apl.uw.edu is not
ping-able; killed download_live_ocean and used yesterday's symlink-persisted for today
that was created early this morning for forecast2; unblocked automation:
  upload_forcing arbutus nowcast+
  upload_forcing orcinus nowcast+
  upload_forcing optimum nowcast+
  upload_forcing graham-dtn nowcast+
graham came back online after maintenance; backfilled upload_forcing:
  for dd in {23..29}; do upload_forcing graham-dtn nowcast+ 2022-06-${dd}; done
  for dd in {23..29}; do upload_forcing graham-dtn turbidity 2022-06-${dd}; done
(SalishSeaCast)

Sent Slack DM to Tereza asking for here paper citations and 1-liners to add to 
publications page, etc.

Continued work on info sub-command; added output of list of variables in
time-base/var-group.
(Reshapr)

Phys Ocgy seminar: Mathilde Jutras, McGill; Unsupervised clustering of Lagrangian tranjectories in Labradour Sea
* OceanParcels in GLORYS12 re-analysis
* K-means from Scikit-learn


July
====


Fri 1-Jul-2022
^^^^^^^^^^^^^^

sockeye changed to new default environment making many of the modules we were using
unavailable; see #sockeye channel
Got VSCode remote dev env to run on sockeye.
My work env on sockeye was so old that the repos were hg clone; updated:
* added aliases to .bashrc
* added default, always needed module loads to .bashrc
    module load gcc/9.4.0
    module load git/2.31.1
* **NOTE:** sockeye philosophy seems to be that all module loads should be explicit;
  i.e. `module load git` doesn't implicitly load the gcc dependency, nor default to 
  the version
* made symlinks in $HOME for $PROJECT and $SCRATCH to avoid annoying \ prefix when I tab-complete
    ln -s $PROJECT project
    ln -s $SCRATCH scratch
* Cloned repos into ~/project/
* Worked on building XIOS:
  * updated module loads in arch-GCC_SOCKEYE.env:
    * 1st attempt:
        module load gcc/9.4.0
        module load openmpi/4.1.1-cuda11-3
        module load netcdf-fortran/4.5.3-hdf4-support
        module load netcdf-cxx/4.2-hdf4-support
        module load perl/5.34.0
        module load perl-uri/1.72
  * 1st build attempt failed due to unable to find netcdf.H
  * used `nc-config --cflags` to get ridiculous collection of paths and assigned them to 
    NETCDF_INCDIR in arch-GCC_SOCKEYE.path
  * 2nd build attempt failed at final mpif90 link step due to not finding 
    -lnetcdf, -lnetcdff, -lhdf5_hl, -lhdf5_hl
  * used `nc-config -flibs` to get netcdf-fortran lib/ path and prefix it as `-L` to 
    NETCDF_LIB in arch-GCC_SOCKEYE.path
  * 3rd build attempt failed at final mpif90 link step due to not finding 
    -lnetcdf, -lhdf5_hl, -lhdf5_hl
  * used `nc-config -libs` to get netcdf-c lib/ path and prefix it as `-L` to 
    NETCDF_LIB in arch-GCC_SOCKEYE.path
  * 4th build attempt failed at final mpif90 link step due to not finding 
    -lhdf5_hl, -lhdf5_hl
  * dug around in /arc/software/spack-2021/spack/opt/spack/linux-centos7-skylake_avx512/gcc-9.4.0/
    to find hdf5 lib/ path to prefix as `-L` to HDF5_LIB in arch-GCC_SOCKEYE.path
  * 5th build attempt succeeded
  * found envvars that contain root paths from `nc-config` and one for HDF5;
    changed arch-GCC_SOCKEYE.path to use them
  * clean and 6th build attempt succeedded
* Worked on building NEMO:
  * 1st build attempt failed due to unable to find all includes and libs
  * added to arch-GCC_SOCKEYE.fcm
      %NCDF_HOME  $NETCDF_FORTRAN_ROOT
  * changed %NCDF_INC to
      %NCDF_INC  -I%NCDF_HOME/include
  * 2nd attempt failed due to unable to find libs
    * changed %NCDF_LIB to 
        %NCDF_LIB  -L%NCDF_HOME/lib -lnetcdff -lnetcdf
  * clean and 3rd build attempt failed due to not finding -lnetcdf
    * changed %NCDF_LIB to 
        %NCDF_LIB  -L%NCDF_HOME/lib -L$NETCDF_C_ROOT/lib -lnetcdff -lnetcdf
  * 4th build attempt succeedded
* successful build of REBUILD_NEMO
* Susan symlinked executables to run test
* Uncommitted changes in:
    NEMO-3.6-CODE/NEMOGCM/ARCH/UBC_EOAS/arch-GCC_SOCKEYE.fcm
    XIOS-ARCH/UBC-ARC/arch-GCC_SOCKEYE.env
    XIOS-ARCH/UBC-ARC/arch-GCC_SOCKEYE.path
(DoubleRezSSC)

Changed module loads for sockeye re: new env; sockeye-2022-env branch; uncommitted
(SalishSeaCmd)


Sat 2-Jul-2022
^^^^^^^^^^^^^^

Drove to Wite Rock to visit J&M.
Picked Max up at YVR.


Sun 3-Jul-2022
^^^^^^^^^^^^^^

Susan & Max picked Jingli up at YVR, and Sylvia up at ferry.

Susan's test jobs from Fri failed:
  Cgroup mem limit exceeded: Task in /pbspro.service/jobid/3840994.pbsha.ib.sockeye killed as a result of limit of /pbspro.service/jobid/3840994.pbsha.ib.sockeye
* built a full working env on sockeye in /project/st-sallen1-1/dlatorne/MEOPAR/
  * modules required to install NEMO-Cmd and SalishSeaCmd:
      module load python/3.8.10 
      module load py-setuptools/50.3.2 
      module load py-pip/21.1.2
      module load py-wheel/0.36.2
  * had to hack ~/.local/bin/nemo and ~/.local/bin/salishsea to change she-bang to 
      #!/bin/env python3
    perhaps because 
      #!/arc/software/spack-2021/spack/opt/spack/linux-centos7-skylake_avx512/gcc-9.4.0/python-3.8.10-gdthw5ahkql24mqrkzq4x6bnkwlvx537/bin/python3
    from install it too long?
* re-tried /scratch/st-sallen1-1/sallen1/test_new_gcc_small3/SalishSeaNEMO.sh
  from /home/dlatorne/project/dlatorne/MEOPAR/runs/01jan07_sockeye.yaml 
  with node request bumped from 3 to 4
* re-tried /home/dlatorne/project/dlatorne/MEOPAR/runs/01jan07_sockeye.yaml 
  with 3 nodes and 186gb of memory
* sockeye docs suggest that it is possible to get a mixture of node memory sizes:
    #PBS -l walltime=100:00:00,select=1:ncpus=16:mpiprocs=16:mem=200gb+1:ncpus=20:mpiprocs=20:mem=20gb
* Read about -mcpu option in gcc-9.
* Investigated sockeye modules for Intel-2021 compilters.
(DoubleRezSSC)


Week 27
-------

Mon 4-Jul-2022
^^^^^^^^^^^^^^

Max & Jingli visiting.
Drove to White Rock to visit J&M

Tried builds w/ gcc-5.5.0, if nothing else, just to get something working as a baseline:
Module loads:
  module load gcc/5.5.0
  module load openmpi/4.1.1-cuda11-3
  module load netcdf-fortran/4.5.3-hdf4-support
  module load netcdf-cxx/4.2-hdf4-support
  module load perl/5.34.0
  module load perl-uri/1.72
i.e. only change is gcc version
Got ocean.output until errors re: init conditions and turbulence, but no time steps.
Susan helped me fix namelist.time to resolve errors above; new test; got time steps.
Explored gcc-7.5.0, but discovered that there are no netcdf libs for it.
Updated SalishSeaCmd to new sockeye module loads and memory request; PR #17.
Updated XIOS-ARCH to new sockeye module loads; no PR.
(DoubleRezSSC)


Tue 5-Jul-2022
^^^^^^^^^^^^^^

Max & Jingli visiting.
Drove to White Rock to visit J&M

Updated NEMO arch for sockeye w/ new envvars; no PR.
Explored -march compiler option for gcc-5.5: no Skylake or Cascade Lake.
Explored Intel 2021.4.0 compilers; no setuptools module.
(DoubleRezSSC)

uptimerobot reported that salishsea-site is down: investigation:
* Henryk rebooted salish to fix its ocean mounts, but that messed up its NFS exports;
* exportfs -f on salish refused to work saying:
    exportfs: -f is available only with new cache controls. Mount /proc/fs/nfsd first
  and I don't know what that means.
* Decided to update and reboot skookum:
    sudo apt update
    # reviewed 34 pkgs to be updated
    sudo apt upgrade
    # reported lots of Linux old kernels that can be auto-remove-ed
* skookum didn't get mounts from salish after reboot
* ran download_weather processes in debug mode on salish
    download_weather 18 2.5km
    download_weather 12 1km
    download_weather 00 1km --yesterday  # due to after 17:00
* Henryk says that salish lost NFS config sure to root fs ssd problems; restored from backup;
  ssds need replacement; mounts to skookum and workstations restored
* recovery:
  * start ERDDAP
      sudo /opt/tomcat/bin/startup.sh
  * start salishsea-site app
  * start automation
      collect_weather 2.5km 
      download_results arbutus forecast
      make_turbidity_file  # to start nowcast-green and nowcast-agrif
      launch_remote_worker arbutus make_fvcom_boundary "arbutus x2 nowcast"
(SalishSeaCast)

Started work on adding --core-pre-node and --cpu-arch options and removing --cedar-broadwell.
(SalishSeaCmd)


Wed 6-Jul-2022
^^^^^^^^^^^^^^

EGBC notified me that my CE reporting was overdue to 30jun2022; I objected by email.

Susan, Max & Jingli went ot White Rock to visit J&M
Jingli went to Victoria later.

Susan noticed that ssh connections to salish are now instant rather than ~30s delay as formerly
and on skookum.

FAL estate work:
* Jocinda from TSX Trust called to discuss DRS statement registration issue;
  she will escallate to back office and follow-up in 1 wk.

Power failure in ESB resulted in name resolution failures and manager restart just after 10:00;
automation stopped w/ forecast run completed but not downloaded, and x2 nowcast running; 
recovery started at ~12:00:
  download_results arbutus forecast
  make_turbidity_file  # to start nowcast-green and nowcast-agrif
(SalishSeaCast)

Found 1.19 community ports of Masa mods at https://kosma.pl/masamods/
Downloaded:
  malilib-fabric-1.19-0.12.1.jar
  minihud-fabric-1.19-0.22.0.jar
Downloaded ComplementaryShaders_v4.5.1.zip
Downloaded:
  lithium-fabric-mc1.19-0.8.0.jar
  phosphor-fabric-mc1.19.x-0.8.1.jar
Installed all of the above in client and tested successfully in single player and on server.
Uploaded lithium and phosphor to nodecraft server, restarted it, and tested it successfully.

Squash-merged dependabot PRs re: ujson:
  UBC-MOAD/docs
  SalishSeaCast/docs
Squash-merged dependabot PRs re: lxml:
  SalishSeaCast/SalishSeaNowcast
  SalishSeaCast/tools
(MOAD)

Copntinued work on adding --core-pre-node and --cpu-arch options and removing --cedar-broadwell;
PR #18.
(SalishSeaCmd)


Thu 7-Jul-2022
^^^^^^^^^^^^^^

Copntinued work on adding --core-pre-node and --cpu-arch options and removing --cedar-broadwell;
PR #18.
(SalishSeaCmd)

watch_NEMO messages were not being logged; resolved by restarting log_aggregator.
(SalishSeaCast)

Drove to White Rock to visit J&M.


Fri 8-Jul-2022
^^^^^^^^^^^^^^

collect_weather 06 did not complete; investigation:
* 575 of 576 files downloaded; missing 1 file from hour 047:
    CMC_hrdps_west_DSWRF_SFC_0_ps2.5km_2022070806_P047-00.grib2
* no problem messages in log
* missing file is not present on dd or hpfx
* recovery started at ~08:55:
    created symlink to persist 046 as 047
    collect_river_data
    get_onc_ctd
    skipped get_onc_ferry
    collect_HeanBay_ssh 00
    grib_to_netcdf forecast2 --debug
    skipped forecast2 runs
    download_weather 12 2.5km
    collect_weather 18 2.5km &
During recoery noticed that San Juan River at Port Renfrew data stream resumed on 23-Jun
(SalishSeaCast)

Susan & Max went ot White Rock to visit J&M.

Searched for image to go with AGU feature about Saurav's paper.

FAL estate work:
* Sheena from TSX trust called; investigation shows that DRS statement was issued as it is
  because there was no secutiries transfer form; she sent me the form and explained how to 
  complete it; it needs a signature guarantee stamp from TD.
* Email to Andres@TD re: how to get signature guarantee stamp

Advised Raisha on segfault due to malloc() invalid size.
(Atlantis)

Finished adding --core-pre-node and --cpu-arch options and removing --cedar-broadwell;
merged  PR #18.
Tagged and released v22.2; bumped version to 22.3.dev0.
(SalishSeaCmd)

Code base maintenance:
* CodeQL Action v1 will be deprecated on December 7th, 2022. Please upgrade to v2. 
  For more information, see 
  https://github.blog/changelog/2022-04-27-code-scanning-deprecation-of-codeql-action-v1/
  * Updated workflows:
    * SalishSeaCast/SalishSeaCmd
    * SalishSeaCast/SalishSeaNowcast
    * UBC-MOAD/Reshapr
    * MIDOSS/MOHID-Cmd
    * SS-Atlantis/AtlantisCmd
  * Already at v2:
    * SalishSeaCast/NEMO-Cmd
    * UBC-MOAD/moad_tols
* SalishSeaCast/docs
  * Change to Python 3.10; PR#6; its a mess because I forgot to pull main first; squash-merged
    * chg build env to Python 3.10
    * update pkgs & versions used in revent dev env
    * change to 3.10 in GHA linkcheck workflow
  * Improve GHA workflows; PR#7 merged
    * change to run GHA workflows on push to any branch
    * drop pkg caching from GHA linkcheck & CI workflows
    * chg GHA linkcheck & CI workflows to use mambaforge


Sat 9-Jul-2022
^^^^^^^^^^^^^^

Susan & Max went ot White Rock to visit J&M.

Cycled 8th Ave, Chancellor, UBC, SWM, Ridgeway, Arbutus Greenay loop on Gunnar.
(22 km)


Sun 10-Jul-2022
^^^^^^^^^^^^^^^

Max went to White Rock to stay w/ J&M for a few days.

Discussed standard_name attr values for PAR w/ Susan; our ERDDAP presently uses
  downwelling_photosynthetic_photon_radiance_in_sea_water
but that had units of Einsteins' (mol/m2/s) according to CF Standard Name Table;
agreed that 
  downwelling_photosynthetic_radiative_flux_in_sea_water
which had units of W/m2 is better.
Added PAR standard_name to 
  SS-run-sets/v201905/field_def.xml
  SS-run-sets/v202111/field_def.xml
Pulled SS-run-set change on skookum for nowcast-dev (though it is not output there).
Forgot that arbutus us on local branch at 656d78d; need to think about how to get new
field_def.xml there.
(SalishSeaCast)

Changed PAR standard_name value in ubcSSg3DAuxiliaryFields1hV19-05 in erddap-dataset;
touched dataset in erddap/flags to make update take effect
(ERDDAP)


Week 28
-------

Mon 11-Jul-2022
^^^^^^^^^^^^^^^

pre-commit re: v2.20.0 released; used cs.github.com to locate 7 repos where I use it:
  org:SalishSeaCast OR org:UBC-MOAD OR org:MIDOSS OR org:SS-Atlantis OR org:43ravens path:**/.pre-commit-config.yaml  
    SS-Atlantis/AtlantisCmd
    SalishSeaCast/SalishSeaNowcast
    UBC-MOAD/MoaceanParcels
    UBC-MOAD/docs
    UBC-MOAD/cookiecutter-MOAD-pypkg (2 places)

Participated in Susan/Raisha mtg re: debugging segfault.
AtlantisCmd maintenance:
* updated pre-commit re: v2.20.0 release
* updated dev env on khawla
* updated redirected PEP-8 link in docs
(Atlantis)

Maintenance:
* updated pre-commit re: v2.20.0 release
* updated dev env on khawla
* fixed warning re: language setting in Sphinx config
(SalishSeaNowcast)

Maintenance in un-merged PR#3:
* updated pre-commit re: v2.20.0 release
* updated dev env on khawla
* updated redirected PEP-8 link in docs
Merged PR#3.
(MoaceanParcels)

Maintenance:
* updated pre-commit re: v2.20.0 release
* updated dev env on khawla
* fixed warning re: language setting in Sphinx config
* updated redirected PEP-8 link in docs
(MOAD docs)

Maintenance:
* updated pre-commit re: v2.20.0 release
* updated dev env on khawla
(cookiecutter-MOAD-pypkg)

Continued work on standard_name attrs in v201905 and v202111:
* successfully tested `reshapr extract` on ncatted-modified SalishSea_1d_20070101_20070101_carp_T.nc
* worked out bash command to run in tmux to do bulk ncatted:
    time_base=h; 
    yyyy=2007; 
    yy=$(date --date="${yyyy}-01-01" +%y); 
    for mm in {01..12}; 
    do 
      mmm=$(date --date="${yyyy}-${mm}-01" +%b | tr '[:upper:]' '[:lower:]'); 
      for dd in {01..31}; 
      do 
        yyyymmdd=${yyyy}${mm}${dd}; 
        fn=${dd}${mmm}${yy}/SalishSea_1${time_base}_${yyyymmdd}_${yyyymmdd}_carp_T.nc; 
        echo ${fn}; 
        ncatted -O -h -a standard_name,PAR,c,c,downwelling_photosynthetic_radiative_flux_in_sea_water ${fn} ${fn}; 
      done; 
    done
  see: /results2/SalishSea/nowcast-green.201905/add_std_name.sh
* successfully tested month-average resampling of 2007-jan auxiliary (carp_T) files
  in /results2/SalishSea/month-avg.201905/
* Ran bash loop to produce 201905 re-run month-averaged physics & biology files for jun22
on a 4 worker x 4 threads stand-alone cluster in tmux on salish
in /results2/SalishSea/month-avg.201905/:
* ran bash loops to add PAR standard_name to v201905 
  (/results2/SalishSea/nowcast-green.201905/add_std_name.sh):
  * 2007 1d & 1h
  * 2008 1d & 1h
  * 2009 1d & 1h
  * 2010 1d & 1h
  * 2011 1d & 1h
  * 2012 1d & 1h
  * 2013 1d & 1h
  * 2014 1d & 1h
  * 2015 1d & 1h
  * 2016 1d & 1h
  * 2017 1d & 1h
  * 2018 1d & 1h
  * 2019 1d & 1h
  * 2020 1d & 1h
  * 2021 1d & 1h
  * 2022 1d & 1h to 11jul22
Ran bash loop to produce 201905 month-averaged aux/chemistry files
on a 4 worker x 4 threads stand-alone cluster in tmux on salish
in /results2/SalishSea/month-avg.201905/:
  2007
  2008
  2009
  2010
  2011
  2012
  2013
  2014
  2015
Cherry-picked commit that adds standard_name to PAR into production branch on arbutus:
  git cherry-pick --no-commit 531ec571435b
(SalishSeaCast)


Tue 12-Jul-2022
^^^^^^^^^^^^^^^

Worked at ESB while Rita was at home.

Confirmed that production nowcast-green carp_T files have standard_name for PAR now.
Committed cherry-picked commit re: PAR standard_name on PROD branch on arbutus to silence
log warnings about uncommitted changes in SS-run-sets.
Continued running bash loop to produce 201905 month-averaged aux/chemistry files
on a 4 worker x 4 threads stand-alone cluster in tmux on salish
in /results2/SalishSea/month-avg.201905/:\
  2016
  2017
  2018
  2019
  2020
Confirmed that monthly tarball transfer to graham:/nearline/ happened via automation for jun22.
r12 nowcast finished too early; investigation:
* fvcom executable not found on fvcom3
* fvcom3 does not have /nemoShare/MEOPAR/ mounted
* fvcom3 rebooted at 15:30 UTC == 08:30 PDT
* recovery started at ~13:00:
    * fvcom3:
        sudo mount -t nfs -o proto=tcp,port=2049 192.168.238.14:/MEOPAR /nemoShare/MEOPAR
    * skookum:
        launch_remote_worker arbutus make_fvcom_boundary "arbutus r12 nowcast"
(SalishSeaCast)

Created sockeye-dbl-rez branch to adjust PBS directives for next week's double resolution
runs on sockeye:
* added `#PBS -q R3896244`
(SalishSeaCmd)

Did year roll-over and other code maint on salishsea-site pkg;
used NEMO-Cmd repo for guidance.
* PR#17; merged and deployed manually:
  * bump version to 22.1.dev0
  * change copyright year range to end with `– present`
  * add SPDX short-form license identifiers
(salishsea-site)

Helped Susan set up conda env for DFO model analysis pkg.


Wed 13-Jul-2022
^^^^^^^^^^^^^^^

MOAD coffee zoom.

Drove to White Rock to visit J&M.
Dropped Max at YVR.

sarracenia clients for HRDPS and hydrometric obs got stuck with multiple connection refused
and ssl protocol errors starting at ~05:30:
* killed collect_weather 2.5km 12
* restarted sarracenia clients
* rmdir forcing dir
* download_weather 2.5km 12
* collect_weather 2.5km 18
hydrometric obs still not working due to connection errors; stopped, waited minutes, started;
checked at 13:30: still not working; restarted: still not working; checked files on dd.weather.gc.ca
and found no updates in Fraser or Englishman csvs since 06:10; concluded that the problem in
server-side.
Finished running bash loop to produce 201905 month-averaged aux/chemistry files
on a 4 worker x 4 threads stand-alone cluster in tmux on salish
in /results2/SalishSea/month-avg.201905/:
  2021
  2022 jan-jun
Name resolution failures when make_plots for x2 nowcast tried to connect to api-iwls.dfo-mpo.gc.ca;
also HRDPS sarracenia client starting at ~14:00;
pinged EOAS IT slack; power outage in EOS-Main and South.
Restarted sarracenia clients after power restored; still erroring out.
Manual HRDPS downloads for 2.5km 18 and 1 km 00 & 12 started at ~16:00.
Manual HRDPS download for 2.5km 00.
(SalishSeaCast)


Thu 14-Jul-2022
^^^^^^^^^^^^^^^

Manual HRDPS download for 2.5km 06 at ~08:45.
Started collect_weather 18.
Still getting errors in sarracenia logs; stopped clients at 08:45; restarted them at 09:30;
started to write email to Sandrine, then noticed that hydrometric obs were coming in; no publihser errors from HRDPS client either.
Manual HRDPS download for 2.5km 12 at ~10:10
nowcast-agrif got stuck at 46% due to node/infiniband failure; probably fallout from yesterday's powere bump induced crash; killed and restarted via `upload_forcing turbidity`
(SalishSeaCast)

Fixed GHA deployment workflow, apparently by just updating repo DEPLOY_KEY secret to 
contents of SalishSeaNEMO-nowcast_id_rsa (which is what I believe it previous was); I tried
updating it to several other inappropriate keys along the way though, so maybe just "refreshing"
the key did the trick? This might also be a manifestation of the `PubkeyAcceptedKeyTypes=+ssh-rsa`
thing that I had to do for orcinus and optimum, but I'm less convinced.
Continued code maint on salishsea-site pkg;
used NEMO-Cmd repo for guidance.
* improved GHA workflows; forgot to create branch:
  * change to run GHA workflows on push to any branch
  * drop pkg caching from GHA workflows
  * change GHA workflows to use mambaforge
  * add name to Slack channel notification step
* PR#18:
  * Add GHA CodeQL scanning workflow
  * Add CodeQL analysis badges to README & pkg dev docs
* PR#19:
  * Change to Python 3.10 for pkg dev & deployment
  * Change rtd Python built tool to mambaforge-4.10
  * Rename readthedocs.yml to .readthedocs.yaml
  * Move requirements.txt to envs/
  * Update pkgs & versions used in recent dev env
  * Move entry points from setup.py to setup.cfg
  * Drop setup.py and add pyproject.toml
  * Move coverage.py config to pyproject.toml
  * Explicitly exclude use of conda defaults channel
Cleaned up stale remote branches.
(salishsea-site)


Fri 15-Jul-2022
^^^^^^^^^^^^^^^

FAL estate work:
* prepared securities transfer form for BCE shares, took it to appt at TD w/ Sahi
  for signature guarantee stamp, and UPS-ed it with tracking & receipt signature

Updated mamba and conda in khawla base env:
  mamba update -n base mamba
  mamba update -n base conda
mamba brought updates to the ususal collection of foundational pkgs with it:
ca-certificates, certifi, openssl and their deps

Explored the idea of using functools.partial() or .partialmethod() to reduce code duplication
in Susan's results comparison figures code; no obviously simple way to 
partial xarray.Dataset.plot() :-(

Subscribed to dd_info email list w/ dlatornell@eoas address because old sub was dlatorne@eos, I think.

ONC SoG nodes down.

Discovered at ~20:00 that nowcast-x2 run was stalled; investigation:
* fvcom0 was non-responsive w/ messages about stuck fvcom process in its log
* recovery:
  * hard reboot fvcom0 from dashboard
  * mount /nemoShare/MEOPAR
  * launch_remote_worker arbutus make_fvcom_boundary "arbutus r12 nowcast"
nowcast-r12 failed on luanch
(SalishSeaCast)


Sat 16-Jul-2022
^^^^^^^^^^^^^^^

Investigated nowcast-r12/15jul22 failure:
* no restart; 14jul22 run stopped at about 75%
* recovery:
    wait for 16jul22 run to fail
    launch_remote_worker arbutus make_fvcom_boundary "arbutus r12 nowcast 2022-07-14"
    launch_remote_worker arbutus make_fvcom_boundary "arbutus r12 nowcast 2022-07-15"
(SalishSeaCast)


Sun 17-Jul-2022
^^^^^^^^^^^^^^^

Backfill nowcast-r12:
    wait for 17jul22 run to fail
    launch_remote_worker arbutus make_fvcom_boundary "arbutus r12 nowcast 2022-07-16"
    launch_remote_worker arbutus make_fvcom_boundary "arbutus r12 nowcast 2022-07-17"
(SalishSeaCast)


Week 29
-------

Mon 18-Jul-2022
^^^^^^^^^^^^^^^

Cancelled my paper presentation for tomorrow; not ready; paper/pkg I was thinking about:
  A New Open Source Implementation of Lagrangian Filtering: 
  A Method to Identify Internal Waves in High-Resolution Simulations
  Shakespeare, VJ, AH Gibson, AM Hogg, SD Bachman, SR Keating, N Velzeboer (2021), 
  Journal of Advances in Modeling Earth Systems, 13, e2021MS002616
  https://doi.org/10.1134/S1560354721050063

  Code is at https://github.com/angus-g/lagrangian-filtering and 
  docs at https://lagrangian-filtering.readthedocs.io/en/latest/
(OceanParcels)

Worked on performance review.

Double resolution run on sockeye
Checked storage: /result & /opp are 98% full; 377G & 471G free, respectively.
Helped Susan w/ double resolution run on sockeye.
(SalishSeaCast)

MOAD group mtg.
(MOAD)


Tue 19-Jul-2022
^^^^^^^^^^^^^^^

Tried to run 5-yr average biology extraction for Karyn on khawla; lots of memoery use warnings;
worked better on salish.

Answered Becca's question about single point extraction for carbon/oxygen with suggestion to
use Reshapr.

Found bug re: missing default values for CLI start-date/end-date options; issue #34
(Reshapr)

Finished performance review for and passed to Susan.


Wed 20-Jul-2022
^^^^^^^^^^^^^^^

Slack w/ Karyn & Becca re: Reshapr extractions.
* Karyn's 5-yr average produced 2 time coordinate values, neither correct
* Becca's all-of-201905 produced large chunk warnings due to slice, and failed
  w/ KeyError on standard_name lookup

MOAD coffee.

Continued work on test_vars_list re: PR#33.
(Reshapr)

Walked to Rain or Shine for sundaes in afternoon heat.


Thu 21-Jul-2022
^^^^^^^^^^^^^^^

Finished work on test_vars_list; merged PR#33.
Resolved issue #34 re: default values for --start-date and --end-date; merged PR#35.
Fixed some extraneous highlighting in `info` output; merged PR#36.
Created issue #37 re: `reshapr extract` raises KeyError on y coordinate if variable requested is 
not in specified variable group.
Created issue #38 re: semantics of single point extractions and max+1 re: Becca's use case this 
week.
(Reshapr)

Email from arbutus support; fvcom3 failed due to temperature; VM was migrated to a different
hypervisor; mounted shared storage; r12 run failed to start:
* host key changed
* SalishSeaNEMO-nowcast key (id_rsa on nowcast0) missing from authorized_keys on fvcom3
* restored key to fvcom3
* cleaned up 
* re-luanched r12 at ~13:15
(SalishSeaCast)

Phys Ocgy seminar: Christopher Peck, U Manitoba, La Grande River plume (east coast of James Bay)


Fri 22-Jul-2022
^^^^^^^^^^^^^^^

Cycled to ESB via Kerrisdale and Pacific Spirit trails.

Performance review mtg w/ Philippe.

Started alpine base in Minecraft 1_18-1 world.


Sat 23-Jul-2022
^^^^^^^^^^^^^^^

Planned power outage in EOS-Maind and -South.

collect_weather 12 still waiting for files at 10:15; investigation:
* name resolution failures
* recovery:
    kill collect_weather 12 2.5km
    collect_weather 18 2.5km
    wait for power to come back on at 11:00
    download_weather 12 2.5km
(SalishSeaCast)

Walked in Pacific Spirit Park; Nature, Swordfern & Hucleberry trails.
(~2.5 hr)


Sun 24-Jul-2022
^^^^^^^^^^^^^^^

Cycled Iona loop on Gunnars
(40 km)

nowacst-agrif stuck on launch; lots of TCP failure messages from compute nodes;
killed job; killed watcher; re-submitted job; confirmed that it was time stepping; 
launched new watcher.
ww3 nowcast stuck on launch; discovered that nowcast2 was non-responsive; hard reboot from web 
dashboard, then re-mount shared storage; use launch_remote_worker on skookum to re-run 
make_ww3_wind_file and make_ww3_current_file to restart automation
(SalishSeaCast)


Week 30
-------

Mon 25-Jul-2022
^^^^^^^^^^^^^^^

Updated PyCharm on khawla to 2022.1.4.

Worked on weird time coordinate values in year-average extractions (Karyn's 5-yr average use case):
* ran 1 year; has expected time coordinate value: 2015-07-01 12
* ran 2 years for just nitrate; way faster; has 2 time coordinate values and they are weird:
  "2014-12-31 12", "2016-12-30 12"
* ran 2 years for just nitrate w/ label="left" and loffset commented out; 
  has 2 time coordinate values and they are weird: "2015-12-31", "2017-12-31"
* ran 2 years for just nitrate w/ label="left" and loffset commented out and time interval A 
  instead of 2A; 
  has 2 time coordinate values that make sense: "2015-12-31", "2016-12-31"
* restored label="left" and loffset
* ran 2 years for just nitrate and time interval 731D instead of 2A; 
  has 1 time coordinate value that makes sense: "2016-01-01 12:00:00"
* 2015-2017 and 2016-2018 w/ 24M time interval; 2 time coordinate values
* ran 5 years for just nitrate and time interval 1826D (4 * 365 + 366); 
  has 1 time coordinate value that makes sense: "2017-07-02 00:00:00"
* ran 5 years for all variables; success!! 8095s = 2.25h
Created PR#39 re: docs improvements:
* pulled YAML out of Atlantis diatoms use case blurb file into separate file so that I can run it
Ran Atlantis day-avg diatoms extration for jan07 with deflation for Raisha to test; 244M vs. 1.7G.
Reviewed late-2020 pkgs & envs presentation notebook in 
https://github.com/UBC-MOAD/PythonNotes/tree/master/pkgs-envs
re: planning for Reshapr workshop.
Started dev of slides notebook for Reshapr Intro workshop in branch in 
UBC-MOAD/PythonNotes/reshapr-intro/.
(Reshapr)

Reviewed late-2020 pkgs & envs presentation notebook in 
https://github.com/UBC-MOAD/PythonNotes/tree/master/pkgs-envs
re: planning for Reshapr workshop.

MOAD group mtg.
(MOAD)

Beginning of heat wave


Tue 26-Jul-2022
^^^^^^^^^^^^^^^

Hotter than yesterday.

Worked at ESB while Rita was at home.

collect_weather 12 didn't finish:
* connection refused msgs in log; also "broker forced connection closure" and queue declaration
  failures for both hrdps and hydrometric; so, probably publisher issue
  * 499 of 576 files downloaded
  * recovery started at ~11:00
      kill collect_weather 12
      collect_weather 18 2.5km
      download_weather 12 2.5km
* upload_forcing to orcinus failed due to connection timeout
(SalishSeaCast)

Started work on metadata cleanup for 201905 dia2_T files (grazing & mortality) in Slack direct msg 
w/ Susan & Karyn.
(SS-run-sets)

Attended Ben's Ph.D. defense and the subsequent pub outing to Keorner's patio.


Wed 27-Jul-2022
^^^^^^^^^^^^^^^

Hottest day yet.

Took a van-load of bikes and parts to OCB; Vitali, red Marinoni, On-Ones, Rock hoppers, and
MEC commuter that was stolen & returned; also saddles, platform pdeals, and Avid disk brake pads.

nowcast-agrif failed due to no restart because yesterday's run didn't happen; yesterday's outage was due to network address change maintenance; recovery:
  upload_forcing orcinus nowcast+ --run-date 2022-07-26
    failed with:
      paramiko.ssh_exception.SSHException: encountered RSA key, expected OPENSSH key
    seems like a flaky login node; Mark confirmed maintenance
  upload_forcing orcinus turbidity --run-date 2022-07-26
  wait for 26jul22 run to complete
  watch_NEMO_agrif failed due to connection issue; try again tomorrow
collect_weather 18 was atter 17:00; ran download_weather 00 1km --yesterday; accidentally deleted
26jul22 1km downloads
(SalishSeaCast)

Slept on the airbed in the tent on the patio.


Thu 28-Jul-2022
^^^^^^^^^^^^^^^

collect_weather 12 slow:
  132 of 576 by 08:15 then pause...
  276 of 576 by 10:15 then pause...
  finished at 11:27
NEMO forecast got stuck at 84.7%:
  errors in ocean.output:
      ===>>> : E R R O R
             ===========

            iom_get_123d, file: ./NEMO-atmos/ops_y2022m07d30.nc, var: atmpres
          start and count too big regarding to the size of the data, 
          (istart(3) + icnt(3) - 1) =     8 
          is larger than idimsz(3) =     7 
  killed watcher
  make_turbidity_file  # resume automation to start nowcast-green and nowacst-agrif
Backfill nowacst-agrif:
  download_results nowcast-agrif 2022-07-26
  wait for run to fail
  upload_forcing orcinus nowcast+ --run-date 2022-07-27
  upload_forcing orcinus turbidity --run-date 2022-07-27
  make_forcing_links orcinus nowcast-agrif 2022-07-28
make_ww3_current_file failed in preparation for WWatch3 nowcast run;
recovery:
  grib_to_netcdf nowcast_ --debug
  upload_forcing nowcast+ --debug
  make_forcing_links nowcast+ --debug
  make_forcing_links ssh --debug
  run_NEMO arbutus.cloud-nowcast forecast --debug  # on arbutus
  wait for run to finish
  download_results arbutus forecast
  make_ww3_wind_file arbutus forecast
  make_ww3_current_file arbutus forecast
(SalishSeaCast)

Phys Ocgy seminar: Shilliang (Dan) Shan, RMC, wind driven upwelling on the Scotia Shelf

Continued work on metadata cleanup for 201905 dia2_T files (grazing & mortality) in Slack direct 
msg w/ Susan & Karyn.
Started on prod_T files (biology & chemistry rates).
(SS-run-sets)


Fri 29-Jul-2022
^^^^^^^^^^^^^^^

PyCharm webinar: I Can't Believe It's Not Real Data! An Introduction into Synthetic Data,
Mason Egger, Developer Advocate at Gretel.ai, @masonegger
* Jodie Burchell, host
* Gretel.ai generates synthetic data as a service
* gretelai on GitHub
* models that generate synthetic data; blog
* GPT3: text data generation
* Lumina syth genomic data
* access to relevant data for testing/training bocked by personal privacy regulations (PII)
* 35% of time spent in data gathering stage
* synth data generated from real initial data; how, given PII???
* benefits:
  * making private data accessible & sharable
    * statistical similarity
  * augment small datasets
    * but bad small data generates bad big data
    * public section issue due to inaccessible formats like PDFs
  * reduce bias in data sets
    * identify bias in data; use synth data to balance
    * https://gretel.ai/blog/reducing-ai-bias-with-synthetic-data
* time series data gen using DoppelGANger (open source)
* challenges:
  * highly dimensional data is compute-intensive
  * relational dataset require manual config
  * privacy preservation requires logs of real data to operate on to provide strong security
  * not that fast
* uses
  * robotics training
  * financial Services
  * cybersecurity
  * healthcare
  * manufacturing & supply chain
* getel.ai is all open-source; GPUs required; kubernetes; free tier; Python & Rust APIs
* differential privacy: add noise to obs that is proportional to variable in real data
* Jupyter notebook demo:
  * greta-client pkg
    * API access key, OAuth
  * dispatches job to gretel cloud
* TPU == Tensor Processing Unit (Google GPU)
* docs.gretel.ai
* gretelai/gretel-blueprints
* mason.dev

Discussed storage of hindcast spin-up products w/ Susan; agreed on storage on optimum
(where pressure to delete is low and products are most likely to be reused in case of disaster),
/ocean (to avoid collocation w/ production products on /results*, /data, /opp),
and graham:nearline/

Reviewed storage pressure:
  ~$ df -h /data /opp /results /results2
  Filesystem        Size  Used Avail Use% Mounted on
  /dev/sdb1          37T   33T  2.3T  94% /data
  /dev/sdc1          19T   17T  440G  98% /opp
  skookum:/results   19T   17T  217G  99% /results
  /dev/sdd1          89T   42T   43T  50% /results2
* /opp/
  * confirmed that all of /opp/GEMLAM/ is preserved on graham:nearline/
  * deleted /opp/GEMLAM/2014/ to free 1.3T
* /results/
  * removed erddap-dataset.hg/
  * forcing/ is 1.9T
  * confirmed that nowcast-green.201812/ (11T) 2015-2019 are on graham:nearline
  * /results/SalishSea/nowcast-green.201812/ contains 01jan15 to 30jun19
  * deleted SalishSea_1[dh]_*.nc to free ~9.9T
Modified /results2/SalishSea/nowcast-green.201905/add_std_name.sh to do all of SalishSea_1d_*dia2_T.nc variables and ran it for 2007 to today.
Started running bash loop to produce 201905 month-averaged grazing & mortality files
on a 4 worker x 4 threads stand-alone cluster in tmux on salish
in /results2/SalishSea/month-avg.201905/ for 2007 to 2017
Cherry-picked 3 dia2_T file commits from SS-run-sets improve-201905-metadata branch in 
SS-run-sets on arbutus so that tomorrow-onward files will have standard_name attrs.
(SalishSeaCast)

Continued work on prod_T files (biology & chemistry rates); sorted out gross primary productivity
standard names with Susan.
Created PR#2 as draft.
(SS-run-sets)

Sent out when2meet for Reshapr Intro session: https://www.when2meet.com/?16258775-HSMB7
(Reshapr)


Sat 30-Jul-2022
^^^^^^^^^^^^^^^

Finished running bash loop to produce 201905 month-averaged grazing & mortality files
on a 4 worker x 4 threads stand-alone cluster in tmux on salish
in /results2/SalishSea/month-avg.201905/: 2018 to 2022-jun
forecast2 and nowcast-blue failed due to XML parse errors; see notes re: SS-run-sets below.
Cherry-picked SS-run-sets channges re: productivity standard_name attrs and tag closure
reversion into production on arbutus.
(SalishSeaCast)

Reverted change to explicit closure tags in field_def.xml; I made a spelling mistake in my
change, but on examination of XIOS's rejection of that, noted that the only other places
where explicity </field> tags are used are where XIOS is being given a calculation to do;
worried that it would look for calculations to do where there are none if I use </field>
tags generally, I decided to live with <field ... />.
(SS-run-sets)

Drove to White Rock to visit J&M.

Discussed w/ Susan a scheme to store research paper citation data in 1 place and process
it from there into website, ERDDAP front page, and ERDDAP dataset comment metadata.
Also discussed spitting website citations into parts for papers people should cite
when they use SalishSeaCast, and papers that use SalishSeaCast products.


Sun 31-Jul-2022
^^^^^^^^^^^^^^^

Cycled Greenway to North Rd and back; early start to beat heat, humidity and traffic.
(45 km)

Goofed off.


August
======

Week 31
-------

Mon 1-Aug-2022
^^^^^^^^^^^^^^

**Statutory Holiday** - Emancipation Day

Cycled 8th, Balaclava, 29th, Camosun, Salish Trail, Spanish Banks, Jericho, Pt. Grey loop;
early start to beat heat and traffic.
(20 km)

Goofed off.


Tue 2-Aug-2022
^^^^^^^^^^^^^^

Heat warning ended. Slept indoors last night.

Squash-merged dependabot PRs re: catastrophic backtracking in inline markup in mistune
* UBC-MOAD/docs
* 43ravens/ECget
* SalishSeaCast/SOG-Bloomcast-Ensemble
* SalishSeaCast/analysis-doug/dask-expts
* SalishSeaCast/analysis-doug/melanie-geotiff
* SalishSeaCast/tools
* SalishSeaCast/docs

Group mtg.
(OceanParcels)

Continued work on slides notebook for Reshapr Intro workshop in branch in 
UBC-MOAD/PythonNotes/reshapr-intro/.
(Reshapr)

nowcast r12 failed to launch due to 
`packet_write_wait: Connection to 192.168.238.9 port 22: Broken pipe`
* investigation:
  * fvcom4 non-responsive
  * log has logs of messages like:
      [45739127.900239] INFO: task systemd-journal:601 blocked for more than 120 seconds.
      [45739127.905009]       Not tainted 4.15.0-135-generic #139-Ubuntu
      [45739127.908879] "echo 0 > /proc/sys/kernel/hung_task_timeout_secs" disables this message.
  * similar to other recent VM lock-ups
* recovery started at ~14:15
  * hard reboot of fvcom4 from web dashboard
  * mount shared storage fon fvcom4
  * on skookum:
      launch_remote_worker arbutus make_fvcom_boundary "arbutus r12 nowcast"
* failed again
* ssh to fvcom1 gets stuck; log shows similar messages; hard reboot from web dashboard
* fvcom2 shows similar messages; hard reboot from web dashboard
* another launch attempt from skookum; failed again on connection to fvcom4
* swapped fvcom1 for fvcom4 in mpi_hosts.fvcom.r12
* another launch attempt from skookum; failed again on connection to fvcom6
* gave up
(SalishSeaCast)


Wed 3-Aug-2022
^^^^^^^^^^^^^^

Raisha asked for implementation of -h flag for fisheries harvest that we discussed previously;
issue #3.
Created local harvest-flag branch.
Looks like impmentation can be exactly analogous to -m migrations flag in PR#11.
Asked Raisha to confirm type of harvest file; .csv?
(Atlantis)

Scheduled Reshapr intro session for 10:30 to 12:00 on Friday.
Continued work on slides notebook for Reshapr Intro workshop in branch in 
UBC-MOAD/PythonNotes/reshapr-intro/.
Reviewed and polished with Susan.
Invited Amber, Michael & Natasha to Friday session or their own later private session; 
Amber is away.
(Reshapr)

Reviewed and tweaked file system settings for Cassidy:
  sudo chgrp sallen /ocean/cdonaldson/
  sudo chmod g+s /ocean/cdonaldson/
  sudo chgrp sallen /data/cdonaldson/
  sudo chmod g+s /data/cdonaldson/
Confirmed that /home/cdonaldson/ exists and has cdonaldson:cdonaldson ownership.
**cdonaldson needs to be added to sallen group** - done by Henryk

Tried to backfill nowcast-r12/02aug22; failed.
Discovered that 01aug22 run failed due to connection error on fvcom4.
Killed watcher.
Started backfilling at 01aug22:
  launch_remote_worker arbutus make_fvcom_boundary "arbutus r12 nowcast 2022-08-01"
  running, but no progress messages
  restarted log_aggregator
  estimated run time is ~8h40m!!!
(SalishSeaCast)


Thu 4-Aug-2022
^^^^^^^^^^^^^^

upload_forcing failed for forecast2 and nowcast due to missing Neah Bay obs; obs file was not created by make_ssh_files, and symlink creation race condition in upload_forcing; recovery:
* manually created symlink from fcst/ssh_y2022m08d03.nc to obs/ssh_y2022m08d03.nc
* ran upload_forcing nowcast+ to all 4 destinations
Continued backfilling nowcast-r12:
  wait for r12 run from automation to fail at ~12:15
  launch_remote_worker arbutus make_fvcom_boundary "arbutus r12 nowcast 2022-08-02"
  wait for run to finish at ~22:15
  launch_remote_worker arbutus make_fvcom_boundary "arbutus r12 nowcast 2022-08-03"
(SalishSeaCast)

Added -h flag for harvest.prm file; issue #3 and PR#13.
Helped Raisha with git wrangling to test PR branch; test showed that we also need -q flag for
fisheries.csv file; added that.
Raisha got a run time stepping with PR branch; rebase-merged.
(AtlantisCmd)

Project mtg.
(Atlantis)

Puzzled over Michael's email about transposition of netCDF files to make time fastest changing
coordinate rather than slowest.
Buffed slides notebook for presentation tomorrow.
(Reshapr)


Fri 5-Aug-2022
^^^^^^^^^^^^^^

Intro presentation from UBC-MOAD/PythonNotes/reshapr-intro/ notebook to MOAD, 
Michael & Natasha @IOS and Greig @IOF
* discussion items:
  * model profile for ANHA12 on graham
  * model profile(s) for SalishSeaCast-201905 and others on graham
  * cluster config for interactive sessions on graham
  * "slicing creates large chunks" warning/failure issue 
  * output chunk control for special cases
  * coordinate permutations
  * Michael's trick for pkg editable install in conda env YAML file:
    - pip:
          -e .
(Reshapr)

Continued backfilling nowcast-r12:
  wait for r12 run from automation to fail at ~12:00
  launch_remote_worker arbutus make_fvcom_boundary "arbutus r12 nowcast 2022-08-04"
  wait for run to finish at ~22:15
  launch_remote_worker arbutus make_fvcom_boundary "arbutus r12 nowcast 2022-08-05"
nowacst-agrif failed due to no 04aug22/namelist_cfg **investigate**
(SalishSeaCast)


Sat 6-Aug-2022
^^^^^^^^^^^^^^

nowcast-agrif failures investivation:
* upload_forcing turbidity failed on 4aug due to SSH protocol banner issue;
  probably login node network stack glitch
* recovery started at ~13:00
    upload_forcing orcinus turbidity 2022-08-04
    wait for run to finish
    make_forcing_links orcinus nowcast-agrif 2022-08-05
    wait for run to finish
    make_forcing_links orcinus nowcast-agrif 2022-08-06
wwatch3 nowcast got stuck waiting for time steps; investigation:
* yesterday's run stalled w/ no output
* recovery started at ~14:30:
    cleaned up directories
    launch_remote_worker arbutus make_ww3_wind_file "arbutus forecast 2022-08-05"
    launch_remote_worker arbutus make_ww3_current_file "arbutus forecast 2022-08-05"
    no time steps
    nowcast9 is non-responsive; log shows lots of:
      [47082373.969252] INFO: task jbd2/vda1-8:477 blocked for more than 120 seconds.
      [47082373.974257]       Not tainted 4.15.0-135-generic #139-Ubuntu
      [47082373.978060] "echo 0 > /proc/sys/kernel/hung_task_timeout_secs" disables this message.
    and
      [47082373.983560] INFO: task systemd-journal:21576 blocked for more than 120 seconds.
      [47082373.988497]       Not tainted 4.15.0-135-generic #139-Ubuntu
      [47082373.992436] "echo 0 > /proc/sys/kernel/hung_task_timeout_secs" disables this message.    
    did a hard reboot of nowcast9 from web dashboard
    cleaned up directories
    launch_remote_worker arbutus make_ww3_wind_file "arbutus forecast 2022-08-05"
    launch_remote_worker arbutus make_ww3_current_file "arbutus forecast 2022-08-05"
    wait for runs to finish
    launch_remote_worker arbutus make_ww3_wind_file "arbutus forecast 2022-08-06"
    launch_remote_worker arbutus make_ww3_current_file "arbutus forecast 2022-08-06"
(SalishSeaCast)


Sun 7-Aug-2022
^^^^^^^^^^^^^^

Goofed off!

Installed MultiMC on khawla: conda envs but for Minecraft.
Successfully tested local 1.19.2 with updated mods and shaders (no resource packs).
Experimented with Tweakeroo to get free camera feature; could have used FreeCam mod,
but Tweakeroo is part of the Malilib/MiniHUD/Litematica ecosystem that we already use.


Week 32
-------

Mon 8-Aug-2022
^^^^^^^^^^^^^^

Group mtg.
(MOAD)

Confirmed that depth chunk size matches number of depth levels in extraction.
Experimented with 2 layer extraction using depth chunk size of 1 vs. 40:
* jan07, 40, 206.9s on khawla
* jan07, 1, 189.8s on khawla
* jan07, 40, 4526 tasks, 123.5s on khawlab
* jan07, 1, 8990 tasks, 199.6s on khawla
* jan07, 2, 4526 tasks, 139.9s on khawla
* jan07, 40, 4526 tasks, 123.3s on khawla
Worked on date formatter additions and refactoring in add-date-formatters branch; PR#40.
Realized that Reshapr is presently hard-wired to process day-by-day files;
Greig's use case has day-avg fields in month files; e.g.
  /scratch/goldford/SalishSea-RUN203_1d_grid_U_y1984m04.nc
Asked Birgit for path to ANHA12 5-day files:
  /project/def-allen/brogalla/GEOTRACES/data/ANHA12/ANHA12-EXH006_5d_gridT_y2002m01d05.nc
happy to see that they are day-by-day, with a 5 day stride.
Neither Greig nor ANHA12 use deflation!
(Reshapr)


Tue 9-Aug-2022
^^^^^^^^^^^^^^

Worked at ESB while Rita was at home.

Finished work on prod_T files (biology & chemistry rates); sorted out surface CO2 flux
standard name with Susan; merged PR#2.
Realized that I forgot to do the TQ10 variable; Susan came up with a standard_name that fits the
CF style.
Modified /results2/SalishSea/nowcast-green.201905/add_std_name.sh to do all of SalishSea_1d_*prod_T.nc variables and ran it for 2007 to today.
* HDF errors:
    20aug20/SalishSea_1d_20200820_20200820_prod_T.nc
    21aug20/SalishSea_1d_20200821_20200821_prod_T.nc
    22aug20/SalishSea_1d_20200822_20200822_prod_T.nc
  resolved on re-run of add_std_name.sh
Started running bash loop to produce 201905 month-averaged biology & chemistry rates files
on a 4 worker x 4 threads stand-alone cluster in tmux on salish
in /results2/SalishSea/month-avg.201905/ for 2007 to 2016.
Cherry-picked 2 prod_T file commits from SS-run-sets master branch in 
SS-run-sets on arbutus so that tomorrow-onward files will have standard_name attrs
and corrected surface CO2 flux long_name and units attrs.
(SS-run-sets)


Wed 10-Aug-2022
^^^^^^^^^^^^^^^

Finished running bash loop to produce 201905 month-averaged biology & chemistry rates files
on a 4 worker x 4 threads stand-alone cluster in tmux on salish
in /results2/SalishSea/month-avg.201905/ for 2017 to 2022-jul.
(SS-run-sets)

forecast2 nowcast got stuck waiting for time steps; investigation:
* nowcast4 is non-responsive; repeated jbd2/vda1 blocked msgs
* recovery started at ~09:00:
    cleaned up directories
    did a hard reboot of nowcast4 from web dashboard
    mounted shared storage on nowcast4
    skipped forecast2 runs
    make_forcing_links arbutus nowcast+
(SalishSeaCast)

Prius regular service:
* oil change & tire/brake inspection; tires are 8/32s, brakes are 8mm front, 7mm rear
* **rear wiper blade & cabine air filter should be replaced**
* hot oil flush
* brake fluid change
* fuel system service; cleaned injectors

Cleaned the espresso machine.

Helped Karyn find GEMLAM HRDPS atmos forcing files and warned her of their ideocyncracies.

Squash-merged dependabot PRs in 43ravens/ECget re:
* html5lib re: cross-site scripting (XSS)
* html5lib re: improper input neutralization
* notebook token bruteforcing
* nbconvert XSS
Squash-merged dependabot PRs in SalishSeaCast/tools & SalishSeaCast/analysis-doug re:
* nbconvert XSS
(MOAD)

Updated nodecraft server to 1.19.2:
* stopped server
* created Scurry Junkertown backup
* used 1 click installer to change version from 1.19 w/ fabric 1.19-0.14.6 to
  1.19.2 w./ fabric 1.19.2-0.14.9 via archive method
* copied files from _old_files/2022-08-10T22-46-01-276Z/ to /:
    1_18-1/ (world)
    banned-ips.json
    banned-players.json
    eula.txt
    ops.json
    server.properties
    whitelist.json
* no need to update coordinatesHUD and doubleshulkerShells datapacks; release versions are unchanged
* server started successfully
* uploaded to /mods/:
    lithium-fabric-mc1.19.2-0.8.3.jar
    phosphor-fabric-mc1.19.x-0.8.1.jar
* restarted server
* re-purposed Fabric 1.19.2 testing instance to become Nodecraft 1.19.2
  * had some hassels getting big screen resolution
  * manually configured MiniHUD, but could have copied minihud.json from config folder of
    another instance
* copied resource packs from Nodecraft 1.19 instance; no new releases:
    BorderlessStainedGlass
    ClearerWater
    LowerShield
    RedstonDevices (my name for hoopers, droppers, dispensers, observers & levers together)


Thu 11-Aug-2022
^^^^^^^^^^^^^^^

Team mtg.
Started review/comments on Raisha & Sara paper; others won't finish until end of Aug.
(Atlantis)


Fri 12-Aug-2022
^^^^^^^^^^^^^^^

Finished review/comments on Raisha & Sara paper.
(Atlantis)

Created issue #41 re: extractions from ANHA12 for Birgit.
Added comment to PR#40 about need for other than day-by-day date stepping in calc_ds_paths()
and how that requirement is related to issue #32 re: month-average datasets 
and issue #40 re: ANHA12.
(Reshapr)


Sat 13-Aug-2022
^^^^^^^^^^^^^^^

Vancouver to Longbeach on West Arm of Kootenay Lake, east of Nelson.
Rest area stop west of Hope.
Lunch at Fanny's Café in Princeton
Stopped at Mom & Pop's Fruit Stand in Keremeos
Rest area stop at Boundary Creek provincial campground


Sat 13-Aug-2022
^^^^^^^^^^^^^^^

Vacation at Longbeach Suites near Nelson


Week 33
-------

Mon 15-Aug-2022
^^^^^^^^^^^^^^^

Vacation at Longbeach Suites near Nelson


Tue 16-Aug-2022
^^^^^^^^^^^^^^^

Vacation at Longbeach Suites near Nelson

Drove to Nelson
Coffee & blueberry cinnamon buns at Kootenay Lake Bakery
Walked length of Baker St.
Shopped at Co-op


Wed 17-Aug-2022
^^^^^^^^^^^^^^^

Vacation at Longbeach Suites near Nelson

Drove 16km up very rough Kokanee Provincial Park access road to Kokanee Lake trailhead.
Walked around Gibson Lake (2.4 km)
Hiked up to ~2000m pass above Kokanee Lake and back to trailhead (10 km)
Went to Balfour Supperette for groceries.

collect_weather 12 didn't store any files; no obvious reason, though #it-support has hints
of a problem this morning
recovery started at ~16:00
  kill collect_weather 12
  rm -rf /results/forcing/atmospheric/GEM2.5/GRIB/20220817/12
  download_weather 12 2.5 km
  download_weather 18 2.5 km
  download_weather 00 1km
  download_weather 12 1km
  collect_weather 00 2.5km
(SalishSeaCast)


Thu 18-Aug-2022
^^^^^^^^^^^^^^^

Vacation at Longbeach Suites near Nelson

Cycled to Balfour ferry, crossed, and rode over the hill to Crawford Bay and back
(32 km)


Fri 19-Aug-2022
^^^^^^^^^^^^^^^

Vacation at Longbeach Suites near Nelson

Drove to Kaslo.
Cycled Hwy 31 to Meadow Creek and back. Big climb out of Kaslo. Hilly to Lardeau Valley at head
of Kootenay Lake and mouth of Duncan River, then a fast flat-ish section to Meadow Creek.
Hills were steeper on west sides than on east. Rolling time was almost exactlly 2h each way.
(81 km)

See work journal.
(Resilient-C)


Sat 20-Aug-2022
^^^^^^^^^^^^^^^

Vacation at Longbeach Suites near Nelson


Sun 21-Aug-2022
^^^^^^^^^^^^^^^

Vacation at Longbeach Suites near Nelson


Week 34
-------

Mon 22-Aug-2022
^^^^^^^^^^^^^^^

Vacation at Longbeach Suites near Nelson

Rode Great Northern Rail Trail from Cottonwood Lake through Ymir to Salmo and back.
(68 km)


Tue 23-Aug-2022
^^^^^^^^^^^^^^^

Vacation at Longbeach Suites near Nelson

Explored around Harrop and Procter; Sunshine Bay, Lasca Creek Rd.
(30 km)
Went to Le Grand Fromage cheese shop and Backroads Brewing.
Explored Stanley St, Gore St, Innis St neighbourhood where Latornells lived.
Found Bobbie Latornell window in St. Saviour church.
Visited Kokanee Creek spawning channel where Kokanee salmon are spawning.


Wed 24-Aug-2022
^^^^^^^^^^^^^^^

Vacation at Longbeach Suites near Nelson

Hiked Sproule Creek Millsite trail with East Fork loop on return.


Thu 25-Aug-2022
^^^^^^^^^^^^^^^

Vacation at Longbeach Suites near Nelson


Fri 26-Aug-2022
^^^^^^^^^^^^^^^

Longbeach on West Arm of Kootenay Lake, east of Nelson to Vancouver.

Rest area stop at Boundary Creek provincial campground
Lunch stop at Anarchist Summit lookup above Osoyoos
Stopped at Mom & Pop's Fruit Stand in Keremeos
Rest area stop west of Hope.


Sat 27-Aug-2022
^^^^^^^^^^^^^^^

Discovered that nowcast-green onward failed yesterday due to too many levels of symlinks on
turbidity forcing file; recovery:
  symlink 26aug22 to 16jul22 (last good obs)
  wait for nowcast-blue to fail
  upload_forcing arbutus turbidity 2022-08-26
  upload_forcing optimum turbidity 2022-08-26
  upload_forcing graham-dtn turbidity 2022-08-26
  wait for nowcast-green/26aug runs to finish
  launch_remote_worker arbutus make_ww3_wind_file "arbutus forecast 2022-08-26"
  launch_remote_worker arbutus make_ww3_current_file "arbutus forecast 2022-08-26"
  wait for wwatch2/26aug runs to finish
  upload_forcing arbutus nowcast+ 2022-08-27
  wait for nowacst-agrif to fail
  upload_forcing orcinus turbidity 2022-08-26
  wait for nowacst-agrif run to complete
  upload_forcing orcinus turbidity 2022-08-27
  wait for nowacst-dev to fail
  make_forcing_links salish nowcast+ --shared-storage 2022-08-26
  wait for nowacst-dev run to complete at ~19:30
  make_forcing_links salish nowcast+ --shared-storage 2022-08-27
(SalishSeaCast)

Drove to White Rock to visit J&M and celebrate 64th wedding anniversary & JRA 96th bday
w/ Max, Jingli & Sylvia


Sun 28-Aug-2022
^^^^^^^^^^^^^^^

nowcast-blue got stuck waiting for time steps; investigation:
* nowcast1 is non-responsive; repeated jbd2/vda1 blocked msgs
* recovery started at ~09:40:
    did a hard reboot of nowcast4 from web dashboard
    mounted shared storage on nowcast1
    killed watcher and run scrip on arbutus
    cleaned up directories
    make_forcing_links arbutus nowcast+
(SalishSeaCast)

Rode Iona and Canada Line loop with a deviation at the start to look at a house for sale
on W 11th; used 14th (very rough), Valley, and Arbutus Greenway to get to Arthur Lang bridge.
(43 km)


Week 35
-------

Mon 29-Aug-2022
^^^^^^^^^^^^^^^

Updated PyCharm on khawla to 2022.2.1.

Removed get_onc_ferry from automation because instrumented TWDP ferry was moved to another
route on 21jun22; PR#109 merged; deployed to production
  Consider adding datasets from HBDB and TWSB ferry instruments that are presently operational.
Updated hindcast results dirs re: Susan's uncommitted chg in prod for v202111 runs.
(SalishSeaNEMO)

Squash-merged dependabot PRs:
* nbconvert re: XSS vulnerability
  * UBC-MOAD/docs
  * SalishSeaCast/tools
  * SalishSeaCast/analysis-doug/melanie-geotiff
  * SalishSeaCast/docs
  * SalishSeaCast/SOG-Bloomcast-Ensemble
  * SalishSeaCast/analysis-doug/dask-expts
 * 43ravens/ECget 
Updated docs re: Compute Canada -> Alliance and Westgrid -> BC DRI Group; triggered by linkcheck
failures.
Group mtg; see whtieboard.
Toured repos to re-enable scheduled GHA workflows that were disabled due to lack of activity.
(MOAD)

Updated sentry-sdk (and certifi & openssl as deps) in prod env on skookum.
Updated docs re: Compute Canada -> Alliance and Westgrid -> BC DRI Group; triggered by linkcheck
failures.
(SalishSeaCast)


Tue 30-Aug-2022
^^^^^^^^^^^^^^^

collect_river_data failed for all rivers
* investigation:
  * last update of datamart/hydrometric/ files was ~28aug22 21:40
  * sarracenia log shows server closed connection at ~21:55 then repeated
      sr_amqp/build could not declare queue q_anonymous.sr_subscribe.hydrometric.91042830.24145946 (anonymous@dd.weather.gc.ca) with EOF occurred in violation of protocol (_ssl.c:2396)
* recovery started at ~09:15
  * restarted sr_subscribe-hydrometric via supervisorctl
  * wait for expected hydrometric files update at ~09:40
  * run collect_river_data for 12 rivers via script in datamart/hydrometric/
    upload_forcing arbutus nowcast+
    upload_forcing orcinus nowcast+
    upload_forcing optimum nowcast+
    upload_forcing graham-dtn nowcast+
(SalishSeaCast)

Created issue #42 re: arrow timezone parser error reported by Natasha.
Created issue #43 re: extraction failure for HRDPS due to change in set of variables in dataset
reported by Natasha.
Created issue #44 re: sea bottom field extractions requested by Greig and someone else communicating
with Susan and Raisha.
Updated pkgs & versions in reshapr-dev env on khawla.
Added editable install to env description files; PR#45: merged.
Worked on issue #42 re: arrow timezone parser error.
(Reshapr)


Wed 31-Aug-2022
^^^^^^^^^^^^^^^

collect_river_data failed for Salmon River at Sayward; stream gauge out of service due to cableway 
issue as of 2022-08-29T19:10-07:00.
(SalishSeaCast)

MOAD coffee chat.

Resolved issue #42 re: arrow timezone parser error; merged PR#46.
Finished adding yyyy() and nemo_yyyymm() date formatter functions;
refactored date formatter functions into ``utils.date_formatters`` module;
re: PR#40
(Reshapr)


September
=========

Thu 1-Sep-2022
^^^^^^^^^^^^^^

uptimerobot reported 2 intervals of downtime for arbutus.cloud:
* 43 min starting at 2022-09-01 06:16:39
* 14 min starting at 2022-09-01 07:14:05
* fortunately, no impact on automation
(SalishSeaCast)

Updated sodium, iris, ComplementaryShaders & ComplementaryReimagined in multimc instances.

See work journal.
(Resilient-C)


Fri 2-Sep-2022
^^^^^^^^^^^^^^

Zoom w/ Karyn re: HRDPS winds across 22sep11 gemlam grid change, and change from gemlam to ops grid.

Confirmed that /home/cstang/ exists and has cstang:cstang ownership.
Confirmed that cstang is a member of sallen group.
Reviewed and tweaked file system settings for Camryn:
  sudo chgrp sallen /ocean/cstang/
  sudo chmod g+s /ocean/cstang/
  sudo mkdir /data/cstang/
  sudo chgrp sallen /data/cstang/
  sudo chmod g+s /data/cstang/

Rebase-merged PR#40 re: adding yyyy() and nemo_yyyymm() date formatter functions
and refactoring date formatter functions into ``utils.date_formattersm`` module.
Created issue #47 re: extraction from Greig & Michael's coarsened SalishSeaCast model product wutb
day avgs stored in month files like:
  SalishSea1500-RUN203_1d_grid_T_2D_y1984m04.nc
  SalishSea1500-RUN203_1h_grid_U_y1984m04.nc
  SalishSea-RUN203_1d_grid_U_y1984m04.nc
Pushed addition of bottleneck & flox to user env after a month of successful in dev, GHA test & my
salish user env.
(Reshapr)

wwatch3 nowcast got stuck waiting for time steps; investigation:
* nowcast3 is non-responsive; repeated jbd2/vda1 blocked msgs
* recovery started at ~17:30:
    did a hard reboot of nowcast3 from web dashboard
    mounted shared storage on nowcast3
    killed watcher and run script on arbutus
    cleaned up directories
    launch_remote_worker arbutus make_ww3_wind_file "arbutus forecast 2022-09-02"
    launch_remote_worker arbutus make_ww3_current_file "arbutus forecast 2022-09-02"
(SalishSeaCast)


Sat 3-Sep-2022
^^^^^^^^^^^^^^

upload_forcing arbutus  nowcast+ failed due to bad ssh protocol banner; investigation:
* nowcast0 is non-responsive; repeated jbd2/vda1 blocked msgs
* checked other VMs via web dashboard:
  * nowcast5 has repeated jbd2/vda1 blocked msgs
  * nowcast7 has repeated jbd2/vda1 blocked msgs
  * fvcom3 log is not waiting for login; ends in daily apt upgrade & clean activities
* decided to update and reboot all VMs
  * compute VMs:
      fvcom[0-6]:
        sudo apt update
        sudo apt upgrade -y
        sudo apt autoremove
        sudo shutdown -r now
      nowcast[2-4,6,8-9]:
        sudo apt update
        sudo apt upgrade -y
        sudo apt autoremove
      nowcast[1]:
        # sudo apt upgrade failed
        sudo dpkg --configure -a
        sudo apt upgrade -y
        sudo apt autoremove
        sudo shutdown -r now
      nowcast[5,7]:
        # sudo apt upgrade failed: dpkg frontend is locked by another process
        ps faux | grep dpkg  # shows stuck dpkg processes:
          4540 /usr/bin/dpkg --status-fd 12 --configure --pending
          4553 /bin/sh /var/lib/dpkg/info/linux-image-4.15.0-191-generic.postinst triggered linux-update-4.15.0-191-generic
        # killed stuck dpkg processed; dpkg interrupted state
        sudo dpkg --configure -a  # got stuck; interupted
        sudo shutdown -r now
        # stuck dueing reboot due to:
          A stop job is running for /nemoShare/MEOPAR
          A stop job is running for /mnt
        # hard reboot via web dashboard
        sudo apt update
        sudo apt upgrade -y
        sudo apt autoremove
        sudo shutdown -r now
      nowcast0:
        sudo apt update
        sudo apt upgrade
        sudo apt autoremove
        sudo shutdown -r now
        # hard reboot via web dashboard
        sudo mount /dev/vdc /nemoShare
        ll /nemoShare/MEOPAR/  # to confirm mount
        sudo mount --bind /nemoShare/MEOPAR /export/MEOPAR
        ll /export/MEOPAR  # to confirm mount
        sudo systemctl start nfs-kernel-server.service
        sudo exportfs -f  # to reset NFS handles for compute nodes
      nowcast[1-9] and fvcom[0-6]:
        sudo mount -t nfs -o proto=tcp,port=2049 192.168.238.14:/MEOPAR /nemoShare/MEOPAR
        # fvcom6 was stubborn; hard reboot; shutdown -r
      nowcast0
        # confirm compute nodes have /nemoShare/MEOPAR/ mounted:
        for n in {1..9}; do   echo nowcast${n};   ssh nowcast${n} "mountpoint /nemoShare/MEOPAR"; done
        for n in {1..9}; do   echo nowcast${n};   ssh nowcast${n} "ls -C /nemoShare/MEOPAR"; done
        for n in {0..6}; do   echo fvcom${n};   ssh fvcom${n} "mountpoint /nemoShare/MEOPAR"; done
        for n in {0..6}; do   echo fvcom${n};   ssh fvcom${n} "ls -C /nemoShare/MEOPAR"; done
(SalishSeaCast)


Sun 4-Sep-2022
^^^^^^^^^^^^^^

Goofed off.


Week 36
-------

Mon 5-Sep-2022
^^^^^^^^^^^^^^

**Statutory Holiday** - Labour Day

Cycled Fort Langley, Derby Reach, Mt. Lehman loop
(67 km)


Tue 6-Sep-2022
^^^^^^^^^^^^^^

Worked at ESB while Rita was at home.

Worked on issue #38 re: single index value extraction selection semantics; 
stalled on whether or not to extend code max+1 to all selections; doing so breaks with expectations
of working with 0-base Python indexing, despite how nice it looks for single index value extractions
Updated reshapr clone and user env on salish.
Tested single point, 2 depths extraction of temperature and salinity for Becca with code changes
for issue #38:
* single point semantics are good
* need to decide if max + 1 should be done for all values of max that are not None (grid extent)
* ran tests to find the point at which "large chunk" warning appears:
  * 1-4 yrs okay
(Reshapr)

Ran /results2/SalishSea/month-avg.201905/month-average.sh script on salish to generated 2019-05 
files for August.
(SalishSeaCast)


Wed 7-Sep-2022
^^^^^^^^^^^^^^

Continued testing single point, 2 depths extraction of temperature and salinity for Becca re:
"large chunk" warning appears:
  * 7, 11, 13, 15 yrs okay
  * warning arose when I tried to make the end date 2022-08-31; full years are okay
Started improving CLI start/end dates variable names and handling in extracted dataset history 
attribute.
(Reshapr)

Emailed EGBC practice advisor re: necessity for permit to practice for 43ravens.

Power failure in ESB at ~10:00 caused manager to shutdown;
* impacts:
  * lots of name resolution failure messages from watch_NEMO_agrif, but it continued to run
  * qstat on orcinus is failing; motd says that all compute nodes went down
  * job was restarted by queue manager, I restarted watcher
      watch_NEMO_agrif orcinus 10961523.orca2.ibb
(SalishSeaCast)

Configured docs.blogofile.com and www.blogofile.com in response to email from readthedocs; 
blogofile.com domain is still registered, but there is nothing there or at the subs

FAL estate work:
* met w/ Sahi @ TD to do forms to get BCE DRS shares into my TD Direct cash account;
  may take 10-15 business day on TD side plus time for TSX to respond


Thu 8-Sep-2022
^^^^^^^^^^^^^^

Raisha reported VSCode connection problem to tyee; confirmed; survey other systems:
* okay:
  * salish
  * smelt
  * hake
  * lox
* fail:
  * tyee - rebooted
  * char - started & working
  * chum - working
  * cod - on disposal pile
  * coho - on disposal pile
  * halibut - on disposal pile
  * herring - on disposal pile

Telcon w/ Alice Krutchen @EGBC re: firm registration & permit to practice:
* software is covered by engineering practice, so registration is probably required
* official review can be requested to provide definitive rulling; she will send link

Reviewed onboarding docs:
* move Alliance account setup to #8; need link back to ssh-setup
* add Windows stuff to ssh setup
* add section about VSCode for remote access, notebooks, git integration, etc.
Added links to pkgs & envs, and sphinx docs slide notebooks to MOAD docs.

Went to UBC for onboarding mtg w/ Cassidy & Camryn and to locate/reboot workstations.
Onboarding:
* cycling facilities
* machines and storage
* Linux
* ssh
* git
  * adds to MOAD list
  * change/commit via GitHub interface
  * change in editor, commit via command-line
  * change/commit in VSCode
Next session:
* SalishSeaCast, website, ERDDAP
* conda
* analysis repos
* jupyter
* VSCode
(MOAD)

Weekly mtg.
(Atlantis)


Fri 9-Sep-2022
^^^^^^^^^^^^^^

upload_forcing forecast2 and nowcast+ both failed due to symlink race condition on 
obs/ssh_y2022m09d08.nc
* recovery started at ~09:05
    ln -s /results/forcing/sshNeahBay/fcst/ssh_y2022m09d08.nc /results/forcing/sshNeahBay/obs/ssh_y2022m09d08.nc
    upload_forcing arbutus nowcast+
    upload_forcing orcinus nowcast+
    upload_forcing optimum nowcast+
    upload_forcing graham-dtn nowcast+
(SalishSeaCast)

Decided to abandon issue #38 re: single index value extraction selection semantics because
breaks with expectations of working with 0-base Python indexing, despite how nice it looks for 
single index value extractions.
Cherry-picked test improvements from issue38 branch to main.
Finished improving CLI start/end dates variable names and handling in extracted dataset history 
attribute; PR#48: rebase-merged
(Reshapr)

Helped Cassidy debug ssh public key installation and connection issues from Windows 11 to waterhole
machines.

Installed iris-1.3 in nodecraft and local 1.19.2 minecraft instances.


Sat 10-Sep-2022
^^^^^^^^^^^^^^^

upload_forcing forecast2 and nowcast+ both failed due to symlink race condition on 
obs/ssh_y2022m09d09.nc; Susan confirmed missing obs on 8th & 9th
* recovery started at ~08:45
    nemo_nowcast.workers.clear_checklist  # to rotate logs
    ln -s /results/forcing/sshNeahBay/fcst/ssh_y2022m09d09.nc /results/forcing/sshNeahBay/obs/ssh_y2022m09d09.nc
    upload_forcing arbutus nowcast+
    upload_forcing orcinus nowcast+
    upload_forcing optimum nowcast+
    upload_forcing graham-dtn nowcast+
(SalishSeaCast)

Drove to White Rock to visit J&M.


Sun 11-Sep-2022
^^^^^^^^^^^^^^^

Cycled to Steeveston via Richmond Dyke southbound, and 2 Rd greenway path northbound;
took it slow because the air was quite smokey.
(48 km)

Changed a bunch more logins from oplop to 1password.

upload_forcing forecast2 and nowcast+ both failed due to symlink race condition on 
obs/ssh_y2022m09d10.nc; Susan confirmed missing obs on 8th & 9th
* recovery started at ~13:35
    nemo_nowcast.workers.clear_checklist  # to rotate logs
    ln -s /results/forcing/sshNeahBay/fcst/ssh_y2022m09d10.nc /results/forcing/sshNeahBay/obs/ssh_y2022m09d10.nc
    upload_forcing arbutus nowcast+
    upload_forcing orcinus nowcast+
    upload_forcing optimum nowcast+
    upload_forcing graham-dtn nowcast+
nowcast-r12 failed on launch
* investigation:
* fvcom5 is non-responsive; repeated jbd2/vda1 blocked msgs
* recovery started at ~17:55
    did a hard reboot of fvcom5 from web dashboard
    mounted shared storage on fvcom5
    cleaned up directories
  launch_remote_worker arbutus make_fvcom_boundary "arbutus r12 nowcast 2022-09-11"
(SalishSeaCast)

Installed tables & chairs datapack-4.3.4 local 1.19.2 minecraft instance.
Server installation was sort of tricky/non-intuitive:
* Download Chuckchuk/Chuck-RP.zip v6.22 from GitHub
* use sha1sum to create SHA-1 hash of it
* Add download URL and SHA-1 hash to nodecraft server via Game Settings > Gamemode
* Download datapack from planetminecraft.com
* Upload datapack to nodecraft workd datapacks direcory via File manager
* Restart server


Week 37
-------

Mon 12-Sep-2022
^^^^^^^^^^^^^^^

Emailed Hillcrest Plumbing re: repairs.

Group mtg; see whiteboard.
* Susan want's time series at ONC central node from double resolution run
(MOAD)

Updated docs:
* broken & redirected links
* dropped Anaconda from installation & dev docs in favour of Miniforge or Miniconada3
* add pip install -e to conda env descriptions
(NEMO-Cmd)

Created issue #49 re: StopIteration exception from `reshapr info` when results archive path 
does not exist; fixed it with PR#50: rebase-merged.
Analyzed Natasha's issue #43 report re: Extraction failure for HRDPS due to change in 
set of variables in dataset:
* She didn't give enough detail of the extraction she was doing, but I suspect that it was
  1 variable-year per file. If so, the behaviour she saw is not a but. File should have NaNs
  before the variables appeared and values after.
* Did find a bug whereby extractions for another variable that span the date when a new variable
  was added to the dataset include the new variable even though it was not requested.
  Discussion w/ Susan lead to the hypothesis that this is due to the calculation of the drop_vars
  set based on the list of variables in only the 1st dataset file in the time range. 
  Need to at least union the variable lists from 1st and last datset files.
  Perfact solution would be to union variable lists from all dataset files in time range,
  but that might significantly slow processing. We know that so far, variables have only been added.
(Reshapr)


Tue 13-Sep-2022
^^^^^^^^^^^^^^^

Mtg. Decided that it will be the last scheduled because only Raisha and Jose are using Parcels
in research.
(OceanParcels)

ONC SoG east node data stream resumed on 30aug.
(SalishSeaCast)

Sent Cassidy links about ssh.exe instance gcross-up between Git and Windows 10.

See work journal.
(Resilient-C)

Helped Camryn w/ .bash_profile and conda env setup.

Rode Zwift Academy baseline ride.


Wed 14-Sep-2022
^^^^^^^^^^^^^^^

Read readthedocs service data analysis email report; see TODOS re:
* sphinx-notfound-page
* build:os config update to ubuntu-22.04

Created issue #51 re: unrequested variable in extractions that span date of variable added to dataset.
(Reshapr)

Checked wwatch3 results archives:
* /opp
    wwatch3$ find hindcast -type d -name "*15" | wc -l
    59
    wwatch3$ find hindcast -type d -name "*16" | wc -l
    35
    wwatch3$ find hindcast -type d -name "*17" | wc -l
    24
    wwatch3$ find hindcast2 -type d -name "*17" | wc -l
    9
    wwatch3$ find nowcast/ -type d -name "*17" | wc -l
    279
    wwatch3$ find nowcast/ -type d -name "*18" | wc -l
    368
    wwatch3$ find nowcast/ -type d -name "*19" | wc -l
    361
* graham:project/MIDOSS/forcing/wwatch3/
    [dlatorne@gra-login2 wwatch3]$ find . -type d -name "*15" | wc -l
    365
    [dlatorne@gra-login2 wwatch3]$ find . -type d -name "*16" | wc -l
    366
    [dlatorne@gra-login2 wwatch3]$ find . -type d -name "*17" | wc -l
    365
    [dlatorne@gra-login2 wwatch3]$ find . -type d -name "*18" | wc -l
    365
Deleted hindcast12/
Cleared hindcast/
Used tmux session to rsync graham:project/MIDOSS/forcing/wwatch3/ to hindcast/
  rsync -rltvz --progress --perms --chmod=Do+rx,Fo+r \
    graham-dtn:project/MIDOSS/forcing/wwatch3/ /opp/hindcast/
(WWatch3)


Thu 15-Sep-2022
^^^^^^^^^^^^^^^

Changed readthedocs config to use ubuntu-22.04.
Added sphinx-notfound-page extension to docs build.
Added model profile for 1905 double resolution experiment including example
use case re: Susan's request for T&S at ONC central node; PR#xx
Discovered that chunking of:
  time: 24
  depth: 80
  y: 898
  x: 398
is faster than storage chunking of:
  time: 1
  depth: 40
  y: 1796
  x: 796
so, we need a way to override chunking from extraction config YAML.
I wonder if 1h files that contain 24h of results should always use 24 as the time chunk size?
(Reshapr)

UBC-DFO modeling mtg:
* ESMPy via Neil Swart for HRDPS land mask: https://earthsystemmodeling.org/regrid/

Weekly mtg.
(Atlantis)

Started work on visualizing and presenting SoG deep water renewal events in 2017 in the 
double resolution hindcast; had to regenerate nowcast-green research figures for a bunch
of dates in summer 2017.
(Hindcast)

Went to Faculty of Science ADs thank-you dinner at the Teahouse.


Fri 16-Sep-2022
^^^^^^^^^^^^^^^

Continued work on visualizing and presenting SoG deep water renewal events in 2017 in the 
double resolution hindcast; regenerated more nowcast-green research figures for dates in 
summer 2017.
(Hindcast)

See work journal.
(Resilient-C)

Squash-merged dependabot PRs re: DoS vulnerability in mako:
* SalishSeaNowcast
* salishsea-site
* SOG-Bloomcast
* douglatornell/raspi_x10
(SalishSeaCast)

Cleaned up uncommitted env file in deployment env that was preventing GHA deployment workflow.
(salishsea-site)


Sat 17-Sep-2022
^^^^^^^^^^^^^^^

Rode Zwift Academy workeout #1.

See work journal.
(Resilient-C)


Sun 18-Sep-2022
^^^^^^^^^^^^^^^

Rode Gunnars on Steeveston out & back route; strong NW wind.
(44 km)

Added lizzy to borg-backup framework on smelt:
* created borg repo for lizzy
    borg init --encryption=repokey-blake2 /backup/borg/lizzy
* set up .gitconfig in lizzy:/home/doug
* cloned douglatornell/borg-bkup to lizzy:/home/doug
* created borg-bkup/lizzy-smelt.sh script and used it for 1st lizzy backup to smelt


Week 38
-------

Mon 19-Sep-2022
^^^^^^^^^^^^^^^

National Day of Mourning for QE2.

See work journal.
(Resilient-C)

Updated PyCharm to 2022.2.2.

Rode Zwift Academy workeout #2.


Tue 20-Sep-2022
^^^^^^^^^^^^^^^

Worked at ESB while Rita was at home.

Got COVID-19 booster.

Worked on improving MOAD onboarding docs, mostly re: analysis repos.
Used https://github.com/ammaraskar/sphinx-problem-matcher
to add a VSCode problem-matcher to sphinx build task.
Added section about VSCode and recommended extensions.
(MOAD)

Got EOAS-AD password reset to one I generated via 1password; works now for
bookings, gitlab, helpdesk, nextcloud, and www.

Reviewed and commented on Susan's updated ad for the O2 postdoc job.


Wed 21-Sep-2022
^^^^^^^^^^^^^^^

Hillcrest Plumbing in to repair master bathroom sink & toilet, and install laundry box
so that washer & dryer can sit back in laundry closet far enough for bifold door to be 
re-installed.

Worked w/ Susan on re-org of variables in results files for 2111 hindcast.
(SalishSeaCast)

Phys Ocgy seminar.

Renewed car insurance.

Continued work on visualizing and presenting SoG deep water renewal events in 2017 in the 
double resolution hindcast; confirmed nearest model point to nominal obs location; created preliminary salinity plots to make sure there is something interesting.
(Hindcast)


Thu 22-Sep-2022
^^^^^^^^^^^^^^^

Buffed SalishSeaCast.202111-2xrez-salish model profile and created PR#53 to add it.
(Reshapr)

Discussed w/ Susan calculation of day & month averages for 2111 spin-up:
* will be done on salish after download, not optimum
* no need for day-averages during spin-up, just month-averages
* should eventually be done via worker that uses Reshapr
* TODO:
  * create SalishSeaCast.202111-salish model profile
(SalishSeaCast)

Prepped for 2nd onboarding mtg w/ Cassidy & Camryn.

Worked at ESB for Welcome Back BBQ and mtg w/ Cassidy & Camryn.

Created personal docs/example/SalishSeaCast-202111-blue_single model profile for 
2017 regular resolution run results in /results2/SalishSea/hindcast_blue.single/ 
that Susan created for comparison to double resolution run

TODO:
* Do T&S extraction from blue_single - need to get files split
(Hindcast)

EOAS Welcome Back! BBQ.

Installed rust on khawla via:
  curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
Installed some rust replacements for command-line tools:
(from https://betterprogramming.pub/5-cli-tools-made-with-rust-to-improve-already-popular-tools-506af07b6d54)
* bat replaces cat
* exa replaces ls
* du-dust replaces du (dust)
* bottom repalces top (btm)
* ripgrep replaces grep

Reviewed nowcast-green.202111 output files:
TODO:
* long_name for time_counter: UTC Date/Time - can't figure out how to do this :-(
* 1h_grid_T:
  * sossheig long_name title-case - done
  * votemper long_name -> Conservative Temperature - done
  * votemper units -> degree_C - done
  * vosaline long_name -> Reference Salinity - done
  * sigma_theta long_name -> Potential Density (sigma_theta) - done
  * sigma_theta units -> kg m-3 - done
  * e3t long_name -> title-case - done
* 1h_grid_U:
  * vozorcrtx long_name title-case - done
  * vozorcrtx units -> m s-1 - done
* 1h_grid_V:
  * time_counter long_name title-case - done
  * vomecrty long_name title-case - done
  * vomecrty units -> m s-1 - done
* 1h_grid_W:
  * vovecrtz long_name title-case - done
  * vovecrtz units -> m s-1 - done
  * vert_eddy_diff long_name title-case - done
  * vert_eddy_diff units -> m2 s-1 - done
  * vert_eddy_visc long_name title-case - done
  * vert_eddy_visc units -> m2 s-1 - done
  * **dissipation long_name title-case**
  * dissipation units -> m2 s-3 - done
* 1h_biol_T:
  * ALL GOOD!!!
* 1h_chem_T:
  * PAR units -> W m-2 - done
  * turbidity standard_name > sea_water_turbidity - done
  * turbidity long_name > Fraser River Turbidity Tracer - done
  * turbidity units 1 or NTU  -> Susan/Elise - done
  * dissolved_oxygen standard_name > mole_concentration_of_dissolved_molecular_oxygen_in_sea_water - done
* 1d_graz_T:
  * all units -> mmol N m-3 s-1 - done
  * Microzoo, Mesozoo vs. Microzooplankton, Mesozooplankton - done
* 1d_prod_T:
  * all units -> mmol N m-3 s-1 - done
(SS-run-sets)


Fri 23-Sep-2022
^^^^^^^^^^^^^^^

Susan sent manager into restart loop with a syntax error in a live edit of next_workers module
trying to re-activate download_results for hindcast; fixed mangle of unmatched parens & square brackets and supervisord sorted manager out.
(SalishSeaCast)

Finished review and updates in field_defs and file_defs for nowcast-green.202111 output files.
Susan pulled them to optimum so that they were used for 11jun02 runs onward; inspected results files
and they look good.
(SS-run-sets)

Added SalishSeaCast-202111-salish model profile; PR#54 rebase-merged.
(Reshapr)


Sat 24-Sep-2022
^^^^^^^^^^^^^^^

Rode Zwift Academy workout #3.

Drove to White Rock to visit J&M.


Sun 25-Sep-2022
^^^^^^^^^^^^^^^

Goofed off.

Walked to English Bay overlook.


Week 39
-------

Mon 26-Sep-2022
^^^^^^^^^^^^^^^

Ran make_plots nowcast-green for more dates in 2017 to provide animations for discussion of 
2xrez deep water renewal.
Started extraction of month-averaged physics, biology & chemistry from 202111 hour-averaged
results:
* created extraction YAML configs in /results2/SalishSea/month-avg-202111/
* jun02 physics:
  * time chunk size: 1; 523.1 s
  * time chunk size: 24; 214.9 s
    * TimeoutError
    * produces large chunk warning (faster than Becca's single point extraction!!)
  * time chunk size: 1 repeat; nowcast-dev started near end; 588.8 s
* increased dask worker memory limit from auto-default of 32G to 48G
* jun02 physics:
  * time chunk size: 1 repeat; nowcast-dev running; 546.8 s
  * time chunk size: 24 repeat; nowcast-dev running;  213.0 s
    * large chunk warning
* jun02 biology;
  * time chunk size: 24 repeat; nowcast-dev running;  715.5 s
    * large chunk warning
* jun02 chemisty;
  * time chunk size: 24 repeat; nowcast-dev running;  311.2 s
    * large chunk warning
* jul02
  * time chunk size: 24
  * nowcast-dev running
  * large chunk warning
  * physics: 307.1 s
  * biology: 606.6 s
  * chemistry: 321.5 s
* aug02
  * time chunk size: 24
  * nowcast-dev running
  * large chunk warning
  * physics: 276.7 s
  * biology: 643.2 s
  * nowcast-dev ended
  * chemistry: 292.3 s
* changed dask worker local-directory to /dev/shm
* sep02
  * time chunk size: 24
  * nowcast-dev not running
  * large chunk warning
  * physics: 231.4 s
  * biology: 508.2 s
  * chemistry: 272.9 s
* increased dask worker memory limit to 64G
* oct02
  * time chunk size: 24
  * nowcast-dev not running
  * large chunk warning
  * physics: 237.7 s
  * biology: 541.9 s
  * chemistry:  s
(Hindcast)

Group mtg; talked about 2xrez deep water renewal.
(MOAD)

Started work on EGBC firm practice requirements for 30sep:
* skimmed program webinar recording
* paid for training program but have to wait for access credentials
* downloaded sole practitioner PPMP template, read it, and started 43ravens version

Rode Zwift Academy workout #4.


Tue 27-Sep-2022
^^^^^^^^^^^^^^^

Continued work on EGBC firm practice requirements for 30sep:
* received PPMP training credentials
* Started training: see /media/doug/warehouse/43ravens/egbc/PPMP/2022/RegOfFirmsTraining.rst

Continued extraction of month-averaged physics, biology & chemistry from 202111 hour-averaged
results:
* nowcast-dev not running
* tested using salish_cluster config
* time chunk size: 24
* large chunk warnings
* invalid value in divide warnings
* nov02
  * physics: 237.7 s
  * biology: 541.9 s
  * chemistry: 255.7 s
* hard-coded memory_limit=None (unlimited) in core.extract.py
* dec02
  * physics: 237.5 s
  * biology: 545.6 s
  * chemistry: 278.9 s
* nowcast-dev running
* created month-average.sh script to run 3 extractions from 1 command
* jan03
  * Jose running 5x beaching sims
  * physics: 313.2 s
  * biology: 776.2 s
  * chemistry: 425.9 s
* adapted month-average.sh script to accept yyyy and mm from command-line
* reduced cluster to 3 workers w/ 4 threads each avoid over-committing salish cores
* feb03
  * Jose running 5x beaching sims
  * physics: 389.8 s
  * biology: 795.3 s
  * chemistry: 397.2 s
* mar03
  * Jose running 5x beaching sims
  * nowcast-dev finished
  * physics: 414.7 s
  * biology: 913.8 s
  * chemistry: 466.1 s
* nowcast-dev not running
* apr03
  * Jose running 5x beaching sims
  * physics: 304.5 s
  * biology: 679.9 s
  * chemistry: 340.0 s
* increased cluster to 6 workers w/ 4 threads each
* may03
  * Jose running 5x beaching sims
  * physics: 253.1 s
  * biology: 456.5 s
  * chemistry: 211.7 s
* created month_avg.py module to run 3 extraction for a specified month
* Jose's 5 beaching sims finished
* jun03
  * physics: 167.3 s (maybe biased due to file caching; extraction was repeated for testing)
  * biology: 414.4 s
  * chemistry: 209.8 s
(Hindcast)

Coffee chat w/ Raisha.


Wed 28-Sep-2022
^^^^^^^^^^^^^^^

Continued work on EGBC firm practice requirements for 30sep:
* Continued training: see /media/doug/warehouse/43ravens/egbc/PPMP/2022/RegOfFirmsTraining.rst

Passed month averaging processing over to Susan for the moment; failed for her w/ max memory use,
max swap, and exception re: failure to spill data to disk.
Resumed processing:
* nowcast-dev not running
* using salish_cluster config; 6 workers w/ 4 threads each
* time chunk size: 24
* hard-coded memory_limit=None (unlimited) in core.extract.py
* extractions run via month_avg.py module
* large chunk warnings
* invalid value in divide warnings
* jul03
  * physics: 163.2 s (maybe biased due to file caching; extraction was already run by Susan)
  * biology: 361.3 s
  * chemistry: 188.5 s
* aug03
  * physics: 164.7 s
  * nowcast-dev started
  * biology: 497.0 s
  * chemistry: 283.7 s
* nowcast-dev running
* sep03
  * physics: 231.6 s
  * biology: 495.7 s
  * chemistry: 260.2 s
* nowcast-dev finished
* increased cluster to 8 workers w/ 4 threads each
* oct03
  * physics: 184.1 s
  * biology: 356.7 s
  * chemistry: 196.3 s
(Hindcast)

Phys Ocgy seminar: Sam Stevens sub-surface drifters


Thu 29-Sep-2022
^^^^^^^^^^^^^^^

Continued work on EGBC firm practice requirements for 30sep:
* Finished training modules: see notes in
  /media/doug/warehouse/43ravens/egbc/PPMP/2022/RegOfFirmsTraining.rst
* determined that PPMP does not have to be submitted to EGBC, just needs to exist

Continued extraction of month-averaged physics, biology & chemistry from 202111 hour-averaged
results:
* nowcast-dev not running
* using salish_cluster config; 8 workers w/ 4 threads each
* time chunk size: 24
* hard-coded memory_limit=None (unlimited) in core.extract.py
* extractions run via month_avg.py module
* large chunk warnings
* invalid value in divide warnings
* nov03
  * physics: 224.4 s
  * reduced cluster to 6 workers w/ 4 threads each
  * biology: 484.3 s
  * chemistry: 203.3 s
* dec03
  * physics: 166.7 s
  * biology: 397.1 s
  * chemistry: 208.2 s
* nowcast-dev running
* jan04
  * physics: 267.3 s
  * biology: 583.1 s
  * chemistry: 283.0 s
* nowcast-dev finished
* Jose running 5x beaching sims
* feb04
  * physics: 229.1 s
  * biology: 486.5 s
  * chemistry: 196.1 s
(Hindccast)

Helped Cassidy w/ conda config in bash profile.

Coffee chat with Camryn.

Rode Zwift Academy workout #5.


Fri 30-Sep-2022
^^^^^^^^^^^^^^^

**Statutory Holiday** - Truth & Reconcilliation Day

Continued work on EGBC firm practice requirements for 30sep:
* completed taining course exam

Continued extraction of month-averaged physics, biology & chemistry from 202111 hour-averaged
results:
* nowcast-dev not running
* using salish_cluster config; 8 workers w/ 4 threads each
* time chunk size: 24
* hard-coded memory_limit=None (unlimited) in core.extract.py
* extractions run via month_avg.py module
* large chunk warnings
* invalid value in divide warnings
* mar04
  * physics: 213.0 s
  * biology: 377.0 s
  * chemistry: 172.9 s
* nowcast-dev running
* apr04
  * physics: 300.0 s
  * biology: 429.6 s
  * chemistry: 208.7 s
* nowcast-dev finished
* may04
  * physics: 185.8 s
  * biology: 363.4 s
  * chemistry: 182.0 s
(Hindccast)

Investigated dependabot alert re: critical arbitrary code execution vulnerability in joblib
(CVE-2022-21797):
* used ``mama repoquery whoneeds joblib`` to learn that it is a dep for scikit-learn
* worked up the deps tree:
  * joblib -> scikit-learn -> mapclassify -> geopandas
  * geopandas is there because moad_tools has it as a dep for random_oil_spills.py
* no PR from dependabot yet
(SalishSeaNowcast)

Email from Derek White at port authority re: missing hours in depth-averaged currents dataset;
suspect it is a glitch in forecast2 processing.
(SalishSeaCast)


October
=======

Sat 1-Oct-2022
^^^^^^^^^^^^^^

Rode Salish Trail, Midtown, Cypress loop
(22 km)

Continued extraction of month-averaged physics, biology & chemistry from 202111 hour-averaged
results.
(Hindcast)


Sun 2-Oct-2022
^^^^^^^^^^^^^^

Sore back after yesterday's ride.

Continued extraction of month-averaged physics, biology & chemistry from 202111 hour-averaged
results:
* updated conda env prior to jan05 to try to reproduce the memory explosion issue that Susan had;
  today's pkg vesions are different to Susan's (see below)
* nowcast-dev not running
* using salish_cluster config; 8 workers w/ 4 threads each
* time chunk size: 24
* hard-coded memory_limit=None (unlimited) in core.extract.py
* extractions run via month_avg.py module
* large chunk warnings
* invalid value in divide warnings
* jan05
  * physics: 188.1 s
  * biology: 359.6 s
  * chemistry: 155.7 s
* feb05
(Hindcast)

Squash-merged dependabot PRs re: critical arbitrary code execution vulnerability in joblib
(CVE-2022-21797):
* SalishSeaNowcast
* moad_tools
(MOAD)

Created issue #55 re: adding memory_limit handling to cluster config; default to auto.
Investigated Susan's memory blow-up using Reshapr for month-avg on Wed:
* only significant difference in envs is dask 2022-9.0 in my env vs. 2022.9.1 in Susan's
* changelogs for dask and distributed don't reveal anything obvious
* 2022.9.2 was released on 30-Sep
* updated my env:
  - dask         2022.9.0  pyhd8ed1ab_0             installed                      
  + dask         2022.9.2  pyhd8ed1ab_0             conda-forge/noarch          6kB
  - dask-core    2022.9.0  pyhd8ed1ab_0             installed                      
  + dask-core    2022.9.2  pyhd8ed1ab_0             conda-forge/noarch        870kB
  - distributed  2022.9.0  pyhd8ed1ab_0             installed                      
  + distributed  2022.9.2  pyhd8ed1ab_0             conda-forge/noarch        761kB
  - netcdf4         1.6.0  nompi_py310h55e1e36_102  installed                      
  + netcdf4         1.6.1  nompi_py310h55e1e36_100  conda-forge/linux-64     Cached
  - xarray       2022.6.0  pyhd8ed1ab_1             installed                      
  + xarray       2022.9.0  pyhd8ed1ab_0             conda-forge/noarch        721kB
(Reshapr)


Week 40
-------

Mon 3-Oct-2022
^^^^^^^^^^^^^^

Continued extraction of month-averaged physics, biology & chemistry from 202111 hour-averaged
results:
* nowcast-dev not running
* using salish_cluster config; 8 workers w/ 4 threads each
* time chunk size: 24
* hard-coded memory_limit=None (unlimited) in core.extract.py
* extractions run via month_avg.py module
* large chunk warnings
* invalid value in divide warnings
* mar05
  * exception: ``OSError: [Errno -51] NetCDF: Unknown file format: b'/results2/SalishSea/nowcast-green.202111/27mar05/SalishSea_1h_20050327_20050327_grid_T.nc'``
* success on retry
* nowcast-dev not running
* successfully tested worker memory limit from cluster config re: issue #55 and PR#56
* apr05
  * sporadic exceptions: ``RuntimeError: NetCDF: Not a valid ID``
  * success on retries
(Hindcast)

Weekly group mtg; see whiteboard.
(MOAD)

Worked on issue #55 re: worker memory limit from cluster config; tested in use for hindcast month
averages.
(Reshapr)

Ran /results2/SalishSea/month-avg.201905/month-average.sh script on salish to generated 2019-05 
files for September.
Symlinked today's turbidity forcing to last good obs of 16jul; hoping to avoid 
"symlink chain too long" failure; limit appears to be 40 chained symlinks which would have 
happened in a couple of days.
(SalishSeaCast)

Rode Zwift Academy workout #6.


Tue 4-Oct-2022
^^^^^^^^^^^^^^

Worked at ESB while Rita was at home.

Finished work on issue #55 re: worker memory limit from cluster config; rebase-merged PR#56
(Reshapr)

Continued extraction of month-averaged physics, biology & chemistry from 202111 hour-averaged
results:
* using salish_cluster config; 8 workers w/ 4 threads each
* time chunk size: 24
* hard-coded memory_limit=None (unlimited) in core.extract.py
* extractions run via month_avg.py module
* large chunk warnings
* invalid value in divide warnings
* nowcast-dev running
* jun05
* jul05
  * chemistry failed with: ``RuntimeError: NetCDF: Not a valid ID``
  * added month_avg.py module CLI to specify dataset(s) to process
  * chemistry succeeded on retry
* pulled PR#56 re: memory_limit control from cluster config
* changed salish_cluster to use memory_limit=None
(Hindcast)

Updated conda env on khawla.
Changed docs build to use ubuntu-22.04.
Added sphinx-notfound-page to docs.
Created issue #112 re: Derek White's report of present day missing from ERDDAP depth-averaged 
currents dataset.
Experimented with GitHub-driven workflow to get to PyCharm task for work on issue #112:
* used GH Development sidebar element in issue to create branch; name was sensible, though I 
  editted it some; GHA workflows were triggered - surprising!; branch was auto-linked to issue;
  expect that PR will be too
* pulled new issue112 branch in to local clone w/ Ctrl-T in PyCharm
* used context menu to switch to issue112 branch in PyCharm
* created task for issue112 work in PyCharm; it auto-offered to use expected branch
Mostly modernized update_forecast_datasets unit tests; created PR#113; still a few @patch decorators remain
where tests assert on things like Mock.call_arg_list.
Started tracing ``update_forecast_datasets nemo forecast2 --run-date 2020-10-03``
(SalishSeaNowcast)


Wed 5-Oct-2022
^^^^^^^^^^^^^^

Continued work on issue #112 and PR#113 re: Derek White's report of present day missing 
from ERDDAP depth-averaged currents dataset.
* examined /results/SalishSea/rolling-forecasts/nemo in detail because NEMO runs are late starting
  today
    * 05oct22/CHS_currents.nc is MIA; is should have been constructed from 1st 24 hours of 
      /results/SalishSea/forecast.201905/04oct22/CHS_currents.nc
* traced ``update_forecast_datasets nemo forecast2 --run-date 2020-10-04``
* found and fixed bug
* improved exlusion of files that we don't publish forecast datasets of to ERDDAP
* rebase-merged PR#113 and closed issue #112
* email Derek to inform him of resolution
collect_weather 12 didn't finish:
* investigation:
  * no bad messages in log
  * 524 of 576 files downloaded
  * missing files in hours 001 and 035-048
  * sent email to Sandrine at ~11:30; she replied that the issue is known and analysts are working 
    on it
  * still no files at 16:45
    * download_weather 18 2.5km
    * download_weather 00 1km
    * download_weather 12 1km
  * I was decieved! all files except 001/PRMSL came in by 15:15
* recovery started at ~18:45:
  * kill collect_weather 12
  * collect_weather 00 2.5km
  * symlink 06/007/PRMSL as 12/001/PRMSL
  * collect_NeahBay_ssh 06
  * grib_to_netcdf nowcast+
  * download_live_ocean
* run_NEMO_agrif failed with 
  ``paramiko.ssh_exception.SSHException: Error reading SSH protocol banner``
(SalishSeaNowcast)


Thu 6-Oct-2022
^^^^^^^^^^^^^^

Backfill nowacst-agrif:
  wait for run to fail
  make_forcing_links orcinus nowcast-agrif 2022-10-05
  make_forcing_links orcinus nowcast-agrif 2022-10-06
download_results orcinus nowcast-agrif 2022-10-06 failed; no explanation; success on re-run
(SalishSeaNowcast)

Continued extraction of month-averaged physics, biology & chemistry from 202111 hour-averaged
results:
* using salish_cluster config; 8 workers w/ 4 threads each, memory_limit=None
* time chunk size: 24
* extractions run via month_avg.py module
* large chunk warnings
* invalid value in divide warnings
* aug05
  * failed due to no 31aug05 dir/files; Susan realized that she messed up the restart of the 
    hindcast after the mystery fail on Tue and left out 31aug05; restart again...
* aug05
(Hindcast)

Finished work on PR#53 re: 2xrez model profile and physics extraction:
* rebased SSC-2xrez branch on to main and resolved Conflicts
* buffed extract_ONC_SCVIP_physics_hour_avg.yaml; stashed version w/ regular resolution values 
  in scratch_5.yaml
* wrote docs/examples/ section
* conflict mess when I rebased SSC-2xrez on to main; only way I could resolve was to merge SSC-2xrez
  into main locally; that closed PR#53
(Reshapr)

Rode Zwift Academy Finish Line Ride.


Fri 7-Oct-2022
^^^^^^^^^^^^^^

Teams mtg w/ Susan and Nancy & Jared Penney at DFO NAFC re: adapting SOG model to stn 27 off
Cape Spear.
(SOG)

Continued extraction of month-averaged physics, biology & chemistry from 202111 hour-averaged
results:
* using salish_cluster config; 8 workers w/ 4 threads each, memory_limit=None
* time chunk size: 24
* extractions run via month_avg.py module
* large chunk warnings
* invalid value in divide warnings
* sep05
* oct05
  * biology failed with ``Exception: "OSError(-51, 'NetCDF: Unknown file format')"``
  * success on retry
* nov05
(Hindcast)

Drove to White Rock for Thanksgiving dinner w/ J&M and M&J.


Sat 8-Oct-2022
^^^^^^^^^^^^^^

Installed head unit, light & power meter pedals on Pico and power meter pedals on Gunnar.

Rode hill repeats on 8th Ave to test power meter pedals.
(9 km)


Sun 9-Oct-2022
^^^^^^^^^^^^^^

Rode Iona, Steeveston, south dyke, 5 Rd, 6 Rd loop with Cassidy.
(68 km)

Continued extraction of month-averaged physics, biology & chemistry from 202111 hour-averaged
results:
* using salish_cluster config; 8 workers w/ 4 threads each, memory_limit=None
* time chunk size: 24
* extractions run via month_avg.py module
* large chunk warnings
* invalid value in divide warnings
* dec05 through sep06
(Hindcast)


Week 41
-------

Mon 10-Oct-2022
^^^^^^^^^^^^^^^

**Statutory Holiday** - Thanksgiving Day

Continued extraction of month-averaged physics, biology & chemistry from 202111 hour-averaged
results:
* using salish_cluster config; 8 workers w/ 4 threads each, memory_limit=None
* time chunk size: 24
* extractions run via month_avg.py module
* large chunk warnings
* invalid value in divide warnings
* may06 through nov06
(Hindcast)


Tue 11-Oct-2022
^^^^^^^^^^^^^^^

Continued extraction of month-averaged physics, biology & chemistry from 202111 hour-averaged
results:
* using salish_cluster config; 8 workers w/ 4 threads each, memory_limit=None
* time chunk size: 24
* extractions run via month_avg.py module
* large chunk warnings
* invalid value in divide warnings
* dec06
  * chemistry failed w/ invalid NetCDF ID error; sucess on retry
* jan07
* feb07
  * chemistry failed w/ NetCDF unknown file format; sucess on retry
* mar07
(Hindcast)

Codebase maintenance:
* updated dev env on khawla
* added language to GHA CodeQL job status Slack messages so it doesn't look like 2 identical 
  workflow jobs; rebase-merged PR#21
* added pip -e install to conda env descriptions; rebase-merged PR#22
* updated rtd build:
  * chg to use ubuntu-22.04
  * add rtd-installed pkgs to env description
  * add sphinx-notfound-page extension
  * fix warning re: language setting in conf.py
  * rebase-merged PR#23
* fixed default branch setting on rtd so that docs build; last build was ~11 months ago :grimace:
* updated page footer & SalishSeaCast branding; rebase-merged PR#24
  * Fixed page footer:
      © Copyright 2013 – present SalishSeaCast Project contributors and The University of British Columbia 
  * got rid of _copyright_year_range() request method
* Created 22.1 release on GitHub.
* Bumped version to 22.2.dev0.
* Updated prod env on skookum.
* fixed in-press annotation on Olson et al (2020); rebase-merged PR#25
* added Jarníková et al (2021) cluster analysis paper to pubs pg; rebase-merged PR#26
* added Jarníková et al (2022) SKOG carbonate chemistry model paper to pubs pg; rebase-merged PR#27
(salishsea-site)

Updated khawla minecraft to iris-1.4 and lithium-0.8.3.


Wed 12-Oct-2022
^^^^^^^^^^^^^^^

Continued extraction of month-averaged physics, biology & chemistry from 202111 hour-averaged
results:
* using salish_cluster config; 8 workers w/ 4 threads each, memory_limit=None
* time chunk size: 24
* extractions run via month_avg.py module
* large chunk warnings
* invalid value in divide warnings
* apr07 through jul07
(Hindcast)

Added Jarnikova 2021 & 2022 to SalishSeaCast/docs/CITATION.rst; GitHub
improved semantic markup of publication years and journal names.
Fixed build warnings re: AMM12-BDY-analysis.ipynb.
(SalishSeaCast docs)

Toured repos to re-enable scheduled GHA workflows that were disabled due to lack of activity.

Updated khawla to PyCharm 2022.2.3.

Resolved issue #37 re: KeyError for variable not in variables group:
* branch: issue37-keyerror-for-var-not-in-vars-group
* PR#57; rebase-merged
(Reshapr)


Thu 13-Oct-2022
^^^^^^^^^^^^^^^

Power failure at UBC caused name resolution failures and manager crashes in Slack notifications of
hindcast run completions; see 43ravens/NEMO_Nowcast issue #15.
make_ssh_files was unsuccessful to due missing Neah Bay 12oct obs; triggered persistences symlink
race condition during upload_forcing forecast2; forecast2 runs skipped.
make_ssh_files was unsuccessful to due missing Neah Bay 12oct obs; triggered persistences symlink
race condition during upload_forcing nowcast+:
* recovery started at ~08:45:
  ln -s ../fcst/ssh_y2022m10d12.nc
  clear_checklist
  upload_forcing arbutus nowcast+
  upload_forcing optimum nowcast+
  upload_forcing orcinus nowcast+
  upload_forcing graham-dtn nowcast+
Started work on moving sea surface height fcst -> obs symlink when obs are missing into 
make_ssh_files:
* branch: symlink-fcst-as-obs
* traced through make_ssh_files in PyCharm debugger to understand it and to tweak config so that I 
  can run it on khawla without writing to skookum:/results/forcing/sshNeahBay/
* created PR#114
(SalishSeaCast)

Continued extraction of month-averaged physics, biology & chemistry from 202111 hour-averaged
results:
* using salish_cluster config; 8 workers w/ 4 threads each, memory_limit=None
* time chunk size: 24
* extractions run via month_avg.py module
* large chunk warnings
* invalid value in divide warnings
* aug07 through oct07
(Hindcast)

Created 43ravens/NEMO_Nowcast issue #15 re: name resolution failure in manager._slack_notification()
causing manager to crash.
(NEMO_Nowcast)

UBC-DFO modeling collaboration mtg; Susan re: SalishSeaCast bathymetry changes for 202111:
* bathy version is 202108
* this bathy is for 202111 runs
* changes:
  * physics:
    * daily rivers
    * coastal wave parameterization (slippery water)
    * new bathy
    * spin-up started w/ 2002 using climate downscaled atmos
    * fix OCB
    * fix GMLAM weights
  * biology:
    * fix Asselin filter
    * improve sinking
    * remove ciliates
    * retuned biology
    * new OBC for bio
    * fix chemistry OBC
* depth < 2m = 0m
* 2m < depth < 4m = 4m

Weekly project mtg.
Helped Raisha with R kernel issue in VS Code.
(Atlantis)


Fri 14-Oct-2022
^^^^^^^^^^^^^^^

Continued extraction of month-averaged physics, biology & chemistry from 202111 hour-averaged
results:
* using salish_cluster config; 8 workers w/ 4 threads each, memory_limit=None
* time chunk size: 24
* extractions run via month_avg.py module
* large chunk warnings
* invalid value in divide warnings
* nov07 through feb08
(Hindcast)

Continued work on moving sea surface height fcst -> obs symlink when obs are missing into 
make_ssh_files:
* branch: symlink-fcst-as-obs
* PR#114
* finally got something that appears to work; failed to create a unit test for ti though :-(
* pulled branch into prod on skookum for testing
* TODO:
  * Fix tests to work without access to /results (CI fails on GH, and locally w/o sshfs mount)
TLS cert for aquatic.pyr.ec.gc.ca expired today, so the Fraser buoy cronjob failure at 10:35
  was a ``Connection timed out``, but then it went back to ``invalid turbidity data:  NTU``
(SalishSeaCast)


Sat 15-Oct-2022
^^^^^^^^^^^^^^^

Minecraft Live

Continued work on moving sea surface height fcst -> obs symlink when obs are missing into 
make_ssh_files:
* branch: symlink-fcst-as-obs
* PR#114
* worked as expected in prod with normal obs from Neah Bay
make_forcing_links arbutus nowcast-green failed w/ 
``paramiko.ssh_exception.SSHException: Error reading SSH protocol banner``
* re-ran successfully at ~14:45
(SalishSeaCast)

Municipal Election


Sun 16-Oct-2022
^^^^^^^^^^^^^^^

Continued work on moving sea surface height fcst -> obs symlink when obs are missing into 
make_ssh_files:
* branch: symlink-fcst-as-obs
* PR#114
* apparently there were Neah Bay obs missing for 15oct at forecast2 time; symlink and critical log 
  message as expected
(SalishSeaNowcast)

Hindcast stopped due to name resolution failures and manager crashes in Slack notifications of
hindcast run completions; see 43ravens/NEMO_Nowcast issue #15.
(SalishSeaCast)

Continued extraction of month-averaged physics, biology & chemistry from 202111 hour-averaged
results:
* using salish_cluster config; 8 workers w/ 4 threads each, memory_limit=None
* time chunk size: 24
* extractions run via month_avg.py module
* large chunk warnings
* invalid value in divide warnings
* mar07 through sep08
(Hindcast)

Rode TFC Sunday D group ride on Zwift.

ESB power outage mid-afternoon.


Week 42
-------

Mon 17-Oct-2022
^^^^^^^^^^^^^^^

collect_weather 18 didn't finish yesterday
* investigation:
  * lots of name resolution failures in log between 16oct22 14:22 and 15:35
  * why was skookum DNS affected by ESB power outage???
  * 540 of 576 files downloaded
* recovery; started at ~09:15:
  * move /results/forcing/atmospheric/GEM2.5/GRIB/20221016/18/ aside
  * kill collect_weather 18
  * commands:
      download_weather 18 2.5km
      download_weather 00 1km --yesterday
        * failed due to files purged from server
      download_weather 12 1km --yesterday
      download_weather 00 2.5km
      download_weather 06 2.5km
      wait for forecast2 runs to finish
      download_weather 12 2.5km
      collect_weather 18 2.5km
Investigated why skookum is affected by ESB name server outages
* I thought that Henryk fixed that in Apr-2022 by adding fallbacks elsewhere on the network, 
  but skookum (18.04) now only has:
    137.82.49.124 == dhcp2.eoas.ubc.ca
* salish (18.04) has:
    nameserver 142.103.43.16
    nameserver 142.103.250.10
    nameserver 137.82.1.2

    (/home/dlatorne/conda_envs/reshapr) month-avg.202111$ nslookup 142.103.43.16
    16.43.103.142.in-addr.arpa      name = udc-ad-dc.eoas.ubc.ca.

    (/home/dlatorne/conda_envs/reshapr) month-avg.202111$ nslookup 142.103.250.10
    10.250.103.142.in-addr.arpa     name = dhcp2.eoas.ubc.ca.

    (/home/dlatorne/conda_envs/reshapr) month-avg.202111$ nslookup 137.82.1.2
    2.1.82.137.in-addr.arpa name = ns-int-1.netcom.ubc.ca.
* note that dhcp2.eoas.ubc.ca has many IP addresses:
    (base) ~$ dig dhcp2.eoas.ubc.ca

    ; <<>> DiG 9.18.1-1ubuntu1.2-Ubuntu <<>> dhcp2.eoas.ubc.ca
    ;; global options: +cmd
    ;; Got answer:
    ;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 16006
    ;; flags: qr rd ra; QUERY: 1, ANSWER: 7, AUTHORITY: 0, ADDITIONAL: 1

    ;; OPT PSEUDOSECTION:
    ; EDNS: version: 0, flags:; udp: 65494
    ;; QUESTION SECTION:
    ;dhcp2.eoas.ubc.ca.		IN	A

    ;; ANSWER SECTION:
    dhcp2.eoas.ubc.ca.	1095	IN	A	142.103.250.31
    dhcp2.eoas.ubc.ca.	1095	IN	A	137.82.22.4
    dhcp2.eoas.ubc.ca.	1095	IN	A	137.82.49.124
    dhcp2.eoas.ubc.ca.	1095	IN	A	142.103.250.10
    dhcp2.eoas.ubc.ca.	1095	IN	A	137.82.49.88
    dhcp2.eoas.ubc.ca.	1095	IN	A	137.82.23.5
    dhcp2.eoas.ubc.ca.	1095	IN	A	137.82.107.4

    ;; Query time: 7 msec
    ;; SERVER: 127.0.0.53#53(127.0.0.53) (UDP)
    ;; WHEN: Mon Oct 17 11:12:10 PDT 2022
    ;; MSG SIZE  rcvd: 158
* after a couple of hours of research...
* Updated skookum /etc/network/interfaces em1 stanza with line:
    dns-nameservers 142.103.43.16 142.103.250.10 137.82.1.2
  hoping that will ensure that /run/resolvconf/resolv.conf is correctly set in future
* did on skookum:
    sudo systemctl restart resolvconf
  and confirmed that DNS servers have been updated with:
    systemd-resolve --status
* Updated salish /etc/network/interfaces eth1 stanza with line:
    dns-nameservers 142.103.43.16 142.103.250.10 137.82.1.2
  hoping that will ensure that /run/resolvconf/resolv.conf is correctly set in future
* didn't restart resolvconf service on salish because systemd-resolve --status shows that it 
  (somehow) has the correct name servers configured
(SalishSeaCast)

Continued extraction of month-averaged physics, biology & chemistry from 202111 hour-averaged
results:
* using salish_cluster config; 8 workers w/ 4 threads each, memory_limit=None
* time chunk size: 24
* extractions run via month_avg.py module
* large chunk warnings
* invalid value in divide warnings
* oct08 through jan09
Split hindcast results into spinup and prod directories:
* renamed nowcast-green.202111/ to spinup.202111/
* created new nowcast-green.212111/
* moved 07, 08, and 09 results dirs from spinup.202111/ to nowcast-green.202111/
(Hindcast)


Tue 18-Oct-2022
^^^^^^^^^^^^^^^

Worked at ESB while Rita was at home.

Continued extraction of month-averaged physics, biology & chemistry from 202111 hour-averaged
results:
* using salish_cluster config; 8 workers w/ 4 threads each, memory_limit=None
* time chunk size: 24
* extractions run via month_avg.py module
* large chunk warnings
* invalid value in divide warnings
* feb09 through may09
Started archiving spin-up month tarballs to graham in tmux session (202111-tarballs) on skookum.
(Hindcast)

Added note re: changing "remote.SSH.connectTimeout" setting value to 45 s to VS Code docs.
(MOAD)

Started Slack discussion w/ Susan about why there are month-avg.201905/ collections on both 
/results/ and /results2/, and which one ERDDAP should be looking at.
(ERDDAP)

Photoshoot for EOAS website photo.

Finished work on moving sea surface height fcst -> obs symlink when obs are missing into 
make_ssh_files:
* branch: symlink-fcst-as-obs
* PR#114
* refactored to get test suite to work without access to /results/ and added tests for new code
(SalishSeaNowcast)


Wed 19-Oct-2022
^^^^^^^^^^^^^^^

Continued extraction of month-averaged physics, biology & chemistry from 202111 hour-averaged
results:
* using salish_cluster config; 8 workers w/ 4 threads each, memory_limit=None
* time chunk size: 24
* extractions run via month_avg.py module
* large chunk warnings
* invalid value in divide warnings
* jun09 through sep09
Continued archiving spin-up month tarballs to graham in tmux session (202111-tarballs) on skookum.
(Hindcast)

Rebase-merged PR#114 re: moving sea surface height fcst -> obs symlink when obs are missing into 
make_ssh_files; pulled into production.
(SalishSeaCast)

Added release watches on the repos for the 5 GHA actions I use:
* actions/checkout
* conda-incubator/miniconda3
* 8398a7/action-slack
* github/codeql-action/init
* github/codeql-action/analyze

Worked on setting up UBC-MOAD/SOG-code-collab repo:
* worked in /media/doug/warehouse/MOAD on khawla
* hg cloned repo from /ocean/:
    hg clone ssh://smelt//ocean/sallen/hg_repos/SOG-code SOG-code-hg
* confirmed that HEAD of that clone is the version that we run in 
  /data/dlatorne/SOG-projects/SOG-code-bloomcast/ for bloomcast
* cloned https://github.com/frej/fast-export
* created a conda env to work in because python and mercurial installs need to be coordinated
  (got fail using system mercurial pkg with base env python)
    mamba create -n hg-fast-export python mercurial
* converted SOG-code-hg git repo:
    mkdir SOG-code-collab
    cd SOG-code-collab
    git init
    (hg-fast-export) SOG-code-collab$ ../fast-export/hg-fast-export.sh -r ../SOG-code-hg/
    git switch master
    git branch -m main  # change default branch name from master to main
* do my local git clone setups:
    git config --local --add user.email "dlatornell@eoas.ubc.ca"
    ln -s /home/doug/dotfiles/pop_os/khawla/githooks/rescuetime_commit_highlight.sh .git/hooks/post-commit
* TODO:
  * replace .hgignore with .gitignore
  * add LICENSE file
  * add README.md file
  * add CITATION file
  * discuss repo name w/ Susan
  * discuss absence of copyright notices w/ Susan
(SOG)

Started work w/ Susan on RAC application.


Thu 20-Oct-2022
^^^^^^^^^^^^^^^

Continued extraction of month-averaged physics, biology & chemistry from 202111 hour-averaged
results:
* using salish_cluster config; 8 workers w/ 4 threads each, memory_limit=None
* time chunk size: 24
* extractions run via month_avg.py module
* large chunk warnings
* invalid value in divide warnings
* oct09 through jan10
Continued archiving spin-up month tarballs to graham in tmux session (202111-tarballs) on skookum.
* mar03 spin-up tarball rsync failed
(Hindcast)

See 2022 and new 2023 work journals.
(Resilient-C)

Flu shot.

Weekly project mtg.
(Atlantis)

Updated GHA actions re: Node.js 12 and codeql-actions@v1 deprecations; rebase-merged PR#58.
Tagged v22.1 and published release of v22.1 on GitHub.
Bumped version to 22.2.dev0 for next dev cycle.
(Reshapr)

Discovered that GitHub CLI tool can query and enable workflows; it's also installable via conda :-)
Installed gh in conda env on khawla:
  mamba create -n github-cli gh  # just 1 package!
Query workflow statuses for a repo; e.g.
  gh -R SalishSeaCast/SalishSeaNowcast workflow list -a
(MOAD)


Fri 21-Oct-2022
^^^^^^^^^^^^^^^

First rainfall in weeks.

Continued extraction of month-averaged physics, biology & chemistry from 202111 hour-averaged
results:
* using salish_cluster config; 8 workers w/ 4 threads each, memory_limit=None
* time chunk size: 24
* extractions run via month_avg.py module
* large chunk warnings
* invalid value in divide warnings
* feb10 through apr10
Continued archiving spin-up month tarballs to graham in tmux session (202111-tarballs) on skookum.
* aug is missing from bash loop :-(
(Hindcast)

Toured GitHub repos w/ GHA actions to re-enable scheduled sphinx-linkcheck workflows 
that have been disabled due to 60d inactivity:
  for repo in docs SalishSeaNowcast SalishSeaCmd NEMO-Cmd salishsea-site; \
  do \
    echo ${repo}:; \
    gh -R SalishSeaCast/${repo} workflow list -a; \
    echo ""; \
  done

  for repo in docs moad_tools MoaceanParcels Reshapr; \
  do \
    echo ${repo}:; \
    gh -R UBC-MOAD/${repo} workflow list -a; \
    echo ""; \
  done

  gh -R SS-Atlantis/AtlantisCmd workflow list -a

  for repo in docs Make-MIDOSS-Forcing MOHID-Cmd WWatch3-Cmd; \
  do \
    echo ${repo}:; \
    gh -R MIDOSS/${repo} workflow list -a; \
    echo ""; \
  done
Created MOAD/gha-workflows-checker repo and intial implementation of script.
(MOAD)

Coffee/char w/ Jose.

Did ZRacing October Stage 3: Figure8 Reverse.


Sat 22-Oct-2022
^^^^^^^^^^^^^^^

Continued extraction of month-averaged physics, biology & chemistry from 202111 hour-averaged
results:
* using salish_cluster config; 8 workers w/ 4 threads each, memory_limit=None
* time chunk size: 24
* extractions run via month_avg.py module
* large chunk warnings
* invalid value in divide warnings
* may10
Continued archiving spin-up month tarballs to graham in tmux session (202111-tarballs) on skookum.
* cleaned up errors:
    rsync mar03, then deleted files
    month_avg aug02

* aug is missing from bash loop :-(
**redo aug02 aug03**
(Hindcast)

Drove to White Rock to visit J&M.


Sun 23-Oct-2022
^^^^^^^^^^^^^^^

Continued extraction of month-averaged physics, biology & chemistry from 202111 hour-averaged
results:
* using salish_cluster config; 8 workers w/ 4 threads each, memory_limit=None
* time chunk size: 24
* extractions run via month_avg.py module
* large chunk warnings
* invalid value in divide warnings
* jun10 through dec10
Continued archiving spin-up month tarballs to graham in tmux session (202111-tarballs) on skookum.
* cleaned up errors:
    month_avg aug03
(Hindcast)

Discovered that code runs stopped sometime yesterday:
* investigation:
  * name resolution failure in ending of watch_NEMO nowcast-green on Fri appears to have stopped
    everything
  * forecast2/21oct22 ran successfully early on 22oct22, but watcher was blocked by stalled watcher 
    from nowcast-green/21oct22; no download
  * nowcast-blue/22oct22 ran successfully on 22oct22, but watcher was blocked by stalled watcher 
    from nowcast-green/21oct22; no download
* spent a bunch of time trying to get skookum to have more than the unreliable 137.82.49.124
  but can't get systemd-resolve --status to show any update
  * ended up adding ``44.237.180.172  hooks.slack.com`` to /etc/hosts
* recovery:
    download_results arbutus nowcast-green --run-date 2022-10-21
    pkill -f watch_NEMO  # kill stalled worker on arbutus
    make_forcing_links salish nowcast+ --shared-storage --run-date 2022-10-21
    launch_remote_worker arbutus make_ww3_wind_file "arbutus forecast --run-date 2022-10-21"
    launch_remote_worker arbutus make_ww3_current_file "arbutus forecast --run-date 2022-10-21"
    download_results arbutus nowcast --run-date 2022-10-22
    wait for wwatch3 runs to finish
    make_forcing_links arbutus ssh --run-date 2022-10-22
    # no messages from watch_NEMO on arbutus
    supervisorctl restart log_aggregator
    # upload_forcing turbidity failed to all hosts due to no riverTurbDaily2_y2022m10d22.nc file
    pushd /results/forcing/rivers/river_turb/ 
    ln -s /results/forcing/rivers/river_turb/riverTurbDaily2_y2022m10d21.nc riverTurbDaily2_y2022m10d22.nc
    upload_forcing arbutus turbidity --run-date 2022-10-22
    upload_forcing orcinus turbidity --run-date 2022-10-22
    upload_forcing optimum turbidity --run-date 2022-10-22
    upload_forcing graham-dtn turbidity --run-date 2022-10-22
    wait for nowcast-green to finish
    launch_remote_worker arbutus make_ww3_wind_file "arbutus forecast --run-date 2022-10-22"
    launch_remote_worker arbutus make_ww3_current_file "arbutus forecast --run-date 2022-10-22"
    wait for wwatch3 runs to finish
    make_forcing_links arbutus nowcast+ --run-date 2022-10-23
    wait for x2 nowcast run to fail
    launch_remote_worker arbutus make_fvcom_boundary "arbutus x2 nowcast --run-date 2022-10-22"
    wait for fvcom runs to finish
(SalishSeaCast)


Week 43
-------

Mon 24-Oct-2022
^^^^^^^^^^^^^^^

Continued recovery from automation failure:
  wait for x2 nowcast run to fail
  launch_remote_worker arbutus make_fvcom_boundary "arbutus x2 nowcast --run-date 2022-10-23"
  wait for nowcast-dev run to fail
  make_forcing_links salish nowcast+ --shared-storage --run-date 2022-10-22
  make_forcing_links salish nowcast+ --shared-storage --run-date 2022-10-23
  make_forcing_links salish nowcast+ --shared-storage --run-date 2022-10-24
  wait for r12 nowcast run to finish at ~21:00
  launch_remote_worker arbutus make_fvcom_boundary "arbutus x2 nowcast --run-date 2022-10-24"
(SalishSeaCast)

Continued extraction of month-averaged physics, biology & chemistry from 202111 hour-averaged
results:
* using salish_cluster config; 8 workers w/ 4 threads each, memory_limit=None
* time chunk size: 24
* extractions run via ``/results2/SalishSea/month-avg.202111/month_avg.py`` module
* large chunk warnings
* invalid value in divide warnings
* jan11 through mar11
Continued archiving spin-up month tarballs to graham in tmux session (202111-tarballs) on skookum;
finished 2004.
**Susan realized that there is an error in the 2007-onward boundary conditions configuration**
Prep to restart hindcast from 01jan07:
* empty ``/results2/SalishSea/nowcast-green.202111/``
* deleted ``/results2/SalishSea/month-avg.202111/SalishSeaCast_1m_*_200[789]*.nc``
* deleted ``/results2/SalishSea/month-avg.202111/SalishSeaCast_1m_*_201[01]*.nc``
(Hindcast)

Continued work on RAC application.

Python 3.11.0 released.


Tue 25-Oct-2022
^^^^^^^^^^^^^^^

graham down for maintenance

Continued work on RAC application.

nowcast-x2/25oct22 launched while nowcast-r12/24oct22 still had ~12m to run; competitive Struggled
until ~11:30.
download_weather 1km 12 failed due to missing file
``001/CMC_hrdps_west_DLWRF_SFC_0_rotated_latlon0.009x0.009_20221025T12Z_P001-00.grib2``
(SalishSeaCast)

FAL estate work:
* liquidated BCE shares

Continued extraction of month-averaged physics, biology & chemistry from 202111 hour-averaged
results:
* using salish_cluster config; 8 workers w/ 4 threads each, memory_limit=None
* time chunk size: 24
* extractions run via ``/results2/SalishSea/month-avg.202111/month_avg.py`` module
* large chunk warnings
* invalid value in divide warnings
* jan07 through apr07
No spin-up month tarball archiving today due to graham maintenance.
(Hindcast)

Python 3.11.0 available from conda-forge.
Started watching conda-forge packages migration at https://conda-forge.org/status/#python311

Updated GHA actions re: Node.js 12 deprecation; rebase-merged PR#37.
Updated docs build system; rebase-merged PR#38.
Created draft PR#39 to start migration to Python 3.11; added 3.11 to GHA CI version matrix.
* should be able to test periodically with ``gh workflow run CI --ref py311``
CI 3.11 workflow failed with:
``package pyyaml-5.3-py36h97a6639_1 requires python_abi 3.6 *_pypy36_pp73, but none of the 
providers can be installed``
(NEMO-Cmd)


Wed 26-Oct-2022
^^^^^^^^^^^^^^^

Continued work on RAC application.

Continued extraction of month-averaged physics, biology & chemistry from 202111 hour-averaged
results:
* using salish_cluster config; 8 workers w/ 4 threads each, memory_limit=None
* time chunk size: 24
* extractions run via ``/results2/SalishSea/month-avg.202111/month_avg.py`` module
* large chunk warnings
* invalid value in divide warnings
* may07 through aug07
Resumed spin-up month tarball archiving after graham maintenance; started 2005.
Discoverd that /nearline was not mounted on graham-dtn; rectified after email to support;
started rsync-ing tarballs that were skipped: jan05, feb05
(Hindcast)

Tried to run CI workflow with ``gh workflow run CI --ref py311`` and it failed with:
``could not create workflow dispatch event: HTTP 422: Workflow does not have 'workflow_dispatch'
trigger (https://api.github.com/repos/SalishSeaCast/NEMO-Cmd/actions/workflows/858353/dispatches)``
Ran workflow from browser; failed with:
``package pyyaml-6.0-py311hd4cff14_5 requires python_abi 3.11.* *_cp311, but none of the providers 
can be installed``
Added workflow_dispatch trigger to CI workflow in PR#37.
(NEMO-Cmd)

``*.eos.ubc.ca`` TLS cert expired this morning; opened helpdesk ticket.
download_weather 1km 00 and download_weather 1km 12 failed due to missing files
(SalishSeaCast)

conda-forge Python 3.11 migration stopped in the evening; no idea why.


Thu 27-Oct-2022
^^^^^^^^^^^^^^^

Continued work on RAC application.

Continued extraction of month-averaged physics, biology & chemistry from 202111 hour-averaged
results:
* using salish_cluster config; 8 workers w/ 4 threads each, memory_limit=None
* time chunk size: 24
* extractions run via ``/results2/SalishSea/month-avg.202111/month_avg.py`` module
* large chunk warnings
* invalid value in divide warnings
* sep07 through nov07
Continued spin-up month tarball archiving after graham maintenance; finished 2005, started 2006.
Finished rsync-ing skipped tarballs: mar05, apr05
(Hindcast)

conda-forge Python 3.11 migration resumed.

Ran py311 CI workflow from browser; failed again with:
  ``package pyyaml-6.0-py311hd4cff14_5 requires python_abi 3.11.* *_cp311, but none of the providers can be installed``
Odd, because in the terminal:
  ``mamba create -n foo python=3.11 arrow attrs cliff f90nml pip pyyaml black pytest pytest-cov sphinx sphinx_rtd_theme sphinx-notfound-page``
fails with:
  ``package cliff-2.9.1-py_0 requires cmd2 >=0.6.7, but none of the providers can be installed``
(NEMO-Cmd)

Charles renewed cert and replied on last year's ticket: https://helpdesk.eoas.ubc.ca/tickets/ABXO-3634-CRWD

AAPS AGM:
* United Way: Kelli Kadokawa
* mtg chair: Afsaneh Sharif
* nativeland.ca interactive map
* Strategic plan:
  * EDI working group
  * comms & engagement working group
  * services & support working group
* collective bargaining
  * priorities:
    * pay re: inflation, general increase, COLA
    * flexibile work arrangements
      * subsidized transit passes
    * paid leave for culture; 5 days
    * entrench benefits
    * additional hours
  * questions
* advocacy
  * >1100 cases last year, increasing complexity
* staff introductions
* financials
* board election results
* education awards
* adjournment; recording stopped
* general Q&A:

Tried to explain salishsea-site figure machanics to Tereza on Slack.

Weekly mtg.
(Atlantis)


Fri 28-Oct-2022
^^^^^^^^^^^^^^^

Continued extraction of month-averaged physics, biology & chemistry from 202111 hour-averaged
results:
* using salish_cluster config; 8 workers w/ 4 threads each, memory_limit=None
* time chunk size: 24
* extractions run via ``/results2/SalishSea/month-avg.202111/month_avg.py`` module
* large chunk warnings
* invalid value in divide warnings
* dec07 through mar08
Finished spin-up month tarball archiving.
(Hindcast)

Added model profile description to info sub-command output and to all model profiles:
* branch: info-description
* PR#59; rebase-merged
Started work on adding API for reshapr.core.extract():
* not as simple as I expected...
* branch: api_v1
* PR#60
(Reshapr)


Sat 29-Oct-2022
^^^^^^^^^^^^^^^

Pulled api_v1 branch on salish to test in context of hindecast month-averages; 
(Reshapr)

Continued extraction of month-averaged physics, biology & chemistry from 202111 hour-averaged
results:
* using salish_cluster config; 8 workers w/ 4 threads each, memory_limit=None
* time chunk size: 24
* extractions run via ``/results2/SalishSea/month-avg.202111/month_avg.py`` module
* large chunk warnings
* invalid value in divide warnings
* apr08 through jul08
Started hindcast month tarball archiving.
(Hindcast)


Sun 30-Oct-2022
^^^^^^^^^^^^^^^

Continued extraction of month-averaged physics, biology & chemistry from 202111 hour-averaged
results:
* using salish_cluster config; 8 workers w/ 4 threads each, memory_limit=None
* time chunk size: 24
* extractions run via ``/results2/SalishSea/month-avg.202111/month_avg.py`` module
* large chunk warnings
* invalid value in divide warnings
* aug08 through nov08
Continued hindcast month tarball archiving.
(Hindcast)

Experimented with editable install of MOAD dep pkgs in env decriptions; 
i.e. in SalishSeaCmd/envs/environment-dev:
    # editable install of NEMO-Cmd package
    - --editable git+https://github.com/SalishSeaCast/NEMO-Cmd.git/#egg=NEMO-Cmd
    # editable install of SalishSeaCmd package
    - --editable ../
Result was a clone of NEMO-Cmd in SalishSeaCmd/envs/src/ and successful installation.
(MOAD)

Started thinking about worker to calculate day-averages and month-average datasets as part of 
post-processing of hindcast/nowcast runs:
* possible names:
  * make_averaged_dataset
  * resample_dataset
* uses:
  * after every download_results, calculate day-averaged biology, chemistry, physics datasets 
    from hour-averaged
  * after month-end download_results, calculate month-averaged biology, chemistry, physics datasets 
    from hour-averaged or day-averaged???
* need Reshapr.api.v1.extract_netcdf()
* args:
  * Resphapr extraction config
    * file path, or config key, or derive from other args:
      * run-type; i.e. nowcast, hindcast, spinup
        * for choice of Reshapr extraction config
      * resampling interval
  * run-date
    * for backfilling
  * resampling interval; i.e. day, month
    * to set Reshapr start/end date
    * maybe involved in choice of Reshapr extraction config
* run worker on salish to take advantage of its cores and big RAM
(SalishSeaNEMO)

Finished RAC application.





TODO:
* SalishSeaCast/docs:
  * replace broken links:
    * http://pages.physics.cornell.edu/~myers/teaching/ComputationalMethods/
    * http://pages.physics.cornell.edu/~myers/teaching/ComputationalMethods/LectureNotes/Intro_to_Python.pdf
    * https://www.pac.dfo-mpo.gc.ca/science/oceans/data-donnees/search-recherche/profiles-eng.asp
    * https://www.waterlevels.gc.ca/eng/data#s2
    * https://www.westgrid.ca/support/systems/orcinus


TODO:
* update GHA actions to Node.js 16 versions; warnings now, no set final date as of 12oct22:
  * actions/checkout@v2 -> actions/checkout@v3
  * conda-incubator/setup-miniconda - no node.js 16 version available yet
  * 8398a7/action-slack@v3 - did node.js 16 as micro version bump
  * codecov/codecov-action@v1 -> codecov/codecov-action@v3
* more deprecation warnings in SalishSeaNEMO re: `set-output` and `save-state`
  * coming from conda-incubator/setup-miniconda@v2
* confirm that we are using:
  * github/codeql-action/init@v2
  * github/codeql-action/analyze@v2 (probably using v1 in some repos)
  * EOL date for v1 is Dec-2022
* commit messages:
  * Bump GHA actions/checkout to v3

    re: Node.js 12 actions deprecation. See:
    https://github.blog/changelog/2022-09-22-github-actions-all-actions-will-begin-running-on-node16-instead-of-node12/

  * Bump GHA codecov/codecov-action to v3

    re: Node.js 12 actions deprecation. See:
    https://github.blog/changelog/2022-09-22-github-actions-all-actions-will-begin-running-on-node16-instead-of-node12/

  * Bump GHA github/codeql-action/analyze to v2

    re: CodeQL Action v1 deprecation. See:
    https://github.blog/changelog/2022-04-27-code-scanning-deprecation-of-codeql-action-v1/


Becuase I can never remember how to get a git feature branch that I set asdie back into working
state:
* ref: https://www.atlassian.com/git/tutorials/merging-vs-rebasing
* git switch feature
* git rebase main
* In PyCharm > Git > Log context menu "Rebase 'feature' onto 'main'"
* **BUT** if the changes in the feature branch overlap files in main, it's possible that
  a merge will be required




TODO:
  EGBC firm registration next steps by 30-Sep
    * practice mgmt plan
  2022-2023 CE plan




I'm interested in having our windows cleaned, inside and outside. We live in a 3 unit triplex in Kitsilano, but the service I'm looking for is just for our unit.

We have 2 floors. On the ground floor there are 6 windows and a set of patio doors with a window above them. 3 of those windows, and the patio doors have screens. On the second floor there are 8 windows. 4 of them have screens. 1 of them is a window in a balcony door. There are also 2 skylights. One in a small roof section over the front door entry. The other is low in a sloping roof section over the 2nd floor. Inside, the window coverings are mostly mini-blinds except for the patio doors and an adjacent window which have vertical blinds.




TODO:
* citations data ideas discussed w/ Susan on 30-Jul drive to White Rock


TODO:
* write use case for Karyn's 5-yr average biololgy
* write use case for Becca's single point, 2 depths physics & chemistry
* write use case for month-average model products
* Becca's single point extraction triggers:
    /home/dlatorne/conda_envs/reshapr/lib/python3.10/site-packages/xarray/core/indexing.py:1228: PerformanceWarning: Slicing is producing a large chunk. To accept the large
    chunk and silence this warning, set the option
        >>> with dask.config.set(**{'array.slicing.split_large_chunks': False}):
        ...     array[indexer]

    To avoid creating the large chunks, set the option
        >>> with dask.config.set(**{'array.slicing.split_large_chunks': True}):
        ...     array[indexer]
      return self.array[key]
  then fails with:
    Traceback (most recent call last):
    File "/ocean/dlatorne/MOAD/Reshapr/reshapr/core/extract.py", line 655, in calc_extracted_vars
      std_name = var.attrs["standard_name"]
    KeyError: 'standard_name'

  



TODO:
* update .readthedocs.yaml build:os to ubuntu-22.04
* add sphinx-notfound-page extension to to repos with docs
  * https://sphinx-notfound-page.readthedocs.io/en/latest/index.html
  * MOAD:
    * Reshapr - done
    * docs - done
    * moad_tools
    * MoaceanParcels
    * cookiecutter-MOAD-pypkg
  * SalishSeaCast:
    * SalishSeaNowcast - done 4oct22
    * salishsea-site - done 11oct22
    * SalishSeaCmd
    * NEMO-Cmd - done 25oct22
    * SOG-Bloomcast-Ensemble
    * tools



Add Tereza's pubs to ERDDAP.


Set up VSCode for reStructuredText editing of docs.
* Used https://github.com/ammaraskar/sphinx-problem-matcher to add a VSCode problem-matcher
  to sphinx build task.


Reshapr ideas:
* extraction config examples in docs:
  * simple whole field extraction for a few variables
  * temporal and spatial selection
  * resampling
* extraction from month-avg datasets; issue #32
  * need to handle month-by-month dataset files 
    (e.g. SalishSeaCast_1m_ptrc_T_20220301_20220331.nc); 
    code presently assumes day-by-day
    (e.g. SalishSea_1d_20220314_20220314_ptrc_T.nc)


TODO:
* change SalishSeaNowcast automation key to ED-25519



TODO:
  Bug re: log rotation during download_wwatch3_results forecast2

* update SalishSeaCmd installation docs re: no anaconda and `python3 -m pip install`



TODO:
* for MoaceanParcels
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
Fix ariane docs:
* maybe re:  adding a bin-like directory to prefix gets rid of errors from doc/ and examples/ that confused Becca ???
 versions re: .bashrc



Update ONC URLs from dmas.uvic.ca to https://data.oceannetworks.ca/

jupyter kernelspec uninstall unwanted-kernel



TODO:

https://linuxize.com/post/getting-started-with-tmux/

update deployment docs re: spinning up a new compute node

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
