## Chromecast Chrome Browser SDK (v0.1)

## Introduction

This documentation describes the steps to integrate and use the vuplay SDK for Chromecast.

The Chromecast SDK allows easy development of custom Chromecast receivers with both DRM encrypted and no-DRM content. It currently supports Playready encrypted Microsoft Smooth Streams and no-DRM MPEG-DASH. 


## Project Requirements

* A Google Chromecast running firmware version 27946 or greater
* Chrome Browser using Google Cast extension 15.605.1.3 or greater
* The Vuplay Chromecast SDK
* A javascript and html editor
* A computer with a static IP address on the same network as the Chromecast for development
* A Google Cast SDK Developer's account

When playing content served from a different domain or origin, standard HTML5 same-origin security policies apply. To overcome this, content has to be made available through CORS.

Please contact ``` support@vualto.com``` to request a download of the SDK.


## Before Starting

1. Setup a web server making your development directory available on your computer's IP address. It is important that this is completed as the receiver app will be loaded from the given address by the Chromecast. 
2. Make two files in this folder, sender.html and receiver.html.
3. Ensure your Chromecast device has been registered with Google in the cast developers console. 
4. Register a new application with the following settings:
	Receiver Type: Custom Receiver
	Receiver Details, URL: The IP/path combination for your receiver.html file (e.g. http://192.168.1.81/receiver.html
    Google Cast for Audio: unticked
    All other options can be set as desired. Make a note of the Application ID after saving. 


## Sender

The sender is the client-side implementation which resides in the user’s browser. This code is required to trigger the connection with the chromecast. When designing your sender app it is worth taking note of the Google UX Guidelines: ```https://developers.google.com/cast/docs/ux_guidelines```  and Design Checklist: ```https://developers.google.com/cast/docs/design_checklist```

## Setup

* Setup the basic html page with the required assets:

```
<html>
  <head>
     <title>Vuplay Chromecast Example</title>
  </head>
  <body>
    <script type="text/javascript" src="<sdk_url>"></script>
  </body>
</html>
```

* Add a button to start the cast when the user is ready, and hook up an event listener:

```
<button id="startCast">Start Chromecast</button>
<script type=”text/javascript”>
    (function() {
        var startButton = document.getElementById("startCast");
        startButton.addEventListener("click", startChromecast);
    })();
</script>

```
* Next, add a function which calls the Vuplay SDK when the button is clicked. 

```
<script type="text/javascript">
    var cast;
    (function() {
        var startChromecast = function() {
            var castConfig = {
                        source: "<media_source>",
                        autostart: true,
                        appId: "<app_id>"
}
             	cast = new vuplay.Chromecast(castConfig);
}
		var startButton = document.getElementById("startCast");
        startButton.addEventListener("click", startChromecast);
        })();
</script>

```

## Complete Exmples

```
<html>
   <head>
      <title>Vuplay Chromecast Example</title>
   </head>
   <body>
      <button id="startCast">Start Chromecast</button>
      <script type="text/javascript" src="<sdk_url>"></script>
      <script type="text/javascript">
         var cast;
         (function() {
         var startChromecast = function() {
         var castConfig = {
                     source: "<media_source>",
                     autostart: true,
                     appId: "<app_id>"
         }
          	cast = new vuplay.Chromecast(castConfig);
         }
         var startButton = document.getElementById("startCast");
         startButton.addEventListener("click", startChromecast);
         })();
      </script>
   </body>
</html>
```

## Live Examples

Live examples can be found at the Vuplay Portal: ```http://vuplay/portal.drm/.technology```. Please contact support@vualto.com for a login.


**Configuraton Parameters**

| Name              | Description                                                           |
|-------------------|-----------------------------------------------------------------------|
| autostart         | Set to true to start playing as soon as a source is passed. 
| source            | The mpeg-dash manifest url 
| drmToken          | The drm token used if the stream is encrypted.
| laurl             | License server URL. Overrides the url in the dash manifest. Required for widevine.
| debug             | Set to true to see output in the console


**API Methods**

| Method            | Description                                                           |
|-------------------|-----------------------------------------------------------------------|
| getVersion()      | Returns the version of the SDK.
| setSource(string) | Set the MPEG-dash source url. Returns a Promise that will fulfil once source has been loaded.
| setAutoStart(boolean)| Sets if the player will start playing automatically after setSource(value) is called.
| setDebug(boolean) | Sets the DRM token. Required if attempting to playback and encrypted stream. Must be set before setSource().
| setLaURL(string)  | Sets the License Acquisition URL. Required if playing back a Widevine encrypted stream. In other cases will override the MPEG-dash manifest’s laURL. Must be set before setSource().
| play()            | Will start playback in the player.
| pause()           | Will pause playback in the player


## Receiver App

A receiver app is very similar to a sender. It is an HTML, CSS and JavaScript app which is loaded by the Chromecast to display the media playback. In order to load the receiver is makes use of the App ID and the given Receiver Url, of which the setup is directed in the before starting section. 

## Setup

**Start by creating a basic HTML with the required assets. **

```
<html>
  <head>
    <script type="text/javascript" src="<receiver_sdk_url>"></script>
      <link rel="stylesheet" href="<receiver_sdk_styles>" />
  </head>
  <body>

  </body>
</html>
```

**Then, add a video container with the ID “vuplay wrapper”: **

```
<div class="vuplay-wrapper"></div>
```

**Initiate the chromecast connection with the sender application: ** 

```
<script type="text/javascript">
      var connection = new vuplay.chromecast.receiver.Connection({
        debug: true,
      });
</script>
```

**Catch any custom error message you send through with an event listener:**

```
connection.addEventListener('customMessage', function(message) {
    console.log(message);
  });
```

## Complete Example

```
<!DOCTYPE html>
<html>
  <head>
    <script type="text/javascript" src="receiver.js"></script>
    <link rel="stylesheet" href="vuplay.receiver.css" />
  </head>

  <body>
    <div id="vuplay-wrapper"></div>

    <script type="text/javascript">
      var connection = new vuplay.chromecast.receiver.Connection({
        debug: true
      });
      
      connection.addEventListener('customMessage', function(message) {
        console.log(message);
      });
    </script>
  </body>
</html>
```











