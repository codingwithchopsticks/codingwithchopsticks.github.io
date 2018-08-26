---
title: How to pass arguments to a Rake task
description: There are many ways how to pass an argument to a rake task, some of these are covered in at this blog post.
---

<small>
  ![Osaka Prefecture, Japan](/img/2018-08-08-how-to-pass-argument-to-a-rake-task/1.jpg "Osaka Prefecture, Japan")
  *Photo by [Lukas](https://unsplash.com/photos/80UpjrtFxLA?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/search/photos/tokio-night?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)*
</small>

There are many ways how to pass an argument to a rake task, some of these are covered in at this [blog post](https://cobwwweb.com/4-ways-to-pass-arguments-to-a-rake-task).

IMHO, the most elegant way to do this is using the first way described at post, the [Rake Way](https://cobwwweb.com/4-ways-to-pass-arguments-to-a-rake-task#method-1-the-rake-way):

```ruby
  task :add, [:num1, :num2] do |_, args|
    puts args[:num1].to_i + args[:num2].to_i
  end
```

And, you run it…

```bash
  $ rake add[1,2]
  # => 3
```

All right! Nothing to do here! YAY!

A common task block is like this:

```ruby
  task some_task: :environment do
    # Do awesome things...
  end
```

The `:environment` symbol is what tells to rake task to [load your entire Rails environment](https://stackoverflow.com/questions/7044714/whats-the-environment-task-in-rake/18617481#18617481). So, without this you can't access your models, for example.

To using arguments in a elegant way and load your Rails environment in your Rake task, you can write your task method like this:

```ruby
  task :add, [:num1, :num2] => :environment do |_, args|
    puts args[:num1].to_i + args[:num2].to_i
  end
```

And, this is the output:

```shell
  $ rake add[1,2]
  # => 3
```

Thanks! 😄

### References:

  - [4 Ways to Pass Arguments to a Rake Task](https://cobwwweb.com/4-ways-to-pass-arguments-to-a-rake-task#method-1-the-rake-way)
  - [How to pass arguments into a Rake task with environment in Rails?](https://stackoverflow.com/questions/1357639/how-to-pass-arguments-into-a-rake-task-with-environment-in-rails/5393324#5393324)
  - [What's the 'environment' task in Rake?](https://stackoverflow.com/questions/7044714/whats-the-environment-task-in-rake/18617481#18617481)

{% include disqus.html %}
