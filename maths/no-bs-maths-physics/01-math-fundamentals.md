# 01 Math fundamentals
<br>

![Map of the fundamental math topics](fundamentals-map.png)
## 1.4 Functions and their inverses
By definition, $f^{-1}$ performs the opposite action of $f$ so together the two functions cancel each other out.

**Example:** Solving for $x$ in the equation $f(x) = c$. 
- The inverse function $f^{-1}$ to undo effects of $f$ 
- Then apply $f^{-1}$ to both sides of the equation $f^{-1}(f(x)) = x = f^{-1}(c)$

This notation is borrowed from the notion of inverse numbers $a^{-1}ax=1x=x$. In the case of functions, the negative-one exponent refers to the function’s inverse.
$$f^{−1}(y) = x\ such\ that\ f(x) = y$$
**Note:** in some cases, applying the inverse leads to multiple solutions.
- For example $f(x) = x^2$ maps $x$ and $−x$ to the same output value.
- The inverse function of $f(x) = x^2$ is $f^{-1} (x) = \sqrt x$
- This equation’s solutions can be indicated by $x=\pm\ \sqrt{ c }$
### Formulas
A list of common functions and their inverses:
- $f(x) ⇔ f^{-1}(x)$
- $x+2 ⇔ x - 2$
- $2x ⇔ \frac{1}{2}x$
-  $-x ⇔ -x$
- $x^2 ⇔ \pm\ \sqrt x$
- $2^x ⇔ \log_{2} (x)$
- $3x+5 ⇔ \frac{1}{3}(x-5)$
- $a^x ⇔ \log_a(x)$
- $exp(x) \equiv e^x ⇔ \ln(x) \equiv \log_{e}(x)$ 
- $sin(x) ⇔ sin^{-1}(x) \equiv arcsin(x)$
- $cos(x) ⇔ cos^{-1}(x) \equiv arccos(x)$
### Example
$...$
### Discussion
There’s no general formula for solving complicated equations
- technique of “digging toward $x$” is sufficient for most problems
- the rest requires solving the quadratic equation $ax^2 + bx + c = 0$.

Solving third-degree polynomial equations like $ax^3 + bx^2 + cx + d = 0$ is possible by hand, but might as well start using a computer.

The principle of “digging” toward the unknown by applying inverse functions is the key for solving all these types of equations.
## 1.5 Fractions
The rational numbers $\mathbb{Q}$ is the set of numbers written as a fraction of two integers: $$\mathbb{Q} \equiv \{\frac{m}{n} |\ \text{m and n are in}\ \mathbb{Z} \ \text{and}\ n \neq 0\}$$where $\mathbb{Z}$ denotes the set of integers $\mathbb{Z} ≡ \{. . . , −3, −2, −1, 0, 1, 2, 3, ...\}$.
### Definitions
The fraction “$a$ over $b$” can be written in different ways:
$$a/b \equiv a\ ÷\ b \equiv \frac{a}{b}$$
The top and bottom parts of a fraction have special names:
- $b$ is called the _denominator_ 
- $a$ is called the _numerator_

### Addition of fractions
If the denominators are the same, it makes sense to add the numerators since they refer to parts of the same whole: $\frac{1}{5} + \frac{2}{5}=\frac{3}{5}$

if the denominators are different, we rewrite the fractions so they have a _common denominator_ before we can add the numerators

We can obtain a common denominator by multiplying
- the first fraction by $\frac{d}{d} = 1$ 
- and the second fraction by $\frac{b}{b} = 1$.
$$\frac{a}{b}\ +\ \frac{c}{d}\ =\ \frac{a}{b}(\frac{d}{d})\ +\ (\frac{b}{b}) \frac{c}{d}\ =\ \frac{ad}{bd}\ +\ \frac{bc}{bd}$$
More generally, we can pick the least common multiple $LCM(b, d)$ to use as the common denominator.

The $LCM$ of two numbers is obtained by multiplying the numbers together and removing their common factors.
$$LCM(b, d)\ =\ \frac{b\ \times\ d}{GCD(b, d)}$$
where $GCD(b, d)$ is the greatest common divisor (largest number that divides both numbers) of $b$ and $d$.

**For example:** $\frac{1}{6}\ +\ \frac{1}{15}\ =\ \frac{5\ \times\ 1}{5\ \times\ 6}\ +\ \frac{1\ \times\ 2}{15\ \times\ 2}\ =\ \frac{5}{30}\ +\ \frac{2}{30}\ =\ \frac{7}{30}$

$LCM$ and $GCD$ is not required. If you use the common denominator $b\ \times\ d$, you will arrive at the same answer as above:
$$\frac{1}{6}\ +\ \frac{1}{15}\ =\ \frac{15\ \times\ 1}{15\ \times\ 6}\ +\ \frac{1\ \times\ 6}{15\ \times\ 6}\ =\ \frac{15}{90}\ +\ \frac{6}{90}\ =\ \frac{21}{90}\ =\ \frac{7}{30}$$
### Multiplication of fractions
Multiply the numerators together and multiply the denominators together:
$$\frac{a}{b}\ \times\ \frac{c}{d}\ =\ \frac{a\ \times\ c}{b\ \times\ d}\ =\ \frac{ac}{bd}$$
### Division of fractions
Compute the product of the first fraction times the second fraction flipped:
$$\frac{a/b}{c/d}\ =\ \frac{a}{b} \div \frac{c}{d}\ =\ \frac{a}{b}\ \times\ \frac{d}{c}\ =\ \frac{a\ \times\ d}{b\ \times\ c}\ =\ \frac{ad}{bc}$$
### Whole and fraction notation
To indicate an improper fraction like $\frac{5}{3}$ which is greater than $1$, we sometimes use the $1\frac{2}{3}$ notation.
### Repeating decimals
We use the overline notation to indicate the digit(s) that repeat in the expansion:
$$\frac{1}{3}\ =\ 0.3\ =\ 0.333\dots; \frac{1}{7}\ =\ 0.\overline{142857}\ =\ 0.14285714285714\dots$$
## 1.6 Basic rules of algebra
The general rules for manipulating numbers and variables, a process otherwise known as algebra.

An expression contains _terms_, which are usually composed of many things multiplied together.

When number $x$ is obtained as the product of other numbers like $x = abc$.
- we say “$x$ factors into $a$, $b$, and $c$”
- and $a$, $b$ and $c$ are the factors of $x$

Given $a$, $b$, $c$, $d$, we can apply the following algebraic properties:
1. Associative property: 
	- $a + b + c = (a + b) + c = a + (b + c)$ 
	- $abc = (ab)c = a(bc)$
2. Commutative property: $a + b = b + a and ab = ba$
3. Distributive property: $a(b + c) = ab + ac$

We use the distributive property every time we _expand_ brackets
$$a(b + c + d) = ab + ac + ad$$
The brackets indicate the expression $(b + c + d)$ must be treated as a whole 
- a factor that consists of three terms
- multiplication $a(b + c + d)$ is equivalent to multiplying each term by $a$

The opposite of expanding is _factoring_, which consists of rewriting the expression with the common parts taken out in front of a bracket.
$$ab + ac = a(b + c)$$
### Expanding brackets
The distributive property is useful when dealing with polynomials:
$$(x + 3)(x + 2)$$
$$x(x + 2) + 3(x + 2)$$
$$x^2 + x2 + 3x + 6$$
$$x^2 + 5x + 6$$
**Abstract form:** $(x + a)(x + b) = x^2 + (a + b)x + ab$
- The product of two linear terms is equal to a quadratic expression
- The middle term on the RHS contains the _sum_ of the two constants on the LHS $(a + b)$.
- The third term contains their product $ab$.

**Example:** 
$(x + a)(bx^2 + cx + d)$
$\ = x(bx^2 + cx + d) + a(bx^2 + cx + d)$
$\ = bx^3 + cx^2 + dx + abx^2 + acx + ad$
$\ = bx^3 + (c + ab)x^2 + (d + ac)x + ad$

**Note:** the pattern of grouping all terms containing $x^2$ and $x$ into separate terms is used when dealing with expressions containing different powers of $x$.

**Example 2:** 
Solve for $t$ in the equation $7(3 + 4t) = 11(6t − 4)$
1. Bring all $t$ terms to one side and all constant terms to the other side.
	$21 + 28t = 66t − 44$
2. Relocate all $ts$ to the equation’s RHS and all constants to the LHS:
	$21 + 44 = 66t − 28t$
3. $t$ is contained in both terms on the RHS, so we can rewrite it as:
	$21 + 44 = (66 − 28)t$

$$t\ =\ \frac{21+44}{66-28}\ =\ \frac{65}{38}$$
### Factoring
Factoring involves taking out the common part(s) of a expression.

**Example:** Simplify $6x^2y + 15x$ by taking out common factors.

The expression has two terms and each term can be split into its constituent factors:
$$6x^2y + 15x = (3)(2)(x)(x)y + (5)(3)x$$
Since factors x and 3 appear in both terms, we can _factor them out_:
$$6x^2y + 15x = 3x(2xy + 5)$$
Expressions shows $3x$ is common to both terms.

**Example 2:** 
$$2x^2y + 2x + 4x = 2x(xy + 1 + 2) = 2x(xy + 3)$$
### Quadratic factoring
It is often useful to rewrite the function as a product of two factors.
$...$

### Completing the square
$...$

## 1.8 Exponents
The notation is used to denote some number $b$ $multiplied by itself $n$ times.
$b^n = \underbrace{b\cdot b \cdot \ldots \cdot b}_{n \text{ times}}$
### Definitions
The fundamental ideas of exponents:
- $b^n$ is the number $b$ raised to the power $n$
	- $b$: the base
	- $n$: the exponent/power of $b$
 - $b^0$ = 1

Important exponential functions, $f : \mathbb{R} \to \mathbb{R}$
- $b^x$: the exponential function base $b$
- $10^x$: the exponential function base $10$
- $exp(x) \equiv e^x$: the exponential function base $e$ (the Euler’s number)
- $2^x$: the exponential function base $2$

**Special bases:**
- _Natural base:_ $e = 2.7182818\dots$
- _Base 10:_ we use the decimal system for our numbers
	- $1 000 = 10^3, 1 000 000 = 10^6$
### Properties
1. Multiplying together two exponential expressions that have the same base is the same as adding the exponents:
$$b^m b^n = \underbrace{bbb \cdots bb}_{m \text{ times }}\ \underbrace{bbb \cdots bb}_{n \text{ times}} = \underbrace{bbbbbb \cdots bb}_{m+n \text{ times}} = b^{m+n}$$
2. Division by a number can be expressed as an exponent of minus one:
$$b^{-1} \equiv \frac{1}{b}$$
	A negative exponent corresponds to a division:
$$b^{-n} = \frac{1}{b^n}$$
3. By combining Property 1 and Property 2 we obtain the following rule:
	$$\frac{b^m}{b^n} = b^{m-n}$$
	In particular: $b^nb^{−n} = b^{n−n} = b^0 = 1$
	- Multiplication by $b^{−n}$ is the inverse operation of multiplication by $b^n$
	- The net effect of the combination of both operations is the same as multiplying by one, i.e., the identity operation.

4. When an exponential expression is exponentiated, the inner exponent and the outer exponent multiply:
$$(b^m)^n = \underbrace{\underbrace{(bbb\cdots bb)}_{m\text{ times}}\ \underbrace{(bbb\cdots bb)}_{m\text{ times}}\cdots\underbrace{(bbb\cdots bb)}_{m\text{ times}}}_{n\text{ times}} = b^{mn}$$
5. $(ab)^n = \underbrace{(ab)(ab)(ab)\cdots(ab)(ab)}_{n\text{ times}} = \underbrace{aaa\cdots aa}_{n\text{ times}}\ \underbrace{bbb\cdots bb}_{n\text{ times}} = a^nb^n$

6. $\left(\frac{a}{b}\right)^n = \underbrace{\left(\frac{a}{b}\right)\left(\frac{a}{b}\right)\left(\frac{a}{b}\right)\cdots\left(\frac{a}{b}\right)\left(\frac{a}{b}\right)}_{n\text{ times}} = \frac{\overbrace{aaa\cdots aa}^{n\text{ times}}}{\underbrace{bbb\cdots bb}_{n\text{ times}}} = \frac{a^n}{b^n}$

7. Raising a number to the power $\frac{1}{n}$ is equivalent to finding the $n^{th}$ root of the number:
$$b^{\frac{1}{n}} \equiv \sqrt[3]{b}$$
	In particular, the square root corresponds to the exponent of one half $\sqrt{b} = b^{\frac{1}{2}}$
	- The cube root (the inverse of $x^3$ ) corresponds to $\sqrt[3]{b} \equiv b^{\frac{1}{3}}$.
	- Properties 5.1 and 5.2 also apply for fractional exponents:
$$\sqrt[n]{ab} = (ab)^{\frac{1}{n}} = a^{\frac{1}{n}}b^{\frac{1}{n}} = \sqrt[n]{a}\sqrt[n]{b}, \quad \sqrt[n]{\left(\frac{a}{b}\right)} = \left(\frac{a}{b}\right)^{\frac{1}{n}} = \frac{a^{\frac{1}{n}}}{b^{\frac{1}{n}}} = \frac{\sqrt[n]{a}}{\sqrt[n]{b}}$$
### Even and odd exponents
The function $f(x) = x^n$ behaves differently depending on whether the exponent $n$ is even or odd.
### Scientific notation
The number is expressed as: a decimal between $1.0$ and $9.9999\dots \times 10^n$
- The effect of multiplying by $10^8$ is to move the decimal point eight steps to the right, making the number bigger.
- Multiplying by $10^{−6}$ has the opposite effect, moving the decimal to the left by six steps and making the number smaller.

Scientific notation is useful because it allows us to clearly see the size of numbers: $1.23 \times 10^6$ is $1 230 000$ whereas $1.23×10^{−10}$ is $0.000 000 000 123$.

The number of decimal places we use when specifying a certain physical quantity is usually an indicator of the precision with which we are able to measure this quantity.

On computer systems, _floating point numbers_ are represented in scientific notation:
- $2.99792458e8$ instead of $2.99792458 \times 10^8$
- $1.256637e-6$ instead of $1.256637 \times 10^{-6}$
## 1.9 Logarithms
Logarithms are used to compare very large numbers and very small numbers on the same scale.
### Definitions
- $log_b(x)$: the logarithm of $x$ base $b$ is the inverse function of $b^x$
- $ln(x)$: the “natural” logarithm base $e$ is the inverse of $e^x$
- $log_2(x)$: the logarithm base $2$ is the inverse of $2^x$ .

### Formulas
Logarithms are defined as the inverses of their corresponding exponential functions.
$$\log_{b}(x) = m ⇔ b^m = x$$
Logarithms with base $e$ - $ln(x)$ - for “logarithme naturel” because $e$ is the “natural” base.

Another special base is $10$ because our numbers are based on the decimal system.
- $\log_{10}(x)$ tells us roughly the size of $x$ — how many digits the number has

**Example:** The number of figures $N_S$ in a salary is calculated as 1 plus the logarithm base 10 of the salary $S$.
$$N_{S} = 1 + log_{10}(S)$$
Solve for $S$ given $N_S=7$ to find the smallest 7 figure salary: $$7=1+log_10(S)$$$$6=\log_{10}(S)$$Using the inverse relationship logarithm between base 10 and exponentiation base 10.
$$S=10^6=1000000$$
### Properties
1. The sum of two logarithms is the logarithm of the product of the arguments.
$$\log(x)+\log(y)=\log(xy)$$
2. When you have a logarithm of a power, you can bring the exponent $k$ to the front as a coefficient. $$\log(x^k)=k\log(x)$$
3. The difference of logarithms equals the logarithm of the quotient 
   $$\log(x)-\log(y)=\log\big(\frac{x}{y}\big)$$
4. This property helps us change from one base to another.
   $$\log_B(x) = \frac{\log_b(x)}{\log_b(B)}$$
   For example, the $log_{10}$ of a number $S$ can be expressed as a $log_2$ or $ln$:
   $$\log_{10}(S) = \frac{\log_{10}(S)}{1} = \frac{\log_{10}(S)}{\log_{10}(10)} = \frac{\log_2(S)}{\log_2(10)} = \frac{\ln(S)}{\ln(10)}$$
**Proof for properties 1, 2 and 3**
Show that the expression on the left is equal to the expression on the right.$$b^mb^n=b^{m+n}$$
If we define some new variables $x$ and $y$ such that $b^m = x$ and $b^n = y$:
$$xy=B^{m+n}$$
Taking the logarithm of both sides gives:
$$\log_b(xy) = \log_b(b^{m+n}) = m + n = \log_b(x) + \log_b(y)$$
The last step above uses the definition of the log function again:
$$b^m = x \Leftrightarrow m = \log_b(x) \quad \text{and} \quad b^n = y \Leftrightarrow n = \log_b(y)$$
## 1.13 Functions
We use functions to describe the relationships between variables. 
- In particular, functions describe how one variable depends on another (modelling reality).

**For example:**
- The revenue $R$ from a music concert depends on the number of tickets sold $n$.
- If each ticket costs $25, the revenue from the concert can be written as a function of $n$:
	- $R(n) = 25n$

To “know” a function, you must be able to understand and connect several of its aspects.
- **definition**, which describes exactly what the function does
- **graph** of the function; what the function looks like if you plot $x$ versus $f(x)$
- **values** of the function for some important inputs
- **relations** of the function to other functions
### Definitions
A function is a mathematical object that takes numbers as inputs and gives numbers as outputs.
- $f : A \to B$ denotes a function from the input set $A$ to the output set $B$.

Terms used to describe the input and output sets:
- The _domain_ of a function is the set of allowed input values.
- The _image_ or _range_ of the function $f$ is the set of all possible output values of the function.
- The _codomain_ of a function describes the type of outputs the function has.

Difference between the image of a function and its codomain:
- The quadratic function $f(x)=x^2$ is of the form $f: \mathbb{R} \to \mathbb{R}$.
- However, not all outputs are possible.
- The image of $f(x)=x^2$ consists only of the nonnegative real numbers.

A function is not a number; it is a mapping from numbers to numbers. For any input $x$, the output value of $f$ for that input is denoted $f(x)$. 

Hence, we say “$f$ maps $x$ to $f(x)$”.

Terminology to classify the type of mapping that a function performs:
- A function is _one-to-one_ or _injective_ if it maps different inputs to different outputs.
- A function is _onto_ or _surjective_ if it covers the entire output set.
	- In other words, if the image of the function is equal to the function’s codomain.
- A function is _bijective_ if it is both _injective_ and _surjective_. 
	- In this case, $f$ is a one-to-one correspondence between the input set and the output set.
	- For each of the possible outputs $y ∈ Y$ (surjective part), there exists exactly one input $x ∈ X$, such that $f(x) = y$ (injective part).
### Function composition
Combining two simple functions by chaining them together to build a more complicated function.

The function $f \circ g: A → C$ is defined through the formula $f \circ g (x) ≡ f(g(x))$

**For example:** $f \circ g (x) \equiv f(g(x)) = z$
1. First, $g: A \to B$ acts on some input $x$ to produce an intermediary value $y = g(x)$ in the set $B$.
2. The intermediary value $y$ is then passed through $f: B \to C$.
3. The final output value $z = f(y) = f(g(x))$ in the set $C$.
### Inverse function
Given a bijective function $f: A \to B$, there exists an inverse function $f^{−1}: B \to A$, which performs the inverse mapping of $f$.

If you start from some $x$, apply $f$, and then apply $f^{−1}$.
$f^{−1}(f(x)) \equiv f^{−1} \circ f(x) = x$

### Handles on functions
The main handle for a function is its **definition**, but it is also important to “feel” what the function does intuitively.

**Table of values**
One simple way to represent a function is to pick random inputs and create a table of values i.e., a list of input-output pairs: $\{(x1, f(x1)), (x2, f(x2)), (x3, f(x3)), . . .\}$

**Function graph**
The horizontal axis, sometimes called the *abscissa*, is used to measure $x$.

The vertical axis is used to measure $f(x)$ — alias for the output value of $f$ is $y ≡ f(x)$

Each input-output pair of the function $f$ as a point $(x, y)$ in the coordinate system.

**Facts and properties**
- An example of a mathematical fact is $\sin(30 \deg) = \frac{1}{2}$
- An example of a mathematical relation is the equation $\sin^2x + \cos^2x = 1$, which indicates a link between the $sin$ function and the $cos$ function.

To develop mathematical skills, it is vital to practice path-building between related concepts by solving exercises and reading and writing mathematical proofs
## 1.14 Function reference
### Line
The equation of a line describes an input-output relationship where the change in the output is _proportional_ to the change in the input.
$$f(x) = mx + b$$
where constant $m$ describes the slope of the line and constant $b$ is the _y-intercept_ — value of the function when $x = 0$

![[./images/linear.jpg|center|500]]
#### Properties
- Domain: $x ∈ \mathbb{R}$ - defined for all input values $x ∈ \mathbb{R}$
- Image: $x ∈ \mathbb{R}$ if $m \neq 0$. If $m = 0$ the function is constant.
  $f(x) = b$, so the image set contains only a single number $\{b\}$.
- $b/m$: the x-intercept of $f(x) = mx + b$, obtained by solving $f(x) = 0$.
- A unique line passes through any two points $(x_{1}, y_{1})$ and $(x_{2}, y_{2})$ if $x_{1} \neq x_2$.
- The inverse to the line $f(x) = mx + b$ is $f^{−1}(x) = \frac{1}{m}(x − b)$, which is also a line.

#### General equation
A line can also be described in a more symmetric form as a relation:
$$Ax + By = C$$
Given the general equation of a line, you can convert to the function form $y = f(x) = mx + b$ using $b = \frac{C}{B}$ and $m = \frac{−A}{B}$.
### Square
The formula for the quadratic function (or parabola) is:
$$f(x)=x^2$$

![[./images/quadratic.jpg|center|500]]
#### Properties
- Domain: $x ∈ \mathbb{R}$
  The function $f(x) = x^2$ is defined for all input values $x ∈ \mathbb{R}$.
- Image: $f(x) \in [0, \infty$
  The outputs are never negative: $x 2 \geq 0$, for all $x ∈ \mathbb{R}$.
- The function $x^2$ is the inverse of the square root function $\sqrt{x}$.
- $f(x) = x^2$ is _two-to-one:_ it sends both _x_ and _−x_ to the same output value $x^2 = (−x)^2$.
- The quadratic function is *convex* — it curves upward.
### Square root
The square root function is denoted as:
$$f(x) = \sqrt{x} \equiv \frac{1}{2}$$
The square root is the inverse function of the square function for $x \geq 0$. The symbol $\sqrt{c}$ refers to the positive solution of $x^2 = c$. $-\sqrt{c}$ is also a solution of $x^2 = c$.
 ![|500][./images/square-root.jpg|center
#### Properties
- Domain: $x \in [0, \infty$
  The function is only defined for non-negative inputs $x \geq 0$.
  There is no real number $y$ such that $y^2$ is negative, hence is not defined for negative $x$.
- Image: $f(x) \in [0, \infty$
  The outputs of the function are never negative: $\sqrt{x} \geq 0$, for all $x \in [0, \infty$.

In general, we can define the $n^{th}$ root function $\sqrt[n]{x}$ as the inverse function of $x^n$.
### Absolute value
The absolute value function specifies the _size_ of numbers, ignoring the sign. Thus, a number’s absolute value corresponds to its distance from the origin of the number line.
$$f(x) = |x| = \begin{cases} x & \text{if } x \geq 0, \\ -x & \text{if } x < 0. \end{cases}$$

![[./images/absolute.jpg|center|500]]
#### Properties
- Always returns a non-negative number
- The combination of square followed by square-root is equivalent to the absolute function.
### Polynomial functions
The general equation for a polynomial function of degree $n$:
$$f(x)=a_{0}+a_{1}x+a_{2}x^2+a_{3}x^3+\dots+a_{n}x^n$$
The constants $a_i$ are known as the *coefficients*.
#### Parameters
- $n$: the _degree_ of the polynomial
- $a_{0}$: the constant term
- $a_1$: the *linear* coefficient, or first-order coefficient
- $a_2$: the *quadratic* coefficient
- $a_3$: the *cubic* coefficient
- $a_n$: the $n^{th}$ order coefficient
#### Properties
- Domain: $x \in \mathbb{R}$ - defined for all inputs $x \in \mathbb{R}$
- Image: depends on the coefficients
- Sum of two polynomials is also a polynomial.
#### Even and odd functions
Depending on the choice of degree and coefficients, a polynomial function can take on many different shapes.

Observations about symmetries of polynomials:
- If a polynomial contains only even powers of $x$, it is an _even_ polynomial. Even polynomials have the property $f(x) = f(−x)$, where the sign of the input doesn't matter.
- Odd polynomials have the property $g(x) = −g(−x)$.

	This terminology applies to all functions.
### Sine
The sine function represents a fundamental unit of vibration. The graph of $sin(x)$ _oscillates_ up and down and crosses the $x$-axis multiple times.
$$f(x) = sin(x)$$

![[./images/sine.jpg|center|500]]
- The graph starts from (0, 0) and smoothly increases until it reaches the maximum value at $x=\frac{\pi}{2}$.
- Afterward, the function comes back down to cross the $x$-axis at $x = \pi$.
- After $\pi$, the function drops below the $x$-axis and reaches minimum value of $−1$ at $x = \frac{3\pi}{2}$.
- It then travels up again to cross the $x$-axis at $x = 2\pi$.

This $2\pi$-long cycle repeats after $x = 2\pi$, hence the function is called periodic — the shape of the graph repeats.

![[./images/sine-3.jpg|center|center|500]]
#### Properties
- Domain: $x \in \mathbb{R}$ - defined for all input values $x \in \mathbb{R}$.
- Image: $sin(x) \in [−1, 1]$
- Roots: $[\dots, −3\pi, −2\pi, −\pi, 0, \pi, 2\pi, 3\pi, \dots]$
	- The function $sin(x)$ has roots at all multiples of $\pi$
- The function is periodic, with period $2\pi$: $sin(x) = sin(x + 2\pi)$.
- The sin function is odd: $sin(x) = −sin(−x)$.
- Relation to cos: $sin^2x + cos^2x = 1$
- Relation to csc: $csc(x) \equiv \frac{1}{sin x}$ (csc is read cosecant)
- The inverse function of $sin(x)$ is $sin^{−1}(x)$
	- Not $(\sin(x))^{−1} = \frac{1}{\sin(x)} \equiv \csc(x)$.
	- Sometimes the function $sin^{−1}(x)$ is denoted $arcsin(x)$
- The number $\sin(\theta)$ is the length-ratio of the vertical side and the hypotenuse in a right-angle triangle with angle $\theta$ at the base.

### Cosine
The cosine function is the same as the sine function shifted by $\frac{\pi}{2}$ to the left:
$$\cos(x) = \sin(x + \frac{π}{2})$$
Everything that applies to sine function also applies to the cosine function.

![[./images/cosine.jpg|center|500]]
#### Properties
- Domain: $x \in \mathbb{R}$
- Image: $\cos(x) \in [-1, 1]$
- Roots: $[\dots, −\frac{3\pi}{2}, −\frac{\pi}{2}, \frac{\pi}{2}, \frac{3\pi}{2}, \frac{5\pi}{2}, \dots]$
- Relation to sin: $\sin^2x + cos^2x = 1$
- Relation to sec: $\sec(x) \equiv \frac{1}{\cos x}$ (sec is read secant)
- The inverse function of $cos(x)$ is denoted $\cos^{−1}(x)$
- The cos function is even: $\cos(x) = \cos(−x)$
- The number $\cos(\theta)$ is the length-ratio of the horizontal side and the hypotenuse in a right-angle triangle with angle $\theta$ at the base.
### Tangent
The tangent function is the ratio of the sine and cosine functions:
$$f(x) = \tan(x) \equiv \frac{\sin(x)}{\cos(x)}$$

![[./images/tangent.jpg|center|500]]
#### Properties
- Domain: $\{x \in \mathbb{R} \mid x \neq \frac{(2n+1)\pi}{2} \text{ for any } n \in \mathbb{Z}\}$
- Range: $x \in \mathbb{R}$
- The function tan is periodic with period $\pi$
- The $\tan$ function “blows up” at values of $x$ where $cos x = 0$
	- These are called asymptotes of the function
	- Their locations are $x = \ldots, \frac{-3\pi}{2}, \frac{-\pi}{2}, \frac{\pi}{2}, \frac{3\pi}{2}, \ldots$
- Value at $x = 0$: $\tan(0) = \frac{0}{1} = 0$, because $sin(0) = 0$
- The number $\tan(\theta)$ is the length-ratio of the vertical and the horizontal sides in a right-angle triangle with angle $\theta$.
- The inverse function of $\tan(x)$ is $\tan^{−1}(x)$
- The inverse tangent function is used to compute the angle at the base in a right-angle triangle with horizontal side length $\ell_{h}$ and vertical side length $\ell_v$
  $\tan^{-1}\left(\frac{\ell_v}{\ell_h}\right)$
### Exponential
The exponential function base $e = 2.7182818\dots$
$$ f(x)=e^x\equiv \exp(x)$$

![[./images/exponential.jpg|center|500]]
#### Properties
- Domain: $x \in \mathbb{R}$ 
- Range: $e^x \in (0, \infty$
- The multiplication of exponential functions with the same base means that you add the exponents.
$$f(a)f(b)=f(a+b)\ since\ e^ae^b=e^{a+b}$$
- The derivative (the slope of the graph) is the exponential function: 
$$f(x) = e^x \implies f'(x) = e^x$$

In general, $f(x)=Ae^{\gamma x}$ where $A$ is the initial value and $\gamma$ is the _rate_ of the exponential.
- **For $\gamma > 0$,** the function $f(x)$ is increasing like in the image.
- **For $\gamma<0$,** the function is decreasing and tends to 0 for large values of $x$.
- $\gamma = 0$ is a special case since $e^0 = 1$, so $f(x)$ is a constant of $f(x)=A1^x=A$. 
### Natural logarithm
The natural logarithm function, the inverse function of the exponential $e^x$:
$$f(x) = ln(x) = log_{e}(x)$$

![[./images/natural_log.jpg|center|500]]
### Function transformations
$\dots$
### General quadratic function
The general quadratic function takes the form
$$f(x) = A(x − h)^2 + k$$
where $x$ is the input, and $A$, $h$, and $k$ are the parameters.
#### Parameters
- $A$: the slope multiplier
	- The larger $abs(A)$, the steeper the slope.
	- If $A < 0$, the function opens downward.
- $h$: the horizontal displacement of the function
	- Notice that subtracting a number inside the bracket makes the function go to the right.
- $k$: the vertical displacement of the function
#### Graph
The graph illustrates a quadratic function with parameters $A = 1$, $h = 1$, and $k = −2$.

![[./images/general-quadratic-fn.jpg|center|500]]

If a quadratic crosses the $x$-axis:  $f(x)=A(x-a)(x-b)$, where $a$ and $b$ are the roots.
Another common way of writing a quadratic function is $f(x) = Ax^2 + Bx + C$.
#### Properties
- There is a unique quadratic function that passes through any three points $(x_1, y_1)$, $(x_2, y_2)$ and $(x_3, y_3)$ if $x_1 \neq x2$, $x_2 \neq x_3$, and $x_1 \neq x_3$.
- The derivative of $f(x) = Ax^2 + Bx + C$ is $f'0(x) = 2A^x + B$.
### General sine function
Introducing all possible parameters into the sine function:
$$f(x) = A\sin \bigg(\frac{2\pi}{\lambda}x - \phi\bigg)$$
where $A$, $\lambda$, and $\phi$ are the function’s parameters.
#### Parameters
- $A$: the amplitude describes the distance above and below the $x$-axis that the function reaches as it oscillates.
- $\lambda$: the _wavelength_ of the function 
$$\lambda = \text{\{ the distance from one peak to the next \}}$$
- $\phi$: is a phase shift, analogous to the horizontal shift $h$
	- This number dictates where the oscillation starts
	- The default sine function has $\phi=0$, so it passes through the origin with an increasing slope.

The function $f(x) = \sin(x)$ has wavelength $2\pi$ and produces outputs that oscillate between $−1$ and $1$.

Multiplying the bare function by constant $A$ results in oscillations ranging between $−A$ and $A$.

When the input $x$ is scaled by the factor $\frac{2\pi}{\lambda}$ , the wavelength of the function becomes $\lambda$.
## 1.15 Polynomials

## 1.16 Trigonometry

## 1.17 Trigonometric identities

## 1.18 Geometry

## 1.19 Circle

## 1.20 Ellipse

