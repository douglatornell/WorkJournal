*****************
2021 Work Journal
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

Fri 1-Jan-2021
^^^^^^^^^^^^^^

Week 42 of UBC work-from-home due to COVID-19


Week 1
------

Mon 4-Jan-2021
^^^^^^^^^^^^^^

Week 43 of UBC work-from-home due to COVID-19

Group mtg; see whiteboard.
(MOAD)

Created 2021 work journal.

On-boarding planning mtg for Keegan & Aline w/ Susan, Elise & Karyn:
* Keegan w/ Karyn
* Aline w/ Elise
Slack call w/ Becca re: LoadFiles notebook, dask, etc.
Helped Karyn with accidentally committed mycert files in analysis-karyn.
(SalishSeaCast)

Change cookiecutter-analysis-repo to make SalishSeaCast the default GitHub org choice; updated MOAD docs to reflect that change.
Added SalishSeaTools deps pkgs to cookiecutter-analysis-repo env description.
Updated MOAD docs copyright year range.
Got GHA linkcheck failures in MOAD docs due to x2go wiki links.
(MOAD)


Tue 5-Jan-2021
^^^^^^^^^^^^^^

Investigated GHA linkcheck failures in MOAD docs due to x2go wiki links:
* also fails locally
* maybe due to outdated certifi and/or ca-certificate; updated them in moad-docs env; still no-go
Continued work on Getting Started section of MOAD docs.
(MOAD)

Requested, received, and set up Zoom account on UBC license.
Set up on-boarding mtg w/ Aline & Keegan for Thu 09:00.
Checked hake & halibut that Aline & Keegan will use for /results, /results2 & /data mounts; opened tickket to get /results2 and /data mounted on hake.
Uploaded LinuxCommandLine.pdf to Google Drive.
(SalishSeaCast)

See work journal.
(Ocean Navigator)


Wed 6-Jan-2021
^^^^^^^^^^^^^^

See work journal.
(Ocean Navigator)

Joined initial on-boarding Zoom for Aline & Keegan joinng MOAD to work with Elise & Karyn.
(SalishSeaCast)

FAL estate work: deposit BCE & MFC Q4 cheques; pay MCL CRA balance owing.

Wrote preliminary bash config section in MOAD docs.
(MOAD)


Thu 7-Jan-2021
^^^^^^^^^^^^^^

Did computing on-boarding session w/ Aline & Keegan; chaotic due to /ocaean failures and no Linux accounts for them yet.
(SalishSeaCast)

Got more warnings on kudu that root file system in low on space; that means /home/doug/; did some cleanup and recovered 12 of ~100 Gb.
Updated kudu to 20.10 groovy.
Moved minecraft from ~/.minecraft to /media/doug/warehouse/minecraft via symlink.
Discovered that flatpak installations are consuming >8Gb in /home/doug/; used https://github.com/flatpak/flatpak/issues/1224 to try to move installations; didn't work.

Cycled to West Point to pick up truing stand adapters and brake pads, then up to Blanca and home via Jericho (10km)


Fri 8-Jan-2021
^^^^^^^^^^^^^^

Experimented with xarray and hvplot, inspired by Rich Signell's video; didn't work worth a damn.
(MOAD)

Started work on a module to calc day averages of phytos for 6 mo periods for Tereza; PythonNotes/xarray-dayavg/
(SalishSeaCast)


Sat 9-Jan-2021
^^^^^^^^^^^^^^

Continued work on a module to calc day averages of phytos for 6 mo periods for Tereza; PythonNotes/xarray-dayavg/
(SalishSeaCast)

Drove to White Rock for Susan to visit M; walked in Ruth Johnson Park.


Sun 10-Jan-2021
^^^^^^^^^^^^^^^

Finances and Minecraft :-)


Week 2
------

Mon 11-Jan-2021
^^^^^^^^^^^^^^^

Finished work on a module to calc day averages of phytos for 6 mo periods for Tereza; PythonNotes/xarray-dayavg/ but decided to push it quietly.
Continued computing on-boarding w/ Keegan & Aline; still auth problems on hake/halibut/salish.
nowcast-agrif run failed due to orted issue; recovery at ~17:30:
  make_forcing_links orcinus-nowcast-agrif nowncast-agrif 2021-01-11
    job started, but now output; more orted issues?
(SalishSeaCast)


Tue 12-Jan-2021
^^^^^^^^^^^^^^^

Work at UBC while Rita is at home.


nowcast-agrif backfilling:
  make_forcing_links orcinus-nowcast-agrif nowncast-agrif 2021-01-11
  make_forcing_links orcinus-nowcast-agrif nowncast-agrif 2021-01-12
    failed; retried

Finished computing on-boarding w/ Keegan & Aline; they have to use VPN to access hake/halibut/salish.
(SalishSeaCast)


Add Git editor commands link to docs.




jupyter kernelspec uninstall unwanted-kernel



TODO:

Add `export CLICOLOR=auto` to bash setup docs for Mac.

https://linuxize.com/post/getting-started-with-tmux/

update unpublished status of Olson, et al (2020)

update deployment docs re: spinning up a new compute node

Fix permissions in /opp dirs

OPPTools PRs:
  add numpy-indexed dependency
  fix pyproj.Proj() initializations
  fix nctime().strftime in OPPTools.utils.fvcom_postprocess.vertical_transect_snap()


Add CI workflows to run linkcheck on docs; see SalishSeaCast#repos-maint channel:
  need sphinx>3.1 in env
  example workflow in salishsea-site repo
  don't forget to add sphinx & sphinx_rtd_theme to environment-test.yaml


Update cookiecutter-MOAD-pypkg re: migration from hg to git, and requirements.txt in top level directory; probably more issues too.


15jun20: check mitigation of "index exceeds dimension bounds" IndexError in make_plots fvcom forecast-x2 research

Add VCS revision recording to run_fvcom

Update SalishSeaNowcast fig-dev docs

fix SalishSeaTools unit tests

fix old colander dependency in SOG

Fix Pillow security issue in analysis-doug


Stack:
* create NEMO_Nowcast.workers.spotter to monitor and optionally kill workers that tend to get stuck; initial use cases: collect_weather, make_ww3_wind_file
* wwatch3 run success confirmation
* fix warnings in figure modules
* fix get_vfpa_hadcp MMSI AttributeError issue
* debug gemlam interpolation
Done:
*
