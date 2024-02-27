[.Net](https://fr.wikipedia.org/wiki/Microsoft_.NET):
- [.Net Framework](https://fr.wikipedia.org/wiki/Framework_.NET)
  - library
    - [base class library](https://fr.wikipedia.org/wiki/Base_Class_Library)
    - XML Web Services and Web Forms (ASP.Net)
    - Windows Forms
  - Common Language Runtime (VM)
- languages
  - C#
  - VB

- [Introduction to the C# Language and the .NET Framework | Microsoft Docs](https://docs.microsoft.com/en-us/dotnet/csharp/getting-started/introduction-to-the-csharp-language-and-the-net-framework)
- [| C# Online Compiler | .NET Fiddle](https://dotnetfiddle.net/)

Convert VB.Net to C#:

- [How to: Declare an Object by Using an Object Initializer - Visual Basic | Microsoft Docs](https://docs.microsoft.com/en-us/dotnet/visual-basic/programming-guide/language-features/objects-and-classes/how-to-declare-an-object-by-using-an-object-initializer)
- [c# - What's the equivalent VB.NET syntax for anonymous types in a LINQ statement? - Stack Overflow](https://stackoverflow.com/questions/3142225/whats-the-equivalent-vb-net-syntax-for-anonymous-types-in-a-linq-statement/32283458#32283458)
- [Comparison of C Sharp and Visual Basic .NET - Wikipedia](https://en.wikipedia.org/wiki/Comparison_of_C_Sharp_and_Visual_Basic_.NET)
- [Convert VB.NET to/from C# online](https://codeconverter.icsharpcode.net/) - [Roslyn Code Converter - icsharpcode/CodeConverter: Convert code from C# to VB.NET and vice versa using Roslyn](https://github.com/icsharpcode/CodeConverter/)
- [Code Converter C# to VB and VB to C# – Telerik](https://converter.telerik.com/)
- [CodeTranslator: Code Translation From VB.NET <-> C# <-> TypeScript <-> Java](https://www.carlosag.net/tools/codetranslator/)
- [Source Code Converters](https://www.tangiblesoftwaresolutions.com/)
- [VB.NET and C# Equivalents](https://www.tangiblesoftwaresolutions.com/vb-and-csharp-equivalents.html)

.NET Framework:

- [Reference Source](https://referencesource.microsoft.com/)

ASP.NET MVC (and WebForms, but not Core):

- [aspnet/AspNetWebStack: ASP.NET MVC 5.x, Web API 2.x, and Web Pages 3.x (not ASP.NET Core)](https://github.com/aspnet/AspNetWebStack)
- [.NET API browser | Microsoft Docs](https://docs.microsoft.com/en-us/dotnet/api/?view=aspnet-mvc-5.2)

ASP.NET Core:

- [dotnet/aspnetcore: ASP.NET Core is a cross-platform .NET framework for building modern cloud-based web applications on Windows, Mac, or Linux.](https://github.com/dotnet/aspnetcore)
- [.NET API browser | Microsoft Docs](https://docs.microsoft.com/en-us/dotnet/api/?view=aspnetcore-3.1)
- [Source Browser](https://source.dot.net/)

## Debug

- Windows application: Event Viewer
- [dnSpy/dnSpy: .NET debugger and assembly editor](https://github.com/dnSpy/dnSpy) - debug process, assembly browser
	- breakpoint:
		1. start dnSpy as admin
		2. menu "Debug" -> "Attach to process"
		3. select `w3wp.exe`
		4. menu "Debug" -> "Windows" -> "Modules" to see all loaded assemblies
	- if local variables didn't show (JIT optimization):
		- by updating assembly attributes: [hacktricks/reversing.md at master · carlospolop/hacktricks](https://github.com/carlospolop/hacktricks/blob/master/exploiting/reversing.md#dnspy-debugging) - [Reversing - HackTricks](https://web.archive.org/web/20201118144644/https://book.hacktricks.xyz/exploiting/reversing#dnspy-debugging)
			```csharp
			[assembly: Debuggable(DebuggableAttribute.DebuggingModes.Default |
			DebuggableAttribute.DebuggingModes.DisableOptimizations |
			DebuggableAttribute.DebuggingModes.IgnoreSymbolStoreSequencePoints |
			DebuggableAttribute.DebuggingModes.EnableEditAndContinue)]
			```
		- For ASP.Net, set `configuration/system.web/compilation/@debug` to `true` (`Web.config`) to disable execution optimizations (see also `@optimizeCompilations`, set to `false`) (only for generated code?)
		- by use ini file or registry:
			- set the environment variable `COMPLUS_ZAPDISABLE=1`  or the registry key `HKLM\SOFTWARE\Microsoft\.NETFramework\ZapDisable`

			For ASP.Net, set `system.web/hostingEnvironment/@shadowCopyBinAssemblies` to `false` (`Web.config`) to disable shadow copies of DLLs (in a tmp dir)

			For the DLL `somelib.dll` create a `somelib.ini` with:
			```ini
			[.NET Framework Debugging Control]
			GenerateTrackingInfo=1
			AllowOptimize=0
			```

		- [Making an Image Easier to Debug · dnSpy/dnSpy Wiki](https://github.com/dnSpy/dnSpy/wiki/Making-an-Image-Easier-to-Debug)
		- [dnSpy - A Fantastic .NET Debugger](https://web.archive.org/web/20200129155827/http://omnine.blogspot.com/2016/11/dnspy-fantastic-net-debugger.html#!http://web.archive.org/web/20201120101936/http://omnine.blogspot.com/2016/11/dnspy-fantastic-net-debugger.html)
		- [Easily debug Sitecore assemblies using dnSpy](https://web.archive.org/web/20201107225457/https://blog.richardszalay.com/2019/06/14/debugging-sitecore-assemblies/)
		- [Making an image easier to debug in .NET | Microsoft Docs](https://web.archive.org/web/20201120104100/https://docs.microsoft.com/en-us/dotnet/framework/debug-trace-profile/making-an-image-easier-to-debug?redirectedfrom=MSDN)
		- [fgreinacher/nooptimize: A tiny command line tool that allows you to disable JIT optimization for a given set of .NET assemblies.](https://github.com/fgreinacher/nooptimize) - Create a ini file for all assemblies

		- [.net - How can I disable compiler optimization in C#? - Stack Overflow](https://stackoverflow.com/questions/1199204/how-can-i-disable-compiler-optimization-in-c)
		- [dotnet/testing-with-ryujit.md at 2ab884e04a0a40c84dcb8782033b2191b7a94fd4 · microsoft/dotnet](https://github.com/microsoft/dotnet/blob/2ab884e04a0a40c84dcb8782033b2191b7a94fd4/Documentation/testing-with-ryujit.md)
- [ProcDump - Windows Sysinternals | Microsoft Docs](https://docs.microsoft.com/en-us/sysinternals/downloads/procdump) - generate process dump
- WinDbg - load process dump

## Decompiler

- [ILSpy](http://ilspy.net/) [icsharpcode/ILSpy: .NET Decompiler](https://github.com/icsharpcode/ILSpy)
	[ILSpy/ICSharpCode.Decompiler.Console at master · icsharpcode/ILSpy](https://github.com/icsharpcode/ILSpy/tree/master/ICSharpCode.Decompiler.Console)
	[docs/using-on-macos.md at master · dotnet/docs](https://github.com/dotnet/docs/blob/master/docs/core/tutorials/using-on-macos.md)
- [dotPeek: Free .NET Decompiler & Assembly Browser by JetBrains](https://www.jetbrains.com/decompiler/)
	[Download dotPeek: Free .NET Decompiler by JetBrains](https://www.jetbrains.com/decompiler/download/#section=standalone)
	Wine: need dotnet45 + Windows NT 6.0+ (Vista+)
- [.NET Decompiler: Decompile Any .NET Code | .NET Reflector](https://www.red-gate.com/products/dotnet-development/reflector/)
- [0xd4d/de4dot: .NET deobfuscator and unpacker.](https://github.com/0xd4d/de4dot)
- [wildcardc/cfxc-deobf: A ConfuserEx-custom deobfuscation toolchain](https://github.com/wildcardc/cfxc-deobf)
- [ViRb3/de4dot-cex: de4dot deobfuscator with full support for vanilla ConfuserEx](https://github.com/ViRb3/de4dot-cex)

## Attributes

- [Extending Metadata Using Attributes | Microsoft Docs](https://docs.microsoft.com/en-us/dotnet/standard/attributes/)
- [c# - How to pass objects into an attribute constructor - Stack Overflow](https://stackoverflow.com/questions/1235617/how-to-pass-objects-into-an-attribute-constructor)
- [c# - Lambda expression in attribute constructor - Stack Overflow](https://stackoverflow.com/questions/16809294/lambda-expression-in-attribute-constructor)
- [c# - Attribute with action/condition - Stack Overflow](https://stackoverflow.com/questions/21902812/attribute-with-action-condition)

## Compilation

- [MichalStrehovsky/zerosharp: Demo of the potential of C# for systems programming with the .NET native ahead-of-time compilation technology.](https://github.com/MichalStrehovsky/zerosharp)

## Language version

- [C# language versioning - C# Guide - C# | Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/configure-language-version)
- [.net - What are the correct version numbers for C#? - Stack Overflow](https://stackoverflow.com/questions/247621/what-are-the-correct-version-numbers-for-c/38506668#38506668)

## Documentation comments

- [Documentation comments - C# language specification | Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/language-specification/documentation-comments)
- [Recommended XML documentation tags for a class and its members - C# | Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/xmldoc/recommended-tags)
- [c# - How to reference generic classes and methods in xml documentation - Stack Overflow](https://stackoverflow.com/questions/532166/how-to-reference-generic-classes-and-methods-in-xml-documentation/41208166#41208166) - `cref` attribute
- [Documentation comments - document APIs using /// comments - C# | Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/xmldoc/)
- [C# XML Documentation Website Link - Stack Overflow](https://stackoverflow.com/questions/6960426/c-sharp-xml-documentation-website-link)

##

- [Understanding Async, Avoiding Deadlocks in C# | by Eke Péter | Rubrikk Group | Medium](https://medium.com/rubrikkgroup/understanding-async-avoiding-deadlocks-e41f8f2c6f5d)
- [Why is .GetAwaiter().GetResult() bad in C#?](https://www.nikouusitalo.com/blog/why-is-getawaiter-getresult-bad-in-c/)
- [C# - Handling exceptions from Tasks that are not awaited](https://peterdaugaardrasmussen.com/2021/06/05/dot-net-catching-exceptions-in-unawaited-tasks/)
