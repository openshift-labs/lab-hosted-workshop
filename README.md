LAB - Hosted Workshop
=====================

This repository provides a workshop in which you can learn how to deploy a hosted workshop for multiple users, in an OpenShift cluster setup for the workshop and where OpenShift users have been pre-created in the OpenShift cluster.

To deploy this workshop, it is recommended you first create a fresh project into which to deploy it.

```
oc new-project labs
```

In the active project you want to use, run:

```
oc new-app https://raw.githubusercontent.com/openshift-labs/workshop-dashboard/master/templates/production.json \
  --param TERMINAL_IMAGE="quay.io/openshiftlabs/lab-hosted-workshop:master" \
  --param APPLICATION_NAME=hosted-workshop
```

To get the hostname for the sample workshop, run:

```
oc get route hosted-workshop
```

Use your browser to access the workshop.

You may need to supply your login/password again for the OpenShift cluster you deployed the sample workshop to. You will only be able to access it if you are a project admin of the project it is deployed to.

When you are finished you can delete the project you created, or if you used an existing project, run:

```
oc delete all,serviceaccount,rolebinding,configmap -l app=hosted-workshop
```

Note that this will not delete anything which may have been deployed when you went through the workshop. Ensure that you go right through the workshop and execute any steps described in it for deleting any deployments it had you make.
