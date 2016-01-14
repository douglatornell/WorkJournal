*****************
2016 Work Journal
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

Mon 4-Jan-2016
^^^^^^^^^^^^^^

Restarted nowcast mgr after end-of-day to enable automation of PMV feed.
Finished enough implementation of run_NEMO36 worker that it should be able to run nowcast-green on salish; figured out how to paraeterize unit tests re: absolute paths in run description; lots of other unit tests need to be written.
(MEOPAR)

Created 2016 journal file and did catch-up summary of holidays work to end 2015 journal.

Attended Phys Ocgy seminar by Susan on barotropic tides in the Salish Sea NEMO model.


Tue 5-Jan-2015
^^^^^^^^^^^^^^

Started work on operational nowcast talk for 11-Jan Phys Ocgy seminar.

Automated feed generation worked for forecast/04jan16 and forecast2/04jan15 runs.
Tested run_NEMO36 worker in collaborations with Susan to launch nowcast-green run.; not yet ready for integration w/ mgr.
Salish Sea team group meeting; see Google Drive whiteboard.
(MEOPAR)


Wed 6-Jan-2015
^^^^^^^^^^^^^^

Salvaged files off flaky ONC flash drive.
Explored Google drive pull/push utility for Linux: https://github.com/odeke-em/drive
Wrote docs re: Insurgency server: personal/insserver.rst

Pinged Ken re: overdue Nordion invoices.
Pinged Kevin re: overdue UBC SCARP invoice.
(43ravens)

Handled ZeroDivisionError exceptions on Compare page as NA HVSI values per 27Dec15 email from Jackie; also changed layout of map and bar graph panels as she requested.
Delayed rounding of HVSI values until they are displayed as numbers on Analysis page.
Started exploring Bootstrap popovers for Compare page; probably not a good idea because there is too much data per panel to display well in a popover, perhaps a table below the bar chart panels.
Started exploring mapbox.com to generate map images.
(sealinkd)


Thu 7-Jan-2016
^^^^^^^^^^^^^^

Continued work on operational nowcast talk for 11-Jan Phys Ocgy seminar.
(MEOPAR)

Mtg w/ Jackie re: new HVSI indicator data, app progress, and design details.
Got latest update of data spreadsheet for app.
(sealinkd)

Attended Dept Colloquium on clay sedimentation in salt water by Bruce Sutherland.


Fri 8-Jan-2016
^^^^^^^^^^^^^^

Struggled to install Mapbox Studio Classic on kudu due to node.js and npm issues; ultimately gave up.
Installed Mapbox Studio Classic on tom and created & uploaded a label-less map that I can access via the static API.
Mapbox Studio Classic and static API were a bust; switched to Mapbox.js and made lots of progress on Compare page map.
Corrected mix-up of Squamish and Sooke coordinates in HVSI data spreadsheet.
Corrected spelling mismatches between Communitites and Data sheets in HVSU data spreadsheet for City & District of North Van, and Comox C (Puntledge - Black Creek).
Added marker lat & lon attrs to Community data model object.
Re-created dev database and loaded it from the 6Jan HVSI data spreadsheet.
(sealinkd)

Discussed with Susan slides for operational nowcast talk for 11-Jan Phys Ocgy seminar, and continued to work on them.
Helped Susan launch nowcast-green worker on salish.
Help Susan get Jie's mess sorted out on orcinus.
Helped Kyle get Anaconda usable on jasper.
(MEOPAR)


Sat 9-Jan-2016
^^^^^^^^^^^^^^

Nowcast critical error: make_plots worker failed at 04:13, but that was because the forecast2 run didn't produce results. That was due to 5 of the nodes having dropped their sshfs connections to the shared storage.
(MEOPAR)

Finished implementation of map on Compare page that shows communities that are being compared; marker coordinates come from database, and marker on-click events load the community's Profile page.
Re-created prod database and loaded it from the 6Jan HVSI data spreadsheet.
Deployed Compare page map feature to production, after a minor thrash due to section names in production.ini; model scripts now need to be run with `production.ini#sealinkd`.
(sealinkd)


Sun 10-Jan-2016
^^^^^^^^^^^^^^^

Worked on tools repo docs; got nowcast model changes docs up to date.
Worked w/ Susan on refactoring nowcast.figures.website_thumbnail().
(MEOPAR)


Week 2
------

Mon 11-Jan-2016
^^^^^^^^^^^^^^^

Tidied, stored & committed work on kudu in preparation for working at UBC for a few days.
Finished slides for operational nowcast talk and delivered it at the Phys Ocgy seminar.
Sorted out Jie's salishsea gather problem; circular import issue between run and api modules; my bad.
(MEOPAR)


Tue 12-Jan-2016
^^^^^^^^^^^^^^^

Fixed bugs in make_feeds worker that showed up the 1st time that a feed entry was generated under automation.
Fixed circular import bug in SalishSeaCmd package by moving pbs_common() and td2hms() functions from run to api module.
Re-closed tools repo SalishSeaNowcat branch that Muriel accidentally re-opened a while ago.
Created mixing-paper and internal-tides-paper groups in team account on Bitbucket and changed access to the corresponding repos so that only those groups & admins have write access.
Started work on generating datasets.xml file for skookum ERDDAP server.
Salish Sea team group meeting; see Google Drive whiteboard.
(MEOPAR)


Wed 13-Jan-2016
^^^^^^^^^^^^^^^

* refactor, unit tests & docs for forcing links checking for NEMO-3.6
* update quick-start docs re: NEMO-3.6 - Elise???
* finish run_NEMO36 unit tests

Attended Compute Canada SPARC2 consultation session; see notebook.

Pinged Youyu re: NEMO nowcast project and got a positive response.

Authorized Charles to buy 2x8Tb archive drives to enlarge backup on salish & skookum; salish storage will be reconfigured from 2x3Tb RAID 1 to 3x3Tb RAID 5.
Continued work on refactoring website_thumbnail() function in nowcast.figures.
Continued work on generating datasets.xml file for skookum ERDDAP server, and actually landed a test version of the CampbellRiver.nc dataset.
(MEOPAR)

Worked on notebook to validate HVSI calcs module against Jackie's spreadsheet calcs; v1 doesn't agree :-(
(sealinkd)


ToDo
====

* get HTTPS working for alternate sealinkd app domain names
* reduce resolution of landing page images for faster load times
* add docs re: sealinkd server-side app framework
* add EduCloud deployment docs
* deploy Piwik
* implement user mgmt

* update storm surge paper refs w/ doi link
* research_ferries module
* JSON logging use example notebook
* numpy.testing assert weirdness

* review remaining nosy PRs
