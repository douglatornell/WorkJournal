*****************
2021 Work Journal
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

Fri 1-Jan-2021
^^^^^^^^^^^^^^

Week 42 of UBC work-from-home due to COVID-19


Week 1
------

Mon 4-Jan-2021
^^^^^^^^^^^^^^

Week 43 of UBC work-from-home due to COVID-19

Group mtg; see whiteboard.
(MOAD)

Created 2021 work journal.

On-boarding planning mtg for Keegan & Aline w/ Susan, Elise & Karyn:
* Keegan w/ Karyn
* Aline w/ Elise
Slack call w/ Becca re: LoadFiles notebook, dask, etc.
Helped Karyn with accidentally committed mycert files in analysis-karyn.
(SalishSeaCast)

Change cookiecutter-analysis-repo to make SalishSeaCast the default GitHub org choice; updated MOAD docs to reflect that change.
Added SalishSeaTools deps pkgs to cookiecutter-analysis-repo env description.
Updated MOAD docs copyright year range.
Got GHA linkcheck failures in MOAD docs due to x2go wiki links.
(MOAD)


Tue 5-Jan-2021
^^^^^^^^^^^^^^

Investigated GHA linkcheck failures in MOAD docs due to x2go wiki links:
* also fails locally
* maybe due to outdated certifi and/or ca-certificate; updated them in moad-docs env; still no-go
Continued work on Getting Started section of MOAD docs.
(MOAD)

Requested, received, and set up Zoom account on UBC license.
Set up on-boarding mtg w/ Aline & Keegan for Thu 09:00.
Checked hake & halibut that Aline & Keegan will use for /results, /results2 & /data mounts; opened tickket to get /results2 and /data mounted on hake.
Uploaded LinuxCommandLine.pdf to Google Drive.
(SalishSeaCast)

See work journal.
(Ocean Navigator)


Wed 6-Jan-2021
^^^^^^^^^^^^^^

See work journal.
(Ocean Navigator)

Joined initial on-boarding Zoom for Aline & Keegan joinng MOAD to work with Elise & Karyn.
(SalishSeaCast)

FAL estate work: deposit BCE & MFC Q4 cheques; pay MCL CRA balance owing.

Wrote preliminary bash config section in MOAD docs.
(MOAD)


Thu 7-Jan-2021
^^^^^^^^^^^^^^

Did computing on-boarding session w/ Aline & Keegan; chaotic due to /ocaean failures and no Linux accounts for them yet.
(SalishSeaCast)

Got more warnings on kudu that root file system in low on space; that means /home/doug/; did some cleanup and recovered 12 of ~100 Gb.
Updated kudu to 20.10 groovy.
Moved minecraft from ~/.minecraft to /media/doug/warehouse/minecraft via symlink.
Discovered that flatpak installations are consuming >8Gb in /home/doug/; used https://github.com/flatpak/flatpak/issues/1224 to try to move installations; didn't work.

Cycled to West Point to pick up truing stand adapters and brake pads, then up to Blanca and home via Jericho (10km)


Fri 8-Jan-2021
^^^^^^^^^^^^^^

Experimented with xarray and hvplot, inspired by Rich Signell's video; didn't work worth a damn.
(MOAD)

Started work on a module to calc day averages of phytos for 6 mo periods for Tereza; PythonNotes/xarray-dayavg/
(SalishSeaCast)


Sat 9-Jan-2021
^^^^^^^^^^^^^^

Continued work on a module to calc day averages of phytos for 6 mo periods for Tereza; PythonNotes/xarray-dayavg/
(SalishSeaCast)

Drove to White Rock for Susan to visit M; walked in Ruth Johnson Park.


Sun 10-Jan-2021
^^^^^^^^^^^^^^^

Finances and Minecraft :-)


Week 2
------

Mon 11-Jan-2021
^^^^^^^^^^^^^^^

Week 44 of UBC work-from-home due to COVID-19

Finished work on a module to calc day averages of phytos for 6 mo periods for Tereza; PythonNotes/xarray-dayavg/ but decided to push it quietly.
Continued computing on-boarding w/ Keegan & Aline; still auth problems on hake/halibut/salish.
nowcast-agrif run failed due to orted issue; recovery at ~17:30:
  make_forcing_links orcinus-nowcast-agrif nowncast-agrif 2021-01-11
    job started, but now output; more orted issues?
(SalishSeaCast)


Tue 12-Jan-2021
^^^^^^^^^^^^^^^

Work at UBC while Rita is at home.

nowcast-agrif backfilling:
  make_forcing_links orcinus-nowcast-agrif nowncast-agrif 2021-01-11
  make_forcing_links orcinus-nowcast-agrif nowncast-agrif 2021-01-12
    failed; retried; failed
Finished computing on-boarding w/ Keegan & Aline; they have to use VPN to access hake/halibut/salish.
(SalishSeaCast)


Wed 13-Jan-2021
^^^^^^^^^^^^^^^

See work journal.
(Ocean Navigator)

Helped Karyn & Elise sort out ssh key issue re: cloning analysis-karyn to /data; due to ssh from lox to lox; also helped Elise craft email re: Karyn's loss of access to /ocean/ksuchy/.
Discovered that forecast got stuck; recovery:
  killed xios; nowcast-green started
nowcast-agrif backfilling:
  make_forcing_links orcinus-nowcast-agrif nowncast-agrif 2021-01-12
    failed
  emailed Mark
(SalishSeaCast)


Thu 14-Jan-2021
^^^^^^^^^^^^^^^

No NEMO or wwatch3 forecast2 runs due to forecast failure yesterday
DFO-IOS modeling collab mtg; Becca presented CANRMC4 downscaling work; discussion of Ambers's proposal.
(SalishSeaCast)

See work journal.
(Ocean Navigator)


Fri 15-Jan-2021
^^^^^^^^^^^^^^^

Helped Birgit w/ GitHub personal access token vs. ssh key question.
Pinged Elise re: discussion classes, inheritance & dependency injection.
Continued 2021 year rollover updates on repos; see https://salishseacast.slack.com/files/TFR25L4LU/F01HTF1MCBD
(MOAD)

See work journal.
(Ocean Navigator)

Emailed Mark@orciunus re: pod29 reservation; his reply explains how reservation interacts with scheduler; need to add QDR partition directive for best performance; resumed backfilling:
  make_forcing_links orcinus-nowcast-agrif nowncast-agrif 2021-01-12
  make_forcing_links orcinus-nowcast-agrif nowncast-agrif 2021-01-13
Started 2021 year rollover updates on repos; see https://salishseacast.slack.com/files/TFR25L4LU/F01HTF1MCBD:
  * skipped docs due to WIP re: linkcheck (I think)
  * deleted >2.1M lines in >400 files of run results that had been committed to SS-run-sets, reducing working files storage by >50% to 112M
Updated salishsea-site env on kudu and requirements.txt to address crytography pkg security warning; dropped -e pkgs from requirements.txt so that Dependabot can generate PRs for future updates.
(SalishSeaCast)

Started 2021 year rollover updates on repos; see https://salishseacast.slack.com/files/TFR25L4LU/F01HTF1MCBD
(MOAD)

Susan's parents received 1st doses Pfizer/BioNGen vaccine.


Sat 16-Jan-2021
^^^^^^^^^^^^^^^

Continued nowncast-agrif backfilling:
  make_forcing_links orcinus-nowcast-agrif nowncast-agrif 2021-01-14
  make_forcing_links orcinus-nowcast-agrif nowncast-agrif 2021-01-15
  make_forcing_links orcinus-nowcast-agrif nowncast-agrif 2021-01-16
(SalishSeaCast)

Drove to White Rock for Susan to visit J&M; walked in Ruth Johnson Park.


Sun 17-Jan-2021
^^^^^^^^^^^^^^^

FAL estate work: start prep for estate trust 19/20 income tax

nowcast-agrif run stopped
(SalishSeaCast)


Week 3
------

Mon 18-Jan-2021
^^^^^^^^^^^^^^^

Week 45 of UBC work-from-home due to COVID-19

FAL estate work: continued prep for estate trust 19/20 income tax

Helped Susan update OS on Glago Pro from 19.10 to 20.10 via 20.04.

Weekly group mtg; see whiteboard.
(MOAD)

Investigated 17jan nowncast-agrif failure; nothing obvious, so re-ran:
  make_forcing_links orcinus-nowcast-agrif nowncast-agrif 2021-01-17
(SalishSeaCast)


Tue 19-Jan-2021
^^^^^^^^^^^^^^^

See work journal.
(Ocean Navigator)

Emailed System76 re: support for custom install location for flatpak pkgs re: recent filling of $HOME.


Wed 20-Jan-2021
^^^^^^^^^^^^^^^

See work journal.
(Ocean Navigator)

Investigated upload_forcing to graham failures for forecast2 and turbidity; also reproduced for nowcast+; decided the errors are probably transient graham file system issues
(SalishSeaCast)

Researched removal of accidentally committed large files from git repos: 2 options: immediate and commit history:
  1) git rm --cached gitand_file; git commit --amend -CHEAD
  2) git filter-branch ...
see https://docs.github.com/en/github/managing-large-files/removing-files-from-a-repositorys-history
Fixed linkcheck failure and a couple of minor TODOs in MOAD docs.
(MOAD)

D&D w/ Allens.


Thu 21-Jan-2021
^^^^^^^^^^^^^^^

nowncast-agrif stopped 11 minutes into run; nothing obvious in *ocean.output; "SISTER_EOF attempting to communicate with sister MOM's" in stderr; re-ran
Started work on generating day-average files for nowcast-green.201905 results:
* profiled ncra on skookum:
    naive:
      skookum:01jan14$ time ncra -4 -L4 -O SalishSea_1h_20140101_20140101_grid_T.nc /tmp/SalishSea_1d_20140101_20140101_grid_T.nc
      real  0m29.276s
      user  0m13.576s
      sys 0m4.188s
    select variables (but all extra vars linke bounds_lon remain in output)
      skookum:01jan14$ time ncra -4 -L4 -O -v sossheig,votemper,vosaline SalishSea_1h_20140101_20140101_grid_T.nc /tmp/SalishSea_1d_20140101_20140101_grid_T.nc
      real  0m16.570s
      user  0m12.132s
      sys 0m3.892s
    carp_T:
      skookum:01jan14$ time ncra -4 -L4 -O -v PAR,sigma_theta,e3t,Fraser_tracer,dissolved_inorganic_carbon,total_alkalinity,dissolved_oxygen SalishSea_1h_20140101_20140101_carp_T.nc /tmp/SalishSea_1d_20140101_20140101_carp_T.nc
      real  1m1.229s
      user  0m41.204s
      sys 0m13.372s
    ptrc_T w/o variable selection:
      skookum:01jan14$ time ncra -4 -L4 -O SalishSea_1h_20140101_20140101_ptrc_T.nc /tmp/SalishSea_1d_20140101_20140101_ptrc_T.nc
      real  1m28.905s
      user  1m6.196s
      sys 0m21.536s
    ptrc_T w/ variable selection:
      skookum:01jan14$ time ncra -4 -L4 -O -v nitrate,ammonium,silicon,diatoms,flagellates,ciliates,microzooplankton,dissolved_organic_nitrogen,particulate_organic_nitrogen,biogenic_silicon,mesozooplankton SalishSea_1h_20140101_20140101_ptrc_T.nc /tmp/SalishSea_1d_20140101_20140101_ptrc_T.nc
      real  1m32.693s
      user  1m8.700s
      sys 0m22.724s
* profiled on salish:
    salish:01jan14$ time ncra -4 -L4 -O SalishSea_1h_20140101_20140101_grid_T.nc SalishSea_1d_20140102_20140102_grid_T.nc
    real  0m20.159s
    user  0m12.960s
    sys 0m7.188s
* Variables to day average:
  * grid_T:
      sossheig,votemper,vosaline
  * carp_T:
      AR,sigma_theta,e3t,Fraser_tracer,dissolved_inorganic_carbon,total_alkalinity,dissolved_oxygen
  * ptrc_T:
      nitrate,ammonium,silicon,diatoms,flagellates,ciliates,microzooplankton,dissolved_organic_nitrogen,particulate_organic_nitrogen,biogenic_silicon,mesozooplankton
* worked out most details and did some timing of xarray/dask implementation in an untitled notebook in PythonNotes; xarray/dask is faster than ncra: ~60s/day for 3 files
(SalishSeaCast)

See work journal.
(Ocean Navigator)

Helped Tereza diagnose Jupyter client drops; recommended ServerAliveInterval in .ssh/config.
(MOAD)


Fri 22-Jan-2021
^^^^^^^^^^^^^^^
Continued work on generating day-average files for nowcast-green.201905 results:
* moved work to analysis-doug/notebooks/hindcast-dayavgs
* added lots of narrative and more performance measurements to notebook
(SalishSeaCast)

See work journal.
(Ocean Navigator)


Sat 23-Jan-2021
^^^^^^^^^^^^^^^

Walked in Pacific Spirit Park from SWM & Camosun: Salish, Imperial, Hemlock, St. Georges trails

Read Django tutorial with the idea of re-implementing cyclelog instead of migrating it through many Django releases.


Sun 24-Jan-2021
^^^^^^^^^^^^^^^

Started working through Django tutorial.
Experimented with pre-commit hook tool because PyCharm pre-commit hook plugin appears to be un-maintained.


Week 4
------

Mon 25-Jan-2021
^^^^^^^^^^^^^^^

Week 46 of UBC work-from-home due to COVID-19

Re-ran a selection of the timing tests in the hindcast-dayavgs-dev notebook with engine="h5netcdf" and found (as usual) that it is *not* faster than netcdf4 (despite the assertion in the xarray docs).
Investigated yesterday's nowcast-agrif failure: inifiband error; re-ran 24jan & 25jan.
Added narrative re: writing netCDF4 files, and buffed sketch of stand-alone script.
(SalishSeaCast)

Collected OS & git version info from machines with:
  for host in char chum cod coho hake halibut herring lox sable salish skookum smelt tyee; \
    do echo -n "$host: "; \
    ssh $host "tail -1 /etc/lsb-release"; \
    ssh $host "git --version"; \
  done
Result:
  char: DISTRIB_DESCRIPTION="Ubuntu 16.04.7 LTS"
    bash: git: command not found
  chum: DISTRIB_DESCRIPTION="Ubuntu 16.04.6 LTS"
    git version 2.7.4
  cod: ssh: connect to host cod.eos.ubc.ca port 22: Connection timed out
  ssh: connect to host cod.eos.ubc.ca port 22: Connection timed out
  coho: DISTRIB_DESCRIPTION="Ubuntu 14.04.5 LTS"
    git version 1.9.1
  hake: DISTRIB_DESCRIPTION="Ubuntu 16.04.7 LTS"
    git version 2.7.4
  halibut: DISTRIB_DESCRIPTION="Ubuntu 14.04.6 LTS"
    git version 1.9.1
  herring: ssh: connect to host herring.eos.ubc.ca port 22: Connection timed out
  ssh: connect to host herring.eos.ubc.ca port 22: Connection timed out
  lox: DISTRIB_DESCRIPTION="Ubuntu 16.04.6 LTS"
    git version 2.7.4
  sable: DISTRIB_DESCRIPTION="Ubuntu 14.04.5 LTS"
    git version 1.9.1
  salish: DISTRIB_DESCRIPTION="Ubuntu 16.04.7 LTS"
    git version 2.7.4
  skookum: DISTRIB_DESCRIPTION="Ubuntu 16.04.7 LTS"
    git version 2.21.0
  smelt: DISTRIB_DESCRIPTION="Ubuntu 14.04.6 LTS"
    git version 1.9.1
  tyee: DISTRIB_DESCRIPTION="Ubuntu 16.04.6 LTS"
    bash: git: command not found
Created ticket requesting git>=2.28 be installed on tyee done.
(MOAD)

See work journal.
(Ocean Navigator)


Tue 26-Jan-2021
^^^^^^^^^^^^^^^

Work at UBC while Rita is at home.

Implemented CLI version of hindcast_dayavgs and started running it for 2014 in tmux session on salish.
(SalishSeaCast)


Wed 27-Jan-2021
^^^^^^^^^^^^^^^

See work journal.
(Ocean Navigator)

Ran hindcast_dayavgs for 2015-2016: 13.25 hrs
(SalishSeaCast)


Thu 28-Jan-2021
^^^^^^^^^^^^^^^

Sentry webinar: 3 Ways to Group Similar Issues:
* Armin Ronacher, Director of Engrg
* aka Grouping & Fingerprinting Errors
* sentry-cli send-event -m "Hello World"
* server-side:
  * Event grouping at bottom of event page
  * Merge button
  * Settings: Issue Grouping: Stack Trace Rules, Fingerprint Rules
    * hide flask frames, for example
* sdk-side:
  * before_send
  * scope

Continued 2021 year rollover updates on repos; see https://salishseacast.slack.com/files/TFR25L4LU/F01HTF1MCBD
(MOAD)

Ran hindcast_dayavgs for 2017-2018.
Cleaned up group rrg-allen -> def-allen and permissionss in project/SalishSea/forcing on graham
(SalishSeaCast)

See work journal.
(Ocean Navigator)


Fri 29-Jan-2021
^^^^^^^^^^^^^^^

collect_weather 00 didn't complete;
* investigation: 487 of 576 files downloaded, new message in log:
  2021-01-28 20:46:14,553 [ERROR] sr_amqp/publish: Sleeping 4 seconds ... and reconnecting
  2021-01-28 20:46:18,557 [ERROR] sr_amqp/close 2: [Errno 32] Broken pipe
  2021-01-28 20:46:18,562 [INFO] Using amqp module (AMQP 0-9-1)
  2021-01-28 20:46:20,617 [INFO] declared queue q_anonymous.sr_subscribe.hrdps-west.74434425.78671301 (anonymous@dd.weather.gc.ca)
  2021-01-28 20:46:20,953 [INFO] file_log downloaded to: /SalishSeaCast/datamart/hrdps-west/00/043/CMC_hrdps_west_DLWRF_SFC_0_ps2.5km_2021012900_P043-00.grib2
  2021-01-28 20:46:20,954 [INFO] heartbeat. Sarracenia version is: 2.20.08post1

  2021-01-28 20:46:20,954 [INFO] hb_memory cpu_times user=3731.62 system=420.24 elapse=54622530.87
  2021-01-28 20:46:20,954 [INFO] hb_memory, current usage: 58.2 MiB trigger restart if increases past: 165.0 MiB
  2021-01-28 20:46:20,954 [INFO] hb_retry on_heartbeat
  2021-01-28 20:46:20,954 [INFO] sr_retry on_heartbeat
  2021-01-28 20:46:20,964 [INFO] No retry in list
  2021-01-28 20:46:20,968 [INFO] sr_retry on_heartbeat elapse 0.012886
  2021-01-28 20:46:21,123 [WARNING] sr_amqp/consume: could not consume in queue q_anonymous.sr_subscribe.hrdps-west.74434425.78671301: Basic.ack: (406) PRECONDITION_FAILED - unknown delivery tag 193452
  2021-01-28 20:46:21,246 [INFO] Using amqp module (AMQP 0-9-1)
  2021-01-28 20:46:22,005 [INFO] declared queue q_anonymous.sr_subscribe.hrdps-west.74434425.78671301 (anonymous@dd.weather.gc.ca)
* recovery, started at 09:55:
    rm /results/forcing/atmospheric/GEM2.5/GRIB/20210129/00
    pkill -f collect_weather
    download_weather 00 2.5km
    rm -rf /SalishSeaCast/datamart/hrdps-west/00/*
    rm -rf /SalishSeaCast/datamart/hrdps-west/18/*
    collect_weather 18 2.5km
    download_weather 06 2.5km
    rm -rf /SalishSeaCast/datamart/hrdps-west/06/*
    wait for forecast2 runs to complete
    download_weather 12 2.5km
    rm -rf /SalishSeaCast/datamart/hrdps-west/12/*
Backfilled upload_forcing graham nowcast+ and turbidity for 20-28 Jan.
Answered question from Guoqi about relative run time of wwatch3 and NEMO:
* 19jan21 SSC/nowcast:
  * start run: 07:47:03
  * end results gathering: 08:12:33
  * elapsed: 25m30s
* 19jan21 wwatch3/nowcast:
  * start wind.nc creation: 10:53:42
  * end results gathering: 11:15:59
  * elapsed: 22m17s
Upgraded grouping algorithm on Sentry.
(SalishSeaCast)

See work journal.
(Ocean Navigator)

Cleaned up group rrg-allen -> def-allen in project/MIDOSS on graham; lots of files owned by Vicky though
(MIDOSS)


Sat 30-Jan-2021
^^^^^^^^^^^^^^^

Drove to White Rock for Susan to visit M&J; walked in Ruth Johnson Park.

upload_forcing graham nowcast+ and turbidity failed again
(SalishSeaCast)


Sun 31-Jan-2021
^^^^^^^^^^^^^^^

See work journal.
(Ocean Navigator)

upload_forcing graham nowcast+ and turbidity failed again; also failed on manual re-try
Ran hindcast_dayavgs for 2019-2020.
(SalishSeaCast)


February
========

Week 5
------

Mon 1-Feb-2021
^^^^^^^^^^^^^^

Week 47 of UBC work-from-home due to COVID-19

collect_weather 06 didn't complete;
* investigation: 574 of 576 files downloaded, new messages in log:
  lots of:
    2021-02-01 01:17:12,136 [ERROR] Download failed 5 https://dd5.weather.gc.ca/model_hrdps/west/grib2/06/012/CMC_hrdps_west_DSWRF_SFC_0_ps2.5km_2021020106_P012-00.grib2
    2021-02-01 01:17:12,136 [ERROR] Failed to reach server. Reason: [Errno 111] Connection refused
  and a few:
    2021-02-01 01:25:16,478 [INFO] expired message skipped 20210201091710.806 https://dd5.weather.gc.ca /model_hrdps/west/grib2/06/012/CMC_hrdps_west_APCP_SFC_0_ps2.5km_2021020106_P012-00.grib2
* recovery, started at ~09:40:
    pkill -f collect_weather
    collect_weather 18 2.5km
    rm /results/forcing/atmospheric/GEM2.5/GRIB/20210201/06
    download_weather 06 2.5km
    wait for forecast2 runs to complete
    download_weather 12 2.5km
    rm -rf /SalishSeaCast/datamart/hrdps-west/12/*
* log_aggregator was not getting messages from watch_ww3, so restarted it as preliminary forecast run finished
Experimented with issue grouping on Sentry to consolidate ONC SCVIP data fail messages across dates.
Discovered something funky about 201905/15feb20 that prevents dayavgs metadata cleanup.
Ran hindcast_dayavgs for 2012-2013.
(SalishSeaCast)

Group mtg; see whiteboard.
(MOAD)

Phys Ocgy Seminar: Karyn re: zooplankton

See work journal.
(Ocean Navigator)


Tue 2-Feb-2021
^^^^^^^^^^^^^^

Added more Sentry fingerprint rules to group issues for ONC data fails.
Continued 2021 year rollover updates on repos; see https://salishseacast.slack.com/files/TFR25L4LU/F01HTF1MCBD
Updated pkgs & versions in salishsea-nowcast env on kudu.
Investigated SalishSeaNowcast CI failures:
* comma accidentally dropped in Ben's commit yesterday
* change ProgressBar dep to tqdm
support@graham adjusted rrg-allen -> def-allen and vdo -> sallen; finished backfilling upload_forcing
Contributed to Ubuntu 20.04 packages list for new image for waterhole workstations.
Ran hindcast_dayavgs for 2010-20111.
Experimented with adding river-name & stn-id tags to sentry context in collect_river_data to make exceptions captured by Sentry more easily understood.
(SalishSeaCast)

Contributed to system pkgs list for Ubuntu 20.04 image to upgrade waterhole workstations.
(MOAD)

Telcon w/ Connor @ Buntain re: strata insurance; need to confirm:
* year of roof replacement
* no polybutyl plumbing
* no use of in-ceiling radiant head panels
* >100 amp electical service
* gathered all info and emailed it to him

Replaced failed lights in garage and utility room.


Wed 3-Feb-2021
^^^^^^^^^^^^^^

See work journal.
(Ocean Navigator)

upload_forcing failed because I inadvertently pulled tools updates with a missing comma in places.PLACES; recovered by pulling in fixed tools and re-running 4x upload_forcing nowcast+ manually.
Started looking at splitting tools repo via git filter-branch:
* I_ForcingFiles: new repo, new name
* Marlin: new repo/pkg
* NetCDF_Plot: placeholder; no action required
* Run_files: old/ancient ???
* SOGTools: new repo/pkg ???
* SalishSeaCmd: placeholder; no action required
* SalishSeaNowcast: placeholder; no action required
* SalishSeaTools: new repo/pkg
* analysis_tools: notebooks only; new repo, new name?
* bathymetry: almost all notebooks; combine w/ I_ForcingFiles in new repo w/ new name
* docs: mix of old stuff, and stuff that needs to be moved somewhere
  * I_ForcingFiles: index describing notebooks
  * LiveOcean: legacy?
  * bathymetry: index describing notebooks, also notebook about BAG files
  * erddap: outdated; see erddap-datasets repo
  * legacy_docs: old/ancient ???
  * nemo-tools: build instructions for rebuild_nemo
  * netCDF4: KEEP! creation & conventions docs; need update?
  * python_packaging: ???
* nocscombine: old/ancient ???
* random files:
  * ariane_memory.log: empty
  * namelist: empty
  * update_copyright.py: move into SalishSeaTools?
(SalishSeaCast)


Thu 4-Feb-2021
^^^^^^^^^^^^^^^

Experimented w/ renaming default branch name from master to main on GitHub in analysis-doug repo:
* ref: https://docs.github.com/en/github/administering-a-repository/renaming-a-branch
* rename master to main in web UI on GitHub
* in each clone:
  * git branch -m master main
  * git fetch origin
  * git branch -u origin/main main
* updated make_readme.py scripts and README.md files
Tried to run hindcast_dayavgs for 2008-20109; failed with "KeyError: 'online_operation'" on 2008-01-01 grid_T; re-tried for 2009, same issue.
(SalishSeaCast)

Updated example make_readme.py script to put creator name and repo's default branch name in constants at the top; updated make_readme.py in cookiecutter-analysis-repo similarly.
(MOAD)

See work journal.
(Resilient-C)

See work journal.
(Ocean Navigator)


Fri 5-Feb-2021
^^^^^^^^^^^^^^

arbutus OS updates plan re: CVE-2021-3156:
* after ww3-forecast finishes:
  * nowcast1 - nowcast9
* after fvcom-x2 finishes:
  * fvcom0 - fvcom1
* after fvcom-r12 finishes:
  * fvcom2 - fvcom6
  * nowcast0
* After doing sudo apt update; sudo apt upgrade on nowcast1 noticed that sudo was not in upgraded packages; checked version and found that installed version (1.8.21p2-3ubuntu1.4) is the one that is patched for CVE-2021-3156; assuming that auto-updates for security issues handled the issue. However, checking MOD and
  cat /var/run/reboot-required
shows that the VMs require reboots, so updated and rebooted them; after reboot on each VM:
  sudo mount -t nfs -o proto=tcp,port=2049 192.168.238.14:/MEOPAR /nemoShare/MEOPAR
remounted
  nowcast1
  nowcast3
  nowcast4
  nowcast5
  nowcast6
  nowcast7
  nowcast8
  nowcast9
  nowcast2
rebooted
upgraded
todo
  fvcom0
  fvcom1
  fvcom2
  fvcom3
  fvcom4
  fvcom5
  fvcom6
  nowcast0
Successfully booted nowcast2 and updated it as an extra VM.
(SalishSeaCast)

Coffee w/ Ben

Slack w/ Birgit about ANHA34 to ANHA12 interpolation.

See work journal.
(Ocean Navigator)

FAL estate work: delivered estate T3 return & draft to Cameron's office.


Sat 6-Feb-2021
^^^^^^^^^^^^^^

Set up Wahoo trainers, Emma & Red, and started riding Zwift.


Sun 7-Feb-2021
^^^^^^^^^^^^^^

Walked to English Bay overlook @ Stephen St.

Investment statements & transaction records catch-up.



Update cookiecutter-MOAD-pypkg re: hg -> git


jupyter kernelspec uninstall unwanted-kernel



TODO:

https://linuxize.com/post/getting-started-with-tmux/

update unpublished status of Olson, et al (2020)

update deployment docs re: spinning up a new compute node

Fix permissions in /opp dirs

OPPTools PRs:
  add numpy-indexed dependency
  fix pyproj.Proj() initializations
  fix nctime().strftime in OPPTools.utils.fvcom_postprocess.vertical_transect_snap()


Add CI workflows to run linkcheck on docs; see SalishSeaCast#repos-maint channel:
  need sphinx>3.1 in env
  example workflow in salishsea-site repo
  don't forget to add sphinx & sphinx_rtd_theme to environment-test.yaml


Update cookiecutter-MOAD-pypkg re: migration from hg to git, and requirements.txt in top level directory; probably more issues too.


15jun20: check mitigation of "index exceeds dimension bounds" IndexError in make_plots fvcom forecast-x2 research

Add VCS revision recording to run_fvcom

Update SalishSeaNowcast fig-dev docs

fix SalishSeaTools unit tests

fix old colander dependency in SOG

Fix Pillow security issue in analysis-doug


Stack:
* create NEMO_Nowcast.workers.spotter to monitor and optionally kill workers that tend to get stuck; initial use cases: collect_weather, make_ww3_wind_file
* wwatch3 run success confirmation
* fix warnings in figure modules
* fix get_vfpa_hadcp MMSI AttributeError issue
* debug gemlam interpolation
Done:
*
