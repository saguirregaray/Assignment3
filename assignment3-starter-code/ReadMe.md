#Part 2:
### Build docker images
docker build -t flask-app . <br> 
docker-compose up -d <br>
docker ps <br>

### Push images
docker login <br>
docker tag flask-app:latest serriaguirregaray/flask-app:latest <br>
docker push serriaguirregaray/flask-app:latest <br>

#Part 3:
minikube start <br>

### Deployment
kubectl apply -f flask-app-deployment.yaml <br>
kubectl apply -f mongodb-deployment.yaml <br>

### Services
kubectl apply -f flask-app-service.yaml <br>
kubectl apply -f mongodb-service.yaml <br>

### Access the app
minikube service flask-app-service

#Part 4:










