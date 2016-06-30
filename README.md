1. create project ab
oc new-project ab

2. create Template

2.1 using WebUI
2.1.1 create template: oc create -f template.json
2.1.2 add template to project
2.1.3 create deployments

2.2 using CLI in one go
oc new-app -f template.json

3. tag for production deployment
oc tag v1:latest v1:1.0 \
oc tag v1:1.0 production:v1 \
oc tag production:v1 production:latest

4. clone v2 repo
git clone https://github.com/j1cken/nodejs-ex
git co v2

5. curl loop to v2
for i in {1..10000};do curl v2-ab.rhcloud.example.com;done

6. rsync changes into running container

6.1 show terminal access in WebUI to find rsync directory

6.2 show from commandline
oc get pods
oc rsh v2-1-4bnic
oc rsync --exclude='.git' . v2-1-4bnic:/opt/app-root/src

7. add Jenkins using Web UI

7.1 create release build job
curl -k -u admin:password -XPOST -d @jenkins-jobs/rel-v2.xml 'https://jenkins-ab.rhcloud.example.com/createItem?name=rel-v2' -H "Content-Type: application/xml"

7.2 trigger build for v2:2.0 thru Jenkins Web UI

8. Deploy Acceptance

8.1 Create DC for Acceptance
oc create -f acceptance.template.json

8.2 Tag Release Build Image for Acceptance

8.2.0 create jenkins job
curl -k -u admin:password -XPOST -d @jenkins-jobs/deploy-acc.xml 'https://jenkins-ab.rhcloud.example.com/createItem?name=deploy-acc' -H "Content-Type: application/xml"

8.2.1 trigger build of deploy-acc job
!!!BUG!!! Workaround: oc tag v2:1.0 acceptance:v2

8.2.1 show reference of tagged image: acc --> v2-1.0

8.3 Watch deploy to Acceptance

9. Promote to Production
curl -k -u admin:password -XPOST -d @jenkins-jobs/promote-prod.xml 'https://jenkins-ab.rhcloud.example.com/createItem?name=promote-prod' -H "Content-Type: application/xml"

9.1 Rolling Update
run promote-prod job
Workaround: oc tag v2:v2 production:v2

9.2 Rollback
curl -k -u admin:password -XPOST -d @jenkins-jobs/rollback-prod.xml 'https://jenkins-ab.rhcloud.example.com/createItem?name=rollback-prod' -H "Content-Type: application/xml"
