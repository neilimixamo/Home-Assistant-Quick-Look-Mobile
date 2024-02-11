# Changelogs

## [2024-02-11]
### Fixes
-  `security.yaml` and `security_expandable.yaml` updated to v2.0.3 including the fix for the door-open icon size issue and the disabling of the icon tap action
-  `alarm_footer` updated to v2.0.1 including the addition of an icon tap_action to seamlessly toggle the alarm between armed_away and disarmed states

## [2023-11-07]
- `routines_footer (v2.0.3).yaml` template has been improved to seamlessly trigger scenes, scripts and/or automations with no more need to specify a "routine_type" variable.
  
<p align="center">
    <img src="https://github.com/neilimixamo/Home-Assistant-Quick-Look-Mobile/assets/43101688/f09578d9-9d4a-4513-b1ce-497eb0628ac2" alt="Image">
</p>

- Default views using this template have also been updated accordingly:
`1.1_home (v2.0.2).yaml`
`4.1_light_bulbs (v2.0.2).yaml`
`4.2_light_covers (v2.0.2).yaml`
`4.1.1_light_bulbs_expanded_1 (v2.0.2).yaml`
`4.1.2_light_bulbs_expanded_1 (v2.0.2).yaml`
`4.2.1_light_covers_expanded_1 (v2.0.2).yaml`
`5.1_media_audio (v2.0.1).yaml`
`5.2_media_video (v2.0.1).yaml`
`5.1.1_media_audio_expanded_1 (v2.0.1).yaml`
`5.1.2_media_video_expanded_1 (v2.0.1).yaml`
`6.1_devices_favorites (v2.0.2).yaml`
`6.1.1_devices_expanded_1 (v2.0.1).yaml`
`7.1_persons (2.0.2).yaml`
`7.2_map (v2.0.1).yaml`

## [2023-11-06]
### New
- The `light(_expandable) (v2.0.2).yaml` cards can now provide battery badge status, useful for battery-powered light switches.

<p align="center">
    <img src="https://github.com/neilimixamo/Home-Assistant-Quick-Look-Mobile/assets/43101688/8f8efb0b-d49c-4e17-8fc8-eaa2d08730fa" alt="Image">
</p>

## [2023-11-04]
### Reduced Frontend Load
- With `basic_card (v2.0.1).yaml` and `basic_card_expandable (v2.0.1)`, cards will now only update themselves when there are changes in entity or battery states, rather than updating with every type of entity change.
- `climate(_expandable) v2.0.1.yaml`, `media(_expandable) v2.0.2.yaml` and `media_expanded (2.0.1).yaml`  will also update when there is a change in their temperature or remote variable states.
### Fixes
- Updated `badge_battery (v2.0.2).yaml`, `security (v2.0.1)`, `security_expandable (v2.0.1)` to fix a low battery icon showing when the battery is fully charged at 100%.

## [2023-10-29]
- QLM theme updated to v2.0.2: The native header bar is hidden by default and no longer requires the custom component browser-mod.

## [2023-10-22]
- Renamed the `scenes_footer.yaml` template to `routines_footer.yaml`, which now handles script actions in addition to scene actions depending on the new `routine_type` variable.
- Updated dashboard views accordingly 
  
## [2023-09-16]
- Added `start_listening: true` to the upper right Assist button

## [2023-07-23]
### Fixes
-  `cover.yaml` and `cover_expandable.yaml` updated to v2.0.1: Fixed icon.

## [2023-07-06]
### Fixes
-  `person.yaml` and `person_expandable.yaml` updated to v2.0.1: Fixed image and badge positions.
-  `badge_battery.yaml` updated to v2.0.1: Added border color to match the header badges style.
  
## [2023-07-04]
### Fixes
-  `quick_look_mobile_macros (v2.0.1).jinja` renamed to `quick_look_mobile_macros.jinja` as it was resulting in the absence of header colors and badges.

## [2023-07-03]
### Fixes
- `light.yaml` and `light_expandable.yaml` updated to v2.0.1: Fixed color and label issues when no brightness feedback is available.
- `media.yaml` and `media_expandable.yaml` updated to v2.0.1: Enable overriding the default label with a custom label variable.
- `header.yaml` updated to v2.0.1: Fixed issue with box-shadow of the media header not being displayed.

## [2023-07-02] : Quick Look Mobile v2.0.0

<p align="center">
    <img src="https://github.com/neilimixamo/Home-Assistant-Quick-Look-Mobile/assets/43101688/6c649318-d1e8-4601-bbc3-70736457260e" alt="Image">
</p>

### Breaking Changes: 
- Full reinstall recommended for those who used v1.0

### New Features :
  - Dark Mode.
  - Active entity counters displayed as badges in the header, to be defined in the `/config/custom_templates/quick_look_mobile_macros.jinja` file.
  - Wider template cards options :
    - `_expandable.yaml` version for each card, allowing navigation to subview pages, specifically designed for group management.
    - `media_expanded.yaml` version to provide a full width of active media content when grid columns is set to "1" (instead of default "2").
    - remote variable to the `media.yaml` cards, allowing to turn TV on/off by clicking on the icon.
    - battery variable added to all cards (except for the light, media, and camera cards) for tracking the battery level of each entity. When the battery level is below 60%, a yellow battery badge will be displayed. When the battery level drops below 25%, a red battery badge will be displayed.
    - lock variable added to the `security.yaml` cards, complementing the existing occupancy and contact binary_sensors entities. At least one of the three entities is required. If multiple entities are provided, the card will prioritize displaying open door sensors > motion detection sensors > unlocked locks when activated.


## [2023-06-21]
### New Features
- `climate.yaml` updated to version 1.2:
  - Handles various hvac_modes. While version 1.1 was limited to the "heat" mode, the updated version should now manage multiple modes including "auto", "heat/cool", "heat", "cool", "fan", and "dry", and dynamically adjusts the card's color based on the selected mode.
  - Add variable `temp_unit` to choose between celsius (by default) or fahrenheit.
- `fan.yaml` updated to version 1.2:
  - Style : orange color has been replaced with blue color to better represent cooling, while keeping orange for heating entities.
  - In addition to recognizing the "on" state, it now also recognizes any "fan" containing state.

## [2023-06-20]
### Fixes
- `subheader_1.yaml` and `subheader_2.yaml` updated to version 1.1: No more cropped letters in contact with the corners of its container.

