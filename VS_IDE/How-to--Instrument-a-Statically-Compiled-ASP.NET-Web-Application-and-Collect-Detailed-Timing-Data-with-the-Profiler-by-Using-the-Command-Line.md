---
title: "How to: Instrument a Statically Compiled ASP.NET Web Application and Collect Detailed Timing Data with the Profiler by Using the Command Line"
ms.custom: na
ms.date: 10/10/2016
ms.prod: visual-studio-dev14
ms.reviewer: na
ms.suite: na
ms.technology: 
  - vs-ide-debug
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b260ce68-76e6-4c3b-8062-3c00bd5cf7b8
caps.latest.revision: 23
manager: ghogen
translation.priority.ht: 
  - cs-cz
  - de-de
  - es-es
  - fr-fr
  - it-it
  - ja-jp
  - ko-kr
  - pl-pl
  - pt-br
  - ru-ru
  - tr-tr
  - zh-cn
  - zh-tw
---
# How to: Instrument a Statically Compiled ASP.NET Web Application and Collect Detailed Timing Data with the Profiler by Using the Command Line
This topic describes how to use Visual Studio Profiling Tools command-line tools to instrument a precompiled ASP.NET Web component or Web site and collect detailed timing data.  
  
> [!NOTE]
>  Command-line tools of the Profiling Tools are located in the \Team Tools\Performance Tools subdirectory of the Visual Studio installation directory. On 64-bit computers, both 64-bit and 32-bit versions of the tools are available. To use the profiler command-line tools, you must add the tools path to the PATH environment variable of the Command Prompt window or add it to the command itself. For more information, see [Specifying the Path to Command Line Tools](../VS_IDE/Specifying-the-Path-to-Profiling-Tools-Command-Line-Tools.md).  
>   
>  Adding tier interaction data to a profiling run requires specific procedures with the command line profiling tools. See [Collecting tier interaction data](../VS_IDE/Adding-tier-interaction-data-from-the-command-line.md).  
  
 To collect detailed timing data from a ASP.NET Web component by using the instrumentation method, you use the [VSInstr.exe](../VS_IDE/VSInstr.md) tool to generate an instrumented version of the component. On the computer that hosts the component, you replace the noninstrumented version of the component with the instrumented version. You then use the [VSPerfCLREnv.cmd](../VS_IDE/VSPerfCLREnv.md) tool to initialize the global profiling environment variables and restart the host computer. You then start the profiler.  
  
 When the instrumented component is executed, timing data is automatically collected to a data file. You can pause and resume data collection during the profiling session.  
  
 To end a profiling session, you close the ASP.NET worker process that hosts the component and then explicitly shut down the profiler. In most cases, we recommend clearing the profiling environment variables at the end of a session.  
  
## Starting to Profile  
  
#### To instrument an ASP.NET Web component and start profiling  
  
1.  Open a Command Prompt window.  
  
2.  Use the **VSInstr** tool to generate an instrumented version of the target application. If necessary, replace the application binaries on the ASP.NET host computer with the instrumented binaries.  
  
3.  Initialize the .NET profiling environment variables. In the Command Prompt window, type:  
  
     **VSPerfClrEnv /globaltraceon**  
  
4.  Restart the computer.  
  
5.  Open a Command Prompt window. If necessary, set the profiler tools path.  
  
6.  Start the profiler. Type:  
  
     **VSPerfCmd /start:trace /output:** `OutputFile` [`Options`]  
  
    -   The [/start](../VS_IDE/Start.md)**:trace** option initializes the profiler.  
  
    -   The [/output](../VS_IDE/Output.md)**:**`OutputFile` option is required with **/start**. `OutputFile` specifies the name and location of the profiling data (.vsp) file.  
  
     You can use any of the following options with the **/start:trace** option.  
  
    > [!NOTE]
    >  The **/user** and **/crosssession** options are usually required for ASP.NET applications.  
  
    |Option|Description|  
    |------------|-----------------|  
    |[/user](../VS_IDE/User--VSPerfCmd-.md) **:**[`Domain`**\\**]`UserName`|Specifies the domain and user name of the account that owns the ASP.NET worker process. This option is required if the process is running as a user other than the logged on user. The process owner is listed in the User Name column on the Processes tab of Windows Task Manager.|  
    |[/crosssession](../VS_IDE/CrossSession.md)|Enables profiling of processes in other logon sessions. This option is required if the ASP.NET application is running in a different session. The session idenitifier is listed in the Session ID column on the Processes tab of Windows Task Manager. **/CS** can be specified as an abbreviation for **/crosssession**.|  
    |[/wincounter](../VS_IDE/WinCounter.md) **:** `WinCounterPath`|Specifies a Windows performance counter to be collected during profiling.|  
    |[/automark](../VS_IDE/AutoMark.md) **:** `Interval`|Use with **/wincounter** only. Specifies the number of milliseconds between Windows performance counter collection events. Default is 500 ms.|  
    |[/events](../VS_IDE/Events--VSPerfCmd-.md) **:** `Config`|Specifies an Event Tracing for Windows (ETW) event to be collected during profiling. ETW events are collected in a separate (.etl) file.|  
    |[/globaloff](../VS_IDE/GlobalOn-and-GlobalOff.md)|To start the profiler with data collection paused, add the **/globaloff** option to the **/start** command line. Use **/globalon** to resume profiling.|  
  
7.  Open the Web site that contains the instrumented component.  
  
## Controlling Data Collection  
 When the target application is running, you can control data collection by starting and stopping the writing of data to the file by using **VSPerfCmd.exe** options. Controlling data collection enables you to collect data for a specific part of program execution, such as starting or shutting down the application.  
  
#### To start and stop data collection  
  
-   The following pairs of options start and stop data collection. Specify each option on a separate command line. You can turn data collection on and off multiple times.  
  
    |Option|Description|  
    |------------|-----------------|  
    |[/globalon /globaloff](../VS_IDE/GlobalOn-and-GlobalOff.md)|Starts (**/globalon**) or stops (**/globaloff**) data collection for all processes.|  
    |[/processon](../VS_IDE/ProcessOn-and-ProcessOff.md) **:** `PID` [/processoff](../VS_IDE/ProcessOn-and-ProcessOff.md) **:** `PID`|Starts (**/processon**) or stops (**/processoff**) data collection for the process specified by the process ID (`PID`).|  
    |[/threadon](../VS_IDE/ThreadOn-and-ThreadOff.md) **:** `TID` [/threadoff](../VS_IDE/ThreadOn-and-ThreadOff.md) **:** `TID`|Starts (**/threadon**) or stops (**/threadoff**) data collection for the thread specified by the thread ID (`TID`).|  
  
## Ending the Profiling Session  
 To end a profiling session, close the ASP.NET Web application, and then use the Internet Information Services (IIS) **IISReset** command to close the ASP.NET worker process. Call the **VSPerfCmd** [/shutdown](../VS_IDE/Shutdown.md) option to turn off the profiler and close the profiling data file.  
  
 The **VSPerfClrEnv /globaloff** command clears the profiling environment variables. You must restart the computer for the new environment settings to be applied.  
  
#### To end a profiling session  
  
1.  Close the ASP.NET Web application.  
  
2.  Close the ASP.NET worker process. Type:  
  
     **IISReset /stop**  
  
3.  Shut down the profiler. Type:  
  
     **VSPerfCmd /shutdown**  
  
4.  (Optional). Clear the profiling environment variables. Type:  
  
     **VSPerfCmd /globaloff**  
  
5.  Restart the computer.  
  
## See Also  
 [Profiling ASP.NET Web Applications](../VS_IDE/Command-Line-Profiling-of-ASP.NET-Web-Applications.md)   
 [Instrumentation Method Data Views](../VS_IDE/Instrumentation-Method-Data-Views.md)