# Go By Example
[Go by Example](https://gobyexample.com/) is a hands-on introduction to Go using annotated example programs.
## Hello World
- To run the program, put the code in `hello-world.go` and use `go run hello-world.go`.
- To build our programs into binaries by using `go build`, then execute the built binary directly.
	```go
	package main
	
	import "fmt"
	
	func main() {
	    fmt.Println("hello world")
	}
	```
## Values
- Go has various value types including strings, integers, floats, booleans, etc.
- Strings, which can be added together with +.
	```go
	fmt.Println("go" + "lang")
	fmt.Println("1+1 =", 1+1)
	fmt.Println("7.0/3.0 =", 7.0/3.0)
	```
- Booleans with boolean operators.
	```go
	fmt.Println(true && false)
	fmt.Println(true || false)
	fmt.Println(!true)
	```

## Variables
- Variables are explicitly declared and used by the compiler e.g. to check type-correctness of function calls.
	```go
	var a = "initial"
	fmt.Println(a)
	```
- You can declare multiple variables at once - `var` declares 1 or more variables.
	```go
	var b, c int = 1, 2
	fmt.Println(b, c)
	```
- Go will infer the type of initialized variables.
	```go
	var d = true
	fmt.Println(d)
	```
- Variables declared without a corresponding initialization are _zero-valued_.
	```go
	var e int
	fmt.Println(e)
	```
- The `:=` syntax is shorthand for declaring and initializing a variable e.g., `var f string = "apple"`
	```go
	f := "apple"
	fmt.Println(f)
	```

## Constants
- Go supports constants of character, string, boolean, and numeric values.
- `const` declares a constant value.
	```go
	const s string = "constant"
	```
- A `const` statement can appear anywhere a `var` statement can.
- Constant expressions perform arithmetic with arbitrary precision.
	```go
	const n = 500000000
	const d = 3e20 / n
	fmt.Println(d)
	```
- A numeric constant has no type until it’s given one, such as by an explicit conversion.
	```go
	fmt.Println(int64(d))
	```
- A number can be given a type by using it in a context that requires one, such as a variable assignment or function call. For example, here `math.Sin` expects a `float64`.
	```go
	    fmt.Println(math.Sin(n))
	```

## For loops
- `for` is the only looping construct.
- The basic type with a single condition.
	```go
	i := 1
	for i <= 3 {
		fmt.Println(i)
	    i = i + 1
	}
	```
- A classic initial/condition/after `for` loop.
	```go
	  for j := 0; j < 3; j++ {
	    fmt.Println(j)
	}
	```
- Another way of accomplishing the basic “do this N times” iteration is `range` over an integer.
	```go
	for i := range 3 {
		fmt.Println("range", i)
	}
	```
- `for` without a condition will loop repeatedly until you either:
	- `break` out of the loop 
	- `return` from the enclosing function.
	```go
	for {
		fmt.Println("loop")
		break
	}
	```
- You can also `continue` to the next iteration of the loop.
	```go
	for n := range 6 {
		if n%2 == 0 {
			continue
		}
		fmt.Println(n)
	}
	```

## If/Else
- Branching with `if` and `else` in Go is straight-forward.
	```go
	if 7 % 2 == 0 {
		fmt.Println("7 is even")
	} else {
		fmt.Println("7 is odd")
	}
	```
- You can have an `if` statement without an else.
- Logical operators like `&&` and `||` are often useful in conditions.
	```go
	if 8 % 4 == 0 {
		fmt.Println("8 is divisible by 4")
	}

	if 8%2 == 0 || 7%2 == 0 {
		fmt.Println("either 8 or 7 are even")
	}
	```

- A statement can precede conditionals; any variables declared in this statement are available in the current and all subsequent branches.
- Note that you don’t need parentheses around conditions in Go, but that the braces are required.
	```go
	if num := 9; num < 0 {
		fmt.Println(num, "is negative")
	} else if num < 10 {
		fmt.Println(num, "has 1 digit")
	} else {
		fmt.Println(num, "has multiple digits")
	}
	```
- There is no "ternary if" in Go, so you’ll need to use a full `if` statement even for basic conditions.
## Switch
- Switch statements express conditionals across many branches.
	```go
	i := 2
	fmt.Print("Write ", i, " as ")
	switch i {
	case 1:
		fmt.Println("one")
	case 2:
		fmt.Println("two")
	case 3:
		fmt.Println("three")
	}
	```
- You can use commas to separate multiple expressions in the same `case` statement. We use the optional `default` case in this example as well.
	```go
	import (
	    "fmt"
	    "time"
	)
	
	.
	.
	.
	
	switch time.Now().Weekday() {
	case time.Saturday, time.Sunday:
		fmt.Println("It's the weekend")
	default:
		fmt.Println("It's a weekday")
	}
	```
- `switch` without an expression is an alternate way to express if/else logic. Here we also show how the `case` expressions can be non-constants.
	```go
	t := time.Now()
	switch {
	case t.Hour() < 12:
		fmt.Println("It's before noon")
	default:
		fmt.Println("It's after noon")
	}
	```
- A type `switch` compares types instead of values. 
- You can use this to discover the type of an interface value. 
- In this example, the variable `t` will have the type corresponding to its clause.
	```go
	whatAmI := func(i interface{}) {
		switch t := i.(type) {
		case bool:
			fmt.Println("I'm a bool")
		case int:
			fmt.Println("I'm an int")
		default:
			fmt.Printf("Don't know type %T\n", t)
		}
	}
	
	whatAmI(true)
	whatAmI(1)
	whatAmI("hey")
	```