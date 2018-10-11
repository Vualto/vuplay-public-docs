## iOS SDK v0.9.8 (build 636)

This documentation describes the steps to integrate and use the vuplay SDK for iOS.

## Introduction

The iOS SDK is provided as a static framework that can be quickly and simply integrated into your Xcode project.  The SDK was initially modelled after MPMoviePlayerController and MPMoviePlayerViewController.  However in iOS 9, Apple depreciated these APIs and provided a new direction in the form of AVPlayerViewController. As a result the SDK is gradually being remodelled to support Apple’s latest approach.

The SDK provides three distinct usage options:

1. A full screen player with built-in controls in the form of vuplayViewController.
2. A fully customisable player in form of vuplayController that can be sent messages, such as -play or -pause    
   and vends a view that can be added anywhere in your view hierarchy.
3. An advanced use case where the SDK will prepare a AVPlayer instance and asynchronously return this to you.

The SDK is fully supported in both Objective-C and Swift applications. Basic demos are provided in both languages. Advanced demos are not yet available for iOS.

Please contact support@vualto.com to request a download of the SDK.

## Project Requirements

  * Minimum iOS deployment target of 8.x or higher
  * Xcode 7.3.1 or higher

**Xcode Integration**

1. Copy the vuplaySDK.framework into your application's project directory
2. Drag the copied vuplaySDK.framework into the “Frameworks” group in your Xcode project and link against the  
   required targets
   
**Information about Application Transport Security (ATS)**

iOS 9 introduces Application Transport Security (ATS). In order to permit playback of content exemptions need to be added into your application's Info.plist.

If your content is delivered via HTTPS that meets Apple’s ATS guidelines, then the following exemption needs to be added for localhost:

```XML
<key>localhost</key>
<dict>
  <key>NSIncludesSubdomains</key>
  <true/>
  <key>NSTemporaryExceptionAllowsInsecureHTTPLoads</key>
  <true/>
</dict>
```

If your content is delivered via HTTP then you need need to add exemptions for this traffic.  For example to disable ATS for any connection you would add the following into your application's Info.plist:


```XML  
<dict>
  <key>NSAppTransportSecurity</key>
  <dict>
    <key>NSAllowsArbitraryLoads</key>
    <true/>
   </dict>
</dict>
```

More information about ATS can be found in Apple’s TechNote:

```URL
https://developer.apple.com/library/prerelease/ios/technotes/App-Transport-Security-Technote
```

## vuplayController usage (Objective-C)


1. Import the vuplaySDK into your player:

    @import vuplaySDK;

2. Create a new property for the vuplayController:

    @property (nonatomic, readwrite, strong) vuplayController *player;

3. Initialise an instance of vuplayController:

    self.player = [[vuplayController alloc] initWithURL:[NSURL URLWithString:@"<stream URL>"] token:@"<DRM token>"];

4. Add the vuplayController’s view into your view hierarchy:

    self.player.view.frame = CGRectMake(0, 20, self.view.bounds.size.width, self.view.bounds.size.height - 64);
    self.player.view.autoresizingMask = UIViewAutoresizingFlexibleHeight | UIViewAutoresizingFlexibleWidth;
    [self.view addSubview:self.player.view];

5. As vuplayController implements the MPMediaPlayback protocol you can now send it the -play message for it      to start playing your content.


## vuplayController usage (Swift)

1. Import the vuplaySDK into your player:

    import vuplaySDK


2. Initialise an instance of vuplayController:

    let player = vuplayController(address: "<stream URL>", token: "<DRM token>")

3. Add the vuplayController’s view into your view hierarchy:

    player.view.frame = CGRectMake(0, 20, view.bounds.size.width, view.bounds.size.height - 64)
    player.view.autoresizingMask = [.FlexibleHeight, .FlexibleWidth]
    view.addSubview(player.view)


4. As vuplayController implements the MPMediaPlayback protocol you can now call the play() function for it to 
   start playing your content.
   
## vuplayViewController usage (Objective-C)

1. Import the vuplaySDK:
    
    @import vuplaySDK;

2. Initialise an instance of vuplayController as above, then initialise an instance of vuplayViewController 
   and provide it with a reference to the vuplayController:

    vuplayController *player = [[vuplayController alloc] initWithURL:[NSURL URLWithString:@"<stream URL>"] token:@"<DRM token>"];
    vuplayViewController *playerViewController = [[vuplayViewController alloc] init];
    playerViewConrtoller.player = player;


3. Optionally, you can set a title for the content:

    playerViewController.title = @"<content title>";

4. Present the player view controller:

    [self presentViewController:playerViewController animated:YES completion:nil];


## vuplayViewController usage (Swift)

1. Import the vuplaySDK:

    import vuplaySDK
   
2. Initialise an instance of vuplayController as above, then initialise an instance of vuplayViewController    
   and provide it with a reference to the vuplayController:

    let player = vuplayController(URL: NSURL(string: "<stream URL>"), token: "<DRM token>")
    let playerViewController  = vuplayViewController()
    playerViewController.player = player
   
3. Optionally, you can set a title for the content:
    playerViewController.title = "<content title>"
    
4. Present the player view controller:

    presentViewController(playerViewController, animated: true, completion: nil)
    
## Limitations

* The SDK does not support playback of protected content when running in the iOS Simulator
* Xcode 7 introduces Bitcode, however this is not yet supported if you use PlayReady DRM and must be disabled.
    
## Known Issues

* The status bar is not hidden in vuplayViewController when hiding the player controls if UIViewControllerBasedStatusBarAppearance is not set in your application’s Info.plist


## Advanced SDK usage

Starting with v0.9.3 of the SDK it is now possible to get direct access to the underlying instance of AVPlayer after it has been prepared for playback. Eg:

```
    vuplaySDK.playerWithURL(
        NSURL,
        token: String?,
        licenseServer: NSURL?,
        timeout: NSTimeInternal) 
        { (AVPlayer?, NSError?) -> Void in
            // Your code
        }

```
When your completion handler is called, it is then your responsibility to for managing its lifecycle and all events that occur. Eg, you will need to ensure it is ready for playback, or seeking.


Vualto will fully support the initial configuration and setup of the DRM integration for AVPlayer.  However, our support ends once the reference to AVPlayer is provided to you.


## Limitations
*  Only works with unencrypted HLS streams or HLS streams encrypted with Fair Play Streaming


## Release Notes

**v0.9.8 (build 636)**

* Fix issue whereby no subtitles languages should be nil, but was an empty array
* Fixed issue with parsing subtitle tracks with non-ascii in their name (e.g., 'Bokmål Norwegian')
* Expose ‘allowsExternalPlayback’ and ‘isExternalPlaybackActive’ on vuplayController
* Controls will now stay visible on vuplayViewController when playback is paused
* Fix memory leak that could have occurred if subtitles were enabled and a player was closed
* Fixed a few issues with subtitles after seeking and/or changing languages
* Improved performance of FairPlay license acquisition


**v0.9.7 (build 548)**

* Due to enhancements in the vudrm platform, you are no longer required to supply your API-KEY using +[vudrm configureAPIKey:]. As such the API has been completely removed.
* The current version of the vuplaySDK can be ascertained by calling +[vuplaySDK version] / vuplaySDK.version()

**v0.9.6 (build 513)**

* The methods -initWithURL:, -initWithURL:token: and -initWithURL:token:licenseServer: are now depreciated on vuplayViewController. The methods will be removed before v1.0.

    Instead, initialise an instance of vuplayController using it’s -initWithURL:. -initWithURL:token: or -initWithURL:token:licenseServer: methods and set the player property on vuplayViewController.

* selectedSubtitle and selectedLanguage can now be set immediately after initialising vuplayController and will be respected once the player is prepared.
* Fixed issue with subtitle cue positioning always being at the bottom of the player view, rather than bottom of the content
* Fixed issue with subtitle cue’s being out of sync if seeking backwards
* Fixed issue with seeking causing the current subtitles not to be available
* vuplayViewController will now only show the first error that occurs
* Resolved issue with duplicate subtitle cue’s appearing on certain combination of content/iOS version

**v0.9.5 (build 451)**

* Fix issue that could cause AirPlay to Apple TV 4th generation not to work as expected

**v0.9.4 (build 443)**

* The languages property on vuplayController will now return an array of 1 language, previously it would return nil unless there were two or more languages
* Fix issue with preparation or playback errors not being reported properly in some use cases
* Fixed issue with playback not starting automatically in vuplayViewController
* An error will now be correctly reported, if trying to play anything other than unencrypted HLS or HLS protected with FairPlay Strreaming whilst using the advanced SDK usage
* Added timeout parameter to the advanced SDK usage, so you can specify the maximum amount of time you are prepared to wait for an initialised player

**v0.9.3 (build 429)**

* Add multi-audio and subtitle selectors on vuplayViewController
* Fix issue with multi-audio HLS implementation returning languages when actually it should be been returning nil
* Fix potential issue with in-stream HLS subtitles not working due to unexpected characters in the URI
* Added advanced use case for the SDK. See the ‘Advanced SDK usage’ section above.

**v0.9.2 (build 354)**

* Improved feedback when FPS was not able to retrieve certificate from vudrm

**v0.9.1a (build 328)**

* Fix linker issues with undefined symbols


**v0.9.1 (build 326)**

* Fair Play Streaming security enhancements (see Fair Play Streaming section above)
* Support for multi audio with HLS streams

**v0.9.0 (build 293)**

* Initial support for Fair Play Streaming
* Increased minimum supported iOS version to 8.0


**v0.4.3 (build 287)**

* Fix issue with playback audio incorrectly being muted when mute switch is toggled
* Add support for playing back MP4's via HTTP progressive download
* Fix issue with the playback progress not showing 100% in vuplayViewController when the end of the movie is reached
* Fix issue with playback duration not showing correctly if over one hour in vuplayViewController
* Fixed issue whereby WebVTT subtitles did not pass validation
* Improved the behaviour of vuplayViewController when content is being prepared
* The UI in vuplayViewController will now hide automatically

**v0.4.2 (build 216)**

* Make use of the latest Objective-C language improvements - nullability and lightweight generics.  This makes the API clearer and improves its usage, especially with Swift
* Fix issue with incorrect import statements in umbrella header file causing potential compilation issues with Xcode 7.1
* Dramatically simplified the steps required to integrate the SDK into a project
* Only reset PlayReady license store if absolutely necessary
* Add new API for proactively acquiring a PlayReady license from a downloaded ISMV. 

Please call +[vuplayController acquireLicense:token:completionHandler:] at a point in your application workflow that make sense to you. See built-in documentation for more information!

**v0.4.1 (build 187)**

* Resolve compiler warnings seen in v0.4 when building with Xcode 7
* Fix issue with parsing subtitles with Windows style (CRLF) line endings
* Fix crash related to enabling subtitles whilst still being parsed
* Fix crash caused by error handling when no underlying NSLocalizedFailureReason was provided
* Fix issue with HLS streams not being able to enable out of stream subtitles via -addSubtitle:withURL:
* Resolved issue with HTML tags being shown in WebVTT subtitles
* Update PlayReady DRM to v2.4.1

**v0.4 (build 176)**

* Add support for playing downloaded ISMVs
* Disable the system idle timer when playing content and enable when paused or stopped
* Update PlayReady DRM to v2.4

**v0.3.1 (build 156)**

* Add messages for PlayReady errors 0x80014011 and 0x8001422a
* If the content URL is not found (404), provide a message to consumer to that effect
* If the remote server returns a non-2xx status code, provide a message to consumer to that effect

**v0.3 (build 150)**

* Fix issue whereby if the stream type could not be determined the consumer was not aware of the problem
* Fix issue of spinner showing in centre of player view when playback type is not supported
* Provide underlying PlayReady SDK error, if no extra information can be added
* Fix issue with playback caused by unexpected CDN redirect
* Add additional validation on media provided to SDK
* Add support for in-stream and externally loaded WebVTT subtitles.

    Exposed via two properties ‘subtitles’ and ‘selectedSubtitle’ with external subtitles being added with -[vuplayController addSubtitle:withURL:]. See built-in documentation for more information!

* Multi audio is now supported for Microsoft Smooth Streaming and DASH.

    Exposed via two properties ‘languages’ and ‘selectedLanguage’. See built-in documentation for more information

**v0.2 (build 107)**

* **IMPORTANT:**  
  vuplayView has been removed. Instead instantiate an instance of vuplayController (synonymous with MPMoviePlayerController) and access the .view property.
* Add support for Swift
* Removed -initWithAddress:token: initialiser for vuplayController, please use -initWithURL:token: instead
* Attempting to play a Smooth or DASH stream in the iOS simulator will now show a friendly reason why  
  playback will not work, rather than an empty player view.
* Updated the documentation in the header in-line with Apple’s documentation for MPMoviePlayerController and 
  to make the initialisers clearer
* Expose properties on vuplayController for ‘duration’, ‘playableDuration’, ‘scalingMode’ and ‘naturalSize’
* Support for MPMoviePlayerLoadStateDidChangeNotification, MPMoviePlayerPlaybackStateDidChangeNotification 
  and MPMoviePlayerPlaybackDidFinishNotification notifications.

**IMPORTANT: **
Ensure to observe your instance of vuplayController for these notifications:
    
* Added vuplayViewController a fully functional player with the following features:
    * Vualto skin
    * Play / Pause
    * Seeking
    * Playback duration


**v0.1 (build 15)**

* Initial release


**Example Projects**

*vuplayController Demo* - Demonstrates the vuplayController usage scenario. Edit the demo to insert your stream and token!

*vuplayViewController Demo* - Demonstrates the vuplayViewController usage scenario. Edit the demo to insert your stream and token!




