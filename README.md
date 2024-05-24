# "Sealed Secrets" for Kubernetes

get own certs and apply https://github.com/bitnami-labs/sealed-secrets/issues/1232#issuecomment-1641941631

 kubectl create secret tls $SECRET_NAME --cert=$SEAL_PUB --key=$SEAL_PRIV -n sealed-secrets

 kubectl label secret $SECRET_NAME "sealedsecrets.bitnami.com/sealed-secrets-key=active" --overwrite -n sealed-secrets

kubectl -n ingress-nginx  create secret tls ssl-ingress-secret  --key=./TLSnewCert.pem --cert=./TLSnewCert.crt --dry-run=client -o yaml > infrastructure/dev/ingress-nginx/sealed-secret-main.yaml


cat infrastructure/dev/ingress-nginx/sealed-secret-main.yaml | kubeseal  --controller-name sealed-secrets --controller-namespace sealed-secrets -o yaml > infrastructure/dev/ingress-nginx/sealed-secret.yaml