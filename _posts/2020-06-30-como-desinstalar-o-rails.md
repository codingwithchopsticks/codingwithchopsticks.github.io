---
title: Como desinstalar o Rails?
description: Bom, nem sempre as coisas acontecem como esperamos e, as vezes, precisamos desinstalar o Rails. Seja para fazer downgrade de versão, para corrigir alguma coisa na instalação ou porque você não gostou do framework (#triste). Seja qual for seu motivo, espero que esse post te ajude :D
updated: 2020-06-30 03:32
---

<small>
  ![Capa do álbum "¡Adiós Amigos!" da banda nova iorquina de Punk Rock, Ramones](/assets/2020-06-30-como-desinstalar-o-rails/2.jpeg "Capa do álbum "¡Adiós Amigos!" da banda nova iorquina de Punk Rock, Ramones")
  *Capa do álbum "¡Adiós Amigos!" dos Ramones. Foto disponível em [Anomalia Distro](https://anomaliadistro.com.br/produtos/ramones-adios-amigos-lp/). Acessado em 30/06/2020.*
</small>

Bom, nem sempre as coisas acontecem como esperamos e, as vezes, precisamos desinstalar o Rails. Seja para fazer downgrade de versão, para corrigir alguma coisa na instalação ou porque simplesmente não gostamos do framework (#triste).

A idéia de fazer esse post me veio depois que [um amigo](https://github.com/MoisesBorges) me perguntou como ele poderia desinstalar o Rails para instalar uma versão mais antiga. Obrigado Moisés por todas as perguntas muito instigantes que você tem me feito durante seu processo de aprender Rails!

E se por acaso você queira instalar a última versão do Rails, você pode seguir o [Rails Guides (em inglês).](https://guides.rubyonrails.org/v5.0/getting_started.html#installing-rails)

## Aviso antes de zarpar 🚢!

Tudo o que vou fazer aqui foi feito no meu computador pessoal, ele roda o MacOS 10.15.5, Ruby 2.7.1 gerenciado pelo ASDF e o meu terminal é o kitty 🐱💻.

(Para quem não entendeu o porquê de eu ter dado essas informações, acho boa prática dizer qual ambiente eu estou utilizando para realizar os procedimentos e isso não quer dizer que você não vai conseguir seguir esse tutorial se tiver um ambiente totalmente diferente do meu. Caso tenha alguma dificuldade, fique a vontade para postar nos comentários desse post 😊)

## Mãos à obra!

Para tentar reproduzir um ambiente com mais de uma versão do Rails, instalei as versões 6.0.3.2, 5.2.4.3 e 4.2.11.3. Você pode checar as versões do Rails usando o seguinte comando:

```
→ gem list | grep rails
rails (6.0.3.2, 5.2.4.3, 4.2.11.3)
```

O comando `gem list` serve para listar todas as gems instaladas no seu computador. Enquanto o comando `| grep` (a barrinha na vertical se chama pipe e se pronuncia "páip") pega o resultado do comando `gem list` e pesquisa nele o que eu passar como argumento, o que no nosso caso é a palavra `rails`.

Para desinstalar uma dessas versões do Rails, podemos usar o comando `gem uninstall rails`:

```
→ gem uninstall rails

Select gem to uninstall:
 1. rails-4.2.11.3
 2. rails-5.2.4.3
 3. rails-6.0.3.2
 4. All versions
>
```

Olha que legal! O comando `gem` nos leva para uma CLI (_command line interface_ ou interface de linha de comando) onde podemos escolher, de forma interativa, qual versão do rails queremos desinstalar! Agora podemos digitar a posição da versão que queremos desinstalar ou desinstalar todas as versões! No meu caso, vou escolher a opção 2 para desinstalar o Rails 5.2.4.3.

```
gem uninstall rails

Select gem to uninstall:
 1. rails-4.2.11.3
 2. rails-5.2.4.3
 3. rails-6.0.3.2
 4. All versions
> 2
Successfully uninstalled rails-5.2.4.3
```

Uhul! Desinstalamos uma versão do Rails 🥳 🎉!

Rodando denovo o `gem list | grep rails` vemos que ele não lista mais a versão 5.2.4.3:

```
→ gem list | grep rails
rails (6.0.3.2, 4.2.11.3)
```

## Outra forma de fazer a mesma coisa

Outra forma de desinstalar uma versão de uma gem, é passar o numero da versão direto no comando `gem uninstall`. Por exemplo, para desinstalar a versão 6.0.3.2 do Rails, podemos usar `gem uninstall rails -v 6.0.3.2`. Vamos rodar esse comando no terminal:

```
→ gem uninstall rails -v 6.0.3.2
Successfully uninstalled rails-6.0.3.2
```

Denovo, checando as versões do Rails instaladas:

```
→ gem list | grep rails
rails (4.2.11.3)
```

Uau! Ficamos apenas com uma versão do Rails instalada!

## O Rails que me amava

Para finalizar, podemos rodar o comando `gem uninstall rails -v 4.2.11.3` (ou usar apenas `gem uninstall rails` já que só temos uma versão instalada) e desinstalar todas as versões do Rails!

Porém, ao rodar o comando `rails -v` em vez de vermos uma mensagem de erro, nos deparamos com isso:

```
→ rails -v
Rails 6.0.3.2
```

_"Como assim????? Eu desinstalei tudo!!!!!"_ você pode pensar, mas tem um ponto que eu não mencionei: Precisamos desinstalar todos os  _Railties_.

O Railties é a gem responsável por "colar" todas as peças do framework. É ela que faz todo o procedimento inicial para rodarmos um app Rails, nos dá comandos CLI do framework e os generators. Caso se interesse, essa gem está disponível [lá no GitHub.](https://github.com/rails/rails/tree/master/railties)

Como o Railties é uma gem, podemos desinstalar ela rodando o comando `gem uninstall railties`. Como não estamos passando a versão, vamos entrar no modo interativo onde podemos desinstalar todas as versões da gem Railties de uma vez só:

```
→ gem uninstall railties

Select gem to uninstall:
 1. railties-4.2.11.3
 2. railties-5.2.4.3
 3. railties-6.0.3.2
 4. All versions
> 4
Successfully uninstalled railties-4.2.11.3
Successfully uninstalled railties-5.2.4.3
Remove executables:
        rails

in addition to the gem? [Yn]  y
Removing rails
Successfully uninstalled railties-6.0.3.2
```

Você pode notar que antes de desinstalar a ultima versão do Rails ele pergunta se você deseja desinstalar o executável de linha de comando "rails". Digite apenas "y" para "yes" (ou "s" para "sim", caso seu esteja em português) para finalizar a desinstalação. E para termos certeza que desinstalamos o Rails de uma vez por todas:

```
rails -v
asdf: No preset version installed for command rails
```

Pronto! Rails desinstalado! No seu computador, a segunda linha pode ser um pouco diferente. A minha aparece assim porque utilizo o [ASDF](https://github.com/asdf-vm/asdf) para gerenciar as versões das linguagens de programação que uso no meu computador. Caso você não utilize um gerenciador para isso, recomendo que use um :D

## Ora, ora! Um Xeroque Rolmes!

Caso você tenha notado, sempre que rodamos o comando `gem list | grep rails` aparecem outras gems com a palavra "rails" no nome. Essas gems são de funcionalidades descontinuadas nas versões mais novas do Rails que foram extraidas para gems externas para que as versões antigas possam continuar utilizando. Aqui no meu computador, tenho as seguintes gems dessa situação:

```
→ gem list | grep rails
rails-deprecated_sanitizer (1.0.3)
rails-dom-testing (2.0.3, 1.0.9)
rails-html-sanitizer (1.3.0)
sprockets-rails (3.2.1)
```

Para desinstalá-las, você pode usar o nosso bom e velho `gem uninstall <nome da gem>`.

Espero que tenham gostado do texto é até uma próxima! 👋

## Fontes

- [Stack Overflow - Uninstall Rails completely](https://stackoverflow.com/a/38607861)
- [JetBrains Mono](https://www.jetbrains.com/pt-pt/lp/mono/) (essa aqui eu uso no Sublime 😆)
