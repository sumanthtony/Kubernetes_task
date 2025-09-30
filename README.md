# Kubernetes_task
Deploy and manage apps in Kubernetes using Minikube cluster/Kops cluster

Following steps has taken to complete the task

NOTE: AS IN MY AWS ACCOUNT HAS SOME PERMISSION ISSUES WHILE LAUNCHING AND PERFORMING TASKS IN **MINIKUBE** HENCE USED **KOPS AS IT IS A MULTINODE-CLUSTER** AND WILL HAVE HIGH AVAILABILITY WHEN COMPARED TO MINIKUBE.

**--->** Launched a EC2 instance and install packages to create **KOPS cluster** **(AWS CLI, KOPS, KUBECTL)** and attached **ADMIN** role to the server to communicate and integrate with AWS services.

**--->** To **store** all **KOPS information** exported to **Amazon S3 Bucket** with command: **export KOPS_STATE_STORE=s3://demo.bucket.one**

**--->** Created a **KOPS cluster** with command : kops create cluster --name sumanth.k8s.local --zones ap-south-1a,ap-south-1b --master-size t2.medium --master-volume-size 20 --node-size t2.micro --node-volume-size 20 --node-count 2

Note: 
1. Here I have created **1 Master and 2 Worker node** with each EBS volume of 20 and for **High Availability** placed the nodes in **multiple Availability zones**
2. In the backend **Infrastructure** is created and will take some time to reflect the changes in the **EC2 page**, and once done using this command **(kubectl get no)** we can confirm when the nodes state is in **READY** we can say cluster creation is completed and now can start working on it.

**--->** Written a **Deployment.yml & service.yml** in same file and saved. 

Deployments are one of the main resources in K8S and has following features:

1. **No Downtime**: Sometimes in docker we face some **latency** while accessing the application, but in deployment within no time we can access and work on it.
2. **Rollback** : We can **rollback to any specific version** if the current version is not stable and we can rollback using 2 ways: (by editing manually in deployment.yml file & using directly with command)
3. **AutoScaling** : We can scale the applications according to our requirement, and we have 2 types of scaling features in deployments: **Manual Scaling Auto Scaling**
   a) Manual Scaling: We can scale in or scale out the deployments either using commands or editng the deployment.yml file.
   b) Auto Scaling: For this we use HPA (Horizontal Pod AutoScaler) it will **scale-in/scale-out** the Pods automatically based on the traffic/load occured.
4. **Image-Updation** : We can update the images using commands without any dowmtime and access the application and can even **pause & resume** the deployments as well when required.
   a) We can **check and maintain the history** of deployments status of rollbacks and if required we can rollout to specific version.


**--->** Below is the deployment snapshot

<img width="625" height="216" alt="Deployment creation steps" src="https://github.com/user-attachments/assets/5ddd1adc-4c24-4701-86eb-9f43f6f59ef4" />

**--->** Described the deployment.yml file to check the logs and events (We can even check Pod details as well using **describe** command)

<img width="610" height="368" alt="Described deploy file" src="https://github.com/user-attachments/assets/cfaea570-7f5b-4c5d-af67-b733f4dc1f99" />

**--->** **Below are the Snapshots of the features in Deployment used practically.**

<img width="482" height="137" alt="Image Updation" src="https://github.com/user-attachments/assets/d3e4f1a4-f216-4408-91df-d7280c8665d5" />

<img width="455" height="173" alt="Rollback" src="https://github.com/user-attachments/assets/c8ce0141-f82f-46a5-9762-f2695797c1e2" />

<img width="393" height="218" alt="Scale-1" src="https://github.com/user-attachments/assets/a601f08c-9f41-40a1-b643-325b7529bed7" />

<img width="442" height="194" alt="Scale-2" src="https://github.com/user-attachments/assets/3621f07d-db90-4725-a5ef-557f2ab8bf20" />

**--->** Below is the output of the **Netflix Application** accessed using **NodePort** 

<img width="670" height="404" alt="Netflix output" src="https://github.com/user-attachments/assets/d70460c5-9a90-46fe-bb4d-e89f87e2a11e" />



