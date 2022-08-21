# GOCSPD
![](https://img.shields.io/github/v/release/LeviMarvin/gocspd_pkg?display_name=tag&include_prereleases&style=for-the-badge)
![](https://img.shields.io/github/downloads/LeviMarvin/gocspd_pkg/total?style=for-the-badge)
![](https://img.shields.io/badge/GO%20VERSION-1.19-blueviolet?style=for-the-badge&logo=go)

OCSP Responder for CA. Developed in GoLang.

Now is using Go 1.19.

## Installation
1. Go to the GitHub [releases](https://github.com/LeviMarvin/gocspd/releases) page;
2. Download the version for your server;
3. Run it :)

## Usage
GOCSPD support HTTP OCSP request with POST and GET. 

To start, you should prepare an index file that recorded the certificate's status.
File format must be like the database of OpenSSL.
Example:
```text
V	511231235959Z		0B5C49F09295E869	unknown	/CN=XXX
R	420817235959Z	220818141852Z	5E1ACBC65BD25C5D	unknown	/CN=XXX
```
And you need an ocsp signing certificate for the responder.

**IMPORTANT!**
All certificate files must be encoded with PEM, All keys must are PKCS8 format and encoded with PEM.

When program is running, it will create a http handle for accepting OCSP requests and sending OCSP responses.
You can set binding IP by `-bind` arg to let it know what address should it listen. set listen port by `-port` arg.

**If you set a bind address, then the responder will ONLY accept request that sending to bind address.**
So the final location must be bind address.
For example the responder is running with this command:
```shell
./gocspd -bind <Public IP> -port 8888
```
If the client in local host sends a request to `http://127.0.0.1:8888/`, the responder will reject the connection.
Unless the client sends the request to `http://<Public IP>:8888/`. If your domain pointed to the bind address,
The connection will also be accepted.

More details please use `-help` for lookup.

## Default Situation
If you have not set all args, the responder will load undefined files from the path that showed by the table:

| The Arg | The Path      |
|---------|---------------|
| index   | index.txt     |
| ca      | ca.crt        |
| s_cert  | responder.crt |
| s_key   | responder.key |
| log     | gocspd.log    |
