[![hacs_badge](https://img.shields.io/badge/HACS-Default-orange.svg)](https://github.com/hacs/integration)

[![Support the author on Patreon][patreon-shield]][patreon]

[![Buy me a coffee][buymeacoffee-shield]][buymeacoffee]

[patreon-shield]: https://frenck.dev/wp-content/uploads/2019/12/patreon.png
[patreon]: https://www.patreon.com/dutchdatadude

[buymeacoffee]: https://www.buymeacoffee.com/dutchdatadude
[buymeacoffee-shield]: https://www.buymeacoffee.com/assets/img/custom_images/orange_img.png

# HADailySensor
![](logo.png?raw=true)

Daily Sensor custom component for Home Assistant. It takes aggregates an input sensor until midnight. Then it resets.
Aggregation is configurable - available options are: minimum, maximum, sum, average (mean), median, standard deviation and variation.

## Configuration
Install the custom component (preferably using HACS) and then use the Configuration --> Integrations pane to search for 'Daily Sensor'. You will need to specify the following:
- **Name** - Unique name for this daily sensor instance
- **Input Sensor** - The source sensor to aggregate data from
- **Operation** - Aggregation method: `min`, `max`, `sum`, `mean`, `median`, `stdev`, or `variance`
- **Unit of Measurement** - Display unit for the sensor value
- **Interval** - Update frequency in seconds (default: 1800)
- **Auto Reset** - Automatically reset at midnight (default: enabled)
- **Preserve on Unavailable** - Keep last value when source sensor becomes unavailable (default: disabled)
  - When enabled, the daily sensor retains its current value if the input sensor becomes unavailable (e.g., during Home Assistant restart)
  - When disabled (default), the daily sensor becomes unavailable when the input sensor is unavailable
  - Useful for maintaining accurate daily statistics across HA restarts

All sensors will be reset at 00:00 local time (unless auto-reset is disabled) and can be reset manually by calling the `daily.reset` service for each instance.

## Use case
This component is most frequently used to create a minimum and maximum daily temperature sensor based on a temperature sensor that is provided by a weather station, but can be used for many different things.
