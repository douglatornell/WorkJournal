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




TODO: add assign-issue-pr action to MOAD/docs repo




Started reading Susan's mixing paper that I am co-author on.



* tidy module & functions notebook & module


TODO:
* update sphinx-rtd-theme pin in envs when 1.2 is released
  * MOAD/docs
  * SalishSeaNowcast
  * NEMO_Nowcast


TODO:
* numpy.int in moad_tools random_oil_spills

* Revisit salishsea-site dependabot PRs re: actions versions & reusable workflows

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
  * Make-MIDOSS-Forcing - archived
  * WWatch3-Cmd - archived
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
