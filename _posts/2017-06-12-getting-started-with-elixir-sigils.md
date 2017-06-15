---

layout: post
title: "Getting Started With Elixir: Sigils"
date: 2017-06-12
published: true

---

When writing code with Elixir, I often find myself feeling like I'm writing code in Ruby. There are a number of things about the Elixir language that feel just like the Ruby language. *Sigils* are one of those things at first glance - and then I remember how cool it is that Elixir lets you write your own sigils. In this post, we'll take a look at some of the built in Elixir sigils, and then wrap things up by writing our own custom sigil at the end. 

### First, What's a Sigil?
According to Google, here's the definition of a *sigil*:
>an inscribed or painted symbol considered to have magical power.

In Elixir, much like in Ruby, a sigil is a shorthand name for a function, expressed using a tilde followed by an uppercase or lowercase letter, some kind of delimited content, and then a set of options. 

Let's take a look at some examples. 

### Lists
Lists come in handy frequently when working with Elixir, and building those lists is super easy using the `~w` sigil. 
```
iex> ~w(moana zootopia trolls)
["moana", "zootopia", "trolls"]
```

Elxiir uses the "white space" between each word in the expression we pass to the sigil to break the content apart and build a list for us.

If we'd rather build a list of atoms or characters, instead of strings, we can pass the optional `a` or `c` modifier to the sigil. 

```
iex> ~w(moana zootopia trolls)a
[:moana, :zootopia, :trolls]

iex> ~w(moana zootopia trolls)c
['moana', 'zootopia', 'trolls']
```

Of course, we could always build the same list using a more traditional syntax, like this: 
```
iex> ["moana", "zootopia", "trolls"]
["moana", "zootopia", "trolls"]
```

And we get the same results. But where is the fun in that! 

### Regular Expressions
Regular expressions can be created in a similar way using the `~r` sigil. Here's an example using Elixir's `Regex` library. The regular expression to match against is defined using the `~r` sigil, and then that is passed along to the `Regex.match?` function with the string to match against the expression:

```
iex> Regex.match?(~r/elixir is fun/, "elixir is fun to learn")
true

iex> Regex.match?(~r/elixir is fun/, "elixir")
false
```

This example just barely scratches the surfact of what is possible with the built in `Regex` module in Elixir. For additional examples and documentation, check out the [full documentation for the `Regex` module](https://hexdocs.pm/elixir/Regex.html).

### Creating Your Own Sigils
Finally, the best part about sigils in the Elixir language (especially compared to their counterpart in Ruby), is the ability to create your own custom sigils. Almost everything in the Elixir language is extensible, and sigils are no exception. 

Before we implement our own sigil, we need to learn one more fundamental thing about sigils: the built in sigils in Elixir are simple functions defined with the signature `sigil_x(term, opts)`. 

These sigil functions can be called using their shorthand name (i.e. `~w(<words>)`, like we have been) or using their full sigil name (i.e. `sigil_w(<words>)`). Both forms will produce the same results. 

With that in mind, we can write our own custom sigils by defining functions that follow the same format.

For example, let's assume we find ourselves continually wanting to create strings with all uppercase letters. According to the [Elixir hexdocs](https://hexdocs.pm/elixir/1.4.4/String.html#upcase/1), the string uppercase function in Elixir is `String.upcase(binary)`. 

We can shorten this by creating our own sigil. Let's call it `sigil_u`. 

```
defmodule MySigils do
  def sigil_u(string, _opts), do: String.upcase(string)
end

defmodule SigilTest do
  import MySigils

  def test_name do
    IO.puts ~u(moana)
    IO.puts ~u(zootopia)
    IO.puts ~u(tRoLls)
    IO.puts ~u(1230)
  end
end

SigilTest.test_name
```

In this block, we first define a new module named `MySigils`, where we can define all of our custom sigils. Inside that module, we define the `sigil_u` function, which accepts two parameters: the first parameter is the string we are going to manipulate, and the second is a set of options. 

Options come in handy when  you want to slightly modify the output of the sigil. For example, if we want to control whether or not string interpolation is performed by the function, we could provide an option to specify this behavior. For this example, we are going to skip any additional options, so we define the options parameter with a leading underscore so Elixir will know we intend to ignore it (i.e. `_opts`). 

If we run this in an `iex` session, we should get uppercase versions of each string, just like we expect: 
```
MOANA
ZOOTOPIA
TROLLS
1230
```
And that's it! We now have a custom sigil that automatically returns an uppercase string representation of the value we pass into it. 

### Last Minute Thoughts On Creating Your Own Sigils
As I mentioned in the beginning of this post, I think having the ability to create your own custom sigils is cool, especially coming from a Ruby background where I didn't have that option. 

However, keep in mind that every custom sigil is another redirection point. One of our primary goals as software craftsman is writing clean and simple code, and we still want to hold true to that idea, even when using custom sigils. 

If you find yourself getting ready to write your own sigil, first stop and ask yourself if a custom sigil is the *right* solution for the problem. Would it make more sense to implement this new functionality as an additional function on an existing module? Would it make more sense to implement this new functionality as an entirely new module? 

At the end of the day, a sigil is really just a function with a single-letter name. Will the other developers on your team be able to understand your intent and follow your thought process, even if the function name is only one letter long? 

With that said, custom sigils are pretty slick. I would just make sure you are very intentional about when you choose to use them, and use them sparingly when you do. 

Remember... 
> "With great power comes great responsibility." ~ Voltaire (or was it Uncle Ben?)