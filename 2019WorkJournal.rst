*****************
2019 Work Journal
*****************

This is my public work journal.
It is patterned after one that I have kept for several years for my work at Nordion_.
This journal is about:

* my work as a Research Software Engineer with `Dr. Susan Allen`_ in the `Department of Earth, Ocean and Atmospheric Sciences`_ at the `University of British Columbia`_
* my freelance work via my consulting business,
  `43ravens`_
* my `open-source activities`_


January
=======

Week 1
------

Tue 1-Jan-2018
^^^^^^^^^^^^^^

**Statutory Holiday** - New Year's Day

Handled issues from 1st day of 2018-06 production automation.
Worked with Susan to move hindcast-201812 into automation.
(SalishSea)

Continued dev of MOHID-Cmd package.
(MIDOSS)

Felt progressively crappier as the day went on; headache, body aches, fatigue.


Wed 2-Jan-2018
^^^^^^^^^^^^^^

Worked with headache, body aches, sore throat, and lethargy.

Upgraded kudu and niko to Pop!_OS 18.10:
* followed https://support.system76.com/articles/upgrade-pop/
* flashed iso to USB
* after upgrade, edited files in /etc/apt/sources.list.d/ to re-enable and adjust distro names of 3rd party packages

download_live_ocean was initially launched by automation at 08:53 and failed due to file not found; repeated manual launches failed until 10:33; manual launch at 10:48 succeeded.
Hacked nemo_nowcast.workers.get_web_data() to time out on sum of sleep times instead of product of exponential waits, and SalishSeaNowcast.nowcast.workers.download_live_ocean() call to use wait_exponential_max=7200, and pushed the hacks to skookum for testing tomorrow.
Updated copyright year range in:
* SalishSeaCmd
* SalishSeaNowcast
(SalishSea)

Continued dev of MOHID-Cmd package.
(MIDOSS)

See project journal.
(SalishSeaCast-FVCOM)


Thu 3-Jan-2018
^^^^^^^^^^^^^^

Monitored download_live_ocean; new timeout calc in get_web_data() worked as expected, but 7200s wasn't long enough; collect_weather finished at ~08:40 and LiveOcean file wasn't ready until ~11:20; increased wait_exponential_max=10800.
Discovered that 18-06 ERDDAP dataset updates have turned into a dumpster fire :-(
(SalishSea)

See project journal.
(SalishSeaCast-FVCOM)

See project journal.
(Resilient-C)

See project work journal.
(GOMSS)


Fri 4-Jan-2018
^^^^^^^^^^^^^^

Team mtg; see whiteboard.
Started dev of mohid run subcomaand.
(MIDOSS)

Worked w/ Ben to get SalishSeaCmd and Mercurial working under Python 3.5 on orcinus:
* see hg build notes from Tue 11-Sep-2018, but load gcc and do make install-home
* change PATH to put $HOME/bin near the front
* hg version is stuck at 4.8rc0
download_live_ocean worked on 1st try at 08:26; forecast finished at 09:48; nowcast-agrif was queued at 09:49; nowcast-green finished at 11:39.
Disabled ECget river flow crob jobs on salish in favour of collect_river_data worker.
Worked with Susan to sort why 18-06 ERDDAP datasets suddenly disappeared; nowcast-green/31dec18 files downloaded from ceder were 30dec18 by accident; Susan fixed that.
Email to Emilio re: availability of new datsets for NANOOS and change in dataset id version.
(SalishSea)


Sat 5-Jan-2018
^^^^^^^^^^^^^^

2018-2019 financial roll-over


Sun 6-Jan-2018
^^^^^^^^^^^^^^

upload_forcing nowcast+ got triggered before grib_to_netcdf finished due to race conditions between grib_to_netcdf and make_live_ocean_files, but no runs got launched; recovery:
* upload_forcing west.cloud nowcast+
* upload_forcing orcinus nowcast+
* upload_forcing cedar nowcast+
(SalishSea)

Demoted Fraser water quality buoy wind speed from warning level notification because sensor is out of commission and we don't care.
(ECget)

See project journal.
(SalishSeaCast-FVCOM)


Week 2
------

Mon 7-Jan-2018
^^^^^^^^^^^^^^

Sent email to Roman requesting change nowcast-agrif reservation window to 10:00 to 13:00, and asking if he will consider building a Python 3.7 module on orcinus.
Sent email to Michael & Maxim re: change to 2018-06 config and sarracenia-based HRDPS file management.
Updated ERDDAP index page re: dates of V17-02 to V18-06 change-over and planned removal dates for V17-02 datasets.
Started updating tide gauge station water level datasets from V17-02 to V18-06.
(SalishSea)

Phys Ocgy seminar by Hayley Dosser.

Scary experience with Mercurial and SalishSeaNowcast: niko was left with tip on branch closure commit and when I pulled in work since 23-Dec hg update failed with a traceback about a node with no descendents.

Continued dev of mohid run sub-command.
(MIDOSS)


Tue 8-Jan-2018
^^^^^^^^^^^^^^

Investigated figure failures due to ERDDAP dataset id changes and found that accommodating mix of 17-02 and 18-06 is very troublesome.
Continued updating tide gauge station water level datasets from V17-02 to V18-06, but then reverted them all due to make_plots issue.
hindcast-201812 filled /results/ and crashed the automation; big thrash to get it re-started.
SalishSeasCast team mtg; see whiteboard.
(SalishSea)

Continued dev of mohid run sub-command.
(MIDOSS)

Spin class.


Wed 9-Jan-2018
^^^^^^^^^^^^^^

Started learning rust.

forecast finished at 08:53; agrif finished at 10:23
(SalishSea)

See project journal.
(SalishSeaCast-FVCOM)

See project work journal.
(GOMSS)


Thu 10-Jan-2018
^^^^^^^^^^^^^^^

Confirmed that hindcast-201812 is indeed archiving VHFR FVCOM boundary slab files.
(SalishSea)

See project journal.
(SalishSeaCast-FVCOM)

Continued dev of mohid run sub-command.
Created MIDOSS-MOHID-config repo.
Set up $PROJECT/$USER/MIDOSS/ work space on cedar to test research runs setup.
(MIDOSS)

AtSci candidate seminar by Kate Marvel.


Fri 11-Jan-2018
^^^^^^^^^^^^^^^

Continued learning rust:
* need to export BROWSER=firefox for rustup doc to work

See project work journal.
(GOMSS)


Sat 12-Jan-2018
^^^^^^^^^^^^^^^

Did more research on converting EC RPN files to netCDF and found http://collaboration.cmc.ec.gc.ca/science/rpn.comm/wiki/doku.php?id=armnlib which looks like it will give us librmn to enable getting farther in compilation of code from Francois Roy; review of ARMNLIB installation script tells me I want to run it in a VM.
Updated cedar:hindcast-sys/ repo clones to PROD-hindcast_201812-v2 tag
(SalishSea)

Discovered that TLS certs for susanallen.ca and 43ravens.ca have expired; opened support ticket on webfaction after a bunch of digging showed that something there changed between 21sep18 when susanallen.ca auto-renewed and 6oct18 when 43ravens.ca failed to auto-renew.
Webfaction now has control panel support for HTTPS via Let's Encrypt.


Sun 13-Jan-2018
^^^^^^^^^^^^^^^

Enabled HTTPS via control panel for susanallen.ca and 43ravens.ca; still unclear whether or not redirect sites & apps are still required.
Tested control panel HTTPS on other domains:
* cyclelog looses style presumably due to how /static is being accessed
* douglatornell.ca shows mixed content warning due to how flickr images are accessed
* phpgedview has insecure content warnings on some pages
* sadahome.ca looses style presumably due to how /static is being accessed
Set up Pyramid app at test_pyramid_https, mounted at test-pyramid-http.douglatornell.ca.

Continued learning rust.


Week 3
------

Mon 14-Jan-2018
^^^^^^^^^^^^^^^

Got test_pyramid_https app working with HTTPS by adding url_scheme = https to server:main section of config file.

See work journal.
(Resilient-C)

Replied to email from Michael asking for sample GEMLAM RPN file with path on /data/, notes about building cstrpn2cdf, and my progress re: ARMNLIB on the weekend. He replied with libs and a binary that I successfully tested on salish and niko.
(SalishSea)

Phys Ocgy seminar by Rachael on MIDOSS project.

Continued dev of mohid run sub-command.
(MIDOSS)


Tue 15-Jan-2018
^^^^^^^^^^^^^^^

MOHID-Cmd intro session w/ Rachael and Ashu.
(MIDOSS)

Submitted expense claim for 2x8Tb external drives.

Worked on SalishSeasCast test case with Intel MPI libraries on cedar for Martin re: ticket:
* updated repos in /home/dlatorne/project/dlatorne/MEOPAR/
* cleaned all NEMO configs
* built XIOS-2 with:
  * module load intel/2018.3 impi/2018.3.222
  * module load hdf5-mpi/1.8.18
  * module load netcdf-c++-mpi/4.2 netcdf-fortran-mpi/4.4.4 netcdf-mpi/4.4.1.1
  The last module load results in:
  * The following have been reloaded with a version change:
  1) hdf5-mpi/1.8.18 => hdf5-mpi/1.10.3
(SalishSea)


Wed 16-Jan-2018
^^^^^^^^^^^^^^^

Continued learning rust.

Another attempt to build XIOS-2 with Intel 2018 modules requested by Martin:
  module load python/3.7
  module load netcdf-fortran-mpi/4.4.4
  module load intel/2018.3 impi/2018.3.222
  module unload openmpi/2.1.1
  module load netcdf-c++-mpi/4.2
  module load perl/5.22.2
but that changes the MPI compilers to gcc and gfortran; sent email to Martin for clarification; replied that the  compiler change is a bug that can be worked around with:
  export I_MPI_CC=icc
  export I_MPI_CXX=icpc
  export I_MPI_F90=ifort
  export I_MPI_F77=ifort
netcdf*-mpi module loads fail in interactive session on compute node for build because there are no modules there build against impi, only openmpi; sent email to to Martin.
Released NEMO_Nowcast-19.1 and bumped dev to 19.2.dev0.
(SalishSea)

See project journal.
(SalishSeaCast-FVCOM)

See project work journal.
(GOMSS)


Thu 17-Jan-2018
^^^^^^^^^^^^^^^

See project work journal.
(GOMSS)

Tried building XIOS-2 on login node with env from Martin; failed w/ c++ compile error:
  mpicc -o client.o -DUSING_NETCDF_PAR -I/home/dlatorne/project/dlatorne/MEOPAR/XIOS-2/inc -diag-disable 1125 -diag-disable 279 -D_GLIBCXX_USE_CXX11_ABI=0 -O3 -D BOOST_DISABLE_ASSERTS  -I/home/dlatorne/project/dlatorne/MEOPAR/XIOS-2/extern/src_netcdf -I/home/dlatorne/project/dlatorne/MEOPAR/XIOS-2/extern/boost/include -I/home/dlatorne/project/dlatorne/MEOPAR/XIOS-2/extern/rapidxml/include -I/home/dlatorne/project/dlatorne/MEOPAR/XIOS-2/extern/blitz/include -c /home/dlatorne/project/dlatorne/MEOPAR/XIOS-2/src/client.cpp
  In file included from /home/dlatorne/project/dlatorne/MEOPAR/XIOS-2/inc/calendar_wrapper.hpp(10),
                   from /home/dlatorne/project/dlatorne/MEOPAR/XIOS-2/inc/context.hpp(7),
                   from /home/dlatorne/project/dlatorne/MEOPAR/XIOS-2/src/client.cpp(7):
  /home/dlatorne/project/dlatorne/MEOPAR/XIOS-2/inc/object_template.hpp(76): error: "shared_ptr" is ambiguous
             shared_ptr<T> getShared(void) ;
             ^

  In file included from /home/dlatorne/project/dlatorne/MEOPAR/XIOS-2/inc/calendar_wrapper.hpp(10),
                   from /home/dlatorne/project/dlatorne/MEOPAR/XIOS-2/inc/context.hpp(7),
                   from /home/dlatorne/project/dlatorne/MEOPAR/XIOS-2/src/client.cpp(7):
  /home/dlatorne/project/dlatorne/MEOPAR/XIOS-2/inc/object_template.hpp(77): error: "shared_ptr" is ambiguous
             static shared_ptr<T> getShared(const T* ptr) ;
                    ^

  In file included from /home/dlatorne/project/dlatorne/MEOPAR/XIOS-2/inc/context.hpp(12),
                   from /home/dlatorne/project/dlatorne/MEOPAR/XIOS-2/src/client.cpp(7):
  /home/dlatorne/project/dlatorne/MEOPAR/XIOS-2/inc/data_output.hpp(60): error: "xios::shared_ptr" is ambiguous
                                             const shared_ptr<CCalendar> cal) = 0;
                                                   ^

  In file included from /home/dlatorne/project/dlatorne/MEOPAR/XIOS-2/src/client.cpp(7):
  /home/dlatorne/project/dlatorne/MEOPAR/XIOS-2/inc/context.hpp(208): error: "xios::shared_ptr" is ambiguous
             static shared_ptr<CContextGroup> root;
                    ^

  /home/dlatorne/project/dlatorne/MEOPAR/XIOS-2/src/client.cpp(284): error: no operator "<<" matches these operands
              operand types are: std::basic_ostream<char, std::char_traits<char>> << StdStringStream
            ERROR("void CClient::openStream(const StdString& fileName, const StdString& ext, std::filebuf* fb)",
            ^
  /home/dlatorne/project/dlatorne/MEOPAR/XIOS-2/inc/date.hpp(34): note: this candidate was rejected because function is not visible
                friend StdOStream& operator<<(StdOStream& out, const CDate& date);
  ...
Sent email to ticket 042269.
Martin replied with suggestion to add -std=c++11 compile flag; didn't help.
Did svn checkout of xios-2.0 trunk and got r1637; it built on login node, but took nearly 1 hour.
Built NEMO SalishSeasCast w/ Intel 2018.3 module loads.
Tried 21nov14_oneday tests
(SalishSea)

See project journal.
(SalishSeaCast-FVCOM)

Updated Mercurial on kudu to 4.8.2+3-fbd168455b26:
* conda activate hg-dev
* cd hg-stable
* hg pull -u
* make clean all
* sudo make install PYTHON=/media/doug/warehouse/conda_envs/hg-dev/bin/python2.7


Fri 18-Jan-2018
^^^^^^^^^^^^^^^

See work journal.
(Resilient-C)

Sorted out mess from transition to production yesterday of FVCOM VHFR x2 baroclinic config:
* nowcast-x2/18jan19 is incomplete
* forecast-x2/18jan19 is MIA
* 11jan18-10feb18 hindcast results are going into hindcast.201812/ instead of hindcast.201812_annex/; moved them
* manually re-ran nowcast/18jan19
* changed next_workers to launch make_fvcom_boundary after watch_fvcom forecast, and forecast/18jan19 launched via automation
* fixed x2 baroclinic stations file name to that make plots fvcom works
* manual ran makeplots for *cast/17jan19 and nowcast/18jan19
More cedar ticket#042269 work:
* grabbed xio-2 trunk and built it with Intel 2018.3 compilers and MPI lib
* built NEMO against that XIOS-2
* 2 test runs failed w/ module availability errors on compute notes
(SalishSea)

Installed skype on niko via snap and resurrected my skype account with is now a Microsoft Live account.

AtSci candidate seminar by Pengfei Liu (aerosol chemistry and climate change)


Sat 19-Jan-2018
^^^^^^^^^^^^^^^

Vancouver to Brampton

Forced readthedocs build of SalishSea-MEOPAR docs for Birgit and explained by email to her the issues with webhooks triggering.
(SalishSea)


Sun 20-Jan-2018
^^^^^^^^^^^^^^^

Brampton

Confirmed that all webhooks between Bitbucket and readthedocs are using the rtd v2 API.

Updated Mercurial on niko to 4.8.2+810-593f6359681d:
* conda activate hg-dev
* cd hg-stable
* hg pull -u
* make clean all
* sudo make install PYTHON=/media/doug/warehouse/conda_envs/hg-dev/bin/python2.7

Updated conda on niko and installed conda-build and anaconda-client pkgs into base env.

Started modernizing NEMO-Cmd.

See project work journal.
(GOMSS)


Week 4
------

Mon 21-Jan-2018
^^^^^^^^^^^^^^^

Brampton

More cedar ticket#042269 work:
* test run 15869965 loaded modules but failed due to missing libnetcdf.so.11
* emailed Martin

Continued modernizing NEMO-Cmd.

See project work journal.
(GOMSS)


Tue 22-Jan-2018
^^^^^^^^^^^^^^^

Replied to automated email from arbutus.cloud re: migration, and Venkat is on ensuring our migration happens.
collect_weather 00 stalled, unsure why; recovery:
* download_weather 00 --debug
* download_weather 06 --debug
* collect_river_data Fraser --data-date 2019-01-21
* collect_river_data Englishman --data-date 2019-01-21
* download_weather 12
* get_NeahBay_ssh nowcast
* grib_to_netcdf nowcast+
* collect_weather 18
* download_live_ocean
* get_onc_ctd x3
* get_onc_ferry
(SalishSea)

Brampton to Vancouver


Wed 23-Jan-2018
^^^^^^^^^^^^^^^

collect_weather 18 stalled; recovery:
* download_weather 18 --debug
* download_weather 00 --debug
* download_weather 06 --debug
* collect_river_data Fraser --data-date 2019-01-22
* collect_river_data Englishman --data-date 2019-01-22
* download_weather 12
* collect_weather 18
* get_onc_ferry
* get_onc_ctd x3
Merged SalishSeaNowcast vhfr_x2_baroclinic branch into default re: successful deployment.
Helped Tereza getting a test of SKOG for integration into SalishSeasCast running on salish.
(SalishSea)

See project journal.
(SalishSeaCast-FVCOM)


Thu 24-Jan-2018
^^^^^^^^^^^^^^^

collect_weather 00 stalled; recovery:
* download_weather 00
* download_weather 06 to launch forecast2 runs
* download_weather 12 to launch nowcast runs
* collect_weather 18
Tried to figure out why collect_weather is stalling; 00 had not seen all expected files, but sarracenia log had rolled so I couldn't tell if all were downloaded; restarted sr_subscribe for hrdps-west in case it is the culprit.
Helped Tereza getting a test of SKOG for integration into SalishSeasCast running on salish.
Added produciton config YAML unit tests to make_runoff_files, and removed daily creation of `RLonFraCElse_{:y%Ym%md%d}.nc` files.
More cedar ticket#042269 work:
* reply from Martin says that missing libnetcdf.so.11 was similar to module load failure; should be fixed now
(SalishSea)

See project journal.
(SalishSeaCast-FVCOM)

Updated repo clones on kudu.
(MIDOSS)


Fri 25-Jan-2018
^^^^^^^^^^^^^^^

collect_weather workers have been reliable since yesterday's sr_subscribe restart.
Updated cedar:hindcast-sys/ repo clones to PROD-hindcast_201812-v3 tag:
* in each repo clone: hg pull; hg up -r PROD-hindcast_201812-v3
* ./makenemo -n SalishSeaCast clean
* salloc --time=0:30:0 --cpus-per-task=8 --mem-per-cpu=1000m --account=rrg-allen
* XIOS_HOME=$PROJECT/SalishSea/hindcast-sys/XIOS-2 ./makenemo -n SalishSeaCast -m X64_CEDAR -j8
Susan handled getting hindcast runs restarted with these changes for 01oct18.
More cedar ticket#042269 work:
* cd project/dlatorne/MEOPAR/SS-run-sets/v201812/hindcast/runfiles/spin_up/
* salishsea run 21nov14_oneday.yaml $PROJECT/$USER/MEOPAR/results/21nov14_oneday --debug --no-submit
* emacs SalishSeaNEMO.sh:
  * module load intel/2018.3 impi/2018.3.222
  * module load hdf5-mpi/1.10.3
  * module load netcdf-c++-mpi/4.2 netcdf-fortran-mpi/4.4.4 netcdf-mpi/4.4.1.1
  * module load python/3.7.0
* sbatch SalishSeaNEMO.sh
(SalishSea)

Project mtg; see whiteboard.
(MIDOSS)

Group mtg; see whiteboard.
(Canyons/Arctic)

See project journal.
(SalishSeaCast-FVCOM)

AtSci candidate seminar by Oliver Watt-Meyer.


Sat 26-Jan-2018
^^^^^^^^^^^^^^^

forecast/26jan18 got stuck at 84.7% due to a file length issue in atmos forcing; upload_forcing nowcast+ got triggered before grib_to_netcdf finished due to race conditions between grib_to_netcdf and make_live_ocean_files; recovery:
* kill watch_NEMO on west.cloud
* kill xios_server.exe on west.cloud
* circusctl message_broker restart
* circusctl log_aggregator restart
* circusctl manager restart
* wait for SalishSeaNEMO.sh script to finish on west.cloud
* upload_forcing west.cloud nowcast+ --debug
* upload_forcing orcinus nowcast+ --debug
* upload_forcing cedar nowcast+ --debug
* make_forcing_links west.cloud nowcast+ --debug
* make_forcing_links orcinus nowcast+ --debug
* make_forcing_links west.cloud ssh
* wait for NEMO forecast runs to finish
* launch_remote_worker west.cloud make_fvcom_boundary "west.cloud-nowcast forecast"
Closed SalishSeaNowcast fix_velocity_rotation and vhfr_x2_baroclinic branches.
Started implementing concurrent worker feature in NEMO_Nowcast; see Sat 17-Nov-2018 design notes.
(SalishSea)


Sun 27-Jan-2018
^^^^^^^^^^^^^^^

forecast/26jan19 got stuck at 84.7% due to a file length issue in atmos forcing; upload_forcing nowcast+ got triggered before grib_to_netcdf finished due to race conditions between grib_to_netcdf and make_live_ocean_files; recovery:
* kill watch_NEMO on west.cloud
* kill xios_server.exe on west.cloud
* wait for SalishSeaNEMO.sh script to finish on west.cloud
* upload_forcing cedar nowcast+ --debug
* upload_forcing orcinus nowcast+ --debug
* make_forcing_links orcinus nowcast+ --debug
* upload_forcing west.cloud nowcast+ --debug
* make_forcing_links west.cloud nowcast+ --debug
* make_forcing_links west.cloud ssh
Continued implementing concurrent worker feature in NEMO_Nowcast; see Sat 17-Nov-2018 design notes.
(SalishSea)


Week 5
------

Mon 28-Jan-2019
^^^^^^^^^^^^^^^

No log from nowcast after 17:38:18 Sunday; lots of hung worker processes; recovery:
* kill hung processes
* rm -rf GRIB/20190128/00/
* download_weather 00
* rm -rf GRIB/20190128/00/
* download_weather 06 to launch forecast2 runs
* download_weather 12 to launch nowcast runs
* collect_weather 18
Updated salishsea-site copyright year range, and many http to https, especially stormsurge.bc.ca to eliminate mixed content warning.
Continued implementing concurrent worker feature in NEMO_Nowcast; see Sat 17-Nov-2018 design notes.
Updated cedar-hindcast to PROD-hindcast_201812-v4.
Removed schedule from SalishSeaNEMO configuration & docs.
Added sarracenia client to circus control.
(SalishSea)

Set up sada-network.slack.com workspace for Susan and I; still no go on Bitbucket/Slack integration.

See project journal.
(SalishSeaCast-FVCOM)

Phys Ocgy seminar by Rich re: drifters and surface currents.

Reproduced hg close-head bug in minimal repo.


Tue 29-Jan-2019
^^^^^^^^^^^^^^^

collect_weather 00 stalled; recovery:
* download_weather 00
* download_weather 06 to launch forecast2 runs
* download_weather 12 to launch nowcast runs
* collect_weather 18
Explored slack, especially incoming webhook internal integration for SalishSeaNowcast to post run status messages; got Bitbucket and Sentry notifications working.
Email request from Ian Charlton @coroner for surface current tiles spanning 17-Apr-2016.
Charles bounced salish & skookum to resolve filesystem issue re: mounting /SalishSeaCast, though the issue turned out to be a typo in salish:/etc/exports; provided a good test of code I added to /etc/rc.local
SalishSeaCast mtg; see whiteboard.
(SalishSea)

Dr. Yuan Wang AtSci candidate seminar


Wed 30-Jan-2019
^^^^^^^^^^^^^^^

Changed sentry notifications to new SADA:#ssc-exceptions channel.
collect_weather 12 stalled with 525 files collected:
* confirmed that sarracenia also only downloaded 525 files
* download_weather 12 to get automation started
Started building new prod env in skookum:/SalishSeaCast/.
Ran nowcast-dev/29jan19 manually because it got interrupted yesterday by salish reboot.
Made paths for scour and pdftocairo in SalishSeaNowcast explicitly use $NOWCAST_ENV/bin/; something changed across skookum reboot that caused them not to be found.
(SalishSea)

Deleted kudu nemo-cmd-2.7 env; updated kudu nemo-cmd env to Python 3.7.

See project work journal.
(GOMSS)

See project journal.
(SalishSeaCast-FVCOM)


Thu 31-Jan-2019
^^^^^^^^^^^^^^^

Set up tmp run dir for ticket#042269 test case and replied to Martin.
download_live_ocean timed out; ran upload_forcing nowcast+ x3 manually to restart automation.
Met w/ Venkat @UBC-ARC re: migration to arbutus.cloud:
* he will try for c-flavours with more CPUs bound to physical nodes
* he will get us a c8 or c8 -32g or 64g flavour for xios
* I will switch to 18.04 LTS
* 1Tb persistent storage will be new on arbutus; rsync across from west.cloud
* agreed to target completion of migration for end of Feb
(SalishSea)

MOHID test run submitted under rrg-allen finally ran; debugged and finished dev of `mohid gather` sub-command.
Integrated `mohid gather` into MOHID.sh script generation in `mohid run` and submitted a test run under def-allen.; success!
Updated MOHID-Cmd and MIDOSS docs re: `mohid gather` and finalized `mohid run`.
(MIDOSS)

EOAS colloquium by Evgeny re: Southern Ocean salps and krill

Continued formulating hg close-heads bug report:

hg init close-heads-bug
cd close-heads-bug/
echo "Do some work on default." > foo
hg add foo
hg ci -m"Do some work on default."
echo "Do some more work on default." >> foo
hg ci -m"Do some more work on default."
hg branch feature
echo "Do some work on feature." >> foo
hg ci -m"Do some work on feature."
hg up default
echo "Do more work on default after work on feature." >> foo
hg ci -m"Do more work on default after work on feature."
hg merge feature
hg ci -m"Merge feature branch into default."
echo "Do work on default after merging in feature." >> foo
hg ci -m "Do work on default after merging in feature."
hg close-head feature -m"Close feature branch."
hg log --graph
# tip is at changeset 6
# any attempt to update now fails
hg up -r default
abort: uncommitted changes
(commit or update --clean to discard changes)
hg status
# but status shows no uncommitted changes
hg up --clean
** unknown exception encountered, please report by visiting
** https://mercurial-scm.org/wiki/BugTracker
** Python 2.7.15 |Anaconda, Inc.| (default, Sep 27 2018, 20:19:23) [GCC 4.8.2 20140120 (Red Hat 4.8.2-15)]
** Mercurial Distributed SCM (version 4.8.2+810-593f6359681d)
** Extensions loaded: closehead, graphlog, convert, strip, mq, pager, rebase
Traceback (most recent call last):
  File "/usr/local/bin/hg", line 43, in <module>
    dispatch.run()
  File "/usr/local/lib/python2.7/site-packages/mercurial/dispatch.py", line 99, in run
    status = dispatch(req)
  File "/usr/local/lib/python2.7/site-packages/mercurial/dispatch.py", line 225, in dispatch
    ret = _runcatch(req) or 0
  File "/usr/local/lib/python2.7/site-packages/mercurial/dispatch.py", line 376, in _runcatch
    return _callcatch(ui, _runcatchfunc)
  File "/usr/local/lib/python2.7/site-packages/mercurial/dispatch.py", line 384, in _callcatch
    return scmutil.callcatch(ui, func)
  File "/usr/local/lib/python2.7/site-packages/mercurial/scmutil.py", line 165, in callcatch
    return func()
  File "/usr/local/lib/python2.7/site-packages/mercurial/dispatch.py", line 367, in _runcatchfunc
    return _dispatch(req)
  File "/usr/local/lib/python2.7/site-packages/mercurial/dispatch.py", line 1021, in _dispatch
    cmdpats, cmdoptions)
  File "/usr/local/lib/python2.7/site-packages/mercurial/dispatch.py", line 756, in runcommand
    ret = _runcommand(ui, options, cmd, d)
  File "/usr/local/lib/python2.7/site-packages/hgext/pager.py", line 77, in pagecmd
    return orig(ui, options, cmd, cmdfunc)
  File "/usr/local/lib/python2.7/site-packages/mercurial/dispatch.py", line 1030, in _runcommand
    return cmdfunc()
  File "/usr/local/lib/python2.7/site-packages/mercurial/dispatch.py", line 1018, in <lambda>
    d = lambda: util.checksignature(func)(ui, *args, **strcmdopt)
  File "/usr/local/lib/python2.7/site-packages/mercurial/util.py", line 1670, in check
    return func(*args, **kwargs)
  File "/usr/local/lib/python2.7/site-packages/mercurial/util.py", line 1670, in check
    return func(*args, **kwargs)
  File "/usr/local/lib/python2.7/site-packages/hgext/mq.py", line 3633, in mqcommand
    return orig(ui, repo, *args, **kwargs)
  File "/usr/local/lib/python2.7/site-packages/mercurial/util.py", line 1670, in check
    return func(*args, **kwargs)
  File "/usr/local/lib/python2.7/site-packages/mercurial/commands.py", line 6110, in update
    updatecheck=updatecheck)
  File "/usr/local/lib/python2.7/site-packages/mercurial/hg.py", line 912, in updatetotally
    updata = destutil.destupdate(repo, clean=clean)
  File "/usr/local/lib/python2.7/site-packages/mercurial/destutil.py", line 166, in destupdate
    node, movemark, activemark = destupdatestepmap[step](repo, clean)
  File "/usr/local/lib/python2.7/site-packages/mercurial/destutil.py", line 133, in _destupdatebranchfallback
    assert node is not None, ("any revision has at least "
AssertionError: any revision has at least one descendant branch head

hg summary
parent: 6:7975eae997b7 tip
 Close feature branch.
branch: default
commit: (new branch)
update: 3 new changesets (update)
phases: 7 draft


Fri 1-Feb-2019
^^^^^^^^^^^^^^

nowcast-agrif/31jan19 failed when it tried to run at ~03:46, probably due to forcing links getting stomped by forecast2; recovery:
* make_forcing_links nowcast-agrif --run-date 2019-01-31
* but run_NEMO_agrif was extremely slow
Continued implementing concurrent worker feature in NEMO_Nowcast; see Sat 17-Nov-2018 design notes.
(SalishSea)

Helped Rachael & Ashu w/ initial work on .nc to .hdf5 forcing files for MOHID.
(MIDOSS)

See project journal.
(SalishSeaCast-FVCOM)


Sat 2-Feb-2019
^^^^^^^^^^^^^^

Vancouver to Parksville

Added slack notifications for worker completion in NEMO_Nowcast and deployed to production; restarted circusd from command-line in place of version that was running from /etc/rc.local after 29jan19 reboot.
forecast/02feb19 got stuck at 84.7% due to a file length issue in atmos forcing; upload_forcing nowcast+ got triggered before grib_to_netcdf finished due to race conditions between grib_to_netcdf and make_live_ocean_files; recovery:
* kill xios_server.exe on west.cloud
* kill watch_NEMO on west.cloud
* wait for SalishSeaNEMO.sh script to finish on west.cloud
* upload_forcing cedar nowcast+ --debug
* upload_forcing orcinus nowcast+ --debug
* make_forcing_links orcinus nowcast+ --debug
* upload_forcing west.cloud nowcast+ --debug
* make_forcing_links west.cloud nowcast+ --debug
* make_forcing_links west.cloud ssh
download_wwatch3_results failed due to network disconnection.
(SalishSea)

See project journal.
(SalishSeaCast-FVCOM)


Sun 3-Feb-2019
^^^^^^^^^^^^^^

upload_forcing nowcast+ failed due to grib_to_netcdf/make_live_ocean_files race condition; reran manually to resolve.
Started keeping more notes about resolution of issues in slack threads associated with Sentry notifications, and probably less here.
Figured out that wrong version of nccopy issue that started on 30jan19 was due to circusd start from /etc/rc.local because it disappeared after yesterday restart from command-line.
Started adding nowcast-green run type to make_surface_current_tiles for command-line use to generate tile from archival runs.
Added unit tests for production YAML config for elements unlikely to be tested by workers; e.g. slack notifications, 0mq message system, manager message registry, etc.
(SalishSea)

See project journal.
(SalishSeaCast-FVCOM)


February
========

Week 6
------

Mon 4-Feb-2019
^^^^^^^^^^^^^^

Developed a bash process for generation of 1d netCDF4 files containing 8 hourly variables from GEMLAM archive files; generated 2-3-Nov-2014 for Susan to work with for next step of calculating the other 4 variables that we need; see notes in slack SADA#hrdps-archive channel.
Talked to Ben about getting ONC scalar data.
(SalishSea)

Helped Ashu sort out unstaggering of NEMO velocities, and talked to him about how to write hdf5 files.
(MIDOSS)


Tue 5-Feb-2019
^^^^^^^^^^^^^^

Discussed design of extension of `nemo/salishsea run` sub-commands to do dependent-link segmented runs on HPC for sensitivity studies; see design notes at https://sada-network.slack.com/archives/DFSK9ESUW/p1549387959002800\
download_live_ocean slow: finally finished at 11:35.
Started rsync-ing GEMLAM 2010-2014 files from external drive to /opp/GEMLAM/.
Deleted /results/nowcast-dev/ and /results/nowcast-blue (201702).
Updated trello board re: /results2/ and discovered that hindcast.201812/11jan19-20jan19 have not been downloaded from cedar.
(SalishSea)

Delivered 2x8Tb external drives to Gonzalo; need Charles to fix permissions on automounts from root:root 755. Submitted expense claim.
(Canyons)


Wed 6-Feb-2019
^^^^^^^^^^^^^^

See project work journal.
(GOMSS)

Sent link to nowcast-green/19feb18 surface current tiles to Ian@coroner.
Email thread w/ Susan & Elise about segmented NEMO runs automation.
Updated FVCOM worker ports list on west.cloud to 5580-5583 to accommodate make_fvcom_rivers_forcing.
(SalishSea)

Lots of email w/ Rachael & Ashu about generating forcing files.
(MIDOSS)

See work journal.
(Resilient-C)

See project journal.
(SalishSeaCast-FVCOM)

Re-enabled http-redirect websites on webfaction for 43ravens.ca and susanallen.ca.
Set up http-redirect apps and site on webfaction for cyclelog, douglatornell.ca, phpgedview.
Disabled jjem, mock_sc, and sealinkd sites.

Discovered that waitress has restored support for host/port in config (in addition to listen). chaussette requires the former in its most recent release and only supports the latter in unreleased code on github. But waitress change means that we can unpin from waitress==0.9.0! Tested and confirmed in vagrant VM.
(salishsea-site)


Thu 7-Feb-2019
^^^^^^^^^^^^^^

Finalized unpinning waitress.
Built /SalishSeaCast/salishsea-site-env; had to edit setup.py re:unpinning waitress.
Flipped salishsea.eos.ubc.ca from /results/nowcast-sys/salishsea-site to /SalishSeaCast/salishsea-site:
* Change value of Bitbucket pipelines PROD_DEPLOY_REPO repository variable
* scp modified circus_logger.yaml and deploy.sh production.ini
* circusctl --endpoint tcp://127.0.0.1:7777 quit in /results/nowcast-sys
* rsync -av /results/nowcast-sys/logs/ /SalishSeaCast/logs/
* circusd in /SalishSeaCast
Couldn't get waitress==1.2.1 to work in production, so reverted to pin at 0.9.0.
Removed circusd-status from configuration.
Tried to move sarracenia storage to /SalishSeaCast/, but it didn't work, so updated nowcast-sys SalishSeaNowcast back to a6e5d0dff964
(salishsea-site)

Suggested running ncrcat in subprocesses to Ashu, and discussed Python and SalishSeaCast system with him.
(MIDOSS)

EOAS symposium: Sun Kwak re: organics in space and origins of life on Earth


Fri 8-Feb-2019
^^^^^^^^^^^^^^

The change I put in yesterday afternoon to direct the datamart files that the `sarracenia` client saves to `/SalishSeaCast/datamart/` did in fact take effect; but I thought it hadn't so I reverted the config changes and didn't restart `collect_weather` to make it look there. Consequently, the automation stalled because, as far as `collect_weather` was concerned the `00` forecast never appeared. But it, and the `06`, and the `12`,  and the updates to the rivers `.csv` files are all safe and sound in `/SalishSeaCast/datamart/`; recovery (skipping forecast2 runs):
* kill collect_weather 00
* download_weather 00 --debug
* download_weather 06 --debug
* collect_river_data Capilano --data-date 2019-02-07 --debug
* collect_river_data Englishman --data-date 2019-02-07 --debug
* collect_river_data Fraser --data-date 2019-02-07 --debug
* make_runoff_file --debug
* clear_checklist
* download_weather 12
* collect_weather 18 &
* get_onc_ctd SCVIP --debug
* get_onc_ctd SEVIP --debug
* get_onc_ctd USDDL --debug
* get_onc_ferry --debug
* ping_erddap SCVIP-CTD --debug
* ping_erddap SEVIP-CTD --debug
* ping_erddap USDDL-CTD --debug
* ping_erddap TWDP-ferry --debug
sudo apt-get install pngquant on skookum to support Michael's SalishSeaNowcast PR#6 that compresses surface surrent tile PNGs lossily via pngquant.
Created SalishSeaNowcast issue #65  re: using pngquant on other other image loop PNGs.
(SalishSea)


Sat 9-Feb-2019
^^^^^^^^^^^^^^

get_NeahBay_ssh failed due to NOAA web site down; when it came back there was a new version of the slosh web site.
Started refactoring get_NeahBay_ssh to use new site.


Sat 9-Feb-2019
^^^^^^^^^^^^^^

Deleted /results/forcing/rivers/datamart.aside
Deleted /results/forcing/atmospheric/GEM2.5/GRIB/datamart.aside
nowcast-agrif/09feb19 failed due to missing turbidity file that was there, so maybe an orcinus file syste issue?; recovery:
* make_forcing_links orcinus nowcast-agrif --run-date 2019-02-09
Started planning to move automation to /SalishSeaCast file system Monday afternoon.
Continued dev of NEMO_Nowcast concurrent worker feature.
(SalishSea)


Week 7
------

Mon 11-Feb-2019
^^^^^^^^^^^^^^^

Snowy day after overnight storm; worked at home.
Lunch w/ Max, Sylvia & Lucy.

See work journal.
(Resilient-C)

Continued dev of NEMO_Nowcast concurrent worker feature; started test deployment into GoMSS_Nowcast.
Moved automation to run from /SalishSeaCast/:
* update repos in /SalishSeaCast/
* rsync -av /results/nowcast-sys/logs/ /SalishSeaCast/logs/
* conda install "pyzmq<17" "tornado<5" in nowcast-env
* circusctl quit in old env
* kill running watch_NEMO nowcast-dev
* kill running collect_weather 00
* circusd --daemon in new env
* restart web app in env w/ NOWCAST_LOGS=/SalishSeaCast/nowcast-sys/logs
* watch_NEMO nowcast-dev
* collect_weather 00
Discovered that I built the wrong NEMO config on salish; built SalishSeaCast_Blue, cleaned SalishSeaCast.
Recovered from paths for combine and gather that got messed for nowcast-dev during transition.
(SalishSea)

See project work journal.
(GOMSS)


Tue 12-Feb-2019
^^^^^^^^^^^^^^^

Snowy day after another overnight and continuing snowfall; UBC closed, worked at home.

Fixed ERDDAP dataset paths for bathymetry & mesh mask re: change form /results/nowcast-sys/ to /SalishSeaCast/.
Finished updating tide gauge station water level datasets from V17-02 to V18-06.
Disabled ERDDAP V17-02 forecast datasets.
Enabled ERDDAP V18-06 forecast datasets and updated nowcast.yaml to use them.
Updated ERDDAP index page re: V17-02 to V18-06 datasets.
Bounced ERDDAP to load new index page.
(ERDDAP)

Updated Mercurial on kudu to 4.9+5-f2f538725d07:
* conda activate hg-dev
* cd hg-stable
* hg pull
* hg update -r tip
* make clean all
* sudo make install PYTHON=/media/doug/warehouse/conda_envs/hg-dev/bin/python2.7

Continued dev of NEMO_Nowcast concurrent worker feature; using test deployment into GoMSS_Nowcast.
Started modernizing SalishSeaCmd package in preparation for addition of segmented runs feature:
* create new Python 3.7 dev env on kudu
* added badges to README and dev docs
* added license section to dev docs
* changed to use black for code style management
* modernized docs build configuration and makefile
* dropped support for Python 2.7, minimum is now 3.5

* fix broken and redirected URLs in docs
* add linkcheck section to dev docs
(SalishSea)


Wed 13-Feb-2019
^^^^^^^^^^^^^^^

Dentist appt.

Ticket #042269 update from Martin:
* He got Intel MPI version of NEMO + recent svn XIOS running in /scratch/siegert/dlatorne/oneday_21nov14_2019-01-31T103135.621285-0800 and it produced the same "caller of events ... are not coherent" error as we were getting at the start of the ticket
* He also asked if we had contacted the XIOS list and I sent him our exchange there that points to MPI library.
make_plots nemo forecast* publish failed due to me forgetting to change V17-02 to v18-06 in nowcast.yaml ERDDAP URL template; re-ran manually
Discovered that NEMO_Nowcast concurrent workers feature has a design flaw: ConcurrentWorkers blocks manager :-(
(SalishSea)

Sent Susan info about MOHID grid, and Ashu nextcloud link to MOHID results from Shihan.
(MIDOSS)

See project work journal.
(GOMSS)


Thu 14-Feb-2019
^^^^^^^^^^^^^^^

See project work journal.
(GOMSS)

Backed out --concurrent worker cli option, ConcurrentWorkers, and SequencedWorkers, etc. changes in NEMO_Nowcast.
Lack of support for matplotlib=1.5.3 in modern jupyter bit so hard on kudu that I am blocked on figures work.
(SalishSea)

See project journal.
(SalishSeaCast-FVCOM)


Fri 15-Feb-2019
^^^^^^^^^^^^^^^

Project mtg; see whiteboard.
(MIDOSS)

GEM2.5-2010-2014 drive refused to mount on niko.
Resumed work on migration of figure modules to matplotlib-3.0.0:
* merged default branch into matplotlib3_figures
* Ported:
  * nowcast/figures/publish/pt_atkinson_tide.py
  * nowcast/figures/publish/compare_tide_prediction_max_ssh.py
  * nowcast/figures/publish/storm_surge_alerts.py
  * nowcast/figures/publish/storm_surge_alerts_thumbnail.py
* WIP on niko:
  * nowcast/figures/research/velocity_section_and_surface.py
* TODO:
  * nowcast/figures/research/baynes_sound_agrif.py
  * nowcast/figures/research/time_series_plots.py
  * nowcast/figures/research/tracer_thalweg_and_surface_hourly.py
  * nowcast/figures/research/tracer_thalweg_and_surface.py
  * nowcast/figures/comparison/salinity_ferry_track.py
  * nowcast/figures/publish/surface_current_tiles.py
(SalishSea)


Sat 16-Feb-2019
^^^^^^^^^^^^^^^

Another dance with docker; this time the objective is to use it for testing pipelines for Bitbucket, and perhaps for providing dev envs:
* https://medium.com/@chadlagore/conda-environments-with-docker-82cdc9d25754
* https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-18-04
* tried docker snap package but it has weird issue about permissions when I tried docker build, so ditched it
* sudo apt update
* sudo apt install apt-transport-https ca-certificates curl software-properties-common
* curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
* sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu cosmic stable"
* sudo apt update
* apt-cache policy docker-ce
* sudo apt install docker-ce
* sudo systemctl status docker
* sudo usermod -aG docker ${USER}
* su - ${USER}
* id -nG
Worked through details of Bitbucket pipeline to run pytest and show coverage report for NEMO-Cmd in douglatornell/nemo-cmd-piplines-test repo.
Dockerfile w/ NEMO-Cmd installed for interactive use:
  FROM continuumio/miniconda3

  RUN mkdir /home/NEMO-Cmd
  WORKDIR /home/NEMO-Cmd
  COPY . .
  RUN conda env create -f ./environment-test.yaml
  ENV CONDA_PREFIX /opt/conda/envs/nemo-cmd-test
  ENV PATH $CONDA_PREFIX/bin:$PATH
  RUN echo "source activate nemo-cmd-test" > ~/.bashrc
  RUN $CONDA_PREFIX/bin/python3.7 -m pip install -e .
Docker container for pipeline:
* docker build -t nemo-cmd-test pipelines-test-env/
* docker tag nemo-cmd-test:latest douglatornell/salishsea:nemo-cmd-test
* docker push douglatornell/salishsea:nemo-cmd-test

Pulled and updated to PROD-hindcast_201812-v5 in hindcast-sys on cedar; did a clean build of NEMO SalishSeaCast config for 01feb19 hindcast run.
Added Bitbucket pipeline for coverage run -m pytest and coverage report to NEMO-Cmd.
Added Bitbucket pipeline for coverage run -m pytest and coverage report to SalishSeaCmd.
(SalishSea)


Week 8
------

Mon 18-Feb-2019
^^^^^^^^^^^^^^^

**Statutory Holiday** - Family Day

Replied to Martin's ticket #042269 email w/ instructions on how to build NEMO/SalishSeaCast.
Finished setup graham:project/dlatorne/MEOPAR/.
Got access to EOAS optimum cluster and started exploring:
* module load Miniconda/3
* conda create -n py27 -c conda-forge python=2.7 mercurial
* conda activate py27
* hg clone https://www.mercurial-scm.org/repo/hg-stable
* conda create -n salishseacast -c conda-forge python=3.7 pyyaml arrow attrs cliff
* conda activate salishseacast
* pip install python-hglib
* module load GCC/8.2/0
* cd hg-stable
* make clean install-home PYTHON=$CONDA_PREFIX/bin/python3.7
(SalishSea)


Tue 19-Feb-2019
^^^^^^^^^^^^^^^

Confirmed that niko portable backup drive mounts fine after cold boot.
Installed docker on niko.
Tried GEM2.5-2010-2014 drive again on niko; still refused to mount.
Resumed work on migration of figure modules to matplotlib-3.0.0:
* created issue #66 re: use of "on/off" instead of "True/False" in matplotlib calls like tick_params().
* explored "box-forced" deprecation warning and traced it to salishsea_tools.viz_tools.set_aspect() default arg adjustable="box-forced"; changing to adjustable="box" made no difference to velocity_section_and_surface.py; see issue #67
* Ported:
  * nowcast/figures/research/velocity_section_and_surface.py
  * nowcast/figures/research/baynes_sound_agrif.py
  * nowcast/figures/research/time_series_plots.py
* WIP on niko:
* TODO:
  * nowcast/figures/research/tracer_thalweg_and_surface_hourly.py
  * nowcast/figures/research/tracer_thalweg_and_surface.py
  * nowcast/figures/comparison/salinity_ferry_track.py
  * nowcast/figures/publish/surface_current_tiles.py
Salish Sea team mtg; see whiteboard.
Fixed image symlinks for salishsea.eos.ubc.ca site index page.
(SalishSea)

Discussed runs configuration and mercurial workflows w/ Ashu.
(MIDOSS)


Wed 20-Feb-2019
^^^^^^^^^^^^^^^

Did initial check on Ashu's failed run trying to duplicate Shihan's NextCloud files.
Helped Ashu get his Mercurial configuration right, and MOHID-Cmd updated to dev tip.
(MIDOSS)

Sent gemlam2netcdf.sh script to Fred Dupont for assistance.
Added Bitbucket pipeline for coverage run -m pytest and coverage report to NEMO_Nowcast.
Updated gemlam-netcdf.sh script w/ -ip1 option values from Fred.
(SalishSea)

See project work journal.
(GOMSS)

See project journal.
(SalishSeaCast-FVCOM)

Watched Westgrid/Sharcnet webcast about valgrind:
* Tyson Whitehead, sharcnet
* valgrind: memory analysis and debugging
* computers are vonNuemman machines
* physical memory is a large dense 1D array; divided into 4k byte pages; 0 to 2^64
* physical memory is abstracted to a sparse virtual address space per program, also 4k byte pages; segfaults from virtual addresses that have not been mapped to physical addresses
* program memory layout on Linux is ELF standard (early Unix, Sun, etc.)
  * null catch area (unmapped); to catch null pointer errors to generate segfaults
  * code (read/execute)
  * constant data (read); declared in code
  * mutable data (read/write); declared in code
  * heap (read/write); allocated memory pages; grows downward in memory
  * code, constant data & mutable data for libraries; allocations by library code are in program context, so they get allocated from heap
  * stack (read/write); memory version of cpu stack beyond available number of cpu registers; grows upward in memory
  * kernel interface (read/execute)
  * unmapped area to catch -ve addresses and segfault
* many ways that code can be wrong that don't generate segfaults
* readelf -t executable show memory layout
* cat /proc/PID/???
* heap:
  * dlmalloc algorithm; modified version is what is in glibc
    * allocated chunk:
      * chunk size & status flags
      * user data
      * chunk size
    * unallocated chunk:
      * chunk size & status flags
      * double linked list:
        * next free chunk size
        * previous free chunk size
      * unused memory
      * chunk size
    * duplication of chunk size at top and bottom is a speed optimization
  * heap includes records for tracking allocations
  * allocating and releasing leaves holes in heap
  * what can go wrong:
    * allocating without releasing eventually exhausts memory (memory leak?)
    * releasing non-allocated memory or incorrect chunk address messes up glibc
    * invalid read address returns unexpected data unless outside the address space
    * invalid write address overwrites other data unless outside the address space
* stack frame:
  * function args in reverse order (re: variable arg handling)
  * return address
  * local variables
  * scratch space
  * what can go wrong:
    * invalid reads return unexpected data
    * invalid writes overwrite other functions local variables
* so many things that can go wrong (it's a wonder that computers even work)
* valgrind:
  * binary instrumentation framework; dynamically transforms executables to add instrumentation
  * tracks memory and register usages
  * memcheck
  * cachegrind
  * callgrind
  * massif: heap profiler
  * helgrind
  * DRD
  * DHAT
* can be run on any executable thanks to dynamic transformation
* 5-100x slow-down
* 12-18x size increase of executable
* corner cases have failure for high optimization, new features
* use small test cases
* memcheck:
  * over/under-run heap blocks
  * overrun top of stack
  * accessing released memory
* module load valgrind
  * works against gcc and openmpi
  * default tool is memcheck
  * compile w/ -g option to add debugging info to executable
  * demo of array overrun in c
  * demo of array underrun in c
  * demo of accessing freed memory in c
  * demo of double freed memory in c
  * demo of memory leadk due to missing free() in c
  * demo of memory overlap in c (via strcpy())
  * demo of uninitialized variable in c
  * demo of c++ mismatch of array new/delete
  * demo of stack overwrite in c
* running working code under valgrind/memcheck can/will find subtle or non-fatal bugs, but there are still classes of bug it doesn't catch; e.g. stack overwrite
* sharcnet valgrind page about valgrind has some info about using valgrind w/ mpi; need extra stuff to suppress some useless output


Thu 21-Feb-2019
^^^^^^^^^^^^^^^

See project journal.
(SalishSeaCast-FVCOM)

Sent email to Ashu re: changing ownership & permissions on cedar so that def-allen group can see his files.
(MIDOSS)


Fri 22-Feb-2019
^^^^^^^^^^^^^^^

Tracked down paramiko deprecation warning re: cryptography; see #salishseacast.
Finished migration of figure modules to matplotlib-3.0.0:
* Ported:
  * nowcast/figures/research/tracer_thalweg_and_surface_hourly.py
  * nowcast/figures/research/tracer_thalweg_and_surface.py
  * nowcast/figures/comparison/salinity_ferry_track.py
  * nowcast/figures/surface_current_domain.py
  * nowcast/figures/publish/surface_current_tiles.py
(SalishSea)

Helped Ashu sort out his cedar file space and find the next bug in his MOHID replications of Shihan's NextCloud case.
(MIDOSS)

Paper acceptance party at The Gallery re: Allen, Barth, et al.


Sat 23-Feb-2019
^^^^^^^^^^^^^^^

Vancouver to Parksville

Deleted unused/unmaintained custom log msg attrs (`extra` dicts), dependency on driftwood pkg, and JSON log file configuration from SalishSeaNowcast.
Improved SalishSeaNowcast worker success(0 and failure() unit tests.
Continued dev of SalishSeaCmd towards segmented runs; built new Python 3.7.1 conda env on niko.
(SalishSea)


Sun 24-Feb-2019
^^^^^^^^^^^^^^^

Parksville to Vancouver

Continued dev of SalishSeaCmd towards segmented runs; built new Python 3.7.1 conda env on niko.
(SalishSea)


Week 9
------

Mon 25-Feb-2019
^^^^^^^^^^^^^^^

Home sick with probably food poisoning from egg salad sandwich on the ferry.

Continued dev of SalishSeaCmd towards segmented runs.
(SalishSea)


Tue 26-Feb-2019
^^^^^^^^^^^^^^^

Tagged SalishSeaNowcast v3.3 prior to update to matplotlib-3; bumped version to 19.1.dev0.
Built new salishsea-nowcast-3.7 deve env on niko w/ Python 3.7 and matplotlib 3.0.2; updated envs & docs prior to merging matpltlib3_figures branch into default.
Salish Sea team mtg; see whiteboard.
Merged SalishSeaNowcast matplotlib3_figures branch into default.
Installed latest version of miniconda3 in $HOME on skookum.
Built new /SalishSeaCast/nowcast-env with Python 3.7.1 and matplotlib 3.0.2; lots of mucking around with version and pip vs. conda install due to circus incompatibility with pyzmq>17 and tornado>5; ultimately aborted.
(SalishSea)

Discussed cedar run issue w/ Ashu.
(MIDOSS)


Wed 27-Feb-2019
^^^^^^^^^^^^^^^

Installed skype via snap on kudu.

Updated SalishSeaNowcast to a rev that is really pre-matplotlib-3 to fix issue I created with update at the end of yesterday's thrash.
Changed .condarc on skookum et al to store envs in ~/conda_envs/
Built a new ecget conda env in ~/conda_envs/ to replace the one in miniconda3.aside/envs/; changed fraser_buoy.cron.sh to point to new env.
Merged default from niko and vhfr r12 work on kudu.
Created new SalishSeaNowcast Python 3.7 and matplotlib-3 dev env on kudu.
Created new SalishSeaNowcast Python 3.7 and matplotlib-3 fig dev env on kudu.
(SalishSea)

See project journal.
(SalishSeaCast-FVCOM)


Thu 28-Feb-2019
^^^^^^^^^^^^^^^

Created salishsea-site specific Vagrant file.
Started integration of VHFR FVCOM surface currents and thalweg transect image loops.
(salishsea-site)

See project journal.
(SalishSeaCast-FVCOM)


Fri 1-Mar-2019
^^^^^^^^^^^^^^

Westgrid townhall; #compute-canada channel.
Started rsync of GEMLAM-2007-2009 external drive on to /opp/GEMLAM/ with drive mounted on sable.
Built new /SalishSeaCast/nowcast-env with Python 3.7.1 and matplotlib 3.0.3 and flipped production to it.
Created #compute-canada slack channel and moved status feeds to it.
Continued dev of SalishSeaCmd towards segmented runs.
(SalishSea)

Continued integration of VHFR FVCOM surface currents and thalweg transect image loops.
(salishsea-site)

See project journal.
(SalishSeaCast-FVCOM)

Participated in collaboration workshop for SalishSeaCast and Beth Fulton's Atlantis ecosystem model of the Salish Sea.
(MIDOSS)


Sat 2-Mar-2019
^^^^^^^^^^^^^^

Fallout from yesterday's nowcast-env update on skookum:
* Fixed bug in wave_height_period fig module from matplotlib-3 update
* Fixed bug in make_plots re: VHFR x2/r12 model config keys in results archive
* make_plots fvcom forecast publish 2019-03-01
* make_plots fvcom nowcast publish 2019-03-01
(SalishSea)

Worked on hdf5-to-netcdf failure issues w/ Susan:
* works for her on graham
* fails for her on salish due to filling /tmp/; resolved by using TMP=/data/$USER/tmp/
(MIDOSS)

Fixed deprecation warning issue in moad_tools.observations.get_ndbc_buoy() re: pandas.read_table().
Added scipy as dependency re: geo_tools module that Susan added.
(moad_tools)


Sun 3-Mar-2019
^^^^^^^^^^^^^^

UptimeRobot reported that salishsea-site went down at ~01:16.
skookum and salish won't accept ssh connections at ~10:00.
UptimeRobot reported that salishsea-site came up at ~15:03, but file systems are still wonky; back in business at ~17:00; recovery:
* download_weather 06 --debug
* collect_river_data Capilano --data-date 2019-03-02 --debug
* collect_river_data Englishman --data-date 2019-03-02 --debug
* collect_river_data Fraser --data-date 2019-03-02 --debug
* make_runoff_file
* get_NeahBay_ssh forecast2 --debug
* grib_to_netcdf forecast2 --debug
* download_weather 12
* get_onc_ctd SCVIP --debug
* get_onc_ctd SEVIP --debug
* get_onc_ctd USDDL --debug
* get_onc_ferry TWDP --debug
* get_vfpa_hadcp --data-date 2019-03-02 --debug
* download_weather 18
* collect_weather 00
Neah Bay ssh ops data had rolled away by the time I was able to run get_NeahBay_ssh; recover:
* Susan crafted an ssh txt file
* get_NeahBay_ssh $NOWCAST_YAML nowcast --text-file sshNB_2019-03-04_sea.txt --debug
(SalishSea)

Explored docker for pyramid app dev:
* https://medium.freecodecamp.org/docker-development-workflow-a-guide-with-flask-and-postgres-db1a1843044a
* conda create -n pyramid-docker python=3.7 pip
* pip install pyramid
* conda env export -n pyramid-docker -f environment.yaml
* https://medium.com/backticks-tildes/how-to-dockerize-a-django-application-a42df0cb0a99
* The key to getting an reloading dev env working is to use docker-compose

Helped Susan get salishsea-site vagrant VM up and running so that she could improve acknowledgements on the site.
(salishsea-site)


March
=====

Week 10
-------

Mon 4-Mar-2019
^^^^^^^^^^^^^^

Added instructions for vagrant as pinned msg in #attribution-for-onc channel.
(salishsea-site)

Pulled SalishSeaNowcast rev 391a85754d8c into production re: x2/r12 in download_fvcom_results.
forecast/04mar19 got stuck at 84.7% due to a file length issue in atmos forcing; upload_forcing nowcast+ got triggered before grib_to_netcdf finished due to race conditions between grib_to_netcdf and make_live_ocean_files; recovery:
* kill xios_server.exe on west.cloud
* kill watch_NEMO on west.cloud
* wait for SalishSeaNEMO.sh script to finish on west.cloud
* upload_forcing west.cloud nowcast+ --debug
* make_forcing_links west.cloud nowcast+ --debug
* make_forcing_links west.cloud ssh
* upload_forcing cedar nowcast+ --debug
* upload_forcing orcinus nowcast+ --debug
* make_forcing_links orcinus nowcast+ --debug
Queued a detached XIOS run on cedar to test new OPA version.
Started working on profiling make_plots.
(SalishSea)

See project journal.
(SalishSeaCast-FVCOM)

EOAS seminar about coastal trapped waves in the south Caspian Sea by Mina Masoud.

Talked to Ashu about interpolation weights for wwatch3 to MOHID.
(MIDOSS)


Tue 5-Mar-2019
^^^^^^^^^^^^^^

Confirmed the numpy boolean indexing that Susan and I discussed last night over dinner; see #random channel.
Helped Ashu re-install moad_tools, NEMO-Cmd & MOHID-Cmd and confirm that he has a working env on cedar.
Email discussion w/ Krista about AIS data mgmt and export from ArcMap.
(MIDOSS)

Salish Sea team mtg; see whiteboard.

Refactored figures mgmt classes into separate module.
(salishsea-site)

See project journal.
(SalishSeaCast-FVCOM)


Wed 6-Mar-2019
^^^^^^^^^^^^^^

Backfilled upload_forcing to cedar for 1-5-Mar re: downtime.
Deployed VHFR make_plots split into publish & research.
(SalishSea)

Answered Ashu's questions about why he got waves.hdf5 output file from MOHID.
(MIDOSS)

See project journal.
(SalishSeaCast-FVCOM)

See project work journal.
(GOMSS)


Thu 7-Mar-2019
^^^^^^^^^^^^^^

upload_forcing nowcast+ got triggered before grib_to_netcdf finished due to race conditions between grib_to_netcdf and make_live_ocean_files; recovery:
* tried upload_forcing west.cloud nowcast+ --debug before forecast run got stuck, but it errored out
* upload_forcing cedar nowcast+ --debug
* upload_forcing orcinus nowcast+ --debug
* kill xios_server.exe on west.cloud
* kill watch_NEMO on west.cloud
* wait for SalishSeaNEMO.sh script to finish on west.cloud
* upload_forcing west.cloud nowcast+ --debug
* make_forcing_links west.cloud nowcast+ --debug
* make_forcing_links west.cloud ssh
* make_forcing_links orcinus nowcast+ --debug
Sent email to Venkat re: arbutus.cloud migration and my schedule until after SoPO.
(SalishSea)

Changed randopony.randonneurs.bc.ca to HTTPS and added HTTP->HTTPS redirection via .htaccess.

See project work journal.
(GOMSS)

See project journal.
(SalishSeaCast-FVCOM)


Fri 8-Mar-2019
^^^^^^^^^^^^^^

See project work journal.
(GOMSS)

See project journal.
(SalishSeaCast-FVCOM)

Advised Hayley Dosser @Hakai on how to get T&S fields from SalishSeaCast ERDDAP to produce boundary conditions for Discovery Islands FVCOM model.
(SalishSea)

Started work on setting up 2019 bloomcast:
* runs dir: /data/dlatorne/SOG-projects/SoG-bloomcast-ensemble/run/
* cp 2018_bloomcast_inifile.yaml 2019_bloomcast_infile.yaml
* archived 2018* files in run/2018/
* archived bloomcast.log and bloom_date_evolution.log files into run/2018/
* edit 2019_bloomcast_infile.yaml
* edit config.yaml
* disable push to web for test run
* build /data/dlatorne/SOG-projects/bloomcast-env-mpl-1.5.3 conda env
* pip install -e /data/dlatorne/SOG-projects/SOG
* pip install -e /data/dlatorne/SOG-projects/SoG-bloomcast-ensemble
* test run: cd run && bloomcast ensemble -v config.yaml
* test run succeeded: 13mar 14mar 24mar 14apr 14apr
* enabled push to web
* deleted wind_data_date to allow repeat run for today
* changed cronjob.sh to use new env
* ran manual production run w/ bash ./cronjob.sh; success! :-)
* checked bloomcast page on salishsea-site
* emailed Jim Gower
* posted link to SalishSeaCast whiteboard
* enable cron job on salish
* commit 2018 config files
* edit new weather descriptions into cloud fraction file and commit

* tag for 2018
(bloomcast)

Explored trying to speed up hdf5-to-netcdf on cedar by setting TMPDIR to $SLURM_TMPDIR to node-local SSD storage:
* cdr783 20000m TMPDIR=/tmp: 14m11s 4m45s for ncrcat (timed out of 10min interactive session)
* cdr783 20000m TMPDIR=$SLURM_TMPDIR: 14m21s
* cdr648 1000m TMPDIR=$SLURM_TMPDIR: 17m18s
* cdr648 800m TMPDIR=$SLURM_TMPDIR cp to $SLURM_TMPDIR: 11m23s
* cdr612 800m TMPDIR=$SLURM_TMPDIR cp to $SLURM_TMPDIR: 17m11s
* changed hdf5-to-netcdf to use $SLURM_TMPDIR by default if it exists
(MIDOSS)


Sat 9-Mar-2019
^^^^^^^^^^^^^^

1st cut on 2018 income tax returns.

More testing of hdf5-to-netcdf using $SLURM_TMPDIR:
* cdr767 all by myself :-) cp hdf5 to $SLURM_TMPDIR/; hdf5-to-netcdf using new default: 9m50s

(MIDOSS)


Sun 10-Mar-2019
^^^^^^^^^^^^^^^

collect_weather 06 stalled with 489 of 576 file collected; recovery:
* kill collect_weather 06
* rm -rf /results/forcing/atmospheric/GEM2.5/GRIB/20190310/06
* download_weather 06 --debug
* collect_river_data Capilano 2019-03-09
* collect_river_data Englishman 2019-03-09
* collect_river_data Fraser 2019-03-09
* get_onc_ctd SCVIP
* get_onc_ctd SEVIP
* get_onc_ctd USDDL
* get_onc_ferry TWDP
* get_vfpa_hadcp 2019-03-09
* get_NeahBay_ssh forecast2 --debug
* grib_to_netcdf --debug
* upload_forcing west.cloud-nowcast forecast2 --debug
* upload_forcing orinus-nowcast-agrif forecast2 --debug
* upload_forcing cedar-hindcast forecast2 --debug
* download_weather 12
* collect_weather 18
(SalishSea)


Week 11
-------

Mon 11-Mar-2019
^^^^^^^^^^^^^^^

Shihan Li & Xiaomei Zhong visiting from Dal re: MIDOSS

Introduced Shihan and Xiaomei to version control, Bitbucket, and Mercurial.
Shihan presented MOHID model.
Worked w/ Shihan, Rachael & Xiaomei to create new MIDOSS-MOHID-CODE repo from Shihan's Visual Studio "UBC new" project on his Dal workstation.
Dinner w/ part of MIDOSS team at Mahoney's.
(MIDOSS)

collect_weather 12 stalled; investigation showed that it was due to hours 25 and 26 files apparently not being uploaded; emailed Sandrine who got files uploaded, and automation took it from there.
(SalishSea)


Tue 12-Mar-2019
^^^^^^^^^^^^^^^

Shihan Li & Xiaomei Zhong visiting from Dal re: MIDOSS

Susan presented NEMO grid and VVL
Got MIDOSS-MOHID-CODE repo to build and run some time steps on cedar, todos & things to know to change from MIDOSS-MOHID to new repo:
* clone MIDOSS-MOHID-CODE repo
* build MOHID
* update paths: mohid repo: value in YAML files
* Waves.dat must include whitecap coverage WAVE_WCC = 1 and a wavewcc block
* MIDOSS-MOHID-config/SalishSea/Waves.dat has those for simple case of constant zero whitecap coverage
Xiaomei presented plans for her PhD work on modeling dilbit and synbit.
Tried to re-run ww3-nowcast/16nov17 but failed because NEMO forecast/16nov17 grid_U and grid_V are needed by make_ww3_current_file and they are archived; sent email to Rachael & Ashu.
(MIDOSS)

Salish Sea team mtg; see whiteboard.
(SalishSea)


Wed 13-Mar-2019
^^^^^^^^^^^^^^^

Shihan Li & Xiaomei Zhong visiting from Dal re: MIDOSS

Supported sprint.
Created rpn-to-gemlam project & repo.
(MIDOSS)

See project work journal.
(GOMSS)

Met w/ Henryk re: working on optimum cluster & learned about ndf5 & netcdf4 libs; cloned repos similar to orcinus & cedar for runs automated via ssh.
(SalishSea)


Thu 14-Mar-2019
^^^^^^^^^^^^^^^

4 chain-drops on Shadowfax on the ride in to UBC :-(

Shihan Li & Xiaomei Zhong visiting from Dal re: MIDOSS

Discussed combined SalishSeaCast and VHFR FVCOM runs in MOHID.
(MIDOSS)

Created #ww3-handcast slack channel.
Continued work on rpn-to-gemlam.
Built XIOS-2 on optimum:
* arch-GCC_OPTIMUM.*
* ./make-xios --arch GCC_OPTIMUM --netcdf_lib netcdf4_seq
(SalishSea)


Fri 15-Mar-2019
^^^^^^^^^^^^^^^

Monthly project mtg by skype.
(MIDOSS)

Started work on building NEMO SalishSeaCast config on optimum; stalled by compile error in trcbc & trc (see #salishseacast channel).
Re-created SalishSeaNowcast rtd-Bitbucket webhook to try to get rid of warning on rtd.
(SalishSea)

See project work journal.
(GOMSS)

Made Birgit a maintainer on ubc-moad-docs rtd project so that she can trigger builds when Bitbucket webhook fails to.
(MOAD)

Bought an 8Tb external drive to replace the failed GEMLAM 2010-2014 drive.

Tried to set up .htaccess redirect for https://salishsea.eos.ubc.ca/bloomcast/spring_diatoms to  https://salishsea.eos.ubc.ca/bloomcast/spring_diatoms
(bloomcast)


Sat 16-Mar-2019
^^^^^^^^^^^^^^^

Woke up very depressed.

upload_forcing nowcast+ got triggered before grib_to_netcdf finished due to race conditions between grib_to_netcdf and make_live_ocean_files; recovery:
* upload_forcing cedar nowcast+ --debug
* upload_forcing orcinus nowcast+ --debug
* kill xios_server.exe on west.cloud
* kill watch_NEMO on west.cloud
* wait for SalishSeaNEMO.sh script to finish on west.cloud
* upload_forcing west.cloud nowcast+ --debug
* make_forcing_links west.cloud nowcast+ --debug
* make_forcing_links west.cloud ssh
* make_forcing_links orcinus nowcast+ --debug
Got NEMO SalishSeaCast config built on optimum after a code patch by Susan to work around gcc 4.4.7 issue re: allocation of namelist elements that disappears in gcc 4.8.4 on salish & west.cloud.
Set up forcing, scratch & results areas on optimum.
Got tmp run dir created on optimum; hacked SalishSeaNEMO.sh enough to get it on the queue and started but get an "insufficient slots" error; I think it is due to mpirun -np ...
(SalishSea)

Added missing pkgs to autodocs mocks for moad-tools docs and improves  hdf5_to_netcdf4.cli() docstring.
(MOAD)


Sun 17-Mar-2019
^^^^^^^^^^^^^^^

upload_forcing nowcast+ got triggered before grib_to_netcdf finished due to race conditions between grib_to_netcdf and make_live_ocean_files; recovery:
* upload_forcing cedar nowcast+ --debug
* upload_forcing orcinus nowcast+ --debug
* kill xios_server.exe on west.cloud
* kill watch_NEMO on west.cloud
* wait for SalishSeaNEMO.sh script to finish on west.cloud
* upload_forcing west.cloud nowcast+ --debug
* make_forcing_links west.cloud nowcast+ --debug
* make_forcing_links west.cloud ssh
* make_forcing_links orcinus nowcast+ --debug
Resumed work on race condition mgmt in NEMO_Nowcast.
(SalishSea)

Vancouver to Ardmore for SoPO meeting.


Week 12
-------

Mon 18-Mar-2019
^^^^^^^^^^^^^^^

SoPO Mtg - Mary Windpear Centre, Sidney

Faron Anslow: Land temperature and hydrological conditions in 2018
* La Nina now == previous normal
* May 18 floods almost all freshet
* fall is meh! in terms of climate change
* winter djf 18/19 normal as a whole despite cold dry Feb

Tetjana Ross: Temperature, salinity and density of the NEP using Argo, satellite and Line P data
* 2018 was 4th warmest year globally
* 2018 weak La Niña, 2019 weak El Niño
* warm indicators for 2019 despite cold Feb

Charles Hannah: Ocean Surface Temperatures in 2018 – another marine heat wave?
* classification of marine heat waves
* weather in BC isn't caused by El Niño

Roy Hourston: Wind-driven upwelling along the Northwest coast of North America: timing and magnitude

Peter Chandler: Sea surface temperature and salinity at BC lighthouses
* lighthouse observations have been moved from DFO to public data portal
* broad freshening trend due to increased precipitation

Bill Crawford: Changes in Oxygen Concentration in BC shelf and deep-sea waters
* shift to lower O2 at LB08 since 2006; 2015 is anomalous

Jim Gower: Satellite observations of BC waters
* 29-May-2018 ESA satellite show Fraser River plume bloom; heterosigma; also 9-Jun-2018; 16-Jun Barkely Sound; 709 nm band

Anne Ballantyne: Water level observations on the BC coast

Jennifer Jackson: Interdecadal oceanographic trends in Rivers Inlet, BC
* peak freshet delayed into Aug for 4th yr in a row; glacial melt
* first time hypoxic water upwelled in has been observerd; probablly due to prolonged upwelling on the shelf
* warmer due to persistence into 2018 of sub-surface marine heat wave

Angelica Pena: Results from phytoplankton monitoring at Line P and the west coast of Vancouver Island

Moira Galbraith: West coast zooplankton: annual anomaly time series
* 2018 pretty much the same as 2017

Sonia Batten: An update on oceanic and west coast shelf/slope plankton populations from the CPR survey

Ian Perry: West Coast of Vancouver Island small mesh multispecies bottom trawl survey (target species: smooth pink shrimp) – 2018 update
* cluster analysis shows 2018 similar to 2017 but different from 2016

Jennifer Boldt and Jaclyn Cleary: Pelagic fish: an update on Pacific Herring status and trends

Jennifer Boldt: Eulachon update: Fraser River Egg and Larval Survey and West Coast of Vancouver Island Small Mesh Bottom Trawl survey
* cool Eulachon research

Greg Workman: A review of groundfish surveys in 2018 and an introduction to the groundfish data synopsis report
* github!

Wiley Evans: 2018 Coastal Ocean Conditions Revealed by the Hakai Institute’s Continuous CO2 Datasets
* https://hecate.hakai.org data portal

Mark Hipfner: Seabird observations on the BC Coast

Jessica Heke: Canadian Hydrographic Service Pacific: activities and results

Matthais Herborg: Oil spills in BC waters
* diesel, gasoline, uncategorized hydrocarbon (in order) most common
* HMCS Calgary fuel transfer incident; 20k l naval diesel over 5 hours; 20 kn wind spread it
* Lina Island lodge grounding grounding; 33k l onboard; very little spilled in the end; sponge-bob deployment

Hauke Blanken: A snapshot of 2018 NE Pacific conditions from ECCC’s new CIOPS-W forecasting system
* public results in summer
* daily average whole water column
* hourly average surface

Continued work on race condition mgmt in NEMO_Nowcast.
(SalishSea)


Tue 19-Mar-2019
^^^^^^^^^^^^^^^

**Bloom Day**

SoPO Mtg - Mary Windpear Centre, Sidney

Reflections and highlights on day 1
* 2015-2016 marine heat wave affects are working their way through trophic levels
* marine heat waves may become a new (regular or not) recurring pattern
* flooding has produced massive geomorphic changes in rivers and stream that will feed back to salmon

Peter Chandler: The 2018 Strait of Georgia Water Properties Surveys
* 4 SoG cruises per year; spring bloom, peak freshet, fall quiet, winter storms
* low O2 signal
* early, rapid, high Fraser freshet, then below average until fall rain storms brought is above normal again

Akash Sastri: Deep water and sea surface properties in the Strait of Georgia during 2018: Cabled instruments and ferries
* SoG is warm since 2014; winter cooling has resumed in 2017 & 2018 but temperature is still above normal
* 2018 bloom early
* 2019 bloom started 9-Mar; maybe peak on 17-Mar

Susan Allen: Spring bloom and interannual variations in primary productivity in the SoG

Nina Nemcek: Seasonal dynamics of the phytoplankton community in the Strait of Georgia
* HPLC ground truthed by microscopy
* centric diatoms dominate in spring bloom
* massive June bloom in JdF; heterosigma (HAB); likely triggered by Fraser freshet
* low diatoms in Jun in all areas
* very diverse community of flagellates in northern SoG
* large fall bloom in northern SoG; pennate diatom pseudo-nitzschia (HAB)
* fall is most generally diverse
* diatoms are replaced by flagellates when nitrate is depleted, and diatoms don't return when nitrate is replenished

Kelly Young: Zooplankton status and trends in the central Strait of Georgia, 2018
* copepods dominate zooplankton community; especially little ones

(not) Svetlana Esenkulova: The phytoplankton community and harmful algae in the Salish Sea

Sue Grant: The State of the Salmon initiative

Sue Grant Fraser River Sockeye: abundance and productivity trends


nowcast/19ma19 delayed due to connection refused errors for downloads by `sarracenia` client during 1st 12 hours of 12 forecast. Recovered by running `download_weather` worker manually. It stalled in hour 31 on the first attempt, but succeeded on a 2nd attempt.
Resumed work on race condition mgmt in NEMO_Nowcast and SalishSeaNowcast.
(SalishSea)

Sidney to Vancouver after SoPO mtg.


Wed 20-Mar-2019
^^^^^^^^^^^^^^^

Deployed NEMO_Nowcast race condition management and SalishSeaNowcast grib_to_netcdf/make_live_ocean_files race condition identification to skookum; mostly worked.
`sarracenia` glitched again today during `collect_weather 12`, but I caught it earlier and manually ran `dowload_weather 12`. Before doing so I patched production with race condition management and it mostly behaved as expected (although the bad result of the `grib_to_netcdf`/`make_live_ocean_files` race conditions didn't happen today).
Recovered manually from a bug in NEMO_Nowcast race condition mgmt that caused manager restart on execution of after_*() that returns 2 or more NextWorker instances.
Slack discussion w/ Henryk re: slots issue on optimum.
Finished NEMO_Nowcast race condition management feature and wrote docs for it.
Moved SalishSeaNowcast v3.3 tag to default branch.
Changed salishsea_tools.data_tools.onc_json_to_dataset() to use timezone-naive datetimes; avoids warnings like:
  /SalishSeaCast/nowcast-env/lib/python3.7/site-packages/xarray/core/variable.py:134:
  FutureWarning: Converting timezone-aware DatetimeArray to timezone-naive
  ndarray with 'datetime64[ns]' dtype. In the future, this will return
  an ndarray with 'object' dtype where each element is a
  'pandas.Timestamp' with the correct 'tz'.
    To accept the future behavior, pass 'dtype=object'.
    To keep the old behavior, pass 'dtype="datetime64[ns]"'.
    return np.asarray(pd.Series(values.ravel())).reshape(values.shape)
that get_onc_ctd was raising.
Updated /SalishSeaCast/grid/mesh_mask201702.nc with Susan's new version and pinged ERDDAP.
(SalishSea)

Got RAC allocation; much less than requested due to lack of publications.

See project work journal.
(GOMSS)


Thu 21-Mar-2019
^^^^^^^^^^^^^^^

Woke up with upset, gassy guts.

`sarracenia` glitched again today several times during `collect_weather 12` while I watched it; manually ran `dowload_weather 12` at ~10:00 to recover. It stalled in hour 25 on the first attempt, but succeeded on a 2nd attempt. Sadly, I had messed up NEMO_Nowcast deployment by reverting test patches and not pulling in committed work; re-ran download_weather 12 again to confirm that race condition management works, and it got stuck at hour 29, and again, and worked on 3rd try.
Race condition mgmt worked, and averted hung forecast because make_live_ocean_files finished before grib_to_netcdf.
Met w/ Henryk re: NEMO on optimum:
* I will test w/ mpich
* he will hack qsub to add slots to nodelist file
Started mpich scaling runs on optimum:
* 2nodes-4x9+1 timed out on track for ~5h
* 5nodes-11x14 1h18m11s
* 10nodes-11x33
* 14nodes-16x34 timed out at 1h
(SalishSea)

EOAS colloquium by Julie Keister of UW re: climate effects on Puget Sound zooplankton


Fri 22-Mar-2019
^^^^^^^^^^^^^^^

See project work journal.
(GOMSS)

`sarracenia` glitched again today several times during `collect_weather 12` while I watched it; manually ran `dowload_weather 12` at ~09:20 to recover; stalled at hour 36; retry succeeded.
Continued mpich scaling runs on optimum:
* 14nodes-16x34 49m47s
* 10nodes-11x33 55m38s
* REBUILD_NEMO fails w/ exit code 9
Formatted new 8Tb GEMLAM-2012-2014 drive and delivered it to Robert@ECCC.
Continued dev of rpn-to-gemlam.
(SalishSea)

See project journal.
(SalishSeaCast-FVCOM)


Sat 23-Mar-2019
^^^^^^^^^^^^^^^

Continued dev of rpn-to-gemlam.
I must have forgotten to start collect_weather 18 after yesterday's recovery:
* download_weather 18 --yesterday --debug
* download_weather 00 --debug
* download_weather 06
* collect_weather 18
* download_weather 12
orcinus lustre file system failed at ~14:00
Built XIOS-2 and NEMO/SalishSeaCast on optimum against new OpenMPI/4.0.0/GCC/SYSTEM module that Henryk built.
OpenMPI scaling runs on optimum:
* 14nodes-16x34 17m11s
* REBUILD_NEMO fails w/ exit code 9
Built XIOS-2 and NEMO/SalishSeaCast on optimum against new OpenMPI/2.1.6/GCC/SYSTEM module that Henryk built.
OpenMPI scaling runs on optimum:
* 14nodes-16x34 32m16s
(SalishSea)

Worked with Susan on wwatch3 hindcast.
(MIDOSS)


Sun 24-Mar-2019
^^^^^^^^^^^^^^^

Create PR#2849 in xarray re: fixing 1 more collections.abc deprecation warning.

Continued working with Susan on wwatch3 hindcast.
Added nowcast run type to make_ww3_wind_file.
grib_to_netcdf failed for 06 and 12 forecasts due to /data file system issue:
* /data came back at ~11:45
* grib_to_netcdf nowcast+
* upload_forcing west.cloud nowcast+
* upload_forcing cedar nowcast+
(MIDOSS)

Susan confirmed that optimum runs produce readable results files that don't differ significantly from archived results.
Repeat optimum OpenMPI/2.1.6/GCC/SYSTEM test run:
* 14nodes-16x34 --bind-to core: time stepping finished in <14m but completion took 18m57s
* 12nodes-15x30 --bind-to core 36m52s
* 12nodes-15x30 --bind-to core repeat #1
(SalishSea)


Week 13
-------

Mon 25-Mar-2019
^^^^^^^^^^^^^^^

See project work journal.
(GOMSS)

See project journal.
(Resilient-C)

`sarracenia` glitched again today during `collect_weather 12`; manually ran `dowload_weather 12` at ~13:15 to recover.
Started backfilling nowcast-agrif runs after orcinus lustre filesystem issue over the weekend:
* upload_forcing orcinus nowcast+ 2019-03-23 --debug
* make_forcing_links orcinus nowcast+ 2019-03-23 --debug
* make_forcing_links orcinus turbidity 2019-03-23 --debug
* upload_forcing orcinus nowcast+ 2019-03-24 --debug
* make_forcing_links orcinus nowcast+ 2019-03-24--debug
* make_forcing_links orcinus turbidity 2019-03-24 --debug
* make_forcing_links nowcast-agrif 2019-03-23
* make_forcing_links nowcast-agrif 2019-03-24
* make_forcing_links nowcast-agrif 2019-03-25
Started adding nowcast run type to make_ww3_current_file.
(SalishSea)

Phys Ocgy seminar by Ben S


Tue 26-Mar-2019
^^^^^^^^^^^^^^^

See project journal.
(SalishSeaCast-FVCOM)

See project work journal.
(GOMSS)

Finished adding nowcast run type to make_ww3_current_file.
SalishSea team mtg; see whiteboard.
(SalishSea)


Wed 27-Mar-2019
^^^^^^^^^^^^^^^

See project journal.
(SalishSeaCast-FVCOM)

See project work journal.
(GOMSS)


Thu 28-Mar-2019
^^^^^^^^^^^^^^^

See project journal.
(SalishSeaCast-FVCOM)

See project work journal.
(GOMSS)

Started adding support for optimum cluster to SalishSeaCmd.
(SalishSea)

Attended EOAS poster corral; Vicky won people's choice.


Fri 29-Mar-2019
^^^^^^^^^^^^^^^

See project journal.
(SalishSeaCast-FVCOM)

PyCharm updated to PyCharm 2019.1 Build #PY-191.6183.50 that includes task name underscore big fix, and activation of conda env in terminal; also some interesting looking changes to how notebooks work within PyCharm.

See project journal.
(Resilient-C)


Sat 30-Mar-2019
^^^^^^^^^^^^^^^

See project journal.
(Resilient-C)

See project journal.
(SalishSeaCast-FVCOM)


Sun 31-Mar-2019
^^^^^^^^^^^^^^^

See project journal.
(Resilient-C)

See project journal.
(SalishSeaCast-FVCOM)

Did Iona ride solo with 20.6 avg; 1st time over 20 in a while :-)


April
=====

Week 14
-------

Mon 1-Apr-2019
^^^^^^^^^^^^^^

Created #beluga-into-herd channel; started todo post
Finished adding support for optimum cluster to SalishSeaCmd.
Got serious about scaling study on optimum; see Google spreadsheet.
Resumed work on SalishSeaCmd segmented runs.
(SalishSea)

See project journal.
(SalishSeaCast-FVCOM)


Tue 2-Apr-2019
^^^^^^^^^^^^^^

Telcon w/ Kate re: Dad's accounts.

Continued work on SalishSeaCmd segmented runs.
Continued scaling study on optimum; see Google spreadsheet:
* mostly finished OpenMPI 2.1.6 tests
* 8 node job failed due to core binding issue; reported to Henryk
* built XIOS-2 and NEMO SalishSeaCast against OpenMPI 3.1.3
  * 14 node tests were slightly slower than 2.1.6
* built XIOS-2 and NEMO SalishSeaCast against OpenMPI 4.0.0
  * 14 node tests
(SalishSea)

See project journal.
(SalishSeaCast-FVCOM)


Wed 3-Apr-2019
^^^^^^^^^^^^^^

LiveOcean product was not available for download until ~11:20, but automation and patience handled it.
Started setup of beluga:
  ssh-copy-id
  maybe different project file spaces for def-allen and rrg-allen ???
  no nco module
Started writing docs for working on beluga in MOAD/docs/.
(SalishSea)

See project journal.
(SalishSeaCast-FVCOM)


Thu 4-Apr-2019
^^^^^^^^^^^^^^

See project journal.
(SalishSeaCast-FVCOM)

LiveOcean product was slow again, and timed out; re-ran manually twice before it succeeded at ~16:00.
Ran 8 node test on optimum thanks to -map-by core in mpiexec command.
Continued working on beluga setup; discussed and figured out storage trees w/ Susan; discussed move to newer xios-2 that will compile with Intel 2018.3.
(SalishSea)

See project journal.
(Resilient-C)

EOAS colloquium on phytoplankton proteomics by Erin Bertrand from Dalhousie


Fri 5-Apr-2019
^^^^^^^^^^^^^^

See project journal.
(SalishSeaCast-FVCOM)

Changed config to specify 2 ports for fvcom workers on west.cloud to facilitate concurrency for x2 and r12 nowcast runs prep, execution, and watching; changed firewall rules on west.cloud nowcast0 VM to open new ports; updated west.cloud deployment docs re: new rules.
LiveOcean product was slow again, and timed out; re-ran manually twice before it succeeded at ~16:40; fvcom workers failed to launch.
Continued work on SalishSeaCmd segmented runs.
(SalishSea)

Attended Idalia's M.Sc. defense.


Sat 6-Apr-2019
^^^^^^^^^^^^^^

LiveOcean product was slow again...
Added NEMO_Nowcast feature to allow multiple logging ports for remote workers to facilitate concurrent VHFR nowcast x2 & r12 runs.
Discussed with Susan adding collection of more real-time river discharges to the system.
(SalishSea)

Worked on income tax returns.


Sun 7-Apr-2019
^^^^^^^^^^^^^^

LiveOcean product was ready shortly after collect_weather 00 finished!!
collect_river_data didn't run for the rivers that Susan added yesterday because I didn't think to restart the manager to make them available to after_collect_weather().
(SalishSea)

Finalized and files 43ravens GST return, and income tax returns.


Week 15
-------

Mon 8-Apr-2019
^^^^^^^^^^^^^^

SalishSeaCast blew up before forecast2 runs due to more workers than logging ports on skookum thanks to 9 new collect_river_data instances; Susan got things resolved enough to get the forecast2 runs launched at ~07:30; rest of recovery:
* collect_river_data TheodosiaScotty 2019-04-07
* get_onc_ctd SCVIP
* get_onc_ctd SEVIP
* get_onc_ctd USDDL
* get_onc_ferry TWDP
* get_vfpa_hadcp 2019-04-07
* Added 6 new worker logging .pub/sub ports to skookum list
Backfilled get_onc_ferry TWDP for 21Mar-25Mar to update O2 observations due to ONC software update issue that Rich alerted me to in 1Apr email.
Set up $PROJECT/SalishSea/forcing/ tree on beluga and added it to nowcast.yaml so that it is updated daily.
(SalishSea)

See project journal.
(SalishSeaCast-FVCOM)

See project journal.
(Resilient-C)


Tue 9-Apr-2019
^^^^^^^^^^^^^^

See project journal.
(SalishSeaCast-FVCOM)

See project journal.
(Resilient-C)

All early morning workers launched and completed successfully.
LiveOcean product was slow again; timed out at 12:11; re-launched manually at ~12:30; product available at ~13:30.
Concurrent VHFR x2 and r12 nowcast runs launched successfully under automation.
Continued work on beluga setup:
* successfully built xios-2 svn rev 1600 on beluga
* cloning repos from Bitbucket kept timing out, but got:
  * XIOS-ARCH
  * grid
  * tides
  * tracers
  * NEMO-Cmd
  * SalishSeaCmd
  * NEMO-3.6-code
* Installed NEMO-Cmd and SalishSeaCmd w/ python3.7 -m pip install --user -e
* NEMO SalishSeaCast build failed with multiple instances of::

    /cvmfs/soft.computecanada.ca/easybuild/software/2017/avx512/Compiler/intel2018.3/openmpi/3.1.2/include/mpif-sizeof.h(213): error #5286: Ambiguous generic interface MPI_SIZEOF: previously declared specific procedure MPI_SIZEOF_COMPLEX32_R12 is not distinguishable from this declaration. [MPI_SIZEOF_COMPLEX32_R12]

  which I traced to https://forge.ipsl.jussieu.fr/nemo/ticket/1799 and its fix at https://forge.ipsl.jussieu.fr/nemo/changeset/8537
  So, I copied NEMO/OPA_SRC/LBC/lib_mpp.F90 into MY_SRC/ and hacked out 2 instances of::

    USE lbcnfd          ! north fold

    INCLUDE 'mpif.h'

  and tried the build again, and was successful.
Set up /data/sallen/shared/SalishSeaCast/forcing/ tree on optimum
make_turbidity_file failed due to inconsistent time stamp issue; recovery:
* ln -s riverTurbDaily2_y2019m04d08.nc riverTurbDaily2_y2019m04d09.nc
* upload_forcing west.cloud turbidity
* upload_forcing orcinus turbidity
* upload_forcing cedar turbidity
* upload_forcing beluga turbidity
* upload_forcing optimum turbidity
(SalishSea)


Wed 10-Apr-2019
^^^^^^^^^^^^^^^

See project journal.
(SalishSeaCast-FVCOM)

Email w/ Tereza re: working on graham & beluga, and SalishSeaCmd segmented runs.
Set up $PROJECT/SalishSea/forcing/ tree on graham` and added it to nowcast.yaml so that it is updated daily.
(SalishSea)

Phys Ocgy seminars by Ashu & Iris (co-op students)



  /home/dlatorne/projects/def-allen/dlatorne/MEOPAR/NEMO-3.6-code/NEMOGCM/CONFIG/SalishSeaCast/BLD/ppsrc/nemo/p4zflx.f90(395): warning #6178: The return value of this FUNCTION has not been defined.   [P4Z_FLX_ALLOC]
     INTEGER FUNCTION p4z_flx_alloc()
  --------------------^

warning I noticed in beluga build yesterday - bad code smell.
Got SS-run-sets & rivers-climatology repos on to beluga by rsync-ing them from salish after a bunch more tries that timed out.
Picked up GEMLAM disk from Robert@ECCC.
(SalishSea)


Thu 11-Apr-2019
^^^^^^^^^^^^^^^

Worked on Mom and Dad's 2018 income tax returns.

Helped Tereza diagnose and report cedar file system issue.
(SalishSea)


Fri 12-Apr-2019
^^^^^^^^^^^^^^^

Wrote report on 2018-2019 MEOPAR Prediction Core work.


Sat 13-Apr-2019
^^^^^^^^^^^^^^^

Vancouver to Parksville


Sun 14-Apr-2019
^^^^^^^^^^^^^^^

make_turbidity_file failed due to inconsistent time stamp issue; recovery:
* ln -s riverTurbDaily2_y2019m04d13.nc riverTurbDaily2_y2019m04d14.nc
* upload_forcing west.cloud turbidity
* upload_forcing orcinus turbidity
* upload_forcing cedar turbidity
* upload_forcing beluga turbidity
* upload_forcing optimum turbidity
(SalishSea)

Parksville to Vancouver


Week 16
-------

Mon 15-Apr-2019
^^^^^^^^^^^^^^^

Woke up with low energy, slight headache, sinus congestion, and pain the centre of my chest.

See project journal.
(SalishSeaCast-FVCOM)

Email w/ Tereza re: working on graham & beluga, and SalishSeaCmd segmented runs.
Set up $PROJECT/SalishSea/forcing/ tree on graham` and added it to nowcast.yaml so that it is updated daily.
(SalishSea)

Phys Ocgy seminars by Ashu & Iris (co-op students)


Tue 16-Apr-2019
^^^^^^^^^^^^^^^

Copied SalishSeaNEMO-nowcast key to graham and re-ran upload_forcing forecast2.
Charles started Ububtu 16.04 LTS upgrades:
* salish done
* ocean done
* skookum done
16.04 upgrade interrupted:
* collect_weather 12; launched download_weather 12 manually to recover
* ERDDAP; restarted automatically from /etc/rc.local
* salishsea-site; restarted manually
* SalishSeaNowcast; restarted manually
* watch_NEMO_agrif; restarted manually
* collect_weather 18; launched download_weather 18 and collect_weather 00 instead
Continued work on SalishSeaCmd segmented runs.
nowcast-dev failed on launch; traced to change in libmpi.so version; XIOS-2 and SalishSeaCast_Blue NEMO config on salish need to be rebuilt; XIOS-2 build attempt failed, traced to http://forge.ipsl.jussieu.fr/nemo/discussion/topic/28
(SalishSea)

Dr. appt at 16:20.


Wed 17-Apr-2019
^^^^^^^^^^^^^^^

Started migration to arbutus.cloud:
* researched ed25519 keys, but openstack doesn't support as of queens release that is on arbutus.cloud
* generated new arbutus.cloud_id_rsa key pair on kudu and uploaded public key via web console
* launched an Ubuntu 18.04 LTS minimal VM with the nemo-c8-60gb-90 flavour as nowcast0
* associated public ip address w/ nowcast0
* added ssh access rule to security group
* ssh-ed in from kudu
* created #arbutus-into-herd channel
(SalishSea)

See project journal.
(SalishSeaCast-FVCOM)

Investigated FutureWarning re: matplotlib datetime converter registration; best explanation is https://pandas.pydata.org/pandas-docs/stable/whatsnew/v0.21.1.html#whatsnew-0211-converters


Thu 18-Apr-2019
^^^^^^^^^^^^^^^

See project journal.
(SalishSeaCast-FVCOM)

Worked on XIOS-2 and NEMO build issues on 16.04 salish:
* adding -D_GLIBCXX_USE_CXX11_ABI=0 to %BASE_CFLAGS in arch-GCC_SALISH.fcm as recommended in http://forge.ipsl.jussieu.fr/nemo/discussion/topic/28 gets farther; now the problem is that there is no netcdf.mod file
* looks like we need to update to libnetcdff6 and libnetcdff-dev which will move use from netcdf-4.1.3 to 4.4.3; opened ticket for Charles opinion, and he installed libnetcdff-dev-4.4.0 and libnetcdff-4.4.3
* successfully built XIOS-2
* successfully built NEMO SalishSeaCast_Blue config
* successfully run nowcast-dev/16apr19 and 17apr19
Continued migration to arbutus.cloud:
* started writing SalishSeaNowcast arbutus_cloud deployment docs
(SalishSea)

Publication party for Idalia's M.Sc. thesis.


Fri 19-Apr-2019
^^^^^^^^^^^^^^^

**Statutory Holiday** - Good Friday

Launched nowcast-dev/18apr19 and it finished in time for automation to handle nowcast-dev/19apr19.
(SalishSea)


Sat 20-Apr-2019
^^^^^^^^^^^^^^^

Easter Saturday

Hiking in Golden Ears park; Lower Fall and North Beach trails, and parts of West Canyon and Menzies trails.


Sat 21-Apr-2019
^^^^^^^^^^^^^^^

Easter Sunday

grib_to_netcdf failed before forecast2 runs due to a mount issue with /ocean:
* changed wgrib2 path in config to use executable that is committed in private-tools repo
* manually ran grib_to_netcdf forecast2 to backfill
* manually ran grib_to_netcdf nowcast+
* manually ran make_live_ocean_files to restart automation at ~11:30
(SalishSea)

See project journal.
(SalishSeaCast-FVCOM)

Walked along the False Creek Seawall to Columbia St, then to MEC, Dunbar & Bicicletta to look at bikes; Cannondale Topstone & MEC Provincial 222 ot Trail look promising.


Week 17
-------

Mon 22-Apr-2019
^^^^^^^^^^^^^^^

**Statutory Holiday** - Easter Monday

Continued migration to arbutus.cloud:
* continued writing SalishSeaNowcast arbutus_cloud deployment docs
* can't use 18.04 LTS minimal, have to use full to get NFS support
* had to mount export shared storage from /share instead of /export/MEOPAR because I couldn't get the export settings to work
* head node is working, but not snapshotted yet
* made v0 of compute node template
* accidentally detached west.cloud shared storage; got it back but then had a thrash mounting it on nowcast1; ended up doing the same as on arbutus.cloud, i.e. /share/
(SalishSea)


Tue 23-Apr-2019
^^^^^^^^^^^^^^^

Continued migration to arbutus.cloud:
* continued writing SalishSeaNowcast arbutus_cloud deployment docs; pushed WIP
* cloned repos into shares storage
* worked out loop commands to rename and mount shares storage on compute nodes
* started rsync of forcing dirs from west.cloud to arbutus.cloud:
  * GEM2.5
  * LiveOcean
  * rivers
  * sshNeahBay
* XIOS build
  * added -D_GLIBCXX_USE_CXX11_ABI=0 to %BASE_CFLAGS in arch-GCC_ARBUTUS.fcm as recommended in http://forge.ipsl.jussieu.fr/nemo/discussion/topic/28
  * installed svn
  * svn co http://forge.ipsl.jussieu.fr/ioserver/svn/XIOS/trunk XIOS-2-svn; got r1660 (same as on beluga)
  * added -std=c++11 to %BASE_CFLAGS in arch-GCC_ARBUTUS.fcm after an error message told me to
  * successful build
* NEMO build
  * hg up -r PROD-nowcast-green-201806
  * cp ARCH/UBC-EOAS/arch-GCC_SALISH.fcm ARCH/UBC-EOAS/arch-GCC_ARBUTUS.fcm
  scp lib_MPP.F90 from beluga into SalishSeaCast/MY_SRC/
  * SalishSeaCast_Blue built successfully
  * SalishSeaCast built successfully
* launched nowcast5 through 17 VMs
* discovered the / is almost full
* installed miniconda and created nowcast-env
SalishSeaCast mtg; see whiteboard.
(SalishSea)

See project journal.
(SalishSeaCast-FVCOM)


Wed 24-Apr-2019
^^^^^^^^^^^^^^^

Answered Rebecca's questions about M&D tax.

Continued migration to arbutus.cloud:
* updated repos to PROD-nowcast-green-201806:
  * grid
  * rivers-climatology
  * tides
  * tracers
* update SS-run-sets to 5090b620bf9c
*
(SalishSea)


Thu 25-Apr-2019
^^^^^^^^^^^^^^^

Got Mom's OAS tax amounts from Service Canada & sent themto Rebecca.

Continued migration to arbutus.cloud:
* Dug into openmpi errors more
* Venkat recommended spack:
  * git cloned it into /nemoShare/MEOPAR/nowcast-sys
  * copied config to .spack/config.yaml
  * edit config to use /mnt as temp storage
  * . spack/share/spack/setup-env.sh
  * spack bootstrap
  * . spack/share/spack/setup-env.sh
  * spack install openmpi@1.6.5
  * module avail/load etc to manage openmpi
* added XIOS-ARCH/COMPUTECANADA/arch-GCC_ARBUTUS.env to load openmpi, libiconv, numactl
* successfully built XIOS-2-svn r1660
* successfully built NEMO SalishSeaCast_Blue config
* got time steps w/ NEMO on big mem VM
* changed back to openmpi-2.1.2 and got time steps on big mem VM
* NEMO on small mem VMs goes very slow or freezes
* tried to shut down and restart all VMs and arbutus file system crashed
(SalishSea)


Fri 26-Apr-2019
^^^^^^^^^^^^^^^

Monthly project mtg.
(MIDOSS)

Continued setup on beluga:
* rsync-ed XIOS-2 (svn r1066) from niko to beluga as XIOS-2-hg because cloning times out
* deleted extern/, inputs/, src/, and tools/ dirs from XIOS-2-hg
* rsync-ed extern/, inputs/, src/, and tools/ dirs from XIOS-2 (svn r1660) into XIOS-2-hg
* copied bld.cfg and bld_dir.cdf from XIOS-2 to XIOS-2-hg
* discovered that build in XIOS-2-hg was going into XIOS-2
* Try again:
  * svn checkout XIOS-2-svn-pristine
  * rsync XIOS-2-hg-fresh
  * deleted extern/, inputs/, src/, and tools/ dirs from XIOS-2-hg-fresh
  * rsync-ed extern/, inputs/, src/, and tools/ dirs from XIOS-2 (svn r1660) into XIOS-2-hg-fresh
  * copied bld.cfg and make_xios into XIOS-2-hg-fresh
  * successful build
  * symlinked XIOS-2-hg-fresh as XIOS-2
  * built NEMO SalishSeaCast against new XIOS-2
  * submitted 21nov-11x33-xios-patch, and it worked
  * reconciled files in XIOS-2-hg-fresh and create $PROJECT/datorne/MEOPAR/xios-2-r1660.patch
  * rsync XIOS-2-hg from niko
  * apply patch
  * build failed
* Re-confirmed that XIOS-2-hg-fresh builds
* committed patch in XIOS-2-hg-fresh
* built successfully after commit
* cloned XIOS-2-hg-fresh to XIOS-2-hg locally on beluga
* built after clone
* Test on salish:
  * rsync clean clone of XIOS-2-hg-fresh to /data/dlatornel/MEOPAR/XIOS-2-hg
  * had to add -std=c++11 to %BASE_CFLAGS in arch-GCC_ARBUTUS.fcm after an error message told me to
  * successful build
* Test on graham:
  * rsync clean clone of XIOS-2-hg-fresh to /data/dlatornel/MEOPAR/XIOS-2-hg
  * had to add -std=c++11 to %BASE_CFLAGS in arch-X64_GRAHAM.fcm after an error message told me to
  * build timed out
(SalishSea)

Lunch w/ Al and Christina Spence.


Sat 27-Apr-2019
^^^^^^^^^^^^^^^

Vancouver to Parksville; very windy, but sunny, ride and ferry crossing due to passing front

Pushed XIOS-2 update to svn r1660 from beluga.
Added lib_mpp.F90 from svn r8537 to NEMO SalishSeaCast and pushed from beluga.
Added NEMO ARCH file for beluga, and pushed.
Pulled into XIOS-2 on graham, built successfully, pulled lib_mpp.F90 into NEMO-3.6.code, built successfully against XIOS-2.
21nov14_onehour test ran successfully.
(SalishSea)


Sun 28-Apr-2019
^^^^^^^^^^^^^^^

Worked with Susan to get hindcast automation transferred from cedar to optimum; need to refactor watch_NEMO_hindcast to work with qstat as well as squeue.
Resumed work on docs for beluga:
* updated hg docs re: glog alias
* added section to hg docs re: work-around for hg clone timeouts
Figured out mount options for nfsvers=4 on west.cloud: -t nfs -o proto=tcp:port=2049
(SalishSea)

Parksville to Vancouver


May
===

Week 18
-------

Mon 29-Apr-2019
^^^^^^^^^^^^^^^

Removed /share export on west.cloud to go back to /export/MEOPAR on nowcast1 now that I know how to make nfsvers=4 work; mounts on all compute VMs went stale; thrashed with Venkat on slack and eventually recovered by re-doing bind mount of /nemoShare/MEOPAR on /export/MEOPAR; run performance is still 25% of before I accidentally detached shared volume.
Finished docs for MOEPAR on beluga.
Continued migration to arbutus.cloud:
* set up 3 60g VMs, one as head, 2 as compute
* got time steps with nemo on nowcast0 and xios on nowcast1
* got time steps with xios on nowcast0 and nemo on nowcast1
* ran test on 3x7=20 cores for 411 time steps
* ran 4x8=28 cores to completion in 1h28m
* see slack for rest of scaling runs
(SalishSea)


Tue 30-Apr-2019
^^^^^^^^^^^^^^^

See project work journal.
(GOMSS)

Continued migration to arbutus.cloud:
* created new 15g compute node image (v1)
* see slack for scaling runs
SalishSeaCast mtg; see whiteboard.
(SalishSea)

Finalized M&D tax returns w/ Rebecca.

Telcon w/ Max about 43ravens intern possibility


Wed 1-May-2019
^^^^^^^^^^^^^^

Vancouver to New York

See project work journal.
(GOMSS)

Continued work on SalishSeaCmd segmented runs.
collect_weather 12 failed:
* ran download_weather 12 to restart automation
* ran download_weather 18 because it was partially downloaded by sarracenia, but collect_weather 18 wasn't running
* launched collect_weather 00
* accidentally deleted:
  * /results/forcing/atmospheric/GEM2.5/GRIB/20190105/12
  * /results/forcing/atmospheric/GEM2.5/GRIB/20190105/18
Continued migration to arbutus.cloud:
* see slack for scaling runs
(SalishSea)


Thu 2-May-2019
^^^^^^^^^^^^^^

New York

SSC recovery:
* launched nowcast-dev/01may19 via make_forcing_links --shared-storage
* launched nowcast-agrif/28apr19
* launched nowcast-agrif/29apr19
* launched nowcast-agrif/30apr19

* nowcast-agrif/01may19

* too fiddly to recover:
  * ww3 forecast 01may19
  * fvcom forecast 01may19
* Susan will backfill via hindcasting:
  * ww3 nowcast 01may19
  * ww3 nowcast 02may19
Continued work on SalishSeaCmd segmented runs.
Continued migration to arbutus.cloud:
* see slack for scaling runs
(SalishSea)


Fri 3-May-2019
^^^^^^^^^^^^^^

New York

SSC recovery (cont'd):
* launched nowcast-agrif/30apr19

* nowcast-agrif/01may19
Continued migration to arbutus.cloud:
* see slack for scaling runs
(SalishSea)


Sat 4-May-2019
^^^^^^^^^^^^^^

New York

SSC recovery (cont'd):
* launched nowcast-agrif/02may19
Continued migration to arbutus.cloud:
* see slack for scaling runs
(SalishSea)


Sun 5-May-2019
^^^^^^^^^^^^^^

New York to Brampton

See project journal.
(SalishSeaCast-FVCOM)

fvcom-nowcast-x2/05may19 failed because input.x2/ directory was empty; restarted automation manually via make_fvcom_boundary.
Tried to reset shared storage mounts on r12 VMs and discovered that there were orphan and zombie fvcom processes holding files open; killed them all, remounted shared storage, manually launched nowcast-r12/22apr19 and it compute time was normal.
Checked x2 VMs for same problem, but they were okay.
Check nemo VMs and found orphan and zombie wwatch3 processes; nowcast-green in progress immediately sped up when I started killing them.
SSC recovery (cont'd):
* launched nowcast-agrif/03may19
* launched nowcast-agrif/04may19
(SalishSea)


Week 19
-------

Mon 6-May-2019
^^^^^^^^^^^^^^

Brampton

SSC recovery (cont'd):
* launched nowcast-agrif/05may19
Investigated get_vfpa_hadcp failure; netcdf file for May is empty, which causes an error when trying to append data; deleted empty file and re-ran 2019-05-{01..05} manually.
Continued migration to arbutus.cloud:
* see slack for scaling runs; ran 9x19 on 111 cores (same as west.cloud production); 49m16s (compared to 27m16s on west.cloud)
* built wwatch3
* set up wwatch3-runs/ directory
* set up logs/nowcast directory
* successfully ran make_ww3_wind_file
* successfully ran make_ww3_current_file
* successfully ran scaling test runs for 05may19 on 44, 85, and 119 cores; 85 cores is same as west.cloud production, and has similar run time
Continued work on segmented runs.
ECCC reported problems that delayed 18Z forecast products until early Tue morning.
(SalishSea)


Tue 7-May-2019
^^^^^^^^^^^^^^

Brampton

Continued work on segmented runs; successfully queued 2 chained runs from a single YAML file on optimum; after a few bug fixes, they would run but for optimum's inability to run REBUILD_NEMO.
Backfilled fvcom-nowcast-r12 for 25 & 26 Apr.
(SalishSea)

See work journal.
(Resilient-C)


Wed 8-May-2019
^^^^^^^^^^^^^^

Brampton

Continued migration to arbutus.cloud:
* built fvcom
Backfilled fvcom-nowcast-r12 for 27 & 28 Apr.
Resumed work on rpn-to-gemlam.
(SalishSea)

Dinner w/ Linda & Steve.


Thu 9-May-2019
^^^^^^^^^^^^^^

Continued migration to arbutus.cloud:
* set up fvcom-runs/ directory
* make_fvcom_boundary failed on import of ttide module; compared git repo hash to west.cloud and found that arbutus is at 2c58c1f24, but west is at 4af96c4; checked out 4af96c4
* successfully ran make_fvcom_boundary 2019-04-22
* successfully ran make_fvcom_rivers_forcing 2019-04-22
* launched nowcast-x2/22apr19
* see slack for scaling tests details
* recommendation from arbutus  team via Venkat to use 60g flavours to force 1:1 vcpu:cpu mapping; replaced 15g nowcast5&6 w/ 60g instances
Continued work on rpn-to-gemlam.
forecast failed w/ high velocity errors on deep western boundary.
Backfilled fvcom-nowcast-r12 for 29 & 30 Apr.
(SalishSea)

Brampton to Vancouver


Fri 10-May-2019
^^^^^^^^^^^^^^^

Continued migration to arbutus.cloud:
* fvcom nowcast-x2/22apr19 on 7 cores on 4x15g VMs
* nowcast-blue/23apr19 on 41 cores on 6x60g VMs; 62m, so no improvement w/ 60g VMs
* Venkat confirmed w/ UVic that hyper-threading is indeed disabled on the hardware that our instances run on
* Venkat is working on creating a c16 flavor that will guarantee full node occupation
nowcast failed w/ same high velocity errors on deep western boundary as yesterday's forecast.
Continued work on rpn-to-gemlam; it now writes almost NEMO/FVCOM compatible hour forecast files; over to Susan.
Backfilled fvcom-nowcast-r12 for 1-May.
(SalishSea)


Sat 11-May-2019
^^^^^^^^^^^^^^^

Continued migration to arbutus.cloud:
* created fvcom0 15g instance to allow nowcast-r12 backfilling to run on arbutus
* added arbutus.cloug-prep to upload_forcing
* rsync-ed forcing up to date
* ran nowcast-green.201812/21mar19 from hindcast.201812/20mar19 to test XIOS on 60g nowcast0 instance
Discussed west boundary high velocity failures w/ Susan:
* she thinks that it is due to sea surface height discontinuity due to forcing shift from obs to fcst combined with seasonal large tidal currents occurring at day roll-over; she has a plan to produce a ssh forcing file that smooths the transition based on output of instantaneous ssh forcing values from NEMO at grid point near Neah Bay; she will manually construct the smoothed ssh forcing file for 10may19 so that we can test hypothesis when we backfill; didn't work - ended up re-running nowcast-green/09may19 with updated ssh forcing to get automation running again and backfilling started
Backfilled fvcom-nowcast-r12 on arbutus.cloud for 2 & 3 May.
(SalishSea)


Sun 12-May-2019
^^^^^^^^^^^^^^^

Created SalishSeaNowcast patches for ``--bind-to core`` and ``--mca btl ^openib`` for transition to arbutus.cloud.
Backfilled fvcom-nowcast-r12 on arbutus.cloud for 4 & 5 May.
(SalishSea)


Week 20
-------

Mon 13-May-2019
^^^^^^^^^^^^^^^

My back pranged out while I was in the shower :-( worked at home

Continued migration to arbutus.cloud:
* Venkat suggested file io test with dd if=/dev/zero of=testfile bs=1M oflag=direct; showed that arbutus is, if anything, slightly faster than west
Investigated IndexError and missing r12 lines in vhfr water level figures; cause is the use of the rolling forecast datasets as the source for NEMO results; i.e. can't backfill VHFR figures more than ~5d in the past.
Answered questions from Tereza re: deflation via ncks, and Rachael re: GUI merge tools on cedar.
Looked a building XIOS & NEMO on optimum against Loren Oh's GCC-8.3.0 netcdf/hdf5 libs, but don't have read access; sent email; Phil replied re: "offical builds":
  module load GCC/8.3
  module load OpenMPI/4.0.0/GCC/8.3
  module load ZLIB/1.2/11
  module load use.paustin
  module load HDF5/1.08/20
  module load NETCDF/4.6/1
XIOS on optimum builds, but finishes w/ warning:
 /usr/bin/ld: warning: libgfortran.so.3, needed by /usr/lib/../lib64/libnetcdff.so, may conflict with libgfortran.so.5
resolved by adding explicit -L directives to .fcm
Experimented with MEOPAR/ in $HOME on beluga to speed up deep dir traversals:
* mkdir $HOME/MEOPAR
* chgrp def-allen $HOME/MEOPAR
* chmod g+rwsx $HOME/MEOPAR
* clone repos
* stopped when I discovered that $PROJECT file system response has improved dramatically
Started work on refactoring watch_NEMO_hindcast to work with qstat as well as squeue; stopped when I got GCC-8.3.0 libs info from Phil
Backfilled fvcom-nowcast-r12 on arbutus.cloud for 6 & 7 May.
(SalishSea)

Updated Mercurial on kudu to Python 3 build of 5.0+5-ce5f1232631f:
* conda activate hg-dev-py3
* updated hg-dev-py3 env
* cd hg-stable
* hg pull
* hg update -r tip
* make clean all
* sudo make install PYTHON=/media/doug/warehouse/conda_envs/hg-dev-py3/bin/python3.7
It's noticibally slower than 2.7 version :-(
Enabled uncommit extension, and ui tweakdefaults.
hg commit -i fails with traceback; py3 issue?


Tue 14-May-2019
^^^^^^^^^^^^^^^

Back is more stiff than acutely sore; went to UBC.

Updated Mercurial on niko to 5.0+5-ce5f1232631f:
* conda activate hg-dev
* updated hg-dev env
* cd hg-stable
* hg pull
* hg update -r tip
* make clean all
* sudo make install PYTHON=/media/doug/warehouse/conda_envs/hg-dev/bin/python2.7
Enabled uncommit extension, and ui tweakdefaults.
hg commit -i works!

LiveOcean delayed; failed at ~12:05; re-launched for 2 more tries, then ran with 14may values persisted via symlink, starting daily runs at ~19:15.
Resumed experiments with MEOPAR/ in $HOME on beluga to speed up deep dir traversals because Tereza reported that beluga is still slow for her:
* mkdir $HOME/MEOPAR
* chgrp def-allen $HOME/MEOPAR
* chmod g+rwsx $HOME/MEOPAR
* clone repos
* time salishsea run 21nov14_oneday.yaml $SCRATCH/21nov14-home --debug
    real  2m37.135s
    user  0m2.322s
    sys 0m4.453s
  repeat took 7.72s
* time salishsea run 21nov14_oneday.yaml $SCRATCH/21nov14-project --debug
    real  8m33.917s
    user  0m1.452s
    sys 0m3.534s
  repeat took 8.26s
Tried experiments with MEOPAR/ in $HOME on cedar; clones worked, XIOS-2 build timed-out in 20 minute interactive session.
Resumed work on building XIOS & NEMO on optimum against GCC-8.3.0 netcdf/hdf5 libs:
  module load GCC/8.3
  module load OpenMPI/4.0.0/GCC/8.3
  module load ZLIB/1.2/11
  module load use.paustin
  module load HDF5/1.08/20
  module load NETCDF/4.6/1
NEMO on optimum builds, but finishes w/ warning:
 /usr/bin/ld: warning: libgfortran.so.3, needed by /home/Software/system/OpenMPI/4.0.0/lib/libmpi_usempi.so, may conflict with libgfortran.so.5
resolved by adding explicit -L directive to .fcm
Worked w/ Henryk to sort out a queuing issue; must include module loads in .bashrc
Queued job fails immediately; both nemo and xios executables segfault.
Backfilled fvcom-nowcast-r12 on arbutus.cloud for 8 & 9 May.
(SalishSea)


Wed 15-May-2019
^^^^^^^^^^^^^^^

Back was stiff, but not painful to walk; worked at home standing all day.

download_live_ocean backfill for 14may was still 404 at ~08:45 and ~12:30
download_live_ocean failed at 12:24; re-launched for another try, and emailed Parker; he fixed a netcdf4 issue in the low-pass file generation code; download_live_ocean succeeded at ~13:54.
nowcast-r12/10may19 failed to start due to in sufficient space for shared-memory backing file on nowcast11 (and maybe nowcast13); work-around:
* sudo mkdir -p /mnt/openmpi_tmp
* sudo chmod 777 /mnt/openmpi_tmp
* add --mca orte_tmpdir_base /mnt/openmpi_tmp to mpirun command
Discovered that nowcast-x2/14may19 failed silently
Backfilled fvcom-nowcast-r12 on arbutus.cloud for 10 & 11 May.
2nd Narrows HADCP observations file for May was corrupted; re-built from AIS files.
(SalishSea)

Re-built Mercurial w/ Python 2.7 because the speed hit of Python 3 was too much to take.

Upgraded kudu to Pop OS 19.04.

Haircut

Email convo w/ Rachael about mohid run tmp work dir lifespan.
(MIDOSS)

See work journal.
(Resilient-C)


Thu 16-May-2019
^^^^^^^^^^^^^^^

Back was improved; worked at home, sitting w/ 30 minute stretch breaks.

nowcast-x2 stumbled; re-launched manually
2nd Narrows HADCP observations file for May was corrupted again; suspect that is due to 2 instances for get_vfpa_hadcp running concurrently; re-built from AIS files.
Disabled r12 runs on west.cloud.
Added code to run_fvcom generated bash script to delete useless .fvcomtestfile and output/ directory, the latter should make run_fvcom idempotent.
Changed make_plots to store VHFR r12 and x2 figures separate so that the former for image loops don't overwrite the latter.
Backfilled fvcom-nowcast-r12 on arbutus.cloud for 12 & 13 May.
(SalishSea)

Helped Rachael add Markdown syntax to her MOHID error-log file.
(MIDOSS)

See work journal.
(Resilient-C)

See work journal.
(SalishSeaCast-FVCOM)


Fri 17-May-2019
^^^^^^^^^^^^^^^

Back regressed some, back to standing; was especially bad when I got up in the night, and I fainted.

Resumed experiments with MEOPAR/ in $HOME on cedar:
* XIOS-2 build on login node; took 489s
* NEMO SalishSeaCast build on login node; took 646s
* have to be on $SCRATCH or $PROJECT to use salishsea run
* time salishsea run $HOME/MEOPAR-home/SS-run-sets/v201812/hindcast/cedar-test/21nov14_oneday.yaml $SCRATCH/21nov14-home --debug
  real  3m44.110s
  user  0m2.125s
  sys 0m5.505s
  repeat took 3m13s
Continued migration to arbutus.cloud:
* new flavours: c16-60g, c16-120g, c8-120g
* deleted nowcast1 & nowcast2 (c8-60g)
* created new nowcast1 c16-120g compute node and snapshotted it as nowcast-c16-120g-compute-v0
* deleted nowcast3 & nowcast4 (c8-60g)
* launched new nowcast2 c16-120g from nowcast-c16-120g-compute-v0
* run nowcast-blue/xxx 4x9 on 30 cores w/ xios on nowcast0
* deleted nowcast5 & nowcast6 (c8-60g)
* created new head-build c16-120g head node and snapshotted it as nowcast-c16-120g-head-v0
Paired w/ Susan on rpn-to-gemlam.
Backfilled fvcom-nowcast-r12 on arbutus.cloud for 14 & 15 May.
(SalishSea)


Sat 18-May-2019
^^^^^^^^^^^^^^^

Back was stiff, right hip joint felt very constricted; worked standing all day; sat to watch movie in the evening.

Continued migration to arbutus.cloud:
* 4x9 decomp, 30 c16-120g VM cores, 2.5-2.5h/24h w/ 3 different values for orte_tmpdir_base
* messed around with network parameters tuning to no avail
Backfilled fvcom-nowcast-r12 on arbutus.cloud for 16 & 17 May.
(SalishSea)


Sun 19-May-2019
^^^^^^^^^^^^^^^

Back was stiff, but less restrictive of movement when I got up

Paired w/ Susan on rpn-to-gemlam.
Got NEMO built w/ GCC-4.4.7 and system netCDF/HDF5 libraries running again on optimum; put GCC-8.3 executables aside in $HOME for forensics.
Continued migration to arbutus.cloud:
* 7x9 decomp, 48 c8-15g VM cores, 75m/24h, ran to completion (compared to 51m on 30-Apr)
Backfilled fvcom-nowcast-r12 on west.cloud for 18 & 19 May.
(SalishSea)


Week 21
-------

Mon 20-May-2019
^^^^^^^^^^^^^^^

**Statutory Holiday** - Victoria Day

Back was still a little stiff, but better, except when I sat too long; no drugs; walked to Cambie St.

Wrote email to Javier re: NEMO fields for Atlantis model.
Figured out that rebuild_nemo on optimum was failing due to netCDF3/4 issues; came up with kludgy work-around of using rebuild_nemo built w/ GCC-8.3; need to add module loads to run_NEMO_hindcast-generated run script.
Paired w/ Susan on rpn-to-gemlam; it is production-ready!
fvcom-nowcast-r12/20may19 ran via automation!!
(SalishSea)


Tue 21-May-2019
^^^^^^^^^^^^^^^

**Statutory Holiday** - Victoria Day

Back was still a little stiff, but better, cycled to UBC until Red's threadbare rear tire punctured at the top of the hill, then walked from there; no drugs.

Spent some time reading Ansible docs.

Agreed to meet w/ Venkat ton Fri to pair on arbutus issues; installed his public key on nowcast0.
Wifi on niko doesn't connect in my EOAS office, but works in CompStaff office.
SalishSeaCast team mtg; welcomed May for the summer; see whiteboard.
Updated cedar hindcast-sys repos to PROD-hindcast_201812-v6:
  in each repo:
    hg pull
    hg update PROD-hindcast_201812-v6
  clean build of SalishSeaCast config
Updated optimum hindcast-sys repos to PROD-hindcast_201812-v6:
  in each repo:
    hg pull
    hg update PROD-hindcast_201812-v6
  clean build of SalishSeaCast config
(SalishSea)


Wed 22-May-2019
^^^^^^^^^^^^^^^

Back seems to be back to normal; stood for part of the day, then sat in the afternoon.

Caught up on Dad-work; arranged H&B Disher Courier pickup/delivery of his hearing aids.

Helped Susan w/ hindcast tests on optimum and nowcast-dev catch-up.
(SalishSea)

Updated process flow figure re: make_plots worker, web site, where processing happends, and colours for stages of processing.
(GoMSS_Nowcast)

See work journal.
(Resilient-C)


Thu 23-May-2019
^^^^^^^^^^^^^^^

Pulled salishsea_cmd/run.py WIP from niko backup drive:
* borg list to find archive date/time
* borg mount path::archive /mnt/borg-niko
* cp /mnt/borg-niko/...
* borg umount /mnt/borg-niko
Investigated why borg backups on salish stopped:
* scripts are in /etc/cron.daily/daily-*-backup.sh
* borg was not installed after upgrade to 16.04
Finalized loading of GCC-8.3 modules just before `salishssea combine` on optimum in `salishsea run` because rebuild_nemo on optimum is built with them, in contrast to XIOS and NEMO which are built with the system GCC-4.4.7; this was tested in the hindcast runs that Susan did on optimum yesterday.
(SalishSea)


Fri 24-May-2019
^^^^^^^^^^^^^^^

Monthly team mtg; see whiteboard.
(MIDOSS)

Debugged run_NEMO_hindcast targeting optimum; found that `salishsea run` is failing due to undefined PATH, FORCING, and PROJECT envvars; implemented a work-around.
Started work on enabling run_NEMO_hindcast to chain runs on torque systems as well as on slurm systems.
(SalishSea)


Sat 25-May-2019
^^^^^^^^^^^^^^^

Vancouver to Parksville in fairly epic North Shore rainfall

Finished enabling run_NEMO_hindcast to chain runs on torque systems as well as on slurm systems.
Built SKOG  on optimum after Susan patched namelist allocation issue that she previously patched in SalishSeaCast config.
Susan launched first test of segmented runs on optimum for Mar-Dec 2016 of SKOG; failed after 1st segment due to restart file names starting with SKOG, not SalishSeaCmd.
(SalishSea)


Sun 26-May-2019
^^^^^^^^^^^^^^^

Fixed bug in SalishSeaCmd segmented runs re: restart file names that don't start with SalishSea.
Susan launched continuation of segmented runs on optimum for Apr-Dec 2016 of SKOG; discovered possible mess mode of overwriting restart dir with results.
Started work on preventing SalishSeaCmd segmented runs feature from writing results of first segment to the same directory it restarted from; that is a possibility if a series of segmented runs are launched to continue after a failed segmented series.
(SalishSea)

Parksville to Vancouver


Week 22
-------

Mon 27-May-2019
^^^^^^^^^^^^^^^

Finished re-enabling packages in /etc/apt/sourcelist.d/ re: update to 19.04

More Gmail clean-up; inbox down to ~1630.

Started work on materials for MEOPAR ATM Mercurial session; ssh://hg@bitbucket.org/43ravens/meopar-atm-2019-06-11
(MEOPAR - 30min)

HRDPS 12 forecast was ~2h late; emailed Sandrine and she recommended switching to http://hpfx.collab.science.gc.ca/ although inspection shows that the files were delayed there too.
Finalized grid/weights-gem2.5-gemlam_201702.nc with CF-conventions metadata; deployed on optimum.
Emailed Steve@ONC re: recovery date for DDL node.
Discovered that ONC has a node in Burrard Inlet off Brockton Point.
Continued trying to prevent SalishSeaCmd segmented runs feature from writing results of first segment to the same directory it restarted from; that is a possibility if a series of segmented runs are launched to continue after a failed segmented series.
(SalishSea)

Phys Ocgy seminar by Ben M-M re: wind-driven upwelling in the SoG


Tue 28-May-2019
^^^^^^^^^^^^^^^

Steve@ONC replied that DDL node will likely be out of commission until mid-Sep;
Added Lu Guan (who has taken Akash's place) to the list of ONC contacts on the web site.
upload_forcing to cedar failed due to cedar down; re-ran manually at ~12:30
SalishSeaCast mtg; see whiteboard
(SalishSea)

Installed VSCode on niko via snap.

Continued work on materials for MEOPAR ATM Mercurial session.
(MEOPAR - 1h45m)


Wed 29-May-2019
^^^^^^^^^^^^^^^

Mtg w/ Venkat re: arbutus; new numa-enabled flavours w/ 30g root file system and no quota limits:
* killed nowcast14-17
* created nowcast3 from 18.04 image in new c16-60g-numa flavor; snapshot
* killed fvcom0 and nowcast11-13
* launched nowcast4 from c16-60g-numa snapshot
* created ArbutusCloudTests spreadsheet on Google Drive
* broke <51min on 5x16->59 cores
* got faster still on 73 and 90 cores
(SalishSea)

CMOS tour seminar on O2 in the ocean by Roberta Hamme.


Thu 30-May-2019
^^^^^^^^^^^^^^^

Continued migration to arbutus.cloud:
* replaced nowcast0 with a c16-60g-numa instance; thrashed getting shared storage re-mounted to compute nodes due to docs typo :-(
* big speed jump on 90 cores
* faster on 101 and 119 cores
* explored --bind-to and orte_tmpdir_base on 119 cores
* sent Venkat rationale for 17 c16-60g-numa instances and 1020g RAM for our tenant
(SalishSea)

Seminar on modeling rock weathering in the carbon cycle by Larry Mysak.

Continued work on materials for MEOPAR ATM Mercurial session.
(MEOPAR - 1h45m to 16:45)


Fri 31-May-2019
^^^^^^^^^^^^^^^

See work journal.
(Resilient-C)

Fixed off-by-1 bug in calc of no. of segment days at end of segmented run; deployed to optimum for Susan to test.
Continued migration to arbutus.cloud:
* wwatch3/nowcast/05may19 test and spreadsheet
* fvcom/nowcast-x2/22apr19 tests and spreadsheet
Reviewed MEOPAR ASM program.
(SalishSea)

Continued work on materials for MEOPAR ATM Mercurial session.
(MEOPAR - 2h15m to 18:00)


Sat 1-Jun-2019
^^^^^^^^^^^^^^

Continued migration to arbutus.cloud:
* more fvcom/nowcast-x2/22apr19 tests
(SalishSea)

Hiked Capilano River Trail & Coho Loop.


Sun 2-Jun-2019
^^^^^^^^^^^^^^

Continued migration to arbutus.cloud:
* more wwatch3/nowcast/05may19 tests; ~25% slower than yesterday
* NEMO nowcast-blue/23apr19 reproducibility test; within 15s of previous tests
Started running rpn-to-gemlam for 2013 in gemlam tmux session:
* immediately found missing hour; hacked code back to dev mode to store intermediate results in /data/dlatorne/tmp-rpn-to-gem-lam/ for Susan to work on.
* changed rpn_netcdf.sh to use /dev/shm when possible
* discovered that there are no /opp/GEMLAM/2013/ files prior to 16-Jul
Disabled processing of ONC CTD observations from DDL nodes pending repairs expected in mid-Sep.
Removed get_vfpa_hadcp worker launch from after_download_weather for 06 forecast because it should no longer be necessary to update figures to get all of UTC day observations now that nowcast-r12 finishes after the end  of the UTC day; need to commit after functional confirmation.
(SalishSea)

Continued work on materials for MEOPAR ATM Mercurial session.
Installed Ubuntu 18.04 in VM on kudu to get TortoiseHg
(MEOPAR - 30m to 13:00)


June
====

Week 23
-------

Mon 3-Jun-2019
^^^^^^^^^^^^^^

NEMO orientation w/ William Xu.
(Prediction Core)

Set up Ubuntu 18.04 VM w/ TortoiseHg on niko for MEOPAR ATM Mercurial session; had guest additions in dir beside ISO image of OS and didn't have to install it to get full screen.
(MEOPAR - 45m to 14:00)

Continued migration to arbutus.cloud:
* created c16-60g-nonuma compute and head instance images
* set up 6+1 no-numa instances and ran nowcast-blue/23apr19 test cast; ~45m
Susan started rsync-ing early 2013 GEMLAM files on to salish for external drive; started processing them through rpn-to-gemlam in tmux session.
(SalishSea)


Tue 4-Jun-2019
^^^^^^^^^^^^^^

Ran rpn-to-gemlam for feb-mar13.
Committed removal of get_vfpa_hadcp worker launch from after_download_weather for 06 forecast because it is no longer be necessary to update figures to get all of UTC day observations now that nowcast-r12 finishes after the end  of the UTC day.
nowcast delayed due to sarracenia client connection errors; ran download_weather 12 manually to start automation; killed collect_weather 12; launched collect_weather 18; watching sarracenia log
(SalishSea)

Mercurial in depth session w/ William.
(Prediction Core)

Walked home with Susan; dinner at Hitoe Sushi on 4th.


Wed 5-Jun-2019
^^^^^^^^^^^^^^

Sharcnet Julia Seminar:
* Edward Armstrong; C, Java, Jacvascript background
* high level, dynamic, mathematical, minimalistic core (mostly written in Julia)
* dev started in 2007, 1.0 in 2018, May-2019 1.2, 1.3 in Jul-2019
* MIT design
* hype
* juno plugin for Atom
* plugin for Jupyter
* PyCall pkg to call Python
* call C/Fortran natively
* compilable and JIT
* optional typing, multiple dispatch
* utf-8 support; greek characters in variable names
* variables:
  * a = 6
  * println(), show()
  * typeof()
  * parse(Int8, "18")
* types:
  * usual int & float
  * a = Int16(15)
  * int defaults to int16
  * 1-based indexing
  * strings are indexable
  * \-escaping in stings
  * python-like """ strings
  * "" for strings
  * '' for characters; a separate type
  * s[end] is s[-1] in Python
  * string() constructor for concatenation
  * * is string concat operator!  b = "red" * " " * b
  * string interpolation via $; like bash
  * regex: r"cd|de"
* "not an object oriented language"
* functions:
  * function f(value)
      return value=='g'
    end
  * last evaluation is returned by default
  * ordered args separated by comma
  * args... is unlimited collection of args assigned to args
  * kwargs are separated from args by ;
  * functions are first-class objects
  * anonymous functions:
    * c->c == 'b'
    * map(round, A)  # round used as anon
* flow control:
  * significant whitespace
  * block; end
  * if; then; elseif; else; end
  * blocks are leaky - don't have local scope
  * boolean ops; and &&, or ||
  * while; end
  * break, continue
  * for; end
  * for i = 1:2:10, j = 1:10 - instead of nexted
  * struct; end
* arrays:
  * []
  * mixed types results in type(Any)
  * Int8[] forces all Int8
  * [1 2 3; 4 5 6] is sugar for 2-row matrix
  * collect() makes array from range
  * undef keyword
  * reshape() and lots of other array functions
* convention: splice!(A, rnage); ! indicates that A will be changed, not required syntax, just convention

collect_weather 12 got stuck; another sarracenia client freak out?; ran download_weather 12 manually at ~~11:35 to start automation
download_results nowcast failed, probably due to files that Susan put in the dir with incorrect group.
Built SalishSeaCast on optimum for next section of 201812 hindcast.
Continued rpn-to-gemlam for apr-jun2013 and rsync-ing results to optimum.
Tried to run rpn-to-gemlam for jul-sep13, but it failed on 16sep13.
(SalishSea)

Continued work on materials for MEOPAR ATM Mercurial session.
(MEOPAR - 2h15m to 17:30)

Pulled Phil BB out of Gunnar and confirmed that drive side bearing is toast.
Started prepping Carib for Parksville/Victoria ride next week.


Thu 6-Jun-2019
^^^^^^^^^^^^^^

Ran rpn-to-gemlam for jul13 & aug13; found missing hour on 29aug13.
Ran make_runoff_file for 2013 and rsync-ing results to optimum; see slack #salishseacast for notes on merging data from /data/dlatorne/SOG-projects/SOG-forcing/ECget/Fraser_flow_2014-02-09.
Got 256 cores, 1000Gb RAM quota on arbutus; spun up FVCOM instances.
(SalishSea)

Worked w/ Susan, Ben Birgit & William on Dease Strait lake configuration.
(Prediction Core)


Fri 7-Jun-2019
^^^^^^^^^^^^^^

Sent NEMO-Cmd and SalishSeaCmd docs links to William.
(Prediction Core)

Called Phil Wood re: BB overhaul and followed up with email request to Mark@sales.
Finished prepping Carib for Parksville/Victoria ride.

Emailed Johannes re: migration to arbutus.cloud, suggesting that he download anything he needs from west.cloud before 14-Jun.
Isolated missing gemlam hour in 29aug13 in tmp-rpn-to-gem-lam/
Backfilled VHFR figures for 4-Jun.
(SalishSea)

Continued work on materials for MEOPAR ATM Mercurial session.
(MEOPAR - 2h15m to 17:30)

MOAD at the Gallery re: end of William's visit.


Sat 8-Jun-2019
^^^^^^^^^^^^^^

Vancouver to Parksville

Discussed w/ Susan interpolation of missing hours ≤4 in rpn-to-gemlam; started implementation.
(SalishSea)


Sun 9-Jun-2019
^^^^^^^^^^^^^^

download_weather 00 failed; recovery:
* kill collect_weather 00
* download_weather 00 at ~11:40
* download_weather 06 at ~11:52
* wait for forecast2 runs to complete
* download_weather 12
* collect_weather 18 failed; ran download_weather 18
* collect_weather 00 was never launched; need to run download_weather 00 tomorrow
(SalishSea)

Continued work on materials for MEOPAR ATM Mercurial session.
(MEOPAR - 2h to 11:30)

Udpated prod from 673:ae681cdc3b05 to 689:375ed4babcfa; reapplied lru cache disabling patch; restarted app; notified Ryan.
(Resilient-C)

Parksville to Chemainus


Week 24
-------

Mon 10-Jun-2019
^^^^^^^^^^^^^^^

Ran download_weather 00 to backfill.
download_live_ocean failed; Susan launched manually to start automation.
VHFR runs failed; discovered it was due to the model going unstable on 09jun19.
(SalishSea)

Continued work on materials for MEOPAR ATM Mercurial session.
(MEOPAR - 1h15m to 10:15)

Chemainus to Victoria


Tue 11-Jun-2019
^^^^^^^^^^^^^^^
MEOPAR ATM

Finished materials for MEOPAR ATM Mercurial session; presented it.
(MEOPAR - 5h to 16:30)


Wed 12-Jun-2019
^^^^^^^^^^^^^^^

download_weather 12 missed some files; re-ran manually and discovered that there are files missing from datamart; confirmed that files are missing from xxx too; emailed Sandrine; issue fixed; ran download_weather 12 at ~12:30 to start automation.
Emailed Michael and Maxim about VHFR 9jun19 aborts.
Replied to Johannes about migration to arbutus re: cronjobs.
Resumed work on migration to arbutus:
* mounted shared storage on fvcom instances
* ran nowcast-blue via run_NEMO
* ran vhfr nowcast-x2 via run_fvcom
* ran vhfr nowcast-r12 via run_fvcom
* couldn't run forecast due to request to mgr for nowcast run-info
* couldn't run nowcast-green due to:
    E R R O R :   misspelled variable in namelist nampissink in configuration namelist iostat = 5010
* hacked run_NEMO to enable forecast to be launched for present date when there is no run-info payload from mgr
* updated NEMO-3.6-code to PROD-nowcast-green-201806 branch
* clean built SalishSeaCast config
(SalishSea)

Telcon w/ Kate re: IPC to APC move by Horst.


Thu 13-Jun-2019
^^^^^^^^^^^^^^^

MEOPAR ASM


Got nowcast-green v201812 running on arbutus.cloud with Susan's help in setting up SS-run-sets/v201812/nowcast-green/ dir.
(SalishSea)


Fri 14-Jun-2019
^^^^^^^^^^^^^^^

MEOPAR ASM

Successfully completed manually managed functional test of arbutus.cloud ops; see Google Drive spreadsheet & #arbutus-into-herd channel.
(SalishSea)


Sat 15-Jun-2019
^^^^^^^^^^^^^^^

Hike to Cabin Point in East Sooke Regional Park lead by Kim of MEOPAR RMC and WWF.

Victoria to Vancouver


Sun 16-Jun-2019
^^^^^^^^^^^^^^^


Week 25
-------

Mon 17-Jun-2019
^^^^^^^^^^^^^^^


Tue 18-Jun-2019
^^^^^^^^^^^^^^^

Monthly mtg; see whiteboard.
(MIDOSS)

Added comparative analysis from 08jun19 on west.cloud to arbutus.cloud functional test on #arbutus-into-herd
Prep for flipping SalishSeaCast to arbutus.cloud tomorrow:
* rsync nowcast-blue/18jun19
* rsync forecast/18jun19
* create SS-run-sets/v201812/nowcast-blue/
* create SS-run-sets/v201812/forecast/
* create SS-run-sets/v201812/forecast2/
* rsync nowcast-green/18jun19
* rsync wwatch3 nowcast/18jun19
* rsync wwatch3 forecast/18jun19
* updated repos to PROD-hindcast_201812-v6:
  * grid
  * rivers-climatology
  * tides
  * tracers
* update config/nowcast.yaml
* update run_ww3
* update run_fvcom
* update run_NEMO
* pull SalishSeaNowcast to update arbutus.cloud
(SalishSea)


Wed 19-Jun-2019
^^^^^^^^^^^^^^^

Re-installed Rapid Photo Downloader v0.9.14 on kudu in virtualenv:
* Downloaded install.py from https://www.damonlynch.net/rapid/download.html to /home/doug/Pictures/RapidPhotoDownloader-0.9.14/
* python3  -m venv RapidPhotoDownloader
* source RapidPhotoDownloader/bin/activate
* python3 install.py --virtual-env
* installation failed on PyGObject, but I was able to recover with:
  * python3 -m pip install -U PyGObject
  * python3 install.py --virtual-env
* launch with /media/doug/warehouse/Pictures/RapidPhotoDownloader-0.9.14/RapidPhotoDownloader/bin/rapid-photo-downloader
Downloaded all images from OM-D card; imported them into Darktable; updated backup drive.

Mailed Gunnar BB to Phil Wood; tracking # LM119345536CA
MEC shopping & old tyres drop-off
Bathroom LEDs from Home Depot
Picked up Dyson AM09 from Canadian Tire

Flipped SalishSeaCast compute from west.cloud to arbutus.cloud after day's NEMO & wwatch3 runs completed on west.cloud:
* skookum:
  * local tag west.cloud-pre-migration in SalishSeaNowcast
  * update SalishSeaNowcast
  * clear_checklist
  * restart manager
  * restart log_aggregator
  * make_forcing_links arbutus nowcast+
* arbutus:
  * issue w/ namelist_light_blue symlink name
  * issue w/ file_def_blue.xml symlink name
  * issue w/ ssh keys for mpirun to use to connect to compute instances
  * run_NEMO worker wasn't getting any reply from manager
* skookum
  * reverted to west.cloud-pre-migration
  * edit checklist re: nowcast run date so that forecast2 works, I hope
  * restart manager
  * restart log_aggregator
(SalishSea)


Thu 20-Jun-2019
^^^^^^^^^^^^^^^

NEMO & wwatch3 runs are nominal on arbutus.
Susan is running hindcast.201812 to 20-Jun to provide restarts for officially changing production to 201812 tomorrow.
Finishing migration to arbutus.cloud:
* set up cron jobs to auto-clean old results
* committed arbutus arch files for NEMO & XIOS-2
VHFR FVCOM backfilling on west.cloud:
* nowcast-x2/18jun19 done
* nowcast-x2/19jun19 done
* nowcast-r12/18jun19 done
VHFR FVCOM backfilling on arbutus.cloud:
* nowcast-x2/20jun19 done
Figured out how to generate (365, 40, 898, 398) array populated w/ depth on axis 1 for Tereza using numpy methods instead of loop assignments.
Started working on Tereza's mocsy pipeline, but stalled on mocsy AttributeError.
(SalishSea)

Farewell party for Roger Beckie's headship.


Fri 21-Jun-2019
^^^^^^^^^^^^^^^

VHFR FVCOM backfilling on west.cloud:
* nowcast-r12/19jun19 done
* nowcast-r12/20jun19 running; eta 03:30
Investigated get_vfpa_hadcp failure; netcdf file for June is empty, which causes an error when trying to append data; deleted empty file and re-ran 2019-06-{01..21} manually.
rysnc-ed LiveOcean_v201905* (2013-2018) files to optimum.
rysnc-ed ssh_y* (2007 to 2019-06-20) files to optimum.
rysnc-ed riverTurbDaily201906* (2010 to 2019-06-15) files to optimum.
Copied Michael, Maxim & Johannes ssh keys from west.cloud to arbutus.cloud.
Brain-fart last night meant that vhfr nowcat-x2 didn't launch after nowcast-blue; used launch_remote_worker to start it.
Discovered that wwatch3/18jun19 files were not in the correct directory; recovery:
* make_ww3_wind_file forecast 2019-06-19 --debug
* make_ww3_current_file forecast 2019-06-19 --debug
* run_ww3 nowcast 2019-06-19 --debug
* make_ww3_wind_file forecast 2019-06-20 --debug
* make_ww3_current_file forecast 2019-06-20 --debug
* run_ww3 nowcast 2019-06-20 --debug
* make_ww3_wind_file forecast 2019-06-21 --debug
*  launch_remote_worker make_ww3_current_file forecast 2019-06-21
(SalishSea)

Emailed invoice 20190621-01 to Laura Avery re: MEOPAR ATM Mercurial workshop.
(MEOPAR)

Re-installed Rapid Photo Downloader v0.9.14 on niko in virtualenv:
* Downloaded install.py from https://www.damonlynch.net/rapid/download.html to /home/doug/Pictures/RapidPhotoDownloader-0.9.14/
* python3  -m venv RapidPhotoDownloader
* source RapidPhotoDownloader/bin/activate
* python3 install.py --virtual-env
* launch with /media/doug/warehouse/Pictures/RapidPhotoDownloader-0.9.14/RapidPhotoDownloader/bin/rapid-photo-downloader


Sat 22-Jun-2019
^^^^^^^^^^^^^^^

Vancouver to St John's
Dinner at Get Stuffed

VHFR FVCOM backfilling on west.cloud:
* nowcast-r12/21jun19 done
VHFR FVCOM backfilling on arbutus.cloud:
* nowcast-r12/22jun19 done
(SalishSea)


Sun 23-Jun-2019
^^^^^^^^^^^^^^^

St John's

Planned transition of hindcast.201812 into nowcast-green production w/ Susan; see #hindcast1812-nowcast channel.
First day of full automation on arbutus.cloud.
Started adding V18-12 datasets to ERDDAP:
* deleted inactive V17-02 dataset stanzas from datasets.xml:
  * ubcSSg3DuGridFields1hV17-02
  * ubcSSg3DvGridFields1hV17-02
  * ubcSSg3DwGridFields1hV17-02
  * ubcSSg3DTracerFields1hV17-02
  * ubcSSgSurfaceTracerFields1hV17-02
  * ubcSSfSurfaceTracerFields1hV17-02
  * ubcSSg3DBiologyFields1hV17-02
  * ubcSSgNearSurfaceUVelocity20mV17-02
  * ubcSSgNearSurfaceVVelocity20mV17-02
  * ubcSSfBoundaryBaySSH10mV17-02
  * ubcSSfCampbellRiverSSH10mV17-02
  * ubcSSfCherryPointSSH10mV17-02
  * ubcSSfFridayHarborSSH10mV17-02
  * ubcSSfHalfmoonBaySSH10mV17-02
  * ubcSSfNanaimoSSH10mV17-02
  * ubcSSfNeahBaySSH10mV17-02
  * ubcSSfNewWestminsterSSH10mV17-02
  * ubcSSfPatriciaBaySSH10mV17-02
  * ubcSSfPointAtkinsonSSH10mV17-02
  * ubcSSfPortRenfrewSSH10mV17-02
  * ubcSSfSandHeadsSSH10mV17-02
  * ubcSSfSandyCoveSSH10mV17-02
  * ubcSSfSquamishSSH10mV17-02
  * ubcSSfVictoriaSSH10mV17-02
  * ubcSSfWoodwardsLandingSSH10mV17-02
  * ubcSSf3DuGridFields1hV17-02
  * ubcSSf3DvGridFields1hV17-02
  * ubcSSfDepthAvgdCurrents1hV17-02
* updated ERDDAP index page re: change from V18-06 to V18-12
* copied setup.xml file into /opt/tomcat/content/erddap/ and bounced ERDDAP
* added ubcSSg3DBiologyFields1hV18-12 dataset
* emailed Emilio about change to V18-12
(SalishSea)

Walking in downtown St. John's on a very windy day.
Bought East Coast Trail Maps at Outfitters.
Lunch at Rocket Bakery.
Afternoon at The Rooms.
Dinner at Bannermans Brewery w/ dessrt at Coffee Matters.


Week 26
-------

Mon 24-Jun-2019
^^^^^^^^^^^^^^^

St. John's

Continued adding V18-12 datasets to ERDDAP:
* did a bunch of metadata correction and cleanup
* added ubcSSg3DTracerFields1hV18-12 dataset
(SalishSea)

Hike to Signal Hill via Battery St and North Head trail, then down via Lady's Lookout trail, Burma Rd, and Signal Hill Rd.
Lunch at Battery Café

Gunnar BB overhaul completed at Phil Woods.
Ordered new right hearing aid for Dad.


Tue 25-Jun-2019
^^^^^^^^^^^^^^^

St. John's to Port Kirwan


Wed 26-Jun-2019
^^^^^^^^^^^^^^^

Port Kirwan


Thu 27-Jun-2019
^^^^^^^^^^^^^^^

Port Kirwan


Fri 28-Jun-2019
^^^^^^^^^^^^^^^

Port Kirwan to Pouch Cove


Sat 29-Jun-2019
^^^^^^^^^^^^^^^

Pouch Cove


Sun 30-Jun-2019
^^^^^^^^^^^^^^^

Pouch Cove


July
====

Week 27
-------

Mon 1-Jul-2019
^^^^^^^^^^^^^^

Short walk on Pouch Cove to Cape St. Francis section to find pitcher plants; also saw minke whale.

Pouch Cove to St. John's


Tue 2-Jul-2019
^^^^^^^^^^^^^^

Changed ERDDAP forecast datasets to unversioned.
Big thrash re: ncks number of time steps in CHS_currents.nc file for forecast day; unresolved.
(SalishSea)


Wed 3-Jul-2019
^^^^^^^^^^^^^^


Thu 4-Jul-2019
^^^^^^^^^^^^^^

Visit to DFO Northwest Atlantic Fisheries Centre hosted by Nancy; Susan gave seminar on Olson, et al 2019; talked with Fraser and his software team re: Ocean Navigator.

Susan hindcast-201812 on optimum to backfill re: my mistake of running with the wrong tag in NEMO.
Finished implementation of watch_NEMO_hindcast qstat capability.
forecast-x2 stopped working for no apparent reason.
(SalishSea)


Fri 5-Jul-2019
^^^^^^^^^^^^^^

Rented truck, drove to Cape Spear, hiked south to North Head on bay that has Petty Harbour at its head.
Stopped at Blackhead village.
Walked to Fort Amherst lighthouse.


Sat 6-Jul-2019
^^^^^^^^^^^^^^

Walked North Head trail to Signal Hill, then down the hill to Bannerman's Brewing with Nancy, Will, and Carter.
Dinner at Granite where The Old Contemporaries were playing.

Updated optimum hindcast deployment to PROD-hindcast_201905-v1.
Susan started running 2013 as spin-up year of hindcast-201905.
Started working on unit tests for watch_NEMO_hindcast qstat capability.
(SalishSea)


Sun 7-Jul-2019
^^^^^^^^^^^^^^

Finished unit tests for watch_NEMO_hindcast qstat capability.
Deployed watch_NEMO_hindcast to skookum and started watching hindcast-201905 spin-up runs.
(SalishSea)

Taxi to MUN Ocean Research Centre at Logy Bay; walked ECT to Qidi Vidi, then back to Elizabeth Manor after a stop at the brewery tap room.


Week 28
-------

Mon 8-Jul-2019
^^^^^^^^^^^^^^

St. John's to Brampton

Worked on rpn-to-gemlam interpolation for ≤4 misssing hours.
(SalishSea)


Tue 9-Jul-2019
^^^^^^^^^^^^^^

Brampton

Discovered that nowcast-x2/07jul19 failed; started backfilling.
Discovered that forecast-x2 spontaneously started working again on 06jul19!
download_fvcom_results nowcast-r12/08jul19 didn't run; stuck watcher?; re-ran manually.
Finished rpn-to-gemlam interpolation for ≤4 misssing hours; tested on 29-31aug13; continued processing of sep13.
(SalishSea)


Wed 10-Jul-2019
^^^^^^^^^^^^^^^

Brampton

Committed and deployed rpn-to-gemlam interpolation for ≤4 misssing hours; continued processing of oct-nov13.
nowcast-x2/08jul19 got stomped on by 09jul19 launched by automation so both failed; backfilling 08jul19
download_fvcom_results nowcast-r12/09jul19 didn't run; don't know why; re-ran manually.
Helped Susan get hindcast-201905 sorted out on optimum; her SalishSeaNEMO_finish.sh script was the cause of $HOME directory getting moved into results dir; fortunately today it only moved part of .conda/ unlike last time when it moved everything and killed access due to missing .ssh/authorized_keys file.
backfilled nowcast-x2/09jul19
hindcast-201905/11mar19 and 21mar19 ran
watch_NEMO_hindcast tried to watch completed job on optimum; modified it to ignore completed jobs in qstat output.
got watcher running again against hindcast-201905/01apr19 and queued 11apr19
(SalishSea)


Thu 11-Jul-2019
^^^^^^^^^^^^^^^

Brampton

Continued rpn-to-gemlam processing of dec13-feb14.
backfilled nowcast-x2/10jul19
hindcast-201905 automation worked fine for flow from 01apr19 to 11apr19 and then to 21apr19, and onward.
Committed fix for bug in SalishSeaCmd restart dirs calculation for segmented runs that Susan identified weeks ago, including unit test.
Resumed work on SalishSeaCmd segmented runs docs.
(SalishSea)


Fri 12-Jul-2019
^^^^^^^^^^^^^^^

Brampton to Vancouver

Spasm in middle right back started at YYZ and didn't get any better on flight, very painful by the time I got home.

Continued rpn-to-gemlam processing of mar-may14.
Resumed work on SalishSeaCmd segmented runs docs.
(SalishSea)


Sat 13-Jul-2019
^^^^^^^^^^^^^^^

Continued rpn-to-gemlam processing of jun-jul14.
Refactored make_plots to make INFO level logging less noisy.
Changed paramiko and matplotlib logging thresholds to WARNING to reduce INFO level noise.
(SalishSea)


Sun 14-Jul-2019
^^^^^^^^^^^^^^^

Refactored make_surface_current_tiles to make INFO level logging less noisy.
(SalishSea)




>10-May-2019:
* talk to Charles about borg on salish (re-install?)
* recover from borg:
  * /results/forcing/atmospheric/GEM2.5/GRIB/20190105/12
  * /results/forcing/atmospheric/GEM2.5/GRIB/20190105/18
* get daily borg restarted


Week 29
-------

Mon 15-Jul-2019
^^^^^^^^^^^^^^^

Worked on Dad's 2018 CRA medical expenses review w/ Rebecca; emailed Dr. Shilash to request letter supporting care needs.

Received payment of invoice 20190621-01 re: MEOPAR ATM Mercurial workshop.

HRDPS 12/048 files were >2h late; appeared almost immediately after I emailed Sandrine.
Continued work on SalishSeaCmd segmented runs docs.
Started work on creating updated nowcast-env conda env on skookum by creating nowcast-env-15jun19 from environment-prod.yaml; confirmed that YAML warnings from dask are gone with make_plots.
Confirmed that Sentry Shoal wave buoy data has been unavailable since 29-Jun; need to fix wave_height_period figure module to handle missing obs; also 2 other FutureWarnings:
  * /SalishSeaCast/moad_tools/moad_tools/observations.py:83: FutureWarning: read_table is deprecated, use read_csv instead, passing sep='\t'.
    date_parser=datetime_parser,
  * /SalishSeaCast/nowcast-env-15jul19/lib/python3.7/site-packages/pandas/plotting/_converter.py:129: FutureWarning: Using an implicitly registered datetime converter for a matplotlib plotting method. The converter was registered by pandas on import. Future versions of pandas will require you to explicitly register matplotlib converters.

  To register the converters:
    >>> from pandas.plotting import register_matplotlib_converters
    >>> register_matplotlib_converters()
    warnings.warn(msg, FutureWarning)
(SalishSea)

Read an commented on Rachel's version tracking documents and protocol proposal.
(MIDOSS)


Tue 16-Jul-2019
^^^^^^^^^^^^^^^

Monthly project mtg.
Met w/ Rachael & Shihan re: repo tagging, milestone documentation, etc.
Set up MIDOSS slack workspace with #soiled channel, subscribed it to Bitbucket repos and Compute Canada status feed.
(MIDOSS)

SalishSeaCast team mtg.
Exercised external archive drive #2.
Worked on handling missing wave buoy obs in wave_height_period figure module; fix doesn't cover all the bases due to confusing nowcast-fig-dev envs on niko.
Tried to update niko conda and base env got corrupted; re-installed miniconda3 from download.
Built new nowcast-fig-dev env.
Neither jupyter lab nor notebook work in new env; downgraded jupyterlab from 1.0.2 to 0.35.6; that forced tornado to update from 4.5.3 to 6.0.3, and lab worked; updated lab again to 1.0.2 and it started working there too; so circus and its out of date tornado and pyzmq dependencies are the problem, I think.
(SalishSea)


Wed 17-Jul-2019
^^^^^^^^^^^^^^^

Worked on setting up new nowcast-env on skookum:
* confirmed circus deps restrictions and no movement to resolving them:
  * tornado<5.0,>=3.0
  * pyzmq<17.0,>=13.1.0
* those restrictions limit conda to Python 3.6
* explored https://pypi.org/project/python-daemon/ but realized that it is just a daemon-izer, not a process manager (with e.g. monitoring and restart)
* explored http://supervisord.org/; Python≥3.4; sole dep is meld3 templating lib from supervisor project that has no deps; available on conda-forge
* updated conda env descriptions w/ python=3.6 and circus=0.15 to ensure consistency
Installed new salishsea-nowcast dev env on kudu.
Installed new nowcast-env prod env on skookum.
(SalishSea)

Physio appt w/ Ehren; diagnosed mid-back issue as slightly dislocated ribs.


Thu 18-Jul-2019
^^^^^^^^^^^^^^^

Continued struggle to tame Gmail inbox.

Installed new salishsea-nowcast dev env on niko.
Started to look at rpn-to-gemlam for 2007; need to enable processing of 12Z forecast files.
Exercised external archive drive #4; had to fix superblock with fsck due to improper previous umount.
Fixed wwatch3 Sentry Shoal missing obs figure issue for real.
Started work on fixing figures re: pandas FutureWarning: Using an implicitly registered datetime converter (issue#69):
* wave_height_period - done
* compare_tide_prediction_max_ssh - done
Also encountered pandas/xarray FutureWarning: Converting timezone-aware DatetimeArray to timezone-naive ndarray with 'datetime64[ns]' dtype.
(SalishSea)

ATSC seminary by Amanda Giang on atmospheric pollution policy modeling


Fri 19-Jul-2019
^^^^^^^^^^^^^^^

Pinged Henryk on slack re: uneven hindcast execution rate; he gave me access to optimum node metrics web app.
(SalishSea)

Upgraded niko to 16Gb RAM.

Installed overhauled bottom bracket in Gunnar & prepped it for ride to Parksville.


Sat 20-Jul-2019
^^^^^^^^^^^^^^^

Vancouver to Parksville
Met Keith & Trish at Horseshoe Bay; invited them for dinner at Saturna Dr.


Sun 21-Jul-2019
^^^^^^^^^^^^^^^

Worked on adding forecast hour to rpn-to-gemlam; test for 2007-01-03 failed, but not sure why.
collect_weather 00 failed; manually ran download_weather 00, 06, 12, and 18 over the course of the day to get automation back on track.
(SalishSea)

Parksville to Vancouver


Week 30
-------

Mon 22-Jul-2019
^^^^^^^^^^^^^^^

Finished expense claim for MEOPAR ATM.

See new 2019 project work log.
(Resilient-C)

Exercised external archive drive #6.
cedar came back online; tried to backfill upload_forcing for 15-21: nowcast+ & turbidity; disk quota exceeded.
Started work on changing SalishSeaNowcast to use supervisor instead of circus.
(SalishSea)


Tue 23-Jul-2019
^^^^^^^^^^^^^^^

Continued work on changing SalishSeaNowcast to use supervisor instead of circus.
SalishSeaCast team mtg; see whiteboard.
Continued work on fixing figures re: pandas FutureWarning: Using an implicitly registered datetime converter (issue#69):
* wwatch3.wave_height_period - done
* publish.compare_tide_prediction_max_ssh - done
* fvcom.publish.tide_stn_water_level
* fvcom.publish.second_narrows_current
* comparison.sandheads_winds
* research.tracer_thalweg_and_surface
* research.velocity_section_and_surface
Built new nowcast-env on skookum with supervisor instead of circus.
Exercised external archive drive #8.
Started work on changing salishsea-site to use supervisor instead of circus.
(SalishSea)


Wed 24-Jul-2019
^^^^^^^^^^^^^^^

Updated Mercurial on kudu to 5.1rc0+6-ce52377102db:
* conda activate hg-dev
* updated hg-dev env
* cd hg-stable
* hg pull
* hg update -r tip
* make clean all
* sudo make install PYTHON=/media/doug/warehouse/conda_envs/hg-dev/bin/python2.7

backfilled cedar upload_forcing for 15-21 & 23: nowcast+ & turbidity
(SalishSea)

See new 2019 project work log.
(Resilient-C)


Thu 25-Jul-2019
^^^^^^^^^^^^^^^

Researched bikes, especially comparing frame geometries to Gunnar.
Test rode Kona Rove NRB DL and Libre DL.


Fri 26-Jul-2019
^^^^^^^^^^^^^^^

Helped Ben apply patch to ariane so that it can build against libnetcdf.so instead of libnetcdf.a.
Finished changing salishsea-site to use supervisor instead of circus.
Worked on SalishSeaNowcast docs re: change to supervisor.
(SalishSea)

Updated Mercurial on niko to 5.1rc0+12-7fae3b0bd893:
* conda activate hg-dev
* updated hg-dev env
* cd hg-stable
* hg pull
* hg update -r tip
* make clean all
* sudo make install PYTHON=/media/doug/warehouse/conda_envs/hg-dev/bin/python2.7


Sat 27-Jul-2019
^^^^^^^^^^^^^^^

Bike shopping; test rode Cannondale Synpase, Trek Checkpoint, and Cannondale Topstone; bought Topstone.


Sun 28-Jul-2019
^^^^^^^^^^^^^^^

Explored hindcast performance issues on optimum:
* confirmed Henryk's report that XIOS and all NEMO processes are using 3 threads each; compared to arbutus where they only use 1 each
* confirmed that arbutus is using OpenMPI-2.1.1, compared to
(SalishSea)

Picked up Tina from Mighty, and Topstones from BSP; installed computer, mirror, etc. on Susan's Topstone.


Week 31
-------

Mon 29-Jul-2019
^^^^^^^^^^^^^^^

Removed Miniconda/3 module load from run bash scripts generated for optimum.
Corrected SalishSeaCmd version to 19.2.dev0.
Built XIOS-2 and NEMO/SalishSeaCast on optimum with OpenMPI-2.1.6; got messages at end of NEMO build:
  /usr/bin/ld: skipping incompatible /usr/lib/libm.so when searching for -lm
  /usr/bin/ld: skipping incompatible /usr/lib/libpthread.so when searching for -lpthread
  /usr/bin/ld: skipping incompatible /usr/lib/libc.so when searching for -lc
don't recall if they appeared at end of XIOS-2 build.
Continued updating SalishSeaNowcast docs re: change to supervisor, move to arbutus, etc.
Continued work on fixing figures re: pandas FutureWarning: Using an implicitly registered datetime converter (issue#69).
ocean mount went unavailable in the later afternoon.
(SalishSea)

Installed computer & mirror on my Topstone.


Tue 30-Jul-2019
^^^^^^^^^^^^^^^

Email reply to Mike@Bedford re: GoMSS offline since 21-Jul power outage.

Commute took just over 29min for the first time in ages :-)

upload_forcing orcinus nowcast+ failed; re-ran manually.
Reviewed storage: 1.6T free on /results2; nowcast-green.201806/ needs to be archived.
Reviewed and analyzed ComputeCanada ssh keys changes for group.
SalishSeaCast team mtg; see whiteboard.
Released SalishSeaNowcast-19.1.
Cloned Elise's tuningRunsArchive; 761 files took >20 minutes.
Investigated get_vfpa_hadcp AttributeError issue and found that csv files contain data from Port aux Basque since sometime on 24Jul; emailed Michael & Maxim.
Discussed deletion of files from nowcast-green.201806 w/ Susan.
Continued work on fixing figures re: pandas FutureWarning: Using an implicitly registered datetime converter (issue#69); added warning suppression to test notebooks re: arrow.get() parser ch
anges coming in v0.15.0
(SalishSea)


Wed 31-Jul-2019
^^^^^^^^^^^^^^^

Cycled a 25 km loop to UBC, then through Pacific Spirit, to Kerrisdale, and home on the Arbutus greenway.

Telcon w/ Kate.

Pulled NEMO-3.6-code on optimum to 1656:ea9eba6f8a91 and did a clean build of SalishSeaCast.
Pulled and rebased SS-run-sets on optimum to 2467:b62960a6d316.
Reverted rpn-to-gemlam forecast arg changes on salish and re-tried 2012-11-11 to 201-11-12 to confirm whether issue is really >4hr interpolation, or a new bug; it's a new bug; ran 2012-11-01 to 201-11-10
Updated SalishSeaNowcast and salishsea-site dev envs on kudu.
(SalishSea)


Thu 1-Aug-2019
^^^^^^^^^^^^^^

Ordered Alex Boondocks 650b wheels & RT56 brake rotors to test on Topstones.

See new 2019 project work log.
(Resilient-C)

Started experiment to move salishsea-site from pyramid-crow and raven to sentry-sdk.
Continued email thread re: 2nd Narrows HADCP w/ ONC people; got some observations early this morning, but no files since 08:03.
rpn-to-gemlam 2012-11-13 2012-11-30 completed
(SalishSea)


Fri 2-Aug-2019
^^^^^^^^^^^^^^

See new 2019 project work log.
(Resilient-C)

rpn-to-gemlam 2012-10-01 2012-10-31 failed due to file issue
Deleted unneeded files from /results2/SalishSea/nowcast-green.201806/ to free ~1.3Tb:
* find /results2/SalishSea/nowcast-green.201806/ -name "SalishSea_1?_*_dia?_?.nc" -delete
* find /results2/SalishSea/nowcast-green.201806/ -name "SalishSea_1h_*_VT?.nc" -delete
* find /results2/SalishSea/nowcast-green.201806/ -name "SalishSea_1h_*_prod_T.nc" -delete
Ran make_runoff_file for 10Aug12 to 31Dec12 and rsynced to optimum
Hacked up a Sphinx site demo from Elise's tuningrunarchive repo and asked for her feedback on it.
Closed issue #69 re: figure modules re: pandas FutureWarning: Using an implicitly registered datetime converter.
Merged a bunch of Fraser river daily avg discharge files into /data/dlatorne/SOG-projects/SOG-forcing/ECget/Fraser_flow, then ran make_runoff_file for finish 2007-2012; rsynced files top optimum.
Fixed bug in SalishSeaCmd unearthed by William@UCalgary re: checking default waitjob value; result of bug was jobs not being queued on beluga/cedar/graham, and being queued but held on optimum.
(SalishSea)

Canyons/Arctic; see whiteboard.
(Canyons/Arctic)

Discovered that proj4-fortran is now available on beluga, so building MOHID there should be the same as building it on cedar; started the process.
(MIDOSS)


Sat 3-Aug-2019
^^^^^^^^^^^^^^

Prep for Friday Harbor trip.


Sun 4-Aug-2019
^^^^^^^^^^^^^^

Vancouver to Friday Harbor; cycled to Tsawwassen via Alex Fraser Bridge, ferry to Swartz Bay, cycled to Sidney; ferry to Friday Harbor, cycled to lab


August
======

Week 32
-------

Mon 5-Aug-2019
^^^^^^^^^^^^^^

**Statutory Holiday** - BC Day

Friday Harbor

Refactored run_NEMO_hindcast to default to 5d runs insted of 10d to try to get more efficient operations on optimum.
nowcast-blue got stuck on launch; killed, cleaned up, and re-launched manually via make_forcing_links.
Added code to run_NEMO_hindcast to avoid logging errors for "qstat: Unknown Job Id" at end of hindcast runs when job has disappeared from qstat's awareness.
Discussed Python packaging re: LiveOcean w/ Parker.
Discovered that wwatch3 has not run properly since 01aug19; made worse by the fact that the run date is not propagated among the ww3 workers; backfilling:
* make_ww3_wind_file --debug forecast 2019-08-01
* make_ww3_current_file --debug forecast 2019-08-01
* run_ww3 nowcast 2019-08-01
* make_ww3_wind_file --debug forecast 2019-08-02
* make_ww3_current_file --debug forecast 2019-08-02
* run_ww3 nowcast 2019-08-02
Added run date propagation from make_ww3_current_file to run_ww3
* make_ww3_wind_file --debug forecast 2019-08-03
* make_ww3_current_file --debug forecast 2019-08-03
* make_ww3_wind_file --debug forecast 2019-08-04
* make_ww3_current_file --debug forecast 2019-08-04
* make_ww3_wind_file --debug forecast 2019-08-05
* make_ww3_current_file --debug forecast 2019-08-05
Investigated why observations have disappeared from sandheads_winds figure; after way to much digging in the weeds, discovered that ECCC have recorded no observations from Sandheads since 20Jul :-(
(SalishSea)


Tue 6-Aug-2019
^^^^^^^^^^^^^^

Friday Harbor
Attended Susan's lecture on spring bloom modeling.

Replied to William's email suggesting that he roll back to XIOS-2 r1066 on cedar.
(Prediction Core)


Wed 7-Aug-2019
^^^^^^^^^^^^^^

Friday Harbor
Attended Susan's lecture on canyons.

Re-read blog posts by Henyk and others about using src/ directory in Python packages.
Also learned about how much of setup.py can be made declarative in setup.cfg.
Figures out how I can make definition of package version in __init__.py the single definition.
Tested above ideas in restructured rpn-to-gemlam package.

Debugged foreacst hour issue in rpn-to-gemlam and started processing 2007 files.
(SalishSea)


Thu 8-Aug-2019
^^^^^^^^^^^^^^

Friday Harbor

More research on packaging; tested flit and pyproject.toml but that doesn't support pip install -e; decided against src/-layout for now pending developments by PyPA and flit.

gemlam failed on 14jan07 due to solar radiation missing from hourly file:
  * hour 005 is missing FB variable
  * tried to restart processing on 16jan07; found that 14jan07 hour 012 is also missing FB
  * tried to restart processing on 17jan07;
Changed rpn-to-gemlam to use setup.cfg for package configuration, __version__ in __init__.py for version identifier, and env/ directory for environment description files.
Susan filled /results with hindcast spin-up results; then did some cleanup to get things back in business.
(SalishSea)

Started writing Python packaging section in ubc-moad-docs.
(MOAD)


Fri 9-Aug-2019
^^^^^^^^^^^^^^

Friday Harbor to Chemainus

collect_weather 18 failed yesterday due to full /results; recovery (all --debug):
* download_weather 18
* download_weather 00
* download_weather 06
* collect_river_data Capilano 2019-08-08
* collect_river_data ChilliwackVedder 2019-08-08
* collect_river_data ClowhomClowhomLake 2019-08-08
* collect_river_data Englishman 2019-08-08
* collect_river_data Fraser 2019-08-08
* collect_river_data HomathkoMouth 2019-08-08
* collect_river_data SalmonSayward 2019-08-08
* collect_river_data SanJuanPortRenfrew 2019-08-08
* collect_river_data SquamishBrackendale 2019-08-08
* collect_river_data TheodosiaScotty 2019-08-08
* collect_river_data TheodosiaBypass 2019-08-08
* collect_river_data TheodosiaBypass 2019-08-08
* make_runoff_file
* get_NeahBay_ssh forecast2
* grib_to_netcdf forecast2
* get_onc_ctd SCVIP
* get_onc_ctd SEVIP
* get_onc_ferry TWDP
* upload_forcing arbutus.cloud-nowcast forecast2 --debug
Warnings:
* 2019-08-09 08:07:37,680 DEBUG [get_NeahBay_ssh] observations & predictions table saved to /results/forcing/sshNeahBay/txt/sshNB_2019-08-09_15.txt
/SalishSeaCast/SalishSeaNowcast/nowcast/residuals.py:767: FutureWarning: `item` has been deprecated and will be removed in a future version
  tide = ttide.pred_all[ttide.time == d].item()
(SalishSea)


Sat 10-Aug-2019
^^^^^^^^^^^^^^^

Chemainus to Parksville


Sun 11-Aug-2019
^^^^^^^^^^^^^^^

Parksville


Week 33
-------

Mon 12-Aug-2019
^^^^^^^^^^^^^^^

Continued writing Python packaging section in ubc-moad-docs.
(MOAD)

Worked with Susan on our application for the sockeye.arc.ubc.ca beta.
(SalishSea)

Parksville to Vancouver


Tue 13-Aug-2019
^^^^^^^^^^^^^^^

download_live_ocean timed out in automation; re-launched manually; success at 16:27.
Helped Susan finalize our application for the sockeye.arc.ubc.ca beta.
SalishSeaCast team mtg; see whiteboard.
Confirmed that Sand Heads and Sentry Shoal obs are still offline, and that Halibut Bank has decreased from 45d to 24h.
Confirmed that orcinus returned to service at ~13:30 on 12-Aug after a weekend power outage: backfilled:
* upload_forcing nowcast+ 2019-08-{09..12} --debug
* upload_forcing turbidity 2019-08-{09..12} --debug
* make_forcing_links nowcast-agrif 2019-08-10
* make_forcing_links nowcast-agrif 2019-08-11
* make_forcing_links nowcast-agrif 2019-08-12
(SalishSea)


Wed 14-Aug-2019
^^^^^^^^^^^^^^^

Finished backfilling nowcast-agrif:
* make_forcing_links nowcast-agrif 2019-08-13
(SalishSea)

Dentist appt.

Built 650B wheels for Tommy Topstone; Alex Boondocks 3 wheelset, Shimano RT56 rotors, Conti tubes, René Herse Loup Loup 38mm tires.


Thu 15-Aug-2019
^^^^^^^^^^^^^^^

Signed forms for Dad's IPC to TD xfer; dropped them off at TD.

upload_forcing to orcinus failing again, but ssh is okay...
Renamed sada-network slack workspace to salishseacast; created new sada-network workspace; exported old sada; imported #random & #world-domination from export; deleted old #world-domination and #random; re-created empty #random in SalishSeaCast workspace; added pinned explanation of bot channels to #general in SalishSeaCast; disconnected Bitbucket from #midoss-repos channel and archived it.
Susan got confirmation from ECCC that Sentry Shoal buoy has a hardware failure.
Discovered that wwatch3 nowcast has been failing since 12aug19 due to stuck make_ww3_wind_file; backfilling:
* make_ww3_wind_file forecast 2019-08-12
* make_ww3_current_file forecast 2019-08-12
* make_ww3_wind_file forecast 2019-08-13
* make_ww3_current_file forecast 2019-08-13
* make_ww3_wind_file forecast 2019-08-14
* make_ww3_current_file forecast 2019-08-14
Added code to wave_height_period fig module to handle 404 error from buoy data service; there is still an Error level exception that bubbles up  from moad_tools.observations.get_ndbc_buoy()
(SalishSea)

Invited Vicky to slack workspace.
(MIDOSS)


Fri 16-Aug-2019
^^^^^^^^^^^^^^^

Finished backfilling wwatch3:
* make_ww3_wind_file forecast 2019-08-15
* make_ww3_current_file forecast 2019-08-15
(SalishSea)

Updated Mercurial on kudu to 5.1+12-f59f8a5e9096:
* conda activate hg-dev
* updated hg-dev env
* cd hg-stable
* hg pull
* hg update -r tip
* make clean all
* sudo make install PYTHON=/media/doug/warehouse/conda_envs/hg-dev/bin/python2.7

See work journal.
(Resilient-C)


Sat 17-Aug-2019
^^^^^^^^^^^^^^^

Vancouver to Bowen Island


Sun 18-Aug-2019
^^^^^^^^^^^^^^^

Bowen Island

Deleted spinup.201812/, forecast.201806/, forecast2.201806/ & nowcast-blue.201806 from /results/SalishSea/ to free up space for hindcast.201905 spinup files.
(SalishSea)

Continued writing Python packaging section in ubc-moad-docs.
(MOAD)


Week 34
-------

Mon 19-Aug-2019
^^^^^^^^^^^^^^^

Bowen Island

Finished writing Python packaging section in ubc-moad-docs.
(MOAD)

Resumed work on 2007 GEMLAM processing; worked on flagging missing RPN variables (i.e. FB == solar radiation); started work on interpolation code to fill them in.
(SalishSea)


Tue 20-Aug-2019
^^^^^^^^^^^^^^^

Bowen Island

Bitbucket announced sunsetting of their support for Mercurial.
Tried to create WorkJournal git repo on Bitbucket and can't because an hg repo of that name exists; so all repos will have to got through a name change if we convert to git on Bitbucket.

Monthly team mtg; see whiteboard.
(MIDOSS)

Continued work on 2007 GEMLAM processing; worked on flagging missing RPN variables (i.e. FB == solar radiation); finished work on interpolation code to fill them in; started testing it on salish.
Got access to sockeye for beta testing.
(SalishSea)


Wed 21-Aug-2019
^^^^^^^^^^^^^^^

Bowen Island

Worked on sockeye for beta testing:
* pip and setuptools installation issues; resolved
* XIOS-ARCH files; created
* perl URI.pm module required; resolved
* XIOS-2 build; succeeded
* NEMO build; succeeded
* Susan got successful run, but ~25m for 1d, so slower than optiumum, et all
* requested ennvar to identify sockeye to code and Venkat set up UBC_CLUSTER
* started adding sockeye to SalishSeaCmd
(SalishSea)

See work journal.
(Resilient-C)


Thu 22-Aug-2019
^^^^^^^^^^^^^^^

Bowen Island

Continued work on sockeye beta test:
* added most of the necessary features for sockeye to SalishSeaCmd, except calc of #PBS -l select=...
* did some exploration of binding options, but stopped due to chaotic changes by support.arc in netcdf and hdf5 libs
(SalishSea)

See work journal.
(Resilient-C)


Fri 23-Aug-2019
^^^^^^^^^^^^^^^

Bowen Island

Manager failed w/ ZMQError due to timing collision between ping_erddap and clear_checklist; exit code was 0, so supervisor didn't try to restart manager; options for resolution:
* add SystemExit(2) to nemo_nowcast._process_messages() ZMQError and Exception stanzas; probably sensible to do regardless
* change supervisor config program:manager.autorestart from unexpected to true; this replicates the behaviour of circus, and is semantically what we want, so do it
Continued work on 2007 GEMLAM processing; finished inter-day interpolation for missing solar variable values; successfully processed 13-16jan07; started feb07 but it looks like all of the frist 5 days have missing solar.
Continued work on sockeye beta test:
* finished adding sockeye to SalishSeaCmd
* helped Susan run about 25 1d tests; --bind-to core is best, 11 nodes is fastest, 8 nodes is most efficient
orcinus came back online after storage controller failure; Susan backfilled upload_forcing; I queued 20aug19 run.
(SalishSea)


Sat 24-Aug-2019
^^^^^^^^^^^^^^^

Bowen Island

Discovered that the reread function in supervisorctl was all that was required to apply autostart changes to all programs.
Continued working on nowcast-agrif backfilling:
* lots of clobbering by automation; waiting until after today's run attempt
* make_forcing_links nowcast+ 2019-08-20
* make_forcing_links nowcast-agrif 2019-08-20
* make_forcing_links nowcast+ 2019-08-21
* make_forcing_links nowcast-agrif 2019-08-21
* make_forcing_links nowcast+ 2019-08-22
* make_forcing_links nowcast-agrif 2019-08-22
* make_forcing_links nowcast+ 2019-08-23
* make_forcing_links nowcast-agrif 2019-08-23
* make_forcing_links nowcast+ 2019-08-24
* make_forcing_links nowcast-agrif 2019-08-24
Continued work on 2007 GEMLAM processing:
* discovered that there are no 01feb07 RPN files in /opp/GEMLAM/2007/; confirmed in PDF from Robert
* added exception for edge case of missing forecast hour files at end of date range
* worked on adding inter-day interpolation for >4 missing hours
* Robert's PDF also confirms that 2-23feb07 are lacking solar variable; Susan will write code to calculate it from sun angle and cloud fraction
* processed at 26-28feb07 and mar07
* started processing apr07; failed on 11apr due to <4hr missing hour interpolation w/ missing solar variable
(SalishSea)

See work journal.
(Resilient-C)


Sun 25-Aug-2019
^^^^^^^^^^^^^^^

Bowen Island

See work journal.
(Resilient-C)

Explored Cape Roger Curtis, Tunsall Bay, and Dorman Point by bike; lots of steep hills...


Week 35
-------

Mon 26-Aug-2019
^^^^^^^^^^^^^^^

Bowen Island

See work journal.
(Resilient-C)

Helped Susan set up conda-forge, etc. defaults via ~/.condarc, and env mgmt via env.yaml files.
Continued 2007 GEMLAM processing:
* re-ran 01-10apr to get close to 11apr interpolation issue
Worked on NEMO-Cmd:
* released v19.1; bumped version to v19.2.dev0
* changed to new MOAD package layout (1hr)
* replaced nemo_cmd.namelist module with f90nml; turns out nemo_cmd.namelist is used more outside NEMO-Cmd than inside it (SalishSeaNowcast, GoMSS_Nowcast, FVCOM-Cmd but only because it copies most of NEMO-Cmd instead of extending it)
* started refactoring run_NEMO and watch_NEMO to use f90nml instead of nemo_cmd.namelist
* fixed failing unit tests in SalishSeaNowcast
(SalishSea)


Tue 27-Aug-2019
^^^^^^^^^^^^^^^

Bowen Island

Fixed bugs in namelist.py to f90nml change in NEMO-Cmd re: strs instead of ints written to patched namelist, comments and formatting not preserved in patched namelist, and original namelist file permissions not preserved on patched namelist file.
Finished refactoring run_NEMO and watch_NEMO to use f90nml instead of nemo_cmd.namelist; added a TODO re: refactoring namelist writing code to use f90nml.patch().
SalishSeaCast team mtg; see whiteboard.
(SalishSea)

See work journal.
(Resilient-C)

Investigated bad surface currents forecast URL exception; someone typing bad URL?
Replaced raven & pyramid-crow packages w/ sentry-sdk.
(salishsea-site)


Wed 28-Aug-2019
^^^^^^^^^^^^^^^

Bowen Island

Continued work on 2007 GEMLAM processing:
* implemented calculation of solar radiation from cloud fraction and sun angle for gaps of >24h using code that Susan extracted from SOG
(SalishSea)


Thu 29-Aug-2019
^^^^^^^^^^^^^^^

Bowen Island to Vancouver

Continued work on 2007 GEMLAM processing:
* debugged implementation of calculation of solar radiation from cloud fraction and sun angle for gaps of >24h using code that Susan extracted from SOG
(SalishSea)


Fri 30-Aug-2019
^^^^^^^^^^^^^^^

Canyons/Arctic group mtg; see whiteboard.
(Canyons/Arctic)

* changed to new MOAD package layout (1,5h)
* released v19.1; bumped version to v19.2.dev0
(salishsea-site)

Continued work on 2007 GEMLAM processing:
* 16-25feb07 failed with various interpolation errors at ends
* 1-25feb07 failing on handling emptied missing_var_hrs["solar"] dict item
Helped Susan w/ sockeye module system issue on compute nodes, and 2015 bio-tuning on optimum.
Changed SalishSeaNowcast to new MOAD package layout
(SalishSea)


Sat 31-Aug-2019
^^^^^^^^^^^^^^^


Sun 1-Sep-2019
^^^^^^^^^^^^^^

Continued work on 2007 GEMLAM processing:
* added intra-day interpolation for ≤4 hr missing variable gaps
* ran 11-30apr07
(SalishSea)


September
=========

Week 36
-------

Mon 2-Sep-2019
^^^^^^^^^^^^^^

**Statutory Holiday** - Labour Day

Added production config YAML unit tests for download_results worker.
(SalishSea)





Tue 3-Sep-2019
^^^^^^^^^^^^^^

Added Sphinx autodoc import mocks for watchdog & PyPDF2 pkgs to SalishSeaNowcast docs.
Added index & module index to SalishSeaNowcast docs w/ links in sidebar menu.
Started adding destination host option to download_results worker.
SalishSeaCast team mtg; see whiteboard.
Invited Elise, Rachael, Ben, Tereza & Vicky to SalishSeaCast workspace.
(SalishSea)

Helped Vicky w/ HPC issues, and Rachael w/ Mercurial issues.
Had a visit from Ashu.
(MIDOSS)




Stack:
* debug gemlam interpolation
* wwatch3 hindcast automation
* wwatch3 run success confirmation
* fix warnings in figure modules
* release NEMO_Nowcast 19.2; change from circus to supervisor
* add hindcast deployment to SalishSeaNowcast docs
* Elise's notebooks into Sphinx
* fix get_vfpa_hadcp MMSI AttributeError issue

* hdf5 prep into MOHID-cmd

* docs for working on beluga
* rpn_to_gemlam
* change compute-canada HPC setup to put repos on $HOME to speed up deep dir traversals and nemo/salishsea run ops
* segmented runs code
* migration to arbutus.cloud
* refactor watch_NEMO_hindcast to work with qstat
* segmented runs docs
* build mohid on beluga
* change SADA workspace to SalishSeaCast; create new SADA workspace
* modernize salishsea-site repo; release 19.1
* close inactive branches in SalishSeaNowcast




 2004  hg init close-heads-bug
 2005  echo "Do some work on default." > foo
 2006  cat foo
 2007  hg add foo
 2008  cd close-heads-bug/
 2009  mv ../foo ./
 2010  hg add foo
 2011  hg ci -m"Do some work on default."
 2012  hg glog
 2013  echo "Do some more work on default." >> foo
 2014  hg ci -m"Do some more work on default."
 2015  hg glog
 2016  hg branch feature
 2017  echo "Do some work on feature." >> foo
 2018  hg ci -m"Do some work on feature."
 2019  hg glog
 2020  hg branches
 2021  hg up -r default
 2022  hg branches
 2023  hg glog
 2024  hg ci -m"Do more work on default after work on feature."
 2025  echo "Do more work on default after work on feature." >> foo
 2026  hg ci -m"Do more work on default after work on feature."
 2027  hg glog
 2028  hg merge -h
 2029  hg merge -r feature
 2030  hg glog
 2031  hg ci -m"Merge feature branch into default."
 2032  hg glog
 2033  echo "Do work on default after merging in feature." >> foo
 2034  hg ci -m "Do work on default after merging in feature."
 2035  hg glog
 2036  hg close-head -h
 2037  hg close-head feature -m"Close feature branch."
 2038  hg glog
 2039  hg up -r default
 2040  hg status
 2041  hg up --clean
 2042  history
close-heads-bug$ hg up default
abort: uncommitted changes
(commit or update --clean to discard changes)
close-heads-bug$ hg summary
parent: 6:7975eae997b7 tip
 Close feature branch.
branch: default
commit: (new branch)
update: 3 new changesets (update)
phases: 7 draft




* Replace old 2014 bloomcast page on ~sallen w/ redirect to present page
* Stephanie would like web access to prior year's bloomcasts




SalishSeaAGRIF production:
* generate sub-grids mapping dict for rivers so that sub-grid runoff files can be worker-generated instead of interpolated from full domain runoff file by nesting tools
* get Haro Strait sub-grid working
* enable turbidity, if possible

Move production to 201702:
* Rename riverTurbDaily2_*.nc to (at least) exclude the 2
* Update dir tree in docs/results_server/index.rst


* Process some images
* Take knives for sharpening


ToDo
====

* refactor, unit tests & docs for forcing links checking for NEMO-3.6

* reduce resolution of landing page images for faster load times
* add docs re: Resilient-C server-side app framework
* add EduCloud deployment docs

* research_ferries module
* JSON logging use example notebook

* review remaining nosy PRs
