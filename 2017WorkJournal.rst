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
download_live_ocean worker failed due to no files available.
(SalishSea)


February
========

Week 5
------

Mon 30-Jan-2017
^^^^^^^^^^^^^^^

Merged pyramid branch into default and tagged v2.0.
Replaced catch-all static page view with similar figure server static view.
(salishsea-site)

Changed dates in titles on bloomcast results page to be day after run data date; i.e. so that results from today's run have today's date.
(bloomcast)

Reduced XIOS buffer size for nowcast-green runs on west.cloud and started a new test.
Backfilled 19jan Live Ocean files that were unavailable yesterday.
Re-ran 30jan17 nowcast-green on west.cloud with reduced XIOS buffer size so that run output is complete; downloaded for Susan to compare to salish run results.
(SalishSea)


Tue 31-Jan-2017
^^^^^^^^^^^^^^^

Added `NEMO code config` key to selected run description YAML files.
Updated working env setup docs re: NEMO-Cmd and SalishSeaCmd repos.
Deleted SalishSeaCmd package from tools repo.
Changed tools repo docs to use autodoc mocks for most packages.
Added --no-submit option to salishsea run sub-command.
Salish Sea team mtg; see whiteboard.
(SalishSea)

Reviewed and commented on Idalia's latest iteration of NEMO repos org & YAML file.
Help Idalia try to sort out inability to run commands on salish - very weird; punted to Charles.
(Canyons)


Wed 1-Feb-2017
^^^^^^^^^^^^^^

Susan says that there are significant differences in nowcast-green results between salish and west.cloud, so copied nowcast-green/31jan17 restart files from salish to west.cloud to restart testing.
Diffed namelists, domain, fields & iodef, and everything else I could think of, and summarized in email to Susan.
Emailed Belaid to give back sshfs shared storage.
(SalishSea)

Explored and started implementation of 0mq-based distributed logging.
(NEMO_Nowcast)


Thu 2-Feb-2017
^^^^^^^^^^^^^^

Dentist appt: upper right molar filling, lower right molar contact repair.

Bloomcast failed in cloud fraction data processing.
Rebuilt bloomcast env & pycharm project on niko to try to get debugging working no go :-(
Cloud fraction bug was extension of an edge case we already handle due to Nav Can not reporting weather descriptions at 23:00 when there is no precipitation; problem on 1-Feb was that there was also no observation recorded at 22:00.
(bloomcast)

Added fspath module to SalishSeaCmd to unify interface for Path objects across Python 2.7 to 3.6+.
Explored latest comparison of nowcast-green results from west.cloud and salish w/ Susan, and she gave her blessing for production to switch to west.cloud; committed, pushed and deployed the changes to make it so.
Figured out how to get torque on salish to deliver stdout & stderr files from spool to result directories; wrote docs about it.
Finished and deployed make_live_ocean_files worker.
(SalishSea)


Fri 3-Feb-2017
^^^^^^^^^^^^^^

download_weather failed for 00 forecast overnight; re-ran manually at ~08:00.
Restarted manager to ensure proper loading of next_workers module with make_live_ocean_files worker.
1st nowcast-green production run on west.cloud instead of salish; fixed bug re: missing message types for download_results worker.
1st automated run of make_live_ocean_files worker, after a couple of minor bug fixes.
(SalishSea)

Attended Small Business Info Expo by gov't of Canada to try to learn about setting up a standing offer for DFO clients.

See project work journal.
(SoG waves)

Continued work on 0mq-based distributed logging.
(NEMO_Nowcast)


Sat 4-Feb-2017
^^^^^^^^^^^^^^

Continued work on 0mq-based distributed logging.
(NEMO_Nowcast)

Added nowcast-dev run on salish to automation; initially to test addition of UW Live Ocean T&S boundary conditions for western boundary.
(SalishSea)


Sun 5-Feb-2017
^^^^^^^^^^^^^^

make_runoff_file worker failed due to a config key that Susan added to the worker but not to the production config file.
Tracked down debugging writes that are bloating nowcast-green stdout from 89kb to 51Mb and asked Elise if they can be deleted, or wrapped in a namelist-controlled if-block.
Continued work on 0mq-based distributed logging.
Tested nowcast distributed logging between west.cloud and kudu and skookum; opened ticket to get ports opened between salish and skookum.
Dealt with chaos caused by a config error that made upload_forcing run with salish as a destination; caused forcing files to be overwritten with zero-length versions of themselves.
Checked status of ONC ferry instruments: HB-DB is the only one that has been working since Christmas.
(SalishSea)

Merged open pull requests in hg-novice lesson in prep for next release.
(swc)


Week 6
------

Mon 6-Feb-2017
^^^^^^^^^^^^^^

nowcast-dev/04feb17 ran for only 12h due to a bad assumption in run_NEMO; changed run_NEMO worker to try to get time step from namelist.domain in run prep dir, then fall back to getting it from previous run's namelist_cfg.
Power outage disrupted download_weather 12 run because group sallen couldn't be resolved.
Discussed model results at ONC central node and Boundary Pass monitoring site w/ Rich & Susan.
Got nowcast system running again after power outage ripples; had to rename restart file for nowcast-dev initiation so that it had the spected restart timestep for a 20s timestep run, and change namelist-time so that NEMO ignores the restart file date/time.
(SalishSea)

Upgraded conda root env on niko to Python 3.6.
Built and uploaded Python 3.6 versions of gomss-nowcast channel packages.

Campus-wide(?) power outage from 11:15 to 11:45

Applied yapf to code-base.
Started work on docs.
(salishsea-site)

Attended inaugural Salish Sea Network monthly seminar.


Tue 7-Feb-2017
^^^^^^^^^^^^^^

Worked on generating model results time series at ONC central node and Boundary Pass mooring site for Rich; found that xarray.open_mfdataset() is ~65 times slower than xarray.open_dataset().
Salish Sea team mtg; see whiteboard.
nowcast-dev run w/o Orlanski boundary conditions and 20s time step was successful.
(SalishSea)

Bloomcast run failed, not sure why.
(bloomcast)


Wed 8-Feb-2017
^^^^^^^^^^^^^^

Finished generating model results time series at ONC central node and Boundary Pass mooring site for Rich.
Tweaked nowcast-dev config to run at 40s time step.
Michael profiled the Boundary Pass code and found that the .values attr access in the loop that build the csv lines was a big culprit; chunking x and y also improved things, but not to better than 20% slower than looping over datasets.
Continued work on 0mq-based distributed logging; did some functional tests, started writing unit tests.
Tried to switch nowacst-dev run to 40s timestep, but it ran for 2 days instead of 1.
(SalishSea)

Photographed American Robin the in snow in the front yard bushes.


Thu 9-Feb-2017
^^^^^^^^^^^^^^

Continued work on 0mq-based distributed logging; finished writing unit tests, started writing docs.
Michael and Susan discovered that e1t and e2t are flipped in the Salish Sea coordinates, so the domain aspect ratio has been wrong from that start :-(
Got nowcast-dev back to running w/ 40s timestep for 1 day duration.
(SalishSea)

Helped Idalia get running with nemo prepare.
(Canyons)

Processed photograph of American Robin the in snow in the front yard bushes; got locked out of Flickr account when I tried to upload it.


Fri 10-Feb-2017
^^^^^^^^^^^^^^^

Wrote intro and dev docs, and got them to build on readthedocs.
(salissea-site)

Attended canyons group mtg.
Helped Idalia with nemo combine.
(Canyons)

Met w/ Susan, Michael & Elise to discuss our way forward in light of the SalishSea NEMO coordinates file issue.
Replied to email question from Nancy about what GEM forecasts the nowcast system uses.
(SalishSea)

See project work journal.
(GOMSS)


Sat 11-Feb-2017
^^^^^^^^^^^^^^^

Acted on Susan's discovery that nowcast-blue and nowcast-green can use the same iodef.xml file; rolled back iodef-blue.xml and iodef-green.xml links in run_NEMO to test on nowacst-dev run.
Added closing tags and whitespace to nemo3.6/nowcast/iodef.xml, and created a copy of it as iodef_cloud.xml with the XIOS buffer size set for runs on west.cloud.
Continued work on 0mq-based distributed logging in NEMO_Nowcast.
Discussed w/ Susan how to provide platform-specific PBS directives to planned nemo run sub-command; agreed on YAML file stanza.
Changed SalishSeaNowcast to use distributed logging; not deployed yet.
(SalishSea)


Sun 12-Feb-2017
^^^^^^^^^^^^^^^

Deployed nowcast distributed logging to skookum and west.cloud.
After a minor bump re: config keys for the location of the grib_to_netcdf and get_NeahBay_ssh diagnostic figure image files, it worked well for logs from west.cloud, but not from salish.
A bonus is that the diagnostic figure images are being produced again (see issues #28 and #29); now the salishsea-site app needs to be able to render them.
Also, the wgrib2 debug log messages have started appearing again (see issue #28), but in the nowcast.debug.log rather than in the wgrib2.log file.
Changed west.cloud to use unified iodef_cloud.xml for blue and green runs.
(SalishSea)

Cleaned espresso machine.

Started adding run sub-command to NEMO_Cmd.
Started working through Melanie's new NEMO GYRE proto-docs.
(Canyons)


Week 7
------

Mon 13-Feb-2017
^^^^^^^^^^^^^^^

06 weather download failed; re-ran download_weather 06 manually to restart automation.
forecast2 watch_NEMO worker failed to bind to logging port; had to run download_resutls worker manually to restart automation.
Added SMTP logging handler to log_aggregator config.
Worked on debugging why remote workers are inconsistent in connecting to the PUB ports.
changed SalishSeaCmd prepare to link to ref namelists in CONFIG/config_name/EXP00/ instead of CONFIG/SHARED/.
(SalishSea)

See project work journal.
(GOMSS)

Finished adding run sub-command to NEMO_Cmd.
Continued working through Melanie's new NEMO GYRE proto-docs.
(Canyons)


Tue 14-Feb-2017
^^^^^^^^^^^^^^^

Forgot to take niko's power adapter to UBC w/ me, so worked on discovery for most of the day.

Updated copyright year range in packages:
* NEMO-Cmd
* SalishSeaCmd
* analysis-doug
Debugged watch_NEMO distributed logging failures and found that they are due to prior watch_NEMO instances that don't terminate.
Started work on collecting ONC ferry data for ERDDAP datasets.
SalishSea team mtg; see whiteboard.
(SalishSea)


Wed 15-Feb-2017
^^^^^^^^^^^^^^^

forecast2 failed because upload_forcing couldn't find LiveOcean files for 15/16feb; turns out that's because download_lilve_ocean failed yesterday because python-hglib wasn't installed in nemo-nowcast-env; created symlinks for LiveOcean files and re-ran upload_forcing to get forecast2 run to go; re-ran download_live_ocean to backfill.
I think I got the remote workers distributed logging issues sorted out by changing to use the same port number regardless of the worker's host, and setting an ingress firewall rule on west.cloud.
Changed next_workers so that download_live_ocean worker passes run-date arg value on to make_live_ocean_files worker, otherwise the latter craps out when the former is run to backfill a prior date.
Helped Giorgio with ideas on how to manage stuck ariane jobs from Python.
(SalishSea)

Saw Dr. Dodek at Cityview who diagnosed the lump on my right arm as an actinic keratosis and treated it with cryosurgery.

See project work journal.
(SoG waves)

Helped Idalia straighten out a repo branch, and diagnose 1st use of nemo run.
(Canyons)


Thu 16-Feb-2017
^^^^^^^^^^^^^^^

Wrote CMOS talk idea email to Youyu, Susan, Shilliang & Keith.
(CMOS)

Continued helping Idalia w/ nemo run.
(Canyons)

Changed location of grib_to_netcdf worker monitoring image storage to figures/ and moved it in config so that it doesn't get deleted when log_aggregator is restarted.
Added grib_to_netcdf worker plots image to salishsea-site automation monitoring page.
Explored why watch_NEMO worker for nowcast-green doesn't get an ack from manager; inconclusive.
Helped Giorgio with detecting stuck ariane runs, and cleaning up hg in his analysis repo.
Worked on adding resolved_path() to NEMO-Cmd.
(SalishSea)

Attended CMEM seminar by Peter Ross on microplastics pollution.


Fri 17-Feb-2017
^^^^^^^^^^^^^^^

Bug in Wednesday's change to make next_workers so that download_live_ocean worker passes run-date arg value on to make_live_ocean_files worker, caused the latter to not run yesterday, so upload_forcing for forecast2 failed this morning. Fixed the bug, re-ran make_live_ocean_files, then re-ran upload_forcing to restart automation.
Confirmed that yesterday's change in location of grib_to_netcdf worker monitoring image storage to figures/ works as expected in production.
Changed location of get_NeahBay_ssh worker monitoring image storage to figures/ and moved it in config so that it doesn't get deleted when log_aggregator is restarted.
Added get_NeahBay_ssh worker plots image to salishsea-site automation monitoring page.
download_live_ocean failed with a 0-length file for hour 29; re-ran manually.
Re-organized SalishSeaNowcast deployment docs to make a place for west.cloud deployment, and worked on porting in docs from west.cloud quick-start in docs repo.
(SalishSea)

See project work journal.
(SoG waves)


Sat 18-Feb-2017
^^^^^^^^^^^^^^^

Log aggregator was not receiving messages from watch_NEMO workers on west.cloud, perhaps due to killing of stuck nowcast-green watcher yesterday; restarted log aggregator and messages started flowing.
Added debug logging to manager to show raw message received via broker to try to track down why manager doesn't acknowledge watch_NEMO nowcast-green success message.
download_live_ocean failed with a 0-length file for hour 32; re-ran manually several time to no avail.
Fixed get_onc_ctd worker handling of empty data; see issue #33.
Moved wgrib2.log handler from aggregator to publisher config section; see issue #28
Fixed dev run results archive config key for comparison plots; nowcast-green -> nowcast-dev; backfilled make_plots comparison runs for 12 and 14-17 Fed.
Experimented with adding a TCP_KEEPALIVE_IDLE=900 option value to the worker -> message broker socket setup in nemo_nowcast.worker; comes from the theory that watch_NEMO nowcast-green can't talk to manager at end of run because the network connection has been idle too long.
(SalishSea)


Sun 19-Feb-2017
^^^^^^^^^^^^^^^

Forgot to create LiveOcean symlinks to persist 17feb files to compensate for missing 18feb ones; did so and re-ran upload_forcing worker manually to restart automation; upload_forcing workers should do symlinking; see issue #36.
Decided to leave wgrib2.log handler as it, closing issue #28, because the log should be available if grib_to_netcdf fails, or if it is run with --debug.
Fixed DataArray objects in  get_onc_ctd worker handling of empty salinity data; closed issue #33.
Backfilled get_onc_ctd USDDL runs to 28oct16.
Worked through updating salishsea-nowcast dev env on kudu to Python 3.6; see notebook.
Worked through updating nemo-nowcast-env on kudu VM to Python 3.6; see notebook.
nowcast-green watch_NEMO worker still failed to get ack from manager, so added TCP_KEEPALIVE=1 option value to the worker -> message broker socket setup in nemo_nowcast.worker; also changed net.ipv4.tcp_keepalive_time to 900 on nowcast0 and skookum to try to get watch_NEMO nowcast-green success message to be heard by manager; it worked, but now I don't know which change(s) made the difference.
Reverted net.ipv4.tcp_keepalive_time to 7200 on skookum and re-ran nowcast-green; it worked.
Removed --shared-storage flag from run_NEMO & watch_NEMO; unneeded with distributed logging.
Reverted net.ipv4.tcp_keepalive_time to 7200 on nowcast0 and re-ran nowcast-green; it worked.
Committed and pushed worker socket options TCP_KEEPALIVE=1 and TCP_KEEPALIVE_IDLE=900 that ensure that watch_NEMO nowcast-green get ack from manager.
Got checklist log being written and rotated; see SalishSeaNowcast issue #27, but all the work was in NEMO_Nowcast.
(SalishSea)

Wrote abstract for CMOS talk.

See project work journal.
(SoG waves)


Week 8
------

Mon 20-Feb-2017
^^^^^^^^^^^^^^^

Updated nemo-nowcast-env on west.cloud to Python 3.6.
Updated nemo-nowcast-env on skookum to Python 3.6.
Continued work on NEMO_Nowcast checklist logging bug fix.
Fix bug & unit tests re: removal of --shared-storage flag from watch_NEMO.
Updated niko salishsea-nowcast dev env to Python 3.6.
Rebuild NEMO-3.6 SalishSea and SOG configs on west.cloud with boundary sponge layer code.
Updated niko nemo-cmd dev env to Python 3.6.
Added fspath() and resolved_path() to NEMO-Cmd API.
Worked on ERDDAP datasets from hindcast run results; decided with Susan to designate them g for green and V17.03.
Creatd fspath branch in SalishSeaCmd and started using fspath functions and thinking about YAML file refactoring that Michael and I designed.
(SalishSea)

Phys Ocgy seminar by Jacquie-Lee re: vertical dissipation parameterizations and internal tide breaking in the Arctic.

See project work journal.
(GOMSS)


Tue 21-Feb-2017
^^^^^^^^^^^^^^^

Started materials prep.
Emailed Marion re: student backgrounds and computer lab facilities.
(UQAR Winter School)

See project work journal.
(SoG waves)

Reviewed and refactored Michael's scDataset module.
(SalishSea)


Wed 22-Feb-2017
^^^^^^^^^^^^^^^

See project work journal.
(SoG waves)

Reviewed session outline w/ Susan.
(UQAR Winter School)


Thu 23-Feb-2017
^^^^^^^^^^^^^^^

See project work journal.
(SoG waves)

See project work journal.
(GOMSS)

ONC Tsawwassen - Duke Point ferry data came back online starting 16feb; Jie's download cron doesn't appear to be working though; no sign of Tsawwassen - Swatrz Bay data.
Updated kudu nemo-cmd dev env to Python 3.6.
Transcribed notes from NEMO=Cmd run porting from handwritten into Bitbucket issues.
Resurrected nowcast, salishsea-site, and ERDDAP after skookum reboot associated with ocean being moved to data centre.
(SalishSea)

Went looking for sunset light at Kits Beach, but the sun sets too far to the south this time of year and there wasn't as much alpenglow as I hoped.
Got an dusk image of KYC dock, downtown, mountains, and interesting clouds.


Fri 24-Feb-2017
^^^^^^^^^^^^^^^

See project work journal.
(GOMSS)

nowcast run on west.cloud failed because nowcast10 and nowcast12 nodes had shutdown for some reason after the forecast2 run completed; shutdown meant that they lost their /nemoShare/MEOPAR mounts; remounted and re-ran make_forcing_links nowcast+ to restart automation.
watch_NEMO nowcast-green failed w/ the bad pid error; re-launched it manually with the correct pid.
Discussed scDataset refactoring w/ Michael.
download_live_ocean failed due to 0-length file for hour 59.
Helped Susan update her salishsea-nowcast dev env.
(SalishSea)

Got gitlasso.uqar.ca account set up.
Continued work on materials prep.
Discussed material and pedagogy w/ Idalia.
(UQAR Winter School)


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
