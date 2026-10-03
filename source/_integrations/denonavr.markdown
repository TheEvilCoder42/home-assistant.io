---
title: Denon AVR Network Receivers
description: Instructions on how to integrate Denon AVR Network Receivers into Home Assistant.
ha_category:
  - Media player
ha_iot_class: Local Push
ha_release: 0.7.2
ha_domain: denonavr
ha_codeowners:
  - '@ol-iver'
  - '@starkillerOG'
ha_config_flow: true
ha_ssdp: true
ha_platforms:
  - media_player
  - number
  - select
  - switch
ha_integration_type: device
---

The **Denon AVR Network Receivers** {% term integration %} allows you to control [Denon Network Receivers](https://www.denon.com/category/heos) from Home Assistant. It might be that your device is supported by the [Denon] platform.

Known supported devices:

- Denon AVR-X1000
- Denon AVR-X1100W
- Denon AVR-X1200W
- Denon AVR-X1300W
- Denon AVR-X1400H
- Denon AVR-X1500H
- Denon AVR-X1600H
- Denon AVR-X1700H
- Denon AVR-X1800H
- Denon AVR-X2000
- Denon AVR-X2100W
- Denon AVR-X2200W
- Denon AVR-X2300W
- Denon AVR-X2400H
- Denon AVR-X2500H
- Denon AVR-X2600H
- Denon AVR-X2700H
- Denon AVR-X2800H
- Denon AVC-X2850H
- Denon AVR-X3000
- Denon AVR-X3200W
- Denon AVR-X3300W
- Denon AVR-X3400H
- Denon AVR-X3500H
- Denon AVR-X3600H
- Denon AVR-X3700H
- Denon AVR-X3800H
- Denon AVC-X3800H
- Denon AVR-X4100W
- Denon AVR-X4300H
- Denon AVR-X4400H
- Denon AVR-X4500H
- Denon AVR-X4700H
- Denon AVC-X4800H
- Denon AVR-X6500H
- Denon AVR-X6700H
- Denon AVR-X7200W
- Denon AVR-X8500H
- Denon AVR-1713
- Denon AVR-1912
- Denon AVR-2112CI
- Denon AVR-2312CI
- Denon AVR-3311CI
- Denon AVR-3312
- Denon AVR-3313CI
- Denon AVR-4810
- Denon AVR-E300
- Denon AVR-E400
- Denon AVR-S650H
- Denon AVC-S660H
- Denon AVR-S710W
- Denon AVR-S720W
- Denon AVR-S740H
- Denon AVR-S750H
- Denon AVR-S760H
- Denon AVR-S770H
- Denon AVR-S940H
- Denon AVR-S950H
- Denon AVR-S960H
- Denon AVR-S970H
- Denon DN-500AV
- Denon DRA-N5
- Denon DRA-800H
- Denon RCD-N8
- Denon RCD-N9
- Marantz AV 20
- Marantz AV7702
- Marantz AV7703
- Marantz AV7704
- Marantz AV8802A
- Marantz AV8805
- Marantz CINEMA 50
- Marantz CINEMA 60
- Marantz CINEMA 70s
- Marantz M-CR510
- Marantz M-CR511
- Marantz M-CR603
- Marantz M-CR610
- Marantz M-CR611
- Marantz SR5006
- Marantz SR5008
- Marantz SR5010
- Marantz SR5011
- Marantz SR5015
- Marantz SR6007 - SR6012
- Marantz SR7007
- Marantz SR7010
- Marantz SR7012
- Marantz SR8015
- Marantz NR1504
- Marantz NR1506
- Marantz NR1509
- Marantz NR1510
- Marantz NR1602
- Marantz NR1603
- Marantz NR1604
- Marantz NR1606
- Marantz NR1607
- Marantz NR1609
- Marantz NR1710
- Marantz NR1711
- Other Denon AVR receivers (untested)
- Marantz receivers (experimental)

If your model is not on the list then give it a test, if everything works correctly then add it to the list by clicking on the **Edit** link at the bottom of this page.

If you are using VLANs, Home Assistant needs access to the following ports on the AVR: 23, 8080, and 60006 (all TCP).

{% warning %}
If you have something else using the IP controller for your Denon AVR 3808CI, such as your URC controller, it will not work! There is either a bug or security issue with some models where only one device could be controlling the IP functionality.
{% endwarning %}

{% include integrations/config_flow.md %}

{% configuration_basic %}
host:
  description: IP address of the device, for example, `192.168.1.32`. If not set, auto-discovery is used.
show_all_sources:
  description: If True all sources are displayed in sources list even if they are marked as deleted in the receiver. If False deleted sources are not displayed. Some receivers have a bug that marks all sources as deleted in the interface. In this case, this option could help.
zone2:
  description: Specifies if zone 2 should be activated. Zones are displayed as additional media players with the same functionality as the Main Zone of the device supports.
zone3:
  description: Specifies if zone 3 should be activated. Zones are displayed as additional media players with the same functionality as the Main Zone of the device supports. Some receivers do not support a second zone.
update_audyssey:
  description: Specifies if Audyssey settings should be updated. This can take up to 10 seconds for some receivers.
use_telnet:
  description: Specifies if a telnet connection should be used to receive device status updates. Using telnet provides realtime updates (local push) for many values but each receiver is limited to a single connection. If you enable this setting, no other connection to your device can be made via telnet. This will be set to true for new installations of the integration but false for existing installs to prevent compatibility issues.
{% endconfiguration_basic %}

A few notes:

- An additional option for the control of Denon AVR receivers with a built-in web server is using the HTTP interface with `denonavr` platform.
- The `denonavr` platform supports some additional functionalities like album covers, custom input source names and auto discovery.
- Marantz receivers seem to a have quite a similar interface. Thus if you own one, give it a try.
- To remotely power on Marantz receivers with Home Assistant, the Auto-Standby feature must be enabled in the receiver's settings.
- Sound mode: The command to set a specific sound mode is different from the value of the current sound mode reported by the receiver (sound_mode_raw). There is a key-value structure (sound_mode_dict) that matches the raw sound mode to one of the possible commands to set a sound mode (for instance {'MUSIC':['PLII MUSIC']}. If you get a "Not able to match sound mode" warning, please open an issue on the [denonavr library](https://github.com/ol-iver/denonavr), stating which raw sound mode could not be matched so it can be added to the matching dictionary. You can find the current raw sound mode under {% my developer_states title="**Settings** > **Tools** > **States**" %}.

## Number

The `denonavr` integration creates the following [Number](/integrations/number/) entities on the receiver's device, as configuration entities.

- **Tone control bass**
  - **Description**: Boosts or cuts the bass, in the dB the receiver shows. Shows unknown until the receiver first reports a value.
  - **Range**: -6 dB to +6 dB, in 1 dB steps
  - **Availability**: The same as the **Tone control** switch, except that before the receiver first reports a value it shows unknown instead.
- **Tone control treble**
  - **Description**: Boosts or cuts the treble, in the dB the receiver shows. Shows unknown until the receiver first reports a value.
  - **Range**: -6 dB to +6 dB, in 1 dB steps
  - **Availability**: The same as the **Tone control** switch, except that before the receiver first reports a value it shows unknown instead.

## Select

The `denonavr` integration creates the following [Select](/integrations/select/) entities on the receiver's device, as configuration entities.

- **Audyssey Dynamic Volume**
  - **Description**: Evens out very quiet and very loud passages, so the volume stays consistent across different content. Heavy adjusts the most, Light the least.
  - **Options**: Off, Light, Medium, Heavy
  - **Availability**: Unavailable when the receiver has no Audyssey, when **Audyssey MultEQ** is off, and in the Direct and Pure Direct sound modes.
- **Audyssey MultEQ**
  - **Description**: The room correction curve Audyssey applies.
  - **Options**: Off, Flat, L/R bypass, Reference, Manual. Manual can only be selected with **Use Telnet connection** enabled.
  - **Availability**: Unavailable when the receiver has no Audyssey, and in the Direct and Pure Direct sound modes.
- **Audyssey reference level offset**
  - **Description**: Adjusts Audyssey Dynamic EQ for content that is not mixed to the film reference level. Denon recommends 0 dB for movies, +5 dB for classical music, +10 dB for jazz and TV, and +15 dB for pop and rock.
  - **Options**: 0 dB, +5 dB, +10 dB, +15 dB
  - **Availability**: Unavailable when the receiver has no Audyssey, when the **Audyssey Dynamic EQ** switch is off, and in the Direct and Pure Direct sound modes.
- **Auto standby**
  - **Description**: How long the receiver stays idle before it switches itself to standby. Unlike the other settings, it can be changed while any zone is on.
  - **Options**: Off, 15 minutes, 30 minutes, 60 minutes, 2 hours, 4 hours, 8 hours
- **Display dimmer**
  - **Description**: Front-panel display brightness.
  - **Options**: Off, Dark, Dim, Bright
- **Eco mode**
  - **Description**: The receiver's power-saving mode.
  - **Options**: On, Auto, Off

## Switch

The `denonavr` integration creates the following [Switch](/integrations/switch/) entities on the receiver's device, as configuration entities.

- **Audyssey Dynamic EQ**
  - **Description**: Adjusts the frequency response to compensate for listening at low volume. This is the same setting as the `denonavr.set_dynamic_eq` action.
  - **Availability**: Unavailable when the receiver has no Audyssey, when Audyssey MultEQ is off, and in the Direct and Pure Direct sound modes. The receiver ignores Dynamic EQ changes in all of these. While Dynamic EQ is off, the **Audyssey reference level offset** select is unavailable; while it is on, the tone control entities are.
- **Tone control**
  - **Description**: Turns the receiver's tone control on or off. Setting **Tone control bass** or **Tone control treble** turns it on.
  - **Availability**: Unavailable when the receiver does not support tone control, while the **Audyssey Dynamic EQ** switch is on, in the Direct and Pure Direct sound modes, and until the receiver first reports it. The receiver ignores bass, treble and tone control changes while Dynamic EQ is on and in Direct and Pure Direct.

A setting can only be changed while the zone it applies to is on. While that zone is off, the change is refused with an error, because the receiver accepts it in standby without applying it. The `denonavr.set_dynamic_eq` action is refused the same way while the main zone is off, even when it targets another zone's media player.

{% note %}
With **Use Telnet connection** enabled, a change made on the receiver itself or in its app shows up in Home Assistant right away for every entity above. Without Telnet, **Auto standby**, **Display dimmer**, **Eco mode** and the tone control entities follow on the next regular update, while the Audyssey selects and **Audyssey Dynamic EQ** are only picked up when **Update Audyssey settings** is enabled, which reads the Audyssey settings on every update. Some receivers take up to 10 seconds to answer that request, which is why the option is off by default.
{% endnote %}

{% include integrations/actions.md %}

[Denon]: /integrations/denon
