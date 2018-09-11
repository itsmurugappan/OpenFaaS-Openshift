# Open FaaS deployment on Openshift

This repo helps you run Open-FaaS on Openshift project without any elevated access.

### About the openshift template

   1. Templates have 2 required parameters , both of them are openshift projects,
   one is for faas control plane and another for function namespace. Please create them before installing 
   this template.
   2. If you are planning to have 2 separate projects and if your pod network is not flat. Please join 
   them as mentioned here (https://docs.openshift.com/enterprise/3.1/admin_guide/pod_network.html#joining-project-networks)

#### NATS and Queue Worker

```aidl
oc new-app -f nats-template.yaml -p CP_NAMESPACE={control plane project name} -p FN_NAMESPACE={function project name}
``` 

#### FaaS-Netesd

```aidl
oc new-app -f faasnetesd-template.yaml -p CP_NAMESPACE={control plane project name} -p FN_NAMESPACE={function project name}
``` 

#### Gateway

```aidl
oc new-app -f gateway-template.yaml -p CP_NAMESPACE={control plane project name} -p FN_NAMESPACE={function project name}
``` 

#### Prometheus and Alert Manager

```aidl
oc new-app -f prom-am-template.yaml -p CP_NAMESPACE={control plane project name}
``` 

#### FaaS Idler

```aidl
oc new-app -f idler-template.yaml -p CP_NAMESPACE={control plane project name}
``` 

By now all your components should be running. You can verify by visting gateway route url and running functions.

#### Problems I encountered and overcame

1. I created a python function through faas cli template and deployed that function in openfaas.
when i tried to hit the function i got access issue. To over come it , I edited the Dockerfile to give 
access. This file is under templates folder which gets created in your machine when you use faas-cli.

