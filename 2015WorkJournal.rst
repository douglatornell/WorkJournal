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

There was a hiatus in my journalling between Fri 17-Oct-2014 and Wed 27-May-2015 - sorry!


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

Pinged Stephanie & Penny about atatus of SealinkD project agreement and got reply that UBC Procurement are working on it.
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


Fri 18-Sep-2015
^^^^^^^^^^^^^^^

Finished refactoring the 02-collab section of the hg-novice lesson to the extent that needs to be done for next week's workshop; same for 03-conflict, and 04-open sections.
Created PR in Python lesson repo to add command reminders page & docs links.
(SWC)


Thu 17-Sep-2015
^^^^^^^^^^^^^^^

Tried to add Stephanie to Bitbucket Sealinkd team and discovered that it is limited to 5 collaborators, probably because it was created from my non-academic account.
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
