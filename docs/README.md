## Table Of Contents

* [Starting BioImage Suite Web](#starting-bioimage-suite-web) — how to get and run the software.
* [Some Key Information](#some-key-information) — information about configuring your browser and default image orientations.
* [The Orthogonal Viewer Application](#the-orthogonal-viewer-application) — the "first" application with an explanation of how the viewers work, including colormapping etc.
* [The Overlay Viewer Application](#the-overlay-viewer-application) — an application optimized for displaying functional overlays.
* [The Image Editor Application](#image-editor) — an application that can be used for interactive segmentation and VOI analysis of images.

__Note:__ This document and those linked to it contain the beginnings of the user documentation for [BioImage Suite Web](https://bioimagesuiteweb.github.io/webapp/). A brief introduction to the software can be found in this [presentation](https://bioimagesuiteweb.github.io/webapp/images/BioImageSuiteWeb_NIHBrainInitiativeMeeting_April2018.pdf). If you are looking for developer documentation, this may be found in [the doc directory of the source repository](https://github.com/bioimagesuiteweb/bisweb/tree/master/docs).

_This document represents work in progress._

---

### Starting BioImage Suite Web

BioImage Suite Web has three major components:

* [The web application](https://bioimagesuiteweb.github.io/webapp/) 
    * runs in your browser — no installation required!
* The desktop application using [Electron](https://electronjs.org/)
     * may be downloaded from the [download page](http://bisweb.yale.edu/binaries/binaries.html)
* [Command line applications](CommandLineTools.md) 
    * may also be downloaded [from the download page](http://bisweb.yale.edu/binaries/binaries.html). 
    * requires a recent version of [Node.js](https://nodejs.org/en/).  8.9 or later is recommended (but not 9 or 10).

![Introduction Page](images/welcome.png)
This is the main page at [https://bioimagesuiteweb.github.io/webapp/](https://bioimagesuiteweb.github.io/webapp/)

BioImage Suite Web is a collection of applications that is likely to grow over time. The list can be accessed under the Applications menu as shown above, and snapshots and brief descriptions of each application can be seen in the slide show in the center of the page.

From the menu you can also navigate to the downloads page, the documentation and the source code repository.

---

## Some Key Information

### Download File Location

Most browsers send all downloads to the Downloads directory, which may be inconvenient when trying to manage your data. It is recommended to change this before attempting any analysis in Bio Image Suite.

#### Chrome

![Chrome Download Settings](images/chromesettings.png)

Click the triple dot icon at the top-right of the page, directly under the minimize/maximize/close window buttons and to the right of the navigation bar and select 'Settings'.

Turn the option `Ask where to save each file before downloading` to `ON`.

#### Safari 
See the [description on this web page](https://apple.stackexchange.com/questions/264594/prevent-safari-10-x-from-auto-downloading-files).

### Image Orientations

The Viewers and command line tools can load images in the [NIFTI-1](https://nifti.nimh.nih.gov/) `.nii.gz` format.

 A key component of the image is the image orientation. This relates the internal image coordinates to "world" coordinate space.

![Image Orientation](images/image_orientation.png)

Consider a 3-dimensional image matrix `F(i,j,k)` where `i`, `j` and `k` are the coordinate axes in the images where `i,j` are the in-plane directions and `k` is the slice axis. For example in the image shown above for Axial images, `i` is often Left->Right, `j` is Posterior->Anterior. The slice axis `k` is often Inferior->Superior. Such an image is described as having orientation __RAS__ where the letters stand for the direction of the individual axes i.e

* __R:__ i-axis to the RIGHT
* __A:__ j-axis to the ANTERIOR
* __S:__ k-axis to the SUPERIOR

RAS is probably the most common orientation for Neuroimaging research. An alternative orientation that is commonly used (and which the legacy BioImage Suite used) is `LPS` which is 180 degrees rotated w.r.t. RAS (flip i and flip j).

There are 48 (!) possible combinations of orientations. BioImage Suite Web can display all of these, but also provides the user with the option of converting images to RAS or LPS to standardize. Under the Help menu, if you select the option `Set Image Orientation on Load`, the following GUI will appear.

![Image Orientation on Load](images/setorientationonload.png)

If you select either RAS or LPS then any image load will be repermuted to be in RAS or LPS orientation on load. The settings are stored either in the Browser Database or the text file ``${HOME}/.bisweb`` for commandline and Desktop applications. This is a ``.JSON`` key-value database file that may look something likes this:

![The Settings File](images/settings.png)

In this case ``orientationOnLoad`` is set to ``None``, which means the image's orientation will not be changed.

---

## The Orthogonal Viewer Application

All BioImage Suite web applications share components and have similar user interfaces. The picture below shows the `Orthogonal Viewer Tool`, which  consists of a single viewer plus some controls. All viewers in BioImage Suite Web can display two images:

1. The underlay — typically this is often the anatomical image and be loaded and saved from the `Image` Menu.
2. The overlay or "objectmap" — typically a functional image or a segmentation image. This can be loaded and saved from the `Overlay` menu.



![An Application ](images/viewer.png)

The application consists of the following parts:

* A. The Menu Bar — Provides access to all algorithmic functionality in the application. Contains the following tabs:
    * `Image` — Loads and saves the underlay.
    * `Overlay` — Loads, saves, and clears the overlay. 
    * `Edit` — Various tools to manipulate images in the viewers, including  undo, redo, functionality for image manipulation operations, tools to move images from overlay to image, and more.
    * `Image Processing` — Contains image processing functions like smoothing, thresholding, etc.
    * `Segmentation` — Contains image segmentation functions like masking, morphological filtering, and segmentation itself. The `Dual Viewer` application also contains a `Registration` menu that contains the image registration tools.
    * `Display` — In a single viewer, this simply displays information about the current image. In the `Dual Viewer` application there are additional options to set the relative size of the two viewers.
    * `Help` — Contains the usual `About this Application` option plus options for setting user preferences.

* B. The Viewer — This can display the two images in either single slice or three-linked slice views. There is also a viewer component (see `Overlay Tool`) which displays multiple parallel sections of the same image. Note that some applications have multiple viewers.

* C. The image information under the cursor. Displays the current coordinates (__i__, __j__, __k__) of the image, the current intensity of the image, and information about the overlay if one is present.

* D. The side panel containing viewer controls. 

* E. Viewer Controls — Allows the user to control how the image is displayed. 
    * `Mode` — Selects single slice or three orthogonal slice view.
    * `I-Coord`, `J-Coord`, `K-Coord` sliders — Select the `i,j,k` coordinates of the viewer crosshairs.
    * `Labels` toggle — Shows and hides labels in the viewer (all text and lines.)
    * `Disable Mouse` toggle — Locks the viewer from user mouse input. When this option is on, cross-hairs may only be changed using the `I, J, and K-coord` sliders.
    * `Reset Slices` button — Resets the viewer to default zooms.
    * `Z-` and `Z+` buttons — Perform zoom in and out operations. You may also zoom using the mouse wheel.
    * `?` button — Shows the current image information ('See H'). 

* F. In the case of a 4D image, there will be extra controls in the `Viewer Controls`. This include the `Frame` slider for slecting the frame and the `Movie` controls for playing a movie and setting the framerate.

* G. Image color-mapping controls — Sets the windowing for the anatomical image. Intensities below `Min Int` are set black and fully transparent while intensities above `Max Int` are saturated to white. The `Interpolate` flag can be used to allow WebGL interpolation or not (smoother images vs being able to see the actual voxels). The `Auto-Contrast` toggle enables automatic windowing if this is desired. If there is a funtional image loaded, an additional set of controls called `Overlap Color Mapping` will appear, see [the section below](#the-overlay-viewer-application).

* I. The viewer snapshot tool — Save a snapshot of the current viewer in a `.png` file. The three sub controls are:
    *  `Scale` — Sets the size of the image in voxels relative to the size of the viewer. For publication quality set this to '5x' or higher.
    *  `White Bkgd` — Sets the viewer background to white instead of black.
    * `Crop` — If turned on, automatically crops empty space in the viewer to give a nicer looking snapshot.
    * `Take Snapshot` — Takes a snapshot.

* J. The `_` button — Minimizes the sidebar.

---

### The Overlay Viewer Application

All viewers can display overlays, but the `Overlay Viewer` is particularly suited for the task. 

![The Overlay Viewer](images/overlayviewer.png)

The overlay viewer can show functional in both an `Orthogonal` and `Mosaic` view, the first which is shown above and the second at the end of this section. Both views are synchronized to have the same color mapping scheme.

To try this out, open the application from the main BioImage Suite web page under `Applications| Overlay Viewer`, and then under `Help`, select `Load Sample Data`. This will load a sample anatomical/functional image pair. You may load your own images using `Image|Load Image` and `Overlay|Load Overlay`. Once an overlay image is loaded, the `Viewer Controls` will display an additional set of controls labeled `Overlay Color Mapping`, which perform the following tasks:

* `Opacity` — The relative opacity of the overlay, from 0 (completely transparent) to 1 (fully opaque). 
* `Overlay Type` — The overlay can be displayed using a number of different color maps.
    * `Objectmap` — Used for displaying sementation objectmaps. The overlay is rendered using a rainbow-like lookup table.
    * `Overlay` and `Overlay2` — Slightly different variants of colormaps used to display functional images. The mapping is performed as follows:
        * `Overlay Show` — If set to `Both`, both positive and negative values are shown; otherwise, only one of positive or negative is shown.
        * `Min Overlay` — Lower intensity threshold. Parts of the image with intensity values below this value will be removed from the image (made completely transparent).
        * `Max Overlay` — Upper intensity threshold. Parts of the image with intensity values above this value will be saturated.
        * `Cluster Size` — If this is greater than 0, cluster filtering is performed to eliminate small blobs.
    * `Red`, `Green`, `Blue`, `Orange`, `Gray` — Displays the image using an anatomical style mapping. This is useful for overlaying two anatomical images to check registration results, etc. In this setting, no clustering is performed and the colorscale is hidden.

This viewer can also be switched to `Mosaic` view by clicking the `Mosaic` Tab just below the menu.

![Mosaic Mode for Overlay Viewer](images/mosaic.png)

This shows multiple parallel slices of a particular orientation selected using `Plane`. You may set the number of rows and columns, the first slice, and increment. The colormapping controls are identical to the orthogonal (3-slice) view and are synchronized between the `Orthogonal` and `Mosaic` tabs.

---
## Image Editor


#### Introduction

![The Image Editor Tool](images/imageeditor.png)

The Image Editor tool is designed to create and visualize interactive segmentations, as well as to correct existing segmentations (e.g. by performing skull stripping). This tool shares much of the functionality of the [The Orthogonal Viewer Application](#the-orthogonal-viewer-application) with the following additions:

* Overlays are explicitly labeled as Objectmaps, i.e. the value in this overlay image is explicitly a tag for a region
* The ability to edit the object maps using the Paint Tool.
* Provision of selected set of modules — Create Objectmap, Morphology Operations, Regularize Objectmap, and Mask Image — for modifying object maps.
* The integration of the VOI (`Volume-of-interest`) analysis tool, which uses the current objectmap to analyze the underlying data. This is useful if the data is a timeseries as opposed to a static image.

#### Creating an Objectmap

![Threshold Image](images/thresholdimage.png)

An objectmap is created in one of three ways:

* Load it from an existing binary file
* Create it by manually defining the regions using the `Paint Tool`
* Create it by thresholding the underlying image. The example above shows the use of the `Create Objectmap` tool (essentially a binary thresholding tool) to create the obejctmap.

#### Detailed Operations

![Image Editor Parts](images/imageeditor_parts.png)

Once an objectmap is in memory, it can displayed and manipulated using tools provided in the `Image Editor` Tool. The figure above highlights five different pieces of functionality as follows:

* A. Overlay color mapping: This assumes that the overlay is an objectmap hence the only display/color mapping option available is the `Opacity`. 
* B. Paint Tool: The core of the BioImageSuite Web interactive segmentation tools — it is essentially a "smart" paintbrush tool wherein the user selects a color and paints over the image to create/edit an objectmap.
The following is a brief description of the functionality included in this:
    * The `Enable` toggle. If this is `on` then the paint tool receives mouse input and uses it to paint over the image (i.e. edit the objectmap). If this is turned to `on` the paint tool is highlighted with a red background color as shown in the picture. 
    * The `Overwrite` toogle. If this is `on` then regions already defined may be erased by painting over them. If this is `off`, the paint tool will only paint where the objectmap is `zero` or `background`.
    * The `3D Brush` toggle. If this is `on` the painting is done with a brush that extends to multiple slices. Otherwise the image is colored only on the current slice. Note that if this is `off` the area selected will be different depending on which slice is painted.
    * The `Threshold` toggle. If this is on then the image is colored only if the intensity is between the `Min Threshold` and `Max Threshold`.
    * The `Connect` toggle. If `Threshold` is on then the paintbrush only fills in voxels between the thresholds and who are connected to the central voxel. Otherwise has no effect.
    * The `Brush Size` slider — Sets the brush size in voxels.
    * The Color bar `[0][1][2][3][4][5][6][..]`. Allows the user to select the color to paint. The `black` color selected by `[0]` is the eraser, provided that `Overwrite` is `on`.
    * The editor can also perform undo and redo operations using the `Undo` and `Redo` buttons.

C. The Morphology Operations Tool — Performs mathematical operations such as `erode`, `dilate`, `median`, and `connect` (seed connectivity from current cross-hairs) on binary objectmaps. If the objectmap contains multiple colors, they will be converted to a binary map.

D. The Regularize Objectmap Tool —  Performs Markov Random Field regularization to smooth manually painted regions. It was developed for the construction of the Yale Brodmann atlas image, which can be loaded under ``Obejctmap | Load Yale Brodmann Atlas``. The smoothing kernel can be adjusted to a desired value using the ``Smoothness``` slider.

E. The Mask Image Tool — Masks the underlying anatomical image with the objectmap to remove all parts of the image outside the mask. Setting `Inverse` to `On` reverses the behavior of the tool by masking everything _inside_ the mask. Before masking, the objectmap must be binarized by thresholding it using the threshold set using the `Threshold` slider.

![VOI Analysis](images/voianalysis.png)

Given an objectmap and a 4D image we can generate image timeseries plots as shown above using `Objectmap | VOI Analysis`. By default, the graph shows the average intensity in each region over time. There are five buttons at the bottom of this which perform the following operations:

* Plot VOI Values — The default operation. If the underlying anatomical image is 4D the result is a plot like the figure above. If it is a 3D image, then a bar chart is generated instead.

* Plot VOI Volumes — Creates a bar chart of VOI region volumes.

* Export as CSV — Outputs the data used in the plots as a comma-separated value file (``.CSV``) for import into Excel, Matlab etc. 

* Save Snaphot — Saves the current plot as a ``.png`` image file

* Close — Closes the VOI Timeseries plotter window.


