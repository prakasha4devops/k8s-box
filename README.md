# Kubernetes K8S  Environments and CKA exam some tips


```
git clone git@github.com:prakasha4devops/k8s-environments.git
cd k8s-environments/cluster1

./up.sh  # to run k8s envionment with 3 worker note

vagrant ssh cluster1-master-1

vagrant@cluster1-master-1:~$kubectl version
vagrant@cluster1-master-1:~$kubectl get node
vagrant@cluster1-master-1:~$kubectl get pods
vagrant@cluster1-master-1:~#kubectl cluster-info


#assign role label to worker
kubectl label node cluster1-worker-1 node-role.kubernetes.io/worker=worker
kubectl label node cluster1-worker-2 node-role.kubernetes.io/worker=worker

## example folder
=============
cd /vagrant/cka-examples


# few examples to run


cat <<EOF | kubectl apply -f -
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  selector:
    matchLabels:
      app: nginx
  replicas: 2 
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:latest
        ports:
        - containerPort: 80      
EOF

# Expose the Nginx deployment on a NodePort 32000

cat <<EOF | kubectl apply -f -
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  selector: 
    app: nginx
  type: NodePort  
  ports:
    - port: 80
      targetPort: 80
      nodePort: 32000
EOF

kubectl get pods


curl localhost:3200
# will nginx welcome page

kubectl run  busybox --image=busybox --command -- sleep 3600

kubectl get pods -l run=busybox


kubectl exec -ti busybox -- nslookup kubernetes

#VM IP Address

| VM Name	          |   Purpose	  |  IP	                | 
|-------------------------|---------------|---------------------| 
| clster1-master          | 	 Master	  |  192.168.101.101	| 
| cluster1-worker-1	  | 	 Worker1  |  192.168.101.201    | 
| cluster1-worker-2	  |      Worker2  |  192.168.101.202    | 

  

crictl version
crictl ps  # chekc docker iamges
crictl images
```



# CKA exam some tips
1) cka-tips-and-tricks (https://medium.com/faun/certified-kubernetes-administrator-cka-tips-and-tricks-part-1-2e98e9b31de4)
PART 1 -5
2) awesome-cka-guide(https://github.com/raviacloudguy/awesome-cka-guide)
CKA_Preparation_Guide.pdf (https://github.com/raviacloudguy/awesome-cka-guide/blob/master/CKA_Preparation_Guide.pdf)
3) Practice Enough With These 150 Questions for the CKAD Exam (https://medium.com/bb-tutorials-and-thoughts/practice-enough-with-these-questions-for-the-ckad-exam-2f42d1228552)

few notes 
1) useful command ( https://github.com/prakasha4devops/k8s-environments/blob/master/cluster1/cka-examples/useful-command.txt )
2) import bookmarks to your chrome browser (https://github.com/prakasha4devops/k8s-environments/blob/master/CKA-exam-bookmarks/bookmarks_5_13_20.html )

***Mumshad Mannambeth CKA course practice test , troublesting chapter and light test 3-4 times before exam. 

Best luck 

# CKAD Exam some tips
 
 time management , 12-15 questions in 1 hours, imperative command , troubleshoot service/pods/deployment
 
1) mumshad course CKAD  - practice test  light test 3-4 times before exam. 

2) CKAD Exercises
 https://github.com/dgkanatsios/CKAD-exercises
3) CKAD Prep
https://github.com/bmuschko/ckad-prep
4) Practice Enough With These 150 Questions for the CKAD Exam (https://medium.com/bb-tutorials-and-thoughts/practice-enough-with-these-questions-for-the-ckad-exam-2f42d1228552
5) ckad-notes
https://github.com/nikhilagrawal577/ckad-notes

## setup and run - latest kubernets version 1.18.2-00 
You will start a 3 node cluster on your machine, one master and 2 worker. For this you need to install VirtualBox and vagrant, then:
