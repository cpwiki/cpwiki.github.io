---
title: C# Environment Setup for Linux(deb) Users
tags: [C#,C-Sharp,Linux,Terminal,Mono]
---
### Install Compiler
Open the terminal and execute the following command,
```console
sudo apt install mono-complete
```

### C# Example
Create a file named **test.cs** with the following content and save the file.
```csharp
using System;

public class Hello {

	static public void Main()
	{
		Console.WriteLine("Hello World!");
		Console.ReadKey();
	
	}
}
```

### Build and Run
Open the terminal in the same folder/directory that contains our **test.cs** example file. Then execute the following command to set the apropreate permission.
```console
sudo chmod +x test.cs
```
To build the **test.exe** executable file,
```console
mcs -out:test.exe test.cs
```
To run the **test.exe** executable file,
```console
mono test.exe
```

### Output
```console
Hello World!
```

Happy Coding!
