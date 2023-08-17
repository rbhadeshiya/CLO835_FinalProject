CLO835 Final Project: Deployment of 2-tiered web application to managed K8s cluster on Amazon EKS, with pod auto-scaling and deployment automation. 

To run this github files,

1. make terraform infrastructure
2. push ecr repo
3. make eks cluster
4. check accessbility locally
5. for mysql
   5.1 docker run -d -e MYSQL_ROOT_PASSWORD=pw <dbreponame>
   5.2 docker exec -it <sql container id> bin/bash
   5.3 check if you can access database or not
6. for app
   6.1 docker run docker run --name <anyname> -it -d -p 81:81 -e DBHOST=172.17.0.2 -e DBPORT=3306 -e DBUSER=root -e DBPWD=pw <appreponame>
   6.2 docker inspect <container id>
   6.3 copy ip add and curl <ip>:81
7. go to your cloud9 ec2 instance and open port 81 for all traffic and copy <instance id>:81
8. lets run all manifests file
   8,1 so we have already deployed eks cluster so now lets check if its working or not -- kubectl get nodes
   8.2 Now lets create namespace-- kubectl create ns final
   8.2 now after this lets run all manifests file in below order
       alias k=kubectl
   k apply -f secret.yaml -n final
   k apply -f configmap.yaml -n final
   k apply -f serviceaccount.yaml -n final
   k apply -f role.yaml -n final
   k apply -f rolebinding.yaml -n final
   k apply -f pv.yaml -n final
   k apply -f pvc.yaml -n final
   k apply -f db_deployment.yaml -n final
   k apply -f db_service.yaml -n final
   k apply -f app_deployment.yaml -n final
   k apply -f app_service.yaml -n final
9. Now try to access application through LoadBalancer dns name and access application externally
   

   
   
   

     
