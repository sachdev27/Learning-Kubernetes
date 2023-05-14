# Certificates Renewal


## 1. Checking the expiry date of the certificates using kubeadm

```bash
kubeadm certs check-expiration
```

### using openssl

```bash
openssl x509 -in /etc/kubernetes/pki/apiserver.crt -text -noout
```


## 2. Renewing the certificates using kubeadm

```bash
kubeadm alpha certs renew all
```

### for single certificate

```bash
kubeadm alpha certs renew apiserver
```


## 3. Restarting the control plane components

```bash
systemctl restart kube-apiserver && systemctl restart kube-controller-manager && systemctl restart kube-scheduler
```

## 4. Restarting the kubelet service

```bash
systemctl restart kubelet
```

## 5. Restarting the kube-proxy service

```bash
systemctl restart kube-proxy
```


