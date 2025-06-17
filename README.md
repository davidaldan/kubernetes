# KUBERNETES

```bash
# ver url del servicio de minikube
minikube service app1-service --url
```

## PODS
```bash
# información de los pods
kubectl get pods
kubectl describe pods
kubectl get pods -o wide
```

```bash
# listar todo lo creado
kubectl get all
```

```bash
# eliminar un deployment
kubectl delete deployment name
```

## YAML
```bash
-   apiVersion
-   kind (Pod, service, ReplicaSet, deployment)
-   metadata (name, labels -> app | type)
-   spec ( containers -> name | image)
```

## CREAR
```bash
kubectl create -f file.yml
kubectl apply -f file.yml
```

## REPLICASET
```bash
kubectl delete replicationcontroller name (viejo modo)
kubectl get replicaset
kubectl delete replicaset name
# Actualizar replicas:
kubectl scale --replicas=2 -f rstest.yml
```

## DEPLOYMENTS
```bash
kubectl scale deploy/app1-dp --replicas 2
kubectl delete deployment name
kubectl rollout status deploy/app1-dp
kubectl rollout history deploy/app1-dp
# registra cambios de deployment
kubectl apply -f dptest.yml --record 
# cambiar imagen de deployment
kubectl set image deployment/app1-dp nginx-container=nginx:1.17.10
# rollback cambios
kubectl rollout undo deployment/app1-dp
```

## SERVICES
```bash
kubectl get services
```

## NAMESPACES
```bash
kubectl get namespaces
kubectl get pods --all-namespaces
kubectl get pods --namespace=name
```

## CONFIGMAP
```bash
kubectl create configmap game-config --from-file=configmaptest
kubectl get configmap -o wide
kubectl get configmap game-config -o yaml
```

## SECRETS
```bash
echo -n 'admin' > ./username.txt 
echo -n '123456' > ./password.txt
kubectl create secret generic db-user-pass --from-file=username.txt --from-file=password.txt
kubectl get secrets

#encript and decript base64
kubernetes % echo -n 'admin' | base64
echo 'YWRtaW4=' | base64 --decode

#ver variables de secret en mypod
kubectl exec mypod -- ls /etc/foo
#ver detalle del secret en mypod
kubectl exec mypod -- cat /etc/foo/username

# ver env en modo
kubectl exec secret-env-pod -- env | grep SECRET

```

## PRUEBA
```bash
kubectl create namespace appvotacion
kubectl apply -f . --namespace=appvotacion
kubectl get deployments --namespace=appvotacion
kubectl get services --namespace=appvotacion
kubectl scale deployment vote --replicas=5 --namespace=appvotacion
kubectl scale deployment result --replicas=5 --namespace=appvotacion
kubectl delete all --all --namespace=appvotacion
 kubectl delete namespace appvotacion
```