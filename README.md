# Home Assistant - Quick Look Mobile

Welcome to the Quick Look Mobile Dashboard for Home Assistant! 

This dashboard provides a clear and minimalistic mobile interface for your home devices. It is designed to provide you with answers to critical questions at a glance such as "Is there someone in my house?", "Is there an open door or window?", "Did I forget to turn off a light?", and more. Here are the steps to install and configure it:

## Demo :
<p align="center">
  <a href="https://www.youtube.com/watch?v=hZRSu72m1gw">
    <img src="https://img.youtube.com/vi/hZRSu72m1gw/0.jpg" alt="Step-by-Step Video">
  </a>
</p>


## Prerequisites

Before beginning, make sure you have:

- Familiarity with YAML and Home Assistant configuration files
- HACS with following integrations:
  - [Button Card](https://github.com/custom-cards/button-card) by ROM Rider
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

### 3. Add This to Your `configuration.yaml` File

```yaml
frontend:
  themes: !include_dir_merge_named themes/

lovelace:
  mode: storage
  dashboards: !include dashboards/dashboards.yaml
  
sensor: !include_dir_list entities/sensors/
```

You might need to modify these lines to match your current setup, particularly if your configuration is split across multiple files.

### 4. Reboot and Apply Theme

- Restart your Home Assistant for the changes to take effect.
- Once rebooted, apply the 'Quick Look Mobile' theme and select 'light mode'.
- On the left lateral menu, open the newly created dashboard. Since this dashboard is designed for mobile view, it might appear too large on a computer screen. To correct this, press F12 or open your browser's developer tools and select the 'mobile view' option.

### 5. Dashboard Structure

#### 5.1 Views

- Navigate to your `/config/dashboard/quick_look_mobile/views` folder.
- Each file in this `views` folder corresponds to a different view on your dashboard. For instance, `1.1_home.yaml` corresponds to your home view, `2.1_security_access.yaml` corresponds to your security access view, and so forth.
- Each view has sections for the header, subheader, main title, main and footer spaces.

#### 5.2 Header

- The header contains five main categories: `security`, `air`, `light`, `media`, and `devices`. Each of these categories leads to a different view.
- If none is selected, `home` view is selected. You can also navigate back to it by clicking on an active view.
- Each of these categories further has two subcategories. `Security` includes `access` and `video`, `air` includes `heating` and `cooling`, `light` includes `bulbs` and `covers`, `media` includes `music` and `TV`, and `devices` includes `rooms` and `favorites`.
- Additionally, there is a special `family` category which can be accessed through the upper left person icon.
- The header is designed for two main purposes: 
  1) allow for rapid navigation through these views 
  2) provide useful status information by changing its color and icon based on 'template sensors' (see 6. Customize Template Sensors) e.g. if a lightbulb is turned on, the light category will turn yellow. If no entities are active, it will revert to its default grey color. This feature provides a quick and easy way to identify the status of your various devices and systems. 

### 6. Add Your Entities

- Open the file corresponding to the view you want add entities to. eg open the `3.1_air_heating.yaml` file to add your climate and temperature sensors
- To avoid disrupting the setup, only modify the lines where it is explicitly mentioned ```#can be changed, #required or #optional``` at the end. These lines have been marked for easy and safe modification.
- Navigate to the "main" section in the view file. By default, you have space for 16 entities but you can add as many as you need or delete unnecessary blocks.
- Each entity block requires certain variables to be defined. For a climate entity, you'll define `entity` and `name`. `Entity` is the entity_id of your device (e.g., `climate.kitchen`), and `name` is optional; it's the name that will be displayed on the dashboard. If no name is given, the friendly name of the entity will be used.
- Refresh your dashboard to see the changes by clicking the three dots in the upper-right corner of the Home Assistant interface.
- Repeat the above steps to all your views.

### 7. Customize Template Sensors

- Each sensor contains a list of entities that are intended to trigger the header for color change if at least one is active.
- To modify or add entities to a template sensor, open the corresponding file and adjust the entity list.
- Template sensors are located at `/config/entities/sensors/quick_look_mobile`.
- Entities should match those you chose for the corresponding view e.g `some_lights_are_on.yaml` template sensor should match the entities you selected first in '`4.1_light_bulbs.yaml` view
- Dont't put a comma after the last entity
- After modification, remember to restart your Home Assistant for the changes to take effect.

### 8. Hide the Native Header (Optional)

- To improve the aesthetics of the dashboard, you may want to hide the native upper horizontal header.
- Open the browser mod integration settings.
- Select 'Hide Header'.
- Choose the mobile device on which you wish to hide the header. The dashboard will look cleaner on mobile without it.

## Known Issues and Fixes

- If the native header is hidden, the lateral menu can't be accessed from the views. To access it again, press the 'dev' button located at the bottom of the screen.
- Currently, the 'assist' icon located at the upper right of the dashboard isn't functional as the way to trigger this popup keeps unclear for me.

Enjoy your new, customized mobile dashboard for Home Assistant!


