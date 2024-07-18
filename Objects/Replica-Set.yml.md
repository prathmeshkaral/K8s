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
${\color{red} \textbf{RS In}}$
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
${\color{blue} \textbf{RS NotIn}}$
````
apiVersion: apps/v1
kind: ReplicaSet
metadata:
 name: nginx-app
 labels:
    app: nginx-app
spec:
  replicas: 3
  selector:
     matchExpressions:
       - key : app
         operator: NotIn
         values:
         - nginx-app

  template:
     metadata:
       name: nginx-temp
       labels:
          app: nginx-app
     spec:
       containers:
        - name: nginx-cont
          image: nginx:latest
          ports:
          - containerPort: 80

  template:
     metadata:
       name: httpd-temp
       labels:
          app: httpd
     spec:
       containers:
        - name: httpd
          image: httpd:latest
          ports:
          - containerPort: 81
````
${\color{purple} \textbf{RS Exists}}$
````
# ReplicaSet With Exits set based selector
apiVersion: apps/v1
kind: ReplicaSet
metadata:
 name: nginx-app
 labels:
    app: nginx-app
spec:
  replicas: 3
  selector:
     matchExpressions:
       - key : app
         operator: Exists

  template:
     metadata:
       name: nginx-temp
       labels:
          app: nginx-app
     spec:
       containers:
        - name: nginx-cont
          image: nginx:latest
          ports:
          - containerPort: 80

  template:
     metadata:
       name: httpd-temp
       labels:
          app: httpd
     spec:
       containers:
        - name: httpd
          image: httpd:latest
          ports:
          - containerPort: 81
````

## Selectors

1. Equality Based Selector

- it is old version of selectors
- we use Equality based in Replication controoler for manage with pod
- it define with key:value
 
2. Set Based Selector

- it is updated version of selector
- we use Set based in Replica set and Replication controller also.
- it define with
- In = key: value
- NotIN = key: value : avoid it and run
- Exists = env{ } : run all which hav in that env 
