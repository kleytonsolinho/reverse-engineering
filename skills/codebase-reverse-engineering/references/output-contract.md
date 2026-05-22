# Output Contract

Toda resposta deste skill deve seguir este contrato minimo.

O objetivo final e produzir um relatorio de engenharia reversa que sirva como base de conhecimento para engenheiros que precisam entender um projeto feito por terceiros.

Quando a tarefa pedir export estruturado, a saida deve ser organizada em:

- `reports/<NomeDoProjeto>/REVERSE-ENGINEERING.md`
- `reports/<NomeDoProjeto>/ONBOARDING-GUIDE.md`
- `reports/<NomeDoProjeto>/ARCHITECTURE-GRAPHS.md`

Os documentos textuais devem referenciar o arquivo de graficos quando a visualizacao ajudar a entender fluxos, conexoes ou boundaries.

## 1. Resumo

- Responda a pergunta principal em linguagem direta.
- Diga o que esta confirmado no codigo.
- Se houver incerteza, explicite.

## 2. Como funciona

- Descreva o fluxo real em ordem.
- Cubra o fluxo ponta a ponta, da entrada inicial ate a saida final, sempre que o recorte permitir.
- Cite arquivos, modulos, simbolos ou pontos de composicao relevantes.
- Separe `fluxo confirmado` de `hipotese ainda nao confirmada` quando necessario.

## 3. Por que funciona assim

- Explique a estrutura com base em evidencias do repositorio.
- Aponte camadas, boundaries, contratos, adapters, factories ou outras regras estruturais observadas.
- Nao atribua intencao sem evidencia local.

## 4. Padroes encontrados

- Liste os padroes estruturais efetivamente encontrados no codigo.
- Para cada padrao, diga onde ele aparece e por que essa leitura e sustentada por evidencia.
- Se houver duvida, marque explicitamente como `nao confirmado no codigo lido`.

## 5. Grafo

- Inclua um grafo ASCII quando ele ajudar a visualizar fluxo, dependencias ou propagacao de falha.
- Prefira grafo pequeno, legivel e baseado no fluxo confirmado.

Exemplo:

```text
entrada
  -> rota/controller
  -> use-case/servico
  -> adapter/repositorio
  -> persistencia ou saida
```

## 6. Exemplo concreto

- Mostre um caminho real do repositorio.
- Use pelo menos um arquivo ou trecho nominal para ancorar a explicacao.

## 7. Lacunas ou proximos arquivos a ler

- Liste o que ainda nao foi confirmado.
- Diga quais arquivos devem ser lidos para fechar a resposta.
- Use frases explicitas como:
  - `nao confirmado no codigo lido`
  - `nao encontrei evidencia local para isso`
  - `preciso ler mais arquivos para fechar essa resposta`

## Profundidade obrigatoria

Antes de concluir, o skill deve se auto responder perguntas como:

- por que acredito que esse fluxo comeca aqui
- que arquivo confirma essa regra
- que modulo depende disso
- existe excecao para esse comportamento
- como esse dado muda ao atravessar camadas
- o que ainda nao foi explicado sobre esse trecho

Se essas perguntas abrirem novas trilhas relevantes, o skill deve investigar mais antes de fechar o relatorio.

## Artefatos visuais

- Gere diagramas Mermaid quando a estrutura do sistema, os fluxos por harness, os boundaries ou as conexoes ficarem mais claros visualmente.
- Se os diagramas ficarem extensos ou forem reutilizaveis, extraia-os para `ARCHITECTURE-GRAPHS.md`.
- Em `REVERSE-ENGINEERING.md` e `ONBOARDING-GUIDE.md`, aponte explicitamente para `ARCHITECTURE-GRAPHS.md` quando isso ajudar.
