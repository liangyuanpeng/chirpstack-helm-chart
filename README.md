# chirpstack-helm-chart
helm chart for chirpstack, still development

# 

`git clone https://github.com/liangyuanpeng/chirpstack-helm-chart.git`  

`cd chirpstack-helm-chart/`  

` helm install chirpstack .` 

```
root@yh-console:~/lan/iot/chirpstack-helm-chart#  kubectl get po 
NAME                              READY   STATUS    RESTARTS   AGE
chirpstack-as-84b68cb7fd-zgs5j    1/1     Running   0          45s
chirpstack-ns-7d9b9867f-zftn6     1/1     Running   0          45s
mosquitto-0                       1/1     Running   0          45s
pgsql-0                           1/1     Running   0          45s
redis-0                           1/1     Running   0          45s
redis-exporter-64f8bf4f46-2rcgl   1/1     Running   0          45s
```  

```
root@yh-console:~/lan/iot/chirpstack-helm-chart# kubectl get svc
NAME             TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)                      AGE
chirpstack-as    ClusterIP   10.98.227.61     <none>        8080/TCP,8001/TCP,8003/TCP   77s
chirpstack-ns    ClusterIP   10.108.182.238   <none>        8000/TCP                     77s
mosquitto        ClusterIP   10.104.149.103   <none>        1883/TCP                     77s
pgsql            ClusterIP   10.102.33.231    <none>        5432/TCP                     77s
redis            ClusterIP   10.109.138.95    <none>        6379/TCP                     77s
redis-exporter   ClusterIP   10.106.66.131    <none>        9121/TCP                     77s
```  

```
root@yh-console:~/lan/iot/chirpstack-helm-chart# kubectl get pvc
NAME                               STATUS   VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS   AGE
pgsql-pvc-pgsql-0                  Bound    pvc-c1c6adf4-32ef-4431-bd6a-3825a6ef408c   96Mi       RWO            longhorn       3d
redis-pvc-redis-0                  Bound    pvc-e464d0e8-e04a-4958-858e-5efef1aeba9c   48Mi       RWO            longhorn       3d
```  

```
root@yh-console:~/lan/iot/chirpstack-helm-chart# helm list
NAME            NAMESPACE       REVISION        UPDATED                                 STATUS          CHART                           APP VERSION
chirpstack      default         1               2021-01-29 16:11:48.984574857 +0800 CST deployed        chirpstack-helm-chart-0.1.0     1.16.0
```  

network-servers/create  
The 'hostname:port' of the network-server, e.g. 'localhost:8000'.
```
chirpstack-ns.default:8000
chirpstack-ns.default.svc.cluster.local:8000
```


设置UDP数据转发  NodePort模式 

k expose deploy gateway-bridge --port 1700 --target-port=1700 --protocol=UDP --name udpservice --type=NodePort