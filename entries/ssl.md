## How to generate a self-signed certificate

```
openssl genrsa -out my-cert.key 2048
openssl req -new -x509 -days 3650 -key my-cert.key -out my-cert.crt
```

## How to generate a certificate

Generate key
```
openssl genrsa -out client1.key 2048
```

Generate certificate sign request
```
openssl req -new -key client1.key -out client1.csr
```

The csr should either be sent to the CA or self signed.

To sign request with <YOUR> CA.
```
openssl x509 -req -in client1.csr -out client1.crt -sha1 -CA <your>_ca.crt -CAkey <your>_ca.key -CAcreateserial -days 365
```

## Verifying SSL email address

SSL companies need to validate that you own a domain, but you don't want to pay for email service just to receive one email. Here is how you can configure postfix to receive email for admin@example.com

*(don't use example.com unless you own that domain)*

1. Create an admin user.

```sudo adduser admin```

2. Tell postfix what domains you want to use.

```sudo postconf -e "mydestination = example.com"```

3. Tell postfix to listen on internet

```sudo postconf -e "inet_interfaces = all"```

4. Restart postfix

```sudo service postfix restart```

Now you can receive email at admin@example.com

type: ```mail``` when logged into the admin user to check email.

UPDATE: check out http://www.binarytides.com/postfix-mail-forwarding-debian/

## NGINX Chained certificates

*Problem:* Apache allows you to declare an intermediate SSL certificate, but Nginx does not. Instead, nginx wants you to mush all your certs together.

```
cp example_com.crt example_com.chained.crt
cat AddTrustExternalCARoot.crt >> example_com.chained.crt
cat COMODORSAAddTrustCA.crt >> example_com.chained.crt
cat COMODORSADomainValidationSecureServerCA.crt >> example_com.chained.crt
```

Shorthand for the above is like this:

```
cp example_com{,.chained}.crt &&
cat AddTrustExternalCARoot.crt COMODORSAAddTrustCA.crt COMODORSADomainValidationSecureServerCA.crt >> example_com.chained.crt
```
