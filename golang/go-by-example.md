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

## Arrays
- An array is a numbered sequence of elements of a specific length. In typical Go code, slices are much more common; arrays are useful in some special scenarios.
- An array `a` that will hold exactly 5 `int`s. The type of elements and length are both part of the array’s type. 
- By default an array is zero-valued, which for `int`s means `0`s.
	```go
	var a [5]int
	fmt.Println("emp:", a)
	
	a[4] = 100
	fmt.Println("set:", a)
	fmt.Println("get:", a[4])

	fmt.Println("len:", len(a))
	```
- To declare and initialize an array in one line:
	```go
	b = [...]int{1, 2, 3, 4, 5}
	fmt.Println("dcl:", b)
	```
- If you specify the index with `:`, the elements inbetween will be zeroed.
	```go
	b = [...]int{100, 3: 400, 500}
	fmt.Println("idx:", b)
	```
- You can compose types to build multi-dimensional data structures.
	```go
	var twoD [2][3]int
	for i := 0; i < 2; i++ {
		for j := 0; j < 3; j++ {
			twoD[i][j] = i + j
		}
	}
	fmt.Println("2d: ", twoD)
	```
	```go
	twoD = [2][3]int{
		{1, 2, 3},
		{1, 2, 3},
	}
	fmt.Println("2d: ", twoD)
	```

## Slices
- Slices are an important data type in Go, giving a more powerful interface to sequences than arrays.
	```go
	import (
		"fmt"
		"slices"
	)
	```
- Unlike arrays, slices are typed only by the elements they contain (not the number of elements).
- An uninitialized slice equals to nil and has length 0.
	```go
	var s []string
	fmt.Println("uninit:", s, s == nil, len(s) == 0)
	```
- To create an empty slice with non-zero length, use the builtin `make`. Here we make a slice of `string`s of length `3` (initially zero-valued).
- By default a new slice's capacity is equal to its length; if we know the slice is going to grow ahead of time, it's possible to pass a capacity explicitly as an additional parameter to `make`.
	```go
	s = make([]string, 3)
	fmt.Println("emp:", s, "len:", len(s), "cap:", cap(s))

	s[0] = "a"
	s[1] = "b"
	s[2] = "c"
	fmt.Println("set:", s)
	fmt.Println("get:", s[2])

	fmt.Println("len:", len(s))
	```
- In addition to these basic operations, slices support several more that make them richer than arrays. One is the builtin `append`, which returns a slice containing one or more new values.
- Note that we need to accept a return value from `append` as we may get a new slice value.
	```go
	s = append(s, "d")
	s = append(s, "e", "f")
	fmt.Println("apd:", s)
	```
- Slices can also be `copy`'d. 
- Here we create an empty slice `c` of the same length as `s` and copy into `c` from `s`.
	```go
	c := make([]string, len(s))
	copy(c, s)
	fmt.Println("cpy:", c)
	```
- Slices support a "slice" operator with the syntax `slice[low:high]`. For example, this gets a slice of the elements `s[2]`, `s[3]`, and `s[4]`.
	```go
	l := s[2:5]
	fmt.Println("sl1:", l)
	```
- This slices up to (but excluding) `s[5]`.
	```go
	l = s[:5]
	fmt.Println("sl2:", l)
	```
- And this slices up from (and including) `s[2]`.
	```go
	l = s[2:]
	fmt.Println("sl3:", l)
	```
- We can declare and initialize a variable for slice in a single line as well.
	```go
	t := []string{"g", "h", "i"}
	fmt.Println("dcl:", t)
	```
- The `slices` package contains a number of useful utility functions for slices.
	```go
	t2 := []string{"g", "h", "i"}
	if slices.Equal(t, t2) {
		fmt.Println("t == t2")
	}
	```
- Slices can be composed into multi-dimensional data structures. 
- The length of the inner slices can vary, unlike with multi-dimensional arrays.
	```go
	twoD := make([][]int, 3)
	for i := 0; i < 3; i++ {
		innerLen := i + 1
		twoD[i] = make([]int, innerLen)
		for j := 0; j < innerLen; j++ {
			twoD[i][j] = i + j
		}
	}
	fmt.Println("2d: ", twoD)
	```
- Note that while slices are different types than arrays, they are rendered similarly by `fmt.Println`.|
- Extra: https://go.dev/blog/slices-intro
## Maps
- Maps are Go’s built-in associative data type (sometimes called hashes or dicts in other languages).
	```go
	import (
	    "fmt"
	    "maps"
	)
	```
- To create an empty map, use the built-in `make(map[key-type]val-type)`.
- Printing a map with e.g. `fmt.Println` will show all of its key/value pairs.
	```go
	m := make(map[string]int)
	
	m["k1"] = 7
	m["k2"] = 13
	
	fmt.Println("map:", m)
	
	v1 := m["k1"]
	fmt.Println("v1:", v1)

	fmt.Println("len:", len(m))
	```
- The builtin `delete` removes key/value pairs from a map.
	```go
	delete(m, "k2")
	fmt.Println("map:", m)
	```
- To remove all key/value pairs from a map, use the `clear` built-in.
	```go
    clear(m)
    fmt.Println("map:", m)
	```
- The optional second return value when getting a value from a map indicates if the key was present in the map. 
- This can be used to disambiguate between missing keys and keys with zero values like `0` or `""`. 
- Here we didn’t need the value itself, so we ignored it with the _blank identifier_ `_`.
	```go
	_, prs := m["k2"]
	    fmt.Println("prs:", prs)
	```
- You can also declare and initialize a new map in the same line:
	```go
	  n := map[string]int{"foo": 1, "bar": 2}
	    fmt.Println("map:", n)
	```
- The `maps` package contains a number of useful utility functions for maps.
	```go
    n2 := map[string]int{"foo": 1, "bar": 2}
    if maps.Equal(n, n2) {
        fmt.Println("n == n2")
    }
	```
- Note that maps appear in the form `map[k:v k:v]` when printed with `fmt.Println`.

## Functions
- A function that takes two `int`s and returns their sum as an `int`.
- Go requires explicit returns, i.e. it won’t automatically return the value of the last expression.
	```go
	func plus(a int, b int) int {
		return a + b
	}
	```
- For multiple consecutive parameters of the same type, you may omit the type name for the like-typed parameters up to the final parameter that declares the type.
	```go
	func plusPlus(a, b, c int) int {
	    return a + b + c
	}
	```
- Call a function just as you’d expect, with `name(args)`.
	```go
	func main() {
	
	    res := plus(1, 2)
	    fmt.Println("1+2 =", res)
	
	    res = plusPlus(1, 2, 3)
	    fmt.Println("1+2+3 =", res)
	}
	```

## Multiple Return Values
- Go has built-in support for _multiple return values_. 
- Often in idiomatic Go e.g., to return both result and error values from a function.
- The `(int, int)` in this function signature shows that the function returns 2 `int` values.
	```go
	func vals() (int, int) {
	    return 3, 7
	}
	```
- We use the 2 different return values from the call with _multiple assignment_.
- If you only want a subset of the returned values, use the blank identifier `_`.
	```go
	func main() {
	    a, b := vals()
	    fmt.Println(a)
	    fmt.Println(b)
	    
	    _, c := vals()
	    fmt.Println(c)
	}
	```
- Another feature: accepting a variable number of arguments.
## Variadic Functions
- Variadic functions can be called with any number of trailing arguments.
- For example, a function that will take an arbitrary number of `int` values as arguments. The type of `nums` is equivalent to `[]int`. 
- We can call `len(nums)`, iterate over it with `range`, etc.
	```go
	func sum(nums ...int) {
	    fmt.Print(nums, " ")
	    total := 0
	
	    for _, num := range nums {
	        total += num
	    }
	    fmt.Println(total)
	}
	```
- Variadic functions can be called in the usual way with individual arguments.
- If you already have multiple args in a slice, apply them to a variadic function using `func(slice...)`:
	```go
    sum(1, 2)
    sum(1, 2, 3)

    nums := []int{1, 2, 3, 4}
    sum(nums...)
	```
- Another key aspect of functions in Go is their ability to form closures.