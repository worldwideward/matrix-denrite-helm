# Matrix + Element

This helm chart deploys matrix + element (the web ui) on a kubernetes cluster.

## Important values

To make your Matrix deployment reachable from the internet, make sure you correctly configure the ingresses.

```
# my-values.yaml

ingress:
  enabled: true
  annotations: 
    kubernetes.io/ingress.class: nginx
    kubernetes.io/tls-acme: "true"
    cert-manager.io/cluster-issuer: "letsencrypt"
    acme.cert-manager.io/http01-edit-in-place: "true"
  hosts:
    - host: dendrite.example.com
      paths: 
      - path: "/"
  tls: 
  - secretName: dendrite-tls
    hosts:
    - dendrite.example.com

element:
  homeserver_url: dendrite.example.com
  ingress:
    enabled: true
    annotations:
      kubernetes.io/ingress.class: nginx
      kubernetes.io/tls-acme: "true"
      cert-manager.io/cluster-issuer: "letsencrypt"
      acme.cert-manager.io/http01-edit-in-place: "true"
    hosts:
      - host: chat.example.com
        paths:
        - path: "/"
    tls:
    - secretName: element-tls
      hosts:
      - chat.example.com

```
