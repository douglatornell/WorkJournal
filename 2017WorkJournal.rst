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


Sat 25-Feb-2017
^^^^^^^^^^^^^^^

Forgot to persist 23feb LiveOcean boundary conditions files, so upload_forcing for forecast2/24feb failed; confirmed that hour 59 was still 0-length; symlinked for persistence:
* ln -s fcst/LO_y2017m02d25.nc
* cd fcst
* ln -s LO_y2017m02d25.nc LO_y2017m02d26.nc
ran upload_forcing forecast2 to restart annimation.
(SalishSea)

Continued work on materials prep.
Started work on slide deck.
(UQAR Winter School)


Sun 26-Feb-2017
^^^^^^^^^^^^^^^

Continued work on materials prep.
Started work on slide deck and directories and repository figures.
Reviewed slide deck and teaching outline w/ Susan re: content and pedagogy.
(UQAR Winter School)

download_live_ocean worker stalled on hour 42 file, but resumed work when I sent it an INT signal; also had to run make_live_ocean_files worker manually.
(SalishSea)


March
=====

Week 9
------

Mon 27-Feb-2017
^^^^^^^^^^^^^^^

Travel from Vancouver to Barrie to visit parents on the way to Rimouski for MEOPAR Winter School.

Worked on NEMO-Cmd enhancement issues.
(SalishSea)


Tue 28-Feb-2017
^^^^^^^^^^^^^^^

Took photos along Kempenfelt Bay shoreline path between Harbourview Inn and Bohemia.

River data download failed in automation, but worked fine when re-run manually.
(bloomcast)

See project work journal.
(GOMSS)

Prepped M&D 2017 income tax info and updated accounts spreadsheet.

Continued work on slide deck and directories and repository figures.
(UQAR Winter School)


Wed 1-Mar-2017
^^^^^^^^^^^^^^

See project work journal.
(GOMSS)

Continued work on slide deck and directories and repository figures.
(UQAR Winter School)

Took M to banks; closed inactive Scotia account.


Thu 3-Mar-2017
^^^^^^^^^^^^^^

Continued work on slide deck and directories and repository figures.
(UQAR Winter School)

Met w/ M&D accountant re: 2017 income tax.


Fri 3-Mar-2017
^^^^^^^^^^^^^^

Start travel from Barrie to Rimouski for MEOPAR Winter School.

Continued work on slide deck.
Started work on notebook for Python automation intro.
(UQAR Winter School)


Sat 4-Mar-2017
^^^^^^^^^^^^^^

Finish travel from Barrie to Rimouski for MEOPAR Winter School.
Arrived in Rimouski at 03:30; no taxis at VIA station to walked the 1.1km to the hotel in -19°C night with -29°C wind-chill thanks to the stiff NW wind.
Red MEC bag does a great job of rolling/sliding on hard snow and ice.

ERDDAP reported high failure rates overnight, so did a shutdown/startup on it.
(SalishSea)

Continued work on slide deck and notebook for Python automation intro.
(UQAR Winter School)

Photographed sunset over Rimouski Bay.


Sun 5-Mar-2017
^^^^^^^^^^^^^^

Finalized slide deck and notebook for Python automation intro.
Walk in Parc du Bic including maple toffee on snow (tire d'erable).
Susan arrived in Rimouski.
(UQAR Winter School)


Week 10
-------

Mon 6-Mar-2017
^^^^^^^^^^^^^^

Student presentations
Git, Gitlab, and UQAR HPC cluster by James Caveen (UQAR)
My code automation session.
(UQAR Winter School)


Tue 7-Mar-2017
^^^^^^^^^^^^^^

Student presentations
Ocean Dynamics Modeling by Daniel Bourgault and Louis-Phillip Nadeau (UQAR)
Regional Models and Open Boundary Conditions and lab by Susan
(UQAR Winter School)

Added the option to use absolute paths for coordinates and bathymetry files in the run description YAML file in NEMO-cmd (issue #5) and SalishSeaCmd (fspath branch).
(SalishSea)


Wed 8-Mar-2017
^^^^^^^^^^^^^^

Student presentations
Surface Wave Physics by Peter Sutherland (IFREMER)
Wave-Ice Interactions and lab by Dany Dumont (QUAR)
HF Radars and trip to Point-au-Père radar by Cédric Chavanne (UQAR)
5@7 at Le Bein Le Malt
(UQAR Winter School)

Added option to provide in the run description YAML file a list of HPC environment modules to include ``module load`` commands for in the run shell script generated by the NEMO-Cmd run sub-command; see issue #11.
(SalishSea)


Thu 9-Mar-2017
^^^^^^^^^^^^^^

Sea Ice Modeling by Jean-Francois Lemieux (UQAR?)
Data Assimilation by Andrea Scot (Waterloo)
(UQAR Winter School)

Investigated SalishSea docs repo build error on readthedocs re: SMELT docs for Youyu's g-oup.
(prediction-core)


Fri 10-Mar-2017
^^^^^^^^^^^^^^^

Climate scenarios and lab by Patrick Grenier (OURANOS and UQAM)
Modeling Marine Plankton by Irene Schloss (UQAR)
Biogeochemical models and lab by Dany Dumont (UQAR)
Ice canoeing in a park
Closing banquet at Les Compromises
(UQAR Winter School)

Added option to provide in the run description YAML file a list of PBS resource key-value pairs that will produce ``#PBS -l`` directives in the run shell script generated by the NEMO-Cmd run sub-command; see issue #10.
(SalishSea)


Sat 11-Mar-2017
^^^^^^^^^^^^^^^

Travel from Rimouski to Vancouver.


Sun 12-Mar-2017
^^^^^^^^^^^^^^^

Added get_run_desc_value() to NEMO-Cmd to provide better error messages re: key(s) missing from YAML file.
Refactored VCS revision and status recording in NEMO-Cmd so that it can also be used by SalishSeaCmd (fspath branch).
(SalishSea)


Week 11
-------

Mon 13-Mar-2017
^^^^^^^^^^^^^^^

make_runoff_file worker failed; probably a DST change glitch because the Fraser and Englishman river flow files contained two 11-Mar entries with different flows; manually ran ecget, make_runoff_file, and upload_forcing to restart automation.
Continued work on Path and YAML file refactoring in SalishSeaCmd (fspath branch).
(SalishSea)

Run failed with an ElementTree parse error during wind processing; failed again in a different month on 1st manual re-run, then succeeded on a 2nd try.
(bloomcast)


Tue 14-Mar-2017
^^^^^^^^^^^^^^^

Continued work on Path and YAML file refactoring in SalishSeaCmd (fspath branch).
(SalishSea)

Extracted nowcast-green temperature and salinity fields for Boundary Pass and ONC Central Node region for Rich & Kevin.
(prediction-core)

Run failed with an ElementTree parse error during meteo processing; failed again in a different month on 1st manual re-run, then succeeded on a 2nd try.
(bloomcast)

Salish Sea team mtg - see whiteboard.


Wed 15-Mar-2017
^^^^^^^^^^^^^^^

Outlined steps for Idalia to run on orcinus in prep for mtg next Monday.
(canyons)

Refactored worklog to capture MEOPAR prediction core activities.

See project work journal.
(SoG waves)

Thrashed most of the afternoon on skookum nemo_nowcast-env; started with a silly error re: cricusctl, but uncovered that Matplotlib imports were messed up.
Built new nowcast-env production environment.
(SalishSea)


Thu 16-Mar-2017
^^^^^^^^^^^^^^^

Recovering from yesterday's nowcast system meltdown:
* download_weather 18
* make_live_ocean_files --run-date 2017-03-15 (on salish)
* make_plots forecast publish --run-date 2017-03-15
EC GEM2.5 06 forecast was late, causing download_weather 06 to fail; recovery:
* download_weather 06
* upload_forcing forecast2 (due to missing LiveOcean files)
Added Susan to critical error email logger address list and restarted log_aggregator to make that effective.
Started work on hindcast metadata for ERDDAP but stalled when I couldn't ssh into skookum.
skookum had to be rebooted at about 13:00 because it somehow got fail2ban-ed by the owncloud server, thereby loosing access to its /home partition; recover:
* download_results $NOWCAST_YAML west.cloud-nowcast nowcast
* get_NeahBay_ssh $NOWCAST_YAML forecast
* make_plots $NOWCAST_YAML nowcast publish --run-date 2017-03-16
* upload_forcing $NOWCAST_YAML west.cloud-nowcast ssh
* make_plots $NOWCAST_YAML nowcast research --run-date 2017-03-16
* make_plots $NOWCAST_YAML nowcast comparison --run-date 2017-03-16
* ping_erddap $NOWCAST_YAML nowcast
* download_live_ocean $NOWCAST_YAML
Warnings from make_plots worker:
  $ python -m nowcast.workers.make_plots $NOWCAST_YAML nowcast publish --run-date 2017-03-16
/results/nowcast-sys/tools/SalishSeaTools/salishsea_tools/stormtools.py:403: RuntimeWarning: invalid value encountered in less
  wind_dir = wind_dir + 360 * (wind_dir < 0)
/results/nowcast-sys/SalishSeaNowcast/nowcast/figures/figures.py:840: FutureWarning: elementwise comparison failed; returning scalar instead, but in the future will perform elementwise comparison
  if inds == 'all':

  $ python -m nowcast.workers.make_plots $NOWCAST_YAML nowcast comparison --run-date 2017-03-16
/results/nowcast-sys/tools/SalishSeaTools/salishsea_tools/stormtools.py:403: RuntimeWarning: invalid value encountered in less
  wind_dir = wind_dir + 360 * (wind_dir < 0)
/results/nowcast-sys/tools/SalishSeaTools/salishsea_tools/data_tools.py:358: FutureWarning: inferring DataArray dimensions from dictionary like ``coords`` has been deprecated. Use an explicit list of ``dims`` instead.
  'actualSamples': sensor['actualSamples'],
(SalishSea)

Mtg w/ Jackie; see project work journal.
(Resilient-C)


Fri 17-Mar-2017
^^^^^^^^^^^^^^^

download_live_ocean failed during yesterday's recover, perhaps due to being left to run in background of closed terminal session; recovery:
* download_live_ocean $NOWCAST_YAML --run-date 2017-03-16
* make_live_ocean_files $NOWCAST_YAML --run-date 2017-03-16
* upload_forcing west.cloud-nowcast forecast2
(SalishSea)

See project work journal.
(SoG waves)

Westgrid townhall:
* https://www.westgrid.ca/files/WG%20Town%20Hall%20March%2017%202017.pdf
* new systems updates
  * Patrick Mann, ops dir of westgrid
  * arbutus 7600 cores running, ceph expansion in progress, Ryan Enge UVic is team lead
  * storage is biggest issue in RAC, not enough
  * Cedar racks & servers installed, cabling in progress, still on target for mid-April, pessimistic end of April or early May
  * Graham ~2wks behind Cedar
  * Network agreements are delaying national object storage service
  * Lustre FS is done
  * Scheduler changed to Slurm (open source w/ commercial support), docs soon on docs wiki
  * Niagara RFP issued, ~60k cores, late 2017
  * NDC (National Data Cyberinfrastructure) 13Pb delivered to Waterloo available early-Apr, 10Pb at SFU in mid-April
  * Object storage in summer, lots of demand
  * Jasper defunding delayed to 1Oct, all other system defunding dates also extended
  * **data will be deleted after defunding dates - no backups**
  * orcinus & bugaboo (and others) defunded 13-Mar-2018
* migration
  * Patrick Mann, ops dir of westgrid
  * westgrid.ca/migration_process docs
  * move data in advance to avoid network bottlenecks
  * jasper will be available to UofA researchers for 1-3 years (but not computecanada users)
  * delete, archive, compress
  * use globus for file transfers (high speed)
  * docs.computecanada.ca
* silo decommisioning
  * Sergiy Stepanenko USask site lead
  * 1st stage migration from Silo to SFU & Waterloo completed
  * 2nd stage will be to NDC sometime in summer 2017
* national updates
  * Erin Trifunov
  * account renewals by 13Apr or deleted; no CCV
  * email notifications going out in batches
  * 2017 RAC award letters going out next week; date of effect TBD based on Cedar and Graham availability
  * scaling:
    * 54% of compute requests
    * 90% of storage requests
  * HPCS 6-9Jun in Kingston
* westgrid updates
  * training:
    * 29mar paraviewweb
    * 19-22 jun ubc summer school


Sat 18-Mar-2017
^^^^^^^^^^^^^^^

See project work journal.
(SoG waves)


Sun 19-Mar-2017
^^^^^^^^^^^^^^^

12 weather download failed due to unavailability of EC files, ran download_weather 12 to recover at 14:05.
watch_NEMO failed to find nowcast run PID; recover:
* get_NeahBay_ssh forecast
* download_results nowcast
make_plots nowcast research failed
Started changing SalishSeaCmd package to use f-strings.
(SalishSea)


Week 12
-------

Mon 20-Mar-2017
^^^^^^^^^^^^^^^

Created provisional ubcSSnBathymetryV17-02 ERDDAP dataset.
Continued changing SalishSeaCmd package to use f-strings.
Requested access to Python 3.6 beta on readthedocs for SalishSeaCmd project.
(SalishSea)

Seminar by SCOR tour speaker CJ Mundy of UManitoba on under-ice spring algae blooms in the Arctic.

Helped Idalia get set up and running on orcinus.
(Canyons)


Tue 21-Mar-2017
^^^^^^^^^^^^^^^

Created provisional ubcSSg3DuVelocity1hV17-02, ubcSSg3DvVelocity1hV17-02, ubcSSg3DwVelocity1hV17-02 ERDDAP datasets.
Worked on generating ERDDAP datasets from ONC ferry data.
Salish Sea team mtg; see whiteboard.
(SalishSea)


Wed 22-Mar-2017
^^^^^^^^^^^^^^^

State of the PAcific Ocean (SOPO) meeting in Sydney.

See project work journal.
(SoG waves)


Thu 23-Mar-2017
^^^^^^^^^^^^^^^

State of the PAcific Ocean (SOPO) meeting in Sydney.

Extracted nowcast-green temperature and salinity fields for Boundary Pass and ONC Central Node region *for correct date range* for Rich & Kevin.
(prediction-core)


Fri 24-Mar-2017
^^^^^^^^^^^^^^^

See project work journal.
(SoG waves)


Sat 25-Mar-2017
^^^^^^^^^^^^^^^

See project work journal.
(SoG waves)


Sun 26-Mar-2017
^^^^^^^^^^^^^^^

forecast2 watch_NEMO worker failed due to bad run_NEMO pid; ran download_results manually to restart automation.
download_live_ocean worker failed with 404 error on hour 26; created symlinks to persist the previous day's files.

See project work journal.
(SoG waves)


Week 13
-------

Mon 27-Mar-2017
^^^^^^^^^^^^^^^
Debugged conservative temperature fields def issue in Susan's hindcast runs.
Added colour bar range attribute values setting feature to ERDDAP dataset notebook.
Worked toward provisional ubcSSg3DTracerFields1hV17-02 ERDDAP dataset.
Continued work on generating ERDDAP datasets from ONC ferry data.
Helped Tereza w/ hg heads, rebasing, merging, ssh keys, and NEMO namelists.
(SalishSea)

Phys Ocgy seminars by Rob Izett (net community production in subarctic Pacific based on dO2/Ar observations with NO2-based corrections for vertical mixing) and Phillipe Tortell (vertical mixing and net community production in Arctic based on observations and modeling - MEOPAR proposal)


Tue 28-Mar-2017
^^^^^^^^^^^^^^^

Got close to provisional ubcSSg3DTracerFields1hV17-02 ERDDAP dataset; incorrect salinity standard_name value, need to repeat all hindcast runs; conflicting salinity units in run results, need to repeat all hindcast runs.
Created provisional ubcSSgSurfaceTracerFields1hV17-02 ERDDAP dataset.
Explored ptrc_T files, working toward ubcSSg3DBiologyTracerFields1hV17-02 ERDDAP dataset; need to buff variables names, standard_name attributes, and units in field_def.xml and iodef.xml.
Tide gauge station datasets fail to load due to dimension issues.
Helped Tereza more with ssh keys.
Talked to Susan about biology tracers metadata edits.
Continued work on generating ERDDAP datasets from ONC ferry data.
(SalishSea)

Discussed Kevin's Boundary Pass to Central Node analysis w/ he, Rich & Susan.
Started generation of 3 velocity component field datasets for Kevin.
(prediction-core)

Discussed model runs progress w/ Idalia.
(Canyons)


wed 29-Mar-2017
^^^^^^^^^^^^^^^

See project work journal.
(SoG waves)

Created a visualization notebook in analysis-doug/SoG-waves/ to explore ww3 results.
(SalishSea)


Thu 30-Mar-2017
^^^^^^^^^^^^^^^

Tried test of 36h forecast2 run by changing run duration in config file from 1.25 to 1.5 days; failed 46 timesteps after 30h 'cuz that's beyond the end of weather forcing; looks like only forecast can be extended to 36h.
Restarted erddap.
Started work on XIOS2 repo for group and production:
* NEMO docs recommend trunk r819, but that is from 1feb16
* after consultation w/ Susan and Michael, created repo from tip of trunk
* set up XIOS-2-hg-mirror, XIOS-2-mirror-merge, Bitbucket XIOS-2, and working XIOS-2 repos
* wrote docs for repo mgmt in re-organized NEMO code docs section
* worked on building XIOS-2 on orcinus, but it is failing with a duplicate main() error
(SalishSea)

See project work journal.
(SoG waves)

Started generation of 3 velocity component field datasets for Kevin's Boundary Pass to Central Node analysis.
(prediction-core)

Attended EOAS colloquium by John Thompson (ex-EOAS, now Cornell) re: future of mineral exploration and mining.

Attended poster corral.


Fri 31-Mar-2017
^^^^^^^^^^^^^^^

Did a successful 36h forecast run test; agreed with Susan to make that the default from here forward.
Modernized run_NEMO worker _launch_run_script().
Tracked XIOS-2 build issue down to an upstream bug; svn r1066 that Michael is using builds fine.
(SalishSea)

See project work journal.
(SoG waves)

See project work journal.
(GOMSS)


Sat 1-Apr-2017
^^^^^^^^^^^^^^

Changed YAML file `output: files:` key to `iodefs` (breaking change), and `output: domain:` key to `domains` with fall-back to `domain`.
Added processing for optional YAML file `output: files:` key for the XIOS-2 file_def.xml file to SalishSeaCmd.
watch_NEMO failed to find run_NEMO process; idea let watch_NEMO do pgrep instead of run_NEMO because pgrep in run_NEMO sometimes returns multiple pids, and the most recent is not the correct one.
(SalishSea)


Sun 2-Apr-2017
^^^^^^^^^^^^^^

Resolved NEMO-Cmd issue #16 re: Python 2.7 unicode/str error in vcs revision file writing.
Ported YAML file output section key spelling changes & addition of filedefs item to NEMO-Cmd.
Started adding path existence check to nemo_cmd.utils.get_run_desc_value().
(SalishSea)

ssh keys thrash on west.cloud because my west.cloud_id_rsa somehow got deleted from nowcast1; default key available on all VMs is the nefos sshfs one.

See project work journal.
(SoG waves)


April
=====

Week 14
-------

Mon 3-Apr-2017
^^^^^^^^^^^^^^

Finished adding path existence check to nemo_cmd.utils.get_run_desc_value().
Integrated path existence check into SalishSeaCmd.
Expanded use of get_run_desc_value() in SalishSeaCmd.
(SalishSea)

SoG Networks seminars by Kevin Fan re: deep gravity currents, and Giorgio Sgarbi re: Iona outfall particle tracking.

Late lunchtime conversation w/ Yoshi of Mark J's group re: NEMO model & explosive volcanoes.


Tue 4-Apr-2017
^^^^^^^^^^^^^^

Continued work on NEMO-Cmd and SalishSeaCmd improvements.
NEMO-Cmd VCS recording now ignores CONFIG/cfg.txt and TOOLS/COMPILE/full_key_list.txt files.
Fixed bug re: VCS recording file name for NEMO code repo in SalishSeaCmd.
Started refactoring forcing paths in SalishSeaCmd to use get_run_desc_value().
Salish Sea team mtg; see whiteboard.
(SalishSea)


Wed 5-Apr-2017
^^^^^^^^^^^^^^

ECget river flow failed for Fraser; wateroffice site has added commas to discharge values in HTML table; hacked code to make it work.
Manually re-ran make_runoff_file and upload_forcing to restart automation for forecast2 run.
Tried to help Susan switch to running hindcast on orcinus; environment mess, then config file mess.
(SalishSea)

See project work journal.
(SoG waves)


Thu 6-Apr-2017
^^^^^^^^^^^^^^

See project work journal.
(SoG waves)

EOAS colloquium by Nicolas Cassar re: remote sensing of net community production

Started refactoring forcing paths in SalishSeaCmd to use get_run_desc_value().
(SalishSea)


Fri 7-Apr-2017
^^^^^^^^^^^^^^

Submitted renewal request for Compute Canada account.

See project work journal.
(GOMSS)

Updated bloomcast dev env on kudu to Python 3.6.
Fixed rivers discharge commas issue in bloomcast and manually ran for today.
(SalishSea)

See project work journal.
(SoG waves)


Sat 8-Apr-2017
^^^^^^^^^^^^^^

Finished refactoring forcing paths in SalishSeaCmd to use get_run_desc_value().
Split SalishSeaCmd run description file docs to improve TOC visibility.
(SalishSea)


Sun 9-Apr-2017
^^^^^^^^^^^^^^

Continued work on metadata for v17-02 ERDDAP datasets.
Added restart section handling to SalishSeaCmd.prepare for NEMO-3.6 runs.
(SalishSea)


Week 15
-------

Mon 10-Apr-2017
^^^^^^^^^^^^^^^

Changed SalishSeaNEMO.sh script generation to return exit code of mprirun command; re: SalishSeaCmd issue #3.
Got SalishSeaCmd docs to build on readthedocs re: Python 3.6.
Continued work on metadata for v17-02 ERDDAP datasets.
(SalishSea)


Tue 11-Apr-2017
^^^^^^^^^^^^^^^

Worked on expense claim for SoPO trip.

Salish Sea team mtg; see whiteboard.
Re-created XIOS-2 maint repos based on r1066 checkout; unable to build on salish because netcdf.mod is not found.
Continued work on ERDDAP metadata via email discussions w/ group.
(SalishSea)

EOAS retreat lunch; long chat w/ Phil.

Drinks at The Point to celebrate Cindy & Jie's thesis submissions.


Wed 12-Apr-2017
^^^^^^^^^^^^^^^

Off-kilter morning; hard to settle down to work.

Resolved PyCharm issue of test runner using elements from 2016.3.2 by downloading and installing 2017.1.1 tarball; looks like I was seeing 2016.3.2 because I did an in-place upgrade from 2016.3.2 to 2017.1.1.

Added Amber Holdsworth to SealishSea-MEOPAR and CCAR-modeling teams on Bitbucket.
(prediction-core)

See project work journal.
(SoG waves)


Thu 13-Apr-2017
^^^^^^^^^^^^^^^

forecast2 watch_NEMO failed w/ bad pid error; manually re-ran download_results to restart automation.
Continued work on XIOS-2 repo; got a successful build on salish by adding -I/user/include.
Sent email to Roman@westgrid re: updating Mercurial on orcinus and suggested building module from Centos RPM to perhaps avoid Python 2.7/3 conflict.
Added NEMO-3.6 repos maint section to docs.
Ported get_run_desc_value() refactoring from SalishSeaCmd to NEMO-Cmd.
Helped Susan get her salishsea-nowcast dev env sorted out so that she can do rivers files updates.
(SalishSea)

Sumitted expense claim for SoPO meeting trip.

See project work journal.
(SoG waves)

Attended final EOAS colloquium re: 65Mya extinction event crater off Yucatan.


Fri 14-Apr-2017
^^^^^^^^^^^^^^^

**Statutory Holiday** - Good Friday

Extracted nowcast-green temperature, salinity and 3 velocity components fields for Boundary Pass and ONC Central Node region for 9-22-Aug-2016 for Rich & Kevin.
(prediction-core)

Split NEMO-Cmd run description file docs to improve TOC visibility.
Worked on SalishSeaCmd issue #2 re: making land processor elimination MPI-LPE mapping file configurable in YAML file.
(SalishSea)

See project work journal.
(SoG waves)


Sat 15-Apr-2017
^^^^^^^^^^^^^^^

Restarted ERDDAP after overnight email reports of excessive failure rates.
Added west.cloud rule to allow ingress on port 5570 for make_ww3_wind_file worker.
Updated SalishSeaNowcast on skookum and west.cloud to enable make_ww3_wind_file in automation.
Resolved SalishSeaCmd issue #2 re: making land processor elimination MPI-LPE mapping file configurable in YAML file.
Buffed NEMO-Cmd example YAML files and docs.
Ported separate YAML restart section from SalishSeaCmd to NEMO-Cmd.
Changed NEMO-Cmd generated NEMO.sh script to return exit code of mpirun command.
Refactored SalishSeaCmd to make temporary run directory a Path object throughout.
(SalishSea)

See project work journal.
(SoG waves)


Sun 16-Apr-2017
^^^^^^^^^^^^^^^

Added west.cloud rule to allow ingress on ports 5571-5572 for make_ww3_current_file and run_ww3 workers.
Updated SalishSeaNowcast on skookum and west.cloud to enable make_ww3_current_file and run_ww3 in automation.
Started refactoring NEMO-Cmd to make temporary run directory a Path object throughout.
(SalishSea)

Replied to Étienne's eamil about submitting patches.
Updated club membership link and emailed Mark Ford thanks for the heads-up.
(randopony)

See project work journal.
(SoG waves)


Week 16
-------

Mon 17-Apr-2017
^^^^^^^^^^^^^^^

**Statutory Holiday** - Easter Monday

See project work journal.
(SoG waves)

download_live_ocean failed silently yesterday at hour 49, causing forecast2 to fail this morning; a check upstream shows that hour 49 is now available, so manually re-ran download_live_ocean.
Finished refactoring NEMO-Cmd to make temporary run directory a Path object throughout.
download_live_ocean for 16apr stalled again at hour 51; manually added symlinks to persist previous day's product, and launched nowcast and nowcast-dev late.
Resumed work on clearing old SalishSeaNowcast pkg out of tools repo.
Discussed nowcast figures dev/test workflow and docs w/ Susan.
(SalishSea)

Resolved insecure content issue on site index page by symlinking circle image into /results/nowcast-sys/figures/ tree so that it can be served via apache2 figures static content server.
Confirmed that today's resolution of chaussette github issue #82 allows us to unpin waitress from 0.9.0; decided to wait a couple of weeks to see if there is a new release of chaussette.
(salishsea-site)


Tue 18-Apr-2017
^^^^^^^^^^^^^^^

HRDPS 06 forecast was late so download_weather worker failed; re-ran manually to restart automation.
Salish Sea team mtg; see whiteboard.
Continued work on ERDDAP metadata until I realized that there is un-pushed work at home on kudu.
Finished deleting SalishSeaNowcat pkg from tools repo.
Started work on revising web site figures docs.
Fixed import issues in tools docs so that they build without error again.
(SalishSea)

Checked Kevin's report that the Aug-2016 Boundary Pass to Central Node results slabs contain incorrect variables; unable to reproduce.
(prediction-core)

Mtg w/ Saurav re: workspace organization.
(Canyons)


Wed 19-Apr-2017
^^^^^^^^^^^^^^^

watch_NEMO forecast2 reported bad pid; manually ran download_results, but accidentally overwrote 17apr17.
Explored tracer figures code from Muriel and Elise and thought about how to integrate it into research figures.
Changed plot_dir to Path object in make_plots worker.
(SalishSea)

See project work journal.
(SoG waves)

See project work journal.
(GOMSS)

See project work journal.
(Resilient-C)


Thu 20-Apr-2017
^^^^^^^^^^^^^^^

get_NeahBay_ssh failed due to missing Mercurial on skookum, but forecast2 run proceeded thanks to persistence symlinking in upload_forcing.
Opened ticket UDSE-5732-LXGF re: missing Mercurial on skookum & salish, and downgrade to 3.3.2 on other machines.
run_ww3 forecast2 didn't launch because I forgot to pull, update & restart manager on skookum.
Buffed SalishSeaNowcast deployment docs.
Added provision 17-02 biology tracers dataset to ERDDAP.
Sorted out value of _FillValue and missing_value variable attrs in ERDDAP; keeping both.
Renamed 3D[uvw]Velocity datasets to 3D[uvw]Variables.
(SalishSea)

See project work journal.
(SoG waves)

See project work journal.
(GOMSS)

See project work journal.
(Resilient-C)


Fri 21-Apr-2017
^^^^^^^^^^^^^^^

Continued work on ERDDAP datasets metadata; lots more buffing.
Struggled with extra dimension in single point ssh files; ERDDAP doesn't like dimensions of ssosheig.
(SalishSea)

Attended canyons team mtg; did refresher on hg rebase.
Met w/ Saurav to continue towards NEMO-Cmd.
(Canyons)

EOAS dept. computer committee issues.

Saw Vertical Influences at Britannia Arena.


Sat 22-Apr-2017
^^^^^^^^^^^^^^^

Confirmed that run_ww3 worker is cleaning up wind and current files after itself, and deleted all the old ones from test runs and pre-production.
Tagged several significant points in SalishSeaNowcast repo; NEMO_Nowcast, distributed logging, Python 3.6, wave forecasts; now on v3.3.dev0 for dev edge.
Continued work on revising web site figures docs.
(SalishSea)

Took lots of old electronics/appliances to recycling drop-off at Dunbar Community Centre.

See project work journal.
(GOMSS)


Sun 23-Apr-2017
^^^^^^^^^^^^^^^

Continued work on revising web site figures docs.
Restarted ERDDAP server due to high error rate reports overnight.
Exposed nemo_cmd.combine.find_rebuild_nemo_script() in nemo_cmd.api; re: NEMO-Cmd issue #20.
Added confirmation of existence of rebuild_nemo script to nemo_cmd.prepare; re: NEMO-Cmd issue #19.
Added confirmation of existence of rebuild_nemo script to salishsea_cmd.prepare; re: SalishSeaCmd issue #4.
Finally succeeded in creating and XIOS-2 repo on Bitbucket that builds on salish and orcinus.
(SalishSea)

See project work journal.
(GOMSS)


Week 17
-------

Mon 24-Apr-2017
^^^^^^^^^^^^^^^

See project work journal.
(GOMSS)

Merged Michael's NEMO-Cmd pr#1 re: undotted booleans in fortran namelists but it breaks 2 units tests.
Continued work on revising web site figures docs.
(SalishSea)


Tue 25-Apr-2017
^^^^^^^^^^^^^^^

See project work journal.
(GOMSS)

Salish Sea team mtg; see whiteboard.
Continued work on revising web site figures docs.
Tracked down code literal line number alignment issue down to sphinx_rtd_theme; broken in 0.1.7, fixed in 0.1.9, broken again in 0.2.4, fixed 0.2.5b1; removed line numbers until readthedocs updates or allows choice of theme version.
Continued development of research.tracer_thalweg_and_surface website figure.
Fixed unit test failures that resulted from Michael's NEMO-Cmd pr#1.
(SalishSea)


Wed 26-Apr-2017
^^^^^^^^^^^^^^^

See project work journal.
(GOMSS)

Filed and paid 2016 GST return; see biz journal.

Aded deflation of *_dia[12]_T*.nc files to SalishSeaCmd generated SalishSeaNEMO.sh scripts.
Discovered that 25apr nowcast-green run failed with high velocity; Susan increased viscosities, and I relaunched the run via make_forcing_links.
Closed NEMO-Cmd issue #15 re: minimizing environment-rtd.yaml.
(SalishSea)

Watched recording of webinar on PyCharm debugger; learned that breakpoints can be added/removed while process is running, about watches, moving up and down the frame stack, attaching the debugger to running processes, setting breakpoints in web app templates, and debugging JavaScript.

See project work journal.
(SoG waves)


Thu 27-Apr-2017
^^^^^^^^^^^^^^^

Signed off MEOPAR cycle 2 NCE and disclosure agreements.
(prediction-core)

Updated Soontiens-Allen-2017 citation in docs and salissea-site.
Added publications page to salishsea-site.
Bumped NEMO-Cmd to v1.0.
Created conda package recipe for python-hglib-2.4, built it, and uploaded it to gomss-nowcast channel to support nemo-cmd-1.0 package.
Bumped SalishSeaCmd to v3.1.
make_ww3_current_file failed with a dask memory error; re-ran it manually and successfully restarted automation.
Continued development of research.tracer_thalweg_and_surface website figure.
Discussed a scheme with Susan to run NEO results file deflation as 3 (possibly concurrent) serial jobs chained to the NEMO run, but held until its execution completes successfully.
(SalishSea)

Attended AAPS spring general meeting.


Fri 28-Apr-2017
^^^^^^^^^^^^^^^

See project work journal.
(SoG waves)

Worked w/ Michael on docs cleanup in preparation for Vicky joining the group on 1-May.
Started adding --separate-deflate feature to salishsea run.
download_live_ocean worker apparently just stopped during hour 12 file download or processing; re-ran manually, and it failed later, causing forecast2 to fail.
Helped Susan test SalishSeaCmd WIP on orcinus.
(SalishSea)


Sat 29-Apr-2017
^^^^^^^^^^^^^^^

Helped Susan get SalishSeaCmd WIP operational on jasper.
Added LiveOcean persistence symlinks for yesterday and manually re-ran upload_forcing forecast2 to restart automation.
Finalized v17-02 biology dataset on ERDDAP.
(SalishSea)


Sun 30-Apr-2017
^^^^^^^^^^^^^^^

Fraser River flow cron job failed; manual re-run worked fine; ran make_runoff_file and upload_forcing workers to restart automation.
Finalized v17-02 datsets: 3d physics tracers, surface physics tracers, u grid, v grid, w grid.
(SalishSea)


May
===

Week 18
-------

Mon 1-May-2017
^^^^^^^^^^^^^^

Vicky Do joined the team.
Finalized 17-02 bathymetry dataset.
Continued work on revising web site figures docs.
(SalishSea)

SoG network seminar by Elise on light attenutation.


Tue 2-May-2017
^^^^^^^^^^^^^^

Salish Sea team mtg; see whiteboard.
Continued work on revising web site figures docs.
Updated nowcast-vm to current production configuration.
Started refactoring make_plots worker to make it more researcher-friendly for declaration of figures, and more efficiently abstracted for their production; code reviewed by Susan.
(SalishSea)

Deleted all stored vagrant VMs, recovering ~30% of /home storage.


Wed 3-May-2017
^^^^^^^^^^^^^^

Deleted all stored vagrant VMs.
Moved VirtualBox VM storage from /home/doug to warehouse/, recovering ~50% of /home storage.

Continued refactoring make_plots worker.
Updated NEMO-3.6-code on west.cloud and salish, and did clean builds of SalishSea, SOG and SMELT configurations.
Updated clones on west.cloud: NEMO-forcing, SalishSeaNowcast, SalishSeaWaves, SS-run-sets.
Cloned XIOS-2 and built on west.cloud and salish.
(SalishSea)


Thu 4-May-2017
^^^^^^^^^^^^^^

Continued refactoring make_plots worker.
Discovered that biology tracers (and maybe some physics too?) blew up in nowcast-green/29apr17 run.
Discovered that James colour bar levels calculation code is not robust to spring conditions.
(SalishSea)


Fri 5-May-2017
^^^^^^^^^^^^^^

Continued work on revising web site figures docs.
Sprint planning mtg.
With Susan's help, figures out why tracer_thalweg_and_surface contour levels calculation function was flaky in the spring; numpy.percentile() doesn't play well with masked arrays.
(SalishSea)


Sat 6-May-2017
^^^^^^^^^^^^^^

Cycled to Craig Bay

Refactored upload_forcing worker to use f-strings.
Refactored upload_forcing worker to use pathlib; re: issue #24.
Added IOError handling to upload_forcing worker to handle missing LiveOcean boundary conditions files by creating symlinks to persist previous day's files; re: issue #36.
(SalishSea)


Sun 7-May-2017
^^^^^^^^^^^^^^

Added make_plots nowcast-green to automation.
Refactored make_forcing_links worker to use pathlib; re: issue #26.
Refactored salishsea-site to change research figures page to currents and physics tracers page.
Added biology tracers figures page to salishsea-site with nitrate thalweg and surface figure on it.
Started refactoring run_NEMO worker to be compatible with SalishSeaCmd-3.1; issue #40.
(SalishSea)

Returned to Vancouver


Week 19
-------

Mon 8-May-2017
^^^^^^^^^^^^^^

Frequent Firefox crashes since upgrading niko to Ubuntu1 7.04 prompted me to blow away my old tabs collection and start over in a new window; it made no difference - crashed on naming of new tab group.

Email cleanup.
Continued work on revising web site figures docs.
Tested nowcast-fig-dev environment on herring; sent email to Susan, Elise, Michael & Ben requesting them to test it for themselves and provide docs feedback.
(SalishSea)

Phys Ocgy seminar on Baltic Sea mixing by Hans Burchard.


Tue 9-May-2017
^^^^^^^^^^^^^^

Fixed bugs in upload_forcing and make_forcing_links so that missing LiveOcean files handling actually works.
Created a separate Sentry project for salishsea-site, changed the envvar value in the salishsea-site-env, and restarted circusd to make it effective.
Fixed SalishSeaNowcast repo "path" on Sentry so that issue tracker integration should work now.
upload_forcing nowcast+ to west.cloud timed out for no apparent reason; re-ran manually to restart automation.
Added note to nowcast-green docs re: restoration of missing light attenuation w/ depth term, effective 29apr17.
Finished revising web site figures docs.
Fixed atmospheric link checking function call bug in NEMO-Cmd reported by Saurav.
(SalishSea)

Started creating EOAS TODOs list re: discussion of priorities w/ Susan on Saturday.


Wed 10-May-2017
^^^^^^^^^^^^^^^

Deleted NEMO-3.6r6204, NEMO-3.6r6459, and NEMO-3.6r6770 repos from Bitbucket.
Tested single point, single variable time series request to ERDDAP; ~35s for 30 days, ~70s for 2mo.
Located https://nbviewer.jupyter.org/urls/bitbucket.org/salishsea/tools/raw/tip/bathymetry/mesh_mask_SalishSea2_metadata.ipynb to help with adding metadata to v17-02 mesh mask.
Resumed work on checklist.log file writing and rotation bug in NEMO_Nowcast; see SalishSeaMowcast issue #27 and NEMO_Nowcast issue #9.
(SalishSea)

Worked on 43ravens business development; see biz journal.

See project work journal.
(Resilient-C)

System76 Meerkat for M&D was delivered.


Thu 11-May-2017
^^^^^^^^^^^^^^^

Finished fixing NEMO_Nowcast bug whereby checklist.log file was being neither written nor rotated; see SalishSeaMowcast issue #27 and NEMO_Nowcast issue #9.
Fixed NEMO_Nowcast readthedocs environment re: Python 3.6.
Changed NEMO_NOwcast docs diagrams to PNG renderings due to docutils 0.13.1 bug on readthedocs.
Tagged NEMO_Nowacst v1.4, build conda package, and uploaded it to gomss-nowcast channel.
download_results nowcast-green failed for no obvious reason other than /results being 98% full; re-ran manually.
Worked on 17-02 mesh mask ERDDAP datasets.
(SalishSea)

Reviewed and refined T2125 business income tax form and spreadsheet.

Discovered that portable TimeMachine backup drive for tom won't boot.

See project work journal.
(Resilient-C)

Did initial setup of System76 Meerkat for M&D; see google doc.


Fri 12-May-2017
^^^^^^^^^^^^^^^

Stopped scheduler, manager, message_broker, and log_aggregator on skookum.
Updated skookum and west.cloud to NEMO_Nowcast-1.4.
Started scheduler, manager, message_broker, and log_aggregator on skookum.
Finished parts of hindcast-*/ cleanup and spin-up/ move to /ocean that Susan couldn't do due to permissions; /results now at 90% w/ 1.2Tb free.
Worked on 17-02 mesh mask ERDDAP datasets.
Worked on refactoring SalishSeaNowcast run config section; issue #12.
(SalishSea)

Did research file space organization session with Birgit and Melanie.
Helped Brigit try to debug why GYRE with TOP blows up with an MPI-ish error almost immediately.
(GEOTRACES)


Sat 13-May-2017
^^^^^^^^^^^^^^^

Worked on refactoring SalishSeaNowcast run config section; issue #12; further work on hold until issue #40 is completed.
Discussed make_runoff_file worker use of coordinates w/ Susan; re: issues #21 and #31.
Continued refactoring run_NEMO worker to be compatible with SalishSeaCmd-3.1; issue #40.
(SalishSea)


Sun 14-May-2017
^^^^^^^^^^^^^^^

Worked on 17-02 mesh mask ERDDAP datasets.
Pulled and updated on skookum: tools, NEMO-forcing, SalishSeaNowcast, NEMO-Cmd, SalishSeaCmd; installed NEMO-Cmd-1.0 and SalishSeaCmd-3.1; re-ran nowcast-dev as a test of 3.1 integration and Susan's improvements to make_runoff_file worker.
(SalishSea)


Week 20
-------

Mon 15-May-2017
^^^^^^^^^^^^^^^

EC Fraser River flow data unavailable; recover:
* persisted 13may value
* ran make_runoff_file
* ran upload_forcing forecast2 to restart aoutmation
(SalishSea)


Tue 16-May-2017
^^^^^^^^^^^^^^^

SalishSeaCast sprint.
Started work on ECget plug-in to scrape Fraser River water quality buoy data web page.
(SalishSea)


Wed 17-May-2017
^^^^^^^^^^^^^^^

After trashing around trying to add a 2nd organizer email to the LM400, improved the data mgmt docs to remind myself how to launch pshell and do the 2nd email task.
(randopony)

Susan discovered that the tools repo blew up with a merge of old SalishSeaNowcast and salishsea-site commits from TJ.
(SalishSea)

Helped Birgit sort out her YAML file for initial use of NEMO-Cmd; highlighted issue #12 re: need to gracefully handle empty YAML stanzas.
(GEOTRACES)

See project work journal.
(GOMSS)

See project work journal.
(Resilient-C)


Thu 18-May-2017
^^^^^^^^^^^^^^^

watch_NEMO forecast2 failed due to 2 pids issue; recover:
* manually ran download_results to restart automation
* manually ran make_ww3_wind_file, make_ww3_current_file, run_ww3
Backed out tools repo changeset b726e031970d, a 3357 file pkg build/ directory that TJ probably accidentally committed in Feb and merged on Tue.
Triaged sprint contributions.
Reworked SealishSea-MEOPAR team permissions on Bitbucket to add Guests (read-only) and Guest Contributors (read/write) groups so that Developers (read/write/create) contains only MOAD members and alumni.
(SalishSea)

See project work journal.
(GOMSS)

See project work journal.
(Resilient-C)


Fri 19-May-2017
^^^^^^^^^^^^^^^

download_weather 06 timed out on hour 37; re-ran manually to restart automation.
(SalishSea)


* Reply to Peg
* Process some images
* Test attrs-17.1
* Take knives for sharpening
* Check out Herman Miller chairs at EQ3


ToDo
====

* refactor, unit tests & docs for forcing links checking for NEMO-3.6

* reduce resolution of landing page images for faster load times
* add docs re: sealinkd server-side app framework
* add EduCloud deployment docs

* research_ferries module
* JSON logging use example notebook

* review remaining nosy PRs
