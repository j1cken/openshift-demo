# JBoss Enterprise Application Platform Example
## Prerequisites
+ Namespace called 'ci'
  + deployed application called ['nexus'](https://github.com/j1cken/nexus-ose/)
  + deployed application called ['jenkins'](../jenkins/README.md)
    + Plugins needed
      + [OpenShift Pipeline Jenkins Plugin](https://wiki.jenkins-ci.org/display/JENKINS/OpenShift+Pipeline+Plugin)
      + [Build Flow plugin](https://wiki.jenkins-ci.org/display/JENKINS/Build+Flow+Plugin)
      + Pipeline
      + Pipeline: Basic Steps
      + Pipeline: Nodes and Processes
      + Build Flow Extensions

## How to run the demo
```shell
oc login https://<your_oscp_instance>:8443
bash -x demo
```

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
