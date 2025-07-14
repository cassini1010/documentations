# How HTTPS Works

## Handshake

| Client                                                                                | Server                                                                                                            |
| ------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------- |
| send a list of SSL/TLS versions and encryption algorithms that client can work with   |                                                                                                                   |
|                                                                                       | choose the best SSL/TLS version and encryption algorithm among the ones sent by client                            |
|                                                                                       | reply with certificate, which includes public key, so client can verify who I am.                                 |
| Verifies servers certificate to make sure its Legit.                                  |                                                                                                                   |
| Generate a symmetric Key and encrypt it with Servers Public Key and send it to server |                                                                                                                   |
|                                                                                       | Server decrypts the message using private key and finds symmetric key, and uses it for any further communication. |

## SSL/TLS

SSL protocol was created in the 90s. It is deprecated and is now evolved as TLS. So the names are used interchangably..

## Certificate Authorities

`Let's Encrypt` is one of the examples for a certificate authority (CA). Certificates are obtained by CA. 

Self-signed certificates also provide same level of secutiry as a certificate issued by CA. But browsers are designed to trust a certificate issued by trusted authority. Therefore even if self-signed certificate provide same level of security, they are not trusted by the browser.

| Self-signed certificate                       | CA signed certificate                                 |
| --------------------------------------------- | ----------------------------------------------------- |
| It says "Trust me, please! I promise its me!" | It says "Trust me! Im verified by trusted Authority!" |

Some of the popular CA are

- Symantec

- Comodo

- Let's Encrypt

Most of the time the certificate is signed by an Intermediate certificate which is signed by Root certificate.

### Steps Involved in Certificate Validation

- The browser connects to a site via HTTPS and downloads the site's certificate.

- If the downloaded certificate is not a root certificate, the browser attempts to download the intermediate certificate that was used to sign it.

- If the intermediate certificate is also not a root certificate, the browser tries to download the certificate that signed the intermediate certificate.

- The browser eventually finds the root certificate, which is issued by a trusted Certificate Authority (CA). As a result, it trusts the entire Certificate chain
