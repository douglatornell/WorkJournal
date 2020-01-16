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
