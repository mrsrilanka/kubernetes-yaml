kubernetes-yaml
YAML repo
This YAML will create a mongodb instance with 3 replicas and attach storage in the datera backend assuming the dynamic-provisioner, agent-provisioner are running and also secrets and storageClass defined. 

naninga@k8s-Master-pf9:~/home/test$ kc get pods -o wide 

NAME                                        READY     STATUS    RESTARTS   AGE       IP             NODE 

datera-provisioner-agent-5d8576d987-4h6bw   1/1       Running   0          4d        172.16.7.160   k8s-vm1-pf9 

mongo-0                                     2/2       Running   0          2m        172.174.1.21   k8s-vm1-pf9 

mongo-1                                     2/2       Running   0          1m        172.174.1.22   k8s-vm1-pf9 

mongo-2                                     2/2       Running   0          1m        172.174.1.23   k8s-vm1-pf9 

 

naninga@k8s-Master-pf9:~/home/test$ kc get pvc 

NAME                               STATUS    VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS   AGE 

datera-volume-claim                Bound     pvc-622d5a71-308d-11e9-aad0-525400bb83f4   10Gi       RWO            datera         4d 

demo-vol2-claim                    Bound     pvc-5b04f5e5-308e-11e9-aad0-525400bb83f4   100G       RWO            datera         4d 

mongo-persistent-storage-mongo-0   Bound     pvc-77950bb0-3479-11e9-aad0-525400bb83f4   29Gi       RWO            datera         2m 

mongo-persistent-storage-mongo-1   Bound     pvc-8b58f4ed-3479-11e9-aad0-525400bb83f4   29Gi       RWO            datera         2m 

mongo-persistent-storage-mongo-2   Bound     pvc-9226dcda-3479-11e9-aad0-525400bb83f4   29Gi       RWO            datera         1m 

 

 

naninga@k8s-Master-pf9:~/home/test$ kc get sts -o wide 

NAME        DESIRED   CURRENT   AGE       CONTAINERS            IMAGES 

mongo       3         3         2m        mongo,mongo-sidecar   mongo:3.4,cvallance/mongo-k8s-sidecar 

nginx-sts   3         3         1h        nginx                 nginx:1.7.9 

 

 

Headless service 

naninga@k8s-Master-pf9:~/home/test$ kc get services 

NAME         TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)     AGE 

kubernetes   ClusterIP   10.96.0.1    <none>        443/TCP     5d 

mongo        ClusterIP   None         <none>        27017/TCP   38m 

nginx        ClusterIP   None         <none>        80/TCP      1h 

naninga@k8s-Master-pf9:~/home/test$  
