[![hacs_badge](https://img.shields.io/badge/HACS-Default-orange.svg)](https://github.com/hacs/integration)

[![Support the author on Patreon][patreon-shield]][patreon]

[![Buy me a coffee][buymeacoffee-shield]][buymeacoffee]

[patreon-shield]: https://frenck.dev/wp-content/uploads/2019/12/patreon.png
[patreon]: https://www.patreon.com/dutchdatadude

[buymeacoffee]: https://www.buymeacoffee.com/dutchdatadude
[buymeacoffee-shield]: https://www.buymeacoffee.com/assets/img/custom_images/orange_img.png

# HADailySensor
![](logo.png?raw=true)

Daily Sensor is a Home Assistant custom component that accumulates readings from a chosen sensor throughout the day and resets at midnight.
You can select how values are aggregated: minimum, maximum, sum, average (mean), median, standard deviation, or variation. It's a simple way to produce clear daily summaries from any numeric sensor.

## ⚠️ Critical Fix Available (v2026.2.6)

**If you're experiencing a 500 error when editing Daily Sensor configuration**, this fork contains critical bug fixes that are pending merge to the upstream repository.

### Issue
The upstream HACS version has a breaking bug that causes a `500 Internal Server Error` when attempting to edit existing Daily Sensor configurations via the UI.

### Solution
Until [PR #105](https://github.com/jeroenterheerdt/HADailySensor/pull/105) is merged, install this maintained fork:

**Via HACS (Custom Repository):**
1. HACS → Integrations → ⋮ (top right) → Custom repositories
2. Add repository: `https://github.com/elyobelyob/HADailySensor`
3. Category: Integration
4. Click "Add"
5. Search for "Daily Sensor" and install **v2026.2.6 or later**
6. Restart Home Assistant

**What's Fixed:**
- ✅ 500 error when editing sensor configuration
- ✅ AttributeError on config_entry property
- ✅ ValueError when source sensor is unavailable
- ✅ Options flow type handling improvements
- ✅ Code quality and formatting improvements

---

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
