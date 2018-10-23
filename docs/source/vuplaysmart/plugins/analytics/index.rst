Analytics
=========

.. toctree::
   :maxdepth: 1
   :hidden:
   :glob:

   *

The stats engines that are currently supported are:

- `Adobe analytics <https://www.adobe.com/uk/data-analytics-cloud/analytics/>`__
- `AT-Internet <https://www.atinternet.com/en/>`__
- `cim <https://www.cim.co.uk>`__
- `comscore <https://www.comscore.com>`__
- `Youbora <http://youbora.com/>`__

.. tip:: Please contact `support@vualto.com <mailto:support@vualto.com>`__ if you require another stats system.

Plugin Setup
++++++++++++

In order to use any statistical plugins they must be setup on your Vualto account. Please contact `support@vualto.com <mailto:support@vualto.com>`__ for more information.

Any configured plugins will be automatically loaded when an instance of  `Smart </en/latest/api/smart.html>`__ is created.
You must then start the loaded plugins using the :code:`startStatsMonitoring` method on  `Smart </en/latest/api/smart.html>`__.
It is recommended to call this method as soon as  `Smart </en/latest/api/smart.html>`__ is instantiated.
You can pass any stats plugin configuration before starting the stats plugins by using the :code:`setStatsConfigs` method on  `Smart </en/latest/api/smart.html>`__.

.. code-block:: js
    var vuplaySmart = new Vuplay.Smart("<player-key>", Vuplay.LogLevel.WARN);
    var statsConfigs = {
        "<plugin-id>": { ... },
        "<plugin-id>": { ... }
    };
    vuplaySmart.setStatsConfigs(statsConfigs);
    vuplaySmart.startStatsMonitoring();


You can stop the stats plugins from reporting stats by calling :code:`stopStatsMonitoring` on  `Smart </en/latest/api/smart.html>`__. This will not remove the stats plugin from the DOM, it will just pause the plugin from reporting events.

Calling :code:`reset` on  `Smart </en/latest/api/smart.html>`__ will internally call :code:`stopStatsMonitoring` on  `Smart </en/latest/api/smart.html>`__. If you are resetting the player and setting a new src then you must call :code:`startStatsMonitoring` again before calling :code:`setSrc` on  `Smart </en/latest/api/smart.html>`__.
