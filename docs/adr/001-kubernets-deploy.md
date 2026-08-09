# ADR 001 - Usar K3s em VM para deploy

**Status:** Aceito
**Data:** 2026-08-05

## Contexto
Precisamos de um ambiente de orquestração de containers para a API de pedidos, com capacidade de escalar horizontalmente e usar manifests Kubernetes padrão, mas com orçamento e complexidade limitados para o escopo do projeto.

## Alternativas consideradas
**K3s em VM (Nó Único):** Custo menor, provisionamento em menos de 2 minutos, manifests idênticos aos de produção. 
**MKS (Kubernetes Gerenciado):** Alta disponibilidade e gerenciamento facilitado, porém com custo mais elevado para o escopo inicial.
**Docker Compose:** Simples de rodar, mas não reflete práticas reais de orquestração exigidas.

## Decisão
Optamos por utilizar K3s em uma VM (Single Node). O critério decisivo foi manter o custo menor e o provisionamento rápido, garantindo que os manifests gerados sejam idênticos ao que usaríamos em um cluster gerenciado.

## Consequências
**Positivas:** Baixo custo e ambiente Kubernetes real validando os manifestos YAML.
**Negativas:** Falta de alta disponibilidade nativa do control plane; manutenção do sistema operacional fica sob nossa responsabilidade.
