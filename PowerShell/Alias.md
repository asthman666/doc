# $PSHOME/profile.ps1 or $PROFILE.AllUsersAllHosts for all users

    function Open-Configuration { C:\Windows\notepad.exe $PSHOME/profile.ps1 }
    
    function Open-Hosts { C:\Windows\notepad.exe C:\Windows\System32\drivers\etc\hosts }
    
    function Goto-Src { cd C:\src }
    
    Set-Alias -Name conf -Value "Open-Configuration"
    Set-Alias -Name hosts -Value "Open-Hosts"
    Set-Alias -Name src -Value "Goto-Src"


# Useful command

    alias | ? {$_.Name -like 'src'}  

[how-to-create-permanent-powershell-aliases](https://stackoverflow.com/questions/24914589/how-to-create-permanent-powershell-aliases)
[how to edit a profile](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_profiles?view=powershell-7.3#how-to-edit-a-profile)
