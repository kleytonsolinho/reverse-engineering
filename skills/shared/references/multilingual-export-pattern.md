# Multilingual Export Pattern

Use este padrao quando um skill ou agente precisar aceitar pedidos em linguas diferentes, mas ainda assim produzir artefatos estruturados em um formato fixo.

## Objetivo

Permitir que o usuario fale naturalmente no idioma dele sem precisar aprender nomes tecnicos do plugin, while keeping export structure deterministic.

## Regras

1. Detecte o idioma principal do pedido inicial do usuario.
2. Responda ao usuario no mesmo idioma predominante.
3. Escreva o conteudo dos artefatos exportados no mesmo idioma do pedido inicial.
4. Mantenha fixos nomes de arquivos, slugs, ids tecnicos e caminhos estruturais.
5. Se o pedido misturar idiomas, escolha o idioma predominante do primeiro pedido relevante.
6. Se o idioma nao estiver claro, use ingles como fallback.

## O que fica localizado

- introducoes
- explicacoes
- tabelas
- checklists
- exemplos narrativos
- titulos de secoes dentro dos reports

## O que fica fixo

- nomes de arquivo
- nomes de skill
- ids tecnicos
- nomes de pasta
- chaves de configuracao
- caminhos de exportacao

## Exemplo

Pedido em portugues:

- export path:
  - `reports/MyProject/REVERSE-ENGINEERING.md`
- report language:
  - portugues

Pedido em espanhol:

- export path:
  - `reports/MyProject/ONBOARDING-GUIDE.md`
- report language:
  - espanhol

Pedido em ingles:

- export path:
  - `reports/MyProject/ARCHITECTURE-GRAPHS.md`
- report language:
  - ingles

## Reutilizacao em novos agentes

Ao criar novos agentes ou skills:

- reutilize este padrao para separar idioma do usuario de estrutura tecnica
- mantenha o contrato de export estavel
- adicione prompt signals em mais de um idioma
- nao force o usuario a invocar o skill por nome quando a intencao puder ser inferida
