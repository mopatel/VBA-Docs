---
title: CommandButton.IsVisible property (Access)
keywords: vbaac10.chm10491
f1_keywords:
- vbaac10.chm10491
ms.prod: access
api_name:
- Access.CommandButton.IsVisible
ms.assetid: f5438725-4628-4f8e-1bf3-0027348b9285
ms.date: 06/08/2017
localization_priority: Normal
---


# CommandButton.IsVisible property (Access)

You can use the  **IsVisible** property in to determine whether a control on a report is visible. Read/write **Boolean**.


## Syntax

_expression_.**IsVisible**

_expression_ A variable that represents a [CommandButton](Access.CommandButton.md) object.


## Remarks


 **Note**  You can set the  **IsVisible** property only in the **Print** event of a report section that contains the control.

You can use the  **IsVisible** property together with the **HideDuplicates** property to determine when a control on a report is visible and show or hide other controls as a result. For example, you could hide a line control when a text box control is hidden because it contains duplicate values.


## Example

The following example uses the  **IsVisible** property of a text box to control the display of a line control on a report. T



Paste the following code into the Declarations section of the report module, and then view the report to see the line formatting controlled by the  **IsVisible** property:




```vb
Private Sub Detail_Print(Cancel As Integer, PrintCount As Integer) 
 If Me!CategoryID.IsVisible Then 
 Me!Line0.Visible = True 
 Else 
 Me!Line0.Visible = False 
 End If 
End Sub
```


## See also


[CommandButton Object](Access.CommandButton.md)

[!include[Support and feedback](~/includes/feedback-boilerplate.md)]