# ACME Runner

This is a docker image that will provide you the means to get certificates from Lets Encrypt for the box you run it from.
This is useful so you don't have to implement the ACME endpoint in your production codebase.

# How To Use

1. Pull the acme-runner image into the machine you want certificates for
```
docker pull csueiras/acme-runnner
```
2. Run: 
```
docker run -it -v $(pwd):/acme-runner/certificates \
    -p 8080:8080 \
    csueiras/acme-runner:0.1.0 \
    --server.port=8080 \
    --acme.endpoint=acme://letsencrypt.org/staging \
    --acme.domain-name=dev.mydomain.com \
    --acme.key-store-password="MyPassword"
```

## Ngrok

I personally use this to provision certificates for domains that I use for development through ngrok. This is how you
can use it yourself. 

1. Start the ngrok tunnel, for example with your own domain name
```
ngrok http -hostname=dev.mydomain.com 8080
```
2. Run acme-runner
```
docker run -it -v $(pwd):/acme-runner/certificates \
    -p 8080:8080 \
    csueiras/acme-runner:0.1.0 \
    --server.port=8080 \
    --acme.endpoint=acme://letsencrypt.org/staging \
    --acme.domain-name=dev.mydomain.com \
    --acme.key-store-password="KeyStorePasswordForMyDomain"
```
3. Done! You should have all of the files you need sitting in the directory you mounted into the container (current directory in this example)