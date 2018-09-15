## Displaying Images

All BioImage Suite web applications share components and have a similar user interface. The picture below shows the [Orthogonal Viewer Tool](https://bioimagesuiteweb.github.io/webapp/viewer.html). This viewer consists of a single viewer plus some controls. All viewers in BioImage Suite Web can display two images:

1. The underlay "image" -- this is often the anatomical image and be loaded and saved from the `Image` Menu.
2. The "overlay" or "objectmap" image -- this is often a functional image or a segmentation image. This can be loaded and saved from the `Overlay` menu.



![An Application ](images/viewer.png)

The application consists of the following parts:

* A. The Menu Bar -- this provides access to all algorithmic functionality in the application. 
    * `File` -- functionality for loading and saving the underlay anatomical image
    * `Overlay` -- functionality for loading and saving (and clearing) the overlay functional image. 
    * `Edit' -- typically contains Undo and Redo functionality for image manipulation operations and tools to move images from overlay to image etc.
    * `Image Processing` -- this contains the image processing tools.
    * `Segmentation` -- this contains more modules to perform image segmentation. In the `Dual Viewer` application there is also a `Registration` menu that contains the image registration tools.
    * `Help` -- this contains the usual `About this Application` option plus options for setting user preferences.

We will discuss the tools in `Image Processing` and `Segmentation` in other documents.

* B. The Viewer (one application has two viewers). This can display the two images in either single slice or three-linked slice views. There is also a viewer component (see `Overlay Tool`) which displays multiple parallel sections of the same image. The orange arrows next to each slice view allow you to increment or decrement that slice as desired. If the image is '4D' movie controls will appear at the bottom of the screen.

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

* F. Expanded View of the Viewer Controls. In the case of a 4D image, there will be extra controls in the `Viewer Controls`. This include the `Frame` slider for slecting the frame and the `Movie` controls for playing a movie and setting the framerate.

* G. The image color-mapping controls. This set the windowing for the anatomical image. Values below 'Min Int' are to black (and also fully transparent) and intensities above 'Max Int' are saturated to white. The `Interpolate` flag can be used to allow WebGL interpolation or not (smoother images vs being able to see the actual voxels). Finally the `Auto-Contrast` toggle enables automatic windowing if this is desired. If there is a funtional image loaded, an additional set of controls called `Overlap Color Mapping` will appear. More on this below.

* I. This is the viewer snapshot tool. It can be used to save a snapshot of the current viewer in a png file. The three sub controls are:

*  `Scale` -- sets the size of the image in voxels relative to the size of the viewer. For publication quality set this to 'x5' (five times) or higher.
*  `White Bkgd` -- sets the viewer background to white instead of black.
* `Crop` -- if turned on automatically crops empty space in the viewer to give a more pleasing snapshot.
* `Take Snapshot` -- this actually invokes the code to acquire a snapshot.

* J. The "double arrow" button at the top right of the sidebar can be used to minimize and restore the sidebar.

---

### 4D Images and Movie Display

![4D Overlay](images/4doverlay.png)

The figure above shows the viewer displaying two images. The underlay image is a 4D image (once of our synthetic test motion images with exaggerated motion) and the overlay is the average frame of the 4D image resampled to a lower resolution (for illustration). Four things in particular from this figure are worth pointing out:

* A -- the movie controls. When either image (underlay or overlay) is a 4D image, the movie controls automatically appear. You can use these to either manually advance the frame, play a movie of step.

* B -- the image information in the viewer. This shows the intensity of both the image and the intensity under the cross-hairs. Since the images have different resolution, the coordinates are different, i.e. for the Image (`Img`) we get the value at (32,28,21,2) (frame =2, all coordinates _including_ frame begin at zero), whereas for the lower resolution overlay (`Ovr`) we get the value at (24,21,14,0)  (the last number is capped to the number of frames in the overlay). (Compare this to item `C` of the previous figure.)

* C -- in the viewer controls we now have a 'Frame/Comp' control. This allows us to set the 4th dimension of the cross hairs. While the range of the I,J and K-coord sliders correspond to the dimensions of the underlay image, the Frame slider, has range equal to the maximum of the the number of frames in the two images.

* D -- the movie controls. This last set of controls allows us to set the frame rate at which a movie will play and provides a secondary means to start/stop a movie in addition to the controls in A.

![Image Information](images/4doverlay2.png)

If at any point, you are curious (or have forgotten) what images are being displayed and their characteristics, simply click on the `?` button under Viewer Controls as shown in the figure above. This will provide information about both images (names, dimensions, voxel size, orientation etc.) It is easy, to notice, for example, that the two images in the previous two figures have different resolution.

