## Example Voting App Kubernetes

This is based on the original [example-voting-app](https://github.com/dockersamples/example-voting-app) repository from the [docker-examples](https://github.com/dockersamples) GitHub page

and modified it to work on the Kubernetes/Openshift cluster.

For Openshift serviceaccount should be created using admin account
and deployment.apps/postgres-deploy, deployment.apps/result-app-deploy, deployment.apps/voting-app-deploy should be deployed under this serviceaccount, for example:

oc login -u developer -p xxxxxxxxx
oc new-project vote
oc login -u admin -p xxxxxxxxx
oc create sa vote-sa
oc adm policy add-scc-to-user anyuid -z vote-sa
oc login -u developer -p xxxxxxxxx
oc create -f .
oc set sa deployment.apps/result-app-deploy vote-sa
oc set sa deployment.apps/voting-app-deploy vote-sa
oc set sa deployment.apps/postgres-deploy vote-sa
oc expose service/result-service
oc expose service/voting-service
oc get routes

