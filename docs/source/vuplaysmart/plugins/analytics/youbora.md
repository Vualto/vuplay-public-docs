# Youbora

The following example creates a [Smart](/en/latest/api/smart.html) instance, sets a Youbora config and calls the `startStatsMonitoring` method. The value for the key `youbora` can be anything you want and will be passed directly to the Youbora code. Please see the Youbora documentation for values to pass.

``` javascript
var vuplaySmart = new Vuplay.Smart("<player-key>", Vuplay.LogLevel.WARN);
vuplaySmart.setStatsConfigs({
    "youbora": {
        accountCode: "<account-id>",
        media: {
            title: "<title>"
        },
        properties: {
            content_id: "<content-id>"
        }
    }
});
vuplaySmart.startStatsMonitoring();
```

The next code example will reset the player, set a new Youbora config, restart the stats monitoring and set a new src:

``` javascript
vuplaySmart.reset();
vuplaySmart.setStatsConfigs({
    "youbora": {
        accountCode: "<account-id>",
        media: {
            title: "<a-new-title>"
        },
        properties: {
            content_id: "<a-new-content-id>"
        }
    }
});
vuplaySmart.startStatsMonitoring();
vuplaySmart.setSrc("<mpeg-dash-url>");
```

Please note: If you call `stopStatsMonitoring` and then `startStatsMonitoring` without calling `setSrc` or `reset` then `setSrc` the Youbora ping API call will not be performed. There could also be other abnormal behaviour.
