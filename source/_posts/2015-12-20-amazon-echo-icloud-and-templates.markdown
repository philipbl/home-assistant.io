---
layout: post
title: "0.10: Amazon Echo, iCloud, Dweet.io, Twitch and templating support!"
description: "Home Assistant 0.10 has been released with a bunch of added components and brand new templating support."
date: 2015-12-22 01:30:00 -0800
date_formatted: "December 22, 2015"
author: Paulus Schoutsen
author_twitter: balloob
comments: true
categories: Release-Notes
og_image: /images/blog/2015-12-release-10/alexa-fb.png
---

Alrighty, it's time for Home Assistant 0.10. A lot amazing things have changed and sadly we also had to introduce a bunch of backwards incompatible changes. I would like to give a big shoutout to Philip Lundrigan ([@philipbl]) who put a lot in effort in helping the migration to move towards using templates for a wide variety of platforms.

<div class='videoWrapper'>
<iframe width="560" height="315" src="https://www.youtube.com/embed/1Ke3mtWd_cQ" frameborder="0" allowfullscreen></iframe>
</div>

<img src='/images/supported_brands/icloud.png' style='clear: right; border:none; box-shadow: none; float: right; margin-bottom: 16px;' width='150' /><img src='/images/supported_brands/heatmiser.png' style='clear: right; border:none; box-shadow: none; float: right; margin-bottom: 16px;' width='150' /><img src='/images/supported_brands/dweet.png' style='clear: right; border:none; box-shadow: none; float: right; margin-bottom: 16px;' width='150' /><img src='/images/supported_brands/amazon-echo.png' style='clear: right; border:none; box-shadow: none; float: right; margin-bottom: 16px;' width='150' /><img src='/images/supported_brands/eliq.png' style='clear: right; border:none; box-shadow: none; float: right; margin-bottom: 16px;' width='150' />

 - Device tracker: [iCloud] platform added ([@xorso], [@kevinpanaro])
 - Frontend: Improved caching using service workers if served over SSL ([@balloob])
 - Sensor: [Twitch] platform added ([@happyleavesaoc])
 - [Template] support ([@balloob], [@philipbl], [@fabaff])
 - Thermostat: [Heatmiser] platform added ([@andylockran])
 - Sensor: [Dweet.io] platform added ([@fabaff])
 - [Alexa/Amazon echo] component added ([@balloob])
 - Device Tracker: [FritzBox] platform added ([@deisi], [@caiuspb])
 - Sensor: [Wink] now supports the Egg minders ([@w1ll1am23])
 - Sensor: [ELIQ Online] platform added ([@molobrakos])
 - Binary sensor: [REST] platform added ([@fabaff])
 - Sensor: [Torque (OBD2)] platform added ([@happyleavesaoc])

[iCloud]: /components/device_tracker.icloud/
[Twitch]: /components/sensor.twitch/
[Template]: /getting-started/templating/
[Heatmiser]: /components/thermostat.heatmiser/
[Dweet.io]: /components/sensor.dweet/
[Alexa/Amazon echo]: /components/alexa/
[FritzBox]: /components/device_tracker.fritzbox/
[Wink]: /components/sensor.wink/
[ELIQ Online]: /components/sensor.eliqonline/
[REST]: /components/binary_sensor.rest/
[Torque (OBD2)]: /components/sensor.torque/
[@andylockran]: https://github.com/andylockran
[@balloob]: https://github.com/balloob
[@caiuspb]: https://github.com/caiuspb
[@deisi]: https://github.com/deisi
[@fabaff]: https://github.com/fabaff
[@happyleavesaoc]: https://github.com/happyleavesaoc
[@kevinpanaro]: https://github.com/kevinpanaro
[@molobrakos]: https://github.com/molobrakos
[@philipbl]: https://github.com/philipbl
[@w1ll1am23]: https://github.com/w1ll1am23
[@xorso]: https://github.com/xorso

<!--more-->

### Templates

This release introduces templates. This will allow you to parse data before it gets processed or create messages for notifications on the fly based on data within Home Assistant. The notification component and the new Alexa/Amazon Echo component are both using the new template functionality to render responses. A template editor has been added to the developer tool section in the app so you can get instant feedback if your templates are working or not.

```jinja2
The temperature at home is {% raw %}{{ states('sensor.temperature') }}{% endraw %}.
```

More information and examples can be found in the [template documentation][Template].

### Breaking changes

Templates will now be the only way to extract data from 'raw' sources like REST, CommandSensor or MQTT. This will replace any specific option that used to do this before. This means that `precision`, `factor`, `attribute` or `json_path` etc will no longer work.

Affected components and platforms:

 - sensor: [arest][sensor.arest]
 - sensor: [command_sensor][sensor.command]
 - sensor: [rest][sensor.rest]
 - sensor: [MQTT][sensor.mqtt]
 - switch: [MQTT][switch.mqtt]
 - rollershutter: [MQTT][rollershutter.mqtt]
 - light: [MQTT][light.mqtt]
 - binary_sensor: [MQTT][binary_sensor.mqtt]
 - automation: [numeric_state][automation-numeric-state]

[sensor.arest]: /components/sensor.arest/
[sensor.command]: /components/sensor.command_sensor/
[sensor.rest]: /components/sensor.rest/
[sensor.mqtt]: /components/sensor.mqtt/
[switch.mqtt]: /components/switch.mqtt/
[rollershutter.mqtt]: /components/rollershutter.mqtt/
[light.mqtt]: /components/light.mqtt/
[binary_sensor.mqtt]: /components/binary_sensor.mqtt/
[automation-numeric-state]: /components/automation/#numeric-state-trigger
