# 2025 Work Journal

This is my public work journal.
This journal is about:

* my work as a Research Software Engineer with Dr. Susan Allen in the
  Department of Earth, Ocean and Atmospheric Sciences at the University of British Columbia
* my open-source activities
* occasional notes about life in general


## January

### Week 1

#### Wed 1-Jan-2025

**Statutory Holiday** - New Year's Day

Goofed off


#### Thu 2-Jan-2025

##### Miscellaneous

* created 2025 work journal file
* End of 2024 releases:
  * salishsea-site


##### salishsea-site

* added no-cover pragma to version string to avoid coverage failures on version changes; PR#102
* added sections for release notes to dev docs; PR#103
* release v24.2



#### Fri 3-Jan-2025

##### Security Updates

* Squash-merged dependabot PR to update jinja2 to 3.1.5 re: CVE-2024-56201 & CVE-2024-56326 re:
  arbitrary code execution vulnerabilities
  * SOG-Bloomcast
  * cookiecutter-analysis-repo
  * MoaceanParcels
* dropped cookiecutter-analysis-repo from pre-commit.ci



#### Sat 4-Jan-2025

##### tools

* continued repo refactoring
  * PR#121
    * add pre-commit to repo
    * enable repo on pre-commit.ci
    * discovered horribly broken `I_ForcingFiles/Atmos/weather.py` module
      * mixture of tabs and spaces for indentation - fixed
      * lots of undefined variables
      * lots of statements ended with semicolons



#### Sun 5-Jan-2025

##### FUN

* renamed repo clones:
  * `FUN` for `FUN-old-webapp`
  * `FUN-cmdline` to `FUN`
* discovered that I created private `FUN` repo on GitHub at `douglatornell/FUN` on ~26dec20 from
  `FUN-cmdline` and it has commits that aren't on the clone on `lizzy` that I rsync-ed
* reverted rename of `FUN` to `FUN-cmdline`
* created PyCharm project by cloning `FUN` from GitHub
* changed default branch name from `master` to `main`
* replaced `.hgignore` with `.gitignore`
* adjusted GitHub repo settings:
  * enabled dependency graph
  * enabled dependabot vulnerability alerts with rule for low-impact alerts for dev deps dismissed
  * enabled dependabot security updates
  * enabled dependabot to run on Actions runners
  * code scanning, protection rules & secret scanning are not available due to private repo(?)
  * enabled automatic deletion of branches when PRs are merged
* got signed commits working; need to ensure that repo `user.email` matches one that GitHub knows about
* added `assign-issue-pr` workflow based on UBC-MOAD shared workflow



### Week 2

#### Mon 6-Jan-2025

##### Miscellaneous

* inaugural NEMO forum monthly seminar
  * Paul Meyers


##### erddap-datasets

* started removal of V19-05 datasets:
* PR#30:
  * marked V19-05 u, v & w day-average fields datasets as inactive in preparation
    for their removal
* restarted ERDDAP server



#### Tue 7-Jan-2025

Worked at ESB while Rita was at home

##### Security Updates

* Squash-merged dependabot PR to update setup-micromamba to 2.0.3 re: bug fixes
  * AtlantisCmd
* Squash-merged dependabot PR to update codecov-action to 5.1.2 re: bug fixes
  * AtlantisCmd


##### erddap-datasets

* continued removal of V19-05 datasets in PR#30:
  * added checklist to PR#30
  * marked V19-05 u, v & w month-average fields datasets as inactive in preparation
    for their removal
  * marked V19-05 biology day-average and month-average fields datasets as inactive in preparation
    for their removal
* restarted ERDDAP server


##### tools

* continued repo refactoring
  * PR#122 - modernize packaging
    * replaced `setup.py` with `pyproject.toml`
    * moved `coverage` config from `.coveragerc` to `pyproject.toml`


##### SalishSeaCast

* `crop_gribs 00` time out at ~22:00 with 528 files unprocessed
* `collect_weather 00` finished ~3h late



#### Wed 8-Jan-2025

##### SalishSeaCast

* early morning automation all ran successfully
* ran `crop_gribs 00 --debug` to recover from last night's time-out
  * it didn't finish before `grib_to_netcdf nowcast+` needed the files
  * re-ran `grib_to_netcdf nowcast+` manually
* `download_live_ocean` timed out at 10:55
  * re-ran at 11:12 and it timed out again at 14:13
  * persisted 7jan download via symlink
  * ran `make_live_ocean_files` to jump start automation at ~14:18


##### tools

* continued repo refactoring
  * PR#122 - modernize packaging
    * removed version pin from `arrow` dependency
    * switched to `hatch` for build system
    * moved version identifier to `salishsea_tools/__about__.py`
    * updated copyright year range to replace end year with `present`



#### Thu 9-Jan-2025

##### SalishSeaCast/docs

* scheduled sphinx-linkcheck workflow failed
  * nbviewer.org rate limiting


##### tools

* continued repo refactoring
  * PR#122 - modernize packaging - squash-merged
    * released v24.1
  * PR#123 - squash-merged
    * updated release process docs re: breaking changes file
    * added missed release date for v24.1 to breaking changes section
  * PR#124 - squash-merged
    * add Python 3.13 support
  * reviewed imports and found that the only packages that are exclusively imported in `evaltools.py`
    are `sqlalchemy` and `erddapy`
    * also realized that `cliff` can be dropped from env because the repo no longer includes SalishSeaCmd
  * PR#125 - squash-merged
    * exclude version string from coverage


##### erddap-datasets

* continued removal of V19-05 datasets in PR#30:
  * marked V19-05 biology day-average and month-average fields datasets as inactive in preparation
    for their removal
  * restarted ERDDAP server
* finally no more inotify watches limit warnings 🙋


##### SalishSeaNowcast

* successfully tested Python 3.13 environment
  * found dep pkgs that are now definitely needed by `SalishSeaTools`:
    * `et_xmlfile`
    * `openpyxl`
    * `tqdm`



#### Fri 10-Jan-2025

Worked at ESB.

##### erddap-datasets

* continued removal of V19-05 datasets in PR#30:
  * marked V19-05 physics & surface tracers day-average and month-average
    fields datasets as inactive in preparation for their removal
  * restarted ERDDAP server
  * marked V17-02 depth-averaged seasonal tracer fields dataset as inactive in
    preparation for their removal
  * marked V17-02 bathymetry & mesh mask datasets as inactive in preparation
    for their removal
  * restarted ERDDAP server
  * dropped V17-02 bathymetry mentions from summary attributes of VHFR FVCOM and
    wwatch3 datasets because they contain their own grid information and the NEMO
    bathymetry only plays a role in the creation of the forcing files for the other
    models, so it's not directly relevant
  * updated bathymetry dataset in summary attributes of rolling forecast datasets
    amd added explanation of lack of versioning
  * updated front page to remove mentions of V19-05
  * restarted ERDDAP server


##### Miscellaneous

* MOAD group mtg; see whiteboard



#### Sat 11-Jan-2025

Goofed off



#### Sun 12-Jan-2025

##### SalishSeaNowcast

* finished update to Python 3.13 in PR#302
* added dep pkgs that are now definitely needed by `SalishSeaTools` in PR#321:
  * `et_xmlfile`
  * `openpyxl`
  * `tqdm`
* updated codecov-action `file` key to `files` re: API change in PR#322


##### SalishSeaCast

* updated all repo clones on `arbutus`
  * replaced `/nemoShare/MEOPAR/nowcast-sys/nowcast-env` with new Python 3.13.1 env
* wait until after I can delete the `SalishSeaNowcast/graham-offline` branch to update `skookum` env



### Week 3

#### Mon 13-Jan-2025

##### Security Updates

* Squash-merged dependabot PRs to update virtualenv to 20.26.6 re: CVE-2024-53899 re: command
  injection vulnerability
  * cookiecutter-MOAD-pypkg
  * gha-workflows
  * SOG
  * SOG-forcing


##### gha-workflows

* updated codecov-action `file` key to `files` re: API change in PR#50
* updated repo to Python 3.13 in PR#51


##### AtlantisCmd

* updated codecov-action `file` key to `files` re: API change in PR#56
  * docs build failed due to no `sphinx.configuration` key; readthedocs config API change
    * see https://about.readthedocs.com/blog/2024/12/deprecate-config-files-without-sphinx-or-mkdocs-config/



#### Tue 14-Jan-2025

##### SalishSeaCast

* noticed that Baynes Sound AGRIF results figure generation is failing due to removal of
  `ubcSSnBathymetryV17-02` dataset from ERDDAP
  * created issue #323


##### SalishSeaTools

* dependencies cleanup in PR#126:
  * dropped `cliff` because NEMO-Cmd and SalishSeaCmd are long gone from the repo
  * dropped unnecessary `ipdb` and `jupyterlab` from test env
* cleaned up docs build env and autodoc mocks list in PR#127
* added `sphinx` stanza to `.readthedocs.yaml` re: deprecation of automatic `conf.py` file detection
  in PR#128


##### 202405 Bathymetry

* continued work on `tools/bathymetry/Process20405Bathymetry.ipynb`
  * continued refactoring west open boundary channel straightening to use `xarray` and new grid shape



#### Wed 15-Jan-2025

##### SalishSeaCast

* `download_live_ocean` timed out at 10:55
  * retried at 11:12; succeeded instantly


##### SalishSeaNowcast

* added `sphinx` stanza to `.readthedocs.yaml` re: deprecation of automatic `conf.py` file detection
  in PR#324
* started work on updating Baynes Sound AGRIF results figure re: issue #323
  * can't get figure to work in dev env



#### Thu 16-Jan-2025


##### SalishSeaNowcast

* continued work on updating Baynes Sound AGRIF results figure re: issue #323
  * eventually got figure to generate in an env similar with relevant pkgs at similar versions to
    those in production; suspect that numpy>2 is the critical difference


##### SalishSeaCast

* re-ran `make_averaged_dataset day biology|chemistry|physics 2015-06-28` after Ilias reported that
  the stored files has incorrect coordinate names; a transition to Reshapr post-processing issue


##### Miscellaneous

* answered question from Isaak Haberman @ Hakai re: ERDDAP limits



#### Fri 17-Jan-2025

Worked at ESB.

Pal Issacson joined group for 6 mo sabbatical

##### Miscellaneous

MOAD group mtg; see whiteboard


##### ERDDAP

1 message per day from ERDDAP complaining about
"java.io.IOException: User limit of inotify watches reached"

* realized that limit was set lower than last value before `skookum` OS was updated:
* set new value to take effect after next ERDDAP restart:
  <!-- markdownlint-disable MD013 -->
  ```bash
  sudo sysctl fs.inotify.max_user_watches=196608
  sudo sysctl -p
  ```
  <!-- markdownlint-enable MD013 -->


##### moad_tools

* added `sphinx` stanza to `.readthedocs.yaml` re: deprecation of automatic `conf.py` file detection
  in PR#84


##### MOAD/docs

* added `sphinx` stanza to `.readthedocs.yaml` re: deprecation of automatic `conf.py` file detection
  in PR#47


##### SalishSeaCast/docs

* added `sphinx` stanza to `.readthedocs.yaml` re: deprecation of automatic `conf.py` file detection
  in PR#60



#### Sat 18-Jan-2025

Goofed off.



#### Sun 19-Jan-2025

##### salishsea-site

* added `sphinx` stanza to `.readthedocs.yaml` re: deprecation of automatic `conf.py` file detection
  in PR#104


##### NEMO-Cmd

* added `sphinx` stanza to `.readthedocs.yaml` re: deprecation of automatic `conf.py` file detection
  in PR#98


##### NEMO_Nowcast_

* added `sphinx` stanza to `.readthedocs.yaml` re: deprecation of automatic `conf.py` file detection
  in PR#65


##### Reshapr

* added `sphinx` stanza to `.readthedocs.yaml` re: deprecation of automatic `conf.py` file detection
  in PR#147


##### SalishSeaCmd

* added `sphinx` stanza to `.readthedocs.yaml` re: deprecation of automatic `conf.py` file detection
  in PR#87


##### AtlantisCmd

* added `sphinx` stanza to `.readthedocs.yaml` re: deprecation of automatic `conf.py` file detection
  in PR#57


##### ECget

* Squash-merged dependabot PR to update jinja2 to 3.1.5 re: CVE-2024-56201 & CVE-2024-56326 re:
  arbitrary code execution vulnerabilities



### Week 4

#### Mon 20-Jan-2025

##### Security Updates

* Squash-merged dependabot PRs to update setup-micromamba to 2.0.4 re: dependency updates
  * SalishSeaNowcast
  * erddap-datasets
  * rwhite/numeric_2024
  * moad_tools
  * gha-workflows
  * AtlantisCmd
  * salishsea-site


##### erddap-datasets

* updated `setup.xml`
  * PR#30
  * drop mention of removal of V19-05 datasets
  * improve line breaks
  * diatoms -> phytoplankton
  * Moore-Maley out of bio & DO reference
  * add zooplankton ref example
    * same papers as bio & DO + Suchy, et al, 2023
  * add Suchy, et al, 2023
* restarted ERDDAP:
  <!-- markdownlint-disable MD013 -->
  ```bash
  sudo /opt/tomcat/bin/shutdown.sh
  # confirm shutdown
  sudo /opt/tomcat/bin/startup.sh
  ```
  <!-- markdownlint-disable MD013 -->



#### Tue 21-Jan-2025

Worked at ESB while Rita was at home

##### SalishSeaCast

* `collect_weather 12 2.5km` failed to collect any files
  * `sarracenia` client went off the rails at 03:13 when the server unexpectedly
    closed the connection
  * same problem with hydrometric files client
  * `crop_gribs 12` reported 528 unprocessed files at 09:54
* recovery started at 11:54:
  <!-- markdownlint-disable MD013 -->
  ```bash
  # killed collect_weather 12 2.5km
  supervisorctl -c $NOWCAST_CONFIG/supervisord.ini restart sr_subscribe-hrdps-continental
  supervisorctl -c $NOWCAST_CONFIG/supervisord.ini restart sr_subscribe-hydrometric
  collect_weather 18 2.5km
  crop_gribs 18
  download_weather 12 2.5km
  crop_gribs 12 --backfill
  ```
  <!-- markdownlint-enable MD013 -->
* mtg w/ Susan to discuss response to ONC re: `arbutus` migration


##### Miscellaneous

* mtg w/ Pål re: SalishSeaCast, NEMO and MOAD group



#### Wed 22-Jan-2025

##### Miscellaneous

* in response to email from `narval` admin about a large `.pack` file in `grid` clone on `$HOME`,
  moved `grid` clone to `$HOME/projects/def-allen/dlatorne/MEOPAR/grid/`
  * I thought I did this after an email on 19dec24, but can find no record or evidence
  * I recall trying unsuccessfully to purge or re-pack the repo clone, but can find no record or
    evidence of that either


##### SalishSeaNowcast

* finished work on updating Baynes Sound AGRIF results figure re: issue #323
  * refactored to read 17-02 bathymetry from `grid` repo clone instead of ERDDAP
  * changed to use `engine="h5netcdf"` for dataset reads
  * fixed surface fields contour levels calculation issue that arose with update to `numpy>=2`
    by using `values` property to cast `xarray.DataArray` scalars to values acceptable to
    `numpy.linspace()`


##### SalishSeaCast

* re-ran `make_averaged_dataset day biology|chemistry|physics` for 21|23|24|25|27|29jun15 after
  Ilias reported that the stored files has incorrect coordinate names; more transition to Reshapr
  post-processing issues



#### Thu 23-Jan-2025

##### Miscellaneous

* replied to email from Parker about failures in code that he copied from
  `salishsea_tools.tidetools.get_dfo_wlev()`
  * recommended `salishsea_tools.data_tools.get_chs_tides()` as alternative
* GitHub started showing me the new issues interface that includes issue type tags and sub-issues


##### tools

* created issue #129 to mark `salishsea_tools.tidetools.get_dfo_wlev()` as deprecated and recommend
  `salishsea_tools.data_tools.get_chs_tides()` as alternative
* created issue #130 to update API server URL in `salishsea_tools.data_tools.get_chs_tides()`



#### Fri 24-Jan-2025

Worked at ESB.

##### Miscellaneous

* MOAD group mtg; see whiteboard
* helped Tall with `git push` issue on `beluga`; I suspect it's the VSCode
  ssh extension problem with not connecting to ssh-agent


##### SalishSeaCast

* Wrote technical part of reply to Benoît at ONC re: arbutus changes
* Prepared for figure tests in preparation for updating production env to Python 3.13
  * inspired by `numpy>=2` issue I found while fixing Baynes Sound figure;
    need to test all figures
  * `make_plots nemo nowcast research`
    * `tracer_thalweg_and_surface_hourly`
      * `notebooks/figures/research/TestTracerThalwegAndSurfaceHourly.ipynb`
      * salinity & temperature
    * `velocity_section_and_surface`
      * `notebooks/figures/research/TestVelocitySectionAndSurface.ipynb`
    * `research_VENUS.plot_vel_NE_gridded`
      * no test notebook
      * not even a figure module
  * `make_plots nemo nowcast-green research`
    * `time_series_plots`
      * `notebooks/figures/research/TestTimeSeriesPlots.ipynb`
    * `tracer_thalweg_and_surface_hourly`
      * `notebooks/figures/research/TestTracerThalwegAndSurfaceHourly.ipynb`
      * salinity & temperature
      * biology variables
      * turbidity
  * `make_plots nemo nowcast-agrif research` - done
  * `make_plots nemo nowcast comparison`
    * `sandheads_winds`
      * `notebooks/figures/comparison/TestSandHeadsWinds.ipynb`
    * `compare_venus_ctd`
      * `notebooks/figures/comparison/TestCompareVENUS_CTD.ipynb`
    * `research_VENUS.plotdepavADCP` - keep?
      * 3 nodes
    * `research_VENUS.plottimeavADCP` - keep?
      * 3 nodes
    * `research_VENUS.plotADCP` - keep?
      * 3 nodes
  * `make_plots nemo forecast publish` and `make_plots nemo forecast2 publish`
    * `storm_surge_alerts_thumbnail`
      * `notebooks/figures/publish/TestStormSurgeAlertsThumbnailModule.ipynb`
    * `storm_surge_alerts`
      * `notebooks/figures/publish/TestStormSurgeAlertsModule.ipynb`
    * `pt_atkinson_tide`
      * `notebooks/figures/publish/TestPtAtkinsonTideModule.ipynb`
    * `compare_tide_prediction_max_ssh`
      * `notebooks/figures/publish/TestCompareTidePredictionMaxSSH.ipynb`
      * 14 locations
      * drop Halfmoon Bay and Squamish because obs have disappeared
    * `surface_current_tiles`
      * `notebooks/figures/publish/TestSurfaceCurrentTiles.ipynb`
  * `make_plots wwatch3 forecast publish` and `make_plots wwatch3 forecast2 publish`
    * `wave_height_period`
      * `notebooks/figures/wwatch3/TestWaveHeightPeriod.ipynb`
      * 2 locations
* `collect_weather 18 2.5km` failed to collect any files
  * no activity other than heartbeats in `sarracenia` logs for either HRDPS or hydrometric obs
  * no 18Z 2.5km files on hpfx or dd
  * 00Z 1km files but no 12Z 1km files on dd.alpha
* mitigation started at ~17:20:
  <!-- markdownlint-disable MD013 -->
  ```bash
  crop_gribs 18
  download_weather 00 1km
  supervisorctl -c $NOWCAST_CONFIG/supervisord.ini restart sr_subscribe-hydrometric
  collect_weather 00 2.5km 2025-01-25
  crop_gribs 00 2025-01-25
  ```
  <!-- markdownlint-enable MD013 -->



#### Sat 25-Jan-2025

##### SalishSeaCast

* Started figure tests in preparation for updating production env to Python 3.13 in PR#327
  * inspired by `numpy>=2` issue I found while fixing Baynes Sound figure;
    need to test all figures
  * `make_plots nemo nowcast research`
    * `tracer_thalweg_and_surface_hourly`
      * `notebooks/figures/research/TestTracerThalwegAndSurfaceHourly.ipynb`



#### Sun 26-Jan-2025

##### SalishSeaCast

* Continue figure tests in preparation for updating production env to Python 3.13 in PR#327
  * `make_plots nemo nowcast research`
    * `velocity_section_and_surface`
      * `notebooks/figures/research/TestVelocitySectionAndSurface.ipynb`
    * `research_VENUS.plot_vel_NE_gridded`
      * created `notebooks/figures/research/TestPlotVelNEGridded.ipynb`
      * not a figure module
  * `make_plots nemo nowcast-green research`
    * `time_series_plots`
      * `notebooks/figures/research/TestTimeSeriesPlots.ipynb`



### Week 5

#### Mon 27-Jan-2025

##### Security Updates

* Squash-merged dependabot PRs to update codecov-action to 5.3.1 re: dependency, docs & feature updates
  * gha-workflows
  * SalishSeaNowcast
  * AtlantisCmd


##### Miscellaneous

* Checked status of scheduled GHA workflows:
  <!-- markdownlint-disable MD013 -->
  ```bash
  conda activate gha-workflows
  python /media/doug/warehouse/MOAD/gha-workflows/gha_workflow_checker/gha_workflows_checker.py
  ```
  <!-- markdownlint-enable MD013 -->


##### 202405 Bathymetry

* continued work on `tools/bathymetry/Process20405Bathymetry.ipynb`
  * finished refactoring west open boundary channel straightening to use `xarray` and new grid shape



#### Tue 28-Jan-2025

Worked at ESB

Migration of FASmail to M365 Outlook was completed successfully.

##### SalishSeaCast

* Continue figure tests in preparation for updating production env to Python 3.13 in PR#327
  * `make_plots nemo nowcast comparison`
    * `sandheads_winds`
      * `notebooks/figures/comparison/TestSandHeadsWinds.ipynb`
    * `compare_venus_ctd`
      * `notebooks/figures/comparison/TestCompareVENUS_CTD.ipynb`
  * `make_plots nemo forecast publish` and `make_plots nemo forecast2 publish`
    * `storm_surge_alerts_thumbnail`
      * `notebooks/figures/publish/TestStormSurgeAlertsThumbnailModule.ipynb`
    * `storm_surge_alerts`
      * `notebooks/figures/publish/TestStormSurgeAlertsModule.ipynb`
    * `pt_atkinson_tide`
      * `notebooks/figures/publish/TestPtAtkinsonTideModule.ipynb`
    * `compare_tide_prediction_max_ssh`
      * `notebooks/figures/publish/TestCompareTidePredictionMaxSSH.ipynb`
      * 14 locations
      * drop Halfmoon Bay and Squamish because obs have disappeared



#### Wed 29-Jan-2025

##### Miscellaneous

* SharcNet seminar: Converting Python code with NumPy to run on the GPU
  * Pawel Pomorski, Waterloo
  * https://helpwiki.sharcnet.ca/wiki/Online_Seminars
  * CuPy, a library highly compatible with NumPy, which offers drop-in replacement for most NumPy
    (and SciPy) functions
    * needs memory management
  * basic techniques used to convert a NumPy program to CuPy
  * cuPyNumeric library from NVIDIA, which allows running NumPy code on the GPU with no code changes
  * GPUs have thousands of cores; appropriate for massively parallel jobs
  * GPUs have separate memory; performance cost due to bandwidth between CPU and GPU
  * eliminate explicit loops
  * example: solve 1D Poisson equation
    * tri-diagonal matrix
    * identity(), reshape() and matrix->vector->matrix dance to construct matrix without explicit loops
    * 16000 x 16000 matrix:
      * <1000 not worthwhile on GPU
      * 89 seconds on 1 core
      * speed up using OMP threads peters out at 8 threads (6.85 s) due to memory access competition
  * CuPy
    * decide what code to run on CPU, and what on GPU
    * x_gpu = cp.asarray(x_cpu)  # move from CPU to GPU
    * x_cpu = cp.asnumpy(x_gpu)  # move from GPU to CPU
    * 0.265 s
  * `nvtop` is `top` for GPUs
    * 100% GPU usage is the beginning of efficient use; want more threads than cores
  * cuPyNumeric
    * no changes to numpy code
    * install via `conda` in an `apptainer` image
    * all code runs on GPU
    * user `legate` as launcher
    * lots of weedy details
    * crashes for 32000 x 32000 test case because it exceeds GPU memory


##### 202405 Bathymetry

* paused work on `tools/bathymetry/Process20405Bathymetry.ipynb`
  * "Check continuity and Add Missed Islands" is too opaque
* wrote base double resolution 202405 bathymetry to `grid/bathymetry_double_202405.nc`


##### 2x resolution SalishSeaCast

* started work on `tools/bathymetry/Process202405-2xrezBathymetry.ipynb`


##### tools/SalishSeaTools

* started work on issue #104 re: FutureWarning from pandas re: read_csv() date_parser arg
  * figured out how to resolve the issue
  * use PyCharm AI to generate unit tests for `stormtools.load_tidal_predictions()` and tuned them
    to work



#### Thu 30-Jan-2025

##### tools/SalishSeaTools

* continued work on issue #104 re: FutureWarning from pandas re: read_csv() date_parser arg in PR#132
  * added test for bad date format
  * extended stripping of leading/trailing whitespace in `load_tidal_predictions()` to all column
    names
  * refactored time zone conversion to eliminate FutureWarning
  * didn't do `load_observations()` because it call `get_dfo_wlev()` that we know no longer works
* added GHA workflow to automatically add milestone with closest due date to issues and PRs when
  they are opened; PR#131
  * based on https://github.com/marketplace/actions/add-milestone-by-due-date
  * this is proof of principle; convert it to a reusable workflow


##### SalishSeaCast

* Continue figure tests in preparation for updating production env to Python 3.13 in PR#327
  * updated modules and test notebooks after fix for FutureWarning in `salishsea_tools.stormtools`



#### Fri 31-Jan-2025

Worked at ESB.

##### Miscellaneous

* Susan's IOS talk about her estuarine flux paper
* MOAD group mtg; see whiteboard
* triaged issues in all of our repos to assign new GitHub issue types to them
  and closed a few that were truly stale


##### SalishSeaCast

* Continue figure tests in preparation for updating production env to Python 3.13 in PR#327
  * `make_plots nemo forecast publish` and `make_plots nemo forecast2 publish`
    * `surface_current_tiles`
      * `notebooks/figures/publish/TestSurfaceCurrentTiles.ipynb`
  * `make_plots wwatch3 forecast publish` and `make_plots wwatch3 forecast2 publish`
    * `wave_height_period`
      * `notebooks/figures/wwatch3/TestWaveHeightPeriod.ipynb`
      * 2 locations



## February

<!-- markdownlint-disable MD001 -->
#### Sat 1-Feb-2025
<!-- markdownlint-enable MD001 -->

##### Miscellaneous

* updated `khawla` PyCharm to 2024.3.2


##### SalishSeaCast

* squash-merged PR#327 re: figure tests in preparation for updating production env to Python 3.13



#### Sun 2-Feb-2025

##### gha-workflows

* Added reusable workflow to automatically add current milestone to new issues and PRs; PR#54
  * based on workflow created and tested in `tools` repo PR#131
  * changed to use latest release commit hash for `benelan/milestone-action` re: security; PR#55


##### Miscellaneous

* discussed update of `https://github.com/UBC-MOAD/AIMS-Workshop/blob/master/dynmodes/dynmodes.ipynb`
  with Susan
  * written in 2013; last used in 2020
  * needs porting to Python 3


##### tools/SalishSeaTools

* updated auto-milestone action to use reusable workflow; PR#133


##### AtlantisCmd

* added auto-milestone workflow; PR#60
* updated to Python 3.13 for dev and 3.11 to 3.13 for CI testing; PR#61
* released v25.1



### Week 6

#### Mon 3-Feb-2025

##### Miscellaneous

* NEMO seminar:
  * Claire Parrott: The Role of Glacier Melt on Freshwater Dynamics in the Canadian Arctic
    * NEMO 3.4 & CGRF
  * Fred Dupont: Efforts towards NEMO4 and development plans for a contribution to the NEMO consortium
    * features:
      * most options are namelist params rather than cpp keys
      * wetting & drying, but only for sigma coordinates
        * Stephanie Taylor (DFO port modeling?) is working on W&D with ice
      * adaptive implicit vertical advection: increase time setup
      * atmospheric boundary layer
      * sub-tiling: MPI improvement
      * mixed precision
    * target is 4.2.2 in production by 2027
    * ECCC in control of NEMO-CICE interface in consortium
    * simplified LPE in both NEMO & CICE
    * consortium membership stuck on 1 FTE commitment since 2019
    * NEMO consortium is -1 on non-hydrostatic
    * both ECCC and UofA did 3.6 to 4.2.2 transition
    * NEMO 5 changes from leapfrog to Runge-Kutta stepping
* squash-merged PRs from `pre-commit autoupdate` that update `black` to 25.1.0:
  * docstrings get changed to have closing `"""` on same line as the rest of the docstring
  * NEMO_Nowcast
  * NEMO-Cmd
  * erddap-datasets
  * SalishSeaCmd
  * cookiecutter-MOAD-pypkg
  * gha-workflows
  * tools
  * salishsea-site
  * MoaceanParcels
  * Reshapr
  * moad_tools
  * SalishSeaNowcast
  * AtlantisCmd


##### AIMS-Workshop repo

* started work on updating dynamic modes notebook for Susan
  * updated default branch of `UBC-MOAD/AIMS-Workshop` repo on GitHub from `master` to `main`
  * cloned `UBC-MOAD/AIMS-Workshop` repo from GitHub in `warehouse/EOAS-teaching/`
  * started `modernize` branch and PR#1
    * added conda env
    * fixed a failing code-block in the `Ex2-DynamicModes.rst` doc file
    * added the UBC EOAS favicon to be able to commit the `_static/` directory
    * discovered that notebooks need to be converted from version 3 format and did so with
      `jupyter nbconvert`


##### MoaceanParcels

* added auto-milestone workflow; PR#56
  * does nothing because repo milestone (V22.1) due date is in the past
  * resolved by setting due date to 31dec25
* added `sphinx` stanza to `.readthedocs.yaml` re: deprecation of automatic `conf.py` file detection
  in PR#57



#### Tue 4-Feb-2025

##### AIMS-Workshop repo

* continued work on updating dynamic modes notebook for Susan
  * used `jupyter nbconvert` to update `dynmodes/dynmodes.ipynb` from nbformat 3 to 4.5
  * updated `print` statements to functions re: Python 3
  * change `xrange()` to `range()` re: Python 3
  * fixed a typo in a `plot_modes()` call
  * updated URLs in dynmodes notebook
  * for Susan:
    * alternative link to Klinck's work (multiple occurrences)
      * http://woodshole.er.usgs.gov/operations/sea-mat/klinck-html/dynmodes.html
        goes to WHOI index page
    * will the class use the notebook, the module(s), or both
      * update docs that describe `ipython` and modules use?
    * update links in `aims_allen.tex`
      * some are broken
      * all are `http://` but should be `https://`


##### SalishSeaCast

* `crop_gribs 00` timed out with 528 files unprocessed
  * consequences:
    * automation stopped
    * `collect_weather 00` finished at 06:06
    * 00 and 06 forecasts files were interleaved in `sarracenia` downloads
    * 06 and 12 forecasts downloaded by `sarracenia`
* recovery started at ~08:55:
  <!-- markdownlint-disable MD013 -->
  ```bash
  # kill crop_gribs 06
  # kill collect_weather 06 2.5km
  collect_weather 18 2.5km &
  crop_gribs 18 &
  crop_gribs 00 --backfill
  crop_gribs 06 &
  collect_weather 06 2.5km --backfill --backfill-date 2025-02-04
  # kill collect_weather 12 2.5km
  # wait for wwatch3-forecast2 run to finish
  collect_weather 12 2.5km --backfill --backfill-date 2025-02-04
  ```
  <!-- markdownlint-enable MD013 -->


##### Miscellaneous

* helped Raisha with a bad BOM issue in a `.cdl` file
* helped Vicente with old host key issue connecting to `salish`



#### Wed 5-Feb-2025

##### SalishSeaCast

* `make_turbidity_file` is still failing
  * `/results/observations/ECCC/fraser_buoy.csv` contains no obs after 2025-01-27 12:10
  * `ecget/bin/ecget fraser water quality` fails with `'NoneType' object has no attribute 'parent'`


##### AIMS-Workshop repo

* continued work on updating dynamic modes notebook for Susan
  * Susan approved PR
  * improved README
  * updated `Makefile`
  * pushed rendered docs to Susan's EOAS public web space


##### ECget

* started modernization; repo is mostly untouched since 2018, though there was a minor update in 2022
* create v25.1 milestone on GitHub
* added GHA workflows for dependabot monitoring of actions, auto-assign of issues & PRs, and auto-add
  of current milestone to new issues & PRs; PR#35
* test suite fails horribly
* traced production problem to a change in the identifier for dissolved oxygen
  * I suspect that the new instrument that was installed during the week of 20jan25 changed from
    reporting percent DO to DO in mg/l
  * fixed in PR#36
  * testing fix on `skookum` required a new conda environment, so I built a Python 3.13 one



#### Thu 6-Feb-2025

Goofed off.



#### Fri 7-Feb-2025

Worked at ESB.

##### Miscellaneous

* MOAD group mtg; see whiteboard
* PO seminar: Pål re: modeling the Arctic gyres
* VSCode 1.98 expected in early March will not support connections to legacy OS hosts:
  * `arbutus`
  * `graham`


##### erddap-datasets

* finished removal of V19-05 datasets in PR#30:
  * deleted datasets and their entries in `datasets.yaml`
* restarted ERDDAP:
  <!-- markdownlint-disable MD013 -->
  ```bash
  sudo /opt/tomcat/bin/shutdown.sh
  # confirm shutdown
  sudo /opt/tomcat/bin/startup.sh
  ```
  <!-- markdownlint-disable MD013 -->
* squash-merged PR#30



#### Sat 8-Feb-2025

Goofed off.


#### Sun 9-Feb-2025

##### FUN

* started work on modernizing codebase



### Week 7

#### Mon 10-Feb-2025

##### SalishSeaCast

* `download_live_ocean` timed out at 10:57
  * retried at 11:00; succeeded almost immediately



#### Tue 11-Feb-2025

##### ECget

* continued modernization:
  * replaced `.hgignore` with `.gitignore`; PR#38
  * modernized readthedocs config; PR#39
  * moved `environment-dev.yaml` and `requirements.txt` to `envs/` directory; PR#40


##### SalishSeaCast

* `crop_gribs 18` timed out at 16:14 with all 528 files unprocessed
  * `collect_weather 2.5km 18` finished at 17:09
  * ran `crop_gribs 18 --backfill --debug` at ~17:30


##### Security Updates

* squash-merged dependabot PRs that update `cryptography` to 44.0.1 re: CVE-2024-12797 re: OpenSSL
  vulnerability
  * cookiecutter-analysis-repo
  * SalishSeaNowcast
  * cookiecutter-MOAD-pypkg
  * AtlantisCmd
  * NEMO_Nowcast
  * moad_tools
  * NEMO-Cmd
  * SalishSeaCmd
  * salishsea-site
  * SalishSeaTools



#### Wed 12-Feb-2025


##### SalishSeaCast

* `collect_river_data ECCC HomathkoMouth` with KeyError for 2025-02-11
  * no obs since 11:20 on 10feb
* discussed figures w/ Susan
  * drop VENUS node ADCP comparison figures
  * make Squamish & Halfmoon Bay behave like Boundary Bay water level model-only figure
  * add issue to add Darrell Bay to model output for comparison with water level obs there
* `download_live_ocean` timed out at 10:59
  * retried at 11:01; succeeded almost immediately


##### sss150

* explained 2nd Narrow HADCP dataset storage to Camryn
* generated boundary files for 3-30mar23:
  * VSCode session on `skookum` in `/data/dlatorne/MEOPAR/SS-run-sets/`
    <!-- markdownlint-disable MD013 -->
    ```bash
    cd sss150
    # edit file patterns in `bdytools_ssc_to_sss150_salish.yaml`
    mamba activate bdytools
    bdytools bdytools_ssc_to_sss150_salish.yaml --bdy ssh ts uv --bdy_date0 20230303 --bdy_date1 20230330
    ```
    <!-- markdownlint-enable MD013 -->


##### 202405 Bathymetry

* continued work on `tools/bathymetry/Process20405Bathymetry.ipynb`
  * got help from Susan to understand "Check continuity and Add Missed Islands"
    * that section is the beginning of changes that are driven by 50x50 inspections done in the
      `analysis-susan/notebooks/bathymetry/lookat201702_201803d*.ipynb` notebooks
    * things seemed to go well until the section to add the Steveston Jetty where I discovered
      that the base bathymetry in that region (at least) is quite different
      * Susan traced that issue to processing for the Fraser River that she did in her version of
        Michael's bathymetry creation notebook that she didn't share with me


##### 2x resolution SalishSeaCast

* continued work on `tools/bathymetry/Process202405-2xrezBathymetry.ipynb`
  * got help from Susan:
    * north boundary: adjust 10 grid points
      * stopped because channel at north boundary looks markedly different in 2xrez



#### Thu 13-Feb-2025

##### 202405 Bathymetry

* continued work on `tools/bathymetry/Process20405Bathymetry.ipynb`
  * added Susan's Fraser River depth adjustment (CHS2 max depths instead of means) to
    `analysis-doug/notebooks/2xrez-202111/bathymetry-202405.ipynb`
  * completed the rest of the bathymetry processing steps
    * do we want to include Tall's changes at the entrance to Saanich Inlet? (elsewhere?)
      * Susan says yes


##### erddap-datasets

* discovered that V19-05 datasets were back on ERDDAP
  * perhaps an artefact of not having restarted server after merging PR#30 and switching back
    to `main` branch?
  * restarted server


##### Atlantis

* explored Raisha's suggestion of moving Salish Sea calibration & parameters repo from CSIRO Bitbucket
  to our GitHub org in light of CSIRO closing access for external collaborators



#### Fri 14-Feb-2025

Worked at ESB

##### Miscellaneous

* MOAD group mtg; see whiteboard


##### tools

* added sphinx-notfound-page extension to docs build; PR#136


##### cookiecutter-MOAD-pypkg

* docs maintenance in package recipe; PR#39
  * pinned versions of Sphinx and optional extensions
  * updated `readthedocs.yaml` to use Ubuntu 24.04 and mambaforge 23.11
  * add explicit Sphinx config to `readthedocs.yaml`
  * add sphinx-notfound-page extension



#### Sat 15-Feb-2025

##### Miscellaneous

* updated `khawla` PyCharm to 2024.3.3


##### 2x resolution SalishSeaCast

* added Susan's Fraser River depth adjustment (CHS2 max depths instead of means) to
  `analysis-doug/notebooks/2xrez-202111/bathymetry-202405-2xrez.ipynb`


##### SOG-Bloomcast-Ensemble

* modernized repo and package; PR#65
  * moved env descriptions & `requirements.txt` to `envs/` directory
  * added dependabot workflow to monitor actions versions
  * added GHA workflow to auto-assign issues & PRs
  * added GHA workflow to to run CodeQL analysis
  * added GHA workflow to to run pytest-with-coverage
  * added pre-commit config and updated coding style
  * modernized packaging
* updated to Python 3.13; PR#66
* fixed DeprecationWarning re: bs4 findAll() method; PR#67
* refactored metadata handling in CLI init; RP#68
* added `aiosmtpd` dependency to dev env to address removal of `smtpd` module from Python 3.12
  stdlib re: issue #56; PR#69


##### 2025 Bloomcast

* Prep on `khawla`:
  * modernized SOG-Bloomcast-Ensemble repo & package
  * confirmed that SOG clone is up to date
  * worked in bloomcast-dev env (Python 3.13)
    <!-- markdownlint-disable MD013 -->
    ```bash
    mkdir run/2024
    cp run/2024_bloomcast_infile.yaml run/2025_bloomcast_infile.yaml
    mv run/2024_bloomcast_infile.yaml run/2024/
    mkdir -p run/timeseries run/profiles
    ```
    <!-- markdownlint-enable MD013 -->
  * committed archive of 2024 SOG YAML infile
  * edit run/2025_bloomcast_infile.yaml
  * edit run/config/yaml
  * successfully tested run prep w/ SOG runs and publish to web disabled with
    <!-- markdownlint-disable MD013 -->
    ```bash
    python -m aiosmtpd -n -l localhost:1025
    cd run
    bloomcast ensemble -v config.yaml --debug
    ```
    <!-- markdownlint-enable MD013 -->
    * ends with:
      <!-- markdownlint-disable MD013 -->
      ```text
      INFO:bloomcast.ensemble:Skipped running SOG
      ERROR:bloomcast:[Errno 2] No such file or directory: 'timeseries/std_bio_2025_bloomcast.out_8081'
      ```
      <!-- markdownlint-enable MD013 -->
  * committed run/2025_bloomcast_infile.yaml and run/config.yaml
* Setup on salish:
  * updated SOG-Bloomcast-Ensemble clone
  * SOG clone needs to be at 55af3c2 to avoid error from Ben's post 7-Apr-2014 commits
  * created new bloomcast env: Python 3.13
  * did editable installs of SOG & SOG-Bloomcast-Ensemble
  * runs dir: /data/dlatorne/SOG-projects/SOG-Bloomcast-Ensemble/run
  * archived 2024_bloomcast* files in run/2024/
  * archived Englishman_flow Fraser_flow Sandheads_wind in run/2024/
  * archived YVR_* in run/2024/
  * archived last year's `bloom_date_evolution.log` and `bloomcast.log` in run/2024/
  * test run failed
    <!-- markdownlint-disable MD013 -->
    ```text
    ../../SOG-code-bloomcast/SOG:
      error while loading shared libraries: libgfortran.so.3:
      cannot open shared object file: No such file or directory
    ```
    <!-- markdownlint-enable MD013 -->
    * due to `salish` OS upgrade in sep25
    * did a clean build in `SOG-code-bloomcast/`
    * ran test
      * unrecognized weather description:
          `Moderate Rain,Snow`
      * bloom predictions:
          <!-- markdownlint-disable MD013 -->
          ```text
          INFO:bloomcast.ensemble:Predicted earliest bloom date is 2025-02-20
          INFO:bloomcast.ensemble:Earliest bloom date is based on forcing from 2004/2005
          INFO:bloomcast.ensemble:Predicted early bound bloom date is 2025-02-21
          INFO:bloomcast.ensemble:Early bound bloom date is based on forcing from 2009/2010
          INFO:bloomcast.ensemble:Predicted median bloom date is 2025-03-08
          INFO:bloomcast.ensemble:Median bloom date is based on forcing from 1985/1986
          INFO:bloomcast.ensemble:Predicted late bound bloom date is 2025-03-27
          INFO:bloomcast.ensemble:Late bound bloom date is based on forcing from 2005/2006
          INFO:bloomcast.ensemble:Predicted latest bloom date is 2025-04-05
          INFO:bloomcast.ensemble:Latest bloom date is based on forcing from 1998/1999
          ```
          <!-- markdownlint-enable MD013 -->
  * confirmed web page updated as expected
  * installed cron job to run at 09:30 daily



#### Sun 16-Feb-2025

##### SalishSeaNowcast

* changed to project name retrieval from `pyproject.toml`; PR#332
* added auto-milestone workflow; PR#333


##### SOG-Bloomcast-Ensemble

* fixed base env path in cronjob script


##### SalishSeaCmd

* added auto-milestone workflow; PR#90


##### NEMO-Cmd

* added auto-milestone workflow; PR#101



### Week 8

#### Mon 17-Feb-2025

**Statutory Holiday** - Family Day

##### AtlantisCmd

* changed to project name retrieval from `pyproject.toml`; PR#64


##### ERDDAP

* > 25% requests failed messages resumed:
  * group 1:
    * 45.89.148.113
    * 45.89.148.58
    * 45.93.184.164
    * arin.net VA domain registry?
  * group 2:
    * 69.176.86.127
    * 69.176.86.133
    * 69.176.86.217
    * 69.176.86.247
    *
    * 69.176.88.187
    *
    * 69.176.91.93
    * no name servers! or maybe ethr.net CA colo?


##### 2025 Bloomcast

* cron job on `salish` failed to run again
  * created ticket for compstaff
    * Henryk restarted cron process on `salish`
  * ran the cron job script manually


##### NEMO_Nowcast

* added auto-milestone workflow; 5b2693f3
* changed to project name retrieval from `pyproject.toml`; PR#68


##### 2x resolution SalishSeaCast

* worked with Susan to understand differences in north boundary channel straightening section
  * she came up with an improved straightening for the 2xrez bathymetry
* started 2xrez verification notebook
  * added plotting functions
  * did a few tiles on row 0 in south Puget Sound but stopped until we resolved the
    stippling issue
  * created row 5 tiles from south side of Juan de Fuca to Bellingham Bay
    * made notes on adjustments needed in several tiles


##### Reshapr

* added auto-milestone workflow; PR#149
* changed to project name retrieval from `pyproject.toml`; PR#151


##### Security Update

* squash-merged dependabot PR that updates `cryptography` to 44.0.1 re: CVE-2024-12797 re: OpenSSL
  vulnerability
  * Reshapr


##### salishsea-site

* added auto-milestone workflow; PR#108
* changed to project name retrieval from `pyproject.toml`; PR#109


##### moad_tools

* added auto-milestone workflow; PR#88
* changed to project name retrieval from `pyproject.toml`; PR#89


##### moad/docs

* added auto-milestone workflow; PR#48
  * no value because docs repos don't presently use milestones


##### tools

* changed CHS water level station ids for Halfmoon Bay and Squamish to `None` to fix comparison
  figure failures in SalishSeaCast automation; PR#137
  * changed to `retire-water-level-stations` branch on `skookum`
  * successfully tested `make_plots nemo forecast`
  * **WAIT** until tomorrow to merge to see if we can get rid of the `graham` offline branch



#### Tue 18-Feb-2025

Sylvia stayed overnight on her way to Victoria.

Worked at ESB while Rita was at home.


##### 2025 Bloomcast

* cron job on `salish` ran successfully
  * closed compstaff ticket


##### Miscellaneous

* updated PyCharm to 2024.3.3 on `kudu`


##### 2x resolution SalishSeaCast

* created `tools` repo PR#138 for bathymetry processing because Susan and I are both
  working on the `process-202405-bathy` branch
* continued work on 2xrez processing notebook
  * added WIP storage of final bathy file
  * added smoothing; it took ~47 minutes on `kudu`
* continued work on 2xrez verification notebook



#### Wed 19-Feb-2025

##### 2x resolution SalishSeaCast

* smoothing took ~26 minutes on `khawla`
* continued work on 2xrez verification notebook
  * factored out tile x mins/maxs for less editing in each `plot_tile()` call
  * added row 6 - Juan de Fuca, Jordan River, Saanich Inlet, boundary islands, Neptune Beach
  * added lon/lat panels to plots to help with comparison to Google Maps
* continued work on 2xrez processing notebook
  * added code to adjust specific grid cells
  * adjusted row 5 grid cells



#### Thu 20-Feb-2025

##### Miscellaneous

* uploaded 2016 forcing files to `beluga` for Tall
  <!-- markdownlint-disable MD013 -->
  ```bash
    # atmospheric/GEM2.5/operational/ops_y2016*.nc are already on beluga
  yyyy=2016; rsync -tv /results/forcing/sshNeahBay/obs/ssh_y${yyyy}*.nc \
    beluga:projects/def-allen/SalishSea/forcing/sshNeahBay/obs/
  yyyy=2016; rsync -tv /results/forcing/rivers/R202108Dailies_y${yyyy}*.nc \
    beluga:projects/def-allen/SalishSea/forcing/rivers/
  yyyy=2016; rsync -tv /results/forcing/rivers/turbidity_201906/riverTurbDaily201906_y${yyyy}*.nc \
    beluga:projects/def-allen/SalishSea/forcing/rivers/river_turb/
  yyyy=2016; rsync -tv /results/forcing/LiveOcean/boundary_conditions/LiveOcean_v201905_y${yyyy}*.nc \
    beluga:projects/def-allen/SalishSea/forcing/LiveOcean/
  ```
  <!-- markdownlint-enable MD013 -->
* emailed Peter Thompson, postdoc at SFU with advice to use xarray to access datasets from our ERDDAP


##### 2025 Bloomcast

* squash-merged 2025 prep PR#70
* Added new unrecognized weather description `Moderate Rain,Snow` to cloud fraction mapping; PR#71
* experimented with code in `bloomcast._configure_logging()` to change `matplotlib` logging level to
  `WARNING`

* TODO:
  * silence `matplotlib.font_manager` log messages


##### SalishSeaNowcast

* rebased `graham-offline` on to `main` in preparation for env update on `skookum`
* updated deployment docs; PR#334


##### SalishSeaCast

* updated all repo clones on `skookum`
  * `NEMO-3.6-code` had not been updated since Jan-2022; still had `master` as default branch
    * maybe was that way because of running `nowcast-dev`?; probably irrelevant now
    * changed default branch to `main` and pulled updates
  * switched `SalishSeaNowcast` to `graham-offline` branch
  * switched `tools` to `retire-water-level-stations`
* shut down automation:
  * killed `collect_weather 00 2.5km`
  * removed `/results/forcing/atmospheric/continental2.5/GRIB/20250221/00/`
  * killed `crop_gribs 00 --fcst-date 2025-02-21`
  * `supervisorctl shutdown`
* replaced `/SalishSeaCast/nowcast-env` with new Python 3.13.1 env
  * `mamba env remove --prefix /SalishSeaCast/nowcast-env`
  * created new env
  * install packaged
  * copied in envvars `activate.d/` and `deactivate.d/` scripts
* started automation:
  * `supervisord -c ...`
  * `collect_weather 00 2.5km`
  * `crop_gribs 00 --fcst-date 2025-02-21`
* shut down and restarted persistent dask cluster on `salish` in new env
* `crop_gribs 00` failed with TypeError and raised a FutureWarning



#### Fri 21-Feb-2025

5.1 magnitude earthquake new Sechelt at 13:26; felt it in the kitchen

##### SalishSeaNowcast

* created issue#335 re: FutureWarning in `crop_gribs` due to to non-nanosecond datetime and
  timedelta resolution in xarray=2025.1.2
* created issue#336 re: TypeError in `crop_gribs` due to addition of `engine` arg to
  `xarray.backends.api._validate_attrs()` in 2024.9.0
  * this was resolved in cfgrib=0.9.14.1
  * tried updating to cfgrib=0.9.15.0 in dev env, hoping that the issue that prompted pinning
      cfgrib=0.9.11.0 in PR#276 has been resolved
    * `crop_gribs 00` on `khawla` sort of worked; it failed after apparently successfully cropping
      9 files with:
      <!-- markdownlint-disable MD013 -->
      ```python-traceback
      KeyError: "No variable named 'lhtfl'. Variables on the dataset include
      ['time', 'step', 'surface', 'latitude', 'longitude', 'valid_time', 'slhtf']"
      ```
      <!-- markdownlint-enable MD013 -->
      * that variable is for "upward surface latent heat flux (for VHFR FVCOM)"
        * changed value in `weather.download.2.5 km.variables` config to `slhtf` and `crop_gribs 00`
          runs successfully in dev env
    * successfully ran `crop_gribs 06` on `khawla`
    * successfully ran `grib_to_netcdf forecast2` on `khawla`
    * successfully ran `upload_forcing arbutus forecast2` on `skookum`
    * successfully ran `crop_gribs 12` on `khawla`
    * NEMO forecast2 run was successful
    * `make_ww3_wind_file` failed with
      ValueError: Resulting object does not have monotonic global indexes along dimension time_counter
    * cfgrib=0.9.15.0 is not at solution:
      * it produces files in which all the the time stamps are the same; that is the issue that caused
        us to pin cfgrib=0.9.11.0 in PR#276
  * tried pinning dev env to cfgrib=0.9.11.0 and xarray=2024.7.0
      <!-- markdownlint-disable MD013 -->
      ```bash
      find /results/forcing/atmospheric/continental2.5/GRIB/20250221/00/ \
        -type f -name "*_SSC.grib2" -delete  # skookum
      crop_gribs 00  # khawla
      find /results/forcing/atmospheric/continental2.5/GRIB/20250221/06/ \
        -type f -name "*_SSC.grib2" -delete  # skookum
      crop_gribs 06  # khawla
      grib_to_netcdf forecast2  # khawla
      upload_forcing arbutus forecast2  # skookum
      ```
      <!-- markdownlint-enable MD013 -->
    * `run_NEMO forecast2` and `watch_NEMO forecast2` didn't launch on `arbutus` from automation
      so I launched them manually
    * `make_ww3_wind_file` launched and ran successfully in automation
    * had to re-run `make_ww3_current_file` manually due to overwrites of copies of NEMO velocity files
    * `run_www3 forecast2` and `watch_ww3 forecast2` launched successfully in automation
    * `make_plots nemo forecast2` ran without errors
      <!-- markdownlint-disable MD013 -->
      ```bash
      find /results/forcing/atmospheric/continental2.5/GRIB/20250221/12/ \
        -type f -name "*_SSC.grib2" -delete  # skookum
      crop_gribs 12  # khawla
      ```
      <!-- markdownlint-enable MD013 -->
* downgraded to `xarray=2024.7.0` on `skookum`
  <!-- markdownlint-disable MD013 -->
  ```bash
  grib_to_netcdf nowcast+
  upload_forcing arbutus nowcast+
  upload_forcing orcinus nowcast+
  upload_forcing optimum nowcast+
  crop_gribs 18 --backfill
  ```
  <!-- markdownlint-enable MD013 -->
  * automation worked smoothly



#### Sat 22-Feb-2025

Goofed off.



#### Sun 23-Feb-2025

##### SalishSeaNowcast

* squash-merged PR#337 re: fix for `crop_gribs`
* started to explore how to deal with GRIB2 files producing netCDF files in which all the the time
  stamps are the same (the issue that caused us to pin cfgrib=0.9.11.0 in PR#276)
  * looked at changing `crop_gribs` but decided that `grib_to_netcdf` might be the better place
    to solve the problem
  * need to run `crop_gribs 06 --backfill` with `cfgrib=0.9.15.0` and `xarray=2025.1.1` so that I
    can see what `grib_ds.step` looks like in `grib_to_netcdf`



### Week 9

#### Mon 24-Feb-2025

##### SalishSeaNowcast

* continued to explore how to deal with GRIB2 files producing netCDF files in which all the the time
  stamps are the same (the issue that caused us to pin cfgrib=0.9.11.0 in PR#276)
  * ran `crop_gribs 06 --backfill` with `cfgrib=0.9.15.0` and `xarray=2025.1.1` on `khawla`
    * in `grib_to_netcdf`:
      * `grib_ds.step = [0] * 25`
      * `grib_ds.time = 2025-02-24T06:00:00.000000000`
    * in `grib_to_netcdf` on GRIB files processed with `cfgrib=0.9.11.0` and `xarray=2027.7.0`:
      * `grib_ds.step = [ 61200000000000,  64800000000000  ..., 147600000000000]`
      * `grib_ds.time = 2025-02-23T06:00:00.000000000`
    * discovered that `grib_ds.valid_time` holds the timestamp values that we want, so refactored
      `grib_to_netcdf` to use `grib_ds.valid_time.values` instead of
      `grib_ds.time.values + grib_ds.step.values`



#### Tue 25-Feb-2025

Meeting w/ Michele Blanchet, Cardiac Rehab Dietician

##### SalishSeaCast

* manager crashed when `download_wwatch3_results forecast2` finished because checklist was cleared
  while that worker was running
  * when manager restarted it loaded the hacked version of the config that had uploads to
    `robot.graham` enabled; that caused errors from `upload_forcing`
  * corrected config and restarted manager at ~14:30
* `graham` is finally back online, with the exception of `/nearline`
  * switched to `main` branch and pull updates from GitHub
  * restarted manager to load config with `robot.graham` enabled
  * ran `upload_forcing robot.graham nowcast+ 2024-12-0[789]` and was prompted for MFA
    * emailed support to get restricted ssh access restored; fixed in <~1h!

* backfilled `upload_forcing nowcast+` to `graham`


##### Security Updates

* Squash-merged dependabot PR to update ssh-action to 1.2.1 re: feature update
  * salishsea-site



Update grib_to_netcdf to use `valid_time`

Replaced usages of `step` and `time` with `valid_time` to make our
timestamp processing compatible with non-hourly step handling that
was introduced in `cfgrib=0.9.12.0`. Adjusted preprocessing, data
array creation, and coordinate handling to align with this change.

This change removes the need for version pinning of `cfgrib=0.9.11.0`
that was introduced in PR#276. By doing that, issue #336 is resolved.



#### Wed 26-Feb-2025

Installed new gen 3 modem from Rogers; booster pod won't connect to it, but signal was strong enough
for Zwift to work okay for Susan's race.


##### SalishSeaNowcast

* FutureWarning issue #335 needs an upstream change in cfgrib to resolve; ecmwf/cfgrib#414 is
  tracking the issue there


##### SalishSeaCast

* `crop_gribs 00` timed out with 408 files unprocessed
* `collect_weather 00 2.5km` finished ~2.5h late, after `crop_gribs` timed out



#### Thu 27-Feb-2025

##### Miscellaneous

* helped Jose and Tall with getting work restarted on `graham`
* completed new UBC sexual misconduct training


##### SalishSeaCast

* explored `cfgrib`, `eccodes-python` and `ecCodes` packages in search of knowledge and a way the
  quiet the latter's excess of inconsequential messages on `stderr`

##### 2x resolution SalishSeaCast

* continued work on 2xrez verification notebook
  * added row 7 - Neah Bay to Semiahmoo Bay
* continued work on 2xrez processing notebook
  * adjusted most of row 6 grid cells


##### SalishSeaNowcast

* started testing `fix-grib-time-parsing` branch in PR#338 in production
  * updated production env to `xarray=2025.1.1` and `cfgrib-0.9.15.0`
  * killed & re-launched `crop_gribs 00`



#### Fri 28-Feb-2025

Worked at ESB after I got SalishSeaCast operational

##### SalishSeaCast

* `grib_to_netcdf forecast2` and `grib_to_netcdf nowcast+` didn't produce netCDF files with the
  expected `time_counter` values
* killed `nowcast-blue` run in progress
* Fraser River buoy web page TSL cert expired between 11:35 and 12:35
  * hacked `/data/dlatorne/SOG-projects/ECget/ecget/fraser_buoy.py` to change `DATA_URL` to http
  * obs collection succeeded at 15:35
* `nowcast-agrif` hung because I didn't upload corrected atmospheric forcing to `orcinus`
  * uploaded corrected atmospheric forcing to `orcinus`, `optimum`, and `graham`
  * re-launched `nowcast-agrif`
* `/nearline` access on `graham` was restored around 11:30, just in time for feb25 results tarball :-)


##### Miscellaneous

* uploaded 2017 forcing files to `beluga` for Tall
  <!-- markdownlint-disable MD013 -->
  ```bash
    # atmospheric/GEM2.5/operational/ops_y2017*.nc are already on beluga
  yyyy=2017; rsync -tv /results/forcing/sshNeahBay/obs/ssh_y${yyyy}*.nc \
    beluga:projects/def-allen/SalishSea/forcing/sshNeahBay/obs/
  yyyy=2017; rsync -tv /results/forcing/rivers/R202108Dailies_y${yyyy}*.nc \
    beluga:projects/def-allen/SalishSea/forcing/rivers/
  yyyy=2017; rsync -tv /results/forcing/rivers/turbidity_201906/riverTurbDaily201906_y${yyyy}*.nc \
    beluga:projects/def-allen/SalishSea/forcing/rivers/river_turb/
  yyyy=2017; rsync -tv /results/forcing/LiveOcean/boundary_conditions/LiveOcean_v201905_y${yyyy}*.nc \
    beluga:projects/def-allen/SalishSea/forcing/LiveOcean/
  ```
  <!-- markdownlint-enable MD013 -->
* MOAD group mtg; see whiteboard
* Phys Ocgy seminar: Yayla Sezginer, Tortel lab: Resolving fine-scale variability in phytoplankton
  growth and physiology with Chlorophyll fluorescence
* updated PyCharm on `kudu` to 2024.3.4


##### 2x resolution SalishSeaCast

* talked to Rich about 2xrez and sent him links to comparison and processing notebooks on GitHub


## March

<!-- markdownlint-disable MD001 -->
#### Sat 1-Mar-2025
<!-- markdownlint-enable MD001 -->

Goofed off.



#### Sun 2-Mar-2025

##### SalishSeaCast

* `nowcast-blue` stalled before 1st time step
  * connections to `arbutus` fail after authentication
  * sent email to support
  * got connected at ~12:30
    * NEMO was stalled in startup
    * eventually got things cleaned up and `nowcast-blue` started at ~13:15


##### Miscellaneous

* updated PyCharm to 2024.3.4 on `khawla`


##### 2x resolution SalishSeaCast

* continued work on 2xrez verification notebook
  * discussed row 7 - Neah Bay to Semiahmoo Bay with Susan
* continued work on 2xrez processing notebook
  * reviewed row 6 grid cell adjustments with Susan



### Week 10

#### Mon 3-Mar-2025

##### Security Updates

* Squash-merged dependabot PRs to update codecov-action to 5.4.0 re: dependency updates:
  * SalishSeaNowcast
  * AtlantisCmd
  * gha-workflows


##### SalishSeaNowcast

* squash-merged `fix-grib-time-parsing` branch; PR#338
* closed PR#311 re: `graham` offline and deleted branch
* standardized `python3 -m` to `python -m` because it's time; PR#340


##### SalishSeaCast

* backfilled `archive_tarball 2024-dec`


##### Miscellaneous

* NEMO seminar:
  * climate model downscaling for Salish Sea
  * BGC models in Hudson Bay



#### Tue 4-Mar-2025

Worked at ESB while Rita was at home.

Traveled to Sidney for SoPO.

##### SalishSeaCast

* backfilled `archive_tarball 2025-jan`


##### sss150

* generated boundary files for 3apr23 to 2may23:
  * VSCode session on `skookum` in `/data/dlatorne/MEOPAR/SS-run-sets/`
    <!-- markdownlint-disable MD013 -->
    ```bash
    # edit file patterns in `bdytools_ssc_to_sss150_salish.yaml`
    cd sss150
    mamba activate bdytools
    bdytools bdytools_ssc_to_sss150_salish.yaml --bdy ssh ts uv --bdy_date0 20230403 --bdy_date1 20230430
    # edit file patterns in `bdytools_ssc_to_sss150_salish.yaml`
    bdytools bdytools_ssc_to_sss150_salish.yaml --bdy ssh ts uv --bdy_date0 20230430 --bdy_date1 20230502
    ```
    <!-- markdownlint-enable MD013 -->


##### Atlantis

* worked with Raisha to push her `salish-sea-atlantis-model` config repo to GitHub to remove reliance
  on CSIRO Bitbucket repo that we are loosing access to
  * stalled by large files in repo history
  * TODO:
    * remind myself how to filter large files out of a repo


##### SalishSeaTools

* squash-merged PR#137 re: CHS water level station ids for Halfmoon Bay and Squamish changed to `None`
* cleaned up docstring type annotation and unreachable `return` statements in `rivertools`; PR#139


##### SalishSeaNowcast

* explored renaming `make_runoff`
  * discussed with Susan and she agrees that `make_v202111_runoff_file` should become the generic
    worker, and `make_runoff file` change to `make_v201702_runoff_file` that is specific to v201702
    bathymetry that is now only used for Baynes Sound AGRIF model config runs
  * need to accept rivers dict module as arg and handle importing it during execution instead
    of at worker module startup
  * may be able to use refactored worker for sss150 as well as SalishSeaCast



#### Wed 5-Mar-2025

##### SoPO

* Oxygen & hypoxia in BC Waters
  * Charles Hannah:
* Land Temperature & Hydrology
  * Charles Curry, Pacific Climate Impacts Consortium
    * 2024 was warmest globally, 2nd warmest in BC
    * still in a snow drought even though precip returned to normal in summer/fall
* River Discharges
  * Ian Geisbrecht, Hakai
    * with Dan Moore, UBC
    * big watersheds: Fraser, Skeena & Naas
    * small watershed are 22% of area, but 65% of glacier ice ??
    * 5 watershed types:
      * snow continental: Fraser, Skeena, Naas
      * glaciated mountain: Homathko, Wannock, Klinaklini
      * snow mountain: Oyster, Stawamus, Kitimat
      * rain mountain: WCVI: Zeballos, Tofino, Sarita
      * rain hills (northern): Yakoun, Premier (both Haida Gwai), San Josef (north VI)
* NE Pacific Temperature, Salinity, Density & Marine Heatwaves from Satellites & ARGOs
  * Tetjana Ross
* Satellite obs Chlorophyll-a, temperature & marine Heatwaves
  * Andrea Hilborn
* Coastal Upwelling/Downwelling, La Perouse time series
  * Roy Hourston
* Shore stations temperature and salinity
  * Jen Jackson
* Gwaii Haanas Marine monitoring
  * Lynn Lee
* BC Shelf Mooring program
  * Cynthia Bluteau
    * taking over program from Charles
    * primarily showed Scott2 and EO1 moorings
    * post-blob cooling ended in 2024, temperatures rising
    * after 3 years in a row, summer hypoxia at Scott2 is now a feature, not a bug
    * **good contact for mooring obs** some in SoG, improving data access
* Climate Variability from 2km ocean model
  * Amber Holdsworth
    * NEP36-CanOE
* Currents and Temperature off the BC Coastal
  * Guoqi Han
* OA dynamics in the near-Shore
  * Wiley Evans, Hakai
* Nutrients & phytos on line P
  * Angelica Peña
    * 1500 km long transect
    * 1956-1981 by measurements from weather ships
    * 1982-now research cruises
    * 2019-now gliders
* Phyto biomass & community composition in northern SoG & central Coast
  * Justin Del Bel Belluz, Hakai
* West Coast zooplankton
  * Akash Sastri
* Kelp
  * Sandie Hankewich
    * huge economic importance as dependent species
* Olympia Oyster index monitoring site
  * Erin Herder
    * only endemic oyster in BC
    * species of special interest under SARA
* Tsawout First Nation Dungeness Crab Stewardship
  * Lais Chaves, Tsawout First Nation
* eDNA metabarcoding
  * Emily Rubidgem, Kristen Westfall
    * eDNA == environmental DNA; material shed by organisms into environment
    * rapid biodiversity assessments


##### SalishSeaNowcast

* continued work on updating NowcastWorker mocks in unit tests; issue #81



#### Thu 6-Mar-2025

##### SoPO

* Continuous plankton recorders (CPR)
  * Clare Ostle
* Deep-Sea Maps
  * Cherisse DuPreez
* Pelagic Fish, primarily Pacific Herring
  * Jennifer Boldt
    * herring increase since 2010 continues
    * some anchovies
    * few sardines
* Juvenile Salmon on the Shelf
  * Jackie King
    * summer
      * chum dominate
      * sockeye mainly in Queen Charlotte Sound on their out-migration
* Groundfish
  * Jillian Dunic, Sean Anderson
* Pacific Hake
  * Stéphane Gauthier
* Seabirds
  * Mark Hipfner
* Haro Strait bird counts
  * Douglas Bertram
* Stellar Sea Lions
  * Strahan Tucker
* Offshore Killer Whale (OKW) diet specialization
  * Brianna Wright
    * discovered in 1988; rarely seen
    * ~300 individuals; large groups of ~50
    * feed on sharks and salmon
* Gray Whale collaboration w/ Mexico & USA
  * Paul Cottrell
* West Coast BC Distributed Biological Observatory (DBO)
  * Kohen Bauer, Eddy Carmac, ONC
    * Salish Sea observing workshop in summer
* Marine biotoxins
  * Andrew Ross
* Salish Sea Temperature, Salinity & O2
  * Jenn Jackson
* Gulf of Alaska ecosystem status
  * Bridget Ferriss, NOAA
* SoG spring bloom and summer productivity
  * Susan Allen
* SoG conditions and HABs
  * Svetlana Esenkulova, Rich Pawlowicz, PSF, UBC
* Salish Sea Soundscape monitoring
  * Rianna Burnham, Svein Vagle, Max Lauch
* SoG zooplankton
  * Kelly Young

Talked with David Dick of Quentol,Yen Wsanec Marine Guardians, manager of program that I worked
with Dan Baker and EMSA on to use SalishSeaCast currents for vessel ground-speed monitoring via AIS


##### SalishSeaNowcast

* continued work on updating NowcastWorker mocks in unit tests; PR#81


##### Miscellaneous

* Started to upload 2018 forcing files to `beluga` for Tall
  <!-- markdownlint-disable MD013 -->
  ```bash
    # atmospheric/GEM2.5/operational/ops_y2018*.nc are already on beluga
  yyyy=2018; rsync -tv /results/forcing/sshNeahBay/obs/ssh_y${yyyy}*.nc \
    beluga:projects/def-allen/SalishSea/forcing/sshNeahBay/obs/
  ```
  <!-- markdownlint-enable MD013 -->
  * rivers upload stalled



#### Fri 7-Mar-2025

##### SalishSeaCast

* no obs from any of the USGS rivers


##### SalishSeaNowcast

* finished work on updating NowcastWorker mocks in unit tests; issue #81; PR#343


##### Miscellaneous

* finished uploading 2018 forcing files to `beluga` for Tall
  <!-- markdownlint-disable MD013 -->
  ```bash
    # atmospheric/GEM2.5/operational/ops_y2018*.nc are already on beluga
  yyyy=2018; rsync -tv /results/forcing/sshNeahBay/obs/ssh_y${yyyy}*.nc \
    beluga:projects/def-allen/SalishSea/forcing/sshNeahBay/obs/
  yyyy=2018; rsync -tv /results/forcing/rivers/R202108Dailies_y${yyyy}*.nc \
    beluga:projects/def-allen/SalishSea/forcing/rivers/
  yyyy=2018; rsync -tv /results/forcing/rivers/turbidity_201906/riverTurbDaily201906_y${yyyy}*.nc \
    beluga:projects/def-allen/SalishSea/forcing/rivers/river_turb/
  yyyy=2018; rsync -tv /results/forcing/LiveOcean/boundary_conditions/LiveOcean_v201905_y${yyyy}*.nc \
    beluga:projects/def-allen/SalishSea/forcing/LiveOcean/
  ```
  <!-- markdownlint-enable MD013 -->


##### Security Updates

* Squash-merged dependabot PRs to update jinja2 to 3.1.6 re: CVE-2025-27516 re:
  arbitrary code execution vulnerability
  * SalishSeaNowcast
  * salishsea-site
  * ECget
  * SOG-Bloomcast-Ensemble


##### PythonNotes

* started work on notebook about matching obs in Pandas dataframe with field
  values from ERDDAP



#### Sat 8-Mar-2025

##### SalishSeaCast

* no obs from Skagit River
* `download_live_ocean` timed out out at 10:57
  * restarted at 12:13 and it succeeded immediately



#### Sun 9-Mar-2025

##### SalishSeaCast

* `download_live_ocean` timed out out at 11:54
  * restarted at ~13:20 and it failed again at 16:19
  * restarted again at 16:58; more 404s, so gave up and killed it
  * persisted 8mar download via symlink
  * ran `make_live_ocean_files` to jump start automation at ~17:15


##### PythonNotes

* finished notebook about matching obs in Pandas dataframe with field values from ERDDAP



### Week 11

#### Mon 10-Mar-2025

##### SalishSeaCast

* LiveOcean/20250309/ was available at 19:14 yesterday
  * backfilled `download_live_ocean` and `make_live_ocean_files`
* workers were slow to launch and ERDDAP was at >400% CPU and >50% RAM
  * killed ERDDAP and workers started to work
    * most requests in the past 24h from 90.127.41.108 == lfbn-idf1-1-2113-108.w90-127.abo.wanadoo.fr
* Fraser River buoy web page TSL cert was renewed on 7mar
  * removed hack from `/data/dlatorne/SOG-projects/ECget/ecget/fraser_buoy.py`
    that changed `DATA_URL` to http


##### SalishSeaNowcast

* finished dropping VENUS node ADCP figures because the obs collection code has never been ported
  from Matlab; nobody cares enough; PR#344


##### Security Updates

* Squash-merged dependabot PR to update ssh-action to 1.2.2 re: feature & docs updates
  * salishsea-site



#### Tue 11-Mar-2025

##### SalishSeaCast

* `upload_forcing graham nowcast+` failed with an SSH protocol banner read error
  * manual re-try failed initially; succeeded later in the day


##### 2025 Bloomcast

* prep failed due to no new wind data


##### PythonNotes

* started notebook about scaling matching of obs in Pandas dataframe with field values from ERDDAP
  * sorting the obs dataframe on `time` takes advantage of file system caching on server to provide
    some speedup
  * `dask.DataFrame` does nothing to parallelize the processing



#### Wed 12-Mar-2025

##### Security Updates

* squash-merged dependabot PR that updates `cryptography` to 44.0.1 re: CVE-2024-12797 re: OpenSSL
  vulnerability
  * cookiecutter-djl-pypkg
* Squash-merged dependabot PRs to update jinja2 to 3.1.6 re: CVE-2025-27516 re:
  arbitrary code execution vulnerability
  * cookiecutter-djl-pypkg
  * cookiecutter-MOAD-pypkg
  * MOAD/docs
  * moad_tools
  * erddap-datasets
  * NEMO-Cmd
  * SalishSeaCast/docs
  * SalishSeaCmd
  * tools/SalishSeaTools
  * SalishSeaCast/SOG


##### 2025 Bloomcast

* prep failed due to no new wind data


##### SalishSeaCast

* `upload_forcing orcinus turbidity` failed with an SSH protocol banner read error
  * manual re-try succeeded


##### SalishSeaNowcast

* renamed `make_*runoff_file` workers to make 201702 for `nowcast-agrif` the special one, and the
  one we now use for everything else the one that will become generic after some refactoring to
  handle bathymetry as a CLI arg/option; PR#345
  * deployed branch on `skookum` for testing
  * restarted manager to load updated config and `next_workers` module



#### Thu 13-Mar-2025

##### 2025 Bloomcast

* prep failed due to no new wind data
* debugging on `khawla`:
  * last wind data date at ~10:15 is 2025-03-11; i.e. ECCC wind obs aren't updating for previous day
    before we try to run at 09:30
  * wateroffice web page table layout has changed from 4 columns to 5
  * successfully hacked code to:
    * suppress noisy info and debug messages from matplotlib
    * successfully process rivers obs
    * calculate an 11mar25 bloom date forecast



#### Fri 14-Mar-2025

##### SalishSeaNowcast

* squash-merged PR#345 re: renamed `make_*runoff_file` workers to make 201702 for `nowcast-agrif`
  the special one, and the one we now use for everything else the one that will become generic after
  some refactoring to handle bathymetry as a CLI arg/option
* released v25.1


##### Miscellaneous

* MOAD group mtg; see whiteboard
* Phys Ocgy seminar: Patagonia field school
* read the Real Python `asyncio` tutorial
  * unclear if it will work for concurrent ERDDAP obs matching or if `xarray.open_dataset()`
    will block
  * `xarray.open_dataset()` blocks, so strike the `asyncio` approach



#### Sat 15-Mar-2025

Goofed off



#### Sun 16-Mar-2025

Goofed off



### Week 12

#### Mon 17-Mar-2025

##### Miscellaneous

* Checked status of scheduled GHA workflows:
  <!-- markdownlint-disable MD013 -->
  ```bash
  mamba activate gha-workflows
  python /media/doug/warehouse/MOAD/gha-workflows/gha_workflow_checker/gha_workflows_checker.py
  ```
  <!-- markdownlint-enable MD013 -->


##### gha-workflows

* add SalishSeaCast/tools to list of repos for checking
* add 43ravens/ECget to list of repos for checking


##### Security Updates

* tightened GitHub Actions permission as recommended in
  https://semgrep.dev/blog/2025/popular-github-action-tj-actionschanged-files-is-compromised/
  * SalishSeaCast org:
    * `UBC-MOAD/gha-workflows/*`
    * `benelan/milestone-action`
    * `mamba-org/setup-micromamba`
    * `appleboy/ssh-action`  # used in salishsea-site deployment workflow
  * UBC-MOAD org:
    * `benelan/milestone-action`
    * `mamba-org/setup-micromamba`
  * 43ravens org:
    * `UBC-MOAD/gha-workflows/*`
    * `benelan/milestone-action`
    * `mamba-org/setup-micromamba`
  * SS-Atlantis org:
    * `UBC-MOAD/gha-workflows/*`
    * `benelan/milestone-action`
    * `mamba-org/setup-micromamba`



#### Tue 18-Mar-2025

Worked at ESB while Rita was at home

##### Atlantis

* hangout with Raisha to migrate SSAM repo from CSIRO Bitbucket to our SS-Atlantis GitHub org
  * tried unsuccessfully to preserve history by using `git-filter-repo` to remove large
    files from history
  * Raisha populated a new repo from her working copy from Bitbucket, curating as she went
* invited Javier to SS-Atlantis org


##### Miscellaneous

* EOAS colloquium: Isla Myers-Smith, Forestry re: Arctic tundra ecosystem responses


##### Security Updates

* Squash-merged dependabot PRs to update jinja2 to 3.1.6 re: CVE-2025-27516 re:
  arbitrary code execution vulnerability
  * SOG-Bloomcast
  * cookiecutter-analysis-repo
  * MoaceanParcels
  * Reshapr
  * AtlantisCmd
* updated lists of allows actions after failures showed that I had patterns too tight
  * SalishSeaCast org:
    * `UBC-MOAD/gha-workflows/*`
    * `benelan/milestone-action@*`
    * `mamba-org/setup-micromamba@*`
    * `appleboy/ssh-action@*`  # used in salishsea-site deployment workflow
  * UBC-MOAD org:
    * `benelan/milestone-action@*`
    * `mamba-org/setup-micromamba@*`
  * 43ravens org:
    * `UBC-MOAD/gha-workflows/*`
    * `benelan/milestone-action@*`
    * `mamba-org/setup-micromamba@*`
  * SS-Atlantis org:
    * `UBC-MOAD/gha-workflows/*`
    * `benelan/milestone-action@*`
    * `mamba-org/setup-micromamba@*`


##### SalishSeaNowcast

* continued work on replacing mock loggers in tests with caplog re: issue #82
  * branch: caplog-fixture



#### Wed 19-Mar-2025

Yesterday's UBC email problems on `kudu` turn out to be an actual ongoing outage; resolved around noon

##### Atlantis

* added Apache license file to SSAM repo and updated README
* worked with Raisha to get an image that GitHub would accept (square and <1M>) for the org


##### SOG-Bloomcast-Ensemble

* created issue #73 re: wateroffice web page table layout change from 4 columns to 5



#### Thu 20-Mar-2025

##### SalishSeaCast

* `manager` crashed and restarted at 04:23 due to KeyError on `WWATCH3 run`
  * caused by checklist clearance  just before `download_wwatch3_results forecast2` finished
* deleted ingress security group rule on `arbutus` for ports 5580-5587 that were used for VHFR-FVCOM
  runs preparation


##### Miscellaneous

* ONC annual survey


##### 2x resolution SalishSeaCast

* continued work on 2xrez processing notebook
  * adjusted most of row 7 grid cells
* continued work on 2xrez verification notebook
  * added row 8 - Neah Bay to Surrey


##### sss150

* generated boundary files for 3may23 to 2jul23:
  * VSCode session on `skookum` in `/data/dlatorne/MEOPAR/SS-run-sets/`
    <!-- markdownlint-disable MD013 -->
    ```bash
    # edit file patterns in `bdytools_ssc_to_sss150_salish.yaml`
    cd sss150
    mamba activate bdytools
    bdytools bdytools_ssc_to_sss150_salish.yaml --bdy ssh ts uv --bdy_date0 20230503 --bdy_date1 20230530
    # edit file patterns in `bdytools_ssc_to_sss150_salish.yaml`
    bdytools bdytools_ssc_to_sss150_salish.yaml --bdy ssh ts uv --bdy_date0 20230531 --bdy_date1 20230602
    # edit file patterns in `bdytools_ssc_to_sss150_salish.yaml`
    bdytools bdytools_ssc_to_sss150_salish.yaml --bdy ssh ts uv --bdy_date0 20230603 --bdy_date1 20230629
    # edit file patterns in `bdytools_ssc_to_sss150_salish.yaml`
    bdytools bdytools_ssc_to_sss150_salish.yaml --bdy ssh ts uv --bdy_date0 20230630 --bdy_date1 20230702
    ```
    <!-- markdownlint-enable MD013 -->


##### SalishSeaNowcast

* started removal of VHFR-FVCOM runs from automation and repository
  * branch: drop-vhfr-fvcom
  * PR#347
  * dropped worker:
    * `make_fvcom_boundary`



#### Fri 21-Mar-2025

Worked at ESB

##### SalishSeaCast

* ONC VENUS central and east node CTD data streams resumed


##### SalishSeaNowcast

* created PR#347 for removal of VHFR-FVCOM runs from automation and repository
  * branch: drop-vhfr-fvcom
* continued work on replacing mock loggers in tests with caplog re: issue #82
  * branch: caplog-fixture


##### Miscellaneous

* MOAD group mtg; see whiteboard
* Phys Ocgy seminar: Patagonia field school
* updated PyCharm to 2024.3.5 on `kudu`



#### Sat 22-Mar-2025

##### FUN

* continued work on modernizing codebase



#### Sun 23-Mar-2025

##### FUN

* finished initial modernization of codebase; PR#8
  * test suite runs without errors
  * forecast script runs successfully, though the UI code needs work


##### 2x resolution SalishSeaCast

* continued work on 2xrez processing notebook
  * reviewed row 7 grid cell adjustments with Susan
* continued work on 2xrez verification notebook
  * discussed row 8 - Neah Bay to Surrey with Susan



### Week 13

#### Mon 24-Mar-2025

##### 2x resolution SalishSeaCast

* continued work on 2xrez processing notebook
  * adjusted row 8 grid cells
* continued work on 2xrez verification notebook
  * added row 9 - Carmanah Point to Fraser River
* realized that I have misnumbered the rows; rows 5-9 are actually 9-14



#### Tue 25-Mar-2025

##### SalishSeaCast

* `collect_river_data ECCC` failed
  * `sarracenia` client reported "server unexpectedly closed connection" at 2025-03-23 20:02:03
    and did not recover; all messages since are "EOF in violation of protocol"
  * restarted `sarracenia` client at 08:42; files updated at 09:02
  * recovery:
    * backfill `collect_river_data ECCC` for 24mar
    * backfill `make_runoff_file` for 24mar
    * backfill `make_201702_runoff_file` for 24mar
* TWDP ferry data stream may be back but an error from the CO2 sensor is preventing file creation
  * Queen of New Westminster is on the Swartz Bay run; maybe instruments have been moved to a different
    vessel?


##### 2x resolution SalishSeaCast

* continued work on 2xrez processing notebook
  * reviewed row 8 grid cell adjustments with Susan
  * reviewed tiles 13(9),6 and 13(9),7 grid cell adjustments with Susan
  * waiting for her to finish detailed review of row 13 (9)
* continued work on 2xrez verification notebook
  * discussed row 9 - Carmanah Point to Fraser River with Susan
  * added row 14(10) - Tsusiat Point to English Bay
* changed row labels 5-9 to 9-13


##### SalishSeaNowcast

* continued removal of VHFR-FVCOM runs from automation and repository
  * branch: drop-vhfr-fvcom
  * PR#347
  * dropped worker:
    * `make_fvcom_atmos_forcing`
    * `upload_fvcom_atmos_forcing`
    * `make_fvcom_rivers_forcing`
    * `run_fvcom`
    * `watch_fvcom`
    * `download_fvcom_results`



#### Wed 26-Mar-2025

##### Miscellaneous

* SHARCNet webinar: Is Cython Still Relevant?
  * Tyler Collins, Brook U
  * types & complexity
  * give up some abstractions to get speed
  * changes since 2020:
    * better interfacing to Python's native typing
    * shorthand annotations to disable array bounds checking
    * optimizations for memory views, NumPy
    * the rise of LLMs
  * live demo optimization problems:
    * `%load_ext cython`  # enable cython in notebook
    * `%%cython`  # cython-ize cell
      * Jupyter does compilation behind the scenes
    * `%%cython -a`  # annotate compilation
      * naive without type annotations
      * `cimport cython`
        * `cdef int ...`
          * 1/3 faster
    * `@cython.boundscheck(False)`
    * `@cython.wraparound(False)`
    * type annotations in function signatures are a big win
      * factor of 2
    * special bindings for NumPy to optimize for memory views:
      * `cimport numpy as cnp`
      * factor of 20!
    * not everything (robust statistic) is massively improved
      * but low hanging fruit like type annotations scale
    * LLMs raise the floor level of skill
  * examples:
    * levenshtein distance: edit distance between 2 strings; dynamic programming problem on strings
    * robust statistic
    * prime sieve


##### SalishSeaCast

* Fraser River buoy data stream stopped after 2025-03-25 03:10
  * turbidity persisted on 26mar
  * tried and failed to find alternative to web scraping
* tried to understand TWDP ferry data stream
  * most instruments not operating, I think


##### SalishSeaNowcast

* continued removal of VHFR-FVCOM runs from automation and repository
  * branch: drop-vhfr-fvcom
  * PR#347
  * dropped worker options:
    * `update_forecast_datasets fvcom...`
    * `ping_erddap fvcom...`



#### Thu 27-Mar-2025


##### SalishSeaCast

* Fraser River buoy data stream stopped before 2025-03-27 09:10
  * turbidity persisted on 27mar


##### SalishSeaNowcast

* continued removal of VHFR-FVCOM runs from automation and repository
  * branch: drop-vhfr-fvcom
  * PR#347
  * dropped worker options:
    * `make_plots fvcom research|publish`
  * dropped FVCOM figures from `make_plots`
  * dropped figure modules and notebooks



#### Fri 28-Mar-2025

Worked at ESB

##### Miscellaneous

* MOAD group mtg; see whiteboard
* phys ocgy seminar: Michael A, Scripps re: internal waves and ocean turbulence
* uploaded 2019 forcing files to `beluga` for Tall:
  <!-- markdownlint-disable MD013 -->
  ```bash
    # atmospheric/GEM2.5/operational/ops_y2019*.nc are already on beluga
  yyyy=2019; rsync -tv /results/forcing/sshNeahBay/obs/ssh_y${yyyy}*.nc \
    beluga:projects/def-allen/SalishSea/forcing/sshNeahBay/obs/
  yyyy=2019; rsync -tv /results/forcing/rivers/R202108Dailies_y${yyyy}*.nc \
    beluga:projects/def-allen/SalishSea/forcing/rivers/
  yyyy=2019; rsync -tv /results/forcing/rivers/turbidity_201906/riverTurbDaily201906_y${yyyy}*.nc \
    beluga:projects/def-allen/SalishSea/forcing/rivers/river_turb/
  yyyy=2019; rsync -tv /results/forcing/LiveOcean/boundary_conditions/LiveOcean_v201905_y${yyyy}*.nc \
    beluga:projects/def-allen/SalishSea/forcing/LiveOcean/
  ```
  <!-- markdownlint-enable MD013 -->
* uploaded 2020 forcing files to `beluga` for Tall:
  <!-- markdownlint-disable MD013 -->
  ```bash
  yyyy=2020; rsync -tv /results/forcing/atmospheric/GEM2.5/operational/ops_y${yyyy}*.nc
       beluga:projects/def-allen/SalishSea/forcing/atmospheric/
  yyyy=2020; rsync -tv /results/forcing/sshNeahBay/obs/ssh_y${yyyy}*.nc \
    beluga:projects/def-allen/SalishSea/forcing/sshNeahBay/obs/
  yyyy=2020; rsync -tv /results/forcing/rivers/R202108Dailies_y${yyyy}*.nc \
    beluga:projects/def-allen/SalishSea/forcing/rivers/
  yyyy=2020; rsync -tv /results/forcing/rivers/turbidity_201906/riverTurbDaily201906_y${yyyy}*.nc \
    beluga:projects/def-allen/SalishSea/forcing/rivers/river_turb/
  yyyy=2020; rsync -tv /results/forcing/LiveOcean/boundary_conditions/LiveOcean_v201905_y${yyyy}*.nc \
    beluga:projects/def-allen/SalishSea/forcing/LiveOcean/
  ```
  <!-- markdownlint-enable MD013 -->
  * discovered that I have been uploading from `/results/forcing/rivers/turbidity_201906/` instead of
    `/results/forcing/rivers/river_turb/`


##### SalishSeaNowcast

* added HTTP 400 error handling to `get_onc_ferry` worker to deal with recently appeared
  error state when sensor is reported as non-existent; PR#348



#### Sat 29-Mar-2025

Goofed off.



#### Sun 30-Mar-2025

##### Minecraft

* checked mods, etc. for releases compatible with 1.21.5:
  * sodium: yes
  * lithium: yes
  * malilib: rc1
  * minihud: rc1
  * tweakeroo: rc1
  * iris: no
  * fresh animations: no


##### SalishSeaNowcast

* squash-merged PR#348 re: HTTP 400 error handling to `get_onc_ferry` worker to deal with recently
  appeared error state when sensor is reported as non-existent
  * deployed to production


##### Miscellaneous

* finished uploading 2020 forcing files to `beluga` for Tall
  <!-- markdownlint-disable MD013 -->
  ```bash
  yyyy=2020; rsync -tv /results/forcing/rivers/river_turb/riverTurbDaily2_y${yyyy}*.nc \
    beluga:projects/def-allen/SalishSea/forcing/rivers/river_turb/
  ```
  <!-- markdownlint-enable MD013 -->



### Week 14

#### Mon 31-Mar-2025

##### Miscellaneous

* sent Slack message to Tall explaining my mistake and the need for him to change the turbidity
  file name pattern his namelist for 2020 onward


##### SalishSeaNowcast

* continued removal of VHFR-FVCOM runs from automation and repository
  * branch: drop-vhfr-fvcom
  * PR#347
  * dropped FVCOM workers from process flow diagram
  * dropped FVCOM-Cmd package from envs & setup
  * dropped OPPTools package & deps from envs & setup
  * dropped FVCOM-4.1 clone & build from production env setup
  * dropped FVCOM-VHFR-config clone & envs setup


##### SS-run-sets

* started to drop FVCOM boundary files from NEMO `file_def.xml`
  * hacked `SS-run-sets/v202111/v202111/file_def_blue.xml` on `arbutus` for testing tomorrow


##### SalishSeaCast

* `archive_tarball` failed in `rsync` phase


## April

<!-- markdownlint-disable MD001 -->
#### Tue 1-Apr-2025
<!-- markdownlint-enable MD001 -->

First time riding to UBC since 20-Aug.

##### SalishSeaCast

* investigated `archive_tarball` failure
  * it appears to be a `/nearline` mount issue on `robot.graham`
  * sent email to support


##### Miscellaneous

* Cassidy's defense and celebration


##### SalishSeaNowcast

* continued work on replacing mock loggers in tests with caplog re: issue #82
  * branch: caplog-fixture
  * PR#346



#### Wed 2-Apr-2025

##### Miscellaneous

* helped Camryn with build issue in her new `WWTP` NEMO config
  * errors from `USER ice` statements
  * suspiciously, the Susan's `WasteWater` config that Camryn is basing off lacks a cpp keys file


##### SS-run-sets

* dropped `FVCOM_[TUVW].nc` files from `v202111/file_def_blue.xml` re: SalishSeaNowcast PR#347


##### SalishSeaNowcast

* continued removal of VHFR-FVCOM runs from automation and repository
  * branch: drop-vhfr-fvcom
  * PR#347
  * change `test_split_results` to use a file not named `FVCOM_[TUVW]*.nc`
  * drop `FVCOM_*.nc` file handling from `download_results`
  * add notes to deployment docs re: end of FVCOM runs and removal of code, etc. after v25.1
    release
  * deployed branch to `arbutus` and restarted `log_aggregator` and `manager` to load updated
    config


##### ERDDAP

* stopped and restarted ERDDAP server because it was using ~81% of memory on `skookum` and most of
  the recent requests looked like spam


##### SalishSeaCast

* discovered that `make_averaged_dataset month physics` failed on Monday
  * re-ran manually, but it took 2 tries to get success
* manually touched ERDDAP flag files to get month-averaged physics and chemistry datasets to load
  March


##### SalishSeaCast_hourly_prod

* started work on `graham` runs of a new SalishSeaCast v202111 config with oxygen diagnostics from
  Tall and hourly productivity output for Sacchi to use to compare with 22-27 Aug 2024 cruise
  observations
  * created new `NEMOGCM/CONFIG/SalishSeaCast_hourly_prod` config on `graham`
    * `./makenemo -n SalishSeaCast_hourly_prod -r SalishSeaCast`
  * added `key_trdtrc` cpp key to new config because Tall said to
    * `./makenemo -n SalishSeaCast_hourly_prod add_key key_trdtrc`
  * changed to `StdEnv/2020` environment with modules required to build NEMO:
    <!-- markdownlint-disable MD013 -->
    ```bash
    module --force purge
    module load StdEnv/2020
    module load netcdf-fortran-mpi/4.6.0
    module load perl/5.30.2
    ```
    <!-- markdownlint-enable MD013 -->
  * built XIOS-2



#### Thu 3-Apr-2025

##### SalishSeaCast_hourly_prod

* continued work on `graham` runs of a new SalishSeaCast v202111 config with oxygen diagnostics from
  Tall and hourly productivity output for Sacchi to use to compare with 22-27 Aug 2024 cruise
  observations
  * built `SalishSeaCast_hourly_prod` config
    * failed in `trczdf.f90` with:
      <!-- markdownlint-disable MD013 -->
      ```text
      mpif90 -o trczdf.o -I/home/dlatorne/MEOPAR/NEMO-3.6-code/NEMOGCM/CONFIG/SalishSeaCast_hourly_prod/BLD/inc -c -fpp -r8 -O3 -assume byterecl -heap-arrays -diag-disable 6738 -I/home/dlatorne/projects/def-allen/dlatorne/MEOPAR/XIOS-2//inc  /home/dlatorne/MEOPAR/NEMO-3.6-code/NEMOGCM/CONFIG/SalishSeaCast_hourly_prod/BLD/ppsrc/nemo/trczdf.f90
      /home/dlatorne/MEOPAR/NEMO-3.6-code/NEMOGCM/CONFIG/SalishSeaCast_hourly_prod/BLD/ppsrc/nemo/trczdf.f90(174): error #6404: This name does not have a type, and must have an explicit type.   [IOM_USE]
            IF( iom_use("O2ZDF")) THEN
      ----------^
      /home/dlatorne/MEOPAR/NEMO-3.6-code/NEMOGCM/CONFIG/SalishSeaCast_hourly_prod/BLD/ppsrc/nemo/trczdf.f90(174): error #6341: A logical data type is required in this context.   [IOM_USE]
            IF( iom_use("O2ZDF")) THEN
      ----------^
      compilation aborted for /home/dlatorne/MEOPAR/NEMO-3.6-code/NEMOGCM/CONFIG/SalishSeaCast_hourly_prod/BLD/ppsrc/nemo/trczdf.f90 (code 1)
      fcm_internal compile failed (256)
      ```
      <!-- markdownlint-enable MD013 -->
    * added `key_dian` based on discussion on Slack with Susan & Tall and build succeeded
    * warnings from `stpctl.f90` should be cleaned up:
      <!-- markdownlint-disable MD013 -->
      ```text
      mpif90 -o stpctl.o -I/home/dlatorne/MEOPAR/NEMO-3.6-code/NEMOGCM/CONFIG/SalishSeaCast_hourly_prod/BLD/inc -c -fpp -r8 -O3 -assume byterecl -heap-arrays -diag-disable 6738 -I/home/dlatorne/projects/def-allen/dlatorne/MEOPAR/XIOS-2//inc  /home/dlatorne/MEOPAR/NEMO-3.6-code/NEMOGCM/CONFIG/SalishSeaCast_hourly_prod/BLD/ppsrc/nemo/stpctl.f90
      /home/dlatorne/MEOPAR/NEMO-3.6-code/NEMOGCM/CONFIG/SalishSeaCast_hourly_prod/BLD/ppsrc/nemo/stpctl.f90(198): remark #8291: Recommended relationship between field width 'W' and the number of fractional digits 'D' in this edit descriptor is 'W>=D+7'.
      9300  FORMAT(' it :', i8, ' ssh2: ', e16.10, ' Umax: ',e16.10,' Smin: ',e16.10)
      --------------------------------------^
      /home/dlatorne/MEOPAR/NEMO-3.6-code/NEMOGCM/CONFIG/SalishSeaCast_hourly_prod/BLD/ppsrc/nemo/stpctl.f90(198): remark #8291: Recommended relationship between field width 'W' and the number of fractional digits 'D' in this edit descriptor is 'W>=D+7'.
      9300  FORMAT(' it :', i8, ' ssh2: ', e16.10, ' Umax: ',e16.10,' Smin: ',e16.10)
      --------------------------------------------------------^
      /home/dlatorne/MEOPAR/NEMO-3.6-code/NEMOGCM/CONFIG/SalishSeaCast_hourly_prod/BLD/ppsrc/nemo/stpctl.f90(198): remark #8291: Recommended relationship between field width 'W' and the number of fractional digits 'D' in this edit descriptor is 'W>=D+7'.
      9300  FORMAT(' it :', i8, ' ssh2: ', e16.10, ' Umax: ',e16.10,' Smin: ',e16.10)
      -------------------------------------------------------------------------^
      /home/dlatorne/MEOPAR/NEMO-3.6-code/NEMOGCM/CONFIG/SalishSeaCast_hourly_prod/BLD/ppsrc/nemo/stpctl.f90(197): remark #8291: Recommended relationship between field width 'W' and the number of fractional digits 'D' in this edit descriptor is 'W>=D+7'.
      9200  FORMAT('it:', i8, ' iter:', i4, ' r: ',e16.10, ' b: ',e16.10 )
      ----------------------------------------------^
      /home/dlatorne/MEOPAR/NEMO-3.6-code/NEMOGCM/CONFIG/SalishSeaCast_hourly_prod/BLD/ppsrc/nemo/stpctl.f90(197): remark #8291: Recommended relationship between field width 'W' and the number of fractional digits 'D' in this edit descriptor is 'W>=D+7'.
      9200  FORMAT('it:', i8, ' iter:', i4, ' r: ',e16.10, ' b: ',e16.10 )
      -------------------------------------------------------------^
      ```
      <!-- markdownlint-enable MD013 -->
  * built `Rebuild_NEMO`
* created  `#salishseacast-hourly-productivity` channel on Slack
* created `SS-run-sets/SalishSea/djl/SalishSeaCast_hourly_prod/` and files in it:
      <!-- markdownlint-disable MD013 -->
      ```bash
      field_def.xml
      file_def.xml
      namelist.time.22aug24
      SalishSeaCast_hourly_prod.yaml
      ```
      <!-- markdownlint-enable MD013 -->
* queued 4-node test job for 1st day of interest: `22aug24-9x22`
  * initial start time assigned: 2025-04-06T08:17:26
  * updated to 2025-04-04T16:30:59
  * ran at ~22:35 and failed during NEMO initialization with:
    <!-- markdownlint-disable MD013 -->
    ```text
    In file "object_factory_impl.hpp", function "static std::shared_ptr<U> xios::CObjectFactory::GetObject(const std::basic_string<char, std::char_traits<char>, std::allocator<char>> &) [with U = xios::CField]",  line 78 -> [ id = GLS_KE, U = field ] object was not found.
    ```
    <!-- markdownlint-enable MD013 -->


##### SalishSeaCast

* yesterday's deployment of `drop-vhfr-fvcom` branch undid the fix for `get_onc_ferry`
  * switched back to `main` after day's runs completed successfully
    * restarted `log_aggregator` and `manager` to reload config and `next_workers` module
  * successfully re-ran manually on `main`


##### Miscellaneous

* helped Camryn with getting restart files for her new `WWTP` NEMO config runs



#### Fri 4-Apr-2025

Worked at ESB

##### Miscellaneous

* MOAD group mtg; see whiteboard
* helped Camryn with permissions in her `/scratch/cstang/` file space
* VSCode v1.99 broke my ability to use it on `graham` due to expiry of unsupported OS work-around
* coffee w/ Roman


##### SalishSeaCast_hourly_prod

* continued work on `graham` runs of a new SalishSeaCast v202111 config with oxygen diagnostics from
  Tall and hourly productivity output for Sacchi to use to compare with 22-27 Aug 2024 cruise
  observations
  * yesterday's XIOS error was due to changes Susan made to GLS variable output names in Sep-2024
    * fixed by edits to `field_def.xml`
  * new 22aug24 4 node run queued
    * scheduled for: 2025-04-07T04:46:37
    * started at: 2025-04-06T07:06:43
    * finished after: 53m33s


##### SalishSeaNowcast

* continued work on replacing mock loggers in tests with caplog re: issue #82
  * branch: caplog-fixture
  * PR#346



#### Sat 5-Apr-2025

Bike ride and long line to vote in civic byelection.



#### Sun 6-Apr-2025

Worked on income tax.



### Week 15

#### Mon 7-Apr-2025

##### SalishSeaCast_hourly_prod

* continued work on `graham` runs of a new SalishSeaCast v202111 config with oxygen diagnostics from
  Tall and hourly productivity output for Sacchi to use to compare with 22-27 Aug 2024 cruise
  observations
  * 23aug24 5 node run queued
    * scheduled for: 2025-04-07T20:00:00
    * started at: 2025-04-07T17:11:13
    * finished after: 37m42s
  * 24aug24 6 node run queued
    * scheduled for: 2025-04-09T10:35:27
    * updated to: 2025-04-10T14:31:11
    * updated again to: 2025-04-12T02:29:05
    * updated again to: 2025-04-10T04:50:00
    * killed after >2d on the queue because 5 node run started after 3h46m on the queue



#### Tue 8-Apr-2025

##### SalishSeaCast

* manager crashed when `download_wwatch3_results forecast2` finished because checklist was cleared
  while that worker was running
* `collect_river_data USGS` failed for all 4 rivers
  * successfully backfilled all except Snohomish at ~14:50
* re-ran `make_runoff_file` to produce better forcing for future hindcasts
* `crop_gribs 00` timed out with 528 files unprocessed
  * `collect_weather 00 2.5km` finished ~2.5h late, after `crop_gribs` timed out


##### SalishSeaNowcast

* finalized removal of VHFR-FVCOM runs from automation and repository
  * PR#347 - squash-merged
  * deployed to production after today's runs
* added handling for missing "WWATCH3 run" item in checklist; PR#349
* refactored text fixtures; PR#350
  * change from `tmpdir` to `tmp_path`
  * add some type annotations to reduce the noise from PyCharm static analysis
  * make `pytest.fixture` consistent with respect to parentheses


##### salishsea-site

* created issue#113 re: dropping VHFR-FVCOM results pages from site re: SalishSeaNowcast PR#347


##### SalishSeaCast_hourly_prod

* continued work on `graham` runs of a new SalishSeaCast v202111 config with oxygen diagnostics from
  Tall and hourly productivity output for Sacchi to use to compare with 22-27 Aug 2024 cruise
  observations
  * created comparison notebook in `analysis-doug/notebooks/SalishSeaCast_hourly_prod/` to confirm
    that new config output matches that or production run



#### Wed 9-Apr-2025

##### SalishSeaCast

* ran `crop_gribs 00 --backfill --debug` at ~07:30


##### SalishSeaCast_hourly_prod

* 24aug24 5 node run queued
  * scheduled for: 2025-04-09T19:10:59
  * updated to: 2025-04-10T03:20:00
  * started at: 2025-04-09T19:40:43
  * finished after: 36m58s


##### SalishSeaNowcast

* started researching `importlib` to figure out how to be able to use a CLI arg to specify which
  `salishsea_tools.river_yyyymm` module is imported to provide the `rivers` dict in `make_runoff_file`


##### Miscellaneous

* replied to email from Peter @ SFU re: `multiprocessing` for ERDDAP access:
  * Outlook is blocking access to his Python script attachment



#### Thu 10-Apr-2025

##### SalishSeaNowcast

* started refactoring `make_runoff_file` workers:
  * branch:refactor-make_runoff_file
  * PR#351
  * improved module-level variables data structures
  * made river names consistent with those in `nowcast.yaml` config
  * started work on restructuring `nowcast.yaml` config to put all bathymetry-specific values
    under bathy version keys; step towards adding a bathy version cli argument



#### Fri 11-Apr-2025

Worked at ESB

##### SalishSeaCast

* `collect_river_data USGS` failed for all by Nisqually
  * successfully re-ran manually for 3 missing rivers at ~11:00
  * re-ran `make_runoff_file` to backfill
* `download_live_ocean` was delayed ~2.5h


##### Miscellaneous

* MOAD group mtg; see whiteboard
* Phys Ocgy seminar: Emma Boland, British Antarctic Survey
  * North Atlantic Winds, Arctic Freshwater & the AMOC
* searched for past presentations on SalishSeaCast re: doing a Phys Ocgy seminar
  * `private-docs/presentations/CMOS-2015/Doug/NowcastAutomationFramework`
  * `private-docs/presentations/Doug/PhysOcgy-11Jan2016/`
  * `private-docs/presentations/CMOS-2017/Doug/NEMO-NowcastSoftwareAutomationFramework`
  * `private-docs/presentations/CMOS-2018/Doug/SalishSeaCast`
  * `private-docs/presentations/Doug/ECCC-Datamart-15Sep2020/`


##### SalishSeaNowcast

* continued work on replacing mock loggers in tests with caplog re: issue #82
  * branch: caplog-fixture
  * PR#346



#### Sat 12-Apr-2025

##### SalishSeaCast

* `download_live_ocean` was delayed ~2h


##### Minecraft

* checked mods, etc. for releases compatible with 1.21.5:
  * sodium: yes
  * lithium: yes
  * malilib: yes
  * minihud: yes
  * tweakeroo: yes
  * iris: no
  * fresh animations: no



#### Sun 13-Apr-2025

##### SalishSeaCast_hourly_prod

* 25aug24 5 node run queued
  * scheduled for: 2025-04-15T18:15:53
  * started at: 2025-04-15T08:53:16
  * finished after: 37m9s



### Week 16

#### Mon 14-Apr-2025

##### SalishSeaNowcast

* continued refactoring `make_runoff_file` workers:
  * branch:refactor-make_runoff_file
  * PR#351
  * finished restructuring `nowcast.yaml` config to put all bathymetry-specific values
    under bathy version keys; step towards adding a bathy version cli argument
  * added `bathy_version` arg to `make_runoff_file` worker to control selection of filename template
    string and `prop_dict` module
  * deployed to `skookum` for testing
    * restarted manager to load updated `nowcast.yaml`



#### Tue 15-Apr-2025

Worked at ESB.

##### SalishSeaCast

* `make_forcing_links forecast2` failed due to incomplete refactoring in the `refactor-make_runoff_file`
  branch being tested
  * no forecast2 runs
  * deployed fix in time for nowcast runs


##### SalishSeaNowcast

* continued refactoring `make_runoff_file` workers:
  * branch:refactor-make_runoff_file
  * PR#351
  * refactored `make_forcing_links` re: rivers config structure changes; missed this yesterday
* continued work on replacing mock loggers in tests with caplog re: issue #82
  * branch: caplog-fixture
  * PR#346


##### SalishSeaCast_hourly_prod

* 26aug24 5 node run queued
  * scheduled for: 2025-04-17T09:10:00
  * started at: 2025-04-17T05:21:07
  * timed out after: 45m at 68.2% complete


##### Miscellaneous

* reviewed Peter's `multiprocessing` code for ERDDAP-obs matching



#### Wed 16-Apr-2025

Filed 2024 income tax returns.

##### Security Updates

* Squash-merged dependabot PR to update codecov-action to 5.4.1 re: dependency updates
  * AtlantisCmd
    * new codecov-action failed due to envvar issue; maybe action or maybe GitHub


##### Miscellaneous

* Slack discussion w/ Becca re: onboarding for Griffon
* emailed Peter re: improvements to his `multiprocessing` code for ERDDAP-obs matching
  * set testing meeting for tomorrow


##### salishsea-site

* fixed typos re: Strait that Ilias reported


##### SalishSeaCast/docs

* fixed broken link in `CITATION.rst` that Ilias reported



#### Thu 17-Apr-2025

##### Miscellaneous

* zoom w/ Peter re: testing his `multiprocessing` code for ERDDAP-obs matching
  * small scale test used 5 threads on `skookum` and minimal memory bump
  * he has more work to do before he can scale on `cedar`
* Slack discussion w/ Becca re: onboarding for Griffon


##### SalishSeaCast_hourly_prod

* investigated 26aug24 run time out
  * 1473 time steps; ~68.2% complete
  * no errors in `ocean.output`
* 26aug24 5 node run re-queued with 1h walltime
  * scheduled for: 2025-04-17T16:28:56
  * started at: 2025-04-19 05:54:47
  * finished after: 38m12s


##### ERDDAP

* reviewed new installation and update docs at https://erddap.github.io/
* did test installation on `khawla`
  * in contrast to what I recall discussing with Henryk (in a now-inaccessible Slack thread)
    `tomcat` is now no longer bundled with erddap
  * Java 21 is required for ERDDAP>=2.19
  * Tomcat 10 latest version is recommended: https://tomcat.apache.org/download-10.cgi
    * downloaded and verified sha512 hash with `sha512sum`
    * unpacked tarball in `/usr/local/`
    * created `tomcat` user: `sudo useradd tomcat -s /bin/bash -p '*'`
    * changed ownership of tomcat tree: `sudo chown -R tomcat apache-tomcat-10.1.40/`
    * created `erddap` group: `sudo groupadd erddap`
    * added myself and `tomcat` to `erddap` group:
      * `sudo usermod -a -G erddap doug; sudo usermod -a -G erddap tomcat`
    * changed group of tomcat tree: `sudo chgrp -R erddap apache-tomcat-10.1.40/`
    * changed user and group permissions: `sudo chmod -R ug+rwx apache-tomcat-10.1.40/`
    * removed permissions for other: `sudo chmod -R o-rwx apache-tomcat-10.1.40/`
    * created `apache-tomcat-10.1.40/bin/setenv.sh` containing:
      <!-- markdownlint-disable MD013 -->
      ```bash
      export JAVA_HOME=/usr/lib/jvm/java-21-openjdk-amd64
      export JAVA_OPTS='-server -Djava.awt.headless=true -Xmx1500M -Xms1500M'
      export TOMCAT_HOME=/usr/local/apache-tomcat-10.1.40
      export CATALINA_HOME=/usr/local/apache-tomcat-10.1.40
      ```
      <!-- markdownlint-enable MD013 -->
    * messed around to get execute permissions on `bin/*.sh` correct
    * launched `tomcat` to test at `http://localhost:8080`:
      <!-- markdownlint-disable MD013 -->
      ```bash
      sudo su - tomcat
      /usr/local/apache-tomcat-10.1.40/bin/startup.sh
      ```
      <!-- markdownlint-enable MD013 -->
    * downloaded https://github.com/ERDDAP/erddapContent/releases/download/content1.0.0/erddapContent.zip
      * verified its md5 hash with `md5sum`
    * unpacked zip in `/usr/local/apache-tomcat-10.1.40/` and fixed ownership and permissions
    * re-logged so that my `erddap` group membership took effect
    * created `/home/tomcat/erddap/` and set ownership to `tomcat:erddap`
    * edited `/usr/local/apache-tomcat-10.1.40/content/erddap/setup.xml`:
      * `bigParentDirectory` to `/media/doug/warehouse/erddap/`
      * `emailEverythingTo`
      * `admin*`
      * `flagKeyKey`
    * downloaded https://github.com/ERDDAP/erddap/releases/download/v2.26.0/erddap.war
      * verified its md5 hash with `md5sum`
      * copied it into `/usr/local/apache-tomcat-10.1.40/webapps/` and set ownership to `tomcat:erddap`
    * server works at `http://localhost:8080/erddap/` after a few iterations of `startup.sh`, browse,
      error, check log, edit `setup.xml`



#### Fri 18-Apr-2025

**Statutory Holiday** - Good Friday

##### Minecraft

* stopped server
* did lizzy-smelt backup
* updated OS packages and auto-removed outdated packages
* rebooted
* set up 1.21.5 server
  <!-- markdownlint-disable MD013 -->
  ```bash
  mkdir ~/Games/MinecraftFabric1.21.5Server
  cd ~/Games/MinecraftFabric1.21.5Server
  curl -OJ https://meta.fabricmc.net/v2/versions/loader/1.21.5/0.16.13/1.0.3/server/jar
  pushd ~/Games/MinecraftFabric1.21.4Server
  cp banned-* eula.txt ops.json whitelist.json start.sh ../MinecraftFabric1.21.5Server/
  popd
  ```
  <!-- markdownlint-enable MD013 -->
  * edited `start.sh` to:
  <!-- markdownlint-disable MD013 -->
    ```bash
    #!/usr/bin/env bash
    java -Xmx2G -jar fabric-server-mc.1.21.5-loader.0.16.13-launcher.1.0.3.jar nogui
    ```
  <!-- markdownlint-enable MD013 -->
* launched and stopped server to create instance directories and files
  <!-- markdownlint-disable MD013 -->
  ```bash
  ./start.sh
    ...
  /stop
  ```
  <!-- markdownlint-enable MD013 -->
  * edited `server.properties` to sync with 1.21.4 settings
  * installed mods, and rsync-ed `1-20-1-25jul23` world tree:
  <!-- markdownlint-disable MD013 -->
  ```bash
  cd ~/Games/MinecraftFabric1.21.5Server/mods/
  curl -LO https://github.com/CaffeineMC/lithium/releases/download/mc1.21.5-0.16.2/lithium-fabric-0.16.2+mc1.21.5-api.jar
  cd ~/Games/MinecraftFabric1.21.5Server
  rsync -av ../MinecraftFabric1.21.4Server/1-20-1-25jul23 ./
  ```
  <!-- markdownlint-enable MD013 -->
  * downloaded and unzipped on `khawla` VanillaTweaks double shulker shells v1.3.11 datapacks
    * rsync-ed it to `Games/MinecraftFabric1.21.5Server/1-20-1-25jul23/datapacks/` and removed v1.3.9
  * launched server in `tmux`
  <!-- markdownlint-disable MD013 -->
  ```bash
  tmux new -n minecraft-server
  ./start.sh
  ```
  <!-- markdownlint-enable MD013 -->
* set up 1.21.5 client instance in MultiMC
  * created instance
  * installed fabric 0.16.13
  * downloaded and installed loader mods:
    * sodium-fabric-0.6.13+mc1.21.5.jar
    * lithium-fabric-0.16.2+mc1.21.5.jar
    * malilib-fabric-1.21.5-0.24.0-sakura.8.jar
    * minihud-fabric-1.21.5-0.35.0-sakura.7.jar
    * tweakeroo-fabric-1.21.5-0.24.0-sakura.5.jar
  * selected Java: `/usr/lib/jvm/java-21-openjdk-amd64/bin/java`
  * started and stopped client instance to populate `config/`
  * copied `minihud.json` and `tweakeroo.json` from 1.21.4 instance `config/`
  * Fresh Animations isn't available for 1.21.5 yet, though `Entity [Model|Texture] Features` are
  * downloaded and installed Vanilla Tweaks resource packs `VanillaTweaks_r503680_MC1.21.x.zip`:
    * iron bars fix
    * lower shield
    * redstone devices:
      * StickyPistonSides
      * DirectionalHoppers
      * DirectionalDispensersDroppers
      * DirectionalObservers
      * GroovyLevers
      * RedstoneWireFix
  * added server: `SADA on lizzy` at 10.0.0.81
* started game and adjusted UI:
  * FOV: 80
  * Video:
    * Brightness: Bright
    * GUI Scale: 2x
    * Weather: Fancy
    * Leaves: Fancy
  * enabled resource packs
  * Music & Sound:
    * Music: 50%
    * Show Subtitles: on
    * Directional Audio: on
  * Optional Telemetry Data
  * F3-h to enable advanced tooltips
  * used `/gamerule` to increase spawn chunks radius from 3 to 4 to keep iron farm loaded


##### SalishSeaNowcast

* squash-merged refactoring of `make_runoff_file` workers; PR#351
  * deployed `main` to production and restarted manager to ensure that updated config is loaded
* started work on changing checklist returned by `make_201702_runoff_file` so that it is a dict item
  that will consolidate with that returned by `make_runoff_file`
  * PR#352



#### Sat 19-Apr-2025

##### SalishSeaCast

* `after_update_forecast_datasets()` failed with a KeyError on `WWATCH3 run`
  * I thought I fixed this in PR#349, but that was only for `after_download_wwatch3_results()` ☹️


##### SalishSeaNowcast

* finished work on changing checklist returned by `make_201702_runoff_file` so that it is a dict item
  that will consolidate with that returned by `make_runoff_file`; PR#352
* fixed KeyError issue in `after_update_forecast_datasets()` by changing scope of `run_date` lookup;
  PR#353
* fixed issue #170 re: `collect_river_data` putting only last processed river in checklist
  * branch: collect_river_data-checklist
  * PR#354
  * plan to test in production tomorrow before merging
  * deployed branch to production and restarted manager to load `next_workers` module re: PR#353


##### SalishSeaCast_hourly_prod

* 27aug24 5 node run queued with 1h walltime
  * scheduled for: 2025-04-19T17:00:00
  * started at: 2025-04-20 03:06:31
  * finished after: 37m18s


##### FUN

* solved a circular import issue by renaming `fun` module to `fun_core`
* UI needs work, no working entry point script
  * run with `fun/FUN-forecast sample_scenario.yaml`
* set up `/home/doug/Documents/finances/FUN-scenarios/` to hold scenarios, notes, etc. privately
  outside of repo clone


#### Sun 20-Apr-2025

##### SalishSeaCast

* `after_ping_erddap()` failed with a KeyError on `WWATCH3 run`


##### SalishSeaNowcast

* test of fix for issue #170 re: `collect_river_data` putting only last processed river in checklist
  was successful in production; PR#354 squash-merged
* fixed KeyError issue in `after_ping_erddap()` by assuming that run type is `forecast2` and launching
  `make_plots` without `run-date` arg; PR#355 squash-merged and deployed with manager restart to load
  updated `next_workers` module



### Week 17

#### Mon 21-Apr-2025

**Statutory Holiday** - Easter Monday

##### Miscellaneous

* help Susan with commands to build tarballs from her exchange paper run results and rsync them to
  `graham:/nearline/`


##### FUN

* started notes file in `/home/doug/Documents/finances/FUN-scenarios/`
* started creating 2026 pension income scenario



#### Tue 22-Apr-2025

Worked at ESB.

##### SalishSeaCast

* `make_turbidity_file` failed due to insufficient obs
  * no web page updates between 03:10 and 10:10
* nowcast-agrif run stuck on `orcinus` queue
  * unclear why; other jobs are running
* `orcinus` OS and software infrastructure is going to be upgraded over the summer!


##### Security Updates

* Squash-merged dependabot PR to update codecov-action to 5.4.2 re: hotfix for OIDC token
  * SalishSeaNowcast
  * gha-workflows
  * AtlantisCmd


##### SalishSeaNowcast

* finished work on replacing mock loggers in tests with caplog re: issue #82
  * branch: caplog-fixture
  * PR#346; squash-merged
* created issue #357 re: handling noisy missing river discharge obs messages
  when `make_runoff_file` is run in preparation for forecast2 runs


##### Miscellaneous

* copied `SalishSeaCast_hourly_prod` runs results to Sacchi's portable SSD



#### Wed 23-Apr-2025

##### SalishSeaCast

* email conversation w/ Mark re: yesterday's stuck nowcast-agrif run; scheduler issue
  * `run_NEMO_agrif` failed due to no `namelist_cfg` for yesterday's run
  * re-tried yesterday's run with `make_forcing_links orcinus nowcast-agrif 2025-04-22`
    * emailed update to Mark
    * job was queued from ~10:42 to ~11:08, then started


##### Miscellaneous

* helped Tall with missing symlinks for persisted LiveOcean boundary condition files on 8-9 Ocr-2020
  on `beluga` and `graham`
* uploaded 2021 forcing files to `beluga` for Tall:
  * note the change of the `rsync` options from `tv` to `-tLv`; that is to cause symlinks to be copied
    as files
  <!-- markdownlint-disable MD013 -->
  ```bash
  yyyy=2021; rsync -tLv /results/forcing/atmospheric/GEM2.5/operational/ops_y${yyyy}*.nc \
       beluga:projects/def-allen/SalishSea/forcing/atmospheric/
  yyyy=2021; rsync -tLv /results/forcing/sshNeahBay/obs/ssh_y${yyyy}*.nc \
    beluga:projects/def-allen/SalishSea/forcing/sshNeahBay/obs/
  yyyy=2021; rsync -tLv /results/forcing/rivers/R202108Dailies_y${yyyy}*.nc \
    beluga:projects/def-allen/SalishSea/forcing/rivers/
  yyyy=2021; rsync -tLv /results/forcing/rivers/river_turb/riverTurbDaily2_y${yyyy}*.nc \
    beluga:projects/def-allen/SalishSea/forcing/rivers/river_turb/
  yyyy=2021; rsync -tLv /results/forcing/LiveOcean/boundary_conditions/LiveOcean_v201905_y${yyyy}*.nc \
    beluga:projects/def-allen/SalishSea/forcing/LiveOcean/
  ```
  <!-- markdownlint-enable MD013 -->



#### Thu 24-Apr-2025

##### Miscellaneous

* uploaded 2022 forcing files to `beluga` for Tall:
  <!-- markdownlint-disable MD013 -->
  ```bash
  yyyy=2022; rsync -tLv /results/forcing/atmospheric/GEM2.5/operational/ops_y${yyyy}*.nc \
       beluga:projects/def-allen/SalishSea/forcing/atmospheric/
  yyyy=2022; rsync -tLv /results/forcing/sshNeahBay/obs/ssh_y${yyyy}*.nc \
    beluga:projects/def-allen/SalishSea/forcing/sshNeahBay/obs/
  yyyy=2022; rsync -tLv /results/forcing/rivers/R202108Dailies_y${yyyy}*.nc \
    beluga:projects/def-allen/SalishSea/forcing/rivers/
  yyyy=2022; rsync -tLv /results/forcing/rivers/river_turb/riverTurbDaily2_y${yyyy}*.nc \
    beluga:projects/def-allen/SalishSea/forcing/rivers/river_turb/
  yyyy=2022; rsync -tLv /results/forcing/LiveOcean/boundary_conditions/LiveOcean_v201905_y${yyyy}*.nc \
    beluga:projects/def-allen/SalishSea/forcing/LiveOcean/
  ```
  <!-- markdownlint-enable MD013 -->
* updated `khawla` PyCharm to 2025.1
* UBC-DFO modeling meeting, now with ECCC/CCCma; Tall's O2 SalishSeaCast work


##### Security Updates

* Squash-merged dependabot PRs to update h11 to 0.16.0 re: CVE-2025-43859 re: request smuggling
  vulnerabilities
  * SalishSeaNowcast
  * SalishSeaCmd
  * NEMO-Cmd
  * moad_tools
  * Reshapr
  * salishsea-site
  * MoaceanParcels
  * NEMO_Nowcast
  * AtlantisCmd
  * tools
  * SOG-Bloomcast-Ensemble
  * erddap-datasets
  * FUN
* Squash-merged dependabot PR to update jinja2 to 3.1.6 re: CVE-2025-27516 re:
  arbitrary code execution vulnerability
  * NEMO_Nowcast


##### erddap-datasets

* started developing test versions of `datasets.xml` and `setup.xml` for v2.26 on `khawla`
  * branch: erddap-2.26
  * copied collection of tags in v2.00 upgrade notes into `prefix.xml`
    * edited their values to match old `setup.xml`
    * removed tags from `setup.xml`
    * made `setup.xml` "match" the one in v2.26
  * tried to run server with just v202108 bathymetry dataset
    * failed due to permissions on dataset netCDF file when I tried to use `sshfs` mount



#### Fri 25-Apr-2025

First session of FoMS program

##### Miscellaneous

* replied to email from Rhian at UTas re: downloading temperature fields from ERDDAP for SDM
  euphausid model



#### Sat 26-Apr-2025

Goofed off.



#### Sun 27-Apr-2025

##### erddap-datasets

* continued developing test versions of `datasets.xml` and `setup.xml` for v2.26 on `khawla`
  * branch: erddap-2.26
  * successfully ran server with just v202108 bathymetry dataset
    * `sshfs` mount has permission that `tomcat` restricted use can't deal with
    * worked when I used `/media/doug/warehouse/MEOPAR/grid/`
    * also got symlinks for `setup.xml` and `datasets.xml` from
      `/usr/local/apache-tomcat-10.1.40/content/erddap/` to `erddap-datasets` clone working



### Week 18

#### Mon 28-Apr-2025

##### erddap-datasets

* continued developing test versions of `datasets.xml` and `setup.xml` for v2.26 on `khawla`
  * branch: erddap-2.26
  * cleaned up edits in `prefix.xml` and `setup.xml`
  * experimented with multi-language support:
    * auto-translations are only for parts of the index page
    * adding translations for our content looks cumbersome
      * I think we would have to add translations to files like
        `webapps/erddap/WEB-INF/classes/gov/noaa/pfel/erddap/util/translatedMessages/messages-fr.xml`
  * it seems that `datasets.xml` is automatically reloaded every 15 to 60 minutes
    * that means that changes to the file take effect without restarting the server; confirmed



#### Tue 29-Apr-2025

Worked at ESB.

##### Miscellaneous

* created ticket for compstaff re: login failures on `lox` at console
* AAPS spring AGM


##### ERDDAP

* met with Henryk re: updating to v2.26



#### Wed 30-Apr-2025

##### erddap-datasets

* continued developing test versions of `datasets.xml` and `setup.xml` for v2.26 on `khawla`
  * branch: erddap-2.26
  * created PR#35 to use for testing new setup on `skookum`
  * added `setenv.sh` to repo so that `java` and `tomcat` version changes are recorded in commits


##### 2025 Bloomcast

* ended cronjob for 2025 runs


##### ERDDAP

* started upgrade to v2.26 on `skookum`
  * installed `openjdk-21-jre`:
    <!-- markdownlint-disable MD013 -->
    ```bash
    sudo apt autoremove
    sudo apt update
    sudo apt install openjdk-21-jre
    sudo apt autoremove
    ```
    <!-- markdownlint-enable MD013 -->
    * installation is in `/usr/lib/jvm/java-21-openjdk-amd64/`
  * installed `tomcat` in `/opt/`:
    <!-- markdownlint-disable MD013 -->
    ```bash
    cd /opt/
    curl -LO https://dlcdn.apache.org/tomcat/tomcat-10/v10.1.40/bin/apache-tomcat-10.1.40.tar.gz
    sudo tar xvzf apache-tomcat-10.1.40.tar.gz
    sudo rm -i apache-tomcat-10.1.40.tar.gz
    ```
    <!-- markdownlint-enable MD013 -->
  * configure `tomcat`:
    * ref: https://erddap.github.io/docs/server-admin/deploy-install
    * edit `conf/server.xml`
      * change the `Server` tag `port` to 8085 for setup testing
      * change the `Connector` tag `port` to 8081 for setup testing
      * change the `Connector` tag `connectionTimeout` to 300000
      * add `relaxedQueryChars="[]|"` to the `Connector` tag
    * edit `conf/content.xml`
      * add `<Resources cachingAllowed="true" cacheMaxSize="80000" />` to `Context`
  * set ownership & permissions on `/opt/apache-tomcat-10.1.40`
    <!-- markdownlint-disable MD013 -->
    ```bash
    sudo chown -R tomcat:erdap apache-tomcat-10.1.40/
    sudo chmod g+rwx apache-tomcat-10.1.40/conf/
    sudo chmod -R g+rw apache-tomcat-10.1.40/*
    ```
    <!-- markdownlint-enable MD013 -->
  * clone `erddap-datasets` so that we can access the `erddap-2.26` branch independent of the
    deployed version:
    <!-- markdownlint-disable MD013 -->
    ```bash
    git clone git@github.com:SalishSeaCast/erddap-datasets.git erddap-datasets-2.26
    cd erddap-datasets-2.26
    git switch erddap-2.26
    ```
    <!-- markdownlint-enable MD013 -->
  * symlink `erddap-datasets-2.26/setenv.sh` into `/opt/apache-tomcat-10.1.40/bin/`
    <!-- markdownlint-disable MD013 -->
    ```bash
    cd /opt/apache-tomcat-10.1.40/bin/
    ln -s /results/erddap-datasets-2.26/setenv.sh
    ```
    <!-- markdownlint-enable MD013 -->
  * started `tomcat`
    <!-- markdownlint-disable MD013 -->
    ```bash
    sudo su - tomcat
    /opt/apache-tomcat-10.1.40/bin/startup.sh
    ```
    <!-- markdownlint-enable MD013 -->
    * used log reading and `wget` to confirm that `tomcat` is running
    * deployed ERDDAP died somewhere in here
    * added reverse proxy on `test-erddap` for port 8081 to `/etc/apache2/sites-available/000-default.conf`
      and restarted `apache` with `sudo systemctl restart apache2.service`
    * got to the (asset-free) tomcat index page at https://salishsea.eos.ubc.ca/test-erddap
  * stopped `tomcat` and restarted ERDDAP


## May

<!-- markdownlint-disable MD001 -->
#### Thu 1-May-2025
<!-- markdownlint-enable MD001 -->

##### SalishSeaCast

* nowcast-agrif failed with:
    stpctl: the zonal velocity is larger than 20 m/s
    kt=****** max abs(U):   61.58    , i j k:     2  392   13


##### erddap-datasets

* continued developing test versions of `datasets.xml` and `setup.xml` for v2.26 on `khawla`
  * branch: erddap-2.26
  * PR#35


##### ERDDAP

* continued upgrade to v2.26 on `skookum`
  * deployed v1.82 survived startup of testing v2.26
  * created `/results/erddap-2.26/` for testing
  * installed ERDDAP v2.26 content config files:
    <!-- markdownlint-disable MD013 -->
    ```bash
    sudo su - tomcat
    cd /opt/apache-tomcat-10.1.40/
    curl -LO https://github.com/ERDDAP/erddapContent/releases/download/content1.0.0/erddapContent.zip
    md5sum erddapContent.zip
    unzip erddapContent.zip
    chgrp -R erdap content
    chmod -R o-rwx content
    rm -i erddapContent.zip
    ```
    <!-- markdownlint-enable MD013 -->
  * symlink `erddap-datasets-2.26/setup.xml` and `erddap-datasets-2.26/datasets.xml` into
    `/opt/apache-tomcat-10.1.40/content/erddap/`:
    <!-- markdownlint-disable MD013 -->
    ```bash
    sudo su - tomcat
    cd /opt/apache-tomcat-10.1.40/content/erddap/
    mv setup.xml setup.xml.orig
    mv datasets.xml datasets.xml.orig
    ln -s /results/erddap-datasets-2.26/setup.xml
    ln -s /results/erddap-datasets-2.26/datasets.xml
    ```
    <!-- markdownlint-enable MD013 -->
  * installed ERDDAP 2.26 `erddap.war` file:
    <!-- markdownlint-disable MD013 -->
    ```bash
    sudo su - tomcat
    cd /opt/apache-tomcat-10.1.40/webapps/
    curl -LO https://github.com/ERDDAP/erddap/releases/download/v2.26.0/erddap.war
    md5sum erddap.war
    chmod o-rwx erddap.war
    chgrp -R erdap erddap.war erddap/
    ```
    <!-- markdownlint-enable MD013 -->
  * prep for initial test:
    * `setup.xml`:
      * `<bigParentDirectory>/results/erddap-2.26/</bigParentDirectory>`
      * `<baseUrl>https://salishsea.eos.ubc.ca:8081</baseUrl>`
    * `datasets.yaml`:
      * comment out all datasets except `nemo-grid/ubcSSnBathymetryV21-08.xml`
      * run `build_datasets_xml.py`
    * test was successful in the logs, but reverse proxy wasn't working
  * shut down v1.82 and flipped v2.26 into its place
    * `setup.xml`:
      * `<baseUrl>https://salishsea.eos.ubc.ca</baseUrl>`
    * removed reverse proxy on `test-erddap` for port 8081 from `/etc/apache2/sites-available/000-default.conf`
      and restarted `apache` with `sudo systemctl restart apache2.service`
    * `datasets.yaml`:
      * gradually added datasets back a few at a time
  * copied `favicon.ico` & `UBC_MEOPAR_logo.png` into `content/erddap/images/`
    * needed a server restart for them to be loaded



#### Fri 2-May-2025

##### Miscellaneous

* MOAD group mtg; see whiteboard
  * Griffon joined the group for a co-op term
* Phys Ocgy seminar: Griffon re: PSF citizen science work with Rich


##### ERDDAP

* time series datasets (ONC & 2nd Narrows HADCP) failed to load due to:
    For cdm_data_type=TimeSeries, the variable with cf_role=timeseries_id (time) must be in the
    cdm_timeseries_variables list.
* datasets are not updating because the `ping_erddap` worker is writing to the fold `erddap/flag/`
  directory



#### Sat 3-May-2025

##### SalishSeaCast

* figure out nowcast-agrif velocity issue then backfill from 01may25


##### FUN

* continued creating 2026 pension income scenario



#### Sun 4-May-2025

##### ERDDAP

* renamed `/results/erddap/` to `/results/erddap-1.82/` and `/results/erddap-2.26/` to `/results/erddap/`
* confirmed that `ping_erddap` worker is triggering dataset updates
* scanned CF-1.10 (supported by 2.26) to try to understand how it differs from CF-1.6 (supported by 1.82)
  * unclear, and verification tool's most recent version is CF-1.8 (https://cfchecker.ncas.ac.uk)
* explored new in 2.26 `displayInfo` & `displayAttribute` tags
  * they control fields and tooltips at the beginning of the `Information` line on the `data` pages
  * we could add a field called `Citation` that shows the `comment` attr
    * perhaps change the name of the `comment` attr to `citation`
* noticed that forecast datasets lacks v21-11 info



### Week 19

#### Mon 5-May-2025

##### SalishSeaCast

* posted details of 01may25 nowcast-agrif run failure on #crashingjobs channel
* strange exception from `make_plots nemo forecast` re: no IO backend for xarray


##### erddap-datasets

* squash-merged PR#35 re: config for 2.26
* Increased the `nGridThreads` and `nTableThreads` settings from 1 to 3 as recommended in the v2.19
  update notes; PR#36 - squash-merged and deployed
* Add `ipAddressMaxRequests`, `ipAddressMaxRequestsActive` and `ipAddressUnlimited` settings as
  recommended in the v2.12 upgrade notes
  * Use the new `ipAddressMaxRequests` value of 15 recommended in the v2.20 upgrade notes
  * limits malicious users and overly aggressive concurrent requests
  * PR#37 - squash-merged


##### ERDDAP

* confirmed that site `robots.txt` file matches recommendation in ERDDAP docs (unchanged in years)
* changed symlinks to point to deployed `erddap-datasets`:
  * `bin/setenv.sh`
  * `content/erddap/setup.xml`
  * `content/erddap/datasets.xml`
* deployed increased threads (PR#36)
* deployed `ipAddressMaxRequests` settings (PR#37)


##### Miscellaneous

* NEMO seminar:
  * Madhurima Chakraborty, U Manitoba, Exploring the environmental factors controlling the iceberg
    season severity along the east coast of Canada
  * Stephanne Taylor, DFO, Transitioning Port Models to NEMO 4.2 with Wetting and Drying
    * 4.2 namelist structures are very different to 3.6
    * Fundy uses zps & vvl in 3.6
      * had to change to sigma coordinates for 4.2



#### Tue 6-May-2025

Worked at ESB

##### Miscellaneous

* MOAD group mtg; see whiteboard
* helped Griffon with onboarding


##### SalishSeaCast

* investigated `make_plots` failures
  * `make_plots wwatch3 forecast publish` was run as
    `make_plots wwatch3 forecast2 publish` after forecast run
    * bug in calculation of `run_type` in `after_ping_erddap()` due to PR#355
  * manual re-run got stuck for >15m collecting Halibut Bank obs from
    https://www.ndbc.noaa.gov/data/realtime2/
  * `make_plots nemo forecast publish` fails because ERDDAP isn't responding correctly
    with `ubcSSfCampbellRiverSSH10m` dataset
  * failed requests seem to be returning JSON? to xarray instead of nothing and
    that triggers `ValueError`
      did not find a match in any of xarray's currently installed IO backends
      ['netcdf4', 'h5netcdf', 'scipy', 'cfgrib']. Consider explicitly selecting
      one of the installed engines via the ``engine`` parameter, or installing
      additional IO dependencies, see:
      https://docs.xarray.dev/en/stable/getting-started-guide/installing.html
      https://docs.xarray.dev/en/stable/user-guide/io.html
  * `make_plots wwatch3 forecast publish` failed with `TypeError`
      Plotting requires coordinates to be numeric, boolean, or dates of type
      numpy.datetime64, datetime.datetime, cftime.datetime or pandas.Interval.
      Received data of type object instead.


##### ERDDAP

* dataset responses not working
* memory no freed after I stopped process
* stopped everything
* ran `/usr/local/sbin/update_spt.sh`
  * kept modified `/etc/zabbix/zabbix_agent2.conf`
* responses were stalling for `make_plots nemo forecast publish` to changed
  threads back from 3 to 1



#### Wed 7-May-2025

##### SalishSeaCast

* `grib_to_netcdf nowcast+` failed due to missing
  `20250506T18Z_MSC_HRDPS_UGRD_AGL-10m_RLatLon0.0225_PT005H_SSC.grib2`
  * all 18Z grib files are missing despite `collect_weather` and `crop_gribs` having completed
    successfully; evidence of more weirdness on `skookum` before I rebooted it yesterday?
  * added `--backfill` feature to `download_weather` re: issue #309
  * successfully re-ran `crop_gribs` and `download_weather`
* started backfilling `nowcast-agrif`:
      <!-- markdownlint-disable MD013 -->
    ```bash
    rsync -tv /home/sallen/MEOPAR/ANALYSIS/analysis-susan/notebooks/Crashes/SalishSea_08432640_restart.nc \
    orcinus:/global/scratch/dlatorne/nowcast-agrif/30apr25/
    make_forcing_links orcinus nowcast-agrif 2025-05-01
    make_forcing_links orcinus nowcast-agrif 2025-05-02
    make_forcing_links orcinus nowcast-agrif 2025-05-03
    make_forcing_links orcinus nowcast-agrif 2025-05-04
    make_forcing_links orcinus nowcast-agrif 2025-05-05
    make_forcing_links orcinus nowcast-agrif 2025-05-06
    make_forcing_links orcinus nowcast-agrif 2025-05-07
    ```
    <!-- markdownlint-enable MD013 -->


##### SalishSeaNowcast

* added `--backfill` feature to `download_weather` re: issue #309
  * branch: download_weather-backfill
  * tested successfully to resolve missing 18Z gribs issue above


##### Miscellaneous

* pinged Henryk re: bad `/results` mount on `salish` that Ilias reported
  * he got it re-mounted by killing a bunch of users' processes



#### Thu 8-May-2025

##### SalishSeaCast

* recent `make_plots wwatch3 forecast` failures may be due to change in presentation of missing obs
* `make_plots wwatch3 forecast2` ran instead of `make_plots wwatch3 forecast`
  * likely due to the bug I identified on 6may
  * manually re-ran the correct worker


##### Miscellaneous

* Alliance town hall re: AI Sovereign Compute Infrastructure Program submission to fed govt


##### erddap-datasets

* fixed time series datasets load failures:
  * PR#38
  * `ubcVFPA2ndNarrowsCurrent2sV1`
    * added dataset attrs:
      * `<att name="cdm_data_type">TimeSeries</att>`
      * `<att name="cdm_timeseries_variables">time, longitude, latitude</att>`
  * added `time` to `cdm_timeseries_variables` dataset attr:
    * `ubcONCLSBBLCTD15mV1`
    * `ubcONCSCVIPCTD15mV1`
    * `ubcONCSEVIPCTD15mV1`
    * `ubcONCUSDDLCTD15mV1`
    * `ubcONCTWDP1mV18-01`



#### Fri 9-May-2025

##### SalishSeaNowcast

* tried to fix issue of `make_plots wwatch3 forecast2` ran instead of `make_plots wwatch3 forecast`
  * live edit on `skookum` to flip calculation of `run_type` in `after_ping_erddap()`
  * restarted manager to load updated `next_workers` module



#### Sat 10-May-2025

Chores



#### Sun 11-May-2025

Bike ride and goofed off.



### Week 20

#### Mon 12-May-2025

##### ERDDAP

* tried to figure out why TWDP, SEVIP & SCVIP datasets time values are incorrect


##### Miscellaneous

* fixed path that 2022 atmospheric forcing files were uploaded to on `beluga`
* uploaded 2023 forcing files to `beluga` for Tall:
  <!-- markdownlint-disable MD013 -->
  ```bash
  yyyy=2023; rsync -tLv /results/forcing/atmospheric/GEM2.5/operational/ops_y${yyyy}*.nc \
    beluga:projects/def-allen/SalishSea/forcing/atmospheric/GEM2.5/operational/
  yyyy=2023; rsync -tLv /results/forcing/atmospheric/continental2.5/nemo_forcing/hrdps_y${yyyy}*.nc \
    beluga:projects/def-allen/SalishSea/forcing/atmospheric/continental2.5/nemo_forcing/
  yyyy=2023; rsync -tLv /results/forcing/sshNeahBay/obs/ssh_y${yyyy}*.nc \
    beluga:projects/def-allen/SalishSea/forcing/sshNeahBay/obs/
  yyyy=2023; rsync -tLv /results/forcing/rivers/R202108Dailies_y${yyyy}*.nc \
    beluga:projects/def-allen/SalishSea/forcing/rivers/
  yyyy=2023; rsync -tLv /results/forcing/rivers/river_turb/riverTurbDaily2_y${yyyy}*.nc \
    beluga:projects/def-allen/SalishSea/forcing/rivers/river_turb/
  yyyy=2023; rsync -tLv /results/forcing/LiveOcean/boundary_conditions/LiveOcean_v201905_y${yyyy}*.nc \
    beluga:projects/def-allen/SalishSea/forcing/LiveOcean/
  ```
  <!-- markdownlint-enable MD013 -->
* uploaded 2024 forcing files to `beluga` for Tall:
  <!-- markdownlint-disable MD013 -->
  ```bash
  yyyy=2024; rsync -tLv /results/forcing/atmospheric/continental2.5/nemo_forcing/hrdps_y${yyyy}*.nc \
    beluga:projects/def-allen/SalishSea/forcing/atmospheric/continental2.5/nemo_forcing/
  yyyy=2024; rsync -tLv /results/forcing/sshNeahBay/obs/ssh_y${yyyy}*.nc \
    beluga:projects/def-allen/SalishSea/forcing/sshNeahBay/obs/
  yyyy=2024; rsync -tLv /results/forcing/rivers/R202108Dailies_y${yyyy}*.nc \
    beluga:projects/def-allen/SalishSea/forcing/rivers/
  yyyy=2024; rsync -tLv /results/forcing/rivers/river_turb/riverTurbDaily2_y${yyyy}*.nc \
    beluga:projects/def-allen/SalishSea/forcing/rivers/river_turb/
  yyyy=2024; rsync -tLv /results/forcing/LiveOcean/boundary_conditions/LiveOcean_v201905_y${yyyy}*.nc \
    beluga:projects/def-allen/SalishSea/forcing/LiveOcean/
  ```
  <!-- markdownlint-enable MD013 -->



#### Tue 13-May-2025

Worked at ESB

##### Miscellaneous

* MOAD group mtg; see whiteboard
* helped Grace get set up to use Parcels on `grinder`
* helped Tall update his analysis env on `beluga`



#### Wed 14-May-2025

##### erddap-datasets

* fixed TWDP, SEVIP & SCVIP datasets time values
  * time units were being interpreted as `seconds since 1970-01-01T00:00:00Z` despite being
    `minutes since 1970-01-01T00:00:00Z`, so make that explicit in XML files
  * PR#39
* committed reversion of n*Threads from 3 to 1; PR#40


##### SalishSeaTools

* removed the uncommitted `test_stormtools2` module after confirming that its contents are in
  `test_stormtools`
* closed issue #98 re: HTTPS for climate.weather.gc.ca requests; done in PR #106 while fixing broken
  links
* fixed issue #108 re: "SyntaxWarning: invalid escape sequence '\*'" in `tidetools` docstrings
  with docstring re-writes by PyCharm AI; PR#142



#### Thu 15-May-2025

##### SalishSeaCast

* `make_plots wwatch3 forecast2 publish` failed at 04:05 with
  `RuntimeError: NetCDF: Access failure` on Halibut Banks figure
  * this is perhaps due to ERDDAP dataset update not being finished; mitigate with `tenacity` wrapper
    around dataset request in `figures.wwatch3.wave_height_period._prep_plot_data()` line 77
  * manual re-try at 09:10 failed on Sentry Shoal figure with:
      TypeError: Plotting requires coordinates to be numeric, boolean, or dates of type
      numpy.datetime64, datetime.datetime, cftime.datetime or pandas.Interval. Received data of type
      object instead.
    * this is be due to missing values filled with `MM`; probably a recent change in the NDBC product
    * fixed in PR#360; deployed to `skookum` for verification


##### Atlantis

* mtg w/ Javier
* pointed Raisha at Rainbow CSV extension for VSCode



#### Fri 16-May-2025

Worked at ESB

##### SalishSeaCast

* confirmed that `make_plots wwatch3 forecast* publish` are working correctly
  re: `run_type` calculation hack and PR#360


##### Miscellaneous

* helped Griffon get `SalishSeaTools` installed in his analysis env\
* cleaned up `/var/cache/apt/` re: nearly full `root` partition on `kudu`
  * started with 24.2 GB in 5222 items
  * ran `sudo apt-get autoclean`
  * resulted in 7.4 GB in 3304 items
* helped Tall get `eval_tools` obs matching working in batch jobs on `beluga`


##### private-docs

* replaced `.hgignore` with `.gitignore`
* started work on talk outline for 30may25 Phys Ocgy seminar



#### Sat 17-May-2025

Patio work and bike work



#### Sun 18-May-2025

Cycled to Sanctuary and back

##### SalishSeaCast

* `make_plots wwatch3 forecast publish` failed with `RuntimeError: NetCDF: DAP failure`
  * I suspect a race condition with the ERDDAP dataset reload triggered by `ping_erddap wwatch3`


##### ERDDAP

* Rich reported that the TWDP ferry dataset has reverted to 1970 dates
  * forced dataset reload corrected the issue



### Week 21

#### Mon 19-May-2025

**Statutory Holiday** - Victoria Day

##### SalishSeaCast

* `make_plots wwatch3 forecast2 publish` failed with `RuntimeError: NetCDF: DAP failure`
* `make_plots wwatch3 forecast publish` failed similarly
  * manual re-run at ~12:40 was successful


##### Security Updates

* Squash-merged dependabot PRs to update codecov-action to 5.4.3 re: dependency updates
  * gha-workflows
  * SalishSeaNowcast
  * AtlantisCmd
* Squash-merged dependabot PRs to update setuptools to 78.1.1 re: CVE-2025-47273 re: path traversal
  vulnerability
  * SalishSeaNowcast
  * AtlantisCmd
  * gha-workflows
  * cookiecutter-MOAD-pypkg
  * cookiecutter-analysis-repo


##### ERDDAP

* forced dataset reloads of TWDP, SEVIP & SCVIP to correct time units



#### Tue 20-May-2025

Worked at ESB.

Attended VGH Cardiac Rehab program fund raiser.

##### SalishSeaCast

* `make_plots wwatch3 forecast2 publish` failed
  * netCDF error
  * ran for 19may instead of 20may; probably due to running before checklist reset?


##### ERDDAP

* TWDP, SEVIP & SCVIP datasets reverted to 1970 times after morning updates
  * forced dataset reloads of TWDP, SEVIP & SCVIP at ~08:40 to correct time units


##### Security Updates

* Squash-merged dependabot PRs to update setuptools to 78.1.1 re: CVE-2025-47273 re: path traversal
  vulnerability
  * MOAD/docs
  * SalishSeaCast/docs
  * NEMO_Nowcast
  * moad_tools
  * SalishSeaTools
  * Reshapr
  * SalishSeaCmd
  * NEMO-Cmd
  * salishsea-site
  * MoaceanParcels
  * SOG-Bloomcast-Ensemble
  * FUN
  * SOG-forcing
  * SOG-Bloomcast
  * erddap-datasets


##### Miscellaneous

* MOAD group mtg; see whiteboard



#### Wed 21-May-2025

##### ERDDAP

* TWDP, SEVIP & SCVIP datasets reverted to 1970 times after morning updates
  * forced dataset reloads of TWDP, SEVIP & SCVIP at ~08:55 to correct time units


##### SalishSeaCast

* `make_plots wwatch3 forecast2 publish` failed after checklist reset with netCDF access failure
  * re-ran successfully at ~09:00


##### Miscellaneous

* had to do the upstairs/downstairs dance again to get VSCode to connect to Zwift PC
  * PC wifi setting gets changed from Private to Public by the Windows Security Nanny


##### private-docs

* continued work on talk for 30may25 Phys Ocgy seminar



#### Thu 22-May-2025

##### ERDDAP

* TWDP, SEVIP & SCVIP datasets reverted to 1970 times after morning updates
  * forced dataset reloads of TWDP, SEVIP & SCVIP at ~09:45 to correct time units


##### private-docs

* continued work on talk for 30may25 Phys Ocgy seminar


##### SalishSeaCast

* `make_plots wwatch3 forecast publish` failed at 11:18 with `RuntimeError: NetCDF: DAP failure`
  * manual re-run at ~11:35 also failed
  * manual re-run at ~11:45 succeeded
  * I suspect that the problem is slow response to `ping_erddap` for rolling forecast dataset due to
    ERDDAP being busy loading results from `nowcast-green` run
    * try to mitigate with `tenacity` wrapper around dataset request in
      `figures.wwatch3.wave_height_period._prep_plot_data()` line 77
* squash-merged and deployed PR#360 re: missing wave buoy obs values filled with `MM` due to a
  change in the NDBC product


##### Miscellaneous

* updated PyCharm on `khawla` to 2025.1.1.1
* UBC-IOS-CCCma modeling mtg
  * Kyoko Ohashi: IOS on Dal work of particle tracking on East Coast re: MPAs for CMOS
  * Laura Bianucci: obs & models in fjords



#### Fri 23-May-2025

##### ERDDAP

* TWDP, SEVIP & SCVIP datasets reverted to 1970 times after morning updates
  * forced dataset reloads of TWDP, SEVIP & SCVIP at ~09:45 to correct time units


##### SalishSeaCast

* `make_plots wwatch3 forecast publish` failed at 11:23 with `RuntimeError: NetCDF: DAP failure`
  * manual re-run at ~15:25 succeeded


##### Security Updates

* Squash-merged dependabot PRs to update tornado to 6.5.1 re: CVE-2025-47287 re: DoS attack vulnerability
  * moad_tools
  * MOAD/docs
  * MoaceanParcels
  * SalishSeaCast/docs
  * Reshapr
  * SalishSeaNowcast
  * SalishSeaTools
  * ECget
  * SOG-Bloomcast-Ensemble
  * erddap-datasets
  * SOG-Bloomcast


##### NEMO-Cmd

* fixed broken and redirected docs links found by linkcheck; PR#105



#### Sat 24-May-2025

##### ERDDAP

* TWDP, SEVIP & SCVIP datasets reverted to 1970 times after morning updates
  * forced dataset reloads of TWDP, SEVIP & SCVIP at ~08:05 to correct time units


##### SalishSeaCast

* `make_plots wwatch3 forecast2 publish` failed at 04:11 with `RuntimeError: NetCDF: DAP failure`
  * manual re-run at ~08:05 succeeded



#### Sun 25-May-2025

##### ERDDAP

* TWDP, SEVIP & SCVIP datasets reverted to 1970 times after morning updates
  * forced dataset reloads of TWDP, SEVIP & SCVIP at ~08:05 to correct time units


##### SalishSeaCast

* `make_plots wwatch3 forecast2 publish` failed at 04:05 with `RuntimeError: NetCDF: DAP failure`
  * manual re-run at ~09:05 succeeded



### Week 22

#### Mon 26-May-2025

##### ERDDAP

* TWDP, SEVIP & SCVIP datasets reverted to 1970 times after morning updates
  * forced dataset reloads of TWDP, SEVIP & SCVIP at ~08:52 to correct time units
  * tried using `erddap/hardFlag/ubcONCSCVIPCTD15mV1` to reload the internal database for that dataset
    * probably didn't work because time units are now `seconds since 1970-01-01T00:00:00Z`
    * perhaps there's file(s) with incorrect time units?


##### SalishSeaCast

* `make_plots wwatch3 forecast2 publish` failed at 04:09 with `RuntimeError: NetCDF: DAP failure`
  * manual re-run at ~08:53 succeeded



#### Tue 27-May-2025

Worked at ESB while Rita was at home

##### ERDDAP

* TWDP, SEVIP & SCVIP datasets reverted to 1970 times after morning updates
  * forced dataset reloads of TWDP, SEVIP & SCVIP at ~09:15 to correct time units


##### SalishSeaCast

* Fraser River turbidity data stream stopped after 03:10; update Tuesday?


##### Miscellaneous

* MOAD group mtg; see whiteboard
* helped Griffon expunge a large file from his `analysis-griffon` commit history
  and diagnose a mystery failure of quantitative Ariane that turned out to be
  due to running out of memory on `chum`


##### private-docs

* continued work on talk for 30may25 Phys Ocgy seminar



#### Wed 28-May-2025

##### ERDDAP

* TWDP, SEVIP & SCVIP datasets reverted to 1970 times after morning updates
  * forced dataset reloads of TWDP, SEVIP & SCVIP at ~09:15 to correct time units


##### SalishSeaCast

* no obs for Skagit River
* Fraser River turbidity obs data stream resumed, but there are enough missing obs that we persisted
  again


##### private-docs

* continued work on talk for 30may25 Phys Ocgy seminar



#### Thu 29-May-2025

Cardiac rehab exit stress test

##### ERDDAP

* TWDP, SEVIP & SCVIP datasets reverted to 1970 times after morning updates
  * forced dataset reloads of TWDP, SEVIP & SCVIP at ~09:15 to correct time units


##### SalishSeaCast

* `make_plots wwatch3 forecast2 publish` failed at 04:09 with `RuntimeError: NetCDF: DAP failure`
  * manual re-run at ~09:20 succeeded


##### private-docs

* finished slides for talk for 30may25 Phys Ocgy seminar


##### Miscellaneous

* listened to NEMO collab workshop at CMOS



#### Fri 30-May-2025

Worked at ESB

Cardiac rehab exit blood lab draw

##### ERDDAP

* TWDP, SEVIP & SCVIP datasets reverted to 1970 times after morning updates
  * forced dataset reloads of TWDP, SEVIP & SCVIP at ~08:10 to correct time units


##### SalishSeaCast

* `make_plots wwatch3 forecast2 publish` failed at 04:11 with `RuntimeError: NetCDF: DAP failure`
  * manual re-run at ~08:10 succeeded


##### Miscellaneous

* presented Phys Ocgy seminar: SalishSeaCast Configuration & Automation


##### SalishSeaNowcast

* fixed logic for make_plots wwatch3 run type selection
  * PR#364
  * prioritize forecast over forecast2 to ensure correct choice when there is a forecast key in The
    "WWATCH3 runs" item in the checklist
* fixed `test_run_NEMO_hindcast` tests that almost always fail in GHA workflow, but not locally
  * PR#365
  * moved assertions into `pytest.raises()` context manager scope



#### Sat 31-May-2025

##### ERDDAP

* TWDP, SEVIP & SCVIP datasets reverted to 1970 times after morning updates
  * forced dataset reloads of TWDP, SEVIP & SCVIP at ~11:40 to correct time units


##### SalishSeaCast

* `make_plots wwatch3 forecast2 publish` failed at 04:07 with `RuntimeError: NetCDF: DAP failure`
  * manual re-run at ~11:40 succeeded


##### SalishSeaNowcast

* started work to resolve `make_plots wwatch3 forecast* publish` failures with
  `RuntimeError: NetCDF: DAP failure`
  * dropped unused `buoy` arg from `_plot_wave_height_time_series()` and
    `_plot_dominant_period_time_series()`



## June

<!-- markdownlint-disable MD001 -->
#### Sun 1-Jun-2025
<!-- markdownlint-enable MD001 -->

##### ERDDAP

* TWDP, SEVIP & SCVIP datasets reverted to 1970 times after morning updates
  * forced dataset reloads of TWDP, SEVIP & SCVIP at ~11:40 to correct time units


##### SalishSeaNowcast

* started work to resolve `make_plots wwatch3 forecast* publish` failures with
  `RuntimeError: NetCDF: DAP failure`
  * PR#366
  * added `tenacity.retry` decorator to `_plot_wave_height_time_series()` and
    `_plot_dominant_period_time_series()`
  * tried to remove excess x-axis labels in wave height sub-plot; success for axis label, but not
    for month tick label
  * deployed branch to production for testing



### Week 23

#### Mon 2-Jun-2025

##### ERDDAP

* TWDP, SEVIP & SCVIP datasets **hadn't** revert to 1970 times at 09:10, but had by 09:40
  * forced dataset reloads of TWDP, SEVIP & SCVIP at ~09:40 to correct time units


##### SalishSeaCast

* `make_ssh_files forecast2` errored due to missing obs
* `make_plots wwatch3 forecast2 publish` failed at 04:18 with `RuntimeError: NetCDF: DAP failure`
  apparently after `tenacity` did its job
  * manual re-run at ~09:10 succeeded


##### SalishSeaNowcast

* continued work to resolve `make_plots wwatch3 forecast* publish` failures with
  `RuntimeError: NetCDF: DAP failure`
  * PR#366
  * `make_plots wwatch3 forecast2 publish` seems to have failed after 10 minutes of retrying
    * changed retry parameters to 1-3 minutes random intervals for 20 minutes
    * added logging before



#### Tue 3-Jun-2025

Worked at ESB

##### ERDDAP

* TWDP, SEVIP & SCVIP datasets reverted to 1970 times after morning updates
  * forced dataset reloads of TWDP, SEVIP & SCVIP at ~08:42 to correct time units


##### SalishSeaCast

* `make_plots wwatch3 forecast2 publish` failed at 04:27 with `RuntimeError: NetCDF: DAP failure`
  apparently after `tenacity` did its job
  * manual re-run at ~08:43 succeeded


##### Miscellaneous

* MOAD group mtg; see whiteboard
* met w/ Susan to discuss my work focus
  * centre on next version of SalishSeaCast
  * marked up whiteboard with:
    * things that will be included:
      * Tall's O2 improvements
      * Karyn's Z2 seasonal cycle work
      * temperature growth curve for diatoms and nanoflagellates
      * correct the density correction for river/plume water from 1026 to 1000
      * move the south edge of the grid to include all of Puget Sound
      * tuning and evaluation
    * things that may be included:
      * higher nitrate/ammonium in Puget Sound
      * include swage outfalls
      * river temperatures
      * improved Puget Sound bathymetry re: Tall's finding that it is too shallow
        in the inlets
      * update Howe Sound runoff calculations to include Capilano River gauge
    * things that won't be included:
      * bacteria
      * turbidity affecting other variables
      * update to NEMO 4.2 or 5
      * SSS150 (perhaps as an AGRIF sub-grid)
  * implications for my work focus:
    * improve `SalishSeaTools.evaltools` module
      * poll group on who is using what functions and what dataset sources they use
    * finish 202405 bathymetry with Susan
    * get NEMO running again on `sockeye`
      * work with ARC to get automation auth on `sockeye`
      * target the runs that Susan needs to do for Karyn
    * do we want to eliminate nowcast-blue run on `arbutus`?
      * what are the implications of that for future SSS150 AGRIF?


##### SalishSeaTools

* started reviewing `evaltools` module:
  * 3216 LOC
  * dependencies:
    * excel engine:
      * `openpyxl` for Excel 2010 xlsx/xlsm files
        * v3.1.5 of 29jun2024 is on conda-forge
      * `xlrd` for legacy `.xls` files
        * last release was 2.0.1 in Dec-2020
      * used in `loadPDF()` via `pandas.read_excel()`
      * used in `loadHakai()` via `pandas.read_excel()`
      * used in `load_Pheo_data()` via `pandas.read_excel()`
    * imports inside functions:
      * `sqlalchemy` in
        * `loadDFOCTD()`
          * used to access `/ocean/shared/SalishSeaCastData/DFO/CTD/DFO_CTD.sqlite`
        * `loadDFO()`
          * used to access `/ocean/eolson/MEOPAR/obs/DFOOPDB/DFO_OcProfDB.sqlite`
      * `erdddapy` in:
        * `load_ferry_ERDDAP()`
        * `load_ONC_node_ERDDAP()`
  * functions:
    * `matchData()`
      * `_gridHoriz()`
      * `_vertNetmatch()`
      * `_binmatch()`
      * `_vvlBin()`
      * `_interpvvlZ()`
      * `_ferrymatch()`
      * `_nextfile_bin()`
      * `_getTimeInd_bin()`
      * `_getTimeInd_bin_ops()`
      * `_getZInd_bin()`
    * `index_model_files()`
    * `index_model_files_flex()`
    * `loadDFOCTD()`
    * `loadDFO()`
    * `loadPSF()`
      * `_lt0convert()`
    * `loadPSFCTD()`
    * `loadHakai()`
    * `load_ferry_ERDDAP()`
    * `load_ONC_node_ERDDAP()`
    * `stats()`
      * `WSS()`
      * `RMSE()`
    * `varvarScatter()`
    * `varvarPlot()`
    * `varvarIter()`
    * `tsertser_graph()`
    * `_deframe()`
    * `_flatten_nested_dict()`
    * `displayStats()`
    * `displayStatsFlex()`
    * `utc_to_pac()`
    * `pac_to_utc()`
    * `pdt_to_utc()`
    * `pst_to_utc()`
    * `datetimeToDecDay()`
    * `printstats()`
    * `datetimeToYD()`
    * `getChlNRatio()`
    * `load_Pheo_data()`
    * `load_WADE_data()`
    * `load_CTD_data()`
  * so many hard-coded paths in `/ocean/eolson/MEOPAR/obs/`
  * WADE datasets stored as pickles in `/ocean/eolson/MEOPAR/obs/WADE/ptools_data/ecology/`



#### Wed 4-Jun-2025

##### ERDDAP

* TWDP, SEVIP & SCVIP datasets reverted to 1970 times after morning updates
  * forced dataset reloads of TWDP, SEVIP & SCVIP at ~09:27 to correct time units
* Reviewed today's email messages log and found many:
  "java.io.IOException: User limit of inotify watches reached"
  * realized that limits had reverted to low default values after last `skookum` reboot:
  * set new values:
    <!-- markdownlint-disable MD013 -->
    ```bash
      sudo sysctl fs.inotify.max_user_instances=2048
      sudo sysctl fs.inotify.max_user_watches=196608
      sudo sysctl -p
    ```
    <!-- markdownlint-enable MD013 -->
* opened ticket for Henryk to look at no email issue
  * he noted that `/home/tomcat/` doesn't exist and created it


##### SalishSeaCast

* `make_plots wwatch3 forecast2 publish` failed at 04:35 with `RuntimeError: NetCDF: DAP failure`
  apparently after `tenacity` did its job
  * manual re-run at ~09:30 succeeded


##### erddap-datasets

* removed `updateEveryNMillis` tag from all datasets because we shouldn't need it; we use a flag to
  trigger updates whenever our datasets change


##### `sockeye`

* 210 base nodes w/ 32 cores & 192 GB RAM (6 GB/core) `skylake`
* 170 base nodes w/ 40 cores & 192 GB RAM (4.8 GB/core) `cascade`
* 2? login nodes
* 2 data transfer nodes (`dtn.sockeye.arc.ubc.ca`)
* `gcc` 5.5.0, 7.5.0, 9.4.0
* `intel` 2023.1.0, 2023.2.1
* `miniconda3` 4.9.2 (2020-11-10)
* `netcdf-fortran` 4.5.3, 4.6.1
* `openmpi` 4.1.1, 4.1.6
* `/project/` has become `/arc/project/`
* fix `$PROJECT` path
  * edit `.bash_profile`
  * `ln -sf /arc/project/st-sallen1-1/ project`
  * re-log
* remove old `module load` statements from `.bashrc`
* remove `mambaforge-pypy3` installation
  <!-- markdownlint-disable MD013 -->
  ```bash
  cp .condarc .condarc-aside
  conda activate base
  conda init --reverse --all
  conda deactivate
  rm -rf mambaforge-pypy3/ Mambaforge-pypy3-Linux-x86_64.sh .conda .condarc project/dlatorne/conda-envs/*
  rm -rf ~/.local/*
  ```
  <!-- markdownlint-enable MD013 -->
* install `miniforge3`
  <!-- markdownlint-disable MD013 -->
  ```bash
  curl -L -O \
    "https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-$(uname)-$(uname -m).sh"
  bash Miniforge3-$(uname)-$(uname -m).sh
  ```
  <!-- markdownlint-enable MD013 -->
  * allow it to auto-initialize conda
  * re-log
* configure conda/mamba:
  <!-- markdownlint-disable MD013 -->
  ```bash
  conda config --set auto_activate_base false
  conda config --add envs_dirs /arc/project/st-sallen1-1/dlatorne/conda-envs/
  ```
  <!-- markdownlint-enable MD013 -->
  * re-log
* install SalishSeaCmd
  <!-- markdownlint-disable MD013 -->
  ```bash
  cd project/dlatorne/MEOPAR/NEMO-Cmd/
  git pull
  cd project/dlatorne/MEOPAR/SalishSeaCmd/
  git pull
  mamba env create -f envs/environment-hpc.yaml
  mamba activate salishsea-cmd
  python -m pip install --user -e ../NEMO-Cmd
  python -m pip install --user -e .
  ```
  <!-- markdownlint-enable MD013 -->
* build XIOS
  <!-- markdownlint-disable MD013 -->
  ```bash
  cd project/dlatorne/MEOPAR/XIOS-ARCH/
  git pull
  cd project/dlatorne/MEOPAR/XIOS-2/
  git pull
  ```
  <!-- markdownlint-enable MD013 -->



#### Thu 5-Jun-2025

##### Miscellaneous

* helped Camryn with the fact that VSCode will no longer allow connections to `graham`
* looked for ONC Saanich Inlet node profile datasets for Tall
  * Yarrow Point, 2015-2016, sparse obs, maybe compromised quality


##### ERDDAP

* TWDP, SEVIP & SCVIP datasets **hadn't** revert to 1970 times at 08:55
* no daily status email, as usual
  * daily message was sent at 07:12:05
  * I don't see `/home/tomcat/`; told Henryk, he says that it is `/var/tomcat/`
    because it is a dummy user
* Reviewed today's email messages log and found **no**:
  "java.io.IOException: User limit of inotify watches reached"
* restarted ERDDAP at ~15:55
  * got "Cannot load from object array because "this.sourceAxisValues" is null" messages for:
    * ubcSSf2DWaveFields30mV17-02
    * ubcSSf3DuGridFields1h
    * ubcSSf3DvGridFields1h
    * ubcSSfSurfaceTracerFields1h
    * ubcSSfDepthAvgdCurrents1h
  * resolved by doing `hardFlag/` reloaded on the datasets; weird


##### SalishSeaCast

* `make_plots wwatch3 forecast2 publish` **worked** at 04:16
* Clowhom River obs collection failed


##### SalishSeaTools

* put message in #evaluations-observations asking who uses `evaltools`
  * Karyn
  * Susan


##### `sockeye`

* successfully built XIOS
  * deleted `fcm_env.ksh -> /project/st-sallen1-1/dlatorne/MEOPAR/XIOS-2/fcm_env.sh`
  * tried to use intel OneAPI compilers but the C++ compiler appears to have a dependency on GCC
    (error #10417) that requires a hacky work-around: https://scicomp.ethz.ch/wiki/Migrating_to_Ubuntu
  * buffed `arch-GCC_SOCKEYE.*` files
    * changed deprecated `mpif90` to `mpifort`
    * changed to `gcc-9.4.0`
    * added `parallel-netcdf/1.12.2-additional-bindings` module
    * build failed with `/usr/bin/ld: cannot find -lz`
      * dropped `-lz` from `arch-GCC_SOCKEYE.path`
  * success!
* successfully built SalishSeaCast NEMO
  * module loads
    <!-- markdownlint-disable MD013 -->
    ```bash
    module load gcc/9.4.0
    module load openmpi/4.1.1-cuda11-3
    module load netcdf-fortran/4.5.3-hdf4-support
    module load parallel-netcdf/1.12.2-additional-bindings
    module load perl/5.34.0
    module load perl-uri/1.72
    ```
    <!-- markdownlint-enable MD013 -->
  * buffed `arch-GCC_SOCKEYE.fcm` file
    * changed deprecated `mpif90` to `mpifort`
    * updated `%NCDF_INC` to match that used for XIOS build
  * success!
* `rebuild_nemo` build doesn't like the `-lxios` in `%XIOS_LIB -L%XIOS_HOME/lib -lxios`
  * works when that is temporarily removed


##### SalishSeaCmd

* started updating for present `sockeye` environment
  * branch: sockeye-2025
  * PR#
  * changed module loads



#### Fri 6-Jun-2025

##### ERDDAP

* TWDP, SEVIP & SCVIP datasets **hadn't** revert to 1970 times at 06:55 nor at 13:00
* uncommented `emailSmtpPort` tag in `setup.xml` and set it to 25 in case my assumption about it getting
  the correct default value is wrong
  * restarted ERDDAP
  * still no email
* successfully tested using `mail` to send mail from `dlatorne@skookum`
  * same test as `tomcat` failed due to `Cannot open mailbox /var/mail/tomcat: Permission denied`
  * updated ticket to Henryk


##### SalishSeaCast

* `make_plots wwatch3 forecast2 publish` failed at 04:38 with `RuntimeError: NetCDF: DAP failure`
  after `tenacity` did its job
  * manual re-run at ~13:15 succeeded


##### Miscellaneous

* Phys Ocgy seminar: Charles Hannah re: O2 in the NW Pacific


##### `sockeye`

* created `SS-run-sets/SalishSea/djl/v202111/sockeye-example.yaml`
* added `sockeye-Jun25` sheet to HPC scaling Google spreadsheet
* fixed `.bash_profile` exports of `PROJECT` and `SCRATCH`
* created `$PROJECT/$USER/MEOPAR/runs/` and `$PROJECT/$USER/MEOPAR/results/`
* updated repo clones:
  * `grid`
  * `rivers-climatology`
  * `tides`
  * `tracers`
* uploaded restart files:
  * `$SCRATCH/$USER/MEOPAR/results/28feb23/SalishSea_16701120_restart.nc`
  * `$SCRATCH/$USER/MEOPAR/results/28feb23/SalishSea_16701120_restart_trc.nc`
* uploaded forcing files for 29feb23 and 01-02mar23



#### Sat 7-Jun-2025

##### ERDDAP

* TWDP, SEVIP & SCVIP datasets **hadn't** revert to 1970 times at 06:55 nor at 13:00
* `ubcSSaSurfaceAtmosphereFieldsV23-02` has max time of 2025-06-06T23:00:00Z
  * shouldn't it be later?
* still no daily report email


##### SalishSeaCast

* `make_plots wwatch3 forecast2 publish` failed at 04:34 with `RuntimeError: NetCDF: DAP failure`
  after `tenacity` did its job
  * manual re-run at ~09:50 succeeded
* river obs collection failed for Salmon and Skagit rivers
* `crop_gribs 12` missed 1 file; delayed runs by ~2h


##### `sockeye`

* fixed mess re: `GLS_k` in code and `field_def.xml` caused by Tall reverting Susan's code changes
  instead of updating his `field_def.xml`
* 01mar23-4x9 run is time stepping!
* 01mar23-5x10 run is time stepping!
  * annoying restriction causes `salishsea run` to fail without `--no-submit`
    <!-- markdownlint-disable MD013 -->
    ```text
      sbatch: error: ---------------------------------------------------------------------
      sbatch: error: Submitting jobs from directories residing in /arc/project is not allowed.
      sbatch: error: Transfer your files to a directory in /scratch FS  and submit the job from there.
      sbatch: error: ---------------------------------------------------------------------
      sbatch: error: Batch job submission failed: Job cannot be submitted without the current working directory specified.
      salishsea ERROR: Command '['sbatch', '/scratch/st-sallen1-1/dlatorne/MEOPAR/runs/01mar-5x10_2025-06-07T102312.373568-0700/SalishSeaNEMO.sh']' returned non-zero exit status 1.
    ```
    <!-- markdownlint-enable MD013 -->
* finished scaling runs up to 5 nodes
* `rebuild_nemo` was consistently not found



#### Sun 8-Jun-2025

##### ERDDAP

* TWDP, SEVIP & SCVIP datasets **hadn't** revert to 1970 times at 06:55 nor at 13:00
* `ubcSSaSurfaceAtmosphereFieldsV23-02` has max time of 2025-06-06T23:00:00Z
  * definitely a problem
    * file pattern was some how reverted to `ops_*` from `hrdps_*`
    * resolved by doing a `hardFlag/` touch
* still no daily report email


##### SalishSeaCast

* `make_plots wwatch3 forecast2 publish` failed at 04:34 with `RuntimeError: NetCDF: DAP failure`
  after `tenacity` did its job
  * failure was on Sentry Shoal plot instead of Halibut Bank
  * plots are on website ???


##### `sockeye`

* resolved job submission restriction issue by using only absolute paths in YAML file and doing
  `salishsea run` in a directory on `/scratch/`
* finished scaling runs for 6-9 nodes
  * best NEMO time is 9m59s with 18x40 decomposition on 9 40 core cascade nodes
  * node hours per model day curve has flattened, but no evident minimum yet
  * waiting for Susan to generate decompositions for 383+ cores



### Week 24

#### Mon 9-Jun-2025

##### SalishSeaCast

* river obs collection failed for Salmon River
* `make_plots wwatch3 forecast2 publish` **worked** at 04:10
* `crop_gribs 12` missed 1 file; delayed runs by ~2h


##### ERDDAP

* TWDP, SEVIP & SCVIP datasets **hadn't** revert to 1970 times at 09:45
  * no reversions since I fixed the inotify limits; so issue resolved
* still no daily report email
* `ubcSSaSurfaceAtmosphereFieldsV23-02` has max time of 2025-06-06T23:00:00Z
  * definitely a problem


##### erddap-datasets

* pushed removal of `updateEveryNMillis` tag from all datasets because we shouldn't need it;
  we use a flag to trigger updates whenever our datasets change; PR#44


##### Security Updates

* Squash-merged dependabot PR to update setup-micromamba to 2.0.5 re: dependency & docs updates
  * SalishSeaNowcast
  * numeric_2024
  * erddap-datasets
  * moad_tools
  * gha-workflows
  * AtlantisCmd
  * salishsea-site


##### `sockeye`

* retried 19x39 9nodes/40cores run that was failing yesterday with fabric issues
  * queued for 13m8s; the 1st time since I started these scaling tests


##### Miscellaneous

* Checked status of scheduled GHA workflows:
  <!-- markdownlint-disable MD013 -->
  ```bash
  mamba activate gha-workflows
  python /media/doug/warehouse/MOAD/gha-workflows/gha_workflow_checker/gha_workflows_checker.py
  # re-enabled NEMO_Nowcast CodeQL action
  gh workflow enable -R 43ravens/NEMO_Nowcast CodeQL
  ```
  <!-- markdownlint-enable MD013 -->



#### Tue 10-Jun-2025


##### SalishSeaCast

* `make_plots wwatch3 forecast2 publish` **worked** at 04:06


##### ERDDAP

* still no daily report email
* `ubcSSaSurfaceAtmosphereFieldsV23-02` has max time of 2025-06-06T23:00:00Z
  * definitely a problem
  * discovered that SalishSeaNowcast still has `ubcSSaSurfaceAtmosphereFieldsV1` as the dataset id
    that is being pinged ☹️
    * fixed for now by doing a `flag/` touch


##### Miscellaneous

* MOAD group mtg; Zhiguo's last meeting


Jamie & Lin arrived for a night after their Rocky Mountaineer tour



#### Wed 11-Jun-2025


##### SalishSeaCast

* `make_plots wwatch3 forecast2 publish` **worked** at 04:07
* NEMO `forecast/11jun25` run failed with `output.abort.nc`
  * no wwatch3 runs


##### ERDDAP

* still no daily report email
* `ubcSSaSurfaceAtmosphereFieldsV23-02` has max time of 2025-06-10T23:00:00Z
  * touched to fix for today
  * updated SalishSeaNowcast config for long term fix in PR#369


##### SalishSeaNowcast

* Updated ERDDAP weather dataset ID in config & tests; PR#369
  * Revised the ERDDAP `weather` dataset ID from `ubcSSaSurfaceAtmosphereFieldsV1` to
    `ubcSSaSurfaceAtmosphereFieldsV23-02` in `nowcast.yaml` and the corresponding test file.
    This was missed when we switched to the HRDPS continental rotated lon-lat product, but the
    oversight was hidden by ERDDAP doing dataset updates every 10 minutes. The ERDDAP behaviour was
    recently dropped, resulting in this issue being surfaced.


##### Security Updates

* Squash-merged dependabot PRs to update requests to 2.32.4 re: CVE-2024-47081
  re: credentials leakage vulnerability
  * AtlantisCmd
  * salishsea-site
  * cookiecutter-analysis-repo
  * cookiecutter-MOAD-pypkg
  * ECget
  * SalishSeaNowcast
  * MoaceanParcels
  * MOAD/docs
  * SalishSeaCmd
  * NEMO-Cmd
  * moad_tools
  * Reshapr
  * SalishSeaCast/docs
  * SalishSeaTools
  * NEMO_Nowcast
  * SOG-Bloomcast-Ensemble
  * FUN
  * erddap-datasets



#### Thu 12-Jun-2025


##### SalishSeaCast

* NEMO `forecast/11jun25` run failed with `output.abort.nc`
  * no forecast2 runs
* forgot to restart manager to reload config for PR#369 re: `ping_erddap weather` to take effect
  * restarted manager to load updated config at ~14:45
* can't use VSCode to connect to `arbutus` due to it being on 18.04
* backfilled yesterday's missed runs:
  <!-- markdownlint-disable MD013 -->
  ```bash
  # on arbutus
  cd /nemoShare/MEOPAR/SalishSea/nowcast/11jun25/
  mv SalishSea_18502560_restart.nc SalishSea_18502560_restart.nc-borked
  cp ../../nowcast-green/11jun25/SalishSea_18502560_restart.nc ./

  # on skookum
  make_forcing_links arbutus nowcast+ 2025-06-11 --debug
  make_forcing_links arbutus ssh 2025-06-11

  # on arbutus
  run_NEMO arbutus forecast 2025-06-11 --debug
  # wait for forecast run to finish
  make_ww3_wind_file arbutus forecast 2025-06-11 --debug
  make_ww3_current_file arbutus forecast 2025-06-11 --debug
  run_ww3 arbutus nowcast 2025-06-11 --debug

  # wait for run to finish

  # on skookum
  download_results arbutus forecast 2025-06-11 --debug
  download_wwatch3_results arbutus nowcast 2025-06-11 --debug
  ```
  <!-- markdownlint-enable MD013 -->


##### ERDDAP

* still no daily report email
* `ubcSSaSurfaceAtmosphereFieldsV23-02` has max time of 2025-06-08T23:00:00Z
  * fixed via manual `ping_erddap weather`


##### erddap-datasets

* removed `drawLandMask` tag from all datasets because it is now set as the server default; PR#45


##### `sockeye`

* committed & pushed XIOS-ARCH changes; PR#3
  * accidentally merged rather than squash-merged on GitHub ☹️
* committed & pushed NEMO-3.6-code arch file changes
* discussed Susan getting running on #sockeye channel


##### Miscellaneous

* helped Susan with git and repo updates on `sockeye`
* helped Jose with mystery failure in dev on `graham`



#### Fri 13-Jun-2025

Worked at ESB on a whim after last day of FoMS

##### Miscellaneous

* Phys Ocgy seminar: Susan's expanded version of her CMOS talk on cross-border
  flows in the Salish Sea
* Birgit visited
* cleaned up spelling issues in this file
* helped Susan get set up and running on `sockeye`


##### SalishSeaCast

* wwatch3 forecast2 run failed due to the same `make_ww3_current_file` issue that
  prevented running nowcast/11jun25


##### ERDDAP

* still no daily report email
* `ubcSSaSurfaceAtmosphereFieldsV23-02` has max time of 2025-06-12T23:00:00Z
  * discovered that file name pattern was a file name, not a regex; fixed in PR#47
  * fixed by manual `ping_erddap weather` at ~15:00


##### erddap-datasets

* started work on setting `colorBarPalette` attr tag values to our favourite cmocean
  colour maps



#### Sat 14-Jun-2025

##### SalishSeaCast

* wwatch3 forecast2 run failed due to incorrect `run_type`
  * production working copy is messed up due to rebasing
  * fixed by re-running manually
* no Theodosia Bypass river obs for 13jun


##### ERDDAP

* still no daily report email
* `ubcSSaSurfaceAtmosphereFieldsV23-02` has correct time


##### Miscellaneous

* uploaded 2011 forcing files to `sockeye` for Susan:
  <!-- markdownlint-disable MD013 -->
  ```bash
  yyyy=2011; rsync -tv /results/forcing/atmospheric/GEM2.5/gemlam/gemlam_y${yyyy}*.nc \
    sockeye:/arc/project/st-sallen1-1/SalishSea/forcing/atmospheric/GEM2.5/gemlam/
  yyyy=2011; rsync -tv /results/forcing/sshNeahBay/obs/ssh_y${yyyy}*.nc \
    sockeye:/arc/project/st-sallen1-1/SalishSea/forcing/sshNeahBay/obs/
  yyyy=2011; rsync -tLv /results/forcing/rivers/R202108Dailies_y${yyyy}*.nc \
    sockeye:/arc/project/st-sallen1-1/SalishSea/forcing/rivers/
  yyyy=2011; rsync -tLv /results/forcing/rivers/turbidity_201906/riverTurbDaily201906_y${yyyy}*.nc \
    sockeye:/arc/project/st-sallen1-1/SalishSea/forcing/rivers/river_turb/
  yyyy=2011; rsync -tv /results/forcing/NEP36/NEP_v202209_y${yyyy}*.nc \
    sockeye:/arc/project/st-sallen1-1/SalishSea/forcing/NEP/
  ```
  <!-- markdownlint-enable MD013 -->



#### Sun 15-Jun-2025

Went to White Rock to visit Jim and see Max & Sylvia for Father's Day

##### SalishSeaCast

* wwatch3 forecast2 run failed due to incorrect `run_type`
  * production working copy is messed up due to rebasing
  * fixed by re-running manually
* no Theodosia Bypass river obs for 14jun


##### ERDDAP

* still no daily report email


##### sockeye

* figured out that `salishsea combine` failure is due to no `ksh` on compute nodes
  * `ksh` is required by the `REBUILD_NEMO/rebuild_nemo` script
  * sent email to Roman for help



### Week 25

#### Mon 16-Jun-2025

##### SalishSeaCast

* no Theodosia Bypass river obs for 15jun


##### ERDDAP

* still no daily report email


##### SalishSeaNowcast

* cherry-picked useful commits from wave plots `tenacity` PR#366 into PR#370
* closed PR#370 because using `tenacity` did not resolve the intermittent ERDDAP latency issue


##### erddap-datasets

* continued setting `colorBarPalette` attr tag values to our favourite cmocean colour maps
  * TODO:
    * turbulence vars in w grid file


##### sockeye

* Roman says that `ksh` will be deployed during July maintenance
* started testing 10 node scaling with decompositions that Susan calculated



#### Tue 17-Jun-2025

##### SalishSeaCast

* `make_plots wwatch3 forecast2 publish` failed at 04:08 with `RuntimeError: NetCDF: DAP failure`
  * failure was on Sentry Shoal plot instead of Halibut Bank
  * success on manual re-run at ~09:24
* `skookum` and `salish` lost network at ~09:45
  * communication with `arbutus` seems to have stopped at ~10:15
    * stalled workers on `arbutus`
      * `run_NEMO nowcast-green`
      * `make_ww3_wind_file`
      * `make_ww3_current_file`
      * nowcast-green run finished but there was no follow-on automation
  * restarted `log_aggregator` at ~13:54
    * didn't restart automation
  * killed `make_ww3_wind_file` and it showed up in log on `skookum`
  * attempts to manually restart automation failed; `arbutus` workers stall waiting
    for ack from `manager`
  * restarted `message_broker` and `manager`
    * still no go
  * ran `download_results nowcast-green` manually at ~15:35
  * compstaff resolved the UBC IT induced firewall issue at ~19:30
  * backfilled wwatch3 runs


##### ERDDAP

* still no daily report email



#### Wed 18-Jun-2025

##### ERDDAP

* still no daily report email


##### sockeye

* continued testing 10 and 11 node scaling with decompositions that Susan calculated
* Susan's 6mo carbon run w/ day-avg output was fastest (8m42s per model-day) and most efficient
  (1.3029 node-hr per model-day)


##### erddap-datasets

* continued setting `colorBarPalette` attr tag values to our favourite cmocean colour maps
  * TODO:
    * turbulence vars in w grid file
    * chemistry vars:
      * DIC
      * TA
      * DO - oxy?
    * CO2 flux



#### Thu 19-Jun-2025

##### ERDDAP

* still no daily report email


##### Security Updates

* Squash-merged dependabot PRs to update urllib3 to 2.5.0 re: CVE-2025-50181 and CVE-2025-50182
  re: SSRF vulnerability
  * cookiecutter-analysis-repo
  * cookiecutter-MOAD-pypkg
  * MOAD/docs
  * moad_tools
  * SalishSeaCast/docs
  * Reshapr
  * NEMO_Nowcast
  * SalishSeaCmd
  * AtlantisCmd
  * salishsea-site
  * SalishSeaTools
  * SalishSeaNowcast
  * MoaceanParcels
  * SOG-Bloomcast-Ensemble
  * FUN
  * NEMO-Cmd
  * erddap-datasets
* SalishSeaCast/docs link-check failed with "unauthorized" on `forge.ipsl.fr/nemo` links


##### SalishSeaCast

* `make_plots wwatch3 forecast2 publish` failed at 04:35 with `RuntimeError: NetCDF: DAP failure`
  * failure was on Sentry Shoal plot instead of Halibut Bank
  * success on manual re-run at ~10:15


##### SalishSeaNowcast

* resumed work on `make_plots wwatch3` reliability
  * realized that I can't easily change from ERDDAP to file system rolling forecast because the
    latter is spread over several files, not a single file as I thought
  * restored `tenacity` retrying code and deployed to `skookum`


##### SalishSeaTools

* continued reviewing `evaltools` module:
  * drop option to import `xlrd`
    * no need to specify `engine=openpyxl` in `pandas=2.3`
      * `loadPSF()`
      * `loadHakai()`
      * `load_Pheo_data()`
  * move `sqlalchemy` and `erddapy` imports to top of module
    * make them part of package env and analysis-repo env



#### Fri 20-Jun-2025

##### ERDDAP

* still no daily report email


##### SalishSeaCast

* `crop_gribs 06` delayed forecast2 runs by ~2h
* `make_plots wwatch3 forecast2 publish` worked at 06:18 after checklist reset
* `make_plots wwatch3 forecast publish` failed due to TypeError because no obs for Sentry Shoal


##### sockeye

* collected times from 10 and 11 node scaling tests


##### SalishSeaTools

* continued reviewing `evaltools` module:
  * uses in `analysis-karyn`:
    * `matchData()`
    * `varvarPlot()`
    * `displayStats()`
    * `pac_to_utc()`
    * `datetimeToYD()`
  * uses in `analysis-susan`:
    * `matchData()`
    * `loadDFOCTD()`
    * `loadDFO()`
    * `load_ferry_ERDDAP()`
    * `load_ONC_node_ERDDAP()`
    * `varvarPlot()`
    * `printstats()`
  * uses in `MOAD/analysis-becca`:
    * `matchData()`
  * uses in `MOAD/analysis-abdoul`:
    * `matchData()`
    * `loadDFOCTD()`
    * `loadDFO()`
    * `load_ferry_ERDDAP()`
    * `load_ONC_node_ERDDAP()`
    * `varvarPlot()`
    * `printstats()`
  * almost all functions are used in `analysis-elise-2`, those that aren't are used in `analysis-keegan`
  * discussion hangout with Karyn:
    * add match by salinity code to `matchData()` ???
      * `analysis-karyn/notebooks/Evaluations/OA_PugetSound_CarbonateChemModelvsObsMatches20072024_v202111_qualcontrol_MatchbySalinity.ipynb`
  * functions:
    * widely used:
      * `matchData()`
        * `_gridHoriz()`
        * `_vertNetmatch()`
        * `_binmatch()`
        * `_vvlBin()`
        * `_interpvvlZ()`
        * `_ferrymatch()`
        * `_nextfile_bin()`
        * `_getTimeInd_bin()`
        * `_getTimeInd_bin_ops()`
        * `_getZInd_bin()`
        * `index_model_files()`
      * `load_ferry_ERDDAP()`
      * `load_ONC_node_ERDDAP()`
    * obs loaders:
      * so many hard-coded paths in `/ocean/eolson/MEOPAR/obs/`
      * `loadDFOCTD()`
      * `loadDFO()`
      * `loadPSF()`
        * 567 loc !!!
        * `_lt0convert()`
      * `loadPSFCTD()`
      * `loadHakai()`
      * `load_Pheo_data()`
      * `load_WADE_data()`
        * WADE datasets stored as pickles in `/ocean/eolson/MEOPAR/obs/WADE/ptools_data/ecology/`
      * `load_CTD_data()`
    * statistics:
      * `stats()`
        * `WSS()`
        * `RMSE()`
      * `displayStats()`
      * `displayStatsFlex()`
        * `_flatten_nested_dict()`
      * `printstats()`
    * plotting:
      * `varvarScatter()`
      * `varvarPlot()`
      * `varvarIter()`
      * `tsertser_graph()`
        * `_deframe()`
    * datetime manipulation:
      * `utc_to_pac()`
      * `pac_to_utc()`
      * `pdt_to_utc()`
      * `pst_to_utc()`
      * `datetimeToDecDay()`
      * `datetimeToYD()`
    * miscellaneous:
      * `index_model_files_flex()`
        * not used in module
      * `getChlNRatio()`
        * not used in module
* added tests & docstring for `datetimeToYD()` and refactored it to use `arrow`; PR#147


##### Miscellaneous

* Phys Ocgy seminar: Shumin re: double diffusion event in Bedford Basin



#### Sat 21-Jun-2025

##### SalishSeaTools

* finished adding refactored `datetimeToYD()`; PR#147



#### Sun 22-Jun-2025

##### SalishSeaCast

* `make_plots wwatch3 forecast` ran instead of `forecast2` at 04:16 before checklist was reset
  * ran manually at ~10:52


##### sockeye

* Susan's >1d runs continue to set new records for speed and efficiency
* queued `01mar23-18x46-day-avg` to test if day-avg output only makes a difference on a 1d run



### Week 26

#### Mon 23-Jun-2025

##### SalishSeaTools

* cleaned up some docstrings, comments, and organized the imports; PR#148
* started reading `matchData()`


##### SalishSeaCmd

* merged PR#94 re: updates for running on sockeye
* started work to add support for `nibi` cluster (replacement for `graham`)



#### Tue 24-Jun-2025

Worked at ESB

##### Miscellaneous

* MOAD group mtg; Päl's last before he returns to Oslo
* updated `kudu` PyCharm to 2025.1.2


##### SalishSeaCast

* `make_plots wwatch3 forecast` ran instead of `forecast2` at 04:21 before checklist was reset
  * ran manually at ~08:40
* Fraser River turbidity data stream did not update after 03:10
* `download_results nowcast-green` took ~2h


##### erddap-datasets

* asked in #general for group advice on colour map choices


##### Security Updates

* Squash-merged dependabot PRs to update requests to 2.32.4 re: CVE-2024-47081
  re: credentials leakage vulnerability
  * SOG-Bloomcast
* Squash-merged dependabot PRs to update urllib3 to 2.5.0 re: CVE-2025-50181 and CVE-2025-50182
  re: SSRF vulnerability
  * cookiecutter-djl-pypkg
  * SOG-Bloomcast


##### SalishSeaTools

* continued review of `evaltools` module:
  * almost all netCDF access is via `netcdf4.Dataset()` rather than `xarray.open_dataset()`
    * Susan says to change to `xarray`
  * `_gridHoriz()`: see TODOs
  * most used methods for `matchData()`
    * `analysis-karyn`:
      * `vertNet`: 8, `bin`: 1
    * `analysis-susan`:
      * `bin`: 2, `ferry`: 1
    * `analysis-abdoul`:
      * `salinity`: 1, `bin`: 2, `ferry`: 1
    * `analysis-becca`:
      * `bin`: 2
  * `_vertNetmatch()`:
    * lots of dancing about `time_centered` and `time_counter`
      * code may prefer `time_centered`, but `time_counter` is more reliably present
        in model files
      * Susan says to change to `time_counter`



#### Wed 25-Jun-2025

##### SalishSeaCmd

* continued work to add support for `nibi` cluster (replacement for `graham`)


##### erddap-datasets

* continued setting `colorBarPalette` attr tag values to our favourite cmocean colour maps
* reverted PR#47 re: atmospheric datasets file patterns because it was done on the grid datasets
  that only require 1 file due to a brain fart


##### nibi

* prepared for scaling test runs
  * created `XIOS-ARCH/ALLIANCE/arch-X64_NIBI.[env|fcm|path]` files for StdEnv/2020
    * symlinked them in `XIOS-2/arch/`
  * built XIOS-2: `./make_xios --arch X64_NIBI --full --job 8`
    * failed due to no Intel license file
  * created `XIOS-ARCH/ALLIANCE/arch-GCC_NIBI.[env|fcm|path]` files for StdEnv/2023
    * symlinked them in `XIOS-2/arch/`
  * built XIOS-2: `./make_xios --arch GCC_NIBI --full --job 8`
    * success
  * loaded `StdEnv/2023` environment with modules required to build NEMO:
    <!-- markdownlint-disable MD013 -->
    ```bash
    module --force purge
    module load StdEnv/2023
    module load netcdf-fortran-mpi/4.6.1
    module load perl/5.36.1
    ```
    <!-- markdownlint-enable MD013 -->
  * created `NEMOGCM/ARCH/arch-GCC_NIBI.fcm` files for StdEnv/2023
  * experimented with `NEMOGCM/ARCH/arch-GCC_NIBI.env` but it doesn't fully work
  * built SalishSeaCast
    * success
  * built REBUILD_NEMO
* remove `mambaforge-pypy3` installation
  <!-- markdownlint-disable MD013 -->
  ```bash
  conda init --reverse --all
  conda deactivate
  rm -rf miniforge3/ Miniforge3-Linux-x86_64.sh .conda/
  rm -rf ~/.local/*
  ```
  <!-- markdownlint-enable MD013 -->
* install `miniforge3`
  <!-- markdownlint-disable MD013 -->
  ```bash
  curl -L -O \
    "https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-$(uname)-$(uname -m).sh"
  bash Miniforge3-$(uname)-$(uname -m).sh
  ```
  <!-- markdownlint-enable MD013 -->
  * allow it to auto-initialize conda
  * re-log
* configure conda/mamba:
  <!-- markdownlint-disable MD013 -->
  ```bash
  conda config --set auto_activate_base false
  conda config --add envs_dirs /project/def-allen/dlatorne/conda-envs/
  ```
  <!-- markdownlint-enable MD013 -->
  * re-log
* install SalishSeaCmd
  <!-- markdownlint-disable MD013 -->
  ```bash
  cd project/dlatorne/MEOPAR/NEMO-Cmd/
  git pull
  cd project/dlatorne/MEOPAR/SalishSeaCmd/
  git pull
  mamba env create -f envs/environment-hpc.yaml
  mamba activate salishsea-cmd
  python -m pip install --user -e ../NEMO-Cmd
  python -m pip install --user -e .
  ```
  <!-- markdownlint-enable MD013 -->
* queued 11x32 run
  * no jobs running at 12:45


##### Miscellaneous

* helped Jose understand restart files from his longer runs



#### Thu 26-Jun-2025

##### nibi

* analyzed queued jobs
* added `rrg-allen` job to queue to try to get better priority


##### SalishSeaCast

* `collect_weather 12` was slow
  * 17 files not yet processed at ~10:30
  * `crop_gribs 12` timed out at 11:00
  * `grib_to_netcdf` failed
  * 17 missing files appeared at 11:17 causing `collect_weather 12` to finish successfully and
    subsequent workers to run but automation to stall at 11:20 waiting for `grib_to_netcdf`
  * recovery:
    * `crop_gribs 12 --backfill --debug`
    * `grib_to_netcdf nowcast+`
    * automation resumed control at 11:33
* `collect_weather 18` never finished
  * `crop_gribs 18` time out at 19:20
    * re-ran manually at 20:54
    * timed out again at 04:55


##### SalishSeaTools

* simplified Excel reads; PR#149
  * dropped option to import `xlrd`
    * dropped `engine=openpyxl` because it's the default in `pandas=2.3`
      * `loadPSF()`
      * `loadHakai()`
      * `load_Pheo_data()`
* fixed `SyntaxWarning` due to single `\` characters in regexes and LaTeX label strings; PR#150
  * change regex strings to raw strings (`r""`)
  * use `\\` in LaTeX label strings
* started moving `erddapy` from in-function import to required package dependency; PR#151


##### Miscellaneous

* answered question from Crystal (on of Hal's students) relayed by Camryn about ONC DDL node obs


##### erddap-datasets

* continued setting `colorBarPalette` attr tag values to our favourite cmocean colour maps



#### Fri 27-Jun-2025

Worked at ESB after I got automation sorted out

##### SalishSeaCast

* `collect_weather 18` from yesterday never finished
  * 2nd re-try of `crop_gribs 18` time out at 04:55
  * email from Sandrine at 04:27 about operational problems with forecast runs since yesterday's 12Z
* 00Z and 06Z are on datamart server and downloaded by sarracenia, but no 18Z
* recovery started at ~07:50:
  <!-- markdownlint-disable MD013 -->
  ```bash
      collect_weather 12 2.5km
      crop_gribs 12
      crop_gribs 00
      collect_weather 00 2.5km --backfill 2025-06-27
      # kill collect_weather 06
      # kill crop_gribs 06 --fcst-date 2025-06-27
      crop_gribs 06
      collect_weather 06 2.5km --backfill 2025-06-27
  ```
  <!-- markdownlint-enable MD013 -->
* `grib_to_netcdf nowcast+` failed while NEMO forecast2 was running due to missing 18Z hours 5 & 6
* race condition management for NEMO nowcast run got overwritten by that for wwatch3 forecast2 run
* recovery started at ~09:00:
  <!-- markdownlint-disable MD013 -->
  ```bash
      # copy the cropped 011 & 012 files from the previous 26jun 12Z forecast to create
      # best estimates of 26jun 18Z 005 & 006 files
      for var in UGRD_AGL-10m VGRD_AGL-10m DSWRF_Sfc DLWRF_Sfc LHTFL_Sfc TMP_AGL-2m SPFH_AGL-2m RH_AGL-2m APCP_Sfc PRATE_Sfc PRMSL_MSL
      do
        cp /results/forcing/atmospheric/continental2.5/GRIB/20250626/12/011/20250626T12Z_MSC_HRDPS_${var}_RLatLon0.0225_PT011H_SSC.grib2 \
        /results/forcing/atmospheric/continental2.5/GRIB/20250626/18/005/20250626T18Z_MSC_HRDPS_${var}_RLatLon0.0225_PT005H_SSC.grib2
        cp /results/forcing/atmospheric/continental2.5/GRIB/20250626/12/012/20250626T12Z_MSC_HRDPS_${var}_RLatLon0.0225_PT012H_SSC.grib2 \
        /results/forcing/atmospheric/continental2.5/GRIB/20250626/18/006/20250626T18Z_MSC_HRDPS_${var}_RLatLon0.0225_PT006H_SSC.grib2
      done
      # wait for wwatch3 forecast2 run to finish
      grib_to_netcdf nowcast+
  ```
  <!-- markdownlint-enable MD013 -->
* LiveOcean was delayed until ~11:15


##### cookiecutter-analysis-repo

* added `erddapy` to notebooks env description re: it becoming a required dependency for SalishSeaTools


##### Miscellaneous

* Phys Ocgy seminar: Roger Pieters re: meromixis in a mine tailings lake in NWT
* discussed time line and details of 17jun eos.ubc.ca firewall issue with Susan


##### SalishSeaTools

* started work on test for `load_ferry_ERDDAP()`



#### Sat 28-Jun-2025

##### FUN

* continued creating 2026 pension income scenario


##### SalishSeaCast

* wwatch3 forecast run was reported as crashed because `watch_ww3` didn't find a time step value
  * run appears to have finished normally on `arbutus`
  * successfully manually ran `download_wwatch3_results forecast`


##### ERDDAP

* atmospheric forcing dataset had not updated since 26jun
  * message out "outer axis overlap" between 26jun and 27jun
  * touched dataset in `hardFlag/` to force full reload



#### Sun 29-Jun-2025

##### SalishSeaCast

* `make_plots nowcast comparison` failed due to inaccessible atmospheric forcing dataset on ERDDAP


##### ERDDAP

* atmospheric forcing dataset did not load:
  <!-- markdownlint-disable MD013 -->
  ```text
    ubcSSaSurfaceAtmosphereFieldsV23-02: Outer axis overlap between files.
    max=1.7509788E9 for /results/forcing/atmospheric/continental2.5/nemo_forcing/hrdps_y2025m06d26.nc
    is greater than
    min=1.7509608E9 for /results/forcing/atmospheric/continental2.5/nemo_forcing/hrdps_y2025m06d27.nc
  ```
  <!-- markdownlint-enable MD013 -->



### Week 27

#### Mon 30-Jun-2025

Last Cardiac Rehab session.

##### SalishSeaCast

* `make_plots wwatch3 forecast2 publish` failed at 04:17 with `RuntimeError: NetCDF: DAP failure`
  after `tenacity` did its job
  * re-ran manually at 09:38
* `make_plots nowcast comparison` failed due to inaccessible atmospheric forcing dataset on ERDDAP


##### ERDDAP

* confirmed Susan's suspicion that one of the `time_counter` values in
  `/results/forcing/atmospheric/continental2.5/nemo_forcing/hrdps_y2025m06d27.nc` was incorrect;
  `time_counter[0]`
  * fix:
    <!-- markdownlint-disable MD013 -->
    ```python
    ds.time_counter.data[0] = pandas.to_datetime("2025-06-27T00:00:00")
    encoding = {
        "time_counter": {
            "calendar": "gregorian",
            "units": "seconds since 1970-01-01 00:00",
            "dtype": float,
        },
    }
    encoding.update({var: {"zlib": True, "complevel": 4} for var in ds.data_vars})
    ds.to_netcdf("hrdps_y2025m06d27.nc.fixed", encoding=encoding, unlimited_dims=("time_counter",))
    ```
    <!-- markdownlint-disable MD013 -->
* changed `colorBarPalette` attr tag values to our favourite cmocean colour maps; PR#49
* reverted PR#47 re: atmospheric datasets file patterns because it was done on the grid datasets
  that only require 1 file due to a brain fart;PR#50



## July

<!-- markdownlint-disable MD001 -->
#### Tue 1-Jul-2025
<!-- markdownlint-enable MD001 -->

**Statutory Holiday** - Canada Day

##### Security Updates

* Squash-merged dependabot PRs to update pillow to 11.3.0 re: CVE-2025-48379
  re: buffer overflow vulnerability
  * SalishSeaTools
  * SalishSeaNowcast



#### Wed 2-Jul-2025

##### SalishSeaCast

* `make_plots wwatch3 forecast` ran instead of `forecast2` at 04:04 before checklist was reset
  * ran manually at ~08:40
  * test-reverted PR#364 re: wwatch3 run type selection for plots because it is causing this problem
    * restarted manager for update `next_workers` module to take effect


##### 2x resolution SalishSeaCast

* refreshed mine and Susan's memories on where we left off in late-March
  * Susan needs to finish detailed review of row 13


##### SalishSeaTools

* continued work on test for `load_ferry_ERDDAP()`
  * created `test_evaltools_loaders` module
  * renamed `test_evaltools` module to `test_evaltools_datetime`
  * added tests for `load_ferry_ERDDAP()` based on initial generation by PyCharm AI
    * custom variables implementation is problematic; talk to Susan
  * added tests for `load_ONC_node_ERDDAP()` based on initial generation by PyCharm AI



#### Thu 3-Jul-2025

##### sockeye

* collected run time data from Susan's recent runs
  * 20x41 10 node runs are most efficient ~7m40s NEMO per model day
  * still waiting for a run that includes `salishsea combine`


##### nibi

* 11x32 1 node jobs have been queued since 25 & 26 jun due to unavailable nodes


##### SalishSeaCast

* `crop_gribs 12` failed with many errors:
    <!-- markdownlint-disable MD013 -->
    ```text
    ERROR [crop_gribs] skipping corrupted Message
    gribapi.errors.PrematureEndOfFileError: End of resource reached when reading message
    ```
    <!-- markdownlint-enable MD013 -->
  * errors are from hour 036 `APCP_Sfc` file; the rest of hour 036 and hours 039-048 were not processed
  * confirmed with `crop_gribs 12 --var APCP_Sfc --var-hour 36 --debug`
    * unexpected end of file
    * sarracenia log shows: "[ERROR] util/writelocal mismatched file length writing ..."
    * manually downloaded `APCP_Sfc` file from hpfx and got a larger one
    * successfully ran `crop_gribs 12 --var APCP_Sfc --var-hour 36 --debug`
    * successfully ran `crop_gribs 12 --var DLWRF_Sfc --var-hour 36 --debug`
    * successfully ran `crop_gribs 12 --backfill` to restart automation at ~10:10
* `make_plots wwatch3 forecast publish` failed at 12:51 with `RuntimeError: NetCDF: DAP failure`
  after `tenacity` did its job
  * re-ran manually at 16:18


##### SalishSeaTools

* finished on tests for `load_ferry_ERDDAP()` and refactored it



#### Fri 4-Jul-2025

Worked at ESB.

##### sockeye

* collected run time data from Susan's recent runs


##### Miscellaneous

* Becca gave a practice version of a talk she will give next week at Hakai
* read https://docs.alliancecan.ca/wiki/Advanced_MPI_scheduling and learned of `srun`
  * the syntax we use with `mpirun` can also be used with `srun` (see its docs);
    that may result in better performance due to avoiding "a mismatch between the
    resources allocated by Slurm an those used by OpenMPI"
* applied for access to `rorqual`


##### ERDDAP

* explored CF standard name table versions re: recommendation to use v91
  * our metadata presently says v29 (from 2015)


##### Minecraft

* checked mods, etc. for releases compatible with 1.21.6:
  * sodium: yes
  * lithium: yes, and 1.21.7 too
  * malilib: yes, and 1.21.7 too
  * minihud: yes
  * tweakeroo: yes
  * iris: yes, and 1.21.7 too
  * fresh animations: yes, and 1.21.5 to 1.21.7



#### Sat 5-Jul-2025

##### SalishSeaCast

* `make_plots wwatch3 forecast publish` failed at 11:53 with `RuntimeError: NetCDF: DAP failure`
  after `tenacity` did its job
  * re-ran manually at 18:20



#### Sun 6-Jul-2025

##### sockeye

* collected run time data from Susan's recent runs



### Week 28

#### Mon 7-Jul-2025

##### SalishSeaCast

* discovered that yesterday `make_plots wwatch3 forecast2` ran instead of `make_plots wwatch3 forecast`
  * happened because `make_plots wwatch3 forecast2` ran after the morning checklist reset,
    so there were both `forecast2` and `forecast` keys in the `WWatch3 run` checklist item
  * the situation is always the case, so there is no way to choose a run type and run date selection
    strategy that is robust with respect to wwatch3 runs finishing before or after checklist reset
  * after discussion with Susan, decided to try using race condition management to force checklist
    reset to happen after both NEMO and WWatch3 plots have finished
    * that won't work because there isn't enough uniqueness in the process flows after preliminary
      NEMO and WWatch3 runs
  * least bad option is to return to PR#364 re: wwatch3 run type selection for plots and live with
    the fact that it will sometime do `forecast` when it should do `forecast2`
    * restarted manager for update `next_workers` module to take effect


##### Miscellaneous

* updated PyCharm on `khawla` to 2025.1.3
* replied to email from Jan & Troy re: SalishSeaCast on NANOOS NVS



#### Tue 8-Jul-2025

Worked at ESB

##### SalishSeaCast

* `crop_gribs 12` waited until time out to process 1 file


##### Miscellaneous

* MOAD group mtg; see whiteboard
* updated PyCharm on `kudu` to 2025.1.3


##### erddap-datasets

* changed `standard_name_vocabulary` to `CF Standard Name Table v91`; PR#51


##### NEMO-Cmd

* changed `cmd.split()` to `shlex.split(cmd)` in `run` plugin re: issue #8; PR#108



#### Wed 9-Jul-2025

##### SalishSeaCast

* `upload_forcing orcinus forecast2` failed with "permission denied"
* `make_plots wwatch3 forecast` ran instead of `forecast2` at 04:04 before checklist was reset
  * ran manually at ~09:06
* `upload_forcing orcinus nowcast+` failed with "permission denied"
  * write permission to `/home/sallen/` where forcing files are stored got revoked; Susan restored it


##### SalishSeaTools

* finished on tests for `load_ONC_node_ERDDAP()` and refactored it
  * squash-merged PR#151


##### salishsea-site

* email from UBC IT security re: debug log page security concerns



#### Thu 10-Jul-2025

##### sockeye

* collected run time data from Susan's recent runs
* sent email to arc.support re: possible incomplete deployment of compute node image that includes `ksh`
  * Ryan replied that `ksh` image deployment had been troublesome but is should stabilize soon


##### nibi

* users who have pending whole-node jobs:
  * islamm65
  * cournoyc
* looked for slurm constraints to use `nibi` nodes on `graham` and found that the test nodes that were
  on `graham` have been moved back to `nibi`
* sent email to support@tech.alliancecan.ca asking about `nibi` test jobs


##### SalishSeaTools

* updated intersphinx inventory URLs for numpy & scipy; PR#153
  * intersphinx inventory has moved: https://docs.scipy.org/doc/scipy/reference/objects.inv -> https://docs.scipy.org/doc/scipy/objects.inv
  * intersphinx inventory has moved: https://docs.scipy.org/doc/numpy/objects.inv -> https://numpy.org/doc/stable/objects.inv
* started work on fixing SyntaxWarning messages from various modules; PR#154


##### erddap-datasets

* updated env to Python 3.13; PR#52
  * updated envs on `khawla` and `skookum`



#### Fri 11-Jul-2025

Worked at ESB

##### SalishSeaCast

* `make_plots wwatch3 forecast2 publish` failed at 06:38 with `RuntimeError: NetCDF: DAP failure`
  after `tenacity` did its job
  * re-ran manually at 08:45
* `download_results nowcast-green` took ~90 minutes


##### nibi

* users who have pending whole-node jobs:
  * islamm65
  * abadchi
* users whose whole-node jobs left the queue
  * cournoyc: cancelled


##### MIDOSS/docs

* un-archived repo
* changed Rachael's email and website addresses
* removed `sphinx-linkcheck` badges because the workflow outputs disappear in archived repos
* tried to trigger a new build on readthedocs
  * it failed because the config is outdated
  * updated config to new readthedocs API in VSCode web editor on GitHub
  * manually triggered new docs build on readthedocs
* re-archived repo


##### Miscellaneous

* Phys Ocgy seminar: Vicente re: PBDEs modelling
* reviewed VSCode v102 release notes
* updated `kudu` to PyCharm 2025.1.3.1
* helped Susan with Reshapr not recognizing persistent dask cluster
  * suspect Reshapr exception type bug due to change in dask


##### salishsea-site

* update to Python 3.13; ref PR#77 for update to 3.12; PR#119
  * change dev, prod & rtd envs to 3.13
  * change `pyproject.toml` to 3.13
  * change CI, sphinx-linkcheck & deployment workflow to 3.13
  * change index doc & README to 3.13 for pkg dev
* release v25.1
* update prod env on `skookum`



#### Sat 12-Jul-2025

##### SalishSeaCast

* `upload_forcing orcinus nowcast+` failed due to already existing file?
  * `/home/sallen/` has disappeared from `orcinus`
  * email to Mark
  * fixed around noon; tested at ~16:00


##### nibi

* users who have pending whole-node jobs:
  * cournoyc
  * islamm65
  * lamming6
  * abadchi


##### Minecraft

* checked mods, etc. for releases compatible with 1.21.7:
  * sodium: yes
  * lithium: yes
  * malilib: yes
  * minihud: yes
  * tweakeroo: yes
  * iris: yes
  * fresh animations: yes



#### Sun 13-Jul-2025

##### SalishSeaCast

* `crop_gribs 12` waited until time out to process 1 file



### Week 29

#### Mon 14-Jul-2025

##### SalishSeaCast

* `make_plots wwatch3 forecast2 publish` failed at 04:33 with `RuntimeError: NetCDF: DAP failure`
  after `tenacity` did its job
  * re-ran manually at 09:25
* `upload_forcing orcinus forecast2`, `nowcast+`, and `turbidity` failed due to SSH key issue
* `nowcast-blue run` failed:
  * zonal velocity >20m/s at 2, 393, 22
  * Susan fixed `nowcast-green.202111/13jul25/` restart file
  * `make_forcing_links arbutus nowcast+` at 09:55 to restart automation


##### nibi

* users who have pending whole-node jobs:
  * islamm65
  * lamming6
  * cournoyc
  * abadchi
  * doppenbe
  * arashy: 6 4 node, 128 core jobs scheduled for 19jul
* no success jobs in the past 10 days from queued users
* email from Liam Sbarro at ARC confirming that delay is ue to commissioning, though he is not part
  of `nibi` team


##### Miscellaneous

* updated `khawla` to PyCharm 2025.1.3.1


##### SalishSeaTools

* finished fixing SyntaxWarning messages from various modules; PR#154
  * also cleaned up imports and added module docstring & copyright info to `loadDataFRP` module
    where many of the regex SyntaxWarning messages were coming from


##### salishsea-site

* started work on adding access control to debug log to make UBC IT security folks happy:
  * `views.salishseacast.nowcast_logs()` just renders file name passed as the `filename` path element
    in the request matchdict through the `string` renderer
  * plan:
    * detect if `filename` value contains `debug`
    * if so, compare `token` parameter value to values in "secret" `debug_log_tokens.txt` file
    * if `token` parameter is missing, or value isn't in file raise `HTTPForbidden`



#### Tue 15-Jul-2025

Worked at ESB

##### SalishSeaCast

* `upload_forcing orcinus forecast2` worked overnight
* backfill nowcast-agrif:
  <!-- markdownlint-disable MD013 -->
  ```bash
  upload_forcing orcinus nowcast+ 2025-07-14 --debug
  upload_forcing orcinus turbidity 2025-07-14 --debug
  ```
  <!-- markdownlint-enable MD013 -->
* `download_live_ocean` timed out out at 12:20
  * restarted at ~12:50
  * success at 14:47
* email from Parker about changing LiveOcean to s3 storage at UW


##### nibi

* other users who have pending whole-node jobs:
  * cournoyc
  * arashy: 5 4 node, 128 core jobs not scheduled
  * doppenbe
  * haddaram
* 1 successful job in the past 10 days from queued users
  * arashy: 4 nodes, 128s core ran on g[13,17,23,31] for 26m


##### rorqual

* continued setup on `rorqual`
  * created `links/projects/def-allen/SalishSea/` and make it group writable
  * confirmed that `tmux` is available on `beluga` so that I can `rsync`
    156G of forcing files from `projects/def-allen/SalishSea/forcing/` in a
    single session
  * started `rsync` in `dlatorne-rsync-rorqual` tmux session on `beluga`


##### SalishSeaNowcast

* updated LiveOcean URL templates in config; PR#373
  * deployed branch to `skookum`
  * restarted manager to load updated config for tomorrow's runs



#### Wed 16-Jul-2025

##### Miscellaneous

* Sharcnet webinar: Julia Threads, Ed Armstrong, Guelph
  * shared memory, bu separate CPU state
  * first 15 minutes are great intro to low level computing: cpu, registers, RAM
  * Julia tasks are coroutines, green threads, or lightweight threads
    * tasks have to be explicitly scheduled and waited for to complete
    * tasks are only runnable once
    * `@spawn` creates and schedules a task, `fetch()` gets the result of the task
  * `Threads.@threads` distributes loop iteration across threads
  * `mutex` == mutual exclusion lock or reentrant lock
    * programmer's responsibility
    * deadlocks are a problem; locks acquired out of order
      * avoid long lock holds
  * `Atomic`: great for counters; maps to CPU atomic instructions


##### SalishSeaCast

* `make_plots wwatch3 forecast2 publish` failed at 04:43 with `RuntimeError: NetCDF: DAP failure`
  after `tenacity` did its job
  * re-ran manually at 09:00
* 12Z downloads didn't start until 09:37; `crop_gribs 12` finished at 10:32
* `download_live_ocean` worked correctly from new s3 storage via PR#373


##### nibi

* my jobs have now both changed to Priority as their reason for queuing
* other users who have pending whole-node jobs:
  * cournoyc
  * arashy: 5 4 node, 128 core jobs not scheduled
  * doppenbe
  * haddaram
  * zemskova
* no new successful jobs in the past 10 days from queued users


##### SalishSeaNowcast

* squash-merged LiveOcean URL templates in config; PR#373
  * restored `skookum` to `main` branch


##### salishsea-site

* continued work on adding access control to debug log to make UBC IT security folks happy
  * PR#120



#### Thu 17-Jul-2025

Worked at ESB before published papers celebration at Brown's

##### SalishSeaCast

* `make_plots wwatch3 forecast2` ran for 16jul instead 17jul` at 04:32 before checklist was reset
  * ran manually at ~09:30
* `upload_forcing orcinus turbidity` failed due to SSH key issue


##### salishsea-site

* deployed PR#120 to `skookum` to test debug log token access:
  * added token envvar
  * deployed branch
  * shutdown and restarted supervisor to add token envvar
  * confirmed expected operation


##### nibi

* other users who have pending whole-node jobs:
  * cournoyc
  * arashy: 5 4 node, 128 core jobs not scheduled
  * doppenbe
  * haddaram
  * azek88: 2 1 node, 192 core jobs
  * blaisbru
  * jgleason: 2 1 node, 192 core jobs
  * jvalenti
  * awpye: 2 1 node, 192 core jobs
  * kbwarren
* jobs in the past 10 days from queued users
  * arashy: 4 nodes, 128s core ran on g[13,17,23,31] for 26m
  * blaisbru: 3 fails


##### SalishSeaTools

* started `matchData()` refactoring and adding tests; PR#155
  * extracted column validation logic into `_reqd_cols_in_data_frame()`
  * extracted file types list minimization logic into `_calc_file_types()`



#### Fri 18-Jul-2025

##### SalishSeaCast

* `upload_forcing orcinus forecast2` failed due to SSH key issue


##### nibi

* both test runs failed with `line 76 -> [ id = GLS_k, U = field ] object was not found.` error
  during XIOS setup
  * caused by NEMO build on year-old `graham-stdenv2023` branch that is out of sync with recent
    `v202111/field_def.xml`
  * switched branch and build NEMO clean
  * queued new `01mar23-nibi-rrg-11x32` run, scheduled for 2025-07-23T11:17:10


##### SalishSeaTools

* continued `matchData()` refactoring and adding tests; PR#155
  * extracted file map inversion logic into `_invert_filemap()`



#### Sat 19-Jul-2025

##### Minecraft

* checked mods, etc. for releases compatible with 1.21.8:
  * sodium: yes
  * lithium: yes
  * malilib: yes
  * minihud: no
  * tweakeroo: no
  * iris: no
  * fresh animations: no



#### Sun 20-Jul-2025

##### SalishSeaCast

* `make_plots wwatch3 forecast` ran for 19jul instead `forecast2` for 20jul` at 04:15
  * ran manually just in time at ~11:07


##### nibi

* `01mar23-nibi-rrg-11x32` run, schedule updated to 2025-07-20T16:10:00
  * pushed back to 2025-07-23T17:11:49 within 2h or scheduled start ☹️



### Week 30

#### Mon 21-Jul-2025

##### SalishSeaCast

* `make_plots wwatch3 forecast2 publish` failed at 04:36 with `RuntimeError: NetCDF: DAP failure`
  after `tenacity` did its job
  * re-ran manually at 09:15


##### salishsea-site

* squash-merged PR#120 re: debug log token access


##### SalishSeaNowcast

* added envvar for debug log token to `skookum` deployment docs; PR#374


##### nibi

* `01mar23-nibi-rrg-11x32` run finished overnight
  * almost the same performance as Jose's run: 10m49s + 1m combine
* insta-run on subsequent tests:
  * 14x25: 11:24
  * 15x23: 11m37s; 1st attempt stalled due to system issue
  * 21x38: 2 nodes; 7m3s + 1m3s combine, less efficient node-h/model-d
  * 21x37: 2 nodes; 7m2s + 1m2s combine
  * 29x44: 3 nodes; 7m2s + 58s combine
  * 21x61: 3 nodes; 6m51s + 1m14s combine
  * 11x32, 31 days: 9m34s/day + 50s combine
  * 14x25, 31 days: 10m15s/day + 53s combine
  * 21x37, 31 days: 6m51s/day + 58s combine; 0.2281 NEMO-h/model-d
* experimented unsuccessfully with `srun` instead of `mpirun` in 11x32 job



#### Tue 22-Jul-2025

Worked at ESB

##### SalishSeaCast

* `crop_gribs 12` waited until time out at 11:18 to process 1 file
* `make_turbidity_file` failed due to insufficient obs
  * last update on website was at 03:10
  * `upload_forcing turbidity` persisted 21jul file via symlink
* `make_plots wwatch3 forecast publish` failed at 13:59 with `RuntimeError: NetCDF: DAP failure`
  after `tenacity` did its job
  * re-ran manually at ~15:30


##### nibi

* `nibi.alliancecan.ca` is now working
  * added host alias to `kudu` ssh config
* committed and pushed `XIOS-ARCH` files for StdEnv/2023 GCC build
* committed and pushed `NEMO-3.6-code` arch file for StdEnv/2023 GCC build
* squash-merged SalishSeaCmd PR#97 to add `nibi` support
* committed and pushed example `nibi` run YAML file
* created temporary docs for `nibi` in canvas in #alliance-hpc channel



#### Wed 23-Jul-2025

##### SalishSeaCast

* `make_plots wwatch3 forecast2 publish` failed at 04:35 with `RuntimeError: NetCDF: DAP failure`
  after `tenacity` did its job
  * re-ran manually at ~09:25
* `make_turbidity_file` failed due to insufficient obs
  * updates on website had resumed by 09:10
  * `upload_forcing turbidity` persisted 21jul file via symlink


##### SalishSeaCmd

* closed PR#62 re: StdEnv/2023 on `graham` and deleted `graham-stdenv2023` branch
* released v25.1 re: `nibi`


##### SalishSeaTools

* received PR#156 to update Earth radius in `geo_tools.haversine()` to be consistent with NEMO source
  code value in `DOM/phycst.F90`
  * asked Susan for review
* continued `matchData()` refactoring and adding tests; PR#155
  * changed error message to KeyError in `_calc_file_types()`
  * discussed geo-ref processing (maskName, meshPath, navlon, navlat, omask, nemops) with Susan
    * agreed to not implement handling of atmospheric forcing grid for now
  * started stepping through code with a modified version of Susan's `comparison_script.py` module


##### salishsea-site

* started work on removing VHFR-FVCOM pages; PR#121
  * `views.fvcom.py` module
  * `fvcom.*` routes in `__init__.py`
  * templates:
    * `fvcom/results_index.mako`
    * `fvcom/publish.mako`
  * mentions in `views.figures.py` module
  * link in `templates/nav.mako`



#### Thu 24-Jul-2025


##### SalishSeaTools

* continued `matchData()` refactoring and adding tests; PR#155
  * continued stepping through code with a modified version of Susan's `comparison_script.py` module
  * simplified data frame sorting logic
  * renamed required columns list
  * refactored mesh mask handling to use `xarray`, simplify code, and only load lons/lats when needed
  * drop support for atmospheric data matching
  * change `meshPath` to `mesh mask_path` and make it a mandatory arg
* started stepping through `index_model_files()`
  * used PyCharm AI to generate unit test for it, but they needed work...



#### Fri 25-Jul-2025

##### SalishSeaNowcast

* email from Mark re: Luster file system collapse on `orcinus` due to loss of metadata volumes
  * `upload_forcing forecast2` failed
  * `upload_forcing nowcast+` failed
  * `upload_forcing turbidity` failed
* `get_onc_ctd SEVIP` failed due to boolean index array size mismatch during API request


##### SalishSeaTools

* continued `matchData()` refactoring and adding tests; PR#155
  * renamed variables and args for improved descriptiveness and consistency with Python conventions
    * `lonvar`, `latvar`
    * `sdim`
    * `preIndexed`
    * `fdict`
    * `filemap`
  * dropped unused `fid` arg
  * renamed internal variables
  * renamed `_invert_filemap()` to `_calc_filetype_model_vars()`
  * added API docs
  * added a couple of unit tests
* started looking at Karyn's `_salinityMatch()`



#### Sat 26-Jul-2025

##### SalishSeaCast

* `make_plots wwatch3 forecast2 publish` failed at 06:32 with `RuntimeError: NetCDF: DAP failure`
  after `tenacity` did its job
  * re-ran manually at ~08:40


##### SalishSeaTools

* continued `matchData()` refactoring and adding tests; PR#155
  * refactored `flist` to `file_lists` using dict comprehension
  * got idea for matching handler based on dict of `lambdas` from PyCharm AI; that gets around the
    issue of the matcher functions having different signatures that was blocking my dict-based idea



#### Sun 27-Jul-2025

Watched the `nibi` upgrade video on training.sharcnet.ca

Rode the Sanctuary ride.



### Week 31

#### Mon 28-Jul-2025

##### SalishSeaCast

* `make_plots wwatch3 forecast2 publish` failed at 04:27 with `RuntimeError: NetCDF: DAP failure`
  after `tenacity` did its job
  * re-ran manually at ~08:50

* `crop_gribs 12` waited until time out at 11:00 to process 1 file


##### nibi

* requested a 3h 2-core, 8 Gb interactive session via OnDemand to see what can be done with item
  * video suggests that this is how to run Jupyter
  * queued for an annoyingly long time
* experimented with automation key; not configured yet on `nibi`


##### SalishSeaTools

* discussed `matchData()` refactoring with Susan:
  * she approves of signature changes so far
  * decided to leave existing quasiCamelCase args as is unless they are changed for code refactoring
  * agreed to change `fastSearch` to a arg for the high-res lon/lat to model indices mapping file path
    (presently hard-coded) with a default of `None` to disable fast indexing
  * she approves of the dict of `lambda` matching method handler that the PyCharm AI suggests
* continued `matchData()` refactoring and adding tests; PR#155
  * simplified start/end date handling with `or` statements and f-string prints
  * started refactoring matching function calls into dict-of-lambdas function



#### Tue 29-Jul-2025

Worked at ESB

##### Miscellaneous

* MOAD group mtg; see whiteboard


##### salishsea-site

* squash-merged removal of VHFR-FVCOM pages; PR#121
* fixed Automation Monitoring page failure with `KeyError: 'token'`; PR#122
  * forgot to add `token` parameters to log page URLs in automation monitoring
    page template
  * deployed branch to `skookum` for testing




#### Wed 30-Jul-2025

##### Miscellaneous

* HPC update webinar
  * Sergey Mashchenko
  * guideline for scalability is 25% core waste limit
    * https://docs.alliancecan.ca/wiki/Scalability
    * https://en.wikipedia.org/wiki/Scalability_testing
  * GPUs are generally under-utilized due to jobs too small to saturate and spiky use patterns
    * now using GPU segmentation technology (MIGs) to split GPUs into 8ths
  * interconnect changes
    * `nibi` is the only cluster that switched from InfiniBand to Ethernet
      * I should test on `fir` and `rorqual`
  * file systems
    * `nibi` and `trillium` are VAST
      * automatic deduplication and **compression**
    * `fir` is Lustre
    * `rorqual` has `~/links/`
    * use absolute paths in job scripts
    * scratch accounting
      * 1T soft quota
      * >1T triggers 60d over-quota grace period
      * >60d hard-quota limit; must reduce to <1T to reset quota
    * may introduce "whole sub-node" partitions for ~32 cores
    * `StdEnv/2020` is hidden and deprecated, but still loadable if needed
    * interactive access
      * OnDemand webinar on 27-Aug
    * mini-graham dies on 1-Sep


##### nibi

* portal.nibi.sharcnet.ca is starting to come to life



#### Thu 31-Jul-2025

##### SalishSeaCast

* `make_plots wwatch3 forecast2 publish` failed at 06:46 with `RuntimeError: NetCDF: DAP failure`
  after `tenacity` did its job
  * re-ran manually at ~08:00


##### SalishSeaTools

* continued `matchData()` refactoring and adding tests; PR#155
  * refactored matching function calls into dict-of-lambdas function
  * changed `fastSearch` to a arg for the high-res lon/lat to model indices mapping file path
    (presently hard-coded) with a default of `""` to disable fast indexing


##### salishsea-site

* squash-merged fix for Automation Monitoring page failure with `KeyError: 'token'`; PR#122
  * GHA automation successfully deployed it
* released v25.2



## August

<!-- markdownlint-disable MD001 -->
#### Fri 1-Aug-2025
<!-- markdownlint-enable MD001 -->

Worked at ESB

##### Miscellaneous

* Phys Ocgy seminar: Stephanie's summer students
* completed annual COI declaration


##### nibi

* portal.nibi.sharcnet.ca is mostly fully alive
* experimented with interactive session via OnDemand
  * Mate desktop
  * no ssh agent connection, so couldn't clone `analysis-doug` from GitHub to
    test `jupyterlab`


##### SalishSeaNowcast

* fixed redirected rtd badge links and broken arbutus cloud docs link; PR#375



#### Sat 2-Aug-2025

##### Vacation

* prep for trip to Nelson
* picked up Modo 2024 Rogue
* dinner at Provisions



#### Sun 3-Aug-2025

##### Vacation

* drove from home to Longbeach near Nelson
* stops:
  * fuel in Hope
    * Modo card failed at Esso, but worked at Chevron
  * lunch at Fannie's in Princeton
  * produce at B&J's in Keremeos
  * rest stop on east side of Poulson pass



### Week 32

#### Mon 4-Aug-2025

**Statutory Holiday** - BC Day

##### Vacation

* rode out and back from Mountain Station to the beaver/grizzly bear meadow just south of Cottonwood
  Lake
  * steady climb
  * 30+ minute descent on return with only a few dog walkers


##### SalishSeaCast

* `make_plots wwatch3 forecast2 publish` failed at 04:34 with `RuntimeError: NetCDF: DAP failure`
  after `tenacity` did its job
  * re-ran manually at ~08:25
* `make_plots wwatch3 forecast publish` failed at 11:40 with `RuntimeError: NetCDF: DAP failure`
  after `tenacity` did its job
  * re-ran manually at ~16:40



#### Tue 5-Aug-2025

##### Vacation

* rode out and back to Procter Park with a stop at the Procter store for ice cream on the way back
  * discovered that middle chainring on Gunnar is skipping with the new chain when I stand


##### SalishSeaCast

* `make_plots wwatch3 forecast2 publish` failed at 04:31 with `RuntimeError: NetCDF: DAP failure`
  after `tenacity` did its job
  * re-ran manually at ~09:10
* `make_plots wwatch3 forecast publish` failed at 11:31 with `RuntimeError: NetCDF: DAP failure`
  after `tenacity` did its job



#### Wed 6-Aug-2025

##### Vacation

* drove to Winlaw with a plan of riding part of the Slocan Valley trail, but the rain came on while
  we were having lunch at Sleep is for Sissies and we drove back to Longbeach after a brief stop at
  the Winlaw trailhead


##### SalishSeaCast

* `make_plots wwatch3 forecast2 publish` failed at 04:18 with `RuntimeError: NetCDF: DAP failure`
  after `tenacity` did its job
  * re-ran manually at ~09:00


##### NEMO-Cmd

* replaced permission denied link to https://modules.sourceforge.net/ in
  `docs/run_description_file/3.6_yaml_file.rst` with
  https://docs.alliancecan.ca/wiki/Utiliser_des_modules/en; PR#109



#### Thu 7-Aug-2025

##### Vacation

* rode to Balfour and back
  * explored Upper Balfour Rd and forest road up to power line cut
  * coffee & snacks at bakery at ferry; cinnamon buns were all sold out
  * finished the windy ride back to Longbeach just as the rain started


##### SalishSeaCast

* `make_plots wwatch3 forecast2 publish` failed at 04:38 with `RuntimeError: NetCDF: DAP failure`
  after `tenacity` did its job
  * re-ran manually at ~08:15
* `make_plots wwatch3 forecast publish` failed at 11:34 with `RuntimeError: NetCDF: DAP failure`
  after new `tenacity` use did its job
  * re-ran manually at ~14:00


##### SalishSeaNowcast

* tried another way of handling `RuntimeError: NetCDF: DAP failure` in `make_plots wwatch3`
  * added `.load()` call on dataset from ERDDAP
  * moved ERDDAP dataset loading to a separate function so that it can be wrapped with `@tenacity()`
  * copied updated code to `skookum` on `main` branch for testing



#### Fri 8-Aug-2025

##### Vacation

* drove to Shutty Bench, north of Kaslo on hwy 31
  * rode to Lardeau and back
  * best ever cinnamon buns at Sal's Bakery in house kitchen
  * longest, climbiest, highest TSS ride I've done since last August



#### Sat 9-Aug-2025

##### Vacation

* drove to Cottonwood Lake, north of Nelson on hwy 6
  * rode to Ymir and back
  * set new power bests on the long steady climb back
  * Training Peaks tagged the ride with an FTP increase from 190 to 192 W



#### Sun 10-Aug-2025

##### Vacation

* rode to Sunshine Beach for Sunday market, then on to Procter for olive oil and cinnamon buns
  at the café


##### SalishSeaNowcast

* `make_plots wwatch3 forecast publish` failed at 11:37 with `RuntimeError: NetCDF: DAP failure`
  after new `tenacity` use did its job
  * re-ran manually at ~15:11



### Week 33

#### Mon 11-Aug-2025

##### Vacation

* rode the Slocan Trail from Winlaw to Slocan and back
  * early start and low pace due to heat
  * ice cream at Mountain Valley Station
  * lunch at Sleep is for Sissies


##### Security Updates

* Squash-merged dependabot PRs to update `pre-commit` to 6.0.0 re: feature & dependency updates, and
  bug fixes
  * NEMO_Nowcast
  * SalishSeaCast/docs
  * SalishSeaNowcast
  * NEMO-Cmd
  * salishsea-site
  * SalishSeaCmd
  * erddap-datasets
  * SOG-Bloomcast-Ensemble
  * MoaceanParcels
  * cookiecutter-MOAD-pypkg
  * MOAD/docs
  * gha-workflows
  * SalishSeaTools
  * Reshapr
  * moad_tools
  * AtlantisCmd
* Squash-merged dependabot PRs to update `actions/checkout` to 5.0.0 re: update to use node 24
  * moad_tools
  * gha-workflows



#### Tue 12-Aug-2025

##### Vacation

* hiked several trails in a loop in Kokanee Creek Park
  * Canyon Trail to lookout
  * trail across Kokanee Glacier access road down to MTB area trailhead
  * up through MTB climb trails to a higher point on the Kokanee Glacier road
  * back to Canyon trail
  * down Woodland trail to Kokanee Creek camping area
  * along beach and Grasslands trail to nature centre for ice cream


##### 2x resolution SalishSeaCast

* refreshed mine and Susan's memories on where we left off in early-July
  * Susan finished detailed review of row 13


##### SalishSeaNowcast

* `crop_gribs 12` waited until time out at 11:00 to process 1 file
* `make_plots wwatch3 forecast publish` failed at 13:44 with `RuntimeError: NetCDF: DAP failure`
  after new `tenacity` use did its job
  * re-ran manually at ~15:45



#### Wed 13-Aug-2025

##### Vacation

* rode the Great Northern trail above Nelson
  * started from the trailhead above Selkirk College
  * rode down to Troop Beach and back, then up to Mountain Station and back
  * lunch at L&C French café
  * grocery shopping at the Co-op


##### SalishSeaCast

* LiveOcean was delayed due to HPC problems
  * email from Parker
  * `download_live_ocean` timed out at 11:49
  * restarted it manually at 14:35, but it stopped at ~15:25
  * re-ran it manually at 19:45
  * stopped it at 20:50
  * persisted 12aug download via symlink
  * ran `make_live_ocean_files` to jump start automation at ~20:55


##### Security Updates

* Squash-merged dependabot PRs to update `pypdf` to 6.0.0 re: CVE-2025-55197 re: RAM exhaustion
  vulnerability
  * SalishSeaNowcast
* Squash-merged dependabot PRs to update `actions/checkout` to 5.0.0 re: update to use node 24
  * AtlantisCmd
  * salishsea-site



#### Thu 14-Aug-2025

##### Vacation

* rode Slocan Valley trail from Crescent Valley to Winlaw and back
  * snack at Sleep is for Sissies
  * late lunch at Frog Peak Café
  * drove up to Linden Lane Farm but didn't find anything we wanted in the shop
  * tried and failed to find Popov Leather
  * got cherries and a red pepper at fruit stand on the north shore


##### SalishSeaCast

* LiveOcean was delayed due to HPC problems
  * `download_live_ocean` timed out at 11:47
  * email from Parker at ~17:00 to say that today's run is finished
  * re-ran `download_live_ocean` at ~17:07 to jump start automation
* `make_plots wwatch3 forecast publish` failed at 19:44 with `RuntimeError: NetCDF: DAP failure`
  after new `tenacity` use did its job
  * re-ran manually at ~21:05



#### Fri 15-Aug-2025

##### Vacation

* rode Granite and Blewett Roads from Cottonwood Falls Park to the South Slocan dams complex
  * lots of climbing, especially a switch-backed, 5 km, cat 3 climb on the way back
  * a little rain on the ride, more on the drive back to Longbeach
  * coffee & carrot cake at Oso Negro Café after the ride


##### SalishSeaNowcast

* read some of the docs of the `pydap` project
  * that got me thinking about alternate engines that might solve the `make_plots wwatch3` issue
  * changed code to use `engine="h5netcdf"` because `pydap` isn't (yet?) a dependency
* `make_plots wwatch3 forecast publish` failed at 11:37 with `ImportError` from `fsspec` re: `aiohttp`
  after new `tenacity` use did its job
  * installed `aiohttp` and its dependencies in production env on `skookum`
  * re-ran manually at ~17:35
    * failed because `h5netcdf` can't handle an streaming ERDDAP dataset
  * installed `pydap` and its dependencies in production env on `skookum`
  * changed code to use `engine="pydap"`
  * works with `dap2://` protocol, but not with `pydap` preference of `dap4://`



#### Sat 16-Aug-2025

##### Vacation

* rain in the morning, but it cleared in the afternoon for a humid ride to Procter for cinnamon buns


##### Reshapr

* fixed broken and redirected docs links found be monthly scheduled `sphinx-linkcheck` action; PR#159


##### SalishSeaCast

* `make_plots wwatch3 forecast publish` with `pydap` and no `tenacity` failed at 11:11 with `ValueError`
  * first manual re-run at 11:33 failed
  * 2nd manual re-run in debug mode at ~11:38 worked
  * restored `tenacity` for tomorrow's attempts



#### Sun 17-Aug-2025

##### Vacation

* drove home from Longbeach
* stops:
  * fuel in Nelson
  * coffee, cinnamon buns & butter tarts to go at Copper Eagle in Greenwood
  * fruit and veggies at Mom & Pop's in Keremeos
  * fuel and coffee in Hope
  * many slowdowns between east of Chilliwack and west of Langley



### Week 34

#### Mon 18-Aug-2025

##### Security Updates

* Squash-merged dependabot PRs to update `actions/checkout` to 5.0.0 re: update to use node 24
  * SalishSeaNowcast
  * rwhite/numeric_2024
  * erddap-datasets


##### SalishSeaCast

* checked erddap log while `make_plots wwatch3 forecast` was re-trying
  * failures are due to
    `/results/SalishSea/rolling-forecasts/wwatch3/18aug25/SoG_ww3_fields_20250818_20250819.nc`
    `(No such file or directory)`
  * it appears that the wwatch3 dataset update is being blocked by the nowcast-green dataset updates
  * increased the `tenacity` retry time limit from 20 to 30 minutes


##### Miscellaneous

* updated PyCharm on `khawla` to 2025.2.0.1
* requested access on CCDB to `fir`, `narval`, and `trillium`


##### Minecraft

* checked mods, etc. for releases compatible with 1.21.8:
  * sodium: yes
  * lithium: yes
  * malilib: yes
  * minihud: yes
  * tweakeroo: yes
  * iris: yes
  * fresh animations: yes


##### SalishSeaCmd

* dropped support for `graham`; PR#99
  * tried to use PyCharm AI assistant
    * it did okay on the `run` module, but not on `test_run`
* sent support request to ARC to restore `UBC_CLUSTER` envvar to identify `sockeye`
* confirmed that `nibi` is identified by `CC_CLUSTER` envvar



#### Tue 19-Aug-2025

Worked at ESB.

##### Miscellaneous

* MOAD group mtg; see whiteboard
* reviewed `uv` issue re: `conda` support; still not there
* updated `kudu` Pycharm to 2025.2.0.1


##### SalishSeaCast

* `make_plots wwatch3 forecast2` and `forecast` both succeeded
  * `make_plots wwatch3 forecast` succeeded after retrying for 24 minutes
  * increased `tenacity` retry time limit from 30 to 40 minutes
  * changed back to `engine="netcdf4"` because `pydap` is noisier with no advantage


##### SalishSeaCmd

* dropped support for `beluga`; PR#99
* dropped support for `cedar`; PR#99
* squash-merged PR#99
* released v25.2



#### Wed 20-Aug-2025

##### SalishSeaCast

* `make_plots wwatch3 forecast2` was successful with some `tenacity` retries


##### SalishSeaCmd

* started work on adding support for `fir` cluster; PR#100
* got email from Alyza at ARC
  * `UBC_CLUSTER` envvar on `sockeye` is only set after `module load gcc` has bee executed


##### fir

* prepared for scaling test runs:
  * cleaned up `$HOME/`, `$SCRATCH/`, and `$PROJECT/$USER/`
  * cloned repos into `$PROJECT/$USER/`:
    * `grid`
    * `NEMO-3.6-code`
    * `NEMO-Cmd`
    * `rivers-climatology`
    * `SalishSeaCmd`
    * `SS-run-sets`
    * `tides`
    * `tracers`
    * `XIOS-2`

    * `XIOS-ARCH`
  * created `XIOS-ARCH/ALLIANCE/arch-GCC_FIR.[env|fcm|path]` files for StdEnv/2023
    * symlinked them in `XIOS-2/arch/`
  * built XIOS-2: `./make_xios --arch GCC_FIR --full --job 8`
    * success in 97 seconds
  * loaded `StdEnv/2023` environment with modules required to build NEMO:
    <!-- markdownlint-disable MD013 -->
    ```bash
    module --force purge
    module load StdEnv/2023
    module load netcdf-fortran-mpi/4.6.1
    module load perl/5.36.1
    ```
    <!-- markdownlint-enable MD013 -->
  * created `NEMOGCM/ARCH/arch-GCC_FIR.fcm` files for StdEnv/2023
  * built SalishSeaCast:
    * `XIOS_HOME=$PROJECT/$USER/MEOPAR/XIOS-2/ ./makenemo -n SalishSeaCast -m GCC_FIR -j 8`
    * success in 68 seconds
  * built REBUILD_NEMO:
    * `XIOS_HOME=$PROJECT/$USER/MEOPAR/XIOS-2/ ./maketools -n REBUILD_NEMO -m GCC_NIBI -j1`
* install `miniforge3`
  <!-- markdownlint-disable MD013 -->
  ```bash
  curl -L -O \
    "https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-$(uname)-$(uname -m).sh"
  bash Miniforge3-$(uname)-$(uname -m).sh
  ```
  <!-- markdownlint-enable MD013 -->
  * allow it to auto-initialize conda
  * re-log
* configure conda/mamba:
  <!-- markdownlint-disable MD013 -->
  ```bash
  conda config --set auto_activate_base false
  conda config --add envs_dirs /project/def-allen/dlatorne/conda-envs/
  ```
  <!-- markdownlint-enable MD013 -->
  * re-log
* install SalishSeaCmd
  <!-- markdownlint-disable MD013 -->
  ```bash
  cd project/dlatorne/MEOPAR/NEMO-Cmd/
  git pull
  cd project/dlatorne/MEOPAR/SalishSeaCmd/
  git pull
  mamba env create -f envs/environment-hpc.yaml
  mamba activate salishsea-cmd
  python -m pip install --user -e ../NEMO-Cmd
  python -m pip install --user -e .
  ```
  <!-- markdownlint-enable MD013 -->


##### Miscellaneous

* added the new `salishsea@eoas.ubc.ca` generic group email account to my Outlook config



#### Thu 21-Aug-2025

##### Miscellaneous

* GitHub Q3 Roadmap:
  * Mario Rodriguez
  * multi-agent orchestration
  * agent != model
  * issues & projects -> planning
  * try Spaces:
    * in preview
    * pat-to-use
  * Copilot code review
  * `*-instructions.md` files
  * Playwright: product???
  * Actions:
    * agentic autofix
  * Governance:
    * lots of enterprise words
    * top-down: enterprise -> orgs -> repos


##### NEMO-3.6-code

* closed PR#7 re: `StnEnv/2023` on `graham`


##### XIOS-ARCH

* updated README to replace `graham` example with `nibi`
* closed PR#2 re: `StnEnv/2023` on `graham`


##### erddap-datasets

* tested restoring `<updateEveryNMillis>10000</updateEveryNMillis>` element to `ubcSSf2DWaveFields30mV17-02`
  dataset on the thought that its removal from all datasets is the root cause of the latency issue
  for `make_plots wwatch3`
  * `updateEveryNMillis` causes a user request to trigger a dataset update in the request thread
    which probably avoids the delay in updating the dataset caused by processing of the flag file
    updates in the main thread being swamped by `nowcast-green` updates that typically start just
    before `wwatch3-forecast*` updates start; the former take >=30 minutes


##### SalishSeaTools

* finished `matchData()` refactoring and adding tests;
  * squash-merged PR#155
* started adding Karyn's `_salinityMatch()` function to `matchData()`; PR#
  * started work on `tests/salinityMatch_test.py` based on Karyn's notebook so that I have a
    functional test as I integrate and refactor the `salinityMatch()` code



#### Fri 22-Aug-2025

##### SalishSeaCast

* `make_plots wwatch3 forecast*` was successful without `tenacity` retries


##### fir

* uploaded 28feb23 restart files
* uploaded feb-apr 2023 forcing files to `fir`:
  <!-- markdownlint-disable MD013 -->
  ```bash
  yyyy=2023; rsync -tLv /results/forcing/atmospheric/GEM2.5/operational/ops_y${yyyy}m0[2-4]*.nc \
    fir:projects/def-allen/SalishSea/forcing/atmospheric/GEM2.5/operational/
  yyyy=2023; rsync -tLv /results/forcing/atmospheric/continental2.5/nemo_forcing/hrdps_y${yyyy}m0[2-4]*.nc \
    fir:projects/def-allen/SalishSea/forcing/atmospheric/continental2.5/nemo_forcing/
  yyyy=2023; rsync -tLv /results/forcing/sshNeahBay/obs/ssh_y${yyyy}m0[2-4]*.nc \
    fir:projects/def-allen/SalishSea/forcing/sshNeahBay/obs/
  yyyy=2023; rsync -tLv /results/forcing/rivers/R202108Dailies_y${yyyy}m0[2-4]*.nc \
    fir:projects/def-allen/SalishSea/forcing/rivers/
  yyyy=2023; rsync -tLv /results/forcing/rivers/river_turb/riverTurbDaily2_y${yyyy}m0[2-4]*.nc \
    fir:projects/def-allen/SalishSea/forcing/rivers/river_turb/
  yyyy=2023; rsync -tLv /results/forcing/LiveOcean/boundary_conditions/LiveOcean_v201905_y${yyyy}m0[2-4]*.nc \
    fir:projects/def-allen/SalishSea/forcing/LiveOcean/
  ```
  <!-- markdownlint-enable MD013 -->
* ran 11x32 with `--ntasks-per-node=192`
  * 10m38s, ~10% faster than `nibi`, consistent with 2.7 vs 2.4 GHz CPUs
* ran 11x32 with `--cpus-per-task=8 --ntasks-per-node=24`
  * failed due to over-subscription
* ran 14x25 with `--ntasks-per-node=192`
  * 10m59s
* ran 21x38 with `--ntasks-per-node=192`
  * 9m24s
* no job start/end emails


##### Miscellaneous

* dean team party at Mark's house



#### Sat 23-Aug-2025

##### Miscellaneous

* went to White Rock to visit JRA and family



#### Sun 24-Aug-2025

##### Miscellaneous

* JRA passed away early in the morning
* went to White Rock to help with emptying JRA's suite



### Week 35

#### Mon 25-Aug-2025

##### SalishSeaCast

* `make_plots wwatch3 forecast*` has been successful without `tenacity` retries since 22aug
  * removed `tenacity` decorator to see if `updateEveryNMillis` tag on ERDDAP dataset fully resolves
    the latency issue


##### Miscellaneous

* went to White Rock to help with emptying JRA's suite



#### Tue 26-Aug-2025

##### SalishSeaCast

* `make_plots wwatch3 forecast*` was successful without `tenacity` decorator
* Fraser river turbidity was persisted from 25aug


##### Miscellaneous

* cargo van to White Rock to help with emptying JRA's suite



#### Wed 27-Aug-2025

##### SalishSeaCast

* `make_plots wwatch3 forecast*` was successful without `tenacity` decorator
* Fraser river turbidity was persisted from 26aug


##### Security Updates

* Squash-merged dependabot PRs to update codecov-action to 5.5.0 re: dependency & docs updates,
  and bug fixes
  * SalishSeaNowcast
  * gha-workflows
  * AtlantisCmd
* Squash-merged dependabot PRs to update h2 to 4.3.0 re: CVE-2025-57804 re: HTTP/2 request splitting
  vulnerability
  * SalishSeaNowcast
  * AtlantisCmd
  * Reshapr



#### Thu 28-Aug-2025

##### SalishSeaCast

* `make_plots wwatch3 forecast2` failed, but it appears to be due to bad wave height values in the run
* Fraser river buoy site froze from 23:10 on 27aug to 03:10 on 28aug
* `make_plots wwatch3 forecast` was successful without `tenacity` decorator


##### Reshapr

* updated to Python 3.13; PR#161
* released v25.1


##### Minecraft

* stopped server
* did lizzy-smelt backup
* updated OS packages and auto-removed outdated packages
* rebooted
* set up 1.21.8 server
  <!-- markdownlint-disable MD013 -->
  ```bash
  mkdir ~/Games/MinecraftFabric1.21.8Server
  cd ~/Games/MinecraftFabric1.21.8Server
  curl -OJ https://meta.fabricmc.net/v2/versions/loader/1.21.8/0.17.2/1.1.0/server/jar
  pushd ~/Games/MinecraftFabric1.21.5Server
  cp banned-* eula.txt ops.json whitelist.json start.sh ../MinecraftFabric1.21.8Server/
  popd
  ```
  <!-- markdownlint-enable MD013 -->
  * edited `start.sh` to:
  <!-- markdownlint-disable MD013 -->
    ```bash
    #!/usr/bin/env bash
    java -Xmx2G -jar fabric-server-mc.1.21.8-loader.0.17.2-launcher.1.1.0.jar nogui
    ```
  <!-- markdownlint-enable MD013 -->
* launched and stopped server to create instance directories and files
  <!-- markdownlint-disable MD013 -->
  ```bash
  ./start.sh
    ...
  /stop
  ```
  <!-- markdownlint-enable MD013 -->
* edited `server.properties` to sync with 1.21.5 settings
* installed mods, and rsync-ed `1-20-1-25jul23` world tree:
<!-- markdownlint-disable MD013 -->
```bash
cd ~/Games/MinecraftFabric1.21.8Server/mods/
curl -LO https://github.com/CaffeineMC/lithium/releases/download/mc1.21.8-0.18.0/lithium-fabric-0.18.0+mc1.21.8.jar
cd ~/Games/MinecraftFabric1.21.8Server
rsync -av ../MinecraftFabric1.21.5Server/1-20-1-25jul23 ./
```
<!-- markdownlint-enable MD013 -->
* downloaded and unzipped on `khawla` VanillaTweaks double shulker shells v1.3.13 datapack
  * rsync-ed it to `Games/MinecraftFabric1.21.8Server/1-20-1-25jul23/datapacks/` and removed v1.13.11
* launched server in `tmux`
<!-- markdownlint-disable MD013 -->
```bash
tmux new -n minecraft-server
./start.sh
```
<!-- markdownlint-enable MD013 -->
* set up 1.21.8 client instance in MultiMC
  * created instance
  * installed fabric 0.17.2
  * downloaded and installed loader mods:
    * sodium-fabric-0.6.13+mc1.21.6.jar
    * lithium-fabric-0.18.0+mc1.21.8.jar
    * malilib-fabric-1.21.8-0.25.5-sakura.4.jar
    * minihud-fabric-1.21.8-0.36.4-sakura.1.jar
    * tweakeroo-fabric-1.21.8-0.25.4-sakura.4.jar
    * FreshAnimations_v1.10.zip
    * entity_model_features_1.21.6-fabric-3.0.1.jar
    * entity_texture_features_1.21.6-fabric-7.0.1.jar
    * iris-fabric-1.9.1+mc1.21.7.jar
  * selected Java: `/usr/lib/jvm/java-21-openjdk-amd64/bin/java`
  * started and stopped client instance to populate `config/`
  * copied `minihud.json` and `tweakeroo.json` from 1.21.5 instance `config/`
  * downloaded and installed Vanilla Tweaks resource packs `VanillaTweaks_r503680_MC1.21.x.zip`:
    * iron bars fix
    * lower shield
    * redstone devices:
      * StickyPistonSides
      * DirectionalHoppers
      * DirectionalDispensersDroppers
      * DirectionalObservers
      * GroovyLevers
      * RedstoneWireFix
  * added server: `SADA on lizzy` at 10.0.0.81
* started game and adjusted UI:
  * FOV: 80
  * Video:
    * Brightness: Bright
    * GUI Scale: 2x
    * Weather: Fancy
    * Leaves: Fancy
  * enabled resource packs
  * Music & Sound:
    * Music: 50%
    * Show Subtitles: on
    * Directional Audio: on
  * Optional Telemetry Data
  * F3-h to enable advanced tooltips
  * used `/gamerule` to confirm increased spawn chunks radius from 3 to 4 to keep iron farm loaded



#### Fri 29-Aug-2025

##### Miscellaneous

* set up Brother DCP-L2550DW printer in eyre
* updated `khawla` PyCharm to 2025.2.1


##### SalishSeaCmd

* squash-merged PR#100 to add support for `fir`



#### Sat 30-Aug-2025

##### SalishSeaCast

* `make_plots wwatch3 forecast2` failed with:
    `OSError: [Errno -70] NetCDF: DAP server error: 'https://salishsea.eos.ubc.ca/erddap/griddap/ubcSSf2DWaveFields30mV17-02'`
  * re-ran it manually with success
* `make_plots wwatch3 forecast` succeeded



#### Sun 31-Aug-2025

Rode to Sanctuary and back with Susan



## September

### Week 36

#### Mon 1-Sep-2025

**Statutory Holiday** - Labour Day

##### SalishSeaCast

* `crop_gribs 12` waited until time out at 10:46 to process 1 file
* `archive_tarball` failed yesterday
  * `/nearline/` on `graham` is not responding
  * `/nearline/` on `nibi` does not exist yet


##### FUN

* started adding handling for TFSAs



#### Tue 2-Sep-2025

Worked at ESB

##### SalishSeaCast

* `make_ssh_files forecast2` failed
* `collect_NeahBay_ssh 06` failed at 08:45 due to no `etss.20250902/t06z_csv/9443090.csv`
  in tarball
  * re-ran at 11:27 and it failed again
  * punted to Susan in #ssc-daily-progress for a plan to get automation restarted
  * together we discovered that the tarball csv file template changed from:
     `etss.{yyyymmdd}/t{forecast}z_csv/9443090.csv`
    to:
     `etss.{yyyymmdd}/t{forecast}z.csv/9443090.csv`
  * changed `nowcast.yaml` and re-ran successfully at 12:51


##### Security Updates

* Squash-merged dependabot PRs to update h2 to 4.3.0 re: CVE-2025-57804 re: HTTP/2 request splitting
  vulnerability
  * erddap-datasets
  * SOG-Bloomcast-Ensemble
  * NEMO-Cmd
  * SalishSeaCmd
  * salishsea-site
  * moad_tools


##### SalishSeaNowcast

* Changed the Neah Bay ssh CSV file template in nowcast.yaml and associated
  test files to match the surprise change by NOAA
  * PR#381; squash-merged and deployed


##### SalishSeaCmd

* explored how to refactor run plug-in to use `UBC_CLUSTER` envvar that is only
  loaded after `gcc` module has been loaded
* did some work on replacing `@patch` mocks with `monkeypatch` fixtures; PR#102


##### Miscellaneous

* updated PyCharm on `kudu` to 2025.2.1
  * test runner stopped working 😱



#### Wed 3-Sep-2025

##### Miscellaneous

* updated PyCharm on `khawla` to 2025.2.1.1
  * test runner issue fixed 😌


##### SalishSeaNowcast

* reverted uncommitted `tenacity` changes in `wave_height_period` figure module because the ERDDAP
  latency issue seems to have been resolved by restoring the
  `<updateEveryNMillis>10000</updateEveryNMillis>` element to `ubcSSf2DWaveFields30mV17-02` dataset


##### 2x resolution SalishSeaCast

* refreshed my memory on where we left off in early-August
  * Susan added code to 2xrez processing notebook to smooth the Juan de Fuca mouth
  * Susan finished detailed review of row 13
  * Susan finished detailed review of row 14
* continued work on 2xrez processing notebook:
  * adjusted row 13 grid cells 6 and 7
    * reviewed changes with Susan
* continued work on 2xrez verification notebook
  * discussed row 13 cell 9 with Susan



#### Thu 4-Sep-2025

##### SalishSeaCast

* `crop_gribs 12` missed 1 file; delayed runs by ~2h


##### 2x resolution SalishSeaCast

* continued work on 2xrez processing notebook:
  * adjusted row 13 grid cells 9 to 11

    * reviewed changes with Susan
      * **do we want to open the river south of the east end of Swishwash Island in the 202405 bathy?**
      * "connect tip of Alaska" ??? 13, 11
* continued work on 2xrez verification notebook

  * adjusted row 14 grid cells
    * reviewed changes with Susan
  * added row 15 -



#### Fri 5-Sep-2025

Worked at ESB

##### Miscellaneous

* MOAD group mtg; see whiteboard
  * Junqi joined the group as an M.Sc. student
* cleaned up `/var/cache/apt/` re: nearly full `root` partition on `kudu`
  * started with 14.2 GB in 3698 items
  * ran `sudo apt-get autoclean`
  * resulted in 8.2 GB in 3302 items
* updated PyCharm on `kudu` to 2025.2.1.1
  * test runner issue fixed 😌
* discussed Vicente's move to running OceanParcels on `nibi` with Susan


##### SalishSeaCmd

* squash-merged PR#102 re: replacing some `@patch` mocks with `monkeypatch` fixtures
* change to default to `rrg-allen` account on `nibi`; PR#103; squash-merged
* change `sockeye` to deal with `UBC_CLUSTER` envvar only set after `module load gcc`
  * PR#104; squash-merged
  * successfully tested on `sockeye`
    * error message generation
    * run with gcc module loaded
* did more tests modernization; PR#105; squash-merged



#### Sat 6-Sep-2025

##### SalishSeaCast

* USGS rivers obs were unavailable
  * `make_runoff_file` used patching strategy

Set up new desk in my office at home.



##### 2x resolution SalishSeaCast

* continued work on 2xrez processing notebook:
  * finished adjusting row 13 grid cell 11
    * Susan says land at west end of Annacis Island is part of the island, not the low islets
  * started adjusting row 14 cell 7

* continued work on 2xrez verification notebook

  * adjusted row 14 grid cells
    * reviewed changes with Susan
  * added row 15 -



#### Sun 7-Sep-2025

##### SalishSeaCast

* USGS rivers obs were unavailable
  * `make_runoff_file` used patching strategy


##### FUN

* continued adding handling for TFSAs



### Week 37

#### Mon 8-Sep-2025

##### SalishSeaCast

* `make_plots wwatch3 forecast2` produced a spiky plot with negative wave heights for Halibut Bank
  and failed with `RuntimeError: NetCDF: DAP failure` for Sentry Shoal
  * saw this a week or so ago
  * successful on manual re-run at ~11:00
* USGS rivers obs improved somewhat:
  * NisquallyMcKenna time series was empty; `make_runoff_file` used patching strategy
  * other rivers were successful


##### Miscellaneous

* NEMO seminar:
  * Bill Merryfield, CCCma
    * "Applications of ECCC's NEMO-based global climate models to seasonal and decadal predictions"
    * between weather prediction models and climate models
    * seasonal is 1-12 months, decadal is 1-10 years
    * CanSIPS: Canadian Seasonal to Interannual Prediction System
      * combines CanESM5 climate model and GEM5.2-NEMO weather prediction model
    * Luiz da Silva, University of Manitoba to speak
      * "ANHALYZE: Handling and Visualizing NEMO outputs"
      * Python package for analysis of ANHA configs of NEMO
      * side-project
      * data analysis, analyses, visualizations
      * `xarray` wrapper
      * github.com/PORTAL-CEOS
      * not much there there...
* uploaded `nowcast-green.202111` u, v, w & T grid results files to
  `nibi:/project/def-allen/SalishSea/nowcast-green.202111/` for Vicente with
  `rsync -rtlv --relative *07/SalishSea_1h_*_grid_*.nc nibi:/project/def-allen/SalishSea/nowcast-green.202111/`
  in `tmux` session `djl-nibi-xfer`
  * 2 days took 12m20s
  * group-write is not propagated, despite setgid permission bit being set


##### Security Updates

* Squash-merged dependabot PRs to update setup-micromamba to 2.0.6 re: dependency updates
  * SalishSeaNowcast
  * erddap-datasets
  * rwhite/numeric_2024
  * moad_tools
  * gha-workflows
  * AtlantisCmd
  * salishsea-site
* Squash-merged dependabot PRs to update codecov-action to 5.5.1 re: dependency updates
  * SalishSeaNowcast
  * gha-workflows
  * AtlantisCmd
* Squash-merged dependabot PR to update github-script to 8 re: dependency updates
  * gha-workflows
* Squash-merged pre-commit PR to update blacken-docs to 1.20.0 re: adding Python 3.14 support
  * MoaceanParcels



#### Tue 9-Sep-2025

##### SalishSeaCast

* USGS rivers obs successful for all rivers












* upload nowcast-green u, v, w, T files for 2007 to `nibi` for Vicente
  * `/scratch/` or `/project/`:
    * size of a year: 678G
    * figure out quota implications
  * think about `salloc` vs. web interface for interactive


* Susan: do we want to set up Globus on `salish` or `skookum`, or engage compstaff
  to set it up for `ocean` or wider EOAS context
  * I should get to know Stephan and discuss bigger context with him


##### SalishSeaCmd

* can we run on `trillium`?
  * 400 Gb/s NDR InfiniBand
  * VAST file system
  * cpus: AMD EPYC 9655 (Zen 5) @ 2.6 GHz, 384MB cache L3
  * no mention of special tasks directives for whole nodes
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


##### ERDDAP

* update to v2.28.1
  * review v2.27.0 changes because they will be included as we jump from v2.26.0


##### SalishSeaCast

* backfill forcing uploads and AGRIF runs on `orcinus` from ~14jul


##### salishsea-site

* SMELT link in nav bar has no target


##### SalishSeaNowcast

* change config to upload forcing to `nibi` instead of `graham`
  * need automation key activated on `nibi`
* change config to drop forcing uploads to `optimum`
* change automation workflow to run nowcast-green in place of nowcast-blue
  * add output of 10min avg tide gauge station files






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
  <!-- markdownlint-disable MD013 -->
  ```python
  import tomllib
  from pathlib import Path

  ...

  with Path("../pyproject.toml").open("rb") as f:
      pkg_info = tomllib.load(f)
  project = pkg_info["project"]["name"]
  ```
  <!-- markdownlint-enable MD013 -->
  <!-- markdownlint-disable MD013 -->
  ```text
  Chg to project name retrieval from pyproject.toml

  Replaced the hardcoded project name with dynamic retrieval from
  `pyproject.toml` using `tomllib`. This ensures consistency and
  reduces manual updates for project metadata.
  ```
  <!-- markdownlint-enable MD013 -->
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



* Python 3.13:
  * successful workflow test with 3.13:
    * MOAD/docs - migrated on 14oct24
    * NEMO-Cmd - migrated on 27oct24 in PR#92
    * SalishSeaCmd - migrated on 27oct24 in PR#77
    * SalishSeaCast/docs - migrated on 11nov24 in PR#57
    * NEMO_Nowcast - migrated on 27nov24 in PR#62
    * moad_tools - migrated on 15dec24 in PR#80
    * tools/SalishSeaTools - migrated on 9jan25 in PR#124
    * SalishSeaNowcast - migrated on 12jan25 in PR#302
    * gha-workflows - migrated on 13jan25 in PR#51
    * AtlantisCmd - migrated on 2feb25 in PR#61
    * SOG-Bloomcast-Ensemble - migrated on 15feb25 in PR#66
    * erddap-datasets - migrated on 10jul25 in PR#52
    * salishsea-site - migrated on 11jul25 in PR#119
    * Reshapr - migrated on 28aug25 in PR#161
  * no workflows:
    * SOG
    * ECget
    * analysis-doug
    * SOG-Bloomcast ??



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

* change download_weather to gather only files missed by collect_weather so that it can
  work with crop_gribs monitoring incoming files
  * check for presence of files before downloading them; skip if present



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
