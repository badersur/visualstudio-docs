---
title: "How to: Register a Service"
ms.custom: na
ms.date: 10/01/2016
ms.prod: visual-studio-dev14
ms.reviewer: na
ms.suite: na
ms.technology: 
  - devlang-csharp
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d086be78-ec3c-43cc-b799-5180a71e19f1
caps.latest.revision: 16
manager: douge
translation.priority.ht: 
  - de-de
  - es-es
  - fr-fr
  - it-it
  - ja-jp
  - ko-kr
  - ru-ru
  - zh-cn
  - zh-tw
translation.priority.mt: 
  - cs-cz
  - pl-pl
  - pt-br
  - tr-tr
---
# How to: Register a Service
The managed package framework (MPF) provides attributes to control the registration of managed services. The RegPkg utility uses these attributes to register a service with Visual Studio.  
  
## Example  
 The code that follows is from [VSSDK Samples](../VS_not_in_toc/VSSDK-Samples.md).  
  
 [!CODE [VSSDKRegisterService#1](../CodeSnippet/VS_Snippets_VSSDK/vssdkregisterservice#1)]  
  
 The <xref:Microsoft.VisualStudio.Shell.ProvideServiceAttribute?qualifyHint=False> registers the SMyGlobalService service with Visual Studio. For more information about <xref:Microsoft.VisualStudio.Shell.DefaultRegistryRootAttribute?qualifyHint=False> and <xref:Microsoft.VisualStudio.Shell.PackageRegistrationAttribute?qualifyHint=False>, see [Registering and Unregistering VSPackages](../Topic/Registering%20and%20Unregistering%20VSPackages.md).  
  
 To register a service that replaces another service with the same name, use the <xref:Microsoft.VisualStudio.Shell.ProvideServiceOverrideAttribute?qualifyHint=False> instead of the <xref:Microsoft.VisualStudio.Shell.ProvideServiceAttribute?qualifyHint=False>.  
  
## Robust Programming  
 To make it easier to recompile a service provider without changing the service client, or vice versa, you can define the service and its interfaces in a separate assembly module. The following code is from the IMyGlobalService.cs file in the Reference.Services (C#) sample.  
  
 [!CODE [VSSDKRegisterService#2](../CodeSnippet/VS_Snippets_VSSDK/vssdkregisterservice#2)]  
  
 The <xref:System.Runtime.InteropServices.ComVisibleAttribute?qualifyHint=False> is required to obtain the interface from unmanaged code.  
  
> [!NOTE]
>  Although you could use the same type or GUID for both the service and the interface, we recommend that you separate the two because a service can expose different interfaces.  
  
## See Also  
 [Registering VSPackages](assetId:///31e6050f-1457-4849-944a-a3c36b76f3dd)   
 [Service Essentials](../Topic/Service%20Essentials.md)