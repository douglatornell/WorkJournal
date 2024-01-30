# 2023 Work Journal

This is my public work journal.
This journal is about:

* my work as a Research Software Engineer with Dr. Susan Allen in the
  Department of Earth, Ocean and Atmospheric Sciences at the University of British Columbia
* my open-source activities
* occasional notes about life in general


## January

### Week 0

#### Mon 1-Jan-2023

**Statutory Holiday** - New Year's Day

Days since last wwatch3 prep stall: 0

##### SalishSeaCast

Day 1 of v202111 in production.

* Startup problems:
  * forgot to drop old runoff file from upload forcing re: missing Fraser obs
  * forgot to edit nowcast/31dec23/namelist_cfg on arbutus to adjust starting time step number for
    nowcast-blue run
  * nowcast-blue/namelist.light was incorrect; Susan fixed
* nowcast-blue time stepping at 09:20
* forecast success
* nowcast-green time stepping at 10:25
* make_ww3_wind_file forecast stalled; killed and re-run; took 2 tries; arbutus terminal sluggish
* nowcast-green success
  * `make_plots nemo nowcast-green research` failed due to results file name change from
  * `ptrc_T` to `biol_T`
* nowcast-agrif stalled on 1st time step due to no runoff file
  * killed run
  * patched Fraser discharge file
  * reverted exclusion of launching make_runoff_file
  * reverted exclusion of uploading make_runoff_file
  * re-ran with:

    ```bash
    make_runoff_file
    upload_forcing orcinus nowcast+
    make_forcing_links orcinus nowcast-agrif
    ```

* nowcast-dev stalled on 1st time step due to no runoff file
  * killed run because we decided not to continue running nowcast-dev
* tagged repos with PROD-nowcast-green-202111:
  * NEMO-3.6-code
  * XIOS-2
  * XIOS-ARCH
  * grid
  * rivers-climatology
  * SS-run-sets
  * tides
  * tracers
* updated to tags on arbutus
* deleted PROD-nowcast-green-201905 branches and a few other miscellaneous branches on arbutus


##### SalishSeaNowcast

Continued SalishSeaNowcast updates for v202111:

* branch: v202111-nowcast
* PR#223 -
* dropped launch of make_runoff_file from automation re: missing Fraser obs now,
  and it's replaced by make_v202111_runoff_file
* reverted drop of make_runoff_file launch and upload of 201702 runoff file because nowcast-agrif
  needs it
* fixed make_plots re: `ptrc_T` to `biol_T`
* fixed make_plots re: `carp_T` to `chem_T`
* dropped ciliates thalweg & surface plot because v202111 doesn't model or output ciliates
* changed ciliates & flagellates time series plot to microzooplankton & flagellates because v202111
  doesn't model or output ciliates
* changed Fraser_tracer variable name to turbidity due to output variable name change


#### Tue 2-Jan-2023

Days since last wwatch3 prep stall: 0

##### SalishSeaCast

* make_runoff_file failed due to data error for Fraser discharge:
  * no discharge obs for Fraser since 28dec 17:00
* make_v202111_runoff_file patched Fraser discharge
* upload_forcing forecast2 and nowcast+ failed due to no 201905 runoff file
* recovery started at ~07:30:

    ```bash
    # persisted 28dec Fraser discharge in /data/dlatorne/SOG-projects/SOG-forcing/ECget/Fraser_flow
    make_runoff_file
    ```

* make_ww3_current_file forecast stalled; killed and re-run; took 2 tries
* nowcast-agrif watcher reported crash at 09:49
  * `qstat` says run is still going at 11:20
  * scratch file system response is slow


##### salishsea-site

Squash-merged dependabot PR to update appleboy/ssh-action to 1.0.2 re: ssh-proxy security patches.
1-2jan24 biology figures pages are failing with an internal server error;
see `/logs/salishsea-site/pyramid.log`


##### Numeric 2024 Course Support

Helped Susan investigate gh-pages build failure on GitHub;
it looks like maybe nbsphinx has changes since 2022 to need a jupyter kernel in the env


##### Other

* Continued gnucash setup for 2024:
  * finished creating scheduled transactions
  * disabled all scheduled transactions in 2023 file
  * started adding opening balances


#### Wed 3-Jan-2023

Days since last wwatch3 prep stall: 1

##### SalishSeaCast

* make_runoff_file failed due to data error for Fraser discharge:
  * no discharge obs for Fraser since 28dec 17:00
* make_v202111_runoff_file patched Fraser discharge
* upload_forcing forecast2 and nowcast+ failed due to no 201905 runoff file
* recovery started at ~07:15:

    ```bash
    # persisted 28dec Fraser discharge in /data/dlatorne/SOG-projects/SOG-forcing/ECget/Fraser_flow
    make_runoff_file
    upload_forcing arbutus forecast2
    ```

* I used the wrong date for `upload_forcing arbutus forecast2` and caused cascade of failures:
  * NEMO forecast2 failed with error in ocean.output
  * `make_ww3_wind_file forecast2` failed due to missing `NEMO-atmos/fcst/hrdps_y2024m01d05.nc`
  * `make_ww3_current_file forecast2` failed due to `ValueError: Cannot handle size zero dimensions`
    during `open_mfdataset()`
  * `make_plots nemo forecast2 publish` failed with `IndexError: list index out of range` for all
    water level plots
  * `make_feeds forecast2` failed with `IndexError: list index out of range`


##### Numeric 2024 Course Support

* Cloned numeric_2024 to khawla:/media/doug/warehouse/EOAS-teaching/
* built new `numeric_2024` env with Python 3.12
* `.vscode/settings.json` changes:
  * updated default Python interpreter path
  * replaced `restructuredtext.confPath` with `esbonio.sphinx.confDir`
* no push permission on GitHub
* 340 warnings in sphinx build
* gh-pages deployment was broken due to bad rST edits by Susan, and pushing a notebook with empty
  output cells
* learned that we can force nbsphinx to not run notebooks with empty output cells with config
  that is either per-notebook in the json or repo-wide in conf.py
  * Susan will discuss w/ Rachel the pedagogy change of rendering the notebooks to the website
    without output to force the students to run the notebooks


#### Thu 4-Jan-2023

Days since last wwatch3 prep stall: 2

##### SalishSeaCast

* make_runoff_file failed due to data error for Fraser discharge:
  * no discharge obs for Fraser since 28dec 17:00
* make_v202111_runoff_file patched Fraser discharge
* upload_forcing forecast2 and nowcast+ failed due to no 201905 runoff file
* recovery started at ~07:25:

    ```bash
    # persisted 28dec Fraser discharge in /data/dlatorne/SOG-projects/SOG-forcing/ECget/Fraser_flow
    make_runoff_file
    upload_forcing arbutus forecast2
    ```


##### Numeric 2024 Course Support

* got push access
* pushed dependabot config to keep actions in gh-pages workflow up to date
* pushed update to actions/checkout@v4
* merged dependabot PR to update conda-incubator/setup-miniconda to v3
* pushed update to change to use mamba-org/setup-microconda
* updated envs to use Python 3.12
* pushed VSCode workspace settings and tasks updates


##### Other

* Continued gnucash setup for 2024:
  * continued adding opening balances


#### Fri 5-Jan-2023

Days since last wwatch3 prep stall: 3

##### SalishSeaCast

* make_runoff_file failed due to data error for Fraser discharge:
  * no discharge obs for Fraser since 28dec 17:00
* make_v202111_runoff_file patched Fraser discharge
* upload_forcing forecast2 and nowcast+ failed due to no 201905 runoff file
* recovery started at ~07:29:

    ```bash
    # persisted 28dec Fraser discharge in /data/dlatorne/SOG-projects/SOG-forcing/ECget/Fraser_flow
    make_runoff_file
    upload_forcing arbutus forecast2
    ```

  * `run_NEMO forecast2` failed, probably due to timing of yesterday's checklist clearance


#### Sat 6-Jan-2023

Days since last wwatch3 prep stall: 4

##### SalishSeaCast

* make_runoff_file failed due to data error for Fraser discharge:
  * no discharge obs for Fraser since 28dec 17:00
* make_v202111_runoff_file patched Fraser discharge
* upload_forcing forecast2 and nowcast+ failed due to no 201905 runoff file
* recovery started at ~10:00:

    ```bash
    # persisted 28dec Fraser discharge in /data/dlatorne/SOG-projects/SOG-forcing/ECget/Fraser_flow
    make_runoff_file
    upload_forcing arbutus nowcast+
    upload_forcing orcinus nowcast+
    upload_forcing optimum nowcast+
    upload_forcing graham-dtn nowcast+
    ```


#### Sun 7-Jan-2023

Days since last wwatch3 prep stall: 5

##### SalishSeaCast

* make_runoff_file failed due to data error for Fraser discharge:
  * no discharge obs for Fraser since 28dec 17:00
* make_v202111_runoff_file patched Fraser discharge
* upload_forcing forecast2 and nowcast+ failed due to no 201905 runoff file
* recovery started at ~09:20:

    ```bash
    # persisted 28dec Fraser discharge in /data/dlatorne/SOG-projects/SOG-forcing/ECget/Fraser_flow
    make_runoff_file
    upload_forcing arbutus nowcast+
    upload_forcing orcinus nowcast+
    upload_forcing optimum nowcast+
    upload_forcing graham-dtn nowcast+
    ```

Changed to passkey auth on Google.


### Week 1

#### Mon 8-Jan-2023

Days since last wwatch3 prep stall: 6

##### SalishSeaCast

* make_runoff_file failed due to data error for Fraser discharge:
  * no discharge obs for Fraser since 28dec 17:00
* make_v202111_runoff_file patched Fraser discharge
* upload_forcing forecast2 and nowcast+ failed due to no 201905 runoff file
* recovery started at ~08:00:

    ```bash
    # persisted 28dec Fraser discharge in /data/dlatorne/SOG-projects/SOG-forcing/ECget/Fraser_flow
    make_runoff_file

    upload_forcing arbutus nowcast+
    upload_forcing orcinus nowcast+
    upload_forcing optimum nowcast+
    upload_forcing graham-dtn nowcast+
    ```

* crop_gribs 00 went MIA, causing grib_to_netcdf to fail
  * crop_gribs failed due to FileNotFoundError on
    `/results/forcing/atmospheric/continental2.5/GRIB/20240108/00/` when it started
* recovery started at ~08:00:

    ```bash
    crop_gribs 00
    wait for crop_gribs to finish
    grib_to_netcdf nowcast+
    upload_forcing arbutus nowcast+
    upload_forcing orcinus nowcast+
    upload_forcing optimum nowcast+
    upload_forcing graham-dtn nowcast+
    ```

* Slack conversation w/ Henryk re: restoring localhost SMTP on skookum for SalishSeaNowcast CRITICAL
  errors and ERDDAP daily reports and errors

* storm surge alert for 9jan at 05:35, 5.06m; big winds at Neah Bay; 5 days before spring/neap peak

* Fraser River discharge data stream resumed at ~11:20


##### Numeric 2024 Course Support

* got lab1 to render with empty cell outputs


##### MIDOSS

* Found random_oil_spills config file for Susan:
  <https://github.com/MIDOSS/MIDOSS-MOHID-config/blob/main/monte-carlo/random-oil-spills.yaml>


##### SalishSeaNowcast

Squash-merged PR#223 re: migration to 202111 in production.

Fixed test_download_live_ocean failure on khawla with nccopy not found:

* branch: mock-NEMO-Cmd-api-deflate
* PR#224 - squash-merged
* added monkeypatch mock for nemo_cmd.api.deflate() to avoid launching nccopy in subprocess in test

Updated envs to use python-feedgen v1.0.0

* branch: feedgen-1.0.0
* PR#225

Released v23.2 and bumped version to 24.1.dev0.


#### Tue 9-Jan-2023

Worked at ESB

Days since last wwatch3 prep stall: 7


##### MOAD

Group mtg; see whiteboard.


##### salishsea-site

Squash-merged dependabot PR to update apple-boy/ssh-action to v1.0.3 re: request_pty
parameter.


##### Security Updates

Squash-merged dependabot PRs to update fonttools re: CVE-2023-45139 re: arbitrary file
access vulnerability:

* MoaceanTools
* SOG-Bloomcast-Ensemble


##### ERDDAP

Rolling forecast datasets for u & v currents are throwing errors due to mixture of
`m/s` and `m s-1` units:

* today's error was about 4jan & 5jan; check tomorrow to see if error recurs and
  moves to 5jan & 6jan (bad - investigate further), or disappears
  (good - artefact of v202111 rollover)


Messages from ERDDAP complaining about
"java.io.IOException: User limit of inotify watches reached"

* limits got reset during the skookum OS upgrade, so adjust them with:

  ```bash
  sudo sysctl fs.inotify.max_user_watches=131072
  sudo sysctl fs.inotify.max_user_instances=2048
  sudo sysctl -p
  ```


##### SalishSeaCast Docs

* Fixed broken links found by Sphinx linkcheck
* forge.ipsl.jussieu.fr links remain broken due to expired TLS cert
* Intel is forbidding access to docs


##### ERDDAP Datasets

Started adding V21-11 hr-avg fields datasets:

* branch: 202111-hr-avg-fields
* PR#6
* added ubcSSg3DuGridFields1hV21-11
* triggered dataset load with `touch erddap/flag/ubcSSg3DuGridFields1hV21-11`;
  ERDDAP took many minutes to build cache
* added ubcSSg3DvGridFields1hV21-11
* added ubcSSg3DwGridFields1hV21-11
* added ubcSSg3DBiologyFields1hV21-11
  * changed names of micro & meso zooplankton to z1 and z2 zooplankton
* Dropped `testOutOfDate` attribute from V19-05 datasets


#### Wed 10-Jan-2023

Days since last wwatch3 prep stall: 8


##### Security Updates

Squash-merged dependabot PRs to update git-python to v3.1.41 re: CVE-2024-22190 re: arbitrary code
execution vulnerability on Windows:

* AtlantisCmd
* SalishSeaCmd
* SalishSeaNowcast
* NEMO-Cmd


##### Miscellaneous

Sent email to IPSL Forge re: expired TLS cert; reply says that new cert has been requested for over
a month.

Slack conversation w/ Cassidy that lead to discovery that the .git/ trees in most of her clones
on graham have missing files; advised her to do a full new setup for NEMO runs on /scratch.


##### ERDDAP

Rolling forecast datasets for u & v currents are throwing errors due to mixture of
`m/s` and `m s-1` units:

* today's error was about 5jan only; so it appears to be an artefact of the v202111 rollover


##### ERDDAP Datasets

Slack conversation w/ Karyn re: adding Suchy et al 2023 to biology dataset citations comment,
one-liner blurb for it for citation web pages (docs & site),
and explanatory comments for z1 and z2 variables.


##### Stakeholder Support

Replied to email from Dan Baker of QENTOL, YEN W̱SÁNEĆ Marine Guardians:

* summary of changes in 2021-11
* links to 2021-11 datasets: bathymetry, mesh mask, u & v currents
* links to rotate and unstagger functions in SalishSeaTools
* link to use of rotate and unstagger functions in `make_CHS_currents_file` worker


##### SalishSeaNowcast

Started changing ERDDAP dataset ids to V21-11 for `ping_erddap` worker:

* branch: v202111-erddap
* PR#227


#### Thu 11-Jan-2023

Days since last wwatch3 prep stall: 9

Epic Arctic outflow event started overnight; big winds, dropping temperatures, bright sunshine


##### Miscellaneous

Continued Slack conversation w/ Cassidy re: new setup on /scratch.


##### ERDDAP Datasets

Continued adding V21-11 hr-avg fields datasets:

* branch: 202111-hr-avg-fields
* PR#6
* added ubcSSg3DPhysicsFields1hV21-11
* added ubcSSgSeaSurfaceHeightField1hV21-11
* started ubcSSg3DChemistryFields1hV21-11
  * waiting for colour bar limits from Susan


##### SalishSeaNowcast

Continued changing ERDDAP dataset ids to V21-11 for `ping_erddap` worker:

* branch: v202111-erddap
* PR#227


##### Security Updates

Squash-merged dependabot PRs to update jinja2 to v3.1.3 re: CVE-2024-22195 re: XSS vulnerability:

* cookiecutter-analysis-repo
* SalishSeaCast/docs
* MoaceanParcels
* cookiecutter-MOAD-pkg
* MOAD/docs
* AtlantisCmd
* SalishSeaNowcast
* Reshapr
* salishsea-site
* NEMO-Cmd
* SalishSeaCmd
* SalishSeaTools
* moad_tools
* NEMO_Nowcast


#### Fri 12-Jan-2023

Days since last wwatch3 prep stall: 10


##### ERDDAP Datasets

Continued adding V21-11 hr-avg fields datasets:

* branch: 202111-hr-avg-fields
* PR#6
* started ubcSSg3DChemistryFields1hV21-11
  * waiting for colour bar limits from Susan
* added Karyn's descriptive comment attributes for z1 & z2 variables in biology dataset


##### Numeric 2024 Course Support

* changed labs 2-10 to render on website with empty cell outputs
* flagged expired TLS cert for clouds on Slack
* told Susan about funky labs toc headings for labs 2 & 7


##### SalishSeaNowcast

Continued changing ERDDAP dataset ids to V21-11 for `ping_erddap` worker:

* branch: v202111-erddap
* PR#227

Started removing nowcast-dev runs from configuration and workflow:

* branch: drop-nowcast-dev


#### Sat 13-Jan-2023

Days since last wwatch3 prep stall: 11


##### Numeric 2024 Course Support

* opened helpdesk ticket re: expired TLS cert on clouds; Henryk installed new cert


##### ERDDAP Datasets

Continued adding V21-11 hr-avg fields datasets:

* branch: 202111-hr-avg-fields
* PR#6
* finished ubcSSg3DChemistryFields1hV21-11


#### Sun 14-Jan-2023

Days since last wwatch3 prep stall: 12


##### SalishSeaCast

* upload_forcing orcinus forecast2 and nowcast+ failed
* collect_river_data Snohomish_Monroe failed; bad since 15dec
* make_ssh_file forecast2 failed
* no Fraser River turbidity obs since 10jan 11:35


##### Miscellaneous

Figured out steps to run a VSCode remote ssh session in an interactive job on graham via an
ssh `proxy-jump`:

* there is evidence of Alliance staff doing this in the ssh config section of
  <https://www.youtube.com/watch?v=u9k6HikDyqk> though the video doesn't describe doing so
* steps:

  * create a `.ssh/config` entry for interactive compute node sessions on graham:

    ```ssh-config
    Host graham-interactive
      HostName gra111.graham.sharcnet
      User dlatorne
      ProxyJump dlatorne@graham.computecanada.ca
    ```

  * ensure that ssh public key is in `.ssh/authorized_keys` on graham (use ssh-copy-id -i if necessary)
    because proxy-jump to compute node doesn't support CCDB keys
  * open a VSCode session on a graham login node
  * open a terminal on graham
  * request an interactive session:

    ```bash
    salloc --time=1:0:0 --mem=4G --ntasks=1 --account=rrg-allen
    ```

  * wait for interactive session to start with message like:

    ```text
    salloc: Pending job allocation 15395255
    salloc: job 15395255 queued and waiting for resources
    salloc: job 15395255 has been allocated resources
    salloc: Granted job allocation 15395255
    salloc: Waiting for resource configuration
    salloc: Nodes gra633 are ready for job
    (base) [dlatorne@gra633 ~]$
    ```

  * edit `graham-interactive` entry in `.ssh/config` to use assigned node name; e.g. `gra633`
  * start a VSCode session on `graham-interactive`


### Week 2

#### Mon 15-Jan-2023

Days since last wwatch3 prep stall: 13


##### Numeric 2024 Course Support

* confirmed that lab9 code that accesses clouds.eos.ubc.ca now works as expected
* closed helpdesk ticket re: expired TLS cert on clouds


##### SalishSeaCast

* collect_river_data Snohomish_Monroe failed; bad since 15dec
* no Fraser River turbidity obs since 10jan 11:35
  * email conversation w/ Jenn; sensor was removed to avoid damage during cold snap; it will be
    redeployed next week
* yesterday's upload_forcing orcinus forecast2 and nowcast+ failures were due to chiller failure
  * backfill nowcast-agrif:

    ```bash
    upload_forcing orcinus nowcast+ 2024-01-14
    upload_forcing orcinus turbidity 2024-01-14
    # wait for run to finish
    make_forcing_links orcinus nowcast-agrif 2024-01-15
    ```


##### Miscellaneous

Wrote canvas in #alliance-hpc Slack channel re: VSCode remote sessions in interactive compute node
sessions on graham,


##### Phys-Ocgy Seminar

* Ilias


##### ERDDAP Datasets

Continued adding V21-11 hr-avg fields datasets:

* branch: 202111-hr-avg-fields
* PR#6
* started ubcSSgSeaSurfaceCO2FluxField1hV21-11
  * waiting for colour bar limits from Susan


##### SalishSeaNowcast

Continued removing nowcast-dev runs from configuration and workflow:

* branch: drop-nowcast-dev


#### Tue 16-Jan-2023

Worked at ESB

Days since last wwatch3 prep stall: 14


##### ERDDAP Datasets

Continued adding V21-11 hr-avg fields datasets:

* branch: 202111-hr-avg-fields
* PR#6
* started ubcSSgSeaSurfaceCO2FluxField1hV21-11
  * waiting for colour bar limits from Susan
* researched NEMO vvl; found original report; decided on dataset name of
  ubcSSgVariableVolumeLayers1hV21-11


##### MOAD

Group mtg; see whiteboard.


##### SalishSeaCast

Restarted manager to load updated nowcast.yaml with chemistry dataset added to
ping_erddap dataset ids list.


##### Security Updates

Squash-merged dependabot PRs to update jinja2 to v3.1.3 re: CVE-2024-22195 re: XSS vulnerability:

* cookiecutter-djl-pypkg
* SOG-Bloomcast-Ensemble
* SOG
* SOG-Bloomcast

Changed SOG-Forcing default branch name on GitHub from `master` to `main`.
Cloned SOG-Forcing on kudu.
Created sog-forcing-tools env:

```bash
mamba create -n sog-forcing-tools python=3.12 arrow cliff coverage pytest python-dateutil \
  six tox virtualenv
```

Ran `pytest` without problems
(though there were test failures due to changes in `arrow`) to confirm that
env was viable.
Updated `requirements.txt` to resolve long-standing dependabot alert re: py
(former pytest dependency).
Removed sog-forcing-tools env

Created sog-dev env:

```bash
mamba create -n sog-dev python=3.12 pyyaml "colander<2" six translationstring sphinx coverage \
  pytest tox virtualenv
```

Ran `pytest` without problems
(though there were test failures due to changes in `arrow`) to confirm that
env was viable.
Updated `SOGcommand/requirements/production.txt` and `develop.txt` to resolve
long-standing dependabot alert re: py (former pytest dependency).
Removed sog-dev env.

Created sog-bloomcast env:

```bash
mamba create -n sog-bloomcast python=3.12 arrow beautifulsoup4 mako matplotlib numpy pyyaml \
  requests ipython sphinx pytest six
```

Ran `pytest` without problems
(though there were test failures due to changes in `arrow`) to confirm that
env was viable.
Updated `requirements.txt` to resolve
long-standing dependabot alerts re: py (former pytest dependency) and requests.
Removed sog-bloomcast env.


##### SalishSeaNowcast

Explored changes necessary to update `get_onc_ctd` worker to ONC scalar data API v3.0:

* it appears that I wrote `salishsea_tools.data_tools.get_onc_data()` in a generic enough
  way that its doesn't need to be changed
* instead, need to update its call in:
  * `get_onc_ctd` worker
  * `get_onc_ferry_data` worker
  * `figures/comparison/compare_venus_ctd.py` figure module
* possible new call:

  ```python
  onc_data = data_tools.get_onc_data(
      "scalardata",
      "getByLocation",
      TOKEN,
      locationCode=parsed_args.onc_station,
      deviceCategoryCode="CTD",
      sensorCategoryCodes="salinity,temperature",
      dateFrom=data_tools.onc_datetime(f"{ymd} 00:00", "utc"),
  )
  ```


#### Wed 17-Jan-2023

Major snowfall overnight and through day.

Days since last wwatch3 prep stall: 15

##### SalishSeaCast

Email from Parker to say that there was a problem with LiveOcean this morning; he says it's fixed,
but `test_download_live_ocean` is still waiting for sentinel file; told Parker.


##### Sharcnet Seminar

False Sharing and Contention in Parallel Codes

* Paul Preney, U Windsor
* All the materials (slides, YouTube links etc) will go to this web page:
  <https://helpwiki.sharcnet.ca/wiki/Online_Seminars>
* slow performance of threaded code due to concurrent access of values close enough together in
  memory that they are in the same cache line (64 or 128 bytes)
* mitigate in C++11 via `alignas`, or dynamic allocation in general


##### ERDDAP Datasets

Finished adding V21-11 hr-avg fields datasets:

* branch: 202111-hr-avg-fields
* PR#6
* finished ubcSSgSeaSurfaceCO2FluxField1hV21-11
* added ubcSSgVariableVolumeLayers1hV21-11
* fixed description dataset attr values
* added ubcSSg3DLightFields1hV21-11


##### SalishSeaNowcast

Finished changing ERDDAP dataset ids to V21-11 for `ping_erddap` worker:

* branch: v202111-erddap
* PR#227
* added ubcSSgSeaSurfaceCO2FluxField1hV21-11
* added ubcSSg3DVariableVolumeLayers1hV21-11
* added ubcSSg3DLightFields1hV21-11



#### Thu 18-Jan-2023

Days since last wwatch3 prep stall: 16


##### SalishSeaCast

Greenwater river discharge time series was empty.

nowcast-agrif failed with `FileNotFoundError`:

* 17jan24 didn't complete due to power bump at ~17:00 yesterday; compute nodes are shut down
* re-run:

  ```bash
    make_forcing_links orcinus nowcast-agrif 2024-01-17
    # wait for run to finish
    make_forcing_links orcinus nowcast-agrif 2024-01-18
  ```

Email conversation with Rich re: resumption of TWDP data stream:

* The message we got from Richard back in Mar-2022 was that there was no plan for the TWDP data
  stream to resume after the vessels re-organization in Jun-2022. At the end of Aug-2022 I dropped
  the `get_onc_ferry` worker from automation because a daily stream of errors is annoying,
  desensitizing (and in this case maddening).
* It appears that the data stream resumed on 11-Oct-2022 and was continuous until at least
  19-Nov-2023. There is also data on 23-25 Nov-2023, but that may not be on-route,
  rather from repositioning of the vessel for refit.
* The message on the data preview page says:
  "Instruments off in preparation for the refit | high (Applies to: 16-Nov-2023 00:00:00 UTC - Now)".
* No data in the 11-Oct-2022 to 25-Nov-2023 time period from the following sensors:
  * Turbidity, Chlorophyll, Florescence
  * Thermosalinograph
  * Pyranometer (solar radiation)
  * Oxygen Sensor
  * Carbon Dioxide Sensor
* There is data from:
  * Pyrogenometer (longwave radiation)
  * Air Temperature
  * Relative Humidity
  * Barometric Pressure


##### Security Updates

Squash-merged dependabot PRs to update jupyterlab-lsp to v2.2.2 re: CVE-2024-22415 re: unsecured
endpoints vulnerability:

* SalishSeaTools


##### SalishSeaNowcast

Started work on updating `get_onc_ctd` worker to ONC APIv3:

* branch:
* PR#
* updated `get_onc_data()` call; discoverd need to update `salishsea_tools.data_tools.onc_json_to_dataset()`
* hacked `get_onc_data()` enough to be able to run `get_onc_ctd SEVIP` to backfill from
  12dec23 to 17jan24


##### SalishSeaTools

Started work on updating `data_tools.onc_json_to_dataset()` worker to ONC APIv3:

* branch: update-onc_json_to_dataset
* PR#
* used PyCharm AI to hack together a unit test to help with update
* hacked `onc_json_to_dataset()` enough to be able to run `get_onc_ctd SEVIP` to backfill from
  12dec23 to 17jan24



#### Fri 19-Jan-2023

Days since last wwatch3 prep stall: 0


##### SalishSeaCast

`crop_gribs 12` stalled with 1 file not processed
`make_ww3_current_file forecast2` stalled; killed it and re-ran
Greenwater river discharge time series was empty.

Pulled SalishSeaNowcast v202111-erddap branch on skookum and restarted manager to load updated
nowcast.yaml with chemistry dataset added to ping_erddap dataset ids list.


##### SalishSeaTools

Finished work on updating `data_tools.onc_json_to_dataset()` worker to ONC APIv3:

* branch: update-onc_json_to_dataset
* PR#93 -
* cleaned up unit tests


##### SalishSeaNowcast

Continued work on updating `get_onc_ctd` and `get_onc_ferry` workers to ONC APIv3:

* branch:
* PR#
* started digging into `get_onc_ferry`
* it fails with KeyError on `nav_data.attrs["station"]` in `_resample_nav_coord()`



#### Sat 20-Jan-2023

Days since last wwatch3 prep stall: 1


##### SalishSeaCast

nowcast-agrif/19jan24 timed out; recovery:

  ```bash
    # wait for 20jan24 run to fail
    make_forcing_links orcinus nowcast-agrif 2024-01-19
    # wait for run to finish
    make_forcing_links orcinus nowcast-agrif 2024-01-20
  ```

Email from Mark saying he has moved nowcast-agrif file space form scratch to data and added a symlink
to enable him to isolate the scratch file system for troubleshooting.


##### Security Updates

Squash-merged dependabot PRs to update jupyterlab to v3.6.7 re: CVE-2024-22421 re: auth & XSRF token
exposure vulnerability:

* MoaceanParcels
* SOG-Bloomcast-Ensemble



#### Sun 21-Jan-2023

Days since last wwatch3 prep stall: 2


##### SalishSeaCast

* nowcast-agrif/21jan24 ran in 47 min, like the old days :-)


##### SalishSeaNowcast

`ping_erddap` successfully updated V21-11 datasets after nowcast-green run

* branch: v202111-erddap
* PR#227 - squash-merged

Changed branch on skookum back to main and pulled.


##### ERDDAP Datasets

Finalized adding V21-11 hr-avg fields datasets:

* branch: 202111-hr-avg-fields
* PR#6 - squash-merged

Changed branch on skookum back to main and pulled.

Squash-merged dependabot PRs re: jinja2, jupyterlab, and jupyterlab-lsp.



### Week 3

#### Mon 22-Jan-2023

Days since last wwatch3 prep stall: 3


##### Stakeholder Support

Replied to email from Dan Baker of QENTOL, YEN W̱SÁNEĆ Marine Guardians:

* 21-08 bathymetry dataset to map x/y to lon/lat
* explanation of grid orientation and rotation
* link to Ben's thesis ch 2 for evaluation of model surface currents vs obs


##### SalishSeaNowcast

Continued removing nowcast-dev runs from configuration and workflow:

* branch: drop-nowcast-dev
* PR#229
* rebased branch on to main
* pulled branch on skookum for testing tomorrow; restarted manager to load updated
  config & `next_workers` module

Continued work on updating `get_onc_ctd` and `get_onc_ferry` workers to ONC APIv3:

* branch: onc-api-v3
* PR#
* started digging into `get_onc_ferry`
* it fails with KeyError on `nav_data.attrs["station"]` in `_resample_nav_coord()`
  * fixed in SalishSeaTools


##### SalishSeaTools

Continued work on updating `data_tools.onc_json_to_dataset()` worker to ONC APIv3:

* branch: update-onc_json_to_dataset
* PR#93 -
* added `parameters.locationCode` to dataset attrs as `station` because that's how `get_onc_ferry`
  expected to get a metadata element



#### Tue 23-Jan-2023

Worked at ESB

Days since last wwatch3 prep stall: 4


##### SalishSeaCast

* launches of `upload_forcing forecast2` after `grib_to_netcdf 06` failed due to
  missing `shared storage` key
  * added key on skookum and launched workers manually at 03:45
* launches of `upload_forcing nowcast+` after `grib_to_netcdf 12` failed due to
  missing `shared storage` key and me forgetting to restart manager at 03:45
  * restarted manager and launched workers manually at 09:45
* launches of `make_plots` failed due to missing `nowcast-dev` results archive
  key
  * added key on skookum and launched workers manually starting at 13:45

    ```bash
    make_plots nemo forecast2 publish 2024-01-22
    make_plots nemo nowcast publish 2024-01-23
    make_plots nemo nowcast comparison 2024-01-22  # persistent failure
    make_plots nemo forecast publish 2024-01-23

    make_plots nemo nowcast-agrif research 2024-01-23
    make_plots nemo nowcast-green research 2024-01-23
    ```

* started working on backfilling day & month average datasets for 21-11 from
  01sep23 to present
  * confirmed that `make_averaged_dataset` worker works:

    ```bash
    make_averaged_dataset salish day biology 2023-09-03
    make_averaged_dataset salish day chemistry 2023-09-03
    make_averaged_dataset salish day physics 2023-09-03
    ```

  * logs go to hindcast*.log
  * host arg seems irrelevant because worker can run on skookum and use cluster
    on salish via reshapr cluster config
  * used bash loop to process to 15sep23


##### MOAD

Group mtg; see whiteboard.


##### Security Updates

Squash-merged dependabot PR to update pillow to v10.2.0 re: CVE-2023-50447 re:
arbitrary code execution vulnerability:

* MoaceanParcels
* Reshapr
* moad_tools
* SOG-Bloomcast-Ensemble

TODO:

* SalishSeaTools re: jupyterlab


##### Miscellaneous

* Slack conversation w/ Ilias about problems loading 10may2016 biol & grid_T datasets
* Slack conversation w/ Cassidy re: rsync as alternative to sftp for wildcard/regex downloads



#### Wed 24-Jan-2023

Days since last wwatch3 prep stall: 5


##### SalishSeaCast

* launch of `run_NEM forecast2` failed probably due to checklist clearance during figure backfilling
  yesterday
* finished backfilling day & month average datasets for 21-11 from
  01sep23 to present
  * used bash loop in new `day-month-avg` tmux session on skookum to process to 24jan24
  * also calculated month average datasets for sep-dec 2023
* nowcast-agrif died on launch; re-ran and it failed again due to 1 node being unable to access nemo.exe


##### SalishSeaNowcast

Continued removing nowcast-dev runs from configuration and workflow:

* branch: drop-nowcast-dev
* PR#229
* dug into removal of `nowcast-dev` from plots
  * it's all about the `compare_venus_ctd` fig module, but ONC API v3 needs to be handled there;
    decided to defer that to a future PR

Continued work on updating `get_onc_ctd` and `get_onc_ferry` workers to ONC APIv3:

* branch: onc-api-v3
* PR#
* continued digging into `get_onc_ferry`
* it fails with ValueError due to all NaNs and all bad qaqc flags in `_qaqc_filter()`
  * fixed by checking for those conditions and returning an empty data array when true



#### Thu 25-Jan-2023

Days since last wwatch3 prep stall: 6


##### SalishSeaNowcast

Continued work on updating `get_onc_ctd` and `get_onc_ferry` workers to ONC APIv3:

* branch: onc-api-v3
* PR#
* continued digging into `get_onc_ferry`
* it fails with AttributeError on `REL_HUMIDITY` sensor from `TEMPHUMID` device
  * fixed by changing `REL_HUMIDITY` to `rel_humidity` in config
* it fails with AttributeError on `solar_radiation` sensor from `PYRANOMETER` device
  * fixed by refactoring `_qaqc_filter()` to catch AttributeError and use `_empty_device_data()`
    and to handle all NaNs and all bad qaqc flags case from yesterday
* got `get_onc_ferry` to a state where it would run
    get_onc_ferry TWDP 2022-10-11
  lots of missing data
* dataset load on ERDDAP failed due to units mismatches on `temperature` and `air_temperature`
  variables
  * fixed with another hack in `_empty_device_data()`


TODO:

* update `compare_venus_ctd` fig module re: ONC API v3, then drop dev model elements
* rename make_runoff_file to make_v201702_runoff_file
* rename make_v202111_runoff_file to make_runoff_file
* add config tests for `run type[*][mesh mask]`
* add config tests for `run type[*][bathymetry]`
* add config tests for `run type[*][land processor elimination]`
* add config tests for `run type[*][run sets dir]`
* improve test_run_NEMO test for forcing symlinks ??
* add tests for _upload_*_files in upload_forcing
* `make_averaged_dataset`:
  * change logging to nowcast*.log
  * drop host arg
  * add `make_averaged_dataset day *` to `after_download_results nowcast-green`
  * add `make_averaged_dataset month *` to `after_make_averaged_dataset physics`
      at month-end, or maybe use race condition mgmt ??


##### SalishSeaTools

Continued work on updating `data_tools.onc_json_to_dataset()` worker to ONC APIv3:

* branch: update-onc_json_to_dataset
* PR#93 -
* changed to branch on `skookum:/SalishSeaCast/tools/SalishSeaTools`


##### SalishSeaCast

* nowcast-agrif died on launch due to `pod29a11.ibb` node being unable to access `nemo.exe`
  * confirmed that executable exists and symlink is okay in --no-submit test
  * email from Mark explained that problem was due to a node that rebooted and didn't get the
    scratch -> data symlink when it restarted
  * backfilled:

  ```bash
    make_forcing_links orcinus nowcast-agrif 2024-01-25
    # wait for run to finish
    make_forcing_links orcinus nowcast-agrif 2024-01-25
  ```

* manually ran `make_averaged_dataset day biology|chemistry|physics` after nowcast-green run


##### ERDDAP

Successfully loaded TWDP ferry obs for 11-31oct22; most/all datasets empty except navigation.



#### Fri 26-Jan-2023

Days since last wwatch3 prep stall: 7


##### ERDDAP

* Successfully loaded TWDP ferry obs for 01nov22 to 30nov22:
  * most/all datasets empty except navigation
  * vessel went out of service on 15nov22 and moved to refit on 18nov22
  * vessel resumed runs on 24dec22; empty datasets except nav to 31dec22


##### SalishSeaNowcast

Finished removing nowcast-dev runs from configuration and workflow:

* branch: drop-nowcast-dev
* PR#229 - squash-merged
* successfully tested in production since 24jan24
* fixed tests re: restoration of nowcast-dev results archive necessary to keep `make_plots` working
* returned skookum to main branch and updated


##### Numeric 2024 Course Support

Updated uibcdf/action-sphinx-docs-to-gh-pages version. Pinned it to Git hash of its v2.1.0
release so that dependabot notifies us of future updates.



#### Sat 27-Jan-2023

Days since last wwatch3 prep stall: 8



#### Sun 28-Jan-2023

Days since last wwatch3 prep stall: 9



### Week 4

#### Mon 29-Jan-2023

Days since last wwatch3 prep stall: 0


##### SalishSeaCast

`make_ww3_current_file forecast` stalled; killed it and re-ran


##### Miscellaneous

Checked status of scheduled GHA workflows:

  ```bash
  conda activate gha-workflows
  python /media/doug/warehouse/MOAD/gha-workflows/gha_workflow_checker/gha_workflows_checker.py
  ```

Reactivated workflows that had been disabled due to inactivity:

  ```bash
  gh workflow enable -R SS-Atlantis/AtlantisCmd CodeQL
  gh workflow enable -R UBC-MOAD/docs sphinx-linkcheck
  ```

Squash-merged dependabot PRs to bump mamba-org/setup-micromamba to 1.8.0 re: feature updates:

* SalishSeaNowcast
* rhwhite/numeric_2024
* erddap-datasets
* gha-workflows

Squash-merged dependabot PRs to bump codecov/codecov-action to 3.1.5 re: update to Node.js 20:

* SalishSeaNowcast
* gha-workflows

Updated PyCharm on khawla to 2023.3.3.

Reviewed notification, re-raised by Gmail, from readthedocs re: manually configured webhooks that
lack secrets; found that I had already handled all of the affected projects.


##### salishsea-site

Fixed issue #64 re: dynamic copyright years range on license page.

Started owrk on biology page re: no more ciliates figure in V21-11, and name change for turbidity
figure file; can handle via `ImageLoop.available()` but doing so triggers unit test failures.


TODO:

* drop ciliates thalweg and surface plot from biology pages for 01jan24 onward re: v202111
* fix file name for Fraser River turbidity thalweg & surface plot for 01jan24 onward re: v202111
  variable name change
* add Suchy et al 2023 to publications page (and docs/CITATION.rst)


##### Phys Ocgy Seminar

Sam re: TReX Deep tracer release experiment in St. Lawrence.






Add Tereza's pubs to ERDDAP.


TODO:

* change automation workflow to run nowcast-green in place of nowcast-blue
  * add output of 10min avg tide gauge station files
* remove VHFR FVCOM from automation workflow
  * remove FVCOM boundary slab files output from nowcast-green/file_def.xml
  * drop FVCOM-Cmd and OPPTools dependencies


TODO:

* Update AtlantisCmd to drop Python 3.10 because NEMO-Cmd has dropped it;
  GHA workflow is failing



TODO:

* update xarray-tests instructions to use Python 3.11
* drop pkg install from xarray-docs instructions; it's included in docs.yml



* Python 3.12:
  * successful workflow test with 3.12:
    * AtlantisCmd
    * NEMO_Nowcast
    * salishsea-site
    * moad_tools - migrated on 18Dec23 in PR#43
    * SalishSeaCmd - migrated on 29nov23  PR#49
    * NEMO-Cmd - migrated on 20nov23 in PR#68
    * SalishSeaNowcast - success on khawla on 6nov23, migrated on 10nov23 in PR#209
    * Reshapr - migrated on 28oct23 in PR#99
  * failed workflow test with 3.12:
    * SalishSeaCast/docs
    * MOAD/docs - expect same problem as SalishSeaCast/docs
    * MoaceanParcels - failing with 3.10; no point in trying 3.12 yet
  * no workflows:
    * erddap-datasets
    * analysis-doug






Refresh myself on Fortran in VS Code and on-the-fly compilation; prep to present to group.






TODO:

* change download_weather to gather only files missed by collect_weather so that it can
  work with crop_gribs monitoring incoming files
  * check for presence of files before downloading them; skip if present


TODO:

* update .readthedocs.yaml to use ubuntu-22.04 and mambaforge-22.9 in many repos
  * MOAD/docs - done in PR#32
  * FVCOM-Cmd - done in PR#10
  * Reshapr - done 28oct23 in PR#100
  * NEMO-Cmd - done 20nov23 in PR#71
  * SalishSeaCmd - done 29nov23 in PR#54
  * moad_tools - done 18dec23 in PR#47


TODO:

* fix straight line gaps in wwatch3 forecast plots (forecast2 are okay)

* migrate PyPDF2 to pypdf in SalishSeaNowcast


TODO:

* modernize packaging:
  * Reshapr - done 30oct23 in PR#101
  * moad_tools - done 18dec23 in PR#48
  * cookiecutter-MOAD-pypkg
  * salishsea-site
  * NEMO_Nowcast
  * ECget
  * MoaceanParcels
  * AtlantisCmd
  * SOG
  * SOG-Bloomcast-Ensemble
  * SalishSeaTools
  * rpn-to-gemlam
  * Marlin



TODO:

* review and clean up permissions in GitHub orgs




Because I can never remember how to get a git feature branch that I set aside back into working
state:

* ref: <https://www.atlassian.com/git/tutorials/merging-vs-rebasing>
* git switch feature
* git rebase main
* In PyCharm > Git > Log context menu "Rebase 'feature' onto 'main'"
* **BUT** if the changes in the feature branch overlap files in main, it's possible that
  a merge will be required



TODO:

* update .readthedocs.yaml build:os to ubuntu-22.04
* add sphinx-notfound-page extension to to repos with docs
  * <https://sphinx-notfound-page.readthedocs.io/en/latest/index.html>
  * MOAD:
    * Reshapr - done
    * docs - done
    * moad_tools - done 14Nov22
    * MoaceanParcels - done 18Dec22
    * cookiecutter-MOAD-pypkg - issue created
  * SalishSeaCast:
    * SalishSeaNowcast - done 4oct22
    * salishsea-site - done 11oct22
    * SalishSeaCmd - done 20Dec22
    * NEMO-Cmd - done 25oct22
    * SOG-Bloomcast-Ensemble - issue created
    * tools - issue created
