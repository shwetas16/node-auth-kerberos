# node-auth-kerberos
Node.js native addon for simple Kerberos 5 user authentication based on the older node-krb5 module. Updated to support Node 8.x, fixed spoofing vulnerability.

The module currently builds on linux with krb5 headers and libs (tested on centos) and windows (tested on windows 8.1 with MIT Kerberos)

The older node-krb5 module was tested on OSX, so give it a shot!

Updates:
Support for Node 8.x 
Verification of KDC once the credentials are supplied

More info from MIT on the vulnerability that was fixed in this version:
Whenever a program grants access to a resource (such as a local login session on a desktop computer) based on a user successfully getting initial Kerberos credentials, it must verify those credentials against a secure shared secret (e.g., a host keytab) to ensure that the user credentials actually originate from a legitimate KDC. Failure to perform this verification is a critical vulnerability, because a malicious user can execute the “Zanarotti attack”: the user constructs a fake response that appears to come from the legitimate KDC, but whose contents come from an attacker-controlled KDC.

Credits:
https://github.com/qesuto/node-krb5
https://github.com/qesuto/node-krb5/pull/17



Installation
------------

Install the required Linux header libraries needed for install if nessecary:
``` bash
$ sudo apt install -y libkrb5-dev 
```
or
``` bash
$ sudo yum install -y krb5-devel
```

You can install with `npm`:

``` bash
$ npm install -g node-auth-kerberos
```

On windows you will need to have MIT Kerberos (http://web.mit.edu/Kerberos/dist/) installed.

You will also need to set the environment variable MITKRB5 to the MIT Kerberos home. 

```
set MITKRB5=C:\Program Files\MIT\Kerberos
```

How to Use
----------

``` js
const kerberos = require('node-auth-kerberos');

kerberos.authenticate('username@REALM', 'password', function(err) {
  if (err) {
    console.log("Error: " + err);
  } else {
    console.log("OK");
  }
});
```
