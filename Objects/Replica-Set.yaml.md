${\color{green} \textbf{Replica-Set file}}$
````
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: rs-demo
  labels:
    app: nginx-app
spec:
 replicas: 4
 selector:
   matchLabels:
     app: nginx-app
     env: dev
 template:
  metadata:
   labels:
    app: nginx-app
    env: dev
  spec:
   containers:
   - name: nginx
     image: nginx:latest
     ports:
     - containerPort: 80
````
````
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: rs-demo
  labels:
    app: nginx-app
spec:
 replicas: 4
 selector:
   matchExpressions:
     - key: app
       operator: In
       values:
       - nginx-app
 template:
  metadata:
   labels:
    app: nginx-app
    env: dev
  spec:
   containers:
   - name: nginx
     image: nginx:latest
     ports:
     - containerPort: 80``
````
