1. Introduction
   In this module, we will learn how to make web-apps function offline using service workers.

2. Adding Service Workers

    typical Javascript runs on one single thread, attached to individual HTML pages.

    a service worker runs on a seperate thread, decoupled from HTML page.
    Manages ALL pages of given scope (e.g. all pages of the app)
    
    What is a service worker?
        a service worker can be seen as a proxy in between the app and the http requests of the back-end. which means it caches it, and then might allow it to continue.

    the terminal command to build a service worker in the CLI is: 

        ng add @angular/pwa
    
    this does many things to the app.

    First, it adds a <noscript> message telling the user to enable javascript to continue using the page.

    add @angular/pwa adds ServiceWorkerModule.register(), an import in the app.module @NgModule meta-data object. The first argument of the register method is a javascript file that doesn't exist, but will be created when the project is 'built', the second argument is an object that enables the creation of this .js file if envionment.production is true.


    while apps can be hosted using:

        ng serve --prod

    This won't generate a 'real' web-app, it will only build it in memory, and it will not properly utilize a service worker.
    To host a production app, you need an http server. To do that, you can easily install a light-weight node server with:

        npm install -g http-server
    
    then navigate into the dist folder and run command:

        http-server -p 8081
    
    to run the server and assign a -port to 8081.
    
    if the server is set to offline, the app should run, with the requests being resolved by the service worker. This will only show what's hard-coded into the app, and not the dynamic components of the app.

    You might need to disable your internet connection to test offline mode, as chrome's offline mode still allows api requests to go through.

    ng build --prod

3. Caching Assets for Offline Use

    ngsw-config.json is a standard .json file that outlines the page

    the index: 
        indicates the root page of our app that we want to cache and load

    assetGroups:
        configurations that define which static assets should be cached and how they should be cached. for example: dynamic assets would be data from the API that change frequently 

        name:
            the name of the asset group
        installMode:
            defines how the assets should load.
            prefetch, lazy
        updateMode:
            defines updates to the service worker 
        resources: { files:
            defines the files included in the service worker's cache.
            the file is always relative to the dist folder
            "/*.css" would include all the css in the root folder
            "/**/*.js" would include all the js in all the subfolders
        urls: [
            an array of strings that contains the external URLs of files and resources to be fetched for offline mode.
        ]
            }
        


4. Caching Dynamic Assets & URLS

    dataGroups :
        for dynamic data from external APIs that is expected to change frequently
        [
            {
                "name":
                "urls":
                "cacheConfig": {
                    maxSize: 
                        could be useful to limit a less specific url target. like tinyurl/*
                    maxAge:
                        defines how long the data should be stored before its dumped to fetch new data
                    timeout:
                        defines how long to wait on a response from the server before it uses the cache
                    strategy:
                        freshness - always reach out to the server for a response first, resorting to the cache if server response times out
                        performance - only reaches out to the back-end if the maxAge has timed out
                }
            }
        ]

5. Resources
   
     Official Angular Service Worker Docs: 
        https://angular.io/guide/service-worker-intro
    
    Academind Resources on PWAs: 
        https://academind.com/learn/progressive-web-apps
