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


Thu 25-Jan-2018
^^^^^^^^^^^^^^^

Fixed bugs in update_forecast_datasets worker re: forecast2 runs.
(SalishSea)

Continued getting kudu set up under PoP_OS!.

See project journal.
(SalishSeaCast-FVCOM)


Fri 26-Jan-2018
^^^^^^^^^^^^^^^

Opened ports on west.cloud for make_fvcom_boundary and run_fvcom worker logging; restart log_aggregator on skookum so that it knows about new ports.
Enabled compare_tide_prediction_max_ssh fig module to handle forecast2 runs.
Changed make_plots forecast* publish to launch after update_forecast_datasets worker.
Eliminated production of publish figures for nowcast runs because the information is contained in the new, long forecast* runs publish figures.
Updated SalishSeaNowcast on skookum from rev da6f17bda01b to rev 5fd55a7e6a65.
(SalishSea)

See project journal.
(SalishSeaCast-FVCOM)

Attended AAPS "Focus in the Age of distraction" training session; mediation, but I'm pretty good a focus already, it seems.

Built a new salishsea-site Vagrant VM on niko, but couldn't get it to sshfs mount /results/ for testing.
(salishsea-site)


Sat 27-Jan-2018
^^^^^^^^^^^^^^^

get_NeahBay_ssh for forecast2 run failed due to change in tidal prediction file to 10min; recovery:
* hg revert -r 677 tidal_predictions/Neah\ Bay_tidal_prediction_01-Jan-2013_31-Dec-2020.csv
* get_NeahBay_ssh forecast2
* upload_forcing west.cloud-nowcast forecast2
* hg revert -C tidal_predictions/Neah\ Bay_tidal_prediction_01-Jan-2013_31-Dec-2020.csv
Same failure happened before nowcast run, but upload_forcing or make_forcing_links papered things over for us.
Failure happened again before forecast; worked w/ Susan to fix it by giving get_NeahBay_ssh an hourly tide prediction file to work with, independent of the new 10min files we use for figures.
Susan reproduced the make_plots nowcast-green research Python core dump issue in a notebook; found that it is not an issue in a newly constructed env with conda-forge as priority channel.
(SalishSea)

Continued getting kudu set up under PoP_OS!.

Emailed Sean Farley to offer to help maintain the Mercurial PPA.

Updated nowcast-vm Vagrant description.
Struggled with inability to sshfs mount /results in Vagrant VM.
(salishsea-site)


Sun 28-Jan-2018
^^^^^^^^^^^^^^^

Ordered and received new 275Gb SSD for niko.

Started removing nowcast row from storm surge & tides section of results index and improving table layout.
(salishsea-site)


Week 5
------

Mon 29-Jan-2018
^^^^^^^^^^^^^^^

Replaced /results/nowcast-sys/nowcast-env/ on skookum with a new one built with conda-forge channel prioritized to try to resolve make_plot issues and provide pygrib for coming make_fvcom_wind worker:
* circusctl stop scheduler
* circusctl stop manager
* circusctl stop message_broker
* circusctl stop log_aggregator
* circusctl stop quit
* conda env remove --prefix /results/nowcast-sys/nowcast-env/
* conda create ... (see deployment docs)
* source activate
* pip install ... (see deployment docs)
* git clone OPPTools
* updated repos
* pip install -e ...
* created etc/conda/activated.d/envvars.sh
* created etc/conda/deactivated.d/envvars.sh
* deactivate and reactivate env to set envvars
* circusd --daemon $NOWCAST_CONFIG/circus.ini
Ran make_plots forecast2 2018-01-28 to test new env (was failing on NewWest max ssh figure);
Noted that sotrm_surge_alerts figure takes ~4min to run.
Warnings from make_plots:
* xarray/plot/utils.py:51: FutureWarning: 'pandas.tseries.converter.register' has been moved and renamed to 'pandas.plotting.register_matplotlib_converters'.converter.register()
* /results/nowcast-sys/nowcast-env/lib/python3.6/site-packages/numpy/ma/core.py:6385: MaskedArrayFutureWarning: In the future the default for ma.minimum.reduce will be axis=0, not the current None, to match np.minimum.reduce. Explicitly pass 0 or None to silence this warning.
  return self.reduce(a)
* /results/nowcast-sys/nowcast-env/lib/python3.6/site-packages/numpy/ma/core.py:6385: MaskedArrayFutureWarning: In the future the default for ma.maximum.reduce will be axis=0, not the current None, to match np.maximum.reduce. Explicitly pass 0 or None to silence this warning.
  return self.reduce(a)
Emailed stakeholders re: ERDDAP sea surface height ERDDAP datasets and forecast figures.
make_turbidity_file failed; fixed bug in numpy array copying.
Updated copyright year range in:
* SalishSeaNowcast
* salishsea-site
(SalishSea)

Did a pull request to the ropensci/rerddap project on github to add our ERDDAP server.
(prediction-core)

Phys Ocgy seminar by Ben S re: turbulence measurement in the Arctic.

Finished removing nowcast row from storm surge & tides section of results index and improved table layout.
Worked on cleanup in salishseacast views module.
Ensured that only available figures appear in figure group selectors.
(salishsea-site)

Installed 275Gb drive in niko.


Tue 30-Jan-2018
^^^^^^^^^^^^^^^

Started preparing niko for clean install of PoP_OS!:
* installed miniconda warehouse drive
* started cloning MEOPAR repos on to warehouse drive
* started creating conda envs on warehous drive

Worked on improving speed of results index page.
(salishsea-site)

Salish Sea team mtg; see whiteboard.
Helped Susan set up archival storage of nowcast-green Aug-2015 to Aug-2017 section with bad rivers.
Started refactoring ssh forecast dataset URL out of compare_tide_prediction_max_ssh module to config.
(SalishSea)

See project journal.
(SalishSeaCast-FVCOM)


Wed 31-Jan-2018
^^^^^^^^^^^^^^^

Dentist Appt

Continued getting kudu set up under PoP_OS!.

See project journal.
(SalishSeaCast-FVCOM)

Email convo w/ Rich & Katia about averaging of Fraser River flow.
(SalishSea)

See project journal.
(Resilient-C)


February
--------

Thu 1-Feb-2018
^^^^^^^^^^^^^^

Telcon from Kathlean Knapp @ Homecare.

Consultation at Body & Soul.

See project journal.
(Resilient-C)

See project journal.
(SalishSeaCast-FVCOM)


Fri 2-Feb-2018
^^^^^^^^^^^^^^

Continued preparing niko for clean install of PoP_OS!:
* continued cloning MEOPAR repos on to warehouse drive
* cloned MOAD repos on to warehouse drive

SalishSeaCast results index page sped up to 3.25s now that 16-28 Jan time series and biology image loop figures are available.
Refactored ssh forecast dataset URL out of compare_tide_prediction_max_ssh module to config.
Added CHS water level observations to compare_tide_prediction_max_ssh figure.
(SalishSea)

Canyons/Arctic team mtg; see whiteboard.
(Canyons/Arctic)


Sat 3-Feb-2018
^^^^^^^^^^^^^^

Continued getting kudu set up under PoP_OS!.

Did the year-end randopony database rollover via the database interface in PyCharm.
Set up Chili 200 and emailed Mike.
(randopony)

Helped Elise sort out missing arrow dependency on bugaboo.
(SalishSea)

See project work journal.
(GOMSS)


Sun 4-Feb-2018
^^^^^^^^^^^^^^

Cleared backlog of issues in Sentry.
(SalishSea)

Finished preparing niko for upgrade to PoP_OS! and installed it (had to physically remove 275Gb drive so that grub could install on internal drive).
Started setting niko up under PoP_OS!

February
========

Week 6
------

Mon 5-Feb-2018
^^^^^^^^^^^^^^

Continued getting niko set up under PoP_OS!.



Need to suppress zeep output in debug log.



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
