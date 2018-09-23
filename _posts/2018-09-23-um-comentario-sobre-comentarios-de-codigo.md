---
title: Um comentário sobre comentários de código
description: Comentários de código é uma daquelas coisas que costumam dividir os programadores. Nesse post eu vou comentar sobre o assunto e falar um pouco das minhas experiências.
updated: 2016-08-08 23:37
---

<small>
  ![People eating a meal around a table](/assets/2018-09-23-a-comment-about-code-comments/1.jpg "People eating a meal around a table")
  *Photo by [Priscilla Du Preez](https://unsplash.com/@priscilladupreez) on [Unsplash](https://unsplash.com/photos/W3SEyZODn8U?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)*
</small>

Comentários de código foram algo muito confuso para mim por muito tempo. Durante a faculdade, todos os professores de todas as disciplinas que abordavam programação de software sempre diziam que todo o seu código deveria ser comentado. As justificativas sempre eram no sentido de que quando você, ou outra pessoa, precisar voltar naquele trecho, o comentário iria ajudar o programador a compreender melhor o que o código está fazendo. Eu concordo com a faculdade, em partes, mas preciso dizer que acabava sempre fazendo esse tipo de comentário:

```ruby
  # Public: Return the sum of two numbers.
  #
  # number1 - First number to sum.
  # number2 - Second number to sum.
  #
  # Examples
  #
  #   sum(2, 5)
  #   # => 7
  #
  # Returns the duplicated String.
  def sum(number1, number2)
    number1 + number2
  end
```

Fora da faculdade, quando comecei a usar linguagens com propostas mais modernas, me deparei com pessoas, livros e posts que diziam que meu código precisava ser limpo, auto-explicativo e qualquer tipo de comentário deveria ser evitado em favor de um código que fosse mais limpo e mais auto-explicativo. Um memória muito boa que tenho disso é do meu bom amigo [Arthur](https://github.com/arthurfsilva) comentando sobre um parágrafo do livro [Clean Code](https://www.amazon.com.br/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882) escrito por Robert C. Martin, mais conhecido como [Uncle Bob](https://blog.cleancoder.com/):

> `So when you find yourself in a position where you need to write a comment, think it through and see whether there isn’t some way to turn the tables and express yourself in code. Every time you express yourself in code, you should pat yourself on the back. Every time you write a comment, you should grimace and feel the failure of your ability of expression. `

Robert C. Martin. Clean Code. Page 54, line 7.

_(Tradução livre: Então quando você se ver numa situação onde precisa escrever um comentário, pense se não há uma maneira de contornar e se expressar através de código. Sempre que conseguir se expressar através do código, você deve dar-se um tapinha nas costas. Sempre que não conseguir, você deve fazer uma careta e sentir a falha da suas habilidades de expressão.)_

## Ok, vamos tentar no mundo real agora

Num belo dia, me pego escrevendo uma função onde eu desejei desde o primeiro caractere que houvesse um comentário para que eu economizasse tempo quando precisasse voltar a ela.

Em vez de explicar o que está acontecendo, vou deixar o código com seu comentário e sugerir um exercício: Imagine que não há comentário documentando o código e tente entender o que a função faz. Acredito que a tarefa será um pouco complicada.

```ruby
# In some worksheet rows, is returned formula errors that are inside
# an extra cell object, at the end of map process, an array is returned
# with an extra element.
#
# As we are treating that values by this position, this extra element
# in the array beginning causes validations errors when the line is
# persisted on the database.
#
# Examples
#
#  clean_formula_errors_from(['item 1', 'item 2', 'item 3'])
#  # => ['item 1', 'item 2', 'item 3']
#
#  clean_formula_errors_from(['#SomeKindOfError!', 'item 1', 'item 2', 'item 3'])
#  # => ['item 1', 'item 2', 'item 3']
#
# Returns an array without error items
def clean_formula_errors_from(row)
  row.map(&:value)
    .reject { |value| value.to_s.match?(/^\#\w*!$/) }
end
```

Muito mais simples de entender com o comentário, não?

Comentários valorosos para a sua aplicação são aqueles que, além de explicar o que o seu código faz, explica o por quê do seu código estar fazendo aquilo. Isso não invalida o fato de que você sempre deve manter o seu código o mais limpo e auto-explicativo possível, mas como vimos no exemplo, nem sempre é possível fazer um código totalmente auto-explicativo. Muitas vezes é necessário entender o contexto para que esse trecho de código de código limpo e auto-explicativo faça sentido.

## Dicas rápidas

Quando precisar fazer, deixe seus comentários com a linguagem o mais simples possível. Não economize na hora de escrever mas mantenha o bom senso: Se o seu comentário está muito grande considere refatorar seu código. Procure sempre a opinião de um colega de trabalho ou algum desenvolvedor mais sênior, seja pessoalmente ou na hora do Code Review. E sempre que surgir dúvidas sobre documentar ou não, provavelmente é melhor documentar.

Para escrever esses comentários do texto eu utilizei as regras do [TomDoc](http://tomdoc.org/). Vale muito a pena ler não importa qual seja seu nível de experiência em desenvolvimento de software. Embora o TomDoc seja focado em Ruby, há padrões para outras linguagens como [JSDoc](http://usejsdoc.org/) para Javascript ou as definições da [PEP 257](https://www.python.org/dev/peps/pep-0257/) para Python.

## Um (muito) breve comentário sobre documentação fora do código

Sobre documentação fora do código para procedimentos e/ou especificidades que não estejam totalmente ligadas ao código: Sim, vale muito a pena pois você compartilha o conhecimento sobre determinada parte do seu sistema com os demais programadores além de facilitar muito para programadores novos entenderem melhor sobre o sistema.

Fui breve aqui pois acredito que alguém possa ficar com dúvidas sobre comentários fora do código. E também por que pretendo abordar esse assunto melhor em post futuro.


Obrigado! 😄
