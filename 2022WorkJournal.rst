*****************
2022 Work Journal
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

Sat 1-Jan-2022
^^^^^^^^^^^^^^





TODO:
* for MoaceanParcels
  * add disappeared particle kernel w/ Birgit's notebook as docs
  * add docs re: adding pkgs to env
  * add docs re: adding kernels to pkg
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
MIDOSS:
* figure out how to merge/cherrypick relevant changes from Rachael's add_terminal branch in moad_tools

Fix ariane docs:
* maybe re:  adding a bin-like directory to prefix gets rid of errors from doc/ and examples/ that confused Becca ???
 versions re: .bashrc



Update ONC URLs to https://data.oceannetworks.ca/

jupyter kernelspec uninstall unwanted-kernel



TODO:

https://linuxize.com/post/getting-started-with-tmux/

update deployment docs re: spinning up a new compute node


OPPTools PRs:
  add numpy-indexed dependency
  fix pyproj.Proj() initializations
  fix nctime().strftime in OPPTools.utils.fvcom_postprocess.vertical_transect_snap()


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
