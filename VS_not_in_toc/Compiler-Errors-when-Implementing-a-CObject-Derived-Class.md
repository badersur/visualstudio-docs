---
title: "Compiler Errors when Implementing a CObject-Derived Class"
ms.custom: na
ms.date: 10/01/2016
ms.devlang: 
  - C++
ms.prod: visual-studio-dev14
ms.reviewer: na
ms.suite: na
ms.technology: 
  - devlang-csharp
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9f249b52-aeff-41a1-8a74-a52aa08c4fcf
caps.latest.revision: 6
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
# Compiler Errors when Implementing a CObject-Derived Class
When you implement a class derived from `CObject` and your code is written so that the copy constructor or assignment operator for the class needs to be called, the compiler may report errors similar to the following:  
  
```  
error C2660: 'CSample::CSample' : function does not take 1 parameters  
error C2582: 'CSample' : 'operator =' function is unavailable  
```  
  
 You can reproduce the problem by compiling the example in the Sample Code section below.  
  
> [!NOTE]
>  The sample code shown in this article generates the following error messages:  
  
```  
error C2558: 'CSample::CSample' : no copy constructor available  
error C2582: 'CSample' : 'operator =' function is unavailable  
```  
  
 The reason for the compiler errors is that `CObject` declares a private copy constructor and assignment operator in the AFX.h file. Consequently, the compiler does not generate a default copy constructor and assignment operator for the `CObject`-derived class. Because the compiler does not find these functions declared in the class, it reports the errors.  
  
 To avoid the compiler errors, you need to implement a copy constructor and assignment operator for the `CObject`-derived class. This is illustrated in the sample code below. You can avoid the errors by uncommenting the lines indicated in the sample code.  
  
## Sample Code  
  
```  
// _error_Compiler_Errors_when_Implementing_a_CObject.2d.Derived_Class.cpp  
/* Compile options needed: /c  
*/  
  
// replace with #define _CONSOLE when compiling for Windows NT  
#define _DOS  
  
#include <afx.h>  
  
class CSample : public CObject  
{  
private:  
    short m_nValue;  
public:  
// uncomment the lines below to avoid the compiler errors  
//    CSample() {}  
//    CSample( const CSample &s )  // copy ctor  
//        { m_nValue = s.m_nValue; }  
//    CSample& operator=( const CSample &s )  // assignment operator  
//        { m_nValue = s.m_nValue; return *this; }  
};  
  
int main()  
{  
    CSample a;  
    CSample b = a;  
    a = b;  
}  
  
```  
  
## See Also  
 [Compiler Warnings C4600 Through C4799](../Topic/Compiler%20Warnings%20C4600%20Through%20C4799.md)