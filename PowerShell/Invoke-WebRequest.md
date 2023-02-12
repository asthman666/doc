  
# Set the SSL version
    
    [Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
  
# Request a url

    Invoke-WebRequest [url]

    Invoke-WebRequest https://www.baidu.com

