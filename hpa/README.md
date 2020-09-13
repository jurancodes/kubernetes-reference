# Horizontal Pod Autoscaler

## Descrição dos Arquivos
`nginx-deployment.yml`: cria um deployment básico do nginx para testes com HPA.  
`nginx-hpa-cpu-v1.yml`: cria um HPA baseado em **CPU** utilizando a API stable v1.  
`nginx-hpa-cpu-v2beta2.yml`: cria um HPA baseado em **CPU** utilizando a API beta v2beta2.  
`nginx-hpa-memory-v2beta2.yml`: cria um HPA baseado em **Memória** utilizando a API beta v2beta2.  

## Comandos Básicos
Criação de objetos utilizando arquivo YAML:  
`kubectl apply -f <nome-do-arquivo>`  
\
Visualizar a utilização de recursos dos pods (cpu/mem):  
`kubectl top pods -n <namespace>`  
\
Visualizar a utilização de recursos dos nodes (cpu/mem):  
`kubectl top nodes`  
\
Visualizar HPA:  
`kubectl get hpa -n <namespace>`  
`kubectl describe hpa <hpa-name> -n <namespace>`   

## Pod Stress  
**Entrar no pod usando `kubectl exec`:**   
`kubectl get pods -n <namespace>`  
`kubectl exec -it <pod-name> -n <namespace> -- bash`  
\
**Instalar stress e procps no pod:**  
_stress:_ utilizado para realizar testes de stress no pod.  
_stress-ng:_ utilizado para realizar testes de stress no pod.   
_procps:_ habilita comandos como ps, top, pkill, etc.  
`apt update && apt install stress procps -y`  
\
**CPU Stress:**  
`apt update && apt install procps stress-ng -y`  
`stress-ng -c 1 -l 95 &`: executa um stress de CPU em 1 core (`-c 1`) com carga de 95% (`-l 95`).   
\
**Memory Stress:**  
`stress --vm 1 --vm-bytes 770M --vm-keep &`  

## Outros Comandos
Obter métricas dos pods:  
`kubectl get --raw /apis/metrics.k8s.io/v1beta1/namespaces/<namespace>/pods/<pod-name>`   