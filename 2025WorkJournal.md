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


##### erddap-Datasets

* marked V19-05 u, v & w fields datasets as inactive in preparation for their removal
* restarted ERDDAP server



##### 202405 Bathymetry

* continued work on `tools/bathymetry/Process20405Bathymetry.ipynb`
  * finished refactoring west open boundary channel straightening to use `xarray` and new grid shape




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
  * successfully env creation with separated pkgs branch of `moad_tools`:
    * SalishSeaNowcast
  * not yet tested
    * AtlantisCmd
      * Update AtlantisCmd to drop Python 3.10 because NEMO-Cmd has dropped it;
        GHA workflow is failing
    * salishsea-site
    * Reshapr
    * erddap-datasets
  * no workflows:
    * gha-workflows
    * tools/SalishSeaTools
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

  * SalishSeaTools
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
