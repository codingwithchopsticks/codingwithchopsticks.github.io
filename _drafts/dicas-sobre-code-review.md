---
title: Dicas sobre Code Review
description: Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
updated: 2016-08-08 23:37
---

<small>
  ![People at a book fair](/assets/dicas-sobre-code-review/1.jpg "People eating a meal around a table")
  *Photo by [Charlie Read](https://unsplash.com/@charliereadd) on [Unsplash](https://unsplash.com/photos/3nBzJH_NYWg?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)*
</small>

Desde quando comecei a trabalhar na Plataformatec, tenho ouvido muito sobre como fazer um bom Pull Request. Recebi valiosas dicas sobre a forma de escrever a mensagem do Pull Request, como me expressar, como receber e como responder comentários.

Mas continuei com uma dúvida bem simples: E o Code Review? Como fazer um bom Code Review?

Desde quando me conheço por programador que faz Code Reviews, tenho a impressão que um Code Review de valor é aquele consegue perceber problemas de código, seja eles de organização, de performance ou algum problema em regras de negócio. Ou aquele que consegue sugerir alguma melhoria no seu código.

Ou ainda aquele comentário onde a pessoa tem o poder da Espada Justiceira e consegue ver além do alcance e dizer que, talvez, seu código pode dar algum problema lá na frente num ponto onde você nem imagina onde seu código iria chegar.

Sempre achei que conforme eu fosse evoluindo como programador eu iria conseguir identificar esses pontos em Pull Requests e assim, iria melhorar a forma que eu faço Code Review.

Mas caí, mais uma vez, numa dúvida conhecida:

"Eu não faço code reviews porque eu não tenho experiência ou eu não tenho experiência por que não faço code reviews?"

Nesse momento, caro leitor, percebi que estava na hora de escalar essa dúvida e aproveitar melhor as pessoas que trabalham comigo.

Fui expor a minha dúvida para o [João](https://twitter.com/noteu), um colega de trabalho que programa a muito tempo e que é uma ótima companhia para conversas.

Expus minhas dúvidas e ele me deu valiosas dicas de como fazer um code review saindo um pouco disso de olhar apenas para melhorias de código:

0. Se você trabalhar com Kanban ou alguma outra forma de organização de tarefas, você pode observar a tarefa referente aquele PR e verificar se a descrição do Pull Request cobre o que foi pedido na descrição da tarefas.

1. Você pode também olhar para a descrição do Pull Request e/ou da tarefa e ver se tem algo que pode não ter sido coberto no código.

2. Olhando para o código, você pode olhar os testes e ver se tem algum caso que não foi coberto, ou então, sugerir um teste em alguma condição mais específica para a funcionalidade.

---

Posso dizer que saí muito satisfeito da nossa conversa e tenho aplicado essas dicas nos meus code reviews. Não virei nenhum mestre em
revisar código mas essas dicas tem me ajudado muito!

Para completar, vou deixar alguns links sobre code review que tem me ajudado muito no meu dia-a-dia:

- [Human Code Reviews pt. 1](https://mtlynch.io/human-code-reviews-1)
- [Human Code Reviews pt. 2](https://mtlynch.io/human-code-reviews-2)
- [Plataformatec Guidelines for Pull Requests](http://guidelines.plataformatec.com.br/pull-requests.html#reviewing-pull-requests)
- [Awesome Code Reviews: Articles (Github Repo)](https://github.com/joho/awesome-code-review#articles)
