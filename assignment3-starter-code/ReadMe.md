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

#Part 4:

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
kubectl apply -f prometheus-service.yaml
kubectl apply -f prometheus-server-conf.yaml
kubectl apply -f alert.rules
kubectl apply -f prometheus-deployment.yaml


minikube service prometheus-service --url

kubectl delete pod -l app=prometheus

















