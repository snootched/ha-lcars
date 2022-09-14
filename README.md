# Home Assistant LCARS
LCARS theme for Home Assistant

Color codes and font choice from https://www.thelcars.com
    --thanks Jim Robertus!
    


## Installation instructions
### Prerequisites
#### I. Enable themes and install card-mod

1. Install `card-mod` per the instructions on its [GitHub page](https://github.com/thomasloven/lovelace-card-mod "card-mod").

2. Make sure in your **configuration.yaml** file you have the following:
```yaml
frontend:
  javascript_version: latest
  themes: !include_dir_merge_named themes
  extra_module_url:
    - /local/community/card-mod.js #or wherever you ended up putting card-mod.js
```
3. Under the Home Assistant **Config** folder, create a new folder named **themes**, and another folder under that called **LCARS**, then place this .yaml file therein. 
4. **Restart** Home assistant to apply the changes.

#### II. Add the font
This theme requires you to add the `Antonio` font as a resource to your lovelace configuration:
```yaml
resources:
  - url: https://fonts.googleapis.com/css2?family=Antonio:wght@400;700&display=swap
  type: css
```
##### -OR-
Navigate to `Settings` → `Dashboards` → `3-dot menu` → `Resources` and add a new Resource with the above URL and selected as a stylesheet.

#### III. Set up the clock
In order for the clock to work, you need to set up the Time & Date integration by adding the following to your configuration.yaml:
```yaml
sensor:
  - platform: time_date
    display_options:
      - 'time'
      - 'date'
      - 'date_time'
      - 'date_time_utc'
      - 'date_time_iso'
      - 'time_date'
      - 'time_utc'
      - 'beat'
```

More info:
https://www.home-assistant.io/integrations/time_date/

### Enable theme
#### Option 1: Via profile
1. Open your Home Assistant **Profile**
2. Under, **Themes**, select the new LCARS theme

#### Option 2: Setting the default `backend-selected` theme
In order to have this theme set automatically as the backend selected default, add the following automation to your Home Assistant:
```yaml
- alias: Set Default Theme
  description: ''
  trigger:
  - event: start
    platform: homeassistant
  condition: []
  action:
  - data:
      name: LCARS
    service: frontend.set_theme
```
## Usage instructions
The theme includes 5 classes that can be added to cards like this to give them special styling:
```yaml
card-mod:
  class: header
```
Those classes are as follows
1. `header` - top blue bar meant for Markdown cards with one `H1` line that will start a section
2. `middle` -  side red bar meant for non-button sections below `header` and above `footer`
3. `footer` - bottom gray bar meant for the last card in a section
4. `button-small` - squared off buttons intended to go in middle sections
5. `button-large` - rounded button meant to be standalone outaide of `header`-`middle`-`footer` sections