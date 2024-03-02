# k8s-playground

## Build
```
docker build -t minikube-dind -f Dockerfile.dev .
```

## Run
```
docker run --privileged --name minikube-dind-1 -d minikube-dind
```
