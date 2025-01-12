- [msdeploy - How to find if file exist with msbuild command(or before) - Stack Overflow](https://stackoverflow.com/questions/37416230/how-to-find-if-file-exist-with-msbuild-commandor-before)
- [visual c++ - msbuild, how to set environment variables? - Stack Overflow](https://stackoverflow.com/questions/14267938/msbuild-how-to-set-environment-variables)

- [MSBuild tasks with dependencies](https://web.archive.org/web/20220717095807/https://natemcmaster.com/blog/2017/11/11/msbuild-task-with-dependencies/)
- [Implement custom MSBuild tasks and distribute them via NuGet - Rico Suter's blog.](https://web.archive.org/web/20211026123752/https://blog.rsuter.com/implement-custom-msbuild-tasks-and-distribute-them-via-nuget/)
- [TaskLoggingHelper Class (Microsoft.Build.Utilities) | Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/api/microsoft.build.utilities.tasklogginghelper?view=msbuild-17-netcore)
- [Implementing and Debugging Custom MSBuild Tasks - Matthias Koch](https://web.archive.org/web/20220810105041/https://ithrowexceptions.com/2020/08/04/implementing-and-debugging-custom-msbuild-tasks.html)

## Inline task

```xml
<UsingTask TaskName="MethodDemo" TaskFactory="CodeTaskFactory" AssemblyFile="$(MSBuildToolsPath)\Microsoft.Build.Tasks.Core.dll">
	<Task>
		<Reference Include="System.Web.Extensions" />
		<Using Namespace="System" />
		<Code Type="Method" Language="C#">
			<![CDATA[
				public override bool Execute()
				{
					if(Random.NextDouble() > 0.5)
					{
						Log.LogError("Fail because random value said so");
						//return false;
					}

					//return true;
					return !Log.HasLoggedErrors;
				}
			]]>
		</Code>
	</Task>
</UsingTask>

<UsingTask TaskName="ClassDemo" TaskFactory="CodeTaskFactory" AssemblyFile="$(MSBuildToolsPath)\Microsoft.Build.Tasks.Core.dll">
	<ParameterGroup>
		<InputParam0 ParameterType="Microsoft.Build.Framework.ITaskItem[]" Required="true" />
		<OutputParam0 ParameterType="Microsoft.Build.Framework.ITaskItem[]" Output="true" />
	</ParameterGroup>
	<Task>
		<Using Namespace="System" />
		<Code Type="Class" Language="C#">
			<![CDATA[
				using System;
				using System.IO;
				using System.Security;
				using System.Collections;
				using Microsoft.Build.Framework;
				using Microsoft.Build.Utilities;

				namespace Microsoft.Build.Tasks
				{
					public class ClassDemo : Task
					{
						[Required]
						public ITaskItem[] InputParam0 { get; set; }

						[Output]
						public ITaskItem[] OutputParam0 { get; set; }

						public override bool Execute()
						{
							ArrayList items = new ArrayList();
							foreach (var item in InputParam0)
							{
								Log.LogMessage(MessageImportance.High, item.ItemSpec);
							}

							OutputParam0 = new TaskItem[]{new TaskItem("itemspec1")};

							return !Log.HasLoggedErrors;
						}
					}
				}
			]]>
		</Code>
	</Task>
</UsingTask>
```

- [UsingTask Element (MSBuild) - MSBuild | Microsoft Learn](https://learn.microsoft.com/en-us/visualstudio/msbuild/usingtask-element-msbuild?view=vs-2022)
- [Walkthrough: Creating an Inline Task - MSBuild | Microsoft Learn](https://learn.microsoft.com/en-us/visualstudio/msbuild/walkthrough-creating-an-inline-task?view=vs-2022)
- [MSBuild Inline Tasks - MSBuild | Microsoft Learn](https://learn.microsoft.com/en-us/visualstudio/msbuild/msbuild-inline-tasks?view=vs-2022)
- [Task Writing - MSBuild | Microsoft Learn](https://learn.microsoft.com/en-us/visualstudio/msbuild/task-writing?view=vs-2022)
- [msbuild/RoslynCodeTaskFactory.cs at main · dotnet/msbuild · GitHub](https://github.com/dotnet/msbuild/blob/main/src/Tasks/RoslynCodeTaskFactory/RoslynCodeTaskFactory.cs)
- [c# - How to create MSBuild inline task from multiple source files - Stack Overflow](https://stackoverflow.com/questions/25089520/how-to-create-msbuild-inline-task-from-multiple-source-files/25113818#25113818) - run time compilaton of custom task
- [Use MSBuild To Do More](https://web.archive.org/web/20221116081051/https://3gstudent.github.io/Use-MSBuild-To-Do-More) - [msbuild-inline-task/ at master · 3gstudent/msbuild-inline-task · GitHub](https://github.com/3gstudent/msbuild-inline-task/tree/master) - [3gstudent.github.io/2016-9-20-Use MSBuild To Do More.md at main · 3gstudent/3gstudent.github.io · GitHub](https://github.com/3gstudent/3gstudent.github.io/blob/main/_posts/2016-9-20-Use%20MSBuild%20To%20Do%20More.md)
- only C# 5 is supported with `CodeTaskFactory`, or use `RoslynCodeTaskFactory` but available from VS 15.8+ (it's possible to [use a fallback](https://learn.microsoft.com/en-us/previous-versions/visualstudio/visual-studio-2017/msbuild/msbuild-roslyncodetaskfactory?view=vs-2017#provide-backward-compatibility)). See also [Are C#7 local functions allowed in inline tasks? · Issue #2742 · dotnet/msbuild](https://github.com/dotnet/msbuild/issues/2742)
- [MSBuild Inline Tasks with RoslynCodeTaskFactory - MSBuild | Microsoft Learn](https://learn.microsoft.com/en-us/previous-versions/visualstudio/visual-studio-2017/msbuild/msbuild-roslyncodetaskfactory?view=vs-2017)
- [MSBuild 4.0 Custom Task Walkabout pt4 | owenG.net](https://web.archive.org/web/20211022181256/http://oweng.net/Visual-Studio-2010/MSBuild/Custom-Tasks-in-MSBuild-4.0-and-Team-Foundation-Build-4.aspx)
- [Failure using 15.8 RoslynCodeTaskFactory · Issue #3726 · dotnet/msbuild](https://github.com/dotnet/msbuild/issues/3726) - can't use external assemblies. See also [RoslynCodeTaskFactory doesn't load external assemblies · Issue #5106 · dotnet/msbuild](https://github.com/dotnet/msbuild/issues/5106)
- [jeffkl/RoslynCodeTaskFactory: An MSBuild CodeTaskFactory that uses Roslyn compiler for cross platform compatibility](https://github.com/jeffkl/RoslynCodeTaskFactory)

## Exec task

Aka tool task

How to encode `;` in variable given to `EnvironmentVariables` (which use `;` as variables separator). TL;DR: use `%3B`:

- [Customize system environment variable Path for MSBuild Exec Task - Stack Overflow](https://stackoverflow.com/questions/31664834/customize-system-environment-variable-path-for-msbuild-exec-task/66560402#66560402)
- [Exec.EnvironmentVariables fails to parse well-formed PATH · Issue #773 · dotnet/msbuild](https://github.com/dotnet/msbuild/issues/773#issuecomment-262295113)
- use an item group

Other:

- [Exec Task - MSBuild | Microsoft Learn](https://learn.microsoft.com/en-us/visualstudio/msbuild/exec-task?view=vs-2022)
- [Running Windows PowerShell Scripts from MSBuild Project Files | Microsoft Learn](https://learn.microsoft.com/en-us/aspnet/web-forms/overview/deployment/advanced-enterprise-web-deployment/running-windows-powershell-scripts-from-msbuild-project-files)

## Variables

MSBuild Property, Item, Item Metadata

```
<Exec Command="powershell -NonInteractive -executionpolicy Unrestricted &quot;Write-Host `&quot;A=1``0B=2``0C=3`&quot;&quot;" EchoOff="true" ConsoleToMSBuild="true">
	<Output TaskParameter="ConsoleOutput" PropertyName="EnvironmentVariablesRaw"/>
</Exec>
<ItemGroup>
	<FnmEnvironmentVariables Include="$(EnvironmentVariablesRaw.Split(`%00`))"/>
</ItemGroup>
<Exec Command="powershell -NonInteractive -executionpolicy Unrestricted &quot;[System.Environment]::GetEnvironmentVariables()&quot;" EnvironmentVariables="@(FnmEnvironmentVariables)"/>
```

- [Different ways to pass variables in MSBuild - Stack Overflow](https://stackoverflow.com/questions/2814424/different-ways-to-pass-variables-in-msbuild#2816244)
- [Use property functions to call .NET methods - MSBuild | Microsoft Learn](https://learn.microsoft.com/en-us/visualstudio/msbuild/property-functions?view=vs-2022)
- [IT:AD:MSbuild:HowTo:Project Syntax/Properties and Arrays / IT:AD:MSBuild:HowTo / IT:AD:MSBuild / IT:AD (IT App Development) / IT \[Notes\]](https://www.skysigal.com/it/ad/msbuild/howto/project_syntax_properties_and_arrays)
- [How do I perform the EXEC task in a "loop" with MSBuild ItemGroups? - Stack Overflow](https://stackoverflow.com/questions/6036748/how-do-i-perform-the-exec-task-in-a-loop-with-msbuild-itemgroups)
- [Escape Special Characters in MSBuild - MSBuild | Microsoft Learn](https://learn.microsoft.com/en-us/visualstudio/msbuild/how-to-escape-special-characters-in-msbuild?view=vs-2022)
