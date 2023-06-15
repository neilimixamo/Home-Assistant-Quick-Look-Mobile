# Home Assistant - Quick Look Mobile

Welcome to the Quick Look Mobile Dashboard for Home Assistant! 

- This dashboard offers a minimalist mobile interface for a simple home devices management. 
- It is designed to
  - Deliver crucial information at a glance, such as "Is there someone in the house?", "Is there an open door or window?", or "Did I forget to turn a light off ?"
  - Facilitate rapid navigation to any desired device in just two clicks, while still maintaining complete access to all of their controls.

## Demo
Here is a video presentation of the dashboard :
<p align="center">
  <a href="https://www.youtube.com/watch?v=hZRSu72m1gw">
    <img src="https://img.youtube.com/vi/hZRSu72m1gw/0.jpg" alt="Step-by-Step Video">
  </a>
</p>

You can also try the [Figma Demo](https://www.figma.com/proto/G7cHGCjgFJwMrq9WdT41gv/HA---Quick-Look-Mobile?node-id=153-1125&starting-point-node-id=153%3A1006&scaling=scale-down) before installation.

## Prerequisites

Before beginning, make sure you have:

- Familiarity with YAML and Home Assistant configuration files.
- HACS with following integrations:
  - [Button Card](https://github.com/custom-cards/button-card) by RomRider
  - [Slider Card](https://github.com/AnthonMS/my-cards) by Anton MS
  - [Layout Card](https://github.com/thomasloven/lovelace-layout-card) by Thomas Lovén
  - [Browser Mod 2](https://github.com/thomasloven/hass-browser_mod) by Thomas Lovén
  - [Card Mod 3](https://github.com/thomasloven/lovelace-card-mod) by Thomas Lovén

## Installation

### 1. Download and Extract Dashboard Files

- Click on the 'Code' button, then select 'Download ZIP'.
- Save the ZIP file to a location on your computer.
- Extract the contents of the ZIP file.

### 2. Copy Folders to Your Home Assistant Server

- Using your preferred method (Visual Studio Code, Samba, SSH, local access, etc.),
- Copy the three extracted folders (`/dashboards`, `/entities` and `/themes`) to your `/config` directory.

### 3. Setup `configuration.yaml`

```yaml
frontend:
  themes: !include_dir_merge_named themes/

lovelace:
  mode: storage
  dashboards: !include dashboards/dashboards.yaml
  
sensor: !include_dir_list entities/sensors/
```

<details>
<summary>sensor: alternative</summary>
  
You might need to modify these lines to match your current setup, particularly if you don't want to split your sensor configuration across multiple files. Here is the non-splitted alternative:

```yaml
sensor: 
  - platform: template
    sensors: 
      some_alarms_are_on:
        friendly_name: "Some Alarms Are On"
        value_template: >-
          {% set entity_ids = [
            'alarm_control_panel.your_entity'
            ] %}

          {% set count = namespace(value=0) %}

          {% for entity_id in entity_ids %}
            {% if is_state(entity_id, 'triggered') or is_state(entity_id, 'pending') %}
              {% set count.value = count.value + 1 %}
            {% endif %}
          {% endfor %}

          {{ 'off' if count.value == 0 else 'on' }}

  - platform: template
    sensors:
      some_contact_sensors_are_on:
        friendly_name: "Some Contact Sensors Are On"
        value_template: >-
          {% set entity_ids = [
            'binary_sensor.your_entity', 
            'binary_sensor.your_entity',
            'binary_sensor.your_entity',
            'binary_sensor.your_entity',
            'binary_sensor.your_entity'
            ] %}

          {% set count = namespace(value=0) %}

          {% for entity_id in entity_ids %}
            {% if is_state(entity_id, 'on') %}
              {% set count.value = count.value + 1 %}
            {% endif %}
          {% endfor %}

          {{ 'off' if count.value == 0 else 'on' }}

  - platform: template
    sensors:
      some_occupancy_sensors_are_on:
        friendly_name: "Some Occupancy Sensors Are On"
        value_template: >-
          {% set entity_ids = [
            'binary_sensor.your_entity',
            'binary_sensor.your_entity',
            'binary_sensor.your_entity',
            'binary_sensor.your_entity',
            'binary_sensor.your_entity',
            'binary_sensor.your_entity',
            'binary_sensor.your_entity'
            ] %}

          {% set count = namespace(value=0) %}

          {% for entity_id in entity_ids %}
            {% if is_state(entity_id, 'on') %}
              {% set count.value = count.value + 1 %}
            {% endif %}
          {% endfor %}

          {{ 'off' if count.value == 0 else 'on' }}

  - platform: template
    sensors:
      some_climates_are_on:
        friendly_name: "Some climates are on"
        value_template: >-
          {% set entity_ids = [
            'climate.your_entity',
            'climate.your_entity',
            'climate.your_entity'
            ] %}

          {% set count = namespace(value=0) %}

          {% for entity_id in entity_ids %}
            {% if is_state(entity_id, 'heat') or is_state(entity_id, 'on') %}
              {% set count.value = count.value + 1 %}
            {% endif %}
          {% endfor %}

          {{ 'off' if count.value == 0 else 'on' }}

  - platform: template
    sensors:
      some_fans_are_on:
        friendly_name: "Some fans are on"
        value_template: >-
          {% set entity_ids = [
            'fan.your_entity',
            'fan.your_entity',
            'fan.your_entity'
            ] %}

          {% set count = namespace(value=0) %}

          {% for entity_id in entity_ids %}
            {% if is_state(entity_id, 'on') %}
              {% set count.value = count.value + 1 %}
            {% endif %}
          {% endfor %}

          {{ 'off' if count.value == 0 else 'on' }}

  - platform: template
    sensors:
      some_lights_are_on:
        friendly_name: "Some Lights Are On"
        value_template: >-
          {% set entity_ids = [
            'light.your_entity',
            'light.your_entity',
            'light.your_entity',
            'light.your_entity',
            'light.your_entity',
            'light.your_entity',
            'light.your_entity',
            'light.your_entity'
            ] %}

          {% set count = namespace(value=0) %}

          {% for entity_id in entity_ids %}
            {% if is_state(entity_id, 'on') %}
              {% set count.value = count.value + 1 %}
            {% endif %}
          {% endfor %}

          {{ 'off' if count.value == 0 else 'on' }}

  - platform: template
    sensors:
      some_media_players_are_on:
        friendly_name: "Some Media Players Are On"
        value_template: >-
          {% set entity_ids = [
            'media_player.your_entity',
            'media_player.your_entity',
            'media_player.your_entity',
            'media_player.your_entity'
            ] %}

          {% set count = namespace(value=0) %}

          {% for entity_id in entity_ids %}
            {% if is_state(entity_id, 'playing') %}
              {% set count.value = count.value + 1 %}
            {% endif %}
          {% endfor %}

          {{ 'off' if count.value == 0 else 'on' }}

  - platform: template
    sensors:
      some_devices_are_on:
        friendly_name: "Some Devices Are On"
        value_template: >-
          {% set entity_ids = [
            'switch.your_entity',
            'switch.your_entity',
            'switch.your_entity',
            'switch.your_entity',
            'switch.your_entity',
            'vacuum.your_entity',
            'vacuum.your_entity'
            ] %}

          {% set count = namespace(value=0) %}

          {% for entity_id in entity_ids %}
            {% if is_state(entity_id, 'on') or is_state(entity_id, 'cleaning')%}
              {% set count.value = count.value + 1 %}
            {% endif %}
          {% endfor %}

          {{ 'off' if count.value == 0 else 'on' }}
```
</details>

### 4. Reboot and Apply Theme

- Restart your Home Assistant for the changes to take effect.
- Once rebooted, apply the 'Quick Look Mobile' theme and select 'light mode'.
- On the left lateral menu, open the newly created dashboard. 
- Since this dashboard is designed for mobile view, it might appear too large on a computer screen. To correct this, press F12 or open your browser's developer tools and select the 'mobile view' option.

## Dashboard Structure
  
  - This dashboard is pre-configured with 15 distinct views, which are uniformly structured and can be accessed at `/config/dashboard/quick_look_mobile/views/`.
  - `1.1_home.yaml` corresponds to your home view, `2.1_security_access.yaml` corresponds to your security access view, and so forth.
  - Each view represents a unique mobile interface that can be navigated to, using the header and subheader sections.
  - The remaining sections, from top to bottom, include the main title, main, footer title and footer spaces.
  
  ### 1. Header
  
  - The header is designed for two main purposes: 
    1) allow for __rapid navigation__ through five main categories, each leading to different views: `Security`, `Air`, `Light`, `Media`, and `Devices`. Additionally, there is a special `Family` category which can be accessed through the upper left person icon. If none of those categories is selected, `Home` view will be displayed. You can also navigate back to `Home` by clicking again on the active category.
    2) provide useful __status information__ by changing its color and icon based on 'template sensors' (see [Customize Template Sensors](#customize-template-sensors)) e.g. if a lightbulb is turned on, the light category will turn yellow. If no entities are active, it will revert to its default grey color. This feature provides a quick and easy way to identify the status of your various devices and systems.
   
  ### 2. SubHeader
  
  - Each of the Header categories further has two subcategories :
    - `Home` includes `Favorites` and `Energy` (this last one is no functional yet),
    - `Security` includes `Access` and `Video`,
    - `Air` includes `Heating` and `Cooling`,
    - `Light` includes `Bulbs` and `Covers`,
    - `Media` includes `Music` and `TV`,
    - `Devices` includes `Rooms` and `Favorites`,
    - `Family` includes `Members` and `Map`.
   
  ### 3. Main
  
  - This section is designed with a two-column layout that can display eight cards at once.
  - However, it does not limit the total number of cards as it allows for vertical scrolling to view and interact with an unlimited number of cards.
  - Each card is structured with an icon on the left, acting as a switch, and a name&label on the right, providing the more-info dialog for full control.
  - To configure those cards with your entities, refer to [Add your Entities](#add-your-entities).
  
  ### 4. Footer
  
  - This section is primarily designed for scene management, offering group controls or shortcuts for quick actions. However, when scenes are not relevant, it can be used to display specialized cards such as the alarm or weather cards.


## Add Your Entities

- Open the file corresponding to the view you want add entities to. eg open the `3.1_air_heating.yaml` file to add your climate and temperature sensors.
- To avoid disrupting the setup, only modify the lines where it is explicitly mentioned ```#can be changed, #required or #optional``` at the end. These lines have been marked for easy and safe modification.
- Navigate to the "main" section in the view file. By default, you'll find 16 empty entities but you can also add or delete some blocks, based on your needs.
- Each entity block requires certain variables to be defined. For a climate entity, you'll define `entity` and `name`. `Entity` is the entity_id of your device (e.g., `climate.kitchen`), and `name` is optional; it's the name that will be displayed on the dashboard. If no name is given, the friendly name of the entity will be used.
- Refresh your dashboard to see the changes by clicking the three dots in the upper-right corner of the Home Assistant interface.
- Repeat the above steps to all your views.

## Customize Template Sensors

- Each sensor contains a list of entities that are intended to trigger the header for color change if at least one is active.
- To modify or add entities to a template sensor, open the corresponding file and adjust the entity list.
- Template sensors are located at `/config/entities/sensors/quick_look_mobile` or at `/config/configuration.yaml` depending on your [configuration.yaml setup](#3-setup-configurationyaml).
- Entities should match those you chose for the corresponding view e.g `some_lights_are_on.yaml` template sensor should match the entities you selected first in '`4.1_light_bulbs.yaml` view.
- Dont't put a comma after the last entity.
- After modification, remember to (quick) restart your Home Assistant for the yaml changes to take effect.

##  Translations (Optional)

- The Titles for Subheader, Main, and Footer sections can be easily modified or translated in their corresponding view YAML files, located in `/config/dashboards/quick_look_mobile/views/` where `#can be changed` is mentioned.
- If you need to translate Header titles or any content within a card (such as the weather card) that can't be modified directly via its view file, you will need to adjust the corresponding template YAML file, located in `/config/dashboards/quick_look_mobile/templates/`.

## Hide the Native Header (Optional)

- To improve the aesthetics of the dashboard, you may want to hide the native upper horizontal header.
- Open the browser mod integration settings.
- Select 'Hide Header'.
- Choose the mobile device on which you wish to hide the header. The dashboard will look cleaner on mobile without it.

## Known Issues and Fixes

- If the native header is hidden, the lateral menu can't be accessed from the views. To access it again, press the 'dev' button located at the bottom of the screen.
- Currently, the 'assist' icon located at the upper right of the dashboard isn't functional as the way to trigger this dialog keeps unclear for me.

Enjoy your new, customized mobile dashboard for Home Assistant!


