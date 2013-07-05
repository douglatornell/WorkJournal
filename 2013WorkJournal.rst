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
