# BioImage Suite Web User Documentation

## Table Of Contents

* [Starting BioImage Suite Web](#starting_bioimage_suite_web) -- how to get and run the software.
* [Some Key Information](#Some_Key_Information) -- information about configuring your browser and default image orientations.
* [The Orthogonal Viewer Application](#The_Orthogonal_Viewer_Application) -- the "first" application with an explanation of how the viewers work (including colormapping etc.)
* [The Overlay Viewer Application](#the_overlay_viewer_application) -- an application optimized for displaying functional overlays.

__Note:__ This document and those linked to it contain the beginnings of the user documentation for [BioImage Suite Web](https://bioimagesuiteweb.github.io/webapp/). A brief introduction to the software can be found in this [presentation](https://bioimagesuiteweb.github.io/webapp/images/BioImageSuiteWeb_NIHBrainInitiativeMeeting_April2018.pdf). If you are looking for developer documentation, this may be found in [the doc directory of the source repository](https://github.com/bioimagesuiteweb/bisweb/tree/master/doc). _This is work in progress._

---

### Starting BioImage Suite Web

BioImage Suite Web consists of three major components

* [The web applications](https://bioimagesuiteweb.github.io/webapp/) which directly run in your browser with no installation required.
* Desktop applications using [Electron](https://electronjs.org/) which may be downloaded from our [download page](http://bisweb.yale.edu/binaries/binaries.html)
* Command line applications which may also be downloaded [from our download page](http://bisweb.yale.edu/binaries/binaries.html). This require a recent version of [Node.js](https://nodejs.org/en/). We recommend v 8.9 or later (but not 9 or 10).

![Introduction Page](images/welcome.png)

BioImage Suite Web consists of a collection of applications (which is likely to grow over time.) The list can be accessed under the Applications menu (as shown) and snapshots and brief descriptions of each application can be seen in the carousel (slide show) at the top of the page.

From the menu you can also navigate to the downloads page, the documentation and the source code repository.

---

## Some Key Information

### Download File Location

When using BioImage Suite Web in a web browser all save operations are implemented as download operations, i.e the software creates the data output and initiates a download event. By default most browsers send all downloads to your Downloads directory which is completely unsuitable for using BioImage Suite Web as an analysis software. We recommend going under Settings in your favorite browser as shown below for Chrome:

![Chrome Download Settings](images/chromesettings.png)

You need to turn the option `Ask where to save each file before downloading` to `ON`.

For Safari on MacOS see the [description on this web page](https://apple.stackexchange.com/questions/264594/prevent-safari-10-x-from-auto-downloading-files).

### Image Orientations

The Viewers and commandline tools can load images in the [NIFTI-1](https://nifti.nimh.nih.gov/) `.nii.gz` format. A key component of the image is the image orientation. This relates the internal image coordinates to "world" coordinate space.

![Image Orientation](images/image_orientation.png)

If we consider a 3-dimensional image matrix `F(i,j,k)` where `i`,`j` and `k` are the coordinate axes in the images where `i,j` are the in-plane directions and `k` is the slice axis. For example in the image shown above for Axial images, `i` is often Left->Right, `j` is Posterior->Anterior. The slice axis `k` is often Inferior->Superior. Such an image is described as having orientation __RAS__ where the letters stand for the direction of the individual axes i.e

* __R:__ i-axis to the RIGHT
* __A:__ j-axis to the ANTERIOR
* __S:__ k-axis to the SUPERIOR

RAS is probably the most common orientation for Neuroimaging research. An alternative orientation that is commonly used (and which the legacy BioImage Suite used) is `LPS` which is 180 degrees rotated w.r.t. RAS (flip i and flip j).

There are 48 (!) possible combinations of orientations. BioImage Suite Web can display all of these (at least as far as we have tested) but also provides the user with the option of converting images `on-load` to RAS or LPS to standardize. Under the Help menu if you select the option `Set Image Orientation on Load` the following GUI appears.

![Image Orientation on Load](images/setorientationonload.png)

If you select either RAS or LPS then any image load will be repermuted to be in RAS or LPS orientation on load. The settings are stored either in the Browser Database or the text file ${HOME}/.bisweb for commandline and Desktop applications. This is a JSON key-value database file that may look something likes this:

![The Settings File](images/settings.png)

In this case "orientationOnLoad" is set to "None" which preserves the image orientation as is.

---

## The Orthogonal Viewer Application

All BioImage Suite web applications share components and have a similar user interface. The picture below shows the `Orthogonal Viewer Tool`. This viewer consists of a single viewer plus some controls. All viewers in BioImage Suite Web can display two images:

1. The underlay "image" -- this is often the anatomical image and be loaded and saved from the `Image` Menu.
2. The "overlay" or "objectmap" image -- this is often a functional image or a segmentation image. This can be loaded and saved from the `Overlay` menu.



![An Application ](images/viewer.png)

The application consists of the following parts:

* A. The Menu Bar -- this provides access to all algorithmic functionality in the application. 
    * `Image` -- functionality for loading and saving the underlay anatomical image
    * `Overlay` -- functionality for loading and saving (and clearing) the overlay functional image. 
    * `Edit' -- typically contains Undo and Redo functionality for image manipulation operations and tools to move images from overlay to image etc.
    * `Image Processing` -- this contains the image processing tools.
    * `Segmentation` -- this contains more modules to perform image segmentation. In the `Dual Viewer` application there is also a `Registration` menu that contains the image registration tools.
    * `Display` -- in this single viewer, this simply has an option to display information about the currently display image. In the `Dual Viewer` application there are additional options to set the relative size of the two viewers.
    * `Help` -- this contains the usual `About this Application` option plus options for setting user preferences.

* B. The Viewer (one application has two viewers). This can display the two images in either single slice or three-linked slice views. There is also a viewer component (see `Overlay Tool`) which displays multiple parallel sections of the same image.

* C. The image information under the cursor. As you click in the image, the current coordinates (i,j,k) of the image and the current intensity of the image (and the overlay if present) are shown here.

* D. The side panel containing viewer controls. 

* E. The `Viewer Controls` which allow the user to control how the image is displayed. 
    * `Mode` -- this selects single slice or three orthogonal slice view.
    * The `I-Coord`, `J-Coord`, `K-Coord` sliders select the `i,j,k` coordinates of the viewer crosshairs.
    * The `Labels` toggle shows and hides labels in the viewer (all text and lines.)
    * The `Disable Mouse` toggle locks the viewer from user mouse input. The cross-hairs may only be changed using the `I,J,K-coord` sliders.
    * The `Reset Slices` rests the viewer to default 'zooms'.
    * The `Z-` and `Z+` buttons perform zoom in and out operations. You may also zoom using the mouse wheel in the usual way.
    * The `?` button shows the current image information ('See H'). 

* F. In the case of a 4D image, there will be extra controls in the `Viewer Controls`. This include the `Frame` slider for slecting the frame and the `Movie` controls for playing a movie and setting the framerate.

* G. The image color-mapping controls. This set the windowing for the anatomical image. Values below 'Min Int' are to black (and also fully transparent) and intensities above 'Max Int' are saturated to white. The `Interpolate` flag can be used to allow WebGL interpolation or not (smoother images vs being able to see the actual voxels). Finally the `Auto-Contrast` toggle enables automatic windowing if this is desired. If there is a funtional image loaded, an additional set of controls called `Overlap Color Mapping` will appear. More on this below.

* I. This is the viewer snapshot tool. It can be used to save a snapshot of the current viewer in a png file. The three sub controls are:

*  `Scale` -- sets the size of the image in voxels relative to the size of the viewer. For publication quality set this to 'x5' (five times) or higher.
*  `White Bkgd` -- sets the viewer background to white instead of black.
* `Crop` -- if turned on automatically crops empty space in the viewer to give a more pleasing snapshot.
* `Take Snapshot` -- this actually invokes the code to acquire a snapshot.

* J. The `_` button at the top right of the sidebar can be used to minimize and restore the sidebar.

---

### The Overlay Viewer Application

All viewers can display overlays. The `Overlay Viewer` is particularly optimized for this task. This is shown below.

![The Overlay Viewer](images/overlayviewer.png)

This is a dual viewer that shows functional overlays in both an `Orthogonal` (three orthogonal slice viewer shown above) and a `Mosaic` (multiple parallel slices -- see below) viewer which are synchronized to have the same color mapping scheme.

To try this out, open the application from the main BioImage Suite web page (under `Applications| Overlay Viewer`) and then under `Help`, select `Load Sample Data`. This will load a sample anatomical/functional image pair. (You may load your own images using `Image|Load Image` and `Overlay|Load Overlay`. As discussed above, once an overlay image is loaded, the `Viewer Controls` have an additional set of controls labeled `Overlay Color Mapping` (shown on the right). The controls here perform the following tasks:

* `Opacity` - the relative opacity for 0 (completely transparent) to 1 (fully opaque). Use this to partially show the anatomy under the functional map if desired.
* `Overlay Type` -- the overlay can be displayed using a number of different color maps. These are
    * `Objectmap` -- this is used for displaying sementation objectmaps. The overlay is rendered using a rainbow-like lookup table.
    *  `Overlay` and `Overlay2` -- these are slightly different variants of colormaps used to display functional images. The mapping (explicitly shown in the colorscale in the viewer -- bottom right -- is performed as follows):
        * If `Overlay Show` is set to `Both` both positive and negative values are shown otherwise either only positive or only negative values are shown.
        * `Min Overlay` : parts of the image whose intensity is below this (in an absolute sense) is displayed in a completely transparent color (not shown effectively).
        * `Max Overlay` : values above these are saturated.
        * `Cluster Size` : if this is greater than 0 then cluster filtering is performed to eliminate `small` blobs.
    * `Red`, `Green`, `Blue`, `Orange`, `Gray` -- this display the image using an anatomical style mapping. This is useful for overlaying two anatomical images to check registration results etc. In this setting, no clustering is performed and the colorscale is hidden.

This viewer can also be switched to `Mosaic` view by clicking the `Mosaic` Tab (just below the menu).

![Mosaic Mode for Overlay Viewer](images/mosaic.png)

This shows multiple parallel slices of a particular orientation (selected using `Plane`). You may set the number of rows and columns, the first slice and increment (which may be negative). The colormapping controls are identical to the orthogonal (3-slice view) and is synchronized between the `Orthogonal` and `Mosaic` tabs.


