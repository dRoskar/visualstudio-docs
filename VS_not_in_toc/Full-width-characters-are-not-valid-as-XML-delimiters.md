---
title: "Full width characters are not valid as XML delimiters"
ms.custom: na
ms.date: 10/01/2016
ms.prod: visual-studio-dev14
ms.reviewer: na
ms.suite: na
ms.technology: 
  - devlang-csharp
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f5d724f8-545b-4cf8-9606-12c63814c6e8
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
# Full width characters are not valid as XML delimiters
An XML literal has been defined that includes a full-width character as a delimiter. Full-width characters are also referred to as wide or multi-byte characters.  
  
 **Error ID:** BC31197  
  
### To correct this error  
  
-   Remove the full-width character from the XML literal definition and replace it with a valid ANSI delimiter character. Valid delimiter characters include the following: `<`, `>`, `=`, `:`, `/`.  
  
## See Also  
 [XML Literals](../Topic/XML%20Literals%20\(Visual%20Basic\).md)   
 [Character Encoding in the .NET Framework](../Topic/Character%20Encoding%20in%20the%20.NET%20Framework.md)   
 [XML](../Topic/XML%20in%20Visual%20Basic.md)