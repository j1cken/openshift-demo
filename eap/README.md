# JBoss Enterprise Application Platform Example
## Prerequisites
+ Namespace called 'ci'
  + deployed application called ['nexus'](https://github.com/j1cken/nexus-ose/)
  + deployed OSCP instant application called ['jenkins'](../jenkins/)
    + Plugins needed
      + [OpenShift Pipeline Jenkins Plugin](https://wiki.jenkins-ci.org/display/JENKINS/OpenShift+Pipeline+Plugin)
        + needs to be uploaded manually
        + version >=1.0.22 tested to be working
      + [Build Flow plugin](https://wiki.jenkins-ci.org/display/JENKINS/Build+Flow+Plugin)
      + [Pipeline](https://wiki.jenkins-ci.org/display/JENKINS/Pipeline+Plugin)
      + [Pipeline: Basic Steps](https://wiki.jenkins-ci.org/display/JENKINS/Pipeline+Basic+Steps+Plugin)
      + [Pipeline: Nodes and Processes](https://wiki.jenkins-ci.org/display/JENKINS/Pipeline+Nodes+and+Processes+Plugin)
      + [Build Flow Extensions](https://wiki.jenkins-ci.org/display/JENKINS/Build+Flow+Extensions+Plugin)

## How to run the demo
```shell
oc login https://<your_oscp_instance>:8443
bash demo
```
If u want to debug the demo script just use `bash -x demo`.

## Outcome

The demo script will create the following projects:
* eap-integration
* eap-uat
* eap-production

Namespace 'eap-integration' will host two applications based on different source code branches:
* master
* v2

Namespace 'ci' will be used to promote images through the above stages. Jenkins jobs will be created automatically during the script. Please obey the pre-reqs.

## Topics covered
+ incremental builds
+ use OSCP internal Nexus artifact repository for faster builds
+ promotion of images through different stages
+ building a CI/CD pipeline with Jenkins
+ rolling updates
+ canary deployments
+ blue/green deployments
+ quotas and limits
+ readiness- and livenessProbe
+ autoscaling
