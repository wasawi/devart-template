# Using Google+ API with python
--------------------------------------------------------------
Installation:
#############


To set up Authentication access with Oauth
follow the steps here:
https://developers.google.com/+/quickstart/python

Our application at google console:
https://console.developers.google.com/project


At Step 2:
---------
download pip here
http://pip.readthedocs.org/en/latest/installing.html
create a file named get-pip.py with its contents and then run
sudo python get-pip.py

then run the step2.3
pip install -r requirements.txt

Step 3: Run the application
python signin.py
and go to:
http://localhost:4567

if you succeed you must see something like this at
![connected](connected.png?raw=true "connected")

--------------------------------------------------------------
create Posts:
#############

first get sample code at google python API:
https://developers.google.com/api-client-library/python/
$ pip install --upgrade google-api-python-client
