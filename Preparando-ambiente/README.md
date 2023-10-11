## Instalar o kubectl

```sh
curl -LO "https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl"
chmod +x kubectl
sudo mv kubectl /usr/local/bin/
```

## Verificar se o aplictivo foi instalado corretamente:
	
```sh
$ kubectl version --client
Client Version: v1.28.0
Kustomize Version: v5.0.4-0.20230601165947-6ce0bf390ce3
```

## Executar o instalador do Minikube


```sh
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
```

## Configurar o docker como driver padrão (container runtime) para o Kubernetes 

```sh
	minikube config set driver docker
```

## Inicializar um cluster

```sh
	minikube start 
```

## Listar o IP do apiServer

```sh
	kubectl describe service kubernetes 
```

## Criando um namespace via linha de comando

```sh
kubectl create namespace frontend --save-config
```

