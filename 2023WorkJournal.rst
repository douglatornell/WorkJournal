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

Murrayville

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


Week 1
------

Mon 2-Jan-2023
^^^^^^^^^^^^^^

**Statutory Holiday** - New Year's Day lieu day

Installed PyCharm 2022.3.1 on khawla.

collect_river_data is not collecting Roberts Creek; best guess is that manager needed to be
restarted to get Roberts Creek into its config, so did that.
(SalishSeaCast)


Tue 3-Jan-2023
^^^^^^^^^^^^^^

collect_weather 06 didn't complete
  * 573 of 576 files downloaded despite lots of error messages in log:
    * 503 Service Unavailable
    * 110 Connection timed out
    * 104 Connection reset by peer
    * 111 Connection refused
* recovery started at ~10:15
    kill collect_weather 06
    mv /results/forcing/atmospheric/GEM2.5/GRIB/20230103/06/ aside
    download_weather 06 2.5km
    wait for forecast2 runs to finish; delayed ~9.5h
    download_weather 12 2.5km; delayed ~4.5h
    collect_weather 18
    rm -rf /results/forcing/atmospheric/GEM2.5/GRIB/20230103/06.aside
Clean up /SalishSeaCast/datamart/hrdps-west/[00|06|12|18]/*
Confirmed that collect_river_data is working for Roberts Creek after yesterday's manager restart.
collect_weather 18 didn't complete
  * 566 of 576 files downloaded
  * lots of error messages in log:
    * 104 Connection reset by peer
    * 111 Connection refused
* recovery started at ~15:50
    kill collect_weather 18
    mv /results/forcing/atmospheric/GEM2.5/GRIB/20230103/18/ aside
    download_weather 18 2.5km
    download_weather 00 1km --yesterday  # because after 16:00 Pacific == 0:00 UTC
    download_weather 12 1km
    collect_weather 00
    rm -rf /results/forcing/atmospheric/GEM2.5/GRIB/20230103/18.aside
(SalishSeaCast)

There are finally releases for pillow 9.4.0 and gitpython 3.1.30 that address CVEs;
squash-merged dependabot PRs re: pillow CVE-2022-45199 re: DoS vulnerability;
no PRs yet for GitPython (released 3 days ago)

Squash-merged dependabot PRs re: jupyter-core CVE-2022-39286 re: arbitrary code execution 
vulnerability

Started researching how to get USGS river discharge data into automation:
* https://waterservices.usgs.gov/
* messed around with WaterML and owslib but just got frustrated by XML, SOAP-ish services
  and bad code/docs
* decided to use httpx and json
* discussed error handling w/ Susan
  * enable follow_redirects for httpx.get()
  * don't do tenacity.retry()
  * log an error if there is not data added to obs file
  * Susan will enable make_runoff_file to handle missing obs by persistence or fitting,
    depending on the river
(SalishSeaNowcast)


Wed 4-Jan-2023
^^^^^^^^^^^^^^

collect_weather 06 didn't complete
  * 554 of 576 files downloaded
  * lots of error messages in log:
    * 110 Connection timed out
    * 111 Connection refused
    * 503 Service Unavailable
* recovery started at ~09:20
    kill collect_weather 06
    mv /results/forcing/atmospheric/GEM2.5/GRIB/20230104/06/ aside
    download_weather 06 2.5km
    wait for forecast2 runs to finish; delayed ~8.5h
    download_weather 12 2.5km; delayed ~3.5h
    collect_weather 18 2.5km
    rm -rf /results/forcing/atmospheric/GEM2.5/GRIB/20230104/06.aside
Clean up /SalishSeaCast/datamart/hrdps-west/[00|06|12|18]/*
``make_plots fvcom nowcast-r12 research`` failed with many ``KeyError: 'Times'``:
* investigation:
  * run crashed due to restart file "time dimension equal zero"
  * 03jan23 run aborted with no message, just vh_r12_abort.nc file
* recovery:
    launch_remote_worker arbutus make_fvcom_boundary arbutus r12 nowcast 2023-01-03
(SalishSeaCast)

Started work on adding USGS rivers collect_river_data:
branch: add-usgs-rivers
PR#143
* added httpx as dependency
* added data_src (ECCC or USGS) arg to collect_river_data worker
* added ECCC key (ECCC or USGS) to rivers.stations in config
(SalishSeaNowcast)

Updated firmware on khawla and installed nvidia-driver-525.60.11.

Installed Iris 1.5.1, sodium 0.4.8, and lithium 0.10.4. 
Frame rate with shaders on is way worse (~7 fps) than it used to be :-(


Thu 5-Jan-2023
^^^^^^^^^^^^^^

collect_weather 00 didn't complete
  * 389 of 576 files downloaded
  * 1 error messages in log:
    * 404 no queue
* recovery started at ~09:40
    kill collect_weather 00
    mv /results/forcing/atmospheric/GEM2.5/GRIB/20230105/00/ aside
    download_weather 00 2.5km
    download_weather 06 2.5km
    wait for forecast2 runs to finish; delayed ~8.5h
    download_weather 12 2.5km; delayed ~4h
    collect_weather 18 2.5km
    rm -rf /results/forcing/atmospheric/GEM2.5/GRIB/20230105/00.aside
Clean up /SalishSeaCast/datamart/hrdps-west/[00|06|12|18]/*
Backfill nowcast-r12:
  wait for today's run to fail at ~14:30
    launch_remote_worker arbutus make_fvcom_boundary arbutus r12 nowcast 2023-01-04
(SalishSeaCast)

Investigated security alert on python-future:
* pkg seems unmaintained; recommendation is to drop it because it is from 2to3 Earth
* used by numpy-indexed which we install explicitly, due to use by OPPTools
  * numpy-indexed last commit was 22-Jan-2019; Python versions listed are 2.7 and 3.5;
    unmaintained??
  * numpy-indexed is imported in OPPTools.general_utilities.mut **but use is commented out**
    so I can probably work around it in my fork
* used by commonmark due it being a dependency for rich
  * commonmark is archived; recommended alternative is markdown-it-py
  * rich has 5-month-old PR#2439 that switches from commonmark to markdown-it-py
Continued work on adding USGS rivers collect_river_data:
branch: add-usgs-rivers
PR#143
* added USGS rivers to config
* refactored test_collect_river_data to use pytest.monkeypatch instead of unittest.mock.patch
* refactored ECCC day-avg discharge calc function in prep for adding USGS REST query function
(SalishSeaNowcast)

UBC-IOS modeling collab mtg:
* Amber: wavelets for teleconnection of hypoxia and aragonite corrosion in NEP36 results
* teleconnections == climate anomalies related over large distances


Fri 6-Jan-2023
^^^^^^^^^^^^^^

Backfill nowcast-r12:
  wait for today's run to fail at ~10:30
    launch_remote_worker arbutus make_fvcom_boundary arbutus r12 nowcast 2023-01-05
    wait for run to finish at ~21:00
    launch_remote_worker arbutus make_fvcom_boundary arbutus r12 nowcast 2023-01-06
UptimeRobot report that ERDDAP went offline for ~3min at ``Date modified: 2023-01-06 20:10:00``
(SalishSeaCast)

Continued work on adding USGS rivers collect_river_data:
branch: add-usgs-rivers
PR#143
* added pytest-httpx as dep for dev & test envs
* added USGS river REST query function and unit tests
* pulled changes to skookum and changed to branch for production testing; 
  restarted manager to load new config
* ran collect_river_data for 4 rivers from 1-5 Jan in command-line --debug bash loops
(SalishSeaNowcast)


Sat 7-Jan-2023
^^^^^^^^^^^^^^

collect_river_data USGS for all 4 rivers failed with empty timeSeries messages;
successfully re-ran manually at ~11:30
Fraser River turbidity data stream stopped on 6jan; web page frozen at 
(SalishSeaCast)

Experimented with 1password as ssh agent for more than git commit signing;
tested for tyee


Sun 8-Jan-2023
^^^^^^^^^^^^^^

More experiments w/ .ssh/config and 1password ssh agent; agent is now default;
Added lots of:
  IdentitiesOnly yes
  IdentityAgent None
to .ssh/config for situations that don'w use default ed25519 key.

Started work on updating packaging docs re: recent modernization to pyproject.toml and hatch.
(MOAD docs)

Fixed typo in name of Nisqually River that Susan noticed.
Manually ran collect_river_data for 4 USGS rivers that fail in early morning automation.
(SalishSeaNowcast)


Week 2
------

Mon 9-Jan-2023
^^^^^^^^^^^^^^

Resumed backfilling day & month avg files using nowcast.workers.day_month_avgs.py module:
* mar14
  * 20mar14 physics is another case of make_averaged_dataset worker just hanging
  * resolved by running ``reshapr extract`` on salish
* apr14
  * 28apr14 physics is another case of make_averaged_dataset worker just hanging
Created ``/results2/SalishSea/month-avg.202111/day_avg.py`` to run ``reshapr extract`` on salish
and rename resulting file correctly
* may14
  * 27may14 biology is another case of make_averaged_dataset worker just hanging
  * fixed with ``month-avg.202111/day_avg.py``
* jun14 success
* jul14 success
(Hindcast)

Manually ran collect_river_data for 4 USGS rivers that fail in early morning automation.
(SalishSeaNowcast)

Group mtg; see whiteboard.
(MOAD)

Continued work on adding USGS rivers collect_river_data:
branch: add-usgs-rivers
PR#143
* changed next_workers to run collect_river_data for USGS rivers after [collect|download]_weather 12
  because obs are not available at PST time when [collect|download]_weather 06 runs
(SalishSeaNowcast)


Tue 10-Jan-2023
^^^^^^^^^^^^^^^

Worked at ESB while Rita was at home.

Discussion of Python modules & functions w/ Karyn & Raisha; see 
``analysis-doug/notebooks/mods_and_funcs/``

Finished adding USGS rivers collect_river_data:
branch: add-usgs-rivers
PR#143; rebase-merged
* USGS rivers successfully collected in production after collect_weather 12 finished
* switched back to main branch on skookum, pulled changes, and restarted manager to ensure
  that update config takes effect
Released v22.1 (first release since 19.1!!) and bumped version to 23.1.dev0 for next dev cycle.
Triaged issues to clean up some stale ones and move some to 23.1 milestone.
(SalishSeaNowcast)

Continued backfilling day & month avg files using nowcast.workers.day_month_avgs.py module:
* aug14 success
* sep14
  * 22sep14 physics is another case of make_averaged_dataset worker just hanging
  * fixed with ``month-avg.202111/day_avg.py``
(Hindcast)


Wed 11-Jan-2023
^^^^^^^^^^^^^^^

SharcNet webinar re: future Canadian ARC directions & performance:
Mark Hahn, McMaster
* dies/chiplets make up packages/sockets
* cache line = 64 bytes; nothing happens on less than a cache line, in contrast to conceptual
  byte addressable memory
* more cores, higher burst clock speeds, larger L3 cache (Intel is limited), higher memory bandwidth
* core-seconds vs. cores (as I have done) is a good way to view scaling performance
* all broadwell nodes going away in next year; slow
* tradeoffs around usage profiles:
  * CPU vs. GPU
  * compact vs. memory-intensive
* Intel has been stuck at 14 nm fabs
* AMD reinvented itself:
  * chiplets win due to better yields than large chips
  * 7 & 5 nm fab from TSMC
* Intel Sapphire Rapids introduced yesterday (4th gen Xenon) uses chiplets
  * possible memory in chiplet; terrabyte memory bandwisth
  * very hot: 350W TPD; systems designed for 140W
* AMD next will be Genoa w/ 96 core; also 360W hot
  * huge cache in pkg
  * beyond that 128 cores w/ smaller L3 cache; 256 core per node @ 250W
* no likely hardware updates this year due to funding and proposal lead time
* graham broadwell nodes are from Huawei (political optics),
  power dissipation per core is 2x Skylake, out of warranty
* local SSD use is variable among workloads
* new SSD approach memory speed
* think about:
  * NEMO w/o MPI for fat nodes
  * XIOS and node-local SSD

Continued backfilling day & month avg files using nowcast.workers.day_month_avgs.py module:
* oct14 success
* nov14 
  * 12nov14 physics is another case of make_averaged_dataset worker just hanging
  * fixed with ``month-avg.202111/day_avg.py``
* dec14 success
* jan15 
  * 21jan15 physics is another case of make_averaged_dataset worker just hanging
  * fixed with ``month-avg.202111/day_avg.py``
* feb15 success
* mar15 success
(Hindcast)

Modernized packaging:
* metadata to pyproject.toml
* chg to hatchling
* chg to importlib.metadata.version()
* move __version__ to __about__
* clear caches
* update requirements.txt
Added version release notes.
Pinned sphinx-rtd-theme=1.1.1 to avoid incompatible versions of Sphinx and docutils
(SalishSeaNowcast)

Dropped Click<8.0 pin that was added for fiona and rasterio pkgs in Jun-2021.
(moad_tools)


Thu 12-Jan-2023
^^^^^^^^^^^^^^^

Started migration of Slack SADA workspace into private channels in SalishSeaCast workspace.

Goofed off.

Reverted khawla to Nvidia 515.65.01 drivers: excessive fan operation stopped
and Minecraft frame rates returned to "normal".


Fri 13-Jan-2023
^^^^^^^^^^^^^^^

Continued backfilling day & month avg files using nowcast.workers.day_month_avgs.py module:
* apr15 success
* may15 success
* jun15 
  * 07jun15 biology is another case of make_averaged_dataset worker just hanging
  * fixed with ``month-avg.202111/day_avg.py``
(Hindcast)

Finished migration of Slack SADA workspace into private channels in SalishSeaCast workspace:
* merged users
* imported channels as private with #sada- prefix
* got 19 of 29 files:
  * reviewed missed ones and founds that they were all in DMs and of no consequenc
* manually copy-pasted notes from priovate #fal-estate to #sada-fal-estate

See work journal.
(Resilient-C)


Sat 14-Jan-2023
^^^^^^^^^^^^^^^

Drove to White Rock to visit J&M.

Goofed off.


Sun 15-Jan-2023
^^^^^^^^^^^^^^^

FAL estate work:
* sent scan of CRA 2022 assessment to Cameron
* sorted out handling of estate savings account in GnuCash
* transferred funds for 2022 disbursements and storage locker rent, and jan-22 locker rent


Week 3
------

Mon 16-Jan-2023
^^^^^^^^^^^^^^^

Continued backfilling day & month avg files using ``nowcast.workers.day_month_avgs.py`` module.
jul15 is the beginning of a section of runs where automation produced 1d files with ``time``
coordinate name instead of ``time_counter``; removed check for 1d file from ``day_month_avgs.py``
to force extraction of 1d files with ``time_counter``
* jul15 success
Added ``--check-day-avg-exists/--no-check-day-avg-exists`` option and output of  count of 
month-avg files to ``day_month_avgs.py``
* aug15 success
* sep15 success
* oct15 success
* 1d files with ``time`` coordinate stop at end of oct15
(Hindcast)

Continued work on updating packaging docs re: recent modernization to pyproject.toml and hatch.
(MOAD docs)

dependabot PRs for gitpython and future landed


Tue 17-Jan-2023
^^^^^^^^^^^^^^^

Continued backfilling day & month avg files using ``nowcast.workers.day_month_avgs.py`` module.
* nov15 
  * some days skipped; problems at month-avg due to mixed time coordinate names
  * re-ran with --no-check-day-avg-exists
* dec15 success
* jan16 with --no-check-day-avg-exists success
* feb16 with --no-check-day-avg-exists success
* mar16 with --no-check-day-avg-exists 
  * mar16 chemistry is a case of make_averaged_dataset worker not workingh without a msg
  * eventually figured out that 14mar16 chemistry 1d file had time coord named "time"
  * fixed by running ``month-avg.202111/day_avg.py`` then ``month-avg.202111/month_avg.py`` on  
    salish
(Hindcast)

Ran periodic gha-workflows-checker check: all good.

Squash-merged dependabot PRs:
* GitPython re: CVE-2022-24439 re: remote code execution
* future re: CVE-2022-40899 re: DoS attack
* repos:
  * SalishSeaCmd
  * gha-workflow-checker
  * Reshapr
  * NEMO-Cmd
  * cookiecutter-djl-pypkg
  * MEOPAR-ATM-2019-06-11
  * AtlantisCmd
  * WWatch3-Cmd
Group mtg; see whiteboard.
(MOAD)

After discussion w/ Susan, decided to archive WWatch3-Cmd on GitHub instead of putting work
into keeping up with GHA and dependabot alerts.
(WWatch3-Cmd)

Weekly group mtg; see whiteboard
(MOAD)

Helped Raisha sort out her GitHub ssh key issue; ssh-agent on her mac had stopped.
Tried to help with VS Code Jupyter R kernel not working:
* failed to help on Slack
* can't get local setup to work on khawla
(Atlantis)


Wed 18-Jan-2023
^^^^^^^^^^^^^^^

Continued backfilling day & month avg files using ``nowcast.workers.day_month_avgs.py`` module;
used --no-check-day-avg-exists unless otherwise noted
* apr16 success
* may16 
  * may16 biology is a case of make_averaged_dataset worker not workingh without a msg
  * fixed by running ``month-avg.202111/month_avg.py`` on salish
* jun16 
  * 28jun16 physics is another case of make_averaged_dataset worker just hanging
  * fixed with ``month-avg.202111/day_avg.py``
* jul16 success
(Hindcast)


Thu 19-Jan-2023
^^^^^^^^^^^^^^^

Continued backfilling day & month avg files using ``nowcast.workers.day_month_avgs.py`` module;
used --no-check-day-avg-exists unless otherwise noted
* change salish env for dask cluster from reshapr to /SalishSeaCast/nowcast-env to silence version
  difference messages from ``nowcast.workers.day_month_avgs.py`` runnin in that env on skookum; 
  makes progress messages easier to see
* aug16 success
* sep16 success
* oct16 success
* nov16 success
* dec16 success
* jan17 success
* feb17 success
* mar17 success
* apr17 success
(Hindcast)

Moved gha-workflows-checker code etc. from gha-workflows-checker repo to gha-workflows repo.
Archived gha-workflows-checker repo.

Finished updating packaging docs re: recent modernization to pyproject.toml and hatch.
Set up branch build on readthedocs for Susan to review.
(MOAD docs)


Fri 20-Jan-2023
^^^^^^^^^^^^^^^

Continued backfilling day & month avg files using ``nowcast.workers.day_month_avgs.py`` module;
used --no-check-day-avg-exists unless otherwise noted
* may17 success
* jun17 success
* jul17 success
* aug17 success
* sep17 success
* oct17 success
* nov17 success
* dec17 success
(Hindcast)

Changed to use reusable GHA workflows.
Change to Python 3.11 for dev and dropped support for 3.6 through 3.9.
Started work on fixing broken links and old content in docs.
(NEMO_Nowcast)


Sat 21-Jan-2023
^^^^^^^^^^^^^^^

Continued backfilling day & month avg files using ``nowcast.workers.day_month_avgs.py`` module;
used --no-check-day-avg-exists unless otherwise noted
* jan18 success
* feb18 success
* mar18 success
* apr18 success
* may18 success
* jun18 success
(Hindcast)


Sun 22-Jan-2023
^^^^^^^^^^^^^^^

Continued backfilling day & month avg files using ``nowcast.workers.day_month_avgs.py`` module;
used --no-check-day-avg-exists unless otherwise noted
* jul18 success
* aug18 success
* sep18 success
* oct18 success
* nov18 success
* dec18 success
(Hindcast)


Week 4
------

Mon 23-Jan-2023
^^^^^^^^^^^^^^^

Continued backfilling day & month avg files using ``nowcast.workers.day_month_avgs.py`` module;
used --no-check-day-avg-exists unless otherwise noted
* jan19 success
* feb19 success
* mar19 success
* apr19 success
* may19 success
(Hindcast)

Worked on getting current version of R working with Jupyter and VS Code:
* added r-languageserver to env
  * installed VS Code R extension, set r.rterm.linux to path to R; got R in a terminal
* can't get past --salve bad option; tried older Python and R versions, all the same

Finished fixing broken links and old content in docs.
Released v22.1.
(NEMO_Nowcast)


Tue 24-Jan-2023
^^^^^^^^^^^^^^^

Worked at ESB while Rita was at home.

collect_river_data failed for Snohomish; time series empty.
(SalishSeaCast)

Weekly group mtg; see whiteboard
(MOAD)

Continued backfilling day & month avg files using ``nowcast.workers.day_month_avgs.py`` module;
used --no-check-day-avg-exists unless otherwise noted
* jun19 success
* jul19 success
* aug19 success
(Hindcast)

Squash-merged dependabot PRs:
* certifi
* cryptography
Released v22.2 and bumped version to 23.1.dev0.
Pinned sphinx-rtd-theme=1.1.1 until 1.2 is released re: incompatible versions of docutils
and Sphinx.
Changed to use reusable GHA workflows.
(salishsea-site)


Wed 25-Jan-2023
^^^^^^^^^^^^^^^

Continued backfilling day & month avg files using ``nowcast.workers.day_month_avgs.py`` module;
used --no-check-day-avg-exists unless otherwise noted
* sep19 success
* oct19 success
* nov19 success
* dec19 success
* jan20 success
* feb20 success
(Hindcast)

Squash-merged dependabot PR re: future.
(SalishSeaNowcast)

Experimented with new setup for running SalishSeaCast NEMO on graham:
* installed Miniforge3 (conda 22.9.0, Python 3.10.8) in $HOME
  (sam,e process as we use on Waterhole machines instead of my preferred Mambaforge-pypy3)
    curl -LO https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-Linux-x86_64.sh
* got warning about PYTHONPATH defined in env:
  * point to /cvmfs/soft.computecanada.ca/custom/python/site-packages which contains ``_manylinux.py``
* allowed modification of ``.bash_profile``
* updated conda to latest version:
    conda update -n base -c conda-forge conda
* pulled updated into all MEOPAR repo clones
* created salishsea-cmd env:
    conda env create -f SalishSeaCmd/envs/environment-hpc.yaml
* activated env and installed pkgs in --user mode
    conda activate salishsea-cmd
    python3 -m pip install --user -e NEMO-Cmd/
    python3 -m pip install --user -e SalishSeaCmd/

Discussed new rivers runoff code w/ Susan.
(SalishSeaCast)

Helped Camryn set up extractions for 202111 month-avg salinity and u/v velocities.

Pinned sphinx-rtd-theme=1.1.1 until 1.2 is released re: incompatible versions of docutils
and Sphinx.
Corrected SalishSeaCast v202111 geo ref dataset path in model profile; left-over from before
spin-up runs were moved to separate directory tree.
Released v22.2 and bumped version to 23.1.dev0.
(Reshapr)


Thu 26-Jan-2023
^^^^^^^^^^^^^^^

Continued backfilling day & month avg files using ``nowcast.workers.day_month_avgs.py`` module;
used --no-check-day-avg-exists unless otherwise noted
* mar20 success
* apr20 success
* may20 success
* jun20 
  * 08jun chemistry is the first case since jun16 of make_averaged_dataset worker not working 
    without a msg
  * fixed by running ``month-avg.202111/day_avg.py`` and ``month-avg.202111/month_avg.py`` on salish
* jul20 success
(Hindcast)

Coffee w/ Becca on Slack.

Helped Karyn on Zoom w/ accessing 202111 month-avg files.

Started reading Susan's mixing paper that I am co-author on.

Helped Matt on Slack w/ ssh keys.

EOAS Colloquium: Jan Newton on ocean acidification.

Dinner w/ Jan and Dan at Cactus Club English Bay.


Fri 27-Jan-2023
^^^^^^^^^^^^^^^

Continued backfilling day & month avg files using ``nowcast.workers.day_month_avgs.py`` module;
used --no-check-day-avg-exists unless otherwise noted
* aug20 
  * 04aug chemistry is the another of make_averaged_dataset worker not working 
    without a msg
  * fixed by running ``month-avg.202111/day_avg.py`` on salish
* sep20 success
* oct20 success
* nov20 success
* dec20 
  * 04dec biology is the another of make_averaged_dataset worker not working 
    without a msg
  * fixed by running ``month-avg.202111/day_avg.py`` on salish
* jan21 success
* feb21 success
* mar21 success
* apr21 success
(Hindcast)

Continued reading Susan's mixing paper that I am co-author on.

Helped Matt on Slack w/ Jupyter and Parcels in VS Code.

Enabled GitHub secret scanning for all public repos in all orgs except MIDOSS.

Started thinking about how to migrate Susan's new rivers processing code into repo:
* branch: v202111-rivers
* copy tools/SalishSeaTools/I_ForcingFiles/Rivers/DailyRiverFlows.py into SSN/nowcast/
* copy tools/SalishSeaTools/I_ForcingFiles/Rivers/ProductionDailyRiverNCfile.ipynb into
  notebooks/
  * strip out function defs that are in DailyRiverFlows.py
  * create ref image cells for comparison baseline during refactoring
Cleaned up environment-test and environment-linkcheck env descriptions
(SalishSeaNowcast)


Sat 28-Jan-2023
^^^^^^^^^^^^^^^

Continued backfilling day & month avg files using ``nowcast.workers.day_month_avgs.py`` module;
* may21 success
* jun21 success
(Hindcast)

Changed to use reusable GHA workflows; the last repo that needed this!!
Added badges to README.
Created issue #20 to review use of :kbd: role.
(SalishSeaCast docs)

Drove to White Rock to visit J&M.


Sun 29-Jan-2023
^^^^^^^^^^^^^^^

Continued backfilling day & month avg files using ``nowcast.workers.day_month_avgs.py`` module;
* jul21 
  * 30jul biology is the another of make_averaged_dataset worker not working without a msg
  * fixed by running ``month-avg.202111/day_avg.py`` on salish
* aug21 
  * 06aug physics is the another of make_averaged_dataset worker not working without a msg
  * fixed by running ``month-avg.202111/day_avg.py`` on salish
(Hindcast)


Week 5
------

Mon 30-Jan-2023
^^^^^^^^^^^^^^^

Continued backfilling day & month avg files using ``nowcast.workers.day_month_avgs.py`` module;
* sep21 success
* oct21 success
* nov21 success
* dec21 success
* oct-dec 2022 for v201905 after reminder of that processing stream from Karyn
* jan22 success
* feb22 success
* mar22 success
(Hindcast)

Updated PyCharm on khawla to 2022.3.2.

Ran periodic gha-workflows-checker check: all good.

Fixed bugs in sphinx-linkcheck workflow; PRs #21 & #22.
Worked on fixing broken and redirected links:
* branch: fix-broken-links
* PR#23
* https://nbviewer.org/github/SalishSeaCast/tools/blob/master/* -> .../main/*
* https://www.westgrid.ca/support/systems/orcinus; deleted section
* https://www.waterlevels.gc.ca/eng/data#s2 -> https://www.pac.dfo-mpo.gc.ca/science/charts-cartes/obs-app/observed-eng.aspx?StationID=07786
* https://www.pac.dfo-mpo.gc.ca/science/oceans/data-donnees/search-recherche/profiles-eng.asp
* https://cfpub.epa.gov/surf/state.cfm?statepostal=WA -> https://mywaterway.epa.gov/
(SalishSeaCast docs)

Phys Ocgy seminar: Ruiqi Li, U Coloroado; Bivalves

Updated .gitignore files in cookiecutter-analysis-repo to include more OS and editor templates;
inspired by seeing ``.DS_store`` files in analysis-jose.
(cookiecutter-analysis-repo)

Started migrating Susan's new rivers processing code into repo:
* branch: v202111-rivers
* copied tools/SalishSeaTools/I_ForcingFiles/Rivers/DailyRiverFlows.py to 
  SalishSeaNowcast/nowcast/daily_river_flows.py
(SalishSeaNowcast)

FAL estate work:
* mtg at TD s/ Sahi's successor Christine re: CML chq from CRA; no progress


Tue 31-Jan-2023
^^^^^^^^^^^^^^^

FAL estate work re: MCL chq from CRA
* Christine called with info & instructions for me to contact TD Estates
* reviewed comms w/ CRA and confirmed that this should be only chq
* telcon w/ TD estates

Continued backfilling day & month avg files using ``nowcast.workers.day_month_avgs.py`` module;
* apr22 success
* may22 
  * 31may biology is the another of make_averaged_dataset worker not working without a msg
  * fixed by running ``month-avg.202111/day_avg.py`` on salish
* jun22 success
* jul22 success
* aug22 success
* sep22 success
* oct22 success
* nov22 success
(Hindcast)

collect_weather 12 had not finished at 09:15
* investigation:
  * log shows server disconnect at 07:16, than continueous connection timeouts, retrying every 64 s2
  * 364 fo 576 files downloaded
* recovery started at ~09:35
    kill collect_weather 12 2.5km
    mv /results/forcing/atmospheric/GEM2.5/GRIB/20230131/12 aside
    download_weather 12 2.5km
    rm -rf /results/forcing/atmospheric/GEM2.5/GRIB/20230131/12.aside
    collect_weather 18 2.5km
    restart sr_subscribe-hrdps-west
* server resumed operation at ~12:21
sr_subscribe-hydrometric lost server connection on 30jan at ~11:30; restarted at ~09:45
* resumed operation at ~12:22
Experimented with new queues from hpfx.collab.science.gc.ca, longer than default message expiries, and multiple client instances:
* hydrometric-hpfx worked for 2 cycles of .csv file updates
* hrdps-west.hpfx started at ~12:20 to test 18Z files; successful
Tried to use queue on dd.alpha.meteo.gc.ca for 1km HRDPS; connection refused.
(SalishSeaCast)

Group mtg; see whiteboard.
(MOAD)


February
========

Wed 1 Feb-2023
^^^^^^^^^^^^^^^

FAL estate work re: MCL chq from CRA
* mtg w/ Christine at TD to create MCL estate acct and deposit chq

Continued backfilling day & month avg files using ``nowcast.workers.day_month_avgs.py`` module;
* dec22 success
* jan23 day success to 25jan
(Hindcast)

Updated production sarracenia-env:
* branch: update-sarracenia
* PR#147
* reviewed changed in metpx-sarracenia==2.22.10.post2
  * note that dev is well into refactoring to metpx-sr3
* recorded installed pkgs & versions in envs/requirements-sarracenia.txt
* built new env on khawla to compare to production pkgs & versions
* updated environment-sarracenia.yaml
  * change to Python=3.11
  * drop [amqp] option from metpx-sarracenia
* shut down sr_subscribe instances via supervisorctl
* removed sarracenia-env
* built new sarracenia-env
* started sr_subscribe instances via supervisorctl
* recorded installed pkgs & versions in envs/requirements-sarracenia.txt
* confirmed that sr_subscribe hydrometric downloaded files at ~10:10
* dismissed dependabot alert #18 re: setuptools<65.5.1 and CVE-2022-40897 in sarracenia-env
  as "tolerable in project" because some dependency in that env is apparently not ready for 
  setuptools>57.4.0
* confirmed that sr_subscribe hrdps-west downloaded files at ~13:30

* changed sr_subscribe instances to use queues on hpfx
(SalishSeaNowcast)


Thu 2 Feb-2023
^^^^^^^^^^^^^^^

UptimeRobot reported that ERDDAP was down for 3m28s at 08:06 due to connection timout.
(ERDDAP)

make_ssh_files forecast2 didn't find obs for 1feb so persisted forecast
Updated to sentry-sdk 1.14.0 in prod env on skookum
Started changing sr_subscribe instances to use queues on hpfx:
* branch: hpfx-queues
* noticed that Tuesday's test of hrdps-west-hfpx had 2 unwanted directory levels;
  changed strip from 4 to 6 and started another test to /tmp/hrdps-hpfx for tomorrow's 00 forecast;
  success
Continued migrating Susan's new rivers processing code into repo:
* branch: v202111-rivers
* copied tools/SalishSeaTools/I_ForcingFiles/Rivers/ProductionDailyRiverNCfile.ipynb into
  notebooks/
(SalishSeaNowcast)

Deleted no longer used GCC arch files for orcinus; Michael created them 6y ago for debugging and
valgrind which we would not do on orcinus again, and they had incorrect file name convention.
Fixed typos and update README re: SalishSeaCast branding and outdated instructions that mentioned
orcinus.
(XIOS-ARCH)

Added XIOS-2/arch/ symlink names for clusters we use to XIOS-2/.gitignore to prevent
accidental commits.
(XIOS-2)

Resumed work on creating SOG-code-collab repo on GitHub for Nancy & Jared at NAFC to fork.
* TODO:
  * discuss repo name w/ Susan - done
  * discuss absence of copyright notices w/ Susan - done
  * replace .hgignore with .gitignore - done
  * add LICENSE file - done
  * add CITATION file
  * add README.md file
(SOG-code-collab)

MOAD-IOS modeling mtg; Becca.


Fri 3 Feb-2023
^^^^^^^^^^^^^^

Worked at ESB to be there for Becca's defense.

Coffee w/ Karyn.

Finished changing sr_subscribe instances to use queues on hpfx:
* branch: hpfx-queues
* PR#149
* deployed branch on skookum
  * supervisor ops:
    * stop processes
    * reload config
    * remove processes
    * add processes
    * confirm changes by inspecting logs (new log file names)
Continued migrating Susan's new rivers processing code into repo:
* branch: v202111-rivers
* PR#150
* Started merging tools/I_ForcingFiles/Rivers/nowcast.yaml into SalishSeaNowcast/config/nowcast.yaml
(SalishSeaNowcast)

  Becca's M.Sc. defense.


Sat 4 Feb-2023
^^^^^^^^^^^^^^

Continued work on creating SOG-code-collab repo on GitHub for Nancy & Jared at NAFC to fork.
* TODO:
  * discuss repo name w/ Susan - done
  * discuss absence of copyright notices w/ Susan - done
  * replace .hgignore with .gitignore - done
  * add LICENSE file - done
  * add CITATION file
  * add README.md file
(SOG-code-collab)


Sun 5-Feb-2023
^^^^^^^^^^^^^^

Marjorie passed away.

Finished creating SOG-code-collab repo on GitHub for Nancy & Jared at NAFC to fork.
* TODO:
  * discuss repo name w/ Susan - done
  * discuss absence of copyright notices w/ Susan - done
  * replace .hgignore with .gitignore - done
  * add LICENSE file - done
  * add CITATION file - done
  * add README.md file - done
  * add GHA assign-issue-pr workflow - done
Sent email to Jared and Nancy.
(SOG-code-collab)


Week 6
------

Mon 6-Feb-2023
^^^^^^^^^^^^^^

Raisha discovered that Jupyter R kernel startup issue is resolved; probably due to new releases
last week of VS Code and Jupyter extension.

Created issue #151 re: migrating sarracenia to sr3.
Rebase-merged PR#149 re: changing sr_subscribe instances to use queues on hpfx
Continued migrating Susan's new rivers processing code into repo:
* branch: v202111-rivers
* PR#150
* Finished merging tools/I_ForcingFiles/Rivers/nowcast.yaml into 
  SalishSeaNowcast/config/nowcast.yaml
* made minimal changes necessary to get ProductionDailyRiverNCfile notebook to run
(SalishSeaNowcast)

Continued reading Susan's mixing paper that I am co-author on.

Phys Ocgy seminar; Shumin, Jose, Camryn & Cassidy re: Chile field school

nowcast-agrif run failed due to storage failure on orcinus
(SalishSeaCast)


Tue 7-Feb-2023
^^^^^^^^^^^^^^

Woke feeling slow and tired.
Cancelled hearing test and didn't go to ESB as planned.

nowcast-agrif failed due to no restart file; orcinus storage still having problems.
(SalishSeaCast)

Group mtg; see whiteboard.
Helped Camryn w/ day-avg velocity w/ reshapr.
(MOAD)


Wed 8-Feb-2023
^^^^^^^^^^^^^^

Woke feeling better than yesterday.
Negative COVID RAT test.
Slight headache by mid-morning.

nowcast-agrif failed due to no restart file; orcinus storage still having problems;
storage controllers to be rebooted at ~12:00.
06feb23 job completed w/ timeouts
backfilled:
  upload_forcing orcinus-nowcast-agrif nowcast+ 2023-02-06
  upload_forcing orcinus-nowcast-agrif nowcast+ 2023-02-07
  upload_forcing orcinus-nowcast-agrif nowcast+ 2023-02-08
  upload_forcing orcinus-nowcast-agrif turbidity 2023-02-06
  wait for run to finish
  
  upload_forcing orcinus-nowcast-agrif turbidity 2023-02-07
  wait for run to finish
  upload_forcing orcinus-nowcast-agrif turbidity 2023-02-08
(SalishSeaCast)

Started work on reference letter for Ben.

Reviewed cryptography changelog re: dependabot alerts: CVE-2023-23931; accepted Python buffer 
protocol objects, but allowed immutable buffers; squash-merged lots of PRs

Opthamologist appt.


Thu 9-Feb-2023
^^^^^^^^^^^^^^

Finished backfilling nowcast-agrif:
  upload_forcing orcinus-nowcast-agrif turbidity 2023-02-08
  wait for run to finish
  upload_forcing orcinus-nowcast-agrif turbidity 2023-02-09
(SalishSeaCast)

Continued migrating Susan's new rivers processing code into repo:
* branch: v202111-rivers
* PR#150
* updated make_readme.py
* added title and description to ProductionDailyRiverNCfile.ipynb
* debugged corrupted ERDDAP_datasets.ipynb notebook
* dropped multiple runoff forcing filename templates
* dropped unused imports
* dug into multiple instances of:
    /media/doug/warehouse/MEOPAR/SalishSeaNowcast/nowcast/daily_river_flows.py:122: ParserWarning: Length of header or names does not match length of data. This leads to a loss of data with index_col=False.
      river_flow = pd.read_csv(
  nothing made sense until I found https://github.com/pandas-dev/pandas/issues/49279 bug report
  which says that ``on_bad_lines`` is being ignored because we have ``index_col=False`` and the 
  overlength lines are being ignored
(SalishSeaNowcast)

MCL estate work:
* signed forms to get CRA funds moved from estate to e-premium acct


Fri 10-Feb-2023
^^^^^^^^^^^^^^^

Continued migrating Susan's new rivers processing code into repo:
* branch: v202111-rivers
* PR#150
* dug deeper into multiple instances of:
    /media/doug/warehouse/MEOPAR/SalishSeaNowcast/nowcast/daily_river_flows.py:122: ParserWarning: Length of header or names does not match length of data. This leads to a loss of data with index_col=False.
      river_flow = pd.read_csv(
  re: https://github.com/pandas-dev/pandas/issues/49279 bug report
  found that all lines are being processed as we want; ParserWarning seems to be extraneous
* refactored river flow .csv reading using functools.partial()
* added warnings.catch_warnings() context managers to suppress ParserWarnings; created issue #154
* refactored transformation of dataframe from .csv to 2-column dataframe with date as indes
* added unit test module for daily_river_flows.py
(SalishSeaNowcast)


Sat 11-Feb-2023
^^^^^^^^^^^^^^^

Drove to White Rock for MA memorial gathering.


Sun 12-Feb-2023
^^^^^^^^^^^^^^^

Drove to White Rock for MA family lunch.

Continued migrating Susan's new rivers processing code into repo:
* branch: v202111-rivers
* PR#150
* added unit tests for read_river()
* started work on unit tests for read_river_Theodosia()
(SalishSeaNowcast)


Week 7
------

Mon 13-Feb-2023
^^^^^^^^^^^^^^^

download_live_ocean timed out at 10:24; re-ran manually at 10:45
(SalishSeaCast)

Continued migrating Susan's new rivers processing code into repo:
* branch: v202111-rivers
* PR#150
* continued work on unit tests for read_river_Theodosia()
(SalishSeaNowcast)

Did jan23 day & month avg files using ``nowcast.workers.day_month_avgs.py`` module.
(Hindcast)

Finished and sent reference letter for Ben's LANL postdoc.

Phys ocgy seminar: Kate Schuler; in-progress CH4 measurements in the Arctic.


Tue 14-Feb-2023
^^^^^^^^^^^^^^^

Ruff: Faster Python Linting With Rust
Charlie Marsh
Staff Software Engineer at Spring Discovery
* recent Talk Python podcast
* recent PyCharm blog post
* fast linter & fixer
* rust niches
  * performance
  * interop w/ Python is really good
    * PyO3 ecosystem
    * Rust crates can be published to PyPI
* Ruff is on conda-forge
* replaces "Flake8 (plus a variety of plugins), isort, pydocstyle, yesqa, 
  and even a subset of pyupgrade and autoflake" (from conda-frge description)
* embedded docs in ruff; e.g.
    ``ruff rule F541``
* autofix capability:
    ``ruff --fix ...``
    * *caution* can break code; code transformation is a hard problem
* can be configured in ``pyproject.toml``
* number of violations of each rule
    ``ruff --statistics``
* can add ``# nopqa`` comments to silence notifications to get to clean state
    ``ruff --add-noqa``
* no plugin support at present due to early state and not ready to define public API
* discussion of rust-python; ruff uses r-p's AST parser
* ruff is designed to be used along-side black
* building an auto-formatter integrated into ruff
* PyCharm plugin: called Ruff, community built, in marketplace
* design intent is that ruff is to be used a la carte
  * pick and choose sub-linters
  * ``ruff linters`` shows sub-linters and their rule prefixes
* **pyupgrade <-- investigate** by Anthony Sottle> of pre-commit
* "fearless parallelization" in rust
* avoid allocation in rust for performance
* **ruff doesn't support structural pattern matching**
* works with pre-commit

Group mtg; see whiteboard
* Birgit reported in Paul's attendence at DRAKKAR mtg:
  * 3.6 -> 4.0 20-30% faster
  * 4.0 -> 4.2 20-30% faster again
  * working on AGRIF sub-grids w/ sigma coords in z coord grid
(MOAD)

Continued migrating Susan's new rivers processing code into repo:
* branch: v202111-rivers
* PR#150
* finished unit tests & refactoring of _read_river_Theodosia()
* started unit tests & refactoring of _do_a_pair()
* started unit tests & refactoring of _patch_gaps()
* started unit tests & refactoring of _patch_fitting()
(SalishSeaNowcast)

Squash-merged dependabot PRs re: ipython CVE-2023-24816 re: command injection on Windows.


Wed 15-Feb-2023
^^^^^^^^^^^^^^^

Continued migrating Susan's new rivers processing code into repo:
* branch: v202111-rivers
* PR#150
* finished unit tests & refactoring of _read_river_Theodosia()
* finished unit tests & refactoring of _patch_fitting()
(SalishSeaNowcast)

Rode to ESB for hearing test.


Thu 16-Feb-2023
^^^^^^^^^^^^^^^

Set up 2023 bloomcast:
* khawla:
  * updated SOG-Bloomcast-Ensemble clone
  * updated SOG clone
  * changed SOG default branch name from master to main
  * added branch protection rule for main on GitHub
  * created new bloomcast env (Python 3.11)
  * did editable installs of SOG & SOG-Bloomcast-Ensemble
  * SOG-Bloomcast-Ensemble test suite ran successfully
  * mkdir run/2021
  * cp run/2022_bloomcast_inifile.yaml run/2023_bloomcast_infile.yaml
  * mv run/2022_bloomcast_inifile.yaml run/2022/
  * committed archive of 2022 SOG YAML infile
  * edit run/2023_bloomcast_infile.yaml
  * edit run/config/yaml
    * change back to Englishman River at Parksville from Nanaimo River at Cassidy 
      because the Englishman data stream resumed on 30-Apr-2021
    * added ``scale_factor: 1`` for Englishman River
  * successfully tested run prep w/ SOG runs and publish to web disabled
  * committed run/2023_bloomcast_infile.yaml and run/config.yaml
Jared at NAFC reported that SOG command processor works with colander=1.8.3:
* built env on salish w/ colander<2 from conda-forge; got Python 3.11
* salish:
  * updated SOG-Bloomcast-Ensemble clone
  * noted that SOG clone is a Mercurial repo
    * replaced w/ git clone from GitHub
  * created new bloomcast env: Python 3.11, colander 1.8.3
  * did editable installs of SOG & SOG-Bloomcast-Ensemble
  * runs dir: /data/dlatorne/SOG-projects/SOG-Bloomcast-Ensemble/run
  * archived 2021_bloomcast* files in run/2021/
  * archived Englishman_flow Fraser_flow Sandheads_wind in run/2021/
  * archived YVR_* in run/2021/
  * ran test w/ push to web disabled
    * failed with:
        Invalid SOG YAML in 2023_bloomcast_infile.yaml. The following parameters are missing or misspelled:
        {'physics.fresh_water.river_CO2_chemistry': 'Required'}
    * suspect Ben's commits since Susan's 55af3c2 on 7-Apr-2014
  * git switch 55af3c2
  * re-ran test w/ push to web disabled
      INFO [bloomcast.ensemble] Predicted earliest bloom date is 2023-03-14
      INFO [bloomcast.ensemble] Earliest bloom date is based on forcing from 2004/2005
      INFO [bloomcast.ensemble] Predicted early bound bloom date is 2023-03-14
      INFO [bloomcast.ensemble] Early bound bloom date is based on forcing from 2004/2005
      INFO [bloomcast.ensemble] Predicted median bloom date is 2023-03-23
      INFO [bloomcast.ensemble] Median bloom date is based on forcing from 2003/2004
      INFO [bloomcast.ensemble] Predicted late bound bloom date is 2023-04-09
      INFO [bloomcast.ensemble] Late bound bloom date is based on forcing from 1987/1988
      INFO [bloomcast.ensemble] Predicted latest bloom date is 2023-04-14
      INFO [bloomcast.ensemble] Latest bloom date is based on forcing from 1998/1999
  * enabled cron job
Added new unrecognized weather descriptions to cloud fraction mapping.
(Bloomcast)

Project mtg w/ Javier.
Helped Raisha with tyee connection failure; suspect fail2ban
(Atlantis)


Fri 17-Feb-2023
^^^^^^^^^^^^^^^

Updated sphinx-rtd-theme pin to 1.2 re: its release; 
rely on that pin to ensure compatible versions of the rest of the Sphinx tool chain.
* Reshapr
* salishsea-site
* NEMO_Nowcast


Pin sphinx-rtd-theme=1.2

Sphinx=6 and docutils=0.18 are now supported.
We're relying on the sphinx-rtd-theme version pin to ensure compatible versions 
of the rest of the Sphinx tool chain.


Updated prod env to use sentry-sdk=1.15.0.
(salishsea-site)

Updated prod env to use sentry-sdk=1.15.0.
(SalishSeaCast)

Continued migrating Susan's new rivers processing code into repo:
* branch: v202111-rivers
* PR#150
* finished unit tests & refactoring of _patch_missing_obs(); renamed from patch_gaps()
* started unit tests & refactoring of _do_a_pair()

Code analysis errors & warnings for 
/media/doug/warehouse/MEOPAR/SalishSeaNowcast/nowcast/daily_river_flows.py
  Warning:(261, 13) Statement seems to have no effect
  Error:(261, 13) Unresolved reference 'stop'
  Warning:(278, 20) Local variable 'primary_flow' might be referenced before assignment
(SalishSeaNowcast)


Sat 18-Feb-2023
^^^^^^^^^^^^^^^

``download_results nowcast`` and ``make_forcing_links ssh`` failed with ssh auth problems
(but ``make_fvcom_boundary x2 nowcast`` worked); so, apparently a transient issue
* recovery started at ~09:30:
    make_forcing_links arbutus ssh
    download_results arbutus nowcast
(SalishSeaCast)

Drove to White Rock to visit J.


Sun 19-Feb-2023
^^^^^^^^^^^^^^^

Continued migrating Susan's new rivers processing code into repo:
* branch: v202111-rivers
* PR#150
* continnued unit tests & refactoring of _do_a_pair()
(SalishSeaNowcast)


Week 8
------

Mon 20-Feb-2023
^^^^^^^^^^^^^^^

download_live_ocean was ~1h late.
``upload_fvcom_atmos_forcing arbutus r12 nowcast`` failed reading SSH protocol banner;
worked on manual re-run; so, another transient
(SalishSeaCast)

Continued migrating Susan's new rivers processing code into repo:
* branch: v202111-rivers
* PR#150
* finished unit tests & refactoring of _do_a_pair()
* finished unit tests & refactoring of _do_fraser()
* finished unit test & refactoring of _calc_watershed_flows()
(SalishSeaNowcast)


Tue 21-Feb-2023
^^^^^^^^^^^^^^^

Worked at ESB while Rita was at home.

Weekly group mtg; see whiteboard.
(MOAD)

Finished reading draft of Susan's flux paper.

Continued migrating Susan's new rivers processing code into repo:
* branch: v202111-rivers
* PR#150
* finished refactoring of _get_area()
* started unit test & refactoring of _create_runoff_array()
(SalishSeaNowcast)


Wed 22-Feb-2023
^^^^^^^^^^^^^^^

collect_river_data for ECCC rivers failed with:
  UnicodeDecodeError: 'utf-8' codec can't decode byte 0xe9 in position 81: invalid continuation byte
* investigation:
  * accented character in position 81 is the problem:
      ``...Discharge / Débit (cms)...``
  * issue resolved by changing pandas.read_csv() from default utf-8 encosing to old iso-8859-1 
    (Western European) encoding; suspect config control bug at ECCC
* recover started at ~09:00:
  * hacked collect_river_data worker on skookum to add ``encoding="iso-8859-1"``
  * updated /SalishSeaCast/datamart/hydrometric/collect_river_date.sh to include Roberts Creek and 
    ECCC arg to collect_river_data, then ran it
  * restarted automation:
      upload_forcing arbutus forecast2
      upload_forcing orcinuns forecast2
      upload_forcing optimum forecast2
      upload_forcing graham-dtn forecast2
      wait for forecast2 runs to finish
      upload_forcing arbutus nowcast+
      upload_forcing orcinuns nowcast+
      upload_forcing optimum nowcast+
      upload_forcing graham-dtn nowcast+
(SalishSeaCast)

Reverted accidental main branch commit of daily_river_flows.py that was causing merge conflict
for v202111-rivers branch.
Continued migrating Susan's new rivers processing code into repo:
* branch: v202111-rivers
* PR#150
* finished unit test & refactoring of _create_runoff_array()
(SalishSeaNowcast)


Thu 23-Feb-2023
^^^^^^^^^^^^^^^

download_weather 18 2.5km didn't finish and I didn't notice until this morning
* investigation:
  * /results/forcing/atmospheric/GEM2.5/GRIB/20230222/18/ dir created, but no files downloaded
  * no 18/ dir or files on hpfx
  * HRDPS west was part of polar stereographic product that was discontinued on 22feb
* salvage:
    download_weather 12 1km --yesterday
    /SalishSeaCast/datamart/hydrometric/collect_river_date.sh 2023-02-22
    collect_NeahBay_ssh 00  # necessary for continuity???
    get_onc_ctd SCVIP  # backfillable
    get_onc_ctd SEVIP  # backfillable
    collect_NeahBay_ssh 06
    download_live_ocean
    collect_river_data USGS SkagitMountVernon 2023-02-22
    collect_river_data USGS SnohomishMonroe 2023-02-22
    collect_river_data USGS NisquallyMcKenna 2023-02-22
    collect_river_data USGS GreenwaterGreenwater 2023-02-22
    download_weather 00 1km 
    wait for 10:45
    download_weather 12 1km 
* created /results/forcing/rivers/observations/collect_river_data.sh to do USGS rivers
* mapping of west variable names to continental:
    UGRD_TGL_10: UGRD_AGL_10m  1.8M
    VGRD_TGL_10: VGRD_AGL_10m  1.7M
    DSWRF_SFC_0: DSWRF_Sfc  198: 959K
    DLWRF_SFC_0: DLWRF_Sfc  119K: 2.1M
    LHTFL_SFC_0: LHTFL_Sfc  82K: 1.2M
    TMP_TGL_2: TMP_AGL_2m  3.1M
    SPFH_TGL_2: SPFH_AGL_2m  187: 2.6M
    RH_TGL_2: RH_AGL_2m  113K: 2.2M
    APCP_SFC_0: APCP_Sfc  136K: 2.0M
    PRATE_SFC_0: PRATE_Sfc 54K: 361K
    PRMSL_MSL_0: PRMSL_MSL  148K: 743K
    TCDC_SFC_0: TCDC_Sfc 51K: 2.3M  # necessary? used to parametrize radiation missing from GEMLAM
* present size is 89M per forecast, 356M per day
* continental is 1.2G per forecast, 4.7G per day
* started downloading as much 2023 continental as possible:
  * each forecast takes ~15min to download
  * 03jan-14jan
* future daily grind, after 10:45, yyyy-mm-dd is previous day:
    /SalishSeaCast/datamart/hydrometric/collect_river_data.sh yyyy-mm-dd
    /results/forcing/rivers/observations/collect_river_data.sh yyyy-mm-dd
    get_onc_ctd SCVIP  # backfillable
    get_onc_ctd SEVIP  # backfillable
    get_vfpa_hadcp yyyy-mm-dd
    collect_NeahBay_ssh 06
    download_live_ocean
    download_weather 00 1km 
    download_weather 12 1km 
* Python packages for handling GRIB files:
  * cfgrib: https://github.com/ecmwf/cfgrib
    * "enables the engine='cfgrib' option to read GRIB files with xarray"
  * pynio: https://github.com/NCAR/pynio **unmaintained**
(SalishSeaCast)

Squash-merged dependabot PR re: CVE-2023-26302 re: command-line DoS in markdown-it-py.
(Reshapr)

Changed weather config to use HRDPS 2.5km continental product
branch: hrdps-continental
PR#156
(SalishSeaNowcast)

Experimented with cfgrib:
* ``mamba create -n cfgrib-test python=3.11 xarray cfgrib netcdf4 jupyterlab``
* ``xarray.open_dataset(path, engine="cfgrib")`` works, but data variable name is sometimes     
  ``unknown``


Fri 24-Feb-2023
^^^^^^^^^^^^^^^

Continued work on changes to use HRDPS 2.5km continental product
branch: hrdps-continental
PR#156
* replaced download_weather --yesterday w/ --run-date
* updated worker failure docs re: broken links and outdated content
* started work on replacing @patch with monkeypathc in download_weather
* started work on updating grb_to_netcdf
  * updated sub-region and Sand Heads indices with values that Susan found in contineental domain
  * stalled out on step of getting grid defintion via grid_defn.pl and wgrib2
    * Susan found updated tools: pywgrib2_s
(SalishSeaNowcast)

Continued downloading as much 2023 continental as possible:
  * 15jan-31jan
Did manual tasks that automation isn't doing due to change to HRDPS continental product:
  nemo_nowcast.workers.clear_checklist
  /SalishSeaCast/datamart/hydrometric/collect_river_data.sh yyyy-mm-dd
  /results/forcing/rivers/observations/collect_river_data.sh yyyy-mm-dd
  get_onc_ctd SCVIP  # backfillable
  get_onc_ctd SEVIP  # backfillable
  get_vfpa_hadcp yyyy-mm-dd
  collect_NeahBay_ssh 06
  download_live_ocean
  download_weather 00 1km 
  download_weather 12 1km 
Created /SalishSeaCast/daily_grind.sh to automate the above tasks.
(SalishSeaCast)


Sat 25-Feb-2023
^^^^^^^^^^^^^^^

Continued downloading as much 2023 continental as possible:
* 01feb-21feb
Did manual tasks that automation isn't doing due to change to HRDPS continental product by running
  bash /SalishSeaCast/daily_grind.sh
(SalishSeaCast)

Rode 50km Muckle Yin fondo on Zwift.


Sun 26-Feb-2023
^^^^^^^^^^^^^^^

Continued downloading as much 2023 continental as possible:
* 22feb stalled on missing files:
   ``00/002/20230222T00Z_MSC_HRDPS_SPFH_AGL-2m_RLatLon0.0225_PT002H.grib``
   ``06/001/20230222T06Z_MSC_HRDPS_RH_AGL-2m_RLatLon0.0225_PT001H.grib2``
Added previous day's ``download_weather * 2.5km`` to /SalishSeaCast/daily_grind.sh
Did manual tasks that automation isn't doing due to change to HRDPS continental product by running
  bash /SalishSeaCast/daily_grind.sh
(SalishSeaCast)

Continued work on changes to use HRDPS 2.5km continental product
branch: hrdps-continental
PR#156
* did unit tests & refactoring in grib_to_netcdf up to the first of the wgrib2 subprocess calls
* tried to use pwgrib2_xr but it fails with:
    ImportError: cannot import name 'dask_array_type' from 'xarray.core.pycompat' (/home/doug/conda_envs/pywgrib2-test/lib/python3.9/site-packages/xarray/core/pycompat.py)
  suspect that xarray/dask have evolved since last pwgrib2_xr release on 23-Mar-2021
  * dask was then at 2021.03.0
  * xarray was then at 0.17.0
  Also, pwgrib2_xr supports only Python 3.9
* found wgrib2 up to 2.0.5 through 3.1.1 packages on conda-forge
(SalishSeaNowcast)


Week 9
------

Mon 27-Feb-2023
^^^^^^^^^^^^^^^

Continued work on changes to use HRDPS 2.5km continental product
branch: hrdps-continental
PR#156
* installed wgrib2 3.1.1 from conda-forge in wgrib2-test env on khawla
* successfully ran ``wgrib2 grib-file -append -grib uv.grib`` to create u-v winds file
* read grid_defn.pl and learned that it parses the output of ``wgrib2 -d 1 -grid grib-file``
* ran that for 
    ``continental2.5/GRIB/20230225/00/001/20230225T00Z_MSC_HRDPS_UGRD_AGL-10m_RLatLon0.0225_PT001H.grib2``
  and got:
    1:0:grid_template=1:winds(grid):
      rotated lat-lon grid:(2540 x 1290) units 1e-06 input WE:SN output WE:SN res 56
      lat -12.302501 to 16.700001 by 0.022500
      lon 345.178780 to 42.306283 by 0.022500 #points=3276600
      south pole lat=-36.088520 lon=245.305142 angle of rot=0.000000
* https://www.cpc.ncep.noaa.gov/products/wesley/wgrib2/new_grid.html shows that grid description
  for ``wgrib2 uv.grib -new_grid_winds earth -new_grid grid-desc uvrot.grib`` that we want is:
    rot-ll:sp_lon:sp_lat:sp_rot lon0:nlon:dlon lat0:nlat:dlat
  I think that translates to:
    rot-ll:245.305142:-36.088520:0.000000 lon0:2540:0.022500 lat0:1290:0.022500
* tried 
    ``wgrib2 uv.grib -new_grid_winds earth -new_grid rot-ll:245.305142:-36.088520:0.000000 345.178780:2540:0.022500 -12.302501:1290:0.022500 uvrot.grib``
  and got (not unexpectedly):
    IPOLATES package is not installed
* built a new pywgrib2-test env with:
    mamba create -n pywgrib2-test -c conda-forge -c yt87 \
      python=3.9 dask=2021.03.0 xarray=0.17.0 libwgrib2 pywgrib2_xr matplotlib cartopy jupyterlab
  * successfully did:
    * u-v append 
    * query of grid description
    * rotation to earth-referenced NS grid
  * created analysis-doug/notebooks/pywgrib2-grib_to_netcdf.ipynb to properly record exploration
* author of pywgrib2_xr package listed in metadata is George Trojan who is also listed as an 
  author of wgrib2
(SalishSeaNowcast)

Did manual tasks that automation isn't doing due to change to HRDPS continental product by running
  bash /SalishSeaCast/daily_grind.sh
(SalishSeaCast)


Tue 28-Feb-2023
^^^^^^^^^^^^^^^

Continued work on changes to use HRDPS 2.5km continental product
branch: hrdps-continental
PR#156
* built pywgrib2-no-dask-pin with
    mamba create -n pywgrib2-no-dask-pin -c conda-forge -c yt87 \
      python=3.9 dask xarray=0.17.0 libwgrib2 pywgrib2_xr
  * pywgrib2 works
* built pywgrib2-xarray-0.18 with
    mamba create -n pywgrib2-xarray-0.18 -c conda-forge -c yt87 \
      python=3.9 dask xarray=0.18.0 libwgrib2 pywgrib2_xr
  * pywgrib2 works
* built pywgrib2-xarray-0.19 with
    mamba create -n pywgrib2-xarray-0.19 -c conda-forge -c yt87 \
      python=3.9 dask xarray=0.19.0 libwgrib2 pywgrib2_xr
  * pywgrib2 works
* built pywgrib2-xarray-0.20 with
    mamba create -n pywgrib2-xarray-0.20 -c conda-forge -c yt87 \
      python=3.9 dask xarray=0.20.0 libwgrib2 pywgrib2_xr
  * pywgrib2 works
* built pywgrib2-xarray-0.21 with
    mamba create -n pywgrib2-xarray-0.21 -c conda-forge -c yt87 \
      python=3.9 dask xarray=0.21.0 libwgrib2 pywgrib2_xr
  * pywgrib2 works
* built pywgrib2-xarray-2022.03 with
    mamba create -n pywgrib2-xarray-2022.03 -c conda-forge -c yt87 \
      python=3.9 dask xarray=2022.03.0 libwgrib2 pywgrib2_xr
  * pywgrib2 works
* built pywgrib2-xarray-2022.06 with
    mamba create -n pywgrib2-xarray-2022.06 -c conda-forge -c yt87 \
      python=3.9 dask xarray=2022.06.0 libwgrib2 pywgrib2_xr
  * pywgrib2 works
* built pywgrib2-xarray-2022.09 with
    mamba create -n pywgrib2-xarray-2022.09 -c conda-forge -c yt87 \
      python=3.9 dask xarray=2022.09.0 libwgrib2 pywgrib2_xr
  * pywgrib2 works
* built pywgrib2-xarray-2022.10 with
    mamba create -n pywgrib2-xarray-2022.10 -c conda-forge -c yt87 \
      python=3.9 dask xarray=2022.10.0 libwgrib2 pywgrib2_xr
  * pywgrib2 works
* built pywgrib2-xarray-2022.11 with
    mamba create -n pywgrib2-xarray-2022.11 -c conda-forge -c yt87 \
      python=3.9 dask xarray=2022.11.0 libwgrib2 pywgrib2_xr
  * pywgrib2 fails with:
      Traceback (most recent call last):
        File "/home/doug/conda_envs/pywgrib2-xarray-2022.11/bin/pywgrib2", line 33, in <module>
          sys.exit(load_entry_point('pywgrib2_xr==0.2.3', 'console_scripts', 'pywgrib2')())
        File "/home/doug/conda_envs/pywgrib2-xarray-2022.11/bin/pywgrib2", line 25, in importlib_load_entry_point
          return next(matches).load()
        File "/home/doug/conda_envs/pywgrib2-xarray-2022.11/lib/python3.9/importlib/metadata.py", line 86, in load
          module = import_module(match.group('module'))
        File "/home/doug/conda_envs/pywgrib2-xarray-2022.11/lib/python3.9/importlib/__init__.py", line 127, in import_module
          return _bootstrap._gcd_import(name[level:], package, level)
        File "<frozen importlib._bootstrap>", line 1030, in _gcd_import
        File "<frozen importlib._bootstrap>", line 1007, in _find_and_load
        File "<frozen importlib._bootstrap>", line 972, in _find_and_load_unlocked
        File "<frozen importlib._bootstrap>", line 228, in _call_with_frames_removed
        File "<frozen importlib._bootstrap>", line 1030, in _gcd_import
        File "<frozen importlib._bootstrap>", line 1007, in _find_and_load
        File "<frozen importlib._bootstrap>", line 986, in _find_and_load_unlocked
        File "<frozen importlib._bootstrap>", line 680, in _load_unlocked
        File "<frozen importlib._bootstrap_external>", line 850, in exec_module
        File "<frozen importlib._bootstrap>", line 228, in _call_with_frames_removed
        File "/home/doug/conda_envs/pywgrib2-xarray-2022.11/lib/python3.9/site-packages/pywgrib2_xr/__init__.py", line 30, in <module>
          from .accessor import Wgrib2DatasetAccessor
        File "/home/doug/conda_envs/pywgrib2-xarray-2022.11/lib/python3.9/site-packages/pywgrib2_xr/accessor.py", line 9, in <module>
          from xarray.core.pycompat import dask_array_type
      ImportError: cannot import name 'dask_array_type' from 'xarray.core.pycompat' (/home/doug/conda_envs/pywgrib2-xarray-2022.11/lib/python3.9/site-packages/xarray/core/pycompat.py)
  * it appears that the way to resolve the ImportError is:
      from xarray.core.pycompat import array_type
      ...
      dask_array_type = array_type("dask")
    posted this to xarray GitHub discussion and got confirmation that xarray.core.pycompat is a
    private API
* built pywgrib2-py310 with
    mamba create -n pywgrib2-py310 -c conda-forge -c yt87 \
      python=3.9 dask xarray=2022.11.0 libwgrib2
  * to confirm that libwgrib2 will install in Python 3.10 env
* added matplotlib cartopy jupyterlab to pywgrib2-xarray-2022.10 env for continuing work in notebook
* discovered ``winds="earth"`` arg for ``ds.wgrib2.grid()`` that is the equivalent of the wgrib2
  ``-now_grid_winds earth`` option
* Susan confirmed that rotated winds netCDF file created via pywgrib2_xr xarray interface is 
  consistent with 15feb23 HRDPS west vectors

Did manual tasks that automation isn't doing due to change to HRDPS continental product by running
  bash /SalishSeaCast/daily_grind.sh
(SalishSeaCast)


March
=====

Wed 1-Mar-2023
^^^^^^^^^^^^^^

Did manual tasks that automation isn't doing due to change to HRDPS continental product by running
  bash /SalishSeaCast/daily_grind.sh
(SalishSeaCast)

Continued work on changes to use HRDPS 2.5km continental product
branch: hrdps-continental
PR#156
* forked yt87/pywgrib2_xr to SalishSeaCast/pywgrib2_xr
* added dev env description for as-forked version that requires xarray<2022.11
  * successfully ran test suite with warnings
* thrashed on building Python 3.10 env due to version issues among netcdf4 hdf5 and libwgrib2
* hacked on clone of yt87/libwgrib2:
  * eventually figured out that it needs to use jasper<3 due to undefined symbol jpc_decode
    see: https://github.com/NOAA-EMC/NCEPLIBS-wgrib2/issues/53
  * changed recipe/meta.yaml to pin jasper<3
  * env for build
      mamba create -n libwgrib2-dev make gfortran libnetcdf libaec libpng \
        "jasper<3" _openmp_mutex conda-build
  * ``conda-build recipe`` builds libwgrib2.so.3.0.0 but conda-build test step fails to build env
  * dropped ``libwgrib2`` from pywgrib2_xr-dev env to avoid hdf5/netcdf version issues
  * added ``jasper<3`` to env
  * copied libwgrib2.so.3.0.0 and symlinks to pywgrib2_xr-dev/lib/
      cp -P /tmp/conda-builds/libwgrib2_1677718742087/work_moved_libwgrib2-3.0.0-hdee5e95_2_linux-64/lib/libwgrib2.so* /home/doug/conda_envs/pywgrib2_xr-dev/lib/


Thu 2-Mar-2023
^^^^^^^^^^^^^^

Did manual tasks that automation isn't doing due to change to HRDPS continental product by running
  bash /SalishSeaCast/daily_grind.sh
(SalishSeaCast)

Continued work on changes to use HRDPS 2.5km continental product
branch: hrdps-continental
PR#156
* added dependencies for pywgrib2_xr to dev env
* copied libwgrib2 into dev env lib/
* refactored grib_to_netcdf._rotate_grib_wind() to use pywgrib2_xr
  * have to be really careful about all args to pywgrib2_xr.wgrib() being strings
    and calling pywgrib2_xr.free_files() to close files


Fri 3-Mar-2023
^^^^^^^^^^^^^^

Continued work on changes to use HRDPS 2.5km continental product
branch: hrdps-continental
PR#156
* SalishSeaNowcast GHA pytest-with-coverage workflow failing with: 
    In file included from pywgrib2_xr/_wgrib2.c:795:
    pywgrib2_xr/pywgrib2.h:3:10: fatal error: wgrib2/wgrib2.h: No such file or directory
        3 | #include "wgrib2/wgrib2.h"
          |          ^~~~~~~~~~~~~~~~~
    compilation terminated.
  broke build chain on khawla while trying to diagnose; I think because I deleted 
    pywgrib2_xr/pywgrib2_xr/_wgrib2.cpython-310-x86_64-linux-gnu.so
  recovery:
  * got a successful build in libwgrib2 fork:
      /tmp/conda-builds/linux-64/libwgrib2-3.0.0-hdee5e95_2.tar.bz2
  * installed that tarball into pywgrib2_xr-dev:
      conda install /tmp/conda-builds/linux-64/libwgrib2-3.0.0-hdee5e95_2.tar.bz2
  * did editable install of pywgrib2_xr:
      python3 -m pip install -e .
* added pywgrib2_xr/_vendor/libwgrib2-3.0.0-hdee5e95_2.tar.bz2
* updated SalishSeaNowcast pytest-with-coverage workflow to install vendored libwgrib2
* dropped GRIB2 file existence & 0 length checks
* factored out pywgrib2_xr.wgrib() calls
* refactored _collect_grib_scalars() without remapping
* refactored _concat_hourly_gribs()
* refactored _crop_to_watersheds()
* restored remapping of scalars because conversion to netcdf complained about different grid type
  for scalars and winds
* got stopped by netcdf conversion not supporting rotated lat-lon grid
(SalishSeaNowcast)

Did manual tasks that automation isn't doing due to change to HRDPS continental product by running
  bash /SalishSeaCast/daily_grind.sh
(SalishSeaCast)


Sat 4-Mar-2023
^^^^^^^^^^^^^^

Drove to White Rock to visit J.

Did manual tasks that automation isn't doing due to change to HRDPS continental product by running
  bash /SalishSeaCast/daily_grind.sh
* 00, 06, & 12 downloads for 2023-03-03 all failed due to missing 001/UGRD files
* ran download_weather for today: 00 06
* hacked next_workers to temporarily leave out grib_to_netcdf
* created sarracenia/hrdps-continental-hpfx.conf
* changed config/supervisord.ini to use sarracenia/hrdps-continental-hpfx.conf
* test on skookum:
  * copied sarracenia/hrdps-continental-hpfx.conf and config/supervisord.ini 
  * shutdown and relaunched supervisord
  * confirmed that hrdps-continental-hpfx queue was attached
(SalishSeaCast)

Continued work on changes to use HRDPS 2.5km continental product
branch: hrdps-continental
PR#156
* changed next_workers module to temporarily exclude grib_to_netcdf so that automation with
  collect_weather worker can be started to that we know about failures like 03mar in more timely
  manner to communicate to Sandrine
(SalishSeaNowcast)


Sun 5-Mar-2023
^^^^^^^^^^^^^^

Did manual tasks that automation isn't doing due to change to HRDPS continental product by running
  bash /SalishSeaCast/daily_grind.sh
(SalishSeaCast)

Continued work on changes to use HRDPS 2.5km continental product
branch: hrdps-continental
PR#156
* sarracenia client for continental HRDPS is grabbing 2 extra WEonG variables:
  * WEonG_FZPRATE_Sfc and WEonG_PRATE_Sfc
  * updated sarracenia/hrdps-continental-hpfx.conf to reject those files
  * copied to skookum and restarted client to test
    * got expected 528 files in /SalishSeaCast/datamart/hrdps-continental/18
(SalishSeaNowcast)

Rode 50km Bambino fondo on Zwift.


Week 10
-------

Mon 6-Mar-2023
^^^^^^^^^^^^^^

Did manual tasks that automation isn't doing due to change to HRDPS continental product by running
  bash /SalishSeaCast/daily_grind.sh
Resumed automation with grib_to_netcdf disabled:
* deployed hrdps-continental branch to skookum
* restarted manager to load updated config
* started ``collect_weather 18 2.5km`` to test resumption of automation
  * failed; files were downloaded by sarracenia, but not moved
* used (forgotten) --backfill --backfill-date 2023-03-06 options to move files after the fact
* started modified ``collect_weather 00 2.5km`` for another test:
  * 
(SalishSeaCast)

Continued work on changes to use HRDPS 2.5km continental product
branch: hrdps-continental
PR#156
* tried to use pywgrib2_xr xarray interface to read processed grib files and write them to netcdf
  to work around wgrib2 -netcdf not working for rotated lat-lon grid
  * failed due to differing reference times in grib file
    * time_counter attrs in pre-continental ops_y2023m01d19.nc file:
        double time_counter(time_counter) ;
                time_counter:units = "seconds since 1970-01-01 00:00:00.0 0:00" ;
                time_counter:long_name = "verification time generated by wgrib2 function verftime()" ;
                time_counter:reference_time = 1674064800. ; // "2023-01-18 18"
                time_counter:reference_time_type = 0 ; // "1970-01-01"
                time_counter:reference_date = "2023.01.18 18:00:00 UTC" ;
                time_counter:reference_time_description = "kind of product unclear, reference date is variable, min found reference date is given" ;
                time_counter:time_step_setting = "auto" ;
                time_counter:time_step = 3600. ; // "1970-01-01 01"
                time_counter:time_origin = "1970-Jan-01 00:00:00" ;
                time_counter:_Storage = "chunked" ;
                time_counter:_ChunkSizes = 512 ;
                time_counter:_DeflateLevel = 4 ;
                time_counter:_Shuffle = "true" ;
                time_counter:_Endianness = "little" ;
  * hacked processing to use ``-set_date 2023011818`` and got a loadable grib file, but it is weird:
    * 14? time coordinates
    * not cropped to small grid?
    * 44 data variables (due to excess of time coords)
    * only 12 hours of U and V
* explored cfgrib in cfgrib-grib_to_netcdf env and notebook
    mamba create -n cfgrib-grib_to_netcdf python=3.10 xarray netcdf4 dask cfgrib matplotlib jupyterlab
  * created cfgrib-grib_to_netcdf.ipynb
  * learned about grib storing time in 2 coordinates ``time`` and ``step``
  * learned about preprocess arg to xarray.open_mfdataset(0)
* changed collect_weather file system watcher event from on_moved() to on_created()
  * uploaded to skookum for test on 00Z forecast; didn't work
(SalishSeaNowcast)


Tue 7-Mar-2023
^^^^^^^^^^^^^^

Worked at ESB while Rita was at home.

Group mtg; see whiteboard.
(MOAD)

Got suggestions from Becca and Jose re: gribs and contact with Tim Chui, their TA in Roland's
numerical weather forecasting course.
Continued work on cfgrib-grib_to_netcdf.ipynb:
* added narrative on yesterday's work
* created functions to build NEMO forcing comformant xarray dataset from a range of hours of a
  gribs forecast tree; i.e. 00Z 06Z, etc.
* email discussion w/ Tim Chui lead to Salem package; interesting, but not directly useful
* Susan came up with trigonometry to transform wind components to earth-referenced
(SalishSeaNowcast)

Did manual tasks that automation isn't doing due to change to HRDPS continental product by running
  collect_weather 00 2.5km --backfill --backfill-date 2023-03-07
  kill collect_weather 06
  collect_weather 06 2.5km --backfill --backfill-date 2023-03-07
  clear_checklist
  kill collect_weather 12
  collect_weather 12 2.5km --backfill --backfill-date 2023-03-07
  kill collect_weather 18
  collect_weather 18 2.5km --backfill --backfill-date 2023-03-07
(SalishSeaCast)

Picked up new computer glasses


Wed 8-Mar-2023
^^^^^^^^^^^^^^

Continued work on changes to use HRDPS 2.5km continental product
branch: hrdps-continental
PR#156
* reverted pywgrib2_xr from env
* started work on processing using cfgrib and xarray
* set linkcheck to ignore private FVCOM41 GitLab repo; all checks green again, finally
(SalishSeaNowcast)

Did manual tasks that automation isn't doing due to change to HRDPS continental product by running
  collect_weather 00 2.5km --backfill --backfill-date 2023-03-08
  kill collect_weather 06
  collect_weather 06 2.5km --backfill --backfill-date 2023-03-08
  clear_checklist
  kill collect_weather 12
  collect_weather 12 2.5km --backfill --backfill-date 2023-03-08
  kill collect_weather 18
  collect_weather 18 2.5km --backfill --backfill-date 2023-03-08
(SalishSeaCast)


Thu 9-Mar-2023
^^^^^^^^^^^^^^

Enabled pull request build for several projects on readthedocs.

Did manual tasks that automation isn't doing due to change to HRDPS continental product by running
  collect_weather 00 2.5km --backfill --backfill-date 2023-03-09
  kill collect_weather 06
  collect_weather 06 2.5km --backfill --backfill-date 2023-03-09
  clear_checklist
  kill collect_weather 12
  collect_weather 12 2.5km --backfill --backfill-date 2023-03-09
  kill collect_weather 18
  collect_weather 18 2.5km --backfill --backfill-date 2023-03-09
(SalishSeaCast)

Continued work on changes to use HRDPS 2.5km continental product
branch: hrdps-continental
PR#156
* changed forcing file name template from ``ops_`` to ``hrdsp_``
* added netCDF generation code for 24h forecast case; no deallocation or rotation yet
* started work on apportioning accumulation variables (deallocation)
(SalishSeaNowcast)


Fri 10-Mar-2023
^^^^^^^^^^^^^^^

Did manual tasks that automation isn't doing due to change to HRDPS continental product by running
  collect_weather 00 2.5km --backfill --backfill-date 2023-03-10
  collect_weather 06 2.5km --backfill --backfill-date 2023-03-10
  wait for post-collect_weather workers to finish
  clear_checklist
  collect_weather 12 2.5km --backfill --backfill-date 2023-03-10
  wait for 18Z forecast to download
  collect_weather 18 2.5km --backfill --backfill-date 2023-03-10
  pkill -f collect_weather
(SalishSeaCast)

Continued work on changes to use HRDPS 2.5km continental product
branch: hrdps-continental
PR#156
* finished work on apportioning accumulation variables (deallocation)
* factored out _update_checklist()
* added debug level messages
* improved nav_lon/nav_lat variables metadata by pulling more from lon/lat in grib files
* added _calc_grid_angle()
* added  _calc_earth_ref_winds()
(SalishSeaNowcast)

See work journal.
(Resilient-C)


Sat 11-Mar-2023
^^^^^^^^^^^^^^^

Update os pkgs on lizzy and rebooted.

Updated PyCharm on khawla to 2022.3.3.

Did manual tasks that automation isn't doing due to change to HRDPS continental product by running
  pkill -f collect_weather
  collect_weather 00 2.5km --backfill --backfill-date 2023-03-11
  collect_weather 06 2.5km --backfill --backfill-date 2023-03-11
  wait for post-collect_weather workers to finish
  clear_checklist
  collect_weather 12 2.5km --backfill --backfill-date 2023-03-11
  wait for 18Z forecast to download
  collect_weather 18 2.5km --backfill --backfill-date 2023-03-11
(SalishSeaCast)

Continued work on changes to use HRDPS 2.5km continental product
branch: hrdps-continental
PR#156
* fixed missing deg2rad() bug in _calc_earth_ref_winds()
* change longitude from grib's -180-180 to nemo's 0-360
* fixed missing division of apportioned variables by 60*60 s/hr
* started improving metadata
(SalishSeaNowcast)


Sun 12-Mar-2023
^^^^^^^^^^^^^^^

Clocks changed from PST to PDT.

Did manual tasks that automation isn't doing due to change to HRDPS continental product by running
  pkill -f collect_weather
  collect_weather 00 2.5km --backfill --backfill-date 2023-03-12
  collect_weather 06 2.5km --backfill --backfill-date 2023-03-12
  wait for post-collect_weather workers to finish
  clear_checklist
  collect_weather 12 2.5km --backfill --backfill-date 2023-03-12
  wait for 18Z forecast to download
  collect_weather 18 2.5km --backfill --backfill-date 2023-03-12
(SalishSeaCast)

Continued work on changes to use HRDPS 2.5km continental product
branch: hrdps-continental
PR#156
* finished improving metadata
* refactored dataset prep into _calc_nemo_ds()
* added handling for 2 different cases for offset step in _apportion_accumulation_vars()
* Susan confirmed that hrdps_y2023m02d15.nc file from new code compares well with that from old code
* added generation of `hrdps_` file for nowcast day for ``grib_to_netcdf nowcast+``
(SalishSeaNowcast)


Week 11
-------

Mon 13-Mar-2023
^^^^^^^^^^^^^^^

Did manual tasks that automation isn't doing due to change to HRDPS continental product by running
  pkill -f collect_weather
  collect_weather 00 2.5km --backfill --backfill-date 2023-03-13
  collect_weather 06 2.5km --backfill --backfill-date 2023-03-13
  wait for post-collect_weather workers to finish
  clear_checklist
  collect_weather 12 2.5km --backfill --backfill-date 2023-03-13
  wait for 18Z forecast to download
  collect_weather 18 2.5km --backfill --backfill-date 2023-03-13
Hacked download_weather and NEMO_Nowcast.nemo_nowcast.worker to skip missing files so that I could 
download what of HRDPS continental is available for:
* 20230222/00
  * got 479 of 528 files
* 20230222/06
  * got 464 of 528 files
* confirmed expected number of contineental2.5 GRIB files:
  * 03-31 jan all good
  * feb:
    * 14-16 feb have too many files
    * 22-feb has missing files
      * 20230222/00
        * got 479 of 528 files
      * 20230222/06
        * got 464 of 528 files
      12 and 18 are good
    * 23 feb have too many files
  * mar:
    * good except...
    * 03 has missing files
      * ran hacked download_weather 00
        * 186 of 528 files
      * ran hacked download_weather 06
        * 41 of 528 files
      * ran hacked download_weather 12
        * 343 of 528 files
Reverted download_weather and NEMO_Nowcast.nemo_nowcast.worker hacks.
Deployed hrdps-continental branch to skookum to test:
* stopped manager, message_broker & log_aggregator
* updated conda env
* started manager, message_broker & log_aggregator
* 1st test:
    grib_to_netcdf nowcast+ 2023-02-24
  * had to kill ERDDAP to prevent 16G memory blowout during nowcast 24 processing
  * memory continued to rise and swapping started during forecast day 1 processing; 
    killed grib_to_netcdf
* 2nd test:
  * added salish logging port 5562 config for grib_to_netcdf
  * restarted log_aggregator
      launch_remote_worker salish-nowcast grib_to_netcdf "nowcast+ --run-date 2023-02-24 --debug"
  * hrdps_y2023m02d24.nc took 16 minutes and >22G of memory
  * memory footprint continnued to grow for fcst/hrdps_y2023m02d25.nc
  * fcst/hrdps_y2023m02d25.nc took 22 minutes and >36G of memory
  * fcst/hrdps_y2023m02d26.nc took 10 minutes and >42G of memory
* 3rd test:
  * added nemo_ds*.close() calls in hopes of freeing memory
      launch_remote_worker salish-nowcast grib_to_netcdf "nowcast+ --run-date 2023-02-25 --debug"
  * hrdps_y2023m02d25.nc took 19 minutes and 22.136G of memory
  * no memory freed by nemo_ds*.close() calls :-(
  * killed
4th test:
  * added 
      dask_client = dask.distributed.Client("tcp://142.103.36.12:4386") 
      ... 
      dask_client.close()
    to use persistent cluster on salish
      launch_remote_worker salish-nowcast grib_to_netcdf "nowcast+ --run-date 2023-02-25 --debug"
  * hrdps_y2023m02d25.nc took 15 minutes and 18.081G of memory
  * fcst/hrdps_y2023m02d26.nc took 15 minutes and 31.547G of memory
  * fcst/hrdps_y2023m02d27.nc took 9 minutes and 39.098G of memory
4th test:
      launch_remote_worker salish-nowcast grib_to_netcdf "nowcast+ --run-date 2023-02-26"
      launch_remote_worker salish-nowcast grib_to_netcdf "nowcast+ --run-date 2023-02-27"
Started work on generating weights file:
* ref: https://salishsea-meopar-docs.readthedocs.io/en/latest/code-notes/salishsea-nemo/nemo-forcing/atmospheric.html#creating-new-weights-files
* created symlinks in grid/ required to run get_weight_nemo:
    cd /data/dlatorne/MEOPAR/grid
    ln -sf /results/forcing/atmospheric/continental2.5/nemo_forcing/hrdps_y2023m02d23.nc atmos.nc
    ln -sf bathymetry_202108.nc bathy_meter.nc
* Tried to generate weights file:
    /ocean/dlatorne/MEOPAR/NEMO-EastCoast/NEMO_Preparation/4_weights_ATMOS/get_weight_nemo

      sbc_blk_core : flux formulattion for ocean surface boundary condition
      ~~~~~~~~~~~~
                namsbc_core Namelist
                list of files
                      root filename: ./atmos variable name: u_wind climatology:  T  data type: yearly 
                      root filename: ./atmos variable name: v_wind climatology:  T  data type: yearly 
                      root filename: ./atmos variable name: qair climatology:  T  data type: yearly 
                      root filename: ./atmos variable name: solar climatology:  T  data type: yearly 
                      root filename: ./atmos variable name: therm_rad climatology:  T  data type: yearly 
                      root filename: ./atmos variable name: tair climatology:  T  data type: yearly 
                      root filename: ./atmos variable name: precip climatology:  T  data type: yearly 
                      root filename: ./no_snow variable name: snow climatology:  T  data type: yearly 
      reading : ./atmos.nc
      atmospheric forcing netcdf grid dimensions: nx=         230 , ny=         190
                get_atmo_grid ~~~ found X axis varid:           4
                get_atmo_grid ~~~ found Y axis varid:           5
      grid_type           2
      xmin/xmax/origin  0.229678E+03  0.238593E+03  0.229678E+03
      Error in map_interpolation: ymin=   47.387591999999998       and y=   46.859664916992188     
      writing variable : src01
      status put           0
      writing variable : wgt01
      writing variable : src02
      status put           0
      writing variable : wgt02
      writing variable : src03
      status put           0
      writing variable : wgt03
      writing variable : src04
      status put           0
      writing variable : wgt04
  * Susan figured out that we miscommunicated on the lon/lat indices for grid cropping such that
    I had them swapped in the nowcast config; after correcting that, and re-running grib_to_netcdf
    for 2023-02-23, get_weight_nemo ran without error
Started running grib_to_netcdf in preparation to backfill production:
* 2020-02-23 to 2023-02-24
(SalishSeaCast)

Continued work on changes to use HRDPS 2.5km continental product
branch: hrdps-continental
PR#156
* created issue #157 re: restoration of Sand Heads visualization plots for automation monitoring
* added generation of `fcst/hrdps_` file for forecast day 1 for ``grib_to_netcdf nowcast+``
* added generation of `fcst/hrdps_` file for forecast day 2 for ``grib_to_netcdf nowcast+``
* changed _update_checklist() to have fcst=False default arg
* added generation of `fcst/hrdps_` file for forecast day 1 for ``grib_to_netcdf forecast2``
* added generation of `fcst/hrdps_` file for forecast day 2 for ``grib_to_netcdf forecast2``
* deleted old grib_to_netcdf code
* dropped wgrib2 from logging config & deployment docs
* added logging port config for grib_to_netcdf to run on salish
(SalishSeaNowcast)


Tue 14-Mar-2023
^^^^^^^^^^^^^^^

Did manual tasks that automation isn't doing due to change to HRDPS continental product by running
  pkill -f collect_weather
  collect_weather 00 2.5km --backfill --backfill-date 2023-03-14
  collect_weather 06 2.5km --backfill --backfill-date 2023-03-14
  wait for post-collect_weather workers to finish
  clear_checklist
  wait for 12Z forecast to download
  collect_weather 12 2.5km --backfill --backfill-date 2023-03-14
  wait for 18Z forecast to download
  collect_weather 18 2.5km --backfill --backfill-date 2023-03-14
Improved weights file generated yesterday with tools/I_ForcingFiles/Atmos/ImproveWeightsFile.ipynb
* committed new weights file as grid/weights-continental2.5-hrdps_202108_23feb23onward.nc
Continued running grib_to_netcdf in preparation to backfill production:
* 2023-02-16  # for comparison test run
* 2020-02-25 to 2023-03-02
* 2023-03-03 got stopped by missing file:
    FileNotFoundError: [Errno 2] No such file or directory: 
    '/results/forcing/atmospheric/continental2.5/GRIB/20230303/00/012/20230303T00Z_MSC_HRDPS_UGRD_AGL-10m_RLatLon0.0225_PT012H.grib2'
  * Susan looked at missing files and agreed that we should persist fcst/hrdps_y2023m02d03.nc
    as hrdps_y2023m02d03.nc
* 2023-03-04 to 2023-03-06
Worked on arbutus towards comparison test run for 2023-02-16:
* used /results2/SalishSea/nowcast-green.201905/16feb23/16feb23nowcast-green.yaml for guidance
    upload_forcing arbutus nowcast+ --run-date 2023-02-16 --debug
    make_forcing_links arbutus nowcast-green --run-date 2023-02-16 --debug
    * need hrdps_y2023m02d15.nc
    * ran grib_to_netcdf nowcast+ 2023-02-15 on skookum and uploaded file
* updated grid clone; it was at PROD-nowcast-green-201905
    git switch main
    gir pull
* left rivers-climatology, tides, and tracers clones at PROD-nowcast-green-201905
* SS-run-sets on arbutus is at (an apparently uncommitted) PROD-nowcast-green-201905-v2
  * identified that as b86bf51c45bd421224ba30c5600695a71c37107d on main
  * made clone on khawla match arbutus:
      git chekcout b86bf51c45bd
      git switch -c PROD-nowcast-green-201905-v2
  * compared namelist sections between branch and main HEAD
      git diff PROD-nowcast-green-201905-v2 main namelist.domain
    * no differences in namelist_cfg sections
    * no differences in namelist_smelt_cfg sections
    * no differences in namelist_top_cfg sections
    * no differences in xios def files
  * reviewed commits since b86bf51c45bd on GitHub; none are outside of v202111/
  * confident that I can switch to main and work from there
  * discovered that default branch name is still master; fixed that
      git switch master
      git branch -m master main
      git fetch origin
      git branch -u origin/main main
      git remote set-head origin -a
      git pull
  * created new v201905/nowcast-green/namelist.atmos_river_hrdps and rsynced it to arbutus
  * on arbutus:
    * changed v201905/nowcast-green/namelist.atmos_river to point to namelist.atmos_river_hrdps
    * moved /nemoShare/MEOPAR/SalishSea/nowcast-green/16feb23/ to 16feb23.west/
    * launch run:
        run_NEMO arbutus nowcast-green 2023-02-16 --debug
        * failed due to river turbiity path in namelist_smelt_rivers
          * changed path from river_turb/riverTurbDaily2 to rivers/riverTurbDaily2
        run_NEMO arbutus nowcast-green 2023-02-16 --debug
        * success
* rsync-ed files down to /data/dlatorne/16feb23/
* Susan checked and blessed fields; improvements in winds in inlets and solar radiation
(SalishSeaCast)

Continued work on changes to use HRDPS 2.5km continental product
branch: hrdps-continental
PR#156
* corrected swapped lon/lat indices for grid cropping in config
* use persistent cluster on salish
* changed _write_netcdf() file created msg from debug to info level
(SalishSeaNowcast)


Wed 15-Mar-2023
^^^^^^^^^^^^^^^

Did manual tasks that automation isn't doing due to change to HRDPS continental product by running
  pkill -f collect_weather
  collect_weather 00 2.5km --backfill --backfill-date 2023-03-15
  collect_weather 06 2.5km --backfill --backfill-date 2023-03-15
  wait for post-collect_weather workers to finish
  clear_checklist
  wait for 12Z forecast to download
  only 479 of 528 files appeared; sent email to Sandrine
  discovered that collection on dd.weather.gc.ca was complete; ran 
    download_weather 12 2.5km
  instead of:
    collect_weather 12 2.5km --backfill --backfill-date 2023-03-15
  make_turbidity_file 2023-03-15
  wait for 18Z forecast to download
  * never finished
  * ran ``download_weather 18 2.5km`` against dd.weather.gc.ca instead
  collect_weather 18 2.5km --backfill --backfill-date 2023-03-15
Continued running grib_to_netcdf in preparation to backfill production:
* 2023-03-07
  * failed with lots of corrupted GRIB messages
* shut down and restarted dask cluster on salish because scheduler had >52G of memory locked up
* re-ran 2023-03-07; failed again
* 2023-03-08 to 2023-03-14
Manually ran --debug steps of automation to backfill nowcast-green/23feb23:
  * on skoookum
    upload_forcing arbutus nowcast+ --run-date 2023-02-23 --debug
    upload_forcing arbutus turbidity --run-date 2023-02-23 --debug
    make_forcing_links arbutus nowcast-green --run-date 2023-02-23 --debug
  * on arbutus
    # we have no hrdps_y2023m02d22, so delete symlink to got make
    cd runs/
    rm NEMO-atmos/hrdps_y2023m02d22.nc
    # edit runs/namelist.time to have values from 22feb23/namelist_cfg
    run_NEMO arbutus nowcast-green 2023-02-23 --debug
  * on skookum
    # can't run watch_NEMO due to --debug in run_NEMO
    download_results arbutus nowcast-green 2023-02-23 --debug
    make_plots nemo nowcast-green research 2023-02-23 --debug
    # skip make_CHS_current_file
    # skip ping_erddap
Realized that I forgot about running make_turbidity_file since 23feb; resolved with:
  for hh in {24..28}; 
    do 
      python3 -m nowcast.workers.make_turbidity_file $NOWCAST_YAML --run-date 2023-02-${hh} --debug; 
    done
  for hh in {01..15}; 
    do 
      python3 -m nowcast.workers.make_turbidity_file $NOWCAST_YAML --run-date 2023-03-${hh} --debug; 
    done
  * 13mar23 failed due to change from PST to PDT
Hacked next_workers to prevent wwatch3 from being launched after nowcast-green:
* copied it to skookum
* restarted master to load new next_workers
* started automated run:
    upload_forcing arbutus nowcast+ --run-date 2023-02-24 --debug
    upload_forcing arbutus turbidity --run-date 2023-02-24
  * run, watcher, downloader, and make_plots were successful
Manually ran --debug steps of automation to backfill wwatch3-nowcast/23feb23:
  * on arbutus:
    * had to hack make_ww3_wind_file to handle lack of coordinates attr on wind vars
  make_ww3_wind_file arbutus nowcast 2023-02-23 --debug
    * hacked make_ww3_current_file to use nowcast-green/ instead of nowcast/ for currents
  make_ww3_current_file arbutus nowcast 2023-02-23 --debug
    * had to upload 22feb23/restart001.ww3 from skookum because it had been purged from arbutus
  run_ww3 arbutus nowcast 2023-02-23 --debug
  * on skookum
  download_wwatch3_results arbutus nowcast 2023-02-23 --debug
  make_plots wwatch3 nowcast publish 2023-02-23 --debug
  * failed, not sure why
Discovered that turbidity obs are bad for most dates since 25feb23
Removed next_workers to prevent wwatch3 from being launched after nowcast-green:
* copied it to skookum
* restarted master to load new next_workers
* started automated run:
    upload_forcing arbutus nowcast+ --run-date 2023-02-25 --debug
    upload_forcing arbutus turbidity --run-date 2023-02-25
  * run was exceedingly slow: ~0.5%/5min
  * wwatch3 launch failed for lots of reasons
(SalishSeaCast)

Finished work on changes to use HRDPS 2.5km continental product
branch: hrdps-continental
PR#156: squash-merged
Changed sphinx-rtd-theme pin to 1.2; PR#159 rebase-merged.
Changed to run wwatch3 after nowcast-green for out of storm surge season; PR#160 rebase-merged.
(SalishSeaNowcast)


Thu 16-Mar-2023
^^^^^^^^^^^^^^^

Did manual tasks that automation isn't doing due to change to HRDPS continental product by running:
  pkill -f collect_weather
  collect_weather 00 2.5km --backfill --backfill-date 2023-03-16
  collect_weather 06 2.5km --backfill --backfill-date 2023-03-16
  wait for post-collect_weather workers to finish
  clear_checklist
  wait for 12Z forecast to download
  * email from Sanrine about problems on hpfx
  * only got 439 of 528 files
  * ran download_weather instead (with grib_to_netcdf enabled in next_workers) 
    * grib_to_netcdf failed because I forgot to set host to run it on salish; ran it manually
  make_turbidity_file
  wait for 18Z forecast to download
  collect_weather 18 2.5km --backfill --backfill-date 2023-03-16
Finished running grib_to_netcdf in preparation to backfill production:
* 2023-03-15
Added --run-date to make_ww3_wind_file and make_ww3_current_file
Launched wwatch3-nowcast/24feb23:
  make_ww3_wind_file arbutus nowcast 2023-02-24
  make_ww3_current_file arbutus nowcast 2023-02-24 
  * created current file, but crashed manager because there are no ``nowcast`` message types
  make_ww3_current_file arbutus nowcast 2023-02-24 --debug
  run_ww3 arbutus nowcast 2023-02-24
  * watch_ww3 launched via automation and reported to log
  * download_wwatch3_results launched via automation
Launched wwatch3-nowcast/25feb23:
  make_ww3_wind_file arbutus forecast 2023-02-25
  make_ww3_current_file arbutus forecast 2023-02-25 
  * failed due to no NEMO forecast for 2023-02-25
Fixed bug in next_workers whereby the nowcast msg types were missing from
after_make_ww3_current_file(); uploaded to skookum; restarted manager
Launched wwatch3-nowcast/25feb23:
  make_ww3_wind_file arbutus nowcast 2023-02-25
  make_ww3_current_file arbutus nowcast 2023-02-25 
  * run_ww3 2023-02-25 and watch_ww3 launched via automation
  * download_wwatch3_results launched via automation
Launched nowcast/26feb23:
  upload_forcing arbutus nowcast+ --run-date 2023-02-26 --debug
  upload_forcing arbutus turbidity --run-date 2023-02-26
  * run_NEMO, watch_NEMO  launched via automation
  * excessively slow again
    * found 15 wwatch3 processes running on nowcast1 that shouldn't have been; killed them
    * checked other compute nodes and found no wwatch3 processes; nowcast8 is not in use
    * sped up to 8.5%/5min in 4th report message
  * wwatch3 run setup failed because make_ww3_current_file was for forecast, not nowcast
  * make_forcing_links for nowcast-dev got launched
Hacked next_workers to fix those 2 issues; uploaded to skookum, restarted manager
Launched wwatch3-nowcast/25feb23:
  make_ww3_wind_file arbutus nowcast 2023-02-26
  make_ww3_current_file arbutus nowcast 2023-02-26 
Launched nowcast/27feb23:
  upload_forcing arbutus nowcast+ --run-date 2023-02-27 --debug
  upload_forcing arbutus turbidity --run-date 2023-02-27
  * run_NEMO, watch_NEMO, download_results, make_ww3_wind_file, make_ww3_current_file,
    run_ww3, watch_ww3 & download_wwatch3_results launched via automation
  * wwatch3 runs on nowcast1-nowcast5
Launched nowcast/27feb23:
  upload_forcing arbutus nowcast+ --run-date 2023-02-27 --debug
  upload_forcing arbutus turbidity --run-date 2023-02-27
Launched nowcast/28feb23:
  upload_forcing arbutus nowcast+ --run-date 2023-02-28 --debug
  upload_forcing arbutus turbidity --run-date 2023-02-28
Launched nowcast/01mar23:
  upload_forcing arbutus nowcast+ --run-date 2023-03-01 --debug
  upload_forcing arbutus turbidity --run-date 2023-03-01
(SalishSeaCast)

Started work on changes to manage catch-up after change to HRDPS continental product
branch: hrdps-continental-catch-up
PR#161
* Fixed bug in next_workers whereby the nowcast msg types were missing from
  after_make_ww3_current_file()
* Handle wind coords attr drop in make_ww3_wind_file
* Handle ``run when`` in make_ww3_current_file
* Added --run-date to make_ww3_wind_file and make_ww3_current_file
(SalishSeaNowcast)


Fri 17-Mar-2023
^^^^^^^^^^^^^^^

archive_tarball feb23 reported an error overnight:
  sysrsync.exceptions.RsyncError: [sysrsync runner] rsync -t /ocean/dlatorne/nowcast-green.201905-feb23.tar graham-dtn:/nearline/rrg-allen/SalishSea/nowcast-green.201905 exited with code 23
* return code 23 means:
    Partial transfer due to error. The rsync command completed with an error, but some files may 
    have been transferred successfully.
* checks of file sizes and line counts look okay, so leaving this as a mystery of a glitch in the 
  matrix
Did manual tasks that automation isn't doing due to change to HRDPS continental product by running:
  pkill -f collect_weather
  collect_weather 00 2.5km --backfill --backfill-date 2023-03-17
  collect_weather 06 2.5km --backfill --backfill-date 2023-03-17
  wait for post-collect_weather workers to finish
  clear_checklist
  wait for 12Z forecast to download
  collect_weather 12 2.5km --backfill --backfill-date 2023-03-17
  * grib_to_netcdf failed because host to run it on was still not set to salish; ran it manually
  make_turbidity_file
  wait for 18Z forecast to download
  collect_weather 18 2.5km --backfill --backfill-date 2023-03-17
Explored CaSPAr (https://github.com/julemai/CaSPAr/wiki/Home) to obtain missing HRDPS files:
* files are netCDF
* variables probably have different names
  see: https://github.com/julemai/CaSPAr/wiki/Connection-between-CaSPAr-and-MSC-Datamart
* variables that may not be available:
  * wiki list is for RPDS, and it only shows 16 variables on CaSPAr,
    but https://github.com/julemai/CaSPAr/wiki/Available-products says there are 55 RDPS variables
    (and 50 HRDPS)
  * PRATE_SFC_0  # precipitation rate at ground level (for VHFR FVCOM)
  * DSWRF_SFC_0  # accumulated downward shortwave (solar) radiation at ground level
  * SPFH_TGL_2   # specific humidity at 2m elevation
      SPFH_SFC_0 instead, but with note: 
      "Discrepancy with ECCC dictionary: dictionary says it is a 2m variable"
  * RH_TGL_2     # relative humidity at 2m elevation (for VHFR FVCOM)
* instructions say:
    "After that you will need to download and install the app Globus Connect Personal on your machine."
  but I will see if I can get it to work with the graham Globus endpoint so that we can see an
  HRDPS file
* used Compute Canada is to log in to Globus; had to disable Firefox Enhanced Tracking Protection
* registered CaSPAr account
* variable names are way different
* need to specify region via draw or upload shape for geojson file; hacked a draw
* submitted request at 10:38
* request completed at 10:50; got an email containing a link to retrieve data
  * downloaded /data/dlatorne/2023030200.nc
* did another request for 03mar23, hours 0-25 from forecast 00, 06 & 12
  * got results
Launched nowcast/02mar23:
  upload_forcing arbutus nowcast+ --run-date 2023-03-02 --debug
  upload_forcing arbutus turbidity --run-date 2023-03-02
Created symlink to persist fcst/hrdps_y2023m02d03.nc as hrdps_y2023m02d03.nc
Launched nowcast/03mar23:
  upload_forcing arbutus nowcast+ --run-date 2023-03-03 --debug
  upload_forcing arbutus turbidity --run-date 2023-03-03
Launched nowcast/04mar23:
  upload_forcing arbutus nowcast+ --run-date 2023-03-04 --debug
  upload_forcing arbutus turbidity --run-date 2023-03-04
Launched nowcast/05mar23:
  upload_forcing arbutus nowcast+ --run-date 2023-03-05 --debug
  upload_forcing arbutus turbidity --run-date 2023-03-05
Launched nowcast/06mar23:
  upload_forcing arbutus nowcast+ --run-date 2023-03-06 --debug
  upload_forcing arbutus turbidity --run-date 2023-03-06
Launched nowcast/07mar23:
  upload_forcing arbutus nowcast+ --run-date 2023-03-07 --debug
  upload_forcing arbutus turbidity --run-date 2023-03-07
Launched nowcast/08mar23:
  upload_forcing arbutus nowcast+ --run-date 2023-03-08 --debug
  upload_forcing arbutus turbidity --run-date 2023-03-08
Email conversation w/ Michael resulted in an agreement to not restart FVCOM VHFR runs.
(SalishSeaCast)


Sat 18-Mar-2023
^^^^^^^^^^^^^^^

Did manual tasks that automation isn't doing due to change to HRDPS continental product by running:
  pkill -f collect_weather
  collect_weather 00 2.5km --backfill --backfill-date 2023-03-18
  collect_weather 06 2.5km --backfill --backfill-date 2023-03-18
  wait for post-collect_weather workers to finish
  clear_checklist
  wait for 12Z forecast to download
  collect_weather 12 2.5km --backfill --backfill-date 2023-03-18
  wait for 18Z forecast to download
  collect_weather 18 2.5km --backfill --backfill-date 2023-03-18
Launched nowcast/09mar23:
  upload_forcing arbutus nowcast+ --run-date 2023-03-09 --debug
  upload_forcing arbutus turbidity --run-date 2023-03-09
Launched nowcast/10mar23:
  upload_forcing arbutus nowcast+ --run-date 2023-03-10 --debug
  upload_forcing arbutus turbidity --run-date 2023-03-10
Launched nowcast/11mar23:
  upload_forcing arbutus nowcast+ --run-date 2023-03-11 --debug
  upload_forcing arbutus turbidity --run-date 2023-03-11
Launched nowcast/12mar23:
  upload_forcing arbutus nowcast+ --run-date 2023-03-12 --debug
  upload_forcing arbutus turbidity --run-date 2023-03-12
Launched nowcast/13mar23:
  upload_forcing arbutus nowcast+ --run-date 2023-03-13 --debug
  upload_forcing arbutus turbidity --run-date 2023-03-13
Launched nowcast/14mar23:
  upload_forcing arbutus nowcast+ --run-date 2023-03-14 --debug
  upload_forcing arbutus turbidity --run-date 2023-03-14
Launched nowcast/15mar23:
  upload_forcing arbutus nowcast+ --run-date 2023-03-15 --debug
  upload_forcing arbutus turbidity --run-date 2023-03-15
Launched nowcast/16mar23:
  upload_forcing arbutus nowcast+ --run-date 2023-03-16 --debug
  upload_forcing arbutus turbidity --run-date 2023-03-16
(SalishSeaCast)

Continued work on changes to manage catch-up after change to HRDPS continental product
branch: hrdps-continental-catch-up
PR#161
* moved make_turbidity_file to after download_weather/collect_weather 12 
* restored grib_to_netcdf nowcast+ to automation flow
(SalishSeaNowcast)

Drove to White Rock to visit J.


Sun 19-Mar-2023
^^^^^^^^^^^^^^^

Did manual tasks that automation isn't doing due to change to HRDPS continental product by running:
  pkill -f collect_weather
  collect_weather 00 2.5km --backfill --backfill-date 2023-03-19
  collect_weather 06 2.5km --backfill --backfill-date 2023-03-19
  wait for post-collect_weather workers to finish
  clear_checklist
  wait for 12Z forecast to download
  collect_weather 12 2.5km --backfill --backfill-date 2023-03-19
  wait for 18Z forecast to download
  collect_weather 18 2.5km --backfill --backfill-date 2023-03-19
Launched nowcast/17mar23:
  upload_forcing arbutus nowcast+ --run-date 2023-03-17 --debug
  upload_forcing arbutus turbidity --run-date 2023-03-17
Launched nowcast/18mar23:
  upload_forcing arbutus nowcast+ --run-date 2023-03-18 --debug
  upload_forcing arbutus turbidity --run-date 2023-03-18
Launched nowcast/19mar23:
  upload_forcing arbutus nowcast+ --run-date 2023-03-19 --debug
  upload_forcing arbutus turbidity --run-date 2023-03-19
(SalishSeaCast)

Rode the TFC Sunday group ride.








TODO:
* libwgrib2:
  * fork yt87/libwgrib2 - done
  * create SalishSeaCast branch
  * add environment-dev like:
      mamba create -n libwgrib2-dev make gfortran libnetcdf libaec libpng \
        "jasper<3" _openmp_mutex conda-build
* pywgrib2_xr
  * add SalishSeaNowcast docs re: clone & install pywgrib2_xr,
    including install of vendored libwgrib2 before installing pywgrib2_xr


TODO:
* update sphinx-rtd-theme pin in envs when 1.2 is released
  * MOAD/docs
  * SalishSeaCast/docs



TODO:
* SalishSeaCast/docs:
  * replace broken links:
    * http://pages.physics.cornell.edu/~myers/teaching/ComputationalMethods/
    * http://pages.physics.cornell.edu/~myers/teaching/ComputationalMethods/LectureNotes/Intro_to_Python.pdf




TODO:
* rename XIOS-ARCH/COMPUTECANADA to XIOS-ARCH/ALLIANCECANADA
* update MOAD/docs XIOS section accordingly
* update XIOS-ARCH README accordingly

TODO:
* add assign-issue-pr action to MOAD/docs repo
* drop dead link to Advection Kernels in OCean Parcels section; it is 404 and I can't find anything 
  equivalent in Parcels docs or tutorials now.



* tidy module & functions notebook & module



TODO:
* numpy.int in moad_tools random_oil_spills

* pre-commit auto-update
  * SalishSeaNEMO-nowcast - done
  * NEMO-Cmd
  * Reshapr
  * MOAD/docs
  * MoaceanParcels
  * cookiecutter-MOAD-pypkg
  * AtlantisCmd



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
  * Make-MIDOSS-Forcing - archived
  * WWatch3-Cmd - archived
  * also replace setup.py with pyproject.toml ??
    * AtlantisCmd
    * FVCOM-Cmd
    * salishsea-site
    * moad-app-dev - archive
    * rpn-to-gemlam - archive
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
