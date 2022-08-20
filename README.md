# GOCSPD
OCSP Responder for CA. Developed in GoLang.

Now is using Go 1.19

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
All certificate files must be encoded with PEM, All keys must is PKCS8 format and encoded with PEM.

When program is running, it will create a http handle for accepting OCSP requests and sending OCSP responses.
You can set binding IP by `-bind` arg to let it know what address should it listen. set listen port by `-port` arg.

More details please use `-help` for lookup.