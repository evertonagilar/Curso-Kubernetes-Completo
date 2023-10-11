# Laboratório de namespaces k8s

## Subir os pods do tomcat e do redis deste laboratório


```sh
$ kubectl apply -f redis-pod.yaml
$ kubectl apply -f tomcat-pod.yaml
```

## Consultar os pods

```sh
$ kubectl get pods
NAME         READY   STATUS    RESTARTS   AGE
redis-pod    1/1     Running   0          53s
tomcat-pod   1/1     Running   0          44s
```

## Ver os IPs de cada pod

```sh
$ kubectl get pod -o wide
NAME         READY   STATUS    RESTARTS   AGE     IP            NODE                NOMINATED NODE   READINESS GATES
redis-pod    1/1     Running   0          7m32s   10.244.2.43   mycluster-worker2   <none>           <none>
tomcat-pod   1/1     Running   0          7m23s   10.244.1.43   mycluster-worker    <none>           <none>
```

## Consultar o IP de um pod com describe

```sh
$ kubectl describe pod tomcat-pod | grep IP
IP:               10.244.1.43
IPs:
IP:  10.244.1.43
```


## Conectar no pod do tomcat

```sh
$ kubectl exec -it tomcat-pod -- bash
root@tomcat-pod:/usr/local/tomcat# 
```

## Instalar ferramentas necessárias para diagnóstico de rede


```sh
$ apt update && apt install iputils-ping -y
```


