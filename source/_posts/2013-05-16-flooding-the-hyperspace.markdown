---
layout: post
title: "Flooding the Hyperspace"
author: pfac
date: 2013-05-16 23:18
published: true
comments: true
categories: 
---

Rescaldo da sessão #3, grafos e um ornitorrinco.

<!--more-->

A sessão #3, empobrecida pelas ausências típicas das Monumentais Festas do Enterro da Gata, baseou-se no tema de grafos. Durante a sessão fizemos uma revisão do que são grafos, como se representam, e resolvemos uma variante do problema _"Hyperspace Jumping"_ com uma implementação do algoritmo __flood fill__ aplicado a grafos.

Segue abaixo um resumo para os ausentes. Deixem as vossas dúvidas mais imediatas nos comentários, e tragam as mais complexas para a próxima sessão.

__NOTA:__ Desafio aqueles que estiveram presentes a responder às dúvidas dos colegas nos comentários. Têm aqui uma forma de tentar ganhar as recompensas que vos prometi :beer:. Se não tiverem dúvidas para responder, estejam à vontade para transmitir o vosso feedback desta sessão (os menos corajosos que mandem as críticas ao [Perry](http://en.wikipedia.org/wiki/Perry_the_Platypus)). 


## Grafos

![First example](/images/graphs/graph1.svg "First example")
![Directed Graph](/images/graphs/digraph1.svg "Directed Graph")

Um grafo é constituído por um conjunto de vértices e pelas arestas que os ligam. Grafos podem ser __orientados (ou direcionados)__, em que cada aresta só pode ser percorrida num dado sentido, ou __não direcionados__, em que as arestas são válidas para ambos os sentidos. Podem ainda ser __cíclicos__ ou __acíclicos__, dependendo se, em algum vértice, é possível começar a percorrer arestas do grafo e voltar ao mesmo sítio.

![Graph with labels](/images/graphs/graph2.svg "Graph with labels")

Tanto os vértices como as arestas de um grafo podem ter etiquetas, contendo informação relevante para o problema. Problemas com valores associados às arestas são típicos; este tipo de grafos são também chamados de __pesados__, por cada aresta ter um "peso" associado. Etiquetas nos vértices são usadas, por exemplo, para representar uma capacidade ou um custo de visita.


### Estruturas de dados

Existem basicamente duas formas distintas para representar grafos: __matrizes de adjacências__ e __listas de adjacências__.

<img src="/images/tables/graph2.svg" alt="Adjacency Matrix" style="height:150px" />

Matrizes de adjacências são matrizes quadradas, com uma coluna e linha para cada vértice. Cada célula `(i,j)` contém a etiqueta da aresta que liga o vértice `i` ao vértice `j`. Para grafos não direcionados esta matriz é simétrica. Para grafos não pesados, cada célula contem 0 ou 1, dependendo se a aresta existe ou não.

![Adjacency List](/images/graphs/graph2_al.svg "Adjacency List")

Listas de adjacências são compostas por um vector, em que cada posição corresponde a um dos vértices (a origem da aresta). Em cada posição deste vector é colocada uma lista; cada célula corresponde a um vértice de destino, e pode ainda conter uma etiqueta com informação adicional.

Cada forma tem os seus pontos fortes e fracos. Matrizes permitem acesso imediato e cada célula ocupa menos espaço em memória, mas as arestas não existentes também são representadas. Com listas apenas as arestas existentes ocupam espaço, mas o acesso é mais lento.

A característica mais importante para decidir qual usar é a densidade de arestas. Um grafo com muito denso é melhor representado por uma matriz, enquanto que um grafo esparso é melhor representado com uma lista.


## Hyperspace Jumping (sort of)

Já está no [repositório](https://github.com/pfac/dpum) o código feito [nesta sessão](https://github.com/pfac/dpum/tree/master/problems/003-hyperspace-jumping/flood.cpp). Este código usa uma lista de adjacências para representar o universo e resolve uma variação do problema _"Hyperspace Jumping"_ sem as limitações impostas pelo gasto de energia da nave (sem estas limitações o algoritmo é um caso típico de __flood fill__) usando _Breadth First Search_.

Na próxima sessão vamos extender este código para resolver completamente este problema, e estudar melhor o _"The Toxic Clouds of Proxima III"_. Tragam dúvidas e muita vontade.

__Próxima sessão:__ Quinta-feira, 24 de Maio, 16h
