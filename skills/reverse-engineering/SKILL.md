---
name: reverse-engineering
description: Use este skill quando o usuario pedir uma engenharia reversa, analise arquitetural, mapeamento de entrypoints, entendimento profundo de um repositorio, ou um relatorio tecnico sobre como o sistema funciona na pratica.
metadata:
  priority: 10
  promptSignals:
    phrases:
      - "faça uma engenharia reversa completa"
      - "faca uma engenharia reversa completa"
      - "faça uma engenharia reversa"
      - "faca uma engenharia reversa"
      - "engenharia reversa desse repositorio"
      - "engenharia reversa deste repositorio"
      - "reverse engineer this repository"
      - "reverse engineering deste repositorio"
      - "analise a arquitetura desse repositorio"
      - "analise a arquitetura deste repositorio"
      - "entenda como esse repositorio funciona"
      - "entenda como este repositorio funciona"
      - "gere um relatorio da arquitetura"
      - "gere um relatorio tecnico"
      - "mapeie os fluxos principais"
      - "mostre como o sistema funciona na pratica"
      - "do a full reverse engineering of this repository"
      - "reverse engineer this repository"
      - "analyze the architecture of this repository"
      - "map the main flows of this repository"
      - "generate a technical report for this repository"
      - "show how this system works in practice"
      - "haz una ingenieria inversa completa de este repositorio"
      - "haz una ingenieria inversa de este repositorio"
      - "analiza la arquitectura de este repositorio"
      - "mapea los flujos principales de este repositorio"
      - "genera un informe tecnico de este repositorio"
      - "explica como funciona este sistema en la practica"
    allOf:
      - ["engenharia", "reversa"]
      - ["arquitetura", "repositorio"]
      - ["como", "funciona"]
      - ["gere", "relatorio"]
      - ["fluxos", "principais"]
      - ["reverse", "engineer"]
      - ["technical", "report"]
      - ["main", "flows"]
      - ["ingenieria", "inversa"]
      - ["informe", "tecnico"]
    anyOf:
      - "engenharia reversa"
      - "arquitetura"
      - "entrypoints"
      - "fluxos"
      - "relatorio"
      - "repositorio"
      - "runtime"
      - "onboarding"
      - "reverse engineering"
      - "architecture"
      - "report"
      - "repository"
      - "engineering"
      - "ingenieria inversa"
      - "arquitectura"
      - "informe"
      - "repositorio"
    minScore: 3
---

# Reverse Engineering

Quando o usuario pedir uma engenharia reversa de um repositorio, este skill deve assumir o trabalho completo.

Nao espere instrucoes adicionais sobre:

- como investigar
- quais arquivos ler primeiro
- qual formato exportar
- qual estrutura de relatorio usar

Voce deve conduzir a investigacao e entregar o resultado no padrao oficial deste plugin.

## O que fazer

1. Entender como o repositorio funciona de verdade lendo o codigo.
2. Localizar bootstrap, entrypoints e pontos reais de composicao.
3. Seguir fluxos ponta a ponta com base em evidencia concreta.
4. Identificar ownership, contratos, boundaries, adapters e padroes estruturais.
5. Separar claramente:
   - `fluxo confirmado`
   - `hipotese ainda nao confirmada`
6. Exportar o resultado obrigatoriamente em:
   - `reports/<NomeDoProjeto>/REVERSE-ENGINEERING.md`
   - `reports/<NomeDoProjeto>/ONBOARDING-GUIDE.md`
   - `reports/<NomeDoProjeto>/ARCHITECTURE-GRAPHS.md`

## Idioma

- Detecte o idioma principal do pedido do usuario.
- Escreva os tres reports no mesmo idioma do pedido do usuario.
- Mantenha fixos os nomes dos arquivos exportados:
  - `REVERSE-ENGINEERING.md`
  - `ONBOARDING-GUIDE.md`
  - `ARCHITECTURE-GRAPHS.md`
- Se o usuario misturar idiomas, use o idioma predominante do pedido inicial.
- Se o idioma nao estiver claro, use ingles.

## Comportamento obrigatorio

- Nao suponha nada sem evidencia local.
- Nao responda apenas em texto solto quando o pedido for uma engenharia reversa completa.
- Nao pare em um resumo curto se o pedido implica mapeamento estrutural do repositorio.
- Se o usuario nao especificar o nome do projeto para a pasta `reports/`, derive um nome razoavel a partir do repositorio atual.
- Aceite pedidos naturais em portugues, ingles e espanhol sem exigir o nome do skill.

## Fluxo de execucao

Este skill deve executar a metodologia principal definida em `../codebase-reverse-engineering/SKILL.md`.

Antes de concluir:

- leia `../codebase-reverse-engineering/references/investigation-checklist.md`
- siga o contrato em `../codebase-reverse-engineering/references/output-contract.md`
- siga o padrao de idioma em `../shared/references/multilingual-export-pattern.md`
- produza os tres arquivos de exportacao no padrao oficial

## Entrega esperada

Se o usuario pedir engenharia reversa deste repositorio, a resposta correta nao e apenas explicar.

A resposta correta e:

1. investigar
2. exportar
3. responder com base no material gerado
