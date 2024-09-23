# 2024 Work Journal

This is my public work journal.
This journal is about:

* my work as a Research Software Engineer with Dr. Susan Allen in the
  Department of Earth, Ocean and Atmospheric Sciences at the University of British Columbia
* my open-source activities
* occasional notes about life in general


## January

### Week 0

#### Mon 1-Jan-2024

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


#### Tue 2-Jan-2024

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


#### Wed 3-Jan-2024

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


#### Thu 4-Jan-2024

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


#### Fri 5-Jan-2024

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


#### Sat 6-Jan-2024

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


#### Sun 7-Jan-2024

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

#### Mon 8-Jan-2024

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


#### Tue 9-Jan-2024

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


#### Wed 10-Jan-2024

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


#### Thu 11-Jan-2024

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


#### Fri 12-Jan-2024

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


#### Sat 13-Jan-2024

Days since last wwatch3 prep stall: 11


##### Numeric 2024 Course Support

* opened helpdesk ticket re: expired TLS cert on clouds; Henryk installed new cert


##### ERDDAP Datasets

Continued adding V21-11 hr-avg fields datasets:

* branch: 202111-hr-avg-fields
* PR#6
* finished ubcSSg3DChemistryFields1hV21-11


#### Sun 14-Jan-2024

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

#### Mon 15-Jan-2024

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


#### Tue 16-Jan-2024

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


#### Wed 17-Jan-2024

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



#### Thu 18-Jan-2024

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
  * Pyrometer (solar radiation)
  * Oxygen Sensor
  * Carbon Dioxide Sensor
* There is data from:
  * Pyrogenometer (long-wave radiation)
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



#### Fri 19-Jan-2024

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



#### Sat 20-Jan-2024

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



#### Sun 21-Jan-2024

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

#### Mon 22-Jan-2024

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



#### Tue 23-Jan-2024

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

  * logs go to `hindcast*.log`
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


##### Miscellaneous

* Slack conversation w/ Ilias about problems loading 10may2016 biol & grid_T datasets
* Slack conversation w/ Cassidy re: rsync as alternative to sftp for wildcard/regex downloads



#### Wed 24-Jan-2024

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



#### Thu 25-Jan-2024

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



#### Fri 26-Jan-2024

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



#### Sat 27-Jan-2024

Days since last wwatch3 prep stall: 8



#### Sun 28-Jan-2024

Days since last wwatch3 prep stall: 9



### Week 4

#### Mon 29-Jan-2024

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

Started work on biology page re: no more ciliates figure in V21-11, and name change for turbidity
figure file; can handle via `ImageLoop.available()` but doing so triggers unit test failures.


##### Phys Ocgy Seminar

Sam re: TReX Deep tracer release experiment in St. Lawrence.



#### Tue 30-Jan-2024

Days since last wwatch3 prep stall: 1


##### MOAD

Group mtg; see whiteboard.


##### SalishSeaCast

* backfilled day average datasets for 21-11 to present
  * noticed that 20jan24 biology day-avg was missing; re-ran but it stalled repeatedly;
    had to run manually with:

    ```bash
    reshapr extract \
      /SalishSeaCast/SalishSeaNowcast/config/reshapr/day-average_202111_biology.yaml \
      --start-date 2024-01-20 --end-date 2024-01-20
    ```

  * used bash loop in new `day-month-avg` tmux session on skookum to process
    26jan24 to 30jan24


##### Miscellaneous

Squash-merged dependabot PR to bump mamba-org/setup-micromamba to 1.8.0 re: feature updates:

* salishsea-site

Updated PyCharm on kudu to 2023.3.3.


##### 2024 Bloomcast

* Prep on kudu:
  * updated SOG-Bloomcast-Ensemble clone
  * confirmed that SOG clone is up to date
  * created new bloomcast-2024 env (Python 3.12)
  * did editable installs of SOG & SOG-Bloomcast-Ensemble
  * SOG-Bloomcast-Ensemble test suite ran successfully
  * commit environment.yaml and requirements.txt
  * mkdir run/2023
  * cp run/2023_bloomcast_infile.yaml run/2024_bloomcast_infile.yaml
  * mv run/2023_bloomcast_infile.yaml run/2023/
  * committed archive of 2023 SOG YAML infile
  * edit run/2023_bloomcast_infile.yaml
  * edit run/config/yaml
  * successfully tested run prep w/ SOG runs and publish to web disabled
    * smtpd has been dropped from Python stdlib in 3.12, so test email
      functionality is broken
    * aiosmtpd is probably the alternative to use
  * committed run/2024_bloomcast_infile.yaml and run/config.yaml
* Setup on salish:
  * updated SOG-Bloomcast-Ensemble clone
  * SOG clone needs to be at 55af3c2 to avoid error from Ben's post 7-Apr-2014 commits
  * created new bloomcast env: Python 3.12
  * did editable installs of SOG & SOG-Bloomcast-Ensemble
  * runs dir: /data/dlatorne/SOG-projects/SOG-Bloomcast-Ensemble/run
  * archived 2023_bloomcast* files in run/2023/
  * archived Englishman_flow Fraser_flow Sandheads_wind in run/2023/
  * archived YVR_* in run/2023/
  * ran test w/ push to web disabled
    * unrecognized weather description:
        `Thunderstorms,Heavy Rain,Fog`
    * bloom predictions:

        ```text
        INFO [bloomcast.ensemble] Predicted earliest bloom date is 2024-03-03
        INFO [bloomcast.ensemble] Earliest bloom date is based on forcing from 2004/2005
        INFO [bloomcast.ensemble] Predicted early bound bloom date is 2024-03-07
        INFO [bloomcast.ensemble] Early bound bloom date is based on forcing from 1995/1996
        INFO [bloomcast.ensemble] Predicted median bloom date is 2024-03-21
        INFO [bloomcast.ensemble] Median bloom date is based on forcing from 2003/2004
        INFO [bloomcast.ensemble] Predicted late bound bloom date is 2024-04-09
        INFO [bloomcast.ensemble] Late bound bloom date is based on forcing from 2006/2007
        INFO [bloomcast.ensemble] Predicted latest bloom date is 2024-04-13
        INFO [bloomcast.ensemble] Latest bloom date is based on forcing from 1998/1999
        ```

  * deleted last year's `bloom_date_evolution.log` and `bloomcast.log`
  * removed `wind_data_date` and re-ran with push to web enabled
  * confirmed web page updated as expected
  * enabled cron job
* Added new unrecognized weather description to cloud fraction mapping.

TODO:

* replace removed stdlib `smtpd` with `aiosmtpd` for email testing
* silence `matplotlib.font_manager` log messages



#### Wed 31-Jan-2024

Days since last wwatch3 prep stall: 0


##### SalishSeaCast

`upload_forcing forecast2` failed due to no 17-02 runoff file which was due to no Fraser discharge

* recovery started at ~07:45

  ```bash
  ln -s /results/forcing/rivers/R201702DFraCElse_y2024m01d29.nc \
    /results/forcing/rivers/R201702DFraCElse_y2024m01d30.nc
  ```

  * skipped `forecast2` runs because nowcast runs are imminent

* `make_ww3_current_file forecast` stalled; killed it and re-ran
* manually ran `make_averaged_dataset day biology|chemistry|physics` after nowcast-green run
* manually ran `make_averaged_dataset month biology|chemistry|physics` after nowcast-green run


##### SalishSeaNowcast

Created issue #232 to change upload_forcing worker to persist missing runoff files via symlinks
instead of failing:

* branch: symlink-missing-runoff-files
* PR#233
* dropped TODOs re: removing 201702 runoff files from config because they are needed for
  nowcast-agrif
* improved upload_forcing unit tests
* failed to get rid of uses of unittest.mock.patch that apply side effects to test nested exceptions
  code 🙁
* added persistence of previous day for missing runoff files via symlinks
* switched skookum to symlink-missing-runoff-files branch for testing


##### salishsea-site

Continued work on biology page re: no more ciliates figure in V21-11, and name change for turbidity
figure file:

* realized that unit test failures were due to bug that changed biology image loops data
  structure
* cleaned a lot (but not all 🙁) uses of `unittest.mock.patch` out of `test_salishseacast.py`


### February

#### Thu 1-Feb-2024

Days since last wwatch3 prep stall: 0


##### SalishSeaCast

`upload_forcing forecast2` failed due to no 17-02 runoff file which was due to no Fraser discharge
and date offset bug in my work on `upload_forcing` yesterday prevented it from handling the issue
by creating a symlink

* recovery started at ~07:45

  ```bash
  ln -sf /results/forcing/rivers/R201702DFraCElse_y2024m01d30.nc \
    /results/forcing/rivers/R201702DFraCElse_y2024m01d31.nc
  ```

  * skipped `forecast2` runs because nowcast runs are imminent

`upload_forcing nowcast+` failed due to indentation bug in yesterday's work

* recovery started at ~11:00

  ```bash
  upload_forcing $NOWCAST_YAML arbutus nowcast+
  upload_forcing $NOWCAST_YAML orcinus nowcast+
  upload_forcing $NOWCAST_YAML optimum nowcast+
  upload_forcing $NOWCAST_YAML graham-dtn nowcast+
  ```

* `make_ww3_wind_file forecast` stalled; killed it and re-ran

* nowcast-agrif crashed due to node communication issue


##### Stakeholder Support

Teams meeting with:

* Dan Baker of QENTOL, YEN W̱SÁNEĆ Marine Guardians
* Serge Kena-Cohen (project mgr) of Fujitsu who contract for Transport Canada EMSA program
* Peter McLaren (developer) of Fujitsu who contract for Transport Canada EMSA program

* Objective is reports for QENTOL of current-corrected vessel velocities based on recent
  (week to month time frame) vessel AIS obs.
* Discussed overall processing approach and implementation Peter's code
* Agreed to process some AIS obs that Peter will send as a cross-check


##### SalishSeaNowcast

Continued work on issue #232 to change upload_forcing worker to persist missing runoff files via
symlinks instead of failing:

* branch: symlink-missing-runoff-files
* PR#233
* fixed bugs re: date offset, and indentation of symlink creation code


##### Miscellaneous

VSCode v1.86 that landed today refuses to connect to `salish` and `graham` due to too-old versions
of `libc`.
Sent Slack msg to Henryk about planning for an OS upgrade of `salish`.

UBC-IOS modeling mtg:

* Laura re: Bute Inlet paper and OSM poster


#### Fri 2-Feb-2024

Days since last wwatch3 prep stall: 1


##### SalishSeaCast

`crop_gribs 12` stalled with 1 file unprocessed; delayed start of nowcast-blue run by ~2h


##### SalishSeaNowcast

Finished issue #232 to change upload_forcing worker to persist missing runoff files via symlinks
instead of failing:

* branch: symlink-missing-runoff-files
* PR#233 - squash-merged
* returned skookum to main branch

Continued work on updating `get_onc_ctd` and `get_onc_ferry` workers to ONC APIv3:

* branch: onc-api-v3
* PR#234
* continued digging into `get_onc_ferry`
* changed qaqc flags mask in `get_onc_ferry` to <=1 or >=7 to handle the fact that we request
  1-second-averaged data which gets a flag value of 7
* dropped NaN mask because that is now handled by ONC and has a qaqc flag value of 9
* ran successful data requests on skookum for 31mar23
* started working on unit tests


##### ERDDAP

* Successfully re-loaded TWDP ferry obs for 10-31oct22, and 1nov2022 to 31dec2022


#### Sat 3-Feb-2024

Days since last wwatch3 prep stall: 2


##### ERDDAP

* Successfully re-loaded TWDP ferry obs for 10-31oct22, and 1jan2023 to 31mar2023
* something wrong on 9feb23
* first chlorophyll obs on 28mar23


#### Sun 4-Feb-2024

Days since last wwatch3 prep stall: 3


##### ERDDAP

* Successfully re-loaded TWDP ferry obs for 1apr2023 to 30apr2023



### Week 5

#### Mon 5-Feb-2024

Days since last wwatch3 prep stall: 4


##### ERDDAP

* Emailed Rich, Susan & Shumin with update on get_onc_ferry backfilling and link to chlorophyll
  bloom on 8apr23
* Successfully loaded TWDP ferry obs for 1may2023 to 30jun23
* chlorophyll obs end after 6th crossing on 31may23


##### Miscellaneous

Phys Ocgy seminar: Shouyi Wang of MIT re: Indonesian Through-flow (ITF)

Squash-merged dependabot PR to bump codecov-action to 4.0.1 re: feature updates:

* SalishSeaNowcast
* gha-workflows


##### SalishSeaCast

* `crop_gribs 18` timed out due to seeing no files after 8h
* `collect_weather 2.5km 18` finally finished at 17:11; >3h late
* ran `crop_gribs 18 --backfill` at ~18:30 to recover



#### Tue 6-Feb-2024

Days since last wwatch3 prep stall: 0


##### SalishSeaCast

* `make_ww3_current_file forecast2` stalled; killed it and skipped run


##### Miscellaneous

MOAD group mtg; see whiteboard.

Squash-merged dependabot PRs to bump cryptography to 42.0.0 re: CVE-2023-50782
re: remote decryption of captured messages in TLS server that use RSA key
exchanges

* cookiecutter-analysis-repo
* cookiecutter-moad-pkg
* NEMO_Nowcast
* SalishSeaCast/docs
* NEMO-Cmd
* MoaceanParcels
* SalishSeaNowcast
* SalishSeaCmd
* moad_tools
* Reshapr


##### ERDDAP

* Successfully loaded TWDP ferry obs for 1jul2023 to 31aug23


##### MOAD Docs

Fixed broken link that sphinx-linkcheck found in pkg structure docs re:
mambaforge.


##### MoaceanParcels

Fixed broken link re: jinja2T vs. SciPy kernels tutorial.

Researched zarr:

* combining the many small zarr files that Jose gets from Parcels might be a re-chunking operation
* using kerchunk to create a virtual zarr from the nowcast-green netCDF4 files:
  * might allow single dataset access to all variables
  * probably would simplify Reshapr model profile
  * unclear if it would yield performance improvements
  * what is the overhead of running kerchunk daily to add day's run to dataset?
  * Martin Durant, PyData Global 2021: https://www.youtube.com/watch?v=0bqpxX3Nn_A&t=1512s



#### Wed 7-Feb-2024

Days since last wwatch3 prep stall: 1


##### ERDDAP

* Successfully loaded TWDP ferry obs for 1sep2023 to 30nov23; no obs from 17nov23 onward


##### SalishSeaCast

* `upload_forcing orcinus turbidity` failed due to RSA/OPENSSH key issue
  * re-ran successfully at ~17:15
* explored removal of HRDPS continental full domain grib files that we have processed with
  `crop_gribs`
  * first occurrence is in `/results/forcing/atmospheric/continental2.5/GRIB/20230402/00/`


##### SalishSeaTools

Finished work on updating `data_tools.onc_json_to_dataset()` worker to ONC APIv3:

* branch: update-onc_json_to_dataset
* PR#93 - squash-merged

Squash-merged dependabot PR to update jupyterlab to v4.0.11 re: CVE-2024-22421 re: auth & XSRF token
exposure vulnerability.

Updated skookum to main branch.


##### salishsea-site

Continued work on biology page re: no more ciliates figure in V21-11, and name change for turbidity
figure file:

* realized that unit test failures were due to bug that changed biology image loops data
  structure
* cleaned a lot (but not all 🙁) uses of `unittest.mock.patch` out of `test_salishseacast.py`
* forgot to create feature branch, so work is on main 🙁
* added Suchy et al 2023 to publications page (PR#67 - squash-merged)

Squash-merged dependabot PRs to bump cryptography to 42.0.0 re: CVE-2023-50782
re: remote decryption of captured messages in TLS server that use RSA key
exchanges


##### SalishSeaCast/docs

Finished update to Python 3.12:

* branch: py312
* PR#37 - squash-merged

readthedocs build maintenance:

* branch: rtd-build-main
* PR#43 - squash-merged
* change to mambaforge-22.9
* pin sphinx=7.2.6 and install sphinx-rtd-theme from pip

Added Suchy et al 2023 to CITATION.rst:

* branch: suchy-etal-2023
* PR#44 - squash-merged

Added sphinx-notfound-page extension:

* branch: sphinx-notfound-page
* PR#45 - squash-merged


##### SalishSeaNowcast

Continued work on updating `get_onc_ctd` and `get_onc_ferry` workers to ONC APIv3:

* branch: onc-api-v3
* PR#234
* pushed `get_onc_ctd` changes and updated skookum

Started work on adding `make_averaged_dataset` to workflow:

* branch: TDB
* PR#TBD
* changed config to log to nowcast logs instead of hindcast
* added code to `after_download_results()` to launch worker for biology, chemistry & physics
  variable groups
* copied changes to skookum for testing
* restarted manager to load updated config and `next_workers` module



#### Thu 8-Feb-2024

Days since last wwatch3 prep stall: 2


##### ERDDAP

* `get_onc_ferry` ran overnight via automation to collect 7feb24 as a side effect of yesterday's
  manager restart for the `make_averaged_dataset` test
* `get_onc_ferry` found no TWDP ferry obs for 1dec2023 to 29jan24


##### Miscellaneous

VSCode 1.86.1 released with fallback to legacy server for old glibc in place until Feb-2025.

Discussed code and data archives for Suchy, et al 2024 with Karyn.


##### SalishSeaNowcast

Continued work on updating `get_onc_ctd` and `get_onc_ferry` workers to ONC APIv3:

* branch: onc-api-v3
* PR#234
* improved and pushed `get_onc_ferry` tests
* confirmed that issue #174 from pandas 2.0.0 resampling is resolved and removed test skip
* added `ferry data` YAML config and unit tests for it
* updated ERDDAP dataset id for ferry obs in YAML config
* worked on improving test coverage of `get_onc_ferry`


TODO:

* rename make_runoff_file to make_v201702_runoff_file
* rename make_v202111_runoff_file to make_runoff_file
* update `compare_venus_ctd` fig module re: ONC API v3, then drop dev model elements
* add config tests for `run type[*][mesh mask]`
* add config tests for `run type[*][bathymetry]`
* add config tests for `run type[*][land processor elimination]`
* add config tests for `run type[*][run sets dir]`
* improve test_run_NEMO test for forcing symlinks ??
* add tests for _upload_*_files in upload_forcing
* `make_averaged_dataset`:
  * drop host arg
  * add `make_averaged_dataset month *` to `after_make_averaged_dataset physics`
      at month-end, or maybe use race condition mgmt ??


##### SalishSeaCast

* `make_averaged_dataset` failed in automation for biology and physics with KeyErrors; maybe due to
  trying to run them concurrently
  * re-ran successfully manually



#### Fri 9-Feb-2024

Days since last wwatch3 prep stall: 3


##### ERDDAP

Emailed Rich, et al re: finish of ferry obs backfilling and take-over of daily collection by
automation:

* noted that interesting instruments are off most of the time
* Rich emailed Steve Mihaly with questions; replies from Steve and Alice Bui


##### SalishSeaCast

* `get_onc_ferry` failed with IndexError in `_qaqc_filter()`; maybe bug due to partial day of obs?
* `make_averaged_dataset` worked correctly in automation for all 3 variable groups


##### Stakeholder Support

* Started work on my version of current correction notebook in
  `analysis-doug/notebooks/EMSA-currents/explore_current_correction.ipynb` to cross-check Peter's
  method
* emailed Peter to confirm that AIS created times are UTC


##### Miscellaneous

IOS seminar: Youyu Lu re: BC shelf seal level variations from sub-synoptic to interannual time scales

Helped Karyn with code and data archives for Suchy, et al 2024:



#### Sat 10-Feb-2024

Days since last wwatch3 prep stall: 4


##### SalishSeaCast

* `get_onc_ferry` failed with no response for obs request
* `make_averaged_dataset` failed in automation for chemistry with KeyErrors; maybe due to
  trying to run them concurrently
  * re-ran successfully manually



#### Sun 11-Feb-2024

Days since last wwatch3 prep stall: 5


##### SalishSeaCast

* `get_onc_ferry` failed with no response for obs request
* `run_NEMO_agrif` failed due to sftp error
  * re-ran `make_forcing_links nowcast-agrif` to restart
* `make_averaged_dataset` worked correctly in automation for all 3 variable groups



### Week 6

#### Mon 12-Feb-2024

Days since last wwatch3 prep stall: 6


##### SalishSeaCast

* `get_onc_ferry` failed with no response for obs request
* email from MSC re: HPFX AMQP downtime in 02:00 to 04:00 window on 13feb; queues will have to be
  restarted; might impact `collect_weather 06`
* automation stalled at 09:22
  * manager didn't acknowledge completion of forecast run
  * restarted log_aggregator; no effect
  * restarted message_broker; no effect
  * killed `watch_NEMO forecast` on arbutus
  * restarted manager
  * manually restarted automation by running `after_watch_NEMO("forecast")` workers:
    * on `skookum`:
      * download_results arbutus forecast
      * upload_forcing arbutus turbidity
      * upload_forcing orcinus turbidity
      * upload_forcing optimum turbidity
      * upload_forcing graham-dtn turbidity
    * on `arbutus`:
      * make_ww3_wind_file arbutus forecast
* `make_averaged_dataset` worked correctly in automation for all 3 variable groups


##### Stakeholder Support

* Peter to confirmed that AIS created times are UTC
* Serge confirmed that I can push notebook to public repo with AIS dataframe visible
* pushed WIP notebook


##### Miscellaneous

Helped Karyn with code and data archives for Suchy, et al 2024:

* install SalishSeaTools from GitHub ??
* helped Karyn create v2024.02.12 release and got auto-generated DOI from Zenodo



#### Tue 13-Feb-2024

Days since last wwatch3 prep stall: 7


##### SalishSeaCast

* `get_onc_ferry` failed with no response for obs request
* sarracenia clients were apparently unaffected by HPFX AMQP downtime in 02:00 to 04:00 window;
  or the downtime didn't happen?
* `make_averaged_dataset` worked correctly in automation for all 3 variable groups


##### Miscellaneous

MOAD group mtg; see whiteboard.


##### SalishSeaTools

Explored Karyn's report of
`The provided grid type is not in tols. Use another grid type or add your grid type to tols.`
message from `geo_tools.find_closest_model_point()`


##### Stakeholder Support

* Continued work on my version of current correction notebook in
  `analysis-doug/notebooks/EMSA-currents/explore_current_correction.ipynb` to cross-check Peter's
  method
* set up Zoom for Dan, David, Susan & Camryn



#### Wed 14-Feb-2024

Days since last wwatch3 prep stall: 8


##### SalishSeaCast

* `get_onc_ferry` failed with IndexError in `_qaqc_filter()`; maybe bug due to partial day of obs?
* `upload_forcing orcinus forecast2` failed
* `upload_forcing orcinus nowcast+` failed; success on manual re-run
* `upload_forcing orcinus turbidity` failed repeatedly
* started new `make_averaged_dataset` tmux session following deployment docs that smart past me wrote
* `make_averaged_dataset` worked correctly in automation for all 3 variable groups
* `upload_forcing orcinus turbidity` success at 12:20, but NEMO failed very soon after launch


##### Miscellaneous

Narrowly averted `salish` swap-trash; killed dask cluster and its tmux session along the way



#### Thu 15-Feb-2024

Days since last wwatch3 prep stall: 9


##### SalishSeaCast

* `get_onc_ferry` was successful
* backfilled nowcast-agrif:
  * wait for run to fail
  * `upload_forcing orcinus nowcast+ 2024-02-14`
  * `upload_forcing orcinus turbidity 2024-02-14`
  * wait for run to finish
  * `make_forcing_links orcinus nowcast-agrif 2024-02-15`
* `make_averaged_dataset` worked correctly in automation for all 3 variable groups


##### SalishSeaTools

* Worked on Karyn's report of
  `The provided grid type is not in tols. Use another grid type or add your grid type to tols.`
  message from `geo_tools.find_closest_model_point()`
  * branch: improve-find_closest_model_point
  * PR#
  * fixed unit tests that were failing after addition of raiseOutOfBounds param to
    find_closest_model_point()
  * cleaned up test_geo_tools: unused imports and blacken
  * added `continental2.5` tolerances by copying `GEM2.5`
  * created test and demo notebook and pushed it as a Gist:
      https://gist.github.com/douglatornell/95c55fd80b20ac74eeceb45f89199ba0



#### Fri 16-Feb-2024

Days since last wwatch3 prep stall: 10


##### SalishSeaCast

* nowcast-agrif was very slow, then stalled at 10.4%, then rallied and finished strongly
* `make_averaged_dataset` worked correctly in automation for all 3 variable groups


##### Stakeholder Support

* Continued work on my version of current correction notebook in
  `analysis-doug/notebooks/EMSA-currents/explore_current_correction.ipynb` to cross-check Peter's
  method



#### Sat 17-Feb-2024

Days since last wwatch3 prep stall: 11


##### SalishSeaCast

* `crop_gribs 06` stalled with 1 file unprocessed
* `watch_ww3 forecast2` failed to launch due to no port
  * `watch_ww3 forecast` from yesterday did not shut down
    * manager didn't acknowledge its finish message
    * `watch_ww3 forecast2` for today ran okay, but wasn't watched
  * recovery:
    * killed `watch_ww3`
    * `download_wwatch3_results forecast 2024-02-16`
    * `download_wwatch3_results forecast2 2024-02-17`
    * both caused the manager to crash due to missing no `WWATCH3 run` key in checklist; my bad
* `crop_gribs 12` stalled with 1 file unprocessed
* manager crashes resulted in loss of race condition management state, so nothing happened when
  `grib_to_netcdf nowcast+` finished
  * recovery:
    * `make_live_ocean_files`
* restarted log_aggregator
* `run_NEMO_agrif` stalled


##### Security Updates

Squash-merged dependabot PR to update cryptography to v42.0.2 re: CVE-2024-0727 re:
DoS attack vulnerability:

* cookiecutter-MOAD-pypkg
* Reshapr
* NEMO-Cmd
* moad_tools
* cookiecutter-analysis-repo
* SalishSeaCmd
* MoaceanParcels
* SalishSeaNowcast
* salishsea-site
* NEMO_Nowcast



#### Sun 18-Feb-2024

Days since last wwatch3 prep stall: 0


##### SalishSeaCast

* `make_ww3_wind_file forecast2` stalled; killed it and skipped run
* motd from Friday on orcinus says that /scratch is de-synchronized and repairs are in progress;
  it will go unavailable at times, which is probably what happened to our run yesterday
* `run_NEMO_agrif` failed due to no run yesterday; tried to run yesterday and it stalled
* `make_averaged_dataset` failed in automation for chemistry and biology
  * re-ran successfully manually for chemistry
  * it appears that today's biology is one of those day's runs where the worker just won't finish
* `make_ww3_wind_file forecast` stalled; killed it and re-ran it manually; took 2 tries

Email from Mark re: orcinus /scratch recovery causing agrif runs to fail



### Week 9

#### Mon 19-Feb-2024

**Statutory Holiday** - Family Day

Days since last wwatch3 prep stall: 1


##### SalishSeaCast

* ran `day_avg 2024-02-18 biology` in `/results2/SalishSeaCast/month-avg.202111/` on `salish`
  in `make_averaged_dataset` tmux session to deal with yesterday's averaging problem
* `make_averaged_dataset` worked correctly in automation for all 3 variable groups today


##### Stakeholder Support

* Replied to email from Stewart Putnam, Vashon Island WA, USA, kayaker using oceanconnect and curious
  about SalishSeaCast


#### Tue 20-Feb-2024

Worked at ESB while Rita was at home.

Days since last wwatch3 prep stall: 2


##### SalishSeaCast

* `make_averaged_dataset` failed in automation for biology
  * `KeyError: 'particulate_organic_nitrogen'` from deep in dask in
    `Reshapr/reshapr/core/extract.write_netcdf()`; created issue #121 in Reshapr
  * successfully re-rna manually


##### Miscellaneous

* advised Ilias on recovering from accidentally committing large .db files that can't be pushed to
  GitHub
* advised Susan and Karyn on recovery from uncommitted changes in Karyn's
  `salishsea_tools.eval_tools` module
* reviewed changes in xarray 2024.02.0 release
  * size information in text reprs
  * moving toward pandas frequency string changes; e.g. ME, YE, etc.



#### Wed 21-Feb-2024

Days since last wwatch3 prep stall: 3

Finally found a fix for Vivaldi 1password extension issue due to connection failure between extension
and desktop app!
https://1password.community/discussion/129789/browser-desktop-integration-vivaldi-on-linux-doesnt-work


##### ERDDAP

Messages from ERDDAP complaining about
"java.io.IOException: User limit of inotify watches reached"

* increased max_user_watches limit and restarted ERDDAP including waiting for alert from
  uptimerobot:

  ```bash
  sudo sysctl fs.inotify.max_user_watches=196608
  sudo sysctl -p
  sudo /opt/tomcat/bin/shutdown.sh
  # wait for alert
  sudo /opt/tomcat/bin/startup.sh
  ```


##### SalishSeaCast

* `make_averaged_dataset` worked correctly in automation for all 3 variable groups today


##### Minecraft

Tested running a fabric server on khawla:

* refs:
  * https://www.youtube.com/watch?v=sg91I4vg7ew
  * https://hub.tcno.co/games/minecraft/1.20/server/fabric/
  * https://fabricmc.net/use/installer/
  * https://www.curseforge.com/minecraft/mc-mods/fabric-api
* downloaded universal .jar installer and ran it
* set Xmx to 6G
* launched server
* edited eula.txt to accept
* downloaded fabric API and dropped it in mods/
* launched server again
* just works, even with IPv6 address in client


##### Security Updates

Squash-merged dependabot PR to update cryptography to v42.0.4 re: CVE-2024-26130 re:
a NULL pointer dereference that can crash Python:

* cookiecutter-MOAD-pypkg
* cookiecutter-analysis-repo
* SalishSeaNowcast
* salishsea-site
* NEMO-Cmd
* MoaceanParcels
* SalishSeaCmd
* Reshapr
* moad_tools
* NEMO_Nowcast
* cookiecutter-djl-pypkg



#### Thu 22-Feb-2024

Days since last wwatch3 prep stall: 4


##### ERDDAP

Tried to re-run get_onc_ferry for 9-13 Feb because email from Alice@ONC on 15-Feb suggested that
data on ONC side exists but needed to be re-processed; only got some obs for 9-Feb


##### Stakeholder Support

* Continued work on my version of current correction notebook in
  `analysis-doug/notebooks/EMSA-currents/explore_current_correction.ipynb` to cross-check Peter's
  method


##### SalishSeaCast

* `make_averaged_dataset` worked correctly in automation for all 3 variable groups today
* `crop_gribs 18` reported that `003/20240222T18Z_MSC_HRDPS_APCP_Sfc_RLatLon0.0225_PT003H.grib2`
  was not downloaded
  * it is not on hpfx
  * we don't need it for tomorrow's `grib_to_netcdf`
  * automation is stopped
  * recovery:

    ```bash
    # kill collect_weather 18
    collect_weather 00 2.5km
    crop_gribs 00 2024-02-23
    download_weather 12 1km
    ```

    * can't run `download_weather 00 1km` because files have been purged from MSC server


##### Reshapr

* built new dev env on khawla
* did `pre-commit autoupdate`



#### Fri 23-Feb-2024

Days since last wwatch3 prep stall: 5

##### SalishSeaCast

* `crop_gribs 00` reported that `003/20240223T00Z_MSC_HRDPS_APCP_Sfc_RLatLon0.0225_PT003H.grib2`
  was not downloaded
  * it is not on hpfx
  * we need it for `grib_to_netcdf`
  * automation is stopped
  * recovery:

    ```bash
    # kill collect_weather 00
    download_weather 06 2.5km
    crop_gribs 06 --backfill
    # wait for forecast2 runs to finish
    # make_ww3_wind_file stalled; killed and skipped run
    # `003/20240223T00Z_MSC_HRDPS_APCP_Sfc_RLatLon0.0225_PT003H.grib2` appeared on hpfx at 09:46
    curl -LO .../003/20240223T00Z_MSC_HRDPS_APCP_Sfc_RLatLon0.0225_PT003H.grib2
    crop_gribs 00 --var-hour 003 --var APCP_Sfc
    download_weather 12 2.5km
    crop_gribs 12
    collect_weather 18 2.5km
    crop_gribs 18
    crop_gribs 12 --var-hour 001 --UGRD_AGL-10m
    ```

* email conversation w/ Sandrine confirmed that there is a systematic problem with the
  hour 003 APCP_Sfc file
* `collect_weather 18 2.5km` didn't get 003 APCP_Sfc file because it is missing from HPFX
  * recovery:

    ```bash
    collect_weather 00 2.5km
    crop_gribs 00 2024-02-24
    download_weather 00 1km
    download_weather 12 1km
    # kill crop_gribs 18
    # kill collect_weather 18 2.5km
    ```

* `make_averaged_dataset` worked correctly in automation for all 3 variable groups today
* cleaned up `/SalishSeaCast/datamart/hrdps-continental/`
* no 003 hour APCP_Sfc files for 18 or 00 forecasts


##### Reshapr

Made MS the frequency alias of choice for month resampling without breaking backward
compatibility for config where M was used:

* re: deprecation of M in pandas 2.2.0
* branch: month-resampling-MS-freq-alias
* PR#123 - squash-merged



#### Sat 24-Feb-2024

Days since last wwatch3 prep stall: 6

##### SalishSeaCast

* no 003 hour APCP_Sfc files for 06 or 12 forecasts
  * need that file from 00 and 12 for `grib_to_netcdf nowcast+`
* `upload_forcing forecast2` failed due to:

    ```text
    FileExistsError: [Errno 17] File exists: '/results/forcing/sshNeahBay/obs/ssh_y2024m02d23.nc'
     -> '/results/forcing/sshNeahBay/fcst/ssh_y2024m02d23.nc'
    ```

  because nothing from `after_collect_weather 06` ran 😱
  * recovery started at ~09:15:

    ```bash
    # kill collect_weather 18 00 06
    bash /SalishSeaCast/datamart/hydrometric/collect_river_data.sh 2024-02-23  # ECCC rivers
    collect_NeahBay_ssh 00
    get_onc_ctd SCVIP
    get_onc_ctd SEVIP
    get_onc_ferry TWDP
    ```

    * skipped forecast2 runs
* `collect_weather 12 2.5km` and `crop_gribs 12` were not launched
  * sarracenia client collected 527 or 528 12Z files
  * recovery started at ~09:45:

    ```bash
    crop_gribs 12
    collect_weather 12 2.5km --backfill --backfill-date 2024-02-24
    ```

    * `collect_weather` failed due to missing 003 APCP_Sfc file, but it moved all but 2 files into
      `/results/forcing/...`
      * manually moved those files
    * continued recovery:

      <!-- markdownlint-disable MD013 -->
      ```bash
      collect_weather 18 2.5km
      crop_gribs 18
      # wait for crop_gribs to stall with 1 file (003 APCP_Sfc) unprocessed
      # kill crop_gribs 12
      # copy the cropped 009 APCP_Sfc files from the previous 18Z and 06Z forecasts to create
      # best estimates of 00Z and 12Z 003 APCP_Sfc files
      cp /results/forcing/atmospheric/continental2.5/GRIB/20240223/18/009/20240223T18Z_MSC_HRDPS_APCP_Sfc_RLatLon0.0225_PT009H_SSC.grib2 \
        /results/forcing/atmospheric/continental2.5/GRIB/20240224/00/003/20240224T00Z_MSC_HRDPS_APCP_Sfc_RLatLon0.0225_PT003H_SSC.grib2
      cp /results/forcing/atmospheric/continental2.5/GRIB/20240224/06/009/20240224T06Z_MSC_HRDPS_APCP_Sfc_RLatLon0.0225_PT009H_SSC.grib2 \
        /results/forcing/atmospheric/continental2.5/GRIB/20240224/12/003/20240224T12Z_MSC_HRDPS_APCP_Sfc_RLatLon0.0225_PT003H_SSC.grib2
      grib_to_netcdf
      bash /SalishSeaCast/datamart/hydrometric/collect_USGS_river_data.sh 2024-02-23
      make_turbidity_file
      collect_NeahBay_ssh 06
      download_live_ocean
      ```
      <!-- markdownlint-enable MD013 -->

    * nowcast-blue run started on arbutus at ~11:00
* `make_averaged_dataset` worked correctly in automation for all 3 variable groups today
* `collect_weather 18 2.5km` didn't get 003 APCP_Sfc file because it is missing from HPFX
  * recovery:

    ```bash
    collect_weather 00 2.5km
    crop_gribs 00 2024-02-25
    download_weather 00 1km
    download_weather 12 1km
    # kill crop_gribs 18
    # kill collect_weather 18 2.5km
    ```



#### Sun 25-Feb-2024

Days since last wwatch3 prep stall: 0

##### SalishSeaCast

* I forgot to start `collect_weather 06 2.5km` and `crop_gribs 06` before I went to bed,
  but that might have been a good thing in retrospect because I have less manual work to do today
* no 003 hour APCP_Sfc files for 00, 06, or 12 forecasts
  * recovery started at ~09:15:
    * hacked `collect_weather` to ignore FileNotFoundError

    <!-- markdownlint-disable MD013 -->
    ```bash
    # kill collect_weather 00 2.5km
    crop_gribs 06
    collect_weather 06 2.5km --backfill --backfill-date 2024-02-25
    # automation ran `collect_river_data ECCC`, `collect_NeahBay_ssh 00`, `get_onc_ctd`,
    # `get_onc_ferry`, , `collect_weather 12`, and `crop_gribs 12`
    # kill `collect_weather 12`
    # wait for `crop_gribs 06` to stall with 1 file (003 APCP_Sfc) unprocessed
    # kill `crop_gribs 06`
    collect_weather 12 2.5km --backfill --backfill-date 2024-02-25
    # automation ran `collect_river_data USGS`, `collect_NeahBay_ssh 06`, `make_turbidity_file`,
    # `download_live_ocean`, `collect_weather 18`, and `crop_gribs 18`
    # wait for `crop_gribs 12` to stall with 1 file (003 APCP_Sfc) unprocessed
    # kill crop_gribs 12
    # copy the cropped 009 APCP_Sfc files from the previous 18Z and 06Z forecasts to create
    # best estimates of 00Z and 12Z 003 APCP_Sfc files
    cp /results/forcing/atmospheric/continental2.5/GRIB/20240224/18/009/20240224T18Z_MSC_HRDPS_APCP_Sfc_RLatLon0.0225_PT009H_SSC.grib2 \
      /results/forcing/atmospheric/continental2.5/GRIB/20240225/00/003/20240225T00Z_MSC_HRDPS_APCP_Sfc_RLatLon0.0225_PT003H_SSC.grib2
    cp /results/forcing/atmospheric/continental2.5/GRIB/20240225/06/009/20240225T06Z_MSC_HRDPS_APCP_Sfc_RLatLon0.0225_PT009H_SSC.grib2 \
      /results/forcing/atmospheric/continental2.5/GRIB/20240225/12/003/20240225T12Z_MSC_HRDPS_APCP_Sfc_RLatLon0.0225_PT003H_SSC.grib2
    grib_to_netcdf
    ```
    <!-- markdownlint-enable MD013 -->

    * nowcast-blue run started on arbutus at ~10:50
* `make_averaged_dataset` worked correctly in automation for all 3 variable groups today
* `make_ww3_wind_file forecast` stalled; killed it and re-ran it manually; took 2 tries
* `collect_weather 18 2.5km` didn't get 003 APCP_Sfc file because it is missing from HPFX
  * recovery started at ~15:15:

    ```bash
    download_weather 00 1km
    download_weather 12 1km
    # wait for `crop_gribs 18` to report unprocessed file at ~18:00
    # kill collect_weather 18 2.5km
    collect_weather 00 2.5km
    crop_gribs 00 2024-02-26
    ```



### Week 10

#### Mon 26-Feb-2024

Days since last wwatch3 prep stall: 1


##### SalishSeaCast

* I started `collect_weather 00 2.5km` and `crop_gribs 00` to late ast evening
  (after 00Z files were being collected by sarracenia)
* no 003 hour APCP_Sfc files for 00, 06, or 12 forecasts
  * recovery started at ~08:55:

    <!-- markdownlint-disable MD013 -->
    ```bash
    # kill collect_weather 00 2.5km
    crop_gribs 00
    collect_weather 00 2.5km --backfill --backfill-date 2024-02-26
    # `crop_gribs 00` finished with unprocessed files, and that launched `crop_gribs 06`
    # kill `collect_weather 00 2.5km` that can never finish
    # fix files that `crop_gribs 00` missed
    crop_gribs 00 --debug --var-hour 001 --var APCP_Sfc
    crop_gribs 00 --debug --var-hour 009 --var PRMSL_MSL
    crop_gribs 00 --debug --var-hour 023 --var APCP_Sfc
    crop_gribs 00 --debug --var-hour 023 --var DSWRF_Sfc
    crop_gribs 00 --debug --var-hour 023 --var LHTFL_Sfc
    crop_gribs 00 --debug --var-hour 023 --var PRMSL_MSL
    crop_gribs 00 --debug --var-hour 023 --var SPFH_AGL-2m
    # wait for sarracenia to finish collecting 12Z files to avoid partial processing
    collect_weather 06 2.5km --backfill --backfill-date 2024-02-26
    # automation ran `collect_river_data ECCC`, `collect_NeahBay_ssh 00`, `get_onc_ctd`,
    # `get_onc_ferry`, , `collect_weather 12`, and `crop_gribs 12`
    # kill `collect_weather 12`
    # wait for `crop_gribs 06` to stall with 1 file (003 APCP_Sfc) unprocessed
    # kill `crop_gribs 06`
    collect_weather 12 2.5km --backfill --backfill-date 2024-02-26
    # automation ran `collect_river_data USGS`, `collect_NeahBay_ssh 06`, `make_turbidity_file`,
    # `download_live_ocean`, `collect_weather 18`, and `crop_gribs 18`
    # wait for `crop_gribs 12` to stall with 1 file (003 APCP_Sfc) unprocessed
    # kill crop_gribs 12
    # copy the cropped 009 APCP_Sfc files from the previous 18Z and 06Z forecasts to create
    # best estimates of 00Z and 12Z 003 APCP_Sfc files
    cp /results/forcing/atmospheric/continental2.5/GRIB/20240225/18/009/20240225T18Z_MSC_HRDPS_APCP_Sfc_RLatLon0.0225_PT009H_SSC.grib2 \
      /results/forcing/atmospheric/continental2.5/GRIB/20240226/00/003/20240226T00Z_MSC_HRDPS_APCP_Sfc_RLatLon0.0225_PT003H_SSC.grib2
    cp /results/forcing/atmospheric/continental2.5/GRIB/20240226/06/009/20240226T06Z_MSC_HRDPS_APCP_Sfc_RLatLon0.0225_PT009H_SSC.grib2 \
      /results/forcing/atmospheric/continental2.5/GRIB/20240226/12/003/20240226T12Z_MSC_HRDPS_APCP_Sfc_RLatLon0.0225_PT003H_SSC.grib2
    grib_to_netcdf
    ```
    <!-- markdownlint-enable MD013 -->

    * nowcast-blue run started on arbutus at ~11:19
* email from Sandrine at 12:34 saying that issue should be resolved in 18Z forecast thanks to
  rollback of an operational installation change
  * `collect_weather 18 2.5km` was successful!
* `make_averaged_dataset` worked correctly in automation for all 3 variable groups today


##### Miscellaneous

Squash-merged dependabot PRs to bump mamba-org/setup-micromamba to 1.8.1 re: bug fixes & dependency
updates:

* SalishSeaNowcast
* rhwhite/numeric_2024
* erddap-datasets
* gha-workflows
* salishsea-site

Squash-merged dependabot PRs to bump codecov/codecov-action to 4.0.2 re: new features & dependency
updates:

* SalishSeaNowcast
* gha-workflows

Checked status of scheduled GHA workflows:

  ```bash
  conda activate gha-workflows
  python /media/doug/warehouse/MOAD/gha-workflows/gha_workflow_checker/gha_workflows_checker.py
  ```

Phys Ocgy seminar: Patrick Pata; zooplankton in NE Pacific:

* all cluster analysis, all the time
* brooding zooplankton


##### SalishSeaNowcast

Resumed work on updating `get_onc_ctd` and `get_onc_ferry` workers to ONC APIv3:

* branch: onc-api-v3
* PR#234
* tidied changes in PyCharm
* pushed ONC_data_product_url attr updates



#### Tue 27-Feb-2024

Days since last wwatch3 prep stall: 1

Worked at ESB until snow started to fall in early afternoon.

##### SalishSeaCast

* automation worked smoothly
* `make_averaged_dataset` worked correctly in automation for all 3 variable groups today


##### Miscellaneous

* MOAD mtg; see whiteboard
* researched graham StdEnv/2023 that becomes default in April
  * default compiler suite changes from Intel to GCC 12.3, Intel 2023 available
  * new version of OpenMPI
* EOAS colloquium: Martyn Unsworth, Magnetotellurics: Using natural radio waves to look inside the Earth
* helped Becca get ssh-agent running on her new Windows laptop
* couldn't reproduce Susan's permissions problem (reported on Slack) accessing in Cassidy's files
  on /ocean
* dug into Susan's optimum nemo build messages (reported on Slack) about libm, libpthread, and libc



#### Wed 28-Feb-2024

Days since last wwatch3 prep stall: 2


##### SalishSeaCast

* https://github.com/xCDAT/xcdat/issues/561 that I followed because it
  is about `RuntimeError: NetCDF: Not a valid ID`, `xarray.open_dataset()` and `dask` was updated
  this morning with the comments:

    To summarize in this thread, it looks like a work-around in netcdf4-python to deal with netcdf-c
    not being thread safe was removed in 1.6.1. The solution (for now) is to
    [make sure your cluster only uses 1 thread per worker](https://forum.access-hive.org.au/t/netcdf-not-a-valid-id-errors/389/14).

    It seems like some file systems do not like parallel access to files. The workaround seems to be
    to set parallel=False
* `make_averaged_dataset` failed in automation for biology:

  ```text
  distributed.scheduler.KilledWorker:
  Attempted to run task ('blocks-transpose-store-map-a62e9852789c59ac17cce07a3f6fde5c', 0, 0, 0, 0)
  on 3 different workers, but all those workers died while running it. The last worker that attempt
  to run the task was tcp://127.0.0.1:42457. Inspecting worker logs is often a good next step to
  diagnose what went wrong. For more information see https://distributed.dask.org/en/stable/killed.html.
  ```

* killed dask workers in xxx on `salish` and restarted them with 1 thread each:

  ```bash
  dask worker --nworkers=4 --nthreads=1 --memory-limit auto \
    --local-directory /dev/shm \
    --lifetime 3600 --lifetime-stagger 60 --lifetime-restart \
    localhost:4386
  ```


##### ERDDAP

Emailed Alice to ask if TWDP data stream interruption is continuation of cache issue from 9-14 Feb


##### Miscellaneous

Sharcnet colloquium: Debugging with DDT

* Sergey Mashchenko, McMaster
* DDT installed on `graham` and `niagara`
* commercial, designed for HPC, "tens of thousands of $ per year for license"
* primarily for compiled languages, but now Python too
* DDT wiki page on Alliance docs
* graham:
  * ddt-cpu.23.1.1, max 64 cores across all users, StdEnv/2023, annual license
  * ddt-cpu.22.0.1, max 128 cores, StdEnv/2020, perpetual license
* GUI, use X11 forwarding or VNC
* use salloc for interactive session, sbatch is possible
  * `ssh -Y`
  * `salloc --x11 ...`
  * `mpicc -g`
  * `module load ddt-cpu`
  * `ddt path/to/executable`
* can debug optimized code, but `-O0` may be easier to understand because optimized executables can
  be non-linear
* Python a little more complicated
* VNC may be faster; Sergey's `syam/bin/VNC` simplifies setup
* examples in `syam/DDT_2024/`
* can attach to already running program to debug code run by sbatch
* can analyze core files
* can periodically dump state of sbatch run, also offline breakpoints and tracepoints

Helped Susan with getting Cassidy's river tracers NEMO config running on optimum:

* couldn't pull repo updates from GitHub due to `unsupported key type` error
  * trying to use `salishsea-nowcast-deployment_id_rsa` deployment key failed because OpenSSH client
    on optimum is too old
  * after a long trash of trying to work around client issue, finally succeeded by using https
    **note: this will only work for public repos**



#### Thu 29-Feb-2024

Days since last wwatch3 prep stall: 0


##### SalishSeaCast

* `make_ww3_wind_file forecast2` stalled; killed it and skipped run
* ran `day_avg 2024-02-28 biology` in `/results2/SalishSeaCast/month-avg.202111/` on `salish`
  in `make_averaged_dataset` tmux session to deal with yesterday's averaging problem
  * same error as came from worker yesterday!
  * dask workers complaining about high unmanaged memory
  * increased number of dask workers to 6; same high unmanaged memory messages and error
  * tested 27feb biology that was successful in worker; same issues
  * changed back to 4 workers, but with 2 threads each
    * 27feb biology succeeded
    * 28feb biology failed with same high unmanaged memory messages and error
* `make_averaged_dataset` failed in automation for biology with `RuntimeError: NetCDF: HDF error`
  * retried with manual re-run of `make_averaged_dataset skookum day biology 2024-02-29`
* `make_averaged_dataset` failed in automation for chemistry with `KeyError: 'total_alkalinity'`
  * successful manual re-run of `make_averaged_dataset skookum day chemistry 2024-02-29`
    but with lots of messages about unmanaged memory, then HDF5 attribute errors worker logs on
    `salish`
* changed back to 4 workers, but with 4 threads each
  * successfully ran `day_avg 2024-02-28 biology` in `/results2/SalishSeaCast/month-avg.202111/`
    on `salish`
* ran:

  ```bash
  make_averaged_dataset skookum month physics 2024-02-01
  make_averaged_dataset skookum month chemistry 2024-02-01
  make_averaged_dataset skookum month biology 2024-02-01
  ```

  successfully, but with lots of HDF5 attribute error messages in worker logs on `salish`
* `crop_gribs 18` timed out after 8 hours with 216 unprocessed files
  * `collect_weather 18 2.5km` finished at 16:12
  * ran `crop_gribs $NOWCAST_YAML 18 --backfill` to finish processing late files


##### SS150

Read email from Michael and scanned attached Word do re: integration of IOS SS150 NEMO config
into SalishSeaCast.


##### UBC-DFO Modeling Meeting

Jonathan Izert re: central WCVI FVCOM model:

* sensitive to resolution, FVCOM version, and OS/pkgs version


##### SalishSeaNowcast

Finally finished updating `get_onc_ctd` and `get_onc_ferry` workers to ONC APIv3:

* branch: onc-api-v3
* PR#234 - squash-merged



## March

#### Fri 1-Mar-2023  <!-- markdownlint-disable-line MD001 -->

Days since last wwatch3 prep stall: 1


##### SalishSeaCast

* did more reading about dask worker config, their thread use, and Linux temporary storage
* changed dask cluster on `salish` to:
  * 4 workers
  * 1 thread per worker (from 4)
  * 64G memory per worker (from auto == 32G)
  * local directory on `/tmp` (from `/dev/shm`)
* `make_averaged_dataset` worked correctly in automation for all 3 variable groups today
* got email from Maxime @alliance that robot.graham.alliancecan.ca is ready for use
* sent email to Venkat @arc re: updating arbutus.cloud VMs from 18.04.


##### Bloomcast

* discovered over a year's worth of `/tmp/tmp*.infile`:
    `find /tmp -maxdepth 1 -type f -user dlatorne -name "tmp*.infile" -mtime +3 -ls`
  * cleaned them with:
      `find /tmp -maxdepth 1 -type f -user dlatorne -name "tmp*.infile" -mtime +3 -delete`
* today's run took ~3h; maybe io competition with Ilias's jobs?


##### Miscellaneous

Updated PyCharm on khawla to 2023.3.4.


##### SalishSeaNowcast

Resumed work on adding make_averaged_dataset to automation:

* branch: automate-make_averaged_dataset
* committed previous work:
  * automation of day-avg datasets
  * move logging from hindcast to nowcast log

#### Sat 2-Mar-2023

Days since last wwatch3 prep stall: 2


##### SalishSeaCast

* `make_averaged_dataset` worked correctly in automation for all 3 variable groups today



#### Sun 3-Mar-2023

Days since last wwatch3 prep stall: 3


##### SalishSeaCast

* `make_averaged_dataset` worked correctly in automation for all 3 variable groups today



### Week 10

#### Mon 4-Mar-2024

Days since last wwatch3 prep stall: 4


##### Miscellaneous

Squash-merged dependabot PRs to bump codecov/codecov-action to 4.1.0 re: new features & dependency
updates:

* SalishSeaNowcast
* gha-workflows

`salish` refused logins between 09:30 and 10:00 and was at 99.7% swap when I succeeded to connect

* killed dask cluster and it only recovered slightly
* restarted cluster
* Ilias had stalled jobs that he asked me to kill and swap immediately dropped to normal

Phys Ocgy seminar:

* Jo Langer, UVic
* Is the Cdn Arctic Archipelago a Carbon Sink?

Cleaned up stale `vscode-server` processes on `salish` from Jose, Cassidy & Camryn


##### SalishSeaNowcast

Continued work on adding make_averaged_dataset to automation:

* branch: automate-make_averaged_dataset
* PR#242
* expanded `make_averaged_dataset` message types to `f"success {avg_time_interval} {reshapr_var_group}"`
* changed worker message payload to make run date an item in it instead of part of the key
* added automation of month-avg datasets
* dropped unnecessary host name arg from `make_averaged_dataset`


##### SalishSeaCast

* `make_averaged_dataset` worked correctly in automation for all 3 variable groups today
* `crop_gribs 18` stalled with 1 file unprocessed
  * `20240304T18Z_MSC_HRDPS_APCP_Sfc_RLatLon0.0225_PT020H.grib2` was downloaded, but not processed
  * ran `crop_gribs 18 --var-hour 020 --var APCP_Sfc --debug` (unnecessarily)



#### Tue 5-Mar-2024

Worked at ESB while Rita was at home.

Days since last wwatch3 prep stall: 5


##### Miscellaneous

MOAD mtg; see whiteboard.

Mtg w/ Henryk re: `salish` OS upgrade:

* he is worried about how there only being 2.3G free on `/`, but in the course of
  discussion he realized that be can clean up `/boot/` and get back another 0.4G;
  he will also change the packages download location to avoid that consuming space
  on `/`
* he is also worried by the idiosyncratic, bios-based RAID setup of `/`
* he wants us to plan for downtime of a week or more in case things go badly and
  he has to build `salish` from a clean install of 22.04 LTS
  * the concern with that duration of downtime is most of our storage is
    controlled by `salish`; `lsblk` shows:
    * `/data/`
    * `/opp/`
    * `/results2/`
    * `/SalishSeaCast/`


##### `graham` StdEnv/2023

* unloaded all modules with `module --force purge`
* loaded StdEnv/2023 with `module load StdEnv/2023`

  ```bash
  module list

  Currently Loaded Modules:

  1) CCconfig            5) hwloc/2.9.1        9) ucc/1.2.0        13) StdEnv/2023 (S)
  2) gentoo/2023   (S)   6) ucx/1.14.1        10) openmpi/4.1.5   (m)
  3) gcccore/.12.3 (H)   7) libfabric/1.18.0  11) flexiblas/3.3.1
  4) gcc/12.3      (t)   8) pmix/4.2.4        12) imkl/2023.2.0   (math)

  Where:
  S:     Module is Sticky, requires --force to unload or purge
  m:     MPI implementations / Implémentations MPI
  math:  Mathematical libraries / Bibliothèques mathématiques
  t:     Tools for development / Outils de développement
  H:                Hidden Module
  ```

* loaded modules that XIOS-2 build requires to find new versions:

  ```bash
  module load hdf5-mpi/1.14.2
  module load netcdf-mpi/4.9.2
  module load netcdf-c++4-mpi/4.3.1
  module load netcdf-fortran-mpi/4.6.1
  module load perl/5.36.1
  ```

* created `XIOS-ARCH/ALLIANCE/arch-GCC_GRAHAM.env` with above modules and versions
  (including StdEnv/2023)
* hacked up `XIOS-ARCH/ALLIANCE/arch-GCC_ARBUTUS.fcm` from a combination of
  `XIOS-ARCH/ALLIANCE/arch-GCC_GRAHAM.fcm` and
  `XIOS-2/arch/arch-GCC_LINUX.fcm`
* copied `XIOS-ARCH/ALLIANCE/arch-X64_GRAHAM.path` to `XIOS-ARCH/ALLIANCE/arch-GCC_GRAHAM.path`
* symlinked the GCC files above into XIOS-2/arch/
* cleaned XIOS-2 build with `./tools/FCM/bin/fcm build --clean`
* tried build with `./make_xios --arch GCC_GRAHAM -j8`; failed
* more tries with `./make_xios --arch GCC_GRAHAM` lead to:
  * https://forge.ipsl.jussieu.fr/ioserver/ticket/180
    * added `-std=gnu++11` to `%BASE_CFLAGS`
    * added `#include <array>` in `extern/remap/src/meshutil.cpp`
  * https://stackoverflow.com/questions/71296302/numeric-limits-is-not-a-member-of-std
    * added `#include <limits>` in `extern/remap/src/meshutil.cpp`
* got a successful build with `./make_xios --arch GCC_GRAHAM -j8`


##### Minecraft

Installed 32G of RAM in lizzy so that it can run a fabric server for us.
Set up server:

* refs:
  * https://www.youtube.com/watch?v=sg91I4vg7ew
  * https://hub.tcno.co/games/minecraft/1.20/server/fabric/
  * https://fabricmc.net/use/installer/
  * https://www.curseforge.com/minecraft/mc-mods/fabric-api
* updated OS pkgs
  * sudo apt update
  * sudo apt upgrade
  * sudo apt auto-remove
* installed openjdk-21-jre
  * sudo apt install openjdk-21-jre
* downloaded and installed server launcher:
  * cd /media/doug/warehouse/
  * sudo mkdir MinecraftFabric1.20.4Server
  * sudo chown doug:sada MinecraftFabric1.20.4Server
  * cd MinecraftFabric1.20.4Server
  * curl -OJ https://meta.fabricmc.net/v2/versions/loader/1.20.4/0.15.7/1.0.0/server/jar
* did initial server launch with 6G of memory:
  * java -Xmx6G -jar fabric-server-mc.1.20.4-loader.0.15.7-launcher.1.0.0.jar nogui
* edited eula.txt to accept
* stopped Nodecraft server and created `Phrenic Mandraflora` backup
* downloaded and unzipped backup:
  <!-- markdownlint-disable MD013 -->
  ```bash
  mkdir backups/
  curl -L \
    https://backups-b2.nodecraft.gg/file/nodecraft/7da67f08-a869-4ac8-9844-556df29e7e1e/t6NWX6Qal3Q13B_B1AUFF0MLHG4qN411_ChJNRTCmDZpLr0I57KKLL87AGwIxITH.zip?name=Phrenic%20Mandraflora \
    --output PhrenicMandraflora-Nodecraft-6mar24.zip
  unzip PhrenicMandraflora-Nodecraft-6mar24.zip
  ```
  <!-- markdownlint-enable MD013 -->
* moved `1-20-1-25jul23/` world tree up to `MinecraftFabric1.20.4Server/`
* copied `ops.json` up to `MinecraftFabric1.20.4Server/`
* used VSCode remote session to edit `MinecraftFabric1.20.4Server/server.properties` to sync it with
  the one downloaded from Nodecraft:
    initial-enabled-packs=vanilla,bundle
    level-name=1-20-1-25jul23
    level-seed=3266812394423525333
    max-players=4
    motd=SADA on lizzy
    pvp=false
    server-name=sada
  * left view-distance=10
* created `MinecraftFabric1.20.4Server/start.sh`
    #!/usr/bin/env bash
    java -Xmx6G -jar fabric-server-mc.1.20.4-loader.0.15.7-launcher.1.0.0.jar nogui
* installed `tmux`
* started server in tmux session
    tmux new -s minecraft-server
    window 0: `./start.sh`
    window 2: `top -c`
* started server and ran around
  * 1 lag spike
  * 2 "can't keep up messages in log"



#### Wed 6-Mar-2024

Days since last wwatch3 prep stall: 0


##### SalishSeaCast

* `make_ww3_current_file forecast2` stalled; killed it and skipped run
* set up restricted ssh key pair to use for robot.graham
  `ssh-keygen -t ed25519 -C "SalishSeaCast robot.graham" -f ~/.ssh/SalishSeaCast_robot.graham_ed25519`
  * uploaded public key to CCDB
  * edited `nowcast.yaml`
  * added `robot.graham` to `.ssh/config` on `khawla` (for reference) and `ocean` machines (for `skookum`)
  * successfully tested `upload_forcing robot.graham turbidity`


##### SoPO

* Day 1



#### Thu 7-Mar-2024

Days since last wwatch3 prep stall: 1


##### SalishSeaCast

* forgot to restart manager to load config changes re: `robot.graham` so `upload_forcing forecast2`
  failed; restarted manager before nowcast cycle started and all's good
* Henryk alerted that `/results/` is 99% full; ~340G free
  * experimented with finding and deleting pre-crop continental HRDPS files:
    find  /results/forcing/atmospheric/continental2.5/GRIB/20230403/ -type f \
      -name "*_MSC_HRDPS_*_RLatLon0.0225_PT???H.grib2"
    * ~4G per day across 4 forecasts


##### SoPO

* Day 2


##### SalishSeaNowcast

Finished adding make_averaged_dataset to automation:

* branch: automate-make_averaged_dataset
* PR#242 - squash-merged

Updated Sphinx & sphinx_rtd_theme versions in all envs.

pre-commit autoupdate.

Code style gardening by black

* primary modifications were placing conditional logic inside parentheses in
  order to improve readability and understanding of the code's flow control

Started changing from 'graham-dtn' to 'robot.graham':

* branch: robot.graham
* PR#243



#### Fri 8-Mar-2024

Days since last wwatch3 prep stall: 2


##### SalishSeaNowcast

Finished changing from 'graham-dtn' to 'robot.graham':

* branch: robot.graham
* PR#243 - squash-merged
* worked for `upload_forcing` in production

Changed paths for Cassidy & Susan's river tracers hindcast runs on optimum:

* branch: rivers-hindcast
* PR#245 - squash-merged

Fix bugs re: removal of host name arg from `make_averaged_dataset` worker:

* branch: fix-make_averaged_dataset
* PR#246 - squash-merged

`archive_tarball` for river tracers runs failed due to host key conflict with a key in
`known_hosts`; worked fine in production after I resolved that.



#### Sat 9-Mar-2024

Days since last wwatch3 prep stall: 0


##### SalishSeaCast

* `make_ww3_wind_file forecast2` stalled; killed it and skipped run



#### Sun 10-Mar-2024

Days since last wwatch3 prep stall: 1



### Week 11

#### Mon 11-Mar-2024

Annual water filter service completed.

Days since last wwatch3 prep stall: 2

Phys Ocgy Seminar: Atmospheric Quasi-Stationary Waves



#### Tue 12-Mar-2024

Worked at ESB.

Days since last wwatch3 prep stall: 3


##### Miscellaneous

MOAD mtg; see whiteboard.

Helped Tall get an image of Ubuntu 22.04.4 to rebuild his failed laptop.


##### SalishSeaCast

* `download_live_ocean` failed due to timeout at ~12:10; started again at ~12:35; failed again
  at ~15:35
  * recovery started at ~17:45:
    * used symlink of yesterday's boundary conditions file that `upload_forcing forecast2` made

    ```bash
    upload_forcing arbutus nowcast+
    upload_forcing orcinus nowcast+
    upload_forcing optimum nowcast+
    upload_forcing robot.graham nowcast+
    ```


##### `graham` StdEnv/2023

* tested modified build of `extern/remap/src/meshutil.cpp` under StdEnv/2020
  * cleaned XIOS-2 build with `./tools/FCM/bin/fcm build --clean`
  * successful build with `./make_xios --arch X64_GRAHAM -j8`

* added GCC_GRAHAM arch files to XIOS-ARCH:
  * graham-stdenv2023
  * PR#2

* closed issue #1 on XIOS-2 repo re: changing default branch name from
  `master` to `main`; completed some time ago

* added modified `extern/remap/src/meshutil.cpp` files to XIOS-2:
  * graham-stdenv2023
  * PR#2



#### Wed 13-Mar-2024

Days since last wwatch3 prep stall: 4


##### SalishSeaCast

* `download_live_ocean` failed due to timeout at ~12:04
  * emailed Parker; he was unaware of server problem and has alerted people who maintain it
  * recovery started at ~13:35:
    * used symlink of yesterday's boundary conditions file that `upload_forcing forecast2` made

    ```bash
    upload_forcing arbutus nowcast+
    upload_forcing orcinus nowcast+
    upload_forcing optimum nowcast+
    upload_forcing robot.graham nowcast+
    ```

  * email from Parker at 13:40 to says that server was back and extraction for us should be ready
    within an hour
    * ran `download_live_ocean --debug`
    * ran `make_live_ocean_files --debug`
    * ran `upload_forcing --debug`

* `upload_forcing robot.graham nowcast+` repeated stalled for ~45min after uploading Neah Bay files



#### Thu 14-Mar-2024

Days since last wwatch3 prep stall: 5


##### SalishSeaCast

* got serious about recovering space on `/results/` by deleting pre-cropped continental HRDPS GRIB
  files:
  * deleted apr-dec 2023 files, at least ~135G/month with `find` commands like:

    ```bash
    find  /results/forcing/atmospheric/continental2.5/GRIB/202305??/??/ -type f \
    -name "*_MSC_HRDPS_*_RLatLon0.0225_PT???H.grib2" -delete
    ```


##### ERDDAP Datasets

Started adding V23-02 HRDPS continental grid fields datasets:

* branch: HRDPS-continental
* PR#12
* added ubcSSaAtmosphereGridV23-02 geo-location dataset
* pulled on `skookum`, switched to branch, and loaded dataset via flag file



#### Fri 15-Mar-2024

Days since last wwatch3 prep stall: 6


##### ERDDAP Datasets

Continued adding V23-02 HRDPS continental grid fields datasets:

* branch: HRDPS-continental
* PR#12
* added ubcSSaSurfaceAtmosphereFieldsV23-02 dataset
* pulled on `skookum`, and loaded dataset via flag file


##### SalishSeaCast

* `download_results forecast` failed due to dropped connection; re-ran manually


##### Minecraft

* discovered that client performance has returned to nearly 120 fps, perhaps due to nvidia driver
  updates?
  * installed latest version of iris and contemporary shaders
  * updated sodium, malilib, minihud & tweakeroo along the way
* server crashed while Susan was exploring new chunks
  * preceded by lots of disk activity on lizzy



#### Sat 16-Mar-2024

Days since last wwatch3 prep stall: 7


##### Minecraft

* server crashed while Susan was exploring new chunks
  * moved installation from `warehouse/` spinning volume to `/home/doug/Games/` on ssd
  * fewer lag spikes, and shorter



#### Sun 17-Mar-2024

Days since last wwatch3 prep stall: 8



### Week 12

#### Mon 18-Mar-2024

Days since last wwatch3 prep stall: 9


##### SalishSeaCast docs

* Resolved some of the broken links issues for `forge.ipsl.jussieu.fr` by changing to
  `forge.jussieu.fr` alias that  was published in XIOS email list on 14mar
  * works for XIOS links and for NEMO ticket links
  * NEMO code links go to 404 page due to 2022 migration to `forge.nemo-ocean.eu`


##### `graham` StdEnv/2023

Worked on NEMO build using SalishSeaCast config:

* unloaded all modules with `module --force purge`
* loaded env and modules for NEMO build:

  ```bash
  module load StdEnv/2023
  module load netcdf-fortran-mpi/4.6.1
  module load perl/5.36.1
  ```

* created `ARCH/UBC_EOAS/arch-GCC_GRAHAM.fcm` with guidance from `GCC_SOCKEYE.fcm` and `GCC_ARBUTUS.fcm`
* to get correct include path for `netcdf.mod`, had to add:

  ```text
  %NCDF_HOME           $EBROOTNETCDFMINFORTRAN

  %NCDF_INC            -I%NCDF_HOME/include
  ```

* to avoid
  `Error: Type mismatch between actual argument at (1) and actual argument at (2) (REAL(8)/INTEGER(4)).`
  in `lib_mpp.f90`, had to add `-fallow-argument-mismatch` to `%FCFLAGS`
* successful build
* NEMO-3.6-code:
  * branch: graham-stdenv2023
  * PR#7
* SalishSeaCast/docs:
  * branch: graham-stdenv2023
  * PR#46


##### Miscellaneous

Phys Ocgy Seminar: Leonardo Alvarado, Satellites & Phytoplankton; Atmospheric Trace Gas Measurement

Tried to help Ilias with odd xarray behaviour as he combines diatom arrays and cluster indices.



#### Tue 19-Mar-2024

Worked at ESB while Rita was at home.

Days since last wwatch3 prep stall: 10


##### Miscellaneous

Raisha & Sara on campus.

MOAD group mtg; see whiteboard.

EOAS Colloquium: Tsunami 11th Relative documentary by Pieter Romer of ONC.

Coffee w/ Raisha.


##### SalishSeaCmd

Updated module loads to Alliance StdEnv/2023:

* branch: graham-stdenv2023
* PR#62



#### Wed 20-Mar-2024

Days since last wwatch3 prep stall: 11


##### Miscellaneous

* tried to resolve recent issue where Codecov report comments no longer appear in PRs
  * created Codecov token for SalishSeaCast org
  * added token to shared GHA workflow in gha-workflows
  * test with re-run of action in SalishSeaCmd PR#62 failed, but it may not be a good test


##### Security Updates

Squash-merged dependabot PRs to update black to v24.3.0 re: CVE-2024-21503 re: ReDoS vulnerability:

* cookiecutter-MOAD-pypkg
* MoaceanParcels
* gha-workflows
* NEMO_Nowcast
* salishsea-site
* NEMO-Cmd
* moad_tools
* AtlantisCmd
  * readthedocs build failed for PR
* Reshapr
* SalishSeaNowcast


##### `graham` StdEnv/2023

* continued work on testing GCC-12 build on `graham`
  * pulled changes in SS-run-sets
  * pulled changes in XIOS-ARCH and switched to graham-stdenv2023 branch
  * pulled changes in XIOS-2 and switched to graham-stdenv2023 branch
  * pulled changes in NEMO-3.6-code and switched to graham-stdenv2023 branch
    * had to change arch-GCC_GRAHAM.fcm to get REBUILD_NEMO to compile
      * moved `$EBROOTNETCDFMINFORTRAN` path for netcdf-fortran from `%NCDF_HOME` into `%NCDF_INC`
        because `maketools` seems able to only handle `$EBROOTNETCDFMINFORTRAN` or `$XIOS_HOME`
        assignment to fcm variables, not both
  * pulled changes in SalishSeaCmd and switched to graham-stdenv2023 branch
  * rsync-ed 28feb23 restart files to `graham`
  * ran 01mar23-19x26 test run
    * segfault very early in startup of nemo or xios_server

Group dinner at Nuba.



#### Thu 21-Mar-2024

Days since last wwatch3 prep stall: 12


##### SalishSeaNowcast

* resolved recent issue where Codecov report comments no longer appear in PRs
  * added token to repo GHA workflow
    * coverage report upload to Codecov was successful
    * Codecov report comment appeared in PR#248
* worked on docs updates:
  * branch: docs-maint
  * PR#248



#### Fri 22-Mar-2024

Days since last wwatch3 prep stall: 13


##### SalishSeaNowcast

* continued work on docs updates:
  * branch: docs-maint
  * PR#248


##### gha-workflows

* added CODECOV_TOKEN secret parameter to pytest-with-coverage workflow and updated docs in README


##### AtlantisCmd

* added Codecov token to org and pytest-with-coverage workflow to re-enable coverage report comments
  in pull requests:
  * branch codecov-token
  * PR#38 - squash-merged


##### NEMO_Nowcast

* added Codecov token to **repo** and pytest-with-coverage workflow to re-enable coverage report
  comments in pull requests:
  * branch codecov-token
  * PR#47 - squash-merged


##### Reshapr

* added Codecov token to org and pytest-with-coverage workflow to re-enable coverage report comments
  in pull requests:
  * branch codecov-token
  * PR#125 - squash-merged


##### moad_tools

* added Codecov token to pytest-with-coverage workflow to re-enable coverage report comments
  in pull requests:
  * branch codecov-token
  * PR#57 - squash-merged


##### salishsea-site

* added Codecov token to pytest-with-coverage workflow to re-enable coverage report comments
  in pull requests:
  * branch codecov-token
  * PR#72 - squash-merged


##### SalishSeaCmd

* added Codecov token to pytest-with-coverage workflow to re-enable coverage report comments
  in pull requests:
  * branch codecov-token
  * PR#63 - squash-merged
* renamed milestone 23.2 to 24.1 on GitHub re: my decision on 19mar to bump version due to year
  rollover and WIP for graham StdEnv/2023


##### NEMO-Cmd

* added Codecov token to pytest-with-coverage workflow to re-enable coverage report comments
  in pull requests:
  * branch codecov-token
  * PR#81 - squash-merge
* update AGRIF web link re: new forge.ipsl.fr alias for forge.ipsl.jussieu.fr to work around
  slow TLS certificate renewal issue
  * sphinx-linkcheck workflow is finally successful for the 1st time since mid-Dec


##### Miscellaneous

Updated khawla PyCharm to 2023.3.5.

Tweaked `borg-backups/lizzy_smelt.sh` to exclude private dirs in `warehouse/16.04-home/` to that script
runs error-free.
Also added `${HOME}/Games/` to backups so that Minecraft server and worlds get backups on smelt.



#### Sat 23-Mar-2024

Days since last wwatch3 prep stall: 14



#### Sun 24-Mar-2024

Days since last wwatch3 prep stall: 15

Sony TV & sound bar installed.

Started work on 2023 income tax returns.



### Week 13

#### Mon 25-Mar-2024

Days since last wwatch3 prep stall: 16


##### Miscellaneous

Checked status of scheduled GHA workflows:

  ```bash
  conda activate gha-workflows
  python /media/doug/warehouse/MOAD/gha-workflows/gha_workflow_checker/gha_workflows_checker.py
  ```

Phys Ocgy seminar: Michaela Maier, PhD candidate at UVic, Trends and Variability in Depth and
Spiciness of Subsurface Isopycnals on the Vancouver Island Continental Shelf and Slope



#### Tue 26-Mar-2024

Days since last wwatch3 prep stall: 17


##### Miscellaneous

MOAD group mtg; see whiteboard.


##### SalishSeaNowcast

* continued work on docs updates:
  * branch: docs-maint
  * PR#248



#### Wed 27-Mar-2024

Days since last wwatch3 prep stall: 18


##### ERDDAP Datasets

Finished adding V23-02 HRDPS continental grid fields datasets:

* branch: HRDPS-continental
* PR#12 - squash-merged

Investigated daily error from ubcSSg3DVariableVolumeLayers1hV21-11:

* daily error was about 12feb24
* after I triggered a dataset reload with a flag touch there were errors for more datasets
* web site graph page fails for all operations I tried
* reviewed dataset XML:
  * it is missing a depth coordinate 😱
* branch: ubcSSg3DVariableVolumeLayers1hV21-11-depth-coord
* PR#13 -
* pulled branch in production and triggered dataset load with a flag
* no more graph page errors
  * wait for automation to load today's nowcast-green results before merging
    * error report for 4 dates: 12feb24, 14mar24, 19mar24 & 21mar24
    * graph page confirms that those dates aren't loaded


##### SalishSeaNowcast

* finished work on docs updates:
  * branch: docs-maint
  * PR#248
  * added ssh keys & config section to skookum deployment docs; re: issue #244



#### Thu 28-Mar-2024

Days since last wwatch3 prep stall: 19


##### Miscellaneous

Parallel Python mini-course:

* Part 1
  * notes https://wgpages.netlify.app/pythonhpc
  * training cluster (25 x c8-30gb, 70 users)
  * hostname: parpy.c3.ca
  * user from etherpad
* added cluster to `.ssh/config` and uploaded ed25519 public key via `ssh-copy-id`
* connected via VSCode ssh extension
* env setup & activation:

  ```bash
  mkdir -p ~/tmp && cd ~/tmp
  module load StdEnv/2023 python/3.11.5 arrow/14.0.1 scipy-stack/2023b netcdf/4.9.2
  source /project/def-sponsor00/shared/pythonhpc-env/bin/activate
  ```

* don't run Python on the login node; use `salloc` for an interactive compute node session:

  ```bash
  salloc --cpus-per-task=4 --time=2:00:0 --mem-per-cpu=3600   # our default mode
  ```

* parallel efficiency of 100% is hard

* `tmux` tricks:
  * horizontal panes: C-b %
  * change panes C--> c-<- (arrows)
* `htop --filter $USER`

* `slowSeries.py`
  * expected result: 13.277605949858103
  * initial implementation: 13.286 seconds
  * generator comprehension implementation is ~1 second slower !!!

* Numpy arrays:
  * element-wise operations
  * broadcasting

* example: conversion of velocity components on spherical grid to Cartesian grid
  * brute force implementation: ~40 minutes on cluster
  * factor out `sin()` and `cos()` calculations: ~6 minutes on cluster
  * vectorize over dimensions:
    * take advantage of broadcasting; dimensional analysis
    * over lons (k loop): ~7 seconds on cluster
    * over lons and lats (k & j loop): ~2.9 seconds on cluster
    * vectorization over 3rd dimensions doesn't help because of size of memory blocks that Numpy
      moves around due to loss of contiguous allocation

* `tqdm` for progress bar; can be used to estimate completion time:
  * wrap outer loop range in `tqdm()`
  * `for i in tqdm(range(nlat)):`

* `numpy.vectorize()`
  * ~2x slower than initial implementation: 32.996 seconds
  * ternary conditional implementation is slightly faster: 28.157 seconds

* threads vs. processes:
  * process is smallest _independent_ unit of processing
  * threads share memory within process
  * multi-processing communicate via messages
  * Python uses reference counting for memory management; garbage collection
    * problem: multiple threads can access same memory, messing up reference counts
      * results in memory leaks or segmentation faults
      * Python prevents that with GIL; only 1 thread runs at a time
      * GIL will be removed in 3.13
      * threads are useful for io-bound workloads

* NumExpr
  * JIT compiler for Numpy
  * limited set of Numpy expressions compiled to C from strings
  * essentially a map-reduce wrapper that distributes calculations across threads

Helped Becca sort out issues with her analysis-becca repo after remote URLs got messed up and shelf
had to use filter-repo to remove a too-large file from history.


##### ERDDAP Datasets

* still getting error report for 4 dates: 12feb24, 14mar24, 19mar24 & 21mar24; and their fields
  are missing from ERDDAP
* restarted ERDDAP including waiting for alert from uptimerobot:

  ```bash
  sudo /opt/tomcat/bin/shutdown.sh
  # wait for alert
  sudo /opt/tomcat/bin/startup.sh
  ```

* no improvement :-(


##### SalishSeaNowcast

* started work to fix time series plots not showing dates since 31dec23:
  * branch: fix-time-series-plots
  * PR#249
  * modernized test suite



#### Fri 29-Mar-2024

**Statutory Holiday** - Good Friday

Days since last wwatch3 prep stall: 20


##### SalishSeaNowcast

* started work to fix time series plots not showing dates since 31dec23:
  * branch: fix-time-series-plots
  * PR#249
  * updated dataset URLs
  * pulled branch into production for testing
  * changed zooplankton field names from meso & micro to z1 & z2
  * change mesodinium rubrum/flagellates time series plot to diatoms/flagellates per Susan's
    instructions to deal with the fact that mesodinium rubrum is not in V21-11


##### salishsea-site

* started work to update time series plots due to new variables and svg names:
  * branch: update-time-series-plots
  * PR#73



#### Sat 30-Mar-2024

Days since last wwatch3 prep stall: 21


##### SalishSeaNowcast

* Finished fixing time series plots not showing dates since 31dec23:
  * branch: fix-time-series-plots
  * PR#249 -  squash-merged


##### ERDDAP Datasets

* still getting error report for 4 dates: 12feb24, 14mar24, 19mar24 & 21mar24; and their fields
  are missing from ERDDAP
* deactivated dataset; pinged it with flag; reactivated it; pinged it again; no change
* explored ERDDAP log.txt file
  * deleted `/results/erddap/dataset/11/ubcSSg3DVariableVolumeLayers1hV21-11/badFiles.nc`
  * pinged dataset; problem solved
* did the same deletion of `badFiles.nc` and ping for the 4 19-05 datasets that I get less frequent
  error emails for:
  * ubcSSg3DuGridFields1hV19-05; no error on reload
  * ubcSSg3DwGridFields1hV19-05; no error on reload
  * ubcSSg3DTracerFields1hV19-05; no error on reload
  * ubcSSg3DTracerFields1moV19-05; still unhappy


##### SalishSeaCast

* `collect_weather 2.5km 18` didn't finish until 20:05 (~5 hours late), long after `crop_gribs 18`
  gave up
  * `download_weather 1km 00` failed because files had been purged
  * ran `crop_gribs 18 --backfill` at ~21:45
* `collect_weather 2.5 km 00` had no files at 21:45



#### Sun 31-Mar-2024

Days since last wwatch3 prep stall: 22


##### SalishSeaCast

* `upload_forcing orcinus nowcast+` failed due to ssh key exception
* `archive_tarball hindcast 2022-oct graham` failed
  * re-ran rsync manually; slow, and overlapped with 2022-nov from automation


##### SalishSeaNowcast

* Started investigating IndexError in `make_plots._prep_comparison_fig_functions()`
  * due to no dev run results for `figures.comparison.compare_venus_ctd`
  * maybe resolved by enabling figure module to handle `dev_grid_T_hr = None`
* Closed issue #138 that got resolved almost a year ago when the nowcast-env on skookum was updated to
  Python 3.11



## April

### Week 14

#### Mon 1-Apr-2024

**Statutory Holiday** - Easter Monday

Days since last wwatch3 prep stall: 23

##### Miscellaneous

Squash-merged dependabot PRs to bump codecov/codecov-action to 4.1.1 re: maintenance updates:

* SalishSeaNowcast
* gha-workflows


##### ERDDAP Datasets

* Finalized adding missing depth coordinate to variable volume layers (e3t) dataset
* branch: ubcSSg3DVariableVolumeLayers1hV21-11-depth-coord
* PR#13 - squash-merged

* Blacklisted another IP address associated with dataforseo.com that started generating hundreds of
  failed requests last night


#### Tue 2-Apr-2024

Days since last wwatch3 prep stall: 24

Worked at ESB while Rita was at home.


##### SalishSeaCast

* 1st day of LiveOcean delayed forecasts due to cluster maintenance:

  ```bash
  # wait for download_live_ocean to start
  kill download_live_ocean
  ln -s /results/forcing/LiveOcean/downloaded/20240401 \
    /results/forcing/LiveOcean/downloaded/20240402
  make_live_ocean_files
  ```

* `upload_forcing graham forecast2|nowcast+|turbidity` all failed with
  `OSError: [Errno 101] Network is unreachable`

* started `download_live_ocean` at ~21:40:

  ```bash
  rm /results/forcing/LiveOcean/downloaded/20240402  # remove persisted 01apr symlink
  download_live_ocean
  ```

* download happened at ~00:20


##### Miscellaneous

MOAD mtg; see whiteboard

OS pkg updates on kudu; had to fix full boot volume on the way:

* started with 622M == 96% of /boot used
* clean up /var/cache/apt/archives/ with:
    `sudo apt autoclean`
* flatpak cleanup:

    ```bash
    flatpak update --appstream
    flatpak update
    flatpak uninstall --unused\
    ```

* deleted a bunch of old kernels with guidance from askubuntu
  (<https://askubuntu.com/questions/345588/what-is-the-safest-way-to-clean-up-boot-partition>)

  ```bash
  uname -r  # in-use kernel - **don't delete**
  dpkg --list 'linux-image*' | grep ^ii  # installed kernels
  sudo apt remove linux-image-VERSION  # remove all but in-use and previous kernels
  sudo apt autoremove  # remove pkgs associated w/ removed kernels
  ```

* ended with 226M == 35% of /boot used



#### Wed 3-Apr-2024

Days since last wwatch3 prep stall: 25


##### SalishSeaCast

* 2nd day of LiveOcean delayed forecasts due to cluster maintenance:

  ```bash
  # wait for download_live_ocean to start
  kill download_live_ocean
  make_live_ocean_files --debug 2024-04-02  # replace file created yesterday from 01apr persistence
  ln -s /results/forcing/LiveOcean/downloaded/20240402 \
    /results/forcing/LiveOcean/downloaded/20240403
  make_live_ocean_files
  ```

* started `download_live_ocean` at ~22:00:

  ```bash
  rm /results/forcing/LiveOcean/downloaded/20240403  # remove persisted 02apr symlink
  download_live_ocean
  ```

* download happened at ~22:04

* `robot.graham` "Network is unreachable" error stopped early this morning
  * backfilled forcing uploads for 02apr
  * started backfilling tarball uploads
    * nowcast-green.202111-mar24

    * rivers-oct22
    * rivers-nov22
    * rivers-dec22
    * rivers-*23
* `orcinus` appears to be back in operation
  * backfilled forcing uploads
    * 31mar to 02apr, nowcast+ & turbidity
  * recreated missing `/global/scratch/dlatorne/nowcast-agrif/`

    ```bash
    mkdir -p /global/scratch/dlatorne/nowcast-agrif
    chgrp wg-moad /global/scratch/dlatorne/nowcast-agrif
    chmod g+ws /global/scratch/dlatorne/nowcast-agrif
    ```

  * uploaded 16feb24 namelist and restart files from `skookum` to `orcinus`:

    ```bash
    cd /results/SalishSea/nowcast-agrif.201702/16feb24
    rsync -t \
      namelist_cfg \
      1_namelist_cfg \
      SalishSea_07484400_restart.nc \
      SalishSea_07484400_restart_trc.nc \
      1_SalishSea_14968800_restart.nc \
      1_SalishSea_14968800_restart_trc.nc \
      orcinus:/global/scratch/dlatorne/nowcast-agrif/16feb24/
    ```

  * started backfilling:

    ```bash
    make_forcing_links orcinus --run-date 2024-02-17
    make_forcing_links orcinus --run-date 2024-02-18
    make_forcing_links orcinus --run-date 2024-02-19
    make_forcing_links orcinus --run-date 2024-02-20
    make_forcing_links orcinus --run-date 2024-02-21
    make_forcing_links orcinus --run-date 2024-02-22
    make_forcing_links orcinus --run-date 2024-02-23
    ```


##### Security Updates

Squash-merged dependabot PRs to update pillow to v10.3.0 re: CVE-2024-28219 re: strcpy buffer
overflow vulnerability:

* SalishSeaNowcast
* SalishSeaTools
* Reshapr
* moad_tools
* MoaceanParcels


##### Miscellaneous

* replied to Jared's email re: forking SOG-Bloomcast-Ensemble


##### SalishSeaNowcast

* started work on fixing ONC SoG nodes comparison plots
  * need to handle absence of dev run results; call with `None` instead of dataset object
  * discovered that figure code needs update to ONC API v3



#### Thu 4-Apr-2024

Days since last wwatch3 prep stall: 26


##### SalishSeaCast

* continued backfilling nowcast-agrif:

  ```bash
  make_forcing_links orcinus --run-date 2024-02-24
  make_forcing_links orcinus --run-date 2024-02-25
  # wait for automation run_NEMO_agrif to fail
  make_forcing_links orcinus --run-date 2024-02-26
  make_forcing_links orcinus --run-date 2024-02-27
  make_forcing_links orcinus --run-date 2024-02-28
  make_forcing_links orcinus --run-date 2024-02-29
  make_forcing_links orcinus --run-date 2024-03-01
  make_forcing_links orcinus --run-date 2024-03-02
  ```


* 3rd day of LiveOcean delayed forecasts due to cluster maintenance:

  ```bash
  # wait for download_live_ocean to start
  kill download_live_ocean
  make_live_ocean_files --debug 2024-04-03  # replace file created yesterday from 02apr persistence
  ln -s /results/forcing/LiveOcean/downloaded/20240403 \
    /results/forcing/LiveOcean/downloaded/20240404
  make_live_ocean_files
  rm /results/forcing/LiveOcean/downloaded/20240404  # remove persisted 03apr symlink
  ```

* started `download_live_ocean` at 22:35:
* download happened at 22:35


##### Miscellaneous

Parallel Python mini-course:

* Part 2
  * part 1 notes https://wgpages.netlify.app/pythonhpc
  * part2 notes Part 2 notes https://wgpages.netlify.app/ray
  * training cluster (25 x c8-30gb, 70 users)
  * hostname: parpy.c3.ca
  * user from etherpad
* env setup & activation:

  ```bash
  mkdir -p ~/tmp && cd ~/tmp
  module load StdEnv/2023 python/3.11.5 arrow/14.0.1 scipy-stack/2023b netcdf/4.9.2
  source /project/def-sponsor00/shared/pythonhpc-env/bin/activate
  ```

* interactive compute node session:

  ```bash
  salloc --cpus-per-task=4 --time=2:00:0 --mem-per-cpu=3600   # our default mode
  ```

* profiling:
  * many choices
  * `scalene` demo
    * defaults to browser interface
    * `--cli` to for CLI output

* multiprocessing
  * avoids the GIL because each process has separate interpreter, so separate GIL
  * stdlib `multiprocessing` has limitations due to serialization algorithm
  * `multiprocess` fork solves those issues with different serialization algorithm
    * limitation: pool.map() returns a list so memory can be limiting; solve by breaking into
      parts; e.g. partial sums for slow harmonic series case

* other compilers for Python:
  * Cython
  * codon: MIT research project
  * mojo: superset of Python

* Numba JIT compiler
  * on top of LLVM
  * often requires re-implementation to handle code that Numba can't compile
    * mathematical exclusion of 9 strings in the case of slow harmonic series
    * slow series sped up by 10x
  * some additional speed up with `jit(parallel=True)` and `numba.prange()` instead of `range()`
    uses threads, but there is overhead to launching, so scales with problem size

* Ray parallel framework
  * `ray.init(num_cpus=4, configure_logging=False)`
    * need to specify cores because auto-init analyses hardware to find number of cores and tries
      to use all, but our cluster only has 4 cores
    * ray logging is quite verbose
    * default ray cluster uses processes
    * lazy execution
    * `ray.get()` forces calculation
    * "task-based parallelism"
    * `ray.experimental.tqdm_ray.tqdm` distributed progress bars
    * slow series has to be refactored to use partial sums to distribute to ray tasks
    * semantics of ray seem nicer than dask for code that is not using xarray or pandas
    * can use Numba jit compiled functions as `ray.remote` functions to run compiled code in parallel
      ray tasks
      * need to "prime" task processes with compiled Numba before running full scale
      * almost as fast as compiled code
  * `ray.data` objects are distributed data collections based on Python dicts

Helped Cassidy in Slack with using dask to multiply full domain day-averaged tracer fields by
`e3t_1d`.


##### SalishSeaNowcast

* scanned `/SalishSeaCast/logs/nowcast/manager-stderr-*.log` for font warning that I see in
  `compare_venus_ctd` figure test notebook; none, so stop worrying
* created issues for other warnings in manager stderr log:
  * use of `loffset` in `dataset.resample()` in `compare_tide_prediction_max_ssh` figure; issue #252
  * matplotlib UserWarning in surface_current_tiles figure module; issue #253



#### Fri 5-Apr-2024

Days since last wwatch3 prep stall: 27


##### SalishSeaCast

* continued backfilling nowcast-agrif:

  ```bash
  make_forcing_links orcinus --run-date 2024-03-03
  # wait for automation run_NEMO_agrif to fail at ~10:30
  make_forcing_links orcinus --run-date 2024-03-04
  make_forcing_links orcinus --run-date 2024-03-05
  make_forcing_links orcinus --run-date 2024-03-06
  make_forcing_links orcinus --run-date 2024-03-07
  make_forcing_links orcinus --run-date 2024-03-08
  make_forcing_links orcinus --run-date 2024-03-09
  ```

* finish up after LiveOcean delayed forecasts due to cluster maintenance:

  ```bash
  make_live_ocean_files --debug 2024-04-04  # replace file created yesterday from 03apr persistence
  ```


##### Miscellaneous

* Slack huddle w/ Cassidy re: dask processing of river tracer fields:
  * her cluster had a `global.lock` collision with the persistent cluster on `salish`
    * I need to change persistent cluster `local_directory` from `/tmp/` to `/tmp/SalishSeaCast/`


##### SalishSeaNowcast

* continued work on fixing ONC SoG nodes comparison plots
  * branch: venus-ctd-fig-dev-optional
  * PR#254
  * handled absence of dev run results; call with `None` instead of dataset object
  * updated ONC obs collection code to use ONC API v3
  * `sandheads_winds` is using HTTP instead of HTTPS for obs collection



#### Sat 6-Apr-2024

Days since last wwatch3 prep stall: 0


##### SalishSeaCast

* `make_ww3_current_file forecast2` stalled; killed it and skipped run
* continued backfilling nowcast-agrif:

  ```bash
  # wait for automation run_NEMO_agrif to fail at ~10:30
  make_forcing_links orcinus --run-date 2024-03-10
  make_forcing_links orcinus --run-date 2024-03-11
  make_forcing_links orcinus --run-date 2024-03-12
  make_forcing_links orcinus --run-date 2024-03-13
  make_forcing_links orcinus --run-date 2024-03-14
  make_forcing_links orcinus --run-date 2024-03-15
  make_forcing_links orcinus --run-date 2024-03-16
  make_forcing_links orcinus --run-date 2024-03-17
  ```



#### Sun 7-Apr-2024


##### SalishSeaCast

* continued backfilling nowcast-agrif:

  ```bash
  make_forcing_links orcinus --run-date 2024-03-18
  # wait for automation run_NEMO_agrif to fail at ~10:30
  make_forcing_links orcinus --run-date 2024-03-19
  make_forcing_links orcinus --run-date 2024-03-20
  make_forcing_links orcinus --run-date 2024-03-21
  make_forcing_links orcinus --run-date 2024-03-22
  ```



### Week 15

#### Mon 8-Apr-2024

Partial solar eclipse, fully obscured by cloud


##### SalishSeaCast

* continued backfilling nowcast-agrif:

  ```bash
  make_forcing_links orcinus --run-date 2024-03-23
  # wait for automation run_NEMO_agrif to fail at ~10:30
  make_forcing_links orcinus --run-date 2024-03-24
  make_forcing_links orcinus --run-date 2024-03-25
  make_forcing_links orcinus --run-date 2024-03-26
  make_forcing_links orcinus --run-date 2024-03-27
  make_forcing_links orcinus --run-date 2024-03-28
  make_forcing_links orcinus --run-date 2024-03-29
  make_forcing_links orcinus --run-date 2024-03-30
  make_forcing_links orcinus --run-date 2024-03-31
  ```


##### Miscellaneous

Phys ocgy seminar:

Squash-merged dependabot PRs to bump codecov/codecov-action to 4.2.0 re: feature update:

* gha-workflows
* SalishSeaNowcast

Updated khawla PyCharm to 2024.1.


##### SalishSeaNowcast

* finished work on fixing ONC SoG nodes comparison plots
  * branch: venus-ctd-fig-dev-optional
  * PR#254 - squash-merged
  * dropped ONC Delta DDL node comparison plot from `make_plots` because its deployment ended
    in March
* fixed Sandheads winds comparison plot:
  * branch: update-hrdps-erddap-url
  * PR#256 - squash-merged
  * updated ERDDAP URL to V23-02 HRDPS dataset


##### `graham` StdEnv/2023

* continued work on testing GCC-12 build on `graham`
  * checked XIOS-2 and SalishSeaCast NEMO config executables with `ldd`
  * tried to launch `xios-server.exe` and `nemo.exe` on login node; both failed with:

      ```text
      terminate called after throwing an instance of 'std::bad_alloc'
      what():  std::bad_alloc
      Aborted
      ```

  * queued 01mar23-4x9 test run
    * failed on launch with out of memory error
    * looked back and found that 20mar 19x26 test had same cause of failure
  * changed to Intel compilers (`module load intel/2023.2.1`) and tried XIOS-2 and NEMO SalishSeaCast
    builds
    * lots of warnings in XIOS-2 build, but successful
    * successful NEMO build
  * changed `salishsea_cmd.run._modules()` to load `intel/2023.2.1`
  * queued 01mar23-4x9 test run
    * run launched successfully
    * `ocean.output` was created, but no time steps
    * segfault in `stderr`



#### Tue 9-Apr-2024


##### SalishSeaCast

* `download_live_ocean` timed out at 12:10
  * retried at 12:27; timed out at 15:27
  * persisted 8apr24 LiveOcean file via symlink
  * `make_live_ocean_files` to start automation at ~15:35
* continued backfilling nowcast-agrif:

  ```bash
  make_forcing_links orcinus --run-date 2024-04-01
  # wait for automation run_NEMO_agrif to fail at ~17:00
  make_forcing_links orcinus --run-date 2024-04-02
  make_forcing_links orcinus --run-date 2024-04-03
  make_forcing_links orcinus --run-date 2024-04-04
  make_forcing_links orcinus --run-date 2024-04-05
  make_forcing_links orcinus --run-date 2024-04-06
  make_forcing_links orcinus --run-date 2024-04-07
  make_forcing_links orcinus --run-date 2024-04-08
  make_forcing_links orcinus --run-date 2024-04-09
  ```


##### Miscellaneous

* Erik Eberhardt interview meetings for headship
  * dept-wide vision presentation w/ Q&a
  * staff mtg
* MOAD group mtg; see whiteboard
* Reviewed readthedocs projects (list at bottom) re: updating .readthedocs.yaml
  * 5 repos remaining to be done
* updated kudu to PyCharm 2024.1


##### salishsea-site

* readthedocs build maintenance:
  * branch: rtd-build-maint
  * PR#74 - squash-merged



#### Wed 10-Apr-2024


##### SalishSeaCast

* finished backfilling nowcast-agrif:

  ```bash
  make_forcing_links orcinus --run-date 2024-04-04
  make_forcing_links orcinus --run-date 2024-04-05
  # wait for automation run_NEMO_agrif to fail at ~12:30
  make_forcing_links orcinus --run-date 2024-04-06
  make_forcing_links orcinus --run-date 2024-04-07
  make_forcing_links orcinus --run-date 2024-04-08
  make_forcing_links orcinus --run-date 2024-04-09
  make_forcing_links orcinus --run-date 2024-04-10
  ```

* `download_live_ocean` was slow again
  * checked for yesterday's run; extraction was finished at 19:55; backfilled download and boundary
    file creation
  * email to Parker; he replied that runs are delayed due to cluster maintenance again this week;
    Tue-Thu

    ```bash
    ln -s /results/forcing/LiveOcean/downloaded/20240409 \
      /results/forcing/LiveOcean/downloaded/20240410
    make_live_ocean_files
    rm /results/forcing/LiveOcean/downloaded/20240410  # remove persisted 09apr symlink
    ```

  * started `download_live_ocean` at 20:00
  * download happened at ??:??


##### Miscellaneous

* SharcNet seminar: Accelerating data analytics with RAPIDS cuDF
  * Nastaran Shahparlan, York
  * pandas is ubiquitous, but slow
  * RAPIDS
    * NVIDIA, GPU accelerated
    * cuDF, dask-cuDF
    * cudf.pandas; 60% of pandas supported
      * faster than polars
      * run in apptainer container on clusters for now; see wiki page
      * includes a profiler
      * distribution of work between cpu and gpu depends on axis selection for some methods
        * `max()` can't use gpu for axis=0
        * `count()` can't use gpu for axis=1
      * not designed for out-of-core workflows
      * no good interface for Python and NumPy C APIs


##### `graham` StdEnv/2023

* tried Intel build of XIOS-2 without includes of `<limits>` and `<array>` in `meshutil.cpp` but
  that only confirmed that they are necessary for both Intel-2023.2.1 and GCC-12



#### Thu 11-Apr-2024


##### SalishSeaCast

* `crop_gribs 12` stalled with 1 file not processed; APCP in hour 010
* `download_live_ocean` was delayed again

    ```bash
    # wait for download_live_ocean to start
    kill download_live_ocean
    ln -s /results/forcing/LiveOcean/downloaded/20240410 \
      /results/forcing/LiveOcean/downloaded/20240411
    make_live_ocean_files
    rm /results/forcing/LiveOcean/downloaded/20240411  # remove persisted 10apr symlink
    ```

  * started `download_live_ocean` at 20:00
  * download happened at ??:??


##### SalishSeaNowcast

* fixed badge tables in README and dev docs; broken on GitHub due to changes in rendering pipeline
  * branch: fix-badge-tables
  * PR#257 - squash-merged
  * removed split in Meta cell
  * reduced spaces between cell separator and text to prevent addition of quoted
    text bars; it seems that GitHub is doing a reStructuredText to Markdown
    transformation in the rendering pipeline
  * updated the Python version badge to pull from `pyproject.toml` file so that
    there is one less change necessary when the Python version is changed.


##### SOG-Bloomcast-Ensemble

* added new weather descriptions to cloud fraction mapping


##### Miscellaneous

* UCB - IOS modeling mtg: Susan re: Iona Outfall modeling and alkalinity addition proposed by
  Planetary Inc.



#### Fri 12-Apr-2024

Got 1st dose of shingles vaccine.


##### SalishSeaCast

* `crop_gribs 12` stalled with 1 file not processed; APCP in hour 007


##### Security Updates

Squash-merged dependabot PRs to update idna to v3.7 re: CVE-2024-3651 re: DoS vulnerability:

* cookiecutter-analysis-repo
* MOAD/docs
* NEMO-Cmd
* cookiecutter-MOAD-pypkg
* AtlantisCmd
* MoaceanParcels
* NEMO_Nowcast
* SalishSeaCmd
* SalishSeaTools
* moad_tools
* SalishSeaNowcast
* Reshapr
* SalishSeaCast/docs
* salishsea-site


##### SalishSeaCmd

* fixed badge tables in README and dev docs; broken on GitHub due to changes in rendering pipeline
  * branch: fix-badge-tables
  * PR#65 - squash-merged
  * removed split in Meta cell
  * reduced spaces between cell separator and text to prevent addition of quoted
    text bars; it seems that GitHub is doing a reStructuredText to Markdown
    transformation in the rendering pipeline
  * updated the Python version badge to pull from `pyproject.toml` file so that
    there is one less change necessary when the Python version is changed.


##### NEMO-Cmd

* fixed badge tables in README and dev docs; broken on GitHub due to changes in rendering pipeline
  * branch: fix-badge-tables
  * PR#83 - squash-merged
  * removed split in Meta cell
  * reduced spaces between cell separator and text to prevent addition of quoted
    text bars; it seems that GitHub is doing a reStructuredText to Markdown
    transformation in the rendering pipeline
  * updated the Python version badge to pull from `pyproject.toml` file so that
    there is one less change necessary when the Python version is changed.


##### Reshapr

* fixed badge tables in README and dev docs; broken on GitHub due to changes in rendering pipeline
  * branch: fix-badge-tables
  * PR#128 - squash-merged
  * removed split in Meta cell
  * reduced spaces between cell separator and text to prevent addition of quoted
    text bars; it seems that GitHub is doing a reStructuredText to Markdown
    transformation in the rendering pipeline
  * updated the Python version badge to pull from `pyproject.toml` file so that
    there is one less change necessary when the Python version is changed.


##### moad_tools

* fixed badge tables in README and dev docs; broken on GitHub due to changes in rendering pipeline
  * branch: fix-badge-tables
  * PR#60 - squash-merged
  * removed split in Meta cell
  * reduced spaces between cell separator and text to prevent addition of quoted
    text bars; it seems that GitHub is doing a reStructuredText to Markdown
    transformation in the rendering pipeline
  * updated the Python version badge to pull from `pyproject.toml` file so that
    there is one less change necessary when the Python version is changed.



#### Sat 13-Apr-2024

Recovery from shingles vaccine.


##### Resilient-c

* VM went offline late last night; unable to ssh to VM
* unable to investigate due to day-long dashboard maintenance



#### Sun 14-Apr-2024

IRL ride to Iona, home via Heather with a stop at Enroute Café.


##### SalishSeaCast

* `make_ww3_wind_file forecast2` stalled; killed it and skipped run


##### Resilient-c

* email from cloud support that VM backup is failing because VM is powered down
* asked them to restart VM; reply was that they couldn't due to problem with the underlying storage
* asked them to restore VM from recent backup



### Week 16

#### Mon 15-Apr-2024


##### SalishSeaCast

* discovered that yesterday's `make_ww3_wind_file forecast2` stall was due to
  `make_ww3_wind_file nowcast` having stalled:
  * no 13apr24 wwatch3 runs
  * 14apr24 nowcast run was a cold start
  * recovery:
    * wait for 15apr24 runs to finish
    * `make_ww3_wind_file forecast 2024-04-13
    * `make_ww3_current_file forecast 2024-04-13
    * wait for runs to finish
    * `make_ww3_wind_file forecast 2024-04-14
    * `make_ww3_current_file forecast 2024-04-15
    * wait for runs to finish
    * `make_ww3_wind_file forecast 2024-04-15
    * `make_ww3_current_file forecast 2024-04-15
* `upload_forcing orcinus turbidity` failed with ssh protocol banner error
  * re-tried manually several times with no luck
  * traced problem to `seawolf3` login node
  * emailed Mark
  * `seawolf3` working at 11:30; re-ran manually to restart automation


##### Miscellaneous

Squash-merged dependabot PRs to bump codecov/codecov-action to 4.3.0 re: feature update:

* SalishSeaNowcast
* gha-workflows

Phys ocgy seminar: Pouneh Hoshyar, U of A: Studying the Labrador Sea for Ocean and Climate Implications

Checked status of scheduled GHA workflows:

  ```bash
  conda activate gha-workflows
  python /media/doug/warehouse/MOAD/gha-workflows/gha_workflow_checker/gha_workflows_checker.py
  ```

Reactivated workflow that had been disabled due to inactivity:

  ```bash
  gh workflow enable -R SS-Atlantis/AtlantisCmd sphinx-linkcheck
  ```


##### Resilient-c

* Randell Ong of cloud services restored 11apr backup to a new VM; web app restart was trivial



#### Tue 16-Apr-2024

Worked at ESB while Rita was at home.

##### Miscellaneous

* MOAD group mtg; see whiteboard
* coffee with Ilias
* in the course of reviewing the Sphinx 7.3 release, I learned about `pip-tools`, particularly
  `pip-compile` that appears to produce `requirements.txt` files annotated with the packages from
  which each dependency arises


##### Security Updates

Squash-merged dependabot PRs to update idna to v3.7 re: CVE-2024-3651 re: DoS vulnerability:

* cookiecutter-djl-pypkg
* erddap-datasets
* SOG-Bloomcast-Ensemble
* SOG-Bloomcast

Squash-merged dependabot PRs to update jinja2 to v3.1.3 re: CVE-2024-22195 re: XSS vulnerability:

* salishsea-site

Squash-merged dependabot PRs to update pillow to v10.3.0 re: CVE-2024-28219 re: strcpy buffer
overflow vulnerability:

* SOG-Bloomcast


##### `graham` StdEnv/2023

* continued work on testing StdEnv/2023 on `graham`:
  * `intel/2023.2.1` compilers
  * checked XIOS-2 executable from 10apr with `ldd`
  * built SalishSeaCast NEMO config and REBUILD_NEMO
  * queued 01mar23-19x26 test run using hacked SalishSeaCmd
    * failed with ExitCode 139



#### Wed 17-Apr-2024

##### Miscellaneous

* Pangeo weekly mtg; re: https://github.com/pydata/xarray/discussions/8925
  * working with large number of file system (not cloud) files (10k, 100k)
  * gpm-api package: https://gpm-api.readthedocs.io/en/latest/
  * Pycolorbar( https://github.com/ghiggi/pycolorbar/tree/main)
    * to define colormap and colorbar configurations for matplotlib, xarray etc in YAML files
  * I asked, can kerchunk be used incrementally:
    * yes, provided that compression is consistent
    * https://projectpythia.org/kerchunk-cookbook/notebooks/advanced/appending.html
    * VirtualiZarr might be the evolution of Kerchunk
* played with `pip-compile` in NEMO-Cmd project:
  * copied dependencies from `environment-dev.yaml` to `requirements.in` because there is no support
    for conda env description YAML files
  * had to change `=` to `==` for version pins
  * had to `python` from list
  * `pip-compile --allow-unsafe --strip-extras -o envs/requirements.txt envs/requirements.in`
    produced a nicely annotated `requirements.txt` file
    * the versions are the latest from PyPI, not those in the env 🙁
  * decided that `pip-compile` is only useful to me for mapping dependency graph, not for routine
    generation of `requirements.txt` files that I use to record dev env, not build the virtualenv


##### SalishSeaCast

* `nowcast-green` failed
  * MPI comm failure between `nowcast2` and `nowcast3`
  * login to `arbutus` head node was very slow to give bash prompt
  * all arbutus compute nodes respond and show mounted shared storage
  * `ocean.output` shows HDF5 errors reading `restart_trc.nc`
  * recovery started at ~10:45
    * moved failed `17apr24/` directories aside on `arbutus` and `skookum`
    * retried run with `make_forcing_links arbutus nowcast-green`
    * retry run is time stepping
* `make_ww3_current_file forecast` stalled; killed it and re-ran at ~12:40



#### Thu 18-Apr-2024


##### SalishSeaCast

* `make_ww3_wind_file forecast2` stalled; killed it and skipped run
* couldn't attach to `make_averaged_dataset` tmux session on `salish`
  * killed it and set up the cluster in a new session
  * used `--local-directory /tmp/SalishSeaCast` to avoid lock collisions with other users' dask
    clusters (e.g. Cassidy)


##### Miscellaneous

* researched VirtualiZarr: https://github.com/TomNicholas/VirtualiZarr
  and its motivation discussion: https://github.com/fsspec/kerchunk/issues/377
  * probably too early days for me to experiment with compared to Kerchunk
* Slack w/ Karyn to help her build a new, Python 3.12 analysis env
  * `mocsy` hasn't been built for Python 3.12 on conda-forge because it has imports from
    `numpy.distutils`


##### salishsea-site

* Enabled PR build on readthedocs
* Created v24.1 milestone
  * moved open and closed issues from v23.1 milestone to v24.1
  * closed v23.1 milestone, marked as never released

* Resumed work on update to Python 3.12:
  * abandoned py312 branch because it is ~6mo stale
  * branch: py312-redux
  * PR# -
  * cherry-picked commits from py32 branch



#### Fri 19-Apr-2024


##### SalishSeaCast

* `make_ww3_wind_file forecast2` stalled; killed it and re-ran


##### salishsea-site

* Finished update to Python 3.12:
  * abandoned py312 branch because it is ~6mo stale
  * branch: py312-redux
  * PR#77 - squash-merged
  * build Python 3.12 env on kudu and confirmed
    * test suite passed, but with deprecation warnings (all from withing pyramid stack, I think):
      * `webob`: `cgi` will be removed in Python 3.13
      * `pyramid`: `pkg_resources` is deprecated as an API
      * `pyramid`: `pkg_resources.declare_namespace` is deprecated; use implicit namespace packages
        (PEP 420)
      * `pkg_resources` deprecations are WIP: https://github.com/Pylons/pyramid/issues/3731
    * sphinx docs build succeeded
    * sphinx linkcheck succeeded
    * site works in dev mode
  * closed PR#54, marked as stale
  * change envs to 3.12
  * updated pkgs & versions; 3.12 updated
  * dropped TROVE classifiers
  * changed sphinx-linkcheck workflow to 3.12
  * changed index docs, badges, README to 3.12
  * dropped support for 3.10 & 3.11:
    * pytest-with-coverage, setup.cfg, index docs, badges, README


##### Miscellaneous

* helped Tall with git SHA not found error from `salishsea run`
  * I suspect that the root cause is that he is working from clones stored on `/scratch/`;
    the 90-day purge policy appears to have deleted files in SS-run-sets and that is messing up
    vcs recoding
* Slack conversations with Becca and Elise resulted in killing processes that were inadvertently
  using >92% of swap on `salish`



#### Sat 20-Apr-2024


##### SalishSeaCast

* LiveOcean ran early due to UW HPC cluster maintenance; winds degraded



#### Sun 21-Apr-2024


##### SalishSeaCast

* `make_ww3_wind_file forecast2` stalled; killed it and re-ran
* no LiveOcean run due to cluster maintenance:

  ```bash
  # wait for download_live_ocean to start
  kill download_live_ocean
  ln -s /results/forcing/LiveOcean/downloaded/20240420 \
    /results/forcing/LiveOcean/downloaded/20240421
  make_live_ocean_files
  # keep persisted 20apr symlink because it's all we'll ever get
  ```



### Week 17

#### Mon 22-Apr-2024


##### SalishSeaCast

* LiveOcean ran late due to cluster maintenance:
  * `download_live_ocean` launched by automation timed out; re-ran manually
    and it completed at ~12:35


##### salishsea-site

* Modernized packaging:
  * branch: modernize-pkg
  * PR#78 - squash-merged
  * move package metadata and entry points from setup.cfg to pyproject.toml
  * drop setup.py and setup.cfg
  * change from setuptools to hatchling for build backend
  * move version identifier to ``__about__.py``
  * change to use ``importlib.metadata.version()``
  * install pkg in readthedocs env so that Sphinx can access its metadata
  * add release process section to dev docs
  * changed badges layout in README & dev docs to table
  * updated pkgs & versions in recent dev env
* built new Python 3.12 salishsea-site-env on `skookum`



#### Tue 23-Apr-2024

##### Miscellaneous

* MOAD group mtg; see whiteboard
* met w/ Vicente to try to resolve his GitHub permission issue from remote
  VSCode sessions on `chum`
  * the problem seems to be with remote VSCode not connecting properly to
    `ssh-agent` on `chum`, but I couldn't solve it
  * remote VSCode sessions on `salish` are so slow as to be unusable



#### Wed 24-Apr-2024


##### salishsea-site

* Added pre-commit:
  * branch: add-pre-commit
  * PR#79 - squash-merged
  * add pre-commit dependency
  * add .pre-commit-config.yaml
  * update Code Style docs re: pre-commit
  * run `pre-commit run --all` to garden code & docs
Released v24.1 and bumped dev to v24.2.dev0.


##### `graham` StdEnv/2023

* continued work on testing StdEnv/2023 on `graham`:
  * built XIOS-2 with `--debug` flag which uses:
    * %DEBUG_CFLAGS   -DBZ_DEBUG -g -traceback -fno-inline
    * %DEBUG_FFLAGS   -g -traceback
  * built SalishSeaCast NEMO and REBUILD_NEMO with those flags subbed into `%CFLAGS` and `%FCFLAGS`
    * failed with undefined symbols in `trd_mxl_trc` module
    * after consultation with Susan, tried unsuccessfully to isolate `trd_mxl_trc` calls that we
      shouldn't need with `#ifdef`
    * odd and worrying that undefined symbols appear at `O0` level but not at `O3`



#### Thu 25-Apr-2024


##### `graham` StdEnv/2023

* continued work on testing StdEnv/2023 on `graham`:
  * built SalishSeaCast NEMO and REBUILD_NEMO with `-g -traceback -O3` in `%FCFLAGS`
    * successful
  * ran `01mar23-4x9` test
    * got 414 time steps on gra667 before time-out at requested 1h walltime!
  * built SalishSeaCast NEMO and REBUILD_NEMO with `-g -traceback` removed from in `%FCFLAGS`
    * successful
  * ran `01mar23-4x9` test
    * got 370 time steps on gra58 before time-out at requested 1h walltime
  * built XIOS-2 without `--debug` flag
    * successful



#### Fri 26-Apr-2024


##### `graham` StdEnv/2023

* continued work on testing StdEnv/2023 on `graham`:
  * built SalishSeaCast NEMO and REBUILD_NEMO without debug options and linked to no-debug XIOS-2
    * successful
  * ran `01mar23-4x9` test
    * timed out on gra449 with no time steps
  * built XIOS-2 without `--debug` flag
    * successful
  * built SalishSeaCast NEMO and REBUILD_NEMO with `-g -traceback -O3` in `%FCFLAGS`
    * successful
  * ran `01mar23-4x9` test
    * got 416 time steps on gra156 before time-out at requested 1h walltime
  * added a StdEnv/2023-Apr24 sheet to Google docs `graham-SalishSeaCast-v202111-scaling` spreadsheet
    * 01mar23-4x9-debug-3h
      * 1275 time steps vs. 1545 in apr23
    * 01mar23-6x14
      * 2:25:00 vs. 1:57:16 in apr23
    * 01mar23-8x18
      * 1:26:00 vs. 1:08:30 in apr23


##### Miscellaneous

* read Kerchunk Cookbook (https://projectpythia.org/kerchunk-cookbook/README.html)
* started experimenting in `analysis-doug/notebooks/kerchunk-expts/`



#### Sat 27-Apr-2024


##### `graham` StdEnv/2023

* continued work on testing StdEnv/2023 on `graham`:
  * continued filling `StdEnv/2023-Apr24` sheet in Google docs `graham-SalishSeaCast-v202111-scaling`
    spreadsheet
    * 01mar23-9x22
      * 1:02:23 vs. 0:46:35 in apr23
    * 01mar23-10x27
      * 0:56:09 vs. 0:34:45 in apr23
    * 01mar23-11x32
      * 0:52:44 vs. 0:22:24 in apr23


##### Miscellaneous

* more experimenting in `analysis-doug/notebooks/kerchunk-expts/`


##### SalishSeaCast

* `make_ww3_current_file forecast2` stalled; killed it and skipped run



#### Sun 28-Apr-2024


##### `graham` StdEnv/2023

* continued work on testing StdEnv/2023 on `graham`:
  * built SalishSeaCast NEMO and REBUILD_NEMO without debug options and linked to no-debug(?) XIOS-2
    * successful
  * continued filling `StdEnv/2023-Apr24` sheet in Google docs `graham-SalishSeaCast-v202111-scaling`
    spreadsheet
    * 01mar23-12x28
      * 0:55:06 vs. 0:23:58 in apr23
    * 01mar23-13x31
      * failed with ExitCode 139; segfault


##### Miscellaneous

* more experimenting in `analysis-doug/notebooks/kerchunk-expts/`
  * figured out Parquet storage of combined Kerchunk references



### Week 18

#### Mon 29-Apr-2024


##### SalishSeaCast

* yesterday's `make_ww3_wind_file forecast` stalled; killed it and re-ran
  * messy


##### Miscellaneous

* continued discussion with Andrey at PyCharm re: conda env not auto-activating in khawla terminal
  * learned that mambaforge and miniforge merged in Sep-2023
* more experimenting in `analysis-doug/notebooks/kerchunk-expts/`
  * figured out create Parquet storage of combined Kerchunk references from per-netCDF reference
    stored as JSON


##### `graham` StdEnv/2023

* reverted to StdEnv/2020 builds to benchmark against Apr-2023 scaling runs
  * XIOS-ARCH:
    * git stash  # re: intel compilers
    * git switch main
  * XIOS-2:
    * git stash  # re: `<limits>` and `<array>` includes
    * git switch main
    * clean & build
  * NEMO-3.6-code:
    * git stash  # re: intel compilers
    * git switch main
    * load netcdf-fortran-mpi/4.6.0 & perl/5.30.2
    * clean & build SalishSeaCast NEMO & REBUILD_NEMO
  * SalishSeaCmd:
    * git stash  # re: module loads
    * git switch main
  * 01mar23-6x14
    * time stepping, then timed out, and run dir is inaccessible; /scratch hosed?



#### Tue 30-Apr-2024


##### `graham` StdEnv/2023

* re-tried StdEnv/2020 build run to benchmark against Apr-2023 scaling runs
  * 01mar23-6x14
    * success; 2:00:34 vs. 1:57:16 in Apr-2023
    * so, graham compute & storage performance is comparable now to Apr-2023


##### Miscellaneous

* MOAD group mtg; see whiteboard
* Slack w/ Becca re: forking Parker's `lo` repo so that she can keep up to date with his changes
  and track her own
  * I had already forked `lo` as `LiveOcean` in our UBC-MOAD org, so she is using that
  * also discussed forking our MOAD ariane repo
    * I would need to enable private repo forking, then disable forking per-repo on other repos
    * why does she need a fork? why are her changes not shareable with other MOAD users?
* took `khawla` to ESB to compare PyCharm w/ `kudu` re: auto-activation of conda envs in terminal sessions
  * found `JEDISOURCE_*` variables in `kudu` log that aren't in `khawla` log



## May

<!-- markdownlint-disable MD001 -->
#### Wed 1-May-2024
<!-- markdownlint-enable MD001 -->


##### SalishSeaNowcast

* fixed broken salishsea-site docs links found by monthly scheduled run of sphinx-linkcheck workflow
  re: change single version setting in readthedocs project configuration


##### `graham` StdEnv/2023

* continued work on testing StdEnv/2023 on `graham`:
  * return to StdEnv/2023 builds:
  * XIOS-ARCH:
    * git switch graham-stdenv2023
    * git stash pop  # re: intel compilers
  * XIOS-2:
    * git switch graham-stdenv2023
    * git stash pop  # re: `<limits>` and `<array>` includes
    * clean & build with --prod flag
  * NEMO-3.6-code:
    * git switch graham-stdenv2023
    * git stash pop  # re: intel compilers
    * load StdENV/2023, intel/2023.2.1, netcdf-fortran-mpi/4.6.1 & perl/5.36.1
    * clean & build SalishSeaCast NEMO & REBUILD_NEMO without `-g -traceback` flags
  * SalishSeaCmd:
    * git switch graham-stdenv2023
    * git stash  # re: module loads
  * 01mar23-6x14-2023
    * failed after 50 seconds with ExitCode 134
    * segfault with 2 core dumps


##### Miscellaneous

* reported `JEDISOURCE_*` variables finding to Andrey at PyCharm


##### 2x resolution SalishSeaCast

* see Susan's notes in #sockeye channel
* see my notebooks in `analysis-doug/2xrez-202111/`
  * started looking at coordinates
    * goals:
      * look at the coordinates file that Susan created for the 2022 experiment
      * check the coordinates in the lower Fraser River are re: Michael's grid refinements there
      * investigate adding coordinate rows at the south edge of the domain to fully include the south
        coastline of Puget Sound and add a sufficient land buffer for OceanParcels to work correctly
        in that are re: Jose's findings about particle losses at water boundaries



#### Thu 2-May-2024


##### `graham` StdEnv/2023

* continued work on testing StdEnv/2023 on `graham`:
  * NEMO-3.6-code:
    * load StdENV/2023, intel/2023.2.1, netcdf-fortran-mpi/4.6.1 & perl/5.36.1
    * clean & build SalishSeaCast NEMO & REBUILD_NEMO with:
      * `-g -traceback -O3` flags
      * XIOS-2 `--prod` build
  * 01mar23-6x14-g-O3
    * failed after 46 seconds with ExitCode 134
    * segfault with 2 core dumps
  * XIOS-2:
    * clean & build with `--debug` flag
  * NEMO-3.6-code:
    * load StdENV/2023, intel/2023.2.1, netcdf-fortran-mpi/4.6.1 & perl/5.36.1
    * clean & build SalishSeaCast NEMO & REBUILD_NEMO with:
      * no `-g -traceback -O3` flags
      * XIOS-2 `--debug` build
  * 01mar23-6x14-xios-debug
    * time stepping; estimate ~2.5 hr
    * success; 2:23:06 vs. StdEnv/2020 1:57:16 in Apr-2023 and 2:00:34 on 30apr24
  * XIOS-2:
    * clean & build with `--dev` flag
      * `-g -traceback` for C; `-g -O2 -traceback` for fortran
  * NEMO-3.6-code:
    * load StdENV/2023, intel/2023.2.1, netcdf-fortran-mpi/4.6.1 & perl/5.36.1
    * clean & build SalishSeaCast NEMO & REBUILD_NEMO with:
      * no `-g -traceback -O3` flags
      * XIOS-2 `--dev` build
  * 01mar23-6x14-xios-dev
    * time stepping; estimate ~2 hr
    * success; 2:05:27 vs. StdEnv/2020 1:57:16 in Apr-2023 and 2:00:34 on 30apr24
  * 01mar23-19x26-xios-dev
    * success; 0:28:11 vs. StdEnv/2020 0:16:xx in Apr-2023


##### 2x resolution SalishSeaCast

* continued looking at coordinates
  * checked the coordinates in the lower Fraser River are re: Michael's grid refinements there
    * discussed with Susan
    * grid looks acceptable in Fraser River area
  * investigate adding coordinate rows at the south edge of the domain to fully include the south
    coastline of Puget Sound and add a sufficient land buffer for OceanParcels to work correctly
    in that are re: Jose's findings about particle losses at water boundaries
    * Nisqually River estuary is the main water that is cut off
    * will need to add ~10 grid points to production grid


##### Miscellaneous

* 2.25 hours of battery life on khawla in balanced integrated graphics mode



#### Fri 3-May-2024


##### `graham` StdEnv/2023

* continued work on testing StdEnv/2023 on `graham`:
  * 01mar23-19x26-xios-dev2 to re-test time on 8 nodes
    * success; 0:32:21 vs. StdEnv/2020 0:16:xx in Apr-2023 and 0:30:41 yesterday


##### 2x resolution SalishSeaCast

* continued looking at coordinates
  * started work on SSC_202405 coordinates for hindcasts/production with grid extended to include
    all of south Puget Sound water
  * after discussion with Susan, prototyped using pre-cell parabolic curve fits to calculate
    lons/lats of new grid points


##### Miscellaneous

* 1h40m of battery life on khawla in high performance Nvidia graphic mode
* 14:34 to 16:14


##### Security Updates

Squash-merged dependabot PRs to update tqdm to v4.66.3 re: CVE-2024-34062 re: arbitrary code
execution vulnerability:

* MoaceanParcels
* tools/SalishSeaTools
* SalishSeaNowcast



#### Sat 4-May-2024


##### SalishSeaCast

* `make_ww3_current_file forecast2` stalled; killed it and skipped run



#### Sun 5-May-2024


##### SalishSeaCast

* `make_ww3_current_file forecast2` stalled; killed it and skipped run



### Week 19

#### Mon 6-May-2024


##### Miscellaneous

Squash-merged dependabot PRs to update codecov-action to v4.3.1 re: feature & dependency updates:

* SalishSeaNowcast
* gha-workflows

Checked status of scheduled GHA workflows:

  ```bash
  conda activate gha-workflows
  python /media/doug/warehouse/MOAD/gha-workflows/gha_workflow_checker/gha_workflows_checker.py
  ```

Helped Becca with `RuntimeError: NetCDF: HDF error`:

* suggested using context managers to be more explicit about when files opened by
  `xarray.open_dataset()` are closed


##### SalishSeaCast

* investigatedONC ferry obs failures:
  * CO2 sensor request is failing
  * is it possible that, with 1 sensor request failing, we are not recording any obs?


##### Security Updates

Squash-merged dependabot PR to update jinja2 to v3.1.4 re: CVE-2024-34064 re: XSS vulnerability:

* SalishSeaNowcast


##### 2x resolution SalishSeaCast

* continued looking at coordinates
  * continued work on SSC_202405 coordinates for hindcasts/production with grid extended to include
    all of south Puget Sound water
  * generalized code to use pre-cell parabolic curve fits to calculate lons/lats and spacings of
    new grid points
  * got Jose's opinion that the new grid has sufficient land cells to keep OceanParcels happy
  * calculated all of the arrays of values to extend the grid



#### Tue 7-May-2024


##### Miscellaneous

* MOAD group mtg; see whiteboard


##### Security Updates

Squash-merged dependabot PR to update jinja2 to v3.1.4 re: CVE-2024-34064 re: XSS vulnerability:

* NEMO_Nowcast
* NEMO-Cmd
* MoaceanParcels
* SalishSeaCmd
* cookiecutter-MOAD-pypkg
* salishsea-site
* MOAD/docs
* AtlantisCmd
* tools/SalishSeaTools
* Reshapr
* moad_tools
* SalishSeaCast/docs
* cookiecutter-analysis-repo
* cookiecutter-djl-pypkg
* erddap-datasets
* SOG-Bloomcast-Ensemble
* SOG
* SOG-Bloomcast


##### `graham` StdEnv/2023

* decided to shelve migration to StdEnv/2023 for the time being:
  * run time is slower to much slower than StdEnv/2020, and that's a waste of
    our allocation
  * default environment has not yet changed to StdEnv/2023 despite announcement
    that it would on 3-Apr; that suggests we may not be the only users for whom
    the new environment is sub-optimal
* reviewed status of `graham-stdenv2023` branches and pushed commits from graham:
  * XIOS-ARCH:
    * committed env file changes to load intel compilers module and related
      library module versions
    * committed drop of outdated CFLAGS
  * XIOS-2:
    * added GCC arch file names to .gitignore to avoid accidental commits
  * NEMO-3.6-code:
    * nothing to commit
  * SalishSeaCmd:
    * change graham module loads to use Intel compiler collection
      **needs correction for other HPC clusters and tests**
  * SalishSeaCast/docs
    * TODO: `-m GCC_GRAHAM` back to `-m X64_GRAHAM`



#### Wed 8-May-2024


##### Miscellaneous

* tried suggestion from Andrey at PyCharm to add conda activation to bash launch
  * added to `.bash_aliases`

    ```bash
    if [[ "$TERMINAL_EMULATOR" == "JetBrains-JediTerm" ]]
    then
      conda activate {env_name}
    fi
    ```

    got `conda: command not found` messages in PyCharm terminal launch, probably because
    `.bash_aliases` is loaded before conda is set up in `.bashrc`
  * change to add to `.bashrc`

    ```text
    EnvironmentNameNotFound: Could not find conda environment: {env_name}
    You can list all discoverable environments with `conda info --envs`.
    ```

  * uninstalled mambaforge-pypy3
  * moved `~/.condarc` and `~/.conda/` aside
  * downloaded and installed `Miniforge-pypy3-Linux-arch64.sh`
  * copied `~/.conda.aside/environments.txt` into new empty `~/.conda/`
  * re-linked `~/dotfiles/pop_os/khawla/.condarc` as `~/.condarc`
  * still no auto-activation of the correct env in terminal
  * updated to PyCHarm 2024.1.1
  * updated support request with actions and results
* intermittent auth issues on waterhole machines started late in the afternoon


##### `graham` StdEnv/2023

* continued shelving migration to StdEnv/2023 for the time being:
  * SalishSeaCmd:
    * change beluga & cedar module loads to use Intel compiler collection, and fix tests
  * SalishSeaCast/docs
    * added intel/2023.2.1 module load
    * reverted build commands to use X64_GRAHAM arch file


##### 2x resolution SalishSeaCast

* experimented with running the notebook in PyCharm instead of VSCode
  * had to add notebook to conda env to get jupyter server for PyCharm



#### Thu 9-May-2024


##### Miscellaneous

* waterhole intermittent auth issue continued; posted message to Henryk in #oceanography


##### SalishSeaCast

* `upload_forcing graham nowcast+` failed with SSH protocol banner error; succeeded on manual re-try
  * recall that protocol banner error is due to network congestion
* `make_ww3_current_file forecast` and `make_ww3_wind_file forecast` stalled; killed them,
  and re-ran them manually


##### 2x resolution SalishSeaCast

* checked `e1t` and `e2t` grid variable extensions and found weirdness for `e2t`
  * it was because I used parabolic fitting instead of calculating e's from lons/lats via
    `haversine()`



#### Fri 10-May-2024


##### SalishSeaCast

* `crop_gribs 12` stalled with 1 file not processed; APCP in hour 016


##### 2x resolution SalishSeaCast

* started work on `e[12][tuvf]` calculations using `haversine()` formula
  * have to be super careful about which `g[lam|phi][tuvf]` arrays I use for each
  * e's are differences, so there are n-1 of them, but NEMO grid has n of them because
    an edge is padded with unused bogus values; decided with Susan to make them duplicates of
    adjacent real values
  * created and verified implementation of `haversine()` calls for all 8 e's


##### Miscellaneous

* coffee with Karyn



#### Sat 11-May-2024

* bike work and house work



#### Sun 12-May-2024

* rode to Deep Cove and back on Gunnars


##### SalishSeaCast

* wwatch3 nowcast and forecast runs didn't happen
  * re-ran nowcast manually; no logs from watcher
  * restarted log_aggregator



### Week 20

#### Mon 13-May-2024


##### SalishSeaCast

* `make_ww3_wind_file forecast2` stalled; re-run manually
  * run ended prematurely due to MPI error; checks show all node okay, so assume it was a transient
    issue
* `upload_forcing orcinus nowcast+` failed due to file system problem on `orcinus`
  * fix is expected to be completed by 11:00
  * recovery started at ~12:10:
    * upload_forcing orcinus nowcast+
    * upload_forcing orcinus turbidity
* `make_ww3_wind_file forecast` stalled; re-run manually


##### Miscellaneous

* Andrey at PyCharm reported that he can't reproduce my conda env auto-activation failure issue
  * in his test he disabled auto-activation of the base conda env and recommended I do the same;
    that made no difference, but it is valuable now that activation of the base env is not required
    to get conda and mamba in PATH, so I updated `.condarc` for `khawla` in `dotfiles/`


##### 2x resolution SalishSeaCast

* continued work on `e[12][tuvf]` calculations using `haversine()` formula



#### Tue 14-May-2024


##### Miscellaneous

* MOAD group mtg; see whiteboard
* help Tall with build issue on graham as his account was changed to default to StdEnv/2023
* watched YouTube recording of Tom Nicholas's presentation in today's Pangeo mtg on VirtualiZarr
  and how it differs from kerchunk's approach to a zarr layer over netCDF4 files


##### Security Updates

Squash-merged dependabot PR to update jinja2 to v3.1.4 re: CVE-2024-34064 re: XSS vulnerability:

* erddap-datasets



#### Wed 15-May-2024


##### Miscellaneous

* helped Susan w/ unreliable DNS at Quadra
  * home network DNS servers: 64.59.144.92 64.59.150.138


##### SalishSeaCast

* restarted HRDPS and hydrometric sarracenia clients at ~12:00 after MSC network maintenance
  * hydrometric csv file updates started downloading successfully at ~12:09
  * HRDPS client heartbeat success at 12:09 and 12:14


##### 2x resolution SalishSeaCast

* sorted out concatenation of new grid variable arrays to existing
* started work on creation of 202405 coordinates dataset



#### Thu 16-May-2024


##### SalishSeaCast

* `collect_weather 12` was ~1h30m late due to slow flow and long gaps
* `collect_weather 18` was also slow


##### 2x resolution SalishSeaCast

* started work on creation of 202405 `e[12][tuvf]` arrays; so confused 🙁



#### Fri 17-May-2024


##### SalishSeaCast

* `make_ww3_current_file forecast2` stalled; re-run manually
* HRDPS seemed to have returned to pre-maintenance timing, until 18 forecast which was ~90m late
* `make_ww3_wind_file forecast` stalled; re-run manually


##### 2x resolution SalishSeaCast

* continued work on creation of 202405 `e[12][tuvf]` arrays; still confused 🙁


##### SalishSeaNowcast

* started work on replacement of PyPDF2 package with pypdf
  * to resolve Jun-2023 security alert re: CVE-2023-36464 infinite loop vulnerability and
    deprecation of PyPDF2
  * branch: PyPDF2-to-pypdf
  * PR#263
  * https://pypdf.readthedocs.io/en/latest/index.html
  * test suite modernization
  * replaced PyPDF2 with pypdf in env and `make_surface_current_tiles` worker
  * added pypdf to skookum nowcast-env
  * tested branch on skookum, manually, and in automation



#### Sat 18-May-2024

Goofed off.


#### Sun 19-May-2024


##### SalishSeaNowcast

* finished replacement of PyPDF2 package with pypdf
  * to resolve Jun-2023 security alert re: CVE-2023-36464 infinite loop vulnerability and
    deprecation of PyPDF2
  * branch: PyPDF2-to-pypdf
  * PR#263 - squash-merged


##### SalishSeaCast

* updated `skookum` with merged PR#263 re: PyPDF2
  * removed PyPDF2 package from `nowcast-env`
* Changed paths for Tal & Susan's oxygen hindcast runs on optimum:
  * branch: rivers-hindcast
  * PR#264 - squash-merged



### Week 21

#### Mon 20-May-2024

**Statutory Holiday** - Victoria Day

Rode Iona, Sanctuary, 6 Rd loop of Richmond.


#### Tue 21-May-2024

Worked at ESB.


#### Miscellaneous

* MOAD mtg; see whiteboard

Squash-merged dependabot PRs to bump codecov/codecov-action to 4.1.1
re: dependency & feature updates:

* SalishSeaNowcast
* gha-workflows

Updated kudu to PyCharm 2024.1.1.

Updated my ocean installation to Miniforge-pypy3:

* moved `~/.condarc` and `~/.conda/environments.txt` aside
* uninstalled mambaforge-pypy3
  `conda init --reverse`
  `rm -rf ~/mambaforge-pypy3`  # took a very long time
* downloaded and installed `Miniforge-pypy3-Linux-arch64.sh`
* copied `~/.conda.aside/environments.txt` into new empty `~/.conda/`
* re-linked `~/dotfiles/ubuntu/ocean/.condarc` as `~/.condarc`

Updated my kudu installation to Miniforge-pypy3:

* moved `~/.condarc` and `~/.conda/environments.txt` aside
* uninstalled mambaforge-pypy3
  `conda init --reverse`
  `rm -rf /media/doug/warehouse/miniconda3`
* downloaded and installed `Miniforge-pypy3-Linux-arch64.sh`
* copied `~/.conda.aside/environments.txt` into new empty `~/.conda/`
* re-linked `~/dotfiles/ubuntu/ocean/.condarc` as `~/.condarc`


##### SalishSeaCast

* LiveOcean was ~80m late; download happened at ~11:20


##### Security Updates

Squash-merged dependabot PR to update requests to 2.32.0 re: CVE-2024-35195 re:
cert verification disablement leakage vulnerability:

* salishsea-site
* SalishSeaCast/docs
* cookiecutter-moad-pypkg
* Reshapr
* moad_tools
* NEMO-Cmd
* SalishSeaCmd
* tools/SalishSeaTools
* SalishSeaNowcast
* cookiecutter-analysis-repo
* AtlantisCmd
* NEMO_Nowcast
* MOAD/docs
* MoaceanParcels
* cookiecutter-djl-pypkg
* erddap-datasets
* SOG-Bloomcast-Ensemble



#### Wed 22-May-2024


##### SalishSeaCast

* arbutus network maintenance; seemed to have no impact on our runs
* `make_ww3_current_file forecast` stalled; re-run manually


##### 2x resolution SalishSeaCast

* continued work on creation of 202405 `e[12][tuvf]` arrays
  * funky values in southwest corner of grid; Susan traced them to funkiness there in the
    201702 grid that we're extrapolating from; decided that funkiness there is okay because it is
    land in Wa, very far from


Celebration of Becca's paper acceptance at the Gallery.



#### Thu 23-May-2024


##### SalishSeaCast

* `collect_weather 00` finished after `crop_gribs 00` timed out
  * ran `crop_gribs 00 --backfill` to recover before `collect_weather 12` finished
* `make_ww3_current_file forecast` stalled due to leftover process from yesterday; re-run manually


##### 2x resolution SalishSeaCast

* continued work on creation of 202405 `e[12][tuvf]` arrays
* created 202405 coordinates file


##### Miscellaneous

* UBC-IOS modeling Mtg
  * Maxim re: hydrological model



#### Fri 24-May-2024


##### SalishSeaCast

* `make_ww3_wind_file forecast2` stalled ; re-run manually


##### 2x resolution SalishSeaCast

* continued work on creation of 202405 `e[12][tuvf]` arrays


##### Reshapr

* updated hatch build wheel target inclusion list in `pyproject.toml`
  * branch: hatch-build-targets-wheel
  * PR#131 - squash-merged
* started experiment with h5netcdf instead of netcdf4
  * thinking that h5netcdf avoids the netcdf4 thread safety issues that cause random
    HDF5 and NETCDF4 errors when dask workers have more than 1 thread
  * may also allow resumption of use of `parallel=True` in `open_mfdataset()`
  * branch: h5netcdf
  * PR#132
  * tested for April month-avg physics on salish
    * success in 67s, but resulting file has all space coordinates called `gridY` ???



#### Sat 25-May-2024


##### SalishSeaCast

* `make_ww3_wind_file forecast` stalled ; re-run manually



#### Sun 26-May-2024


##### SalishSeaCast

* `download_live_ocean` was ~2h late



### Week 22

#### Mon 27-May-2024


#### Miscellaneous

Squash-merged dependabot PR to bump codecov/codecov-action to 4.1.1
re: dependency & feature updates:

* SalishSeaNowcast

Squash-merged dependabot PRs to bump mamba-org/setup-micromamba to 1.9.0
re: dependency, docs & bug fix updates:

* rwhite/numeric_2024
* erddap-datasets
* gha-workflows
* SalishSeaNowcast
* salishsea-site

Phys Ocgy seminar:

* CMOS practice talks by Camryn, Cassidy & Clare


##### 2x resolution SalishSeaCast

* finished work on creation of 202405 `e[12][tuvf]` arrays
* pushed for Susan to review



#### Tue 28-May-2024


##### Miscellaneous

MOAD group mtg; see whiteboard


##### Security Updates

Squash-merged dependabot PR to update requests to 2.32.0 re: CVE-2024-35195 re:
cert verification disablement leakage vulnerability:

* SOG-Bloomcast-Ensemble


##### Reshapr

* continued experiment with h5netcdf instead of netcdf4
  * branch: h5netcdf
  * PR#132
  * explored coordinate names issue
    * appears to be that `h5netcdf` writes netcdf4 in a way that is not compatible with `ncdump`
      nor `xarray.open_dataset(..., engine="netcdf4)`
      * this might be related to HDF5 dimension scales and how netCDF4 handles them
    * solution seems to be to read using `h5netcdf` and write using `netcdf4`



#### Wed 29-May-2024


##### 2x resolution SalishSeaCast

* started work on double resolution coordinates
  * added calculation of `g[lam|phi][tuvf]` arrays for double resolution coordinates


##### SalishSeaCast

* tested Reshapr `h5netcdf` branch in production
  * installed `h5netcdf` in `skookum nowcast-env`
  * pulled in `/SalishSeaCast/Reshapr` and switched to `h5netcdf` branch
  * restarted dask cluster workers in `tmux make_averaged_dataset` session on `salish`
    with `-nthreads=4`
  * checked results of `make_averaged_dataset` at ~12:00
    * `make_averaged_dataset day biology` failed with `KeyError: 'nitrate'`
    * success on manual re-run with `--debug`
    * success on manual re-run without `--debug`
  * tentative conclusions:
    * `engine="h5netcdf"` may be useful or even essential for analysis work that involves reading
      many dataset files and perhaps not writing a netCDF4 file (Becca's was writing with
      `pandas.Dataframe.to_pickle()`)
    * for Reshapr where `xarray.Dataset.to_netcdf(..., engine="netcdf4")` happens as the final step
      of any extraction, multiple threads per worker is probably still unreliable
* reattached orphaned `tmux make_averaged_dataset` session on `salish`
  * socket file got deleted somehow; https://timvisee.com/blog/reconnect-to-broken-tmux-session/
    explains how to recover:

    ```bash
    # use pgrep to find PID of tmux process
    pgrep -af make_averaged_dataset
    # send SIGUSR1 signal to tmux process to cause it to re-create socket file
    kill -SIGUSR1 PID
    # or kill -SIGUSR1 $(pgrep -f make_averaged_dataset)
    # attach tmux session
    tmux attach -t make_averaged_dataset
    ```


##### Reshapr

* continued experiment with h5netcdf instead of netcdf4
  * branch: h5netcdf
  * PR#132
  * made netcdf4 explicit write engine in tests for consistency with `extract.write_netcdf()`



#### Thu 30-May-2024


##### SalishSeaCast

* `make_ww3_wind_file forecast` stalled ; re-run manually
* continued testing Reshapr `h5netcdf` branch in production
  * checked results of `make_averaged_dataset` at ~12:00
    * `make_averaged_dataset day` succeeded for all 3 datasets; 1 fail from 8 runs
* updated SalishSeaNowcast deployment on `arbutus`
  * changed branch from `v202111-nowcast` to `main`
  * pulled and updated
  * updated env to install h5netcdf; lots of package changes
  * rsync-ed hacked version of `make_ww3_wind_file`
  * successful test of `make_ww3_wind_file forecast`
    * ~7 seconds for file creation


##### Miscellaneous

* updated PyCharm on khawla to 2024.1.2


##### SalishSeaNowcast

* tuned dask, etc. in `make_ww3_wind_file`:
  * `xarray.open_dataset()` for lons/lats
    * dropped unnecessary variables
    * changed to `engine="h5netcdf"`
  * `xarray.open_mfdataset()` for u_wind/v_wind
    * dropped `nav_lon` and `nav_lat` coordinates via `drop_variables=`
    * changed chunks to 24 hours instead of 1
    * changed to `engine="h5netcdf"`
  * added `ds.compute()` to control dask scheduler:
    * processes and max_workers=8
  * made `ds.to_netcdf()` explicitly use `engine="netcdf4"`
  * updated envs to include `h5netcdf`
  * updated unit tests



#### Fri 31-May-2024


##### SalishSeaCast

* `make_ww3_current_file forecast2` stalled; killed and skipped; it delayed nowcast/forecast runs
* LiveOcean download was ~2h late
* continued testing Reshapr `h5netcdf` branch in production
  * checked results of `make_averaged_dataset` at ~14:00:
    * `make_averaged_dataset day biology` failed with `KeyError: microzooplankton
    * re-ran manually
    * 2 fails from 12 runs
  * restarted dask cluster workers in `tmux make_averaged_dataset` session on `salish`
    with `-nthreads=1`
* rsync-ed hacked version of `make_ww3_current_file`
  * successful test of `make_ww3_current_file forecast`
    * ~53 seconds for file creation
* `collect_weather 00` was ~2h late


##### SalishSeaNowcast

* tuned dask, etc. in `make_ww3_current_file`:
  * `xarray.open_dataset()` for lons/lats
    * dropped unnecessary variables
    * changed to `engine="h5netcdf"`
  * `xarray.open_mfdataset()` for u_wind/v_wind
    * dropped unnecessary variables
    * changed chunks to 1 hour instead of 3
    * changed to `engine="h5netcdf"`
  * added `ds.compute()` to control dask scheduler:
    * processes and max_workers=8
  * made `ds.to_netcdf()` explicitly use `engine="netcdf4"`



## June

<!-- markdownlint-disable MD001 -->
#### Sat 1-Jun-2024
<!-- markdownlint-enable MD001 -->


##### SalishSeaCast

* hacked `make_ww3_*_file forecast*` ran successfully
* continued testing Reshapr `h5netcdf` branch in production
  * checked results of `make_averaged_dataset` at ~12:00:
    * `make_averaged_dataset day` succeeded for all 3 datasets; 2 fails from 15 runs


##### SalishSeaNowcast

* tuned dask, etc. in `make_ww3_*_file`:
  * branch: improve-ww3-prep
  * updated `test_make_ww3_current_file`



#### Sun 2-Jun-2024


##### SalishSeaCast

* updated conda on arbutus and ended up with:
  * `Error while loading conda entry point: conda-libmamba-solver (libarchive.so.19:
    cannot open shared object file: No such file or directory)`



### Week 23

#### Mon 3-Jun-2024


##### SalishSeaCast

* `crop_gribs 06` timed out with 270 files unprocessed
  * `find` operations in `/results/forcing/atmospheric/continental2.5/GRIB/20240306/06/`
    on `skookum` keep freezing terminal sessions
  * killed `collect_weather 06` and `crop_gribs 06`
  * `crop_gribs 06 --backfill` failed due to missing `044/APCP` file
  * 157 file remain in `/SalishSeaCast/datamart/hrdps-continental/06/`
  * manually launched `collect_weather 12 2.5km` and `crop_gribs 12` at 07:20
  * asked Henryk to check RAID status of `/results`
  * successfully ran `download_weather 06 2.5km` on `khawla`
  * checked `grib_to_netcdf` code to confirm that 06 forecast is only used for forecast2 runs,
    not nowcast/forecast runs
* Slack conversation w/ Henryk:
  * one of the `/results/` drives dropped out of the `md127_raid5` soft-RAID overnight,
    then reconnected
  * RAID is rebuilding parity slowly; file system is slow as a result
  * Henryk's plan is to force-reboot `skookum` on Tue afternoon and remove to mount of `/results`
    in the hope that will allow the RAID rebuild to complete
* `sarracenia` successfully collected 12 HRDPS files on `/SalishSeaCast/datamart/`
* recovery started at ~15:00:
  * hacked `nowcast.yaml` to put atmospheric forcing on `/results2/` and created directory tree there
  * `collect_weather 12 2.5km --backfill --backfill-date 2024-06-03`
  * `crop_gribs 12 --backfill`
  * copied 18 and 00 GRIB files that `grib_to_netcdf` needs from `/results/` to `results2/`
  * `grib_to_netcdf nowcast+`
  * `collect_ECCC_river_data.sh 2024-06-02`
  * `collect_USGS_river_data.sh 2024-06-02`
  * `collect_NeahBay_ssh 06`
  * `download_live_ocean`
  * `download_weather 00 1km`
  * `download_weather 12 1km`
  * `collect_weather 18 2.5km --backfill --backfill-date 2024-06-03`
  * `crop_gribs 18 --backfill`
* gave up trying to get runs to start; best hope is to keep collecting forcing products
  * `collect_weather 00 2.5km`
  * `crop_gribs 00 2024-06-04`
  * successful
* replaced `miniconda3` with `miniforge-pypy3` on arbutus:
  * no `~/.condarc`
  * moved `~/.conda/environments.txt` aside
  * uninstalled miniconda3
    `conda init --reverse`
    `rm -rf /nemoShare/MEOPAR/nowcast-sys/miniconda3`
  * downloaded and installed `Miniforge-pypy3-Linux-arch64.sh`
  * copied `~/.conda.aside/environments.txt` into new empty `~/.conda/`


##### Miscellaneous

Checked status of scheduled GHA workflows:

  ```bash
  conda activate gha-workflows
  python /media/doug/warehouse/MOAD/gha-workflows/gha_workflow_checker/gha_workflows_checker.py
  ```


#### Tue 4-Jun-2024


##### SalishSeaCast

* overnight:
  * success:
    * `collect_weather 06 2.5km`
    * `crop_gribs 06`
    * `grib_to_netcdf`
    * `collect_river_data ECCC`
    * `get_onc_ferry`
    * `collect_NeahBay_ssh`
  * failure:
    * `get_onc_ctd`
    * `make_ssh_file` due to missing directory on `/results2`; resolved
* today:
  * success:
    * `collect_weather 12 2.5km`
    * `grib_to_netcdf`
    * `collect_river_data USGS`
    * `collect_NeahBay_ssh`
    * `download_live_ocean`
    * `make_turbidity_file`
    * `make_live_ocean_files`
  * failure:
    * `crop_gribs 12`
    * `make_ssh_file`
    * `make_runoff_file`
    * `make_v202111_runoff_file`
  * Henryk rebooted `skookum` at noon
    * removed `/results` mount to try to get RAID rebuild to complete
    * replaced failed drive and restarted RAID rebuild at ~17:00; expects ~15h
  * restarted automation, etc at ~18:30:
    * nowcast automation
    * salishsea-site
    * ERDDAP
    * `download_weather 00 1km`
    * `download_weather 12 1km`
    * `download_weather 18 2.5km`
    * `crop_gribs 18 --backfill`
    * `collect_weather 00 2.5km`
    * `crop_gribs 00 2024-06-05`


##### SalishSeaNowcast

* tuned dask, etc. in `make_ww3_*_file`:
  * branch: improve-ww3-prep
  * started commits


#### Wed 5-Jun-2024


##### SalishSeaCast

* overnight:
  * success:
    * `collect_weather 06 2.5km`
    * `crop_gribs 06`
    * `collect_NeahBay_ssh`
    * `grib_to_netcdf`
  * failure:
    * `collect_river_data ECCC` due to no `/results`
    * `make_ssh_file` due to no `/results`
    * `get_onc_ctd` due to no `/results`
    * `get_onc_ferry` due to no `/results`
* today:
  * success:
    * `collect_weather 12 2.5km`
    * `crop_gribs 12`
    * `grib_to_netcdf`
    * `download_live_ocean`
    * `make_live_ocean_files`
    * `collect_NeahBay_ssh`
  * failure:
    * `collect_river_data USGS` due to no `/results`
    * `make_ssh_file` due to no `/results`
    * `make_runoff_file`
    * `make_v202111_runoff_file`
    * `make_turbidity_file`  due to no `/results`
* Henryk rebooted `skookum` to remount `/results` at ~12:00; started recovery:

  ```bash
  sudo sysctl fs.inotify.max_user_instances=2048
  sudo sysctl fs.inotify.max_user_watches=196608
  sudo sysctl -p
  sudo /opt/tomcat/bin/startup.sh  # ERDDAP
  mamba activate /SalishSeaCast/salishsea-site-env  # website
  supervisord -c /SalishSeaCast/salishsea-site/supervisord-prod.ini
  mamba deactivated
  mamba activate /SalishSeaCast/nowcast-env  # automation
  mamba activate /SalishSeaCast/nowcast-env
  supervisord -c $NOWCAST_CONFIG/supervisord.ini
  collect_weather 18 2.5km &
  crop_gribs 18 &
  ```

* started backfilling at 13:30:

  ```bash
  git restore config/nowcast.yaml
  # 3jun
  mv /results/forcing/atmospheric/continental2.5/GRIB/20240602/06 06.aside
  download_weather 06 2.5km --run-date 2024-06-03 --debug
  crop_gribs 06 --backfill --fcst-date 2024-06-03 --debug
  rm -rf /results/forcing/atmospheric/continental2.5/GRIB/20240602/06.aside
  bash /results/forcing/rivers/observations/collect_ECCC_river_data.sh 2024-06-02  # failed: no obs
  bash /results/forcing/rivers/observations/collect_USGS_river_data.sh 2024-06-02
  rsync -av /results2/forcing/atmospheric/continental2.5/GRIB/20240603/12 \
    /results/forcing/atmospheric/continental2.5/GRIB/20240603/
  make_turbidity_file 2024-06-03 --debug  # insufficient data
  collect_NeahBay_ssh 06 --data-date 2024-06-03 --debug
  rsync -av /results2/forcing/LiveOcean/downloaded/20240603 /results/forcing/LiveOcean/downloaded/
  make_ssh_files nowcast 2024-06-03 --debug
  make_live_ocean_files 2024-06-03 --debug
  make_v202111_runoff_file --data-date 2024-06-02 --debug
  make_runoff_file --run-date 2024-06-03 --debug
  grib_to_netcdf $NOWCAST_YAML nowcast+ --run-date 2024-06-03 --debug
  upload_forcing arbutus nowcast+ 2024-06-03
  upload_forcing orcinus nowcast+ 2024-06-03
  upload_forcing optimum nowcast+ 2024-06-03
  upload_forcing graham nowcast+ 2024-06-03
  get_onc_ctd SEVIP 2024-06-02
  get_onc_ferry TWDP 2024-06-02
  rsync -av /results2/forcing/atmospheric/continental2.5/GRIB/20240603/18 \
    /results/forcing/atmospheric/continental2.5/GRIB/20240603/
  rsync -av /results2/forcing/atmospheric/GEM1.0/GRIB/20240603/00 \
    /results/forcing/atmospheric/GEM1.0/GRIB/20240603/
  rsync -av /results2/forcing/atmospheric/GEM1.0/GRIB/20240603/12 \
    /results/forcing/atmospheric/GEM1.0/GRIB/20240603/

  # 4jun
  rsync -av /results2/forcing/atmospheric/continental2.5/GRIB/20240604/00 \
    /results/forcing/atmospheric/continental2.5/GRIB/20240604/
  rsync -av /results2/forcing/atmospheric/continental2.5/GRIB/20240604/06 \
    /results/forcing/atmospheric/continental2.5/GRIB/20240604/
  bash /results/forcing/rivers/observations/collect_ECCC_river_data.sh 2024-06-03  # failed: no obs
  rsync -av /results2/forcing/atmospheric/continental2.5/GRIB/20240604/12 \
    /results/forcing/atmospheric/continental2.5/GRIB/20240604/
  crop_gribs 12 --backfill --fcst-date 2024-06-04 --debug
  bash /results/forcing/rivers/observations/collect_USGS_river_data.sh 2024-06-03
  make_turbidity_file 2024-06-04 --debug  # insufficient data
  collect_NeahBay_ssh 06 --data-date 2024-06-04 --debug
  rsync -av /results2/forcing/LiveOcean/downloaded/20240604 /results/forcing/LiveOcean/downloaded/
  make_ssh_files nowcast 2024-06-04 --debug
  make_live_ocean_files 2024-06-04 --debug
  make_v202111_runoff_file --data-date 2024-06-03 --debug
  make_runoff_file --run-date 2024-06-04 --debug
  get_onc_ctd SEVIP 2024-06-03
  get_onc_ferry TWDP 2024-06-03
  grib_to_netcdf $NOWCAST_YAML nowcast+ --run-date 2024-06-04 --debug
  upload_forcing arbutus nowcast+ 2024-06-04
  upload_forcing orcinus nowcast+ 2024-06-04
  upload_forcing optimum nowcast+ 2024-06-04
  upload_forcing graham nowcast+ 2024-06-04
  rsync -av /results2/forcing/atmospheric/continental2.5/GRIB/20240604/18 \
    /results/forcing/atmospheric/continental2.5/GRIB/20240604/
  rsync -av /results2/forcing/atmospheric/GEM1.0/GRIB/20240604/00 \
    /results/forcing/atmospheric/GEM1.0/GRIB/20240604/
  rsync -av /results2/forcing/atmospheric/GEM1.0/GRIB/20240604/12 \
    /results/forcing/atmospheric/GEM1.0/GRIB/20240604/

  # 5jun
  rsync -av /results2/forcing/atmospheric/continental2.5/GRIB/20240605/00 \
    /results/forcing/atmospheric/continental2.5/GRIB/20240605/
  rsync -av /results2/forcing/atmospheric/continental2.5/GRIB/20240605/06 \
    /results/forcing/atmospheric/continental2.5/GRIB/20240605/
  bash /results/forcing/rivers/observations/collect_ECCC_river_data.sh 2024-06-04
  rsync -av /results2/forcing/atmospheric/continental2.5/GRIB/20240605/12 \
    /results/forcing/atmospheric/continental2.5/GRIB/20240605/
  bash /results/forcing/rivers/observations/collect_USGS_river_data.sh 2024-06-04
  make_turbidity_file 2024-06-05 --debug  # insufficient data
  collect_NeahBay_ssh 06 --data-date 2024-06-05 --debug
  rsync -av /results2/forcing/LiveOcean/downloaded/20240605 /results/forcing/LiveOcean/downloaded/
  make_ssh_files nowcast 2024-06-05 --debug
  make_live_ocean_files 2024-06-05 --debug
  get_onc_ctd SEVIP 2024-06-05
  get_onc_ferry TWDP 2024-06-05
  ```


#### Thu 6-Jun-2024


##### SalishSeaCast

* overnight downloads and obs collection workers were successful
* `forecast2/04jun24` run launched and stalled at 41.7%; killed; errors like:
        iom_get_123d, file: ./NEMO-atmos/hrdps_y2024m06d06.nc, var: precip
        start and count too big regarding to the size of the data,
        (istart(3) + icnt(3) - 1) =    14
        is larger than idimsz(3) =    13
* continue backfilling:
  * wait for `nowcast` run to fail due to no 5jun run

  ```bash
  grib_to_netcdf $NOWCAST_YAML nowcast+ --run-date 2024-06-05
  upload_forcing arbutus nowcast+ 2024-06-05
  upload_forcing orcinus nowcast+ 2024-06-05
  upload_forcing optimum nowcast+ 2024-06-05
  upload_forcing graham nowcast+ 2024-06-05

  # 6jun
  # wait for 5jun runs to finish at ~12:15
  make_forcing_links arbutus nowcast+
  ```

* `forecast/06jun24` run launched and stalled at 34.7%; errors as above; killed
  * Susan diagnosed the problem as non-existent atmospheric forcing files


##### SalishSeaNowcast

* Updated `make_live_ocean_files` worker re: single filepath instead of list:
  * branch: fix-live-ocean-filepath-msgs
  * PR#269 - squash-merged
  * info message and checklist item were empty because
    `salishsea_tools.LiveOcean_BCs.create_LiveOcean_TS_BCs()` returns a single filepath not a list of
    filepaths



#### Fri 7-Jun-2024


##### Security Updates

Squash-merged dependabot PRs to update tornado to 6.4.1 re:
multiple vulnerabilities:

* MoaceanParcels
* MOAD/docs
* SalishSeaCast/docs
* tools/SalishSeaTools
* moad_tools
* Reshapr
* SalishSeaNowcast


##### SalishSeaCast

* today's forecast run was successful
* backfill forecast/06jun24 and wwatch3/nowcast/06jun24 and 07jun24 runs:

  ```bash
  # NEMO forecast/06jun24
  make_forcing_links nowcast+ 2024-06-06 --debug
  make_forcing_links ssh 2024-06-06
  # failed, and automation launched next runs
  # retry
  make_forcing_links nowcast+ 2024-06-06 --debug
  make_forcing_links ssh 2024-06-06 --debug
  run_NEMO arbutus forecast 2024-06-06 --debug  # on arbutus
  # failed again, complaining about array sized in fcst/hrdps_y2024m06d07.nc, I think
  grib_to_netcdf nowcast+ 2024-06-06 --debug
  upload_forcing nowcast+ 2024-06-06 --debug
  make_forcing_links nowcast+ 2024-06-06 --debug
  make_forcing_links ssh 2024-06-06 --debug
  run_NEMO arbutus forecast 2024-06-06 --debug  # on arbutus
  download_results arbutus forecast 2024-06-06
  # wwatch3/06jun24
  make_ww3_wind_file forecast 2024-06-06
  make_ww3_current_file forecast 2024-06-06
  # wwatch3/07jun24
  make_ww3_wind_file forecast 2024-06-07
  make_ww3_current_file forecast 2024-06-07
  # failed - I give up
  ```


##### SalishSeaNowcast

* tuned dask, etc. in `make_ww3_*_file`:
  * branch: improve-ww3-prep
  * finished commits
  * PR#271



#### Sat 8-Jun-2024


##### SalishSeaCast

* `make_ww3_current_file forecast2` failed
      unable to open file:
      name = '/nemoShare/MEOPAR/nowcast-sys/wwatch3-runs/current/SalishSea_1h_20240608_20240608_grid_U.nc'
* `make_plots nemo forecast2 publish` failed in `compare_tide_prediction_max_ssh.py` call of
  `salishsea_tools.wind_tools.calc_wind_avg_at_point()`
      ValueError: can only convert an array of size 1 to a Python scalar
* `make_plots nemo forecast publish` failed similarly
* `crop_gribs 00` failed due to not directory to watch despite race condition mitigation code



#### Sun 9-Jun-2024

Goofed off. Cycled 85 km around Richmond.



### Week 24

#### Mon 10-Jun-2024


##### SalishSeaCast

* `crop_gribs 06` failed with 484 files unprocessed
  * only a few files from hours 001 to 006 published on hpfx as of 09:00
  * finally finished at ~10:45
* recovery:
  * manually started `collect_weather 12 2.5km` and `crop_gribs 12`
  * manually ran obs collection workers, etc. that automation runs after `collect_weather 06`:

    ```bash
    bash /results/forcing/rivers/observations/collect_ECCC_river_data.sh 2024-06-09
    get_onc_ctd SEVIP
    get_onc_ferry TWDP
    grib_to_netcdf forecast2
    ```

* `collect_weather 12` got a few files around 08:30, then the flow stopped
  * `collect_weather 12` finished at ~11:35
  * `crop_gribs 12` finished at ~11:45
* `make*_runoff_file` failed



#### Tue 11-Jun-2024

Worked at ESB.


##### Miscellaneous

* MOAD mtg; see whiteboard
* Helped Becca with archiving `ariane` results to `graham:/nearline/` and
  testing `ncks -4 -L4` compression of `ariane` results files
* updated `kudu` to PyCharm 2024.1.3


##### Security Updates

Squash-merged dependabot PRs to update tornado to 6.4.1 re:
multiple vulnerabilities:

* erddap-datasets
* SOG-Bloomcast-Ensemble
* SOG-Bloomcast


##### SalishSeaCast

* confirmed that `make_averaged_dataset day` has worked successfully since 31may when I changed the
  dask cluster on `salish` to `--nthreads 1`


##### Reshapr

* tried unsuccessfully to reproduce the broken coordinates with `h5netcdf` for
  writes issue that I saw for a bug report



#### Wed 12-Jun-2024


##### SalishSeaCast

* LiveOcean was delayed until ~11:10


##### Miscellaneous

* updated `khawla` to PyCharm 2024.1.3


##### Atlantis

* helped Raisha make her notebook that parses Parcels output into spill input for Atlantis work
  with the zarr output that Parcels now produces



#### Thu 13-Jun-2024


##### Miscellaneous

* did preliminary searches for `[np|numpy].NAN` and `[np|numpy].NaN` that need to be changed to
  `[np|numpy].nan` for numpy 2.0


##### SalishSeaNowcast

* tuned dask, etc. in `make_ww3_*_file`:
  * branch: improve-ww3-prep
  * PR#271 - squash-merged
  * no stalls since 1jun, so decided to merge
  * pull updates on `skookum` and `arbutus`
* Released v24.1
* updated all 1st party package clones on `skookum` and `arbutus`
* started work on fixing warnings revealed by `pytest`



#### Fri 14-Jun-2024


##### SalishSeaNowcast

* finished work on fixing warnings revealed by `pytest`
  * branch: fix-pytest-warnings
  * PR#273


##### SalishSeaCast

* after `collect_weather 18` finished:
  * built new Python 3.12 nowcast-env on `skookum`
  * replaced `tmux make_averaged_dataset` with new one using new env


JRA arrived for the weekend



#### Sat 15-Jun-2024


##### SalishSeaCast

* `nowcast-blue` stalled at 93.7% (23 hours completed)
  * with a lot of help from Susan, traced the problem to `cfgrib` pkg that was updated from 0.9.10.3
    to 0.9.12.0 in the new env
    * it produces cropped grib files in which all times are the same, apparently because their `time`
      and `valid_time` values are the same rather than `time` being `00:00` and `valid_time` being
      the hour offset; e.g. `06:00`
* `upload_forcing orcinus` failed


##### SalishSeaNowcast

* started debugging `cfgrib` issue
  * reverted `khawla` dev env to `cfgrib 0.9.10.3` and got correct cropped grib files in debug tests



#### Sun 16-Jun-2024


##### SalishSeaNowcast

* continued debugging `cfgrib` issue
  * updated `khawla` dev env to `cfgrib 0.9.10.4`
    * test worked
    * `FutureWarning: GRIB write support is experimental, DO NOT RELY ON IT!` appeared, although
      it appears to have been in the `cfgrib` code for 6 years, this is the first time I recall
      seeing it
  * updated `khawla` dev env to `cfgrib 0.9.11.0`
    * test worked
  * updated `khawla` dev env to `cfgrib 0.9.12.0`
    * test failed
  * issue is probably due to https://github.com/ecmwf/cfgrib/pull/371


##### SalishSeaCast

* changed to `cfgrib 0.9.11.0` in `skookum:nowcast-env`
* started backfilling:

  ```bash
  crop_gribs 00 --backfill --fcst-date 2024-06-15 --debug
  crop_gribs 06 --backfill --fcst-date 2024-06-15 --debug  # 12:02 to 12:18
  crop_gribs 12 --backfill --fcst-date 2024-06-15 --debug  # 12:33 to 12:
  grib_to_netcdf 2024-06-15 --debug
  upload_forcing arbutus 2024-06-15
  upload_forcing optimum 2024-06-15
  upload_forcing robot.graham 2024-06-15
  ~upload_forcing orcinus 2024-06-15~  # skipped due to orcinus offline
  # wait for runs to finish at ~15:15
  crop_gribs 18 --backfill --fcst-date 2024-06-15 --debug
  crop_gribs 00 --backfill --fcst-date 2024-06-16 --debug
  crop_gribs 06 --backfill --fcst-date 2024-06-16 --debug
  crop_gribs 12 --backfill --fcst-date 2024-06-16 --debug
  grib_to_netcdf 2024-06-16 --debug
  upload_forcing arbutus 2024-06-16
  upload_forcing optimum 2024-06-16
  upload_forcing robot.graham 2024-06-16
  ~upload_forcing orcinus 2024-06-16~  # skipped due to orcinus offline
  crop_gribs 18 --backfill --fcst-date 2024-06-16 --debug
  ```



### Week 25

#### Mon 17-Jun-2024


##### SalishSeaCast

* 2h12m from `collect_weather 12` finish to `nowcast-green` finish today vs. 2h46m on 14jun
* lots of messages from `make_averaged_dataset` like:

  ```text
  2024-06-17 11:54:30,492 INFO [make_averaged_dataset] Entering _validate_reindex: reindex is None
  2024-06-17 11:54:30,493 INFO [make_averaged_dataset] Leaving _validate_reindex: method = None, returning None
  2024-06-17 11:54:30,494 INFO [make_averaged_dataset] _choose_engine: Choosing 'flox'
  2024-06-17 11:54:30,494 INFO [make_averaged_dataset] _choose_method: method is None
  2024-06-17 11:54:30,495 INFO [make_averaged_dataset] _choose_method: choosing preferred_method=blockwise
  ```


#### Miscellaneous

Squash-merged dependabot PRs to bump codecov/codecov-action to 4.5.0
re: dependency & feature updates:

* SalishSeaNowcast
* gha-workflows

Updated dev envs to get jupyter_server 2.14.1 into `requirements.txt` files re: security alerts that
dependabot can't resolve re: Jupyter server on Windows discloses Windows user password hash:

* erddap-datasets
* MoaceanParcels
* tools/SalishSeaTools
* SOG-Bloomcast-Ensemble

Squash-merged dependabot PRs to bump urllib3 to 2.2.2 re: CVE-2024-37891 re: cross-origin redirect
authentication vulnerability:

* AtlantisCmd
* MOAD/docs
* moad_tools
* SalishSeaCast/docs
* Reshapr
* SalishSeaNowcast
* SalishSeaCmd
* salishsea-site
* NEMO-Cmd

Squash-merged dependabot PR to bump scikit-learn to 1.5.0 re: CVE-2024-5206 re: sensitive data
leakage vulnerability:

* moad_tools



#### Tue 18-Jun-2024

Worked at ESB.


##### Security Updates

Squash-merged dependabot PRs to update urllib3 to 2.2.2 re: CVE-2024-37891 re: cross-origin redirect
authentication vulnerability:

* cookiecutter-MOAD-pkg
* NEMO_Nowcast
* cookiecutter-analysis-repo
* cookiecutter-djl-pypkg
* SOG-Bloomcast


##### Miscellaneous

* MOAD mtg; see whiteboard
  * presentations for Zhiguo He (sabbatical visitor) next week


##### cfgrib bug

* dug into invalid values for `valid_time` variable from `cfgrib=0.9.12.0`
* created private douglatornell/cfgrib-bug repo
  * wrote code that reproduces the issue seen in `crop_gribs` without cropping
    * almost certainly related to changes in cfgrib that added support
      for sub-hour steps feature of `ecCodes=2.34.0`
    * issue: https://github.com/ecmwf/cfgrib/issues/370
    * PR that resolves issue, but probably creates our problem:
      https://github.com/ecmwf/cfgrib/pull/371


##### SS150

* discussed getting Michael's SS150 NEMO configuration running with Susan & Camryn:
  * just another NEMO config?
  * run initially on `salish` maybe
  * need a worker (and probably standalone module) to calculate SS150 boundary
    conditions file from `nowcast-green` results
  * need atmospheric forcing weights file for SS150
* meeting w/ Camryn next Tuesday



#### Wed 19-Jun-2024


##### SalishSeaCast

* `get_onc_ctd SEVIP` generating reindex messages in log:

  ```text
  2024-06-19 03:08:44,005 INFO [get_onc_ctd] Entering _validate_reindex: reindex is None
  2024-06-19 03:08:44,007 INFO [get_onc_ctd] Leaving _validate_reindex: method = None, returning None
  2024-06-19 03:08:44,009 INFO [get_onc_ctd] _choose_engine: Choosing 'flox'
  ```

  then fails with `ValueError: __resample_dim__ must not be empty` from:

  ```python-traceback
  File "/SalishSeaCast/SalishSeaNowcast/nowcast/workers/get_onc_ctd.py", line 176, in _create_dataset
    salinity_mean = salinity.resample(time="15Min").mean()
  ```

* `make_plots nemo forecast[2] publish` also generating reindex messages in log

* `flox` added INFO level log messages re: heuristics for auto-guessing aggregation method that was
  incorporated in xarray in 2024.02.2


##### SalishSeaNowcast

* pinned cfgrib dependency at 0.9.11.0 until we get a resolution for the incorrect `valid_time`
  issue that seems to arise from support for GRIB files with sub-hourly steps in 0.9.12.0:
  * branch: pin-cfgrib-0.9.11.0
  * PR#276 - squash-merged
* replaced warning suppression context manager in `crop_gribs._xarray_to_grib()` with `no_warn=True`
  in `xarray_to_grib.to_grib()` call
  * branch: xarray_to_grib-no_warn
  * PR#277 - squash-merged
  * deployed to production



#### Thu 20-Jun-2024


##### SalishSeaCast

* orcinus was down due to scheduled building electrical maintenance that I must have forgotten about;
  that was followed by chiller problems on restart
* started backfilling `nowcast-agrif` runs:

  ```bash
  # wait for run to fail
  upload_forcing orcinus nowcast+ 2024-06-15  --debug
  upload_forcing orcinus turbidity 2024-06-15 --debug
  upload_forcing orcinus nowcast+ 2024-06-16 --debug
  upload_forcing orcinus turbidity 2024-06-16 --debug
  upload_forcing orcinus nowcast+ 2024-06-17 --debug
  upload_forcing orcinus turbidity 2024-06-17 --debug
  upload_forcing orcinus nowcast+ 2024-06-18 --debug
  upload_forcing orcinus turbidity 2024-06-18 --debug
  upload_forcing orcinus nowcast+ 2024-06-19 --debug
  upload_forcing orcinus turbidity 2024-06-19 --debug
  upload_forcing orcinus nowcast+ 2024-06-20 --debug
  upload_forcing orcinus turbidity 2024-06-20 --debug
  make_forcing_links nowcast-agrif 2024-06-15
  make_forcing_links nowcast-agrif 2024-06-16
  make_forcing_links nowcast-agrif 2024-06-17
  make_forcing_links nowcast-agrif 2024-06-18
  make_forcing_links nowcast-agrif 2024-06-19
  make_forcing_links nowcast-agrif 2024-06-20
  ```

* backfill `get_onc_ctd SEVIP`:

  ```bash
  get_onc_ctd SEVIP 2024-06-14
  get_onc_ctd SEVIP 2024-06-15
  get_onc_ctd SEVIP 2024-06-16
  get_onc_ctd SEVIP 2024-06-17
  get_onc_ctd SEVIP 2024-06-18
  get_onc_ctd SEVIP 2024-06-19
  ```


##### SalishSeaNowcast

* dug into INFO level reindex log messages from `flox`:
  * I think the best solution would be to demote them in `flox`; it looks like the PR that
    introduced them was started by one person and finished in haste by another
* dug into `ValueError: __resample_dim__ must not be empty` for salinity processing in `get_onc_ctd`
  * this is due to an empty salinity DataArray that previously raised IndexError
  * branch:
  * PR#278 - squash-merged
  * added ValueError to exception catching for empty salinity DataArray
  * deployed to production


##### Miscellaneous

* proposed on xarray general discussion that I would do a PR for flox to change INFO level logging
  messages to DEBUG; @dcherian agreed that it should be done and asked about logging config



#### Fri 21-Jun-2024


<!-- markdownlint-disable MD036 -->
**EOAS owncloud and /home server down from 17:00 to 19:00**
<!-- markdownlint-enable MD036 -->


##### Miscellaneous

* deleted SalishSeaCast/libwgrib2 fork from aborted approach to HRDPS continental grid GRIB
  processing
* prepared for presentation for Zhiguo He at MOAD mtg on Tuesday
  * "slides"
    * presentations/SalishSeaCast_block_diagram.png
    * presentations/CMOS-2018/Doug/AutomationFlow.svg
    * https://salishsea-nowcast.readthedocs.io/en/latest/index.html#process-flow
    * presentations/OceanPredict2019/wheel.png
    * web publishing: https://salishsea.eos.ubc.ca/nemo/
  * created Google doc with headings and images to outline what I and others will talk about


##### SSS150

* learned from Michael that SSS150 stand for South Salish Sea 150m resolution because
  "It only covers a modest amount of the SS =)"
* reviewed Michael's https://github.com/SalishSeaCast/NEMO-3.6-code/pull/6
  * copies `bdydta.F90` into config `MY_SRC/`
  * adds sea surface height boundary condition code to 3 files:
    * `bdydta.F90`
    * `bdydyn2d.F90`
    * `bdyini.F90`
  * need to decide if the changes go into SalishSeaCast config, or a new one


##### Minecraft

* stopped server
* did lizzy-smelt backup
* set up 1.21 server

  ```bash
  mkdir ~/Games/MinecraftFabric1.21Server
  cd ~/Games/MinecraftFabric1.21Server
  curl -OJ https://meta.fabricmc.net/v2/versions/loader/1.21/0.15.11/1.0.1/server/jar
  cd ~/Games/MinecraftFabric1.20.4Server
  cp banned-* eula.txt ops.json whitelist.json start.sh ../MinecraftFabric1.21Server/
  cd ~/Games/MinecraftFabric1.21Server
  ```

  * edited `start.sh` to:

    ```bash
    #!/usr/bin/env bash
    java -Xmx6G -jar fabric-server-mc.1.21-loader.0.15.11-launcher.1.0.1.jar nogui
    ```

  * edited `server.properties` to sync with 1.20.4 settings

  ```bash
  cd ~/Games/MinecraftFabric1.21Server/mods/
  curl -LO https://github.com/CaffeineMC/lithium-fabric/releases/download/mc1.21-0.12.7/lithium-fabric-mc1.21-0.12.7.jar
  cd ~/Games/MinecraftFabric1.21Server
  rsync -av ../MinecraftFabric1.20.4Server/1-20-1-25jul23 ./
  # delete double shulker shells datapack - not yet available for 1.21
  rm 1-20-1-25jul23/datapacks/double\ shulker\ shells\ v1.3.6\ \(MC\ 1.20-1.20.4\).zip

  tmux attach -t minecraft-server
  ./start.sh
  ```

* set up 1.21 client instance in MultiMC
  * install `openjdk-21-jre`

    ```bash
    sudo apt update
    sudo apt install openjdk-21-jre
    ```

  * created instance
  * installed fabric 0.15.11
  * downloaded and installed loader mods:
    * sodium-fabric-0.5.9+mc1.21.jar
    * lithium-fabric-mc1.21-0.12.7.jar
    * malilib-fabric-1.21-0.19.999-sakura.2.jar
    * minihud-fabric-1.21-0.31.999-sakura.3.jar
    * tweakeroo-fabric-1.21-0.20.999-sakura.5.jar
    * iris-1.7.1+mc1.21.jar
  * Fresh Animations isn't available for 1.21 yet, though `Entity [Model|Texture] Features` are
  * downloaded and installed ComplementaryUnbound_r5.2.1.zip shaders
  * downloaded and installed Vanilla Tweaks resource packs:
    * iron bars fix
    * lower shield
    * redstone devices:
      * StickyPistonSides
      * DirectionalHoppers
      * DirectionalDispensersDroppers
      * DirectionalObservers
      * GroovyLevers
      * RedstoneWireFix



#### Sat 22-Jun-2024

Goofed off.



#### Sun 23-Jun-2024

Goofed off.



### Week 26

#### Mon 24-Jun-2024


##### SalishSeaCast

* `download_live_ocean` failed at 10:15
  * sentinel file, but no netCDF file
  * sent email to Parker at ~10:55
  * got the file be email from Jilian Xiong of Parker's group
  * uploaded file to `/results/` and ran `make_live_ocean_files` to restart automation


##### Miscellaneous

* phys ocgy seminar: Stephanie, PRODIGY turbulence lecture


##### SSS150

* started writing `sss150 Implementation Plan` canvas in #sss150 channel on Slack



#### Tue 25-Jun-2024


##### SalishSeaCast

* `collect_weather 12` didn't finish until ~11:00


##### Miscellaneous

* MOAD group mtg; welcome to Zingo


##### SSS150

* Checked rivers that Michael downloads gauge obs for; Capilano and Seymour are
  on wateroffice:
  * we already collect a Capilano gauge
  * we can add Seymour to the SSC config for `collect_river_data` to handle
  * Gallant, Mosquito, and Lynn creeks are not on wateroffice
  * what about other rivers; e.g. Pitt?
* Slack mtg w/ Camryn to discuss how we get started on sss150



#### Wed 26-Jun-2024


##### SalishSeaCast

* `collect_weather 12` was late again; downloads started at ~09:00
  * `crop_gribs 12` timed out at 11:08, causing `grib_to_netcdf` to run and fail
  * `collect_weather 12` finished at ~11:38
  * ran `crop_gribs 12 --backfill` to restart automation


##### SSS150

* copied and renamed coordinates and bathymetry from Michael's `/ocean/` to `grid` repo


##### Miscellaneous

* updated PyCharm on `khawla` to 2024.1.4
* started work on changing flox INFO log messages to DEBUG level
  * created fork on GitHub and cloned it to `/media/doug/warehouse/python/`
  * created Python 3.12 env from `ci/environment.yml`
  * did editable install of flox
  * ran `pytest`: 16037 tests! 4004 skips


##### SalishSeaNowcast

* corrected log message at completion of `crop_gribs --backfill`
* branch: improve-crop_gribs-backfill-log-msg
* PR#279 - squash-merged
* previous msg was probably mindlessly copy-pasted from the single variable-hour
  file option code path
* pulled into production clone on `skookum`


##### 2x resolution SalishSeaCast

* continued work on double resolution coordinates
  * added calculation of `e[1|2][tuvf]` arrays for double resolution coordinates from
    `g[lam|phi][tuvf]` arrays



#### Thu 27-Jun-2024


##### SalishSeaCast

* `collect_weather 12` was back to regular schedule; finishing at ~09:05


##### SalishSeaNowcast

* in light of 11jun failure to reproduce the broken coords when writing with h5netcdf issue I see in
  Reshapr, decided to try using h5netcdf for write in `make_ww3_*current*_file` workers; hacked code
  on `arbutus`
  * wwatch3 doesn't like h5netcdf generated files; reverted hacks and re-run prep workers manually


##### Miscellaneous

* researched HDF5 shuffle filter for netCDF4 files
  * applicable when `zlib=True`
  * learned that `zlib=True` is deprecated in favour of `compression="gzip"`
  * for `xarray.Dataset.to_netcdf(..., engine="h5netcdf")` the encoding dict must explicitly include
    `"shuffle": True` for each compressed coord & variable


##### 2x resolution SalishSeaCast

* continued work on double resolution coordinates
  * visualized padded ends of e arrays; padding looks correct, but other values are less uniform than
    I expect
  * changed compression encoding from `"zlib": True` to `"compression": "gzip"`
  * added `"shuffle": True` to encoding because it is not automatic for compressed h5netcdf writes
    as it is for netcdf4 writes



#### Fri 28-Jun-2024


##### SalishSeaCast

* nowcast-agrif run failed 16min in; apparent node issue
  * I didn't notice until Saturday at ~11:20


##### SalishSeaNowcast

* added comments to `make_ww3_*current*_file` workers re: need to write files with netcdf4 because
  wwatch3 wind & currents pre-processors choke on h5netcdf generated files


##### Miscellaneous

* helped Vicente with ssh setup on his new Windows 11 laptop
* helped Tall with failing VSCode connection to `salish  and waterhole workstations; increased
  ssh connection time-out
* setup OPenSSH client and server on Zwift PC so I can edit workouts from khawla via VSCode
  remote ssh extension:
  * https://learn.microsoft.com/en-us/windows-server/administration/openssh/openssh_install_firstuse?tabs=powershell
  * https://learn.microsoft.com/en-us/windows-server/administration/openssh/openssh_keymanagement
  * my public key had to go in `c:\ProgramData\ssh\administrators_authorized_keys` because I am an
    admin on the PC; putting it in `$env:USERPROFILE\.ssh\authorized_keys` just resulted in auth failures
    and password prompts
  * `$env:USERPROFILE` is a generic way to spell `c:\USERS\djl\`


##### SSS150

* worked on getting NEMO running again on `salish`
  * repo updates and git clones in `/data/dlatorne/MEOPAR/`
    * lots of hg clones and missing repos


##### SalishSeaCast Docs

* updated `salish` quick-start docs
  * added cloning and installation of NEMO-Cmd and SalishSeaCmd



#### Sat 29-Jun-2024


##### SalishSeaCast

* backfill nowcast-agrif:

  ```bash
  make_forcing_links orcinus nowcast-agrif 2024-06-28
  make_forcing_links orcinus nowcast-agrif 2024-06-29
  ```



#### Sun 30-Jun-2024


Goofed off and cycled IRL.



## July

### Week 27

#### Mon 1-Jul-2024

**Statutory Holiday** - Canada Day


##### SalishSeaCast

* `crop_gribs 00` timed out at 23:09 by `collect_weather 00 2.5km` didn't finish until 00:16
  * ran `crop_gribs 00 --backfill --debug` at ~07:30 Tue to recover without starting 06 weather
    processes that already ran



#### Tue 2-Jul-2024


##### Miscellaneous

* MOAD group mtg; see whiteboard.
* discussed Vicente's VSCode Git ssh agent problems with he, Ilias and Cassidy;
  latter two confirmed that they have no issues either in GUI or terminal
* speculated on Jose's loss of uncommitted work in notebooks on `salish`;
  suggested confirming file saves, and using WIP commits to commit and push more
  often
* updated `kudu` PyCharm to 2024.1.4
* aborted work on changing flox INFO log messages to DEBUG level
  * discovered when I pushed my commits to GitHub that dcherian had already
    fixed the issue in unrelated PR#348



#### Wed 3-Jul-2024


##### Miscellaneous

* Slack conversation with Becca about using server-side resampling in the ONC data API
* checked one of Tall's files that Susan can't access; works for me


##### 2x resolution SalishSeaCast

* finished work on double resolution coordinates
  * Susan reviewed padded ends of e arrays
    * she thinks lumpiness of other values is due to y-axis range of plots
    * re-scaled y-axis, and things look better; Susan approved


##### sss150

* continued work on getting NEMO running again on `salish`
  * built XIOS-2 on `salish`
  * built NEMO SalishSeaCast_Blue config on `salish`
  * built REBUILD_NEMO on `salish`


##### MOAD Docs

* updated `salish` XIOS-2 build section
  * `/data/$USER/MEOPAR/` paths


##### SalishSeaCast Docs

* updated `salish` quick-start docs
  * dropped reference to NEMO v3.4



#### Thu 4-Jul-2024


##### 2x resolution SalishSeaCast

* added `coordinates_SalishSeaCast_202405.nc` to grid repo
* can't add `coordinates_SalishSeaCast_double_202405.nc` to grid repo because it is too large to
  push to GitHub


##### sss150

* succeeded in getting NEMO running again on `salish`
  * `SS-run-sets/sss150/djl/`
  * SalishSeaCast/03jul24 run started at 15:11; expect ~15h20m run time, so finish at ~06:40 tomorrow



#### Fri 5-Jul-2024


##### sss150

* continued NEMO test runs on `salish`
  * `SS-run-sets/sss150/djl/`
  * SalishSeaCast/03jul24 in results/ssc_baseline/ stalled at ~03:10 when Neah Bay ssh file got
    overwritten by automation; no time steps in results files 😱
  * re-tried SalishSeaCast/03jul24 in results/ssc_baseline/ with 6h run duration
    * started at 10:55, finished at 15:33; 4h39m11s run time
  * switched to `add_sshbdy` branch
    * re-built SalishSeaCast config
    * ran SalishSeaCast/03jul24 in results/ssc_add_sshbdy/ with 6h run duration; 3h7m31s run time


##### Miscellaneous

* Slack w/ Becca re: collecting ONC datasets; discussed ERDDAP vs. ONC API


##### SalishSeaCmd

* fixed longstanding issue #1 re: duplicated effort in vcs revision recording fro NEMO and XIOS-2
  clones:
  * branch: issue11-vcs-rec-no-dups
  * PR#69 - squash-merged



#### Sat 6-Jul-2024

Cycled to Colony Farm and back


##### Miscellaneous

Squash-merged dependabot PRs to update certifi to 2024.7.4 re: CVE-2024-39689 re: removal of root
certificates from GLOBALTRUST:

* moad_tools
* cookiecutter-MOAD-pypkg
* AtlantisCmd
* MOAD/docs
* NEMO_Nowcast
* cookiecutter-analysis-repo
* SalishSeaCast/docs
* Reshapr
* SalishSeaCmd
* salishsea-site
* NEMO-Cmd
* SalishSeaNowcast
* MoaceanParcels
* tools/SalishSeaTools
* SOG-Bloomcast
* cookiecutter-djl-pypkg
* SOG-Bloomcast-Ensemble
* erddap-datasets



#### Sun 7-Jul-2024


##### sss150

* continued work on visual comparison of baseline and add_sshbdy branch runs:
  * `notebooks/sss150/add_sshbdyPR-check.ipynb`
  * surface salinity fields are identical



### Week 28

#### Mon 8-Jul-2024


##### sss150

* finished work on visual comparison of baseline and add_sshbdy branch runs:
  * `notebooks/sss150/add_sshbdyPR-check.ipynb`
  * improved narrative and pushed


##### NEMO-3.6-code

* merged NEMO-3.6-code PR#6


##### Miscellaneous

* phys ocgy seminar; Birgit, British Antarctic Survey, Human Activities & Ocean-driven melt of
  west Antarctic ice sheet



#### Tue 9-Jul-2024


##### Miscellaneous

* MOAD group mtg; see whiteboard

* Squash-merged dependabot PRs to update zipp to 3.19.1 re: CVE-2024-5569 re: DoS vulnerability:

  * SalishSeaNowcast
  * NEMO_Nowcast
  * AtlantisCmd
  * Reshapr
  * NEMO-Cmd
  * SalishSeaCmd
  * moad_tools
  * SalishSeaCast/docs
  * salishsea-site


##### NEMO-3.6-code

* found that `SalishSeaCast_Blue/MY_SRC/` is symlinked to `SalishSeaCast/MY_SRC/`,
  so PR#6 is automatically included in the former


##### sss150

* set up and ran `/data/dlatorne/MEOPAR/SS-run-sets/sss150/djl/SalishSeaCast_Blue.yaml`
  * 1h13m42s run time
  * verified by hacking salinity field into `add_sshbdy` comparison notebook
    * saw expected minor difference to nowcast-green run field


##### SalishSeaCast/docs

* updated running on salish section



#### Wed 10-Jul-2024


##### sss150

* refined TODOs in Slack canvas


##### Miscellaneous

* read near-final draft of Susan's exchange flux paper



#### Thu 11-Jul-2024


##### sss150

* email to Michael to confirm cpp keys; his reply:

  > The keys are largely the same, but we’ve added Smagorinsky, which also required switching the
  > c3d ldf keys:
  >
  > bld::tool::fppkeys key_bdy key_tide key_dynspg_ts key_vvl key_mpp_mpi key_iomput key_nosignedzero
  > key_zdfgls key_ldfslp key_xios2 key_traldf_c3d key_traldf_smag key_dynldf_c3d key_dynldf_smag
  >
  > key_netcdf4 is removed too, because this does nothing when using xios for output saving.

* NEMO orientation session with Camryn
* created initial sss150 config with Camryn and got a successful build


##### SalishSeaCast

* email from Michael re: end of 2nd Narrows Bridge HADCP obs collection in Mar-2023
  * instrument is still in operation
  * obs emails have piled up on `salish`


##### Miscellaneous

* set up Fortran language server (`fortls` package) for VSCode on `salish`
  * `mamba create -n fortls fortls`
  * `mamba env list`  to confirm env path: `/home/dlatorne/conda_envs/fortls`
  * set `Fortran > Fortls: Path` in `Remote [SSH: salish]` settings to `$HOME/conda_envs/fortls`


##### MOAD/docs

* added sub-section to VS Code re: Fortran language server


##### NEMO-3.6-code

* added `*.mod` to `.gitignore` so that people don't commit the `.mod` files that the VSCode Fortran
  language server generates with its compilation while editing



#### Fri 12-Jul-2024


##### sss150

* added Michael's `namelist_ref` to `sss150/EXP00/`
* pushed sss150 config to GitHub


##### NEMO-3.6-code

* dropped `key_netcdf4` from SalishSeaCast_Blue config based on Michael's assertion that it serves
  no purpose when XIOS-2 is being used
  * test run in `/data/dlatorne/MEOPAR/results/sss150/03jul24-blue-no-key_netcdf4/`;
    identical results
* can we drop `namnc4` from `namelist.compute`?


##### SalishSeaCmd

* duplicate vcs revision recording fix doesn't seem to be working on `salish`


##### SalishSeaCast

* investigated Michael's report of VFPA HADCP dataset no longer updating:
  * stopped on 21mar23 because I inadvertently removed `get_vfpa_hadcp` worker from automation
  * csv files from email messages are available to 01jul23, then stop being extracted; Michael is
    investigating
  * backfilled to 30jun23 in bash loops
  * Michael discovered that the datetime format in the observation .csv files was changed between
    17:00 and 18:00 UTC on 2023-07-02 from `dd/mm/YYYY HH:MM` to `YYYY-mm-dd HH:MM`
    * he fixed and backfilled the cron job script
    * I updated `get_vfpa_hadcp`
    * branch: chg-get_vfpa_hadcp-csv-time-format
    * PR#282 -squash-merged
  * backfilled to 31oct23 in bash loops



#### Sat 13-Jul-2024


##### SalishSeaCast

* continued backfilling VFPA HADCP to 12jul24 in bash loops


##### SalishSeaNowcast

* added `get_vfpa_hadcp` after 06 weather collection
  * branch: get_vfpa_hadcp-after-06-weather
  * PR#283
  * switched to branch in production to test
  * restarted manager to load updated `next_workers` module
  * worked on code and tests maintenance task for worker



#### Sun 14-Jul-2024


##### SalishSeaCast

* `get_vfpa_hadcp` worked as expected in automation
* checked retention on `liveocean.apl.uw.edu` of LiveOcean extraction we use for boundary conditions
  * spot checks of directories back to 01jun24 show `ubc.nc` file is present



### Week 29

#### Mon 15-Jul-2024


##### NEMO-3.6-code

* dropped `namnc4` from `namelist.compute` when `key_netcdf4` is not being used
  * test run in `/data/dlatorne/MEOPAR/results/sss150/03jul24-blue-no-namnc4/`;
    identical results


##### Miscellaneous

* phys ocgy seminar
* helped Karyn with update of Suchy, et al repo on GitHub for final submission
  * **it is important to start the process on zenodo by confirming that the repo is selected for**
    **archiving, then create the GitHub release, otherwise zenodo only does part of the work it should**


##### sss150

* Slack w/ Camryn:
  * her namelist_cfg dissection
  * my rivers processing findings



#### Tue 16-Jul-2024


##### sss150

* finished canvas notes re: need to a worker to process river discharges and water levels to netCDF
  files that Michael's `runofftools` package can ingest
* added canvas notes re: no tides in sss150 config; drop namelists, key_tide, tides item in YAMLs


##### Miscellaneous

* MOAD group mtg; see whiteboard

* Squash-merged dependabot PRs to update setuptools to 70.0.0 re: CVE-2024-6345 re: code injection
  vulnerability:

  * MOAD/docs
  * moad_tools
  * salishsea-site
  * NEMO-Cmd
  * SalishSeaCast/Docs
  * SalishSeaCmd
  * SOG-Bloomcast
  * SOG-forcing
  * AtlantisCmd
  * NEMO_Nowcast
  * gha_workflows
  * cookiecutter-analysis-repo
  * cookiecutter-MOAD-pypkg
  * SalishSeaNowcast


##### NEMO-3.6-code

* dropped `key_netcdf4` from SalishSeaCast and SalishSeaCast_Blue configs


##### SS-run-sets

* dropped `nam_nc4` namelist from `v20211/namelist.compute` to correspond to dropping `key_netcdf4`


##### SalishSeaNowcast

* added `get_vfpa_hadcp` after 06 weather collection
  * branch: get_vfpa_hadcp-after-06-weather
  * PR#283 - squash-merged
  * finished tests maintenance task for worker
* added sss150 river to sarracenia configs
  * branch: sss150-rivers
  * PR#285 - squash-merged
  * deployed branch to skookum for production testing



#### Wed 17-Jul-2024

Home to YYZ w/ Susan



#### Thu 18-Jul-2024

YYZ to Barrie w/ Susan

Triaged storage locker w/ Susan & Jamie



#### Fri 19-Jul-2024

Barrie to Meaford to Barrie w/ Susan & Jamie

Interment service for Mom & Dad



#### Sat 20-Jul-2024

Boxes to VV
Locker clearing and sorting w/ Susan & Jamie
Dropped off prints for de-framing



#### Sun 21-Jul-2024


##### SalishSeaCast

* forecast2/20jul24 failed with large zonal velocity on west boundary
  * probably not a problem for 21jul24 runs because it came from the a forecast restart file


Locker clearing, then walking on Ardagh Bluff trails w/ Susan



### Week 30

#### Mon 22-Jul-2024

Furniture picked up from locker by Habitat for Humanity.
Got fireproof box opened.
Started SDB opening process.



#### Tue 23-Jul-2024

Recycling centre trip.
Bibles & prayer books to Trinity.
Picked up prints


##### Miscellaneous

* Squash-merged dependabot PRs to update sentry-sdk to 2.8.0 re: CVE-2024-40647 re: envvars exposure
  vulnerability:

  * salishsea-site
  * SalishSeaNowcast
  * NEMO_Nowcast


##### SalishSeaNowcast

* finished fixing worker docstrings re: issue #121 - closed; PR#x287 - squash-merged
* started modernizing test_live_ocean_files
  * branch: modernize-test_live_ocean_files
  * PR#288


Dinner w/ Linda & Steven



#### Wed 24-Jul-2024

Junk removed from locker.
Locker vacated.
Documents to UPS store for shredding.
Nostalgia tour in east end
Got contents of SDB



#### Thu 25-Jul-2024

Last boxes to VV

Barrie to home w/ Susan



#### Fri 26-Jul-2024

Susan went to White Rock to relieve Jingli


##### salishsea-site

* updated env to `sentry-sdk=2.9.0` and restarted app re: dependabot PR earlier in the week


##### SalishSeaCast

* updated env to `sentry-sdk=2.9.0` re: dependabot PR earlier in the week
* waited for end of daily runs post-processing
* restarted manager


##### SalishSeaNowcast

* finished modernizing test_live_ocean_files
  * branch: modernize-test_live_ocean_files
  * PR#288 - squash-merged



#### Sat 27-Jul-2024

Rode 8th Ave, Marine Dr, Salish trail loop.



#### Sun 28-Jul-2024

Washed Susan's Cannondale



### Week 31

#### Mon 29-Jul-2024


##### SalishSeaCast

* setup ConnectBot on my phone to monitor/manage automation while traveling


##### sss150

* SSS-run-sets:
  * changed `namelist.atmos_rivers` to use CORE bulk atmospheric Forcing
  * dropped `rpn` namelists and `ln_blk_rpn` variable from `namsbc`
  * dropped `namtide` and 2 `nam_bdy_tide` namelists from `namelist.lateral`
* NEMO-3.6-code:
  * dropped key_tide from `sss150` config on `salish` and did a clean build



#### Tue 30-Jul-2024


##### Miscellaneous

* reviewed release notes for xarray 2024.07.00
  * initial changes in `Groupby` API that should eventually facilitate spatial resampling
* MOAD group mtg; see whiteboard


##### 2x resolution SalishSeaCast

* started loading and re-gridding bathymetry survey products that Michael used
  * copied them from `ocean:/home/mdunphy/...` to `khawla`
  * stalled out on traceback from `pyproj` re: utm zone id


##### SalishSeaCast

* `get_onc_ctd SCVIP` failed due to "no port to publish log messages on"
  * also happened on 24jlu24
  * log shows that all worker logging port on skookum are indeed being used during early morning
    obs collecting
* hindcast downloads from `optimum` started failing at ~22:00


##### SalishSeaNowcast

* added 5 worker logging ports to list in config
* branch: add-logging-ports
* PR#289 - squash-merged
* deployed to production and restarted message_broker, log_aggregator, and manager



#### Wed 31-Jul-2024


##### Miscellaneous

* `ocean` was down due to UBC IT network maintenance in UDC
  * Henryk got it back online at ~11:20


##### 2x resolution SalishSeaCast

* continued loading and re-gridding bathymetry survey products that Michael used
  * email help from Michael resolved traceback from `pyproj` re: utm zone id
    * it has to be integer `10` instead of sting `10U` since `proj=8.0`
    * turns out that the CHS bathy product that was raising that error isn't used anyway 😏
  * created 202405 base bathymetry array
    * set shoreline depth of 4m at the 2m isobath and max depth of 428m


##### SalishSeaCast

* `skookum` and `salish` had to be rebooted at ~15:30 due to `ocean` issue
  * `salish` did not recovery well due to disk problem
  * Henryk booted `salish` from LiveCD for troubleshooting
  * Henryk mounted `/SalishSeaCast` so that I could get automation partially working
  * recovery:
    * `skookum`
    * start website app
    * start automation
      * `collect_weather 00`
      * `crop_gribs 00`



## August

<!-- markdownlint-disable MD001 -->
#### Thu 1-Aug-2024
<!-- markdownlint-enable MD001 -->


##### SalishSeaCast

* Henryk mounted `/results2`, `/data`, and `/opp` on skookum
  * that made them available on all? other waterhole hosts
* started ERDDAP:
  <!-- markdownlint-disable MD013 -->
  ```bash
  sudo sysctl fs.inotify.max_user_instances=2048
  sudo sysctl fs.inotify.max_user_watches=196608
  sudo sysctl -p
  sudo /opt/tomcat/bin/startup.sh  # ERDDAP
  ```
  <!-- markdownlint-enable MD013 -->
* analyze overnight failures:
  * `make_plots nemo forecast publish` failed due to no `/ocean`
  * `archive_tarball nowcast-green 2024-jul` failed due to no `/ocean`
  * `get_vfpa_hadcp` failed due to no `/opp` mount
  * `collect_river_data ECCC Englishman` failed due to no `/data` mount
  * `collect_river_data ECCC Fraser` failed due to no `/data` mount
  * `make_runoff_file` failed due to no `/data` mount
  * `make_v202111_runoff_file` failed due to no `/data` mount
  * forecast2 ran with persisted runoff
  * `make_plots nemo forecast2 publish` failed; unclear why
  * `make_turbidity_file` failed due to insufficient obs
  * `make_runoff_file` failed due to no `/data` mount
  * `make_v202111_runoff_file` failed due to no `/data` mount
  * nowcast-blue ran with persisted runoff
  * forecast ran with persisted runoff
  * `make_plots nemo nowcast comparison` failed due to ERDDAP not running for Sand Heads winds
  * nowcast-green ran with persisted runoff and turbidity
  * nowcast-agrif ran with persisted runoff and turbidity
  * `make_averaged_dataset day physics|chemistry|biology` failed due to no `salish` dask cluster
* backfill:
  * `get_vfpa_hadcp 2024-07-31`
  * `collect_river_data ECCC Englishman 2024-07-31`
  * `collect_river_data ECCC Fraser 2024-07-31`
  * delete runoff file symlinks
  * `make_runoff_file 2024-08-01`
  * `make_v202111_runoff_file 2024-07-31`
  * after call w/ Henryk:
    * `archive_tarball nowcast-green 2024-jul`



#### Fri 2-Aug-2024


##### 2x resolution SalishSeaCast

* refined bathymetry visualization function
* started work on closing First Narrows



#### Sat 3-Aug-2024

Prep for VanIsle tour



#### Sun 4-Aug-2024

VanIsle tour day 1:

* Home to Horseshoe Bay
* Departure Bay to Port Alberni



### Week 31

#### Mon 5-Aug-2024

VanIsle tour day 2:

* Port Alberni to Bamfield



#### Tue 6-Aug-2024

VanIsle tour day 3:

* Bamfield walk to Brady Beach



#### Wed 7-Aug-2024

VanIsle tour day 4:

* Bamfield Marine Centre & walk to East dock



#### Thu 8-Aug-2024

VanIsle tour day 5:

* Bamfield to Lake Cowichan



#### Fri 9-Aug-2024

VanIsle tour day 6:

* Lake Cowichan to Port Renfrew



#### Sat 10-Aug-2024

VanIsle tour day 7:

* Port Renfrew walk to Botanical Beach



#### Sun 11-Aug-2024

VanIsle tour day 8:

* Port Renfrew to Sooke



### Week 33

#### Mon 12-Aug-2024

VanIsle tour day 9:

* Sooke to Debby & Paul's



#### Tue 13-Aug-2024

VanIsle tour day 10:

* Debby & Paul's to Swartz Bay
* Tsawassen to home
* total tour distance: 610.81 km



#### Wed 14-Aug-2024

##### SalishSeaCast

* `download_live_ocean` timed out at 12:03
  * re-ran for another try at 12:07
  * emails from Parker saying that problem is due to HPC failure; file may be available by 15:00
  * worker succeeded at 15:07, and automation took things from there
* backfilled 6aug24 LiveOcean download & boundary conditions file
  <!-- markdownlint-disable MD013 -->
  ```bash
  rm /results/forcing/LiveOcean/downloaded/20240806/low_passed_UBC.nc
  download_live_ocean 2024-08-06 --debug
  make_live_ocean_files 2024-08-06 --debug
  ```
  <!-- markdownlint-enable MD013 -->
* realized that `fraser_buoy.cron.sh` has not been running since `salish` went down
  * asked Henryk to send me `crontab -l` from `salish`
  * added `35 *   *   *   *    /results/observations/ECCC/fraser_buoy.cron.sh` to my `skookum` crontab
  * tried unsuccessfully to find information about web data service for Fraser buoy obs


##### salishsea-site

* Squash-merged dependabot to update webob to 1.8.8 re: CVE-2024-42353 re: domain redirect
  vulnerability
* built new `salishsea-site-env` on `skookum`



#### Thu 15-Aug-2024


##### Miscellaneous

Checked status of scheduled GHA workflows:
  <!-- markdownlint-disable MD013 -->
  ```bash
  conda activate gha-workflows
  python /media/doug/warehouse/MOAD/gha-workflows/gha_workflow_checker/gha_workflows_checker.py
  ```
  <!-- markdownlint-enable MD013 -->

Read about coming readthedocs addon changes; enabled addons and analytics on all non-archived projects.
Confirmed that blogofile project has been archived on GitHub, so I no longer need to worry about it.


##### sss150

* SSS-run-sets:
  * created `sss150_example.yaml` as 1st draft of run description to help figure out forcing files


Paul, Debby & Mina arrived for provincial swim meet



#### Fri 16-Aug-2024


##### Miscellaneous

Updated `khawla` to PyCharm 2024.2


##### SalishSeaCast

* investigated `TypeError string indices must be integers, not 'str'` from
  `make_plots nemo forecast[2] publish`
  * twice per run since forecast2/08aug24 run
  * in `salishsea_tools.data_tools` request to `api-iwls.dfo-mpo.gc.ca`
  * happens for Squamish and Halfmoon Bay stations
  * real-time water levels for those stations appears to have been removed
  * Darrel Bay station near Squamish hs real-time obs


##### SalishSeaCmd

* Discussed namelist editing driven by stanzas in YAML file w/ Susan
  * it is not beneficial for her workflow, and she likes the context-visibility of editing namelist
    segment files


##### 2x resolution SalishSeaCast

* finished closing First Narrows
* closed Pitt River
* closed Fraser River just downstream of Barnston Island
* added Fraser River proxy extension to the south



#### Sat 17-Aug-2024

Goofed off.



#### Sun 18-Aug-2024

Goofed off.



### Week 34

#### Mon 19-Aug-2024

##### SalishSeaCast

* `download_live_ocean` delayed to 11:30


##### Miscellaneous

* discovered just how many of my EOAS web logins fail:
  * success:
    * helpdesk
    * mail
  * fail:
    * www
    * nextcloud
    * bookings
    * gitlab
* completed annual COI declaration on Workday; no COI for me because only
  supervisors are required to declare relationships, and I have no active or
  expected professional software development work outside EOAS


##### sss150

* started reading code in Michael & Maxim's bdytools project:
  * TODO:
    * generate a 201802 mesh mask with the Fraser extension filled as Michael
      did in `/ocean/mdunphy/sss150_20220715/sal500/mesh_mask201702us_No_FR_Ext.nc`
    * generate an `opts.yaml` file based on `FA12/bdytools/config/ssc_to_sss150_salish.yaml`
    * run `bdytools opts.yaml --weights` to create weights file for SSC to sss150 interpolation
* meeting w/ Susan & Camryn to review draft YAML run description and progress
  * reviewed YAML file
  * reviewed and edited namelist files
  * decided on target 01jan23 as start date for runs
  * see whiteboard photos & mtg notes in #sss150 channel



#### Tue 20-Aug-2024


##### Miscellaneous

* AAPS networking decolonization tour of artworks on campus
* met w/ Henryk re: restoring `salish` to full operation
  * plan to rebuild `salish` from scratch on Wed 28-Aug
    * boot 22.04 from LiveCD to confirm that storage controllers are supported
    * initially install 18.04 due to config that can be done there but not in later version
      * expected to take 3-5 hours; storage mounts will work afterwards
    * update to 20.04, then 22.04
      * probably on Thu 29-Aug; reboots required


##### sss150

* continued namelist commits
* started diff-ing namelist_ref files between SSC & sss150



#### Wed 21-Aug-2024

In VGH



#### Thu 22-Aug-2024

In VGH



#### Fri 23-Aug-2024

In VGH



#### Sat 24-Aug-2024

Released from VGH



#### Sun 25-Aug-2024

Recovery at home



### Week 35

#### Mon 26-Aug-2024

Recovery at home



#### Tue 27-Aug-2024

Recovery at home



#### Wed 28-Aug-2024

Recovery at home


##### SalishSeaCast

* stage 1 of `salish` rebuild and OS upgrade
  * shut down ERDDAP, website & automation at ~13:30
    <!-- markdownlint-disable MD013 -->
    ```bash
    sudo /opt/tomcat/bin/shutdown.sh

    mamba activate /SalishSeaCast/salishsea-site-env
    supervisorctl -c /SalishSeaCast/salishsea-site/supervisord-prod.ini stop salishsea-site
    supervisorctl -c /SalishSeaCast/salishsea-site/supervisord-prod.ini shutdown
    mamba deactivate

    mamba activate /SalishSeaCast/nowcast-env
    pkill -f nowcast.workers
    supervisorctl -c /SalishSeaCast/SalishSeaNowcast/config/supervisord.ini stop sr_subscribe-hydrometric
    supervisorctl -c /SalishSeaCast/SalishSeaNowcast/config/supervisord.ini stop sr_subscribe-hrdps-continental
    supervisorctl -c /SalishSeaCast/SalishSeaNowcast/config/supervisord.ini stop manager
    supervisorctl -c /SalishSeaCast/SalishSeaNowcast/config/supervisord.ini stop log_aggregator
    supervisorctl -c /SalishSeaCast/SalishSeaNowcast/config/supervisord.ini stop message_broker
    supervisorctl -c /SalishSeaCast/SalishSeaNowcast/config/supervisord.ini shutdown
    mamba deactivate
    ```
    <!-- markdownlint-enable MD013 -->

  * restarted ERDDAP, website & automation at ~19:30
    <!-- markdownlint-disable MD013 -->
    ```bash
    sudo /opt/tomcat/bin/startup.sh

    mamba activate /SalishSeaCast/salishsea-site-env
    supervisord -c /SalishSeaCast/salishsea-site/supervisord-prod.ini
    mamba deactivate

    mamba activate /SalishSeaCast/nowcast-env
    supervisord -c /SalishSeaCast/SalishSeaNowcast/config/supervisord.ini
    collect_weather 00 2.5km
    crop_gribs 00 2024-08-29
    download_weather 00 1km  # failed due to no files
    download_weather 12 1km
    download_weather 18 2.5km
    crop_gribs 18 --backfill
    mamba deactivate
    ```
    <!-- markdownlint-enable MD013 -->



#### Thu 29-Aug-2024

Recovery at home


##### SalishSeaCast

* reviewed `manager-stderr` log and created issues for warnings:
  * FutureWarning re: `pandas.read_csv(..., date_parser=...)` in `salishsea_tools.stormtools`;
    similar to SalishSeaNowcast #290
  * DeprecationWarning re: `xarray.Dataset.drop()` in `make_CHS_currents_file` worker
* `download_live_ocean` timed out at ~12:45; re-ran manually and it timed out again at 15:47
  * persisted 28aug download via symlink
  * ran `make_live_ocean_files` to jump start automation at ~16:40
* Zoom w/ Henryk re: `salish`:
  * `salish` is running 20.04 but root drive is not RAIDed
  * NFS mounts show some warnings; he wants to monitor operation for a few days
  * there are a flood of warnings when he tries to run under 22.04
  * logins remain disabled


##### Miscellaneous

* Squash-merged dependabot PRs to update jupyterlab to 4.2.5 re: CVE-2024-43805 re: HTML injection
  via Markdown vulnerability:
  * SalishSeaTools
  * MoaceanParcels
  * erddap-datasets
  * SOG-ensemble-bloomcast



#### Fri 30-Aug-2024

Recovery at home


##### SalishSeaCast

* aug29 LiveOcean file appeared at 16:06 yesterday
  * replaced symlinked 28aug file with it for future hindcasts
* more review of `manager-stderr` log and created issues for warnings:
  * FutureWarnings
    in `moad_tools.observations.get_ndbc_buoy()`
    * re: nested sequences for 'parse_dates' in `pd.read_csv()`
    * re: `delim_whitespace` keyword in `pd.read_csv` is deprecated
    * re: `pandas.read_csv(..., date_parser=...)`


##### Miscellaneous

* read docs of hypothesis property-based testing package that seems popular in the pangeo community
* watched Youtube of SharcNet seminar on WASM for scientific computing
  * rust is best
  * Pyodide is compiler for Python
  * JupyterLite is WASM implementation of Jupyter
  * deployable on GitHub pages
  * examples use emscriptem because of many library ports
* updated khawla to PyCharm 2024.2.1


##### SalishSeaNowcast

* fixed issue #253 re: UserWarning in `surface_current_tiles` figure module
  * branch: issue253-surface_current_tiles
  * PR#292 - squash-merged
  * was delighted to find figure test notebook
  * created new nowcast-fig-dev env



#### Sat 31-Aug-2024

Recovery at home


## September

<!-- markdownlint-disable MD001 -->
#### Sun 1-Sep-2024
<!-- markdownlint-enable MD001 -->

Recovery at home


##### SalishSeaCast

* `upload_forcing orcinus nowcast+` failed on key exchange
  * `orcinus` is non-responsive


##### SalishSeaNowcast

* fixed issue #290 re: FutureWarning in `collect_river_date` worker re: date parsing in
  `pandas.read_csv()`
  * branch: issue290-read_csv
  * PR#292 - squash-merged
  * simple change from `date_parser=...` to `date_format="ISO8601"`


##### SalishSeaTools

* started to investigate issue #104 re: FutureWarning in `stormtools.load_tidal_predictions()`
  re: date parsing in `pandas.read_csv()`



### Week 36

#### Mon 2-Sep-2024

**Statutory Holiday** - Labour Day

Recovery at home


##### SalishSeaNowcast

* started work on issue #291 re: DeprecationWarning in `make_CHS_currents` worker re: replacing
  deprecated `xarray.Dataset.drop()` with `.drop_vars()`
  * branch: issue29`-make_CHS_currents-drop_vars
  * PR#294 - squash-merged
  * modernized tests:
    * issue#81 - NowcastWorker mock to fixture
    * issue#82 - logging mocks to caplog
    * replace unittest.mock.patch with pytest monkeypatch
  * corrected unlimited dimension in the netCDF file
  * fixed typos and improved several docstrings


##### SalishSeaCast

* backfilled `nowcast-agrif` runs:
  <!-- markdownlint-disable MD013 -->
  ```bash
  # wait for run to fail
  upload_forcing orcinus nowcast+ 2024-09-01
  upload_forcing orcinus turbidity 2024-09-01
  # wait for run to finish
  make_forcing_links nowcast-agrif 2024-09-02
  ```
  <!-- markdownlint-enable MD013 -->



#### Tue 3-Sep-2024

Recovery at home.
GP appt.


##### Miscellaneous

MOAD group mtg; see whiteboard.


##### SalishSeaNowcast

* set up pre-commit.ci for repo with default config to auto-fix PRs and generate PRs to auto-update
  pre-commit config weekly on Mondays at ~16:00 UTC


##### sss150

* sent email to Michael asking for:
  * `rn_rdt` value for `&namdom` in `namelist.domain`
  * copies of `domain_def.xml` and `iodef.xml` files that they use
  * restart file from around 1-Jan-2023


##### SalishSeaCast

* sent email to chsinfo@dfo-mpo.gc.ca asking about end of water level observations data streams from
  Halfmoon Bay and Squamish stations on IWLS API service



#### Wed 4-Sep-2024

Recovery at home.
Dentists appt.


##### SalishSeaCast

* email reply from chsinfo@dfo-mpo.gc.ca asking says that there was a technical problem with the
  IWLS API service for the water level observations data streams from
  Halfmoon Bay and Squamish stations, but that it was resolved; contact them if it is persisting for
  me
  * still a problem for this morning's forecast2 figures


##### Miscellaneous

* Squash-merged dependabot PRs to update cryptography to 43.0.1 re: GHSA-h4gh-qq45-vh27
  re: vulnerability in statically linked OpenSSL:
  * cookiecutter-analysis-repo
  * NEMO_Nowcast
  * moad_tools
  * cookiecutter-MOAD-pkg
  * SalishSeaNowcast
  * salishsea-site
  * SalishSeaCmd
  * NEMO-Cmd
  * Reshapr
* pre-commit.ci ran on SalishSeaNowcast PR and black found a comma to add to the end of an arg list
  in one of the test modules; the commit was added to the PR and contained a link to all the details
  on the pre-commit.ci site
* Squash-merged dependabot PRs to update fiona to 1.10.0 (finally) re: CVE-2020-14152 and
  CVE-2024-25853 re: vulnerabilities in madler-zip dependency:
  * moad_tools
* set up pre-commit.ci with default config to auto-fix PRs and generate PRs to auto-update
  pre-commit config weekly on Mondays at ~16:00 UTC
  * erddap-datasets
  * NEMO-Cmd
  * salishsea-site
  * SalishSeaCmd
  * SOG-Bloomcast-Ensemble
  * NEMO_Nowcast
  * cookiecutter-analysis-repo
  * cookiecutter-MOAD.pypkg
  * gha-workflows
  * MoaceanParcels
  * moad_tools
  * Reshapr


##### sss150

* continued namelist commits from 19aug mtg



#### Thu 5-Sep-2024

Recovery at home.



#### Fri 6-Sep-2024

Recovery at home.


##### NEMO-Cmd

Updated codecov badge URL to add token re: sphinx-linkcheck failures


##### sss150

* continued namelist commits from 19aug mtg

* TODO:
  * symlink `no_snow.nc` and `no_ice.nc` into `grid/sss150/`
  * rename `rivers/sss150/R_SSS150_Dailies*`  to `rivers/sss150/R_sss150_Dailies*`
    * fix Susan's notebook
  * rename `rivers-climatology/rivers_daily_SS150.nc` to `rivers-climatology/rivers_daily_sss150.nc`
    * fix Susan's notebook


##### Miscellaneous

* updated VSCode Remote - SSH extension on `lox` to 0.114.1 and started getting permission errors
  from GitHub like Vicente's issue
* Zoom w/ Henryk re: `salish`
  * `/backup` is RAID0 of 3x6T drives; one is bad
  * he says that he would have to buy refurbished to get a 10T hot spare for `/data` to go in one of
    the `/backup` slots; I'm surprised because I see 10T on memoryexpress.com
  * the fundamental issue is that he doesn't like Ubuntu; prefers RedHat; `sockeye` runs Rocky, the
    replacement for CentOS that was created when RedHat abandoned



#### Sat 7-Sep-2024

Recovery at home.



#### Sun 8-Sep-2024

Recovery at home.



### Week 37

#### Mon 9-Sep-2024

Recovery at home

FAL estate work: final distribution to Jamie


##### Miscellaneous

* squash-merged pre-commit.ci PRs re: config auto-updates
  * MoaceanParcels
  * NEMO-Cmd - also `black` code gardening
  * cookiecutter-MOAD-pypkg
  * gha-workflows
  * SalishSeaCmd
  * salishsea-site
  * Reshapr
  * SalishSeaNowcast
  * AtlantisCmd
* compiled list of packages for Henryk to install on `salish` to that I can try to build XIOS, NEMO,
  and Ariane:
    <!-- markdownlint-disable MD013 -->
    ```text
    ppa:git-core/ppa
    emacs
    gfortran
    openmpi-bin
    libopenmpi3
    libopenmpi-dev
    libnetcdf-dev
    libnetcdff-dev
    libnetcdf-mpi
    netcdf-bin
    nco
    liburi-perl
    m4
    cmake
    ksh
    ```
    <!-- markdownlint-enable MD013 -->


##### SalishSeaCast

* started dask cluster on `salish`
* backfilled today's day-average datasets:
    <!-- markdownlint-disable MD013 -->
    ```bash
    make_averaged_dataset day physics
    make_averaged_dataset day chemistry
    make_averaged_dataset day biology
    ```
    <!-- markdownlint-enable MD013 -->
  fast and minimal CPU load on `salish`
* backfilled August average physics datasets:
    <!-- markdownlint-disable MD013 -->
    ```bash
    for dd in {01..31}; do make_averaged_dataset day physics 2024-08-${dd}; done
    # launches: make_averaged_dataset month physics 2024-08-01
    ```
    <!-- markdownlint-enable MD013 -->
* month averaging generated 5 messages: `Only found a single cohort. 'map-reduce' is preferred.`
* backfilled August average chemistry datasets:
    <!-- markdownlint-disable MD013 -->
    ```bash
    for dd in {01..31}; do make_averaged_dataset day chemistry 2024-08-${dd}; done
    # launches: make_averaged_dataset month chemistry 2024-08-01
    ```
    <!-- markdownlint-enable MD013 -->



#### Tue 10-Sep-2024

Recovery at home

Debby arrived for Ellie's defense


##### SalishSeaCast

* backfilled August average biology datasets:
    <!-- markdownlint-disable MD013 -->
    ```bash
    for dd in {01..31}; do make_averaged_dataset day biology 2024-08-${dd}; done
    # launches: make_averaged_dataset month chemistry 2024-08-01
    ```
    <!-- markdownlint-enable MD013 -->
* updated production env to `flox=0.9.10` to resolve noisy info messages that were changed to debug
  level
* backfilled September day-average datasets:
    <!-- markdownlint-disable MD013 -->
    ```bash
    for dd in {01..08}; do make_averaged_dataset day physics 2024-09-${dd}; done
    for dd in {01..08}; do make_averaged_dataset day chemistry 2024-09-${dd}; done
    for dd in {01..08}; do make_averaged_dataset day biology 2024-09-${dd}; done
    ```
    <!-- markdownlint-enable MD013 -->


##### Miscellaneous

* tried clean build of XIOS-2 on `salish`:
  * forgot to put c++ packages on list for Henryk:
    <!-- markdownlint-disable MD013 -->
    ```text
    g++
    libnetcdf-c++4-dev
    ```
    <!-- markdownlint-enable MD013 -->
  * success
* tried clean build of `sss150` NEMO config on `salish`:
  * 4 string overflow warnings:
    * `Warning: ‘__builtin_memmove’ reading 80 bytes from a region of size 79 [-Wstringop-overflow=]`
  * failed due to no `xios.mod`
  * succeeded after XIOS-2 build



#### Wed 11-Sep-2024

Recovery at home


##### Miscellaneous

* built `SalishSeaCast_Blue` NEMO config on `salish`:
  * 4 string overflow warnings in `EXTERNAL/IOIPSL/src/calendar.f90`:
    * `Warning: ‘__builtin_memmove’ reading 80 bytes from a region of size 79 [-Wstringop-overflow=]`
* discovered that I need to manually delete pre-commit.ci PR branches 🙁
* tried to run `SalishSeaCast_Blue` NEMO config on `salish`:
  * blows up memory
* got Henryk to install `gdb`



##### SalishSeaCmd

* started changing job submit command for `salish` from `qsub` to `bash`; not a trivial change



#### Thu 12-Sep-2024

Recovery at home


##### Miscellaneous

* running `SalishSeaCast_Blue` in `gdb` shows same growing memory issue; interupt stops in `malloc.c`
  before first executable line
  * same for `xios_server.exe`
* tried `MY_GYRE`
  * can't build without `xios`
  * same memory explosion
* UBC-IOS modeling mtg
  * Karyn on zooplankton evaluation
  * discussed XIOS/NEMO build issues w/ Michael & Amber
* Phys Ocgy seminar: Vicente on PRODIGY Bamfield turbulence obs



#### Fri 13-Sep-2024

Recovery at home


##### Miscellaneous

* MOAD group mtg; see whiteboard
* emailed Michael with details of NEMO build problem
* asked Henryk to downgrade to gcc-7 on `salish`



#### Sat 14-Sep-2024

Recovery at home.



#### Sun 15-Sep-2024

Recovery at home.


##### SalishSeaCast

* `download_live_ocean` was delayed until ~10:30



### Week 38

#### Mon 16-Sep-2024

Recovery at home


##### Miscellaneous

* sent `salish` replacement specs to Henryk
* sent RFQ for `salish` replacement to System76
* researched compilers and opemMPI on conda-forge
  * can't replicate `arbutus`
* shut down and deleted `fvcom6` instance on `arbutus`
* created `test-20-04` instance on `arbutus`
  * image: `Ubuntu-20.04.6-Focal-x64-2023-11`
  * flavour: `nemo-c16-60gb-90-numa-test`
  * ip address: `192.168.238.201`
  * did head node setup from deployment docs
  * installed OS pkgs:
    * git
    * gfortran
    * libopenmpi3 libopenmpi-dev openmpi-bin
    * libnetcdf-dev libnetcdff-dev netcdf-bin libnetcdf-c++4-dev
    * g++ gdb
    * liburi-perl make cmake ksh mg
  * cloned XIOS-ARCH & XIOS-2
  * created arch file symlinks and ran XIOS-2 build
* investigated Karyn's permission denied issue for Susan run results on `lox`


##### SalishSeaCast

* `download_live_ocean` timed out at ~12:00
  * re-ran at ~12:02; success at ~12:07
* deleted old `/results/` archives to free storage:
  * `/results/SalishSea/forecast2.201905/`
  * `/results/SalishSea/forecast.201905/`
  * `/results/SalishSea/nowcast-blue.201905/`
* checked `nowcast-green.201805` status on `graham:/nearline/`:
  * missing:
    * mar15
    * apr15



#### Tue 17-Sep-2024

Worked at ESB while Rita was at home

ESB Welcome Back BBQ


##### Miscellaneous

* continued testing on `test-20-04`
  * built XIOS with GCC-9 compilers and `--debug` flag to set `-O0`
  * started successfully in `gdb` and failed due to no `iodef.xml`
* resumed testing on `salish`
  * built XIOS with GCC-9 compilers and `--debug` flag to set `-O0`
  * started successfully in `gdb` and failed due to no `iodef.xml`
  * ran XIOS + NEMO on 1 + 1, then 1 + 7 processors
    * no time steps, but lots of ocean.output, then failure with a traceback into XIOS
* received quote for new compute server from System76; salivating 🤤



#### Wed 18-Sep-2024


##### Miscellaneous

* email from Michael confirming my XIOS findings and proposing a way forward by updating XIOS checkout
* sent questions re: RAID and storage cost to System76; received updated quote w/ RAID controller



#### Thu 19-Sep-2024

LifeLabs appt


##### Miscellaneous

* continued email discussion w/ Michael re: updating XIOS checkout
* explored XIOS revision log
* asked Henryk to install `svn` on `salish`
* phys ocgy seminar: new students Aidan and Kat past research



#### Fri 20-Sep-2024

Worked at ESB


##### Miscellaneous

* figured out how to create a Python 3.13 release candidate env:
    `mamba create -n py313 -c conda-forge/label/python_rc python=3.13.0rc2`
* updated `kudu` to PyCharm 2024.2.2
* MOAD group mtg; see whiteboard


##### SalishSeaNowcast

* updated repos on `kudu`
* build new `salishsea-nowcast` env on `kudu`
* started work on automating month-average productivity and grazing datasets
* branch: month-avg-prod-graz
* PR#
* stalled thinking about a way to handle `grazing` and `growth` being valid
  options for month-averaging, but not day-averaging



#### Sat 21-Sep-2024

Drove to White Rock to visit JRA



#### **Sun 22-Sep-2024**


##### Miscellaneous

* updated `khawla` to PyCharm 2024.2.2


##### NEMO-Cmd

* tried a hail-mary test of Python 3.13 test env creation on GitHub:
  * branch: py131
  * PR#92
  * added `conda-forge/label/python_rc` to test env channels list
  * added `python=3.13.0rc2` to `python-version` matrix in pytest-with-coverage workflow
  * mamba solver was unable to find a collection of packages to solve the env


##### NEMO_Nowcast

* finished update to Python 3.12
  * branch: py312
  * PR#38 - squash-merged
  * bumped version to 24.1.dev0
* updated readthedocs build config:
  * branch: rtd-build-main
  * PR#57 - squash-merged
  * ubuntu-24.04 and mambaforge-23.11
  * sphinx=7.2.6 and sphinx-rtd-theme=2.0.0





* pre-commit.ci PR revealed failing test and pandas date parser warnings
  * moad_tools







* pip=24.2 has started to complain about -e installs for packages w/o `pyproject.toml`
  * NEMO_Nowcast
  * SalishSeaTools



fortran.fortls.directories




Add Tereza's pubs to ERDDAP.


TODO:

* change automation workflow to run nowcast-green in place of nowcast-blue
  * add output of 10min avg tide gauge station files
* remove VHFR FVCOM from automation workflow
  * remove FVCOM boundary slab files output from nowcast-green/file_def.xml
  * drop FVCOM-Cmd and OPPTools dependencies
* `sandheads_winds` is using HTTP instead of HTTPS for obs collection via
  `salishsea_tools.stormtools.get_EC_observations()`; same in `tools.I_ForcingFiles.Atmos.weather.get_EC_observations()`


TODO:

* Update AtlantisCmd to drop Python 3.10 because NEMO-Cmd has dropped it;
  GHA workflow is failing



* Python 3.12:
  * successful workflow test with 3.12:
    * AtlantisCmd
    * NEMO_Nowcast - migrated on 22Sep24 in PR#38
    * salishsea-site - migrated on 19Apr24 in PR#77
    * moad_tools - migrated on 18Dec23 in PR#43
    * SalishSeaCmd - migrated on 29nov23  PR#49
    * NEMO-Cmd - migrated on 20nov23 in PR#68
    * SalishSeaNowcast - success on khawla on 6nov23, migrated on 10nov23 in PR#209
    * Reshapr - migrated on 28oct23 in PR#99
    * erddap-datasets - migrated on 6nov23 in PR#1
    * SalishSeaCast/docs - migrated on 7feb24 in PR#37
  * failed workflow test with 3.12:
    * MOAD/docs - expect same problem as SalishSeaCast/docs
    * MoaceanParcels - failing with 3.10; no point in trying 3.12 yet
  * no workflows:
    * analysis-doug




Refresh myself on Fortran in VS Code and on-the-fly compilation; prep to present to group.




TODO:

* change download_weather to gather only files missed by collect_weather so that it can
  work with crop_gribs monitoring incoming files
  * check for presence of files before downloading them; skip if present


TODO:

* update .readthedocs.yaml to use ubuntu-22.04 and mambaforge-22.9 in many repos
  * MOAD/docs - done 13sep23 in PR#32
  * FVCOM-Cmd - done in PR#10
  * tools - done 28aug23 in PR#84
  * AtlantisCmd - done 28aug23 in PR#27
  * Reshapr - done 28oct23 in PR#100
  * SalishSeaNowcast - done 10nov23 in PR#215
  * NEMO-Cmd - done 20nov23 in PR#71
  * SalishSeaCmd - done 29nov23 in PR#54
  * moad_tools - done 18dec23 in PR#47
  * SalishSeaCast/docs - done 7feb24 in PR#43
  * salishsea-site - done 9apr24 in PR#74
  * NEMO_Nowcast - done 22sep24 in PR#57 (ubuntu-24.04 and mambaforge-23.11)

  * rpn-to-gemlam
  * MoaceanParcels
  * ECget


TODO:

* fix straight line gaps in wwatch3 forecast plots (forecast2 are okay)



TODO:

* modernize packaging:
  * Reshapr - done 30oct23 in PR#101
  * moad_tools - done 18dec23 in PR#48
  * salishsea-site - done 22apr24 in PR#78
  * NEMO_Nowcast
  * SalishSeaTools
  * cookiecutter-MOAD-pypkg
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
    * docs - done 7feb24 in PR#45
    * SOG-Bloomcast-Ensemble - issue created
    * tools - issue created


Repos that use readthedocs:

* active:
  * AtlantisCmd
  * ECget
  * MoaceanParcels
  * NEMO-Cmd
  * NEMO_Nowcast
  * Reshapr
  * rpn-to-gemlam
  * SalishSeaCmd
  * SalishSeaCast/docs
  * tools
  * SalishSeaNowcast
  * salishsea-site
  * MOAD/docs
  * moad_tools
* archived:
  * Make-MIDOSS-Forcing
  * midoss-docs
  * MOHID-Cmd
  * WWatch3-Cmd
