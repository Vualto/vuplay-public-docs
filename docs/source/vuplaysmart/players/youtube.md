# YouTube

Vuplay smart is capable of loading the [YouTube iframe player](https://developers.google.com/youtube/iframe_api_reference).

The following example loads vuplay smart, sets a YouTube video ID as the `src`, tells vuplay smart to load the [YouTube iframe player](https://developers.google.com/youtube/iframe_api_reference) and sets `autoStart` to `true`.

``` javascript
var vuplaySmart = new Vuplay.Smart("<player-key>", Vuplay.LogLevel.WARN);
var config = {
    src: "<youtube-video-id>",
    loadYoutube: true,
    autoStart: true
};
vuplaySmart.setup(config, document.getElementById("vuplay-container"));
```

Please note that the [YouTube iframe player](https://developers.google.com/youtube/iframe_api_reference) will only be loaded if the `loadYoutube` option is present and has `true` as the value.

Vuplay smart will not check if the browser environment supports [YouTube iframe player](https://developers.google.com/youtube/iframe_api_reference).
Please see the [iframe api requirements](https://developers.google.com/youtube/iframe_api_reference#Requirements) for more information.

## Configuration

Not all of the [Setup Configuration](/api/config.html) properties are supported when loading the [YouTube iframe player](https://developers.google.com/youtube/iframe_api_reference).
The table below details what configuration options are available when loading the [YouTube iframe player](https://developers.google.com/youtube/iframe_api_reference).

| Property    | Type                         | Description                                                                               | Required                       | Default                   |
|-------------|------------------------------|-------------------------------------------------------------------------------------------|--------------------------------|---------------------------|
| src         | string                       | [YouTube](/players/youtube.html) video ID.                                                             | true                           | undefined                 |
| autoStart   | boolean                      | If true playback will begin as soon as possible.                                          | false                          | false                     |
| loadYoutube | boolean                      | Will load the [YouTube](/players/youtube.html) iframe player.                                          | false                          | false                     |

## Supported Methods

Not all methods are supported by the [YouTube iframe player](https://developers.google.com/youtube/iframe_api_reference).
The table below details the methods supported when loading the [YouTube iframe player](https://developers.google.com/youtube/iframe_api_reference).

| Method                  | Parameter(s)                                                                              | Return Type                     | Description                                                                                                                      |
|-------------------------|-------------------------------------------------------------------------------------------|---------------------------------|----------------------------------------------------------------------------------------------------------------------------------|
| setStatsConfigs         | statsConfigs: { [ statsPluginId: string ]: object }                                       | void                            | Sets the stats configs. Will override any previously set stats configs.                                                          |
| startStatsMonitoring    | none                                                                                      | void                            | Starts all stats plugins that have been configured.                                                                              |
| stopStatsMonitoring     | none                                                                                      | void                            | Stops all stats plugins that have been configured.                                                                               |
| setup                   | config: [Configuration](/api/config.html), containerDiv: HTMLDivElement                     | void                            | Sets up vuplay smart using the provided [Configuration](/api/config.html) object and container.                                    |
| setLogLevel             | logLevel: [Vuplay.LogLevel](/api/loglevel.html)                                                     | void                            | Sets the level at which vuplay smart will output logs.                                                                           |
| getLogLevel             | none                                                                                      | [Vuplay.LogLevel](/api/loglevel.html)     | Returns the current log level of vuplay smart.                                                                                   |
| getPlayerKey            | none                                                                                      | string                          | Returns the current player key from the configuration object.                                                                    |
| setSrc                  | src: string                                                                               | void                            | Sets the source to be used by vuplay smart. This will cause the current content to be stopped.                                   |
| getSrc                  | none                                                                                      | string                          | Returns the stream url. It might be different to the src url that is set via `setSrc` due to environment.                        |
| setAutoStart            | autoStart: boolean                                                                        | void                            | Sets the autostart value of the content, must be called before the content is loaded.                                            |
| getAutoStart            | none                                                                                      | boolean                         | Returns the value of autostart.                                                                                                  |
| getContainerDiv         | none                                                                                      | HTMLDivElement                  | Returns the HTMLDivElement being used as the container for vuplay smart.                                                         |
| reset                   | none                                                                                      | void                            | Resets the config and clears the current content. Will stop any loaded stats plugins.                                            |
| play                    | none                                                                                      | void                            | Will start the source playing, if the source is loaded.                                                                          |
| pause                   | none                                                                                      | void                            | Will pause the current content if playing, if not currently playing no action will be taken.                                     |
| isPaused                | none                                                                                      | boolean                         | Returns true is the currently loaded content is paused or stopped.                                                               |
| seek                    | seconds: number                                                                           | void                            | Sets the current time of the player in seconds. This should be positive for VOD or negative for Live.                            |
| setVolume               | volume: number                                                                            | void                            | Sets the volume of the loaded player. The value should be between 0 and 1.                                                       |
| getVolume               | none                                                                                      | number                          | Returns the volume of the loaded player. The value will be between 0 and 1.                                                      |
| getCurrentTime          | none                                                                                      | number                          | Returns the current time value of the player in seconds. Will be positive for VOD or negative for LIVE.                          |
| getDuration             | none                                                                                      | number                          | Returns the duration of the current source in seconds. This value will be the amount of DVR for LIVE.                            |
| on                      | eventType: [EventType](/api/eventtype.html) , event: [Event](/api/events.html) , handler: function            | void                            | [Subscribe to an event](/api/events.html#subscribe-to-an-event).                                                                                 |
| off                     | eventType: [EventType](/api/eventtype.html) , event: [Event](/api/events.html) , handler: function            | void                            | [Unsubscribe from an event](/api/events.html#unsubscribe-to-an-event).                                                                         |

## Supported Events

Not all events are supported by the [YouTube iframe player](https://developers.google.com/youtube/iframe_api_reference).
The table below details the events that will fire when using the [YouTube iframe player](https://developers.google.com/youtube/iframe_api_reference).
It also details the corresponding [YouTube iframe event](https://developers.google.com/youtube/iframe_api_reference#Events).

| Event          | Description                                                                                                                  | [EventType](/api/eventtype.html)  | Args                | corresponding YouTube Event                                                                                    |
|----------------|------------------------------------------------------------------------------------------------------------------------------|-------------------------|---------------------|----------------------------------------------------------------------------------------------------------------|
| playerready    | Fired when the player is ready.                                                                                              | VUPLAY                  | playerId: string    | `onReady`                                                                                                      |
| error          | Fired when an error occurs, an error message and an array of relevant data will be returned.                                 | ERROR                   | none                | `error`                                                                                                        |
| loadsrc        | Fired when a new src is about to be loaded in the player.                                                                    | MEDIA                   | src: string         | `onStateChange` with a value of `5 (video cued)`                                                               |
| playing        | Fired when playback starts.                                                                                                  | MEDIA                   | currentTime: number | `onStateChange` with a value of `1 (playing)`                                                                  |
| pause          | Fired when playback is paused. The `ended` property indicates if the content has paused due to completing playback.          | MEDIA                   | ended: boolean      | `onStateChange` with a value of `2 (paused)`                                                                   |
| ratechange     | Fired when playback speed changes.                                                                                           | MEDIA                   | none                | `onPlaybackRateChange`                                                                                         |
| ended          | Fired when the current playback completes.                                                                                   | MEDIA                   | none                | `onStateChange` with a value of `0 (ended)`                                                                    |
| bufferstart    | Fired when playback data has started preloading.                                                                             | MEDIA                   | currentTime: number | `onStateChange` with a value of `3 (buffering)`                                                                |
| bufferend      | Fired when playback data has finished preloading.                                                                            | MEDIA                   | currentTime: number | `onStateChange` with a value of `1 (playing)` or `2 (paused)` (whichever is first after a `bufferstart` event) |

## Stats Plugins

When the [YouTube iframe player](https://developers.google.com/youtube/iframe_api_reference) the [Statistics](/plugins/analytics/)  plugins will still be loaded.
The events fired by the player will be passed to the loaded [Statistics](/plugins/analytics/)  plugins.

Please beware that not all the [vuplay smart events](/api/events.html)  will be fired when the YouTube player is loaded.

## Ads

When loading the [YouTube iframe player](https://developers.google.com/youtube/iframe_api_reference) normal vuplay smart ad functionality will not work.
Advertising is controlled by YouTube in this scenario. Please see [YouTube's advertising site](https://www.youtube.com/yt/advertise/en-GB/) for more information.

## Casting

When loading the [YouTube iframe player](https://developers.google.com/youtube/iframe_api_reference) normal vuplay smart casting functionality will not work.
Casting is controlled by YouTube in this scenario. Please see [YouTube's casting documentation](https://support.google.com/youtube/answer/3230451) for more information.
