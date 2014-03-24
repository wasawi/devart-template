#Code Samples

The following are the main coding parts of the current application.
We decided to explain what is happening in each class instead of commenting the code line per line.

###Our code:

**VizManager**

This class handles the visualization. It has access to the volume, the volume rendering and the GUI that allows to select a point in the volume. It can do conversions from volume space (volume width/height/depth) to OpenGL space (usually normalized) and to the GUI coordinate space (normalized). 
It can also get the position of the mouse to know where are you pointing on the volume (by using ofxRay).

Here are some of the objects included in this class:
	
	//All Coordinates
	ofVec3f	uiRange;	// maximum and minimum values for UIs
	ofVec3f uiCoord;	// NORMALISED coordinates used in GUI (floats from -1 to 1)
	ofVec3f volCoord;	// coordinates in voxels (integers from 0 to volWidth..)
						// needed to draw the image on position
	ofVec3f uiClamp;	// same as ui but using values only inside volume
	ofVec3f talOffset;	// the offset of the origin (0,0,0) in Tal coordinates
	ofVec3f talCoord;	// volume coords + offset Tal coords for Tal tables.


**ofxVolumeSlice**

This class loads a volume dataset (by loading a set of tiff images) and computes 3 images representing the 3 sections of the brain. In medical tradition those cuts are called Coronal (the one on top) Saggital (middle) and axial (bottom). every time the user selects a point (done by clicking on the image) the GUI will display the according image slice corresponding to the current selected point of the volume.

Here are the objects that handle the cuts:

	//redreaw the volume images
	void redrawSagittal();
	void redrawAxial();
	void redrawCoronal();
	// the depth of the current slice
	int coronalS;
	int sagittalS;
	int axialS;
	// one image for each point of view
	ofImage coronal;
	ofImage sagittal;
	ofImage axial;
	// one pixel array for each image
	ofPixels coronalPixels;
	ofPixels sagittalPixels;
	ofPixels axialPixels;
![VolumeSlice_GUI](../project_images/VolumeSlice_GUI.png?raw=true "VolumeSlice_GUI")

And here are the methods to get the desired information about the voxel:

	int getVoxelValue();
	int getVoxelNumber();

**ofxTalairach**

This class is currently offering information about the selected voxel. We want to know what brain region is included on each voxel. To do that we are loading a volume without intensity values, instead, indices to tables with corresponding labels. For instance:

	0	*.*.*.*.*
	1	Left Cerebellum.Posterior Lobe.Inferior Semi-Lunar Lobule.Gray Matter.*
	2	Right Cerebellum.Posterior Lobe.Inferior Semi-Lunar Lobule.Gray Matter.*
	3	Left Cerebellum.Posterior Lobe.Cerebellar Tonsil.Gray Matter.*
	4	Right Cerebellum.Posterior Lobe.Cerebellar Tonsil.Gray Matter.*
	5	Left Brainstem.Medulla.*.*.*
	6	Right Brainstem.Medulla.*.*.*
	7	*.*.Inferior Temporal Gyrus.*.*
	8	Left Cerebrum.Temporal Lobe.Inferior Temporal Gyrus.Gray Matter.Brodmann area 20
	9	Left Cerebrum.Temporal Lobe.Inferior Temporal Gyrus.*.*
	10	Left Cerebrum.Temporal Lobe.*.*.*



you can find more information about the talairach brain [here](http://www.talairach.org)
![talairach_brain](../project_images/talairach_brain.png?raw=true "talairach_brain")

**tabManager**

We have done a trick here to simulate a tab. Since ofxUI is not offering tabs we are drawing buttons in different states to simulate a tabbed canvas.

**googleManager**

Here we are handling all communication with the google API. for now we are using a twitter reader for the sake of testing. But this class will handle the Google API calls in the future.

**External code**

Using most of the Openframeworks goodies.
We are relying in a library which is supported by a large community.

**ofEasyCam**

Moves the camera around the brain

**ofxVolumetrics**

Creates the render the brain as a volume and cut it at any level
It has been modified to allow cuts at any angle

**ofxSuperlog**

Keep track of events for a good debugging

**ofxUI**

Renders the GUI

**ofxCameraSaveLoad**

Saves and loads the current state of the camera

**ofxJSON**

Responsible for parsing the responses from Google API

**ofxXmlSettings**

Saves UI settings

**ofxOauth**

Communicates with Twitter (in the future if will be replaced by Google)

**ofxTwitter**

Communicates with Twitter (in the future if will be replaced by Google)

**ofxFTGL**

Render fonts from any language

**ofxRay**

Select points in the space with the mouse.
























