This repo is to demonstrate streaming HTML with HTTP/2 and with compression.

## How to run repo

Setup certificate first:

```sh
mkdir certs
cd certs
openssl genrsa -out CA.key -des3 2048
openssl req -x509 -sha256 -new -nodes -days 3650 -key CA.key -out CA.pem
touch localhost.ext
```

Add following to localhost.ext
```
authorityKeyIdentifier = keyid,issuer
basicConstraints = CA:FALSE
keyUsage = digitalSignature, nonRepudiation, keyEncipherment, dataEncipherment
subjectAltName = @alt_names

[alt_names]
DNS.1 = localhost
IP.1 = 127.0.0.1
```

Continue:
```sh
openssl genrsa -out localhost.key -des3 2048
openssl req -new -key localhost.key -out localhost.csr
openssl x509 -req -in localhost.csr -CA CA.pem -CAkey CA.key -CAcreateserial -days 3650 -sha256 -extfile localhost.ext -out localhost.crt
```

Rest of setup (with npm or pnpm):
```
npm i -g nodemon
npm i
```

Start server:
```
npm run dev
```