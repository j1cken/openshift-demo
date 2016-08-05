# TODOs for running on a different OSE instance
* change registry IP
* change wildcard domain
* change token in Jenkins jobs

# create project ab
```
oc new-project ab
```

# create Template

## using WebUI
### create template
```
oc create -f template.json
```
### add template to project
### create deployments

## using CLI in one go
```
oc new-app -f template.json
```

# tag for production deployment
```
oc tag v1:latest v1:1.0
oc tag v1:1.0 production:v1
oc tag production:v1 production:latest
```

# simulate crash
```
docker kill <container-id>
```

# clone v2 repo
```
git clone https://github.com/j1cken/nodejs-ex
git co v2
```

# curl loop to v2
```
for i in {1..10000};do curl v2-ab.rhcloud.example.com; sleep 0.5;done
```

# rsync changes into running container

## show terminal access in WebUI to find rsync directory

## show from CLI
```
oc get pods
oc rsh v2-1-4bnic
oc rsync --exclude='.git' . v2-1-4bnic:/opt/app-root/src
```

# add Jenkins using Web UI

## create release build job
```
curl -k -u admin:password -XPOST -d @jenkins-jobs/rel-v2.xml 'https://jenkins-ab.rhcloud.example.com/createItem?name=rel-v2' -H "Content-Type: application/xml"
```

## trigger build for v2:2.0 thru Jenkins Web UI

# Deploy Acceptance

## Create DC for Acceptance
```
oc create -f acceptance.template.json
```

## Tag Release Build Image for Acceptance

### create jenkins job
```
curl -k -u admin:password -XPOST -d @jenkins-jobs/deploy-acc.xml 'https://jenkins-ab.rhcloud.example.com/createItem?name=deploy-acc' -H "Content-Type: application/xml"
```

### trigger build of deploy-acc job

### show reference of tagged image: acc --> v2-1.0

## Watch deploy to Acceptance

# Promote to Production
```
curl -k -u admin:password -XPOST -d @jenkins-jobs/promote-prod.xml 'https://jenkins-ab.rhcloud.example.com/createItem?name=promote-prod' -H "Content-Type: application/xml"
```

## Rolling Update
run promote-prod job

## Rollback
```
curl -k -u admin:password -XPOST -d @jenkins-jobs/rollback-prod.xml 'https://jenkins-ab.rhcloud.example.com/createItem?name=rollback-prod' -H "Content-Type: application/xml"
```
