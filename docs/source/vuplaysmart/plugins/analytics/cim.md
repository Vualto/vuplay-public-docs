# CIM

The following example creates a [Smart](/en/latest/api/smart.html) instance, sets a CIM config and calls the `startStatsMonitoring` method.

``` javascript
var vuplaySmart = new Vuplay.Smart("<player-key>", Vuplay.LogLevel.WARN);
vuplaySmart.setStatsConfigs({
    "cim": {
        identifier: "identifier", // The account identifier provided by CIM
        materialIdentifier: "material", // A description the current content or stream.
        section: "section", // The section identifier mapping.
        contentType: "content-type", // The content type mapping.
        sourceType: "source-type", // The source type mapping.
        tvLink: "tv-link" // A concatenation of the date and title separated by - e.g (13122017-MYSTREAM)
    }
});
vuplaySmart.startStatsMonitoring();
vuplaySmart.setSrc("<mpeg-dash-url>");
```