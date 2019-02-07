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
Disabled ECget river flow crob jobs on sallish in favour of collect_river_data worker.
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

Sent email to Roman requesting chang nowcast-agrif reservation window to 10:00 to 13:00, and asking if he will consider building a Python 3.7 module on orcinus.
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
Ran nowcast-dev/29jan19 manually because it got interupted yesterday by salish reboot.
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
