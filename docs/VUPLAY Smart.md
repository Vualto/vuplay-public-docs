# vuplay API Documentation

# vuplay Smart (0.5.2)

This documentation describes the steps to integrate and use vuplay Smart

## Introduction


The vuplay smart is a javascript application that can be used to play back live and VOD video streams. 

It will load a player and stream type depending on the browser the end user is using. It is capable of playing back streams encrypted with Microsoft's PlayReady encryption, Google's Widevine encryption or Apple's Fairplay.

## Requirements

* HTML5 capable browser that supports the [Media Extensions](http://www.w3c.github.io/media-source/) and [Encrypted Media Extensions.](http://www.w3c.github.io/encrypted-media/)

or

* A browser that supports [Silverlight](http://www.microsoft.com/getsilverlight/)

and

* A javascript and HTML editor

* The vuplay load javascript file


* A player key supplied by [Vualto](http://vualto.com)

When playing content served from a different domain or origin, standard HTML5 same-origin security policies apply. To overcome this, content has to be made available through CORS.

Please contact * support@vualto.com* to request a download of the load javascript.

## Setup

A. Create the HTML page with the required assets: 


```HTML
<html>
  <head>
    <title>Vuplay Smart Player</title>
  </head> 
  <body>
    <script src="https://cdn-vuplay.drm.technology/load.min.js"type="text/javascript"></script>
  </body>
</html>

```

NB: Using the url above will use the latest version of the player. See the "Versioning" section below on how to request a particular version of the player.

B. Add a ```div``` to the body. The player will append the player HTML to this ```div``` as children:

```
<div id="player-container"></div>
```

NB: You can style this div in order to set the player size and responsiveness. 

C. Create a new configuration object and pass this to a new Vuplay object. You can also pass a function that will be called when the player is loaded. 


```
<script type ="text/javascript">
    var vuplay = null;
    (function () {
        var config = {
            container: document.getElementById("player-container"),
            source: "<stream_url>",
            autostart: true,
            playerKey: "<player_key>"
        };
        vuplay = new Vuplay(config, function() {
            window.console && window.console.log("player loaded");
        });
    })();
</script>
```

NB: Please contact [support@vualto.com](support@vualto.com) to request your player key.


##Complete Example

```HTML
<html lang="en-IE">
    <head>
        <meta charset="utf-8" />
        <title>Vuplay Smart Player</title>
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <style>
             #player-container {
                 width: 640px;
                 height: 360px;
             }
        </style>
    </head>
    <body>
        <div id="player-container"></div>
        <script src="https://cdn-vuplay.drm.technology/load.min.js"></script>
        <script type="text/javascript">
            var vuplay = null;
            (function () {
                var config = {
                    container: document.getElementById("player-container"),
                    autostart: true,
                    source: "<stream_url>",
                    playerKey: "<player_key>"
                };
                vuplay = new Vuplay(config, function() {
                    window.console && window.console.log("player loaded");
                });
            })();
        </script>
    </body>
</html>
```

NB: Please contact [support@vualto.com](support@vualto.com) to request your player key.

## Subtitles

Subtitles can be added to the configuration object when creating a new Vuplay object. [WebVTT](https://w3c.github.io/webvtt) subtitles should be passed into the player.

If a silverlight player is loaded then the player will attempt to transform the WebVTT url into a TTML url by changing the extension to ".xml". 
To make use of this functionality; the urls for the WebVTT subtitle file and the TTML url must be **exactly the same *except* for the extension.**

In stream subtitles are only supported with the silverlight player. To enable this please contact [support@vualto.com.](support@vualto.com)

This example shows how to create and set the subtitles when creating the player:

```HTML
<script type ="text/javascript">
    var englishSubtitle = new Vuplay.Subtitle("http://url.to/webvtt-subtitles.vtt", "English",
        Vuplay.Subtitle.kinds.SUBTITLES, "en", true);
    var frenchSubtitle = new Vuplay.Subtitle("http://url.to/webvtt-subtitles.vtt", "French", 
        Vuplay.Subtitle.kinds.SUBTITLES, "fr", false);
    
    var vuplay = null;
    (function () {
        var config = {
            container: document.getElementById("player-container"),
            source: "<stream_url>",
            autostart: true,
            playerKey: "<player_key>",
            subtitles: [englishSubtitle, frenchSubtitle]
        };
        vuplay = new Vuplay(config, function() {
            window.console && window.console.log("player loaded");
        });
    })();
</script>
```

The ```Vuplay.Subtitle``` constructor can be used to create subtitle objects.

## Versioning

From version **0.3.4** onwards it is possible to request a particular version of the player. 

The url [https://cdn-vuplay.drm.technology/load.min.js](https://cdn-vuplay.drm.technology/load.min.js) will cause the latest version of the player to be used. 
In order to use a particular version you must replace {version} in this url [https://cdn-vuplay.drm.technology/{version}/load.min.js](https://cdn-vuplay.drm.technology/{version}/load.min.js) with your desired version. 

For example: 
Using [https://cdn-vuplay.drm.technology/0.5.2/load.min.js](https://cdn-vuplay.drm.technology/0.5.2/load.min.js) will load version **0.5.2** of the player.


## Force Loading Option

From version **0.3.7** onwards it is possible to force load the player choice. Any automatic decisons will be overridden by this option. 

**Use of this setting is not recommended in production.**


## Configuration Parameters


| Name       | Type         | Description                                                           |
|------------|--------------|-----------------------------------------------------------------------|
| container  | HTMLElement  | The ```div``` element that the player can append to. (Required)
| playerKey  | string       | Supplied by Vualto. Please contact **support@vualto.com** to request your player key. (Required)
| source     | string       | The stream url to play. (Required)
| autostart  | boolean      | Set to ```true``` to start playing as soon as the player is loaded.
| drmToken   | string       | vudrm token. Required if stream is encrypted.
| overrideLaUrl | string    | Set to override the default license server url if the stream is encrypted.
| subtitles  | Array<Vuplay.Subtitle> | Set subtitles to be loaded into the player. Should be in [WebVTT](https://w3c.github.io/webvtt) format.
| forcePlayer | string      | Force load a player by setting the name of the player. ```overrideLaUrl``` config option is required if forcing a player load.
| useSsl     | boolean      | When true the player will use https for all urls. **If this is true and the containing page is http silverlight will NOT work.** The player will automatically use SSL if the containing page is https and this value is not set


## Classes

### Vuplay

**Constructor **
new Vuplay(config, onPlayerLoaded) 

| Constructor Parameters| Type         | Description                                                           |
|------------|--------------|-----------------------------------------------------------------------|
| config     | object       | An object containing the configuration options detailed in the Configuration Parameters section
| onPlayerLoaded | function | Called once the player is loaded and ready for interaction.


| Public Instance Methods| Parameters   | Return Value | Description                                |
|------------|--------------|-------------|----------------------------------------------------------|
| getInnerPlayer | 	n/a     | null/object | Returns a reference to the inner player that was loaded. The type of inner player loaded can be determined by the constant ```Vuplay.PLAYER_ID.``` Will return null if no player has been loaded.
| getDrmConfig | n/a        | object      | Returns an object that contains info about the drm to be used. The values will be null until the player is loaded.


### Vuplay.Subtitle

**Constructor **
new Vuplay.Subtitle(file, label, kind, srclang, isDefault) 


| Constructor Parameters| Type         | Description                                                           |
|------------|--------------|-----------------------------------------------------------------------|
| file       | string       | Url to webVTT subtitles file.
| label      | string       | User friendly language. Will be used in the subtitle selection menu.
| kind       | string       | The type of text track. A ```Vuplay.Subtile.events``` key can be used.
| srclang    | string       | Language of the source file. Should be a valid [BCP 47](http://r12a.github.io/apps/subtags/) language tag.
| isDefault  | boolean      | Use this subtitle as soon as the player loads. If multiple subtitles have ```isDefault``` set to ```true``` the first in the array will be used.


**Public Instance Methods **
n/a 

## Constants

| Variable   | Type         | Description                                                           |
|------------|--------------|-----------------------------------------------------------------------|
| Vuplay.VERSION | string   | Contains the player version
| Vuplay.API_URL | string	| Url to vuplay smart player api.
| Vuplay.PLAYER_ID | null/string | Once the player is loaded this will detail what player has been used. ```null``` until the the player is loaded.
| Vuplay.Subtitle.kinds | Object<key,value>	| Contains the supported types of subtitles. Can be used in the Vuplay.Subtitle constructor.

## Known Issues

* Choppy playback when chrome dev tools are open.
* No mobile or tablet support
* `vuplay hls` does not support subtitles.


## Release Notes

v0.2.0

* Initial Release

v0.2.1

* Change from use of clientToken to apiKey

v0.3.0

* Change apiKey to playerKey
* Support for subtitles loaded from external files.

v0.3.1

* Increased logging from player to console.
* All laurls are https.

v0.3.4

* Old versions of the player are now available.

v0.3.5

* Drm type exposed through a constant.

v0.3.7

* Fixed Edge sometimes not initialising the playready key session in a timely way.
* Fix for when styling jwplayer size.
* Fix spelling of level in log comment.
* Force player choice option added.
* Fixed callback not being called when jwplayer is ready.
* [MPEG-dash THEOplayer](https://www.theoplayer.com/features/mpeg-dash) added.
* Return 403 if no valid player is found in the loading rules.
* Add DRM key system id constant that is set after player load.

v0.3.8

* vuplay skin added to THEOplayer dash.
* THEOplayer dash updated to 2.1.0
* no longer requires ```Vuplay.DRM_TYPE``` or the override laurl to be set when forcing the player choice.

v0.4.0

* vuplay dash integrated into the smart player.
* ```Vuplay.Subtitle``` construtor changed to add subtitle kind and srclang.

v0.4.2

* vuplay silverlight updated to 2.1.0

v0.4.4

* fix for https stream urls being converted to http
* ```useSsl``` config option added
* if ```useSsl``` option is not used the the player will use the containing pages url scheme
* query strings are supported on the stream url

v0.4.5

* vuplay dash updated to 0.7.1

v0.4.6

* ```Vuplay.PLAYER_TYPE``` values changed to match serverside config
* ```Vuplay.PLAYER_TYPE``` renamed to Vuplay.PLAYER_ID
* ```Player.Name``` returned by api renamed to Player.Id
* fix for callback function not being called when vuplay-dash is loaded
* vuplay-dash updated to 0.7.2
* vuplay-silverlight updated to 2.1.1


v0.5.0

* vuplay hls 0.2.0 intergrated into vuplay smart
* ```Vuplay.DRM_TYPE``` and ```Vuplay.DRM_KEY_SYSTEM_ID``` constants removed. You can now get this information by calling ```getDrmConfig``` on the vuplay instance.
* vuplay dash can now be used in firefox v47+

v0.5.1

* vuplay dash updated to 0.7.3

v0.5.2

* vuplay hls updated to 0.2.1

