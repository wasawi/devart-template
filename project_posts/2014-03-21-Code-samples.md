#Code samples

The following are the main parts of the current application.
We decided to explain what is doing each class instead of commenting the code per line.

###Own code

#####VizManager
This class handles the visualization. It has access to the volume, the volume rendering and the GUI that allows to select a point in the volume. It can do conversions from volume space (volume width/height/depth) to OpenGL space (usually normalized) and to the GUI coordinate space(normalized). 
It also can get the position of the mouse to know where are you pointing on the volume (by using ofxRay) 

#####ofxVolumeSlice

#####ofxTalairach
#####tabManager
#####twitterManager


###External code

#####ofEasyCam
#####ofxVolumetrics
#####ofxSuperlog
#####ofxUI
#####ofxCameraSaveLoad
#####ofxJSON
#####ofxXmlSettings
#####ofxOauth
#####ofxTwitter
#####ofxFTGL
#####ofxRay
