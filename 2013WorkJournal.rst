*****************
2013 Work Journal
*****************

This work journal was initiated on 1 July 2013 at the beginning of my sabbatical working with Susan Allen; see :file:`README.rst` for more details.

July
====

Week 27
-------

Mon 01-Jul-2013
~~~~~~~~~~~~~~~

**Statutory Holiday** - Canada Day

Tue 02-Jul-2013
~~~~~~~~~~~~~~~

Got new UBC CWL account set up on :kbd:`tom` and phone.
Started this work journal.
Installed https://github.com/dbousamra/sublime-rst-completion via :program:`git` on :kbd:`tom`.
:program:`git` installation was necessary because it is a Sublime Text 2 package.
Added completions for :kbd:`h4`, :kbd:`progam`, and :kbd:`kbd`.

Mapped out an initial work plan with Susan.
See `Google Drive document_`, and whiteboard_ images_ on Google+.

.. _Google Drive document: https://docs.google.com/document/d/1lnv_piFHrRGP5OfpoM-DbrrK1zUk_CsXGZbox_NZVt0/edit?usp=sharing
.. _whiteboard: https://plus.google.com/u/0/photos?pid=5896127424219627362&oid=114271466086835822013
.. _images: https://plus.google.com/u/0/photos?pid=5896127441965873394&oid=114271466086835822013

Added Julython_ webhooks to :kbd:`WorkJournal`, :kbd:`randopony-tetra`, and :kbd:`douglatornell.ca` projects on bitbucket_, and :kbd:`blogogile`, and :kbd:`blogofile_blog` on github_

.. _bitbucket: http://bitbucket.org/
.. _github: http://github.com

Moved into office 3053.

Toured ESB 5th floor rooms re: location for SWC bootcamp in Sep.
Tentatively settled on boardroom on 26 & 27 Sep.


Wed 03-Jul-2013
~~~~~~~~~~~~~~~

Got wired IP address assigned for :kbd:`tom`.

Tested Sublime Text 3 InsertDate package but it doesn't seem to work, so removed it again.

Investigated changes in EC online data.
It appears that the YVR sensors and reporting tools were changed from old EC to new NAV Canada on about 11-Jun.
The new YVR station number is 51442 in contrast to 889 that was used in :program:`bloomcast`.
Started writing email to Pat Wong @ EC re: station id discontinuity and availability of near-real-time hourly cloud fraction data from YVR but climate.weatheroffice.gc.ca site went down.
To be continued...
(bloomcast)

Buildbot slaves on :kbd:`cod`, :kbd:`nerka`, and :kbd:`snapper` all went down due to network/workstation issues.
Restarted them.
Forced all builds re: Susan's reversion of the mesozooplankton fit;
see http://bjossa.eos.ubc.ca:9000/SOG/changeset/1c1c453e6b29/SOG-code
(SOG)

Attended Physical Ocgy seminar where Jessica Spurgin talked about her research: "A numerical study of downwelling submarine canyons: The results are in!".

Investigated implications of Python :program:`setuptools`/:program:`distribute` merge for :program:`pip` and :program:`virtualenv`.
Neither have done releases yet that include :program:`setuptools-0.7`.

Set up :file:`~/.bash_profile` and :file:`~/.bashrc` files for Susan, and updated her :file:`~/.hgrc` file.
Talked her through setup of :kbd:`py27-SOG virtualenv`.

Worked on https://bitbucket.org/douglatornell/randopony-tetra/issue/17/.
3 out of 4 tests completed along with corresponding :meth:`BrevetViews.rider_emails` implemenation.
(randopony)

SublimeLinter plugin wasn't working; traced it to https://github.com/SublimeLinter/SublimeLinter/issues/479 and resolved it by deleting the :file:`Installed Packages/SublimeLinter.sublime-package` as recommended.


Thu 04-Jul-2013
~~~~~~~~~~~~~~~

Worked at home in the morning before doing a long ride to UBC via Iona.

Finished https://bitbucket.org/douglatornell/randopony-tetra/issue/17/ re: brevet rider email address list.
Added Sublime build system to randopony-tetra project to run :command:`python -m unittest discover` in the editor.
(randopony)

Watched John Hunter's SciPy 2012 keynote: http://www.youtube.com/watch?v=e3lTby5RI54.
:kbd:`streamplots` could be useful for NEMO results visualization.

Finished and sent email to Pat Wong @ EC re: YVR station id change and near-real-time cloud fraction data.
Her response says that the discontinuity in the data sets due to the YVR station id change is permanent, and that there is a closer to real-time web service (datamart) that provides YVR data sets that include cloud fraction numbers.
(bloomcast)

Reviewed http://software-carpentry.org/bootcamps/how-to.html.
Got confirmation from Julia that she will co-instruct with me in September.
(swc)

Wrote and published http://douglatornell.ca/blog/2013/07/04/sublime-text-build-system-for-project-unit-tests/
(douglatornell.ca)

Accepted "invited" lightening talk slot for my bloomcast talk at PyCon.ca.
Registered for conference, and book accommodation at the Chestnut residence for Fri 9-Aug through Tue 13-Aug.
Signed up to sprint on something; need to decide between Pyramid and CPython.
(pycon)


Fri 05-Jul-2013
~~~~~~~~~~~~~~~

Helped Tara sort out a segmentation fault in her working copy of SOG.
It was caused by some pretty messed up twisted merges that resulted in the :file:`chemistry_model.f90` memory allocation subroutines being missing.
(SOG)

EOAS Software Carpentry bootcamp is confirmed for 26 & 27 September.
(SWC)

Started reading Sublime Text plugin docs and tutorials with an eye toward creating a snippets package for Sphinx roles etc., and perhaps porting some of my favourite packages to 3.
Turns out that Sphinx snippets were as simple as creating :file:`Packages/User/Sphinx.sublime-completions` and defining the completions I wanted based on what's done in :file:`Packages/sublime-rst-completion/RestructuredText.sublime-completions`.
Sent a pull request to https://github.com/dbousamra/sublime-rst-completion re: changing the OS/X key mapping to avoid shadowing :kbd:`super+[bik]`.

Worked on assessing EC datamart service wrt bloomcast.
Datamart top level README is at http://dd.weatheroffice.gc.ca/about_dd_apropos.txt.
The near-real-time XML data (aka SWOB) are at http://dd.weatheroffice.ec.gc.ca/observations/swob-ml/.
They are organized by day, station, and hour and the file naming convention is documents at http://dd.weatheroffice.ec.gc.ca/observations/swob-ml/.
The SWOB-ML schema is documented at http://dd.weatheroffice.ec.gc.ca/observations/doc/SWOB-ML_Product_User_Guide_v5.2_e.pdf.

Things to be aware of:

  * The SWOB data are purged on a rolling 30-day basis.
  * The way in which YVR cloud fraction is reported changed on about 2013-06-13 when the YVR station sensors changed from EC to Nav Canada

Subscribed to :kbd:`dd_info` email list (powered by Mailman and Python :-)
(bloomcast)


Sun 07-Jul-2013
~~~~~~~~~~~~~~~

Experimented with moving :file:`Packages/User/Sphinx.sublime-completions` to :file:`Packages/sublime-sphinx-completion/` with an eye toward releasing it as a package on Github.
Confirmed that :file:`Packages/User/Sphinx.sublime-completions` can augment completions defined in :file:`Packages/sublime-sphinx-completion/Sphinx.sublime-completions`, which provides an extension mechanism for user-defined Sphinx roles.


Week 28
-------

Mon 08-Jul-2013
~~~~~~~~~~~~~~~~~

Updated work plan with my goals for this week and next.

Tagged the :program:`SOG`, :program:`SOG-code`, and :program:`SoG-bloomcast` repos at the revisions that were used for the 2013 spring bloomcast runs.
(bloomcast)

Cloned my https://github.com/douglatornell/sublime-rst-completion fork into my :file:`Packages` directory so that I can add the requested :file:`README.rst` docs to my pull request, and get Julython points for the commit (I hope).
Updated :file:`README.rst` with OS/X key bindings and another minor consistency edit and added it to the pull request.

Read Mark Halverson's "A Strait of Georgia Primer" (28-Feb-2013).
(MEOPAR)

Weekly mtg w/ Susan:

  * Discussed SoG Primer; Work w/ Mark to get it on the web
  * Susan and Rich will discuss & decide on SSMEP-ish web presence on 16-Jul
  * Discussed SOG-forcing data from EC datamart & climate.weatheroffice.gc.ca
  * Use isiknowledge.com to scope out background for bloomcast paper

Emailed Tim Morgan about status of my office key.
Delay is apparently not abnormal if a new key has to be cut.
Sigh.

Sent email to info@swc re: making EOAS bootcamp in Sep official.

Tara reported that the only substantive difference between her working :program:`SOG-code` repo and the reference repo on :kbd:`ocean` is the missing memory allocation code that we identified last week.
Bisected :program:`SOG-code` repo to figure out when :file:`chemistry_model.f90` memory allocation code got dropped, and the answer is in Ben's merge from :kbd:`changeset:1702:77d52eb0cf83` to :kbd:`changeset:1703:1b8cb697c7b7`.
Need to talk to Ben about what's in his working copy, and how the chemistry and carbonate modules are used.
Subsequent discussion with Susan lead to the hypothesis that Ben deliberately deleted the memory allocation code in :file:`chemistry_model.f90` when he was finished development because the quantities that he was allocating memory for are actually derived quantities.
Need to confirm that idea with Ben.
(SOG)


Tue 09-Jul-2013
~~~~~~~~~~~~~~~

Picked up keys to my office and the GFD lab.
Had to pay $20 deposit because I didn't pay one for my TRIUMF keys, or that payment is lost in the mists of time, or something.
Won't get $20 back until I return both TRIUMF and ESB keys; IOW it not really a deposit...

Confirmed with Ben that memory allocation in :file:`chemistry_model.f90` was indeed only used for development and was deliberately deleted before he pushed code to :kbd:`ocean` repo.
Helped Tara prepare her oxygen model changes to be push to the :kbd:`ocean` repo.
They caused new build failures for:

* R3 baseline regression
* YAML infile
* R3 microzoo regression
* R3 no remin regression

Those are expected failures due to the change in the dissolved oxygen boundary condition values.
Diffs are in run stdout file, standard chemistry timeseries file, profile file, and Hoffmueller file.
Built new refs for R3 baseline regression build.
(SOG)

:kbd:`sublime-rst-completions` pull request was merged.
Cleaned up my fork, flipped my working copy back to the :kbd:`master` branch, and synced it with upstream.

Created :kbd:`sublime-sphinx-completions` repo.

Got 24" 1920 x 1080 monitor - yahoo!

Drafted email to pat.wong@ec.gc.ca re: QA for datamart vs. climate.weatheroffice, and requesting algorithm for cf octas to tenths.

Afternoon coffee with Valentina.

Updated :program:`python2.7` :program:`virtualenvwrapper` on :kbd:`tom` to 4.0.
Updated :program:`pip-3.2` and :program:`virtualenv-3.2` to 1.3.1 and 1.9.1, repectively.

Started porting :program:`bloomcast` to :program:`python3.2`.
Chose 3.2 because that is the version of :program:`python3` that ships with Ubuntu 12.04 LTS, the target environment on the :kbd:`ocean` machines.
Ran into my chronic compilation issues on :kbd:`tom` during installation of :program:`MarkupSafe` and :program:`numpy` in a clean virtualenv; :program:`numpy` installation failed.
Time to reload :program:`Xcode` and :program:`python3.2`, and perhaps try :program:`homebrew` for the latter.
(bloomcast)


Wed 10-Jul-2013
~~~~~~~~~~~~~~~

Installed :program:`Xcode` on :kbd:`tom`.
Used :program:`homebrew` to install :program:`python2.7.5` and :program:`python3.3.2`, both with the :kbd:`--with-brewed-openssl` option, as :program:`python` and :program:`python3` repsectively.
Tweaked :file:`.bash_profile` to add :file:`/usr/local/share/python` to :envvar:`PATH` and put :file:`~/bin` and :file:`~/Documents/scripts` at the front of :envvar:`PATH`.
Also adjusted path to source :file:`virtualenvwrapper.sh` from.
Used :program:`pip` installed with :program:`homebrew` :program:`python2.7.5` (now the default) to install :program:`virtualenv` and :program:`virtualenvwrapper`.
Used :program:`homebrew` to install :program:`python3.2.3` with the :kbd:`--with-brewed=openssl` option so that I have a comparable version to the :kbd:`ocean` machines.

Created at new :kbd:`bloomcast-3.2` virtualenv and tried installing :program:`bloomcast` dependencies again:

* :program:`MarkupSafe` speedups extension compiled successfully
* :program:`PyYAML` extension compiled successfully after doing :kbd:`brew install libyaml`
* :program:`numpy` compiled and installed successfully, though with plenty of compiler warnings
* :program:`matplotlib` compiled and installed successfully, though with plenty of compiler warnings

Tagged beginning of :program:`bloomcast` port to Python 3.
Got test suite running under Python 3 with the exception of 4 tests that I marked as expected failures because they test SOG infile reading implementation details that no were changed in the Python 2.6 version without updating the tests.
:program:`MarkupSafe` is presently incompatible with Python 3.2 so removed it from dependencies as :program:`Mako` has been modified to not try to use it under 3.2.
Main :program:`bloomcast` script can only be run if I remove the relative import changes that I made to get the test suite to run under :command:`unitest discover` and :program:`pytest`; need to fix that.
Even when it does run, it fails during infile editing.
To be continued...
(bloomcast)

Had coffee with Julia to start planning for Sep EOAS SWC bootcamp.
(SWC)

Checked YAML infile build results; they show the same failure pattern as the R3 baseline regression build.
Built new refs for YAML infile build.
(SOG)


Thu 11-Jul-2013
~~~~~~~~~~~~~~~

Finished and sent email to pat.wong@ec.gc.ca re: QA for datamart vs. climate.weatheroffice, and requesting algorithm for cf octas to tenths.
(bloomcast)

Explored :command:`hg rebase` re: improving Mercurial workflow for SOG.
(SOG)

Long bike ride with Susan to Iona then around UBC: 49.2 km; then worked at home.

Did more research on whether or not we should to license SOG docs under a Creative Commons license in constrast the the Apache 2.0 license that we've settled on for the code.
Coming to the conclusion that one license is sufficient.
(SOG)

Decided on public domain release with emphsis via unlicense.org for :kbd:`sublime-sphinx-completions` project.
Wrote :file:`README.rst`.

Checked R3 microzoo regression and R3 no remin regression build results; they show the same failure pattern as the R3 baseline regression build.
Susan checked the graphs.
Built new refs for those builds.
(SOG)


Fri 12-Jul-2013
~~~~~~~~~~~~~~~

Worked on setup of EOAS SWC bootcamp.
(SWC)

Built a Python 2.7 virutalenv for :program:`bloomcast` and tried to run the test suite via :program:`nose`; hit the same relative import issue as under Python 3.2.
Running the script hit the same infile editing issue in :program:`colander` as under Python 3.2.
Based on the decision to build the new :kbd:`salish` compute machine with Ubuntu 13.04, and the likelihood that :program:`bloomcast` will run there, changed port traget to Python 3.3.
Added :command:`bloomcast` entry point to resolve relative import issue.
Finished porting :program:`bloomcast` to Python 3.3.
Had to do a provisional port of :program:`SOGcommand` to Python 3 too because :program:`bloomcast` uses its API.
:program:`SOG-code` runs fail due to :program:`bloomcast` infiles not having been kept up to date with changes in the repo.
Updated :file:`2013_bloomcast_infile.yaml` to match :program:`SOG-code` repo.
(bloomcast)

Read MEOPAR stakeholders workshop report.
(MEOPAR)

Tweaked :file:`rdiff_backup.backup.py` script to use :command:`ssh matisse true` to wake :kbd:`matisse` after remote connection to :kbd:`sada.home` network via :kbd:`wall`.
However, it seems that :command:`ssh` from :kbd:`wall` cannot consistently wake :kbd:`matisse` (though it worked in a test yesterday).

Helped Susan update an old SciPy/NumPy script for the SOG freshwater parameterization fit that had rotted out due to API changes.
(SOG)


Week 29
-------

Mon 15-Jul-2013
~~~~~~~~~~~~~~~~~

Debugged :kbd:`SOG-code-bloomcast` runtime failure due to bad infile structure; I had done an :command:`hg update` in my :file:`SOG_2and3` repo to an earlier version that I forgot to undo before I created the Python 3.3 port patch.
Mixing layer depth graph generation fails with a :py:exc:`IndexError` if the wind data date is outside the range of the run dates.
:program:`Mako` is raising a :py:exc:`TypeError` during the results template rendering.
(bloomcast)

Prepared for weekly mtg w/ Susan.

* Susan and Rich have decided on a single web domain/site with Susan and I taking the lead, but we need a new name that includes "observation"
* Discussed SWC bootcamp outline:

  * Day 1: minimal sh intro, git intro, python intro; use YVR air temperature and precipitation data as basis for examples, do data read, plots, histograms, distruibution fitting, and export code from ipynb to source file(s); us git as we go along to track the project

  * Day 2: base examples on plotting data on maps, use git collaboratively, need to work in testing, wrap up with python, sh & cron automation

  * Postpone opening of registration until 30-Jul
  * Riff on SWC pre-assessment questionaire


Tue 16-Jul-2013
~~~~~~~~~~~~~~~

Opened ticket for Charles to install buildbot package on ocean machines.
Re-enabled buildbot on-push hooks in :program:`SOG`, :program:`SOG-code`, :program:`SOG-forcing`, and :program:`SOG-initial` repos, and sent email to SOG users reminding them how the hooks work, and telling them to get rid of the :kbd:`remote_cmd` section of their :file:`.hg/hgrc` files in their clones of those repos.

Helped Tara get new Fraser and Englishman river files added to the :program:`SGO-forcing` repo so that :kbd:`YAML infile` buildbot case could run to completion.
(SOG)

Built a Python 3 :program:`bloomcast` virtualenv on :kbd:`salish`.
After Charles changed :file:`/data` so that it was writable, I created :file:`/data/dlatorne/.virtualenvs/` and used :command:`pyvenv-3.3` to create a :file:`bloomcast` virtualenv within it.
With the virtualenv activated I installed :program:`setuptools` via::

  wget https://bitbucket.org/pypa/setuptools/downloads/ez_setup.py -O - | python

and then used :command:`easy_install` to install :program:`pip`.
I installed the required packages manually with reference to :file:`SOG-bloomcast/requirements.txt`.
To compile C extensions I opened at ticket for Charles to install the :program:`phthon-dev` and :program:`python3-dev` packages.
Also opened a ticket to get the :program:`libyaml-dev` and :program:`python3-matplotlib` packages installed; when that was done I symlinked :program:`matplotlib`, :program:`dateutil`, and :program:`pytz` from :file:`/usr/lib/python3/dist-packages/`.
I was able to use :program:`pip` to installed the rest of the packages, although :program:`numpy` did warn about the lack of :program:`atlas`, :program:`blas`, and :program:`lapack` packages.
(bloomcast)

Cloned the :program:`SOG-code` repo to :kbd:`salish` and confirmed that :kbd:`salish` is *fast*; :command:`make clean && time make` reports about 5 seconds, and :command:`make clean && time make -j2` reports about 2.5 seconds.
Letting :command:`make` use more than 2 processes tends to result in failures, and event :kbd:`-j2` failed at least once.
Created a Python 2.7 virtualenv for :program:`scons` and installed it from the source tarball.
Playing with :command:`scons --clean && time scons -j` I found that 8 processes gives the minimum compile/link time of about 3 seconds.

Cloned the :program:`SOG`, :program:`SOG-forcing`, and :program:`SOG-initial` repos.
Tried to install :program:`SOG` under Python 2.7 and it failed because :file:`Python.h` was missing, so I re-opened the :program:`python-dev` request ticket.
Applied the work-in-progress Python 3 patch to :program:`SOG` and was able to install it.
Ran the :file:`infile.yaml` case and it completed in 6 minutes 4.028 seconds, in contrast to a :program:`buildbot` of the same case that happened this afternoon on :kbd:`herring` that took 20 minutes 43 seconds.
(SOG)

Researched papers on operational ocean models on Web of Science: 2 journals look promising; Journal of Operational Oceanography, and Environmental Modelling and Software.

Continued working on tracking down the :program:`Mako` :py:exc:`TypeError` issue in the Python 3.3 port.
(bloomcast)


Wed 17-Jul-2013
~~~~~~~~~~~~~~~

Tried to restart :program:`buidbot` slaves after last night's :kbd:`ocean` upgrade.
:kbd:`bjossa` reports a stale NFS handle for :file:`/ocean`, :kbd:`nerka` says that :file:`ocean` is not mounted, and :kbd:`cod` and :kbd:`coho` are down.
(SOG Buildbot)

Continued email conversation with Amy@swc re: preparations for SWC bootcamp.
(SWC)

Resolved :program:`Mako` :py:exc:`TypeError` issue in the Python 3.3 port; it was caused by the use of :py:builtin:`xrange` in the template.
Started working on confirming that current :program:`SOG-code` produces the same :program:`bloomcast` results as the 2013 production version did.
(bloomcast)

Created a new :kbd:`SOG-2.7` virutalenv and used it to update Python package dependencies for :program:`SOGcommand`.
Determined that :command:`scons -j2` is optimal for full compilation of :program:`SOG` on :kbd:`tom`.
Worked on understanding the differences between the new river flow files that Tara pushed to :program:`SOG-forcing` yesterday and the :file:`*_hostirc.dat` files that we have been using.
New files are formatted differently, and include data for 2011 and part of 2012.
(SOG)

Attended physical ocgy seminar on SoG pH and aragonite saturation given by Ben M-M.

Finally got DVI working on BenQ monitor with a MiniDisplayPort to HDMI cable.


Thu 18-Jul-2013
~~~~~~~~~~~~~~~

Created https://github.com/douglatornell/sublime-sphinx-completion and pushed intial work on the package to it.

Long bike ride with Susan to Iona then around UBC: 49.7 km; then worked at home.

Restarted :kbd:`herring` and :kbd:`sable` build slaves.
:kbd:`cod` and :kbd:`nerka` are down due to disk failure and configuration issues after the :kbd:`ocean` upgrade.
(SOG)

Worked with Susan and Charles to resolve Tara's and Susan's inability to push commits to the :kbd:`ocean` hg repos; :kbd:`sallen` group on :kbd:`ocean` was missing.

Wrote G+ post about porting Mako templates to Python 3 and the need for manual checking for deprecated syntax.


Fri 19-Jul-2013
~~~~~~~~~~~~~~~

Manually updated :program:`sublime-rst-completion` package via git fetch/merge since automatic updating doesn't seem to work.
Determined that :program:`SublimeLinter` packages gets messed every time that it auto-updates because the unpatched Sublime 2 version gets dropped in the :file:`Installed Packages/` directory; added a comment to https://github.com/SublimeLinter/SublimeLinter/issues/479.

Tagged v3.0b1 of :program:`SoG-bloomcast` re: completion of port to Python 3.3.
Started evaluation vs. results of 2013 production deployment; running on :kbd:`salish`.
Determined that :command:`scons -j16` is optimal for full compilation of :program:`SOG` on :kbd:`sable`.
Had to add a symlink to :file:`/usr/lib/python3/dist-packages/matplotlib-1.2.1.egg-info` to the :program:`bloomcast` virtualenv on :kbd:`salish` to get :program:`bloomcast` to install with :command:`pip install -e .`.
Had to add the :kbd:`northern_water_power_riverflow_influence` and :kbd:`northern_water_normalization_riverflow_influence` parameters that Susan added yesterday to :file:`2013_bloomcast_infile.yaml`.
Had to tweak path to :program:`SOG` executable in :py:mod:`bloomcast.py`; it should probably be read from :file:`config.yaml`.
Susan figured out that differences vs. results of 2013 production deployment are probably due to the river flow forcing data files starting on 19-Jan-2012 instead of 1-Jan-2012; bug in :program:`bloomcast` or glitch at wateroffice.ec.gc.ca?
(bloomcast)

Mtg w/ Susan, Ben M-M, and Tara to discuss tuning dissolved oxygen results to STRATEGEM data via northern return flow parameters (power and normaliztion factor) that Susan added yesterday.
Restarted :kbd:`nerka` build slave.
Got Tara set up to run :program:`SOG` on :kbd:`salish`.
(SOG)


Week 29
-------

**Vacation** - Washington Coast Cycletour


Week 30
-------

Mon 29-Jul-2013
~~~~~~~~~~~~~~~

Restarted :kbd:`snapper` build slave.
Updated :file:`.local/python2.7/` packages on :kbd:`ocean` because sessions on :kbd:`cod` were throwing errors about :program:`stevedore` and :program:`distribute`.
All of the :kbd:`ocean` workstations that run build slaves are now on Ubuntu 12.04 LTS and thus Python 2.7, so support for Python 2.6 can be dropped from :program:`SOG` tools and projects.
Restarted :kbd:`cod` build slave.
Finished porting :program:`SOGcommand` to run under Python 2.7 and 3.3.
Added error handling for the case of elements that are present in the YAML schema but missing from the YAML infile.
Added licensing files and header blocks to :program:`SOGcommand` to relicense it under the Apache License, Version 2.0 in preparation for release to a public repo on Bitbucket.
(SOG)

Commented out code in :file:`.bashrc` on :kbd:`ocean` that forces :program:`virtualenv` to use :program:`distribute`, selects Python version based on OS ditribution release, and sets up PGF90 environment variable.

Weekly research meeting with Susan:

* Tried to test hypotheses about why the river flow data doesn't start on 1-Jan-2012 and discovered that the climate.weatheroffice URL structure has changed
* Discussed J. Operational Ocgy and Env Modeling & Software as target journals for bloomcast paper; Douw may be an editor of the latter - check
* Discussed design of :program:`sog-forcing` update automation that we came up with last week.
* Agreed on :kbd:`salishsea-meopar.eos.ubc.ca` as domain for EOAS MEOPAR work
* Discussed :kbd:`SoG-P` as name for :program:`SOG` operational productivity calculation project, but hoping that we can do better
* Need to write and release the SWC bootcamp announcement email, and move forward with the outline of the bootcamp
* Need to get serious about bloomcast lightening talk for PyCon.ca
* Need to run GEOTRACES NEMO on Westgrid

Discovered that climate.weatheroffice has changed their URL structure so that :program:`bloomcast` now fails when it tries to request the Sandheads wind data.
(bloomcast)

Discussed with Susan and Charles the idea of moving :program:`SOG-buildbot` master and :program:`trac` server from :kbd:`bjossa` to :kbd:`coho` so that the former can be retired, and the latter can serve a useful role despite its Athlon processor.
(buildbot)
