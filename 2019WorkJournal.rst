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



Wed 2-Jan-2018
^^^^^^^^^^^^^^

Upgraded kudu to Pop!_OS 18.10:
* followed https://support.system76.com/articles/upgrade-pop/
* flashed iso to USB
* after upgrade, edited files in /etc/apt/sources.list.d/ to re-enable and adjust distro names of 3rd party packages

download_live_ocean was initially launched by automation at 08:53 and failed due to file not found; repeated manual launches failed until 10:33; manual launch at 10:48 succeeded.
Hacked nemo_nowcast.workers.get_web_data() to time out on sum of sleep times instead of product of exponential waits, and SalishSeaNowcast.nowcast.workers.download_live_ocean() call to use wait_exponential_max=7200, and pushed the hacks to skookum for testing tomorrow.
(SalishSea)




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
