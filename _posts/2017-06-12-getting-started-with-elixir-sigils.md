---

layout: post
title: "Getting Started With Elixir: Sigils"
date: 2017-06-12
published: true

---

As I play with Elixir more and more, I frequently find myself feeling like I'm writing Ruby. Then I have to pinch myself and remind myself 

When writing code with Elixir, I often find myself thinking I'm writing code in Ruby. There are so many things about the Elixir language that feel just like the Ruby language. *Sigils* are one of those things at first glance - then I remember how cool it is that Elixir lets you write your own sigils. In this post, we'll take a look at some of the built in Elixir sigils, and then wrap things up by writing our own custom sigil at the end. 

### What's a Sigil?
According to Google, here's the definition of a *sigil*:
>an inscribed or painted symbol considered to have magical power.

In Elixir, much like in Ruby, a sigil is a shorthand name for a function, expressed using a tilde followed by an uppercase or lowercase letter and then some kind of delimited content. 

Let's take a look at some examples. 

### Lists
Building lists of things comes in handy frequently when working with Elixir, and this is super easy using the `~w` sigil. 
```
iex> ~w(moana zootopia trolls)
["moana", "zootopia", "trolls"]
```

Elxiir uses the "white space" between each word in the expression we provided to the sigil to break the content apart and build a list for us.

If we'd rather build a list of atoms or characters, instead of strings, we can pass the optional `a` or `c` modifier to the sigil. 

```
iex> ~w(moana zootopia trolls)a
[:moana, :zootopia, :trolls]

iex> ~w(moana zootopia trolls)a
['moana', 'zootopia', 'trolls']
```

Of course, we could always build the same list using a more traditional syntax and get the same results, like this: 
```
iex> ["moana", "zootopia", "trolls"]
["moana", "zootopia", "trolls"]
```

But where is the fun in that! 

### Regular Expressions
### Strings
### Creating Your Own Sigils
