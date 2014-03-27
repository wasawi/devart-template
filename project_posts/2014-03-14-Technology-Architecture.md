## Technology Architecture

### Use case

People will start the application and log in to their Google+ account. 
Then people will be able to set some keywords in the search bar.
The brain will start populating with the dreams of people that contain those words.
The user is then able to look though the titles of the dreams on the brain and fine tune the search either by introducing more keywords or by selecting an area or region on the brain.
The user is also able to upload dreams containing text, images, sounds or videos. All these data will be uploaded at Google+ under the #dreamsprawler hashtag.

**Here are the main coding efforts:**
- Dreamsprawler application:
	- This is the client application that handles the visualization. The application for the user.
	- It also manages queries to Google+ API
	- Uses volume rendering (ofxVolumetrix) to display a real brain. (taken form Gallant Lab's dataset).
	- Uses ofxUI as a GUI to allow users to search and show posts on top of the visualization.
	- It also handles user interation on the volume so that people can select a precise area of the brain to fine tune a query.

- ofxGallant:
	- An addon to map words to the brain space.
	- We will write a wrapper for Openframeworks using Gallant Lab`s data correlations (www.gallantlab.org).
Currently Gallant database is used as a flat 2D space map wrapping the surface of a brain. The data is also provided with the volume (a nifti file) of the subjects brain where the correlations where created.
We will use the Volume as source for the visualization and the 3D-model of the map to deal with the interactions.

- ofxGoogle+:
	- An addon to handle Oauth2.0 Authintication.
	- It also handles queries to Google+ API
	- Addon will be written in Python and C++ as interface.

### Application requirements:
--------------------------------------------------------------------------------
		• We need full Unicode support in the application so that people can use any language to search, create or read posts.
		For this reason we will use ofxFTGL
		• We would like to offer browser tool too.

### TODO:
--------------------------------------------------------------------------------
		• callback from Google+ addon to fill scroll !
		• Talairach is will not map well, load nifti volume

### Achieved milestones:
--------------------------------------------------------------------------------
	ofxGoogle+
		√ get posts automatically (no key)

	ofxUI Improvements:
		√ draw gui slider from fbo (so that posts are not cut)
		√ implement ofxFTGL in ofxUI
		√ fix ofxFTGL emoji CRASH 
		√ Use variable binding in UI as in example (this reduce tons of code)

	ofxVolumetrix
		√ Get ofxRay to work
		√ Make selection in Volume

	Volume in 2Dslices
		√ 2D volume to look through the brain with saggital, coronal and axial cuts.
		√ draw slice planes in Volume and connect to VolumeSlicer
		√ coronal mirror coordinates, fixed!

	General:
		√ Filter mouse events. otherwise, we cannot controll where to click.
		√ enable/disable camera movements with key
		√ store camera matrices using Roy mcDonald's camerasaveLoad
		√ use ofxSuperLogger for logging actions


### BUGS
--------------------------------------------------------------------------------
		• GUI textInput only works on mouse over
		• fix coordinate systems and make sure volumes are loaded on the exact coordinates


### Diagram of information flow
--------------------------------------------------------------------------------
Below is a diagram describing the flow of information:

<img src="https://docs.google.com/drawings/d/1bihc5fLX7nLSxHqRrgZz9CodR5Uqk4YVInev_7imNFA/pub?w=960&amp;h=720">


