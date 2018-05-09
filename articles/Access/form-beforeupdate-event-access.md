---
title: Form.BeforeUpdate Event (Access)
keywords: vbaac10.chm13637
f1_keywords:
- vbaac10.chm13637
ms.prod: access
api_name:
- Access.Form.BeforeUpdate
ms.assetid: b783fcab-f697-a464-820c-712eac46cb4b
ms.date: 11/30/2017
---


# Form.BeforeUpdate Event (Access)

The **BeforeUpdate** event occurs before changed data in a control or record is updated.


## Syntax


_expression_. **BeforeUpdate**(**_Cancel_**)


_expression_ A variable that represents a **Form** object.


### Parameters

|**Name**|**Required/Optional**|**Data Type**|**Description**|
|:-----|:-----|:-----|:-----|
| _Cancel_|Required|**Integer**|The setting determines if the **BeforeUpdate** event occurs. Setting the _Cancel_ argument to **True** (?1) cancels the **BeforeUpdate** event.|

## Remarks

Changing data in a control by using Visual Basic or a macro containing the **SetValue** action doesn't trigger these events for the control. However, if you then move to another record or save the record, the form's **BeforeUpdate** event does occur.

To run a macro or event procedure when this event occurs, set the **BeforeUpdate** property to the name of the macro or to [Event Procedure].

This event does not apply to option buttons, check boxes, or toggle buttons in an option group. It applies only to the option group itself.

The **BeforeUpdate** event is triggered when a control or record is updated. Within a record, changed data in each control is updated when the control loses the focus or when the user presses **ENTER** or **TAB**. When the focus leaves the record or if the user clicks **Save Record** on the **Records** menu, the entire record is updated, and the data is saved in the database.

When you enter new or changed data in a control on a form and then move to another record or save the record by clicking **Save Record** on the **Records** menu, the **AfterUpdate** event for the form occur immediately after the **AfterUpdate** event for the control. When you move to a different record, the **Exit** and **LostFocus** events for the control occur, followed by the **Current** event for the record you moved to, and the **Enter** and **GotFocus** events for the first control in this record. To run the **AfterUpdate** macro or event procedure without running the **Exit** and **LostFocus** macros or event procedures, save the record by using the **Save Record** command on the **Records** menu.

**BeforeUpdate** macros and event procedures run only if you change the data in a control. This event does not occur when a value changes in a calculated control. **BeforeUpdate** macros and event procedures for a form run only if you change the data in one or more controls in the record.

For forms, you can use the  **BeforeUpdate** event to cancel updating of a record before moving to another record.

If the user enters a new value in the control, the  **OldValue** property setting isn't changed until the data is saved (the record is updated). If you cancel an update, the value of the **OldValue** property replaces the existing value in the control.

You often use the **BeforeUpdate** event to validate data, especially when you perform complex validations, such as those that:

- Involve conditions for more than one value on a form.
    
- Display different error messages for different data entered.
    
- Can be overridden by the user.
    
- Contain references to controls on other forms or contain user-defined functions. 
    
> [!NOTE]
> To perform simple validations, or more complex validations such as requiring a value in a field or validating more than one control on a form, you can use the  **ValidationRule** property for controls and the **ValidationRule** and **Required** properties for fields and records in tables.

A run-time error will occur if you attempt to modify the data contained in the control that fired the  **BeforeUpdate** event in the event's procedure.


## Example

The following example shows how you can use a **BeforeUpdate** event procedure to check whether a product name has already been entered in the database. After the user types a product name in the **ProductName** box, the value is compared to the **ProductName** field in the **Products** table. If there is a matching value in the **Products** table, a message is displayed that informs the user that the product has already been entered.

To try the example, add the following event procedure to a form named **Products** that contains a text box called **ProductName**.

```vb
Private Sub ProductName_BeforeUpdate(Cancel As Integer) 
    If(Not IsNull(DLookup("[ProductName]", _ 
        "Products", "[ProductName] ='" _ 
        &; Me!ProductName &; "'"))) Then 
        MsgBox "Product has already been entered in the database." 
        Cancel = True 
        Me!ProductName.Undo 
    End If 
End Sub
```

The following example shows how to display a message when a control is empty on a continuous form when a user moves to another record.

**Sample code provided by:** Bill Jelen, [MrExcel.com](http://www.mrexcel.com/)

```vb
Private Sub Form_BeforeUpdate(Cancel As Integer)
    Dim oContr As Control
    For Each oContr In Me.Detail.Controls
        If IsNull(oContr) = True Then
            If MsgBox(oContr.Name &; " is empty", vbOKCancel) = vbCancel Then
                Cancel = True: oContr.SetFocus: Exit Sub
            End If
        End If
    Next oContr
End Sub
```

The following example shows how to use the **BeforeUpdate** event of a form to require that a value be entered into one control when another control also has data.

**Sample code provided by:** The [Microsoft Access 2010 Programmer's Reference](http://www.wrox.com/WileyCDA/WroxTitle/Access-2010-Programmer-s-Reference.productCd-0470591668.html)

```vb
Private Sub Form_BeforeUpdate(Cancel As Integer)
If (IsNull(Me.FieldOne)) Or (Me.FieldOne.Value =  "") Then
    ' No action required
Else
    If (IsNull(Me.FieldTwo)) or (Me.FieldTwo.Value = "") Then
        MsgBox "You must provide data for field 'FieldTwo', " &; _
            "if a value is entered in FieldOne", _
            vbOKOnly, "Required Field"
        Me.FieldTwo.SetFocus
        Cancel = True
        Exit Sub
    End If
End If

End Sub
```


## About the contributors
<a name="AboutContributors"> </a>

Holy Macro! Books publishes entertaining books for people who use Microsoft Office. See the complete catalog at MrExcel.com. 

Wrox Press is driven by the Programmer to Programmer philosophy. Wrox books are written by programmers for programmers, and the Wrox brand means authoritative solutions to real-world programming problems. 


## See also

[Form Object](form-object-access.md)
