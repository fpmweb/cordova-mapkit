cordova-mapkit
==============

Upgraded mapkit plugin for cordova 

[the old mapkit plugin](https://github.com/purplecabbage/phonegap-plugins/tree/master/iOS/MapKit) was getting pretty tired

How to use
------------

1. Drag and drop the MapKit folder into the top level of your xcode project. The folder should be yellow
2. Add the MapKit library to the main project. To do this, go to the "Build Settings" tab on the main project config. Under "Link Binaries with Libraries" pick MapKit
3. In the plugins node of the config.xml document, add: `<plugin name="MapKitView" value="MapKitView" />`

Gotchas
------------

Maps wont show if you call them before cordova is ready and connected. Thus, you have to put all map logic in a handler:


	 // Native maps need some defaults to work properly
	 var mapDefaults = {
	     buttonCallback: 'window.plugins.mapKit.onMapCallback',
	     height: 460,
	     diameter: 1000,
	     atBottom: true,
	     lat: 49.281468,
	     lon: -123.104446
	 };
	 
	 document.addEventListener('deviceready', go, false);
	 
	 function go() {
	     alert("device ready")
	     cordova.exec('MapKitView.setMapData', this.mapDefaults);
	     cordova.exec('MapKitView.showMap');
	     var info = document.getElementById('deviceProperties');
	     alert(info)
	 };
	 
I have also seen maps fail when told to 'show' without any default pins