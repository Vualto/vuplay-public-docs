## Android SDK v1.1.1 (build 1304)

## Introduction

This documentation describes the steps to integrate and use the vuplay SDK for Android.

The Android SDK is provided as a Android Library (AAR) that can be quickly and simply integrated into your Android Studio project.  It also provides three distinct usage options:

1. A full screen player with built-in controls in the form of vuplayActivity
2. A view in the form of vuplayView that can be added anywhere in your layout and exposes an interface methods, 
   such as -play or -pause.
3. An advanced use case where the SDK will prepare an instance of Exoplayer and asynchronously return this to you.

Please contact support@vualto.com to request a download of the SDK.

## Important Notice

 v0.9.3 is the last release that will support Android 4.1 - 4.3 OS versions. With version 1.0 of the SDK we will be moving minimum OS support to Android 4.4+.

As from v1.1 we have added ExoPlayer as an external dependency, this will require a gradle compile directive for ExoPlayer, please review Android studio integration instructions for further information.

## Project Requirements

* Minimum SDK version is 19 (Android 4.4)
* Android Studio 2.1.2
* If wishing to use Android 6 (M) You’ll need to grant the dangerous runtime permission READ_EXTERNAL_STORAGE 
  before consuming the SDK. Information on how to do this can be found in the Android documentation:
  http://developer.android.com/training/permissions/requesting.html
	
  Alternatively you can fallback to the old Android permissions model by specifying ‘targetSdkVersion 22’ in your applications gradle file.

## Android Studio Integration

* Ensure your scope is set to Project so you can see the whole project structure.  Add the 'vuplaySDK' AAR to  
   your 'libs' directory in your project.

* Go into your module's build.gradle file and add the following to the end of your file:

```
repositories{
    flatDir{
        dirs 'libs'
    }
}
```

* Add the following to your module's build.gradle files dependencies, then run Gradle sync and clean your 
   project:
      
```
  compile 'com.google.android.exoplayer:exoplayer:r1.5.12'
  compile 'com.vualto.vuplay:vuplaySDK-v1.1.1@aar'  
```

* If you are using proguard you will need to add the following rule when obfuscating:

```
-keepclasseswithmembers class com.google.android.exoplayer.ExoPlayerLibraryInfo {
	*;
}
```

## vuplayView usage

1. Add the vuplayView to your layout by clicking custom view in UI editor, select vuplayView and place where 
   desired.

2. Import the vuplaySDK into your player:

	*import com.vualto.sdk.vuplay.InvalidVideoConfigurationException;*
    
    *import com.vualto.sdk.vuplay.VideoConfiguration;*
    
    *import com.vualto.sdk.vuplay.vuplayView;*

3. Reference the view in your activity as syou would any other view.

    *_vuplayView = (vuplayView) findViewById(R.id.vuplayview);*
    
4. Create a new VideoConfiguration object in your onCreate call:

    *VideoConfiguration _videoConfiguration = new VideoConfiguration("Your stream URL here");*

    If you are playing encrypted content you will need to provide a DRM token, an optional second parameter is available to do so in the VideoConfiguration constructor:

    *VideoConfiguration _videoConfiguration = new VideoConfiguration("Your stream URL here", "Your DRM Token here");*

    If you wish to specify a different license server, an optional third parameter is available to do so in the VideoConfiguration constructor:
    
    *VideoConfiguration _videoConfiguration = new VideoConfiguration("Your stream URL here", "Your DRM Token here", "Your license server URL here");*
    
5. (Optionally) To receive callbacks from onPrepared, onCompleted, onError, onSeekComplete or onInfo implement the 
    native android MediaPlayer event listeners.

    Then pass the instance into vuplayView using the addOnInfoListener, addOnErrorListener, addOnPreparedListener, addOnCompletionListener and onSeekCompleteListenermethods.

6.  Call initialise player on the vuplayView, passing the VideoConfiguration object and the current activity.  An 
    exception will be thrown if you have the wrong application permissions, a blank token or stream URL.

    ```
    try {
        _vuplayView.initialisePlayer(_videoConfiguration, this);
        } catch (InvalidVideoConfigurationException e) {
        e.printStackTrace();
        }
    ```

7. A stream cannot be resumed if paused, so onCreate is a good time to check if the stream is live or not by calling the 'canPause()' function on the vuplayView.

8. When the activity calls 'onStop()', ensure to call the 'stop()' function on the vuplayView object.


## vuplayActivity usage

1. Import vuplayActivity from the SDK into your project:

    *import com.vualto.sdk.vuplay.VideoConfiguration;*
    
    *import com.vualto.sdk.vuplay.vuplayActivity;*
      

2. Create a new VideoConfiguration object:

    *VideoConfiguration _videoConfiguration = new VideoConfiguration("Your stream URL here");*

    If you are playing encrypted content you will need to provide a DRM token, an optional second parameter is available to do so in the VideoConfiguration constructor:

    *VideoConfiguration _videoConfiguration = new VideoConfiguration("Your stream URL here", "Your DRM Token here");*

    If you wish to specify a different license server, an optional third parameter is available to do so in the VideoConfiguration constructor:

    *VideoConfiguration _videoConfiguration = new VideoConfiguration("Your stream URL here", "Your DRM Token here", "Your license server URL here");*
    
3. Create an Intent as you would to launch any other Android Activity, specifying vuplayActivity as the Class   
   parameter.
   
    *Intent intent = new Intent(yourContext, vuplayActivity.class);*
   
4. Put the video configuration object as a SerializableExtra, using
   VideoConfiguration.INTENT_KEY as the intent key, then launch the activity.

    *intent.putExtra(VideoConfiguration.INTENT_KEY, _videoConfiguration);
	startActivity(intent);*
    

## Out of band subtitle support for vuplayActivity

To add a subtitle to vuplay Activity, you will need to create an ArrayList of HashMaps with one hashmap of key and value type of String per arraylist entry. This list can then be passed as an extra intent to vuplay Activity. An Example flow of usage would be as follows:

*ArrayList<HashMap<String, String>> subtitleList = new ArrayList();*

*HashMap<String, String> hashMap = new HashMap();*

*hashMap.put("<Subtitle name>", "<Your subtitle URL here>");*

*subtitleList.add(hashMap);*

*intent.putExtra(vuplayActivity.OUT_OF_BAND_SUBTITLES, subtitleList);*

## Pro-active license acquisition for vuplayView

vuplayView currently supports the PIFF content type (eg, ISMV) and content produced by USP.

* An example usage flow would be the following in your onCreate method:

```
vuplayView.acquireLicence(Environment.getExternalStorageDirectory() + "/your_file_name.ismv”,
“Your DRM Token here”,
new ILicenceAcquisitionListener() {
    @Override
    public void onAcquisitionFinished(vuplayErrorCode error) {
        if (error == null) {
            Log.d(TAG, "Acquisition worked");
        } else {
            Log.d(TAG, "Failed: " + error.getValue());
        }
    }
  },
getApplicationContext()
);
```

* In your callback you then may then want to make use of vuplayView to play your content as normal:

```
_vuplayView.initialise(
    new VideoConfiguration(“Environment.getExternalStorageDirectory() + 
        "/your_file_name.ismv””),
    YourActivity.this
);
```

## Advanced usage for vuplaySDK

Starting with v1.1 of the SDK it is now possible to get direct access to the underlying instance of ExoPlayer after it has been prepared for playback. Eg:

```
vuplaySDK.playerWith(VideoConfiguration videoConfiguration,
        Activity activity,
        SurfaceHolder surfaceHolder,
        int timeout,
        new MediaCodecVideoTrackRenderer.EventListener()  {
        //Your code
        },

        new TextRenderer() {
            …
            //Your code
        },
        new vuplaySdk.InitialiseCompletionListener() {
        @Override

        public void initialiseComplete(final ExoPlayer exoPlayer, Exception error) {
    	   //Your code
        }});

```

When your completion handler is called, it is then your responsibility for managing its lifecycle and all events that occur. Eg, you will need to ensure it is ready for playback, or seeking.

Vualto will fully support the initial configuration and setup of the DRM integration for ExoPlayer.  However, our support ends once the reference to ExoPlayer is provided to you

**Optional parameters:**

* MediaCodecVideoTrackRenderer.EventListener can be null, see:     
  ```https://google.github.io/ExoPlayer/doc/reference/com/google/android/exoplayer/MediaCodecVideoTrackRenderer.EventListener.html```

* TextRenderer can be null, see:
    ```https://google.github.io/ExoPlayer/doc/reference/com/google/android/exoplayer/text/TextRenderer.html```
    

**Limitations:**

* Only works with unencrypted DASH or DASH streams encrypted with Widevine.

## vuplayErrorCode Enumeration

* Unknown error

    UNKNOWN(957000)

* Unable to connect to streaming server, check internet connection and try again.

    UNABLE_TO_READ_FROM_SOURCE(957004)

* There is no license to play this content and one could not be acquired from the supplied DRM parameters.
  
    REVOCATION_PACKAGE_INVALID(957005)

* Unable to ascertain the stream type

    UNKNOWN_STREAM_TYPE(957006)

* Unexpected HTTP status code, eg, 307 - HTTP1.1 redirect
  
    UNEXPECTED_HTTP_STATUS(957008)

* Invalid seek position
  
    INVALID_SEEK_POSITION(957009)

* The content URL you provided returned an HTTP 404 - Not Found
  
    CONTENT_HTTP_404(957010)

* The DRM protecting this media is not supported by this version of the SDK
    
    DRM_UNSUPPORTED(957011)

* Unable to retrieve full manifest from remote server.
  
    MANIFEST_INCOMPLETE(957013)

* "Device could not be individualised due to a server or connectivity issue."

    DEVICE_INDIVIDUALIZATION_ERROR(957015)

* No Support for PlayReady live content.
 
    NO_PLAYREADY_LIVE_SUPPORT(957016)

* Wait for existing completion handler callback before invoking again.
 
    WAITING_ON_PREVIOUS_COMPLETION_HANDLER(957019)

* Timeout exceeded whilst trying to prepare player.
 
    TIMEOUT_EXCEEDED(957020)
    
* The consumer has supplied a version of ExoPlayer which is not used by the SDK
 
    INVALID_EXOPLAYER_VERSION(957024)

* This version of the SDK only supports Widevine
 
    ONLY_SUPPORTS_WIDEVINE(957027)

* This version of the SDK only supports PlayReady
 
    ONLY_SUPPORTS_PLAYREADY(957028)


## Limitations

* The SDK does not support playback of protected content when running on an Android Virtual Device
    
## Known Issues

* On devices running 4.4 and above, the onCompleted callback is called three or so seconds after the content has actually finished - PlayReady DRM Only.

* Playback may not work on certain mobile networks (EE) - PlayReady DRM only.

* Seeking multiple times in quick succession will block the UI thread - PlayReady only.

* On the Asus 7 MeMoPad (4.4.2) DASH and Widevine DRM will not work.

* Offline license acquisition will not work on Android 7 and above - PlayReady DRM only.


## Notes

* To speed up device rotation you can set the xml attribute android:screenOrientation to fullSensor on the activity using the view. This bypasses the activity lifecycle on device rotation, which is where the player is recreated and causes a delay while loading.



## Devices tested on:

Internally

* Nexus 6P (7.0.1)
* Samsung Tab 10 A5 (6.0.1)
* Nexus 7 [2013] (6.0.1)
* Nexus 7 [2012] (5.1.1)
* Samsung Galaxy Tab 4 (4.4.2)
* Asus 10 MeMoPad (4.2.2)
* Asus 7 MeMoPad (4.4.2)
* Nexus 4 (5.0.1)
* Samsung S5 (5.0.2)
* Tesco Hudl (4.2.2)


Externally, by Microsoft for PlayReady DRM Only

* Nexus 9
*Nexus 7 2013
* Nexus 5
* Nexus 4
* Nexus 10
* Samsung Galaxy S5
* Samsung Galaxy S4
* Motorola Moto X
* LG G3
* LG G2


## Release Notes

**v1.1.1 (build 1304)**

* Improves compatibility of SDK with Android 7 and above
* Updates minimum ExoPlayer version to 1.5.12

**v1.1 (build 1282)**

* vuplayActivity features:

    * Subtitle and audio selectors now sort alphabetically
    * Clear option for disabling subtitles
    * Action bar and controls are displayed when playback is prepared
    

* vuplayView fixes:
    * when selecting audio languages from DASH manifest lang attribute is used for display as opposed to id.
    * VideoConfiguration now exposes two setters for configuring selected subtitle and audio track before playback. ‘setSelectedSubtitle(language)’ and ‘setSelectedLanguage(language)’ respectively.
    * Call to getLanguages now always returns an audio language when present.

* Added advanced use case for the SDK. See the ‘Advanced SDK usage’ section above.

* The current version of the vuplaySDK can be ascertained by calling vuplaySDK.version()

**v1.0 (build 890)**

* vuplayActivity features:	  

    * Support for DVR when using DASH and Widevine.       
    * Out of band subtitle support for SAMI subtitle format.       
    * Add support for external subtitles - see section ‘Out of band subtitle support for vuplay Activity’.
    * Setting the intent key of vuplayActivity.CONTENT_TITLE with a string parameter will set the title for vuplayActivity, if none is set no action bar will appear.
    * Dragging seek bar updates playback position.
    * Numerous UI Improvements.
    * Changes watermark drawable intent key from ‘INTENT_KEY’ to ‘WATERMARK’.
    * Updates to pause/stop graphic to represent type of stream played. When playing VOD will use pause icon, when playing live a stop icon.


* vuplayActivity fixes:
    * Screen no longer warps when tapping controls.

* vuplayView features:
    * Widevine encryption with DASH support.
    * Pro-active license acquisition - see section ‘Pro-active license acquisition for vuplay View’.
    * Subtitle API now has a call to getSubtitles. This will return an ArrayList of Strings containing the subtitles added using the addSubtitle call.

* vuplayView fixes:
    * Fixes issue where on mobile sized devices time would overflow onto new line.
    * Optimizations for subtitles.
    * Updates aspect ratio on bitrate change.
    * Improved error handling and reporting.

**v0.9.3 (build 454)**

 * Performance enhancements to subtitle parsing.

**v0.9.2 (build 450)**

 * Experimental support for Android 6 Marshmallow.
 
 * Improved reliability and performance of subtitles.

**v0.9.1 (build 417)**

* Improved responsiveness of player, especially on slow network connections.

* Updated vuplayView Demo to not display play/pause until the player is prepared and the content is not live.

**v0.9 (build 395)**

* Updated PlayReady SDK to 3.2.1.

* Add support for externally loaded WebVTT subtitles
    Call addSubtitle(language, url) at any time on a vuplayview instance, pass in the language name you wish to later select it as, and a url to the subtitle file. Inserting the same language name will replace the previous same named entry.

    The subtitle parser will only accept UTF-8 encoding.

    To select your added subtitle(s) simply call selectSubtitle(language) passing in the same language that has been used previously with addSubtitle.

* Performance optimisations for seeking and preparing content.
* Added error code enumeration for incomplete manifest retrieval.

**v0.8.2 (build 317)**

* Fixed rare timing issue with SDK initialisation that could result in a missed onPrepare callback.

* Fixed bug where the onError callback would happen on the wrong thread.

* Updated the default licence server used by the VideoConfiguration object if not specified to 
```http://playready-license.drm.technology/rightsmanager.asmx.```

**v0.8.1 (build 311)**

* Fixed bug where vuplayView class canSeekForward() and canSeekBackward() methods would always return false.

* Exposed method parameter names for vuplayView class.

* Fixed bug where seekTo() method would generate an onPrepared callback.
vuplayActivity changes:

* Fixed bug where tapping the multi-audio button would bring up multiple dialogs.

* Fixed bug where tapping twice was required to show the controls.

**v0.8 (build 293)**

* Improved accuracy and consistency of native android player events: MEDIA_INFO_BUFFERING_START, MEDIA_INFO_BUFFERING_END and MEDIA_INFO_VIDEO_RENDERING_START.

* Multi audio is now supported for Microsoft Smooth Streaming and DASH, to see if a stream has multi-audio tracks, call getLanguages() on the vuplayView object. If there is not multi audio streams this will return null. To change stream, call setSelectedLanguage() on vuplayView passing in one of the languages provided by getLanguages().

* Improved error handling, exposed vuplayErrorCode enumeration to provide matches for MediaPlayer.OnError ‘what’ codes. See vuplayErrorCode enumeration documentation above for further information.

* Fixed bug where a segfault would occur if canPause() was called while the player was not initialised.

* vuplayActivity changes:
    * Exposed multi audio option with a dialogue if there are multiple audio tracks present in the stream.
    * Error dialog now provides further information to the problem.
    * Fixed BinderProxy bug that can occur where a Dialogue tries to show when the Activity was in the wrong  lifecycle state.
    * Updated Stop graphic to a pause graphic.
    * Fixed aesthetics where Android Lollipop devices would display an older API version ProgressBar spinner.
    * Responsive UI for buffering and seek events.


**v0.7 (build 165)**

* Replaced isLive() call with canPause() call to mirror the native player’s interface.
* MPEG DASH encrypted and unencrypted streams now play.
* Event listeners can now be added before the initialisePlayer call.
* Added vuplayActivity class.

* vuplayActivity features:
    * Pause  / Start in VOD.
    * Seek in VOD.
    * VOD time tracking.
    * Vualto skin.
    * Playing live streams will replace the time tracking section with the text ‘LIVE’ and will disable the seekbar and set it to maximum.

**v0.6 (build 100)**

 * Improved scaling code
 * Update usage of PlayReady SDK to latest recommendations from Microsoft
 * Added event listeners for onInfo, onError, onCompletion, onPrepared and onSeekCompleted
 * vuplayView will now seek to a position provided in milliseconds
 * vuplayView getCurrentPosition / getDuration now return values in milliseconds

**v0.5 (build 44)**

 * Initial release


## Example Projects

*vuplayView Demo* - Demonstrates the vuplayView usage scenario. Edit the demo to insert your stream and token! Note that the controls are hidden when playing a live stream.

*vuplayActivity Demo* - Demonstrates the vuplayActivity usage Scenario. Edit the demo to insert your stream and token! You’ll have the features specified in vuplayActivity features in a player.






