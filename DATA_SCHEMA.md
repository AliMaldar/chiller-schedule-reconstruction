# Input data

Place authorized input files under `data/` in the repository root. Files in this directory are ignored by Git.

| File | Required content |
| --- | --- |
| `data/meter_data.xlsx` (sheet `meter_data`) | `DateTime_local`; `total_load_S1` through `total_load_S7`; `chiller_load_S1` through `chiller_load_S7` (power in kW) |
| `data/weather_data.xlsx` (sheet `weather`) | `DateTime_local`, `outdoor_temperature`, and `direct_radiation` and/or `shortwave_radiation` |
| `data/season_windows.json` | Named cooling-season periods with `start`, `end`, and `clip_to_joint_availability` fields |

Timestamps must use a consistent local-time convention and support 15-minute alignment. The notebook applies its original cleaning, resampling, and weather-channel selection rules. Do not pre-fill missing chiller reference values.

A season configuration uses the following structure (replace placeholders privately):

```json
{
  "season_A": {
    "start": "YYYY-MM-DD HH:MM",
    "end": "YYYY-MM-DD HH:MM",
    "clip_to_joint_availability": false
  }
}
```

The optional `data/system_settings.json` holds system-specific `legacy_fixed_threshold_kw` and `near_zero_max_kw` parameters **only if those optional modes are enabled**. Neither the confidential parameters nor the private correspondence between source systems and S1–S7 is included.

Run from the project root, or set `TASK1_WORKDIR` to the absolute root path. Generated checkpoints, metrics, and figures remain local under `results/` and `validation_results/`.
