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
Participated in Phys Ocgy seminar where Elise practiced her talk and some of the rest os us previewed our posters.
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
(SalishSea)

Participated w/ Susan & Elise in summer student RA interview.


ToDo
====

* Fix nowcast-green watch_NEMO logging
* refactor, unit tests & docs for forcing links checking for NEMO-3.6
* update quick-start docs re: NEMO-3.6 - Elise???

* get HTTPS working for alternate sealinkd app domain names
* reduce resolution of landing page images for faster load times
* add docs re: sealinkd server-side app framework
* add EduCloud deployment docs

* update storm surge paper refs w/ doi link - need issue details
* research_ferries module
* JSON logging use example notebook

* review remaining nosy PRs
