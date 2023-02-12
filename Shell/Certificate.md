  openssl s_client -showcerts -servername xxx.com -connect xxx.com:444
  
  no client certificate example:
  
  <img src="no_client_certificate.png">
  
Get the certificate expiry date

  openssl s_client -showcerts -servername xxx.com -connect xxx.com:444 | openssl x509 -noout -dates
  
