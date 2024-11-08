# Recon

### Recon - 0

Check robots.txt

### Recon - 1

Generate a 404 error page and check details

### Recon - 2

SECURITY.TXT File.

The security.txt file is used to tell security researchers how they can disclose vulnerabilities for a website. You can learn more about it here: [securitytxt.org](https://securitytxt.org/) and on Wikipedia: [Security.txt](https://en.wikipedia.org/wiki/Security.txt).

security.txt files can be served under the [`/.well-known/`](https://en.wikipedia.org/wiki/Well-known\_URI) directory (i.e. `/.well-known/security.txt`) or the top-level directory (i.e. `/security.txt`) of a website.

[http://hackycorp.com/.well-known/security.txt](http://hackycorp.com/.well-known/security.txt)

### Recon - 3

> goal is to find a directory with directory listing

access /images.

Indexing directory can be disabled on most webservers. For example, with Apache, you need to use the option: -Indexes.

### Recon - 4

> find a directory that is commonly used to manage applications

When accessing a new webserver, it often pays off to manually check for some directories before starting to brute force using a tool. For example, you can manually check for /admin/.

[http://hackycorp.com/admin/](http://hackycorp.com/admin/)

### Recon - 5

> goal is to find a directory that is not directly accessible.

When accessing a new webserver, it often pays off to brute force directories. To do this, you can use many tools like [patator](https://github.com/lanjelot/patator), [FFUF](https://github.com/ffuf/ffuf) or [WFuzz](https://wfuzz.readthedocs.io/en/latest/) (amongst many others).

```
wfuzz -c -z file,wordlist/general/common.txt --sc 200 http://hackycorp.com/FUZZ/
```

http://hackycorp.com/startpage

### Recon - 6

> goal is to access the default virtual host ("vhost").
>
>
>
> When accessing a new webserver, it often pays off to replace the hostname with the IP address or to provide a random Host header in the request. To do this, you can either modify the request in a web proxy or use:
>
> ```bash
> curl -H "Host: ...."
> ```

1. Use dig to check the ip of the target.
2. curl the ip using curl http://\<ip> -v

This will give us the default one.

[http://51.158.147.132/](http://51.158.147.132/)

### Recon - 7

> goal is to access the default virtual host ("vhost") over TLS.

```
curl https://hackycorp.com -H "Host: vhost"
```

### Recon - 8

> Aliases in TLS Connections
>
> When accessing a TLS server, it often pays off to check the content of the certificate used. It's common for TLS servers to have certificates that are valid for more than one name (named alternative names).&#x20;
>
> Looking for alternative names can be done in your client or by using openssl.

![](<../.gitbook/assets/image (10).png>)

### Recon - 9

> goal is to access the headers from responses
>
> When accessing a web server, it often pays off to check the responses' headers. It's common to find information around version and technologies used

We can use the flag "-v" for getting a verbose output of curl.

We can also use, --dump-header

### Recon - 10

> goal is to use visual reconnaissance. You will need to find the website with the key in red.
>
> For this challenge, the web applications are hosted under: 0x\["%02x"].a.hackycorp.com
>
>
>
> If you haven't done visual reconnaissance before, you can try to use the tool [Aquatone](https://github.com/michenriksen/aquatone) to get images that you can browse easily to find the right key.

```
for i in `seq 0 150`; do
printf "%02x.a.hackycorp.com\n" $i
done > hosts.txt
```

```
for i in `cat hosts.txt`;do
curl http://0x$i/logo.png -o $i.png
done
```

483f8b15-e4a8-4387-b052-4b2204c7eb69

### Recon - 11

> goal is to brute a virtual host.
>
>
>
> In this challenge, you need to brute force a virtual host by only manipulating the Host header. There is no DNS resolution setup for this host. Therefore you will need to target hackycorp.com and bruteforce the virtual host (that ends in .hackycorp.com).

```
```

