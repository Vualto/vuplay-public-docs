# Smart

This is the main object in vuplay smart and can be instantiated. There are no public properties on the Smart object.

## Constructor

| Parameter(s) | Description                                                                              | Type                         |
|--------------|------------------------------------------------------------------------------------------|------------------------------|
| playerKey    | Set the player key (required).                                                           | string                       |
| logLevel     | Set the level of logs displayed in the console (optional).                               | [Vuplay.LogLevel](/en/latest/api/loglevel.html) |

<div class="admonition hint">
    <p class="first admonition-title">Tip</p>
    <p class="last">Please contact <a href="mailto:support@vualto.com">support@vualto.com</a> to get your player key.</p>
</div>

## Methods

Here are all the methods available for the Smart object

### addSocketChannel

---

- **Parameter(s):** channel: string
- **Return type:** void
- **Description:** Start listening to the push notifications for the passed channel.

### getAudioTracks

---

- **Parameter(s):** none
- **Return type:** Array\<[AudioTrack](/en/latest/api/smart.html#audiotrack)>
- **Description:** Returns an array of the loaded audio-tracks.

### getAutoStart

---

- **Parameter(s):** none
- **Return type:** boolean
- **Description:** Returns the value of autostart.

### getAvailableCastTypes

---

- **Parameter(s):** none
- **Return type:** Array\<[CastTypes](/en/latest/plugins/casts/#cast-types)>
- **Description:** Returns the currently available cast devices.

### getContainerDiv

---

- **Parameter(s):** none
- **Return type:** HTMLDivElement
- **Description:** Returns the HTMLDivElement being used as the container for vuplay smart.

### getCurrentTime

---

- **Parameter(s):** none
- **Return type:** number
- **Description:** Returns the current time value of the player in seconds. Will be positive for VOD or negative for LIVE.

### getDuration

---

- **Parameter(s):** none
- **Return type:** number
- **Description:** Returns the duration of the current source in seconds. This value will be the negative amount of DVR for LIVE. e.g. 15 minutes will be represented as -900 seconds.

### getLogLevel

---

- **Parameter(s):** none
- **Return type:** [Vuplay.LogLevel](/en/latest/api/eventtype.html#log-eventtype)
- **Description:** Returns the current log level of vuplay smart.

### getOpenChannels

---

- **Parameter(s):** none
- **Return type:** Array
- **Description:** Returns an array of the currently open channels

### getPlayerKey

---

- **Parameter(s):** none
- **Return type:** string
- **Description:** Returns the current player key from the configuration object.

### getSrc

---

- **Parameter(s):** none
- **Return type:** string
- **Description:** Returns the stream url. It might be different to the src url that is set via setSrc due to environment.

### getTextTracks

---

- **Parameter(s):** none
- **Return type:** Array\<[TextTrack](/en/latest/api/smart.html#texttrack)>
- **Description:** Returns an array of the loaded text-tracks.

### getUtcTime

---

- **Parameter(s):** none
- **Return type:** Date
- **Description:** Returns the current time in UTC. Not supported by all players.

### getVolume

---

- **Parameter(s):** none
- **Return type:** number
- **Description:** Returns the volume of the loaded player. The value will be between 0 and 1.

### getVudrmToken

---

- **Parameter(s):** none
- **Return type:** string
- **Description:** Returns the current vudrm token.

### isFullScreen

---

- **Parameter(s):** none
- **Return type:** boolean
- **Description:** Returns the value of full-screen. If true the player is currently fullscreen.

### isLive

---

- **Parameter(s):** none
- **Return type:** boolean
- **Description:** Returns whether the current stream is LIVE.

### isPaused

---

- **Parameter(s):** none
- **Return type:** boolean
- **Description:** Returns true is the currently loaded content is paused or stopped.

### off

---

- **Parameter(s):** eventType: [EventType](/en/latest/api/eventtype.html), event: [Event](/en/latest/api/events.html), handler: function
- **Return type:** void
- **Description:** [Unsubscribe from an event](/en/latest/api/events.html#unsubscribe-from-an-event).

### on

---

- **Parameter(s):** eventType: [EventType](/en/latest/api/eventtype.html), event: [Event](/en/latest/api/events.html), handler: function
- **Return type:** void
- **Description:** [Subscribe to an event](/en/latest/api/events.html#subscribe-to-an-event).

### pause

---

- **Parameter(s):** none
- **Return type:** void
- **Description:** Will pause the current content if playing, if not currently playing no action will be taken.

### play

---

- **Parameter(s):** none
- **Return type:** void
- **Description:** Will start the source playing, if the source is loaded.

### removeSocketChannel

---

- **Parameter(s):** channel: string
- **Return type:** void
- **Description:** Stop listening to the push notifications for the passed channel.

### reset

---

- **Parameter(s):** none
- **Return type:** void
- **Description:** Resets the config and clears the current content. Will stop any loaded stats plugins.

### scheduleAd

---

- **Parameter(s):** adType: [AdEventType](/en/latest/plugins/ads/#ad-events), vastUrl: string, startTime: number, skipTime: number
- **Return type:** void
- **Description:** Schedules an ad. See the [Ads section](/en/latest/plugins/ads/) for usage.

### seek

---

- **Parameter(s):** seconds: number
- **Return type:** void
- **Description:** Sets the current time of the player in seconds. This should be positive for VOD or negative for Live.

### setAudioTrack

---

- **Parameter(s):** id: number
- **Return type:** void
- **Description:** Sets the audio-tracks of the loaded source. The ID can be found by calling getAudioTracks.

### setAutoStart

---

- **Parameter(s):** autoStart: boolean
- **Return type:** void
- **Description:** Sets the autostart value of the content, must be called before the content is loaded.

### setClipEnd

---

- **Parameter(s):** seconds: number
- **Return type:** number
- **Description:** Sets the clipping marker end position.

### setClipStart

---

- **Parameter(s):** seconds: number
- **Return type:** number
- **Description:** Sets the clipping marker start position.

### setFullScreen

---

- **Parameter(s):** fullscreen: boolean
- **Return type:** void
- **Description:** If passed true the player will enter fullscreen mode. Setting false will exit fullscreen mode.

### setLogLevel

---

- **Parameter(s):** logLevel: [Vuplay.LogLevel](/en/latest/api/eventtype.html#log-eventtype)
- **Return type:** void
- **Description:** Sets the level at which vuplay smart will output logs.

### setSrc

---

- **Parameter(s):** src: string
- **Return type:** void
- **Description:** Sets the source to be used by vuplay smart. This will cause the current content to be stopped.

### setStatsConfigs

---

- **Parameter(s):** statsConfigs: { [ statsPluginId: string ]: object }
- **Return type:** void
- **Description:** Sets the stats configs. Will override any previously set stats configs.

### setTextTrack

---

- **Parameter(s):** id: number
- **Return type:** void
- **Description:** Sets the text-tracks of the loaded source. The ID can be found by calling getTextTracks.

### setup

---

- **Parameter(s):** config: [Configuration](/en/latest/api/config.html), containerDiv: HTMLDivElement
- **Return type:** void
- **Description:** Sets up vuplay smart using the provided [Configuration](/en/latest/api/config.html) object and container.

### setVolume

---

- **Parameter(s):** volume: number
- **Return type:** void
- **Description:** Sets the volume of the loaded player. The value should be between 0 and 1.

### setVudrmToken

---

- **Parameter(s):** vudrmToken: string
- **Return type:** void
- **Description:** Sets the token to be used as part of the license request.

### skipCurrentAd

---

- **Parameter(s):** none
- **Return type:** boolean
- **Description:** Skips the current playing ad. Will return true if the skip is allowed. Ads cannot be skipped before the skipTime is reached.

### skipTo

---

- **Parameter(s):** seconds: number
- **Return type:** void
- **Description:** Jumps to an earlier or later moment in the stream by a defined number of seconds in relation to the current moment being watched.

### startCasting

---

- **Parameter(s):** castType: CastType, title: string
- **Return type:** void
- **Description:** Starts casting to the specified cast type. Sets the title to be displayed on the cast device.

### startStatsMonitoring

---

- **Parameter(s):** none
- **Return type:** void
- **Description:** Starts all stats plugins that have been configured.

### stopCasting

---

- **Parameter(s):** none
- **Return type:** void
- **Description:** Stops casting on the currently casting device.

### stopStatsMonitoring

---

- **Parameter(s):** none
- **Return type:** void
- **Description:** Stops all stats plugins that have been configured.

## TextTrack

The text track object is not available to instantiate but is returned by the call to `getTextTracks`.

| Property      | Description                                                                                                      | Type      |
|---------------|------------------------------------------------------------------------------------------------------------------|-----------|
| id            | Unique identifier                                                                                                | number    |
| lang          | [Two letter ISO 639-1 language code](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes)                      | string    |
| label         | Friendly language name.                                                                                          | string    |
| kind          | The kind of text track. Value will depend on the player loaded.                                                  | string    |
| defaultTrack  | Determines whether text-track is default. If true the first default text track will be displayed automatically.  | boolean   |

## AudioTrack

The audio track object is not available to instantiate but is returned by the call to `getAudioTracks`.

| Property      | Description                                                                                 | Type      |
|---------------|---------------------------------------------------------------------------------------------|-----------|
| id            | Unique identifier                                                                           | number    |
| lang          | [Two letter ISO 639-1 language code](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) | string    |
| isActive      | Determines whether audio-track is active                                                    | boolean   |

## Duration, Current time and Seeking

<div class="admonition hint">
    <p class="first admonition-title">Tip</p>
    <p class="last">When dealing with a mixture of Live and VOD content, the values returned from <code class="docutils literal notranslate"><span class="pre">getDuration</span></code> and <code class="docutils literal notranslate"><span class="pre">getCurrentTime</span></code> are slightly different.</p>
</div>

The differences effect how you should deal with seeking. The explanations below should give you a better understanding of how we handle the differences, and how you should use vuplay smart when seeking.

### VOD

In VOD the timings are the simplest to explain and use.

#### VOD duration

The start of the content is represented by 0.
`getDuration` will return the length of the content in seconds.

#### VOD current time

`getCurrentTime` in a VOD stream, is the positive position in the stream, returned in seconds.

#### VOD seeking

To seek through a VOD stream simply pass the positive point in seconds you wish to seek to, `seek` will update the players position.

### Live

Live timings work on a negative basis with the LIVE edge being treated as 0.

#### Live duration

Live timings are different due to the introduction of the DVR Window.
The DVR window is a set time range that the player is allowed to seek within.
`getDuration` will return the length of the DVR window as a negative number, for example content with a DVR Window of 10 minutes will return -600.

#### Live current time

`getCurrentTime` will return a negative position in the stream, returned in seconds. The player will never be able to be at the LIVE edge (0) so expect values such as -4 etc.

#### Live seeking

Seeking through a Live stream is slightly different but following on from the concepts above, a negative number between the DVR Window and the LIVE edge (0) should be provided. So using our example above of a DVR Window of 10 minutes (600 seconds) if we were to provide `seek` with -300 we would expect to seek back 50% of the DVR Window.

## Push Notifications

Vuplay smart is capable of receiving push notifications. The following example demonstrates how to listen to the push notifications:

``` javascript
(function () {
    // generic event listener for non-channel specific socket events
    function onEvent(event) {
        if (window.console && window.console.info) {
            console.info(event);
        }
    }

    // event listener for push notification messages
    function onSocketMessageEvent(event) {
        if (window.console && window.console.info) {
            console.info("push notification received", { channel: event.args.channel, message: event.args.message });
        }
    }

    // create vuplay smart
    var vuplaySmart = new Vuplay.Smart("<player-key>", Vuplay.LogLevel.WARN);

    // add event listeners for the push notification events
    vuplaySmart.on(Vuplay.EventType.SOCKET, Vuplay.Events.socketconnect, onEvent);
    vuplaySmart.on(Vuplay.EventType.SOCKET, Vuplay.Events.socketreconnect, onEvent);
    vuplaySmart.on(Vuplay.EventType.SOCKET, Vuplay.Events.socketerror, onEvent);
    vuplaySmart.on(Vuplay.EventType.SOCKET, Vuplay.Events.socketdisconnect, onEvent);
    vuplaySmart.on(Vuplay.EventType.SOCKET, Vuplay.Events.socketping, onEvent);
    vuplaySmart.on(Vuplay.EventType.SOCKET, Vuplay.Events.socketpong, onEvent);
    // this last event contains the actual message
    vuplaySmart.on(Vuplay.EventType.SOCKET, Vuplay.Events.socketmessage, onSocketMessageEvent);

    // set the channel you want to receive the notifications from
    vuplaySmart.addSocketChannel("<channel>");

    var config = {
        src: "<mpeg-dash-url>",
        vudrmToken: "<vudrm-token>",
        autoStart: true
    };

    vuplaySmart.setup(config, document.getElementById("vuplay-container"));
})();

```

You can then stop listening to a channel:

``` javascript
vuplaySmart.removeSocketChannel("<channel>");
```