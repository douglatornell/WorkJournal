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
* changed row labels 5.9 to 9-13


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

* replied to email from Peter @ SFU re: `mutiprocessing` for ERDDAP access:
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
  * North Atlantic Winds, Arctic Freshawater & the AMOC
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
  * finihsed restructuring `nowcast.yaml` config to put all bathymetry-specific values
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
* `oricnus` OS and software infrastructure is going to be upgraded over the summer!


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
  when `make_funoff_file` is run in preparation for forecast2 runs


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
  euphausiid model



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
* TODO:
  * drop `<drawLandMask>over</drawLandMask>` from datasets because it is now set as the server default
  * change `colorBarPalette` attr tag values to our favourite cmocean colour maps
  * 2.10: test `accessibleViaFiles` setting; if it does what I think, discuss with Susan if we want it
  * 2.11: add `emailDiagnosticsToErdData` setting
  * 2.12: add 3 `ipAddress*` tags to `prefix.xml` to limit malicious users and overly aggressive
    concurrent requests
  * 2.15: think about languages other than english
  * 2.16: full? utf-8 support; fix accented names in `datasets.xml`
  * 2.19:
    * increase `n*Threads` tag values to 3 in `prefix.xml`
    * hyphens in datasetIDs are deprecated ???
  * 2.23: CF-1.10 vs. CF-1.6
  * 2.25:
    * zarr support
    * Prometheus metrics
    * `Xinclude` in `datasets.xml`
    * `unusualActivityFailPercent` can be set to other than 25%
  * 2.26:
    * docs now on https://erddap.github.io/
    * dataset citations in UI



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





##### erddap-datasets

* TODO:
  * drop `<drawLandMask>over</drawLandMask>` from datasets because it is now set as the server default
  * change `colorBarPalette` attr tag values to our favourite cmocean colour maps
  * 2.10: test `accessibleViaFiles` setting; if it does what I think, discuss with Susan if we want it
  * 2.11: add `emailDiagnosticsToErdData` setting
  * 2.12: add 3 `ipAddress*` tags to `prefix.xml` to limit malicious users and overly aggressive
    concurrent requests
  * 2.15: think about languages other than english; only partially automated though
  * 2.16: full? utf-8 support; fix accented names in `datasets.xml`
  * 2.19:
    * increase `n*Threads` tag values to 3 in `prefix.xml`
    * hyphens in datasetIDs are deprecated ???
  * 2.23: CF-1.10 vs. CF-1.6
  * 2.25:
    * zarr support
    * Prometheus metrics
    * `Xinclude` in `datasets.xml`
    * `unusualActivityFailPercent` can be set to other than 25%
  * 2.26:
    * docs now on https://erddap.github.io/
    * dataset citations in UI



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
