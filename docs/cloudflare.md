# Cloudflare Certificate Management

- buy a DNS name (gkcluster.org)
- create an A record with * pointing to your server's IP
- probably need to auto update that IP with https://dnsomatic.com/
- Go to TLS/SSL -> Origin Server -> Create Certificate -> Select the domain -> Create Certificate
- Download the certificate and key
- kubectl create secret tls tls-cloudflare --cert=cert.crt --key=private.key --namespace default
  - for each namespace, you need to create a secret

ingress then looks like this (for the echo service and subdomain):
```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: echo-ingress
  namespace: default
  annotations:
    kubernetes.io/tls-acme: "true"
spec:
  ingressClassName: nginx
  # ADD TLS #2
  tls:
    # Replace the domain below with your domain accordingly.
    - hosts:
        - echo.gkcluster.org
      secretName: tls-cloudflare
  rules:
    # Replace the domain below with your domain accordingly.
    - host: echo.gkcluster.org
      http:
        paths:
          - pathType: Prefix
            path: /
            backend:
              service:
                name: echo-service
                port:
                  number: 80
```
