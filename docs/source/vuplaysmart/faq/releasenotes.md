# Release Notes

## 1.15.0 

* Rewrite of the wrappers surrounding THEOplayer

## 1.13.14-PreRelease

* Add support for wrappers that rely on container div rather that player div.
* Fix bug where comScore labels were not being set.

## 1.13.8-PreRelease

* Add a `skipTo()` method to jump to an earlier or later moment in the stream by a defined number of seconds in relation to the current moment being watched. This feature is supported in both VOD and LIVE streams.

## 1.13.6-PreRelease

* Fix bug where THEOplayer-HLS wrapper would fetch the wrong DIV element in certain instances on iOS.

## 1.13.4-PreRelease

* Modify THEOplayer-HLS wrapper to handle fullscreen requests from a player with no skin.

## 1.13.2-PreRelease

* Update docs and release notes.

## 1.13.1-PreRelease

* Add support for AT-Internet statistics plugin.

## 1.12.21-PreRelease

* Modify VIASAT skin type to use the Menu Translation json.

## 1.12.18-PreRelease

* Fix support for dash.js v2.6.x and TTML subtitles.

## 1.12.10-PreRelease

* Remove source map loader from release build.
* Fix audio language not being set correctly when using the VIASAT skin.

## 1.12.9-PreRelease

* Audio and Text track menus split in VIASAT skin.
* Change events for showing audio and text track menus in VIASAT skin.
* Fix in vuplay hls wrapper for Safari adding a blank text track when content has no text tracks.
* Fix audio menu not appearing in VIASAT skin when using vuplay hls
* Fix text track menu not appearing in VIASAT skin when using vuplay hls.

## 1.12.8-PreRelease

* fix regression in for multiple scripts loading Chromecast.

## 1.12.4-PreRelease

* fix for Chromecast recast

## 1.12.3-PreRelease

* fix for Chromecast seeking

## 1.12.2-PreRelease.4a78ea4

* fix for YouTube, player container height and width styles.
* fix for CIM config invalid blocking Comscore.

## 1.12.0-PreRelease.14afe93

* removes castavailable event.
* removes castready event.
* adds castloaded event.
* adds viasat skin

## 1.11.2-PreRelease.51d2050

* fixes subtitles and audio button display.
* fixes Chromecast castready event not firing issue.

## 1.11.0-PreRelease.373409a

* introduces the GoosensContainer to handle _singleton dependencies_.
* introduces the ability to have multiple instances of _vuplay smart_ on a single page.
* introduces the `smartId` identifier for each _vuplay smart_ instance.
* fixes Chromecast plugin to allow _play, pause, seeking & volumecontrols_ in new firmware version.
* fixes cim config validation issue _CIM identifier_ is an optional config setting

## 1.10.2-PreRelease.95a7d05

* Promise polyfill is now automatically added to all modules.
* Fixes for the Europarl skin.

## 1.10.1-PreRelease.1b2f51c

* Webpack updated to version 3.
* Multiple dependencies updated.
* Demo page updated to add ability to select skin.
* Europarl skin added to vuplay smart.

## 1.10.0-PreRelease.4d507eb

* Push notification functionality added.

## 1.9.8-PreRelease.5bc9c5a

* Demo files copied on build.
* Remove README.docx.
* `loadScript` function moved to helper class.
* `isChrome` function moved to helper class.
* Fix incorrect import for `AdManager`.
* Fix "Promise undefined" error in IE11.
* `Vuplay.Smart.getLive` method will now attempt to use USP's `/state` url and fallback to checking for the `isml` in the url.

## 1.9.4-PreRelease.30e48f1

* Audio tracks will take time to switch when loading dash.js. See [dash.js github issue](https://github.com/Dash-Industry-Forum/dash.js/issues/1639).
* Fix text track menu not displaying correctly in `Vuplay.SkinType.VUPLAY` when loading a new source in dash.js (requires dash.js v2.5.0).
* Fix multiple audio flags being added in `Vuplay.SkinType.VUPLAY` when loading a new source in dash.js.

## 1.9.1-PreRelease.9f940de

* Add `audiotrackchanged` event.
* Add `fullscreenchanged` event.
* Fix for Chromecast plugin loading in all browsers.
* Fix for multi-audio button being recreated when it already exists.
* Fix typos in documentation.

## 1.8.3-PreRelease.36bbfa1

* Exposes `isLive`.
* Fix ios10 fullscreen bug.

## 1.8.2-PreRelease.1269c53

* Adds Chromecast default receiver support
* Adds [YouTube iframe player](https://developers.google.com/youtube/iframe_api_reference) support.
* Fix error message for invalid setup configuration. The vudrm token is not required.
* Fix live times being reported wrong when loading THEOplayer.
* Fix `Promise` not being polyfilled correctly when loading CIM and Comscore stats plugins.

## 1.7.0-PreRelease.2a66c3

* New advanced vuplay skin with multi-audio and text track support added.
* `loadSkin` config option replaced by `skin` option.
* Add vuplay hls multi-audio track support.
* Fix vuplay hls text track support.

## 1.6.0-PreRelease.c35c3b7

* Support for VAST ads with THEOplayer added.

## 1.5.6-PreRelease.bb9a278

* Call `playHandler` in youbora plugin when content is restarted after an `ended` event.
* Fix duplication of `getPlayhead` handler method in youbora plugin.

## 1.5.5-PreRelease.5cec20f

* Fix dashjs not reporting `ended` event on some USP VOD content.

## 1.5.4-PreRelease.4f61f2f

* Fix dashjs reset not reattaching the video element.

## 1.5.3-PreRelease.7d7495e

* Fix `bufferend` event firing before `bufferstart` when using THEOplayer.
* Fix buffering icon not displaying correctly in Safari.
* Fix Youbora not detecting buffer ends correctly.

## 1.5.2-PreRelease.a431da1

* Fix buffer and seek ended handlers not being called in the Youbora plugin.

## 1.5.1-PreRelease.56992df

* `getUtcTime` method added. This will return the current UTC time for the playing video. Only supported by theoplayer and dash.js currently.
* Fix firing of Youbora jointime. Start will now fire when the src is loaded into the player, JoinTime will fire when the video starts playing.
* Fix buffer and seek handlers not being called in the Youbora plugin when buffering and seeking completes.

## 1.5.0-PreRelease.af9c888

* Cim support added. contact [support@vualto.com](mailto:support@vualto.com) for more information.
* Optional params on `Smart` constructor removed.
* Fix Youbora plugin not reporting a live stream correctly.
* Fix player not loading if css url from API is null or an empty string.
* Fix for incorrect live times being returned by multiple players.

## 1.4.6-PreRelease.7d0901e

* `getSrc` will now return the url that is actually used by the player. This could be different from the set url as it may have been changed to Smooth Stream or HLS depending on the loaded player.
* Fix youbora being sent the wrong url if the stream type used is not MPEG-dash.

## 1.4.5-PreRelease.9a407ce

* `progress` event will return the current time as part of the event args.
* Clicking the volume bar while muted will set the volume.
* Fire warning if accessing THEOplayer's live times too early.
* Controls will hide if pointer is above the video and not moving after 3 seconds.
* Fire warning when no accountcode is passed in Youbora stats config.
* THEOplayer progress events will contain data about how much video has been buffered.
* Remove check against stream type when setting the source on THEOplayer.
* Fix text tracks not being hidden correctly on THEOplayer.
* Fix current times for events from THEOplayer when the stream is live.
* Fix incorrect state being set on the play/pause button.

## 1.4.4-PreRelease.6d7c903

* Update vuplay HLS support to include all functionality except live time support, text track support and multi audio track support.
* Warning will be fired if SSL is not detected on the containing page's url.

## 1.4.3-PreRelease.e60cc74

* Comscore support added. Contact [support@vualto.com](mailto:support@vualto.com) for more information.
* Default skin css url comes from the API call.
* Throw an error if stats config is not a javascript object.
* Display error if `loadSkin` is true and no player can be loaded for the environment.
* Fix null reference error when no player can be loaded for the environment.
* Fix wrong version number used in Youbora stats plugin.
* Fix THEOplayer HLS not returning text track ids.

## 1.4.2-PreRelease.2fc4caa

* Add support for vuplay-hls. This does not include subtitle or multiple audio support.
* Fix the default skin not handling text tracks being added.
* Bring setting selected text track inline with dash.js docs.
* Fix IE11 support for default skin by importing the promise polyfill.
* Fix IE11 fullscreen controls not displaying.
* Check `head` html tag exists before adding skin css link.
* Bring live times for THEOplayer inline with other players.
* Fix player height being 0px when loading THEOplayer HLS.

## 1.4.0-PreRelease.06f89fa

* `loadSkin` option added to the setup configuration.
* Default skin added. It will not be used by default but can be added by setting the `loadSkin` configuration option in the setup.
* Stats plugin's configs must be passed through `setStatsConfigs`
* Added a `stopStatsMonitoring` method that will stop the loaded stats plugins from sending stats.
* Renamed the `startAllStatsMonitoring` to `startStatsMonitoring`
* Calling `reset` will call `stopStatsMonitoring` internally.

## 1.3.1-PreRelease.ca6c9e9

* Fix KID being null in some cases on widevine license request.
* Fix logging error where logs were tagged as media events.
* Add Promise polyfill to support Promises on IE11.

## 1.3.0-PreRelease.5edb413

* Support vuplay silverlight. Please note that the player *must* be loaded over https for silverlight to load.
* Logging now uses the event bus.
* Transformation of mpeg-dash stream url will now use regex for matching. The regex is configured in central config on a per client per player basis.

## 1.2.3-PreRelease.c8a8a88

* Player Key should not be passed through the constructor.
* Supports Youbora stats engine.

## 1.1.2-PreRelease.7901c78

* Support instream text tracks.
* Support multi-audio streams.
* Change port on dev server.
* Expose fullscreen functionality.
* `texttrackadded`, `bufferstart`, `bufferend` events added.
* Logging an error will cause the error event to fire.
* Fix `isPaused` method not returning a value.
* Fix issue with unsubcribing events. Named functions *must* be used.
* Fix issue with seeking causing buffer end to fire in dash.js.

## 1.1.1-PreRelease.0c80b68

* Removes min from vuplay smart output javascript file.
* Automation of docs creation on build
* Adds volume controls
* Exposes event handling.
* Maps THEOplayer events to exposed events
* Supports THEOplayer v2.8.5
* Supports dash.js v2.4.1
* Fixes issue with event bus handler publishing
* Fixes bugs with event publish
* Fixes around not passing a vudrm token.

## 1.0.1-PreRelease.7dd4342

First release!

* Supports THEOplayer v2.8.1
* Basic command support.

## 1.4.0-PreRElease.06f89fa

* Default skin added. It will not be used by default but can be added by setting the `loadSkin` configuration option in the setup.
* `loadSkin` option added to the setup configuration.
* Adds LIVE/VOD stream detection
* Fixes duration return for LIVE/VOD dash.js
* Stats plugin's configs must be passed through `setStatsConfigs`
* Added a `stopStatsMonitoring` method that will stop the loaded stats plugins from sending stats.
* Renamed the `startAllStatsMonitoring` to `startStatsMonitoring`
* Calling `reset` will call `stopStatsMonitoring` internally.

## 1.4.1-PreRelease.7b1b36a

* Fixes Promise undefined bug in deafult skin in IE 11.
* Fixes subtitles auto enabling bug in dash.js.
* Fixes text track detection bug in dash.js.

![Stormtroopocat](https://octodex.github.com/images/stormtroopocat.jpg "The Stormtroopocat")
