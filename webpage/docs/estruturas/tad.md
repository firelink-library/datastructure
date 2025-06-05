---
title: Tipo Abstrato de Dados
sidebar_position: 1
slug: /tad
---

Aqui pessoal vamos estudar uma forma de abstrair as informações. Vamos criar uma abstração que permite armazenar os dados e realizar sua manipulação. Vamos trabalhar com uma descrição genérica e com sua implementação em algumas linguagens de programação.

## 1. Tipo Abstrato de Dado

Pessoal, para iniciarmos a construção do conceito de tipo abstrato de dado, vamos fazer uma avaliação primeiro sobre o que é abstração. Por definição **abstração** é uma representação não física de algo. Pode também ser definida como 'imagem mental subjetiva, irreal. operação intelectual em que um objeto de reflexão é isolado de fatores que comumente lhe estão relacionados na realidade.' (Oxford Language, 2025). Podemos tomar como algo abstrato, uma representação de um elemento ou realidade ainda não materializada. Ainda temos a definição que a abstração é uma versão simplificada de visualizar uma entidade, que omite detalhes que não são importantes.

:::tip[O que é Abstração]

<iframe width="560" height="315" src="https://www.youtube.com/embed/mTNu_seOKFI?si=1t2T2pSueeWnDJCQ" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen style={{ display: 'block', marginLeft: 'auto', maxHeight: '40vh', marginRight: 'auto', marginBottom: '24px' }}></iframe>
<br />
<iframe width="560" height="315" src="https://www.youtube.com/embed/Conf8DKHWmY?si=GhY6hJ0WBmU8z5dN" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen style={{ display: 'block', marginLeft: 'auto', maxHeight: '40vh', marginRight: 'auto', marginBottom: '24px' }}></iframe>
<br />

:::

> "Murilão, vamos lá, gostei da filosofia agora, mas para que isso?"

Ótima pergunta! Vamos utilizar esse conceito de abstração para compreender por que utilizamos os tipos abstratos de dados. Em sua essência, quando estamos falando de tipo abstrato de dados, estamos pensando no que estamos esperando que este elemento traga de funcionamento. Pode parecer obvio, mas ele permite que a energia do desenvolvimento fique focada na implementação da solução que faz uso deste elemento, não dos detalhes se sua implementação.

Quando trabalhamos com TAD, estamos trabalhando com as interfaces fornecidas por eles.

:::note[TAD]

<iframe width="560" height="315" src="https://www.youtube.com/embed/nDeIz2Kq0RE?si=yTn5yVB4rt8fkcA-" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen style={{ display: 'block', marginLeft: 'auto', maxHeight: '40vh', marginRight: 'auto', marginBottom: '24px' }}></iframe>
<br />

<iframe width="560" height="315" src="https://www.youtube.com/embed/XkoeF-xXo2o?si=-qMROvlFdOQMwuJM" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen style={{ display: 'block', marginLeft: 'auto', maxHeight: '40vh', marginRight: 'auto', marginBottom: '24px' }}></iframe>
<br />

<iframe width="560" height="315" src="https://www.youtube.com/embed/ZniDyolzrBw?si=vbARYMdCN7FmMExK" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen style={{ display: 'block', marginLeft: 'auto', maxHeight: '40vh', marginRight: 'auto', marginBottom: '24px' }}></iframe>
<br />

:::

Legal agora vamos trabalhar com uma forma de fazer essas implementações.

## 2. Pensando em uma Implementação para TAD

Legal, agora vamos pensar em como podemos trabalhar com essa implementação. Vamos pensar em um caso de um sistema de emergências. Este sistema deve armazenar os dados das chamadas enviadas pelos usuários. Cada chamada deve ser implementada com algum nível de prioridade atribuída a ele. 

Vamos pensar onde o TAD pode ser implementado nesse sentindo. Vamos analisar o processo em duas frentes:
- Precisamos implementar o registro da chamada, suas características;
- Precisamos implementar o comportamento que liste os dados (do registro) e permita fazer a priorização.

Vamos pensar em como podemos fazer essa implementação. Podemos descrever nosso elemento de chamada como:

```bash
TAD: ChamadaEmergencia
  Atributos:
    - identificador
    - tipo_ocorrencia
    - localizacao
    - horario
    - prioridade

  Operações:
    - acessar_dados()
    - obter_prioridade()
```

Aqui temos um exemplo de como a utilização da abstração é importante e relevante. Observe que aqui, não temos uma especificação para alguma linguagem ou tecnologia, estamos falando apenas dos elementos e da interface que este elemento deve possuir.
Agora, vamos pensar em como podemos utilizar o mesmo padrão para descrever a interface do TAD com o comportamento da lista.

```bash
TAD: FilaPrioridadeChamadas
  Operações:
    - inserir(chamada: ChamadaEmergencia)
    - removerMaisUrgente() -> ChamadaEmergencia
    - consultarMaisUrgente() -> ChamadaEmergencia
    - estáVazia() -> booleano
```

Observe aqui que temos um comportamento apresentado não está dependendo de nenhuma implementação direta. Ele traz uma forma de ver a abstração que traz o comportamento desejado, adicionado ao elemento que desejamos o que queremos sem a necessidade de alterar este comportamento diretamente ao objeto.

Vamos discutir mais um pouco sobre como essa implementação pode ser realizada.

## 3. Pseudocódigo da Implementação

Vamos analisar essa implementação do objeto `ChamadaEmergencia`:

```bash
TAD ChamadaEmergencia
  ATRIBUTOS:
    id: inteiro
    tipo_ocorrencia: texto
    localizacao: texto
    horario: texto
    prioridade: inteiro

  MÉTODOS:
    criar(id, tipo_ocorrencia, localizacao, horario, prioridade) -> ChamadaEmergencia
      nova_chamada.id ← id
      nova_chamada.tipo_ocorrencia ← tipo_ocorrencia
      nova_chamada.localizacao ← localizacao
      nova_chamada.horario ← horario
      nova_chamada.prioridade ← prioridade
      RETORNAR nova_chamada

    obter_prioridade() -> inteiro
      RETORNAR prioridade

    acessar_dados() -> texto
      RETORNAR "ID: " + id + ", Tipo: " + tipo_ocorrencia + ", Local: " + localizacao + ", Prioridade: " + prioridade
```

O que temos aqui:
- Um conjunto de atributos primitivo. Aqui um ponto importante: em alguns casos é necessário 