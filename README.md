# Home Assistant Matchday Calendar

A lightweight Home Assistant package that adds upcoming matches for selected teams to a calendar.

It is designed to be easy to configure and reuse with different teams, sports, calendars, and schedules.

## Features

- Supports football (soccer), basketball, volleyball, handball, tennis
- Track any team using its Sportradar competitor ID
- Creates calendar events automatically
- Prevents duplicate events
- Configurable calendar entity
- Configurable number of days ahead
- Configurable event duration per sport
- Automatic daily sync
- No HACS or custom integration required

## Installation

1. Enable packages in `configuration.yaml`:

```yaml
homeassistant:
  packages: !include_dir_named packages
```

2. Create:

```text
/config/packages/
```

3. Copy `matchcenter_calendar.yaml` to:

```text
/config/packages/matchcenter_calendar.yaml
```

4. Add your API key to `secrets.yaml`:

  ```yaml
matchcenter_api_key: "YOUR_API_KEY"
```

  An API key can be retrieved inspecting a request [here](https://www.sport24.gr/matchcenter/).

5. Restart Home Assistant.

## Configuration

Edit the configuration section near the top of `matchcenter_calendar.yaml`.

Example:

```yaml
calendar_entity_id: calendar.matchday
days_ahead: 7

sports:

  - sport: soccer
    emoji: "⚽"
    duration_minutes: 120

    teams:
      - name: Panathinaikos FC
        competitor_id: "sr:competitor:3248"

      - name: Greece Men's National Football Team
        competitor_id: "sr:competitor:4710"


  - sport: basketball
    emoji: "🏀"
    duration_minutes: 150

    teams:
      - name: Panathinaikos BC
        competitor_id: "sr:competitor:3508"

      - name: Greece Men's National Basketball Team
        competitor_id: "sr:competitor:6128"
```

Change the calendar entity, import window, teams, IDs, emojis, and event durations as needed.

## Syncronization
### Automatic

The included automation runs once per day.

Default:

```yaml
- trigger: time
  at: "06:00:00"
```

Change the time directly in the automation section if needed.

### Manual

Run manually from:

**Developer Tools → Actions**

```yaml
action: script.matchcenter_sync_calendar
```


