1. Get Process

        Get-Process -Name "winword" | Select-String -Pattern Id
        Get-Process -Name "iisexpress"
        Get-Process

2. Stop Process use Name
   
        Stop-Process -Name "winword"
        Stop-Process -Name "iexplore"
        Stop-Process -Name "iisexpress"

3. Stop Process use Id
   
        taskkill /f /pid  43208

    <img src="killpid.png">

4. Add Content for File

        Add-Content -Path 'C:\log.txt' -Value 'test string'

5. Print

        Write-Host 'Hello, World!'

6. Try-Catch

        try { NonsenseString }
        catch { Write-Host "error: " + $_ }

7. How to find port pid

        netstat -ano | findstr :3000

    <img src="find_port_pid.png"> 

8. How to get powershell version?

        $PSVersionTable

9. How to get Environment Path in powershell.    

        $env:path


[authenticodesignature](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.security/set-authenticodesignature)