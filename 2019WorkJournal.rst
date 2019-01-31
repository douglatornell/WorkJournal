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
(SalishSea)

See project journal.
(SalishSeaCast-FVCOM)

Updated repo clones on kudu.
(MIDOSS)


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

forecast/26jan18 got stuck at 84.7% due to a file length issue in atmos forcing; upload_forcing nowcast+ got triggered before grib_to_netcdf finished due to race conditions between grib_to_netcdf and make_live_ocean_files; recovery:
* kill watch_NEMO on west.cloud
* kill xios_server.exe on west.cloud
* wait for SalishSeaNEMO.sh script to finish on west.cloud
* upload_forcing cedar nowcast+ --debug
* upload_forcing orcinus nowcast+ --debug
* make_forcing_links orcinus nowcast+ --debug
* upload_forcing west.cloud nowcast+ --debug
* make_forcing_links west.cloud nowcast+ --debug
* make_forcing_links west.cloud ssh
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

(SalishSea)


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
