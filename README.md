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
