---
title: "IDebugArrayObject::GetCount | Microsoft Docs"
ms.custom: ""
ms.date: "11/04/2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "vs-ide-sdk"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "IDebugArrayObject::GetCount"
helpviewer_keywords: 
  - "IDebugArrayObject::GetCount method"
ms.assetid: 7931f3f7-033c-4bf8-8abd-95183952ebb0
caps.latest.revision: 10
author: "gregvanl"
ms.author: "gregvanl"
manager: ghogen
ms.workload: 
  - "vssdk"
---
# IDebugArrayObject::GetCount
Gets the count of elements in the array.  
  
## Syntax  
  
```  
[C++]  
HRESULT GetCount(   
   DWORD* pdwElements  
);  
```  
  
```  
[C#]  
int GetCount(  
   out uint pdwElements  
);  
```  
  
#### Parameters  
 `pdwElements`  
 [out] Returns the count.  
  
## Return Value  
 If successful, returns S_OK; otherwise, returns an error code.  
  
## Remarks  
 This method sees all of the elements of an array object as a one-dimensional array, even if the array object is multi-dimensional. For example, given the array `myarray[3][2][6]`, this method would return 36 in the `pdwElements` parameter. Use the [GetElement](../../../extensibility/debugger/reference/idebugarrayobject-getelement.md) method to retrieve the individual elements one at a time.  
  
## See Also  
 [IDebugArrayObject](../../../extensibility/debugger/reference/idebugarrayobject.md)