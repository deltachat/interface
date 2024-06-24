# Known UI config keys

| key                                                              | meaning                                                                      | usage                          |
| ---------------------------------------------------------------- | ---------------------------------------------------------------------------- | ------------------------------ |
| `ui.lastchatid`                                                  | stores last seleted chat id                                                  | used by desktop and deltatouch |
| `ui.custom_webrtc_instance`                                      | to persist value of custom video chat url option                             | used by ios                    |
|                                                                  |                                                                              |                                |
| `ui.desktop.muted`                                               | `"1"` means this account is muted, anything else is interpreted as not muted | used by desktop and deltatouch |
| `ui.desktop.webxdcBounds.<msg_id>`                               | contains json object with window bounds[^1]                                  | used by desktop                |
|                                                                  |                                                                              |                                |
| `ui.ios.show_system_contacts`, `ui.android.show_system_contacts` | whether system contact list should be imported to dc contact list            | used by ios and android        |

[^1]: for example `{ x: 25, y: 38, width: 800, height: 600 }`
