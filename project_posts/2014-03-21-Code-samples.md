#Code samples

The following are the main parts of the current application.
We decided to explain what is doing each class instead of commenting the code per line.

###Own code

#####VizManager
This class handles the visualization. It has access to the volume, the volume rendering and the GUI that allows to select a point in the volume. It can do conversions from volume space (volume width/height/depth) to OpenGL space (usually normalized) and to the GUI coordinate space(normalized). 
It also can get the position of the mouse to know where are you pointing on the volume (by using ofxRay).

these are some of the objects included:
	
	//All Coordinates
	ofVec3f	uiRange;	// maximum and minimum values for UIs
	ofVec3f uiCoord;	// NORMALISED coordinates used in GUI (floats from -1 to 1)
	ofVec3f volCoord;	// coordinates in voxels (integers from 0 to volWidth..)
						// needed to draw the image on position
	ofVec3f uiClamp;	// same as ui but using values only inside volume
	ofVec3f talOffset;	// the offset of the origin (0,0,0) in Tal coordinates
	ofVec3f talCoord;	// volume coords + offset Tal coords for Tal tables.


#####ofxVolumeSlice
This class loads a volume dataset (by loading a set of tiff images) and computes 3 images representing the 3 sections of the brain. In medical tradition those cuts are called Coronal (the one on top) Saggital (middle) and axial (bottom). every time the user selects a poin by clicking on the image the GUI will display the according image slice corresponding to the current selected point of the volume.

These are the objects that handle the cuts:

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

And these are the methods to get the desired information about the voxel:

	int getVoxelValue();
	int getVoxelNumber();

#####ofxTalairach
This class is currently offering information about the selected voxel. We want to konw what brain region is included on each voxel. To do that we have loaded a volume that instead of intensity values contains a number that corresponds to a table with labels.
you can find more information about the talairach brain [here](http://www.talairach.org)
![talairach_brain](../project_images/talairach_brain.png?raw=true "talairach_brain")

#####tabManager
We have done a trick here to simulate a tab. Since ofxUI is not oofering tabs we are drawing buttons in different states to simulate a tabbed canvas.

#####googleManager
Here we handle all communication with the google API. for now we have plugged a twitter reader because we had some code from a previous project. But here is where Google API will be living.

###External code
Using most of the Openframeworks goodies :) 
We are relying in the libary which is supported by a large community.

#####ofEasyCam
Used to move the camera around the brain

#####ofxVolumetrics
Used to render the brain as a volume and cut it at any level
It has been modified to allow cuts at any angle

#####ofxSuperlog
Used to keep track of events for a good debugging

#####ofxUI
Used to render the GUI, these

#####ofxCameraSaveLoad
Used to save and load the current state of the camera

#####ofxJSON
Used to parse the responses from Google API

#####ofxXmlSettings
Used to save UI settings

#####ofxOauth
Used to communicate with Twitter (in the future if will be replaced by Google)

#####ofxTwitter
Used to communicate with Twitter (in the future if will be replaced by Google)

#####ofxFTGL
Used to render fonts from any language

#####ofxRay
Used to select points in the space with the mouse.
























