---
autogenerated: true
title: Andor SRRF-Stream
layout: page
---

## Introduction

Andor ‘SRRF-Stream’ is a Real-Time Super-Resolution Microscopy module
that is offered as an extension of iXon Life, iXon Ultra EMCCD camera
and Sona functionality. Super-resolution radial fluctuations (SRRF –
pronounced ‘Surf’) is a synthesis of temporal fluctuation analysis and
localisation microscopy. SRRF takes a frame-burst (e.g. a short rapid
burst of 50 frames or greater) at a given focal plane and wavelength, as
input to create a single super-resolution image. As they are acquired
the images are streamed to the GPU for processing. Once all frames are
acquired and processed the result is then delivered to the imaging
pipeline. Further information on the algorithm can be found in the [SRRF
paper](https://www.nature.com/articles/ncomms12471) published in Nature
Communications. A short talk describing the algorithm can also be found
[here](https://www.youtube.com/watch?v=HjrcM8NfWJE).

## Minimum Requirements

-   x64 [Nightly
    Build](http://valelab4.ucsf.edu/~MM/nightlyBuilds/1.4/Windows/)
    MMSetup\_64bit\_1.4.23\_20170825.exe or later
-   A NEW iXon Life, iXon Ultra EMCCD or Sona camera
-   Andor Driver Pack (public download available
    [here](http://www.andor.com/downloads?src=micro))
    -   version 2.102.30024.0 or later for owners of an iXon Life and
        iXon Ultra EMCCD camera
    -   version 3.14.30005.0 or later for owners of a Sona camera
-   SRRF-Stream license (unlocks SRRF-Stream in camera)
-   A CUDA-compatible Nvidia GPU card with Compute Capability 3.0 or
    above:
    -   At least 4GB of on-board GPU RAM is required
    -   (Note: At least 8GB is recommended for best performance, and is
        required for dual camera SRRF on Sona with largest recommended
        magnification of 6)
-   Latest Nvidia Drivers for all installed Nvidia CUDA capable GPU
    cards
-   Windows 7, 8 or 10: 32-bit or 64-bit Operating System. *Note
    SRRF-Stream is not currently compatible with Linux or mac OS.*
-   3.0GHz single core or 2.6GHz multi-core processor
-   At least 4GB CPU RAM
-   200MB free disc space to install SDK and SRRF-Stream software (at
    least 1GB recommended for data spooling)
-   Solid-state drive (SSD) capable of a minimum sustained write speed
    of 100MBs for spooling data

## Installation

### Prerequisites

1.  Install the latest nightly build of Micro-Manager
2.  Install the Andor Driver Pack 2 for Ultra USB or the Andor Driver
    Pack 3.
    -   On the Select Destination Location dialog, click browse and
        choose the current Micro-Manager installation directory. Then
        click Yes to confirm that you do want to install to that folder.
3.  Install the latest NVidia drivers from
    <http://www.nvidia.co.uk/Download/index.aspx>.
4.  Install SRRF-Stream for Micro-Manager
    -   On the Select Destination Location dialog, click browse and
        choose the current Micro-Manager installation directory. Then
        click Yes to confirm that you do want to install to that folder.

## Configuration

If using a previous configuration, you may need to remove and re-add the
Andor camera device in order to pick up your new iXon/Sona camera.
Alternatively, create a new configuration using the Tools - Hardware
Configuration Wizard...

You will see the SRRF properties in the device property browser as shown
below  
<img src="media/AndorSRRFPropertiesSona.jpeg" title="fig:media/AndorSRRFPropertiesSona.jpeg" width="600" alt="media/AndorSRRFPropertiesSona.jpeg" />  
If there are no SRRF properties in the device property browser, please
check you have installed the SRRF-Stream to the correct location, and
you are running that version of Micro-Manager. Ensure this is 64-bit.  
If there is but one read-only property (SRRF Status), a description of
the error will be displayed for that property value. Please check you
have met the minimum requirements and completed the prerequisites. If a
further attempt does not reveal all the SRRF properties, please attach
the relevant CoreLog txt file (present in the Micro-Manager installation
directory / CoreLogs folder) and send to 3rdpartysupport@andor.com

## Properties

Parameters for the SRRF algorithm can be set via the device property
browser. Sensible default values are used for each parameter if the
values are not explicitly set by the user.  
;**Enable**

  
SRRF is disabled by default. Enable this to acquire SRRF Images.

<!-- -->

**Interpolation Type**  
This type determines the method by which sub-pixel values are calculated
from the gradient fields that are calculated for each frame.

The default value for this parameter is Catmull-Rom.

:\*Catmull-Rom - This method typically provides the sharpest result
possible when re-sizing an image.

:\*Fast B-spline - This method may produce results that are slightly
blurred when compared to the Catmull-Rom filter. However, it is much
faster than the Catmull-Rom, and can provide speed-up of close to 50%.

**Number of Frames per Time point**  
This is the number of frames input per time point, i.e. the number of
frames within each SRRF frame-burst. The larger this value, the greater
the achievable resolution enhancement, but the longer the processing
takes.

The default is 100.

<!-- -->

**Radiality Magnification**  
The radiality magnification setting determines how many pixels each
original image pixel is split into. For example, a radiality
magnification of 2 will split each image pixel into 2x2 pixels. Each
resultant SRRF Image will therefore be proportionally larger e.g. camera
ROI = 128x128, radiality = 8, SRRF image = 1024x1024 pixels.

The default is 4, the range being 1 - 10 inclusive. (as of SRRF version
1.14.0.0 the range is 1 - 6)

<!-- -->

**Radiality Temporal Analysis**  
This determines the way in which the final super-resolution image is
created from the output of each radiality transform calculation.

The default value is Mean.

:\*Mean - This method calculates the final image as an average intensity
calculation of the radiality transforms of each acquired frame in the
frame burst.

  
  
This is often a good starting point for analysis, especially for
blinking data sets where fluorophores overlap, or data sets where
fluorophores display limited intensity fluctuations such as in
conventional TIRF or widefield microscopy.

‘Mean’ is ‘Temporal Radiality Average’ in NanoJ.

:\*MIP - This method calculates the final image as a maximum intensity
projection of the radiality transforms of acquired frame in the
frame-burst.

  
  
MIP works most successfully for sparse data sets i.e. classical
PALM/STORM experiments.

‘MIP’ is ‘Temporal Radiality Maximum’ in NanoJ

<!-- -->

**Ring Radius**  
The ring radius will set the radius in pixels (before radiality
magnification) in order to calculate the intensity gradients surrounding
each co-ordinate.

The default for this parameter is 0.5. Valid decimal values range
between 0.1 and 3.0 inclusive. (as of SRRF version 1.14.0.0 the default
is 2.0 and values range between 1.0 and 3.0)

<!-- -->

**Save Original Data - Option**  
This option allows the user to save the original data from the camera
directly to disk. The default is None.

These images cannot be displayed during acquisition, however, ImageJ
will easily read this file format back in again. See [Opening .raw data
files](#Opening_.raw_Data_files "wikilink") section.

The images are placed in a Date and Time stamped folder to prevent
overwriting  
*e.g. 2017-Jul-17\_14.25.25.557025*  
at the location specified by the Save Original Data - Path property.

:\*None - No data from the camera is saved. Only the SRRF images will be
displayed and available to save or process etc.

:\*All - An image stack consisting of all the frame-burst images from
the camera is saved to disk, for each SRRF image generated.

  
  
An image generated from a 256x256 ROI with 100 frames per burst is named
*"Image\_AllOriginalData\_256x256x100.raw".*

:\*Averaged - A single average image of the frame burst images from the
camera is saved to disk.

  
  
This image will be the same size as each frame coming from camera e.g.
512x512 pixels, and is named *"Image\_AvgOriginalData\_512x512x1.raw".*

  

## Other SRRF property defaults

All ‘hidden’ parameters are set to the defaults in NanoJ, as follows:

-   Axes in Ring: 6 (as of SRRF version 1.14.0.0 this is 24)
-   No Drift Correction
-   No Cropping of data
-   All Advanced Radiality settings set to disabled (Remove Positivity
    Constraint / Renormalize, Gradient Smoothing)
-   Intensity Gradient Weighting enabled
-   Gradient Weighting disabled
-   Minimize SRRF patterning disabled
-   Fast linearise SRRF disabled

  

## Opening .raw Data files

The original data from the camera is written to disk as raw data, with
the file extenstion .raw appended to the filename. The file dimensions
are also included in the filename, as ImageJ can interpret these and
pre-set the width, height and number of images contained within the data
file.  
This .raw file can be dragged into the ImageJ status bar and will open
the Import &gt; Raw dialog with the correct dimensions pre-set.  
Alternatively, navigate to File &gt; Import &gt; Raw... from ImageJ and
select the desired image data file. The only other 2 pieces of
information ImageJ needs to know is the Image type which should be set
to ***16-bit Unsigned*** and that ***Little-endian*** byte order is
set/checked. Click OK, and the original data will open in a new display
window.

  
== Known issues / Troubleshooting ==

-   Multi-Dimensional Acquisition has a 20s timeout - if a large burst,
    from for example a full frame iXon Ultra 888 (1024x1024), is
    acquired then the timeout may occur before the first SRRF image is
    displayed.

  
  
*Workaround:*

The device adapter cannot access that setting directly, but if it
exposes a (read-only) property indicating how long the timeout should be
(based on the input settings) then a simple script function can read
that property and configure the acquisition engine timeout accordingly.
This is attached as a runnable, and executed as specified when Acquire
is clicked.

An example script is shown below:

<!-- -->

    acq.clearRunnables();

    runnable = new Runnable() {

      public void run() {
        settings = gui.getAcquisitionSettings();
        value = mmc.getProperty("Andor", "TimeOut");
        settings.cameraTimeout = Integer.parseInt(value);
        gui.setAcquisitionSettings(settings);
      }

    };

    gui.attachRunnable(0, 0, 0, 0, runnable);

-   Live has a timeout of 10s - no workaround is available.
-   Snap has a timeout property value implemented, but this is per
    image, and will not affect SRRF datasets.
-   When running a sequence acquisition with a Sona camera in Full frame
    and a high radiality magnification the resulting image can require
    too much memory to be handled by Micro-Manager using default
    settings. It is therefore required to update the size of the
    Sequence Buffer. This is found under Tools/Options. We recommend
    using a size of 512MB instead of the default 250MB.
-   If you encounter errors related to the system being out of memory
    when acquiring large data samples especially with a Sona camera, you
    can increase ImageJ's Maximum Memory from 2000MB to 4000MB. The
    option is found in the ImageJ window under Edit/Options/Memory &
    Threads. (you can find more information on this parameter and its
    limitations
    [here](Micro-Manager_Configuration_Guide#Memory_Settings "wikilink"))
-   SRRF computation time increases with frame size therefore the larger
    the camera frame and the higher the radiality magnification are, the
    more time will be required for the computer to process the SRRF
    frame. As a result, when using a Sona camera, using Internal Trigger
    (the default trigger mode) or External Trigger with low exposure
    times and/or low trigger delays can result in the camera acquiring
    frames faster than the computer can handle. Eventually this
    situation may lead to a camera buffer overflow error indicating that
    the buffer on the camera head is full and can’t store any more
    frames forcing the camera to stop the acquisition. This can be
    solved by changing acquisition settings:
    -   The easiest solution when using Internal Trigger is to switch to
        Software Trigger which will ensure that the camera acquires
        frames at a rate sustainable by the computer. This solution
        however incurs a small overhead and will therefore not provide
        the best frame rate.
    -   A more advanced solution is to increase the delay between
        triggers of the triggering device (when using External Trigger)
        or to decrease the camera frame rate (when using Internal
        Trigger). This solution has the advantage of being able to
        provide the best possible frame rate but requires a significant
        amount of work and may lead to occasional camera buffer
        overflows if the timings are not properly set.

  
For more information, see <http://www.andor.com/srrf-stream>