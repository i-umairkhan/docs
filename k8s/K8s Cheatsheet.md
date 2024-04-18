- Importent paths.
```
/etc/kubernetes/
/etc/kubernetes/mainfests/
/var/lib/kubelet/
```
- To list down all API resources in kubernates.
```
kubectl api-resources
```
- List linux services assosiated with kubernates.
```
sudo systemctl list-units --all --type service | grep kube
```
- Check status of kubelet.
```
sudo systemctl status kubelet.service
```
- Create a pod declaratively.
```
kubectl run pod-name --image nginx --dry-run=client -o yaml > pod-name.yaml
kubectl apply -f pod-name.yaml
```
- List all resources in a cluster across all namespaces.
```
kubectl get all -A
```
- Get IP of pods in kube-system namespace.
```
kubectl get pods -n kube-system -o wide
```
- View kubelet client certificate.
```
openssl x509 -in /var/lib/kubelet/pki/kubelet-client-current.pem -text -noout
```
- Create and get service account, role, rolebinding.
```
kubectl create sa admin-user
kubectl create role admin --verb=create --resource=sa
kubeclt create rolebinding admin-binding --role=admin --service-account=admin-user
kubectl get role,rolebinding

kubectl auth can-i create sa --as=system:serviceaccount:default:admin-user
```
- Create and get clusterrole, clusterrolebinding.
```
kubectl create clusterrole admin --verb create --resource deploy
kubectl -n default create clusterrolebinding admin-role-binding --clusterrole admin --serviceaccount default:admin-user

kubectl auth can-i create ds --namespace default --as=system:serviceaccount:default:admin-user
```
- Upgrade kubeadm cluster.
```
kubeadm version -o json 
kubeadm upgrade plan
sudo apt install -y kubeadm=1.29.3-1.1
kubeadm upgrade apply v1.29.3
```
- Service account for pod without exposing service account token to pod.
```
kubectl -n default create sa admin-acc --dry-run client -o yaml > sa.yaml
echo "automountServiceAccountToken: false" >> sa.yaml
kubectl apply -f sa.yaml

vi pod.yaml
_______________
apiVersion: v1
kind: Pod
metadata:
  name: secure-pod
spec:
  serviceAccountName: secure-sa
  containers:
  - image: nginx
    name: secure-pod
_______________

kubectl apply -f pod.yaml
kubectl exec secure-pod -- cat /var/run/secrets/kubernetes.io/serviceaccount/token
```
- Applying taints on nodes and tolarations on pods.
```
kubectl describe node node01 | grep Taints

kubectl taint nodes node01 gpu=true:NoSchedule

vi pod.yaml
_________
apiVersion: v1  
kind: Pod  
metadata:  
  name: gpu-pod  
spec:  
  containers:  
  - name: my-app  
    image: my-app-image  
  tolerations:  
  - key: "gpu"  
    value: "Exists"  
    effect: "NoSchedule"
_________

kubectl apply -f pod.yaml
```
- Backup etcd.
```
/etc/kubernetes/pki/etcd
```

```
export ETCDCTL_API=3
```