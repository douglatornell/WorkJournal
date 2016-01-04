*****************
2015 Work Journal
*****************

This is my public work journal.
It is patterned after one that I have kept for several years for my work at Nordion_.
This journal is about:

* my work as a Research Software Engineer with `Dr. Susan Allen`_ in the `Department of Earth, Ocean and Atmospheric Sciences`_ at the `University of British Columbia`_
* my freelance work via my consulting business,
  `43ravens`_
* my `open-source activities`_

There was a hiatus in my journaling between Fri 17-Oct-2014 and Wed 27-May-2015 - sorry!


May
===

Week 22
-------

Wed 27-May-2015
^^^^^^^^^^^^^^^


June
====

Week 23
-------

Mon 1-Jun-2015
^^^^^^^^^^^^^^

CMOS conference in Whistler.

Tue 2-Jun-2015
^^^^^^^^^^^^^^

CMOS conference in Whistler.
Presented "Automation Framework for a Regional Ocean Forecast Model" talk.


Wed 3-Jun-2015
^^^^^^^^^^^^^^

CMOS conference in Whistler.


Thu 4-Jun-2015
^^^^^^^^^^^^^^

CMOS conference in Whistler.


Week 24
-------

Mon 8-Jun-2015
^^^^^^^^^^^^^^

Visiting Oslo for Susan to participate in a PhD exam.

Started preparation for version control workshop for MEOPAR 2015 ASM MEOPeers training program.
Re-mixed content, layout, and workflow from SWC hg-novice lesson.


Tue 9-Jun-2015
^^^^^^^^^^^^^^

Visiting Oslo for Susan to participate in a PhD exam.

Continued preparation for version control workshop for MEOPAR 2015 ASM MEOPeers training program.


Sun 14-Jun-2015
^^^^^^^^^^^^^^^
Finished preparation for version control workshop for MEOPAR 2015 ASM MEOPeers training program.


Week 25
-------

Mon 15-Jun-2015
^^^^^^^^^^^^^^^

Delivered version control workshop for MEOPeers as part of MEOPAR 2015 ASM training program.
(MEOPAR)


Tue 16-Jun-2015
^^^^^^^^^^^^^^^

MEOPAR 2015 ASM in Vancouver.


Wed 17-Jun-2015
^^^^^^^^^^^^^^^

MEOPAR 2015 ASM in Vancouver.


Thu 18-Jun-2015
^^^^^^^^^^^^^^^

MEOPAR 2015 ASM in Vancouver.


Week 26
-------

Fri 26-Jun-2015
^^^^^^^^^^^^^^^

Helped Jie get her Westgrid account access sorted out.
Had email discussion w/ Youyu about timeframe for DFO/CONCEPTS collaboration.
(MEOPAR)


Sat 27-Jun-2015
^^^^^^^^^^^^^^^

Discovered that nowcast system failed between nowcast and forecast runs on 24-Jun; get_NeahBay_ssh worker failed because it couldn't write its raw data text file to forecast/24jun15/ directory.
(MEOPAR)

Set up conda env for randopony; pleasantly surprised to find that Pyramid is packaged for conda.
(RandoPony)


Sun 28-Jun-2015
^^^^^^^^^^^^^^^

Tried to get 2015r1 release running on webfaction but encountered issues with persona login and deform widgets; both appear to be due to changes in versions of those packages that have been released since 2013r3 was deployed.
(RandoPony)


July
====

Week 27
-------

Mon 29-Jun-2015
^^^^^^^^^^^^^^^

Started recovery from 24-Jun nowcast failure with Susan's help preparing runs on orcinus.
Telcon w/ Youyu re: DFO/CONCEPTS collaboration.
Helped Jie get her salishsea environment set up on orcinus.
(MEOPAR)


Tue 30-Jun-2015
^^^^^^^^^^^^^^^

Completed recovery from 24-Jun nowcast failure with Susan's help preparing runs on orcinus.
(MEOPAR)


Wed 1-Jul-2015
^^^^^^^^^^^^^^

Added SMTP logging handler to nowcast to send email to all group members when a CRITICAL level message is logged.
(MEOPAR)

Pushed SoG-bloomcast intro page to salishsea site.
(Bloomcast)


Thu 2-Jul-2015
^^^^^^^^^^^^^^

Worked on cleanup of SalishSeaTools nowcast package in preparation for moving it to SalishSeaNowcast.
Started refreshing Salish Sea nowcast development, deployment & testing docs.
(MEOPAR)


Fri 3-Jul-2015
^^^^^^^^^^^^^^

Continued refreshing Salish Sea nowcast development, deployment & testing docs.
(MEOPAR)

Week 27
-------

Mon 6-Jul-2015
^^^^^^^^^^^^^^

Continued refreshing Salish Sea nowcast development, deployment & testing docs.
(MEOPAR)

Tue 7-Jul-2015
^^^^^^^^^^^^^^

Salish Sea team meeting; see Google Drive Drawing.
(MEOPAR)

Wed 8-Jul-2015
^^^^^^^^^^^^^^

Finished refreshing Salish Sea nowcast development, deployment & testing docs.
Fixed several autodoc issues, especially mocking a value for numpy.pi for nowcast.figures module.
(MEOPAR)


August
======

Week 32
-------

Tue 3-Aug-2015
^^^^^^^^^^^^^^

First day as paid UBC staff.

Delivered benefits forms to Cary.
Requested furniture for office I'm sharing with Melanie Grenier.

Worked on getting NEMO-3.6 running on jasper.
Opened ticket INC0507507 on westgrid re: very outdated Mercurial version (1.4 vs 3.5 present).
Reviewed ~90 NEMO-3.6-stable changesets from r5258 to present (r5628) (see NEMO changesets spreadsheet on Google Drive).
Started work on changing svn base of NEMO-3.6-hg-mirror repo from http://forge.ipsl.jussieu.fr/nemo/svn/trunk to http:////forge.ipsl.jussieu.fr/nemo/svn/branches/2015/nemo_v3_6_STABLE
(MEOPAR)

Salish Sea team meeting; see Google Drive Drawing. Todos:
* tag change to iso-neutral mixing
* sort out NEMO-3.6 build & run MPI issues viz-a-viz anaconda


Wed 4-Aug-2015
^^^^^^^^^^^^^^

Helped Susan try to understand how NEMO-3.6 and XIOS are using cores on salish re: why 7+1 and 15+1 runs have almost the same duration.
Confirmed that newly installed Mercurial v3.5 on jasper works by updating all MEOPAR repos there.
Updated build of NEMO-3.6 on jasper, and added docs section describing arch file and build command.
(MEOPAR)

Started writing proposal for UBC SCARP SeaLink'd web app project.
(sealinkd)


Thu 6-Aug-2015
^^^^^^^^^^^^^^

Started running NEMO-3.6 tests on jasper; missing input files seem to result in segfaults - hostile!
After getting the input file issues sorted out, the run failed with an integer division error that leave no trace in ocean.output; Susan took over debugging that.
(MEOPAR)

Lat/lon and timecounter bug fixes in GEM2.5 research model output took effect today.
(MEOPAR)

Got ocean mount on bjossa reset, restarted buildbot master, and all slaves.
(SOG)


Fri 7-Aug-2015
^^^^^^^^^^^^^^

Continued working on getting NEMO-3.6 running on jasper:
* Tried 6x14 run with attached XIOS; failed due to memory limits
* Did a series of walltime=00:05:00 test:
    * From 1x7+1 test run, learned that XIOS buffer must be >= 48906418, so set it to 50000000
    * 1x7+1 test with and procs=7 ran 10+ time steps
    * 1x7+1 test with nodes=1:ppn=12 ran 27+ time steps
    * 2x5+1 test with nodes=1:ppn=12 ran 35+ time steps
    * 4x9+3 test with nodes=13:ppn=12 ran 215+ time steps (28m40s model/min)
    * 8x18+12 test with nodes=13:ppn=12 ran 805+ time steps (107m20s model/min)
* Increased walltime to 30m hoping to complete the 1 model day:
    * 8x18+12 test with nodes=13:ppn=12 ran + time steps (107m42s model/min)
* Experimented on number of XIOS servers:
    * 8x18+6 test with nodes=13:ppn=12
    * 8x18+3 test with nodes=13:ppn=12
    * 8x18+4 test with nodes=13:ppn=12 had some 30% performance ratios and lots of 8% ones
    * 8x18+1 test with nodes=13:ppn=12 took 48m52, or which 35m was output file writing, and XIOS performance ratio was >98% (very bad) for all opa processors
Updated docs re: Mercurial 3.5 on jasper.
(MEOPAR)

Participated in canyons group mtg; todos:
* help Karina get ssh keys setup for all the things
* build MITgcm on orcinus and test it with its repo rotating table test case; write docs
* develop a canyon command processor for MITgcm similar to the salishsea command processor for NEMO
Started setting up canyons workspace on tom and orcinus; did CVS checkout of MITgcm HEAD on both.
(Canyons)

Got UBC staff card :-)


Sat 8-Aug-2015
^^^^^^^^^^^^^^

Continued NEMO-3.6 tests on jasper:
* 8x18p1 w/ 6h output ran in 13m39s
Wrote docs re: run setup outside of NEMOGCM/CONFIG/SalishSea/EXP00/ and tested them with 8x18p6 w/ 6h output, but had lots of fails in run.
(MEOPAR)

Re-implemented eFunds.py in Python 3 and created private Bitbucket repo for the project.


Sun 9-Aug-2015
^^^^^^^^^^^^^^

Continued NEMO-3.6 tests on jasper:
* 8x18p6 w/ 6h output


Week 33
-------

Mon 10-Aug-20156
^^^^^^^^^^^^^^^^

Continued refining NEMO-3.6 run environment on jasper:
* Tested mpirun -np 144 ./nemo.exe : -np 6 ./xios_server.exe syntax; worked
* Repeated 8x18p1 1d w/ 6h output in non-EXP00 directory; timed out at 20m on 1st try, but ran in 13m16s on wnd try w/ PBS feature=X5675
(MEOPAR)

Susan confirmed 22-25 Sep, 9-12 each day as dates for EOAS SWC workshop.
Invited Julia to join the teaching team, but she declined, though offered to come as a helper on day 1.
(SWC)

Attended Phys Ocgy seminar by Mark Halverson about surface tides.

Finished writing 1st draft of proposal for UBC SCARP SeaLink'd web app project.
(sealinkd)


Tue 11-Aug-2015
^^^^^^^^^^^^^^^

Updated jasper NEMO-3.6 and SS-run-sets to Susan's most recent near-production configuration, re-built NEMO, and tested:
* 8x18p1-1d-6h: completed NEMO in 19m, but timed out at 1h on XIOS
* 8x18p1-1d-6h again: queued ETS 23:00
* 8x18p2-1d-6h again: queued ETS 23:30
Resumed trying to build XIOS and NEMO on orcinus.
Met w/ Nancy & Muriel re: transition of ONC ADCP data gathering code at end of Muriel's term.
Tried to help Elise with borked NEMO-code dir; no go.
Worked on getting XIOS to build on orcnius; down to 1 undefined symbol; need to ping Roman again.
Started pulling upstream changesets in to NEMO-3.6.
Salish Sea team meeting; see Google Drive Drawing.
Helped Jie figure out an approach to rebuilding per-processor files from zoomed sub-domains.
(MEOPAR)

Attended special Phys Ocgy seminar by Julio Sheinbaum (Karina's "father-in-law") on Gulf of Mexico.


Wed 12-Aug-2015
^^^^^^^^^^^^^^^

Discovered that sloppy, subtle use of tag closings in iodef.xml resulted in all test jobs to date on jasper doing 1h output.
Overnight:
* 8x18p1-1d-6h again: actually 8x18p1-1d-1h took 19m22s
* 8x18p2-1d-6h again: actually 8x18p2-1d-1h took 28m28s
Fixed tag closing issue.
* 8x18p2-1d-6h: 17m32s
Continued pulling upstream changesets in to NEMO-3.6; up to r5518.
(MEOPAR)

Investigated randopony persona.org sign-in issue discovered on 28Jun and found that it is not a problem today - weird.
Investigated deform widgets issue discovered on 28Jun; on kudu it is resolved by downgrading to deform==0.9.9.
Updated deployment to 2015r1 release; lots of manual work because of fabric security issue that seems to be about my local userid not matching the bcrandonneur userid on webfaction.
Explored Unicode handling issue in brevet pre-registration and discovered that it is in the email generation functions, not the form handlers.
(RandoPony)

Finalized proposal for UBC SCARP SeaLink'd web app project and emailed it to Stephanie.
(sealinkd)

After a  lot of mucking about to figure out which packages I hadn't yet installed, got enough TeX and LaTeX packages and fonts installed to render sealinkd proposal from rst to pdf via both rst2latex and pandoc; former produces nicer output, presumably due to deficiencies in pandoc's rst parser; e.g. no generic role (:data:) handling.


Thu 13-Aug-2015
^^^^^^^^^^^^^^^

Worked on migrating Muriel's ONC ADPC processing to group operability.
(MEOPAR)

Attended SWC workout session on Pandas lead by Nancy.
(SWC)

Met w/ Susan and Charles re: setting up a server for OPeNDAP and dynamic web sites and arrived at a provisional plan for a new 6 core, 6Tb storage machine to be located in the UBC data centre.

Got key to my EOSM office and discovered that furniture has been moved in for me.


Fri 14-Aug-2015
^^^^^^^^^^^^^^^

Finished migrating Muriel's ONC ADPC processing to group operability in /ocean/dlatorne/MEOPAR/ONC_ADCP/; discussed future use and coordination w/ Rich.
Emailed Diego re: OceanViewer and planned OPeNDAP server for Salish Sea NEMO model results.
(MEOPAR)

Moved into office in EOS Main.


Sun 16-Aug-2015
^^^^^^^^^^^^^^^

Nowcast automation failed due to west.cloud sshfs storage quota being exceeded.
Manually deleted enough files to get things running again, and manually re-started via the upload_forcing worker.
Worked on cron job to automatically delete run results more than 30 days old, but struggled with getting the script to run from cron - perhaps because it is stored in the tools repo which is on the sshfs mount?
(MEOPAR)

Experimented with Mercurial bookmarks and named branches in a toy repo and on Bitbucket.


Week 34
-------

Mon 17-Aug-2015
^^^^^^^^^^^^^^^

Worked on setting smelt up as a daily use machine.

NEMOGCM/NEMO/OFF_SRC/domain.F90 conflict remains
Nowcast automation failed again due to west.cloud sshfs storage quota being exceeded.
Finally got cron job to automatically delete run results working; set it to delete results directories more than 20 days old every day at midnight.
The trick to getting it working is that the script from /MEOPAR/tools/... had to be symlinked into $HOME - weird.
Switched NEMO-3.6-hg-mirror svn URL to ^/branches/2015/nemo_v3_6_STABLE; svn r5519 is the creations of that branch and produces no changeset in Mercurial.
svn revisions 5531, 5533, 5540, 5546, and 5550 seem to be from another branch and it is not clear how/if they enter the 3.6-stable branch.
Finished pulling upstream changesets in to NEMO-3.6-hg-mirror; it is now at svn r5628.
Merged NEMO-3.6-hg-mirror and NEMO-3.6-code, then tagged the latter at NEMO-3.6r5628 and pushed so that the update to 3.6-stable is finished.
Fixed bugs in the /ocean/dlatorne/MEOAPR/ONC_ADCP/east/ setup with help from Nancy and Muriel.
(MEOPAR)

Continued experiment with Mercurial named branches by confirming that when Susan cloned the test repo she got both branches; also updating to a branch tip by rev number puts you on the branch.

Confirmed that bugaboo is up, so MITgcm build can wait for a day or 2.
(canyons)


Tue 18-Aug-2015
^^^^^^^^^^^^^^^

Stephanie accepted my SeaLink'd web app proposal and is proceeding with a Supply Agreement.
(sealinkd)

Pinged Youyu re: travel funding for MEOPAR-CONCEPTS workshop & visit to Halifax; deadline for decision is tomorrow.
Bedford contract folks have confirmed that 43ravens is set up on the standing offer list in a way that they can work with.
(CONCEPTS)

Updated salishsea-site to include Elise as a Salish Sea NEMO model team member, and Jie as a site content contributor.
Investigated compilation error that Susan is seeing in NEMO-3.6-stable; looks ugly.
Started work on SalishSeaCmd package update to Python 3 and NEMO-3.6 in tools/SalishSeaCmd-3.6 named branch.
Started backing out object-based Nowcast commits in tools repo in preparation for re-doing them in a named branch.
Salish Sea team meeting; see Google Drive Drawing.
(MEOPAR)


Wed 19-Aug-2015
^^^^^^^^^^^^^^^

More investigation of NEMO-3.6-stable compilation error in light of Fatemeh's 31Jul message to the NEMO list suggests that we need to update our XIOS-1.0 checkout (because the developers have committed ~37 changesets since our checkout - is it too much trouble for them to create releases and coordinate with NEMO?)
Created tools repo issues for several todos that I had set up reminders for in my Inbox.
(MEOPAR)

Updated CHANGES.txt file that I forgot to do prior to the 2015r1 release.
Changed version number scheme to be PEP-440 compliant.
Bumped version to 2015.2.dev0.
Worked on mods to properly handle Unicode characters in brevet riders' names.
Created new 2015.2 staging deployment on webfaction (manually due to fabric userid/ssh-key issue) to test Unicode mods through real email servers and agents.
(RandoPony)


Thu 20-Aug-2015
^^^^^^^^^^^^^^^

Confirmed to Hal, Youyu, et al that I will not be attending the MEOPAR-CONCEPTS collaboration workshop at Dorval next week.
Worked on NEMO-3.6 and XIOS build issues.
Grabbed up-to-date (svn r648) version of XIOS-1.0 branch and successfully compiled it on salish; compile fails on smelt due to lack of OpenMPI library - a watchout for people with anaconda in their path (I think).
Update XIOS repo to svn r648, merged our arch files, etc., and tagged it as XIOS-1.0r648.
Updated docs re: NEMO-3.6 and XIOS build issues.
Finished backing out NowcastWorker worker & unit test module commits in tools repo in preparation for re-doing them in the nowcast-obj named branch.
Explored ONC data web app; ADCP data appears to be available in real-time.
Did Python 3.4 porting & cleanup on SalishSeaCmd package, and added `--nemo3.4` command line option to `salishsea prepare` parser.
(MEOPAR)

Sent email to Ben re: problems getting builbot running on bjossa salvage hardware; included path to most recently created comparison plots PDFs.
(SOG buildbot)

Sent kick-off email w/ copy of Sealinkd app proposal to Stephanie group.
1st review/feedback mtg scheduled for 1-Sep.
(sealinkd)

Did a tour of waterhole/ocean machines and found that all but salish and snapper are running 12.04; no ssh key access to fraser, and no access at all to glider.


Fri 21-Aug-2015
^^^^^^^^^^^^^^^

Started work on Sealinkd web app project.
Created Sealinkd team and sealinkd repo on Bitbucket.
Set up sealinkd repo issue tracker milestones & components, and translated stage 1 section of proposal into task issues.
Set up docs framework, and wrote initial developer information section.
Started setup of back-end framework.
(sealinkd)


Sat 22-Aug-2015
^^^^^^^^^^^^^^^

Tried to set up remote desktop access on kudu to waterhole/ocean machines; missing something.

Experimented with a bcrandonneur account on kudu and a doug account on web faction, but didn't find a satisfactory resolution for the fabric auth issue.
bcrandonneur account can auth, but lacks access to desktop on kudu.
Finished writing unit tests for mods to properly handle Unicode characters in brevet riders' names; next up, populaire riders.
(RandoPony)


Sat 22-Aug-2015
^^^^^^^^^^^^^^^

Continued work on SalishSeaCmd-3.6 branch; added lots of unit tests, the --nemo3.4 command-line option, and started propagating it through the prepare module.
(MEOPAR)


Week 35
-------

Mon 24-Aug-2015
^^^^^^^^^^^^^^^

Worked on sprint planning.
(MEOPAR)

Added skeleton implementations of site-wide page banner, navbar, nav tabs for maps/charts/profiles pages, and Javascript functions to manage highlighting of nav elements.
(sealinkd)

Tue 25-Aug-2015
^^^^^^^^^^^^^^^

Participated in sprint re: Salish Sea NEMO model stakeholder issues.
(MEOPAR)


Wed 26-Aug-2015
^^^^^^^^^^^^^^^

Shadowed by Katie.

Reviewed yesterday's sprint commits in tools repo and decided to pull them into nowcast production; need to talk to Jie (for sure), Ben & Elise (both maybe) about PEP8.
Received email from Marlene@OCN re: search failure in ADCP cron job saying that script access to the data was not supported.
Investigated west.cloud disk quota failure in 24aug15 forecast run; rebuild failed during 1d/restart files, but 1h files appear to be good (though maybe not LZ-compressed), so web page figures are okay.
get_NeahBay_ssh worker failed due to permissions because I accidentally committed nowcast.yaml w/ a path that we used for testing Elise's worker mods during the sprint.
make_plots worker failed because I forgot to install scikit-learn package that got introduced as a dependency in the research_ferries.py module from yesterday' sprint; ran make_plots nowcast research and make_plots forecast publish manually late in the afternoon to get things back on the rails.
Wrote ToDo lists into sprint tasks doc on Google Drive re: task required to move sprint work into nowcast system.
(MEOPAR)

Added fly-make/flake8 config to emacs on ocean/waterhole machines; need to get ~/.local/bin/ on to path at desktop login.

Received email from Jerry@Nordion re: boot failure on production server.
(Nordion)

Participated in GEOTRACES team mtg.
(GEOTRACES)


Thu 27-Aug-2015
^^^^^^^^^^^^^^^

Replied to Marlene's email re: script access to ADCP data and sparked a discussion among EOAS & ONC re: availability of data via web service.
Updated contributors lists in docs repo and on salishsea site w/ names from this week's sprint.
Updated XIOS repo on orcinus and tried a build; fails with 1 unresolved symbol:
/global/software/lib64/intel/ncsa-tools/mpi/lib/libnetcdf.so: undefined reference to `H5Pset_fapl_mpiposix'
(MEOPAR)

Offered Nordion site visit next week to try to resolve production server /backup partition issue.
(Nordion)

Received provisional approval of SealinkD proposal from UBC Procurement via Penny@SCARP; Procurement wants the finished app to be hosted on the UBC VM service, and webfaction deleted from the proposal.
(Sealinkd)

Sent email to Cary for help w/ CWL sign-up PIN.

Started moving ocean machine configuration files in my dotfiles repo.

Participated in SWC workout session on make lead by Susan.

Sent email to Cindy & Kyle re using REBUILD_NEMO.
(GEOTRACES)


Fri 28-Aug-2015
^^^^^^^^^^^^^^^

Email w/ Stephanie re: proposal amendments, Bitbucket account for her, and in-progress deployment on webfaction.
Experimented with static page content on About page.
Emailed team re: setting up Bitbucket accounts and sending me their userids so that I can added them to the SealinkD team.
Did skeleton implementation of sign-in re: visibility of maps/charts/profiles nav tabs.
Implemented alternative nav layout w/ About drop-down & maps/charts/profiles as navbar items instead of nav tabs.
Implemented alternative layout of About items as a single page.
Added CJ to SealinkD team on Bitbucket.
(sealinkd)

getNeahBay_ssh worker failed to produce an observations file for forecast2 and for nowcast; let the former pass, but symlinked forecast file as observations for nowcast and restarted automation via upload_forcing worker.
(MEOPAR)


Sat 29-Aug-2015
^^^^^^^^^^^^^^^

Added placeholder content to Research, People, Contact & Privacy Policy pages & sections of alternative About page.
(sealinkd)

Researched WorkSafeBC coverage; not required for 43ravens as sole-proprietorship, but eligible for voluntary POP.

getNeahBay_ssh worker failed to produce an observations file for forecast2 and for nowcast; let the former pass, but symlinked forecast file as observations for nowcast and restarted automation via upload_forcing worker.
Resolved issue #22 re: handling missing ssh obs files; upload_forcing and upload_all_files workers create symlinks to corresponding fcst/ file if obs is missing, and get_NeahBay_ssh worker deletes obs/ file before writing in order to avoid overwriting fcst/ file if observations become available.
(MEOPAR)

Telcon w/ Jerry re: resolving production server /backup partition issue, and him contracting work to 43ravens.
(Nordion)


Sun 30-Aug-2015
^^^^^^^^^^^^^^^

Added Tugce to SealinkD team on Bitbucket.
Revised proposal re: using UBC IT VM Service as final hosting service and sent it to Stephanie for approval.
(sealinkd)

Sent email to westgrid support requesting Python 3.4 be installed on jasper.
Sent email to Roman re: libnetcdf.so undefined symbol in XIOS build on orcinus.
Started work on creating an arch file and building NEMO-3.6 on orcinus.
Continued work on SalishSeaCmd-3.6 branch; added more unit tests & docstrings, and continued propagating the --nemo3.4 command-line option through the prepare module.
(MEOPAR)


September
=========

Week 36
-------

Mon 31-Aug-2015
^^^^^^^^^^^^^^^

Email from Stephanie confirmed her acceptance of the revised proposal, and my plan to do an initial deployment on webfaction.
Set up sealinkd.43ravens.ca on webfaction, thrashed through getting the app deployed in a Python 3.4 and mod_wsgi environment.
Wrote email re: tomorrow's mtg w/ the SCARP team.
(sealinkd)

Met w/ Nancy & Karina to plan the EOAS workshop.
(SWC)

Attended seminar by Aranildo Lima about art, science, and the prog rock album that he is developing based on the climate change literature.

Melanie returned to EOAS after the GEOTRACES cruise.

Tue 1-Sep-2015
^^^^^^^^^^^^^^

Prep for mtg w/ SCARP group.
Met w/ UBC SCARP team (Jackie, CJ, Tugce & Michelle); finalized navigation & page layouts, and made decisions about user mgmt data model and sign-up process.
(sealinkd)

Worked on MITgcm build process on orcinus, and docs for it.
(Canyons)

Met w/ Nancy & Karina to plan 22-25 Sep EOAS workshop.
(SWC)

Salish Sea team meeting; see Google Drive Drawing.
(MEOPAR)


Wed 2-Sep-2015
^^^^^^^^^^^^^^

Buffed MITgcm on orcinus build docs, and passed the process over to Karina for testing.
(canyons)

Site visit to Nordion to recover from isoinfo production server boot failure due to corruption of the /backup filesystem.
Discussed possible service contract arrangement between 43ravens and Nordion with Jerry.
(Nordion)

Refactored navigation and page layouts to reflect decisions taken at 1-Sep meeting with UBC SCARP team.
Implemented skeleton of Start page that initializes the maps/charts/profiles flow for signed in users.
(sealinkd)


Thu 3-Sep-2015
^^^^^^^^^^^^^^

Created invoice for 2-Sep site visit to Nordion and emailed it to Jerry.
(Nordion)

Started setting up web site for EOAS workshop and sent email to admin to get it listed on the swc site.
(SWC)

Continued work on SalishSeaCmd-3.6 branch; added more unit tests & docstrings, and continued propagating the --nemo3.4 command-line option through the prepare module.
Tested Python 3.4 on jasper; successfully installed SalishSeaCmd v2.0dev0.
13:00 to
(MEOPAR)


Fri 4-Sep-2015
^^^^^^^^^^^^^^

Kayaking at Deep Cove.


Sat 5-Sep-2015
^^^^^^^^^^^^^^

Pulled in Jackie's Research page content, cleaned it up, added images that she provided, and deployed to demo site.
Updated issues on Bitbucket re: 1-Sep mtg decision to put About, Research, Contact, and Privacy Policy content on separate pages.
(sealinkd)

Disabled ONC ADCP observation download cron job pending testing and installation of matlab script from Marlene for new deployments.
Continued work on SalishSeaCmd-3.6 branch; added more unit tests & docstrings, and continued propagating the --nemo3.4 command-line option through the prepare module.
(MEOPAR)


Sun 6-Sep-2015
^^^^^^^^^^^^^^

Hiking in Golden Ears Park - Allouette Mtn trail.


Week 37
-------

Mon 7-Sep-2015
^^^^^^^^^^^^^^

Labour Day

Learned more about Darktable imports by playing with images from Sylus 6020 camera; seems best to copy them from SD to disk via SD reader on kudu rather than importing from camera.

Learned of Hai Yun's lost prop; worked on logistics of getting a new prop to them.

Did iniital implementations of skeletons of Maps and Analysis pages.
(sealinkd)


Tue 8-Sep-2015
^^^^^^^^^^^^^^

Did code and docstring gardening on research_ferries.py module; started with autopep8 and docformatter, then did manual tweaks; halted when I realized that the functions contain hard-coded paths that need to be changed to args.
(MEOPAR)

Continued tuning up the workshop site.
Met w/ Nancy & Karina to continue planning workshop. Observed by Katie.
(SWC)

Salish Sea team meeting; see Google Drive Drawing. Observed by Katie.
(MEOPAR)


Wed 9-Sep-2015
^^^^^^^^^^^^^^

Implemented swapping of maps between main panel and sidebar on Maps page skeleton.
Added comparison community links to Analysis page skeleton.
Did initial implementation of Compare and Profiles page skeletons.
(sealinkd)

Telcon w/ Nathan re: coastal flooding web app proposal.


Thu 10-Sep-2015
^^^^^^^^^^^^^^^

Finished prep for workout session about pdb, and delivered it with lots of crappy bugs :-(
(SWC)

forecast2 result download failed due to disk quota exceeded on ocean/sallen/;
restarted manually mid-afternoon after Susan and Nancy freed up some space.
Manually rebuilt results files from botched forecast/24aug15/ run, then manually re-ran the rest of the post-processing steps on smelt.
Manually ran make_plots and make_site_page workers for nowcast/23jul15 and nowcast/15jun15 results because the plots and pages somehow didn't get made.
(MEOPAR)

Got buildbot and tracd running again on new bjossa hardware.
(SOG)

Created slides for next week's Phys Ocgy Research Carnival.


Fri 11-Sep-2015
^^^^^^^^^^^^^^^

Sent slides for next week's Phys Ocgy Research Carnival to Jie.

Investigated forecast2/10sep15 run failure this morning; appears to have been caused by in appropriate clearing of the nowcast_mgr checklist when I downloaded the forecast2/09sep15 results "live" yesterday.
Looked at research_ferries module wrt refactoring hard-coded paths out to arguments and realized that deeper refactoring is necessary; bounced to Susan the decision about whether I should do it, or work w/ Jie to get it done.
Continued work on SalishSeaCmd-3.6 branch; added more unit tests & docstrings, and continued propagating the --nemo3.4 command-line option through the prepare module; salishsea prepare command is ready for testing by Susan and Nancy.
(MEOPAR)

Investigated buildbot failures since re-start of bjossa; R3 baseline regression case is failing due to a dependency issue for matplotlib (presumably due to snapper's upgrade to Ubuntu 14.04 LTS), and SOGCommand-coho is failing due to package installation issues.
Sent email to Susan and Ben to determine priority for fixing those issues.
(SOG)

Sent email re: resolution of mess between ipdb install and ipython-notebook package for yesterday's workout.
(SWC)


Sat 12-Sep-2015
^^^^^^^^^^^^^^^

Fixed specificity of jQuery selectors for navbar items re: enabling maps/analysis/compare/profiles items and updating their anchor hrefs.
(sealinkd)

Attended VanPyDay; talked w/ Jordan Dawe, Michelle Bannister, Brett & Andrea Cannon, Damien from Centre for Disease Control, Russell Keith-Magee, and other.

Tested use of conda environments on jasper and orcinus.
SalishSeaCmd-3.6 is usable on jasper via conda environment, the the hg interface a little fragile.
Started updating SalishSeaCmd docs, and started writing a Bitbucket snippet about conda environment setup for testing on jasper.
(MEOPAR)


Sun 13-Sep-2015
^^^^^^^^^^^^^^^

Walked in Serpentine River wildlife area, and Burns Bog nature preserve.


Week 38
-------

Mon 14-Sep-2015
^^^^^^^^^^^^^^^

ESB power outage.

Pinged Stephanie & Penny about status of SealinkD project agreement and got reply that UBC Procurement are working on it.
(sealinkd)

Mostly finished tuning up the workshop site, and the setup check scripts.
(SWC)

Participated in Phys Ocgy Reseach Carnival to kick off this term's seminars.

Backfilled 11Sep GEM2.5 research forecast download.
Added functionality to salishsea prepare command to update namelist with MPI decomposition specified in the YAML run description file.
(MEOPAR)


Tue 15-Sep-2015
^^^^^^^^^^^^^^^

Prep for mtg w/ SCARP group.
Met w/ UBC SCARP team (Jackie, Tugce & Michelle); reviewed and refined navigation & page layouts.
(sealinkd)

Met w/ Nancy & Karina to continue planning workshop.
(SWC)

Explored DFO water level web service to get real-time tide gauge data for various Salish Sea sites; SOAP.
Started to look at adding --nemo3.4 command-line option to salishsea run and make it work for NEMO-3.6.
Salish Sea team meeting; see Google Drive Drawing.
Helped Jie get new make_readme.py instances working, and helped her get ssh keys set up properly.
(MEOPAR)


Wed 16-Sep-2015
^^^^^^^^^^^^^^^

Continued work on SalishSeaCmd-3.6 branch:
Fixed failing unit tests for salishsea prepare re: addition of MPI decomposition handling.
Added unit tests & docstrings, started propagating the --nemo3.4 command-line option through the run plug-in module, and worked toward a better API structure for the run module.
(MEOPAR)

Booked mtg rm for final workshop prep mtg, and projector/MacBook for workshop.
Closed 2 open pull requests in SWC hg-novice repo and pulled those changes into my working fork, and the EOAS workshop copy.
Refactored 01-backup section of hg-novice lesson into 8 sections based on content from the git-novice lesson and my MEOPAR ASM workshop; create PR #22 in swcarpentry/hg-novice for v5.4 w/ the result of that work.
Started refactoring the 02-collab section.
(SWC)

Got email from MEOPeer Patrick Duplessis @dal re: using MEOPAR ASM version control workshop site as basis for a tutorial that he is creating.


Thu 17-Sep-2015
^^^^^^^^^^^^^^^

Tried to add Stephanie to Bitbucket Sealinkd team and discovered that it is limited to 5 collaborators, probably because it was created from my non-academic account.
(sealinkd)


Fri 18-Sep-2015
^^^^^^^^^^^^^^^

Finished refactoring the 02-collab section of the hg-novice lesson to the extent that needs to be done for next week's workshop; same for 03-conflict, and 04-open sections.
Created PR in Python lesson repo to add command reminders page & docs links.
(SWC)

Upgraded SealinkD Bitbucket team account to 10 private collaborators.
(sealinkd)


Sat 19-Sep-2015
^^^^^^^^^^^^^^^

Continued work on SalishSeaCmd-3.6 branch:
Improved docstrings in the run plug-in module.
Wrote unit tests for run plug-in and got number of processors from run description file instead of from namelist.
(MEOPAR)


Sun 20-Sep-2015
^^^^^^^^^^^^^^^

Continued work on SalishSeaCmd-3.6 branch:
Changed nodes & ppn calculation for jasper to be based on number of processors instead of being read from run description.
Started testing run plug-in on jasper.
(MEOPAR)

Helped Nancy try to debug a Unicode issue in the shell lesson build process.
Created slide deck for workshop introductory remarks.
Had productive discussion in hg-novice PR #22 w/ John Corless re: adding reference links to lesson index page.
(SWC)

Discovered that tom lacks a TeX installation; downloaded MacTeX-2015, and installed it.


Week 39
-------

Mon 21-Sep-2015
^^^^^^^^^^^^^^^

Re-organized office furniture to make way for locking 2-drawer cabinet.

Continued testing salishsea run plug-in on jasper.
Tried to sort out module load commands on jasper for Python 3; PYTHONPATH seems to consistently end up with a bogus 3.4/2.7/site-packages path, but it is unclear if that is a problem.
(MEOPAR)

Added prompts & exits page to shell lesson.
Buffed hg slides for remote repos, collaboration, merging & conflicts.
Met w/ helpers for briefing, Nancy & Karina for final prep.
(SWC)


Thu 24-Sep-2015
^^^^^^^^^^^^^^^

Received PO from UBC for SealinkD app project.
(sealinkd)


Fri 25-Sep-2015
^^^^^^^^^^^^^^^

Day 4 of EOAS workshop; Nancy taught Python functions, I taught tracebacks and exceptions, and Karina taught Python command-line scripts.
(SWC)

nowcast results download failed due to full /data/ partition on salish; got some space cleared and nowcast back in operation later in the afternoon.
Met w/ Roman re: building XIOS on orcinus; convinced him that libnetcdf.so needs to be re-built to deal with a symbol that was removed from the HDF5 lirbary.
(MEOPAR)

Last Friday of the Month Club :-)


Sat 26-Sep-2015
^^^^^^^^^^^^^^^

Craft brewery bike crawl for Keith's 60th birthday.


Sun 27-Sep-2015
^^^^^^^^^^^^^^^

Continued working getting salishsea run to work for NEMO-3.6 runs on salish and jasper; successful to the combine stage where we now have to deal with single tile sub-domain files that have _0000.nc endings.
(MEOPAR)


Week 40
-------

Mon 28-Sep-2015
^^^^^^^^^^^^^^^

Worked on items that arose from 15Sep2015 mtg w/ UBC SCARP group:
* buffed Research page layout
* added Help page to app & nav, and created skeleton content & layout
* started implementation of flow links on HSVI pages to guide users through basic flow
Received HVSI data spreadsheet from Jackie.
Agreed with Jackie to postpone the next review/feedback mtg until next week.
(sealinkd)

Phys Ocgy seminar by Ben S on his glider adventures and micro-scale turbulence in the Arctic.

Ordered Lemur from System 76.

Drafted response to Nathan's inundation proposal & estimate request for a web app.

Researched whether or not NCO could be used to combine per-processor NEMO output files into whole domain results files; not easily.
Wrote new tools docs about `ncks -4 -L4` command to apply variable -level LZ compression to NEMO output files.
Discussed setup of skookum server w/ Charles; decided to use virtual hosts for DAP service and salishsea site rather than VMs so that resources are used more flexibly.
Discussed nowcast run times on west.cloud and Susan's idea to make calculation of run times less labourious.
(MEOPAR)


Tue 29-Sep-2015
^^^^^^^^^^^^^^^

Pulled updates on to west.cloud that change namelist.dynamics rn_avm0 value to 1e-5; tagged SS-run-sets repo to make the change.
Explored logging strategy for nowcast run time monitoring.
Introduced Nancy to py.test in the context of her nowcast.analyze.depth_average() function.
Salish Sea team meeting; see Google Drive Drawing.
ocean downtime caused nowcast 18 weather download to fail; subsequent issues with ocean mount on salish caused 00 and 06 downloads to also fail.
(MEOPAR)

Sent response to Nathan's inundation proposal & estimate request for a web app.

Prepared for and participated in post-workshop debrief.
(SWC)

Next review/feedback mtg tentatively set for Fri 9-Oct.
(sealinkd)


Wed 30-Sep-2015
^^^^^^^^^^^^^^^

Got nowcast system running again after yesterday's ocean mount issues on salish.
Researched machine readable logging & pandas for nowcast performance monitoring.
(MEOPAR)

Emailed Lazy Gourmet to request that they put their own phone number on their Facebook page instead of ours.

Noticed that Digital Ocean has added a cloud data centre in Toronto.

Worked on items that arose from 15Sep2015 mtg w/ UBC SCARP group:
* finished implementation of flow links on HSVI pages to guide users through basic flow
* added command to update deployment on webfaction to Makefile
* refactored routes map into 3 functions for readability
* refactored views into separate modules for info pages and HVSI pages
* refactored Analysis page to use sidebar layout similar to Maps page
* changed Anaysis page to use selector instead of links for comparison community choice
* improved handling of reference & comparison communities in select elements on Compare page
* created pre-compare page that is enabled when reference community is selected and allows user to choose comparison community
Changed generation of comparison community select options to use XHR so that selected reference community is always excluded from choices for comparison community.
(sealinkd)

Cleaned up Sublime Text settings files for Ubuntu systems in dotfiles repo; made them strictly machine specific.


Thu 1-Oct-2015
^^^^^^^^^^^^^^

Moved NEMO results other than nowcast from /data/ to /ocean/.
Confirmed that pandas.read_json() exists.
(MEOPAR)

Investigated UBC IT virtual server setup request form.
Added UBC and MEOPAR logos; way too much messing around with responsive CSS.
Added page footer; more CSS thrashing.
Sent email to UBC SCARP team re: completion of app skeleton.
Started playing with Postgres; created db and admin use for sealinkd on webfaction, and installed pgadmin on kudu.
Downloaded ubuntu/trusty64 box for vagrant and started experimenting with vagrant.
(sealinkd)


Fri 2-Oct-2015
^^^^^^^^^^^^^^

Picked up key for EOSM door from loading dock, and returned Rob's Waterhole office key.

Met w/ Klara to help her sort out Bitbucket auth issues.

Prepared to get automated ONC ADCP data downloads working again.
Put 15May_mod and new 2Sep scripts under version control on tom.
Manually merged Muriel's and Rich's changes, and my email address and ONC user id into 2-Sep getSogAdcpData.m script from Marlene@ONC.
Discussed w/ Rich next steps to get ADCP download automation working again; need to append latest deployment data to histories in GETDATA_fun.m and GETDEPL_fun.m, and use the former to download all of the raw data since the deployments.
Sent email to Miguel Castrillo at the Barcelona Supercomputing Centre re: getting their NEMO code improvements re: message packing.
Updated nowcast dev pkg list & docs.
Worked on nowcast run time monitoring via JSON logging; have to back-port 2 modules in the driftwood package from Python 3 to be able to use it.
Figured out how to read JSON log records into a pandas dataframe.
Changed nowcast mgr so that checklist is no longer logged each time that it is updated; also added a link to the checklist YAML dump to the monitoring page.
(MEOPAR)

Lemur shipped.


Sat 3-Oct-2015
^^^^^^^^^^^^^^

Added daily logging of nowcast mgr checklist just before it is cleared; log files are retained for 7 days.
Succeeded (with much hacking) in building XIOS and NEMO-3.6 on orcinus with new netCDF and HDF5 libraries that Roman built.
Created orcnius_build.sh scripts for NEMO-3.6 code and REBUILD_NEMO tool to deal with intel module shell level issue.
(MEOPAR)


Sun 4-Oct-2015
^^^^^^^^^^^^^^

Rando AGM; rode to/from w/ Susan B and Keith.


October
=======

Week 41
-------

Mon 5-Oct-2015
^^^^^^^^^^^^^^

Lemur is in customs hold.

Updated NEMO-3.6 migration docs with notes about building XIOS and NEMO-3.6 on orcinus.
Worked on hacking envvars to be able to run NEMO-3.6 on orcinus and update Roman on our status.
Continued email conversation w/ Miguel@Barcelona re: NEMO-3.6 message packing.
Implemented JSON logging in nowcast, but it failed when the 00 weather forecast started, so rolled it back.
Ported SalishSeaTools package (including nowcast) to Python 3 in tools repo nowcast-py3 branch.
(MEOPAR)

Attended Phys Ocgy seminar about Burns Bog carbon cycle measurements.


Tue 6-Oct-2015
^^^^^^^^^^^^^^

Attended AAPS orientation session.

Ported SalishSeaTools package test suite to Python 3 and wrote docs about the minimal changes that the porting effort required.
Fixed the bug that caused JSON nowcast logging to fail, and redeployed it.
Started downloading backlog of VENUS ADCP data since instrument maintenance at end of Aug.
Salish Sea team meeting; see Google Drive Drawing.
Confirmed that message packing improvements in NEMO-3.6 are present in our codebase.
(MEOPAR)

Missed UPS's 1st delivery attempt of Lemur.


Wed 7-Oct-2015
^^^^^^^^^^^^^^

Fixed bug in grib_to_netcdf worker that stopped automation between 06 weather download and forecast2 run.
(MEOPAR)

Sent email to it@ubc with questions about virtual server service request form.
Updated docs about initial temporary deployment on webfaction.
Started adding vagrant to dev environment to mirror UBC virtual server environment.
Got app running on vagrant VM proxied by nginx.
Started adding unit test suite.
(sealinkd)

UPS claimed a 2nd delivery attempt of Lemur that didn't happen; called and complained.

Thu 8-Oct-2015
^^^^^^^^^^^^^^

Continued downloading backlog of VENUS ADCP data since instrument maintenance at end of Aug; each 6 day download takes about 1 hr; finished east & central nodes.
Wrote email re: moving tools repo to Python 3.
(MEOPAR)

Did first iteration on data model for HVSI and user mgmt; see sealinkdERD.svg.
Figured out postgresql password auth and remote access.
(sealinkd)

Lemur delivered.
Started setting it up; see Google Drive doc.


Fri 9-Oct-2015
^^^^^^^^^^^^^^

Worked through ONC ADCP new deployment bootstrap snd tuning process with Rich.
Closed and merged nowcast-py3 branch in tools repo to move us to Python 3.
Helped Elise with mysteriously failing runs on salish; probaby a memory leak.
(MEOPAR)

Met w/ SCARP group; discussed app skeleton, hazard & action filtering, and data model.
(sealinkd)

Continued setting up Lemur, now named niko.


Sat 10-Oct-2015
^^^^^^^^^^^^^^^

Cycled to Parksville for Thanksgiving.

Built dotfiles/ubuntu/niko/ based on kudu/ and symlinked files into place.

Started development of 43ravens.ca web page.
(43ravens)


Sun 11-Oct-2015
^^^^^^^^^^^^^^^

Merged tools repo default branch into SalishSeaCmd-3.6 dev branch.
Changed conda environment description for SalishSeaNowcast package to use Python 3.
Changed salishsea combine sub-command to get number of MPI processors from run description file.
Changed salishsea combine sub-command to handle NEMO-3.6 single tile results files that end in _0000.nc by renaming them without _0000, multi-tile results files that don't cover the entire domain (e.g. CODAR region) by not processing them, and full domain sets of tiles by processing them with REBUILD_NEMO.
SalishSeaCmd-3.6 is ready for merge/release once I write some docs, but the beginnings of that work is on tom.
Tried to merge tools repo default branch into nowcast-obj dev branch, but they have diverged too much.
Ported nowcast-py3 changes into nowcast-obj branch.
Changed zmq send/receive methods to work with Unicode strings for Python 3.
Fixed unit tests that failed when test_nowcat_worker module was not tested in isolation.
(MEOPAR)


Week 42
-------

Mon 12-Oct-2015
^^^^^^^^^^^^^^^

**Statutory Holiday** - Thanksgiving

Fixed nowcast mgr bug whereby JSON log files are being rotated every day instead of every 30 days.
Consolidated JSON log files that have been generated to date.
Tagged SalishSeaTools-2.0 re: port to Python 3.
Dealt with nowcast failure in which west.cloud head node had lost some of its locale settings, causing salishsea gather to fail.
Explored using cdo to combine NEMO output files; not much success.
Discovered that results files from NEMO-3.6 run on salish with 3x5 MPI decomposition appear to be full width band across the domain (398 x ~60) rather than per-processor tiles as expected.
(MEOPAR)

Buffed 43ravens.ca web page and deployed it to webfaction.
(43ravens)


Tue 13-Oct-2015
^^^^^^^^^^^^^^^

Cleaned up tools docs so that they build cleanly in a Python 3 environment.
Added display of relative path to temporary run directory to salishsea run sub-command.
Changed salishsea gather & combine sub-commands to not compress results files, making them consistent with salishsea run.
Worked on refactoring and updating SalishSeaCmd package docs for v2.0.
Switched readthedocs virtualenv for tools docs to Python 3.
Salish Sea team meeting; see Google Drive Drawing.
(MEOPAR)


Wed 14-Oct-2015
^^^^^^^^^^^^^^^

Read 2015-2016 storm surge almanac published last night by Scott Tinis.
(MEOPAR)

Resubmitted questions re: UBC IT virtual server service via general IT support request form.
Refactored vagrant provisioning script to make step modular, and to run app under sealinkd user; hoping that the new scripts will be close to usable for provisioning UBC VM.
Improved Postgres provisioning automation & docs.
Added connection to Postgress for app data persistence, including private credentials dance.
(sealinkd)

Updated vagrant package to 1.7.4 by installing from deb downloaded from launchpad (wily werewolf).


Thu 15-Oct-2015
^^^^^^^^^^^^^^^

Emailed UBC HR re: access to M&P PD fund for PyCon.ca expenses.
Paid AGU membership for 2016.

Answered question from Nancy about .items() vs. .iteritems() for dicts and OrderedDicts in Python 2 and 3.
Pinged Roman re: libraries for NEMO-3.6 on orcinus.
Fixed Python 2 to 3 issues in nowcast.figures.plot_map() and stormtools.get_EC_observations(); first was zip() returning an iterator where a list was expected, 2nd was use of response.content (bytes) attr where response.text (str) should have been used.
Continued working on SalishSeaCmd v2.0 docs.
(MEOPAR)

Participated in kick-off mtg for next series of software-workouts.


Fri 16-Oct-2015
^^^^^^^^^^^^^^^

Sent email to Stephanie re: EduCloud setup.
Continued work on data model:
* Added create_tables script
* Read alembic docs and confirmed that it is aimed at schemas evolution, not creation, and that it does not include data migration
* Added Community object to data model with only a name attribute
* Added init_communities script to initialize community names into database
* Hooked HVSI views for Compare and PRofiles pages to database to provide community names for drop-down selectors
Updated my local sealinkd environment to be based on Python 3.5 so that it and the installed packages are the same as in the vagrant VM.
(sealinkd)

Re-built XIOS on orcinus with module libraries for netcdf and hdf5 that Roman set up yesterday.
Scheduled salishse command processor tutorial for Tue 20-Oct at 10:00.
Continued work on SalishSeaCmd package docs.
(MEOPAR)


Sat 17-Oct-2015
^^^^^^^^^^^^^^^

Added Mako text filters for title case, spaces-to-underscores, and underscores-to-spaces to templates.
(sealinkd)


Re-built NEMO-3.6 on orcinus with module libraries for netcdf and hdf5 that Roman set up on Thursday.
Committed and pushed cleaned up build files for XIOS and NEMO-3.6 on orcinus that use new netCDF and HDF5 modules.
Continued work on SalishSeaCmd package docs.
(MEOPAR)

Built new front wheel for Emma.


Sun 18-Oct-2015
^^^^^^^^^^^^^^^

Finished SalishSeaCmd package docs to the point where I am ready to merge the SalishSeaCmd-3.6 branch into default.
Set up nowcast-ish run on orcinus and mostly succeeded in using salishsea run to execute it:
* Had to hack run module to convert batch script to Unicode for writing
* nco is no longer installed, so deflation fails
Confirmed that output files are in full domain width strips.
Discovered that Python 3.5 is installed on orcinus.
(MEOPAR)

Added Community.count() class method.
Refactored Start page view to show all community names.
(sealinkd)


Week 43
-------

Mon 19-Oct-2015
^^^^^^^^^^^^^^^

Prepared for salishsea command processor tutorial tomorrow.
Made some minor backward changes in the SalishSeaCmd package so that it will run under Python 2.7 on orcinus and jasper, thereby avoiding the messiness that happens on those platforms when we try to use Mercurial rebase an Python 3.
Confirmed to Roman that new netCDF4 and HDF5 modules on orcinus work for us.
Requested that Roman build us a new NCO module to replace the one that got deleted when the new netCDF4 and HDF5 modules came into effect; later discovered that NCO library is still there, just not included in a module anymore.
Cleaned up NEMO-3.6 reference namelist section files, and added a reference iodef.xml file with proper file group closing tags.
Re-build XIOS and NEMO-3.6 on orcinus with the _mpi version of the netCDF & HDF5 modules/libraries; test run with just XIOS rebuilt took 28 minutes; _mpi != parallel output.
Investigated Nancy's discovery that python-netCDF4 Dataset.close() method crashes jupyter notebook under Python 3 but not under Python 2.7.
(MEOPAR)

Attended Phys Ocgy seminar about canyon upwelling by Karina.

Liberals won a 184 seat majority in parliament, ending the Harper era.


Tue 20-Oct-2015
^^^^^^^^^^^^^^^

Ran tutorial about SalishSeaCmd package.
Merged SalishSeaCmd-3.6 branch into tools default branch, and tagged repo with SalishSeaCmd-2.0.
Roman built nco-4.5.2 module for us on orcinus.
Salish Sea team meeting; see Google Drive Drawing.
Helped Jie figure out why salishsea run was failing on salish; her SalishSeaCmd package was installed in anaconda3/ not $HOME/.local/.
(MEOPAR)

Set up smelt as build slave to take over R3_baseline_regression from snapper; created ticket #15022 to get port 9989 opened between bjossa and smelt.
(SOG)

Katie shadowed me for the afternoon.

Got wired connection for niko.


Wed 21-Oct-2015
^^^^^^^^^^^^^^^

Submitted request for EduCloud service;
Sent email to help.desk@it.ubc for help with the EAD admin account authorization.
Updated the 2 North Vancouvers to City & District per email from Jackie.
Continued work on data model:
* Added Capital object to data model to persist HVSI capital names
* Added init_capitals script to initialize HVSI capital names into database
* Populated comparison community drop-down on Analysis page with community names from database and random HVSI values
* Tried unsuccessfully to format comparison community drop-down option text strings so that HVSI values are right justified
* Add Asset object to data model to persist data about digital assets managed by the UBC SCARP team
* Changed vagrant setup to sync SealinkD-assets/ to VM
* Changed nginx config to serve assets from Sealinkd-assets/
* Changed app setup to get static & asset server URLs from config file
* Moved Research page images out of app repo and into SealinkD-assets/ and used Asset object to hook them into the app
Added issues for data model components.
(sealinkd)

Marlene@ONC says that Muriel's ADCP cron job is still firing; bumped ticket #14984 for Charles to kill it.
(MEOPAR)


Thu 22-Oct-2015
^^^^^^^^^^^^^^^

Booked travel for trip to PyCon.ca and Barrie.

Continued struggle with CWL EAD admin account.
Continued work on data model:
* Changed init_assets script to load_assets and make it update as well as add new
* Added aerial photos from CJ to assets and randomly choose one for each load of landing page
* Changed footer to be sticky at bottom of viewport
* Added UserRole and HVSI Dimension object to data model
* Started adding HVSI Indicator object to data model
(sealinkd)

Restarted buildbot slaves on coho, herring & snapper.
Restarted buildbot master on bjossa to allow smelt to join the party.
Started buildbot slave on smelt, and forced an R3_baseline_regression run to test it.
(SOG)

Muriel's ADCP cron job is still firing and annoying ONC.
(MEOPAR)


Fri 23-Oct-2015
^^^^^^^^^^^^^^^

Installed vagrant, virtualbox, and ubuntu/trusty64 imaage on niko; image download took ~2min on EOAS wire in contrast to ~2hr at home :-)

Reviewed and edited RAC application.
Sent email Muriel re: killing her ADCP cron job.
Added XIOS attached/detached support to `salishsea run` and `salishsea prepare`.
(MEOPAR)

Sent email to Jackie re: getting indicators and community data spreadsheets.
(sealinkd)


Sat 24-Oct-2015
^^^^^^^^^^^^^^^

Fixed typo in file_definition closing tag in SS-run-sets/SalishSea/nemo-3.6/ iodef.xml files.
Fixed missing intel module load on orcinus and re-submitted separate-XIOS test run.
Started to play with creation of a thalweg salinity contours video that can be updated daily.
(MEOPAR)

Worked on trying to get offsite backups to sable working again.
Decided to delete the badly named and bloated /mnt/data1/picassoBackup/ on sable and start a new matisseBackup/.
Stopped and unloaded backup and rsync daemons on matisse.
Started manually rsync-ing contents of matisse /Volumes/Backup/ to sable matisseBackup/: ESB_2/, kudu/

Crazy-glued 3 Fitbit bracelets and one of Susan's winter cycling boots.

Got vagrant dev env running on niko for Monday's meeting.
(sealinkd)


Sun 25-Oct-2015
^^^^^^^^^^^^^^^

Continued playing toward thalweg salinity video.
Muriel replied that she had deleted her cron jobs.
(MEOPAR)


Week 44
-------

Mon 26-Oct-2015
^^^^^^^^^^^^^^^

Prepared for and participated in mtg w/ UBC SCARP group; demo-ed app from vagrant VM on niko.
* new app name: Resilient-C
* new layout and content ideas for community profiles page
(sealinkd)

Sent email to ONC  to get confirmation that Muriel's ADCP cron job search failures have stopped; apparently not...
Updated ADCP data downloads, and started writing docs re: the process of restarting the ADCP automation after new sensor deployments.
(MEOPAR)

Attended Phys Ocgy seminary by Drew Snauffer about machine learning prediction of snow-water equivalent values for BC.

Reviewed and commented on Susan's NSERC Discovery grant proposal.


Tue 27-Oct-2015
^^^^^^^^^^^^^^^

Copied kudu backup repo from home Backup drive to data1 mount on sable via EOAS wired network.

Finished ADCP raw data downloads to catch up to calendar, and created a cron job to do the downloads daily until the full automation can be restarted.
Changed symlinks to an ocean clone of private-tools so that the code is easier for Rich to access, and there is a separation between the code used for dev and that used for the automation.
Struggled to get compare_daily.m automation restarted; finally reproduced what Rich & did on 9-Oct for east node.
Salish Sea team meeting; see Google Drive Drawing.
(MEOPAR)

Solicited people to answer the questions posed for this week's workout.
(SWC)


Wed 28-Oct-2015
^^^^^^^^^^^^^^^

Switched on compare_daily.m automation for east node ADCP data; continued trying to get central & ddl nodes rebooted.
Investigated why analysis repo is so large; no conclusion.
(MEOPAR)

Moved emily and matisse backups to _snapshot_* directories.
Re-enabled matisse backup to start a new rdiff_backup repo.

Emailed Maria@it.ubc re: EduCloud setup; VM was ready around midday, but my only access is via a web console.
Wrote a ticket requesting ssh port be opened, but got no response.
Refactored Indicator data model to handle HVSI indicators metadata and loaded those into the dev database.
Implemented IndicatorValue data model and started loading those data into the database.
Michelle committed the About page content.
(sealinkd)


Thu 29-Oct-2015
^^^^^^^^^^^^^^^

Finished loading indicator values to dev database.
Installed nginx on prod VM so that there is something listening on port 80.
Fiddled with hosts.allow and hosts.deny but VM remains inaccessible from anywhere other than VMware web console.
Sent another service request to UBC IT and again got no ticket notification in response.
(sealinkd)

Explored NumPy masked array creation techniques re: Karina's question; broadcasting does not appear to be an option.
Participated in workout Q&A session.
(SWC)

Started investigating NEMO TOP BDY branch that Elise wants to use.
Continued working on ONC ADCP automation.
Charles made skookum available to us.
(MEOPAR)


Fri 30-Oct-2015
^^^^^^^^^^^^^^^

Email to Charles to hold off on opendap config on skookum pending eval of erddap vs. opendap/hyrax.
Wrote blurbs to MEOPAR report re: storm surge portal and OceanViewer objectives to year 4.
Talked to Rich about progress on ADCP automation.
Finally got central node automation restarted.
(MEOPAR)

Emailed Tereza with suggestions about using lvdiff for hg diff on Labview VIs.
(SWC)

Reviewed and commented on Susan's letter for Nancy.

Figured out that I needed to open port 80 on the VM for HTTP access from Internet.
UBC IT finally added firewall rule to allow ssh access from smelt; requested another rule for salish for redundancy and got it quickly.
Started deployment.
(sealinkd)


Sat 31-Oct-2014
^^^^^^^^^^^^^^^

More farting around with port forwarding for access to production VM; finally got it working.
Finished initial deployment, though there are a few loose ends to clean up, and docs to write.
(sealinkd)

Restarted automation for ddl ADCP node; the key to bootstrapping the automation for a new deployment is to run GETDEPL_fun.m to create a DEPL* file in a day directory, then copy that DEPL* file as the current DEPL* file before running compare_daily.m.
(MEOPAR)


Sun 1-Nov-2014
^^^^^^^^^^^^^^

Re-initialized Darktable database because I don't like how it manages copying images from SD to disk.
Finally transferred Norway, Skookumchuk & Alaska images from SD to dated dirs on kudu for import to Darktable.


November
========

Week 45
-------

Mon 2-Nov-2015
^^^^^^^^^^^^^^

Did email intro between Neil Swart and Roland Schigas.

Told Marlene@ONC that there is nothing more we can do about the bogus search requests from Muriel's account unless she can tell us what IP address they originate from; proposed deletion of Muriel's dmas account.
Started working on skookum
* worked through a bunch of setup issues w/ Charles via tickets
* created /results/MEOPAR/nowcast-prod and cloned tools repo
* created nowcast-prod conda env
Got NEMO-3.6 w/ separate XIOS running on orcinus; tested 3x5+1, 4x9+1, 8x18+1, 6x14+1.
Looked deeper at NEMO-3.6 TOP BDY branch and discussed it with Susan and Elise.
(MEOPAR)

Attended Phys Ocgy seminary by Stephanie Waterman about turbulence in the Antarctic Counter Current ?? (ACC)


Tue 3-Nov-2015
^^^^^^^^^^^^^^

* do AGU abstract claim
* finish ONC ADCP deployment bootstrapping docs
* explore skookum
* characterize data available from DFO water level web service

Pulled Nancy's western boundary condition salinity changes on to salish & west.cloud for nowcast; then recovered form nowcast system crash caused by not creating a symlink for the new BCs file.
Worked w/ Susan & Charles to get halibut shutdown before 10:00 to establish whether or not it is really the source of the daily bad requests from Muriel's account that are hitting ONC.
Added ubuntu@compute deployment key to NEMO-forcing repo on bitbucket.
Salish Sea team meeting; see Google Drive Drawing.
After multiple tries, got a 1d, 8x18+1 nowcast run on orcinus to complete in 21m14s of walltime.
Started creating a notebook that explores the DFO water levels web service uisng the suds-jurko library to deal with the service's SOAP interface.
(MEOPAR)

Attended dept. colloquium by Paul Hoffman about snowball earth


Wed 4-Nov-2015
^^^^^^^^^^^^^^

Phone call from Jerry re: problems w/ Minerva; replied w/ offer of site visit tomorrow, pricing for on-site and remote pre-incident responses, and an offer of a proposal for a monitoring and response service.
(Nordion)

Site app was detached from stie on webfaction, so restored it.
(43ravens.ca)

Queued nowcast 3d 8x18+1 run w/ 5e6 XIOS buffer (reduced from 5e7) on orcinus to compare to Susan's jasper experience with end of run XIOS lag; initially a 5m test to check XIOS config, then 1h30m walltime.
Explored min XIOS buffer size vs. MPI decomposition.
(MEOPAR)

Sent email to Maria re: DNS & TLS certs but she is away on sick leave; opened a new systems service request per instructions in her auto-reply.
Created invoice for stage 1 and wrote progress report to Stephanie.
Rebranded app from Sea-link'D to Resilient-C.
Cleaned up About page content.
Worked on production deployment management automation.
(sealind)


Thu 5-Nov-2015
^^^^^^^^^^^^^^

Emailed status report & invoice to Stephanie & Jackie.
(sealinkd)

Queued nowcast 1d 12x27+1 run on orcinus w/ 2.5e6 XIOS buffer size.
Talked with Nancy about masked arrays, broadcasting, and DFO water level web service.
Continued working on notebook re: DFO water level web service.
(MEOPAR)

Got flu shot at ESB clinic.

Site visit investigate Minerva issues.
/var filesystem was corrupted; had to re-install mako & formencode pkgs to get Minerva app to start.
Minerva app is slow, won't render PDFs.
Beaver app not running.
Noticed mfi0 errors in log and on console screen; RAID issues.
Agreed to provide proposal for a return visit to dig deeper and identify longer term solutions.
(Nordion)


Fri 6-Nov-2015
^^^^^^^^^^^^^^

Travel to Toronto for PyCon.ca 2015

Analyzed results of 3d 8x18+1 and 1d 12x27+1 nowcast runs on orcinus.
(MEOPAR)

Fix permissions on site CSS and JS file in production deployment so that they serve properly as static data.
(sealinkd)

Attended PyCon.ca social at The Prenup Pub.


Sat 7-Nov-2015
^^^^^^^^^^^^^^

PyCon.ca day 1
* Opening keynote by Brett Canon; benchmarking implementations, CPython 3.5 w/ PGO optimization trained against test suite is slightly faster than 2.7
* Good web app security talk by Frederic Harper; OWASP top 10, outofcomfortzone.com
* Good Django GeoJSON talk by Tyler Savory; PyProj4, Kmeans, gdal (.shp -> GeoJSON), slippy tiles, AnyCluster
* Good Jupyter cell magics extensions talk by Nicolas Kruchten; _repr_html_, DIY cell magics
* Met Pierre-Yves David, Mercurial core dev employed by Facebook to work on community (i.e. not Facebook-specific) development


Sun 8-Nov-2015
^^^^^^^^^^^^^^

Created Freshbooks account.
(43ravens)

PyCon.ca day 2
* Data mining Python code & metadata keynote by Cameron Davidson-Pilon
* "tutorial" about exponentiation and numbers in Python by En_zyme; math.expm1, math.hypot
* Legacy codebase talk by Scott Triglia; functional/acceptance tests facilitate legacy refactoring better than unit tests
* Good Python in Mercurial talk by Pierre-Yves David; storage model combines diffs & full copies to optimize length of diff chain, extensions are easy & faster than revsets (which are awesome)
* Fabric -> Ansible talk by Dorian Pula


Week 46
-------

Mon 9-Nov-2015
^^^^^^^^^^^^^^

PyCon.ca sprints

The nosy codebase is more mature than I recalled, including a bunch of unit tests.
Researched nosier; it works on Linux only because it uses inotify instead of polling.
Stefan Wiechula joined my sprint and did most of the heavy lifting to test and finalize the Python 3 port.
After initially deciding to drop Python 2.5 support due to the lack of the "as" keyword, a discussion with Brandon Rhodes lead to parsing exception messages out of sys.exc_info() so that Python 2.5 support can be retained.
Tried unsuccessfully to get tox and conda to work together, but Stefan drew my attention to pyenv that enabled him to tox the nosy tests under 2.6, 2.7, and 3.5.
(nosy)

Scheduled 26-Nov w/ Youyu and Susan when Youyu will be in BC.
(43ravens)


Tue 10-Nov-2015
^^^^^^^^^^^^^^^

Travel from Toronto to Barrie.

Reviewed Nancy's recent nowcast improvements and wrote explanatory email about transition from salish/Py2.7 to skookum/Py3.5.
Pulled SS-run-sets changes on to west.cloud to include output from tide gauge stations that Nancy added
Answered questions on Google whiteboard for team mtg.
(MEOPAR)


Wed 11-Nov-2015
^^^^^^^^^^^^^^^

(MEOPAR)


Fri 13-Nov-2015
^^^^^^^^^^^^^^^

Set up PayPal business account and used it to invoice Nordion for 5-Nov site visit.
(43ravens)

Worked on deployment of nowcast system on skookum and wrote docs re: skookum /results/ storage organization.
(MEOPAR)


Sat 14-Nov-2015
^^^^^^^^^^^^^^^

Continued working on nowcast deployment on skookum; got broker & object implementation of mgr operational under Python 3.5; started working through _launch_worker() issues from download_weather worker onward; object impl of get_NeahBay_ssh worker appears to work.
Realized that nowcast-obj branch is badly out of sync with default.
(MEOPAR)


Sun 15-Nov-2015
^^^^^^^^^^^^^^^

Travel home from Barrie.

Continued working on nowcast deployment on skookum.
Started new SalishSeaNowcast branch to keep dev in sync w/ default and move nowcast to its own package.
(MEOPAR)


Week 47
-------

Mon 16-Nov-2015
^^^^^^^^^^^^^^^

Continued work on SalishSeaNowcast package:
* cleaned up test suite
* ported in object-based nowcast_mgr and grib_to_netcdf worker
* changed JSON logging to use driftwood package
(MEOPAR)

Attended Phys Ocgy seminar by Sophie Clayton about modeling phytoplankton diversity in a global MITgcm configuration.


Tue 17-Nov-2015
^^^^^^^^^^^^^^^

Updated niko to Ubuntu 15.10 "Wily Werewolf".

Completed M&P ProDev fund claim re: Pycon.ca.
Completed EOAS claim re: Ocean Sciences abstract.

Finally got active response re: DNS and SSL certs from Brian Wu.
(sealinkd)

Continued work on SalishSeaNowcast package:
* added checklist logging setup to manager
* added after_grib_to_netcdf method to mgr
* ported in NowcastWorker-based get_NeahBay_ssh worker
* updated and deployed weather download cron scripts on skookum
Salish Sea team meeting; see Google Drive Drawing.
Fixed bug that Nancy reported whereby salishsea run was producing "nodes=7.0:ppn=12" on jasper; it was a 2vs3 issue involving integer division and the type returned by math.ceil().
(MEOPAR)


Wed 18-Nov-2015
^^^^^^^^^^^^^^^

Downloaded, printed, read, and annotated Chang, et al (2015), Using vulnerability indicators to develop resilience networks: a similarity approach - the HVSI paper.
Started development of sealinkd.hvsi module of functions to do HVSI calculations in a way that is independent of the app.
(sealinkd)

Confirmed that the part of nowcat that is running on skookum is doing so smoothly.
Opened ticket to request skookum /results file system be exported to salish, sable, tyee, char, cod & snapper.
Helped Susan recover from accidentally merging SalishSeaNowcast branch into default.
(MEOPAR)

Full SOG build on herring was failing because gfortran wasn't installed; opened a ticket to remedy that, then forced build, which completed with dirty diffs.
(SOG)

Ken reported more isoinfo server trouble; requested Del service tag so that I can spec disks.
(Nordion)


Thu 19-Nov-2015
^^^^^^^^^^^^^^^

Continued work on SalishSeaNowcast package:
* ported in NowcastWorker-based make_runoff_file & download_results workers
* added after_make_runoff_file & after_download_results methods to mgr
* started porting in NowcastWorker-based upload_forcing worker
Opened ticket to have netcdf-bin package installed on skookum; done.
Charles set up /results exports & mounts.
Helped Nancy with fallout of yesterday tools branch merge issue.
Moved /ocean/sallen/allen/research/MEOPAR/GRIB/ to /results/forcing/atmospheric/GEM2.5/GRIB/.
(MEOPAR)

Finished initial implementation of sealinkd.hvsi module of functions to do HVSI calculations; no dependencies!
Updated database and app on production server; database updates were due to change in schema of IndicatorValues, and lower-casing of indicator type values.
(sealinkd)


Fri 20-Nov-2015
^^^^^^^^^^^^^^^

Continued work on SalishSeaNowcast package:
* fixed bugs in download_results worker
Moved /ocean/sallen/allen/research/MEOPAR/SalishSea/forecast2 to /results/SalishSea/forecast2.
Moved /ocean/sallen/allen/research/MEOPAR/SalishSea/forecast to /results/SalishSea/forecast.
Change nowcast config on salish to use /results file system:
* bathymetry, rivers, forecast & forecast2 results
Got ports 5555 and 5556 on skookum opened for traffic from salish and west.cloud.
Disabled make_runoff_file worker in salish nowcast system in favour of the one in on skookum.
Youyu launched conversation between Susan and Danny re: repos, docs, etc. (aka NEMO Sandbox).
(MEOPAR)

Attended special Phys Ocgy seminar by Kjetil Vage of Bergen about change in Nordic seas deep water formation.


Sat 21-Nov-2015
^^^^^^^^^^^^^^^

Confirmed that yesterday's path changes for the nowcast system were effective.
Restarted nowcast mgr to shift make_run_off worker to skookum deployment.
Discussed with Susan the make_run_off worker changes to add Jie's Fraser River bathymetry to produce new run-off file for nowcast-2.0.
Moved /data/dlatorne/MEOPAR/SalishSea/nowcast to /results/SalishSea/nowcast.

Continued work on SalishSeaNowcast package:
* continued porting in NowcastWorker-based upload_forcing worker
(MEOPAR)

Sent email to Stephanie for decision on 1yr or 3yr TLS certs.
(sealinkd)


Sun 22-Nov-2015
^^^^^^^^^^^^^^^

Continued work on SalishSeaNowcast package:
* finally finished porting in NowcastWorker-based upload_forcing worker
* started porting NowcastWorker-based make_forcing_links worker and adding _after_make_forcing_links method to mgr
(MEOPAR)


Week 48
-------

Mon 23-Nov-2015
^^^^^^^^^^^^^^^

Pulled and updated NEMO-forcing repo on west.cloud.
Nowcast failed due to missing Content-Length header on some GRIB files; temporarily removed our code that uses that header to get the system restarted; later testing on skookum showed that the header was back.
Continued work on SalishSeaNowcast package:
* worked on porting make_plots worker to NowcastWorker basis
(MEOPAR)

Generated CSRs for 3 resilient-c app domains and sent them to Karen @ UBC IT.
(sealinkd)

Attended Phys Ocgy seminar.


Tue 24-Nov-2015
^^^^^^^^^^^^^^^

Continued work on SalishSeaNowcast package:
* continued porting NowcastWorker-based make_plots worker and adding _after_make_plots method to mgr; works except ferries comparison plots
* refactored nowcast_mgr
* added run_NEMO worker launching to _after_make_forcing_links method
Telcon w/ Dany Dumont re: Canada-wide NEMO collaboration
Salish Sea team meeting; see Google Drive Drawing.
(MEOPAR)


Wed 25-Nov-2015
^^^^^^^^^^^^^^^

Continued work on SalishSeaNowcast package:
* finished NowcastManager implementation sufficient to run the system (I think) but couldn't test it on skookum because weather download didn't finish until 14:35
* added nowcast_mgr module to API docs
(MEOPAR)

Attended special seminar by Katie Kuksenok about her observational research of oceanography groups' software practices.

Received certs for resilient-c app domains from Karen @ UBC IT.
(sealinkd)


Thu 26-Nov-2015
^^^^^^^^^^^^^^^

Generated certificate chains for resilient-c app domains by following instructions at https://confluence.id.ubc.ca:8443/x/0pxvB.
Started work on a Jupyter Notebook to demo hvsi calcs module.
(sealinkd)

Prep for and attended workout session on R lead by Laura:
* installed r-base 3.2.2-1 package on niko via software centre
* installed RStudio 0.99.489 package on niko via download from RStduio site
(swc)

Met w/ Youyu & JP re: NEMO models.
(MEOPAR)


Fri 27-Nov-2015
^^^^^^^^^^^^^^^

push_to_web worker failed for forecast2 on salish due to DNS failure for shelob; re-ran manually.
Stopped nowcast mgr on salish, copied nowcast.yaml config from skookum test dir, and started mgr on skookum.
Fixed logic bugs in _after_download_weather and _after_get_NeahBay_ssh.
Updated west.cloud to SalishSeaNowcast branch.
Installed Python 3 packages that nowcast needs on west.cloud: python3-pip, python3-dev, python3-matplotlib, python3-pandas, python3-cliff, python3-zmq.
Installed SalishSeaTools, SalishSeaCmd, and SalishSeaNowcast for Python 3 on west.cloud using --user.
Added nemo34=True flag to salishsea_cmd.api.prepare() call in runNEMO worker.
Removed --no-compress from salishsea gather options in run_NEMO worker.
Changed checklist run date key used by run_NEMO and watch_NEMO workers from "run_date" to "run date".
Changed _launch_worker method to get remote host Python interpreter and config file from nowcast system config.
Changed run_NEMO worker to use config on remote host to find Python interpreter and config file to run watch_NEMO worker with.

Hacked salishsea_cmd.api on west.cloud to include MPI decomposition key in run description
(MEOPAR)


Sat 28-Nov-2015
^^^^^^^^^^^^^^^

skookum nowcast system ran forecast2 without manual intervention, but make_plots worker failed with a KeyError.
Fixed bug in make_plots worker and re-ran it for forecast/28nov15, forecast2/27nov15, and forecast/27nov15.
Merged tools default branch into SalishSeaNowcast branch.
(MEOPAR)

Finished Python lists section of Jupyter Notebook to demo hvsi calcs module, and added it to docs with an nbviewer link.
Added notebook section re: using data from spreadsheet to calculate HVSI values.
(sealinkd)


Sun 29-Nov-2015
^^^^^^^^^^^^^^^

Got sealinkd VM up and running on niko after thrash due to mistyped postgres app password.
Got access to the app database in the dev VM working in a Jupyter notebook.
Added Indicator.types_for_capital() class method that returns indicator types iterable for use in hvsi.hvsi().
Added IndicatorValue.for_community_capital() class method that returns indicator values iterable for use in hvsi.hvsi().
Added IndicatorValue.ranges_for_capital() class method that is a indicator value ranges generator for use in hvsi.hvsi().
Added section to hvsi calcs notebook about using app database data in hvsi.hvsi().
(sealinkd)

Discovered that nowcast mgr had crashed on Sat evening so none of forecast2/28nov15, nowcast/29nov15, or forecast/29nov15 ran; re-started mgr and got nowcast/29nov15 running.
(MEOPAR)


December
========

Week 49
-------

Mon 30-Nov-2015
^^^^^^^^^^^^^^^

Continued cleaning up from yesterday's nowcast mgr downtime mess.
Met w/ Elise and Muriel re: tasks for Muriel.
Stripped 349dd1cc8d64 based branch (Susan's mistake) from tools repo, but I suspect that it is only a local effect, and that those commits will come back when next I pull.
Enabled commit notification emails for tools repo so that I can review Muriel's commits.
Decided on salishsea.eos.ubc.ca/erddap/ as mount point for ERDDAP app; emailed Charles to meet re: install & config.
Met w/ Muriel re: onboarding.
Discussed remaining salishsea_tools/nowcast/ file moves w/ Susan and Nancy.
Moved notebooks to nowcast/notebooks/ and buffed make_readme.py there.
Moved tidal_predictions/ to nowcast/ and fixed paths for it there, including adding it to nowcast.yaml for get_NEahBay_ssh worker.
(MEOPAR)

Cleaned up, committed and pushed the weekend's work.
(sealinkd)

Attended Phsy Ocgy seminary by Nancy on mixing in ocean models & Salish Sea NEMO in particular.


Tue 1-Dec-2015
^^^^^^^^^^^^^^

Moved the rest of the spin-up run results from /ocean/dlatorne/MEOPAR/SalishSea/results/spin-up/ to /results/SalishSea/spin-up/.
Hacked around a path bug in the make_plots worker that I introduced yesterday when I moved the tidal_predictions/ files.
Moved the NeahBay ssh forcing history from /ocean/nsoontie/MEOPAR/sshNeahBay/ to /results/forcing/sshNeahBay/.
Moved /ocean/sallen/allen/research/MEOPAR/Operational/ to /results/forcing/atmospheric/GEM2.5/operational/.
Deleted SalishSeaTools/salishsea_tools/nowcast/ in SalishSeaNowcat branch.
Investigated Atom vs. RSS feed format for Port Metro Vancouver; still no clear winner, so ask what they prefer.
ONC-ADCP data download for east node failed.
Met w/ Charles re: ERDDAP on skookum.
Merged, closed, tagged & pushed SalishSeaNowcast branch.
Salish Sea team group meeting; see Google Drive whiteboard.
(MEOPAR)

Figured out how to determine what repo revision was used to build SOG buildbot ref files byt digging in build history & ref files dirs; see whiteboard.
(SOG)

Updated SCARP team on progress and plans, in response to Jackie's update yesterday re: profiles page layout.
Copied ssl certs to my sysadmin space on the app vm.
Installed resilient-c.ubc.ca cert & key but can't connect from Internet, only locally; sent email to Karen re: possible firewall rule tweak, and she passed the ticket to NMC where Nathan did the necessary firewall change.
(sealinkd)


Wed 2-Dec-2015
^^^^^^^^^^^^^^

Site visit re: isoinfo server failure; see notes in 2dec15-isoinfo-maint.rst file in client file.
(Nordion)

Investigated and resolved issue of why download_weather workers are not logging into ~/public_html/MEOPAR/nowcast/; path issues in cron scripts.
Pulled merged code into skookum nowcast-sys deployment and flipped branch there to default.
(MEOPAR)


Thu 3-Dec-2015
^^^^^^^^^^^^^^

Invoiced Nordion for 1/3 of present project.
(Nordion)

Noticed dramatic speed-up in nowcast weather downloads and sent thankyou email to Pat@EC; she was surprised by the speed-up.
Worked on figures.get_tides() path issue and SalishSeaCmd API changes that nowcast needs.
Discussed use of SalishSeaNowcast package w/ Nancy.
Helped Nancy get NEMO-3.6 running or orcinus, and Elise get set up on orcinus.
Discussed SalishSeaCmd features required for green model w/ Elise.
(MEOPAR)


Fri 4-Dec-2015
^^^^^^^^^^^^^^

Reviewed project progress & status, and updated issue tracker.
Tagged 1.0.dev0 re: start of implementation of HVSI into app page skeletons.
Changed community selector on Analysis page to use HVSI values calculated from the database.
Updated conda and sealinkd envs on kudu, dev VM, and sealinkd-vm, and installed matplotlib in all 3 envs.
Started work on bar charts for analysis page, and got an initial implementation of the main panel chart that looks and works okay.
(sealinkd)


Sat 5-Dec-2015
^^^^^^^^^^^^^^

Cleaned up, committed, and pushed to production yesterday's Analysis page HVSI bar chart work.
Fixed site.css permissions on production server; changes due to hg update?
(sealinkd)

Started adding nowcast-green to nowcast system by adding nowcast-green run type to make_forcing_links worker and launching make_forcing_links nowcast-green from after_grib_to_netcdf message handler.
Bumped SalishSeaCmd version to 2.1.dev0.
Added nemo34 arg to SalishSeaCmd API run_description() and run_in_subprocess() functions.
Changed salishsea prepare to be able to create multiple namelist files for NEMO-3.6 from section file lists in YAML run description file; lists are keyed by the namelist file name they are concatenated into.
(MEOPAR)


Sun 6-Dec-2015
^^^^^^^^^^^^^^

Set up vagrant VM for tox testing; got test suite passing under 3.5, 3.4, 3.3, 3.2, 2.7, 2.6, and 2.5.
Released nosy v1.2 on PyPI.
(nosy)

Discussed Salish Sea NEMO 2.0 docs organization w/ Susan.
Manually ran make_forcing_links nowcast-green because I messed up pulling it into the automation.
Re-organized Python packaging docs to make room for library code section and started writing it.
Re-named and re-labeled SalishSeaTools package docs section.
(MEOPAR)


Week 50
-------

Mon 7-Dec-2015
^^^^^^^^^^^^^^

Discussed nowcast system and research_ferries module w/ Muriel.
Attended Phys Ocgy seminar by Idalia about her submarine canyons research.
Fixed path errors in nowcast.yaml so that nowcast-green could finally start.
Discussed new SalishSeaTools sea surface height anomaly module w/ Nancy.
Added initial version of nowcast system production deployment docs to SalishSeaNowcast package docs.
Fixed bug in _after_grib_to_netcdf() that it to try to launch upload_forcing worker for nowcast-green; deployed bug fix.
Add notes on installation of SalishSeaNowcast package as a library to docs, and moved worker failure mitigation docs into a separate section.
Fixed docs config so that API sections build again on readthedocs.
(MEOPAR)


Tue 8-Dec-2015
^^^^^^^^^^^^^^

Changed relative imports to absolute in SalishSeaNowcast and SalishSeaCmd packages.
Added teos_tools module to SalishSeaTools package w/ unit tests & API docs.
Wrote draft email to Cindy Jeromin @PMV re: storm surge forecast feed.
Discussed research_ferries progress w/ Muriel.
Discussed nowcast-green & database for nutrient data w/ Elise.
Started working on forcing links changes for NEMO-3.6 in SalishSeaCmd package.
Salish Sea team mtg; see Google Drive whiteboard.
(MEOPAR)


Wed 9-Dec-2015
^^^^^^^^^^^^^^

Finished implementation of flexible naming for forcing links for NEMO-3.6 in SalishSeaCmd package.
Reviewed Nancy's changes to the get_NeahBay_ssh worker.
Started work on fixing make_plots worker and figures.get_tides() issue re: tidal predictions path.
Tested and debugged flexible naming for forcing links for NEMO-3.6 in SalishSeaCmd package in nowcast-green context.
(MEOPAR)

Fixed project name in package metadata file - it must be the package name (SealinkD) in order for the package to install properly.
Moved auth ticket signing secret to private credentials file.
Fix default umask on EduCloud VM and documented that in the deployment notes.
Fixed the Analysis page main panel chart spill-over issue that Jackie reported; incorrectly spelled class in the img tag.
Added HVSI bar charts to capital sidebars on the Analysis page.
(sealinkd)


Thu 10-Dec-2015
^^^^^^^^^^^^^^^

Discussed w/ Susan provision of data to Yongsheng@DFO for FVCOM model of harbour & Fraser.
Pushed flexible naming for forcing links for NEMO-3.6 in SalishSeaCmd package in nowcast-green context.
Investigated missing nowcast/early-days/ 1d_grid_T file that Nancy spotted; no explanation, lost from /data/dlatorne/MEOPAR/SalishSea/nowcast/early-days/.
Pulled Nancy's get_NeahBay_ssh worker and nowcast.residuals changes into production nowcast.
Finished fixing make_plots worker and figures.get_tides() issue re: tidal predictions path; pulled into production.
Wrote draft email to Cindy Jeromin @PMV re: storm surge forecast feed, and got an enthusiastic reponse.
Worked on results server docs, especially model changes for nowcast runs.
Helped Nancy w/ NEMO-3.4 on orcinus libnetcdff.so not found issue.
(MEOPAR)

Start work on HVSI bar charts for Compare page.
Re-organized panels on Compare page to accommodate addition of Institutional capital.
(sealinkd)


Fri 11-Dec-2015
^^^^^^^^^^^^^^^

Added dimension HVSI bar charts for each capital to the Compare page, however, there is an unresolved ZeroDivisionError issue in many renderings, and the charts that do render show almost uniform 1.0 values - suspicious.
(sealinkd)

Dealt with overnight download failures from EC web services.
Manually ran ECget river flow cron jobs, make_runoff_file worker, download_weather workers for 00, 06, and 12 forecasts, upload_forcing worker against west.cloud to get nowcast run started, and make_forcing_links worker against salish to prepare for nowcast-green run.
Thought about ATOM feed for storm surge notifications and realized how it can probably be implemented as a nowcast worker.
make_plots nowcast research worker failed due to ConnectionError getting VENUS data; research_VENUS.load_VENUS() does not use nowcast.lib.get_web_data() techniques (but it rarely fails); created tools repo issue #25.
Cleaned up and committed my notebook re: DFO water levels web service.
Fixed run_NEMO worker re MPI decomposition addition to salishsea_cmd.api.run_description().
Worked on nemo34 bug in salishsea run re: orcinus modules; waiting for confirmation from Nancy.
Stopped nowcast test suite from writing nowcast_checklist.log file, and fixed test_analyze.py so that it had a non-uniform depths array in code instead of reading it from a run results file.
(MEOPAR)


Sat 12-Dec-2015
^^^^^^^^^^^^^^^

Started work on nowcast ATOM feeds.
(MEOPAR)


Sun 13-Dec-2015
^^^^^^^^^^^^^^^

Continued work on nowcast ATOM feeds in analysis/Doug/ notebook.
Did some refactoring in nowcast.figures.
(MEOPAR)


Week 51
-------

Mon 14-Dec-2015
^^^^^^^^^^^^^^^

Congratulated Nancy on the accuracy of the model residuals in her Dec analysis notebook, and discussed nowcast.figures refactoring.
Discussed forcing for 8-Dec nowcast-green run w/ Elise to help her reproduce the exploding nutrients; also talked about her run failures on orcinus that I offered to investigate.
Checked in with Muriel and briefly discussed nowcast.figures refactoring, and extraction of code into salishsea_tools modules.
Investigate nowcast 12 forecast download_weather worker failure: same Content-Length header issue as on 23-Nov; looks like EC server is sending text/plain; send email to Sandarine@EC.
Continued work on nowcast ATOM feeds in notebook.
Hacked around EC issue to get 12 and 18 weather downloads and get nowcast/forecast runs happening in the evening.
(MEOPAR)

Attended Phys Ocgy seminar by Lian Kwong on micronekton ecosystem modeling.

Christmas lunch w/ MOAD group.

Headache and fatigue in the late afternoon and evening.


Tue 15-Dec-2015
^^^^^^^^^^^^^^^

Fatigue and body aches.

Nowcast 06 weather download got 2 zero length files that caused grib_to_netcdf worker to fail; Susan manually re-downloaded the files and I manually re-ran grib_to_netcdf worker to restart automation and get forecast2 run going at 08:15.
12 weather forecast was still MIA at 11:00.
Continued work on nowcast ATOM feeds in notebook.
Downloaded missing 11dec15 HRDPS research forecast.
Salish Sea team meeting; see Google Drive whiteboard.
(MEOPAR)

Restarted build slaves on smelt and snapper.
(SOG)


Wed 16-Dec-2015
^^^^^^^^^^^^^^^

Worked on recovering nowcast system; 15dec15 12 and 18 HRDPS weather forecasts never appeared on EC site.
Via various hacks and weather file symlink patches got 15dec15 nowcast and forecast runs, then moved on to 16dec15.
Reviewed Muriel's refactoring of the nowcast.research_ferries module.
(MEOPAR)

Investigated ZeroDivisionError exceptions in Compare page view; e.g. Squamish-Richmond is for Institutional size 0 and None values; added some logging and tested some other cases and it looks like the exception occurs capital by dimension HVSIs whenever there is missing data for one of the communities, so it is a 0/0 situation.
(sealinkd)

Christmas shopping


Thu 17-Dec-2015
^^^^^^^^^^^^^^^

Several 06 forecast weather files downloaded as zero length; Susan manually re-downloaded them and I ran grib-to_netcdf manually to restart the automation for the forecast2 run.
EC emailed about grid changes for the forecast models that were rolled out on 15Dec but made no mention of missing forecasts, etc.
Continued work on nowcast ATOM feeds in notebook; realized that wind reported in feed should be average for 4 hrs before max water level to provide information about wave setup.
(MEOPAR)

Site visit re: isoinfo server RAID rebuild & Minerva maintenance; see notes in 17dec15-isoinfo-maint.rst file in client file.
(Nordion)


Fri 18-Dec-2015
^^^^^^^^^^^^^^^

Site visit re: Minerva maintenance; see notes in 17dec15-isoinfo-maint.rst file in client file.
(Nordion)

One 06 forecast weather file downloaded as zero length; Susan manually re-downloaded it and I ran grib-to_netcdf manually to restart the automation for the forecast2 run.
Two 06 forecast weather files downloaded as zero length; Susan manually re-downloaded them and I ran grib-to_netcdf manually to restart the automation for the nowcast run.
Continued work on nowcast ATOM feeds in notebook; finished 4 hr average wind calculations, and made a lot of progress on the template and rendering it to RST then HTML.
(MEOPAR)


Sat 19-Dec-2015
^^^^^^^^^^^^^^^

Upgraded kudu to Ubuntu 15.10 "Wily Werewolf".

One 06 forecast weather file downloaded as zero length; Susan manually re-downloaded it and I ran grib-to_netcdf manually to restart the automation for the forecast2 run.
Helped Susan refactor map generation to reduce bloat that started when we moved to Python 3.5 and matplotlib 1.5.
Fixed use of FileNotFoundError in prepare.py so that it works for Python 2.7 and 3.5.
Fixed nemo34 bug in salishsea run re: orcinus modules.
Started work on adding forcing link checks to NEMO-3.6 to salishsea prepare.
(MEOPAR)


Sun 20-Dec-2015
^^^^^^^^^^^^^^^

One 06 forecast weather file downloaded as zero length; Susan manually re-downloaded it and *she* ran grib-to_netcdf manually to restart the automation for the forecast2 run.
One 12 forecast weather file downloaded as zero length; Susan manually re-downloaded it and *she* ran grib-to_netcdf manually to restart the automation for the nowcast run.
Did code review on Susan's figures.py refactoring.
Committed and pushed 1st draft of adding forcing link checks to NEMO-3.6 to salishsea prepare for Susan to test on nowcast-green.
Fixed wind calculation bugs in nowcast ATOM feeds in notebook, and added humanized time of day calculation.
Produced a feed that I could read on feedly!
(MEOPAR)

Did year-end database rollover on randopony.
Fixed a membership link bug in populaires entry form view.
Updated membership link to 2016.
Set up New Year's Pop event.
(RandoPony)


Week 52
-------

Mon 21-Dec-2015
^^^^^^^^^^^^^^^

Updated Sublime Text 3 theme on kudu to SoDaReloaded.

EC wateroffice site is down so ECget failed to collect daily average flows for Fraser and Englishman; Susan patched Fraser flow for nowcast w/ yesterday's file.
One 06 forecast weather file downloaded as zero length; Susan manually re-downloaded it ran grib-to_netcdf manually to restart the automation for the forecast2 run.
Started development of nowcast make_feeds worker.
Dealt with mysterious permission error during forecast2 sphinx build.
Generated feeds for forecast2 and forecast from notebook and manually uploaded them to site.
(MEOPAR)

Separated project files from client files on kudu and set up client files repo for Nordion w/ cloud storage on Bitbucket.
(43ravens)

Wrote draft of report to Nordion re: state of isoinfo server and future options.
(Nordion)


Tue 22-Dec-2015
^^^^^^^^^^^^^^^

Nowcast make_run_off worker failed due to cruft from yesterday's patching of the Fraser flow file; fixed that, downloaded Fraser and Englishman flows for yesterday, re-ran make_run_off worker, then ran upload_forcing worker to restart automation.
The run_NEMO worker crashed for forecast2 because there was no nowcast item in the checklist; edited the checklist and restarted the mgr, then ran make_forcing_links worker to restart automation.
Sent email to Cin@PMV announcing availability of their feed, thereby putting myself on the treadmill.
Started development of nowcast make_feeds worker.
Salish Sea team meeting; see Google Drive whiteboard.
(MEOPAR)


Wed 23-Dec-2015
^^^^^^^^^^^^^^^

Traveled to Parksville for Christmas holidays.

Continued development of nowcast make_feeds worker.
(MEOPAR)


Thu 24-Dec-2015
^^^^^^^^^^^^^^^

Continued development of nowcast make_feeds worker.
(MEOPAR)


Fri 25-Dec-2015
^^^^^^^^^^^^^^^

Christmas Day


Sat 26-Dec-2015
^^^^^^^^^^^^^^^

Continued development of nowcast make_feeds worker.
Created salishsea_tools.unit_conversions module.
Added ssh_timeseries_at_point() and uv_wind_timeseries_at_point() functions to salishsea_tools.nc_tools module.
(MEOPAR)


Sun 27-Dec-2015
^^^^^^^^^^^^^^^

Continued development of nowcast make_feeds worker.
Added ssh_timeseries_at_point() and uv_wind_timeseries_at_point() functions to salishsea_tools.nc_tools module.
Created salishsea_tools.wind_tools module.
(MEOPAR)


Week 53
-------

Mon 28-Dec-2015
^^^^^^^^^^^^^^^

Worked on salishsea_tools modules and unit tests.
(MEOPAR)


Tue 29-Dec-2015
^^^^^^^^^^^^^^^

Finished nowcast make_feeds worker to the point where it can be run manually to produce feed files.
(MEOPAR)


Wed 30-Dec-2015
^^^^^^^^^^^^^^^

Started development of nowcast run_NEMO36 worker, initially for nowcast-green.
Started improvement of salishsea_cmd.api.run_description() function for NEMO-3.6 runs.
(MEOPAR)


Thu 31-Dec-2015
^^^^^^^^^^^^^^^

Continued development of nowcast run_NEMO36 worker.
Continued improvement of salishsea_cmd.api.run_description() function for NEMO-3.6 runs.
(MEOPAR)


Fri 1-Jan-2016
^^^^^^^^^^^^^^

Continued development of nowcast run_NEMO36 worker.
Refactored tell_manager() function from nowcast.lib as a NowcastWorker method.
(MEOPAR)


Sat 2-Jan-2016
^^^^^^^^^^^^^^

Continued development of nowcast run_NEMO36 worker.
Refactored zmq initialiation function from nowcast.lib as a NowcastWorker method, and put WorkerError definition in nowcast_worker module.
Changed NowcastWorker so that it does note connect to the messaging system when a worker is run with the --debug flag.
(MEOPAR)


Sun 3-Jan-2016
^^^^^^^^^^^^^^

Continued development of nowcast run_NEMO36 worker.
Hooked nowcast make_feeds worker in to nowcast_mgr so that feeds generation is fully automated.
Removed clean build of salishsea site from push_to_web worker.
(MEOPAR)
