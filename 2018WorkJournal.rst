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

upload_forcing made symlink to 01jan18 LiveOcean files, as expected; moved it aside, but need to figure out how to force make_live_ocean_files to overwite it with a file instead of writing to it.
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

Travelled home from Barrie


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

Did clean install of Pop!_OS 17.10 on 120Gb SSD OS drive.

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
Noted that storm_surge_alerts figure takes ~4min to run.
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
* started creating conda envs on warehouse drive

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

Discussed automation of hindcast runs on cedar w/ Susan; see whiteboard photo.
Discussed Fraser flow values w/ Rich & Katia.
Started setting up projects/SalishSea/hindcast-sys/ tree on cedar:
* cloned repos
* built XIOS-2
* built NEMO-3.6-code SMELT config
* built NEMO-3.6-code REBUILD_NEMO
Set up hindcast-sys/17nov14/ where we will initialize from, but discussion w/ Susan revealed that we can't run there yet due to bathymetry issues; run from neap in mid-Nov 2017 for testing.
(SalishSea)

Started exploring new ONC data API docs: https://wiki.oceannetworks.ca/display/O2A/Oceans+2.0+API+Home
(ONC API)


Tue 6-Feb-2018
^^^^^^^^^^^^^^

Continued getting niko set up under PoP_OS!.

Continued setting up projects/SalishSea/hindcast-sys/ tree on cedar:
* Deleted hindcast-sys/17nov14/ because we're not ready for it, and we decided to keep the results on $SCRATCH
* Created $SCRATCH/hindcast/
* Installed miniconda3 in $PROJECT/SalishSea/hindcast-sys/
* set aside system PYTHONPATH with `export OLD_PYTHONPATH=$PYTHONPATH; unset PYTHONPATH`
* created $PROJECT/SalishSea/hindcast-sys/hindcast-env conda env
* installed Python packages
* Set up 16nov17 run in hindcast-sys/runs
* squeue -u $USER -o"%i %j %t %r %S" provides:
    JOBID NAME ST REASON START_TIME
    4747883 16nov17hindcast PD Priority N/A
  before job is scheduled, and:
    JOBID NAME ST REASON START_TIME
    4749279 16nov17hindcast PD Priority 2018-02-06T19:10:22
  once it has an allocation, and:
    JOBID NAME ST REASON START_TIME
    4749279 16nov17hindcast R None 2018-02-06T18:16:26
  when the job is running.
* 16nov17 run failed due to river turbidity file path issue.
Salish Sea team mtg; see whiteboard.
(SalishSea)


Wed 7-Feb-2018
^^^^^^^^^^^^^^

Dentist appt re: lr molars contact.

See project work journal.
(GOMSS)

See project journal.
(SalishSeaCast-FVCOM)

Replied to email from Neeraj Kashyap @google re: getting started running NEMO on GCP; contact from PyCascades.
(SalishSea)


Thu 8-Feb-2018
^^^^^^^^^^^^^^

See project journal.
(SalishSeaCast-FVCOM)

See project work journal.
(GOMSS)

download_weather 12 failed; re-ran manually at 17:00 when final files appeared on datamart.
download_weather 18 failed; re-ran manually at 23:00
(SalishSea)

See project journal.
(SalishSeaCast-FVCOM)

Fitness assessment at Body & Soul.

See project journal.
(Resilient-C)


Fri 9-Feb-2018
^^^^^^^^^^^^^^

See project journal.
(SalishSeaCast-FVCOM)

Continued setting up hindcast automation on cedar:
* fixed river turbidity forcing path issue
* fixed LiveOcean forcing path issue
* had to change tracers/west/bioOBC_const.nc to make time_counter a record dimension
* had to update LiveOcean file to wide western boundary (Susan's dec18 refactoring)
Started dev of watch_NEMO_hindcast worker.
(SalishSea)

Canyons/Arctic group mtg; see whiteboard.
(Canyons/Arctic)

See project work journal.
(GOMSS)


Sat 10-Feb-2018
^^^^^^^^^^^^^^^

See project work journal.
(GOMSS)

See project journal.
(Resilient-C)


Sun 11-Feb-2018
^^^^^^^^^^^^^^^

See project work journal.
(GOMSS)

See project journal.
(Resilient-C)

Investigated TWDP ferry data failures since 7feb; TWDP.N2 nav sensors appear to have stopped working, but TWDP.N1 are working again; refactored get_onc_ferry to enable it to work with a list of nav sensor station identifiers.
Updated get_onc_ferry and get_onc_ctd to use xarray>=0.10.0 resampling API.
(SalishSea)


Week 7
------

Mon 12-Feb-2018
^^^^^^^^^^^^^^^

Travel to Barrie.


Web 14-Feb-2018
^^^^^^^^^^^^^^^

nowcast-green failed due to a west boundary condition issue; Susan symlinked 13feb LiveOcean files at 14feb and re-ran; run succeeded, but launched another nowcast-dev run that I had to kill.
(SalishSea)

See project work journal.
(GOMSS)

See project journal.
(Resilient-C)


Thu 15-Feb-2018
^^^^^^^^^^^^^^^

download_weather 06 failed; re-ran manually.
Tried a logging config edit to suppress zeep output from debug log; partially successful.
(SalishSea)

See project work journal.
(GOMSS)

See project journal.
(SalishSeaCast-FVCOM)


Fri 16-Feb-2018
~~~~~~~~~~~~~~~

download_weather 06 failed; re-ran manually.
Widened zeep logging config from zeep.transport to zeep to try to suppress more zeep output from debug log.
(SalishSea)

Travelled home from Barrie.


Sat 17-Feb-2018
~~~~~~~~~~~~~~~

upload_forcing forecast2 failed due to connection timeout on west.cloud; ssh to west.cloud initially failed, but started to work after some poking around in the west.cloud web control panel; re-ran upload_forcing manually to restart automation.
Intermittent network access to west.cloud continued; ticket to support yielded response that it is a known issue that they are working on.
Started tmux session calculating LiveOcean boundary files from 2013-01-02 from archive that Parker provided.
Worked with Susan on hindcast test run on cedar to develop watch_NEMO_hindcast worker against.
(SalishSea)


Sun 18-Feb-2018
~~~~~~~~~~~~~~~

Finished initial implementation of watch_NEMO_hindcast.
Continued tmux session calculating LiveOcean boundary files from 2013-01-02 from archive that Parker provided.
Started dev of run_hindcast.
(SalishSea)


Week 8
------

Mon 19-Feb-2018
^^^^^^^^^^^^^^^

Body & Soul session w/ Stephen.

upload_forcing forecast2 failed due to network connectivity issue.
nowcast run went unstable.
Restarted log_aggregator to try to restore progress log messages from watch_NEMO.
Continued tmux session calculating LiveOcean boundary files from 2013-01-02 from archive that Parker provided.
Committed change from 10min avg to instantaneous values in VHFR FVCOM boundary files and updated SS-run-sets on west.cloud with changesets 703f5f930807:9da857a8ccee.
Susan cleaned up tracers/west/bioOBC_const.nc in repo and pulled it on to west.cloud.
Susan confirmed that domvvl ...
Restarted nowcast circus daemon after a thrash due to a bad edit in the logging config to minimize zeep log messages.
Continued dev of run_hindcast.
(SalishSea)

See project work journal.
(GOMSS)


Tue 20-Feb-2018
~~~~~~~~~~~~~~~

Finished initial implementation of run_hindcast.
Salish Sea team mtg; see whiteboard.
(SalishSea)

Explored ONC Oceans 2.0 API Python client library in notebook in analysis-doug/onc-api.
(ONC API)


Wed 21-Feb-2018
~~~~~~~~~~~~~~~

get_NeahBay_ssh failed because it couldn't find a port to log to; Susan re-ran manually to restart automation.
dowload_results forecast2 failed because it couldn't fix perms on the Neah Bay ssh txt file that was owned by Susan for some reason; files were okay, used sudo to fix perms; re-ran update_forecast_datasets to restart automation.
Created new nowcast-fig-dev conda env on kudu to use conda-forge priority and h5netcdf.
(SalishSea)

See project journal.
(SalishSeaCast-FVCOM)

Body & Soul session w/ Yusuke.


Thu 22-Feb-2018
~~~~~~~~~~~~~~~

upload_forcing forecast2 failed due to network issue on west.cloud;
get_onc_ferry failed because it couldn't find a port to log to; added more ports to config, and restarted log log_aggregator.
make_live_ocean_files ran for 21feb instead of 22feb; re-ran manually
Ran make_forcing_links salish --shared-storage to launch nowcast-dev run.
(SalishSea)

See project journal.
(SalishSeaCast-FVCOM)

See project work journal.
(GOMSS)


Fri 23-Feb-2018
~~~~~~~~~~~~~~~

west.cloud network issue resolved overnight.
forecast2 failed due to missing 22feb atmospheric forcing file; Susan launched workers manually to start catch-up.
(SalishSea)

Continued exploration of ONC Python client library in JupyterLab; couldn't get a successful 2h dataset from SCVIP ADCP :-(
(ONC-API)

See project journal.
(SalishSeaCast-FVCOM)

See project work journal.
(GOMSS)

Started work on setting up 2018 bloomcast:
* archived 2012-2017 files into directories
* cp 2017_bloomcast_inifile.yaml 2018_bloomcast_infile.yaml
* edit 2018_bloomcast_infile.yaml
* edit config.yaml
* disable push to web for test run
* test run succeeded: 14mar 16mar 27mar 10apr 15apr
* enabled push to web
* deleted wind_data_date to allow repeat run for today
* run manual production run; success! :-)
* checked bloomcast page on salishsea-site
* edit new weather descriptions into cloud fraction file and commit
* commit 2018 config file
* tag for 2018
* enable cron job on salish
(bloomcast)


Sat 24-Feb-2018
~~~~~~~~~~~~~~~

Walked to Granville Island and back along the shoreline, in the snow.
Haircut to a shorter me.

See project work journal.
(GOMSS)

Experimented with Python asyncio for ECCC datamart file downloads; implementation was not difficult for the basics; async was generally faster for 1 or 2 hours of files, but less conclusively so for 6 hours.


Sun 25-Feb-2018
~~~~~~~~~~~~~~~

See project work journal.
(GOMSS)

Changed bloomcast view so that bloom date log shows most recent predictions at the top.
(salishsea-site)

Helped Susan with debugging 2016 bloomcast date fail.
(bloomcast)

Worked on migrating sqlalchemyorg to blogofile 0.8.3 under Python 3.

Week 9
------

Mon 26-Feb-2018
^^^^^^^^^^^^^^^

Body & Soul session with Theresa.

Added Heavy Snow to cloud fraction mapping.
(bloomcast)

upload_forcing nowcast failed due to west.cloud network connection issue.
Added u&v velocity fields rolling forecast datasets to ERDDAP.
Started work on adding seasonal average tracer fields dataset to ERDDAP.
(SalishSea)

Phys Ocgy seminar about Raman spectra temperature measurement in water w/ lasers.


Tue 27-Feb-2018
^^^^^^^^^^^^^^^

See project work journal.
(GOMSS)


Finished adding seasonal average tracer fields dataset to ERDDAP.
Salish Sea team mtg; see whiteboard.
nowcast stalled in download_weather, and again in upload_forcing
ERDDAP failed to restart after Charles increased JVM memory to 8Gb; I figured out how to bump limits to 3000mb, got dataset memory warnings, so bumped to 4500mb; continued to get dataset memory warnings, and continued to increase JVM memory in 1500mb steps to 12000mb; continued to get dataset memory warnings, so reset JVM memory to 6000mb.
Refactored make_plots to accept model CLI arg, and tested it on missing make_plots nemo nowcast research 2017-02-17 figures.
Added fvcom nowcast publish workflow to make_plots.
(SalishSea)

See project journal.
(SalishSeaCast-FVCOM)


Wed 28-Feb-2018
^^^^^^^^^^^^^^^

Decreased wwatch3 results retention on west.cloud from 30 to 15 days.
Added cron jobs on west.cloud to delete wwatch3 wind and current forcing files older than 15 days.
rsynced wwatch3/forecast/11apr17 to 30nov17 from skookum to west.cloud SoG_ww3_share/forecast/ for Johannes to grab; took ~xx per month
Added cron job on west.cloud to delete fvcom-nowcast results directories older than 15 days.
(SalishSea)

See project journal.
(Resilient-C)

Body & Soul session w/ Stephen.


Thu 1-Mar-2018
^^^^^^^^^^^^^^

See project journal.
(Resilient-C)

Deleted west.cloud:SoG_ww3_share/forecast directory after email from Johannes that he is done with it.
(SalishSea)

Mucked around with nowcast-vm Vagrantfile, trying to get sshfs to skoookum working again inside VM; works in simple test VM and several more complete iterations.

See project journal.
(SalishSeaCast-FVCOM)

Worked on bikes: Shadowfax, Emma, Red.


Fri 2-Mar-2018
^^^^^^^^^^^^^^^

Canyons/Arctic team mtg; see whiteboard.
Sarauv asked how to combine NEMO results files from XIOS-1; Idalia reported that she was running nemo combine manually; looking at her stderr revealed a NEMO-Cmd bug whereby the COMBINE, GATHER, and DEFLATE shell vars in NEMO.sh had double {} around them.
Fixed the bug in NEMO-Cmd, but had to hack it with a "module load nco" command to that it will work for Birgit on graham; that module load should be in the YAML file.
(Canyons/Arctic)

Discussed ONC API w/ Rich.
(ONC-API)

Started work on changing SalishSeaCmd to use account rrg-allen for runs on cedar because bugaboo is gone and our allocation has been moved to cedar.
(SalishSea)


Sat 3-Mar-2018
^^^^^^^^^^^^^^

Travel to Parksville by bike.

Continued work on changing SalishSeaCmd to use account rrg-allen for runs on cedar.
Removed bugaboo from working environment docs because it has been decommissioned.
(SalishSea)


Sun 4-Mar-2018
^^^^^^^^^^^^^^

Finished changing SalishSeaCmd to use account rrg-allen for runs on cedar, and removed handling for bugaboo.
(SalishSea)

Forked sqlalchemyorg on Bitbucket and started serious work on migrating it to blogofile 0.8 and Python 3.

Travel home from Parksville by bike.


March
=====

Week 10
-------

Mon 5-Mar-2018
^^^^^^^^^^^^^^

Body & Soul session w/ Theresa.

Cédric Chavanne from Rimouski give SCOR west tour seminar on his method for verification of mesoscale heat flux parametrizations for the winter mixing layer in global climate models.

See project journal.
(SalishSeaCast-FVCOM)

Renewed CMOS membership.
Submitted CMOS abstract.


Tue 6-Mar-2018
^^^^^^^^^^^^^^

Salish Sea team mtg; see whiteboard.
Added account key for sbatch machines to SalishSeaCmd example YAML files.
(SalishSea)

Continued exploration of ONC API for ADCP data products; it works.
Discussed ONC API w/ Rich.
(ONC-API)

Set up ubc-moad account on readthedocs.org, imported MOAD/docs repo as ubc-moad-docs, added me as an admin, enabled webhook on Bitbucket for on-push builds, initialized Sphinx docs framework.
(MOAD)

Travel to Nanaimo for SoPO meeting.

Verified bug report from Golnaz re: image.path() call model arg, and applied her fix.
(salishsea-site)


Wed 7-Mar-2018
^^^^^^^^^^^^^^

Repeated tmux session calculating LiveOcean boundary files from 2013-01-02 from archive that Parker provided; using Susan's most recent stabilization code in tools repo.
Replaced 25aug15 through 31dec15 nowcast-green files w/ bad rivers w/ same period hindcast files.
(SalishSea)

SoPO meeting in Nanaimo; see notebook.

See project journal.
(SalishSeaCast-FVCOM)


Thu 8-Mar-2018
^^^^^^^^^^^^^^

SoPO meeting in Nanaimo; see notebook.

Added 4d fields for baroclinic VHFR FVCOM boundary conditions.
Continued repeating tmux session calculating LiveOcean boundary files from 2013-01-02 from archive that Parker provided; using Susan's most recent stabilization code in tools repo.
(SalishSea)


Fri 9-Mar-2018
^^^^^^^^^^^^^^

Body & Soul session w/ Theresa.

download_weather 12 failed; re-ran manually to restart automation.
Confirmed that FVCOM boundary files were correctly generated and that make_fvcom_boundary was able to use them successfully.
Continued repeating tmux session calculating LiveOcean boundary files from 2013-01-02 from archive that Parker provided; using Susan's most recent stabilization code in tools repo.
Update west.cloud SalishSeaNowcast from 1454:2e8b0ecdcb17 to 1479:d3f054ab58bb.
Changed SalishSeaNowcast docs to use Python 3.6 on readthedocs, but need to handle a bunch of import errors.
(SalishSea)

See project journal.
(SalishSeaCast-FVCOM)


Sat 10-Mar-2018
^^^^^^^^^^^^^^^

Finished repeating tmux session calculating LiveOcean boundary files from 2013-01-02 from archive that Parker provided; using Susan's most recent stabilization code in tools repo; cleaned up /results/forcing/LiveOcean/; rsynced files to cedar.
Replaced 01jan16 through 23aug17 nowcast-green files w/ bad rivers w/ same period hindcast files.
Added salishsea-nowcast key to cedar in preparation for production hindcast operations.
Hooked download_results into automation after watch_NEMO_hindcast.
Got Python3.6 builds working on readthedocs for SalishSeaNowcast.
(SalishSea)


Sun 11-Mar-2018
^^^^^^^^^^^^^^^

Modified Richmond loop in the sunshine.

Hooked split_results into automation after successful download_results hindcast.
Helped Susan re-process Neah Bay ssh files to extend the west boundary to match the 201702v2 bathymetry.
(SalishSea)


Week 11
-------

Mon 12-Mar-2018
^^^^^^^^^^^^^^^

upload_forcing failed due to missing runoff file:
* make_runoff_file failed due to no Fraser observation; ECget had retrieved values, but they were dated 10-Mar instead of 11-Mar; PST->PDT issue??
* re-ran ECget manually for Fraser and Englishman
* deleted bad lines from Fraser_flow and Englishman_flow files
* re-ran make_runoff_file manually
* re-ran upload_forcing to restart automation
Updated NEMO-3.6-code on west.cloud from 1133:a4ce977666d6 to 1188:e18a429921aa; did a clean build of SMELT to bring in corrected zooplankton grazing.
Updated SS-run-sets on west.cloud with changesets af97a587ca14:2bb75c3357a1.
Worked with Susan to get 201702v2 hindcast working under automation.
Automated launch of watch_NEMO_hindcast for next queued run.
Coddled 201702v2 hindcast; after Susan's 19-31aug17 runs, got sep17 done more or less under automation; oct17 run stalled on 6oct for no obvious reason.
(SalishSea)

Started writing XIOS-2 section of MOAD docs.
(MOAD)


Tue 13-Mar-2018
^^^^^^^^^^^^^^^

Body & Soul session w/ Theresa

Launched oct17 hindcast 201702v2 run via worker and it progressed past 6oct.
Salish Sea team mtg; see whiteboard.
Launched nov17 hindcast 201702v2 run via worker
oct17 hindcast run completed and nov17 run started immediately.
Launched dec17 hindcast 201702v2 run via worker
Launched jan17 hindcast 201702v2 run via worker
Observed bug in launch of split_results; wrong date.
Observed bug in run_NEMO_hindcast; YAML file is not deleted from run prep directory.
(SalishSea)

Continued writing XIOS-2 section of MOAD docs.
(MOAD)

Met w/ Birgit re: migration to XIOS-2.
(Canyons/Artic)


Wed 14-Mar-2018
^^^^^^^^^^^^^^^

Launched feb17 hindcast 201702v2 run via worker, but it NaN-ed out; Susan found that was due to 3-19feb LiveOcean files not having been updated to most recent stabilization.
Ran make_live_ocean_files for feb18 to apply Susan's most recent stabilization and uploaded files to cedar; discovered that downloaded files have been replaced with symlinks into uzipped archive that Parker sent; transformed them into files.
Launched feb17 hindcast 201702v2 run via worker again.
(SalishSea)

See project journal.
(SalishSeaCast-FVCOM)

Online intro to MOHID oil spill model by Shihan Li from Haibo's group at Dal.
(MIDOSS)

CMOS speaker tour and chapter AGM.

Continued helping Birgit re: migration to XIOS-2.
(Canyons/Arctic)


Thu 15-Mar-2018
^^^^^^^^^^^^^^^

feb17 hindcast 201702v2 run failed due to missing runoff forcing; Susan uploaded all necessary forcing files to cedar; launched feb17 hindcast 201702v2 run via worker again.
Built new nowcast-env on west.cloud with conda-forge priority and all new dependencies from OPP and surface current tiles projects.
Fixed production glitches that arose because SalishSeaCmd was not installed in new nowcast-env on west.cloud.
Copied hindcast/14mar18 restart files from cedar to west.cloud; re-ran nowcast-green/15mar18 with new restart to repair diatom bloom (among other things)
(SalishSea)

See project journal.
(SalishSeaCast-FVCOM)

Checked out Method cycling studio.

Continued helping Birgit re: migration to XIOS-2.
(Canyons/Arctic)


Fri 16-Mar-2018
^^^^^^^^^^^^^^^

See project journal.
(SalishSeaCast-FVCOM)

Downloaded and split mar18 hindcast run results.
Resurrected nowcast-green datasets that got bombed because I created 15mar18.aside/
(SalishSea)

Reviewed and improved data mgmt plan on portagenetwork.ca.
(MIDOSS)


Sat 17-Mar-2018
^^^^^^^^^^^^^^^

Cycled to Sidney.

Wwatch3 failed due to lon/lat issue; need to investigate.
(SalishSeaWaves)

See project journal.
(SalishSeaCast-FVCOM)


Sun 18-Mar-2018
^^^^^^^^^^^^^^^

Cycled on Saanich Peninsula in the morning, attended Bea's memorial in the afternoon, and cycled home to Vancouver in the evening.


Week 12
-------

Mon 19-Mar-2018
^^^^^^^^^^^^^^^

Fixed bug in make_ww3_current_file re: coordinates deletion and update to xarray 0.10.2.
Continued work on setting up SalishSeaAGRIF runs on orcinus.
(SalishSea)

Picked Jamie up from YVR.

Reviewed and fixed RST in Birgit's XIOS-1 to XIOS-2 docs.
Wrote docs section about local build and preview of MOAD docs re: contributing to them.
(MOAD)


Tue 20-Mar-2018
^^^^^^^^^^^^^^^

Salish Sea team mtg; see whiteboard.
Continued work on setting up SalishSeaAGRIF runs on orcinus.
(SalishSea)


Wed 21-Mar-2018
^^^^^^^^^^^^^^^

Pulled NEMO-3.6-code changesets c226b7b85520:b525795a2ddd on to west.cloud to correct BSi bug; did clean build of SMELT.
Replaced nowcast-green/19aug17/ through 14mar18/ with results from mesozoo correction hindcast/; bug in split_results means that restart files are all in the last day of the month.
Restarted log_aggregator to try to get make_fvcom_boundary messages back into log.
(SalishSea)

Updated to raven-6.6.0.
(salishsea-site)

See project journal.
(SalishSeaCast-FVCOM)


Thu 22-Mar-2018
^^^^^^^^^^^^^^^

See project journal.
(SalishSeaCast-FVCOM)

See project work journal.
(GOMSS)

Body & Soul session w/ Theresa

download_weather 18 failed; re-ran manually at ~18:45.
(SalishSea)


Fri 23-Mar-2018
^^^^^^^^^^^^^^^

Did ONC annual survey.

Canyons/Arctic team mtg; see whiteboard.
(Canyons/Arctic)

Discussed SMELT-AGRIF nowcast runs on orcinus w/ Susan; see office whiteboard photo.
make_plots comparison nowcast 2018-03-22 failed due ONC site down; re-ran manually.
Continued work on setting up SalishSeaAGRIF runs on orcinus; TODO:
* generate HaroStrait_init_conditions.nc
* generate BaynesSound_init_conditions.nc
* hg add namelist.time.init.*.template files
* maybe add YAML template for cold start run
Reviewed Elise's make_turbidity_file worker log message fixes; need code style cleanup.
Met w/ Roman re: orcinus fat runs:
* he can reserve a chassis (32 x 12 core nodes, 24 Gb/node) to us for a job to start in a time window and can adjust the time window on an emergency basis; reservation can be by user or group
* he can also make more storage quota available on home if we need it
(SalishSea)


Week 13
-------

Sat 31-Mar-2018
^^^^^^^^^^^^^^^

Travel to Parksville.

Started writing field_def.xml file docs.
(MOAD)

Continued work on upload_forcing for nowcast-agrif runs on orcinus.
(SalishSea)


Sun 1-Apr-2018
^^^^^^^^^^^^^^

Finished upload_forcing mods for nowcast-agrif on orcinus; worked w/ Susan to get permission correct in forcing trees in /home/sallen/.
Modified make_forcing_links for nowcast-agrif runs on orcinus.
Worked on nowcast-agrif config and got to the point of failing due to not having real initial conditions files for sub-grids.
Cloned bitbucket.org/mdunphy/nestingtools as /data/dlatorne/MEOPAR/NEMO-nesting-tools/ and built nesting tools on salish; nesting tools operate on restart files, not initial conditions files.
After discussion w/ Susan, decided to transform 19aug17 restart files to enable 1st nowcast-agrif run to be 20aug17.
(SalishSea)


April
=====

Week 14
-------

Mon 2-Apr-2018
^^^^^^^^^^^^^^

Travel home from Parksville.

Refactor ssh & sftp functions in SalishSeaNowcast.
Fix orcinus-agrif config so that upload_forcing stops failing.
(SalishSea)


Tue 3-Apr-2018
^^^^^^^^^^^^^^

Body & Soul session w/ Theresa.

Salish Sea team mtg; see whiteboard.
Pulled recent SalishSeaCmd and SalishSeaNowcast changes into production envs on skookum and west.cloud.
Worked on generation of sub-grid restart files; nesting tools are a pita.
(SalishSea)


Wed 4-Apr-2018
^^^^^^^^^^^^^^

make_forcing_links forecast2 failed because I forgot to restart manager after adding make forcing links config item; re-ran manually.
Updated mean sea level values from Marlene via 20mar18 email from Micahel for VHFR tide gauge stations into PLACES.
(SalishSea)

See project journal.
(SalishSeaCast-FVCOM)

See project work journal.
(GOMSS)


Thu 5-Apr-2018
^^^^^^^^^^^^^^

See project journal.
(SalishSeaCast-FVCOM)

See project work journal.
(GOMSS)

See project work journal.
(Resilient-C)

Spinning at Method w/ Dervia.


Fri 6-Apr-2018
^^^^^^^^^^^^^^

Finished writing XIOS-2 field_def.xml file docs.
(MOAD)

Canyons/Arctic group mtg; see whiteboard.
(Canyons/Arctic)

download_weather 12 failed; re-ran manually at ~12:26 to restart automation.
Discussed runoff files and AGRIF w/ Vicky; they are required.
Continued working on nowcast-agrif setup and testing on orcinus:
* email to Roman re: running on full nodes
* run and re-run restart nesting files creation in tmux on salish; runs that failed due to excluded variables previous work sometimes on re-runs.
Changed SalishSeaCmd to use Python 3.6 for docs builds on readthedocs.
Experimented with black code formatter on SalishSeaCmd package.
(SalishSea)


Sat 7-Apr-2018
^^^^^^^^^^^^^^

Worked on income tax returns.


Sun 8-Apr-2018
^^^^^^^^^^^^^^

Volunteered at Woodwards control of PacPop.


Week 15
-------

Mon 9-Apr-2018
^^^^^^^^^^^^^^

Continued working on nowcast-agrif setup and testing on orcinus:
* analyzed errors in 6apr18 attempt at 20aug17 run from restart that produced 2_ocean_output for the 1st time
* queued 2 test runs that use 5 nodes
* email to Roman re: pmem vs. mem directives
* Vicky says that neither she nor Idalia know how Michael did the AGRIF transformation of the NEMO configs; Idalia confirmed
* sent email to Michael about TRBTRA variable fail in Haro restart_trc generations, and how to generate AGRIFLIB/
(SalishSea)


Tue 10-Apr-2018
^^^^^^^^^^^^^^^

Updated file name for ERDDAP ubcSSg2DTracerFieldsSeasonalV17-02 dataset.
Continued working on nowcast-agrif setup and testing on orcinus:
* nn_date0 nn_it000 mismatch error in 1_oceean_output might be due to sub-grid time step factor; tested with nn_rstctl=0 for sub-grid namelist.time files
* set ln_turb to false in sub-grid namelist_smelt_cfg files as test
* the above 2 changes got me 2x5+1 run with 22 errors re: rivers bio tracers climatology files for sub-grids, and 1 error due to Haro sub-grid TRBTRA variable missing from restart
* Used nesting tools to create sub-grids rivers_bio_tracers_* files for 19-21aug17 and uploaded them to orcinus
* with the above a 2x5+1 run had 1 error due to Haro sub-grid TRBTRA variable missing from restart
* Hacked TRATRB variable into Haro restart_trc.nc by using ncks & ncrename to clone TRNTRA; had to convert files to netCDF4 due to error:
  ERROR NC_EVARSIZE One or more variable sizes violate format constraints
  HINT: NC_EVARSIZE errors can occur when attempting to aggregate netCDF3 classic files together into outputs that exceed the capacity of the netCDF3 classic file format, e.$
  ., a variable with size in excess of 2^31 bytes. In this case, try altering the output file type to netCDF3 classic with 64-bit offsets (with --64) or to netCDF4 (with -4).
   For more details, see http://nco.sf.net/nco.html#fl_fmt
* with the above a 2x5+1 run completed several steps in Haro, 1 in Baynes, and part of 1 in the full domain
* queued 5x11+1 and 5-node runs w/ 1h walltime
* 5x11+1 blew up with high velocity
* Refactored iodef, file_def & domain_def files; tested them on another 5x11+1 run
Salish Sea team mtg; see whiteboard.
(SalishSea)

Spinning at Method w/ Lauren


Wed 11-Apr-2018
^^^^^^^^^^^^^^^

Paid 2017 GST filing amount.

See project work journal.
(GOMSS)

See project work journal.
(Resilient-C)

See project journal.
(SalishSeaCast-FVCOM)


Thu 12-Apr-2018
^^^^^^^^^^^^^^^

See project work journal.
(GOMSS)

See project work journal.
(Resilient-C)

Deleted and re-created erddap-datasets conda env on kudu because of failures when I tried to update it.

Body & Soul session w/ Theresa


Fri 13-Apr-2018
^^^^^^^^^^^^^^^

make_plots nemo forecast2 failed due to network glitch at UBC that disconnected everything from Internet for 6-8 minute at ~05:30; re-ran manually to restart automation.
Started looking at NOAA Nat'l Data Buoy Center (NDBC) re: real-time buoy data for Sentry Shoal, Halibut Bank, New Dungeness, and Neah Bay; discussed how we will use those observations w/ Susan and agreed that we will not accumulate them at this time, and that I will create a function in a new MOAD-tools repo that will return the real-time (last 45 days) as a pandas dataframe.
Continued working on nowcast-agrif setup and testing on orcinus:
* Susan could find no obvious cause for failure of the 20aug17-boom run
* pulled, updated, and did a clean build of SMELTAGRIF on orcinus
* 5x11+1 test run failed w/ a bus error
* hg up -r 1203 to get back to code running on 10apr
* 5x11+1 test run failed w/ XIOS-2 out of memory
* experimented with various PBS directives for 5 node job; still unclear if we can avoid per-processor memory limit of 2000mb
* queued 5x11+3 job; blew up on western boundary same as 10apr
* hg up to tip, and clean build
* another 5x11+3 run blew up on western boundary, same as 10apr
* 55+1 run on 5 nodes failed w/ XIOS-2 out of memory
(SalishSea)

Canyons/Arctic group mtg; see whiteboard.
(Canyons/Arctic)

Created moad_tools package complete w/ docs on readthedocs.
(MOAD)


Sat 14-Apr-2018
^^^^^^^^^^^^^^^

See project work journal.
(GOMSS)


Continued working on nowcast-agrif setup and testing on orcinus with Susan's help:
* 20aug17 SMELTAGRIF w/o agrif won't start
* 20aug17 SMELT blows up
(SalishSea)

See project work journal.
(Resilient-C)


Sun 15-Apr-2018
^^^^^^^^^^^^^^^

Continued working on nowcast-agrif setup and testing on orcinus with Susan's help:
* 19aug17 SMELT init run ended at walltime
* Fixed some namelist issues by changing symlinks in smelt-agrif/ to point to nowcast-green/ instead of v201702/
* another 20aug17 5x11+3 SMELT run blew up on western boundary, same as 10apr
(SalishSea)

See project work journal.
(Resilient-C)


Week 16
-------

Mon 16-Apr-2018
^^^^^^^^^^^^^^^

Continued working on nowcast-agrif setup and testing on orcinus:
* Susan figured out that sshNeahBay/fsct/ files from aug17 have short western boundary; replaced fcst/ symlinks with obs/ ones
* 20aug17 5x11+3 SMELT run got past time step 4...
* 20aug17 5x11+3 SMELTAGRIF run started...
* email to Roman requesting a week of dedicated chassis runs
* queued a 5 node run to see if we get insta-run like for 5x11 runs; reservation is for 2h20 in the future; failed w/ insufficient virutal memory error
* 5x11+3 run w/ 1ts output
* email from Roman confirming that we have an exclusive reservation on a full chassis (pod29?)
(SalishSea)


Tue 17-Apr-2018
^^^^^^^^^^^^^^^

See project work journal.
(Resilient-C)

Continued working on nowcast-agrif setup and testing on orcinus:
* 5 node run did insta-run on pod29, but failed again w/ insufficient virtual memory
* 5x11+3, 30 time step = 20min run w/ 10min output timed out, maybe due to bad XIOS file_def attr values
* tweaked file_def attrs 5x11+3, 30 time steps = 20min run w/ 10min output ran to successful completion!!! on pod28 in 27m37s, including deflation, says it needs more XIOS servers
* 5x11+4-90ts@10min failed w/ insufficient virtual memory error
* 8x18+3-90ts@10min blew up w/ ssh NaN in Haro after 72/144/290 time steps
* discovered that I can ssh to pod nodes and found xios for above run using 3x5.8g on a node where there were also 3 nemo processes using 3x700m
* 12x27+3-90ts@10min had processes on several nodes, blew up same way in Haro
* 8x18+3mem-60ts@10min XIOS memory mode 1.0 factor uses 4.1g per xios, nemo uses 765m each
Salish Sea team mtg; see whiteboard.
Updated SS-run-sets on west.cloud with changesets 0cc9bde28b75:e9a5bc834f46 to bring in reduced bSi and PON sinking rates.
(SalishSea)

AAPS Spring General mtg


Wed 18-Apr-2018
^^^^^^^^^^^^^^^

See project work journal.
(GOMSS)

Email to Elise re: running concurrent nco jobs.
Improved wwatch3 rolling forecast dataset metadata and sent email announcing it.
(SalishSea)

See project journal.
(SalishSeaCast-FVCOM)

See project work journal.
(Resilient-C)


Thu 19-Apr-2018
^^^^^^^^^^^^^^^

See project work journal.
(GOMSS)

Confirmed that restart files generated by nesting tools contain mostly zeros, even for latitudes.
Email to Teresa re: running on cedar and fortran on Mac.
(SalishSea)

See project journal.
(SalishSeaCast-FVCOM)

See project work journal.
(Resilient-C)

Body & Soul session w/ Theresa


Fri 20-Apr-2018
^^^^^^^^^^^^^^^

Fix bug in update_forecast_datasets whereby wwatch3 rolling forecast dataset starts 1 day too late.
Worked on debugging zeros in sub-grid restart files; Baynes Sound looks okay after re-running w/ complete nesting namelist; Haro Strait physics looks okay after namelist fix and symlinking in the coordinates and bathymetry from grid/sub-grids/.
Ran 8x18+3mem SalishSeaAGRIF case; 1/4 day in 40m
Re-built and visualized sub-grid restart files; commands to fix TRBTRA variable issue in Haro Strait:
  ncks -4 -O -v TRNTRA 1_SalishSea_02360880_restart_trc.nc TRNTRA.nc
  ncks -4 -O 1_SalishSea_02360880_restart_trc.nc 1_SalishSea_02360880_restart_trc.nc
  ncrename -4 -O -v TRNTRA,TRBTRA TRNTRA.nc TRBTRA.nc
  ncrename -O -v TRNTRA,TRBTRA TRNTRA.nc TRBTRA.nc
  ncks -4 -A TRBTRA.nc 1_SalishSea_02360880_restart_trc.nc
Started development of watch_NEMO_agrif.
(SalishSea)

Farewell party for Vicky.


Sat 21-Apr-2018
~~~~~~~~~~~~~~~

Started SMELT-AGRIF scaling tests on orcinus:
* See Google Drive spreadsheet https://docs.google.com/spreadsheets/d/12IW0zzyKuZXFl45brVa2aEq5VkFPzmEVI9M25NP1yPk/edit?usp=sharing
* 8x18p+3m; stopped at 1675 time steps because 10h walltime was going to be exceeded
* 9x20p+3m; 8h54m
(SalishSea)

Added observations.get_ndbc.buoy() and places.PLACES to moad_tools.
(MOAD)


Sun 22-Apr-2018
~~~~~~~~~~~~~~~

download_weather 00 failed; re-ran manually to restart automation
Continued SMELT-AGRIF scaling tests on orcinus:
* See Google Drive spreadsheet https://docs.google.com/spreadsheets/d/12IW0zzyKuZXFl45brVa2aEq5VkFPzmEVI9M25NP1yPk/edit?usp=sharing
* 10x23p+3m; 6h40m
* 11x25p+3m; 5h31m
(SalishSea)


Week 17
-------

Mon 23-Apr-2018
~~~~~~~~~~~~~~~

download_weather 06 failed; re-ran manually to restart automation
Continued SMELT-AGRIF scaling tests on orcinus:
* See Google Drive spreadsheet https://docs.google.com/spreadsheets/d/12IW0zzyKuZXFl45brVa2aEq5VkFPzmEVI9M25NP1yPk/edit?usp=sharing
* 12x27p+3m; 4h18m
* 13x29p+3m; 3h42m
* 13x29p+4m; 3h45m
* 13x29p+5m12d; 3h46m
Confirmed that combine and deflate jobs run on a compute node:
* should be able to increase concurrent deflates to 12
* should be possible to run nemo_rebuild concurrently
* deflate seems to the constrained by embedded nccopy that is slow for big files (e.g. 1_*_ptrc_T.nc)
Continued development of watch_NEMO_agrif.
(SalishSea)

Phys Ocgy seminars by Rich's co-op students Forbes (detection of sewage effluent for GVRD via CTD casts) and Rhys (PSF citizen science dataset climatologies)


Tue 24-Apr-2018
~~~~~~~~~~~~~~~

Continued SMELT-AGRIF scaling tests on orcinus:
* See Google Drive spreadsheet https://docs.google.com/spreadsheets/d/12IW0zzyKuZXFl45brVa2aEq5VkFPzmEVI9M25NP1yPk/edit?usp=sharing
* 13x29p+1m12d; 3h37m
* 13x29p+1m-xd; 3h37m
* 13x29p+1m-xd-r2; 3h36m
Salish Sea team mtg; see whiteboard.
Discussed environments and multi-process Python on cedar w/ Elise & Ben.
Finished development of watch_NEMO_agrif.
make_turbidity_file ValueError caused automation to stop before upload_forcing turbidity; re-ran upload_forcing turbidity manually to restart automation for nowcast-green
Updated tracers on west.cloud from 57c3f17aa17a with 3aae9bae4eef:c9808b098359 re: Elise's PON and DON based on model-derived profiles,
Updated tracers on skookum from b8f0f2dd2425 with xxx re: Elise's PON and DON based on model-derived profiles,
Updated project/SalishSea/hindcast-sys/tracers on cedar from 57c3f17aa17a with 3aae9bae4eef:c9808b098359 re: Elise's PON and DON based on model-derived profiles,
Updated nowcast-agrif-sys/tracers on orcinus from 57c3f17aa17a with 3aae9bae4eef:c9808b098359 re: Elise's PON and DON based on model-derived profiles,
(SalishSea)

Attended Digital Tech Supercluster info mtg lead by Gail Murphy.


Wed 25-Apr-2018
~~~~~~~~~~~~~~~

get_onc_ferry failed w/ UnboundLocalError on nav_data
Continued SMELT-AGRIF scaling tests on orcinus:
* See Google Drive spreadsheet https://docs.google.com/spreadsheets/d/12IW0zzyKuZXFl45brVa2aEq5VkFPzmEVI9M25NP1yPk/edit?usp=sharing
* 13x29p+1.475m-xd; 3h37m
(SalishSea)

See project journal.
(SalishSeaCast-FVCOM)

See project work journal.
(GOMSS)


Thu 26-Apr-2018
~~~~~~~~~~~~~~~

Network issues caused early morning nowcast trouble:
* no nav data from TWDP ferry raised UnboundLocalError again; fixed bug via issue#52
* connection failures to water levels service; manually re-ran make_plots forecast2 to restart automation
(SalishSea)

Worked on parents' taxes and mail redirection.

See project journal.
(SalishSeaCast-FVCOM)

Body & Soul session w/ Theresa.

Saw World Without Us at The Cultch.


Fri 27-Apr-2018
~~~~~~~~~~~~~~~

1st monthly project mtg.
(MIDOSS)

Group mtg; see whiteboard.
(Canyons/Arctic)

See project journal.
(SalishSeaCast-FVCOM)

Wrote email to Tom Prime at UK NOC Liverpool comparing and contrasting the GoMSS and SalishSea system.
Updated skookum:SS-run-sets from 9961fd75186d with e52638f8b65c:815d84f23428 to bring in Elise's plankton growth temperature dependence parameter changes.
Updated west.cloud:SS-run-sets from 67b1a35765a0 with 27bc9c4c0c86:815d84f23428 to bring in Elise's plankton growth temperature dependence parameter changes.
Updated cedar:SS-run-sets from 0cc9bde28b75 to 815d84f23428.
Updated orcinus:SS-run-sets from 3e64fad9e3bb with 937ff95ba1e7:815d84f23428 to bring in Elise's plankton growth temperature dependence parameter changes.
Started development of run_NEMO_agrif worker.
(SalishSea)


Sat 28-Apr-2018
~~~~~~~~~~~~~~~

Resolved manager crash after download_fvcom_results and added a temporary hack to prevent make_plot fvcom forecast publish from launching.
(SalishSea)

Completed income taxes to the review stage.

Saw Circa: Opus at the Chan.


Sun 29-Apr-2018
~~~~~~~~~~~~~~~

See project work journal.
(GOMSS)


May
===

Week 18
-------

Mon 30-Apr-2018
^^^^^^^^^^^^^^^

Continued development of run_NEMO_agrif worker.
Helped Tereza get sorted out on cedar.
(SalishSea)


Tue 1-May-2018
^^^^^^^^^^^^^^^

See project work journal.
(GOMSS)

Salish Sea group mtg; see whiteboard.
Continued development of run_NEMO_agrif worker; successfully launched a run (that failed due to lack of forcing...)
(SalishSea)


Wed 2-May-2018
^^^^^^^^^^^^^^

Deployed make_plots wwatch3 to skookum.
(SalishSea)

See project journal.
(SalishSeaCast-FVCOM)

See project journal.
(Resilient-C)


Thu 3-May-2018
^^^^^^^^^^^^^^

Vancouver to Barrie

Worked on refactoring [run|watch]_NEMO_agrif workers to use paramiko.ssh_client.exec_command().
(SalishSea)


Fri 4-May-2018
^^^^^^^^^^^^^^

Visiting parents and business w/ Kate and Horst in Barrie; Susan arrived in evening after exciting landing and shuttle trip thanks to wind storm.


Sat 5-May-2018
^^^^^^^^^^^^^^

upload_forcing forecast2 to orcinus failed due(?) to grib2netcdf/LiveOcean race condition; no consequences.
(SalishSea)

Visiting parents and business w/ Rebecca in Barrie.


Sun 6-May-2018
^^^^^^^^^^^^^^

upload_forcing forecast2 to west.cloud failed due(?) to grib2netcdf/LiveOcean race condition; re-ran manually to restart automation.
Created nowcast.ssh_sftp.ssh_exec_command() to do in-process remote commands via paramiko connection w/ subprocess.run()-like API.
Worked on refactoring [run|watch]_NEMO_[agrif|hindcast] workers to use ssh_exec_command().
(SalishSea)

Visiting parents in Barrie.


Week 19
-------

Mon 7-May-2018
^^^^^^^^^^^^^^

upload_forcing forecast2 to west.cloud failed due(?) to grib2netcdf/LiveOcean race condition; re-ran manually to restart automation.
download_weather 12 failed; re-ran manually to restart automation at ~12:30.
Worked on refactoring [run|watch]_NEMO_[agrif|hindcast] workers to use ssh_exec_command().
(SalishSea)

Barrie to Vancouver


Tue 8-May-2018
^^^^^^^^^^^^^^

See project work journal.
(GOMSS)

Finished refactoring [run|watch]_NEMO_[agrif|hindcast] workers to use ssh_exec_command().
Salish Sea group mtg; see whiteboard.
Helped Elise understand big nco ops on cedar node.
After a lot of thrashing, got 21aug17 nowcast-agrif run going via run_NEMO_agrif worker; **have to remember that old sshNeahBay/fcst/ files do not have long enough western boundary arrays**.
Started writing orcinus deployment docs.
(SalishSea)

Helped Saurav with conda env for mayavi.
(Canyons)


Wed 9-May-2018
^^^^^^^^^^^^^^

Discovered that salishsea combine failed for nowcast-agrif/21aug17, but gather worked; manually ran salishsea combine in results directory; no phsyics restarts for sub-grids, tracer restarts fail due to netCDF attr error; sigh...
Tried to run nowcast-agrif automation:
* upload_forcing turbidity to orcinus didn't happen; ran manually
* run_NEMO launch failed due to missing host_config['envvars']
Created issue #53 re: apparent race condition between ping_erddap and make_plots wwatch3 forecast*; the possible fix of launching make_plots after ping_erddap doesn't work because ping_erddap doesn't provide the run type.
(SalishSea)

See project work journal.
(GOMSS)

See project journal.
(SalishSeaCast-FVCOM)

See project journal.
(Resilient-C)


Thu 10-May-2018
^^^^^^^^^^^^^^^

See project journal.
(SalishSeaCast-FVCOM)

See project work journal.
(GOMSS)

Body & Soul session w/ Theresa.


Fri 11-May-2018
^^^^^^^^^^^^^^^

See project journal.
(Resilient-C)

Continued working on nowcast-agrif automation.
(SalishSea)


Sat 12-May-2018
^^^^^^^^^^^^^^^

Filed income tax returns.

Met w/ Brian re: repairs to fence between back yards.

Continued working on nowcast-agrif automation.
(SalishSea)


Sun 13-May-2018
^^^^^^^^^^^^^^^

Continued working on nowcast-agrif automation.
Started working on nowcast-agrif production; todo:
* sub-grid restart files
* sub-grid rivers_bio_tracers_*.nc files
(SalishSea)


Week 20
-------

Mon 14-May-2018
^^^^^^^^^^^^^^^

Continued working on nowcast-agrif production:
* did clean build of nesting tools on salish
* ran nesting tools to generate (for both sub-grids):
  * coordinates
  * restart files
  * river bio tracer daily files
* launched 13may18 run and it is working; failed w/ -ve SSS in Haro on timestep 1925
* used ncra to produce river bio tracer mean file:
    /bin/ls | grep rivers_bio_tracers_'m..d..'.nc | ncra -4 -o rivers_bio_tracers_mean.nc
Phys Ocgy seminar by Sam re: his work on Atlantic mode water, and on Arduino-based LIAM wave measurement device that rides ODL drifter.
(SalishSea)

See work journal.
(SalishSeaCast-FVCOM)

See project journal.
(Resilient-C)


Tue 15-May-2018
^^^^^^^^^^^^^^^

Many UBC central IT services down, including wifi and matlab license server.

download_weather 06 failed; re-ran manually to restart automation at ~08:40.
make_plots wwatch3 forecast2 publish failed; re-ran manually.
make_live_ocean_files failed due to Matlab license server down
run_NEMO_agrif ran for the 1st time in automation; failed due to no 14aug18 run dir.
SalishSeaCast team mtg w/ visitor from UofA; see whiteboard.
Queued nowcast-agrif/13may18 21h run on orcinus; finished successfully.
Pushed and deployed code that should run make_plots wwatch3 after ping_erddap instead of concurrently; fixes issue #53.
Ordered 2x8Tb desktop drives for Elise.
(SalishSea)


Wed 16-May-2018
^^^^^^^^^^^^^^^

Attended day 1 of MEOPAR Climate Change and Marine Transportation expert forum.

Continued work on trying to get nowcast-agrif productions started:
* Decided to try 16may18 because it is present, and NW wind blowing fresh water south into Haro Strait sub-grid has abated compared to 13may18
* created restart etc. files for 15may18 and tried run for 16may18; failed after 10 time steps with NaN ssh
* rolled back to trying 13may18 after Susan pointed out that 16may18 is approaching peak of spring/neap tide cycle
* tried to run 13may18 w/ 5s time step for Haro Strait, but forgot to change time step factor in AGRIF file
2x8Tb desktop drives for Elise delivered.
(SalishSea)


Thu 17-May-2018
^^^^^^^^^^^^^^^

Decide to skip day 2 of MEOPAR forum.

Continued work on trying to get nowcast-agrif productions started:
* Susan realized that AGRIF.in time step factor needs to be changed too for 5s Haro sub-grid; 5s won't work because NEMO time step must be an even integer; 13may18 run w/ 8s time step failed in 22nd hour, same as 10s time step; Susan send email to Michael asking for ideas.
Charles updated ERDDAP to v1.82.
(SalishSea)

Body & Soul session w/ Theresa.


Fri 18-May-2018
^^^^^^^^^^^^^^^

Ran make_plots nemo forecast publish that failed yesterday due to ERDDAP down for upgrade.
Launch nowcast-agrif/13may18 w/ 4s time step in Haro to reduce vertical advection per Michael's recommendation; failed w/ -ve SSS.
Reviewed Susan's sample near surface velocity dataset; very sad panda, but she is working on it.
Worked on ERDDAP:
* Updated and buffed /opt/tomcat/content/erddap/setup.xml.
* Experimented with adding testOutOfDate dataset attributes.
* Experimented with files dataset interface for VHFR FVCOM results:
  * /opt/tomcat/webapps/erddap/WEB-INF/GenerateDatasetsXml.sh EDDTableFromFileNames /opp/fvcom/ .*vhfr_low_v2_[0s].*\.nc$ true 10080 "" "" "" ""
Susan decided that we should remove the Haro Strait sub-grid from nowcast-agrif and hope to get production running with just Baynes Sound.
(SalishSea)


Sat 19-May-2018
^^^^^^^^^^^^^^^

orcinus had lustre file system issue all day long, so upload_forcing for nowcast-agrif failed twice.
(SalishSea)

Removed clematis, honey suckle & chocolate vine from fences, as well as their trellises. Cut down cedar shrub near house. Met new neighbour Shan and told her to go ahead with limbing cedars over fence at back of yard.


Sun 20-May-2018
^^^^^^^^^^^^^^^

make_plots wwatch3 forecast2 failed due to no dataset; so the race condition with ping_erddap is unresolved; re-opened issue#53.
(SalishSea)

See work journal.
(GOMSS)


Week 21
-------

Mon 21-May-2018
^^^^^^^^^^^^^^^

**Statutory Holiday** - Victoria Day

Formatted 2x8Tb drives for Elise /data near-line storage as elise1 and elise2 via gparted.
Started trying to run nowcast-agrif on orcinus w/ only Baynes Sound sub-grid:
* disabled automation make_forcing_links
* created AGRIF.in file w/ 1 sub-grid
* created iodef.xml file w/ 1 sub-grid
* created YAMl file w/ 1 sub-grid
* 9387484.orca2.ibb succeeded
Updated run_NEMO_agrif worker to handle only Baynes Sound sub-grid.
Updated SS-run-sets re: nowcast-agrif with only Baynes Sound sub-grid.
Updated namelist.atmos_rivers to eliminate need for no_snow and weights file links in NEMO_atmos/ forcing dir.
Fixed bug in run_NEMO_agrif re: putting tmp run dir and job id in checklist when there are uncommitted files messages.
Ran nowcast-agrif:
* 13may18
* 14may18
* 15may18
* 16may18
Changed subgrids/*/namelist_smelt_cfg.* to use rivers-climatology/bio/rivers_bio_tracers_mean.nc.
Continued running nowcast-agrif:
* 17may18
* 18may18
* 19may18
* 20may18
(SalishSea)

See work journal.
(GOMSS)


Tue 22-May-2018
^^^^^^^^^^^^^^^

Continued running nowcast-agrif:
* 21may18
Changed config so that today's nowcast-agrif should launch automatically.
Updated namelist.atmos_rivers to eliminate need for rivers climatology file links in rivers/ forcing dir.
nowcast-agrif/22may18 almost ran fully automated.
Salish Sea team mtg; see whiteboard.
Talked to Elise about confusing motd on cedar re: 48-core nodes and whole-node jobs.
(SalishSea)

Installed Signal desktop on niko.

Spinning at Method w/ Lauren


Wed 23-May-2018
^^^^^^^^^^^^^^^

Investigated 48-core nodes and whole-node jobs on cedar based on email that Elise got form support@; replied to Elise.
Helped Tereza w/ her plotting from script issue.
make_plots wwatch3 failed for both runs; manual re-runs also failed due to SSL error.
(SalishSea)


See work journal.
(GOMSS)

See work journal.
(Resilient-C)


Thu 24-May-2018
^^^^^^^^^^^^^^^

See work journal.
(Resilient-C)

See work journal.
(GOMSS)

See work journal.
(SalishSeaCast-FVCOM)

make_plots wwatch3 forecast2 failed again due to SSL error.
Emailed Idalia re: re-installing anaconda, and using a conda env for gsw.
Diagnosed make_plots wwatch3 SSL issue as being due to an SSL config issue on ndbc.noaa.gov; added work-around to moad_tools.observations.
(SalishSea)

Body & Soul session w/ Theresa.


Fri 25-May-2018
^^^^^^^^^^^^^^^

Monthly project mtg.
* Set up contact between Leni and Matthias Herborg via Micahel; sent email
* get MOHID running on salish
(MIDOSS)

Canyons/Arctic mtg; see whiteboard.
Helped Idalia get a gsw conda env set up.
(Canyons/Arctic)

Post-agrif launch cleanup.
make_plots wwatch3 failed for both runs; re-ran forecast manually; made another try at fixing issue #53 by adding retry decorator to fig module _get_wwatch3_fields() that downloads fields from ERDDAP.
Started playing with visualization of Baynes Sound AGRIF results.
(SalishSea)


Sat 26-May-2018
^^^^^^^^^^^^^^^

See work journal.
(Resilient-C)

Started outlining CMOS talk.
(SalishSea)


Sun 27-May-2018
^^^^^^^^^^^^^^^

See work journal.
(GOMSS)


Week 22
-------

Mon 28-May-2018
^^^^^^^^^^^^^^^

See work journal.
(GOMSS)

Got Elise set up with 2x*Tb drives.
Discussed use of orcinus reservation w/ Roman and Elise.
Added provisional VHFR FVCOM files dataset to ERDDAP.
Continued working on visualization of Baynes Sound AGRIF results.
(SalishSea)

See work journal.
(SalishSeaCast-FVCOM)


Tue 29-May-2018
^^^^^^^^^^^^^^^

See work journal.
(Resilient-C)

Continued working on visualization of Baynes Sound AGRIF results.
Salish Sea team mtg; see whiteboard.
Discussed XIOS on-the-fly deflation w/ Tereza; need to change salishsea run to default to deflation.
Worked w/ Susan to develop outline of CMOS talk and started creating slides.
(SalishSea)


Wed 30-May-2018
^^^^^^^^^^^^^^^

Talked to Aunt Elinor and Isobel.

See work journal.
(GOMSS)

See work journal.
(Resilient-C)


Thu 31-May-2018
~~~~~~~~~~~~~~~

See work journal.
(Resilient-C)

Body & Soul session w/ Theresa.

See work journal.
(GOMSS)


Fri 1-Jun-2018
~~~~~~~~~~~~~~

See work journal.
(Resilient-C)

Continued work on slides for CMOS talk.
nowcast-agrif run failed due to a power bump; re-ran manually.
(SalishSea)

See work journal.
(GOMSS)


Sat 2-Jun-2018
~~~~~~~~~~~~~~

Got Carib ready for Nova Scotia tour.


Sun 3-Jun-2018
~~~~~~~~~~~~~~

Worked on prep for Nova Scotia trip.


June
====

Week 23
-------

Mon 4-Jun-2018
~~~~~~~~~~~~~~

Early morning phone call from Uncle John.
Email to Jamie.
Long conversation w/ Mom's doctor of the week, Kevin Ali.
Telcon w/ Aunt Elinor.

Timesheets for June.

Released SalishSeaCmd v3.4 re: --deflate, no more bugaboo, no more NEMO-3.4, and rrg-allen default account on cedar.
Continued work on slides for CMOS talk.
(SalishSea)


Tue 5-Jun-2018
~~~~~~~~~~~~~~

See work journal.
(GOMSS)

Continued work on slides for CMOS talk.
Salish Sea team mtg; see whiteboard.
(SalishSea)

See work journal.
(Resilient-C)


Thu 7-Jun-2018
~~~~~~~~~~~~~~

Vancouver to Barrie

Fixed issue#54 bug in watch_NEMO_agrif so that end-of-run disappearance of job from queue on orcinus does not generate a bogus ERROR level logging message.
Started exposing functions in nemo-cmd.prepare for use by SalishSeaCmd and other packages that may extend NEMO-Cmd.
(SalishSea)


Fri 8-Jun-2018
~~~~~~~~~~~~~~

Discovered that nowcast-green/06jun18 failed; helped Susan through getting it re-running.
Removed --no-deflate command-line option from salishsea run command in watch_NEMO_agrif and watch_NEMO_hindcast.
(SalishSea)

See work journal.
(GOMSS)


Sat 9-Jun-2018
~~~~~~~~~~~~~~

Disabled orcinus-nowcast-agrif host re: orcinus maintenance downtime.
nowcast run failed due to no 08jun18/namelist_cfg
(SalishSea)

Barrie to Halifax


Sun 10-Jun-2018
~~~~~~~~~~~~~~~

Peggy's Cove photo tour

CMOS Congress

Ocean modeling community of practice meeting.
CMOS ice breaker
Dinner w/ Mitchell, Susan Haig, Dave Greenberg


Week 24
-------

Mon 11-Jun-2018
~~~~~~~~~~~~~~~

CMOS Congress

Breakfast w/ Neil Swart

Backfilling nowcast & forecast runs to generate FVCOM_*.nc files:
* make_forcing_links nowcast+ 2018-06-07 to launch nowcast/07jun18
* upload_forcing nowcast+ 2018-06-07 --debug
* make_forcing_links nowcast+ 2018-06-07 --debug
* make_forcing_links ssh 2018-06-07 to launch forecast/07jun18
* make_forcing_links nowcast+ 2018-06-08 to launch nowcast/08jun18
* upload_forcing nowcast+ 2018-06-08 --debug
* make_forcing_links nowcast+ 2018-06-08 --debug
* make_forcing_links ssh 2018-06-08 to launch forecast/08jun18
Added Halfmoon Bay and Squamish tide gauge stations to default v201702 file_def.xml.
Added VHFR FVCOM boundary regions to new dedicated v201702 file_def_green.xml.
Continued work on slides for CMOS talk.
(SalishSea)

See work journal.
(SalishSeaCast-FVCOM)


Tue 12-Jun-2018
~~~~~~~~~~~~~~~

CMOS Congress

See work journal.
(SalishSeaCast-FVCOM)

forecast2 failed due to bad run date from backfilling in checklist:
* edited nowcast_checklist.yaml
* restarted manager
* re-ran make_forcing_links forecast2 to restart automation
Finished backfilling nowcast & forecast runs to generate FVCOM_*.nc files:
* edited nowcast_checklist.yaml
* restarted manager
* upload_forcing nowcast+ 2018-06-10 --debug
* make_forcing_links nowcast+ 2018-06-10 --debug
* make_forcing_links ssh 2018-06-10 to launch forecast/10jun18
(SalishSea)

Mom passed away.


Wed 13-Jun-2018
~~~~~~~~~~~~~~~

CMOS Congress

See work journal.
(GOMSS)

Finished slides for CMOS talk.
(SalishSea)


Thu 14-Jun-2018
~~~~~~~~~~~~~~~

CMOS Congress
Presented SalishSeaCast in coupled models session.

See work journal.
(GOMSS)

Halifax to Toronto

Continued exposing functions in nemo_cmd.prepare for use by SalishSeaCmd and other packages that may extend NEMO-Cmd.
(SalishSea)

Added VHFR FVCOM results page to nav.
Updated SS-run-sets on skookum to pull in Susan's change to use west boundary sea surface height at north boundary too, initially in nowcast-dev.
(salishsea-site)


Fri 15-Jun-2018
~~~~~~~~~~~~~~~

Toronto to Barrie

orcinus came back into operation
(SalishSea)


Sat 16-Jun-2018
~~~~~~~~~~~~~~~

make_runoff_file failed because downloads from wateroffice on salish failed:
* re-tried ecget river flow and it is still failing
* manually persisted 14jun values to 15jun for Fraser and Englishman
* manually re-ran make_runoff_file to restart automation
Backfilling nowcast-agrif on orcinus:
* 07jun18 got hammered by automation make_forcing_links
(SalishSea)


Sun 17-Jun-2018
~~~~~~~~~~~~~~~

Backfilling nowcast-agrif on orcinus:
* 07jun18
* 08jun18
* 09jun18
* 10jun18
* 11jun18
Simplified nowcast run dirs symlinks (similar to what we have for hindcast and nowcast-agrif) by:
* adding links to grid and rivers-climatology repo clones
* changing nowcast-green/namelist.atmos_rivers and namelist_smelt_cfg
* changing smelt-agrif/namelist_smelt_cfg
* removing from make_forcing_links creation of no_snow.nc, weights, rivers constant temperature, rivers monthly climatology, river bio-tracers dir
Discovered that ECget scraping of Fraser River water quality buoy is broken due to a pointless span element id attribute change on the web page; fixed.
(SalishSea)


Week 25
-------

Mon 18-Jun-2018
~~~~~~~~~~~~~~~

Backfilling nowcast-agrif on orcinus:
* 12jun18
* 13jun18
* 14jun18
* 15jun18
make_forcing_links turbidity failed again with a FileNotFoundError, then a FileExistsError, and that scuttles nowcast-green and nowcast-dev (didn't notice dev yesterday); recovery:
* upload_forcing turbidity west.cloud
* mkdir nowcast-dev/17jun18
* cp nowcast-green/17jun18 nowcast-dev/17jun18
* make_forcing_links nowcast+ salish --shared-storage
Pulled Susan's nowcast namelist changeset 6b89d1af1aec to use western boundary ssh at norther boundary in production on skookum/salish, west.cloud, orcinus, and cedar.
(SalishSea)


Tue 19-Jun-2018
~~~~~~~~~~~~~~~

Backfilling nowcast-agrif on orcinus:
* 16jun18
* 17jun18
* 18jun18
Restored automation in time for nowcast-agrif/19jun18 to run normally.
Explored ideas for enabling run_hindcast to operate for an arbitrary number of days <1 month.
(SalishSea)


Wed 20-Jun-2018
~~~~~~~~~~~~~~~

watch_ww3 forecast2 failed due to unavailable port; restart automation with download_wwatch3_results.
(SalishSea)


Sun 24-Jun-2018
~~~~~~~~~~~~~~~

Discovered that watch_ww3 has been failing due to no port available on west.cloud since 20-Jun:
* download_wwatch3_results forecast 18-23
* download_wwatch3_results forecast2 19-24
(SalishSea)


Week 26
-------

Mon 25-Jun-2018
~~~~~~~~~~~~~~~

Changed download_weather 12 schedule from 10:30 to 11:30 in anticipation of 26jun west.cloud network maintenance that may disrupt active use of shared storage.
(SalishSea)


Tue 26-Jun-2018
~~~~~~~~~~~~~~~

Barrie to Vancouver

Finished exposing functions in nemo_cmd.prepare for use by SalishSeaCmd and other packages that may extend NEMO-Cmd.
(SalishSea)


Wed 27-Jun-2018
~~~~~~~~~~~~~~~

Changed download_weather 12 schedule back to 10:30.
Answered email from Sandrine Edouard @MSC re: our use of HRDPS.
Pulled NEMO-Cmd and SalishSeaCmd refactoring on to oricnus to test via nowcast-agrif.
Explored cartopy; can use RotatedPole project to get a map of SoG with vertical "axis" and lat/lon grid lines, but no labels.
(SalishSea)

See work journal.
(GOMSS)


Thu 28-Jun-2018
~~~~~~~~~~~~~~~

More messing w/ cartopy using the land and coast from bathymetry technique that Ben uses with basemap, but can't get rotation and would still have to add a bunch of gist code to get lat/lon labels.
(SalishSea)

See work journal.
(GOMSS)


Fri 29-Jun-2018
~~~~~~~~~~~~~~~

See work journal.
(GOMSS)

Continued development of Baynes Sound AGRIF surface fields figure module.
Fixed bug in NEMO-Cmd re: land processor elimination that crept in during refactoring.
(SalishSea)

Planned 7-12 July trip to move Dad into Amica.


Sat 30-Jun-2018
~~~~~~~~~~~~~~~

Vancouver to Parksville

(SalishSea)


Sun 1-Jul-2018
~~~~~~~~~~~~~~

Built and installed Mercurial from clone of hg-stable repo on niko.
(SalishSea)


Week 27
-------

Mon 2-Jul-2018
~~~~~~~~~~~~~~~

Started changing Arrow.replace() to Arrow.shift() where appropriate; improved semantics.
(SalishSea)

Parksville to Vancouver


Tue 3-Jul-2018
~~~~~~~~~~~~~~~

Finished changing Arrow.replace() to Arrow.shift() where appropriate; improved semantics.
Salish Sea team mtg; see whiteboard.
Fixed failing unit tests in SalishSeaNowcast re: out of date OPPTools and NEMO-Cmd/SalishSeaCmd refactoring.
Updated NEMO-Cmd, SalishSeaCmd, and SalishSeaNowcast on cedar, skookum, and west.cloud re: NEMO-Cmd and SalishSeaCmd refactoring.
(SalishSea)

Started generating /opp/wwatch3/nowcast/ddmmmyy/ directories from forecast/ dirs.
Added ubcSSWaveWatch3-SoGFilesV17-02 files dataset to ERDDAP.
(SoG waves)

Upgraded kudu to Pop!_OS 18.04 via `sudo do-release-upgrade`.

Built and installed Mercurial from clone of hg-stable repo on kudu.


Wed 4-Jul-2018
~~~~~~~~~~~~~~~

Researched, installed and tested borgbackup package:
* borg init --encryption=repokey-blake2 /media/doug/kudu_backup/borg-kudu
* export BORG_PASSPHRASE
* export BORG_REPO=/media/doug/kudu_backup/borg-kudu
* borg create --list --stats --compression=lz4 ::kudu-{now} $HOME --exclude '/home/doug/.dbus' --exclude 'home/doug/Downloads/' --exclude '/home/doug/.vagrant.d/' --exclude '/home/doug/.cache/' --exclude '/home/doug/snap/' --exclude '/home/doug/.PyCharm*/system/'
* borg create --list --stats --compression=lz4 ::kudu-{now} $HOME /media/doug/warehouse --exclude '/home/doug/.dbus' --exclude 'home/doug/Downloads/' --exclude '/home/doug/.vagrant.d/' --exclude '/home/doug/.cache/' --exclude '/home/doug/snap/' --exclude '/home/doug/.PyCharm*/system/' --exclude '/media/doug/warehouse/Downloads/'  --exclude '/media/doug/warehouse/conda_envs/'  --exclude '/media/doug/warehouse/VirtualBoxVMs/'  --exclude '/media/doug/warehouse/Mailpile/'  --exclude '/media/doug/warehouse/vidyo'  --exclude '/media/doug/warehouse/.Trash-1000'  --exclude '/media/doug/warehouse/lost+found'  --exclude '/media/doug/warehouse/minconda3/'

Continued generating /opp/wwatch3/nowcast/ddmmmyy/ directories from forecast/ dirs.
(SoG waves)


Thu 5-Jul-2018
~~~~~~~~~~~~~~~

Body & Soul session w/ Theresa

Sent email to Rich re: availability of ubcSSWaveWatch3-SoGFilesV17-02 files dataset on ERDDAP.
Continued generating /opp/wwatch3/nowcast/ddmmmyy/ directories from forecast/ dirs.
(SoG waves)


Fri 6-Jul-2018
~~~~~~~~~~~~~~~

Finished generating /opp/wwatch3/nowcast/ddmmmyy/ directories from forecast/ dirs.
(SoG waves)

Worked w/ Susan on getting next iteration of hindcast running on cedar, and testing watch_NEMO_hindcast run success checking code.
Susan found issues w/ running on skylake nodes; if 32 cores, jobs run slow due to competition; if 48 cores jobs fail to start.
Updates on cedar:
* grid from 2298a95bf000 to 77e9cce1dcd6
* NEMO-3.6-code from c8684a10b28e to 5d5d5c95cd8b
* SS-run-sets from f7eb987b308b to a86be84a6915
* tracers from c9808b098359 to 3c6019a2e7ea
Clean build of NEMO SMELT config on cedar.
Added run id option to watch_NEMO_hindcast worker.
Improved unit test coverage of watch_NEMO_hindcast.
(SalishSea)


Sat 7-Jul-2018
~~~~~~~~~~~~~~~

Updated SS-run-sets on cedar from a86be84a6915 to e3f898810547.
Worked on adding --cedar-broadwell option to SalishSeaCmd:
* default cedar to 48 tasks per node with skylake constraint
* option make cedar use 32 tasks per node w/ broadwell constraint
Fixed bugs in watch_NEMO_hindcast and hindcast YAML template file while working with Susan to get hindcast running.
(SalishSea)

Vancouver to Toronto


Sun 8-Jul-2018
~~~~~~~~~~~~~~~

Continued work on adding --cedar-broadwell option to SalishSeaCmd.
Investigated Susan's results directory not created issue on cedar; probably out of sync installation of SalishSeaCmd.
(SalishSea)


Week 28
-------

Mon 9-Jul-2018
^^^^^^^^^^^^^^

Worked w/ Scott to move Dad's furniture to Amica.


Tue 10-Jul-2018
^^^^^^^^^^^^^^^

Dad moved to Amica via RNR transport.
Finished unpacking boxes for Dad.


Wed 11-Jul-2018
^^^^^^^^^^^^^^^

Helped Dad settle in.

Manually ran run_NEMO_hindcast to queue sep15-dec15 runs.
(SalishSea)


Thu 12-Jul-2018
^^^^^^^^^^^^^^^

01sep15 hindcasst run failed during combine due to a bad local installation of SalishSeaCmd on cedar; fix installation and manually ran combine and gather.
Cleaned up failed oct15-dec15 run dirs.
Manually ran run_NEMO_hindcast to queue oct15-dec15 runs, and watch_NEMO_hindcast to start watching.
Manually ran download_results for sep15 run to restart download/split automation.
Added launch of run_NEMO_hindcast after successful completion of watch_NEMO_hindcast so that hindcast runs queue is kept loaded until month-just-finished is queued.
(SalishSea)


Fri 13-Jul-2018
^^^^^^^^^^^^^^^
Westgrid townhall:
* Federated Research Data Repository Project (FRDR):
  * Lee Wilson
  * https://www.frdr.ca/repo/
  * Uses Globus file transfer
  * alternative to institution or domain-specific archive platforms
  * Archivematica
* RAC 2019 Updates and Preparation:
  * Guides late-Aug
  * Fast Track 25-Oct
  * RRG & RPP 8-Nov
  * RPP Progress Reports 10-Jan
  * expect similar success rates as past few years
    * performance estimates
    * storage usage & estimates
    * cloud usage & estimates
    * nearline storage estimates (not available yet, still)
  * GP4 (Béluga) ordered; ~30k cores +GPUs (similar to Graham)
  * Orcinus to be defunded 31-Mar-2019
* A look at the new Arbutus and Cedar expansion:
  * cedar is now 60656 cores (640 skylake 48 core nodes w/ 187G/node), 5.2Pflops peak compute
  * cedar GPU usage is increasing; expansion didn't include new GPUs
  * outages
    * arbutus 22-Jul network 10-30 minutes between 06:00 and 10:00
    * graham 21-24-Aug
    * cedar 4 days late-Aug; OS update to CentOS-7.5; related Lustre & Omnipath upgrades
    * orcinus 2 days on 25-Aug
    * arbutus September for expansion
  * Arbutus expansion (Ryan Enge):
    * moving to OpenStack Queens release w/ CI
    * adding ~1400 skylake compute cores & ~3.5PB storage
    * high availability for clients
    * improved monitoring & alerting
    * improved HPC performance
    * https://arbutus.cloud.computecanada.ca
    * migration will be required; wiki docs Arbutus_West_Cloud_Migration
    * cloud user survey coming soon
* Results & feedback from recent user surveys:
  * Erin Trifunov
  * see slides: https://www.westgrid.ca/files/July%202018%20WG%20Town%20Hall%20.pdf
  * westgrid users w/ RAC allocations are least satisfied with computecanada
  * UBC has highest lab to market collaboration level
* summer school materials are now online: https://westgrid.github.io/trainingMaterials/
* Masao has retired; got career achievement award
* Kamil got team choice award

Discussed hindcast issues w/ Susan:
* running 31 day months; fix and restart from 01sep15; fixed
* split_results is fragile:
  * using wrong date; maybe from checklist?; fixed
  * dies if there are unexpected file patterns; e.g. output.abort.nc
hindcast:
* tested salishsea run mods for skylake on cedar
* queued 01sep15 via PyCharm debugger run
* queued 01oct15 via skookum
* download_results 01sep15 launched via automation
* run_NEMO_hindcast ran via automation, but queued another 01oct15 run instead of 01nov15, probably because 01sep15 was still on queue in completed state
Improved download_results message payload to include run date so that follow-on workers (especially split_results) are correctly chained.
Changed split_results to use f-strings.
Fixed bug in run_NEMO_hindcast re: finding previous run queue info when a run as just finished and is still on the queue in COMPLET* state.
(SalishSea)

Worked with Ben & Elise to delete Vicky's files that we don't need any longer to free up space on /data/.

Emailed Charles about borg vs. rdiff-backup.

Canyons/Arctic mtg; see whiteboard.
(Canyons/Arctic)


Sat 14-Jul-2018
~~~~~~~~~~~~~~~

Lower back pain that started Friday was much worse, though lying on my front on the floor seemed to relieve it by evening.

Upgraded niko to Pop!_OS 18.04 via `sudo do-release-upgrade`.

Finished hindcast runs to end of jan16.
(SalishSea)

See work journal.
(GOMSS)


Sun 15-Jul-2018
~~~~~~~~~~~~~~~

Really bad lower back pain in the night, more time on the floor in the morning relieved it for a while.

Updated repos in nowcast-sys on skookum:
* moad_tools: a80c338e7956 to 577b16c939fc
* SalishSeaNowcast: d14aa61e677e to 44bda01719fe
* SS-run-sets: e3f898810547 to de290c84ebc1
* tides: cce641a99390 to 9e87d9f7087a
* tools: d0a1d289ff62 to e7646d07561c
Started tmux session on salish calculating LiveOcean boundary files from 2013-01-02 re: Susan's addition of O2, DIC & TAlk, and update of NO3-Si correlation coefficients from Elise.
* started 2013 at 10:51, finished at 14:05
* started 2014-2017 at 15:15, finished at 05:10
Started work on enabling upload_forcing to keep cedar forcing files collections updated daily.
(SalishSea)


Week 29
-------

Mon 16-Jul-2018
^^^^^^^^^^^^^^^

Finished tmux session on salish calculating LiveOcean boundary files from 2013-01-02 re: Susan's addition of O2, DIC & TAlk, and update of NO3-Si correlation coefficients from Elise.
* started 2018 jan-jun at 08:00, finished at 09:40
* started 2018 jul 1-15 at 10:20, finished at 10:35
* rsync-ed updated collection to cedar:/project/6001313/SalishSea/forcing/LiveOcean/ and orcinus:/home/sallen/MEOPAR/LiveOcean/
Tested upload_forcing cedar-hindcast via scp to skookum.
(SalishSea)

Created https://bitbucket.org/midoss/ team on bitbucket.
Created midoss account on readthedocs.org with email dlatorne@eoas.ubc.ca.
Created midoss/docs repo and started writing docs.
(MIDOSS)


Tue 17-Jul-2018
^^^^^^^^^^^^^^^

Traced recent Fraser River water quality buoy data scraping issue to the fact that a 404 page is being sent with a 200 status code :-()
(ECget)

Added link checking section to MODA docs.
(MOAD)

Salish Sea team mtg; see whiteboard.
Confirmed that upload_forcing cedar-hindcast works.
Continued working on baynes_sound_agrif figure module dev notebook.
(SalishSea)

Worked w/ Ben to build MOHID on salish:
* project site: http://www.mohid.com/
* GitHub repo: https://github.com/Mohid-Water-Modelling-System/Mohid
* Linux build instructions: https://github.com/Mohid-Water-Modelling-System/Mohid/tree/master/Solutions/mohid-in-linux
Linux build instructions use Intel compilers (C and Fortran)
* mkdir cedar:project/MIDOSS/
* git clone git@github.com:Mohid-Water-Modelling-System/Mohid.git MOHID
* 1st build attempt failed on `use proj4`
* Sent email to support@computecanada re: proj4 and proj4fortran modules
(MIDOSS)

Met w/ Charles re: changing backup for /data and /results to borg.


Wed 18-Jul-2018
^^^^^^^^^^^^^^^

Discussed Baynes Sound figure w/ Susan.
Formulated borg backup and pruning policies for /results and /opp and emailed them to Charles.
(SalishSea)

Email reply from Ali@computecanada who will look into adding proj4 and proj4fortran to cvmfs.
(MIDOSS)

See work journal.
(GOMSS)

Received Spark cardboard monitor/keyboard/mouse stands and set one up in 43ravens HQ.


Thu 19-Jul-2018
^^^^^^^^^^^^^^^^^^^^^^^^^^^

Started setting up meerkat as media and backup machine.

Cancelled this afternoon's Body & Soul session with Theresa due to back pain.

Email to Peg re: https://science.ubc.ca/teaching

Ali@computecanada has aded proj4 to cvmfs; tested MOHID build and it failed the same; replied to email with failure transcript and more details about building proj4fortran bindings.
(MIDOSS)

See work journal.
(GOMSS)

Worked on borg backup scripts (/etc/cron.daily/daily-*-backup.sh) on salish at Charles' request. May have accidentally scrapped part of /data/dlatorne/ :-(


Fri 20-Jul-2018
^^^^^^^^^^^^^^^

Prep for next hindcast runs series:
* Susan ran 13nov14
* Susan queued 14nov14 to runs to 30nov14
* Susan queued 01dec14
* started watch_NEMO_hindcast to watch 14nov14
* updated clones on cedar:
  * grid: 77e9cce1dcd6 to 4c269545a0c0
  * NEMO-3.6-code: 5d5d5c95cd8b to 15d3162f0b92
  * SS-run-sets: b7558ecdea3c to a2b0fc96c2f3
  * tools: 9e72ef37f952 to e7646d07561c
  * tracers: c9808b098359 to a5ed7d8b98a3
* built SalishSeaCast config on cedar
* symlinked SS-run-sets/v201702/hindcast/cedar_hindcast_template.yaml into runs/ so that I can stop remembering to copy it
download_weather 12 failed; launched manually at ~13:25 to restart automation.
Fixed bug in download_results that crept in when upload_forcing was enabled for cedar.
Deleted old nowcast-agrif results from orcinus scratch with find ... -type d -mtime +20 | xargs rm -rf
Continued working on baynes_sound_agrif figure module dev notebook.
(SalishSea)

Continued work on borg backup scripts and checked in with Charles on progress.


Sat 21-Jul-2018
^^^^^^^^^^^^^^^

download_weather 06 failed; re-ran manually at ~09:30 to restart automation.
ecget river flow failed due to accidental deletion of /data/dlatorne (see below)
Recovery:
* download_weather 06
* make_runoff_file
* upload_forcing west.cloud-nowcast nowcast+
* upload_forcing orcinus-nowcast-agrif nowcast+
* upload_forcing cedar-hindcast nowcast+
(SalishSea)

Got to do an unplanned recovery test on the /data/dlatorne borg backup:
* I accidentally deleted /data/dlatorne yesterday
* restored with:
  * cd /
  * sudo borg extract --list /backup/borg/data::data-2018-07-20T15:47:43 data/dlatorne
  * sudo chown dlatorne:sallen /data/dlatorne
  * chmod 755 /data/dlatorne


Sun 22-Jul-2018
^^^^^^^^^^^^^^^

01jun15 hindcast run stalled; Susan suspects the pattern indicates a node network glitch:
* killed 01jun15 and 01jul15
* cleaned up scratch dirs
* run_NEMO_hindcast 2015-05-01
* watch_NEMO_hindcast
* run_NEMO_hindcast
(SalishSea)

borg backup production tests:
* results for initial nowcast-green: ~25.5h
* opp update: ~12s (but there is no wwatch3 nowcast)
* results update: ~4h, but that included some several months of hindcast
* data update/add nsoontie ~2h, but that also included touching all of the dlatorne/ files that were restored yesterday
* launched data update/add jpetrie at ~17:30

Worked on switching to HTTPS on Webfaction via LetsEncrypt using 43ravens.ca as the test case:
* refs:
  * https://wesort.co.uk/blog/writing/switching-to-https-on-webfaction
  * https://github.com/Neilpang/acme.sh
  * https://github.com/gregplaysguitar/acme-webfaction
* in webfaction control panel:
  * create new 43ravens_dev website
  * create new 43ravens_dev static only (no .htaccess) application
  * copy files from webapps/43ravens_site/ to webapps/43ravens_dev
  * add 43ravens_dev app to 43ravens_dev website
* installed acme.sh and acme_webfaction.py:
  * cd ~
  * curl https://get.acme.sh | sh
  * wget https://raw.githubusercontent.com/gregplaysguitar/acme-webfaction/master/acme_webfaction.py
  * mv acme_webfaction.py ~/bin/
  * chmod +x ~/bin/acme_webfaction.py
* start a new shell session to enable acme.sh alias
* test certificate generation:
  * acme.sh --issue --test -d dev.43ravens.ca -w ~/webapps/43ravens_dev
* issue certificate
  * acme.sh --issue -d dev.43ravens.ca -w ~/webapps/43ravens_dev --force
* in webfaction control panel use Domains/Websites > SSl Certificates > Add SSL certificate > Copy & Paste:
  * name 43ravens_dev
  * certificate: contents of ~/.acme.sh/dev.43ravens.ca/dev.43ravens.ca.cer
  * private key: contents of ~/.acme.sh/dev.43ravens.ca/dev.43ravens.ca.key
  * intermediates/bundle: contents of ~/.acme.sh/dev.43ravens.ca/ca.cer
  * enable HTTPS and select 43ravens_dev cert in 43ravens_dev website
* install certificate to enable automatic renewal via cron job:
  * acme.sh --install-cert -d dev.43ravens.ca \
 --reloadcmd "WF_SERVER=WebxXx WF_USER=xXxXxXxX WF_PASSWORD=XxXxXxXx WF_CERT_NAME=43ravens_dev acme_webfaction.py"
* tighten permissions on cert files:
  * chmod o-r .acme.sh/dev.43ravens.ca/dev.43ravens.ca*
* tested renewal check and renewal:
  * acme.sh --cron --home "/home/dlatornell/.acme.sh"
  * acme.sh --cron --home "/home/dlatornell/.acme.sh" --force
**Because the app is static-only there is no way of setting up a HTTP->HTTPS redirect.**
* Enabled HTTPS for susanallen.ca:
  * acme.sh --issue --test -d susanallen.ca -w ~/webapps/sea_static
  * acme.sh --issue -d susanallen.ca -w ~/webapps/sea_static --force
  * tighten cert file permissions
  * add cert, key & bundle to webfaction control panel
  * enable HTTPS for sea_static website
  * install cert for automatic renewal


Week 30
-------

Mon 23-Jul-2018
^^^^^^^^^^^^^^^

get_NeahBay_ssh failed due to worker publish ports pool exhaustion; that cascaded to 3 upload_forcing failures:
* Susan manually re-ran get_NeahBay_ssh and it worked
download_results forecast2 failed due to sallen ownership of results dir:
* used sudo to change ownership of forecast2/22jul18/ and sshNB_2018-07-23_15.txt in it
* ran update_forecast_datasets manually to restart automation
* investigated adding ownership setting to lib.fix_perms, but (of course) that won't work without sudo
* investigated worker publish ports pool exhaustion and found lots of stale workers; killed them
download_results hindcast 2015-08-01 failed due to /scratch/dlatorne/hindcast/01aug15/SandyCove_20150827-20150827.nc: Input/output error'; confirmed that was the only file to fail and downloaded it manually; ran split_results manually.
Deleted /results/SalishSea/nowcast-green.19aug17.14mar18.bad_mesozoo/ to recover 1.2T of space on /results which is now at 2.3T (88%).
watch_NEMO_hindcast failed due to: slurm_load_jobs error: Socket timed out on send/recv operation; killed the failed one and launched a new one.
hindcast/01sep15 failed with what looks like a write failure due to disk quota; did some clean-up, then re-queued 01sep15 and 01oct15.
Continued working on baynes_sound_agrif figure module dev notebook.
(SalishSea)

borg data update and add jpetrie took ~2h
borg data update and add mdunphy took ~1h10m
confirmed that /data/$USER/results/ exclusion was not working properly; iterated
borg data update and add sallen retry took ~40m
borg opp update took 33s
borg results update started took ~3.5h, but that included a bunch of new hindcast/ results

Phys Ocgy seminar by Susan on estuarian fluxes in the SoG.

Worked on CMOS expenses.


Tue 24-Jul-2018
^^^^^^^^^^^^^^^

watch_NEMO_hindcast failed due to: slurm_load_jobs error: Socket timed out on send/recv operation; killed the failed one and launched a new one.
Salish Sea team mtg; see whiteboard.
Talked to Tereza about conda packages and environments, and helped her get mocsy built on her Mac.
Continued working on baynes_sound_agrif figure module dev notebook.
(SalishSea)

Deleted /backup/skookum/ to free as much space as possible for borg backups; got to:
  Filesystem        Size  Used Avail Use% Mounted on
  /dev/sda1          17T   11T  5.3T  67% /backup
borg data update and add kramosmu took ~5m
borg data update and add tjarniko took ~20m
Moved /data/vdo/MEOPAR/completed_runs to /data/vdo/results/ and symlinked it into /data/vdo/MEOPAR to avoid notebooks breakage.
borg data update and add gsalidas took ~5m
borg data update and add vdo took ~26m
borg data update and add eolson took ~1h20m
borg opp update was fast
borg results update took ~2h10m

Moved /results/SalishSea/forecast/ to /opp/SalishSea/forecast/ for temporary archival storage.

Worked on CMOS expenses.


Wed 25-Jul-2018
^^^^^^^^^^^^^^^

hindcast/01dec15 stalled at ~95% complete; Susan decided to restart for final 11 days rather re-run entire month.
Investigated Elise's complaint about dia1 file names generated by split_results worker; but that has been there since Dec-2016.
Queued hindcast/01jan15.
(SalishSea)

Deleted old forecast results from /results with find /results/SalishSea/forecast -type d -mtime +20 | xargs rm -rf

Checked internet speed on kudu using fast.com: 160 down, 180 up, 1-8 ms latency.

See project work journal.
(GOMSS)

Installed VirtualBox on kudu; I guess it was removed during upgrade to 18.04??

See project journal.
(Resilient-C)


Thu 26-Jul-2018
^^^^^^^^^^^^^^^

See project journal.
(Resilient-C)

Body & Soul session w/ Theresa.

Atmos Sci seminar by Rachel White of UW.

Answered Elise's question about getting log output of salishsea run from stderr in a bash script.
Set up another hindcast/01jan16 tmp run dir for Susan on cedar.
(SalishSea)

Got a totally useless message from Ali@computecanada re: proj4 & proj4-fortran libraries on cedar for MOHID.
Started trying to build MODHID on salish:
* mkdir /data/dlatorne/MIDOSS
* cd /data/dlatorne/MIDOSS
* git clone git@github.com:Mohid-Water-Modelling-System/Mohid.git MOHID

Created and tested /etc/cron.daily/daily-backup.sh script to sequentially run borg for opp, data, and results.


Fri 27-Jul-2018
^^^^^^^^^^^^^^^

Monthly project mtg by skype.
(MIDOSS)

See project journal.
(Resilient-C)

Checked cron execution of daily-backup.sh:
* no update of opp; perhaps no new files?
* update of data appeared to be successful
* update of results showed checkpoint, indicating that it did not complete successfully
Ran daily-backup.sh manually at ~12:00 for another test.

See project work journal.
(GOMSS)

Updated generation of /opp/wwatch3/nowcast/ddmmmyy/ directories from forecast/ dirs.
(SoG waves)

See project journal.
(SalishSeaCast-FVCOM)


Sat 28-Jul-2018
^^^^^^^^^^^^^^^

Vancouver to Brampton

Started work on separating WWatch3 forecast runs into nowcast + forecast.
NEMO forecast run failed w/ high velocity on western boundary after 1st time step; Susan can't figure out why; decided to leave things and see what happens tomorrow.
(SalishSea)


Sun 29-Jul-2018
^^^^^^^^^^^^^^^

Brampton to Barrie

Sorted through Mom's clothes, etc and took some to Value Village.

Realized that nowcast-agrif/28jul18 didn't run due to symlink race condition in upload_forcing turbidity; recovery:
* upload_forcing turbidity 2018-07-28 --debug
* make_forcing_links nowcast-agrif 2018-07-28
Susan diagnosed that fvcom-nowcast/28jul18 got cobbered by upload of forcing files for fvcom-forecast when NEMO forecast aborted; recovery:
* ssh west.cloud-nowcast make_fvcom_boundary nowcast 2018-07-28
Catch-up runs:
* ssh west.cloud-nowcast make_fvcom_boundary nowcast 2018-07-29
* upload_forcing turbidity 2018-07-29 --debug
* make_forcing_links nowcast-agrif 2018-07-29
* ssh west.cloud-nowcast make_fvcom_boundary forecast 2018-07-29
(SalishSea)


August
======

Week 31
-------

Mon 30-Jul-2018
^^^^^^^^^^^^^^^

borg backup cron job didn't run last night; launched manually.

Sorted through Mom's clothes, etc and took some to Value Village; consolidated lockers into one; got SDB for jewellery.

Barrie to Brampton

nowcast-agrif/30jul18 didn't run due to symlink race condition in upload_forcing turbidity; recovery:
* upload_forcing turbidity 2018-07-28 --debug
* make_forcing_links nowcast-agrif 2018-07-28
nowcast-dev/30jul18 failed on qsub due to full / partition on salish:
* eventually figured out that /root/.cache/borg/ was to blame
* deleted chunk archives and prevented their creation with steps in https://borgbackup.readthedocs.io/en/stable/faq.html#the-borg-cache-eats-way-too-much-disk-space-what-can-i-do
(SalishSea)


Tue 31-Jul-2018
^^^^^^^^^^^^^^^

borg backup cron still not running; changed to sequencing commands with &&; launched manually.

Brampton to Waterloo


Wed 1-Aug-2018
^^^^^^^^^^^^^^

borg backup cron still not running; changed script name back to daily-backup.sh; launched manually.

Worked in Marek's lab at Waterloo while Susan attended & spoke at Frontiers in Applied Math symposium.

Susan noted that nowcast-dev/31jul18 failed because there was no 30jul18/namelist_cfg; created nowcast-dev/31jul18/ and copied nowcast-blue/31jul18/namelist_cfg into it.
Investigated 1h time shift of water level predictions in compare_tide_prediction_max_ssh figure module.
(SalishSea)

See project journal.
(SalishSeaCast-FVCOM)

Dinner w/ Frontiers in Applied Math Symposium speakers.


Thu 2-Aug-2018
^^^^^^^^^^^^^^

Nexus 5X went brick in the night.

Emailed Elise to ask her to investigate Fraser River water quality buoy data page 404; Jennifer MacDonald from ECCC replied with almost instant restoration of page, and request to talk to us about how they can better provide the observations to us.
Set up uptimerobot monitoring on Fraser River water quality buoy data page.
(SalishSea)

See project journal.
(SalishSeaCast-FVCOM)

Listened to Susan's talk in Frontiers in Applied Math Symposium.


Fri 3-Aug-2018
^^^^^^^^^^^^^^

See project journal.
(Resilient-C)

See project work journal.
(GOMSS)

Cleaned up sentry issues.
Created issue #57 re: upload_forcing turbidity file symlink race condition; created a fix and pushed it to skookum for testing.
Moved nemo_cmd.lib.load_run_desc() into prepare module & deleted lib module.
Updated copyright year range in SalishSeaCmd.
Refactored SalishSeaCmd to use prepare.load_run_desc() from NEMO-Cmd pkg.
(SalishSea)

Waterloo to Vancouver


Sun 5-Aug-2018
^^^^^^^^^^^^^^

Discovered that issue #57 re: upload_forcing race condition also can occur for LiveOcean files; added a fix similar to what I did for turbidity and pushed it to skookum for testing.
Updated NEMO-Cmd and SalishSeaCmd clones on production systems:
* skookum:
  * NEMO-Cmd from 00934d451842 to 7c4c47e63ff3
  * SalishSeaCmd from e603ea746db1 to d365dffaec8a
* orcinus:
  * NEMO-Cmd from 00934d451842 to 7c4c47e63ff3
  * SalishSeaCmd from 34a4d4dc4625 to d365dffaec8a
* cedar:
  * NEMO-Cmd from 00934d451842 to 7c4c47e63ff3
  * SalishSeaCmd from e603ea746db1 to d365dffaec8a
* west.cloud:
  * NEMO-Cmd from 00934d451842 to 7c4c47e63ff3
  * SalishSeaCmd from 34a4d4dc4625 to d365dffaec8a
(SalishSea)

Continued work on switching to HTTPS on Webfaction via LetsEncrypt using susanallen.ca as the test case (see Sun 22-Jul-2018 for initial work):
* created sea_http_redirect Static/CGI/PHP-7.2 app to put .htaccess for redirection rules in
* created susanallen_http_redirect website *w/o* HTTPS, connected to susanallen.ca and www.susanallen.ca, w/ the sea_http_redirect app mounted
* created sea_http_redirect/.htaccess containing::

    RewriteEngine On
    #
    # Redirect all http and www traffic to https non-www URL
    # Ref for all but first line: https://simonecarletti.com/blog/2016/08/redirect-domain-http-https-www-apache/
    # Ref to correct for Webfaction using nginx ssl proxy: cpbotha.net... https://goo.gl/Vnbdw9
    #
    RewriteCond %{HTTP:X-Forwarded-SSL} !on [OR]
    RewriteCond %{HTTP_HOST} ^www\. [NC]
    RewriteCond %{HTTP_HOST} ^(?:www\.)?(.+)$ [NC]
    RewriteRule ^ https://%1%{REQUEST_URI} [L,NE,R=301]
* tested with https://www.whynopadlock.com/


Week 32
-------

Mon 6-Aug-2018
^^^^^^^^^^^^^^

Continued work on switching to HTTPS on Webfaction via LetsEncrypt (see Sun 22-Jul-2018 for initial work, and Sun 5-Aug-2018 for HTTP redirection):
* 43ravens.ca:
  * couldn't get acme.sh --issue --test to work in static-only app (despite it working 2wks ago for 43ravens_dev)
  * changed 43ravens_site app to Static/CGI/PHP-7.2
  * test certificate generation:
    * acme.sh --issue --test -d 43ravens.ca -w ~/webapps/43ravens_site
  * issue certificate
    * acme.sh --issue -d 43ravens.ca -w ~/webapps/43ravens_site --force
  * in webfaction control panel use Domains/Websites > SSl Certificates > Add SSL certificate > Copy & Paste:
    * name 43ravens_dev
    * certificate: contents of ~/.acme.sh/43ravens.ca/43ravens.ca.cer
    * private key: contents of ~/.acme.sh/43ravens.ca/43ravens.ca.key
    * intermediates/bundle: contents of ~/.acme.sh/43ravens.ca/ca.cer
    * enable HTTPS and select 43ravens cert in 43ravens_site website
  * install certificate to enable automatic renewal via cron job:
    * acme.sh --install-cert -d 43ravens.ca \
   --reloadcmd "WF_SERVER=WebxXx WF_USER=xXxXxXxX WF_PASSWORD=XxXxXxXx WF_CERT_NAME=43ravens acme_webfaction.py"
  * tighten permissions on cert files:
    * chmod o-r .acme.sh/43ravens.ca/43ravens.ca*
  * tested renewal check:
    * acme.sh --cron --home "/home/dlatornell/.acme.sh"
  * created 43ravens_http_redirect Static/CGI/PHP-7.2 app to put .htaccess for redirection rules in
  * created 43ravens_http_redirect website *w/o* HTTPS, connected to 43ravens.ca and www.43ravens.ca, w/ the 43ravens_http_redirect app mounted
  * created 43ravens_site/.htaccess containing::

      RewriteEngine On
      #
      # Redirect all http and www traffic to https non-www URL
      # Ref for all but first line: https://simonecarletti.com/blog/2016/08/redirect-domain-http-https-www-apache/
      # Ref to correct for Webfaction using nginx ssl proxy: cpbotha.net... https://goo.gl/Vnbdw9
      #
      RewriteCond %{HTTP:X-Forwarded-SSL} !on [OR]
      RewriteCond %{HTTP_HOST} ^www\. [NC]
      RewriteCond %{HTTP_HOST} ^(?:www\.)?(.+)$ [NC]
      RewriteRule ^ https://%1%{REQUEST_URI} [L,NE,R=301]

  * symlinked 43ravens_site/.htaccess into 43ravens_http_redirect/
  * tested with https://www.whynopadlock.com/
Cleared away 43ravens_dev elements:
* acme.sh --revoke -d dev.43ravens.ca -w ~/webapps/43ravens_dev
* acme.sh --remove -d dev.43ravens.ca -w ~/webapps/43ravens_dev
* rm -rf /home/dlatornell/.acme.sh/dev.43ravens.ca
* in control panel:
  * deleted 43ravens_dev website
  * deleted 43ravens_dev certificate
  * deleted 43ravens_dev app


Tue 7-Aug-2018
^^^^^^^^^^^^^^

Finished adding support for `nemo run --waitjob command-line` option on systems that use slurm resource manager.
Salish Sea team mtg; see whiteboard.
Discovered that there are no run results for 6Aug18 onward; debugging and recover:
* confirmed that all nowcast VMs are up and have /nemoShare/MEOPAR mounted with:
  * for n in {0..16}; do echo nowcast$n; ssh nowcast$n mountpoint /nemoShare/MEOPAR/; done
* discovered that I forgot to update SalishSeaNowcast re: load_run_desc() refactoring in NEMO-Cmd and SalishSeaCmd; fixed that bug and updated west.cloud SalishSeaNowcast from e0345389e816 to ca34c765ed58.
* backfilling:
  * make_forcing_links nowcast+ 2018-08-06
  * on west.cloud: make_fvcom_boundary nowcast 2018-08-06
  * upload_forcing west.cloud turbidity 2018-08-06
  * upload_forcing orcinus turbidity 2018-08-06
  * make_forcing_links nowcast-green 2018-08-06
  * make_forcing_links nowcast-agrif 2018-08-06
  * make_forcing_links nowcast+ 2018-08-07
  * make_turbidity_file failed due to inconsistent output hour
  * upload_forcing west.cloud turbidity 2018-08-07
  * upload_forcing orcinus turbidity 2018-08-07
  * cp nowcast-green/07aug18/namelist_cfg nowcast-dev/07aug18/
Susan discovered that as of 01aug18 all hourly files contain 23 instead of 24 hours; it appears that XIOS is spiking to exceed available memory at the end of the run; reduced iodef.xml buffer size factor value from 0.12 to 0.1 for 07aug18 run; it worked.
(SalishSea)


Wed 8-Aug-2018
^^^^^^^^^^^^^^

Dentist appt.

make_turbidity_file failed due to inconsistent output hour:
* upload_forcing west.cloud turbidity
* upload_forcing orcinus turbidity
* upload_forcing cedar turbidity
Started backfilling nowcast-green for 01-06aug18 re: XIOS buffer size factor issue:
* make_forcing_links nowcast-green 2018-08-01
(SalishSea)

See project work journal.
(GOMSS)

See project journal.
(Resilient-C)


Thu 9-Aug-2018
^^^^^^^^^^^^^^

download_weather 00 timed out; re-ran manually and it failed due to missing VGRD file; email to Sandrine@ECCC; reply says it is known and file will appear soon; finally able to complete at ~15:45.
Continued backfilling nowcast-green for 01-06aug18 re: XIOS buffer size factor issue:
* make_forcing_links nowcast-green 2018-08-02
* make_forcing_links nowcast-green 2018-08-03

* make_forcing_links nowcast-green 2018-08-04
* make_forcing_links nowcast-green 2018-08-05
* make_forcing_links nowcast-green 2018-08-06
grib_to_netcdf failed due to missing 00/VGRD file; re-ran manually to restart automation
Update SS-run-sets on west.cloud from f7eb987b30 to 2994df2b01.
(SalishSea)

Email from Ali asking if we still want MOHID installed on cedar; he can build mb1 and mb2; I tried that, but don't know where proj4-fortran bindings are.
(MIDOSS)

Email from Tom Prime asking about how to trigger download_weather.failure().


Fri 10-Aug-2018
^^^^^^^^^^^^^^^

Continued backfilling nowcast-green for 01-06aug18 re: XIOS buffer size factor issue:
* make_forcing_links nowcast-green 2018-08-04

* make_forcing_links nowcast-green 2018-08-05
* make_forcing_links nowcast-green 2018-08-06
Closed the email loop w/ Sandrine re: yesterday HRDPS 00 issues.
nowcast/aug18 failed due to segfault; traced that to yesterday's SS-run-sets update that introduced the use of tracers/north/Dosser_north_TEOS10.nc; ran make_forcing_links manually to restart automation after Susan fixed namelist.
Backed out Vicky's rivers-climatology sub-grid files renaming changeset.
Continued work on Baynes Sound figure module.
Update repos on cedar:
* grid from 4c269545a0c0 to a835327433ca
* NEMO-3.6-code from f8c04b0e8294 to 703f974565e7
* NEMO-Cmd from 7c4c47e63ff3 to 0ac681fbb2d1
* rivers-climatology from 8a4711873c44 to 32e744fbf004
* SS-run-sets from a2b0fc96c2f3 to 5e132065a71f
* tools from e7646d07561c to d05d961b0863
* tracers from a5ed7d8b98a3 to b7c4bd23c455
* XIOS-ARCH from 71122bbcddfe to 967b77939c6e
Did a clean build of NEMO SalishSeaCast config.
(SalishSea)

Email from Tom Prime asking about checklist updating and dumping to YAML.

Canyons/Arctic mtg; see whiteboard.
(Canyons/Arctic)

Worked on building MOHID on salish; got proj4 built, but stopped in proj4-fortran build because autoconf and automake are required and I want to consult with Charles before I install those system packages.
Worked on building MOHID on cedar:
* cd /home/dlatorne/project/MIDOSS/
* mkdir mohid_deps tmp_install_dir
* export DIRINSTALL=$(pwd)/mohid_deps
* export CC=icc
* export FC=ifort

* cd tmp_install_dir
* wget http://download.osgeo.org/proj/proj-4.9.3.tar.gz
* tar -xf proj-4.9.3.tar.gz
* cd proj-4.9.3
* ./configure --prefix=$DIRINSTALL/$proj CC=$CC FC=$FC
* make install
* ln -sf $DIRINSTALL/$proj/lib/libproj.so $DIRINSTALL/$proj/lib/libproj4.so

* cd tmp_install_dir
* git clone https://github.com/mhagdorn/proj4-fortran.git
* cd proj4-fortran/
* ./bootstrap
* ./configure --with-proj4=$DIRINSTALL/$proj --prefix=$DIRINSTALL/$proj4fortran CC=$CC FC=$FC
* PROJ4FORTRAN=$DIRINSTALL/$proj4fortran
* export PATH=$PATH:$PROJ4FORTRAN/lib:$PROJ4FORTRAN/include
* export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$PROJ4FORTRAN/lib
* make
* icc -DIFORT -DPACKAGE_NAME=\"libfproj4\" -DPACKAGE_TARNAME=\"libfproj4\" -DPACKAGE_VERSION=\"1.0\" -DPACKAGE_STRING=\"libfproj4\ 1.0\" -DPACKAGE_BUGREPORT=\"Magnus.Hagdorn@ed.ac.uk\" -DPACKAGE_URL=\"\" -DPACKAGE=\"libfproj4\" -DVERSION=\"1.0\" -DHAVE_LIBM=1 -DHAVE_LIBPROJ=1 -I.   -I/home/dlatorne/project/MIDOSS/mohid_deps//include  -g -O2 -MT fort-proj.o -MD -MP -MF .deps/fort-proj.Tpo -c -o fort-proj.o fort-proj.c
* make install

* cd /home/dlatorne/project/MIDOSS/MOHID/Solutions/mohid-in-linux
* edit compile_mohid.sh:
  * DIR_REQ=/home/dlatorne/project/MIDOSS/mohid_deps
  * PROJ4=$DIR_REQ
  * PROJ4F=$DIR_REQ
* ./compile_mohid.sh -mb1 -mb2 -mw
(MIDOSS)


Sat 11-Aug-2018
^^^^^^^^^^^^^^^

Vancouver to Parksville

Continued backfilling nowcast-green for 01-06aug18 re: XIOS buffer size factor issue:
* make_forcing_links nowcast-green 2018-08-05
* make_forcing_links nowcast-green 2018-08-06
(SalishSea)


Sun 12-Aug-2018
^^^^^^^^^^^^^^^

Parksville to Vancouver


Week 33
-------

Mon 13-Aug-2018
^^^^^^^^^^^^^^^

Finished implementation of Baynes Sound figure module.
Susan launched latest hindcast iteration 01jan16 run; I launched watcher for it and manually queued 01feb16 to start automation.
Helped Tereza design her CO2 results analysis pipeline.
Started adding Baynes Sound surface fields figure to NEMO biology results page.
(SalishSea)

Attended phys ocgy seminar about nighttime turbulent and heat transfer in vineyards.


Tue 14-Aug-2018
^^^^^^^^^^^^^^^

Picked up replacement Nexus 5X at Purolator.

Salish Sea team mtg; see whiteboard.
Finished adding Baynes Sound surface fields figure to NEMO biology results page and deployed it.
Telcon w/ Jennifer MacDonald @EC Water Quality re: alternate web data formats for Fraser River buoy data.
Restarted SalishSeaNowcast manager to add add make_plots nemo nowcast-agrif research messages to registry.
Changed make_plots nemo nowcast-agrif research to run after nowcast-green pings ERDDAP so that all of the results fields are ready for use.
Added badges to SalishSeaNowcast docs and worked on updating pkg dev docs.
(SalishSea)


Wed 15-Aug-2018
^^^^^^^^^^^^^^^

Created SalishSeaNowcast issue#58 re: hindcast slurm_load_jobs error: Socket timed out on send/recv operation.
rsync-ed all forcing useful for hindcast & research runs from skookum to cedar to backfill what is missing between manual uploads and start of upload_forcing cedar.
Queued 01jun16 and 01jul16 hindcast runs that launched watch_NEMO_hindcast 01jun16 to restart automation; 01jun16 failed in the node loss of connection to file system pattern.
(SalishSea)

See project work journal.
(GOMSS)

Updated Mercurial on kudu to 4.7:
* conda activate hg-dev
* cd hg-stable
* hg pull -u
* make clean all
* sudo make install PYTHON=/media/doug/warehouse/conda_envs/hg-dev/bin/python2.7


Thu 16-Aug-2018
^^^^^^^^^^^^^^^

See project work journal.
(GOMSS)

nowcast-blue blew up on 1st time step at south point of west boundary; Susan suspects bug in Orlanski boundary conditions code, which she fixed, and deployed on west.cloud.
Updated NEMO-3.6-code in /results/nowcast-sys/ from 4e7e6a13f8bf to 42097d159d19 and did a clean build of SalishSea config for nowcast-dev; manually ran make_forcing_links salish --shared-storage to restart nowcast-dev automation.
Update NEMO-3.6-code on orcinus from 15480482073d to 42097d159d19; did a clean build of SalishSeaAGRIF config.
Susan ran hindcast/21jun16, and queued 01jul16, but it failed; I requeued 01jul16, launched watcher, then queued 01aug16.
hindcast/01jul16 failed in the node loss of connection to file system pattern; Susan re-queued it manually from the tmp run dir, and requeued 01aug16 too, but that left a zombie watcher on 01jul16.
(SalishSea)

JupyterDay 2018 PIMS:
* "computational narratives"
* syzygy.ca
* Ian Allison - PIMS
  * syzygy is institutional JupyterHubs across Canada
  * hardware agnostic
  * github
  * partitioned resources
  * how:
    * terraform (hashicorp like vagrant)
    * ansible
    * JupyterHub
    * shibboleth - auth
    * docker - each notebook server is a container
    * zfs
    * prometheus
    * grafana
  * lots of inspiration from UC Berkley
  * lab available via url
  * git in container, so clone, etc.

* Meghan Allen CS 103
  * Intro to Systematic Program Design
  * non-majors course cuz 110 doesn't work (2 yrs old)
  * Python & notebooks
  * just-in-time teaching
  * in Jan 103 + 107 will equal 110 (Phil asked

* Sam Hinshaw Data Science 100:
  * integrating Jupyter into Canvas
  * canvas
  * JupyterHub
  * nbgrader
  * canvas has robust API

* Phil Austen EOAS
  * 1995 origin of numerical course to today

* Kim Dill-MacFarland Eco-Scope
  * Experiential Data Science - microbio
  * EDUCE

* Patrick Walls Math 210:


Fri 17-Aug-2018
^^^^^^^^^^^^^^^

Installed openssh-server on lizzy and got ssh working between kudu and it.

Killed hindcast watcher zombies on skookum, launched watcher for 01aug16, queued 01sep16.
Manually ran make_plots nowcast-agrif research.
Updated hindcast-sys repos on cedar:
* NEMO-Cmd
* rivers-climatology
* SS-run-sets
* tools
* tracers
* NEMO-3.6-code
Did a clean build of NEMO SalishSeaCast config on cedar.
Re-queued 01sep16 to use updated rivers, tracers, and SalishSeaCast build; after a big thrash due to a typo in the hindcast YAML file that caused silent failures.
Purged old nowcast-agrif results dirs on orcinus.
nowcast-agrif failed due to unmerged changes from SMELT; updated NEMO-3.6-code back to changeset 1548048207 that worked for 16aug18 run, and re-launched.
(SalishSea)

See project work journal.
(GOMSS)

See project journal.
(SalishSeaCast-FVCOM)

See project journal.
(Resilient-C)


Sat 18-Aug-2018
^^^^^^^^^^^^^^^

Moved watch_NEMO_hindcast month at a time to --full-month option and made default 3 runs per month (2x10 days, then the rest of the days).
hindcast/11nov16 failed.
(SalishSea)

See project work journal.
(GOMSS)


Sun 19-Aug-2018
^^^^^^^^^^^^^^^

See project work journal.
(GOMSS)

Updated SS-run-sets on cedar; queued hindcast 11nov16 and 21nov16; started watcher for 11nov16.
Confirmed that nowcast-agrif/17aug18 finished last night; ran make_plots.
Added run_NEMO_hindcast --walltime option.

Need to backfill nowcast-agrif/18aug18 and 19aug18
(SalishSea)

Installed borg v1.1.6 on lizzy via PPA:
* sudo add-apt-repository ppa:costamagnagianfranco/borgbackup
* sudo apt update
* sudo apt install borgbackup
Changed kudu borg to PPA and upgraded to v1.1.6:
* sudo add-apt-repository ppa:costamagnagianfranco/borgbackup
* sudo apt update
* sudo apt install borgbackup
Set up borg repos tree on lizzy:
* sudo mkdir /media/doug/backup/borg
* sudo chown doug:doug /media/doug/backup/borg
Initialized borg repo for kudu on lizzy from kudu:
* export BORG_PASSCOMMAND="cat ${HOME}/.borg-passphrase"
* borg init --encryption=repokey-blake2 lizzy:/media/doug/backup/borg/kudu
Created borg-bkup/kudu-lizzy.sh and ran initial backup of kudu to lizzy:backup.
Installed anacron on kudu and set it up in ~/.anacron/ to run kudu-lizzy backup daily.


Week 34
-------

Mon 20-Aug-2018
^^^^^^^^^^^^^^^

See project work journal.
(GOMSS)

Fixed outdated and broken links in SalishSeaNowcast docs.
Started work on fixing Baynes Sound AGRIF surface fields figure so that full-domain fringe is from nowcast-agrif run too, but found that we only store daily averages for full-domain.
Resumed work on changing wwatch3 from forecast to nowcast+forecast.
(SalishSea)

Started work on EOAS merit review.


Tue 21-Aug-2018
^^^^^^^^^^^^^^^

See project work journal.
(GOMSS)

Continued work on EOAS merit review.

Ordered 2x8Tb drive for archival results storage (#5 & #6).
Salish Sea team mtg; see whiteboard.
Resumed work on changing wwatch3 from forecast to nowcast+forecast.
Noticed that Slab[UV].nc datssets on ERDDAP hadn't been updated since 17Aug; Susan investigated and said files there the, so I manually pinged ERDDAP with touches in flags/ dir, and everything is good now.
(SalishSea)


Wed 22-Aug-2018
^^^^^^^^^^^^^^^

See project work journal.
(GOMSS)

2x8Tb drives for archival storage were delivered and formatted as archive5 and archive6 via gparted.
orcinus was offline around the time of nowcast-agrif setup, but came back at ~14:00; re-ran make_forcing_links turbidity to restart automation.
(SalishSea)

Finished EOAS merit review; sent it to Roger, Susan & Dafna; scheduled mtg w/ Roger who will review on Susan's behalf.


Thu 23-Aug-2018
^^^^^^^^^^^^^^^

See project work journal.
(GOMSS)


Fri 24-Aug-2018
^^^^^^^^^^^^^^^

See project work journal.
(GOMSS)

Submitted expense claim for 2x8Tb archival results storage drives.
Susan finished archiving nowcast-dev to external drives; I deleted 22au17 through 19aug18 with:
* find /results/SalishSea/nowcast-dev/* -type d -mtime +3 | xargs rm -rf
Worked on updating trello board.
Fixed salishsea-site bug reported and diagnoses by Michael re: show_figure() js function that I accidentally deleted from FVCOM publish template.
(SalishSea)

Canyons/Arctic mtg; see whiteboard.
(Canyons/Arctic)

Vancouver to Victoria


Sat 25-Aug-2018
^^^^^^^^^^^^^^^

Victoria to Sooke

See project work journal.
(GOMSS)


Sun 26-Aug-2018
^^^^^^^^^^^^^^^

Sooke


Week 35
-------

Mon 27-Aug-2018
^^^^^^^^^^^^^^^

Sooke

See project work journal.
(GOMSS)


Tue 28-Aug-2018
^^^^^^^^^^^^^^^

Sooke to Vancouver, via Parksville


Wed 29-Aug-2018
^^^^^^^^^^^^^^^

See project work journal.
(GOMSS)

Researched Bitbucket pipelines and deployments.

Pulled and updated NEMO-3.6-code for Susan on cedar re: hindcast.
(SalishSea)


Thu 30-Aug-2018
^^^^^^^^^^^^^^^

See project work journal.
(GOMSS)

Restarted log_aggregator on skookum because progress messages from watch_NEMO workers on west.cloud weren't appearing.
(SalishSea)


Fri 31-Aug-2018
^^^^^^^^^^^^^^^

download_weather 06 failed; re-ran manually to restart automation.
Worked w/ Susan on archival storage:
* nowcast-blue 31aug17 to 19aug18 archived on archive drives #1 & #2 and deleted from /results/
* nowcast-agrif 21may18 to 19aug18 archived on archive drives #3 & #4 and deleted from /results/
* forecast 31aug17 to 24jul18 moved from /opp/ back to /results/ in preparation for archiving
Added BaynesSoundAGRIF zoom sub-domain, axis, grid, and file definitions to do hourly average output of temperature, salinity, nitrate, and diatoms on full-domain grid for fringe of BaynesSoundAGRIF surface tracers figure.
(SalishSea)

Canyons/Arctic mtg; see whiteboard.
(Canyons/Arctic)

Wrote domain_def.xml section of moad docs.
Added badges to MOAD docs.
Added dev docs and badges to moad_tools docs; also added general and Python modules indices to docs sidebar.
(MOAD)

Updated generation of /opp/wwatch3/nowcast/ddmmmyy/ directories from forecast/ dirs.
(SoG waves)


Sat 1-Sep-2018
^^^^^^^^^^^^^^

See project work journal.
(GOMSS)

Moved portfolio pkg from ~/.local/ on kudu to portfolio conda env.
Did 2017-Q4 and 2018-Q1 ROIs.

Advised Susan on dev of make_CHS_currents_file worker.
(SalishSea)


Sun 2-Sep-2018
^^^^^^^^^^^^^^

See project work journal.
(GOMSS)

Reduced watch_NEMO_hindcast is-queued polling interval from 1 minute to 5 minutes; re: issue #58, but not a complete solution, just a mitigation.
Added unit tests for make_CHS_currents_file worker, and did some refactoring on it.
Network switch failure at UDC disconnected salish and skookum from network.
(SalishSea)

Put Carib back together from Halifax trip.
Gunnar maintenance issues:
* computer transmitter battery is probably dead
* front wheel (that was on Carib for the trip) needs a bearing overhaul
* bottom bracket bearing cups have 16 indentations, so BBT-9 should work


September
=========

Week 36
-------

Mon 3-Sep-2018
^^^^^^^^^^^^^^

**Statutory Holiday** - Labour Day

See project work journal.
(GOMSS)

Thrashed around getting salishsea-site running after network disconnection; stopping and re-starting circus daemon was probably the solution, but only after failing by bouncing the web via circusctl and bouncing apache2.
(SalishSea)

Installed Rapid Photo Downloader on kudu and got image transfers from SD cards and imports to Darktable back under control.


Tue 4-Sep-2018
^^^^^^^^^^^^^^

See project work journal.
(GOMSS)

Email from Charles at ~09:00 saying that skookum has an NFS lock on /data and needs a reboot to resolve; many more things were clearly wrong, but skookum came back online at ~12:00:
* restarted nowcast-sys circus
* restarted salishsea-site circus
* download_weather 12 to restart automation
Sent email to Charles asking if I can add circus launches to /etc/rc.local on skookum.
Refactored Baynes Sound AGRIF figure to use new near-surface fields sub-grid plus fringe hourly average output file from nowcast-agrif runs instead of nowcast-green fields.
(SalishSea)


Wed 5-Sep-2018
^^^^^^^^^^^^^^

root file system on skookum is full:
* checked to see if borg was to blame, then realized that it runs on salish
* opened ticket; Charles fixed it; problem was that when NFS locks the systems write to local storage, so salish was affected too.
(SalishSea)

Finished arrangements for 8-11 Sep trip to Ontario.

See project work journal.
(GOMSS)


Thu 6-Sep-2018
^^^^^^^^^^^^^^

See project work journal.
(GOMSS)

Emailed Jennifer@ECCC re: Fraser buoy web page down.
Worked w/ Susan on archival storage:
* forecast2 31aug17 to 19aug18 archived on archive drives #5 & #6 and deleted from /results/
Added launch envvars and commands for SalishSeaCast, salishsea-site, and ERDDAP to skookum:/etc/rc.local.
Created 2G emergency reserved space on /backup/borg/ so that we can delete it if necessary when something else fills /backup:
* sudo fallocate -l 2G /backup/borg/emergency_reserved_space
Continued work on splitting ww3 runs into nowcast+forecast.
(SalishSea)

EOAS Symposium: Faculty Research Carnival


Fri 7-Sep-2018
^^^^^^^^^^^^^^

Email from Tom@NOC re: nowcast in containers, especially access to config, and launching workers.

Continued work on splitting ww3 runs into nowcast+forecast.
Discussed storage expansion with Charles and then with Susan:
* backup/borg/results: 13T
* backup/borg/data: 1.2T
* backup/borg/opp: 336G
* du -sh /results/forcing /results/observations /results/SalishSea/climatology /results/nowcast-sys/figures /results/SalishSea/nowcast-agrif /results/SalishSea/hindcast /results/SalishSea/nowcast-green:
  465G  /results/forcing
  1.7G  /results/observations
  1.3G  /results/SalishSea/climatology
  81G /results/nowcast-sys/figures
  42G /results/SalishSea/nowcast-agrif
  6.3T  /results/SalishSea/hindcast
  7.7T  /results/SalishSea/nowcast-green
  = ~14.6T
* so, for /results, backup == storage
* /results/hincast stands at ~3yrs (2015-2017), or ~2.1T/yr
* 12yr hindcast (2007-2018) will require 25.2T storage
(SalishSea)

Canyons/Arctic mtg; see whiteboard.
(Canyons/Arctic)

Installed autoconf and automake on salish.
Worked on building MOHID on salish:
* cd /home/dlatorne/project/MIDOSS/
* mkdir mohid_deps tmp_install_dir
* export DIRINSTALL=$(pwd)/mohid_deps
* export CC=gcc
* export FC=gfortran

* cd tmp_install_dir
* wget http://download.osgeo.org/proj/proj-4.9.3.tar.gz
* tar -xf proj-4.9.3.tar.gz
* cd proj-4.9.3
* proj='proj-4.9.3'
* ./configure --prefix=$DIRINSTALL/$proj CC=$CC FC=$FC
* make install
* ln -sf $DIRINSTALL/$proj/lib/libproj.so $DIRINSTALL/$proj/lib/libproj4.so

* cd tmp_install_dir
* git clone https://github.com/mhagdorn/proj4-fortran.git
* cd proj4-fortran/
* proj4fortran='proj4-fortran'
* ./bootstrap
* ./configure --with-proj4=$DIRINSTALL/$proj --prefix=$DIRINSTALL/$proj4fortran CC=$CC FC=$FC
* PROJ4FORTRAN=$DIRINSTALL/$proj4fortran
* export PATH=$PATH:$PROJ4FORTRAN/lib:$PROJ4FORTRAN/include
* export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$PROJ4FORTRAN/lib
* gcc -Df2cFortran -DPACKAGE_NAME=\"libfproj4\" -DPACKAGE_TARNAME=\"libfproj4\" -DPACKAGE_VERSION=\"1.0\" -DPACKAGE_STRING=\"libfproj4\ 1.0\" -DPACKAGE_BUGREPORT=\"Magnus.Hagdorn@ed.ac.uk\" -DPACKAGE_URL=\"\" -DPACKAGE=\"libfproj4\" -DVERSION=\"1.0\" -DHAVE_LIBM=1 -DHAVE_LIBPROJ=1 -I.   -I/data/dlatorne/MIDOSS/tmp_install_dir/proj-4.9.3/mohid_deps//include  -g -O2 -MT fort-proj.o -MD -MP -MF .deps/fort-proj.Tpo -c -o fort-proj.o fort-proj.c
* make install

* cd MOHID/Solutions/mohid-in-linux
* edit compile_mohid.sh:
  * change she-bang to #!/bin/bash
  * FC=gfortran
  * DIR_REQ=/data/dlatorne/MIDOSS/mohid_deps
  * PROJ4=$DIR_REQ
  * PROJ4F=$DIR_REQ
* ./compile_mohid.sh -mb1 -mb2 -mw
Compile mb1 fails due to incorrect include paths for zlib, hdf5, and netcdf4.
Monthly mtg; see notebook.
(MIDOSS)

See project journal.
(SalishSeaCast-FVCOM)


Sat 8-Sep-2018
^^^^^^^^^^^^^^

Vancouver to Brampton


Sun 9-Sep-2018
^^^^^^^^^^^^^^

Brampton-Barrie-Brampton

Email reply to Tom@NOC re: running remote workers, and thoughts on how to do it in containerized nowcast system.
(Prediction Core)

See project work journal.
(GOMSS)

Week 37
-------

Mon 10-Sep-2018
^^^^^^^^^^^^^^^

Brampton

See project work journal.
(GOMSS)

Sent emails to Susan re: tests for her to try re: new Python & SciPy modules on cedar; added notes to whiteboards.
(SalishSea)

Continued work on splitting ww3 runs into nowcast+forecast, but got very confused about restart dates in ww3_shel file for different run types.
(SoG waves)

See project journal.
(SalishSeaCast-FVCOM)


Tue 11-Sep-2018
^^^^^^^^^^^^^^^

Changed SalishSeaCmd and NEMO-Cmd to use/recommend python/3.7.0 module on cedar and graham re: deprecation of python27-scipy-stack module; also updated onboarding docs re: setup on cedar and graham.
Experimented with Mercurial on orcinus re: outdated Python 2.7.3 SSL:
* can't pip install --user hg due to SSL
* hg won't work with both python/2.7.3 and python/3.5.0 modules loaded
* Tried build from source and $HOME install:
  * hg clone
  * cd hg-stable
  * make local PYTHON=/global/software/python-3.5.0/bin/python3
  * edit hg-stable/hg to change she-bang to python3
  * did a sucessful pull and update on NEMO-3.6-code
  * make install-home failed
Restarted log_aggregator because there have been no messages from watch_NEMO on west.cloud since middle of forecast run yesterday.
(SalishSea)

See project journal.
(SalishSeaCast-FVCOM)

See project work journal.
(GOMSS)

Brampton to Vancouver


Wed 12-Sep-2018
^^^^^^^^^^^^^^^

Worked w/ Rachael re: on-boarding.
Added Python code guidelines sections to docs.
Initialized rachael-analysis repo w/ README and LICENSE.
(MIDOSS)

See project work journal.
(GOMSS)

Discovered that download_weather 12 was frozen in hour 24; killed it and downloads finished, but message exchange with manager failed; manually ran:
* get_NeahBay_ssh nowcast
* download_live_ocean
* grib_to_netcdf nowcast+
to restart automation at ~16:55
(SalishSea)


Thu 13-Sep-2018
^^^^^^^^^^^^^^^

See project work journal.
(GOMSS)

EOAS Welcome Back BBQ

Updated hindcast-sys on cedar in preparation for next cycle of hindcast runs:
* change ~/.bashrc to load python/3.7.0 module
* pull, update & pip install --user -e NEMO-Cmd
* pull, update & pip install --user -e SalishSeaCmd
* pull & update rivers-climatology
* pull & update SS-run-sets
* pull & update NEMO-3.6-code
Worked w/ Susan on archival storage:
* forecast 31aug17 to 19aug18 archived on archive drives #5 & #6 and deleted from /results/
Deleted 2018-07-22 borg results archive to try to make space to complete a new results backup.
Deleted /opp/SalishSea tempoary storage.
Started work on adding ubcSSfDepthAveragedCurrents1hV17-02 dataset to ERDDAP based on CHS_currents.nc files in rolling-forecasts/nemo/:
* GenerateDatasetsXml.sh failed complaining about long data type of time variable; fixed by adding dtype item to encoding
* generated and edited XML fragment
* worked on changing automation flow so that CHS_currents files get included in rolling forecasts
* need to change time variable to be called time_counter to keep update_forecast_datasets worker happy
(SalishSea)

Updated generation of /opp/wwatch3/nowcast/ddmmmyy/ directories from forecast/ dirs:
* y=18; m=sep; for d in {04..12}; do dmy=${d}${m}${y}; ymd=$(date '+%C%y%m%d' -d ${dmy}); ymdp2=$(date '+%C%y%m%d' -d "${dmy}+2 days"); echo ${dmy}; mkdir -p -m775 /opp/wwatch3/nowcast/${dmy}; cp -p /opp/wwatch3/forecast/${dmy}/std* /opp/wwatch3/forecast/${dmy}/*.inp /opp/wwatch3/forecast/${dmy}/SoGWW3.sh /opp/wwatch3/forecast/${dmy}/restart001.ww3 /opp/wwatch3/forecast/${dmy}/ww3_shel.log /opp/wwatch3/nowcast/${dmy}/; /usr/bin/ncks -d time,0,47 /opp/wwatch3/forecast/${dmy}/SoG_ww3_fields_${ymd}_${ymdp2}.nc /opp/wwatch3/nowcast/${dmy}/SoG_ww3_fields_${ymd}_${ymd}.nc; /usr/bin/ncks -d time,0,143 /opp/wwatch3/forecast/${dmy}/SoG_ww3_points_${ymd}_${ymdp2}.nc /opp/wwatch3/nowcast/${dmy}/SoG_ww3_points_${ymd}_${ymd}.nc; done
(SoG waves)

MOAD picnic


Fri 14-Sep-2018
^^^^^^^^^^^^^^^

Increased inotify watches limit because PyCharm complained; see https://confluence.jetbrains.com/display/IDEADEV/Inotify+Watches+Limit; setting is in /etc/sysctl.d/30-pycharm.conf

See project work journal.
(GOMSS)

Westgrid townhall:
* slides: https://drive.google.com/file/d/16kyvwKwBfFVGyVKVUeMIo6dlAd8M3O3V/view
* Patrick Mann, Westgrid ops director:
  * RAC 2019
    * UBC site visit by Patrick on Fri 12-Oct afternoon; RAC best practices
    * online 4-Oct
    * informal mtg w/ researchers during site visits:
      * RAC 2018 issues, feedback?
      * new systems feedback
      * survey; what should they ask?
      * future focus?
      * what to tell gov't? how to spend $572M over 5 yrs announced by cabinet in Mar-18?
      * anything else?
      * beer!?
    * RAC schedule
      * Fast track: invitations 11-sep, due 27-sep to 25-oct
      * RRG & RPP: 27-sep to 8-nov
      * reviews: feb-2019
      * awards: late mar-2019
      * implementation: early apr-2019
      * RPP will be subject to progress review
    * RAC resources:
      * cedar, graham, beluga, niagara, arbutus, maybe orcinus
      * expect <50% of CPU ask
      * expect nearline tape storage to be available
    * Westgrid update:
      * graham recovery from 3wk outage continuing; 2% corruption of /project
      * cedar network is now 100 GBit
      * orcinus 2d power system maintenance in October
      * cedar 4d outage for os updates in mid-late Oct
      * arbutus 3cloud expansion:
        * new cloud, migrate VMs, then add old cloud hardware to new cloud
        * 20-sep webinar
        * new platform available 3-oct; migration over several months
      * orcinus defunded Mar-2019, but UBC may continue operation; need to talk to Roman
      * niagara:
        * dragonfly+ inifiband topology is unique; no central switch, edge nodes keep track of routing, very complex cabling
        * 256Tb burst buffer, NVMe SSDs; useful for checkpoint/restart for very large node-count jobs
* Jamie Rosner, UBC ARC
  * Bioinformatics help desk
    * bioinformatics.computecanada.ca
    * bilingual service
    * forum and knowledge-base
    * dedicated panel of ComputeCanada experts will answer questions, in addition to community discussion
    * one-on-one support
* Alex Razoumov, training coordinator
  * training:
    * bi-weekly webinars 10:00 Wednesdays starting 19-sep; https://bit.ly/wgFallTraining
    * in-person:
      * UofA Research Computing Bootcamp 24-28-Sep
      * SFU intro to Python & ArcGIS 25-27-Sep
  * visualization competition:
    * 1-oct to 30-nov
    * datasets provided
    * https://westgrid.github.io/visualizeThis
  * Materials from past training events: https://westgrid.github.io/trainingMaterials

Helped Rachael by email with Mercurial learning curve.
(MIDOSS)

See project work journal.
(Resilient-C)


Sat 15-Sep-2018
^^^^^^^^^^^^^^^

See project work journal.
(GOMSS)

See project work journal.
(Resilient-C)

Discussed storage expansion plans w/ Susan:
* decided to exclude hindcast from /results backup
* initial expansion will be 3x12Tb drives in a RAID5 in the storage chassis
  * need to confirm with Charles that we can expand RAID5 in place by installing additional 12Tb drives
* plan to automate storage of production results from cedar and west.cloud (and maybe orcinus) into ComputeCanada nearline storage
Helped Susan set up sshfs mount of cedar hindcast results on sable so that she can test performance in analysis notebooks; for simple contourf plots the performance is marginally slower than when using the files from /results, but not enough slower that downloading the files from cedar is worth it.
Started dev of tag_release script.
(SalishSea)


Sun 16-Sep-2018
^^^^^^^^^^^^^^^

Continued dev of tag_release script.
(SalishSea)


Week 38
-------

Mon 17-Sep-2018
^^^^^^^^^^^^^^^

Pushed initial version of tag_release script.
Finished adding ubcSSfDepthAveragedCurrents1hV17-02 dataset to ERDDAP based on CHS_currents.nc files in rolling-forecasts/nemo/:
* changed time variable to be called time_counter to keep update_forecast_datasets worker happy, and changed datasets.xml to match
* added ubcSSfDepthAvgdCurrents1hV17-02 to list of ERDDAP datasets that get pinged after NEMO forecast runs
* changed automation to run update_forecast_datasets after make_CHS_currents_file
Changed from yapf to black for formatting SalishSeaNowcast:
* black forces attrs>=17.4.0 (18.2.0 got installed) and that breaks 85 unit tests that have a spec on the nemo_nowcast.NowcastWorker patch; the problem can be resolved by adding m_worker().cli = Mock(name='cli') to the TestMain methods.
* initial run of black took 19s; no additional unit test failures; subsequent run of black that didn't have to do any conversion too 0.3s
* do-nothing run of yapf took 23s
Fixed unit tests that were failing as a result of update of attrs from 16.3.0 to 18.2.0.
Started deleting borg backups of /results to make room for new archives that exclude /results/hindcast.
Added handling of duplicate tag error to tag_release script.
(SalishSea)


Tue 18-Sep-2018
^^^^^^^^^^^^^^^

update_forecast_datasets forecast2 failed, maybe due to time instead of time_counter variable in older forecast/forecast2 files?
SalishSeaCast logs did not roll.
Continued deleting borg backups of /results to make room for new archives that exclude /results/hindcast.
Added coloured log messages and more verbose logging levels (especially success) to tag_release script.
Figured out that near-surface velocity fields slab datasets were not being updated on ERDDAP due to typos in dataset ids in nowcast.yaml; fixed.
Investigated recent get_onc_ferry failures; ferry out of service part of 15sep, all of 16sep, and a bit of 17sep; 17sep data has time mismatch issue; email to Rich and Katia.
Tested tag_release script on cedar:
* pip install --user coloredlogs verboselogs
* yaml and hglib are already install thanks to NEMO-Cmd/SalishSeaCmd
* hg clone SalishSeaNowcast; no need to pip install
* have to run from SalishSeaNowcast/release_mgmt/, but that will make Susan happy...
(SalishSea)

SalishSeaCast mtg; see whiteboard.

Resumed work on changing wwatch3 from forecast to nowcast+forecast.
(SoG Waves)


Wed 19-Sep-2018
^^^^^^^^^^^^^^^

Declined Roger's request to co-instruct EOSC-213 with him.

Worked on debugging update_forecast_datasets forecast2 failure:
* stopped and restarted circusd
* found ncks errors for SlabU, SlabV, and CHS_current and sent them to Susan
* successfully ran update_forecast_datasets foreecast2 manually
* manually ran clear_checklist
Clearance of borg backups of /results finished; 14T free:
* manually ran daily-opp-backup.sh 375G
* manually ran daily-data-backup.sh 1.25T
* manually ran daily-results-backup.sh
Updated SalishSeaNowcast dev env on kudu:
* conda uninstall attrs=16.3.0
* conda install coloredlogs verboselogs
* pip install -U python-hglib
* pip install black
* pip uninstall yapf
* updated pre-commit-hook.sh to use black instead of yapf
(SalishSea)

Updated generation of /opp/wwatch3/nowcast/ddmmmyy/ directories from forecast/ dirs.
(SoG waves)

See project work journal.
(Resilient-C)

See project work journal.
(GOMSS)

See project journal.
(SalishSeaCast-FVCOM)

Updated Mercurial on kudu to 4.7.1+10-41ac8ea1bdd7:
* conda activate hg-dev
* cd hg-stable
* hg pull -u
* make clean all
* sudo make install PYTHON=/media/doug/warehouse/conda_envs/hg-dev/bin/python2.7


Thu 20-Sep-2018
^^^^^^^^^^^^^^^

west.cloud/arbutus upgrade webinar:
Venkat Mahadevan, UBC ARC
* 3 clouds: west.cloud -> arbutus, east.cloud, graham.cloud
* wiki/Cloug_resources
* arbutus present:
  * 7640 cores on 290 nodes
  * 500 TB ceph storage
  * 78 RAM
  * 10 GigE network to nodes and storage
  * 320 projects
* hardware upgrade:
  * 9048 cores on 334 nodes, 56 core machines
  * 5.3 PB storage
  * 91 TB RAM
  * hyperthreading enabled
  * C flavour == 1:1 vCPU to physical CPU, otherwise 10:1
  * C nodes 256 GB RAM and SAS drives
* software upgrade:
  * OpenStack Queens
  * much improved web portal & instance creation wizard (horizon)
  * NUMA aware compute flavours (C), schedules VMs for optimal memory access
  * hypervisor & scheduler improvements
  * attach volumes to multiple instances (instead of NFS)
  * volume stability improved
  * continuous improvement facilitated via dev env
  * better monitoring and alerting
  * new availability zones:
    * compute (C flavours) - assumed to be ephemeral
    * persistent (P flavours)
    * nova (general)
* migration details:
  * arbutus.cloud.computecanada.ca
  * supports firefox & chrome, not safari
  * migration steps:
    * migration to avoid downtime and data safety
    * period of simultaneous arbutus and west.cloud
    * copy images from west.cloud to arbutus
    * can use ansible
    * migrate data
    * update DNS
    * decommission old instances & delete old volumes
    * migration wiki
* RAC tenants will be pre-created
* Keystone identity API v3
* migration:
  * download image via glance from old cloud to local storage
  * upload image via glance to new cloud from local storage
  * can be done via web dashboard GUI or API scripts
* timeline:
  * arbutus available starting in early Oct18
  * tenants will be notified as the system is ready for them to start migration
  * west.cloud logins shutdown Jan19
  * west.cloud storage deletion Feb19
* wiki/Arbutus_West_Cloud_upgrade
* support requests cloud@computecanada.ca

PMEL Salish Sea model webcast:
*  Khangaonkar, et al (2017) Ocean Modelling
*  Khangaonkar, et al (2018) JGR Oceans
(SalishSea)

Sent email to team about ERDDAP datasets.
(MIDOSS)


Fri 21-Sep-2018
^^^^^^^^^^^^^^^

MIDOSS team mtg.
Starred, watched, and forked MOHID on GitHub.
Continued trying to build MOHID on salish:
* edit compile_mohid.sh:
  * ZLIBINC=/usr/include
  * ZLIBLIB=/lib/x86_64-linux-gnu
  * Z_LIB="-lz -lm"
  * HDF5INC=/usr/include
  * HDF5LIB=/lib/x86_64-linux-gnu
  * NETCDFINC=/usr/include
  * NETCDFLIB=/usr/lib
  * LIBS="$LIBS -I${ZLIBINC} -L${ZLIBLIB} $Z_LIB"
  * USE_IEEE_ARITHMETIC=false
That allows mb1 and mb2 to build successfully.
* edit mohid-in-linux/src/MohidWater/src/ModuleConsolidation.F90:
  * comment output private statement on line 250
That results in mw link failure::
  * /data/dlatorne/MIDOSS/mohid_deps/lib/libfproj4.a(fort-proj.o): In function `prjf_strerrno_':
  * /data/dlatorne/MIDOSS/tmp_install_dir/proj4-fortran/fort-proj.c:27: undefined reference to `pj_strerrno'
  * /data/dlatorne/MIDOSS/mohid_deps/lib/libfproj4.a(fort-proj.o): In function `cfort_pj_init':
  * /data/dlatorne/MIDOSS/tmp_install_dir/proj4-fortran/fort-proj.c:43: undefined reference to `pj_init'
  * /data/dlatorne/MIDOSS/tmp_install_dir/proj4-fortran/fort-proj.c:48: undefined reference to `pj_errno'
  * /data/dlatorne/MIDOSS/mohid_deps/lib/libfproj4.a(fort-proj.o): In function `cfort_pj_free':
  * /data/dlatorne/MIDOSS/tmp_install_dir/proj4-fortran/fort-proj.c:57: undefined reference to `pj_free'
  * /data/dlatorne/MIDOSS/tmp_install_dir/proj4-fortran/fort-proj.c:57: undefined reference to `pj_free'
  * /data/dlatorne/MIDOSS/mohid_deps/lib/libfproj4.a(fort-proj.o): In function `cfort_pj_fwd':
  * /data/dlatorne/MIDOSS/tmp_install_dir/proj4-fortran/fort-proj.c:72: undefined reference to `pj_fwd'
  * /data/dlatorne/MIDOSS/tmp_install_dir/proj4-fortran/fort-proj.c:80: undefined reference to `pj_errno'
  * /data/dlatorne/MIDOSS/mohid_deps/lib/libfproj4.a(fort-proj.o): In function `cfort_pj_inv':
  * /data/dlatorne/MIDOSS/tmp_install_dir/proj4-fortran/fort-proj.c:94: undefined reference to `pj_inv'
  * /data/dlatorne/MIDOSS/tmp_install_dir/proj4-fortran/fort-proj.c:102: undefined reference to `pj_errno'
  * collect2: error: ld returned 1 exit status
Tried:
* ./configure --with-proj4=$DIRINSTALL/$proj --prefix=$DIRINSTALL/$proj4fortran CC=$CC FC=$FC CFLAGS="-g -O2 -Df2cFortran"
but still no joy.
Tried to test MohidWater on cedar:
  * mohid-in-linux/test/mohidwater/25m_deep/exe/MohidWater.exe
  * symbol lookup error: test/mohidwater/25m_deep/exe/MohidWater.exe: undefined symbol: __libm_exp_table_128
  * unloaded mpi versions of netcdf, netcdf-fortran, and hdf5 modules and replaced them with non-mpi versions; also unloaded python and perl modules; all because Google suggested that undefined symbol could arise due to module conflicts; no difference...
(MIDOSS)

Discussed ONC API interface for ADCP observations w/ Ben; pushed my uncommitted version of my exploration notebook, and send link to Ben.
Helped Susan setup SalishSeaNowcast tag_release script on cedar.
Manually prototyped flow for SalishSeaNowcast deploy_release script on cedar:
* cd NEMO-3.6-code
* hg pull
* hg update --rev PROD-hindcast-201806-v3
* cd SS-run-sets
* hg pull
* hg update --rev PROD-hindcast-201806-v3
* cd rivers-climatology
* hg pull
* hg update --rev PROD-hindcast-201806-v3
* cd grid
* hg pull
* hg update --rev PROD-hindcast-201806-v3
* cd tides
* hg pull
* hg update --rev PROD-hindcast-201806-v3
* cd tracers
* hg pull
* hg update --rev PROD-hindcast-201806-v3
* cd XIOS-ARCH
* hg pull
* hg update --rev PROD-hindcast-201806-v3
* cd XIOS-2
* hg pull
* hg update --rev PROD-hindcast-201806-v3
* cd NEMO-3.6-code/NEMOGCM/CONFIG/
* ./makenemo -n SalishSeaCast -m X64_CEDAR clean
* XIOS_HOME=/home/dlatorne/project/SalishSea/hindcast-sys/XIOS-2 ./makenemo -n SalishSeaCast -m X64_CEDAR -j 4
After Susan had to edit and re-tag SS-run-sets, I landed in a merge conflict on cedar when I tried to update to new tag rev, so flow should probably be:
* hg update --rev tip
* hg pull
* hg update --rev tag
(SalishSea)


Sat 22-Sep-2018
^^^^^^^^^^^^^^^

nowcast-agrif run failed due to a daemon launch error on pod28b16:
* moved borked results aside on orcinus and skookum
* re-ran run_NEMO_agrif manually to restart automation
(SalishSea)

Started researching automatic deployment on push via Bitbucket pipelines.
(salishsea-site)


Sun 23-Sep-2018
^^^^^^^^^^^^^^^

Set up automatic deployment on push via Bitbucket pipelines.
(salishsea-site)


Week 39
-------

Mon 24-Sep-2018
^^^^^^^^^^^^^^^

Delete Jie's crontab that Susan had noticed was still trying to run ferry data download jobs.
Investigated make_turbidity_file worker errors; buoy web page has not been updated since 2018-09-20 13:10.
Started watch_NEMO_hindcast for 11jun15.
Ran run_NEMO_hindcast for 21jun15.
Add blurb to ERDDAP front page about coming transition from v17-02 to v18-06.
(SalishSea)

Continued trying to build MOHID on salish:
* cleaned up /data/dlatorne/MIDOSS/mohid_deps/
* proj-4.9.3:
  * make clean
  * proj='proj-4.9.3'
  * ./configure --prefix=$DIRINSTALL/$proj CC=$CC FC=$FC
  * make
  * make install
  * ln -sf $DIRINSTALL/$proj/lib/libproj.so $DIRINSTALL/$proj/lib/libproj4.so
  * PROJ4=$DIRINSTALL/$proj
  * export LD_LIBRARY_PATH=$PROJ4/lib
  * export PATH=$PATH:$PROJ4/bin:$PROJ4/lib:$PROJ4/include
  * export PROJ_PREFIX=$PROJ4/lib
* proj4-fortran make clean doesn't delete proj4.mod, and maybe not libfproj4.a, so did manual deletion of everything that git status said was untracked
* did proj4-fortran clean build with:
  * ./configure --with-proj4=$DIRINSTALL/$proj --prefix=$DIRINSTALL/$proj4fortran CC=$CC FC=$FC CFLAGS="-g -O2 -Df2cFortran"
  * make
  * make check
  * ./test_proj worked
  * PROJ4FORTRAN=$DIRINSTALL/$proj4fortran
  * export PATH=$PATH:$PROJ4FORTRAN/lib:$PROJ4FORTRAN/include
  * export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$PROJ4FORTRAN/lib
  * make install
* ./compile_modid.sh -c
* ./compile_modid.sh -mb1 -mb2 -mw
Test MohidWater on salish:
  * mohid-in-linux/test/mohidwater/25m_deep/exe/MohidWater.exe

Add email about ERDDAP datasets to Google Drive.
(MIDOSS)

Phys Ocgy seminar on Mode 2 internal waves by David Deepwell (Waterloo, no UofA)


Tue 25-Sep-2018
^^^^^^^^^^^^^^^

Reviewed conduino docs and paper for Karina/Susan.
Canyons/Arctic mtg; see whiteboard.
(Canyons/Arctic)

Reviewed matplotlib 3.0 changes.
Salish Sea mtg; see whiteboard.
(SalishSea)

Continued trying to build MOHID on salish:
* export CC=gcc
* export FC=gfortran
* export DIRINSTALL=/data/dlatorne/MIDOSS/mohid_deps
* clean build of proj-4.9.3:
  * proj='proj-4.9.3'
  * make clean
  * ./configure --prefix=$DIRINSTALL/$proj CC=$CC FC=$FC
  * make
  * make check
  * make install
  * ln -sf $DIRINSTALL/$proj/lib/libproj.so $DIRINSTALL/$proj/lib/libproj4.so
  * PROJ4=$DIRINSTALL/$proj
  * export LD_LIBRARY_PATH=$PROJ4/lib
  * export PATH=$PATH:$PROJ4/bin:$PROJ4/lib:$PROJ4/include
  * export PROJ_PREFIX=$PROJ4/lib
* clean build of proj4-fortran:
  * proj4fortran='proj4-fortran'
  * ./bootstrap
  * ./configure --with-proj4=$DIRINSTALL/$proj --prefix=$DIRINSTALL/$proj4fortran CC=$CC FC=$FC CFLAGS="-g -O2 -Df2cFortran"
  * PROJ4FORTRAN=$DIRINSTALL/$proj4fortran
  * export PATH=$PATH:$PROJ4FORTRAN/lib:$PROJ4FORTRAN/include
  * export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$PROJ4FORTRAN/lib
  * make
  * make check
  * make install
* clean build of mohid:
  * ./compile_mohid --clean
  * ./compile_mohid -mb1 -mb2 -mw
  * same mw link failure as 21sep
* clean build of mohid w/o proj4 and with debugging:
  * edit compile_mohid:
    * IS_DEBUG=true
    * USE_PROJ4=false
  * ./compile_mohid --clean
  * ./compile_mohid -mb1 -mb2 -mw
  * build succeeded!!! but with a major crap-load of warnings
  * cd test/mohidwater/25m_deep/exe
  * ./MohidWater.exe
    * failed quickly:
      Program received signal SIGSEGV: Segmentation fault - invalid memory reference.

      Backtrace for this error:
      #0  0x7F1A43070777
      #1  0x7F1A43070D7E
      #2  0x7F1A42599CAF
      #3  0xC6B87C in __modulefillmatrix_MOD_killfillmatrix at ModuleFillMatrix.F90:11773
      #4  0x673F54 in constructrugosity at ModuleInterfaceSedimentWater.F90:1794
      #5  0x67A9AE in __moduleinterfacesedimentwater_MOD_startinterfacesedimentwater at ModuleInterfaceSedimentWater.F90:913
      #6  0x7C9471 in __modulemodel_MOD_constructmodel at ModuleModel.F90:982
      #7  0xD78349 in constructmohidwater at Main.F90:293
      #8  0x4106C8 in mohidwater at Main.F90:227
      #9  0x7F1A42584F44
      Segmentation fault (core dumped)
Switched to  try building mohid on cedar:
* clean build of mohid w/o proj4 and with debugging:
  * edit compile_mohid:
    * IS_DEBUG=true
    * USE_PROJ4=false
  * ./compile_mohid --clean
  * ./compile_mohid -mb1 -mb2 -mw
  * build succeeded!!! with absolutely no warnings
  * cd test/mohidwater/25m_deep/exe
  * ./MohidWater.exe
    * worked!!
    * output in:
      * Error_and_Messages_1.log
      * ../res/Outwatch_1.txt
      * ../res/Hydrodynamic_1.hdf5
* clean build of mohid w/ proj4 and with debugging:
  * module load proj4-fortran/1.0
  * edit compile_mohid:
    * IS_DEBUG=true
    * USE_PROJ4=true
  * ./compile_mohid --clean
  * ./compile_mohid -mb1 -mb2 -mw
  * cd test/mohidwater/25m_deep/exe
  * ./MohidWater.exe
    * worked!!
* I'm really puzzled about how linker is finding netCDF, hdf5, proj4 etc. libraries because the paths in compile_mohid are bogus
* build w/ USER_MPI failed
(MIDOSS)


Wed 26-Sep-2018
^^^^^^^^^^^^^^^

See project work journal.
(GOMSS)

See project journal.
(SalishSeaCast-FVCOM)

Started trying to debug NEMO_Nowcast.cli.CommandLineInterface unhashable object issue that arises w/ attrs-18.2.0.
(SalishSea)

Helped Rachael w/ bash setup on tyee.
(MIDOSS)


Thu 27-Sep-2018
^^^^^^^^^^^^^^^

Power outage in EOS Main at ~09:00 disrupted network access, so I worked at home.

Researched mohid Convert2netcdf tool; discovered that it was "under development" in 2009 and nohting since, apparently.
Continued scoping mohid on cedar:
* reverted compile_mohid to repo head
* module load proj4-fortran
* clean build of mb1, mb2 & mw and 25m_deep test worked, so LIBRARY_PATH envvar must override paths in compile_mohid
* attempt to build mohid_tools fails due to missing ModuleNOAA_ShoreLine.F90 file
Added content to MIDOSS docs index page.
Wrote docs section about running on cedar.
Experimented with running on cedar in interactive allocation; 1 process is optimal for tank_25m test case, and with alternative files layout.
(MIDOSS)

salishsea-site went down late in the evening.
(SalishSea)


Fri 28-Sep-2018
^^^^^^^^^^^^^^^

Killed and re-launched salishsea-site circus to get site operational again.
nowcast-agrif/27sep18 spent all night on the queue on orcinus, then failed because turbidity file was missing; recovery at 10:45:
* upload_forcing turbidity 2018-09-27 --debug
* make_forcing_links nowcast-agrif 2018-09-27
* email to Roman
Created skookum:/opp/observations/AISDATA/ and rsync-ed contents of /home/mdunphy/AISDATA/ into it.
Started work on notebook exploring creating netCDF files from AIS data to feed ERDDAP dataset.
(SalishSea)

Email to team about docs site and MOHID on cedar.
(MIDOSS)

See project work journal.
(GOMSS)

See project journal.
(SalishSeaCast-FVCOM)


Sat 29-Sep-2018
^^^^^^^^^^^^^^^

download_weather 12 froze in hour 41; killed it and downloads finished, but message exchange with manager failed; manually ran:
* get_NeahBay_ssh nowcast
* download_live_ocean
* grib_to_netcdf nowcast+
to restart automation at ~14:00
That caused nowcast-agrif run to be queued, and it didn't start until 04:25 on Sunday.
Debugged NEMO_Nowcast.cli.CommandLineInterface unhashable object issue that arises w/ attrs-18.2.0; problem is cli._arrow_date() method: a bound method is unhashable; changed it to a function defined within cli.add_date_option() or a static method of CommandLineInterface.
(SalishSea)


Sun 30-Sep-2018
^^^^^^^^^^^^^^^

Watched EuroPycon 2018 talk about VS Code & Python Extension: https://www.youtube.com/watch?v=6YLMWU-5H9o then send email about it to MOAD group.

nowcast-agrif/29sep18 failed when early morning make_forcing_links pulled the turbidity file out from under it; recover at ~10:20:
* upload_forcing turbidity 2018-09-29 --debug
* make_forcing_links nowcast-agrif 2018-09-29
* clobbered by nowcast turbidity file upload/linking
* tried make_forcing_links again at ~11:05
Enabled watch_NEMO_hindcast worker to cancel stuck jobs.
(SalishSea)

Monitored ONC dive to deploy new SCVIP node.


October
=======

Week 40
-------

Mon 1-Oct-2018
^^^^^^^^^^^^^^

Investigated stalling watch_NEMO_hindcast; looks like cat ocean.output is the problem.
Reverted watch_NEMO_hindcast in production; started a new one for 01jun176, queued 11jun16.
Continued work on watch_NEMO_hindcast; change cat ocean.output to grep ocean.output for better performance over ssh.
Flipped mdunphy cron job from salish to skookum to download VFPA AIS data to skookum:/opp/observations/AISDATA/ instead of /home/mdunphy/AISDATA/ into it (after final rsync from the latter location).
Found email thread with Neil Swart from 11oct17 in which he provided me with CMC cstintrp package code that includes cstrpn2cdf; now I just have to remember where I downloaded that code to; re-downloaded code to /data/dlatorne/MEOPAR/cstintrp_3.0.4/ on salish and warehouse/MEOPAR/cstintrp_3.0.4/ on kudu and niko.
hindcast/21jun16 started but didn't write any files, and ls freezes; decar recovered later in the evening.
(SalishSea)

uptimerobot reported site down at ~10:00; stopped and restarted circus daemon at 11:45; need to add logging to figure out how/why app is locking up now more than it used to.
(salishsea-site)

ONC replaced SEVIP node.

Phys Ocgy seminar by Melanie Chinoan about internal wave energy in the Arctic.

Resumed work on changing wwatch3 from forecast to nowcast+forecast:
* ran wwatch3-nowcast/01oct18 successfully
* ran wwatch3-forecast/01oct18 successfully
* deployed changed to west.cloud and skookum
* restart manager on skookum
(SoG Waves)

Tried building mohid on salish with -finit-local-zero; still segfaults.
Helped Rachael understand sys.path via email.
(MIDOSS)


Tue 2-Oct-2018
^^^^^^^^^^^^^^

Killed wwatch3 processes left over from yesterday's testing that caused NEMO forecast2 to take ~4h.
SalishSeaCast mtg; see whiteboard.
01oct18 comparison figures show amazing agreement between model and observations at ONC central and east nodes.
Started work on GEMLAM RPN to NEMO netCDF input file conversion:
* cstrpn2cdf executable in pkg from CMC failed w/ undefined symbol netcdf_mp_nf90_create_
* built cstrpn2cdf on salish:
  * cd /data/dlatorne/MEOPAR/cstintrp_3.0.4/tools/src/csttools
  * gfortran -fno-range-check -I/usr/include -c std.f90 cdf.f90 cdf_std.f90 cstrpn2cdf.F90
  * linking fails; looks like we need librmn
Fixed next_workers bug re: running wwatch3 as nowcast+forecast.
Adapted update_forecast_datasets re: running wwatch3 as nowcast+forecast.
Updated nowcast-fig-dev env on niko to matplotlib-3.0.0 and it brought a lot of stuff with it; also updated xarray, and jupyterlab; prep for SalishSeaCast figures breakage assessment.
(SalishSea)


Wed 3-Oct-2018
^^^^^^^^^^^^^^

wwatch3-forecast2/03oct18 run succeeded, and logs rolled, but rolling forecast update and wave figures failed.
Deployed watch_NEMO_hindcast that detects and cancels stuck runs; detection worked well later in the day, but had to fix a bug in job cancellation command.
(SalishSea)

See project work journal.
(GOMSS)

Updated Mercurial on kudu to 4.7.2+2-3e61146d7b24:
* conda activate hg-dev
* cd hg-stable
* hg pull -u
* make clean all
* sudo make install PYTHON=/media/doug/warehouse/conda_envs/hg-dev/bin/python2.7

Updated 43ravens biz journal.

Spent the afternoon feeling really unmotivated, and worrying about onset of back pain episode.


Thu 4-Oct-2018
^^^^^^^^^^^^^^

Woke with very stiff, sore back.

See project work journal.
(GOMSS)

Deployed watch_NEMO_hindcast that detect stuck runs via exactly-one E R R O R signature and re-queues them.
Worked on 2nd Narrows AIS HADCP feed to ERDDAP dataset notebook, and found jupyter lab black extension along the way.
(SalishSea)

Updated Mercurial on niko to 4.7.2+2-3e61146d7b24:
* conda activate hg-dev
* cd hg-stable
* hg pull -u
* make clean all
* sudo make install PYTHON=/media/doug/warehouse/conda_envs/hg-dev/bin/python2.7

EOAS Colloquium: Valentina - Modeling Glacier Contributions to Streamflow and Sea Level Rise

Add handling of missing stream velocity data from Fraser River water quality buoy.
Set aside some uncommitted code in production that preventing warning level log messages when relative humidity
(ECget)


Fri 5-Oct-2018
^^^^^^^^^^^^^^

hindcast/21sep16 run got stuck and watch_NEMO_hindcast successfully cancelled and re-queued it.
download_weather 06 failed; re-ran to restart automation at ~07:50.
Changed wave buoy obs from line to points in wwatch3 figures.
Change VENUS node comparison figures to plot obs behind models and added alpha transparency to model lines.
(SalishSea)

Sent email to Susan, Elise, Ben, Birgit & Tereza about using interactive sessions on cedar for compiling NEMO, running salishsea run, and executing test runs. Tried salishsea prepare in an interactive session and it has the same behaviour as on the login node: 7+ minutes on first execution, 17 seconds subsequently, so my file system caching hypothesis holds :-(

See project journal.
(SalishSeaCast-FVCOM)


Sat 6-Oct-2018
^^^^^^^^^^^^^^

Vancouver to Parksville

Started refactoring watch_NEMO_hindcast to move interaction with cedar to  _HindcastJob class so that watcher can re-queue dependent jobs, and change the cedar job that it is watching when it recovers from a stuck job error condition.
(SalishSea)


Sun 7-Oct-2018
^^^^^^^^^^^^^^

Continued refactoring watch_NEMO_hindcast:
* finished _HindcastJob class
* changed unit tests to use a YAML config fixture that provided nemo_nowcast.Config instances instead of dicts
* started adding unit tests for _HindcastJob
* added ability to re-queue dependent runs after a stuck run failure
Updated attrs form 16.3.0 to 18.2.0 on skookum so that refactored watch_NEMO_hindcast would work.
(SalishSea)


Week 41
-------

Mon 8-Oct-2018
^^^^^^^^^^^^^^

**Statutory Holiday** - Thanksgiving

Last night's attrs update on skookum caused multiple early morning worker failures because I didn't update NEMO_Nowcast at the same time; fixed, and restarted forecast2 automation at ~09:40.
Helped Susan w/ nowcast-fig-dev package version issues.
Continued refactoring watch_NEMO_hindcast:
* continued adding unit tests for _HindcastJob
* fixed bug in re-queuing dependent runs after a stuck run failure
(SalishSea)

Parksville to Vancouver


Tue 9-Oct-2018
^^^^^^^^^^^^^^

MOAD group mtg /w Youyu Lu & Hao Wei (Tainjin Univ) visiting.

Continued refactoring watch_NEMO_hindcast:
* added monitoring of re-queued stuck run until it starts running so that watcher switches to monitoring new run
* continued adding unit tests for _HindcastJob
Tested pytest-xdist on niko for SalishSeaNowcast; tests run faster, but setup takes longer than to run 1-core tests.
Figured out the package version pins necessary to create a new nowcast-fig-dev environment that is both compatible with production, and with as many recent package updates as possible; emailed diff to Susan.
Built nowcast-fig-dev-mpl-3 env for migration to matplotlib-3.0.0; figures that need to be assessed/ported:
* nowcast/figures/comparison/compare_venus_ctd.py
* nowcast/figures/comparison/salinity_ferry_track.py
* nowcast/figures/comparison/sandheads_winds.py
* nowcast/figures/fvcom/second_narrows_current.py
* nowcast/figures/fvcom/tide_stn_water_level.py
* nowcast/figures/publish/compare_tide_prediction_max_ssh.py
* nowcast/figures/publish/pt_atkinson_tide.py
* nowcast/figures/publish/storm_surge_alerts.py
* nowcast/figures/publish/storm_surge_alerts_thumbnail.py
* nowcast/figures/research/baynes_sound_agrif.py
* nowcast/figures/research/time_series_plots.py
* nowcast/figures/research/tracer_thalweg_and_surface_hourly.py
* nowcast/figures/research/tracer_thalweg_and_surface.py
* nowcast/figures/research/velocity_section_and_surface.py
* nowcast/figures/wwatch3/wave_height_period.py
(SalishSea)

See project work journal.
(GOMSS)


Wed 10-Oct-2018
^^^^^^^^^^^^^^^

See project journal.
(SalishSeaCast-FVCOM)

See project work journal.
(GOMSS)

nowcast-green failed at end of run due to XIOS process dying; re-run had the same fate; reduced XIOS buffer size factor from 0.1 to 0.08 for a 3rd try.
Reviewed and buffed Susan's email to Richard@ONC re: nowcast and fvcom VMs on arbutus.cloud.
(SalishSea)


Thu 11-Oct-2018
^^^^^^^^^^^^^^^

See project journal.
(SalishSeaCast-FVCOM)

Continued work on notebook exploring creating netCDF files from AIS data to feed ERDDAP dataset.
Tested pytest-xdist on kudu for SalishSeaNowcast; nice speedup at -n4; also tested pytest-randomly, and it randomizes test order (duh!)
(SalishSea)


Fri 12-Oct-2018
^^^^^^^^^^^^^^^

Project mtg.
Python model viz session w/ Rachael.
Teid to load mohid hdf5 output in python; no luck.
(MIDOSS)

Charles mounted /results2/ on skookum:
* created /results2/SalishSea/hindcast/
* changed nowcast.yaml to make /results2/SalishSea/hindcast/ the hindcast results archive
* started rsync of /results/SalishSea/hindcast to /results2/SalishSea/hindcast/
Got 14Tb cold spare drive from Charles for safekeeping in my office.
Deployed watch_NEMO_hindcast to skookum w/ monitoring of re-queued stuck run until it starts running so that watcher switches to monitoring new run.
(SalishSea)

UBC ARC session about RAC.


Sat 13-Oct-2018
^^^^^^^^^^^^^^^

Installed VS Code on kudu with Python, Mercurial, reStructuredText, Sublime, and code spell extensions; not thrilled enough yet to switch from Sublime (at least for rst).


Sun 14-Oct-2018
^^^^^^^^^^^^^^^

Started adding narrative to model results viz notebook from Friday's session w/ Rachael.
(MIDOSS)


Week 42
-------

Mon 15-Oct-2018
^^^^^^^^^^^^^^^

Continued adding narrative to model results viz notebook from Friday's session w/ Rachael.
(MIDOSS)

hindcast stopped on 10feb18 due to cedar maintenance downtime.
Lots of unsuccessful farting around trying to get PyCharm debugger working with a notebook by attaching to the kernel process.
Deployed temporary nowcast config with cedar-hindcast commented out of enabled hosts until cedar returns to service.
Continued work on migration of figure modules to matplotlib-3.0.0:
* Fixed bug in salishsea_tools.nc_tools.timestamp() re: MaskedArrays and netCDF4>-1.4.0.
* Created SalishSeaNowcast issue #62 re: changing Axes.set_axes_bgcolor() calls to Axes.set_facecolor() in figure modules, and resolved it.
* Created SalishSeaNowcast issue #63 re: replacing marker color with markerfacecolor and markeredgecolor in figure modules, and resolved it.
* Ported:
  * nowcast/figures/comparison/compare_venus_ctd.py
  * nowcast/figures/comparison/sandheads_winds.py
download_weather 18 failed
download_weather 00 failed
(SalishSea)

See project work journal.
(Resilient-C)


Tue 16-Oct-2018
^^^^^^^^^^^^^^^

download_weather 06 failed
Email from Sandrine re: major issues at ECCC delaying HRPDS to datamart; expecting at least 4h delay of 12 weather.
Ran download_weather 18 at ~09:15.
download_weather 06 failed
SalishSeaCast mtg; see whiteboard.
Ran download_weather 00 at ~13:00.
Ran download_weather 06 at ~14:00.
Continued work on migration of figure modules to matplotlib-3.0.0:
* Created SalishSeaNowcast issue #64 re: setting time series x-axis limits explicitly in figure modules.
* Set axes facecolor in several figure modules where it was not done.
* Ported:
  * nowcast/figures/fvcom/second_narrows_current.py
  * nowcast/figures/fvcom/tide_stn_water_level.py
  * nowcast/figures/publish/compare_tide_prediction_max_ssh.py
  * nowcast/figures/wwatch3/wave_height_period.py
* TODO:
  * nowcast/figures/publish/pt_atkinson_tide.py
  * nowcast/figures/publish/storm_surge_alerts.py
  * nowcast/figures/publish/storm_surge_alerts_thumbnail.py
  * nowcast/figures/research/baynes_sound_agrif.py
  * nowcast/figures/research/time_series_plots.py
  * nowcast/figures/research/tracer_thalweg_and_surface_hourly.py
  * nowcast/figures/research/tracer_thalweg_and_surface.py
  * nowcast/figures/research/velocity_section_and_surface.py
  * nowcast/figures/comparison/salinity_ferry_track.py
Deleted /results/SalishSea/hindcast/ now that it is on /results2/ and that is mounted on fish machines.
Ran download_weather 12 at ~15:40.
(SalishSea)

See project work journal.
(GOMSS)


Wed 17-Oct-2018
^^^^^^^^^^^^^^^

See project work journal.
(GOMSS)

Listened to Vancouver mayoral debate on CBC Radio 1.

Worked w/ Rachael on conda env issue related to https://github.com/Unidata/netcdf-c/issues/657
(MIDOSS)

Eye exam by Dr. Rupnow.


Thu 18-Oct-2018
^^^^^^^^^^^^^^^

Despaired of resolving Rachael's conda env issue until I can lay hands on her Mac; recommended x2go or headless jupyter from tyee.
Prep for stakeholder's workshop.
(MIDOSS)

Investigated yesterday's turbidity file failure; Fraser buoy web page is unchanged since 2018-10-16 15:10.
(SalishSea)

Investigated duplicated lines in Fraser turbidity feed only to discover "that how it's supposed to work".
(ECget)

See project work journal.
(GOMSS)


Fri 19-Oct-2018
^^^^^^^^^^^^^^^

Local stakeholders workshop @ Robson Square.
(MIDOSS)

See project journal.
(SalishSeaCast-FVCOM)

Ordered new daily glasses and new lens for cycling.

Continued work on migration of figure modules to matplotlib-3.0.0:
* Moved Axes.set_facecolor() into _prep_fig_axes() functions; re: issue #62.
* TODO:
  * nowcast/figures/publish/pt_atkinson_tide.py
  * nowcast/figures/publish/storm_surge_alerts.py
  * nowcast/figures/publish/storm_surge_alerts_thumbnail.py
  * nowcast/figures/research/baynes_sound_agrif.py
  * nowcast/figures/research/time_series_plots.py
  * nowcast/figures/research/tracer_thalweg_and_surface_hourly.py
  * nowcast/figures/research/tracer_thalweg_and_surface.py
  * nowcast/figures/research/velocity_section_and_surface.py
  * nowcast/figures/comparison/salinity_ferry_track.py
Continued work on notebook exploring creating netCDF files from AIS data to feed ERDDAP dataset; got all the way to a tableDAP dataset on ERDDAP.
(SalishSea)


Sat 20-Oct-2018
^^^^^^^^^^^^^^^

orcinus went down for building power maintenance
cedar resumed hindcast runs at ~02:00, but 11feb18 failed due to bad LiveOcean file:
* make_live_ocean_files 2018-02-18
* make_live_ocean_files 2018-02-19
Re-enabled cedar-hindcast in config on skookum, and backfilled uploads for the week:
* for d in {15..20}; upload_forcing nowcast+ 2018-10-$d
* for d in {15..20}; upload_forcing turbidity 2018-10-$d
* for d in {15..20}; upload_forcing forecast2 2018-10-$d
Started dev of get_vfpa_hadcp worker.
(SalishSea)


Sun 21-Oct-2018
^^^^^^^^^^^^^^^

Continued dev of get_vfpa_hadcp worker.
(SalishSea)


Week 43
-------

Mon 22-Oct-2018
^^^^^^^^^^^^^^^

Replaced symlinked LiveOcean files for 20, 21, 23 & 29 jul18 on skookum with newly generated real files so that Susan can upload them to cedar to continue hindcast.
Pushed get_vfpa_hadcp worker w/ minimal test suite.
backfill nowcast-agrif runs on orcinus after weekend power outage downtime:
* for d in {20..22} upload_forcing forecast2 --debug --run-date 2018-10-$d
* for d in {20..22} upload_forcing nowcast+ --debug --run-date 2018-10-$d
* for d in {20..22} upload_forcing turbidity --debug --run-date 2018-10-$d
* make_forcing_links nowcast-agrif --run-date 2018-10-20

* make_forcing_links nowcast-agrif --run-date 2018-10-21
* make_forcing_links nowcast-agrif --run-date 2018-10-22
(SalishSea)

Explored Salish Sea test case that Shihan sent us:
* ~7d run 2015-04-08 00:30 to 2015-04-14 22:30
* 1200 s time step
* SalishSea/Model_7.dat file says 12 thread for OpenMP; VancouverHarbour/Model_1.dat has OPENMP_NUM_THREADS commented out
* results:
  * Lagrangian*.hdf5; 200M and 335M
  * OilOutput.sro; 991K; seems to be csv-ish
Continued exploration in larger context of Rachael's sensitivity/montecarlo runs work w/ her.
(MIDOSS)


Tue 23-Oct-2018
^^^^^^^^^^^^^^^

Canyons/Arctic team mtg; see whiteboard.
(Canyons/Arctic)

Built MIDOSS/SalishSeaShihan repo of test case files.
Tested MOHID compilation on cedar:
* login node: 6m44.762s
* salloc --ntasks=1 failes w/ out of memory
* salloc --cpus-per-task=2 --mem-per-cpu=4000m: 5m46.079s
* salloc --cpus-per-task=1 --mem-per-cpu=512m: 6m0.658s
* salloc --cpus-per-task=1 --mem-per-cpu=1024m: 5m47.186s
Figured out how to read MOHID HDF5 files; funky nested group structure that xarray can't handle, byt h5netcdf can.
Updated MOHID to rev 24d9c4061751 and fixed missing line continuation bug that Rachael found at Software/MOHIDWater/ModuleHydrodynamic.F90:29905; compile time in interactive job dropped to 3m17.187s,
Started pull request re missing continuation.
(MIDOSS)

SalishSeaCast team mtg; see whiteboard.
Fixed mysteriously symlinked LiveOcean files on salish: 6-7aug18, 18sep18, 08oct18.
(SalishSea)


Wed 24-Oct-2018
^^^^^^^^^^^^^^^

See project work journal.
(GOMSS)

See project journal.
(SalishSeaCast-FVCOM)

Sent email to Bob Simons @ NOAA re: pathRegex tag issue that is preventing use from having most_recent_forecast datasets on ERDDAP; got a reply that resolved the issue (regex syntax is hard :-).
Changed ww3 and fvcom ERDDAP files datasets to show only nowcast/ and most_recent_forecast/.
Started refactoring update_forecast_datasets to symlink most recent forecast results from vhfr and wwatch3 into most_recent_forecast/ dirs.
(SalishSea)


Thu 25-Oct-2018
^^^^^^^^^^^^^^^

download_weather 06 failed; re-ran manually at ~09:20 to restart automation.
Finished refactoring update_forecast_datasets to symlink most recent forecast results from vhfr and wwatch3 into most_recent_forecast/ dirs; deployed and tested it with manual runs.
(SalishSea)

See project work journal.
(GOMSS)

See project journal.
(SalishSeaCast-FVCOM)


Fri 26-Oct-2018
^^^^^^^^^^^^^^^

MIDOSS project mtg; debrief from stakeholders workshop.
Worked w/ Rachael on Mercurial and MOHID.
Reproduced MOHID 25m_deep tank run in project/MIDOSS/runs/:
* rsync -rv ../MOHID/Solutions/mohid-in-linux/test/mohidwater/25m_deep ./
* cd 25m_deep
* rm -rf res
* cd exe
* ln -s ../../../MOHID/Solutions/mohid-in-linux/bin/MohidWater.exe
* ./MohidWater.exe
None of the keywords in nomfich.dat have definitions in the keyword dict wiki :-(
Successfully commented out the LIFE_DATA keyword in nomfich.dat.
Successfully commented out the ROOT_SRT keyword in nomfich.dat.
Successfully commented out the AIRW_FIN keyword in nomfich.dat.
Successfully commented out the BOT_HDF keyword in nomfich.dat.
Successfully commented out the BOT_FIN keyword in nomfich.dat.
Successfully commented out the OUT_DESF keyword in nomfich.dat, but got no Hydrodynamic.hdf file.
Successfully commented out the OUT_FIN keyword in nomfich.dat.
Successfully commented out the EUL_HDF keyword in nomfich.dat.
Successfully commented out the EUL_FIN keyword in nomfich.dat.
Run seems unaffected by removal of data/Nomfich.dat.
Following data/ files are empty:
* Atmosphere_1.dat
* FreeVerticalMovement_1.dat
* WaterProperties_1.dat
but the only one whose keyword can successfully commented out of nomfish.dat is FREE_DAT.
Edited nomfich.dat to set IN_BATIM value to ../grid/Tanque_25m.dat, moved files from GeneralData/geometry/ to new grid/, and ran successfully.
Commenting SURF_HDF, or AIRW_HDF out of nomfich.dat causes segfault.
(MIDOSS)

See project journal.
(SalishSeaCast-FVCOM)

Email from Michael Thorne at ONC requesting that we change our API requests from dmas.uvic.ca to data.oceannetworks.ca; discovered that the latter supports HTTPS :-); updated salishsea_tools.data_tools accordingly.
(SalishSea)


Sat 27-Oct-2018
^^^^^^^^^^^^^^^

Vancouver to Yokohama


Sun 28-Oct-2018
^^^^^^^^^^^^^^^

Vancouver to Yokohama


Week 44
-------

Mon 29-Oct-2018
^^^^^^^^^^^^^^^

Yokohama

Reviewed 2019 RAC application; worked on storage request.
(MOAD)


Tue 30-Oct-2018
^^^^^^^^^^^^^^^

Yokohama

Email from Michael@ONC re: dmas domain, my Fri change doesn't appear to have taken effect; updated tools on skookum from e7646d07561c to 2dd9855e4568 to resolve (doh!).
Refactored SalishSeaNowcast prod_config test fixture into tests/conftest.py module.
(SalishSea)

Continued work on RAC storage:
* nowcast-green/SalishSea_1h_*_grid_[TUVW].nc and Slab_*.nc are 1.7Gb/day;
  ww3 is 420Mb/day; vhfr is 805Mb/day; those should be what are needed to force MOHID
(MOAD)

Attended Susan's plenary on SOG-bloomcast at PICES meeting.

Set up MIDOSS/analysis-doug repo.
Started MOHID-hdf5Files notebook to explore Lagrangian files from Shihan, and PyNIO, h5netcdf, and h5py libraries.
(MIDOSS)


Wed 31-Oct-2018
^^^^^^^^^^^^^^^

Yokohama

Discussed 2019 RAC application w/ Susan; continued work on storage request.
(MOAD)

Finished MOHID-hdf5Files notebook exploring Lagrangian files from Shihan; added PyTables library; it provides a Pythonic object interface.
Discussed Lagrangian file structure w/ Susan; Eulerian snapshots by particle, and by 2D and 3D model grid cell.
Next step is transformation into xarray dataset; worked out most of the details in MOHID-HDF5-to-xarray notebook.
(MIDOSS)


Thu 1-Nov-2018
^^^^^^^^^^^^^^

Yokohama

See project journal.
(SalishSeaCast-FVCOM)


Fri 2-Nov-2018
^^^^^^^^^^^^^^

Yokohama

See project journal.
(SalishSeaCast-FVCOM)

Steered Rachael toward numpy ufuncs instead of looping over arrays.
Finished MOHID-HDF5-to-xarray notebook.
Started dev of moad_tools.midoss.hdf5_to_xarray().
(MIDOSS)

See project work journal.
(Resilient-C)

Discovered that make_plots fvcom publish is inifini-looping; updated skookum back to 6661ed2e2d20.
download_weather 18 failed; re-ran manually at ~19:15.
(SalishSea)

See project work journal.
(GOMSS)


Sat 3-Nov-2018
^^^^^^^^^^^^^^

Yokohama

Continued dev of moad_tools.midoss.hdf5_to_xarray(); realized that it will have to be hdf5_to_netcdf() because (168, 40, 898, 398) arrays consume a lot of memory...
(MIDOSS)

make_forcing_links orcinus nowcast+ failed due to ssh-agent issue, causing nowcast-agrif run to not run
(SalishSea)


Sun 4-Nov-2018
^^^^^^^^^^^^^^

Yokohama to Vancouver

Ran nowcast-agrif 2018-11-03 manually.
(SalishSea)


Week 45
-------

Mon 5-Nov-2018
^^^^^^^^^^^^^^

Wrote storage section of RAC proposal.
(MOAD)

Backfilled nowcast-agrif:
* make_forcing_links nowcast-agrif 2018-11-04
* make_forcing_links nowcast-agrif 2018-11-05
(SalishSea)


Tue 6-Nov-2018
^^^^^^^^^^^^^^

Continued dev of moad_tools.midoss.hdf5_to_netcdf4().
(MIDOSS)

SalishSeaCast mtg; see whiteboard.
(SalishSea)


Wed 7-Nov-2018
^^^^^^^^^^^^^^

Updated conda base env on kudu to Python 3.7; still can't create Python 3.7 conda envs in PyCharm.

Updated Mercurial on kudu to 4.8rc0+2-7b48c616431d:
* conda activate hg-dev
* cd hg-stable
* hg pull -u
* make clean all
* sudo make install PYTHON=/media/doug/warehouse/conda_envs/hg-dev/bin/python2.7

Pulled VHFR water levels figure residuals panel patch from niko backup drive via borg mount because I forgot to upload it to skookum yesterday.

See project journal.
(SalishSeaCast-FVCOM)

See project work journal.
(GOMSS)

Worked on revising technical section of RAC proposal to reduce it to 4 pages.
(MOAD)

Updated skookum back to tip, and tested next_workers that launches previous day's make_plots fvcom workers after ping_erddap.
Fielded emails from Johannes about wwatch3 change to nowcast + forecast.
Helped elise w/ setgid bit issue on cedar; pretty sure now that it's new file system behaviour, not my stupidity as Ali implied.
(SalishSea)


Thu 8-Nov-2018
^^^^^^^^^^^^^^

See project work journal.
(GOMSS)

Manually ran get_vfpa_hadcp 2018-11-07 at ~09:00 to test the idea of running it early in the morning to avoid gaps; solves gap issue, but after_ping_erddap blew up because there is not FVCOM run in the checklist to use to launch make_plots... sigh...
(SalishSea)

See project journal.
(SalishSeaCast-FVCOM)

Reviewed and revised RAC proposal.
(MOAD)

Added exception handling so that get_vfpa_hadcp can ping ERDDAP without launching make_plots fvcom before there are run results to plot.
Added launch of get_vfpa_hadcp for previous UTC day after download_weather 06 to ensure that dataset is complete for previous UTC day.
(SalishSea)


Fri 9-Nov-2018
^^^^^^^^^^^^^^

Vancouver to Toronto.

Worked on refactoring unit tests to use YAML-based nowcast.Config objects.
(SalishSea)

See project work journal.
(GOMSS)


Sat 10-Nov-2018
^^^^^^^^^^^^^^^

PyCon Canada


Sun 11-Nov-2018
^^^^^^^^^^^^^^^

PyCon Canada

Change sequencing so that upload_forcing is launched after make_live_ocean_files instead of grib_to_netcdf because the LiveOcen grid is finer now, and we are using gsw in Python instead of spawning matlab processes.
(SalishSea)


Week 46
-------

Mon 12-Nov-2018
^^^^^^^^^^^^^^^

PyCon Canada Sprints

Worked on pandas docs:
* pull request to fix dev env setup instructions in python-sprints repo; merged
* pull request to improve message for double line breaks in pandas validate_docstrings.py script; awaiting merge
* pull request to fix double line break occurrences flagged by validate_docstrings script; reviewed and approved, told to put additional work in a new PR

See project work journal.
(GOMSS)

See project journal.
(Resilient-C)


Tue 13-Nov-2018
^^^^^^^^^^^^^^^

See project work journal.
(GOMSS)

PyCon Canada Sprints

Worked on pandas docs:
* added unit tests to PR improve message for double line breaks in pandas validate_docstrings.py script; review asked for changes in tests
* branch for pull request to fix more double line break occurrences flagged by validate_docstrings script; got all but 2 fixed, and reviewer says that's fine because the 2 are deprecated methods that will soon disappear


Wed 14-Nov-2018
^^^^^^^^^^^^^^^

Brampton

PyCon Canada Sprints

Worked on pandas docs:
* 1st pull request to fix double line break occurrences flagged by validate_docstrings script; merged
* 2nd pull request to fix the rest of the double line break occurrences flagged by validate_docstrings script; approved, resolved a merge conflict, merged

Answered Rachael's questions about wave fields, whitecap coverage, and accessing NEMO fields via ERDDAP.
(MIDOSS)

Started refactoring units tests YAML-based nowcast.Config object elements required by all unit tests into a conftest.py fixture and making unit test config fixtures either provide or augment the base config.
Commented out re-generation of day-1 VHFR figures after ping_erddap to see if that resolves the weird KeyError or MissingDimensionsError exceptions.
More email with Johannes about wwatch3 change to nowcast + forecast.
(SalishSea)


Thu 15-Nov-2018
^^^^^^^^^^^^^^^

Brampton-Barrie-Brampton

ecget river flow failed w/ SSL verification error:
* manually persisted 13nov18 values for Fraser and Englishman
* make_runoff_file --debug
* upload_forcing west.cloud-nowcast
* upload_forcing orcinus-nowcast-agrif
* upload_forcing cedar-hindcast
(SalishSea)


Fri 16-Nov-2018
^^^^^^^^^^^^^^^

Brampton to Vancouver

ecget river flow failed w/ SSL verification error:
* replaced ecget env:
  * conda env remove -n ecget
  * conda create -p /home/dlatorne/miniconda3/envs/ecget -c conda-forge -c defaults arrow beautifulsoup4 cliff kombu python=3.7 requests
* ecget river flow still fails, but the error message is more informative:
  * HTTPSConnectionPool(host='wateroffice.ec.gc.ca', port=443): Max retries exceeded with url: /report/real_time_e.html?mode=Table&type=realTime&prm1=47&prm2=-1&stn=08MF005&startDate=2018-11-15&endDate=2018-11-16 (Caused by SSLError(SSLError("bad handshake: Error([('SSL routines', 'ssl3_get_server_certificate', 'certificate verify failed')])")))
* which lead me to suspect that this was triggered by wateroffice forcing HTPP to HTTPS redirect and a certificate chain issue, based on discussion in https://github.com/requests/requests/issues/3212
* re-produced the issue on niko
* manually persisted 13nov18 values for Fraser and Englishman
* make_runoff_file --debug
* upload_forcing west.cloud-nowcast
* upload_forcing orcinus-nowcast-agrif
* upload_forcing cedar-hindcast
Continued refactoring unit tests to use YAML-based nowcast.Config objects.
(SalishSea)


Sat 17-Nov-2018
^^^^^^^^^^^^^^^

Susan handled make_runoff_file failure by patching Fraser and Englishman files w/ values eyeballed from wateroffice web site plots.
Continued refactoring unit tests to use YAML-based nowcast.Config objects.
watch_ww3 failed w/ unable to logging pub port error:
* found and killed zombie watch_ww3 worker on west.cloud from 08nov18
* for d in {08..16}; download_wwatch3_results nowcast 2018-11-$d --debug
* discovered that there were no forecast runs for 08..16nov
* for d in {09..16}; download_wwatch3_results forecast2 2018-11-$d --debug

Discussed design for workers concurrency that can handle race conditions w/ Susan:
* implementation in nemo_nowcast
* add --concurrent flag to NowcastWorker
  * workers that are being executed concurrently include concurrent=True in their completion message
* add ConcurrentWorkers class
  * accept list of NextWorker instances
  * workers are launched with --concurrent option
  * polls worker pids until all have finished; implies that NextWorker.launch returns pid, and that workers can only run on same host as ConcurrentWorkers instance
  * has a message type for each possible collection of concurrent workers; implies a run_type-like command-line arg
* after_* functions for possibly concurrent workers short-circuit out with empty next_workers list if concurrent==True in message payload
* after_concurrent_workers produces list of NextWorker instances; after_* functions for possibly concurrent workers can still produce NextWorker lists so that they can be run independently to deal with automation failures
* also need a SequencedWorkers worker that can be used to run a sequence of workers (e.g. download_live_ocean, then make_live_ocean_files) within a concurrent workers collection
  * workers are launched with --concurrent option
(SalishSea)

Discussed way forward on MOHID w/ Susan and Rachael re: Rachael's visit to Dal:
* get a usable hdf5_to_netcdf4 tool working
* switch to using MOHID version that Rachael brought back with her; put it in a private hg repo on Bitbucket
(MIDOSS)


Sun 18-Nov-2018
^^^^^^^^^^^^^^^

Finished pandas PR #23649 by moving extra linebreak tests into test_bad_examples() per review; appear to have inherited a broken test from upstream, but assuming that's and env issue or SEP.

SalishSeaCast was delayed due to power outage in EOSM that took away auth service from ~04:15 to ~16:00; Susan had to manually hack get_NeahBay_ssh and the text file that it generated from the web in order to get forecast2 to launch; in response I formalized her get_NeahBay_ssh hack by adding a --text-file command-line option to easy handling of this situation in the future.
(SalishSea)


Week 47
-------

Mon 19-Nov-2018
^^^^^^^^^^^^^^^

Reverted yesterday commit in pandas PR #23649 because review says that test_bad_examples() is for testing the Examples section of docstring (as I thought when I first started work on this). Renamed test_bad_examples() to test_bad_docstrings() and moved extra linebreaks tests back into test_bad_docstrings() parametrize decorator.

Tried to figure out Susan's Jupyter kernel crash from xarray.open_dataset() issue.
Worked on debugging ecget river flow issue on salish. Discussed it with Charles who thinks its a wateroffice server config issue. Discovered that it workds on niko with a wired connection, but not wifi. Hacked ecget.river on salish to skip certs verification.
Investigated EC datamart hydrometric files; csv files containig day-1 and day, Fraser is 5min frequency and lags real-time by at least 90min.
(SalishSea)

Instrumented hdf5_to_netcdf4 and found that it takes ~40s per model hr at hr 8, and ~60s at hr 14, so expect >=30min for 24 model hrs.
Changed to int32 storage with 1e-4 scale factor and got ~x2 speed up.
(MIDOSS)


Tue 20-Nov-2018
^^^^^^^^^^^^^^^

SalishSeaCast team mtg; see whiteboard.
Read anaconda blog post about Python visualization and explored PyViz, HoloViews, GeoViews.
Skimmed StromSurgeBC almanac and tried to print calendar pages.
Added with suppress(urllib3.exception.InsecureRequestWarning) to ecget.river to silence cron job email messages.
Email to Parker about SSL issue in ecget river flow; he's not having trouble!
(SalishSea)

Changed hdf5_to_netcdf4 to store time step files that get concatenated using ncrcat; sped up to ~3.5s/hr; conversion of 7d file with deflation took 532s; send file to Rachael for testing.
Changed instrumentation to decorators; too cool for school!!!
(MIDOSS)


Wed 21-Nov-2018
^^^^^^^^^^^^^^^

suppress(urllib3.exception.InsecureRequestWarning) in ecget.river doesn't silence cron job email messages.
Changed tide prediction vs. max ssh figure to use best location for legend in residuals panel.
Changed SalishSeaNowcast to use black-18.9b0 from conda-forge.
(SalishSea)

See project work journal.
(GOMSS)


Thu 22-Nov-2018
^^^^^^^^^^^^^^^


See project work journal.
(GOMSS)

Added __contains__() method to nemo_nowcast.Config object so that membership tests work at top level.
Added production config YAML unit tests to grib_to_netcdf.
Reviewed and merged SalishSeaNowcast PR#2 from Michael.
(SalishSea)

See project journal.
(SalishSeaCast-FVCOM)


Fri 23-Nov-2018
^^^^^^^^^^^^^^^

See project journal.
(SalishSeaCast-FVCOM)

See project journal.
(Resilient-C)

nowcast-dev/22nov18 got stuck at 35.4% complete; only xios left running, killed it at ~08:45.
ecget river flow failed with parsing issue; it appears that the site has change to now force a secondary y-axis variable which defaults to water temperature; added handling to ecget.river; also changed wateroffice URL there to HTTPS.
Too late to run foreacst2/22nov18.
Manually ran clear_checklist.
Changed next_workers to run make_live_ocean_files on skookum instead of salish because it no longer required Matlab.
(SalishSea)


Sat 24-Nov-2018
^^^^^^^^^^^^^^^

Vancouver to Parksville

ecget river flow Fraser failed w/ string parsing error, so upload_forcing forecast2 failed; recovery:
* ecget river flow Fraser worked fine when I ran it manually at ~07:00
* make_runoff_file
* upload_forcing west.cloud
* upload_forcing orcinus
* upload_forcing cedar failed due to connection reset
Made spec-ed mock of NowcastWorker consistent in SalishSeaNowcast unit tests.
Added blacken file external command to niko PyCharm with Ctrl+Alt+L keyboard mapping.
(SalishSea)

See project work journal.
(GOMSS)


Sun 25-Nov-2018
^^^^^^^^^^^^^^^

Parksville to North Saanich

Continued dev of hdf5_to_netcdf4 module.
(MIDOSS)


Week 48
-------

Mon 26-Nov-2018
^^^^^^^^^^^^^^^

Debby & Paul's

Finished initial dev of hdf5_to_netcdf4 module.
(MIDOSS)


Tue 27-Nov-2018
^^^^^^^^^^^^^^^

IOS

CIOPS-W (NEP36) preview mtg; see notebook.

See project journal.
(Resilient-C)


Wed 28-Nov-2018
^^^^^^^^^^^^^^^

IOS, then North Saanich to home

CIOPS-W (NEP36) preview mtg; see notebook.
Sent email to J-P re: access to SalishSeaCast fields for re-initialization of Salish Sea region of CIOPS-W to remove deep salinity bias.

Added autospec (and in a few cases, spec) args to patch decorators in SalishSeaNowcast unit tests.
(SalishSea)


Thu 29-Nov-2018
^^^^^^^^^^^^^^^

See project work journal.
(GOMSS)

See project journal.
(SalishSeaCast-FVCOM)

make_plots nemo forecast failed due to network error from WSDL service; re-ran manually.
(SalishSea)


Fri 30-Nov-2018
^^^^^^^^^^^^^^^

See project journal.
(SalishSeaCast-FVCOM)

See project work journal.
(GOMSS)


Sat 1-Dec-2018
^^^^^^^^^^^^^^

See project journal.
(SalishSeaCast-FVCOM)

Shopped for ingredients for fruit cake and mincemeat, and prepped them.


Sun 2-Dec-2018
^^^^^^^^^^^^^^

ecget river flow for Fraser failed with ValueError on str to float conversion; didn't get it resolved in time for preliminary forecast runs; that meant that the checklist didn't get cleared, which caused make_live_ocean_files to run for 2018-12-01 instead of today because it gets it run date from the 0th item in the download_live_ocean checklist; recovery:
* debugged and improved ECget (see below)
* ecget river flow >> Fraser_flow
* make_runoff_file
* upload_forcing to restart automation
Fixed make_live_ocean_files run date bug by changing to last item in download_live_ocean checklist.
Installed poppler from conda-forge into SSN production env to provide pdftocairo for make_surface_current_tiles worker.
(SalishSea)

Forced river data table to include water level as 2nd data column so that datetimes for which there is no water level (from which discharge is calculated) will not appear in table.
(ECget)

Researched pip-tools to automate maintenance of requirements.txt files; I would need to add a tool to generate a requirements.in file from environment-dev.yaml; started playing with the idea in the gomss-site repo.


December
========

Week 49
-------

Mon 3-Dec-2018
^^^^^^^^^^^^^^

make_surface_current_tiles forecast2 ran successfully in automation; restarted manager to update it's message registry entry.
(SalishSea)

Tried to set up my own copy of Dal version of MOHID sources tree from what Rachael uploaded after he trip last month, but most of the directories are empty :-( Sent email to Rachael.
Resumed experiments from 26-Oct-2018 re: MOHID 25m_deep test run directory structure:
* MohidWater.exe and nomfich.dat *must* be in the same dir, but don't have to be in exe/; ran successfully with them in 25m_deep/
* successfully used an absolute path for IN_BATIM in nomfich.dat
* ROOT must be present and have a value, but no matter what it is the Hydrodynamic_1.hdf5 file goes into res/
* successfully used an absolute path for IN_MODEL in nomfich.dat, and moved the Model_1.dat file from 25m_deep/data/ to 25m_deep/
* successfully ran with IN_BATIM path set to a symlink
Started dev of MOHID-Cmd package.
(MIDOSS)


Tue 4-Dec-2018
^^^^^^^^^^^^^^

ecget Fraser did the Heisen-bug thing again; ran it, make_runoff_file, and upload_forcing forecast2 x3 to restart automation.
SalishSeaCast team mtg; see whiteboard.
Committed nowcast-green XIOS buffer size factor change that has been in effect for weeks on west.cloud.
(SalishSea)

Helped Saurav resolve TLS deprecation issue on Bitucket; he needs to use ssh keys.

Got MIDOSS-MOHID from Shihan via Rachael built on cedar by hacking on compile_mohid.sh pulled in from Github version.
Got Shihan's constant temperature & salinity, no w velocity, etc. test case from Oct running on cedar; took 35m28s on 12 cores in an interactive session with slow-ish file system.
(MIDOSS)


Wed 5-Dec-2018
^^^^^^^^^^^^^^

Coached Rachael on setup of MOAD repo for bibtex file(s).

Updated west.cloud SS-run-sets from 2017:213385520eef with changesets 1dd628ea1d28:73e283f98c61.
Wrote background email to Susan about rpn to netcdf conversion for 2007-2014 GEMLAM files; dug around in browser history to find http://collaboration.cmc.ec.gc.ca/science/rpn.comm/wiki/doku.php?id=virtual_machine:how_it_was_done (science, science)
(SalishSea)

See project journal.
(SalishSeaCast-FVCOM)


Thu 6-Dec-2018
^^^^^^^^^^^^^^

Added checklist to make_surface_current_tiles.
Improved download_results handling of FVCOM boundary slab files; added unlinking of FVCOM_W.nc file, and suppressed unlinking of all from hindcast runs so that we have them available for VHFR hindcast.
(SalishSea)

Started experimenting with sbatch runs of MOHID on cedar:
* created mohid.sh script
* removed OPENMP_NUM_THREADS from Model.dat in favour of:
  * #SBATCH --cpus-per-task=32
  * export OMP_NUM_THREADS=$SLURM_CPUS_PER_TASK
  so that mohid.sh cpus-per-task directive controls run
* with 32 cores, default 256M mem-per-cpu is too small; 512M allows execution, and seff says that it used 10.69G and has 66.82% memory efficiency
* 8 cores w/ 512M failed
* 8 cores w/ 1500M (based on 12G / 8) works w/ 91.17% memory efficiency
* 16 cores w/ 750M works with 90.33% memory efficiency
Continued dev of MOHID-Cmd package.
(MIDOSS)

Completed PD expense claim for PyCon Canada trip.
Opened ticket to request monitors, keyboard & mouse for smelt for Rachael in January.


Fri 7-Dec-2018
^^^^^^^^^^^^^^

Email from Ali suggests that cedar file system has returned to stability for now, so more experimenting with sbatch runs of MOHID on cedar:
* 16 cores w/ 750M works, seff report for 5min run makes no sense; full run 35m12s, 93.01% memory efficiency, 54.00% cpu efficiency
* 32 cores w/ 750M, 35m13s, 46.64% memory efficiency, 53.18% cpu efficiency
* 12 cores w/ 1000M, 40m7s, 92.32% memory efficiency, 53.32% cpu efficiency
* 8 cores w/ 1500M, 43m58s, 92.23% memory efficiency, 55.41% cpu efficiency
* 4 cores w/ 3000M, 44m4s, 92.02% memory efficiency, 64.80% cpu efficiency
(MIDOSS)

Updated Mercurial on kudu to 4.8.1+2-47719d7c581f:
* conda activate hg-dev
* cd hg-stable
* hg pull -u
* make clean all
* sudo make install PYTHON=/media/doug/warehouse/conda_envs/hg-dev/bin/python2.7

See project journal.
(SalishSeaCast-FVCOM)

Updated repos on skookum and west.cloud:
* FVCOM-VHFR-config
* OPPTools
(SalishSea)


Sat 8-Dec-2018
^^^^^^^^^^^^^^

Renewed EGBC membership; declared 100 hr of PD:
* 50h professional practice
* 30h informal
* 20h presentations

Created 2019 gnucash file via export accts to sqlite3 that made empty file, then exported accounts to csv and imported them, then transcribed jan/feb transactions to initialize accounts and set up scheduled transactions.

Continued MOHID scaling tests on cedar:
* 2 cores w/ 6000M, 53m41s, 93.20% memory efficiency, 76.33% cpu efficiency
(MIDOSS)


Sun 9-Dec-2018
^^^^^^^^^^^^^^

ecget river flow Fraser failed w/ ValueError on empty string to float in automation at ~03:06:
* ecget river flow Fraser ran fine manually at ~10:00
* make_runoff_file
* upload_forcing west.cloud --debug to avoid triggering forecast2 runs
* upload_forcing orcinus-nowcast-agrif
* upload_forcing cedar-hindcast
* clean_checklist
Researched AMQP file access from datamart:
* recommended tool is https://github.com/MetPX/sarracenia
* dependencies from setup.py:
  * amqplib pypi
  * appdirs conda
  * watchdog conda
  * netifaces conda
  * humanize conda
  * psutil conda
* conda create -n sarracenia python=3 appdirs watchdog netifaces humanize psutil
* pip install amqplib metpx-sarracenia
* failed due to missing paramiko dependency; created https://github.com/MetPX/sarracenia/issues/123
* several working experiments in kudu:/media/doug/warehouse/MEOPAR/sarracenia-test/
* note that amqp fork of amqplib probably won't work because sarracenia uses import amqplib.client_0_8 as amqp
(SalishSea)

Continued MOHID scaling tests on cedar:
* 1 core w/ 12000M, 1h3m55s, 93.03% memory efficiency, 94.24% cpu efficiency
* 1 core w/ 11800M, 1h4m20s, 94.59% memory efficiency, 98.91% cpu efficiency
(MIDOSS)

Worked on copying shared storage from matisse RAID to lizzy:
* confirmed that all of finances/ has been copied
* created matisse:moved_to_lizzy/
* moved matisse:finances to moved_to_lizzy/
* copied matisse:manuals to lizzy; moved matisse:manuals to moved_to_lizzy/
* copied matisse:lulu_www to lizzy; moved matisse:lulu_www to moved_to_lizzy/
* copied matisse:CT_Data to lizzy; moved matisse:CT_Data to moved_to_lizzy/
* copied matisse:ebooks to lizzy; moved matisse:ebooks to moved_to_lizzy/
* copied matisse:lists to lizzy; moved matisse:lists to moved_to_lizzy/
* copied matisse:hg to lizzy; moved matisse:hg to moved_to_lizzy/
* copied matisse:cycling to lizzy; moved matisse:cycling to moved_to_lizzy/


Week 50
-------

Mon 10-Dec-2018
^^^^^^^^^^^^^^^

Continued dev of MOHID-Cmd package; started prepare sub-command.
(MIDOSS)

Nick of Rich gave Phys Ocgy seminar about electrical potential effects in double diffusion and pH meter liquid junctions.

nowcast-agrif failed due to missing time step in 09dec18/restart_trc file; suspect disk quota issue on orcinus; cleared out runs and YAML files >15d old and set up crontab to do that daily; backfilling:
* make_forcing_links nowcast-agrif 2018-12-09
* make_forcing_links nowcast-agrif 2018-12-10
* make_forcing_links nowcast-agrif 2018-12-11
* make_forcing_links nowcast-agrif 2018-12-12
(SalishSea)


Tue 11-Dec-2018
^^^^^^^^^^^^^^^

Updated Mercurial on kudu to 44.8.1+3-4265bfb53dd3:
* conda activate hg-dev
* cd hg-stable
* hg pull -u
* make clean all
* sudo make install PYTHON=/media/doug/warehouse/conda_envs/hg-dev/bin/python2.7

Continued dev of MOHID-Cmd package.
(MIDOSS)

SalishSeaCast team mtg; see whiteboard.
download_live_ocean failed:
* used symlink created during forecast2 to presist 10dec18 as 11dec18
* upload_forcing west.cloud-nowcast nowcast+
* upload_forcing orcinus-nowcast-agrif nowcast+
* upload_forcing cedar-hindcast nowcast+
Sent email to Roman about memory allocation issue on orcinus re: nowcast-agrif.
Worked on improving SalishSeaNowcast release_mgmt.tag_release to avoid tagging commits from hg tag operations and instead tag the last substantive changeset.
Helped Susan with build issues on cedar, mostly caused by admins messing with the module system.
(SalishSea)


Wed 12-Dec-2018
^^^^^^^^^^^^^^^

Email w/ Rachael re: loading netCDF files locally vs. from OPenDAP services.
(MIDOSS)

See project journal.
(Resilient-C)

Did nowcast-agrif recovery w/ Roman's help.
(SalishSea)


Thu 13-Dec-2018
^^^^^^^^^^^^^^^

Email to CIRA re: separate registration of randonneurs.ca domain.

See project journal.
(Resilient-C)

Noticed that log did not roll; investigation showed that watch_NEMO nowcast-green 12dec18 on west.cloud went catatonic; recovery:
* kill catatonic watch_NEMO on west.cloud
* restarted log_aggregator on skookum
* used launch_remote_worker to launch watch_NEMO nowcast 13dec18 on west.cloud
* discovered that I forgot to add nest_workers.after_launch_remote_worker
* download_results nowcast-green 2018-12-12 --debug
* make_plots nemo nowcast-green research 2018-12-12
* launch_remote_worker "make_ww3_wind_file --run-date 2018-12-12 --debug"
* launch_remote_worker "make_ww3_current_file --run-date 2018-12-12 --debug"
* launch_remote_worker "run_ww3 nowcast --run-date 2018-12-12"
* launch_remote_worker "make_ww3_wind_file --run-date 2018-12-13"
* launch_remote_worker "make_ww3_current_file --run-date 2018-12-13"
* mkdir nowcast-dev/12dev18
* cp nowcast-blue/12dec18/namelist_cfg nowcast-dev/12dec18/
* make_forcing_links salishsea-nowcast nowcast+ --shared-storage
Updated SalishSeaNowcast on west.cloud from 1679:2a87e4b1e1d1 to 1789:edb54837c379 to facilitate testing vhfr_x2 baroclinic branch.
Updated OPPTools on west.cloud.
(SalishSea)

Added --no-verify-ssl-certs option to RiverFlow plug-in:
* Don't verify SSL certificates chain for requests to https://wateroffice.ec.gc.ca/.
* Also suppress InsecureRequestWarning warnings from urllib3 vendored in the requests package.
* This is a hack to reduce the noise from cron jobs on some systems that have problems with the Nov-2018 forced redirection to https://wateroffice.ec.gc.ca/.
* Defaults to False.
(ECget)

See project journal.
(SalishSeaCast-FVCOM)

salishsea-site went down at ~14:46
Restarted web app but it made no difference, as ususal; killed and relaunched circus daemon and site came back at ~17:00.
(salishsea-site)

Discussed MOHID results viz from Shihan's Oct case w/ Rachael and Susan.
Sent email to Shihan re: VCS for MIDOSS-MOHID code.
Continued MOHID scaling tests on cedar:
* 1 core w/ 11800M, 52m40s, 94.58% memory efficiency, 98.86% cpu efficiency
(MIDOSS)


Fri 14-Dec-2018
^^^^^^^^^^^^^^^

Email w/ Shihan about Mercurial; added him to MOAD team.
Email to Bitbucket requesting academic license for MIDOSS team.
Tried to run hdf5-to-netcdf4 on salish to convert Oct Lagrangian file and it fails w/ out of disk space error on /tmp/; switched to smelt and got success, but it took ~30min and produced at 110M file instead of 26M from niko.
Experimented with hdf5-to-netcdf4 set to not use scaled int storage for field values; no difference to plots in Susan's notebook.
Added hdf5-to-netcdf4 --verbose option to control logging output from CLI.
(MIDOSS)

west.cloud sufferred a network connectivity issue, but automation handled it more or less cleanly.
nowcast-green output files were 1h short; suspect ongoing memory leak on VMs, reduced XIOS buffer size factor from 0.08 to 0.75 and successfully repeated run.
(SalishSea)

Change from HTTP HEAD to Path.exists() to detect figure availability; big speed-up for calendar grids and figure pages.
(salishsea-site)

See project journal.
(SalishSeaCast-FVCOM)


Sat 15-Dec-2018
^^^^^^^^^^^^^^^

See project journal.
(SalishSeaCast-FVCOM)


Finished improving SalishSeaNowcast release_mgmt.tag_release to avoid tagging commits from hg tag operations and instead tag the last substantive changeset.
Helped Susan with alternate combine/deflate strategies for hindcast runs on cedar.
Updated OPPTools on skookum to enable vh_x2_baroclinic branch make_fvcom_atmos_forcing to work:
* got 1ca87ca..6c784a4
* did make_fvcom_atmos_forcing
* git checkout 1ca87ca  # to get back to production state; detached HEAD
* git checkout master should get me back
(SalishSea)

See project journal.
(SalishSeaCast-FVCOM)


Sun 16-Dec-2018
^^^^^^^^^^^^^^^

Forwarded CIRA response re: randonneurs.ca to Cheryl with my opinion that that domain is lost to time.

Helped Susan sort through tagging PROD-nowcast-dev-201806.
forecast/16dec18 got stuck at 84.7% due to a file length issue in atmos forcing; upload_forcing nowcast+ got triggered before grib_to_netcdf finished due to race conditions between grib_to_netcdf and make_live_ocean_files.
(SalishSea)


Week 51
-------

Mon 17-Dec-2018
^^^^^^^^^^^^^^^

Added installation of moad_tools and MOHID-Cmd to MOHID on cedar docs.
Installed moad_tools and MOHID-Cmd in my --user space on cedar.
Tested hdf5-to-netcdf4 on cedar in salloc interactive sessions:
* salloc w/ default 256m memory failed
* salloc w/ 4000m memory failed
* salloc w/ 8000m memory failed
* salloc w/ 12000m memory failed
* salloc w/ 16000m memory failed
* salloc w/ 20000m memory with default TMPDIR (/tmp/) succeeded 6m20.766s
* salloc w/ 20000m memory with TMPDIR=$SLURM_TMPDIR (/localscratch/) succeeded 6m26.409s
Need to add module load nco/4.6.6 to docs.
Need to figure out how to make hdf5-to-netcdf4 use less memory; maybe don't hold hdf5 file open via context manager
Created MIDOSS-MOHID code repo and populated it with code from Shihan; worked on streamlining compile_mohid.sh script to include only what we need.
(MIDOSS)


Tue 18-Dec-2018
^^^^^^^^^^^^^^^

ecget river flow Fraser and Englishman failed w/ ValueError on empty string to float in automation at ~03:06 and ~03:12:
* ecget river flow Fraser ran fine manually at ~07:20
* ecget river flow FraserEnglishman ran fine manually at ~07:20
* make_runoff_file
* upload_forcing west.cloud
* upload_forcing orcinus-nowcast-agrif
* upload_forcing cedar-hindcast
SalishSeaCast team mtg; see whiteboard
download_live_ocean failed:
* used symlink created during forecast2 to presist 17dec18 as 18dec18
* upload_forcing west.cloud-nowcast nowcast+
* upload_forcing orcinus-nowcast-agrif nowcast+
* upload_forcing cedar-hindcast nowcast+
Forgot that orcinus was down for cooling system maintenance, but Roman managed the nowcast-agrif run for us :-)
(SalishSea)

Finished streamlining compile_mohid.sh script to include only what we need; MIDOSS-MOHID repo is ready for use.
Continued dev of MOHID-Cmd package.
(MIDOSS)

Westgrid townhall:
* cyber-security presentation by Jonathan Ferland, Compute Canada Director of Information Security
* discussed cedar problems, but say that system is stable this week
* Webinars:
  * feb 20 memory debugging w/ valgrind
  * may 15 julia


Wed 19-Dec-2018
^^^^^^^^^^^^^^^

ecget river flow Fraser and Englishman failed w/ ValueError on empty string to float in automation at ~03:06 and ~03:12:
* ecget river flow Fraser ran fine manually at ~08:30
* ecget river flow FraserEnglishman ran fine manually at ~08:30
* make_runoff_file
* upload_forcing west.cloud
* upload_forcing orcinus-nowcast-agrif
* upload_forcing cedar-hindcast
Backfilled LiveOcean from 11dec18 and 18dec18:
* download_live_ocean 2018-12-11 --debug
* rm LiveOcean_v201712_y2018m12d11.nc symlink
* make_live_ocean_files 2018-12-11 --debug
* scp LiveOcean_v201712_y2018m12d11.nc west.cloud:/nemoShare/MEOPAR/LiveOcean/
* scp LiveOcean_v201712_y2018m12d11.nc cedar:project/SalishSea/forcing/LiveOcean/
* scp LiveOcean_v201712_y2018m12d11.nc graham:project/SalishSea/forcing/LiveOcean/
* scp LiveOcean_v201712_y2018m12d11.nc orcinus:/home/sallen/MEOPAR/LiveOcean/
* download_live_ocean 2018-12-18
* rm LiveOcean_v201712_y2018m12d18.nc symlink
* make_live_ocean_files 2018-12-18 --debug
* scp LiveOcean_v201712_y2018m12d18.nc west.cloud:/nemoShare/MEOPAR/LiveOcean/
* scp LiveOcean_v201712_y2018m12d18.nc cedar:project/SalishSea/forcing/LiveOcean/
* scp LiveOcean_v201712_y2018m12d18.nc graham:project/SalishSea/forcing/LiveOcean/
* scp LiveOcean_v201712_y2018m12d18.nc orcinus:/home/sallen/MEOPAR/LiveOcean/
Created sarracenia-env on skookum:
* conda create -c conda-forge -p /results/nowcast-sys/sarracenia-env python=3 appdirs watchdog netifaces humanize psutil paramiko
* source activate /results/nowcast-sys/sarracenia-env
* pip install amqplib metpx-sarracenia
* sr_subscribe edit credentials.conf  # initialize datamart credentials
* created /results/nowcast-sys/hydrometric.conf:  # temporary location
    broker amqps://anonymous@dd.weather.gc.ca
    subtopic hydrometric.csv.BC.hourly
    directory /results/forcing/rivers/datamart
    overwrite true
    # Englishman River at Parksville
    accept .*08HB002.*
    # Fraser River at Hope
    accept .*08MF005.*
* sr_subscribe start /results/nowcast-sys/hydrometric.conf  # initiate subscription
* sr_subscribe log /results/nowcast-sys/hydrometric.conf  # monitor for activity
* created /results/nowcast-sys/hrdps-west.conf:  # temporary location
    broker amqps://anonymous@dd.weather.gc.ca
    subtopic model_hrdps.west.grib2.#
    directory /results/forcing/atmospheric/GEM2.5/GRIB/datamart
    mirror true
    strip 4
    # u component of wind velocity at 10m elevation
    accept .*UGRD_TGL_10.*
    # v component of wind velocity at 10m elevation
    accept .*VGRD_TGL_10.*
    # accumulated downward shortwave (solar) radiation at ground level
    accept .*DSWRF_SFC_0.*
    # accumulated downward longwave (thermal) radiation at ground level
    accept .*DLWRF_SFC_0.*
    # upward surface latent heat flux (for VHFR FVCOM)
    accept .*LHTFL_SFC_0.*
    # air temperature at 2m elevation
    accept .*TMP_TGL_2.*
    # specific humidity at 2m elevation
    accept .*SPFH_TGL_2.*
    # relative humidity at 2m elevation (for VHFR FVCOM)
    accept .*RH_TGL_2.*
    # accumulated precipitation at ground level
    accept .*APCP_SFC_0.*
    # precipitation rate at ground level (for VHFR FVCOM)
    accept .*PRATE_SFC_0.*
    # atmospheric pressure at mean sea level
    accept .*PRMSL_MSL_0.*
    # total cloud in percent (for parametrization of radiation missing from 2007-2014 GRMLAM)
    accept .*TCDC_SFC_0.*
  would be nice to figure out how to reject 000/ directory
(SalishSea)

See project journal.
(SalishSeaCast-FVCOM)


Thu 20-Dec-2018
^^^^^^^^^^^^^^^

ecget river flow Fraser and Englishman failed w/ ValueError on empty string to float in automation at ~03:06 and ~03:12:
* ecget river flow Fraser ran fine manually at ~08:00
* ecget river flow FraserEnglishman ran fine manually at ~08:00
* make_runoff_file
* upload_forcing west.cloud
* upload_forcing orcinus-nowcast-agrif
* upload_forcing cedar-hindcast
Checked sarracenia mirror of HRDPS GRIB files; working as expected; added a directive to reject 000/ directory.
(SalishSea)

See project journal.
(SalishSeaCast-FVCOM)


Fri 21-Dec-2018
^^^^^^^^^^^^^^^

ecget river flow Fraser and Englishman failed w/ ValueError on empty string to float in automation at ~03:06 and ~03:12:
* ecget river flow Fraser ran fine manually at ~07:35
* ecget river flow FraserEnglishman ran fine manually at ~07:35
* make_runoff_file
* upload_forcing west.cloud
* upload_forcing orcinus-nowcast-agrif
* upload_forcing cedar-hindcast
Checked sarracenia mirror of HRDPS GRIB files; working as expected.
Worked w/ Susan on trying to get XIOS/NEMO working well again on cedar in light of mtg w/ Roman and 4dec18 mpi lib changes:
* XIOS-2 build fails with errors about ambiguity of shared_ptr in client.cpp
Updated salish:/results/nowcast-sys/ clones for PROD-nowcast-dev-201806:
********note: clones are updated to PROD-nowcast-dev-201806 tag*********
* grid
* NEMO-3.6-code
* rivers-climatology
* SS-run-sets      ******no PROD-nowcast-dev-201806 tag, so at 2209:54a56985baa0
* tides
* tracers
* XIOS-2
* XIOS-ARCH
Killed nowcast-dev/21dec18, and deleted /results/SalishSea/nowcast-dev/21dec18/.
Built SalishSeaCast_Blue configuration on salish:
* XIOS_HOME=/results/nowcast-sys/XIOS-2/ ./makenemo -n SalishSea -m GCC_SALISH -j8
Use restart file from 201806 hindcast/20dec18 to initialize nowcast-dev/21dec18:
* cd /results/SalishSea/nowcast-dev/20dec18/
* mv SalishSea_03414960_restart.nc SalishSea_03414960_restart.nc.aside
* cp /results2/SalishSea/hindcast/20dec18/SalishSea_03235680_restart.nc ./
Relaunch nowcast-dev/21dec18:
* launch_remote_worker $NOWCAST_YAML salish-nowcast run_NEMO "salish-nowcast nowcast-dev --run-date 2018-12-21"
Merged SalishSeaNowcast SurfaceCurrents branch into default and closed it re: full deployment of feature.
(SalishSea)

Moved smelt into ESB-2049 and set up its new monitors, keyboard & mouse; need compstaff to set up network, and need dvi or hdmi cable for 2nd monitor.
(MIDOSS)

Mtg w/ Roman at UBC ARC re: cedar, etc.
* cedar got MPI networks comms libraries on 4dec18
* test XIOS and XIOS builds w/ Intel 2018.3


Sat 22-Dec-2018
^^^^^^^^^^^^^^^

Queued nowcast-agrif/21dec18.
(SalishSea)

Vancouver to Parksville


Sun 23-Dec-2018
^^^^^^^^^^^^^^^

Parksville

See project journal.
(SalishSeaCast-FVCOM)

Worked w/ Susan on XIOS build on cedar; tried to implement Bart's #1 way of using old libibverbs from ticket, but it is unclear how to do so in FCM, and how libibverbs is connected to XIOS executable.
Started work on adding hindcast-201806 to ERDDAP; added disabled XML fragments for all datasets, and Susan created a touch script for testing dataset.xml changes.
Started exploring adding git repo revision tracking to NEMO-Cmd:
* Mercurial flow:
  * hg root
  * files = hg status((hg parents)[0].rev)
  * hg status
* Git flow:
  * git rev-parse --show-toplevel
  * (git rev-list HEAD^..HEAD)[0]
  * files = git show --name-only HEAD
(SalishSea)


Week 52
-------

Mon 24-Dec-2018
^^^^^^^^^^^^^^^

Parksville

forecast/24dec18 got stuck at 84.7% due to a file length issue in atmos forcing; upload_forcing nowcast+ got triggered before grib_to_netcdf finished due to race conditions between grib_to_netcdf and make_live_ocean_files:
(SalishSea)


Tue 25-Dec-2018
^^^^^^^^^^^^^^^

Parksville

**Statutory Holiday** -- Christmas Day


Wed 26-Dec-2018
^^^^^^^^^^^^^^^

Parksville

**Statutory Holiday** -- Boxing Day

Added collect_river_data worker to replace crontab scraping of wateroffice page with ECget with processing data from sarracenia mirrors of datamart hydrology files.
(SalishSea)


Thu 27-Dec-2018
^^^^^^^^^^^^^^^

Parksville

Confirmed that collect_river_data worked overnight.
Discovered that / file system on salish is full so I can't disable ECget cron jobs.
Reviewed Susan's change that added more files for deflation in SalishSeaNEMO.sh script generated by salishsea run sub-command.
Worked on 18-06 ERDDAP datasets w/ Susan; started writing blurb for ERDDAP index page re: move to 18-06 datasets.
(SalishSea)


Fri 28-Dec-2018
^^^^^^^^^^^^^^^

Parksville

Finished and deployed blurb on ERDDAP index page re: move to 18-06 datasets; added setup.xml to erddap-datasets repo.
Started discussing with Susan locations on salishsea-site for NEMO model production configuration descriptions (e.g. 17-02, 18-06) (somewhere on the salishseacast.about page, I think), and the production configuration evolution table (in docs, most recent changes below results calendar grid, and full table(s) somewhere else).
Added sarracenia config files for HRDPS and rivers to SalishSeaNowcast repo, and deployment docs re: sarracenia-env and sr_subscribe use.
Started dev of collect_weather worker.
(SalishSea)


Sat 29-Dec-2018
^^^^^^^^^^^^^^^

Parksville to Vancouver

Continued dev of collect_weather worker.
(SalishSea)

Deirdre & Bob's party


Sun 30-Dec-2018
^^^^^^^^^^^^^^^

Backed up 2018 database; truncated tables for 2019; updated club membership link for 2019; added New Year's Pop event.
(randopony)

Continued dev of collect_weather worker; successful partial test against 18 forecast mirror on skookum.
(SalishSea)

Deirdre & Bob's party


Mon 31-Dec-2018
^^^^^^^^^^^^^^^

Finished dev of collect_weather worker; activated in production on skookum for 18 forecast.
Worked with Susan to change SalishSeaCast runs from V17-02 to V18-06 configuation:
* see https://docs.google.com/drawings/d/1DnQtKXCzkMT2rTMC970E2HliisgG9W2sTk7u2NrldFA/edit
* tagged SalishSeaNowcast with PROD-nowcast-green-201806
forecast/31dec18 got stuck at 84.7% due to a file length issue in atmos forcing; upload_forcing nowcast+ got triggered before grib_to_netcdf finished due to race conditions between grib_to_netcdf and make_live_ocean_files; recovery:
* kill watch_NEMO on west.cloud
* kill xios_server.exe on west.cloud
* wait for SalishSeaNEMO.sh script to finish on west.cloud
* upload_forcing west.cloud nowcast+ --debug
* upload_forcing orcinus nowcast+ --debug
* upload_forcing cedar nowcast+ --debug
* make_forcing_links west.cloud nowcast+ --debug
* make_forcing_links orcinus nowcast+ --debug
* make_forcing_links west.cloud ssh
(SalishSea)

Continued dev of MOHID-Cmd package.
(MIDOSS)
