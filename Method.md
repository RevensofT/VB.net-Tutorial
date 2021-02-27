# Method

- Instance type
  - Always attach with data type like class or structure.
  - Always has attach data type as first argument of method in hidden.
- Static type
  - Can truly has 0 argument.
  - Prefer to be call via data type name instead variant name.
  - Declare by keyword `Shared` except when declare inside `Module` because all method in module type always be static type.

# Delegate

A special class type contain a method pointer also contain attach data if point to instance method type. Very flexible but come with a price and can't do inline call.

Declare with keyword `Delegate` , has standard delegate in `System` namespace `Func` for function and `Action` for sub.

```vb
Delegate Sub Write(Word As String)
Sub Main()
	Dim Write_line As New Write(AddressOf Console.WriteLine)
	Write_line("Hello SIMP.")
End Sub
```

# Event 

- AKA Multicast Delegate.
- An array of delegate.
- When invoke it will invoke all delegate inside.
- Has custom event for add method that invoke on add and remove delegate from event.
- Extremely flexible but also very high price.

# Argument of Method

- ByVal - pass value to argument list.

- ByRef - pass pointer to argument list.

- Optional - for custom default of that argument, can be use with lambda.

  ```vb
  Function Mul(X As Integer, Optional Y As Integer = 10)
      Return X * Y
  End Function
  
  Sub Main()
      Dim A = Mul(5, 6) '5 x 6 = 30'
      Dim B = Mul(3) '3 x 10 = 30'
      Console.WriteLine(A = B) 'True'
  End Sub
  ```

- ParamArray - must be last argument, all pass argument from this combine into an array, can be use with lambda.

  ```vb
  Function Print(ParamArray Input() As Integer)
      For Each Item In Input
  	    Console.WriteLine(Item)
  	Next
  End Function
  
  Sub Main()
  	Print(5, 10, 15, 20)
  End Sub
  
  '5
  '10
  '15
  '20
  ```

  

# Lambda express

A Godlike flexible way to create method with some price, it's anonymous type contain relate all delegate with all relate data.

```vb
Dim Counter = 1
Dim Short_form = Function() Counter + 1

'Only Sub can do continue short form.'
Dim Countinue_short_form = Sub() Console.WriteLine(Counter) : Counter = Short_form()

Dim Full_form = Function(ByRef Input As Integer) As Integer
	Dim Out = Input
    Input += 1
    Return Out
End Function

Dim Instant = 	Function
                    Dim Out = 2
                    For I = 3 To 5
                    	Out *= I
                	Next
        		End Function()
'Instant == 120'
```

# Extension method

A static method type with instance type style, request specify extension attribute and MUST has an argument.

```vb
Module Exten
    <Extension>
    Function [Next](ByRef Input As Integer) As Integer
        Dim Out = Input
        Input += 1
        Return Out
    End Function

    <Extension>
    Function Write(Input As Integer) As Integer
        Console.WriteLine(Input)
    End Function
End Module

Sub Main()
	Call 0.Write.Next.Write.Next.Write.Next.Write.Next.Write.Next.Write()
End Sub

'0
'1
'2
'3
'4
'5
```

