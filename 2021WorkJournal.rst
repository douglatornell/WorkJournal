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
Checked hake & halibut that Aline & Keegan will use for /results, /results2 & /data mounts; opened ticket to get /results2 and /data mounted on hake.
Uploaded LinuxCommandLine.pdf to Google Drive.
(SalishSeaCast)

See work journal.
(Ocean Navigator)


Wed 6-Jan-2021
^^^^^^^^^^^^^^

See work journal.
(Ocean Navigator)

Joined initial on-boarding Zoom for Aline & Keegan joining MOAD to work with Elise & Karyn.
(SalishSeaCast)

FAL estate work: deposit BCE & MFC Q4 cheques; pay MCL CRA balance owing.

Wrote preliminary bash config section in MOAD docs.
(MOAD)


Thu 7-Jan-2021
^^^^^^^^^^^^^^

Did computing on-boarding session w/ Aline & Keegan; chaotic due to /ocean failures and no Linux accounts for them yet.
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

Work at UBC while  is at home.

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
Pinged Elise re: discussion classes, inhence & dependency injection.
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

Continued nowcast-agrif backfilling:
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

Helped Susan update OS on Galago Pro from 19.10 to 20.10 via 20.04.

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

nowncast-agrif stopped 11 minutes into run; nothing obvious in ocean.output; "SISTER_EOF attempting to communicate with sister MOM's" in stderr; re-ran
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

Work at UBC while  is at home.

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
* watch_NEMO forecast failed to launch due to orphaned watch_NEMO nowcast:
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

Week 49 of UBC work-from-home due to COVID-19

**Statutory Holiday** - Family day

Added GHA sphinx linkcheck workflow to SalishSeaCast/docs repo; scheduled for 8th day of month.
Discovered that docs repo has no copyright notices, only CC-By license.
Updated Olson, et al citation from unpublished.
(SalishSeaCast)


Tue 16-Feb-2021
^^^^^^^^^^^^^^^

Finalized docs repo GHA linkcheck workflow monthly schedule after successful scheduled test overnight.
Checked on ONC ferry and SCVIP data flows; both still down; looked at their new forum and status sites.
Investigated hindcast_dayavgs metadata problem; resolved by dropping bounds_nav_[lat|lon] variables present in some NEMO results files; ran hindcast_dayavgs for 2020-02-15 to 2020-12-31.
(SalishSeaCast)

Brought Make-MIDOSS-Forcing repo up to date; merged monte-carlo branch that adds "salishseacast grid" item to YAML config instead of hard-coded ERDDAP URL so that it can work on graham compute nodes w/o network access by using a path to a clone of the SalishSeaCast/grid repo.
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
* Make-MIDOSS-Forcing: up to date
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
Fixed SyntaxWarnings re: string equality test in Make-MIDOSS-Forcing; restricted pkg to Python 3.8.
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

Week 50 of UBC work-from-home due to COVID-19

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
  * started modernize branch in SoG-Bloomcast-Ensemble to modernize packaging in hopes that will resolve unfound ensemble plug-in issue
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
    Failed w/ infiband error; re-ran successfully
  make_forcing_links orcinus-nowcast-agrif nowncast-agrif 2021-02-26
(SalishSeaCast)

Ran bloomcast manually to investigate profiles plotting error; profiles/hoff_2021_bloomcast.out_* files are empty
Pushed changes to use scaled flow from Nanaimo River at Cassidy gauge as replacement for Englishman.
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

nowcast-agrif failed ~14% into run; infiniband error; re-ran successfully
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

Week 51 of UBC work-from-home due to COVID-19

Susan reviewed results of yeaterday's bloomcast run w/ correctly scaled Nanaimo River and accepted them for SoPO presentation.
Committed cronjob.sh updates; env path & --debug flag.
(bloomcast)

nowcast-agrif failed very early in run; infiniband error; re-ran successfully
Deleted stale branches in NEMO-Cnd and SalishSeaCmd repos on GitHub
(SalishSeaCast)

Finalized Lagrangian.dat file templates for Monte Carlo runs:
* mv Lagrangian_BunkerC_crude.dat Lagrangian_bunker.dat
* mv Lagrangian_CLB_crude.dat Lagrangian_dilbit.dat
* ln -s Lagrangian_diesel.dat Lagrangian_gas.dat
* ln -s Lagrangian_diesel.dat Lagrangian_jet.dat
* ln -s Lagrangian_diesel.dat Lagrangian_other.dat
Replied to Rachael's request for terminal in random spills CSV with suggestion to use MMSI and date/time.
Deleted MIDOSS-MOHID-config add-make-hdf5 branch.
Deleted Make-MIDOSS-Forcing monte-carlo branch.
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

Worked on changes to get_onc_ferry worker to add nearest NEMO grid ji indices to datasets; refactored unit tests.
(SalishSeaCast)


Sun 7-Mar-2021
^^^^^^^^^^^^^^

Worked on changes to get_onc_ferry worker to add nearest NEMO grid ji indices to datasets; refactored nav coord resampling; generated sample file for Susan to check.
(SalishSeaCast)


Week 10
-------

Mon 8-Mar-2021
^^^^^^^^^^^^^^

Week 52 of UBC work-from-home due to COVID-19

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

Week 53 of UBC work-from-home due to COVID-19

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

Fixed docs linkcheck issues in Make-MIDOSS-Forcing.
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

Merged PRs from Dependabot re: bump Pillow to 8.1.1 to address memory exhaustion DOS security vulnerability:
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

Week 54 of UBC work-from-home due to COVID-19

Managed get_NeahBay_ssh issue in automation; after nowcast-blue completion:
  pkill -f get_NeahBay_ssh  # killed spinning nowcast and forecast instances
  upload_forcing arbutus ssh
  upload_forcing orcinus nowcast+
  upload_forcing graham nowcast+
  upload_forcing optimum nowcast+
(SalishSeaCast)

Group mtg; see whiteboard.
(MOAD)

Squash-merged Dependabot PRs:
* jinja to 2.11.3:
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
* urllib3 to 1.26.3
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
3. Continue graham migration to StdEnv/2020:
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

Week 55 of UBC work-from-home due to COVID-19

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
Test run of SalishSeaCast nowcast-green on graham in StdEnv/2020:
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

Week 56 of UBC work-from-home due to COVID-19

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
    failed on HalfmoonBay due to: AttributeError: 'Float64Index' object has no attribute 'tz_convert'
  make_plots fvcom nowcast publish
(SalishSeaCast)

Squash-merged Dependabot PRs re: bump urllib3 to 1.26.4:
* UBC-MOAD/docs
* UBC-MOAD/moad_tools
* 43ravens/NEMO_Nowcast
* MIDOSS/MOHID-Cmd
* MIDOSS/Make-MIDOSS-Forcing
* SalishSeaCast/tools
* SalishSeaCast/SalishSeaNowcast
* SalishSeaCast/SOG-Bloomcast-Ensemble
* SalishSeaCast/salishsea-site
(MOAD)


Thu 8-Apr-2021
^^^^^^^^^^^^^^

Rebooted nowcast0 at ~08:30 and it failed with:
  Error: Failed to perform requested operation on instance "nowcast0", the instance has an error status: Please try again later [Error: libvirtError].
Did a shutdown on the instance and tried to restart it, but it kept erroring out; sent email to cloud@. Response at ~10:30 from Jeff Albert; problem was related to persistent volume attachment; he manually re-attached the volume and the instance booted. Recovery:
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
Resumed work on getting NEMO and FVCOM water level figures to work w/ new CHS IWLS API obs and predictions; figures all working now, I think; uncommitted code on skookum to test in automation.
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

Week 57 of UBC work-from-home due to COVID-19

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

Noticed that GitHub have added:
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

Week 58 of UBC work-from-home due to COVID-19

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
Tried to backfill nowcast-dev; failed due to XIOS not finding libmpihf; need to build new executables for new OS, I guess.
(SalishSeaCast)

Strained back after ToW stage 3 make-up Out & Back ride on Zwift.


Week 17
-------

Mon 26-Apr-2021
^^^^^^^^^^^^^^^

Week 59 of UBC work-from-home due to COVID-19

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
Noticed that download_weather xx 1km worked without --no-verify-certs flag; checked https://dd.alpha.meteo.gc.ca on https://entrust.ssllabs.com/analyze.html and found that it appears to now support TLS 1.1; hacked next_workers.py on skookum to remove --no-verify-certs arg; restarted manager.
Charles rebooted skookum again at ~19:30; it failed to come up properly.
(SalishSeaCast)


Fri 30-Apr-2021
^^^^^^^^^^^^^^^

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


Week 18
-------

Mon 3-May-2021
^^^^^^^^^^^^^^

Week 60 of UBC work-from-home due to COVID-19

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
Updated docs & Make-MIDOSS-Forcing and started MOHID-Cmd re: using StdEnv/2016.4.
(MIDOSS)


Wed 5-May-2021
^^^^^^^^^^^^^^

Raisha officially joined the group; invited her to GitHub orgs.

Fixed broken link re: pip -e in docs; found by monthly linkcheck.
Added GitHub Actions shpinx-linkcheck workflow to MOHID-Cmd to run on 10th of the month.
(MOAD)

nowcast run got stuck at 32.6% complete; no obvious reason; stopped run, killed watch_NEMO, and restarted via make_forcing_links; restart took ~6 minutes for run_NEMO to execute.
Eventually learned from status page that arbutus was hving file system issues.
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


Week 19
-------

Mon 10-May-2021
^^^^^^^^^^^^^^^

Week 61 of UBC work-from-home due to COVID-19

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
* salish (full), hardware RAID controllers for salish & storage chassis
  * /backup: 3x6Tb RAID0 =  17Tb
  * /data: 5x10Tb RAID5 = 37Tb
* skookum (full), software RAID
  * /results: 3x10Tb RAID5 = 19Tb
* storage chassis (8 bays free), RAID controller in salish
  * /opp: 3x10Tb RAID5 = 19Tb
  * /backup2: 1x16Tb no RAID = 15Tb + 100Gb partitioned as /SalishSeaCast
  * /results2: 4x14Tb RAID5 = 39Tb
My notes from 18-Oct-2019 imply that all bays on salish and skookum are full, and that storage chassis has 4 free bays (corrected when I found paper that says 8), but we could free 2 bays by replacing /backup with 1 large drive.
So, we have 19 drives across the 3 chassis:
* 3 x 6Tb
* 11 x 10 Tb
* 4 x 14 Tb
* 1 x 16Tb
Largest available drives presently on Memory Express site are 18Tb for $760 + taxes = $850.
3x18Tb RAID5 = 33Tb
4x18Tb RAID5 = 49Tb
Plan for 19 x 18Tb = $15,300 + 1 x 18Tb cold spares = $17,000:
* salish (2 free bays), 2 hardware RAID controllers:
  * /backup: 2x18Tb RAID0 =  33Tb
  * /data: 4x18Tb RAID5 = 49Tb
* skookum (full), software RAID
  * /results: 3x18Tb RAID5 = 33Tb
* storage chassis (7 free bays)
  * /backup2: 2x18Tb RAID0 = 33Tb + 100Gb partitioned as /SalishSeaCast
  * /results2: 4x18Tb RAID5 = 49Tb
  * /opp: 3x18Tb RAID5 = 33Tb
This preserves at least 4 bays in storage chassis for data shuffles (build new array in empty bays, rsync data to it, free bays used by old array)
(SalishSeaCast)


Thu 13-May-2021
^^^^^^^^^^^^^^^

Added long missing fvcom-x2-nowcast & fvcom-r12-nowcast options to ping_erddap worker and next_workers module.
nowcast-agrif failed due to infiniband issue; re-tried successfully.
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

nowcast-agrif failed twice due to infiniband issue.
Continued work on proposal to DFO for funding to replace MEOPAR Prediction Core.
(SalishSeaCast)

Cycled to Fraser River Park and back (16km)


Week 20
-------

Mon 17-May-2021
^^^^^^^^^^^^^^^

Week 62 of UBC work-from-home due to COVID-19

Continued work on proposal to DFO for funding to replace MEOPAR Prediction Core; sent draft to Richard @ONC re: letter of support; he asked for words; Susan and I drafted & sent them
nowcast-agrif failed due to no run yesterday; recovery:
  make_forcing_links orcinus-nowcast-agrif nowncast-agrif 2021-05-16
    failed again w/ Infiniband errors; hacked PBS script to add `#PBS -l partition=QDR` as recommended by Mark Thachuk; Used VSCode remotely on skookum to hack on run_NEMO_agrif.
  make_forcing_links orcinus-nowcast-agrif nowncast-agrif 2021-05-17
Did svn checkout of https://forge.ipsl.jussieu.fr/ioserver/svn/XIOS/branchs/xios-2.5 to salish:/ocean/dlatorne/MEOPAR/xios-2.5/; tweaked arch files to get successful build; build NEMO and REBUILD_NEMO against xios-2.5; 23apr21 run failed with:
  > Error [void noMemory(void)] : In file '/ocean/dlatorne/MEOPAR/xios-2.5/src/memory.cpp', line 9 -> Out of memory
like XIOS-2 version did.
Realized that arbutus VMs are 18.04 and gcc-7.5 (same as salish is now), so NEMO/XIOS issue shouldn't be compiler-related.
fvcom-nowcast-r12 failed at ~12:00, apparently due to fvcom2 VM crashing; restarted VM at ~20:45; re-launched run
(SalishSeaCast)

Group mtg; see whiteboard.
(MOAD)

Phys Ocgy seminar by Ken Ashley re: Fraser River Estuary.


Tue 18-May-2021
^^^^^^^^^^^^^^^

Worked at ESB while Rita was at home.

Found paper notes about storage drives; photo in Slack #proposal channel; updated 12-May-2021 notes re: DFO proposal planning; assuming that price drop by early 2022 will let us buy 19x18Tb drive instead of 18 in proposal budget.
Realized that yesterday's test of nowcast-dev didn't use xios-2.5; copied executable into /SalishSeaCast/XIOS-2/bin/; same out of memory failure; played w/ XIOS config in iodef.xml; always same out of memory failure.
NEMO forecast and nowcast-green runs were very slow.
(SalishSeaCast)

Susan set up SS-Atlantis GitHub org and made me a co-owner.
(Atlantis)


Wed 19-May-2021
^^^^^^^^^^^^^^^

Wrote paragraph about SalishSeaCast storage arrays expansion for proposal.
NEMO forecast and nowcast-green runs were very slow again.
(SalishSeaCast)

FAL estate work: death claim form to Desjardins.

Coffee with Karyn.

Squash-merged dependabot PRs in douglatornell/async-tutorial and douglatornell/randopony repos.
Disabled dependabot alerts & PRs in douglatornell/async-tutorial repo.
Archived douglatornell/randopony repo.


Thu 20-May-2021
^^^^^^^^^^^^^^^

NEMO forecast and nowcast-green runs were very slow again.
(SalishSeaCast)

See work journal.
(Resilient-C)

1st Salish Sea Atlantis project mtg:
* Susan, me, Raisha, Sara, Natalie, Javier, Beth, Jess
* Discussion points
- Welcome and intros, including how members of the team fit together
- Overview of the model code, including workflow, what's been done so far, technical considerations and plans for tech transfer/code sharing between CISRO/UBC
- Model updates - particularly in terms of the contaminants module, how it is running and next steps
- Expectations for the coming months - particularly in the context of Raisha's role, but also for the project as a whole.
- Q&A on all things relating to running the model 
- Anything else you would like to discuss 
* Intros
* Model state:
  * running
  * salmon life cycle is still problematic
  * presently running scenarios
    * Johnstone Strait
    * Vancouver Harbour Dilbit
    * ferries
    * Turn Point
  * using OceanParcels
  * config is on Bitbucket
  * planning weekly mtgs initially
* Raisha's role
  * scenario dev
* SS-Atlantis run time is ~1 core-hr per model year
* OceanParcels on HPC it much more intensive: 2 days of HPC walltime wasn't enough for a recent Javier project
(Atlantis)

Worked through more ariane build issues w/ Susan; adding a bin-like directory to prefix gets rid of errors from doc/ and examples/ that confused Becca.
(SalishSeaCast)


Fri 21-May-2021
^^^^^^^^^^^^^^^

NEMO forecast and nowcast-green runs were very slow again.
(SalishSeaCast)

Explored SS-Atlantis config repo (https://bitbucket.csiro.au/users/por07g/repos/salish-sea-atlantis-model/) on CSIRO Bitbucekt server.
(Atlantis)

See work journal.
(Resilient-C)


Sat 22-May-2021
^^^^^^^^^^^^^^^

Drove to White Rock to visit M&J.

Goofed off.


Sun 23-May-2021
^^^^^^^^^^^^^^^

Cycled River Rd out & back w/ explorations on Queens Canal trail and 8 Rd (50 km)

Started planning Minecraft 1.17 base w/ Susan.


Week 21
-------

Mon 24-May-2021
^^^^^^^^^^^^^^^

Week 63 of UBC work-from-home due to COVID-19

**Statutory Holiday** - Victoria Day

Tried to resume work on getting phpgedview running on Opalstack; not much progress.

Set up new SADA-dev server on CubedHost w/ deep flat creative world for planning 1.17 base.


Tue 25-May-2021
^^^^^^^^^^^^^^^

Set up new runs timing sheet on kudu desktop to track mitigation of recent slow run time after NEMO nowcast:
    NEMO nowcast-blue took expected ~24min
    Killed VHFR nowcast-x2 and nowcast-r12 runs after NEMO forecast started to test io contention hypothesis; NEMO NEMO forecast run sped up from <3%/5min to ~15%/5min
    NEMO forecast took ~41min, slightly longer than the expected ~36min, presumably due to contention w/ VHFR runs for first ~5min
    NEMO nowcast-green took 1h7min, slightly shorter than the expected 1h15min
    wwatch3 nowcast took ~22min, almost exactly the same as yesterday, and almost exactly as expected
    wwatch3 forecast took ~33min, almost exactly the same as yesterday, and almost exactly as expected
    ran VHFR runs sequentially after NEMO & wwatch3 runs finished
    VHFR nowcast-x2 took ~2h, similar to 2019 concurrent w/ nowcast-green, but w/o r12
    VHFR forecast-x2 took ~3h, similar to 2019 concurrent w/ nowcast-green, but w/o r12, and as expected
    VHFR nowcast-r12 took ~7h21nin, similar to 2019 backfill run after forecast-x2
(SalishSeaCast)

Tried to help Birgit with her uninitialized variable issue.
(Arctic)

Updated cookiecutter-analysis-repo re: SS-Atlantis GitHub org.
Worked on MOAD docs re: installation of Miniconda.
(MOAD)
    
    
Wed 26-May-2021
^^^^^^^^^^^^^^^
    
Continued experiments on runs concurrency re: recent slow run times (see timeing sheet):
    NEMO nowcast-blue took expected ~24min
    Killed VHFR nowcast-r12 ~5min after it started, leaving nowcast-x2 concurrnt w/ NEMO forecast
    NEMO forecast took ~42min, slightly longer than the expected ~36min, presumably due to contention w/ VHFR r12 for first ~5min
    NEMO nowcast-green took 1h7min, same as yesterday, slightly shorter than the expected 1h15min
    VHFR nowcast-x2 concurrent w/ NEMO runs took ~2h, very slightly longer than yesterday, not sure if that is due to contention w/ r12 for first ~5min or w/ NEMO & wwatch3 runs, similar to 2019 concurrent w/ nowcast-green, but w/o r12
    wwatch3 nowcast took ~22min, almost exactly the same as yesterday, and almost exactly as expected
    wwatch3 forecast took ~34min, almost exactly the same as yesterday, and almost exactly as expected
    VHFR forecast-x2 took ~3h, almost exactly the same as yesterday, and almost exactly as expected
    VHFR nowcast-r12 took ~7h18nin, almost exactly the same as yesterday, and almost exactly as expected
(SalishSeaCast)

Slack mtg w/ Rasisha re: workflow for Atlantis:
* Discussed workflow for using BitBucket repo; need to discuss w/ Javier
* attempt to run SS model is failing on open SS_init.nc due to invalid netCDF format; rabbit hole about libnetcdf version options on Raisha's Mac
Question for Javier/Beth:
* Does Atlantis have restart? possible, but not fully implemented; lots of manual work.
Investigated warnings that I had to suppress to get build to work with gcc-9.3.0:
    -WARN += -Wformat-overflow
    +WARN += -Wno-format-overflow
        re: buffer overflow avoidance?
    +WARN += -Wno-unused-result
        re: maybe buffer overflow avoidance?
    +WARN += -Wno-stringop-truncation
        re: buffer overflow avoidance?
    +WARN += -Wno-stringop-overflow
        re: buffer overflow avoidance?
Set up atlantis-dev env on tyee and experimented with VSCode tasks etc.
(Atlantis)


Thu 27-May-2021
^^^^^^^^^^^^^^^

Dentist hygene appt (first since Feb-2020).

Repeated yesterday's pattern for runs, pushing VHFR nowcast-r12 to after forecast-x2.
Changed next_workers to launch VHFR nowcast-r12 after forecast-x2 instead of concurrently with nowcast-x2; deployed to skookum.
(SalishSeaCast)

Worked through miniconda installation, VSCode remote-ssh setup, and atlantis-dev env build w/ Raisha.
(Atlantis)


Fri 28-May-2021
^^^^^^^^^^^^^^^

Changed MPI hosts files and nowcast config on arbutus to run forecast-x2 on 45 cores and nowcast-r12 on 90 cores; forecast-x2 was ~15min slower than the past 3 days; nowcast-r12 is trending towrds ~75min faster than the past 3 days
(SalishSeaCast)


Sat 29-May-2021
^^^^^^^^^^^^^^^

nowcast-blue ran at normal speed, or slightly faster.
forecast concurrent with nowcast-x2 on 45 cores both ran slow.
Changed MPI hosts files and on arbutus to run to remove fvcom2 VM from hosts in use because adding it to x2 hosts coincided with slow-down of forecast-x2 yesterday and today's slowness; maybe it is root cause of all recent slowness.
(SalishSeaCast)


Sun 30-May-2021
^^^^^^^^^^^^^^^

Cycled to Colony Farm; discovered that much of its west side is closed for equipment staging for the TMX Fraser River crossing :-(   (64km)

VHFR runs were a complete mess; yesterday's r12 didn't finish before nowcast-x2 tried to run on 2 of the same VMs; killed them at ~18:15 and started over w/ config from 27may21.
(SalishSeaCast)


Week 22
-------

Mon 31-May-2021
^^^^^^^^^^^^^^^

Week 64 of UBC work-from-home due to COVID-19

After yesterday's VHFR disaster, returned config & mpihosts.fvcom.x2 to 30 cores on fvcom[01] because 45 cores seems slightly slower; returned mpihosts.fvcom.r12 to 90 cores including fvcom2 and fvcom0 as extra; backfilled 29-30may:
    wait for 31may r12 run to fail at ~14:45
    launch_remote_worker arbutus make_fvcom_boundary "arbutus r12 nowcast --run-date 2021-05-29"
    wait for run to finish
    launch_remote_worker arbutus make_fvcom_boundary "arbutus r12 nowcast --run-date 2021-05-30"
(SalishSeaCast)

Tried to understand why atlantis code would call fgets() w/o using result, necessitating use of -Wno-unused-result.
(Atlantis)

Worked on borg backup scripts on salish.
Disabled cron scripts that are throwing error emails at root.
Re-created /backup/borg/ that Charles wiped during updates.
Created emergency reserved space for use in the event that borg fills drive:
  sudo fallocate -l 2G /backup/borg/emergency_reserved_space
Initialized /backup/borg/opp:
  sudo borg init --encryption=none /backup/borg/opp
Changed /etc/cron.daily/daily-opp-backup.sh to use --compression auto,zstd instead of lz4.
Ran initial backup of /opp/observations/; ran again to add /opp/wwatch3/nowcast to test exclusion of --list option;


June
====

Tue 1-Jun-2021
^^^^^^^^^^^^^^

Worked at ESB while Rita is at home.

Slack call w/ Raisha:
* build and run atlantis on tyee
* discussed branch workflow for Bitbucket config repo
* gave her docs to create SS-Atlantis/analysis-raisha
* next step: R notebook kernel - low priority
(Atlantis)

Backfilling nowcast-r12:
    wait for 1jun21 run to fail
    launch_remote_worker arbutus make_fvcom_boundary "arbutus r12 nowcast --run-date 2021-05-31"
    wait for run to finish
    launch_remote_worker arbutus make_fvcom_boundary "arbutus r12 nowcast --run-date 2021-06-01"
Worked on nowcast-dev on salish:
    * compared ldd of xios to arbutus and found that salish has and earlier version libnetcdf and libhdf5 instead of libhdf5_serial; discovered that salish has libnetcdf in /usr/lib/ and /usr/lib/x86_64-linux-gnu/; libhdf5 and libhdf5_serial are in the latter
    * started a slack thread to ask Charles about lib cross-ups on salish
(SalishSeaCast)


Wed 2-Jun-2021
^^^^^^^^^^^^^^

Charles thinks that salish libnetcdf issue could be due to PPA install of libs in 2014.
Backfilling nowcast-r12:
  wait for 1jun21 run to fail
  launch_remote_worker arbutus make_fvcom_boundary "arbutus r12 nowcast --run-date 2021-06-01"
  wait for run to finish
  launch_remote_worker arbutus make_fvcom_boundary "arbutus r12 nowcast --run-date 2021-06-02"
(SalishSeaCast)

Squash-merged dependabot PRs re: urllib3 in UBC-MOAD/cookiecutter-analysis-repo, UBC-MOAD/moad_tools, UBC-MOAD/docs, UBC-MOAD/cookiecutter-MOAD-pypkg, MIDOSS/MOHID-Cmd, MIDOSS/Make-MIDOSS-Forcing, MIDOSS/docs
(MOAD)

Debrief from Sara about mtg w/ First Nations Fisheries Council (FNFC):
* response exercise in 2022; Sooke FN; planning starting in mid-Jun
* Nuchalnuth interest in model because they were caught off guard by leak; Susan talked about Michael saying that DFO is looking at relocatable model for deployment over wrecks
* ITAN knowledge sharing platform
(Atlantis)

Finally went to LifeLabs for tests requisitioned by Dr. Tim in mid-Feb.


Thu 3-Jun-2021
^^^^^^^^^^^^^^

nowcast-r12 backfilling finished overnight; now running on 90 cores (6 VMs, added fvcom0), starting after forecast-x2; ~6h run time, so total run time ~11h is consistent with concurrent configuration before slowdown on 18May21 but nowcast-x2 and forecast-x2 now finish earlier.
Committed change from 75 to 90 cores for nowcast-r12 and deployed it to arbutus.
Started work on ERDDAP dataset of month-averaged tracers for stakeholders:
* ncra calculates the month-averaged fields; Susan has this worked out in /data/sallen/results/MEOPAR/averages/
* tracers are spread across 5 files:
SalishSea_1m_200701_200701_carp_T.nc
SalishSea_1m_200701_200701_dia2_T.nc
SalishSea_1m_200701_200701_grid_T.nc - done
SalishSea_1m_200701_200701_prod_T.nc
SalishSea_1m_200701_200701_ptrc_T.nc - done
* lots of mucking around with ncks, ncrcat & necat lead me to conclude that NCO can't merge selected variables from collections of files like those
* crafted ubcSSg3DTracerFields1moV19-05 dataset XML from ubcSSg3DTracerFields1hV19-05 but it failes to load due to:
java.lang.RuntimeException: datasets.xml error on or before line #10012: AxisVariable=time has tied values; fixed by Susan; issue was ERDDAP recursing into sub-dirs
Squash-merged dependabot PRs re: urllib3 in SalishSeaCast/ docs, tools, SOG-Bloomcast-Ensemble, analysis-doug, salishsea-site, SalishSeaCmd, NEMO-Cmd, SalishSeaNowcast.
(SalishSeaCast)

Coffee w/ Elise.

Dentist appt to get gum patch replaced.

Deleted /project/def-allen/dlatorne/GEOTRACES/ and MEOPAR/hg/ on graham to back away from group file count quota.
(MOAD)


Fri 4-Jun-2021
^^^^^^^^^^^^^^

Continued work on ERDDAP dataset of month-averaged tracers for stakeholders:
* decided to store month-averaged files in /results/SalishSea/month-avg.201905/; Susan moved files
* finalized release of ubcSSg3DTracerFields1moV19-05 dataset
* crafted ubcSSg3DBiologyFields1moV19-05 dataset XML from ubcSSg3DBiologyFields1hV19-05 and released it on ERDDAP
(SalishSeaCast)

Estate work:
* confirmed w/ AST that Jamie has to provide notarized signature on waiver
* BCE can only be transferred, even in my DRIP account they would not be DRIP shares, DRS (Direct Registration System) statement will allow me to move them to a brokerage account for action

Discussed midoss-app-dev deployment w/ Ben on Slack.
(MIDOSS)


Sat 5-Jun-2021
^^^^^^^^^^^^^^

upload_forcing to orcinus failed for nowcast+ and turbidity; orcinus was still unresponsive at 15:35
(SalishSeaCast)

Drove to White Rock to visit M&J; spent most of the visit on the roof decks.


Sun 6-Jun-2021
^^^^^^^^^^^^^^

upload_forcing to orcinus failed for nowcast+ and turbidity
(SalishSeaCast)


Week 23
-------

Mon 7-Jun-2021
^^^^^^^^^^^^^^

Week 65 of UBC work-from-home due to COVID-19

orcinus is accepting connections again; backfilled nowcast-agrif:
* wait for 7jun21 run to fail
* upload_forcing orcinus nowcast+ --run-date 2021-06-05
* upload_forcing orcinus turbidity --run-date 2021-06-05
* wait for run to finish
* upload_forcing orcinus nowcast+ --run-date 2021-06-06
* upload_forcing orcinus turbidity --run-date 2021-06-06
* wait for run to finish
* upload_forcing orcinus turbidity --run-date 2021-06-07
Removed option to clone via HTTPS from a couple of repo's docs:
  SalishSeaCast/rpn-to-gemlam
  SalishSeaCast/FVCOM-Cmd
Did git archeology to try to figure out if it is safe to pull SS-run-sets HEAD on arbutus to get rev 656d78d:
| Author: Susan Allen <sallen@eoas.ubc.ca>
| Date:   Thu Mar 11 11:10:01 2021 -0800
| 
|     New file def for production including daily files
very confusing.

* Prep to discuss w/ Susan how to get nowcast-green day-avg files output into production:
  * cherrypick commit on to PROD-nowcast-green-201905 branch on arbutus
  * pull everything and add new PROD-nowcast-green-201905-v2 tag
  * pull everything and move tag (may not be advisable ???)
(SalishSeaCast)

Removed option to clone via HTTPS from a couple of repo's docs:
MIDOSS/docs
MIDOSS/WWatch3-Cmd
(MIDOSS)

Group mtg; see whiteboard.
Updated cookiecutter-MOAD-pkg repo re: hg-git, etc.
(MOAD)

Phys Ocgy seminar by Parker McCready re: estuarine circulation in Salish Sea.

Dropped of FIT sample at LifeLabs.


Tue 8-Jun-2021
^^^^^^^^^^^^^^

docs scheduled linkcheck job failed overnight due to 504 errors from westgrid.ca; checked links and re-ran manually at ~10:00 with success.
upload_forcing nowcast+ to arbutus failed due to connection error; investigation:
* ssh attempt at ~10:30 failed
* action log in web dashboard says nowcast0 was stopped at 11:47 UTC == 04:47 Pacific
* started nowcast0 via dashboard
* took the opportunity to do apt update && apt upgrade and rebooted
* /nemoShare did not automatically remount
* sudo mount /dev/vdc /nemoShare  # quite slow
* /nemoShare/MEOPAR was not mounted at /export/MEOPAR for NFS
* sudo mount --bind /nemoShare/MEOPAR /export/MEOPAR
* ll /export/MEOPAR  # to confirm mount
* sudo systemctl start nfs-kernel-server.service
* sudo exportfs -f  # to reset NFS handles for compute nodes
* confirm compute nodes have /nemoShare/MEOPAR/ mounted:
* for n in {1..9}; do   echo nowcast${n};   ssh nowcast${n} "mountpoint /nemoShare/MEOPAR"; done
* for n in {0..6}; do   echo fvcom${n};   ssh fvcom${n} "mountpoint /nemoShare/MEOPAR"; done
* restarted automation at ~11:00:
* upload_forcing arbutus nowcast+

(SalishSeaCast)

Investigated CI failure in WWatch3-Cmd; outdated GHA workflow.
(MIDOSS)

Minecraft 1.17 released.
Made backup of Allenton world (aka SADAYule2020) on SADA server (archive-1623194729058.zip) and downloaded to kudu as Allenton1-64Backup8Jun21.zip.
Updated CubedHost SADA and SADA-dev servers to 1.17.
Created 1-17OceanTaiga world on SADA server, and a creative branch of it (1-17OceanTaigaCreative).


Wed 9-Jun-2021
^^^^^^^^^^^^^^

Pulled updates of SS-run-sets on arbutus and moved head to:
    commit 656d78d717629426fea4c1c4d6e9a9f23fd7ca64 (HEAD -> PROD-nowcast-green-201905-v2)
    Author: Susan Allen <sallen@eoas.ubc.ca>
    Date:   Thu Mar 11 11:10:01 2021 -0800
        New file def for production including daily files
on a new PROD-nowcast-green-201905-v2 branch; that should give us day-avg output files in nowcast-green production
nowcast-green stalled at 30% completion; investigation:
* ORT error message in stdout re: nowcast6 compute node
* ssh nowcast6 failed: no route to host
* dashboard shows nowcast6 stopped by no user at 10:27 Pacific
recovery:
* restarted nowcast6
* mounted /nemoShare/MEOPAR/ w/ sudo mount -t nfs -o proto=tcp,port=2049 192.168.238.14:/MEOPAR /nemoShare/MEOPAR
* killed watch_NEMO
* deleted tmp run & results dirs
* make_forcing_links arbutus nowcast-green
(SalishSeaCast)

Changed default branch name of WWatch3-Cmd repo from master to main.
Did lots of pkg maintenance on WWatch3-Cmd to bring it up to date w/ more used pkgs; added docs-linkcheck GHA workflow with scheduled runs on 11th of month.
(MIDOSS)

Squash-merged dependabot PRs re: pillow in SalishSeaCast/ SOG-Bloomcast-Ensemble, tools & SalishSeaNowcast, and MOAD/moad_tools.
Squash-merged dependabot PRs re: urllib3 in 43ravens/NEMO_Nowcast.
(MOAD)

Regenerated PyCharm Github Integration Plugin access token for kudu on GitHub and updated it in PyCharm.


Thu 10-Jun-2021
^^^^^^^^^^^^^^^

Tried to help Rhian@DFO via email w/ permission error they get when opening month-avg netCDF file from ERDDAP with R nc_open() function.
(Prediction Core)

Set up tmux session on salish to run analysis-doug/notebooks/hindcast-dayavgs/hindcast_dayavgs.py for 2021-01- through 2021-06-08.
(SalishSeaCast)

Tried to help Rachael via slack DM w/ logging.debug() messages not appearing when she runs random-oil-spills on salish.
(MIDOSS)


Fri 11-Jun-2021
^^^^^^^^^^^^^^^

Confirmed that tmux session on salish running analysis-doug/notebooks/hindcast-dayavgs/hindcast_dayavgs.py for 2021-01-02 through 2021-06-08 finished successfully.
(SalishSeaCast)

Reviewed https://linuxize.com/post/getting-started-with-tmux/; good base intro to tmux, but no serious details on command mode.

Prepared to run random-oil-spills w/ Rachael's recent changes on salish:
* Reviewed Rachael's changes in add-terminal branch of moad_tools re: random-oil-spills; set up moad-tools conda env on salish.
* Cloned into /data/dlatorne/MEOPAR/:
  * MIDOSS/MIDOSS-MOHID-config
* Data for random-oil-spills are in /data/MIDOSS/:
  * marine_transport_data/ repo clone contains oil_attribution.yaml file
  * geotiffs/ contains VTE GeoTIFFs and geotiff-watermask.npy calculated from them
  * shapefiles/ contains AIS vessel track shapefiles
* Rachael ran random-oil-spills on 10jun to produce /ocean/rmueller/MIDOSS/SalishSeaOilSpills_fixbarge_10000.csv; decided with Susan to use that to test on graham instead of me generating a different one
Prepared to test `mohid monte-carlo` on graham with spills from SalishSeaOilSpills_fixbarge_10000.csv:
* module load StdEnv/2016.4
* module load python/3.8.2
* updated repo clones:
  * Make-MIDOSS-Forcing/
  * MIDOSS-MOHID-CODE/  # up to date
  * MIDOSS-MOHID-config/  # up to date
  * MIDOSS-MOHID-grid/  # up to date
  * moad_tools/
  * MOHID-Cmd/
  * NEMO-Cmd/
  * SalishSeaCast-grid/  # up to date
* set up $SCRATCH space because it got wiped during upgrade in the spring:
  * mkdir -p $SCRATCH/MIDOSS/forcing/
  * mkdir -p $SCRATCH/MIDOSS/runs/monte-carlo/
  * chmod -R g+w $SCRATCH/MIDOSS  # because the sticky bit is being ignored
* installed pkgs via --user -e:
  * NEMO-Cmd  # already installed
  * MOHID-Cmd
  * Make-MIDOSS-Forcing
  * moad_tools  # forgot this one at first; required for hdf5-to-netcdf4
* set up run area and test run:
  * mkdir $PROJECT/$USER/MIDOSS/monte-carlo/
  * uploaded SalishSeaOilSpills_fixbarge_10000.csv from salish:
    * rsync -tlv SalishSeaOilSpills_fixbarge_10000.csv graham:project/dlatorne/MIDOSS/monte-carlo/
  * created glost job description YAML file & csv fragment file to run 1st 3 spills; submitted as /scratch/dlatorne/MIDOSS/runs/monte-carlo/first3_2021-06-11T174451/
    * run 1 failed in MOHID start-up due to line-ending : in comment in Lagrangian_bunker.dat template file
    * run 2 finished MOHID, but failed to convert hdf5 output to netcdf4 because moad_tools pkg wasn't installed
    * run 3 timed out during hdf5-to-netcdf4 processing
    * crap-ton of debug output in stdout
* discovered that moad_tools must have cliff<8.0 pin due to pins in fiona and rasterio
* repeated 1st 3 spills run with:
  * corrected Lagrangian_bunker.dat template file
  * per run walltime increased to 3hr
  * hdf5-to-netcdf4 installed
  * MOHID debug output removed by Susan
* submitted 30 spill run for northern SoG spill chosen by Susan and with glost_job.sh hacked to set ntask-per-node to 32 so we get on the large-by-node queue
(MIDOSS)
  
Slack w/ Raisha:
* introduced her to tmux
* TODO:
  * headless shiny ? - done 14-Jun
  * R kernel for Jupyter - done 16-Jun
  * design AtlantisCmd
  * think about runs diary feature
(Atlantis)
  

Sat 12-Jun-2021
^^^^^^^^^^^^^^^

skookum connections failed from 09:25 to 10:04; nowcast-blue appears stuck in log; investigation & recovery:
* on skookum:
* restarted log aggregator to no avail
* restarted message broker to no avail
* on arbutus:
* nowcast-blue run finished, but watcher is stuck
* pkill -f watch_NEMO
* restart automation on skookum:
* download_results arbutus nowcast
* make_forcing_links arbutus ssh
* launch_remote_worker arbutus make_fvcom_boundary "arbutus x2 nowcast"
(SalishSeaCast)

Confirmed that monte-carlo sets ntasks-per-node to 32 so we get on the by-node queue when we are running >30 spills.
Ran 60 more northern SoG spills that Susan chose as north_strait_2nd60.
Susan plotted first aggregated Monte-Carlo results :-)
Changed MOHID run script to:
* rename resOilOuput.sro file to MassBalance_${RUN_ID}.sro; more descriptive and eliminates ambiguity in Monte-Carlo results collections
* delete big, unused Turbulence*.hdf5, res*.elf5, and res*.ptf output file s
Helped Ben sort out jupyter venv issues on graham.
Ran 150 more northern SoG spills that Susan chose as north_strait_3rd150.
(MIDOSS)


Sun 13-Jun-2021
^^^^^^^^^^^^^^^

Ran 122 more northern SoG spills that Susan chose as north_strait_4th122 to complete 1/2 of the north strait spills in Rachael's 10k file.
(MIDOSS)


Week 24
-------

Mon 14-Jun-2021
^^^^^^^^^^^^^^^

Week 66 of UBC work-from-home due to COVID-19

Deleted Turbulence*.hdf5, res*.elf5 & res*.ptf from monte-carlo results/ dirs of runs that happened before change to MOHID-Cmd landed on Saturday; space for 362 runs before cleanup: 1.2T; space after: 25G
Ran 362 more northern SoG spills that Susan chose as north_strait_5th362 to complete 2nd 1/2 of the north strait spills in Rachael's 10k file.
(MIDOSS)

upload_forcing orcinus nowcast+ failed w/ "private key encrypted" error; that's usually a login node network stack problem; re-tried manually at ~10:06; success
(SalishSeaCast)

Experimented to try to get shiny ReactiveAtlantis app to run headless on tyee:
  cd /ocean/dlatorne/Atlantis/
  git clone git@github.com:Atlantis-Ecosystem-Model/ReactiveAtlantis.git
  cd /ocean/dlatorne/Atlantis/atlantis-trunk/example/outputFolder/
  conda activate atlantis-dev
  R
  > options(browser = "false")
  > library("devtools")
  > install_local("/ocean/dlatorne/Atlantis/ReactiveAtlantis")
  # lots of compulation; hopefully only required once
  > library("ReactiveAtlantis")
  # in example/outputFolder/
  > biom <- "outputSETASBiomIndx.txt"
  > diet.file <- "outputSETASDietCheck.txt"
  > bio.age <- "outputSETASAgeBiomIndx.txt"
  > grp.csv <- "../SETasGroupsDem.csv"
  > predation(biom, grp.csv, diet.file, bio.age)
  Loading required package: shiny
  
  Listening on http://127.0.0.1:6155
  Winning!!! :-)
  ssh tunnel on kudu between tyee port 6155 and kudu port 4343:
    ssh -N -L 4343:127.0.0.1:6155 tyee
Refining:
  * control port shiny uses to prevent random selection
  * handle browser launch in shiny context instead of R-wide
  * combine option settings in 1 call
  * use pathed files
    > options(shiny.port=6155, shiny.launch.browser = "false")
    > biom <- "atlantis-trunk/example/outputFolder/outputSETASBiomIndx.txt"
    > diet.file <- "atlantis-trunk/example/outputFolder/outputSETASDietCheck.txt"
    > bio.age <- "atlantis-trunk/example/outputFolder/outputSETASAgeBiomIndx.txt"
    > grp.csv <- "atlantis-trunk/example/SETasGroupsDem.csv"
    > predation(biom, grp.csv, diet.file, bio.age)
Wrote preliminary docs in #atlantis channel at https://salishseacast.slack.com/archives/C01TE50SZ8E/p1623702157000700
Tried to help Raisha debug compare() app.
(Atlantis)

Group mtg; see whiteboard.
(MOAD)


Tue 15-Jun-2021
^^^^^^^^^^^^^^^

Work at ESB while Rita is at home.

forecast2 failed; investigation:
* fvcom2 node stopped at 2:34 UTC, no user or explanation
* nowcast8 node stopped at 2:34 UTC, no user or explanation
Restarted fvcom & nowcast8 from arbutus dashboard; re-mounted /nemoShare/MEOPAR on them.
VHFR nowcast-r12 failed due to no restart file; 14jun21 run stopped at 19:34 (i.e. 02:34 UTC) when fvcom2 node stopped; recovery started at ~16:30:
* launch_remote_worker arbutus make_fvcom_boundary "arbutus r12 nowcast 2021-06-14"
(SalishSeaCast)

Coffee (in person!) with Birgit outside ESB.

Worked on updating cookiecutter-MOAD-pypkg:
* changed git default branch name from master to main
* updated dev env to Python 3.9
* add intersphinx mapping for MOAD docs
* update re: migration from Mercurial on Bitbucket to Git on GitHub
(MOAD)


Wed 16-Jun-2021
^^^^^^^^^^^^^^^

collect_weather 12 still running at 09:30; no 12Z files have appeared yet in sarracenia log, but 06Z forecast appears to have been re-broadcast between 04:20 and 06:14; 12Z files started to arrive at ~10:00; finished at 10:34.
Backfilling VHFR nowcast-r12:
* wait for run to fail
* launch_remote_worker arbutus make_fvcom_boundary "arbutus r12 nowcast 2021-06-15"
  * started at ~17:00
(SalishSeaCast)

Started exploring R kernel for Jupyter.
Updated /media/doug/warehouse/Atlantis/environment-dev.yaml:
* re-organized dependencies w/ comments about what they are for
* added IRKernel and its deps
* added jupyterlab
and it just works! :-)
(Atlantis)

Stakeholder workshop 1st day 12-Jul (tentative?)
* data collection
* test hypotheses that arose from analysis of data from 1st workshop
* 2nd day is about model products
(MIDOSS)


Thu 17-Jun-2021
^^^^^^^^^^^^^^^

collect_weather 06 didn't complete so no forecast2 runs; investigation:
* no error messages in sarracenia log
* 531 of 576 files downloaded; files missing from hours 017, 018, 020, 022, 023
* spot check of files in 017 and 018 on datamart web site show they are there
* recovery:
    pkill -f collect_weather
    rm -rf /results/forcing/atmospheric/GEM2.5/GRIB/20210617/06/
    download_weather 06 2.5km
    collect_weather 18 2.5km
    wait for forecast2 runs to finish
    download_weather 12 2.5km
collect_weather 18 appears to have stalled; investigation:
* no error messages in sarracenia log
* 558 of 576 files downloaded; files missing from hours 019, 020, 021, 024
* spot check of files in 019 and 024 on datamart web site show they are there
* recovery:
    pkill -f collect_weather
    rm -rf /results/forcing/atmospheric/GEM2.5/GRIB/20210617/18/
    download_weather 18 2.5km
    download_weather 00 1km
    download_weather 12 1km
    collect_weather 00 2.5km
Didn't get a VHFR nowcast-r12 no restart file run failure, and forgot to start 16jun backfill run
(SalishSeaCast)

Weekly project mtg.
(Atlantis)


Fri 18-Jun-2021
^^^^^^^^^^^^^^^

collect_weather 06 didn't complete so no forecast2 runs; investigation:
* no error messages in sarracenia log
* 554 of 576 files downloaded; files missing from hours 014, 016, 022, 023, 024
* spot check of files in 014 on datamart web site show they are there with same time stamp as other files
* recovery:
    pkill -f collect_weather
    rm -rf /results/forcing/atmospheric/GEM2.5/GRIB/20210618/06/
    download_weather 06 2.5km
    wait for 12Z forecast files to finsih in sarracenia log
    clean up /SalishSeaCast/datamart
      find /SalishSeaCast/datamart/hrdps-west/ -type f -delete
    restart sarracenia processes
      supervisorctl -c $NOWCAST_CONFIG/supervisord.ini restart sr_subscribe-hrdps-west
      supervisorctl -c $NOWCAST_CONFIG/supervisord.ini restart sr_subscribe-hrdps-west-1km
      supervisorctl -c $NOWCAST_CONFIG/supervisord.ini restart sr_subscribe-hydrometric
    collect_weather 18 2.5km
    wait for forecast2 runs to finish
    download_weather 12 2.5km
VHFR nowcast-x2 not reporting progress to log; confirmed that it is running; restarted log aggregator; resolved.
nowcast-agrif run failed during prep; investigation:
* 17jun21 run stopped for no evident reason
* recovery:
    upload_forcing orcinus nowcast+ --run-date 2021-06-17
    upload_forcing orcinus turbidity --run-date 2021-06-17
    wait for run to finish
    upload_forcing orcinus nowcast+ --run-date 2021-06-18
    upload_forcing orcinus turbidity --run-date 2021-06-18
collect_weather 18 stalled; investigation:
* no error messages in sarracenia log
* 539 of 576 files downloaded; files missing from hours 015, 016, 017, 019, 020, 022, 023, 024
* recovery:
    pkill -f collect_weather
    rm -rf /results/forcing/atmospheric/GEM2.5/GRIB/2021061/18/
    download_weather 18 2.5km
    download_weather 00 1km
    download_weather 12 1km
    collect_weather 00 2.5km
Backfilling VHFR nowcast-r12:
* wait for run to fail
* launch_remote_worker arbutus make_fvcom_boundary "arbutus r12 nowcast 2021-06-16"
(SalishSeaCast)

Started thinking about design of AtlantisCmd, a Atlantis model run command processor based on NEMO-Cmd:
* example model run command from Raisha:
    /ocean/rlovindeer/Atlantis/atlantis-trunk/atlantis/atlantismain/atlantisMerged -i SS_init.nc 0 -o outputSalishSea.nc -r SS_run.prm -f SS_forcing.prm -p SS_physics.prm -b 02SS_biology.prm -s SS_grps.csv -d /ocean/rlovindeer/MOAD/analysis-raisha/SSmodel_outputs/output-25yr
* goal is a command like:
    atlantis run run_description.yaml output_directory/
    e.g. atlantis run 25yr.yaml /ocean/rlovindeer/MOAD/analysis-raisha/SSmodel_outputs/output-25yr/
* run description YAML file structure:
    run id: 25yr

    paths:
      Atlantis code: /ocean/rlovindeer/Atlantis/atlantis-trunk/
      runs directory: /ocean/rlovindeer/Atlantis/runs/

    forcing:
      # keys are the file/directory names that are used for the
      # symlinks created to the values of the `link to:` items
      SS_init.nc:
        link to: /ocean/rlovindeer/Atlantis/salish-sea-atlantis-model/SS_init.nc
      
      # important design questions here!!!

      # This approach links an entire directory of forcing files into tmp run dir
      # and leaves the specification of which files from there are used to lines in forcing.prm
      inputs:
        link to: /ocean/rlovindeer/Atlantis/salish-sea-atlantis-model/inputs

      # This approach identifies the forcing files explicitly here
      # and potentially lets forcing.prm be generic;
      # i.e. no inputs/... just file names that match keys here.
      # This also keeps tmp run dir flat.
      SS_hydro.nc:
        link to: /ocean/rlovindeer/Atlantis/salish-sea-atlantis-model/inputs/SS_hydro.nc
      SS_temp.nc:
        link to: /ocean/rlovindeer/Atlantis/salish-sea-atlantis-model/inputs/SS_temp.nc
      SS_salt.nc:
        link to: /ocean/rlovindeer/Atlantis/salish-sea-atlantis-model/inputs/SS_salt.nc

    parameters:
      groups: /ocean/rlovindeer/Atlantis/salish-sea-atlantis-model/SS_grps.csv
      run: /ocean/rlovindeer/Atlantis/salish-sea-atlantis-model/SS_run.prm
      forcing: /ocean/rlovindeer/Atlantis/salish-sea-atlantis-model/SS_forcing.prm   
      physics: /ocean/rlovindeer/Atlantis/salish-sea-atlantis-model/SS_physics.prm   
      biology: /ocean/rlovindeer/Atlantis/salish-sea-atlantis-model/SS_biology.prm   

      # Another design question!!

      # Alternative is to make these lists of files that are concatenated 
      # to create the filename that is the key.
      # This is a little cumbersome because we still need to know what kind of 
      # parameter file each is
      groups:
        # example of single file list
        SS_grps.csv:
          - /ocean/rlovindeer/Atlantis/salish-sea-atlantis-model/SS_grps.csv


    output filename base: outputSalishSea

    vcs revisions:
      svn:
        # can probably make this automatic because we have it already in `paths: Atlantis code:`
        - /ocean/rlovindeer/Atlantis/atlantis-trunk/
      git:
        - /ocean/rlovindeer/Atlantis/salish-sea-atlantis-model/
(Atlantis)


Sat 19-Jun-2021
^^^^^^^^^^^^^^^

Drove to White Rock to visit J&M; took them to Bayview Park.

Backfilling VHFR nowcast-r12:
* wait for run to fail
* launch_remote_worker arbutus make_fvcom_boundary "arbutus r12 nowcast 2021-06-17"
* wait for run to finish
* launch_remote_worker arbutus make_fvcom_boundary "arbutus r12 nowcast 2021-06-18"
collect_weather 18 stalled; investigation:
* no error messages in sarracenia log
* 543 of 576 files downloaded; files missing from hours 014, 015, 017, 018, 020, 021, 022
* recovery:
    pkill -f collect_weather
    rm -rf /results/forcing/atmospheric/GEM2.5/GRIB/20210619/18/
    download_weather 18 2.5km
    download_weather 00 1km - failed due to 404s
    download_weather 12 1km
    collect_weather 00 2.5km
(SalishSeaCast)


Sun 20-Jun-2021
^^^^^^^^^^^^^^^

collect_weather 06 stalled; investigation:
* no error messages in sarracenia log
* 565 of 576 files downloaded; files missing from hours 013, 019
* recovery:
    pkill -f collect_weather
    rm -rf /results/forcing/atmospheric/GEM2.5/GRIB/20210620/06
    download_weather 06 2.5km
    collect_weather 18 2.5km
    wait for forecast2 runs to finish
    download_weather 12 2.5km
collect_weather 18 stalled; investigation:
* no error messages in sarracenia log
* 534 of 576 files downloaded; files missing from hours 015-018, 021, 022, 024
* recovery:
    pkill -f collect_weather
    rm -rf /results/forcing/atmospheric/GEM2.5/GRIB/20210620/18/
    download_weather 18 2.5km
    download_weather 00 1km - failed due to 404s
    download_weather 12 1km
    collect_weather 00 2.5km
Backfilling VHFR nowcast-r12:
* wait for run to finish
* launch_remote_worker arbutus make_fvcom_boundary "arbutus r12 nowcast 2021-06-19"
(SalishSeaCast)


Week 25
-------

Mon 21-Jun-2021
^^^^^^^^^^^^^^^

Week 67 of UBC work-from-home due to COVID-19

collect_weather 00, 06, 12 successful
Backfilling VHFR nowcast-r12:
* wait for run to finish
* launch_remote_worker arbutus make_fvcom_boundary "arbutus r12 nowcast 2021-06-20"
* wait for run to finish
* launch_remote_worker arbutus make_fvcom_boundary "arbutus r12 nowcast 2021-06-21"
collect_weather 18 stalled; investigation:
* no error messages in sarracenia log
* 566 of 576 files downloaded; files missing from hours 016, 019 022, 023
* recovery:
    pkill -f collect_weather
    rm -rf /results/forcing/atmospheric/GEM2.5/GRIB/20210621/18/
    download_weather 18 2.5km
    download_weather 00 1km - failed due to 404s
    download_weather 12 1km
    collect_weather 00 2.5km
(SalishSeaCast)

Installed Litematica & MiniHUD client mods via :
* Stored files in ~/Minecraft/mods/1.17/
* Downloaded -installer-0.7.4.jar from mc.net, made it executable, and ran it to create new profile
* Launch minecraft in 1.17 profile; crash complaining about 1.16 mods
* Moved 1.16 mods from ~/.minecraft/mods/ to ~/Minecraft/mods/1.16/
* Launch minecraft in 1,17 profile; success; shutdown
* Downloaded from curseforge.com:
  * malilib--1.17.0-0.10.0-dev.22+beta.1.jar
  * minihud--1.17.0-0.19.0-dev.20210609.185508.jar
  * litematica--1.17.0-0.0.0-dev.20210616.033538.jar
* Copied 3 mods into ~/.minecraft/mods/
* Launch minecraft in 1.17 profile
(Minecraft)

Worked on running hdf5-to-netcdf4 on files in $SCRATCH/MIDOSS/runs/monte-carlo/north_strait_5th362_2021-06-14T150753/results/ that didn't get processesed due to filling node-local scratch storage:
* all spills <=219 were processesed
* hit and miss for spills 220 through 306
* no spills >=306 were processesed
* processing spill 220 on login node took 9m37s
* need to load python/3.8.2 and nco/4.9.5
* processing spill 221 in interactive session on gra800 using node-local scratch ($SLURM_TMPDIR) took 10m35s
  salloc --time=0:30:0 --cpus-per-task=1 --mem-per-cpu=1024m --account=def-allen
  export RESULTS_FILE=Lagrangian_diesel-221_north_strait_5th362-221
  cp -v /scratch/dlatorne/MIDOSS/runs/monte-carlo/north_strait_5th362_2021-06-14T150753/results/north_strait_5th362-221/${RESULTS_FILE}.hdf5 $SLURM_TMPDIR/
  time hdf5-to-netcdf4 -v debug $SLURM_TMPDIR/${RESULTS_FILE}.hdf5 $SLURM_TMPDIR/${RESULTS_FILE}.nc
Developed a script to process results dirs one at a time; ran for several in sacct sessions.
(MIDOSS)


Tue 22-Jun-2021
^^^^^^^^^^^^^^^

collect_weather 06 stalled; investigation:
* no error messages in sarracenia log
* 525 of 576 files downloaded; files missing from hours 013-019, 021, 022
* recovery:
    pkill -f collect_weather
    rm -rf /results/forcing/atmospheric/GEM2.5/GRIB/20210622/06
    download_weather 06 2.5km
    collect_weather 18 2.5km
    wait for forecast2 runs to finish
    download_weather 12 2.5km
Emailed Sandrine; she's on leave, so resent to DPS-Client address.
Tempoary failure of /ocean, but resolved itself.
Discovered that log aggregator stopped around 11:16; maybe connected with other transient network issues this morning; restarted at ~16:40.
nowcast-agrif failed, perhaps also due to network issue this morning; re-launched at ~17:10; failed again.
(SalishSeaCast)

Continued running sacct sessions to run hdf5-to-netcdf4 on files in $SCRATCH/MIDOSS/runs/monte-carlo/north_strait_5th362_2021-06-14T150753/results/ that didn't get processesed due to filling node-local scratch storage.
(MIDOSS)

Got serious about trying to choose a new dishwasher.


Wed 23-Jun-2021
^^^^^^^^^^^^^^^

Stored script for backfilling MOHID HDF5 to netCDF4 conversions at https://gist.github.com/douglatornell/f5821b42c0153494592133010c6f8a7c; continued running sacct sessions to run hdf5-to-netcdf4 on files in $SCRATCH/MIDOSS/runs/monte-carlo/north_strait_5th362_2021-06-14T150753/results/ that didn't get processesed due to filling node-local scratch storage.
Stakeholder workshop prep mtg;
* <32 HDF5 to netCDF4 conversions to go; finish today?
(MIDOSS)

collect_weather 00 stalled; investigation:
* no error messages in sarracenia log, but it stopped at 11:15 on 22jun - network quake?
* 543 of 576 files downloaded; files missing from hours 013, 015, 017, 020, 021, 024
* recovery started at ~10:00:
    pkill -f collect_weather
    rm -rf /results/forcing/atmospheric/GEM2.5/GRIB/20210623/00
    download_weather 00 2.5km
    collect_weather 18 2.5km
    download_weather 06 2.5km
    wait for forecast2 runs to finish
    download_weather 12 2.5km
Retried 22jun nowcast-agrif with a step back to re-upload forcing
  upload_forcing orcinus nowcast+ --run-date 2021-06-22
  upload_forcing orcinus turbidity --run-date 2021-06-22
  run failed after 7 min
collect_weather 18 & 1km HRDPS downloads worked.
Email to Jenn re: stalled Fraser River Buoy page; she restarted DMS.
collect_weather 00 stalled
* no error messages in sarracenia log
* 500 of 576 files downloaded; files missing from hours 013-022; no files in 014 and 019
* recovery:
    download_weather 06 2.5km
    collect_weather 18 2.5km
(SalishSeaCast)

Email to Kate Schuler to help her w/ ERDDAP access to vertical diffusivity to analyze in matlab.
(Prediction Core)


Thu 24-Jun-2021
^^^^^^^^^^^^^^^

Booked appt for 2nd dose of COVID-19 vaccine.

collect_weather 06 stalled; investigation:
* no error messages in sarracenia log
* 543 of 576 files downloaded; files missing from hours 013, 017-019, 021, 022, 024
* recovery:
    pkill -f collect_weather
    rm -rf /results/forcing/atmospheric/GEM2.5/GRIB/20210624/06/
    download_weather 06 2.5km
    collect_weather 18 2.5km
    wait for forecast2 runs to finish
    download_weather 12 2.5km
UBC-DFO modeling mtg; Laura's FVCOM model in Bute & Toba Inlets; Michael shared arch file that works for XIOS-2 r1625 on graham.
Changed HRDPS west sr_subscribe log level to debug and restarted it.
SalishSeaCast is running sarracenia-2.20.08post1; latest release is 2.12.04, but it is bug fixes that don't look like they have anything to do with the issues we are seeing.
(SalishSeaCast)

Created AtlantisCmd repo on GitHub and started design notes & discussion in issue #1.
Weekly mtg w/ CSIRO:
* SS_xy.bgm file name is provided to Atlantis as a global attribute in SS_init.nc
(Atlantis)


Fri 25-Jun-2021
^^^^^^^^^^^^^^^

Beginning of dome heat wave, expected to last 7 days.

collect_weather 18, 00, and 06 worked in automation
collect_weather 12 stalled; investigation:
* sarracenia log is less useful due to ~20 lines of debug message for every file in forecast, making finding info about the 576 we care about hard
* 539 of 576 files downloaded; files missing from hours 015-017, 019-022
* recovery:
  pkill -f collect_weather
  rm -rf /results/forcing/atmospheric/GEM2.5/GRIB/20210625/12/
  download_weather 12 2.5km
  collect_weather 18 2.5km
Reviewed notes about missing files and confirmed that they are always in the 013-024 hours range.
Set log level for sr_subscribe for HRDPS west back to info.
Set log level for sr_subscribe for HRDPS west 1km to debug; no file notifications.
collect_weather 18 stalled; investigation:
* no error messages in sarracenia log
* 539 of 576 files downloaded; files missing from hours 015-017, 019-022, 024
* collect_weather 18 wasn't running; maybe because the skookum session I started it in died?
* recovery:
    rm -rf /results/forcing/atmospheric/GEM2.5/GRIB/20210625/18/
    download_weather 18 2.5km
    download_weather 00 1km --yesterday
    download_weather 12 1km
    collect_weather 00 2.5km
collect_weather 00 stalled
* no error messages in sarracenia log
* 548 of 576 files downloaded; files missing from hours 013, 018-022, 024
* recovery:
    pkill -f collect_weather
    rm -rf /results/forcing/atmospheric/GEM2.5/GRIB/20210626/00/
    download_weather 00 2.5km
    collect_weather 06 2.5km
(SalishSeaCast)

Coffee w/ Tereza.

Continued work on design of AtlantisCmd; started creating handcrafted example/template tmp run dir.
(Atlantis)


Sat 26-Jun-2021
^^^^^^^^^^^^^^^

Heat wave continued, hotter.

collect_weather 06, 12, 18 & 00 worked in automation
(SalishSeaCast)

Fixed permissions on post-processing converted netCDF4 files on graham.
(MIDOSS)

Drove to White Rock to visit M&J.


Sun 27-Jun-2021
^^^^^^^^^^^^^^^

Heat wave continued, hotter.

collect_weather 06 worked in automation
collect_weather 12 stalled; investigation:
* no messages in sarracenia log
* 574 of 576 files downloaded; files missing from hours 018, 021
* recovery:
    pkill -f collect_weather
    rm -rf /results/forcing/atmospheric/GEM2.5/GRIB/20210627/12
    download_weather 12 2.5km
    collect_weather 18 2.5km
collect_weather 00 stalled; investigation revealed a steady stream of "Tempoary failure in name resolution" errors; nothing to be done to recover.

(SalishSeaCast)

Robinson reunion on Zoom

Got 2nd dose of COVID-19 vaccine


Week 26
-------

Mon 28-Jun-2021
^^^^^^^^^^^^^^^

Week 68 of UBC work-from-home due to COVID-19

Heat wave continued, hotter; moved downstairs to work.

Widespread connection issues on ocean machines; name resolution errors continued in sarracenia log for 06Z forecast; mitigation:
  pkill -f collect_weather
  rm -rf /results/forcing/atmospheric/GEM2.5/GRIB/20210628/00
  # on kudu
    sshfs -o nonempty skookum:/results /results
    download_weather 00 --debug
    download_weather 06 --debug
    download_weather 12 --debug
    download_live_ocean
At ~11:30 Charles confirmed DNS failure in EOSM due to overnight AC failures; compounded by ocean2 crashes yesterday and again this morning.
* recovery:
    mv /results/forcing/atmospheric/GEM2.5/GRIB/20210628/06 /results/forcing/atmospheric/GEM2.5/GRIB/20210628/06.aside
    collect_weather 18 2.5km
    download_weather 06 2.5km
    wait for forecast2 runs to finish
    mv /results/forcing/atmospheric/GEM2.5/GRIB/20210628/12 /results/forcing/atmospheric/GEM2.5/GRIB/20210628/12.aside
    download_weather 12 2.5km
Charles restored /ocean mounts on skookum & salish at ~14:30.
ocean was apparently the target of brute force attack over the weekend.
collect_weather 18 worked in automation.
(SalishSeaCast)

Group mtg; see whiteboard.
(MOAD)

Phys Ocgy seminar by Susan; her CAIMS talk on Gonzalo & Karina's canyon work.


Tue 29-Jun-2021
^^^^^^^^^^^^^^^

Heat wave continued, a little cooler.

Work at ESB while Rita is at home.

collect_weather 00, 06, 12, 18 worked in automation
upload_forcing nowcast+ to arbutus failed due to connection error; investigation:
* ssh attempt at ~07:30 failed
* action log in web dashboard says nowcast0 was stopped at 05:12 UTC == 22:12 Pacific
* started nowcast0 via dashboard
* took the opportunity to do apt update && apt upgrade and rebooted
* /nemoShare did not automatically remount
* sudo mount /dev/vdc /nemoShare  # quite slow
* /nemoShare/MEOPAR was not mounted at /export/MEOPAR for NFS
* sudo mount --bind /nemoShare/MEOPAR /export/MEOPAR
* ll /export/MEOPAR  # to confirm mount
* sudo systemctl start nfs-kernel-server.service
* sudo exportfs -f  # to reset NFS handles for compute nodes
* confirm compute nodes have /nemoShare/MEOPAR/ mounted:
* for n in {1..9}; do   echo nowcast${n};   ssh nowcast${n} "mountpoint /nemoShare/MEOPAR"; done
* for n in {0..6}; do   echo fvcom${n};   ssh fvcom${n} "mountpoint /nemoShare/MEOPAR"; done
* restarted automation at ~07:45:
    upload_forcing arbutus forecast2
nowcast-green run stalled at 25.3% complete; investigation:
* nowcast6 node stopped at 17:52 UTC == 10:52 Pacific
* recovery:
    restarted intance from dashboard
    sudo mount -t nfs -o proto=tcp,port=2049 192.168.238.14:/MEOPAR /nemoShare/MEOPAR # on nowcast6
    killed xios_server
    killed watch_NEMO
    deleted tmp run & results dirs
    make_forcing_links arbutus nowcast-green
Noticed that there were no progress messages from nowcast-x2, so restarted log aggregator.
Discovered that nowcast-r12 28jun runs stopped, and 27jun run did not download to skookum; recovery:
    download_fvcom_results arbutus r12 nowcast 2021-06-27
    wait for 29jun run to fail
    launch_remote_worker arbutus make_fvcom_boundary "arbutus r12 nowcast 2021-06-28"
    wait for run to finish
    launch_remote_worker arbutus make_fvcom_boundary "arbutus r12 nowcast 2021-06-29"
Reviewed Michael's XIOS arch files on graham; no substantial differences from ours.
(SalishSeaCast)

Updated alarm monitoring contacts list; requested assessment for system upgrade.

Called Nanaimo Toyota to request assessment on Prius summer tires; they can ship to Vancouver; assessment: original tires are >10 yrs old (>7 is illegal), 40-50% tread wear, but bad edge wear; not recommended; authorized dealer to send them to recycling.

rsync-ed $SCRATCH/MIDOSS/runs/monte-carlo/ to $PROJECT/MIDOSS/monte-carlo-results/ to preserve them from $SCRATCH purge policy:
  rsync -rltv $SCRATCH/MIDOSS/runs/monte-carlo/ $PROJECT/MIDOSS/monte-carlo-results/
That creates ~19.7k files that pushes on our 100k file count quota on $PROJECT.
Noticed that north_strait_4th122_2021-06-13T143859/results/north_strait_4th122-47/ contains a core dump; divide by zero.
(MIDOSS)


Wed 30-Jun-2021
^^^^^^^^^^^^^^^

Heat wave continued, cool enough overnight to get downstairs temperature down to 22°C.

collect_weather 06 stalled; investigation:
* no error messages in sarracenia log
* 538 of 576 files downloaded; files missing from hours 014-017, 019-022, 024
* recovery:
    pkill -f collect_weather
    rm -rf /results/forcing/atmospheric/GEM2.5/GRIB/20210630/06
    download_weather 06 2.5km
    collect_weather 18 2.5km
    wait for forecast2 runs to finish
    download_weather 12 2.5km
collect_weather 18 stalled; investigation:
* no error messages in sarracenia log; 576 file messages though
* 199 of 576 files downloaded
* no collect_weather worker running; perhaps collect_weather 18 got killed while working due to my skookum session hanging up???
* recovery:
    rm -rf /results/forcing/atmospheric/GEM2.5/GRIB/20210630/18/
    download_weather 18 2.5km
    download_weather 00 1km --yesterday  # ran after 17:00 == 00:00 UTC
    download_weather 12 1km
    collect_weather 00 2.5km
collect_weather 00 worked in automation
(SalishSeaCast)

Continued work on design of AtlantisCmd; finished creating handcrafted example/template tmp run dir; ran Atlantis in rsync clone of it; design questions:
* should Atlantis console output go to stdout only, to screen and stdout, or option to screen
* vcs recording for svn may be hard; log info is on server
(Atlantis)

Workshop prep mtg.
Worked w/ Ben on settings to serve static tiles.
(MIDOSS)


July
----

Thu 1-Jul-2021
^^^^^^^^^^^^^^^

**Statutory Holiday** - Canada Day

collect_weather 06, 12, 18, 00 worked in automation
(SalishSeaCast)

Drove to Mt. Thom Air BnB for long weekend.

Hiked from Thom Creek trailhead, out & back including walk from rental.


Fri 2-Jul-2021
^^^^^^^^^^^^^^^

collect_weather 06, 12, 18, 00 worked in automation
(SalishSeaCast)

Hiked Elk-Thurston trail to ~1km beyond Elk; many steep sections; very sore tired quads on return.


Sat 3-Jul-2021
^^^^^^^^^^^^^^^

collect_weather 06, 12, 18, 00 worked in automation
(SalishSeaCast)

Hiked TCT downstream from Chilliwack Lake to near split of Radium Lake trail.


Sun 4-Jul-2021
^^^^^^^^^^^^^^^

collect_weather 06, 12, 18, 00 worked in automation
(SalishSeaCast)


Week 27
-------

Mon 5-Jul-2021
^^^^^^^^^^^^^^

Week 69 of UBC work-from-home due to COVID-19

docs linkcheck workflow failed after a push by Becca last week and overnight in its scheduled run; investigation:
* 403 Client Error: Forbidden for url: https://www.baeldung.com/cs/ssh-intro
* confirmed that page is alive
* workflow failed again on manual re-try
* decided to do nothing for a month to see if the issue resolves; not sure if it is baeldung blocking connections from GitHub, or what
Group mtg; see whiteboard.
Resumed work on conda section of docs:
* traced rampant ``Error in "image" directive:
unknown option: "target"`` errors from rST snooty linter to https://github.com/vscode-restructuredtext/vscode-restructuredtext/issues/290
(MOAD)

New dishwasher delivered and installed.

Reviewed UBC/CSIRO contract re: copyright and licence of project IP; copyright is clearly project contributors, UBC & CSIRO; license is ambiguous other than UBC & CSIRO grant free reciprocal license; discussed w/ Susan and decided on our usual CC-By for doc and Apache 2.0 for code & docs; 
(Atlantis)


Tue 6-Jul-2021
^^^^^^^^^^^^^^

Submitted PWGSC ProServices quarterly usage report for 43ravens supply arrangement.

Coffee w/ Ben.

Finished updating cookiecutter-MOAD-pypkg:
* add SS-Atlantis gitHub org and copyright holders
(MOAD)

Continued work on design of AtlantisCmd; finished creating handcrafted example/template tmp run dir; ran Atlantis in rsync clone of it; design questions:
* should Atlantis console output go to stdout only, to screen and stdout, or option to screen; decided on stdout & stderr
* should stdout & stderr be separate or combined/interleaved?
* vcs recording for svn may be hard; log info is on server
Explored getting info from svn w/o auth to server:
* svn info provides:
* repo URL
* last changed rev
* last changed authored
* last changed date
* missing files and message compared to git/hg
* not sure what svn info output for committed but unpushed changes
* svn diff provides file by file diffs for uncommitted changes
(Atlantis)


Wed 7-Jul-2021
^^^^^^^^^^^^^^

Continued discussion of design of AtlantisCmd w/ Raisha in issue #1.
(Atlantis)

Helped Tereza sort out running from PROD-HINDCAST_201905-v? re: need to create branches for tag checkouts so that VCS recording works.
Retried 22jun nowcast-agrif from re-upload forcing:
    upload_forcing orcinus nowcast+ --run-date 2021-06-22
    upload_forcing orcinus turbidity --run-date 2021-06-22
    * stepping, but ~25% of usual speed
Finally sorted out logic of adding partition=QDR PBS directive to SalishSeaCmd for orcinus runs (dates back to email w/ Mark in Jan-21 :-(
Had to mess araound with git config in an elderly version on orcinus to get merge of main to work.
Started backfilling nowacst-agrif:
    upload_forcing orcinus nowcast+ --run-date 2021-06-23
    upload_forcing orcinus turbidity --run-date 2021-06-23
    also took 4h20m to run
(SalishSeaCast)

Coffee w/ Raisha.

Workshop planning mtg:
* Note-taker w/ Stephanie for #7 on day 2: discussion of getting fields and Ben's viz app
(MIDOSS)


Thu 8-Jul-2021
^^^^^^^^^^^^^^

Investigated SalishSeaCast/docs scheduled linkcheck failure:
* connection failed to http://pages.physics.cornell.edu/~myers/teaching/ComputationalMethods/LectureNotes/Intro_to_Python.pdf; maybe temporary?
Emailed Sandrine re: resolution of HRDPS west AMQP reliability issue on 1jul.
Continued backfilling nowacst-agrif:
    wait for automation to fail
    upload_forcing orcinus nowcast+ --run-date 2021-06-24
    upload_forcing orcinus turbidity --run-date 2021-06-24
    wait for run to finish
    upload_forcing orcinus nowcast+ --run-date 2021-06-25
    upload_forcing orcinus turbidity --run-date 2021-06-25
    wait for run to finish
    upload_forcing orcinus nowcast+ --run-date 2021-06-26
    upload_forcing orcinus turbidity --run-date 2021-06-26
Noted that partition=QDR PBS directive is still not appearing in run scripts on orcinus; figured out that value of SYSTEM in SalishSeaCmd/run.py is not getting set to orcinus when it is run via sftp client in run_NEMO_agrif worker because WGSYSTEM envvar is not set; instead SYSTEM is set to seawolf? via socket.gethostname()
(SalishSeaCast)

Archived 1-17OceanTaiga on SADA CubedHost server as archive-1625773673456.zip and updated server to 1.17.1.
Updated Litematica & MiniHUD client mods via :
* Launch minecraft 1.17.1
* Run -installer-0.7.4.jar (same as for 1.17), to create new profile
* Launch minecraft in -1.17.1 profile
* Downloaded from curseforge.com ~/Minecraft/mods/1.17.1/:
* malilib--1.17.1-0.10.0-dev.23.jar
* minihud--1.17.1-0.19.0-dev.20210707.150016.jar
* litematica--1.17.1-0.0.0-dev.20210707.011234.jar
* Copied 3 mods into ~/.minecraft/mods/
* Launch minecraft in -1.17.1 profile
(Minecraft)


Fri 9-Jul-2021
^^^^^^^^^^^^^^

Telus Security assessment of alarm system for update.

Continued backfilling nowacst-agrif:
    wait for automation to fail
    make_forcing_links orcinus nowcast-agrif --run-date 2021-06-27
    wait for run to finish
    make_forcing_links orcinus nowcast-agrif --run-date 2021-06-28
    wait for run to finish
    make_forcing_links orcinus nowcast-agrif --run-date 2021-06-29
Emailed Mark re: >4h run times.
Resumed trying to sort out why nowcast-dev won't run on salish since upgrade to 18.04; compared libnetcdf* on skookum, salish and arbutus:
* arbutus:
    ubuntu@nowcast0:~$ ls /usr/lib/libnetcdf*
    ls: cannot access '/usr/lib/libnetcdf*': No such file or directory

    ubuntu@nowcast0:~$ ls -1 /usr/lib/x86_64-linux-gnu/libnetcdf*
    /usr/lib/x86_64-linux-gnu/libnetcdf.settings
    /usr/lib/x86_64-linux-gnu/libnetcdf.so
    /usr/lib/x86_64-linux-gnu/libnetcdf.so.13
    /usr/lib/x86_64-linux-gnu/libnetcdff.a
    /usr/lib/x86_64-linux-gnu/libnetcdff.so
    /usr/lib/x86_64-linux-gnu/libnetcdff.so.6
    /usr/lib/x86_64-linux-gnu/libnetcdff.so.6.1.1
* skookum:
    skookum:~$ ls -1 /usr/lib/libnetcdf*
    /usr/lib/libnetcdf_c++.so.4@
    /usr/lib/libnetcdf_c++.so.4.1.0
    /usr/lib/libnetcdff.so.5@
    /usr/lib/libnetcdff.so.5.1.0
    /usr/lib/libnetcdf.so.7@
    /usr/lib/libnetcdf.so.7.1.1

    skookum:~$ ls -1 /usr/lib/x86_64-linux-gnu/libnetcdf*
    /usr/lib/x86_64-linux-gnu/libnetcdf.settings
    /usr/lib/x86_64-linux-gnu/libnetcdf.so@
    /usr/lib/x86_64-linux-gnu/libnetcdf.so.13
* salish:
    salish:~$ ls -1 /usr/lib/libnetcdf*
    /usr/lib/libnetcdf_c++.so@
    /usr/lib/libnetcdf_c++.so.4@
    /usr/lib/libnetcdf_c++.so.4.1.0
    /usr/lib/libnetcdff.so@
    /usr/lib/libnetcdff.so.5@
    /usr/lib/libnetcdff.so.5.1.0
    /usr/lib/libnetcdf.so@
    /usr/lib/libnetcdf.so.7@
    /usr/lib/libnetcdf.so.7.1.1

    salish:~$ ls -1 /usr/lib/x86_64-linux-gnu/libnetcdf*
    /usr/lib/x86_64-linux-gnu/libnetcdff.a
    /usr/lib/x86_64-linux-gnu/libnetcdff.so@
    /usr/lib/x86_64-linux-gnu/libnetcdff.so.6@
    /usr/lib/x86_64-linux-gnu/libnetcdff.so.6.1.1
    /usr/lib/x86_64-linux-gnu/libnetcdf.settings
    /usr/lib/x86_64-linux-gnu/libnetcdf.so@
    /usr/lib/x86_64-linux-gnu/libnetcdf.so.11@
    /usr/lib/x86_64-linux-gnu/libnetcdf.so.11.0.0
    /usr/lib/x86_64-linux-gnu/libnetcdf.so.13
What I want to do on salish:
    apt purge libnetcdf11
    apt purge libnetcdfc++4
    apt purge libnetcdfc7
    apt purge libnetcdff5
    apt purge libhdf5-10
    apt purge libhdf5-7
What I did on salish:
    apt purge libnetcdf11
        triggered removal of libhdf5-10
    apt purge libnetcdfc++4
    apt purge libnetcdfc7
        triggered removal of libnetcdff5
    apt purge libhdf5-7
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
(SalishSeaCast)


Sat 10-Jul-2021
^^^^^^^^^^^^^^^

Drove to White Rock to visit J&M.

Continued backfilling nowacst-agrif:
wait for automation to fail
make_forcing_links orcinus nowcast-agrif --run-date 2021-06-30
wait for run to finish
make_forcing_links orcinus nowcast-agrif --run-date 2021-07-01
(SalishSeaCast)


Sun 11-Jul-2021
^^^^^^^^^^^^^^^

collect_weather 06 stalled; investigation:
* 404 message in sarracenia log:
    2021-07-11 02:24:58,295 [WARNING] sr_amqp/consume: could not consume in queue q_anonymous.sr_subscribe.hrdps-west.74434425.78671301: Basic.get: (404) NOT_FOUND - failed to perform operation on queue 'q_anonymous.sr_subscribe.hrdps-west.74434425.78671301' in vhost '/' due to timeout
* 506 of 576 files downloaded; 10 files missing from hour 001, and all files missing from hours 002-006
* recovery:
    pkill -f collect_weather
    rm -rf /results/forcing/atmospheric/GEM2.5/GRIB/20210711/06
    download_weather 06 2.5km
    collect_weather 18 2.5km
    wait for forecast2 runs to finish
    download_weather 12 2.5km
Found another 404 in sarracenia log:
    2021-07-11 09:47:29,288 [WARNING] sr_amqp/consume: could not consume in queue q_anonymous.sr_subscribe.hrdps-west.74434425.78671301: Basic.get: (404) NOT_FOUND - failed to perform operation on queue 'q_anonymous.sr_subscribe.hrdps-west.74434425.78671301' in vhost '/' due to timeout
forecast2 runs catch-up failed due to upload_forcing connection failure on arbutus; investigation:
* nowcast0 shut down
     Request ID  Action  Start Time  User ID  Message 
    req-e6458e48-c215-4844-89b9-ebfd7f67840c 	Stop 	July 10, 2021, 5:16 p.m. 	- 
* nowcast6 shut down
    req-6ad1f4f1-9966-40a2-92bc-fbf5605083d2 	Stop 	July 10, 2021, 5:16 p.m. 	- 
* recovery:
    * started nowcast0 via dashboard
    * took the opportunity to do apt update && apt upgrade; minor pkg upgrades so didn't reboot
    * /nemoShare did not automatically remount
    * sudo mount /dev/vdc /nemoShare  # quite slow
    * /nemoShare/MEOPAR was not mounted at /export/MEOPAR for NFS
    * sudo mount --bind /nemoShare/MEOPAR /export/MEOPAR
    * ll /export/MEOPAR  # to confirm mount
    * sudo systemctl start nfs-kernel-server.service
    * started nowcast6 via dashboard
      * sudo mount -t nfs -o proto=tcp,port=2049 192.168.238.14:/MEOPAR /nemoShare/MEOPAR
    * sudo exportfs -f  # to reset NFS handles for compute nodes
    * confirm compute nodes have /nemoShare/MEOPAR/ mounted:
    * for n in {1..9}; do   echo nowcast${n};   ssh nowcast${n} "mountpoint /nemoShare/MEOPAR"; done
    * for n in {0..6}; do   echo fvcom${n};   ssh fvcom${n} "mountpoint /nemoShare/MEOPAR"; done
    * restarted automation at ~12:30:
        upload_forcing arbutus forecast2
No message from watch_NEMO on arbutus, so restarted log_aggregator.
forecast2 run failed - no time steps; investigation:
  * nowcast-green/10jul11 tmp run dir still in runs/
    * ocean.output ends with a blob of NULLs (^@)
  * VHFR nowcast-x2/10jul11 tmp run dir still in fvcom-runs
    * fvcom.log ends abruptly
* recovery:
    make_forcing_links arbutus nowcast-green 2021-07-10
        run failed because I forgot to re-mount /nemoShare/MEOPAR/ on nowcast6
    make_forcing_links arbutus nowcast-green 2021-07-10  # ~13:15
    launch_remote_worker arbutus make_ww3_wind_file arbutus forecast 2021-07-10
    launch_remote_worker arbutus make_ww3_current_file arbutus forecast 2021-07-10
nowcast running slow (~2%/5min); replaces nowcast6 in mpi_hosts w/ nowcast2 to try to speed things up; didn't help because forecast ran slow too.
(SalishSeaCast)


Week 28
-------

Mon 12-Jul-2021
^^^^^^^^^^^^^^^

Week 70 of UBC work-from-home due to COVID-19

Assessed state of automation:
* last completed run was forecast/11jul21
* collect_weather was successful for all forecasts
Continued recovery/catch-up:
* restore nowcast6 node to cluster
    make_forcing_links arbutus nowcast-green 2021-07-11
  failed due to no turbidity file
    upload_forcing arbutus turbidity 2021-07-11
  nowcast-green running at near normal speed
    make_forcing_links arbutus nowcast+ 2021-07-12
Continued backfilling nowacst-agrif:
    wait for automation to fail
    make_forcing_links orcinus nowcast-agrif --run-date 2021-07-02
        # back on pod29 and running at full speed :-)
    wait for run to finish
    make_forcing_links orcinus nowcast-agrif --run-date 2021-07-03
    wait for run to finish
    make_forcing_links orcinus nowcast-agrif --run-date 2021-07-04
    wait for run to finish
    make_forcing_links orcinus nowcast-agrif --run-date 2021-07-05
Started backfilling VHFR runs:
    launch_remote_worker arbutus make_fvcom_boundary "arbutus x2 nowcast 2021-07-10"
(SalishSeaCast)

Stakeholder workshop day 1:
Breakout discussion:
  * Cat Galbraith: all useful for marine spatial planning; had to leave
  1a & 1b:
  * Sam Mansfield:
    * 1a better for prep; 1b better for response
    * both effective for vizualization
  * Charmaine Bosse:
    * 1a more useful than 1b for preparedness
  * Lee Britton
    * 1a useful for planning response resources placement
    * 1b would like to see confidence intervals
  * Nathan Leung:
    * both useful; 1a for resource placement planning; 1b for exercise for response
  2c & 2d: location; beaching & water column
  * Nathan:
    * 2c more useful; beaching more likely to be cleaned up
  * Lee:
    * **soluble fraction in water column (2d) would be useful for sampling planning for ecosystem impacts**
  * Sam:
    * 2c useful for inform baseline shoreline collection survey (scat surveys)
  * Lee:
    * need shorline hydraulics; 2c is useful
  3e & 3f
  * Charmaine & Sam:
    * equally useful; slight nod to probability
    * threshold by oil type might be useful
  * Lee:
    * vast majority if of oil on water is marine diesel; but concern is bunker
  * Nathan:
    * concentration useful for size of response resources allocation
  4g & 4f
  * Lee:
    * OilMap produces this kind of output
    * volume of spill is important; lots of inconsistency in units of volume; m3, litres, barrels, gallons
  5i & 5j: AIS vessel tracks
  * Sam:
    * UVic research on improving AIS info for small vessels
  * Charmaine & Lee: 5i more useful
  * John:
    * vessel traffic centre also has data
  * Sam:
    * source of AIS data matters; terrestrial vs. satellite
(MIDOSS)


Tue 13-Jul-2021
^^^^^^^^^^^^^^^

Worked at ESB while Rita is at home.

Automation worked correctly overnight.
Continued backfilling VHFR runs:
    launch_remote_worker arbutus make_fvcom_boundary "arbutus x2 nowcast 2021-07-11"
    nowcast-x2 eta 13:22 and it was accurate
    forecast-x2 eta 17:14 and it was accurate
    nowcast-r12 eta 00:05 and it was accurate
    but... that means it is impossible to catch up!
  Continued backfilling nowacst-agrif:
    wait for automation to fail
    make_forcing_links orcinus nowcast-agrif --run-date 2021-07-06
    wait for run to finish
    make_forcing_links orcinus nowcast-agrif --run-date 2021-07-07
    wait for run to finish
    make_forcing_links orcinus nowcast-agrif --run-date 2021-07-08
    wait for run to finish
    make_forcing_links orcinus nowcast-agrif --run-date 2021-07-09
    wait for run to finish
    make_forcing_links orcinus nowcast-agrif --run-date 2021-07-10
    wait for run to finish
    make_forcing_links orcinus nowcast-agrif --run-date 2021-07-11
    crashed quickly; probably forcing problem
(SalishSeaCast)

Completed new UBC COVID-19 safety training and send cert to Tim.

Started work on deployment of Ben's MIDOSS model results viz app:
* kudu:
  * clone repo
  * debugged symlink to tiles and a couple of other minor issue w/ Ben on Slack
  * added deployment notes to README
* skookum:
  * clone repo
  * created symlink to Ben's tiles tree
  * tweaked env-dev.yaml
  * created midoss-app-dev env
  * did editable install of app in env
  * added reverse proxy to /etc/apache2/sites-enabled/000-default.conf; some trial and error; added comments re: order of proxies
  * thrashed trying to figure out to get static assets served properly
(MIDOSS)


Wed 14-Jul-2021
^^^^^^^^^^^^^^^

Treid to watch SHARCNET webinar on Hybrid MPI, but had the time wrong in my calendar and came in at the end; check for recorded version on Youtube by end of week.

Automation worked correctly overnight.
Continued backfilling VHFR runs:
    launch_remote_worker arbutus make_fvcom_boundary "arbutus x2 nowcast 2021-07-12"
    nowcast-x2 eta 12:39 (2:32:27 run time); finished at 12:46
    forecast-x2 eta 18:11 (5:15:37 run time)
Finished backfilling nowacst-agrif:
* investigate yesterday's 11jul failure:
    * missing turbidity forcing file
    wait for automation to fail
    upload_forcing orcinus nowcast+ --run-date 2021-07-11
    upload_forcing orcinus turbidity --run-date 2021-07-11
    wait for run to finish; took 3h55m; emailed Mark
    make_forcing_links orcinus nowcast-agrif --run-date 2021-07-12
    wait for run to finish; back to ~47m
    make_forcing_links orcinus nowcast-agrif --run-date 2021-07-13
    wait for run to finish
    make_forcing_links orcinus nowcast-agrif --run-date 2021-07-14
(SalishSeaCast)

Worked on master bathroom toilet; cleaned mildew; found cracked/broken piece in button interface assembly; refill seems to work at internal button level, so problem is maybe due to broken piece.

Stakeholder workshop prep mtg.
Finished deployment of midoss-app-dev in a tmux session on skookum mounted at salishsea.eos.ubc.ca/midoss:
* streamlined env for deployment
* added rutter to env so that app can be mounted with a URL prefix
* created production.ini for deployment; including bump from 4 to 8 threads after seeing thread queue warnings in log
* debugged apache config for reverse proxy
(MIDOSS)


Thu 15-Jul-2021
^^^^^^^^^^^^^^^

Automation worked correctly overnight.
Continued backfilling VHFR runs:
    launch_remote_worker arbutus make_fvcom_boundary "arbutus x2 nowcast 2021-07-13"
* hacked mpi_hosts to use NEMO nodes for r12 after NEMO & WWatch3 runs finsihed for the day
    launch_remote_worker arbutus make_fvcom_boundary "arbutus r12 nowcast 2021-07-13"
(SalishSeaCast)

Group mtg; see whiteboard.
Various updates to cookiecutter-MOAD-pypkg based on experience of using it to initialize AtlantisCmd.
(MOAD)

Paused GoMSS Nowcast site monitor on uptimerobot because its no longer my concern.

Weekly project mtg.
Started dev of AtlantisCmd from MOAD pypkg cookiecutter.
(Atlantis)


Fri 16-Jul-2021
^^^^^^^^^^^^^^^

Automation worked correctly overnight.
Continued backfilling VHFR runs:
    launch_remote_worker arbutus make_fvcom_boundary "arbutus x2 nowcast 2021-07-14"
    wait for runs to finish ~17:30
    launch_remote_worker arbutus make_fvcom_boundary "arbutus x2 nowcast 2021-07-15"
* use NEMO nodes for r12 after NEMO & WWatch3 runs finsihed for the day
    wait for ww3-forecast to finish ~12:30
    launch_remote_worker arbutus make_fvcom_boundary "arbutus r12 nowcast 2021-07-14"
    wait for run to finish ~19:30
    launch_remote_worker arbutus make_fvcom_boundary "arbutus r12 nowcast 2021-07-15"
(SalishSeaCast)

Created PR#1 in analysis-raisha to add CSIRO to copyright holders.
Continued dev of AtlantisCmd; mostly docs setup.
(Atlantis)

Loaded WTB Nano 700x42 tires & tubes from Tommy to Becca.

Started reviewing Rachael's changes to random_oil_spills.py in her add_terminal branch, and fixing broken unit tests.
(MIDOSS)


Sat 17-Jul-2021
^^^^^^^^^^^^^^^

x2 and r12 runs for 15jul completed successfully
upload_forcing forecast2 and nowcast+ failed due to missing Neah Bay ssh file; investigation:
    * Susan found that make_ssh_files failed silently due to bad values in etss csv file
recovery:
    * Susan removed bad rows from 06 & 00 etss csv files
    * symlinked modified etss csv files in place of broken ones
    * manually ran
        make_ssh_files nowcast 2021-07-17
        upload_forcing arbutus nowcast+
        upload_forcing orcinus nowcast+
        upload_forcing graham nowcast+
        upload_forcing optimum nowcast+
Continued backfilling VHFR runs:
    wait for automation to fail
    launch_remote_worker arbutus make_fvcom_boundary "arbutus x2 nowcast 2021-07-16"
* use NEMO nodes for r12 after NEMO & WWatch3 runs finsihed for the day
    wait for ww3-forecast to finish ~14:00
    launch_remote_worker arbutus make_fvcom_boundary "arbutus r12 nowcast 2021-07-16"
    too late to get another run in before forecast2 runs
(SalishSeaCast)


Sun 18-Jul-2021
^^^^^^^^^^^^^^^

Continued backfilling VHFR runs:
    wait for automation to fail
    launch_remote_worker arbutus make_fvcom_boundary "arbutus x2 nowcast 2021-07-17"
    wait for runs to finish ~20:00
    launch_remote_worker arbutus make_fvcom_boundary "arbutus x2 nowcast 2021-07-18"
* use NEMO nodes for r12 after NEMO & WWatch3 runs finsihed for the day
    wait for ww3-forecast and bike ride to finish
    launch_remote_worker arbutus make_fvcom_boundary "arbutus r12 nowcast 2021-07-17"
    too late to get another run in before forecast2 runs
(SalishSeaCast)

Cycled around UBC, across Midtown/Ridgeway to Kennsington Park, down Dumphries to Kent, and home (44 km). Back was stiff and hips off-centre when I finished :-(


Week 29
-------

Mon 19-Jul-2021
^^^^^^^^^^^^^^^

Week 71 of UBC work-from-home due to COVID-19

Worked w/ Ben on last minute fixes & deployment of demo viz app for workshop.
Stakeholder workshop day 2:
Technical breakout room:
* Are there fields or outputs that we are missing? We do presence, concentration, timing.
  * John Davis:
    * have what is needed
  * Lee Britton
    * need confidence/certainty measure
    * discussion of Monte Carlo concept w/ Susan
  * John Davis:
    * arial photography and collector beaches
  * Patrick O'Hara
    * stocastic model?
    * how well do underlying models capture stocasticity of systems?
    * representation of fields:
      * median may not be sufficient as some spatial areas/scales; seasonal may be particularly important
      * wants to think more about statistics; excited about direction Monte Carlo modelling is taking in contrast to significant spill modelling
  * Haibo:
    * discussion of uncertainty rep in response to Lee's question/comments

Data distribution & visualization discussion:
* Sam Mansfield:
  * Hub e-GIS via ESRI
  * data sources like OpenScience data platform
* John Davis:
  * social info layers important
* Warren Mills; is this useful to municipality
  * yes, but paper is important too
* Mike Andrews
  * 80-90% of communities are ESRI clients
  * want API feeds
* Andrew (Raincoast)
  * public access?
    * Mike: would produce products for public
* Lee:
  * wants WMS
  * shared https://geonode.org/ as means of distributing data?
(MIDOSS)

Continued backfilling VHFR runs:
* VHFR x2 ran in automation!!
* use NEMO nodes for r12 after NEMO & WWatch3 runs finsihed for the day
    wait for ww3-forecast and bike ride to finish
    launch_remote_worker arbutus make_fvcom_boundary "arbutus r12 nowcast 2021-07-18"
    wait for run to finish ~20:15
    launch_remote_worker arbutus make_fvcom_boundary "arbutus r12 nowcast 2021-07-19"
(SalishSeaCast)

Continued dev of AtlantisCmd:
* added cliff framework
* decided to use cookiecutter for tmp run dir like WWatch3Cmd
* started run sub-command
(Atlantis)


Tue 20-Jul-2021
^^^^^^^^^^^^^^^

Continued dev of AtlantisCmd:
* finished run sub-command parser tests
* added pre-commit framework:
* add pre-commit to dev env description
* generate .pre-commit-config.yaml w/
pre-commit sample-config > .pre-commit-config.yaml
pre-commit autoupdate
* edit .pre-commit-config.yaml:
* add black
* update versions w/
pre-commit autoupdate
* install git hook scripts:
pre-commit install
* run against all files:
pre-commit run --all-files
* started work on run() creation of tmp run dir via cookiecutter
(Atlantis)


Wed 21-Jul-2021
^^^^^^^^^^^^^^^

Alarm system upgrade.

Continued dev of AtlantisCmd:
* continued work on run() creation of tmp run dir via cookiecutter
(Atlantis)


Thu 22-Jul-2021
^^^^^^^^^^^^^^^

Uptimerobot reported ERDDAP was down for ~33m around 09:00.
nowcast-green reported no progress after starting at 10:14; nowcast-x2 stopped reporting progress after 10:13
* action log in web dashboard says nowcast0 was stopped at 17:16 UTC == 10:16 Pacific
     Request ID  Action  Start Time  User ID  Message
    req-f9b0d480-f3c8-4b0b-9470-7cc567fa8204 	Stop 	July 22, 2021, 5:16 p.m. 	- 	- 
* started nowcast0 via dashboard
* took the opportunity to do apt update && apt upgrade and rebooted
* /nemoShare did not automatically remount
* sudo mount /dev/vdc /nemoShare  # quite slow
* /nemoShare/MEOPAR was not mounted at /export/MEOPAR for NFS
* sudo mount --bind /nemoShare/MEOPAR /export/MEOPAR
* ll /export/MEOPAR  # to confirm mount
* sudo systemctl start nfs-kernel-server.service
* sudo exportfs -f  # to reset NFS handles for compute nodes
* confirm compute nodes have /nemoShare/MEOPAR/ mounted:
* for n in {1..9}; do   echo nowcast${n};   ssh nowcast${n} "mountpoint /nemoShare/MEOPAR"; done
* for n in {0..6}; do   echo fvcom${n};   ssh fvcom${n} "mountpoint /nemoShare/MEOPAR"; done
* restarted automation at ~11:45:
    make_forcing_link arbutus nowcast-green
    launch_remote_worker arbutus run_fvcom "arbutus.cloud-nowcast x2 nowcast --run-date 2021-07-22"
* no messages from watch_NEMO
    restart log_aggregator
    restart message_broker
  * download_results forecast failed due to nowcast0 node stop; re-ran manually ~13:18
(SalishSeaCast)

Reviewed and helped polish Susan's NSERC NOI.

Faron Anslow (PCIC) CMOS talk on Atribution Analysis of Late June heat Event:
* Can an atmospheric river contribute to a heatwave?
* 1 in 10 to 1 in 5 return in +2C world
* 2C due to global warming, but excess was 5C - so other processes
* why:
  * long days
  * clear skies
  * dry spring
  * thermal trough & small upper low
  * mountain waves & downslope winds
  * lots of water vapour (atmos river hitting Alaska & St. Elias range) provided latent heat to atmosper

Continued dev of AtlantisCmd:
* continued work on run() creation of tmp run dir via cookiecutter
Weekly team mtg:
* Javier explained https://bitbucket.csiro.au/users/por07g/repos/ssam_oceanparcels/ for calculation of oil particle input/forcing for Atlantis
Added GHA workflow for CodeQL analysis to repo, and it passed on 1st run :-)
(Atlantis)


Fri 23-Jul-2021
^^^^^^^^^^^^^^^

Woke up stuffy, w/ itchy eyes & slight headache; no energy all day.

upload_forcing forecast2 and nowcast+ failed due to missing Neah Bay ssh file; investigation:
    * Susan found that etss csv files contain bad values
recovery:
    ln -s /results/forcing/sshNeahBay/fcst/ssh_y2021m07d22.nc /results/forcing/sshNeahBay/obs/ssh_y2021m07d22.nc
    upload_forcing arbutus nowcast+
    upload_forcing orcinus nowcast+
    upload_forcing graham nowcast+
    upload_forcing optimum nowcast+
(SalishSeaCast)


Sat 24-Jul-2021
^^^^^^^^^^^^^^^

Vancouver to Sooke (Seagull Studio)


Sun 25-Jul-2021
^^^^^^^^^^^^^^^

Sooke

Cycled around Sooke exploring bluffs, beaches & neighbourhoos. (21 km)


Week 30
-------

Mon 26-Jul-2021
^^^^^^^^^^^^^^^

Week 72 of UBC work-from-home due to COVID-19

Sooke

Hiked in East Sooke Regional Park; Pike Rd, Pike Pt., Iron Mine Bay, Coast Trail to Copper Mine Creek and back; connector trail; Anderson Creek, Pike Rd.; OM-D photos at Pie Pt

Re-installed RaphidPhotoDownloader under miniconda base Python 3.9 in virtualenv:
    2006  python3 -m venv RapidPhotoDownloader-py3.9
    2007  source RapidPhotoDownloader-py3.9/bin/activate
    2008  python3 install.py --virtual-env
    2009  python3 -m pip --version
    2010  python3 -m pip install wheel
    2011  python3 -m pip install -U pip
    2012  python3 -m pip --version
    2013  python3 -m pip install wheel
    2014  python3 -m pip install -U wheel
    2015  python3 install.py --virtual-env
    2016  /media/doug/warehouse/Pictures/RapidPhotoDownloader-0.9.14/RapidPhotoDownloader-py3.9/bin/rapid-photo-downloader


Tue 27-Jul-2021
^^^^^^^^^^^^^^^

Sooke

Cycled Sticleback and Galloping Goose trails to Leechtown and back (48 km)

    
Wed 28-Jul-2021
^^^^^^^^^^^^^^^

Sooke

Discovered that collect_weather 18 never completed yesterday; investigation:
* 530 of 576 files; missing 10 in hour 044, and all of hours 045-047
* sarracenia log:
    2021-07-27 15:09:12,568 [WARNING] sr_amqp/consume: could not consume in queue q_anonymous.sr_subscribe.hrdps-west.74434425.78671301: [Errno 104] Connection reset by peer
    2021-07-27 15:09:12,568 [ERROR] sr_amqp/close 2: [Errno 32] Broken pipe
    2021-07-27 15:09:12,568 [INFO] Using amqp module (AMQP 0-9-1)
    2021-07-27 15:09:15,687 [INFO] declared queue q_anonymous.sr_subscribe.hrdps-west.74434425.78671301 (anonymous@dd.weather.gc.ca) 
    2021-07-27 15:14:24,499 [ERROR] Download failed 3 https://dd5.weather.gc.ca//model_hrdps/west/grib2/18/044/CMC_hrdps_west_PRATE_SFC_0_ps2.5km_2021072718_P044-00.grib2
    2021-07-27 15:14:24,563 [WARNING] downloading again, attempt 2
    2021-07-27 15:14:24,886 [INFO] file_log downloaded to: /SalishSeaCast/datamart/hrdps-west/18/044/CMC_hrdps_west_PRATE_SFC_0_ps2.5km_2021072718_P044-00.grib2
    2021-07-27 15:14:24,886 [INFO] heartbeat. Sarracenia version is: 2.20.08post1 

    2021-07-27 15:14:24,887 [INFO] hb_memory cpu_times user=3040.45 system=346.38 elapse=24799091.01
    2021-07-27 15:14:24,887 [INFO] hb_memory, current usage: 61.7 MiB trigger restart if increases past: 167.4 MiB 
    2021-07-27 15:14:24,887 [INFO] hb_retry on_heartbeat
    2021-07-27 15:14:24,887 [INFO] sr_retry on_heartbeat
    2021-07-27 15:14:24,899 [INFO] No retry in list
    2021-07-27 15:14:24,902 [INFO] sr_retry on_heartbeat elapse 0.014523
    2021-07-27 15:14:25,038 [WARNING] sr_amqp/consume: could not consume in queue q_anonymous.sr_subscribe.hrdps-west.74434425.78671301: Basic.get: (404) NOT_FOUND - no queue 'q_anonymous.sr_subscribe.hrdps-west.74434425.78671301' in vhost '/'
* recovery started at ~09:15:
    pkill collect_weather 18
    rm -rf /results/forcing/atmospheric/GEM2.5/GRIB/20210727/18
    download_weather 18 2.5km
    download_weather 00 2.5km
    collect_weather 18 2.5km
    download_weather 06 2.5km
    wait for forecast2 runs to finish
    download_weather 12 2.5km
(SalishSeaCast)

Walked to the end of Whiffen Spit and back during forecast2 runs; OM-D photos.
Visited wool shop, Sooke Oceanside Brewing, and Bad Dog Brewing.
Walked to Sherringham Pt lighthouse, and around Sherringham forest loop; OM-D photos.

    
Thu 29-Jul-2021
^^^^^^^^^^^^^^^

Sooke

Cycled Billings Spit, Galloping Goose to Pearson College, William Head, Taylor Beach, Galloping Goose, Matheson Lake, Stickleback (60 km)

    
Fri 30-Jul-2021
^^^^^^^^^^^^^^^

Sooke

Hiked Sooke Potholes (disappointing), and East Sooke Park: Aylard Farm, Creyke Pt., Coast Trail, Beechey Head.

Strained back in shower after hike.

    
Sat 31-Jul-2021
^^^^^^^^^^^^^^^

Sooke to Sydney

Afternoon and dinner at Debby & Paul's

nowcast-agrif run timed out
(SalishSeaCast)

    
Sun 1-Aug-2021
^^^^^^^^^^^^^^

Sydney, White Rock, Vancouver

Visited J&M on the way home from Van Is.


Week 31
-------

Mon 2-Aug-2021
^^^^^^^^^^^^^^

Week 73 of UBC work-from-home due to COVID-19

**Statutory Holiday** - BC Day

Back pain improved to overall stiffness rather than acute in lower right.

/home/doug/ filled on kudu to the point where I couldn't fully reboot; resolution:
* cleaned old linux images & headers
* cleaned unused flatpak installations:
    flatpak update --appstream
    flatpak update
    flatpak uninstall --unused
* uninstalled Signal flatpak
* deleted left-over Signal & Teams flatpak files
* moved Minecraft/ to /media/doug/warehouse/
Updated kudu to Pop_OS! 21.04.


Tue 3-Aug-2021
^^^^^^^^^^^^^^

Brought worklog up to date.

Investigated MIDOSS/docs monthly linkcheck errors:
* conda.io cert issue; wait & see
* wiki.mohid.com timeout; wait & see
(MIDOSS)

Investigated upload_forcing errors:
* missing atmos fcst/ directory and all but 1 ops file on graham
* missing all but 1 NeahBay ssh obs/ file on graham
* turns out that Tereza deleted:
    $PROJECT/SalishSea/forcing/rivers/river_turb/*
    $PROJECT/SalishSea/forcing/sshNeahBay/obs/*
    $PROJECT/SalishSea/forcing/sshNeahBay/atmospheric/GEM2.5/operational/*
* recovery:
  * started bash loop in tmux session on skookum to re-run:
        upload_forcing graham nowcast+
        upload_forcing graham turbidity
    for 2021-08-02 to 2015-01-01
Backfilled nowcast-agrif:
    upload_forcing orcinus nowcast+ --run-date 2021-07-31
    make_forcing_links orcinus nowcast-agrif --run-date 2021-07-31
    make_forcing_links orcinus nowcast-agrif --run-date 2021-08-01
    make_forcing_links orcinus nowcast-agrif --run-date 2021-08-02
    make_forcing_links orcinus nowcast-agrif --run-date 2021-08-03
Backfilled VHFR plots.
(SalishSeaCast)

Changed darktable installation source on kudu to OpenSuse server from (unmaintained) launchpad.
Changed borgbackup installation source on kudu to system pkg from (un-updated) luanchpad.
Updated PyCharm on kudu to 2021.2.


Wed 4-Aug-2021
^^^^^^^^^^^^^^

Updated nowcast0 re: Linux security updates (CVE-2021-33909) aka Sequoia:
    sudo apt update
    sudo apt upgrade
    sudo shutdown -r now
    sudo mount /dev/vdc /nemoShare
    ll /nemnoSShare/MEOPAR  # to confirm mount
    sudo mount --bind /nemoShare/MEOPAR /export/MEOPAR
    ll /export/MEOPAR  # to confirm mount
    sudo systemctl start nfs-kernel-server.service
    sudo exportfs -f  # to reset NFS handles for compute nodes
    # confirm compute nodes have /nemoShare/MEOPAR/ mounted:
    for n in {1..9}; do   echo nowcast${n};   ssh nowcast${n} "mountpoint /nemoShare/MEOPAR"; done
    for n in {1..9}; do   echo nowcast${n};   ssh nowcast${n} "ls -C /nemoShare/MEOPAR"; done
    for n in {0..6}; do   echo fvcom${n};   ssh fvcom${n} "mountpoint /nemoShare/MEOPAR"; done
    for n in {0..6}; do   echo fvcom${n};   ssh fvcom${n} "ls -C /nemoShare/MEOPAR"; done
Continued forcing upload recovery on graham.
(SalishSeaCast)

Continued dev of AtlantisCmd.
(Atlantis)


Thu 5-Aug-2021
^^^^^^^^^^^^^^

Continued forcing upload recovery on graham.
Cleaned up a mess of zombie worker processes on skookum, mostly make_surface_current_tiles from mid-July; prompted by "no worker port" error overnight.
(SalishSeaCast)

UBC-DFO modelling mtg.

Continued dev of AtlantisCmd.
Weekly project mtg.
(Atlantis)


Fri 6-Aug-2021
^^^^^^^^^^^^^^

See work journal.
(Resilient-C)

Discovered that collect_weather 18 never completed yesterday; investigation:
* 276 of 576 files; missing all of hours 024-048
* lots of connection timed out and connection refused errors in sarracenia log
* recovery started at ~09:15:
    pkill collect_weather 18
    rm -rf /results/forcing/atmospheric/GEM2.5/GRIB/20210727/18
    download_weather 18 2.5km
    download_weather 00 2.5km
    collect_weather 18 2.5km
    download_weather 06 2.5km
    wait for forecast2 runs to finish
    download_weather 12 2.5km
(SalishSeaCast)

Continued dev of AtlantisCmd.
(Atlantis)


Sat 7-Aug-2021
^^^^^^^^^^^^^^

Scheduled arbutus network maintenance caused upload_forcing to fail at ~09:00; after a bunch of re-tries and some patience, successfully re-ran manually at ~11:25
(SalishSeaCast)


Sun 8-Aug-2021
^^^^^^^^^^^^^^

Cycled Richmond loop; River Rd,, No. & Rd, Westminster Hwy, Sidaway, No. 5 Rd. Dyke Rd. Railway.
Bought corn at CanWest Farms.


Week 32
-------

Mon 9-Aug-2021
^^^^^^^^^^^^^^

Week 74 of UBC work-from-home due to COVID-19

Investigated SalishSeaCast/docs linkcheck failure:
* http://pages.physics.cornell.edu/~myers/teaching/ComputationalMethods/LectureNotes/Intro_to_Python.pdf has gone away
* TODO:
  * re-write intro to Python section w/ new ref materials
  * think about where intro to Python and associated netCDF and model results docs go: SalishSeaCast/docs or UBC-MOAD/docs, or split
(SalishSeaCast)

Worked on DigiKam photos on lizzy:
* Changed collections root to /media/doug/warehouse/shared/photos/ from .../photos/iPhoto-originals so that I can keep multiple top-level albums in photos/

Group mtg; see whiteboard.
(MOAD)

Tried to install Opti and OptiFine for minecrat 1.17.1:
* download OptiFine from https://optifine.net/home
* download OptiFabric from https://www.curseforge.com/minecraft/mc-mods/optifabric
* Put both jars in .minecraft/mods/
* run OptiFine jar to install
* Minecraft refuses to load due to GLX driver version
* Removed OptiFine & Opti from mods/

Phys Ocgy seminar by Sofi Damarkis on marine heat waves


Tue 10-Aug-2021
^^^^^^^^^^^^^^^

Discovered that Prius is dead; maybe starter battery?

Stayed home to teach Rita how to set new alarm system, then worked at ESB while she is at home.

Continued dev of AtlantisCmd; first successful runs of 10d test run.
(Atlantis)

Dinner w/ Kristin & Kirk on their patio.


Wed 11-Aug-2021
^^^^^^^^^^^^^^^

Investigated setup of shared access git repo on /ocean/ for Susan et al to use for EOSC471; git init --bare --shared, and a dedicated group seem to be the key elements; created helpdesk ticket to request group creation.
(EOAS Teaching)

Helped Raisha sort out env issues; parcels deps appear to have downgraded libnetcdf so built atlantis-trunk fails.
(Atlantis)


Thu 12-Aug-2021
^^^^^^^^^^^^^^^

See work journal.
(Resilient-C)

Weekly project mtg.
(Atlantis)


Fri 13-Aug-2021
^^^^^^^^^^^^^^^

Coffee w/ Karyn.

Telus alarm service re: always active motion sensors & communications issue found remotely:
* checked config
* removed sensitivity reduction (pet) shield from downstairs motion detector
* reooted main panel; balcony door sensor was very slow to reconnect
* moved motion sensors out of and back into partition with other sensors
* tested alarm triggering by downstairs motion sensor
* motion sensor reporting in phone app is very laggy


Sat 14-Aug-2021
^^^^^^^^^^^^^^^

nowcast-r12 failed on launch; investigation;
* fvcom3: no route to host; no info in action log; soft reboot failed
* recovery at ~20:15:
    replaced fvcom3 ip in mpi_hosts w/ fvcom2
    launch_remote_worker arbutus make_fvcom_boundary "arbutus r12 nowcast 2021-08-14"
* running slowly (>20hr)
(SalishSeaCast)


Sun 15-Aug-2021
^^^^^^^^^^^^^^^

nowcast-r12 didn't finish; nowcast-x2 running on same node
* killed nowcast-r12/14aug21
* backfilling nowcast-r12
    replaced fvcom3 ip in mpi_hosts w/ fvcom2
    launch_remote_worker arbutus make_fvcom_boundary "arbutus r12 nowcast 2021-08-14"
(SalishSeaCast)

Finally started unpacking family history books and photo albums from Barrie.


Week 33
-------

Mon 16-Aug-2021
^^^^^^^^^^^^^^^

Week 75 of UBC work-from-home due to COVID-19

Helped Susan & Birgit get working w/ EOAS GitLab; bumped Birgit up to Maintainer role to see if that resolved her "can't push initial commit" problem; noted sluggish response to almost everything; e.g. Susan's invitation acceptance intially went 404.

nowcast-r12 didn't finish; nowcast-x2 running on same node
* killed nowcast-r12/14aug21
* backfilling nowcast-r12
    wait for 16aug21 run to fail ~18:45
    launch_remote_worker arbutus make_fvcom_boundary "arbutus r12 nowcast 2021-08-15"
    wait for run to complete
    launch_remote_worker arbutus make_fvcom_boundary "arbutus r12 nowcast 2021-08-16"
* emailed cloud@ support:
  * fairly useless response from Jeam-François of calcul quebec
  * checked fvcom3 at ~12:10; reboot had completed ~28 minutes previously
  * remounted /nemoShare/MEOPAR/
  * restored fvcom3 to mpi_hosts file
(SalishSeaCast)

Group mtg; see whiteboard.
(MOAD)

Got Prius restarted:
* Called Pattison; they recommended Busters for jump/tow
* Called Busters; had to choose jump ot tow; chose jump
* Jump worked; confirmed that domelight was on
* Drove to UBC to drop off carboard, then too Pattison to leave car for checks and service

Started work on borg-backup framework for Susan's Linux laptop (greta);
* created emergency reserved space on lizzy:/media/doug/backup/borg/
    sudo fallocate -l 2G /media/doug/backup/borg/emergency_reserved_space


Tue 17-Aug-2021
^^^^^^^^^^^^^^^

Worked on helping Susan get logged into smelt console in an XFCE4 session.

collect_weather 12 had not finished at 10:00; investigation:
* sarracenia log shows no files yet from MSC at 10:00!!; none on datamart pages either
* files started to appear at 10:21
backfilling nowcast-r12
  wait for automation run to fail ~18:00
  launch_remote_worker arbutus make_fvcom_boundary "arbutus r12 nowcast 2021-08-16"
(SalishSeaCast)

Continued work on AtlantisCmd docs.
(Atlantis)


Wed 18-Aug-2021
^^^^^^^^^^^^^^^

Continued work on AtlantisCmd docs.
(Atlantis)

backfilling nowcast-r12
  wait for automation run to fail ~18:30
  launch_remote_worker arbutus make_fvcom_boundary "arbutus r12 nowcast 2021-08-17"
(SalishSeaCast)

Picked up Prius; all good.


Thu 19-Aug-2021
^^^^^^^^^^^^^^^

Finished initial work on AtlantisCmd docs.
Weekly project mtg.
(Atlantis)

backfilling nowcast-r12
  wait for automation run to fail ~18:30
  launch_remote_worker arbutus make_fvcom_boundary "arbutus r12 nowcast 2021-08-18"
(SalishSeaCast)

Coffee w/ Elise.
Coffee w/ Debby & Paul.

Added resource packs to minecraft client (because Optifine no longer works for me apparently):
    Vanilla Tweaks Resource Pack
    Version: 1.17
    Packs:
        BorderlessGlass
        BorderlessStainedGlass
        BorderlessTintedGlass
        GrassSides
        MyceliumSides
        PathSides
        SnowSides
        PodzolSides


Fri 20-Aug-2021
^^^^^^^^^^^^^^^

upload_forcing trubidity to graham failed due to auth glitch; worked on manual re-run
backfilling nowcast-r12
  wait for automation run to fail ~19:15
  launch_remote_worker arbutus make_fvcom_boundary "arbutus r12 nowcast 2021-08-19"
(SalishSeaCast)

See work journal.
(Resilient-C)

Allen family dinner at Amica


Sat 21-Aug-2021
^^^^^^^^^^^^^^^

download_live_ocean timed out at ~12:00; re-tried at ~12:50
backfilling nowcast-r12
  wait for automation run to fail ~19:15
  launch_remote_worker arbutus make_fvcom_boundary "arbutus r12 nowcast 2021-08-20"
(SalishSeaCast)

See work journal.
(Resilient-C)

Researched Wahoo, Tacx & Stages smart bike trainers.


Sun 22-Aug-2021
^^^^^^^^^^^^^^^

backfilling nowcast-r12
  wait for automation run to fail ~19:15
  launch_remote_worker arbutus make_fvcom_boundary "arbutus r12 nowcast 2021-08-21"
(SalishSeaCast)

Cycled to Deep Cove & back (46km)

X10 switch on upstairs bathroom empty light failed into constate relay cliking state.


Week 34
-------

Mon 23-Aug-2021
^^^^^^^^^^^^^^^

Week 76 of UBC work-from-home due to COVID-19

Vacation

Delivered basket chair to Jose.
Walked in QE Park.
Replaced switch on upstairs bathroom empty light w/ old-school 2 pole.

backfilling nowcast-r12
  wait for automation run to fail ~18:00
  launch_remote_worker arbutus make_fvcom_boundary "arbutus r12 nowcast 2021-08-22"
Squash-merged PRs from dependabot re: jupyterlab & notebook security vulernabilities in:
* SalishSeaCast/tools
* SalishSeaCast/analysis-doug
* SalishSeaCastSOG-Bloomcast-Ensemble
* 43ravens/ECGet
(SalishSeaCast)


Tue 24-Aug-2021
^^^^^^^^^^^^^^^

Vacation

Bike ride while Rita was at home; Iona Spit & North Fraser Spit (50 km)

Finished backfilling nowcast-r12:
  wait for automation run to fail ~16:55
  launch_remote_worker arbutus make_fvcom_boundary "arbutus r12 nowcast 2021-08-23"
  wait for run to finish ~00:00
  launch_remote_worker arbutus make_fvcom_boundary "arbutus r12 nowcast 2021-08-24"
nowcast-agrif failed; investigation:
* no 23aug21 or 22aug21 run
* 22aug21 run never started because upload_forcing turbidity failed due to ssh protocol banner read error
* backfilling:
    upload_forcing orcinus turbidity 2021-08-22
    make_forcing_links orcinus nowcast-agrif 2021-08-23
    wait for run to finish
    make_forcing_links orcinus nowcast-agrif 2021-08-24
(SalishSeaCast)

See work journal.
(Resilient-C)


Wed 25-Aug-2021
^^^^^^^^^^^^^^^

Vacation

Vancouver to Ocean Park

31st anniversary dinner w/ J&M, M,J&S at pool house Air BnB.


Thu 26-Aug-2021
^^^^^^^^^^^^^^^

Vacation

Ocean Park - Pool house Air BnB

See work journal.
(Resilient-C)

kudu reported root file system down to 882Mb
* deleted a bunch of old kernels with guidance from askubuntu (https://askubuntu.com/questions/345588/what-is-the-safest-way-to-clean-up-boot-partition)
* did flatpak cleanup:
    flatpak update --appstream
    flatpak update
    flatpak uninstall --unused
* disk usage app showed that /var/cache/apt/archives/ was largest consumer; cleaned up dramatically with:
    sudo apt autoclean
    
Cut and tasted bottle layer of wedding cake - 31 years old :-)

Added double shulker shells v1.3.0 datapack to CubedHost world.

nowcast-agrif timed out
(SalishSeaCast)


Fri 27-Aug-2021
^^^^^^^^^^^^^^^

Vacation

Ocean Park - Pool house Air BnB

See work journal.
(Resilient-C)

nowcast-agrif failed; investigation:
* excessive zonal velocity on 1st time step of 26aug21 run caused time-out
* Susan did averaging in physics restart file from end of 25aug21 run
(SalishSeaCast)

J 95th bday & J&M 63rd anniversary dinner w/ J&M, M,J&S at pool house Air BnB.


Sat 28-Aug-2021
^^^^^^^^^^^^^^^

Vacation

Ocean Park - Pool house Air BnB

backfilling nowcast-agrif:
* uploaded Susan's fixed physics restart file from end of 25aug21 run
    make_forcing_links orcinus nowcast-agrif 2021-08-26
    make_forcing_links orcinus nowcast-agrif 2021-08-27
    wait for run to finish
    make_forcing_links orcinus nowcast-agrif 2021-08-28
(SalishSeaCast)


Sun 29-Aug-2021
^^^^^^^^^^^^^^^

Vacation

Ocean Park to Vancouver

Cycled Cypress, MM Greenway, Heather, S Kent, Fraser River Trail, Benson, SWN, 16th, 8th, Pt. Grey (~32 km). Felt remarkkably strong going uphill & upwind on SWM.


Week 35
-------

Mon 30-Aug-2021
^^^^^^^^^^^^^^^

Week 77 of UBC work-from-home due to COVID-19

Worked w/ Susan to handle full /results/ partition; manually re-ran download_results forecast.
(SalishSeaCast)

Group mtg; see whtieboard.
(MOAD)

See work journal.
(Resilient-C)


Tue 31-Aug-2021
^^^^^^^^^^^^^^^

Helped Raisha with build of hydroconstruct.
(Atlantis)

Lokked at optifine again and discovered there was a final release for 1.71.1 yesterday.
Then found note on OptiFabric page that lead to https://gist.github.com/modmuss50/deff1658c4550ca8b16cb5d40ceaa468 saying that OptiFabric will be no longer developed due to OptiFine getting more and more invasive; recommnedation for performance improvement is Sodium.
* Downloaded Sodium frame rate optimzer from https://github.com/CaffeineMC/sodium-fabric/releases; works!
* Checked Phosphor lighting engine mod from https://github.com/CaffeineMC/phosphor-fabric/ but there is no 1.17.1 release yet.
* Downloaded Lithium optimizer from https://github.com/CaffeineMC/lithium-fabric/releases; works!

Answered email from Vanessa @ DFO asking for opinions on Python packages for reading GRIB2 files; suggested cfgrib backend for xarray.

Noticed at ~19:40 that fvcom-forecast had not reported to log since 13:35; investigation:
* arbutus nowcast0 node stopped without explanation at 20:38 UTC == 13:38 Pacific
* resolution:
* restarted nowcast0 from web dashboard at 02:44 UTC == 19:44 Pacific
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
    for n in {1..9}; do   echo nowcast${n};   ssh nowcast${n} "ls -C /nemoShare/MEOPAR"; done
    for n in {0..6}; do   echo fvcom${n};   ssh fvcom${n} "mountpoint /nemoShare/MEOPAR"; done
    for n in {0..6}; do   echo fvcom${n};   ssh fvcom${n} "ls -C /nemoShare/MEOPAR"; done
* on skookum:
      launch_remote_worker arbutus make_fvcom_boundary "arbutus x2 foreast 2021-08-31"
      no log msgs from watch_fvcom, so restarted log_aggregator 
      wait for run to finish ~23:40
      launch_remote_worker arbutus make_fvcom_boundary "arbutus r12 nowcast 2021-08-31"
(SalishSeaCast)


September
=========

Wed 1-Sep-2021
^^^^^^^^^^^^^^

collect_weather 12 didn't complete; investigation:
* lots of connection timeout and 404 errors in sarracenia log
* 247 of 576 files downloaded
* no files for hours 001-012, 030-036 & 041; missing files in hours 026, 028, 037-040, 042-044 & 046
* recovery:
    pkill collect_weather 12
    collect_weather 18 2.5km &
    rm -rf /results/forcing/atmospheric/GEM2.5/GRIB/20210901/12
    download_weather 12 2.5km
noticed at ~18:35 that nowcast-green was stalled at 8.8% complete; investigation:
* nowcast6 node stopped inexplicably at 18:05 UTC == 11:05 Pacific
* recovery:
  * restarted nowcast6 node via web dashboard
  * mounted shared storage:
      sudo mount -t nfs -o proto=tcp,port=2049 192.168.238.14:/MEOPAR /nemoShare/MEOPAR
  * on nowcast0:
      pkill -f watch_NEMO
      rm -rf 01sep21nowcast-green_2021-09-01T105826.488964-0700/
  * on skookum:
      make_forcing_links arbutus nowcast-green
(SalishSeaCast)

Worked w/ Susan:
* set up alarm.com web and phone app access
* set up backups from greta to lizzy:
  * created susan account on lizzy
  * mounted backup partition for susan
  * created borg repository w/ encryption and auto compression using zstd
  * cloned douglatornell/borg-backup repo to greta
  * tuned greta-lizzy.sh script


Thu 2-Sep-2021
^^^^^^^^^^^^^^

Continued work on conda section of docs.
(MOAD)

UBC-DFO modeling mtg; Tereza presented clustering work.
Post-mtg discussion of climate-HRDPS model correlation project w/ Susan, Michael & Amber.
(SalishSeaCast)

Weekly project mtg.
Worked w/ Javier & Raisha to get build config for HydroConstruct sorted out; required custom ./configure file that sets C*FLAGS & LDFLAGS vars after autoconfig generated ./configure.
(Atlantis)


Fri 3-Sep-2021
^^^^^^^^^^^^^^

Slack call w/ Raisha to work through initial use of AtlantisCmd and discuss where to store run descriptions & parameter files.
(Atlantis)

Helped Elise recover from having pushed a commit to the old master branch of rivers-climatology.
(SalishSeaCast)

See work journal.
(Resilient-C)


Sat 4-Sep-2021
^^^^^^^^^^^^^^

Goofed off.


Sun 5-Sep-2021
^^^^^^^^^^^^^^

Continued helping Elise recover from having pushed a commit to the old master branch of rivers-climatology.
(SalishSeaCast)


Week 36
-------

Mon 6-Sep-2021
^^^^^^^^^^^^^^

Week 78 of UBC work-from-home due to COVID-19

**Statutory Holiday** - Labour Day

Cycled Central Valley Greenway to North Rd; out via Burnaby Lake freeway trail, back via Winston (46 km)


Tue 7-Sep-2021
^^^^^^^^^^^^^^

Susan's surgery at derm clinic.

Cycled to Iona and home via Heather while Rita was at home (40 km)


Wed 8-Sep-2021
^^^^^^^^^^^^^^

Slack w/ Becca re: running Jupyter in tmux sessions.
Resumed trying to get nowcast-dev to work on salish 18.04:
* created conda env; env description stored for now in /SalishSeaCast/nowcast-dev-env.yaml:
    name: nowcast-dev

    channels:
    - conda-forge
    - nodefaults

    dependencies:
    - cxx-compiler
    - fortran-compiler
    - libnetcdf
    - netcdf-fortran
    - openmpi
* rely on system perl and perl-URI package
* built new XIOS-2 executable:
  * edit arch/arch-GCC_SALISH.fcm to point to mpicc & mpif90 in env
    cd /SalishSeaCast/XIOS-2
    ./tools/FCM/bin/fcm build --clean
    ./make_xios --arch GCC_SALISH --netcdf_lib netcdf4_seq --job 8
* built new NEMO SalishSeaCast_Blue executable:
  * edit arch/arch-GCC_SALISH.fcm to point to gcc, mpif90, and netcdf includes & lib in env
    cd /SalishSeaCast/NEMO-3.6-code/NEMOGCM/CONFIG
    XIOS_HOME=/SalishSeaCast/XIOS-2 ./makenemo -m GCC_SALISH -n SalishSeaCast_Blue clean
    XIOS_HOME=/SalishSeaCast/XIOS-2 ./makenemo -m GCC_SALISH -n SalishSeaCast_Blue -j8
* built new REBUILD_NEMO executable:
    cd /SalishSeaCast/NEMO-3.6-code/NEMOGCM/TOOLS/
    XIOS_HOME=/SalishSeaCast/XIOS-2 ./maketools -m GCC_SALISH -n REBUILD_NEMO clean
    XIOS_HOME=/SalishSeaCast/XIOS-2 ./maketools -m GCC_SALISH -n REBUILD_NEMO
* try to run 23apr21 run:
    make_forcing_links salish nowcast+ --shared-storage --run-date 2021-04-23
* run failed w/ no evidence of NEMO starting with 7 instances in stderr of:
    terminate called after throwing an instance of 'St9bad_alloc'
    what():  std::bad_alloc
* re-built new XIOS-2 executable:
  * edit arch/arch-GCC_SALISH.fcm to point to netcdf includes & lib in env
* run failed w/ no evidence of NEMO starting with **8** instances in stderr of:
    terminate called after throwing an instance of 'St9bad_alloc'
    what():  std::bad_alloc
(SalishSeaCast)

Squash-merged Dependabot PRs re: pillow:
* SalishSeaCast/SOG-Bloomcast-Ensemble
* SalishSeaCast/tools 
* SalishSeaCast/analysis-doug
* SalishSeaCast/SalishSeaNowcast
* UBC-MOAD/moad_tools


Thu 9-Sep-2021
^^^^^^^^^^^^^^

Compared output of ldd for nemo.exe between arbutus & salish nowcast-env builds; different in ways that I don't understand.
make_turbidity_file failed:
  ValueError: Anticipated and output hour were consistent: iout=14 ind=14 44446.166666666664 44446.131944444445
Recovery at ~16:30:
  symlink yesterday's file to persist
  upload_forcing arbutus turbidity
  upload_forcing orcinus turbidity
  upload_forcing graham turbidity
  upload_forcing optimum turbidity
(SalishSeaCast)

Continued work on ERDDAP dataset of month-averaged tracers for stakeholders:
* crafted ubcSSg3DuGridFields1moV19-05 dataset XML from ubcSSg3DuGridFields1hV19-05 and released it on ERDDAP
(ERDDAP)

Weekly project mtg.
(Atlantis)

Replied to email from Xinru Li in Geog asking for help w/ Python & dask.


Fri 10-Sep-2021
^^^^^^^^^^^^^^^

Drove Susan to UBC for 471 lecture and worked there for the day.

Paired w/ Raisha on Slack to figure out why HydroConstruct is not producing T&S files; turned out that it was segfaulting due to inconsistent values of tstart and tstop; can only process one time range file at a time and tstart/tstop need to be correct for file.
(Atlantis)

Long lunch w/ Birgit.

Finished work on ERDDAP dataset of month-averaged tracers for stakeholders:
* crafted ubcSSg3DvGridFields1moV19-05 dataset XML from ubcSSg3DvGridFields1hV19-05 and released it on ERDDAP
* crafted ubcSSg3DwGridFields1moV19-05 dataset XML from ubcSSg3DwGridFields1hV19-05 and released it on ERDDAP
(Prediction Core)

Improved metadata comments for gridY, gridX, and time coordinates.
(ERDDAP)


Sat 11-Sep-2021
^^^^^^^^^^^^^^^

FAL estate work re: BCE & Manulife:
Done:
* Waiver of Probate form
* Declaration of Transmission for BCE
* Declaration of Transmission for Manulife
TODO:
* Letter of direction for BCE shares
* Letter of direction for Manulife shares
* Letter stating the reason for not probating the will
* BCE dividend statement
* Manulife dividend statement
* Cheque to Insurance broker for 3.5% of BCE shares value
* Cheque to Insurance broker for 3.5% of Manulife shares value
* Cheque to AST for $131.25 ($125 + GST) for BCE shares processing
* Cheque to AST for $131.25 ($125 + GST) for Manulife shares processing
* Notarized signature of Waiver of Probate
* 4 notarized copies of death certificate
* 4 notarized copies of will
* Courier pkg to AST

* Send to Jamie for notarized signature:
  * Waiver of Probate form
* Send to Jamie as supporting information:
  * Letter of direction for BCE shares
  * Letter of direction for Manulife shares
  * Copy of death certificate
  * Copy of will
  * Copy of BCE dividend statement
  * Copy of Manulife dividend statement


Sun 12-Sep-2021
^^^^^^^^^^^^^^^

See work journal.
(Resilient-C)

download_results forecast failed; investigation:
* no messages from watch_NEMO for nowcast-green after it started at 10:14
* no messages from watch _fvcom for nowcast-x2 after 10:12
* nowcast0 stopped for no reason at 17:16 UTC == 10:16 Pacific
* recovery:
  * restarted nowcast0 from web dashboard at 20:09 UTC == 13:09 Pacific
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
      for n in {1..9}; do   echo nowcast${n};   ssh nowcast${n} "ls -C /nemoShare/MEOPAR"; done
      for n in {0..6}; do   echo fvcom${n};   ssh fvcom${n} "mountpoint /nemoShare/MEOPAR"; done
      for n in {0..6}; do   echo fvcom${n};   ssh fvcom${n} "ls -C /nemoShare/MEOPAR"; done
  * on skookum:
        # killed stalled processes
        make_forcing_links arbutus nowcast-green
        # no messages from watch_NEMO on arbutus
        # restarted log_aggregator
        launch_remote_worker arbutus make_fvcom_boundary "arbutus x2 nowcast 2021-09-12"
        download_results arbutus forecast
nowcast-green & nowcast-x2 stopped reporting at 14:39:
* web dashboard shows that nowcast0 stopped again for no reason at 21:43 UTC == 14:43
* recovery:
  * restarted nowcast0 from web dashboard at 22:24 UTC == 15:24 Pacific
      sudo mount /dev/vdc /nemoShare
      ll /nemoShare/MEOPAR/  # to confirm mount
      sudo mount --bind /nemoShare/MEOPAR /export/MEOPAR
      ll /export/MEOPAR  # to confirm mount
      sudo systemctl start nfs-kernel-server.service
      sudo exportfs -f  # to reset NFS handles for compute nodes
      # confirm compute nodes have /nemoShare/MEOPAR/ mounted:
      for n in {1..9}; do   echo nowcast${n};   ssh nowcast${n} "mountpoint /nemoShare/MEOPAR"; done
* discovered that nowcast6 also stopped for no reason at 21:43 UTC == 14:43
  * restarted nowcast6 from web dashboard at 22:28 UTC == 15:28 Pacific
      sudo mount -t nfs -o proto=tcp,port=2049 192.168.238.14:/MEOPAR /nemoShare/MEOPAR
* continued recovery of nowcast0:
      for n in {1..9}; do   echo nowcast${n};   ssh nowcast${n} "ls -C /nemoShare/MEOPAR"; done
      for n in {0..6}; do   echo fvcom${n};   ssh fvcom${n} "mountpoint /nemoShare/MEOPAR"; done
      for n in {0..6}; do   echo fvcom${n};   ssh fvcom${n} "ls -C /nemoShare/MEOPAR"; done
  * on skookum:
        # killed stalled processes
        make_forcing_links arbutus nowcast-green
        # no messages from watch_NEMO on arbutus
        # restarted log_aggregator
        launch_remote_worker arbutus make_fvcom_boundary "arbutus x2 nowcast 2021-09-12"
(SalishSeaCast)


Week 37
-------

Mon 13-Sep-2021
^^^^^^^^^^^^^^^

Week 79 of UBC work-from-home due to COVID-19

See work journal.
(Resilient-C)

Weekly group mtg; see whiteboard.
(MOAD)

Phys Ocgy seminar: introductions & Jose on AMOC collapse in climate models.


Tue 14-Sep-2021
^^^^^^^^^^^^^^^

Drove Susan to UBC for 471 lecture and worked there for the day.

See work journal.
(Resilient-C)

Started work on EOAS annual performance review.


Wed 15-Sep-2021
^^^^^^^^^^^^^^^

collect_weather 12 didn't complete; investigation:
* lots of connection refused (111) and at least 1 "expired message skipped" messages in sarracenia log
* 570 of 576 files downloaded
* missing files in hours 021 & 022
* recovery started at ~10:20:
    pkill collect_weather 12
    collect_weather 18 2.5km &
    rm -rf /results/forcing/atmospheric/GEM2.5/GRIB/20210915/12
    download_weather 12 2.5km
* lots of 404 and name resolution failures, then recoveries during download_weather
* hacked config to use https://hpfx.collab.science.gc.ca/20210915/WXO-DD/ for download_weather; killed and re-ran download_weather 12 2.5km, and it worked and was faster than download_weather usually is, probably due to the connection not being reset after every file
collect_weather 18 worked fine.
Removed and re-created kudu salishsea-nowcast env.
Changed config & download_weather to use https://hpfx.collab.science.gc.ca/{date}/WXO-DD/
* worked on hpfx-collab branch; rebased and merged work with the PyCharm equivalent of:
  git switch hpfx-collab
  git rebase main
  git switch main
  git merge hpfx-collab
Deployed change to skookum.
(SalishSeaCast)

Coffee w/ Jose.

Onboarding session on Slack w/ Jose.
(MOAD)


Thu 16-Sep-2021
^^^^^^^^^^^^^^^

Zoom w/ Xinru & Beatrix in Geog re: Python, dask, etc. for MHW analysis of global SST data.
(Prediction Core)

collect_weather 12 finished ~1h later than usual at ~10:00
download_live_ocean failed after ~3h; re-ran
(SalishSeaCast)

Fixed GHA linkcheck workflow in MOAD docs repo by adding www.baeldung.com/cs/ssh-intro to linkcheck ignore list.
(MOAD)

Weekly team mtg.
(Atlantis)

Drove Susan to UBC for late afternoon undergrad advising meet & greet.

Continued work on EOAS annual performance review.


Fri 17-Sep-2021
^^^^^^^^^^^^^^^

Drove Susan to UBC for 471 lecture and worked there for the day.

Telcon w/ Josh at Bicicletta re: trainer bikes:
* only 1 Tacx in stock; not sure of ETA
* Tacx road-feel feature is not that significant
* Tacx is more rigid; Kickr feels more like being on a bike
* no difference in reliability/problems; has happened w/ all and all have been resolved under warranties

Continued work on EOAS annual performance review.

Got Charles to fix numeric user name & no absent $HOME for Jose.
Changed group of /ocean/jvalenti to sallen, and set g+s permission.
(MOAD)


Sat 18-Sep-2021
^^^^^^^^^^^^^^^

upload_forcing orcinus failed due to ssh key permissions (probably a login node network stack issue); recovery:
  upload_forcing orcinus turbidity
Should have also done nowcast+ because run timed out.
(SalishSeaCast)

Drove to White Rock to visit J&M.


Sun 19-Sep-2021
^^^^^^^^^^^^^^^

Backfilled nowcast-agrif:
  upload_forcing orcinus nowcast+ 2021-09-18
  make_forcing_links orcinus nowcast-agrif 2021-09-18
  wait for run to finish
  make_forcing_links orcinus nowcast-agrif 2021-09-19
(SalishSeaCast)

Worked w/ Susan & Rachael to prepare for running near-BP 30 spill test.
(MIDOSS)

FAL estate work re: BCE & Manulife:
Done:
* Waiver of Probate form
* Declaration of Transmission for BCE
* Declaration of Transmission for Manulife
* Letter of direction for Manulife shares
* Letter of direction for BCE shares
* Letter stating the reason for not probating the will
TODO:
* copy BCE dividend statement x3
* copy Manulife dividend statement x3
After Jamie returns notarized waiver:
* Make appointment with notary
* Cheque to Insurance broker for 3.5% of BCE shares value
* Cheque to Insurance broker for 3.5% of Manulife shares value
* Cheque to AST for $131.25 ($125 + GST) for BCE shares processing
* Cheque to AST for $131.25 ($125 + GST) for Manulife shares processing
* Notarized signature of Waiver of Probate x2
* 4 notarized copies of death certificate
* 4 notarized copies of will
* Courier pkg to AST

* Send to Jamie for notarized signature:
  * Waiver of Probate form
* Send to Jamie as supporting information:
  * Letter of direction for BCE shares
  * Letter of direction for Manulife shares
  * Copy of death certificate
  * Copy of will
  * Copy of BCE dividend statement
  * Copy of Manulife dividend statement

Packed up old software and lulu backups optical media.
Packed up 1998-2003 financial and tax records.


Week 38
-------

Mon 20-Sep-2021
^^^^^^^^^^^^^^^

Week 80 of UBC work-from-home due to COVID-19

Federal election day

Changed Lagrangian_other.dat template to symlink to Lagrangian_bunker.dat instead of diesel.
Updated repos on graham in prep for running near-BP 1st 30 spills test run:
* Make-MIDOSS-Forcing
* MIDOSS-MOHID-config
* NEMO-Cmd
* SalishSeaCast-grid
* moad_tools
* MIDOSS-MOHID-CODE
* no changes in:
  * MIDOSS-MOHID-grid
  * MOHID-Cmd
Re-built MIDOSS-MOHID-CODE:
  module load StdEnv/2016.4
  module load python/3.8.2
  module load nco/4.6.6
  module load netcdf-fortran/4.4.4
  module load proj4-fortran/1.0
  cd $PROJECT/$USER/MIDOSS/MIDOSS-MOHID-CODE/Solutions/linux
  ./compile_mohid.sh -mb1 -mb2 -mw
Uploaded spill .csv file:
  rsync -tlv /ocean/sallen/allen/research/MIDOSS/19sep21/SalishSea_oil_spills_BP_first30.csv graham:project/dlatorne/MIDOSS/monte-carlo/
Created near-BP_first30.yaml.
Test run:
  mohid monte-carlo --debug near-BP_first30.yaml SalishSea_oil_spills_BP_first30.csv
.csv file is messed up; had leading empty column name, and leading row number; edited and submitted test run; succeeded.
(MIDOSS)

Finished 1st pass on EOAS annual performance review; passed to Susan for review.

Worked on Jose's auth problem on salish.
Group mtg; see whiteboard.
(MOAD)


Tue 21-Sep-2021
^^^^^^^^^^^^^^^

Drove Susan to UBC for 471 lecture and worked there for the day.

Updated OS pkgs & kernel on kudu; low memory on boot volume:
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
  # recovered 373 Mb == 57% of /boot
* clean up PyCharm cache (largest consumer in ~/.cache):
    File > Invalidate Caches
    restart Pycharm
    Help > Delete Leftover IDE Directories  # recovered ~10Gb !! == 10% of $HOME

Finalized EOAS annual performance review; emailed to Philippe.

FAL estate work re: BCE & Manulife:
Done:
* Waiver of Probate form
* Declaration of Transmission for BCE
* Declaration of Transmission for Manulife
* Letter of direction for Manulife shares
* Letter of direction for BCE shares
* Letter stating the reason for not probating the will
* copy BCE dividend statement x3
* copy Manulife dividend statement x3
TODO:
* Cover letter
After Jamie returns notarized waiver:
* Make appointment with notary
* Cheque to Insurance broker for 3.5% of BCE shares value
* Cheque to Insurance broker for 3.5% of Manulife shares value
* Cheque to AST for $131.25 ($125 + GST) for BCE shares processing
* Cheque to AST for $131.25 ($125 + GST) for Manulife shares processing
* Notarized signature of Waiver of Probate x2
* 4 notarized copies of death certificate
* 4 notarized copies of will
* Courier pkg to AST

* Send to Jamie for notarized signature:
  * Waiver of Probate form
* Send to Jamie as supporting information:
  * Letter stating the reason for not probating the will - copied
  * Letter of direction for BCE shares - copied
  * Letter of direction for Manulife shares - copied
  * Copy of death certificate - copied
  * Copy of will - copied
  * Copy of BCE dividend statement - copied
  * Copy of Manulife dividend statement

Resumed work on trying to get a working build of nowcast-dev on salish:
* studied OS pkgs (gfortran, gcc, libnetcdf, libnetcdff, openmpi, hdf) and their configs
* tweaked NETCDF_LIB in XIOS arch; build XIOS
* compared `ldd xios_server.exe` between salish & arbutus builds; identical
* tweaked NCDF_LIB NEMO arch; built SalishSeaCast_Blue
* compared `ldd nemo.exe` between salish & arbutus builds; identical
* changed mpirun option from `--bind-to core` to `--bind-to none`
* added mpirun options from arbutus
* started increasing pmem from 2000mb, and got time steps at pmem=15000mb; the torque version in 18.04 is evidently policing memory differently and more strictly than it did in 14.04
* to be continued...

Replied to Raisha's question about lists of forcing files in AtlantisCmd YAML; new feature that I started thinking about after last week's mtg discussion.
(Atlantis)


Wed 22-Sep-2021
^^^^^^^^^^^^^^^

Fixed column 0 issue in 19sep21 random spills .csv file.
Collected next 500 spills into /data/dlatorne/MIDOSS/random-oil-spills/19sep21_near-BP/SalishSea_oil_spills_BP_2nd500.csv.
Uploaded spill .csv file:
  rsync -tlv /data/dlatorne/MIDOSS/random-oil-spills/19sep21_near-BP/SalishSea_oil_spills_BP_2nd500.csv graham:project/dlatorne/MIDOSS/monte-carlo/
Created near-BP_2nd-500.yaml and submitted run:
  mohid monte-carlo --debug near-BP_2nd-500.yaml SalishSea_oil_spills_BP_2nd-500.csv
Reservation is presently 2021-09-29T19:09:22.
(MIDOSS)

Drove Susan to VGH for stitches out.

Reviewed `mpirun mpirun --mca` and `--bind-to` options; for salish I think we want:
  --mca btl ^openib,tcp --mca orte_tmpdir_base /dev/shm --bind-to core
or maybe --bind-to numa
Experimented via `salishsea run --no-submit` in /SalishSeaCast/runs/ using 23apr21nowcast-dev.yaml and setup via:
  make_forcing_links salish --shared-storage 2021-04-23
Changed `#PBS -l pmem=2000mb` to `#PBS -l mem=128gb`.
Test with:
  #PBS -l mem=128gb
  --mca btl ^openib,tcp --mca orte_tmpdir_base /dev/shm --bind-to core
  * nemos at ~6gb
  * xios at ~15.5gb; never went above 16gb on top
  * run didn't finish properly due to no ~/.local/bin/salishsea
  * 3h11m
Test with:
  #PBS -l mem=64gb
  mpirun --mca btl ^openib,tcp --mca orte_tmpdir_base /dev/shm --bind-to numa
  * nemos at ~6gb
  * xios at ~15.5gb
  * run finished properly
  * 3h27m
  * --bind-to core is better than numa
(SalishSeaCast)


Thu 23-Sep-2021
^^^^^^^^^^^^^^^

Ran make_plots nemo nowcast comparison 2021-04-23 to confirm that nowcast-dev run produces processable results.
Added logging config to limit PIL.PngImagePlugin to warning level.
Continued nowcast-dev tests:
* checked run time for nowcast-dev/22apr21 for comparison to present tests: 3h22m
* Test 24apr21 with:
    #PBS -l mem=64gb
    mpirun --mca btl ^openib,tcp --bind-to core
  * much chaos getting restart and namelist.time edited correctly
  * run finished properly
  * 3h12m
  * --mca orte_tmpdir_base /dev/shm has minimal effect
(SalishSeaCast)

Created near-BP_2nd-500.yaml and submitted run:
  mohid monte-carlo --debug near-BP_2nd-500.yaml SalishSea_oil_spills_BP_2nd-500.csv
(MIDOSS)

Kickr Bike trainers delivered.

Weekly project mtg.
(Atlantis)


Fri 24-Sep-2021
^^^^^^^^^^^^^^^

Created near-BP.yaml and submitted next 100 spills run:
  mohid monte-carlo --debug near-BP.yaml SalishSea_oil_spills_BP_4th-100.csv
(MIDOSS)

Changed PIL logging level from DEBUG to WARNING to uninformative silence PIL.PngImagePlugin messages.
nowcast-blue stopped reporting after 09:13:55:
* web dashboard shows that nowcast0 and nowcast6 stopped again for no reason at 16:14 UTC == 09:14
* recovery:
  * restarted nowcast0 and nowcast6 from web dashboard at 20:14 UTC == 13:14 Pacific
    * nowcast0:
        sudo apt update
        sudo apt upgrade
        sudo shutdown -r now
        sudo mount /dev/vdc /nemoShare
        ll /nemoShare/MEOPAR/  # to confirm mount
        sudo mount --bind /nemoShare/MEOPAR /export/MEOPAR
        ll /export/MEOPAR  # to confirm mount
        sudo systemctl start nfs-kernel-server.service
        sudo exportfs -f  # to reset NFS handles for compute nodes
    * nowcast6:
        sudo mount -t nfs -o proto=tcp,port=2049 192.168.238.14:/MEOPAR /nemoShare/MEOPAR
    * nowcast0:
      # confirm compute nodes have /nemoShare/MEOPAR/ mounted:
      for n in {1..9}; do   echo nowcast${n};   ssh nowcast${n} "mountpoint /nemoShare/MEOPAR"; done
      for n in {1..9}; do   echo nowcast${n};   ssh nowcast${n} "ls -C /nemoShare/MEOPAR"; done
      for n in {0..6}; do   echo fvcom${n};   ssh fvcom${n} "mountpoint /nemoShare/MEOPAR"; done
      for n in {0..6}; do   echo fvcom${n};   ssh fvcom${n} "ls -C /nemoShare/MEOPAR"; done
  * replaced nowcast6 with nowcast2 in mpi_hosts because it appears that nowcast0 and nowcast6 are on the same hypervisor (maybe hardware)
  * on skookum:
      # killed stalled processes
      # restarted log_aggregator
      make_forcing_links arbutus nowcast+
(SalishSeaCast)

Merit review mtg w/ Philippe.


Sat 25-Sep-2021
^^^^^^^^^^^^^^^

Continued nowcast-dev tests:
Test with:
  #PBS -l mem=64gb
  mpirun --mca orte_tmpdir_base /dev/shm --bind-to core
  * eta 15:40
  * run finished properly
  * 3h12m
  * --mca btl ^openib,tcp has no effect
Test with:
  #PBS -l mem=64gb
  mpirun --bind-to none
  * eta 19:15
  * run finished properly
  * 3h10m
  * --bind-to none is marginally better than core
(SalishSeaCast)

100 spills job ran overnight.
Prepared and submitted 12 more 100 spill jobs:
  for grp in {5..16}; do head -1 SalishSea_oil_spills-fixed-col0.csv > SalishSea_oil_spills_BP_${grp}th-100.csv; done
  starts=(9 10 11 12 13 14 15 16 17 18 19 20); grps=(5 6 7 8 9 10 11 12 13 14 15 16); for i in "${!grps[@]}"; do head -${starts[$i]}31 SalishSea_oil_spills-fixed-col0.csv | tail -100 >>SalishSea_oil_spills_BP_${grps[$i]}th-100.csv; done
  for grp in {5..16}; do sed -i "s/near-BP_.*th-100/near-BP_${grp}th-100/" near-BP.yaml && mohid monte-carlo --debug near-BP.yaml SalishSea_oil_spills_BP_${grp}th-100.csv; done
(MIDOSS)


Sun 26-Sep-2021
^^^^^^^^^^^^^^^

Added CodeQL analysis GHA workflow to SalishSeaNowcast.
(SalishSeaCast)

Discussed w/ Susan running Monte Carlo on cedar to get better priority.
(MIDOSS)


Week 39
-------

Mon 27-Sep-2021
^^^^^^^^^^^^^^^

Week 81 of UBC work-from-home due to COVID-19

5 x 100 spills running on graham.
(MIDOSS)

Teams mtg w/ Derek White at Port of Vancouver:
* ECHO program to protect SRKWs (southern resident killer whales)
* collab w/ BC pilots
* model to correct speed over ground to speed through water based on webtide; poor agreement; want to use SalishSeaCast
(Prediction Core)

Group mtg; see whiteboard.
(MOAD)

Added GHA CodeQL analysis workflow to SalishSeaCmd repo.
Tracked down `DeprecationWarning: EntryPoint tuple interface is deprecated. Access members by name.` in SalishSeaCmd tests to a change introduced in importlib=4.8.1 that stevedore=3.4.0 doesn't handle.
Updated SalishSeaCmd to use mem=64gb and --bind-to none on salish re: Ubuntu 18.04.
Ran nowcast-dev/27apr21 via updated SalishSeaCmd
Updated SalishSeaNowcast re: SalishSeaCmd changes.
Created nowcast-dev/27sep21/ directory containing namelist_cfg and restart.nc from nowcast-blue/27sep21/ so that nowcast-dev should run in automation tomorrow.
(SalishSeaCast)

FAL estate work re: BCE & Manulife:
* sent AST waiver form to Jamie for notarized signature

Reviewed and signed merit review from from Philippe.


Tue 28-Sep-2021
^^^^^^^^^^^^^^^

Copied Raisha's 2007-2021 hydro, salt & temp forcing file to ~/public_html/Atlantis/, gzip compressed them, and sent email to Javier that they are available for him ot download.
(Atlantis)

Tried to start setting up for Monte Carlo runs on cedar but got blocked by cedar auth failure; email to support got response from Venkat! :-)  resolved at 12:40.
(MIDOSS)

nowcast-dev ran via automation using restart from nowcast-blue.201905/27sep21/ :-)
(SalishSeaCast)


Wed 29-Sep-2021
^^^^^^^^^^^^^^^

near-BP_10th-100 started
Accidentally deleted part of $SCRATCH/MIDOSS/runs/monte-carlo/near-BP_1st-30_2021-09-20T144849/results/
Started set up to run Monte Carlo on cdear:
* created /home/dlatorne/project/dlatorne/MIDOSS/monte-carlo/
* confirmed that $PROJECT/SalishSea/forcing/SalishSea/hindcast.201905/ contains expected 4*365+1=1461 (because 2016 was a leap year) dirs for 2015-2018
    `find $PROJECT/SalishSea/forcing/SalishSea/hindcast.201905/ -type d -name *1[5-8] | wc -l`
  but at least some ownership is vdo, and some dirs are not group readable
    find $PROJECT/SalishSea/forcing/SalishSea/hindcast.201905/ -type f -wholename *1[5-8]/SalishSea_1h*grid_T.nc | wc -l
* found that there are only ~246 `grid_*.nc` files in that tree though; e.g.
    `find $PROJECT/SalishSea/forcing/SalishSea/hindcast.201905/ -type f -wholename *1[5-8]/SalishSea_1h*grid_T.nc | wc -l`
  shows 246 files; decided to create new $PROJECT/MIDOSS/forcing/nowcast-green.201905/ to match graham
    `cd /results2/SalishSea/nowcast-green.201905/`
    `rsync -rltv --include=*1[5-8] --include=SalishSea_1h_*grid_*.nc --include=SalishSea_1h_*carp_T.nc --exclude=* *1[5-8] cedar:project/MIDOSS/forcing/nowcast-green.201905/`
* confirmed that $PROJECT/SalishSea/forcing/atmospheric/GEM2.5/operational/ contains expected 1461 ops_y201[5-8]*.nc files and ownership/permissions are good
    `find $PROJECT/SalishSea/forcing/atmospheric/GEM2.5/operational/ -maxdepth 1  -type f -name "ops_y201[5-8]*.nc" | wc -l`
* it appears that the only complete 2015-2018 collection of wwatch3 fields we have is in graham:$PROJECT/MIDOSS/forcing/wwatch3/
* created $PROJECT/MIDOSS/forcing/wwatch3/ and rsync-ed files from graham
    `rsync -rltv --include=*1[5-8] --include=SoG_ww3_fields_*.nc --exclude=* $PROJECT/MIDOSS/forcing/wwatch3/ cedar:project/MIDOSS/forcing/wwatch3/`
* wwatch3 rsync hit disk quota exceeded; cleaned out lots of hg repo clones, but it wasn't enough
Worked on Rachael's problem w/ xarray.open_dataset() in new vnev on graham; turns out that netCDF4 wheel in Compute Canada wheelhouse is incompatible w/ xarray=0.19.0; maybe due to openmpi in stdenv?; got a working env by swapping h5netcdf for netCDF4.
(MIDOSS)


Thu 30-Sep-2021
^^^^^^^^^^^^^^^

*Statutory Holiday** - Reconcilliation Day

Prepared and submitted 10 more 100 spill jobs on graham:
  for grp in {17..26}; do head -1 SalishSea_oil_spills-fixed-col0.csv > SalishSea_oil_spills_BP_${grp}th-100.csv; done
  starts=(21 22 23 24 25 26 27 28 29 30); grps=(17 18 19 20 21 22 23 24 25 26); for i in "${!grps[@]}"; do head -${starts[$i]}31 SalishSea_oil_spills-fixed-col0.csv | tail -100 >>SalishSea_oil_spills_BP_${grps[$i]}th-100.csv; done
  for grp in {17..26}; do sed -i "s/near-BP_.*th-100/near-BP_${grp}th-100/" near-BP.yaml && mohid monte-carlo --debug near-BP.yaml SalishSea_oil_spills_BP_${grp}th-100.csv; done
Susan came up with:
  ls -ltrd $SCRATCH/MIDOSS/runs/monte-carlo/*/near-BP_*
to find spill runs that don't complete due to GLOST job timeout; presently yields 4 spills:
  drwxr-s--- 3 dlatorne def-allen 41472 Sep 25 05:38 /scratch/dlatorne/MIDOSS/runs/monte-carlo/near-BP_4th-100_2021-09-24T125848/near-BP_4th-100-94/
  drwxr-s--- 3 dlatorne def-allen 41472 Sep 25 05:58 /scratch/dlatorne/MIDOSS/runs/monte-carlo/near-BP_4th-100_2021-09-24T125848/near-BP_4th-100-96/
  drwxr-s--- 3 dlatorne def-allen 41472 Sep 25 06:20 /scratch/dlatorne/MIDOSS/runs/monte-carlo/near-BP_4th-100_2021-09-24T125848/near-BP_4th-100-99/
  drwxr-s--- 3 dlatorne def-allen 41472 Sep 25 11:18 /scratch/dlatorne/MIDOSS/runs/monte-carlo/near-BP_4th-100_2021-09-24T125848/near-BP_4th-100-92/
  d
Evaluated extent of accidentally deleted result files in xxx:
  * spills: 0 3 4 9 11 16 23 24 27 29
Continued set up to run Monte Carlo on cedar:
* Checked storage on graham:
  * du -sh $PROJECT/MIDOSS/forcing/wwatch3/: 331G
  * du -sh $PROJECT/MIDOSS/forcing/nowcast-green.201905/: 3.8T
  * du -sh $PROJECT/SalishSea/forcing/atmospheric/GEM2.5/operational/: 57G
  So, not enough storage on cedar:$PROJECT for wwatch3 and nowcast-green; will have to use $SCRATCH and plan to restore files deleted by 60d purge policy monthly after 15-Dec (if necessary).
* removed $PROJECT/MIDOSS/forcing/wwatch3/
* created $SCRATCH/MIDOSS/forcing/monte-carlo/wwatch3/ and rsync-ed files from graham in tmux sesion:
    `rsync -rltv --include=*1[5-8] --include=SoG_ww3_fields_*.nc --exclude=* $PROJECT/MIDOSS/forcing/wwatch3/ cedar:/scratch/dlatorne/MIDOSS/forcing/monte-carlo/wwatch3/`
* created $SCRATCH/MIDOSS/forcing/monte-carlo/nowcast-green.201905/ and rsync-ed files from skookum in tmux sesion:
    `rsync -rltv --include=*1[5-8] --include=SalishSea_1h_*grid_*.nc --include=SalishSea_1h_*carp_T.nc --exclude=* /results2/SalishSea/nowcast-green.201905/ cedar:/scratch/dlatorne/MIDOSS/forcing/monte-carlo/nowcast-green.201905/`
(MIDOSS)


October
=======

Fri 1-Oct-2021
^^^^^^^^^^^^^^

Prepared and submitted 10 more 100 spill jobs on graham:
  for grp in {27..36}; do head -1 SalishSea_oil_spills-fixed-col0.csv > SalishSea_oil_spills_BP_${grp}th-100.csv; done
  starts=(31 32 33 34 35 36 37 38 39 40); grps=(27 28 29 30 31 32 33 34 35 36); for i in "${!grps[@]}"; do head -${starts[$i]}31 SalishSea_oil_spills-fixed-col0.csv | tail -100 >>SalishSea_oil_spills_BP_${grps[$i]}th-100.csv; done
  for grp in {27..36}; do sed -i "s/near-BP_.*th-100/near-BP_${grp}th-100/" near-BP.yaml && mohid monte-carlo --debug near-BP.yaml SalishSea_oil_spills_BP_${grp}th-100.csv; done
Confirmed completion of rsyncs of forcing to $SCRATCH on cedar; agreed w/ Susan to put cedar deployment on hold because runs are progressing well on graham (4-6 x 100 spills at a time now).
(MIDOSS)


Sat 2-Oct-2021
^^^^^^^^^^^^^^

Prepared and submitted 10 more 100 spill jobs on graham:
  for grp in {37..46}; do head -1 SalishSea_oil_spills-fixed-col0.csv > SalishSea_oil_spills_BP_${grp}th-100.csv; done
  starts=( $(seq 41 50) ); grps=( $(seq 37 46) ); for i in "${!grps[@]}"; do head -${starts[$i]}31 SalishSea_oil_spills-fixed-col0.csv | tail -100 >>SalishSea_oil_spills_BP_${grps[$i]}th-100.csv; done
  for grp in {37..46}; do sed -i "s/near-BP_.*th-100/near-BP_${grp}th-100/" near-BP.yaml && mohid monte-carlo --debug near-BP.yaml SalishSea_oil_spills_BP_${grp}th-100.csv; done
Replaced near-BP_2nd-500 job with 5x100 jobs:
  for grp in {2000..2004}; do head -1 SalishSea_oil_spills-fixed-col0.csv > SalishSea_oil_spills_BP_${grp}th-100.csv; done
  starts=( $(seq 1 5) ); grps=( $(seq 2000 2004) ); for i in "${!grps[@]}"; do head -${starts[$i]}31 SalishSea_oil_spills-fixed-col0.csv | tail -100 >>SalishSea_oil_spills_BP_${grps[$i]}th-100.csv; done
  for grp in {2000..2004}; do sed -i "s/near-BP_.*th-100/near-BP_${grp}th-100/" near-BP.yaml && mohid monte-carlo --debug near-BP.yaml SalishSea_oil_spills_BP_${grp}th-100.csv; done
(MIDOSS)

Took old skis, lawn chairs, vacuum cleaner, etc. and Wahoo Bikes card board to recycling centre.

Drove to White Rock to visit J&M.


Sun 3-Oct-2021
^^^^^^^^^^^^^^

Prepared and submitted 20 more 100 spill jobs on graham:
  for grp in {47..66}; do head -1 SalishSea_oil_spills-fixed-col0.csv > SalishSea_oil_spills_BP_${grp}th-100.csv; done
  starts=( $(seq 51 70) ); grps=( $(seq 47 66) ); for i in "${!grps[@]}"; do head -${starts[$i]}31 SalishSea_oil_spills-fixed-col0.csv | tail -100 >>SalishSea_oil_spills_BP_${grps[$i]}th-100.csv; done
  for grp in {47..66}; do sed -i "s/near-BP_.*th-100/near-BP_${grp}th-100/" near-BP.yaml && mohid monte-carlo --debug near-BP.yaml SalishSea_oil_spills_BP_${grp}th-100.csv; done
(MIDOSS)

Cycled River Rd Out & Back route really strongly; new 40 km PR (48 km)


Week 40
-------

Mon 4-Oct-2021
^^^^^^^^^^^^^^

Week 82 of UBC work-from-home due to COVID-19

Resumed work on getting phpgedview set up on OpalStack; see webfaction-opalstack-migration.md

Python 3.10 release party on Youtube:
* live release process w/ feature talks interspersed
* CI runs on buildbot

Group mtg; see whiteboard.
(MOAD)

Phys Ocgy seminar: Patrick Pata on BC coastal zooplanton provinces


Tue 5-Oct-2021
^^^^^^^^^^^^^^

Work at UBC while Rita is at home.

`download_results forecast2`, `update_forecast_datasets wwatch3 forecast2`, and subsequent workers failed due to /results full; recovery started at 11:15:
* delete /results/SalishSea/forecast2.201905/ 16feb20/ through 31mar21/ that Susan has archived; freed 1.1T
* update_forecast_datasets wwatch3 forecast2
* download_results forecast2 --run-date-2021-10-04
* rm -rf /results/forcing/atmospheric/GEM2.5/GRIB/20211005/12
* pkill -f collect_weather 12 2.5km
* collect_weather 18 2.5km &
* download_weather 12 2.5km
* delete /results/SalishSea/nowcast-agrif.201702/ 01apr21/ through 30sep21/ that Susan has archived; freed 0.4T more for total of 1.5T
Updated Trello Results Archive board w/ forecast2.201905 deletions and disk use details.
Started building tarballs of GEMLAM files for archival storage on graham:/nearline/ so that we can free space on /opp/ (which is down to 1.4T free, and GEMLAM/ is using 11T):
  tar -cvvf /opp/GEMLAM/2007.tar /opp/GEMLAM/2007/ | tee GEMLAM_2007.index
Reviewed plans for splitting tools repo from 2-Feb-2021, and experiment with git-filter-repo tool on Marlin package from 15-Mar-2021.
(SalishSeaCast)

Reviewed our Python packaging docs and setuptools docs re: evolution:
* entry points can now be included in setup.cfg, but need to experiment to see if cliff-style entry point declarations are supported, for if it is just console_scripts
* minimal setup.py is still required for pip install -e to work; need to experiment to see if presence of pyproject.toml is still incompatible with editable installs
(MOAD)


Wed 6-Oct-2021
^^^^^^^^^^^^^^

SHARCNET META webinar:
* Sergey Mashchenko, McMaster
* alternative to:
  * bash loop: heavy scheduler load
  * SLURM job array: less typing, but same heavy scheduler load
  * GLOST: reduced scheduler load, but big queue wait time
* optimum solution to above: a few "meta-jobs", low scheduler load, reasonable queue wait time
* applications include Monte Carlo: "serial farming of workloads"
* dynamic workload balancing across meta-jobs
* more flexible than GLOST
* uses serialized queue based on OS lockfile command for sync instead of MPI in GLOST
* convenient re-submit feature: re-submit just failed workloads
* meta-jobs analyze runtimes of individual workloads to improve efficiency; probablistic estimator based on 12.5% quantile after 8 workloads completed
* 2 modes:
  * META mode
  * simple for 1 job per code exec; to get re-submit feature
* can be used for any kind of workload: serial, multi-thread, MPI, GPU
* sub-commands:
  * submit.run
  * resubmit.run
  * list.run
  * query.run
  * kill.run
  * prune.run
  * status.run
  * clean.run
* META commands executed inside farm directories
* install from https://git.sharcnet.ca/syam/META
* docs: https://docs.computecanada.ca/wiki/META_package_for_serial_farming
* appears to be written in bash!!!
* single_case.sh controls execution; length of table.dat controls number of workloads to execute

Confirmed that Python 3.10.0 is available from conda-forge.

Built new salishsea-nowcat env on kudu to get upgrade from pillow=8.2.0 to pillow=8.3.2 re: dependabot PR#80; squash-merged PR, and updated requirements.txt.
rsync of GEMLAM/2007 tarball and index in tmux session on salish failed due to broken pipe; re-tried.
(SalishSeaCast)

Resumed work on getting XIOS & NEMO to work under StdEnv/2020 on graham (ref 23-Mar-2021):
* updated repos
* did clean build of XIOS-2, SalishSeaCast NEMO config, REBUILD_NEMO
* test-9 failed w/ errors in ocean.output
(NEMO)

Experimented w/ pyproject.toml, no setup.py, and python3 -m pip install -e . in SalishSeaNowcast pkg, and it appears to work!
Updated SalishSeaNowcast to drop setup.py and add pyproject.toml; also added check-toml to pre-commit hooks.
(MOAD)


Thu 7-Oct-2021
^^^^^^^^^^^^^^

Prepared and submitted 20 more 100 spill jobs on graham:
  for grp in {67..86}; do head -1 SalishSea_oil_spills-fixed-col0.csv > SalishSea_oil_spills_BP_${grp}th-100.csv; done
  starts=( $(seq 71 90) ); grps=( $(seq 67 86) ); for i in "${!grps[@]}"; do head -${starts[$i]}31 SalishSea_oil_spills-fixed-col0.csv | tail -100 >>SalishSea_oil_spills_BP_${grps[$i]}th-100.csv; done
  for grp in {67..86}; do sed -i "s/near-BP_.*th-100/near-BP_${grp}th-100/" near-BP.yaml && mohid monte-carlo --debug near-BP.yaml SalishSea_oil_spills_BP_${grp}th-100.csv; done
(MIDOSS)

rsync of GEMLAM/2007 tarball and index in tmux session on salish failed again due to broken pipe; successfully rsync-ed index alone to confirm opeations; re-tried tarball again, this time with --progress and --partial.
(SalishSeaCast)

Coffee and debugging OceanParcels for Atlantis w/ Raisha.

Helped Raisha debug reading HRDPS winds into OceanParcels.
Emailed Javier re: forcing fields xfer; send file lengths & sha1 checksums to try to confirm xfer integrity.
(Atlantis)

EOAS symposium: data science - right answers for the right reasons?


Fri 8-Oct-2021
^^^^^^^^^^^^^^

Helped Becca w/ her re-tiding of day average fields workflow re: vectorization and dask.
(MOAD)

Drove to Squamish.


Sat 9-Oct-2021
^^^^^^^^^^^^^^

Squamish

forecast2 and nowcast did not start due to missing 08sep21 Neah ay ssh file; recovery:
* Susan discovered that obs are missing since 04:00 08oct10 so building sshNeahBay/obs/ssh_y2021m10d08.nc is hard
* symlinked fcst/ssh_y2021m10d08.nc as obs/ssh_y2021m10d08.nc
    upload_forcing arbutus forecast2
    upload_forcing orcinus forecast2
    upload_forcing graham forecast2
    upload_forcing optimum forecast2
    wait for runs to finish
    upload_forcing arbutus nowcast+
    upload_forcing orcinus nowcast+
    upload_forcing graham nowcast+
    upload_forcing optimum nowcast+
rsync of GEMLAM/2007 tarball and index in tmux session on salish failed again due to broken pipe; changed to rsync 2007/ to $SCRATCH with --partial-dir option for better restart performance.
(SalishSeaCast)

Walked a loop on trails from Coho Park trailhead.

Created douglatornell/cliff-structlog-expt pkg to explore several things:
* Using VSCode from scratch for Python dev
  * initialized git repo in code and published it to personal GitHub account
* using envs/requirements.txt instead of top level of repo
  * GitHub's dependency tool found it!
* using pyproject.toml in conjunction with pip install -e
* using setup.cfg to define cliff plugin sub-command entry points


Sun 10-Oct-2021
^^^^^^^^^^^^^^^

Squamish

Cycled Squamish River Rd to ~10km beyond end of pavement (~2km beyond High Falls Rec Area - out lunch stop) (71 km)


Week 41
-------

Mon 11-Oct-2021
^^^^^^^^^^^^^^^

Week 83 of UBC work-from-home due to COVID-19

**Statutory Holiday** - Thanksgiving

Walked on Stawamus River dyke trail.

Drove from Squamish to Vancouver; tire inflation sensor system signalled that it is malfunctioning part way through drive.

Grace called to tell of Elinor's passing earlier in the day.

Prepared and submitted 20 more 100 spill jobs on graham:
  for grp in {87..93}; do head -1 SalishSea_oil_spills-fixed-col0.csv > SalishSea_oil_spills_BP_${grp}th-100.csv; done
  starts=( $(seq 91 97) ); grps=( $(seq 87 93) ); for i in "${!grps[@]}"; do head -${starts[$i]}31 SalishSea_oil_spills-fixed-col0.csv | tail -100 >>SalishSea_oil_spills_BP_${grps[$i]}th-100.csv; done
  for grp in {87..93}; do sed -i "s/near-BP_.*th-100/near-BP_${grp}th-100/" near-BP.yaml && mohid monte-carlo --debug near-BP.yaml SalishSea_oil_spills_BP_${grp}th-100.csv; done
Spills from .csv line 9732 onward need to be run in a wrap-up run.
(MIDOSS)


Tue 12-Oct-2021
^^^^^^^^^^^^^^^

download_live_ocean slow today; timed out at 12:07; re-tried at 12:36; timed out again at 15:47; email from Parker says that delay is due to server maintenance, file should be ready by 17:30; restarted worker at ~15:41
rsync of GEMLAM/2007/ directory in tmux session on salish failed again on Saturday after ~3h due to broken pipe with 3613 of 9089 files transferred; restarted at ~10:25; broken pipe again after another 3016 files transferred; restarted at ~15:40
(SalishSeaCast)

Continued work on douglatornell/cliff-structlog-expt pkg:
* found bug that was preventing cliff plugin sub-command registration
* confirmed that registration via setup.cfg (no setup.py) works; requires setuptools>=51.0.0
* pip==20.0.2 on graham prevents editable install with pyproject.toml file in repo :-( (but acts like --user install pattern has been disabled)

Installed mamba in conda base env on kudu:
  conda install -n base -c conda-forge mamba
Still need to use conda to activate/deactivate envs; mamba seems to work for all else, and added repoquery sub-command.


Wed 13-Oct-2021
^^^^^^^^^^^^^^^

Yesterday's r12 still had ~1h40m to run when today's nowcast-blue started; checked mpi_hosts files: overlap of fvcom0 VM for r12 and x2 will not end well..
* x2 running, but says it will take >35h
* r12 stalled at 1h21m and slowly rising
* killed x2, re-launch after r12 finishes:
    pkill -f "x2 nowcast"  # on arbutus nowcast0
    top -c  # kill x2 on fvcom0
    wait for r12 to finish
    launch_remote_worker arbutus make_fvcom_boundary "arbutus x2 nowcast 2021-10-13"
rsync of GEMLAM/2007/ directory in tmux session on salish failed again yesterday after ~2h due to broken pipe after another 1216 files transferred; restarted at ~11:00; finally succeeded!!
Created /nearline tarball on graham:
    cd /scratch/dlatorne/
    tar -cvvf /nearline/rrg-allen/SalishSea/GEMLAM/GEMLAM_2007.tar MEOPAR/GEMLAM/2007/ | tee /nearline/rrg-allen/SalishSea/GEMLAM/GEMLAM_2007.index
tarball creation ended, but only ~75% of expected size
Started rsync of 2008/ from salish to graham $SCRATCH:
    time rsync -rtlv --partial-dir=/scratch/dlatorne/MEOPAR/GEMLAM/rsync-partial --progress /opp/GEMLAM/2008 graham:/scratch/dlatorne/MEOPAR/GEMLAM/
(SalishSeaCast)

Re-ran 1st-30 spills to recover accidentally deleted results for spills 0 3 4 9 11 16 23 24 27 29; run timed out; re-submitted w/ 4h walltime
Set up final 103 spills in .csv as 94th-103; run completed.
(MIDOSS)

Resumed work on getting XIOS & NEMO to work under StdEnv/2020 on graham (ref 23-Mar-2021 and 6-Oct-2021):
  module load netcdf-fortran-mpi/4.5.2
  module load perl/5.30.2
  module load python/3.9.6
  git pull SS-run-sets
  cp SS-run-sets/v202007/newbathy called 02jan17_graham_short.yaml
  salishsea run 02jan17_graham_short.yaml $SCRATCH/MEOPAR/results/02jan17_short-test-1 --no-submit
time stepping!!!
But run timed out :-(
(NEMO)

Rachael visited to pick up the stuff she had left here when COVID started.


Thu 14-Oct-2021
^^^^^^^^^^^^^^^

Cleaned up aborted 1st-30 and 94th-103 directories.
Did file counts for Lagrangian*.nc; numbers don't tally: >10_000 total, but <100 in multiple run directories; sep
(MIDOSS)

Re-tried 2007 /nearline tarball on graham:
    cd /scratch/dlatorne/
    tar -cvvf /nearline/rrg-allen/SalishSea/GEMLAM/GEMLAM_2007.tar MEOPAR/GEMLAM/2007/ | tee /nearline/rrg-allen/SalishSea/GEMLAM/GEMLAM_2007.index
rsync of GEMLAM/2008/ directory in tmux session on salish failed again yesterday after ~2h40m due to broken pipe after 2670 files transferred; restarted at ~10:10 
(SalishSeaCast)

Investigated 02jan17_short-test-1 timeout on graham:
* core dumped
* completed 8934 of 10800 time steps
* found ORTE error in stderr
Re-ran as 02jan17_short-test-2; was on track to timeout; Susan noted decomp that resulted in only 4 nodes used; her test timed out too.
Re-ran w/ 16x34 decomp; finished in 1hr :-)
* salishsea combine step failed; investigation:
  * error from rebuild_nemo:
       ERROR! : NetCDF: Invalid argument
       *** NEMO rebuild failed ***
        
       9
(NEMO)

Tried to build Python 3.10 dev env using mamba; failed due to docutils.
Moved requirements.txt to envs/ because GitHub dependency analysis tools can find it there now.
Updated readthedocs config to new API:
* renamed readthedocs.yml to .readthedocs.yaml because that's the only supported name now
* changed build spec to use ubunu-20.04 container and mambaforge-4.10 build tool
Reviewed tests for use of config(base_config) fixure; updates needed in:
* test_next_workers - done
* test_run_NEMO - done
* test_run_NEMO_agrif
* test_split_results
* test_watch_NEMO
* test_watch_NEMO_agrif
* test_watch_ww3
* worked on update-test-config-fixture branch
(SalishSeaNowcast)


Fri 15-Oct-2021
^^^^^^^^^^^^^^^

Power failed at 08:15 due to tree down across wires somewhere nearby; back on at about 10:15

collect_weather 06 stalled; investigation:
* sarracenia queue permission problem:
    2021-10-14 23:09:33,040 [WARNING] sr_amqp/consume: could not consume in queue q_anonymous.sr_subscribe.hrdps-west.74434425.78671301: [Errno 110] Connection timed out
    2021-10-14 23:09:33,040 [ERROR] sr_amqp/close 2: [Errno 32] Broken pipe
    2021-10-14 23:09:33,040 [INFO] Using amqp module (AMQP 0-9-1)
    2021-10-14 23:09:36,913 [INFO] declared queue q_anonymous.sr_subscribe.hrdps-west.74434425.78671301 (anonymous@dd.weather.gc.ca) 
    2021-10-14 23:09:46,800 [ERROR] bind queue: q_anonymous.sr_subscribe.hrdps-west.74434425.78671301 to exchange: xpublic with key: v02.post.model_hrdps.west.grib2.# failed with [Errno 110] Connection timed out
    2021-10-14 23:09:46,800 [ERROR] Permission issue with anonymous@dd.weather.gc.ca or exchange xpublic not found.
  error repeats every 64 seconds
* 0 files downloaded
* recovery:
    pkill -f collect_weather
    rm -rf /results/forcing/atmospheric/GEM2.5/GRIB/20211015/06
    # clean up datamart mirror dirs
    for d in 00 06 12 18; do rm -rf /SalishSeaCast/datamart/hrdps-west/${d}/*; done
    collect_weather 18 2.5km
    download_weather 06 2.5km
    wait for forecast2 runs to finish
    download_weather 12 2.5km
Restarted sr_subscribe-hrdps-west via supervisorctl; queue subscription was successful.
Checked sr_subscribe-hrdps-west-1km; no problems.
Checked sr_subscribe-hydrometric; also stared failing w/ permission issued last night; restarted via supervisorctl; queue subscription was successful.
(SalishSeaCast)

Continued updating tests to use config(base_config) fixure:
* test_next_workers - done
* test_run_NEMO - done
* test_run_NEMO_agrif - done
* test_split_results - done
* test_watch_NEMO - done
* test_watch_NEMO_agrif - done
* test_watch_ww3 - trivial test suite; no config :-(
* worked on update-test-config-fixture branch; rebased and merged work with the PyCharm equivalent of:
  git switch update-test-config-fixture
  git rebase main
  git switch main
  git merge update-test-config-fixture
(SalishSeaNowcast)

Re-organized garage storage to be able to park Prius farther back and reach recycling containers more easily.

Started reading rebuild_nemo.f90 code to debug error on graham, or replace it with Python.
(NEMO)


Sat 16-Oct-2021
^^^^^^^^^^^^^^^

Minecraft Live.

LiveOcean delayed almost 3h. 
(SalishSeaCast)

Drove to White Rock and cooked Thanksgiving chicken dinner for J&M.


Sun 17-Oct-2021
^^^^^^^^^^^^^^^

Created issue #81 re: updating NowcastWorker mocks in tests, and issue #82 re: updating logging mocks in tests; decided that issues were a better place to keep list of modules and progress than here.
(SalishSeaNowcast)







TODO:
* Python packaging docs and pkg cookiecutters updates:
  * change to nodefaults in conda channels list
  * move requirements.txt to envs/
  * add .gitignore ???
  * add .pre-commit-config.yaml; include pre-commit in environment-dev.yaml
  * rename readthedocs.yml to .readthedocs.yaml
  * update .readthedocs.yaml to new build API (see SalishSeaNowcast)
  * add pyproject.toml ???
  * remove setup.py ???
  * add docs re: entry points in setup.cfg; requires setuptools>=51.0.0
  * figure out if graham versions of pip, setuptools, wheel support pyproject.toml, setup.cfg, and pip install -e
    * graham python/3.9.6 has:
        pip            20.0.2 
        setuptools     56.2.0 
        wheel          0.36.2 
    * graham python/3.8.2 has:
        pip            20.0.2 
        setuptools     45.2.0       
        wheel          0.34.2       
    * pip 20.0.2 doesn't support editable install with pyproject.toml :-(  that feature seems to have appeared in 21.2.4, but it is not official in the changelog until 21.3



TODO:
* re-run spills:
  * 4th-100: 92 94 96 99

* figure out how to merge/cherrypick relevant changes from Rachael's add_terminal branch in moad_tools

Fix ariane docs:
* maybe re:  adding a bin-like directory to prefix gets rid of errors from doc/ and examples/ that confused Becca ???



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
