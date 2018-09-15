[Back to main page](../index.html)

---

# The Connectivity Visualization Tool

This application is also described in [Shen et al, Nature Protocols 2017](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5526681/) -- see in particular Figure 6. It was initially created for the needs of work published in [Finn et al, Nature Neuroscience 2015](https://www.ncbi.nlm.nih.gov/pubmed/26457551) and [Rosenberg et al, Nature Neusocience 2016](https://www.ncbi.nlm.nih.gov/pubmed/26595653). The default parcellation used is from [ Shen at al, NeuroImage 2013](https://www.ncbi.nlm.nih.gov/pubmed/23747961) and is available for download from our [NITRC page](https://www.nitrc.org/frs/?group_id=51).


---

## Using the Application

To open the connectivitity visualization tool navigate to [https://bioimagesuiteweb.github.io/webapp/connviewer.html](https://bioimagesuiteweb.github.io/webapp/connviewer.html).

![The Connectivity Control](figures/conn1.png).

Once the application is opened, you will be presented with a view as shown in the figure above. The Shen 268 region parcellation (Shen et al 2013) is loaded and a panel showing a circle plot (top left), a 3D view (top right) and the linked slice viewer bottom is shown. 

This application can visualize two connectome matrices at once. These can be loaded as the `Positive` matrix and the `Negative` Matrix under the file menu. These should be binary files containing 1 or 0 and stored in .csv file (.txt also works but be careful). The program expects that the matrices are square and have the same dimensions as the underlying parcellation (e.g. 268x268 in the case of the Shen parcellation).

You may also select the [AAL atlas](http://neuro.imm.dtu.dk/wiki/Automated_Anatomical_Labeling) instead from the `Parcellations` menu.

## The Three Panels

![The 3D Panels](figures/conn1.1.png)

The default display shows three linked panels as follows.

* Panel A (bottom) -- the slice view. This is straightforward to understand.  Note, that like the rest of BioImage Suite Web, we follow the standard radiological convention, so in the axial and coronal views the left side of the brain is shown on the right of the image (see the annotations L and R in the image).  If you click in the slice views, the cross hairs you can navigate to different parts of the brain. The point 'clicked' is annotated just below the circles (just above and the right of the `A` in the figure) showing the node, the region and the MNI coordinates.

* Panel B -- The 3D `glass brain` view shows two brain surfaces (one for each hemisphere) slightly separated for better visualization. The default/initial view has the subject facing the screen (hence right is on the left) but can be changed using either by using the mouse or by using the options under the `View` menu (e.g. `Set 3D View to Top` will show the brain surfaces from the top). The cross hairs from the slice views are also shown in the 3D view.

* Panel C -- The Circle View. This is a more abstract visualization of the brain as a circle. The two half circles represent the two brain hemispheres (with the left semi-circle showing the right hemisphere, in standard radiological convention). The circles are color-coded in a rainbow-style coloring with each color representing a part of the brain (e.g. the Pre-frontal lobe is shown in red, the Temporal lobe is shown in Blue etc. as shown in the legent to the right of the circles).

Clicking any point on the circle or the slice views will syncronize the 2 views and also place the cross-hairs in the appropriate location the 3D view.


## Exploring the Application using the Sample Data

Under the `Help` menu select `Load Sample Data` as shown in the figure below

![Load Sample Data](figures/conn2.png)

The connectome matrices are shown under `A` (these are simply binary matrices with red dots showing the connections). The currently selected node (`B`) is shown by a line from the center of the circles to its location on the circle, and its location is also shown in the 2D slices and 3D view.

To visualize a connectivity pattern, one uses the controls in the `Connectivity Control` which appears on the far right of the viewer and shown magnigied in the figure above. The options here are:

1. The Filtering Controls. Given the number of edges in a connectome, it is impractal to visualize them all at the same time. The following controls enable the user to filter edges to highlight aspects of their data. An edge connects two nodes. It will be shown if at least one of the nodes satisfies the filtering criteria below.

* Mode -- this selectes the filtering mode which is one of
    * 'All' -- use all nodes
    * 'Single Node' -- only show edges that connect a specific node
    * 'Single Lobe' -- only show edges that have one connection in a single lobe
    * 'Single Network' -- only show edges that have at least one connection in a single network. (The Networks are as defined by Power et al, Neuron 2011)

* Node -- if the mode is `Single Node`, this control is used to specify the node.

* Lobe -- if the mode is `Single Lobe`, this control is used to specify the lobe.

* Network -- if the mode is `Single Network`, this control is used to specify the network.

* Degree Threshold -- If the mode is not `Single Node` this control is used to futher filter connections to have at least one node that has degree at least equal to this value. `Degree` is defined as the number of non-zero connections of the given node. For thresholding purposes, if two connectome matrices are loaded (a `positive` and a `negative` we use the sum of the two degrees)

* Lines to Draw -- this is one of `Both`, `Positive` or `Negative`. If `Positive` we will only show edges from the `Positive` Matrix, `Both` from both and `Negative` from the negtive `Matrix`.










