---
title: How getters and setters works in Ruby?
description: 
updated: 2019-06-15 20:47
---

<small>
  ![Toddler's standing in front of beige concrete stair](/assets/2019-06-15-como-funcionam-os-getters-e-setters-no-ruby/1.jpg "Toddler's standing in front of beige concrete stair")
  *Photo by [Jukan Tateisi](https://unsplash.com/@tateisimikito) on [Unsplash](https://unsplash.com/search/photos/stairs?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)*
</small>

Há alguns dias um amigo me mandou a seguinte pergunta: O que são e como funcionam os _getters_ e _setters_?

Fui pensar um pouco nisso para bolar uma resposta e lembrei que eu também tive dificuldade com esse tópico quando comecei a programar e  continuei tendo dificuldades com isso quando iniciei no mundo de Ruby 😅.

Assim, mandei um textão para meu amigo explicando o que seriam os _getters_ e _setters_ e achei que seria um ótimo tópico para compartilhar aqui com vocês! Vamos lá?

_Getters_ e _setters_ servem para você manipular atributos do objeto (atributos são informações sobre objeto).

_Getters_ servem para você ler valores de algum atributo do objeto e _setters_ servem pra você escrever valores valores em algum atributos do objeto.

Em código ruby, um objeto com _getter_ e _setter_ seria assim:

```ruby
class Humano
  # aqui eu inicializo meu objeto apenas com o atibuto nome:
  def initialize(nome)
    @nome = nome
  end

  # Aqui eu defino um getter para o atributo nome que me permite ler o valor desse atributo:
  def nome
    @nome
  end

  # Aqui eu defino um setter para idade que me permite atribuir um valor para esse atributo:
  def idade=(idade)
    @idade = idade
  end

  # Aqui eu defino um getter para idade que me permite ler o valor desse atributo:
  def idade
    @idade
  end
end
```

Podemos usar esse objeto assim:

```ruby
# instancio um novo objeto Humano com o valor "odinei" no atributo nome
# e o coloco dentro da variável "odinei"
> eu = Humano.new('odinei')
=> #<Humano:0x00007fa450006918 @nome="odinei">

# aqui eu chamo o getter nome para que ele me devolva o valor do atributo nome do meu objeto
> eu.nome
=> "odinei"

# aqui eu chamo o getter idade para que ele me devolva o valor do atributo idade do meu objeto
# como eu não atribui valor à esse atributo, ele me devolve nil (nulo) como valor
> eu.idade
=> nil

# aqui eu chamo o setter idade para atribuir à esse atributo o valor 27
> eu.idade = 27
=> 27

# aqui eu chamo o getter idade para que ele me devolva o valor do atributo nome 
# do meu objeto, que agora tem um valor
> eu.idade
=> 27

# aqui eu estou sobreescrevendo o valor anterior do atributo idade para o valor 23
> eu.idade = 23
=> 23
```

Como eu não defini um _setter_ para nome, eu não consigo trocar o valor do atributo nome do meu objeto:

```ruby
eu.nome = 'Arthur'
Traceback (most recent call last):
        4: from /Users/odineiribeiro/.asdf/installs/ruby/2.6.2/bin/irb:23:in `<main>'
        3: from /Users/odineiribeiro/.asdf/installs/ruby/2.6.2/bin/irb:23:in `load'
        2: from /Users/odineiribeiro/.asdf/installs/ruby/2.6.2/lib/ruby/gems/2.6.0
                /gems/irb-1.0.0/exe/irb:11:in `<top (required)>'
        1: from (irb):26
NoMethodError (undefined method `nome=' for #<Humano:0x00007fa450006918 @nome="odinei", @idade=23>)
Did you mean?  nome
```

Aqui temos uma parte interessante do erro: 

```
NoMethodError (undefined method `nome=' for #<Humano:0x00007fa450006918 @nome="odinei", @idade=23>)
```

O ruby está no dizendo que o nosso objeto não tem o método _setter_ `def nome=` por isso, não podemos atribuir um valor para o atributo nome do nosso objeto!

## A mesma coisa, só que diferente

Em ruby, podemos usar alguns metodos nos nossos objetos para poupar linhas ao escrever nossos _getters_ e _setters_.
São eles 

- `attr_accessor` que cria os métodos de leitura (_getter_) e escrita (_setter_) para um determinado atributo.
- `attr_writer` que cria apenas o método de escrita para um determinado atributo.
- `attr_reader` que cria apenas o método de leitra para um determinado atributo.

Vejamos um exemplo: 

```ruby
class Humano
  # aqui eu crio um getter para o atributo nome
  attr_reader :nome
  
  # aqui eu crio um getter e um setter para o atributo idade 
  attr_accessor :idade

  def initialize(nome)
    @nome = nome
  end
end
```

Esse novo objeto `Humano` se comporta igual ao objeto que criamos anteriormente! Inclusive dando o mesmo erro ao chamarmos um setter inexistente!

```ruby
eu = Humano.new('odinei')
=> #<Humano:0x00007fb20d0344b0 @nome="odinei">
> eu.nome
=> "odinei"
> eu.idade
=> nil
> eu.idade = 27
=> 27
> eu.idade
=> 27
> eu.idade = 23
=> 23
> eu.nome = 'Arthur'
Traceback (most recent call last):
        4: from /Users/odineiribeiro/.asdf/installs/ruby/2.6.2/bin/irb:23:in `<main>'
        3: from /Users/odineiribeiro/.asdf/installs/ruby/2.6.2/bin/irb:23:in `load'
        2: from /Users/odineiribeiro/.asdf/installs/ruby/2.6.2/lib/ruby/gems/2.6.0
                /gems/irb-1.0.0/exe/irb:11:in `<top (required)>'
        1: from (irb):17
NoMethodError (undefined method `nome=' for #<Humano:0x00007fb20d0344b0 @nome="odinei", @idade=23>)
Did you mean?  nome
```

## Método de escrita, pra quê te quero?

O `attr_writer` pode ser um pouco estranho de entender quando usar, afinal, pra quê eu vou colocar um valor em um atributo do meu objeto sem ter um método para lê-lo? 

A resposta é simples: Você pode querer um valor para fazer alguma operação com ele e retorná-lo de uma forma diferente. Vamos ver um exemplo:

```ruby
> eu = Humano.new('odinei')
=> #<Humano:0x00007fd577a279a8 @nome="odinei">
> eu.nome
=> "odinei"
> eu.ano_nascimento = 1992
=> 1992
> eu.idade
=> 27
```

No exemplo acima eu calculo a minha idade com base na atributo `ano_nascimento` que foi criada apenas para leitura!

Em ruby é muito mais comum usar os `attr_accessor`, `attr_reader` e `attr_writer` para criar métodos de leitura e escrita em vez de criar esses métodos "na mão" para termos menos linhas no nossos arquivos 😄!
