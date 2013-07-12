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
