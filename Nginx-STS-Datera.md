# kubernetes-yaml
YAML repo
The yaml will create a headless service and then create a statefulset wth three replicas with a Datera volumes attached in the backend.
Assuming StorageClass Secrets are created in the default namespace and dynamic-provisioner and agent provisioner is running. 

```
naninga@k8s-Master-pf9:~/home/test$ kc get pods -o wide  

NAME                                        READY     STATUS              RESTARTS   AGE       IP             NODE 

datera-provisioner-agent-5d8576d987-4h6bw   1/1       Running             0          4d        172.16.7.160   k8s-vm1-pf9 

nginx-sts-0                                 1/1       Running             0          2m        172.174.1.18   k8s-vm1-pf9 

nginx-sts-1                                 1/1       Running             0          2m        172.174.1.19   k8s-vm1-pf9 

nginx-sts-2                                 1/1       Running             0          1m        172.174.1.20   k8s-vm1-pf9 

percona2                                    1/1       Running             0          4d        172.174.1.3    k8s-vm1-pf9 

 

 

naninga@k8s-Master-pf9:~/home/test$ kc get pvc 

NAME                   STATUS    VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS   AGE 

datera-volume-claim    Bound     pvc-622d5a71-308d-11e9-aad0-525400bb83f4   10Gi       RWO            datera         4d 

demo-vol2-claim        Bound     pvc-5b04f5e5-308e-11e9-aad0-525400bb83f4   100G       RWO            datera         4d 

mongodb-volumeclaim1   Bound     pvc-dd1853a6-3461-11e9-aad0-525400bb83f4   60Gi       RWO            datera         1h 

www-nginx-sts-0        Bound     pvc-12b10a16-3471-11e9-aad0-525400bb83f4   19Gi       RWO            datera         2m 

www-nginx-sts-1        Bound     pvc-17a8fe30-3471-11e9-aad0-525400bb83f4   19Gi       RWO            datera         2m 

www-nginx-sts-2        Bound     pvc-1d370949-3471-11e9-aad0-525400bb83f4   19Gi       RWO            datera         1m 

 

naninga@k8s-Master-pf9:~/home/test$ kc get sts -o wide 

NAME        DESIRED   CURRENT   AGE       CONTAINERS   IMAGES 

mongo       3         2         1h        mongo        mongo:4.1 

nginx-sts   3         3         3m        nginx        nginx:1.7.9 

 

 

naninga@k8s-Master-pf9:~/home/test$ kc get services -o wide 

NAME         TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)     AGE       SELECTOR 

kubernetes   ClusterIP   10.96.0.1    <none>        443/TCP     4d        <none> 

mongo        ClusterIP   None         <none>        27017/TCP   1h        role=mongo 

nginx        ClusterIP   None         <none>        80/TCP      3m        app=nginx 

naninga@k8s-Master-pf9:~/home/test$  
```
