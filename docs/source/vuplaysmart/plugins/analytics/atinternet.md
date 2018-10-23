# AT-Internet

The following example creates a [Smart](/api/smart.html) instance, sets an AT-Internet config and calls the `startStatsMonitoring` method.

Please refer to the [AT-Internet documentation](https://developers.atinternet-solutions.com/javascript-en/getting-started-javascript-en/tracker-initialisation-javascript-en/) for what values should be set in different scenarios.

``` javascript
var vuplaySmart = new Vuplay.Smart("<player-key>", Vuplay.LogLevel.WARN);
vuplaySmart.setStatsConfigs({
    "at_internet": {
        "page": {
            name: "Vuplay Web Player",  // The page's name within the site.
            level2: ""                  // Level 2 section in which the page is located.
        },
        "richMedia": {
            mediaType: "video",         // The content type (“video” or “audio”).
            mediaLevel2: "",            // Level 2 section in which the content is located.
            mediaLabel: "Content name", // The content's label/name.
            duration: "",               // Total duration of content in seconds (leave empty if Live). The duration must be inferior to 86400; mandatory when using a “clip”-type broadcast.
            isEmbedded: false,          // Defines whether the media is located on an external site.
            broadcastMode: "live",      // The type of meeting (“live” or “clip”).
            webdomain: ""               // The URL in cases of external placements.
        }
    }
});
vuplaySmart.startStatsMonitoring();
```