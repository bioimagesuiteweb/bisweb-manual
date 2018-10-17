## Displaying Images

All BioImage Suite web applications share components and have a similar user interface. All viewers in BioImage Suite Web can display two images:

1. The "underlay" or "background" image — This is often the anatomical image and can be loaded and saved from the `File` Menu.
2. The "overlay" or "objectmap" image — This is often a functional image or segmentation image. This can be loaded and saved from the `Overlay` menu.


![An Application ](images/viewer.png)
_Figure 1: The [Orthagonal Viewer Tool](https://bioimagesuiteweb.github.io/webapp/viewer.html)_

The application consists of the following parts:

* A. The Menu Bar — This provides access to all I/O and algorithmic functionality in the application. 
    * `File` — Functionality for loading and saving the underlay anatomical image
    * `Overlay` — Functionality for loading, saving, and clearing the overlay functional image. 
    * `Edit` — Typically contains Undo and Redo functionality for image manipulation operations and tools to move images from overlay to image, etc.
    * `Image Processing` — Standard image processing and maniuplations tools. Details can be found [here](./tools/imageprocessing.md).
    * `Segmentation` — Modules to perform image segmentation. Details can be found [here](./tools/segmentationtools.md).
    * `Registration` — Modules to perform image registration. Details can be found [here](./dualviewer.md) (scroll about halfway down the page, note that these tools are only available in the dual viewer).
    * `Help` — Contains the usual `About this Application` option plus options for setting user preferences.

* B. The Viewer can display the underlay and the overlay images in either single slice or three-linked slice views. There is also a viewer component which displays multiple parallel sections of the same image (see [Overlay Viewer](overlayviewer.md)). Pressing the orange arrows next to each view will show the next or previous slice. If the image is '4D' then movie controls will appear at the bottom of the screen.

* C. Information about the currently selected voxel. This includes the coordinates (i,j,k) of the image, the intensity of the image under the cursor, and the intensity of the overlay under the cursor if one is present. They are displayed in the format `(i,j,k) = itensity (overlay intensity)`

* D. The side panel containing viewer and algorithm functionality controls. 

* E & F. The `Viewer Controls` allow the user to control how the underlay and overlay images are displayed. Arrows on the left can be used to collapse or expand these controls as desired.
  * `Core` viewer controls: 
    * `Mode` — Selects single slice or three orthogonal slice view.
    * `I-Coord`, `J-Coord`, `K-Coord` — Select the `i,j,k` coordinates of the viewer crosshairs.
    * `Frame` — Selects the currently displayed image frame in the viewer. Only appears for 4D data.
    * `Labels` — Shows or hides labels in the viewer.
    * `Disable Mouse` — Locks the viewer from mouse input. The cross-hairs may only be changed using the `I,J,K-coord` sliders if enabled.
    * `Reset Slices` — Resets the viewer to default zoom.
    * `Z-` and `Z+` — Zooms the viewers in and out. You may also zoom using the mouse wheel in the usual way.
    * `?` — Shows the current image information (see H). 

  * `Movie` controls how to play the movie if 4D data is loaded:
    * `Frames/s` —Sets the movie frame rate in frames/second.
    * `Play Movie` — Toggle to enable movie playback of the data.

* G. `Image Color Mapping` adjusts the windowing of the background image.
    * `Min Int` — Intensity values below this value are set to black and made fully transparent.
    * `Max Int` — Intensity values above this value are saturated to white.
    * `Interpolate` — Whether or not to use WebGL interpolation or not. WebGL images will be smoother, but raw images will let you see the individual voxels.
    * `Auto-Contrast` — If enabled, this will set the windowing automatically.

* `Overlay Color Mapping` adjusts the overlay/functional image display properties. See the [Overlay Viewer Application](overlayviewer.md) for more details. Will only appear if an overlay is loaded.

* H. `Viewer Information` contains technical information about the image and the overlay, including the name, file format, dimensions, spacing, orientation, and underlying data type, e.g. `uchar`, `sshort`, `float32`. The arrow on the left side of the box will display an example script to convert a BioImage Suite Web image to the legacy BioImage Suite format.

* I. `Viewer Snapshot` tool. It can be used to save a snapshot of the current viewer in a `.png` file. The three sub controls are:
  *  `Scale` — Sets the size of the image in voxels relative to the size of the viewer. For publication quality set this to 'x5' (five times) or higher.
  *  `White Bkgd` — Sets the viewer background to white instead of black.
  * `Crop` — If turned on automatically crops empty space in the viewer to give a more pleasing snapshot.
  * `Take Snapshot` — Takes the picture.

* J. The double arrow icon at the top right of the sidebar can be used to minimize and restore the sidebar.

___

### 4D Images and Movie Display

![4D Overlay](images/4doverlay.png)
_Figure 2: An example of a 4D underlay image using a synthetic motion image._ 

The figure above shows the viewer displaying two images. The underlay image is a 4D image and the overlay is the average frame of the 4D image resampled to a lower resolution (for purposes of illustration). Take note of the following elements:

* A — The movie controls. When either under or overlay is a 4D image, the movie controls automatically appear. You can use these to manually advance or rewind the frame, play the movie, or pause the movie.

* B — Image information. This shows the intensity of both the image and the overlay under the cross-hairs. Since the images have different resolution, the coordinates are different, e.g. for the Image (`Img`) we get the value at (32,28,21,2) (frame = 2, all coordinates _including_ frame begin at zero), whereas for the lower resolution overlay (`Ovr`) we get the value at (24,21,14,0)  (the last number is capped to the number of frames in the overlay). Compare this to item `C` of the previous figure.

* C — The `Core` viewer controls with a `Frame` control. This allows us to set the 4th dimension of the image. While the range of the `I`,`J` and `K`-coord sliders correspond to the dimensions of the underlay image, the Frame slider has range equal to the maximum of the the number of frames in the two images.

* D — The `Movie` controls. This last set of controls allows us to set the frame rate at which a movie will play and provides a secondary means to start and stop the movie in addition to the controls in A.

![Image Information](images/4doverlay2.png)
_Figure 3: The viewer information popup from the `?` button_

If at any point, you are curious what images are being displayed and their characteristics, simply click on the `?` button under Viewer Controls as shown in the figure above. This will provide information about both images, including names, dimensions, voxel size, and orientation. The viewer information screen can make details about the image and overlay clearer, for example, it is easy to notice that the two images in the previous two figures have different resolution from the info screen (note the different dimensions).

