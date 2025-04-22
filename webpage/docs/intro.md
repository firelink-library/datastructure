---
sidebar_position: 1
slug: /
---

# Introdução

Este é apenas um template para você poder criar um repositório de conteúdo
rapidamente e com uma configuração opinionada do Docusaurus.

Neste repositório, já estão configurados:

* A base do docusaurus, que fica dentro do diretório `webpage`

## 1. O que você precisa fazer

### 1.1. Modificar o nome da página

## 2. O que você pode querer fazer

Não vou delinear todas as funcionalidades do docusaurus. Para isso, existe a
[documentação do docusaurus](https://docusaurus.io/docs/next). No entanto, há
algumas coisas que você pode querer fazer e que são esperadas pela natureza do
conteúdo que vamos publicar aqui. Para essas, vou deixar um pequeno tutorial.

### 2.1. Adicionando equações `LaTeX`

**Inline**

```LaTeX
Let $f\colon[a,b]\to\R$ be Riemann integrable. Let $F\colon[a,b]\to\R$ be
$F(x)=\int_{a}^{x} f(t)\,dt$. Then $F$ is continuous, and at all $x$ such that
$f$ is continuous at $x$, $F$ is differentiable at $x$ with $F'(x)=f(x)$.
```

Let $f\colon[a,b]\to\R$ be Riemann integrable. Let $F\colon[a,b]\to\R$ be
$F(x)=\int_{a}^{x} f(t)\,dt$. Then $F$ is continuous, and at all $x$ such that
$f$ is continuous at $x$, $F$ is differentiable at $x$ with $F'(x)=f(x)$.

**Bloco**

```LaTeX
$$
I = \int_0^{2\pi} \sin(x)\,dx
$$
```

$$
I = \int_0^{2\pi} \sin(x)\,dx
$$
