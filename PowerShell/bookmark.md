 The aliases are stored as a hash table in a .PS1 file in $env:UserProfile

    PS C:\> Install-Module -Name PSBookmark

    PS C:\> Get-Command -Module PSBookmark -CommandType Alias

    #This will save $PWD as scripts
    PS C:\> save scripts 

    #This will save C:\Documents as docs
    PS C:\> save docs C:\Documents

    #You don't have to type the alias name. Instead, you can just tab complete. This function uses dynamic parameters.
    goto docs

    PS C:\> glb
    #Get all saved alias locations
    Name                           Value                                                                                           
    ----                           -----                                                                                           
    docs                           C:\Documents                                                                                                                                          
    oss                            C:\Documents\Github    

    #You don't have to type the alias name. Instead, you can just tab complete. This function uses dynamic parameters.
    PS C:\> rlb docs    

### **NOTE**:

If you have some permission issues, maybe need to run:

    Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Scope CurrentUser


[PSBookmark](https://github.com/rchaganti/PSBookmark)

[Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Scope CurrentUser](https://docs.microsoft.com/zh-cn/powershell/module/microsoft.powershell.core/about/about_execution_policies?view=powershell-7.2)