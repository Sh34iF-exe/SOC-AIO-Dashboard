# Incident / Case count by Severity (Last 24 hours)

## Critical Severity

```bash
dataset = incidents  
| fields severity, creation_time  
| filter severity = ENUM.CRITICAL   
| filter timestamp_diff(current_time(), creation_time, "SECOND") <= 86400
| comp count() as Total by severity
| view graph type = single subtype = standard xaxis = severity yaxis = Total scale_threshold("#900808") 
```

## High Severity

```bash
dataset = incidents  
| fields severity, creation_time  
| filter severity = ENUM.HIGH    
| filter timestamp_diff(current_time(), creation_time, "SECOND") <= 86400
| comp count() as Total by severity
| view graph type = single subtype = standard xaxis = severity yaxis = Total scale_threshold("#ff2323") headerfontsize = 70 
```

## Medium Severity

```bash
dataset = incidents  
| fields severity, creation_time  
| filter severity = ENUM.MEDIUM     
| filter timestamp_diff(current_time(), creation_time, "SECOND") <= 86400 
| comp count() as Total by severity
| view graph type = single subtype = standard xaxis = severity yaxis = Total scale_threshold("#e6a30f") headerfontsize = 70 
```

## Low Severity

```bash
dataset = incidents  
| fields severity, creation_time  
| filter severity = ENUM.LOW     
| filter timestamp_diff(current_time(), creation_time, "SECOND") <= 86400
| comp count() as Total by severity
| view graph type = single subtype = standard xaxis = severity yaxis = Total scale_threshold("#0e9ce6") headerfontsize = 70 
```