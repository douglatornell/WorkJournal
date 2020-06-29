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
(Prediction Core)

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
* that poses 2 problems:
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


Week 7
------

Mon 10-Feb-2020
^^^^^^^^^^^^^^^

UBC/DFO model collab mtg:
* SSMS presentation by Elise
* discussed Laura's initial analysis of dissolved O2 from hindcast; model seems low
* talked about 1km HRDPS
* I emailed link to Susan's 2019-05 hindcast viz book to Laura & Michael
* forwarded 1km HRDPS email to Laura and Michael
(Prediction Core)

Weekly group mtg; see whiteboard.
(MOAD)

Phys ocgy seminar; Ocean Sciences practice talks by Elise & Anna

Emailed Sandrine re: my failure to get sarracenia working for 1 km HRDPS; solution: amqp instead of amqps because dd.alpha is not yet HTTPS.
Started work on adapting download_weather and collect_weather to operate on either 2.5km or 1km HRDPS product streams.
Hacked download_weather enough to get files from dd.alpha server.
(SalishSeaCast)


Tue 11-Feb-2020
^^^^^^^^^^^^^^^

See work journal.
(Navigator)

FAL estate work.


Wed 12-Feb-2020
^^^^^^^^^^^^^^^

See work journal.
(Navigator)

Finished backlog downloads of 1km HRDPS files from dd.alpha server using hacked download_weather.
Continued hacking on SalishSeaNowcast CI workflow:
* used pip install --src to try to get dependencies pkgs source checkouts out of pkg envs/ dir
Continued work on adapting download_weather and collect_weather to operate on either 2.5km or 1km HRDPS product streams.
(SalishSeaCast)

Completed UBC staff conflict of interest declaration.


Thu 13-Feb-2020
^^^^^^^^^^^^^^^

Dentist appt for final lower right molar cap.

See work journal.
(Navigator)

See work journal.
(Resilient-C)

Helped Rachael via slack to try to get started using mohid monte-carlo.
(MIDOSS)

Downloaded today's 1km HRDPS files from dd.alpha server using hacked download_weather.
(SalishSeaCast)


Fri 14-Feb-2020
^^^^^^^^^^^^^^^

See work journal.
(Navigator)

Fixed bugs reported by Vicky in Make-MIDOSS-Forcing re: MF0 in output path, and output directories creation in /scratch/dlatorne/MIDOSS/forcing/.
(MIDOSS)

Continued hacking on SalishSeaNowcast CI workflow:
* used Bitbucket password passed as secret to do pip VCS install of private FVCOM-Cmd pkg
* used GitLab personal access token passed as secret to do pip VCS install of private OPPTools pkg
Downloaded today's 1km HRDPS files from dd.alpha server using hacked download_weather.
Continued work on adapting download_weather and collect_weather to operate on either 2.5km or 1km HRDPS product streams.
Updated skookum OPPTools checkout to detached HEAD 6c784a4d to get get_cmap_speed() that was causing `make_plots fvcom * research` to fail.
(SalishSeaCast)

Attended CMOS annual tour lecture about 2020 Canadian Climate Change Assessment Report by NAthan Gillet of CCCma.

Deleted ubcSSfDepthAvgdCurrents1hV18-06 from ERDDAP.
(ERDDAP)


Sat 15-Feb-2020
^^^^^^^^^^^^^^^

Created navigator conda env on kudu so that I can run unit tests there rather than in container to avoid PyCharm remote interpreter file sync hitches; had to remove strict version pinning on gdal and libgdal from config/conda/environment.yml

Worked with Susan to migrate production from 2018-12 to 2019-05:
* Susan crafted SS-run-sets/v201915/nowcast-[blue|green] dirs and symlinked forecast and forecast2 from the nowcast-blue dir
* uploaded to arbutus.cloud:
  * recent LiveOcean_v201905_*.nc files
  * hindcast.201905/14feb20 restart files
  * symlinked hindcast.201905/14feb20 as nowcast-green/14feb20
* update nowcast.yaml:
  * "temperature salinity"."file template"
  * "temperature salinity".parameter_set
  * "run types":"run sets dir"
  * "results archive"
  * run."enabled hosts".salish-nowcast."run types".nowcast-green.results
* tag repos with PROD-nowcast-green-201905 at PROD-hindcast_201905-v3
  * grid
  * NEMO-3.6-code
  * rivers-climatology
  * tides
  * tracers
  * XIOS-ARCH
* tag repo with PROD-nowcast-green-201905 at PROD-nowcast-green-201812
  * XIOS-2
* pulled and update SalishSeaNowcast repo on skookum
* pulled and updated repos on arbutus.cloud:
  * updated to PROD-nowcast-green-201905:
    * NEMO-3.6-code
    * XIOS-2
    * XIOS-ARCH
    * grid
    * rivers-climatology
    * tides
    * tracers
  * updated to tip:
    * NEMO-Cmd
    * NEMO_Nowcast
    * SS-run-sets
    * SalishSeaCmd
    * SalishSeaNowcast
    * moad_tools
* update NEMO-3.6-code:
  * arbutus.cloud SalishSeaCast and SalishSeaCast_Blue
  * salish for nowcast-dev SalishSeaCast_Blue
* Susan edited nowcast-green/14feb20/namelist_cfg on arbutus to make its nn_it000 value consistent with the uploaded restart files
* launched nowcast-green test via make_forcing_links
  * nowcast-green and wwatch3 nowcast ran successfully
  * wwatch3 forecast failed
* created results dirs:
  * /results/SalishSea/nowcast-blue.201905
  * /results/SalishSea/forecast.201905
  * /results/SalishSea/forecast2.201905
* symlinked 10-15feb20 into above results dirs so that rolling forecasts will be smooth
Downloaded today's 1km HRDPS files from dd.alpha server using hacked download_weather.
(SalishSeaCast)

See work journal.
(Navigator)


Sun 16-Feb-2020
^^^^^^^^^^^^^^^

Continued work w/ Susan to migrate production from 2018-12 to 2019-05:
* nowcast/16feb20 failed due to incorrect nn_it000 value in nowcast/15feb20/namelist_cfg; the value on arbutus needed to be changed to be compatible with the nowcast-green/15feb20 restart file that we produced last night
* nowcast/16feb20 failed again due to a missed closing tag in file_def.xml; Susan fixed
* nowcast-agrif failed due to outdated LiveOcean file names:
  * uploaded recent LiveOcean_v201905_*.nc files to orcinus
  * Susan updated namelist.lateral to refer to them
  * pulled SS-run-sets on orcinus
  * re-launched with make_forcing_links orcinus nowcast-agrif
* nowcast-agrif failed due to broken symlink for namelist_top_cfg after updating SS-runsets re: above failure:
  * breakage due to splitting of namelist_top_cfg into several files
  * Susan replaced broken symlink with appropriate concatenated namelist_top_cfg file for agrif only
  * pulled SS-run-sets on orcinus
  * re-launched with make_forcing_links orcinus nowcast-agrif
* updated nowcast-green ERDDAP dataset ids to V19-05 in config for ping_erddap
* modernized ping_erddap unit tests
* nowcast-agrif failed due to too agreesive updating of namelist.lateral:
  * Susan fixed namelist.lateral
  * pulled SS-run-sets on orcinus
  * re-launched with make_forcing_links orcinus nowcast-agrif
* nowcast-dev failed because it was looking for 201712 LiveOcean files:
  * Susan added nowcast-dev/ dir to SS-run-sets/v201915/
  * Susan changed nowcast-dev in nowcast.yaml config from running v201702 to v201905
  * pulled SS-run-sets on skookum
  * pulled SalishSeaNowcast on skookum
  * re-launched with make_forcing_links salish nowcast+ --shared-storage
* changed nowcast-dev results storage to new nowcast-dev.201905/ directory
* emailed Emilio re: change from V18-12 to V19-05
* updated ERDDAP front page
Downloaded today's 1km HRDPS files from dd.alpha server using hacked download_weather.
(SalishSeaCast)

See work journal.
(Navigator)


Week 8
------

Mon 17-Feb-2020
^^^^^^^^^^^^^^^

**Statutory Holiday** - BC Family Day

See work journal.
(Navigator)

Continued work w/ Susan to migrate production from 2018-12 to 2019-05:
* nowcast-dev failed because 16feb20 restart and namelist_cfg weren't in nowcast-dev.201905 ???:
  * created appropriate symlinks
  * re-launched with make_forcing_links salish nowcast+ --shared-storage
Downloaded today's 1km HRDPS files from dd.alpha server using hacked download_weather.
(SalishSeaCast)


Tue 18-Feb-2020
^^^^^^^^^^^^^^^

See work journal.
(Navigator)

Got fingerprints done for DFO security screening.

Downloaded today's 1km HRDPS 00 files from dd.alpha server using hacked download_weather.
(SalishSeaCast)


Wed 19-Feb-2020
^^^^^^^^^^^^^^^

collect_weather 06 failed due to network issues; recovery started at 07:30:
  kill collect_weather 06
  rm -rf /results/forcing/atmospheric/GEM2.5/GRIB/20200219/06
  download_weather 06
  wait for 12 weather sarracenia downloads to finish
  collect_weather 18
  wait for forecast2 completion
  download_weather 12
make_ww3_wind_file for forecast2 got stuck; killed it and re-ran manually for forecast.

Downloaded today's 1km HRDPS files from dd.alpha server using hacked download_weather.
(SalishSeaCast)

See work journal.
(Navigator)

Dental hygiene appt.

Sent DFO security screening package to Wanda@NAFC.

Started work on setting up 2020 bloomcast:
* runs dir: /data/dlatorne/SOG-projects/SoG-bloomcast-ensemble/run/
* created /data/dlatorne/SOG-projects/hg/
* moved SoG-bloomcast-ensemble/ to hg/SoG-bloomcast-ensemble.hg/
* cloned SOG-Bloomcast-Ensemble from GitHub
* replaced .hgignore with .gitignore
* cp run/2019_bloomcast_inifile.yaml run/2020_bloomcast_infile.yaml
* archived 2019_bloomcast* files in run/2019/
* archived bloomcast.log and bloom_date_evolution.log files into run/2019/
* edit 2020_bloomcast_infile.yaml
* edit config.yaml
* disable push to web for test run
* source activate /data/dlatorne/SOG-projects/blomcast-env-mpl-1.5.3 # note misspelling
* pip install -e /data/dlatorne/SOG-projects/SoG-Bloomcast-Ensemble
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

* edit new weather descriptions into cloud fraction file and commit
* tag for 2020
(bloomcast)

Talked to Vicky about oil movement wind sensitivity experiment pipeline.
(MIDOSS)


Thu 20-Feb-2020
^^^^^^^^^^^^^^^

See work journal.
(Navigator)

make_forcing_links orcinus nowcast-agrif glitched on auth; re-ran manually with success at ~10:40.
Downloaded today's 1km HRDPS files from dd.alpha server using hacked download_weather.
Continued work on adapting download_weather and collect_weather to operate on either 2.5km or 1km HRDPS product streams.
(SalishSeaCast)

Vancouver to Yellowknife


Fri 21-Feb-2020
^^^^^^^^^^^^^^^

Yellowknife.
Walked part way around Niven Lake near hotel. Went to Aurora Village.

See work journal.
(Navigator)

Downloaded today's 1km HRDPS files from dd.alpha server using hacked download_weather.
Continued work on adapting download_weather and collect_weather to operate on either 2.5km or 1km HRDPS product streams.
(SalishSeaCast)


Sat 22-Feb-2020
^^^^^^^^^^^^^^^

Yellowknife.
Dog sled tour from Grace Lake with Becks Kennels guide Elizabeth.
Walked to Old Town and Snow Castle on Yellowknife Bay of Great Slave Lake, via NWT Brewing tap room.
Midnight stroll to try to view aurora to the hill behind the hotel above Niven Lake.

See work journal.
(Navigator)

Downloaded today's 1km HRDPS files from dd.alpha server using hacked download_weather.
Finished work on adapting download_weather and collect_weather to operate on either 2.5km or 1km HRDPS product streams.
Finally solved CI workflow VCS install for SalishSeaTools; needed quotes in workflow YAML to protect &subdirectory=.
(SalishSeaCast)


Sun 23-Feb-2020
^^^^^^^^^^^^^^^

Long walk part way around Frame Lake.

Yellowknife to Vancouver

Figured out how to suppress TLS certs verification via requests.Session in download_weather instead of having to hack the option all the way into request.get().
(SalishSeaCast)


Week 9
------

Mon 24-Feb-2020
^^^^^^^^^^^^^^^

Deleted YuEtAlV1911 dataset that is now on UBC Dataverse at https://doi.org/10.5683/SP2/ZM89PF
(ERDDAP)

(SalishSeaCast)

Started migration of UBC_MOAD group repos:
* ariane-2.2.6_00
(MOAD)

Phys Ocgy seminar by Tetyana Ross re: O2 min zone and seamount marine protected areas.

Earth Data Science candidate seminar by Alison Malcolm re: data science for geophysics

Helped Vicky run split_results on her wind effect investigation.
(MIDOSS)


Tue 25-Feb-2020
^^^^^^^^^^^^^^^

See work journal.
(Navigator)

Continued migration of UBC_MOAD group repos:
* seatracker-matlab
* SeaTracker-Python
(MOAD)


Wed 26-Feb-2020
^^^^^^^^^^^^^^^

See work journal.
(Navigator)

Continued migration of UBC_MOAD group repos:
* ariane-2.2.8-code
* docs
  * change readthedocs webhook
    * application/json
    * Leave the Secrets field blank
    * select individual events: Branch or tag creation, Branch or tag deletion, and Pushes
  * update copyright year range
  * update badges in README and contributing
  * resolve security alerts re: jinja2, requests, urllib3, cryptography
  * update readthedoc.yml file to schema 2.0
  * subscribe to notifications in #ssc-repos channel
(MOAD)

Emailed Michael about 1km HRDPS archive from 2019-10-24 onward saying that we don't have storage for full RPNs, just 11 surface-ish variables (~75G).
Updated SalishSeaNowcast dev docs & README re: Bitbucket to GitHub migration.
Fixed bugs in NEMO_Nowcast docs re: Bitbucket to GitHub migration.
(SalishSeaCast)


Thu 27-Feb-2020
^^^^^^^^^^^^^^^

Emailed Rachael & Vicky re: deleting /results2/MIDOSS/; got approval and did the deletion.
(MIDOSS)

See work journal.
(Navigator)


Fri 28-Feb-2020
^^^^^^^^^^^^^^^

Mtg w/ Richard Dewey & Gordon Rees of ONC re: modelling support:
* Susan, Doug, Ben
* ONC has lots of new funding for operational support
Discussed new workstations spec and chopstick, and load on skookum with Charles.
Discussed dask and chunking with Ben.
(SalishSeaCast)

Finished migration of UBC_MOAD group repos:
* moad_tools
  * subscribe to notifications in #ssc-repos channel
  * change readthedocs webhook
    * application/json
    * Leave the Secrets field blank
    * select individual events: Branch or tag creation, Branch or tag deletion, and Pushes
  * add .gitignore
  * update copyright year range
  * update readthedoc.yml file to schema 2.0
  * bump version to 20.1.dev0
  * update dev env and requirements.txt
  * update badges in README and contributing
(MOAD)

Created repos migration plan for next week and emailed it.
Discussed proscribed wind runs with Vicky.
(MIDOSS)


Sat 29-Feb-2020
^^^^^^^^^^^^^^^

White Rock

Changed skookum and arbutus installs of moad_tools to be git clones.
Updated deployment docs re: moad_tools clone, and python3 -m pip install.
(SalishSeaCast)

We Shall Overcome MLK concert lead by Damien Sneed at Chan Centre


Sun 1-Mar-2020
^^^^^^^^^^^^^^

Started processing of Yellowknife photos:
* launch RPD with /media/doug/warehouse/Pictures/RapidPhotoDownloader-0.9.14/RapidPhotoDownloader/bin/rapid-photo-downloader
* Downloaded all images from OM-D card
* discovered that camera clock had reset to 2012-01-01 00:00 for all images; fixed file names via Python in /media/doug/warehouse/Pictures/ and on backup drive
* imported them into Darktable
* updated backup drive
* ran borg backup to lizzy

Preliminary 2019 income tax work.

FAL estate work.


Week 10
-------

Mon 2-Mar-2020
^^^^^^^^^^^^^^

Returned JRA's rental scooter to McDonald Home Healthcare.

Moad team mtg; see whiteboard.
Emailed Karina re: her trick for cloning git repo into existing hg clone.
(MOAD)

Started migration of MIDOSS repos:
* Vicky migrated:
  * sensitivity-tests-log
  * docs
  * analysis-ashutosh
* analysis-doug
* analysis-xaoimei
Emailed Shihan and Xaoimei for their GitHub ids
* docs:
  * subscribe to notifications in #soiled channel
  * change readthedocs webhook
    * application/json
    * Leave the Secrets field blank
    * select individual events: Branch or tag creation, Branch or tag deletion, and Pushes
  * update copyright year range
  * resolve security alerts re: jinja2, requests, urllib3, cryptography
  * update badges in README and contributing
  * update readthedoc.yml file to schema 2.0
(MIDOSS)

readthedocs doesn't like to use conda-forge channel because repodata.json file is too big.

Invited Elise to GitHub orgs.
Backfilled fvcom nowcast-r12 publish figures for 13-19 and 22-29 Feb
(SalishSeaCast)

Did ONC annual survey and compiled list of talks, posters, etc. I was named on in 2019.


Tue 3-Mar-2020
^^^^^^^^^^^^^^

See work journal.
(Navigator)

FAL estate work.


Wed 4-Mar-2020
^^^^^^^^^^^^^^

See work journal.
(Navigator)

Continued migration of MIDOSS repos:
* salishseashihan
* midoss-mohid
* ubc-week-mar19
* wwatch3-cmd:
  * subscribe to notifications in #ssc-repos channel
  * change readthedocs webhook
    * application/json
    * Leave the Secrets field blank
    * select individual events: Branch or tag creation, Branch or tag deletion, and Pushes
  * replace .hgignore with .gitignore
  * change env/ to envs/
  * change `pip install` to `python3 -m pip install`
  * move requirements.txt from envs/ to top level; remember to change in comments
  * update copyright year range
  * bump version to 20.1.dev0
  * **failed to update dev env to Python 3.8 due to conda pkg conflicts**
  * add github-actions incoming webhook app to MIDOSS #soiled channel
  * add SLACK_WEBHOOK_URL secret to repo on GitHub
  * add CODECOV_TOKEN secret to repo on GitHub
  * add CI workflow; remember to delete Python from environment-test.yaml
  * update badges and text in README and contributing
(MIDOSS)

Discovered that wwatch3 runs failed in forecast2 on 3-Mar.
(SalishSeaCast)


Thu 5-Mar-2020
^^^^^^^^^^^^^^

wwatch3/forecast2/03mar20 failure is due to stuck make_ww3_wind_file worker.
Discovered automation mess:
* ValueError due to time dimension values from make_plots fvcom that had been running all night
* collect_weather 00 never finished
    2020-03-04 19:55:41,980 [ERROR] Unexpected error: [Errno 110] Connection timed out
    2020-03-04 19:55:52,149 [ERROR] Unexpected error: [Errno 32] Broken pipe
    ...
    2020-03-04 20:57:40,286 [INFO] heartbeat. Sarracenia version is: 2.20.02b1

    2020-03-04 20:57:40,286 [INFO] hb_memory cpu_times user=2334.92 system=254.64 elapse=26111210.2
    2020-03-04 20:57:40,286 [INFO] hb_memory, current usage: 52.3 MiB trigger restart if increases past: 154.1 MiB
    2020-03-04 20:57:40,286 [INFO] hb_pulse message_count 1774786 publish_count 0
    2020-03-04 20:57:40,291 [WARNING] hb_pulse no pulse, and no connection... reconnecting
    2020-03-04 20:57:40,291 [ERROR] Unexpected error: [SSL: BAD_LENGTH] bad length (_ssl.c:2457)
    2020-03-04 20:57:40,291 [ERROR] Unexpected error: [SSL: BAD_LENGTH] bad length (_ssl.c:2457)
    2020-03-04 20:57:40,291 [ERROR] Unexpected error: [SSL: BAD_LENGTH] bad length (_ssl.c:2457)
    2020-03-04 20:57:40,292 [ERROR] Unexpected error: [SSL: BAD_LENGTH] bad length (_ssl.c:2457)
    2020-03-04 20:57:40,292 [ERROR] Unexpected error: [SSL: BAD_LENGTH] bad length (_ssl.c:2457)
    2020-03-04 20:57:40,292 [INFO] AMQP  broker(dd.weather.gc.ca) user(anonymous) vhost()
    2020-03-04 20:57:40,292 [INFO] Using amqp module (AMQP 0-9-1)
    2020-03-04 20:57:40,932 [INFO] Binding queue q_anonymous.sr_subscribe.hrdps-west.74434425.78671301 with key v02.post.model_hrdps.west.grib2.# from exchange xpublic on broker amqps://anonymous@dd.weather.gc.ca
    2020-03-04 20:57:41,234 [INFO] reading from to anonymous@dd.weather.gc.ca, exchange: xpublic
    2020-03-04 20:57:41,367 [INFO] report_back to anonymous@dd.weather.gc.ca, exchange: xs_anonymous
    2020-03-04 20:57:41,367 [INFO] hb_retry on_heartbeat
    2020-03-04 20:57:41,367 [INFO] sr_retry on_heartbeat
    2020-03-04 20:57:41,379 [INFO] No retry in list
    2020-03-04 20:57:41,382 [INFO] sr_retry on_heartbeat elapse 0.014716
  recovery:
    mv /results/forcing/atmospheric/GEM2.5/GRIB/20200305/00 /results/forcing/atmospheric/GEM2.5/GRIB/20200305/00.aside
    pkill -f collect_weather
    download_weather 00 2.5km
    download_weather 06 2.5km
    rm -rf /results/forcing/atmospheric/GEM2.5/GRIB/20200305/00.aside
    rm -rf /SalishSeaCast/datamart/hrdps-west/06/*
    rm -rf /SalishSeaCast/datamart/hrdps-west/12/*
    wait for forecast2 runs to complete
    download_weather 12 2.5km
    collect_weather 18 2.5km
* wwatch3 recovery:
    arbutus: pkill -f make_ww3_wind_file
    launch_remote_worker arbutus.cloud-nowcast make_ww3_wind_file "arbutus.cloud-nowcast forecast --run-date 2020-03-03"
    had some trouble with left over race condition management
    launch_remote_worker arbutus.cloud-nowcast make_ww3_current_file "arbutus.cloud-nowcast forecast --run-date 2020-03-03"
    launch_remote_worker arbutus.cloud-nowcast make_ww3_wind_file "arbutus.cloud-nowcast forecast --run-date 2020-03-04"
    launch_remote_worker arbutus.cloud-nowcast make_ww3_current_file "arbutus.cloud-nowcast forecast --run-date 2020-03-04"
    launch_remote_worker arbutus.cloud-nowcast make_ww3_wind_file "arbutus.cloud-nowcast forecast --run-date 2020-03-05"
    launch_remote_worker arbutus.cloud-nowcast make_ww3_current_file "arbutus.cloud-nowcast forecast --run-date 2020-03-05"
(SalishSeaCast)

See work journal.
(Navigator)


Fri 6-Mar-2020
^^^^^^^^^^^^^^

Continued migration of MIDOSS repos:
* MIDOSS-MOHID-grid
  * subscribe to notifications in #soiled channel
* MIDOSS-MOHID-CODE
  * subscribe to notifications in #soiled channel
  * replace .hgignore with .gitignore
* Make-MIDOSS-Forcing
  * subscribe to notifications in #soiled channel
  * replace .hgignore with .gitignore
  * change readthedocs webhook
    * application/json
    * Leave the Secrets field blank
    * select individual events: Branch or tag creation, Branch or tag deletion, and Pushes
  * rename env/ to envs/
  * change pip install to python3 -m pip install
  * update pkgs & versions in recent dev env
  * move requirements.txt to top level dir
  * update README and dev docs re: migration to GitHub
(MIDOSS)

Zoom mtg w/ Yvonne Coady & Derek Jacoby at uVic re: 3D viz of SalishSeaCast.
(Prediction Core)

Mtg w/ Tiffany re: pytest.


Sat 7-Mar-2020
^^^^^^^^^^^^^^

Continued migration of MIDOSS repos:
* MIDOSS-MOHID-config failed; sent support request msg to GitHub; response was that it is unclear from logs what the problem is
Updated MOHID-Cmd code & docs re: repos migrated to GitHub.
(MIDOSS)

Explored merge conflict resolution in `git pull --rebase` context in work journal:
  git pull --rebase
  # merge conflict
  git mergetool --tool kdiff3
  # resolve conflicts
  git rebase --continue
Can set kdiff3 as default merge tool on kudu with:
  git config --global merge.tools kdiff3
Added section to MOAD VCS migration doc.


Sun 8-Mar-2020
^^^^^^^^^^^^^^

See work journal.
(Navigator)


Week 11
-------

Mon 9-Mar-2020
^^^^^^^^^^^^^^

Re-familiarized myself with `mohid monte-carlo` sub-command in prep for session this afternoon w/ Rachael & Vicky.
Continued migration of MIDOSS repos:
* mohid-cmd:
  * subscribe to notifications in #ssc-repos channel
  * change readthedocs webhook
    * application/json
    * Leave the Secrets field blank
    * select individual events: Branch or tag creation, Branch or tag deletion, and Pushes
  * add SLACK_WEBHOOK_URL secret to repo on GitHub
  * add CODECOV_TOKEN secret to repo on GitHub
  * replace .hgignore with .gitignore
  * move requirements.txt from envs/ to top level; remember to change in comments
  * **failed to update dev env to Python 3.8 due to conda pkg conflicts**
  * add CI workflow; remember to delete Python from environment-test.yaml
  * update badges and text in README and contributing
(MIDOSS)

UBC-IOS modelling collaboration mtg:
* UBC: Susan, Elise, Doug
* IOS: Laura, Maxim
* Elise presented her Ocean Sciences talk
(Prediction Core)

MOAD team mtg; see whiteboard.
(MOAD)

Vancouver to Nanaimo


Tue 10-Mar-2020
^^^^^^^^^^^^^^^

Nanaimo

See work journal.
(Navigator)

SoPO mtg:
* pull temperature and salinty time series for Departure Bay and Chrome Island lighthouse locations to compare w/ Peter Chandler time series
(SalishSeaCast)


Wed 11-Mar-2020
^^^^^^^^^^^^^^^

Nanaimo

Started migration of SalishSeaCast repos:
* SalishSeaWaves
* NEMO-3.1
* CONCEPTS-110
* NEMO-EastCoast
* SoG-Obs
* NEMO-3.4-Code
* NEMO-Forcing; has 13 large files (1 mesh mask, 12 initial T&S) that we have to decide how to handle
SoPO mtg; see hand-written notes.
(SalishSeaCast)

Finished MOHID-Cmd docs updates re: VCS migration.
(MIDOSS)

Vancouver to Nanaimo


Thu 12-Mar-2020
^^^^^^^^^^^^^^^

See work journal.
(Navigator)

Built new Python 3.8 dev env for SalishSeaNowcast on kudu.
Updated psutil version on skookum and arbutus re: dependabot security alert; conda says that arbutus env is inconsistent.
(SalishSeaCast)

Conjunctivitis


Fri 13-Mar-2020
^^^^^^^^^^^^^^^

See work journal.
(Navigator)

Continued migration of SalishSeaCast repos:
* XIOS-1.0
download_live_ocean failed with an import error; presumed due to psutil update yesterday making env unstable; built a new nowcast-env on skookum:
  cp nowcast-env/etc/conda/activate.d/envvars.sh nowcast-env-envvars.sh
  conda update -n base -c defaults conda
  conda env remove --prefix /SalishSeaCast/nowcast-env
    lots of stale NFS handles messages
  mv nowcast-env nowcast-env-borked
  conda env create \
    --prefix /SalishSeaCast/nowcast-env \
    -f SalishSeaNowcast/envs/environment-prod.yaml
  resulted in a Python 3.8.2 env
  python3 -m pip install -e packages
  cp nowcast-env-envvars.sh nowcast-env/etc/conda/activate.d/envvars.sh
  create nowcast-env/etc/conda/deactivate.d/envars.sh
  deactivate, re-activate & check env
  supervisord --configuration $NOWCAST_CONFIG/supervisord.ini
  download_live_ocean -h is very slow
Built new nowcast-env on arbutus:
  sudo apt update
  sudo apt upgrade
  update clones
  git clone SalishSeaWaves
  cp nowcast-env/etc/conda/activate.d/envvars.sh nowcast-env-envvars.sh
  conda update -n base -c defaults conda
  conda env remove --prefix /nemoShare/MEOPAR/nowcast-sys/nowcast-env
  resulted in a Python 3.8.2 env
  cp nowcast-env-envvars.sh nowcast-env/etc/conda/activate.d/envvars.sh
  create nowcast-env/etc/conda/deactivate.d/envars.sh
  python3 -m pip install -e packages
Restarted automation at ~12:00:
  collect_weather 18 2.5km &
  download_live_ocean
  make_live_ocean_files was very slow
  had to launch run_NEMO and watch_NEMO mnaually on arbutus
  restarted log_aggregator
(SalishSeaCast)


Sat 14-Mar-2020
^^^^^^^^^^^^^^^

Lots of fail at ~09:45; investigation:
* make_plots comparison failed
  * nowcast-dev/13mar20 did not have complete
    * envvars not being set for run_NEMO because I messed up the cp of nowcast-env-envvars, just like I did on arbutus :-(
  * make_forcing_links salish nowcast+ --shared-storage --run-date 2020-03-13
  * make_plots nemo nowcast comparison 2020-03-13
  * make_forcing_links salish-nowcast nowcast+ --shared-storage 2020-03-14
* nowcast-r12 finished too fast
  * because there were no 13mar20 runs, maybe due to envvars.sh file name issue
  * launch_remote_worker arbutus.cloud-nowcast make_fvcom_boundary "arbutus.cloud-nowcast x2 nowcast --run-date 2020-03-13"
  * launch_remote_worker arbutus.cloud-nowcast make_fvcom_boundary "arbutus.cloud-nowcast r12 nowcast --run-date 2020-03-13"
make_fvcom_boundary issued FutureWarning twice:
  /nemoShare/MEOPAR/nowcast-sys/nowcast-env/lib/python3.8/site-packages/pyproj/crs/crs.py:279: FutureWarning: '+init=<authority>:<code>' syntax is deprecated. '<authority>:<code>' is the preferred initialization method. When making the change, be mindful of axis order changes: https://pyproj4.github.io/pyproj/stable/gotchas.html#axis-order-changes-in-proj-6
    projstring = _prepare_from_string(projparams)
Started planning week of 16-Mar (and beyond) VCS migrations:
  salishsea-site
  analysis
  docs
  analysis-nancy
  analysis-sprints
  analysis-michael
  rpn-to-gemlam
  fvcom-cmd
  mestingtools
  sog
  sog-forcing
  sog-initial
  sog-runsets

  analysis-idalia
  analysis-muriel

  private-tools
  xios-arch
  xios-2
  nemo-cmd
  salishseacmd
  grid
  rivers-climatology
  tides
  tracers
  nemo-3.6-code
  tools
  ss-run-sets
(SalishSeaCast)


Sun 15-Mar-2020
^^^^^^^^^^^^^^^

fvcom backfilling:
  * launch_remote_worker arbutus.cloud-nowcast make_fvcom_boundary "arbutus.cloud-nowcast x2 nowcast --run-date 2020-03-14"
  * launch_remote_worker arbutus.cloud-nowcast make_fvcom_boundary "arbutus.cloud-nowcast r12 nowcast --run-date 2020-03-14"
(SalishSeaCast)


Week 12
-------

Mon 16-Mar-2020
^^^^^^^^^^^^^^^

First day of official UBC work-from-home due to COVID-19

See work journal.
(Navigator)

MOAD team mtg; see whiteboard.
(MOAD)

fvcom backfilling:
  * launch_remote_worker arbutus.cloud-nowcast make_fvcom_boundary "arbutus.cloud-nowcast x2 nowcast --run-date 2020-03-15"
  * launch_remote_worker arbutus.cloud-nowcast make_fvcom_boundary "arbutus.cloud-nowcast r12 nowcast --run-date 2020-03-15"
  * nowcast to forecast chaining fails because run-date is not passed from watch_fvcom to make_fvcom_boundary
  * launch_remote_worker arbutus.cloud-nowcast make_fvcom_boundary "arbutus.cloud-nowcast x2 forecast --run-date 2020-03-15"
Sent email re: this week's SalishSeaCast VCS migration plan.
nowcast-agrif backfilling:
* 10mar20 run completed successfully, but wasn't downloaded
* 11mar20 upload_forcing failed
* download_results orcinus nowcast-agrif 2020-03-10
* upload_forcing orcinus nowcast+ 2020-03-11
* upload_forcing orcinus turbidity 2020-03-11 --debug
* make_forcing_links orcinus nowcast-agrif 2020-03-11
(SalishSeaCast)


Tue 17-Mar-2020
^^^^^^^^^^^^^^^

fvcom backfilling:
  * launch_remote_worker arbutus.cloud-nowcast make_fvcom_boundary "arbutus.cloud-nowcast x2 nowcast --run-date 2020-03-16"
  * launch_remote_worker arbutus.cloud-nowcast make_fvcom_boundary "arbutus.cloud-nowcast r12 nowcast --run-date 2020-03-16"
  * launch_remote_worker arbutus.cloud-nowcast make_fvcom_boundary "arbutus.cloud-nowcast r12 nowcast --run-date 2020-03-17"
  * r12 caught up
nowcast-agrif backfilling:
* 12mar20 run failed due to InfiniBand issue; retried:
* make_forcing_links orcinus nowcast-agrif 2020-03-12
* make_forcing_links orcinus nowcast-agrif 2020-03-13
* make_forcing_links orcinus nowcast-agrif 2020-03-14
* make_forcing_links orcinus nowcast-agrif 2020-03-15
* make_forcing_links orcinus nowcast-agrif 2020-03-16
* make_forcing_links orcinus nowcast-agrif 2020-03-17
Continued migration of SalishSeaCast repos:
* tides:
  * subscribe in #ssc-repos
  * clone to skookum, arbutus, orcinus, optimum
  * arbutus: checkout -b PROD-nowcast-green-201905
  * optimum: checkout -b PROD-hindcast_201905-v3
  * update run_NEMO
  * update docs/repos_organization
  * update SalishSeaNowcast/docs
  * update SS-run-sets/v201905/hindcast/optimum_hindcast_template.yaml
  * deploy SalishSeaNowcast to skookum, arbutus
(SalishSeaCast)

See work journal.
(Navigator)


Wed 18-Mar-2020
^^^^^^^^^^^^^^^

collect_weather 00 didn't finish:
* investigation:
    2020-03-17 20:18:19,156 [ERROR] Unexpected error: [Errno 110] Connection timed out
    2020-03-17 20:18:19,168 [ERROR] Unexpected error: [Errno 32] Broken pipe
    ...
    2020-03-17 20:26:29,853 [ERROR] Unexpected error: [Errno 32] Broken pipe
    2020-03-17 20:26:39,863 [INFO] heartbeat. Sarracenia version is: 2.20.02b1
    2020-03-17 20:26:39,863 [INFO] hb_memory cpu_times user=372.85 system=40.37 elapse=27228949.78
    2020-03-17 20:26:39,863 [INFO] hb_memory, current usage: 51.8 MiB trigger restart if increases past: 148.5 MiB
    2020-03-17 20:26:39,863 [INFO] hb_pulse message_count 284284 publish_count 0
    2020-03-17 20:26:39,900 [WARNING] hb_pulse no pulse, and no connection... reconnecting
    2020-03-17 20:26:39,900 [ERROR] Unexpected error: [SSL: BAD_LENGTH] bad length (_ssl.c:2457)
    2020-03-17 20:26:39,900 [ERROR] Unexpected error: [SSL: BAD_LENGTH] bad length (_ssl.c:2457)
    2020-03-17 20:26:39,900 [ERROR] Unexpected error: [SSL: BAD_LENGTH] bad length (_ssl.c:2457)
    2020-03-17 20:26:39,900 [ERROR] Unexpected error: [SSL: BAD_LENGTH] bad length (_ssl.c:2457)
    2020-03-17 20:26:39,901 [ERROR] Unexpected error: [SSL: BAD_LENGTH] bad length (_ssl.c:2457)
    2020-03-17 20:26:39,905 [INFO] AMQP  broker(dd.weather.gc.ca) user(anonymous) vhost()
    2020-03-17 20:26:39,905 [INFO] Using amqp module (AMQP 0-9-1)
    2020-03-17 20:26:40,782 [INFO] Binding queue q_anonymous.sr_subscribe.hrdps-west.74434425.78671301 with key v02.post.model_hrdps.west.grib2.# from exchange xpublic on broker amqps://anonymous@dd.weather.gc.ca
    2020-03-17 20:26:41,172 [INFO] reading from to anonymous@dd.weather.gc.ca, exchange: xpublic
    2020-03-17 20:26:41,356 [INFO] report_back to anonymous@dd.weather.gc.ca, exchange: xs_anonymous
    2020-03-17 20:26:41,356 [INFO] hb_retry on_heartbeat
    2020-03-17 20:26:41,356 [INFO] sr_retry on_heartbeat
    2020-03-17 20:26:41,363 [INFO] No retry in list
    2020-03-17 20:26:41,366 [INFO] sr_retry on_heartbeat elapse 0.009733
    2020-03-17 20:30:16,889 [INFO] file_log downloaded to: /SalishSeaCast/datamart/hrdps-west/00/022/CMC_hrdps_west_TCDC_SFC_0_ps2.5km_2020031800_P022-00.grib2
* recovery:
    mv /results/forcing/atmospheric/GEM2.5/GRIB/20200318/00 /results/forcing/atmospheric/GEM2.5/GRIB/20200318/00.aside
    pkill -f collect_weather
    download_weather 00 2.5km
    download_weather 06 2.5km
    rm -rf /results/forcing/atmospheric/GEM2.5/GRIB/20200318/00.aside
    rm -rf /SalishSeaCast/datamart/hrdps-west/06/*
    wait for forecast2 runs to complete
    download_weather 12 2.5km
    rm -rf /SalishSeaCast/datamart/hrdps-west/12/*
    collect_weather 18 2.5km
fvcom backfilling:
  * launch_remote_worker arbutus.cloud-nowcast make_fvcom_boundary "arbutus.cloud-nowcast x2 nowcast --run-date 2020-03-17"
Discovered that NEMO-Cmd Git VCS recording feature does not handle detached HEAD state that results from checking out a tag; solution is to create a branch when checking out the tag; e.g.
  git checkout -b PROD-nowcast-green-201905 PROD-nowcast-green-201905
(SalishSeaCast)


Thu 19-Mar-2020
^^^^^^^^^^^^^^^

See work journal.
(Navigator)

fvcom backfilling:
  * launch_remote_worker arbutus.cloud-nowcast make_fvcom_boundary "arbutus.cloud-nowcast x2 nowcast --run-date 2020-03-18"
  * launch_remote_worker arbutus.cloud-nowcast make_fvcom_boundary "arbutus.cloud-nowcast x2 nowcast --run-date 2020-03-19"
(SalishSeaCast)


Fri 20-Mar-2020
^^^^^^^^^^^^^^^

Continued migration of SalishSeaCast repos:
* XIOS-ARCH:
  * subscribe in #ssc-repos
  * update run_NEMO
  * update SalishSeaNowcast/docs
  * update UBC-MOAD/docs
  * update SalishSeaCast/docs/repos_organization & quickstart
  * skookum:
    * git clone
    * git pull SalishSeaNowcast
  * arbutus:
    * git clone
    * checkout -b PROD-nowcast-green-201905 PROD-nowcast-green-201905
    * git pull SalishSeaNowcast
  * orcinus:
    * git clone
  * update SS-run-sets/v201905/hindcast/optimum_hindcast_template.yaml
  * optimum:
    * git clone
    * checkout -b PROD-hindcast_201905-v3 PROD-hindcast_201905-v3
nowcast-agrif backfilling:
* 19mar20 didn't time step due to missing forcing
* upload_forcing orcinus nowcast+ 2020-03-19
* upload_forcing orcinus turbidity 2020-03-19 --debug
* fix orcinus:~/nowcast-agrif-sys/runs/nowcast-agrif_template.yaml re: tides and XIOS-ARCH from GitHub
* fix orcinus env:
  * module load python/3.5.0
  * module unload python/2.7.3
  * ~/hg-stable/hg
  * update and re-install NEMO-Cmd from:
      changeset:   575:7c4c47e63ff3
      tag:         tip
      user:        Doug Latornell <dlatornell@eoas.ubc.ca>
      date:        Fri Aug 03 22:01:43 2018 -0400
      summary:     Move lib.load_run_desc() into prepare module & delete lib module.
    to:
      changeset:   626:1e9cdfbbe270
      tag:         tip
      user:        Doug Latornell <djl@douglatornell.ca>
      date:        Wed Jan 08 15:23:42 2020 -0800
      summary:     Rename env/ to envs/
  * python3 -m pip install --user -e NEMO-Cmd
  * update and re-install SalishSeaCmd from:
      changeset:   614:d365dffaec8a
      tag:         tip
      user:        Doug Latornell <dlatornell@eoas.ubc.ca>
      date:        Fri Aug 03 22:08:10 2018 -0400
      summary:     Refactor to use prepare.load_run_desc() from NEMO-Cmd pkg.
    to:
      changeset:   724:3b45c2c9435a
      tag:         tip
      user:        Doug Latornell <dlatornell@eoas.ubc.ca>
      date:        Wed Jan 08 15:32:04 2020 -0800
      summary:     Rename env/ to envs/
  * python3 -m pip install --user -e SalishSeaCmd
  * hacked /home/dlatorne/.local/lib/python3.5/site-packages/hglib/__init__.py to set HGPATH = '/home/dlatorne/hg-stable/hg'
* make_forcing_links orcinus nowcast-agrif 2020-03-19
* make_forcing_links orcinus nowcast-agrif 2020-03-20
(SalishSeaCast)

1st MOAD pub-on-Skype


Sat 21-Mar-2020
^^^^^^^^^^^^^^^

collect_weather 12 didn't finish due to broken pipe and bad SSL length errors:
* recovery:
    pkill -f collect_weather
    collect_weather 18 2.5km
    mv /results/forcing/atmospheric/GEM2.5/GRIB/20200321/12 /results/forcing/atmospheric/GEM2.5/GRIB/20200321/12.aside
    download_weather 12 2.5km
    rm -rf /results/forcing/atmospheric/GEM2.5/GRIB/20200321/12.aside
    rm -rf /SalishSeaCast/datamart/hrdps-west/12/*
Fixed Path to str conversion issues in NEMO-Cmd that cropped up in yesterday's orcinus thrash.
(SalishSeaCast)


Sun 22-Mar-2020
^^^^^^^^^^^^^^^

See work journal.
(Navigator)


Week 13
-------

Mon 23-Mar-2020
^^^^^^^^^^^^^^^

Week 2 of UBC work-from-home due to COVID-19

Sent email re: VCS migration plan for week of 23-Mar; continue SalishSeaCast migrations that didn't get finished last week.
Continued migration of SalishSeaCast repos:
* analysis-jie
* NEMO-Cmd
  * subscribe in #ssc-repos
  * subscribe in #soiled
  * subscribe in 43ravens#gomss
* migrate issues:
  * use kudu /media/doug/warehouse/bitbucket-issue-migration clone of https://github.com/jeffwidman/bitbucket-issue-migration and bitbucket-issue-migration conda env
    * python3 -m migrate salishsea/nemo-cmd SalishSeaCast/NEMO-Cmd douglatornell
      * use GitHub personal access token instead of GitHub password
  * failed on issue #22 of #25; manually migrated issues 22-25
(SalishSeaCast)

MOAD group skype mtg; see whiteboard.
(MOAD)

See work journal.
(Navigator)


Tue 24-Mar-2020
^^^^^^^^^^^^^^^

See work journal.
(Navigator)

Slack product demo webinar; waste of time sales pitch.

Monthly team mtg on Skype.
Helped Rachael w/ Python package installation issues on graham after migration to Git clones.
(MIDOSS)

Continued migration of SalishSeaCast repos:
* NEMO-Cmd
  * change readthedocs webhook
    * application/json
    * Leave the Secrets field blank
    * select individual events: Branch or tag creation, Branch or tag deletion, and Pushes
(SalishSeaCast)


Wed 25-Mar-2020
^^^^^^^^^^^^^^^

See work journal.
(Navigator)

Email discussion about multiple NEMO configs and NEMO-Cmd option for executable mgmt w/ Birgit.
(Arctic)

Continued migration of SalishSeaCast repos:
* NEMO-Cmd
  * update run_NEMO
  * update SalishSeaNowcast/docs
  * update salishsea/docs/repos_organization & quickstarts
  * update MIDOSS/docs
  * add SLACK_SALISHSEACAST_WEBHOOK_URL secret to repo on GitHub
  * add SLACK_MIDOSS_WEBHOOK_URL secret to repo on GitHub
  * add CODECOV_TOKEN secret to repo on GitHub
  * replace .hgignore with .gitignore
  * update dev env and requirements.txt
  * move requirements.txt from envs/ to top level; remember to change in comments
  * add CI workflow; remember to delete Python from environment-test.yaml
  * update badges and text in README and contributing
  * update CHANGES.rst issue URLs
  * skookum:
    * git clone
    * git pull SalishSeaNowcast
  * arbutus:
    * git clone
    * git pull SalishSeaNowcast
  * orcinus:
    * git clone
    * update runs/nowcast-agrif_template.yaml
  * update SS-run-sets/v201905/hindcast_long/optimum_hindcast_template.yaml
  * optimum:
    * git clone
    * git pull SS-run-sets
(SalishSeaCast)


Thu 26-Mar-2020
^^^^^^^^^^^^^^^

Emails to Johannes and Mike C re: repos migrated to GitHub.
(43ravens)

Email to Ben and discussion w/ Susan of consolidation of 201905 files on /results2.
(ERDDAP)

See work journal.
(Navigator)

Continued migration of SalishSeaCast repos:
* grid
  * ncks -4 -L4 deflate 2 large files
  * subscribe in #ssc-repos
  * update copyright year range
  * add license badge
  * update run_NEMO
  * update SalishSeaNowcast/docs
  * update salishsea/docs/repos_organization & quickstarts
  * skookum:
    * git clone
    * git pull SalishSeaNowcast
  * arbutus:
    * git clone
    * checkout -b PROD-nowcast-green-201905 PROD-nowcast-green-201905
    * git pull SalishSeaNowcast
  * orcinus:
    * git clone
    * update runs/nowcast-agrif_template.yaml
  * update SS-run-sets/v201905/hindcast/optimum_hindcast_template.yaml
  * optimum:
    * git clone
    * checkout -b PROD-hindcast_201905-v3 PROD-hindcast_201905-v3
    * git pull SS-run-sets
Dropped Python 3.5 from CI for NEMO-Cmd because I used a lot of pathlib fixtures in the test suite.
Fixed issues in SalishSeaCmd that cropped up in 20-Mar-2020 orcinus thrash:
* module load git
* module load python/3.5.0
* change to use 12 processors/node
Gave up on FileNotFoundError that gets raised by pathlib.resolve; seems to be either a bug in pathlib, or a bug in orcinus file system.
Researched adding python-hglib to conda-forge.
(SalishSeaCast)


Fri 27-Mar-2020
^^^^^^^^^^^^^^^

See work journal.
(Navigator)

Helped Rachael sort out NEMO-Cmd VCS recording issue.
(MIDOSS)

MOAD pub-on-Skype


Sat 28-Mar-2020
^^^^^^^^^^^^^^^

See work journal.
(Navigator)

Did 1st pass on income tax returns.

Received news of Amica White Rock overnight staff member who tested positive for COVID-19.


Sun 29-Mar-2020
^^^^^^^^^^^^^^^

Continued migration of SalishSeaCast repos:
* docs
  * subscribe to notifications in #ssc-repos channel
  * change readthedocs webhook
    * application/json
    * Leave the Secrets field blank
    * select individual events: Branch or tag creation, Branch or tag deletion, and Pushes
  * update environment-rtd.yaml
  * update readthedoc.yml file to schema 2.0
  * update SalishSeaNowcast/docs
  * update salishsea/docs/repos_organization
  * update contributors list URL:
    * SalishSeaNowcast
    * FVCOM-Cmd
    * NEMO-Cmd
    * rpn-to-gemlam
    * SalishSeaCmd
    * tools
* rivers-climatology
  * subscribe in #ssc-repos
  * update copyright year range
  * add license badge
  * update SalishSeaCast contributors list URL
  * update run_NEMO
  * update SalishSeaNowcast/docs
  * update salishsea/docs/repos_organization & quickstarts
  * skookum:
    * git clone
    * git pull SalishSeaNowcast
  * arbutus:
    * git clone
    * checkout -b PROD-nowcast-green-201905 PROD-nowcast-green-201905
    * git pull SalishSeaNowcast
  * orcinus:
    * git clone
    * update runs/nowcast-agrif_template.yaml
  * update SS-run-sets/v201905/hindcast/optimum_hindcast_template.yaml
  * optimum:
    * git clone
    * checkout -b PROD-hindcast_201905-v3 PROD-hindcast_201905-v3
    * hg pull SS-run-sets
Fixed contributors list URLs in:
* MOHID-Cmd
* moad_tools


April
=====

Week 14
-------

Mon 30-Mar-2020
^^^^^^^^^^^^^^^

Week 3 of UBC work-from-home due to COVID-19

Discovered that nowcast-agrif failed due to problem finding 1_BS_rivers-climatology/bio/rivers_bio_tracers_mean.nc; I guess the rivers_bio_tracers_mean.nc files were never committed; found notes about their creation on 14-May-2018; re-created them with:
  cd rivers-climatology/bio
  /bin/ls | grep rivers_bio_tracers_'m..d..'.nc | ncra -4 -o ../subgrids/BaynesSound/bio/rivers_bio_tracers_mean.nc
Changed orcinus deployment to make runs/nowcast-agrif_template.yaml a symlink to SS-run-sets/v201702/smelt-agrif/orcinus_nowcast_template.yaml
Launched nowcast-agrif/30mar20 with:
  make_forcing_links orcinus-nowcast-agrif nowcast-agrif --run-date 2020-03-30
Cleaned up leftovers that caused the mess:
* update SS-run-sets/v201702/smelt-agrif/orcinus_nowcast_template.yaml re: repos from GitHub
* add symlinking runs/nowcast-agrif_template.yaml from SS-run-sets/v201702/smelt-agrif/orcinus_nowcast_template.yaml to deplyment docs
* add creation of rivers-climatology/subgrids/BaynesSound/bio/rivers_bio_tracers_mean.nc to deployment docs
* commit rivers-climatology/subgrids/BaynesSound/bio/rivers_bio_tracers_mean.nc
(SalishSeaCast)

See work journal.
(Navigator)

MOAD group mtg; see whiteboard.
(MOAD)


Tue 31-Mar-2020
^^^^^^^^^^^^^^^

See work journal.
(Navigator)

Telcon re: coastal flooding and wwatch3:
* Devon Telford, others
* Will provide link for data stream from OPP buoys in SoG & English Bay
Telcon w/ Doug Hrynyk at Cdn Wildlife Service re: GIS injest from ERDDAP.
(Prediction Core)

FAL estate work.

Disabled v18-12 datasets.
Added testOutOfDate=now+24hours attr to a rolling forecast datasets.
Updated index page re: removal of 18-05 datasets.
Copied setup.xml file into /opt/tomcat/content/erddap/ and bounced ERDDAP with:
* sudo /opt/tomcat/bin/shutdown.sh
* sudo /opt/tomcat/bin/startup.sh
Added ubcSSg3DAuxiliaryFields1hV19-05 dataset.
(ERDDAP)


Wed 1-Apr-2020
^^^^^^^^^^^^^^

See work journal.
(Resilient-C)

See work journal.
(Navigator)

Emailed Jamie McLean @ECCC re: RSS feed & out-of-date page for monitoring wwatch3 runs completion.
(SalishSeaCast)


Thu 2-Apr-2020
^^^^^^^^^^^^^^

See work journal.
(Resilient-C)

See work journal.
(Navigator)

(SalishSeaCast)


Fri 3-Apr-2020
^^^^^^^^^^^^^^

See work journal.
(Resilient-C)

See work journal.
(Navigator)

Continued migration of SalishSeaCast repos:
* tracers
  * decided with Susan what to do about large files in initial/
    * deflated and committed initial/winter2017_201702.nc and initial/summer2016_201702.nc
    * cloned from Bitbucket to /ocean/sallen/hg_repos/SalishSeaCast-tracers to preserve initial/201905/ restart files that are already deflated and still too large
    * Added initial/201905/README to explain where large restart files are preserved
  * subscribe in #ssc-repos
  * update copyright year range
  * add license badge
  * update SalishSeaCast contributors list URL
  * change to SalishSeaCast branding
  * update run_NEMO
  * update salishsea/docs/repos_organization & quickstarts
  * update SalishSeaNowcast/docs
  * skookum:
    * git clone
    * git pull SalishSeaNowcast
  * arbutus:
    * git clone
    * checkout -b PROD-nowcast-green-201905 PROD-nowcast-green-201905
    * git pull SalishSeaNowcast
  * update SS-run-sets/v201702/smelt-agrif/orcinus_nowcast_template.yaml
  * update SS-run-sets/v201905/hindcast/optimum_hindcast_template.yaml
  * orcinus:
    * git clone
    * hg pull SS-run-sets
  * optimum:
    * git clone
    * checkout -b PROD-hindcast_201905-v3 PROD-hindcast_201905-v3
    * hg pull SS-run-sets
Maintenance on SalishSeaNowcast:
* add --debug flag to run_nemo_agrif `salishsea run` command
* stop collecting obs from ONC USDDL CTD; node went out of service again on 22-Dec-2019; ETA for return to service is unknown
* started work on update to use sentry-sdk instead of raven
  * installed sentry-sdk=0.14.3 skookum:nowcast-env
(SalishSeaCast)


Sat 4-Apr-2020
^^^^^^^^^^^^^^

Played Minecraft w/ Susan **all day** :-)


Sun 5-Apr-2020
^^^^^^^^^^^^^^

collect_weather 06 didn't finish:
* investigation:
  2020-04-05 02:23:58,313 [INFO] file_log downloaded to: /SalishSeaCast/datamart/hrdps-west/06/010/CMC_hrdps_west_PRATE_SFC_0_ps2.5km_2020040506_P010-00.grib2
  2020-04-05 02:28:59,590 [ERROR] Download failed https://dd4.weather.gc.ca//model_hrdps/west/grib2/06/010/CMC_hrdps_west_APCP_SFC_0_ps2.5km_2020040506_P010-00.grib2
  2020-04-05 02:28:59,671 [WARNING] downloading again, attempt 2
  2020-04-05 02:29:00,669 [INFO] file_log downloaded to: /SalishSeaCast/datamart/hrdps-west/06/010/CMC_hrdps_west_APCP_SFC_0_ps2.5km_2020040506_P010-00.grib2
  2020-04-05 02:29:00,670 [INFO] heartbeat. Sarracenia version is: 2.20.02b1
  2020-04-05 02:29:00,670 [INFO] hb_memory cpu_times user=1958.48 system=220.96 elapse=28805890.59
  2020-04-05 02:29:00,670 [INFO] hb_memory, current usage: 53.4 MiB trigger restart if increases past: 148.5 MiB
  2020-04-05 02:29:00,670 [INFO] hb_pulse message_count 1486002 publish_count 0
  2020-04-05 02:29:00,670 [INFO] hb_retry on_heartbeat
  2020-04-05 02:29:00,670 [INFO] sr_retry on_heartbeat
  2020-04-05 02:29:00,681 [INFO] No retry in list
  2020-04-05 02:29:00,685 [INFO] sr_retry on_heartbeat elapse 0.013830
  2020-04-05 02:29:00,819 [ERROR] sr_amqp/consume: could not consume in queue q_anonymous.sr_subscribe.hrdps-west.74434425.78671301: Basic.get: (404) NOT_FOUND - no queue 'q_anonymous.sr_subscribe.hrdps-west.74434425.78671301' in vhost '/'
  2020-04-05 02:29:01,422 [INFO] Using amqp module (AMQP 0-9-1)
  2020-04-05 02:29:15,190 [INFO] file_log downloaded to: /SalishSeaCast/datamart/hrdps-west/06/018/CMC_hrdps_west_APCP_SFC_0_ps2.5km_2020040506_P018-00.grib2
* recovery:
    mv /results/forcing/atmospheric/GEM2.5/GRIB/20200405/06 /results/forcing/atmospheric/GEM2.5/GRIB/20200405/06.aside
    pkill -f collect_weather
    download_weather 06 2.5km
    rm -rf /results/forcing/atmospheric/GEM2.5/GRIB/202000405/06.aside
    rm -rf /SalishSeaCast/datamart/hrdps-west/06/*
    wait for forecast2 runs to complete
    collect_weather 18 2.5km
    download_weather 12 2.5km
    rm -rf /SalishSeaCast/datamart/hrdps-west/12/*
Deployed Friday's SalishSeaNowcast maint changes to skookum (because I forgot to do so on Friday).
nowcast-x2 failed on launch; recover:
  launch_remote_worker arbutus.cloud-nowcast make_fvcom_boundary "arbutus.cloud-nowcast x2 nowcast --run-date 2020-04-05"
(SalishSeaCast)


Week 15
-------

Mon 6-Apr-2020
^^^^^^^^^^^^^^

Week 4 of UBC work-from-home due to COVID-19

See work journal.
(Navigator)

Wrote 6-Apr VCS migration email to group.
Continued migration of SalishSeaCast repos:
* SalishSeaCmd
  * subscribe in #ssc-repos
  * change readthedocs webhook
    * application/json
    * Leave the Secrets field blank
    * select individual events: Branch or tag creation, Branch or tag deletion, and Pushes
  * add SLACK_WEBHOOK_URL secret to repo on GitHub
  * add CODECOV_TOKEN secret to repo on GitHub
  * migrate issues:
    * use kudu /media/doug/warehouse/bitbucket-issue-migration clone of https://github.com/jeffwidman/bitbucket-issue-migration and bitbucket-issue-migration conda env
      * python3 -m migrate salishsea/salishseacmd SalishSeaCast/SalishSeaCmd douglatornell
        * use GitHub personal access token instead of GitHub password
  * update run_NEMO
  * update SalishSeaNowcast/.github/workflows/pytest-coverage.yaml
  * update SalishSeaNowcast/docs
  * update salishsea/docs/repos_organization & quickstarts
  * kudu:
    * mv SalishSeaCmd hg/SalishSeaCmd.hg
    * git clone SalishSeaCmd
    * rsync -rltv ../hg/SalishSeaCmd.hg/.idea ./
    * rm .idea/vcs.xml
    * git config --local user.email "dlatornell@eoas.ubc.ca"
    * ln -s ~/dotfiles/ubuntu/kudu/githooks/generic/rescuetime_commit_highlight.sh .git/hooks/post-commit
    * ln -s ~/dotfiles/ubuntu/kudu/githooks/generic/pre-commit-hook.sh
    * tweak PyCharm commit dialog settings
  * replace .hgignore with .gitignore
  * git push to confirm that slack and readthedocs webhooks are working
  * update dev env and requirements.txt
  * move requirements.txt from envs/ to top level; remember to change in comments
  * add CI workflow; remember to delete Python from environment-test.yaml
  * delete Bitbucket pipelines CI configuration
  * update badges and text in README and development
  * run linkcheck and fix broken links in docs
  * skookum:
    * git clone
    * pip install -e SalishSeaCmd
    * git pull SalishSeaNowcast
  * arbutus:
    * git clone
    * pip install -e SalishSeaCmd
    * git pull SalishSeaNowcast
  * update SS-run-sets/201702/smelt-agrif/orcinus_nowcast_template.yaml
  * update SS-run-sets/v201905/hindcast_long/optimum_hindcast_template.yaml
  * orcinus:
    * git clone
    * pip install -e SalishSeaCmd
    * hg pull SS-run-sets
  * optimum:
    * git clone
    * pip install -e SalishSeaCmd
    * hg pull SS-run-sets
(SalishSeaCast)

Weekly group mtg; see whiteboard.
(MOAD)

Vicky Do & Trent Suzuki gave phys ocgy seminars on their term's work on MIDOSS and SoG climatology.


Tue 7-Apr-2020
^^^^^^^^^^^^^^

See work journal.
(Navigator)

forecast2 failed to rebuild its restart file
nowcast failed to rebuild its restart file; investigation
* I forgot to pip install after cloning SalishSeaCmd from GitHub
* recover:
  * pip install -e SalishSeaNowcast on all platforms
  * arbutus:
    * cd runs/06apr20forecast2_2020-04-07T025754.995579-0700
    * salishsea combine 06apr20forecast2.yaml
    * salishsea gather /nemoShare/MEOPAR/SalishSea/forecast2/06apr20/
    * cd runs/07apr20nowcast_2020-04-07T090321.278406-0700
    * salishsea combine 07apr20nowcast.yaml
    * salishsea gather /nemoShare/MEOPAR/SalishSea/nowcast/07apr20/
  * skookum:
    * download_results arbutus nowcast 2020-04-07
    * launch_remote_worker arbutus run_NEMO "arbutus forecast 2020-04-07"
    * launch_remote_worker arbutus make_fvcom_boundary "arbutus x2 nowcast 2020-04-07"
    * launch_remote_worker arbutus make_fvcom_boundary "arbutus 12 nowcast 2020-04-07"
Stopped forcing uploads to beluga & cedar, and cleaned up unit test references to them.
Restart manager to get  drop of USDDL CTD, and uploads to beluga and cedar to take affect.
Continued migration of SalishSeaCast repos:
* mdunphy/nestingtools
  * subscribe in #ssc-repos
  * update SalishSeaNowcast/docs
(SalishSeaCast)
^^^^^^^^^^^^^^

See work journal.
(Resilient-C)


Wed 8-Apr-2020
^^^^^^^^^^^^^^

Re-pro photoed on my phone prints from Aunt Grace of Jenna & Gareth.
Processed photo of Susan & Jenna on Highline waslk in NYC from May-2019.
Sent photos to Jenna for her 21st bday.

Migrated douglatornell/borg-bkup repo to GitHub.

See work journal.
(Resilient-C)

Continued work on update to use sentry-sdk instead of raven.
(SalishSeaCast)

Video chat w/ NZ Latornells for Jenna's 21st bday.


Thu 9-Apr-2020
^^^^^^^^^^^^^^

Updated to PyCharm 2020.1; learned of Ctrl-Shft-i for quick file view.

Reviewed Make-MIDOSS-Forcing code in prep for working with Vicky to integrate her stats module into it, and integrate both into `mohid monte-carlo`.
MOHID-Cmd code maintenance.
Updated MIDOSS working env on graham re: git clones:
* clones are in ~/project/dlatorne/MIDOSS
* clones state:
    * MIDOSS-MOHID-CODE:
        changeset:   59:f5b4515eed53
        tag:         sensitivity_tests
        user:        Shihan
        date:        Sun Dec 01 23:00:22 2019 -0400
        summary:     Fixed bug in oil dissolution when component percentage is zero
    * MIDOSS-MOHID-config:
        changeset:   275:42c21b1655c4
        tag:         tip
        user:        Doug Latornell <dlatornell@eoas.ubc.ca>
        date:        Mon Jan 20 17:21:55 2020 -0800
        summary:     Increase limits for AKNS_spatial sensitivity runs
    * moved MIDOSS-MOHID-grid, moad_tools, MOHID-Cmd, NEMO-Cmd to hg/
* git cloned Make-MIDOSS-Forcing, MIDOSS-MOHID-grid, moad_tools, MOHID-Cmd, NEMO-Cmd
* pip install --user -e Make-MIDOSS-Forcing, moad_tools, MOHID-Cmd, NEMO-Cmd
Started adding make-hdf5 to mohid monte-carlo in add-make-hdf5 branch.
Skype w/ Vicky & Rachael re: adding make-hdf5-stats and make-mohid-stats commands to Make-MIDOSS-Forcing repo.
Write docs for make-hdf5 and its YAML file.
(MIDOSS)


Fri 10-Apr-2020
^^^^^^^^^^^^^^^

**Statutory Holiday** - Good Friday

Bike ride around UBC via SW Marine.

Worked on local conversion of MIDOSS-MOHID-config to Git:
  * get the tool
    git clone git@github.com:frej/fast-export.git as /media/doug/waterhouse/hg-fast-export/
  * build conda env to use it in
    conda create -n hg-fast-export python=3 mercurial
    conda activate hg-fast-export
  * local conversion
    cd /tmp
    git init MIDOSS-MOHID-config
    cd MIDOSS-MOHID-config
    /media/doug/waterhouse/hg-fast-export/hg-fast-export.sh -r /media/doug/waterhouse/MIDISS/MIDOSS-MOHID-config
  * prep for push to GitHub (using my user token to authenticate)
    cd /tmp
    git clone --bare MIDOSS-MOHID-config MIDOSS-MOHID-config.bare
    cd MIDOSS-MOHID-config.bare
    git push https://github.com/MIDOSS/MIDOSS-MOHID-config
  * GitHub rejected the push due to large files:
      remote: error: GH001: Large files detected. You may want to try Git Large File Storage - https://git-lfs.github.com.
      remote: error: Trace: 7ac327bed05c2ef5b3c5b9f3dd2e75f8
      remote: error: See http://git.io/iEPt8g for more information.
      remote: error: File test_vvl/currents_west_above2_north_below2.hdf5 is 273.84 MB; this exceeds GitHub's file size limit of 100.00 MB
      remote: error: File test_vvl/constant_waves.hdf5 is 1366.37 MB; this exceeds GitHub's file size limit of 100.00 MB
      remote: error: File test_vvl/e3t.hdf5 is 1352.95 MB; this exceeds GitHub's file size limit of 100.00 MB
  * used git filter-branch to remove 3 large files
      git filter-branch --force --index-filter   "git rm --cached --ignore-unmatch test_vvl/currents_west_above2_north_below2.hdf5"   --prune-empty --tag-name-filter cat -- --all
      git filter-branch --force --index-filter   "git rm --cached --ignore-unmatch test_vvl/constant_waves.hdf5"   --prune-empty --tag-name-filter cat -- --all
      git filter-branch --force --index-filter   "git rm --cached --ignore-unmatch test_vvl/e3t.hdf5"   --prune-empty --tag-name-filter cat -- --all
  * successful push to GitHub
      git push https://github.com/MIDOSS/MIDOSS-MOHID-config
Rachael and Vicky agreed that they have nothing else that needed to be pushed to MIDOSS-MOHID-config on Bitbucket, so the version I migrated to GitHub is official.
(MIDOSS)

make_turbidity_file failed due to inconsistent time stamps:
  ValueError: Anticipated and output hour were consistent: iout=20 ind=20 43929.416666666664 43929.381944444445
recovery:
  symlink 2020-04-09 river_turb forcing file as 2020-04-10
  upload_forcing arbutus turbidity
  upload_forcing orcinus turbidity
  upload_forcing graham turbidity
  upload_forcing optimum turbidity
Continued work on update to use sentry-sdk in SalishSeaNowcast instead of raven.
(SalishSeaCast)


Sat 11-Apr-2020
^^^^^^^^^^^^^^^

**Easter Saturday**

nowcast-blue blew up on launch:
  zonal velocity is larger than 20 m/s
  kt=****** max abs(U):   24.77    , i j k:    46  897    7
investigation & recovery:
  * Susan traced cause to large discrepancy between Neah Bay ssh forecast and observations. Fix is to use forecast ssh for all days instead of obs for present day and forecast thereafter. Done by manual adjustment of symlink for this run.
  * same issue occurred for nowcast-green; same resolution
Updated make_forcing_links unit tests re: production config testing, some changes to use monkeypathc & cap log.
Uploaded to skookum hacked change to use all fcst ssh instead of obs for 1st day then fcst thereafter; started work on unit tests for make_forcing_links._make_NeahBay_ssh_links().
(SalishSeaCast)


Sun 12-Apr-2020
^^^^^^^^^^^^^^^

**Easter Sunday**

Bike ride along River Rd to 8 Rd.

Finished adding unit tests for make_forcing_links._make_NeahBay_ssh_links().
Finalized change to use all fcst ssh instead of obs for 1st day then fcst thereafter.
Rebased feature branch on to clean, up to date master, then pushed.
Helped Susan sort out divergence in SS-run-sets on optimum.
(SalishSeaCast)


Week 16
-------

Mon 13-Apr-2020
^^^^^^^^^^^^^^^

**Statutory Holiday** - Easter Monday

Week 5 of UBC work-from-home due to COVID-19

Rebased and pushed orcinus:SS-run-sets for Susan to get changesets 2649-2655 from a local anonymous branch on to default; prep for her to run 201812 research runs for Elise & Tereza.
Helped Susan change next_workers to suppress download_results after automated runs on optimum.
Continued migration of SalishSeaCast repos:
* salishsea-site
  * subscribe in #ssc-repos
  * change readthedocs webhook
    * application/json
    * Leave the Secrets field blank
    * select individual events: Branch or tag creation, Branch or tag deletion, and Pushes
  * add SLACK_WEBHOOK_URL secret to repo on GitHub
  * add CODECOV_TOKEN secret to repo on GitHub
  * migrate issues:
    * use kudu /media/doug/warehouse/bitbucket-issue-migration clone of https://github.com/jeffwidman/bitbucket-issue-migration and bitbucket-issue-migration conda env
      * python3 -m migrate salishsea/salishsea-site SalishSeaCast/salishsea-site douglatornell
        * use GitHub personal access token instead of GitHub password
  * update SalishSeaNowcast/docs
  * update salishsea/docs/repos_organization & quickstarts
  * kudu:
    * mv salishsea-site hg/salishsea-site.hg
    * git clone salishsea-site
    * rsync -rltv ../hg/salishsea-site.hg/.idea ./
    * rm .idea/vcs.xml
    * git config --local user.email "dlatornell@eoas.ubc.ca"
    * ln -s ~/dotfiles/ubuntu/kudu/githooks/generic/rescuetime_commit_highlight.sh .git/hooks/post-commit
    * ln -s ~/dotfiles/ubuntu/kudu/githooks/generic/pre-commit-hook.sh
    * tweak PyCharm commit dialog settings
  * replace .hgignore with .gitignore
  * git push to confirm that slack and readthedocs webhooks are working
  * update dev env and requirements.txt
  * change env/ to envs/
  * change `pip install` to `python3 -m pip install`
  * move requirements.txt from envs/ to top level; remember to change in comments
  * update copyright year range
  * bump version to 20.1.dev0
  * remove Python version from readthedocs build config
  * add CI workflow; remember to delete Python from environment-test.yaml
(SalishSeaCast)

Finish migration of MIDOSS-MOHID-config:
  * subscribe in #soiled
  * update MIDOSS/docs
  * update MOHID-Cmd
  * clone on kudu
  * clone on graham
(MIDOSS)

MCL & FAL tax court estate work.


Tue 14-Apr-2020
^^^^^^^^^^^^^^^

Sorted out building REBUILD_NEMO on orcinus w/ GCC-8.3 by creating NEMOGCM/ARCH/UBC_EOAS/arch-GCC_OPTIMUM_REBUILD_NEMO.fcm from gcc-8.3.patch file that I had created on 20-May-2019; committed new ARCH file.
Continued migration of SalishSeaCast repos:
* salishsea-site
  * Change to Python 3.8 for dev, prod & test envs
  * update badges and text in README and pkg dev docs
  * run linkcheck and fix broken links in docs
  * skookum:
    * git clone
    * supervisorctl shutdown
    * pip install -e salishsea-site
    * supervisord
(SalishSeaCast)

Continued adding make-hdf5 to mohid monte-carlo in add-make-hdf5 branches in MOHID-Cmd and MIDOSS-MOHID-config.
(MIDOSS)


Wed 15-Apr-2020
^^^^^^^^^^^^^^^

Asked Vicky for csv file to use for functional testing of adding make-hdf5 to mohid monte-carlo.
Cleaned up left over
  replace :kbd:`you_userid` with you GitHub userid,
in docs: Make-MIDOSS-Forcing, MOHID-Cmd, docs & WWatch3-Cmd
(MIDOSS)

Cleaned up left over
  replace :kbd:`you_userid` with you GitHub userid,
in SalishSeaNowcast docs.
Continued migration of SalishSeaCast repos:
* analysis-michael
* analysis-sprints
Worked on fixing update_forecast_datasets re: missing day after wwatch3 forecast3 run; scp-ed fix to production for overnight testing.
(SalishSeaCast)

Cleaned up left over
  replace :kbd:`you_userid` with you GitHub userid,
in docs: cookiecutter-MOAD-pypkg, moad_tools, docs
(MOAD)


Thu 16-Apr-2020
^^^^^^^^^^^^^^^

Confirmed that update_forecast_datasets fix re: missing day after wwatch3 forecast3 run worked in production; emailed Jamie@ECCC; finalized fix.
Changed SalishSeaNowcast package to use and test under only Python 3.8.
Continued migration of SalishSeaCast repos:
* mdunphy/fvcom-cmd
  * subscribe in #ssc-repos
  * update SalishSeaNowcast/.github/workflows/pytest-coverage.yaml
  * update SalishSeaNowcast/docs
  * kudu:
    * mv FVCOM-Cmd hg/FVCOM-Cmd.hg
    * git clone FVCOM-Cmd
    * git config --local user.email "dlatornell@eoas.ubc.ca"
    * ln -s ~/dotfiles/ubuntu/kudu/githooks/generic/rescuetime_commit_highlight.sh .git/hooks/post-commit
  * arbutus:
    * git clone
    * pip install -e FVCOM-Cmd
Tested and updated SalishSeaNowcast dev env instructions re: running test suite.
Removed my Bitbucket password from GitHub secrets for SalishSeaNowcast repo because it is no longer needed to clone FVCOM-Cmd for CI workflow.
Tagged SS-run-sets rev 657cd75d5d95 as PROD-nowcast-green-201905; clean up from 16-Feb transition to 201905 productions, and a bit of a thrash because of crazy long out of sequence merges in the repo from other folks in the group.
Explored cleaning up tags on tags in rivers-climatology, but decided it is best to leave well enough be because Git makes a HUGE deal about how wrong it is to change release (annotated) tags that have been pushed.
Explored changing NEMO_Nowcast to use slotted classes:
* mocks in test suite prevent use for:
  * NowcastManager
  * NextWorker
  * NowcastWorker
* @staticmethod prevents use for Config
Worked on modernizing test_update_forecast_datasets.
(SalishSeaCast)


Fri 17-Apr-2020
^^^^^^^^^^^^^^^

Westgrid Townhall:
* John Longbottom, CEO
  * intro
* Jay Black, NDRIO (digital research infra)
  * another umbrella? ~6mo old
    * ARC
    * data mgmt
    * research software
    * CANARI network
    * supported by cybersecurity & HQP
  * interface to gov of Canada
  * Gail Murphy is on board
  * engagedri.ca
* Patrick Mann, Dir. Ops
  * COVID-19 resource support
    * increase priority (any analyst can do)
    * special allocations (3mo initial via RAC admin)
    * dedicated reservations
  * 2020 RAC
    * 40% compute ask
    * 26% GPU ask
    * 86% storage ask
    * 99% cloud ask
    * almost 50% UBC in west
    * graham is 72% allocated; aim for 80%
    * most GPUs on cedar; > graham and beluga combined
    * 72% project awarded; 103% nearline awarded
  * one 1 person allowed in a data centre at a time
  * cedar upgraded; 37k cores, 192 GPUs
* Alex Razoumov, Training
  * 25-May to 10-Jul summer school (7 wks)
    * single stream
    * 2-3 day parse learning courses
    * pre-recorded and zoom
    * registration in early May

Grocery shopping.

Rescheduled ECCC MSC datamart user seminar to 15-Sep.

See work journal; repo clean-up.
(Ocean Navigator)

Continued adding make-hdf5 to mohid monte-carlo in add-make-hdf5 branches in MOHID-Cmd and MIDOSS-MOHID-config.
(MIDOSS)


Sat 18-Apr-2020
^^^^^^^^^^^^^^^

Grumpy.


Sun 19-Apr-2020
^^^^^^^^^^^^^^^

Continued migration of SalishSeaCast repos:
* private-tools
  * subscribe in #ssc-repos
  * update SalishSeaNowcast/docs
  * update salishsea/docs/repos_organization & quickstarts
  * kudu:
    * mv private-tools hg/private-tools.hg
    * git clone private-tools
    * git config --local user.email "dlatornell@eoas.ubc.ca"
    * ln -s ~/dotfiles/ubuntu/kudu/githooks/generic/rescuetime_commit_highlight.sh .git/hooks/post-commit
  * skookum:
    * git clone
    * mkdir -p /SalishSeaCast/private-tools/grib2/wgrib2/
    * cp --preserve=timestamps \
        /ocean/sallen/allen/research/MEOPAR/private-tools/grib2/wgrib2/wgrib2 \
        /SalishSeaCast/private-tools/grib2/wgrib2/
Update XIOS-ARCH and MOAD/docs to move graham and cedar arch files to COMPUTECANADA/.
Analyzed SS-run-sets, tools & NEMO-3.6-code for migration:
  NEMO-3.6-code hg default has 3 heads; can I strip:
    both are single commits:
      changeset:   297:116f03a9dad8
      user:        Elise Olson <eolson@eos.ubc.ca>
      date:        Mon Mar 14 20:51:17 2016 -0700
      summary:     testing
    (hg glog -r290:300)

      changeset:   625:167addfc9729
      parent:      564:482d695638f7
      user:        Your Name <your_email_address>
      date:        Fri Feb 24 09:49:06 2017 -0800
      summary:     copy SMELT2 to SMELT_carbon
    (hg glog -r560:630)
(SalishSeaCast)


Week 17
-------

Mon 20-Apr-2020
^^^^^^^^^^^^^^^

Week 6 of UBC work-from-home due to COVID-19

See work journal.
(Ocean Navigator)

upload_forcing to orcinus failed due to login node connection issue.
Continued migration of SalishSeaCast repos:
* nemo-forcing
  * resolving large files issue by deflating with ncks -4 -L4 -O:
      grid/mesh_mask_downbyone.nc
      initial_strat/TS_01dec2002.nc
      initial_strat/TS01jul2016DeepSmooth.nc
      initial_strat/TS06jan2016Deep.nc
      initial_strat/TS20mar2016DeepSmooth.nc
      initial_strat/TSApri.nc
      initial_strat/TSforBlastFraser.nc
      initial_strat/TSforDeepenByGridThickness.nc
      initial_strat/TSforDeepenByGridThicknessDec.nc
      initial_strat/TSforDeepHaroBoundary.nc
      initial_strat/TSforextendedFraserRiver.nc
      initial_strat/TSfornorthextendedFraserRiver.nc
      initial_strat/TSforsmoothto033.nc
* rpn-to-gemlam
  * subscribe in #ssc-repos
  * change readthedocs webhook
    * application/json
    * Leave the Secrets field blank
    * select individual events: Branch or tag creation, Branch or tag deletion, and Pushes
  * add SLACK_WEBHOOK_URL secret to repo on GitHub
  * add CODECOV_TOKEN secret to repo on GitHub
  * kudu:
    * mv rpn-to-gemlam hg/rpn-to-gemlam.hg
    * git clone rpn-to-gemlam
    * rsync -rltv ../hg/rpn-to-gemlam.hg/.idea ./
    * rm .idea/vcs.xml
    * git config --local user.email "dlatornell@eoas.ubc.ca"
    * ln -s ~/dotfiles/ubuntu/kudu/githooks/generic/rescuetime_commit_highlight.sh .git/hooks/post-commit
    * ln -s ~/dotfiles/ubuntu/kudu/githooks/generic/pre-commit-hook.sh
    * tweak PyCharm commit dialog settings
  * replace .hgignore with .gitignore
  * git push to confirm that slack and readthedocs webhooks are working
  * update dev env and requirements.txt
  * change env/ to envs/
  * change `pip install` to `python3 -m pip install`
  * move requirements.txt from envs/ to top level; remember to change in comments
  * update copyright year range
  * bump version to 20.1.dev0
  * remove Python version from readthedocs build config
  * salish:
    * git clone
    * pip install
(SalishSeaCast)


Tue 21-Apr-2020
^^^^^^^^^^^^^^^

See work journal.
(Ocean Navigator)

Continued migration of SalishSeaCast repos:
* SS-run-sets
  * subscribe in #ssc-repos
  * kudu:
    * mv SS-run-sets hg/SS-run-sets.hg
    * git clone SS-run-sets
    * git config --local user.email "dlatornell@eoas.ubc.ca"
    * ln -s ~/dotfiles/ubuntu/kudu/githooks/generic/rescuetime_commit_highlight.sh .git/hooks/post-commit
  * update copyright year range
  * add license badge
  * update SalishSeaCast contributors list URL
  * change to SalishSeaCast branding
  * git push to confirm that slack notification works
  * update run_NEMO
  * update SalishSeaNowcast/docs
  * update other docs refs:
      find . -name "*.rst" -not -path "./hg/*" | xargs grep -n "salishsea/ss-run-sets"
      * MOAD/docs
      * docs
      * SalishSeaCmd
  * skookum:
    * git clone
    * git pull SalishSeaNowcast
  * arbutus:
    * git clone
    * checkout -b PROD-nowcast-green-201905 PROD-nowcast-green-201905
    * git pull SalishSeaNowcast
  * update SS-run-sets/v201702/smelt-agrif/orcinus_nowcast_template.yaml
  * update SS-run-sets/v201905/hindcast/optimum_hindcast_template.yaml
  * orcinus:
    * git clone
  * optimum:
    * git clone
Upgraded OS pkgs on arbutus.cloud.
Changed to git from PPA on arbutus.cloud:
  sudo add-apt-repository ppa:git-core/ppa
  sudo apt update
  sudo apt install git
Backfilled nowcast-agrif runs:
* upload_forcing nowcast+ 2020-04-20 --debug
* upload_forcing turbidity 2020-04-20 --debug
* make_forcing_links nowcast-agrif 2020-04-20
* make_forcing_links nowcast-agrif 2020-04-21
(SalishSeaCast)

Risk of Oil Exposure to Marine Birds in the SoG:
* ECCC: Patrick O'hara, Doug Bertram, Ally (Alexandra) King
* birds are extremely sensitive to oil; essentially lethal; so focus on vulnerability (risk of exposure to oil)
* sand lance also matters; important prey for birds
* Rhino Auklet big colony (world's 2nd largest) on Protection Is., WA; feed on sand lance
* Marbled Murrelets nest in old growth forest up to 50 km from ocean
* KDE == Kernel Density ???; sums of rasters divided by areas ??
(MIDOSS)

See biz journal.
(GoMSS Nowcast)

Continued adding make-hdf5 to mohid monte-carlo in add-make-hdf5 branches in MOHID-Cmd and MIDOSS-MOHID-config.
(MIDOSS)


Wed 22-Apr-2020
^^^^^^^^^^^^^^^

**Earth Day**

NEMO forecast2 run failed to launch; I didn't push the SalishSeaNowcast change re: SS-run-sets moving to Git, so it didn't get deployed to arbutus.cloud and skookum; decided w/ Susan to skip forecast2 runs.
Continued migration of SalishSeaCast repos:
* analysis-idalia
* tools
  * subscribe in #ssc-repos
  * change readthedocs webhook
    * application/json
    * Leave the Secrets field blank
    * select individual events: Branch or tag creation, Branch or tag deletion, and Pushes
  * add SLACK_WEBHOOK_URL secret to repo on GitHub
  * add CODECOV_TOKEN secret to repo on GitHub
  * migrate issues:
    * use kudu /media/doug/warehouse/bitbucket-issue-migration clone of https://github.com/jeffwidman/bitbucket-issue-migration and bitbucket-issue-migration conda env
      * python3 -m migrate salishsea/tools SalishSeaCast/tools douglatornell
        * use GitHub personal access token instead of GitHub password
  * update run_NEMO
  * update SalishSeaNowcast/.github/workflows/pytest-coverage.yaml
  * update SalishSeaNowcast/docs
  * update salishsea/docs/repos_organization & quickstarts
  * kudu:
    * mv tools hg/tools.hg
    * git clone tools
    * rsync -rltv ../hg/tools.hg/.idea ./
    * rm .idea/vcs.xml
    * git config --local user.email "dlatornell@eoas.ubc.ca"
    * ln -s ~/dotfiles/ubuntu/kudu/githooks/generic/rescuetime_commit_highlight.sh .git/hooks/post-commit
    * ln -s ~/dotfiles/ubuntu/kudu/githooks/generic/pre-commit-hook.sh
    * tweak PyCharm commit dialog settings
  * replace .hgignore with .gitignore
  * git push to confirm that slack and readthedocs webhooks are working
  * update dev env and requirements.txt
  * move requirements.txt from envs/ to top level; remember to change in comments
  * add CI workflow; remember to delete Python from environment-test.yaml
  * delete Bitbucket pipelines CI configuration
  * update badges and text in README and development
  * run linkcheck and fix broken links in docs
  * skookum:
    * git clone
    * pip install -e tools/SalishSeaTools
    * git pull SalishSeaNowcast
  * arbutus:
    * git clone
    * pip install -e tools/SalishSeaTools
    * git pull SalishSeaNowcast
  * update SS-run-sets/201702/smelt-agrif/orcinus_nowcast_template.yaml ???
  * update SS-run-sets/v201905/hindcast_long/optimum_hindcast_template.yaml
  * optimum: ???
    * git clone
    * pip install -e tools/SalishSeaTools
    * hg pull SS-run-sets
(SalishSeaCast)

Continued adding make-hdf5 to mohid monte-carlo in add-make-hdf5 branches in MOHID-Cmd and MIDOSS-MOHID-config:
* make-hdf5 fails on compute node when it tries to open https://salishsea.eos.ubc.ca/erddap/griddap/ubcSSn3DMeshMaskV17-02
(MIDOSS)


Thu 23-Apr-2020
^^^^^^^^^^^^^^^

See biz journal.
(Ocean Navigator)

Continued migration of SalishSeaCast repos:
* tools
  * subscribe in #ssc-repos
  * change readthedocs webhook
    * application/json
    * Leave the Secrets field blank
    * select individual events: Branch or tag creation, Branch or tag deletion, and Pushes
  * add SLACK_WEBHOOK_URL secret to repo on GitHub
  * add CODECOV_TOKEN secret to repo on GitHub
  * migrate issues:
    * use kudu /media/doug/warehouse/bitbucket-issue-migration clone of https://github.com/jeffwidman/bitbucket-issue-migration and bitbucket-issue-migration conda env
      * python3 -m migrate salishsea/tools SalishSeaCast/tools douglatornell
        * use GitHub personal access token instead of GitHub password
  * update run_NEMO
  * update SalishSeaNowcast/.github/workflows/pytest-coverage.yaml
  * update SalishSeaNowcast/docs
  * update salishsea/docs/repos_organization & quickstarts
  * update rpn-to-gemlam/docs
  * kudu:
    * mv tools hg/tools.hg
    * git clone tools
    * rsync -rltv ../hg/tools.hg/.idea ./
    * rm .idea/vcs.xml
    * git config --local user.email "dlatornell@eoas.ubc.ca"
    * ln -s ~/dotfiles/ubuntu/kudu/githooks/generic/rescuetime_commit_highlight.sh .git/hooks/post-commit
    * tweak PyCharm commit dialog settings
  * replace .hgignore with .gitignore
  * git push to confirm that slack and readthedocs webhooks are working
  * to be continued...
* NEMO-3.6-code
  * subscribe in #ssc-repos
  * to be continued...
(SalishSeaCast)


Fri 24-Apr-2020
^^^^^^^^^^^^^^^

See biz journal.
(Ocean Navigator)

Ocean Navigator team zoom to say farewell to Nabil, James R & Samuel.

Grocery shopping.

Kate called w/ good news re: probate and Dad's estate.

Updated SalishSeaCmd re: NEMO-3.6-code as git clone; thanks to Tereza live-testing
Continued migration of SalishSeaCast repos:
* tools
  * fix readthedocs build
  * update dev env and requirements.txt
  * skookum:
    * git clone
    * pip install -e tools/SalishSeaTools
    * git pull SalishSeaNowcast
    * git pull SalishSeaCmd
  * arbutus:
    * git clone
    * pip install -e tools/SalishSeaTools
    * git pull SalishSeaNowcast
    * git pull SalishSeaCmd
  * optimum:
    * rm -rf ~/SalishSeaCast/hindcast-sys/tools  # unneeded
(SalishSeaCast)


Sat 25-Apr-2020
^^^^^^^^^^^^^^^

Finances, cleaning, walking, minecraft.


Sun 26-Apr-2020
^^^^^^^^^^^^^^^

Discovered that NEMO runs failed yesterday due to premature deployment of SalishSeaCmd with NEMO as git clone; recovery;
* arbutus:
  git checkout -b 9d3aabd back-to-NEMO-hg
* skookum:
  git checkout 9d3aabd  ## detached HEAD state
  make_forcing_links arbutus nowcast+ 2020-04-25
  wait for nowcast-blue to finish
  make_forcing_links arbutus ssh 2020-04-25
  launch_remote_worker arbutus.cloud-nowcast make_fvcom_boundary "arbutus.cloud-nowcast x2 nowcast --run-date 2020-04-25"
  launch_remote_worker arbutus.cloud-nowcast make_fvcom_boundary "arbutus.cloud-nowcast r12 nowcast --run-date 2020-04-25"
  wait for forecast to finish
  download_results forecast --run-date 2020-04-25
  make_forcing_links salish nowcast+ --shared-storage 2020-04-25
  make_turbidity_file --run-date 2020-04-25 --debug
  upload_forcing arbutus turbidity 2020-04-25 --debug
  upload_forcing orcinus turbidity 2020-04-25 --debug
  upload_forcing graham turbidity 2020-04-25 --debug
  upload_forcing optimum turbidity 2020-04-25 --debug
  make_forcing_links orcinus nowcast-agrif 2020-04-25
  make_forcing_links arbutus nowcast-green 2020-04-25
  wait for nowcast-green to finish
  make_forcing_links arbutus nowcast+ 2020-04-26
*  26arp20 fvcom runs tromped on 25apr20, so re-launched the latter
  launch_remote_worker arbutus.cloud-nowcast make_fvcom_boundary "arbutus.cloud-nowcast x2 nowcast --run-date 2020-04-25"
  launch_remote_worker arbutus.cloud-nowcast make_fvcom_boundary "arbutus.cloud-nowcast r12 nowcast --run-date 2020-04-25"
Discovered that most events in Sentry are now attributed to log_aggregator, and a rule I had on the Sentry/Slack integration suppresses those events from being forwarded to Slack, so removed the rule.
Fixed in SalishSeaTools several instances of deprecated Arrow.replace() by replacing them with Arrow.shift().
Continued migration of SalishSeaCast repos:
* NEMO-3.6-code
  * update SalishSeaNowcast/docs
  * update SalishSeaCmd/docs
  * kudu:
    * mv NEMO-3.6-code hg/NEMO-3.6-code.hg
    * git clone NEMO-3.6-code
    * git config --local user.email "dlatornell@eoas.ubc.ca"
    * ln -s ~/dotfiles/ubuntu/kudu/githooks/generic/rescuetime_commit_highlight.sh .git/hooks/post-commit
  * replace .hgignore with .gitignore
  * git push to confirm that slack webhook is working
  * update NEMO-Cmd/docs
  * update salishsea/docs/repos_organization & quickstarts
(SalishSeaCast)


Week 18
-------

Mon 27-Apr-2020
^^^^^^^^^^^^^^^

Week 7 of UBC work-from-home due to COVID-19

See biz journal.
(Ocean Navigator)

MOAD group mtg; see whiteboard.
(MOAD)

Continued recovery from Sat SalishSeaCast pause:
* backfill fvcom:
    launch_remote_worker arbutus.cloud-nowcast make_fvcom_boundary "arbutus.cloud-nowcast x2 nowcast --run-date 2020-04-26"
    launch_remote_worker arbutus.cloud-nowcast make_fvcom_boundary "arbutus.cloud-nowcast r12 nowcast --run-date 2020-04-26"
    launch_remote_worker arbutus.cloud-nowcast make_fvcom_boundary "arbutus.cloud-nowcast x2 nowcast --run-date 2020-04-27"
* backfill wwatch3
    delete bogus results dirs
    launch_remote_worker arbutus.cloud-nowcast make_ww3_current_file "arbutus.cloud-nowcast forecast --run-date 2020-04-25"
    launch_remote_worker arbutus.cloud-nowcast make_ww3_wind_file "arbutus.cloud-nowcast forecast --run-date 2020-04-25"
    launch_remote_worker arbutus.cloud-nowcast make_ww3_current_file "arbutus.cloud-nowcast forecast --run-date 2020-04-26"
    launch_remote_worker arbutus.cloud-nowcast make_ww3_wind_file "arbutus.cloud-nowcast forecast --run-date 2020-04-26"
    launch_remote_worker arbutus.cloud-nowcast make_ww3_current_file "arbutus.cloud-nowcast forecast --run-date 2020-04-27"
    launch_remote_worker arbutus.cloud-nowcast make_ww3_wind_file "arbutus.cloud-nowcast forecast --run-date 2020-04-27"
make_turbidity_file failed due to inconsistent time stamps:
  ValueError: Anticipated and output hour were consistent: iout=12 ind=12 43946.08333333333 43946.04861111111
recovery:
  symlink 2020-04-26 river_turb forcing file as 2020-04-27
  upload_forcing arbutus turbidity
  upload_forcing orcinus turbidity
  upload_forcing graham turbidity
  upload_forcing optimum turbidity
Continued migration of SalishSeaCast repos:
* NEMO-3.6-code
  * arbutus:
    * git clone
    * git checkout -b PROD-nowcast-green-201905 PROD-nowcast-green-201905
    * build SalishSeaCast
    * build SalishSeaCast_blue
    * build REBUILD_NEMO
    * SalishSeaCmd:
      * git checkout master
      * git pull
  * optimum:
    * git clone
    * git checkout fluxes
    * build SalishSeaCast
    * git checkout master
    * build REBUILD_NEMO
        module unload OpenMPI/2.1.6/GCC/SYSTEM
        module load GCC/8.3
        module load OpenMPI/2.1.6/GCC/8.3
        module load ZLIB/1.2/11
        module load use.paustin
        module load HDF5/1.08/20
        module load NETCDF/4.6/1
    * git checkout fluxes
    * SalishSeaCmd:
      * git checkout master
      * git pull
  * orcinus
    * git clone
    * find revision:
        @ | |  changeset:   1243:15480482073d
        | | |  user:        Doug Latornell <djl@douglatornell.ca>
        | | |  date:        Sun Apr 15 10:38:21 2018 -0700
        | | |  summary:     Correct SMELTAGRIF namelist_ref symlink from SHARED to SMELT.
    * git checkout -b PROD-nowcast-agrif-201702 10878811fdfeac8957d638
    * build SMELTAGRIF
    * build REBUILD_NEMO
    * SalishSeaCmd:
      * git checkout master
      * git pull
(SalishSeaCast)

Phys Ocgy seminary by Haley Dosser.


Tue 28-Apr-2020
^^^^^^^^^^^^^^^

See work journal.
(Resilient-C)

See biz journal.
(Ocean Navigator)

Email conversation w/ Birgit about git rm and some NEMO configs she wants to archive.
(MOAD)

Continued recovery from Sat SalishSeaCast pause:
* backfill fvcom:
    launch_remote_worker arbutus.cloud-nowcast make_fvcom_boundary "arbutus.cloud-nowcast r12 nowcast --run-date 2020-04-27"
    launch_remote_worker arbutus.cloud-nowcast make_fvcom_boundary "arbutus.cloud-nowcast r12 nowcast --run-date 2020-04-28"
Continued migration of SalishSeaCast repos:
* NEMO-3.6-code
  * skookum:
    * git clone
    * SalishSeaCmd:
      * git checkout master
      * git pull
  * salish
    * build SalishSeaCast_blue
    * build REBUILD_NEMO
(SalishSeaCast)

Risk of Oil Exposure to Marine Birds in the SoG:
* ECCC: Patrick O'hara, Doug Bertram, Ally (Alexandra) King
* Rachael, Vicky, Cam & Ben presented
* metric of interest for sea birds is presence or absence of oil because they are so sensitive; volume is less important
(MIDOSS)


Wed 29-Apr-2020
^^^^^^^^^^^^^^^

Continued email conversation w/ Birgit about git rm and some NEMO configs she wants to archive.
(MOAD)

See biz journal.
(Ocean Navigator)

Continued adding make-hdf5 to mohid monte-carlo in add-make-hdf5 branches in MOHID-Cmd and MIDOSS-MOHID-config:
(MIDOSS)


Thu 30-Apr-2020
^^^^^^^^^^^^^^^

Worked w/ Susan on trying to get optimum into a state where she can do research runs; stopped when she got blocked nu read-only file system errors.
(SalishSeaCast)

Continued adding make-hdf5 to mohid monte-carlo in add-make-hdf5 branches in MOHID-Cmd and MIDOSS-MOHID-config, and monte-carlo branch in Make-MIDOSS-Forcing;
traced MOHID segfault issue to using wrong version of bathymetry in mohid-run.yaml; got successful Monte Carlo run; started writing docs about mohid monte-carlo operation, and decided to abbreviate them to be of primary use to me rather than more narrative.
(MIDOSS)


Fri 1-May-2020
^^^^^^^^^^^^^^

Finished work on mohid monte-carlo docs.
(MIDOSS)


Sat 2-May-2020
^^^^^^^^^^^^^^

Replaced up some unnecessary Monte Carlo config items with calculations.
(MIDOSS)


Sun 3-May-2020
^^^^^^^^^^^^^^

Goofed off. Video call w/ Julie & Cor. Went for a walk.


May
===

Week 19
-------

Mon 4-May-2020
^^^^^^^^^^^^^^

Week 8 of UBC work-from-home due to COVID-19

Disabled bloomcast cron job for the year.

Started trying to update bloomcast figs to modern matplotlib; discovered that the production conda env is irreproducible now.
(bloomcast)

MOAD group mtg; see whiteboard.
Created UBC-MOAD/PythonNotes repo and SalishSeaCast#moad-python-notes channel; added notebook about f-strings.
(MOAD)

Phys Ocgy seminar by Alexis Kaminski of UW on N. Pacific transition layer


Tue 5-May-2020
^^^^^^^^^^^^^^

Emailed Cameron at DeViser-Grey re: Dad's tax return.

Discovered at ~11:15 that download_weather 12 for 04may failed; investigation:
* hours 001 through 012 seem to have never appeared in the AMQP stream
* 04may 12 and earlier files are gone from datamart
recovery:
* download_weather 18 2.5km --yesterday --debug
* Susan contacted Pramod and learned that he has files
* killed collect_weather 12
* started collect_weather 18
* download_live_ocean 2020-05-04 --debug
* download_live_ocean 2020-05-05 --debug
* Susan arranged to get 04may 001..012 files from Pramod
* Pramod discovered that he didn't have the files either, so it looks like the problem was at MSC
* Susan hacked grib_to_netcdf and created symlinks in /results/forcing/ so that we will use 12 hours from 20200504/06 gribs
* skookum:
    grib_to_netcdf nowcast+ 2020-05-04 --debug
    get_NeahBay_ssh forecast --debug
    make_live_ocean_files 2020-05-04 --debug
    make_live_ocean_files 2020-05-05 --debug
    upload_forcing arbutus nowcast+ 2020-05-04 --debug
    make_forcing_links arbutus nowcast+ 2020-05-04
    upload_forcing orcinus-nowcast-agrif nowcast+ 2020-05-04 --debug
    upload_forcing graham-hindcast nowcast+ 2020-05-04 --debug
    upload_forcing optimum-hindcast nowcast+ 2020-05-04 --debug
    wait for nowcast-blue to finish
    make_forcing_links arbutus ssh 2020-05-04
    wait for forecast to finish
    collect_weather 00 2.5km --backfill --backfill-date 2020-05-05 --debug (as a test)
    make_turbidity_file --run-date 2020-05-04 --debug
    upload_forcing arbutus turbidity 2020-05-04 --debug
    make_forcing_links arbutus nowcast-green 2020-05-04
    upload_forcing orcinus turbidity 2020-05-04 --debug
    make_forcing_links orcinus nowcast-agrif 2020-05-04
    upload_forcing graham turbidity 2020-05-04 --debug
    upload_forcing optimum turbidity 2020-05-04 --debug
    wait for nowcast-green to finish
    wait for ww3 forcing to fail
    wait for nowcast-dev to fail
    collect_weather 06 2.5km --backfill --backfill-date 2020-05-05
    kill collect_weather 12
    wait for forecast2 to finish
    wait for ww3 forcing to finish running from bogus initial conditions
    collect_weather 00 2.5km --backfill --backfill-date 2020-05-05
    kill collect_weather 18
    wait for nowcast-agrif to fail
    upload_forcing orcinus turbidity 2020-05-04 --debug
    make_forcing_links orcinus nowcast-agrif 2020-05-04
    wait for nowcast-agrif to finish
    upload_forcing orcinus turbidity 2020-05-05 --debug
    make_forcing_links orcinus nowcast-agrif 2020-05-05
    wait for nowcast-dev to fail
    make_forcing_links salish nowcast+ --shared-storage 2020-05-04
    wait for nowcast-dev to finish
    make_forcing_links salish nowcast+ --shared-storage 2020-05-05
  * backfill fvcom:
    launch_remote_worker arbutus.cloud-nowcast make_fvcom_boundary "arbutus.cloud-nowcast x2 nowcast --run-date 2020-05-04"
    launch_remote_worker arbutus.cloud-nowcast make_fvcom_boundary "arbutus.cloud-nowcast r12 nowcast --run-date 2020-05-04"
To be continued...
(SalishSeaCast)


Wed 6-May-2020
^^^^^^^^^^^^^^

GitHub Satellite virtual conference
* 09:00 Keynote - Nat Freidman, CEO
  * 50 million users as of 16-Apr
  * +25% issues
  * -4hr time to merge open source PRs
  * +1hr/day on GitHub
  * news:
    * communities:
      * Discussions product
        * community home
        * per-repo forum
        * interconversion w/ issues
        * included in contributions graph
      * code:
        * Code Spaces - Allison Macmillan
          * containerized cloud dev env and VSCode editor in browser
          * includes connection to dotfile repo
          * includes debugger
          * pay-as-you-go
        * security:
          * vulnerabilities increase linerarly w/ LOC
          * need a community powered solution to scale
          * Code Scanning
            * powered by CodeQL semantic analysis tool
            * actions-based
            * free for open source
* 09:40 Stopping vulnerabilities at source - Grey Baker
* 10:10 Saving time w/ GitHub Actions - Tobias Gabriel (CIO Arduino)
  * self-hosted runner on RaspPi and Arduino in factory
* 11:40 Dependency hell - Ivan Pashchenko
* 13:20 Idea to contribution - Sasha Rosenbaum
* 13:50 Ship it w/ GitHub Actions & Pkgs - Chris Patterson
* 14:20 Scaling remote teams - Aditya Mukerjee (Stripe)
* 14:50 Cloud native deployment w/ GitHub Actions & AWS - Christian Weber (AWS)
* 15:50 GitHub at your fingertips - Neha Batra
* 16:50 GitHub & VSCode - Sana Ajani & Burke Holland (Microsoft)
  * GitHub PRs & Issues extension
  * GitHub theme
  * sidebar on right prevents code from jumping when sidebar collapse is toggled
  * theurlist.com/vscode-github
Continue recovery from Monday's SalishSeaCast pause:
* backfill fvcom:
    launch_remote_worker arbutus.cloud-nowcast make_fvcom_boundary "arbutus.cloud-nowcast x2 nowcast --run-date 2020-05-05"
    launch_remote_worker arbutus.cloud-nowcast make_fvcom_boundary "arbutus.cloud-nowcast r12 nowcast --run-date 2020-05-05"
* backfill wwatch3
    wait for ww3 to start/fail
    launch_remote_worker arbutus.cloud-nowcast make_ww3_current_file "arbutus.cloud-nowcast forecast --run-date 2020-05-04"
    launch_remote_worker arbutus.cloud-nowcast make_ww3_wind_file "arbutus.cloud-nowcast forecast --run-date 2020-05-04"
    launch_remote_worker arbutus.cloud-nowcast make_ww3_current_file "arbutus.cloud-nowcast forecast --run-date 2020-05-05"
    launch_remote_worker arbutus.cloud-nowcast make_ww3_wind_file "arbutus.cloud-nowcast forecast --run-date 2020-05-05"
    launch_remote_worker arbutus.cloud-nowcast make_ww3_current_file "arbutus.cloud-nowcast forecast --run-date 2020-05-06"
    launch_remote_worker arbutus.cloud-nowcast make_ww3_wind_file "arbutus.cloud-nowcast forecast --run-date 2020-05-06"
* backfill nowcast-dev:
    wait for nowcast-dev to fail
    make_forcing_links salish nowcast+ --shared-storage 2020-05-05
    make_forcing_links salish nowcast+ --shared-storage 2020-05-06
To be continued...
(SalishSeaCast)

pip 20.1 changes how pip freeze reports some conda installed packages to local file:/// URLS; change to pip list --format=freeze for my requirements.txt maintenance workflow.

Explored Mélanie's geoTIFF issue with a CAA bathymetry file; basemap fails on ortho projection; cartopy suggests a problem in the geoTIFF file structure; did work in notebook in analysis-doug.


Thu 7-May-2020
^^^^^^^^^^^^^^

FAL estate work; telcon w/ Cameron re: taxes:
* copy and drop off T-slips, 2018 return & TD date-of-death valuation
* plan on income flowing to estate trust, not beneficiaries
* CRA certificate of completion?? is optional

Continue recovery from Monday's SalishSeaCast pause:
* backfill fvcom:
    launch_remote_worker arbutus.cloud-nowcast make_fvcom_boundary "arbutus.cloud-nowcast x2 nowcast --run-date 2020-05-06"
    launch_remote_worker arbutus.cloud-nowcast make_fvcom_boundary "arbutus.cloud-nowcast r12 nowcast --run-date 2020-05-06"
    wait for forecast-x2 to finish

    launch_remote_worker arbutus.cloud-nowcast make_fvcom_boundary "arbutus.cloud-nowcast x2 nowcast --run-date 2020-05-07"

    wait for nowcast-r12 to finish
    launch_remote_worker arbutus.cloud-nowcast make_fvcom_boundary "arbutus.cloud-nowcast r12 nowcast --run-date 2020-05-07"
(SalishSeaCast)

See biz journal.
(Ocean Navigator)

Continued trying to update bloomcast figs to modern matplotlib; discovered that the production conda env is irreproducible now:
* colander=1.5.1 is incompatible with Python 3.8
* fixed unit test re: calling pytest fixtures
* fixed Arrow.replace -> Arrow.shift
* fixed yaml.load & .dump to safe_load & safe.dump
* fixed matplotlib.Axes.set_axis_bgcolor to set_facecolor
(bloomcast)


Fri 8-May-2020
^^^^^^^^^^^^^^

wwatch3/forecast2 results didn't download because worker wasn't communicating w/ manager; manually ruan download_wwatch3_results.
Continue recovery from Monday's SalishSeaCast pause:
* backfill fvcom:
    launch_remote_worker arbutus.cloud-nowcast make_fvcom_boundary "arbutus.cloud-nowcast x2 nowcast --run-date 2020-05-07"
    launch_remote_worker arbutus.cloud-nowcast make_fvcom_boundary "arbutus.cloud-nowcast r12 nowcast --run-date 2020-05-07"
    wait for forecast-x2 to finish
    launch_remote_worker arbutus.cloud-nowcast make_fvcom_boundary "arbutus.cloud-nowcast x2 nowcast --run-date 2020-05-08"
(SalishSeaCast)

IOS seminar - CHS Transformation - Michel Breton
* ENC - Electronic Nav Chart
  * S-57 current standard
  * S-101 future standard
  * S-102 bathymetry
  * S-111 surface currents overlay
  * S-104 water levels overlay
* PPU -  Portable Pilot Unit
* Usage = scale band of products
* automate production of paper charts from ENCs; paper charts are still required as backup to ENCs for mariners; not a mimic of traditional paper chart
* gridded products driven by S-100 implementation
* 6 usages in Canada moving to 3; 0.1°, 1°, 4°
* 5 key areas:
  * Kitimat
  * Vancouver Harbour & Fraser River
  * St. Lawerence River Quebec-Montreal
  * St. John NB
  * Port Hawkesbury, Canso Strait
* S-100 sea trials in Korea in Aug-2019; commercial ECDIS
* soft launch of S-102 and S-111 on 21-Jun in Canada
* Fraser Davidson project mgr for dynamic products
* PPUs mfd by SEAiq
  * heat map to show data stream changes in real time

See work journal.
(Resilient-C)

See biz journal.
(Ocean Navigator)

Finished updating bloomcast figs to modern matplotlib:
* set explicit linestyle for axes grid lines; linestyle=(0, (1, 3)), alpha=0.5 to match matplotlib=1.5.3
(bloomcast)


Sat 9-May-2020
^^^^^^^^^^^^^^

Continue recovery from Monday's SalishSeaCast pause:
* backfill fvcom:
    launch_remote_worker arbutus.cloud-nowcast make_fvcom_boundary "arbutus.cloud-nowcast r12 nowcast --run-date 2020-05-08"
    wait for forecast-x2 to finish
    launch_remote_worker arbutus.cloud-nowcast make_fvcom_boundary "arbutus.cloud-nowcast r12 nowcast --run-date 2020-05-09"
(SalishSeaCast)

50km ride to east end of River Rd and back, then toast on the couch.


Sun 10-May-2020
^^^^^^^^^^^^^^^

See work journal.
(Resilient-C)

Continued work on 2019 income tax returns.

Explored latest state of pyproject.toml, setup.cfg, setup.py and pip re: editable installs and entry points.

Walk around the neighbourhood with sore legs.


Week 20
-------

Mon 11-May-2020
^^^^^^^^^^^^^^^

Week 9 of UBC work-from-home due to COVID-19

FAL estate work: copied documents for Cameron; called AST re: acquisition dates for BCE & MFC; need to send requiest w/ death certs & will.

Weekely MOAD mtg; see whiteboard.
(MOAD)

Phys Ocgy seminar by Robert Izet re: estimating net community productivity while underway using del O2/N2 ratio via optode & cas tension device instead of del O2/Ar via mass spec.

Finished and filed 2019 income tax returns.

Answered email from Maxim re: where to find SalishSeaCast results to drive IOS south Salish Sea Model for Apr-2020.
(SalishSeaCast)

Started to experiment w/ Python packaging re: pip, setup.py, setup.cfg, pyproject.toml, etc., but ended up updating cookiecutter-djl-pypkg re: hg on Bitbucket to Git on GitHub.


Tue 12-May-2020
^^^^^^^^^^^^^^^

See work journal.
(Resilient-C)

FAL estate work:
* telcon w/ Kate re: letters of direction to start distribution
* created assets, liabilities & distribution plan spreadsheet
* delivered papers for final tax return to De Viser Gray office for Cameron and emailed him
* emailed spreadsheet to Jamie


Wed 13-May-2020
^^^^^^^^^^^^^^^

Email to Rachael about repo names and issue labels for Monte Carlo.
(MIDOSS)

See work journal.
(Resilient-C)

Continued migration of SalishSeaCast repos:
* XIOS-2
  * subscribe in #ssc-repos
  * kudu:
    * git clone XIOS-2
    * git config --local user.email "dlatornell@eoas.ubc.ca"
    * ln -s ~/dotfiles/ubuntu/kudu/githooks/generic/rescuetime_commit_highlight.sh .git/hooks/post-commit
  * replace .hgignore with .gitignore
  * git push to confirm that slack webhook is working
  * update SalishSeaNowcast/docs
  * update SalishSeaCmd/prepare
  * update salishsea/docs/repos_organization & quickstarts
  * update MOAD docs
  * graham:
    * git clone
    * build XIOS-2
    * build SalishSeaCast
    * SalishSeaCmd:
      * git checkout master
      * git pull
  * arbutus:
    * git clone
    * git checkout -b PROD-nowcast-green-201905 PROD-nowcast-green-201905
    * build XIOS-2
    * clean SalishSeaCast
    * build SalishSeaCast
    * clean SalishSeaCast_blue
    * build SalishSeaCast_blue
    * SalishSeaCmd:
      * git checkout master
      * git pull
(SalishSeaCast)

FAL estate work: video call w/ Jamie re: distribution and liquidation.


Thu 14-May-2020
^^^^^^^^^^^^^^^

Helped Elise w/ git archeology on NEMOGCM/CONFIG/TRACE2/MY_SRC/traadv_tvd.F90.
nowcast-agrif failed with:
  =>> PBS: job killed: node 32 (pod23b4) requested job terminate, 'EOF' (code 1099) - received SISTER_EOF attempting to communicate with sister MOM's
  mpirun: killing job...
re-ran make_forcing_links orcinus nowcast-agrif to try again; emailed Mark; orcinus had failing nodes due to a chiller failure; re-ran after the cluster stabilized
Tried to resolve "index exceeds dimension bounds" IndexError in make_plots fvcom forecast-x2 research by adding delay after ncrcat.
Worked on changing to sentry-sdk; need to init in NEMO_Nowcast modules and manage log message propagation in config, I think; tested by patches on skookum.
(SalishSeaCast)


Fri 15-May-2020
^^^^^^^^^^^^^^^

sentry-sdk test seems to be working
Cleaned up setnry report to get rid of log_aggregator events.
delay after ncrcat does not seem help with "index exceeds dimension bounds" IndexError in make_plots fvcom forecast-x2 research; removed.
Looking at manager stderr log that supervisord maintains lead me to long-standing bug in ping_erddap worker re: weather dataset name; fixed and deployed.
Updated NEMO_Nowcast docs re: change from circus to supervisor for process mgmt.
Continued migration of SalishSeaCast repos:
* XIOS-2
  * orcinus
    * git clone
    * git checkout -b XIOS-2r1066 XIOS-2r1066
    * build XIOS-2
    * clean SMELTAGRIF
    * build SMELTAGRIF
    * SalishSeaCmd:
      * git checkout master
      * git pull

  * skookum:
    * git clone
    * SalishSeaCmd:
      * git checkout master
      * git pull
  * salish
    * git checkout -b ??? ???
    * build XIOS-2
    * clean SalishSeaCast_blue
    * build SalishSeaCast_blue
  * optimum:
    * git clone
    * git checkout -b ??? ???
    * build XIOS-2
    * clean SalishSeaCast
    * build SalishSeaCast
    * git checkout master
    * SalishSeaCmd:
      * git checkout master
      * git pull
(SalishSeaCast)

FAL estate work: telcon w/ Kate to start distribution process. April statement for non-reg acct arrived; updated spreadsheet, did 3 mo trend, and let Jamie know.


Sat 16-May-2020
^^^^^^^^^^^^^^^

FAL estate work: Susan and I arrived at tax strategy for inheritance account and overall assest allocation strategy.

Goofed off.
Walked 6th, Pine, 14th, Balsam loop.


Sun 17-May-2020
^^^^^^^^^^^^^^^

Upgraded niko to Pop_OS! 20.04.

Goofed off.
Walked around The Crescent.


Week 21
-------

Mon 18-May-2020
^^^^^^^^^^^^^^^

Week 10 of UBC work-from-home due to COVID-19

**Statutory Holiday** - Victoria Day

50 km rode to east end of River Rd on north side of Richmond and back; less shattering than last week's ride.


Tue 19-May-2020
^^^^^^^^^^^^^^^

Emailed Sandrine re: zero length files in HRDPS 1km 00 forecast yesterday and today.
Fixed bad key in ping_erddap msg registry config.
Continued migration of SalishSeaCast repos:
* XIOS-2
  * optimum:
    * git clone
    * git checkout -b PROD-hindcast_201905-v3 PROD-hindcast_201905-v3
    * build XIOS-2
    * clean SalishSeaCast
    * build SalishSeaCast
    * SalishSeaCmd:
      * git checkout master
      * git pull
Wrote SalishSeaNowcast optimum deployment docs.
(SalishSeaCast)

Weekly MOAD group mtg; see whiteboard.
(MOAD)

FAL estate work: Apr TFSA statement arrived; started work on unified asset allocation calculation


Wed 20-May-2020
^^^^^^^^^^^^^^^

Fixed more bad keys re: ping_erddap in next_workers module; sigh.
Worked on finalizing sentry-sdk support in NEMO_Nowcast.
(SalishSeaCast)

Monthly project mtg; see whiteboard.
(MIDOSS)

FAL estate work: finished v1 of unified asset allocation calculation


Thu 21-May-2020
^^^^^^^^^^^^^^^

See work journal.
(Resilient-C)

FAL estate work:
* found TD tax pkg and scanned it to Lucy @ De Viser Gray
* email for BCE & MFC ACB to AST

Upgraded kudu to Pop_OS! 20.04; played with tiling window mgr.

Finalized sentry-sdk support in NEMO_Nowcast; committed config file changes for sentry-sdk use in SalishSeaNowcast; uninstalled raven pkg from skookum and arbutus nowcast-env conda envs.
Continued migration of SalishSeaCast repos:
* XIOS-2
  * skookum:
    * git clone
    * SalishSeaCmd:
      * git checkout master
      * git pull
  * salish
    * build XIOS-2
    * clean SalishSeaCast_blue
    * build SalishSeaCast_blue
Started work on updating nowcast-fig-dev docs and fixing more fig issues.
(SalishSeaCast)


Fri 22-May-2020
^^^^^^^^^^^^^^^

orcinus refused ssh connection for upload_forcing nowcast+; re-ran manually.
(SalishSeaCast)

See work journal.
(Resilient-C)


Sat 23-May-2020
^^^^^^^^^^^^^^^

Bike ride to UBC (via Bridgeport) to pick up things from ESB.


Sun 24-May-2020
^^^^^^^^^^^^^^^

House cleaning.


Week 22
-------

Mon 25-May-2020
^^^^^^^^^^^^^^^

Week 11 of UBC work-from-home due to COVID-19

Replied to Racheal's email about code org for stats & CSV generation, and Monte Carlo MOHID post-processing.
Monte Carlo storage is presently 82 M per MOHID run (excluding Tutbulence.hdf5 file); that means that ~1250 runs (uncompressed) will make a 100 GB nearline chunk; however, that also means that 10,000 MOHID runs will occuupy <1TB of storage, so we should be able to download them to /data and not need to use nearline :-)
(MIDOSS)

See work journal.
(Resilient-C)

Phys Ocgy seminar re: coral reefs & internal waves by Scott Bachman of NCAR

Reviewed nearline storage guidelines: target size for chunks is 100 GB.

Started re-write of MEOPAR-docs on-boarding docs as MOAD docs.
(MOAD)


Tue 26-May-2020
^^^^^^^^^^^^^^^

ESB 2nd floor network switch freaked out, killing connection to smelt, char, tyee.

See work journal.
(Resilient-C)

Email from ProServices re: supply arrangement response; see biz journal.
(43ravens)

Continued re-write of MEOPAR-docs on-boarding docs as MOAD docs.
(MOAD)

Continued migrating personal repos from Bitbucket to GitHub:
 * cyclelog, including issues
 * efunds
 * portfolio
 * fun
 * douglatornell.ca

 Decided that make-monte-carlo-csv belongs in moad_tools.midoss namespace.
 (MIDOSS)


Wed 27-May-2020
^^^^^^^^^^^^^^^

Email from PWGSC security re: DOS clearance; see biz journal.
(43ravens)

Changed kudu ssh config to proxy through salish to optimum.
Worked w/ Elise to get SMELT built in NEMO-3.6-code fluxes1812 branch on optimum; GCC-4.4.7 compiler issue re: "NAMELIST attribute conflicts with ALLOCATABLE attribute"; found history of that error in Slack, pointed Elise at it, she ported in Susan's fix, and I got a clean build.
Investigated make_turbidity_file failures: several hours of duplicated observations on 26may, normal flow restored at 17:10; probably an update-Tuesday issue
(SalishSeaCast)

Skype and email w/ Becca to start her on-boarding.

See work journal.
(Resilient-C)

Continued migrating personal repos from Bitbucket to GitHub:
* meopar2017winterschool
* uqar-winter-school

Bike ride to UBC and back.


Thu 28-May-2020
^^^^^^^^^^^^^^^

Pulled SS-run-sets on optimum for Susan & Elise's fluxes1812 runs.
(SalishSeaCast)

See work journal.
(Resilient-C)

Sentry webinar:
* Will Capazolli, Sol'n Engr
* in-app filtering via beforeSend() callback or beforeBreadcrumb
* data flow:
  * rate limiting: set to capture spikes from graphs in app
  * filtering: inbnound or delete & discard
  * data scrubbing:
  * aggregation (fingerprinting):
    * in-app via beforeSend() callback
    * in-app via Sentry.scope
    * sentry.io: merge button, rules (server-side fingerprinting)
* config:
  * project per code-base
  * teams have multiple projects; projects can be shared among teams
  * releases
  * environments; multiple per project
  * deployments
* integrations
* adding custom metadata:
  * tags - transaction id passed from frontend to backend and tagged
  * breadcrumbs
  * extra aka additional data
* discover reports - visualizations across projects


Fri 29-May-2020
^^^^^^^^^^^^^^^

Deleted archived and non-archive results from /results; see Trello board.
Explored footprint of GEMLAM re: putting a copy on graham:/nearline; month-sized tarbals are ~80G; close to the 100G target size.
(SalishSeaCast)

Explored numpy random choices methods.
(MIDOSS)

Updated moad_tools package structure.
Added GitHub Actions CI worflow to moad_tools pkg.
(MOAD)

Started designing script to generate oil spills csv file to drive Monte Carlo; Susan decided that the command name will be random-oil-spills; it will live in moad_tools.midoss.
(MIDOSS)


Sat 30-May-2020
^^^^^^^^^^^^^^^

Started implementation of moad_tools.midoss.random_oil_spills.py.
(MIDOSS)

50km ride to east end of River Rd and back.


Sun 31-May-2020
^^^^^^^^^^^^^^^

Continued implementation of moad_tools.midoss.random_oil_spills.py.
(MIDOSS)


June
====

Week 23
-------

Mon 1-Jun-2020
^^^^^^^^^^^^^^

Week 12 of UBC work-from-home due to COVID-19

Continued implementation of moad_tools.midoss.random_oil_spills.py:
* finished get_date(), n_spills loop, and csv file generation
* wrote docs
(MIDOSS)


Tue 2-Jun-2020
^^^^^^^^^^^^^^

See work journal.
(Resilient-C)

Worked on ProServices and security screening forms.
(see biz journal)


Wed 3-Jun-2020
^^^^^^^^^^^^^^

Continued implementation of moad_tools.midoss.random_oil_spills.py:
* started get_lat_lon_indieces()
* discussed sub-sampling and GeoTIFF points in SalishSeaCast domain issues w/ Susan, then helped her get set up to test/dev moad_tools.midoss.random_oil_spills
(MIDOSS)

Zoom w/ Venessa & Nancy; see biz-journal.
(Ocean Navigator)


Thu 4-Jun-2020
^^^^^^^^^^^^^^

Worked on Pythonification of Rachael's make_cargo_type_dictionary notebook.
(MIDOSS)

See work journal.
(Ocean Navigator)

Worked on security screening forms.
(see biz journal)


Fri 5-Jun-2020
^^^^^^^^^^^^^^

Discussed geotiff water mask algorithm w/ Susan; calculate a boolean mask that can be applied to AIS ship tracks geotiffs to focus selections from them to be from cells that have surface level water in the SalishSeaCast domain.
(MIDOSS)

Worked on FAL estate; answered Cameron's question about BCE ACB.


Sat 6-Jun-2020
^^^^^^^^^^^^^^

Walked to Prince of Wales school, Quilchena Park, and East Blvd.


Sun 7-Jun-2020
^^^^^^^^^^^^^^

collect_weather 12 didn't finish due to broken pipe and bad SSL length errors:
* recovery:
    pkill -f collect_weather
    rm -rf /results/forcing/atmospheric/GEM2.5/GRIB/20200507/12
    download_weather 12 2.5km
    rm -rf /SalishSeaCast/datamart/hrdps-west/12/*
(SalishSeaCast)

Cycled Spanish Banks, UBC, SWM Dr, Fraser River Park, and to the east end of River Rd. (65 km)


Week 24
-------

Mon 8-Jun-2020
^^^^^^^^^^^^^^

Week 13 of UBC work-from-home due to COVID-19

Realized that I forgot to start collect_weather 18 after yesterday's recovery :-(
  download_weather 18 2.5km --debug
  download_weather 00 2.5km --debug
  download_weather 06 2.5km
  collect_weather 18 2.5km
  wait for forecast2 to finish
  download_weather 12 2.5km
Backfilled VHFR figures; figured out that IndexError exceptions when I do that are due to dates/times before the beginning of the NEMO sea surface height rolling forecast dataset on ERDDAP, so suppressed that exception and updated TestTideStnWaterLevel notebook.
Added nc-time-axis as dependency for SalishSeaNowcast; installed it in nowcast-sys env on skookum.
Tried to update sentry-sdk in nowcast-sys env on skookum, but the ripples are huge.
(SalishSeaCast)

Added geotiff-watermask tool.
Worked on cleanup and integration of Susan's changes to random-oil-spills re: using geotiff water mask for get_lat_lon_indieces(), and calculating fraction of vessel capacity that is spilled.
(MIDOSS)


Tue 9-Jun-2020
^^^^^^^^^^^^^^

Weekly group mtg; see whiteboard.
(MOAD)

collect_weather 00 failed last night due to network issues; recover:
  rm -rf /SalishSeaCast/datamart/hrdps-west/00/*
  rm -rf /SalishSeaCast/datamart/hrdps-west/06/*
  rm -rf /SalishSeaCast/datamart/hrdps-west/12/*
  rm -rf /SalishSeaCast/datamart/hrdps-west/18/*
  rm -rf /results/forcing/atmospheric/GEM2.5/GRIB/20200609/00
  download_weather 00 2.5km
  download_weather 06 2.5km
  wait for forecast2 to finish
  download_weather 12 2.5km
Had to try download_live_ocean twice before success late in the afternoo.
(SalishSeaCast)

See work journal.
(Resilient-C)

Continued work on cleanup and integration of Susan's changes to random-oil-spills re: using geotiff water mask for get_lat_lon_indieces(), and calculating fraction of vessel capacity that is spilled.
(MIDOSS)


Wed 10-Jun-2020
^^^^^^^^^^^^^^^

See work journal.
(Resilient-C)

Forgot to launch collect_weather 18 yesterday; recover:
  collect_weather 18 2.5km
  rm -rf /SalishSeaCast/datamart/hrdps-west/18/*
  rm -rf /SalishSeaCast/datamart/hrdps-west/00/*
  rm -rf /SalishSeaCast/datamart/hrdps-west/06/*
  download_weather 18 2.5km
  download_weather 00 2.5km
  download_weather 06 2.5km
  wait for forecast2 to finish
  rm -rf /SalishSeaCast/datamart/hrdps-west/12/*
  download_weather 12 2.5km
forecast run blew up on western boundary; re-tried using restart from nowcast-green and it failed the same way; Susan smoothed nowcast-green restart velocities in the problem region, and runs were successful.
nowcast-dev blew up; Susan smoothed restart as above, and success.
(SalishSeaCast)

Worked on security screening forms.
(see biz journal)

Monthly project mtg; see whiteboard.
(MIDOSS)


Thu 11-Jun-2020
^^^^^^^^^^^^^^^

Backfilled VHFR figures.
HRDPS 12Z forecast is missing 64 files; emailed Sandrine; she replied to thank me for flagging the issue, then to say that file were being re-uploaded at ~14:50; collect_weather 12 started to see them at ~15:20, and got the last of them at
Deleted many Bitbucket repos to set up redirect messages to GitHub repos.
(SalishSeaCast)

See work journal.
(Resilient-C)


Fri 12-Jun-2020
^^^^^^^^^^^^^^^

FAL estate work; check-in email to Kate re: TD RSP acct form, non-reg acct fees, tax return, and LoDs prompt.

See biz journal.
(Ocean Navigator)


Sat 13-Jun-2020
^^^^^^^^^^^^^^^

Minecraft


Sun 14-Jun-2020
^^^^^^^^^^^^^^^

Minecraft


Week 25
-------

Mon 15-Jun-2020
^^^^^^^^^^^^^^^

Week 14 of UBC work-from-home due to COVID-19

Updated Sentry-Slack integration.
(SalishSeaCast)

Weekly group mtg; see whiteboard.
(MOAD)

Phys Ocgy seminar by Stephanie Waterman on her group's Arctic turbulence measurement work.

Finally finished refactoring get_lat_lon_indieces().
(MIDOSS)

UBC network went down for about 1 hr late in the afternoon.


Tue 16-Jun-2020
^^^^^^^^^^^^^^^

Added Rachael's get_vessel_type() to random-oil-spills, and refactored it.
(MIDOSS)

FAL estate work: reviewed final income tax return.


Wed 17-Jun-2020
^^^^^^^^^^^^^^^

FAL estate work: Emailed Cameron w/ questions about return.

Restarted log aggregator due to missing watch_fvcom messages since UBC network downtime on Monday.
Backfilled VHFR figures; discovered that forecast-x2/10jun20 apparently never happened.
Tweaked new Sentry-Slack integration.
(SalishSeaCast)

Continued migrating personal repos from Bitbucket to GitHub:
  ecget -> 43ravens/ECget
  nosy


Thu 18-Jun-2020
^^^^^^^^^^^^^^^

Continued migrating personal repos from Bitbucket to GitHub:
  nosy
    migrated issues
    archived
  sog-bloomcast
  talks
  cv -> CVs
  sadahome.ca
  rdiff_backup
  asyncio-tutorial
  refactor-extractthalweg
  swc-workout-sphinx-rtd-autodoc
  pdb-workout
  swc-nelle-files
  swc-hbridge-files
  raspi_x10
  raspi_x10_config
  randopony
  pyramid_persona_group_auth_demo
  wake.py
  rm1200
Continued migrating 43ravens repos from Bitbucket to GitHub:
  meopar-atm-2019-06-11
  meopeers-2015-06-15
  client-bio
  client-ios
  client-uottawa-espg
  client-nordion
Moved previously migrated private repos from douglatornell to 43ravens:
  43ravens.ca
  client-UBC-SCARP
  biz-journal
  client-NAFC

Helped Rachael understand get_vessel_type() refactoring.
(MIDOSS)

See work journal.
(Resilient-C)

FAL estate work: Email answers & revised return from Cameron.


Fri 19-Jun-2020
^^^^^^^^^^^^^^^

kudu app maint:
* removed Zoom deb; installed Zoom flatpack
* removed Skype snap; installed Skype flatpack

See work journal.
(Resilient-C)

Skype w/ Rachael about Python code style and techniques.
(MIDOSS)


Sat 20-Jun-2020
^^^^^^^^^^^^^^^

collect_weather 12 failed last night due to network issues; recover:
  pkill -f collect_weather
  collect_weather 18 2.5km &
  rm -rf /results/forcing/atmospheric/GEM2.5/GRIB/20200620/12
  download_weather 12 2.5km
(SalishSeaCast)


Sun 21-Jun-2020
^^^^^^^^^^^^^^^

nowcast-agrif failed due to infiniband error; re-tried, and re-failed.
(SalishSeaCast)


Week 26
-------

Mon 22-Jun-2020
^^^^^^^^^^^^^^^

Week 15 of UBC work-from-home due to COVID-19

Removed forecast.201812 from /results re: Susan's request on Trello.
Removed nowcast-agrif.201702/21aug18 through 31may20 after Susan copied them to archive #9 and #10.
Updated storage use deatils card on Trello.
Continued migrating SalishSeaCast repos from Bitbucket to GitHub:
  private-docs
  analysis
    Decided that 2 old unnamed branches on default can be dropped
Added GitHub Actions workflow to run sphinx linkcheck for salishsea-site repo on every push to GitHub; also did NEMO-Cmd.
(SalishSeaCast)

Group mtg; see whiteboard.
(MOAD)

Phys Ocgy seminar by Sam Anderson on deep machine learning and hydrology modeling.


Tue 23-Jun-2020
^^^^^^^^^^^^^^^

Continued migrating SalishSeaCast repos from Bitbucket to GitHub:
  analysis-nancy
    Extra head is a very old commit involved in a merge-boggle. The commit does not appear to have gotten abandoned, so I decided to let the GitHub importer prune it.
Started work on adding docs-linkcheck Action to moad/docs repo; need to handle links to private GitHub repos, either by auth or by exclusion.
(SalishSeaCast)

See work journal.
(Resilient-C)

Email with Cam about getting origin-destination analysis data and script on to storage accessible by salish.
(MIDOSS)


Wed 24-Jun-2020
^^^^^^^^^^^^^^^

Email with Cam about getting origin-destination analysis data and script on to storage accessible by salish.
(MIDOSS)

FAL estate work: re-reviewed final income tax return; emailed Cameron re: flipped proceeds & ACB for FID M/I transactions in Sep & Oct, and sent him signed engagement agreement. Mtg w/ Monica @TD to sign LoDs for liquidation & distribution of TD wealth accounts; got declaration of transmission for retail accounts that requires notarization.

Created electronic signature PNG w/ transparent background. Installed Xjournal++ so that I could use it to apply signature PNG to documents; a lot of hoops to avoid print/sign/photo-scan.

Added GitHub Actions workflow to UBC-MOAD/docs to run Sphinx linkcheck after every push; messed around trying to find a way to handle private repos URLs via GitHub personal access token, but failed and settled for putting them in an ignore-list in conf.py.
(MOAD)


Thu 25-Jun-2020
^^^^^^^^^^^^^^^

FAL estate work:

UBC-DFO modelling collab mtg: Mike Foreman, WCVI circulation model
(SalishSeaCast)

Started work on origin/destination processing using sciprt & CSV from Casey@MEOPAR via Cam; now stored in /data/MIDOSS/origin_destination_analysis/
* read code
* built py27gdal conda env
  * must use defaults channel only
  * poppler<0.62 has to be installed after env build
* script ran for ~2h but I don't know if it finished or got killed by network hangup
(MIDOSS)


Fri 26-Jun-2020
^^^^^^^^^^^^^^^

Re-launched origin-destination analysis
(MIDOSS)

Westgrid townhall:
* cedar April incident - Martin Siegert SFU site lead
  * compromised ~23-Mar early morning
  * crypto-currency mining
  * compromise came on the heels of system upgrade, so upgrade was blamed for reduced performance
  * 00:00 to 06:00 time window of slowdowns detection by a research group was clue that lead to discovery
    * access via compromised user account, probably via password sniffer on desktop/laptop; unknown if
    * battery check cronjob used to start alternate process
    * kernel mod installed by intruder
    * account had elevated privileges on ATLAS servers that export filesystem to all compute nodes
    * gained root by inserting suid-root shell in exported file system
    * apparently a new compromise technique, though crypto-miners are very secretive
    * head nodes were not compromised, but all authorized_keys files were removed as a precaution, and revoked keys of users who had private keys stored on cedar
  * MFA coming
* there was also a security incident on graham - no details
* system access best practices - Scott Baker, UBC
  * unique passwords/secrets
  * generated passwords, not memorized
  * size matters - passphrases
  * only change when necessary, not scheduled
  * haveibeenpwned.com
  * password/secret vault; keypass, but any is better than none
  * private key should never leave system it is generated on
  * Mozilla infosec key mgmt page
  * don't copy/paste code into command-line
  * sign-out
  * encryption at rest, especially on laptops, USB keys
  * proper file permissions
  * delete unnecessary information
  * software updates; vulnerabilities exploited w/i 36h
  * backup & restore proof
  * VPNs
  * MFA
* westgrid associates
* training
  * UBC ARC summer school in August
  * UBC Research Commons in fall workshops

See work journal.
(Resilient-C)

Started adding ubcSSg3DCarbonFields1hV19-05 ERDDAP dataset; confirm:
  variable names
  colour bar ranges
Stopped because Susan wants to wait until Tereza, et al paper is submitted.
Michael started copying 1km HRDPS for May19-May20 to /data.
Delved into ImportError exceptions in OPPTools that have us pinned at 4af96c499cdc49e96a87f999870be1560807d925; missing numpy-indexed package could be added to env, but missing ttide package has to be installed from GitHub clone, and I don't want to go there; hacked a solution by commenting out contents of OPPTools/__init__.py; works because my code imports explicitly to the module level. Updated arbutus & skookum to present master at e87f5e7c77fa05876c6286a4b8c53879dbcd9543.
**This didn't work! See Sat 27-Jun-2020 for the solution that does work.**
(SalishSeaCast)


Sat 27-Jun-2020
^^^^^^^^^^^^^^^

Yesterday's OPPTools work just made a mess of fail by breaking imports within the package - what was I thinking...; recovery (on skookum & arbutus, unless otherwise noted):
  restored commented out imports in OPPTools/__init__.py
  Installed numpy-indexed
  Commented out import of utils.transit_window_analysis in OPPTools/utils/__init__.py to avoid import ttide (that is not packaged and has to be installed from GitHub clone)
(SalishSeaCast)


Sun 28-Jun-2020
^^^^^^^^^^^^^^^

Virtual Robinson Reunion on Zoom.

Power failure affecting ESB at ~14:40 Sat messed things up but good; recovery:
  pkill collect_weather 18
  rm -rf /results/forcing/atmospheric/GEM2.5/GRIB/20200627/18
  download_weather 18 2.5km
  download_weather 00 2.5km
  download_weather 06 2.5km
  collect_weather 18 2.5km
  wait for forecast2 to finish
  download_weather 12 2.5km
(SalishSeaCast)

Cycled River Rd, through cranberry bogs east of CNR, south dyke to east end of Queensborough, and home via River Rd (60km)



personal repos to migrate:

  randopony-tetra
don't migrate:
  markdown-error-log
  meopar2019-atm-asm-notes
  nemo-cmd-pipelines-test
  test_tag_release
  sqlalchemyorg
  pipeline-test
  workout-sphinx
  forecast
  jasper-rebase-test
  contextlib2
  webtest
  virtualenvwrapper-ksh
  sog
  geotraces-nemo-test
  sog-sublime
  sublimetext3-settings
  sublimetext2-settings


Add CI workflows to run linkcheck on docs:
  need sphinx>3.1 in env
  example workflow in salishsea-site repo
  don't forget to add sphinx & sphinx_rtd_theme to environment-test.yaml
  repos todo:
    UBC-MOAD
      moad_tools
      cookiecutter-MOAD-pypkg
    MIDOSS
      MOHID-Cmd
      docs
      WWatch3-Cmd
      Make-MIDOSS-Forcing
    SalishSeaCast
      SalishSeaNowcast
      docs
      tools
      SalishSeaCmd
    43ravens
      NEMO_Nowcast
      ECget


15jun20: check mitigation of "index exceeds dimension bounds" IndexError in make_plots fvcom forecast-x2 research

8-Jun: talk to Rachael and merge add-make-hdf5 branchs into master x3 repos

Fix xarray.open_mfdataset() re: combine FutureWarning in make_ww3_wind_file

Add VCS revision recording to run_fvcom

Update SalishSeaNowcast fig-dev docs

fix SalishSeaTools unit tests

fix old colander dependency in SOG



Fix Pillow security issue in analysis-doug

Add auto-deploy workflow to salishsea-site to replace bitbucket pipeline

Migrate Baynes Sound fig to cartopy


Advise Michael & Maxim of:
  make_fvcom_boundary issued FutureWarning twice:
    /nemoShare/MEOPAR/nowcast-sys/nowcast-env/lib/python3.8/site-packages/pyproj/crs/crs.py:279: FutureWarning: '+init=<authority>:<code>' syntax is deprecated. '<authority>:<code>' is the preferred initialization method. When making the change, be mindful of axis order changes: https://pyproj4.github.io/pyproj/stable/gotchas.html#axis-order-changes-in-proj-6
      projstring = _prepare_from_string(projparams)


TODO:
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
* Delete ubcSSfDepthAvgdCurrents1hV18-06 from ERDDAP on Fri 7-Feb-2020
* Disable ubcSSfDepthAvgdCurrents1hV18-06 on ERDDAP on Fri 31-Jan-2020
* Update bloomcast plots so that we are not tied to matplotlib-1.5.3
* Sort out OPPTools dependencies so that we can run w/ origin/master:HEAD again
