# Authentication

Services **SHOULD** support TLS authentication.

Services **MAY** support basic authentication.

```yaml
auth: 
  server: 
    tls:
      cert: /path/to/cert.pem
      key: /path/to/key.pem
      enabled: true
    basicAuth:
      username: user
      password: pass
      enabled: true
```
