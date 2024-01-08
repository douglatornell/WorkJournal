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





##### salishsea-site

biology figures pages since 31dec23 are failing with an internal server error;
see `/logs/salishsea-site/pyramid.log`

TODO:

* drop ciliates thalweg and surface plot from biology pages for 01jan24 onward re: v202111
* fix file name for Fraser River turbidity thalweg & surface plot for 01jan24 onward re: v202111
  variable name change


##### SalishSeaNowcast

Fixed test_download_live_ocean failure on khawla with nccopy not found:

* branch: mock-NEMO-Cmd-api-deflate
* PR#
* added monkeypatch mock for nemo_cmd.api.deflate() to avoid launching nccopy in subprocess in test

TODO:

* test_download_live_ocean fails on khawla with nccopy not found
* test_make_feeds fails in pytest-with-coverage due to python-feedgen v1.0.0
* rename make_runoff_file to make_v201702_runoff_file
* rename make_v202111_runoff_file to make_runoff_file
* add config tests for `run type[*][mesh mask]`
* add config tests for `run type[*][bathymetry]`
* add config tests for `run type[*][land processor elimination]`
* add config tests for `run type[*][run sets dir]`
* improve test_run_NEMO test for forcing symlinks ??
* add tests for _upload_*_files in upload_forcing worker: ssh, turbidity, runoff, weather




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
