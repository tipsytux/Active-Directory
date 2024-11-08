# API

## API - 01

* Use a proxy tool to view all the requests, check all requests
* Observe that we can get the secret without auth.

## API - 02

* In this one, they check if we have access to the resource
* So use JWT Attack to change the alg to none, and boom.
* The application does not check if the signature is valid.

## API - 03

Note that JWT Signatures can be cracked.

```
hashcat -m 16500 jwt.txt /opt/wordlists/rockyou.txt
```

![](<../.gitbook/assets/image (3).png>)

Then use jwt.io to create a new JWT.

## API - 04

* This was based on the source code. Look at the Javascript file and see what endpoints are being called.

## API - 05

* This is source code review again, but the JS was not pretty.

```
curl -X POST https://ptl-3e5896d3-43baf810.libcurl.so/get_more_secret
```

## API - 06

This time it was the same thing, but the only thing was that it was compressed.

## API - 07

It is important to view the templates that are added as part of the Javascript.

## API - 08

Check response of alll requests. Was able to get the link in response.

## Mongo IDOR

Simple. Check id, query id. Get the key.











