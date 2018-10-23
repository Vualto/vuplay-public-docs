# Events

## Event Usage

### Subscribe to an event

You can subscribe to the events by using the `on` method on the [Smart](/en/latest/api/smart.html) object.

``` javascript
var handler = function(event) {
    console.log(event);
}

var vuplaySmart  = new Vuplay.Smart(Vuplay.LogLevel.WARN);
vuplaySmart.on(Vuplay.EventType.VUPLAY, Vuplay.Events.playerready, handler);
```

We recommend the use of named functions for the handler. You will not be able to unsubscribe from the event without using named functions.
When an event occurs the handler will be called and passed an object. The type of object will depend on the event type. The possible are types are [Vuplay Event](/en/latest/api/eventtype.html#vuplay-eventtype) , [Media Event](/en/latest/api/eventtype.html#media-eventtype) or [Error Event](/en/latest/api/eventtype.html#error-eventtype).

### Unsubscribe from an event

If you have subscribed to an event using a named function you will be able to unsubscribe from an event using the `off` method on the [Smart](/en/latest/api/smart.html) object.

``` javascript
var handler = function(event) {
    console.log(event);
}

var vuplaySmart  = new Vuplay.Smart(Vuplay.LogLevel.WARN);
vuplaySmart.on(Vuplay.EventType.MEDIA, Vuplay.Events.timeupdate, handler);
vuplaySmart.off(Vuplay.EventType.MEDIA, Vuplay.Events.timeupdate, handler);
```

## Events name

There are a number of events that are exposed by vuplay smart. The events can be access through `Vuplay.Events`.
In the table below the events are listed, the args column details the extra parameters that *every* loaded player will return.
Some players may return more information than detailed in the args column.

| Name              | Description                                                                                                                  | [EventType](/en/latest/api/eventtype.html)  | Arguments                        |
|-------------------|------------------------------------------------------------------------------------------------------------------------------|-------------------------|----------------------------------|
| playerready       | Fired when the player is ready.                                                                                              | VUPLAY                  | playerId: string                 |
| error             | Fired when an error occurs, an error message and an array of relevant data will be returned.                                 | ERROR                   | none                             |
| canplay           | Fired when the player is ready to play i.e. content is loaded and all required data is in place.                             | MEDIA                   | none                             |
| loadsrc           | Fired when a new src is about to be loaded in the player.                                                                    | MEDIA                   | src: string                      |
| playing           | Fired when playback starts.                                                                                                  | MEDIA                   | currentTime: number              |
| play              | Fired when playback starts after a pause event.                                                                              | MEDIA                   | currentTime: number              |
| pause             | Fired when playback is paused. The `ended` property indicates if the content has paused due to completing playback.          | MEDIA                   | ended: boolean                   |
| seeking           | Fired when a seek operation begins.                                                                                          | MEDIA                   | currentTime: number              |
| seeked            | Fired when a seek operation completes.                                                                                       | MEDIA                   | currentTime: number              |
| ratechange        | Fired when playback speed changes.                                                                                           | MEDIA                   | none                             |
| progress          | Fired when periodically to update current progress through the content.                                                      | MEDIA                   | currentTime: number              |
| timeupdate        | Fired when the element's currentTime attribute has changed.                                                                  | MEDIA                   | currentTime: number              |
| ended             | Fired when the current playback completes.                                                                                   | MEDIA                   | none                             |
| loadedmetadata    | Fired when all metadata about the stream has finished loading.                                                               | MEDIA                   | none                             |
| loadeddata        | Fired when the first fragments have finished loading.                                                                        | MEDIA                   | none                             |
| volumechange      | Fired when the audio volume changes.                                                                                         | MEDIA                   | volume: number                   |
| texttrackadded    | Fired when a text track is added to the video element.                                                                       | MEDIA                   | none                             |
| bufferstart       | Fired when playback data has started preloading.                                                                             | MEDIA                   | currentTime: number              |
| bufferend         | Fired when playback data has finished preloading.                                                                            | MEDIA                   | currentTime: number              |
| fullscreenchanged | Fired when the player enters or exits fullscreen mode.                                                                       | MEDIA                   | isFullScreen: boolean            |
| audiotrackchanged | Fired when a new audiotrack is set as active.                                                                                | MEDIA                   | none                             |
| clip             | Fired when a marker is moved. (url will be returned only with LIVE, start and end times will be appended in UTC)              | MEDIA                   | clipStartTime: number, clipEndTime: number, url?: string |
| log               | Fired when a log is published.                                                                                               | LOG                     | none                             |
| socketconnect     | Fired when the push notification socket is connected.                                                                        | SOCKET                  | none                             |
| socketreconnect   | Fired when the socket is trying to reconnect or has reconnected.                                                             | SOCKET                  | attemptNumber: number            |
| socketerror       | Fired when a socket error is detected.                                                                                       | SOCKET                  | error: object                    |
| socketdisconnect  | Fired when the socket disconnects. If there are no active channels then the socket will automatically disconnect.            | SOCKET                  | reason: string                   |
| socketping        | Fired when a socket ping is performed.                                                                                       | SOCKET                  | none                             |
| socketpong        | Fired when a response to the ping is received.                                                                               | SOCKET                  | latencyMilliseconds: number      |
| socketmessage     | Fired when a push notification is received through the socket.                                                               | SOCKET                  | channel: string, message: object |
| texttrackchanged  | Fired when the text track is changed, this includes disabling the text tracks.                                               | MEDIA                   | trackId: number                  |
| castloaded        | Fired when the cast framework has loaded                                                                                     | CAST                    | castType: Vuplay.CastType        |
| castavailable     | Fired when a casting device is detected (chrome only)                                                                        | CAST                    | state: cast.framework.CastState  |
| castunavailable   | Fired when no cast device is detected (chrome only)                                                                          | CAST                    | state: cast.framework.CastState  |
| caststart         | Fired when the cast has started                                                                                              | CAST                    | castType: Vuplay.CastType        |
| castend           | Fired when the cast has ended                                                                                                | CAST                    | castType: Vuplay.CastType, currentTime: number |

See the [Ad Events](/en/latest/plugins/ads/#ad-events) section for the ad specific events.