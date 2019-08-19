# Dynatrace Ansible Collection

This Ansible collection comprises several resources that allow you to send comments and deployment information directly from your Ansible playbooks to your Dynatrace tenant.

Capabilities:

- Comment on a Dynatrace problem ticket
- Send deployment information to Dynatrace


## Getting started:

### Send deployment information to Dynatrace

If Ansible is taking care of deploying your artifacts, the Dynatrace provided role can be used to inform your Dynatrace tenant about this deployment to provide more context information in your Dynatrace tenant.
To help you get started, please take a look at the following example:

Example:

```yaml
---
- hosts: localhost
collections:
    - dynatrace_innovationlab.dynatrace_collection
vars:
    tenant_url: 'https://xxx.dynatrace.com'
    api_token:  'your-api-token'

tasks:
- include_role:
    name: dynatrace_custom_deployment
    vars:
    attach_rules:
        tagRule:
        -
            meTypes: ['SERVICE']
            tags: 
            -
            context: 'CONTEXTLESS'
            key: 'service'
            value: 'my-microservice'
    deploymentVersion: '1.2.3'
    deploymentName: 'production-deployment'
    deploymentProject: 'My Webshop'
    source: 'Ansible'
```

The result might look similar as can be seen in the right bottom corner of the screenshot:

<!-- please note this has to be a absolute URL since otherwise it will not show up on galaxy.ansible.com -->
![custom deployment|](https://raw.githubusercontent.com/dynatrace-innovationlab/ansible-collection/master/collection/assets/custom-deployment.png)

### Comment on a Dynatrace problem ticket

If Ansible is taking care of taking counter actions to any problem Dynatrace detects or just forwards information, it is simple to add comments to a Dynatrace problem ticket with this role.


```yaml
---
- hosts: localhost
  collections:
    - dynatrace_innovationlab.dynatrace_collection
  vars:
    tenant_url: 'https://xxx.dynatrace.com'
    api_token:  'your-api-token'

  tasks:
  - include_role:
      name: dynatrace_problem_comment
    vars:
      problem_id: '14959299420367201_1563984V2'
      comment: 'Hello from Ansible'
      user: 'myname@email.com'
      context: 'Ansible'
```

The result might will look similar to the screenshot:

<!-- please note this has to be a absolute URL since otherwise it will not show up on galaxy.ansible.com -->
![problem comment](https://raw.githubusercontent.com/dynatrace-innovationlab/ansible-collection/master/collection/assets/comment.png)