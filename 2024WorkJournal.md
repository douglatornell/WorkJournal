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

Day 1 of v202111 in production.
Startup problems:
* forgot to drop old runoff file from upload forcing re: missing Fraser obs
* forgot to edit nowcast/31dec23/namelist_cfg on arbutus to adjust starting time step number for
  nowcast-blue run
* nowcast-blue/namelist.light was incorrect; Susan fixed
nowcast-blue time stepping at 09:20
forecast success
nowcast-green time stepping at 10:25
make_ww3_wind_file forecast stalled; killed and re-run; took 2 tries; arbutus terminal sluggish

TODO:
* tag repos with PROD-nowcast-green-202111:
  * NEMO-3.6-code
  * XIOS-2
  * XIOS-ARCH - maybe special ??
  * grid
  * rivers-climatology
  * SS-run-sets
  * tides
  * tracers
* update to tags on arbutus
* delete PROD-nowcast-green-201905 branches on arbutus
(SalishSeaCast)

Continued SalishSeaNowcast updates for v202111:
* branch: v202111-nowcast
* PR#223 -
* dropped launch of make_runoff_file from automation re: missing Fraser obs now,
  and it's replaced by make_v202111_runoff_file
Fixed test_download_live_ocean failure on khawla with nccopy not found:
* branch: mock-NEMO-Cmd-api-deflate
* PR#
* added monkeypatch mock for nemo_cmd.api.deflate() to avoid launching nccopy in subprocess in test

TODO:
* revert drop of make_runoff_file launch and upload of 201702 runoff file because nowcast-agrif
  needs it
* test_download_live_ocean fails on khawla with nccopy not found
* test_make_feeds fails in pytest-with-coverage due to python-feedgen v1.0.0
* remove make_runoff_file worker
* rename make_v202111_runoff_file to make_runoff_file
  * drop daily_river_flows module and tests ??
* add config tests for run type[*][mesh mask]
* add config tests for run type[*][bathymetry]
* add config tests for run type[*][land processor elimination]
* add config tests for run type[*][run sets dir]
* improve test_run_NEMO test for forcing symlinks ??
* add tests for _upload_*_files in upload_forcing worker: ssh, turbidity, runoff, weather
(SalishSeaNowcast)



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
