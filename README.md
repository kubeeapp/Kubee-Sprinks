# Kubee Sprinks

## kubee-sprinks

Opensprinkler custom component for Home Assistant

Last tested on OS API `2.1.8` and Home Assistant `0.95.0`

![image](https://user-images.githubusercontent.com/819711/36068687-086820ce-0f2f-11e8-81de-de53c94124f0.png)

### Features

- Binary sensors for each station to show on/off status
- Binary sensors for OpenSprinkler operation, rain sensor and rain delay
- Sensors for each station to show status
- Sensors for water level, last run time and rain delay stop time
- Programs as scenes which can be "activated"
- Stations as switches with individual timers

### Installation

1. Copy `custom_components/kubee_sprinks` folder into `<config_dir>/custom_components`
2. Add the following into your `configuration.yaml`
    ```yaml
    kubee_sprinks:
      host: <host>
      password: <md5-password>
    ```
    - Replace `<host>` with the IP address or hostname of your Opensprinkler controller.
    - Replace `<password>` with the MD5 encrypted version of your password to your Opensprinkler interface.

3. Restart Home Assistant

### Configuration

- `stations` - by default the component will retrieve all stations but you can limit which stations to show by providing a list of station indexes (starting from 0)
    ```yaml
    kubee_sprinks:
      ...
      stations:
        - 0
        - 3
        - 4
    ```

- `programs` - by default the component will retrieve all programs but you can limit which programs to show by providing a list of program indexes (starting from 0)
    ```yaml
    kubee_sprinks:
      ...
      programs:
        - 0
        - 3
    ```

## Support for HACS

This custom component can be tracked with the help of [HACS](https://github.com/custom-components/hacs).

## Troubleshooting

#### My sprinkler switches are not working

Some users have reported that thier switches do not work. This is due to some `input_number` entities not being created by the component. To get around this issue you can manually create these entities by adding the following for each of your stations.

```yaml
input_number:
  <station_name>_timer:
    min: 1
    max: 30
    step: 1
    mode: slider
```

Replace `<station_name` with your station name, it should match the names created for the `sensor`, `switch` and `binary_sensor`.
