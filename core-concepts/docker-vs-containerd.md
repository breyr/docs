# Docker vs ContainerD

## Docker and Kubernetes

### Initial Support

Kubernetes originally supported only Docker as its container runtime.

### Evolution

As Kubernetes gained popularity, the need for broader container runtime support led to the creation of the Container Runtime Interface (CRI).

## Container Runtime Interface (CRI)

Allows Kubernetes to work with any container runtime that adheres to the Open Container Initiative (OCI) standards.

### OCI Standards

* **imagespec**: Defines how container images are structured.
* **runtimespec**: Defines how containers should run.

### Docker Compatibility

* Docker was not initially built to comply with OCI standards, making it incompatible with CRI.
* To maintain Docker support, Kubernetes introduced `dockershim`, a shim layer allowing Docker to work with CRI.

## Transition to containerd

* containerd: A CRI-compatible runtime used by Docker, ensuring OCI compliance.
* Kubernetes v1.24 Update:
  * Removal of Docker Support: Kubernetes v1.24 deprecated direct support for Docker (including CLI, API, BUILD, Volumes, Auth, Security).
  * Continuity: Docker containers still functioned because they were built with the containerd runtime.

## crictl - Universal CLI for Container Runtimes

### Usage

* Purpose: A universal command-line interface for managing and debugging containers across different runtimes.
* Note: crictl is not used for creating containers.

### Common Commands

* Pull Image: `crictl pull busybox`
* List Images: `crictl images`
* List Containers: `crictl ps -a`
* Execute Command in Container: `crictl exec -i -t <containername> ls`
* View Logs: `crictl logs <container>`
* List Pods: `crictl pods`
