---
autogenerated: true
title: Example Beanshell scripts
layout: page
section: Programming
---

These beanshell scripts can be run from the '[Script
Panel](Script_Panel_GUI "wikilink")' (in the 'Tools' menu). Either load
the script in the Script Button Panel (using the 'add' button), or open
the script in the editor (using the 'open' button.

Most of these scripts can be translated with minimal modification to the
Python programming language (see
[Pycro-manager](https://github.com/micro-manager/pycro-manager))

[Media:media/Sdemo1.bsh](Media:media/Sdemo1.bsh "wikilink") - Hello World

[Media:media/Sdemo2.bsh](Media:media/Sdemo2.bsh "wikilink") - Shows how to use
ImageJ functionality within the Beanshell environment

[Media:media/SetZoom.bsh](Media:media/SetZoom.bsh "wikilink") - Utility that sets
the zoom level of the current ImageJ image window

[Media:camera\media/_test.bsh](Media:media/Camera_test.bsh "wikilink") - Example
camera test.

[Media:image\_snap\media/_example.bsh](Media:media/Image_snap_example.bsh "wikilink")
- Shows how to snap (but not display) an image

[Media:image\_snap\_example\media/_2.bsh](Media:media/Image_snap_example_2.bsh "wikilink")
- Shows how to snap and display an image. The image window must already
be open (Snap an image once manually before running the plugin).

[Media:media/SnapAndMeasure.bsh](Media:media/SnapAndMeasure.bsh "wikilink") - Shows
how to use the ImageJ 'Measure' command that updates with every new
image snapped.

[Media:live\media/_demo.bsh](Media:media/Live_demo.bsh "wikilink") - Shows how to
process an image during acquisition. Needs the DemoStreamingCamera to
work.

[Media:media/Burst.bsh](Media:media/Burst.bsh "wikilink") - Shows how to start burst
mode from a script. Also shows how to save to file during acquisition.
Needs burst mode capable camera. May not work.

[Media:media/BurstExample.bsh](Media:media/BurstExample.bsh "wikilink") - Shows how
to run a sequence acquisition (used to be "burst mode") from a script
including setting up and starting the acquisition, grabbing the images
from the circular buffer, and filing them into the acquisition object.

[Media:media/TestAcq.bsh](Media:media/TestAcq.bsh "wikilink") - Demonstrates how to
perform 5D image acquisition using the gui object.

[Media:media/ManualAcq.bsh](Media:media/ManualAcq.bsh "wikilink") - Executes 5D
acquisition, prompting the user to change the filters/dichroics between
channel changes

[Media:media/AcqLC.bsh](Media:media/AcqLC.bsh "wikilink") - Example of a complicated
MD acquisition including visiting multiple positions as defined in the
position list, acquiring time-lapse data in individual channels.

[Media:media/MultiFastZStackASI.bsh](Media:media/MultiFastZStackASI.bsh "wikilink")
- Script used at the ASCB meeting 2008 to synchronize Arduino, camera,
AOTF and piezo stage to do fast multi-channel Z-stack acquistion

[Media:media/PositionList.bsh](Media:media/PositionList.bsh "wikilink") - Shows how
to build a positionList programmatically

[Media:media/Init.bsh](Media:media/Init.bsh "wikilink") - Shows how to configure the
sytem programmatically, i.e. without using configuration files. The GUI
changes will not be visible until you manually run the command 'Rebuild
GUI' or 'Refresh GUI' (Tools menu).

[Media:config\media/_test.bsh](Media:media/Config_test.bsh "wikilink") - Shows how
to define config groups programmatically. Will work with the
demo-configuration.

[Media:Roi\media/_copy.bsh](Media:media/Roi_copy.bsh "wikilink") - Demonstrates
copying of ROI from one camera to another.

[Media:RatiometricImaging\media/_main.bsh](Media:media/RatiometricImaging_main.bsh "wikilink")
- Beanshell for ratiometric Imaging (J. Husson).

[Media:RatiometricImaging\media/_singleImage.bsh](Media:media/RatiometricImaging_singleImage.bsh "wikilink")
- Beanshell for ratiometric Imaging. Takes only one image, can be useful
as a control before starting a whole acquisition with main beanshell
above (J. Husson).

[Media:simplest\_mosaic\media/_experiment.bsh](Media:media/Simplest_mosaic_experiment.bsh "wikilink")
- Control Andor Mosaic via iQ 2.7

The source code repository contains many more [example
scripts](https://valelab.ucsf.edu/trac/micromanager/browser/scripts)

--[Nico](User:Nico "wikilink") 21:04, 15 December 2007 (PST)
