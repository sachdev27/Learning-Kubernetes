# Certificates Renewal


## 1. Checking the expiry date of the certificates using kubeadm

```bash
kubeadm certs check-expiration
```

## 2. Renewing the certificates using kubeadm

```bash
kubeadm alpha certs renew all
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


