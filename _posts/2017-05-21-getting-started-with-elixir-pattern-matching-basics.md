---

layout: post
title: "Getting Started With Elixir: Pattern Matching Basics"
date: 2017-05-21
published: true

---

Pattern matching is one of the most interesting and fundamental aspects of the Elixir programming language. While not unique to Elixir, the idea of pattern matching isn't included in every programming language and it's a fun feature that many developers may not have experienced yet. In this post, we will check out the basics of pattern matching, along with how pattern matching applies to functions in Elixir.

<span class="image right">
  ![alt text](/images/posts/elixir.png "Elixir Logo")
</span>

### What is Pattern Matching?
The `=` operator in Elixir is known as the *match operator*. The match operator is used to *match* expressions on the right hand side of the operator against expressions on the left hand side.

For example, let's look at the following code, which is shown below in an Elixir `iex` session:

```
iex> x = 1
1
```

Most developers might look at this expression and think "I've seen that before - that's easy! The integer value 1 is assigned to the variable x!". And in most programming languages, that developer would be right!

But in Elixir, something else is actually happening. Instead of saying "this expression *assigns* the integer value 1 to the variable x", in Elixir we would say "the integer value 1 is *matched* against - or matched with - the variable x." The match is successful if Elixir is able to find a way to make the left hand side equal the right hand side. If the match cannot be made, then Elixir will let us know by raising an error.

This process of matching the left and right sides of the expression is known as *pattern matching*.

Let's look at another example:
```
iex> x = 1
1
iex> y = 2
2
iex> 1 = x
1
iex> 1 = y
** (MatchError) no match of right hand side value: 2
```

Wait, what just happened!? In the first two expressions, the variable on the left hand side of the match operator is able to match successfully with the integer values on the right hand side - and now the variable `x` has the value `1` and the variable `y` has the value `2`. The third expression matches the value `1` (the left hand side) with the value of the variable `x` (the right hand side). Since we already matched the variable `x` with the value `1` successfully, the variable retains this value and the match completes successfully.

In the final expression, the value `1` is matched with the variable `y`, which fails because the variable `y` retains the value `2`, which is the original value we matched it against. When this value is substituted into the expression, the match fails because the values `1` and `2` cannot be matched. Remember, the `=` operator is matching the left and right hand sides of the expression - not performing an assignment.

So far we've only checked out pattern matching using a simple integer value. Let's check out some examples that are a little more interesting.

### Pattern Matching Basics
- strings
We can extend the use of pattern matching to try to match just about anything we want.

For exmaple, Elixir includes support for "lists" (you can think of them as arrays if you like) and when matching lists, we can also capture references to each item in the list at the same time:
```
iex> [a, b, c] = ["moana", "pua", "heihei"]
["moana", "pua", "heihei"]
iex> a
"moana"
iex> b
"pua"
iex> c
"heihei"
```

We can also pattern match tuples, again destructuring the object and capturing a reference to each item:
```
iex> {a, b, c} = {:moana, :pua, :heihei}
{:moana, :pua, :heihei}
iex> a
:moana
iex> b
:pua
iex> c
:heihei
```

### Using Pattern Matching With Functions

### Pattern Matching and Guard Clauses
