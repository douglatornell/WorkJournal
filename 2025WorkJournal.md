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
      * glacierized mountain: Homathko, Wannock, Klinaklini
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




* tools repo TODO:
  * update library_code section in docs or move it to MOAD docs


* create mesh mask for sss150


* add --backfill option download_weather to allow over-write of existing destination dir
  * issue #309


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
  * not yet tested
    * salishsea-site
    * Reshapr
    * erddap-datasets
  * no workflows:
    * SOG
    * ECget
    * analysis-doug
    * SOG-Bloomcast ??


TODO:

* change automation workflow to run nowcast-green in place of nowcast-blue
  * add output of 10min avg tide gauge station files
* remove VHFR FVCOM from automation workflow
  * remove FVCOM boundary slab files output from nowcast-green/file_def.xml
  * drop FVCOM-Cmd and OPPTools dependencies
* `sandheads_winds` is using HTTP instead of HTTPS for obs collection via
  `salishsea_tools.stormtools.get_EC_observations()`; same in `tools.I_ForcingFiles.Atmos.weather.get_EC_observations()`



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

* fix straight line gaps in wwatch3 forecast plots (forecast2 are okay)



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
