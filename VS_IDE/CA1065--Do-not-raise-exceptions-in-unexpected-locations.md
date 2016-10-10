---
title: "CA1065: Do not raise exceptions in unexpected locations"
ms.custom: na
ms.date: 10/03/2016
ms.prod: visual-studio-dev14
ms.reviewer: na
ms.suite: na
ms.technology: 
  - vs-devops-test
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4e1bade4-4ca2-4219-abc3-c7b2d741e157
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
# CA1065: Do not raise exceptions in unexpected locations
|||  
|-|-|  
|TypeName|DoNotRaiseExceptionsInUnexpectedLocations|  
|CheckId|CA1065|  
|Category|Microsoft.Design|  
|Breaking Change|Non Breaking|  
  
## Cause  
 A method that is not expected to throw exceptions throws an exception.  
  
## Rule Description  
 Methods that are not expected to throw exceptions can be categorized as follows:  
  
-   Property Get Methods  
  
-   Event Accessor Methods  
  
-   Equals Methods  
  
-   GetHashCode Methods  
  
-   ToString Methods  
  
-   Static Constructors  
  
-   Finalizers  
  
-   Dispose Methods  
  
-   Equality Operators  
  
-   Implicit Cast Operators  
  
 The following sections discuss these method types.  
  
### Property Get Methods  
 Properties are basically smart fields. Therefore, they should behave like a field as much as possible. Fields do not throw exceptions and neither should properties. If you have a property that throws an exception, consider making it a method.  
  
 The following exceptions are allowed to be thrown from a property get method:  
  
-   <xref:System.InvalidOperationException?qualifyHint=True> and all derivatives (including <xref:System.ObjectDisposedException?qualifyHint=True>)  
  
-   <xref:System.NotSupportedException?qualifyHint=True> and all derivatives  
  
-   <xref:System.ArgumentException?qualifyHint=True> (only from indexed get)  
  
-   <xref:System.Collections.Generic.KeyNotFoundException?qualifyHint=False> (only from indexed get)  
  
### Event Accessor Methods  
 Event accessors should be simple operations that do not throw exceptions. An event should not throw an exception when you try to add or remove an event handler.  
  
 The following exceptions are allowed to be thrown from an event accesor:  
  
-   <xref:System.InvalidOperationException?qualifyHint=True> and all derivatives (including <xref:System.ObjectDisposedException?qualifyHint=True>)  
  
-   <xref:System.NotSupportedException?qualifyHint=True> and all derivatives  
  
-   <xref:System.ArgumentException?qualifyHint=False> and derivatives  
  
### Equals Methods  
 The following **Equals** methods should not throw exceptions:  
  
-   <xref:System.Object.Equals?qualifyHint=True>  
  
-   [M:IEquatable.Equals](http://go.microsoft.com/fwlink/?LinkId=113472)  
  
 An **Equals** method should return `true` or `false` instead of throwing an exception. For example, if Equals is passed two mismatched types it should just return `false` instead of throwing an <xref:System.ArgumentException?qualifyHint=False>.  
  
### GetHashCode Methods  
 The following **GetHashCode** methods should usually not throw exceptions:  
  
-   <xref:System.Object.GetHashCode?qualifyHint=False>  
  
-   [M:IEqualityComparer.GetHashCode(T)](http://go.microsoft.com/fwlink/?LinkId=113477)  
  
 **GetHashCode** should always return a value. Otherwise, you can lose items in the hash table.  
  
 The versions of **GetHashCode** that take an argument can throw an <xref:System.ArgumentException?qualifyHint=False>. However, **Object.GetHashCode** should never throw an exception.  
  
### ToString Methods  
 The debugger uses <xref:System.Object.ToString?qualifyHint=True> to help display information about objects in string format. Therefore, **ToString** should not change the state of an object and it should not throw exceptions.  
  
### Static Constructors  
 Throwing exceptions from a static constructor causes the type to be unusable in the current application domain. You should have a very good reason (such as a security issue) for throwing an exception from a static constructor.  
  
### Finalizers  
 Throwing an exception from a finalizer causes the CLR to fail fast, which tears down the process. Therefore, throwing exceptions in a finalizer should always be avoided.  
  
### Dispose Methods  
 A <xref:System.IDisposable.Dispose?qualifyHint=True> method should not throw an exception. Dispose is often called as part of the clean up logic in a `finally` clause. Therefore, explicitly throwing an exception from Dispose forces the user to add exception handling inside the `finally` clause.  
  
 The **Dispose(false)** code path should never throw exceptions, because this is almost always called from a finalizer.  
  
### Equality Operators (==, !=)  
 Like Equals methods, equality operators should return either `true` or `false` and should not throw exceptions.  
  
### Implicit Cast Operators  
 Because the user is often unaware that an implicit cast operator has been called, an exception thrown by the implicit cast operator is completely unexpected. Therefore, no exceptions should be thrown from implicit cast operators.  
  
## How to Fix Violations  
 For property getters, either change the logic so that it no longer has to throw an exception, or change the property into a method.  
  
 For all other method types listed previously, change the logic so that it no longer must throw an exception.  
  
## When to Suppress Warnings  
 It is safe to suppress a warning from this rule if the violation was caused by an exception declaration instead of a thrown exception.  
  
## Related Rules  
 [CA2219: Do not raise exceptions in exception clauses](../VS_IDE/CA2219--Do-not-raise-exceptions-in-exception-clauses.md)  
  
## See Also  
 [Design Warnings](../VS_IDE/Design-Warnings.md)