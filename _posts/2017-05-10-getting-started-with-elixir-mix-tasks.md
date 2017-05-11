---

layout: post
title: "Getting Started With Elixir: Mix Tasks"
date: 2017-05-10
published: true

---

The Elixir language ships with a super-powerful build tool named Mix, which can be used to create new projects, compile projects, run tests, and handle just about anything you can throw at it.

In this post, we'll take a look at the foundational aspects of Mix, and how we can bend it to our will by creating our own Mix tasks. And because we're ~~lazy~~ efficient, we will also figure out how to minimize some extra keystrokes by creating shorter aliases for tasks we find ourselves using often.

### The Mix Project
Every Elixir project that uses Mix starts with defining a module using `Mix.Project`. This module is usually named `MyApplicationName.Mixfile` and is placed in a file named `mix.exs`:

```
defmodule MyApplicationName.Mixfile do
  use Mix.Project

  def project do
    [app: :my_application_name,
     version: "1.0.0"]
  end
end
```

If you used Mix to create your Elixir application, then Mix created this file for you as part of the generated project structure.

You can execute a number of different things, directly from the command line, once the `Mix.Project` module is defined. These include:
* `mix compile`: compiles the application (did you know there are different compilers!?)
* `mix test`: runs all of the tests (my favorite!)
* `mix run`: runs a specific task or command in the project (let's create our own!)

### Mix Tasks
You can create your own task to do just about anything you want. For example, let's say you want to send a 
