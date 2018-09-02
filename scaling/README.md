# Scaling

Define scaling schedules.

```yaml
scale:
  metric:
    type: cpu  # cpu or mem
    agg: avg
    period: 20000
    scale_up: 80
    scale_down: 20
  min: 1
  max: 5
  desired: 5
  cooldown: 60 # number of seconds to wait before additional scaling activities begin
```

Some services need to scale dynamically by calling a command before processing.
