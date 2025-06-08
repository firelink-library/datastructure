---
title: Listas
sidebar_position: 2
slug: /listas
---

Legal, minha sugestão de leitura é verificar o material sobre tipo abstrato de dado antes de ver esse aqui! Só para entrar no mesmo conceito de o que estamos conversando sobre abstração e forma de separar responsabilidades.

## 1. Um comportamento específico

Antes de iniciarmos com alguma coisa de código (eu sei, eu sei, você veio pelo código! Calma já vamos chegar ai), quero convidar vocês para uma reflexão: o que é o comportamento de uma lista?

> "Sério que vamos filosofar sobre isso denovo?"

Sim ou com certeza? O comportamento de uma lista, em estruturas de dados, refere-se a uma coleção ordenada de elementos, onde cada elemento ocupa uma posição (índice) e pode ser acessado, inserido ou removido de acordo com sua posição. **Importante**: ordenada quer dizer que os elementos tem e mantém a ordem que foram inseridos dentro dela, não que eles ficam ordenados como ordem crescente ou decrescente. Isso depende da forma como eles foram inseridos ou ordenados dentro dela.

As principais características de uma lista são:

- **Ordem dos elementos:** Os elementos são mantidos em uma ordem específica, geralmente a ordem de inserção.
- **Acesso sequencial ou por índice:** É possível acessar qualquer elemento da lista informando sua posição.
- **Inserção e remoção:** É possível inserir ou remover elementos em qualquer posição da lista.
- **Tamanho variável:** O número de elementos pode crescer ou diminuir conforme necessário.

O conceito de lista está presente em várias situações do dia a dia, muitas vezes de forma intuitiva. Alguns exemplos:

- **Lista de compras:** Você anota os itens que precisa comprar, pode adicionar novos itens, riscar (remover) os que já comprou, e acessar qualquer item da lista.
- **Fila de espera em consultório:** As pessoas entram na fila (lista), podem ser chamadas (removidas) ou alguém pode entrar em uma posição específica (por exemplo, prioridade para idosos).
- **Playlist de músicas:** As músicas são organizadas em uma ordem, você pode adicionar, remover ou reordenar músicas.
- **Agenda de compromissos:** Os compromissos são listados em ordem de horário, mas você pode inserir um novo compromisso em qualquer horário (posição).
- **Pilhas de livros ou papéis:** Você pode adicionar ou remover livros/papéis de qualquer posição da pilha.

Show! Agora temos um comportamento definido, um objetivo a ser implementado e um sonho! Bora agora para os contratos que vamos assinar!

## 2. Contratos ou compromissos assumidos

> "Calma lá Murilão!" 
Operações típicas de uma lista

- Adicionar elemento ao final (append)
- Inserir elemento em uma posição específica
- Remover elemento de uma posição específica
- Acessar elemento por índice
- Percorrer todos os elementos (iterar)

