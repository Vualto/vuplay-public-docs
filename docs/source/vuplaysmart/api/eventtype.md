# Event Type

The events exposed by vuplay smart have been categorised into event types in order to improve performance.
They can accessed through the `Vuplay.EventType` enum.

| Type   | Description                                                                                                             |
|--------|-------------------------------------------------------------------------------------------------------------------------|
| VUPLAY | These are events that are related to the vuplay smart instance rather than a player.                                    |
| MEDIA  | Media events are related to the player and playback of the content.                                                     |
| ERROR  | An event type of error indicates a fatal problem in the player. vuplay smart is not expected to recover.                |
| LOG    | Logging events from the player. These will be printed to the console depending on the [LogLevel](/en/latest/api/loglevel.html)              |
| AD     | These are ad specific events see the [Ad Events](/en/latest/plugins/ads/#ad-events)  section for the information on the events and event types. |
| SOCKET | These are events for the push notifications.                                                                            |

## Vuplay EventType

The vuplay event object cannot be instantiated. It is passed to an event handler function that has been subscribed to an [event type](/en/latest/api/eventtype.html)  of `Vuplay.EventType.VUPLAY` using the `on` method on the [Smart](/api/smart.html) object.

| Property      | Description                                                                                                                                                                  | Type                    |
|---------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------|
| date          | The time and date of when the event was generated.                                                                                                                           | Date                    |
| type          | The type of event.                                                                                                                                                           | [EventType](/en/latest/api/eventtype.html)  |
| name          | The event name.                                                                                                                                                              | [Event](/en/latest/api/events.html)         |
| args          | Extra information from the event. This will vary depending on the loaded player. See the args column in the [event](/en/latest/api/events.html)  table for information provided by every player. | object                  |
| playerId      | The ID of the player loaded.                                                                                                                                                 | string                  |

## Media EventType

The vuplay event object cannot be instantiated. It is passed to an event handler function that has been subscribed to an [event type](/en/latest/api/eventtype.html)  of `Vuplay.EventType.MEDIA` using the `on` method on the [Smart](/en/latest/api/smart.html) object.

| Property      | Description                                                                                                                                                                  | Type                    |
|---------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------|
| date          | The time and date of when the event was generated.                                                                                                                           | Date                    |
| type          | The type of event.                                                                                                                                                           | [EventType](/en/latest/api/eventtype.html)  |
| name          | The event name.                                                                                                                                                              | [Event](/en/latest/api/events.html)         |
| args          | Extra information from the event. This will vary depending on the loaded player. See the args column in the [event](/en/latest/api/events.html)  table for information provided by every player. | object                  |

## Error EventType

The vuplay event object cannot be instantiated. It is passed to an event handler function that has been subscribed to an [event type](/en/latest/api/eventtype.html)  of `Vuplay.EventType.ERROR` using the `on` method on the [Smart](/en/latest/api/smart.html) object.

| Property      | Description                                                                                                                                                                  | Type                    |
|---------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------|
| date          | The time and date of when the event was generated.                                                                                                                           | Date                    |
| type          | The type of event.                                                                                                                                                           | [EventType](/api/eventtype.html)  |
| name          | The event name.                                                                                                                                                              | [Event](/api/events.html)         |
| args          | Extra information from the event. This will vary depending on the loaded player. See the args column in the [event](/en/latest/api/events.html)  table for information provided by every player. | object                  |
| message       | A friendly error message.                                                                                                                                                    | string                  |

## Log EventType

The vuplay event object cannot be instantiated. It is passed to an event handler function that has been subscribed to an [event type](/en/latest/api/eventtype.html)  of `Vuplay.EventType.LOG` using the `on` method on the [Smart](/en/latest/api/smart.html) object.

| Property      | Description                                                                                                                                                                  | Type                    |
|---------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------|
| date          | The time and date of when the event was generated.                                                                                                                           | Date                    |
| logLevel      | The level of the log. Error logs will be published as error events.                                                                                                          | [LogLevel](/en/latest/api/loglevel.html)    |
| name          | The event name.                                                                                                                                                              | [Event](/en/latest/api/events.html)         |
| args          | Extra information from the event. This will vary depending on the loaded player. See the args column in the [event](/en/latest/api/events.html)  table for information provided by every player. | object                  |
| message       | A friendly log message.                                                                                                                                                      | string                  |

## Socket EventType

The vuplay event object cannot be instantiated. It is passed to an event handler function that has been subscribed to an [event type](/en/latest/api/eventtype.html)  of `Vuplay.EventType.SOCKET` using the `on` method on the [Smart](/en/latest/api/smart.html) object.

| Property      | Description                                                                                                                                                                  | Type                    |
|---------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------|
| date          | The time and date of when the event was generated.                                                                                                                           | Date                    |
| name          | The event name.                                                                                                                                                              | [Event](/en/latest/api/events.html)         |
| args          | This will contain information about the socket. If the event is name is `socketmessage` it will contain the actual message from the push notification and the channel.       | object                  |
