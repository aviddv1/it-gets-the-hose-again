The controller software is built on [Node.js](https://nodejs.org) on the backend and Uses [React.js](https://facebook.github.io/react/) & [Redux](https://github.com/rackt/redux) for the frontend web UI. The software is also compatible with Apples HomeKit using [HAP-NodeJS](https://github.com/KhaosT/HAP-NodeJS) if you want to use an IOS based controller app rather than the built in scheduling functionality exposed by the web UI.

Installation
============

* clone or copy this repository to your Raspberry Pi
* Run ```sudo ./install.sh```
* Run ```cp keys.default.js keys.js```
* Edit keys.js in your favourite text editor and add your Google Maps & OpenWeatherMap API keys. These keys are required and the web app will not work correctly without them

 ##### Getting a OpenWeatherMap API key
 Go to [openweathermap.org](http://openweathermap.org) and sign up for a free account. Once signed up, go to home.openweathermap.org and copy the Api key from the setup tab into the ```OPEN_WEATHER_API_KEY``` variable in keys.js

 ##### Getting Google Maps API key
 Go to [console.developers.google.com](https://console.developers.google.com/) and go to the Api manager page. Enable the 'Google Static Maps' API on the overview tab, then go to the credentials page and generate a new browser API key. Copy this key into the ```GOOGLE_MAPS_API_KEY``` in keys.js

* Run ```sudo service start itgetsthehoseagain```
* browse to https://&lt;my-raspberry-pi-ip&gt;/ and enter a valid Linux username/password for your Pi (by default pi/raspberry)

Development
===========

Development on the Raspberry Pi hardware can be somewhat painful, so this application has been built with having a dev environment on OSX or Linux systems in mind. To facilitate this, the software can run in one of two modes - Development or Production. It is recommended to only use production mode when running on the Pi itself, as production mode enables a number of features which are inconvenient for development including HTTPS, authentication (using pwauth), and minified frontend resources. The mode can be controlled by setting the ```NODE_ENV``` environment variable to either development/production (development is the default).

Setting up a working dev environment can be done by following these steps.

* Install Node.js for your platform (OSX or Linux is recommended)
* Run ```npm install -g gulp```
* Run ```npm install```

You should now have a working dev environment set up. To build and run the application run 

```
gulp build
gulp serverw
```

The build command only needs to be run once - this builds some frontend vendor dependancies and does not need to be re-run. The serverw command starts up the application server and watches for changes and restarts/hot-reloads as changes are detected. You should now be able to browse to the web UI on http://localhost:3001/.