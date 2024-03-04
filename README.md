# k8s-Playground

## Creating a Kubernetes Playground with Nested Docker (minikube-dind)

This guide simplifies setting up a Kubernetes environment within a Docker container. This approach, utilizing **minikube-dind**, provides a convenient and isolated space for experimenting with Kubernetes.


## Building and Running the minikube-dind Image:

1. **Build the Image:**

   ```bash
   docker compose up -d
   ```

   This command leverages Docker Compose to build and launch the `minikube-dind` image in the background (`-d`).

2. **Accessing the Nested Docker Environment:**

   Interact with the nested Docker instance using:

   ```bash
   docker exec -it minikube-dind-1 sh
   ```

   This command grants you interactive shell access (`-it`) within the container named `minikube-dind-1`.

3. **Verifying Docker Functionality:**

   Confirm the nested Docker environment is operational by running:

   ```bash
   sudo docker info
   ```

   This command displays information about the Docker instance running within the `minikube-dind` container.

## Starting the Kubernetes Cluster

**Deploy the Kubernetes cluster:**

   ```bash
   sudo minikube start --driver docker --force
   ```

   This command instructs `minikube` to utilize the Docker environment within the `minikube-dind` container to set up a Kubernetes cluster. The `--force` flag ensures any existing cluster is recreated and enforces the use of the "docker" driver even with root privileges.
