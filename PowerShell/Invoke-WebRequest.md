  
# Set the SSL version
    
    [Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
  
# Request a url

    Invoke-WebRequest [url]

    Invoke-WebRequest https://www.baidu.com

# Print response XML body

    $response = Invoke-RestMethod 'https://www.w3schools.com/xml/plant_catalog.xml' -Method 'GET'    
    Write-Host $response.OuterXml
