# MASTER; Get token
kubeadm token list
# MASTER; If token expired, create a new one
kubeadm token create
# MASTER; Get ca-cert-hash
cat /etc/kubernetes/pki/ca.crt | openssl x509 -pubkey  | openssl rsa -pubin -outform der 2>/dev/null | \
   openssl dgst -sha256 -hex | sed 's/^.* //'
# WORKER; join cluster
kubeadm join --token <token> <control-plane-host>:<control-plane-port> --discovery-token-ca-cert-hash sha256:<hash>