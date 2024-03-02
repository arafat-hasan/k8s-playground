# k8s-playground

## Build
```
docker build -t minikube-dind -f Dockerfile.dev .
```

## Run
```
docker run --privileged --name minikube-dind-1 -d minikube-dind
```


### 
```
docker exec -it minikube-dind-1 sh
```

Check if docker is running properly

```
docker info
```

```
 minikube start --driver docker --force

 ```
