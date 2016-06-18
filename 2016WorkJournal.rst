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


ToDo
====

* docs re: stdout & stderr on salish
* Rotate winds in research forecasts prior to 7apr16
* Fix nowcast-green watch_NEMO logging
* refactor, unit tests & docs for forcing links checking for NEMO-3.6

* reduce resolution of landing page images for faster load times
* add docs re: sealinkd server-side app framework
* add EduCloud deployment docs

* research_ferries module
* JSON logging use example notebook

* review remaining nosy PRs

* update darktable and zeal for 16.04
