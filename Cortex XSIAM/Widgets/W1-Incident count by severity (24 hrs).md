# Incident / Case count by Severity (Last 24 hours)

## Medium Severity

dataset = incidents  
| fields severity, creation_time  
| filter severity = ENUM.MEDIUM     
| filter timestamp_diff(current_time(), creation_time, "SECOND") <= 86400 
| comp count() as Total by severity
| view graph type = single subtype = standard xaxis = severity yaxis = Total scale_threshold("#e6a30f") headerfontsize = 70 