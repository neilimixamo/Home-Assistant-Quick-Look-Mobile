
<a href="https://www.buymeacoffee.com/neilimixamo" target="_blank"><img src="https://cdn.buymeacoffee.com/buttons/default-orange.png" alt="Buy Me A Coffee" height="41" width="174"></a>

# Home Assistant - Quick Look Mobile

Welcome to the Quick Look Mobile Dashboard for Home Assistant! 

- This dashboard offers a minimalist mobile interface for a simple home devices management. 
- It is designed to
  - Facilitate rapid navigation to any desired device in just two clicks, while still maintaining access to all of their controls.   
  - Deliver crucial information at a glance, such as "is my home secure? Is it occupied? Are there any lights turned on? If yes, how many?"

![Quick Look Mobile v2](https://github.com/neilimixamo/Home-Assistant-Quick-Look-Mobile/assets/43101688/0c11ab3b-8e5f-40ae-be24-5580a257b7c8)

## Demo

You can watch the [Video Presentation](https://www.youtube.com/watch?v=hZRSu72m1gw) of the v1 dashboard :
Or even try the [Figma Demo](https://www.figma.com/proto/G7cHGCjgFJwMrq9WdT41gv/HA---Quick-Look-Mobile?node-id=153-1125&starting-point-node-id=153%3A1006&scaling=scale-down) before installation.

## Prerequisites

Before beginning, make sure you have:

- Familiarity with YAML and Home Assistant configuration files.
- HACS with following integrations:
  - [Button Card](https://github.com/custom-cards/button-card) by RomRider
  - [Slider Card](https://github.com/AnthonMS/my-cards) by Anton MS
  - [Layout Card](https://github.com/thomasloven/lovelace-layout-card) by Thomas Lovén
  - [Card Mod](https://github.com/thomasloven/lovelace-card-mod) by Thomas Lovén
  - [Browser Mod](https://github.com/thomasloven/hass-browser_mod) by Thomas Lovén (custom component)

## Installation

### 1. Download and Extract Dashboard Files

- Click on the 'Code' button, then select 'Download ZIP'.
- Save the ZIP file to a location on your computer.
- Extract the contents of the ZIP file.

### 2. Copy Folders to Your Home Assistant Server

- Using your preferred method (Visual Studio Code, Samba, SSH, local access, etc.),
- Copy the four extracted folders (`/custom_templates`, `/dashboards`, `/entities` and `/themes`) to your `/config` directory.

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
    
    ############################
    #
    # SECURITY MONITORING
    #
    ############################
    
    # ALARMS :
      some_alarms_are_on:
        friendly_name: "Some Alarms Are On"
        value_template: >-
          {% from 'quick_look_mobile_macros.jinja' import some_alarms_are_on %}
          {{ some_alarms_are_on().split(',')[0] }}
    
      alarms_count:
        friendly_name: "Alarms Count"
        value_template: >-
          {% from 'quick_look_mobile_macros.jinja' import some_alarms_are_on %}
          {{ some_alarms_are_on().split(',')[1] }}
    
    
    # DOORS & WINDOWS :
      some_contact_sensors_are_on:
        friendly_name: "Some Contact Sensors Are On"
        value_template: >-
          {% from 'quick_look_mobile_macros.jinja' import some_contact_sensors_are_on %}
          {{ some_contact_sensors_are_on().split(',')[0] }}
    
      contact_sensors_count:
        friendly_name: "Contact Sensors Count"
        value_template: >-
          {% from 'quick_look_mobile_macros.jinja' import some_contact_sensors_are_on %}
          {{ some_contact_sensors_are_on().split(',')[1] }}
    
    
    # PRESENCES :
      some_occupancy_sensors_are_on:
        friendly_name: "Some Occupancy Sensors Are On"
        value_template: >-
          {% from 'quick_look_mobile_macros.jinja' import some_occupancy_sensors_are_on %}
          {{ some_occupancy_sensors_are_on().split(',')[0] }}
    
      occupancy_sensors_count:
        friendly_name: "Occupancy Sensors Count"
        value_template: >-
          {% from 'quick_look_mobile_macros.jinja' import some_occupancy_sensors_are_on %}
          {{ some_occupancy_sensors_are_on().split(',')[1] }}
    
    # LOCKS :
      some_locks_are_on:
        friendly_name: "Some Locks Are On"
        value_template: >-
          {% from 'quick_look_mobile_macros.jinja' import some_locks_are_on %}
          {{ some_locks_are_on().split(',')[0] }}
    
      locks_count:
        friendly_name: "Locks Count"
        value_template: >-
          {% from 'quick_look_mobile_macros.jinja' import some_locks_are_on %}
          {{ some_locks_are_on().split(',')[1] }}
    
    
    ############################
    #
    # AIR MONITORING
    #
    ############################
    
    
    # CLIMATES :
      some_climates_are_on:
        friendly_name: "Some Climates Are On"
        value_template: >-
          {% from 'quick_look_mobile_macros.jinja' import some_climates_are_on %}
          {% set count = some_climates_are_on().split(',')[1]|int %}
          {{ 'on' if count > 0 else 'off' }}
    
      climates_dominance:
        friendly_name: "Climates Dominance"
        value_template: >-
          {% from 'quick_look_mobile_macros.jinja' import some_climates_are_on %}
          {{ some_climates_are_on().split(',')[0] }}
          
      climates_count:
        friendly_name: "Climates Count"
        value_template: >-
          {% from 'quick_look_mobile_macros.jinja' import some_climates_are_on %}
          {{ some_climates_are_on().split(',')[1] }}
    
    # FANS :
      some_fans_are_on:
        friendly_name: "Some Fans Are On"
        value_template: >-
          {% from 'quick_look_mobile_macros.jinja' import some_fans_are_on %}
          {{ some_fans_are_on().split(',')[0] }}
    
      fans_count:
        friendly_name: "Fans Count"
        value_template: >-
          {% from 'quick_look_mobile_macros.jinja' import some_fans_are_on %}
          {{ some_fans_are_on().split(',')[1] }}
    
    
    ############################
    #
    # LIGHT
    #
    ############################
    
    # LIGHTBULBS :
      some_lights_are_on:
        friendly_name: "Some Lights Are On"
        value_template: >-
          {% from 'quick_look_mobile_macros.jinja' import some_lights_are_on %}
          {{ some_lights_are_on().split(',')[0] }}
    
      lights_count:
        friendly_name: "Lights Count"
        value_template: >-
          {% from 'quick_look_mobile_macros.jinja' import some_lights_are_on %}
          {{ some_lights_are_on().split(',')[1] }}
    
    # COVERS :
      some_covers_are_on:
        friendly_name: "Some Covers Are On"
        value_template: >-
          {% from 'quick_look_mobile_macros.jinja' import some_covers_are_on %}
          {{ some_covers_are_on().split(',')[0] }}
    
      covers_count:
        friendly_name: "Covers Count"
        value_template: >-
          {% from 'quick_look_mobile_macros.jinja' import some_covers_are_on %}
          {{ some_covers_are_on().split(',')[1] }}
    
    
    ############################
    #
    # MEDIA PLAYERS MONITORING
    #
    ############################
    
    # AUDIO PLAYERS :
      some_audio_players_are_on:
        friendly_name: "Some Audio Players Are On"
        value_template: >-
          {% from 'quick_look_mobile_macros.jinja' import some_audio_players_are_on %}
          {{ some_audio_players_are_on().split(',')[0] }}
    
      audio_players_count:
        friendly_name: "Audio Players Count"
        value_template: >-
          {% from 'quick_look_mobile_macros.jinja' import some_audio_players_are_on %}
          {{ some_audio_players_are_on().split(',')[1] }}
    
    
    # VIDEO PLAYERS :
      some_video_players_are_on:
        friendly_name: "Some Video Players Are On"
        value_template: >-
          {% from 'quick_look_mobile_macros.jinja' import some_video_players_are_on %}
          {{ some_video_players_are_on().split(',')[0] }}
    
      video_players_count:
        friendly_name: "Video Players Count"
        value_template: >-
          {% from 'quick_look_mobile_macros.jinja' import some_video_players_are_on %}
          {{ some_video_players_are_on().split(',')[1] }}
    
    
    
    ############################
    #
    # EQUIPMENT MONITORING
    #
    ############################
    
    # DEVICES (SWITCHES, VACUUMS, SENSORS, etc) :
      some_devices_are_on:
        friendly_name: "Some Devices Are On"
        value_template: >-
          {% from 'quick_look_mobile_macros.jinja' import some_devices_are_on %}
          {{ some_devices_are_on().split(',')[0] }}
    
      devices_count:
        friendly_name: "Devices Count"
        value_template: >-
          {% from 'quick_look_mobile_macros.jinja' import some_devices_are_on %}
          {{ some_devices_are_on().split(',')[1] }}

```
</details>

### 4. Reboot and Apply Light or Dark Theme

- Restart your Home Assistant for the changes to take effect.
- Once rebooted, apply the 'Quick Look Mobile' theme.
- On the left lateral menu, open the newly created dashboard. 
- Since this dashboard is designed for mobile view, it might appear too large on a computer screen. To correct this, press F12 or open your browser's developer tools and select the 'mobile view' option.

## Dashboard Structure
  
  - This dashboard is pre-configured with 14 distinct views, which are uniformly structured and can be accessed at `/config/dashboard/quick_look_mobile/views/`.
  - `1.1_home.yaml` corresponds to your home view, `2.1_security_sensors.yaml` corresponds to your security sensors view, and so forth.
  - Each view represents a unique mobile interface that can be navigated to, using the header and subheader sections.
  - The remaining sections, from top to bottom, include main part, footer title and footer spaces.
  
  ### 1. Header
  
  - The header is designed for two main purposes: 
    1) allow for __rapid navigation__ through five main categories, each leading to different views: `Security`, `Air`, `Light`, `Media`, and `Equipment`. Additionally, there is a special `Family` category which can be accessed through the upper left person icon. If none of those categories is selected, `Home` view will be displayed. You can also navigate back to `Home` by clicking again on the active category.
    2) provide useful __status information__ by changing its color and icon based on 'template sensors' (see [Customize Header Monitoring](#customize-header-monitoring)) e.g. if a lightbulb is turned on, the light category will turn yellow. If no entities are active, it will revert to its default grey color. This feature provides a quick and easy way to identify the status of your various devices and systems.
  - Sometimes, icons and colors can change with a predefined priority order. For example, in the Security header, the priority is given to the triggered alarm, followed by open doors, detected motion and unlocked locks.
   
  ### 2. SubHeader
  
  - Each of the Header categories further has two subcategories :
    - `Home` includes `Favorites` and `Energy` (this last one is no functional yet),
    - `Security` includes `Sensors` and `Cameras`,
    - `Air` includes `Climates` and `Fans`,
    - `Light` includes `Bulbs` and `Covers`,
    - `Media` includes `Audio` and `Video`,
    - `Equipment` includes `Favorites` and `All`,
    - `Family` includes `Members` and `Map`.
   
  ### 3. Main
  
  - This section is designed with a two-column layout that can display eight cards at once.
  - However, it does not limit the total number of cards as it allows for vertical scrolling to view and interact with an unlimited number of cards.
  - Each card is structured with an icon on the left, usually acting as a switch, and a name&label container on the right, providing the more-info dialog when clicked for full control.
  - To configure those cards with your entities, refer to [Add your Entities](#add-your-entities).
  
  ### 4. Footer
  
  - This section is primarily designed for scene management, offering group controls or shortcuts for quick actions. However, when scenes are not relevant, it can be used to display specialized cards such as the alarm or weather cards.


## Add Your Entities

- Open the file corresponding to the view you want add entities to. eg open the `3.1_air_climates.yaml` file to add your climate and temperature sensors.
- I recommend starting by customizing views 2.1 to 7.2 to familiarize yourself with the process of templates and variables, then proceed to view 1.1, which provides a wider range of customization options.
- - Navigate to the [Main](#3-main) section in the view file. By default, you'll find 16 empty entities but you can also add or delete some, depending on your needs.
- To avoid disrupting the setup, only modify the lines where it is explicitly mentioned `#can be changed, #required or #optional` at the end. These lines have been marked for easy and safe modification.
- Each entity block requires certain parameters to be defined :
  
### Card Templates
Each entity is associated with a predefined template card. 
The available cards include :
  - `climate`,
  - `climate_expandable`,
  - `cover`,
  - `cover_expandable`,
  - `device`,
  - `device_expandable`,
  - `fan`,
  - `fan_expandable`,
  - `light`,
  - `light_expandable`,
  - `media`,
  - `media_expandable`,
  - `media_expanded`,
  - `person`,
  - `person_expandable`,
  - `security`,
  - `security_expandable`.
- You will notice that each template has an 'expandable' version, which allows expanding the entity to a subview that includes other entities, thanks to the `expand_to` variable.
This feature is particularly useful for managing groups.
- Expanded views can be customized or created in the same way as existing views in `/dashboards/quick_look_mobile/views/expanded/`.
- Expandable cards can also include other 'expandable' cards without nesting limit.

### Variables
- Variables provide you with the flexibility to personalize the cards according to your devices and personal information.
- Some are optional and clearly indicated in the view file that you'll be modifying.
- For a `climate` template card , you'll have to define `entity`, `name`, `temperature`, `temperature_unit`, `battery`, `expand_to`. `Entity` is the entity_id of your device (e.g., `climate.kitchen`), others are optional. When no name is given, the friendly name of the entity will be used.
  
- Refresh your dashboard to see the changes by clicking the three dots in the upper-right corner of the Home Assistant interface.
- Repeat the above steps to all your views.

## Customize Header Monitoring

- The Header is designed to change color and display badge counts based on active devices.
- It is, however, not directly linked to the configured cards in each view.
- To monitor specific entities, an intermediate step of entities listing is required.
- Lists can be modified at `/config/custom_templates/quick_look_mobile_macros.jinja/` where `your_entity` have to be replaced by your entity_ids.
- It is logical, but not mandatory, to list the same entities as those configured in each view.
- Call `service: homeassistant.reload_custom_templates` or restart Home Assistant for the changes to take effect.


###### If you don't like or don't want to use badge counts, you can disable this feature by changing `show_badge: true` to `show_badge: false` in `/dashboards/quick_look_mobile/templates/layout/header_category.yaml` (line 5)


##  Translations (Optional)

- The Titles for Subheader, Main, and Footer sections can be easily modified or translated in their corresponding view YAML files, located in `/config/dashboards/quick_look_mobile/views/` where `#can be changed` is mentioned.
- If you need to translate Header titles or any content within a card (such as the weather card) that can't be modified directly via its view file, you will need to adjust the corresponding template YAML file, located in `/config/dashboards/quick_look_mobile/templates/`.

## Hide the Native Header (Optional)

- To improve the aesthetics of the dashboard, you may want to hide the native upper horizontal header.
- Open the browser mod integration settings.
- Select 'Hide Header'.
- Choose the mobile device on which you wish to hide the header. To successfully hide it on local and external browsing, it’s important to consider your phone as two separate devices with their own Browser ID, each needing to be identified in Browser Mod.

## Known Issues
- If the native header is hidden, the lateral menu can't be accessed from the views. To access it again, press the 'dev' button located at the bottom of the screen.

Enjoy your new, customized mobile dashboard for Home Assistant!


