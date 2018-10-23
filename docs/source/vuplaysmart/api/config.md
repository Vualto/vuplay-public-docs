# Configuration

## Usage


``` javascript
var vuplaySmart = new Vuplay.Smart("<player-key>", Vuplay.LogLevel.WARN);
var config = {
    src: "<mpeg-dash-url>",
    vudrmToken: "<vudrm-token>",
    autoStart: true
};
vuplaySmart.setup(config, document.getElementById("vuplay-container"));
```

## Properties

The configuration object is not provided by the `Vuplay` namespace. This should be created when calling the `setup` method on the [Smart](/api/smart.html) object.

| Property | Type | Description | Required | Default |
|----------|------|-------------|----------|---------|
| src | string | The stream url or [YouTube](/players/youtube.html) video ID. | true | undefined |
| vudrmToken | string | A [vudrm token](http://readme.vualto.com/vudrm/VuDrmTokenIntegration). | true if content is encrypted | undefined |
| ads | array | Will load ads in Theoplayer. [Documentaiton ref.](https://bit.ly/2x6MtRc) | false | undefined |
| autoStart | boolean | If true playback will begin as soon as possible. | false | false |
| skin | [Vuplay.SkinType](/api/skintype.html) | Skin type to load. | false | `Vuplay.SkinType.DEFAULT` |
| skinConfig | PlayerConfig | The skin configuration object. | false | {} |
| clipping | boolean | If true will enable clipping controls on the Vualto skin. | false | false |
| framerate | number | When clipping is true, the skin will use the specified framerate for frame skipping. | false | 30 |
| loadYoutube | boolean | Will load the [YouTube](/players/youtube.html) iframe player. `src` must be set to a YouTube video ID. | false | false |
| isEmbeddable | boolean | enables playback from within an iFrame (!important! THEOPlayer only). | false | false |
| airplay | boolean | If true and in Safari, Airplay plugin will be loaded. | false | false |
| chromecast | boolean | If true and in Chrome, Chromecast plugin will be loaded. | false | false |
| chromecastAppId | string | sets the id of the chromecast app, must be used with `chromecast` config option. | false | undefined |
| streamTypeOverride | string | Prevents vuplay-smart from detecting the live state of the stream by overriding it. Values: "live" or "vod" | false | undefined |

<div class="admonition warning">
    <p class="first admonition-title">Warning</p>
    <p class="last">Setting <code class="docutils literal notranslate"><span class="pre">streamTypeOverride</span></code> configuration property might cause unpredictable behaviour.</p>
</div>