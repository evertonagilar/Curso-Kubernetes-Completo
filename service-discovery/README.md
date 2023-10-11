# Laborat�rio de service discovery

## Verificar como os servi�os s�o encontrados e a estrutura FQDN do Kubernetes

1. Entrar em algum pod e consultar o arquivo /etc/resolv.conf e o arquivo /etc/hosts

```sh
root@debian:/# cat /etc/resolv.conf
search default.svc.cluster.local svc.cluster.local cluster.local
nameserver 10.96.0.10
options ndots:5
``` 

2. Entender como � a FQDN no Kubernetes

kubernetes.default.svn.cluster.local

<pre>
kubernetes      -> nome do servi�o
default         -> namespace padr�o do servi�o
svc             -> servi�o (Kind: Service)
cluster.local   -> nome do cluster
</pre>

3. Usar o nslookup para consultar o dns

```sh
root@debian:/# nslookup kubernetes.default.svc.cluster.local
   Server:		10.96.0.10
   Address:	10.96.0.10#53

Name:	kubernetes.default.svc.cluster.local
Address: 10.96.0.1
```




