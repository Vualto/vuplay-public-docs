# Peer5

Peer5 is a peer-to-peer Content Delivery Network (P2P CDN) for massively-scaled, high-quality streaming. They dynamically construct an elastic mesh network consisting of viewers that integrates seamlessly with the existing edge server infrastructure and dramatically improves its performance, creating the ultimate Multi-CDN.

## Configuration

In order to enable the Peer5 plugin on vuplay smart the following configuration option must be set.

``` javascript
var vuplaySmart = new Vuplay.Smart("<player-key>", Vuplay.LogLevel.WARN);

var config = {
    src: "<mpeg-dash-url>",
    peerFiveCustomerId: "<peer-5-customer-id>"
};

vuplaySmart.setup(config, document.getElementById("vuplay-container"));
```

## Supported players

- shakaDash
- THEOplayer