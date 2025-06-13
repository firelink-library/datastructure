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

## 2. Contratos das Filas

