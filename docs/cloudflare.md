# Cloudflare Certificate Management

- buy a DNS name (gkcluster.org)
- create an A record with echo.gkcluster.org pointing to your server's IP
  - idea being that I don't want to route everything as I'll want local only for dashboard.gkcluster.org etc.
  - BUT is this secure? can someone still go direct to the IP, bypass the DNS and add a host header?
  - my router is set to only allow 443,80 to the server.
  - cloudflare does not expose my IP as it is proxied.
  - Do I also need firewalld to block traffic not proxied through cloudflare? Or is that overkill?
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
## notes

This can get to the echo service - try to use commands like this to test the theory that attackers can bypass the DNS and go direct to the IP:
```bash
curl "Host: echo.gkcluster.org" https://echo.gkcluster.org
```

# this fails which I think is good?
```bash
# curl --insecure "Host: echo.gkcluster.org" https://90.243.208.136                                                                [9:59:09]
curl: (3) URL using bad/illegal format or missing URL
<html>
<head><title>404 Not Found</title></head>
<body>
<center><h1>404 Not Found</h1></center>
<hr><center>nginx</center>
</body>
</html>
```
