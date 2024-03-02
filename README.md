# k8s-playground


## Setting Up a Kubernetes Playground with minikube-dind

This guide will walk you through building and launching a Docker container that includes both `minikube` and a nested Docker instance (`docker-in-docker`, or `dind`). This environment allows you to experiment with Kubernetes within a contained and isolated setting.

### Building the minikube-dind Image

1. Open a terminal and navigate to the directory containing your `Dockerfile.dev`.
2. Run the following command to build the Docker image named `minikube-dind`:

```
docker build -t minikube-dind -f Dockerfile.dev .
```

This command instructs Docker to build an image using the instructions in `Dockerfile.dev` and tag the resulting image with the name `minikube-dind`.

### Launching the minikube-dind Container

1. Run the following command to start a detached container named `minikube-dind-1` based on the `minikube-dind` image:

```
docker run --privileged --name minikube-dind-1 -d minikube-dind
```

Here's a breakdown of the flags used:

* `--privileged`: Grants the container elevated privileges, necessary for running Docker within a container.
* `--name minikube-dind-1`: Assigns a name to the container for easier identification.
* `-d`: Runs the container in detached mode, allowing the terminal to return control immediately.

### Accessing the DinD Container

To interact with the nested Docker environment, you need to access the container's shell:

```
docker exec -it minikube-dind-1 sh
```

This command connects you to the running container (`minikube-dind-1`) in interactive mode (`-it`) and launches a shell (`sh`) within the container.

### Verifying Docker Functionality

Once inside the container's shell, you can verify that the nested Docker instance is functioning by running:

```
docker info
```

This command should display information about the Docker environment running within the `minikube-dind` container.

### Starting the Kubernetes Cluster

With the nested Docker environment confirmed, it's time to deploy the Kubernetes cluster. **Note:** This step requires administrator access on your host machine.

1. Open a separate terminal with administrator privileges.
2. Run the following command to start a `minikube` cluster using the Docker driver and force recreation if necessary:

```
minikube start --driver docker --force
```

This command instructs `minikube` to utilize the Docker environment within the `minikube-dind` container to set up a Kubernetes cluster. The `--force` flag ensures any existing cluster is recreated.
