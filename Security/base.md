# base kb

## TLS

**Transport Layer Security(TLS)**, and its now-deprecated predecessor, **Secure Sockets Layer(SSL)**, are **cryptographic protocols** designed to provide communications security over a computer network

Because HTTPS piggybacks HTTP entirely on top of TLS, the entirety of the underlying HTTP protocol can be encrypted. This includes the **request URL** (which particular web page was requested), **query parameters**, **headers**, and **cookies** (which often contain identity information about the user). However, because host (website) addresses and port numbers are necessarily part of the underlying TCP/IP protocols, HTTPS cannot protect their disclosure. In practice this means that even on a correctly configured web server, eavesdroppers can infer the IP address and port number of the web server (sometimes even the domain name e.g. www.example.org, but not the rest of the URL) that one is communicating with, as well as the amount (data transferred) and duration (length of session) of the communication, though not the content of the communication.

> [TLS 1.1](https://www.ietf.org/rfc/rfc4346.txt)

> [TLS 1.2](https://tools.ietf.org/html/rfc5246)

> [TLS 1.3](https://tools.ietf.org/html/rfc8446)

> [The TLS Handshaking Protocols](https://tools.ietf.org/html/rfc5246#section-7)

* test tls handshake time

        curl -w "TCP handshake: %{time_connect}, SSL handshake: %{time_appconnect}\n" -so /dev/null https://www.baidu.com


## HTTPS

**Hypertext Transfer Protocol Secure(HTTPS)** is an extension of the **HTTP**, the communication protocol is encrypted using **TLS**. The protocol is therefore also often referred to as **HTTP over TLS**, or **HTTP over SSL**

> [are https url encrypted](https://stackoverflow.com/questions/499591/are-https-urls-encrypted)

> [TLS协议的运行机制](http://www.ruanyifeng.com/blog/2014/02/ssl_tls.html)

> [TLS延迟有多大](http://www.ruanyifeng.com/blog/2014/09/ssl-latency.html)