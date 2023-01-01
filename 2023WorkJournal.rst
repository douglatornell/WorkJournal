*****************
2023 Work Journal
*****************

This is my public work journal.
This journal is about:

* my work as a Research Software Engineer with Dr. Susan Allen in the Department of Earth, Ocean and Atmospheric Sciences at the University of British Columbia
* my freelance work via my consulting business,
  43ravens
* my open-source activities
* occasional notes about life in general


January
=======

Week 0
------

Sun 1-Jan-2023
^^^^^^^^^^^^^^

collect_weather 18 didn't complete
* investigation:
  * 2 collect_weather workers running: 18 and 00
  * 515 of 576 files downloaded
  * no error messages in log
* recovery started at ~10:30
    kill collect_weather 18
    kill collect_weather 00
    mv /results/forcing/atmospheric/GEM2.5/GRIB/20221231/18/ aside
    download_weather 18 --yesterday
    download_weather 00
    download_weather 06
    download_weather 12 1km --yesterday
    download_weather 00 1km --yesterday **failed**
    wait for forecast2 runs to finish; delayed ~9.5h
    download_weather 12; delayed ~4.5h
    collect_weather 18
    rm -rf /results/forcing/atmospheric/GEM2.5/GRIB/20221231/18.aside
Cleaned up left-over hindcast workers.
(SalishSeaCast)

Murrayville to Vancouver




TODO:
* Revisit WWatch3-Cmd dependabot PRs re: actions versions & reusable workflows
* Update WWatch3-Cmd to Ptyhon>=3.10

* numpy.int in moad_tools random_oil_spills

* Revisit salishsea-site dependabot PRs re: actions versions & reusable workflows

* pre-commit auto-update





TODO:
* 43ravens/NEMO_Nowcast has something weird going on with Slack webhook secret in dependabot PRs


TODO:
* review and clean up permissions in GitHub orgs




Becuase I can never remember how to get a git feature branch that I set asdie back into working
state:
* ref: https://www.atlassian.com/git/tutorials/merging-vs-rebasing
* git switch feature
* git rebase main
* In PyCharm > Git > Log context menu "Rebase 'feature' onto 'main'"
* **BUT** if the changes in the feature branch overlap files in main, it's possible that
  a merge will be required


TODO:
* SalishSeaCast/docs:
  * replace broken links:
    * http://pages.physics.cornell.edu/~myers/teaching/ComputationalMethods/
    * http://pages.physics.cornell.edu/~myers/teaching/ComputationalMethods/LectureNotes/Intro_to_Python.pdf
    * https://www.pac.dfo-mpo.gc.ca/science/oceans/data-donnees/search-recherche/profiles-eng.asp
    * https://www.waterlevels.gc.ca/eng/data#s2
    * https://www.westgrid.ca/support/systems/orcinus


TODO:
* update GHA actions to Node.js 16 versions; warnings now, no set final date as of 12oct22:
  * actions/checkout@v2 -> actions/checkout@v3
  * conda-incubator/setup-miniconda - no node.js 16 version available yet
  * 8398a7/action-slack@v3 - did node.js 16 as micro version bump
  * codecov/codecov-action@v1 -> codecov/codecov-action@v3
* more deprecation warnings in SalishSeaNEMO re: `set-output` and `save-state`
  * coming from conda-incubator/setup-miniconda@v2
* confirm that we are using:
  * github/codeql-action/init@v2
  * github/codeql-action/analyze@v2 (probably using v1 in some repos)
  * EOL date for v1 is Dec-2022
* commit messages:
  * Bump GHA actions/checkout to v3

    re: Node.js 12 actions deprecation. See:
    https://github.blog/changelog/2022-09-22-github-actions-all-actions-will-begin-running-on-node16-instead-of-node12/

  * Bump GHA codecov/codecov-action to v3

    re: Node.js 12 actions deprecation. See:
    https://github.blog/changelog/2022-09-22-github-actions-all-actions-will-begin-running-on-node16-instead-of-node12/

  * Bump GHA github/codeql-action/analyze to v2

    re: CodeQL Action v1 deprecation. See:
    https://github.blog/changelog/2022-04-27-code-scanning-deprecation-of-codeql-action-v1/




TODO:
  EGBC firm registration next steps by 30-Sep
    * practice mgmt plan
  2022-2023 CE plan




I'm interested in having our windows cleaned, inside and outside. We live in a 3 unit triplex in Kitsilano, but the service I'm looking for is just for our unit.

We have 2 floors. On the ground floor there are 6 windows and a set of patio doors with a window above them. 3 of those windows, and the patio doors have screens. On the second floor there are 8 windows. 4 of them have screens. 1 of them is a window in a balcony door. There are also 2 skylights. One in a small roof section over the front door entry. The other is low in a sloping roof section over the 2nd floor. Inside, the window coverings are mostly mini-blinds except for the patio doors and an adjacent window which have vertical blinds.




TODO:
* citations data ideas discussed w/ Susan on 30-Jul drive to White Rock


TODO:
* write use case for Karyn's 5-yr average biololgy
* write use case for Becca's single point, 2 depths physics & chemistry
* write use case for month-average model products
* Becca's single point extraction triggers:
    /home/dlatorne/conda_envs/reshapr/lib/python3.10/site-packages/xarray/core/indexing.py:1228: PerformanceWarning: Slicing is producing a large chunk. To accept the large
    chunk and silence this warning, set the option
        >>> with dask.config.set(**{'array.slicing.split_large_chunks': False}):
        ...     array[indexer]

    To avoid creating the large chunks, set the option
        >>> with dask.config.set(**{'array.slicing.split_large_chunks': True}):
        ...     array[indexer]
      return self.array[key]
  then fails with:
    Traceback (most recent call last):
    File "/ocean/dlatorne/MOAD/Reshapr/reshapr/core/extract.py", line 655, in calc_extracted_vars
      std_name = var.attrs["standard_name"]
    KeyError: 'standard_name'

Reshapr ideas:
* extraction config examples in docs:
  * simple whole field extraction for a few variables
  * temporal and spatial selection
  * resampling
* extraction from month-avg datasets; issue #32
  * need to handle month-by-month dataset files 
    (e.g. SalishSeaCast_1m_ptrc_T_20220301_20220331.nc); 
    code presently assumes day-by-day
    (e.g. SalishSea_1d_20220314_20220314_ptrc_T.nc)



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



Add Tereza's pubs to ERDDAP.



TODO:
* change SalishSeaNowcast automation key to ED-25519



TODO:
  Bug re: log rotation during download_wwatch3_results forecast2

* update SalishSeaCmd installation docs re: no anaconda and `python3 -m pip install`



TODO:
* for MoaceanParcels
  * add GHA CodeQL workflow
  * add pre-commit hooks:
    * pyupgrade

OceanParcels:
* Explore VisibleDeprecationWarning re: constructing ndarrays from lists of ndarrays; parcels/field.py:241 & 243 and commits f8faf9 & ffb6223; do timestamps & datafiles need to be ndarrays, or can they be lists?


TODO:
* Move entry points from setup.py to setup.cfg
  * SalishSeaCmd - done
  * NEMO-Cmd - done
  * MOHID-Cmd - done
  * moad_tools - done
  * Make-MIDOSS-Forcing
  * WWatch3-Cmd
  * also replace setup.py with pyproject.toml ??
    * AtlantisCmd
    * FVCOM-Cmd
    * salishsea-site
    * moad-app-dev
    * rpn-to-gemlam
    * SOG-Bloomcast
    * SOG-Bloomcast-Ensemble
    * SOG-forcing
    * SOG
* add pre-commit hooks:
  * blacken-docs
  * pyupgrade


TODO:
* Python packaging docs and pkg cookiecutters updates:
  * add docs re: pre-commit



TODO:
Fix ariane docs:
* maybe re:  adding a bin-like directory to prefix gets rid of errors from doc/ and examples/ that confused Becca ???
 versions re: .bashrc



Update ONC URLs from dmas.uvic.ca to https://data.oceannetworks.ca/

jupyter kernelspec uninstall unwanted-kernel



TODO:

https://linuxize.com/post/getting-started-with-tmux/

update deployment docs re: spinning up a new compute node

15jun20: check mitigation of "index exceeds dimension bounds" IndexError in make_plots fvcom forecast-x2 research

Add VCS revision recording to run_fvcom

Update SalishSeaNowcast fig-dev docs

fix SalishSeaTools unit tests

fix old colander dependency in SOG


Stack:
* create NEMO_Nowcast.workers.spotter to monitor and optionally kill workers that tend to get stuck; initial use cases: collect_weather, make_ww3_wind_file
* wwatch3 run success confirmation
* fix warnings in figure modules
* fix get_vfpa_hadcp MMSI AttributeError issue
* debug gemlam interpolation
Done:
*
