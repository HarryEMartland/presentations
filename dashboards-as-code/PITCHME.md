# Dashboards as Code

@snap[south-east]
Harry Martland  
Senior Software Engineer  
**@color[darkblue](Booking)@color[deepskyblue](Go)**
@snapend

---?image=images/pounds-stacked.jpg&size=cover

## Why?

Note:
- Testing: Dashboards can go through the same testing procedure without breaking production
- Code Review: Dashboards can be reviewed like code to spot mistakes
- Automation: Not time is wasted copying dashboards to different instances
- Backup: If Grafana needs to be rebuild you can easily recreate dashboards
- Version Control: If something breaks you can easily revert it.
- Reusable: other teams can fork and change a dashboard to make it their own

---?image=images/grafana-json.png

## @color[white](Grafana)

---?color=black

![Wizzy Logo](images/wizzy-logo.png)

[github.com/utkarshcmu/wizzy](github.com/utkarshcmu/wizzy)

Note:
- Wizzy is a command line tool to manage Grafana 'entities'
- Entities are things like dashboards, datasources
- Download through npm


---

## Provisioning Grafana

```yaml
apiVersion: 1

providers:
- name: 'default'
  orgId: 1
  folder: ''
  type: file
  disableDeletion: false
  updateIntervalSeconds: 3 #how often Grafana will scan for changed dashboards
  options:
    path: /var/lib/grafana/dashboards
```
[http://docs.grafana.org/administration/provisioning/](http://docs.grafana.org/administration/provisioning/)

Note:
- Grafana can auto load dashboards from folder
- **Below are my opinions**
- Dashboards need to be stored/available in folder
- Not scalable to store dashboards with Grafana deployment
- May rely on permissions to deployment repo
- Takes ownership away from team

## Configure Wizzy

```bash
wizzy init #creates an empty config file
wizzy set grafana url http://grafana.service/
wizzy set grafana username grafanaAdmin
wizzy set grafana password superSecret
wizzy set context grafana dev

```

Note:
- First need to init which creates a config file more on that next
- Has the notion of contexts or environments for config

---

### Storing Configuration

```json
{
  "config": {
    "grafana": {
      "envs": {
        "dev": {
          "url": "https://cluster-grafana.europe-west2.dev.bookinggo.cloud",
          "username": "admin", "password": "unsecure"
        }, ...
      }
    },
    "context": {
      "grafana": "dev" //the current selected env/context
    }
  }
}
```

Note:
 - Setting config saves in config file which can be committed in or stored on CI server as a secret
 - the context is stored here but can be set on CI using the context command

---

### Useful Commands
```bash
wizzy import dashboard <dashboard name>
wizzy export dashboard <dashboard name>
```

Note:
 - import is useful to create dashboards in the dev env then import them locally and storing in vcs
 - export is used to upload to Grafana in the CI pipeline
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

Note:
 - show the export command
 - show the setting of url
 - you could use contexts to store the config and set the context here
 - CI server could store config file with secrets in
 - installing npm to download wizzy
 - can use a GoCD alias to deploy to different env's