# Ansible Role: Dynatrace Deployment

This role sends custom deployment information to Dynatrace.

## Download

The role is available via:

- Ansible Galaxy
- GitHub

## Configuration

Please find below a list of variables that have to be configured:

| Name              | Default            | Description
|-------------------|--------------------|------------
| tenant_url        |                    | URL of your Dynatrace tenant
| api_token         |                    | API Token from your Dynatrace tenant
| deploymentVersion | 0.1.0              | version of the artifact to be deployed
| deploymentName    | Default Deployment | name of this deployment
| deploymentProject | Default Project    | project this deployment belongs to
| source            | Ansible            | source of this deployment
| attach_rules      |                    | rules that describe to which entities this deployment event is attached to
| remediationAction |                    | action that can be called in case of problems with this deployment
| customProperties  |                    | custom properties for this deployment


## Usage (Example):

```yaml
---
- hosts: localhost
  vars:
    tenant_url: 'https://XXXXXX.live.dynatrace.com'
    api_token: 'XXXXX'


  tasks:
  - include_role:
      name: dynatrace_deployment_event
    vars:
      deploymentVersion: '1.1'
      attach_rules:
        tagRule:
          meTypes: 'SERVICE'
          tags: 'ansible-deployment'

  - include_role:
      name: dynatrace_deployment_event
    vars:
      deploymentVersion: '1.2'
      attach_rules:
        entity_ids: 'SERVICE-ID'

  - include_role:
      name: dynatrace_deployment_event
    vars:
      deploymentVersion: '1.3'
      attach_rules:
        tagRule:
            -
              meTypes: ['SERVICE']
              tags:
              -
                context: 'CONTEXTLESS'
                key: 'Deployment'
                value: '10.1.0.5:80'
      customProperties:
          'CI Tool': 'Ansible'
          'Build Number': '12321'
          'Git Commit': '23422323233332'

```
