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
  * NEMO forecast2 failed with error in oceean.output
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
  https://github.com/MIDOSS/MIDOSS-MOHID-config/blob/main/monte-carlo/random-oil-spills.yaml


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

TODO:

* e3t from grid_T -> vvl ??
* PAR & turbidity from chem -> light ??


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

TODO:

* e3t from grid_T -> vvl ??
* PAR & turbidity from chem -> light ??
* co2_flux from chem -> surface co2 flux


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
  https://www.youtube.com/watch?v=u9k6HikDyqk though the video doesn't describe doing so
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

#### **Mon 15-Jan-2023**

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

TODO:

* e3t from grid_T -> vvl ??
* PAR & turbidity from chem -> light ??


##### SalishSeaNowcast

Continued changing ERDDAP dataset ids to V21-11 for `ping_erddap` worker:

* branch: v202111-erddap
* PR#227

Continued removing nowcast-dev runs from configuration and workflow:

* branch: drop-nowcast-dev


TODO:

* rename make_runoff_file to make_v201702_runoff_file
* rename make_v202111_runoff_file to make_runoff_file
* add config tests for `run type[*][mesh mask]`
* add config tests for `run type[*][bathymetry]`
* add config tests for `run type[*][land processor elimination]`
* add config tests for `run type[*][run sets dir]`
* improve test_run_NEMO test for forcing symlinks ??
* add tests for _upload_*_files in upload_forcing worker: ssh, turbidity, runoff, weather





##### salishsea-site

biology figures pages since 31dec23 are failing with an internal server error;
see `/logs/salishsea-site/pyramid.log`

TODO:

* drop ciliates thalweg and surface plot from biology pages for 01jan24 onward re: v202111
* fix file name for Fraser River turbidity thalweg & surface plot for 01jan24 onward re: v202111
  variable name change
* add Suchy et al 2023 to publications page (and docs/CITATION.rst)




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
* ref: https://www.atlassian.com/git/tutorials/merging-vs-rebasing
* git switch feature
* git rebase main
* In PyCharm > Git > Log context menu "Rebase 'feature' onto 'main'"
* **BUT** if the changes in the feature branch overlap files in main, it's possible that
  a merge will be required



TODO:
* update .readthedocs.yaml build:os to ubuntu-22.04
* add sphinx-notfound-page extension to to repos with docs
  * https://sphinx-notfound-page.readthedocs.io/en/latest/index.html
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
