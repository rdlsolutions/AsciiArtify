# Analize concept small k8s platform

## Minikube

 You start the cluster using ```minikube start```, wait a few minutes and your kubectl is ready to go. To specify a Kubernetes version you can use the ```--kubernetes-version``` flag.

### WM

```mermaid
classDiagram
      Master <|-- Pod1
      Master <|-- Pod2
      Master : Cluster
      Master : Minikube
      Master: Kubectl (..)
      class Pod1{
         %% +String beakColor
         %% +swim()
         %% +quack()
      }
      class Pod2{
         %% -int sizeInFeet
         %% -canEat()
      }
```

## Kind

Creating a cluster is very similar to minikubes approach. Executing kind ```create cluster```, playing the waiting game and afterwards you are good to go. By using ```different names (--name)``` kind allows you to create multiple instances in parallel.

One feature that I personally enjoy is the ability to load my local images directly into the cluster. This saves me a few extra steps of setting up a registry and pushing my image each and every time I want to try out my changes. With a simple ```kind load docker-image my-app:latest``` the image is available for use in my cluster.

### Nodes

```mermaid
classDiagram
      Master <|-- Worker 1
      Master <|-- Worker 2
      class Worker 1{
          Pod 1* 
          Pod 2* 
         %% +quack()
      }
      class Worker 2{
          Pod 3* 
          Pod 4* 
      }
```

## K3d

  K3d is the alternative to Kubeadm. Utility designed to easily run multi-node K3s clusters in Docker.
  The application is split into the K3d server and the agent. The former acts as a manager while the latter is responsible for handling the actual workload. I discourage you from running them on your workstation as this leads to some cluster in your local filesystem. Instead put K3d in a container (e.g. by using rancher/K3d) which also allows you to easily run several independent instances.

### WM cluster

```mermaid
classDiagram
      Master <|-- Worker 1
      Master <|-- Worker 2
      Master : Docker
      Master : Kubelet (..)
      Master : Kubeadm (..)
      Master : Kubectl (..)
      class Worker 1{
          Docker
          Kubectl
          Pod (1)* 
          Pod (2)* 
         %% +quack()
      }
      class Worker 2{
          Docker
          Kubectl
          Pod (3)* 
          Pod (4)* 
      }
```

One feature that stands out is called auto deployment. It allows you to deploy your Kubernetes manifests and Helm charts by putting them in a specific directory. K3d watches for changes and takes care of applying them without any further interaction. This is especially useful for CI pipelines and IoT devices (both target use cases of K3d). Just create/update your configuration and K3d makes sure to keep your deployments up to date.

### Table compare parameters

| Propose | minikube | kind | K3d |
|---------|----------|------|-----|
| runtime | VM | container | native |
| architectures | AMD64 | AMD64 | AMD64, ARMv7, ARM64 |
| supported container runtimes | Docker,CRI-O,containerd,gvisor | Docker | Docker, containerd |
| memory | 2GB | 8GB (Windows, MacOS) | 512 MB |
| root | no | no | yes |
| multi-cluster | yes | yes | no |
| multi-node | no | yes | yes |

### Demonstration

![alt text](demo.gif)

### Alternatives Minikube

*microk8s* - An upstream Kubernetes distribution made for operations on IoT and edge computing devices in remote locations. It is optimized for IoT and edge computing resource constraints.

*kind* (Kubernetes in Docker) - Tool for running local Kubernetes clusters using Docker containers as nodes. It is primarily designed for testing Kubernetes itself.

*k0s* - Extremely lightweight Kubernetes distribution created specifically for edge computing workloads with minimal resource usage.

*kubeadm* - Official Kubernetes tool for installing vanilla Kubernetes distributions. It is used by many Kubernetes vendors and initiatives under the hood.

*Rancher Desktop* - All-in-one Kubernetes distribution for developer desktops. It includes Rancher's user-friendly management GUI and a full Docker desktop runtime.

*Charmed Kubernetes* - Canonical's enterprise-grade Kubernetes management platform for production infrastructure.

*Oracle Container Engine for Kubernetes* - Oracle's public cloud Kubernetes offering which can be run locally using tools like Oracle VM VirtualBox.

*Red Hat CodeReady Containers* - OpenShift-based Kubernetes distribution with features like easy cluster provisioning, simple network configurations, persistent volumes, integrated container registry and more.

*Docker Desktop* - Popular option for running Kubernetes locally. The version included is typically a bit behind the latest but has native Docker engine integration.
