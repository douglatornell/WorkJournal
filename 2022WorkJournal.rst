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




GEMLAM external drives:
2007-2009
2010-2011 failed; needs to be re-made
2012-2014


(/SalishSeaCast/nowcast-env) ~$ python3 -m nowcast.workers.make_plots $NOWCAST_YAML wwatch3 forecast publish
/SalishSeaCast/nowcast-env/lib/python3.9/site-packages/pandas/io/parsers.py:3339: FutureWarning: 
        Use pd.to_datetime instead.

  return generic_parser(date_parser, *date_cols)
/SalishSeaCast/nowcast-env/lib/python3.9/site-packages/pandas/io/parsers.py:3339: FutureWarning: 
        Use pd.to_datetime instead.

  return generic_parser(date_parser, *date_cols)



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
