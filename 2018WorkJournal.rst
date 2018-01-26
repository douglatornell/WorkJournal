*****************
2018 Work Journal
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

Mon 1-Jan-2018
^^^^^^^^^^^^^^

**Statutory Holiday** - New Year's Day

Travel home from Parksville

Fixed bug in make_live_ocean_files re: file name template as Path instead of string.
Discovered that netcdf4-1.2.4 supports opening datasets from Path instances.
After a long thrash, got to the bottom of make_live_ocean_files seemingly creating the file for the previous day - it's due to writing to a symlink created by make_forcing_links when the previous day's make_live_ocean_files fails.
(SalishSea)


Tue 2-Jan-2018
^^^^^^^^^^^^^^

upload_forcing make symlink to 01jan18 LiveOcean files, as expected; moved it aside, but need to figure out how to force make_live_ocean_files to overwite it with a file instead of writing to it.
Changed make_live_ocean_files to delete any existing symlink with the name of the file to be generated for the present day.
(SalishSea)

See project work journal.
(GOMSS)

See project journal.
(SalishSeaCast-FVCOM)


Wed 3-Jan-2018
^^^^^^^^^^^^^^

Discussed ONC ADCP data trials and tribulations w/ Rich.
Worked on get_onc_ferry worker, and updating ERDDAP dataset XML fragment; TWDP files aside; started backfill downloading in tmux bash loop.
(SalishSea)


Thu 4-Jan-2018
^^^^^^^^^^^^^^

Travel from home to Barrie.

See project journal.
(SalishSeaCast-FVCOM)


Fri 5-Jan-2018
^^^^^^^^^^^^^^

See project journal.
(SalishSeaCast-FVCOM)


Sat 6-Jan-2018
^^^^^^^^^^^^^^

See project journal.
(SalishSeaCast-FVCOM)


Sun 7-Jan-2018
^^^^^^^^^^^^^^

See project journal.
(SalishSeaCast-FVCOM)

Started work on well-documented dev of class-based SeaTracker module.
(SalishSea)


Week 2
------

Mon 8-Jan-2018
^^^^^^^^^^^^^^

See project journal.
(SalishSeaCast-FVCOM)

SalishSeaCast salinity and temperature fields went live on nvs.nanoos.org!
(SalishSea)


Tue 9-Jan-2018
^^^^^^^^^^^^^^

Continued work on well-documented dev of class-based SeaTracker module.
(SalishSea)


Wed 10-Jan-2018
^^^^^^^^^^^^^^^


Thu 11-Jan-2018
^^^^^^^^^^^^^^^

Continued work on well-documented dev of class-based SeaTracker module.
(SalishSea)


Fri 12-Jan-2018
^^^^^^^^^^^^^^^

Continued work on well-documented dev of class-based SeaTracker module.
(SalishSea)

See project journal.
(SalishSeaCast-FVCOM)


Sat 13-Jan-2018
^^^^^^^^^^^^^^^

See project journal.
(SalishSeaCast-FVCOM)


Week 3
------

Mon 15-Jan-2018
^^^^^^^^^^^^^^^

See project journal.
(SalishSeaCast-FVCOM)

Travelled home crom Barrie


Tue 16-Jan-2018
^^^^^^^^^^^^^^^

Salish Sea team mtg; see whiteboard.
Continued changing ssh vs. tide prediction figure to use forecast datasets.
(SalishSea)


Wed 17-Jan-2018
^^^^^^^^^^^^^^^

See project journal.
(SalishSeaCast-FVCOM)

See project work journal.
(GOMSS)


Thu 18-Jan-2018
^^^^^^^^^^^^^^^

See project journal.
(SalishSeaCast-FVCOM)

See project work journal.
(GOMSS)


Fri 19-Jan-2018
^^^^^^^^^^^^^^^

See project journal.
(SalishSeaCast-FVCOM)

Canyons/Arctic group mtg; see whiteboard.
(Canyons/Arctic)

Continued changing ssh vs. tide prediction figure to use xarray.
(SalishSea)

See project journal.
(Resilient-C)


Sat 20-Jan-2018
^^^^^^^^^^^^^^^

See project journal.
(SalishSeaCast-FVCOM)

Uploaded gemlam/2014[10|11]*.bz2 from 1Tb drive to /data/dlatorne/MEOPAR/GEMLAM/2014/.
(SalishSea)


Sun 21-Jan-2018
^^^^^^^^^^^^^^^

Walked down to Kits Beach to observe morning high tide and storm surge.

Formatted red 1Tb portable drive to use as backup for kudu in preparation for change to PoP_OS!.

See project journal.
(SalishSeaCast-FVCOM)


Finished changing ssh vs. tide prediction figure to use xarray for forecast runs; still need to do forecast2.
(SalishSea)



Week 4
------

Mon 22-Jan-2018
^^^^^^^^^^^^^^^

PyCascades conference.


Tue 23-Jan-2018
^^^^^^^^^^^^^^^

PyCascades conference.


Wed 24-Jan-2018
^^^^^^^^^^^^^^^

See project journal.
(SalishSeaCast-FVCOM)

Helped Tereza sort out her NEMO build issues.
Added processing for forecast2 runs to update_forecast_datasets worker.
(SalishSea)



SalishSeaAGRIF production:
* add AGRIF option to run_NEMO worker:
  * sub-grid runoff namelists use sub-grid climatologies

Move production to 201702:
* Move LiveOcean BC files from modified/ to boundary_conditions/
* Rename LiveOcean BC files from single_LO*.nc and single_bio_LO*.nc to LO_TS_*.nc and LO_bio*.nc
* Rename riverTurbDaily2_*.nc to (at least) exclude the 2
* Update dir tree in docs/results_server/index.rst


* Process some images
* Test attrs-17.1
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
