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

Discussed automation of hindcast runs on cedar w/ Susan; see whiteboard photo.
Discussed Fraser flow values w/ Rich & Katia.
Started setting up projects/SalishSea/hindcast-sys/ tree on cedar:
* cloned repos
* built XIOS-2
* built NEMO-3.6-code SMELT config
* built NEMO-3.6-code REBUILD_NEMO
Set up hindcast-sys/17nov14/ where we will initialize from, but discussion w/ Susan revealed that we can't run there yet to to bathymetry issues; run from neap in mid-Nov 2017 for testing.
(SalishSea)

Started exploring new ONC data API docs: https://wiki.oceannetworks.ca/display/O2A/Oceans+2.0+API+Home
(ONC API)


Tue 6-Feb-2018
^^^^^^^^^^^^^^

Continued getting niko set up under PoP_OS!.

Continued setting up projects/SalishSea/hindcast-sys/ tree on cedar:
* Deleted hindcast-sys/17nov14/ because we're not ready for it, and we decided to keeo the results on $SCRATCH
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
Created new nowcast-fig-dev conda env on kudu to use aconda-forge priority and h5netcdf.
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

Experimented with Python asyncio for ECCC datamart file downloads; implementation was not difficult for the basics; async was generatlly faster for 1 or 2 hours of files, but less conclusively so for 6 hours.


Sun 25-Feb-2018
~~~~~~~~~~~~~~~

See project work journal.
(GOMSS)

Changed bloomcast view so that bloom date log shows most recent predictions at the top.
(salishsea-site)

Helped Susan with debugging 2016 bloomcast date fail.
(bloomcast)

Worked on migrating sqlalchemyorg to blogofile 0.8.3 under Python 3.s

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

Cédric Chavanne from Rimouski give SCOR west tour seminar on his method for verification of mesoscale heat flux parameterizations for the winter mixing layer in global climate models.

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

Reviewed and fixed RST in Birgit's XIOS-1 to XIOS-2 docs.
Wrote docs section about local build and preview of MOAD docs re: contributing to them.
(MOAD)



* Replace old 2014 bloomcast page on ~sallen w/ redirect to present page
* Stephanie would like web access to prior year's bloomcasts
* Ask Michael for access to 2nd Narrows ADCP for VHFR currents evaluation figure
* Charles says wwatch3 results can go public; ask Marlene for a visualization contract




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
