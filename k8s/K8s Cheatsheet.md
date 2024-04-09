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