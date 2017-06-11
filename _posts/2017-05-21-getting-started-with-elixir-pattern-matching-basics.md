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
When you start diving into Elixir, probably the most interesting thing you find right away is this idea of "pattern matching". In Elixir, the `=` operator is known as the *match operator*. The match operator is used to *match* expressions on the right hand side of the operator against expressions on the left hand side.

For example, let's look at the following code, which is shown below in an Elixir `iex` session:

```
iex> x = 1
1
```

Most developers might look at this expression and think "I've seen that before - that's easy! The integer value 1 is assigned to the variable x!". In most programming languages, that would be correct!

But in Elixir, something else is actually happening. Instead of saying "this expression *assigns* the integer value 1 to the variable x", in Elixir we would say "the integer value 1 is *matched* against - or matched with - the variable x." The match is successful if Elixir is able to find a way to make the left hand side equal the right hand side. If the match cannot be made, then Elixir will let us know by shouting at us with an error.

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

So far we've only played with pattern matching using simple integer values. Let's look at some examples that are a little more interesting.

### Pattern Matching Basics
We can extend the use of pattern matching to try to match just about anything we want, and we can be as specific or as general as we want with the match.

For exmaple, Elixir includes support for "lists" (similar to arrays in a lot of other languages) and when matching lists, we can also capture references to each item in the list at the same time:
```
iex> [a, b, c] = ["moana", "maui", "heihei"]
["moana", "maui", "heihei"]
iex> a
"moana"
iex> b
"maui"
iex> c
"heihei"
```

We can also pattern match tuples, again destructuring the object and capturing a reference to each item in the tuple:
```
iex> {a, b, c} = {:moana, :maui, :heihei}
{:moana, :maui, :heihei}
iex> a
:moana
iex> b
:maui
iex> c
:heihei
```

### Using Pattern Matching With Functions
This fun idea of pattern matching goes beyond just matching on simple types and data structures. We can also use pattern matching within functions to invoke a specific function body based on the values of the parameters we pass to the function.

For this example, we are going to use a basic type in Elixir called anonymous functions. Here's the syntax of the anonymous function type:
```
fn
  parameter-list -> body
  parameter-list -> body ...
end
```

Elixir matches the `parameter-list` passed in the function call to the parameter lists defined in the function definition to determine which function body to execute.

In the example below (again, sticking with the Moana theme), we are defining an anonymous function named `tagline()` with three different function bodies:
```
tagline = fn
  :moana -> "Board my boat!"
  :maui -> "You're welcome!"
  :heihei -> "Cock-a-doodle-do!"
end

IO.puts "Moana says: #{tagline.(:moana)}"
IO.puts "Maui says: #{tagline.(:maui)}"
IO.puts "Heihei says: #{tagline.(:heihei)}"
```

When we call the `tagline()` function and pass the atom `:moana` as the parameter list, this is matched successfully with the first function body in our function definition and the string "Moana says: Board my boat!" is returned by the function.

Likewise, when we call the `tagline()` function again, this time passing the atom `:maui` as the parameter list, this matches successfully with the second function body in the function definition and the string "Maui says: You're welcome!" is returned.

Here's what the full output should look like:
```
Moana says: Board my boat!
Maui says: You're welcome!
Heihei says: Cock-a-doodle-do!
```

So. Awesome. We were able to return different messages from our simple `tagline()` anonymous function, all without having to write a single conditional statement.

### Wrapping Up
[<span class="image left">
  ![alt text](/images/posts/programming_elixir_1.3.jpg "Programming Elixir 1.3: Functional |> Concurrent |> Pragmatic |> Fun")
</span>](https://www.amazon.com/Programming-Elixir-1-3-Functional-Concurrent/dp/168050200X/ref=sr_1_1?ie=UTF8&qid=1497208782&sr=8-1&keywords=programming+elixir)
This just barely scratches the surface of what you can do with pattern matching.

If you're interested in learning more about pattern matching and what you can do with it in Elixir, you should check out ["Programming Elixir" by Dave Thomas](https://www.amazon.com/Programming-Elixir-1-3-Functional-Concurrent/dp/168050200X/ref=sr_1_1?ie=UTF8&qid=1497208782&sr=8-1&keywords=programming+elixir) (published by [Pragmatic Press](https://pragprog.com/)). I made my way through it earlier this year and feel it is the authoritative book on getting up and going with Elixir.
