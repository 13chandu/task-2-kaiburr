# task-3-kaiburr
# deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: your-app-deployment
spec:
  replicas: 1
  selector:
    matchLabels:
      app: your-app
  template:
    metadata:
      labels:
        app: your-app
    spec:
      containers:
        - name: your-app
          image: your-docker-image:latest
          ports:
            - containerPort: 80
          env:
            - name: MONGODB_URI
              value: "mongodb://mongodb-service:27017/your-database"

# service.yaml
apiVersion: v1
kind: Service
metadata:
  name: your-app-service
spec:
  selector:
    app: your-app
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
  type: NodePort # You can use LoadBalancer or Ingress here as well
