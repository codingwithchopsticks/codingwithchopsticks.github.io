---
title: Quando usar e quando não usar gems?
description: Essa pergunta é bem boa... Nesse texto eu falo um pouco sobre a minha forma de pensar quando me deparo com essa questão. Não sei se a minha opinião é a opinião da maioria das pessoas na comunidade Ruby porém espero que você termine de ler esse texto e tenha um pouco mais de insumos para te ajudar a decidir quando usar e quando não usar gems :D
updated: 2016-08-08 03:32
---

<small>
  ![Placas de trânsito pintadas de preto e branco indicando mão única](/assets/2020-06-13-quando-usar-e-quando-não-usar-gems/1.jpeg "Placas de trânsito pintadas de preto e branco indicando mão única")
  *Photo by [Brendan Church](https://unsplash.com/@bdchu614) on [Unsplash](https://unsplash.com/s/photos/choose?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)*
</small>

> Essa pergunta foi feita pelo Leonardo Fragozo lá no [canal Ruby Brasil no Telegram](https://t.me/rubybrasil) e achei bacana postar a resposta em forma de texto para servir de consulta para quem mais tiver esse tipo de dúvida.

Nesse texto eu falo um pouco sobre a minha forma de pensar quando me deparo com essa questão. Não sei se a minha opinião é a opinião da maioria das pessoas na comunidade Ruby porém espero que você termine de ler esse texto e tenha um pouco mais de insumos para te ajudar a decidir quando usar e quando não usar gems.

## Um pouco sobre dependência e como decidir qual usar

Usar uma gem significa ter uma dependência no seu projeto. Significa você ficar dependente de um código externo que você não tem muito controle. Logo, é bom pensar em quem mantém as gems que você tá usando. No caso de usar uma gem, é melhor você usar uma que seja atualizada com alguma frequencia e/ou que tenha uma empresa por trás da manutenção dela.

Um lugar legal que pode ajudar muito a ver como anda a "saúde" de uma gem ("saúde" de uma gem seria se a gem recebe updates, se tem muitas _issues_ abertas, etc.) é o [Ruby Toolbox](https://www.ruby-toolbox.com)!

Dê uma olhada na categoria [_Background Jobs_](https://www.ruby-toolbox.com/categories/Background_Jobs?display=compact&order=score) (processamento em segundo plano). Na página você verá um gráfico comparando o _score_ de cada gem da categoria (sinceramente, não sei como esse _score_ é calculado 😅). Mais para baixo você encontra todas as gems da categoria com informações como quantidade de downloads, quantidade de estrelas no GitHub e algumas _badges_ falando sobre a saúde do projeto:

<small>
  ![Screenshot da tela da categoria Background Jobs do Ruby Toolbox](/assets/2020-06-13-quando-usar-e-quando-não-usar-gems/ruby-toolbox.png "Screenshot da tela da categoria Background Jobs do Ruby Toolbox")
  *Screenshot da tela da categoria Background Jobs do Ruby Toolbox*
</small>

## Usar ou não usar gems, eis a questão

Eu gosto de usar gems quando eu preciso de uma solução que não seja o foco do meu negócio e que seja para algo mais complexo de lidar. Um exemplo bem bom disso é autenticação. Autenticação dificilmente vai ser core no meu negócio, então eu posso delegar isso para uma gem como o [Devise](https://github.com/heartcombo/devise), por exemplo ❤️ .

Outra situação onde eu posso usar uma gem é para validação de CPF. Denovo, isso não é o core do meu negócio e eu posso delegar isso para uma gem. Porém validar CPF não é algo tão complexo como autenticação. Eu posso fazer uma [validação mais simples](https://www.campuscode.com.br/conteudos/codigo-ruby-para-calculo-de-validacao-de-cpf), por exemplo, e não ter uma dependência desse tipo no meu projeto.

Vamos ver outro caso aqui: Eu tenho uma loja online e preciso cotar frete nos correios e em empresas de entregas. Isso é parte do meu negócio, posso delegar para uma gem? Posso (porém eu não sei se existem gems que façam isso). Porém eu teria uma dependência externa de um código que eu não tenho muito controle. Se eu fizer essa pesquisa de frete na minha aplicação, eu tenho muito mais controle das consultas e posso utilizar esses dados com mais inteligência e exibir um comparativo das empresas que fazem entregas, por exemplo.

## Um pouco mais de lenha na fogueira 🔥

Antes de finalizar, quero puxar um assunto bacana aqui:  As vezes, faz sentido reinventar a roda!

As vezes faz sentindo você implementar algo que não faz parte do seu negócio dentro do seu projeto. Principalmente se você estiver estudando novas tecnologias.

É muito fácil pegar o Devise, por exemplo, e botar ele pra funcionar. Ele só funciona e pronto. Mas ai eu te pergunto, você sabe o que tá acontecendo embaixo dos panos ali?

O próprio [README do Devise recomenda *não* usá-lo se você estiver construindo sua primeira aplicação em Rails](https://github.com/heartcombo/devise/blob/master/README.md#starting-with-rails) (eu AMO essa parte desse README)

<small>
  ![Screenshot do README do Devise](/assets/2020-06-13-quando-usar-e-quando-não-usar-gems/devise-readme-screenshot.png "Screenshot do README do Devise")
  *Screenshot do README do Devise*
</small>

_Tradução: Iniciando com Rails? Se você estiver construindo sua primeira aplicação Rails, nós recomendamos que você não use o Devise. O Devise requer um bom conhecimento do Rails. Nestes casos, nós recomendamos que você começe com uma autenticação básica. Aqui tem algumas fontes que podem te ajudar (fontes em inglês):_

- _O livro do Michael Hartl: [https://www.railstutorial.org/book/modeling_users](https://www.railstutorial.org/book/modeling_users)_

- _Railscasts com Ryan Bate: [http://railscasts.com/episodes/250-authentication-from-scratch](http://railscasts.com/episodes/250-authentication-from-scratch) e [http://railscasts.com/episodes/250-authentication-from-scratch-revised](http://railscasts.com/episodes/250-authentication-from-scratch-revised)_

- _Ruby on Rails no Codecademy: Authentication and Authorization: [https://www.codecademy.com/learn/rails-auth](https://www.codecademy.com/learn/rails-auth)_


Por último, mas de forma alguma menos importante, um grande amigo, o glorioso [Paulo Henrique](https://twitter.com/EuSouUmPaulo) fez uma talk sobre porque, as vezes, é importante "reinventar a roda" e eu recomendo DEMAIS que ela seja assistida: 

<iframe width="560" height="480" src="https://www.youtube.com/embed/l2q94BE2mA8" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## Concluindo

É um pouco complexo saber quando usar gems ou não. Acho que o que eu escrevi aqui nesse texto pode ajudar mas não deixe de desenvolver seu próprio “faro” para quando usar gems ou não.

Espero que tenham gostado do texto é até uma próxima! 👋
