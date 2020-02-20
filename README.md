## Install
- npm
- docker
- minikube and kubectl (https://kubernetes.io/docs/tasks/tools/install-minikube/)
## Stages of deployment
1. Start minikube: 
```sh
minikube start
```
2. Deploy <b>authserver</b>
```sh
kubectl apply -f ./kubernetes-files/kub-auth-deployment.yaml --record
kubectl apply -f ./kubernetes-files/service-kub-auth-lb.yaml
```
3. Get auth server IP  
Get kub-auth IP from "TARGET PORT" column.
```sh
minikube service list
```
4. Deploy <b>resourceserver</b>  
Open "kubernetes-files/kub-res-deployment.yaml" file and replace <b>env value</b>
```sh
kubectl apply -f ./kubernetes-files/kub-res-deployment.yaml --record
kubectl apply -f ./kubernetes-files/service-kub-res-lb.yaml
```
5. Get resource server IP  
Get kub-res-lb IP from "TARGET PORT" column.
```sh
minikube service list
```
6. Create docker images of <b>reactclient</b>  
Open "kub/reactclient/src/config.json" and replase host and port each url to values obtained previously
```sh
npm install
npm run build
docker build -f $DOCKERFILE_PATH -t $IMAGE_NAME .
```
7. Deploy <b>reactclient</b>  
Open "kubernetes-files/kub-front-deployment.yaml" file and replace <b>containers image</b>
```sh
kubectl apply -f ./kubernetes-files/kub-front-deployment.yaml --record
kubectl apply -f ./kubernetes-files/service-kub-front-lb.yaml
```

## Open application
```sh
minikube service kub-front-lb
```
<b>login: test</b>  
<b>password: 123</b>
