*****************
2019 Work Journal
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

Tue 1-Jan-2018
^^^^^^^^^^^^^^

**Statutory Holiday** - New Year's Day

Handled issues from 1st day of 2018-06 production automation.
Worked with Susan to move hindcast-201812 into automation.
(SalishSea)

Continued dev of MOHID-Cmd package.
(MIDOSS)

Felt progressively crappier as the day went on; headache, body aches, fatigue.


Wed 2-Jan-2018
^^^^^^^^^^^^^^

Work with headache, body aches, sore throat, and lethargy.

Upgraded kudu and niko to Pop!_OS 18.10:
* followed https://support.system76.com/articles/upgrade-pop/
* flashed iso to USB
* after upgrade, edited files in /etc/apt/sources.list.d/ to re-enable and adjust distro names of 3rd party packages

download_live_ocean was initially launched by automation at 08:53 and failed due to file not found; repeated manual launches failed until 10:33; manual launch at 10:48 succeeded.
Hacked nemo_nowcast.workers.get_web_data() to time out on sum of sleep times instead of product of exponential waits, and SalishSeaNowcast.nowcast.workers.download_live_ocean() call to use wait_exponential_max=7200, and pushed the hacks to skookum for testing tomorrow.
Updated copyright year range in:
* SalishSeaCmd
* SalishSeaNowcast
(SalishSea)

Continued dev of MOHID-Cmd package.
(MIDOSS)

See project journal.
(SalishSeaCast-FVCOM)


Thu 3-Jan-2018
^^^^^^^^^^^^^^

Monitored download_live_ocean; new timeout calc in get_web_data() worked as expected, but 7200s wasn't long enough; collect_weather finished at ~08:40 and LiveOcean file wasn't ready until ~11:20; increased wait_exponential_max=10800.
Discovered that 18-06 ERDDAP dataset updates have turned into a dumpster fire :-(
(SalishSea)

See project journal.
(SalishSeaCast-FVCOM)

See project journal.
(Resilient-C)


Fri 4-Jan-2018
^^^^^^^^^^^^^^

Team mtg; see whiteboard.
Started dev of mohid run subcomaand.
(MIDOSS)

Worked w/ Ben to get SalishSeaCmd and Mercurial working under Python 3.5 on orcinus:
* see hg build notes from Tue 11-Sep-2018, but load gcc and do make install-home
* change PATH to put $HOME/bin near the front
* hg version is stuck at 4.8rc0
download_live_ocean worked on 1st try at 08:26; forecast finished at 09:48; nowcast-agrif was queued at 09:49; nowcast-green finished at 11:39.
Disabled ECget river flow crob jobs on sallish in favour of collect_river_data worker.
Worked with Susan to sort why 18-06 ERDDAP datasets suddenly disappeared; nowcast-green/31dec18 files downloaded from ceder were 30dec18 by accident; Susan fixed that.
Email to Emilio re: availability of new datsets for NANOOS and change in dataset id version.
(SalishSea)


Sat 5-Jan-2018
^^^^^^^^^^^^^^

2018-2019 financial roll-over


Sun 6-Jan-2018
^^^^^^^^^^^^^^

upload_forcing nowcast+ got triggered before grib_to_netcdf finished due to race conditions between grib_to_netcdf and make_live_ocean_files, but no runs got launched; recovery:
* upload_forcing west.cloud nowcast+
* upload_forcing orcinus nowcast+
* upload_forcing cedar nowcast+
(SalishSea)

Demoted Fraser water quality buoy wind speed from warning level notification because sensor is out of commission and we don't care.
(ECget)

See project journal.
(SalishSeaCast-FVCOM)


Week 2
------

Mon 7-Jan-2018
^^^^^^^^^^^^^^

Sent email to Roman requesting chang nowcast-agrif reservation window to 10:00 to 13:00, and asking if he will consider building a Python 3.7 module on orcinus.
Sent email to Michael & Maxim re: change to 2018-06 config and sarracenia-based HRDPS file management.
Updated ERDDAP index page re: dates of V17-02 to V18-06 change-over and planned removal dates for V17-02 datasets.
Started updating tide gauge station water level datasets from V17-02 to V18-06.
(SalishSea)

Phys Ocgy seminar by Hayley Dosser.

Scary experience with Mercurial and SalishSeaNowcast: niko was left with tip on branch closure commit and when I pulled in work since 23-Dec hg update failed with a traceback about a node with no descendents.

Continued dev of mohid run sub-command.
(MIDOSS)


Tue 8-Jan-2018
^^^^^^^^^^^^^^

Investigated figure failures due to ERDDAP dataset id changes and found that accommodating mix of 17-02 and 18-06 is very troublesome.
Continued updating tide gauge station water level datasets from V17-02 to V18-06.
(SalishSea)

Continued dev of mohid run sub-command.
(MIDOSS)



* Replace old 2014 bloomcast page on ~sallen w/ redirect to present page
* Stephanie would like web access to prior year's bloomcasts




SalishSeaAGRIF production:
* generate sub-grids mapping dict for rivers so that sub-grid runoff files can be worker-generated instead of interpolated from full domain runoff file by nesting tools
* get Haro Strait sub-grid working
* enable turbidity, if possible

Move production to 201702:
* Rename riverTurbDaily2_*.nc to (at least) exclude the 2
* Update dir tree in docs/results_server/index.rst


* Process some images
* Take knives for sharpening


ToDo
====

* refactor, unit tests & docs for forcing links checking for NEMO-3.6

* reduce resolution of landing page images for faster load times
* add docs re: Resilient-C server-side app framework
* add EduCloud deployment docs

* research_ferries module
* JSON logging use example notebook

* review remaining nosy PRs
