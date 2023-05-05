---
title: "[vscode] how to create c# project in vscode"
categories:
  - vscode
tags:
  - vscode
  - c#
  - create project
  - dotnet
  - .net
---


# Open folder (folder is name using namespasename).

Open folder and terminal. And Typing bellow command.  

```bash
dotnet new console
```

It's mean that create console project on opened folder.  
![set define on](/assets/images/create_console_project.png)


---

# Build project 

Typing bellow command on terminal.  

```bash
dotnet run
```

![set define on](/assets/images/dotnet_run_1.png)

Display "Hollo World!" on terminal.  


Now. Changie code in project.cs file into bellow code.  
```c#
using System;

namespace  MyProject
{
    public class MyProject{
        static void Main(string[] args)
        {
            Console.WriteLine("Typing this.");
        }
    }   
}
```


Building project.   

![set define on](/assets/images/dotnet_run_2.png)