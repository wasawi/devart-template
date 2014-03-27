## Google+ API user`s post and activities retrieval test

*Note: Using Python with Google+ API is frustrating especially if you have Xcode and other Python math and science packages previously installed. We spend so much time troubleshooting until finally we just need to re-install everything in a freshly formatted Mac.

There is no real straightforward way to test Google+ API for fetching data, we have to go over several examples. For this project, we decided to use python scripting to later on integrate it with OpenFrameworks and three.js. 

The installation procedure for the Google + API various from one machine to another depending on the package manager that you are using. But, here is our steps:


* Step 1: We generated an API key through Google API Console which gives us the authentication access with OAuth 2.0 - the client ID and client secret. 

Point your browser to https://console.developers.google.com and it will take you to the login page of the API Console. 

In the list of services, find the Google+ API make sure that it is turned on:


![G+ connection](../project_images/Gplus_API_on.png?raw=true "G+ connection")

Clicking the API Access allowed us to create an OAuth 2.0 client ID:

![G+ OAuth](../project_images/Gplus_API_OAuth.png?raw=true "G+ OAuth")


* Step 2: We installed Python using Homebrew:

```
 $ brew install python
```
 Google + API requires Pip. Pip comes with the Homebrew installation, but if you are using another package manager, download pip at, http://pip.readthedocs.org/en/latest/installing.html. Create a file named get-pip.py with its contents, and then run:

```
 $ sudo python get-pip.py
```
 
Setuptools can be updated via Pip, without having to re-brew Python:

```
 $ pip install --upgrade setuptools
```
Similarly, Pip can be used to upgrade itself via:

```
 $ pip install --upgrade pip
```

 
* Step 3: Set up the Python quick-start app

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

* Step 4: Run the Python quick-start app:

```
 $ python signin.py
```

 Browse to your quick-start app, which by default is at:

 http://localhost:4567

 You should see a similar page confirmation in your browser:


![G+ connection confirmation](../project_images/Gplus_connected.png?raw=true "G+ connection confirmation")


## This is a simple command-line sample for the Google+ API that retrieves the list of the user's posts

First follow all the steps here:
https://developers.google.com/api-client-library/python/start/installation

Then create a new API key using google's console:

 https://console.developers.google.com/project/796723238762/apiui/credential  
 Client ID for native application  
 Redirect URIs: urn:ietf:wg:oauth:2.0:oob, http://localhost

Download the new client_secrets.json file and put it next to the plus.py file.
Assuming that the client_secrets.json file was edited and supplied with G+ client ID and client secret, run the python application (see code below) in the terminal:

![Users post bash](../project_images/Users_post_bash.png?raw=true "Users post bash")

Running this application will also open a web browser asking for user authentication:

![Users post authentication](../project_images/Users_post.png?raw=true "Users post authentication")

After accepting, you should see this page confirmation:

![Users post authentication](../project_images/Users_post_authentication.png?raw=true "Users post authentication")


##To get the query of the hashtag #dreamsprawler, we can then use a similar request command as:

https://developers.google.com/+/api/latest/activities/search
https://console.developers.google.com/project/796723238762/apiui/api/plus/method/plus.activities.search


```
GET https://www.googleapis.com/plus/v1/activities?query=%23Dreamsprawler&key={YOUR_API_KEY}
```

This retrieves list of data that can be extracted at Google+ (activities search results):

```
{ "kind": "plus#activityFeed",
 "etag": "\"7zD...................\"",
 "nextPageToken": "Ci4Iq............",
 "selfLink": "https://content.googleapis.com/plus/v1/activities?query=%23Dreamsprawler&key=..............",
 "title": "Google+ Activities Search Results",
 "updated": "2014-03-19T16:29:32.707Z",
 "items": [ {
   "kind": "plus#activity",
   "etag": "\"7zDxHg...............\"",
   "title": "#Dreamsprawler  In my dream, I was quite scared that the skin of my face is detached and a friend of...",
   "published": "2014-03-19T16:29:32.707Z",
   "updated": "2014-03-19T16:29:32.707Z",
   "id": "z12gc.....................",
   "url": "https://plus.google.com/110..........",
   "actor": { "id": "10................", "displayName": "D Sprawler","url": "https://plus.google.com/108.........",
    "image": { "url": "https://lh3.googleusercontent.com/.............."} },
    "verb": "post",
   "object": { "objectType": "note", "content": " <a rel=\"nofollow\" class=\"ot-hashtag\" href=\"https://plus.google.com/s/%23Dreamsprawler\">#Dreamsprawler</a>  In my dream, I was quite scared that the skin of my face is detached and a friend of mine helped me stitch it back. \ufeff", "url": "https://plus.google.com/.........................",
    "replies": {"totalItems": 0, "selfLink": "https://content.googleapis.com/plus/v1/activities/...../comments" },
    "plusoners": { "totalItems": 0, "selfLink": "https://content.googleapis.com/plus/v1/activities/...../people/plusoners" },
    "resharers": { "totalItems": 0, "selfLink": "https://content.googleapis.com/plus/v1/activities/......../people/resharers" } },
   "provider": { "title": "Google+" }, 
   "access": {"kind": "plus#acl", "description": "Public", 
   "items": [ { "type": "public" } ] 
   } } ] }
```


