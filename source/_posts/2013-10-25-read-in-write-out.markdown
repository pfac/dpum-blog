---
layout: post
title: "BOOM! We're back!"
date: 2013-10-25 20:00
comments: true
categories: [snippets, c++]
---

Uma tarefa comum a todos os problemas num torneio é a interpretação de input. Isto é algo característico de cada linguagem. C usa `scanf`, Java usa `InputStream`s, e C++ usa `stream`s.

Este artigo tem como objectivo mostrar como é feita a leitura dos parâmetros em C++, algo que pode ser um desafio para os mais inexperientes com a linguagem.

<!--more-->

## Hashmat the Brave Warrior

[Este problema](http://uva.onlinejudge.org/index.php?option=com_onlinejudge&Itemid=8&page=show_problem&problem=996) é um bom exemplo para mostrar a leitura de parâmetros em C++. A resolução do problema consiste em ler pares de números e imprimir a sua diferença.

Ao contrário do que acontece com C, a forma ideal de percorrer um `stream` até ao fim (como o _standard input_) em C++ consiste em utilizar o próprio `stream` como condição de teste. Isto permite que seja testada não só a condição de _end-of-file_, mas também outros erros que impossibilitem a leitura de mais parâmetros.

Junta-se a isto uns pozinhos para calcular a diferença de dois inteiros de 64 bits (porque o limite do problema exige pelo menos 33 bits), e temos o problema resolvido.

```c++
#include <iostream>

using namespace std;

#define DIFF(x,y) ((x) > (y) ? (x) - (y) : (y) - (x))

int main () {
	while (cin) {
		long long int army[2];
		cin >> army[0] >> army[1];
		long long int diff = DIFF(army[0], army[1]);
		cout << diff << endl;
	}
	return 0;
}
```


## The line of offense

Uma variante também comum nos problemas de torneios é a leitura de parâmetros linha por linha. Ao contrário do que acontece com C, em que tem de ser estabelecido um _buffer_ de tamanho fixo, em C++ é possível guardar toda a linha numa `string` usando a função `getline`. Usando depois um `stringstream`, os dados podem ser obtidos a partir da mesma forma que seriam a partir do _standard input_.

```c++
#include <iostream>
#include <sstream>

using namespace std;

#define DIFF(x,y) ((x) > (y) ? (x) - (y) : (y) - (x))

int main () {
	string line;

	while (getline(cin, line)) {
		stringstream ss;
		long long int army[2];

		ss << line;
		ss >> army[0] >> army[1];

		long long int diff = DIFF(army[0], army[1]);

		cout << diff << endl;
	}

	return 0;
}
```
