---
title: Pilhas
sidebar_position: 4
slug: /pilhas
---

## 1. O que são Pilhas

Uma **pilha** é um Tipo Abstrato de Dados que implementa o comportamento **LIFO** (“Last In, First Out”), isto é, o último elemento que entrou na estrutura será o primeiro a sair. Na vida real, é como uma pilha de pratos: você empilha um em cima do outro e, na hora de retirar, pega sempre o prato que está por cima.

> "Murilão, denovo mais uma estrutura? Por que tantas?"

Aqui você tem uma ótima pergunta! Trabalhar com diferentes estruturas, nos permite implementar comportamentos específicos por cada uma das estruturas. O que ganhamos com isso? Estruturas mais especializadas para realizar suas tarefas. Fica mais fácil de compreender como ela está funcionando e também nos permite manter melhor esse código.

As operações fundamentais de uma pilha são:

* **push(elemento):** insere um novo elemento no “topo” da pilha.
* **pop() → elemento:** remove e retorna o elemento que está no topo.
* **top() → elemento (ou peek):** consulta o elemento no topo sem removê-lo.
* **isEmpty() → booleano:** verifica se a pilha não contém elementos.
* **size() → inteiro:** retorna quantos elementos estão atualmente empilhados.

## 2. Por que usar uma pilha?

Vamos la, vamos ver algumas das aplicações que podemos desenvolver utilizando essa estrutura. Pessoal vale lembrar que podemos utilizar esse tipo abstrato quando for interessante utilizar este comportamento!

* **Controle de fluxo em chamadas de função:** a pilha de chamadas armazena cada frame de execução e desempilha quando a função retorna.
* **Desfazer/refazer (undo/redo):** em editores de texto ou gráficos, cada ação é empilhada para que possa ser revertida na ordem inversa.
* **Avaliação de expressões e parsing:** compiladores usam pilhas para converter e avaliar notações infix, prefix ou pós-fix.
* **Algoritmos de backtracking:** como DFS em grafos ou soluções de labirintos, empilha-se uma escolha e desempilha-se quando for preciso “voltar atrás”.

A abstração de pilha permite que você se concentre em **o que** precisa empilhar e desempilhar, sem expor detalhes de como a memória ou o vetor subjacente está sendo manipulado. Isso torna o código mais claro, flexível e fácil de manter.

## 3. Pseudocódigo das funções

Pessoal aqui vamos dar uma olhada em como são as funções que podem ser implementadas com as pilhas.

```sh
# Exemplo 1: Pilha com vetor (Array-Based Stack)

TAD PilhaArray
  CONSTANTES:
    MAX ← 100           # capacidade máxima da pilha

  ATRIBUTOS:
    dados: vetor[0..MAX-1] de Elemento
    topo: inteiro       # índice do próximo slot livre

  MÉTODOS:

    criar() -> PilhaArray
      pilha.topo ← 0
      RETORNAR pilha

    isEmpty() -> booleano
      RETORNAR (pilha.topo = 0)

    isFull() -> booleano
      RETORNAR (pilha.topo = MAX)

    push(elem: Elemento)
      SE isFull()
        ESCREVER "Erro: pilha cheia"
        RETORNAR
      pilha.dados[pilha.topo] ← elem
      pilha.topo ← pilha.topo + 1

    pop() -> Elemento
      SE isEmpty()
        ESCREVER "Erro: pilha vazia"
        RETORNAR nulo
      pilha.topo ← pilha.topo - 1
      RETORNAR pilha.dados[pilha.topo]

    top() -> Elemento
      SE isEmpty()
        ESCREVER "Erro: pilha vazia"
        RETORNAR nulo
      RETORNAR pilha.dados[pilha.topo - 1]

    size() -> inteiro
      RETORNAR pilha.topo
```

Vamos agora analisar alguns pontos desse pseudocódigo:

- A implementação é realizada com vetor.
- Criar a pilha, inicia seu topo com o valor zero.
- A operação de `push`, se a pilha não estiver cheia, adiciona o elemento no final da pilha.
- A operação de `pop` retira o elemento da pilha, o último que foi adicionado. 

## 4. Implementação em C

Agora, vamos ver a implementação do código em C:

```c
#include <stdio.h>
#include <stdbool.h>

#define MAX 100    // capacidade máxima da pilha

// Tipo PilhaArray armazenando inteiros
typedef struct {
    int dados[MAX];
    int topo;      // índice do próximo slot livre
} Pilha;

// Inicializa a pilha vazia
void criarPilha(Pilha *p) {
    p->topo = 0;
}

// Retorna true se a pilha estiver vazia
bool isEmpty(Pilha *p) {
    return (p->topo == 0);
}

// Retorna true se a pilha estiver cheia
bool isFull(Pilha *p) {
    return (p->topo == MAX);
}

// Insere elemento no topo
bool push(Pilha *p, int x) {
    if (isFull(p)) {
        printf("Erro: pilha cheia\n");
        return false;
    }
    p->dados[p->topo++] = x;
    return true;
}

// Remove e retorna o elemento do topo
// em *ret; retorna false em underflow
bool pop(Pilha *p, int *ret) {
    if (isEmpty(p)) {
        printf("Erro: pilha vazia\n");
        return false;
    }
    *ret = p->dados[--p->topo];
    return true;
}

// Consulta o topo sem remover
bool top(Pilha *p, int *ret) {
    if (isEmpty(p)) {
        printf("Erro: pilha vazia\n");
        return false;
    }
    *ret = p->dados[p->topo - 1];
    return true;
}

// Retorna o número de elementos na pilha
int size(Pilha *p) {
    return p->topo;
}

// Exemplo de uso
int main() {
    Pilha pilha;
    criarPilha(&pilha);

    // Empilhando valores
    push(&pilha, 10);
    push(&pilha, 20);
    push(&pilha, 30);

    printf("Tamanho após pushes: %d\n", size(&pilha));  // deve imprimir 3

    // Consultando o topo
    int v;
    if (top(&pilha, &v))
        printf("Topo atual: %d\n", v);                  // deve imprimir 30

    // Desempilhando valores
    while (!isEmpty(&pilha)) {
        pop(&pilha, &v);
        printf("Pop: %d  |  Tamanho agora: %d\n", v, size(&pilha));
    }

    // Tentando pop em pilha vazia
    pop(&pilha, &v);  // imprime "Erro: pilha vazia"

    return 0;
}
```

Importante destacar aqui que essa pilha foi implementada para números inteiros. Contudo, podemos utilizar o mesmo princípio para construir pilhas para outros tipos de dados.

## 5. Exercícios

### 5.1: Histórico de Navegação Web

**Contexto:** Um navegador mantém o histórico de páginas visitadas para permitir “Voltar” e “Avançar”.
**Tarefa:**

1. Modele o TAD `PilhaHistorico` onde cada elemento guarda `url` (texto) e `timestamp`.
2. Defina operações:

   * `push(pagina)`
   * `pop() -> pagina`
   * `top() -> pagina`
   * `isEmpty() -> booleano`
   * `size() -> inteiro`
3. Escreva pseudocódigo para implementar cada operação.
4. Simule: visita “A”, “B”, “C”; dá 2 cliques em “Voltar” (pop); mostra a página atual (top).

---

### 5.2: Validação de Parênteses em Expressões

**Contexto:** Um compilador verifica se todos os parênteses, chaves e colchetes estão corretamente balanceados.
**Tarefa:**

1. Crie TAD `PilhaChar`.
2. Escreva função `validar(expressao: texto) -> booleano` que:

   * Percorre cada caractere; ao abrir “( \{ \[” faz `push`; ao fechar “) \} \]” faz `pop` e compara tipo.
   * Em qualquer inconsistência, retorna `false`.
3. Demonstre com as expressões “(\[\]{})”, “(\[)\]” e “((())”.

---

### 5.3: Undo/Redo em Editor de Texto

**Contexto:** Um editor permite desfazer (`undo`) e refazer (`redo`) operações de digitação.
**Tarefa:**

1. Modele duas pilhas: `PilhaUndo` e `PilhaRedo`, cada elemento contendo o texto inserido/removido.
2. Defina operações:

   * `digitar(acao)` → `push` em `Undo`, limpa `Redo`
   * `undo()` → `pop` de `Undo` e `push` em `Redo`
   * `redo()` → `pop` de `Redo` e `push` em `Undo`
3. Escreva pseudocódigo para estas funções.
4. Simule: digita “A”, “B”; undo; digita “C”; redo (não deve refazer); undo.

---

### 5.4: Avaliação de Expressões Pós-fixadas (RPN)

**Contexto:** Calculadoras RPN (Reverse Polish Notation) usam pilha para avaliar expressões.
**Tarefa:**

1. Modele `PilhaNum` de `double`.
2. Escreva função `avaliarRPN(tokens: lista<string>) -> número` que:

   * Ao ler número faz `push`, ao ler operador ( + - \* / ) faz `pop` duas vezes, aplica e `push` resultado.
3. Dê pseudocódigo e avalie as expressões `["2","3","+","4","*"]` e `["5","1","2","+","4","*","+","3","-"]`.

---

### 5.5: Pilha de Chamadas de Funções (Call Stack)

**Contexto:** Em tempo de execução, cada chamada de função é empilhada; ao retornar, desempilha-se.
**Tarefa:**

1. Modele `PilhaFrame` onde cada `Frame` contém `funcao` (texto) e `retorno` (endereço).
2. Defina `pushFrame`, `popFrame`, `topFrame`.
3. Escreva pseudocódigo que simule as chamadas: `main` → `A` → `B` → retorna → `C` → retorna → retorna.
4. Exiba a pilha após cada operação.

---

### 5.6: Conversão de Base Numérica

**Contexto:** Para converter um número decimal em binário, usa-se pilha para armazenar restos.
**Tarefa:**

1. Modele `PilhaInt`.
2. Escreva função `converterParaBase(n: inteiro, base: inteiro) -> string` que:

   * Enquanto `n > 0`, faz `push(n % base)` e `n /= base`.
   * Depois, pop todos os restos para formar a representação.
3. Demonstre convertendo `n=45` para base `2` e `16`.

---

### 5.7: Verificação de Rotas em Labirinto

**Contexto:** Um algoritmo de backtracking empilha posições visitadas para explorar caminhos e desempilha ao voltar.
**Tarefa:**

1. Modele `PilhaPosicao` com `x, y`.
2. Escreva pseudocódigo de DFS que:

   * Ao mover para próxima célula válida faz `push`;
   * Se chega em beco sem saída, faz `pop` até encontrar outra direção.
3. Descreva como a pilha cresce e encolhe para um labirinto 3×3 simples.

---

### 5.8: Implementação de Undo em Jogo de Desenho

**Contexto:** Num app de desenho, cada traço (linha) é um objeto empilhado para possibilitar “desfazer”.
**Tarefa:**

1. Modele `PilhaTraço` onde `Trazado` guarda coordenadas `(x1,y1)-(x2,y2)`.
2. Defina `adicionarTraco(traco)`, `undoTraco()`.
3. Pseudocódigo para desenhar 5 traços, desfazer 3, adicionar 2 e desfazer 1.

---

### 5.9: Avaliação de Notação Infix para Pós-fix

**Contexto:** Algoritmo Shunting-Yard converte expressão infix para postfix usando uma pilha de operadores.
**Tarefa:**

1. Modele `PilhaOp` de operadores `+ - * / ( )`.
2. Escreva pseudocódigo do Shunting-Yard (push em `(`, pop até `(` ao encontrar `)` etc.).
3. Converta “3 + 4 \* 2 / ( 1 - 5 )”.

---

### 5.10: Verificação de Palíndromo

**Contexto:** Para testar se uma string é palíndroma, empilha-se a primeira metade e compara com a segunda.
**Tarefa:**

1. Modele `PilhaChar`.
2. Escreva função `ehPalindromo(s: texto) -> booleano` que:

   * Empilha `s[0..mid-1]`;
   * Se `len` ímpar, ignora `mid`;
   * Percorre `mid..end`, pop e compara.
3. Demonstre com “radar”, “level”, “hello”.


