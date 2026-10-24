#########################
Streaks and Glints in DP2
#########################

.. abstract::

   We describe the detected streaks and glints in difference images and DiaSource catalogs in Data Preview 2, and comment on plans to improve detections in future data releases.

Add content here
================

In the Data Release Pipelines (DRP), the detection and analysis of trailed 
objects is performed during the detection and measurement phase of the
difference image analysis (DIA). 

Linear Feature Detection
========================

Describe underlying Kernel Hough Transform methodology.
1. Operates on a binary array typically setting a threshold for a "detected pixel". Ideally generated from background subtracted difference image free of cosmic rays and instrumental effects.
2. Detects 2 lines for each edge of the streak profile. These are clustered using iterative KMeans and averaged to obtain 1 line per streak.
3. Create an initial footprint and fit with a Gaussian cross-sectional profile model. Iterate fit until convergence and exclude regions along the oriented bounding box that do not include DETECTED pixels.
4. Output are lines in rho/theta Hesse normal parameterization for a image-centered detector pixel coordinate system.

Streak Detection in DP2
=======================

Describe full streak detection algorithm and results.
1. Describe the processing in the context of the overarching `DetectAndMeasureTask` and the pipeline workflow.
2. Describe the results and the population statistics.
   1. Include histograms of sigma/peak signal values for detected streaks by detector and filter.
   2. Maybe include some notable examples of identified streaks?

The number of detected streaks per visit is shown in the following table, both
separated by band, and as a cumulative total.

====== ======= ====== =================
Filter Streaks Visits Streaks per Visit
====== ======= ====== =================
u-band 16167   3433   4.7
g-band 40072   6248   6.4
r-band 54111   8345   6.5 
i-band 69380   9693   7.2
z-band 108166  7118   15.2
Y-band 98661   4672   21.1
All    386557  39509  9.8
====== ======= ====== =================

There is a substantial increase in the number of detected streaks per visit in
z-band and Y-band visits. Based on the canonical reflectivity properties of the
surfaces of orbiting objects and the spectral energy distribution of the
illumination from the Sun, it was expected that the greatest number of bright
streaks would be observed in g-band or r-band.


Identified Improvements
=======================

List of identified issues including:
1. DM-56055 to address bad pixel masking in preprocessing.
2. DM ticket to address SPIKE mask.
3. Inclusion of ITL_DIPS mask as default bad mask plane.
4. Persistence of streak results as a catalog of streaks, rather than a structured dictionary.

Glint Detection in DP2
======================

1. Describe algorithm (looks for sources along linear tracts within a single detector image).
2. Describe results (images/tables from PCW presentation)
3. List of identified issues:
   1. Lack of inter-detector source linking.
   2. Many false positives associated with sources in crowded fields (many sources, increased probability that several fall approximately along a line).


See the `Documenteer documentation <https://documenteer.lsst.io/technotes/index.html>`_ for tips on how to write and configure your new technote.
