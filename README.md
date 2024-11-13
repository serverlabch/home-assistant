# Home Assistant - tips
## IP Ban
```yaml
http:
  use_x_forwarded_for: true
  trusted_proxies:
    - 10.0.0.2
    - 2000:abcd:1234:1234::2
  ip_ban_enabled: true
  login_attempts_threshold: 3
  cors_allowed_origins:
    - https://google.com
    - https://www.home-assistant.io
```
## Recorder for long-term data history
More information: https://www.home-assistant.io/integrations/recorder/#custom-database-engines
```yaml
recorder:
  purge_keep_days: 60
  db_url: mysql://username:password@ipaddress/databasename?charset=utf8mb4
  exclude: # Enter entities to exclude from recording in the database
    entity_globs: # Wildcard (*) possible here, enter entity classes to exclude
        - scene.*
        - sensor.sun*
        - weather.*
        - switch.*
    entities: # Enter single entities here
        - sun.sun # Don't record sun data
    domains: # Enter domains here
      - automation
      - update
    event_types: # Enter events here, like service calls
      - call_service # Don't record actions
```
### Links
- [Home Assistant - HTTP](https://www.home-assistant.io/integrations/http/)
