---
title: Como passar argumentos para um comando Rake
description: THá muitas maneiras de passar um argumento para um comando Rake, algumas delas são abordadas neste blog post.
updated: 2016-08-08 23:37
---

<small>
  ![Osaka Prefecture, Japan](/assets/2018-08-08-how-to-pass-argument-to-a-rake-task/1.jpg "Osaka Prefecture, Japan")
  *Photo by [Lukas](https://unsplash.com/photos/80UpjrtFxLA?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/search/photos/tokio-night?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)*
</small>

Há muitas maneiras de passar um argumento para um comando Rake, algumas delas são abordadas neste [blog post](https://cobwwweb.com/4-ways-to-pass-arguments-to-a-rake-task).

Na minha humilde opinião, a maneira mais elegante de fazer isso é usar a primeira maneira descrita no post, o [Rake Way](https://cobwwweb.com/4-ways-to-pass-arguments-to-a-rake-task#method-1-the-rake-way):

```ruby
  task :soma, [:numero1, :numero2] do |_, args|
    puts args[:numero1].to_i + args[:numero2].to_i
  end
```

E, no seu terminal…

```bash
  $ rake soma[1,2]
  # => 3
```

Ok! Nada mais o que fazer aqui! Uhul!

Um bloco de tarefas Rake normalmente é assim:

```ruby
  task alguma_tarefa: :environment do
    # Coisas incríveis aqui...
  end
```

O símbolo `:environment` está dizendo para a sua tarefa Rake [carregar todo o seu ambiente Rails](https://stackoverflow.com/questions/7044714/whats-the-environment-task-in-rake/18617481#18617481). Então, sem isso você não pode acessar seus modelos, por exemplo.

Para usar argumentos de uma maneira elegante e carregar seu ambiente Rails em sua tarefa Rake, você pode escrever seu método de tarefa da seguinte forma:

```ruby
  task :soma, [:numero1, :numero2] => :environment do |_, args|
    puts args[:numero1].to_i + args[:numero2].to_i
  end
```

E esta é a saída:

```shell
  $ rake soma[1,2]
  # => 3
```

Obrigado! 😄

### Referencias:

  - [4 Ways to Pass Arguments to a Rake Task](https://cobwwweb.com/4-ways-to-pass-arguments-to-a-rake-task#method-1-the-rake-way)
  - [How to pass arguments into a Rake task with environment in Rails?](https://stackoverflow.com/questions/1357639/how-to-pass-arguments-into-a-rake-task-with-environment-in-rails/5393324#5393324)
  - [What's the 'environment' task in Rake?](https://stackoverflow.com/questions/7044714/whats-the-environment-task-in-rake/18617481#18617481)
