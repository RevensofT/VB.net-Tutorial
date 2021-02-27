# Generic Type

A macro for late define type for use in object or method scope.

## Why and when should you use generic type ?

- If your code do the same thing but all change is just those class/structure use with in code.
- If your code doesn't care which type is affiliate with then it's fine to use generic type.

# Declare generic type

## - Class/structure scope

```vb
Class List(Of T) 'T is generic type, can be almost any type.'
End Class

Interface Boxing(Of T As Structure) 'T must be value/structure type.'
End Interface

Class Forge(Of T As New) 'T must be constructable by New keyword.'
End Class 

'T0 can be any type but T1 must be implement by IList of T0 '
'and must be constructable with New keyword.'
Class Enumable(Of T0, T1 As {New, IList(Of T0)}) 
End Class
```



## - Method scope

```vb
'T and V can be any type, Input will be type of T and method will return V type data back.'
Function [As](Of T, V)(Input As T) As V 
End Function

'T must be value/structure type and V must be refrence/class type'
Function Reforge(Of T As Structure, V As Class)(ByRef Input As T) As V
```

# Example

```vb
Public Module Extensioning    
    <Extension>
    Public Function boxed(Of T As Structure)(Input As T) As box(Of T)
        Return New Custom.box(Of T) With {.value = Input}
    End Function
End Module
   
Public Class box(Of T As Structure)
    Public value As T

    Public Shared Widening Operator CType(Input As T) As box(Of T)
    	Return New box(Of T) With {.value = Input}
	End Operator

    Public Shared Widening Operator CType(Input As box(Of T)) As T
        Return Input.value
    End Operator
End Class   
```

## Usage

```vb
<Extension>
Function double_box(Input As Integer) As box(Of Integer)
    Return (Input * 2).boxed
End Function

<Extension>
Sub box_double(Input As box(Of Integer))
    Input.value *= 2
End Sub

Sub main()
    Dim Box = 10.double_box
    Box.box_double()
    Console.WriteLine(Box)
End Sub

'Result = 40'
```

