
## Loading Images

The Viewers and commandline tools can load images in the .nii.gz format. The
way images are loaded is affected by the user preference setting. This can
take one of three values 'None', 'RAS', 'LPS'

If None then the image is not repermuted
If LPS or RAS then the image is repermuted to LPS or RAS Axial orientations

The settings are stored either in the Browser Database or the text file
${HOME}/.bisweb for commandline and Desktop applications

## Viewers Image and Overlay

The viewers can display two images at a time, an underlay "anatomical" image
which is the main image and an overlay image ("functional" or segmentation
map). The main image determines the range of the slider range (i,j,k) of the
viewer and is displayed using a grayscale colormap with window and level
settings.

The overlay image (outside of the image editor) can be displayed using a
number of colormaps. Two of these are ("overlay" and "overlay2") are
explicitly meant to store functional maps and allow for cluster filtering. The
other colormaps are meant to show continuous images (in red, green, blue or
orange) colormaps in the same way as the anatomical images

In most viewers changing the underlay image to something of a different
dimension will clear the overlay image.

One can load/save the anatomical image using the "Image" menu (and "Image2"
menu in the case of dual viewers) and the functional image using the "Overlay"
menu (or "Overlay2").

### Image Display, Viewer settings and Colormaps

Three slices vs individual views

Colormaps etc.

### Screenshots

...



### Modules for Image Processing and Registration

* Input Image
* Output Image
* Parameters
  * Save/Load 
* Registration tools and matrices (Transformation Tool)

### Image Editor

* Paint Tool
* Morphology Tool
* Create Objectmap
* Regularize Objectmap
* Mask Image

### Connectivity Tool

* Parcellation
* Matrices
* MNI

### MNI 2 TAL

* Conversions
* Batch Mode


### Paravision Importer

* Process

### Command Line Tools

* Execution

