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

Attended Compute Canada SPARC2 consultation session; see notebook.

Pinged Youyu re: NEMO nowcast project and got a positive response.

Authorized Charles to buy 2x8Tb archive drives to enlarge backup on salish & skookum; salish storage will be reconfigured from 2x3Tb RAID 1 to 3x3Tb RAID 5.
Continued work on refactoring website_thumbnail() function in nowcast.figures.
Continued work on generating datasets.xml file for skookum ERDDAP server, and actually landed a test version of the CampbellRiver.nc dataset.
(MEOPAR)

Worked on notebook to validate HVSI calcs module against Jackie's spreadsheet calcs; v1 doesn't agree :-(
(sealinkd)


Thu 14-Jan-2016
^^^^^^^^^^^^^^^

Prepared for and helped Elise lead workout session code review/refactoring of nowcast-green plotting notebook that Susan claims is slow.
(swc)

Continued work on generating datasets.xml file for skookum ERDDAP server, and landed the real nowcast PointAtkinson.nc dataset.
Attended dept colloquium by Julie Laroche from Dal re: T. oceania and iron limitation; mostly omics.
Discussed priorities
(MEOPAR)


Fri 15-Jan-2015
^^^^^^^^^^^^^^^

Dentist appt.

Tweaked admin permissions for new paper repos.
Added ERDDAP as component in tools repo issue tracker.
Created tools repo issue #27 re: inconsistent time interval in tide gauge station ERDDAP results datasets.
Created tools repo issue #28 re: inclusion of run type in ERDDAP dataset ids.
Refined ERDDAP dataset setup docs, and discussed metadata w/ Susan.
(MEOPAR)

Continued work on notebook to validate HVSI calcs module againse Jackie's spreadsheet to the point where I am convinced that I am correct; pushed the notebook to the app site so that Jackie can use nbviewer to look at it.
Added map to Start page and pushed to production.
(sealinkd)


Sat 16-Jan-2016
^^^^^^^^^^^^^^^

Finished initial work on adding maps to Maps page; with main map markers that are colour-coded by HVSI range, and page guidance in a legend panel on the main map; pushed to production.
Finally resolved too-persistent CSS caching issue; nginx sendfile setting interactions with Vagrant & virtualbox.
Added HVSI values colour-bar to title legend of Maps page main map.
Added colour-coded community markers to Maps page sidebar maps.
Worked on adding HVSI values to marker popups on Maps page main map.
(sealinkd)


Sun 17-Jan-2016
^^^^^^^^^^^^^^^

Confirmed that skookum ERDDAP server is automatically extending nowcast Point Atkinson sea surface height dataset based on :kbd:`reloadEveryNMinutes` dataset value.
Looked at the numpy.testing.assert_array_equal() weirdness that Nancy reported months ago; no real resolution other than calling the function w/ an int and and array is using it wrong even though it doesn't complain.
(MEOPAR)

Restarted build slaves on cod, coho, herring, sable, and snapper.
(SOG)

Re-ran HVSI validation notebook w/ Jan9 spreadsheet from Jackie; no useful difference, but lots more "no data" situations to deal with.
Finished on adding HVSI values to marker popups on Maps page main map.
Found and corrected bug in how joins were specified in Indicator and IndicatorValue data model object.
(sealinkd)


Week 3
------

Mon 18-Jan-2016
^^^^^^^^^^^^^^^

Jackie confirmed that there were errors in her HVSI calc validation spreadsheet; her revisions and my fix of the join bug result in agreement for the validation cases.
Jakie is happy with the maps on the Start and Maps pages, but requested a monochrome colour-bar palette so I told her to provide the palette and it can be so.
(sealinkd)

Investigated stoppage of ONC-ADCP data downloads on 31-Dec-2015; probably happened due to 2016 not being included in years arrays in case statement in GETDEPL.m script.
Continued working on ERDDAP server setup & docs; got Charles to restart server w/ corrected config to put files in /results/erddap/, but it is still also looking at /results/erddap*/ dirs.
Discovered that ERDDAP will not present our model results on lat/lon grid because it is not rectilinear; also discovered that memory and file size limit in the app are easily exceeded by our datasets.
(MEOPAR)

Attended Phys Ocgy seminar by Noel Fitzpatrick about glacier surface energy balance measurement & modeling.


Tue 19-Jan-16
^^^^^^^^^^^^^

Gave Jackie a preliminary opinion on why I think that a Feb launch data is too ambitious.
(sealinkd)

Continued working on ERDDAP server setup; got nowcast 3d tracers and u-velocity datasets in place; requested another restart from Charles to better tune our setup.
Salish Sea team group meeting; see Google Drive whiteboard.
Participated in undergrad research fair w/ Elise.
(MEOPAR)

Wed 20-Jan-2016
^^^^^^^^^^^^^^^

Located for Susan the notebook in tools/bathymetry/ used to create the file containing the actual (partial step) bathymetry that NEMO uses for calculations.
(MEOPAR)


Confirmed that RandoPony uses smtp.webfaction.com for outbound email so it will be unaffected by their upcoming spam prevention port changes.
(RandoPony)

Sent another reminder email to UBC AP re: still unpaid 4-Nov-2015 invoice.
Fixed an issue in the hvsi module validation notebook re: ending row iteration for data reading at end of communities rows now that additional calculation rows have been added to the sheet.
Published a new version of the notebook based on the V2HVSIIndicatorData_Final.xlsx spreadsheet.
Created a notebook that uses Pandas to generate Excel worksheet renderings of matrices of HVSIs for all communities for a capital.
Worked on setting up Piwik analytics; devolved into a thrash about getting PHP files process by FastCGI but static files not being served.
(sealinkd)


Thu 21-Jan-2016
^^^^^^^^^^^^^^^

Downloaded missing HRDPS research forecast files for 16-19-Jan.
upload_forcing worker failed for nowcast+ run; no apparent reason; manual re-run got automation restarted.
Fixed the hard-coded date bug that Rich found in LTIM_fun.m and manually ran that script for the 3 nodes; seems to have gotten that ONC-ADCP data downloads back in operation.
Continued work on ERDDAP datasets with a notebook to start automating the editing of generated XML fragments.
(MEOPAR)

Finally got PHP vs. static files sorted out enough that Piwik runs as well as can be expected in Vagrant dev environment.
Helped Jacki try to figure out why her matrix spreadsheets differ from my example; perhaps Python 3 division.
(sealinkd)

Received proposed contract from Youyu.
(nemo-nowcast)

Attended Civl Engrg hydrology seminar by Christian Schoof about glacier base water flow.

Met w/ Susan & Elise re: screening of students we interviewed at research fair.


Fri 22-Jan-2016
^^^^^^^^^^^^^^^

Telus contractor visit to install fibre Internet connection.

Deployed Piwik for prod on EduCloud instance and added notes about the setup to deployment docs.
Helped Jackie get her Python 3 Anaconda environment set up so that she can generate HVSI matrix spreadsheet for the UBC SCARP team to work with.
(sealinkd)


Sat 23-Jan-2016
^^^^^^^^^^^^^^^

Created Bitbucket Resliient-C project and added sealinkd repo to it.
(sealinkd)

Tried to finalize storm surge paper citation in all the places but stalled out because it hasn't yet been assigned to an issue.
Created Bitbucket Publications project for SalishSea-MEOPAR team and added 4 paper repos to it.
Continued work on refactoring figures.py.
Created nc_tools.dataset_from_path() function to facilitate loading netCDF datasets from files given by pathlib objects; also RuntimeError to IOError for file not found.
Started work on wind_tools.calc_wind_avg_at_point() function with code that Susan had extracted from nowcast.worker.make_feeds module.


Sun 24-Jan-2016
^^^^^^^^^^^^^^^

Finished implementatio of wind_tools.calc_wind_avg_at_point() function.
Passed the figures.py patch to Susan to check the timing of the Campbell River max ssh on 10Jan16, and for her to continue refactoring.
(MEOPAR)

Set up 2016 deployment of SoG bloomcast system.
Had to add work-around for very 1st cloud fraction value being None and causing interpolation to fail.
(bloomcast)

Set up BIO client repo.
(43ravens)


Week 4
------

Mon 25-Jan-2016
^^^^^^^^^^^^^^^

Accepted contract from Youyu for Scotia Shelf nowcast system development.
(43ravens)

Set up SOG-projects work area on niko.
Fixed off-by-1 error in profile number for plots.
Added Smoke,Haze to cloud fraction mapping.
(bloomcast)

Wrote with Susan MEOPAR renewal proposal section re: code repo.
Continued work on ERDDAP datasets XML fragments generation automation notebook.
(MEOPAR)

Attended Phys Ocgy seminary by Romain Di Constanzo about measurement of the Fraser River plume via satellite imagery.


ToDo
====

* refactor, unit tests & docs for forcing links checking for NEMO-3.6
* update quick-start docs re: NEMO-3.6 - Elise???
* finish run_NEMO36 unit tests

* get HTTPS working for alternate sealinkd app domain names
* reduce resolution of landing page images for faster load times
* add docs re: sealinkd server-side app framework
* add EduCloud deployment docs
* implement user mgmt

* update storm surge paper refs w/ doi link - need issue details
* research_ferries module
* JSON logging use example notebook

* review remaining nosy PRs
