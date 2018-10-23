# Adobe

The following example creates a [Smart](/api/smart.html) instance, sets an Adobe config and calls the `startStatsMonitoring` method.

Please refer to the [Adobe Analytics documentation](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/js_2.0/c_vhl_feature-js.html) for what values should be set in different scenarios.

``` javascript
var vuplaySmart = new Vuplay.Smart("<player-key>", Vuplay.LogLevel.WARN);
vuplaySmart.setStatsConfigs({
    "adobe": {
        player: {
            name: "vualto_player-name",
            videoId: "vualto_player-video-id",
            videoName: "vualto_player-video-name"
        },

        visitor: {
            marketingCloudOrgId: "{marketing_cloud_org_id}@adobeorg",
            trackingServer: "{tracking_server}",
            dpid: "vualto_visitor-dpid",
            dpuuid: "vualto_visitor-dpuuid"
        },

        appMeasurement: {
            rsid: "{client_rsid}",
            trackingServer: "{tracking_server}",
            pageName: "vualto_appmeasurement-page-name",
            visitorId: "vualto_appmeasurment-visitor-id"
        },

        heartbeat: {
            trackingServer: "{tracking_server}",
            publisher: "{publisherid}@adobeorg",
            channel: "vualto_heartbeat-channel",
            ovp: "vualto_heartbeat-ovp", // name of the online video platform through which content gets distributed.
            sdk: "vualto_heartbeat-sdk_vuplaysmart_v0.16.x"
        },

        video: {
            name: "vualto_videofakename",
            id: "vualto_videofakeid",
            duration: 6000, // video.duration
            streamType: "vod",  // vod/live/linear
            initialBitrate: 144704, // default minimal value
            metadata: {
                standard: {
                    show: "vualto_a.media.show",
                    season: "vualto_a.media.season",
                    episode: "vualto_a.media.episode",
                    assetId: "vualto_a.media.asset",
                    genre: "vualto_a.media.genre",
                    firstAirDate: "vualto_a.media.airdate",
                    firstDigitalDate: "vualto_a.media.digitaldate",
                    rating: "vualto_a.media.rating",
                    originator: "vualto_a.media.originator",
                    network: "vualto_a.media.network",
                    showType: "vualto_a.media.type",
                    adLoad: "vualto_a.media.adload",
                    mvpd: "vualto_a.media.pass.mvpd",
                    authorized: "vualto_a.media.pass.auth",
                    dayPart: "vualto_a.media.daypart",
                    feed: "vualto_a.media.feed",
                    streamFormat: "vualto_a.media.format"
                },
                custom: {
                    customVideoMetadata: "vualto_custom-metadata"
                }
            }
        },

        ad: {
            adName: "",
            adId: "",
            position: 1,
            length: 600,
            standardMetadata: {
                advertiser: "",
                campaignId: "",
                creativeId: "",
                placementId: "",
                siteId: "",
                creativeUrl: ""
            },
            customMetadata: {
                vualtoAdMeta: "vualto_client-id-1234"
            }
        },

        adBreak: {
            adbreakName: "",
            position: 1
        }
    }
});
vuplaySmart.startStatsMonitoring();
```