### 1. Overview

This is an example of using module `tls` in NodeJS to create a client securely connecting to a TLS server.

It is a modified version from [documentation about TLS](https://nodejs.org/api/tls.html), in which:
+ The server is a simple echo one. Clients connect to it, get the same thing back if they send anything to the server. 
+ The server is a TLS-based server. 
+ Clients somehow get the server's public key and use it to work securely with the server

### 2. Preparation

We need to generate keys & certs for the server. Pay attention to `Common Name (e.g. server FQDN or YOUR name)` when creating `server-csr.pem`. It should be your domain name.

```sh
$ mkdir tls
$ cd tls
$ openssl genrsa -out server-key.pem 4096
$ openssl req -new -key server-key.pem -out server-csr.pem
$ openssl x509 -req -in server-csr.pem -signkey server-key.pem -out server-cert.pem
```

For example:
```sh
$ openssl req -new -key server-key.pem -out server-csr.pem
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) [AU]:VN
State or Province Name (full name) [Some-State]:Hanoi
Locality Name (eg, city) []:Hanoi
Organization Name (eg, company) [Internet Widgits Pty Ltd]:Evolas Technologies
Organizational Unit Name (eg, section) []:
Common Name (e.g. server FQDN or YOUR name) []:evolastech.com
Email Address []:hi@evolastech.com

Please enter the following 'extra' attributes
to be sent with your certificate request
A challenge password []:
An optional company name []:
```

### 3. Run the demo

```sh
$ node server.js &
$ node client.js &
```

You may have following things printed out:

```text
server bound
server connected unauthorized
client connected authorized
welcome!
```