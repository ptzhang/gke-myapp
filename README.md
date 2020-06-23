# gke-myapp

GKE_Beginner_To_Pro

Saturday, 20 June 2020
9:57 AM

https://github.com/ACloudGuru-Resources/Course_GKE_Beginner_To_Pro


docker build -t myapp .
docker images
docker history myapp

docker run -d -p 8888:8888 myapp
docker ps
curl http://localhost:8888
docker logs friendly_poitras

docker exec -it friendly_poitras /bin/bash
echo "hello" > test.txt
cat test.txt
exit

docker stop friendly_poitras
docker start friendly_poitras

docker rm friendly_poitras

docker tag myapp gcr.io/playground-s-11-f8264a/myapp
docker push gcr.io/playground-s-11-f8264a/myapp

gcloud container clusters get-credentials your-first-cluster-1 --zone=us-central1-c

kubectl get nodes
kubectl get pods
kubectl get services

kubectl run nginx --image=nginx
kubectl expose deployment nginx --port=80 --type=LoadBalancer

kubectl apply -f nginx.yaml
kubectl get pods
kubectl port-forward nginx 8080:80
^c
kubectl delete -f nginx.yaml


kubectl apply -f nginx.yaml
kubectl get pods
kubectl exec -it multi -c ftp-container -- /bin/bash
cd pod-data
echo "hello from ftp-container" > index.html
curl http://localhost
^d

echo $FTP_USER
yum -y install ftp



kubectl describe deployment myapp-deployment

kubectl apply -f myapp-service.yaml

kubectl get services

kubectl rollout status deployment.v1.apps/myapp-deployment

kubectl rollout undo deployment.v1.apps/myapp-deployment

kubectl logs pod/myapp-deployment-5ccf8d8d84-c4b7p


**
gcloud container clusters get-credentials your-first-cluster-1 --zone=us-central1-c
kubectl apply -f redis-master-deployment.yaml
kubectl apply -f redis-master-service.yaml
kubectl apply -f redis-slave-deployment.yaml
kubectl apply -f redis-slave-service.yaml
kubectl apply -f frontend-deployment.yaml
kubectl apply -f frontend-service.yaml

kubectl get pods
kubectl get services

**Maintaining a service with unhealthy pods
gcloud iam service-accounts create cloudsqlproxy
gcloud projects add-iam-policy-binding playground-s-11-92c9ad --member serviceAccount:cloudsqlproxy@playground-s-11-92c9ad.iam.gserviceaccount.com --role roles/cloudsql.client
gcloud iam service-accounts keys create ./sqlproxy.json --iam-account cloudsqlproxy@playground-s-11-92c9ad.iam.gserviceaccount.com
kubectl create secret generic cloudsql-instance-credentials --from-file=credentials.json=./sqlproxy.json
kubectl logs pod/myapp-deployment-857857fd9d-5gc8p -c cloudsql-proxy

docker build -t myapp:probes1 .
docker tag myapp:probes1 gcr.io/playground-s-11-92c9ad/myapp:probes1
docker push gcr.io/playground-s-11-92c9ad/myapp:probes1

kubectl get pods
kubectl patch deployment.v1.apps/myapp-deployment -p '{"spec":{"progressDeadlineSeconds":120}}'
kubectl rollout status deployment.v1.apps/myapp-deployment
kubectl describe deployment myapp-deployment

**Volumes and persistent storage
kubectl apply -f mysql-volumeclaim.yaml
kubectl apply -f wordpress-volumeclaim.yaml
kubectl get pvc

kubectl create secret generic mysql --from-literal=password=MYSECRETPASS
kubectl get secrets

kubectl apply -f mysql-deployment.yaml
kubectl apply -f mysql-service.yaml

kubectl apply -f wordpress-deployment.yaml
kubectl apply -f wordpress-service.yaml

kubectl delete pod -l app=mysql

kubectl delete -f wordpress-service.yaml
kubectl delete -f wordpress-deployment.yaml
kubectl delete -f wordpress-volumeclaim.yaml

kubectl delete -f mysql-service.yaml
kubectl delete -f mysql-deployment.yaml
kubectl delete -f mysql-volumeclaim.yaml

** Deployment patterns blue/red
gcloud container clusters get-credentials cluster-1 --zone=us-central1-c
gcloud builds submit --tag gcr.io/playground-s-11-d98568/myapp:v1
gcloud builds submit --tag gcr.io/playground-s-11-d98568/myapp:v2
gcloud builds submit --tag gcr.io/playground-s-11-d98568/myapp:v3

kubectl apply -f myapp-blue.yaml
kubectl apply -f myapp-service.yaml

kubectl apply -f myapp-green.yaml
kubectl apply -f myapp-service.yaml

kubectl describe service myapp-service

kubectl delete -f myapp-blue.yaml
kubectl delete -f myapp-green.yaml

while true; do curl http://34.70.131.90/; sleep 0.5; done

**Autoscaler
go get -u github.com/rakyll/hey


**Helm
gcloud container clusters get-credentials cluster-1 --zone us-central1-c --project playground-s-11-cebfc0
kubectl apply -f tiller-serviceaccount.yaml
//download
wget https://git.io/get_helm.sh
//permission
chmod 700 get_helm.sh
//run it
./get_helm.sh

helm init --service-account helm
kubectl get deploy,svc tiller-deploy -n kube-system

//install a chart
//https://github.com/helm/charts/tree/master/stable

kubectl get deployments
kubectl get statefulsets
kubectl get pv
helm status kneeling-boxer

helm upgrade --set service.type='LoadBalancer' kneeling-boxer stable/bookstack

helm list

helm delete kneeling-boxer

wget https://raw.githubusercontent.com/helm/charts/master/stable/bookstack/values.yaml

helm install -f values.yaml stable/bookstack --name mybooks
helm status mybooks

