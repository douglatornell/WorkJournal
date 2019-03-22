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

Tracked down paramiko deprecatsion warning re: cryptography; see #salishseacast.
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

Advised Hayley Dawson @Hakai on how to get T&S fields from SalishSeaCast ERDDAP to produce boundary conditions for Discovery Islands FVCOM model.
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
Recovered manually from a but in NEMO_Nowcast race condition mgmt that caused manager restart on execution of after_*() that returns 2 or more NextWorker instances.
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
mpich scaling runs on optimum:
* 2nodes-4x9+1 timed out on track for ~5h
* 5nodes-11x14 running; eta 72mh18m11s
* 10nodes-11x33
* 14nodes-16x34 running; eta 68m
(SalishSea)

EOAS colloquium by Julie Keister of UW re: climate effects on Puget Sound zooplankton







If I am correctly understanding what you want to do, you need to build both xios and nemo with the new compilers and libraries. xios has to be built first because it provides a lib that nemo links to. The xios I used in /scratch/dlatorne/oneday_21nov14_2019-01-31T103135.621285-0800/ is built from an svn checkout of rev 1637. If you want to replicate exactly you need to grab that rev from http://forge.ipsl.jussieu.fr/ioserver/svn/XIOS/trunk, or you can just grab whatever rev the present trunk is at - one of the xios devs asserted on the xios list this morning that trunk is stable.

Once you have an xios checkout, copy these 3 files into its arch/ directory:
/home/dlatorne/project/dlatorne/MEOPAR/xios-2.0/arch/arch-X64_CEDAR.env
/home/dlatorne/project/dlatorne/MEOPAR/xios-2.0/arch/arch-X64_CEDAR.fcm
/home/dlatorne/project/dlatorne/MEOPAR/xios-2.0/arch/arch-X64_CEDAR.path

and edit them as you wish to point to the libs you want to use, etc. Then built xios with:
cd /home/dlatorne/project/dlatorne/MEOPAR/xios-2.0/
./make_xios --arch X64_CEDAR

I often do that build in an 8-core interactive session with the --job 8 option added to speed it up. If you need to do a clean build of xios, the command to clean the tree is:

./tools/FCM/bin/fcm build --clean





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
