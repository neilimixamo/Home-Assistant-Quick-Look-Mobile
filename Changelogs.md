# Changelog

## [2023-07-03]
### Fixes
- `light.yaml` and `light_expandable.yaml` updated to v2.0.1: Fixed color and label issues when no brightness feedback is available.
- `header.yaml` updated to v2.0.1: Fixed issue with box-shadow of the media header not being displayed.

## [2023-07-02] : Quick Look Mobile v2.0.0

### Breaking Changes: 
- Full reinstall recommended for those who used v1.0

### New Features :
  - Dark Mode.
  - Active entity counters displayed as badges in the header, to be defined in the `/config/custom_templates/quick_look_mobile_macros.jinja` file.
  - Wider template cards options :
    - `_expandable.yaml` version for each card, allowing navigation to subview pages, specifically designed for group management.
    - `media_expanded.yaml` version to provide a full width of active media content when grid columns is set to "1" (instead of default "2").
    - remote variable to the `media.yaml` cards, allowing to turn TV on/off on the icon click.
    - battery variable for tracking the battery level of each entity. When the battery level is below 60%, a yellow battery badge will be displayed. When the battery level drops below 25%, a red battery badge will be displayed.
    - lock variable to the `security.yaml` cards, complementing the existing occupancy and contact binary_sensors entities. At least one of the three entities is required. If multiple entities are provided, the card will prioritize displaying open door sensors > motion detection sensors > unlocked locks when activated.


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

