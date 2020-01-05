*****************
2020 Work Journal
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

Wed 1-Jan-2018
^^^^^^^^^^^^^^

**Statutory Holiday** - New Year's Day

Helped Allens settle in at Amica White Rock.


Thu 2-Jan-2018
^^^^^^^^^^^^^^

Helped Allens settle in at Amica White Rock.


Fri 3-Jan-2018
^^^^^^^^^^^^^^

Finished initialization of 2020 GnuCash SADA books.

Enabled guest network and SmartSteering (2.4G/5G) on Telus router to phase out airport express.
Added port forwarding for lizzy and kudu.
Added ssh key to ConnectBot on phone.

Set up 43ravens organization under my personal account on GitHub, and moved imported NEMO_Nowcast repo to it.

Imported this repo to GitHub.
Imported dotfiles repo to GitHub. Added githooks/generic/ pre-commit.sh and rescuetime commit highlight post-commit hooks; there is no post-tag hook in git.


Sat 4-Jan-2018
^^^^^^^^^^^^^^

Set local git repo email with: git config user.email "name@example.com"
Set kudu git config to always pull --rebase; git config --global pull.rebase true; see:
* https://coderwall.com/p/tnoiug/rebase-by-default-when-doing-git-pull
* https://mislav.uniqpath.com/2013/02/merge-vs-rebase/

Changed NEMO_Nowcast readthedocs webhook to GitHub.
Updated NEMO_Nowcast copyright year range and bumped version to 20.1.dev0
Set up CI workflow for NEMO_Nowcast via GitHub Actions.
Changed to launch clear_checklist after wwatch3 forecast2 pings ERDDAP instead of after NEMO forecast2 make_feeds to avoid wwatch3 post-processing workers not being able to find what they need in the checklist.
(SalishSeaCast)

Started writing https://docs.google.com/document/d/1Gex3JdO8GpMdp0vxCPR05KOw5YFyg7mRV35j5gGJ8V8/edit?folder=0AMzQNtq8h6DpUk9PVA re: MOAD version control migration.
(MOAD)
