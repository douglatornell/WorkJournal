*****************
2017 Work Journal
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

Mon 2-Jan-2017
^^^^^^^^^^^^^^

Started feeling onset of flu or some other viral infection.

Fixed bugs in NEMO-Cmd deflate and combine modules.
Worked on de-boilerplating SalishSeaNowcast unit tests; issue #6.
(SalishSea)


Tue 3-Jan-2017
^^^^^^^^^^^^^^

Seriously hammered by virus.


Wed 4-Jan-2017
^^^^^^^^^^^^^^

Starting to recover from virus; felt like I had incipient motion sickness for a lot of the day, especially when working on kudu.

Finished de-boilerplating SalishSeaNowcast unit tests; issue #6.
(SalishSea)

See project work journal.
(GOMSS)


Thu 5-Jan-2017
^^^^^^^^^^^^^^

Continuing to recover from virus; incipient motion sickness feeling relented somewhat by the end of the day.

See project work journal.
(GOMSS)

Continued refactoring combine plug-in in NEMO-Cmd.
(SalishSea)


Fri 6-Jan-2017
^^^^^^^^^^^^^^

Continuing to recover from virus.

Started testing free tier of rescuetime.com.

See project work journal.
(GOMSS)

Continued refactoring combine plug-in in NEMO-Cmd.
Updated NEMO-3.6, XIOS, etc. on /data on salish, and on orcinus to do test runs of NEMO-Cmd tools.
(SalishSea)


Sat 7-Jan-2017
^^^^^^^^^^^^^^

Continuing to recover from virus.

Tested and debugged on orcinus combine plug-in and integration of combine, deflate, and gather into Salish Sea run script.
Finished refactoring combine plug-in in NEMO-Cmd.
(SalishSea)


Sun 8-Jan-2017
^^^^^^^^^^^^^^

Continuing to recover from virus.

Tested refactored NEMO-Cmd integrated into SalishSeaCmd on orcinus and salish.
Worked on moving west.cloud nowcast to /nemoShare/MEOPAR/:
* Deleted ~/MEOPAR-nfs symlink on nowcast0
* Updated all repo clones in /nemoShare/MEOPAR/nowcast-sys/nemo_nowcast-env/
* Rebuilt XIOS
* Rebuilt NEMO-3.6 at r6770
* Rebuilt rebuild_nemo
* Created /nemoShare/MEOPAR/nowcast-sys/nemo_nowcast-env/etc/conda/activate.d/envvars.sh
* Updated paths in nowcast.yaml
* Successfully uploaded forcing for 07jan18 and 08jan18, make symlinks, and ran nowcast/08jan17.
Pushed integration of NEMO-Cmd into SalishSeaCmd.
Re-ran forecast/08jan17 in /nemoShare/MEOPAR/nowcast-sys via automation.
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
