---
title: "[vscode] how to install c# extention in vscode"
categories:
  - vscode
tags:
  - vscode
  - c#
  - extention
  - dotnet
  - .net
  - install error
---


# Install C# Extention
Install c# extention in vscode for using c#.  
![set define on](/assets/images/install_cshap_extention.png)  



Install [.Net 6][install-dotnet6](or newer).  

That's required for c# extention.  
![set define on](/assets/images/cshap_extention_requirement.png)  
![set define on](/assets/images/cshap_extention_requirement_dotnet6.png)  



# Restart VSCode & Check Install C# Extention
Start vscode and open folder that's creating project namespace.   


Open terminal in vscode and typing 'dotnet --version'.   


If C# Extention installed perpectly that show information installed dotnet version.   
![set define on](/assets/images/check_vscode_install.png)  



# Accured Error (not found dotnet), Solved Error.

If Accured Error, not found dotnet, when check version.   
![set define on](/assets/images/vscode_install_error_not_found_dotnet.png)   


Typing bellow command on termial.  
```bash
sudo ln -s /usr/local/share/dotnet/x64/dotnet /usr/local/bin/
```
![set define on](/assets/images/vscode_install_error_not_found_solved.png)    


And Check install C# Extention. Typing 'dotnet --version' one more.  
![set define on](/assets/images/check_vscode_install.png)  



--- 
[install-dotnet6]:https://dotnet.microsoft.com/en-us/download/dotnet/6.0