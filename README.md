# Chromecast MQTT connector

Provides status information and control capabilities of your Chromecast devices via MQTT.

## Installation requirements

* Python 3
* pychromecast
* paho-mqtt

## Discovery and control

Using MQTT you can find the following topics. `IP` is the ip address used to connect
to each Chromecast.

```
# - read only
chromecast/IP/friendly_name
chromecast/IP/connection_status
chromecast/IP/cast_type
chromecast/IP/current_app
chromecast/IP/player_duration
chromecast/IP/media/title
chromecast/IP/media/album_name
chromecast/IP/media/artist
chromecast/IP/media/album_artist
chromecast/IP/media/track
chromecast/IP/media/images
chromecast/IP/media/content_type
chromecast/IP/media/content_url

# - read- and writable
chromecast/IP/volume_level
chromecast/IP/volume_muted
chromecast/IP/player_position
chromecast/IP/player_state
```

Control the player by publishing values to the four topics above.


Change volume using values from `0` to `100`:

* Absolute: publish e.g. `55` to `chromecast/192.168.0.1/volume_level`
* Relative: publish e.g. `+5` or `-5` to `chromecast/192.168.0.1/volume_level`


Change mute state: publish `0` or `1` to `chromecast/192.168.0.1/volume_muted`.


Play something: Publish a json array with two elements (content url and content type) to
`chromecast/192.168.0.1/player_state`, e.g. `["http://your.stream.url.here", "audio/mpeg"]`.


For other player controls, simply publish e.g. `RESUME`, `PAUSE`, `STOP`, `SKIP` or `REWIND` to
`chromecast/192.168.0.1/player_state`.
