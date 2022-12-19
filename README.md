# December_Devops_workshop
========================================
## CI/CD Pipelines for container based application: 
-----------------------------------------
Architecture link : `https://docs.saleor.io/docs/3.x/overview/architecture`
git link gist:https://gist.github.com/shaikkhajaibrahim/8480b42a0a08be6697e525e88ce0fde8

## manual setup:
----------------
* Manually setup: https://docs.saleor.io/docs/3.x/setup/docker-compose follow the steps given in the link. make sure the machine you created have minimum 30 gb volume.
* refer here for the setup page `https://docs.saleor.io/docs/3.x/category/setup`
```jekinsfile
pipeline {
    agent any
    triggers {
        pollSCM('* * * * *')
    }
    stages {
        stage('vcs') {
            steps {
                git branch: 'main', url: 'https://github.com/WorkshopsByKhaja/saleor-dashboard.git'
            }
        }
        stage('docker image build') {
            steps {
                sh 'docker image build -t shaikkhajaibrahim/saleor-dashboar:DEV .'
            }
        }
        stage('push image to registry') {
            steps {
                sh 'docker image push shaikkhajaibrahim/saleor-dashboar:DEV'
            }
        }
    }
}
```
azure-devops
--------
---yaml
---
# where to run the ci/cd pipeline
pool:
  vmImage: ubuntu-22.04

# when to run
trigger:
  - main

# what has to be done
steps:
  - task: Docker@2
    inputs:
      command: buildAndPush
      Dockerfile: "./Dockerfile"
      tags: "shaikkhajaibrahim/saleordashboard:AZDEV"
      containerRegistry: DockerHub

## Activity4:
-------------
* Create a saleor-core : `
Saleor core: https://github.com/WorkshopsByKhaja/saleor`
---yaml
---
---
# where to run the ci/cd pipeline
pool:
  vmImage: ubuntu-22.04

# when to run
trigger:
  - main

# what has to be done
steps:
  - task: Docker@2
    inputs:
      command: buildAndPush
      Dockerfile: "./Dockerfile"
      tags: "shaikkhajaibrahim/saleorcore:AZDEV"
      containerRegistry: DockerHub
---

## Activity 5:
* create a image on saleor storefront
