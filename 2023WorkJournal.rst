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
  * possible memory in chiplet; terabyte memory bandwidth
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
  * reviewed missed ones and founds that they were all in DMs and of no consequence
* manually copy-pasted notes from private #fal-estate to #sada-fal-estate

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
  * mar16 chemistry is a case of make_averaged_dataset worker not working without a msg
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
  * may16 biology is a case of make_averaged_dataset worker not working without a msg
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
  difference messages from ``nowcast.workers.day_month_avgs.py`` running in that env on skookum; 
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

Phys Ocgy seminar: Ruiqi Li, U Colorado; Bivalves

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
  * log shows server disconnect at 07:16, than continuous connection timeouts, retrying every 64 s2
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

UptimeRobot reported that ERDDAP was down for 3m28s at 08:06 due to connection timeout.
(ERDDAP)

make_ssh_files forecast2 didn't find obs for 1feb so persisted forecast
Updated to sentry-sdk 1.14.0 in prod env on skookum
Started changing sr_subscribe instances to use queues on hpfx:
* branch: hpfx-queues
* noticed that Tuesday's test of hrdps-west-hpfx had 2 unwanted directory levels;
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

Ophthalmologist appt.


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
  over-length lines are being ignored
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
* refactored transformation of dataframe from .csv to 2-column dataframe with date as index
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
  and even a subset of pyupgrade and autoflake" (from conda-forge description)
* embedded docs in ruff; e.g.
    ``ruff rule F541``
* autofix capability:
    ``ruff --fix ...``
    * *caution* can break code; code transformation is a hard problem
* can be configured in ``pyproject.toml``
* number of violations of each rule
    ``ruff --statistics``
* can add ``# noqa`` comments to silence notifications to get to clean state
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
* Birgit reported in Paul's attendance at DRAKKAR mtg:
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
  * cp run/2022_bloomcast_infile.yaml run/2023_bloomcast_infile.yaml
  * mv run/2022_bloomcast_infile.yaml run/2022/
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
* continued unit tests & refactoring of _do_a_pair()
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
  * issue resolved by changing pandas.read_csv() from default utf-8 encoding to old iso-8859-1 
    (Western European) encoding; suspect config control bug at ECCC
* recover started at ~09:00:
  * hacked collect_river_data worker on skookum to add ``encoding="iso-8859-1"``
  * updated /SalishSeaCast/datamart/hydrometric/collect_river_date.sh to include Roberts Creek and 
    ECCC arg to collect_river_data, then ran it
  * restarted automation:
      upload_forcing arbutus forecast2
      upload_forcing orcinus forecast2
      upload_forcing optimum forecast2
      upload_forcing graham-dtn forecast2
      wait for forecast2 runs to finish
      upload_forcing arbutus nowcast+
      upload_forcing orcinus nowcast+
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
    get_onc_ctd SCVIP  # backfill-able
    get_onc_ctd SEVIP  # backfill-able
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
    get_onc_ctd SCVIP  # backfill-able
    get_onc_ctd SEVIP  # backfill-able
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
* started work on replacing @patch with monkeypatch in download_weather
* started work on updating grb_to_netcdf
  * updated sub-region and Sand Heads indices with values that Susan found in continental domain
  * stalled out on step of getting grid definition via grid_defn.pl and wgrib2
    * Susan found updated tools: pywgrib2_s
(SalishSeaNowcast)

Continued downloading as much 2023 continental as possible:
  * 15jan-31jan
Did manual tasks that automation isn't doing due to change to HRDPS continental product:
  nemo_nowcast.workers.clear_checklist
  /SalishSeaCast/datamart/hydrometric/collect_river_data.sh yyyy-mm-dd
  /results/forcing/rivers/observations/collect_river_data.sh yyyy-mm-dd
  get_onc_ctd SCVIP  # backfill-able
  get_onc_ctd SEVIP  # backfill-able
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
  collect_weather worker can be started so that we know about failures like 03mar in more timely
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
* created functions to build NEMO forcing conformant xarray dataset from a range of hours of a
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
* changed forcing file name template from ``ops_`` to ``hrdps_``
* added netCDF generation code for 24h forecast case; no de-allocation or rotation yet
* started work on apportioning accumulation variables (de-allocation)
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
* finished work on apportioning accumulation variables (de-allocation)
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
* confirmed expected number of continental2.5 GRIB files:
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
  * memory footprint continued to grow for fcst/hrdps_y2023m02d25.nc
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

      sbc_blk_core : flux formulation for ocean surface boundary condition
      ~~~~~~~~~~~~
                nam+sbc_core Namelist
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
  * Susan figured out that we mis-communicated on the lon/lat indices for grid cropping such that
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
      git checkout b86bf51c45bd
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
  * created new v201905/nowcast-green/namelist.atmos_river_hrdps and rsync-ed it to arbutus
  * on arbutus:
    * changed v201905/nowcast-green/namelist.atmos_river to point to namelist.atmos_river_hrdps
    * moved /nemoShare/MEOPAR/SalishSea/nowcast-green/16feb23/ to 16feb23.west/
    * launch run:
        run_NEMO arbutus nowcast-green 2023-02-16 --debug
        * failed due to river turbidity path in namelist_smelt_rivers
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
  * on skookum
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
  * email from Sandrine about problems on hpfx
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
Launched nowcast-green/26feb23:
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
Launched nowcast-green/27feb23:
  upload_forcing arbutus nowcast+ --run-date 2023-02-27 --debug
  upload_forcing arbutus turbidity --run-date 2023-02-27
  * run_NEMO, watch_NEMO, download_results, make_ww3_wind_file, make_ww3_current_file,
    run_ww3, watch_ww3 & download_wwatch3_results launched via automation
  * wwatch3 runs on nowcast1-nowcast5
Launched nowcast-green/27feb23:
  upload_forcing arbutus nowcast+ --run-date 2023-02-27 --debug
  upload_forcing arbutus turbidity --run-date 2023-02-27
Launched nowcast-green/28feb23:
  upload_forcing arbutus nowcast+ --run-date 2023-02-28 --debug
  upload_forcing arbutus turbidity --run-date 2023-02-28
Launched nowcast-green/01mar23:
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
Launched nowcast-green/02mar23:
  upload_forcing arbutus nowcast+ --run-date 2023-03-02 --debug
  upload_forcing arbutus turbidity --run-date 2023-03-02
Created symlink to persist fcst/hrdps_y2023m02d03.nc as hrdps_y2023m02d03.nc
Launched nowcast-green/03mar23:
  upload_forcing arbutus nowcast+ --run-date 2023-03-03 --debug
  upload_forcing arbutus turbidity --run-date 2023-03-03
Launched nowcast-green/04mar23:
  upload_forcing arbutus nowcast+ --run-date 2023-03-04 --debug
  upload_forcing arbutus turbidity --run-date 2023-03-04
Launched nowcast-green/05mar23:
  upload_forcing arbutus nowcast+ --run-date 2023-03-05 --debug
  upload_forcing arbutus turbidity --run-date 2023-03-05
Launched nowcast-green/06mar23:
  upload_forcing arbutus nowcast+ --run-date 2023-03-06 --debug
  upload_forcing arbutus turbidity --run-date 2023-03-06
Launched nowcast-green/07mar23:
  upload_forcing arbutus nowcast+ --run-date 2023-03-07 --debug
  upload_forcing arbutus turbidity --run-date 2023-03-07
Launched nowcast-green/08mar23:
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
Launched nowcast-green/09mar23:
  upload_forcing arbutus nowcast+ --run-date 2023-03-09 --debug
  upload_forcing arbutus turbidity --run-date 2023-03-09
Launched nowcast-green/10mar23:
  upload_forcing arbutus nowcast+ --run-date 2023-03-10 --debug
  upload_forcing arbutus turbidity --run-date 2023-03-10
Launched nowcast-green/11mar23:
  upload_forcing arbutus nowcast+ --run-date 2023-03-11 --debug
  upload_forcing arbutus turbidity --run-date 2023-03-11
Launched nowcast-green/12mar23:
  upload_forcing arbutus nowcast+ --run-date 2023-03-12 --debug
  upload_forcing arbutus turbidity --run-date 2023-03-12
Launched nowcast-green/13mar23:
  upload_forcing arbutus nowcast+ --run-date 2023-03-13 --debug
  upload_forcing arbutus turbidity --run-date 2023-03-13
Launched nowcast-green/14mar23:
  upload_forcing arbutus nowcast+ --run-date 2023-03-14 --debug
  upload_forcing arbutus turbidity --run-date 2023-03-14
Launched nowcast-green/15mar23:
  upload_forcing arbutus nowcast+ --run-date 2023-03-15 --debug
  upload_forcing arbutus turbidity --run-date 2023-03-15
Launched nowcast-green/16mar23:
  upload_forcing arbutus nowcast+ --run-date 2023-03-16 --debug
  upload_forcing arbutus turbidity --run-date 2023-03-16
(SalishSeaCast)

Continued work on changes to manage catch-up after change to HRDPS continental product
branch: hrdps-continental-catch-up
PR#161
* moved make_turbidity_file to after download_weather/collect_weather 12 
* restored grib_to_netcdf nowcast+ to automation flow
* added pytest.mark.skip() to tests for features disabled during catch-up
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
Launched nowcast-green/17mar23:
  upload_forcing arbutus nowcast+ --run-date 2023-03-17 --debug
  upload_forcing arbutus turbidity --run-date 2023-03-17
Launched nowcast-green/18mar23:
  upload_forcing arbutus nowcast+ --run-date 2023-03-18 --debug
  upload_forcing arbutus turbidity --run-date 2023-03-18
Launched nowcast-green/19mar23:
  upload_forcing arbutus nowcast+ --run-date 2023-03-19 --debug
  upload_forcing arbutus turbidity --run-date 2023-03-19
(SalishSeaCast)

Rode the TFC Sunday group ride.


Week 12
-------

Mon 20-Mar-2023
^^^^^^^^^^^^^^^

Did manual tasks that automation isn't doing due to change to HRDPS continental product by running:
  pkill -f collect_weather
  collect_weather 00 2.5km --backfill --backfill-date 2023-03-20
  collect_weather 06 2.5km --backfill --backfill-date 2023-03-20
  wait for post-collect_weather workers to finish
  clear_checklist
  wait for 12Z forecast to download
  collect_weather 12 2.5km --backfill --backfill-date 2023-03-20
  wait for 18Z forecast to download
  collect_weather 18 2.5km --backfill --backfill-date 2023-03-20
Set up simple watchdog logger observing /SalishSeaCast/datamart/hrdps-continental/12 to try to 
understand why collect_weather observer is not working; events for a file:
  2023-03-20 08:48:55 - Created file: /SalishSeaCast/datamart/hrdps-continental/12/012/20230320T12Z_MSC_HRDPS_DLWRF_Sfc_RLatLon0.0225_PT012H.grib2.tmp
  2023-03-20 08:48:55 - Modified directory: /SalishSeaCast/datamart/hrdps-continental/12/012
  2023-03-20 08:48:55 - Modified directory: /SalishSeaCast/datamart/hrdps-continental/12/012
  2023-03-20 08:48:57 - Modified file: /SalishSeaCast/datamart/hrdps-continental/12/012/20230320T12Z_MSC_HRDPS_DLWRF_Sfc_RLatLon0.0225_PT012H.grib2.tmp
  2023-03-20 08:48:57 - Modified file: /SalishSeaCast/datamart/hrdps-continental/12/012/20230320T12Z_MSC_HRDPS_DLWRF_Sfc_RLatLon0.0225_PT012H.grib2.tmp
  2023-03-20 08:48:57 - Modified file: /SalishSeaCast/datamart/hrdps-continental/12/012/20230320T12Z_MSC_HRDPS_DLWRF_Sfc_RLatLon0.0225_PT012H.grib2.tmp
  2023-03-20 08:48:57 - Modified directory: /SalishSeaCast/datamart/hrdps-continental/12/012
  2023-03-20 08:48:57 - Moved file: from /SalishSeaCast/datamart/hrdps-continental/12/012/20230320T12Z_MSC_HRDPS_DLWRF_Sfc_RLatLon0.0225_PT012H.grib2.tmp to /SalishSeaCast/datamart/hrdps-continental/12/012/20230320T12Z_MSC_HRDPS_DLWRF_Sfc_RLatLon0.0225_PT012H.grib2
  2023-03-20 08:48:57 - Modified directory: /SalishSeaCast/datamart/hrdps-continental/12/012
  2023-03-20 08:48:57 - Modified file: /SalishSeaCast/datamart/hrdps-continental/12/012/20230320T12Z_MSC_HRDPS_DLWRF_Sfc_RLatLon0.0225_PT012H.grib2
  2023-03-20 08:48:57 - Modified file: /SalishSeaCast/datamart/hrdps-continental/12/012/20230320T12Z_MSC_HRDPS_DLWRF_Sfc_RLatLon0.0225_PT012H.grib2
Reverted hack on skookum of collect_weather.py that changed it to watching for create events
instead of move events
* traced through collect_weather to confirm that expected_files set is correct
* ran collect_weather 18 2.5km in PyCharm debugger on khawla; not useful
* found change in watchdog 2.17 releaes re: replacing time.sleep() in observer loop with 
  observer.join(); tested on skookum and files get collected, but worker never stops
Reverted hacks in next_workers that prevented runs other than nowcast-green and wwatch3-nowcast.
Hacked next_workers to prevent FVCOM runs by not launching make_fvcom_boundary
rsync-ed hacked next_workers to skookum, and restarted manager
Launched nowcast/20mar23:
    collect_weather 12 2.5km --backfill --backfill-date 2023-03-20
* grib_to_netcdf took ~50min
* missed that upload_forcing in after_make_live_ocean_files was still commented out
    upload_forcing arbutus nowcast+
* run_NEMO nowcast failed due to no /nemoShare/MEOPAR/SalishSea/nowcast/19mar23/namelist_cfg
* copied /nemoShare/MEOPAR/SalishSea/nowcast-green/19mar23/namelist_cfg to 
  /nemoShare/MEOPAR/SalishSea/nowcast/19mar23/namelist_cfg
    make_forcing_links arbutus nowcast+
* NEMO failed due to incorrect namelist_rivers_atmos
* moved SS-run-sets/v201905/nowcast-green/namelist.atmos_rivers_hrdps to 
  SS-run-sets/v201905/namelist.atmos_rivers_hrdps
* symlinked nowcast-green/namelist.atmos_rivers and nowcast-blue/namelist.atmos_rivers to 
  v201905/namelist.atmos_rivers_hrdps
    make_forcing_links arbutus nowcast+
* nowcast-blue ran successfully
* download_results nowcast ran successfully
* make_plots nemo nowcast comparison failed due to no nowcast-blue/19mar23
* make_CHS_currents_file nowcast ran successfully
* forecast ran successfully
* nowcast-green didn't start because there was no upload_forcing turbidity
    upload_forcing arbutus turbidity
  * added upload_forcing turbidity to after_watch_NEMO forecast branch
* download_results forecast ran successfully
* make_CHS_currents_file forecast ran successfully
* update_forecast_datasets nemo forecast ran successfully
* emailed Faith at SMRU re: resumption of ss dataset
* make_surface_current_tiles failed failed due to missing file
* make_plots nemo forecast publish failed due to looking for ops_ files
  * root cause is hard-coded filename template in 
    salishsea_tools.wind_tools.calc_wind_avg_at_point()
* make_feeds forecast ran successfully
* nowcast-green ran successfully
* wwatch3 nowcast launched successfully
* wwatch3 nowcast ran successfully
* wwatch3 forecast launched successfully
* download_results nowcast-green ran successfully
* wwatch3 forecast ran successfully
* download_wwatch3_results nowcast ran successfully
* download_wwatch3_results nowcast ran successfully
Hacked collect_weather to try to resolve lack of exit from loop; didn't work for 00Z forecast;
tried a different hack for 06Z forecast.
(SalishSeaCast)

Cleaned up aborted work on planned fork of libwgrib2.
Cleaned up aborted work on planned fork of pywgrib2_xr.

SoG spring diatoms bllom day!!

Continued work on changes to manage catch-up after change to HRDPS continental product
branch: hrdps-continental-catch-up
PR#161
* restored grib_to_netcdf nowcast+ after after_make_live_ocean_files to automation flow
* added upload_forcing turbidity after forecast run finishes
* restored run_ww3 after wwatch3 nowcast run finishes
Cherry-picked improvement commits from hrdps-continental-catch-up branch into their own
PR branches.
(SalishSeaNowcast)


Tue 21-Mar-2023
^^^^^^^^^^^^^^^

Worked at ESB while Rita was at home.

Overnight hack of collect_weather 06 didn't resolve lack of exit from loop
* ran daily_grind.sh script to do post-collect_weather tasks
* skipped forecast2 runs
Hacked collect_weather another way to test on 12Z foreacst
* 12Z weather did start to flow until 10:47
* at ~12:35 there were 527 of 528 files; most recent file landed at 12:26:45
* missing file:
    /results/forcing/atmospheric/continental2.5/GRIB/20230321/12/026/20230321T12Z_MSC_HRDPS_ACPCP_Sfc_RLatLon0.0225_PT026H.grib2
* file was on hpfx
* decided to kill collect_weather, curl missing file, and get on with things
Launched automation:
  pkill -f collect_weather
  collect_weather 18 2.5km
  bash /results/forcing/rivers/observations/collect_river_data.sh 2023-03-20
  make_turbidity_file
  collect_NeahBay_ssh 06
  download_live_ocean
  launch_remote_worker salish-nowcast grib_to_netcdf "nowcast+"
  * failed because I curl-ed the wrong file
  upload_forcing arbutus nowcast+
collect_weather 18 2.5km finished correctly when all files hae been downloaded :-)

(SalishSeaCast)

Continued work on restoring next_workers to restore more automation steps:
* upload_forcing after make_live_ocean_files
* run_ww3 forecast after wwatch3 nowcast
* cleaned up commented out code in next_workers
* Skip launch of nowcast-dev test during HRDPS catch-up
Changed to run grib_to_netcdf on salish so it can use the persistent dask cluster and lots of
memory there:
* branch: grib_to_netcdf-on-salish
* PR#167
Changed watchdog observer thread management in collect_weather:
branch watdog-2.1.7
PR#168
* replaced time.sleep(1) with observer.join(timeout=1)
* dropped some no longer needed os.fspath() calls
(SalishSeaNowcast)


Wed 22-Mar-2023
^^^^^^^^^^^^^^^

Fixed run-date passing for wwatch3-forecast2
* fixed in branch; fix-ww3-fcst2-run-date
* uploaded to skookum for test tomorrow
* created py311 branch  
  * added 3.11 to python-version matrices of pytest-with-coverage and sphinx-linkcheck
    and let GHA chew on them; both were successful
  * researched mamba-org/provision-with-micromamba as an alternative to 
    conda-incubator/setup-miniconda
    * claims to be faster
    * has environment caching feature with default 1-day TTL
    * tested in pytest-with-coverage; works, but workflow execution was slower than previous one
(SalishSeaNowcast)

Automation worked as expected with the following issues:
* wwatch3-forecast2 failed due to incorrect run-date passing
  * fixed in branch; uploaded to skookum for test tomorrow
* nowcast-blue comparison figs failed; probably due to no nowcast-dev runs?
* figures/research/velocity_section_and_surface.py failed with IndexError
* run_NEMO_agrif failed due to backfill not done
* figures/publish/storm_surge_alerts_thumbnail.py and others failed due to 
  hard-coded ops_*.nc filename template
  * need to fix in salishsea_tools/wind_tools
dask cluster on salish did not appear to leak memory as I was seing earlier
(SalishSeaCast)

Coffee w/ Karyn.

Updated dev env pkgs.
(SalishSeaTools)

Emailed Dafna about reset of sickleave hours.
Did 1/3 of "new employee" training.

Installed Chromium on khawla so that I can maybe use MS Teams PWA (progressive web app)
Installed 1password extension in Chromium.

Checked status of scheduled GHA workflows:
  conda activate gha-workflows
  python3 /media/doug/warehouse/MOAD/gha-workflows/gha_workflows_checker.py


Thu 23-Mar-2023
^^^^^^^^^^^^^^^

Helped Karyn with loading datasets from Susan's sockeye carbon runs.
Helped Cassidy with ssh key on graham via CCDB.

Fixed run-date passing for wwatch3-forecast2
* fixed in branch; fix-ww3-fcst2-run-date
* worked as expected overnight
* PR#171; rebase-merged
Changed codeql-analysis workflow to trigger on push to main and pull requests
targeting main; trying to resolve warning re: 
  configuration present on refs/heads/main was not found:
    .github/workflows/codeql-analysis.yaml:analyze/language:python
(SalishSeaNowcast)

Restarted nowcast-dev in automation:
* on khawla:
  * restored ``make_forcing_links salish nowcast+ --shared-storage`` in after_watch_NEMO
  * copied to skookum to test, and restarted manager to load
* on salish:
    mkdir /results/SalishSea/nowcast-dev.201905/22mar23/
    cp -p /results2/SalishSea/nowcast-green.201905/22mar23/SalishSea_09640080_restart.nc \
      /results/SalishSea/nowcast-dev.201905/22mar23/
    cp -p /results2/SalishSea/nowcast-green.201905/namelist_cfg \
      /results/SalishSea/nowcast-dev.201905/22mar23/
    rsync -av arbutus.cloud-nowcast:/nemoShare/MEOPAR/nowcast-sys/runs/namelist.time \
      /SalishSeaCast/runs/
* on skookum:
    supervisorctl restart manager
    make_forcing_links salish nowcast+ --shared-storage
    * no timesteps because NEMO-atmos links have wrong path
    * fixed path in nowcast.yaml, and copied to skookum
    make_forcing_links salish nowcast+ --shared-storage
(SalishSeaCast)


Fri 24-Mar-2023
^^^^^^^^^^^^^^^

Created ``forcing/atmospheric/continental2.5/nemo_forcing/`` directories on graham-dtn
and optimum; moved ``hrdps_*.nc`` files uploaded by automation to ``GEM2.5/operational/``
Tried to investigate dask scheduler high and increasing memory use without much luck,
other than it appears to be a known issue that the devs don't udnerstand.
Restarted dask cluster scheduler and workers; reduced reserved memory, but no change in swap.
Backfilled ``upload_forcing nowcast+`` to graham-dtn and optimum-hindcast via bash loops
``make_plots nemo forecast publish`` failed with:
  arrow.parser.ParserError: Could not match input '01-Jan-1970 00:00' to any of the following 
  formats: YYYY-MMM-DD HH:mm:ss, DD-MMM-YYYY HH:mm:ss, YYYY-MM-DD HH:mm:ss.
in salishsea_tools.nc_tools.time_origin()
Started to get nowcast-agrif working again
* got stalled by permissions on 
``/home/sallen/MEOPAR/`` preventing me from creating new storage tree:
/home/sallen/MEOPAR/continental2.5/NEMO-atmos/fcst; fixed
(SalishSeaCast)

Updated atmospheric forcing paths on optimum-hindcast and graham-dtn in config & unit tests;
Copied config to skookum for testing after grib_to_netcdf nowcast+; confirmed that uploads 
were stored as expected.
Updated atmospheric forcing paths in figure dev & test notebooks
nowcast-dev launched by automation, so committed and puished code to resume nowcast-dev runs after 
HRDPS catch-up.
(SalishSeaNowcast)

Search of SalishSeaCast org shows that only uses of 
salishsea_tools.wind_tools.calc_wind_avg_at_point() are in SalishSeaNowcast and analysis-vicky;
decided to just change hard-coded weather filename templte from ``ops_`` to ``hrdps_`` instead
of trying to generalize; copied planned change to skookum for use by
``make_plots nemo forecast publish``.
Added 'DD-MMM-YYYY HH:mm' to arrow.get() parser patterns in salishsea_tools.nc_tools.time_origin()
to handle ``hrdps_*.nc`` files.
(SalishSeaTools)

GitHub RSA key rotation issue hit Susan on a pull, then me on a push; replacement key I got was
ed25519.

Rode ToW stage 3 on Mountain Route.


Sat 25-Mar-2023
^^^^^^^^^^^^^^^

JRA admitted to Peace Arch; Susan spent the day there.

No increase in dask scheduler memory after 2 runs of grib_to_netcdf.
figures/comparison/sandheads_winds.py failed:
  Traceback (most recent call last):
    File "/SalishSeaCast/SalishSeaNowcast/nowcast/workers/make_plots.py", line 1102, in _calc_figure
      fig = fig_func(*args, **kwargs)
    File "/SalishSeaCast/SalishSeaNowcast/nowcast/figures/comparison/sandheads_winds.py", line 72, in make_figure
      plot_data = _prep_plot_data(hrdps_dataset_url, run_type, run_date)
    File "/SalishSeaCast/SalishSeaNowcast/nowcast/figures/comparison/sandheads_winds.py", line 88, in _prep_plot_data
      u_hrdps = hrdps.u_wind.sel(time=run_date.format("YYYY-MM-DD")).isel(
    File "/SalishSeaCast/nowcast-env/lib/python3.10/site-packages/xarray/core/dataarray.py", line 1329, in sel
      ds = self._to_temp_dataset().sel(
    File "/SalishSeaCast/nowcast-env/lib/python3.10/site-packages/xarray/core/dataset.py", line 2501, in sel
      pos_indexers, new_indexes = remap_label_indexers(
    File "/SalishSeaCast/nowcast-env/lib/python3.10/site-packages/xarray/core/coordinates.py", line 421, in remap_label_indexers
      pos_indexers, new_indexes = indexing.remap_label_indexers(
    File "/SalishSeaCast/nowcast-env/lib/python3.10/site-packages/xarray/core/indexing.py", line 121, in remap_label_indexers
      idxr, new_idx = index.query(labels, method=method, tolerance=tolerance)
    File "/SalishSeaCast/nowcast-env/lib/python3.10/site-packages/xarray/core/indexes.py", line 241, in query
      indexer = self.index.get_loc(label_value)
    File "/SalishSeaCast/nowcast-env/lib/python3.10/site-packages/pandas/core/indexes/datetimes.py", line 714, in get_loc
      raise KeyError(key) from err
  KeyError: '2023-03-24'
figures/research/velocity_section_and_surface.py failed:
  Traceback (most recent call last):
    File "/SalishSeaCast/SalishSeaNowcast/nowcast/workers/make_plots.py", line 1102, in _calc_figure
      fig = fig_func(*args, **kwargs)
    File "/SalishSeaCast/SalishSeaNowcast/nowcast/figures/research/velocity_section_and_surface.py", line 112, in make_figure
      cbar = _plot_vel_section(
    File "/SalishSeaCast/SalishSeaNowcast/nowcast/figures/research/velocity_section_and_surface.py", line 240, in _plot_vel_section
      ax.fill_between(
    File "/SalishSeaCast/nowcast-env/lib/python3.10/site-packages/matplotlib/__init__.py", line 1412, in inner
      return func(ax, *map(sanitize_sequence, args), **kwargs)
    File "/SalishSeaCast/nowcast-env/lib/python3.10/site-packages/matplotlib/axes/_axes.py", line 5252, in fill_between
      return self._fill_between_x_or_y(
    File "/SalishSeaCast/nowcast-env/lib/python3.10/site-packages/matplotlib/axes/_axes.py", line 5180, in _fill_between_x_or_y
      for idx0, idx1 in cbook.contiguous_regions(where):
    File "/SalishSeaCast/nowcast-env/lib/python3.10/site-packages/matplotlib/cbook/__init__.py", line 1262, in contiguous_regions
      idx, = np.nonzero(mask[:-1] != mask[1:])
  IndexError: too many indices for array: array is 0-dimensional, but 1 were indexed
This is issue #138 from before change to HRDPS continental.
(SalishSeaCast)

Reviewed 2022 tax docs; still waiting for trusts T3.

Replaced tube in Susan's rear 650B wheel and extracted glass shard from tire. Installed 650B
wheels and mudguards on her Topstone.


Sun 26-Mar-2023
^^^^^^^^^^^^^^^

dask scheduler held virtual memory is up to 29.333G after 4 runs of grib_to_netcdf.
Created atmospheric forcing interpolation weights file for nowcast-agrif Baynes Sound sub-grid:
In /data/dlatorne/MEOPAR/grid/subgrids/BaynesSound:
  ln -s /results/forcing/atmospheric/continental2.5/nemo_forcing/hrdps_y2023m02d23.nc atmos.nc
  ln -s bathymetry_201702_BS.nc bathy_meter.nc
  cp ../../namelist.get_weight_nemo.gem2.5-gemlam namelist.get_weight_nemo
  ln -s namelist.get_weight_nemo namelist
  /ocean/dlatorne/MEOPAR/NEMO-EastCoast/NEMO_Preparation/4_weights_ATMOS/get_weight_nemo
Improved interpolation weights file with tools/I_ForcingFiles/Atmos/ImproveWeightsFile.ipynb
* Worked in khawla:/media/doug/warehouse/MEOPAR/tools with ``sshfs salish:/data /data``
  and VSCode as Jupyter client
(SalishSeaCast)

Rode TFC Sunday group ride.


Week 13
-------

Mon 27-Mar-2023
^^^^^^^^^^^^^^^

Susan spent the day in White Rock.

Changed email address for EGBC to djl@.

Researched symbolic debugging of C/C++ in VS Code and messaged Raisha about it.
(Atlantis)

dask scheduler held virtual memory is up to 29.371G after 6 runs of grib_to_netcdf.
Continued work on resuming nowcast-agrif runs:
* tried to pull grid repo updates;faield with "fatal: The remote end hung up unexpectedly"
  * initially due to github.com host key change - fixed
  * next due to id_rsa key on oricnus that is not on GitHub; installed id_rsa.pub on GitHub
  * next due to orcinus ssh client using SHA-1
  * gave up
* rsync-ed HRDPS continental interpolation weights files to orcinus
* launched 1st backfill run:
    make_forcing_links orcinus nowcast-agrif 2023-02-23
  * failed due to missing turbidity file; also noticed missing hrdps_y2023m02d22.nc
      upload_forcing orcinus turbidity 2023-02-23
      # we have no hrdps_y2023m02d22, so delete symlink to make NEMO use 1st hour of hrdps_y2023m02d23.nc
        cd /home/dlatorne/nowcast-agrif-sys/runs/
         rm NEMO-atmos/hrdps_y2023m02d22.nc
  * re-try #1; failed
    * trying to use ops_*.nc and weights-gem2.5*.nc files
    * updated SS-run-sets/v201702/smelt-agrif/namelist.atmos_rivers
    * updated SS-run-sets/v201702/smelt-agrif/subgrids/BaynesSound/namelist.atmos_rivers.BS
  * re-try #2; time stepping; success :-)
Backfilled ``upload_forcing turbidity`` to graham-dtn and optimum-hindcast via bash loops
Started backfilling nowcast-agrif runs:
  make_forcing_links orcinus nowcast-agrif 2023-02-24
  make_forcing_links orcinus nowcast-agrif 2023-02-25
  make_forcing_links orcinus nowcast-agrif 2023-02-26
  make_forcing_links orcinus nowcast-agrif 2023-02-27
  make_forcing_links orcinus nowcast-agrif 2023-02-28
* committed new weights file as 
  grid/subgrids/BaynesSound/weights-continental2.5-hrdps_201702_23feb23onward_BS.nc
(SalishSeaCast)

Phys Ocgy seminar by Sacchi re: hyperspectral optical measurement of phytoplacnkton taxonomy

Committed updated atmospheric forcing storage path on orcinus for nowcast-agrif.
(SalishSeaNowcast)

Committed namelist updates:
* AGRIF atmos_rivers
* 201905 atmos_rivers
* 201905 smelt rivers for runs on arbutus re: flatter dir structure
(SS-run-sets)


Tue 28-Mar-2023
^^^^^^^^^^^^^^^

Susan spent the day in White Rock.

Group mtg; see whiteboard.
docs repo maintenance:
* Updated sphinx-rtd-theme pin to 1.2
* Fixed markup re: warnings; mostly missing newlines after directives and some title level
  inconsistencies
* Tracked down new domain hosting Ariane docs and fixed broken links
(MOAD)

dask scheduler held virtual memory is up to 29.408G after 8 runs of grib_to_netcdf.
Continued backfilling nowcast-agrif runs:
  wait for automation run to fail at ~11:20
  make_forcing_links orcinus nowcast-agrif 2023-03-01
  make_forcing_links orcinus nowcast-agrif 2023-03-02
  make_forcing_links orcinus nowcast-agrif 2023-03-03
  make_forcing_links orcinus nowcast-agrif 2023-03-04
  make_forcing_links orcinus nowcast-agrif 2023-03-05
  make_forcing_links orcinus nowcast-agrif 2023-03-06
  make_forcing_links orcinus nowcast-agrif 2023-03-07
  make_forcing_links orcinus nowcast-agrif 2023-03-08
nowcast-green failed because I forgot to pull SalishSeaNowcast update re: namelist_smelt_rivers
on arbutus; re-ran
  make_forcing_links arbutus nowcast-green
(SalishSeaCast)

Started exploring cropping HRDPS continental files to SalishSeaCast domain coverage in 
analysis-doug/notebooks/continental-HRDPS/crop-grib-to-SSC-domain.ipynb.ipynb on khawla.
* discovered that xarray.open_dataset(..., engine="cfgrib") relies on GRIB_Nx and GRIB_Ny
  variable attribute values, but those don't get adjusted by 
  ``ds.sel(y=slice(230, 461), x=slice(300, 491))``
(SalishSeaNowcast)


Wed 29-Mar-2023
^^^^^^^^^^^^^^^

Susan spent the day in White Rock. JRA should go home by weekend.
Picked up all-round glasses with new prescription lens.
Did a spontaneous training ride around UBC; new PR on Spanish Bankc climb.

Answered email from Nate at Hakai re: max time in wave forecast dataset.
dask scheduler held virtual memory jumped up to 53.228G after 10 runs of grib_to_netcdf.
Continued backfilling nowcast-agrif runs:
  wait for automation run to fail at ~11:20
  make_forcing_links orcinus nowcast-agrif 2023-03-09
  make_forcing_links orcinus nowcast-agrif 2023-03-10
  make_forcing_links orcinus nowcast-agrif 2023-03-11
  make_forcing_links orcinus nowcast-agrif 2023-03-12
(SalishSeaCast)

Continued exploring cropping HRDPS continental files to SalishSeaCast domain coverage in 
analysis-doug/notebooks/continental-HRDPS/crop-grib-to-SSC-domain.ipynb.ipynb on khawla.
* setting GRIB_Nx and GRIB_Ny variable attribute values (and GRIB_numberOfPoints for consistency)
  after cropping and before cfgrib.xarray_to_grib.to_grib() results in a file that 
  xarray.open_dataset(..., engine="cfgrib") can read
* warnings on write:
  * FutureWarning: GRIB write support is experimental, DO NOT RELY ON IT!
  * unknown 'typeOfLevel': 'heightAboveGround'. Using GRIB2 template
* to_grib() doesn't like "unknown" var name in ACPC files; decides that it is a temperature!!!
(SalishSeaNowcast)


Thu 30-Mar-2023
^^^^^^^^^^^^^^^

Continued backfilling nowcast-agrif runs:
  make_forcing_links orcinus nowcast-agrif 2023-03-13
  wait for automation run to fail at ~14:00
  make_forcing_links orcinus nowcast-agrif 2023-03-14
  make_forcing_links orcinus nowcast-agrif 2023-03-15
  make_forcing_links orcinus nowcast-agrif 2023-03-16
Discovered that yesterday's collect_weather 18 didn't finish:
* 523 of 528 files
* recovery:
    pkill -f collect_weather
    download_weather 18 2.5km 2023-03-29
    rm -rf /SalishSeaCast/datamart/hrdps-continental/18/*
    download_weather 00 2.5km
    rm -rf /SalishSeaCast/datamart/hrdps-continental/00/*
    download_weather 06 2.5km
    rm -rf /SalishSeaCast/datamart/hrdps-continental/06/*
    wait for forecast2 runs to finish
    download_weather 12 2.5km
    rm -rf /SalishSeaCast/datamart/hrdps-continental/12/*
    collect_weather 18 2.5km
  * nowcast runs started at 12:45, ~2.5h late
dask scheduler held virtual memory edged up to 53.237G after 11 runs of grib_to_netcdf.
dask scheduler held virtual memory edged up to 53.240G after 12 runs of grib_to_netcdf.
Tried to run ``nowcast.workers.day_month_avgs 2023-02-01`` in ``202111-tarballs`` tmux session on
skookum; failed due to no time steps in 22feb23 1h grid_T and biol_T files; passed to Susan in
#hindcast202111-nowcast; she fixed the files, and I completed the averaging.
(SalishSeaCast)

Continued exploring cropping HRDPS continental files to SalishSeaCast domain coverage in 
analysis-doug/notebooks/continental-HRDPS/crop-grib-to-SSC-domain.ipynb.ipynb on khawla.
* confirmed that ACPF_Sfc seems to be the only problem variable
* no amount of mucking around with metadata and changing the dataset variable name seems to make
  a differenece: APCP_Sfc is always stored at air_temperature by to_grib()
* decided to just live with that and hack grib_to_netcdf to handle it
* ran GRIB cropping notebook call for 20230329/06 hours 17 to 41 to make cropped grib files
  that are needed to build run_date + 1 fcst/hrdps_*.nc file
  * took 11m20.1s to process 25x11 = 275 files on khawla with /results mounted by sshfs
* hacked grib_to_netcdf work:
  * 17s to create fcst/hrdps_y2023m03d30.nc on khawla with /results mounted by sshfs
  * precip metadata items that are inaccurate:
    * GRIB_paramId
    * GRIB_cfName
    * GRIB_cfVarName
    * GRIB_name
    * GRIB_shortName
    * GRIB_units
* Susan verified that fcst/hrdps_y2023m03d30.nc fields compare well with hrdps_y2023m03d30.nc
  from uncropped files when plotted by grid indices, but that lons/lats are incorrect
(SalishSeaNowcast)


Fri 31-Mar-2023
^^^^^^^^^^^^^^^

Drove to White Rock to visit J and adapt suite.

Continued backfilling nowcast-agrif runs:
  wait for automation run to fail at ~15:15
  make_forcing_links orcinus nowcast-agrif 2023-03-17
  * stalled due to orcinus down-time
dask scheduler held virtual memory edged up to 53.243G after 13 runs of grib_to_netcdf.
dask scheduler held virtual memory edged up to 53.247G after 14 runs of grib_to_netcdf.
collect_weather 12 didn't finish:
* 0 files
* server failure at ~07:45; queue did not reconnect
* recovery started at ~12:45
    rm -rf /results/forcing/atmospheric/continental2.5/GRIB/20230331/12/
    pkill -f collect_weather
    download_weather 12 2.5km
    supervisorctl restart sr_subscribe 
    collect_weather 18 2.5km
(SalishSeaCast)

Continued exploring cropping HRDPS continental files to SalishSeaCast domain coverage in 
analysis-doug/notebooks/continental-HRDPS/crop-grib-to-SSC-domain.ipynb.ipynb on khawla.
* lons/lats of SSC grib files are getting messed up when they are written by cfgrib
* tried setting attrs re: first and last point to those of cropped grid; that changed what
  is in the SSC grib file, but not to be correct
* gave up; decided to store a georef dataset for the 191x231 lons/lats used in 
  grib_to_netcdf._calc_nemo_var_ds() and read it in grib_to_netcdf._calc_nemo_ds() to pass to
  the many calls of _calc_nemo_var_ds()
Started work on crop_gribs worker and modifying grib_to_netcdf and next_workers to work with it:
* branch: crop-gribs
* PR#
* added --full-continental-grid option to grib_to_netcdf
(SalishSeaNowcast)


April
=====

Sat 1-Apr-2023
^^^^^^^^^^^^^^

Susan went to White Rock to for J's return.

dask scheduler held virtual memory edged up to 53.250G after 16 runs of grib_to_netcdf.
orcinus compute nodes down due to problems with new chiller installation
(SalishSeaCast)

Continued work on crop_gribs worker and modifying grib_to_netcdf and next_workers to work with it:
* branch: crop-gribs
* PR#173
* added ``backend_kwargs={"indexpath": ""}`` to grib_to_netcdf ``open_*dataset()`` calls to
  prevent storage of GRIB index files
* Use stored SSC_grid_georef.nc to set lons/lats
(SalishSeaNowcast)

Rode ToW Stage 4 standard route on Road to Ruins.


Sun 2-Apr-2023
^^^^^^^^^^^^^^

Susan spent part of the day in White Rock.

dask scheduler held virtual memory edged up to 77.048G after 16 runs of grib_to_netcdf.
orcinus login nodes down due to problems with new chiller installation
(SalishSeaCast)

Continued work on crop_gribs worker and modifying grib_to_netcdf and next_workers to work with it:
* branch: crop-gribs
* PR#173
* fixed bug in worker module detection for after_*() functions
* added crop_gribs worker framework
(SalishSeaNowcast)


Week 14
-------

Mon 3-Apr-2023
^^^^^^^^^^^^^^

dask scheduler held virtual memory was unchanged at 77.048G after 18 runs of grib_to_netcdf.
orcinus login nodes down due to problems with new chiller installation
(SalishSeaCast)

Continued work on crop_gribs worker and modifying grib_to_netcdf and next_workers to work with it:
* branch: crop-gribs
* PR#173
* added implmentation of crop_gribs
* tested crop_gribs on khawla w/ sshfs mount
* tested grib_to_netcdf in crop-gribs branch on skookum; 1 min for forecast2
* tested crop_gribs in crop-gribs branch on skookum; 34 min for 00Z
(SalishSeaNowcast)

Planned intro to NEMO on graham w/ Susan; see 
https://salishseacast.slack.com/files/TFR25L4LU/F051YJVREE5?origin_team=TFR25L4LU
Updated docs to move graham setup out of on-boarding sections.
(MOAD)


Tue 4-Apr-2023
^^^^^^^^^^^^^^

Group mtg; see whiteboard.
Did intro to Alliance accounts, getting ssh public key into CCDB, ssh config stanzas for
graham, and connecting via terminal and VS Code.
(MOAD)

dask scheduler held virtual memory jumped to >99G after 20 runs of grib_to_netcdf:
* stopped workers and scheduler
* updated dask in nowcast-env from 2022.12.1 to 2023.3.2; came with:
  * dask, dask-core, distributed, lz4, openssl, and a bunch of arrow, parquet & aws stuff
* restarted scheduler and workers:
    dask scheduler --port 4386 --dashboard-address :4387
    dask worker --nworkers=4 --nthreads=4 --memory-limit auto --local-directory /dev/shm \
      --lifetime 3600 --lifetime-stagger 60 --lifetime-restart localhost:4386
* memory use:
  * worker spawner: 5.010g
  * scheduler: 4.546g
  * 4 workers: 0.664g each
Updated sentry-sdk in nowcast-env
Backfilled forcing to graham-dtn re: yesterday's maintenance downtime:
  upload_forcing graham-dtn nowcast+ 2023-04-03
  upload_forcing graham-dtn turbidity 2023-04-03
Ran ``nowcast.workers.day_month_avgs 2023-03-01`` in ``202111-tarballs`` tmux session on
skookum: successfully created all day-avg and month-avg files without intervention
* small amunt of memory leakage:
  * worker spawner: 5.018g
  * scheduler: 4.588g
  * 4 workers: 1,085g
(SalishSeaCast)

Continued work on crop_gribs worker and modifying grib_to_netcdf and next_workers to work with it:
* branch: crop-gribs
* PR#173
* added crop_gribs to automation flow
* TODO:
  * fix inaccurate ``GRIB_*`` metadata values in ACPC variable
* pulled changes on to skookum after collect_weather 18 finished
  and restarted manager to load updated next_workers module to test overnight
Created issue #174 re: TypeError in get_onc_ferry that seems to be coming from pandas=2.0.0.
(SalishSeaNowcast)


Wed 5-Apr-2023
^^^^^^^^^^^^^^

dask held spawner/scheduler/workers virtual memory steady at 5.018/4.589/0.668 after 1 run of 
grib_to_netcdf
make_ww3_wind_file forecast2 failed with:
  Traceback (most recent call last):
    File "/nemoShare/MEOPAR/nowcast-sys/NEMO_Nowcast/nemo_nowcast/worker.py", line 391, in _do_work
      checklist = self.worker_func(
    File "/nemoShare/MEOPAR/nowcast-sys/SalishSeaNowcast/nowcast/workers/make_ww3_wind_file.py", line 118, in make_ww3_wind_file
      ds = _create_dataset(
    File "/nemoShare/MEOPAR/nowcast-sys/SalishSeaNowcast/nowcast/workers/make_ww3_wind_file.py", line 131, in _create_dataset
      "u_wind": u_wind.rename({"time_counter": "time"}),
    File "/nemoShare/MEOPAR/nowcast-sys/nowcast-env/lib/python3.8/site-packages/xarray/core/dataarray.py", line 1552, in rename
      dataset = self._to_temp_dataset().rename(name_dict)
    File "/nemoShare/MEOPAR/nowcast-sys/nowcast-env/lib/python3.8/site-packages/xarray/core/dataset.py", line 2841, in rename
      variables, coord_names, dims, indexes = self._rename_all(
    File "/nemoShare/MEOPAR/nowcast-sys/nowcast-env/lib/python3.8/site-packages/xarray/core/dataset.py", line 2798, in _rename_all
      variables, coord_names = self._rename_vars(name_dict, dims_dict)
    File "/nemoShare/MEOPAR/nowcast-sys/nowcast-env/lib/python3.8/site-packages/xarray/core/dataset.py", line 2772, in _rename_vars
      raise ValueError(f"the new name {name!r} conflicts")
  ValueError: the new name 'time' conflicts
* unclear why, but a time variable crept into fcst/hrdps_ files
* changed drop_vars() call that should have gotten rid of it from conditional on full_grid to 
  try...except; tested on skookum for 12Z
* grib_to_netcdf failed because I forgot to run crop_gribs for yesterday's 18Z; recovery:
    crop_gribs 18 2023-04-04
    # test grib_to_netcdf w/o dask cluster
    grib_to_netcdf nowcast+
    * failed because crop_gribs 00 last night cropped 4apr rather than 5apr
        crop_gribs 00 2023-04-05
    # test grib_to_netcdf w/o dask cluster
    grib_to_netcdf nowcast+
    * virtual memory stays <3500m, so no need to run in dask cluster on salish
    upload_forcing arbutus nowcast+
    upload_forcing optimum-hindcast nowcast+
    upload_forcing graham-dtn nowcast+
    upload_forcing orcinus nowcast+
* nowcast-blue started at 12:05
orcinus login nodes are back, but not compute yet
* backfill forcing:
    upload_forcing orcinus nowcast+ 2023-04-02
    upload_forcing orcinus nowcast+ 2023-04-03
    upload_forcing orcinus nowcast+ 2023-04-04
    upload_forcing orcinus turbidity 2023-04-02 --debug
    upload_forcing orcinus turbidity 2023-04-03 --debug
    upload_forcing orcinus turbidity 2023-04-04 --debug
(SalishSeaNowcast)

Continued work on crop_gribs worker and modifying grib_to_netcdf and next_workers to work with it:
* branch: crop-gribs
* PR#173
* fixed after_download_weather so that crop_gribs 00 runs for the correct date
* changed drop_vars(time, lon, lat) to use try/except and separated time dropping to resolve issue
  that caused make_ww3_wind_file failure above
* marked failing test_get_onc_ferry.test_resample_nav_coord() test to skip re: pandas=2.0.0 to
  make GHA workflow happy
* updated ECCC file template key change into collect_weather and download_weather
* added crop_gribs to docs including process flow diagram
* changed next_workers to run grib_to_netcdf on skookum instead of salish because we no longer
  need the big memory dask cluter on salish
  * copied change to skookum and restarted manager to load next_workers
* fixed inaccurate ``GRIB_*`` metadata values in ACPC variable
  * GRIB_paramId: 500041
  * GRIB_cfName: precipitation_flux
  * GRIB_cfVarName: precipitation_flux
  * GRIB_name: Total Precipitation rate (S)
  * GRIB_shortName: tot_prec
  * GRIB_units: kg m-2 s-1

* TODO:
  * finish removal of running grib_to_netcdf on salish instead of skookum
(SalishSeaNowcast)

Fixed GitHub OAuth for readthedocs in orgs so that PR builds work now for SalishSeaNowcast

Listened to https://testandcode.com/197 w/ Brett talking about TROVE classifiers:
* can be mostly dropped except for:
  * license
  * private
  * something else to do with framework, maybe


Thu 6-Apr-2023
^^^^^^^^^^^^^^

wwatch3-forecast2 didn't report overnight; investigation showed a stalled watch_ww3 process
from yesterday on arbutus; killed it
* no wwatch3 runs downloaded since 03apr
  * found and downloaded nowcast/04apr
  * no forecast/04apr
  * forecast2/04apr failed due to no wind file
* found apparent off-by-1 error in run dates: nowcast/04apr ran on 05apr
* recovery:
    download_wwatch3_results arbutus nowcast 2023-04-04
    wait until wwatch3-forecast finishes
    * restarted log_aggregator due to no messages from run_wwatch3 or watch_wwatch3
    launch_remote_worker make_ww3_wind_file arbutus forecast
    launch_remote_worker make_ww3_current_file arbutus forecast
grib_to_netcdf failed because 00Z GRIBs weren't cropped; related to date bug I fixed yesterday,
but didn't flow the fix through to production
* got production branch up to date with PR#173
* restarted manager to load latest next_workers
* restarted automation manually; nowcast-blue started at 11:09
orcinus compute nodes are running again; resumed backfilling nowcast-agrif runs:
  wait for automation run to fail at ~12:15
  make_forcing_links orcinus nowcast-agrif 2023-03-17
  make_forcing_links orcinus nowcast-agrif 2023-03-18
  make_forcing_links orcinus nowcast-agrif 2023-03-19
  make_forcing_links orcinus nowcast-agrif 2023-03-20
  make_forcing_links orcinus nowcast-agrif 2023-03-21
  make_forcing_links orcinus nowcast-agrif 2023-03-22
  make_forcing_links orcinus nowcast-agrif 2023-03-23
collect_weather 18 didn't finish
  mv /results/forcing/atmospheric/continental2.5/GRIB/20230406/18/ \
    /results/forcing/atmospheric/continental2.5/GRIB/20230406/18.aside
  download_weather 18 2.5km
  collect_weather 00 2.5km --backfill
(SalishSeaCast)

Continued work on crop_gribs worker and modifying grib_to_netcdf and next_workers to work with it:
* branch: crop-gribs
* PR#173
* removed running grib_to_netcdf on salish instead of skookum

* fixed run-date propogation from watch_NEMO to make_ww3_*_files
  * copied next_workers to skookum
  * restarted manager to load updated next_workers
(SalishSeaNowcast)

UBC-IOS modeling mtg:
* nested inside SS500 (older version of our SSC)
  * SSS150: 129x98m
    * 7 more tidal constituents than SS500
  * VH20: 26x20m
  * SF30: 30x30m
* non-stationary tidal model for Mission water level for use when Mission gauge is down


Fri 7-Apr-2023
^^^^^^^^^^^^^^

**Statutory Holiday** - Good Friday

Worked on graham storage session for 13-Apr (see #alliance-hpc post)
* TODO:
  * confirm XIOS and NEMO builds, etc. with module stack:
      module load StdEnv/2020
      module load netcdf-fortran-mpi/4.6.0
      module load perl/5.30.2
      module load python/3.11.2
    * update MOAD setup docs if okay
(MOAD)

Continued backfilling nowcast-agrif runs:
  wait for automation run to fail at ~
  make_forcing_links orcinus nowcast-agrif 2023-03-24
  make_forcing_links orcinus nowcast-agrif 2023-03-25
  make_forcing_links orcinus nowcast-agrif 2023-03-26
  make_forcing_links orcinus nowcast-agrif 2023-03-27
  make_forcing_links orcinus nowcast-agrif 2023-03-28
  make_forcing_links orcinus nowcast-agrif 2023-03-29
  make_forcing_links orcinus nowcast-agrif 2023-03-30
(SalishSeaCast)

Continued work on crop_gribs worker and modifying grib_to_netcdf and next_workers to work with it:
* branch: crop-gribs
* PR#173
* automation worked without my intervention; rebase-merged PR
(SalishSeaNowcast)


Sat 8-Apr-2023
^^^^^^^^^^^^^^

wwatch3-forecast2 didn't run due to ``run_ww3 --run-date 2023-04-09`` from my edits yesterday;
forcing files were correct to 2023-04-10 06:00 though; re-ran
  launch_remote_worker arbutus run_ww3 "arbutus forecast2 --run-date 2023-04-08"
* success!
Continued backfilling nowcast-agrif runs:
  make_forcing_links orcinus nowcast-agrif 2023-03-31
  wait for automation run to fail at ~
  make_forcing_links orcinus nowcast-agrif 2023-04-01
  make_forcing_links orcinus nowcast-agrif 2023-04-02
  make_forcing_links orcinus nowcast-agrif 2023-04-03
  make_forcing_links orcinus nowcast-agrif 2023-04-04
  make_forcing_links orcinus nowcast-agrif 2023-04-05
crop_gribs failed due to corrupted 
18/030/20230408T18Z_MSC_HRDPS_VGRD_AGL-10m_RLatLon0.0225_PT030H.grib2
* curl-ed file from hpfx and re-ran crop-gribs successfully
collect_weather 00 didn't finish; 517 of 528 files; ran download_weather to recover
(SalishSeaCast)

Committed fix for run-date propogation from watch_NEMO to make_ww3_*_files
* branch: fix-ww3-date-propagation
* PR#175
(SalishSeaNowcast)

Susan formulated plan to deal with nearly full /results2:
* Archive nowcast-green.201905_wrap 2017 & 2018 to graham:/nearline/, then delete
* Archive nowcast-green.201905_wrap 2013-2016 to graham:/nearline/, then replace
  nowcast-green.201905 with them
Created and set permissions on dir on graham:
  mkdir /nearline/rrg-allen/SalishSea/nowcast-green.201905_wrap/
  chmogd g+w /nearline/rrg-allen/SalishSea/nowcast-green.201905_wrap/
Started archiving on skookum in 202111-tarballs tmux session:
* jan18-jun18 done
(hindcast)

Deleted /opp/GEMLAM/2013 after confirming it is archived on /nearline/ and desktop USB drives;
freed 1.5T.

Cleaned up graham:project/dlatorne/MIDOSS.
Deleted graham:/scratch/dlatorne/MIDOSS that was full of empty dirs.


Sun 9-Apr-2023
^^^^^^^^^^^^^^

Finished backfilling nowcast-agrif runs:
  wait for automation run to fail at ~
  make_forcing_links orcinus nowcast-agrif 2023-04-06
  make_forcing_links orcinus nowcast-agrif 2023-04-07
  make_forcing_links orcinus nowcast-agrif 2023-04-08
  make_forcing_links orcinus nowcast-agrif 2023-04-09
(SalishSeaCast)

Continued archiving on skookum in 202111-tarballs tmux session:
* jul18-dec18 done
(hindcast)

Rebase-merged PR#175 re: fix for run-date propogation from watch_NEMO to make_ww3_*_files.
Returned production skookum to up to date main branch.
(SalishSeaNowcast)

Updated PyCharm to 2023.1 on khawal; switched to new UI.

Took transit to White Rock to visit J for Easter Dinner.


Week 15
-------

Mon 10-Apr-2023
^^^^^^^^^^^^^^^

**Statutory Holiday** - Easter Monday

Continued archiving on skookum in 202111-tarballs tmux session:
* jan17-oct17 done
(hindcast)

Did first pass on 2022 income tax returns.

Rode Dust in the Wind ToW stage 4 makeup ride.


Tue 11-Apr-2023
^^^^^^^^^^^^^^^

Squash-merged dependabot PR to update appleboy/ssh-action used in deployment workflow.
(salishsea-site)

Group mtg; see whiteboard.
(MOAD)

Continued archiving on skookum in 202111-tarballs tmux session:
* sep17-dec17 done
(hindcast)

Fixing broken and redirected links except Cornell Python links that are to be replaced by
a new Python section in MOAD docs.
(SalishSeaCast docs)


Wed 12-Apr-2023
^^^^^^^^^^^^^^^

Continued archiving on skookum in 202111-tarballs tmux session:
* jan13-apr13 archived; may13 in progress; jan13 moved from _wrap/
* to preserve dates, ownership & permissions, did a 3-step move from _wrap/
    rm -rf /results2/SalishSea/nowcast-green.201905/*jan13
    rsync -av /results2/SalishSea/nowcast-green.201905_wrap/*jan13 \
      /results2/SalishSea/nowcast-green.201905/
    rm -rf /results2/SalishSea/nowcast-green.201905_wrap/*jan13
(hindcast)

Added intro to Python section.
(MOAD docs)

* Deleted intro to Python section with broken Cornell links in favour of a 
  new Python section in MOAD docs; squash-merged PR#23.
* Replaced ComputeCanada quick-start with graham version, updated to reflect current practice
  and linked to MOAD docs
(SalishSeaCast docs)

Contined changing dev & production envs to Python 3.11
(SalishSeaNowcast)


Thu 13-Apr-2023
^^^^^^^^^^^^^^^

NEMO on graham session #1
(MOAD)

collect_weather 12 didn't finish unitl 11:30; maybe due to WEonG updates?
collect_weather 18 hadn't finished at 17:45
* 506 of 528 files downloaded
* changed sarracenia config to 1 instance from 2 to see if that gets rid of the checksum warnings
* killed collect_weather 18, started collect_weather 00, moved partial 18 aside, 
  launched download_weather 18
collect_weather 00 hadn't finished at 21:45
* 516 of 528 files downloaded
* missing files in hours 016 019 022 023
* still getting checksum warnings with 1 instance
(SalishSeaCast)

Continued archiving on skookum in 202111-tarballs tmux session:
* may13-dec13 archived; feb13 moved from _wrap/
(hindcast)

Contined changing dev & production envs to Python 3.11.
Had to add pygrib (used by OPPTools) to environment-rtd because it suddenly started
to be pip installed and that fails on rtd because there is a C extension.
(SalishSeaNowcast)

Got new phones connected to ubcsecure and eduroam.


Fri 14-Apr-2023
^^^^^^^^^^^^^^^

Got COVID-19 booster shot.

collect_weather 00 didn't make any further progress overnight; sarracenia did download
all 06 files, but was still showing checksum warnings; 12Z downloads finished at 09:30
* recovery:
    kill collect_weather 00
    move 00 aside
    download_weather 00 2.5km
    collect_weather 06 --backfill 2023-04-14
    collect_weather 18 2.5km
    wait for forecast2 runs to finish & sarracenia to finish 12Z downloads
    collect_weather 12 --backfill 2023-04-14
  Exception in thread Thread-1:
  Traceback (most recent call last):
    File "/SalishSeaCast/nowcast-env/lib/python3.10/shutil.py", line 815, in move
      os.rename(src, real_dst)
collect_weather 18 2.5km failed with:
  OSError: [Errno 18] Invalid cross-device link: '/SalishSeaCast/datamart/hrdps-continental/18/001/20230414T18Z_MSC_HRDPS_APCP_Sfc_RLatLon0.0225_PT001H.grib2' -> '/results/forcing/atmospheric/continental2.5/GRIB/20230414/18/001/20230414T18Z_MSC_HRDPS_APCP_Sfc_RLatLon0.0225_PT001H.grib2'

  During handling of the above exception, another exception occurred:

  Traceback (most recent call last):
    File "/SalishSeaCast/nowcast-env/lib/python3.10/threading.py", line 1016, in _bootstrap_inner
      self.run()
    File "/SalishSeaCast/nowcast-env/lib/python3.10/site-packages/sentry_sdk/integrations/threading.py", line 69, in run
      reraise(*_capture_exception())
    File "/SalishSeaCast/nowcast-env/lib/python3.10/site-packages/sentry_sdk/_compat.py", line 60, in reraise
      raise value
    File "/SalishSeaCast/nowcast-env/lib/python3.10/site-packages/sentry_sdk/integrations/threading.py", line 67, in run
      return old_run_func(self, *a, **kw)

    File "/SalishSeaCast/nowcast-env/lib/python3.10/site-packages/watchdog/observers/api.py", line 205, in run
      self.dispatch_events(self.event_queue)
    File "/SalishSeaCast/nowcast-env/lib/python3.10/site-packages/watchdog/observers/api.py", line 381, in dispatch_events
      handler.dispatch(event)
    File "/SalishSeaCast/nowcast-env/lib/python3.10/site-packages/watchdog/events.py", line 272, in dispatch
      {
    File "/SalishSeaCast/SalishSeaNowcast/nowcast/workers/collect_weather.py", line 231, in on_moved
      _move_file(expected_file, self.grib_forecast_dir, self.grp_name)
    File "/SalishSeaCast/SalishSeaNowcast/nowcast/workers/collect_weather.py", line 211, in _move_file
      shutil.move(expected_file, grib_hour_dir)
    File "/SalishSeaCast/nowcast-env/lib/python3.10/shutil.py", line 836, in move
      os.unlink(src)
  FileNotFoundError: [Errno 2] No such file or directory: '/SalishSeaCast/datamart/hrdps-continental/18/001/20230414T18Z_MSC_HRDPS_APCP_Sfc_RLatLon0.0225_PT001H.grib2'
but that doesn't seem to have causes a problem
nowcast-agrif failed with an out of memory error; re-ran and it failed again.
Updated repos and miniconda3 installation on arbutus.
* Built new Python 3.11 nowcast-env
collect_weather 18 didn't finish; recovery
  kill collect_weather
  collect_weather 00 2.5km
  delete 18 tree
  download_weather 18 2.5km

  download_weather 00 1km 2023-04-14
  download_weather 12 1km
(SalishSeaCast)

Continued archiving on skookum in 202111-tarballs tmux session:
* jan14-may14 done; mar14 in progress; mar13-jun13 moved from _wrap/; jul13 move in progress
(hindcast)

Renamed COMPUTECANADA/ to ALLIANCE/.
Updated XIOS-2/arch/ symlinks on graham.
Did a successful test build of XIOS-2 on graham with:
  module load StdEnv/2020
  module load hdf5-mpi/1.10.6
  module load netcdf-c++4-mpi/4.3.1
  module load netcdf-fortran-mpi/4.6.0
  module load netcdf-mpi/4.7.4
  module load perl/5.30.2
(XIOS-ARCH)

Updated XIOS-2 build docs re: XIOS-ARCH COMPUTECANADA/ to ALLIANCE/ change.
Dropped many redundant project/cluster commands sections.
(MOAD docs)


Sat 15-Apr-2023
^^^^^^^^^^^^^^^

Workers were not launching on arbutus:
* no forecast2, or wwatch3-forecast2 runs
* run_NEMO nowcast failed
* traced to me not using envvars.sh as names when I copied files into 
  etc/conda/[de]activate.d/ dirs of new env DOH!
(SalishSeaCast)

Continued archiving on skookum in 202111-tarballs tmux session:
* jun14-dec14 done; aug13-jan14 moved from _wrap/
(hindcast)

Cleaned up horrific rebase mess in py311 branch by cherry-picking to a new py311 branch in PyCharm
and force-pushing to GitHub.
(SalishSeaNowcast)

Did a successful test build of NEMO SalishSeaCast config on graham with:
  module load StdEnv/2020
  module load netcdf-fortran-mpi/4.6.0
  module load perl/5.30.2
  module load python/3.11.2
* TODO:
  * add ``./makenemo -n <config> clean``
  * add typical compilation times:
    * NEMO:  ~3 minutes
    * REBUILD_NEMO: ~15 seconds
(SalishSeaCast docs)


Sun 16-Apr-2023
^^^^^^^^^^^^^^^

Continued archiving on skookum in 202111-tarballs tmux session:
* paused tarball archiving so that I can update skookum:nowcast-env
* feb14-jun14 moved from _wrap/; jul14 move in progress
* resumed tarball archiving in new nowcast-env
* jan15 done; feb15 in progress
(hindcast)

Started setting up my configs for 202111 test & benchmarking runs
Added v202111/file_def.xml w/o day-splitting.
Added v202111/namelist.atmos_rivers_hrdps
(SS-run-sets)

Built new Python 3.11 skookum:nowcast-env.
collect_weather 00 didn't finish;
* 494 of 528 files downloaded
* killed worker, deleted 00 tree, ran download_weather, started collect_weather 06
(SalishSeaCast)


Week 16
-------

Mon 17-Apr-2023
^^^^^^^^^^^^^^^

wwatch3-forecast2 didn't run due to stuck make_ww3_wind_file worker.
collect_weather 12 downloads didn't start until ~10:00!!
* 517 of 528 files downloaded at ~12:00; missing 5 in hour 022, and 6 in hour 023
* used curl to collect missing 11 files from hpfx
* manually restarted automation:
    kill collect_weather 12
    collect_weather 18
    crop_gribs 12
    collect_river_data SkagitMountVernon 2023-04-16
    collect_river_data SnohomishMonroe 2023-04-16
    collect_river_data NisquallyMcKenna 2023-04-16
    collect_river_data GreenwaterGreenwater 2023-04-16
    make_turbidity_file
    collect_NeahBay_ssh 06
    wait for crop_gribs to finish
    grib_to_netcdf nowcast+
    download_live_ocean 
Posted question re: onfly_checksum warnings in sarracenia discussion !&A on GitHub.
Experimented with making collect_weather more robust:
* can monitor time since startup
* can monitor time since previous file downloaded
* scanned sarracenia logs for duration of gaps during download sessions
  * >45 min is not uncommon somewhere around hour 010 since yesterday afternoon's restart
collect_weather 18 had collected only 399 files at 16:15 when hour 048 was full;
* lots of missing files in hours 015-022, 028-036, and 039
collect_weather 00 had only collected 492 files at ~22:00; missing around hours 020
* fixed via the usual dance
(SalishSeaCast)

Continued archiving on skookum in 202111-tarballs tmux session:
* jan15-aug15 done; sep15 in progress; aug14-dec14 moved from _wrap/; jan15 move in progress
(hindcast)


Tue 18-Apr-2023
^^^^^^^^^^^^^^^

Worked at ESB while Rita was at home.

Group mtg; see whiteboard.
(MOAD)

Lunch w/ Camryn.

Updated CCDB domain to ccsb.alliancecan.ca
(MOAD docs)

Squash-merged gha-workflows dependabot PR to bump codecove/codecove-action 
from 3.1.1 to 3.1.2.
Ran gha_workflow_checker/gha_workflows_checker.py and re-enabled workflows that had
been disabled due to inactivity.
Added example of re-enable command to gha-workflows README.
Changed workflow pins in all repos that use gha-workflows from @SHA to @main
to reduce maintenance burden of updates in reusable workflows:
* SalishSeaNowcast
* SalishSeaCast/docs
* UBC-MOAD/gha-workflows
* UBC-MOAD/docs
* UBC-MOAD/SOG-code-collab
* UBC-MOAD/cookiecutter-analysis-repo
* UBC-MOAD/MoaceanParcels
* UBC-MOAD/Reshapr
* UBC-MOAD/moad_tools
* SalishSeaCast/SalishSeaCmd
* SalishSeaCast/NEMO-Cmd
* SalishSeaCast/salishsea-site
* SalishSeaCast/tools
* 43ravens/NEMO_Nowcast
* SS-Atlantis/AtlantisCmd
Changed reusable pytest-with-coverage & sphinx-linkcheck workflows to use 
mamba-org/provision-with-micromamba for conda env creation and caching.
(repos maint)

Started refactoring collect_weather to handle missing file messages by switching
between watchdog and direct download modes:
* branch: robust-collect_weather
(SalishSeaNowcast)

Continued archiving on skookum in 202111-tarballs tmux session:
* sep15-dec15 done; no _wrap moves done
(hindcast)


Wed 19-Apr-2023
^^^^^^^^^^^^^^^

Planned maintenance on ECCC servers delayed 06 weather availability:
* 06 files started appearing at ~05:55
* 12 files started appearing at ~08:12 with 06 files interleaved
* 121 of 528 06 files downloaded as of 09:15; that is all files visible on hpfx & dd.weather
* 12 files still flowing at 09:15; dirs to 047 visible on hpfx & dd.weather
* 06 012-023 dirs appeared on hpfx at ~09:20
* 06 024-048 dirs appeared on hpfx at ~09:25
* 06 files started flowing again at ~09:30
* 12 files stalled at 474 of 528 at ~09:30
* 498 of 528 06 files as of ~10:05; missing files in hours 013-106 & 017-021
* server connection errors at 10:18 to 10:21
* recovery started at 11:00:
    kill collect_weather 06
    restart sarracenia client
    collect_weather 18 2.5km
    move 06 dir aside
    download_weather 06 2.5km
    delete 06.aside dir
  * run_NEMO stalled:
    * manager stderr log on skookum shows 
      ``ssh_exchange_identification: Connection closed by remote host``
    * re-tried successfully via launch_remote_worker
  * make_ww3_current_file failed due to stalled worker from yesterday
    * killed stalled worker
    * restarted automation via launch_remote_worker
  * no wwatch3-forecast/18apr23 restart file, so forecast2 is running from quiescent state
    wait for forecast2 runs to finish
    download_weather 12 2.5 km
    clean up /SalishSeaCast/datamart/hrdps-continental/ sub-dirs
(SalishSeaCast)

Continued archiving on skookum in 202111-tarballs tmux session:
* paused tarball processing so that I cam switch skookum from py311 branch to main
* jan15-may15 moved from _wrap/; jun15 move in progress
(hindcast)

Cancelled EGBC permit to practice.


Thu 20-Apr-2023
^^^^^^^^^^^^^^^

Continued archiving on skookum in 202111-tarballs tmux session:
* continued pause of tarball processing so that I cam switch skookum from py311 branch to main
* jan15-sep15 moved from _wrap/; oct15 move in progress
(hindcast)

Downloaded Minecraft 1.19.4 mods, shader packs, resource packs, data packs:
* sodium 0.4.10
* lithium 0.11.1
* phosphor 0.8.1 is unchanged since 1.19.0 release
* malilib 0.15.3
* MiniHUD 0.26.2
* Twekeroo 0.16.0
* Iris 1.6.1
* ComplementaryShaders 4.7.1
* ComplementaryReimagined 2.0.3
* IronBarsFix-1.19.4
* LowerShield-1.19.4
* RedstoneDevices-1.19.4
  * RedstoneWireFix
  * StickyPistonSides
  * DirectionalDispensersDroppers
  * DirectionalObservers
  * GroovyLevers
  * HopperBottomFix
  * DirectionalHoppers
* DoubleShulkerShells 1.3.3
Noticed interesting resource packs:
* TranslucentPumpkinOverlay
* NoPumpkinOverlay
Installed mods, shader packs & resource packs in MultiMC 1.19.4 instance.
Copied minihud.json & tweakeroo.json from 1.19.3 config/ to 1.19.4 config/
Installed mods & data packs on NodeCraft:
* sodium 0.4.10
* lithium 0.11.1
* phosphor 0.8.1
* DoubleShulkerShells 1.3.3

Changed max HR and zone ranges on Strava & Garmin.

Installed fortls on khawla & graham in its own conda env.
Created ``SS-run-sets/SalishSea/djl/v202111/graham-example.yaml`` on graham.
(graham)

Started work on updating module loads for runs on graham and other Alliance clusters.
(SalishSeaCmd)

Jose reported dates that are missing wwatch3-nowcast runs:
*  30Sep19, 31Dec19, 27Dec20, 13Jan21, 30apr21, 16Apr23
(wwatch3)

Switched SalishSeaNowcast from py311 branch to main after day's runs finished.
collect_weather 18 had only downloaded 512 of 528 files at 16:45; last download was at 15:33
* resolved via the usual dance, but forgot to kill 18 worker and start 00
* used collect_weather 00 --backfill to get 00 files
  * it raised another bogus FileNotFoundError (see Fri 14-Apr)
(SalishSeaCast)


Fri 21-Apr-2023
^^^^^^^^^^^^^^^

make_ww3_current_file forecast2 got stuck again; -15 signal isn't enough to kill it, 
have to use a -9 signal; restarted log_aggregator after kill
graham-dtn rejected ssh key from upload_forcing
* sent email to support
(SalishSeaCast)

On to graham session #2
(MOAD)

Continued archiving on skookum in 202111-tarballs tmux session:
* continued pause of tarball processing due to graham-dtn auth issue
* jan15-oct15 moved from _wrap/; nov15 move in progress
(hindcast)


Sat 22-Apr-2023
^^^^^^^^^^^^^^^

graham-dtn rejected ssh key from upload_forcing
(SalishSeaCast)

Finally got a v202111 1d run to time step; 4x9 decomp on 1 node; timed out after 3h13s;
completed 1545 of 2160 time steps
(graham)

Transit to White Rock to visit J.


Sun 23-Apr-2023
^^^^^^^^^^^^^^^

make_ww3_current_file forecast2 got stuck again; -15 signal isn't enough to kill it, 
have to use a -9 signal; restarted log_aggregator after kill
graham-dtn rejected ssh key from upload_forcing
run_ww3 nowcast failed w/ seg fault in automation and on re-try:
(SalishSeaCast)

Continued SalishSeaCast v202111 scaling tests on graham:
* 01mar23-6x14: 2 nodes
* 01mar23-8x18: 3 nodes
* 01mar23-9x22: 4 nodes
* 01mar23-10x27: 5 nodes
Analysis spreadsheet:
https://docs.google.com/spreadsheets/d/1vUyMXTk2kvam7Ae2Tv8hzadiDIENltYBnvlpayc8-aY/edit?usp=sharing
(graham)


Week 17
-------

Mon 24-Apr-2023
^^^^^^^^^^^^^^^

Continued SalishSeaCast v202111 scaling tests on graham:
* 01mar23-11x32: 6 nodes
* 01mar23-12x28: 6 nodes
* 01mar23-13x31: 7 nodes
* 01mar23-14x34: 8 nodes
* 01mar23-15x38: 9 nodes
* 01mar23-16x40: 10 nodes
* 01mar23-17x41: 11 nodes
* 01mar23-18x44: 12 nodes
* 01mar23-14x32: 8 nodes
* 01mar23-14x40: 9 nodes
* 01mar23-15x34: 9 nodes
* 01mar23-14x33: 8 nodes
* 01mar23-14x35: 9 nodes
* 01mar23-14x31: 8 nodes
* 01mar23-14x34-nopy: 8 nodes; 3s faster than previous 14x34; no need to load Pyhon module
  in SalishSeaNEMO.sh due to having SalishSeaCmd installed in conda env
* 01mar23-19x25: 8 nodes
* 01mar23-19x26: 8 nodes
* 01mar23-16x31: 8 nodes
* 01mar23-15x33: 8 nodes
Analysis spreadsheet:
https://docs.google.com/spreadsheets/d/1vUyMXTk2kvam7Ae2Tv8hzadiDIENltYBnvlpayc8-aY/edit?usp=sharing
(graham)

Squash-merged dependabot PRs re: codecove/codecove-action v3.1.13:
* SalishSeaNowcast
* gha-workflows

graham-dtn rejected ssh key from upload_forcing
TODO:
* backfill upload_forcing nowcast+
* backfill upload_forcing turbidity
Backfilled wwatch3 runs:
* 23apr23/wwatch3-nowcast
* 23apr23/wwatch3-forecast
* 24apr23/wwatch3-nowcast
* 24apr23/wwatch3-forecast
(SalishSeaCast)


Tue 25-Apr-2023
^^^^^^^^^^^^^^^

Email to alliance re: graham-dtn auth issue.

Email to Jenn at ECCC re: Fraser buoy web server problem.

Continued archiving on skookum in 202111-tarballs tmux session:
* resumed tarball processing: jan16-apr16 archived; jan16 in progress
* nov15-dec15 & jan16 moved from _wrap/
(hindcast)

Group mtg; see whiteboard.
(MOAD)

Email to Brad de Young re: 10m water level datasets on ERDDAP.

graham-dtn ssh auth issue resolved; backfilled nowcast+ and turbidity for 21-25 Apr.
Changed sarracenia clients to use queues on dd.weather instead of hpfx in preparation for hpfx
server maintenance tomorrow, and to test if dd.weather is more reliable re: missing messages.
Backfilled nowcast-agrif runs:
  upload_forcing orcinus-nowcast-agrif nowcast+ 2023-04-22
  upload_forcing orcinus-nowcast-agrif nowcast+ 2023-04-23
  upload_forcing orcinus-nowcast-agrif nowcast+ 2023-04-24
  upload_forcing orcinus-nowcast-agrif nowcast+ 2023-04-25
make_ww3_current_file forecast2 got stuck again; killed it; restarted log_aggregator;
re-ran vai launch_remote_worker
Searched work journals back to 2019 re: stalled make_ww3_current_file; past issues were stalled
make_ww3_wind_file; nothing about resolutions, just notes about idea for spotter worker to 
work around issue.
(SalishSeaCast)


Wed 26-Apr-2023
^^^^^^^^^^^^^^^

Mostly occupied with 2547 W 1st deal.

ECCC delayed the hpfx server move that was scheduled for today to Wed 3-May.
make_ww3_current_file forecast got stuck again; killed it; re-ran via launch_remote_worker
collect_weather 18 didn't finish; 522 of 528 files downloaded; resolved via the ususal dance, including 1km downloads
used collect_weather 00 --backfill
launched collect_weather 06
(SalishSeaCast)

Continued archiving on skookum in 202111-tarballs tmux session:
* may16-dec16 archived
* feb16-mar16 moved from _wrap/
(hindcast)


Thu 27-Apr-2023
^^^^^^^^^^^^^^^

make_ww3_current_file forecast got stuck again; killed it; re-ran via launch_remote_worker;
it failed oddly while trying to write 
``/nemoShare/MEOPAR/nowcast-sys/wwatch3-runs/current/SalishSea_1h_20230427_20230427_grid_U.nc``
but the run was successful.
HRDPS 12Z files stopped at 08:30 for the typical break after hour 011, but didn't resume until
11:00.
grib_to_netcdf 12 failed due to missing 20230426/18/005/*TMP_AGL-2m* cropped file
* there was an error crom crop_gribs 18 last night
* re-ran crop-gribs 18 in debug mode; failed
* curl-ed file from hpfx
* re-ran crop-gribs 18 in debug mode; success
* recovery at ~17:00:
    grib_to_netcdf nowcast+
    upload_forcing arbutus
    upload_forcing orcinus
    upload_forcing graham-dtn
    upload_forcing optimum
(SalishSeaCast)

Continued SalishSeaCast v202111 scaling tests on graham:
* longer runs with 19x26 decomposition to find max model days per scheduler partition
  * 3h by-node queue
    * 10d run failed w/ core dump; node failure?
    * re-try 10d failed w/ Transport retry count exceeded
  * 12h by-node queue
    * 40d run: failed with ORTE issue after ~8h, then timed out 
  * 24h by-node queue
    * 80d run planned
(graham)

Continued archiving on skookum in 202111-tarballs tmux session:
* apr16 moved from _wrap/
(hindcast)

AAPS Spring general mtg on Zoom

UBC-IOS modeling collab mtg


Fri 28-Apr-2023
^^^^^^^^^^^^^^^

On to graham session #3
(MOAD)

Continued SalishSeaCast v202111 scaling tests on graham:
* longer runs with 19x26 decomposition to find max model days per scheduler partition
  * 3h by-node queue
    * 10d run: success; 2h30m42s
(graham)

Updated links for workspace, SalishSeaCmd installation, and XIOS-2 & NEMO builds.
(MOAD docs)

Continued archiving on skookum in 202111-tarballs tmux session:
* apr16-aug16 moved from _wrap/; sep16 in progress
(hindcast)

Finihsed work on updating module loads for runs on graham and other Alliance clusters;
rebase-merged PR#37.
(SalishSeaCmd)


Sat 29-Apr-2023
^^^^^^^^^^^^^^^

Continued archiving on skookum in 202111-tarballs tmux session:
* oct16-nov16 moved from _wrap/
(hindcast)

make_ww3_wind_file forecast2 got stuck; killed it
(SalishSeaCast)


Sun 30-Apr-2023
^^^^^^^^^^^^^^^

Finished archiving on skookum in 202111-tarballs tmux session:
* dec16 moved from _wrap/
(hindcast)

Continued SalishSeaCast v202111 scaling tests on graham:
* longer runs with 19x26 decomposition to find max model days per scheduler partition
  * 12h by-node queue
    * 40d run: success: 10h3m56s
  * 24h by-node queue
    * 80d run decided not to run after discussion w/ Susan.
(graham)


May
===

Week 18
-------

Mon 1-May-2023
^^^^^^^^^^^^^^

Tested positive for COVID-19.

Strata windows, gutters & screens cleaned by Flat Mate Property Services.


Tue 2-May-2023
^^^^^^^^^^^^^^

Group mtg; see whiteboard.
(MOAD)


Wed 3-May-2023
^^^^^^^^^^^^^^

Recovery.


Thu 4-May-2023
^^^^^^^^^^^^^^

Recovery.


Fri 5-May-2023
^^^^^^^^^^^^^^

IOS seminar by Dwight Owen re: ONC Oceans 3.0 web portal.

Recovery.

make_ww3_current_file forecast2 got stuck again; noticed when nowcast didn't start; killed it; 
ran ``make_ww3_current_file forecast`` via launch_remote_worker to get back on track
(SalishSeaCast)


Sat 6-May-2023
^^^^^^^^^^^^^^

Recovery.


Sun 7-May-2023
^^^^^^^^^^^^^^

Recovery.


Week 19
-------

Mon 8-May-2023
^^^^^^^^^^^^^^

Recovery.
COVID RAT test still positive, but much fainter.

make_ww3_current_file forecast got stuck again; killed it; 
ran ``make_ww3_current_file forecast`` via launch_remote_worker to get back on track
Did OS pkgs update on arbutus:nowcast0 and rebooted in hopes of resolving 
make_ww3_current_file issue.
(SalishSeaCast)

See work journal.
(Resilient-C)


Tue 9-May-2023
^^^^^^^^^^^^^^

Recovery.
Positive COVID RAT test with a faint line.

Forgot to:
  sudo mount /dev/vdc /nemoShare/
  sudo mount --bind /nemoShare/MEOPAR /export/MEOPAR
  sudo systemctl start nfs-kernel-server.service
  sudo exportfs -f
after restarting arbutus:nowcast0 yesterday; so, no forecast2 runs.
make_ww3_wind_file forecast got stuck; killed it; ran ``run_ww3 nowcast`` via launch_remote_worker
to get back on track; run failed:
* eventually got things working by re-running make_ww3_wind_file via launch_remote_worker
(SalishSeaCast)


Wed 10-May-2023
^^^^^^^^^^^^^^^

Recovery.

Discovered that I already put archive_tarball for V202111 into automation.
Restarted dask scheduler and workers cluster on salish.
Ran ``nowcast.workers.day_month_avgs 2023-04-01`` in ``202111-tarballs`` tmux session on
skookum against dask cluster on salish: 
* successfully created all day-avg and month-avg files without intervention
* 3 FutureWarning per day-avg:
    /SalishSeaCast/Reshapr/reshapr/core/extract.py:929: 
    FutureWarning: Following pandas, the `loffset` parameter to resample will be deprecated 
    in a future version of xarray.  Switch to using time offset arithmetic.
      resampler = extracted_ds.resample(
  created Reshapr issue #82
* small amunt of memory leakage:
  * worker spawner: 5.025g
  * scheduler: 4.670g
  * 4 workers: 0.667g
make_ww3_current_file forecast got stuck again; killed it; 
ran ``make_ww3_current_file forecast`` via launch_remote_worker to get back on track
(SalishSeaCast)

Tidied up refactoring collect_weather to handle missing file messages by switching
between watchdog and direct download modes:
* branch: robust-collect_weather
* **not pushed to GitHub**
* on hold because the issue went away after 25-Apr change to use queues on dd.weather instead of
  hpfx due to impending hpfx server maintenance outage; continned using dd.weather queues after
  hpfx maintenance because missing file messages problem was not present
Made sarracenia change to use queues on dd.weather official:
* branch: sarracenia-dd-weather
* PR#180
* changed to branch on skookum and restarted sarracenia clients to test
  * hydrometric file downloads worked correctly after restart
  * HRDPS continental file downloads worked correctly after restart
(SalishSeaNowcast)


Thu 11-May-2023
^^^^^^^^^^^^^^^

Recovery.

Rebase-merged sarracenia change to use queues on dd.weather official:
* branch: sarracenia-dd-weather
* PR#180
* pull changes on skookum production and returned to main branch
Resumed work on migrating Susan's new rivers processing code into repo:
* last work was 22-Feb before HRDPS flipped to continental grid
* branch: v202111-rivers
* PR#150
* resolved merge conflicts that GitHub was showing in branch:
  * updated envs/requirements.txt
  * cherry-picked yesterday's supervisord.ini changes to use dd.weather servers
* added _calc_runoff_dataset() to do part of the work of write_file()
(SalishSeaNowcast)


Fri 10-May-2023
^^^^^^^^^^^^^^^

Recovery.
COVID RAT test looked negative after 15 minutes, but I noticed a very faint positive line an
hour or more later.

Continued work on migrating Susan's new rivers processing code into repo:
* last work was 22-Feb before HRDPS flipped to continental grid
* branch: v202111-rivers
* PR#150
* refactored the remainder of write_file() into _write_netcdf() and _to_netcdf() patterned after
  those I wrote in grib_to_netcdf worker; latter isolates actual file write so that it can be 
  mocked for testing of the rest of _write_netcdf() functionality
* started thinking about how to proceed to including this work in make_runoff_file worker:
  * PR#150 is big and branched almost 3 months ago, though GitHub says it is can merge without
    conflicts now
  * discussion with Susan concluded that it would be good to be able to run versions of 
    make_runoff_file in automation for both v201702 and v202108 bathymetires
  * maybe squash-merged PR#150, then start a new branch & PR to create make_v202108_runoff_file
    from make_runoff_file?
(SalishSeaNowcast)


Sat 11-May-2023
^^^^^^^^^^^^^^^

Goofed off and worked on prep for move to 2547.


Sun 12-May-2023
^^^^^^^^^^^^^^^

Goofed off and worked on prep for move to 2547 and prep of 2356 for listing.


Week 20
-------

Mon 15-May-2023
^^^^^^^^^^^^^^^

Vancouver to Bellingham

Emailed Emma about missing sick leave pay.

Drove to Bellingham for Susan to attend Salish Sea Salmon workshop.


Tue 16-May-2023
^^^^^^^^^^^^^^^

Bellingham

Cycled Chuckanut Mtn South Summit loop (42km, 1111m, 6.5h)

Email from payroll via Emma explaining that I need to submit hours as well as request sick leave
in order to be paid for sick leave; not how I remember it...

Salish Sea Marine Survival Projet mtg dinner at Two Sisiters Brewing


Wed 17-May-2023
^^^^^^^^^^^^^^^

Bellingham to Vancouver

Noticed that both make_ww3_current_file and make_ww3_wind_file for forecast2/16may23 got stuck;
* recovery:
    wait for nowcast/17may23 to fail
    kill make_ww3_wind_file
    kill make_ww3_current_file
    launch_remote_worker arbutus make_ww3_wind_file forecast 2023-05-16
      * had to try twice to get worker to run; it got stuck the first time
    launch_remote_worker arbutus make_ww3_current_file forecast 2023-05-16
    wait for forecast/16may23 to finish
    launch_remote_worker arbutus make_ww3_wind_file forecast 2023-05-17
    launch_remote_worker arbutus make_ww3_current_file forecast 2023-05-17
download_weather 12 1km failed due to no files in 001-023 directories on dd-alpha server.
(SalishSeaCast)

Drove home from Bellingham


Thu 18-May-2023
^^^^^^^^^^^^^^^

make_ww3_current_file forecast2 stalled overnight; killed it.
download_weather 00 1km and 12 1km failed due to missing files
(SalishSeaCast)

Continued work on migrating Susan's new rivers processing code into repo:
* branch: v202111-rivers
* PR#150
* reviewed changes that will happen on merge file-by-file
* changed 2 config changes to hard-code in daily_river_flows module so as not to disrupt
  v201905 automation with merge
* squash-merged PR#150
* updated production to HEAD of main to test that the squash-merge didn't break anything
* created new branch to continue work with creation of make_v202111_runoff_file
  * branch: make_v202111_runoff_file
(SalishSeaNowcast)

Went with Susan to Faculty of Science promotion celebration dinner at botanical garden.


Fri 19-May-2023
^^^^^^^^^^^^^^^

I missed reverting the rivers."prop_dict module" config change before yesterday's merge of PR#150
so make_runoff_file failed;
* recovery started at ~08:30
    fixed config on skookum
    make_runoff_file
    upload_forcing arbutus forecast2
    upload_forcing orcinus forecast2
    upload_forcing optimum forecast2
    upload_forcing graham-dtn forecast2
* fixed on main
download_weather 00 1km and 12 1km failed due to missing files; sent email to Sandrine;
she confirmed that dd.alpha is unstable; won't be fixed unitl Tuesday
(SalishSeaCast)

Coffee and code help with Karyn.

Continued work on make_v202111_runoff_file:
* branch: make_v202111_runoff_file
(SalishSeaNowcast)


Sat 20-May-2023
^^^^^^^^^^^^^^^

Planning for move to 2547 and prep for listing 2356.

download_weather 00 1km and 12 1km failed due to missing files
(SalishSeaCast)


Sun 21-May-2023
^^^^^^^^^^^^^^^

Prep for listing 2356.

download_weather 00 1km and 12 1km failed due to missing files
(SalishSeaCast)


Week 21
-------

Mon 22-May-2023
^^^^^^^^^^^^^^^

**Statutory Holiday** - Victoria Day

Prep for listing 2356.

Squash-merged dependabot PRs re: version update of codecov-action:
* SalishSeaNowcast
* gha-workflows

LiveOcean changed to new versions; NO3 and NH4 are now separate variables
* Susan updated tools module to add new NO3 and NH4 to be consistent with our prior values
* pulled tools on skookum before grib_to_netcdf finished, so new forcing was in effect for the 
  day's runs
download_weather 00 1km and 12 1km failed due to missing files
(SalishSeaCast)


Tue 23-May-2023
^^^^^^^^^^^^^^^

Group mtg; see whiteboard.
(MOAD)

Checked status of scheduled GHA workflows:
  conda activate gha-workflows
  python3 /media/doug/warehouse/MOAD/gha-workflows/gha_workflows_checker.py
Changed pytest-with-coverage and sphinx-linkcheck reusable workflows to use 
mamba-org/setup-microconda from deprecated mamba-org/provision-with-micromamba.
Squash-merged dependabot PRs to bump requests to 2.31.0 re: CVE-2023-32681 re: 
Proxy-Authorization headers:
* cookiecutter-analysis-repo
* cookiecutter-MOAD-pypkg
* AtlantisCmd
* MoaceanParcels
* NEMO-Cmd
* moad_tools
* NEMO_Nowcast
* Reshapr
* salishsea-site
* SalishSeaCast/docs
* tools
* UBC-MOAD/docs
* SalishSeaCmd
(repos-maint)


Changed pytest-with-coverage workflow to use mamba-org/setup-microconda 
from deprecated mamba-org/provision-with-micromamba.
Squash-merged dependabot PR to bump requests to 2.31.0 re: CVE-2023-32681 re: 
Proxy-Authorization headers.

Continued work on make_v202111_runoff_file:
* branch: make_v202111_runoff_file
* PR#183
(SalishSeaNowcast)

download_weather 00 1km and 12 1km failed due to missing files
(SalishSeaCast)


Wed 24-May-2023
^^^^^^^^^^^^^^^

make_ww3_wind_file forecast stalled yesterday; killed it; re-ran it via launch_remote_worker;
had to run make_ww3_current_file twice too to get run started.
make_ww3_wind_file forecast stalled; killed it; re-ran it via launch_remote_worker.
download_weather 00 1km and 12 1km failed due to missing files
(SalishSeaCast)

Filed income tax returns and 43ravens GST return.


Thu 25-May-2023
^^^^^^^^^^^^^^^

Updated MOAD & SalishSeaCast docs re: building NEMO on graham and installing command processor
packages.
(MOAD docs)
(SalishSeaCast docs)

UBC-DFO modeling collab mtg;
* Susan re: 201702 to 202108 bathymetry

Raisha submitted proffs of paper.
Group mtg.
(Atlantis)

Squash-merged dependabot PRs to bump tornado to 6.3.2 re: CVE-2023-28370 re: open redirect vulnerability:
* MoaceanParcels
* SalishSeaCast/docs
* UBC-MOAD/docs
* tools
* moad_tools
* Reshapr
* SalishSeaNowcast
* ECget
* SOG-Bloomcast-Ensemble
(repos-maint)

make_ww3_current_file forecast stalled; killed it; re-ran it via launch_remote_worker.
download_weather 00 1km and 12 1km failed due to missing files
(SalishSeaCast)


Fri 26-May-2023
^^^^^^^^^^^^^^^

On to graham session #4.
(MOAD)

Continued work on make_v202111_runoff_file:
* branch: make_v202111_runoff_file
* PR#183
(SalishSeaNowcast)

Sandrine sent email to say that dd.alpha should be fixed.
download_weather 00 1km and 12 1km failed due to missing files.
Sent email to Sandrine to tell her that dd.alpha is not fixed.
(SalishSeaCast)

Prep for listing 2356.


Sat 27-May-2023
^^^^^^^^^^^^^^^

Prep for listing 2356.

make_ww3_current_file forecast stalled; killed it; re-ran it via launch_remote_worker;
download_weather 00 1km and 12 1km failed due to missing files
(SalishSeaCast)

Dinner at Kristin & Kirk's.


Sun 28-May-2023
^^^^^^^^^^^^^^^

Prep for listing 2356.


Week 22
-------

Mon 29-May-2023
^^^^^^^^^^^^^^^

make_ww3_current_file forecast2 stalled; killed it; re-ran it via launch_remote_worker.
make_ww3_current_file forecast stalled; killed it; re-ran it via launch_remote_worker:
* multiple tries from skookum failed; ran make_ww3_current_file on arbutus
(SalishSeaCast)

Continued work on make_v202111_runoff_file:
* branch: make_v202111_runoff_file
* PR#183
(SalishSeaNowcast)


Tue 30-May-2023
^^^^^^^^^^^^^^^

Worked at ESB while Rita was at home.

make_ww3_current_file forecast2 stalled; killed it; re-ran it on arbutus; segfault.
(SalishSeaCast)

Continued work on make_v202111_runoff_file:
* branch: make_v202111_runoff_file
* PR#183
(SalishSeaNowcast)

On-boarding session #1 with Tall.
(MOAD)


Wed 31-May-2023
^^^^^^^^^^^^^^^

Invited Tall to SalishSeaCast and UBC-MOAD orgs on GitHub.
Fixed /data/atall/ and /ocean/atall/ re: sallen group and guid sticky bit;
pinged Henryk re: numeric uid & gid on /ocean/atall/; sent password to Tall.
Helped Cassidy with file downloads from graham re: rsync, scp & sftp.
(MOAD)

Finished work on make_v202111_runoff_file:
* branch: make_v202111_runoff_file
* PR#183; squash-merged
* pulled changes on skookum; restarted manager for new next_workers module to take affect
* ran make_v202111_runoff_file for 30may
Moved launching of ``make_*runoff_file`` workers to ``after_make_live_ocean_files()``:
* branch: move-make_runoff_file
* PR#185
* practical solution to handling race condition among USGS instances of ``collect_river_data``
  that run after ``collect_weather 2.5km 12``
* rsync-ed uncommitted code to skookum for testing; restarted manager for changed next_workers
  module to take effect
(SalishSeaNowcast)


June
====

Thu 1-Jun-2023
^^^^^^^^^^^^^^

upload_forcing forecast2 failed due to no runoff files; discussed with Susan and decided to 
restore make_runoff_file and make_v202111_runoff_file after collect_weather 06, then let them
update the runoff files after collect_weather 12
make_runoff_file failed due to missing b202108 key in ``monthly climatology``
upload_forcing nowcast+ launched immediately from make_live_ocean_files instead of waiting for
grib_to_netcdf to finish, so it faailed
* recovery:
  * hacked make_runoff_file to use only b201702 key in ``monthly climatology``; copied it to
    skookum and re-ran it
  * manually ran upload_forcing nowcast+ to restart automation
(SalishSeaCast)

Continued work on make_v202111_runoff_file:
* branch: make_v202111_runoff_file
* PR#183
Pulled and switched to move-make_runoff_file branch on skookum to test new solution of creating
runoff files after make_ssh_files; restarted manager for changed next_workers
module to take effect.
(SalishSeaNowcast)

Prep for listing 2356.


Fri 2-Jun-2023
^^^^^^^^^^^^^^

make_runoff_file and make_v202111_runoff_file failed to run because I created a loop in the
race condition management; automation for forecast2 resumed when I ran them manually.
make_ww3_wind_file forecast stalled; killed it; re-ran it on arbutus several times before it worked.
(SalishSeaCast)

Continued work on make_v202111_runoff_file:
* branch: make_v202111_runoff_file
* PR#183
* more iterations on how to get make_runoff_file workers properly inserted into automation
(SalishSeaNowcast)

Prep for listing 2356.


Sat 3-Jun-2023
^^^^^^^^^^^^^^

Prep for listing 2356.

make_ww3_current_file forecast2 stalled; killed it; re-ran it on arbutus; also re-ran 
make_ww3_wind_file forecast2: run succeeded
(SalishSeaCast)

Continued work on make_v202111_runoff_file:
* branch: make_v202111_runoff_file
* PR#183
* pulled latest version of branch on skookum for more testing; restarted manager for updated 
  next_workers module to take affect
(SalishSeaNowcast)


Sun 4-Jun-2023
^^^^^^^^^^^^^^

Prep for listing 2356.

Happy hour at new strata.


Week 23
-------

Mon 5-Jun-2023
^^^^^^^^^^^^^^

make_ww3_current_file forecast2 stalled; killed it; re-ran it on arbutus
rsync-ed ``/results/forcing/rivers/R202108Dailies_*y2002m01d28*.nc`` to compute hosts:
* arbutus.cloud
* orcinus
* graham-dtn
* no need to do optimum because Susan ran hindcast there, so she did it
(SalishSeaCast)

Finished work on make_v202111_runoff_file:
* branch: make_v202111_runoff_file
* PR#183: rebase-merged
(SalishSeaNowcast)

Squash-merged dependabot PRs re: updating to cryptography=41.0.1 re: CVE-2023-2650 DoS
vulnerability in OpenSSL:
* SalishSeaNowcast

Phys Ocgy seminar: Birgit on Pb model chapter of her thesis.

Prep for listing 2356.


Tue 6-Jun-2023
^^^^^^^^^^^^^^

Used VSCode ``SalishSeaNowcast [SSH:skookum]`` session to run 
``nowcast.workers.day_month_avgs 2023-05-01`` in ``202111-tarballs`` tmux session on
skookum against dask cluster on salish: 
* 3 FutureWarning per day-avg:
    /SalishSeaCast/Reshapr/reshapr/core/extract.py:929: 
    FutureWarning: Following pandas, the `loffset` parameter to resample will be deprecated 
    in a future version of xarray.  Switch to using time offset arithmetic.
      resampler = extracted_ds.resample(
  created Reshapr issue #82
* successfully created all day-avg and month-avg files without intervention
* very small amount of memory leakage:
  * worker spawner: 5.028g
  * scheduler: 4.711g
  * 4 workers: 0.667g (no change) 
(hindcast)

Squash-merged dependabot PRs re: updating to cryptography=41.0.1 re: CVE-2023-2650 DoS
vulnerability in OpenSSL:
* SalishSeaCmd
* NEMO-Cmd
* SalishSeaCast/docs
* MOAD/docs
* tools/SalishSeaTools
* MoaceanParcels
* AtlantisCmd
* salishsea-site
* NEMO_Nowcast
* Reshapr
* cookiecutter-analysis-repo
* moad_tools
* cookiecutter-MOAD-pypkg
* analysis-doug
* SOG-Bloomcast-Ensemble

Group mtg; see whiteboard.
(MOAD)

make_ww3_current_file forecast stalled; killed it; re-ran it on arbutus
(SalishSeaCast)

Prep for listing 2356.


Wed 7-Jun-2023
^^^^^^^^^^^^^^

make_ww3_wind_file forecast2 stalled; killed it; re-ran it on arbutus
make_ww3_current_file forecast stalled; killed it; re-ran it on arbutus
(SalishSeaCast)

Prep for listing 2356.


Thu 8-Jun-2023
^^^^^^^^^^^^^^

Prep for listing 2356.

Went to ESB for graham session #5.
(MOAD)

make_ww3_current_file forecast stalled; killed it; re-ran it on arbutus
(SalishSeaCast)


Fri 9-Jun-2023
^^^^^^^^^^^^^^

Prep for listing 2356.

Explored adding debug log messages to make_ww3_current_file to try to understand where it is 
getting stuck; discovered that there are no recent debug messages from the worker; restarted
log_aggregator to try to resolve
* dug back in last debug logs to 3jun forecast2 failure:
  * failure occurred in either function that returns xarray.Dataset() or .to_netcdf()
  * added log msg between those calls; copied worker to arbutus to test
(SalishSeaCast)


Sat 10-Jun-2023
^^^^^^^^^^^^^^^

Prep for listing 2356.

make_ww3_current_file forecast2 stalled; killed it; re-ran it on arbutus
Started researching dask config management as possible mitigation.
(SalishSeaCast)


Sun 11-Jun-2023
^^^^^^^^^^^^^^^

Prep for listing 2356.

make_ww3_current_file forecast stalled; killed it; re-ran it on arbutus
(SalishSeaCast)

Experimented with dask ``schedduler="processes"`` and local cluster for make_ww3_current_file;
neither worked properly.
De-nested current components dataset loading from mesh mask reading.
(SalishSeaNowcast)


Week 24
-------

Mon 12-Jun-2023
^^^^^^^^^^^^^^^

Called and emailed Hillcrest plumbing for repair of leaking kitchen faucet.

Squash-merged dependabot PR re: new version of setup-microconda:
* SalishSeaNowcast
* gha-workflows

Investigated KeyError on wind components date in sandheads_winds figure module:
* failing due to no atmostpheric forcing on web since 22-Feb change to rotated lon/lat grid
(SalishSeaNowcast)

nowcast-agrif failed due to no run yesterday; backfill:
  upload_forcing orcinus nowcast+ 2023-06-11
  make_forcing_links orcinus nowcast-agrif 2023-06-11
  wait for run to finish
  make_forcing_links orcinus nowcast-agrif 2023-06-12
(SalishSeaCast)

Prep for listing 2356.

Phys Ocgy seminar:


Tue 13-Jun-2023
^^^^^^^^^^^^^^^

Final prep for 2356 photos; digital nomads in Kits while Rita cleaned, then do pre-showing
checklist, then UBC for afternoon evening to test "live at UBC" scheme.
* Platform 7 for Coffee
* London Drugs and new Gandi's hardware location for TP holder
* library for WiFi

Discussed atmos forcing datasets on ERDDAP with Susan; agreed that HRDPS continental lon/lat grid
needs to be a separate dataset; need to decide if it is v2111 or v2.
Also discussed doing erddap-datasets repo overhaul concurrently:
* initially:
  * split ``datasets.xml`` into 1 file per dataset description
  * add script to assemble dataset descriptions into ``datasets.xml``
* longer term:
  * GitHub Actions workflows:
    * validate dataset descriptions XML - maybe
    * assemble ``datasets.xml`` as build artifact
    * deploy ``datasets.xml`` and ``setup.xml`` to skookum, bracketted by tomcat stop/start
* researched:
  * XML parsing and validation:
    * https://realpython.com/python-xml-parser/
    * schema validation is out, I think, because there is no ERDDAP schema and I don't want to
      create one
    * stdlib xml.etree.ElementTree or lxml (same API) should do the job
      * does success of ElementTree.parse() guarantee well-formed XML?
  * https://github.com/7yl4r/erddap-config-template
  * https://github.com/7yl4r/erddap-datasetsxml-builder
  * mentioned in Mar-2023 ERDDAP list thread: 
      [ERDDAP] Best practices to version control datasets.xml
(ERDDAP)

De-nested wind components dataset loading from mesh mask lons/lats reading in make_ww3_wind_file.
(SalishSeaNowcast)

make_ww3_wind_file forecast stalled; killed it; re-ran it on arbutus
(SalishSeaCast)


Wed 14-Jun-2023
^^^^^^^^^^^^^^^

Worked at ESB while home was in semi-staged state.

make_ww3_wind_file forecast stalled; killed it; re-ran it on arbutus
(SalishSeaCast)

Mtg w/ Tall:
* sorted out issues  in Susan's O2 eval notebook
* fixed miniforge install on char, et al
* fixed VSCode ssh connection timeout value
* got analysis-abdoul env connected in VSCode on char for notebook kernel 

Started work on separating dataset descriptions into files to be composed into
dataset.xml by a script:
* branch: separate-dataset-files
* PR#1
(ERDDAP)


Thu 15-Jun-2023
^^^^^^^^^^^^^^^

Worked at ESB while home was in semi-staged state.

Killed stuck upload_forcing graham-dtn workers from 11may.
Discovered that collect_weather 00 stalled last night
* investigation:
  * missing 4 files, APCP_Sfc from each of hours 7-10
  * files are present on dd.weather.gc.ca
  * no error messages in sarracenia log; appears that messages were never published
* recovery started at ~11:30
    curl files from dd.weather.gc.ca
    kill collect_weather 00
    collect_weather 18 2.5km
    crop_gribs 00 --fcst-date 2023-06-15
    wait for crop_gribs to finish
* files I got from dd.weather.gc.ca were APCP_Sfc, not APCP_Sfc, so crop_gribs failed
  * emailed Sandrine
  * files appeared at ~14:20
  * email from Sandrine at 14:43 confirming that files were ready 
* re-recovery started at ~14:20
    curl files from dd.weather.gc.ca
    crop_gribs 00 --fcst-date 2023-06-15
    wait for crop_gribs to finish
    collect_weather 06 2.5km --backfill
    wait for forecast2 runs to finish; skipped wwatch3-forecast2
    collect_weather 12 2.5km --backfill
* collect_weather 18 stopped for unknown reason, leaving hour 048 in
  /SalishSeaCast/datamart/hrdps-continental/18/048
  * recovery:
      collect_weather 00 2.5km
      download_weather 00 1km
      download_weather 12 1km
      mkdir /results/forcing/atmospheric/continental2.5/GRIB/20230615/18/048
      mv /SalishSeaCast/datamart/hrdps-continental/18/048/* \
        /results/forcing/atmospheric/continental2.5/GRIB/20230615/18/
      crop_gribs 18 --fcst-date 2023-06-15
* crop_gribs 18 failed due to missing 
  18/019/20230615T18Z_MSC_HRDPS_APCP_Sfc_RLatLon0.0225_PT019H.grib2
  * no file on server
  * ignored because we only need hours 005 and 006 for forcing
(SalishSeaCast)

Resigned from EGBC.

Shutdown all of my Google Cloud projects.


Fri 16-Jun-2023
^^^^^^^^^^^^^^^

Haircut.

Worked at ESB while home was in semi-staged state.

Either I forgot to start collect_weather 00 last night, or it failed
* recovery started at ~07:45:
    kill left over collect_weather 12 and 18
    collect_weather 00 --backfill
    kill collect_weather 06
    wait for crop_gribs to finish
    collect_weather 06 --backfill
    kill collect_weather 12
    wait for forecast2 runs to finish
    collect_weather 12 --backfill
grib_to_netcdf failed due to missing 
18/005/20230615T18Z_MSC_HRDPS_PRATE_Sfc_RLatLon0.0225_PT005H_SSC.grib2
* recovery started at ~13:00
    symlinked 20230615T18Z_MSC_HRDPS_APCP_Sfc_RLatLon0.0225_PT019H.grib2 as 
    20230615T18Z_MSC_HRDPS_APCP_Sfc_RLatLon0.0225_PT018H.grib2
    crop_gribs 18 2023-06-15
    grib_to_netcdf nowcast+
(SalishSeaCast)

Scalded left hand.


Sat 17-Jun-2023
^^^^^^^^^^^^^^^

Telcons w/ 811 and on-call doc at Cityview.

Downloaded Minecraft 1.20 mods, shader packs, resource packs, data packs:
* sodium 0.4.10
* lithium 0.11.2
* phosphor is probably N/A for 1.20 due to Mojang lighting engine updates
* malilib 0.16.0
* MiniHUD 0.27.0
* Twekeroo 0.17.0
* Iris 1.6.6
* ComplementaryReimagined 2.2
* ComplementaryShaders 4.7.2
* IronBarsFix-1.20
* LowerShield-1.20
* RedstoneDevices-1.20
  * RedstoneWireFix
  * StickyPistonSides
  * DirectionalDispensersDroppers
  * DirectionalHoppers
  * DirectionalObservers
  * GroovyLevers
    * HopperBottomFix is N/A due to fix by Mojang
* DoubleShulkerShells-1.3.4
Created MultiMC instance:
* Minecraft 1.20.1
* Fabric Loader 0.14.21
Installed mods, shader packs & resource packs in MultiMC 1.20.1 instance.
Copied minihud.json & tweakeroo.json from 1.19.4 config/ to 1.20.1 config/


Sun 18-Jun-2023
^^^^^^^^^^^^^^^

Goofed off and nursed left hand.


Week 25
-------

Mon 19-Jun-2023
^^^^^^^^^^^^^^^

Worked at ESB due to showing 2356; showing rescheduled.

Squash-merged dependabot PR re: mamba-org/setup-micromamba from 1.4.2 to 1.4.3
Dug into test_collect_river_data errors in pytest-with-coverage GHA workflow that were not
appearing in dev env:
* httpx=0.24 changed from custom logging to standard Python logging levels, so it is more
  verbose at the DEBUG and INFO levels
* decided that the messages it provides are worthwhile at the DEBUG level,
  so changed caplog.records index numbers in tests to look at messages from worker that come
  after those from httpx
(SalishSeaNowcast)

Continued work on separating dataset descriptions into files to be composed into
dataset.xml by a script:
* branch: separate-dataset-files
* PR#1
* confirmed that lxml.etree.ElementTree.parse() will parse a dataset fragment
  contained in a <dataset></dataset> tag and raise lxml.etree.XMLSyntaxError 
  exceptions when the XML is not well-formed; so, it can be used for the level of
  XML validation that I had in mind
* added build_datasets_xml.py script
* successfully tested datasets.xml from script for just atmospheric/ubcSSaAtmosphereGridV1.xml
  on skookum
* migrated ubcSSaSurfaceAtmosphereFieldsV1 to atmospheric/ubcSSaSurfaceAtmosphereFieldsV1.xml
* added erddap-datasets repo notifications to #SSC-repos channel with:
    /github subscribe SalishSeaCast/erddap-datasets workflows:{event:"pull_request","push" branch:"main"}
(ERDDAP)


Tue 20-Jun-2023
^^^^^^^^^^^^^^^

Worked at ESB due to open at 2356.

Group mtg; see whiteboard.
(MOAD)

Archived old repos on GitHub to stop weekly dependabot alerts:
* douglatornell/2014-09-25-ubc (SWC workshop)
* douglatornell/python-inflammation-2015-04-30-sfu
* douglatornell/hg-novice-2015-09-22-ubc
* douglatornell/2016-09-20-ubc

Dr. appt; see notes on Slack DM.

One of the drives in the /data RAID failed; Henryk found an identical unit in IT spares, so the failed drive is replaced and parity rebuilding has started; ETA to full restoration is a day or two.


Wed 21-Jun-2023
^^^^^^^^^^^^^^^

Worked at ESB while home was in semi-staged state.

make_ww3_current_file forecast2 stalled; skipped run
make_ww3_current_file forecast stalled due to above; killed forecast2 and re-ran it on arbutus
make_ww3_wind_file forecast stalled; killed it and re-ran it on arbutus
(SalishSeaCast)

Continued work on separating dataset descriptions into files to be composed into
dataset.xml by a script:
* branch: separate-dataset-files
* PR#1
* created check_datasets_xml.py script
* finished migrating atmospheric forcing datasets to datasets/ files
* migrated ONC observations datasets to datasets/ files
(ERDDAP)


Thu 22-Jun-2023
^^^^^^^^^^^^^^^

Dentist appt.

Worked at ESB while home was in semi-staged state.

Talked with Sebastian about his EOAS Research Software Engineer proposal.

Team mtg; discussed story for Raisha's next paper.
(Atlantis)


Fri 23-Jun-2023
^^^^^^^^^^^^^^^

Worked at ESB while home was being shown.

No Neah Bay ssh obs for forecast2 run.
LiveOcean lagged HRDPS 12Z by ~1.75h.
(SalishSeaCast)

Continued work on separating dataset descriptions into files to be composed into
dataset.xml by a script:
* branch: separate-dataset-files
* PR#1
* started migrating bathy & mesh mask datasets to datasets/nemo-grid/
* discovered that infoUrl is a required dataset attribute
* TODO: 
  * Fix source attr URL from Bitbucket to GitHub in ubcSSnBathymetryV17-02
(ERDDAP)


Sat 24-Jun-2023
^^^^^^^^^^^^^^^

Spent the afternoon and evening during open house.


Sun 25-Jun-2023
^^^^^^^^^^^^^^^

Spent the afternoon at ESB during open house.

make_ww3_current_file forecast stalled; killed it and re-ran it on arbutus;
restarted log_aggregator on skookum
(SalishSeaCast)

Updated khawla to PyCharm 2023.1.3.

Did pre-commit autoupdate and other dependency pkg updates:
* SalishSeaCmd
* NEMO-Cmd


Week 26
-------

Mon 26-Jun-2023
^^^^^^^^^^^^^^^

Worked at ESB due to home inspection of 2356.

Phys Ocgy seminar: Jonathan Iszet of IOS on BGC data assimilation in a ROMS model of the
California Current system.

Continued work on separating dataset descriptions into files to be composed into
dataset.xml by a script:
* branch: separate-dataset-files
* PR#1
* finished migrating bathy & mesh mask datasets to datasets/nemo-grid/
* Fixed source attr URL from Bitbucket to GitHub in ubcSSnBathymetryV17-02
* added infoUrl to all migrated datasets
(erddap-datasets)


Tue 27-Jun-2023
^^^^^^^^^^^^^^^

Worked at ESB due to open house.

Group mtg; see whiteboard.
(MOAD)

Continued work on separating dataset descriptions into files to be composed into
dataset.xml by a script:
* branch: separate-dataset-files
* PR#1
* started migrating wwatch3 datasets to datasets/wwatch3/
(erddap-datasets)

Picked up J&L at YVR.


Wed 28-Jun-2023
^^^^^^^^^^^^^^^

2547 posession


Thu 29-Jun-2023
^^^^^^^^^^^^^^^

Birgit's defense.


Fri 30-Jun-2023
^^^^^^^^^^^^^^^

Locker contents to 2547.

make_ww3_wind_file forecast stalled; killed it and re-ran it on arbutus;
restarted log_aggregator on skookum
(SalishSeaCast)


Sat 1-Jul-2023
^^^^^^^^^^^^^^

**Canada Day**

Went to Steeveston Salmon Festival w/ J&L.


Sun 2-Jul-2023
^^^^^^^^^^^^^^

make_ww3_current_file forecast stalled; killed it and re-ran it on arbutus;
restarted log_aggregator on skookum
nowcast-agrif failed due to incomplete 29jun23 run and no no run yesterday; backfill:
  make_forcing_links orcinus nowcast-agrif 2023-06-29
  wait for run to finish
  make_forcing_links orcinus nowcast-agrif 2023-06-30
  wait for run to finish
  make_forcing_links orcinus nowcast-agrif 2023-07-01
(SalishSeaCast)


Week 27
-------

Mon 3-Jul-2023
^^^^^^^^^^^^^^

**Statutory Holiday** - Canada Day lieu day

Finish backfilling nowcast-agrif:
  make_forcing_links orcinus nowcast-agrif 2023-07-02
(SalishSeaCast)


Tue 4-Jul-2023
^^^^^^^^^^^^^^

Took J&L to YVR.

(Group mtg; see whiteboard.
(MOAD))


Wed 5-Jul-2023
^^^^^^^^^^^^^^

download_weather 12 didn't complete; noticved at ~16:30
* investigation:
  * no files in hours 024-030; 4 files in hour 035
  * files are missing from server; sent email to Sandrine; she is on vacation; forwarded message
    to André Giguère, her emergency contact
* recovery started at ~16:40
    kill collect_weather 12
    mv /results/forcing/atmospheric/continental2.5/GRIB/20230705/12 aside
    download_weather 12 2.5km - failed
    collect_weather 18 2.5km --backfill
(SalishSeaCast)


Thu 6-Jul-2023
^^^^^^^^^^^^^^

Worked at ESB for mtgs w/ Becca & Tall.

Mtg w/ Becca re: getting obs from CIOOS:
* scoped a concept for a module to do ERDDAP requests to files from a YAML request file
* TODO:
  * look at erddapy and erddap-python

Emails w/ ECCC re: restoration of missing 5jul 12Z files; eventually they issued alert that
a network issue was causing them trouble
* backfill runs:
    download_live_ocean 2023-07-05 --debug
    make_live_ocean_files 2023-07-05 --debug
    collect_river_data USGS SkagitMountVernon 2023-07-04 --debug
    # fix line order at end of file
    collect_river_data USGS SnohomishMonroe 2023-07-04 --debug
    # fix line order at end of file
    collect_river_data USGS NisquallyMcKenna 2023-07-04 --debug
    # fix line order at end of file
    collect_river_data USGS GreenwaterGreenwater 2023-07-04 --debug
    # fix line order at end of file
    make_turbidity_file --run-date 2023-07-05 --debug
    # failed due to insufficient data
    collect_NeahBay_ssh 06 --data-date 2023-07-05 --debug
    make_ssh_files nowcast --run-date 2023-07-05 --debug
    make_v202111_runoff_file --data-date 2023-07-04 --debug
    make_runoff_file --run-date 2023-07-05 --debug
(SalishSeaCast)

Mtg w/ Tall re: conda envs, cdo, nco, and Reshapr.

Group mtg.
Raisha discovered that whe can use list of Atlantis boxes as selector in dataset.variables[].
(Atlantis)

Explored packaging of Parker's LO/lo_tools w/ Becca; need to figure out how to get it to install
in modern env.


Fri 7-Jul-2023
^^^^^^^^^^^^^^

Still no progress on recovery of 5-Jul HRDPS 12Z files.
(SalishSeaCast)

Forked parkermac/LO to UBC-MOAD/LiveOcean to try to hack lo_tools packaging so that Becca
can install it in a conda env.
* cloned on khawla in MOAD/
* created lo_tools-dev env w/ Python 3.11; got pip=23.1.2 and setuptools=68.0.0
* tried `python3 -m pip install -e lo_tools` and it worked just finished
  * sent msg to Becca to clone Parker's repo and install from there
(MOAD)


Week 28
-------

Mon 10-Jul-2023
^^^^^^^^^^^^^^^

Email from Amadou at MSC saying that 5-Jul files are ready and asking for FTP server to upload
them to; I proposed hpfx; he can't do hpfx, but is trying to get access to a collaboration server
for the transfer; EOAS has no public facing FTP server; I proposed Alliance cluster scratch space
(SalishSeaCast)

Updated dev env.
Did pre-commit autoupdate.
Updated dev, test, docs & user envs to Python 3.11.
Fixed bugs in 202111 model profile.
Tested in preparation for Tall's use.
(Reshapr)


Tue 11-Jul-2023
^^^^^^^^^^^^^^^

Worked at ESB.

Group mtg; see whiteboard.
(MOAD)

Lunch at Perugia w/ Jose.

Received link for tarball of files from ECCC MSC:
* 00Z and 12Z files
* only 10 files per hour:
    APCP_SFC_0
    DLWRF_SFC_0
    DSWRF_SFC_0
    LHTFL_SFC_0
    PRATE_SFC_0
    PRES_SFC_0
    PRMSL_MSL_0
    SPFH_TGL_2
    UGRD_TGL_10
    VGRD_TGL_10
  * missing RH_AGL-2m and TMP_AGL-2m
  * unneeded PRES_SFC_0
  * name differences
* sent email to Amadou
Email from Derek & Jennifer at Port Metro Vancouver re: currents fields dataset not updating.
(SalishSeaCast)

Changed all email addresses in setup.xml from Charles to mine.
(ERDDAP)


Wed 12-Jul-2023
^^^^^^^^^^^^^^^

Rita's first time at 2547.

Received link for new (hopefully correct) tarball from ECCC MSC:
* very slow download; tarball was 305G compared to yesterday's 4.7G; i.e. yesterday's was a Total
  fuck up :-(
* file count and variable names appear to be correct
collect_weather 18 2.5km didn't finish
* missing files in hours 016-018, 020, 022, 023; no error messages in log
* recovery started at ~21:00:
    mv /results/forcing/atmospheric/continental2.5/GRIB/20230712/18 aside
    kill collect_weather 18 2.5km
    download_weather 18 2.5km
    collect_weather 00 2.5km --backfill
(SalishSeaCast)

Continued work on separating dataset descriptions into files to be composed into
dataset.xml by a script:
* branch: separate-dataset-files
* PR#1
* finished migrating wwatch3 datasets to datasets/wwatch3/
* started migrating FVCOM VHFR datasets to datasets/fvcom-vhfr/
(erddap-datasets)


Thu 13-Jul-2023
^^^^^^^^^^^^^^^

Furniture move day.


Fri 14-Jul-2023
^^^^^^^^^^^^^^^

Tried to use latest 5jul HRDPS 12Z tarball from ECCC:
* files are much larger than those downloaded from hpfx, all var files are same size
* Susan gleaned that the files may contain all? levels of atmospheric model
* sent email to Amadou
Started to hack 5jul handling of files we got from hpfx to run nowcast runs only:
* hacked ``weather.download.2.5 km.forecast duration`` config from 48 to 11
* ran ``crop_gribs 12 --fcst-date 2023-07-05 --debug``
* hacked grib_to_netcdf to produce only ``hrdps_y2023m07d05.nc``
* ran ``grib_to_netcdf nowcast+ --run-date 2023-07-05 --debug``
* backfilled 05jul23/nowcast-blue and 05jul23/nowcast-green runs:
    upload_forcing graham-dtn nowcast+ --run-date 2023-07-05 --debug
    upload_forcing optimum-hindcast nowcast+ --run-date 2023-07-05 --debug
    upload_forcing orcinus-nowcast-agrif nowcast+ --run-date 2023-07-05 --debug
    upload_forcing arbutus.cloud-nowcast nowcast+ --run-date 2023-07-05 --debug
    make_forcing_links arbutus.cloud-nowcast nowcast+ --run-date 2023-07-05
    forecast run was unexpectedly successful
    nowcast-green and nowcast-agrif run launches failed due to no date on 
    ``upload_forcing turbidity``
    upload_forcing graham-dtn turbidity --run-date 2023-07-05
    upload_forcing optimum-hindcast turbidity --run-date 2023-07-05
    upload_forcing orcinus-nowcast-agrif turbidity --run-date 2023-07-05
    upload_forcing arbutus.cloud-nowcast turbidity --run-date 2023-07-05
* backfilled 06jul23 runs:
    make_forcing_links arbutus.cloud-nowcast nowcast+ --run-date 2023-07-06
    nowcast-green and nowcast-agrif run launches failed due to no date on 
    ``upload_forcing turbidity``
    upload_forcing graham-dtn turbidity --run-date 2023-07-06
    upload_forcing optimum-hindcast turbidity --run-date 2023-07-06
    upload_forcing orcinus-nowcast-agrif turbidity --run-date 2023-07-06
    upload_forcing arbutus.cloud-nowcast turbidity --run-date 2023-07-06
  * make_ww3_wind_file forecast stalled; killed it and re-ran it on arbutus;
  * restarted log_aggregator on skookum
(SalishSeaCast)

Updated PyCharm on khawla to 2023.1.4.

Got several message from ERDDAP complaining about 
"java.io.IOException: User limit of inotify watches reached"; tried mitigate that as
docs suggest:
  sudo sysctl fs.inotify.max_user_watches=65536
  sudo sysctl fs.inotify.max_user_instances=1024
  sudo sysctl -p
(ERDDAP)


Sat 15-Jul-2023
^^^^^^^^^^^^^^^

Added --run-date arg to upload_forcing turbidity launches in after_watch_NEMO
to remove need for intervention after NEMO forecast run during backfilling;
tested successfully on skookum, committed, pushed & deployed to skookum.
(SalishSeaNowcast)

collect_weather 06 finished without gathering many files; moved dir aside,
and ran download_weather 06 --debug.
Continued backfilling NEMO and wwatch3 runs:
  wait for nowcast-blue to fail at ~10:15
  upload next_workers to skookum re: turbidity run-date
  restart manager to load next_workers changes
  make_forcing_links arbutus.cloud-nowcast nowcast+ --run-date 2023-07-07
  wait for wwatch3/forecast to finish at ~13:45
  clear_checklist
  make_forcing_links arbutus.cloud-nowcast nowcast+ --run-date 2023-07-08
  wait for wwatch3/forecast to finish at ~17:15
  clear_checklist
  make_forcing_links arbutus.cloud-nowcast nowcast+ --run-date 2023-07-09
  * make_ww3_current_file forecast stalled; killed it and re-ran it on arbutus;
  * restarted log_aggregator on skookum
  wait for wwatch3/forecast to finish at ~21:45
  clear_checklist
  make_forcing_links arbutus.cloud-nowcast nowcast+ --run-date 2023-07-10
  * make_ww3_wind_file forecast stalled; killed it and re-ran it
    and make_ww3_current_file on arbutus;
(SalishSeaCast)


Sun 16-Jul-2023
^^^^^^^^^^^^^^^

Continued backfilling NEMO and wwatch3 runs:
  wait for nowcast-blue to fail at ~10:15
  clear_checklist
  make_forcing_links arbutus.cloud-nowcast nowcast+ --run-date 2023-07-11
  wait for wwatch3/forecast to finish at ~14:15
  clear_checklist
  make_forcing_links arbutus.cloud-nowcast nowcast+ --run-date 2023-07-12
  wait for wwatch3/forecast to finish at ~17:30
  clear_checklist
  make_forcing_links arbutus.cloud-nowcast nowcast+ --run-date 2023-07-13
  * make_ww3_wind_file forecast stalled; killed it and re-ran it on arbutus
  wait for wwatch3/forecast to finish at ~22:00
  clear_checklist
  make_forcing_links arbutus.cloud-nowcast nowcast+ --run-date 2023-07-14
(SalishSeaCast)


Week 29
-------

Mon 17-Jul-2023
^^^^^^^^^^^^^^^

forecast2/17jul23 got stuck at 0%; killed it
Finished backfilling NEMO and wwatch3 runs:
  wait for nowcast-blue to fail at ~10:05
  clear_checklist
  make_forcing_links arbutus.cloud-nowcast nowcast+ --run-date 2023-07-15
  * make_ww3_current_file forecast stalled; killed it and re-ran it on arbutus;
    it took 2 tries before it completed
  wait for wwatch3/forecast to finish at ~13:55
  clear_checklist
  make_forcing_links arbutus.cloud-nowcast nowcast+ --run-date 2023-07-16
  wait for wwatch3/forecast to finish at ~17:30
  clear_checklist
  make_forcing_links arbutus.cloud-nowcast nowcast+ --run-date 2023-07-17
  * make_ww3_current_file forecast stalled; killed it and re-ran it on arbutus;
    it took 2 tries before it completed
(SalishSeaCast)

Email w/ Rachael re: vessel track stitching script; not in a Git repo to my knowledge.
(MIDOSS)

Squash-merged dependabot PRs to update cryptography re: CVE-2023-38325 re: 
mishandling creation and parseing of SSH certificates that have critical options:
* SalishSeaCmd
* NEMO_Nowcast
* SalishSeaCast/docs
* salishsea-site
* MOAD/docs
* MoaceanParcels
* SalishSeaTools
* moad_tools
* AtlantisCmd
* cookiecutter-analysis-repo
* cookiecutter-MOAD-pypkg
* SalishSeaNowcast
* NEMO-Cmd
Squash-merged dependabot PR to update SciPy in MoaceanParcels re: CVE-2023-25399
re: recounting issue that leads to potential memory leak.


Tue 18-Jul-2023
^^^^^^^^^^^^^^^

Worked at ESB.

Got latest tarball from ECCC MSC:
* 1.2G, ~36 min download
* initial check of variables and file sizes looks good
* files need to be renamed to match published names - done
* crop_gribs worked
* grib_to_netcdf worked
Emailed Derek @ Port Metro Vancouver to let him know that SalishSeaCast is back to real-time;
he's away until 1-Aug
make_ww3_current_file forecast stalled; killed it and re-ran it on arbutus
Got nowcast-dev running again:
  copy nowcast-green/17jul23 namelist_cfg and restart to nowcast-dev.201905/17jul23/
  make_forcing_links salish nowcast+ --shared-storage
(SalishSeaCast)

Group mtg; see whiteboard.
Discussed obs collection w/ Cassidy; very similar needs to Becca's.
(MOAD)

Helped Raisha start thinking about running Parcels from a Python module instead of from a notebook
as she scales up the number of particles she is running.
(Atlantis)


Wed 19-Jul-2023
^^^^^^^^^^^^^^^

Modo van for big items move from 2356.

download_live_ocean failed; re-ran at ~15:35
(SalishSeaCast)


Thu 20-Jul-2023
^^^^^^^^^^^^^^^

Squash-merged dependabot PRs to update pygments re: CVE-2022-40896 re: ReDOS issue:
* SalishSeaTools
* salishsea-site
* NEMO_Nowcast
* gha-workflows
* moad_tools
* MOAD/docs
* AtlantisCmd
* MoaceanParcels
* NEMO-Cmd

Explored changing crop_gribs worker to use watchdog file system monitor to operate on
files as they are moved into the /results/forcing/atmospheric/continental2.5/GRIB/{yyyymmdd}/{hh}/
directory:
branch: faster-crop_gribs
PR#: 
(SalishSeaNowcast)

Helped Tall explore Puget Sound dissolved O2 observations:
* analysis-doug/notebooks/puget_O2/
* accessed and plotted profile from obs dataset via xarray
Discussed alternative to find_nearest_model_point() with Susan:
* do ``method="nearest"`` lookups in ``grid/grid_from_lat_lon_mask999.nc``;
  see code in ``salishsea_tools.geo_tools.get_ij_coordinates()``, but don't use that
  function as it opens the file for each lookup

download_weather 00|12 1km failed due to bad TLS cert on dd.alpha.
Sent email to Sandrine.
Re-tried with --no-verify-certs; failed with 404 errors.
(SalishSeaCast)


Fri 21-Jul-2023
^^^^^^^^^^^^^^^

Email from Sandrine to day that dd.alpha cert issue had been resolved; it has not:
* sent her a screenshot
* fixed by 11:30; 20jul 00Z files were gone, but got 20jul 12Z
* Sandrine said to use dd.alpha.weather.gc.ca as an alternative to dd.alpha.meteo.gc.ca
make_ww3_current_file forecast2 stalled; killed it and re-ran it on arbutus.
make_ww3_current_file forecast stalled; killed it and re-ran it on arbutus.
(SalishSeaCast)

M&J arrived, then drove to White Rock and back to bring JRA.


Sat 22-Jul-2023
^^^^^^^^^^^^^^^

M&J left for Van Isle & Heart Isle.
JRA visiting.


Sun 23-Jul-2023
^^^^^^^^^^^^^^^

make_ww3_wind_file forecast2 stalled; killed it
(SalishSeaCast)

Drove JRA back to White Rock and had dinner at Amica.


Week 30
-------

Mon 24-Jul-2023
^^^^^^^^^^^^^^^

First rain since 13-Jun.

crop_gribs 00 failed due to bad file:
  /results/forcing/atmospheric/continental2.5/GRIB/20230724/00/040/20230724T00Z_MSC_HRDPS_APCP_Sfc_RLatLon0.0225_PT040H.grib2
grib_to_netcdf nowcast+ failed as a result; cascaded to upload_forcing failures
* recovery started at ~10:45:
  * downloaded 20230724T00Z_MSC_HRDPS_APCP_Sfc_RLatLon0.0225_PT040H.grib2 again; got a different
    size
  crop_gribs 00 --debug
    * new 20230724T00Z_MSC_HRDPS_APCP_Sfc_RLatLon0.0225_PT040H.grib2 was successfully processed
  grib_to_netcdf nowcast+
  upload_forcing graham-dtn nowcast+ --run-date 2023-07-24
  upload_forcing optimum-hindcast nowcast+ --run-date 2023-07-24
  upload_forcing orcinus-nowcast-agrif nowcast+ --run-date 2023-07-24
  upload_forcing arbutus.cloud-nowcast nowcast+ --run-date 2023-07-24
(SalishSeaCast)

AAPS 2022 Tentative Agreement Information Session
* health account increasing from $200 to $400 per year
* personal spending account: $200 per year

Helped Tall explore Puget Sound dissolved O2 observations:
* analysis-doug/notebooks/puget_O2/
* added locating nearest model grid point to obs cast, and accessing and plotting
  model results profile from that point
Helped Matt sort out using Git in VSCode; his workspace was at the MOAD/ level.

Squash-merged dependabot PR re: update to apple-boy/ssh-action that I use for deployment.
(salishsea-site)


Tue 25-Jul-2023
^^^^^^^^^^^^^^^

Waited at home until Rita arrived, then worked at ESB.

Group mtg; see whiteboard.
(MOAD)

upload_forcing to graham-dtn failed due to scheduled maintenance
(SalishSeaCast)

Helped Becca get ariane built on perigee:
* key was to include gfortran in her conda env so that it was consistent with
  libnetcdf and netcdf-fortran from conda-forge

Discussed skookum RAM upgrade w/ Henryk.

Talked to Tall about next steps:
* need to get Reshapr working for him to pull profiles from NEMO to compare to obs profiles

Updated nodecraft server to 1.20.1:
* stopped server
* locked Turgent Falcon's Punching Fist backup of 2023-07-21 10:52
* used 1 click installer to change version from 1.19.4 w/ fabric 1.19-0.14.19 to
  1.20.1 w/ fabric 1.20.1-0.14.21 via archive method
* copied files from _old_files/2023-07-26T02-57-18-191Z/ to /:
    banned-ips.json
    banned-players.json
    eula.txt
    ops.json
    server.properties
    whitelist.json
* created new world:
  * name: 1020-1-25jul23
  * seed: 3266812394423525333
  * difficulty: normal
* server started successfully
* uploaded to /1-20-1-25jul23/datapacks:
    DoubleShulkerShells-1.3.4
* uploaded to /mods/
    lithium-fabric-mc1.20.1-0.11.2.jar 
* restarted server


Wed 26-Jul-2023
^^^^^^^^^^^^^^^

make_ww3_current_file forecast2 stalled; killed it
(SalishSeaCast)

Housewares shopping, car load to Salvation Army, car load from 2356.

K&K for dinner and fireworks; Mexico better than Australia.


Thu 27-Jul-2023
^^^^^^^^^^^^^^^

collect_weather 06 didn't complete; perhaps due to ocean YP server issue since ~02:30
* all files for hours 001-023 collected; none after that, though sarracenia log shows them arriving
* was able to connect to skookum at ~17:40; started recovery
    kill collect_weather 06
    move /results/forcing/atmospheric/continental2.5/GRIB/20230727/06/ aside
    download_weather 06 2.5km
    collect_weather 00 2.5km
    wait for forecast2 runs to finish
      make_ww3_current_file got stuck; killed it
    collect_weather 12 2.5km --backfill
    collect_weather 18 2.5km --backfill
backfill upload_forcing to graham-dtn:
  upload_forcing nowcast+ graham-dtn 2023-07-25
  upload_forcing turbidity graham-dtn 2023-07-25
  upload_forcing nowcast+ graham-dtn 2023-07-26
  upload_forcing turbidity graham-dtn 2023-07-26
upload_forcing nowcast+ instances didn't launch after grib_to_netcdf 12; launched 4 instances manually at ~22:10
(SalishSeaCast)

Email from Henryk at ~10:15 says ETA for ocean auth fix is unknown.

Squash-merged dependabot PRs to update certifi re: CVE-2023-37920 re: dropping
root certs from "e-Turga" due to Mozilla finding security issues in their system:
* analysis-doug/dask-expts
* analysis-doug/melanie-geotiff
* SalishSeaCmd
* NEMO-Cmd
* SalishSeaNowcast
* Reshapr
* salishsea-site
* SalishSeaCast/docs
* MoaceanParcels
* AtlantisCmd
* moad_tools
* UBC-MOAD/docs
* cookiecutter-MOAD-pypkg
* NEMO_Nowcast
* tools
* cookiecutter-analysis-repo

Squash-merged dependabot PRs to update pygments re: CVE-2022-40896 re: ReDOS issue:
* analysis-doug/dask-expts
* analysis-doug/melanie-geotiff

Squash-merged dependabot PRs to update cryptography re: CVE-2023-38325 re: 
mishandling creation and parseing of SSH certificates that have critical options:
* analysis-doug/dask-expts
* analysis-doug/melanie-geotiff

Squash-merged dependabot PR to update SciPy re: CVE-2023-25399 re: recounting issue 
that leads to potential memory leak:
* analysis-doug/dask-expts
* analysis-doug/melanie-geotiff

Dropped requirements.txt files from analysis-doug to avoid unecessary dependabot PRs.

Ran:
  python3 /media/doug/warehouse/MOAD/gha-workflows/gha_workflow_checker/gha_workflows_checker.py

Continued work on separating dataset descriptions into files to be composed into
dataset.xml by a script:
* branch: separate-dataset-files
* PR#1
* finished migrating FVCOM VHFR datasets to datasets/fvcom-vhfr/
* migrated 2nd Narrows railway bridge HADCP dataset to datasets/2ndNarrowsHADCP-observations/
(erddap-datasets)


Fri 28-Jul-2023
^^^^^^^^^^^^^^^

Recovery from yesterday's EOAS auth system outage was not entirely successful:
* ``make_forcing_links forecast --shared-storage`` failed due to running after midnight;
  so nowcast-dev run failed
* collect_river_data failed with KeyError for 2023-07-27
  * /SalishSeaCast/datamart/hydrometric/ files have not been updated since 26jul 13:35
  * sarracenia log show queue binding failure due to permission issue at ~13:46
recovery started at ~08:35:
  * restarted sr_subscribe-hydrometric via supervisorctl
  * wait for sarracenia to update river discharge csv files
  /results/forcing/rivers/observations/collect_river_data.sh
  make_runoff_file  
  make_v202111_runoff_file
Backfill nowcast-dev:
  wait for 28jul to fail
  make_forcing_links salish nowcast+ --shared-storage 2023-07-27
  wait for run to finish at ~19:15
  make_forcing_links salish nowcast+ --shared-storage 2023-07-28
(SalishSeaCast)

Quarterbacked recovery of waterhole machines after yesterday's EOAS auth outage:
* reboots needed: lox, char
* no problems: salish, skookum, smelt, hake, chum

Continued work on changing crop_gribs worker to use watchdog file system monitor to operate on
files as they are moved into the /results/forcing/atmospheric/continental2.5/GRIB/{yyyymmdd}/{hh}/
directory:
branch: faster-crop_gribs
PR#: 
(SalishSeaNowcast)


Sat 29-Jul-2023
^^^^^^^^^^^^^^^

Continued work on changing crop_gribs worker to use watchdog file system monitor to operate on
files as they are moved into the /results/forcing/atmospheric/continental2.5/GRIB/{yyyymmdd}/{hh}/
directory:
branch: faster-crop_gribs
PR#: 191
* hacked next_workers enough to allow test to proceed for 18Z forecast today
* updated skookum to faster-crop_gribs branch
* restarted manager to load next_workers module
* manually launched ``crop_gribs 18``; no file system events were detected
* reverted to main branch; restarted manager; manually launched ``crop_gribs 18``
(SalishSeaNowcast)


Sun 30-Jul-2023
^^^^^^^^^^^^^^^

make_ww3_wind_file forecast2 stalled; killed it
Noticed that yesterday's make_ww3_current_file forecast stalled; killed it
Backfill wwatch3:
  wait for forecast run to finish
  make_ww3_wind_file forecast 2023-07-29
  make_ww3_current_file forecast 2023-07-29
  wait for forecast run to finish
  make_ww3_wind_file forecast 2023-07-30
  make_ww3_current_file forecast 2023-07-30
(SalishSeaCast)


Week 31
-------

Mon 31-Jul-2023
^^^^^^^^^^^^^^^

NEMO forecast2 failed overnight; Susan investigated: 1st time step, high velocity components
on western boundary; may not affect nowcast runs because they are initialized from 
yesterday's nowcast-green restart file, whereas forecast2 is initialized from a restart file
generated part way through the forecast run.
No 18Z messages in sarracenia log; warning & error at 10:38:
  2023-07-31 10:38:44,016 [WARNING] sr_amqp/consume: could not consume in queue q_anonymous.sr_subscribe.hrdps-continental-dd-weather.UBC.SalishSeaCast: EOF occurred in violation of protocol (_ssl.c:2393)
  2023-07-31 10:38:44,198 [ERROR] sr_amqp/close 2: [SSL: BAD_LENGTH] bad length (_ssl.c:2393)
* recovery started at ~15:56
    killed collect_weather 18
    download_weather 18 2.5km
    * slower than ususal: 20 hours in ~2h
    restarted sr_subscribe-hrdps-continental via supervisorctl
    collect_weather 00 2.5km
    download_weather 00 1km
    download_weather 12 1km
Checked hydrometric feed in sarracenia:
* last update was ~13:06
* restarted client via supervisorctl at 16:18
(SalishSeaCast)

Jumped in to kill dask processes to prevent swapping on salish; Camryn was running 6 ariane jobs
using ~30G each; discussed limits with her on Slack.

Used VSCode ``SalishSeaNowcast [SSH:skookum]`` session to run 
``nowcast.workers.day_month_avgs 2023-06-01`` in ``202111-tarballs`` tmux session on
skookum against dask cluster on salish: 
* 3 FutureWarning per day-avg:
    /SalishSeaCast/Reshapr/reshapr/core/extract.py:929: 
    FutureWarning: Following pandas, the `loffset` parameter to resample will be deprecated 
    in a future version of xarray.  Switch to using time offset arithmetic.
      resampler = extracted_ds.resample(
  see Reshapr issue #82
* successfully created all day-avg and month-avg files
  * failure:
    * 2jul chemistry
      * Used VSCode ``month-avg.202111 /results2/SalishSea [SSH: salish]`` session to run
        ``python3 -m day_avg 2023-06-02 chemistry`` in ``/results2/SalishSea/month-avg.202111/``
        on salish
* very small amount of memory leakage:
  * worker spawner: 5.025g
  * scheduler: 4.697g
  * 4 workers: 0.675g
(hindcast)

Ran 12-month extraction for O2 profiles at Twanoh for Tall; no errors like happened on Friday;
17.7 minutes.
Merged PR#87 re: georef variables names.
Slack conversation w/ Tall; plan to meet on Friday.
(Reshapr)

Tried to test concurrent crop_gribs in PyCharm debugger on khawla; revealed that 18Z files were
not appearing in sarracenia client (see above).
(SalishSeaNowcast)

Slack converation w/ Jose re: running Parcels on graham.
Realized that he needs nowcast-green.202111 and wwatch3 files there:
* Ran rsync to upload wwatch3/nowcast/*19/SoG_ww3_fields_2019*_2019*_*.nc files
* Ran rsync to upload nowcast-green.202111/*19/SalishSea_1d_*_prod_T.nc files
* Ran rsync to upload nowcast-green.202111/*19/SalishSea_1d_*_grid_[TUVW].nc files


August
======

Tue 1-Aug-2023
^^^^^^^^^^^^^^

make_ww3_wind_file forecast2 stalled; killed it, then re-ran it manually, took 2 tries.
(SalishSeaCast)

PyCharm 2023.2 livestream:
* Helen Scott, Jodie Burchell, Paul Everitt, Aleksei Kniazev
* lots of Django:
  * endpoints discovery; endpoints are symbols so operations work across Python & JS
* black integration; on save, or via code reformat <--
  * need a "stationary" black installation
  * will collect settings from pyproject.toml
  * pyproject.yaml integration
* GitLab merge request integration
  * similar to GitHub pull request integration
* "Run Anything"
  * like "Search Anywhere" (Shift-Shift)
  * keyboard shortcut is Ctrl-Ctrl
  * select in terminal window, then shortcut
  * creates temporary run configurations (like temporary test configs)
  * platform feature from Intelli-J
  * hold down shift to change from run to debug
* new UI
  * change project colour
  * sidebar/toolbar configurability
* AI assistant
  * pro only, limited pre-release
  * write function docstrings
  * function and variable name suggestions via refactoring
  * write commit messages - via analysis of diff
  * explain commits - via analysis of diff
  * writing is verbose because it's a large language model
  * explain code
  * refactor code
  * generate code from description
  * write unit tests
  * mixture of local LLMs and ChatGPT
  * most functionality working in Jupyter notebooks
  * access to preview
    * install PyCharm AI Assistant plug-in
    * limited beta - want feedback via YouTrack
  * OpenAI products
  * pricing to be determined
* polars data frames
  * polars is higher performance pandas
  * post next week on DataCells (?) blog
  * works with plotly
* collapse type hindcast
* type hints help AI assistant
* indexing improvements
  * CLI tool to generate shared indexes to share with teams
* better support for pytest fixtures
* Python packages GUI
  * click to update; auto-updates requirements.txt
* use EAP releases

Updated to PyCharm 2023.2 on khawla.
Signed in to AI Assistant beta, I think.

Group mtg; see whiteboard.
(MOAD)

Met w/ Camryn re: top, memory, processing, etc.

Met w/ Jose re: running Parcels as MPI jobs on graham.

Squash-merged some dependabot PRs from weekly email alert; they didn't generate notifications
for some reason:
* SOG-Bloomcast-Ensemble: cryptography, pygments, certifi
* NEMO-Cmd: requests, GitPython, future, cryptography
* FVCOM-Cmd: 


Wed 2-Aug-2023
^^^^^^^^^^^^^^

make_ww3_wind_file forecast stalled; killed it, then re-ran it manually.
(SalishSeaCast)

Squash-merged more dependabot PRs from weekly email alert; they didn't generate notifications
for some reason:
* FVCOM-Cmd: requests, pygments
* rpn-to-gemlam: cryptography, requests, pygments, scipy, tornado, certifi
* SOG: pygments
  * dismissed security alert re: colander because the vulnerability is in URL parsing that we don't
    use
* SOG-Bloomcast: pygments
Squash-merged dependabot PRs re: statically linked version of OpenSSL in cryptography:
* SalishSeaCmd
* SalishSeaNowcast
* SalishSeaCast/docs
* tools
* cookiecutter-MOAD-pypkg
* MoaceanParcels
* NEMO_Nowcast
* moad_tools
* UBC-MOAD/docs
* AtlantisCmd
* cookiecutter-analysis-repo

Updated requirements.txt to drop py and bump pytest to re: security alert from 
18-Oct-2022:
* FVCOM-Cmd
* rpn-to-gemlam
* SOG
* SOG-forcing
* SOG-Bloomcast


Thu 3-Aug-2023
^^^^^^^^^^^^^^

make_ww3_current_file forecast2 stalled; killed it, then re-ran it manually.
make_ww3_wind_file forecast2 stalled; killed it, then re-ran it manually.
make_ww3_wind_file forecast stalled; killed it, then re-ran it manually; also had to run
make_ww3_current_file manually to get run started.
(SalishSeaCast)

Continued work on changing crop_gribs worker to use watchdog file system monitor to operate on
files as they are moved into the /results/forcing/atmospheric/continental2.5/GRIB/{yyyymmdd}/{hh}/
directory:
branch: faster-crop_gribs
PR#: 191
* discovered that files are being copied into /results/forcing/atmospheric/... directories,
  so file system events are create, multiple modify, close
* changed crop_gribs to detect on_closed event
* updated skookum to faster-crop_gribs branch
* restarted manager to load next_workers module
* manually launched ``crop_gribs 18`` - worked!!! :-)
* ``collect_weather 00`` and ``crop_gribs 00 2023-08-04`` launched correctly
* ``crop_gribs 00 2023-08-04`` finished its work, but didn't terminate; killed manuallly :-(
(SalishSeaNowcast)


Fri 4-Aug-2023
^^^^^^^^^^^^^^

Continued work on changing crop_gribs worker to use watchdog file system monitor to operate on
files as they are moved into the /results/forcing/atmospheric/continental2.5/GRIB/{yyyymmdd}/{hh}/
directory:
branch: faster-crop_gribs
PR#: 191
* ``collect_weather 06`` launched correctly but ``crop_gribs 06`` was looking for 2023-08-03 because
  it was launched before midnight
  * killed it
  * reverted to main branch; ran ``crop_gribs 06`` manually
  * changed back to faster-crop_gribs branch
* ``collect_weather 12`` and ``crop_gribs 12`` launched correctly, and worked as expected;
  nowcast-blue run started 65 seconds after they finished rather than >1h :-)
* added forecast date arg to ``crop_gribs 06`` launch because it gets launched before midnight
* ``collect_weather 18`` and ``crop_gribs 18`` launched correctly, and worked as expected
* ``collect_weather 00`` and ``crop_gribs 00 2023-08-05`` launched correctly
(SalishSeaNowcast)

make_ww3_wind_file forecast stalled; killed it, then re-ran it manually; also had to run
make_ww3_current_file manually to get run started.
restarted log_aggregator because there were no messages from ww3 workers.
(SalishSeaCast)

Met w/ Tall to orient him to using Reshapr.


Sat 5-Aug-2023
^^^^^^^^^^^^^^

Finished pack-up of 2356.


Sun 6-Aug-2023
^^^^^^^^^^^^^^

crop_gribs 12 stalled with the observer thread reporting 1 file remaining to process,
but all files show as cropped
* recovery started at ~10:40:
    killed crop_gribs 12
    * maybe there's a signal other than INT that will look like completion to manager?
    grib_to_netcdf nowcast+
    * failed due to no 12/023/20230806T12Z_MSC_HRDPS_APCP_Sfc_RLatLon0.0225_PT023H_SSC.grib2
    * upload_forcing, etc. went ahead due to race condition mgmt not caring about failure
    * recovery:
        hacked crop_gribs and nowcast.yaml on main branch to process only hour 23 APCP file
        crop_gribs 12 --debug
        reverted hacks
        grib_to_netcdf nowcast+ --debug
        forecast stalled at 84.7%, presumably due to messed up atmospheric forcing
        * re-ran upload_forcing nowcast+ to restart automation
(SalishSeaNowcast)


Week 32
-------

Mon 7-Aug-2023
^^^^^^^^^^^^^^

**Statutory Holiday** - BC Day

make_ww3_current_file forecast2 stalled; killed it, skipped run.
crop_gribs 18 stalled with 1 file remaining to be processed:
  20230807T18Z_MSC_HRDPS_DLWRF_Sfc_RLatLon0.0225_PT038H.grib2
  * recovery:
      killed crop_gribs 18
      hacked crop_gribs and nowcast.yaml on main branch to process only hour 38 DLWRF file
      crop_gribs 18 --debug
      reverted hacks
(SalishSeaCast)

Shuffled stuff in the garage enough to get a bike work space and preliminary tool storage.

Cleaned up network wiring panel.


Tue 8-Aug-2023
^^^^^^^^^^^^^^

Worked at ESB while Rita was at home.

Group mtg; see whiteboard.
(MOAD)

skookum memory upgrade:
* 16G to 128G
* Henryk did the work
* scheduled for 15:00
* prep:
  * kill collect_weather 18
  * kill crop_gribs 18
  * stop SalishSeaCast supervisord
      supervisorctl -c /SalishSeaCast/SalishSeaNowcast/config/supervisord.ini shutdown
  * stop salishsea-site supervisord
      supervisorctl -c /SalishSeaCast/salishsea-site/supervisord-prod.ini shutdown
  * stop ERDDAP
      sudo /opt/tomcat/bin/shutdown.sh
  * stop apache2
      sudo systemctl stop apache2.service
* recovery:
  * apache2 started on boot
  * start ERDDAP
      sudo /opt/tomcat/bin/startup.sh
  * start salishsea-site supervisord
      conda activate /SalishSeaCast/salishsea-site-env
      supervisord -c /SalishSeaCast/salishsea-site/supervisord-prod.ini
  * start SalishSeaCast supervisord
      conda activate /SalishSeaCast/salishsea-site-env
      supervisord -c /SalishSeaCast/SalishSeaNowcast/config/supervisord.ini
  * crop_gribs 18
  * download_weather 18 2.5km
    * crop_gribs is not processing files:
      * because I forgot to delete the empty 18/ directory, so download_weather failed
        and crop_gribs was left watching a on existent directory
  * download_weather 00 1km
  * download_weather 12 1km
  * crop_gribs 00 2023-08-09
  * collect_weather 00 2.5 km
  * crop_gribs 18
(SalishSeaNowcast)


Wed 9-Aug-2023
^^^^^^^^^^^^^^

Tagged batch-crop_gribs on main to use for recovery from collect_weather and/or crop_gribs
problems untile file-on-demand feature is implemented in crop_gribs, and backfill feature is
implemented in download_weather.
Finished work on changing crop_gribs worker to use watchdog file system monitor to operate on
files as they are moved into the /results/forcing/atmospheric/continental2.5/GRIB/{yyyymmdd}/{hh}/
directory:
branch: faster-crop_gribs
PR#: 191 - squash-merged
* update process flow diagram
(SalishSeaNowcast)

ERDDAP was reporting ``java.io.IOException: User limit of inotify watches reached`` errors;
followed suggestions on https://coastwatch.pfeg.noaa.gov/erddap/download/setupDatasetsXml.html:
  sudo sysctl fs.inotify.max_user_watches=65536
  sudo sysctl fs.inotify.max_user_instances=1024
  sudo sysctl -p
ERDDAP was also reporting 
``java.lang.OutOfMemoryError: Ran out of memory trying to read HDF5 filtered chunk. Either increase 
the JVM's heap size (use the -Xmx switch) or reduce the size of the dataset's chunks`` errors:
  * changed Java heap memory settings in /opt/tomcat/bin/startup.sh to:
    -Xmx=48G -Xms=16G  # heap size limit, initial heap size
  * restarted ERDDAP
    * no inotify messages
    * OutOfMemoryError on same sets of files
  * increased Xmx to 64G:
    * same OutOfMemoryError messages in email
  * increased Xmx to 96G:
    * same OutOfMemoryError messages in email
(ERDDAP)


Thu 10-Aug-2023
^^^^^^^^^^^^^^^

crop_gribs 06 stalled with 1 file remaining to be processed:
* bash for loop doesn't reveal which file
* grib_to_netcdf forecast2 --debug to try to find it; successs, so not in 06Z hours 017 to 048;
  hours 001 to 016 of 06Z are not required for grib_to_netcdf nowcast+, so decided no to worry
* grib_to_netcdf forecast2 to restart automation at ~07:55
* killed crop_gribs 06
make_ww3_wind_file and make_ww3_current_file both stalled; killed them, and skipped runs to avoid
conflict with soon-to-start nowcast-blue run
(SalishSeaNowcast)

Vancouver to Heart Island


Fri 11-Aug-2023
^^^^^^^^^^^^^^^

Heart Island

forecast2 runs failed due to no nowcast key in checklist; skipped runs
crop_gribs 12 stalled with 1 file remaining to process:
  20230811T12Z_MSC_HRDPS_APCP_Sfc_RLatLon0.0225_PT028H.grib2
  * recovery started at ~11:55:
      git checkout batch-crop_gribs  # on skookum and khawla; detached head mode
      hacked crop_gribs and nowcast.yaml on khawla to process only hour 28 APCP file
      copied hacks to skookum
      crop_gribs 12 --debug
      reverted hacks on skookum
        git restore config/nowcast.yaml nowcast/workers/crop_gribs.py
        git checkout main
      grib_to_netcdf nowcast+

      killed crop_gribs 12
      reverted hacks on khawla
download_live_ocean timed out at 11:46; re-ran at ~12:15
(SalishSeaNowcast)

Started work on crop_gribs feature to process a specific file; motivation is to handle
stall condition with 1 file remaining to process that happens to frequently
branch: crop_gribs-one-file
(SalishSeaCast)


Sat 12-Aug-2023
^^^^^^^^^^^^^^^

Heart Island

Hiked trail from Nick & Jana's to lake on Hunter Island; visited Nick & Jana, then dinner
with them at Heart Island.

make_ww3_current_file forecast stalled; killed it and re-ran it.
(SalishSeaCast)


Sun 13-Aug-2023
^^^^^^^^^^^^^^^

Heart Island

Installed Rapid Photo Downloader on khawla from PopShop.

make_ww3_wind_file forecast stalled; killed it and re-ran it.
(SalishSeaCast)


Week 33
-------

Mon 14-Aug-2023
^^^^^^^^^^^^^^^

Heart Island

Continued work on crop_gribs feature to process a specific file; motivation is to handle
stall condition with 1 file remaining to process that happens to frequently
branch: crop_gribs-one-file
PR#195
(SalishSeaCast)


Tue 15-Aug-2023
^^^^^^^^^^^^^^^

Heart Island

Continued work on crop_gribs feature to process a specific file; motivation is to handle
stall condition with 1 file remaining to process that happens to frequently
branch: crop_gribs-one-file
PR#195
(SalishSeaCast)

make_ww3_current_file forecast stalled; killed it and re-ran it.
(SalishSeaCast)


Wed 16-Aug-2023
^^^^^^^^^^^^^^^

Heart Island

Went to Shearwater and Bella Bella to pick up James from airport.


Thu 17-Aug-2023
^^^^^^^^^^^^^^^

Heart Island

no NeahBay obs or forecast for forecast2 or nowcast:
* Susan emailed NOAA to enquire
  * reply said that changes upstream mean that scripts need to changed; ETA a few days
* recovery started at ~10:30:
    skipped forecast2 runs
    symlinked 16 fcst at 16 obs
    symlinked 19 fcst as 20 fcst
    make_v202111_runoff_file
    make_runoff_file
(SalishSeaCast)


Fri 18-Aug-2023
^^^^^^^^^^^^^^^

Heart Island

no NeahBay obs or forecast for forecast2 or nowcast:
* recovery started at ~10:15:
    skipped forecast2 runs
    clear_checklist
    symlinked 17 fcst at 17 obs
    symlinked 19 fcst as 20 fcst
    make_v202111_runoff_file
    make_runoff_file
* Susan got reply from NOAA with service announcement of 1 letter change in URL
  due to model upgrade; she hacked it into nowcast.yaml on skookum for testing tomorrow
* tested new URL starting at ~16:20
    delete symlinks
    collect_NeahBay_ssh 00 2023-08-17 --debug  # failed
      new files are .csv.tar.gz rather than .csv_tar; new are larger than old; Susan investigated:
      * the file we are interested in within the tarball appears to be the same
      * change config to store file as .csv_tar_gz; tarfile module handles gz compression 
        transparetnly; need underscores instead of dots to be able to use Path.with_suffix()
        without code changes
    collect_NeahBay_ssh 00 2023-08-17 --debug  # success
    make_ssh_files forecast2 2023-08-17 --debug  # success
    collect_NeahBay_ssh 06 2023-08-17 --debug  # success
    make_ssh_files nowcast 2023-08-17 --debug  # success
    collect_NeahBay_ssh 00 2023-08-18 --debug  # success
    make_ssh_files forecast2 2023-08-18 --debug  # success
    collect_NeahBay_ssh 06 2023-08-18 --debug  # success
    make_ssh_files nowcast 2023-08-18 --debug  # success
* Created PR#196 for changes.
crop_gribs 18 left 1 file uncropped:
  20230818T18Z_MSC_HRDPS_PRATE_Sfc_RLatLon0.0225_PT001H.grib2
  * tested crop_gribs-one_file code
      crop_gribs 18 PRATE_Sfc 1 --debug  # worked
      crop_gribs 18 PRATE_Sfc 1  # worked
  * squash-merged PR#195
(SalishSeaCast)

Squash-merged PR#195 after successful test of crop_gribs-one-file branch.
Created PR#196 for update-NeahBay-ssh-url branch.
(SalishSeaNowcast)


Sat 19-Aug-2023
^^^^^^^^^^^^^^^

Heart Island

collect_NeahBay_ssh worked for forecast2 and nowcast
make_ww3_current_file forecast2 stalled; killed and skipped run
crop_gribs 12 left 1 file uncropped: 20230819T12Z_MSC_HRDPS_APCP_Sfc_RLatLon0.0225_PT031H.grib2
  crop_gribs 12 APCP_Sfc 31  # restarted automation
  kill crop_gribs 12
(SalishSeaCast)

Squash-merged PR#196 for update-NeahBay-ssh-url branch
(SalishSeaNowcast)


Sun 20-Aug-2023
^^^^^^^^^^^^^^^

Heart Island

Discovered that something is wrong with photo backup drive; rsync to it stalls, dismount fails,
fsck reports bad super block; decided to leave it until I get home for further investigation.

Dinner at Pete & Rene's.


Week 34
-------

Mon 21-Aug-2023
^^^^^^^^^^^^^^^

Heart Island

make_ww3_wind_file forecast2 stalled; killed and skipped run
(SalishSeaCast)


Tue 22-Aug-2023
^^^^^^^^^^^^^^^

Heart Island

Hiked Nick & Jana's trail to the lake w/ everyone; rolled my left side into a bog stream.

make_ww3_current_file forecast stalled; killed and re-ran it
(SalishSeaCast)


Wed 23-Aug-2023
^^^^^^^^^^^^^^^

make_ww3_current_file forecast2 stalled; killed and skipped run
(SalishSeaCast)

Heart Island to Vancouver


Thu 24-Aug-2023
^^^^^^^^^^^^^^^

make_ww3_wind_file forecast stalled; killed and re-ran it
(SalishSeaCast)


Fri 25-Aug-2023
^^^^^^^^^^^^^^^

crop_gribs 12 left 1 file uncropped: 20230825T12Z_MSC_HRDPS_RH_AGL-2m_RLatLon0.0225_PT004H.grib2
  crop_gribs 12 RH_AGL-2m 4  # restarted automation
  kill crop_gribs 12
make_ww3_current_file forecast stalled; killed and re-ran it
(SalishSeaCast)

Minecraft sound not working after big wad of system updates. :-(


Sat 26-Aug-2023
^^^^^^^^^^^^^^^

make_ww3_wind_file forecast2 stalled; killed and skipped run
(SalishSeaCast)


Sun 27-Aug-2023
^^^^^^^^^^^^^^^

Fixed Minecraft sound issue:
* first tried https://jackaudio.org/faq/linux_rt_config.html that I found by googling
  "linux realtime-privilege"
  * changes:
      sudo nano /etc/security/limits.d/audio.conf
        @audio   -  rtprio     95
        @audio   -  memlock    unlimited
      sudo usermod -a -G audio doug
      reboot
  * did not fix the issue, but I did not undo the changes
* Googled log message "[ALSOFT] (EE) Failed to connect output port "alsoft:channel_1""
  and found https://forum.garudalinux.org/t/no-audio-in-minecraft-since-recent-update/30532/6
  * changes:
      sudo mkdir /etc/openal
      sudo nano /etc/openal/alsoft.conf
        drivers=alsa
      reboot
  * success!! :-)

Drove to White Rock to celebrate j's 97th birthday.


Week 35
-------

Mon 28-Aug-2023
^^^^^^^^^^^^^^^

make_ww3_current_file forecast2 stalled; killed and skipped run
crop_gribs failed with FileNotFoundError:
* seen before
* all expected 00 files are present
* **but crop_gribs 06 wasn't launched**; launched it manually
(SalishSeaCast)

Ran:
  python3 /media/doug/warehouse/MOAD/gha-workflows/gha_workflow_checker/gha_workflows_checker.py
all good!

Squash-merged dependabot PRs re: gitpython re: CVE-2023-40267 remote code execution vulnerability:
* AtlantisCmd
* NEMO-Cmd
* SalishSeaNowcast
* SalishSeaCmd
Squash-merged dependabot PRs re: tornado re: GHSA-qppv-j76h-2rpx HTTP request smuggling
vulnerability:
* SalishSeaNowcast
* SalishSeaCast/docs
* moad_tools
* MoaceanParcels
* Reshapr
* SalishSeaTools
* MOAD/docs
Squash-merged dependabot PRs re: pyramid re: CVE-2023-40587 static view path traversal
vulnerability:
* salishsea-site

Docs build failures in brown-out on readthedocs due to deprecation of build.image config key in favour of build.os; see https://docs.readthedocs.io/en/stable/config-file/v2.html#build-os:
* AtlantisCmd - fixed
* SalishSeaTools - fixed

Updated readthedocs build config, etc. re: build failures in brown-out on readthedocs due to 
deprecation of build.image config key in favour of build.os;
see https://docs.readthedocs.io/en/stable/config-file/v2.html#build-os
branch: update-readthedocs-config
PR#27 - squash-merged
(AtlantisCmd)

Updated readthedocs build config re: build failures in brown-out on readthedocs due to 
deprecation of build.image config key in favour of build.os;
see https://docs.readthedocs.io/en/stable/config-file/v2.html#build-os
Fixed html_theme specification in Sphinx config.
branch: update-readthedocs-config
PR#84 - squash-merged
(SalishSeaTools)

Fixed html_theme specification in Sphinx config.
Fixed broken links for NEMO book; now at https://zenodo.org/record/3248739
branch: fix-html_theme
PR#34 - squash-merged
(SalishSeaCast/docs)

SalishSeaNowcast had pytest and linkcheck failures.

docs builds failed due to NameError for html_theme
* SalishSeaCast/docs - fixed
* tools/SalishSeaTools - fixed

moad_tools docs build failed due to ImportError for setup_js_tag_helper
* https://github.com/readthedocs/sphinx-notfound-page/issues/219

Updated khawal PyCharm to 2023.2.1.
Updated khawla JetBrains Toolsbox to v2.0

SalishSeaCast/docs linkcheck failed due to broken link for NEMO book;
gone from NEMO site, but Susan found https://zenodo.org/record/3248739


Tue 29-Aug-2023
^^^^^^^^^^^^^^^

Worked at ESB

Group mtg; see whiteboard.
(MOAD)

More analysis of last night's crop_gribs FileNotFoundError failure leads me to 
conclude that it was crop_gribs 06 failing to launch, not crop_gribs 00 failing;
there is a potential race conditions between collect_weather and crop_gribs re:
the creation of the /results/forcing/atmospheric/continental2.5/GRIB/yyyymmdd/hh/ directory;
if collect_weather doesn't get it created before crop_gribs starts to observe it, the latter
fails; created issue #197
(SalishSeaNowcast)

Continued work on separating dataset descriptions into files to be composed into
dataset.xml by a script:
* branch: separate-dataset-files
* PR#1
* started migrating SalishSeaCast NEMO v2019-05 results datasets to
  ssc-nemo-201905/
  * datasets/ssc-nemo-201905/ubcSSg3DuGridFields1hV19-05.xml
  * datasets/ssc-nemo-201905/ubcSSg3DvGridFields1hV19-05.xml
  * datasets/ssc-nemo-201905/ubcSSg3DwGridFields1hV19-05.xml
  * datasets/ssc-nemo-201905/ubcSSgSurfaceTracerFields1hV19-05.xml
(erddap-datasets)

Introduced myself to Karris Hung (the new Emma) and Amber Stefanson (the new Rene).


Wed 30-Aug-2023
^^^^^^^^^^^^^^^

crop_gribs 06 left 2 files uncropped:
  20230830T06Z_MSC_HRDPS_PRMSL_MSL_RLatLon0.0225_PT013H.grib2
  20230830T06Z_MSC_HRDPS_PRATE_Sfc_RLatLon0.0225_PT025H.grib2
  kill crop_gribs 06
  crop_gribs 06 PRMSL_MSL 13 --debug
  crop_gribs 06 PRATE_Sfc 25 --debug
(SalishSeaCast)

Squash-merged dependabot PRs re: jupyter-server re:
* CVE-2023-40170 criss-site inclusion (XSSI) vulnerability
* CVE-2023-39968 open redirect vulnerability
* MoaceanParcels
* SalishSeaTools
* SOG-Bloomcast-Ensemble
  * also cryptography and tornado PRs that were missed

Confirmed that pytest-with-coverage and sphinx-linkcheck failures on Mon were anomalous
(SalishSeaNowcast)

Fixed AttributeError: module 'numpy' has no attribute 'int' in random_oil_spills module;
numpy.int was deprecated in NumPy=1.20
issue #39
branch: fix-numpy.int-deprecation
PR #40 - squash-merged
(moad_tools)

MOAD group party


Thu 31-Aug-2023
^^^^^^^^^^^^^^^

make_ww3_wind_file forecast2 stalled; killed and skipped run
crop_gribs 18 left 1 files uncropped:
  20230831T18Z_MSC_HRDPS_DSWRF_Sfc_RLatLon0.0225_PT035H.grib2
  kill crop_gribs 18
  crop_gribs 06 DSWRF_Sfc 35 --debug
(SalishSeaCast)

Used VSCode ``SalishSeaNowcast [SSH:skookum]`` session to run 
``nowcast.workers.day_month_avgs 2023-07-01`` in new ``day_month_avgs`` tmux session on
skookum against dask cluster on salish: 
* 3 FutureWarning per day-avg:
    /SalishSeaCast/Reshapr/reshapr/core/extract.py:929: 
    FutureWarning: Following pandas, the `loffset` parameter to resample will be deprecated 
    in a future version of xarray.  Switch to using time offset arithmetic.
      resampler = extracted_ds.resample(
  see Reshapr issue #82
* processes that I would have previously considered to be stalled seem to be progressing very 
  slowly; re-ran and some missing day-avgs were completed except:
  * physics 2023-07-19
  * biology 2023-07-26
  * killed those processes on salish and re-tried; same stalls
  * Used VSCode ``month-avg.202111 /results2/SalishSea [SSH: salish]`` session on salish to run
    in ``/results2/SalishSea/month-avg.202111/``:
    ``python3 -m day_avg 2023-07-19 physics`` 
    ``python3 -m day_avg 2023-07-26 biology``
  * re-ran day_month_avgs to finish month-avgs
* noticable memory leakage from workers; kille and restarted them:
  * worker spawner: 5.015g
  * scheduler: 4.822g
  * 4 workers: 0.672g
(hindcast)

Continued work on separating dataset descriptions into files to be composed into
dataset.xml by a script:
* branch: separate-dataset-files
* PR#1
* continued migrating SalishSeaCast NEMO v2019-05 results datasets to
  ssc-nemo-201905/
  * datasets/ssc-nemo-201905/ubcSSg3DBiologyFields1hV19-05.xml
  * datasets/ssc-nemo-201905/ubcSSg3DTracerFields1hV19-05.xml
  * datasets/ssc-nemo-201905/ubcSSg3DAuxiliaryFields1hV19-05.xml
(erddap-datasets)

September
---------

Fri 1-Sep-2023
^^^^^^^^^^^^^^

Noticed that yesterday's make_ww3_current_file forecast stalled:
* recovery:
    kill make_ww3_current_file
    wait for wwatch3 runs to finish at ~11:30;
      didn't happen due to make_ww3_wind_file forecast stall
    make_ww3_wind_file arbutus nowcast 2023-08-31
    make_ww3_current_file arbutus nowcast 2023-08-31 
    wait for wwatch3 runs to finish
    make_ww3_wind_file arbutus nowcast 2023-09-01
    make_ww3_current_file arbutus nowcast 2023-09-01  # took 3 tries to get completion :-(
Found and killed spilling NEMO run from 6-Aug.
(SalishSeaCast)

Email with Henryk re: /ocean/vvalenzuela; first wrong surname, then cross-linked to /ocean/atall;
sigh.

Hacked crop_gribs on skookum to change observer thread timeout from 1s to 2s to see what affect,
if any, that has on stalls.
(SalishSeaNowcast)


Sat 2-Sep-2023
^^^^^^^^^^^^^^

make_ww3_current_file forecast2 stalled; killed and skipped run
crop_gribs 18 failed with FileNotFoundError; launched manually.
make_ww3_current_file forecast stalled; killed and re-ran it
(SalishSeaCast)


Sun 3-Sep-2023
^^^^^^^^^^^^^^

make_ww3_current_file forecast2 stalled; killed and re-ran it
crop_gribs 18 failed with FileNotFoundError; launched manually
crop_gribs 12 finished ~13 min after collect_weather 12 (was ~2m37s yesterday);
perhaps and affect of increaing the observer thread timeout?;
or maybe skookum Sunday file syetem slowness?
(SalishSeaCast)


Week 36
-------

Mon 4-Sep-2023
^^^^^^^^^^^^^^

**Statutory Holiday** - Labour Day

make_ww3_current_file forecast2 stalled; did nothing so...
make_ww3_current_file forecast failed to launch; killed above and re-ran it
(SalishSeaCast)


Tue 5-Sep-2023
^^^^^^^^^^^^^^

Group mtg; see whiteboard.
On-boarding mtg w/ Jake
(MOAD)

download_weather 00 1km failed due to missing hour 1 LHTFL file; skipped
(SalishSeaCast)


Wed 6-Sep-2023
^^^^^^^^^^^^^^

Worked on garage setup re: new Milwaukee workbench.

Rescheduled on-boarding meeting w/ Vicente to Tuesday.
Sent link and directions to Tall for graham setup.
Slack conversation with Jake:
* need a hangout or mtg to resolve ssh config problem
* .bash_profile from compstaff setup is now exactly what we want
* .bashrc from compstaff now exists; need to change docs to add the bit that I recommend
(MOAD)


Thu 7-Sep-2023
^^^^^^^^^^^^^^

Slack conversation w/ Birgit about using NEMO-Cmd for BAS NEMO 4.2 configs.

Squash-merged dependabot PRs re: actions/checkout re: update of default runtime to node20:
* gha-workflows
* salishsea-site
Squash-merged dependabot PRs re: gitpython re: CVE-2023-40590 arbitrary code execution 
vulnerability re: Python on Windows:
* NEMO-Cmd
* AtlantisCmd
* SalishSeaCmd
* SalishSeaNowcast
Squash-merged dependabot PR in gha-workflows re: setup-micromamba update to 1.4.4

Hangout w/ Tall re: setting up to run NEMO on graham.

Confirmed that 28-Aug pytest-with-coverage GHA failure was anomalous; 
subsequent run was successful.
(moad_tools)

Re-ran 28-Aug pytest-with-coverage GHA job; success, so another anomaly.
(Reshapr)

List of Bad Files for datasetID=ubcSSg3DuGridFields1hV19-05:
  /results2/SalishSea/nowcast-green.201905/19dec08/SalishSea_1h_20081219_20081219_grid_U.nc
  /results2/SalishSea/nowcast-green.201905/27aug08/SalishSea_1h_20080827_20080827_grid_U.nc
  /results2/SalishSea/nowcast-green.201905/09feb22/SalishSea_1h_20220209_20220209_grid_U.nc
Error message:
  java.lang.OutOfMemoryError: Ran out of memory trying to read HDF5 filtered chunk.
  Either increase the JVM's heap size (use the -Xmx switch) or reduce the size of the
  dataset's chunks (use nccopy -c).
  at ucar.nc2.iosp.hdf5.H5tiledLayoutBB$DataChunk.getByteBuffer(H5tiledLayoutBB.java:255)
List of Bad Files for datasetID=ubcSSg3DwGridFields1hV19-05
  /results2/SalishSea/nowcast-green.201905/13jan22/SalishSea_1h_20220113_20220113_grid_W.nc
  /results2/SalishSea/nowcast-green.201905/17jan22/SalishSea_1h_20220117_20220117_grid_W.nc
  /results2/SalishSea/nowcast-green.201905/24jan22/SalishSea_1h_20220124_20220124_grid_W.nc
  /results2/SalishSea/nowcast-green.201905/27jan22/SalishSea_1h_20220127_20220127_grid_W.nc
  /results2/SalishSea/nowcast-green.201905/02feb22/SalishSea_1h_20220202_20220202_grid_W.nc
  /results2/SalishSea/nowcast-green.201905/11feb22/SalishSea_1h_20220211_20220211_grid_W.nc
  /results2/SalishSea/nowcast-green.201905/16feb22/SalishSea_1h_20220216_20220216_grid_W.nc
  /results2/SalishSea/nowcast-green.201905/19feb22/SalishSea_1h_20220219_20220219_grid_W.nc
  /results2/SalishSea/nowcast-green.201905/01aug22/SalishSea_1h_20220801_20220801_grid_W.nc
List of Bad Files for datasetID=ubcSSg3DTracerFields1hV19-05
  /results2/SalishSea/nowcast-green.201905/10jan19/SalishSea_1h_20190110_20190110_grid_T.nc
  /results2/SalishSea/nowcast-green.201905/02jan19/SalishSea_1h_20190102_20190102_grid_T.nc
  /results2/SalishSea/nowcast-green.201905/03jan19/SalishSea_1h_20190103_20190103_grid_T.nc
  /results2/SalishSea/nowcast-green.201905/01jan19/SalishSea_1h_20190101_20190101_grid_T.nc
  /results2/SalishSea/nowcast-green.201905/21sep22/SalishSea_1h_20220921_20220921_grid_T.nc
  /results2/SalishSea/nowcast-green.201905/14oct22/SalishSea_1h_20221014_20221014_grid_T.nc
  /results2/SalishSea/nowcast-green.201905/21oct22/SalishSea_1h_20221021_20221021_grid_T.nc
  /results2/SalishSea/nowcast-green.201905/08jan19/SalishSea_1h_20190108_20190108_grid_T.nc
  /results2/SalishSea/nowcast-green.201905/09jan19/SalishSea_1h_20190109_20190109_grid_T.nc
(ERDDAP)

make_ww3_current_file forecast2 stalled; did nothing so...
make_ww3_current_file forecast failed to launch; killed  above and re-ran it
(SalishSeaCast)


Fri 8-Sep-2023
^^^^^^^^^^^^^^

crop_gribs 12 left 1 files uncropped:
  20230908T12Z_MSC_HRDPS_LHTFL_Sfc_RLatLon0.0225_PT014H.grib2
  crop_gribs 12 LHTFL_Sfc 14  # to unblock automation
  kill crop_gribs 12
1st occurrence since I increased observer thread timeout to 2s on 1-Sep
(SalishSeaCast)

An email from "RPN,Service [CMC]" <Service.RPN@ec.gc.ca> revealed that I have an account on
the GPSCC2 collaboration server that is being migrated to the new GPSCC3 server; an ssh attempt
  ssh -v dlatornell@inter-c-eccc-lp.collab.science.gc.ca 
gets me as far as asking for a password (that I don't have).

Used VSCode ``SalishSeaNowcast [SSH:skookum]`` session to run 
``nowcast.workers.day_month_avgs 2023-07-01`` in ``day_month_avgs`` tmux session on
skookum against dask cluster on salish: 
* 3 FutureWarning per day-avg:
    /SalishSeaCast/Reshapr/reshapr/core/extract.py:929: 
    FutureWarning: Following pandas, the `loffset` parameter to resample will be deprecated 
    in a future version of xarray.  Switch to using time offset arithmetic.
      resampler = extracted_ds.resample(
  see Reshapr issue #82
* 1 stalled day-avg; re-ran and same day-avg stalled:
  * physics 2023-08-21
    * killed those processes on salish
  * Used VSCode ``month-avg.202111 /results2/SalishSea [SSH: salish]`` session on salish to run
    in ``/results2/SalishSea/month-avg.202111/``:
    ``python3 -m day_avg 2023-08-21 physics`` 
  * re-ran day_month_avgs to finish month-avgs
* noticable memory leakage from workers:
  * worker spawner: 5.026g
  * scheduler: 4.840g
  * 4 workers: 1.154g
(hindcast)

Started work on issue #82 re: loffset deprecation; little progress.
(Reshapr)


Sat 9-Sep-2023
^^^^^^^^^^^^^^

Did 2023 income tax estimate.

make_ww3_current_file forecast failed to launch; killed and re-ran it; took 4 tries
crop_gribs 00 left 1 files uncropped:
  20230910T00Z_MSC_HRDPS_LHTFL_Sfc_RLatLon0.0225_PT047H.grib2
  crop_gribs 00 LHTFL_Sfc 47 2023-09-10 --debug  # to finish processing
  kill crop_gribs 00
2nd occurrence since I increased observer thread timeout to 2s on 1-Sep
(SalishSeaCast)


Sun 10-Sep-2023
^^^^^^^^^^^^^^^

Block watch meet & greet.

Transit to/from White Rock for dinner with J & Bonnie.


Week 37
-------

Mon 11-Sep-2023
^^^^^^^^^^^^^^^

Squash-merged dependabot PR in gha-workflows re: setup-micromamba update to 1.4.4.
Squash-merged dependabot PR re: actions/checkout re: update of default runtime to node20.
Squash-merged dependabot PR re: gitpython re: DoS vulnerability.
(SalishSeaNowcast)

Continued work on issue #82 re: loffset deprecation; no progress; developed demo code and posted 
question on xarray Q&A discussion.
(Reshapr)


Tue 12-Sep-2023
^^^^^^^^^^^^^^^

Worked at ESB.

Group mtg; wee whiteboard.
On-boarding meeting w/ Vicente.
(MOAD)

make_ww3_current_file forecast failed to launch; killed and re-ran it
(SalishSeaCast)

Decided to try to follow readthedocs recommendation to pin Sphinx version instead of pinning
sphinx-rtd-theme.
Started work on updating bash config section re: compstaff created .bash_profile and .bashrc
files.
branch: update-bash-config
PR#32
(MOAD docs)


Wed 13-Sep-2023
^^^^^^^^^^^^^^^

Rifted on Susan's xarray plot() snippet with water points selected via where()
to make it more explicit/Pythonic using slice() and isel().
(MOAD)

Finished updating bash config section re: compstaff created .bash_profile and .bashrc
files.
Updated redirected links.
Had to change to install all deps via pip in order to get consistent collection with
pinned Sphinx version.
Re-synced readthedocs-GitHub webhook so that PR pushes build on readthedocs.
branch: update-bash-config
PR#32 - squash-merged
(MOAD docs)

Continued work on separating dataset descriptions into files to be composed into
dataset.xml by a script:
* branch: separate-dataset-files
* PR#1
* Migrated SalishSeaCast NEMO v2019-05 month-averaged datasets to
  ssc-nemo-201905/month-average/
  * datasets/ssc-nemo-201905/month-average/ubcSSg3DuGridFields1moV19-05.xml
  * datasets/ssc-nemo-201905/month-average/ubcSSg3DvGridFields1moV19-05.xml
  * datasets/ssc-nemo-201905/month-average/ubcSSg3DwGridFields1moV19-05.xml
  * datasets/ssc-nemo-201905/month-average/ubcSSg3DBiologyFields1moV19-05.xml
  * datasets/ssc-nemo-201905/month-average/ubcSSg3DTracerFields1moV19-05.xml
(erddap-datasets)

crop_gribs 00 left 1 files uncropped:
  20230914T00Z_MSC_HRDPS_APCP_Sfc_RLatLon0.0225_PT002H.grib2
  crop_gribs 00 APCP_Sfc 2 2023-09-14 --debug  # to finish processing
  kill crop_gribs 00
3rd occurrence since I increased observer thread timeout to 2s on 1-Sep
(SalishSeaCast)


Thu 14-Sep-2023
^^^^^^^^^^^^^^^

crop_gribs 06 left 1 files uncropped:
  20230914T06Z_MSC_HRDPS_APCP_Sfc_RLatLon0.0225_PT043H.grib2
  crop_gribs 06 APCP_Sfc 43 2023-09-14  # to restart automation
  kill crop_gribs 06
4th occurrence since I increased observer thread timeout to 2s on 1-Sep;
2nd in ~6h :-(
(SalishSeaCast)

Updated minecraft 1.20.1 single player creative world copy of Nodecraft world:
* stopped server (50d of uptime)
* created and downloaded backup: Lifeful Rainbow Road 
* started server
* created new single player world from backup zip

UBC-IOS modeling collaboration mtg:
Jonathan Izett - WCVI FVCOM model setup
* motivated by hypoxia in Cliquaot Sound
* 2019
* CIOPS-W 1/36 degree initial conditions & boundary
* 29 rivers
  * few gauged or sampled
  * GlobalNEWS2 database for watershed nutrients; annual estimates
* HRDPS 2.5km or 1km atmospheric forcing
  * lots of weather stations at fish farms to evaluate HRDPS
  * HRDPS has orographic filtering that effectively reduces resolution in fjords

Weekly team mtg.
Discussed refactoring dataset loading in plot functions with Raisha.
(Atlantis)


Fri 15-Sep-2023
^^^^^^^^^^^^^^^

make_ww3_current_file forecast2 failed to launch; killed and re-ran it
grib_to_netcdf failed due to missing 00 file
* crop_gribs 00 left 1 files uncropped and I didn't notice last night:
    20230915T00Z_MSC_HRDPS_APCP_Sfc_RLatLon0.0225_PT002H.grib2
    crop_gribs 00 APCP_Sfc 2 --debug
    kill crop_gribs 00
    grib_to_netcdf nowcast+
    upload_forcing arbutus nowcast+
    upload_forcing graham-dtn nowcast+
    upload_forcing orcinus-nowcast-agrif nowcast+
    upload_forcing optimum-hindcast nowcast+
  5th occurrence since I increased observer thread timeout to 2s on 1-Sep;
(SalishSeaCast)

Phys Ocgy Seminar:
* Grace: SOP for drifter obs QA and evaluation; co-op work terms
* Vicente: dissolved iron and high productivity around Elephant Island in southern ocean; 
  undergrad thesis
  * high productivity is anomalous; most southern ocean has low productivity

Helped Vicente through ssh setup on his Windows laptop:
* Windows doesn't have ssh-copy-id; have to do the old dance of creating remote .ssh/authorized_keys
  with correct permissions, then pasting pubilc key into it
* need to use Powershell to start ssh-agent service load authenticate public key
* need to install Git; lots of config choices


Sat 16-Sep-2023
^^^^^^^^^^^^^^^

make_ww3_current_file forecast2 failed to launch; killed and re-ran it
crop_gribs 12 left 1 files uncropped:
  20230916T12Z_MSC_HRDPS_APCP_Sfc_RLatLon0.0225_PT026H.grib2
  crop_gribs 12 APCP_Sfc 26 # to unblock automation
  kill crop_gribs 12
(SalishSeaCast)

Added -O to ncks command in make_ww3_current_file that extracts 1st 24h of currents forecast
during forecast2 prep; trying to eliminate "what should I do" terminal prompts from ncks that
occur sometimes in manual launches of make_ww3_current_file.
* rsynced to arbutus to test in production
(SalishSeaNowcast)


Sun 17-Sep-2023
^^^^^^^^^^^^^^^

crop_gribs 06 left 1 files uncropped:
  20230917T06Z_MSC_HRDPS_LHTFL_Sfc_RLatLon0.0225_PT011H.grib2
  crop_gribs 06 LHTFL_Sfc 11  # to unblock automation
  kill crop_gribs 06
  forecast2 runs started at ~08:00
make_ww3_current_file forecast2 crashed
* -O I added yesterday to ncks caused crash because it is only applicable when output file
  exists; that's not true in normal processing :-(
wwatch3 forecast2 prep race condition management collided with nowcast+ race condition mgmt
causing upload_forcing launches to not happen
* recovery started at ~09:30
    upload_forcing arbutus nowcast+
    upload_forcing graham-dtn nowcast+
    upload_forcing orcinus-nowcast-agrif nowcast+
    upload_forcing optimum-hindcast nowcast+
crop_gribs 18 left 1 files uncropped:
  20230917T18Z_MSC_HRDPS_APCP_Sfc_RLatLon0.0225_PT006H.grib2
  crop_gribs 18 APCP_Sfc 6 --debug
  kill crop_gribs 18
(SalishSeaCast)

Reverted yesterday's addition of -O to ncks command in make_ww3_current_file that extracts 1st 24h 
of currents forecast during forecast2 prep; it is only applicable when output file
exists; that's not true in normal processing :-(
Started work on changes to crop_gribs to have it retry uncropped files after it has been watching
for 8 hours.
(SalishSeaNowcast)


Week 38
-------

Mon 18-Sep-2023
^^^^^^^^^^^^^^^

Worked on Workday Hybrid Work Agreement.

Tried to help Jose with weird connection failure to salish on ubc-secure; other EAOS hosts
are fine; learned about ``sudo fail2ban-client status sshd``.

Helped Vicente with Anaconda vs. Miniforge.

Helped Tall with sample files to run 202111 on graham.

Continued work on changes to crop_gribs to have it retry uncropped files after it has been watching
for 8 hours:
* deployed 1st draft code to skookum and restarted crop-gribs 00 for testing this evening
(SalishSeaNowcast)

Tried to enable bundles in Nodecraft world:
* edit server.properties:
    ``initial-enabled-packs=vanilla,bundle``
* restarted server: no effect
redit suggests need to edit NBT tags for change to take effect after world creation;
unspported

crop_gribs 00 had 1 file uncropped when it should have finished at ~20:42:
  20230919T00Z_MSC_HRDPS_DLWRF_Sfc_RLatLon0.0225_PT012H.grib2
left it alone to see if retry feature I added will work at ~23:15
(SalishSeaCast)

Still getting messages from ERDDAP complaining about 
"java.io.IOException: User limit of inotify watches reached"; tried mitigate that by
doubling ERDDAP docs suggestions:
  sudo sysctl fs.inotify.max_user_watches=131072
  sudo sysctl fs.inotify.max_user_instances=2048
  sudo sysctl -p
(ERDDAP)

Maybe need to restart ERDDAP???


Tue 19-Sep-2023
^^^^^^^^^^^^^^^

crop_gribs 00 retry worked!!
crop_gribs 18 had 1 file uncropped:
  20230919T18Z_MSC_HRDPS_DLWRF_Sfc_RLatLon0.0225_PT035H.grib2
left it alone for retry feature to handle at ~16:50; it worked!
(SalishSeaCast)

Group mtg; see whiteboard.
(MOAD)

Continued work on changes to crop_gribs to have it retry uncropped files after it has been watching
for 8 hours:
* refactored code into a function and realized that it had a redundant failure check in it
* wrote stubs for unit tests for function
* added crop_gribs to Slack notifications list in nowcast system config
(SalishSeaNowcast)

Met with Tall to help him through NEMO build process on graham and first run.

Met with Vicente to explain Anaconda vs. Miniforge to him.

Helped Jake deal with csv dataset from Metro Van that has obs with missing date/time stamps.


Wed 20-Sep-2023
^^^^^^^^^^^^^^^

Coffee w/ Karyn.

ECG at LifeLabs.

Helped Jake csv dataset grouping and aggregation.

Continued work on changes to crop_gribs to have it retry uncropped files after it has been watching
for 8 hours:
* deployed refactored version of code to skookum for testing in crop_gribs 00 onward
* finished writing unit tests for function
(SalishSeaNowcast)

crop_gribs 18 had 1 file uncropped:
  20230920T18Z_MSC_HRDPS_LHTFL_Sfc_RLatLon0.0225_PT019H.grib2
left it alone for retry feature to handle at ~16:31
(SalishSeaCast)


Thu 21-Sep-2023
^^^^^^^^^^^^^^^

crop_gribs 06 had 11 file uncropped distributed across hours 014, and 016-018;
retry feature sent a critical error at 04:28; grib_to_netcdf subsequently failed
* recovery started at ~07:45
    sent email to Sandrine
    files appeared slowly between 08:35 and ????
    ran crop_gribs a file as a time as missing files were downloaded
    at 10:15 email from Sandrine said issue was resolved, but hour 017 files were still missing;
    she said that the issue was due to a server migration in progress; told her about 017 files
    decided to skip forecast2 runs
    collect_weather 12 2.5km --backfill
    hacked crop_gribs to process backfilled 12 files sequentially
    crop_gribs 12
    make_runoff_file failed because collect_river_data didn't run due to collect_weather 06 
    never finishing
    recovery started at ~13:15
      bash /SalishSeaCast/datamart/hydrometric/collect_river_data.sh 2023-09-20
      make_runoff_file
      make_v202111_runoff_file
      upload_forcing arbutus nowcast+
        nowcast-blue run started at 13:30
      upload_forcing graham-dtn nowcast+
      upload_forcing orcinus-nowcast-agrif nowcast+
      upload_forcing optimum-hindcast nowcast+
      get_onc_ctd SCVIP
      get_onc_ctd SEVIP
    killed collect_weather 06  # hour 017 incomplete; only used for forecast2 run
killed and re-ran crop_gribs 18 to ensure the correct version is running
discovered that yesterday's make_ww3* workers both got stuck; recovery:
  killed stuck workers
  make_ww3_wind_file forecast 2023-09-20
  make_ww3_current_file forecast 2023-09-20
  wait for runs to finish
  make_ww3_wind_file forecast 2023-09-20
  make_ww3_current_file forecast 2023-09-20
(SalishSeaCast)

EOAS welcome back BBQ

Squash-merged dependabot PRs re: update of cryptography due to minor vulnerabilities in its
statically linked OpenSSL re: GHSA-v8gr-m533-ghj9
* NEMO-Cmd
* SalishSeaNowcast
* MoaceanParcels
* cookiecutter-analysis-repo
* SalishSeaCast/docs
* cookiecutter-MOAD-pypkg
* SalishSeaCmd
* NEMO_Nowcast
* salishsea-site
Squash-merged dependabot PRs re: gitpython re: CVE-2023-41040 DoS vulnerability
* SalishSeaCmd
* NEMO-Cmd


Fri 22-Sep-2023
^^^^^^^^^^^^^^^

Traced today's spate of ERDDAP request failures to dataforseo.com, an Estonian SEO company;
blocked them by adding IP address 136.243.228.193 to requestBlacklist tag in datasets.xml.
Continued work on separating dataset descriptions into files to be composed into
dataset.xml by a script:
* branch: separate-dataset-files
* PR#1
* Started migrating SalishSeaCast NEMO rolling forecast datasets to
  ssc-nemo-201905/rolling-forecasts/
  * datasets/rolling-forecasts/ubcSSf3DuGridFields1h.xml
  * datasets/rolling-forecasts/ubcSSf3DvGridFields1h.xml
  * datasets/rolling-forecasts/ubcSSfDepthAvgdCurrents1h.xml
(erddap-datasets)

Phys Ocgy seminar: Rosie Eaves, visiting Ph.D. student from Oxford working with Stephanie
mesoscale eddy parameterization for climate models

make_ww3_current_file forecast failed to launch; killed and re-ran it
(SalishSeaCast)


Sat 23-Sep-2023
^^^^^^^^^^^^^^^

make_ww3_current_file forecast2 failed to launch; killed it and skipped run
Restarted manager to enable Slack notifications for crop_gribs instances.
make_ww3_current_file forecast failed to launch; killed and re-ran it
(SalishSeaCast)

Continued work on separating dataset descriptions into files to be composed into
dataset.xml by a script:
* branch: separate-dataset-files
* PR#1
* Contined migrating SalishSeaCast NEMO rolling forecast datasets to
  ssc-nemo-201905/rolling-forecasts/
  * datasets/rolling-forecasts/ubcSSfSurfaceTracerFields1h.xml
(erddap-datasets)

Continued work on changes to crop_gribs to have it retry uncropped files after it has been watching
for 8 hours:
* branch: robust-crop-gribs
* added crop_gribs to Slack notifications
* changed observer thread timeout to 0.5s since 2s didn't seem to be any better than 1s re:
  stalling with 1 file uncropped
* committed stalled observer code and tests
* created PR#203
* merge conflict mess :-(  re: dependabot bump of cryptography versions
(SalishSeaNowcast)


Sun 24-Sep-2023
^^^^^^^^^^^^^^^

make_ww3_wind_file forecast2 failed to launch; killed it and skipped run
crop_gribs 00 stalled and recovered itself at 8h
(SalishSeaCast)


Week 39
-------

Mon 25-Sep-2023
^^^^^^^^^^^^^^^

Email from MSC saying that server migration is causing data dissemination issues.
collect_weather 12 and crop_gribs 12 stalled missing 2 files:
  20230925T12Z_MSC_HRDPS_TMP_AGL-2m_RLatLon0.0225_PT012H.grib2
  20230925T12Z_MSC_HRDPS_RH_AGL-2m_RLatLon0.0225_PT018H.grib2
Sent email to Sandrine about those 2 files.
Expecting:
* crop_gribs 12 to finish, reporting those files missing at ~10:30; happened
* grib_to_netcdf to fail; happened
* collect_weather 12 to continue watching; happened
* recovery started at ~10:30:
    collect_weather 18 2.5km
    crop_gribs 18
    wait for collect_weather 12 to finish

    crop_gribs 12 TMP_AGL-2m 12
    crop_gribs 12 RH_AGL-2m 18
collect_weather 18 2.5km and collect_weather [00|12] 1km finished successfully
crop_gribs 18 stalled with 1 file uncropped; expect recovery at ~18:30; success
Discussed way forward w/ Susan:
* realized that grib_to_netcdf has successfully created today's forcing, but not forecast forcing
  for next 36h, however 30h of that was created for forecast2 this morning
* decided to restart automation with manual launch of workers that would have launched if  
  collect_weather 12 had finished
  * there is a risk that if missing 12 files appear runs will get messed up when proper forcing 
    is uploaded
* recovery started at ~15:35:
    collect_river_data USGS SkagitMountVernon 2023-09-24
    collect_river_data USGS SnohomishMonroe 2023-09-24
    collect_river_data USGS NisquallyMcKenna 2023-09-24
    collect_river_data USGS GreenwaterGreenwater 2023-09-24
    make_turbidity_file
    collect_NeahBay_ssh 06
    download_live_ocean
    wait for NEMO forecast run to fail at ~16:40; stalled at 84.7%
    killed xios_server.exe and watch_NEMO on arbutus
    upload_forcing arbutus turbidity
    upload_forcing orcinus turbidity
    upload_forcing optimum turbidity
    upload_forcing graham turbidity
    make_forcing_links salish nowcast+ --shared-storage
(SalishSeaCast)

Continued work on changes to crop_gribs to have it retry uncropped files after it has been watching
for 8 hours:
* branch: robust-crop-gribs
* PR#203
* resolved merge conflict mess re: dependabot bump of cryptography versions
* added code to create directory that observer watches re: issue #197 and being able to launch
  crop_gribs before collect_weather --backfill for recover from automation problems; pushed code
  to skookum for production testing
* linked to issue#197
* fixed broken docs link re: NOAA Neah Bay sea surface height files
(SalishSeaNowcast)

Found nbt2yaml by Mike Bayer on PyPI; installed it on khawla
  mamba create -n nbt2yaml python=3.11 python-editor PyYAML pip
  conda activate nbt2yaml
  python3 -m pip install nbt2yaml
Made a backup of creative 1.20.1 world; copied its level.dat file to ~/; edited it:
  nbtedit ~/level.dat
  # added just above ``- WorldGenSettings:``
    - enabled_features: !list_string
     - minecraft:bundle
     - minecraft:vanilla
  # move ``bundle`` from ``Datapacks.Disabled`` to ``Datapacks.Enabled``
  # delete ``Datapacks.Disabled``
This makes bundles available in creative, but not in survival.
Found bundle databack in the client .jar and copied it to datapacks/; still no go; the game disables
the feature and removes the recipe from my edited level.dat file

Continued work on separating dataset descriptions into files to be composed into
dataset.xml by a script:
* branch: separate-dataset-files
* PR#1
* Started migrating SalishSeaCast NEMO rolling forecast datasets to
  ssc-nemo-201905/rolling-forecasts/
  * datasets/rolling-forecasts/ubcSSfBoundaryBaySSH10m.xml
  * datasets/rolling-forecasts/ubcSSfCampbellRiverSSH10m.xml
  * datasets/rolling-forecasts/ubcSSfCherryPointSSH10m.xml
(erddap-datasets)


Tue 26-Sep-2023
^^^^^^^^^^^^^^^

Worked at ESB.

Group mtg; see whiteboard.
(MOAD)

Ilias Bougoudis joined group; machine learning post-doc in Prodigy program;
co-supervised by Susan, Raymond Ng in CompSci and Matías Salibián-Barrera in Stats.

Reviewed weekly dependabot alerts email for stale and low priority updates:
* Squash-merged dependabot PRs in cookiecutter-djl-pypkg re: requests and cryptography.
* Squash-merged dependabot PR in SOG-Bloomcast-Ensemble re: cryptography.
* TODO:
  * Update FVCOM-Cmd pytest version to drop py dep - done
  * Update SOG-Bloomcast pytest version to drop py dep; do requests PR
  * Update SOG pytest version to drop py dep
  * Update SOG-forcing pytest version to drop py dep
  * migrate PyPDF2 to pypdf in SalishSeaNowcast
  * Update rpn-to-gemlam pytest version to drop py dep; do tornado and cryptography PRs; 
    then archive repo
  * douglatornell.ca js pkgs
  * Update raspi_x10 pytest version to drop py dep; then archive repo

Finished work on changes to crop_gribs to have it retry uncropped files after it has been watching
for 8 hours:
* branch: robust-crop-gribs
* PR#203; squash-merged
Updated arbutus.cloud deployment docs mostly re: Alliance and use of :kbd: role:
branch: update-arbutus-docs
PR#204; squash-merged
(SalishSeaNowcast)

wwatch3-forecast2 didn't start due to no NEMO forecast currents from yesterday
Missing HRDPS were not uploaded as of 12:00; killed yesterday's collect_weather 12.
(SalishSeaCast)

EOAS Colloquium: Climate Justice panel.


Wed 27-Sep-2023
^^^^^^^^^^^^^^^

Did minimal repo maintenance to remove py pkg dependency with its ReDoS vulnerability;
was reminded of what a hash this project is; Susan says to archive it; done.
Note that test suite appears to have never been updated when this project was
forked from NEMO-Cmd. So, it does not run successfully.
(FVCOM-Cmd)

make_ww3_current_file forecast failed to launch; killed and re-ran it
(SalishSeaCast)

Installed Vivaldi browser on khawla:
* experimented with calendar
  * imported calendars from Google
  * can't see Susan's Assoc Dean calendar, maybe due to Google sharing feature?


Thu 28-Sep-2023
^^^^^^^^^^^^^^^

Released v23.1 of SalishSeaNowcast.
(SalishSeaNowcast)


Fri 29-Sep-2023
^^^^^^^^^^^^^^^

Phys Ocgy seminar: Yulia Egorova, Ph.D. research, Global Mesopelagic Mesozoop

Generated new ed25519 key pair for use on arbutus

Helped Vicente add cartpy to his analysis env.

Added cartopy and its dependencies to notebooks.environment.yaml
(cookiecutter-analysis-repo)

make_ww3_current_file forecast failed to launch; killed and re-ran it
(SalishSeaCast)


Sat 30-Sep-2023
^^^^^^^^^^^^^^^

Rode to Iona and Sanctuary on Gunnars.

make_ww3_wind_file forecast failed to launch; killed and re-ran it
(SalishSeaCast)


October
-------

Sun 1-Oct-2023
^^^^^^^^^^^^^^

make_ww3_current_file and make_ww3_wind_file forecast2 failed to launch; killed and skipped run
make_ww3_current_file and make_ww3_wind_file forecast failed to launch; killed and re-ran them
crop_gribs 18 failed with 143 files not processed; missing hours 036 through 048; we don't need
collect_weather 00 was not launched; backfill mode failed due to missing files;
  ran download_weather 00, but started crop_gribs late
launched collect_weather 06 and crop_gribs 06
(SalishSeaCast)


Week 40
-------

Mon 2-Oct-2023
^^^^^^^^^^^^^^

**Statutory Holiday** - Truth & Reconciliation Day lieu day

grib_to_netcdf nowcast+ failed due to 80 files in 00 forecast that were not cropped because I messed
up late last night
* recovery started at ~09:30
    crop_gribs 00 --backfill  # new feature
    grib_to_netcdf nowcast+
    upload_forcing arbutus nowcast+
    upload_forcing orcinus nowcast+
    upload_forcing optimum nowcast+
    upload_forcing graham-dtn nowcast+
no messages from wwatch3 workers, so restarted log_aggregator
(SalishSeaCast)

Added --backfill arg to crop_gribs to make it run without watching for file system events to 
indicate existence of files to crop; skips already cropped files.
branch: crop_gribs-backfill
PR#
* tested in recovery from last night's collect_weather/crop_gribs 00 mess that stopped today'S
  grib_to_netcdf nowcast+; success
(SalishSeaNowcast)

Set up Minecraft 1.20.2 instance in MultiMC and tried to launch/update copy of 1.20.1 creative 
world; failed due to incompatible version of Malilib mod; not official or community version 
available yet.


Tue 3-Oct-2023
^^^^^^^^^^^^^^

Worked at ESB while Rita was at home.

Weekly group mtg; see whiteboard.
(MOAD)

On-boarding meeting w/ Ilias.

Slack w/ Jake re: open_mfdataset and Reshapr.

Helped Tall with chhosing restart file to run on graham; explained very 5 days + month-end 
restarts in hindcast.

Squash-merged dependabot PRs re: update of urllib3 due to cookie header handling vulnerability
in redirects re: CVE-2023-43804
* Reshapr
* AtlantisCmd
* tools/SalishSeaTools
* moad_tools
* MOAD/docs
* SalishSeaNowcast
* NEMO-Cmd
* cookiecutter-MOAD-pypkg
* MoaceanParcels
* NEMO_Nowcast
* salishsea-site
* SalishSeaCast/docs
* SalishSeaCmd
* cookiecutter-analysis-repo
Squash-merged dependabot PRs re: update of pillow due to a heap buffer overflow in its dependency libwebp re: CVE-2023-4863:
* Reshapr
* moad_tools
* tools/SalishSeaTools
* SalishSeaNowcast
* MoaceanParcels
Squash-merged dependabot PRs re: gitpython re: CVE-2023-41040 DoS vulnerability
* AtlantisCmd


Wed 4-Oct-2023
^^^^^^^^^^^^^^

upload_forcing orcinus forecast2 failed with an OSError;
* investigation:
  * orcinus had a chiller failure on 2-Oct; terminal login okay now
  * no nowcast-agrif runs since 1-Oct
* recovery:
    aborted because logins are flakey
make_ww3_current_file forecast failed to launch; killed and re-ran it
(SalishSeaCast)

Updated PyCharm on khawla to 2023.2.2

Helped Tall with errors in ocean.output.

Continued work on separating dataset descriptions into files to be composed into
dataset.xml by a script:
* branch: separate-dataset-files
* PR#1
* Started migrating SalishSeaCast NEMO rolling forecast datasets to
  ssc-nemo-201905/rolling-forecasts/
  * rolling-forecasts/ubcSSfFridayHarborSSH10m.xml
(erddap-datasets)

Invited Ilias to UBC-MOAD and SalishSeaCast GitHub orgs.

Worked on backfilling missing 2019 wwatch3 runs for Jose:
* missing files on graham:
    /scratch/dlatorne/SalishSeaCast/wwatch3/SoG_ww3_fields_20190501_20190501.nc
    /scratch/dlatorne/SalishSeaCast/wwatch3/SoG_ww3_fields_20190511_20190511.nc
    /scratch/dlatorne/SalishSeaCast/wwatch3/SoG_ww3_fields_20190724_20190724.nc
    /scratch/dlatorne/SalishSeaCast/wwatch3/SoG_ww3_fields_20190906_20190906.nc
    /scratch/dlatorne/SalishSeaCast/wwatch3/SoG_ww3_fields_20190907_20190907.nc
    /scratch/dlatorne/SalishSeaCast/wwatch3/SoG_ww3_fields_20190918_20190918.nc
    /scratch/dlatorne/SalishSeaCast/wwatch3/SoG_ww3_fields_20190930_20190930.nc
    /scratch/dlatorne/SalishSeaCast/wwatch3/SoG_ww3_fields_20191231_20191231.nc
* decided to run on arbutus rather than using WWatch3-Cmd on salish or graham
* rsync-ed restart files from previous days to arbutus:
    cd /opp/wwatch3/nowcast/
    for ddmmm in 30apr 10may 23jul 05sep 17sep 29sep 30dec;
    do
      rsync -tv ${ddmmm}19/restart001.ww3 \
        arbutus.cloud:/nemoShare/MEOPAR/SalishSea/wwatch3-nowcast/${ddmmm}19/; 
    done
* rsync-ed nowcast-green currents files from run days to arbutus:
    cd /results2/SalishSea/nowcast-green.v201905
    rsync -tv 01may19/SalishSea_1h_20190501_20190501_grid_[UV].nc \
        arbutus.cloud:/nemoShare/MEOPAR/SalishSea/nowcast-green/01may19/; 
    rsync -tv 11may19/SalishSea_1h_20190511_20190511_grid_[UV].nc \
        arbutus.cloud:/nemoShare/MEOPAR/SalishSea/nowcast-green/11may19/; 
    rsync -tv 24jul19/SalishSea_1h_20190724_20190724_grid_[UV].nc \
        arbutus.cloud:/nemoShare/MEOPAR/SalishSea/nowcast-green/24jul19/; 
    for dd in 06 07 18 30;
    do
      rsync -tv ${dd}sep19/SalishSea_1h_201909${dd}_201909${dd}_grid_[UV].nc \
          arbutus.cloud:/nemoShare/MEOPAR/SalishSea/nowcast-green/${dd}sep19/; 
    done
    rsync -tv 31dec19/SalishSea_1h_20191231_20191231_grid_[UV].nc \
        arbutus.cloud:/nemoShare/MEOPAR/SalishSea/nowcast-green/31dec19/; 
* changed config ``weather[file template]`` to "ops_{:y%Ym%md%d}.nc" for 2019
* launched runs:
    make_ww3_wind_file arbutus nowcast 2019-05-01
    make_ww3_current_file arbutus nowcast 2019-05-01
    run_ww3 arbutus nowcast 2019-05-01
    make_ww3_wind_file arbutus nowcast 2019-05-11
    make_ww3_current_file arbutus nowcast 2019-05-11
    run_ww3 arbutus nowcast 2019-05-11
    download_wwatch3_results arbutus nowcast 2019-05-11
* uploaded fields files from skookum to graham:
    cd /opp/wwatch3/nowcast/
    rsync -tv 01may19/SoG_ww3_fields_20190501_20190501.nc \
      graham-dtn:/scratch/dlatorne/SalishSeaCast/wwatch3/
    rsync -tv 11may19/SoG_ww3_fields_20190511_20190511.nc \
      graham-dtn:/scratch/dlatorne/SalishSeaCast/wwatch3/
* restored config ``weather[file template]`` to "hrdps_{:y%Ym%md%d}.nc" for 2019 via ``git stash``


Thu 5-Oct-2023
^^^^^^^^^^^^^^

Email to Jen re: annual review form for performance/merit this year.

crop_gribs 12 stalled with 1 file uncropped; expect recovery at ~10:30; succeeded
Backfill nowcast-agrif runs:
  upload_forcing orcinus nowcast+ 2023-10-03
  upload_forcing orcinus nowcast+ 2023-10-04
  wait for nowcast-agrif run to fail at ~11:45
  upload_forcing orcinus turbidity 2023-10-03
  wait for run to finish; took >3h
  upload_forcing orcinus turbidity 2023-10-04
  wait for run to finish; took >3h
(SalishSeaCast)

Sent email to graham support asking if we can avoid purge of /scratch/dlatorne/SalishSeaCast/
on 15-Oct because Jose is resuming use of those files.

Contined backfilling missing 2019 wwatch3 runs for Jose:
  wait for today's forecast run to finish at ~14:00
  git stash pop  # modify config
  make_ww3_wind_file arbutus nowcast 2019-07-24
  make_ww3_current_file arbutus nowcast 2019-07-24
  wait for nowcast run to finish
  kill forecast watcher
  kill forecast run
  rsync -tv 24jul19/SoG_ww3_fields_20190724_20190724.nc \
    graham-dtn:/scratch/dlatorne/SalishSeaCast/wwatch3/
  make_ww3_wind_file arbutus nowcast 2019-09-06
  make_ww3_current_file arbutus nowcast 2019-09-06
  wait for nowcast run to finish
  kill forecast watcher
  kill forecast run
  rsync -tv 06sep19/SoG_ww3_fields_20190906_20190906.nc \
    graham-dtn:/scratch/dlatorne/SalishSeaCast/wwatch3/
  make_ww3_wind_file arbutus nowcast 2019-09-07
  make_ww3_current_file arbutus nowcast 2019-09-07
  wait for nowcast run to finish
  kill forecast watcher
  kill forecast run
  rsync -tv 07sep19/SoG_ww3_fields_20190907_20190907.nc \
    graham-dtn:/scratch/dlatorne/SalishSeaCast/wwatch3/
  git stash  # restore production config


Fri 6-Oct-2023
^^^^^^^^^^^^^^

Finished backfilling nowcast-agrif runs:
  wait for nowcast-agrif run to fail at ~09:45
  upload_forcing orcinus turbidity 2023-10-05
  wait for run to finish
  upload_forcing orcinus turbidity 2023-10-06
(SalishSeaCast)

Watched recording of Wednesday's SharcNet seminar on job wait times and cluster state analysis
by James Desjardins (Brock): Exploring job wait times on Alliance compute clusters: a holistic view
* jadesjardins/show_jobs repo on GitHub notebook used for analysis
* vast majority of accounts are active ~20% of the time
* vast majority of jobs start within 20 minutes
  * 1 core 100M jobs almost always run fast regardless of priority; crack-filling
    useful for interactive jobs?
* partition-stats
* clusterstats
* wait time has almost negligible affect on priority

Contined backfilling missing 2019 wwatch3 runs for Jose:
  wait for today's forecast run to finish at ~12:00
  git stash pop  # modify config
  make_ww3_wind_file arbutus nowcast 2019-09-18
  make_ww3_current_file arbutus nowcast 2019-09-18
  wait for nowcast run to finish
  kill forecast watcher
  kill forecast run
  rsync -tv 18sep19/SoG_ww3_fields_20190918_20190918.nc \
    graham-dtn:/scratch/dlatorne/SalishSeaCast/wwatch3/
  make_ww3_wind_file arbutus nowcast 2019-09-30
  make_ww3_current_file arbutus nowcast 2019-09-30
  wait for nowcast run to finish
  kill forecast watcher
  kill forecast run
  rsync -tv 30sep19/SoG_ww3_fields_20190930_20190930.nc \
    graham-dtn:/scratch/dlatorne/SalishSeaCast/wwatch3/
  make_ww3_wind_file arbutus nowcast 2019-12-31
  make_ww3_current_file arbutus nowcast 2019-12-31
  wait for nowcast run to finish
  kill forecast watcher
  kill forecast run
  rsync -tv 31dec19/SoG_ww3_fields_20191231_20191231.nc \
    graham-dtn:/scratch/dlatorne/SalishSeaCast/wwatch3/
Checked days after missing runs and found cold starts for:
  02may19
  12may19
  25jul19
  08sep19
  19sep19
  01oct19
  * Checked all runs and found more cold start dates; recorded findings in #salishseacast channel
    on Slack
  * rsync-ed nowcast-green currents files from cold start run days to arbutus:
      cd /results2/SalishSea/nowcast-green.v201905
      rsync -tv 02may19/SalishSea_1h_20190502_20190502_grid_[UV].nc \
          arbutus.cloud:/nemoShare/MEOPAR/SalishSea/nowcast-green/02may19/; 
      rsync -tv 12may19/SalishSea_1h_20190512_20190512_grid_[UV].nc \
          arbutus.cloud:/nemoShare/MEOPAR/SalishSea/nowcast-green/12may19/; 
      rsync -tv 25jul19/SalishSea_1h_20190725_20190725_grid_[UV].nc \
          arbutus.cloud:/nemoShare/MEOPAR/SalishSea/nowcast-green/25jul19/; 
      rsync -tv 08sep19/SalishSea_1h_20190908_20190908_grid_[UV].nc \
          arbutus.cloud:/nemoShare/MEOPAR/SalishSea/nowcast-green/08sep19/; 
      rsync -tv 19sep19/SalishSea_1h_20190919_20190919_grid_[UV].nc \
          arbutus.cloud:/nemoShare/MEOPAR/SalishSea/nowcast-green/19sep19/; 
      rsync -tv 01oct19/SalishSea_1h_20191001_20191001_grid_[UV].nc \
          arbutus.cloud:/nemoShare/MEOPAR/SalishSea/nowcast-green/01oct19/; 
  * backfill 2019 cold start runs:
      make_ww3_wind_file arbutus nowcast 2019-05-02
      make_ww3_current_file arbutus nowcast 2019-05-02
      wait for nowcast run to finish
      kill forecast watcher
      kill forecast run
      rsync -tv 02may19/SoG_ww3_fields_20190502_20190502.nc \
        graham-dtn:/scratch/dlatorne/SalishSeaCast/wwatch3/
      make_ww3_wind_file arbutus nowcast 2019-05-12
      make_ww3_current_file arbutus nowcast 2019-05-12
      wait for nowcast run to finish
      kill forecast watcher
      kill forecast run
      rsync -tv 12may19/SoG_ww3_fields_20190512_20190512.nc \
        graham-dtn:/scratch/dlatorne/SalishSeaCast/wwatch3/
      git stash  # restore production config

JRA arrived for the weekend.


Sat 7-Oct-2023
^^^^^^^^^^^^^^

wwatch3 forecast2 run failed because I forgot to restore the production config
after yesterday's backfilling work; killed watcher and skipped run
make_ww3_wind_file forecast stalled; killed and re-ran it
(SalishSeaCast)


Sun 8-Oct-2023
^^^^^^^^^^^^^^

make_ww3_wind_file forecast2 stalled; killed it and skipped run
(SalishSeaCast)


Week 41
-------

Mon 9-Oct-2023
^^^^^^^^^^^^^^

**Statutory Holiday** - Thankgiving

make_ww3_current_file forecast failed to launch; killed and re-ran it
(SalishSeaCast)

Drove to White Rock to take JRA home and have dinner at Amica.


Tue 10-Oct-2023
^^^^^^^^^^^^^^^

Group mtg; see whiteboard.
(MOAD)

Helped Jake prepare to use Reshapr for extractions from Susan's 202111 outfall runs.

Helped Ilias get logged in to char console.

Updated pkgs & versions in dev env.
Started work on extraction config YAML file docs.
(Reshapr)

crop_gribs 12 stalled with 1 file to process; resolved at ~10:30
make_ww3_wind_file and make_ww3_current_file forecast failed to launch; killed and re-ran them
Contined backfilling 2019 wwatch3 cold start runs for Jose:
  wait for today's forecast run to finish at ~15:15
  git stash pop  # modify config
  make_ww3_wind_file arbutus nowcast 2019-07-25
  make_ww3_current_file arbutus nowcast 2019-07-25
  wait for nowcast run to finish
  kill forecast watcher
  kill forecast run
  rsync -tv 25jul19/SoG_ww3_fields_20190725_20190725.nc \
    graham-dtn:/scratch/dlatorne/SalishSeaCast/wwatch3/
  make_ww3_wind_file arbutus nowcast 2019-09-08
  make_ww3_current_file arbutus nowcast 2019-09-08
  wait for nowcast run to finish
  kill forecast watcher
  kill forecast run
  rsync -tv 08sep19/SoG_ww3_fields_20190908_20190908.nc \
    graham-dtn:/scratch/dlatorne/SalishSeaCast/wwatch3/
(SalishSeaCast)

Squash-merged dependabot PRs to update gitpython re: CVE-2023-41040 re: DoS vulnerability:
* SalishSeaCmd
* NEMO-Cmd
* AtlantisCmd
* SalishSeaNowcast


Wed 11-Oct-2023
^^^^^^^^^^^^^^^

crop_gribs 12 stalled with 1 file to process; resolved at ~10:30
make_ww3_current_file forecast failed to launch; killed and re-ran it
Finished backfilling 2019 wwatch3 cold start runs for Jose:
  wait for today's forecast run to finish at ~14:15
  git stash pop  # modify config
  make_ww3_wind_file arbutus nowcast 2019-09-19
  make_ww3_current_file arbutus nowcast 2019-09-19
  wait for nowcast run to finish
  kill forecast watcher
  kill forecast run
  rsync -tv 19sep19/SoG_ww3_fields_20190919_20190919.nc \
    graham-dtn:/scratch/dlatorne/SalishSeaCast/wwatch3/
  make_ww3_wind_file arbutus nowcast 2019-10-01
  make_ww3_current_file arbutus nowcast 2019-10-01
  wait for nowcast run to finish
  kill forecast watcher
  kill forecast run
  rsync -tv 01oct19/SoG_ww3_fields_20191001_20191001.nc \
    graham-dtn:/scratch/dlatorne/SalishSeaCast/wwatch3/
  git restore config/nowcast.yaml
(SalishSeaCast)

xarray office hours:
* xarray tutorial site: https://tutorial.xarray.dev/intro.html
* Dataset.pipe() applies function to 
* apply_ufunc() is for use with numpy functions, not functions that use xarray data structures
* asked about dask threads vs. clusters; my experience is not unique
  * big or complex workflows generally require a cluster; clusters can blow up
  * cubed; early stage project that might 
* kerchunk; compromise between zarr and native netCDF
  * one big metadata file
  * takes time to generate; what does that imply for adding daily runs
* datatree will handle hdf5 groups in files; xarray.datatree()
* in dev fancier HTML repr for notebooks: https://github.com/pydata/xarray/issues/8171#issuecomment-1721324406

Started fixing xarray.Dataset.resample() loffset parameter deprecation bug
* issue #82
* PR #92
* branch: loffset-deprecation
* Created issue #93 re: ``reshapr info`` fail for user-provided model profile or cluster 
  description.
(Reshapr)

Discussed Reshapr model profiles for wastewater runs w/ Susan.
Created example model profile and extraction config files for Jake in analysis-doug/wastewater/.


Thu 12-Oct-2023
^^^^^^^^^^^^^^^

make_ww3_current_file forecast2 failed to launch; killed and skipped run
LiveOcean had a bad day; download completed at 11:07
(SalishSeaCast)

UBC-IOS modeling mtg; Susan talked about historic low Fraser discharge in 9-23 Jul 2023.

Team mtg.
(Atlantis)


Fri 13-Oct-2023
^^^^^^^^^^^^^^^

LiveOcean had another bad day; download completed at 11:08
(SalishSeaCast)

Phys Ocgy seminar: Jose's microfibres work.

1.20.2 versions of Malilib, MiniHUD & Tweakeroo have been released; successfully tested in 
single player creative copy of Nodecraft world.

Cloned my fork of xarray on to khawla.


Sat 14-Oct-2023
^^^^^^^^^^^^^^^

upload_forcing graham turbidity failed; re-ran successfully
(SalishSeaCast)

Updated Nodecraft server to 1.20.2:
* stopped server
* created backup: Talking Falcon's Punching Fist
* used Once Click Installer to change versions of game and fabric:
  * game: 1.20.2
  * fabric: 1.20.2-0.14.23
  * archive install
* copied files from _old_files to /:
  * banned-ips.json
  * banned-players.json
  * ops.json
  * server.properties
  * whitelist.json
* copied world folder to /:
  * 1-20-1-25jul23
* started server


Sun 15-Oct-2023
^^^^^^^^^^^^^^^

make_ww3_current_file forecast failed to launch; killed and re-ran it
(SalishSeaCast)


Week 42
-------

Mon 16-Oct-2023
^^^^^^^^^^^^^^^

make_ww3_current_file forecast2 failed to launch; killed and skipped run
(SalishSeaCast)

Started update to Python 3.12
* branch: py312
* PR#68
* GHA pytest-with-coverage workflow was successful; much closer to 3.12 release this year
  than was the case for 3.11 last year :-)
* thought about Python version support:
  * we no longer depend on Python module version on graham because we use conda env there
  * present oldest support is 3.10, environment-hpc uses 3.11; could drop 3.10 since group is all
    new to graham in 2023, so they are using 3.11
(NEMO-Cmd)

graham /scratch purge removed ~200 wwatch3 files and ~300 NEMO files
* ran rsync on salish to restore purged files:
    cd /opp/wwatch3/nowcast/
    rsync -tv *19/SoG_ww3_fields_*.nc graham-dtn:/scratch/dlatorne/SalishSeaCast/wwatch3/

    cd /results2/SalishSea/nowcast-green.202111/
    rsync -tv *19/SalishSea_1h_2019*_grid_[TUVW].nc graham-dtn:/scratch/dlatorne/SalishSeaCast/NEMO

Squash-merged dependabot PRs to update mamba-org/setup-micromamba to 1.5.0:
* SalishSeaNowcast
* gha-workflows

Started update to Python 3.12
* branch: py312
* PR#49
* GHA pytest-with-coverage workflow was successful; much closer to 3.12 release this year
  than was the case for 3.11 last year :-)
* thought about Python version support:
  * we no longer depend on Python module version on graham because we use conda env there
  * present oldest support is 3.10, environment-hpc uses 3.11; could drop 3.10 since group is all
    new to graham in 2023, so they are using 3.11
* added workflow_dispatch trigger to GHA pytest-with-coverage workflow
(SalishSeaCmd)

Started update to Python 3.12
* branch: py312
* PR#38
* GHA pytest-with-coverage workflow was successful; much closer to 3.12 release this year
  than was the case for 3.11 last year :-)
* added workflow_dispatch trigger to GHA pytest-with-coverage workflow
(NEMO_Nowcast)

Started update to Python 3.12
* branch: py312
* PR#209
* added workflow_dispatch trigger to GHA pytest-with-coverage workflow
* **GHA pytest-with-coverage workflow with 3.12 installed 3.11**
(SalishSeaNowcast)

Started update to Python 3.12
* branch: py312
* PR#23
* GHA pytest-with-coverage workflow was successful; much closer to 3.12 release this year
  than was the case for 3.11 last year :-)
* added workflow_dispatch trigger to GHA pytest-with-coverage workflow
(AtlantisCmd)

Started update to Python 3.12
* branch: py312
* PR#43
* also added 3.11 to test matrix
* GHA pytest-with-coverage workflow was successful; much closer to 3.12 release this year
  than was the case for 3.11 last year :-)
* added workflow_dispatch trigger to GHA pytest-with-coverage workflow
(moad_tools)

Started update to Python 3.12
* branch: py312
* PR#43
* also added 3.11 to test matrix
* GHA pytest-with-coverage workflow was successful; much closer to 3.12 release this year
  than was the case for 3.11 last year :-)
* added workflow_dispatch trigger to GHA pytest-with-coverage workflow
(salishsea-site)

Started update to Python 3.12
* branch: py312
* PR#37
* GHA sphinx-linkcheck workflow failed:
    conda-forge/linux-64                                        Using cache
      conda-forge/noarch                                          Using cache
      error    libmamba Could not solve for environment specs
          The following packages are incompatible
          ├─ python 3.10**  is requested and can be installed;
          └─ python 3.12**  is not installable because there are no viable options
            ├─ python 3.12.0 conflicts with any installable versions previously reported;
            └─ python 3.12.0rc3 would require
                └─ _python_rc, which does not exist (perhaps a missing channel).
      critical libmamba Could not solve for environment specs
* added workflow_dispatch trigger to GHA pytest-with-coverage workflow
(SalishSeaCast docs)

Finished fixing xarray.Dataset.resample() loffset parameter deprecation bug
* issue #82
* PR #92; squash-merged
* branch: loffset-deprecation
* Used VSCode ``month-avg.202111 /results2/SalishSea [SSH: salish]`` session on salish
  in reshapr env to run in ``/results2/SalishSea/month-avg.202111/``:
    ``python3 -m day_avg 2023-09-01`` 
  got FutureWarning exceptions as in the past
* Switched /SalishSeaCast/Reshapr clone to loffset-deprecation branch and ran:
    ``python3 -m day_avg 2023-09-02`` 
  success with no FutureWarning exceptions :-)
Started update to Python 3.12
* branch: py312
* PR#94
* GHA pytest-with-coverage workflow was successful; much closer to 3.12 release this year
  than was the case for 3.11 last year :-)
* added workflow_dispatch trigger to GHA pytest-with-coverage workflow
(Reshapr)

FInalized and pushed example model profile and extraction config files for Jake in 
analysis-doug/wastewater/.

Updated to PyCharm 2023.2.3 on khawla, mostly to get f-strings PEP-701 support in Python 3.12.


Tue 17-Oct-2023
^^^^^^^^^^^^^^^

make_ww3_[wind|current]_file forecast2 failed to launch; killed and re-ran them
slow LiveOcean
(SalishSeaCast)

Group mtg; see whiteboard.
(MOAD)

Helped Ilias with ssh keys on Windows.

Helped Becca with xarray access to ERDDAP and cleaning an accidentally pushed large
file on perigee.


Wed 18-Oct-2023
^^^^^^^^^^^^^^^

Squash-merged dependabot PRs to update urllib3 re: CVE-2023-45803 303 redirect vulnerability:
* MOAD/docs
* tools/SalishSeaTools
* AtlantisCmd
* SalishSeaNowcast
* Reshapr
* moad_tools
* salishsea-site
* SalishSeaCast/docs
* NEMO-Cmd
* MoaceanParcels
* cookiecutter-analysis-repo
* SalishSeaCmd
* NEMO_Nowcast
* cookiecutter-MOAD-pypkg
* cookiecutter-djl-pypkg
* SOG-Bloomcast-Ensemble

Added linux.die.net/man/1/scp to linkcheck ignore list to prevent 
"403 Client Error: Forbidden" errors when checked from the GitHub Actions 
sphinx-linkcheck workflow. Guessing that the server owners don't like their 
content being accessed by automation.
(MOAD docs)

Improved graham docs re: Miniforge setup.
Added sq alias to format squeue output.
Fixed broken and redirected links.
(SalishSeaCast docs)


Thu 19-Oct-2023
^^^^^^^^^^^^^^^

Started writing example section re: extractions for Iona wastewater analysis and other research
run processing.
(Reshapr)

Reviewed and tweaked Ilias's updates to ssh access docs for Windows.
(MOAD docs)


Fri 20-Oct-2023
^^^^^^^^^^^^^^^

Started work on issue #93 re: reshapr info handling user-provided model profile or cluster
description.
branch: 93-info-user-profile-cluster
PR#97: squash-merged
* updated dev env pkg versions
* added type hints to function docstrings in info module
* added handling for user-provided model profiles and cluster descriptions to `reshapr info`
Discovered that my resolution of #93 was flawed; checking for file existence can only work for
cluster or model profile not both :-(
Updated wastewater example docs to show use of user model profile in reshapr info.
(Reshapr)


Sat 21-Oct-2023
^^^^^^^^^^^^^^^

make_ww3_current_file forecast2 failed to launch; blocked forecast run; killed it and skipped run
make_ww3_wind_file forecast stalled; killed and re-ran it
make_ww3_current_file forecast failed to launch; killed and re-ran it
(SalishSeaCast)


Sun 22-Oct-2023
^^^^^^^^^^^^^^^

make_ww3_current_file forecast2 stalled; killed it and skipped run
crop_gribs 12 stalled with 1 file left to process; completed at 10:32
(SalishSeaCast)


Week 43
-------

Mon 23-Oct-2023
^^^^^^^^^^^^^^^

Explored Raisha'a %e/%d format issue; remembered how little I like programming in C.
(Atlantis)

Drop handling of user-provided cluster config in reshapr info;
we can only use file existence for cluster or model profile, and the latter is the more
important use case
branch: drop-user-cluster-info
PR#98; squash-merged

Finished writing example section re: extractions for Iona wastewater analysis and other research
run processing.
branch: wastewater-example
PR#96 - squash-merged
(Reshapr)

Helped Ilias with analysis env build:
* char stalled
* change to nodefaults channel (fixed on GitHub)
* pin python=3.11

Benchmarked analysis env builds on chum:
* 1st try with lots of dowloads: 19m54.107s
* mamba: 7m14.065s  # benefits from download caching
* conda to see effect of cached downloads: 8m36.036s
* conda with python=3 instead of python=3.11 almost blew memory into swap-land !! :-(


Tue 24-Oct-2023
^^^^^^^^^^^^^^^

Worked at ESB

Took kudu to ESB as my leave-there laptop.

Group mtg; see whiteboard.
(MOAD)

Helped Ilias sort out nested dirs in his analysis-ilias and conda-envs setup.
Saw strange disappearing directories issue on /ocean. Told him to switch to /data/.

Set up 1password ssh agent on kudu.

make_ww3_current_file forecast2 stalled; killed it and skipped run
make_ww3_wind_file forecast stalled; killed it and re-ran
(SalishSeaCast)

Helped Jake with coordinates mismatch between Reshapr-generated day-avg files
in 202111 and ncra-generated files in Susan's runs.

Prepared to modernize packaging.
(Reshapr)

Got COVID & flu vaccinations.

Reported disappearing directories that I saw with Ilias on /ocean to Hentryk
on EOAS Slack. He replied that /ocean storage array is optimal, might be an NFS issue.


Wed 25-Oct-2023
^^^^^^^^^^^^^^^

Feeling the effects of yesterday's dual vaccinations.

Helped Jake get started with Reshpr for Iona long run results.
Discovered that Susan didn't include standard_name attr for her outfall variable in her NEMO
output config; Reshapr doesn't like that.
* this should probably be resolved by using variable name as standard_name when neither
  standard_name nor short_name exist; that is sort of implied by 
  https://cfconventions.org/Data/cf-conventions/cf-conventions-1.10/cf-conventions.html#long-name

Continued conversation on EOAS Slack w/ Henryk re: char/ocean weirdness. He thinks it was an NFS issue.

Explored sphinx version limiting to 5.3.0; it's due to sphinx-rtd-theme version; won't move until
v2.0.0 of the latter is released.
Added fallback to use variable name as standard_name when source dataset variable lacks both 
standard_name and short_name attributes:
branch: std_name_fallback
PR#99 - squash-merged
* motivated by Susan not including standard_name for outfall tracer variable; this won't likely be  
  the first time someone does that...
(Reshapr)


Thu 26-Oct-2023
^^^^^^^^^^^^^^^

make_ww3_current_file forecast2 stalled; killed it and skipped run
make_ww3_wind_file forecast stalled; killed it and re-ran
(SalishSeaCast)

Started work to update SalishSeaCmd re: sockeye migration to SLURM:
* load env on sockeye with:
    module load Software_Collection/ARC_2023
* new git modules: 2.31.8 and 2.41.0; they required gcc/5.5.0 9.4.0
    module load gcc/5.5.0
    module load git/2.41.0
* pull updates into NEMO-Cmd and SalishSeaCmd
* used mamba to create new salishsea-cmd env
    cd SalishSeaCmd
    mamba env create -f envs/environment-hpc.yaml
    conda activate salishsea-cmd
    python3 -m pip install --user -e ../NEMO-Cmd
    python3 -m pip install --user -e .
* updated NEMO repos:
    grid
    NEMO-3.6-code  # changed default branch from master to main
    rivers-climatology
    SS-run-sets  # changed default branch from master to main
    tides
    tracers
    XIOS-2  # changed default branch from master to main
    XIOS-ARCH
* confirmed module loads for XIOS-2 build:
    module load gcc/5.5.0
    module load openmpi/4.1.1-cuda11-3
    module load netcdf-fortran/4.5.3-hdf4-support
    module load netcdf-cxx/4.2-hdf4-support
    module load perl/5.34.0
    module load perl-uri/1.72
* cleaned and built XIOS-2
    ./tools/FCM/bin/fcm build --clean
    ./make_xios --arch GCC_SOCKEYE
  * success!
* cleaned and built NEMO SalishSeaCast config and REBUILD_NEMO
    ./makenemo -n SalishSeaCast clean
    XIOS_HOME=$PROJECT/$USER/MEOPAR/XIOS-2 ./makenemo -n SalishSeaCast -m GCC_SOCKEYE
    success!
    cd ../TOOLS
    XIOS_HOME=$PROJECT/$USER/MEOPAR/XIOS-2/ ./maketools -n REBUILD_NEMO -m GCC_SOCKEYE
    success
* changed run module to use sbatch directives on sockeye:
  * branch: sockeye-slurm
  * PR#51
* pulled sockeye-slurm branch on to sockeye
(SalishSeaCmd)


Fri 27-Oct-2023
^^^^^^^^^^^^^^^

Phys Ocgy seminar: Puget Sound HABs by Cheryl Greengrove from the University of Washington Tacoma.

AAPS AGM.

Continued work on separating dataset descriptions into files to be composed into
dataset.xml by a script:
* branch: separate-dataset-files
* PR#1
* Started migrating SalishSeaCast NEMO rolling forecast datasets to
  ssc-nemo-201905/rolling-forecasts/
  * rolling-forecasts/ubcSSfHalfmoonBaySSH10m.xml
(erddap-datasets)



Sat 28-Oct-2023
^^^^^^^^^^^^^^^

Updated pkg to Python 3.12.
branch: py312
PR#94 - squash-merged
Updated readthedocs build config:
* change to mambaforge-22.9
* pin versions of sphinx, sphinx-notfound-page & sphinx-rtd-theme
  * re: build reproducibility: 
    https://docs.readthedocs.io/en/stable/guides/reproducible-builds.html
* add commonmark to dependencies in environment-rtd
  * re: changes to default project depencencies: 
    https://blog.readthedocs.com/defaulting-latest-build-tools/
* added pandas to autodoc import mocks list to resolve warning in API docs section
branch: update-readthedocs-build
PR#100 - squash-merged
(Reshapr)

Helped Susan update her sockeye setup to test my SalishSeaCmd changes:


Sun 29-Oct-2023
^^^^^^^^^^^^^^^

Helped Susan update her sockeye setup to test my SalishSeaCmd changes:
* libnetcdf and libnetcdff not found in ldd of xios & nemo executables

make_ww3_wind_file forecast stalled; killed it and re-ran
(SalishSeaCast)


Week 44
-------

Mon 30-Oct-2023
^^^^^^^^^^^^^^^

make_ww3_wind_file forecast2 stalled; killed and re-ran it and make_CHS_current_file
LiveOcean was slow; download timed out at 11:37, but succeeded when I re-tried the worker at 12:02
(SalishSeaCast)

Squash-merged dependabot PRs to update setup-micromamba re: it updating to nodejs=20:
* gha-workflows
* SalishSeaNowcast

Fixed broken links for HRDPS information page.
(SalishSeaNowcast)

Modernized packaging:
* branch: modernize-pkg
* PR#101 - squash-merged
* used SalishSeaNowcast PR#144 as guidance
  * metadata to pyproject.toml
  * chg to hatchling
  * chg to importlib.metadata.version()
  * move __version__ to __about__
  * add pkg installation to environment-rtd
  * update requirements.txt
* add version release notes; see SalishSeaNowcast PR#145
* change badges layout in README & dev docs to table
Released version 23.1 and bumped to 23.2.dev0 for next dev cycle
(Reshapr)


Tue 31-Oct-2023
^^^^^^^^^^^^^^^

Worked at ESB,

Group mtg; see whiteboard.
(MOAD)

make_ww3_wind_file forecast2 stalled; killed it and skipped run
stalled make_ww3_wind_file prevent automation from launching nowcast/forecast
runs; re-ran manually to restart automation
(SalishSeaCast)

EOAS Colloquium: Hal Bradbury: Carbon in Marine Sediments

Continued work on separating dataset descriptions into files to be composed into
dataset.xml by a script:
* branch: separate-dataset-files
* PR#1
* Started migrating SalishSeaCast NEMO rolling forecast datasets to
  ssc-nemo-201905/rolling-forecasts/
  * rolling-forecasts/ubcSSfNanaimoSSH10m.xml
  * rolling-forecasts/ubcSSfNeahBaySSH10m.xml
  * rolling-forecasts/ubcSSfNewWestminsterSSH10m.xml
  * rolling-forecasts/ubcSSfPatriciaBaySSH10m.xml
(erddap-datasets)

Asked Henryk to consider rebooting ocean file server or restarting its NFS service due to more
intermittent file existence issues reported by Cassidy and Becca.

Coffee w/ Ilias.


November
--------

Wed 1-Nov-2023
^^^^^^^^^^^^^^

Jake reported messed up time coordinate values in month-average extractions;
confirmed; but in new time offset calculation for arbitrary dataset time spans;
created issue #102.
(Reshapr)

Gave Cassidy guidance on how to use ``salishsea split-results`` on graham or an ocean machine.

Continued work on separating dataset descriptions into files to be composed into
dataset.xml by a script:
* branch: separate-dataset-files
* PR#1
* Started migrating SalishSeaCast NEMO rolling forecast datasets to
  ssc-nemo-201905/rolling-forecasts/
  * rolling-forecasts/ubcSSfPatriciaBaySSH10m.xml
  * rolling-forecasts/ubcSSfPointAtkinsonSSH10m.xml
  * rolling-forecasts/ubcSSfPortRenfrewSSH10m.xml
(erddap-datasets)


Henryk proposed setting up performance monitoring on ocean NFS service so that we can try to 
better characterize the issue that people are seeing.
* Ilias reproduced his git clone tools issue
* Becca reported notebook not found issue on perigee@UW, so possible VSCode issue; found
  https://github.com/microsoft/vscode/issues/196740 that points at Pylance version

Re-tried XIOS-2 build on sockeye after default Software_Collection update; eventually got to:
  ``NETCDF_LIB="-Wl,-rpath=$NETCDF_FORTRAN_ROOT/lib -L$NETCDF_FORTRAN_ROOT/lib -lnetcdff -Wl,-rpath=$NETCDF_C_ROOT/lib -L$NETCDF_C_ROOT/lib -lnetcdf"``
in arch-GCC_SOCKEYE.path;
not as brittle as I feared from my initial read of Roman's message.
For NEMO, changed arch-GCC_SOCKEYE.fcm:
  ``%NCDF_LIB            -Wl,-rpath=$NETCDF_FORTRAN_ROOT/lib -L$NETCDF_FORTRAN_ROOT/lib -lnetcdff -Wl,-rpath=$NETCDF_C_ROOT/lib -L$NETCDF_C_ROOT/lib -lnetcdf``
and
  ``%XIOS_LIB            -L%XIOS_HOME/lib -lxios``
Susan replicated these changes and did test run; time steps!!


Thu 2-Nov-2023
^^^^^^^^^^^^^^

Cancelled planned participation in Fire Across the Land session due to illness.

make_ww3_wind_file forecast2 stalled; killed it and skipped run
(SalishSeaCast)

Squash-merged dependabot PRs to update pip re: CVE-2023-5752 re: hg clone config injection 
vulnerability:
* cookiecutter-analysis-repo
* cookiecutter-MOAD-pypkg
* NEMO-Cmd
* MoaceanParcels
* gha-workflows
* salishsea-site
* SalishSeaNowcast
* NEMO_Nowcast
* SalishSeaCast/docs
* SalishSeaCmd
* AtlantisCmd
* tools/SalishSeaTools
* moad_tools
* MOAD/docs


Fri 3-Nov-2023
^^^^^^^^^^^^^^

Phys Ocgy seminar: Bernie Yang from C-PROOF at UVic: Characterizing the lateral mixing of mesoscale 
eddies using underwater gliders


Continued work on separating dataset descriptions into files to be composed into
dataset.xml by a script:
* branch: separate-dataset-files
* PR#1
* Finished migrating SalishSeaCast NEMO rolling forecast datasets to
  ssc-nemo-201905/rolling-forecasts/
  * rolling-forecasts/ubcSSfSandHeadsSSH10m.xml
  * rolling-forecasts/ubcSSfSandyCoveSSH10m.xml
  * rolling-forecasts/ubcSSfSquamishSSH10m.xml
  * rolling-forecasts/ubcSSfVictoriaSSH10m.xml
  * rolling-forecasts/ubcSSfWoodwardsLandingSSH10m.xml
* Migrated 201702 season-averaged, depth-averaged T&S fields dataset to
  * ssc-nemo-201702/ubcSSg2DTracerFieldsSeasonalV17-02.xml
(erddap-datasets)


Sat 4-Nov-2023
^^^^^^^^^^^^^^

Dinner at l'Abitoir for Susan's bday.


Sun 5-Nov-2023
^^^^^^^^^^^^^^

Experimented with running wwatch3 on fvcom VMs:
* created ``mpi_hosts.wwatch3``:
    192.168.238.12  slots=15 max-slots=16  # fvcom0
    192.168.238.7   slots=15 max-slots=16  # fvcom1
    192.168.238.20  slots=15 max-slots=16  # fvcom2
    192.168.238.11  slots=15 max-slots=16  # fvcom3
    192.168.238.9   slots=15 max-slots=16  # fvcom4
* hacked run_ww3 worker to use ``mpi_hosts.wwatch3`` and rsync-ed it to arbutus for test
  tomorrow
(SalishSeaCast)


Week 45
-------

Mon 6-Nov-2023
^^^^^^^^^^^^^^

make_ww3_[wind|current]_file forecast2 both stalled; killed and re-ran them to test wwatch3
running concurrently with NEMO on different VMs:
* run started successfully
* maybe slightly slower: 93 vs. 99 time steps in 1st 5 minutes, 192 vs 201 in 10min, 291 vs 300,
  390 vs 405, 498 vs 507
* run finished sucessfully
make_ww3_current_file forecast stalled; killed and re-ran it
* wondering if stalls are due to file system "congestion" due to wwatch3 prep workers running while
  results of preceding NEMO run results are being downloaded; nowcast-green results download took
  ~35min!!
(SalishSeaCast)

Updated khawla to Pycharm 2023.2.4

Commit and push change to netcdf-fortran/4.6.0 in XIOS-ARCH for graham that was somehow
overlooked in April.
Updated sockeye lib path re: 2023 software stack's need for ``-Wl,-rpath=`` linker options
for netcdf and netcdf-fortran libraries.
(XIOS-ARCH)

Clone repo on khawla; remarkable that it wasn't there already!
Updated sockeye lib path re: 2023 software stack's need for ``-Wl,-rpath=`` linker options
for netcdf and netcdf-fortran libraries.
(NEMO-3.6-CODE)

Worked on plans for ocean file system and server maintenance on Saturday 11nov.

Finished work to update SalishSeaCmd re: sockeye migration to SLURM:
* branch: sockeye-slurm
* PR#51 - squash-merged
(SalishSeaCmd)

Built Python 3.12 dev env on khawla with sphinx version pins and removal of feedgen pin.
Started work on changing wwatch3 runs timing:
* branch: update_ww3-runs
* PR#213
* added mpi hosts file to config so that wwatch3 can run on different VMs to NEMO
* pulled branch on arbutus to test; not much different to yesterday's hack that didn't get tested
  today due to prep worker stalls
(SalishSeaNowcast)

Continued work on separating dataset descriptions into files to be composed into
dataset.xml by a script:
* branch: separate-dataset-files
* PR#1
* Added ip address of dataforseo.com
  (Estonian SEO company that swamped the server with failed requests on 22sep23)
  to prefix requestsBlacklist element
* Changed dev env to Python 3.12
* Added GHA workflow to run check_datasets_xml.py on push or from web interface;
  also added test env description
* Added Dependabot config to monitor Actions versions
* Replaced deconstructed datasets.xml with one generated by build_datasets_xml.py
* Pulled PR on skookum and restarted ERDDAP to test new datasets.xml
Messed around with UptimeRobot settings to try to get notifications.
(erddap-datasets)


Tue 7-Nov-2023
^^^^^^^^^^^^^^

Very windy ride to work at ESB.

Group mtg; see whiteboard.
(MOAD)

Slack discussion w/ Jake on how to access nowcast-green.202111 via Reshapr.

Updated PyCharm on kudu to 2023.2.4.

Started work on changing wwatch3 runs timing:
* branch: update_ww3-runs
* PR#213
* changed next_workers to launch make_ww3_* prep workers for forecast2 run after NEMO forecast2
  results download finishes
* pulled branch on arbutus to test
* restarted manager on skookum for change to take effect
* discovered crop_gribs --backfill option code on skookum and shelved on khawla
(SalishSeaNowcast)


Wed 8-Nov-2023
^^^^^^^^^^^^^^

make_ww3_current_file forecast2 stalled; killed and re-ran it; so much for the hypothesis of
download_results interferring
collect_weather 00 was slow, so crop_gribs 00 timed out with 392 files not processed;
collect_weather 00 finished successfully after crop_gribs timeout;
hacked crop_gribs --backfill back into production from shelved code, and it cleaned things up
successfully
(SalishSeaCast)

GitHub Universe 2023:
* keynote:
  * Thomas Dohmke, CEO
    * "GitHub re-founded on Copilot"
  * Wllison Weins
    * Copilot chat
    * in VSCode and PyCharm, on GitHub mobile
    * included in existing subscriptions in Dec
  * Kedasha Kerr
    * Copilot Chat now in GitHub.com for:
      * code explanation
      * PR descriptions
      * security scanning auto-fixes in PRs; in preview today
      * secret scanning; in preview today
      * regex assistant; in security subscriptions
  * Colin Merkl
    * Copilot customized to your org
    * per-org advanced fine tuning
    * 3rd party connection to Sentry, etc.
  * Copilot Enterprise in Feb for US$39/mo
  * Satya Nadella
    * philosophizing and promoting
  * One more thing...
    * Copilot Workspace; 2024 release
* Copilot
  * Ryan Salva
  * Accenture
  * DevEx
    * Harold Kirschner, VSCode
      * multi-model
  * custom models
    * repo data
    * suggestion acceptance
    * reinforcement learning from human feedback (RLFHF)
    * "eat our own dogfood" -> "drink our own champagne"
    * Alexander Androncik, AMD
  * integrations with services
    * Shutin Zhao
    * Copilot extensibility
      * expand knowledge via project-specific doc sets
      * extend via plugins
* AI-powered security
  * Mike Hanley
    * security feedback is delayed in CI flow vs. code creation
    * in-editor security analysis; pro-active instead of reactive
  * Asha Chakrabarty
    * code scanning auto-fix; AI code in PR
    * secret scanning can detect passwords; AI assistance for custom pattern regexs
* Copilot at Shopify
  * Farhan Thawar, VP and Head of Engineering

Continued work on trying to get make_ww3_* robust again:
* branch: update_ww3-runs
* PR#213
* dropped change to next_workers to launch make_ww3_* prep workers for forecast2 run after NEMO 
  forecast2 results download finishes; it had no effect; force-pushed to PR
* updated branch on skookum
* restarted manager on skookum for change to take effect
* added drop_vars and chunks to workers
  * rsync-ed changes to arbutus to test in debug mode and production tomorrow
  * still got a couple of hangs on debug runs of make_ww3_current_file; fewer tests of 
    make_ww3_wind_file
  * played with chunk size for time; no evident effact on memory use or execution time, so left
    it at 1
(SalishSeaNowcast)

Tried to address ongoing OutOfMemoryError emails from ERDDAP:
* increased JVM max heap size from -Xmx=96G to -Xmx=112G in skookum:/opt/tomcat/bin/startup.sh
  and restarted ERRDAP; no effect
* confirmed that 2008-12-19 grid_U file is not on ERDDAP; its storage size looks no different to 
  2008-12-20
* plotted surface current fields from 19th & 20th; no trouble loading 19th file
(ERDDAP)


Thu 9-Nov-2023
^^^^^^^^^^^^^^

download_wwatch3_results forecast2 stalled due to manager crash caused by KeyError on WWATCH3 run in checklist:
* probably due to yesterday's messing with timing and re-run of wwatch3 wwatch3-forecast2
* decided not to manually run update_forecast_datasets because forecast run will finish soon run it
  automatically
(SalishSeaCast)

GitHub Universe 2023:
* keynote:
  * Inbal Shani, Chief Product Officer
    * DevEx
  * Asha Chakrabarty, VP Product Mgmt
    * platform, tool, etc. agnostic  
    * security embedded in dev workflow
    * actions
    * ARM and M1 runners
  * Shuba Rao, VP Prodcut Strategy
    * Enterprise
    * migration tools for Bitbucket & Azure DevOps
    * repository properties: key-value metadata
      * repository rules: compliance at scale
  * Gerard McMahon, Fidelity
  * Stormy Peters, VP Communities
    * >7 billion action minutes last year
    * Patreon on GitHub
    * Accelerator 2, $400k, 20 projects
  * One more thing...
    * next year at Fort Mason, SF, 29-30 Oct, 10th anniversary
* DevEx
  * Mario Rodriguez, VP Product Mgmt
  * one platform, security baked in, less context switching, more flow
  * iteration velocity
  * demo of docs integration in Copilot
* Octoverse 2023
  * Martin Woodward
    * >100M devs, up 26% in 2023
    * >300M open source contributions in 2023
    * Canada dev community size has dropped from 8th to 10th over 10 years; not shrinking, surpassed
    * huge growth in Nigeria and other African countries
    * Singapore has highest per capita GitHub accounts
    * public activity on GitHub is only 20% of total
    * innersource == open source techniques in private orgs
* AI for Accessibility
  * Ed Summers, Head of Accessibility, blind dev
* AI: Superhero or super villain?
  * Scott Hanselman, VP Developer Community, Microsoft
    * If you are kind to AI you end up in the nice part of the corpus
    * use AI responsibly

Continued work on trying to get make_ww3_* robust again:
* branch: update_ww3-runs
* PR#213
* added drop_vars and chunks to workers after successful forecast2 and forecast run preps
* updated branch on skookum (with some git reset --hard drama due to yesterday's force-push)
Fixed malformed test assertion in test_update_forecast_dataset; unitest.mock assertion that was
malformed but passing silently until Python 3.12.
(SalishSeaNowcast)

Squash-merged dependabot PRs to update pyarrow re: CVE-2023-47248 re: arbitrary code execution 
vulnerability:
* Reshapr
* stopped because pyarrow=14,0.1 is not on conda-forge yet

Team mtg.
(Atlantis)


Fri 10-Nov-2023
^^^^^^^^^^^^^^^

make_ww3_current_file forecast2 stalled; killed and re-ran it; so much for chunks and drop_vars
resolving the issue
make_ww3_wind_file forecast stalled; killed and re-ran it on 2nd try
(SalishSeaCast)

Phys Ocgy seminar: Shumin ocean turbulence lecture #1

Finished migration to Python 3.12
* branch: py312
* PR#209 - squash-merged
Updated readthedocs build config
* branch: update-readthedocs-build
* PR#215 - squash-merged
(SalishSeaNowcast)

J arrived for long weekend visit.


Sat 11-Nov-2023
^^^^^^^^^^^^^^^

upload_forcing to orcinus failed mulitple times due to power outage due to storm
make_ww3_wind_file forecast2 stalled; I didn't attend to it quickly enough and it blocked forecast
run; killed it and ran forecast manually
(SalishSeaCast)

/ocean maintenance postponed due to UBC power outage


Sun 12-Nov-2023
^^^^^^^^^^^^^^^

make_ww3_current_file forecast2 stalled; killed it and skipped run
upload_forcing to orcinus failed mulitple times; orcinus down
(SalishSeaCast)


Week 46
-------

Mon 13-Nov-2023
^^^^^^^^^^^^^^^

**Statutory Holiday** - Remembrance Day in lieu

make_ww3_current_file forecast2 stalled; killed and re-ran it
upload_forcing to orcinus failed mulitple times; orcinus down
(SalishSeaCast)


Tue 14-Nov-2023
^^^^^^^^^^^^^^^

Group mtg; see whiteboard.
(MOAD)

make_ww3_current_file forecast stalled; killed and re-ran it
upload_forcing to orcinus failed mulitple times; orcinus down
(SalishSeaCast)

EOAS Colloquium: Alice Zhu, UofT, Plastics in the Earth System

Continued work on changing wwatch3 runs timing:
* branch: update_ww3-runs
* PR#213
* changed to always launch make_ww3_*_file workers after NEMO forecast run
* pulled branch on skookum; restarted manager for next_workers changes to take
  effect
* pulled branch on arbutus
(SalishSeaNowcast)


Wed 15-Nov-2023
^^^^^^^^^^^^^^^

wwatch3 forecast2 failed to launch overnight:
* KeyError in after_watch_NEMO on ``config["wave forecasts"]["run when"]``
nowcast log stopped updating at 07:44:
* ``watch_NEMO nowcast`` was blocked by stalled ``watch_NEMO forecast2``
* recovery started at ~09:45
    killed ``watch_NEMO forecast2``
    download_results arbutus forecast2 2023-11-14
    make_forcing_links arbutus ssh 
upload_forcing to orcinus failed mulitple times; orcinus down
(SalishSeaCast)

Continued work on changing wwatch3 runs timing:
* branch: update_ww3-runs
* PR#213
* fixed uses of ``config["wave forecasts"]["run when"]`` that I missed yesterday
* pulled branch on skookum; restarted manager for next_workers changes to take
  effect
* pulled branch on arbutus
* wwatch3 nowcast launched successfully after NEMO forecast
Added --backfill option to crop_gribs worker:
* branch: crop_gribs-backfill
* PR#216
* worker code has been used in production at least twice; most of this work was adding
  unit tests and log messages for existing cropped files that are skipped
(SalishSeaNowcast)


Thu 16-Nov-2023
^^^^^^^^^^^^^^^

NEMO forecast2 failed to launch overnight:
* KeyError in checklist due to yesterday's manager restarts
wwatch3 nowcast launched successfully after NEMO forecast
upload_forcing to orcinus failed mulitple times; orcinus down
(SalishSeaCast)

Did UBC required training courses from OCt notifications:
* Workplace Violence Prevention
* Privacy & Information Security Fundamentals 2

Generated new keys and CSRs for Resilient-C domains; see 22-Nov-2022 in 2023 work journal.

Sent CSRs to Karen Beattie at UBC IT.

Handled message from readthedocs re: updating webhook secrets:
* deleted randopony docs project
* deleted webhook for gomms-site project; repo no longer exists on bitbucket
* deleted webhook for gomms-nowcast project; repo no longer exists on bitbucket
* deleted bitbucket webhook for ECget project; added GitHub webhook
* deleted webhook for gomms-nowcast-system project; repo no longer exists on bitbucket
* resync-ed GitHub webbook for midoss-docs project
* resync-ed GitHub webbook for Make-MIDOSS-Forcing project
* resync-ed GitHub webbook for MOHID-Cmd project


Fri 17-Nov-2023
^^^^^^^^^^^^^^^

upload_forcing to orcinus failed mulitple times; orcinus down
make_ww3_current_file forecast stalled; killed and re-ran it; 2 tries
Started backfilling nowcast-agrif:
* only 1 of the 3 login nodes are working properly; sent email to Mark
  * hacked .ssh/config or skookum to use seawolf3 instead of orcinus
  * Mark says issue might be skookum accidentally added to hosts.denied
* backfilling:
    upload_forcing orcinus nowcast+ 2023-11-11
    upload_forcing orcinus turbidity 2023-11-11
    wait for run to finish
    * extremely slow to launch
    * failed at 9m45s w/ fabric error; emailed Mark
Started clean-up of HRDPS continental GRIB files:
* deleted .idx files that were created early in processing
    find /results/forcing/atmospheric/continental2.5/GRIB/ -name "*.idx" -delete
* SSC cropped GRIB files start appearing ~01apr23
(SalishSeaCast)

Finished work on changing wwatch3 runs timing:
* branch: update_ww3-runs
* PR#213 - squash-merged
Docs maintenance:
* branch: docs-maint
* PR#217 - squash-merged
* changed badges layout in README & dev docs to table
* fixed URLs for GHA workflow badges
* added release and Hatch badges to Release process section of dev docs
(SalishSeaNowcast)

Docs maintenance:
* branch: docs-maint
* PR#104 - squash-merged
* added pre-commit badge
* fixed URLs for GHA workflow badges
* added missing target attr to Hatch badge in Release Process section of dev docs
(Reshapr)


Sat 18-Nov-2023
^^^^^^^^^^^^^^^

Continued backfilling nowcast-agrif:
* backfilling:
    wait for automation to fail at ~08:45
    make_forcing_links orcinus nowcast-agrif 2023-11-11
    wait for run to finish
    * failed after 7m41s
(SalishSeaCast)


Sun 19-Nov-2023
^^^^^^^^^^^^^^^

Update os pkgs on arbutus nowcast0 node:
* Got message:
    "The following security updates require Ubuntu Pro with 'esm-infra' enabled"
  re: some pkgs; need to email Venkat about Ubuntu Pro or updating instance from 18.04 LTS
* rebooted nowcast0
* Re-mounted persistent storage volume:
    sudo mount /dev/vdc /nemoShare
* Re-bound /nemoShare/MEOPAR to /export/MEOPAR
    sudo mount --bind /nemoShare/MEOPAR /export/MEOPAR
* Restarted NFS service:
    sudo systemctl restart nfs-kernel-server.service
  * That included reset of stale NFS handles on compute nodes with:
      sudo exportfs -f  # on nowcast0
Updated git repo clones:
* grid
* moad-tools
* NEMO_Nowcast
* NEMO-Cmd
* SalishSeaCmd
* SalishSeaNowcast
* SalishSeaWaves  # default branch is still ``master`` !!
* tools
* skipped due to nervousness about upstream changes
  * SS-run-sets
  * FVCOM41
  * FVCOM-VHFR-config
  * FVCOM-Cmd
  * OPPTools
* skipped updates of repos that are on production tag branches
  * rivers-climatology
  * tides
  * tracers
  * NEMO-3.6-code
  * XIOS-ARCH
  * XIOS-2
Removed conda env:
  conda env remove -p /nemoShare/MEOPAR/nowcast-sys/nowcast-env
Built new conda env:
  conda env create \
    --prefix /nemoShare/MEOPAR/nowcast-sys/nowcast-env \
    -f SalishSeaNowcast/envs/environment-prod.yaml
  copied activate.d and deactivate.d envvars.sh scripts into new env
  installed pkgs (see deploy docs)
Email from Mark to say that orcinus fabric issue appears to be a network switch problem;
possible resolution tomorrow with removal of bad module, but cluster reboot may be required
(SalishSeaCast)


Week 47
-------

Mon 20-Nov-2023
^^^^^^^^^^^^^^^

make_ww3_wind_file forecast2 stalled; killed it and skipped run
orcinus refused connections for nowcast runs
(SalishSeaCast)

Squash-merged dependabot PR in gha-workflows to bump actions/github-script from v6 to v7.

Ran:
  python /media/doug/warehouse/MOAD/gha-workflows/gha_workflow_checker/gha_workflows_checker.py
all good!

Finished work on separating dataset descriptions into files to be composed into
dataset.xml by a script:
* branch: separate-dataset-files
* PR#1 -  squash-merged
* updated README and .gitignore
* added docutils to dev env so that README rendering can be previewed in VSCode
Squash-merged dependabot PR to update setup-micromamba to 1.6.0
Switched skookum back to main branch.
Started work on adding dataset descriptions for 2021-08 bathymetry:
* branch:2108-bathymetry
* PR#3
* worked on ubcSSnBathymetryV2108.xml
  * "with 2m crit. bank but deeper river" ??
  * add changes to history
* worked on section re: 21-11 to landing page
* mtg w/ Susan scheduled for Fri
(erddap-datasets)

Finished update to Python 3.12:
* branch: py312
* PR#68 - squash-merged
* dropped support for Python 3.10
Updated readthedocs build config:
* branch: update-readthedocs-build
* PR#71 - squash-merged
Docs maintenance:
* branch: docs-maint
* PR#72 
* changed badges layout in README & dev docs to table
* fixed URLs for GHA workflow badges
* added release and Hatch badges to Release process section of dev docs
Relased v23.1.
(NEMO-Cmd)



``make_ww3_*wind*_file`` stalls:
* Mon
  * 13-nov: currents forecast2
  * 20-nov: wind forecast2
* Tue
  * 14-nov: currents forecast
* Wed
* Thu
* Fri
  * 17-nov: currents forecast
* Sat
  * 11-nov: winds forecast2
* Sun
  * 12-nov: currents forecast2





Continued backfilling nowcast-agrif:
* backfilling:
    wait for automation to fail at ~08:45
    make_forcing_links orcinus nowcast-agrif 2023-11-11
    wait for run to finish

    upload_forcing orcinus nowcast+ 2023-11-12
    upload_forcing orcinus turbidity 2023-11-12
    wait for run to finish
(SalishSeaCast)








test whether or not to --bind-to-core on sockeye


do we want to change the zoop variable names in ERDDAP for 202111?
might be possible to change them in hindcast and production too?


* Python 3.12:
  * successful workflow test with 3.12:
    * SalishSeaCmd
    * AtlantisCmd
    * NEMO_Nowcast
    * moad_tools
    * salishsea-site
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


TODO:
* fix straight line gaps in wwatch3 forecast plots (forecast2 are okay)

* migrate PyPDF2 to pypdf in SalishSeaNowcast


* tidy module & functions notebook & module

TODO:
* modernize packaging:
  * Reshapr - done 30oct23 in PR#101
  * moad_tools
  * cookiecutter-MOAD-pypkg
  * salishsea-site
  * NEMO_Nowcast
  * ECget
  * MoaceanParcels
  * AtlantisCmd
  * SOG
  * SOG-Bloomcast-Ensemble
  * FVCOM-Cmd
  * SalishSeaTools
  * rpn-to-gemlam
  * Marlin


TODO:
* pre-commit auto-update
  * MOAD/docs - done
  * SalishSeaNowcast
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



Update ONC URLs from dmas.uvic.ca to https://data.oceannetworks.ca/

jupyter kernelspec uninstall unwanted-kernel



TODO:

https://linuxize.com/post/getting-started-with-tmux/

update deployment docs re: spinning up a new compute node

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
