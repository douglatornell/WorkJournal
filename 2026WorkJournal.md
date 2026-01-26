# 2026 Work Journal

This is my public work journal.
This journal is about:

* my work as a Research Software Engineer with Dr. Susan Allen in the
  Department of Earth, Ocean and Atmospheric Sciences at the University of British Columbia
* my open-source activities
* occasional notes about life in general


## January

### Week 1

#### Thu 1-Jan-2025

**Statutory Holiday** - New Year's Day

Juan de Fuca Beach House

##### SalishSeaCast

* `crop_gribs 12` was delayed ~2h due to 1 unprocessed file
* `collect_river_data SquamishBrackendale` got empty time series
* manual `rsync` of dec25 tarball finished in `tmux` session on `skookum`



#### Fri 2-Jan-2025

Juan de Fuca Beach House to Vancouver

##### SalishSeaCast

* `crop_gribs 06` failed with 484 files unprocessed
  * only consequence was no `forecast2` runs
* `collect_river_data SquamishBrackendale` got empty time series
* storm surge alert for Strait of Georgia for tomorrow morning
  * 5.17 m at 06:35 at Sandy Cove; 0 m/s E wind at Sandy Cove



#### Sat 3-Jan-2025

##### SalishSeaCast

* storm surge alert for Strait of Georgia for tomorrow morning
  * 5.49 m at 07:15 at Sandy Cove; 1 m/s S wind at Sandy Cove
* manually re-ran `crop_gribs 06 2026-01-02 --backfill --debug` to backfill from yesterday's failure



#### Sun 4-Jan-2025

##### SalishSeaCast

* `collect_river_data SquamishBrackendale` got empty time series
* storm surge alert for Strait of Georgia for tomorrow morning
  * 5.31 m at 08:25 at Sandy Cove; 3 m/s SSW wind at Sandy Cove



### Week 2

#### Mon 5-Jan-2025

##### SalishSeaCast

* `collect_river_data SquamishBrackendale` got empty time series
* storm surge alert for Strait of Georgia for tomorrow morning
  * 5.31 m at 08:25 at Sandy Cove; 3 m/s SSW wind at Sandy Cove
* `crop_gribs 00` failed due to no directory to watch at 13:44
  * file system sluggishness? I had failures from some ERDDAP tests too...
  * re-ran manually at ~16:30


##### Miscellaneous

* tested single point time series graphs of DIC from ERDDAP in preparation for mtg tomorrow with
  Yayla of CIOOS
  * success from 1jan07 within processing time limit: 32d, 60d, 90d, 96d
  * inconsistent success/failure from 1jan07 within processing time limit: 120d
  * failure from 1jan07 within processing time limit: 125d, 127d, 135d, 151d
* tested single point time series netCDF request for all carbon variables from ERDDAP
  * failure from 1jan07 within processing time limit: 96d, 90d, 60d, 46d
  * success from 1jan07 within processing time limit: 1d, 2d, 5d, 10d, 20d, 31d, 38d
* installed Pixi on `skookum`
  * used it to install improved cli tools in global environments:
    * `pixi global install eza`
    * `pixi global install fd-find`
    * `pixi global install bat`
    * `pixi global install ripgrep`
    * `pixi global install fzf`


##### NEMO-Cmd

* continued changing to use Pixi for project & env mgmt; PR#121
  * updated README re: Pixi and command processor packages that extend `NEMO-Cmd`


##### Security Updates

* Squash-merged dependabot PRs to update `filelock` to 3.20.1 re: CVE-2025-68146
  Time-of-Check-Time-of-Use (TOCTOU) race condition symlink attack vulnerability
  * SOG-forcing


##### Reshapr

* continued writing example use docs for extractions from research runs on `nibi`



#### Tue 6-Jan-2025

Worked at ESB while Rita was at home

##### SalishSeaCast

* `collect_river_data SquamishBrackendale` got empty time series
* `grib_to_netcdf nowcast+` failed due to missing 00 GRIB file
  * re-run of `crop_gribs 00` did nothing
* recovery:
  <!-- markdownlint-disable MD031 -->
  ```bash
  crop_gribs 00 --backfill
  grib_to_netcdf nowcast+
  upload_forcing nowcast+ arbutus
  upload_forcing nowcast+ robot.nibi
  upload_forcing nowcast+ orcinus
  upload_forcing nowcast+ optimum
  ```
  <!-- markdownlint-enable MD031 -->
* storm surge alert for Strait of Georgia for tomorrow morning
  * 5.33 m at 08:55 at Sandy Cove; 3 m/s SSW wind at Sandy Cove


##### NEMO-Cmd

* squash-merged PR#121 re: changing to use Pixi for package & env mgmt
* changed dev env on `kudu` to use Pixi
  * `pixi run 'echo $CONDA_PREFIX/libexec/conda'` helps with that


##### Miscellaneous

* MOAD group mtg; see whiteboard
* changed `alineisabelle` from member of UBC-MOAD on GitHub to Outside Collaborator
  * disappeared from Members list
* Zoom w/ Yayla re: data for CIOOS OA data portal
  * evaluate putting climatology datasets on ERDDAP - **TODO**
* installed Pixi on `kudu`
* updated `kudu` PyCharm to 2025.3.1


##### Security Updates

* Squash-merged dependabot PRs to update `bokeh` to 3.8.2 re: CVE-2026-21883
  Cross-Site WebSocket Hijacking (CSWSH) vulnerability
  * MoaceanParcels
  * Reshapr
  * SalishSeaNowcast
* Squash-merged dependabot PRs to update `pynacl` to 1.6.2 re: CVE-2025-69277
  mishandled elliptic curve point validity check vulnerability
  * SalishSeaNowcast


##### SalishSeaNowcast

* issue#310 re: deprecation of `trapz()` in `nowcast.analyze` module is major as of the release
  numpy-2.4.0 in which the deprecation expired


##### SalishSeaCmd

* started planning to use Pixi for package & env mgmt



#### Wed 7-Jan-2025

##### SalishSeaCast

* `collect_river_data SquamishBrackendale` got empty time series
* storm surge alert for Strait of Georgia for tomorrow morning
  * 5.18 m at 09:25 at Sandy Cove; 2 m/s SW wind at Sandy Cove


##### Miscellaneous

* confirmed that changing `alineisabelle` from member of UBC-MOAD on GitHub to Outside Collaborator
  removed them
  * perhaps it sent them an invitation to become an outside collaborator, but Aline has not been
    publicly active on GitHub since they stopped working with us in apr21


##### SalishSeaNowcast

* fixed issue#310 re: deprecation of `trapz()` in `nowcast.analyze`; PR#410
  * easy fix: just changed `trapz()` to `trapezoid()` and tests passed


##### 2x resolution SalishSeaCast

* continued work on 2xrez processing and verification notebooks:
  * thrash because PyCharm 2025.3.1 stopped including `PYTHONPATH` in `sys.path` so imports from
    `salishsea_tools` fail
    * work-around is to explicitly add `SalishSeaTools/` path - *ugly*
    * see https://youtrack.jetbrains.com/projects/PY/issues/PY-85114/Project-root-and-source-roots-are-not-available-to-Jupyter-notebooks
  * adjusted row 19 tile 7
    * reviewed row 19 changes with Susan
  * added row 20 - Union Bay to Jervis
    * reviewed work needed with Susan


##### SalishSeaCmd

* started changing to use Pixi for package & env mgmt; PR#121
  * `pixi init` to add `[tool.pixi.*]` tables to `pyproject.toml`
  * clean up `.gitignore`
  * add `,gitattributes` to VCS
  * `pixi import envs/environment-hpc.yaml --format conda-env` to get minimal packages in default environment
    * that created tables for a feature called `salishsea-cmd`
    * had to edit `pyproject.toml` to get things set up for the `default` feature
    * deleted `pip` from dependencies table
    * `pixi add --editable --pypi "NEMO-Cmd@git+https://github.com/SalishSeaCast/NEMO-Cmd.git"`
      to install NEMO-Cmd from GitHub
  * `pixi install` created the env and the lock file
    * confirmed with `pixi run salishsea --version`
  * deleted `envs/environment-hpc.yaml`
  * configured PyCharm:
    * `pixi add pixi-pycharm`
    * set `conda` executable to output of `pixi run 'echo $CONDA_PREFIX/libexec/conda'`
    * renamed interpreter in PyCharm UI to `SalishSeaCmd:default`
  * added `test` feature based on `environment-test.yaml`
    * `pixi add --feature test pytest pytest-cov pytest-randomly`
    * `pixi workspace environment add test --feature test --solve-group default`
    * `pixi run -e test pytest` works
      * revealed a new DeprecationWarning re: the `namespace` parameter in `cliff.commandmanager.CommandManager`
        * created issue#122
    * `pixi task add -f test pytest "pytest"` shortens the incantation to `pixi run pytest`
  * added `pytest-cov` and `pytest-cov-html` tasks
    * `pixi task add -f test pytest-cov "pytest --cov=./"`
    * `pixi task add -f test pytest-cov-html "pytest --cov=./ --cov-report html"`
  * updated dev docs to use Pixi tasks to run tests and produce coverage reports
  * added envs for Python 3.12 and 3.13 testing:
    * relax Python version in default env from `"3.14.*"` to `"*"`
    * `pixi add --feature py312 python=3.12`
    * `pixi workspace environment add test-py312 --feature py312 --feature test`
    * `pixi add --feature py313 python=3.13`
    * `pixi workspace environment add test-py313 --feature py313 --feature test`
  * added a `test-py314` env (even though it duplicates `test`) to make GHA explicit and consistent
  * `pixi add --feature py314 python=3.14`
  * `pixi workspace environment add test-py314 --feature py314 --feature test`
  * changed `pytest-with-coverage` workflow to use new reusable `pixi-pytest-with-coverage`



#### Thu 8-Jan-2025

##### SalishSeaCast

* `collect_river_data SquamishBrackendale` got empty time series


##### Miscellaneous

* UBC-IOS modeling mtg
  * Mike Foreman: Update on tidal issues with WCVI FVCOM model
  * oscillations in semi-diurnal amplitudes & phases


##### Security Updates

* Squash-merged dependabot PRs to update `urllib3` to 2.6.3 re: CVE-2026-21441
  decompression-bomb in redirect response vulnerability
  * SalishSeaCmd
  * AtlantisCmd
  * salishsea-site
  * NEMO_Nowcast
  * SalishSeaNowcast
  * Reshapr
  * SOG-Bloomcast-Ensemble
  * SalishSeaTools
  * MOAD/docs
  * MoaceanParcels
  * moad_tools
  * cookiecutter-analysis-repo
  * FUN
  * SalishSeaCast/docs
  * cookiecutter-MOAD-pypkg
  * NEMO-Cmd
  * cookiecutter-djl-pypkg
  * SOG-Bloomcast
  * erddap-datasets



#### Fri 9-Jan-2025

##### SalishSeaCast

* `collect_river_data SquamishBrackendale` got empty time series


##### Miscellaneous

* ERDDAP showcase:
  * Mathew Biddle: remote replication of datasets
    * https://docs.google.com/presentation/d/1MR500hnf2ya2jEzqAoXLT0Pn8I0l6Hcnrxtmew14ABE/edit?usp=sharing
    * IOOS ERDDAP admin
    * `EDDGridFromERDDAP` and `EDDTableFromERDDAP`
      * like symlinks from other servers
      * copies and caches metadata from source servers; forwards data requests to source servers
    * `EDDTableCopy`
      * makes local copies of table datasets
      * reduces load on source servers
      * allows granularity configuration
    * `cacheFromUrl`
      * datasets constructed from HTTP servers
      * downloads files
      * primarily about facilitating cloud data
  * Madison Richardson: Complex ERDDAP dataset configuration example
    * automating access to password protected ERDDAP datasets
    * Selenium WebDriver
  * Giulo Verazzo: ERDDAP CMS
    * web app for users to manage dataset XML generation from netCDF and CSV without
      XML knowledge/editing and server file system access
    * essentially a form version of the XML generation script
  * library to guess standard names based on variable names and provide attrs
    * https://github.com/gulfofmaine/standard_knowledge


##### SalishSeaCmd

* continued changing to use Pixi for package & env mgmt; PR#121
  * added `docs` feature and env based on `environment-test.yaml` and `environment-rtd.yaml`
    * `pixi add --feature docs sphinx=8.1.3 sphinx-notfound-page=1.0.4 sphinx-rtd-theme=3.0.0`
    * `pixi add --feature docs --pypi commonmark recommonmark readthedocs-sphinx-ext`
    * `pixi workspace environment add docs --feature docs --solve-group default`
    * added tasks for common docs work:
      * `pixi task add -f docs --cwd docs/ docs make clean html`
      * `pixi task add -f docs --cwd docs/ linkcheck make clean linkcheck`
  * updated dev docs to use Pixi tasks to build HTML docs and run link checker
  * changed `.readthedocs.yaml` to use customized build process for Pixi from RTD docs
  * Updated `source_suffix` in Sphinx configuration re: support for multiple file types
  * changed `sphinx-linkcheck` workflow to use new reusable `pixi-sphinx-linkcheck`
  * deleted `envs/environment-rtd.yaml`
  * deleted `envs/environment-test.yaml`
  * added `dev` feature and env based on `environment-dev.yaml`
    * `pixi add --feature dev black hatch pre-commit`
    * `pixi add --feature dev pytest pytest-cov pytest-randomly`
    * `pixi add --feature dev sphinx=8.1.3 sphinx-notfound-page=1.0.4 sphinx-rtd-theme=3.0.0`
    * `pixi workspace environment add dev --feature dev --solve-group default`
    * installed `pre-commit` to run from `dev` env
      * `pixi run -e dev pre-commit install`
  * removed `salishsea-cmd` conda env from `khawla`
  * updated dev docs re: use of Pixi
  * dropped `environment-dev.yaml`
  * dropped `pytest.ini` because its job was to exclude `NEMO-Cmd` tests in `envs./src/` on GitHub
    from discovery, and that's no longer an issue
  * moved `requirements.txt` from `envs/` to top level directory and deleted `envs/`
  * added task to update `requirements.txt via`pip list`
    * `pixi task add -f dev update-reqs "python -m pip list --format=freeze >> requirements.txt"`
  * renamed `development.rst` to `pkg_development.rst`
  * updated installation docs and installation paragraph of README to use Pixi



#### Sat 10-Jan-2025

##### SalishSeaCast

* `collect_river_data SquamishBrackendale` got empty time series


##### Security Updates

* Squash-merged dependabot PRs to update `pypdf` to 6.6.0 re: GHSA-4xc4-762w-m6cg
  long runtime vulnerability
  * SalishSeaNowcast


##### SalishSeaCmd

* continued changing to use Pixi for package & env mgmt; PR#121
  * tested updating NEMO-Cmd to latest commit on GitHub:
    * `pixi update nemo-cmd`  # note that the package name is case- and hyphen-sensitive
  * updated use docs to `pixi run salishsea ...`
  * added Pixi badges to README and dev docs
  * changed `salishsea` command definitions in generated `bash` scripts to use `pixi run -m ...`
    by using `Path(__file__).parent.parent` in `run.py`


#### Sun 11-Jan-2025

##### SalishSeaCast

* `collect_river_data SquamishBrackendale` got empty time series
* `get_onc_ferry TWDP` failed due to incompatible boolean index array shape
  * may indicate resumption of data stream
* `collect_weather 18 2.5km` failed at 13:33 in `fix_perms()` due to not finding gid for group `sallen`
* `crop_gribs 18` timed out at 15:50 with 288 files unprocessed


##### SalishSeaCmd

* continued changing to use Pixi for package & env mgmt; PR#121
  * tested updating NEMO-Cmd to latest commit on GitHub:
    * `pixi update nemo-cmd`  # note that the package name is case- and hyphen-sensitive
  * updated use docs to `pixi run salishsea ...`
  * added Pixi badges to README and dev docs
  * changed `salishsea` command definitions in generated `bash` scripts to use `pixi run -m ...`
    by using `Path(__file__).parent.parent` in `run.py`
  * tested doing a SalishSeaCast run on `fir` using the `pixi` branch
    * deleted `NEMO-Cmd` clone
    * uninstalled `mamba` and `conda`
    * `pixi run -m ~/MEOPAR/SalishSeaCmd salishsea run ./fir-example.yaml \
        /scratch/dlatorne/MEOPAR/results/01mar23-11x32-salishsea-pixi-real --debug`
    * success!!!



### Week 3

#### Mon 12-Jan-2025

##### SalishSeaCast

* automation stopped when yesterday's `crop_gribs 18` timed out
  * yesterday's `collect_weather 18 2.5km` is still running
  * recovery started at 09:35:
  <!-- markdownlint-disable MD031 -->
  ```bash
  pkill -f collect_weather  # stalled 18Z process
  # move /results/forcing/atmospheric/continental2.5/GRIB/20260111/18 aside
  crop_gribs 18 --fcst-date 2026-01-11
  download_weather 18 2.5km 2026-01-11 --backfill
  # skipped 1km downloads because the files are no longer available on the ECCC server
  fd --type f . /SalishSeaCast/datamart/hrdps-continental/18 -X rm
  collect_weather 00 2.5km 2026-01-12 --backfill
  crop_gribs 00 --backfill
  pkill -f collect_weather  # 06Z process that is looking for files that have already been downloaded
  collect_weather 06 2.5km 2026-01-12 --backfill
  # crop_gribs 06 stalled with 1 file unprocessed so I killed it and re-ran it
  # wait for forecast2 runs to finish
  pkill -f collect_weather  # 12Z process that is looking for files that have already been downloaded
  collect_weather 12 2.5km 2026-01-12 --backfill
  ```
  <!-- markdownlint-enable MD031 -->
* `collect_river_data SquamishBrackendale` got empty time series


##### SalishSeaCmd

* continued changing to use Pixi for package & env mgmt; PR#121
  * dropped `NEMO-Cmd` from `vcs revisions` stanza of YAML files in docs
  * added docs re: `pixi run -m` flag


##### `nibi`

* changed my installation to use Pixi for `SalishSeaCmd`
  * deleted `NEMO-Cmd` clone
  * `mamba env remove -n salishsea-cmd`
  * deleted `--user` install elements from `NEMO-Cmd` and `SalishSeaCmd`


##### Miscellaneous

* updated PyCharm to 2025.3.1.1 on `khawla`
* started reviewing Tall's paper



#### Tue 13-Jan-2025

Worked at ESB

##### SalishSeaCast

* Fraser buoy relative humidity sensor stopped reporting before 04:35
* `collect_river_data SquamishBrackendale` got empty time series
* `crop_gribs 18` timed out with 144 file unprocessed ~7m before `collect_weather 8 2.5km` finished
  * recovery started at ~19:35:
  * `crop_gribs 18 --backfill`


##### SalishSeaCmd

* squash-merged PR#121 re: changing to use Pixi for package & env mgmt


##### Miscellaneous

* MOAD group mtg; see whiteboard
* continued reviewing Tall's paper


##### MOAD/docs

* planned changing to use Pixi for deps & env mgmt; PR#
* planned updates re: Pixi replacing `conda/mamba`



#### Wed 14-Jan-2025

##### SalishSeaCast

* `collect_river_data SquamishBrackendale` got empty time series


##### Security Updates

* Squash-merged dependabot PRs to update `virtualenv` to 20.36.1 re: CVE-2026-22702
  Time-of-Check-Time-of-Use (TOCTOU) race condition symlink attack vulnerability
  * cookiecutter-MOAD-pypkg
  * moad_tools
  * NEMO_Nowcast
  * MoaceanParcels
  * SOG-Bloomcast-Ensemble
  * SalishSeaTools
  * FUN
  * SalishSeaCast/docs
  * AtlantisCmd
  * salishsea-site
  * SalishSeaNowcast
  * Reshapr
  * MOAD/docs
  * gha-workflows
  * NEMO-Cmd
  * SalishSeaCmd
  * erddap-datasets
  * SOG-forcing

* Squash-merged dependabot PRs to update `filelock` to 3.20.3 re: CVE-2026-22701
   (another) Time-of-Check-Time-of-Use (TOCTOU) race condition symlink attack vulnerability
  * AtlantisCmd
  * SOG-Bloomcast-Ensemble
  * SalishSeaCast/docs
  * MOAD/docs
  * salishsea-site
  * Reshapr
  * SalishSeaTools
  * gha-workflows
  * cookiecutter-MOAD-pypkg
  * MoaceanParcels
  * NEMO_Nowcast
  * moad_tools
  * SalishSeaNowcast
  * FUN
  * NEMO-Cmd
  * SalishSeaCmd
  * erddap-datasets
  * SOG-forcing


##### Miscellaneous

* updated Pixi on `khawla` to 0.63.0


##### SalishSeaCast/docs

* changed to use Pixi for deps & env mgmt; PR#74 - squash-merged
  * `pixi init --import environment-rtd.yaml` to create `pixi.toml`
  * `pixi add --pypi commonmark recommonmark readthedocs-sphinx-ext`
  * cleaned up `pixi.toml`:
    * drop `nodefaults` channel
    * add `"osx-64", "osx-arm64", "win-64"` to platforms list
    * drop `version`
    * add `readme`, `repository`, `documentation`
    * dependencies:
      * add comments re: `pre-commit`, `*sphinx*` and `pypi-dependencies`
  * clean up `.gitignore`
  * add `,gitattributes`, `pixi.lock` and `pixi.toml` to VCS
  * installed `pre-commit` to run from `default` env
    * `pixi run pre-commit install`
  * added `check-toml` to `.pre-commit-config.yaml`
  * added tasks for common docs work:
    * `pixi task add docs make clean html`
    * `pixi task add linkcheck make clean linkcheck`
  * added `.pixi` to `exclude_patterns` in `conf.py`
  * changed `sphinx-linkcheck` workflow to use new reusable `pixi-sphinx-linkcheck`
  * changed `.readthedocs.yaml` to use customized build process for Pixi from RTD docs
  * deleted `environment-rtd.yaml`
  * removed `salishseacast-docs` conda env from `khawla`
  * added task to update `requirements.txt via`pip list`
    * `pixi task add update-reqs "python -m pip list --format=freeze >> requirements.txt"`
  * added Pixi badges to README
* fixed broken and redirected links; PR#75 - squash-merged
  * dropped `mercurial.el` section
  * dropped references to `Marlin` tool and added deprecation warnings to `NEMO` and `XIOS-2`
    repo maintenance sections
  * updated various other links
  * added `www.alliance.ca` and `www.emacswiki.org` patterns to linkcheck ignore list when it runs
    on GHA because those domains rate limit or block requests from GitHub Actions runners
* updated `nibi` setup docs re: Pixi replacing `conda/mamba`; PR#76 - squash-merged
  * drop cloning `NEMO-Cmd`
  * replace install & config of Miniforge with Pixi
    * include note about running commands with `pixi run`
  * fix link to docs about SS-run-sets; i.e. "SalishSea/ Directory repo"
  * change example `salishsea run` command to `pixi run -m $HOME/MEOPAR/SalishSeaCmd salishsea run`




#### Thu 15-Jan-2025

##### SalishSeaCast

* `crop_gribs 12` was delayed ~2h due to 1 unprocessed file
* `collect_river_data SquamishBrackendale` got empty time series


##### Miscellaneous

* updated Pixi on `khawla` to 0.63.1
* Alliance Townhall
  * Michael Schell, new CEO opening remarks
    * emergency MD
    * Alliance is changing from start-up mindset to sustaining mind-set
    * sovereign AI
  * Felipe Pérez-Jostov
    * UofT expanding `trillium` GPUs
    * distributed storage and compute grid
      * S3-object store
      * centred on 5 national data centres
        * UofT, Waterloo, SFU, UVic, UQAM, I think
    * AI research software and training support
    * Canadian Research Data Platform (CRDP)
      * Research Activity Identifiers (RAiD)
      * National Data Spaces pilot in progress
      * expand storage by >160 Pb
  * Stephen Wu
    * AI Sovereign Compute Infrastructure Program
    * generational investment
* helped Tall with `pickle` and Numpy issues



#### Fri 16-Jan-2025

##### SalishSeaCast

* `collect_river_data SquamishBrackendale` got empty time series


##### 2x resolution SalishSeaCast

* continued work on 2xrez processing and verification notebooks:
  * adjusted row 20 tiles 4, 7, 8 & 9
    * reviewed row 20 changes with Susan
  * added row 21 - Comox Harbour to Malibu
    * reviewed work needed with Susan
  * adjusted row 21 tiles 4 & 5
    * reviewed row 20 changes with Susan
  * added row 22 - Saratoga Beach to Head of Jervis Inlet
    * reviewed work needed with Susan


##### Miscellaneous

* helped Tall with adapting to changes in `evaltools.matchData()`
* helped Raisha with repo locations for her paper repo
  * granted access to Zenodo app in SS-Atlantis GitHub org
* decided *not* to enable `write: content` in SalishSeaCast org for Sentry Seer product


##### Security Updates

* Squash-merged dependabot PRs to update `distributed` to 2026.1.1 re: CVE-2026-23528
  Jupyter + Dask XSS vulnerability
  * SalishSeaNowcast
  * MoaceanParcels
  * Reshapr



#### Sat 17-Jan-2025

##### SalishSeaCast

* `crop_gribs 12` was delayed ~2h due to 1 unprocessed file
* `collect_river_data SquamishBrackendale` got empty time series
* `upload_forcing orcinus` failed for `forecast2` and `nowcast+`
* `download_results arbutus nowcast` at 10:12 failed due to power outage
  * automation stopped



#### Sun 18-Jan-2025

##### SalishSeaCast

* `arbutus` dashboard is back
  * VMs were restarted at about 20:00



### Week 4

#### Mon 19-Jan-2025

##### SalishSeaCast

* started automation recovery and runs backfilling on `arbutus` at ~10:40:
  * `arbutus`:
    * updated system packages on `nowcast0` and auto-removed old packages
    * confirmed date, time and timezone: `timedatectl status`
    * confirmed envvars
    * mounted shared storage
      * `sudo mount /dev/vdc /nemoShare` stalled
        * I interrupted it, but it appears to have been successful
        * `nemoShare` volume appears to be stuck in "Attaching" state
    * started NFS service
    * used `mountpoint /nemoShare/MEOPAR` in bash look to confirm that `nowcast*` and `fvcom*` VMs were
      reachable
    * mounted shared storage on compute VMs via bash loops
  * `skoookum`:
    <!-- markdownlint-disable MD031 -->
    ```bash
    make_forcing_links arbutus ssh 2026-01-17
    download_results arbutus nowcast 2026-01-17  # extremely slow
    ```
    <!-- markdownlint-enable MD031 -->
    * forecast/17jan26 run failed due to executable now found on `nowcast9` (that I forgot about!)
    <!-- markdownlint-disable MD031 -->
    ```bash
    make_forcing_links arbutus ssh 2026-01-17
    upload_forcing arbutus nowcast+ 2026-01-18
    upload_forcing robot.nibi nowcast+ 2026-01-18
    upload_forcing orcinus nowcast+ 2026-01-18  # failed due to key format; an orcinus issue
    upload_forcing optimum nowcast+ 2026-01-18
    upload_forcing arbutus nowcast+ 2026-01-19
    upload_forcing robot.nibi nowcast+ 2026-01-19
    upload_forcing optimum nowcast+ 2026-01-19
    ```
    <!-- markdownlint-enable MD031 -->



#### Tue 20-Jan-2025

Worked at ESB while Rita was at home

##### Miscellaneous

* SFU-Alliance webinar:
  * Intro to Python Visualization Libraries
  * Alex Razoumov, SFU
  * Alliance Vis Team:
    * https://ccvis.netlify.app/
      * lots of past webinar recordings
    * https://docs.alliancecan.ca/wiki/Visualization
      * links to docs for various tools/libraries/packages
  * this year's series: https://folio.vastcloud.org/winterseries
  * no recordings, but slides posted
  * Python, ParaView, VMD & Gelphi (specialty tools), web
  * Python:
    * matplotlib
      * seaborn
        * for stats
        * static plots only
        * harder to customize than matplotlib
      * plotnine: grammar of graphics
        * ggplot2
    * javascript
      * plotly
        * interactive plots
        * open source engine & API
        * web dashboards via Dash
      * vega-altair
        * grammar pf graphics
    * OpenGL?
      * ParaView & VisIt
      * based on VTK
      * intro to ParaView on 6-Feb
  * VTK
    * C++ with bindings for Tcl, Java, Python, Javascript (partial)
    * ParaView is a GUI for VTK
    * legacy ASCII, current XML, in-dev HDF5
  * Alex is a huge ParaView fan
  * Python scripting of ParaView is well supported to replace interactive use
    * Python interpreter is integrated in ParaView, independent of system/env Python
  * web viz:
    * trame server/client framework
    * plug-ins for most libraries
  * exclusions:
    * cartopy
    * geoplot
    * Julia
    * Chapel
    * non-open-source
    * AI
* MOAD group mtg; see whiteboard
* replied to email from Charles about memory requirements for SalishSeaCast and guesses about scaling
  for NE Pacific MOM6/Cobalt
* had a visit from Pal
* finished reviewing Tall's paper


##### Security Updates

* Squash-merged `pre-commit` PRs to update `black` to 26.1.0 re: style updates & bug fixes
  * NEMO_Nowcast
  * salishsea-site
  * erddap-datasets
  * NEMO-Cmd
  * SalishSeaCmd
  * SalishSeaTools
  * cookiecutter-MOAD-pypkg
  * gha-workflows
  * SOG-Bloomcast-Ensemble
  * MoaceanParcels
  * Reshapr
  * SalishSeaNowcast
  * moad_tools
  * AtlantisCmd



#### Wed 21-Jan-2025

Intake interview and VO2 max test for SPARC Program

##### Miscellaneous

* helped Becca on Slack with SalishSeaCmd setup on `nibi`


##### MOAD/docs

* started changing to use Pixi for deps & env mgmt; PR#62
  * `pixi init --import environment-rtd.yaml` to create `pixi.toml`
  * `pixi add --pypi commonmark recommonmark readthedocs-sphinx-ext`
  * cleaned up `pixi.toml`:
    * drop `nodefaults` channel
    * add `"osx-64", "osx-arm64", "win-64"` to platforms list
    * drop `version`
    * add `readme`, `repository`, `documentation`
    * dependencies:
      * add comments re: `pre-commit`, `*sphinx*` and `pypi-dependencies`
  * clean up `.gitignore`
  * add `,gitattributes`, `pixi.lock` and `pixi.toml` to VCS
  * installed `pre-commit` to run from `default` env
    * `pixi run pre-commit install`



#### Thu 22-Jan-2025

##### Miscellaneous

* emailed my comments on Tall's paper
* helped Vicente with connection problems to `nibi`


##### MOAD/docs

* continued changing to use Pixi for deps & env mgmt; PR#62
  * added `check-toml` to `.pre-commit-config.yaml`
  * added tasks for common docs work:
    * `pixi task add docs make clean html`
    * `pixi task add linkcheck make clean linkcheck`
  * added `.pixi` to `exclude_patterns` in `conf.py`
  * changed `sphinx-linkcheck` workflow to use new reusable `pixi-sphinx-linkcheck`
  * changed `.readthedocs.yaml` to use customized build process for Pixi from RTD docs
  * deleted `environment-rtd.yaml`
  * removed `moad-docs` conda env from `khawla`
  * added task to update `requirements.txt via`pip list`
    * `pixi task add update-reqs "python -m pip list --format=freeze >> requirements.txt"`
  * update `contributing.rst`
    * similar to changes in `pkg_development.rst` in `SalishSeaCmd`
  * added Pixi badges to README
* updated redirected links; PR#63



#### Fri 23-Jan-2025

##### Security Updates

* Squash-merged dependabot PRs to update `wheel` to 0.46.2 re: CVE-2026-24049
  arbitrary file permissions alteration vulnerability
  * cookiecutter-analysis-repo
  * SalishSeaNowcast
  * cookiecutter-MOAD-pypkg
  * SOG-Bloomcast
  * SOG-forcing
* updated Pixi on `khawla` to 0.63.2


##### 2x resolution SalishSeaCast

* continued work on 2xrez processing and verification notebooks:
  * adjusted row 22 tile 5
    * reviewed row 22 changes with Susan
  * added row 23 - Stories Beach to Desolation Sound
    * reviewed work needed with Susan
  * adjusted row 23 tiles 4 to 7
    * reviewed row 23 changes with Susan
  * added row 24
    * reviewed work needed with Susan
  * adjusted row 24 tiles 4 to 6
    * reviewed row 23 changes with Susan



#### Sat 24-Jan-2025

##### SalishSeaCast

* `collect_weather 2.5km 12` was still running at 11:00
  * no 12Z files downloaded
  * no 12Z files on hpfx
  * `crop_gribs 12` timed out at 11:13 with 528 files unprocessed
  * re-started `crop_gribs 12` at ~11:25
  * 12Z files started arriving at ~12:00
    * `crop_gribs 12` is seeing them
* cleaned `/SalishSeaCast/datamart/hrdps-continental/12/` with
  `fd --type f . /SalishSeaCast/datamart/hrdps-continental/12 -X rm`



#### Sun 25-Jan-2025

##### SalishSeaCast

* `collect_river_data Englishman` got empty time series




##### SalishSeaCmd TODO

* drop `NEMO-Cmd` cloning from dev docs
* finish changing dev docs re: Pixi; e.g. `pixi run hatch...`
* fix docs re: change from temporary run directory names from UUID to run id concatenated to
  microsecond resolution timestamp
  * e.g. `/scratch/dlatorne/MEOPAR/runs/01mar23-11x32_2025-12-24T145433.665751-0800`
* update scaling tests on `narval` with `StdEnv/2023`
  * 100 Gb/s InfiniBand Mellanox HDR interconnect
  * Lustre file system
  * cpus: AMD EPYC 7532 (Zen 2) @ 2.40 GHz, 256M cache L3
* add support for `rorqual`
  * 200 Gb/s HDR InfiniBand
  * Lustre file system
  * cpus: AMD EPYC 9654 (Zen 4) @ 2.40 GHz, 384MB cache L3
  * `--ntasks-per-node=24 --cpus-per-task=8` for whole nodes
* consider removing attached xios server feature
* consider removing separate deflate job feature
* change `orcinus` to use `slurm`
* drop support for `optimum`
* consider removing support for PBS/TORQUE scheduler





##### NEMO-Cmd TODO

* fix typos in README
* remove all `conda activate` mentions from docs
* fix docs re: change from temporary run directory names from UUID to run id concatenated to
  microsecond resolution timestamp
  * e.g. `/scratch/dlatorne/MEOPAR/runs/01mar23-11x32_2025-12-24T145433.665751-0800`
* update `prepare` sub-command docs to make mentions of `hg` refer more generically to version control
* update run description file docs re: references to `cedar` and `graham`
* change default for `--queue-job-cmd` from `qsub` to `sbatch`
* handle hard-coded 32 core/node; we need 192 core for new Alliance clusters




##### MOAD/docs TODO

* plan for updates re: Pixi replacing `conda/mamba`
  * `getting_started.rst`
    * change "Install Miniforge" to "Install Pixi"
  * Alliance setup in `alliance-computing.rst`
  * lots in `conda_pkg_env_mgr.rst`
    * maybe move to `zzz_archival_docs/` and replace with new Pixi section
  * lots in `analysis-repo.rst`
    * maybe not until after `cookiecutter-analysis-repo` is migrated
  * `jupyter.rst`
  * `sphinx_docs.rst`
  * `vscode.rst`
    * Fortran language server setup
  * lots in `pkg_structure.rst`




##### SalishSeaCast/docs TODO

* planned updates re: Pixi replacing `conda/mamba`
  * `netcdf4.rst`
    * change mention of Anaconda
  * `salish.rst`
    * update like `nibi.rst`
    * delete section about `stdout` and `stderr` because they are for PBS/TORQUE that we no longer use
  * `results_server/index.rst`
    * drop SalishSeaNowcast production deployment stuff
  * `anaconda_python.rst`
    * points to `conda` docs in MOAD/docs
    * update re: Pixi
  * `emacs_config.rst`
    * update mention of `$HOME/anaconda/bin`
  * `work_env/index.rst`
    * `anaconda_python`
    * `python3_conda_environment`
  * `python3_conda_environment.rst`
    * maybe delete because everything is Python 3 now
  * `work_env/salishsea_pkgs.rst`
    * directed at work for not running model; e.g. sprints; think about context
    * update like `nibi.rst`




* SalishSeaTools
  * fix failing tests!!!



* TODO:
  * add https://sphinx-copybutton.readthedocs.io/ to add copy button functionality to Sphinx code blocks
    * AtlantisCmd
    * ECget
    * NEMO-Cmd
    * NEMO_Nowcast
    * Reshapr
    * SalishSeaCmd
    * SalishSeaCast/docs
    * tools
    * SalishSeaNowcast
    * salishsea-site
    * MOAD/docs
    * moad_tools



* Migrate to `pixi`:
  * gha-workflows - done 17dec25 in PR#82
  * NEMO-Cmd - done 6jan26 in PR#121
  * SalishSeaCmd - done 13jan26 in PR#121
  * SalishSeaCast/docs - done 14jan26 in PR#74
  * MOAD/docs - done 22jan26 in PR#62

  * Reshapr
  * NEMO_Nowcast
  * AtlantisCmd
  * moad_tools
  * tools/SalishSeaTools
  * SalishSeaNowcast
  * SOG-Bloomcast-Ensemble
  * erddap-datasets
  * salishsea-site
  * SOG
  * ECget
  * analysis-doug
  * SOG-Bloomcast ??


* Python 3.14:
  * NEMO-Cmd - done 18oct25 in PR#114
  * SalishSeaCmd - done 13nov25 in PR#115
  * AtlantisCmd - done 17nov25 in PR#90
  * MOAD/docs - done 19nov in commit 8b73c7d43
  * Reshapr - done 20nov25 in PR#168
  * gha-workflows - done 17dec25 in PR#82
  * SalishSeaCast/docs - done 14jan26 in PR#74

  * workflows available for testing:
    * NEMO_Nowcast
    * moad_tools
    * tools/SalishSeaTools
    * SalishSeaNowcast
    * SOG-Bloomcast-Ensemble
    * erddap-datasets
    * salishsea-site
  * no workflows:
    * SOG
    * ECget
    * analysis-doug
    * SOG-Bloomcast ??



##### Reshapr

* update "Iona wastewater discharge analysis" example docs:
  * remove requirement for multi-day run results to be split; we can handle month-long files now
  * change note about `split-results` to use `salishsea split-results` instead of nowcast worker
* exclude test that often times out on GHA
* consider accepting `dask cluster: nibi_cluster` in extraction YAML (i.e. no extension necessary)
* `reshapr info` should handle user supplied path/file specs for cluster descriptions and model profiles
  * presence of a path element (relative or absolute) triggers file reading from somewhere other than
    in the Reshapr package directories
  * this works now for absolute paths of model profiles
  * improve `--help` information to reflect that
  * provide helpful suggestions instead of a traceback
* maybe `reshapr info` should be able to discover cluster descriptions and model profiles in the pwd
  by checking YAML files for characteristic keys
  * maybe `number of workers` for clusters and  `chunk size` for model profiles



* SalishSeaNowcast
  * `polar.ncep.noaa.gov` sometimes refuses connections from GHA `sphinx linkcheck`


* change docs to use `Pixi`
  * MOAD/docs
  * SalishSeaCast/docs
  * many/most packages dev docs
    * Reshapr


* Susan: do we want to set up Globus on `salish` or `skookum`, or engage compstaff
  to set it up for `ocean` or wider EOAS context
  * I should get to know Stephan and discuss bigger context with him



##### ERDDAP

* update to v2.29.0
  * review v2.27.0 changes because they will be included as we jump from v2.26.0


##### SalishSeaCast TODO

* backfill AGRIF runs on `orcinus` from ~14jul



##### salishsea-site

* SMELT link in nav bar has no target


##### SalishSeaNowcast

* add removal of uncropped GRIB files to `crop_gribs` to avoid storage bloat
* `FutureWarning` re: default value change for `compat` from `compat='no_conflicts'` to `compat='override'`
  in `xarray.combine_by_coords()`; issue#390
* `UserWarning`: no explicit representation of timezones available for np.datetime64
  from `figures/comparison/sandheads_winds.py:119` and `figures/comparison/sandheads_winds.py:127`
* generate a new ed25519 key for automation logins and change to use it everywhere except `optimum`
* change config to upload forcing to `nibi` instead of `graham`
  * need automation key activated on `nibi`
* change config to drop forcing uploads to `optimum`
* change automation workflow to run nowcast-green in place of nowcast-blue
  * add output of 10min avg tide gauge station files
* `supervisor` `pkg_resources` API deprecation issue
  * version 4.3.0 on PyPI contains a fix
  * conda-forge feedstock has CI failures, but it's not abandoned
* change download_weather to gather only files missed by collect_weather so that it can
  work with crop_gribs monitoring incoming files
  * check for presence of files before downloading them; skip if present





* TODO:
  * ask Henryk about email from ERDDAP
  * clean up v1.82:
    * delete `/opt/tomcat/`
    * delete `/results/erddap-1.82`
    * remove old openjdk packages ?



* Reshapr didn't recognize persistent dask cluster for Susan and gave misleading error message
  * suspect Reshapr exception type bug due to change in dask


##### erddap-datasets

* TODO:
  * add v21-11 info to forecast datasets `summary` attr
  * figure out why ERDDAP in unable to send emails
  * 2.11: add `emailDiagnosticsToErdData` setting
  * 2.19:
    * hyphens in datasetIDs are deprecated ???
  * 2.23: CF-1.10 vs. CF-1.6
    * `calendar: gregorian` is now deprecated in favour of `calendar: standard`
  * 2.25:
    * zarr support
    * Prometheus metrics
    * `Xinclude` in `datasets.xml`
    * `unusualActivityFailPercent` can be set to other than 25%
  * 2.26:
    * docs now on https://erddap.github.io/
    * `displayInfo` & `displayAttribute` tags that could be used for dataset citations on `data` pages


##### SalishSeaTools

* TODO:
  * move `sqlalchemy` import to top of module
    * make it part of package env and analysis-repo env
* update library_code section in docs or move it to MOAD docs



Refresh myself on Fortran in VS Code and on-the-fly compilation; prep to present to group.

* fortran.fortls.directories


* Update project name retrieval in `conf.py`:
  * branch: get-project-name
  <!-- markdownlint-disable MD031 -->
  ```python
  import tomllib
  from pathlib import Path

  ...

  with Path("../pyproject.toml").open("rb") as f:
      pkg_info = tomllib.load(f)
  project = pkg_info["project"]["name"]
  ```
  <!-- markdownlint-enable MD031 -->
  <!-- markdownlint-disable MD031 -->
  ```text
  Chg to project name retrieval from pyproject.toml

  Replaced the hardcoded project name with dynamic retrieval from
  `pyproject.toml` using `tomllib`. This ensures consistency and
  reduces manual updates for project metadata.
  ```
  <!-- markdownlint-enable MD031 -->
  * NEMO-Cmd  - done 16jan23 in d41f972e
  * SalishSeaCmd - done 16jan23 in 6780a1af
  * SOG-Bloomcast-Ensemble - done 15feb25 in PR#65
  * SalishSeaNowcast - done 16feb25 in PR#333
  * AtlantisCmd - done 17feb25 in PR#64
  * NEMO_Nowcast - done 17feb25 in PR#68
  * Reshapr - done 17feb25 in PR#151
  * salishsea-site - done 17feb25 in PR#109
  * moad_tools - done 17feb25 in PR#89

  * tools
  * ECget
  * SOG



TODO:

* modernize packaging:
  * Reshapr - done 30oct23 in PR#101
  * moad_tools - done 18dec23 in PR#48
  * salishsea-site - done 22apr24 in PR#78
  * NEMO_Nowcast - done 27nov24 in PR#61
  * AtlantisCmd - done 1dec24 in PR#49
  * Marlin - extract from tools and archive without modernization
  * SalishSeaTools - done 9jan25 in PR#122
  * SOG-Bloomcast-Ensemble - done 15feb25 in PR#65

  * SOG
  * ECget
  * cookiecutter-MOAD-pypkg
  * SOG-Bloomcast ??



TODO:

* review and clean up permissions in GitHub orgs


Here's the PyCharm commit message generation prompt that keeps getting overwritten by updates:

  Avoid overly verbose descriptions or unnecessary details.

  Start with a short sentence in imperative form, no more than 50 characters long.

  Then leave an empty line and continue with a more detailed explanation.

  Write only one sentence for the first part, and two or three sentences at most for the detailed explanation.


Because I can never remember how to get a git feature branch that I set aside back into working
state:

* ref: <https://www.atlassian.com/git/tutorials/merging-vs-rebasing>
* git switch feature
* git rebase main
* In PyCharm > Git > Log context menu "Rebase 'feature' onto 'main'"
* **BUT** if the changes in the feature branch overlap files in main, it's possible that
  a merge will be required


Repos that use readthedocs:

* active:
  * AtlantisCmd
  * ECget
  * NEMO-Cmd
  * NEMO_Nowcast
  * Reshapr
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
  * MoaceanParcels
  * MOHID-Cmd
  * rpn-to-gemlam
  * WWatch3-Cmd
