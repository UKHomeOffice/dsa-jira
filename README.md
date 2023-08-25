# dsa-jira
This repo houses the Docker Build image for DSA Jira. Any changes made to the Dockerfile are automatically pushed to ECR via a Drone pipeline. The current version of Jira is 8.13.25

## Upgrading Jira
A common use case for this repo is upgrading Jira. This can be achieved by simply amending the Jira version and tag in the .drone.yml file.
```yaml
steps:
- name: build_push_to_ecr
  image: plugins/ecr
  settings:
    access_key:
      from_secret: AWS_ACCESS_KEY_ID
    secret_key:
      from_secret: AWS_SECRET_ACCESS_KEY
    repo: dsa/jira
    registry: 340268328991.dkr.ecr.eu-west-2.amazonaws.com
    region: eu-west-2
    create_repository: false
    build_args:
    - APP_BUILD=${DRONE_COMMIT_SHA}
    - JIRA_VERSION=8.20.25  # <------------------Jira Version Here
    - DOCKER_HOST=tcp://172.17.0.1:2375
    tags:
    - 8.20.25  # <-------------------------------Jira Version Here
    - ${DRONE_COMMIT_SHA}
```
 
 
