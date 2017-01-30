*****************
2017 Work Journal
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

Mon 2-Jan-2017
^^^^^^^^^^^^^^

Started feeling onset of flu or some other viral infection.

Fixed bugs in NEMO-Cmd deflate and combine modules.
Worked on de-boilerplating SalishSeaNowcast unit tests; issue #6.
(SalishSea)


Tue 3-Jan-2017
^^^^^^^^^^^^^^

Seriously hammered by virus.


Wed 4-Jan-2017
^^^^^^^^^^^^^^

Starting to recover from virus; felt like I had incipient motion sickness for a lot of the day, especially when working on kudu.

Finished de-boilerplating SalishSeaNowcast unit tests; issue #6.
(SalishSea)

See project work journal.
(GOMSS)


Thu 5-Jan-2017
^^^^^^^^^^^^^^

Continuing to recover from virus; incipient motion sickness feeling relented somewhat by the end of the day.

See project work journal.
(GOMSS)

Continued refactoring combine plug-in in NEMO-Cmd.
Re-booted ERDDAP server in response to an email from Marlene@ONC about Java thread errors.
(SalishSea)


Fri 6-Jan-2017
^^^^^^^^^^^^^^

Continuing to recover from virus.

Started testing free tier of rescuetime.com.

See project work journal.
(GOMSS)

Continued refactoring combine plug-in in NEMO-Cmd.
Updated NEMO-3.6, XIOS, etc. on /data on salish, and on orcinus to do test runs of NEMO-Cmd tools.
(SalishSea)


Sat 7-Jan-2017
^^^^^^^^^^^^^^

Continuing to recover from virus.

Tested and debugged on orcinus combine plug-in and integration of combine, deflate, and gather into Salish Sea run script.
Finished refactoring combine plug-in in NEMO-Cmd.
(SalishSea)


Sun 8-Jan-2017
^^^^^^^^^^^^^^

Continuing to recover from virus.

Tested refactored NEMO-Cmd integrated into SalishSeaCmd on orcinus and salish.
Worked on moving west.cloud nowcast to /nemoShare/MEOPAR/:
* Deleted ~/MEOPAR-nfs symlink on nowcast0
* Updated all repo clones in /nemoShare/MEOPAR/nowcast-sys/nemo_nowcast-env/
* Rebuilt XIOS
* Rebuilt NEMO-3.6 at r6770
* Rebuilt rebuild_nemo
* Created /nemoShare/MEOPAR/nowcast-sys/nemo_nowcast-env/etc/conda/activate.d/envvars.sh
* Updated paths in nowcast.yaml
* Successfully uploaded forcing for 07jan18 and 08jan18, make symlinks, and ran nowcast/08jan17.
Pushed integration of NEMO-Cmd into SalishSeaCmd.
Re-ran forecast/08jan17 in /nemoShare/MEOPAR/nowcast-sys via automation.
(SalishSea)


Week 2
------

Mon 9-Jan-2017
^^^^^^^^^^^^^^

forecast2 ran successfully under automation in /nemoShare/ shared storage.
Fixed bug in NEMO-Cmd deflate() API so that it handles file paths as sequences of either Path objects or strings.
Unmounted ~/MEOPAR/ sshfs shared storage on west.cloud.
nowcast ran successfully under automation in /nemoShare/ shared storage:
* 9x19+1 LPE 104 of 105 on 15 VMs w/ 7 slots/VM
* nowcast: 24:51 + 4:20 = 29:19
* forecast: 30:37 + 7:26 = 38:03
Live ocean download failed twice, 1st in automation, 2nd in manual re-run at 16:00.
Phys Ocgy seminar about bio-optical measurements at an aqauculture site by  Justin Belluz (Hakaii Institute).
Helped Giorgio get Ariane running consistently on halibu (atlantis gives weird netcdf errors), and get his analysis repo set up.
Tried to change NEMO-code key in SalishSeaCmd run description to "NEMO code config" but can't happen because the former is required for hg parents.
(SalishSea)


Tue 10-Jan-2017
^^^^^^^^^^^^^^^

Updated nowcast & nowcast-green config record in docs re: move to r6770 and Ceph/NFS shared storage.
Had to build a new salishsea-docs env to get docs to build.
Added `NEMO code config` key to breaking changes docs.
Started changing SalishSeaNowcast to use SalishSeaCmd & NEMO-Cmd.
Salish Sea team mtg; see whiteboard.
(SalishSea)

Telcon w/ Charles Hannah at IOS re: contract to add SoG wave model to nowcast system

Discussed code organization and MPI runs w/ Idalia.
(Canyons)


Wed 11-Jan-2017
^^^^^^^^^^^^^^^

ECget failed to get 2017-01-10 river flow data overnight; patched Fraser & Englishman river flow files w/ persistence values from 2017-01-09, manually ran make_runoff_file worker, manually ran upload_forcing to restart automation for forecast2 run; NEMo run pid detection failed in watch_NEMO.
Investigated mechanism of pid detection failures; might be mitigated by adding some sleep time before line 500 of run_NEMO worker.
(SalishSea)

See project work journal.
(SoG waves)

Tried to follow request of Dave@ubcit to un-install and re-install vmware tools on the VM, but couldn't figure out how to do it, so asked for more help.
(sealinkd)


Thu 12-Jan-2017
^^^^^^^^^^^^^^^

ECget failed to get 2017-01-11 river flow data overnight; patched Fraser & Englishman river flow files w/ persistence values from 2017-01-09, manually ran make_runoff_file worker, manually ran upload_forcing to restart automation for forecast2 run.
Susan thinks that river flow failures are due to outflow wind events causing the gauges to freeze up.
Ran LTIM for DDL node and it worked despite the lack of a deployment separation in early Oct-2016. Reviewed ONC online record for device to determine end of BBL-SG-05 deployment and beginning of BBL-SG-06 and added those data to GETDEPL, then re-ran it and LTIM.
Re-booted ERDDAP server in response to an email from Marlene@ONC about Java thread errors.
Sent email to Reyna@ONC re: status of ADCP data on their ERDDAP; reply is that they are working through an issue w/ ERDDAP devs.
Copied central node data that Lan downloaded into /ocean/dlatorne/MEOPAR/ONC_ADCP/ tree. Ran GETDEPL, updated VIP-14-13 deployment parameters, and ran LTIM.
Successfully tested run_NEMO worker modified to use SalishSeaCmd API on west.cloud; committed and pushed the change, and applied it on west.cloud.
Copied east node data that Lan downloaded into /ocean/dlatorne/MEOPAR/ONC_ADCP/ tree. Added VIP-15-14 deployment parameters, and started running GETDEPL.
Started work on make_live_ocean_files worker.
Attended dept. colloquium: term 2 research carnival.
(SalishSea)


Fri 13-Jan-2017
^^^^^^^^^^^^^^^

ECget failed to get 2017-01-12 river flow data overnight; patched Fraser & Englishman river flow files w/ persistence values from 2017-01-09, manually ran make_runoff_file worker, manually ran upload_forcing to restart automation for forecast2 run.
East node LTIM produced results w/ no date for final 2 deployments; fixed a possible bug in GETDEPL and re-ran it; no difference.
run_NEMO worker that uses SalishSeaCmd API running in production on west.cloud and sailish; recorded rebuild & deflate metrics on whiteboard.
Tested SalishSeaCmd w/ concurrent deflation on orcinus.
Added logging message to NEMO-Cmd deflate sub-command re: max number of concurrent subprocesses.
Added --max-deflate-jobs command-line option to SalishSeaCmd run sub-command.
(SalishSea)

Un-installed and re-install vmware tools (open-vm-tools package) on the VM via apt-get.
Dave@ubcit says that issue is resovled with a work-around, and asked permission to clone VM for further testing.
(sealinkd)

Set up repo on Bitbucket & Sublime Text project on kudu.
Write 2 sentence topic description and emailed it to Marion.
(Winter School)

See project work journal.
(SoG waves)

Started implementation of salishsea-site app bloomcast pages.
(salishsea-site)


Sat 14-Jan-2017
^^^^^^^^^^^^^^^

ECget failed to get 2017-01-13 river flow data overnight; patched Fraser & Englishman river flow files w/ persistence values from 2017-01-09, manually ran make_runoff_file worker, manually ran upload_forcing to restart automation for forecast2 run.
Finished implementation of salishsea-site app bloomcast about page and deployed it.
(salishsea-site)

Discovered that EC wateroffice web site is showing up to date data, so suspect that the problem is another format change in the HTML table that we scrape.
(ECget)


Sun 15-Jan-2017
^^^^^^^^^^^^^^^

ECget failed to get 2017-01-14 river flow data overnight; patched Fraser & Englishman river flow files w/ persistence values from 2017-01-09, manually ran make_runoff_file worker, but missed time window for forecast2 run.
Organized salissea-site app templates to reflect nav bar.
Started implementation of salishsea-site app bloomcast spring_diatoms page.
(salishsea-site)

See project work journal.
(SoG waves)

Set up PyCharm bloomcast project on kudu and updated dev env packages and versions.
(bloomcast)


Week 3
------

Mon 16-Jan-2017
^^^^^^^^^^^^^^^

ECget failed to get 2017-01-15 river flow data overnight; patched Fraser & Englishman river flow files w/ persistence values from 2017-01-09, manually ran make_runoff_file worker, manually ran upload_forcing to restart automation for forecast2 run.
Continued work on make_live_ocean_files worker.
(SalishSea)

Explored real-time river data on EC datamart; CSV files, files updated contain most recent data and back to beginning of day-2, files updated daily containing last 30 days and part of day-1.
Set up ecget dev env on niko.
Stepped through ecget river flow and discovered that the http://wateroffice.ec.gc.ca/report/report_e.html URL is returning 404; fixed it, tagged v0.5, and backfilled Fraser and Englishman files in SOG-Forcing/ECget/ on salish.
(Ecget)

Phys Ocgy seminar by Cindy on Arctic circulation changes.

Discused web frameworks with Cindy and sent her a bunch of links.

Physio appt; arrange next appt if necessary after 6-Mar.


Tue 17-Jan-2017
^^^^^^^^^^^^^^^

Prep for mtg w/ Idalia about organizing her NEMO workspace, and using NEMO-Cmd.
(canyons)

Continued work on make_live_ocean_files worker.
Salish Sea team mtg; see whiteboard.
(SalishSea)


Wed 18-Jan-2017
^^^^^^^^^^^^^^^

Explored rescuetime; tuned categories; figured out how to set up Mercurial hooks to log highlights to rescuetime (see dotfiles/*/hghooks/ directories).
Added rescuetime hg hooks to dotfiles repo and several project repos: conda-recipes, NEMO-Cmd, SalishSeaCmd, GoMSS-NEMO-config

Created issues in NEMO-Cmd and SalishSeaCmd repos to capture outstanding tasks:
* possible --delete-restart option for gather plug-in
* possible --ignore-restart option for combine plug-in
* more flexible namelist_ref linking in prepare plug-ins
Applied Elise's patch to enable more flexible namelist_ref linking in prepare plug-ins to NEMO-Cmd and SalishSeaCmd repos.
(SalishSea)

See project work journal.
(GOMSS)


Thu 19-Jan-2017
^^^^^^^^^^^^^^^

Set up hg commit and tag hooks to log to rescuetime from niko for SalishSeaCmd, NEMO-Cmd, SalishSeaNowcast, tools.
Set up pycharm hg pre-commit hooks to run yapf on niko for SalishSeaCmd and NEMO-Cmd.

Continued work on make_live_ocean_files worker.
Added logging and did refactoring in salishsea_tools LiveOcean_BCs.py and gsw_calls.py modules.
(SalishSea)

Dept colloquium by William Hsieh on data science in environmental sciences.


Fri 20-Jan-2017
^^^^^^^^^^^^^^^

Reviewed backlog of EC datamart email and forwarded CANSIP indices one to Susan.
Explained ONC east node ADCP data gap in Apr-2016 to Rich.
Created a timeline diagram of nowcast and forecast runs to help visualize what parts of the products of each run will be included in the rolling forecast datasets.
Pointed Michael at XIOS arch file for parallel netcdf build on orcinus.
Explored using python-hglib package in NEMO-Cmd to record repo revs.
Buffed NEMO-cmd dev and run description file docs re: tools.SalishSeaCmd origins.
Worked on adding hglib-based vcs revision recording feature to NEMO-Cmd.
(SalishSea)

Filed more of my email backlog in Thunderbird.

Received payment for maintenance invoice.
Updated Stephanie & Jackie on status of Maps page performance issue; UBC IT says it is resolved and has closed the ticket.
(sealinkd)


Sat 21-Jan-2017
^^^^^^^^^^^^^^^

Continued work on adding hglib-based vcs revision recording feature to NEMO-Cmd; expanded it to include notification and recording of untracked changes in repos.
Investigated Python libraries for svn and git revision recording; svn and gitpyhton appear to be the best choices.
Discussed rolling forecast dataset with Susan.
EC was late with 00 weather, so grib_to_netcdf failed; manually re-ran download_weather 00 and grib_to_netcdf nowcast+ to restart automation.
Investigated ONC DDL CTD data failures; salinity appears to have gone bad in Oct and ONC seems to have retroactively expunged it.
(SalishSea)

See project work journal.
(GOMSS)


Sun 22-Jan-2017
^^^^^^^^^^^^^^^

Created SalishSeaNowcast issues #33 and #34 re: get_onc_ctd worker handling of full day of missing data, and need to process temperature before salinity.
Finished NEMO-Cmd hglib-based vcs revision & status recording feature, except for unit tests.
Updated Salish Sea nowcast-vm to eliminate nowcast-v2 (tools repo) environment and fix other provisioning issues; mercurial installation from ppa fails due to upstream packaging issue.
(SalishSea)

See project work journal.
(GOMSS)


Week 4
------

Mon 23-Jan-2017
^^^^^^^^^^^^^^^

watch_NEMO worker unable to find run pid issue happened again; manually ran download_results worker to restart automation.
(SalishSea)

See project work journal.
(GOMSS)

Set up dev env on niko.
Debugged changes in EC climate data download site.
changed URL for EC wateroffice data downloads.
Set up SOG-code, SOG-forcing, and SOG-initial on niko.
Got bloomcast running on niko.
  INFO:bloomcast.ensemble:Predicted earliest bloom date is 2017-02-25
  INFO:bloomcast.ensemble:Earliest bloom date is based on forcing from 1999/2000
  INFO:bloomcast.ensemble:Predicted early bound bloom date is 2017-03-03
  INFO:bloomcast.ensemble:Early bound bloom date is based on forcing from 2004/2005
  INFO:bloomcast.ensemble:Predicted median bloom date is 2017-03-21
  INFO:bloomcast.ensemble:Median bloom date is based on forcing from 2003/2004
  INFO:bloomcast.ensemble:Predicted late bound bloom date is 2017-04-08
  INFO:bloomcast.ensemble:Late bound bloom date is based on forcing from 1987/1988
  INFO:bloomcast.ensemble:Predicted latest bloom date is 2017-04-13
  INFO:bloomcast.ensemble:Latest bloom date is based on forcing from 1998/1999
Created new bloomcast env on salish.
(bloomcast)

Matplotlib 2.0 landed in conda defaults.


Tue 24-Jan-2017
^^^^^^^^^^^^^^^

Finished bloomcast setup on salish, ran it for today w/o result publication, and enabled cron job.
Start work on modifying bloomcast to integrate its results publication into salishsea-site app.
(bloomcast)

Dentist appt.

Final 6h of 12 weather failed to download, so nowcast/forecast & nowcast-green runs delayed; appeared at 13:04; ran download_weather manually to restart automation.
Worked w/ Rich on ONC ADCP data; more tweaks to GETDEPL and LTIM for east & ddl nodes.
Salish Sea team mtg; see whiteboard.
(SalishSea)

See project work journal.
(GOMSS)


Wed 25-Jan-2017
^^^^^^^^^^^^^^^

Finished modifying bloomcast to integrate its results publication into salishsea-site app.
Released bloomcast-3.1 for 2017 daily forecasts.
Set up rescuetime commit & tag hooks on kudu for SoG-bloomcast-ensemble project.
(bloomcast)

Set up rescuetime commit & tag hooks on kudu for salishsea-site project.
Finished implementation of spring_diatoms view in app.
(salishsea-site)

Google Drive spreadsheets stopped working again in Firefox.

Morphed hg commit & tag hooks that push highlights to rescuetime so that they don't have to be repo specific by getting the repo name of the label from `basename $PWD`.


Thu 26-Jan-2017
^^^^^^^^^^^^^^^

First fully automated run of the year :-)
(bloomcast)

Pulled updates for templates re-organization and bloomcast results view into production.
Ported license page to Pyramid app.
(salissea-site)

Changed to use generic hg commit & tag hooks that push highlights to rescuetime on niko.

Reviewed and commented on Idalia's diagram that maps repos and NEMO run descriptions.
(canyons)

Wrote down the iteration on the run description YAML file that Susan and I came up with to handle AGRIF and a few other warts, and emailed Michael to arrange time to discuss it.
Finished east & DDL node ADCP processing from mtg w/ Rich on Tue.
(SalishSea)

See project work journal.
(SoG waves)


Fri 27-Jan-2017
^^^^^^^^^^^^^^^

See project work journal.
(SoG waves)

Westgrid townhall:
* had lots of trouble connecting; eventually got on via Chrome to Vidyo; Firefox to Vidyo didn't work

* bugaboo is having file system problem; 3000 corrupted files will be lost

Cedar
* 100 Gb/s; 2:1 between islands
* home 50Gb/user
* scratch 20Tb, 1M files/user; 100Tb, 10M files/group
* run on scratch, then move files at end of job to project (preferred) or home

Graham
* very similar to Cedar; should be able to move easily between the 2, but allocations are to specific systems
* fewer GPU nodes
* 50 Gb/s infiniband; 8:1 between islands
* poorer interconnect between islands (1024 cores/island)

Migration
* must move off: jasper
* wait for contact from support
* virtualized user test system available in mid-March
* expect very limited resources in April

* 2017 RAC award letters will be sent in early March
* 2017 RAC allocations take effect in mid-April; may slip
* 2017 CC account renewals delayed to May
* 2017 success rate expected to be similar to 2016; 54% of compute

Built custom vidyodesktop pkg via instructions at https://support.vidyocloud.com/hc/en-us/articles/226103528-VidyoDesktop-3-6-3-for-Linux-and-Ubuntu-15-04-and-higher

Pointed Rich at our Fraser & Englishman River daily discharge data streams.
(SalishSea)

Ported site index page to Pyramid app.
(salishsea-site)


Sat 28-Jan-2017
^^^^^^^^^^^^^^^

Started moving nowcast-green runs to west.cloud; successfully completed a manual test run.
(SalishSea)


Sun 29-Jan-2017
^^^^^^^^^^^^^^^

Continued work on moving nowcast-green runs to west.cloud; launched run va manual make_forcing_links after automation crapped out due to a bug; run failed with an io memory allocation error.
(SalishSea)


ToDo
====

* docs re: stdout & stderr on salish
* refactor, unit tests & docs for forcing links checking for NEMO-3.6

* reduce resolution of landing page images for faster load times
* add docs re: sealinkd server-side app framework
* add EduCloud deployment docs

* research_ferries module
* JSON logging use example notebook

* review remaining nosy PRs
