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

