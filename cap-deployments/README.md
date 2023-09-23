# Laboratório de deployment k8s

## Aplicar o my-deployment.yaml


```sh
kubectl apply -f my-deployment.yaml
```

> Este deployment sobe um container **nginx** para o laboratório


## Consultar o deployment criado

```sh
$ kubectl get deploy -o wide
NAME                  READY   UP-TO-DATE   AVAILABLE   AGE   CONTAINERS        IMAGES         SELECTOR
frontend-deployment   8/8     8            8           66m   nginx-container   nginx:1.18.0   env=production
```

## Consultar o RollingUpdateStrategy. Por padrão é Rolling release e 25% indisponível

```sh
$ kubectl describe deployments.apps frontend-deployment
```

## Fazer o rollout history para ver o histórico de releases

```sh
$ kubectl rollout history deployment frontend-deployment
deployment.apps/frontend-deployment
REVISION  CHANGE-CAUSE
1         <none>
```


## Aumentar o número de replicas e consultar o rollout history. Veja que o número de revisão não muda fazendo scale up ou scale down

1. Alterar replicas no my-deployment.yaml
2. Consultar o rollout history
```sh
$ kubectl rollout history deploy frontend-deployment
deployment.apps/frontend-deployment
REVISION  CHANGE-CAUSE
1         <none>
```

## Mudar a versão da imagem do container e consultar o rollout history. Veja que o número de revisão vai **mudar**

1. Alterar imagem do container no my-deployment.yaml
2. Consultar o rollout history
```sh
$ kubectl rollout history deploy frontend-deployment 
deployment.apps/frontend-deployment 
REVISION  CHANGE-CAUSE
1         <none>
2         <none>
```

## Consultar o status do rollout

```sh
$ kubectl rollout status deploy frontend-deployment
deployment "frontend-deployment" successfully rolled out
```

## Alterar a imagem do container via terminal 

```sh
$ kubectl set image deployment/frontend-deployment nginx-container=nginx:1.18.0
```

## Consultar o histórico de uma revisão específica

```sh
$ kubectl rollout history deployment frontend-deployment --revision 5
Pod Template:
Labels:       env=production
pod-template-hash=65664cf456
Containers:
nginx-container:
Image:      nginx:1.20.2
Port:       <none>
Host Port:  <none>
Environment:        <none>
Mounts:     <none>
Volumes:      <none>
```

## Fazer undo para a última versão da aplicação

```sh
$ kubectl rollout undo deployment frontend-deployment
```

## Fazer undo para uma revisão específica

```sh
$ kubectl rollout undo deployment frontend-deployment --to-revision=2
deployment.apps/frontend-deployment rolled back
```

## Fazer scale up da aplicação para usar 10 replicas

```sh
$ kubectl scale deploy frontend-deployment --replicas=10
deployment.apps/frontend-deployment scaled
```

## Fazer scale down da aplicação para usar 3 replicas

```sh
$ kubectl scale deploy frontend-deployment --replicas=3
deployment.apps/frontend-deployment scaled
```
