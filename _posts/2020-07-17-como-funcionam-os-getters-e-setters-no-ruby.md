---
title: Como funcionam os getters e setters no Ruby?
description: Há alguns dias um amigo me mandou a seguinte pergunta "O que são e como funcionam os getters e setters no Ruby?". Assim, mandei um textão para meu amigo explicando o que seriam os getters e setters e achei que seria um ótimo tópico para compartilhar aqui com vocês! Vamos lá?
updated: 2020-07-17 03:32
---

<small>
  ![Passarela fotografada de baixo para cima](/assets/2020-07-17-como-funcionam-os-getters-e-setters-no-ruby/1.jpg "Passarela fotografada de baixo para cima")
  *Photo by [Danny G](https://unsplash.com/@dannyg) on [Unsplash](https://unsplash.com/photos/aMn-CjhW2c4)*
</small>

Há alguns dias [um amigo](https://github.com/MoisesBorges) me mandou a seguinte pergunta: O que são e como funcionam os *getters* e *setters*?

Fui pensar um pouco nisso para bolar uma resposta e lembrei que eu também tive dificuldade com esse tópico quando comecei a programar e continuei tendo dificuldades com isso quando iniciei no mundo de Ruby 😅.

Assim, mandei um textão para meu amigo explicando o que seriam os *getters* e *setters* e achei que seria um ótimo tópico para compartilhar aqui com vocês! Vamos lá?

*Getters* e *setters* servem para você manipular atributos do objeto (atributos são informações sobre objeto).

*Setters* servem para atribuir valores aos atributos do objeto que são guardadas em variáveis de instâncias (variáveis de instância sempre começam com @) e *getters* leem os valores dessas variáveis nos permitindo acessa-los sempre que necessário.

Em código ruby, um objeto com *getters* e *setters* seria assim:

```ruby
class Humano
  # aqui eu inicializo meu objeto apenas
  # com o atibuto nome:
  def initialize(nome)
    @nome = nome
  end

  # aqui eu defino um getter para nome que
  # me permite ler o valor desse atributo:
  def nome
    @nome
  end

  # aqui eu defino um setter para idade que
  # me permite atribuir um valor para esse atributo:
  def idade=(idade)
    @idade = idade
  end

  # aqui eu defino um getter para idade que
  # me permite ler o valor desse atributo:
  def idade
    @idade
  end
end

```

Podemos usar esse objeto assim:

```bash
# aqui eu instancio um novo objeto Humano com
# o valor "odinei" no atributo nome e o atribuo
# à variável "odinei"
> eu = Humano.new('odinei')
=> #<Humano:0x00007fa450006918 @nome="odinei">

# aqui eu chamo o getter nome para que ele me
# devolva o valor do atributo nome do meu objeto
> eu.nome
=> "odinei"

# aqui eu chamo o getter idade para que ele me
# devolva o valor do atributo idade do meu objeto
# como eu não atribui valor à esse atributo, ele
# me devolve nil (nulo) como valor
> eu.idade
=> nil

# aqui eu chamo o setter idade para atribuir à
# esse atributo o valor 28
> eu.idade = 28
=> 28

# aqui eu chamo o getter idade para que ele me
# devolva o valor do atributo idade do meu objeto,
# que agora tem um valor
> eu.idade
=> 28

# aqui eu sobreescrevo o valor anterior do atributo
# idade para o valor 23
> eu.idade = 23
=> 23

# aqui eu chamo o getter idade para que ele me
# devolva o valor do atributo idade do meu objeto,
# que agora tem um valor diferente do anterior
> eu.idade
=> 23

```

Porém, como eu não defini um *setter* para nome, eu não consigo trocar o valor do atributo nome do meu objeto:

```bash
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

```bash
NoMethodError (undefined method `nome=' for #<Humano:0x00007fa450006918 @nome="odinei", @idade=23>)
```

O ruby está no dizendo que o nosso objeto não tem o método *setter* `def nome=` por isso, não podemos atribuir um valor para o atributo nome do nosso objeto!

## A mesma coisa, só que diferente

Em ruby, podemos usar alguns métodos nos nossos objetos para poupar linhas ao escrever nossos *getters* e *setters*.
São eles

- `attr_accessor` que cria os métodos de leitura (*getter*) e escrita (*setter*) para um determinado atributo.
- `attr_writer` que cria apenas o método de escrita (*setter*) para um determinado atributo.
- `attr_reader` que cria apenas o método de leitura (*getter*) para um determinado atributo.

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

Esse novo objeto `Humano` se comporta igual ao objeto que criamos anteriormente! Inclusive dando o mesmo erro ao chamarmos um *setter*  inexistente!

```bash
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

## Método de escrita, para que te quero?

O `attr_writer` pode ser um pouco estranho de entender quando usar, afinal, para que eu vou colocar um valor em um atributo do meu objeto sem ter um método para lê-lo?

A resposta é simples: Você pode querer um valor para fazer alguma operação com ele e retorna-lo de uma forma diferente. Vamos ver um exemplo:

```ruby
> eu = Humano.new('odinei')
=> #<Humano:0x00007fd577a279a8 @nome="odinei">
> eu.nome
=> "odinei"
> eu.ano_nascimento = 1992
=> 1992
> eu.idade
=> 28

```

No exemplo acima eu calculo a minha idade com base na atributo `ano_nascimento` que foi criada apenas para leitura!

Em ruby é muito mais comum usar os `attr_accessor`, `attr_reader` e `attr_writer` para criar métodos de leitura e escrita em vez de criar esses métodos "na mão" para termos menos linhas no nossos arquivos 😄!

# Quando usar attr_accessor e quando usar getters e setters?

Segundo o livro [Ruby Under a Microscope](http://patshaughnessy.net/ruby-under-a-microscope) escrito pelo [Pat Shaughnessy](http://patshaughnessy.net/) (leitura recomendadíssima para quem quer entender como as mágicas do Ruby funcionam ;D) o Ruby otimiza o uso do *attr_reader*, *attr_writer* e *attr_accessor* fazendo a criação e acesso à variáveis de instância funcionar mais rápido 🚗💨!

O livro entra em mais detalhes do porquê os *attr_accessor* serem mais rápidos do que os outros *getters* e *setters* mas basicamente o Ruby implementa métodos escritos em C que são especializados no tratamento dos *attr_accessors*, ou seja, eles não são simples atalhos  para os métodos em C que criam os *getters* e *setters*.


Caso você queira ler a explicação completa no Ruby Under a Microscope, a parte que trata desses métodos estão na página 97 em *"Calling attr_reader and attr_writer"* e na página 98 em *"Method Dispatch Optimizes attr_reader and attr_writer".*

Espero que tenham gostado do texto é até uma próxima! 👋

## Fontes

- [Ruby Under a Microscope](http://patshaughnessy.net/ruby-under-a-microscope)
- [JetBrains Mono](https://www.jetbrains.com/pt-pt/lp/mono/) (essa aqui eu uso no Sublime 😆)
- Principalmente [isso aqui](https://www.youtube.com/watch?v=AAZWiY_ZfP0) (brincadeira 😅)
