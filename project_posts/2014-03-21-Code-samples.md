## Sample of current draw in visualization class:

	if (bDraw)
	{
		// Draw Volume
		ofSetColor(255);
		cam.begin();
			myVolume.updateVolume(volPos, volSize, 0);
		// check collision
		if (bSelecting){
			doesIntersect = myVolume.getIntersection(&cam, intersectionPosition);
			if (doesIntersect) {
				updateVolume2Slices();
				updateCoordinates();
				updateSlicesImage();
			}
		}
		cam.end();
		myVolume.draw(0, ofGetHeight(), ofGetWidth(), -ofGetHeight());
		
		// Draw ArcBall
		if (!bSelecting && ofGetMousePressed()) cam.drawArcBall();
		
		//Draw Slices canvas
		ofPushView();
		ofTranslate(initX, initY);
		ofPushStyle();
			ofSetColor(OFX_UI_COLOR_BACK);
			ofRect(0, 0, boxW+dist*3, (boxW+dist)*3+dist);
		ofPopStyle();
		
		//Draw Slices
		ofPushView();
		ofTranslate(dist, dist);
		volume2D.draw(CORONAL);
		
		ofPushView();
		ofTranslate( 0, boxH+ dist);
		volume2D.draw(SAGITTAL);
		
		ofPushView();
		ofTranslate( 0, boxH+ dist);
		volume2D.draw(AXIAL);
		
		ofPopView();
		ofPopView();
		ofPopView();
		ofPopView();
		
		//Draw talairach pixel value and labels
		ofPushStyle();
	//		ofSetColor(voxelValue, 255);
	//		ofRect(initX,tempY,boxH*2+dist*5,dist);
		
		ofSetColor(0, 255, 255);
		ofDrawBitmapString("Talairarch coordinate :", talDrawX, talDrawY);
		string str= "x= "+ ofToString(talCoord.x)+" y= "+ ofToString(talCoord.y)+" z= "+ ofToString(talCoord.z);
		ofDrawBitmapString(str, talDrawX, talDrawY+dist);
		for (int i=0; i<outputLabels.size()-2; i++) {
			vector<string> items = ofSplitString(outputLabels[i+2], ",");
				for (int j=0; j<items.size(); j++) {
					ofDrawBitmapString(items[j], talDrawX, talDrawY+i*dist+j*dist+(dist*2));
				}
		}
		ofPopStyle();
	}