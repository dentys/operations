## Document-services-operations
This repository provides solution to deploy [document micro services](https://github.com/dentys/training) 
onto Kubernetes Cluster.


### Prerequisites 
* Install local Kubernetes playground either [minikube](https://github.com/kubernetes/minikube) or enable Kubernetes in 
[Docker Desktop](https://blog.docker.com/2018/07/kubernetes-is-now-available-in-docker-desktop-stable-channel/)
* Install [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)
* Install [helm package manager](https://docs.helm.sh/using_helm/#installing-helm)
* Install [Tiller](https://docs.helm.sh/using_helm/#easy-in-cluster-installation) on Kuberntes Cluster

### Build docker images
First of all [document micro services](https://github.com/dentys/training) need to be built as docker images.
Docker image build step is integrated into maven lifecycle with [dockerfile-maven-plugin](https://github.com/spotify/docker-maven-plugin).

Example to build docker image for metadata-manager micro service:
```
mvn clean package dockerfile:build -f metadata-manager/pom.xml
```
After successful build the following command should show newly created docker images:
```
docker image ls
```

Please notice that deployment example described here operates only with local distributions, 
nothing is pushed to remote docker repositories.

### Deploy on Kubernetes Cluster
The following command deploys and starts all services defined under document-services
[umbrella helm chart](https://docs.helm.sh/developing_charts/#complex-charts-with-many-dependencies).
```
helm install --name document-services document-services/
```
After a while services should be up and running.

To verify state of pods:
```
kubectl get pods
```

To verify state of services:
```
kubectl get services
```
