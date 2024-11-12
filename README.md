# Home Assistant - tipps
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
### Links
- [Home Assistant - HTTP](https://www.home-assistant.io/integrations/http/)
