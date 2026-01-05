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
* storm surge alert for Strait of Georgia on morning of Sat 20dec
  * 5.17 m at 06:35 at Sandy Cove; 0 m/s E wind at Sandy Cove



#### Sat 3-Jan-2025

##### SalishSeaCast

* storm surge alert for Strait of Georgia on morning of Sat 20dec
  * 5.49 m at 07:15 at Sandy Cove; 1 m/s S wind at Sandy Cove
* manually re-ran `crop_gribs 06 2026-01-02 --backfill --debug` to backfill from yesterday's failure



#### Sun 4-Jan-2025

##### SalishSeaCast

* `collect_river_data SquamishBrackendale` got empty time series
* storm surge alert for Strait of Georgia on morning of Sat 20dec
  * 5.30 m at 07:45 at Sandy Cove; 1 m/s SSW wind at Sandy Cove







* NEMO-Cmd TODO:
  * fix docs re: change from temporary run directory names from UUID to run id concatenated to
    microsecond resolution timestamp
    * e.g. `/scratch/dlatorne/MEOPAR/runs/01mar23-11x32_2025-12-24T145433.665751-0800`
  * update `prepare` sub-command docs to make mentions of `hg` refer more generically to version control
  * update run description file docs re: references to `cedar` and `graham`
  * change default for `--queue-job-cmd` from `qsub` to `sbatch`
  * handle hard-coded 32 core/node; we need 192 core for new Alliance clusters





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

  * NEMO-Cmd
  * SalishSeaCmd
  * AtlantisCmd
  * MOAD/docs
  * Reshapr
  * SalishSeaCast/docs
  * NEMO_Nowcast
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

  * workflows available for testing:
    * SalishSeaCast/docs
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


* change docs to use `Miniforge3` and `mamba`
  * MOAD/docs
  * SalishSeaCast/docs
  * many/most packages dev docs
    * Reshapr


* Susan: do we want to set up Globus on `salish` or `skookum`, or engage compstaff
  to set it up for `ocean` or wider EOAS context
  * I should get to know Stephan and discuss bigger context with him


##### SalishSeaCmd

* change `orcinus` to use `slurm`
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
* drop support for `optimum`
* consider removing support for PBS/TORQUE scheduler


##### ERDDAP

* update to v2.28.1
  * review v2.27.0 changes because they will be included as we jump from v2.26.0


##### SalishSeaCast

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
