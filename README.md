# emqx-dev


## emqx mqtts cert

```sh
mkdir emqx_certs && cd emqx_certs

# Generate CA key and cert
openssl req -x509 -newkey rsa:2048 -keyout ca.key -out ca.crt -days 365 -nodes -subj "/CN=EMQX CA"

# Generate server key and CSR
openssl req -newkey rsa:2048 -keyout server.key -out server.csr -nodes -subj "/CN=localhost"

# Sign server cert with CA
openssl x509 -req -in server.csr -CA ca.crt -CAkey ca.key -CAcreateserial -out server.crt -days 365
```

## emqx mqtts client cert

```sh
cd emqx_certs

# 1. Generate client key and CSR (Certificate Signing Request)
openssl req -newkey rsa:2048 -nodes -keyout client.key -out client.csr -subj "/CN=mqtt_client"

# 2. Sign the client cert using the CA cert
openssl x509 -req -in client.csr -CA ca.crt -CAkey ca.key -CAcreateserial -out client.crt -days 365
```