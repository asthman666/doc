## Verify the domain certificate

    echo | openssl s_client -connect xxx.com:443 -showcerts -verify 1

## Show the domain certificate

    echo | openssl s_client -showcerts -servername xxx.com -connect xxx.com:444

### example:

    openssl s_client -showcerts -servername www.amazon.com -connect www.amazon.com:443

### no client certificate example:

<img src="no_client_certificate.png">
  
## Get the certificate expiry date

    openssl s_client -showcerts -servername xxx.com -connect xxx.com:444 | openssl x509 -noout -dates
  
### example:

    openssl s_client -showcerts -servername www.amazon.com -connect www.amazon.com:443 | openssl x509 -noout -dates
