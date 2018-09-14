# Dashboards as Code

@snap[south-east]
Harry Martland  
Senior Software Engineer  
**@color[darkblue](Booking)@color[deepskyblue](Go)**
@snapend

---?image=images/pounds-stacked.jpg&size=cover

## Why?

---?image=images/grafana-json.png

## @color[white](Grafana)

---

## Wizzy

[github.com/utkarshcmu/wizzy](github.com/utkarshcmu/wizzy)

![Wizzy Logo](../images/wizzy-logo.png)

![Grafana Logo](../images/grafana-logo.jpg)

---

## Configure Wizzy

```bash
wizzy init #creates an empty config file
wizzy set grafana url http://grafana.service/
wizzy set grafana username grafanaAdmin
wizzy set grafana password superSecret
```

---

### Storing Configuration

```json
{
  "config": {
    "grafana": {
      "envs": {
        "dev": {
          "url": "https://cluster-grafana.europe-west2.dev.bookinggo.cloud",
          "username": "admin",
          "password": "unsecure"
        },
        ...
      }
    },
    "context": {
      "grafana": "dev" //the current selected env/context
    }
  }
}
```

---

### Useful Commands
```bash
wizzy import dashboard <dashboard name> #download the dashboards locally
wizzy export dashboard <dashboard name> #uplodad the local dashboard
```
---

## Pipeline
```yaml
cloud_deploy:
  elastic_profile_id: 'jdk_docker_npm'
  environment_variables:
    NPM_CONFIG_REGISTRY: 'https://artifactory.server.traveljigsaw.com/artifactory/api/npm/npm/'
  tasks:
    - exec:
        command: '/bin/bash'
        arguments:
        - '-c'
        - 'npm install'
        working_directory: 'grafana-service-dashboard'
    - exec:
        command: '/bin/bash'
        arguments:
          - '-c'
          - 'npm run wizzy set grafana url https://cluster-grafana.${BG_CLOUD_DC}.${BG_CLOUD_ENVIRONMENT}.bookinggo.cloud'
        working_directory: 'grafana-service-dashboard'
    - exec:
        command: '/bin/bash'
        arguments:
        - '-c'
        - 'npm run wizzy export dashboard services'
        working_directory: 'grafana-service-dashboard'
```