# SkinType

## Usage

Currently there are four skin types supported. To set a skin you must set the `skin` value in the setup configuration object.
The following code example loads the default skin.

``` javascript
var vuplaySmart = new Vuplay.Smart("<player-key>", Vuplay.LogLevel.WARN);
var config = {
    src: "<mpeg-dash-url>",
    vudrmToken: "<vudrm-token>",
    autoStart: true,
    skin: Vuplay.SkinType.DEFAULT
};
vuplaySmart.setup(config, document.getElementById("vuplay-container"));
```

## Types

The available skin types can be accessed through the `Vuplay.SkinType` enum, the following table details the types:

| Type    | Description                                                                                      |
|---------|--------------------------------------------------------------------------------------------------|
| DEFAULT | A simple skin that includes a play and fullscreen button, a buffering icon and the current time. |
| VUPLAY  | The default skin with a subtitles button for turning the first text track on or off.             |
| NO_SKIN | No skin will be loaded. Use this option if you wish to create your own custom skin.              |
| VUALTO  | A fully customisable skin that contains a full set of features.                                  |

## Samples

![Vualto skin](/skin/vualto-small.png)