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
Ran hindcast_dayavgs for 2010-2011.
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
Tried to run hindcast_dayavgs for 2008-2009; failed with "KeyError: 'online_operation'" on 2008-01-01 grid_T; re-tried for 2009, same issue.
(SalishSeaCast)

Updated example make_readme.py script to put creator name and repo's default branch name in constants at the top; updated make_readme.py in cookiecutter-analysis-repo similarly.
(MOAD)

See work journal.
(Resilient-C)

See work journal.
(Ocean Navigator)


Fri 5-Feb-2021
^^^^^^^^^^^^^^

Started arbutus OS updates plan re: CVE-2021-3156:
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


Week 6
------

Mon 8-Feb-2021
^^^^^^^^^^^^^^

Week 48 of UBC work-from-home due to COVID-19

See work journal.
(Ocean Navigator)

Group mtg; see whiteboard.
(MOAD)

Headache in the afternoon.


Tue 9-Feb-2021
^^^^^^^^^^^^^^

Work at UBC while Rita is at home.

Updating niko caused /boot to fill; deleted a bunch of old kernels with guidance from askubuntu (https://askubuntu.com/questions/345588/what-is-the-safest-way-to-clean-up-boot-partition).

Tried to review new 20.04 LTS image on waterhole.eoas.ubc.ca and stopped after 5 pkgs from list not installed.

Cleaned up conda envs on waterhole machines; deleted lots that I haven't used recently.

Looked at https://jupyterlab-code-formatter.readthedocs.io/ and found that the JupoyterLab extensions story is much better now; no explicit nodejs or extension manager installation; no need to enable extensions from command-line

Worked on analyzing/refactoring code that Alline & Elise are using for bloom timing time series extraction:
* /ocean/aisabell/MEOPAR/Analysis-Aline/notebooks/Bloom_Timing/201812EnvironmentalDrivers.ipynb
* /ocean/aisabell/MEOPAR/Analysis-Aline/notebooks/Bloom_Timing/extractloc.py
(SalishSeaCast)
* see analysis-doug/notebooks/aline-bloomtiming-extract/
* wrote Slack post about philospohpy of open_mfdataset/dask for Elise


Wed 10-Feb-2021
^^^^^^^^^^^^^^^

See work journal.
(Ocean Navigator)

Finalized Slack post about philospohpy of open_mfdataset/dask for Elise.
(SalishSeaCast)

See work journal.
(Resilient-C)


Thu 11-Feb-2021
^^^^^^^^^^^^^^^

collect_weather 06 didn't complete;
* investigation: 254 of 576 files downloaded, new messages in log:
    2021-02-11 07:31:01,654 [WARNING] sr_amqp/consume: could not consume in queue q_anonymous.sr_subscribe.hrdps-west.74434425.78671301: [Errno 110] Connection timed out
  lots of:
    2021-02-11 07:31:07,923 [ERROR] sr_amqp/build could not declare queue q_anonymous.sr_subscribe.hrdps-west.74434425.78671301 (anonymous@dd.weather.gc.ca) with [Errno 32] Broken pipe
* recovery, started at ~11:00:
    pkill -f collect_weather
    collect_weather 18 2.5km
    rm /results/forcing/atmospheric/GEM2.5/GRIB/20210211/12
    download_weather 12 2.5km
    supervisorctl restart sr_subscribe-hrdps-west
skookum rebooted at ~11:30; Charles reported accidental power cycle; recovery at ~13:00:
* started nowcast system via supervisord
* started salishsea-site via supervisord
* started ERDDAP via sudo /opt/tomcat/bin/startup.sh
automation restart:
* interruption occurred while nowcast-blue run was in progress
* download_results arbutus nowcast
* get_NeahBay_ssh forecast
* watch_NEMO foreacst failed to launch due to orphaned watch_NEMO nowcast:
  * killed orphan
  * launch_remote_worker arbutus watch_NEMO "arbutus forecast"
Took the opportunity to continue arbutus OS updates plan re: CVE-2021-3156:
* after reboot on each VM:
    sudo mount -t nfs -o proto=tcp,port=2049 192.168.238.14:/MEOPAR /nemoShare/MEOPAR
remounted
  fvcom0
  fvcom1
  fvcom2
  fvcom3
  fvcom4
  fvcom5
  fvcom6
rebooted
upgraded
todo
  nowcast0
Continued automation restart:
* launch_remote_worker arbutus make_fvcom_boundary "arbutus x2 nowcast"
* launch_remote_worker arbutus make_fvcom_boundary "arbutus r12 nowcast"
Merged Dependabot PRs re: crytography 3.2.1 -> 3.2.2.
Continued 2021 year rollover updates on repos; see https://salishseacast.slack.com/files/TFR25L4LU/F01HTF1MCBD; started SalishSeaCmd
(SalishSeaCast)

Worked w/ Birgit on parallelizing her ANHA4 to ANHA12 interpolation via GLOST.
Merged Dependabot PRs re: crytography 3.2.1 -> 3.2.2.
(MOAD)


Fri 12-Feb-2021
^^^^^^^^^^^^^^^

Continued 2021 year rollover updates on repos; see https://salishseacast.slack.com/files/TFR25L4LU/F01HTF1MCBD; finished SalishSeaCmd.
Changed SalishSeaNowcast repo default branch name from master to main.
Worked on fixing broken links in docs repo.
(SalishSeaCast)

Coffee w/ Aline.

See work journal.
(Resilient-C)

Rachael changes MIDOSS-MOHID-config repo default branch name from master to main; updated my clones on kudu and graham.
(MIDOSS)


Sat 13-Feb-2021
^^^^^^^^^^^^^^^

Goofed off.


Sun 14-Feb-2021
^^^^^^^^^^^^^^^

Finished fixing broken links in docs repo w/ help from Susan.
(SalishSeaCast)


Week 7
------

Mon 15-Feb-2021
^^^^^^^^^^^^^^^

Week 48 of UBC work-from-home due to COVID-19

**Statutory Holiday** - Family day

Added GHA sphinx linkcheck workflow to SalishSeaCast/docs repo; scheduled for 8th day of month.
Discovered th at docs repo has not copyright notices, only CC-By license.
Updated Olson, et al citation from unpublished.
(SalishSeaCast)


Tue 16-Feb-2021
^^^^^^^^^^^^^^^

Finalized docs repo GHA linkcheck workflow monthly schedule after successful scheduled test overnight.
Checked on ONC ferry and SCVIP data flows; both still down; looked at their new forum and status sites.
Investigated hindcast_dayavgs metadata problem; resolved by dropping bounds_nav_[lat|lon] variables present in some NEMO results files; ran hindcast_dayavgs for 2020-02-15 to 2020-12-31.
(SalishSeaCast)

Brought Makd-MIDOS-Forcing repo up to date; merged monte-carlo branch that adds "salishseacast grid" item to YAML config instead of hard-coded ERDDAP URL so that it can work on graham compute nodes w/o network access by using a path to a clone of the SalishSeaCast/grid repo.
(MIDOSS)


Wed 17-Feb-2021
^^^^^^^^^^^^^^^

See work journal.
(Ocean Navigator)

download_live_ocean failed w/ a connection timeout error; re-tried at 10:20, failed again; recovery:
* ssh to boiler works
* neither status nor product file are present at 11:50
* use LiveOcean boundary conditions file symlink created for forecast2 run to persist 16feb to 17feb
* upload_forcing arbutus nowcast+
* upload_forcing orcinus nowcast+
* upload_forcing graham nowcast+
* upload_forcing optimum nowcast+
Helped Susan with her high resolution lon/lat to SSC j/i mapping.
(SalishSeaCast)


Thu 18-Feb-2021
^^^^^^^^^^^^^^^

See work journal.
(Ocean Navigator)

Zoom coffee w/ Debby & Paul.

Reviewed changes in add-make-hdf5 branch of MIDOSS-MOHID-config in preparation for merge.
Reviewed changes in add-make-hdf5 branch of MOHID-Cmd in preparation for merge.
Reviewed clones on graham:
* Make-MIDOS-Forcing: up to date
* MIDOSS-MOHID-CODE: pulled to bring up to date
* MIDOSS-MOHID-config: up to date on main; WIP on add-make-hdf5
* MIDOSS-MOHID-grid: up to date
* moad_tools: pulled to bring up to date
* MOHID-Cmd: up to date enough; WIP on add-make-hdf5
* NEMO-Cmd: up to date
* SalishSeaCast-grid: up to date
Did a new build of MOHID; updated docs along the way; did a successful test of a 5 run Monte Carlo GLOST job.
(MIDOSS)

Generated MIDOSS Monte Carlo GLOST job for Birgit to look at in graham:/scratch/dlatorne/MIDOSS/runs/monte-carlo/InOneSSGrid_2021-02-18T194507/
(MOAD)


Fri 19-Feb-2021
^^^^^^^^^^^^^^^

Merged add-make-hdf5 branch in MIDOSS-MOHID-config into main.
Queued 3 diesel spills (w/o volume) test from 10k csv; running
Merged add-make-hdf5 branch in MOHID-Cmd into master.
Did year roll-over updates on MOHID-Cmd; did tech debt maintenance too
Fixed SyntaxWarnings re: string equality test in Make-MIDOS-Forcing; restricted pkg to Python 3.8.
Added spill volume to templates and _render...() function.
Ran the nearest thing yet to real Monte Carlo for 3 diesel spills.
(MIDOSS)

Ran hindcast_dayavgs for 2008-2009.
(SalishSeaCast)


Sat 20-Feb-2021
^^^^^^^^^^^^^^^

Goofed off :-)


Sun 21-Feb-2021
^^^^^^^^^^^^^^^

Started work on setting up 2020 bloomcast:
* Changed SOG-Bloomcast-Ensemble repo default git branch name from master to main.
* Built new bloomcast-2021 env on kudu from conda-forge only; got Python 3.7
* runs dir on salish: /data/dlatorne/SOG-projects/SOG-Bloomcast-Ensemble/run
* cp run/2019_bloomcast_inifile.yaml run/2020_bloomcast_infile.yaml; commit
* archived 2020_bloomcast* files in run/2020/
* archived bloomcast.log and bloom_date_evolution.log files into run/2020/
* edit 2021_bloomcast_infile.yaml
* edit config.yaml
* disable push to web for test run
* source activate /data/dlatorne/SOG-projects/bloomcast
* pip install -e /data/dlatorne/SOG-projects/SoG-Bloomcast-Ensemble
  * ensemble plug-in not installed - WTF???

* test run: cd run && bloomcast ensemble -v config.yaml
* test run succeeded: 10mar 12mar 20mar 07apr 13apr
* enabled push to web
* deleted wind_data_date to allow repeat run for today
* updated repo clone spelling in cronjob.sh
* ran manual production run w/ bash ./cronjob.sh; success! :-)
* checked bloomcast page on salishsea-site
* posted link to SalishSeaCast whiteboard
* enable cron job on salish
* commit 2020 config files
(bloomcast)


Week 8
------

Mon 22-Feb-2021
^^^^^^^^^^^^^^^

Week 49 of UBC work-from-home due to COVID-19

Changed WorkJournal and dotfiles repos default branch name from master to main.

nowcast-agrif failure: inifiband error; re-ran successfully.
Ran hindcast_dayavgs for 2007.
(SalishSeaCast)

Phys Ocgy seminar by Marek Stastna; modeling sub-grid internal waves

See work journal.
(Ocean Navigator)


Tue 23-Feb-2021
^^^^^^^^^^^^^^^

Worked at ESB while Rita was at home.

Failed to get bloomcast running:
* pip install -e in new env doesn't find ensemble plug-in
* attempt to run in last year's matplotlib-1.5.3 env on salish revealed that ECCC has changed the climate data interface to stream files for download
* tried to figure out ensemble plug-in failure:
  * created new nemo-cmd-test23feb env on niko, and ti worked fine
  * started modernize branch in SoG-Bloomcast-Ensemble to modernize packaging in hopes that will resolve unofund ensemble plug-in issue
* discovered that ensemble plug-in failure was a registration failure because SOGCommand that it depends on was not installed first - silent failure :-(
* discovered that code added in 2017 to skip 3 BOM characters in text response from ECCC climate requests now clips off 3 real characters at the start of the XML blobs
* remembered the need to start a dummy smtpd
* successfully ran bloomcast, but with Englishman River record ending on 25-Sep-2020
* profile plots failed:
    Traceback (most recent call last):
      File "/home/dlatorne/conda_envs/bloomcast/lib/python3.7/site-packages/cliff/app.py", line 401, in run_subcommand
        result = cmd.run(parsed_args)
      File "/home/dlatorne/conda_envs/bloomcast/lib/python3.7/site-packages/cliff/command.py", line 185, in run
        return_code = self.take_action(parsed_args) or 0
      File "/data/dlatorne/SOG-projects/SOG-Bloomcast-Ensemble/bloomcast/ensemble.py", line 135, in take_action
        profile_plots = self._create_profile_graphs(COLORS)
      File "/data/dlatorne/SOG-projects/SOG-Bloomcast-Ensemble/bloomcast/ensemble.py", line 473, in _create_profile_graphs
        colors=colors,
      File "/data/dlatorne/SOG-projects/SOG-Bloomcast-Ensemble/bloomcast/visualization.py", line 314, in profiles
        axs[0].set_ylim((profiles[0].indep_data[0], profiles[0].indep_data[-1]))
    IndexError: index 0 is out of bounds for axis 0 with size 0
(bloomcast)

See work journal.
(Ocean Navigator)


Wed 24-Feb-2021
^^^^^^^^^^^^^^^

See work journal.
(Ocean Navigator)

Mtg w/ Susan about priorities:
* get bloomcast working w/ Nanaimo River
* do rST/Sphinx tutorial for Aline, Keegan & Becca
* re-run ONC ferry data collection - wait for Susan to provide NEMO grid j/i to lon/lat mapping and include j/i values in new datasets
* migrate water levels to new Swagger API
* learn how to build XIOS & NEMO in new graham default env
* discussed master -> main migration
* discussed adding pre-commit to our repos
(MOAD)

Worked on bloomcast to get scaled Nanaimo River at Cassidy flow in as replacement for Englishman at Parksville (latter's gauge data stream stopped on 25-Sep-2020); got first successful run, still with profile plots failure above.
(bloomcast)


Thu 25-Feb-2021
^^^^^^^^^^^^^^^

Learned about myst-parser for Sphinx docs
(MOAD)

EOAS Colloquium re: carbon capture & storage

Added pre-commit framework to SalishSeaNowcast.
(SalishSeaCast)


Fri 26-Feb-2021
^^^^^^^^^^^^^^^

Teams social w/ NAFC group and Nancy & Riley.

download_results arbutus forecast failed w/ error code 1 in scp; re-ran successfully.
Investigated 25feb nowncast-agrif failure; auth problem during 25feb upload_forcing nowcast+; backfilled:
  upload_forcing orcinus-nowcast-agrif nowncast+ 2021-02-25
  make_forcing_links orcinus-nowcast-agrif nowncast-agrif 2021-02-25
    Failed w/ inifiband error; re-ran successfully
  make_forcing_links orcinus-nowcast-agrif nowncast-agrif 2021-02-26
(SalishSeaCast)

Ran bloomcast manually to investigate profiles plotting error; profiles/hoff_2021_bloomcast.out_* files are empty
Pushed changes to use scalled flow from Nanaaimo River at Cassidy gauge as replacement for Englishman.
Updated cloud fraction mapping re: new weather descriptions in 2020.
Activated daily cron run of bloomcast on salish despite plots not working.
(bloomcast)

Coffee w/ Racahel.

Worked on MOAD docs; added missing TOC entry for bash config; changed default branch name from master to main
(MOAD)


Sat 27-Feb-2021
^^^^^^^^^^^^^^^

Fixed cronjob.sh so that it uses up to date conda env and shows tracebacks on failure
(bloomcast)

nowcast-agrif failed ~14% into run; inifiband error; re-ran successfully
(SalishSeaCast)


Sun 28-Feb-2021
^^^^^^^^^^^^^^^

Fixed bug in accessing minor river scale factor from config.
(bloomcast)

Drove to White Rock for Susan to visit J&M; walked in Ruth Johnson Park.


March
=====

Week 9
------

Mon 1-Mar-2021
^^^^^^^^^^^^^^

Week 50 of UBC work-from-home due to COVID-19

Susan reviewed results of yeaterday's bloomcast run w/ correctly scaled Nanaimo River and accepted them for SoPO presentation.
Committed cronjob.sh updates; env path & --debug flag.
(bloomcast)

nowcast-agrif failed very early run; inifiband error; re-ran successfully
Deleted stale branches in NEMO-Cnd abd SalishSeaCmd repos on GitHub
(SalishSeaCast)

Finalized Lagrangian.dat file tempaltes for Monte Carlo runs:
* mv Lagrangian_BunkerC_crude.dat Lagrangian_bunker.dat
* mv Lagrangian_CLB_crude.dat Lagrangian_dilbit.dat
* ln -s Lagrangian_diesel.dat Lagrangian_gas.dat
* ln -s Lagrangian_diesel.dat Lagrangian_jet.dat
* ln -s Lagrangian_diesel.dat Lagrangian_other.dat
Replied to Rachael's request for terminal in random spills CSV with suggestion to use MMSI and date/time.
Deleted MIDOSS-MOHID-config add-make-hdf5 branch.
Deleted Make-MIDOS-Forcing monte-carlo branch.
Deleted MOHID-Cmd add-make-hdf5 branch.
Changed MOHID-Cmd default branch name from master to main.
Committed change to NEMO_Nowcast to disable Sentry init when worker runs in debug mode; its been uncommitted in production for months.
(MIDOSS)

Worked w/ Susan on mechanics of how to move master->main process forward.
Team mtg; see whiteboard.
(MOAD)

Phys Ocgy seminar: Racahel White; role of orography in ocean overturning circulation.


Tue 2-Mar-2021
^^^^^^^^^^^^^^

download_results forecast2 failed due to broken pipe; re-ran in debug mode at ~09:30.
make_plots nemo forecast publish failed () not the first time:
  requests.exceptions.HTTPError: 500 Server Error: ( The buffers supplied to a function was too small.  ) for url: https://ws-shc.qc.dfo-mpo.gc.ca/observations?WSDL
Updated setup-miniconda & action-slack in NEMO_Nowcast GHA CI workflow.
Investigated 2 unit test failures in NEMO_Nowcast associated with schedule pkg; it went from 0.6.0 to 1.0.0 on 20Jan.
Tried to build new conda pkgs for gomms-nowcast Anaconda channel; conda-build won't install from pip; time for a new approach...
(SalishSeaCast)

SoPO mtg day 1.

Discovered that GoMSS project conda-recipes repo never got migrated from Bitbucket to GitHub.


Wed 3-Mar-2021
^^^^^^^^^^^^^^

See work journal.
(Ocean Navigator)

Updated SalishSeaNowcast conda env for readthedocs to install NEMO_Nowcast from GH instead of gomms-nowcast Anaconda channel; decided to stop maintenance of that channel.
Changed NEMO_Nowcast repo default branch name from master to main.
Released NEMO_Nowcast v21.1.
(SalishSeaCast)

SoPO mtg day 2.


Thu 4-Mar-2021
^^^^^^^^^^^^^^

Advised Rachael on how to add terminal to random oil spills CSV code.
(MIDOSS)

See work journal.
(Ocean Navigator)

SoPO mtg day 3.


Fri 5-Mar-2021
^^^^^^^^^^^^^^

See work journal.
(Ocean Navigator)

FAL estate work: delivered docs to Scotia branch to get funds from chequing account.

Coffee w/ Karyn

Started planning changes to get_onc_ferry worker to add nearest NEMO grid ji indices to datasets.
(SalishSeaCast)


Sat 6-Mar-2021
^^^^^^^^^^^^^^

Worked changes to get_onc_ferry worker to add nearest NEMO grid ji indices to datasets; refactoed unit tests.
(SalishSeaCast)


Sun 7-Mar-2021
^^^^^^^^^^^^^^

Worked on changes to get_onc_ferry worker to add nearest NEMO grid ji indices to datasets; refactored nav coord resampling; generated sample file for Susan to check.
(SalishSeaCast)


Week 10
-------

Mon 8-Mar-2021
^^^^^^^^^^^^^^

Week 51 of UBC work-from-home due to COVID-19

docs repo scheduled linkcheck on GHA failed; fixed http://www.meds-sdmm.dfo-mpo.gc.ca to https://meds-sdmm.dfo-mpo.gc.ca
upload_forcing orcinus nowcast+ failed; auth glitch; re-ran successfully, but was too late to provide forcing to run, so it got stuck on 1st time step; killed stuck run; re-ran make_forcing_links to restart;
Continued work on changes to get_onc_ferry worker to add nearest NEMO grid ji indices to datasets.
Changed grid repo default branch name from master to main; updated on kudu, skookum, arbutus, optimum, orcinus.
(SalishSeaCast)

Group mtg; see whiteboard.
(MOAD)

Phys Ocgy seminar: Kevin Lamb, Waterloo, Internal Waves at low & high lats.


Tue 9-Mar-2021
^^^^^^^^^^^^^^

Worked at ESB while Rita was at home.

Migrated Sphinx docs from SalishSeaCast docs to MOAD docs and updated them.
(MOAD)


Wed 10-Mar-2021
^^^^^^^^^^^^^^^

See work journal.
(Ocean Navigator)

get_NeahBay_ssh failed overnight; investigation:
  * sites we scrape txt files from (main and alternate) are offline
* recovery starting at ~11:30:
  * symlink fcst/ssh_y2021m03d09.nc as obs/ssh_y2021m03d09.nc
  * skip forecast2 runs
  * upload_forcing arbutus nowcast+
  * upload_forcing orcinus nowcast+
  * upload_forcing graham nowcast+
  * upload_forcing optimum nowcast+
  * after nowcast-blue completion:
      upload_forcing arbutus ssh
(SalishSeaCast)


Thu 11-Mar-2021
^^^^^^^^^^^^^^^

Sphinx docs tutorial.
(MOAD)

Managed get_NeahBay_ssh issue in automation; after nowcast-blue completion:
  pkill -f get_NeahBay_ssh  # killed spinning nowcast and forecast instances
  upload_forcing arbutus ssh
  upload_forcing orcinus nowcast+
  upload_forcing graham nowcast+
  upload_forcing optimum nowcast+
Finished changes to get_onc_ferry worker to add nearest NEMO grid ji indices to datasets.
Started updating /results/observations/ONC/ferries/TWDP/ datasets from 2012-05-10 start of records on ONC server in tmux session on skookum:
  2012-05-10
(SalishSeaCast)


Fri 12-Mar-2021
^^^^^^^^^^^^^^^

See work journal.
(Ocean Navigator)

Managed get_NeahBay_ssh issue in automation; after nowcast-blue completion:
  pkill -f get_NeahBay_ssh  # killed spinning nowcast and forecast instances
  upload_forcing arbutus ssh
  upload_forcing orcinus nowcast+
  upload_forcing graham nowcast+
  upload_forcing optimum nowcast+
(SalishSeaCast)


Sat 13-Mar-2021
^^^^^^^^^^^^^^^

Managed get_NeahBay_ssh issue in automation; after nowcast-blue completion:
  pkill -f get_NeahBay_ssh  # killed spinning nowcast and forecast instances
  upload_forcing arbutus ssh
  upload_forcing orcinus nowcast+
  upload_forcing graham nowcast+
  upload_forcing optimum nowcast+
(SalishSeaCast)

Drove to White Rock for Susan to visit M&J; walked along Nikelmikel River.


Sun 14-Mar-2021
^^^^^^^^^^^^^^^

Managed get_NeahBay_ssh issue in automation; after nowcast-blue completion:
  pkill -f get_NeahBay_ssh  # killed spinning nowcast and forecast instances
  upload_forcing arbutus ssh
  upload_forcing orcinus nowcast+
  upload_forcing graham nowcast+
  upload_forcing optimum nowcast+
Retarted manager re: get_onc_ferry failure message change.
Started work on migrating water level obs & prediction collection from zeep to REST API.
(SalishSeaCast)


Week 11
-------

Mon 15-Mar-2021
^^^^^^^^^^^^^^^

Week 52 of UBC work-from-home due to COVID-19

Fixed bug, pushed & deployed re: get_onc_ferry failure message change.
Managed get_NeahBay_ssh issue in automation; after nowcast-blue completion:
  pkill -f get_NeahBay_ssh  # killed spinning nowcast and forecast instances
  upload_forcing arbutus ssh
  upload_forcing orcinus nowcast+
  upload_forcing graham nowcast+
  upload_forcing optimum nowcast+
Set NUMEXPR_MAX_THREADS=6 in SSC envs on skookum & arbutus; updated docs.
Added openpyxl as dep in SalishSeaTools.
Started experiments on splitting SalishSeaCast/tools repo; test of git filter-branch on Marlin pkg lead me to git-filter-repo that is the recommended alternative for (almost?) anything that git filter-branch can do; e.g.
  * created new Marlin repo from tools repo:
      git clone tools Marlin
      cd Marlin
      git filter-repo --subdirectory-filter Marlin/
Continued work on migrating water level obs & prediction collection from zeep to REST API.
(SalishSeaCast)

Group mtg; see whiteboard.
(MOAD)

Received and set up Acer Nitro GTX 1050 PC for Zwift.


Tue 16-Mar-2021
^^^^^^^^^^^^^^^

Fixed docs linkcheck issues in Make-MIDOS-Forcing.
(MIDOSS)

Managed get_NeahBay_ssh issue in automation; after nowcast-blue completion:
  pkill -f get_NeahBay_ssh  # killed spinning nowcast and forecast instances
  upload_forcing arbutus ssh
  upload_forcing orcinus nowcast+
  upload_forcing graham nowcast+
  upload_forcing optimum nowcast+
(SalishSeaCast)

See work journal.
(Ocean Navigator)


Wed 17-Mar-2021
^^^^^^^^^^^^^^^

See work journal.
(Ocean Navigator)

Killed stale get_onc_ferry worker from 15-Mar that caused port error this morning.
Managed get_NeahBay_ssh issue in automation; after nowcast-blue completion:
  pkill -f get_NeahBay_ssh  # killed spinning nowcast and forecast instances
  upload_forcing arbutus ssh
  upload_forcing orcinus nowcast+
  upload_forcing graham nowcast+
  upload_forcing optimum nowcast+
(SalishSeaCast)

Tried to answer Rachael's #moad-python-notes pandas.read_excel() and openpyxl.
(MOAD)


Thu 18-Mar-2021
^^^^^^^^^^^^^^^

See work journal.
(Ocean Navigator)


Replied to Keegan's #pugeteval request for examples of Hovmoller diagrams.
Managed get_NeahBay_ssh issue in automation; after nowcast-blue completion:
  pkill -f get_NeahBay_ssh  # killed spinning nowcast and forecast instances
  upload_forcing arbutus ssh
  upload_forcing orcinus nowcast+
  upload_forcing graham nowcast+
  upload_forcing optimum nowcast+
Continued work on migrating water level obs & prediction collection from zeep to REST API.
(SalishSeaCast)


Fri 19-Mar-2021
^^^^^^^^^^^^^^^

Mmerged PRs from Dependabot re: bump Pillow to 8.1.1 to address memory exhaustion DOS security vulnerability:
* SalishSeaCast/SOG-Bloomcast-Ensemble (rebase-merge: commit authored by Dependabot & me; no ref to PR in commit msg)
* analysis-doug/notebooks/melanie-geotiff (squash-merge: commit authored by Dependabot; commit msg links to PR)
* analysis-doug/notebooks/dask-expts (plain-merge: commit authored by me; commit msg is "Merge pull request #...")
* SalishSeaCast/SalishSeaNowcast (squash-merge)
* UBC-MOAD/moad_tools (squash-merge)

Concluded that I prefer squash-merge for dependabot PRs.

action-slack step in GHA workflows fails when workflows run from PR forks because SLACK_WEBHOOK_URL secret is not passed to forks

Managed get_NeahBay_ssh issue in automation; after nowcast-blue completion:
  pkill -f get_NeahBay_ssh  # killed spinning nowcast and forecast instances
  upload_forcing arbutus ssh
  upload_forcing orcinus nowcast+
  upload_forcing graham nowcast+
  upload_forcing optimum nowcast+
Continued work on migrating water level obs & prediction collection from zeep to REST API; Thrash until I finally figured out that UTC aware timestamps in pandas Series index don't convert to numpy datetime64.
(SalishSeaCast)


Sat 20-Mar-2021
^^^^^^^^^^^^^^^

Zwift Fondo Bambino

Managed get_NeahBay_ssh issue in automation; after nowcast-blue completion:
  pkill -f get_NeahBay_ssh  # killed spinning nowcast and forecast instances
  upload_forcing arbutus ssh
  upload_forcing orcinus nowcast+
  upload_forcing graham nowcast+
  upload_forcing optimum nowcast+
(SalishSeaCast)


Sun 21-Mar-2021
^^^^^^^^^^^^^^^

Managed get_NeahBay_ssh issue in automation; after nowcast-blue completion:
  pkill -f get_NeahBay_ssh  # killed spinning nowcast and forecast instances
  upload_forcing arbutus ssh
  upload_forcing orcinus nowcast+
  upload_forcing graham nowcast+
  upload_forcing optimum nowcast+
(SalishSeaCast)


Week 12
-------

Mon 22-Mar-2021
^^^^^^^^^^^^^^^

Week 53 of UBC work-from-home due to COVID-19

Managed get_NeahBay_ssh issue in automation; after nowcast-blue completion:
  pkill -f get_NeahBay_ssh  # killed spinning nowcast and forecast instances
  upload_forcing arbutus ssh
  upload_forcing orcinus nowcast+
  upload_forcing graham nowcast+
  upload_forcing optimum nowcast+
(SalishSeaCast)

Group mtg; see whiteboard.
(MOAD)

jinja to 2.11.3:
* SOG-Bloomcast
* NEMO-Cmd
* salishsea-site
* FVCOM-Cmd
* analysis-doug x2
* SOG
* ECget
* MIDOSS/docs
* cookiecutter-MOAD-pypkg
* moad_tools
* cookiecutter-analysis-repo
urllib3 to 1.26.3
* salishsea-site

See work journal.
(Ocean Navigator)


Tue 23-Mar-2021
^^^^^^^^^^^^^^^

Worked at ESB while Rita was at home.

Managed get_NeahBay_ssh issue in automation; after nowcast-blue completion:
  pkill -f get_NeahBay_ssh  # killed spinning nowcast and forecast instances
  upload_forcing arbutus ssh
  upload_forcing orcinus nowcast+
  upload_forcing graham nowcast+
  upload_forcing optimum nowcast+
Changed repo default branch names from master to main; updated on niko, skookum, arbutus, optimum, orcinus (old git; requires --set-upstream instead of -u), graham, kudu:
* SalishSeaCast/tracers
* SalishSeaCast/tides
* SalishSeaCast/rivers-climatology
* SalishSeaCast/XIOS-ARCH
Started work on building XIOS, NEMO & REBUILD_NEMO w/ new 2020 default compilers & libraries on graham:
* https://docs.computecanada.ca/wiki/Standard_software_environments
* present env will remain via ``module load StdEnv/2016.4``
  * Intel 2016.4, GCC 5.4.0, OpemMPI 2.1.1
* StdEnv/2020 will be default on 1-Apr-2020
  * Intel 2020.1, GCC 9.3.0, OpemMPI 4.0.3
  * AVX2 and AVX512 instruction sets -> fat binaries -> better skylake node support
  * compatibility changed from Nix to Gentoo Prefix
  * Linux kernel >=3.10, so CentOS 7
  * more Python extensions installed in their corresponding core modules; e.g. PyQt5 now inside qt/5.12.8, so it support mulitple versions of Python; `` module spider ...`` tells the stories of what modules to load
* experimented by creating ~/.modulerc via:
    echo "module-version StdEnv/2020 default" >> $HOME/.modulerc
* no change to Python versions; 3.8.2 is still most recent
* XIOS-ARCH:
    module load hdf5-mpi/1.8.18 - available, also 1.10.3, 1.10.6
    module load netcdf-c++4-mpi/4.3.0 - available, also 4.3.1
    module load netcdf-fortran-mpi/4.4.4 - available, also 4.5.1, 4.5.2
    module load netcdf-mpi/4.4.1.1 - available, also 4.1.3, 4.6.1, 4.7.4
    module load intel/2016.4 - now 2020.1.217
    module load perl/5.22.2 - available, also 5.16.3, 5.22.4, 5.30.2
* NEMO-3.6:
    module load netcdf-fortran-mpi/4.4.4
      in new env this implies:
        netcdf-fortran-mpi/4.5.2
        hdf5-mpi/1.10.6
        netcdf-mpi/4.7.4
        mpi4py/3.0.3
    module load perl/5.22.4 - available, also 5.16.3, 5.22.4, 5.30.2
    module load python/3.8.2 - available, also older versions
* XIOS-ARCH test:
    module load hdf5-mpi/1.10.6
    module load netcdf-c++4-mpi/4.3.1
    module load netcdf-fortran-mpi/4.5.2
    module load netcdf-mpi/4.7.4
    module load intel/2020.1.217
    module load perl/5.30.2
      implies: expat/2.2.9
  * ./make_xios --arch X64_GRAHAM  # no --job so I can clearly see warnings/errors
  * bunch of perl warnings at start
  * 1 warning re: \ in template
  * so slooooow...   2097 seconds = 35 minutes
  * success!
* NEMO-3.6 test, SalishSeaCast config
    module load netcdf-fortran-mpi/4.5.2
    module load perl/5.30.2
    module load python/3.8.2
  * XIOS_HOME=$HOME/MEOPAR/XIOS-2 ./makenemo -n SalishSeaCast -m X64_GRAHAM  # no -j so I can clearly see warnings/errors
  * 1 perl warning at start
  * 5 format statement warnings in stpctl.f90
      /home/dlatorne/MEOPAR/NEMO-3.6-code/NEMOGCM/CONFIG/SalishSeaCast/BLD/ppsrc/nemo/stpctl.f90(194): remark #8291: Recommended relationship between field width 'W' and the number of fractional digits 'D' in this edit descriptor is 'W>=D+7'.
      9300  FORMAT(' it :', i8, ' ssh2: ', e16.10, ' Umax: ',e16.10,' Smin: ',e16.10)
  * success!  891 seconds = 15 minutes
* REBUILD_NEMO test
  * XIOS_HOME=$HOME/MEOPAR/XIOS-2 ./maketools -n REBUILD_NEMO -m X64_GRAHAM
  * success!
* nco versions 4.6.6 (presently used for deflate) and 4.9.5
Continued work on migrating water level obs & prediction collection from zeep to REST API; test nowcast/figures/publish/compare_tide_prediction_max_ssh.py; more datetime index issues in using tidal predictions; suspect issue related to changes in xarray 0.17 re: datetime64 and int64.
(SalishSeaCast)


Wed 24-Mar-2021
^^^^^^^^^^^^^^^

See work journal.
(Ocean Navigator)

Managed get_NeahBay_ssh issue in automation; after nowcast-blue completion:
  pkill -f get_NeahBay_ssh  # killed spinning nowcast and forecast instances
  upload_forcing arbutus ssh
  upload_forcing orcinus nowcast+
  upload_forcing graham nowcast+
  upload_forcing optimum nowcast+
(SalishSeaCast)


Thu 25-Mar-2021
^^^^^^^^^^^^^^^

See work journal.
(Ocean Navigator)

Managed get_NeahBay_ssh issue in automation; after nowcast-blue completion:
  pkill -f get_NeahBay_ssh  # killed spinning nowcast and forecast instances
  upload_forcing arbutus ssh
  upload_forcing orcinus nowcast+
  upload_forcing graham nowcast+
  upload_forcing optimum nowcast+
Discussed priorities w/ Susan:
1. ONC ferry dataset description update to add NEMO gird indices on ERDDAP
2. Continue sorting out pandas/xarray datetime type issue re: CHS water levels, and other things?
3. Continue graham migration to StdEnv2020:
   * test run SalishSeaCast on graham
   * Birgit & Ben will likely stay on StdEnv2016 for present work; change by summer
   * change NEMO-Cmd & SalishSeaCmd from master to main
   * update NEMO-Cmd: docs only?
   * update SalishSeaCmd: code & docs
   * release NEMO-Cmd & SalishSeaCmd as 21.1
   * tag XIOS-ARCH
   * sort out MOHID build; update MIDOSS docs
   * update MOHID-Cmd: code & docs
   * release MOHID-Cmd as 21.1
Changed SalishSeaCast/erddap-datasets repo default branch name from master to main; updated on kudu, skookum.
(SalishSeaCast)

Started updating ERDDAP dataset description for ubcONCTWDP1mV18-01 to add nemo_grid_[ji] variables; stopped and restarted ERDDAP w/ sudo /opt/tomcat/bin/shutdown.sh; sudo /opt/tomcat/bin/startup.sh
(ERDDAP)

Monthly project mtg.
(MIDOSS)

Squash/merged dependabot PR in several repos re: PyYAML security vulnerability fixed in v5.4.


Fri 26-Mar-2021
^^^^^^^^^^^^^^^

See work journal.
(Ocean Navigator)

Managed get_NeahBay_ssh issue in automation; after nowcast-blue completion:
  pkill -f get_NeahBay_ssh  # killed spinning nowcast and forecast instances
  upload_forcing arbutus ssh
  upload_forcing orcinus nowcast+
  upload_forcing graham nowcast+
  upload_forcing optimum nowcast+
Changed GHA workflows to use org level SLACK_SALISHSEACAST_WEBHOOK_URL secret and set that up as a Dependabot secret too so that Dependabot PRs don't fail in their Slack notification step:
* SalishSeaNowcast
* NEMO-Cmd
* SalishSeaCmd
* salishsea-site
Continued work on migrating water level obs & prediction collection from zeep to REST API; test nowcast/figures/publish/compare_tide_prediction_max_ssh.py; more datetime index issues in using tidal predictions; root cause is combination of (mostly) pandas=1.1.0 change to produce timezone-aware indices when tz info is present in parsed data, and (maybe) xarray=0.16.1 change to int64 internal representation of datetime-like values and its increasing focus on CFTime; finally got a working figures/publish/compare_tide_prediction_max_ssh.py
(SalishSeaCast)

Added org-level Dependabot secrets on GitHub for MIDOSS and SalishSeaCast Slack notifications so that Dependabot PRs don't fail in their Slack notification step.
(MOAD)

Added org-level Dependabot secret on GitHub for MIDOSS Slack notifications so that Dependabot PRs don't fail in their Slack notification step.
(MIDOSS)


Sat 27-Mar-2021
^^^^^^^^^^^^^^^

rsync-ed SalishSeaTools and nowcast/figures/publish/compare_tide_prediction_max_ssh.py to skookum for testing.
Managed get_NeahBay_ssh issue in automation; after nowcast-blue completion:
  pkill -f get_NeahBay_ssh  # killed spinning nowcast and forecast instances
  upload_forcing arbutus ssh
  upload_forcing orcinus nowcast+
  upload_forcing graham nowcast+
  upload_forcing optimum nowcast+
(SalishSeaCast)

Drove to White Rock for Susan to visit J&M; walked in Ruth Johnson Park and along beach.


Sun 28-Mar-2021
^^^^^^^^^^^^^^^

Managed get_NeahBay_ssh issue in automation; after nowcast-blue completion:
  pkill -f get_NeahBay_ssh  # killed spinning nowcast and forecast instances
  upload_forcing arbutus ssh
  upload_forcing orcinus nowcast+
  upload_forcing graham nowcast+
  upload_forcing optimum nowcast+
(SalishSeaCast)


Week 13
-------

Mon 29-Mar-2021
^^^^^^^^^^^^^^^

Week 54 of UBC work-from-home due to COVID-19

Managed get_NeahBay_ssh issue in automation; after nowcast-blue completion:
  pkill -f get_NeahBay_ssh  # killed spinning nowcast and forecast instances
  upload_forcing arbutus ssh
  upload_forcing orcinus nowcast+
  upload_forcing graham nowcast+
  upload_forcing optimum nowcast+
(SalishSeaCast)

Started watching Atlantis session #1.
Atlantis session #1 Q&A:
* who, where, interest
(Atlantis)

Group mtg; see whiteboard.
(MOAD)

Updating ERDDAP dataset descriptions:
* chg ubcONCTWDP1mV18-01 temperature vars long name to "potential temperature"
* add addAttributes tags to change ONC URLs from dmas.uvic.ca to data.oceannetworks.ca
Stopped and restarted ERDDAP w/ sudo /opt/tomcat/bin/shutdown.sh; sudo /opt/tomcat/bin/startup.sh
(ERDDAP)


Tue 30-Mar-2021
^^^^^^^^^^^^^^^

Committed, pushed & deployed fixes to addAttributes tag typos that I forgot to do yesterday.
Stopped and restarted ERDDAP w/ sudo /opt/tomcat/bin/shutdown.sh; sudo /opt/tomcat/bin/startup.sh
(ERDDAP)

Managed get_NeahBay_ssh issue in automation; after nowcast-blue completion:
  pkill -f get_NeahBay_ssh  # killed spinning nowcast and forecast instances
  upload_forcing arbutus ssh
  upload_forcing orcinus nowcast+
  upload_forcing graham nowcast+
  upload_forcing optimum nowcast+
Test run of SalishSeaCast nowcast-green on graham in StdEnv2020:
* used builds from 23-Mar; XIOS-ARCH cc-stdenv-2020 branch
* pulled in changes:
  * grid
  * NEMO-3.6
  * NEMO-Cmd
  * rivers-climatology
  * SalishSeaCmd
  * tides
  * tracers
  * XIOS-2
* crafted YAML run description from nowcast-green/30mar21 run
* test failed due to namtrc misspelled variable
Changed default branch name in NEMO-Cmd repo to main.
(SalishSeaCast)

Squash-merged Dependabot PRs re: bump pygments to 2.7.4:
* SalishSeaCast/SOG-Bloomcast
* SalishSeaCast/analysis-doug x2
* SalishSeaCast/SOG
* SalishSeaCast/FVCOM-Cmd
* SalishSeaCast/NEMO-Cmd
* 43ravens/ECget
* MIDOSS/docs
Ignored PR in:
* douglatornell/asyncio-tutorial
* douglatornell/randopony
(MOAD)

See work journal.
(Ocean Navigator)


Wed 31-Mar-2021
^^^^^^^^^^^^^^^

See work journal.
(Ocean Navigator)

Learned of missing HRDPS files in Navigator call, then email, then found that yesterday's 18 forecast contains only 525 of 576 files, and collect_weather 18 never finished; recovery started at ~10:35:
  pkill collect_weather
  rm -rf /results/forcing/atmospheric/GEM2.5/GRIB/20210330/18
  download_weather 18 2.5km --debug  # beause I wasn't sure if I needed --yesterday; turns out no
  download_weather 00 2.5km
  download_weather 06 2.5km
  collect_weather 18 2.5km
  wait for forecast2 runs to finish
  download_weather 12 2.5km
  wait for nowcast-blue run to finish
Managed get_NeahBay_ssh issue in automation; after nowcast-blue completion:
  pkill -f get_NeahBay_ssh  # killed spinning nowcast and forecast instances
  upload_forcing arbutus ssh
  upload_forcing orcinus nowcast+
  upload_forcing graham nowcast+
  upload_forcing optimum nowcast+
Continued testing run of SalishSeaCast nowcast-green on graham in StdEnv2020:
* Susan identified namtrc issue as being due to removal of MYTRC1 variable from newer-than-production SalishSeaCast config
* sorted out Fraser turbidity forcing file location
* Discovered that XIOS-2 is throwing runtime errors and causing core dump
Changed default branch name in SalisheSeaCmd repo to main; updated clones of it and NEMO-Cmd on kudu, graham, skookum, arbutus, optimum & orcinus.
(SalishSeaCast)

Wrote slack msg to Birgit re: staying on StdEnv/2016.4 and how to change to StdEnv/2020 when she is ready.
(Arctic)

Updated SalishSeaCast/docs re: module load versions to build and run NEMO w/ Compute Canada StdEnv/2020.
(MOAD)

Coffee w/ Tereza.


Thu 1-Apr-2021
^^^^^^^^^^^^^^

Compute Canada changed graham env from StdEnv/2016.4 to StndEnv/2020.

Managed get_NeahBay_ssh issue in automation; after nowcast-blue completion:
  pkill -f get_NeahBay_ssh  # killed spinning nowcast and forecast instances
  upload_forcing arbutus ssh
  upload_forcing orcinus nowcast+
  upload_forcing graham nowcast+
  upload_forcing optimum nowcast+
Continued testing run of SalishSeaCast nowcast-green on graham in StdEnv2020:
* repeated yesterday's last run w/ XIOS-2 core dump in case I misinterpreted module load default on compute nodes and StdEnv/2020 wasn't there for yesterday's test; more fail
(SalishSeaCast)

Squash-merged Dependabot PRs re: bump lxml to 4.6.3:
SalishSeaCast/SalishSeaNowcast
SalishSeaCast/tools
(MOAD)

Finished watching Atlantis session #1.
Started watching Atlantis session #2.
Atlantis session #2 Q&A:
* physical env:
  * currents, temperature, salinity, total_alkalinity, pCO2
  * bacteria, phytos, zoops, corals
(Atlantis)


Fri 2-Apr-2021
^^^^^^^^^^^^^^

**Statutory Holiday** - Good Friday

Managed get_NeahBay_ssh issue in automation; after nowcast-blue completion:
  pkill -f get_NeahBay_ssh  # killed spinning nowcast and forecast instances
  upload_forcing arbutus ssh
  upload_forcing orcinus nowcast+
  upload_forcing graham nowcast+
  upload_forcing optimum nowcast+
Fixed broken links in SalishSeaCmd docs.
(SalishSeaCast)

Evaluated linux photo mgmt app; shotwell, digikam.
Got matisse set up and running w/ its external drives on my desk.


Sat 3-Apr-2021
^^^^^^^^^^^^^^

Managed get_NeahBay_ssh issue in automation; after nowcast-blue completion:
  pkill -f get_NeahBay_ssh  # killed spinning nowcast and forecast instances
  upload_forcing arbutus ssh
  upload_forcing orcinus nowcast+
  upload_forcing graham nowcast+
  upload_forcing optimum nowcast+
Was so late starting NEMO forecast run that make_fvcom_boundary forecast failed; recovery:
  wait for NEMO forecast run to finish
  launch_remote_worker make_fvcom_boundary "x2 forecast"
(SalishSeaCast)

rsync-ed iPhoto Originals/ from matisse to lizzy warehouse/shared/photos/.


Sun 4-Apr-2021
^^^^^^^^^^^^^^

Managed get_NeahBay_ssh issue in automation; after nowcast-blue completion:
  pkill -f get_NeahBay_ssh  # killed spinning nowcast and forecast instances
  upload_forcing arbutus ssh
  upload_forcing orcinus nowcast+
  upload_forcing graham nowcast+
  upload_forcing optimum nowcast+
(SalishSeaCast)

Read digikam docs.
Set up remote desktop access to lizzy from kudu via Remmina client on kudu and VNC enabled w/ password on lizzy.


April
=====

Week 14
-------

Mon 5-Apr-2021
^^^^^^^^^^^^^^

**Statutory Holiday** - Easter Monday

Week 55 of UBC work-from-home due to COVID-19

Fixed broken link to pytest docs in UBC-MOAD/docs; found by monthly scheduled linkcheck.
(MOAD)

LiveOcean was slow; failed at 11:54; re-ran successfully at 13:41.

Managed get_NeahBay_ssh issue in automation; after nowcast-blue completion:
  pkill -f get_NeahBay_ssh  # killed spinning nowcast and forecast instances
  upload_forcing arbutus ssh
  upload_forcing orcinus nowcast+
  upload_forcing graham nowcast+
  upload_forcing optimum nowcast+
(SalishSeaCast)

Used `sudo setfacl -m g:sada:rx /media/doug/` after `sudo chgrp`, etc. to make warehouse/shared/ accessible.
Decided to try digikam; installed it on lizzy; initialized a collection from the iPhoto Originals/ directory in warehouse/shared/photos.


Tue 6-Apr-2021
^^^^^^^^^^^^^^

Worked at ESB while Rita was at home.

Skimmed Greg Szorc's fascinating https://gregoryszorc.com/blog/2021/04/06/surprisingly-slow/ post; made me think about all the ways I/we use zlib compression that may actually be bottle necks; also interesting to see all the things that affect CPU core operations.

Updated and rebooted niko.

Managed get_NeahBay_ssh issue in automation; after nowcast-blue completion:
  pkill -f get_NeahBay_ssh  # killed spinning nowcast and forecast instances
  upload_forcing arbutus ssh
  upload_forcing orcinus nowcast+
  upload_forcing graham nowcast+
  upload_forcing optimum nowcast+
Fixed broken link to AGRIF site in NEMO-Cmd changelog; found by monthly scheduled linkcheck.
Discovered that yesterday's nowcast-dev went MIA on launch; recovery:
  make_forcing_links salish nowcast+ --shared-storage --run-date 2021-04-05
(SalishSeaCast)

Watched Atlantis session #3 video.
* autoconf-based build system
* docker for Windows
* executable: atlantisMerged
* model config:
  * .bgm file to define polygons (boxes); can be generated from shape file via utility
  * species groups files: .csv or .xml
    * detritus groups must be last
  * initial conditions in netCDF
    * layers number from 0 upward through water column, then downward through sediments
  * parameter files are:
      scalars: `key value  # comment` text files
      arrays:
        name size
         value value value ...
        * truncated if number of values > size
        * last value repeated if number of values < size
        * warning issued
    * biology parameter file is 14640 lines !!!
    * files:
      * biology
      * harvest
      * physics
      * forcing; different format; mostly pointing to other files
        * catch time series files; .ts
        * homebrewed format
          * # comments
          * schema in ## magic comments !!!
          * tab/space delimited data
    * output file:
      * flat text; post-process w/ R scripts; shiny, Rstudio
      * spatial; Olive old Python viz app; R scripts
Build atlantis on salish:
  mkdir /ocean/dlatorne/Atlantis
  chmod g+ws /ocean/dlatorne/Atlantis/
  cd /ocean/dlatorne/Atlantis/
  svn co --username ... .../svn/ext/atlantis/Atlantis/trunk/ atlantis-trunk
  # declined unencrypted password storage
  # autoconf already installed
  # automake already installed
  aclocal
  autoheader
  autoconf
  automake -a
  ./configure
  # failed with:
      Proj4 library is required for Atlantis. Install package proj
  sudo apt install libproj-dev
  ./configure
  make clean
  make
  # failed with:
      salish:atlantis$ make
      make  all-recursive
      make[1]: Entering directory '/ocean/dlatorne/Atlantis/atlantis-trunk/atlantis'
      Making all in ConvertAtlantis
      make[2]: Entering directory '/ocean/dlatorne/Atlantis/atlantis-trunk/atlantis/ConvertAtlantis'
      gcc -DHAVE_CONFIG_H -I. -I.. -I/usr/include/libxml2 -I../atassess/include -I../atecology/include -I../ateconomic/include -I../atlantisUtil/include -I../atlantismain/include -I../atharvest/include -I../atimplementation/include -I../atmanage/include -I../atphysics/include -I../atFileConvert/include -I../sjwlib/include  -I../ConvertAtlantis/include -I../atSS3Link/include -I. -I../atlantismain     -D PROJ4 -D REPLICATE_OLD_RESULTS -D BETH_LOG_FILE_SIZE  -g -msse2 -mfpmath=sse   -Wall -Wextra -Wno-unused-parameter -Wuninitialized -Warray-bounds -Wunused-but-set-variable -Wno-error=unused-but-set-variable  -Wformat-overflow -Werror  -pedantic  -std=c99    -MT atBioltoXML.o -MD -MP -MF .deps/atBioltoXML.Tpo -c -o atBioltoXML.o atBioltoXML.c
      gcc: error: unrecognized command line option ‘-Wformat-overflow’
      Makefile:453: recipe for target 'atBioltoXML.o' failed
      make[2]: *** [atBioltoXML.o] Error 1
      make[2]: Leaving directory '/ocean/dlatorne/Atlantis/atlantis-trunk/atlantis/ConvertAtlantis'
      Makefile:373: recipe for target 'all-recursive' failed
      make[1]: *** [all-recursive] Error 1
      make[1]: Leaving directory '/ocean/dlatorne/Atlantis/atlantis-trunk/atlantis'
      Makefile:314: recipe for target 'all' failed
      make: *** [all] Error 2
  Sent email to Bec.
  Hacked PreRules.am to remove -Wformat-overflow
  Build success!!
  Skipped `sudo make install`; executable is atlantis-trunk/atlantis/atlantismain/atlantisMerged
Atlantis session #3 Q&A:
* learned about PreRules.am
* learned where executable lives
* Javier uses bash, emacs org-mode, and GitHub to do the equivalent of NEMO-Cmd
* Thoughts:
  * probably need AtlantisCmd
  * probably need equivalent of SS-run-sets
(Atlantis)


Wed 7-Apr-2021
^^^^^^^^^^^^^^

PyCharm 2021.1 released; watched summary video; updated kudu.

Managed get_NeahBay_ssh issue in automation; after nowcast-blue completion:
  pkill -f get_NeahBay_ssh  # killed spinning nowcast and forecast instances
  upload_forcing arbutus ssh
  upload_forcing orcinus nowcast+
  upload_forcing graham nowcast+
  upload_forcing optimum nowcast+
Backfilling nowcast-dev:
  wait for today's run to fail
  make_forcing_links salish nowcast+ --shared-storage --run-date 2021-04-06
  wait for run to complete
  make_forcing_links salish nowcast+ --shared-storage --run-date 2021-04-07
Built new nowcast-env on skookum:
  * killed stale workers:
      ps faux | grep nowcast
      pkill -9 -f make_surface_current_tiles
      pkill -f nowcast.workers.upload_forcing
      pkill -f nowcast.workers.make_runoff_file
      pkill -9 -f nowcast.workers.make_plot
  * killed workers associated with tasks in progress; 3 are note yet timed out ssh connections:
      pkill -f collect_weather
      pkill -f watch_NEMO
      pkill -f run_fvcom
      pkill -f watch_fvcom
  * stopped long-running processes via supervisorctl, then shit down supervisord:
      supervisorctl stop log_aggregator
      supervisorctl stop manager
      supervisorctl stop message_broker
      supervisorctl stop sr_subscribe-hrdps-west
      supervisorctl stop sr_subscribe-hrdps-west-1km
      supervisorctl stop sr_subscribe-hydrometric
      supervisorctl shutdown
  * deactivated and removed nowcast-env
      conda deactivate
      conda env remove --prefix /SalishSeaCast/nowcast-env
  * updated conda
      conda update -n base -c defaults conda
  * updated git clones ** except OPPTools**
      NEMO_Nowcast
      moad_tools
      SalishSeaTools  # git stash; git pull; git stash pop
      NEMO-Cmd
      SalishSeaCmd
      SalishSeaNowcast  # git stash; git pull; git stash pop
  * create new nowcast-env
      conda env create --prefix /SalishSeaCast/nowcast-env -f envs/environment-prod.yaml
  * set up envvars:
      added export NUMEXPR_MAX_THREADS=6 to /SalishSeaCast/nowcast-env-envvars.sh
      cp nowcast-env-envvars.sh nowcast-env/etc/conda/activate.d/envvars.sh
      constructed nowcast-env/etc/conda/deactivate.d/envvars.sh from /SalishSeaCast/nowcast-env-envvars.sh
  * install our pkgs:
      NEMO_Nowcast
      moad_tools
      SalishSeaTools
      OPPTools
      NEMO-Cmd
      SalishSeaCmd
      SalishSeaNowcast
Updated OS pkgs on arbutus nowcast0; TODO reboot nowcast0 when cluster is quiet
  sudo apt update
  sudo apt upgrade
  sudo apt autoremove
Restarted nowcast-env automation on skookum:
  * start supervisord
  * restart workers associated with tasks in progress:
      collect_weather 00 2.5km
Tested water level figs in new env:
  make_plots nemo forecast publish
    failed on CherryPoint, FridayHarbor due to bad id
    failed on HalfmoonBay dur to: AttributeError: 'Float64Index' object has no attribute 'tz_convert'
  make_plots fvcom nowcast publish
(SalishSeaCast)

Squash-merged Dependabot PRs re: bump urllib3 to 1.26.4:
* UBC-MOAD/docs
* UBC-MOAD/moad_tools
* 43ravens/NEMO_Nowcast
* MIDOSS/MOHID-Cmd
* MIDOSS/Make-MIDOS-Forcing
* SalishSeaCast/tools
* SalishSeaCast/SalishSeaNowcast
* SalishSeaCast/SOG-Bloomcast-Ensemble
* SalishSeaCast/salishsea-site
(MOAD)


Thu 8-Apr-2021
^^^^^^^^^^^^^^

Rebooted nowcast0 at ~08:30 and it failed with:
  Error: Failed to perform requested operation on instance "nowcast0", the instance has an error status: Please try again later [Error: libvirtError].
Did a shutdown on the instance and tried to restart it, but it kept erroring out; send email to cloud@. Response at ~10:30 from Jeff Albert; problem was related to persistent volume attachement; he manually re-attached the volume and the instance booted. Recovery:
* Re-mount persistent storage volume:
    sudo mount /dev/vdc /nemoShare  # took several seconds of nervousness
* Re-bind /nemoShare/MEOPAR to /export/MEOPAR
    sudo mount --bind /nemoShare/MEOPAR /export/MEOPAR
* Fix /etc/fstab and restart NFS service:
    # add to /etc/fstab; why was it missing?
    /nemoShare/MEOPAR   /export/MEOPAR  none  bind  0  0
    sudo systemctl start nfs-kernel-server.service
* Fix stale NFS handles on compute nodes:
    sudo exportfs -f  # on nowcast0
* Launched nowcast-blue via make_forcing_links
    make_forcing_links arbutus nowcast+
Managed get_NeahBay_ssh issue in automation; after nowcast-blue completion:
  pkill -f get_NeahBay_ssh  # killed spinning nowcast and forecast instances
  upload_forcing arbutus ssh
  # realized that there is no need to do upload_forcing nowcast+ for orcinus, optimum & optimum because they succeed after grib_to_netcdf, and there is no new ssh data after than
Helped Aline get her SalishSeaCast/docs env sorted out re: pandoc.
(SalishSeaCast)

FAL estate work:
* confirmed info w/ Scotia for closure of account
* authorized and paid for headstone cleaning and engraving

Worked on strata building insurance.

Filed ProServices quarterly usage report.

Atlantis session #4 Calibration & R tools:
* https://seaview.csiro.au/index.html
* RStudio and Shiny


Fri 9-Apr-2021
^^^^^^^^^^^^^^

Managed get_NeahBay_ssh issue in automation; after nowcast-blue completion:
  upload_forcing arbutus ssh
Discussed updating get_NeahBay_ssh w/ Susan.
Resumed work on getting NEMO and FVCOM water level figures to work w/ new CHS IWLS API obs and predicions; figures all working now, I think; uncommitted code on skookum to test in automation.
(SalishSeaCast)

FAL estate work: signed letter of transmission for chequing acct at Scotia; deposited Manulife chq at TD


Sat 10-Apr-2021
^^^^^^^^^^^^^^^

Managed get_NeahBay_ssh issue in automation; after nowcast-blue completion:
  upload_forcing arbutus ssh
(SalishSeaCast)

Drove to white Rock to visit M&J; first time since Mar-2020 that we have been able to go to J's suite; 1st time since Mar-2020 that I have seen them in person.
Walked in Mud Bay Park on the way home; very windy.


Sun 11-Apr-2021
^^^^^^^^^^^^^^^

Managed get_NeahBay_ssh issue in automation; after nowcast-blue completion:
  upload_forcing arbutus ssh
Committed, merged, and pushed SalishSeaTools.data_tools.get_chs_tides() changes re: 7 day water level request limit, pandas datetimes timezone handling, and edge cases of station codes.
Committed, merged, and pushed SalishSeaNowcast CHS-water-levels branch
(SalishSeaCast)

Cycled to east end of River Rd and back; 1st outdoor training ride of the year; pleased with how well Zwift fitness transferred to riding on the road.


Week 15
-------

Mon 12-Apr-2021
^^^^^^^^^^^^^^^

Week 56 of UBC work-from-home due to COVID-19

See work journal.
(Ocean Navigator)

Managed get_NeahBay_ssh issue in automation; after nowcast-blue completion:
  pkill -f get_NeahBay_ssh  # killed spinning nowcast and forecast instances
  upload_forcing arbutus ssh
(SalishSeaCast)

Group mtg; see whiteboard.
(MOAD)

Phys Ocgy seminar: Andrew Shao

No email from outside EOAS is reaching me.

FAL estate: received 2020 trust tax assessment notice & trust number


Tue 13-Apr-2021
^^^^^^^^^^^^^^^

Managed get_NeahBay_ssh issue in automation; after nowcast-blue completion:
  pkill -f get_NeahBay_ssh  # killed spinning nowcast and forecast instances
  upload_forcing arbutus ssh
(SalishSeaCast)

Helped Raisha with Atlantis build system on her Mac.
Watched video #5.
Used VSCode for Atlantis work:
* updated c/c++ extension
* installed autoconf extension for syntax highlighting
Build atlantis on kudu:
  mkdir /media/doug/warehouse/Atlantis
  cd /media/doug/warehouse/Atlantis
  # created enviornment-dev.yaml
  conda env create -f enviornment-dev.yaml
  svn co --username ... ,,,/svn/ext/atlantis/Atlantis/trunk/ atlantis-trunk
  aclocal
  autoheader
  autoconf
  automake -a
  ./configure
  # failed to detect libproj
  # hacked configure.ac to look for proj_context_create() instead of pj_init()
  autoconf
  automake -a
  ./configure
  make
  # problems with with proj function calls
  # rolled env back to proj4
  aclocal
  autoheader
  autoconf
  automake -a
  ./configure
  make
  # bunch of wraning to error conversions; hacked around them in configure.ca:
    WARN += -Wno-unused-result
    WARN += -Wno-format-overflow
    WARN += -Wno-stringop-truncation
    WARN += -Wno-stringop-overflow
  automake -a
  ./configure
  # successful build
    executable: /media/doug/warehouse/Atlantis/atlantis-trunk/atlantis/atlantismain/atlantisMerged
  # successful run of example
Add R to env:
  # add r and r-devtools to conda env
  # from https://github.com/Atlantis-Ecosystem-Model/ReactiveAtlantis README
  R
  > library("devtools")
  > install_github('Atlantis-Ecosystem-Model/ReactiveAtlantis', force=TRUE, dependencies=TRUE)
  # skip updates
  # lots of compilation
  > library("ReactiveAtlantis")
  > biom <- 'atlantis-trunk/example/outputFolder/outputSETASBiomIndx.txt'
  > diet.file <- "atlantis-trunk/example/outputFolder/outputSETASDietCheck.txt"
  > bio.age <- "atlantis-trunk/example/outputFolder/outputSETASAgeBiomIndx.txt"
  > grp.csv <- "atlantis-trunk/example/SETasGroupsDem.csv"
  > predation(biom, grp.csv, diet.file, bio.age)
  Loading required package: shiny

  Listening on http://127.0.0.1:6811
  Error in utils::browseURL(appUrl) :
    'browser' must be a non-empty character string
Emailed Javier for help.
(Atlantis)

Updated conda on kudu from 4.9.2 to 4.10.0.

Some ex-EOAS messages arrived over night
Sent sample of delayed to Charles in EOAS #general.


Wed 14-Apr-2021
^^^^^^^^^^^^^^^

Managed get_NeahBay_ssh issue in automation; after nowcast-blue completion:
  pkill -f get_NeahBay_ssh  # killed spinning nowcast and forecast instances
  upload_forcing arbutus ssh
Continued work on new collect_NeahBay_ssh worker; deployed for testing to skookum; Susan successfully tested it in the evening for the 15Apr 00Z data.
(SalishSeaCast)

Watched video #6.
More work on trying to get ReactiveAtlantis to work:
* got a minimal demo shiny app to run; key was:
    > options(browser = 'firefox')
    # before
    > runApp("app.R")  # or mybe just runApp()
* and for clone of ReactiveAtlantis:
    > options(browser = 'firefox')
    > library("devtools")
    > install_local("/media/doug/warehouse/Atlantis/ReactiveAtlantis")
    > library("ReactiveAtlantis")
    # in example/outputFolder/
    > biom <- "outputSETASBiomIndx.txt"
    > diet.file <- "outputSETASDietCheck.txt"
    > bio.age <- "outputSETASAgeBiomIndx.txt"
    > grp.csv <- "../SETasGroupsDem.csv"
    > predation(biom, grp.csv, diet.file, bio.age)
(Atlantis)


Thu 15-Apr-2021
^^^^^^^^^^^^^^^

FAL estate: emailed PDF of 2020 trust tax assessment notice & trust number to Cameron

Managed get_NeahBay_ssh issue in automation; after nowcast-blue completion:
  pkill -f get_NeahBay_ssh  # killed spinning nowcast and forecast instances
  upload_forcing arbutus ssh
Added step to GHA CI workflow for SalishSeaNowcast to run `env` in shell so that I could audit for secrets in the env that might have been exposed due to https://about.codecov.io/security-update/; found none :-)
Started re-run in tmux on salish of get_onc_ctd for SCVIP for 2015-2018 for Susan's flux paper.
(SalishSeaCast)

See work journal.
(Ocean Navigator)


Fri 16-Apr-2021
^^^^^^^^^^^^^^^

EOAS Linux /home unavailable from 09:00 to ??? due to NextCloud server OS update;

Scanned time tracking spreadsheet and work logs to compile list of MEOPAR Prediction Core activities during Apr-20 through Mar-21 for Susan to report on.
(Prediction Core)

Got reconnected to skookum at ~17:15; collect_weather 12 still waiting to complete w/ 72 of 576 files downloaded; recovery:
  pkill collect_weather 12
  rm -rf /results/forcing/atmospheric/GEM2.5/GRIB/20210416/12
  download_weather 12 2.5km
  download_weather 18 2.5km
  download_weather 00 1km  # 404 errors
  download_weather 12 1km
  collect_weather 00 2.5km
  wait for nowcast-blue run to finish
  pkill -f get_NeahBay_ssh  # killed spinning nowcast and forecast instances
  upload_forcing arbutus ssh
(SalishSeaCast)

Filed 43ravens GST/HST return for 2020.

Updated lots of 43ravens repos to change default branch name from main to master.

Noticed that GitHubhave added:
  git remote set-head origin -a
to the post-default-branch rename commands list.

Did 1st pass on income tax returns.


Sat 17-Apr-2021
^^^^^^^^^^^^^^^

Managed get_NeahBay_ssh issue in automation; after nowcast-blue completion:
  pkill -f get_NeahBay_ssh  # killed spinning nowcast and forecast instances
  upload_forcing arbutus ssh
(SalishSeaCast)

Cycled reverse Richmond loop, minus Iona, and River Rd east of No. 7 Road; used No. 7 Rd instead of No. 6 Rd to get north - less traffic. 60 km


Sun 18-Apr-2021
^^^^^^^^^^^^^^^

Managed get_NeahBay_ssh issue in automation; after nowcast-blue completion:
  pkill -f get_NeahBay_ssh  # killed spinning nowcast and forecast instances
  upload_forcing arbutus ssh
(SalishSeaCast)


Week 16
-------

Mon 19-Apr-2021
^^^^^^^^^^^^^^^

Week 57 of UBC work-from-home due to COVID-19

Managed get_NeahBay_ssh issue in automation; after nowcast-blue completion:
  pkill -f get_NeahBay_ssh  # killed spinning nowcast and forecast instances
  upload_forcing arbutus ssh
Started dev of make_ssh_file worker to replace 2nd step of get_NeahBay_ssh.
(SalishSeaCast)

Group mtg; see whiteboard.
(MOAD)

Phys Ocgy seminar.


Tue 20-Apr-2021
^^^^^^^^^^^^^^^

Worked at ESB while Rita was at home.

Managed get_NeahBay_ssh issue in automation; after nowcast-blue completion:
  pkill -f get_NeahBay_ssh  # killed spinning nowcast and forecast instances
  upload_forcing arbutus ssh
Continued dev of make_ssh_file worker to replace 2nd step of get_NeahBay_ssh.
(SalishSeaCast)

Squash-merged a bunch of dependabot PRs re: regex DoS vulnerability in py pkg.


Wed 21-Apr-2021
^^^^^^^^^^^^^^^

upload_forcing orcinus foreast2 failed due to network connection time-out; still can't connect to orcinus at 09:08.
Managed get_NeahBay_ssh issue in automation; after nowcast-blue completion:
  pkill -f get_NeahBay_ssh  # killed spinning nowcast and forecast instances
  upload_forcing arbutus ssh
Did SalishSeaCast results archives maintenance flowing from Susan's recent work to copy results to archive drives:
* deleted /results/SalishSeaCast/nowcast-blue.201905/*20/ and /results/SalishSeaCast/nowcast-blue.201905/*[jan|feb|mar]21/ to free up ~1Tb
* deleted /results/SalishSeaCast/nowcast-agrif.201702/*20/ and /results/SalishSeaCast/nowcast-agrif.201702/*[jan|feb|mar]21/ to free up ~0.6Tb
(SalishSeaCast)

Monthly project mtg.
Updated repos on graham.
Tried to build MOHID in StdEnv2020 on graham:
  module load nco/4.9.5
  module load netcdf-fortran/4.5.2
  module load python/3.8.2
  module load proj4-fortran -- FAILED!
(MIDOSS)


Thu 22-Apr-2021
^^^^^^^^^^^^^^^

ocean OS upgraded to 18.04 LTS

Managed get_NeahBay_ssh issue in automation; tested new workers; after nowcast-blue completion:
  pkill -f get_NeahBay_ssh  # killed spinning nowcast and forecast instances
  collect_NeahBay_ssh 06
  make_ssh_file nowcast
  upload_forcing arbutus ssh
Surprised that Neah Bay 12Z file was not available at ~09:30.
Backfilling nowcast-agrif:
  upload_forcing forecast2 2021-04-21
  upload_forcing nowcast+ 2021-04-21
  upload_forcing turbidity 2021-04-21
  make_forcing_links nowcast-agrif 2021-04-21
  wait for run to finish
  make_forcing_links nowcast-agrif 2021-04-22
Manager crashed and was restarted when collect_weather 18 tried to finish; recovery:
  pkill -f collect_weather
  collect_weather 00 2.5km &
  download_weather 00 1km &
  download_weather 12 1km &
Managed get_NeahBay_ssh issue in automation; tested new workers; after nowcast-blue completion:
  pkill -f get_NeahBay_ssh  # killed spinning nowcast and forecast instances
  collect_NeahBay_ssh 06
  make_ssh_file nowcast
  upload_forcing arbutus ssh
(SalishSeaCast)

Discussed skookum & salish OS upgrades w/ Charles on Slack; agreed on after 13:00 Fri afternoon.

Practice talks by Keegan & Aline; also Birgit, Elise & Tereza EGU pico-talks.

Zoom-coffee w/ Debby & Paul.

See work journal.
(Ocean Navigator)


Fri 23-Apr-2021
^^^^^^^^^^^^^^^

Booked COVID-19 vaccine appointment!

Morning mgmt of get_NeahBay_ssh issue in automation; after nowcast-blue completion:
  pkill -f get_NeahBay_ssh  # killed spinning nowcast and forecast instances
  collect_NeahBay_ssh 06
  make_ssh_file nowcast
  upload_forcing arbutus ssh
salish & skookum OS upgrades to 18.04 LTS.
Evening mgmt of get_NeahBay_ssh issue in automation; after 22:00:
  collect_NeahBay_ssh 00 2021-04-24
  make_ssh_file forecast2 2021-04-24
(SalishSeaCast)

Farewell MOAD social Zoom for Keegan & Aline.

Susan started shifting to CET for EGU conference.


Sat 24-Apr-2021
^^^^^^^^^^^^^^^

Morning mgmt of get_NeahBay_ssh issue in automation; after nowcast-blue completion:
  pkill -f get_NeahBay_ssh  # killed spinning nowcast and forecast instances
  collect_NeahBay_ssh 06
  make_ssh_file nowcast
  upload_forcing arbutus ssh
Evening mgmt of get_NeahBay_ssh issue in automation; after 22:00:
  collect_NeahBay_ssh 00 2021-04-25
  make_ssh_file forecast2 2021-04-25
(SalishSeaCast)

Drove to White Rock to visit M&J.


Sun 25-Apr-2021
^^^^^^^^^^^^^^^

Morning mgmt of get_NeahBay_ssh issue in automation; after nowcast-blue completion:
  pkill -f get_NeahBay_ssh  # killed spinning nowcast and forecast instances
  collect_NeahBay_ssh 06
  make_ssh_file nowcast
  upload_forcing arbutus ssh
Tried to backfill nowcast-dev; failed due to XIOS mofinding libmpihf; need to build new executables for new OS, I guess.
(SalishSeaCast)

Strained back after ToW stage 3 make-up Out & Back ride on Zwift.


Week 16
-------

Mon 26-Apr-2021
^^^^^^^^^^^^^^^

Week 58 of UBC work-from-home due to COVID-19

Deployed collect_NeahBay_ssh and make_ssh_file automation for testing before nowcast; failed; fixed lots of bugs; updated docs & process flow fig.
Added .gitattributes to SalishSeaNowcast to tell GitHub linguist tool to classify .ipynb files as Python to make repo landing page language statistics more accurate.
(SalishSeaCast)

Phys Ocgy seminars by co-op students.


Tue 27-Apr-2021
^^^^^^^^^^^^^^^

download_results forecast2 failed due to broken pipe; re-ran successfully at ~08:40.
collect_NeahBay_ssh and make_ssh_file worked successfully in automation for forecast2, nowcast, and forecast runs.

Worked on nowcast-dev:
  built new XIOS-2 executable:
    cd /SalishSeaCast/XIOS-2
    ./tools/FCM/bin/fcm build --clean
    ./make_xios --arch GCC_SALISH --netcdf_lib netcdf4_seq --job 8
  built new NEMO SalishSeaCast_Blue executable:
    cd /SalishSeaCast/NEMO-3.6-code/NEMOGCM/CONFIG
    XIOS_HOME=/SalishSeaCast/XIOS-2 ./makenemo -m GCC_SALISH -n SalishSeaCast_Blue clean
    XIOS_HOME=/SalishSeaCast/XIOS-2 ./makenemo -m GCC_SALISH -n SalishSeaCast_Blue -j8
  built new REBUILD_NEMO executable:
    cd /SalishSeaCast/NEMO-3.6-code/NEMOGCM/TOOLS/
    XIOS_HOME=/SalishSeaCast/XIOS-2 ./maketools -m GCC_SALISH -n REBUILD_NEMO clean
    XIOS_HOME=/SalishSeaCast/XIOS-2 ./maketools -m GCC_SALISH -n REBUILD_NEMO
      successful, but with warning:
        /usr/bin/ld: warning: libgfortran.so.3, needed by /usr/lib/libnetcdff.so, may conflict with libgfortran.so.4
  1st attempted run failed re: missing libmpi* that were present
  subsequenst attempts failed in xios:
    In file "memory.cpp", function "void xios::noMemory()",  line 9 -> Out of memory
(SalishSeaCast)

Filed tax returns.


Wed 28-Apr-2021
^^^^^^^^^^^^^^^

See work journal.
(Ocean Navigator)


Thu 29-Apr-2021
^^^^^^^^^^^^^^^

See work journal.
(Ocean Navigator)

FAL estate work: picked up draft from Scotia.

Charles shutdown skookum at 13:00 to replace failed drive in /opp array; restarted at ~14:55:
  sudo /opt/tomcat/bin/startup.sh
  source activate /SalishSeaCast/salishsea-site-env/
  supervisord -c /SalishSeaCast/salishsea-site/supervisord-prod.ini
  conda deactivate
  source activate /SalishSeaCast/nowcast-env
  supervisord -c $NOWCAST_CONFIG/supervisord.ini
  download_weather 18 2.5km
  download_weather 00 1km
  download_weather 12 1km
  collect_weather 00 2.5km
Started work on removing get_NeahBay_ssh worker; need to discuss failure recovery docs w/ Susan.
Noticed taht download_weather xx 1km worked without --no-verify-certs flag; checked https://dd.alpha.meteo.gc.ca on https://entrust.ssllabs.com/analyze.html and found that it appears to now support TLS 1.1; hacked next_workers.py on skookum to remove --no-verify-certs arg; restarted manager.
Charles rebooted skookum again at ~19:30; it failed to come up properly.
(SalishSeaCast)


Fri 30-Apr-2021
^^^^^^^^^^^^^^^

* silence PIL.PngImagePlugin logging
* patch for PreRules.am ??

See work journal.
(Ocean Navigator)

skookum had failed boot SSD and failed drive in /results that Charles replaced; back in operation at ~10:45; started recovery at ~11:05:
  sudo /opt/tomcat/bin/startup.sh
  source activate /SalishSeaCast/salishsea-site-env/
  supervisord -c /SalishSeaCast/salishsea-site/supervisord-prod.ini
  conda deactivate
  source activate /SalishSeaCast/nowcast-env
  supervisord -c $NOWCAST_CONFIG/supervisord.ini
  download_weather 00 2.5km
  collect_weather 18 2.5km
  download_weather 06 2.5km
  wait for forecast2 runs to finish
  download_weather 12 2.5km
download_weather hh 1km works in automation w/o --no-verify-certs flag; push change
download_results nowcast-green failed due to connection closed by arbutus; re-ran manually.
Fixed permissions in /opp where x bit got set for everything.
(SalishSeaCast)

Disabled cron job for daily runs.
(Bloomcast)


May
===

Sat 1-May-2021
^^^^^^^^^^^^^^

Cycled to convention centre to get 1st dose of Moderna COVID-19 vaccine.


Sun 2-May-2021
^^^^^^^^^^^^^^

Another drive failure in one of the RAID arrays on salish.


Week 16
-------

Mon 3-May-2021
^^^^^^^^^^^^^^

Week 59 of UBC work-from-home due to COVID-19

Changed docs repo default branch from master to main.
Email from Ali says that proj4-fortran pkg is now available in StdEnv/2020 on graham.
MOHID build mb1 build now fails w/ lots of errors in h5*() calls like:
  #### Mohid Base 1 ####
  src/ModuleHDF5.F90(494): error #6633: The type of the actual argument differs from the type of the dummy argument.   [STAT_CALL]
          call h5screate_f (H5S_SCALAR_F, space_id, STAT_CALL)
  --------------------------------------------------^
They appear to be due to STAT_CALL being declared as integer(HID_T) when HDF5 library signature says that it should be integer, and the 2020 compiler is pickier than the 2016 one was. After a bunch of editing to resolve this for STAT_CALL, rank & class_id variables, found that some code internal to MOHID is producing similar errors and, in consultation with Susan, decided to belay using StdEnv/2020 until we are forced to.
(MIDOSS)

Group mtg; see whiteboard.
(MOAD)

Phys Ocgy seminar.


Tue 4-May-2021
^^^^^^^^^^^^^^

Worked at ESB while Rita was at home.

Created https://github.com/MIDOSS/MIDOSS-MOHID-CODE/issues/9 re: MOHID build problems in graham StdEnv/2020.
Updated docs & Make-MIDOS-Forcing and started MOHID-Cmd re: using StdEnv/2016.4.
(MIDOSS)


Wed 5-May-2021
^^^^^^^^^^^^^^

Raisha officially joined the group; invited her to GitHub orgs.

Fixed broken link re: pip -e in docs; found by monthly linkcheck.
Added GitHub Actions shpinx-linkcheck workflow to MOHID-Cmd to run on 10th of the month.
(MOAD)

nowcast run got stuck at 32.6% complete; no obvious reason; stopped run, killed watch_NEMO, and restarted via make_forcing_links; restart took ~6 minutes for run_NEMO to execute.
(SalishSeaCast)


Thu 6-May-2021
^^^^^^^^^^^^^^

Arranged 1st on-boarding mtg w/ Raisha.
(Atlantis)

arbutus file system issues got resolved overnight with no explanation other than "closed" on status pages.
Backfilling:
  make_turbidity_file 2021-05-05 --debug
  upload_forcing arbutus turbidity --run-date 2021-05-05
  upload_forcing orcinus turbidity --run-date 2021-05-05
  upload_forcing graham turbidity --run-date 2021-05-05
  upload_forcing optimum turbidity --run-date 2021-05-05
  wait for nowcast-green run to finish
  upload_forcing arbutus nowcast+ --run-date 2021-05-06
  upload_forcing orcinus nowcast+ --run-date 2021-05-06
  upload_forcing graham nowcast+ --run-date 2021-05-06
  upload_forcing optimum nowcast+ --run-date 2021-05-06
  wait for nowcast, forecast, nowcast-green & wwatch3 runs to finish; wwatch3 nowcast will be from quiescent state
  make_forcing_links arbutus ssh 2021-05-05
  kill watch_Nemo forecast
  download_results arbutus forecast 2021-05-05
  launch_remote_worker arbutus make_ww3_wind_file arbutus forecast 2021-05-05
  launch_remote_worker arbutus make_ww3_current_file arbutus forecast 2021-05-05
  launch_remote_worker arbutus make_ww3_wind_file arbutus forecast 2021-05-06
  launch_remote_worker arbutus make_ww3_current_file arbutus forecast 2021-05-06
Lots of trouble getting fvcom to run; eventually figured out that at least one of the namelist files was truncated, probably during yesterday's write failures, I guess.
(SalishSeaCast)

Susan got her 1st dose of Pfizer COVID-19 vaccine.


Fri 7-May-2021
^^^^^^^^^^^^^^

Backfill fvcom runs:
  wait for today's runs to fail
  launch_remote_worker arbutus make_fvcom_boundary arbutus r12 nowcast 2021-05-06
  launch_remote_worker arbutus make_fvcom_boundary arbutus x2 nowcast 2021-05-06
  wait for forecast run to finish
  launch_remote_worker arbutus make_fvcom_boundary arbutus x2 nowcast 2021-05-07
Noticed that ONC SoG central node data stream resumed on 26-Mar.
Created UBC-MOAD/ariane-2.3.0_03 while helping Becca sort out Ariane build issues; started updating MOAD docs re: Ariane.
(SalishSeaCast)

Coffee w/ Becca.


Sat 8-May-2021
^^^^^^^^^^^^^^

Backfill fvcom runs:
  launch_remote_worker arbutus make_fvcom_boundary arbutus r12 nowcast 2021-05-07
(SalishSeaCast)

Drove to White Rock to visit M&J.


Sun 9-May-2021
^^^^^^^^^^^^^^

Woke up feeling like I had been hit by a truck; aches in neck, jaw, shoulder and legs; especially on left side; vaccine after-effects?

Backfill fvcom runs:
  decided to try letting x2 runs complete without competing w/ r12; nowcast took ~2h; forecast tool ~3h
  launch_remote_worker arbutus make_fvcom_boundary arbutus r12 nowcast 2021-05-08
  wait for r12 nowcast run to finish
  launch_remote_worker arbutus make_fvcom_boundary arbutus r12 nowcast 2021-05-09
(SalishSeaCast)

Fixed docs repo linkcheck failure due to ariane-2.3.0_03 being a private repo.
(MOAD)

Enabled VNC desktop sharing on matisse so that kudu can be my kvm between matisse and lizzy for photos work.


Week 17
-------

Mon 10-May-2021
^^^^^^^^^^^^^^^

Week 60 of UBC work-from-home due to COVID-19

Started work on proposal to DFO for funding to replace MEOPAR Prediction Core.
(SalishSeaCast)

Group mtg; see whiteboard.
(MOAD)

Phys Ocgy seminar

1st on-boarding session w/ Raisha:
* compute resources and model runs
* ssh intro; homework to do ssh setup
(Atlantis)


Tue 11-May-2021
^^^^^^^^^^^^^^^

Helped Charles test & debug workstation OS upgrades and slow connection issue.

Experimented with VS-Code remote ssh extension on tyee and graham.

Updated base conda env on kudu to Python=3.9.4.

Experimented with VS-Code as my general purpose editor instead of Sublime Text.
* restructuredtext extension now supports code completions and Sphinx preview

Continued work on proposal to DFO for funding to replace MEOPAR Prediction Core.
(SalishSeaCast)


Wed 12-May-2021
^^^^^^^^^^^^^^^

Added long missing fvcom-forecast option to ping_erddap worker.
Continued work on proposal to DFO for funding to replace MEOPAR Prediction Core.
Used https://vrlatech.com/raid-calculator/ to back out present disk sizes:
* /backup: 3x6Tb RAID0 =  17Tb
* /backup2: 1x16Tb no RAID = 15Tb + 100Gb partitioned as /SalishSeaCast
* /results: 3x10Tb RAID5 = 19Tb
* /results2: 4x14Tb RAID5 = 39Tb
* /data: 4x14Tb RAID5 = 37Tb (not sure why it is 1Tb smaller than /results2)
* /opp: 3x10Tb RAID5 = 19Tb
My notes from 18-Oct-2019 imply that all bays on salish and skookum are full, and that storage chassis has 4 free bays, but we could free 2 bays by replacing /backup with 1 large drive.
So, we have 18 drives across the 3 chassis:
* 3 x 6Tb
* 6 x 10 Tb
* 8 x 14 Tb
* 1 x 16Tb
Largest available drives presently on Memory Express site are 18Tb for $760 + taxes = $850.
3x18Tb RAID5 = 33Tb
4x18Tb RAID5 = 49Tb
Plan for 18 x 18Tb = $15,300 + 2 x 18Tb cold spares = $17,000:
* /backup: 2x18Tb RAID0 =  33Tb
* /backup2: 2x18Tb RAID0 = 33Tb + 100Gb partitioned as /SalishSeaCast
* /results: 3x18Tb RAID5 = 33Tb
* /results2: 4x18Tb RAID5 = 49Tb
* /data: 4x18Tb RAID5 = 49Tb
* /opp: 3x18Tb RAID5 = 33Tb
This consumes the 2 bays freed by replacing 3x6Tb /backup to expand /backup & /backup2 but preserves 4 bays in storage chassis for data shuffles (build new array in empty bays, rsync data to it, free bays used by old array)
(SalishSeaCast)


Thu 13-May-2021
^^^^^^^^^^^^^^^

Added long missing fvcom-x2-nowcast & fvcom-r12-nowcast options to ping_erddap worker and next_workers module.
nowcast-agrif failed due to inifiband issue; re-tried successfully.
Continued work on proposal to DFO for funding to replace MEOPAR Prediction Core.
(SalishSeaCast)

2nd on-boarding session w/ Raisha:
* GitHub orgs and automation
* Git configuration
* bash configuration
* miniconda and conda envs
(Atlantis)


Fri 14-May-2021
^^^^^^^^^^^^^^^

Continued work on proposal to DFO for funding to replace MEOPAR Prediction Core.
(SalishSeaCast)


Sat 15-May-2021
^^^^^^^^^^^^^^^

Goofed off.


Sun 16-May-2021
^^^^^^^^^^^^^^^

nowcast-agrif failed twice due to inifiband issue.
Continued work on proposal to DFO for funding to replace MEOPAR Prediction Core.
(SalishSeaCast)

Cycled to Fraser River Park and back (16km)


* silence PIL.PngImagePlugin logging
* patch for PreRules.am ??





Backfill nowcast-dev:

  make_forcing_links salish nowcast+ --shared-storage 2021-04-23
  make_forcing_links salish nowcast+ --shared-storage 2021-04-24
  make_forcing_links salish nowcast+ --shared-storage 2021-04-25
  make_forcing_links salish nowcast+ --shared-storage 2021-04-26
  make_forcing_links salish nowcast+ --shared-storage 2021-04-27
  make_forcing_links salish nowcast+ --shared-storage 2021-04-28
  make_forcing_links salish nowcast+ --shared-storage 2021-04-29
  make_forcing_links salish nowcast+ --shared-storage 2021-04-30
  make_forcing_links salish nowcast+ --shared-storage 2021-05-01
  make_forcing_links salish nowcast+ --shared-storage 2021-05-02
  make_forcing_links salish nowcast+ --shared-storage 2021-05-03




TODO: when we can change to CC StdEnv/2020:
* XIOS-ARCH:
  * merge cc-stdenv-2020 branch
* NEMO-Cmd:
  * merge cc-stdenv-2020 branch
  * release v21.1
  * bump to v21.2.dev0
* SalishSeaCmd:
  * merge cc-stdenv-2020 branch
  * release v21.1
  * bump to v21.2.dev0
* finalize message in #general channel
  * mention new module load versions re: .bashrc





Update ONC URLs to https://data.oceannetworks.ca/



Update cookiecutter-MOAD-pypkg re: hg -> git


jupyter kernelspec uninstall unwanted-kernel



TODO:

https://linuxize.com/post/getting-started-with-tmux/

update deployment docs re: spinning up a new compute node


OPPTools PRs:
  add numpy-indexed dependency
  fix pyproj.Proj() initializations
  fix nctime().strftime in OPPTools.utils.fvcom_postprocess.vertical_transect_snap()


Add CI workflows to run linkcheck on docs; see SalishSeaCast#repos-maint channel:
  need sphinx>3.1 in env
  example workflow in salishsea-site repo
  don't forget to add sphinx & sphinx_rtd_theme to environment-test.yaml
  See: https://salishseacast.slack.com/archives/C01GYJBSF0X/p1608574921004500


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