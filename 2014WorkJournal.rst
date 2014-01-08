*****************
2014 Work Journal
*****************

This is my public work journal.
It is patterned after one that I have kept for several years for my work at Nordion_.
This journal is about my work as a Research Associate with `Dr. Susan Allen`_ in the `Department of Earth, Ocean and Atmospheric Sciences`_ at the `University of British Columbia`_ during our sabbatical which started on 1 July 2013.
It is also about my `open-source activities`_.


January
=======

Week 1
------

Wed 1-Jan-2014
~~~~~~~~~~~~~~

Changed web remote app to by run via Pyramid pserve utility but stummbled on entry point issue when I deployed it to the RaspPi.
(raspi_x10)


Thu 2-Jan-2014
~~~~~~~~~~~~~~

Dentist appt.
Created 2014 work journal file.

Updated copyright notice year range in tools repo.
Started work on changing :command:`salishsea get_cgrf` to transform CGRF files from 0600Z to day+1 0700Z to 0000Z to 2300Z.
(MEOPAR)

Worked with Charles on tick re: connection failure from hg notify hook on bjossa.
(SOG)


Fri 3-Jan-2014
~~~~~~~~~~~~~~

Hiking at Buntzen Lake with Susan and James.


Sat 4-Jan-2014
~~~~~~~~~~~~~~

Fixed bug in and improved usability of nc_tools module.
Continued work on changing :command:`salishsea get_cgrf` to transform CGRF files from 0600Z to day+1 0700Z to 0000Z to 2300Z and verifying that the CGRF dataset has some resemblance to EC observations at YVR and Sandheads.
(MEOPAR)


Sun 5-Jan-2014
~~~~~~~~~~~~~~

Continued work on changing :command:`salishsea get_cgrf` to transform CGRF files from 0600Z to day+1 0700Z to 0000Z to 2300Z and verifying that the CGRF dataset has some resemblance to EC observations at YVR and Sandheads.
(MEOPAR)


Week 2
------

Mon 6-Jan-2014
~~~~~~~~~~~~~~

Created Storm-Surge repo on Bitbucket for work on 1st paper.
Salish Sea project mtg; see Google Drive whiteboard image file.
Set up and queued a new attempt at the 40d tidal harmonics analysis run on jasper.
The run uses:

* the new bathymetry with smoothing at the Strait of Juan de Fuca boundary
* preliminary (not Masson model) T&S boundary conditions
* baroclinic zero-gradient boundary conditions
* no atmospheric forcing
* enhanced vertical diffusion turbulent viscosity of 100 m^2/s
* lateral turbulent viscosity of 60 m^2/s

Started work on implementing CGRF file rebasing into :command:`salishsea get_cgrf`.
(MEOPAR)

Sorted out buildbot docs issue; path in :file:`master.cfg` was incorrect.
snapper appears to have lost the ability to do mercurial notification hooks via localhost.
Worked on updating buildbot configuration:

* changed default arg values in :py:func:`extensions.config_builder` to reflect present workflow
* started to change builds to flatter directory structure but the 4 repo clones get jumbled
(SOG)


Tue 7-Jan-2014
~~~~~~~~~~~~~~

40d jasper run completed successfully; downloaded results files to /ocean.
Helped Nancy get up and running on jasper.
Finished quick-start docs re running on jasper.
Consolidated :file:`namelist.compute.*` run-set files.
Changed CGRF rebasing notebook to show u & v wind components instead of wind direction due to uncertainty about the CGRF wind compass.
Continued implementation of CGRF file rebasing into :command:`salishsea get_cgrf`; got working code, needs tests and cleanup.
(MEOPAR)

Research meeting w/ Susan.
Agreed to focus on MEOPAR until we go to Berkely, then shift to SOG.

Replied to Pierre Clement @BIO re: his query to Susan about code to download EC historical weather observations.
(SOG)
