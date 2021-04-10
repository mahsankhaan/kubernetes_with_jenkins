# Kubernetes_with_Jenkins

Jenkins:
Jenkins is an open source automation server which can be used to automate all sorts of tasks related to building, testing, and delivering or deploying software.

Kubernetes: 
Kubernetes is a portable, extensible, open-source platform for managing containerized workloads and services, that facilitates both declarative configuration and automation

In this tutorial, we will learn about CI&CD using Jenkins on IBM Kubernetes service. We will use [Helm](https://helm.sh/) a package manager for Kubernetes to configure Jenkins.


## Prerequisites
You need the following tools to complete the steps in this tutorial:
* [IBM Cloud](https://cloud.ibm.com/registration) account.
* Access to the [IBM Cloud Kubernetes Service](https://cloud.ibm.com/kubernetes/catalog/create) to create a Kubernetes cluster. If needed, you can create [one free cluster](https://cloud.ibm.com/docs/containers?topic=containers-cs_ov#cluster_types) for 30 days to get familiar with Kubernetes capabilities.
* A [GitHub](https://github.com/) account and some knowledge of [Git commands](https://training.github.com/).


## Steps

1. [Access IBM Kubernetes service](#step-1-Access-IBM-Kubernetes-service)
1. [Access IBM Kubernetes service](#step-2-Access-IBM-kubernetes-service)
1. [Install Jenkins with YAML files](#step-3-create-a-persistent-volume)
1. [Access Jenkins dashboard & login]()


 

### Step 1. Access IBM Kubernetes service
```
ibmcloud login -a https://cloud.ibm.com -u passcode -p pass 
ibmcloud ks cluster config --cluster mycluster
kubectl config current-context
```

### Step 2. Create a namespace 
A distinct namespace provides an additional layer of isolation and more control over the continuous integration environment.

```
$ kubectl create namespace jenkins
$ kubectl get namespaces

```

### Step 3. Install Jenkins with YAML files
This section describes how to use a set of YAML (Yet Another Markup Language) files to install Jenkins on a Kubernetes cluster.

* Deployment file available [here](updatee)

__Note__ : Description of deployment file 

![GitHub Logo](images/s1.png)

* Run command to execute the deployment:
```
$ kubectl create -f jenkins-deployment.yaml -n jenkins

```
* To validate

```
$ kubectl get deployments -n jenkins

```

* Expose the deployment:
We have a Jenkins instance deployed but it is still not accessible,to make it accessible outside the cluster the Pod needs to be exposed as a service.

Service File available [here](update)
```
$ kubectl create -f jenkins-service.yaml -n jenkins

```

* To validate

```
$ kubectl get services -n jenkins
```

### Step 4. Access Jenkins dashboard & login

* Get worker node details, and under address note __ExternalIP__ 
```
kubectl get nodes
kubectl describe node 10.144.180.39
```

* Also note port where the jenkins service is running, note __PORT__ from details

```
kubectl get svc -n jenkins
```

* Now to open jenkin dashboard, in new web terminal use __ExternalIP:PORT__

* There is __Administrator password__ required, for that run below command and scroll the logs untill there is Please use the following password ...

* Continue the installation, leave the configuration as same. Then you will be in the dashboard. 

```
kubectl logs jenkins-585799558b-jks42  -n jenkins
```


### Step 5. Create a service account
In Kubernetes, service accounts are used to provide an identity for pods.

1. File available here jenkins-sa.yaml.
1. Run the command 
```
kubectl apply -f jenkins-sa.yaml
```

### Step 6. Configure Jenkins and containers
In order for Jenkins to be able to launch pods for running jobs, we have to configure the service account credentials.

* Nagivate to Manage Jenkins > Configure System > Cloud > Add a new cloud, then select “Kubernetes”

* Under kubernetes cloud details > Credentials select __Add__ > Jenkins

* Select Test connection output must be __Connected to Kubernetes v1.19.9+IKS__
