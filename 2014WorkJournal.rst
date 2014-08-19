*****************
2014 Work Journal
*****************

This is my public work journal.
It is patterned after one that I have kept for several years for my work at Nordion_.
This journal is about my work as a Research Software Engineer with `Dr. Susan Allen`_ in the `Department of Earth, Ocean and Atmospheric Sciences`_ at the `University of British Columbia`_ during our sabbatical which started on 1 July 2013.
It is also about my `open-source activities`_.


January
=======

Week 1
------

Wed 1-Jan-2014
~~~~~~~~~~~~~~

Changed web remote app to by run via Pyramid pserve utility but stumbled on entry point issue when I deployed it to the RaspPi.
(raspi_x10)


Thu 2-Jan-2014
~~~~~~~~~~~~~~

Dentist appt.
Created 2014 work journal file.

Updated copyright notice year range in tools repo.
Started work on changing :command:`salishsea get_cgrf` to transform CGRF files from 0600Z to day+1 0700Z to 0000Z to 2300Z.
(MEOPAR)

Worked with Charles on tick re: connection failure from hg notify hook on bjossa.
(SOG)


Fri 3-Jan-2014
~~~~~~~~~~~~~~

Hiking at Buntzen Lake with Susan and James.


Sat 4-Jan-2014
~~~~~~~~~~~~~~

Fixed bug in and improved usability of nc_tools module.
Continued work on changing :command:`salishsea get_cgrf` to transform CGRF files from 0600Z to day+1 0700Z to 0000Z to 2300Z and verifying that the CGRF dataset has some resemblance to EC observations at YVR and Sandheads.
(MEOPAR)


Sun 5-Jan-2014
~~~~~~~~~~~~~~

Continued work on changing :command:`salishsea get_cgrf` to transform CGRF files from 0600Z to day+1 0700Z to 0000Z to 2300Z and verifying that the CGRF dataset has some resemblance to EC observations at YVR and Sandheads.
(MEOPAR)


Week 2
------

Mon 6-Jan-2014
~~~~~~~~~~~~~~

Created Storm-Surge repo on Bitbucket for work on 1st paper.
Salish Sea project mtg; see Google Drive whiteboard image file.
Set up and queued a new attempt at the 40d tidal harmonics analysis run on jasper.
The run uses:

* the new bathymetry with smoothing at the Strait of Juan de Fuca boundary
* preliminary (not Masson model) T&S boundary conditions
* baroclinic zero-gradient boundary conditions
* no atmospheric forcing
* enhanced vertical diffusion turbulent viscosity of 100 m^2/s
* lateral turbulent viscosity of 60 m^2/s

Started work on implementing CGRF file rebasing into :command:`salishsea get_cgrf`.
(MEOPAR)

Sorted out buildbot docs issue; path in :file:`master.cfg` was incorrect.
snapper appears to have lost the ability to do mercurial notification hooks via localhost.
Worked on updating buildbot configuration:

* changed default arg values in :py:func:`extensions.config_builder` to reflect present workflow
* started to change builds to flatter directory structure but the 4 repo clones get jumbled
(SOG)


Tue 7-Jan-2014
~~~~~~~~~~~~~~

40d jasper run completed successfully; downloaded results files to /ocean.
Helped Nancy get up and running on jasper.
Finished quick-start docs re running on jasper.
Consolidated :file:`namelist.compute.*` run-set files.
Changed CGRF rebasing notebook to show u & v wind components instead of wind direction due to uncertainty about the CGRF wind compass.
Continued implementation of CGRF file rebasing into :command:`salishsea get_cgrf`; got working code, needs tests and cleanup.
(MEOPAR)

Research meeting w/ Susan.
Agreed to focus on MEOPAR until we go to Berkely, then shift to SOG.

Replied to Pierre Clement @BIO re: his query to Susan about code to download EC historical weather observations.
(SOG)


Wed 8-Jan-2014
~~~~~~~~~~~~~~

Finished implementation of CGRF file rebasing into :command:`salishsea get_cgrf`.
Updated verification of CGRF vs. Sandheads and YVR observations and added 10 comparison which looks acceptable enough to proceed with.
Created and populated :file:`CGRF/NEMO-atmos/` directory on jasper for NAncy to test; had to copy files from salish because NCO is not available on jasper, but put in a request for it to be installed.
Changed salish :file:`CGRF/NEMO-atmos` to rebased files.
Created private-docs repo.
Added README to Storm-Surge repo.
(MEOPAR)

Participated in Phys Ocgy seminar about Salish Sea MEOPAR project that Kate lead.


Thu 9-Jan-2014
~~~~~~~~~~~~~~

Continued work on updating buildbot configuration.
Got repo cloning sorted out so that the 4 necessary clones are present in the necessary directories.
Got paths sorted out so that all builds are green again.
(SOG)

Ran tutorial for Susan, Kate & Nancy re: migrating Python functions from notebooks into SalishSeaTools package for sharing, re-usability, and automated docs generation.
Set up a jasper run to restart from the end of the 40d run for another 30d; horizontal turbulent viscosity is reduced from 60 to 50 m^2/s thanks to the full development of the dense water flow in from the JdF.
Did atmospheric forcing time interpolation verification.
Started work on getting output of actual level depths at each grid point.
(MEOPAR)


Fri 10-Jan-2014
~~~~~~~~~~~~~~~

Continued work on getting output of actual level depths at each grid point.
(MEOPAR)


Sat 11-Jan-2014
~~~~~~~~~~~~~~~

Restarted hourly rdiff-backup backups from tom to matisse after moving backup directory on matisse aside as a snapshot.


Sun 12-Jan-2014
~~~~~~~~~~~~~~~

Restarted RandoPony app after randonneurs.bc.ca site down time.
Found and reported SSL config issue whereby the default Webfaction cert was being used rather than our domain cert.
Rider sign-up test failed due to a connection error from the membership status database query.
(RandoPony)


Week 3
------

Mon 13-Jan-2014
~~~~~~~~~~~~~~~

Salish Sea project mtg; see Google Drive whiteboard image file.
Queued jasper job to extend tidal harmonics analysis run from day 71 to day 100 with bottom friction value reduced from 5e-3 to 3e-3.
Continued work on getting output of actual level depths at each grid point.
(MEOPAR)

Spent most of the afternoon at Nordion working on re-configuring apps to use the new SMTP relay server that is not identified in the domain MX record.
Figured out why BL1A schedule 125 failed to load into Sr-82 app; there were no currents scheduled.
(Nordion)


Tue 14-Jan-2014
~~~~~~~~~~~~~~~

d71d100_bfri3e-3 run on jasper failed after 626 time steps with -ve sea surface salinity at 149, 13 (down near the bottom of Puget Sound).
Queued another jasper run with bottom friction set to 4e-3.
Finished getting output of actual level depths at each grid point and created notebook to document the process and produce :file:`NEMO-forcing/grid/grid_bathy.nc`.
Started working on cleanup of code in stpctl.F90:stp_ctl() to check for NaN in u-velocity and salinity fields and abort cleanly with messages indicating where in the grid the NaNs occurred.
Got sidetracked into profiling u-velocity and salinity limit checking code because source has vectorized versions of the checks commented out in favour of triply-nested loop versions that are indicated to be faster on NEC SX5; the vectorized code is faster on salish, so changed to that.
(MEOPAR)

Attended SCIAM seminary by Lars Ruthotto (postdoc with Eldad Haber) on scientific programming languages: matlab, python, julia.


Wed 15-Jan-2014
~~~~~~~~~~~~~~~

Participated in ONC/UBC/MEOPAR SoG workshop.
d71d100_bfri4e-3 run on jasper failed identically to bfri3e-3 run after 626 time steps with -ve sea surface salinity at 149, 13 (down near the bottom of Puget Sound).
Queued another jasper run with bottom friction set to 5e-3 (the same as we have run since day 0, to prove that failure of lower bottom friction runs).
(MEOPAR)


Thu 16-Jan-2014
~~~~~~~~~~~~~~~

Participated in ONC/UBC/MEOPAR SoG workshop.
d71d100_bfri5e-3 run on jasper failed with -ve sea surface salinity at 149, 13 (down near the bottom of Puget Sound).
Queued a 41-70d jasper run with horizontal turbulent eddy viscosity nu=200 to see if making things dramatically stickier has a significant affect on tidal harmonic amplitudes.
Started exploratory work on automation of updating NEMO-code repo from Frensh SVN repo; got python-svn package installed on salish and confirmed that I can access the local working copy and remote repos with it.
(MEOPAR)


Fri 17-Jan-2014
~~~~~~~~~~~~~~~

Dentist appt for right molar fillings and bit adjustment.

41-70d jasper run with nu=200 timed out after 16h of run time.
Coincidentally jasper's status was changed to orange due to scheduler issues.
Finished (for now) cleanup of code in stpctl.F90:stp_ctl() to check for NaN in u-velocity and salinity fields and abort cleanly with messages indicating where in the grid the NaNs occurred.
It does the checks for NaNs, high u-velocity, and -ve surface salinity efficiently with vectorized code.
However, the output of NaN locations goes to stdout instead of ocean.output and the message that appears in ocean.output is uniformative.
Furthermore, output.abort files are only produced from the MPI-subdomain processors in which NaNs occur.
(MEOPAR)


Sat 18-Jan-2014
~~~~~~~~~~~~~~~

Travel day to Berkeley.

Discussed next steps for bloomcast and design of new SOG-forcing automated data collection app with Susan.
Reviewed worklog notes re: bloomcast development since July.
(bloomcast)


Sun 19-Jan-2014
~~~~~~~~~~~~~~~

First day back in Zack's lab at UCB.

Started a 10d run on jasper with nu=50 to try to confirm if slowness of nu=200 runs is due to nu=200 or jasper having lost its processor affinity config setting again.
10d run with nu=50 completed with an average compute time of 39.4s/model-hr which is very close to typical values.
Started another 10d run on jasper with nu=200 and it appears to be a ready-to-run but on-hold state.
(MEOPAR)

Confirmed that bjossa ports 8010 and 9000 are blocking connections from the Internet and opened a ticket requesting that they be opened.
Charles resolved the issue within an hour :-)
(SOG)

Fixed failing unit tests re: making HTML results directory a config file value.
Updated development environment packages and :file:`requirements.txt`.
Discussed with Susan the idea of a separate, open-source app, provisionally named :program:`ecget` to get EC weather and river data from web services and write the data to files in the format expected by SOG.
Also discussed designing the app to be extensible so that it could be readily used by other groups who need EC data.
Read the Python stevedore package docs and thought about design.
(bloomcast)


Week 4
------

Mon 20-Jan-2014
~~~~~~~~~~~~~~~

Salish Sea project mtg; see Google Drive whiteboard image file.
10d run on jasper with nu=200 remained queued but ready to run due to jasper scheduler shutdown.
Created a diagram of the NEMO code repos from the SVN repo in France, through our mirror and merge repos, to our Bitbucket and user repos, and diagrammed the workflow to update from France and merge with project revisions.
Tested and refined the workflow by updating to svn r3822; wrote docs about the workflow.
Ran 1h tests on salish starting on day 41 with nu=50 and nu=200; the latter takes 357s vs. 238s for the former, but Susan was doing development runs at the same time.
10d run on jasper with nu=200 finally ran and did so in 39.3s/model-hr; i.e. typical.
Coincidentally jasper's status returned to green with a message that the scheduler issue had been resolved.
(MEOPAR)

Created ECget project on tom, Bitbucket, and readthedocs.
(ECget)


Tue 21-Jan-2014
~~~~~~~~~~~~~~~

Started another 41-70d nu=200 run on jasper.
(MEOPAR)

Started development of ECget based on cliff and stevedore and it works out nicely. Implemented a daily average river flow command plug-in that uses driver plug-ins to get data from the EC wateroffice real-time site and to format the output for a SOG-forcing river file.
(ECget)


Wed 22-Jan-2014
~~~~~~~~~~~~~~~

41-70d nu=200 run on jasper timed out at 88654 time steps after 16h of run time.
Started a 51-60d nu=200 run.
Downloaded 41d50d (nu=50) and 41d50d_nu200 results to ocean and wrote a Python script to automate jasper to ocean transfers.
Closed loop in email thread w/ JP re: rebasing of CGRF dataset.
Changed :command:`salishsea get_cgrf` to use level 4 compression like the default in the python-netCDF4 library.
51-60d nu=200 run on jasper completed in about 110% of the time of 41-50d nu=200; transferred results to ocean.
61-70d nu=200 run on jasper completed in about the same time as the 51-60d run; transferred results to ocean.
(MEOPAR)

Cleaned up some details in ECget river flow sub-command; better logging, interpolation of values for missing days, unit tests.
Set up test environment based on pytest, coverage, and tox, and added dev docs about them.
Wrote a bunch of unit tests; got coverage over 80%.
(ECget)


Thu 23-Jan-2014
~~~~~~~~~~~~~~~

Wrote more unit tests for the river module.
Started exploring the new MSC Datamart AMPQ service for real-time weather data; demo app is http://sourceforge.net/p/metpx/code/HEAD/tree/trunk/sarracenia/.
Got the dd_subscribe script from the sarracenia package running; it is based on the Python 2.7 pika library.
Replicated the core functionality of dd_subscribe in Python 3.3 using the kombu library, but it only works for the alphanumeric bulletins feed that is used as the basic example for dd_subscribe; fails for swob-ml feeds.
(ECget)


Fri 24-Jan-2014
~~~~~~~~~~~~~~~

Implemented a new prototype client experiment based on kombu.mixins.Consumer and eventually got it producing the same CYVR feed as the pika-based client.
I think the tricky bit is ensuring that the name and the routing key of the queue are the same on client and the server.
The pika-based client seems to ignore a routing key different to the one on the server while the kombu-based client tries to use it and then gets no messages because of the mismatch.
Explored the XML schema of the datamart files and found that the ElementTree.find*() method don't work, perhaps due to namespacing (?), use iter() instead.
(ECget)

Helped Kate with advice on how to get the time intervals over which tidal harmonics are calculated in various runs in an automated way.
(MEOPAR)


Sat 25-Jan-2014
~~~~~~~~~~~~~~~

Updated SublimeLinter extension to new v3 release and installed flake8 and corresponding linter plug-in.

Realized that the dev instance failure that I saw on 15-Jan was due to not having a dev SMTP service running (nor celery workers, or that matter).
Decided that the deployment on Webfaction should be okay and did setup for Chili 200, but it failed to create the event spreadsheet on Google Drive with an authenitcation error.
Was unable to log into pony google account due to new location detection security; need to acknowledge access via text to my Wind mobile account.
(RandoPony)


Sun 26-Jan-2014
~~~~~~~~~~~~~~~

Modified kombu-based client to shut itself down after a specified lifetime with the idea being that the client will be run periodically by a cron job instead of running all the time as a daemon.
Implemented wind command plug-in based on kombu client experiment.
Crappy network at BCC enabled tests to confirm that the plug-in handles dropped connections smoothly, anthough the lifetime clock gets reset on re-connection so the client tends toward running forever.
Wrote unit tests for wind plug-in and the kombu consumer class that it is based on.
(ECget)


Week 5
------

Mon 27-Jan-2014
~~~~~~~~~~~~~~~

Used stable network connection in Zack's lab to confirm that wind plug-in terminates itself cleanly after its default lifetime of 900s has expired.
However, starting the client after a period of not running does not result in the receipt of the messages that should have been queued during that period.
Started work on driver plug-in to process Datamart URLs.
Read http://blogs.digitar.com/jjww/2009/01/rabbits-and-warrens/ and clarified some of my knowledge of AMQP.
Added auto_delete=False flag to queue declaration to try to get it to persist between consumer runs, but that didn't seem to work.
(ECget)

Salish Sea project mtg; see Google Drive whiteboard image file.
Investigated source of differences between the 41d70 and *_nu200 runs that are indicated by Kate's finding of tidal phase differences, and the 1d offset that Nancy noted.
Noticed that nn_date0 was truncated to 200209 (instead of 20020915) in the 41d70d namelist; Susan thinks that might affect tide calculations even though the actual start date should be coming from the restart file.
Queued up a new 41d70d run on jasper.
Created /ocean/dlatorne/MEOPAR/SalishSea/results/spin-up/ and .../repo-tests/ directories.
Moved results of Susan's 1st 7 days of spin-up runs into the former.
Plan to use the latter for results of 1d runs to be done after merges from NEMO SVN repo.
Cloned NEMO-code repo to NEMO-code-spin-up on jasper so that spin-up runs can proceed with a version of the code that is independent of other work.
Worked on setting up 23sep2oct 10d spin-up run.
Learned a lot about output for grid zooms in iodef.xml, none of which made me happy - each zoom has to go to a separate file.
(MEOPAR)


Tue 28-Jan-2014
~~~~~~~~~~~~~~~

Checked results of 41d70d re-run and found that it crashed on day 65 because enhanced vertical turbulent diffusion was left at 10 instead of 100.
Queued another re-run.
Finished set-up for 23sep2oct 10d spin-up run and queued it.
Got update from Westgrid support on NCO and netCDF4 on jasper; maybe ready next week.
Started writing docs about spin-up runs.
Investigated what role the nn_date0 value in the namelist plays.
It is mentioned in connection with date correction of tides in ocean.output, but it is not yet clear whether that correction takes into account the elapsed time from the restart file.
What is for certain is that the 41d70d in which it was truncated to 200209 is different to the 10 day runs spanning that period, and the correction date in the ocean output file from 41d70d is 9-Feb-20!!!
Eventually sorted out that nn_date0 *is* used to adjust the tides to match the run date, so it is important that it be set to the date when nn_it000 = 1.
(MEOPAR)


Wed 29-Jan-2014
~~~~~~~~~~~~~~~

23sep2oct 10d spin-up run failed overnight by exceeding its requested memory limit; re-queued it with 3Gb/processor.
3Gb/processor attempt at 23sep2oct 10d spin-up run also failed; re-queued it with 4Gb/processor and started worrying about a memory leak in NEMO.
41d70d tide analysis run succeeded; transferred the results to ocean.
Updated comments in all SS-run-sets namelist.time files to correctly say what value nn_date0 should be set to, and what it is used for.
Added note to NEMO quirks docs about nn_date0 value.
4Gb/processor attempt at 23sep2oct 10d spin-up run also failed.
Re-queued 23sep2oct 10d spin-up run with 2Gb/processor and external barotropic boundary condition forcing disabled to try to isolate the possibility of a memory leak in NEMO.
No-barotropic BCs 23sep2oct 10d spin-up run also failed on memory; requeued it with barotropic BCs restored and atmospheric forcing disabled.
23sep2oct 10d spin-up run without atmospheric forcing also failed on memory.
(MEOPAR)

Sent email to Datamart AMQP trial support email list re: expected queue lifetime but it is being held for moderation.
Experimented with Sand Heads wind queue in IPython and found that it persists and accumulates messages.
Continued work on driver plug-in to process Datamart URLs.
Added hook to Datamart consumer to explicitly close the connection when the consumer times out.
After a false start with the connection repeatedly connection and dropping, got the same behaviour from my ECget plug-in by changing to passive=True in the queue_declare() call.
(ECget)


Thu 30-Jan-2014
~~~~~~~~~~~~~~~

Confirmed that Sand Heads queue peristed overnight on CMC server in the absence of connections from my clients.
Confirmed that driver plug-in for Datamart URLs can extract Sand Heads wind speed and direction values.
Removed method that explicitly closes the connection when the consumer times out.
Changed the consumer to intially declare the queue on the server with passive=True to connect to an existing queue, but with passive=False if a ChannelException (indicating that the queue does not exist on the server) is raised.
Noticed by checking from IPython that, though the consumer created a queue as expected, and that the queue persists after the consumer times out, the queue shows that it still have 1 consumer; that may be leading to a time-out and queu destruction on the server.
(ECget)

23sep2oct 10d spin-up run with :file:`jasper/iodef.3d.xml` also failed on memory.
23sep2oct 10d spin-up run with NEMO-code-spin-up updated to rev:67:8c4a24ba49df (used for 41d70d tides run that worked) and a clean rebuild also failed on memory.
Added function to run :command:`hg parents` command to hg_commands module.
Change :command:`salishsea prepare` command to record working directory rev of NEMO-code and NEMO-forcing repos via :command:`hg parents` instead of :command:`hg heads` which reports the last pulled rev.
Switched to trying to get a 2d version of 41d70d tides run to fail with a memory limit on jasper.
Ran successfully at rev:98:84b90cd75601.
Ran successfully with :file:`spin-up/iodef.1d.xml`.
Ran successfully with atmospheric forcing.
Ran successfully with Masson results baroclinic boundary forcing and Tofino sea surface height barotropic boundary forcing; lateral turbulent viscosity was increased to 80 to compensate for high salinity input from Masson results; memory use increased from ~15.2Gb to ~20.2Gb.
Queue run with start date set to 23-Sep-2002 and restart control set to 1 (in contrast to 15-Sep and 2); testing the idea that the calendar timeframe is the problem.
(MEOPAR)

Set up 2014 bloomcast SOG YAML infiles.
Started investigating the a work-around for the YVR station id change that happened in Jun-2013.
(bloomcast)


Fri 31-Jan-2014
~~~~~~~~~~~~~~~

Got response to email re: queue lifetime; CMC are running tests to provide an answer.
IPython confirmed that yesterday's queue that had a hanging consumer disappeared overnight.
Restored the method that explicitly closes the connection when the consumer times out and the queue behaves as required.
(ECget)

41d70d 2d run with start date set to 23-Sep-2002 and restart control set to 1 ran successfully.
Ran that config successfully with bottom friction set to 1e-4.
Ran that config successfully with start date set to 16-Sep-2002, restart control set to 0, and 22-Sep-2002 spin-up restart file from salish; restults/41d70d.2d.sr/.
u-velocity blew up in Haro Strait area after 2107 time steps on run with start date set to 23-Sep-2002, nn_it000 set to 1, restart control set to 0, and 22-Sep-2002 spin-up restart file from salish; restults/41d70d.2d.sr2/.
Queued a 2h run with start date set to 23-Sep-2002, nn_it000 set to 1, restart control set to 0, and 22-Sep-2002 spin-up restart file from salish.
(MEOPAR)

Hacked ClimateDataProcessor.process_data() method to insert zeros into the data record for YVR data prior to 2013-06-13 because the YVR station id changed on 2013-06-12 but bloomcast doesn't need the data prior to 2013-09-19 to be accurate and SOG just needs there to be some values from 2013-01-01 onward.
Added error condition to abort bloomcast if the runs start date is such that river flow data from more than 18 months in the past are required because EC only maintains river data for a rolling 18-month time window.
Installed gfortran on tom via homebrew and built SOG.
Got a complete bloomcast run on tom.
Deployed bloomcast to salish for 2014 forecasts.
Tagged repo with bloomcast2014.
(bloomcast)

Added 2016 through 2024 leap years to forcing.f90.
Tagged repo with bloomcast2014.
Started work on cleaning up fatal error exits; add ERROR prefix to messages, exit with return code 1, and flush stdout and stderr (in that order) before exiting.
(SOG)


Sat 1-Feb-2014
~~~~~~~~~~~~~~

Cron job failed with path and email address issues; fixed, and ran bloomcast manually via new cronjob script and not in virtualenv.
(bloomcast)

Sand Heads wind queue did not survive overnight; wondering if CMC queue sweepers are unpredictable in how long the let queues without consumers live.
(ECget)

2h run with start date set to 23-Sep-2002, nn_it000 set to 1, restart control set to 0, and 22-Sep-2002 spin-up restart file from salish failed with u-velocity blow-up after 2107 time steps, like previous run.
Started a 23sep2oct spin-up run using NEMO-code executable but killed it when we realized that the run above had failed due to high u-velocity; noted, however, that that its memory use was 67Gb after only 14m of run time.
Successfully ran 23sep2oct spin-up run using NEMO-code executable with nu=80 (to address high u-velocity thought to be due to tide date mismatch between run and restart file) and profiling disabled (because it is one of the few remaining differences that could account for the memory leak).
It appears that profiling may be the source of the memory leak.
Queued 71d100d tides run.
Changed :command:`salishsea prepare` and :command:`salishsea gather` so that YAML run description, iodef.xml, and xmlio_server.def files are now copied to run directory instead of being symlinked.
Queued 23sep2oct spin-up run using NEMO-code executable and a new, nu=55 22sep restart file from salish with correctly adjsuted tides; used nu=55 and no profiling.
Started work on Marlin app to manage SVN updates of NEMO-hg-mirror repo.
(MEOPAR)

Continued work on cleaning up fatal error exits; add ERROR prefix to messages, exit with return code 1, and flush stdout and stderr (in that order) before exiting.
(SOG)


Sun 2-Feb-2014
~~~~~~~~~~~~~~

71d100d tides run failed with -ve sea surface salinity at 264,347 (tip of South Pender Is) at time step 164432 (~0400UTC on 19Dec2002).
23sep2oct spin-up run with nu=55, no profiling, and well adjusted restart file from salish finished successfully.
Added CGRF files for 4Oct2002 through 13Oct2002 to collection on jasper.
Updated spin-up runs docs.
Queued 23sep24sep spin-up run with nu=55 because Susan thinks that the 10d run let too much JdF deep water into the SoG.
(MEOPAR)


February
========

Week 6
------

Mon 3-Feb-2014
~~~~~~~~~~~~~~

Salish Sea project mtg; see Google Drive whiteboard image file.
Finished implementation of Marlin.
Used Marlin to merge r3828:3843 from NEMO upstream repo; pushed the merge to NEMO-code for Nancy to test.
Susan took over running spin-up day by day to tune horizontal turbulent viscosity run by run; I continue to manage results in /ocean/dlatorne/MEOPAR/SalishSea/results/spin-up/.
(MEOPAR)


Tue 4-Feb-2014
~~~~~~~~~~~~~~

Started work on OSM poster.
(bloomcast)


Wed 5-Feb-2014
~~~~~~~~~~~~~~

Noticed that there are literally hundreds of hours when weather description is N/A and cloud fraction value has to be interpolated; it make the log almost unusable.
(bloomcast)

Thrashed around trying to figure out how to use OAuth2 to do RandoPony Google Drive spreadsheet operations from Webfaction deployment since the ClientLogin() call was getting an authentication failure.
Discovered that ClientLogin() works just fine from tom, only failing from Webfaction.
Eventually concluded that OAuth2 is not the correct paradigm because it is based on 3-legged auth and the pony is just a web app and data stored o Drive.
Succeeded in getting ClientLogin() to work by enabling 2-factor auth on pony account and setting up an application-specific password.
(Randopony)

Changed exchange name from :kbd:`cmc` to :kbd:`xpublic` as the email on dd-info said needed to happen at 08:00 today.
Finished implementation of message handling and output formatting for Sand Heads winds consumer.
(ECget)

Reviewed results of Nancy's 1st merge-test results and analysis notebook.
Merged r3846:3847 from NEMO upstream repo and pushed the merge for NEMO-code for Nancy to test.
(MEOPAR)


Thu 6-Feb-2014
~~~~~~~~~~~~~~

Worked on unit tests for Sand Heads wind consumer.
Created a quick command plug-in to investigate the :kbd:`tot_cld_amt` field in the SWOB-ML files.
Learned that :kbd:`tot_cld_amt` is reported every 3 hours (for the most part).
(ECget)

Investigated N/A weather descriptions at YVR; they appear to result from a present_weather code of 125: "Manned Observation: No present or recent weather".
Filtered logging so that interpolation counts are logged to the console and individual interpolation messages are logged to disk.
Learned that 2909 cloud fraction value are being interpolated due to the N/A weather description.
Added a note to the results page indicating that we believe the results to be inaccuracte due to the cloud fraction interpolation issue.
Tagged bloomcast2014r2 in the repo.
(bloomcast)

Merged r3852:3892 from NEMO upstream repo and pushed the merge for NEMO-code for Nancy to test.
Reviewed upstream changes from r3908 to r4391 for their impact on our codebase and drafted a merge-steps plan.
Merged r3908 (1st of the changes necessary for us to open our Johnstone Strait boundary) from NEMO upstream repo and pushed the merge for NEMO-code for Nancy to test.
(MEOPAR)


Fri 7-Feb-2014
~~~~~~~~~~~~~~

Added CSS class to highlight note that was added to results page yesterday; missed it in yesterday's commits.
Fixed the fact that unknow weather description log messsges are not being emailed to Susan by increasing the timeout on the logging SMTP handler.
Worked on understanding the relationship between :kbd:`cld_amt_code_*` values and :kbd:`tot_cld_amt` in SWOB-ML files.
Did several count stats analyses on the available YVR SWOB-ML files using a mapping from :kbd:`cld_amt_code_*` to CF and summing the mapped CF values to get effective :kbd:`tot_cld_amt` values:

* of 744 hourly YVR SWOB-ML files, 55 contain no :kbd:`*cld_amt*` values, 231 contain :kbd:`tot_cld_amt` values, and 65 of those have disagreement between the summation CF value and the reported :kbd:`tot_cld_amt` value

* After UTC midnight roll-over, of 721 hourly YVR SWOB-ML files, 55 contain no :kbd:`*cld_amt*` values, 224 contain :kbd:`tot_cld_amt` values, 59 of those have disagreement between the summation CF value and the reported :kbd:`tot_cld_amt` value, 14 of those have an absolute difference of >0.5, but none have an absolute difference of >1
(bloomcast)

Fixed and added unit tests.
Moved YVR CF check plug-ins to their own package and started documenting the ways in which ECget can be extended and reused.
(ECget)

Merged r3911:3919 from NEMO upstream repo and pushed the merge for NEMO-code for Nancy to test; upstream repo was very balky.
(MEOPAR)


Sat 8-Feb-2014
~~~~~~~~~~~~~~

Drained the Sand Heads wind queue which had not been connected to by a consumer since mid-afternoon on 6-Feb; queue had persisted on server and all expected messages were present.
Discussed next step of YVR cloud fraction analysis with Susan; calculate cummulative error.
(ECget)

Booked travel for PyCon and visit to parents in April.

Created a proof-of-concept for the salishsea.eos.ubc.ca site based on Sphinx, sphinx_bootstrap_theme, and the bootswatch Superhero theme.
(salishsea-site)

Added 4-Oct-2002 through 23-Oct-2002 CGRF files to collection on jasper.
(MEOPAR)


Sun 9-Feb-2014
~~~~~~~~~~~~~~

Added hourly value formmatter.
Separated SOG weather command plug-ins and Datamart AMQP consumer into different modules.
Changed river flow command and daily value formatter to use arrow instead of datetime.
(ECget)

Tried a run on jasper with 6x14-22 = 62 processors based on Susan’s by-eye analysis that found that 22 processors in the 6x14 domain decomposition have grid points that are exclusively on land.
The run failed during start-up with a segmentation fault before the IOM server completed parsing the iodef.xml file.
Speculation is that while NEMO may be capable of running with land processors excluded, the IOM server may not be.
(MEOPAR)

Added cloud fraction mappings for 3 previously unseen weather descriptions.
(bloomcast)


Week 7
------

Mon 10-Feb-2014
~~~~~~~~~~~~~~~

Updated spin-up runs collection on :kbd:`salish` with Susan's recent results from :kbd:`jasper`.
(MEOPAR)

Attended Jeff Dorman's EcoLunch seminar.

Added queue name management to ensure unique per-deployment queue names.
Downloaded the last 18 months of Fraser and Englishman River flow data in SOG-forcing/ECget and started work toward cron jobs that will do that monthly so we don't loose continuity in our dataset due to the wateroffice.ec.gc.ca rolling 18-month window on real-time data.
Bumped ECget version to 0.2 and development status to beta to coincide with 1st deployment on salish.
Started implementing YVR cloud fraction command plug-in.
Refactored SOG weather command plug-ins to use a command base class.
(ECget)

Got YVR station 889 weather data for 2013 < 12-Jun and 2012 for Susan by tweaking and faking out bloomcast.
(bloomcast)


Tue 11-Feb-2014
~~~~~~~~~~~~~~~

Copied 18oct25oct spin-up run results from jasper to ocean.
Added CGRF files for 2002-10-28 through 2002-11-06 to collection on jasper.
(MEOPAR)

Finished unit tests for YVR cloud fraction command plug-in.
Set up hourly cron job on salish to run YVR cloud fraction consumer and append results to SOG-forcing/ECget/YVR_cloud_fraction.
Implemented YVR air temperature and relative humidity command plug-ins and set them up in hourly cron jobs on salish.
Figured out how to plug into ECget from another package via entry-point namespaces - no changes to any ECget files required.
Added command plug-in to backfill YVR data values from past 30 days SWOB-ML files.
Replaced files that cron jobs are appending to with ones that contain past 30 days of data.
(ECget)

Repeated Friday's count stats analyses on the available YVR SWOB-ML files using a mapping from :kbd:`cld_amt_code_*` to CF and summing the mapped CF values to get effective :kbd:`tot_cld_amt` values:

* of 734 hourly YVR SWOB-ML files, 55 contain no :kbd:`*cld_amt*` values, 231 contain :kbd:`tot_cld_amt` values, and 60 of those have disagreement between the summation CF value and the reported :kbd:`tot_cld_amt` value, 54 of those have an absolute difference of >0.5, but none have an absolute difference of >1, and the cummulative difference is 0
(bloomcast)


Wed 12-Feb-2014
~~~~~~~~~~~~~~~

Travel to Vancouver; 2.5 hr flight delay, so lots of time at SFO.

Worked on docs re: API, built-in plug-ins, and extending ECget.
(ECget)


Thu 13-Feb-2014
~~~~~~~~~~~~~~~

Salish Sea project mtg; see Google Drive whiteboard image file.
(MEOPAR)

Continued work on OSM poster; much easier on a desktop workstation that is running Inkscape directly compared to using it via X11 forwarding on a MacBook.
(bloomcast)


Fri 14-Feb-2014
~~~~~~~~~~~~~~~

Sent email to Luc outlining the quantities and frequency we need from the GEM-2.5 products to use in NEMO.
Wrote talk abstract on collaboration tools for CMOS meeting in Rimouski.
(MEOPAR)

Continued work on OSM poster.
(bloomcast)


Sat 15-Feb-2014
~~~~~~~~~~~~~~~

Continued work on OSM poster.
(bloomcast)

Submitted CMOS talk abstract.
(MEOPAR)


Week 8
------

Mon 17-Feb-2014
~~~~~~~~~~~~~~~

Enabled debugging in YVR weather consumer cron job scripts to try to capture the source of the intermittent "unknown entity" messages.
(ECget)

Updated link to SOG buildbot page on buildbot.net success stories page.
(SOG)

Finished OSM poster layout and content template; need to update content with bloomcast results on Friday before printing.
Removed warning note re: YVR weather description and cloud fraction values from bloomcast results page.
Re-organized results page to put profiles below time series plots.
Added a line to the mixing layer depth plot to show the time at which the profiles are plotted.
(bloomcast)


Tue 18-Feb-2014
~~~~~~~~~~~~~~~

Travel to Vancouver Island for State of the Ocean meeting at PBS.

Buffed SoG-bloomcast repo for release on Bitbucket.
(bloomcast)

Investigated `xml.etree.ElementTree.ParseError: undefined entity: line 5, column 64` error that occurs sporadically.
It seems to be of no consequence as the value recorded when it arises is always in agreement with the Firefox rendering of the XML file.
Changed from parsing `response.content` to `response.text` to see if that will quiet things down.
(ECget)


Wed 19-Feb-2014
~~~~~~~~~~~~~~~

State of the Ocean meeting at PBS.

Added clearfix class to profile plots container so that the following container renders below.
Fixed size of title on x-axis of mixing layer depth graph.
(bloomcast)


Thu 20-Feb-2014
~~~~~~~~~~~~~~~

Travel to Vancouver.

Bloomcast cron job and manual re-try failed due to time-outs on wateroffice site.
Created SoG-bloomcast repo on Bitbucket and pushed project to it.
(bloomcast)

Worked on adding filter method to Datamart driver so that, for example, only hourly data and correction messages will be processed.
(ECget)


Fri 21-Feb-2014
~~~~~~~~~~~~~~~

Finalized OSM poster and got it printed.
(bloomcast)

Salish Sea project mtg; see Google Drive whiteboard image file.
(MEOPAR)

Finished adding filter method to Datamart driver so that, for example, only hourly data and correction messages will be processed.
Cleaned repeated hours out of YVR data files on salish.
Discovered that YVR data files on salish have not had data added since 08:00 on 19-Feb; not sure why.
Dug into tox failures under 2.7 and 3.2.
Fixed 2.7 issue by refactoring SWOB-ML get_data driver method.
Traced 3.2 issue to a bug in pbr which is used in cliff's packaging tool chain; nothing for me to do until there is a new release of cliff.
(ECget)


Sun 23-Feb-2014
~~~~~~~~~~~~~~~

Travel to Honolulu for OSM 2014.


Week 9
------

Mon 24-Feb-2014
~~~~~~~~~~~~~~~

Put posters up; sweet corner lot for mine, though the surrounding posters make it look like it is in an uncategorizable ghetto.
Tutorials on 5th IPCC report; see meeting notes file.
(OSM)

Merged r3941 from NEMO upstream repo and pushed the merge for NEMO-code for Nancy to test.
Updated merge workflow docs to clarify that a merge is alway required when changes are pulled from NEMO-hg-mirror repo.
(MEOPAR)

Created salishsea-site repo and pushed it to Bitbucket.
Started building site framework based on Sphinx, sphinx-bootstrap-theme, and Bootswatch superhero theme.
(salishsea-site)


Tue 25-Feb-2014
~~~~~~~~~~~~~~~

Arctic in rapid transition session.
Plenary session about Pacific coral reefs, river outflows, and working with local cultures and leaders.
Plenary panel about communicating science; started okay, but devolved into being very USA-centric.
Tutorials re: biology and marine ecosystem modeling; see meeting notes file:

* bacterial degradation of oil from Deep Sea Horizon on a Gulf of Mexico beach
* Georgina Gibson: how to build a PNZ model
* John Cullen: Charles Yentsch, ocean colour, and phytoplankton
* ocean viruses and bacteria

Poster session conversations with Jeff Dorman, Doug Wallace, and Mark Halverson.
(OSM)

Worked on site makefile and deployed site to shelob server for the first time.
Apparently shelob does not accept ssh connections from outside eos domain so had to do a 2-step deployment via rsync from tom to sable, then from sable to shelob.
(salishsea-site)

Nancy reported that r3941 tested clean on jasper.
(MEOPAR)


Wed 26-Feb-2014
~~~~~~~~~~~~~~~

Awards lectures.
Tutorials on bio-Argo, wavelet transforms, and turbulent diffusion/dispersion.
Poster session conversation with Rich, and a great presentation on turbulence by Stephanie.
(OSM)

Merged r3942:4510 from NEMO upstream repo and pushed the merge to NEMO-code for Nancy to test.
Created Nov 2006 CGRF files on salish for Nancy to use for initial storm surge hindcast test runs.
(MEOPAR)


Thu 27-Feb-2014
~~~~~~~~~~~~~~~

Plenary
Tutorials on US state department, superstorm Sandy and storm surge, and geo-engineering based on growing ocean algae in dessert regions.
Presented my poster and talked to at least 2 or 3 people I didn't already know.
(OSM)

Created Dec 2006 CGRF files on salish for Nancy to use for initial storm surge hindcast test runs.
(MEOPAR)

Added "Freezing Rain,Snow Showers" to cloud fraction mapping.
(bloomcast)


Fri 28-Feb-2014
~~~~~~~~~~~~~~~

River plumes session for talks by Mark, Julie, and Sarah Godding.
Tutorials on global water cycle, carbon in the southern ocean, arctic ice algae, and climate chsnge adaptation in the Gulf of Maine.
(OSM)

Investigated the inclusion of arbitrary passive traces in NEMO and concluded that it is done using TOP.
(GEOTRACES)


Sat 1-Mar-2014
~~~~~~~~~~~~~~

Discussed with Susan the idea of running an ensemble of bloomcast future weathers instead of the contrived average weather, and the early and late weathers from the hindcast.
Started to investigate creating a collection of annual, 2-year long forcing files to drive ensemble bloomcasts.
(bloomcast)


Sun 2-Mar-2014
~~~~~~~~~~~~~~

Talked with Susan about statistical processing of ensemble bloomcasts.
(bloomcast)

Travel to Vancouver.


March
=====

Week 10
-------

Mon 3-Mar-2014
~~~~~~~~~~~~~~

Recovery from delayed overnight flight home from Honolulu.

Replied to email from Alex at EC datamart re: ECget leaking over 250 active connections.
(ECget)

Started creating Mako template of RST file for results so that they can be incorporated into the salishsea-site build process.
(bloomcast)

Resolve <no title> issue in HTML title tag.
(salishsea-site)


Tue 4-Mar-2014
~~~~~~~~~~~~~~

Attended Jessica's master's defense.

Reviewed Nancy's initial storm surge run results.
(MEOPAR)

Set up meeting w/ Ben & Susan re: adding aragonite saturation to bloomcast.
Started work on extracting 2 year long chunks from SOG-forcing data files to support running bloomcast as an ensemble forecast.
(bloomcast)

Sent email to John re: ssh access to shelob from outside eos domain.
(salishsea-site)

Investigated what is going on with ECget queues; it seems that the queues I created around 10-Feb are no longer receiving messages, however, newly created queues receive messages as expected.
(ECget)


Wed 5-Mar-2014
~~~~~~~~~~~~~~

Prepared for code review of bdy_dyn3d_zgd() :file:`MY_SRC/bdydyn3d.F90`.
Salish Sea project mtg; see Google Drive whiteboard image file.
Committed and pushed the results of the :file:`MY_SRC/bdydyn3d.F90` code review.
Cleaned up file organization in NEMO-forcing/open_boundaries/.
(MEOPAR)

Finished implementation of tool to extracting 2 year long chunks from SOG-forcing data files to support running bloomcast as an ensemble forecast.
Used it to process air temperature, relative humidity, cloud fraction, and wind files.
Met with Susan and Ben to discuss adding a page to bloomcast to show pH, alkalinity, DIC, and aragonite saturation.
(bloomcast)

Checked the new YVR air temperature queue created yesterday from salish and found that it continues to receive messages.
(ECget)

Attended David Archer's public lecture on the role of CO2 and CH4 in climate change.


Thu 6-Mar-2014
~~~~~~~~~~~~~~

Realized that 2yr chunk tool will produce incomplete or empty files.
Figured out how to run matlab via the Python subprocess module; see ~/add.py on sable.
Continued working on 2-yr chunk forcing files; added fixes so that incomplete or empty files are not created; added logging; fixed code so that files contain 732 days of data, and updated the meteo and wind files that were shorter than that.
(bloomcast)

Wrote a lengthy email about the scientific Python stack to Francis at Waterloo.
Worked on OSM expense claim with Susan.

Attended David Archer's department seminar on modelling methane hydrates in ocean sediments over geological time scales.


Fri 7-Mar-2014
~~~~~~~~~~~~~~

Created a proof of concept SVG image for the landing page of salishsea.eos.ubc.ca.
It has embedded PNG images that link to pages for NEMO model, bloomcast, and SOG model.
The file needs to be placed in the _static/ directory so that Sphinx copies it to _build/html/ during the build process.
The links hrefs need to take that location into account.
The links also need to use target="_top" so that they open in the full browser window rather than the SVG object frame.
Text must be created in Inkscape as plain text (click and type) rather than flowed text (click-drag-type) because flowed text is incompatible with browser SVG engines.
The font-family of text objects has to be edited manually because Inkscape fonts are named differently to browser fonts and the result is a plain, serif font.
(salishsea-site)

Created 2 year long chunks from SOG-forcing river flow files.
Created SoG-bloomcast-ensemble development branch.
(bloomcast)


Week 11
-------

Mon 10-Mar-2014
~~~~~~~~~~~~~~~

Arrived in Delft.


Tue 11-Mar-2014
~~~~~~~~~~~~~~~

Set up build slaves on coho and nerka running the SOGcommand build as regression tests (nightly when changesets have been pushed, and always weekly); done as a monitoring mechanism to confirm that those machines are up and running a viable configuration.
(SOG)

Checked NEMO SVN repo for updates: none.
Experimented with adding Markdown descriptions from 1st cell of notebooks to nbviewer links lists in tools repo directory READMEs.
(MEOPAR)


Wed 12-Mar-2014
~~~~~~~~~~~~~~~

Finished work on new make_readme.py scripts in tools repo that add descriptions from notebook 1st cells to the list of nbviewer links.
Descriptions may be either in Markdown or raw text cells.
(MEOPAR)

Continued work on ensemble branch.
(bloomcast)

Moved into office at TU Delft.


Thu 13-Mar-2014
~~~~~~~~~~~~~~~

Improved logging re: cliff implementation of bloomcast command.
Started implementation of method to generate infile edit files for each member run of the ensemble.
(bloomcast)

Created results repo; first contents are tidal current predictions for Baynes Sounds that Susan prduced for Debbie.
Created Salish Sea MEOPAR project contributors file re: docs repo issue #1 and linked it into README files in all other repos where it was appropriate to do so.
Salish Sea project mtg; see Google Drive whiteboard image file.
(MEOPAR)


Fri 14-Mar-2014
~~~~~~~~~~~~~~~

Finished implementation of method to generate infile edit files for each member run of the ensemble.
(bloomcast)

Started exploring the Wind-Driven Reduced Gravity 1.5 Layer Rotating Shallow Water Model code that Francis sent.
Instrumented it to measure execution time.


Sun 16-Mar-2014
~~~~~~~~~~~~~~~

Added method to generate ensemble jobs batch description file.
(bloomcast)


Week 12
-------

Mon 17-Mar-2014
~~~~~~~~~~~~~~~

Chunning reported that the ferry data chlorophyl level is rising steadily which agrees with the bloomcast calculations both qualitatively and, apparently, quantitatively.
Added method to run ensemble forecast via new SOG command processor batch API.
(bloomcast)

Added an API for the :command:`SOG batch` command.
Bumped SOGcommand package version to 1.3.3.
Ran a 30 member forecast based on weather from 1980 through 2010 and analyzed the results in an IPython notebook; median bloom date agrees with present method (26-Mar based on actual weather to 15-Mar).
(SOG)


Tue 18-Mar-2014
~~~~~~~~~~~~~~~

Continued analysis of initial 30 member ensemble forecast.
Discussed selection of members to plot when year-day stats yield zero or multiple members.
Started implementation of calculation of ensemble forecast results methods and functions in ensemble.py and bloomcast.py modules.
Moved existing bloomcast unit tests into test modules that reflect code modules.
(bloomcast)


Wed 19-Mar-2014
~~~~~~~~~~~~~~~

Finished implementation of calculation of ensemble forecast results methods and functions.
Started implementation of new time series plotting functions in a new visualization.py module.
(bloomcast)


Thu 20-Mar-2014
~~~~~~~~~~~~~~~

Continued implementation of new time series plotting functions; finished nitrate/diatoms plot.
(bloomcast)

Started work on clean-up of netCDF_Plots directory in tools repo, and creation of example notebooks.
Salish Sea project mtg; see Google Drive whiteboard image file.
(MEOPAR)


Fri 21-Mar-2014
~~~~~~~~~~~~~~~

Continued implementation of new time series plotting functions; temperature/salinity plot.
(bloomcast)

Pushed example notebook re: working with netCDF files in Python.
Started development of salishsea_tools.viz_tools.py module.
Started work on example notebook re: plotting bathymetry data.
(MEOPAR)


Sat 22-Mar-2014
~~~~~~~~~~~~~~~

Added cloud fraction mappings for "Rain,Fog,Blowing Dust" weather description.
Continued implementation of new time series plotting functions.
(bloomcast)


Sun 23-Mar-2014
~~~~~~~~~~~~~~~

Continued implementation of new time series plotting functions.
(bloomcast)


Week 13
-------

Mon 24-Mar-2014
~~~~~~~~~~~~~~~

Did catch-up in this log.

Finished implementation of function to plot mixing layer depth and wind speed time series.
Changed forcing data transition date (config.data_date) to be an arrow object throughout the codebase.
(bloomcast)

Added CGRF files for 2002-11-07 through 2002-11-16 to collection on jasper.
Copied 26oct spin-up run results from Susan's workspace salish to ocean.
Copied 27oct30oct, 31oct, and 1nov4nov spin-up run results from jasper to ocean.
Continued work on example notebook re: plotting bathymetry data.
(MEOPAR)


Tue 25-Mar-2014
~~~~~~~~~~~~~~~

Added CGRF files for 2002-11-17 through 2002-11-26 to collection on jasper.
Copied 5nov14nov spin-up run results from Susan's workspace salish to ocean.
Finished example notebook re: plotting bathymetry data.
Extended salishsea_tools.viz_tools.set_aspect() to calculate map coordinates aspect ratio from latitudes array.
Sent email to Ashley and Shona re: getting NEMO netCDF data and results into a GIS shapefile format that they can use.
(MEOPAR)

Started implementation of functions to render ensemble bloomcast results into
new salishsea domain website framework.
(bloomcast)

Attended Susan's TU Delft seminar on SOG and blomcast.


Wed 26-Mar-2014
~~~~~~~~~~~~~~~

Added CGRF files for 2002-11-17 through 2002-11-26 to collection on jasper.
Copied 15nov19nov spin-up run results from Susan's workspace salish to ocean.
Salish Sea project mtg; see Google Drive whiteboard image file.
Added CGRF files for 2006-12-09 through 2006-12-21 to collection on jasper.
(MEOPAR)

Finished implementation of framework functions to render ensemble bloomcast results into new salishsea domain website framework.
(bloomcast)

Set up pony for 5-Apr VI200.
(RandoPony)

Wrote outline for lunch seminar at TU Delft CITG on 31-Mar.


Thu 27-Mar-2014
~~~~~~~~~~~~~~~

Investigated storage options and limits on jasper.
Only filesystem accessible storage is lustre (which is what we are using) with a quota of 1 Tb per user (1.25 Tb grace).
Silo is available for archival storage.
Restart files are 2.3 Gb each and CGRF files are 146 Mb per day, so there should be room for ~50 spin-up restart files (12 mo * 3/mo + buffer) and a few thousand days of CGRF files in my user space.
Started creation of MEOPAR/SalishSea/spin-up/ collection of restart files on jasper as project resource; rsync-ed spin-up restart files to date from salish with::

  cd MEOPAR/SalishSea/results/spin-up
  rsync -ptRz --progress */SalishSea_*_restart.nc jasper:MEOPAR/SalishSea/spin-up/

Transfer takes ~4 min per file.
Updated repos on jasper and did a clean build of NEMO-code.
Continued spin-up runs on jasper:

* 15nov19nov re-run to generate tidal harmonics files
* 30nov9dec queued

Added CGRF files for 2002-12-07 through 2002-12-10 to collection on jasper.
(MEOPAR)

Started development of spring diatom bloom prediction results web page template.
Started implementation of function to push results page and plots to web server.
(bloomcast)


Fri 28-Mar-2014
~~~~~~~~~~~~~~~

Finished implementation of function to push results page and plots to web server.
Ensemble forecast says that today is bloom day.
(bloomcast)

Improved rsync targets in Makefile.
(salishsea-site)

Checked 15nov19nov tidal harmonics file were sane and downloaded reslts to ocean.
Re-ran 30nov9dec run because its results were mixed with 15nov19nov and tidal harmonics files, etc. were therefore lost.
Re-wrote from_jasper.py script with argparer interface and put it under Mercurial.
(MEOPAR)

Started creating slide deck for lunch seminar at TU Delft CITG on 31-Mar.


Sat 29-Mar-2014
~~~~~~~~~~~~~~~

Updated spin-up page in docs.
Linked contributors file into docs.
Updated links in docs CC-By license.
Added CGRF files for 2002-12-11 through 2002-12-21 to collection on jasper.
Started 10dec19dec spin-up run; timed out.
(MEOPAR)

Worked on slide deck for lunch seminar at TU Delft CITG on 31-Mar.


Sun 30-Mar-2014
~~~~~~~~~~~~~~~

Started trying to implement bloom date evolution table in RST.
(bloomcast)

Worked on slide deck for lunch seminar at TU Delft CITG on 31-Mar.


April
=====

Week 14
-------

Mon 31-Mar-2014
~~~~~~~~~~~~~~~

After repeated failures of RST table layout, switched bloom date evolution table to Mako-generated raw html.
(bloomcast)

Determined that 10dec19dec spin-up run timed out because its end time step was accidentally set to 90 days instead of 10 days; re-queued the run.
Added CGRF files for 2002-12-12 through 2002-12-31 to collection on jasper.
Transferred results of 20nov29nov and 30nov9dec spin-up runs to ocean, and copied restart files to collection on jasper.
Tested, debugged, and improved from_jasper.py script.
(MEOPAR)

Finshed slide deck for, and gave lunch seminar on version control and software automation at TU Delft CITG.
Built a new blogofile virtualenv for working on douglatornell.ca, and added a blurb ans links to the slide deck from today's talk to my talks page.
Noted that blogofile can only be sucessfully installed from the dev repo, not from the released 0.8b1 package on PyPI.
Also, for Python 3, textiles-2.1.4-py3k has to be installed explicitly from the GitHub tarball because pip will no longer automatically download packages from external links.

Met with Marcel Zijlema (maintainer of SWAN and SWASH codes) to talk about VCSs.

Added project-specific layout template to facilitate addition of custom CSS, and added styles to control column widths and padding in bloom date evolution table of spring diatoms page from ensemble version of SoG-bloomcast.
(salishsea-site)


Tue 1-Apr-2014
~~~~~~~~~~~~~~

Tried to run ensemble bloomcast as cron job; works except for pushing results to shelob, which fails because cron is unable to use my ssh key for authentication.
(bloomcast)

Added CGRF files for 2003-01-01 to collection on jasper.
Transferred results of 10dec19dec spin-up run to ocean, and copied restart files to collection on jasper.
Started 20dec31dec spin-up run on jasper.
Added code to salishsea prepare sub-command to confirm that symlink targets exist before linking to them.
Simplified logging handler configuration in salishsea_cmd.
Started work on example notebook re: plotting tracer results on surface and depth slices.
(MEOPAR)

Set up pony for 19-Apr SI200.
(RandoPony)


Wed 2-Apr-2014
~~~~~~~~~~~~~~

Continued work on example notebook re: plotting tracer results on surface and depth slices.
20dec31dec spin-up run on jasper timed out after 18 hours with 1586 time steps to go.
Analysis shows that it took ~91.5 min per model day compared to the ~67 min that was typical of 10d runs; this is probably just due to filesystem or processor selection issues on jasper.
Re-queued 20dec31dec spin-up run on jasper with walltime increased to 20h.
Updated spin-up docs to recommend walltimes of 16.75h for 10d runs and 20h for 12d runs.
Created tools/storm_surges/SandHeadsWinds.ipynb to demonstrate how to read SOG-forcing repo historical wind data files from Sand Heads station.
(MEOPAR)

Ran ensemble bloomcast manually on salish.
(bloomcast)


Thu 3-Apr-2014
~~~~~~~~~~~~~~

20dec31dec spin-up run on jasper timed out again after 20 hours.
Queued 20dec25dec spin-up run on jasper with 12h walltime.
Continued work on example notebook re: plotting tracer results on surface and depth slices.
Added viz_tools.plot_coastline() function and refactored tidetools module to use it, deprecating tidetools.plot_coastline().
Salish Sea project mtg; see Google Drive whiteboard image file.
(MEOPAR)


Fri 4-Apr-2014
~~~~~~~~~~~~~~

Transferred results of 20dec25dec spin-up run to ocean, and copied restart files to collection on jasper.
Queued 26dec31dec spin-up run on jasper with 12h walltime.
Finished example notebook re: plotting tracer results on surface and depth slices.
Added viz_tools.calc_abs_max() function.
Refactored netCDF.Dataset pytest fixture into salishsea_tools/tests/conftest.py for shared use.
(MEOPAR)

Ran ensemble bloomcast manually on salish.
(bloomcast)


Sat 5-Apr-2014
~~~~~~~~~~~~~~

Added CGRF files for 2003-01-02 to 2003-01-11 to collection on jasper.
Queued 1jan10jan spin-up run on jasper with 18h walltime.
Refactored netCDF.Dataset pytest fixture into salishsea_tools/tests/conftest.py for shared use.
Checked progress of 1jan10jan spin-up run and found that it was running at 140-180 min per modle day; stopped the run and re-queued it with the walltime reduced to 15h in the hope that that would force it to use only fast x5675 nodes.
Re-run of 1jan10jan spin-up run also timed out.
(MEOPAR)

Ran ensemble bloomcast manually on salish.
Re-enabled ensemble cron job to run daily at 22:00 even though it will fail to push the results to shelob; at least I won't have to remember to run the job.
(bloomcast)

Sun 6-Apr-2014
~~~~~~~~~~~~~~

Travel from Delft to Vancouver.

Modified namelist.py from https://gist.github.com/krischer/4943658 to handle Salish Sea NEMO namelists:

  1. Handle double quoted strings
  2. Handle empty string as values
  3. Handle &end as group ending token
  4. Add array element assignments
  5. Relax restriction that all elements of a list assignment must be of the same type; Python lista are hetrogenous
  6. Ignore empty groups
(MEOPAR)


Week 15
-------

Mon 7-Apr-2014
~~~~~~~~~~~~~~

Forked namelist.py from https://gist.github.com/krischer/4943658 to https://gist.github.com/douglatornell/10020346 and pushed my changes to the fork.
Added CGRF files for 2006-01-31 to 2006-02-11 to collection on jasper.
Queued 1jan5jan spin-up run on jasper with 10h walltime.
Transferred results of 26dec31dec spin-up run to ocean, and copied restart files to collection on jasper.
Added comment to namelist.py gist (https://gist.github.com/krischer/4943658) with link to my fork and description/rationale re: my mods.
Added namelist module and mods to tools repo.
Started work on making `salishsea prepare` confirm that correct atmospheric forcing files exist.
(MEOPAR)

Disabled automatic push of results to shelob until rsync auth issue can be resolved.
Manually pushed results, and created shell script to do so with fewer keystrokes.
Fixed the bug whereby the production version of mixing layer depth and wind speed plot is shifted 1 day too far right.
(bloomcast)

Helped Susan get up and running on salish with a conda environment to work on tuning of summer bloomcast.
(SOG)

Updated to Python 3.4 via homebrew, but lost Python 3.3 in the process.


Tue 8-Apr-2014
~~~~~~~~~~~~~~

Transferred results of 1jan5jan spin-up run to ocean, and copied restart files to collection on jasper.
Updated default namelist.domeain, namelist.lateral, and namelist.dynamics files to contain the present spin-up run values; dt=10s, 5 barotropic time steps per dt, open Johnstone Strait boundary, and lateral eddy diffusion & evd = 20 m2/s.
Queued 6jan10jan spin-up run on jasper with 10h walltime.
Added CGRF files for 2003-01-12 to 2003-01-21 to collection on jasper.
Added function to `salishsea prepare` to confirm that correct atmospheric forcing files exist.
Salish Sea project mtg; see Google Drive whiteboard image file.
An email discussion with Masao@westgrid has cleared up what's going on with job run time; L5420 nodes run at about half the speed of X5675 nodes, and our jobs appear to the allocated either all L5420 or all X5675 nodes.
If we specify X5675 nodes only we'll likely wait longer in the queue than if we specify enough walltime for the job to finish on L5420 nodes.
Sent email to Ashley with bathymetry netCDF file attached.
Fixed axes labels in bathymetry plotting example notebook.
Queued 11jan20jan spin-up run on jasper with 30h walltime; it started on X5675 nodes at 20:45.
(MEOPAR)

Restarted buildbot master and trac server on bjossa after today's openssl patch reboot.
Restarted buildbot slaves on cod, herring, snapper, and tyee; coho and sable were not rebooted, so no slave restart necessary; nerka's ocean mount is bad, so no slave restart possible.
(SOG)

Installed Python 3.3.5 framework from python.org; plan going forward is to have python2 and python3 from homebrew which should be latest versions (presently 2.7.6 and 3.4.0) and use framework installs or conda installs for other versions.


Wed 9-Apr-2014
~~~~~~~~~~~~~~

Transferred results of 6jan10jan spin-up run to ocean, and copied restart files to collection on jasper.
Added CGRF files for 2003-01-22 to 2003-01-31 to collection on jasper.
Queued 21jan30jan spin-up run on jasper with 30h walltime.
Updated spin-up docs page with recent runs status and notes about jasper X5675 and L5420 nodes and new recommended walltimes.
Add test to confirm that namelist groups with the same name are append to the list under the group name key in the Python dict.
Added CGRF files for 2003-01-22 to 2003-01-31 to collection on jasper.
Prepared for 31jan9feb spin-up run on jasper with 30h walltime.
(MEOPAR)

Research meeting w/ Susan.

Updated conda on tom re: heartbleed bug.
Created a conda Python 3.4 environment containing IPython and the notebook dependencies.
Sent email to Susan's group re: heartbleed and updating Anaconda Python distro.


Thu 10-Apr-2014
~~~~~~~~~~~~~~~

Travel to PyCon 2014 in Montréal.
Dinner with Brett, Andrea, and Guido.
(PyCon)


Fri 11-Apr-2014
~~~~~~~~~~~~~~~

PyCon 2014 talks; see :file:`PyCon2014/notes.rst`.
PyCon dinner hosted by Brandon.
(PyCon)


Sat 12-Apr-2014
~~~~~~~~~~~~~~~

PyCon 2014 talks; see :file:`PyCon2014/notes.rst`.
(PyCon)


Sun 13-Apr-2014
~~~~~~~~~~~~~~~

PyCon 2014 talks; see :file:`PyCon2014/notes.rst`.
Dinner with Software Carpentry crew.
(PyCon)


Week 16
-------

Mon 14-Apr-2014
~~~~~~~~~~~~~~~

PyCon 2014 development sprints; worked on porting SWC version control lesson to Mercurial.
Dinner with Software Carpentry crew.
(PyCon) (SWC)


Tue 15-Apr-2014
~~~~~~~~~~~~~~~

Travel to Barrie to visit parents.

Continued work on porting SWC version control lesson to Mercurial.
(SWC)

Updated weekly project mtg whiteboard page.
Reviewed SVN updated that we haven't yet pulled from the upstream NEMO code repo.
(MEOPAR)


Wed 16-Apr-2014
~~~~~~~~~~~~~~~

Salish Sea project mtg; see Google Drive whiteboard file.
Found gfortran array bounds checking option flag for Nancy to try; -fbounds-check.
Prepared 26oct 1-core run on salish to check run rate of 1 core with lots of memoery vs. multiple cores/nodes.
(MEOPAR)


Thu 17-Apr-2014
~~~~~~~~~~~~~~~

Ran 26oct 1-core run on salish for 3.8 hours and it completed 541 time steps for a run rate of 60.7h per model day; i.e. much slower than multi-core/node runs.
Dug into array bounds error that Nancy found and concluded with Susan that it is a code smell, but not relevant to the boundary condition v-eta mixup issue.
Created notebook to check 2.5km GEM atmospheric forcing intial test dataset from EC; found that lats/lons do not correspond to our domain location and informed Kao-Shen and Luc of the problem.
(MEOPAR)


Fri 18-Apr-2014
~~~~~~~~~~~~~~~

Branched tools repo to work on changing SalishSeaCmd to a cliff cli app and set up a conda environment in which to work on it.
(MEOPAR)


Sat 19-Apr-2014
~~~~~~~~~~~~~~~

Travel from Barrie to Vancouver.

Changed SalishSeaCmd `prepare` and `gather` sub-commands to cliff command plug-ins.
Transferred results of 10feb19feb spin-up run to ocean, and copied restart files to collection on jasper.
Added CGRF files for 2003-03-03 to 2003-03-12 to collection on jasper.
Queued 2mar11mar spin-up run on jasper X5675 nodes with 16h walltime; experiment to see how queue time when fast nodes are requested compares to run time when we end up on slow nodes; queue time was a little over 1h, so a win.
(MEOPAR)


Sun 20-Apr-2014
~~~~~~~~~~~~~~~

Transferred results of 20feb1mar spin-up run to ocean, and copied restart files to collection on jasper.
Added CGRF files for 2003-03-13 to 2003-03-22 to collection on jasper.
Queued 2mar11mar spin-up run on jasper X5675 nodes with 16h walltime.
Updated spin-up docs page with recent runs status.
Changed SalishSeaCmd `combine` sub-command to cliff command plug-in.
(MEOPAR)


Week 17
-------

Mon 21-Apr-2014
~~~~~~~~~~~~~~~

Transferred results of 2mar11mar spin-up run to ocean, and copied restart files to collection on jasper.
Added CGRF files for 2003-03-23 to 2003-04-01 to collection on jasper.
Queued 12mar21mar spin-up run on jasper X5675 nodes with 16h walltime.
Changed SalishSeaCmd `get_cgrf` sub-command to cliff command plug-in.
Updated SalishSeaCmd docs.
Transferred results of 12mar21mar spin-up run to ocean, and copied restart files to collection on jasper.
Added CGRF files for 2003-04-02 to 2003-04-11 to collection on jasper.
Queued 22mar31mar spin-up run on jasper X5675 nodes with 16h walltime.
(MEOPAR)


Tue 22-Apr-2014
~~~~~~~~~~~~~~~

Added code to script that transfers results from jasper runs to ocean and spin-up collection on jasper so that ocean files and directories are group read/write-able.
Transferred results of 22mar31mar spin-up run to ocean, and copied restart files to collection on jasper.
Queued 1apr10apr spin-up run on jasper X5675 nodes with 16h walltime.
Added CGRF files for 2003-04-12 to 2003-04-21 to collection on jasper.
Tested and debugged tools-cliff branch on salish in a Python 3.4 conda environment.
Merged, tagged and released tools-cliff branch.
Started changing tidetools.get_run_length() to use namelist module.
(MEOPAR)


Wed 23-Apr-2014
~~~~~~~~~~~~~~~

Transferred results of 1apr10apr spin-up run to ocean, and copied restart files to collection on jasper.
Queued 11apr20apr spin-up run on jasper X5675 nodes with 16h walltime.
Added CGRF files for 2003-04-22 to 2003-05-01 to collection on jasper.
Salish Sea project mtg; see Google Drive whiteboard file.
Finished changing tidetools.get_run_length() to use namelist module, and fixed 2 bugs in it; run lengths could be off by orders of magnitude depending on spaces in namelist file, and run length was 1 time step less than the actual run duration.
Added CGRF files for 2009-11-13 to 2009-11-25 to collection on jasper.
Started work on example notebook re: plotting velocity field results on depth slices.
Transferred results of 11apr20apr spin-up run to ocean, and copied restart files to collection on jasper.
Queued 21apr30apr spin-up run on jasper X5675 nodes with 16h walltime.
Added CGRF files for 2003-05-02 to 2003-05-11 to collection on jasper.
(MEOPAR)

Attended Phys Ocgy seminar - Susan talking about our trip to Holland.

Surveyed tech specs of westrgid machines and concluded that the QDR nodes of orcinus are probably the next fastest to jasper's X5675 nodes.
(GEOTRACES)


Thu 24-Apr-2014
~~~~~~~~~~~~~~~

Participated in online SWC monthly lab meeting.

Continued email conversation with Diego re: open-sourcing and collaborating on oceanviewer.
Continued work on example notebook re: plotting velocity field results on depth slices.
Transferred results of 21apr30apr spin-up run to ocean, and copied restart files to collection on jasper.
Queued 1may10may spin-up run on jasper X5675 nodes with 16h walltime.
Added CGRF files for 2003-05-12 to 2003-05-21 to collection on jasper.
(MEOPAR)

Logged into orcinus, installed public ssh key, and sent email to support@westgrid requesting installation of Mercurial.
(GEOTRACES)


Fri 25-Apr-2014
~~~~~~~~~~~~~~~

Participated in CCAR-Modeling meeting w/ Susan, Paul, Xianmin, Nadja, and Tessa.
(GEOTRACES)

Transferred results of 1may10may spin-up run to ocean, and copied restart files to collection on jasper.
Queued 11may20may spin-up run on jasper X5675 nodes with 16h walltime.
Added CGRF files for 2003-05-22 to 2003-05-31 to collection on jasper.
(MEOPAR)


Sat 26-Apr-2014
~~~~~~~~~~~~~~~

Transferred results of 11may20may spin-up run to ocean, and copied restart files to collection on jasper.
Queued 21may30may spin-up run on jasper X5675 nodes with 16h walltime.
Added CGRF files for 2003-06-01 to 2003-06-10 to collection on jasper.
Investigated data storage on silo.
Discussed discrepany in the unstagger algorithm between Susan and Nancy & my implementations and Susan agreed that hers is incorrect.
(MEOPAR)


Sun 27-Apr-2014
~~~~~~~~~~~~~~~

Transferred results of 21may30may spin-up run to ocean, and copied restart files to collection on jasper.
Queued 31may9jun spin-up run on jasper X5675 nodes with 18h walltime.
Added CGRF files for 2003-06-11 to 2003-06-20 to collection on jasper.
(MEOPAR)


Week 18
-------

Mon 28-Apr-2014
~~~~~~~~~~~~~~~

31may9jun spin-up run on jasper failed due to time-out, probably related to system-wide filesystem issue that took jasper offline early this morning.
Continued work on example notebook re: plotting velocity field results on depth slices, and adding new functions to viz_tools module.
Re-queued 31may9jun spin-up run on jasper X5675 nodes with 18h walltime.
(MEOPAR)


Tue 29-Apr-2014
~~~~~~~~~~~~~~~

Continued work on example notebook re: plotting velocity field results on depth slices, and adding new functions to viz_tools module.
Changed docs repo to use sphinx-rtd-theme for local builds.
Started work on docs improvements.
Explored widgets and plots of NEMO results in IPython Notebook 2.0.
Transferred results of 10jun19jun spin-up run to ocean, and copied restart files to collection on jasper.
Queued 20jun29jun spin-up run on jasper X5675 nodes with 18h walltime.
Added CGRF files for 2003-07-01 to 2003-07-10 to collection on jasper.
(MEOPAR)


Wed 30-Apr-2014
~~~~~~~~~~~~~~~

Salish Sea project mtg; see Google Drive whiteboard file.
20jun29jun spin-up run on jasper X5675 nodes timed out with 18h walltime.
Re-queued 20jun29jun spin-up run on jasper X5675 nodes with 24h walltime.
(MEOPAR)

Attended Phys Ocgy seminar - Nancy talking about open boundary conditions.

Created CCAR-Modeling discussion group on Google Groups with Paul, Xianmin and I as owners.
Created ccar-modeling team account on Bitbucket with Paul, Xianmin and I as administrators, and Susan as a developer; sent email to Nadja and Tessa for them to create user accounts and send me their ids.
Created ccarmodeling account on readthedocs.org.
Started trying to build NEMO 3.4 on orcinus.
(GEOTRACES)


Thu 1-May-2014
~~~~~~~~~~~~~~

Transferred results of 20jun29jun spin-up run to ocean, and copied restart files to collection on jasper.
Queued 30jun9jul spin-up run on jasper X5675 nodes with 24h walltime.
Added CGRF files for 2003-07-11 to 2003-07-20 to collection on jasper.
Updated PBS files for jasper to include directive to run only on X5675 nodes.
Discussed API for viz_tools plot_coastline and plot_land_mask functions with Susan re: addition of z, x_slice, and y_slice arguments.
Decided to revert the addition of the plot_coastline call to plot_land_mask.
Added CGRF files for 2009-11-13 to 2003-11-25 to collection on ocean.
Updated all tracked PBS scripts re: permissions, reduced repetition of run id, and use of X5675 nodes on jasper.
Discussed failure of sphinxcontrib-programoutput on RTD w/ Eric on IRC; he thinks it should work.
Changed tools/docs to use sphinx-rtd-theme for local builds.
Started adding isobath, xslice & yslice args to plot_coastline and plot_land_mask viz_tools functions.
(MEOPAR)

Added Nadja and Tessa to the ccar-modeling team account on Bitbucket as a developers.
Continued trying to build NEMO 3.4 on orcinus.
Sent email to support@westgrid re: szip library and my build problems on orcinus compared to jasper.
(GEOTRACES)

Sent link to PDF copy of Linux command line book to Waterhole users.


Fri 2-May-2014
~~~~~~~~~~~~~~

Stayed home sick with body aches and fatigue.

Transferred results of 30jun9jul spin-up run to ocean, and copied restart files to collection on jasper.
Queued 10jul19jul spin-up run on jasper X5675 nodes with 24h walltime.
Added CGRF files for 2003-07-21 to 2003-07-30 to collection on jasper.
(MEOPAR)


Sun 3-May-2014
~~~~~~~~~~~~~~

Transferred results of 10jul19jul spin-up run to ocean, and copied restart files to collection on jasper.
Queued 20jul29jul spin-up run on jasper X5675 nodes with 24h walltime.
Added CGRF files for 2003-07-31 to 2003-08-09 to collection on jasper.
(MEOPAR)


May
===

Week 19
-------

Mon 5-May-2014
~~~~~~~~~~~~~~

Still home sick.

Finished adding isobath arg to plot_coastline and plot_land_mask viz_tools functions.
Transferred results of 20jul29jul spin-up run to ocean, and copied restart files to collection on jasper.
Queued 30jul8aug spin-up run on jasper X5675 nodes with 24h walltime.
Added CGRF files for 2003-08-10 to 2003-08-19 to collection on jasper.
Finished adding xslice & yslice args to plot_coastline and plot_land_mask viz_tools functions () harder than expected.
Updated example notebook re: plotting velocity field results on depth slices to use slices for land mask; much faster.
Confirmed that readthedocs build virtualenv bin/ dir is not on path, so program-output extension cannot work for salishsea command help docs generation.
(MEOPAR)


Tue 6-May-2014
~~~~~~~~~~~~~~

Still home sick.

Transferred results of 30jul8aug spin-up run to ocean, and copied restart files to collection on jasper.
Queued 9aug18aug spin-up run on jasper X5675 nodes with 24h walltime.
Added CGRF files for 2003-08-20 to 2003-08-29 to collection on jasper.
Helped Susan thrash through out of date SalishSeaTools installation on salish that caused SalishSeaCmd to fail.
Reverted salishsea command docs to pasted output from shell because program-output extension does not work on readthedocs.org; opened issue#814 in rtfd/readthedocs.org GitHub repo explaining the issue.
(MEOPAR)


Wed 7-May-2014
~~~~~~~~~~~~~~

Salish Sea project mtg; see Google Drive whiteboard file.
Copied Apr spin-up restart files and 15apr-15may-2003 atmospheric forcing files from jasper to orcinus in hopes of continuing Susan and Nancy's tide test runs there next week while jasper is down.
Reviewed report from Jun-2013 stakeholder's workshop.
(MEOPAR)

Restarted build slaves on cod and tyee after recent reboots; the latter highlighted a DNS issue for Charles.
Also finally got nerka slave working again - another configuration issue, not an autofs issue as I thought.
(SOG)


Thu 8-May-2014
~~~~~~~~~~~~~~

Created tools repo issue#11 re: :command:`salishsea prepare` cleanup failing when restart file is not found; reported by Nancy.
Created tools repo issued #12 re: :command:`salishsea prepare` atmospheric forcing files checking being too sensitive (fails if atmos files are missing even if atmospheric forcing it disabled for run); reported by Susan.
Marked tools repo issue#13 reported by Susan as a duplicate of issue#12.
Continued work on improving working environment section of docs.
(MEOPAR)

Attended 3 Minute Postdoc Slam; Nancy won a runner-up prize and I got a coffee card for live-tweeting :-)


Fri 9-May-2014
~~~~~~~~~~~~~~

9aug18aug spin-up run that has been queued since 6-May finally started running.
Continued work on improving working environment section of docs.
Participated in mtg of UBC MEOPAR collaborators to plan June stakeholders workshop.
Transferred results of 9aug18aug spin-up run to ocean, and copied restart file to collection on jasper.
Queued 19aug28aug spin-up run on jasper X5675 nodes with 24h walltime.
Added CGRF files for 2003-08-30 to 2003-09-08 to collection on jasper.
(MEOPAR)

Helped Ashley get started on Linux, hg, and nerka.
(GEOTRACES)


Sat 10-May-2014
~~~~~~~~~~~~~~~

Transferred results of 19aug28aug spin-up run to ocean, and copied restart file to collection on jasper.
Queued 29aug7sep spin-up run on jasper X5675 nodes with 24h walltime.
Added CGRF files for 2003-09-09 to 2003-09-18 to collection on jasper.
Copied CGRF files for 2003-09-01 to 2003-09-18 to collection on orcinus.
(MEOPAR)


Sun 11-May-2014
~~~~~~~~~~~~~~~

Transferred results of 29aug7sep spin-up run to ocean, and copied restart files to collection on jasper.
Queued 8sep17sep spin-up run on jasper X5675 nodes with 24h walltime.
Added CGRF files for 2003-09-19 to 2003-09-28 to collection on jasper.
Copied CGRF files for 2003-09-19 to 2003-09-18 to collection on orcinus.
Investigated splitting a Mercurial repo; hg convert and a file/directory mapping is the key.
Started work on :command:`salishsea run` sub-command.
Transferred results of 8sep17sep spin-up run to ocean, and copied restart file to collections on jasper and orcinus.
(MEOPAR)


Week 20
-------

Mon 12-May-2014
~~~~~~~~~~~~~~~

jasper.westgrid.ca down for 5 days maintenance.

Helped Nancy resolve a bad :command:`salishsea gather` on salish.
Helped Nancy sort out .bashrc and .bash_profile issued on salish; the latter file was missing.
Worked on salishsea site index page image; figured out how to do circular clips of plot images and adjust their alpha transparency so that site section titles can be overlaid.
(MEOPAR)

Helped Ashley get set up to work through MEOPAR example notebooks.
(GEOTRACES)


Tue 13-May-2014
~~~~~~~~~~~~~~~

Finished salishsea site index page image sufficiently for it to launch on the site.
Thought about splitting analysis work out of tools repo into a new analysis repo and discussed the logistics with Susan; outlined plan in weekly Google Doc.
Worked on content for salishsea site.
(MEOPAR)


Wed 14-May-2014
~~~~~~~~~~~~~~~

Attended EOAS dept forum re: Roger Beckie's headship candidacy.

Salish Sea project mtg; see Google Drive whiteboard file.
Continued working on content for salishsea site; particularly NEMO model section landing page.
(MEOPAR)


Thu 15-May-2014
~~~~~~~~~~~~~~~

Worked at home so that I could do some bike maintenance.

Committed to having Mercurial lesson pull request ready for vote at 22-May SWC lab meeting.
Cherry-picked revs from @jdcorless into Mercurial lesson pull request.
Updated PR todo list.
(SWC)

Added notes about Linux Command Line book and SWC shell quick ref to bash section of docs.
Added Jackie Yip to SCARP collaborators team list on salishsea site NEMO model page.
Queued 18sep27sep spin-up run on jasper X5675 nodes with 24h walltime, and on slow nodes with 36h walltime..
Added CGRF files for 2003-09-29 to 2003-10-08 to collection on jasper.
(MEOPAR)


Fri 16-May-2014
~~~~~~~~~~~~~~~

Helped Nancy with recurring bug in :command:`salishsea gather` on salish; see tools repo issue#15; os.rename[s]() fails if source and destination are on different filesystems, replaced with shutil.move().
Reviewed questionnaire for stakeholders workshop and discussed it with Nancy.
Split the tools repo to separate analysis directories into a new analysis repo, and updated docs and notebooks to reflect the change.
Started work on storm surge portal page on salishsea site.
(MEOPAR)


Sat 17-May-2014
~~~~~~~~~~~~~~~

Transferred results of 18sep27sep spin-up run to ocean, and copied restart files to collection on jasper.
Changed domain namelist to use flux-corrected northern boundary tide files.
Queued 28sep7oct spin-up run on jasper X5675 nodes with 24h walltime.
Added CGRF files for 2003-10-09 to 2003-10-18 to collection on jasper.
(MEOPAR)


Sun 18-May-2014
~~~~~~~~~~~~~~~

:file:`/ocean/` mount not accessible on salish or sable.

Hard linked restart file from 28sep7oct spin-up run to spin-up collection on jasper.
Queued 8oct17oct spin-up run on jasper X5675 nodes with 24h walltime.
Added CGRF files for 2003-10-19 to 2003-10-28 to collection on jasper.
(MEOPAR)


Week 21
-------

Mon 19-May-2014
~~~~~~~~~~~~~~~

:file:`/ocean/` mount was inaccessible on salish and sable in the morning but came back online sometime before mid-afternoon.

Hard linked restart file from 8oct17oct spin-up run to spin-up collection on jasper.
Queued 18oct27oct spin-up run on jasper X5675 nodes with 24h walltime.
Added CGRF files for 2003-10-29 to 2003-11-07 to collection on jasper.
Finished storm surge portal page on salishsea site and pushed it to shelob.
(MEOPAR)

Moved non-regressable emily backup directory aside on matisse so that a new one will start.

Sent email to try to push Mercurial lesson review to closure.
(SWC)


Tue 20-May-2014
~~~~~~~~~~~~~~~

Worked on getting Mercurial lesson pull request ready for vote at Thursday's SWC lab mtg.
Cherry-picked Jordi's work on 03-conflict.md.
Built lesson and uploaded it to http://eos.ubc.ca/~dlatorne/swc/novice/hg/.
Resolved issue re: screen shot width attributes.
Added discussion of :command:`hg revert` and :file:`*.orig` files.
Merged PR re: GitHub -> Bitbucket in SVGs in 03-conflict.md, but images have excess whitespace below them.
(SWC)

Participated in UBC collaborators meeting and learned lots about indicators and risk work that SCARP team are doing.
Changed :file:`from_jasper.py` script to hard link restart file on jasper instead of copying.
Transferred results of 28sep7oct, 8oct17oct, and 18oct27oct spin-up runs to ocean, and hard linked restart files to collection on jasper.
Queued 28oct6nov spin-up run on jasper X5675 nodes with 24h walltime.
Added CGRF files for 2003-11-08 to 2003-11-17 to collection on jasper.
(MEOPAR)


Wed 21-May-2014
~~~~~~~~~~~~~~~

Salish Sea project mtg; see Google Drive whiteboard file.
Worked on :command:`salishsea run`.
Transferred results of 28oct6nov spin-up run to ocean, and hard linked restart files to collection on jasper.
Queued 7nov16nov spin-up run on jasper X5675 nodes with 24h walltime.
Added CGRF files for 2003-11-18 to 2004-01-01 to collection on jasper.
(MEOPAR)


Continued getting Mercurial lesson pull request ready for vote at Thursday's SWC lab mtg.
Stalled out on merge conflict handling because Jordi wants to include GUI tools but doesn't want to deal with :kbd:`[merge-tools]` config on OS/X; waiting for email thread input from other hg-list members.
Confirmed that file annotation is the default on OS/X and Ubuntu, provided that the user does not have a merge tools specified in their config; Jordi sees different on Debian and Windows/TortoiseHg.
(SWC)

Attended Phys Ocgy seminar: Mark & Nancy presented trial runs of one of their CMOS talks.


Thu 22-May-2014
~~~~~~~~~~~~~~~

Participated monthly SWC lab meeting; sufficient support for Mercurial lesson that it will be merged, but no further input yet on merge conflicts & GUI tools issue.
(SWC)

Continued work on :command:`salishsea run`.
(MEOPAR)

Experimented with ipdb in ipython notebook - useable.
Helped Ashley debug her initial 2D advection/diffusion model.
(GEOTRACES)


Fri 23-May-2014
~~~~~~~~~~~~~~~

Transferred results of 7nov16nov spin-up run to ocean, and hard linked restart files to collection on jasper.
Queued 17nov26nov spin-up run on jasper X5675 nodes with 24h walltime.
Added CGRF files for 2003-09-16 to 2003-09-19 to collection on salish.
Started work on slides for CMOS talk on collaboration tools.
(MEOPAR)

Researched Mercurial default merge behaviour further and found that it depends on both the presence and location of :file:`mergetools.rc` and the presence of a tool mentioned in that file on :envvar:`$PATH`. OS/X lacks :file:`mergetools.rc`, salish lacks all of the mentioned tools, but jasper has vimdiff.
Added my findings to the email thread.
(SWC)

Helped Ashley locate the source of a divide by zero runtime error, and learned about toggling line numbers in ipynb, and controlling warnings via envar in Python.
(GEOTRACES)


Sun 25-May-2014
~~~~~~~~~~~~~~~

Transferred results of 17nov26nov spin-up run to ocean, and hard linked restart files to collection on jasper.
Queued 27nov6dec spin-up run on jasper X5675 nodes with 24h walltime.
(MEOPAR)


Week 22
-------

Mon 26-May-2014
~~~~~~~~~~~~~~~

Created local Pa-Th repo for Ashley's work; waiting for copyright holder info from Nadja before creating repo on Bitbucket.
(GEOTRACES)

Continued work on slides for CMOS talk on collaboration tools.
(MEOPAR)


Tue 27-May-2014
~~~~~~~~~~~~~~~

Started testing batch runs of NEMO on salish via :command:`at`.
Added CGRF files for 2006-01-31 to 2006-02-09 to collection on salish.
Finished 1st draft of slides for CMOS talk on collaboration tools.
Transferred results of 27nov6dec spin-up run to ocean, and hard linked restart files to collection on jasper.
Queued 7dec16dec spin-up run on jasper X5675 nodes with 24h walltime.
(MEOPAR)

Wrote APEGBC registration reference for Jeff Wood.


Wed 28-May-2014
~~~~~~~~~~~~~~~

Worked on inbox 0-ish.

Started work on example notebook re: plotting on vertical planes; especially thalweg plot, working toward animation of annual salinity cycle.
Salish Sea project mtg; see Google Drive whiteboard file.
Prepared for and gave CMOS practice test run in Phys Ocgy seminar.
Improved CMOS talk slide deck based on feedback from practice talk.
Started work on cleaning up analysis/compare_tides/comp_wlev_harm-wNorth.ipynb notebook and improving tidetools.plot_scatter_pha_amp() function.
(MEOPAR)


Thu 29-May-2014
~~~~~~~~~~~~~~~

Finished improving tidetools.plot_scatter_pha_amp() function and cleanup of  analysis/compare_tides/comp_wlev_harm-wNorth.ipynb.
Helped Susan sort out her very messed up PYTHONPATH.
(MEOPAR)

Pa-Th model team meeting; see Google Drive whiteboard file.
Created Pa-Th repo on Bitbucket.
Helped Ashley get up to speed with hg and Bitbucket, and moving code from IPython Notebook to importable modules.
(GEOTRACES)


Fri 30-May-2014
~~~~~~~~~~~~~~~

Transferred results of 7dec16dec spin-up run to ocean, and hard linked restart files to collection on jasper.
Queued 17dec26dec spin-up run on jasper X5675 nodes with 24h walltime.
Discussed terrible scheduling of Nancy's CMOS talk and how I can advertise it in my talk.
Worked on building NEMO on orcinus now that Roman has built netcdf libraries for us.
Resumed checking 2.5km GEM atmospheric forcing intial test dataset from EC; now with correct lats/lons.
(MEOPAR)

Sent email to Neil with suggestions for talk topics for 23-Jun at CCCma.
Closed the loop on Will's email re: talking about Cython.

Changed Government of Canada copyright holder to Fisheries and Oceans Canada per email from Nadja.
Set up Pa-Th repo docs on readthe docs.org.
Assed Ashley to CCAR-Modeling Google group.
Changed CCAR-Modeling Google group to default to reply-to-group.
Posted to CCAR-Modeling group about creation of Pa-Th repo and readthedocs site.
(GEOTRACES)


Sat 31-May-2014
~~~~~~~~~~~~~~~

Travel to Rimouski for CMOS congress.

Worked on flake8 cleanup of SalishSeaTools.tidetools module.
(MEOPAR)


Sun 1-Jun-2014
~~~~~~~~~~~~~~

Transferred results of 17dec26dec spin-up run to ocean, and hard linked restart files to collection on jasper.
Queued 27dec31dec spin-up run on jasper X5675 nodes with 12h walltime.
Annotated runs with 5-day restart files in spin-up docs, and noted on the whiteboard the 7 runs that would have to be repeated to give us 5-day restart from 28Oct through 1Mar.
(MEOPAR)


June
====

Week 23
-------

Mon 2-Jun-2014
~~~~~~~~~~~~~~

Attended CMOS conference in Rimouski.
Participated in GEOTRACES lunch meeting w/ Susan, Paul, Nadja, and Xianmin.
Presented "Software Collaboration Tools and the Salish Sea MEOPAR Project" and it was well received.

Transferred results of 27dec31dec spin-up run to ocean, and hard linked restart files to collection on jasper.
(MEOPAR)

Tue 3-Jan-2014
~~~~~~~~~~~~~~

Attended CMOS conference in Rimouski.
William Hsieh was awarded the EC Patterson medal, and Paul Harrison wond the DFO Parsons medal.


Wed 4-Jan-2014
~~~~~~~~~~~~~~

Attended CMOS conference in Rimouski.
Nancy won the Tertia Hughes prize for best thesis.


Thu 5-Jan-2014
~~~~~~~~~~~~~~

Attended CMOS conference in Rimouski.
Participated in MEOPAR breakfast meeting w/ Susan, Nancy, Keith, Youyu, Hal, J-P, and Fatemeh.

Hiked in Bic provincial part in the afternoon with Susan, Nancy, Mark & Ben.


Fri 6-Jun-2014
~~~~~~~~~~~~~~

Travel to Québec City.


Sat 7-Jun-2014
~~~~~~~~~~~~~~

Toured Québec.


Sun 8-Jun-2014
~~~~~~~~~~~~~~

Toured Québec in the morning.

Traveled to Vancouver.

Worked on flake8 cleanup of SalishSeaTools.tidetools module, and refactoring plotting functions to return figure objects instead of saving figure image files to disk.
(MEOPAR)


Week 24
-------

Mon 9-Jun-2014
~~~~~~~~~~~~~~


(MEOPAR)


Tue 10-Jun-2014
~~~~~~~~~~~~~~~

Met w/ Roman re: undefined references linking failure on orcinus; concluded that it is an FCM issue whereby the object library files is not created, or deleted before linking.
Did 6h 21apr evd=3 profiling runs on orcinus:

* 6x14 2Gb QDR: 21:36
* 7x16 2Gb QDR: 17:46
* 8x18 2Gb QDR: 11:27
* 9x20 2Gb QDR: 9:21
* 10x22 2Gb QDR: 8:20

Continued checking 2.5km GEM atmospheric forcing initial test dataset from EC; atmospheric pressure values are surface rather than sea level that NEMO expects.
(MEOPAR)

Studied Ashley's Pa-Th code to develop ideas for refactoring and speed ups.
(GEOTRACES)


Wed 11-Jun-2014
~~~~~~~~~~~~~~~

Discussed Pa-Th code refactoring ideas with Ashley.
(GEOTRACES)

Attended Phys Ocgy seminar where Susan did an extended presentation of her CMOS talk on downwelling canyons.

Continued 6h 21apr evd=3 profiling runs on orcinus:

* 11x25 2Gb QDR: 7:19
* 12x27 2Gb QDR: 5:55
* 13x29 2Gb QDR: 6:34
* 14x32 2Gb QDR: 5:30
* 15x34 2Gb QDR: 4:38
* 16x36 2Gb QDR: 4:30

See plots at http://nbviewer.ipython.org/gist/douglatornell/9e140cb555c07344b2e4
Total CPU hrs jumps up at 13x29, so 12x27 appears to be the sweet spot.

Struggled to figure out how to repeatably build NEMO on orcinus.
Apparently link steps can only be run at SHLVL=1.
(MEOPAR)


Thu 12-Jun-2014
~~~~~~~~~~~~~~~

Finished an initial implementation of `salishsea run` that works on jasper and orcinus.
Started 6h 21apr evd=3 profiling runs on jasper:

* 6x14 2Gb X5675: 19:34
* 7x16 2Gb X5675: 14:16
* 8x18 2Gb X5675: 12:40
* 9x20 2Gb X5675: 9:08
* 10x22 2Gb X5675: 8:06

See plots at http://nbviewer.ipython.org/gist/douglatornell/9e140cb555c07344b2e4
(MEOPAR)


Fri 13-Jun-2014
~~~~~~~~~~~~~~~

Continued 6h 21apr evd=3 profiling runs on orcinus:

* 11x25 2Gb X5675: 6:05
* 12x27 2Gb X5675: 6:04
* 13x29 2Gb X5675: 5:25

See plots at http://nbviewer.ipython.org/gist/douglatornell/9e140cb555c07344b2e4

Finally succeeded in creating a brittle but repeatable build script for orcinus; how intel and netcdf_hdf5 modules are loaded turns out to matter too.
Queued 5d 12x27 evd=4 tide run on orcinus.
(MEOPAR)


Week 25
-------

Mon 16-Jun-2014
~~~~~~~~~~~~~~~

Charles told me that when he updated salish to Ubuntu 14.04 a bug that was preventing TORQUE from working was resolved.
Worked on testing qsub execution of NEMO on salish.
Found that executable needs to be re-built because the version of gfortran and some other libraries has been bumped.
The -cpp compiler flag is now required to successfully build the IO server, but that causes a failure in a comment in NEMOGCM/EXTERNAL/XMLF90/src/xpath/m_path.f90.
Eventually got runs working via qsub; issues:

* PBS procs, pmem, and walltime directives are probably all irrelevant
* PBS -o and -e directives do not work; hoping Charles can fix that
* PBS -m and -M directives do not work; hoping Charles can fix that
* mpirun need its -n option flag

Got a 5d run on orcinus initiated by :command:`salishsea run` that included gathering of results and deletion of temporary run directory; at job is not required for run directory deletion.
(MEOPAR)

Worked with Ashley on the next step of refactoring here Pa-Th model: isolation and vectorization of the advection scheme function.
Introduced her to unit testing and pytest.
(GEOTRACES)


Tue 17-Jun-2014
~~~~~~~~~~~~~~~

Added Hal Ritchie's CMOS slide deck, my CMOS slide deck and source files, and a collection of logo image files to private-docs repo.
(MEOPAR)

Started work on talk for CCCma using IPython Notebook reveal.js slide conversion as a test.

Worked with Ashley on isolation and vectorization of the advection scheme function.
(GEOTRACES)


Wed 18-Jun-2014
~~~~~~~~~~~~~~~

Travel to Halifax for MEOPAR Scientific Mtg; 2 hr flight delay in Montréal.

Continued work on talk for CCCma using IPython Notebook reveal.js slide conversion as a test.

Continued checking 2.5km GEM atmospheric forcing initial test dataset from EC; added air temperature and specific humidity.
(MEOPAR)


Thu 19-Jun-2014
~~~~~~~~~~~~~~~

Continued checking 2.5km GEM atmospheric forcing initial test dataset from EC; refactored plots to be 2-up, and added precipitation, and thermal & solar radiation.
Participated in NEMO modeling meeting at Dalhousie.
Attended MEOPAR/Industry luncheon.
Met with Diego & Susan re: OceanViewer development and possible use on the west coast.
Attended MEOPAR boat cruise around Halifax harbour; talked to Rich about Python implementation or wrapper for the new sea water equation of state utilities.
(MEOPAR)


Fri 20-Jun-2014
~~~~~~~~~~~~~~~

Attended MEOPAR Scientific Mtg.
Lobster dinner with Susan and Ken Denman.
(MEOPAR)


Sat 21-Jun-2014
~~~~~~~~~~~~~~~

Travel from Halifax to Vancouver.

Continued work on talk for CCCma.


Sun 22-Jun-2014
~~~~~~~~~~~~~~~

Finished slide deck for CCCma talk.

Travel to Sidney for talk at CCCma.


Week 26
-------

Mon 23-Jun-2014
~~~~~~~~~~~~~~~

Gave talk to CCCma Python user's group about version control and Python as a tools and glue language.
Met with Neil Swart, Colin Goldblatt, and CCCma model runtime diagnostics developers group.

Travel home from CCCma.


Tue 24-Jun-2014
~~~~~~~~~~~~~~~

Added section about netCDF & visualization notebooks to working environment section of docs.
Continued work on analysis_tools notebooks; added section on streamline plots; created new notebook re: plotting velocities and tracers on vertical planes.
Prepared for Phys Ocgy seminar.
(MEOPAR)


Wed 25-Jun-2014
~~~~~~~~~~~~~~~

Salish Sea project mtg; see Google Drive whiteboard file.
Reviewed 2.5km GEM atmospheric forcing initial test dataset analysis notebook w/ Susan and Nancy and updated comments and actions.
Worked on thalweg section salinity plot example.
Gave Phys Ocgy seminar entitle "Snake Eyes: Using Python to Visualize netCDF Model Results".
(MEOPAR)


Thu 26-Jun-2014
~~~~~~~~~~~~~~~

Participated in Salish Sea MEOPAR stakeholders workshop at Green College.
Added time_origin and timestamp functions to nc_tools module.
(MEOPAR)


Week 34
-------

Mon 18-Aug-2014
^^^^^^^^^^^^^^^

Cloned NEMO-code, tools, docs, NEMO_EastCoast, SS-run-sets, NEMO-forcing, private-docs, Storm-Surge, and salishsea-stie repos and updated analysis repo on Ubuntu machine.
NEMO-code repo raised an "abort: revlog decompress error: Error -3 while decompressing data: incorrect data check!" error during the updating to branch default part of the operation on the first clone attempt; deleted clone and tried again with success.
Sent email to Kao-Shen et al re: next step of getting 2.5km atmospheric forcing files for 13-21 Dec-2012 for Nancy to use to run that storm surge case.
Added success messages to the orcinus_build.sh scripts and examples of their expected output to the orcinus quick-start docs; all to add clarity to the fact that those scripts throw failure messages as part of their normal operation.
Fixed build issue on salish wherein C pre-processor had to be enabled in arch-salish.fcm, but that caused comments in EXTERNAL/XMLF90/src/xpath/m_path.f90 to be interpreted as cpp directives; resolved by enclosing offending comments in quotes.
Created NEMO online interpolation weights file for 2.5km GEM atmospheric forcing dataset.
(MEOPAR)
