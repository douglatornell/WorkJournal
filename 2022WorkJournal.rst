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
* salish:
  * pull changes from GitHub
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
Change ot Python 3.10 for pkg dev; PR#
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
* created symlinks in grid/ required to run xxx
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
  * manager got start msg from watch)NEMO nowcast
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



Update ONC URLs to https://data.oceannetworks.ca/

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
