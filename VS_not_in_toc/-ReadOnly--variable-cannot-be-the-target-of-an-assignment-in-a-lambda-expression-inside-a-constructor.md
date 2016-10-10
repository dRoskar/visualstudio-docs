---
title: "&#39;ReadOnly&#39; variable cannot be the target of an assignment in a lambda expression inside a constructor"
ms.custom: na
ms.date: 10/01/2016
ms.prod: visual-studio-dev14
ms.reviewer: na
ms.suite: na
ms.technology: 
  - devlang-csharp
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f96f8c79-86df-4727-bc6d-f0844da21395
caps.latest.revision: 7
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
# &#39;ReadOnly&#39; variable cannot be the target of an assignment in a lambda expression inside a constructor
You have referred to a `ReadOnly` variable from within a lambda expression, which is not permitted. The following code causes this error by sending the `ReadOnly` variable `m` as the argument to a `ByRef` parameter.  
  
```vb#  
Class Class1  
  
    ReadOnly m As Integer  
  
    Sub New()  
        ' The use of m triggers the error.  
        Dim f = Function() Test(m)  
    End Sub  
  
    Function Test(ByRef n As Integer) As String  
    End Function  
  
End Class  
```  
  
 **Error ID:** BC36602  
  
### To correct this error  
  
-   If possible, change parameter `n` in function `Test` to a `ByVal` parameter, as shown in the following code.  
  
    ```vb#  
    Class Class1Fix1  
  
        ReadOnly m As Integer  
  
        Sub New()  
            Dim f = Function() Test(m)  
        End Sub  
  
        Function Test(ByVal n As Integer) As String  
        End Function  
  
    End Class  
    ```  
  
### To correct this error  
  
-   Assign the `ReadOnly` variable `m` to a local variable in the constructor, and use the local variable in place of `m`, as shown in the following code.  
  
    ```vb#  
    Class Class1Fix2  
         ReadOnly m As Integer  
  
        Sub New()  
            Dim temp = m  
            Dim f = Function() Test(temp)  
        End Sub  
  
        Function Test(ByRef n As Integer) As String  
        End Function  
  
    End Class  
    ```  
  
## See Also  
 [Lambda Expressions](../Topic/Lambda%20Expressions%20\(Visual%20Basic\).md)   
 [ReadOnly](../Topic/ReadOnly%20\(Visual%20Basic\).md)   
 [NOT IN BUILD: Using Constructors and Destructors](assetId:///548eebe1-86c4-4377-b2f5-447cb8be3d90)