Cast
====

.. toctree::
   :maxdepth: 1
   :hidden:
   :glob:

   *

Cast Types
++++++++++

Currently only Chromecast with the default receiver is supported for casting.

Cast Configuration
++++++++++++++++++

In order to enable the Chromecast plugin on vuplay smart the following configuration option must be set.

.. code-block:: js
    var vuplaySmart = new Vuplay.Smart("<player-key>", Vuplay.LogLevel.WARN);

    var config = {
        src: "<mpeg-dash-url>",
        vudrmToken: "<vudrm-token>",
        autoStart: true
    };

    vuplaySmart.setup(config, document.getElementById("vuplay-container"));

Start Casting
+++++++++++++

In order to start casting, the `startCasting` function is called, vuplay smart will then take the currently loaded source and initiate casting.

.. code-block:: js
    vuplaySmart.startCasting(CastType.CHROMECAST, "vuplay smart test content");


Stop Casting
++++++++++++

In order to stop casting, the `stopCasting` function is called, vuplay smart will then stop casting and hand control back to the loaded player.

.. code-block:: js
    vuplaySmart.stopCasting();


Cast Events
+++++++++++

================ ==================================================================== =========================================
 Event            Description                                                          Arguments                                
================ ==================================================================== ========================================= 
 caststart        Fired when the casting device reports casting has been successful.   castType: CastType, castDevice: string   
 castend          Fired when an individual ad begins playback.                         castType: CastType, currentTime: number  
 castloaded       Fired when vuplay smart has loaded the cast plugin.                  castType: CastType                       
================ ==================================================================== =========================================

The Chromecast plugin in each `Smart </en/latest/api/smart.html>`__ instance will load the Chromecast plugin by default when in Chrome:

.. code-block:: js
    var vuplaySmart = new Vuplay.Smart("<player-key>", Vuplay.LogLevel.WARN);

    var config = {
        src: "<mpeg-dash-url>",
        vudrmToken: "<vudrm-token>",
        autoStart: true
    };

    vuplaySmart.setup(config, document.getElementById("vuplay-container"));

    // setup cast specific events
    vuplaySmart.on(Vuplay.EventType.CAST, Vuplay.Events.castloaded, console.log);
    vuplaySmart.on(Vuplay.EventType.CAST, Vuplay.Events.caststart, console.log);
    vuplaySmart.on(Vuplay.EventType.CAST, Vuplay.Events.castend, console.log);
