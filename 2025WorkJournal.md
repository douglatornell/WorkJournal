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

##### Miscellaneous

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

##### Miscellaneous

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

##### Miscellaneous

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
  the stored files has incorrect coordinate names; a transition to Reshapr pos-processing issue


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





* TODO in all readthedocs projects:
  * add `sphinx` stanza to `.readthedocs.yaml` re: config API change
      branch: rtd-sphinx-config
<!-- markdownlint-disable MD013 -->
```yaml
sphinx:
    builder: html
    configuration: docs/conf.py
    fail_on_warning: false
```
```text
Add explicit Sphinx configuration for readthedocs

Updated `.readthedocs.yaml` to define Sphinx builder settings,
including the builder type, configuration file path,
and `fail_on_warning` option. This is necessary due to
readthedocs deprecating projects without explicit builder
configuration that comes into effect on 20-Jan-2025.
```
<!-- markdownlint-enable MD013 -->
  * tools - done on 14Jan25 in PR#128
  * SalishSeaNowcast - done on 15jan25 in PR#324
  * moad_tools - done on 17jan25 in PR#84
  * MOAD/docs - done on 17jan25 in PR#47
  * SalishSeaCast/docs - done on 17jan25 in PR#60

  * salishsea-site
  * NEMO-Cmd
  * NEMO_Nowcast
  * Reshapr
  * SalishSeaCmd
  * AtlantisCmd
  * ECget




* tools repo TODO:
  * update library_code section in docs or move it to MOAD docs


* create mesh mask for sss150


* add --backfill option download_weather to allow over-write of existing destination dir
  * issue #309


* add pre-commit:
  * SOG-Bloomcast-Ensemble



* pip=24.2 has started to complain about -e installs for packages w/o `pyproject.toml`
  * NEMO_Nowcast - fixed 27nov24 in PR#61
  * FVCOM-Cmd - archived; plan to drop from SalishSeaNowcast
  * OPPTools - fork on GitLab; plan to drop from SalishSeaNowcast
  * SalishSeaTools


Refresh myself on Fortran in VS Code and on-the-fly compilation; prep to present to group.

* fortran.fortls.directories



TODO:

* update `.readthedocs.yaml` to use ubuntu-24.04 and mambaforge-23.11 in many repos
* also update sphinx & deps version pins
    <!-- markdownlint-disable MD013 -->
    ```yaml
    - sphinx=8.1.3
    - sphinx-notfound-page=1.0.4
    - sphinx-rtd-theme=3.0.0
    ```
    <!-- markdownlint-enable MD013 -->
* use `nbsphinx=0.9.5` if required
  * NEMO_Nowcast - done 22sep24 in PR#57; sphinx & deps version pins done 26oct24 in PR#58
  * MOAD/docs - done 14oct24; sphinx & deps version pins done 26oct24
  * NEMO-Cmd - done 18oct24 in PR#92
  * SalishSeaCmd - done 25oct24 in PR#76
  * SalishSeaNowcast - done 30oct24 in PR#301
  * moad_tools - done 31oct24 in PR#73
  * salishsea-site - done 2nov24 in PR#62
  * Reshapr - done 3nov24 in PR#141
  * SalishSeaCast/docs - done 11nov24 in PR#56
  * tools - done 14nov24 in PR#106
  * AtlantisCmd - done 18nov24 in PR#48
  * MoaceanParcels - done 19nov24 in PR#52 - consider archiving repo due to bit-rot
  * rpn-to-gemlam - done 20nov24 in PR#21 - archived project

  * ECget - needs some love first


* TODO:
  * Change `source_suffix = '.rst'` to `source_suffix = {'.rst': 'restructuredtext'}` in `conf.py`
    or omit `source_suffix` config because `.rst` is the default (works in Reshapr docs)
  * Investigate `no theme named 'sphinx_rtd_theme' found (missing theme.toml?)



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
  * not yet tested
    * AtlantisCmd
      * Update AtlantisCmd to drop Python 3.10 because NEMO-Cmd has dropped it;
        GHA workflow is failing
    * salishsea-site
    * Reshapr
    * erddap-datasets
  * no workflows:
    * gha-workflows
    * SOG-Bloomcast-Ensemble
    * SOG-Bloomcast ??
    * analysis-doug
    * ECget


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

  * SOG-Bloomcast-Ensemble
  * SOG-Bloomcast
  * cookiecutter-MOAD-pypkg
  * ECget
  * SOG


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
    * tools - issue created
    * SOG-Bloomcast-Ensemble - issue created
    * SOG-Bloomcast


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
