*****************
2014 Work Journal
*****************

This is my public work journal.
It is patterned after one that I have kept for several years for my work at Nordion_.
This journal is about my work as a Research Associate with `Dr. Susan Allen`_ in the `Department of Earth, Ocean and Atmospheric Sciences`_ at the `University of British Columbia`_ during our sabbatical which started on 1 July 2013.
It is also about my `open-source activities`_.


January
=======

Week 1
------

Wed 1-Jan-2014
~~~~~~~~~~~~~~

Changed web remote app to by run via Pyramid pserve utility but stummbled on entry point issue when I deployed it to the RaspPi.
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
