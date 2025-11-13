# Time left until sunset card
This script shows a box with the time to the next sunset in the format "X Stunden X Minuten".

If there is more than 3 hours left, the box is green (`alert-type=success`), if it is more than 1 hour and 30 minutes, this box becomes yellow (`alert-type=warning'`), otherwise, it becomes red (`alert-type='error'`).

## HowTo
Create a new dashboard card of type `markdown`.

Use this script as content:
```yaml
Sonnenuntergang
{% set time = (as_timestamp(state_attr('sun.sun', 'next_dusk')) - as_timestamp(now())) | int %}
  {% set minutes = ((time % 3600) / 60) | int %}
  {% set hours = ((time % 86400) / 3600) | int %}
  {% set days = (time / 86400) | int %}

  <ha-alert alert-type="{%- if hours >= 3 -%}success{%- elif hours >= 1 and minutes >= 30 -%}warning{%- else -%}error{%- endif -%}">

  {%- if time < 60 -%}
    In weniger als 1 Minute
    {%- else -%}
    {%- if days > 0 -%}
      {{ days }}d
    {%- endif -%}
    {%- if hours > 0 -%}
      {%- if days > 0 -%}
        {{ ' ' }}
      {%- endif -%}
      {{ hours }} Stunde{%- if hours == 0 or hours >= 2 -%}n{%- endif -%}
    {%- endif -%}
    {%- if minutes > 0 -%}
      {%- if days > 0 or hours > 0 -%}
        {{ ' ' }}
      {%- endif -%}
      {{ minutes }} Minute{%- if minutes == 0 or minutes >= 2 -%}n{%- endif -%}
    {%- endif -%}
  {%- endif -%}
</ha-alert>
```