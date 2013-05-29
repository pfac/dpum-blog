---
layout: post
title: "The Shortest Path to Pretty Much Anywhere"
date: 2013-05-29 12:25
comments: true
categories: 
---

## Resumo da sessão #4
- Revisão do conceito de grafo e das estruturas de dados usadas na sua representação;
- O algoritmo de Dijkstra, também conhecido como o algoritmo do [Caminho Mais Curto](http://en.wikipedia.org/wiki/Dijkstra's_algorithm);
- Modificação da implementação da sessão #3 para o problema __[Hyperspace Jumping](https://github.com/pfac/dpum/tree/master/problems/003-hyperspace-jumping)__, agora incluindo a restrição da energia e usando o algoritmo de Dijkstra.
- Batismo implícito dos participantes com nomes muito mais fixes que aqueles que trazem no Cartão de Cidadão.

<!--more-->

A curiosidade despertada pelo nome do senhor que inventou o algoritmo em que a sessão #4 se focou ("_Dijkstra_", que raio, quase que só tem consoantes), levou a que fosse feita uma pequena pesquisa para este post, de forma a elucidar todos sobre quem foi exatamente este indivíduo.

## Um bocadinho de história

{% blockquote Edsger W. Dijkstra %}
Brainpower is by far our scarcest resource.
{% endblockquote %}

O professor Edsger Dijsktra, nascido a 1930 em Rotterdam (Nederland), filho de um professor de física, estudou também ele física no início da sua vida académica. A sua mãe, sem nunca ter tido um emprego formal, teve uma influência determinante na sua abordagem à matemática e no seu ênfase pela elegância.

Com a intenção de se tornar um físico teórico, Dijkstra pensou que a utilização de um computador pudesse vir a ser vantajosa no seu percurso, pelo que passou três anos a programar no Mathematisch Centrum em Amsterdam. Estes três anos convenceram-no que o desafio intelectual de programar excedia o da física, mas não havia um corpo de conhecimento sólido onde basear a programação como uma disciplina intelectualmente respeitável.

O algoritmo do caminho mais curto foi desenvolvido por Dijkstra enquanto relaxava, e apresentado na inauguração do computador [ARMAC][dijkstra_armac] em 1956 para resolver um problema interessante para o público em geral: dada a rede de estradas que liga um conjunto de cidades, qual o caminho mais curto entre duas dessas cidades. O algoritmo de Dijkstra ainda é uma das melhores alternativas para resolver este tipo de problemas (dependendo da quantidade de informação disponível), sendo bastante usado em [comunicações por computador](https://en.wikipedia.org/wiki/Routing#Link-state_algorithms).

As contribuições de Dijkstra não se ficaram por este algoritmo, mas essas são deixadas para outra altura. Os mais curiosos podem seguir os links [1][dijkstra_amturing] e [2][dijkstra_mathcenter].


## O algoritmo

O algoritmo de Dijkstra pode ser entendido como uma modificação do __Flood Fill__. Sendo o algoritmo para resolver o problema do caminho mais curto, é usado com grafos __pesados__, mas só funciona quando o valor de cada ligação __não é negativo__.

Dado um ponto de partida, o algoritmo começa por anotar o custo desse ponto como nulo (não custa nada chegar ao ponto em que se começa) e marca-o como visitado. De seguida seleciona-se a aresta de saída com custo mais baixo, e anota-se o custo dessa aresta no ponto de destino, marcando-o também como visitado.

Considerando agora as arestas de saída de todos os pontos já visitados, seleciona-se a aresta com menor custo. O custo a anotar no ponto de destino é o custo anotado no ponto de origem da aresta adicionado ao custo da própria aresta. Esse ponto de destino é então marcado como visitado.

No caso de um ponto de destino já possuir um custo associado (i.e., já tiver sido visitado), o custo final será o menor.

Sempre que o custo de um dado ponto muda (ou porque é visitado pela primeira vez ou porque o novo custo é mais baixo), é registada a aresta associada a esse custo.

O algoritmo repete até que todos os pontos tenham sido visitados. No final, o conjunto de arestas registadas constitui o sub-grafo cujos caminhos são os mais curtos desde o ponto de partida para todos os outros.


## Hyperspace Jumping

Tendo agora em consideração as limitações energéticas da nave, o algoritmo de __Flood Fill__ original não é capaz de resolver o problema, pelo que se tem de mudar para o algoritmo de __Dijkstra__.

Tal como na implementação anterior, a representação do grafo como uma lista de adjacências é a que faz mais sentido. Olhe-se para os [limites](https://github.com/pfac/dpum/tree/master/problems/003-hyperspace-jumping#constraints): o número máximo de pontos `N` é igual ao número máximo de wormholes `H`. Logo a densidade máxima do problema é de uma aresta por ponto. Uma matriz de adjacências seria demasiado esparsa.

No caso particular deste problema não é necessário saber a origem da aresta que se usou para chegar a um dado ponto. Assim, ao acrescentar uma aresta à fila é apenas anexado o custo total até ao ponto de destino da aresta. Em C++ podemos representar o par _(destino,custo)_ como um elemento do tipo `pair<int,int>`.

Para tirar partido da ordenação automática utiliza-se uma `priority_queue`, disponível na STL. Utilizando `pair` como tipo dos elementos da fila, a ordenação é automática: ordena pelo primeiro elemento, usando o segundo em caso de empate. Por esta razão, inverte-se o significado dos valores nas arestas, sendo estas representadas na forma _(custo,destino)_.

O custo final para chegar a cada ponto é guardado num vector `costs`. Sempre que uma dada aresta permite chegar a um ponto já visitado por um custo inferior, este valor é substituído.

Foi ainda implementado um último "truque", tirando partido do problema. Uma aresta, quando inserida na fila, é associada ao custo __total__ de chegar ao destino e é sempre selecionada a aresta com o custo total mais baixo. Desta forma, a primeira vez que este custo exceder a energia disponível o algoritmo pode ser interrompido.

O código produzido na última sessão já está no [repositório](https://github.com/pfac/dpum/blob/master/problems/003-hyperspace-jumping/dijkstra.cpp). Foram acrescentados comentários e alguns tipos foram redefinidos para facilitar a compreensão. Todas estas definições estão devidamente comentadas no início do ficheiro. Tal como nas sessões anteriores, deixem as vossas dúvidas na zona de comentários, se as tiverem.


## Próxima Sessão

__Quinta, 30 de Maio, às 16h na sala 1.09__ 

Na próxima sessão (que é já amanhã, podem desancar na organização pelo atraso), vamos extender o algoritmo de Dijkstra para o algoritmo [A*](http://en.wikipedia.org/wiki/A*_search_algorithm). O novo algoritmo é o ideal para resolver o problema _The Toxic Clouds of Proxima III_, pelo que devem ter este problema bem percebido, de forma a acelerar as coisas. Se quiserem estudar o algoritmo previamente podemos focar esta sessão na parte prática.

Havendo a possibilidade, vamos ainda revisitar a sintaxe de C++, em especial vamos tentar focar a programação orientada a objetos. Tragam as vossas questões.


[dijkstra_amturing]: http://amturing.acm.org/award_winners/dijkstra_1053701.cfm "Edsger W. Dijkstra - A.M. Turing Award Winner"
[dijkstra_mathcenter]: http://cs-exhibitions.uni-klu.ac.at/index.php?id=29 "Mathematical center Amsterdam"
[dijkstra_armac]: http://www-set.win.tue.nl/UnsungHeroes/machines/armac.html "ARMAC | Unsung Heroes in Dutch Computing History"
