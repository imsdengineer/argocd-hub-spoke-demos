# Argo CD Setup

## Install Argo CD

```
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

## Run Argo CD in HTTP Mode(Insecure)

https://github.com/argoproj/argo-cd/blob/54f1572d46d8d611018f4854cf2f24a24a3ac088/docs/operator-manual/argocd-cmd-params-cm.yaml#L82

kubectl get cm -n argocd

## Edit the cm argocd-cmd-params-cm 

kubectl edit cm argocd-cmd-params-cm -n argocd

## Add an entry 
data:
   # Run server without TLS
  server.insecure: "false"

## Expose Argo CD Server Service in NodePort Mode

```
kubectl edit svc argocd-server -n argocd
```

and change the type to NodePort from ClusterIP

## Get the inital password from the secret

kubectl get secrets -n argocd

## Convert into base64

echo '####' | base64 --decode

