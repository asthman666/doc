1. Get Process

        Get-Process -Name "iisexpress"
        Get-Process -Name "*Wall*"
        Get-Process

        Get-Process -Id 12323

    1.1 Get Thread from Process

    [use-powershell-to-explore-process-threads-in-windows](https://devblogs.microsoft.com/scripting/use-powershell-to-explore-process-threads-in-windows/)

2. Stop Process use Name
   
        Stop-Process -Name "winword"
        Stop-Process -Name "iexplore"
        Stop-Process -Name "iisexpress"

3. How to find port pid

        netstat -ano | findstr :3000

    <img src="find_port_pid.png"> 

4. Stop Process use Id
   
        taskkill /f /pid  43208

    <img src="killpid.png">

5. Add Content for File

        Add-Content -Path 'C:\log.txt' -Value 'test string'

6. Print

        Write-Host 'Hello, World!'

7. Try-Catch

        try { NonsenseString }
        catch { Write-Host "error: " + $_ }

8. How to get powershell version?

        $PSVersionTable

9. How to get Environment Path in powershell.    

        $env:path

10. How to get all Environment variables in powershell.

        Get-ChildItem env:

11. Get the `dll` file full name

        [System.Reflection.AssemblyName]::GetAssemblyName("C:\Program Files (x86)\Microsoft Visual Studio\2019\Professional\Common7\IDE\CommonExtensions\Microsoft\SSRS\Neodynamic.ReportingServices.Barcode.dll").FullName

        Neodynamic.ReportingServices.Barcode, Version=5.0.2000.0, Culture=neutral, PublicKeyToken=c6b33c3093a0d4cd


[authenticodesignature](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.security/set-authenticodesignature)