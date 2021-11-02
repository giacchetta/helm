# OpenSearch with TLS (Production)

1. `$ openssl genrsa -out root-ca-key.pem 2048`
2. `$ openssl req -new -x509 -sha256 -key root-ca-key.pem -out root-ca.pem -days 730 -subj "/C=CA/ST=ONTARIO/L=TORONTO/O=ORG/OU=UNIT/CN=Root"`

3. `$ openssl genrsa -out admin-key-temp.pem 2048`
4. `$ openssl pkcs8 -inform PEM -outform PEM -in admin-key-temp.pem -topk8 -nocrypt -v1 PBE-SHA1-3DES -out admin-key.pem`
5. `$ openssl req -new -key admin-key.pem -out admin.csr -subj "/C=CA/ST=ONTARIO/L=TORONTO/O=ORG/OU=UNIT/CN=admin"`
5. `$ openssl x509 -req -in admin.csr -CA root-ca.pem -CAkey root-ca-key.pem -CAcreateserial -sha256 -out admin.pem -days 730`

7. `$ openssl genrsa -out node-key-temp.pem 2048`
8. `$ openssl pkcs8 -inform PEM -outform PEM -in node-key-temp.pem -topk8 -nocrypt -v1 PBE-SHA1-3DES -out node-key.pem`
9. `$ openssl req -new -key node-key.pem -out node.csr -subj "/C=CA/ST=ONTARIO/L=TORONTO/O=ORG/OU=UNIT/CN=node"`
10. `$ openssl x509 -req -in node.csr -CA root-ca.pem -CAkey root-ca-key.pem -CAcreateserial -sha256 -out node.pem -days 730`

11. `$ rm *-temp.pem *.csr`