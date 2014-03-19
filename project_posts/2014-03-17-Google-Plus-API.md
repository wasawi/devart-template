## Google + Documentation and Retrieval Test with Python

There is no straightforward implementation of Google+ API available, we have to use Python Scripting. 
The installation procedure for the Google + API various from one machine to another depending on the package manager that you are using. But, here is our steps:



Step 1: We create a Google APIs Console project, authentication access with OAuth 2.0 which gives us the client ID and client secret following the steps in this link:

 https://developers.google.com/+/quickstart/python

Step 2: We installed Python using Homebrew:

```
 $ brew install python
```
 Google + API requires Pip. Pip comes with the Homebrew installation but if you use anothe package manager:

 Download pip at, http://pip.readthedocs.org/en/latest/installing.html.
 
 Create a file named get-pip.py with its contents and then run:

```
 $ sudo python get-pip.py
```
Step 3: Set up the Python quick-start app

 The terminal commands below clones the Google+ application repository using git and decompresses it to your harddrive.
```
 $ git clone https://github.com/googleplus/gplus-quickstart-python.git
 $ wget https://github.com/googleplus/gplus-quickstart-python/archive/master.zip
 $ unzip gplus-quickstart-python-master.zip
 $ cd gplus-quickstart-python
 $ pip install -r requirements.txt
```
 Go to the directory with the sample app and install the requirements of this quick start
```
 $ cd gplus-quickstart-python
 $ pip install -r requirements.txt
```

 Go to your clone G+ application repository and edit client_secrets.json, and replace YOUR_CLIENT_ID and YOUR_CLIENT_SECRET with the values that you generated in Step 1.

Step 4: Run the Python quick-start app:

```
 $ python signin.py
```

 Browse to your quick-start app, which by default is at:

 http://localhost:4567

 You should see a similar page confirmation in your browser:





![G+ connection confirmation](../project_images/Gplus_connected.png?raw=true "G+ connection confirmation")

