# Helm Chart for Istio demo app bookinfo

## Prerequisites
The rest of the docutment assumes you have Istio installed for you Kubernetes cluster.
If you're using minikube, use the following as a reference.

### Start miniku
```
minikube start --memory=8192 --cpus=4 --kubernetes-version=v1.10.0 \
    --extra-config=controller-manager.cluster-signing-cert-file="/var/lib/localkube/certs/ca.crt" \
    --extra-config=controller-manager.cluster-signing-key-file="/var/lib/localkube/certs/ca.key" \
    --vm-driver=virtualbox
```

### Get your Gateway URL
```
export INGRESS_HOST=$(minikube ip)
export INGRESS_PORT=$(kubectl -n istio-system get service istio-ingressgateway -o jsonpath='{.spec.ports[?(@.name=="http2")].nodePort}')
export GATEWAY_URL=$INGRESS_HOST:$INGRESS_PORT
```

## Login to Quay registry
`helm registry login -u $USERNAME quay.io`

## Install bookinfo
`helm registry install quay.io/jackzzj/bookinfo`

You have your bookinfo available at http://$GATEWAY_URL/productpage