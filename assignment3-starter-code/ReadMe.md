#Part 2:
### Build docker images
docker build -t flask-app .   
docker-compose up -d   
docker ps 

### Push images
docker login
docker tag flask-app:latest serriaguirregaray/flask-app:latest 
docker push serriaguirregaray/flask-app:latest 

#Part 3:
minikube start

### Deployment
kubectl apply -f flask-app-deployment.yaml  
kubectl apply -f mongodb-deployment.yaml

### Services
kubectl apply -f flask-app-service.yaml  
kubectl apply -f mongodb-service.yaml

### Access the app
minikube service flask-app-service

#Part 4:eksctl create cluster --name Assignment3Cluster --region us-east-1 --zones us-east-1a,us-east-1b,us-east-1c,us-east-1d,us-east-1f
aws eks --region us-east-1 update-kubeconfig --name Assignment3Cluster
kubectl config get-contexts
kubectl config use-context A3User@Assignment3Cluster.us-east-1.eksctl.io

http://aa9a87c431e74449fa2d7f7216cff703-814797648.us-east-1.elb.amazonaws.com:32738

aws cloudformation delete-stack --stack-name eksctl-Assignment3Cluster-cluster

#Part 5:

### Create
kubectl create -f replication-controller.yaml  

### Verify its up
kubectl get replicationcontroller  
kubectl get pods  

### Test healing
kubectl delete pod <pod-name>  

### Test replica number change
Change the replicas in the file and then:  
kubectl apply -f replication-controller.yaml  
kubectl get pods  

#Part 6:

Modify the flask app deployment file then:  
kubectl apply -f flask-app-deployment.yaml

### Monitor rolling update
kubectl get deployment flask-app-deployment  
kubectl rollout status deployment/flask-app-deployment

#Part 7:
Modify the flask app deployment file then:  
kubectl apply -f flask-app-deployment.yaml
kubectl apply -f flask-app-service.yaml  

### Verify
kubectl get pods
kubectl describe pod <pod-name>

# Part 8
kubectl apply -f prometheus-deployment.yaml
kubectl apply -f prometheus-config.yaml
kubectl apply -f alertmanager-deployment.yaml
kubectl apply -f alertmanager-config.yaml

kubectl delete configmap prometheus-server-conf
kubectl create configmap prometheus-server-conf --from-file=prometheus-config.yaml
kubectl delete configmap alertmanager-config
kubectl create configmap alertmanager-config --from-file=alertmanager-config.yaml

minikube service prometheus-service --url















