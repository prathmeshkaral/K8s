${\color{red} \textbf{pod.yaml file }}$
````
apiVersion: v1
kind: Pod
metadata:
   name: pod2
spec:
 containers:
 - name: pod1
   image: nginx:latest
   ports:
   - containerPort: 80
  - name: pod2
   image: tomcat
   ports:
   - containerPort: 8080
````
