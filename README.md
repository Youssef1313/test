---
title: "How to: Create localized exception messages"
description: "The article demonstrates how to create custom exceptions and localized exception messages"
author: "Youssef1313"
ms.date: 09/01/1999
---
# Create custom exceptions
The .NET Framework contains many different exceptions that are likely to happen. However, in some cases we need to create our own custom exceptions.
Let's assume you want to create a `StudentNotFoundException` that contains a `StudentName` property.
To create our custom exception, we follow these steps:

- Create a serializable class that inherits from `Exception`. The class name is preferred to end in "Exception".

```csharp
[Serializable]
public class StudentNotFoundException : Exception
{
    
}
```

- Add the default constructors.

```csharp
[Serializable]
public class StudentNotFoundException : Exception
{
    public StudentNotFoundException()
    {
    }

    public StudentNotFoundException(string message)
        : base(message)
    {
    }

    public StudentNotFoundException(string message, Exception inner)
        : base(message, inner)
    {
    }
}
```

- Add properties and/or more constructors depending on your needs.

```csharp
[Serializable]
public class StudentNotFoundException : Exception
{
    public string StudentName { get; }

    public StudentNotFoundException()
    {
    }

    public StudentNotFoundException(string message)
        : base(message)
    {
    }

    public StudentNotFoundException(string message, Exception inner)
        : base(message, inner)
    {
    }
	
    public StudentNotFoundException(string message, string studentName)
        : base(message)
    {
        StudentName = studentName;
    }
}
```

# Create localized exception messages
We have created our custom exception and we can throw it anywhere in our code like the following:

```csharp
throw new StudentNotFoundException("The student cannot be found.", "John");
```

The previous line looks good, but its only problem is that `The student cannot be found.` is just a constant string, we want to have different messages depending on user culture.
We will do that by using [Satellite Assemblies](https://docs.microsoft.com/dotnet/framework/resources/creating-satellite-assemblies-for-desktop-apps).

To start creating the localized exception messages:
- Create a new folder to hold the resource files, let's name the folder `Resources`.
- Add a new resource file to it. To do that in Visual Studio, Right click the folder in solution explorer -> Add -> New Item -> Choose `Resources File` -> Name it `ExceptionMessages.resx`.
- Add a Name Value pair for your exception messages like the following image shows:

![image](https://user-images.githubusercontent.com/31348972/64116635-28ce3500-cd93-11e9-953e-6cefea27804b.png)
