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
Continued pulling upstream changesets in to NEMO-3.6.
(MEOPAR)

Investigated randopony persona.org sign-in issue discovered on 28Jun and found that it is not a problem today - wierd.
Investigated deform widgets issue discovered on 28Jun; on kudu it is resolved by downgrading to deform==0.9.9.
Updated deployment to 2015r1 release; lots of manual work because of fabric security issue that seems to be about my local userid not matching the bcrandonneur userid on webfaction.
Explored Unicode handling issue in brevet pre-registration and discovered that it is in the email generation functions, not the form handers.
(RandoPony)

Finalized proposal for UBC SCARP SeaLink'd web app project and emailed it to Stephanie.
(sealinkd)

After a  lot of mucking about to figure out which packages I had't yet installed, got enough TeX and LaTeX packages and fonts installed to render sealinkd proposal from rst to pdf via both rst2latex and pandoc; former produces nicer output, presumably due to deficiencies in pandoc's rst parser; e.g. no generic role (:data:) handling.
