---

layout: post
title: "Getting Started With Elixir: Mix Tasks"
date: 2017-05-12
published: true

---

The Elixir language ships with a super-powerful build tool named Mix, which can be used to create new projects, compile projects, run tests, and handle just about anything you can throw at it.

In this post, we'll take a look at the foundational aspects of Mix, and how we can bend it to our will by creating our own Mix tasks. And because we're ~~lazy~~ efficient, we will also figure out how to minimize some extra keystrokes by creating shorter aliases for Mix tasks we find ourselves using often.

<span class="image right">
  ![alt text](/images/posts/elixir.png "Elixir Logo")
</span>

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

If you use Mix to generate the skeleton of your Elixir application by running `mix new hello_world`, then Mix created this file for you automatically as part of the generated project structure.

With the `Mix.Project` module in place, you can execute a number of different things directly from the command line. These include:
* `mix compile`: compiles the application (did you know there are different compilers!?)
* `mix test`: runs all of the tests (who doesn't love tests!?)
* `mix run`: runs a specific task or command in the project (we will look at how to create our own Mix task next!)

### Mix Tasks
You can create your own task to do just about anything you want. For example, let's say your team uses Slack and you want to send a Slack message to your team channel for different events.

We can create a custom Mix task to send Slack messages by creating a new module like the one below:

```
defmodule Mix.Tasks.Slack do
  use Mix.Task

  def run(_) do
    # post a new message to Slack using an Elixir HTTP Client
  end
end
```

Most likely, you aren't going to use this task as part of your local developer workflow (unless you want team members to kick you off the team for spamming them in Slack). But, maybe you do want to send out a Slack message from your continuous integration server every time the build fails. You could avoid writing a lot of configuration code and running it on your build server and agents by encapsulating all of this in a custom Mix task instead.

### Getting Efficient with Aliases
We can also eliminate a few extra keystrokes from our developer workflow using aliases for Mix tasks we find ourselves using frequently.

For example, we can run all of the tests in our project using the command `mix test`. If we want to eliminate three keystrokes by passing the parameter `t` to the mix command (instead of `test`), we can set up an alias for the parameter `t` and get the same results.

Aliases are defined within the `Mix.Project` module we created above. Here is an example:

```
defmodule MyApplicationName.Mixfile do
  use Mix.Project

  def project do
    [app: :my_application_name,
     version: "1.0.0",
     aliases: aliases]
  end

  defp aliases do
    [t: "test"]
  end
end
```

In this example, we configured aliases by creating a private function. Then we call this function from within the project configuration.

And that's it - now we can run `mix t` to run all of the tests in our project. Just think of all the time we saved by not having to type those three extra letters!*

*Note: If we are *really* running our tests as often as we should, we should look into running the tests using a file watcher. Then we can rerun the tests every time we change a file in the project.

### Conclusion
This is really just beginning to scratch the surface of all the things available within Mix. For more info on Mix, you can:
* run `mix help` from the command line to see all of the available commands
* head over to the [Mix build tool documentation](https://hexdocs.pm/mix/Mix.html)
