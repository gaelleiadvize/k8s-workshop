# Quickstart for Node.js in the App Engine standard environment

This is the sample application for the
[Quickstart for Node.js in the App Engine standard environment][tutorial]
tutorial found in the [Google App Engine Node.js standard environment][appengine]
documentation.

* [Setup](#setup)
* [Running locally](#running-locally)
* [Deploying to App Engine](#deploying-to-app-engine)
* [Running the tests](#running-test-version)

## Setup

Before you can run or deploy the sample, you need to do the following:

1.  Install dependencies:

            
            yarn install

## Running locally

with `yarn`:

    yarn start

## Deploying to App Engine

 At the root directory : 
 
   1 - Edit app.yaml & choose a name for the service
   
   2 - Deploy !
    
        gcloud app deploy
        
        
<p align="center">
<img src="https://i.giphy.com/d2Z9QYzA2aidiWn6.gif">
</p>
       

## Running test version

  At the root directory : 
        
            gcloud app deploy --no-promote   


[appengine]: https://cloud.google.com/appengine/docs/standard/nodejs
[tutorial]: https://cloud.google.com/appengine/docs/standard/nodejs/quickstart
