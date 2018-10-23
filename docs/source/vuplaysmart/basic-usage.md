# BASIC USAGE

``` javascript
  var vuplaySmart = new Vuplay.Smart("<player-key>", Vuplay.LogLevel.WARN);
  vuplaySmart.setup({ src: "<mpeg-dash-url>" }, document.getElementById("vuplay-container"));
```

<div class="admonition warning">
    <p class="first admonition-title">Warning</p>
    <p class="last">Please note that any pages embedding vuplay smart must use SSL. This is due to Google Chrome EME restrictions and Silverlight limitations.</p>
</div>

## Step by Step instructions

The following instructions will walk you through using vuplay smart.

- Create the HTML page and add a reference to vuplay smart javascript. To get a copy of vuplay smart please contact [support@vualto.com](mailto:support@vualto.com)

``` html
<!DOCTYPE html>
<html lang="en-IE">
    <head>
        <meta charset="utf-8" />
        <title>Vuplay Smart</title>
    </head>
    <body>
        <script src="vuplay-smart.min.js "></script>
    </body>
</html>
```

- Add a HTML div to the page. The vuplay smart HTML will be added to this div along with the loaded player. You can add style to this div in order to control the size of any loaded players.

``` html
<div id="vuplay-container"></div>
```

- Create a new instance of vuplay smart. This will *not* load a player or start playback and you must pass the player key. Please contact [support@vualto.com](mailto:support@vualto.com) if you do not have a player key. See the [Smart](api/smart.html) section for more information.

``` javascript
var vuplaySmart = new Vuplay.Smart("<player-key>", Vuplay.LogLevel.WARN);
```

<div class="admonition note">
    <p class="first admonition-title">Tip</p>
    <p class="last">Please contact <a href="mailto:support@vualto.com">support@vualto.com</a> for a player key.</p>
</div>

- Optionally start any stats monitoring. See [Statistics](plugins/analytics/)  section for more information.

``` javascript
vuplaySmart.setStatsConfigs({
    "statsPluginId": {
        "some": "data"
    }
});
vuplaySmart.startStatsMonitoring();
```

- You can now add event listeners to vuplay smart before calling the setup method. See the [Event Usage](api/events.html#event-usage)  section for more information.

``` javascript
vuplaySmart.on(Vuplay.EventType.VUPLAY, Vuplay.Events.playerready, eventHappened);
vuplaySmart.on(Vuplay.EventType.MEDIA, Vuplay.Events.canplay, eventHappened);
vuplaySmart.on(Vuplay.EventType.MEDIA, Vuplay.Events.timeupdate, eventHappened);
```

- Create a vuplay smart config. See the [Configuration](api/config.html) section for more information.

``` javascript
var config = {
    src: "<mpeg-dash-url>",
    vudrmToken: "<vudrm-token>",
    autoStart: true
};
```

- Setup vuplay smart by passing the config and the container div. This will load a player based on client rules and environment. If `autostart` has been set to true playback will begin as soon as possible. See the [Smart](api/smart.html) section for more information.

``` javascript
vuplaySmart.setup(config, document.getElementById("vuplay-container"));
```

## A complete example

Below is a basic example of the required code to setup the vuplay smart.

``` html
<!DOCTYPE html>
<html lang="en-IE">
    <head>
        <meta charset="utf-8" />
        <title>Vuplay Smart</title>
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <style>
            #vuplay-container {
                width: 50%;
            }
        </style>
    </head>
    <body>
        <div id="vuplay-container"></div>
        <script src="vuplay-smart.min.js "></script>
        <script type="text/javascript">
            (function () {
                var vuplaySmart = new Vuplay.Smart("<player-key>", Vuplay.LogLevel.WARN);
                vuplaySmart.startStatsMonitoring();
                vuplaySmart.on(Vuplay.EventType.VUPLAY, Vuplay.Events.playerready, eventHappened);
                vuplaySmart.on(Vuplay.EventType.MEDIA, Vuplay.Events.canplay, eventHappened);
                vuplaySmart.on(Vuplay.EventType.MEDIA, Vuplay.Events.timeupdate, eventHappened);

                var config = {
                    src: "<mpeg-dash-url>",
                    vudrmToken: "<vudrm-token>",
                    autoStart: true
                };

                vuplaySmart.setup(config, document.getElementById("vuplay-container"));
            })();
        </script>
    </body>
</html>
```