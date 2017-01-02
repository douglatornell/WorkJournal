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
Finished enough implementation of run_NEMO36 worker that it should be able to run nowcast-green on salish; figured out how to parameterize unit tests re: absolute paths in run description; lots of other unit tests need to be written.
(SalishSea)

Created 2016 journal file and did catch-up summary of holidays work to end 2015 journal.

Attended Phys Ocgy seminar by Susan on barotropic tides in the Salish Sea NEMO model.


Tue 5-Jan-2015
^^^^^^^^^^^^^^

Started work on operational nowcast talk for 11-Jan Phys Ocgy seminar.

Automated feed generation worked for forecast/04jan16 and forecast2/04jan15 runs.
Tested run_NEMO36 worker in collaborations with Susan to launch nowcast-green run.; not yet ready for integration w/ mgr.
Salish Sea team group meeting; see Google Drive whiteboard.
(SalishSea)


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
(SalishSea)

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
(SalishSea)


Sat 9-Jan-2016
^^^^^^^^^^^^^^

Nowcast critical error: make_plots worker failed at 04:13, but that was because the forecast2 run didn't produce results. That was due to 5 of the nodes having dropped their sshfs connections to the shared storage.
(SalishSea)

Finished implementation of map on Compare page that shows communities that are being compared; marker coordinates come from database, and marker on-click events load the community's Profile page.
Re-created prod database and loaded it from the 6Jan HVSI data spreadsheet.
Deployed Compare page map feature to production, after a minor thrash due to section names in production.ini; model scripts now need to be run with `production.ini#sealinkd`.
(sealinkd)


Sun 10-Jan-2016
^^^^^^^^^^^^^^^

Worked on tools repo docs; got nowcast model changes docs up to date.
Worked w/ Susan on refactoring nowcast.figures.website_thumbnail().
(SalishSea)


Week 2
------

Mon 11-Jan-2016
^^^^^^^^^^^^^^^

Tidied, stored & committed work on kudu in preparation for working at UBC for a few days.
Finished slides for operational nowcast talk and delivered it at the Phys Ocgy seminar.
Sorted out Jie's salishsea gather problem; circular import issue between run and api modules; my bad.
(SalishSea)


Tue 12-Jan-2016
^^^^^^^^^^^^^^^

Fixed bugs in make_feeds worker that showed up the 1st time that a feed entry was generated under automation.
Fixed circular import bug in SalishSeaCmd package by moving pbs_common() and td2hms() functions from run to api module.
Re-closed tools repo SalishSeaNowcat branch that Muriel accidentally re-opened a while ago.
Created mixing-paper and internal-tides-paper groups in team account on Bitbucket and changed access to the corresponding repos so that only those groups & admins have write access.
Started work on generating datasets.xml file for skookum ERDDAP server.
Salish Sea team group meeting; see Google Drive whiteboard.
(SalishSea)


Wed 13-Jan-2016
^^^^^^^^^^^^^^^

Attended Compute Canada SPARC2 consultation session; see notebook.

Pinged Youyu re: NEMO nowcast project and got a positive response.

Authorized Charles to buy 2x8Tb archive drives to enlarge backup on salish & skookum; salish storage will be reconfigured from 2x3Tb RAID 1 to 3x3Tb RAID 5.
Continued work on refactoring website_thumbnail() function in nowcast.figures.
Continued work on generating datasets.xml file for skookum ERDDAP server, and actually landed a test version of the CampbellRiver.nc dataset.
(SalishSea)

Worked on notebook to validate HVSI calcs module against Jackie's spreadsheet calcs; v1 doesn't agree :-(
(sealinkd)


Thu 14-Jan-2016
^^^^^^^^^^^^^^^

Prepared for and helped Elise lead workout session code review/refactoring of nowcast-green plotting notebook that Susan claims is slow.
(swc)

Continued work on generating datasets.xml file for skookum ERDDAP server, and landed the real nowcast PointAtkinson.nc dataset.
Attended dept colloquium by Julie Laroche from Dal re: T. oceania and iron limitation; mostly omics.
Discussed priorities
(SalishSea)


Fri 15-Jan-2015
^^^^^^^^^^^^^^^

Dentist appt.

Tweaked admin permissions for new paper repos.
Added ERDDAP as component in tools repo issue tracker.
Created tools repo issue #27 re: inconsistent time interval in tide gauge station ERDDAP results datasets.
Created tools repo issue #28 re: inclusion of run type in ERDDAP dataset ids.
Refined ERDDAP dataset setup docs, and discussed metadata w/ Susan.
(SalishSea)

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
(SalishSea)

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
(SalishSea)

Attended Phys Ocgy seminar by Noel Fitzpatrick about glacier surface energy balance measurement & modeling.


Tue 19-Jan-16
^^^^^^^^^^^^^

Gave Jackie a preliminary opinion on why I think that a Feb launch data is too ambitious.
(sealinkd)

Continued working on ERDDAP server setup; got nowcast 3d tracers and u-velocity datasets in place; requested another restart from Charles to better tune our setup.
Salish Sea team group meeting; see Google Drive whiteboard.
Participated in undergrad research fair w/ Elise.
(SalishSea)

Wed 20-Jan-2016
^^^^^^^^^^^^^^^

Located for Susan the notebook in tools/bathymetry/ used to create the file containing the actual (partial step) bathymetry that NEMO uses for calculations.
(SalishSea)


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
(SalishSea)

Finally got PHP vs. static files sorted out enough that Piwik runs as well as can be expected in Vagrant dev environment.
Helped Jacki try to figure out why her matrix spreadsheets differ from my example; perhaps Python 3 division.
(sealinkd)

Received proposed contract from Youyu.
(GOMSS)

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
(SalishSea)


Sun 24-Jan-2016
^^^^^^^^^^^^^^^

Finished implementatio of wind_tools.calc_wind_avg_at_point() function.
Passed the figures.py patch to Susan to check the timing of the Campbell River max ssh on 10Jan16, and for her to continue refactoring.
(SalishSea)

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
(SalishSea)

Attended Phys Ocgy seminary by Romain Di Constanzo about measurement of the Fraser River plume via satellite imagery.


Tue 26-Jan-2015
^^^^^^^^^^^^^^^

Preserved results of today's runs that used last year's SOG-code-bloomcast executable for Susan to compare to.
Updated SOG-code-bloomcast clone to rev c5d167d58046 and did a clean build.
Re-ran bloomcast and got apparently the same results.
(bloomcast)

Finished 1st draft of ERDDAP datasets automation notebook and used it to generate XML fragment for grid_W v1 dataset.
Salish Sea team group meeting; see Google Drive whiteboard.
(SalishSea)

Restarted buildbot slave on smelt.
(SOG)

Discussed plans for bash & editor workout on Thu w/ Cindy & Ben.
Researched Atom editor.
(swc)


Wed 27-Jan-2016
^^^^^^^^^^^^^^^

Installed Atom on kudu and confirmed its striking similarity to Sublime Text.
Prep for bash & editors customization workout.
(swc)

Pulled refactored figures.py into nowcast production; changes affect website_thumbnail & website_thresholds figures.
(SalishSea)

Loaded data from V2HVSIIndicatorData_Final.xlsx data spreadsheet into dev and production databases.
Wrote deployment docs re: setup of app database and loading data.
Reworked Profiles page skeleton to match latest mock-up from Jackie; skeletons for several tables, and implementation for HVSI Indicators tables.
(sealinkd)


Thu 28-Jan-2016
^^^^^^^^^^^^^^^

Continued Atom research.
Installed Atom on niko.
Finished :file:`public_html/swc/2016-01-28-bash-editors/BashEditorsCustomization-DJL.ipynb` notebook for workout.
Participated in workout session about bash & editor customization.
(swc)

Did some more polishing on the Profiles page HVSI tables.
(sealinkd)

Improved time zone rendering in figures.website_thumbnail() and added that function to the refactoring testing notebook.
Continued work on ERDDAP datasets automation notebook re: using it to generate tide gauge station datasets.
(SalishSea)


Fri 29-Jan-2016
^^^^^^^^^^^^^^^

Fiddled around with Atom; rst support sucks, no auto-complete in text grammar.

Pushed reworked Profiles page to production.
Renamed Indicator data model object units column to metric to be consistent with SCARP team terminology.
Started adding data columns for Profiles page to Community model and hooking them into the page; profile_description, contact_person, contact_email, contact_phone.
Added community profile photo to Profiles page via asset info from database; load_communities now loads asset information into the database when it is available in the spreadsheet.
Tried to start adding hazard exposure and mitigation activities data to app, but it is still too poorly defined.
Updated data model entity relationship diagram and linked it into the data model docs.
Started implementation of users data model and user management features.
(sealinkd)

Replied to latest /var fiesystem corruption report w/ offer of a site visit on 5-Feb; accepted.
(Nordion)


Sat 30-Jan-2016
^^^^^^^^^^^^^^^

Wrote status email re: Profiles page to Jackie.
Added indicator value tables below bar charts on Compare page.
Improved app banner styling & merged UBC & MEOPAR logos into single image for better flow.
Worked on sign-up and sign-in pages.
(sealinkd)


Sun 31-Jan-2016
^^^^^^^^^^^^^^^

Finished user sign-up processing.
Added sign-in authentication processing and page level security permissions.
(sealinkd)


February
========

Week 5
------

Mon 1-Feb-2016
^^^^^^^^^^^^^^

Moved SalishSeaNowcat/nowcast/notebooks/ to SalishSeaNowcat/notebooks/.
Moved SalishSeaNowcat/nowcast/tidal_predications/ to SalishSeaNowcat/tidal_predications/.
Closed dangling nowcast-obj branch in tools repo.
Continued work on generating ERDDAP dataset via notebook; success for hourly v1 of u, v, and w velocities, and tracers; v2 w not working.
Requested ERDDAP server reboot & re-config by Charles.
Set up /results/nowcast-sys/figures/ and requested Charles set up static server to serve it at https://salishsea.eos.ubc.ca/nowcast-sys/figures/.
Refactored Mercurial update of nowcast salishsea-site repo into separate worker.
Investigated alternative DAP servers, especially PyDAP.
(SalishSea)


Tue 2-Feb-2016
^^^^^^^^^^^^^^

Debugged why hg_update_site worker didn't run; I think it was because I had restarted nowcast_mgr in the wrong conda env.
Fixed bug in hg_update_site worker whereby a Path object was sent to the manager as a message payload; added unit tests that would have caught the bug if I had been stricter with myself.
Refactored make_feeds worker to use wind_tools.calc_wind_avg_at_point().
Started work on unit test for wind_tools.calc_wind_avg_at_point() and found possible off-by-1 bug.
(SalishSea)

Worked on contract details for Youyu; proposed alternate justification wording; completed ABACUS form; wrote contractor proposal; wrote draft of company profile.
(GOMSS)

Wrote draft of app dev progress report for Stephanie and Jackie.
(sealinkd)


Wed 3-Feb-2016
^^^^^^^^^^^^^^

Confirmed and fixed off-by-1 bug in wind_tools.calc_wind_avg_at_point() and added unit tests for it to give 100% coverage.
Charles restarted eddy and (after a minor issue with its Bitstream Vera Sans font getting blown away by a Java JRE update) it is now running from /results/erddap/ without 500 errors.
Wrote a post on the ERDDAP Google group re: generation of grid_W v2 dataset.
Got responses form Bob Simmons that point at using NCO to add variables to old results files when we add new variables (like w-eddy visocity & diffusivity) to model output; other options re: file regexs and results directory tree segmentation don't feel like they will scale.
(SalishSea)

Fixed location of profile time line and label in mixing layer depth & wind speed plot re: matplotlib.date.date2num() issue w/ arrow object.
(bloomcast)

Did final revision on company profile and sent documents to Youyu.
(GOMSS)

Added Piwik custom variables containing community name and role of authenticated users.
Add change password form.
(sealinkd)


Thu 4-Feb-2016
^^^^^^^^^^^^^^

Felt like crap; nagging headache thing of the past couple of days spread to my ear, throat and neck, then most of my joints.

Explored NCO re: creation of new, empty variables in old nowcast system results files so that ERDDAP will accept new variables into a dataset.
Spurred by a subsequent response from Bob Simmons, I tried just loading the Grid_W v2 dataset via a flag file instead of running DasDdl.sh first, and it worked!
Added surface tracer fields dataset.
Explored PyDAP package; useful, but Python 3 port not yet released.
(SalishSea)


Fri 5-Feb-2016
^^^^^^^^^^^^^^

Nordion site visit re: isoinfo server boot failure; RAID degraded by 1 drive but suspected controller or cabling issue; see work notes.
(nordion)

Investigated Nancy's contourf images AttributeError: 'QuadContourSet' object has no attribute 'set_animated' issue;
Added ping_erddap worker to nowcast system.
Continued working on xfail tests for run_NEMO36 worker.
(SalishSea)


Sat 6-Feb-2016
^^^^^^^^^^^^^^

Fixed bug in ping_erddap re: handling run types w/ no datasetIDs.
Started refactoring make_site_page worker and page templates to use static figures server, and to add titles and link anchors to figure images.
(SalishSea)


Sun 7-Feb-2016
^^^^^^^^^^^^^^

Finished refactoring make_site_page worker and page templates to use static figures server, and to add titles and link anchors to figure images.
Changed run_NEMO36 worker to get run timestep from the previous run's namelist_cfg instead of from the default namelist.domain file.
Hard-linked results figures on skookum from /results/SalishSea/*cast/*/figures/ to /results/nowcast-sys/figures/*cast/*/.
Started rebuilding all past publish & research pages to use statically served figures.
(SalishSea)


Week 6
------

Mon 8-Feb-2016
^^^^^^^^^^^^^^

**Satuatory Holiday** - BC Family Day

Debugged intro of static image pages into production; sphinx build time reduced from 19:45 to 01:39, and rsync time reduced from 00:20 to 00:05.
Refactored make_site_page worker to use NowcastWorker.
Fixed bug in make_plots worker re: FileExistsError on attempt to link a file created by an earlier run of the worker (nowcast research).
(SalishSea)


Tue 9-Feb-2016
^^^^^^^^^^^^^^

Researched xarray package - Pandas for geoscience data; e.g. 4d NEMO results.
Confirmed that netCDF4 conda package included the ability to open datasets via OPeNDAP.
Tracked down log messages associated with sporadic null pointer errors.
Continued rebuilding nowcast system results pages to use figures from static server.
Salish Sea team group meeting; see Google Drive whiteboard.
(SalishSea)

Restarted build slaves on smelt and sable.
(SOG)

Met w/ Tom Yerex (new EOAS IT mgr).

Attended Phys Ocgy seminar by Nancy re: mixing & prep for McGill.


Wed 10-Feb-2016
^^^^^^^^^^^^^^^

Fixed title for run duration average winds figure on nowcast publish pages.
Fix orphan file Sphinx warning from README in nowcast ATOM feeds directory.
Ran update_copyright script over repos; tools, analysis, salishsea-site, SS-run-sets.
(SalishSea)

Reviewed and updated status report.
Implemented app admin auth principal and added user management item to user menu for users with that authorization.
Added users list page, and edit user form.
(sealinkd)


Thu 11-Feb-2016
^^^^^^^^^^^^^^^

Finalized and sent status report to Stephanie and Jackie.
(sealinkd)

Prep for continuation of editors session.
Participated in workout session about bash & editor customization.
(swc)

Youyu says project is a go.
Got credentials for Dal cluster account.
Installed a newly generated ssh key on Dal cluster login node.
(GOMSS)

Started planning poster for OSM.
(osm)

nowcast research plots failed due to DNS error, then malformed data from ONC VENUS nodes; re-ran worker with those figures commented out
Continued rebuilding nowcast system results pages to use figures from static server.
(SalishSea)

Fri 12-Feb-2016
^^^^^^^^^^^^^^^

Propagated newly generated ssh key to nemo nodes.
Got Mercurial installed on nemo nodes; installed miniconda3.
(GOMSS)

nowcast research plots failed due to malformed data from ONC VENUS nodes; re-ran worker with those figures commented out
Finished rebuilding nowcast system results pages to use figures from static server.
Created ticket 15399 re: proxying ERDDAP to salishsea.eos.ubc.ca/erddap/.
Created ticket 15400 re: installation of SSL/TLS certs & auto-redirection to make salishsea.eos.ubc.ca HTTPS only.
(SalishSea)

Worked on nowcast system poster for OSM.
(osm)


Sat 13-Feb-2016
^^^^^^^^^^^^^^^

Deleted _static/nemo/results_figures/ tree on shelob, freeing 14 Gb of storage.
(SalishSea)


Sun 14-Feb-2016
^^^^^^^^^^^^^^^

Worked on nowcast system poster for OSM.
Emailed Youyu & Dany w/ idea for CMOS talk re: MERCAD.
(SalishSea)


Week 7
------

Mon 15-Feb-2016
^^^^^^^^^^^^^^^

Worked on nowcast system poster for OSM.
Participated in Phys Ocgy seminar where Elise practiced her talk and some of the rest of us previewed our posters.
Explored xarray package (pandas concept for N-dimensional data, especially climate & ocean model results).
Created NEMO-forcing repo ticket #4 re: missing FillValue & least_significant_digit attributes in SalishSea2_NEMO_bathy.nc file.
Worked with Charles on the transition to HTTPS for salishsea.eos.ubc.ca.
Got favourable responses from both Youyu and Dany re: CMOS talk about MERCAD.
(SalishSea)


Tue 16-Feb-2016
^^^^^^^^^^^^^^^

Created project-specific work journal for GOMSS nowcast system project/contract; that project will no longer be tracked in detail here.
(nemo-nowcast)

Prep for mtg w/ Jackie; updated sealinkd/vagrant dev environment on niko; scrubbed and re-built database.
Mtg w/ Jackie re: filters data and design, and data for community profiles page.
(sealinkd)

Salish Sea team group meeting; see Google Drive whiteboard.
(SalishSea)


Wed 17-Feb-2016
^^^^^^^^^^^^^^^

Telcon w/ Youyu; see GOMSS work journal.
(GOMSS)

Replied to Stephanie's email re: tracking Resilient-C app users.
(sealinkd)


Thu 18-Deb-2016
^^^^^^^^^^^^^^^

Finished OSM poster.
(SalishSea)

Created UptimeRobot account and setup up monitoring for Resilient-C and RandoPony apps, and salishsea site.


Fri 19-Feb-2016
^^^^^^^^^^^^^^^

Traveled to New Orleans for OSM 2016.


Sat 20-Feb-2016
^^^^^^^^^^^^^^^

Added copyright year range to nowcast feed generator.
Work on integrating run_NEMO36 worker for nowcast-green into automation framework.
(SalishSea)

Sightseeing in New Orleans; French Quarter and River walk


Sun 21-Feb-2016
^^^^^^^^^^^^^^^

Finished integrating run_NEMO36 worker for nowcast-green into automation but can't test it because 20feb16 run timed out, so we are running a day behind; was able to launch run via ssh from skookum as manager process would do.
(SalishSea)

Sightseeing in New Orleans; Garden District and Lafayette No. 1 cemetary

OSM opening, keynote, and mixer reception
(OSM)


Week 8
------

Mon 22-Feb-2016
^^^^^^^^^^^^^^^

Operational Ocgy and Ocean modeling sessions; my Salish Sea Nowcast system poster.
(OSM)


Tue 23-Feb-2016
^^^^^^^^^^^^^^^

Excellent Susan Lozier plenary about MOC variability.
A few bio-physical modeling presentations.
(OSM)

Worked on porting watch_NEMO worker to NowcastWorker basis and enabling it to work in the shared storage context used for the nowcast-green runs on salish.
(SalishSea)

Big storm blew through New Orleans.
Dinner w/ Zack & Mimi at Herbsaint.


Wed 24-Feb-2016
^^^^^^^^^^^^^^^

Amy Waterhouse's talk on internal tide beam in the Tasman Sea.
Awards lectures
Tutorials on ensemble data assimilation, Unidata DMRC curated data mgmt tools portal, and R for ocgy.
Mimi Koehl's talk on swimming in turbulence.
(OSM)

Continued work on watch_NEMO worker.
(SalishSea)

Dinner w/ Rich, Nicole, Paul, Sophie & Caroline at Murate's.


Thu 25-Feb-2016
^^^^^^^^^^^^^^^

Fixed leap-year handling bug in residuals._to_datetime() re: conversion of Neah Bay ssh scraped data dates to datetime objects; strptime() assumes non-leap-year unless date string includes the year.
Continued work on watch_NEMO worker.
Fixed bug in NowcastWorker that was preventing run_NEMO36 worker on salish from communicating with manager on skookum.
forecast run was killed by a network switch failure on west.cloud; re-ran.
(SalishSea)

Nick Bond's talk on the NE Pacific blob.
Plenaries
Tutorials on turbulence.
Elise's talk on modeling primary production controls in the SoG.
(OSM)

Dinner at Cochon w/ Ben, Nancy & Elise.


Fri 26-Feb-2016
^^^^^^^^^^^^^^^

David Smeed's talk about AMOC measurements at 26°N
Ivo Pasmans' talk about data assimilation in the OSU OR/WA coast ops model.
More data assimilation talks.
(OSM)

Finished NowcastWorker implementation of watch_NEMO worker w/ salish runs & NEMO-3.6 capabilities.
(SalishSea)


Sat 27-Feb-2016
^^^^^^^^^^^^^^^

Started work on nowcast data comparison page automation.
(SalishSea)


March
=====

Week 9
------

Mon 29-Feb-2016
^^^^^^^^^^^^^^^

Submitted CMOS abstract re: MERCAD framework.

Finished initial implementation of nowcast data comparison page automation.
Refatored run_NEMO36 unit tests to eliminate remaining xfails.
(SalishSea)

Traveled home from New Orleans after OSM 2016.


Tue 1-Mar-2016
^^^^^^^^^^^^^^

Tested and fixed bugs in new watch_NEMO worker and got it running for nowcast-green via manual launch; hoping that automation will work tomorrow.
Tested make_plots and make_site_page workers comparison option via manual launch; hoping that it will work via automation tomorrow after manager restart.
Buffed work env docs re: Jupyter Notebook & nbviewer URLS.
Worked on notebook re: exploring netCDF datasets from ERDDAP servers.
Restarted nowcast mgr after nowcast-green run finished to enable automation for nowcast-green watch_NEMO and comparison plots and page.
(SalishSea)


Wed 2-Mar-2016
^^^^^^^^^^^^^^

Worked on work plan for project.
(GOMSS)

Fixed watch_NEMO worker PID cal bug that prevented nowcast-green watcher from starting, and manually started watcher.
Investigated Ben's report of trouble reading ONC central node ADCP dataset on Monday; couldn't reproduce the issue; concluded that it was other a transient glitch that was fixed by Tuesday's cron script run, or that he was unluckily reading the dataset while it was being written by the cron job.
Investigated why nowcast 01mar16 comparison page was not built; _after_make_plots function was launching make_site_page worker with present day's date instead of previous day's; fixed.
Tried to add lon & lat as variables to ubcSSn3DTracerFields1hV1 dataset but ERDDAP is acting up because the Bitdstream Vera Sans font has gone MIA again; created ticket for Charles.
Fixed fill value and precision in ubcSSnBathymetry2V1 dataset re: NEMO-forcing issue #4.
(SalishSea)

Did no-Flash speed tests at TestMy.com and concluded that kudu is faster on a wired connection than on wifi.


Thu 3-Mar-2016
^^^^^^^^^^^^^^

nowcast-green and its watcher launched without manual intervention, though logging from watcher is messed up (I think due to buffer).
Including lon/lat at variables in 3d field erddap datasets doesn't work.
Added valid_range attributed to ubcSSnBathymetry2V1 dataset.
Explored erddap dataset access via xarray and found that it solves the time slicing issue very neatly.
Finished notebook re: exploring netCDF datasets from ERDDAP servers.
Worked on bringing ferry track salinity plots into comparison page.
Attended dept coloquium by Paul Snellgrove about biodiveristy - SCOR west speaker.
(SalishSea)


Fri 4-Mar-2016
^^^^^^^^^^^^^^

Confirmed w/ Dominik@EC that we can handle compression and directory change for GEM2.5 research model results effective 8-Mar.
Prep for salishsea site move from shelob to skookum and HTTPS:
* changed paths in nowcast.yaml
* changed make_plots worker to copy figure files instead of hard-linking them
* changed URL to use HTTPS
Continued work on bringing ferry track salinity plots into comparison page; completed TW-DP figure.
Met w/ Ben to teach him about ERDDAP server.
Met w/ Charles to finalize salishsea site move from shelob to skookum and HTTPS.
(SalishSea)

Changed publication server path from shelob to skookum and set up ssh key in preparation for salishsea site move.
(bloomcast)

Investigate Englishman River failure in ECget (also affected bloomcast); no data on site after 23:50 on 2-Mar.
(ecget)


Sat 5-Mar-2016
^^^^^^^^^^^^^^

Removed rsync -t option from push_to_web worker because we can't update time stamps due to permissions in /var/www/html/ tree.
Also changed path to exclude host prefix because we can rsync directly to /var/www/html/; realized that we could sphinx-build to there directly.
(SalishSea)


Sun 6-Mar-2016
^^^^^^^^^^^^^^

Removed rsync -t option from push_to_web function because we can't update time stamps due to permissions in /var/www/html/ tree.
(bloomcast)

Checked on wateroffice Englishman river data; an hour or two's worth appeared for yesterday.
(ecget)

Figured out how to configure reverse proxy for ERDDAP and added notes to ticket 15400 for Charles; unfortunately, the config, when applied, does not work properly.
Investigated EC license and redistribution terms for HDRPS model products and concluded that we are clear to distribute our ops dataset on ERDDAP.
Started work on adding atmospheric forcing datasets to ERDDAP
(SalishSea)


Week 10
-------

Mon 7-Mar-2016
^^^^^^^^^^^^^^

Shut down Google Cloud Platform nowcast account.

Renewed Compute Canada account.

Changed baseURL setting in ERDDAP setup.xml file to resolve the remaining issue with the reverse proxy to SSL setup.
Modified ERDDAP setup.xml to change as much as possible of page template from NOAA to UBC Salish Sea NEMO identity.
Added HRDPS atmospheric forcing grid dataset to ERDDAP.
(SalishSea)

Implemented user password reseet feature.
(sealinkd)


Tue 8-Mar-2016
^^^^^^^^^^^^^^

Slow start to the morning because I think I'm coming down with a version of Susan's virus.

Finished dev docs for SalishSeaCmd package.
Refactored SalishSeaTools packaging, and wrote dev docs.
Team meeting - see whiteboard.
Discussed summer co-op student interviews w/ Susan and Elise.
(SalishSea)


Wed 9-Mar-2016
^^^^^^^^^^^^^^


Started work on integrating Elise's river run-off tracer climatology into nowcast-green.
Checked on PMV storm surge alerts feed and found that I needed to update the URL to HTTPS in feedly; sent email about that to Cindy@PMV.
(SalishSea)

Updated production deployment to enable user management system and bootstrapped myself with the app admin role.
Changed banner to use logo & tagline image that Jackie provided.
Added favicon from logo image that Jackie provided.
Uppercased and left justified HVSI indicator table headings on Profiles page per Jackie's request in 16-Feb mtg.
Changed indicator metric display on Profiles and Compare pages to use | character as line break indicator; reloaded inidicators data from 19Feb spreadsheet in both dev and production to get |-separated metrics data into databases.
Updated layout of Profiles page Hazard-at-a-Glance and Hazard Exposure tables per Jackie's request in 16-Feb mtg.
Reloaded communities data from 19Feb spreadsheet in both dev and production to get community descriptions into databases.
Started adding data for Profiles page Hazard-at-a-Glance table to community data model.
(sealinkd)


kudu crashed hard (spontaneous power off) at about 13:45

I crashed mid-afternoon with headache and increasingly productive cough.


Thu 10-Mar-2016
^^^^^^^^^^^^^^^

Stayed home due to productive cough and headache.

Patched around failing NOAA water levels data download to get make_plots forecast publish to stop failing; re-ran worker for 9Feb forecast and forecast2 runs.
Added nowcast Campbell River sea surface height dataset to ERDDAP.
Added ops atmospheric forcing dataset to ERDDAP; including download_weather option to ping_erddap worker so that dataset gets updated after grib_to_netcdf worker finishes nowcast+ work.
(SalishSea)

Finished adding data for Profiles page Hazard-at-a-Glance table to community data model; loaded data from spreadsheet into both dev and productions databases.
Created app admin user sign-in for Jackie because she was stuck in a state due to having been signed in with fake credentials when I enabled user management.
(sealinkd)


Fri 11-Mar-2016
^^^^^^^^^^^^^^^

Still suffering with cough, headache, and, new for today, sinus congestion.

Reviewed and commented on Elise's NEMO-3.6 on orcinus quick start docs, and their punting of the 3.4 version.
Brought rivers run-off climatology and open boundary conditions for green ocean model into nowcast system.
Added nowcast Cherry Point sea surface height to ERDDAP.
(SalishSea)

Created issue #50 typography of table headings on Profiles page.
(sealinkd)

Participated w/ Susan & Elise in summer student RA interview.

Experimented with Wingware and was under-impressed.


Sat 12-Mar-2016
^^^^^^^^^^^^^^^

Still coughing and snotting.

Experimented with PyCharm and found it much more to my liking than Wingware.

Started work on sphinx_build worker to replace push_to_web worker.
Fixed worker failure log messages to that they are all at the critical level and will therefore generate email notifications.
Changed storm surge alerts ATOM feed entries to use storm-surge/forecast.html page instead of (incorrect) dated publish pages.
Added nowcast Friday Harbor sea surface height to ERDDAP.
(SalishSea)


Sun 13-Mar-2016
^^^^^^^^^^^^^^^

Still coughing and snotting.

Continued experimented with PyCharm.

Added nowcast Nanaimo sea surface height to ERDDAP.
(SalishSea)


Week 11
-------

Mon 14-Mar-2016
^^^^^^^^^^^^^^^

make_runoff_files worker failed because ECget produced duplicated 12mar Fraser River flow instead of 13mar; re-ran ECget, make_runoff_files, and upload_forcing to start forecast2 run ~4h late
Noted that weather downloaded are back to taking >1h, so our runs are starting >1h later than last week - thank you DST.
Added nowcast Neah Bay & Victori asea surface heights to ERDDAP.
Emailed Diego about getting nowcast results from ERDDAP on to OceanViewer; and he produced a preliminary demo in a few hours!
Participated in Phys Ocgy seminar discussion of February conferences.
Worked on NEMO quick-start and Python/netCDF intro docs.
(SalishSea)

Submitted expense claim for CMOS abstract.

Set up PyCharm on niko.


Tue 15-Mar-2016
^^^^^^^^^^^^^^^

Investigated salishsea.eos.ubc.ca SSL issues reported by Nancy in Firefox on tyee, and Diego in Python 2.7.10 PyDAP & urllib2; concluded that it is an incomplete certificate chain issue in the configuration of apache on skookum, and opened ticket 15506.
Added nowcast Sand Heads sea surface heights to ERDDAP.
Salish Sea team mtg; see whiteboard.
Added source encoding indicator comment to unit_conversions module so that Jie can used it with some Python 2.7 code that Rob wrote.
Started work on handling missing ferry data in comparison plots.
The 00 weather downloaded failed, but I didn't investigate.
(SalishSea)

Participated w/ Susan & Elise in summer student RA interviews.


Wed 16-Mar-2016
^^^^^^^^^^^^^^^

Discovered that the /results filesystem on skookum was full, in large part, due to nowcast-green result files not being LZ compressed; realized that that was due to a bug in salishsea-cmd.combine whereby no NEMO-3.6 run results (other than restart files) are being compressed.
Got thing back on the rails by moving and starting LZ compression on results, and manually running 00 and 06 weather download workers, and make_runoff_file worker; forecast2/15mar16 skipped, and nowcast-green in is catch-up.
Emailed Dominik re: rotation of GEM2.5 winds to north-south grid, saying that we prefer him to do the rotation, and asking for the transformation so that we can back-apply it as necessary.
(SalishSea)

Replaced brake blocks on Red and prepped spkokes for Emma's new rear wheel.

Set up SealinkD project in PyCharm.
Updated app logo in banner with new version from Tugce.
Changed more Profiles page column headings to uppercase per Jackie's request.
Started adding data for Profiles page Flood Planning Data Availability table to community data model.
(sealinkd)


Thu 17-Mar-2016
^^^^^^^^^^^^^^^

Continued adding data for Profiles page Flood Planning Data Availability table to community data model.
Emailed w/ Jackie to try to debug inability of SCARP team users to create sign-ups.
(sealinkd)

Worked on handling no observations data issues in research_ferries figures.
Fixed bug in SalishSeaCmd combine where by results from NEMO-3.6 runs w/ 1 XIOS processor are not LZ-compressed.
(SalishSea)

Met w/ Chris Edwards of UC Santa Cruz and discussed quasi-real-time models automation.

Attended dept colloquium by Chris Edwards.


Fri 18-Mar-2016
^^^^^^^^^^^^^^^

Nordion site visit re: isoinfo server boot failure; replaced failed drive in RAID array and left it rebuilding; see work notes and expected follow-up visit next week.
(Nordion)

Jackie told me that she and other SCARP team members did sign-ups with community name Other selected; turns out I had not implemented handling for that; see issue #51.
Jackie requested addition of UBC Research Team community and role; see issue #52; implemented and pushed to production.
(sealinkd)


Sat 19-Mar-2016
^^^^^^^^^^^^^^^

Snowshoeing at Callahan.


Sun 20-Mar-2016
^^^^^^^^^^^^^^^

Set up randopony project in PyCharm.
Changed development environment files & docs to use conda.
Started refactoring populaire tests to pytest and adding Unicode handling for rider names.
(RandoPony)


Week 12
-------

Mon 21-Mar-2016
^^^^^^^^^^^^^^^

Continued refactoring populaire tests to pytest and adding Unicode handling for rider names.
(RandoPony)

Nancy reported bug in SalishSeaCmd API due to removal of name_roots arg from _netcdf4_deflate_results() function; fixed.
Updated EC GEM2.5 research forecast download cron scripts to handle gzip compressed files from EC.
(SalishSea)

Attended Phys Ocgy seminar by Jenna about tracking water masses via Nd in sediment cores.

Tried to help Karina w/ hg SSL issue, and gvfs firefox issue.


Tue 22-Mar-2016
^^^^^^^^^^^^^^^

Continued catch-up on nowcast-green run results compression, and GEM2.5 research forecast downloads.
Replied to Elise's email re: anonymous branch management in the NEMO-3.6-code repo.
Worked on research_ferries figures; Jupytper notebook in PyCharm is too buggy/laggy to use in that application.
Confirmed that make_site_page bug fix to prevent calendar truncation and missing forecast row works.
Salish Sea team meeting - see whiteboard.
Worked with Charles to resolve the SSL intermediate certs issue (and other vulnerabilities) on salishsea.eos.ubc.ca; emailed Diego to let him know that urlopen() should now work properly, and that current vectors needs to be rotated.
Added Horseshoe Bay-Departure Bay and Tsawwassen-Schwartz Bay ferry route figures to nowcast model vs. observations comparison page.
Discussed ferry salinity comparison figures w/ Susan; agreed to attempt another refactoring of the module, and the nowcast site figures architecture in general.
(SalishSea)

Email re: 18-Mar visit, plan for 23-Mar visit, IBM xSeries server research, and reiteration of proposal for off-site hosted Minerva.
(Nordion)

Attended CMOS annual lecture by Ron Stewart of U Manitoba about hazardous precipitation near 0°C.


Wed 23-Mar-206
^^^^^^^^^^^^^^

Nordion site visit re: isoinfo server boot failure; RAID array rebuild succeeded and server rebooted successfully; see work notes.
(Nordion)

Updated PyCharm on kudu to new 2016.1 release.

Added data for Profiles page Hazard Exposure table to community data model, and reworked the table to include a metric column so that the data integers make sense.
Started development of RiskReductionAction data model to hold data to populate Profiles page Activities table (and maybe Actions filter?).
(sealinkd)

Attended Python meetup hosted by ContinuumIO; Spiro Sideris talked about pdb, Casey Clements talked about Anaconda, JupyterLab & Dask, Brett Canon talked about async/await.


Thu 24-Mar-2016
^^^^^^^^^^^^^^^

Upgraded to PyCharm 2016.1 on niko.

Continued work on ferry salinity comparison figures.
Created refactor-nowcast-figures branch in tools repo; discussed refactoring ideas w/ Susan and Ben.
Fixed bug in file names for ferry route salinity comparison plots.
Enabled building of docs for refactor-nowcast-figures on readthe docs.
(SalishSea)

Participated in software workout about datetimes lead by Ben.


Fri 25-Mar-2016
^^^^^^^^^^^^^^^

Good Friday

Continued development of RiskReductionAction data model.
(sealinkd)


Sat 26-Mar-2015
^^^^^^^^^^^^^^^

Finished development of RiskReductionAction data model and implementation of its data into the Profiles page Activities table.
That completes Stage 2 of the Sea-link'D app contract!!!
(sealinkd)


Sun 27-Mar-2015
^^^^^^^^^^^^^^^

Easter

Removed nowcast index page surface salinity row.
Moved PyCharm .idea dir for tools repo on kudu into dotfiles repo and symlinked it into tools clone.
Discussed nowcast figures architecture ideas in refactor-nowcast-figures branch with Susan and continued developing them by prototyping a salinity_ferry_track module to refactor research_ferries.
(SalishSea)


Week 13
-------

Mon 28-Mar-2016
^^^^^^^^^^^^^^^

Easter Monday

Wrote docs about Mercurial named branches.
Developed and tested plan for splitting analysis repo.
(SalishSea)

Tue 29-Mar-2016
^^^^^^^^^^^^^^^

Wrote nowcast figures architecture docs.
Wrote library code docs.
Salish Sea team mtg; see whiteboard.
(SalishSea)


Wed 30-Mar-2016
^^^^^^^^^^^^^^^

Did dist-upgrade on sealinkd-vm to apply security updates, etc.
Deleted test Tom Dickson user from production instance.
Set up automatic redirect from HTTP to HTTPS on resilient-c.ubc.ca.
Set up nginx configs for 3 domains to all use SSL via SNI; set up automatic HTTP-> HTTPS redirection on all 3 domains.
Added deployment docs re: nginx setup.
Tweaked Profiles page Flood Planning data table layout per Jackie's request.
Loaded updated version of Profiles page Activities table data from Jackie.
Started development of hazard exposure filter for Maps and Analysis pages.
(sealinkd)

Email discussion w/ Nancy about a new thalweg section viz function.
Reviewed Ben's new salishsea_tools.data_tools module.
(SalishSea)


Thu 31-Mar-2016
^^^^^^^^^^^^^^^

Added Sphinx autodoc section to library code docs.
Worked on analysis repo split; completed analysis-jie, analysis-elise, and analysis-ben splits.
Started work on nowcast.figures.publish.storm_surge_alerts module from figures.plot_threshold_website().
(SalishSea)

EOAS Poster Corral


Fri 1-Apr-2016
^^^^^^^^^^^^^^

Participated in annual-ish GEOTRACES research mtg w/ groups from UofA and UVic.
(GEOTRACES)

Continued work on nowcast.figures.publish.storm_surge_alerts module from figures.plot_threshold_website().
Mostly refactored nowcast.figures.plot_map & dependencies into nowcast.figures.shared module.
(SalishSea)


Sat 2-Apr-2016
^^^^^^^^^^^^^^

Spent the day at Langara College first in a session about the continuing studies photography program, and later in a DLSR seminar lead by Kurt Stewart, a Basic Digital instructor in the program.


Sun 3-Apr-2016
^^^^^^^^^^^^^^

Continued refactoring populaire unit tests.
(RandoPony)


April
=====

Week 14
-------

Mon 4-Apr-2016
^^^^^^^^^^^^^^

Sent reminder re: invoice for 18 and 23 Mar site visits; got paid almost immediately.
(Nordion)

Finished refactoring nowcast.figures.plot_map & dependencies into nowcast.figures.shared module.
Continued work on nowcast.figures.publish.storm_surge_alerts module from figures.plot_threshold_website().
Reviewed Nancy's new salishsea_tools.visualizations module that holds contour_thalweg().
Moved nowcast.figures.get_tides() into nowcast.figures.shared module.
(SalishSea)

Attended Phys Ocgy seminar by Hakase Hayashida of UVic GEOTRACES about arctic ice algae biogeochemistry model.


Tue 5-Apr-2016
^^^^^^^^^^^^^^

Reviewed and commented on Susan's piece of the 2016 State of the Pacific Ocean report.
(bloomcast)

Continued work on nowcast.figures.publish.storm_surge_alerts module from figures.plot_threshold_website().
Salish Sea team mtg; see Google whiteboard; discussed creation of salishsea_tools.geo_tools module.
(SalishSea)

Voted in favour of 6 month release schedule and suggested Ubuntu-like, date-based release identifiers.
(SWC)

Met w/ Tamsin Lyle & Samaneh ?? of Ebbwater re: using Salish Sea NEMO model results as part of sea level rise plus storm surge visualization for Sechelt.

Attended GEOTRACES mtg.

Updated niko to PyCharm 2016.1.1.


Wed 6-Apr-2016
^^^^^^^^^^^^^^

Feeling achy and discombobulated.

Updated kudu to PyCharm 2016.1.1.

Moved SealinkD repo .idea/ directory into dotfiles repo.
Wrote end of stage 2 status report and created invoice.
Developed design and implementation of hazards & actions filters to the extent of a demo of the flooding filter on the Maps page.
(sealinkd)


Thu 7-Apr-2016
^^^^^^^^^^^^^^

Created client repo for UBC-SCARP.
(43ravens)

Email from Dominik@EC confirming that today is the first day for which the GEM2.5 research forecast winds are rotated to zonal/meridional.
Continued work on nowcast.figures.publish.storm_surge_alerts module from figures.plot_threshold_website().
(SalishSea)

Helped Karina w/ ariane installation issued on coho??
(canyons)

Sent status report and stage 2 invice to Stephanie, Jackie & Penny.
(sealinkd)

Participated in workout led by Elise about sqlalchemy.
(swc)


Fri 8-Apr-2016
^^^^^^^^^^^^^^

Travel to Barrie to visit parents

Continued work on nowcast.figures.publish.storm_surge_alerts module from figures.plot_threshold_website().
(SalishSea)


Sat 9-Apr-2016
^^^^^^^^^^^^^^

Attended memorial gathering in Stayner for Bernard Chalmers.


Sun 10-Apr-2016
^^^^^^^^^^^^^^^

Visiting parents in Barrie


Week 15
-------

Mon 11-Apr-2016
^^^^^^^^^^^^^^^

Visiting parents in Barrie; met Maria, their accountant.

Continued work on nowcast.figures.publish.storm_surge_alerts module from figures.plot_threshold_website().
(SalishSea)


Tue 12-Apr-2016
^^^^^^^^^^^^^^^

Visiting parents in Barrie.

Continued work on nowcast.figures.publish.storm_surge_alerts module from figures.plot_threshold_website().
(SalishSea)


Wed 13-Apr-2016
^^^^^^^^^^^^^^^

Travel home from Barrie.


Thu 14-Apr-2016
^^^^^^^^^^^^^^^

Brought dev env up to date on niko.
Set up PyCharm to run app from Vagrant VM in hopes of enabling debugging in PyCharm on both niko and kudu; still some wrinkles to sort out.
(sealinkd)

Successfully tested nbsphinx extension that allows Jupyter notebooks to be incorporated into Sphinx docs.
Changed readthedocs config for tools repo to use conda environment so that mocks in conf.py are no longer required.
Changed tools and docs repos on Bitbucket to use webhooks instead of service hooks to send signals to readthedocs.org.
Added docs and a demo notebook re: using xarray.
(SalishSea)


Fri 15-Apr-2016
^^^^^^^^^^^^^^^

Did more exploration of remote debugging of Vagrant apps in PyCharm; got the flask example to work, and made progress on sealinkd, but frames are still not visible and breakpoints are ignored.

Added section re: public & private object names to library code docs.
Changed handling of storm surge alerts thumbnail image so that it is provided by the figures server instead of coming from the site _static/ directory.
Updated salishsea-site rsync deployment target re: move of server to skookum.
Finished sphinx_build worker to replace sphinx build section of push_to_web worker.
Started work on rsync_to_web worker to complete refactoring of push_to_web worker into 3 NowcastWorker-based workers.
(SalishSea)


Sat 16-Apr-2016
^^^^^^^^^^^^^^^

Finished rsync_to_web worker.
Replaced push_to_web worker with sphinx_build and rsync_to_web workers.
Dealt with loss of sshfs connection on west.cloud node 13; no forecast2/15apr16 run.
(SalishSea)


Sun 17-Apr-2016
^^^^^^^^^^^^^^^

Deployed sphinx_build and push_to_web workers and dealt with the inevitable bugs; also recovered from failed make_plots worker runs yesterday, and fixed a bug whereby make_plots worker would overwrite the storm surge alerts thumbnail with an incorrect one when the worker is run on a date other than the one of the present forecast run's.
(SalishSea)


Week 16
-------

Mon 18-Apr-2016
^^^^^^^^^^^^^^^

Added earthquake to hazards exposure filter on Maps page; need to confirm how Jackie wants criteria from different hazards combined: or or and?
(sealinkd)

Fixed bug that caused nowcast results index page to exclude right-most date after nowcast comparison page build.
Helped Elise get ready to use salishsea command processor on orcinus.
Buffed docs in anticipation of James starting on 2-May.
(SalishSea)

Attended Phys Ocgy seminar re: magnetic fields on Mars.

Bought PyCharm annual license.


Tue 19-Apr-2016
^^^^^^^^^^^^^^^

Worked w/ Susan on metadata for SalishSea2 bathymetry mesk mash dataset for ERDDAP.
Planned Friday IOS ERDDAP workshop w/ Susan.
Checked status of OceanViewer and it appears to be picking up our daily nowcast results in its test instance (but not in production), and the currents have not yet been rotated.
Started development of a notebook to explore a nowcast sea surface temperature and associated atmospheric forcing via ERDDAP and xarray; for IOS workshop on Friday and our analysis_tools notebooks collection.
Salish Sea team meeting; see whiteboard.
(SalishSea)

Met w/ Jackie to discuss preliminary design & implementation of hazards and actions filters, and her plans for beta testing the app.
(sealinkd)

Party to celebrate Julia Gustanson's successful PhD defense.


Wed 20-Apr-2016
^^^^^^^^^^^^^^^

Researched current state of github.io pages for tomorrow's workout.
(swc)

Finished adding metadata to SalishSea2 mesh mask file in preparation for creation of ERDDAP datasets.
Added ubcSSn2DMeshMask2V1 and ubcSSn3DMeshMask2V1 datasets to ERDDAP.
Continued development of a notebook to explore a nowcast sea surface temperature and associated atmospheric forcing via ERDDAP and xarray; for IOS workshop on Friday and our analysis_tools notebooks collection.
(SalishSea)


Thu 21-Apr-2016
^^^^^^^^^^^^^^^

Prep for and delivered workout about GitHub Pages.
(swc)

Continued development of a notebook to explore a nowcast sea surface temperature and associated atmospheric forcing via ERDDAP and xarray; for IOS workshop on Friday and our analysis_tools notebooks collection.
Created no-web version of above notebook and downloaded dataset slabs to niko in anticipation of having limited network access at IOS.
(SalishSea)

Traveled to Sydney for IOS workshop.


Fri 22-Apr-2016
^^^^^^^^^^^^^^^

Attended Susan's seminar at IOS, then presented ERDDAP workshop with her.
Discussed publication of value-added product of real-time data from automated tide gauge stations with Charles.
Discussed boundary condition coupling of our NEMO model to DFO FVCOM model of Vancouver Harbour and Lower Fraser River.
Created salishsea_tools.geo_tools module and started moving distance_along_curve() into it from visualizations module.
(SalishSea)


Sat 23-Apr-2016
^^^^^^^^^^^^^^^

Finished moving distance_along_curve() from visualizations module into geo_tools.
Switched nowcast production to refactor-nowcast-figures branch and restarted manager; had to fix some minor bugs, mostly re: imports, but after that things were good.
(SalishSea)


Sun 24-Apr-2016
^^^^^^^^^^^^^^^

Finished implementation of hazard exposure filter for Maps page w/ "or" within hazard columns and "and" between them; pushed it to production for Jackie to use during her user observation beta tests.
(sealinkd)


Week 17
-------

Mon 25-Apr-2016
^^^^^^^^^^^^^^^

Completed and submitted EOSM office safety self-inspection.

Continued review & cleanup of docs in preparation for James onboarding.
Created analysis-james repo.
Moved results server docs from tools/docs to docs repo.
Re-ran make_plots nowcast comparison w/o funky Tw-DP ferry data.
Worked on moving haversine() from tidetools module to geo_tools.
(SalishSea)

Attended Phys Ocgy seminar by Richard Dewey about the blob, El Nino & oscillations.

Met w/ Richard, Susan & Nancy re: nowcast, MEOPAR, ONC sensors & data, etc.

Helped Karina sort out how to use ncks to shape her MITgcm results files so that Ariane will accept them.
(canyons)

Added explanatory text for filters to Maps page per Jackie's request in issue #57.
(sealinkd)


Tue 26-Apr-2016
^^^^^^^^^^^^^^^

Finished moving haversine() into geo_tools module, changed it to use NumPy ufuncs so that it becomes polymorphic, and refactored distance_along_curve() to be vectorized by passing arrays to haversine().
Merged tools repo refactor-nowcast-figures branch into default.
Added nbsphinx extension to tools repo docs.
Added ERDDAP datasets notebook to tools docs via nbsphinx.
Started writing nowcast system framework docs.
Salish Sea team mtg; see whiteboard.
(SalishSea)

Shut down bloomcast cron job for the year.
(bloomcast)

Investigated last week's buildbot failures; appears to have been a hack attempt or a wandering bot.
Also found a bunch of long-standing build failures.
(SOG)


Wed 27-Apr-2016
^^^^^^^^^^^^^^^

Copied backlog of photos from Inbox to iPhoto on matisse.

Updated kudu to 16.04; didn't end smoothly, perhaps due to outdate SHA1 hash issue on Google hangouts plugin?
Had to pip3 install flake8 to get SublimeLinter for Python 3 happy again, perhaps due to system Python 3 being updated from 3.4 to 3.5.

Updated firmware on OM-D camera.

See project journal.
(GOMSS)

Explored configs & options in my pycharm-pyramid-test project until I figured out that the :kbd:`--reload` option has to be added to the :guilabel:`Additional options:` section of the PyCharm run config to get :command:`pserve --reload` functionality.
Also succeeded in getting pycharm-pyramid-test remote debugging on a Vagrant VM to work with an in-place deployment with the app installed in a conda-env.

Increased dev VM memory from default 512 kB to 1024 kB in hopes of resolving period app crashes.
Enabled :command:`pserve --reload` functionality in PyCharm SealinkD project.
Experimented in sealinkd_test clone with new dev VM that puts app in /home/vagrant/ to try to get PyCharm remote debugging to work.
(sealinkd)


Thu 28-Apr-2016
^^^^^^^^^^^^^^^

Failed to get PyCharm remote debugging to work in sealinkd_test clone with new dev VM that puts app in /home/vagrant/.
Email from Stephanie re: stage 3; did preliminary estimate to finish filters implementation.
Updated data model initialization docs.
Triaged issues created by Jackie after last mtg.
(sealinkd)

See project journal.
(GOMSS)

Tracked down origin of comment describing `wind grid ji` items in PLACES dict and concluded that it had lon and lat flipped.
(SalishSea)

Finished refactoring populaire tests to use pytest and handle unicode characters in names.
(RandoPony)

Registered for WestGrid advanced scheduler workshop on 17-19 May.


Fri 29-Apr-2016
^^^^^^^^^^^^^^^

Canyons team mtg
(canyons)

Upgraded niko to Ubuntu 16.04 Xenial; not the smoothest trip ever...

Met w/ Elise to plan on-boarding for James.

Refactored nowcast.figures.website_thumbnail() into nowcast.figures.publish.storm_surge_alerts_thumbnail module.
Toured Romain & Rich's drifter project web site.
(SalishSea)


Sat 30-Apr-2016
^^^^^^^^^^^^^^^

Refactored Elise's extractThalweg.py script to try to understand where it is spending its time, and to make the code more Pythonic.
(SalishSea)


Sun 1-May-2016
^^^^^^^^^^^^^^

Changed nowcast production back to default branch, pulled in Friday's storm surge thumbnail image changes, and restarted the manager; lost the make_plots worker patch that was in effect in production.
Continued refactoring Elise's extractThalweg.py script to try to understand where it is spending its time, and to make the code more Pythonic.
(SalishSea)

Decluttered some of my Firefox tab groups thanks to "Bookmark all tabs".


May
===

Week 18
-------

Mon 2-May-2016
^^^^^^^^^^^^^^

James Petrie first day on the Salish Sea team; met w/ he and Elise re: on-boarding.

Responded to Tom's plan to lock down the 142.103.250.0/24 subnet; port 22 will remain open, but some form of desktop sharing will be required to reach http://bjossa.eos.ubc.ca:8010/.

Attended Phys Ocgy seminary by Cindy on Pa/Th parameterizations in the Arctic.

Finished analysis repo splitting except analysis-nancy.
Finished refactoring Elise's extractThalweg.py script to try to understand where it is spending its time, and to make the code more Pythonic.
Explored visualisations.contour_thalweg() function.
(SalishSea)


Tue 3-May-2016
^^^^^^^^^^^^^^

Met w/ Jackie to discuss feedback from last week's end-user beta tests.
(sealinkd)

Worked w/ James & Idalia re: on-boarding.

GEOTRACES mtg; participated in review of Cindy's Pa/Th tracer code to try to find speed-ups.
(GEOTRACES)

nowcast failed at 82% due to west.cloud maintenance; restarted at about 17:45.
SalishSea team mtg.
(SalishSea)


Wed 4-May-2016
^^^^^^^^^^^^^^

Reconnected sshfs shared storage to nodes 10, 11 & 14 on west.cloud.
Experimented with elimination of module-under-test fixture in test_geo_tools and decided to make that standard practice because it makes tests easier to understand and PyCharm introspection more functional.
(SalishSea)

Experimented with new network wiring and confirmed that LAN port of Telus router needs to be connected to LAN port of Airport Extreme in order for AE to act as DHCP server; so 4 drops are required on dining room north wall.

Finished travel arrangements for Fredericton & Barrie.
Eye exam.

Wrote draft of stage 3 estimate email to Stephanie.
Updated project time tracking spreadsheet with stage 3 tasks.
Continued work on hazard exposure filter; applied it to sidebar panels on Maps page, and transferred filter criteria via query string when a sidebar panel is selected.
(sealinkd)


Thu 5-May-2016
^^^^^^^^^^^^^^

Reviewed and integrated Jackie's changes to the Help, Contact, and Privacy Policy page; CJ's how-to video looks really good!
(sealinkd)

Met w/ Elise & James to discuss running NEMO.
Software workouts planning session that merges w/ MOAD software session because only MOAD people showed up for the workout.
Worked with Susan on trying to get 04may16 nowcast run to work on orcinus.
Reconnected west.cloud instances to shared storage.
Worked on pulling svn updates from NEMO-3.6 upstream repo; got NEMO-3.6-hg-mirror to r5890, but messed up NEMO-3.6-mirror-merge step.
(SalishSea)


Fri 6-May-2016
^^^^^^^^^^^^^^

Worked on moving nowcast back to west.cloud after 2 days runs on orcinus.
Finished pulling svn updates from NEMO-3.6 upstream repo; got NEMO-3.6-hg-mirror to r5890, yesterday's NEMO-3.6-mirror-merge step was okay after all.
Committed re-enabling of VENUS central and east node T&S comparison plots.
Added handling for missing ferry salinity data that aborts comparison plot creation.
Back-filled figures and results pages for nowcast runs that were missing them due to cloud maintenance, etc.
Tested creation of a west.cloud nemo-c8-15gb-90 flavour instance from our nowcast-head-node-v4 image snapshot.
Did more elimination of module-under-test fixtures in test modules.
(SalishSea)

Finalized stage 3 estimates and send them to Stephanie.
Received payment for stage 2.
Refactor Maps page view function to encapsulate map marker attribute calculations.
Added Hazard Exposure filter to Analysis page, and implemented transfer of filter criteria between Maps and ANalysis pages.
(sealinkd)

Successfully restored timesheet spreadsheet from kudu backup to mostly recover from yesterday brainfart of copying the wrong way between kudu & USB.

Received email request from Ken for site-visit due to another Minerva server boot failure; site visit set for 11-May.
(Nordion)


Sat 7-May-2016
^^^^^^^^^^^^^^

Traveled to Parksville.

Continued elimination of module-under-test fixtures in test modules.
Explored scipy.io.loadmat() re: ONC ferry data.
(SalishSea)


Sun 8-May-2016
^^^^^^^^^^^^^^

Explored oauth2 to access Google Drive spreadsheets; made some progress with a new service account for the pony (see notes in Documents/RandoPony/test-oauth2/)
(randopony)

Returned to Vancouver.


Week 19
-------

Mon 9-May-2016
^^^^^^^^^^^^^^

Experimented with X2Go on niko but it acts like the X2Go server is not installed on smelt, sable, or cod.
Explored DFO 500m bathymetry .bag file with help from Kurt Schwehr video on YouTube; started compiling what I learned into a notebook.
Helped Elise debug `salishsea gather` failure on salish; due to missing --user flag for pip install in docs; fixed docs & corrected James' installation.
Located stdout & stderr for salish runs and wrote email to Elise & James.
Elise uncovered a bug in `salishsea combine` whereby it fails if there are no `*_0000.nc` files; resolved by changing that condition from a fatal error to an info log message.
(SalishSea)

Attended Phys Ocgy seminary by Karina about upwelling dynamics of tracers in canyons.

Helped Idalia get SaishSeaTools package installed.
(canyons)


Tue 10-May-2016
^^^^^^^^^^^^^^^

Listened to SWC lab mtg.
(swc)

west.cloud nodes went unreachable overnight; sent support request and Eric Kolb resolved the issue.
Started discussion with Eric about moving instances to new nemo- flavour so that hypervisors can be upgraded; request another segregated hypervisor to test on, and an additional temporary floating IP.
Finished BAG datasets notebook.
Talked to James about local Sphinx builds, configuring emacs, and automating SMELT parameter sensitivity runs.
Discussed consolidation of find_*_model_point() functions w/ Susan.
Salish Sea team mtg; see whiteboard.
Fixed some SalishSeaCmd package tests that were failing under Python 2.7.
Removed nowcast.lib module fixture from SalishSeaNowcast test suite; more de-boilerplating.
nowcast and forecast run plots failed due to parsing error in XML observation data from EC for Sandheads; re-ran the worker with the troublesome plots temporarily commented out.
(SalishSea)


Wed 11-May-2016
^^^^^^^^^^^^^^^

Site visit to resolve isoinfo server boot problem; see client notes file.
(Nordion)

Sandheads wind data parsing error recurred for forecast2 and nowcast runs, so I suspect that it is due to a change that EC has made; pushed code to disable troublesome plots, and re-ran worker for failed cases.
(SalishSea)

Released v2016.1 with Unicode handling for names & comments in brevet and populaire entry forms.
(randopony)


Thu 12-May-2016
^^^^^^^^^^^^^^^

Improved packaging; especially got reid of duplicated pkg metadata.
Added PayPal button integration with button from PayPal sandbox for testing.
(randopony)

Ran make_plots & make_site_page workers for nowcast 09may16 comparison.
Planned refactoring of figures.find_model_point() and stormtools.find_closest_model_point() into geo_tools.find_closest_model_point() for James to work on.
(SalishSea)

Set up swc-lesson conda environment on kudu.
Reviewed state of hg-novice lesson; pulled in changes by meta-maintainers from upstream.
Merged PR#24 re: v5.3 lesson, mostly exposition touch-ups.
Incorporated review items into refactor-01-backup branch PR#22, along with a bit of PR#24.
Started trying to figure out workflow to cherry-pcik the rest of the refactoring from the UBC 2015 workshop repo, and make it all useful for the bug bbq.
(swc)


Fri 13-May-2016
^^^^^^^^^^^^^^^

Created tools repo issue #35 re: adding geo_tools.find_closest_model_point().
Finally fixed date range bug in grid on nowcast results index page after nowcast comparison page generation.
Added A-O vol & iss to storm surge paper citations on nowcast results pages.
Merged NEMO-3.6r5890 repo into NEMO-3.6-code and deleted the former.
Pulled svn r5912 (re: tides) from upstream and created NEMO-3.6r5912 repo for Susan to test.
Fixed Sandheads wind observations data issue that was breaking figures; EC added 2 underscores to the bulk climate data service URL.
(SalishSea)

Participated in MOAD software session; topics: waterhole OS upgrade & editors, PEP8, `if __name__ == '__main__':`, PBS scripts


Sat 14-May-2016
^^^^^^^^^^^^^^^

Worked on network cabling at home; making Cat 6 patch cables is harder than it looks :-(

Discussed new SalishSeaCmd features w/ Susan and decided that moving iodef.xml into YAML file has priority over making rebuild_nemo explicit in YAML file.
(SalishSea)


Sun 15-May-2016
^^^^^^^^^^^^^^^

Installed Vidyo in preparation for Westgrid advanced scheduling session this week.

Tagged SalishSeaCmd v2.1 re: start of v2.2 dev and bumperd version to 2.2.dev0.
Changed salishsea run and salishsea prepare so that iodef.xml comes from YAML file instead of command-line; applies to 3.4 and 3.6.
Continued elimination of module-under-test fixtures in test modules.
Reviewed and helped Susan merge her SalishSeaCmd job chaining changes.
Started changing patch.object() to patch() in light of elimination of module-under-test fixtures.
(SalishSea)


Week 20
-------

Mon 16-May-2016
^^^^^^^^^^^^^^^

Installed Vidyo in preparation for Westgrid advanced scheduling session this week.

Disabled ONC-ADCP data download cron job until old data feed is fixed and new deployment configuration is set up.
Data download failed on 4-Apr due to full disk on /ocean; processing has failed since 5-Apr due to unexpected EOF, presumably due to 4-Apr download failure.
Introduced James to tools repo, and the work I want him to do in geo_tools (issue #35); also discussed his bio model parameter study code with him.
Redundancy actually saved the day in the central/raw/ data tree; deleting an incomplete 2-Apr file and an empty 3-Apr one got us back on track for that node until the end of the deployment on 30-Apr.
East and DDL node downloads end with 2-Apr; started downloads to backfill; abject failure.
Started work on extracting all actual ferry crossings for a given NEMO results day from ONC ferry data.
Discovered and fixed bug whereby all of the ferry route surface salinity comparison figures since 3-May were using the HB_DB route; re-build figures and pages.
Did more exploring of the ferry data and found that the "day" TSG files vary in time span, and are only about 17 hours long.
(SalishSea)

Attended Phys Ocgy seminary by Ben Moore-Malley about winds and current in the Salish Sea model.


Tue 17-May-2016
^^^^^^^^^^^^^^^

Worked on salishsea_tools.data_tools.
Fixed nowcast run_NEMO & run_NEMO36 workers re: moving iodef.xml into YAML file.
Salish Sea team mtg; see whiteboard.
Helped James get flake8 and python-mode working emacs23.
(SalishSea)

Participated in day 2 of Westgrid scheduling & job mgmt online workshop; basic scheduling.


Wed 18-May-2016
^^^^^^^^^^^^^^^

Discussed CMOS talk & eastern-MEOPAR collaboration activities w/ Susan.
Worked through Python 3.4/3.5 tuple unpacking issue with Nancy.
(SalishSea)

Moved timesheet to Google Sheets because USB stick transfers are getting old.

Started work on docs & web services setup; see project work journal.
(GOMSS)

Participated in day 2 of Westgrid scheduling & job mgmt online workshop; memory, job features, queue & job info.
Resulted in discovery that nowcast-green runs on orcinus seem to use 332mb per processor when run on 145 processors, so Susan is testing runs with 500mb memory request instead of 2000mb, based on advice from Roman.


Thu 19-May-2016
^^^^^^^^^^^^^^^

Discovered that west.cloud shared storage connection failed on all but head node, so 18-May runs all failed, but the failure message was way too innocuous.
Helped Nancy get conda environments working for her.
Discussed conda-forge and gsw package w/ Elise.
Started testing nemo-c8-15gb-90 flavour on west.cloud; spotted 0Gb root disk issue, and Eric fixed that.
Got nowcast run started on west.cloud after Susan ran 18-May run on orcinus.
Discussed j,i indexing and find_closest_model_point() refactoring w/ James.
Wrote library code docs section re: returning namedtuples.
Added James to project contributors lists & nowcast critical messages list.
Diagnosed 18 weather download failure caused by IMAP server maintenance.
Manually ran 18 weather download at ~19:45 and it took ~2m!!
Advanced times of all weather downloads by 1h to see if we can win vs. our present 1h40h typical download times.
(SalishSea)

Participated in day 3 of Westgrid scheduling & job mgmt online workshop; priority, fairshare, cluster operations.


Fri 20-May-2016
^^^^^^^^^^^^^^^

Physio appt re: left shoulder; stretches: broomstick, towel, and shoulders back on bike at stops.

Continued work on docs & web services setup; see project work journal.
(GOMSS)


Sat 21-May-2016
^^^^^^^^^^^^^^^

Explored circus process manager for Pyramid apps (and perhaps for nowcast).
circus-web fails under Python 3.5, so no web interface to stats; use circus-top instead.
Installation of dependencies:
  conda create -n circus libevent pyzmq tornado psutil six
  pip install circus chaussette
chaussette is a WSGI server front-end that works well with circus; it uses wsgiref by default, but can use waitress as a backend, or lots of other Py2 backends.

Confirmed that west.cloud compute and head node images can be launched on new nemo-c8-15gb-90 flavour VM, and that shard storage can be mounted; emailed Eric re: plan for transition.
Worked on nowcast system software framework docs.
(SalishSea)


Sun 22-May-2016
^^^^^^^^^^^^^^^

Hiked to 1st Summit of the Stawamus Chief.


Week 21
-------

Mon 23-May-2016
^^^^^^^^^^^^^^^

**Victoria Day**

Worked on nowcast messaging system docs.
Discussed nowcast biogeochemistry figures w/ Susan and work for James while we are at CMOS.
Created tools repo issue #36 re: nowcast.figures.tracer_thalweg_and_surface module for James to work on during CMOS, but Elise says that he is well into the SMELT parameters study.
(SalishSea)

Experimented with vagrant VMs and docker containers for development of nowcast system and, once again, concluded that, cool as it is, docker isn't the right tool for the job.


Tue 24-May-2016
^^^^^^^^^^^^^^^

Worked on CMOS talk outline.
(CMOS)

Agreed w/ Eric@uvic to bring west.cloud instances down by 09:30 on Thu for shift to segregated nodes.
Reviewed James' geo_tools.find_closest_model_point() code.
Experimented with building XIOS with .hg/ and README.md in arch/ directory, and it went fine.
Emailed Dany re: content for my CMOS talk.
(SalishSea)


Wed 25-May-2016
^^^^^^^^^^^^^^^

Added my support to a nomination of Andrew Pollard for a Queen's grad supervision award.

forecast2 run failed due to missing Fraser River flow data; manually downloaded Fraser & Englishman River flows, and ran make_runoff_file worker.
06 weather download took almost 3h.
Skipped forecast2/24may16 run.
Experimented with building XIOS w/ arch files in an arrch/ sub-directory; no go, so XIOS-arch repo has to manage arch names in a single directory.
Started development of NEMO_Nowcast framework package with a new version of the message broker that uses dict logging configuration from the YAML config file.
(SalishSea)

Physio appt re: left shoulder; stretches: broomstick or wall crawl, towel, hands behind head, doorway chest stretch, and hunch to flatten blades, then shoulders back on bike at stops.

Triaged issues created by Jackie from beta test observations.
Wrote proposal for stage 3 and sent it to Penny.
(sealinkd)

Pinged Ken at Nordion re: overdue invoice.
(43ravens)

Started development of NEMO_Nowcast framework package; see project work journal.
(GOMSS)


Thu 26-May-2016
---------------

Got NEMO_Nowcast message broker working under the supervision of circus process manager so that it is properly daemonized rather than a background process with a disconnected tty.
Shut down west.cloud instances for migration to segregated VMMs.
Started re-building west.cloud instances on nemo-c8-15gb-90 flavours at 10:42; finished by 11:40.
Nowcast run failed due to Python 3 environment issue; after much thrashing with system packages, ended up installed in miniconda3 and a nowcast-prod conda env.
(SalishSea)

Continued development of NEMO_Nowcast framework package; see project work journal.
(GOMSS)


Fri 27-May-2016
^^^^^^^^^^^^^^^

Prepared for and participated in MOAD software session; topics: figures.py & SalishSeaNowcast conda env; westgrid scheduling, priority & job mgmt.

Created slides for CMOS talk and reviewed them with Susan.
Read abstracts and planned my conference.
(CMOS)


Sat 28-May=2016
^^^^^^^^^^^^^^^

Travel to Fredericton for CMOS conference

Continued work on NEMO_Nowcast package; see project work journal.
(GOMSS)


Sun 29-May-2016
^^^^^^^^^^^^^^^

CMOS conference

Created on GOMSS_Nowcast package; see project work journal.
(GOMSS)


June
====

Week 22
-------

Mon 30-May-2016
^^^^^^^^^^^^^^^

CMOS conference

Participated in collaboration session I presented my "Towards a National Repository..." talk to good reception.


Tue 31-May-2016
^^^^^^^^^^^^^^^

CMOS Conference

Participated in parts 3 & 4 of coastal ocgy session.
Stephanie Waterman won inaugural early career CNC-SCOR award.
Roger François won the Tim Parsons medal.

Continued buffing notebook about nowcast time series via ERDDAP & xarray.
(SalishSea)


Wed 1-Jun-2016
^^^^^^^^^^^^^^

CMOS Conference

Skipped plenaries.
Attended Phys Ocgy Atlantic & Arctic session.
Susan won CMOS President's Prize for Allen & Hickey (2010).

Finished buffing notebook about nowcast time series via ERDDAP & xarray.
Worked through ADCP download scripts updated for May-2016, but downloads still fail, so sent email to Marlene for advice.
(SalishSea)

Continued work on NEMO_Nowcast package; see project work journal.
(GOMSS)


Thu 2-Jun-2016
^^^^^^^^^^^^^^

CMOS Conference

Travel to Barrie to visit parents.


Fri 3-Jun-2016
^^^^^^^^^^^^^^

Visiting parents in Barrie.

Started refactoring figures.PA_tidal_predictions() to publish.pt_atkinson_tide module.
(SalishSea)


Sat 4-Jun-2016
^^^^^^^^^^^^^^

Visiting parents in Barrie.

Continued refactoring figures.PA_tidal_predictions() to publish.pt_atkinson_tide module.
(SalishSea)


Sun 5-Jun-2016
^^^^^^^^^^^^^^

Visiting parents in Barrie.

Finished refactoring figures.PA_tidal_predictions() to publish.pt_atkinson_tide module.
Investigated error from geo_tools.finde_closest_model_point() in figures.research_ferries(); probably due to overly aggressive vectorization that I suggested to James.
(SalishSea)

Continued work on NEMO_Nowcast package; see project work journal.
(GOMSS)


Week 23
-------

Mon 6-Jun-2016
^^^^^^^^^^^^^^

Visiting parents in Barrie.

Worked on building conda packages; see project work journal.
(GOMSS)

Experimented successfully with serving salishsea static site from a Pyramid app so that it can be incrementally converted to a dynamic site.
(SalishSea)


Tue 7-Jun-2016
^^^^^^^^^^^^^^

Travel from Barrie to Vancouver

Continued removal of module-under-test boilerpate code from SalishSeaNowcast workers test suite.
(SalishSea)


Wed 8-Jun-2016
^^^^^^^^^^^^^^

Physio appt; continue stretches: broomstick or wall crawl, towel, hands behind head, doorway chest stretch, and hunch to flatten blades, then shoulders back on bike at stops; add new stretches: tubing arm pull in front of mirror, arm push lying on side.
Reconfigures my home desk per Stephanie's recommendations, and ordered laptop roost.

Reviewed James' fix for find_closest_model_point() issue in research_ferries module and pulled it into production.
Dealt with nowcast launch failure due to full disk on west.cloud; cron job that deletes old run results got lost when cloud was rebuilt.
(SalishSea)

Uploaded initial packages to GoMSS-Nowcast org on Anaconda.org; see project work journal.
(GOMSS)

Got PO for stage 3 work.
(sealinkd)

Set up Sentry service trial account and tested raven client against GoMSS Nowcast project there.


Thu 9-Jun-2016
^^^^^^^^^^^^^^

Reviewed slides for Westgrid townhall tomorrow; orcinus, jasper & bugaboo all scheduled for decommissioning in 2017!!

Worked on hg-novice lesson for v5.4 release.
Merged refactor-01-backup pull request (#22).
Cherry-picked refactor-02-collab branch from UBC 22Sep2015 workshop repo, buffed it, and created PR#25.
Cherry-picked refactor-03-conflict branch from UBC 22Sep2015 workshop repo and created PR#26.
Cherry-picked refactor-04-conflict branch from UBC 22Sep2015 workshop repo, buffed it, and created PR#27.
Reviewed and updated open issues.
(swc 3.5 hr)

Started refactoring figures.compare_tidalpredictions_maxSSH() to publish.compare_tide_prediction_max_ssh module.
(SalishSea)


Fri 10-Jun-2016
^^^^^^^^^^^^^^^

Sent invitations to bitbucket team, and worked on project docs; see project work journal.
(GoMSS)

Continued refactoring figures.compare_tidalpredictions_maxSSH() to publish.compare_tide_prediction_max_ssh module.
Reviewed James' progress on tracer_thalweg_and_surface().
(SalishSea)

Watched Westgrid townhall mtg re: future direction:
* 200k old cores -> 126k new cores -> 300k new cores in 2018
* 27 data centres -> 5-10 data centres in 2018
* 2 Pflops -> 12 Pflops in 2018
* 20 Pb -> 50 Pb storage in 2018
* 4 sites: Victoria, SFU, Waterloo, Toronto
* GP1: Vic cloud
* GP2 & GP3:SFU & Waterloo general compute - take over orcinus, etc.
* LP1: Toronto large parallel jobs (>1000 cores)
* national storage infrastructure:
  * silo -> sfu
  * new distributed object store
  * dCache at sfu for ATLAS, SNO, etc.
* RAC 2017 will start in Aug, and it will be tight
* very little compute available, no storage available, minimal support for existing software


Sun 12-Jun-2016
^^^^^^^^^^^^^^^

Travel fro Vancouver to Portland

Continued work on NEMO_Nowcast package; see project work journal.
(GOMSS)


Week 24
-------

Mon 13-Jun-2016
^^^^^^^^^^^^^^^

Travel from Portland to Corvallis

Continued work on NEMO_Nowcast package; see project work journal.
(GOMSS)


Tue 14-Jun-2016
^^^^^^^^^^^^^^^

Visiting OSU College of Earth, Ocean & Atmospheric Sciences; hosted by Ted Strub.

Discussion of operational ocean models and working with stakeholders w/ Ted, Craig Risien (OOI & NANOOS), Lana Erofeeva (runs OSU op model), Anthony (CS student on seacast.org team). Looked at:
* salishsea.eos.ubc.ca
* http://ingria.coas.oregonstate.edu/rtdavow/
* http://seacast.org/
* oceanviewer.org/
* http://nvs.nanoos.org/Explorer

Changed make_site_page worker so that only available figures are rendered, and page is note rendered if there are no figures to show.
(SalishSea)

Attended Susan's seminar at OSU about what the model tells us about deep water renewal and vice versa.


Wed 15-Jun-2016
^^^^^^^^^^^^^^^

Visiting OSU College of Earth, Ocean & Atmospheric Sciences; hosted by Ted Strub.

Started serious work on creating a Vagrant VM that emulates the nowcast system deployment on skookum; repo is nowcast-vm.
forecast2 run failed because EC had issues that meant that the 06 weather was incomplete.
nowcast and nowcast-green runs failed to launch; probably due to make_runoff_file worker not having been run because it is triggered by the completion of download_weather 06.
nowcast was also impacted by all 18 nodes on west.cloud having lost their connection to shared storage.
Answered Paul's email about NEMO results metadata.
(SalishSea)

Lost eduroam access to Internet at 14:15.

Continued work on NEMO_Nowcast package; see project work journal.
(GOMSS)

Toured OOI Ocean Observing Initiative operations.


Thu 16-Jun-2016
^^^^^^^^^^^^^^^

Travel from Corvallis to Vancouver

Continued work on NEMO_Nowcast package; see project work journal.
(GOMSS)

Worked on stage 3 issues; completed #64, #65, #67, #68 & #69; did #63 for Maps page (also need to do Analysis page).
(sealinkd)


Fri 17-Jun-2016
^^^^^^^^^^^^^^^

Pushed yesterday's closed issued to production.
(sealinkd)

Physio appt; continue stretches: broomstick or wall crawl, towel, hands behind head, doorway chest stretch, and hunch to flatten blades, then shoulders back on bike at stops, tubing arm pull in front of mirror, arm push lying on side; add new stretch: spread arms against tubing, working subscapular not trapezius.
Reconfigures my EOAS desk per Stephanie's recommendations, and ordered laptop roost; need higher desk & monitor lift.

Discussed progress w/ James.
Continued work on nowcast-vm; added miniconda installation, and nowcast-env setup.
(SalishSea)


Sat 18-Jun-2016
^^^^^^^^^^^^^^^

Email discussion w/ Elise about incorporating latest SMELT changes into nowcast-green production.
Finished refactoring figures.compare_tidalpredictions_maxSSH() to publish.compare_tide_prediction_max_ssh module; need Nancy to confirm whether the residual calculation is correct.
(SalishSea)

Worked on hg-novice lesson for v5.4 release.
Merged refactor-02-collab PR#25.
Merged refactor-03-conflict PR#26.
Merged refactor-04-conflict PR#27.
Pinged the pong to Greg for conversion to new lesson layout/style.
(swc 1 hr)

See project work journal.
(GOMSS)


Sun 19-Jun-2016
^^^^^^^^^^^^^^^

Investigated time series axis tick labels offset in production deployment of compare_tide_prediction_max_ssh compared to test notebook; suspect different matplotlib package difference (1.5.0 vs 1.5.1), so updated that and dependencies on both skookum and kudu.
Pullled Elise's nowcast-green changes in SS-run-sets and NEMO-3.6-code into nowcast-sys and rebuilt NEMO-3.6 on salish.
Changed `salishsea combine` to find rebuild_nemo on NEMO-code path instead of from nemo executable.
Fixed failing unit tests due to introduction of run chaining changes.
(SalishSea)

Discovered forgotten hazard filter refactoring work on kudu that wasn't pushed to Bitbucket; merged it with recent work from niko, and landed in a horror show.
VM on kudu was corrupted, so had to rebuild it from scratch:
* sudo -i -u postgres to create dlatornell & sealinkd users & sealinkd database
* sudo -i -u sealinkd
* source /home/sealind/miniconda/bin/activate sealinkd to activate conda env
* load database using model.scripts
* didn't set up Piwik
Recovered rebase merge horror show.
Pushed Analysis page hazard filter work from kudu to production and closed issue #63.
Decided to not try to propagate filter criteria from Maps page through map marker clicks to Profiles page then back to Analysis/Maps pages.
(sealinkd)

Experimented with pyramid_crow package in sealinkd dev context and found possible bug in over-long request body handling; created issue #1 on github.


Week 25
-------

Mon 20-Jun-2016
^^^^^^^^^^^^^^^

Continued work on nowcast-vm; got /results/nowcast-sys/nowcast-env conda environment setup, and successfully launched message broker and manager processes.
Explored ONC data web services API.
Dicsused ONC data access w/ Rich.
(SalishSea)

Attended Susan's Phys Ocgy version of the seminar she gave at OSU last week.


Tue 21-Jun-2016
^^^^^^^^^^^^^^^

Continued Exploring ONC data web services API; see analysis-doug ONC-DataWebServices notebook.
Prepared for and executed splitting analysis/Nancy into analysis-nancy repo.
Changed analysis repo to be read-only for everyone but admins.
Explained nowcast system to James.
Participated in Salish Sea team mtg; see whiteboard.
(SalishSea)

Received email request from Ken for site-visit due to another Minerva server boot failure.
(Nordion)


Wed 22-Jun-2016
^^^^^^^^^^^^^^^

Scheduled Nordion site visit for 30-Jun.
(Nordion)

See project work journal.
(GOMSS)


Thu 23-Jun-2016
^^^^^^^^^^^^^^^

See project work journal.
(GOMSS)

Helped James with full disk issues in /data partition.
(SalishSea)


Fri 24-Jun-2016
^^^^^^^^^^^^^^^

Fixed storm surge residual calculation for nowcast publish pages re: corrected ssh per Nancy's email.
Moved compute_residual from figures to nowcast.residuals module.
Prototyped GEM2.5 wind rotation correction in notebook and sent results to Ben for checking.
Started work on VENUS nodes CTD observations vs. model results comparison figure.
(SalishSea)

MOAD software session re: SalishSeaTools.
(MOAD)

Reproduced IE11 sing-up button issue #72 on EOAS Win7 IE11 laptop and tracked it down to lack of support for the form attribute in button elements in all Microsoft browsers.
(sealinkd)


Sat 25-Jun-2016
^^^^^^^^^^^^^^^

See project work journal.
(GOMSS)

Inspected result of setting ln_cfmeta flag to true in NEMO-3.6; more CF-1.5 metadata, but nothing dramatic.
(SalishSea)


Week 26
-------

Mon 27-Jun-2016
^^^^^^^^^^^^^^^

Continue work on VENUS nodes CTD observations vs. model results comparison figure.
Started working on parsing ONC web service data into something more Pythonic.
(SalishSea)

Phys Ocgy seminars by 2 visiting MIT/WHOI PhD students; one on linearized ssh modeling, the other on turbulence microstructure in the Drake Passage.


Tue 28-Jun-2016
^^^^^^^^^^^^^^^

Settled on xarray.Dataset object to parse ONC web service data into.
Continue work on VENUS nodes CTD observations vs. model results comparison figure.
Salish Sea team mtg; see whiteboard; Serena, visiting from Hong Kong, joined the group for a month.
(SalishSea)

Farewell party for John Amor.

Helped Karina setup up CanyonTools repo and package.
(canyons)


Wed 29-Jun-2016
^^^^^^^^^^^^^^^

Physio appt; continue stretches: broomstick or wall crawl, towel, hands behind head, doorway chest stretch, flatten blades, then shoulders back on bike at stops, tubing arm pull in front of mirror, arm push lying on side, spread arms against tubing, working subscapular not trapezius; add new stretches: free the bird every 90 minutes at desk, and forearm raise against tubing under foot.

Discussed next stage of NEMO-3.6 updates from upstream w/ Susan.
(SalishSea)

Implemented possible fix for IE forms button issue #72.
Explored Compare page community selectors updating bug reported as issue #77 but can't reproduce it.
Implemented Actions of Interest filter on Maps and Analysis pages (closed issue #78); also updated explanatory text about filters (closed issue #57).
I think I convinced myself that the sentry raven client picks up its DSN from the environment if it is not defined in the app's .ini file.
(sealinkd)


Thu 30-Jun-2016
^^^^^^^^^^^^^^^

Nordion site visit re: isoinfo server boot failure; see work notes.
(nordion)

Prep for and attended workout by Ben & Jie re: animation.
(swc)

Continue work on VENUS nodes CTD observations vs. model results comparison figure.
(SalishSea)

Tested sign-in and sign-up on Win 7 Pro IE 11 and confirmed that new code works; closed issue #72.
Re-opened issue #65 re: target of map marker clicks on Maps page; s/b Compare page, not Profiles page.
(sealinkd)


Fri 1-Jul-2016
^^^^^^^^^^^^^^

**Canada Day**

Enabled Sentry exception logging for production deployment.
Cleaned up Jackie's HTML edits on the About page.
(sealinkd)


Sat 2-Jul-2016
^^^^^^^^^^^^^^

See project work journal.
(GOMSS)

Helped Susan change nowcast-green to use bathymetry that facilitates use of Orlanski boundary conditions; 1st stage is a clean start initialized with restart T&S and a 20s time step.
(SalishSea)


Sun 3-Jul-2016
^^^^^^^^^^^^^^

Helped Susan change nowcast-green to use bathymetry that facilitates use of Orlanski boundary conditions; 2nd stage is a restart with a 30s time step.
(SalishSea)


July
====

Week 27
-------

Mon 4-Jul-2016
^^^^^^^^^^^^^^

Helped Susan change nowcast-green to use bathymetry that facilitates use of Orlanski boundary conditions; 3rd stage is a restart with a 40s time step.
Changed runNEMO36 worker to enable group write permission on run results directories.
Discussed interpolation to VENUS node depths for CTD comparison figure w/ Susan.
Continue work on VENUS nodes CTD observations vs. model results comparison figure; added T&S time series from nowcast-green results.
Worked on testing CTD comparison figures in nowcast-vm and improved it in it's first real use test.
(SalishSea)

Attended Phys Ocgy seminar by Serena McDonnell about shelf slope modeling in the South China Sea around Hong Kong.


Tue 5-Jul-2016
^^^^^^^^^^^^^^

Restarted nowcast manager from an environment that exported ONC_USER_TOKEN envvar in preparation for release to production of CTD comparison figures code.
Added VENUS upper slope Delta node to places module.
Pushed CTD comparison figures code to production.
Merged NEMO-3.6-code into NEMO-3.6-mirror-merge at NEMO-3.6r5912 tag on niko and pushed to NEMO-3.6-code on Bitbucket; deleted NEMO-3.6-r5912 repo from Bitbucket.
Pulled changesets 5918 through 6036 into NEMO-3.6-hg-mirror on salish.
Merged NEMO-3.6-hg-mirror into NEMO-3.6-mirror-merge on niko.
Tagged NEMO-3.6-r6036 in NEMO-3.6-mirror-merge and pushed to new NEMO-3.6-r6036 repo on Bitbucket for Susan to use for merge-comparison test.
Set up Apache2 and a salishsea.eos.ubc.ca virtual host in the nowcast-vm so that I can start developing and testing Pyramid-based implementation of the site.
Worked through critical errors due to pushing CTD comparison figures to production.
(SalishSea)


Wed 6-Jul-2016
^^^^^^^^^^^^^^

Triaged issues that have been added since Stage 3 PO.
Reviewed and buffed Jackie & Michelle's changes to the help & about pages; adding team member images to bios will be a bit of work.
Fixed and re-closed issue #65 re: Maps markers linking to Compare page, not Profiles page.
Added "work-in-progress" banner to landing page at Stephanie's request.
Resolved issue #71 pending approval from Jackie.
Closed issues: #62, #59, #66, #80, #81.
Restructured Compare page to move panel header & communities selectors into left column.
(sealinkd)

Updated nowcast-green NEMO code to NEMO-3.6r5912+ (specifically, changeset 421738d4896d).
Discussed ONC data row limit w/ Nancy.
Discussed ONC ADCP data w/ Rich.
(SalishSea)


Thu 7-Jul-2016
^^^^^^^^^^^^^^

Updated deployment docs re: loading data from CommunityProfileTableData spreadsheet.
Added team member photos to bios on About page via Assets.
Added new contact info fields to Community data model & Profiles page; issue #82.
Updated communities table from HVSIIndicatorData_Jun30.xlsx spreadsheet.
Updated deployment docs re: loading data from HVSIIndicatorData spreadsheet.
Added new fields to Indicator data model; issue #83.
Updated indicators & indicator_values tables from HVSIIndicatorData_Jun30.xlsx spreadsheet.
Reviewed and buffed Jackie's addition of the new Youtube URL to About page.
Closed issue #75 re: addition of indicator short names to Maps page community marker popups.
Closed issue #76 re: revised Compare page capital HVSI details tables.
Sent email to Jackie declaring v1.1 finished and asking for her confirmation of that and outstanding issues; she closed issue #71.
Jackie reported various features and data not working properly and I eventually realized that I had not correctly run all of the data loading scripts upon completion of issue #82.
Explored page loading indications re: issue #56; CSS/js techniques trigger once the page starts to load in the browser so okay for xhr but useless for initial server-side processing. Changing mouse cursor to wait icon is doable but couldn't figure out how to reset it if the user does a browser back function.
Experimented with memoization caching of sqlalchemy query functions and found that I can generally reduce page load times to <100ms on dev vm.
(sealinkd)


Fri 8-Jul-2016
^^^^^^^^^^^^^^

MOAD software session where we discussed Ariane and other Lagrangian particle tracking tools.

Discussed nowcast CTD comparison figures and adding ONC CTD data to our ERDDAP server w/ Nancy and later w/ Susan.
Discussed profiling NEMO and code vectorization w/ Elise.
Worked on notebook to explore getting ADCP data from ONC using Python instead of Matlab.
(SalishSea)

EOAS network suffered major failure due to a disk crash on anu server; lost DNS, DHCP, and /home partition.


Sat 9-Jul-2016
^^^^^^^^^^^^^^

Early morning thrash before ferry to Nanaimo to try to recover nowcaast system from anu failure. skookum's /home mount point is stale and needs to be reset by Charles before I can access it; Susan can access it, but it can't find libpython35 due to stale mount handle.
Changed nowcast worker sequencing to laumch hg_update_site worker after make_site_page completes for comparison figures page instead of publish figures page because comparison plots now takes longer to generate than publish plots.
Pulled NEMO-3.6 code updates to fix light extinction coefficients calculation into nowcast env on salish and re-built.
Ran a bunch of workers manually to eventually get automation running again.
(SalishSea)

See project work journal.
(GOMSS)


Sun 10-Jul-2016
^^^^^^^^^^^^^^^

Manually downloaded nowcast results for 9jul2016 and ran make-plots research worker; necessary because I had to kill the watch_NEMO workers yesterday in order to get logging from manager working again after anu crash.
(SalishSea)

See project work journal.
(GOMSS)


Week 28
-------

Mon 11-Jul-2016
^^^^^^^^^^^^^^^

Added handling for FileNotFoundError to make_plots comparison worker so that it doesn't crash when the ferry data files are missing.
Made teos_tools functions more polymorphic.
Changed VENUS nodes CTD comparison figures to use reference salinity.
Added attribution to ONC for data on VENUS nodes CTD comparison figures.
Changed VENUS nodes CTD comparison figures to include only observations with qaqcFlag==1.
Continued work on getting ONC ADCP data; debugged matlab script to the point that I understand that it times out because the search status reporting is broken on the ONC server end.
Generated enough error messages that Marlene inadvertently gave me the hint that my Python requests were using the wrong deployment location; fixed that and now my notebook works as well as the matlab script.
Reported progress to Rich.
Added debug logging of figure files as they are saved to make_plots worker to facilitate progress monitoring.
Manually ran make_plots and make_site_page workers for comparison plots for 3jul16 through 10jul16 runs.
Updated nowcast deployment docs re: crating conda environment and adding activate/deactivate hook scripts to export/unset environment variables.
(SalishSea)

Attended Phys Ocgy seminar by Yulia Egorova about analysis of young salmon in Rivers Inlet.


Tue 12-Jul-2016
^^^^^^^^^^^^^^^

More EOAS network chaos.
Continued email discussion w/ Marlene@ONC re: ADCP data; polling ftp directly, other API?, netCDF format?
Fixed a bunch of warnings in tools docs.
Ran download_results & make_plots workers manually for forecast2 run; site build didn't happen because of recent change to build after comparison plots (non-existent for forecast runs).
Fixed nowcast flow so that publish plots & pages always happen last so that site gets built and updated regardless of run type.
Added -q flag to sphinx_build worker to reduce volume of debug log output.
Salish Sea team mtg; see whiteboard.
(SalishSea)

Started work on html-css-js presentation for Thu workout.
(swc)


Wed 13-Jul-2016
^^^^^^^^^^^^^^^

Physio appt; continue stretches: broomstick or wall crawl, towel, hands behind head, doorway chest stretch, flatten blades, then shoulders back on bike at stops, tubing arm pull in front of mirror, arm push lying on side, spread arms against tubing, working subscapular not trapezius, free the bird every 90 minutes at desk, and forearm raise against tubing under foot; add rows against tubing with focus on using subscapulars not neck, switch to rows when other resistance exercises fatigue me to to point of shoulder hunching.

Replied to query from Mitchell@DFO re: accessing our NEMO model results & docs.
(SalishSea)

See project work journal.
(GOMSS)


Thu 14-Jul-2016
^^^^^^^^^^^^^^^

Finished and presented SWC workout on HTML, CSS, and JavaScript.
(swc)

Got invitation from Dwight@ONC to discuss ONC API design.
Discussed API requirements idea w/ Susan, Kong & Drew.
Worked on polling ONC FTP server to get ADCP results; works so long as their backend doesn't fall over; retrying library is awesome!
(SalishSea)


Fri 15-Jul-2016
^^^^^^^^^^^^^^^

Nowcast system collapsed again overnight due to failure of communication re: timing of restoration of anu server home.
* touched NBssh.png & wg.png to refresh file handles
* killed and restarted message broker and manager to reconnect them to log files
* manually ran get_NeahBay_ssh forecast2 worker
* manually ran make_runoff_file worker
* manually ran dowonload_weather 00 worker
Discussed ERDDAP & xarray issue on 2d mesh mask dataset w/ Nancy; perhaps relatedly got >25% request failure alert from ERDDAP.
ubcSSn2DMeshMask2V1 dataset is missing variables glamf and gphif, but more importantly it is malformed, probably because the time_counter variable in the source file has no units; ubcSSn3DMeshMask2V1 probably only works by accident.
(SalishSea)

See project work journal.
(GOMSS)

MOAD bbq at Locarno Beach.


Sat 16-Jul-2016
^^^^^^^^^^^^^^^

Triaged issues in Jackie's 8-Jul pre-release review email.
Re-opened issue #76, moved icons, and re-closed.
Created and addressed new issues #84 through #88.
Added extraction of URLs from spreadsheet HYPERLINK functions to load_flood_planning_data & load_risk_reduction_actions scripts.
Handled empty category cells in load_risk_reduction_actions script.
Added changing mouse cursor to wait style prior to loading slow pages, though I hated doing so.
Rationalized community names in URLs to always use spaces, not underscores, and trashed my way through the mess that made of js updating of the compare page selectors.
Started hacking a way of serving PoCo emergency recover doc from assets; re: issue #79.


Sun 17-Jul-2016
^^^^^^^^^^^^^^^
Finished hacking a way of serving PoCo emergency recover doc from assets; re: issue #79.
Strongly suggested to Jackie that stage 3 is done.
(sealinkd)

Fixed permissions on pre-jul16 nowcast-green results directories so that Susan can delete outdated restart files.
Added KeyError handling to ferry salinity plots section of make_plots worker; another way that ferry data can fail.
(SalishSea)


Week 29
-------

Mon 18-Jul-2016
^^^^^^^^^^^^^^^

Fixed time_counter metadata in mesh_mask_SalishSea2.nc to make ERDDAP happy; re: issue that Nancy raised on Friday.
Finished notebook re: getting ONC ADCP data; started work on implementation in data_tools.
(SalishSea)


Tue 19-Jul-2016
^^^^^^^^^^^^^^^

Deleted Profile page template code for community image because it was prducing spurious text on some pages, and the feature is not presently wanted; issue #89.
Removed work-in-progress banner from landing page.
Bumped version to 1.1, tagged it, and declared it released.
(sealinkd)

Video conference w/ ONC re: web service APIs for data; Dwight, Ryan & Christine.
Finished initial implementation of functions to get ONC ADCP data in data_tools.
Salish Sea team mtg; see whiteboard.
(SalishSea)


Wed 20-Jul-2016
^^^^^^^^^^^^^^^

Wrote report on stage 3 work and submitted invoice.
Emailed Stephanie re: ending or transferring monthly Bitbucket charge; she elected to remove CJ from the account, so I did so and downgraded to the free tier.
(sealinkd)

Nowcast forecast2 hg_update, sphinx_build & rsync_to_web workers all failed weirdly, and logs seem to be stuck.
(SalishSea)

See project work journal.
(GOMSS)


Thu 21-Jul-2016
^^^^^^^^^^^^^^^

See project work journal.
(GOMSS)

Stopped and re-started message broker and manager to try to resolve what looks like a stale NFS handle issue.
Fielded question from Marlene about EC HRDPS dataset on our ERDDAP server.
Built a salishsea-tools conda env on ocean for ONC ADCP file processing; downloaded 2 central node files, but am puzzled that the file names imply that they are for the day before the date requested.
Investigated lack of log messages from west.cloud that magically resolved itself.
(SalishSea)


Fri 22-Jul-2016
^^^^^^^^^^^^^^^

Dentist appt.

MOAD software session where we worked on porting Rob Irwin's CTD database code to Python 3.

Reviewed Nancy's module for extraction of Salish Sea NEMO model western boundary conditions from UW Live Ocean model product.
Mtg w/ Elise & James re: next steps for James running on jasper and tuning bio parameters.
Mtg w/ Nancy re: script to get boundary conditions from LiveOcean model, and xarray.
Fixed date parsing bug in ONC ADCP search & download code.
(SalishSea)

Updated Ubuntu to 16.04.1 and PyCharm to 2016.2 on niko.


Sat 23-Jul-2016
^^^^^^^^^^^^^^^

Updated PyCharm to 2016.2 and Ubuntu to 16.04.1 on kudu.

Worked on backfilling ONC ADCP data, but central node May 1 & 2 are troublesome.
(SalishSea)


Sun 24-Jul-2016
^^^^^^^^^^^^^^^

Ordered portable backup drive for niko.

Got backfilling of ONC ADCP data flowing by skipping central node May 1 & 2; completed the rest of May.
Started backfilling of ONC ADCP data for east node but it stalled on April 9 & 10.
(SalishSea)

See project work journal.
(GOMSS)


Week 30
-------

Mon 25-Jul-2016
^^^^^^^^^^^^^^^

See project work journal.
(GOMSS)

Refactored data_tools functions to get ONC ADCP data to separate request for data that launches search on ONC backend, and polling FTP server to find and download .mat file that results from search; doh! because I forgot to create the destination directory :-(
Backfilled model results pages re: last week's network issues.
Backfilled ONC ADCP data for east node from May 3-31.
Started working on production of ERDDAP dataset from ONC CTD data.
Found and fixed bug whereby ONC CTD data wasn't actually being converted to TEOS-10 reference salinity.
(SalishSea)


Tue 26-Jul-2016
^^^^^^^^^^^^^^^

Started backfilling ONC ADCP data for east node from April 15-30.
Figured out via Oceans2.0 that ONC East node ADCP was out of commission from 9apr through 30apr, explaining why download requests fail for that period.
Traced failure of Delta BBL node downloads to incorrect siteId values in matlab script from ONC; got 3 or 4 days of Apr data from that node before ONC service fell over, again.
Continued working on production of ERDDAP dataset from ONC CTD data.
Salish Sea team mtg; see whiteboard.
(SalishSea)

See project work journal.
(GOMSS)


Wed 27-Jul-2016
^^^^^^^^^^^^^^^

Physio appt; continue stretches: broomstick or wall crawl, towel, hands behind head, doorway chest stretch, flatten blades, then shoulders back on bike at stops, tubing arm pull in front of mirror, arm push lying on side, spread arms against tubing, working subscapular not trapezius, free the bird every 90 minutes at desk, and forearm raise against tubing under foot; add rows against tubing with focus on using subscapulars not neck, switch to rows when other resistance exercises fatigue me to to point of shoulder hunching. Focus on towel & hands behind head.

Discussed skookum RAID expansion with Charles and worked out plan to run parts of nowcast on salish today before data dump back to /results tomorrow.
Set up a nowcast environment on salish, edited nowcast.yaml to look at temporary /results mount at /skookum, and successfully ran get_NeahBay_ssh and grib_to_netcdf workers, but launch of upload_forcing for nowcast, ping_erddap, and make_forcing_links for nowcast-green failed.
Finished ONC ADCP Delta BBL April downloads; started May downloads by they time out on 1-May.
Manually ran download_weather worker for 18 forecast.
Sent email to Charles telling him to start data transfer to new RAID asap.
(SalishSea)

See project work journal.
(GOMSS)

Received email from Jackie with HVSI data changes to be loaded.
(sealinkd)


Thu 28-Jul-2016
^^^^^^^^^^^^^^^

Found that ONC ADCP Delta BBL 1-May download is failing due to search request error; that's due to no instrument deployed.
Started downloading ONC ADCP Delts BBL data for 2-31 May.
Got nowcast system back up and running on skookum and new 11Tb RAID 5 /results filesystem; hacked runNEMO worker on west.cloud to run 27jul16 nowcast.
(SalishSea)

See project work journal.
(GOMSS)

Decided that I don't have time this week to confidently load HVSI data changes; emailed Jackie to say I will do it after 15-Aug.
(sealinkd)

Attended SWC workout session by Susan on xarray and ERDDAP.

Registered for Basic Digital Photography Workflow course at Langara in Sep.


Fri 29-Jul-2016 & Sat 30-Jul-2016
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

**Vacation** - Travelled to Beaune; what a story!

Rebuild of 29-Jul nowcast-green results failed due to a weird version conflict issue for SalishSeaCmd pkg; 30-Jul run couldn't start and comparison & publish plots failed.
(SalishSea)



Sun 31-Jul-2016 through Thu 4-Aug-2016
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

**Vacation** - Cycletouring in Burgundy

Settled into apartment in Beaune.


Fri 5-Aug-2016
^^^^^^^^^^^^^^

**Vacation** - Beaune

Fixed bug in salishsea combine whereby per-processor results files, and lots of other netcdf4 files were being unnecessarily deflated.
Susan ran nowcast-green catch-up runs on orcinus.
(SalishSea)


Sat 6-Aug-2016
^^^^^^^^^^^^^^

**Vacation** - Beaune

Manually ran make_plots, make_pages, sphinx_build & rsync_to_web workers to catch up figures and pages that were missed due to 30-Jul nowcast-green failure.
Opened ticket to restart ERDDAP to resolve 500/javascript errors reported by Ben.
(SalishSea)


Sun 7-Aug-2016
^^^^^^^^^^^^^^

**Vacation** - Beaune

Charles restarted ERDDAP.
(SalishSea)


Week 32
-------

Mon 9-Aug-2016
^^^^^^^^^^^^^^

**Vacation** - Beaune

Started dev of Pyramid app for salishsea_site.
(SalishSea)


Thu 11-Aug-2016
^^^^^^^^^^^^^^

**Vacation** - Beaune to Paris

Continued dev of Pyramid app for salishsea_site.
(SalishSea)


Sat 13-Aug-2016
^^^^^^^^^^^^^^

**Vacation** - Paris to Vancouver

Continued dev of Pyramid app for salishsea_site; finally figured out that reverse proxy was being blocked by Apache detault site still enabled.
(SalishSea)


Sun 14-Aug-2016
^^^^^^^^^^^^^^

Created salishsea_site Pyramid app in pyramid branch of salishsea_site repo.
(SalishSea)


Week 33
-------

Mon 15-Aug-2016
^^^^^^^^^^^^^^^

ECget had timeouts trying to get 14Aug river flow data; faked values assuming persistence, ran make_runoff_file manually, and upload_forcing to restart automation for forecast2.
Set up Sentry project for Salish Sea Nowcast system and site web app.
Prepared salishsea-site-env conda environment on skookum; need to set up circus to run the app before opening the ticket to add the reverse proxy.
Started downloading ONC ADCP central node data for 1-30 June; timeout on 21; restarted and finished; started east node.
Continued work on production of 15min averaged ONC CTD datasets for ERDDAP.
Discussed ADCP & other ONC data w/ Rich.
(SalishSea)

Summer student seminars including James at Phys Ocgy seminar.

Coffee w/ Julie.


Tue 16-Aug-2016
^^^^^^^^^^^^^^^

Restarted downloading ONC ADCP east node data for 1-30 June after overnight timeout on 11.
Finished downloading ONC ADCP east node data for 1-30 June; started downloading Delta BBL node (aka ddl) June data.
Continued work on production of 15min averaged ONC CTD datasets for ERDDAP; succeeded in publishing proof of concept dataset.
(SalishSea)

Salish Sea team mtg; see whiteboard.


Wed 17-Aug-2016
^^^^^^^^^^^^^^^

Physio appt. Need to relearn the skill of keeping my shoulder down and back. Focus on band resistance exercises, to the side, then up when skill returns.

Took Gunnars to Speed Theory for right shifter G-strings replacement.

Dentist appt to fill small cavity between lower right molars.

Started downloading ONC ADCP central node data for 1-31 July.
(SalishSea)

See project work journal.
(GOMSS)


Thu 18-Aug-2016
^^^^^^^^^^^^^^^

Discovered that EC research forecast model product has not been updated since 9-Aug.
ONC ADCP download failed for 28-Jul onward, reporting no deployment.
Started downloading east node July data; like central, it failed for 28-Jul onward, reporting no deployment.
Started downloading Delta BBL (aka ddl) node July data.
(SalishSea)

See project work journal.
(GOMSS)


Fri 19-Aug-2016
^^^^^^^^^^^^^^^

Reviewed Ben's nc_tools & viz_tools and James's geo_tools code to prep for today's MOAD software session on library code.
(MOAD)

Pulled and updated NEMO-3.6-code on niko.
Merged NEMO-3.6-code into NEMO-3.6-mirror-merge at NEMO-3.6r6036 tag on niko and pushed to NEMO-3.6-code on Bitbucket; emailed group and updated whiteboard re: merge.
Deleted NEMO-3.6-r6036 repo from Bitbucket.
Pulled changesets 6039 through 6204 into NEMO-3.6-hg-mirror on salish.
Merged NEMO-3.6-hg-mirror into NEMO-3.6-mirror-merge on niko.
Tagged NEMO-3.6-r6204 in NEMO-3.6-mirror-merge and pushed to new NEMO-3.6-r6204 repo on Bitbucket for Susan & Elise to use for merge-comparison test.
Traced the ERDDAP issue that Nancy, Ben and I have been discussing down to a timeout on the Apache proxy in front of ERDDAP; opened a ticket for Charles to double ProxyPass timeout value to 600s.
Helped James get output set up for short test runs on jasper.
Skimmed XIOS2 docs PDF.
Downloaded ONC-ADCP central and east node data for Aug to the 18th.
(SalishSea)


Sat 20-Aug-2016
^^^^^^^^^^^^^^^

Reviewed and improved .condarc file on kudu.

Added pynco to sphinx-build environment for readthedocs and cleaned up docstring issued to get salishsea_tools API docs building again.
Pulled NEMO-3.6-code svn r6036 into nowcast-sys/ on salish and did a clean build.
Downloaded ONC-ADCP Delta BBL node data for Aug to the 18th; almost "real-time" now!
(SalishSea)

Watched Gord Downie's final concert with The Tragically Hip broadcast on the CBC.


Sun 21-Aug-2016
^^^^^^^^^^^^^^^

Add 2000 km brevet distance.
Added pyramid-crow to monitor exceptions on Sentry and integrated Sentry project with Bitbucket repo to enable issue creation; tested with manual replication of populaires/VicPop AttributeError from log; see issue #22.
Changed deployment on Webfaction to randopony_prod with Pyramid 1.7.3 and Mercurial clone from Bitbucket.
Had to downgrade colander to 1.2; see issue #21.
(RandoPony)

Loaded 27-Jul indicator list version of spreadsheet from Jackie.
(sealinkd)


Week 34
-------

Mon 22-Aug-2016
^^^^^^^^^^^^^^^

Reviewed changes in 2016.06 shell & Python lessons release.
Met w/ Nancy & Karina to plan 20/21-Sep EOAS workshop.
(SWC)

Morphed ADCP data download code into daily per node form to move it toward a cron job.
Ran GETDEPL on central node data to 19-Aug; had forgotten how horribly slow it is, loading each day's raw data file (partly because there at least 2 files per day from Muriel's automation).
Fixed a typo in GETDEPL_fun re: deployment dates.
GETDEPL reported corrupted files for 2016-05-07, 2016-05-13; re-downloaded
Started work on raw ADCP data download script in Python.
(SalishSea)

Phys Ocgy seminars by summer student Vahid Dehghanniri re: gravity currents in the bottom of the SoG, and Idalia about her research plan for upwelling in Mackenzie Canyon.


Tue 23-Aug-2016
^^^^^^^^^^^^^^^

See project work journal.
(GOMSS)

Terminated west.cloud instances 14, 16 & 17 at Eric Kolb's request due to memory issues on the hypervisor that they were running on; launched new instances and got nowcast started at about 14:05.
Continued running GETDEPL for central node ADCP data; 2016-05-07 again reported corrupt (after re-download & acceptance yesterday) so deleted the file.
Lots more corrupted central node ADCP files (see notebook); deleted them.
Deleted all duplicate central node raw ADCP files to try to speed up GETDEPL.
Got GETDEPL to complete on central node ADCP data, tuned rotation angle via LTIM, and released data to 22-Aug.
(SalishSea)

Salish Sea team mtg; see whiteboard.


Wed 24-Aug-2016
^^^^^^^^^^^^^^^

Debugged ONC ADCP data download cron job.
(SalishSea)

See project work journal.
(GOMSS)

Got new Rancilio Sylvia M espresso machine :-)


Thu 25-Aug-2016
^^^^^^^^^^^^^^^

See project work journal.
(GOMSS)

Got salishsea-site pyramid branch running under circus process mgr and chaussette WSGI server on VM.
Confirmed that reverse proxies to site app and erddap can be used together; put erddap proxy (longest root URL) first.
Helped Elise get anaconda on char updated to Python 3.5.
Read Drakkar slidedeck on TEOS-10 and NEMO.
(SalishSea)

Participated in SWC workout lead by Susan on matlab from python.


Fri 26-Aug-2016
^^^^^^^^^^^^^^^

See project work journal.
(GOMSS)

Traveled from home to Heriot Bay Inn for JRA's 90th bday wknd.


Sat 27-Aug-2016
^^^^^^^^^^^^^^^

See project work journal.
(GOMSS)

Manually started nowcast run after west.cloud network maintenance.
(SalishSea)


Sun 28-Aug-2016
^^^^^^^^^^^^^^^

Traveled home from Heriot Bay Inn after JRA's 90th bday wknd.

See project work journal.
(GOMSS)


Week 35
-------

Mon 29-Aug-2016
^^^^^^^^^^^^^^^

Worked w/ Dominik@EC to backfill GEM 2.5km research model products for day missed when his automation failed on 10-Aug.
(SalishSea)

Created 2016-09-20-ubc workshop repo and site.
Met w/ Nancy & Karina to plan 20/21-Sep EOAS workshop.
(SWC)


Tue 30-Aug-2016
^^^^^^^^^^^^^^^

River discharge downloads failed due to timeout on wateroffice site; patched files with persistence values from 29-Aug.
(SalishSea)

See project work journal.
(GOMSS)


Wed 31-Aug-2016
^^^^^^^^^^^^^^^

River discharge downloads failed due to timeout on wateroffice site; patched files with persistence values from 29-Aug.
Salish Sea team mtg; see whiteboard.
Continued dev of ONC CTD data ERDDAP dataset XML description.
(SalishSea)

Scheduled site visit for server boot failure for Thu 8-Sep.
(Nordion)

Used apt to install jekyll on niko (ruby & gem were already installed as part of base OS packages).
Buffed 2016-09-20-ubc workshop repo and site.
Created hg-novice-2016-09-20-ubc lesson repo & site.
(SWC)


Thu 1-Sep-2016
^^^^^^^^^^^^^^

See project work journal.
(GOMSS)

Wrote spec for new drivetrain for Shadowfax and discussed it with Ed@Mighty.


Fri 2-Sep-2016
^^^^^^^^^^^^^^

Code review of canyon_tools.readout_tools.py.
(MOAD)

Continued dev of ONC CTD data ERDDAP dataset XML description.
Helped James make storage decisions about his auto-generated notebooks from the SMELT sensitivity analysis.
Wrap up mtg w/ James & Elise, then drinks at The Point.
(SalishSea)


September
=========

Week 36
-------

Mon 5-Sep-2016
^^^^^^^^^^^^^^

**Statutory Holiday** - Labour Day

EC GEM2.5 research products missing from FTP site since 4sep.
Created XIOS-ARCH repo to hold XIOS arch files publicly and separately from XIOS code.
Added xios-2.0 branch to XIOS-ARCH repo with mods for building XIOS-2.0 on orcinus.
Updated salish & orcinus quick-start docs re: use of XIOS-ARCH files.
(SalishSea)


Tue 6-Sep-2016
^^^^^^^^^^^^^^

See project work journal.
(GOMSS)

Salish Sea team mtg; see whiteboard.
Backfilled res_y2016m09d04.nc & res_y2016m09d05.nc.
Continued dev of ONC CTD data ERDDAP dataset XML description.
(SalishSea)


Wed 7-Sep-2016
^^^^^^^^^^^^^^

Physio appt; continue towel stretches for range of motion & arm spread against resistance.

Pulled conservative temperature and reference salinity boundary condition files into nowcast-sys/NEMO-forcing for nowcast-green to use & updated nowcast-green events table.
Backfilled res_y2016m09d06.nc.
Changed get_res.sh script to include 024 file that Dominik added on 05sep16.
(SalishSea)

See project work journal.
(GOMSS)


Thu 8-Sep-2016
^^^^^^^^^^^^^^

Nordion site visit re: isoinfo server boot failure; see work notes.
(Nordion)

Continued dev of ONC CTD data ERDDAP dataset XML description.
(SalishSea)

Code review of Nancy's grid_tools module & notebook re: time-varying water column factors in NEMO.
(MOAD)

Helped Melanie upgrade to Anaconda 3 on smelt & her laptop.
Split Cindy's analysis notebooks out of the 2Gb limited analysis repo into a new analysis-cindy repo.
(GEOTRACES)

Attended the dept. colloquium research carnival, including watching the launch of the OSIRIS-REX mission to Bennu on which Catherine Johnson is an instrument PI.


Fri 9-Sep-2016
^^^^^^^^^^^^^^

Notified Dominik@EC that GEM2.5 research products failed on 8sep; he fixed the issue.
Backfilled res_y2016m09d08.nc and res_y2016m09d09.nc.
Finalized ONC CTD data notebook w/ working ERDDAP XML fragment generation code.
Started development of get_onc_ctd worker.
Updated salishsea-site-env on skookum.
Cloned salishsea-site repo into /results/nowcast-sys/ on skookum.
Tried to get salishsea-site pyramid app running on skookum but got hung up on an invalid host/port issue.
Worked on testing get_onc_ctd worker in nowcast-vm.
(SalishSea)

Helped Melanie get SalishSeaTools package installed in her anaconda env.
(GEOTRACES)

See project work journal.
(GOMSS)


Sat 10-Sep-2016
^^^^^^^^^^^^^^^

Discovered that ERDAP requires a consistent time-base among all files in a dataset; so ONC CTD data files must be rebased; turns out to be easily done via the encoding arg of Dataset.to_netcdf().
Ran get_onc_ctd SCVIP worker for all of 2016 to date.
Integrated get_onc_ctd worker into automation to run after 06 weather download.
Added SEVIP to get_onc_ctd and started backfill running it.
(SalishSea)

See project work journal.
(GOMSS)


Sun 11-Sep-2016
^^^^^^^^^^^^^^^

get_onc_ctd worker ran in automation without problems!
Continued backfill runs of get_onc_ctd SEVIP but things went wrong in May w/ >>900 samples per aggregation period
(SalishSea)

See project work journal.
(GOMSS)


Week 37
-------

Mon 12-Sep-2016
^^^^^^^^^^^^^^^

See project work journal.
(GOMSS)

Helped Melanie get seawater package installed in her anaconda env.
Created file maps to migrate Melanie, Susan and Kyle to separate analysis repos.
(GEOTRACES)

Got salishsea-site pyramid app running on skookum; Friday's invalid host/port issue seems to have just disappeared.
Created ticket requesting Charles add reverse proxy to apache config on skookum.
Proxy works when I run app via pserve, but not when I run it via circus.
Charles gave me sudo on skookum so that I can continue testing.
On the bus in the evening learned of the change in config that waitress 1.0 brought.
Started creating file map to move SalishSeaNowcast package from tools repo into its own repo.
(SalishSea)

Phys Ocgy seminar research carnival.

Started creation of spreadsheet version of EOAS timesheet.

Zack Powell visiting.

Week 1 of Digital Photography Workflow course at Langara; intro and greyscale histograms.


Tue 13-Sep-2016
^^^^^^^^^^^^^^^

See project work journal.
(GOMSS)

Tried new waitress listen directive for salishsea-site app on skookum but no magic; need to experiment more in VM env.
Worked on ONC CTD data; discovered NaN T&S produce NaN sample counts and that semi-borks ERDDAP; also discovered that xarray can't load tables - use pandas.read_csv() with crafted URL.
Salish Sea team mtg; see whiteboard.
(SalishSea)

Created file maps for analysis-melanie, analysis-kyle & analysis-susan.
Helped Melanie start cloning analysis repo - hours!
Split Kyle's analysis notebooks out of the 2Gb limited analysis repo into a new analysis-kyle repo.
(GEOTRACES)

Got quoted in ONC press release about new CANARIE funding: http://www.oceannetworks.ca/canarie-funding-supports-new-tools-big-data


Wed 14-Sep-2016
^^^^^^^^^^^^^^^

See project work journal.
(GOMSS)

Staff welcome back bbq.

Code review session on Cindy's Hovmeuller diagram transect code.
(MOAD)

Split Melanie's analysis notebooks out of the 2Gb limited analysis repo into a new analysis-melanie repo.
Helped Melanie w/ Python data structures.
(GEOTRACES)

Added workshop intro slides; helped Kelly get kDiff3 installed on Mac.
Prepped etherpad.
(swc)


Thu 15-Sep-2016
^^^^^^^^^^^^^^^

See project work journal.
(GOMSS)

EOAS colloquium by Chuck Kosman & Tom Yrex re: new EOAS web site, email system, and move to Active Directory auth for new services.


Fri 16-Sep-2016
^^^^^^^^^^^^^^^

forecast2/15sep16 failed due to loss of shared storage connection on 17 or 18 VMs; reconnected in time for nowcast/16sep16.
Removed James of nowcast email notifications list and restarted manager.
(SalishSea)

Registered HST/GST account with CRA.
Invoiced Nordion for 8-Sep site visit.

See project work journal.
(GOMSS)

Shadowfax to Mighty for new drivetrain.


Sat 17-Sep-2016
^^^^^^^^^^^^^^^

Travel to Parksville to move Forth.

Finished creation of spreadsheet version of EOAS timesheet.


Sun 18-Sep-2016
^^^^^^^^^^^^^^^

Added extra content (especially workshop slide decks) to shell and hg lessons.
Had to re-generate lots of PNG images (for hg lesson in particular) to use in slide decks.
(swc)


Week 38
-------

Mon 19-Sep-2016
^^^^^^^^^^^^^^^

Continued prep for workshop.
Met w/ helpers and co-instructors.
(swc)

Restarted ERDDAP server with my new sudo powers when Nancy reported it was returning null pointer errors.
Investigated ONC CTD datasets sample count NaNs and prototyped a solution.
(SalishSea)

Presented myself and ERDDAP at week 2 of Phys Ocgy research carnival.

Week 2 of Digital Photography Workflow course at Langara.


Tue 20-Sep-2016
^^^^^^^^^^^^^^^

EOAS 4th annual SWC workshop
(swc)


Wed 21-Sep-2016
^^^^^^^^^^^^^^^

EOAS 4th annual SWC workshop - best ever!
(swc)


Thu 22-Sep-2016
^^^^^^^^^^^^^^^

Emailed Greg re: workshop & Idalia's app for instructor training.
Added my notes to attendees list.
(swc)

See project work journal.
(GOMSS)


Fri 23-Sep-2016
^^^^^^^^^^^^^^^

Sent invoice reminder.
(Nordion)

See project work journal.
(GOMSS)


Sat 24-Sep-2016
^^^^^^^^^^^^^^^

River discharge downloads failed on salish, so forecast2 run failed; salish and /data/ are unreachable.
Finished file map to move SalishSeaNowcast package from tools repo into its own repo, and created the repo.
Set up SalishSea-Nowcast project on readthedocs for SalishSeaNowcast package.
Got nowcast system running again after loss of access to /data and salish restart; re-ran nowcast-green/23sep16 that was incomplete due to salish failure.
Cleaned up SalishSeaNowcast README, hg tags, package names, namespace names, etc.
Got salishsea-site pyramid app working in skookum by downgrading waitress to 0.9.0 from 1.0 because chassette doesn't support the changes in 1.0.
(SalishSea)


Sun 25-Sep-2016
^^^^^^^^^^^^^^^

Ran nowcast-green/24sep16 that was delayed due to recent salish failure.
Re-ran 23sep16 comparison plots that couldn't run until nowcast-green/23sep16 finiished.
Started migrating SalishSeaNowcast issues from tools repo tracker to SalishSeaNowcast tracker.
Added nowcast3-env provisioning to nowcast-vm.
Got docs to build in SalishSeaNowcast NEMO_Nowacst branch.
Added enough config and an empty next_workers module so that system could be launched via circus in the VM.
Started updating docs in NEMO_Nowcast branch.
(SalishSea)


Week 39
-------

Mon 26-Sep-2016
^^^^^^^^^^^^^^^
Backfilled 16-20 & 25-26 Sep GEM2.5km research forecast downloads.
Set up SalishSeaNowcast NEMO_Nowcast dev env on niko.
Started downloading ONC-CTD data again in a tmux session on skookum (working backward in time) to deal with the NaN sample count issue.
(SalishSea)

Migrated EOAS email to Exchange and set up Gmail client on my phone to access it.
Set up Thunderbird on niko to access Exchange.

Week 3 of Digital Photography Workflow course at Langara; ISO noise, JPEG compression, sorting, technical adjustments, cropping.


Tue 27-Sep-2016
^^^^^^^^^^^^^^^

Enable folder syncing between Exchange server and Thunderbird on niko.
Started folderizing EOAS email via Thunderbird on niko.

Created analysis-tereza repo.
Continued updating docs in NEMO_Nowcast branch.
Set up PyCharm project & VM for SalishSeaNowcast on niko.
Salish Sea team mtg; see whiteboard; Tereza joined the team.
Continued downloading ONC-CTD data again in a tmux session on skookum (working backward in time) to deal with the NaN sample count issue.
(SalishSea)


Wed 28-Sep-2016
^^^^^^^^^^^^^^^

Some EAOS machines and sites disappeared for several hours due to an DNS issue.

Discussed approach to ONC re: west.cloud resources w/ Susan and helped her write the email.
Continued downloading ONC-CTD data again in a tmux session on skookum (working backward in time) to deal with the NaN sample count issue.
Manually re-ran forecast2 publish plots that failed (perhaps due to DNS issue?).
(SalishSea)

See project work journal.
(GOMSS)


Thu 29-Sep-2016
^^^^^^^^^^^^^^^

Set up Thunderbird for EOAS mail on kudu.
Emailed Chuck@EOAS about learning Git.

Reviewed ONC-CTD central node data back to 2014-09-01; the feed transitions from per-minute to per-second on 2015-09-01.
Continued downloading ONC-CTD east node data; big gap for most of Apr-2016, and feed transitions from per-minute to per-second on 2016-05-04.
Started porting download_weather worker into NEMO_Nowcast framework; profiling revealed that it is >3x faster than old worker (for off-peak downloads).
(SalishSea)

Used Firefox dev tools to profile Maps page loading to investigate Jackie's report of times as long as 10 minutes (!!):
Production server:
  * 1st load: 43 requests, 1249.31 kb, 71.71 s
    * all_capitals: 17.37 kb transferred = 251.04 kb uncompressed, 68542 ms
    * css & js assets all cached
    * a few mapbox tiles cached, the rest ranged from 41 ms to 519 ms, mostly 100-200 ms
  * awesome bar refresh: 51 requests, 1104.83 kb, 74.91 s
    * all_capitals: 17.57 kb transferred = 251.04 kb uncompressed, 71155 ms
    * css & js assets requested; all returned 304
Dev VM:
  * 1st load: 37 requests, 1272.57 kb, 6.83 s
    * all_capitals: 17.66 kb transferred = 250.05 kb uncompressed, 3804 ms
    * css & js assets partially cached
    * a few mapbox tiles cached, the rest ranged from 58 ms to 212 ms, mostly <100 ms
  * awesome bar refresh: 53 requests, 870.56 kb, 6.84 s
    * all_capitals: 17.59 kb transferred = 250.05 kb uncompressed, 3822 ms
    * css & js assets requested; all returned 304
Production server:
  * Start -> Maps:
    * restarted postgres, nginx, and app
    * 16 requests, 752.22 kb 72.41 s
    * all_capitals: 17.38 kb transferred = 251.04 kb uncompressed, 70184 ms
    * everything else was cached
  * reload Maps via awesome bar refresh while watching top:
    * lots of time in pserve, some in postgres
    * 51 requests, 1570.07 kb, 76.86 s
    * all_capitals: 17.51 kb transferred = 251.04 kb uncompressed, 73690 ms
    * css & js assets requested; all returned 304
Queries:
  * Start 10
  * Maps 970
  * Analysis 374
  * Compare 222
  * Profile 88
(SealinkD)

See project work journal.
(GOMSS)


Fri 30-Sep-2016
^^^^^^^^^^^^^^^

Continued profiling new download_weather worker; speed-up is mostly due to session reuse.
Tested new download_weather worker in combat for 12 forecast; scheduled launch failed, manual run gets stuck in back-off and retry loop after awaited download succeeds; found and fixed the bug during 18 forecast download, which was successfully launched by scheduler.
(SalishSea)

Helped Elise sort out how to use f2py3 to build Pyton 3 wrappers for fortran modules.
Tried to help Tereza build XIOS, but there is somthing wrong re: tools/archive.


Sat 1-Oct-2016
^^^^^^^^^^^^^^

Set up unit test environment on nowcast-vm for SalishSeaNowcast dev.
Manually re-ran make_plots comparison for 29sep nowcast & publish for 30sep nowcast;
Susan started to investigate Sandheads wind observations XML parsing issue and confirmed that obs are available.
Susan ran 30sep NEMO-3.6 nowcast blue (physics only; rc1 for nowcast production upgrade) on salish using 3x5+1 MPI decomposition; 2h1m for computations, 4m for restart rebuild, netcdf4 deflation, and results clean-up.
Started trying to test NEMO-3.6 nowcast blue on west.cloud:
* struggled with clone repos on to sshfs-mounted MEOPAR filesystem; way too slow
* cloned repos into /mnt/MEOPAR, then stopped until tomorrow morning
* built XIOS-1.0r
* built NEMO-3.6r
* used 8x17+1 MPI decomposition
*
Tried to replicate Tereza's problems w/ building XIOS, but can't; okay on salish, no mpicc on oven
Fixed paths in working on salish XIOS build docs.
Did lots of maintenance on salishsea static site; added Tereza, fixed broken & redirect links, added citation for Soontiens & Allen mixing paper.
Cherry-picked changesets from tools repo into SalishSeaNowcast repo with `hg export -R ../tools -r | hg import -p2 -e -` to minimize transcription and preserve commit metadata.
Updated unit tests for download_weather worker in NEMO_Nowcast branch
Added unit tests for next_workers module.
Started documenting and building nemo_nowcast-env on skookum and conda went weird with installation problems.
download_weather 00 worker failed due to messed up nowcast-env; 1st clue that everything had come crashing down.
Deleted anaconda and miniconda3 from $HOME, and all envs in /results/nowcast-sys.
Re-installed minconda3, recreated /results/nowcast-sys/nowacst-env, started message broker and manager, and manually launched download_weather 00 worker.
(SalishSea)


Sun 2-Oct-2016
^^^^^^^^^^^^^^

Continued trying to test NEMO-3.6 nowcast blue on west.cloud:
* built XIOS-1.0 at svn r648 in /mnt/MEOPAR/
* built NEMO-3.6 at svn r6036 in /mnt/MEOPAR/
* copied XIOS-1.0 and NEMO-3.6 dirs to sshfs-mounted $HOME/MEOPAR
* un-mounted and re-mounted $HOME/MEOPAR sshfs on all nodes
* used 8x17+1 MPI decomposition
* after lots of namelist and run script thrashing, got the run going, ETA 1h
* xios server runs on node 0 along with 8 nemo processes
* got xios to run by itself on node 17 with: ${MPIRUN} -np 136 ./nemo.exe : -host 192.168.1.79 -np 1 xios_server.exe
* other things to try:
  * --bind-to-core
Discovered how many conda envs were in use as things failed through the night and this morning:
* ecget
* onc_adcp
Created new ecget conda env for salish cron jobs to use and confirmed that it works by manually running Fraser and Englishman cron scripts to get 1oct discharges.
Manually re-ran workers:
* make_runoff_file
* get_onc_ctd for SCVIP & SEVIP nodes
* corrected spelling of ONC_USER_TOKEN envvar and restarted manager
* salishsea gather for nowcast-green/01oct16
* download_results for forecast/01oct16
Finished SalishSeaNowcast environment set-up on skookum and wrote deployment docs.
Started porting grib_to_netcdf worker into NEMO_Nowcast framework.
(SalishSea)


October
=======

Week 40
-------

Mon 3-Oct-2016
^^^^^^^^^^^^^^

Applied network interface setting recommended by Eric@uvic in Apr-2015 to west.cloud nowcast VMs:
/sbin/ethtool -K eth0 tso on ufo on gso on gro on sg on
Continued porting grib_to_netcdf worker into NEMO_Nowcast framework.
Got 12h nowacst-blue run to complete on west.cloud; 7*18+1, 5e6 XIOS buffer, no gather, 27m13s.
Helped Susan get nowcast-green running after change to conservative temperature for rivers runoff.
(SalishSea)

Participated in workouts planning mtg.
(swc)

Phys ocgy seminar by Dan Robb on meshless Lagrangian modeling for ice jams & debris flows.

Mtg w/ Stephanie & Jackie; discussed  data updates, Maps page load time variations, scaling, future development.
Agreed to data update in January, data gathering by SCARP for me to email UBC with re: loading time.
(sealinkd)

Week 4 of Digital Photography Workflow course at Langara; still-life studio shoot.


Tue 4-Oct-2016
^^^^^^^^^^^^^^

Continued porting grib_to_netcdf worker into NEMO_Nowcast framework.
Got 24h nowcast-blue run to complete on west.cloud; 7*18+1, 2.5e7 XIOS buffer, no gather, 51m56s, ~8Gb memory.
Helped Terza get NEMO-3.4 GYRE running on halibut.
Salish Sea team mtg; see whiteboard.
Started 24h nowcast-blue run; 7*18+1, 3.75e7 XIOS buffer; memory looks like ~10Gb.
(SalishSea)

See project work journal.
(GOMSS)


Wed 5-Oct-2016
^^^^^^^^^^^^^^

Analyzed 24h nowcast-blue run; 7*18+1, 3.75e7 XIOS buffer; no gather; 49m25s, no improvement in XIOS performance ratio vs. 2.5e7 buffer.
Accept system config dict as argument to ``next_workers.after_*()`` functions.
Started benchmarking rebuild_nemo for restart files, and ``ncks -4 -L4`` w/ copy to another directory for results and restart files on west.cloud; see notebook & Google spreadsheet.
(SalishSea)

See project work journal.
(GOMSS)


Thu 6-Oct-2016
^^^^^^^^^^^^^^

Added "slow loading time" notice banner to site.
Set up UptimeRobot monitor for Maps page every 15 minutes, and created public monitoring page (new feature today) that I shared with Jackie & Stephanie.
(sealinkd)

See project work journal.
(GOMSS)

Finished benchmarking ``ncks -4 -L4`` in-place for results and restart files on west.cloud; see notebook & Google spreadsheet.
(SalishSea)


Fri 7-Oct-2016
^^^^^^^^^^^^^^

See project work journal.
(GOMSS)

Researched how to get time-stamped log message out of salishsea command processor; --log-file should do it.
Re-ran nowcast-blue/01oct16 on west.cloud to get a new set of raw results & restart files to use for profiling salishsea gather/combine.
Running salishsea gather with --log-file allowed me to confirm that it rebuilds and deflates with timings similar to my benchmark measurements; so either it behaves differently when run in a subprocess, or the holdup happens after deflation, in deletion of symlinks, or deletion of temporary working directory (which is not happening).
Finished porting grib_to_netcdf worker into NEMO_Nowcast framework; got logging sorted out, got wgrib2 executable from skookum to work on dev VM, and used a logging handler config to define the storage location for the weather forecast checking image.
Started creating a new process flow diagram and linked it into the docs.
Moved old unit test module to v2_tests so that NEMO_Nowcast-based system can be tested as a package.
Ported make_runoff_file worker into NEMO_Nowcast framework.
(SalishSea)


Sat 8-Oct-2016
^^^^^^^^^^^^^^

Travel to Parksville for Thanksgiving and to empty Forth


Sun 9-Oct-2016
^^^^^^^^^^^^^^

In Parksville for Thanksgiving and to empty Forth

Ported get_NeahBay_ssh worker into NEMO_Nowcast framework.
(SalishSea)


Week 41
-------

Mon 10-Oct-2016
^^^^^^^^^^^^^^^

**Thanksgiving Day** - traveled home form Parksville

Expanded nowcast process flow docs.
Started porting upload_forcing and make_forcing_links workers to NEMO_Nowcast framework.
(SalishSea)


Tue 11-Oct-2016
^^^^^^^^^^^^^^^

Participated in Westgrid townhall mtg; news about object storage, new systems, decommissioning, and RAC process; overall rather unsatisfying.
Finished porting upload_forcing and make_forcing_links workers to NEMO_Nowcast framework.
Salish Sea team mtg; see whiteboard.
Draft response to Ryan@ONC re: Empower project user stories, and sent it to Susan for buffing.
(SalishSea)

Listened to SWC lesson maintainers video call.
(swc)


Wed 12-Oct-2016
^^^^^^^^^^^^^^^

Physio appt.
Replaced Keen boots with broken sole.
Shadowfax is still not ready.

Handled off-line ONC SCVIP node in nowcast automation.
Sent response to Ryan@ONC re: Empower project user stories.
Manually ran make_plots and make_stie_page workers to catch-up nowcast comparison and publish pages due to SCVIP node issue; Sandheads winds issue appears to have been resolved.
(SalishSea)

See project work journal.
(GOMSS)


Thu 13-Oct-2016
^^^^^^^^^^^^^^^

Added launch of make_forcing_links for nowcast-green from grib_to_netcdf to next_workers.
Started porting run_NEMO36 worker to NEMO_Nowcast framework as run_NEMO.
Set up /results/nowcast-sys/runs dir on skookum for shift to NEMO_Nowcast framework.
Started setting up MEOPAR/nowcast-sys/runs dir on west.cloud for shift to NEMO_Nowcast framework.
(SalishSea)


Fri 14-Oct-2016
^^^^^^^^^^^^^^^

Finished porting run_NEMO36 worker to NEMO_Nowcast framework as run_NEMO for nowcast-green runs.
Modified run_NEMO for nowcast & forecast runs on west.cloud.
Finished setting up MEOPAR/nowcast-sys/runs dir and nemo_nowcast-env on west.cloud for shift to NEMO_Nowcast framework.
Ported watch_NEMO worker to NEMO_Nowcast framework.
**1st storm surge alert of the season**
Fixed bug in make_feeds worker re: too many args in _generate_feed_entry() call.
Re-ran nowcast-green run that failed due to salish loosing network connectivity again.
(SalishSea)


Sat 15-Oct-2016
^^^^^^^^^^^^^^^

Started porting download_results worker to NEMO_Nowcast framework.
Disabled GEM2.5/research/get_res.cron.sh job.
1st production test of SalishSeaNowcast package:
* Disabled weather download cron jobs
* Stopped v2 manager & message broker processes on skookum
* Changed v3 config on skookum and west.cloud to use skookum.eos.ubc.ca as zmq server
* Changed v3 config on skookum and west.cloud to use zmq ports 5554 (manager) and 5555 (workers)
* Restarted message_broker, manager, and scheduler on skookum
* Uploaded nowcast-green/14oct16/namelist_cfg to nowcast/14oct16/ on west.cloud
* Uplodaed nowcast-green/14oct16/restart to nowcast/14oct16/ on west.cloud
* scheduler failed to launch download_weather worker; ran in manually
* config key spelling bug in get_NeahBay_ssh worker; fixed and re-ran manually
* config lookup missing forcing level in upload_forcing worker; fixed and re-ran manually
* ssh launch of run_NEMO worker on west.cloud lacks NOWACST_LOGS and NOWCAST_ENV envvars
* NEMO_Nowcast manager didn't know how to handle log and need messages; hacked it in
* getting coordinates from config instead of implicitly from forcing config in run description doesn't work across hosts
* getting bathymetry from "run types" config might not be appropriate for multi-host ops
(SalishSea)


Sun 16-Oct-2016
^^^^^^^^^^^^^^^

Finished porting download_results worker to NEMO_Nowcast framework.
Worked on resolving issues identified during yesterday's production testing, and getting automation fully operational.
(SalishSea)


Week 42
-------

Mon 17-Oct-2016
^^^^^^^^^^^^^^^

Woke up to find that overnight nowcast automation **all just worked** :-)
Michael Dunphy joined MOAD.
Fixed calculation of restart timestep for forecast2 runs prep in nowcast.
Manually ran v2 make_plots publish worker for forecast & forecast2 15 & 16 oct, and research for nowcast for same days.
Manually ran v2 make_site_page worker for nowcast, forecast & forecast2, publish, research & comparison pages for 15 & 16 oct.
Manually ran sphinx_build & rsync_to_web workers to push 15 & 16 oct figures pages to web.
Manually ran post-processing workers for 17oct runs.
Update nowcast results page with notes about move to NEMO-3.6.
Moved NEMO-3.6-code repo forward to r6204:
* Pulled changesets to 395:7914a357d7b3 from NEMO-3.6-r6204 on Bitbucket; that left behind Susan XIOS2 changes because we found that XIOS2 is slower than XIOS1
* Merged NEMO-3.6-code changes since NEMO-3.6-r6204 tag into NEMO-3.6-mirror-merge at on niko, tagged it as NEMO-3.6r6204-ubc, and pushed to NEMO-3.6-code on Bitbucket
Started moving NEMO-3.6-code repo forward to r6459
* Pulled changesets 6205 through 6287 into NEMO-3.6-hg-mirror on salish.
(SalishSea)

Workout session on publication figures by Ben & Nancy.
(swc)

Phys ocgy seminar by Melanie about Arctic circulation from Th-230 isotope sampling.

Week 5 of Digital Photography Workflow course at Langara; processing images from week 4 still-life studio shoot; sync-ing settings acrosss groups of images.


Tue 18-Oct-2016
^^^^^^^^^^^^^^^

See project work journal.
(GOMSS)

Continued moving NEMO-3.6-code repo forward to r6459
* Pulled changesets 6303 through 6459 into NEMO-3.6-hg-mirror on salish.
* Merged NEMO-3.6-hg-mirror into NEMO-3.6-mirror-merge on niko.
* Tagged NEMO-3.6-r6459 in NEMO-3.6-mirror-merge and pushed to new NEMO-3.6-r6459 repo on Bitbucket for Elise to use for merge-comparison test.
Got salishsea site Pyramid app running again, and added a quickly hacked view to it to render files from the /results/nowcast-sys/logs/nowcast/ directory.
Salish Sea team mtg; see whiteboard.
Paired with Susan on another try to resolve the run_NEMO worker restart timestep calculation bug for forecast2 runs.
(SalishSea)


Wed 19-Oct-2016
^^^^^^^^^^^^^^^

Pulled the run_NEMO worker restart timestep calculation bug for forecast2 runs bug-fixes onto west.cloud and re-ran the forecast2/18oct16 run.
Experimented with stdout/stderr redirection in qsub-ed SalishSeaNEMO.sh script on salish for nowcat-green; seems to work well.
Updated NEMO_Nowcast pkg on skookum to v1.2 re: manager need & log message handling.
(SalishSea)

See project work journal.
(GOMSS)


Thu 20-Oct-2016
^^^^^^^^^^^^^^^

Ordered 24" BenQ monitor for home desk and 1Tb portable drive for photography from NCIX.

Discussed LiveOcean boundary conditions code w/ Nancy.
Cleaned up vestigial u prefixes on string literals in SalishSeaNowcast.
Added stdout/stderr rediection to nowcast SalishSeaNEMO.sh script regardless of compute host.
Added clear_checklist and rotate_logs logs workers to nowcast automation.
Started porting make_plots worker in SalishSeaNowcast.
Attended Tetiyana Ross's EOAS colloquium about broadband acoustic measurements in the ocean.
Helped Tereza with ssh config.
Did a config reload on the manager to inform it of the clear_checklist and rotate_logs workers.
(SalishSea)

Helped Melanie restructure her code for reading profiles from WOD into a list of panadas dataframes so that she can concatenate them.
(GEOTRACES)


Fri 21-Oct-2016
^^^^^^^^^^^^^^^

get_NeahBay_ssh worker had issues getting data from NOAA site that caused it to finish after grib_to_netcdf, so upload_forcing had to patch the ssh obs file. But then make_forcing lists for forecast2 didn't launch. Re-ran get_NeahBay_ssh manually and it hung waiting for an acknowledgment from the manager. Restarted the manager, ran upload_forcing forecast2 manually, and the automation resumed, starting forecast2 run at 08:30.
clear_checklist worker failed with a KeyError.
Restarted ERDDAP server due to lots of errors reported.
Various failures in make_plot, presumably due to global DNS DDOS.
Started porting make_plots worker to NEMO_Nowcast framework.
(SalishSea)

Helped Karina sort out her messed up Anaconda env; ended up re-installing.

See project work journal.
(GOMSS)

Re-organized my desk at home to add 24" monitor to my setup.

Helped Saurav get SalishSeaTools installed.


Sat 22-Oct-2016
^^^^^^^^^^^^^^^

Fraser river discharge download failed due to DNS DDOS; re-ran download, make_runoff_file worker, and upload_forcing worker to restart automation for forecast2 run.
Fixed indentation error in config file that was causing clear_checklist worker to fail.
Worked with Susan to test her operating the nowcast system as proof of anyone in the sallen group being able to; almost there - see issue #17.
Continued porting make_plots worker to NEMO_Nowcast framework.
(SalishSea)

Silenced HTML parser warning from BeautifulSoup in ECget.
(SOG)


Sun 23-Oct-2016
^^^^^^^^^^^^^^^

Fraser river discharge download failed due to DNS DDOS; re-ran download, make_runoff_file worker, and upload_forcing worker to restart automation for forecast2 run.
Network connections to west.cloud failed; no obvious reason, so sent email to support@westgrid.
Continued porting make_plots worker to NEMO_Nowcast framework.
Changed NEMO_Nowcast manager to pass system state checklist to next_workers.after_*() functions.
Deployed make_plots worker for publish figures.
Added passing of run date from make_forcing_links worker to run_NEMO worker to facilitate back-fill runs and recovery for other automation failures.
(SalishSea)

Picked up Shadowfax from Mighty (finally!) and the chain broke on the way home.


Week 43
-------

Mon 24-Oct-2016
^^^^^^^^^^^^^^^

Forgot to update NEMO_Nowcast package on salish, so after_download_weather() failed due to lack of checklist; manually re-ran make_runoff_file, get_NeahBay_ssh, and grib_to_netcdf workers for 23oct16.
Network connections to west.cloud restored; manually re-ran upload_forcing and make_forcing_links workers for nowcast/23oct16 run to get automation restarted; forecast/23oct16 followed it automatically, make_plots worker launched for publish plots but is failing with a DNS error (presumably due to ongoing DNS DDOS).
Met w/ Susan & Nancy to discuss details of how we will use LiveOcean model product to produce boundary conditions for nowcast and research runs.
Worked on cleaning up logs/nowcast/ view in salishsea-site.
(SalishSea)

Phys Ocgy seminary by Tereza about DMS in the Arctic on the 2015 GEOTRACES cruise.

Whiteboard session with Saurav, Birgit & Terza about storage and ssh.

Week 6 of Digital Photography Workflow course at Langara; tethered shooting, digital assets management & backup; midterm.


Tue 25-Oct-2016
^^^^^^^^^^^^^^^

Fraser river discharge download failed due to DNS DDOS; re-ran download, make_runoff_file worker, and upload_forcing worker to restart automation for forecast2 run.
Found and fixed bug in stderr/stdout redirection in NEMO run script that was causing nowcast-green runs to fail during restart rebuilds; manually launched nowcast-green/24oct16.
DNS DDOS finally let me get make_plots publish runs up to 24oct16.
Finished cleaning up logs/nowcast/ view in salishsea-site, and set up unit test framework for views.
Started development of nowcast publish figures page view.
Salish Sea team mtg; see whiteboard.
Charles changed upstream DNS server for skookum & salish from UBC to EOAS, and overnight automation (including figures) completed smoothly :-)
(SalishSea)

Installed new chain on Shadowfax and tweaked derailleur alignment, then rode it to UBC :-)


Wed 26-Oct-2016
^^^^^^^^^^^^^^^

Reviewed ERDDAP daily report; atmospheric forcing dataset is up to date, but not model results.
Emailed Dominik about duplication of effort between he and us if his files are from same source as EC datamart.
Suppressed key_vectopt_loop cpp key in SOG(SMELT) config as Michael did for SalishSea config.
Pulled NEMO-3.6-code r6204+ on salish and did a clean build of the SOG(SMELT) config.
(SalishSea)

See project work journal.
(GOMSS)

Restarted app, postgres, mysql & nginx and saw a Maps page load time improvement from ~65s to ~10s, but that later degraded to ~60s again, though Stephanie reported ~60s intially and ~5s on subsequent requests.
(sealinkd)


Thu 27-Oct-2016
^^^^^^^^^^^^^^^

See project work journal.
(GOMSS)

Maps page load time at 08:30 ~60s intially and ~5s on subsequent requests (like Stephanie's report from yesterday). Also noted a cluster of alternating POST/GET hits from 74.142.146.84 with agent "Mozilla/5.0 (Windows NT 6.1; WOW64; Trident/7.0; rv:11.0) like Gecko"; address geolocates to Hamilton, OH.
(sealinkd)

Results directories disappeared from west.cloud :-(
Discussed tide file changes w/ Nancy.
Created NEMO-Cmd repo by extracting SalishSeaCmd package from tools repo (see GoMSS project work journal).
(SalishSea)


Fri 28-Oct-2016
^^^^^^^^^^^^^^^

Improved handling of deployment ssh key in SalishSeaNowcast to move closer to anyone-runnability re: issue #17.
Closed issue #15 re: PSU/TEOS-10 conversions in figures; Susan fixed it last weekend.
Continued work on salishsea-site nowcast publish figures page view; site is now styled with Bootswatch-3.3.7 Superhero theme, like Sphinx generated pages.
Discussed salishsea prepare changes for directory flexibility & exclusion of land processors w/ Michael.
(SalishSea)

Helped Mesdes with her WRF build and running it on orcinus.


Sat 29-Oct-2016
^^^^^^^^^^^^^^^

Experimented with WatchedFileHandlers to try to make manager, etc. notice log file rotations; re: NEMO_Nowcast issue #8.
Added `make_plots nowcast research` and `make_plots nowcast comparison` to automation.
Discussed results archive directory names and ERDDAP dataset id versioning w/ Susan re: 15oct16 move to NEMO-3.6 and planned hindcast of nowcast-green.
Discussed nav bar for salishsea-site app w/ Susan and implemented it.
Worked on salishsea combine rebuild_nemo path bug reported by Michael.
(SalishSea)

See project work journal.
(GOMSS)


Sun 30-Oct-2016
^^^^^^^^^^^^^^^

Worked on salishsea-site app layout and backend processing.
(SalishSea)

Photo-walk through Arbutus valley; leaves and a big, red mushroom.


November
========

Week 44
-------

Mon 31-Oct-2016
^^^^^^^^^^^^^^^

Continued email conversation w/ Dominik@EC re: HRDPS model products.
Resolved salishsea combine rebuild_nemo path bug reported by Michael.
Added forecast and forecast2 publish figure routes & views to salishsea-site app.
(SalishSea)

Workout lead by Elise re: pandas and sqlalchemy.
(swc)

Phys Ocgy seminar by Lan Li about internal waves in the South China Sea near Qingdao.

Week 7 of Digital Photography Workflow course at Langara; panorama & HDR shoot at Granville Island.


Tue 1-Nov-2016
^^^^^^^^^^^^^^

Continued development of salishseacast publish figures template and views.
Moved NEMO-3.6-code repo forward to r6459:
* Pulled changesets from NEMO-3.6-r6459 on Bitbucket into NEMO-3.6-mirror-merge at on niko
* Merged NEMO-3.6-code changes since NEMO-3.6r6204-ubc tag into NEMO-3.6-mirror-merge at on niko, tagged it as NEMO-3.6r6459-ubc, and pushed to NEMO-3.6-code on Bitbucket
Started moving NEMO-3.6-code repo forward to r6770
* Pulled changesets 6467 through 6770 into NEMO-3.6-hg-mirror on salish.
* Merged NEMO-3.6-hg-mirror into NEMO-3.6-mirror-merge on niko.
* Tagged NEMO-3.6-r6770 in NEMO-3.6-mirror-merge  and pushed to new NEMO-3.6-r6770 repo on Bitbucket for Elise to use for merge-comparison test.
Salish Sea team mtg; see whiteboard.
(SalishSea)


Wed 2-Nov-2016
^^^^^^^^^^^^^^

Headache and sinus congestion.

See project work journal.
(GOMSS)

Finally re-found the utilities Python package that I have been searching for for over a year - boltons.
Discovered that nowcast-sys/logs/nowcast/ dir was g-w but sticky, so set g+w there; hoping to resolve the next roadblock in the multi-person ops story.
Worked on porting creating worker docs from SalishSeaNowcast docs to NEMO_Nowcast docs.
(SalishSea)


Thu 3-Nov-2016
^^^^^^^^^^^^^^

Tired, but felling healthier than yesterday.

See project work journal.
(GOMSS)

Setting g+w on nowcast-sys/logs/nowcast/ did not resolve the permissions issue on logs created by the rotate_logs worker, so applied the patch that uses the boltons FilePerms so that it will get tested tomorrow morning.
Finished porting creating worker docs from SalishSeaNowcast docs to NEMO_Nowcast docs.
Reviewed Michael's changes to add land processor elimination to salishsea prepare.
(SalishSea)


Fri 4-Nov-2016
^^^^^^^^^^^^^^

Shot panoramas from roof of ESB and on east side of Main Mall (featuring biodiversity whale).

Debugged rotate_logs worker permissions setting.
Got salishseacast publish figures template and views to the point where the pages include all figures, and the code is mostly well-factored and covered by unit tests.
Started writing NEMO cloud description for ONC; discussed IO w/ Michael.
(SalishSea)


Sat 5-Nov-2016
^^^^^^^^^^^^^^

Confirmed that rotate_logs worker permissions setting works.
Released salishseacast publish figures template and views as the code that produces the pages for the site; added route to intercept requests for publish_ddmmmyy.html requests.
Started work on salishseacast research figures template and view; refactored lots of template markup out of publish template so that it can be re-used.
(SalishSea)


Sun 6-Nov-2016
^^^^^^^^^^^^^^

Time change from PDT to PST.

forecast2 run and post-processing were completed by 06:40.
Released salishseacast research figures template and views as the code that produces the pages for the site; added route to intercept requests for research_ddmmmyy.html requests.
Released salishseacast results index calendar grid template and view.
Released salishseacast storm surge forecast view; off the results page production treadmill!!
(SalishSea)


Week 44
-------

Mon 7-Nov-2016
^^^^^^^^^^^^^^^

NEMO Telcon
* BIO: Youyu, JP, Shiliang, M Casey, S Higginson
  * JP working on N Pacific 1/36
  * GoMSS 1/36
  * SW Nova Scotia 500m
  * Areas of work:
    * short term forecasting, evaluation
    * decade/multi-decade hindcasts
    * seasonal/sub-seasonal prediction
    * biogeochemistry
* UA: Paul Xiamin
* UBC: Susan, Michael, Doug
  * Salish Sea
    * storm surge
    * daily biology
    * deep water renewal
    * wind driven surface currents
    * open boundaries from LiveOcean
    * AGRIF for Baynes Sound
    * carbon chemistry
* EC: Fred, Fraser, Greg

Phys Ocgy seminar by Birgit about her M.Sc. work on the CHIME radio telescope.

Discussed failed status of ONC ADCP data downloads with Rich.
Finished writing draft of NEMO cloud description for ONC; sent to Susan & Michael for review.
Started porting ping_erddap worker to SalishSeaNowcast.
(SalishSea)

Week 8 of Digital Photography Workflow course at Langara; processing panorama & HDR images.


Tue 8-Nov-2016
^^^^^^^^^^^^^^

Contributed to the discussion about ONC DACP data that Rich resurrected.
Reviewed and commented on RAC application.
Discussed roll-out of modified rebuild_nemo tool w/ Michael.
Finished porting ping_erddap worker.SalishSeaNowcast.
Asked Jie for ONC ferry data download cron job details.
Sent NEMO cloud description to ONC.
Started working on v16.10 ERDDAP datasets; first stop - fixing metadata in mesh_mask_SalishSea2.nc.
Salish Sea team mtg w/ Ellie from SFU as guest; see whiteboard.
(SalishSea)

Discussed Jupyter Notebook w/ Matlab kernel & Google Drive for collaborations w/ Roger & Dan.


Wed 9-Nov-2016
^^^^^^^^^^^^^^

Physio appt; more chest stretches to work on shoulder range of motion.

Restarted manager because yesterday's config reload messed it up to the point that it didn't launch the grib_to_netcdf forecast2, make_runoff_file, or forecast2 runs; manually ran  grib_to_netcdf forecast2, & make_runoff_file before nowcast.
Corrected long_name attribute values for e1t e2t, e1u, e2u, e1v, e2v, e1f, and e2f variables in mesh_mask_SalishSea2.nc.
(SalishSea)

Tried to access EduCloud web interface to explore adding VCPUs to Resilient-C VM but auth failed; opened UBC IT ticket for help; resolved after 14 email exchanges; can't alter VM resources from web console.
(sealinkd)

See project work journal.
(GOMSS)


Thu 10-Nov-2016
^^^^^^^^^^^^^^^

Prep for workout session on Sphinx, Readthedocs & autodoc.
(swc)

EOAS seminar.


Fri 11-Nov-2016
^^^^^^^^^^^^^^^

**Statutory Holiday** - Remembrance Day

Finished development of workbook & zip archive for 14nov16 workout about Sphinx, Readthedocs, autodoc & nbsphinx.
(swc)

Started porting make_feeds worker into SalishSeaNowcast framework.
(SalishSea)


Sat 12-Nov-2016
^^^^^^^^^^^^^^^

Finished porting make_feeds worker into SalishSeaNowcast framework.
Merged SalishSeaCmd land-processor-elimination branch.
Added route & view for storm surge alert feeds to salishsea-site app.
(SalishSea)


Sun 13-Nov-2016
^^^^^^^^^^^^^^^

Changed auth from persona.org to Stormpath.
(randopony)


Week 46
-------

Mon 14-Nov-2016
^^^^^^^^^^^^^^^

Continued working on nowcast-green/blue mesh mask metadata.
Discussed ONC ADCP and ferry data w/ Rich & Mark.
(SalishSea)

Delivered workout about Sphinx, Readthedocs, autodoc & nbsphinx.
(swc)

Phys Ocgy seminar by Saurav on his M.Sc. research on dry-line thunderstorms in eastern India.

Week 9 of Digital Photography Workflow course at Langara; studio shoot with models.


Tue 15-Nov-2016
^^^^^^^^^^^^^^^

Helped Susan build vagrant config for EOSC-471 and test it on EOSM lab PC.
(EOAS teaching)

Continued working on nowcast-green/blue mesh mask metadata; published bathymetry & 2D mesh mask datasets.
(SalishSea)

Salish Sea team mtg; see whiteboard.


Wed 16-Nov-2016
^^^^^^^^^^^^^^^

See project work journal.
(GOMSS)

Continued email conversation w/ Belaid about optimizing west.cloud; changes on his side resulted in ~30% deacrease in MPI run times:
* nowcast/16nov16 - 37m vs 47m for 15nov16
* forecast/16nov16 - 42m34s vs 60m for 15nov16
No change, or slight increase in rebuild/deflate times.
forecast runs produce completely useless restart files at 30h that could be eliminated.
Michael's rebuild_nemo improvements and LPE have not yet been applied.
(SalishSea)


Thu 17-Nov-2016
^^^^^^^^^^^^^^^

See project work journal.
(GOMSS)


Fri 18-Nov-2016
^^^^^^^^^^^^^^^

Emails to ONC about nowcast performance and results on web.
Explored early history of nowcast system to help Susan find initial conditions for hindcast runs.
Emailed ONC to confirm that ADCP profile data will appear on their ERDDAP.
finished nowcast-green/blue mesh mask metadata; published 3D mesh mask dataset.
Started porting get_onc_ctd worker to SalishSeaNowcast framework.
(SalishSea)

Took photo of MOAD group on ESB staircase.

Helped Susan w/ tech support for EOSC-471 mini-project 3 (Ariene on vagrant).
(EOAS teaching)


Sat 19-Nov-2016
^^^^^^^^^^^^^^^

Wrote inventory/state report email to Rich about ONC ADCP, ferry & CTD data downloads.
(SalishSea)

Worked on NEMO-Cmd package; see project work journal.
(GOMSS)


Sun 20-Nov-2016
^^^^^^^^^^^^^^^

Updated tools & NEMO-3.6-code in nowcast system to bring in NEMO r6459, land processor elimination, and rebuild_nemo level 4 deflation to speed up restart file processing.
Rebuilt rebuild_nemo, SalishSea & SOG configs on salish.
Update nowcast-green model changes table.
Updated nowcast-sys/SS-run-set after nowcast-green launch failed due to out of date namelist.compute.
nowcast-blue on west.cloud failed with non-obvious error during upload_forcing because shared storage was full;
re-enabled cron jobs to clear old results.
Looked at Belaid's test run results; his 128-core 16nov16 run took 31m compared to our 37m production run on 136 cores; guessing that the trade-off of 1 less VM's network overhead for MPI is worth it for slightly less square MPI sub-domains.
Thought some more about leaving 1 core/VM free for network overhead, and land processor elimination; we should try a 7x17+1 run and a 9x21+1 LPE run on 17+1 VMs w/ host slots set to 7, and a 10x22+1 LPE run on 16+1 VMs.
Plan:
* 8x16+1 for 21nov16 runs
* 7x17+1 w/ slots=7
* 9x21+1 w/ LPE & slots=7
* 10x22+1 w/ LPE & slots=8
nowcast-blue/20nov16 didn't finished rebuild & gather due to full disk, so forecast failed; did gather on salish and scp-ed restart file to west.cloud to get run started.
(SalishSea)

Worked on NEMO-Cmd package; see project work journal.
(GOMSS)


Week 47
-------

Mon 21-Nov-2016
^^^^^^^^^^^^^^^

Changed config on west.cloud to use 8x16+1 MPI decomposition based on Belaid's test run results.
Finished porting get_onc_ctd worker to SalishSeaNowcast framework; backfilled 20-Nov to 15-Oct data.
Ran GETDEPL on central node ADCP data to 31-Aug, and released data to 22-Aug.
Started working through repeated runs of GETDEPL on east node ADCP data to 31-Aug, eliminating data files that matlab says it can't read one run at a time :-(
Deleted unused modules from SalishSeaNowcast NEMO_Nowcast branch in preparation for merging into default.
Started cleaning up SalishSeaNowcast docs in preparation for merge and release.
(SalishSea)

Phys Ocgy seminar by Rich & Roger about GVRD-funded SoG monitoring program

Week 10 of Digital Photography Workflow course at Langara; process last week's studio shoot with models images; B&W, split-tone, HSL adjustments & brushing adjustments.


Tue 22-Nov-2016
^^^^^^^^^^^^^^^

nowcast system blew up after download_weather 06 because I forgot to restart manager to load config for get_onc_ctd worker; manually ran get_onc_ctd, make_runoff_file, get_NeahBay_ssh & grib_to_netcdf workers to get automation restarted and run forecast2 late.
Continued working through repeated runs of GETDEPL on east node ADCP data to 31-Aug, eliminating data files that matlab says it can't read one run at a time :-(
Added Fraser delta lower slope BBL and upper slope DDL nodes CTD stations to get_onc_ctd & ping_erddap workers, and started backward downloading of datasets.
Analyzed timing of 8x16+1 west.cloud runs: nowcast: 31m+22m, forecast: 40m+35m.
Change west.cloud config to max-slots=7 and 7x17+1.
Found bug in get_onc_ctd worker whereby both alinity and temperature data were salinity; fixed it and started re-generating all 4 datasets.
Salish Sea team mtg; see whiteboard.
(SalishSea)


Wed 23-Nov-2016
^^^^^^^^^^^^^^^

Fixed west.cloud config brainfart: max-slots=7 s/b slots=7; run times:
* forecast2: 35m+29m.
* nowcast: 27m+19m.
* forecast: 34m+29m.
East node ADCP GETDEPL finally finished. After fumbling around because I forgot that you have to copy a DEPL* file into the east/, finally got a deployment rotation angle set for LTIM.
Started working through repeated runs of GETDEPL on DDL node ADCP data to 31-Aug, eliminating data files that matlab says it can't read one run at a time :-(
(SalishSea)

Profiled Start->Maps page load: ranged from 4.5s to 20s. Did apt-get update, upgrade & autoremove. Rebooted VM. Load times unchanged, and erratic. Opened ticket #INC0729450 w/ UBC IT (email thread in @eoas email).
(sealinkd)

See project work journal.
(GOMSS)


Thu 24-Nov-2016
^^^^^^^^^^^^^^^

Continued working through repeated runs of GETDEPL on DDL node ADCP data to 31-Aug, eliminating data files that matlab says it can't read one run at a time :-(
Reviewed Nancy's Live Ocean docs and dealt with docs & dependency changes of adding her modules to SalishSeaTools.
Set up cron job to download Live Ocean 72h forecast product daily and extract salish Sea western boundary sub-domain from it.
West.cloud lost network connectivity at about 11:12; after 2 emails to support@westgrid it was restored at about 14:45; had to re-mount sshfs on most VMs, then ran make_forcing_links manually to restart automation.
Started creating download_live_ocean worker.
Investigated Jie's ferry data download scripts; they use the ONC scalar data API.
(SalishSea)

Westgrid townhall:
* Patrick Mann, Director of Operations
  * big news: migration off jasper delayed to 31-Mar-2017
  * https://docs.computecanada.ca/wiki/Migration2016
  * GP1 == Arbutus, uVic, operational
  * GP2 == Cedar, SFU
    * PO soon, sched Apr, hope Feb/Mar
  * GP3 == Graham, Waterloo
    * sched Apr
  LP1 == Niagra, late 2017, Toronto
  NDC == Silo replacement, Nat'l Data Cyberinfrastructure
    * NDC-1 at SFU,
    * NDC-2 at Waterloo, migration in progress
    * NDC-Object, hope Apr, likely mid-2017
  * orcinus will continue beyond Mar-2018 but not on support contract, needed until Niagra comes online, important data should go to NDC
* Ryan Enge, uVic site lead
  * 7640 cores
  * 200 Tb ceph storage, increasing to 600-700 Tb
  * serious allocation by RAC/RPP
  * Hermes has been virtualized into the new cloud; optimized for serial jobs
* Kamil, UofA
  * jasper available until 31-Mar, will shrink as pieces die
  * recommending move to orcinus or parallel, bugaboo seems to have storage issues
* GP2 & GP3 are Omni-Path (100Gb), not InfiniBand (10Gb if QDR)
* Sergy @UofS, Silo migration
  * future storage:
    * scratch on clusters
    * NDC:
      * project (10Pb per site)
      * nearline (15Pb per site automated move from disk to tape, request required for retrieval to online)
      * object (all sites, special projects, RAC-allocated)
* RAC allocation: reviews Dec/Jan, decisions 6-7-Feb-2016, notifications 9-Mar-2017
* defunded == off nat'l funded infra, institutions own systems and will decide what to do with them
* bugaboo has huge (2928h) max walltime, lowest on list of recommended migration destinations
* next townhall in January

Upgraded niko to PyCharm 2016.3.


Fri 25-Nov-2016
^^^^^^^^^^^^^^^

Upgraded kudu to PyCharm 2016.3.

forecast2 failed due to 3 sshfs mount disconnects; remounted and restarted via make_forcing_links worker.
Continued working through repeated runs of GETDEPL on DDL node ADCP data to 31-Aug, eliminating data files that matlab says it can't read one run at a time :-(
Changed download_weather 12 launch time from 11:00 to 10:45 based on yesterday's un-delayed weather downloads.
After review of EC datamart file availability times, changed download_weather 06 launch time from 05:00 to 04:15, and 12 launch time from 10:45 to 10:30.
(SalishSea)

See project work journal.
(GOMSS)


Sat 26-Nov-2016
^^^^^^^^^^^^^^^

Forgot to restart scheduler, so download_waether adjustments only applied to 12 weather; it was ready at 10:59, but we went into a 512s wait at 10:58:30.
Continued working through repeated runs of GETDEPL on DDL node ADCP data to 31-Aug, eliminating data files that matlab says it can't read one run at a time :-(
(SalishSea)

Fiddled with new Telus router and Airport Extreme to try to optimize home network.

See project work journal.
(GOMSS)


Sun 27-Nov-2016
^^^^^^^^^^^^^^^

Fixed SalishSeaNowcast.next_workers bug that was causing ERDDAP falg files for CTD datasets to be ineffective.
forecast2 run started at 04:36 and logs rolled at 05:51
nowcast run started at 11:03.
Continued working through repeated runs of GETDEPL on DDL node ADCP data to 31-Aug, eliminating data files that matlab says it can't read one run at a time :-(
(SalishSea)

See project work journal.
(GOMSS)


Week 48
-------

Mon 28-Nov-2016
^^^^^^^^^^^^^^^

Explored Bitbucket pipelines for pytest & yapf.

Continued working through repeated runs of GETDEPL on DDL node ADCP data to 31-Aug, eliminating data files that matlab says it can't read one run at a time :-( (25Jul was a really weird error)
Updated tools, NEMO-3.6-code & SS-run-sets repos on west.cloud to bring in NEMO r6459, land processor elimination, and rebuild_nemo level 4 deflation to speed up restart file processing.
Rebuilt rebuild_nemo, SalishSea config on west.cloud.
Changed nowcast MPI decommissioning to 10x20+1 w/ LPE & slots=7 (116 of 119 available cores).
Update nowcast model changes table.
Continued cleaning up SalishSeaNowcast docs in preparation for merge and release.
(SalishSea)

Phys Ocgy seminar by Kyle about Ba & del O-18 tracer modeling in the Arctic

Ticket #INC0729450 re: erratic Maps page load times got picked up by Dave@ubcit.
Sent Jackie's spreadsheet and a screenshot; Dave reported no obvious correlation w/ cloud ops.
(sealinkd)

Week 11 of Digital Photography Workflow course at Langara; processing copies of 4 HDR & panorama images w/ sharpening, transformations, spot removal, and brush/filter adjustments.


Tue 29-Nov-2016
^^^^^^^^^^^^^^^

Fixed bug in run_NEMO worker whereby number of processors was not correctly calculated for LPE runs;
* forecast2/28nov16 took 24m37s (30% faster) for MPI + 18m28s (36% faster)
* nowcast/29nov16: 23m39s (13% faster ???) + 14m12s (24% faster)
* forecast/29nov16: 23m49s + 17m6s; alert feed published at 12:24
Continued working through repeated runs of GETDEPL on DDL node ADCP data to 31-Aug, eliminating data files that matlab says it can't read one run at a time :-(
Added page footer to salishsea-site app.
Worked on poster for stakeholders workshop.
Salish Sea team mtg; see whiteboard.
(SalishSea)

See project work journal.
(GOMSS)

Continued ticket #INC0729450 conversation re: erratic Maps page load times; agreed to test app w/ VM memory increased to 2Gb.
(sealinkd)


Wed 30-Nov-2016
^^^^^^^^^^^^^^^

Tested app w/ 2Gb VM; not consistently faster; maybe we need another vCPU?
Emailed Stephanie & Jackie who agreed to collect more data.
Fixed minor issues in nginx configs that were causing spew in the error log; localhost in server_name list & proxy_pass directive.
(sealinkd)

Continued working through repeated runs of GETDEPL on DDL node ADCP data to 31-Aug, eliminating data files that matlab says it can't read one run at a time :-( (was weird like 25Jul)
Fixed broken links that Michael found in ERDDAP dataset metadata.
* forecast2/29no16: 24:24 + 19:23
* nowcast/30nov16: 21:35 + 13:31
* forecast/30nov16: 25:58 + 17:23
ONC ERDDAP dataset for present ADCP deployments at east & DDL nodes appeared on their server; tabledap datasets, but 80% cassandra database failure rate.
(SalishSea)

See project work journal.
(GOMSS)


Thu 1-Dec-2016
^^^^^^^^^^^^^^

Forced reload of all ERDDAP datasets via flag files to apply yesterday's metadata URL fixes.
East node ADCP GETDEPL finally finished. After fumbling around because I forgot that you have to copy a DEPL* file into the east/, finally got a deployment rotation angle set for LTIM.
DDL node ADCP data GETDEPL to 31-Aug finally finished; LTIM shows 2 data clusters for most recent deployment; corrected angle for one and sent email to Rich for advice.
ONC ERDDAP dataset for present ADCP deployments at east & DDL nodes appears to be working; tabledap datasets.
* forecast2/30no16: 24:34 + 19:32
* nowcast/01dec16: 19:24 + 13:34
* forecast/01dec16:
Updated storm surge figure in SalishSeaCast brochure for stakeholders mtg.
(SalishSea)

Maps page loading time was back to ~15s; noticed that memory use was up to 1.8Gb.
Rebooted VM and response came back to ~5s.
(sealinkd)

See project work journal.
(GOMSS)


Fri 2-Dec-2016
^^^^^^^^^^^^^^

See project work journal.
(GOMSS)

Added storm surge text & figure to SalishSeaCast poster for stakeholders mtg.
Updated ONC on status of west.cloud nowcast runs.
Changed west.cloud MPI decomposition to 9x20 for 109 of 112 cores on 16 VMs with slots=7.
Added CITATION.rst file to docs repo so that I could deploy the salishsea-site page footer mods.
Started porting storm surge portal page into Pyramid app.
(SalishSea)

Staff and faculty end of year lunch & farewell for Paul Smith.

Dave@UBCIT added a 2nd vCPU to sealinkd-vm; rebooted.
(sealinkd)


Sat 3-Dec-2016
^^^^^^^^^^^^^^

See project work journal.
(GOMSS)

nowcast results w/ MPI decomposition to 9x20 for 109 of 112 cores on 16 VMs with slots=7:
* forecast2/02dec16: 23:44 + 17:12
* nowcast/03dec16: 20:54 + 13:33
* forecast/03dec16: 23:58 + 16:59
Finished porting storm surge portal page into Pyramid app.
Added salishsea gather option to run_NEMO worker to delete restart files for forecast2 runs because we never use them, and they cost about 10 minutes of post-processing time.
Pulled a lot of changes into west.cloud SalishSeaNowncast.
(SalishSea)

Renewed APEGBC membership; 80h cpd


Sun 4-Dec-2016
^^^^^^^^^^^^^^

nowcast results w/ MPI decomposition to 9x20 for 109 of 112 cores on 16 VMs with slots=7, no more restart files for forecast2 runs:
* forecast2/03dec16: 23:03 + 13:17
* nowcast/03dec16: 20:07 + 12:26
* forecast/04dec16: 23:44 + 16:33
Added west.cloud specific elements to run_NEMO worker: mpi_hosts file, --bind-to-core, and XIOS host ip address.
Explored how restart files are produced by NEMO; did a test forecast run on west.cloud with ln_rst_list = .true. and the end-of-day time step as the first element in nn_stocklist; experiment worked, so incorporated it into run_NEMO worker.
Added option to set max retry waiting time to NEMO_Nowcast worker.get_web_data(); re: issue #3.
Ported SalishSeaCast about page (aka nemo index) into Pyramid app.
(SalishSea)

See project work journal.
(GOMSS)


December
========

Week 49
-------

Mon 5-Dec-2016
^^^^^^^^^^^^^^

Started snowing at about 04:00; about 4cm on the ground by 08:00 when it changed to snain.

Fixed a bug in run_NEMO setting of restart file output times.
Worked through other transition issues related to setting restart file output times.
Started work on adding nowcast-blue datasets to ERDDAP; metadata issues in grid_T.
(SalishSea)

Worked on bio for UQAR winter modeling school.


Tue 6-Dec-2016
^^^^^^^^^^^^^^

Finished on bio for UQAR winter modeling school; emailed it and PyCon headshot to Marion.

Met w/ Daphne@eoas re: vacation pay.

Upgraded niko to Ubuntu 16.10 (yakety yak); updated ppas:
* Google talk plugin
* System76 drivers (took a couple of tries)
* Git
* Zeal
* Mercurial (no yakkety build yet, so disabled)
* deleted bluejeans deb that always reports weakness

Continued work on adding nowcast-blue datasets to ERDDAP; gave up on grid_T for now, succeeded on grid_U and grid_V.
Confirmed that ERDDAP will happily work with a symlinked /opt/tomcat/content/erddap/datasets.xml file, so started setting up a Mercurial repo to hold that file and related stuff.
Added grid_W dataset inthe course of testing workflow with repo.
Salish Sea team mtg; see whiteboard.
(SalishSea)

Tried to disable sslv3 on resilient-c.
(sealinkd)


Wed 7-Dec-2016
^^^^^^^^^^^^^^

Described software on sealinkd-vm to Dave@UBCIT.
Proposed ongoing maintenance fee to Stephanie to cover erratic loading time issue work, and planned January data update, and she accepted it.
Dave@UBC reported that they had made backend changes and have identified CPU spiking; they are working on it and I am monitoring the app; load times vary from <5s to >40s/
(sealinkd)

Tried to deploy stormpath auth upgrade but it fails with:
python2.7/site-packages/requests/packages/urllib3/util/ssl_.py:334: SNIMissingWarning: An HTTPS request has been made, but the SNI (Subject Name Indication) extension to TLS is not available on this platform. This may cause the server to present an incorrect TLS certificate, which can cause validation failures. You can upgrade to a newer version of Python to solve this. For more information, see https://urllib3.readthedocs.io/en/latest/advanced-usage.html#ssl-warnings
  SNIMissingWarning
Tried various fixes with no luck; this could be the push to Python 3...
(randopony)

See project work journal.
(GOMSS)


Thu 8-Dec-2016
^^^^^^^^^^^^^^

See project work journal.
(GOMSS)


Fri 9-Dec-2016
^^^^^^^^^^^^^^

See project work journal.
(GOMSS)

MEPAR Stakeholders workshop at SFU downtown.
* Talked at length with Johannes about moving Salish Sea wave model to production


Sat 10-Dec-2016
^^^^^^^^^^^^^^

See project work journal.
(GOMSS)

Helped Nancy with NEMO build/run issues on orcinus; learned that module commands in .bashrc are compulsory, not optional, and that the generated SalishSeaNEMO.sh script has module load mismatches in it.
(SalishSea)

Upgraded kudu to Ubuntu 16.10 (yakety yak); updated ppas:
* Google talk plugin
* System76 drivers (took a couple of tries)
* Git
* Mercurial (no yakkety build yet, so disabled)
* deleted bluejeans deb that always reports weakness
* deleted darktable ppa because it is now in system packages


Sun 11-Dec-2016
^^^^^^^^^^^^^^^

Hacked through migrating randopony to Python 3.5 in hopes of mitigating openssl sni issue on webfaction; warning still occurs, but it is not fatal; opened a community support request about it on webfaction.
(RandoPony)


Week 50
-------

Mon 12-Dec-2016
^^^^^^^^^^^^^^^

Started NEMO-3.6-code repo forward to r6770:
* Pulled changesets from NEMO-3.6-r6459 on Bitbucket into NEMO-3.6-mirror-merge at on niko, stripped nestingtools-cleanups branch that Michael confirmed should not be merged.
* Pulled NEMO-3.6-code changes since NEMO-3.6r6459-ubc tag into NEMO-3.6-mirror-merge at on niko, stalled on merge conflicts in SMELT code.
Continued adding nowcast-blue datasets to ERDDAP: single point sea surface heights, all except Boundary Bay.
Changed nowcast MPI decomposition to 9x19 for 104 of 105 cores on 15 VMs with slots=7.
Did code cleanup in SalishSeaNowcast; introduced a few instances of FilePerms().
(SalishSea)

Workout about Python modules lead by Susan.
(swc)


Tue 13-Dec-2016
^^^^^^^^^^^^^^^

nowcast results w/ MPI decomposition to 9x20 for 109 of 112 cores on 16 VMs with slots=7, no more restart files for forecast2 runs:
* forecast2/12dec16: 26:12 + 13:40 = 39:52
* nowcast/13dec16: 19:56 + 13:42 = 33:38
* forecast/13dec16: 24:41 + 16:48 = 41:29
Explored NEMO-3.6-mirror-merge merge conflict further, and worked through it with Elise.
* Merged NEMO-3.6-code changes since NEMO-3.6r6770 tag into NEMO-3.6-mirror-merge at on niko, tagged it as NEMO-3.6r6770-ubc, and pushed to NEMO-3.6-code on Bitbucket
* Changed NEMO-3.6r6770, NEMO-3.6r6459, and NEMO-3.6r6204 repos on Bitbucket to read-only.
Started work on get Tb of NFS storage that Belaid arranged into production on west.cloud.
Worked on adding forecast datasets to ERDDAP.
Met w/ Rich re: ONC DDL ADCP data; also discussed ferry data into ERDDAP, agreed on 20s aggregation interval.
Salish Sea team mtg; see whiteboard.
Moved runoff forcing filename templates from make_runoff_file worker to config file to close issue #8.
Did apt-get update/upgrade on nowcast0.
Intalled nfs-kernel-server on nowcast0 and set it up to export /nemoShare/MEOPAR as /export/MEOPAR.
Did apt-get update/upgrade on nowast1.
Installed nfs-common on nowcast1 and NFS-mounted /export/MEOPAR from nowast0 as /home/ubuntu/MEOPAR-nfs.
Refactored make_runoff_file worker to move file name templates into config file.
(SalishSea)


Wed 14-Dec-2016
^^^^^^^^^^^^^^^

Cleared 2016 events & riders data from RandoPony database by swapping copy of production database in as dev database for PyCharm project and using the new multi-row features of the database editor.
Created NewYearsPop event.
Improved and cleaned up pony deployment.
(RandoPony)

Created and submitted invoice for ongoing maintenance of app and Salish Sea communities data update planned for January.
(sealinkd)

See project work journal.
(GOMSS)

Started re-organizing image storage and workflow.
Imported images and sidecars from Langara workflow course into Darktable; sidecar data imported is pretty basic.


Thu 15-Dec-2016
^^^^^^^^^^^^^^^

Re-formatted 1Tb Adata removable drive as Photos01Backup, and loaded photos & darktable config on to it.

See project work journal.
(GOMSS)

Did some edits (marked red) in the 150719-Gustavsen-ReidInlet collection; mostly pulling people out of the background with drawn and parametric masks.
Came up with rsync commands that work better than GUI to keep external backup drive in sync with Pictures/ dir.


Fri 16-Dec-2016
^^^^^^^^^^^^^^^

Installed Chromium on niko so that I can use my Google Drive timesheet spreadsheet again :-(

Changed nowcast config on west.cloud to use nowcast0 as XIOS server.
Cloned repos into /nemoShare/MEOPAR/ on west.cloud.
Updated SalishSeaNowcast deployment docs.
Tried to use the ADCP data that Lan downloaded but it has a completely different data structure to the automated download data.
Helped Tereza with her data analysis project file generation script.
Merged SalishSeaNowcast NEMO_Nowcast branch into default and closed former.
Fought with readthedocs to get a complete build.
(SalishSea)

Helped Idalia with her NEMO-3.6 update mess and files organization for running NEMO.
(canyons)


Sat 17-Dec-2016
^^^^^^^^^^^^^^^

Refactored get_NeahBay_ssh worker to move file name template into config file.
Investigated forecast run failure on west.cloud; watch_nemo worker reported that it couldn't find the run pid, but the run completed; manually ran download_results worker to restart automation.
Updated west.cloud SalishSeaNowcast package to default branch.
Got committed nowcast config file closer to the in-production one on west.cloud, and opened issues #31 and #32 re: remaining differences.
Refactored grib_to_netcdf worker to move file name template into config file.
Refactored download_results worker to use pathlib.
(SalishSea)

See project work journal.
(GOMSS)


Sun 18-Dec-2016
^^^^^^^^^^^^^^^

Investigated forecast2 run failure; cause was NEMO_Nowcast repo not having been updated on west.cloud to correspond to latest SalishSeaNowcast revisions.
(SalishSea)

Fixed sing-up failure issue in Python 3 deployment; had to remove utf-8 encode/decode code that was added to make accented names work in Python 2.7 (kind of ironic...)
Lots of other code cleanups to modernize codebase and embrace Python 3 only.
(randopony)


Week 51
-------

Mon 19-Dec-2016
^^^^^^^^^^^^^^^

Work-at-home day due to overnight snow/rain that produced transit chaos.

Updated SalishSeaNowcast on skookum to default branch.
Created nowcast-compute-node-v5 snapshot image on west.cloud of nowcast1 with MEOPAR-nfs mounted, and tested launching a new instance from it; that worked, but subsequent instance launches failed; sent email to Belaid.
Used ssh in a bash loop to install nfs-common on remaining compute nodes, and mount NFS shared storage from nowcast0.
Continued work on SalishSeaNowcast deployment docs, and on cleaning up readthedocs build issues re: imported environment and modules.
Fixed an args bug in make_forcing_links worker that crept in during weekend work on issue #9, and re-ran it manually to restart automation.
Did initial tests on NFS shared storage on west.cloud:
* ~/MEOPAR-nfs/ mount point is a no-go because path.resolve() spells it as /nemoShare/MEOPAR/, so just use that
* nowcast/19dec16 run time w/ 9x19+1 for 104 of 105 cores on 7x15+1 VMs was ~24m vs. ~20m w/ sshfs shared storage
* nowcast/19dec16 gather was 8m20s vs. 12m-14m w/ sshfs storage
* nowcast/19dec16 run time w/ 9x20+1 for 109 of 112 cores on 7x16+1 VMs was ~22m vs. 20m-21m w/ sshfs shared storage
(SalishSea)


Tue 20-Dec-2016
^^^^^^^^^^^^^^^

forecast2 failed due to me not pulling in Susan's rivers changes, and her not changing namelist.surface; got things fixed in time for nowcast/forecast runs.
Worked w/ Rich to make GETDEPL work w/ ADCP data from both automated downloads, and Lan's web portal downloads.
Discussed salishsea site design w/ Ben.
Salish Sea team mtg; see whiteboard.
(SalishSea)

Continued re-organizing image storage and workflow.


Wed 21-Dec-2016
^^^^^^^^^^^^^^^

Finished re-organizing image storage of all RAW images on kudu.
Created shell script to do rsync to backup drive.

See project work journal.
(GOMSS)

Copied Lan's DDL ADCP dataset files for 2016 into ONC_ACDP/ file space.
Ran GETDEPL for DDL ADCP datasets, fixed a bug, and ran it again to completion.
(SalishSea)


Thu 22-Dec-2016
^^^^^^^^^^^^^^^

Travel from home to Barrie or Christmas holiday.

See project work journal.
(GOMSS)


Sat 24-Dec-2016
^^^^^^^^^^^^^^^

Started work on salishsea site nowcast automation monitoring page.
(SalishSea)


Week 52
-------

Mon 26-Dec-2016
^^^^^^^^^^^^^^^

Finished salishsea site nowcast automation monitoring page.
(SalishSea)


Wed 28-Dec-2016
^^^^^^^^^^^^^^^

Changed ERDDAP server URL to be a request attribute in salishsea site app.
Continued work on download_live_ocean worker.
(SalishSea)


Thu 29-Dec-2016
^^^^^^^^^^^^^^^

Travel home from Barrie.

Continued work on download_live_ocean worker.
(SalishSea)


Fri 30-Dec-2016
^^^^^^^^^^^^^^^

Added deflate plug-in to NEMO-Cmd for Susan to use in hindcast runs.
Extracted tools/SalishSeaCmd into a new SalishSeaCmd repo.
(SalishSea)


Sat 31-Dec-2016
^^^^^^^^^^^^^^^

Created SalishSeaCmd repo on Bitbucket.
Enabled download_results worker to handle hindcast results from jasper.
Added `deflate` sub-command to SalishSeaCmd via plug-in from NEMO-Cmd.
Added SalishSeaNowcast split_results worker to split results files from multi-day hindcast runs into daily run directories as ERDDAP and users expect them to be organized.
After discussion with Susan, decided to make SalishSeaCmd combine, deflate, and gather sub-commands independent rather than nested as they are in tools version of the package.
(SalishSea)


Sun 1-Jan-2017
^^^^^^^^^^^^^^

Discussed concurrency strategy for deflate sub-command w/ Susan.
Fixed bugs in split_results and download_results workers.
Manually downloaded forecast2/31dec16 results that failed due to Path() -> str bug introduced yesterday in download_results worker.
Fixed download_results worker bug introduced yesterday re: generator -> list in checklist.
Manually ran make_plots forecast2 to restart automation.
Manually ran make_plots forecast/31dec16 and forecast2/30dec16 to generate figures that failed yesterday due to XML parse error in EC data.
Added descriptions of SalishSeaCmd, NEMO-Cmd, and SalishSeaNowcast repos to project docs, and fixed other build errors.
Changed nowcast system deployments on skookum and west.cloud to use NEMO-Cmd and SalishSeaCmd packages, and updated deployment docs.
Finished implementation of download_live_ocean worker and replaced cron job on skookum with it.
Enabled concurrent netCDF file deflation in NEMO-Cmd.
Started refactoring combine plug-in in NEMO-Cmd.
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
