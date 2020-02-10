*****************
2020 Work Journal
*****************

This is my public work journal.
It is patterned after one that I have kept for several years for my work at Nordion_.
This journal is about:

* my work as a Research Software Engineer with `Dr. Susan Allen`_ in the `Department of Earth, Ocean and Atmospheric Sciences`_ at the `University of British Columbia`_
* my freelance work via my consulting business,
  `43ravens`_
* my `open-source activities`_


January
=======

Week 1
------

Wed 1-Jan-2018
^^^^^^^^^^^^^^

**Statutory Holiday** - New Year's Day

Helped Allens settle in at Amica White Rock.


Thu 2-Jan-2018
^^^^^^^^^^^^^^

Helped Allens settle in at Amica White Rock.


Fri 3-Jan-2018
^^^^^^^^^^^^^^

Finished initialization of 2020 GnuCash SADA books.

Enabled guest network and SmartSteering (2.4G/5G) on Telus router to phase out airport express.
Added port forwarding for lizzy and kudu.
Added ssh key to ConnectBot on phone.

Set up 43ravens organization under my personal account on GitHub, and moved imported NEMO_Nowcast repo to it.

Imported this repo to GitHub.
Imported dotfiles repo to GitHub. Added githooks/generic/ pre-commit.sh and rescuetime commit highlight post-commit hooks; there is no post-tag hook in git.


Sat 4-Jan-2018
^^^^^^^^^^^^^^

Set local git repo email with: git config user.email "name@example.com"
Set kudu git config to always pull --rebase; git config --global pull.rebase true; see:
* https://coderwall.com/p/tnoiug/rebase-by-default-when-doing-git-pull
* https://mislav.uniqpath.com/2013/02/merge-vs-rebase/

See work journal.
(Ocean Navigator)

Changed NEMO_Nowcast readthedocs webhook to GitHub.
Updated NEMO_Nowcast copyright year range and bumped version to 20.1.dev0
Set up CI workflow for NEMO_Nowcast via GitHub Actions.
Changed to launch clear_checklist after wwatch3 forecast2 pings ERDDAP instead of after NEMO forecast2 make_feeds to avoid wwatch3 post-processing workers not being able to find what they need in the checklist.
(SalishSeaCast)

Started writing https://docs.google.com/document/d/1Gex3JdO8GpMdp0vxCPR05KOw5YFyg7mRV35j5gGJ8V8/edit?folder=0AMzQNtq8h6DpUk9PVA re: MOAD version control migration.
(MOAD)


Sun 5-Jan-2018
^^^^^^^^^^^^^^

Experimented with `git config --global user.useConfigOnly true` on kudu and niko to ensure that I set per-repo email addresses for commits.
Deleted bitbucket.org/douglatornell/dotfiles with redirect to github.com/douglatornell/dotfiles.
`git config --global core.excludesfile ~/.gitignore_global` is the way to set up a cross-repo .gitignore file.

Replaced NEMO_Nowcast hg clone w/ git clone on arbutus.cloud.
Backfilled nowcast-agrif runs:
* upload_forcing nowcast+ 2020-01-02 --debug
* upload_forcing turbidity 2020-01-02 --debug
* make_forcing_links nowcast-agrif 2020-01-02
* make_forcing_links nowcast-agrif 2020-01-03
* make_forcing_links nowcast-agrif 2020-01-04
* make_forcing_links nowcast-agrif 2020-01-05
Started building new nowcast-sys and salishsea-site deployments on salish:/scratch2 partition of 16Tb drive that also holds /backup2.
(SalishSeaCast)

Continued writing https://docs.google.com/document/d/1Gex3JdO8GpMdp0vxCPR05KOw5YFyg7mRV35j5gGJ8V8/edit?folder=0AMzQNtq8h6DpUk9PVA re: MOAD version control migration.
(MOAD)


Week 2
------

Mon 6-Jan-2018
^^^^^^^^^^^^^^

Fixed fallout from changing to Git clone of NEMO_Nowcast on arbutus.cloud; SalishSeaCmd was not ready to handle git repos.
Continued building new nowcast-sys and salishsea-site deployments on salish:/scratch2 partition of 16Tb drive that also holds /backup2; next step is building sarracenia-env.
Explored getting notifications from GitHub CI workflow into slack.
(SalishSeaCast)

Group mtg; see whiteboard.
(MOAD)

Discussed sensitivity studies progress and term work schedule w/ Vicky.
(MIDOSS)


Tue 7-Jan-2018
^^^^^^^^^^^^^^

Woke up feeling pretty exhausted.

Discussed Git & GitHub w/ Roger.

Added GitHub status atom feed to #general channel of SalishSeaCast workspace.
Explored educational pricing for Slack and sent to Susan via DM for consideration.
Finished building new nowcast-sys and salishsea-site deployments on salish:/scratch2 partition of 16Tb drive that also holds /backup2.
Added Slack incoming webhook for GitHub actions to SalishSeaCast workspace; added notification step to NEMO_Nowcast CI workflow.
(SalishSeaCast)

Lay down for a nap in the early afternoon and didn't get up until dinner time.


Wed 8-Jan-2018
^^^^^^^^^^^^^^

clear_checklist sequencing change from 4-Jan seems to have caused a manager crash and automation freeze this morning; resolution:
* backed out changeset de273bd2f867 re: clear_checklist launch
collect_weather 12 didn't finish; 8 files missing log shows 8 "expired message skipped" messages:
* killed collect_weather 12
* moved 20200108/12 aside
* ran download_weather 12
* started collect_weather 18
* deleted 20200108/12.aside
Updated copyright year range and versions in:
* SalishSeaNowcast
* NEMO-Cmd
* SalishSeaCmd
(SalishSeaCast)

Tried to help Rachael with her plan to change MIDOSS results files from x/y grid index dimensions to lon/lat dimensions.
Rachael pushed sensitivity_tests tag in CODE repo at r59
Updated code from r60 to r59 and re-built.
15jun17-21jun17 AKNS test run at code:r59 & config:r271; core dump
Created MOHID-Cmd issue#1 re: copying *.date files into temp run dir so that they are preserved with results of run for better reproducibility and easier run configuration archaeology.
(MIDOSS)

Restarted VHFR FVCOM runs for 07jan20 from 06jan20 23:30 restart files that Maxim provided:
* on arbutus.cloud:
  * hacked make_fvcom_boundary, make_fvcom_rivers_forcing & run_fvcom for -30 offset of start_time
  * stored hack in 30m-restart.patch
* on skookum:
  * hacked make_fvcom_atmos_forcingfor -30 offset of start_time
  * stored hack in 30m-restart.patch
  * launch_remote_worker arbutus.cloud-nowcast make_fvcom_boundary "arbutus.cloud-nowcast x2 nowcast --run-date 2020-01-07"
  * launch_remote_worker arbutus.cloud-nowcast make_fvcom_boundary "arbutus.cloud-nowcast r12 nowcast --run-date 2020-01-07"
* reverted hacks
(VHFR)


Thu 9-Jan-2018
^^^^^^^^^^^^^^

See work journal.
(Ocean Navigator)

Continued backfilling VHFR:
  * launch_remote_worker arbutus.cloud-nowcast make_fvcom_boundary "arbutus.cloud-nowcast x2 nowcast --run-date 2020-01-08"
  * launch_remote_worker arbutus.cloud-nowcast make_fvcom_boundary "arbutus.cloud-nowcast x2 nowcast --run-date 2020-01-09"
  * launch_remote_worker arbutus.cloud-nowcast make_fvcom_boundary "arbutus.cloud-nowcast r12 nowcast --run-date 2020-01-08"

  * launch_remote_worker arbutus.cloud-nowcast make_fvcom_boundary "arbutus.cloud-nowcast r12 nowcast --run-date 2020-01-09"
1st attempt failed because I forgot that I was unable to revert 30-miinnute offset hacks on arbutus.cloud last night; that left zombie watch_fvcom processes; killed them but also had to restart leg_aggregator on skookum to get messages flowing (restarted message_broker first, but that didn't make any difference, I don't think).
(VHFR)

Need to fix problem of `make_plots wwatch3 forecast*` launch after ping_erddap; decision whether we are plotting for forecast or forecast2 is flaky.
(SalishSeaCast)

Created make_readme.py (in 43ravens/on-notebooks) for GtiHub and recent notebook and Markdown.
(MOAD)

Fianlly got a successful AKNS run with relatively up to date repo revs; see https://midoss.slack.com/archives/CQXKS2CD8/p1578679712010700
(MIDOSS)


Fri 10-Jan-2018
^^^^^^^^^^^^^^^

See work journal.
(Ocean Navigator)

Helped Rachael with her quest for lon/lat output.
Experimented with reducing size of Turbulence.hdf5 results file by changing it to daily output after confirming that is apparently can't be completely suppressed; failed due to out of memory.
Discussed management of to-be-deleted /scratch files graham & cedar w/ Susan; decided to move just wwatch3/*/SoG_ww3_fields*.nc files to $PROJECT/
Got AKNS-spatial monte-carlo run going :-) timed out during hdf5-to-netcdf4 on 2h walltime; re-ran w/ 3h walltime;
(MIDOSS)


nowcast-x2 and forecast-x2 ran under automation.
Continued backfilling VHFR:
  * launch_remote_worker arbutus.cloud-nowcast make_fvcom_boundary "arbutus.cloud-nowcast r12 nowcast --run-date 2020-01-09"
  * launch_remote_worker arbutus.cloud-nowcast make_fvcom_boundary "arbutus.cloud-nowcast r12 nowcast --run-date 2020-01-10"
(VHFR)

wwatch3/forecast2 run didn't happen due to stuck make_ww3_wind_file; recovery:
* killed stuck worker
* launch_remote_worker arbutus.cloud-nowcast make_ww3_wind_file "arbutus.cloud-nowcast forecast --run-date 2020-01-10"
* nowcast run started! I guess because I caught it soon enough that race conditions managment with make_ww3_current_file was still waiting; that adds credence to the idea that a workers.spotter that kills make_ww3_wind_file if it hasn't finished after several minutes *and re-runs it* could resolve this issue.
(SalishSeaCast)

Race conditions between make_feeds and ping_erddap after NEMO and wwatch3 forecast2 runs struck again, causing no wwatch3 forecast2 plots, and a manager restart.
wwatch3 forecast2 plots are missing a section (straight line); issue might be in update_forecast_datasets.
(SalishSeaCast)


Sun 12-Jan-2018
^^^^^^^^^^^^^^^

wwatch3/nowcast run didn't happen due to stuck make_ww3_wind_file; recovery:
* killed stuck worker
* launch_remote_worker arbutus.cloud-nowcast make_ww3_wind_file "arbutus.cloud-nowcast forecast --run-date 2020-01-12"


Week 3
------

Mon 13-Jan-2018
^^^^^^^^^^^^^^^

Monthly IOS-UBC modeling collaboration mtg.
orcinus returned to operation; started backfilling nowcast-agrif:
* for d in {08..13}; upload_forcing orcinus-nowcast-agrif nowcast+ --run-date 2020-01-$d --debug
* for d in {08..13}; upload_forcing orcinus-nowcast-agrif turbidity  --run-date 2020-01-$d --debug
* make_forcing_link orcinus-nowcast-agrif nowcast-agrif --run-date 2020-01-08
* make_forcing_link orcinus-nowcast-agrif nowcast-agrif --run-date 2020-01-09

* make_forcing_link orcinus-nowcast-agrif nowcast-agrif --run-date 2020-01-10
* make_forcing_link orcinus-nowcast-agrif nowcast-agrif --run-date 2020-01-11
* make_forcing_link orcinus-nowcast-agrif nowcast-agrif --run-date 2020-01-12
* make_forcing_link orcinus-nowcast-agrif nowcast-agrif --run-date 2020-01-13
Added race condition mgmt after make_plots nemo forecast2 to ensure that boht make_feeds and ping_erddap have finished so that clear_checklist isnt launched until after ping_erddap has collected the information it needs to launch make_plots wwatch3 forecast2.
Changed run type detection in ping_erddap after wwatch3 runs to account for faster wwatch3 forecast2 runs that mean that both forecast and forecast2 are in the checklist.
(SalishSeaCast)

MOAD group mtg; see whiteboard.
(MOAD)

Phys Ocgy seminar by Phillipe Tortel re: flow through fluorescence measurements and phytoplankton production.

rsynced graham:wwatch3/*/SoG_ww3_fields_*.nc tree from $SCRATCH/MIDOSS/ to $PROJECT/MIDOSS/ to protect them from scratch deletion policy:
  rsync -rtv --include='SoG_ww3_fields_*.nc' --include='*/' --exclude='*' *1[5-9] ~/project/MIDOSS/forcing/wwatch3/
(MIDOSS)

See work journal.
(Ocean Navigator)


Tue 14-Jan-2018
^^^^^^^^^^^^^^^

See work journal.
(Ocean Navigator)

Finished backfilling nowcast-agrif:
* make_forcing_link orcinus-nowcast-agrif nowcast-agrif --run-date 2020-01-11
* make_forcing_link orcinus-nowcast-agrif nowcast-agrif --run-date 2020-01-12
* make_forcing_link orcinus-nowcast-agrif nowcast-agrif --run-date 2020-01-13
* make_forcing_link orcinus-nowcast-agrif nowcast-agrif --run-date 2020-01-14
(SalishSeaCast)


Wed 15-Jan-2018
^^^^^^^^^^^^^^^

Helped Susan set up snapd and skype on greta.

Discovered that Monday's power outage in the office due to heater and vacuum cleaner upstairs appears to have fried the D-Link Gigabit switch on my desk.
Cleaned up network gear in pantry.

FAL estate work.

Cherry-picked 2 commits from NEMO_Nowcast hg repo that I somehow pushed to Bitbucket after I migrated the repo to Git & GitHub :-( Discovered because split_results was raising an exception re: worker.cli.arrow_date() when Susan ran it manually (though it works fine in automation??)
(SalishSeaCast)

Updated MOHID-Cmd for 2020.
Resolved MOHID-Cmd issue#1 re: copying *.date files into temp run dir so that they are preserved with results of run for better reproducibility and easier run configuration archaeology.
(MIDOSS)


Thu 16-Jan-2018
^^^^^^^^^^^^^^^

Post-foreacst2 race condition mgmt failed to launch clear_checklist because ping_erddap wwatch3-forecast completed before make_plots nemo forecast2 initiated race condition mgmt.
Updated repos on salish:/scratch2/ in preparation for flip to /SalishSeaCast/; possible issues:
* OPPTools skookum:dc2323443abd2ca 19-Feb-19, salish:d33c4e9cdda8 6-Dec-19
* rivers-climatology skookum:31:45390bf38bd3 16feb19, salish:41:7d55df52a239 23nov19
Renamed /results2/SalishSea/hindcast.201905/ to nowcast-green.201905/ and created symlink for old name.
(SalishSeaCast)

Started adding V19-05 datasets:
* ubcSSg3DuGridFields1hV19-05
Added info to front page re: V19-05 datasets with gap due to server storage mgmt, and not yet real-time.
Copied setup.xml file into /opt/tomcat/content/erddap/ and bounced ERDDAP with:
* sudo /opt/tomcat/bin/shutdown.sh
* sudo /opt/tomcat/bin/startup.sh
(ERDDAP)

Monthly mtg; see whiteboard.
Helped Rachael sort out a merge issue in MIDOSS-MOHID-config.
(MIDOSS)


Fri 17-Jan-2018
^^^^^^^^^^^^^^^

FAL estate work.

Karina's PhD defense and celebration.


Sat 18-Jan-2018
^^^^^^^^^^^^^^^

White Rock; drove Modo Kona EV for the first time.

Test ran import of SSC/analysis-shared from Bitbucket to GitHub re: next week's MOAD mtg.
(SalishSeaCast)

Continued migrating personal & 43ravens repos from Bitbucket to GitHub:
* cookiecutter-djl-pypkg
* 43ravens:biz-journal to 43ravens-biz-journal
Added post-commit hooks to post highlights to rescuetime:
* ln -s ~/dotfiles/ubuntu/kudu/githooks/generic/rescuetime_commit_highlight.sh .git/post-commit
Added local user.email config settings:
* git config --local user.email "doug.latornell@43ravens.ca"


Sun 19-Jan-2018
^^^^^^^^^^^^^^^

Booked flights & hotel for Yellowknife trip.

Continued migrating MOAD repos from Bitbucket to GitHub:
* cookiecutter-moad-pypkg - cookiecutter-MOAD-pypkg
(MOAD)

Continued migrating personal & 43ravens repos from Bitbucket to GitHub:
* huebot -> HueBot
Added black pre-commit hook:
* ln -s ~/dotfiles/ubuntu/kudu/githooks/generic/pre-commit-hook.sh


Week 4
------

Mon 20-Jan-2020
^^^^^^^^^^^^^^^

MOAD group mtg; see whiteboard.
Demo-ed Bitbucket salishsea:analysis-shared to GitHub salishseacast:analysis-shared migration.
Investigated git merge tools.
(MOAD)

Phys Ocgy seminar by Tereza on SalishSeaCast carbon model.

Started updating NEMO_Nowcast dev docs re: migration to GitHub.
Discussed hindcast monthly avgs w/ Susan.
(SalishSeaCast)

Discussed sensitivity test runs and `mohid monte-carlo` w/ Vicky.
Started rsync-ing SalishSeaCast files for MOHID forcing from skookum to graham:
* rsync -rtv --include='SalishSea_1h_*_grid_*.nc' --include='SalishSea_1h_*_carp_T.nc' --include='*/' --exclude='*' 0[12]jan17 graham:project/MIDOSS/forcing/nowcast-green.201905/
(MIDOSS)


Tue 21-Jan-2020
^^^^^^^^^^^^^^^

FAL estate work.

See work joural.
(Resilient-C)

See work journal.
(Ocean Navigator)


Wed 22-Jan-2020
^^^^^^^^^^^^^^^

Continued rsync-ing SalishSeaCast files for MOHID forcing from skookum to graham;
~1h per month upload time; estimate storage at ~900Gb per year.
Turns out that Vicky already did that upload, and found the files.
(MIDOSS)

Answered question from Johannes about building wwatch3 v6.07 on cedar.

Added and updated dataset citation comment attrs:
* Add citation comment attributes to several datasets that were lacking
them.
* Update other citation comment attributes to include
Soontiens and Allen, 2017.
Not citations for:
* ubcSSaAtmosphereGridV1
* ubcSSaSurfaceAtmosphereFieldsV1
* ubcONCSCVIPCTD15mV1
* ubcONCSEVIPCTD15mV1
* ubcONCLSBBLCTD15mV1
* ubcONCUSDDLCTD15mV1
* ubcSSnBathymetryV17-02
* ubcSSn3DMeshMaskV17-02
* ubcSSn2DMeshMaskV17-02
* ubcONCTWDP1mV18-01
* ubcSSf2DWaveFields30mV17-02
* ubcSSWaveWatch3-SoGFilesV17-02
* ubcSSFVCOM-VHFRLowFilesV2
* ubcSSFVCOM-VHFR-BaroclinicX2
* ubcSSFVCOM-VHFR-BaroclinicR12
* ubcVFPA2ndNarrowsCurrent2sV1
* YuEtAlV1911
Continued adding V19-05 datasets:
* ubcSSg3DvGridFields1hV19-05
(ERDDAP)


Thu 23-Jan-2020
^^^^^^^^^^^^^^^

Broke corner off lower right rear molar during breakfast :-(

Pycharm Advanced Debugging Webinar:
Liza Shashkova and Andrey Lisin
  * Liza Debugger Features:
    * JetBrains Mono font (new)
    * can add breakpoints while debugger is running and they will take effect; also enable/disable on the fly
    * use suspend and logging expression on breakpoint to produce logging output
    * breakpoint conditions
    * any exceptions: activation policy (defaults to on termination; i.e. post-mortem debug)
    * cell debugging in Jupyter notebooks
  * Andrey Remote Debugging:
    * ssh interpreter
      * set Python interpreter (probably way into conda env)
      * choose sync folder on remote
    * remote debug run config
      * when you can't control how app runs from PyCharm?

Disabled forecst2 race condition mgmt because wwatch3 has finished before NEMO make_plots 2 days in a row (since ECCC compute upgrade shifted everything earlier).
(SalishSeaCmd)

See work journal.
(Navigator)

FAL estate work.

Email w/ Johannes about files he left on west.cloud that are long gone.


Fri 24-Jan-2020
^^^^^^^^^^^^^^^

Dentist appt to patch broken tooth and start process of getting a cap.

arbutus refused connection for upload_forcing nowcast+; re-ran manually at ~09:20 to restart automation.
Investigated how to better use race condition mgmt to ensure that clear_checklist is not launched so early that it disrupts wwatch3 post-forecast2 processing:
* need to ensure that both `make_plots nemo foreacst2 publish` and `make_plots wwatch3 foreacst2 publish` finish before make_feeds is launched
* that poses to problems:
  1. race condition mgmt doesn't know about worker args
  2. wwatch3 forecast2 doesn't run reliably due to make_ww3_wind_file occasionally getting stuck
(SalishSeaCast)

Email w/ Johannes about script to run wwatch3.

Wrote abstract for COSS-TT meeting.

Continued adding V19-05 datasets:
* ubcSSg3DwGridFields1hV19-05
* ubcSSgSurfaceTracerFields1hV19-05
* ubcSSg3DBiologyFields1hV19-05
* ubcSSg3DTracerFields1hV19-05
Datasets that have 18-12 versions but will not get 19-05 versions (and so will disappear):
* ubcSSgNearSurfaceUVelocity20mV18-12
* ubcSSgNearSurfaceVVelocity20mV18-12
Emailed Marlene to notify her of EOL of the ubcSSfDepthAvgdCurrents1hV18-06 dataset on 31-Jan-2020.
Started migrating erddap-datasets repo from Bitbuket to GitHub.
(ERDDAP)


Sat 25-Jan-2020
^^^^^^^^^^^^^^^

Finished migrating erddap-datasets repo from Bitbuket to GitHub.
(ERDDAP)

See work journal.
(Navigator)


Sun 26-Jan-2020
^^^^^^^^^^^^^^^

See work journal.
(Navigator)


Week 5
------

Mon 27-Jan-2020
^^^^^^^^^^^^^^^

Weekly group mtg; see whiteboard.
(MOAD)

Phys Ocgy seminar by Johannes Gemmrich on SoG wave model.

Timesheet. Staff conflict of interest declaration.

Started exploring if/how NEMO_Nowcast race conditions mgmt can be made to handle different invocations of the same worker.
(SalishSeaCast)

Farewell drinks for Gonzalo.


Tue 28-Jan-2020
^^^^^^^^^^^^^^^

collect_weather 06 had not completed at 10:00; investigation:
* 06 forecast: 109 files accumlated in /results/forcing/; 458 files downloaded byt sarracenia, but not moved to /results/forcing/
* sarracenia log:
  * a bunch of:
      2020-01-28 01:17:47,441 [ERROR] Download failed https://dd5.weather.gc.ca/model_hrdps/west/grib2/06/011/CMC_hrdps_west_LHTFL_SFC_0_ps2.5km_2020012806_P011-00.grib2
      2020-01-28 01:17:47,442 [ERROR] Failed to reach server. Reason: [Errno -3] Temporary failure in name resolution
      2020-01-28 01:17:47,442 [ERROR] Download failed https://dd5.weather.gc.ca//model_hrdps/west/grib2/06/011/CMC_hrdps_west_LHTFL_SFC_0_ps2.5km_2020012806_P011-00.grib2. Type: <class 'urllib.error.URLError'>, Value: <urlopen error [Errno -3] Temporary failure in name resolution>
  * then, later:
      2020-01-28 01:26:03,798 [INFO] expired message skipped 20200128091041.641 https://dd5.weather.gc.ca /model_hrdps/west/grib2/06/011/CMC_hrdps_west_LHTFL_SFC_0_ps2.5km_2020012806_P011-00.grib2
      2020-01-28 01:26:03,799 [INFO] expired message skipped 20200128091041.489 https://dd5.weather.gc.ca /model_hrdps/west/grib2/06/010/CMC_hrdps_west_UGRD_TGL_10_ps2.5km_2020012806_P010-00.grib2
      2020-01-28 01:26:03,799 [INFO] expired message skipped 20200128091043.610 https://dd5.weather.gc.ca /model_hrdps/west/grib2/06/011/CMC_hrdps_west_UGRD_TGL_10_ps2.5km_2020012806_P011-00.grib2
      2020-01-28 01:26:03,799 [INFO] expired message skipped 20200128091043.872 https://dd5.weather.gc.ca /model_hrdps/west/grib2/06/011/CMC_hrdps_west_PRATE_SFC_0_ps2.5km_2020012806_P011-00.grib2
      2020-01-28 01:26:03,799 [INFO] expired message skipped 20200128091044.935 https://dd5.weather.gc.ca /model_hrdps/west/grib2/06/011/CMC_hrdps_west_RH_TGL_2_ps2.5km_2020012806_P011-00.grib2
* all 12 forecast files appear to have been downloaded by sarracenia
* recovery:
    kill collect_weather 06
    rm -rf /results/forcing/atmospheric/GEM2.5/GRIB/20200128/06
    download_weather 06
    upload_forcing forecast2 failed because we were too late requesting Neah Bay ssh; Susan did recovery
    upload_forcing forecast2 for 6 clusters
    collect_weather 18
    wait for forecast2 completion
    download_weather 12
(SalishSeaCast)

See work journal.
(Navigator)

See work journal.
(Resilient-C)

Birthday dinner for Rachael.


Wed 29-Jan-2020
^^^^^^^^^^^^^^^

collect_weather 06 had not completed at 07:00; investigation:
* 06 forecast: 20 files accumulated in /results/forcing/; 546 files downloaded by sarracenia, but not moved to /results/forcing/
* similar pattern of name resolution errors in sarracenia log between 01:09:07 through 01:13:56, and again between 01:19:07 through 01:23:54.
* 12 forecast files download by sarracenia in progress
* recovery:
    kill collect_weather 06
    rm -rf /results/forcing/atmospheric/GEM2.5/GRIB/20200129/06
    download_weather 06
    upload_forcing forecast2 failed because we are using an outdated Neah Bay ssh URL re: 2019 Trump US gov't shutdown; Susan did recovery
    upload_forcing forecast2 for 6 clusters
    wait for 12 weather sarracenia downloads to finish
    collect_weather 18
    wait for forecast2 completion
    download_weather 12
    clear /SalishSeaCast/datamart/hrdps-west/ directories
Network glitched at 09:00 taking both salishsea-site and Resilient-C offline momentarily; also seemed to stall download_weather 12; deleted tree and re-ran to restart automation.
Helped Tereza set up conda env for mocsy and sort through import path issue; puzzled that path to .so has to be added explicitly.
nowcast-green got stuck on launch, and I didn't notice until ~17:30; cleaned up and re-ran make_forcing_links to get it going.
(SalishSeaCast)

See work journal.
(Navigator)

Git refresher session lead by Karina:
* why staging?
* git rm seem hyper aggressive
(MOAD)

Taught Vicky how to migrate repo from hg on Bitbucket to git on GitHub.
(MIDOSS)


Thu 30-Jan-2020
^^^^^^^^^^^^^^^

collect_weather 06 had not completed at 07:00; investigation:
* 06 forecast: 571 files accumulated in /results/forcing/; 0 files downloaded by sarracenia, but not moved to /results/forcing/
* similar pattern of name resolution errors in sarracenia log between 01:18:32 through 01:23:21 accounts for 5 missing files
* 12 forecast files download by sarracenia in progress; completed at 07:51
* recovery started at 08:15:
    kill collect_weather 06
    rm -rf /results/forcing/atmospheric/GEM2.5/GRIB/20200130/06
    download_weather 06
    collect_weather 18
    wait for forecast2 completion
    NEMO forecast2 failed due to nowcast8 VM network connection issue; retry failed due to nowcast2 connection issue; retry at ~10:35 succeeded
    download_weather 12
    clear /SalishSeaCast/datamart/hrdps-west/ directories
    pull Susan's get_NeahBay_ssh fix on salish:/scratch2
(SalishSeaCast)

Helped Rachael with private error-log repo migration to GitHub.
(MIDOSS)


Fri 31-Jan-2020
^^^^^^^^^^^^^^^

Dentist appt to prep for crown and get temporary.

Researched Tereza's mocsy import issue and learned more; see https://salishseacast.slack.com/archives/CFR6VU70S/p1580501579016600
Added codecov.io unittest coverage reporting to NEMO_Nowcast:
* added repo on codecode.io
* stored upload token as CODECOV_TOKEN secret on GitHub
* added pytest-cov to environment-test.yaml
* changed coverage report step of workflow to use codecov/codecov-action@v1 action
Started migration of SalishSeaNowcast repo to GitHub:
* import as public SalishSeaNowcast repo
(SalishSeaCast)

Understood:
  git log --pretty=oneline --abbrev-commit --graph @{u}..
as quasi-equivalent of `hg outgoing`; added `git out` alias on niko; can be used with or without --stat flag.

Disabled ubcSSfDepthAvgdCurrents1hV18-06.
(ERDDAP)


Sat 1-Feb-2020
^^^^^^^^^^^^^^

Worked through my typical "forgot to commit/push my worklog" pull/rebase/merge-conflict-resolution in git:
* git pull  # resulted in merge conflict
* git rebase --abort  # return to state before rebase to research how to proceed
* # decided to try explcity merge tool
* git pull
* git mergetool --tool kdiff3
* # resolved conflicts, saved, and exited kdiff3
* git rebase --continue
* git push
Added `git out` alias on kudu.
Understood:
  git fetch && git log --pretty=oneline --abbrev-commit --graph ..@{u}
as quasi-equivalent of `hg incoming`; added `git in` alias on kudu; can be used with or without --stat flag.
Continued migration of SalishSeaNowcast repo to GitHub:
* add repo description, link, and topics
* add repo to codecov
* store codecov upload token as CODECOV_TOKEN secret on GitHub
* add notifications to #ssc-repos channel; /github subscribe SalishSeaCast/SalishSeaNowcast
* migrate issues:
  * use kudu /media/doug/warehouse/bitbucket-issue-migration clone https://github.com/jeffwidman/bitbucket-issue-migration and bitbucket-issue-migration conda env
    * python3 -m migrate SalishSeaCast/SalishSeaNowcast salishsea/salishseanowcast douglatornell
      * use GitHub personal access token instead of GitHub password
* change readthedocs webhook
* replace .hgignore with .gitignore

* renamed env/ to envs/
* change Bitbucket pipeline to GH Actions CI workflow
  * add #ssc-repos webhook url as SLACK_WEBHOOK_URL secret on GitHub
  * added pytest-cov to environment-test.yaml
  * changed coverage report step of workflow to use codecov/codecov-action@v1 action
* update dev docs:
  *
* change run_NEMO, test_run_NEMO & deployment docs re: install from GH
* delete Bitbucket salishseanowcast repo w/ redirect
* Update clones:
  * kudu
    * mv SalishSeaNowcast hg/SalishSeaNowcast.hg
    * git clone git@github.com:SalishSeaCast/SalishSeaNowcast.git
    * rsync -rltv hg/SalishSeaNowcast.hg/.idea SalishSeaNowcast/
    * rm SalishSeaNowcast/.idea/vcs.xml
    * git config --local user.email "dlatornell@eoas.ubc.ca"
    * ln -s ~/dotfiles/ubuntu/kudu/githooks/generic/pre-commit-hook.sh
    * ln -s ~/dotfiles/ubuntu/kudu/githooks/generic/rescuetime_commit_highlight.sh .git/hooks/post-commit

  * niko
  * skookum
  * salish
  * arbutus.cloud
(SalishSeaCast)


Sun 2-Feb-2020
^^^^^^^^^^^^^^

See work journal.
(Navigator)


February
========

Week 6
------

Mon 3-Feb-2020
^^^^^^^^^^^^^^

MOAD group mtg; see whiteboard.
(MOAD)

See work journal.
(Navigator)

Answered email from Mike re: updating gomss-site.
(GoMSS)

Invited Ben to GitHub orgs.
Continued migration of SalishSeaNowcast repo to GitHub:
* Update clones:
  * niko
    * mv SalishSeaNowcast hg/SalishSeaNowcast.hg
    * git clone git@github.com:SalishSeaCast/SalishSeaNowcast.git
    * rsync -rltv hg/SalishSeaNowcast.hg/.idea SalishSeaNowcast/
    * rm SalishSeaNowcast/.idea/vcs.xml
    * git config --local user.email "dlatornell@eoas.ubc.ca"
    * ln -s ~/dotfiles/ubuntu/niko/githooks/generic/pre-commit-hook.sh
    * ln -s ~/dotfiles/ubuntu/niko/githooks/generic/rescuetime_commit_highlight.sh .git/hooks/post-commit
  * salish
    * rm -rf SalishSeaNowcast
    * git clone git@github.com:SalishSeaCast/SalishSeaNowcast.git
Migrated repos to GitHub:
* SalishSeaCast/analysis-doug
  * update copyright year range
  * update make_readme.py modules
  * fix Markdown headings in notebooks
* SalishSeaCast/nowcast-vm
(SalishSeaCast)


Tue 4-Feb-2020
^^^^^^^^^^^^^^

See work journal.
(Navigator)


Wed 5-Feb-2020
^^^^^^^^^^^^^^

See work journal.
(Navigator)

Email to Emilio re: no SSC datasets on NVS since 30-Sep.
Continued migration of SalishSeaNowcast repo to GitHub:
* renamed env/ to envs/
* moved requirements.txt to top level dir to take advantage of Insights Dependency Graph and Dependabot Security alerts
* starting adding GH Actions CI workflow
  * added #ssc-repos webhook url as SLACK_WEBHOOK_URL secret on GitHub

* update dev docs:
  *
* change run_NEMO, test_run_NEMO & deployment docs re: install from GH
* delete Bitbucket salishseanowcast repo w/ redirect

* Update clones:
  * skookum
  * arbutus.cloud
(SalishSeaCast)


<<<<<<< HEAD
Thu 6-Feb-2020
^^^^^^^^^^^^^^

FAL estate work.

See work journal.
(Navigator)

Migrated Bitbucket douglatornell/aims-workshop to GitHub douglatornell/AIMS-Workshop for one of Susan's classes assignment.
(MOAD)


Fri 7-Feb-2020
^^^^^^^^^^^^^^

See work journal.
(Navigator)

Monthly project mtg; see whiteboard.
(MIDOSS)

Continued migration of SalishSeaNowcast repo to GitHub:
* continued adding GH Actions CI workflow

* update dev docs:
  *
* delete Bitbucket salishseanowcast repo w/ redirect

* Update clones:
  * arbutus.cloud

Worked w/ Charles to flip salish:/scratch2 to become skookum:/SalishSeaCast:
* updated NEMO_Nowcast and SalishSeaNowcast git clones
* create /scratch2/datamart/hrdps-west/[00|06|12|18] directories
* committed removal of forecast2 race condition mgmt
* changed run_NEMO, test_run_NEMO & deployment docs re: install from GH
* kill collect_weather 00
* kill watch_fvcom nowcast-x2
* kill watch_fvcom nowcast-r12
* kill forecast-x2 run
* kill nowcast-r12 run
* stop supervisord
* stop salishsea-site
* flip
* had to build new conda envs :-(
* start salishsea-site
* update arbutus.cloud clone
* start supervisord
* re-start collect_weather 00
* re-start nowcast-x2 run
* re-start nowcast-r12 run
There may be chaos for the forecast2 runs because I did not copy the checklist into the new /SalishSeaCast.
(SalishSeaCast)


Sat 8-Feb-2020
^^^^^^^^^^^^^^

Cleaned up after failed forecast2 launch due to startup without checklist after yesterday's /SalishSeaCast flip; skipped forecast2 runs; started nowcast automation manually about 1hr late.
nowcast-dev failed because I followed the docs that told me to build SalishSeaCast on salish instead of SalishSeaCast_Blue; fixed docs; did build; manually re-launched nowcast-dev via make_forcing_links.
make_fvcom_atmos_forcing failed on skookum due to missing dependencies for OPPTools; did git checkout 4af96c499cdc49e96a87f999870be1560807d925 to get same working version as on arbutus; and launched nowcast-x2 and nowcast-r12 manually.
(SalishSeaCast)

Transferred GitHub douglatornell/AIMS-Workshop to UBC-MOAD/AIMS-Workshop where it really belongs; replaced .hgignore with .gitignore.
(MOAD)

See work journal.
(Navigator)

Migrated repos to GitHub:
* SalishSeaCast/SOG-Bloomcast-Ensemble

  * update copyright year range
  * update make_readme.py modules
  * fix Markdown headings in notebooks
(bloomcast)


Sun 9-Feb-2020
^^^^^^^^^^^^^^

Updated SOG-Bloomcast-Ensemble:
  * post-commit hook
  * user.email
  * no pre-commit hook for black

  * update dev env pkgs re: security alerts
  * update copyright year range
(bloomcast)

FAL estate work.

make_plots nemo forecast publish failing due to numpy errors:
* figures/publish/pt_atkinson_tide.py", line 95, in _plot_tide_cycle
    TypeError: float() argument must be a string or a number, not 'Timestamp'
* figures/publish/compare_tide_prediction_max_ssh.py", line 184, in _prep_plot_data
    numpy.core._exceptions.UFuncTypeError: ufunc 'add' cannot use operands with types dtype('O') and dtype('<m8[s]')
* changed nowcast-fig-dev.yaml from python=3.7 to python>=3.6
* built nowcast-fig-dev-feb20 env
* TypeError: float()... is the new manifestation of issue#69
* Hacked around numpy.core._exceptions.UFuncTypeError: ufunc 'add'... with an astype() in figures.shared, but need to understand the deeper issue.
Explored HRDPS 1km experimental forecast; decided to try to get a sarracenia client running to capture it for now and worry about extending collect_weather later:
* created SalishSeaNowcast/sarracenia/hrdps-west-1km.conf
* added [program:sr_subscribe-hrdps-west-1km] section to SalishSeaNowcast/config/supervisord.ini
* added
    amqps://anonymous:anonymous@dd.alpha.weather.gc.ca
  to skookum:.config/sarra//credentials.conf
* supervisorctl reload added and startd sr_subscribe-hrdps-west-1km
(SalishSeaCast)





TODO:
* Delete ubcSSfDepthAvgdCurrents1hV18-06 from ERDDAP on Fri 7-Feb-2020
* Sort out OPPTools dependencies so that we can run w/ origin/master:HEAD again
* Fix:
    /media/doug/warehouse/conda_envs/nemo-nowcast/lib/python3.8/pathlib.py:1299: DeprecationWarning: an integer is required (got type FilePerms).  Implicit conversion to integers using __int__ is deprecated, and may be removed in a future version of Python.
      self._accessor.chmod(self, mode)



Stack:
* create NEMO_Nowcast.workers.spotter to monitor and optionally kill workers that tend to get stuck; initial use cases: collect_weather, make_ww3_wind_file
* wwatch3 run success confirmation
* fix warnings in figure modules
* add hindcast deployment to SalishSeaNowcast docs
* fix get_vfpa_hadcp MMSI AttributeError issue
* debug gemlam interpolation
* Elise's notebooks into Sphinx

Done:
* Disable ubcSSfDepthAvgdCurrents1hV18-06 on ERDDAP on Fri 31-Jan-2020
