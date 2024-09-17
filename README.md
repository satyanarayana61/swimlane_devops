Step1: Installed the mongo db using helm charts.

**Installed MongoDB:**
helm install my-mongodb bitnami/mongodb   --set auth.rootPassword=supersecretroot   --set auth.username=myuser   --set auth.password=mypassword   --set auth.database=mydatabase   --set auth.enabled=true   --set persistence.enabled=true   --set persistence.size=2Gi   --set persistence.storageClass=azurefile

**#Wrtien the multi stage Docker file to create the image for app.**
Step1 : To build the images to follow below commands.
 docker build -t my-app .
Step2: Created the tag for the image and psuh to Azure container registry(ACR).
         docker tag my-app:latest tbshelmacr.azurecr.io/devopspractical/my-app:latest
         docker push tbshelmacr.azurecr.io/devopspractical/my-app:latest
 Step3:  writen the kubernets manifest file for deployment and service
         File name: **Application.yaml**
                      **Svc.yaml**
          kubectl apply -f  Application.yaml
          kubectl apply -f  Svc.yaml

 Secrets: 
  kubectl create secret docker-registry myregistreykey --docker-server=****** --docker-username=***** --docker-password=******
  
HPA:
kubectl autoscale deployment my-app --cpu-percent=50 --min=1 --max=10

 

       
