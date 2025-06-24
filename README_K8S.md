# Usando Kubernetes no Projeto
## Instalação do Kind
Para começar a usar o Kubernetes com este projeto, você precisa instalar o Kind (Kubernetes IN Docker). Você pode fazer isso facilmente usando o Homebrew. Execute o seguinte comando:
```bash
brew install kind
```
## Criando um Cluster
Depois de instalar o Kind, você pode criar um cluster Kubernetes com o seguinte comando:
```bash
kind create cluster --name=goexpert
```
Isso criará um cluster chamado `goexpert`.
## Verificando o Cluster
Para verificar se o cluster foi criado corretamente, você pode usar o seguinte comando:
```bash
kubectl cluster-info --context kind-goexpert
```
Isso mostrará informações sobre o cluster, incluindo o endereço do servidor de API e outros detalhes.
## Verificando os Nós do Cluster
Para ver os nós do cluster, execute:
```bash
kubectl get nodes
```
Isso listará todos os nós disponíveis no cluster, permitindo que você verifique se tudo está funcionando corretamente.
## Criando o Deployment
O próximo passo é criar um Deployment para o seu aplicativo. O arquivo `deployment.yaml` que você criou deve ter o seguinte conteúdo:
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: server
spec:
  selector:
    matchLabels:
      app: server
  template: 
    metadata:
      labels:
        app: server
    spec:
      containers:
        - name: server
          image: remonato/goapp:latest
          resources:
            limits:
              memory: "128Mi"
              cpu: "500m"
          ports:
            - containerPort: 8080
```
Este arquivo define um Deployment chamado `server`, que usa a imagem `remonato/goapp:latest`. Ele especifica os recursos limitados para o contêiner, como memória e CPU, e define a porta do contêiner como 8080.
## Aplicando o Deployment
Para aplicar o Deployment ao seu cluster, use o seguinte comando:
```bash
kubectl apply -f k8s/deployment.yaml
```
Isso criará o Deployment no cluster Kubernetes.
## Verificando os Pods
Após aplicar o Deployment, você pode verificar os Pods criados com o seguinte comando:
```bash
kubectl get pods
```
Isso listará todos os Pods em execução no cluster, permitindo que você veja se o Deployment foi criado corretamente e se o aplicativo está funcionando como esperado.