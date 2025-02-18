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

#### Sat 1-Feb-2025

##### Miscellaneous

* updated `kahla` PyCharm to 2024.3.2


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
    * alternative link to Klinck's work (mulitple occurrences)
      * http://woodshole.er.usgs.gov/operations/sea-mat/klinck-html/dynmodes.html goes to WHOI index page
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
    * things seemed to go well until the section to add the Steeveston Jetty where I discovered
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
* TODO:
  * Add new unrecognized weather description `Moderate Rain,Snow` to cloud fraction mapping
  * silence `matplotlib.font_manager` log messages


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


##### NEMO_Nowcast

* added auto-milestone workflow; 5b2693f3
* changed to project name retrieval from `pyproject.toml`; PR#68


##### 2x resolution SalishSeaCast

* worked with Susan to understand differences in north boundary channel straightening section
  *
* started 2xrez verification notebook


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




SalishSeaCast TODO:

* drop VENUS nodes ADCP comparison figures because the obs collection code has never been ported
  from Matlab; nobody cares enough
  * `make_plots nemo nowcast comparison`
    * `research_VENUS.plotdepavADCP` - keep?
      * 3 nodes
    * `research_VENUS.plottimeavADCP` - keep?
      * 3 nodes
    * `research_VENUS.plotADCP` - keep?
      * 3 nodes
* resolve Squamish and Halfmoon Bay water level comparison figure failures by setting CHS station
  ids to `None` like we do for Boundary Bay; that should produce model-only figures - done 17feb25
  in `tools` PR#137
  * add an issue to perhaps add Darrell Bay (07808, opposite Woodfibre) as a future location for
    NEMO water level output and a comparison figure
    * Latitude: 49.669, Longitude: -123.169



* tools repo TODO:
  * update library_code section in docs or move it to MOAD docs


* create mesh mask for sss150


* add --backfill option download_weather to allow over-write of existing destination dir
  * issue #309


* add pre-commit:
  * SOG-Bloomcast-Ensemble


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
