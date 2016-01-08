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

* refactor, unit tests & docs for forcing links checking for NEMO-3.6
* update quick-start docs re: NEMO-3.6 - Elise???
* finish run_NEMO36 unit tests

Continued work on operational nowcast talk for 11-Jan Phys Ocgy seminar.
(MEOPAR)

Mtg w/ Jackie re: new HVSI indicator data, app progress, and design details.
(sealinkd)

Attended Dept Colloquium on clay sedimentation in salt water by Bruce Sutherland.


ToDo

====
* Ping Youyu re: NEMO nowcast project.

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
