# StagedReturn
This is an example of a concept to call methods in a chain.

## Introduction
Sometimes it is not smart to give the user the possibility to call every public method in every situation. 
For example our class is designed to work correctly by the workflow: Set start values, 
process the data and after that the user can request the result by calling a getter. So we got the problen, that the user can
call the process method before the start values are set. The goal of this concept is to avoid this.
We will take an existing class to change it.

This is the class how we got it:

```csharp
public class SimpleCalculator
{
    private int? iValue1;
    private int? iValue2;
    private int? result;

    public void SetStartValues(int i1, int i2)
    {
        this.iValue1 = i1;
        this.iValue2 = i2;
    }

    public void Addition()
    {
        this.result = this.iValue1 + this.iValue2;
    }

    public int GetResult()
    {
        return this.result.Value;
    }
}
```

This class is designed really simple to set the focus on the concept and not the calculation. First we will look deeper into it.
How would we use it? Right like this:

```csharp
var calculator = new SimpleCalculator();
calculator.SetStartValues(2, 5);
calculator.Adition();
var result = calculator.GetResult();
```

And we will see it works as expected if the user uses this sequence of calling the methods.
But we can not control the user, so it is possible that the user calls the methods in another order.

```csharp
var calculator = new SimpleCalculator();
calculator.Addition();
calculator.SetStartValues(2, 5);
var result = calculator.GetResult();
```

The result is, the app is crashing with an exception, after that the user looses the trust in our software,
even if everything is working well if the class is used correctly.
So we will take the possibility to always call every method and responsibility away from the user. It should be our job to design the class foolproof. The idea is to let the user just call methods fitting to the current state of the class. Sounds really simple and you will see, it is simple!

How can we achieve this? There are different ways to do it, but we will choose the way of creating nested stage classes. You are asking why not just using different interfaces and every interface implements one method? We could just return the right interface instead of using void methods. Yes that is true but it is not fool proofed. If our class implements all the interfaces, the user has the possibility to cast. And if it is crashing again the user will make us responsive for it. So we will use the stage classes instead.

TO BE CONTINUED...
