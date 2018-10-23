# tvOS SDK v0.9.8 (build 636)

This documentation describes the steps to integrate and use the vuplay SDK for tvOS.

## Introduction

The tvOS SDK is provided as a dynamic framework that can be quickly and simply integrated into your Xcode project.  It is modelled after the stock tvOS media player classes, namely AVPlayer and AVPlayerViewController.

The SDK provides three distinct usage options:
1. A full screen player with built-in controls in the form of vuplayViewController
2. A fully customisable player in form of vuplayController that can be sent messages, such as -play or -pause and 
   vends a view that can be added anywhere in your view hierarchy.
3. An advanced use case where the SDK will prepare a AVPlayer instance and asynchronously return this to you.


The SDK is fully supported in both Objective-C and Swift applications. Basic demos are provided in both languages. Advanced demos are provided in Swift.

Please contact support@vualto.com to request a download of the SDK.


## Project Requirements

* Minimum tvOS deployment target of 9.x or higher
* Xcode 7.3.1 or higher

**Xcode Integration**

1. Copy the vuplaySDK.framework into your application's project directory
2. Navigate to your target and add vuplaySDK.framework to your â€˜Embedded Binariesâ€™. You should see that vuplaySDK.framework also now appears under â€˜Linked Frameworks and Librariesâ€™:


**Information about Application Transport Security (ATS)**

tvOS 9 introduces Application Transport Security (ATS). In order to permit playback of content exemptions need to be added into your application's Info.plist.

If your content is delivered via HTTPS that meets Appleâ€™s ATS guidelines, then the following exemption needs to be added for localhost:


# THIS XML IS MALFORMED !!!!!!! ****

```XML
<key>localhost</key>
<dict>
  <key>NSIncludesSubdomains</key>
  <true/>
  <key>NSTemporaryExceptionAllowsInsecureHTTPLoads</key>
  true/>
</dict>
```

If your content is delivered via HTTP then you need need to add exemptions for this traffic.  For example to disable ATS for any connection you would add the following into your application's Info.plist:

```XML
<dict>
  <key>NSAppTransportSecurity</key>
  <dict>
    <key>NSAllowsArbitraryLoads</key>
    <true />
  </dict>
</dict>
```

More information about ATS can be found in Appleâ€™s TechNote:

``` https://developer.apple.com/library/prerelease/ios/technotes/App-Transport-Security-Technote/ ```


##  vuplayController usage (Objective-C)

1. Import the vuplaySDK into your player:

    @import vuplaySDK;

2. Create a new property for the vuplayController:

    @property (nonatomic, readwrite, strong) vuplayController *player;

3. Initialise an instance of vuplayController:

    self.player = [[vuplayController alloc] initWithURL:[NSURL URLWithString:@"<stream URL>"] token:@"<DRM token>"];

4. Add the vuplayControllerâ€™s view into your view hierarchy:

    self.player.view.frame = CGRectMake(0, 20, self.view.bounds.size.width, 
    self.view.bounds.size.height - 64);
    self.player.view.autoresizingMask = UIViewAutoresizingFlexibleHeight | UIViewAutoresizingFlexibleWidth;
    [self.view addSubview:self.player.view];


5. As vuplayController implements the MPMediaPlayback protocol you can now send it the -play message for it to start playing your content.


## vuplayController usage (Swift)

1. Import the vuplaySDK into your player:
    
    import vuplaySDK

2. Initialise an instance of vuplayController:

    let player = vuplayController(address: "<stream URL>", token: "<DRM token>")

3. Add the vuplayControllerâ€™s view into your view hierarchy:

    player.view.frame = CGRectMake(0, 20, view.bounds.size.width, view.bounds.size.height - 64)
    
    player.view.autoresizingMask = [.FlexibleHeight, .FlexibleWidth]
    
    view.addSubview(player.view)

4. As vuplayController implements the MPMediaPlayback protocol you can now call the play() function for it to   
   start playing your content.


## vuplayViewController usage (Objective-C)

1. Import the vuplaySDK:

    @import vuplaySDK;

2. Initialise an instance of vuplayController:

    vuplayController *player = [[vuplayController alloc] initWithURL:[NSURL URLWithString:@"<stream URL>"] token:@"<DRM token>"];


3. Initialise an instance of vuplayViewController and set the player property:

    vuplayViewController *playerViewController = [[vuplayViewController alloc] initWithURL:[NSURL URLWithString:@"<stream URL>"] token:@"<DRM token>"];
    playerViewController.player = player;

4. Present the player view controller:

    [self presentViewController:playerViewController animated:YES completion:nil];


## vuplayViewController usage (Swift)

1. Import the vuplaySDK:

    import vuplaySDK

2. Initialise an instance of vuplayController:

    let player = vuplayController(address: "<stream URL>", token: "<DRM token>")

3. Initialise an instance of vuplayViewController and set the player property:

    let playerViewController  = vuplayViewController(URL: NSURL(string: "<stream URL>"), token: "<DRM token>")
    playerViewController.player = player

4. Present the player view controller:

    presentViewController(playerViewController, animated: true, completion: nil)


**Limitations**

* The SDK does not support playback of protected content when running in the iOS Simulator

**Known Issues**

* There is currently no support for linking against vuplaySDK when building for the tvOS Simulator. This will 
  be resolved before v1.0.
  
* There are no demos for vuplayController in either Objective-C or Swift. This will be resolved before v1.0.



## Advanced SDK usage

Starting with v0.9.3 of the SDK it is now possible to get direct access to the underlying instance of AVPlayer after it has been prepared for playback. Eg:


```
vuplaySDK.playerWithURL(
    NSURL,
    token: String?,
    licenseServer: NSURL?,
    timeout: NSTimeInternal) { (AVPlayer?, NSError?) -> Void in
    // Your code
}
```

When your completion handler is called, it is then your responsibility to for managing its lifecycle and all events that occur. Eg, you will need to ensure it is ready for playback, or seeking.

Vualto will fully support the initial configuration and setup of the DRM integration for AVPlayer.  However, our support ends once the reference to AVPlayer is provided to you.


##Limitations##

Only works with unencrypted HLS streams or HLS streams encrypted with Fair Play Streaming

##Release Notes##

**v0.9.8 (build 636)**

* Improved performance of FairPlay license acquisition

**v0.9.7 (build 548)**

* Due to enhancements in the vudrm platform, you are no longer required to supply your API-KEY using +[vudrm configureAPIKey:]. As such the API has been completely removed.

* The current version of the vuplaySDK can be ascertained by calling +[vuplaySDK version] / vuplaySDK.version()

* Work around an issue that could cause thumbnail images not to appear on AVPlayerViewController when using the   
  advanced SDK usage
* **selectedSubtitle** can now be set immediately after initialising vuplayController and will be respected once 
  the player is prepared.

**v0.9.6 (build 513)**

* Reintroduced vuplayViewController based on the Apple skinned player.  The skin will however be updated in the 
  future to use the Vualto skin.
  
* **selectedLanguage** can now be set immediately after initialising vuplayController and will be respected once 
  the player is prepared.

**v0.9.5 (build 451)**

* Fix issue that could cause AirPlay to Apple TV 4th generation not to work as expected

**v0.9.4 (build 443)**

* The **languages** property on vuplayController will now return an array of 1 language, previously it would 
  return nil unless there were two or more languages

* An error will now be correctly reported, if trying to play anything other than unencrypted HLS or HLS protected 
  with FairPlay Strreaming whilst using the advanced SDK usage

* Added **timeout** parameter to the advanced SDK usage, so you can specify the maximum amount of time you are 
  prepared to wait for an initialised player


**v0.9.3 (build 429)**

* Removed *vuplayViewController*, instead use the advanced use case for the SDK and supply the provided AVPlayer 
  to your own instance of AVPlayerViewController
  
* Fix issue with multi-audio HLS implementation returning languages when actually it should be been returning nil

* Added advanced use case for the SDK. See the â€˜Advanced SDK usageâ€™ section above.


**v0.9.2 (build 354)**

* Fix issue with bit code generation only being marker rather than full bit code
* Add vuplayViewController providing a fully Apple skinned player


**v0.9.1 (build 346)**

* Initial release


## Example Projects

*vuplayController Demo* - Demonstrates the vuplayController usage scenario. Edit the demo to insert your stream and token!

*vuplayViewController Demo* - Demonstrates the vuplayViewController usage scenario. Edit the demo to insert your stream and token!

*Basic AVPlayerViewController* - Demonstrates basic usage of how to retrieve an instance of AVPlayer and use that for AVPlayerViewController.

*Advanced AVPlayerViewController* - Demonstrates more advanced usage of AVPlayer, so that playback position is restored before being passed to AVPlayerViewController.
