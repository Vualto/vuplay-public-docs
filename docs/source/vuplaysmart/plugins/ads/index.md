# Ads

Currently only [VAST](https://en.wikipedia.org/wiki/Video_Ad_Serving_Template) ads are supported and only when THEOplayer is loaded.

## Scheduling an Ad

You can schedule an ad by calling the `scheduleAd` on the instantiated [Smart](/en/latest/api/smart.html) object.

The following example creates a [Smart](/en/latest/api/smart.html) instance, attaches ad specific event listeners and schedules an ad to play after 120 seconds. The user will be allowed to skip the ad after 10 seconds:

``` javascript
var vuplaySmart = new Vuplay.Smart("<player-key>", Vuplay.LogLevel.WARN);

// setup ad specific events
vuplaySmart.on(Vuplay.EventType.AD, Vuplay.Events.adbreakbegin, console.log);
vuplaySmart.on(Vuplay.EventType.AD, Vuplay.Events.adbreakend, console.log);
vuplaySmart.on(Vuplay.EventType.AD, Vuplay.Events.adbegin, console.log);
vuplaySmart.on(Vuplay.EventType.AD, Vuplay.Events.adskipped, console.log);
vuplaySmart.on(Vuplay.EventType.AD, Vuplay.Events.adend, console.log);
vuplaySmart.on(Vuplay.EventType.AD, Vuplay.Events.aderror, console.log);

// schedule the ad
vuplaySmart.scheduleAd(Vuplay.AdType.VAST, "<vast-url>", 120, 10);
```

An ad can be scheduled at anytime. To schedule multiple ads simply call the `scheduleAd` method multiple times.

## Skipping an Ad

Once the ad has played for more than the `skipTime` the ad can be skipped. To perform this programmatically call the `skipCurrentAd` method on the instantiated [Smart](/en/latest/api/smart.html) object.
The method will return `true` or `false` depending on if the ad is skipped. If an ad is skipped the `adskipped` event will fire.

The following example creates a [Smart](/en/latest/api/smart.html) instance, adds an event listener for the `adskipped` event, schedules an ad and then skips the ad after it begins and 15 seconds has passed.

``` javascript
var vuplaySmart = new Vuplay.Smart("<player-key>", Vuplay.LogLevel.WARN);

vuplaySmart.on(Vuplay.EventType.AD, Vuplay.Events.adskipped, console.log);

// setup an event listener to create the skip timeout after the ad starts playback
vuplaySmart.on(Vuplay.EventType.AD, Vuplay.Events.adbegin, function () {
    setTimeout(function () {
        var adSkipped = vuplaySmart.skipCurrentAd();
    }, 15000);
});

// schedule the ad
vuplaySmart.scheduleAd(Vuplay.AdType.VAST, "<vast-url>", 120, 10);
```

## Ad Events

The event type `Vuplay.EventType.AD` is used to group the ad specific events.

The following table details the ad specific events.

| Event          | Description                                                                      | Arguments                                            |
|----------------|----------------------------------------------------------------------------------|------------------------------------------------------|
| adbreakbegin   | Fired when an ad break begins. One or more ads may play as part of the ad break. | startTime: number, duration: number, adCount: number |
| adbegin        | Fired when an individual ad begins playback.                                     | duration: number, skipTime: number                   |
| adskipped      | Fired when an ad is skipped.                                                     | duration: number, skipTime: number                   |
| aderror        | Fired when an ad fails to play back due to an error.                             | duration: number, skipTime: number                   |
| adend          | Fired when an individual ad completes playback.                                  | duration: number, skipTime: number                   |
| adbreakend     | Fired when an ad break completes.                                                | startTime: number, duration: number, adCount: number |

The following example creates a [Smart](/en/latest/api/smart.html) instance and attaches ad specific event listeners:

``` javascript
var vuplaySmart = new Vuplay.Smart("<player-key>", Vuplay.LogLevel.WARN);

// setup ad specific events
vuplaySmart.on(Vuplay.EventType.AD, Vuplay.Events.adbreakbegin, console.log);
vuplaySmart.on(Vuplay.EventType.AD, Vuplay.Events.adbreakend, console.log);
vuplaySmart.on(Vuplay.EventType.AD, Vuplay.Events.adbegin, console.log);
vuplaySmart.on(Vuplay.EventType.AD, Vuplay.Events.adend, console.log);
vuplaySmart.on(Vuplay.EventType.AD, Vuplay.Events.aderror, console.log);
```
