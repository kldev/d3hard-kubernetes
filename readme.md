# bashrc
```
alias 'mkvm-start'='minikube start --cpus 2 --vm-driver virtualbox --insecure-registry="192.168.39.0/24" --memory 4096'
alias 'kubectl'='k'
```
# install helm

```
kubectl create serviceaccount --namespace kube-system tiller
 
kubectl create clusterrolebinding tiller-cluster-rule --clusterrole=cluster-admin --serviceaccount=kube-system:tiller
 
helm init --service-account tiller
 
kubectl patch deploy --namespace kube-system tiller-deploy -p '{"spec":{"template":{"spec":{"serviceAccount":"tiller"}}}}'
```
# expose port

```
k expose svc/d3env-d3hard  --port=9000 --name=d3hard --type=NodePort

k expose svc/d3env-d3web --name=web --type=LoadBalancer --port=80

k expose svc/d3env-d3web --name=nodePort --type=NodePort --port=80

java -jar app.jar forum --jdbc="jdbc:mysql://mysql-service:3306/forum?useSSL=false&user=d3hard&password=d3hard" --url="http://localhost:9000"

```

# port forward

```
k port-forward svc/d3env-mysql-service 3306:3306
```
# docker tag with local-registry (for minikube)

```
docker tag d3hard localhost:5000/d3hard:v8
docker push  localhost:5000/d3hard:v8
```
