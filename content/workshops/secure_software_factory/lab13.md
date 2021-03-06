---
title: Lab 13 - Deploy Dev
workshops: secure_software_factory
workshop_weight: 23
layout: lab
---

# Deploy Dev Stage

Enter the Deploy Dev Stage to your pipeline text file.  

<img src="../images/pipeline_deploy_dev.png" width="900" />

OpenShift deploys the application and it's deployment configuration to Dev as previously defined from the Create Dev Stage.

<br>
# Append to Jenkins Pipeline Configuration

In Builds > Pipelines > tasks-pipeline > Actions > Edit

<img src="../images/pipeline_actions_edit.png" width="900" />

Append the text below to the bottom of the Jenkins Pipeline Configuration.  Please make sure to append to the beginning of the next line.  


```
    stage('Deploy DEV') {
      steps {
        script {
          openshift.withCluster() {
            openshift.withProject(env.DEV_PROJECT) {
              openshift.selector("dc", "tasks").rollout().latest();
            }
          }
        }
      }
    }
```
