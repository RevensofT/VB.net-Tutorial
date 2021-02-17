# Class and structure

What's really is a class ? What's really is a structure ? Is summary explain like class is reference type and structure is value type really make you understand them ? Let's find out !

## Class

1. Store in a part of memory call Heap, which keep any thing there until it's no reference about it for a while.
2. Always has a meta data or header of class store along with its field data.
3. Arrange field data to fit pack size by default, not arrange by declare order.
4. Support OOP feature like Interface and Inherit with high price to pay when use this feature.

## Structure

1. Store in a part of memory call Stack or Stack-Frame of method, which will dispose anything on it when end method.
2. No meta data or header of it.
3. Arrange field data by declare order by default but has some exception like ValueTuple.
4. Can use Interface but price is sky high.

## Static | Module

1. Store in Heap but it will be there until app | program end.
2. Can't create instance of it.
3. Only place you can make Extension method.
4. Initialize on first use but highly bug when you call uninitialized module on other uninitialized module.

# Any simple rule to choose between class and structure ?

- If you want to update data on its field any where, go for class.
- If you need to use Inherit or Interface, must be class.
- If you plan to create self update method, must be class.
- If you plan to use Event, must be class.
- If you want to store any data, go for structure.
- If you want to each of them no relate to other [A.D = 10 : B.D = A.D : B.D = 5 ' A.D = B.D Is False], go for structure.
- If you plan to overload operator, must be structure.
- If you plan to create self return method, must be structure.

# Class
```vb
Class name_class
    Dim field
    Property surname As String
        
    Sub New(name As String)
    End Sub
        
    Sub method(Argurment_1)
    End Sub
        
    Function method_return(Argurment_1) As String
    End Function
        
    Function to_string() As String	
    End Function
End Class
```

# Structure

```vb
Structure name
    Dim field

    Public Overloads Shared Operator +(Left As name, Right As String) As name
    End Operator

    Public Overloads Shared Operator -(Left As name, Right As String) As name
    End Operator

    Public Shared Widening Operator CType(Input As name) As String
    End Operator

	Public Shared Widening Operator CType(Name As String) As name
    End Operator
End Structure
```

# Example

```vb
A = New("Harry")
A.surname = "Potter"
Console.WriteLine(A.to_string)'Harry Potter'

B = New With {.field = "Jon"}
B += "Smith"
Console.WriteLine(B)'Jon Smith'
```

In this example, you can identify which is a class, which is a structure easily 

# What's store in a local variant of class and structure ?

A variant of structure store all data of that structure but A variant of class only store a memory address of class's data in heap.

# Be careful, a memory address ALSO structure aka value type

Some maybe call it pointer or maybe native int, anyway, it's also structure, don't miss treat it; only meta on local variant that make them count as marker for GC(Garbage Collection) to know that data on this address still in use, don't discard it yet.

# What's GC about ?

Just think it as manager of heap memory, it's job is keep any unuse out of heap, if you code in C or C++ you have to remove EVERY class you create by yourselves, it maybe sound troublesome but you have full control of it; GC do thing difference, you can't force it to clean up any time you want and you can't stop it when it want to clean up so this guy could be come trouble maker when you need performance AND this guy also biggest bottle neck on .net so create your class carefully.