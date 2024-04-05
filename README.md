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
- Name of the daily sensor. This name needs to be unique in your Home Assistant installation.
- Name of the input sensor - this is the sensor that the daily sensor will aggregate during the day.
- The aggregation to run on the input sensor - you can choose min, max, sum, mean, median, stdev and variation.
- The interval in seconds in which to update this sensor.
- Automatic reset at midnight ? By default selected, but can be deselected to allow manual reset

That's all. You can add the component multiple times to aggregate other sensors. All sensors will be reset at 00:00 local time and can be reset manually by calling the `reset` service for each instance of the component.

## Use case
This component is most frequently used to create a minimum and maximum daily temperature sensor based on a temperature sensor that is provided by a weather station, but can be used for many different things.
