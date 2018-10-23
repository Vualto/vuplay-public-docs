# Comscore

The following example creates a [Smart](/en/latest/api/smart.html) instance, sets a Comscore config and calls the `startStatsMonitoring` method.

The information passed into the config will depend on your Comscore requirements. The config supports an optional `publisherId` and two Comscore label collections; `playbackLabels` and `assetLabels`. The implementation-wide labels will be set automatically.

Please refer to the Comscore documentation for what labels should be set in different scenarios.

``` javascript
var vuplaySmart = new Vuplay.Smart("<player-key>", Vuplay.LogLevel.WARN);
vuplaySmart.setStatsConfigs({
    "comscore": {
        publisherId: "<publisher_id>",
        playbackLabels: {
            ns_st_cp: 1 // Expected Number of Assets
        },
        assetLabels: {
            ns_st_ci: 0, // Unique Content ID
            ns_st_pu: "<brand>", // Publisher Brand Name
            ns_st_pr: "<program-title>", // Program Title
            ns_st_ep: "<episode-title>", // Episode Title
            ns_st_ty: "video" // stream type
        }
    }
});
vuplaySmart.startStatsMonitoring();
```

The next code example will reset the player, set a new Comscore config, restart the stats monitoring and set a new src:

``` javascript
vuplaySmart.reset();
vuplaySmart.setStatsConfigs({
    "comscore": {
        publisherId: "<publisher_id>",
        playbackLabels: {
            ns_st_cp: 1 // Expected Number of Assets
        },
        assetLabels: {
            ns_st_ci: 0, // Unique Content ID
            ns_st_pu: "<a-newbrand>", // Publisher Brand Name
            ns_st_pr: "<a-new-program-title>", // Program Title
            ns_st_ep: "<a-new-episode-title>", // Episode Title
            ns_st_ty: "video" // stream type
        }
    }
});
vuplaySmart.startStatsMonitoring();
vuplaySmart.setSrc("<mpeg-dash-url>");
```