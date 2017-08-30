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
(Resilient-C)


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
(Resilient-C)

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
Organized salishsea-site app templates to reflect nav bar.
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
(Resilient-C)


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
(salishsea-site)

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
(salishsea-site)

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

Investigated SalishSea docs repo build error on readthedocs re: SMELT docs for Youyu's group.
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

Added deflation of *_dia[12]_T*.nc files to SalishSeaCmd generated SalishSeaNEMO.sh scripts.
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

Updated Soontiens-Allen-2017 citation in docs and salishsea-site.
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
Finished 17-02 mesh mask ERDDAP datasets.
Disovered that GenerateDatasetXml.sh reports the same "error" for 16-10 single point sea surface height as it does for 17-02, yet 16-10 ERDDAP dataset works; decided to ignore error and hack a 17-02 XML fragment from the 16-10 one, and it works, ffs.
(SalishSea)

Susan floated the idea of MOAD team on Bitbucket w/ docs and MOAD-tools repo.
Michael raised issue of discoverability in SalishSeaTools:
* split API docs by module
* ensure that indices are working
(MOAD software)

Got Idalia and Georgio set up for tomorrow's sprint.
(SalishSeaCast sprint)


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
download_weather 12 timed out on hour 1; re-ran manually to restart automation.
download_results forecast seems to have launched before results files were moved from tmp run dir on west.cloud; I think this happened once before recently; re-ran manually to restart automation.
Continued work on 17-02 tide gauge station ERDDAP datasets; 06jun15 Pt Atkinson file may be bad.
Finished refactoring run_NEMO worker so that it is compatible with SalishSeaCmd-3.1 and XIOS-2.
download_weather 18 timed out on hour 31; re-ran manually to restart automation.
(SalishSea)

Canyons team mtg.
(Canyons)

GEOTRACES team mtg.
(GEOTRACES)

Mtg w/ Youyu and Fan from BIO.


Sat 20-May-2017
^^^^^^^^^^^^^^^

make_runoff_file failed due to patlib refactoring bug; fixed and re-ran it and upload_forcing forecast2 manually to restart automation.
download_weather 12 failed; re-ran manually quite late in the day to restart automation.
run_NEMO nowcast-dev failed due to typo in private-tools repo path; fixed and re-ran make_forcing links manually to restart automation late in the day.
(SalishSea)


Sun 21-May-2017
^^^^^^^^^^^^^^^

download_weather 06 failed due to EOAS network issues; re-ran manually in debug mode quite late in the day; also manually ran make_runoff_file and grib_to_netcdf in debug mode to prep for day's runs.
download_weather 12 failed due to EOAS network issues; re-ran manually quite late in the day to restart automation.
(SalishSea)


Week 21
-------

Mon 22-May-2017
^^^^^^^^^^^^^^^

**Statutory Holiday** - Victoria Day

Yesterday's forecast run got stuck at 84.7%; unclear why, but it complained about 23may weather file; recover:
* kill watch_NEMO
* kill mpirun
* kill bash SalishSeaNEMO.sh
* kill rebuild_nemo
* delete tmp run dir
* delete forecast/21may17
* cp ww3_foreacst/20may17/restart into ww3_foreacst/21may17/ to provide good as possible initial conditions for next wave forecast
Deleted results from west.cloud:
* forecast2 > 15d old
* forecast > 20d old
* nowcast > 30d old
* nowcast-green > 30d old
* enabled cron jobs to maintain the above
Manually ran clear_checklist worker.
Tested nowcast-dev running with XIOS-2:
* ./makenemo -n SalishSea clean
* ./makenemo -n SalishSea add_key "key_xios2"
* XIOS_HOME=/results/nowcast-sys/XIOS-2 ./makenemo -n SalishSea -m GCC_SALISH_MOAD -j8
* made XIOS-2 xml file symlinks in /results/nowcast-sys/runs/
Tested XIOS-2 netcdf4 deflation at level 4 instead of NEMO-Cmd deflate in nowcast-dev.
Major thrash to get nowcast-dev running w/ XIOS-2 on salish due to trying to use XIOS-1 executable.
Set up emergency nowcast-sys on orcinus and successfully tested download_weather 12 in it.
(SalishSea)


Tue 23-May-2017
^^^^^^^^^^^^^^^

Salish Sea tam mtg; see whiteboard.
Changed SalishSeaCmd so that ref namelists are copied to tmp run dir instead of symlinking; Michael's request.
(SalishSea)

Messed around with yapf in salishsea-site repo and decided that I prefer <0.16.2 re: line breaks at ends of function definitions and brackets coallescing.
Reviewed and buffed Idalia's sprint changes until bootstrap.min.js started failing with an SRI hash mismatch error.
(salishsea-site)


Wed 24-May-2017
^^^^^^^^^^^^^^^

See project work journal.
(GOMSS)

See project work journal.
(Resilient-C)

Finished migration to new CentOS7 server web532 (207.38.92.57):
* copied apache2 bin/ and modules/ from a new mod_wsgi-4.5.15/Python-3.5 app
* fixed paths in bin/ restart/start/stop files
* updated ~/bin/hg
(randopony)

Changed 43ravens.ca to use PNG log image instead of SVG to improve anti-aliasing.
(43ravens.ca)


Thu 25-May-2017
^^^^^^^^^^^^^^^

Ported change from SalishSeaCmd to NEMO-Cmd re: ref namelists copied to tmp run dir instead of symlinking.
(NEMO-Cmd)

Banter w/ Michael re: rtd duplicate builds; changed tools repo hook url on bitbucket to new rtd api, but no effect.
watch_NEMO forecast failed due to bad pid; re-ran make_forcing_links and download_results manually to restart automation.
make_plots forecast publish and make_feeds generated bogus storm surge alerts due to NaN sea surface height values.
Continued work on NEMO_Nowcast toy example docs:
* discovered that nemo_nowcast/workers/__init__.py was missing so workers are not installed via conda install.
* also discovered that toy example can't be run from a directory; need a ToyNowcast package
(SalishSea)

Added source images for 43ravens logo to 43ravens.ca repo.
Changed logo to use raven image without shadow.
Designed and ordered card from moo.com.
(43ravens.ca)


Fri 26-May-2017
^^^^^^^^^^^^^^^

Built and uploaded to gommss-nowcast anaconda.org channel build 3 of NEMO_Nowcast-1.4 re: overlooked workers/__init__.py.
Investigated make_plots forecast2 publish failure and found NaN sea surface height values.
Changed iodef.xml for nowcast-dev to use XIOS-2 "performance" buffer size.
Use resolved repo path in VCS revisions recording message about uncommitted changes in NEMO-Cmd; suggested by Michael.
Ran f2py for a case that Kyle was having trouble with, and got an importable shared library as is supposed to happen.
Worked on SalishSeaNowcast issue #38 re: changing watch_NEMO to be remotely launched instead of being launched by run_NEMO.
(SalishSea)

Biz dev re: GoMSS nowcast maintenance contract.
(43ravens)

Finished review and buffing of Idalia's sprint work and pulled it into production.
(salishsea-site)


Sat 27-May-2017
^^^^^^^^^^^^^^^

Hacked SalishSeaNowcast issue #38 changes to work only for nowcast-dev, scp-ed them to skookum, and restarted manager to load next_workers changes; it worked!!
Re-reviewed sprint commits that might impact nowcast production operations:
* addition of hourly nitrate thalweg & surface figures to make_plots
* addition of svg figures scouring to make_plots
All runs went NaN.
Migrated west.cloud runs to XIOS-2:
* update NEMO-3.6-code, XIOS-2
* clean SalishSea config, add key_xios2, build against XIOS-2
* clean SOG config, add key_xios2, build against XIOS-2
* clean SMELT config, add key_xios2, build against XIOS-2
* upadte NEMO-Cmd and pip install -e to move to v1.0
* update NEMO-forcing, NEMO_Nowcast
* upadte SalishSeaCmd and pip install -e to move to v3.1
* upadte SalishSeaNowcast, pip install -e to move to v3.3.dev0, manually apply bathy & coords patch that broke due to addition of lpe path
* update SS-run-sets, tools
nowcast, nowcast-dev, forecast & forecast2 runs work, but not nowcast-green (SOG)
Large sea surface height oscillations in nowcast, forecast, forecast2.
(SalishSea)


Sun 28-May-2017
^^^^^^^^^^^^^^^

Unsuccessful trash to try to get nowcast-green (SOG) working again.
Fixed SalishSeaCmd issue #5 re: expansion of envvars in namelist file paths.
(SalishSea)


Week 22
-------

Mon 29-May-2017
^^^^^^^^^^^^^^^

Continued unsuccessful trash to try to get nowcast-green (SOG) working again.
Ported SalishSeaCmd issue #5 re: expansion of envvars in namelist file paths to NEMO-Cmd.
Reviewed skookum:/results/ storage:
  df -h
  Filesystem                       Size  Used Avail Use% Mounted on
  /dev/md127p1                      11T   10T  306G  98% /results

  cd /results/
  ls
  erddap/  erddap-datasets/  forcing/  lost+found/  nowcast-sys/  observations/  SalishSea/
  skookum:results$ du -sh erddap
  1.4G  erddap
  skookum:results$ du -sh erddap-datasets/
  1.9M  erddap-datasets/
  skookum:results$ du -sh forcing/
  329G  forcing/
  skookum:results$ du -sh nowcast-sys/
  79G nowcast-sys/
  skookum:results$ sudo du -sh lost+found/
  [sudo] password for dlatorne:
  16K lost+found/
  skookum:results$ du -sh observations/
  103M  observations/
Started adding AGRIF support to SalishSeaCmd; completed w/ incremental functional testing by Michael:
  * AGRIF section
  * grid section
  * restart section w/ an outstanding bug
  * output section; pushed but untested
(SalishSea)

Discussed status of ONC observations collection and wave forecast publication w/ Rich.
(prediction-core)

Checked my /ocean mount (nfs3/userdict8/) in response to Michael's alert that it was full:
  ls
  buildbot/       ebooks/   hg_seminar/  notify/         SoG/           SOG-test/     trac/                YVR_relative_humidity
  buildbot-test/  f90play/  Jessica/     presentations/  SOG-buildbot/  SSMEP/        YVR_air_temperature
  CANYONS/        GYRE/     MEOPAR/      RiverDataDocs/  SOG-projects/  test_notify/  YVR_cloud_fraction
  skookum:dlatorne$ du -sh buildbot
  16G buildbot
  skookum:dlatorne$ du -sh buildbot-test/
  308K  buildbot-test/
  skookum:dlatorne$ du -sh CANYONS/
  1.3G  CANYONS/
  skookum:dlatorne$ du -sh ebooks/
  6.3M  ebooks/
  skookum:dlatorne$ du -sh f90play/
  392K  f90play/
  skookum:dlatorne$ du -sh GYRE/
  501M  GYRE/
  skookum:dlatorne$ du -sh hg_seminar/
  79M hg_seminar/
  skookum:dlatorne$ du -sh Jessica/
  64K Jessica/
  skookum:dlatorne$ du -sh MEOPAR/
  348G  MEOPAR/
  skookum:dlatorne$ du -sh notify/
  88K notify/
  skookum:dlatorne$ du -sh presentations/
  11M presentations/
  skookum:dlatorne$ du -sh RiverDataDocs/
  396K  RiverDataDocs/
  skookum:dlatorne$ du -sh SoG/
  2.0G  SoG/
  skookum:dlatorne$ du -sh SOG-buildbot/
  11G SOG-buildbot/
  skookum:dlatorne$ du -sh SOG-projects/
  726M  SOG-projects/
  skookum:dlatorne$ du -sh SOG-test/
  976K  SOG-test/
  skookum:dlatorne$ du -sh SSMEP/
  208K  SSMEP/
  skookum:dlatorne$ du -sh test_notify/
  92K test_notify/
  skookum:dlatorne$ du -sh trac/
  3.2M  trac/

Attended EOAS graduation lunch for Cindy, Kyle and Jie.


Tue 30-May-2017
^^^^^^^^^^^^^^^

Salish Sea team mtg; see whiteboard.
Discussed wind-driven surface currents w/ Ben re: my CMOs talk.
Continued adding AGRIF support to SalishSeaCmd; completed w/ incremental functional testing by Michael:
  * AGRIF section
  * grid section
  * restart section
  * output section
  * namelists section
  * docs
Worked w/ Susan to finally get nowcast-green running again on west.cloud; it was an XIOS-2 file_def.xml and field_def.xml mess, as well as needing the vertical advection sub-stepping mods to be added to SOG.
2 nowcast-green/26may17 attempts failed with errors at the end of the run.
(SalishSea)


Wed 31-May-2017
^^^^^^^^^^^^^^^

More attempts to get nowcast-green running on west.cloud:
  * Removed deflation from XIOS-2; ~7%/5min, saw memory spike to 14.5Gb virtual in final few seconds of run, and it failed to complete properly
  * Restored netcdf4 deflation and changed XIOS-2 from performance to memory mode for buffer optimization; 6.2Gb of virtual memory during run, ~6%/5min, finished in 1h24m compared to 1h25m for 15may17, weird black glitch in nitrate thalweg/salinity figure
  * Launched 27may17
Hacked next_workers on skookum to prevent launch of nowcast-dev; plan is to run it manually late in the day to make salish available for research runs, then automatically launch it after nowcast-green once it returns to stability.
Discovered that nowcast-dev has been Nan since 25may17; need to re-run w/ vertical advection sub-stepping that was introduced on 27may17.
Hacked make_plots to avoid missing and renamed files so that we get some figures for evaluation.
Started developing CMOS talk.
(SalishSea)

See project journal.
(gomss-nowcast)


Thu 1-Jun-2017
^^^^^^^^^^^^^^

See project journal.
(Resilient-C)

forecast2/31may17 ran w/ ConnectionError from NOAA tides and currents site in make_plots.
Launched nowcast-green/26may17 yet again after Susan's file_def.xml debugging session last night; it worked.
Removed most of the make_plots hacks re: missing files.
Symlinked /results/nowcast-green/ into /results/hindcast/ in hopes of adding >26may17 results to ubcSSg ERDDAP datasets; stopped and restarted ERDDAP; only works if the results file are hard linked.
Installed and activated ntpd west.cloud to keep time in sync, after manually updating time to remove accumulated drift.
Started nowcast-green catch-up:
* 27may17, 28may17, 29may17
Started nowcast-dev catch-up:
* 25may17
Continued work on CMOS talk.
(SalishSea)


Fri 2-Jun-2017
^^^^^^^^^^^^^^

Continued nowcast-green catch-up:
* 30may17 through 02jun17
Continued nowcast-dev catch-up:
* 26may17
Continued work on CMOS talk.
Finished ECget plug-in to scrape Fraser River water quality buoy data web page; deployed it as a cron job on salish that writes to /results/observations/ECCC/fraser_buoy.csv.
(SalishSea)

Westgrid townhall:
  Patrick Mann:
    * new systems are still in install stage; westgrid analysts haven't got logins yet
    * arbutus at UVic:
      * 100 Gb network upgrade in progress
    * cedar at SFU:
      * running Linpack benchmarks
    * graham at Waterloo:
      * same state as cedar
    * niagara at UofT:
      * still in RFP stage; delayed for new Intel processors
      * last and best offer phase
      * early 2018; 60k-70k cores
    * alpha access: next week for 1-2 wks; analysts and select users
    * beta-access:
      * all users
      * flat priority
      * system unstable; no uptime guarantees
      * scale-out, diverse usage, docs testing
      * report issues to support@computecanada.ca
      * http://status.computecanada.ca
    * RAC priorities effective in early July (production access)
    * storage:
      * silo interim operational
      * NDC:
        * PROJECT space
        * SFU 10 Pb, Waterloo 13 Pb
        * Object storage, geo-replicated, later in summer; large datasets
    * software stack
      * identical on cedar and graham via CVMFS; great for open-source, not so much for commercial
      * module (LMod) for env config
      * software list on docs wiki: https://docs.computecanada.ca/wiki/Available_software
    * new scheduler on cedar and graham: slurm
      * #SBATCH instead #PBS and new syntax for options
      * srun instead of mpirun
      * legacy systems will continue to use torque/moab
  Alex Razoumov, visualization and training coordinator
    * UBC summer school; 19-22 Jun
    * USask 24-27 Jul; full day on Chapel language (replacement for MPI)
    * both are in-person only


Sat 3-Jun-2017
^^^^^^^^^^^^^^

Set up Aquamacs w/ Flycheck, and MacTeX-2016 on hedi for Susan.

Continued nowcast-dev catch-up:
* 27may17, 28may-17
Finished on CMOS talk slides.
(SalishSea)


Sun 4-Jun-2017
^^^^^^^^^^^^^^

Travel to Toronto for CMOS conference.

get_NeahBay_ssh for forecast2 took long enough that it violated the concurrency assumptions and caused upload_forcing to fail; re-ran upload_forcing manually to restart automation.
Buffed Vicky and Michael's make_plots SVG scour code.
Continued nowcast-dev catch-up:
* 29may17
(SalishSea)

CMOS icebreaker; conversations w/
* Muriel Dunn
* Francis Poulin
* Dave Greenberg
* Paul Meyers
* CMOS podcast producer
* Elise Olson
* Blair Greenham
* Nancy Soontiens
* Shilliang Shan
* Doug ??? of RBR, ex-Neptune


June
====

Week 23
-------

Mon 5-jun-2017
^^^^^^^^^^^^^^

Continued nowcast-dev catch-up:
* 30may17
Buffed Birgit and Michael's make_plots hourly PNG figures for animations.
Discovered that yapf can't handle f-strings; fix will probably land w/ Python 3.6.2 in late June.
Caught Fraser buoy IndexError when it happened; due to empty wind direction table cell; added and deployed exception handling.
Started moving SS-run-sets dir from run_NEMO hard-code to config file.
(SalishSea)

CMOS:
  Plenaries
  Phys Ocgy 1
  Phys Ocgy 2
  Posters


Tue 6-jun-2017
^^^^^^^^^^^^^^

Continued nowcast-dev catch-up:
* 01jun17
Landed changesets since 16-May sprint into production.
(SalishSea)

CMOS:
  Plenaries
  Patterson Lunch


Wed 7-jun-2017
^^^^^^^^^^^^^^

Continued nowcast-dev catch-up:
* 02jun17, 03jun17
Landed changesets since 16-May sprint into production.
(SalishSea)

CMOS:
  Plenaries
  Collaboration, incl my talk
  Long convo w/ Neil Swart & Fred Dupont
  Posters
  AI Analysis of Climate Model Results
  Coastal Ocgy
  Banquet


Thu 8-jun-2017
^^^^^^^^^^^^^^

Continued nowcast-dev catch-up:
* 04jun17, 05jun17
(SalishSea)

Lunch w/ Muriel Dunn to duscuss code testing, documentation, and release mgmt for the RBR Matlab toolkit she is developing.
NEMO Community of Practice meeting.
(prediction-core)

CMOS:
  Plenaries
  Numerical Methods
  NEMO Community of Practice

Travelled to Barrie

wefaction server was migrated to web621; cyclelog, douglatornell.ca, and phpgedview are temporarily broken.


Fri 9-Jun-17
^^^^^^^^^^^^

Visiting M&D in Barrie

Continued nowcast-dev catch-up:
* 06jun17, 07jun17
(SalishSea)


Sat 10-Jun-17
^^^^^^^^^^^^^

McMichael Collection and KCVI reunion in Markham

Continued nowcast-dev catch-up:
* 08jun17, 09jun17
(SalishSea)


Sun 11-Jun-2017
^^^^^^^^^^^^^^^

Visiting M&D in Barrie

EOAS network went down due to flood from ESB 4th floor pipe break; nowcast system was stopped dead due to lack of access to auth system; recover:
* Confirmed fallback of running download_weather on orcinus for 06 and 12
* network came back by 17:00
* download_weather 06 to restart automation for very late forecast2 run
* upload_forcing forecast2 failed due to missing 10jun17 obs; symlinked fcst/10jun17 as obs/
* upload_forcing forecast2 restarted automation
* 90 minutes later... download_weather 12 to trigger nowcast, etc. for the day
Continued nowcast-dev catch-up:
* 10jun17
(SalishSea)


Week 24
-------

Mon 12-Jun-2017
^^^^^^^^^^^^^^^

Visiting M&D in Barrie

Continued nowcast-dev catch-up:
* 11jun17, 12jun17
Restarted erddap after overnight failure of nowcast-green time series figures; re-ran make_plots nowcast-green research manually.
(SalishSea)


Tue 13-Jun-2017
^^^^^^^^^^^^^^^

Travel from Barrie to Vancouver

Finished moving SS-run-sets dir from run_NEMO hard-code to config file.
Finished nowcast-dev catch-up w/ manual 13jun17 run, then re-enabled automation to launch run after nowcast-green.
(SalishSea)


Wed 14-Jun-2017
^^^^^^^^^^^^^^^

Took Allens to YVR

Fixed bug in unexpected exception handling in make_plots figure rendering so that figure module issues don't pass silently.
Cleaned up a bunch of other figure issues introduced by pulling sprint code into production.
Continued rework of run section of nowcast config re: issue #12.
(SalishSea)


Thu 15-Jun-2017
^^^^^^^^^^^^^^^

Fixed bugs introduced yesterday by moving run prep dir path into enabled hosts section of nowcast config; manually re-ran make_forcing_links forecast2 to retart automation.
Finished rework of run section of nowcast config re: issue #12.
Changed nowcast-dev back to use XIOS-2 performance mode for buffer size.
Enabled bathymetry, mesh mask & LPE files to be host-specific; re: issue #32.
Enabled coordinates file path to be host-specific; re: issue #31.
Reviewed sprint commits in SalishSeaTools and did some buffing; also thrashed unsuccessfully on getting module and function indices to work.
Pulled tools changes since sprint into production.
Experimented w/ closing figure objects to avoid matplotlib.pyplot memory use warning; root cause is that we are using matplotlib.pyplot.figure to create Figure objects.
(SalishSea)


Fri 16-Jun-2017
^^^^^^^^^^^^^^^

Discovered that cedar and graham now ping, but auth fails.

Fixed ww3 prep bugs introduced yesterday in nowcast run config restructuring; manually re-ran make_ww3_wind_file and make_ww3_current_file forecast2 to retart automation.
Started work on grouping figures in salishsea-site app.
(SalishSea)

Email conversation w/ Marlene@ONC about her move to CHS.

See project journal.
(gomss-nowcast)

See project journal.
(Resilient-C)

Reviewed agenda for MEOPAR ASM next week.
Skimmed MEOPAR prediction core mission and reporting document on Google Drive.
(prediction-core)


Sat 17-Jun-2017
^^^^^^^^^^^^^^^

Deployed prototype of grouped figures for ONC VENUS node T&S figures on comparison pate.
(SalishSea)

Worked on contributions to the MEOPAR prediction core mission and reporting document:
* Added research support activities
* Started adding code repos, docs sites, and release channels
(prediction-core)


Sun 18-Jun-2017
^^^^^^^^^^^^^^^

Finalized expenses for CMOS trip.
Hard-linked nowcast-green/27may17 results files into hindcast/ to test if time series figures are failing because of gap, or because of only 1 day in past 30; make_plots still fails, so the problem is likely the gap; re-ran make_plots for 2016-09-23 and the failure was still there, so it is not the gap either.
Ran time series figures test notebook; failed.
Ran time series figures dev notebook; failed untile I poed at it for a while, then it worked w/ no evident change (Heisenbug?); did identify off-by-one error in time series end date.
Refactored time_series_plots module, and cleaned up corresponding code in make_plots worker.
Created hard links in hindcast for nowcast-green/28may17 through 18jun17 and ran make_plots nowcast-green research against them.
(SalishSea)

Worked on contributions to the MEOPAR prediction core mission and reporting document:
* Continued adding code repos, docs sites, and release channels
(prediction-core)

See project journal.
(gomss-nowcast)

Worked on post-migration of apps on webfaction (now on centOS 7.3):
* got douglatornell.ca functional again by creating a new static douglatornell_blogofile app and rsync-ing files from djl_static/ into it; deleted djl_static app
* used easy_install-2.7 to install pip-2.7
* used pip-2.7 to update mercurial to 4.2.1
* created a Django 1.11.2 mod_wsgi 4.5.15 Python 2.7 tempalte app to get new apache2 files for cyclelog from
* hacked on cyclelog httpd.conf with comparison to django template until I got cyclelog running
* followed migration docs to remove php53 lines from .htaccess and deleted php53.cgi symlink to get phpgedview working


Week 25
-------

Mon 19-Jun-2017
^^^^^^^^^^^^^^^

Travel to Montréal for MEOPAR ASM

Added handling for missing Fraser River water quality buoy values or units to ECget re: a series of missing relative humidity values.
make_plots nowcast-green failed due to ERDDAP issue; restarted ERDDAP and re-ran worker manually.
Charles started storage upgrade on skookum & salish.
(SalishSea)


Tue 20-Jun-2017
^^^^^^^^^^^^^^^

Work day at Le Westin Montréal

Updated EOAS TODOs spreadsheet.
(SalishSea)

See project journal.
(Resilient-C)

MEOPAR ASM reception and HQP Posters
(prediction-core)

nowcast system failed at ~13:00 PDT due to full /results; recover:
* circusctl quit
* circus --daemon $NOWCAST_CONFIG/circus.ini
* make_forcing_links nowcast-green; nowcast-green run on west.cloud launched, but watch_NEMO launch got stuck
* make_forcing_links salish-nowcast nowcast+; nowcast-dev run on salish launched, and watch_NEMO for it also launched
* download_weather 18
* watch_NEMO for nowcast-green was blocked by a zombie watch_NEMO for the forecast run; killed that violently and manually launched watch_NEMO for nowcast-green to get automation fully back in operation
(SalishSea)


Wed 21-Jun-2017
^^^^^^^^^^^^^^^

MEOPAR ASM

Sessions.
Conversations w/ Bernard Denis (Chief of ECCC Numerical Weather Modeling section) about HRDPS; need to send email to him re: datamart bandwidth.
Lunch w/ Will Perry and Johannes Gimmerich and got them talking about Salish Sea Wave model.
(prediction-core)

See project journal.
(Resilient-C)

Worked w/ Charles on skookum issues after he shifted us to the new 19Tb /results storage mount.
Recovery:
* download_weather 12
* download_results forecast --run-date 2017-06-20 --debug
* make_plots forecast publish --run-date 2017-06-20 --debug

https://salishsea.eos.ubc.ca/storm-surge/forecast goes 404 when there is no recent forecast or forecast2 figures.
(SalishSea)


Thu 22-Jun-2017
^^^^^^^^^^^^^^^

MEOPAR ASM

(prediction-core)

See project journal.
(Resilient-C)

Continued backfilling after /results storage upgrade:
* download_results nowcast --run-date 2017-06-20 --debug
Added ping_erddap worker to handle v17-02 datasets after nowcast-green runs.
Added temporary code to download_results worker to hard link nowcast-green files for datasets into hindcast/ results dir.
(SalishSea)

Travel to Vancouver from MEOPAR ASM


Fri 23-Jun-2017
^^^^^^^^^^^^^^^

Emailed Ryan re: app shutdown due to continued memory usage beyond account limit;
deeper investigation showed that database app had done a memory run-away; restarted pony app.
(randopony)

Continued backfilling after /results storage upgrade:
* make_plots nowcast publish --run-date 2017-06-20 --debug
* make_plots nowcast comparison --run-date 2017-06-20 --debug
* make_plots nowcast research --run-date 2017-06-20 --debug
Worked on cleaning up file and directory permissions that got corrupted during /results storage upgrade; lots of files that shouldn't be are executable w/ sticky bit set, and lots of directories are not group writable and don't have sticky bit set.
Added temporary download_results worker hard link nowcast-green files for datasets into hindcast/ results dir feature in production.
Worked on setup of environments on graham and cedar:
* add cacerts = /etc/pki/tls/certs/ca-bundle.crt to [web] section of .hgrc
* clone repos
* load python27-scipy-stack/2017a module
* load netcdf/4.4.1.1 module
* pip install SalishSeaTools, NEMO-Cmd, SalishSeaCmd
* can use completion for nemo and salishsea command processors
* load perl/5.22.2 module before building XIOS-2; shouw be added to .env
* built XIOS-2
(SalishSea)

Moved 2fa for google, github, bitbucket and slack to authy, and added 2fa to twitter.


Sat 24-Jun-2017
^^^^^^^^^^^^^^^

Continued work on setup of environments on graham and cedar:
* module loads required to build NEMO: perl/5.22.2 netcdf-mpi/4.4.1.1 netcdf-fortran-mpi/4.4.4
* built NEMO
* built REBUILD_NEMO
Ran hindcast/29aug16 set up by Susan w/ slurm directives:
  #SBATCH --job-name=29aug16_hindcast
  #SBATCH --ntasks=156
  #SBATCH --mem-per-cpu=2000M
  #SBATCH --time=02:00:00
  #SBATCH --mail-type=ALL
  #SBATCH --mail-user=dlatornell@eoas.ubc.ca
  #SBATCH --ignore-pbs
Run w/ 1 xios processor took ~25min w/o post-processing; Susan says ~2x jasper speed; performance ratio was 35-40%.
Need to figure out:
* how to get email from slurm
* how to direct stdout and stderr to results dir
Need to load nco/4.6.6 module before running salishsea deflate, but note that it replaces netcdf-*-mpi modules with sequential output variants.
Run w/ 3 xios processors wasn't noticeably faster, but the reported performance ratio was 15-20%
Run w/ 10 xios processors wasn't noticeably faster, but the reported performance ratio was 10-20%.
Run w/ 1 xios processor, 0.18 buffer size factor, and 4000M memory per cpu timed out after 40min.
Started adding code to SalishSeaCmd to enable it to be used on cedar/graham.
(SalishSea)

Picked Allens up at YVR and took them to Parksville.


Sun 25-Jun-2017
^^^^^^^^^^^^^^^

Continued adding code to SalishSeaCmd to enable it to be used on cedar/graham.
Run w/ 1 xios processor, 0.18 buffer size factor, and 4000M memory per cpu took 32min, and reported xios performance ratio of 15-30%.
Re-ran w/ 1 xios processor, 0.12 buffer size factor, and 2000M memory per cpu; but run failed on launch due to a node issue.
Added 2 straits (JdF and SoG) 20min avg surface (top 5 layers) slab for Hauke@UVic to nowcast-dev as of 26jun17.
Restored ONC Central node CTD data downloads to automation and backfilled; node came back online on 23jun17.
(SalishSea)

Travel home from Parksville.


Week 26
-------

Mon 26-Jun-2017
^^^^^^^^^^^^^^^

Re-ran w/ 1 xios processor, 0.12 buffer size factor, and 2000M memory per cpu; timed out after 2h :-(
Resumed work on getting ONC ferry data into ERDDAP; got on-crossing boolean mask, and crossing number assignment worked out, then collided with a 404 from the ONC stations web service.
(SalishSea)

Gave Phys Ocgy seminar based on CMOS NEMO_Nowcast talk.


Tue 27-Jun-2017
^^^^^^^^^^^^^^^

Salish Sea team mtg; see whiteboard.
Sat in on CONCEPTS monthly science call; Susan presented.\
Re-ran w/ 1 xios processor, 0.12 buffer size factor, and 2000M memory per cpu; got 25m502s MPI and 32m03s total.
Tried 5 xios processors, 0.12 buffer size factor, and 2000M memory per cpu; got immediate fail.
Continued work on getting ONC ferry data into ERDDAP; sent email to Mike@ONC re: stations API 404; accidental blocking by ONC dev of new API.
Restarted ERDDAP to make make_plots nowcast-green time series happy.
(SalishSea)

Added time series figures page to salishsea-site.
Worked on backfilling nowcast-green research figures.
(salishsea-site)

Attended GEOTRACES team mtg.
(GEOTRACES)


Wed 28-Jun-2017
^^^^^^^^^^^^^^^

Cycled to UBC w/ Susan and home again for training.

Helped Elise w/ mercurial branch issue.

Updated pyramid-crow and raven versions in salishsea-site env.
Created issue #5 from sentry re: no ONC VENUS figures on current date breaking comparison page.
(salishsea-site)

See project journal.
(Resilient-C)

Set up a douglatornell.ca conda env with blogofile and blogofile_blog installed from git clones in warehouse/python/; pleased that it all still works 3yrs after my last commit to the site. Started updating site.
(douglatornell.ca)

Farewell dinner at Bridges for Melanie and Romain.


Thu 29-Jun-2017
^^^^^^^^^^^^^^^

See project journal.
(Resilient-C)

Swapped desks at UBC.

Re-tried 5 xios processors, 0.12 buffer size factor, and 2000M memory per cpu; got .
(SalishSea)

Refactored figure grouping Mako code.
Started trying to integrate EC ImageLoop JavaScript module into app.
(salishsea-site)


Fri 30-Jun-2017
^^^^^^^^^^^^^^^

See project journal.
(Resilient-C)

See project journal.
(gomss-nowcast)

Started work on changing from Stormpath auth to in-app; migration steps required on production:
* pip install passqlib
* rename admins column persona_email to email:
    BEGIN TRANSACTION;
    DROP INDEX ix_admins_persona_email;
    CREATE TABLE adminsb531
    (
        id INTEGER PRIMARY KEY NOT NULL,
        email TEXT UNIQUE NOT NULL
    );
    INSERT INTO adminsb531(id, email) SELECT id, persona_email FROM admins;
    DROP TABLE admins;
    ALTER TABLE adminsb531 RENAME TO admins;
    COMMIT;
* add indexed admins column password_hash:
    ALTER TABLE admins ADD password_hash TEXT DEFAULT '' NOT NULL;
    CREATE INDEX admins_password_hash_index ON admins (password_hash);
(randopony)


July
====

Week 27
-------

Mon 3-Jul-2016
^^^^^^^^^^^^^^

**Statutory Holiday** - Canada Day lieu day

Moved weather download constants from download_weather to config file.
Changed weather downloads server from dd.weather to dd.beta.weather.
(SalishSea)


Tue 4-Jul-2017
^^^^^^^^^^^^^^

Continued integration of EC ImageLoop JavaScript module into app.
(salishsea-site)

Salish Sea team mtg; see whiteboard.
Ordered 8Tb drive from Amazon for ECCC to put GEM2.5 archive on for us.
(SalishSea)


Wed 5-Jul-2017
^^^^^^^^^^^^^^

Received 8Tb drive and delivered it to Robert Nissen at ECCC downtown.
(SalishSea)

Finished changing admin auth to in-app implementation re: Stormpath acquisition by Okta and no good migration path from Stormpath to Okta SDK.
(randopony)


Thu 6-Jul-2017
^^^^^^^^^^^^^^

Finished and released initial integration of EC ImageLoop JavaScript module into app.
(salishsea-site)


Fri 7-Jul-2017
^^^^^^^^^^^^^^

Reviewed Michael's ncks -> ncopy pull request for NEMO-Cmd deflate plug-in.
Did log analysis to compare weather download times among forecasts, and between dd.weather and dd.beta.weather:
dd.weather 2-3 Jul:
* 12: 10:39:40 to 12:11:15 = 1:31:35
* 18: 17:01:01 to 18:03:29 = 1:02:28
* 00: 23:00:16 to 00:16:48 = 1:16:32
* 06: 04:15:30 to 05:39:14 = 1:23:44
dd.beta.weather 6-7 Jul:
* 12: 10:43:50 to 12:21:08 = 1:37:18
* 18: 17:00:24 to 18:13:10 = 1:12:46
* 00: 23:00:32 to 00:23:08 = 1:22:36
* 06: 04:15:46 to 05:49:58 = 1:34:12
Concluded that the dramatic difference I thought existed for 12 comared to other forecasts is not there, and ss.beta is perhaps slightly slower than dd.
Did log analysis to compare results downloads from west.cloud before and after change to arbutus 100Gb switch:
before, foreacst2/05jul17:
* 06:29:42 to 06:31:57 = 02:15
after, foreacst2/06jul17:
* 06:31:26 to 06:34:11 = 02:45
Concluded no difference, or slower :-(
Improved make_plots worker to generate image files for image loop figures, and deleted rendering of hr=19 snapshot of nitrate on thalweg and surface in favour of image loop.
Pulled into production Susan's changes to add total cloud GRIB variable to download_weather and grib_to_netcdf workers; should be effective for 08jul17/00 forecast.
(SalishSea)

Pushed 2017.1 to production re: change to in-app admin auth.
Deleted app from Stormpath API dashboard.
(randopony)

Added robots.txt route, view, and template to try to reduce search engine bot traffic to ERDDAP; template is based on https://coastwatch.pfeg.noaa.gov/erddap/download/setup.html#organizations
(salishsea-site)

Added ERDDAP near-surface u&v velocity slab datasets from nowcast-dev for Hauke@UVic.
Added nowcast-dev option to ping_erddap re: near-surface slab, and hooked it into after_watch_NEMO().
(prediction-core)


Sat 8-Jul-2017
^^^^^^^^^^^^^^

Confirmed that total cloud GRIB files are being downloaded, and that percentcloud variable is now present in ops*.nc files.
Restarted manager to ensure that after_watch_NEMO nowcast-dev will launch ping_erddap.
Checked ERDDAP traffic sources with the handy one-linner:
  nslookup $IP |awk -F"= " '/name/{print $2}'
Changed run_ww3 worker to return run exec command to checklist instead of trying to look up run pid; re: issue #38.
Started development of make_turbidity_file worker.
(SalishSea)


Sun 9-Jul-2017
^^^^^^^^^^^^^^

Continued development of make_turbidity_file worker.
(SalishSea)


Week 28
-------

Mon 10-Jul-2017
^^^^^^^^^^^^^^^

Continued development of make_turbidity_file worker.
(SalishSea)

Telcon w/ Jackie Dawson @UOttawa (see biz journal).

Added aria labels to image loop controls, and make image loop elements responsive instead of fixed width and height.
Refactored FigureMetadata to provide a separate FigureGroup object that is a collection of FigureMetadata instances with a group description; FigureGroup is an iterator to eliminate frivolous zero-indexes.
Made ImageLoop a trivial iterator to eliminate frivolous zero-indexes.
(salishsea-site)


Tue 11-Jul-2017
^^^^^^^^^^^^^^^

Attended in Google Cloud Onboard training day at Sheraton Wall Centre.


Wed 12-Jul-2017
^^^^^^^^^^^^^^^

Westgrid townhall and cedar demo:
Patrick Mann:
* introduced lots of analysts
* email questions to info@westgrid.ca
* cedar/graham known issues:
  * page on wiki
  * nearline not yet operational
  * /project/<userid> available (1Tb) but no allocations effective
  * email notifications working in cedar but soon on graham
  * slurm fully operational
  * scheduling is leaving unused nodes (due to options people are using - better below):
    * whole nodes preferred: --nodes=4 --ntasks-per-node=32
    * partitions: by-core, by-node (latter is much bigger)
    * short run times preferred: --time=DD-HH:MM or HH:MM:SS
    * partitions: 3, 12, 24, 72, 168, 672 hrs
  * --account becomes a required option if you have an allocation on cedar/graham because default is also an account
  * srun (preferred) knows more about node groupings than mpirun
* jasper will be defunded on 1-Oct-2017
* bugaboo storage is full
* 19-Jul webinar on cedar/graham scheduling (Kamil)
Alex Razoumov:
* cedar will be expanded to 66k CPUs (132k cores) in 2018
* storage:
  * /home: 50Gb, nightly backup, medium performance, mounted on compute
  * /scratch: no quota, no backup, purged, high performance, mounted on compute
  * /project: (1Tb w/o RAC), mounted on compute
  * /local-scratch (will become /tmpdir): no quota, ~1Tb(?) capacity, very high performance, available for job duration only
* modules:
  * module spider
  * module show
* use gridftp for large (size/number) file transfers
* globus web gui does background transfers
* compilers:
  * mpifort, mpicc, mpiCC
* slurm:
  * sbatch, squeue, sacct
  * array jobs: collections of serial jobs; easier for scheduler
* sacct:
  * MaxRSS not guaranteed to catch spikes
* interactive jobs:
  * salloc --time --ntasks
* slurm memory:
  * use sacct to get info
* use -O2 or -O3 optimization
* avoid large ascii files
* Kamil is developing a slurm version of his 9h scheduling webinar
* /scratch purge schedule is not well defined yet; clean up after use

Restarted ERDDAP to make make_plots nowcast-green time series happy.
(SalishSea)


Thu 13-Jul-2017
^^^^^^^^^^^^^^^

See work journal.
(Resilient-C)

Started work on expense claim for CMOS trip.

Met w/ Elise re: make_turbidity_file worker.
Discussed EPOC mtg w/ Susan.
Advised Elise on how to integrate LiveOcean nutrient boundary conditions file calculations into make_live_ocean_files worker.
Emailed UBC_subdomain module to Parker@UW.
Tried to set up SalishSea AGRIF on cedar, but its login nodes are down due to a router issue; got some setup done when cedar came back online:
* NEMO-forcing-BS2
* NEMO-forcing-HS1
Started porting AGRIF handling code from SalishSeaCmd to NEMO-Cmd re: issue #23; also started identifying functions that could be refactored into a public prepare plug-in library module in NEMO-Cmd for use by SalishSeaCmd.
(SalishSea)

Attended part of canyons group mtg.
(canyons)

Emailed links to grib_to_netcdf and our results and ERDDAP surface forcing datasets to Robert@ECCC.
(prediction-core)


Fri 14-Jul-2017
^^^^^^^^^^^^^^^

**Vacation** - Cycletour to Tsawwassen, Saltspring Is, Cheamainus, Parksville, Nanaimo


Sat 15-Jul-2017
^^^^^^^^^^^^^^^

**Vacation** - Cycletour to Tsawwassen, Saltspring Is, Cheamainus, Parksville, Nanaimo


Sun 16-Jul-2017
^^^^^^^^^^^^^^^

**Vacation** - Cycletour to Tsawwassen, Saltspring Is, Cheamainus, Parksville, Nanaimo

Helped Susan test Michael's NEMO-Cmd ncks -> nccopy change on bugaboo and found inconsistency in nccopy UI re: netcdf format selection.
(SalishSea)


Week 29
-------

Mon 17-Jul-2017
^^^^^^^^^^^^^^^

Registered an orchid.org id so SWC can use it for lesson contribution attribution.

Restarted ERDDAP to make make_plots nowcast-green time series happy.
Continued to set up SalishSea AGRIF on cedar:
* rsync NEMO-forcing-MD
* makenemo -n SalishSeaAGRIF
* Ran several 10min test runs:
  * need to use --account because Susan seems to have a non-default allocation on cedar
  * confirmed that --output and --error now work and added them to SalishSeaCmd run
  * experimented with directives to use full nodes, all memory per node
  * email to support re: how to write srun commands
Started work on SalishSeaForcing repo, a slimmed, public version of NEMO-forcing;
discussed how w/ Susan.
(SalishSea)

Started work on private AGRIF repo.
(MOAD)

See project work journal.
(GOMSS)

Tue 18-Jul-2017
^^^^^^^^^^^^^^^

Email discussion of distribution of deflation process4es to cores w/ Michael.
Emailed Parker re: him running UBC_subdomain.py for us; he agrees he will.
SalishSea team mtg; see whiteboard.
download_weather 12 timed out; re-ran manually to restart automation.
Continued working w/ SalishSeaAGRIF on cedar:
* Set up SS-run-sets/SalishSea/djl/SalishSeaAGRIF/
* lots of namelist sections that should(?) be standard are different:
  * namelist.domain
  * namelist.dynamics
  * namelist.lateral
  * namelist.surface
  * namelist.bottom
* got run to work from a single atmospheric forcing tree instead of 3; it would be good to automate the creation of the sub-grid number prefixed weights file symlink.
* submitted 4d run from my setup to compare w/ Michael/Vicky's results
Noted that 50Gb of /home storage is not much (a core dump run failure consumes >25Gb); it turns out that /project (1Tb default) is mounted on the compute nodes, so we should make more use of it.
(SalishSea)


Wed 19-Jul-2017
^^^^^^^^^^^^^^^

SHARCNET web seminar "How jobs are scheduled to run on Graham and Cedar":
James Desjardin, BrockU:
* compute canada intro playlist at youtube
* scheduler plays "world's most complex game of tetris"
* allocation is by core-years; billing is by core & memory e.g. 1 core but full node mem == full node cost
* queue priority: job size/shape, age, fair-share, partitions
* fair-share:
  * based on usage share target
  * fair-share ranges between 0 and 1
  * 0.5 == on par w/ target
  * toward 0 == usage ahead of target
  * toward 1 == usage behind target
  * RACs and RRGs get specified share targets, residual is divided equally for RASs
  * design is for 80% RAC/RRG utilization
  * fair-share usage impact decay rate is presently 50% in 14d
* partitions:
  * allow for job shapes to interact w/ priority on subsets of nodes
  * runtime: 3h, 12h, 1d, 3d, 7d, 28d
  * backfilling: run low priority jobs than can finish before any higher priority job can begin
  * by-node/by-core:
    * by-node jobs can perform better
    * by-core jobs have more opportunity to run
* job monitoring:
  * squeue -u userid
  * squeue -j jobid
  * sstat jobid
    * utilization during job execution
  * sacct jobid
    * utilization after job completion
  * squeue -P --sort=-p,i --states=PD | less
  * scontrol show partition | less
  * sinfo | less
  * sshare
* scheduling configuration policies are being adjusted to maximize utilization and performance of clusters
* job profiling tools like Remora
* optimize your job shapes by profiling, scaling tests, etc.

Continued working w/ SalishSeaAGRIF on cedar:
* set up /project/$USER/MEOPAR/ storage
* confirmed that /project/$USER/ is *not* mirrored between cedar and graham
* successfully ran 10m job from /project
Worked out a useful squeue format:
  squeue -o "%.18i %.8u %.7a %.20j %.2t %.9r %.19S %.10M %.10L %.6D %.5C"
Email from Parker says that LiveOcean daily avg files for our domain boundary (low_passed_UBC.nc) will be available by about 07:20 starting tomorrow.
(SalishSea)


Thu 20-Jul-2017
^^^^^^^^^^^^^^^

Downloaded LiveOcean low_passed_UBC.nc files for 19 & 20 Jul.
Created task lists for:
* Change LiveOcean to daily avg & add nutrient BCs
* Add Fraser River turbidity forcing
* Deploy SalishSeaAGRIF for Baynes Sound and Haro Strait sub-grid to nowcast production
Updated arch file and built SalishSeaAGRIF on west.cloud.
skookum bounced re: new RAID installation; thrash when it came back re: .ssh/old_keys/nefos-sshfs_id_rsa and too many auth failure between nowcast0 and compute nodes.
Added low_passed_UBC.nc to download_live_ocean worker and tested it on skookum.
Started work on watch_ww3 worker.
Created grid, rivers, tides & tracers repos to receive parts of the bloated NEMO-forcing repo.
(SalishSea)


Fri 21-Jul-2017
^^^^^^^^^^^^^^^

root filesystem on skookum is full; opened ticket
Worked w/ Susan on testing daily avg LiveOcean TS boundary conditions.
Opened port for watch_ww3 worker on west.cloud.
Was able to launch the long-missing nowcast3 instance on west.cloud; refreshed my memory about MPI decomposition and VM count profiling on west.cloud and the fact that fewer VMs turned out to be faster, so didn't put nowcast3 into service.
Prepared west.cloud to test watch_ww3 worker.
Restarted nowcast and salishsea-site app after Charles killed them to resolve full root filesystem issue; also had to manually re-run download_weather 12.
Ordered 2x8Tb drive to archive old stuff from /results.
Experimented with srun --multi-prog on cedar; 3 nodes, all memory, 30 nemo tasks and 2 xios tasks per node;
Elise discovered that fraser_buoy.csv file is empty; uniq over-wrote it :-( removed uniq from cron script and requested backup recovery from Charles.
Tested and debugged watch_ww3 worker.
Worked on production SalishSeaAGRIF configuration on salish.
(SalishSea)


Sat 22-Jul-2017
^^^^^^^^^^^^^^^

Got --multi-prog test cases working on cedar but couldnt' work on nemo.xios due to disk quota issue; opened ticket.
Removed LiveOcean hourly downloads from download_live_ocean, and changed it to be launched after download_weather.
Helped Susan test make_live_ocean_files worker operating on daily files instead of hourly.
(SalishSea)

Prep for trip to Norway.


Sun 23-Jul-2017
^^^^^^^^^^^^^^^

2x8Tb drives for /results archive delivered; formatted them via instructions from Robert@ECCC:
  dmesg | grep sd[a-z]1 told me that the drive was mounted as sdc
  # unmount the drive
  sudo parted /dev/sdc
  (parted) mklabel gpt
  (parted) unit Tb
  (parted) mkpart primary 0.00TB 8.00TB
  (parted) print
  (parted) quit
  sudo mkfs.ext4 /dev/sdc1
Discovered that 2nd drive was 4Tb; initiated return/replacement process.
(SalishSea)


Week 30
-------

Mon 24-Jul-2017
^^^^^^^^^^^^^^^

Got cedar /project storage quota issue sorted out; caused by confusing symlinks.
Merged Michael's NEMO-Cmd PR#2 re: changing from ncks to nccopy in deflate plugin.
Helped Elise w/ LiveOcean biology boundary conditions and turbidity forcing nowcast workers.
Submitted expense claim for 3x8Tb external backup drives.
Set up new ~/project/dlatorne/MEOPAR/ and ~/project/SalishSea/forcing/ trees on cedar.
Helped Susan start /results archiving to external backup drives.
Built prototype SalishSeaAGRIF namelists and XML files tree.
(SalishSea)

Set up UBC_MOAD/ariane-2.2.6_00 repo on bitbucket.
(MOAD)

Attended Phys Ocgy seminar by Birgit on MN, Ga & Pb tracer modeling in the CAA.

Worked w/ Susan on expense claims.

Merged pull requests in hg lesson re: template updates and mercurial link URLs.
(swc)

See project work journal.
(SoG-waves)


Tue 25-Jul-2017
^^^^^^^^^^^^^^^

Restored column headings line to fraser_buoy.csv file.
Salish Sea team mtg; see whiteboard.
Backed out commit that temporarily hard linked nowcast-green results into hindcast results directory because of time series figures ERDDAP issues, and hindcast almost caught up to real time.
Temporarily disabled time series figures due to ERDDAP issues.
Deleted hard linked nowcast-green results from hindcast results directory to make way for hindcast approach to real time.
Prepared for 1d SalishSeaAGRIF 2 sub-grid test on west.cloud.
Worked on setting up nowcast/24jul17 run on cedar to test --multi-prog, etc; salishsea prepare was incredibly slow.
download_weather18 failed twice due to lack of files on ECCC server.
Continued porting AGRIF handling code from SalishSeaCmd to NEMO-Cmd re: issue #23.
(SalishSea)

Submitted expense claim for CMOS trip.

Worked on expense claim for MEOPAR ASM trip.

See project work journal.
(SoG-waves)


Wed 26-Jul-2017
^^^^^^^^^^^^^^^

Dentist appt and haircut.

Overnight SalishSeaAGRIF run on west.cloud completed 257 time steps in ~30min before (probably) running out of memory on the XIOS-2 server.
Set up another SalishSeaAGRIF run on west.cloud with 2 xios servers.
salishsea prepare issue on cedar was due to a non-existent repo path; fixed bug.
No successful srun nowcast runs on cedar; tried an mpirun on 1 full node.
(SalishSea)


Thu 27-Jul-2017
^^^^^^^^^^^^^^^

Overnight SalishSeaAGRIF run on west.cloud completed 261 time steps, unclear why it stopped; tried another run w/ 3 xios servers and it stopped after 222 time steps.
1d nowcast mpirun on 1 full node on cedar aborted after 53min; worked on analysis w/ Susan.
Deleted /results/SalishSea/forecast2-3.4/ after Susan finished archiving it to an 8Tb external drive and /ocean/sallen/...
Discussed AGRIF w/ Michael, and bid him farewell.
Populated new tracers repo w/ initialization and boundary conditions fields files from bloated NEMO-forcing repo.
Populated new tides repo w/ boundary conditions fields files from bloated NEMO-forcing repo.
SalishSeaAGRIF run on west.cloud w/ xios buffer factor reduced to 0.125 completed 331 time steps, then zonal velocity in Baynes Sound sub-grid blew up.
(SalishSea)

Helped Birgit sort out her NEMO-3.6-code merge and rebase issue.
(GEOTRACES)

Attended canyons group mtg.
(Canyons)

See biz journal.
(Arctic Corridors)


Fri 28-Jul-2017
^^^^^^^^^^^^^^^

Travel to Tromsø

Sat 29-Jul-2017
^^^^^^^^^^^^^^^

Travel to Tromsø

Sun 30-Jul-2017
^^^^^^^^^^^^^^^

Tromsø

August
======

Week 31
-------

Mon 31-Jul-2017
^^^^^^^^^^^^^^^

Cycled from Tromsø to Sommarøy

Tue 1-Aug-2017
^^^^^^^^^^^^^^

Cycled from Sommarøy to Mefjordvær

Wed 2-Aug-2017
^^^^^^^^^^^^^^

Cycled from Mefjordvær to Hamn

Thu 3-Aug-2017
^^^^^^^^^^^^^^

Cycled from Hamn to Andenes

Fri 4-Aug-2017
^^^^^^^^^^^^^^

Cycled from Andenes to Bø

Sat 5-Aug-2017
^^^^^^^^^^^^^^

Cycled from Bø to Sortland

Sun 6-Aug-2017
^^^^^^^^^^^^^^

Cycled from Sortland to Svolvær


Week 32
-------

Mon 7-Aug-2017
^^^^^^^^^^^^^^

Travel to Oslo


Tue 8-Aug-2017
^^^^^^^^^^^^^^

Edited photos from Sommarøy to Mefjordvær day of tour and them uploaded to Flickr album.

Restarted ERDDAP.
Reviewed whiteboard.
Pulled make_live_ocean_files worker and related tools repo module w/ Elise's nutrient BCs additions into production, fixed minor bugs and tested it with a manual run for 7aug; did some refactoring and automation test for 8aug revealed a bug in my refactoring; fixed.
(SalishSea)

Photo-walk to Chirstiania trov square.

Dinner w/ Pål, Eli, ???, and Susan at Palestinian restaurant.


Wed 9-Aug-2017
^^^^^^^^^^^^^^

Fixed namelist.surface copy/paste errors that Michael found in AGRIF subgrid files.
Launched 7x15+1 w/ buffer=0.25 SalishSeaAGRIF test on west.cloud; completed 360 time steps before it failed; xios memory was ~13Gb just before failure.
Launched 7x15+1 w/ buffer=0.125 SalishSeaAGRIF test on west.cloud; finished in 4h20m.
Improved make_live_ocean_files logging, checklist, and unit tests.
Added LiveOcean nutrients boundary conditions files to upload_forcing and make_forcing_links workers.
Tested and buffed make_turbidity_file worker.
(SalishSea)

Answered email from Marc Delêtre at National Botanic Gardens of Ireland re: accessing and using salishsea_tools package for Ariane analysis.
(prediction-core)

Went to the Edvard Munch museum on a very rainy afternoon.


Thu 10-Aug-2017
^^^^^^^^^^^^^^^

Puzzled w/ Susan about how deflation of production runs is happening: it's via xios-2 and the compression_level=4 attribute in the file_def.xml file_group elements. Note that xios-2 compression is not available in one_file mode when using multiple xios servers; see http://forge.ipsl.jussieu.fr/ioserver/raw-attachment/wiki/WikiStart/XIOS-practical_english.pdf, which also says:
  « memory » : memory optimization : buffers are able to treat one field at once.
  « performance » : performance optimization (reduce elapsed time of the run) : buffers are able to treat all of fields at a writing timestep.
SalishSeaAGRIF results from west.cloud differ from Michael's reference results.
Added make_turbidity_file worker to automation.
Added Fraser River turbidity file to upload_forcing worker.
(SalishSea)

Went exploring Oslo Fjord island via public transit ferries; walked on Bliekøya.


Fri 11-Aug-2017
^^^^^^^^^^^^^^^

Long conversation w/ Anne Claire Fouilloux, research software engineer in Pål's dept at Oslo U.

Discussed west.cloud vs. Michael's SalishSeaAGRIF results comparison w/ Susan; need to find difference.
Fixed bug in make_turbidity_file worker that I introduced when I refactored the code that converts from str date/time to panadas datetime; pandas seems to insist on ugly str concatenation.
Traced SalishSeaAGRIF discrepancy to having left the west boundary SSH disabled from an earlier test.
Realized that SalishSeaAGRIF file consolidation was because I ran with 1 xios server, not 2.
Prepared a new SalishSeaAGRIF run on west.cloud but it will have to wait until tomorrow due to 06 weather issue delaying forecast2 runs.
download_weather 06 failed due to slow uploads by EC; re-ran manually about 3h late to restart automation.
(SalishSea)

Dinner at Ian's apt.


Sat 12-Aug-2017
^^^^^^^^^^^^^^^

Traveled from Oslo to Bergen on a flight full of American cruise tourists.

Frommer's walking tour of Bergen neighbourhoods south of Brygge.

Launched 7x15+1 w/ buffer=0.125 SalishSeaAGRIF test on west.cloud w/ west sea surface height boundary condition activated, and LZ compression by xios-2 enabled; finished successfully in 4h10m
Added Fraser River turbidity file handling to make_forcing_links worker.
(SalishSea)

Sent PDFs of CMOS abstract and conference fee receipt emails to Kirsch in EOAS office.

Sunset photography around Brygge.


Sun 13-Aug-2017
^^^^^^^^^^^^^^^

Reviewed results of west.cloud SalishSeaAGRIF run against Michael's reference run results; still significantly different in sea surface height; tracked that to me using obs/ file and Michael using hindcast/ one (latter is improved).
Launched 7x15+1 w/ buffer=0.125 SalishSeaAGRIF test on west.cloud w/ hindcast/ssh_ file; crashed w/ ~500 time steps to go, probably due to collision w/ forecast2 run.
(SalishSea)

Hiked on Fløyen to the summit of Blåmanen.


Week 33
-------

Mon 14-Aug-2017
---------------

Launched 7x15+1 w/ buffer=0.125 SalishSeaAGRIF test on west.cloud w/ hindcast/ssh_ file; finished successfully in 4h15m
Confirmed that Fraser River turbidity file symlinks are being created on west.cloud.
Started populating new rivers repo w/ runoff fields climatology files from bloated NEMO-forcing repo.
Retried 1d nowcast mpirun on 1 full node on cedar that aborted after 53min on 27Jul; failed w/ high zonal velocity again.
Started work on transforming run_NEMO worker to use new grid, rivers, tracers, and tides repos instead of bloated NEMO-forcing repo.
Discussed plan to move production to v201702 w/ Susan; agreed on a new v201702 tree in SS-run-sets repo.
Susan reviewed and accepted comparison of west.cloud SalishSeaAGRIF with Michael's ref run; differences appear to be due to 1 day different river file (hindcast vs. nowcast), and corrected boundary widths.
Started populating new grid repo w/ coordinates, bathymetry, mesh mask, weights, etc. files from bloated NEMO-forcing repo.
Susan suggested changing cedar nowcast test run to 20Mar17 to reduce tidal currents because the 24Jul17 run blows up in Hood Canal; started prep.
make_turbidity_file failed due to insufficient data, though there was <4h gap.
(SalishSea)


Tue 15-Aug-2017
---------------

Ran 1d nowcast mpirun for 20mar17 on 1 full node on cedar; 1h7m
Manually ran upload_forcing turbidity --run-date 2017-08-14 --debug to persist turbidity forcing file; manually ran make_forcing_links nowcast-green --run-date 2017-08-14 to restart automation.
Continued populating new grid repo w/ coordinates, bathymetry, mesh mask, weights, etc. files from bloated NEMO-forcing repo.
Manually ran make_ww3_wind_file and make_ww3_current_file forecast --run-date 2017-08-14 to launch wave forecast.
Updated SalishSea/nemo3.6/nowcast/nowcast-dev and nowcast namelist.lateral to use tides and tracers repos, and runs/ssh/ directory.
Finished populating new rivers repo w/ runoff fields climatology files from bloated NEMO-forcing repo.
Updated SalishSea/nemo3.6/nowcast/nowcast-green namelist_pisces_cfg and namelist_smelt_cfg to use rivers repo directories and file names.
(SalishSea)

Bought ticket for PyCascades.


Wed 16-Aug-2017
---------------


(SalishSea)


Thu 17-Aug-2017
---------------

nowcast-dev/16aug17 failed due to missing 15aug17 restart file; investigation showed that 15aug17 failed due to not being able to find ssh file, not sure why; re-ran 15aug17.
1d nowcast mpirun for 20mar17 on 2 full nodes on cedar; completed in 1h21m w/ excellent xios performance stats, but it was 14m slower?? repeat of the run took 1h37m w/ gather, but not all files disappeared from tmp run dir before its removal attempt; cedar file system performance is very slow.
(SalishSea)


Fri 18-Aug-2017
---------------

Catch-up of nowcast-dev:
  * make_forcing_links --run-date 2017-08-16
  * make_forcing_links --run-date 2017-08-17

  * make_forcing_links --run-date 2017-08-18
Ordered 8Tb drive from Amazon for off-line results backup; delivery on 25aug.
Changed run_NEMO and config to use new grid repo and finished elimination of NEMO-forcing repo from SalishSeaNowcast.
get_NeahBay_ssh failed due to grid path issue; updated nowcast.yaml
make_live_ocean_files failed because low_passed_UBC.nc that we downloaded was yesterday's.
(SalishSea)

See project journal
(Resilient-C)


Sat 19-Aug-2017
---------------

Catch-up of nowcast-dev:
  * make_forcing_links --run-date 2017-08-18
Restarted ERDDAP.
(SalishSea)

See project journal
(Resilient-C)

Julie and Nicoli arrived.


Sun 20-Aug-2017
---------------

See project journal
(Resilient-C)

Updated docs re: grid, rivers, tides & tracers repos replacing NEMO-forcing.
(SalishSea)


Week 34
-------

Mon 21-Aug-2017
^^^^^^^^^^^^^^^

Observed partial (85%) solar eclipse at UBC alumni centre.

Installed PyCharm 2017.2.1 in /opt/ on niko.

Updated docs and arch files to use XIOS-2.
Updated SalishSeaCmd to not record forcing path VCS revision and status, and use grid, rivers, tides and tracers repos in example YAML file instead of NEMO-forcing and forcing path.
Started adding AGRIF sub-grid files to grid repo, then discovered that they aren't deflated.
(SalishSea)

Phys Ocgy seminar by Pedro Odon about Vancouver fall & winter 2016/17 - how miserable was it?


Tue 22-Aug-2017
^^^^^^^^^^^^^^^

Changed coordinates in SalishSeaNowcast config to by run-type specific, and moved top level coordinates config item into ssh section 'cuz that's where it is used.
Salish Sea team mtg; see whiteboard.
make_turbidity_file failed because buoy data has been repeating since 03:10; manually ran upload_forcing turbidity to restart automation.
Worked on ONC ferry data; struggled w/ API bug that re: conductivity from TWDP TSG device, but eventually got close to a useful dataset; still an issue with the crossing number variable not being associated with the time coordinate.
Changed nowcast-dev to use 201702 bathymetry and hindcast run parameters w/ restart from hindcast/21aug17; run completed, Susan will verify results.
(SalishSea)


Wed 23-Aug-2017
^^^^^^^^^^^^^^^

See project journal.
(Arctic Corridors)

make_turbidity_file failed because buoy data has been repeating since 03:10; manually ran upload_forcing turbidity to restart automation.
(SalishSea)


Thu 24-Aug-2017
^^^^^^^^^^^^^^^

Restarted ERDDAP server.
Update comment on https://bitbucket.org/salishsea/nemo-3.6-code/commits/223d8e2f re: successful nowcast-dev/23aug17 run.
Continued working on ONC ferry data; solved the crossing number variable issue by making it an xarray.DataArray; produced an ERDDAP dataset of 25jun17 TSG observations.
make_turbidity_file failed because buoy data has been repeating since 03:10; manually ran upload_forcing turbidity to restart automation.
Discussed ADCP data w/ Lan, but her questions were about 2012 data which is before we started processing it.
(SalishSea)


Fri 25-Aug-2017
^^^^^^^^^^^^^^^
Changed nowcast-green to use 201702 bathymetry and hindcast run parameters w/ restart from hindcast/24aug17; run completed, Susan will verify results.
Helped Tereza sort out massive permissions change on orcinus.
(SalishSea)

See project journal.
(Arctic Corridors)


Sat 26-Aug-2017
^^^^^^^^^^^^^^^

Cycled to Craig Bay for J 91st bday & J&M 59th anniversary.

Changed make_turbidity_file to not raise WorkerError because there is no need for it to stop the automation; also changed error condition print()s to logger.error()s.
Changed run_NEMO to get run type to restart from from config file.
Changed nowcast-dev to restart from nowcast-green.
(SalishSea)


Sun 27-Aug-2017
^^^^^^^^^^^^^^^

Changed nowcast-blue/forecast/forecast2 to use 201702 bathymetry and nowcast-dev run parameters w/ restart from nowcast-green/26aug17.
(SalishSea)

Cycled home.


Week 35
-------

Mon 28-Aug-2017
^^^^^^^^^^^^^^^

Clean build of SalishSea config on west.cloud at changeset 223d8e2f8cb6.
Fixed make_turbidity_file error handling so that it doesn't stop automation.
Investigated make_plots errors arising since change to 201702.
Continued working on ONC ferry data; added fluorometer and CO2 sensor devices, oxygen sensor device requests fail.
(SalishSea)

Phys Ocgy seminar by Wilken-Jon von Appen re: hgObservations of Atlantic Water subduction below Polar Water at a submesoscale front in Fram Strait


Tue 29-Aug-2017
^^^^^^^^^^^^^^^

See project journal.
(Arctic Corridors)

See project journal
(Resilient-C)

Worked w/ Susan to try to debug nowcast-green/25aug17 ssh nan failure.
(SalishSea)


Wed 30-Aug-2017
^^^^^^^^^^^^^^^

Re-ran nowcast-green/25aug17 w/ LiveOcean symlinks hacked to use 24aug17 throughout.
(SalishSea)


SalishSeaAGRIF production:
* add AGRIF option to run_NEMO worker:
  * sub-grid runoff namelists use sub-grid climatologies

Move production to 201702:
* Move LiveOcean BC files from modified/ to boundary_conditions/
* Rename LiveOcean BC files from single_LO*.nc and single_bio_LO*.nc to LO_TS_*.nc and LO_bio*.nc
* Rename riverTurbDaily2_*.nc to (at least) exclude the 2
* Update dir tree in docs/results_server/index.rst


* tune XIOS-2 buffer size on west.cloud

* Process some images
* Test attrs-17.1
* Take knives for sharpening


ToDo
====

* refactor, unit tests & docs for forcing links checking for NEMO-3.6

* reduce resolution of landing page images for faster load times
* add docs re: Resilient-C server-side app framework
* add EduCloud deployment docs

* research_ferries module
* JSON logging use example notebook

* review remaining nosy PRs
