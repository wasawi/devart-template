## Google+ API content retrieval test

There is no straightforward implementation of Google+ API for fetching data, we decided to use Python Scripting. 

The installation procedure for the Google + API various from one machine to another depending on the package manager that you are using. But, here is our steps:


* Step 1: We generated an API key through Google API Console which give us the authentication access with OAuth 2.0 - the client ID and client secret. 

Point your browser to code.google.com/apis/console/ and it will take you to the login page of the API Console. 

In the list of services, find the Google+ API make sure that it is turned on:


![G+ connection](../project_images/Gplus_API_on.png?raw=true "G+ connection")

Clicking the API Access will allow you to create an OAuth 2.0 client ID:

![G+ OAuth](../project_images/Gplus_API_OAuth.png?raw=true "G+ OAuth")


* Step 2: We installed Python using Homebrew:

```
 $ brew install python
```
 Google + API requires Pip. Pip comes with the Homebrew installation but if you use another package manager, download pip at, http://pip.readthedocs.org/en/latest/installing.html. Create a file named get-pip.py with its contents and then run:

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


### This is a simple command-line sample for the Google+ API that retrieves the list of the user's posts

Run the python application (see code below) in the terminal (assuming that the client_secrets.json file was edited and supplied with G+ client ID and client secret):

![Users post bash](../project_images/Users_post_bash.png?raw=true "Users post bash")

Running this application will also open a web browser asking for user authentication:

![Users post authentication](../project_images/Users_post.png?raw=true "Users post authentication")

```
# WAM: This can be obtained at the Google+ API website, deeper into the links, but for 
# practicality and easy access, we are storing it here. 
# Copy-paste this code and save it with .py extension. Run it with an edited client_secrets.json on 
# the same directory
#
# !/usr/bin/env python
# -*- coding: utf-8 -*-
#
# Copyright (C) 2013 Google Inc.
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#      http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

"""Simple command-line sample for the Google+ API.

Command-line application that retrieves the list of the user's posts."""

__author__ = 'jcgregorio@google.com (Joe Gregorio)'

import sys

from oauth2client import client
from apiclient import sample_tools


def main(argv):
  # Authenticate and construct service.
  service, flags = sample_tools.init(
      argv, 'plus', 'v1', __doc__, __file__,
      scope='https://www.googleapis.com/auth/plus.me')

  try:
    person = service.people().get(userId='me').execute()

    print 'Got your ID: %s' % person['displayName']
    print
    print '%-40s -> %s' % ('[Activitity ID]', '[Title]')
    print

    # Don't execute the request until we reach the paging loop below.
    request = service.activities().list(
        userId=person['id'], collection='public')

    # Loop over every activity and print the ID and a short snippet of content.
    while request is not None:
      activities_doc = request.execute()
      for item in activities_doc.get('items', []):
        print '%-040s -> %s' % (item['id'], item ['title'])

    # WAM removed: item['object']['content'][:30]

      request = service.activities().list_next(request, activities_doc)

  except client.AccessTokenRefreshError:
    print ('The credentials have been revoked or expired, please re-run'
      'the application to re-authorize.')

if __name__ == '__main__':
  main(sys.argv)
```
To get the query of the hashtag #dreamsprawler, we can then use a similar request command:

```
GET https://www.googleapis.com/plus/v1/activities?query=%23Dreamsprawler&key={YOUR_API_KEY}
```

This retrieves list of data that can be extracted at Google+ (Google+ Activities Search Results):

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


