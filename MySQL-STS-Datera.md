# kubernetes-yaml
YAML repo

This yaml will create a statefulset and create 3 stateful volumes in the Datera storage backend.

naninga@k8s-Master-pf9:~/home/test$ kc get sts -o wide
NAME        DESIRED   CURRENT   AGE       CONTAINERS            IMAGES
mysql       3         3         6m        mysql                 mysql:5.6
naninga@k8s-Master-pf9:~/home/test$ 

naninga@k8s-Master-pf9:~/home/test$ kc get pvc
NAME                               STATUS    VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS   AGE
mysql-vol-mysql-0                  Bound     pvc-ed7d4230-3483-11e9-aad0-525400bb83f4   25Gi       RWO            datera         1m
mysql-vol-mysql-1                  Bound     pvc-f2c0b1c1-3483-11e9-aad0-525400bb83f4   25Gi       RWO            datera         1m
mysql-vol-mysql-2                  Bound     pvc-fa8fc2e4-3483-11e9-aad0-525400bb83f4   25Gi       RWO            datera         1m
naninga@k8s-Master-pf9:~/home/test$

naninga@k8s-Master-pf9:~/home/test$ kc get services -o wide
NAME         TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)     AGE       SELECTOR
kubernetes   ClusterIP   10.96.0.1        <none>        443/TCP     5d        <none>
mongo        ClusterIP   None             <none>        27017/TCP   1h        role=mongo
mysql        ClusterIP   None             <none>        3306/TCP    7m        app=mysql
mysql-read   ClusterIP   10.108.158.179   <none>        3306/TCP    16m       app=mysql
nginx        ClusterIP   None             <none>        80/TCP      2h        app=nginx
naninga@k8s-Master-pf9:~/home/test$ 

naninga@k8s-Master-pf9:~/home/test$ kc get pods -o wide -l app=mysql
NAME      READY     STATUS    RESTARTS   AGE       IP             NODE
mysql-0   1/1       Running   0          8m        172.174.1.24   k8s-vm1-pf9
mysql-1   1/1       Running   0          8m        172.174.1.25   k8s-vm1-pf9
mysql-2   1/1       Running   0          8m        172.174.1.26   k8s-vm1-pf9
naninga@k8s-Master-pf9:~/home/test$ 


