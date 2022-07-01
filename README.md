# Volumes-Persistentes-



Jose Carlos Macoratti

Kubernetes - Volumes Persistentes

Persistent Volume Claim ( VPC ) 
Persistent Volume ( PV ) 

Provisioning 
Binding 
Using 
Reclaming 
Exclusão 

Estados do Persistent Volume  ( PV ) 

Available
Bound 
Released 
Failed 

apiVolume:v1 
kind: PersistentVolume
metadata: 
name: aspnet-pv
labels:
   type: local-pv
spec: 
capacity:
   storage: 5Mi
volumeMode: fileSystem  // block - Filesystem 
accessModes: // RWO, ROX, RWX, RWOP 
   ReadWriteOnce
persistentVolumeReclaimPolicy: Recycle // Recycle, Retain, Delete
hostPath:
  path: “/app/meu volume”
storageClassName: manual // StorageClass
pv1.yml



apiVolume:v1 
kind: PersistentVolumeClaim
metadata: 
name: aspnet-pv
labels:
   type: local-pv
spec: 
storageClassName: manual
accessModes: 
ReadWriteOnce
resources: 
requests:
storage: 5Mi
selector:
matchLabels:  
type: local-pv
pvc1.yml



apiVolume:v1 
kind: Pod
metadata: 
name:aspnet-pod
spec:
containers:
-name: aspn-container
image: macoratti/pizzafrontend:latest
ports:
-ContainerPort: 80 
name: “frontend-mvc”
VolumeMounts: 
-monthPath: “/app/meuvolume”
name: aspn-storage
Volumes: 
-name: aspn-storage
persistentVolumeClaim:
claimName: aspnet-pvc
pod1.yml

minikube start 
dir 
     pod1.yml
     pv1.yml
     pvc1.yml

Visual Studio Code 
apiVolume:v1 
kind: PersistentVolume
metadata: 
name: aspnet-pv
labels:
   type: local-pv
spec: 
capacity:
   storage: 5Mi
volumeMode: fileSystem  // block - Filesystem 
accessModes: // RWO, ROX, RWX, RWOP 
   ReadWriteOnce
persistentVolumeReclaimPolicy: Recycle // Recycle, Retain, Delete
hostPath:
  path: “/app/meu volume”
storageClassName: manual // StorageClass
pv1.yml


apiVolume:v1 
kind: PersistentVolumeClaim
metadata: 
name: aspnet-pv
labels:
   type: local-pv
spec: 
storageClassName: manual
accessModes: 
ReadWriteOnce
resources: 
requests:
storage: 5Mi
selector:
matchLabels:  
type: local-pv
pvc1.yml




apiVolume:v1 
kind: Pod
metadata: 
name:aspnet-pod
spec:
containers:
-name: aspn-container
image: macoratti/pizzafrontend:latest
ports:
-ContainerPort: 80 
name: “frontend-mvc”
VolumeMounts: 
-monthPath: “/app/meuvolume”
name: aspn-storage
Volumes: 
-name: aspn-storage
persistentVolumeClaim:
claimName: aspnet-pvc
pod1.yml


cls
kubectl apply -f pv1.yml
kubectl get pv

kubectl aplly -f pvc1.yml 
kubectl get pvc

kubectl aplly -f pod1.yml
kubectl get all 

cls
kubectl get all 
kubectl describe pod aspnet-pod

kubectl get all 
kubectl exec -it aspnet-pod - - /bin/bash 
ls -l
cd meu volume 
cls
ls -l 
cls
clear 
ls -l 

echo teste persistent volume > testepv.txt
ls
cat testepv.txt 
exit

kubectl get pod 
kubectl delete pod aspnet-pod
cls

kubectl get all
kubectl apply -f pod1.yml
kubectl get all
kubectl exec -it aspnet-pod - - /bin/bash 
ls -l 
cd meuvolume 
ls -l 
cat testepv.txt
