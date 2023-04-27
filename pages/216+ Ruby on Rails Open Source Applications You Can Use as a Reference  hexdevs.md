---
created: 2023-04-27T17:35:21 (UTC -04:00)
tags: [ruby,ruby on rails,software design,best practices]
source: https://www.hexdevs.com/posts/massive-list-of-open-source-ruby-on-rails-applications-you-can-use-as-a-reference/
author: Thiago Araujo
---

# 216+ Ruby on Rails Open Source Applications You Can Use as a Reference | hexdevs

> ## Excerpt
> Have no idea how to implement a new Ruby on Rails feature? Or a Rails model? A migration? How to write a test? Here's how to effectively use 200+ Ruby on Rails Applications as a reference for implementing the most common things you need as a Ruby developer.

---
Not sure how to implement a new Ruby on Rails feature? A proper model, controller, migration? Or how to write a test for the code you’re writing?

What if you could easily access a massive library of full-blown Ruby on Rails Applications used in the wild and have them as a reference?

**[real-world-rails](https://github.com/eliotsykes/real-world-rails) gives you a list of _(173 apps + 43 engines)_ = 216 Rails Applications you can learn from 💣**

It’s an awesome repository created by [Eliot Sykes](https://eliotsykes.com/) and I use it all the time for reference.

There are two ways you can use `real-world-rails`:

1.  Use GitHub search to find what you need within the repository (easy)
2.  Clone the repository and use grep or [ripgrep](https://github.com/BurntSushi/ripgrep) to search for what you want (my favorite way).

In this post, I’m going to show you how to install it. And how to use it for implementing some of the most common things you need as a Ruby on Rails Developer.

## A Massive List of Open-Source Ruby on Rails Application Examples

Want to follow along? Watch the video below to see how to browse `real-world-rails` and find answers to your questions:

<iframe src="https://www.youtube.com/embed/zbIdk5ms9G8" allowfullscreen="" title="YouTube Video"></iframe>

## How to Install `real-world-rails`

```
git clone git@github.com:eliotsykes/real-world-rails.git
cd real-world-rails/
bundle install
```

I’m using `ripgrep` to recursively search for code. It’s super fast. [Click here](https://github.com/BurntSushi/ripgrep#installation) to learn how to install it. Or use your favorite grep tool.

You can also add `ripgrep` as the default search tool for your editor (I use it with Emacs).

### Init submodules

**Remove broken submodules**

As I am writing this post, three submodules are not public anymore and will cause an error when pulled. The easiest way to fix this is to just remove them:

```
git rm engines/o_cms
git rm apps/shoppe
git rm apps/netguru-help
```

Then, init the submodules to have access to all linked repositories (on `/apps` and `/engines` folders):

```
git submodule update --init --jobs 4
```

This command will take some time because it will pull about 8 GB of code 💾 (TIP: You can probably get around this by doing a git shallow clone and save some disk space!)

After you have pulled the submodules, you’ll be ready to go. It’s time to move on to the fun part!

## How to Find Examples of Ruby on Rails Projects

Exploring these different open source apps and engines will teach you a lot about how other people write professional code.

The maintainers added [a bunch of cool examples](https://github.com/eliotsykes/real-world-rails#how-you-can-analyze-real-world-rails-apps) of things you can search for and commands you can run.

If you want some more examples and other ideas of things you can search for and learn from, keep reading!

### List All Ruby on Rails Models

To see a list of basic Ruby on Rails models, run:

```
rg --type ruby -C 5 '< ApplicationRecord'
```

You’ll get all models that inherit from ApplicationRecord directly, which means most of them.

### How to Write Ruby method definitions

To find examples of how to write method definitions, just search for it. In this example, we’re searching for any class that defines a method related to `email`:

```
rg -truby 'def email'
```

Similarly, you can search for class methods that start with `email...`:

```
rg -truby 'def self.email'
```

### Other fun examples

Some days ago I wanted to see how and why people create classes that inherit from Hash. What kind of things do they want to accomplish? And how to properly override Hash methods if you want to extend the class. Here’s how I answered my own questions.

First, I searched for classes who inherited from `Hash`:

```
rg -truby -C 5 '< Hash$'
```

Then I wanted to see how people override some basic hash methods, such as `Hash#[]` and `Hash#[]=`:

```
rg --type ruby -C 20 '< Hash$' | rg -C 20 'def \[\]'
```

Here’s the result:

![Overriding Hash methods](https://www.hexdevs.com/images/posts/ripgrep-examples/hexdevs-overriding-hash-methods.png)

Which allowed me to answer my question and satisfy my curiosity.

### How to Write Service Classes

A common question that developers ask is this: “how should I write Service Classes?” Well, just take a look at lots of examples and see how you like them.

Want to find examples of how to write Ruby on Rails Service Classes? This will give you a bunch of examples and the first few lines of each class:

```
rg --type ruby -C 5 'class [A-Za-z]+Service'
```

Here’s the result:

![Writing Ruby Service Classes](https://www.hexdevs.com/images/posts/ripgrep-examples/hexdevs-how-to-implement-service-objects-ruby-on-rails.png)

### How to Write Job Classes

Want to find examples of how people write Ruby on Rails Job Classes? How often jobs should be retried, how many attempts to set, and how to handle errors?

Run this:

```
rg --type ruby -C 5 'class [A-Za-z]+Job'
```

And you will see something like this:

![Overriding Hash methods](https://www.hexdevs.com/images/posts/ripgrep-examples/hexdevs-how-to-implement-job-classes-ruby-on-rails.png)

### How to Write Worker Classes

Same idea: want to find examples of how to write Ruby Worker Classes? Run:

```
rg -truby -C 10  'class .*Worker$'
```

And this is what you’ll see:

![Writing Worker Classes](https://www.hexdevs.com/images/posts/ripgrep-examples/hexdevs-how-to-write-a-worker-class-ruby-on-rails.png)

## How To Structure Large Ruby on Rails Applications

Look at very large Ruby on Rails applications such as Gitlab (and others) and see how they do it. You don’t need to do the same thing they are doing, as they have different goals and contexts.

But you can look at these different apps and form your own opinion. Adapt their ideas and make them work for you. That way, you don’t have to come up with a new approach totally from scratch.

Here are a couple of things you might want to explore.

### How to Structure the Models Folder When you Have Inheritance and Multiple Levels of Hierarchies

When you are not structuring your Ruby on Rails project strictly following the plain old MVC pattern, it’s a good idea to look at how other people organize their code.

This is useful when you are doing Domain Driven Design, or have some complex models with inheritance and complicated hierarchies, nested modules, and things like that.

Take a look at the directory structure of some large Ruby on Rails Applications. Here’s an example:

```
tree apps/gitlabhq/app/models
```

And you should be able to see the directory structure of the `models` folder:

![Organizing Complex Model Files](https://www.hexdevs.com/images/posts/ripgrep-examples/hexdevs-how-to-organize-complex-model-folder-ruby-on-rails.png)

### How to See Examples of Complex Ruby on Rails Features

Gitlab has an interesting worker that imports repositories from different sources, including GitHub.

Want to know how Gitlab imports a repository from GitHub? Take a look at the code:

```
rg -truby 'GithubImport'
```

Here is how you can see the folder structure:

```
tree apps/gitlabhq/app/workers/gitlab/github_import
```

This is what you’ll see:

![Organizing Large Ruby on Rails Features](https://www.hexdevs.com/images/posts/ripgrep-examples/hexdevs-how-to-organize-a-complex-ruby-on-rails-feature.png)

Then open the files/folders with vim, Emacs, VSCode, or your favorite editor.

___

Really cool, right?

Explore, read, and form your own opinions about other people’s code. The more you get exposed to professional code, the more you can build your “coding taste” and expertise.

Next time you need examples or inspiration for a feature, and you’re not sure how to implement it, use this resource as a guide. Bookmark this post for later reference ⭐

By the way, this post was inspired by my Twitter thread:

I did not expect it to gather so much interest. But since people loved it, I decided to show how I use this reference and search for things. If you’d like to get more tips like these on your Twitter feed, [follow me](https://twitter.com/thdaraujo) and [hexdevs](https://twitter.com/HexDevs)!
