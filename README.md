# openui5-pwa-sample

You can build [Progressive Web Apps](https://developers.google.com/web/progressive-web-apps/) with any HTML/JS framework and OpenUI5 is not an exception. This example shows how to easily build a simple PWA with ```sap.m``` library. 

### [Run live demo](https://rawgit.com/SAP/openui5-pwa-sample/master/src/index.html)
Live demo is a simple [TODO list application](https://rawgit.com/SAP/openui5-pwa-sample/master/src/index.html). Add new tasks with the input field at the bottom of the screen. Tasks are stored locally and the application works in online and offline modes without any difference. You may install it on the home screen of a touch device like a native full screen application.

## Local Development Setup:
This sample is a static HTML application.  There are different possibilities to test it locally:

> Clone this repo and:
> * with Chrome Web Server: run the web server from the ```src``` folder or
> * with Node.js, run ```npm install``` and ```npm run serve``` or
> * with a trial SAP Cloud or any other Cloud Foundry account, change the application name in the ```manifest.yml``` and upload the app with ```cf push```

## Steps to create a PWA with OpenUI5

### Build the application
This sample is a simple single screen OpenUI5 TODO application. ```index.html``` is a general purpose loader. You may use it as a template for your own application. The ```todo-app.js``` contains the logic. Replace it with something more useful.

### Design, create and attach a service worker
Service worker is a prerequisite for a PWA. The main purpose of it is to cache application resources (and data) for the offline use on mobile devices.  One can use different [caching strategies](https://jakearchibald.com/2014/offline-cookbook/). The ```service-worker.js``` template in this sample caches application specific resources during the ```install``` event and OpenUI5 libraries during the ```fetch``` event, on the first network response. This scenario is neither complete nor ideal and should serve just as a starting point example.

### Create icons and a splash screen, add meta tags
A set of good looking icons is an essential part of a PWA.  The ```icons``` folder contains a minimal set of images.

Normally, an OpenUI5 application starts with an empty HTML file and generates contents dynamically. One of the PWA requirements is to show some static content or a splash screen immediately, before all javascript libraries are loaded and executed. The sample contains some static HTML that is replaced with the dynamic contents after the application is loaded.

Do not forget to include PWA related meta tags to the HTML head of your application. Use ```index.html``` as a reference. 

### Create a Web App Manifest
Create a Web App Manifest (```manifest.json```) and reference it from the application header. For more details, see the [Web App Manifest](https://developer.mozilla.org/en-US/docs/Web/Manifest) documentation.

### Test your app
After all the steps above are performed, run the application in a Chrome browser on desktop and run a PWA audit in [Chrome devtools](https://developers.google.com/web/tools/chrome-devtools/progressive-web-apps). If you see an image like below, everything is OK and you can submit your application.

> ![100% Progressive Web App](/images/100PWA.png)

### Limitations
OpenUI5 still uses synchronous XMLHttpRequests to load ```messagebundle.properties``` files with default UI labels and text. The texts cannot be cached and may be unavailable in offline mode. You need to provide custom labels for such default texts.

This sample uses local storage for persistence. Caching of application data and implementation of Offline CRUD patterns are not considered here.
