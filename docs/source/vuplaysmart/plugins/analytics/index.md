Analytics
=========

.. toctree::
   :maxdepth: 1
   :hidden:
   :glob:

   *

The stats engines that are currently supported are:

- Adobe analytics <https://www.adobe.com/uk/data-analytics-cloud/analytics/>
- AT-Internet <https://www.atinternet.com/en/>
- cim <https://www.cim.co.uk>
- comscore <https://www.comscore.com>
- Youbora <http://youbora.com/>

.. tip:: Please contact  support@vualto.com <mailto:support@vualto.com> if you require another stats system.

Plugin Setup
++++++++++++

In order to use any statistical plugins they must be setup on your Vualto account. Please contact  support@vualto.com (mailto:support@vualto.com) for more information.

Any configured plugins will be automatically loaded when an instance of  Smart (/api/smart.html) is created.
You must then start the loaded plugins using the `startStatsMonitoring` method on  Smart (/api/smart.html).
It is recommended to call this method as soon as  Smart (/api/smart.html) is instantiated.
You can pass any stats plugin configuration before starting the stats plugins by using the `setStatsConfigs` method on  Smart (/api/smart.html).

.. code-block:: js
    var vuplaySmart = new Vuplay.Smart("<player-key>", Vuplay.LogLevel.WARN);
    var statsConfigs = {
        "<plugin-id>": { ... },
        "<plugin-id>": { ... }
    };
    vuplaySmart.setStatsConfigs(statsConfigs);
    vuplaySmart.startStatsMonitoring();


You can stop the stats plugins from reporting stats by calling `stopStatsMonitoring` on  Smart (/api/smart.html). This will not remove the stats plugin from the DOM, it will just pause the plugin from reporting events.

Calling `reset` on  Smart (/api/smart.html) will internally call `stopStatsMonitoring` on  Smart (/api/smart.html). If you are resetting the player and setting a new src then you must call `startStatsMonitoring` again before calling `setSrc` on  Smart (/api/smart.html).
