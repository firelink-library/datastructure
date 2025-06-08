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

> "Calma lá Murilão! Consegui compreender o que você disse sobre onde as listas, ou melhor, o comportamento de lista é utilizado. Mas como vamos trazer isso para software?"

Ótima pergunta! Vamos ver primeiro quais são as operações que podemos fazer com as listas:

- Adicionar elemento ao final (append)
- Inserir elemento em uma posição específica
- Remover elemento de uma posição específica
- Acessar elemento por índice
- Percorrer todos os elementos (iterar)
- Verificar o tamanho da lista
- Verificar se a lista está vazia

Show, aqui temos algumas delas. Vamos pensar em algumas maneiras que podemos realizar essa implementação.

:::tip[A lista é só um comportamento]

Importante pessoal, vamos falar de algumas operações com listas, mas elas são apenas um comportamento, um "container" que utilizamos sobre algum outro tipo de dado que desejamos que tenha este comportamento. Essa percepção não é simples! Tentem focar energia nessa descrição.

:::

## 3. Comportamentos de Fila

Pessoal, vamos pensar agora em como podemos realizar a implementação destes algoritmos. Vamos considerar que a fila será implementada para guardar os dados da nossa pessoa (nome e idade). É uma representação super simples, mas vai servir para fazermos a nossa lista de pessoas.

```bash
TAD Pessoa
  ATRIBUTOS:
    nome: texto
    idade: inteiro

  MÉTODOS:
    criar(nome, idade) -> Pessoa
      nova_pessoa.nome ← nome
      nova_pessoa.idade ← idade
      RETORNAR nova_pessoa

    get_nome() -> texto
      RETORNAR nome

    get_idade() -> inteiro
      RETORNAR idade

    set_nome(novo_nome: texto)
      nome ← novo_nome

    set_idade(nova_idade: inteiro)
      idade ← nova_idade
```

Legal, temos como lidar com nossas pessoas. Mas ainda não temos como lidar com nossa lista de pessoas. Quando vamos pensar na representação da nossa lista, temos os seguintes comportamentos que devem ser implementados:

```bash
TAD Lista
  OPERACOES FUNDAMENTAIS:
    inserir(posicao, elemento)
    inserirNoFim(elemento)
    remover(posicao)
    buscar(posicao) -> elemento
    buscar(elemento) -> inteiro
    tamanho() -> inteiro
    estáVazia() -> booleano

```

Esses comportamentos trazem  nossa abstração de lista para o que desejarmos. Podemos pensar, para o nosso exemplo de pessoas, que teremos as seguintes representações:

```bash
TAD ListaPessoas
  OPERACOES FUNDAMENTAIS:
    inserir(posicao, Pessoa)
    inserirNoFim(Pessoa)
    remover(posicao)
    buscar(posicao) -> Pessoa
    buscar(Pessoa) -> inteiro
    tamanho() -> inteiro
    estáVazia() -> booleano
```

Legal, agora que temos nossa interface de como vamos utilizar esses elementos basta utilizarmos eles!

> "Calma lá Murilão! Você se emocionou denovo! Como vamos utilizar esses caras de nem vimos nada de implementação?"

Ok, ok, vocês tem razão aqui, vamos pensar em como podemos implementar esses comportamentos das Listas.

## 4. Implementando os comportamentos da Lista

Legal, falamos de forma genérica do que a lista pode fazer, mas como vamos implementar isso? Podemos pensar em duas abordagens diferentes, quero discutir elas com vocês agora. Podemos pensar em implementar as listas, utilizando vetores ou de forma encadeada. Vamos ver as vantagens e desvantagens de cada uma delas.

### 4.1 Utilizando Vetores

Quando pensamos em utilizar vetores, estamos falando de elementos contíguos na memória do nosso dispositivo. Todos do mesmo tipo e alocados previamente. Esse vetor ou array é utilizado para armazenar os elementos. É necessário manter um contador do número de elementos inseridos. Quanto a seu tamanho, pode ser dimensionada previamente ou expandida com cópia (como listas em Python, por exemplo).

✅ Vantagens:
- Acesso direto por índice (lista[i]) é rápido (tempo constante).
- Boa performance quando o tamanho máximo é conhecido ou cresce lentamente.

❌ Desvantagens:
- Inserções e remoções exigem deslocamento dos elementos.
- O tamanho do array pode ser desperdiçado ou insuficiente.
- Crescimento exige realocação (cópia para vetor maior).

Podemos pensar em sua implementação da seguinte maneira:

```bash
TAD ListaPessoas
  CONSTANTES:
    MAX ← 1000  // capacidade máxima do vetor

  ATRIBUTOS:
    dados: vetor[0..MAX-1] de Pessoa
    n: inteiro  // número de elementos inseridos

  MÉTODOS:

    criar() -> ListaPessoas
      nova_lista.dados ← vetor vazio de tamanho MAX
      nova_lista.n ← 0
      RETORNAR nova_lista

    inserir(posicao: inteiro, p: Pessoa)
      SE n = MAX
        ESCREVER "Erro: lista cheia"
        RETORNAR
      SE posicao < 0 OU posicao > n
        ESCREVER "Erro: posição inválida"
        RETORNAR
      PARA i ← n ATÉ posicao+1 PASSO -1
        dados[i] ← dados[i-1]  // desloca elementos para a direita
      dados[posicao] ← p
      n ← n + 1

    inserirNoFim(p: Pessoa)
      inserir(n, p)

    remover(posicao: inteiro)
      SE estáVazia() OU posicao < 0 OU posicao ≥ n
        ESCREVER "Erro: posição inválida"
        RETORNAR
      PARA i ← posicao ATÉ n-2
        dados[i] ← dados[i+1]  // desloca elementos para a esquerda
      n ← n - 1

    buscar(posicao: inteiro) -> Pessoa
      SE posicao < 0 OU posicao ≥ n
        ESCREVER "Erro: posição inválida"
        RETORNAR nulo
      RETORNAR dados[posicao]

    buscar(p: Pessoa) -> inteiro
      PARA i ← 0 ATÉ n-1
        SE dados[i].nome = p.nome E dados[i].idade = p.idade
          RETORNAR i
      RETORNAR -1  // não encontrado

    tamanho() -> inteiro
      RETORNAR n

    estáVazia() -> booleano
      RETORNAR (n = 0)
```

Aqui, por mais direta que possa ser essa representação, devemos ter em mente alguns pontos importantes:
- O tamanho máximo de elementos deve ser utilizado com parcimônia. Muitos elementos, significam muita memória que está alocada e não necessariamente será utilizada. Muito poucos, significa que vamos ter que realocar ou manipular esses elementos durante a sua utilização.
- O controle de inserção e número atual e total de elementos passa pelo nosso controle. 
- Quando desejamos inserir um elemento no vetor, temos que deslocar os elementos dentro do vetor.

> "Caramba Murilão, deu para ver que da um trabalho mas deu para compreender. Tem alguma outra forma de fazer essa manipulação?"

Que bom que você perguntou! Tem sim! Utilizando uma lista encadeada

### 4.2 Lista Encadeada

Vamos compreender que aqui temos uma implementação de um formato diferente do que utilizamos até então. Com a alocação com vetores, separamos todas as posições de memória antes de utilizarmos elas. Com a lista encadeada, vamos iniciar nossa lista e não vamos alocar espaços de memória para ela, até que seja necessário realizar essa operação. Desta forma, vamos utilizar apenas a quantidade de memória que for necessária com nossa lista e poderemos adicionar quantos elementos desejarmos (e tivermos memória).

Podemos ver cada elemento da lista encadeada como um nó. O primeiro nó da lista tem um nome especial, o `Cabeça`. Ele sempre conhece o início da lista. Cada elemento (nó) aponta para o próximo. A alocação dinâmica, permite que ela cresça conforme a necessidade. Ela pode ser simplesmente encadeada, duplamente encadeada ou circular.

✅ Vantagens:
- Inserções e remoções em posições intermediárias são eficientes (sem deslocamento).
- Crescimento e redução de tamanho são flexíveis.

❌ Desvantagens:
- Acesso sequencial: buscar lista[i] exige percorrer os nós até a posição.
- Mais uso de memória por causa dos ponteiros.
- Pode ter impacto em cache e desempenho geral.

A sua implementação pode seguir da seguinte maneira:

```bash
TAD No
  ATRIBUTOS:
    pessoa: Pessoa
    proximo: No

TAD ListaPessoas
  ATRIBUTOS:
    inicio: No
    n: inteiro  // tamanho da lista

  MÉTODOS:

    criar() -> ListaPessoas
      nova_lista.inicio ← nulo
      nova_lista.n ← 0
      RETORNAR nova_lista

    inserir(posicao: inteiro, p: Pessoa)
      SE posicao < 0 OU posicao > n
        ESCREVER "Erro: posição inválida"
        RETORNAR

      novo ← alocar No
      novo.pessoa ← p

      SE posicao = 0
        novo.proximo ← inicio
        inicio ← novo
      SENÃO
        atual ← inicio
        PARA i ← 0 ATÉ posicao - 2
          atual ← atual.proximo
        novo.proximo ← atual.proximo
        atual.proximo ← novo

      n ← n + 1

    inserirNoFim(p: Pessoa)
      inserir(n, p)

    remover(posicao: inteiro)
      SE posicao < 0 OU posicao ≥ n
        ESCREVER "Erro: posição inválida"
        RETORNAR

      SE posicao = 0
        temp ← inicio
        inicio ← inicio.proximo
      SENÃO
        anterior ← inicio
        PARA i ← 0 ATÉ posicao - 2
          anterior ← anterior.proximo
        temp ← anterior.proximo
        anterior.proximo ← temp.proximo

      liberar temp
      n ← n - 1

    buscar(posicao: inteiro) -> Pessoa
      SE posicao < 0 OU posicao ≥ n
        ESCREVER "Erro: posição inválida"
        RETORNAR nulo

      atual ← inicio
      PARA i ← 0 ATÉ posicao - 1
        atual ← atual.proximo

      RETORNAR atual.pessoa

    buscar(p: Pessoa) -> inteiro
      atual ← inicio
      i ← 0
      ENQUANTO atual ≠ nulo
        SE atual.pessoa.nome = p.nome E atual.pessoa.idade = p.idade
          RETORNAR i
        atual ← atual.proximo
        i ← i + 1
      RETORNAR -1

    tamanho() -> inteiro
      RETORNAR n

    estáVazia() -> booleano
      RETORNAR (n = 0)
```

> "Calma lá Murilão, aqui foi golpe baixo! Que monte de setinha é essa que apareceu ai?"

Vamos juntos! Essa implementação é mais complicada mesmo! Mas vamos conseguir! 頑張って!

:::tip[頑張って - Ganbatte]

<iframe width="560" height="315" src="https://www.youtube.com/embed/crbikU7kvLs?si=bg4Df40EkjblDv8r" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen style={{ display: 'block', marginLeft: 'auto', maxHeight: '40vh', marginRight: 'auto', marginBottom: '24px' }}></iframe>
<br />

https://youtube.com/shorts/hGDs76IhWzk?si=Am9U9W7Eb2hsczMK

:::

Primeiro, estamos utilizando um elemento que representa os nós da nossa lista. Ele guarda duas informações: uma pessoa (a abstração dos dados que desejamos utilizar) e o endereço de outro elemento Nó. Assim, conseguimos ligar esse elemento ao próximo elemento nós.

Depois, quando criamos uma lista, temos apenas duas informações: quem é o primeiro nós (cabeça) e o tamanho atual da nossa lista. Para sua criação, o que fazemos é indicar que a cabeça não tem nenhum endereço associado a ela.

Quando queremos inserir uma nova pessoa na lista em uma posição específica, seguimos dois caminhos:
- Se essa posição for o início da lista (posição 0), criamos um novo nó, colocamos os dados da pessoa dentro dele, e dizemos que esse novo nó agora aponta para o antigo primeiro nó da lista. Assim, ele se torna a nova cabeça da lista.
- Para outras posições, percorremos a lista até chegar no nó imediatamente anterior à posição desejada. A partir dele, criamos o novo nó com os dados da nova pessoa, e fazemos esse novo nó apontar para o próximo nó da sequência. Em seguida, atualizamos o ponteiro do nó anterior para apontar para esse novo nó.

Com isso, a nova pessoa é inserida entre dois nós já existentes, sem que seja necessário mover ou copiar dados.

Inserir no fim da lista é apenas um caso particular da operação anterior: a nova pessoa será colocada na posição igual ao tamanho atual da lista. Assim, podemos usar a mesma lógica de inserção, apenas ajustando a posição para o final.

Para remover uma pessoa da lista, precisamos localizar o nó que está na posição desejada e tomar cuidado para não perder a ligação entre os nós. Se a remoção for do primeiro elemento, simplesmente fazemos com que a cabeça da lista passe a apontar para o segundo nó (ou nulo, se não houver mais elementos). Assim, o primeiro nó é descartado da cadeia. Para outras posições, percorremos a lista até o nó anterior à posição desejada. Depois, fazemos com que esse nó anterior pule o nó que queremos remover, apontando diretamente para o próximo da sequência. O nó intermediário é, então, desconectado e poderá ser descartado. Essa operação não exige deslocamento de dados, apenas mudança de referências (ponteiros).

Para buscar uma pessoa com base na posição, percorremos a lista a partir da cabeça, contando passo a passo até chegar à posição desejada. Quando alcançamos essa posição, retornamos os dados armazenados naquele nó. Como a lista encadeada não possui acesso direto como um vetor, precisamos andar sequencialmente até encontrar o que procuramos.

Para buscar uma pessoa na lista, percorremos ela desde o início, comparando cada elemento com a pessoa procurada. A cada passo, verificamos se os dados da pessoa atual correspondem aos buscados (por exemplo, nome e idade). Se encontrarmos, retornamos a posição. Se chegarmos ao final da lista sem sucesso, indicamos que a pessoa não está presente. Essa busca também é sequencial, e pode ser custosa para listas muito grandes, reforçando o valor de saber escolher a estrutura para cada cenário.

Ufa! Agora podemos ver um exemplo de como fazer essas implementações em uma linguagem de programação.

## 5. Implementação em C

### 5.1 Versão com Vetor

Nossa arquivo para lidar com a lista implementada em C:

```c
#include <stdio.h>
#include <string.h>
#include <stdbool.h>

#define MAX 1000

// Definindo o tipo Pessoa
typedef struct {
    char nome[100];
    int idade;
} Pessoa;

// Definindo o tipo ListaPessoas
typedef struct {
    Pessoa dados[MAX];
    int n; // quantidade atual de elementos
} ListaPessoas;

// Cria uma nova lista
void criarLista(ListaPessoas *lista) {
    lista->n = 0;
}

// Verifica se a lista está vazia
bool estaVazia(ListaPessoas *lista) {
    return lista->n == 0;
}

// Retorna o tamanho da lista
int tamanho(ListaPessoas *lista) {
    return lista->n;
}

// Insere uma pessoa em uma posição específica
bool inserir(ListaPessoas *lista, int pos, Pessoa p) {
    if (lista->n == MAX || pos < 0 || pos > lista->n) {
        return false;
    }

    for (int i = lista->n; i > pos; i--) {
        lista->dados[i] = lista->dados[i - 1];
    }

    lista->dados[pos] = p;
    lista->n++;
    return true;
}

// Insere uma pessoa no fim da lista
bool inserirNoFim(ListaPessoas *lista, Pessoa p) {
    return inserir(lista, lista->n, p);
}

// Remove uma pessoa da lista na posição especificada
bool remover(ListaPessoas *lista, int pos) {
    if (estaVazia(lista) || pos < 0 || pos >= lista->n) {
        return false;
    }

    for (int i = pos; i < lista->n - 1; i++) {
        lista->dados[i] = lista->dados[i + 1];
    }

    lista->n--;
    return true;
}

// Busca uma pessoa na posição especificada
Pessoa* buscarPorPosicao(ListaPessoas *lista, int pos) {
    if (pos < 0 || pos >= lista->n) {
        return NULL;
    }

    return &lista->dados[pos];
}

// Busca a posição de uma pessoa com nome e idade iguais
int buscarPessoa(ListaPessoas *lista, Pessoa p) {
    for (int i = 0; i < lista->n; i++) {
        if (strcmp(lista->dados[i].nome, p.nome) == 0 && lista->dados[i].idade == p.idade) {
            return i;
        }
    }
    return -1;
}

// Imprime os dados da lista (para fins de teste)
void imprimirLista(ListaPessoas *lista) {
    printf("Lista de Pessoas (%d elementos):\n", lista->n);
    for (int i = 0; i < lista->n; i++) {
        printf("  [%d] Nome: %s, Idade: %d\n", i, lista->dados[i].nome, lista->dados[i].idade);
    }
}

```

Como podemos utilizar ela no programa principal:

```c
int main() {
    ListaPessoas lista;
    criarLista(&lista);

    Pessoa p1 = {"Alice", 30};
    Pessoa p2 = {"Bruno", 25};
    Pessoa p3 = {"Carla", 28};

    inserirNoFim(&lista, p1);
    inserirNoFim(&lista, p2);
    inserir(&lista, 1, p3); // insere Carla entre Alice e Bruno

    imprimirLista(&lista);

    remover(&lista, 0); // remove Alice

    imprimirLista(&lista);

    return 0;
}

```

### 5.2 Versão com Alocação Dinâmica

Nossa implementação com alocação dinâmica:

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <stdbool.h>

// Tipo Pessoa
typedef struct {
    char nome[100];
    int idade;
} Pessoa;

// Nó da lista
typedef struct No {
    Pessoa pessoa;
    struct No* proximo;
} No;

// Lista de Pessoas
typedef struct {
    No* inicio;
    int n; // tamanho atual
} ListaPessoas;

// Cria uma nova lista
void criarLista(ListaPessoas* lista) {
    lista->inicio = NULL;
    lista->n = 0;
}

// Verifica se a lista está vazia
bool estaVazia(ListaPessoas* lista) {
    return lista->inicio == NULL;
}

// Retorna o tamanho da lista
int tamanho(ListaPessoas* lista) {
    return lista->n;
}

// Insere uma pessoa na posição indicada
bool inserir(ListaPessoas* lista, int pos, Pessoa p) {
    if (pos < 0 || pos > lista->n) return false;

    No* novo = (No*)malloc(sizeof(No));
    if (!novo) return false;

    novo->pessoa = p;
    novo->proximo = NULL;

    if (pos == 0) {
        novo->proximo = lista->inicio;
        lista->inicio = novo;
    } else {
        No* atual = lista->inicio;
        for (int i = 0; i < pos - 1; i++) {
            atual = atual->proximo;
        }
        novo->proximo = atual->proximo;
        atual->proximo = novo;
    }

    lista->n++;
    return true;
}

// Insere no fim
bool inserirNoFim(ListaPessoas* lista, Pessoa p) {
    return inserir(lista, lista->n, p);
}

// Remove pessoa da posição indicada
bool remover(ListaPessoas* lista, int pos) {
    if (pos < 0 || pos >= lista->n || estaVazia(lista)) return false;

    No* temp;
    if (pos == 0) {
        temp = lista->inicio;
        lista->inicio = lista->inicio->proximo;
    } else {
        No* anterior = lista->inicio;
        for (int i = 0; i < pos - 1; i++) {
            anterior = anterior->proximo;
        }
        temp = anterior->proximo;
        anterior->proximo = temp->proximo;
    }

    free(temp);
    lista->n--;
    return true;
}

// Busca pessoa por posição
Pessoa* buscarPorPosicao(ListaPessoas* lista, int pos) {
    if (pos < 0 || pos >= lista->n) return NULL;

    No* atual = lista->inicio;
    for (int i = 0; i < pos; i++) {
        atual = atual->proximo;
    }

    return &atual->pessoa;
}

// Busca posição de uma pessoa
int buscarPessoa(ListaPessoas* lista, Pessoa p) {
    No* atual = lista->inicio;
    int i = 0;
    while (atual != NULL) {
        if (strcmp(atual->pessoa.nome, p.nome) == 0 && atual->pessoa.idade == p.idade) {
            return i;
        }
        atual = atual->proximo;
        i++;
    }
    return -1;
}

// Imprime lista
void imprimirLista(ListaPessoas* lista) {
    No* atual = lista->inicio;
    int i = 0;
    printf("Lista de Pessoas (%d elementos):\n", lista->n);
    while (atual != NULL) {
        printf("  [%d] Nome: %s, Idade: %d\n", i, atual->pessoa.nome, atual->pessoa.idade);
        atual = atual->proximo;
        i++;
    }
}
```

E sua utilização no programa principal:

```c
int main() {
    ListaPessoas lista;
    criarLista(&lista);

    Pessoa p1 = {"Alice", 30};
    Pessoa p2 = {"Bruno", 25};
    Pessoa p3 = {"Carla", 28};

    inserirNoFim(&lista, p1);
    inserirNoFim(&lista, p2);
    inserir(&lista, 1, p3); // insere Carla entre Alice e Bruno

    imprimirLista(&lista);

    remover(&lista, 0); // remove Alice

    imprimirLista(&lista);

    return 0;
}
```

> "Calma lá Murilão! Eita! Os dois programas principais estão iguais?"

Isso mesmo! Se conseguimos chegar nesse ponto, nossas abstrações estão ficando melhores! Lembrem, utilizar as listas são uma forma de fazermos uma abstração de um comportamento e implementá-lo. Quanto mais longe da implementação estiver o nosso código de utilização, mas essa abstração está conseguindo separar os elementos.

## 6. Lista Duplamente Ligada

Uma lista duplamente ligada (ou duplamente encadeada) é uma estrutura de dados linear composta por nós em que cada nó mantém dois ponteiros:
- Um que aponta para o nó anterior
- Um que aponta para o nó seguinte

Dessa forma, é possível navegar tanto para frente quanto para trás na lista. Elas podem ser utilizadas em:
- Navegadores Web: a lista de páginas visitadas pode ser percorrida para frente e para trás.
- Desfazer/Refazer em editores de texto.
- Gerenciadores de tarefas que mantêm elementos acessíveis em ordem mas com possibilidade de mover para trás.
- Implementação de deques (fila com inserção/remoção nas duas extremidades).

✅ Vantagens:
- Permite navegação em ambas as direções, facilitando certas operações (como retrocesso).
- A remoção de um nó intermediário é mais eficiente: você já conhece o nó anterior sem precisar percorrer toda a lista.
- Em algumas implementações, pode-se manter ponteiros para o início e fim da lista, tornando operações nas duas extremidades mais eficientes.

❌ Desvantagens:
- Maior uso de memória (dois ponteiros por nó).
- Manipulação de ponteiros mais complexa (especialmente para inserções e remoções).

```bash
TAD NoDuplo
  ATRIBUTOS:
    pessoa: Pessoa
    anterior: NoDuplo
    proximo: NoDuplo

TAD ListaDuplamenteLigada
  ATRIBUTOS:
    inicio: NoDuplo
    fim: NoDuplo
    n: inteiro

  MÉTODOS:

    criar() -> ListaDuplamenteLigada
      inicio ← nulo
      fim ← nulo
      n ← 0

    inserirNoFim(pessoa: Pessoa)
      novo ← alocar NoDuplo
      novo.pessoa ← pessoa
      novo.anterior ← fim
      novo.proximo ← nulo

      SE fim ≠ nulo
        fim.proximo ← novo
      SENÃO
        inicio ← novo

      fim ← novo
      n ← n + 1

    inserirNoInicio(pessoa: Pessoa)
      novo ← alocar NoDuplo
      novo.pessoa ← pessoa
      novo.anterior ← nulo
      novo.proximo ← inicio

      SE inicio ≠ nulo
        inicio.anterior ← novo
      SENÃO
        fim ← novo

      inicio ← novo
      n ← n + 1

    remover(NoDuplo alvo)
      SE alvo = nulo
        RETORNAR

      SE alvo.anterior ≠ nulo
        alvo.anterior.proximo ← alvo.proximo
      SENÃO
        inicio ← alvo.proximo

      SE alvo.proximo ≠ nulo
        alvo.proximo.anterior ← alvo.anterior
      SENÃO
        fim ← alvo.anterior

      liberar alvo
      n ← n - 1

    percorrerDoInicio()
      atual ← inicio
      ENQUANTO atual ≠ nulo
        ESCREVER atual.pessoa
        atual ← atual.proximo

    percorrerDoFim()
      atual ← fim
      ENQUANTO atual ≠ nulo
        ESCREVER atual.pessoa
        atual ← atual.anterior
```

## 7. Lista Circular

Uma lista circular é uma variação das listas encadeadas (simples ou duplamente ligadas) em que:
- O último nó da lista aponta de volta para o primeiro nó, formando um "ciclo".
- Isso vale tanto para listas simplesmente circulares quanto para duplamente circulares.
- Em vez de terminar em nulo, o ponteiro do último nó fecha o ciclo com o início da lista.

✅ Vantagens:
- Permite percurso contínuo da lista (sem fim), ideal para ciclos.
- Torna mais fácil implementar estruturas como:
- Filas circulares (uso eficiente de espaço em buffers fixos).
- Agendas com repetição (ex: dias da semana, turnos).
- Sistemas com alocação por rodízio (ex: round-robin em SO).

❌ Desvantagens:
- Exige cuidado extra para não entrar em loop infinito.
- Pode ser mais difícil de depurar se os alunos não visualizarem bem o ciclo.


```bash
TAD No
  ATRIBUTOS:
    pessoa: Pessoa
    proximo: No

TAD ListaCircularSimples
  ATRIBUTOS:
    fim: No  // referência ao último nó (que aponta para o primeiro)
    n: inteiro

  MÉTODOS:

    criar() -> ListaCircularSimples
      fim ← nulo
      n ← 0

    inserirInicio(pessoa: Pessoa)
      novo ← alocar No
      novo.pessoa ← pessoa

      SE fim = nulo
        novo.proximo ← novo
        fim ← novo
      SENÃO
        novo.proximo ← fim.proximo
        fim.proximo ← novo

      n ← n + 1

    inserirFim(pessoa: Pessoa)
      inserirInicio(pessoa)
      fim ← fim.proximo  // novo último é o que foi inserido agora

    removerInicio()
      SE fim = nulo
        RETORNAR

      inicio ← fim.proximo

      SE fim = inicio  // lista com um único elemento
        liberar inicio
        fim ← nulo
      SENÃO
        fim.proximo ← inicio.proximo
        liberar inicio

      n ← n - 1

    percorrer()
      SE fim = nulo
        RETORNAR

      atual ← fim.proximo  // começa no primeiro
      FAÇA
        ESCREVER atual.pessoa
        atual ← atual.proximo
      ENQUANTO atual ≠ fim.proximo

```

## 8. Quadro Resumo de Comparação

| Critério                          | **Lista com Vetor**                           | **Lista com Alocação Dinâmica**               |
| --------------------------------- | --------------------------------------------- | --------------------------------------------- |
| **Estrutura de armazenamento**    | Vetor fixo (tamanho máximo definido)          | Nós alocados dinamicamente com ponteiros      |
| **Crescimento**                   | Limitado ao tamanho do vetor                  | Ilimitado (limitado apenas pela memória RAM)  |
| **Acesso por posição (índice)**   | Direto e rápido (tempo constante `O(1)`)      | Sequencial (tempo linear `O(n)`)              |
| **Inserção/rem. no início/meio**  | Requer deslocamento dos elementos (`O(n)`)    | Ajuste de ponteiros (`O(1)` se nó conhecido)  |
| **Inserção no fim**               | Rápida se houver espaço (`O(1)`)              | Rápida se houver ponteiro para o fim (`O(1)`) |
| **Uso de memória**                | Espaço fixo reservado, pode haver desperdício | Memória alocada sob demanda, mais eficiente   |
| **Desempenho em cache**           | Melhor desempenho (dados contíguos)           | Pior desempenho (endereços dispersos)         |
| **Complexidade de implementação** | Mais simples                                  | Mais complexa (manipulação de ponteiros)      |
| **Flexibilidade**                 | Baixa (tamanho fixo ou realocação manual)     | Alta (cresce e diminui dinamicamente)         |
| **Aplicações típicas**            | Listas com tamanho previsível, acesso rápido  | Listas de tamanho variável, muitas inserções  |

---

| Critério                          | **Lista Simplesmente Ligada**          | **Lista Duplamente Ligada**               | **Lista Circular (Simples ou Dupla)**                  |
| --------------------------------- | -------------------------------------- | ----------------------------------------- | ------------------------------------------------------ |
| **Ponteiros por nó**              | 1 (para o próximo)                     | 2 (para o anterior e o próximo)           | 1 ou 2 (dependendo da versão: simples ou dupla)        |
| **Navegação**                     | Apenas para frente                     | Para frente e para trás                   | Pode ser contínua em um ciclo                          |
| **Inserção no início**            | Rápida (`O(1)`)                        | Rápida (`O(1)`)                           | Rápida (`O(1)`)                                        |
| **Inserção no meio/fim**          | Exige percorrer até a posição (`O(n)`) | Igual, mas remoção é mais fácil           | Idem, mas acesso ao fim pode ser direto (em circular)  |
| **Remoção de um nó conhecido**    | Exige ponteiro anterior                | Rápida (`O(1)`)                           | Depende da versão; cuidado com ponteiros circulares    |
| **Acesso à cauda (último nó)**    | Exige percorrer a lista                | Pode ser direto se armazenado             | Pode ser direto (especialmente em circular com `fim`)  |
| **Detecção de fim da lista**      | Quando `nó->proximo == NULL`           | Quando `nó->proximo == NULL`              | Quando `nó == início` novamente (estrutura é um ciclo) |
| **Uso de memória**                | Mais econômico                         | Usa mais memória (2 ponteiros por nó)     | Idem ao tipo base (simples ou dupla)                   |
| **Complexidade de implementação** | Simples                                | Moderada                                  | Maior (cuidados com ciclos e laços infinitos)          |
| **Aplicações típicas**            | Pilhas, filas simples, listas básicas  | Editores de texto, navegação em histórico | Agendas cíclicas, buffers circulares, round-robin      |
| **Cuidado extra necessário**      | Com ponteiro `NULL` ao final           | Com encadeamento duplo ao inserir/remover | Para evitar laços infinitos ao percorrer               |


:::tip[Notação O]

<iframe width="560" height="315" src="https://www.youtube.com/embed/g2o22C3CRfU?si=S0h6G0QChJ71N9g5" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen style={{ display: 'block', marginLeft: 'auto', maxHeight: '40vh', marginRight: 'auto', marginBottom: '24px' }}></iframe>
<br />

<iframe width="560" height="315" src="https://www.youtube.com/embed/XMUe3zFhM5c?si=g_D77IRs_9vkeP_i" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen style={{ display: 'block', marginLeft: 'auto', maxHeight: '40vh', marginRight: 'auto', marginBottom: '24px' }}></iframe>
<br />

:::

## 9. Lista de Exercícios

1. Implemente uma função inserir_na_posicao que insere uma Pessoa (nome e idade) em uma posição específica de uma lista implementada com vetor. A lista tem tamanho máximo 100. Caso a posição seja inválida ou a lista esteja cheia, a função deve emitir uma mensagem de erro.

2. Implemente uma função remover_por_nome que percorre uma lista encadeada de Pessoa e remove o primeiro nó com um nome igual ao informado. Lembre-se de atualizar corretamente os ponteiros e liberar a memória.

3. Implemente uma função buscar_por_nome que recebe um vetor de Pessoa e um nome, e retorna a posição da primeira ocorrência. Caso o nome não seja encontrado, retorne -1.

4. Crie uma função contar_maiores_idade que percorre uma lista encadeada e retorna a quantidade de pessoas com idade superior a um valor informado como parâmetro.

5. Um restaurante deseja um sistema simples para registrar reservas dos clientes. Cada reserva deve armazenar:
- Nome do cliente
- Número de pessoas
- Horário da reserva (ex: "19:30")

Implemente uma estrutura Reserva e uma lista de reservas com as seguintes funcionalidades:
- Inserir nova reserva no fim da lista.
- Remover uma reserva informando o nome do cliente.
- Exibir todas as reservas na ordem em que foram feitas.
- Buscar uma reserva por horário.

Permita ao usuário interagir por um pequeno menu no main().
