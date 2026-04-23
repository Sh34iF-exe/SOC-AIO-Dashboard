# KPI Metrics - Pane

This Pane contains a series of widgets such as average incident count, TP count, MTTD & MTTR values.

## Average Incident

```bash
dataset = incidents
| filter timestamp_diff(current_time(), creation_time, "DAY") <= 7
| bin creation_time span = 1d
| comp count() as Alert_count by creation_time | comp avg(Alert_count) as Average |alter avg_int = to_integer(Average)
| view graph type = single subtype = standard yaxis = avg_int 
```

## TP count

```bash
dataset = incidents
| filter timestamp_diff(current_time(), creation_time, "DAY") <= 1
| filter status = ENUM.RESOLVED_TRUE_POSITIVE | comp count() as TP
| view graph type = single subtype = standard xaxis = TP yaxis = TP scale_threshold("#dd3a32") default_limit = `false` 
```

## Mean Time to Detect (MTTD)

```bash
dataset = incidents 
| filter timestamp_diff(current_time(), creation_time, "DAY") <= 1 
| filter first_assignment_ts != null 
| alter 
    creation_epoch    = to_epoch(creation_time, "millis"), 
    assignment_epoch  = to_epoch(first_assignment_ts, "millis") 
| alter 
    mttd_minutes = divide( 
        subtract(assignment_epoch, creation_epoch), 60000 
    ) 
| fields 
    incident_id, 
    creation_time, 
    first_assignment_ts, 
    mttd_minutes 
| comp avg(mttd_minutes) as mttd
| alter 
    mttd_hours = divide(mttd, 60)
| view graph type = single subtype = standard is_time = `true` yaxis = mttd_hours default_limit = `false` time_units = h 
```