# Abstract Algebra via CS

What are numbers? I'm sure you can name many numbers. I'm also sure you know at least a handful of ways to combine numbers (addition, multiplication, etc.).

Being able to do these things is essential, but they don't tell us what numbers *are*. What distinguishes numbers from functions or strings or any other object that we wouldn't consider a number? After all, we can name and combine strings and functions, too.

Exploring questions like this form the basis of **abstract algebra**.

## Intuition vs. Formalism

We have some intuitive idea of what numbers are, which is how we can say things like "5 is a number", "2 + 4 is 7", etc. and feel confident we're making sense.

This still makes them pretty slippery. How do we know that we can add *any* pair of numbers? How do we know that every integer is either even or odd? A big part of "doing math" is making our intuitions precise enough that we can reason about them with 100% confidence.

This is also how most mathematical definitions come about. They're the definitions that seem to fit our intuitions best. Once the definitions are precise enough, we can see what conclusions follow if we adopt them.

A counterintuitive conclusion is like a bug in software. When something unexpected happens in software, a combination of two things is happening:

1. Our mental model is flawed
1. Our code doesn't reflect our mental model

If a definition entails counterintuitive conclusions, we have to think about whether it's our definition that needs refining or our intuition. This process can feel a lot like [rubber duck debugging][wiki-rubber-duck-debugging].

In the process of rigorously clarifying our own intuitions, we might see new distinctions that were previously invisible to us. These distinctions can lead to new insights or even entirely new branches of mathematics.

This dance between our intuition and formalism is how all new mathematics comes about.

## What Should Numbers Be

To learn what makes numbers *numbers*, let's compare them to things we consider not-numbers. What properties do our intuitive concept of numbers have that these not-numbers lack, or vice versa? Once we have a property, are there things we'd intuitively call not-numbers that also have these properties?

Our goal is to explore this "property space" by holding up our intuitive idea of numbers against objects we consider not-numbers. As we explore, we'll keep track of what distinguishes numbers from not-numbers with an eye towards isolating the properties that best encapsulate our intuitive concept of "number".

We start with two intuitive beliefs:

1. Numbers exist
1. We can combine them in many ways (addition, multiplication, etc.)

### Numbers vs. Strings

To start, let's start with a simplified instance to see what we can learn. Instead of "numbers in general", let's look at the integers. And instead of talking about "combining numbers in general", let's look at addition.

For not-numbers, let's look at strings and string concatenation.

We're going explore the way combining integers with addition differs from combining strings with concatenation. The hope is that in the process we'll find some properties that distinguish integers from strings and gain some insight into our own intuitive notion of what a number is.

Here's the plan:

1. Write down many examples of "integer statements" using integers, addition, equality, etc.
1. Write down a comparable list of "string statements"
1. Spot patterns and isolate properties that distinguish integers from strings
1. See to what extent those properties encapsulate number-ness

If the decision to focus on integers with addition seems arbitrary to you, think of it like trying to isolate and reproduce a bug. We're *assuming* that our intuition isn't as clear as it could be. By starting with an example that feels almost childishly concrete, we'll be able to find and address the "fuzzy spots" in our intuition more quickly.

### Notation For Addition And Concatenation

JavaScript uses the `+` symbol to denote both numerical addition and string concatenation. We run the risk of confusing ourselves if we do the same, so we're going to use `.` to denote string concatenation rather than `+`.

In other words,

- `x + y` will always mean that `x` and `y` are integers and we're adding them
- `r . s` will always mean that `r` and `s` are strings and we're concatenating them

[Perl, PHP, and a few other languages][wiki-string-concatenation-compare] use the `.` symbol to denote string concatenation, too, so it's not that uncommon.

### Terminology

We have two types of objects each with their own operation: integers with addition and strings with concatenation. We'll use `(integers, +)` and `(strings, .)` as short-hand to denote these object/operation pairs.

### Play With Integers And Addition

The goal is to find some interesting properties that distinguish `(integers, +)` and `(strings, ,)` in the hopes that we learn something about number-ness. Before we try to compare the two, let's play around with just `(integers, +)`.

Write down a few dozen statements involving integer addition. Use only integers, the `+` symbol, the `=` symbol, and parentheses. You can use variable names to stand in for integers if you like or only write down literal integers.

We can denote subtraction by writing, e.g., `4 + -5`. Don't try to generalize anything. Just write down as many expressions as you can.

For example, you might start with:

```text
2 + 4 = 6
4 + 2 = 6
4 + -4 = 0
4 + 0 = 4
1 + (4 + 2) = 1 + 6 = 7
```

Seriously, write down 50+ expressions. Vary everything you can think of: the specific numbers involved, the order you add numbers together, where you include parentheses, etc.

It will help if you're intentional about the dimensions you consider, e.g., write down 10+ examples each where...

- The left summand is the same but the right summand varies
- All the numbers are the same but you vary the order of addition
- Only the placement of parentheses vary
- We pair numbers with their negative, like `5` and `-5`, `7123` and `-7123`, etc.
- We include `0`
- etc

The more dimensions and examples you can think of the better.

### Find Some Properties

Let's find some properties that distinguish `(numbers, +)` from `(strings, .)`.

After writing down a few dozen integer expressions, write the same set of expressions down but imagine them as strings with concatenation instead. It can be useful to surround strings with quotes `'...'` so that you don't inadvertently confuse, say, the number `123` with the string `'123'`.

So, instead of writing

```text
2 + 4 = 6
4 + -4 = 0
```

Write the following:

```text
'2' . '4' = '24'
'4' . '-4' = '4-4'
```

What properties hold for `(integers, +)` but not for `(strings, .)`? What patterns do you notice? Are there specific numbers or strings that behave in a special way with respect to each operation? How many ways can we write an expression without changing its value? What role do parentheses play?

## Properties

> **Teacher's Note**
> At this point, students would break into groups and try to find some interesting properties on their own. You'd reconvene 10-20 minutes later as a group to discuss. You'd then point them to some of the more "traditional" properties.

You might have seen some of these properties before. They're usually taught as "fun" factoids about numbers, addition, etc. But another way to think of them is as *measurements*, like temperature or height. From that perspective, these properties are tools for distinguishing `(integers, +)` from `(strings, .)`.

We're also interested in properties that `(integers, +)` and `(strings, .)` _share_. By seeing where they're similar, we can better isolate the aspects that are different.

### Commutativity

We say an operation is **commutative** or that it **commutes** if the order of the operands/arguments doesn't matter. `(integers, +)` commutes because `x + y = y + x` for every integers `x` and `y`.

Compare this with string concatenation in `(strings, .)`:

```text
5 + 4 = 9    '5' . '4' = '59'
4 + 5 = 9    '4' . '5' = '95'
```

For most strings `r` and `s`, `r . s` does **not** equal `s . r`. Be careful about what's being said here.

- **Are saying**: There are pairs of strings `r` and `s` where `r . s != s . r`.

- **Not saying**: There are no pairs of strings `t` and `u` where `t . u` = `u . t`.

  For example, we could say that "every string commutes with itself under concatenation". If `t` and `u` are strings and `t = u` then

  ```text
  t . u = u . u = u . t
  ```

- **Also not saying**: There are no strings which commute with every other string.

  For example, the empty string `''` commutes with everything:

  ```text
  '' . s = s . '' = s   (for EVERY string s)
  ```

But we **are** saying that there are pairs of strings `r` and `s` where `r . s != s . r`. That's enough to distinguish `(integers, +)` from `(strings, .)`.

### Identity / Neutral Element / No-op

Both `(integers, +)` and `(strings, .)` have a neutral, do-nothing element, called an **identity** element. For `+` we have `0` and for `.` we have `''`.

Formally, we could write:

```text
x = x + 0  =  0 + x  (for every integer x)
s = s . '' = '' . s  (for every string s)
```

Or, written out:

- `0` is an identity element of `(integers, +)`
- `''` is an identity element of `(strings, .)`

### Identity is Unique

We can already gain our first "insight" about numbers. How do we know that `0` is the only number with the property that `x + 0 = 0 + x = x` for every integer `x`?

Let's see what happens if we imagine some integer `e` *also* satisfies the same property. We have the following four properties:

```text
P1.     x = x + 0    (for every integer x)
P2.     x = 0 + x    (for every integer x)
P3.     x = x + e    (for every integer x)
P4.     x = e + x    (for every integer x)
```

To prove that `0` is the *only* such integer, we need to prove that `e = 0`. In other words, "If an integer acts like an additive identity then it's equal to `0`." *If* we can prove that `0` is the only integer with this property then we can say that "`0` is **the** additive identity of `(integers, +)`.

The "trick" is as follows:

- We know that `x = x + 0` for EVERY integer `x`
- That means we can substitute in any particular integer for `x` and the equation will remain true
- In particular, we can substitute in `e` for `x`
- Likewise, because `x = e + x` for EVERY integer `x`, we can substitute in `0` for `x`.

The following are all true statements (via substitution):

```text
  2 = 2 + 0
-12 = -12 + 0
104 = 104 + 0
  e = e + 0
```

Here's the full proof, which so short that it might feel like a trick. Recall `P1` - `P4` from above:

```text
e = e + 0     (by P1, substituting in e for x)
  = 0         (by P4, substituting in 0 for x)
```

Think about the juxtaposition of our intuition vs. the formal approach above.

Without formalization, a question like "How do you know that `0` is the only additive identity in `(integers, +)`?" seemed almost philosophical. How could someone possibly answer that?

Once we isolated some properties of `0` with respect to `+`, we were able to justify our intuition in just two lines. Whatever `0` "is", it seems like the property of being an "additive inverse" is critical.

You can prove the same about `''` for `(strings, .)`. In fact, if you have any `(type, op)` pair and there's some element `e` with `x op e = e op x = x` for every element `x`, you can prove that `e` is the ONLY such element.

In other words, a `(type, op)` pair might not have an identity element, but if it does, it only has one.

### Inverses

We can "undo" addition, but we can't "undo" string concatenation. If we add `4` we can undo it by adding `-4`. If we add `12376` we can undo it by adding `12376`. If we add `-9426` we can undo it by adding `9426`.

This works because for every number `x` we can find another number `y` such that `x + y = 0`. We call `y` the **additive inverse** of `x` or the **inverse of `x` with respect to `+`**.

We have no such luck with `(strings, .)`. If we concatenate `'bananas'`, there's no other string we can concatenate which will undo concatenation.

Or put another way, given a string `s` we can't (in general) find another string `t` such that `s . t = ''`. Remember, the empty string `''` is the identity / neutral element for `.`.

**Note**: A `(type, op)` pair has to have an identity if we want to talk about inverses.

### Inverses Are Unique...Or Are They

Given an integer `x`, how many other integers `y` exist such that `x + y = 0`? Our intuition says that there's only one: `-x`. If `5 + y = 0` then `y = -5`, right?

In some ways that reasoning is backwards. If we know that `5 + y = 0` we're *only* justified in concluding that `y = -5` if we know that `y` could only have one possible value.

As with `0`, the (unproven) uniqueness of inverses *justifies* the notation `-5`.  What "is" `-5`? It's the unique number `y` such that `5 + y = 0`.

Let's try and prove that the following that `5` has at most one additive inverse. Formally: if `5 + y = 0` and `5 + z = 0` then `y = z`.

```text
1.  y = y + 0           (0 is the additive identity)
2.    = y + (5 + z)     (z is an inverse of 5)
3.    = (y + 5) + z     (???)
4.    = 0 + z           (y is an inverse of 5)
5.    = z               (0 is the additive identity)
```

You might say that step (3) is "obviously" or "intuitively" true, but what property of `(integers, +)` have we used to justify it?

**Note**: We didn't use anything special about `5` above. If we replace `5` with any arbitrary integer (denoted by `x`), the proof remains unchanged. Assuming we can justify step (3), this proves that if an integer has at least one additive inverse then it has *exactly* one (i.e., if one exists, it's unique).

### Associativity

**Associativity** is the property that

```text
x + (y + z) = (x + y) + z    (for every integer x, y, and z)
```

Both `(integers, +)` and `(strings, .)` have this subtle, almost too-obvious-for-words property.

This property justifies the notation `10 + 20 + 30`. When we write `10 + 20 + 30` do we mean `(10 + 20) + 30` or do we mean `10 + (20 + 30)`? Associativity says, "It doesn't matter which pair you add first, you will get the same number in the end."

```text
10 + (20 + 30) = 10 + 50 = 60
(10 + 20) + 30 = 30 + 30 = 50
```

`(strings, .)` is also associative:

```text
'foo' . ('bar' . 'zim') = 'foo' . 'barzim' = 'foobarzim'
('foo' . 'bar') . 'zim' = 'foobar' . 'zim' = 'foobarzim'
```

This property justifies step (3) in the uniqueness proof of inverses. In other words, if we have a `(type, op)` pair such that:

1. `op` is associative
1. There is an instance of `type` that acts as an identity for `op`

then we know that every instance of `type` has at most one inverse. If we know that every instance of `type` as *at least* one inverse then we can conclude that inverses are unique (exactly one exists for every instance of `type`).

#### Associativity And Parallel Computing

Knowing that a `(type, op)` pair is associative has implications for parallel processing. Consider an expression like:

```text
10 + 20 + 30 + 40 + 50 + 60
```

Because it doesn't matter which parts we add together first, we could process `10 + 20 + 30` on one CPU, `40 + 50 + 60` on another, and then sum the two parallel results once they're both complete.

This doesn't matter much for addition since it's such a cheap operation, but there are more complex/expensive associative operations where associativity plays a big role. For example, modern [GPUs][wiki-gpu] take advantage of the fact that [matrix multiplication][wiki-matrix-multiplication] is associative to parallelize the linear algebra required to render 3D scenes.

Machine learning algorithms also make heavy use of matrix multiplication, which is why many have been written to run on your graphics card's GPU rather than your CPU.

## Taking Stock

We've identified four properties so far:

|              |`(integers, +)`|`(strings, .)`|
|:---          |:---:          |:---:         |
| Associative  | ✅            | ✅           |
| Has identity | ✅            | ✅           |
| Has inverses | ✅            | ❌           |
| Commutative  | ✅            | ❌           |

There are many properties like this that we can use to classify different number-like things. We can also add additional operations, like multiplication, and specify how the two operations interact.

There are names for `(type, op)` pairs that satisfy a particular combination of properties. Their names are nowhere near as important as understanding what properties they satisfy and what motivated us to focus on those properties in particular.

Here are some common ones:

- A **[group][wiki-group]** is any `(type, op)` pair that is associative, has an identity, and has inverses
- If a group is also commutative then it's called an **[abelian group][wiki-abelian-group]**, named after Norwegian mathematician [Niels Abel][wiki-niels-abel].
- A **[monoid][wiki-monoid]** is any `(type, op)` pair that is associative and has an identity, but doesn't necessarily have inverses. A monoid with a commutative operation is simply called a **commutative monoid** (no namesakes here!).

These are just names that describe bundles of properties. A group is a monoid with inverses, for example.

## Other Examples

Both `(integers, +)` and `(strings, .)` are infinite, but that need not be the case.

### Booleans

Consider `(booleans, &&)` where `booleans` is the two-instance type `{true, false}` and `&&` is the logical AND operator.

This forms a commutative monoid:

1. `(x && y) && z = x && (y && z)` for all booleans `x`, `y`, and `z`
1. `true` is the identity
1. `x && y = y && x` for all booleans `x` and `y`

`(booleans, ||)` is *also* a commutative monoid, but `false` is the identity element.

### Integers Modulo N

For any positive integer `N`, the integers with addition modulo `N` form an abelian group. That is, if we define an operation by

```text
addModN(x, y) = (x + y) % N
```

then `(integers, addModN)` is a group. Replace `N` with any number — `2`, `7`, `12`, `146`, etc. — and you'll get a group.

### Sets

[wiki-rubber-duck-debugging]: https://en.wikipedia.org/wiki/Rubber_duck_debugging
[wiki-string-concatenation-compare]: https://en.wikipedia.org/wiki/Comparison_of_programming_languages_(strings)#Concatenation
[wiki-gpu]: https://en.wikipedia.org/wiki/Graphics_processing_unit
[wiki-matrix-multiplication]: https://en.wikipedia.org/wiki/Matrix_multiplication
[wiki-group]: https://en.wikipedia.org/wiki/Group_(mathematics)
[wiki-abelian-group]: https://en.wikipedia.org/wiki/Abelian_group
[wiki-niels-abel]: https://en.wikipedia.org/wiki/Niels_Henrik_Abel
[wiki-monoid]: https://en.wikipedia.org/wiki/Monoid
