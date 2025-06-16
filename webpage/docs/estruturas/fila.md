---
title: Fila
sidebar_position: 3
slug: /filas
---

## 1. O que são filas

Seguindo com o conceito de tipos abstratos de dados, vamos verificar o que são filas e como elas podem ser utilizadas.

> "Calma lá Murilão, eu sei o que são filas na vida real! Aqui é a mesma coisa?"

Boa analogia! As filas aqui incorporam o mesmo comportamento das filas da vida real. Na verdade, esse é o nosso objetivo quando estamos implementando esse tipo de dado. Nós utilizamos o TAD de Fila, quando desejamos implementar o comportamento do tipo **FIFO**.

O **FIFO** significa `First In - First Out`, onde o primeiro elemento que for adicionado na fila será o primeiro elemento que será removido dela. Esse é o comportamento essencial da fila, qualquer implementação com essa estrutura, tem por objetivo trazer esse comportamento para o sistema.

> "Mas Murilo, onde isso é útil? Eu consigo ver isso na vida real, mas em código por que? Um vetor não faz isso e bora?"

Boa pergunta! Vamos pensar no porque utilizamos essas estruturas. Lembrem que a utilização dos TAD, traz um conjunto de interfaces que serão implementadas pelo nosso elemento, para que possamos colocar energia no desenvolvimento da nossa solução. Na vida real, é possível ver filas em diversos locais, como em caixas, as músicas em um player de música ou ainda os episódios que serão vistos em uma plataforma de streaming.

Vamos ver os contratos que essa interface traz para nós!

## 2. Propriedades e Contratos das Filas

Quando estamos trabalhando com Filas, temos algumas propriedades que devemos garantir que esses TAD implementam:

- **Invariante FIFO:** O primeiro elemento adicionado em uma fila deve ser o primeiro elemento removido dela.
- **Comportamento consistente independentemente da implementação:** Não faz diferença se a fila foi implementada utilizando um vetor ou alocação dinâmica, ela deve ter os mesmos comportamentos.
- **Tratamento de underflow (dequeue em fila vazia):** deve ser realizado algum tipo de implementação que sinalize que uma fila vazia tentou ter algum elemento removido dela.

Alguns dos contratos esperados que a TAD implemente:

```sh
TAD Fila
  OPERACOES:
    - enqueue(elemento)
    - dequeue() -> elemento
    - peek() -> elemento
    - isEmpty() -> booleano
    - size() -> inteiro
```

Onde temos:
- **enqueue(elemento):** inserir ao final.
- **dequeue() -> elemento:** remover e retornar o elemento no início.
- **peek() -> elemento:** consultar o elemento no início sem remover.
- **isEmpty() -> booleano:** verificar se está vazia.
- **size() -> inteiro:** tamanho atual, a quantidade de elementos na fila.

Comparando a implementação de fila com um vetor e com alocação dinâmica, podemos destacar:
- **Usando Vetor (Array-Based Queue):**
  - Estrutura: array fixo ou redimensionável + ponteiros front e rear
  - Vantagens e desvantagens (acesso O(1), deslocamentos, realocação) 

- **Usando Lista Encadeada:**
  - Estrutura: nós com referência ao próximo + ponteiros de cabeça e cauda
  - Vantagens e desvantagens (inserções/removals O(1), maior uso de memória)

## 3. Estudando um problema para implementar com listas

Ok, vamos então estudar um problema e ver como poderíamos resolver ele utilizando uma lista.

Você foi contratado para desenvolver o módulo “Lista de Ingredientes” de um sistema de pedidos online de um restaurante que oferece pratos 100% customizáveis. Cada cliente monta seu prato escolhendo ingredientes da “base” (por exemplo, arroz, macarrão, salada) e depois inserindo adicionais (como queijos, molhos, verduras, proteínas) no fim. O sistema precisa manter, para cada pedido, uma lista ordenada de ingredientes que:

1. Permita ao cliente inserir um ingrediente no final.

2. Permita ao cliente remover o primeiro ingrediente que foi adicionado.

3. Ofereça a funcionalidade de buscar por nome de ingrediente, retornando sua posição atual (ou indicando “não encontrado”).

4. Informe o tamanho da lista (quantos ingredientes já foram adicionados).

5. Verifique se a lista está vazia (por exemplo, antes de confirmar o pedido sem extras).

### 3.1 Tarefas para solucionar o problema

Pessoal aqui vou construir com vocês uam solução para este problema. Existem outras soluções que também podem ser desenvolvidas. Vamos analisar essa em conjunto.

Descreva o TAD `ListaIngredientes`, listando seus atributos e operações com assinaturas semelhantes a:

```sh
TAD ListaIngredientes
  ATRIBUTOS:
    – dados: vetor ou encadeamento de Ingrediente
    – n: inteiro  // tamanho atual da lista

  OPERACOES:
    – inserir(posicao: inteiro, ing: Ingrediente)
    – inserirNoFim(ing: Ingrediente)
    – remover()
    – buscarPorNome(nome: texto) -> inteiro
    – tamanho() -> inteiro
    – estaVazia() -> booleano
```

Modele o tipo Ingrediente com, pelo menos, os campos nome (texto) e calorias (inteiro).

```sh
TAD Ingrediente
    ATRIBUTOS:
        - nome : texto
        - calorias: inteiro
```

Vamos pensar agora no pseudo-código para realizar essas implementações.

```sh
# Definição dos tipos

TAD Ingrediente
  ATRIBUTOS:
    nome: texto
    calorias: inteiro

  MÉTODOS:
    criar(nome: texto, calorias: inteiro) -> Ingrediente
      nova.nome ← nome
      nova.calorias ← calorias
      RETORNAR nova

TAD ListaIngredientes
  CONSTANTES:
    MAX ← 100  # capacidade máxima do vetor

  ATRIBUTOS:
    dados: vetor[0..MAX-1] de Ingrediente
    n: inteiro  # número atual de elementos

  MÉTODOS:

    criar() -> ListaIngredientes
      lista.dados ← vetor vazio de tamanho MAX
      lista.n ← 0
      RETORNAR lista

    inserir(posicao: inteiro, ing: Ingrediente)
      # validações
      SE lista.n = MAX
        ESCREVER "Erro: lista cheia"
        RETORNAR
      SE posicao < 0 OU posicao > lista.n
        ESCREVER "Erro: posição inválida"
        RETORNAR
      # desloca para a direita
      PARA i ← lista.n ATÉ posicao+1 PASSO -1
        lista.dados[i] ← lista.dados[i-1]
      lista.dados[posicao] ← ing
      lista.n ← lista.n + 1

    inserirNoFim(ing: Ingrediente)
      inserir(lista.n, ing)

    remover() -> Ingrediente
      SE lista.n = 0
        ESCREVER "Erro: lista vazia"
        RETORNAR nulo
      ing ← lista.dados[0]
      PARA i ← 0 ATÉ lista.n-2
        lista.dados[i] ← lista.dados[i+1]
      lista.n ← lista.n - 1
      RETORNAR ing

    buscarPorNome(nome: texto) -> inteiro
      PARA i ← 0 ATÉ lista.n-1
        SE lista.dados[i].nome = nome
          RETORNAR i
      RETORNAR -1  # não encontrado

    tamanho() -> inteiro
      RETORNAR lista.n

    estaVazia() -> booleano
      RETORNAR (lista.n = 0)


# Exemplo de uso (pseudocódigo)

função principal()
  lista ← criar()

  # cria ingredientes
  queijo  ← criar("Queijo", 200)
  bacon   ← criar("Bacon", 300)
  alface  ← criar("Alface", 10)

  # operações
  inserirNoFim(queijo)        # [Queijo]
  inserirNoFim(bacon)         # [Queijo, Bacon]
  inserirNoFim(alface)          # [Queijo, Alface, Bacon]
  remover()                  # remove “Queijo”: [Alface, Bacon]

  posicaoBacon ← buscarPorNome("Queijo")   # retorna -1 (não existe)
  tamLista      ← tamanho()               # retorna 2
  vazia         ← estaVazia()             # retorna FALSO

  ESCREVER "Posição do Queijo:", posicaoBacon
  ESCREVER "Tamanho da lista:", tamLista
  ESCREVER "Lista vazia?", vazia
```

Beleza! Vamos verificar essa proposta de solução e vamos ver como ela está realizando está implementação.

- Vamos analisar primeiro o programa principal. Vale perceber que a lista é criada antes de qualquer operação ser realizada com ela. Aqui são iniciados o vetor para armazenar os dados e o tamanho da lista é iniciado com zero.
- Os elementos do tipo `Ingrediente` são criados.
- Cada vez que a função `inserirNoFim()` é chamada, ela faz uma chamada para a função `inserir()`, mandando o tamanho atual da lista, assim o elemento é inserido no final dela. Na função, primeiro é verificado se a lista não está cheia. Depois, é verificada se a posição enviada não é invalida. Agora, um laço de repetição que vai do último elemento para a posição informada mais um, vai deslocando todos os elementos dentro da lista para a direita, pegando o elemento anterior ao atual pelo índice `i` e colocando ele na posição `i`. Por fim, o elemento é inserido na lista e seu tamanho atual é atualizado.
- Quando a função `remover()` é invocada, o primeiro elemento que foi inserido será removido. Se a lista não estiver vazia, os itens da lista são deslocados para esquerda e o item removido é retornado. 

Legal! Agora vamos ver um exemplo desse cara implementado com alguma linguagem de programação.

### 3.2 Implementação em C

Vamos verificar essa implementação:

```c
#include <stdio.h>
#include <string.h>
#include <stdbool.h>

#define MAX 100  // capacidade máxima da lista

// Tipo Ingrediente
typedef struct {
    char nome[50];
    int calorias;
} Ingrediente;

// Tipo ListaIngredientes
typedef struct {
    Ingrediente dados[MAX];
    int n;  // número atual de elementos
} ListaIngredientes;

// Cria uma lista vazia
void criarLista(ListaIngredientes *lista) {
    lista->n = 0;
}

// Verifica se a lista está vazia
bool estaVazia(ListaIngredientes *lista) {
    return (lista->n == 0);
}

// Retorna o tamanho da lista
int tamanho(ListaIngredientes *lista) {
    return lista->n;
}

// Insere ingrediente em posição específica
bool inserir(ListaIngredientes *lista, int pos, Ingrediente ing) {
    if (lista->n >= MAX) {
        printf("Erro: lista cheia\n");
        return false;
    }
    if (pos < 0 || pos > lista->n) {
        printf("Erro: posição inválida\n");
        return false;
    }
    // desloca elementos para a direita
    for (int i = lista->n; i > pos; --i) {
        lista->dados[i] = lista->dados[i - 1];
    }
    lista->dados[pos] = ing;
    lista->n++;
    return true;
}

// Insere ingrediente ao fim da lista
bool inserirNoFim(ListaIngredientes *lista, Ingrediente ing) {
    return inserir(lista, lista->n, ing);
}

// Remove ingrediente de posição específica
bool removerPorPosicao(ListaIngredientes *lista, int pos) {
    if (estaVazia(lista)) {
        printf("Erro: lista vazia\n");
        return false;
    }
    if (pos < 0 || pos >= lista->n) {
        printf("Erro: posição inválida\n");
        return false;
    }
    // desloca elementos para a esquerda
    for (int i = pos; i < lista->n - 1; ++i) {
        lista->dados[i] = lista->dados[i + 1];
    }
    lista->n--;
    return true;
}

// Remove o primeiro elemento (comportamento de fila) e retorna cópia
bool removerFila(ListaIngredientes *lista, Ingrediente *retirado) {
    if (estaVazia(lista)) {
        printf("Erro: lista vazia\n");
        return false;
    }
    *retirado = lista->dados[0];
    // desloca restante para a esquerda
    for (int i = 0; i < lista->n - 1; ++i) {
        lista->dados[i] = lista->dados[i + 1];
    }
    lista->n--;
    return true;
}

// Busca ingrediente por nome, retorna índice ou -1
int buscarPorNome(ListaIngredientes *lista, const char *nome) {
    for (int i = 0; i < lista->n; ++i) {
        if (strcmp(lista->dados[i].nome, nome) == 0) {
            return i;
        }
    }
    return -1;
}

// Imprime a lista (para debug)
void imprimirLista(ListaIngredientes *lista) {
    printf("Lista de ingredientes (%d itens):\n", lista->n);
    for (int i = 0; i < lista->n; ++i) {
        printf("  [%d] %s (%d cal)\n",
               i, lista->dados[i].nome, lista->dados[i].calorias);
    }
}

int main() {
    ListaIngredientes lista;
    criarLista(&lista);

    Ingrediente queijo = { "Queijo", 200 };
    Ingrediente bacon  = { "Bacon", 300 };
    Ingrediente alface = { "Alface", 10 };

    // Operações de fila
    inserirNoFim(&lista, queijo);
    inserirNoFim(&lista, bacon);
    inserirNoFim(&lista, alface);
    imprimirLista(&lista);

    // Remove o primeiro (estilo queue)
    Ingrediente primeiro;
    if (removerFila(&lista, &primeiro)) {
        printf("\nRemovido (fila): %s (%d cal)\n", primeiro.nome, primeiro.calorias);
    }
    imprimirLista(&lista);

    // Remove genérico por posição
    removerPorPosicao(&lista, 1);  // remove "Alface"
    printf("\nDepois de remover posição 1:\n");
    imprimirLista(&lista);

    // Buscas e status
    int posBacon = buscarPorNome(&lista, "Bacon");
    printf("\nPosição do Bacon: %d\n", posBacon);
    printf("Tamanho da lista: %d\n", tamanho(&lista));
    printf("Lista vazia? %s\n", estaVazia(&lista) ? "SIM" : "NÃO");

    return 0;
}
```

Analisando a solução:
- A biblioteca `stdbool` é utilizada para que as macros `true` e `false` possam ser utilizadas.
- São definidas as duas estruturas de dados que serão utilizadas, uma para Ingredientes e outra para a Lista que vai se comportar como fila.
- A função `criarLista` recebe por referencia o endereço da variável que irá armazenar a lista. Ele atualiza a quantidade de elementos para zero.
- A função `buscarPorNome()` utiliza a função `strcmp` para verificar o elemento Ingrediente com os que estão no vetor.

## 4. Exercícios

### 4.1 Supermercado

Em um banco, clientes chegam e enfileiram-se para ser atendidos pelo caixa. Modele o TAD FilaClientes onde cada elemento armazena nome_cliente e tipo_conta. Defina operações:

- enqueue(cliente) 
- dequeue() -> cliente
- peek() -> cliente
- isEmpty() -> booleano
- size() -> inteiro

Escolha uma linguagem de programação e faça as implementações. Simule: chega “Alice”, “Bruno”, “Carla”; atenda dois clientes; mostre quem está no início.

### 4.2 Fila de Impressão de Documentos

Um escritório possui uma impressora compartilhada; documentos são enviados e aguardam na fila para serem impressos. Crie o TAD FilaImpressao em que cada job contém id_documento e num_paginas. Implemente métodos para:

- enqueue(job)
- dequeue() -> job
- isEmpty()
- totalJobs() -> inteiro
- Função que, após cada impressão, remove o job e exibe “Imprimindo doc X de Y páginas”.

Demonstre inserindo três jobs e processando todos até a fila zerar.

### 4.3 Buffer de Rede (Pacotes)

Um roteador armazena pacotes de dados recebidos em uma fila antes de encaminhá-los. Modele FilaPacotes com campos origem, destino e tamanho_bytes. Adicione operação drop() que, ao detectar size > capacidade, simplesmente descarta (dequeue) o primeiro pacote sem retornar. Escreva pseudocódigo para enqueue, dequeue, drop e isEmpty.
Simule a chegada de 5 pacotes, com overflow no terceiro, aplicando drop().

### 4.4 Fila de Pedidos em Restaurante

Em um fast-food, os pedidos dos clientes entram em fila na cozinha. Defina Pedido com num_pedido, itens (lista de strings) e tempo_estimado. Modele FilaPedidos com enqueue, dequeue, peek e size.

Código que:

- Insere pedidos
- Quando o cozinheiro finaliza, faz dequeue() e registra “Pedido X pronto em T minutos”.

Demonstre três inserções e duas remoções.

### 4.5 Check-in em Aeroporto

Passageiros fazem check-in e aguardam na fila de embarque. Crie TAD FilaEmbarque onde cada nó tem nome, assento e classe (Econômica, Executiva). Implemente enqueue, dequeue, isEmpty e imprimirFila() (lista todos os passageiros).

Escreva código para essas funções.

Simule cinco passageiros, exiba fila, faça dois dequeue() e exiba novamente.

### 4.6 Escalonamento de Processos (CPU Ready Queue)

No sistema operacional, processos prontos para execução aguardam em uma fila. Modele Processo com pid e tempo_CPU. TAD ReadyQueue com enqueue, dequeue, peek e size. Código que roda num “loop”:

- Enquanto não isEmpty()
  - remove próximo processo, executa por quantum, e se ainda não terminou, faz enqueue de volta.

Simule três processos e um quantum de 5ms.

### 4.7 Fila de Chamadas de Suporte (Help-desk)

Chamados de suporte técnico entram em uma fila e são atendidos por ordem de chegada. Crie Chamado com ticket_id, descricao e usuario. Modele FilaSuporte com as operações básicas. Adicione método cancelar(ticket_id) que remove o chamado da fila (remoção genérica por índice). Pseudocódigo para cancelar, usando buscarPorId + removerPorPosicao.

Simule inserções, um cancelamento e exiba o estado final.

### 4.8 Fila Circular de Sensoriamento

Um sistema embarcado lê valores de sensor e os armazena num buffer circular de tamanho fixo antes de processar. Modele FilaCircularSensor com array de double e índices head, tail. Implemente enqueue, dequeue, isFull, isEmpty. Pseudocódigo do wrap-around dos índices ((i+1) mod capacidade).

Demonstre inserindo até encher, removendo dois, e inserindo mais dois.

### 4.9 Fila de Impressora em Ambiente Multiusuário

Em laboratório de informática, vários usuários mandam jobs para impressoras diferentes; cada impressora mantém sua própria fila. Modele Job com usuario, arquivo e pagina_inicio–pagina_fim. Crie FilaImpressora com enqueue, dequeue. Adicione priorizar(usuario) que remonta a fila, trazendo jobs desse usuário ao início (mantendo ordem relativa entre eles).

Pseudocódigo para priorizar:
   -  Percorre fila, extrai jobs do usuário, os salva em lista auxiliar, depois reconstrói fila com esses jobs na frente.