---
name: codebase-reverse-engineering
description: Use este skill quando a tarefa exigir entender como um projeto funciona de verdade lendo o codigo, fazendo engenharia reversa de projetos feitos por terceiros, mapeando entrypoints, fluxos, dependencias, contratos, padroes estruturais e causas tecnicas sem assumir nada sem evidencia direta do repositorio.
metadata:
  priority: 9
  promptSignals:
    phrases:
      - "engenharia reversa"
      - "engenharia reversa completa"
      - "reverse engineer"
      - "reverse engineering"
      - "analise a arquitetura"
      - "analise a arquitetura do repositorio"
      - "entenda como esse repositorio funciona"
      - "mapeie os fluxos"
      - "mapeie os fluxos principais"
      - "gere um relatorio da arquitetura"
      - "gere um relatorio do repositorio"
      - "explique como o sistema funciona na pratica"
      - "entrypoints reais"
      - "fluxos principais"
      - "runtime flow"
      - "onboarding tecnico"
      - "full reverse engineering"
      - "analyze the repository architecture"
      - "map the main flows"
      - "generate a repository report"
      - "explain how this repository works"
      - "ingenieria inversa"
      - "analiza la arquitectura del repositorio"
      - "mapea los flujos principales"
      - "genera un informe del repositorio"
      - "explica como funciona este repositorio"
    allOf:
      - ["engenharia", "reversa"]
      - ["arquitetura", "repositorio"]
      - ["fluxos", "principais"]
      - ["como", "funciona"]
      - ["gere", "relatorio"]
      - ["entrypoints", "reais"]
      - ["reverse", "engineering"]
      - ["repository", "architecture"]
      - ["main", "flows"]
      - ["ingenieria", "inversa"]
      - ["informe", "repositorio"]
    anyOf:
      - "engenharia"
      - "reversa"
      - "arquitetura"
      - "entrypoint"
      - "entrypoints"
      - "fluxos"
      - "runtime"
      - "relatorio"
      - "onboarding"
      - "repositorio"
      - "reverse"
      - "engineering"
      - "architecture"
      - "report"
      - "repository"
      - "ingenieria"
      - "inversa"
      - "arquitectura"
      - "informe"
    minScore: 4
---

# Codebase Reverse Engineering

Use este skill quando o objetivo for aprender, explicar, auditar ou depurar como um repositorio funciona na pratica.

Ele foi pensado especialmente para projetos construidos por outras pessoas, com inteligencia artificial ou nao, quando a equipe atual precisa formar uma base confiavel de conhecimento sobre como aquele sistema realmente opera.

Ele existe para responder perguntas como:

- onde uma feature realmente comeca e termina
- qual e o entrypoint de runtime
- como o dado cruza camadas, modulos e servicos
- quais padroes arquiteturais estao em uso
- quais dependencias sao centrais e quais sao detalhes
- porque uma estrutura foi feita desse jeito
- onde um bug provavelmente nasce e como ele se propaga

## Regra central

Nao suponha. Nao complete lacunas com intuicao. Nao responda com base em convencao generica se o repositorio ainda nao foi lido.

E tambem nao pare na primeira explicacao plausivel. Sempre que um conceito, regra, dependencia, boundary ou fluxo parecer entendido, force novas perguntas sobre ele ate descobrir como aquilo realmente se sustenta no codigo.

Se algo nao estiver confirmado no codigo, diga explicitamente:

- `nao confirmado no codigo lido`
- `nao encontrei evidencia local para isso`
- `preciso ler mais arquivos para fechar essa resposta`

## Modo de investigacao profunda

Toda vez que este skill encontrar uma regra nova do sistema, um conceito importante ou um comportamento relevante, ele deve entrar em um ciclo de auto-pergunta antes de concluir.

Perguntas que ele deve fazer para si mesmo:

- de onde exatamente essa regra nasce no codigo
- quem depende dessa regra
- quem quebra se essa regra mudar
- qual e o entrypoint dessa decisao
- onde essa regra e aplicada, validada, transformada ou burlada
- isso vale para o sistema inteiro ou apenas para esse fluxo
- existe contradicao ou excecao em outro arquivo
- existe composicao, adapter, factory, provider, middleware, hook ou controller sustentando isso
- qual dado entra, qual dado sai e quem faz a traducao entre camadas
- o que ainda falta ler para transformar essa explicacao em conhecimento completo

Se ainda houver profundidade a extrair, continue perguntando e buscando evidencia antes de responder.

## Leia Antes

- `references/investigation-checklist.md`
- `references/output-contract.md`
- `../shared/references/multilingual-export-pattern.md`

## Processo

1. Identifique a pergunta operacional real.
2. Localize os arquivos de bootstrap e os entrypoints do recorte investigado.
3. Mapeie ownership do fluxo:
   - quem recebe a entrada
   - quem transforma
   - quem orquestra
   - quem integra com fora
   - quem renderiza, persiste ou publica
4. Siga o fluxo real no codigo usando simbolos, imports, chamadas, schemas, rotas, handlers e configuracoes.
5. A cada conceito ou regra descoberta, faca perguntas excessivas e profundas para expandir o entendimento antes de concluir.
6. Monte um mapa de evidencias com arquivos e trechos concretos antes de concluir.
7. Identifique regras de estrutura:
   - camadas
   - direcao de dependencia
   - contratos
   - factories
   - adaptadores
   - hooks
   - servicos
   - use cases
   - entidades
8. Identifique o porque estrutural de cada decisao importante:
   - isolamento de mudanca
   - reuso
   - boundary de framework
   - testabilidade
   - acoplamento controlado
   - composicao de runtime
9. Para debugging, siga a falha do sintoma ate a origem:
   - entrada
   - estado intermediario
   - boundary
   - causa raiz
10. Consolide o entendimento em um relatorio de engenharia reversa para transferencia de conhecimento.
11. Responda apenas o que estiver sustentado por evidencia lida.
12. Sempre feche com resumo, exemplo e lacunas restantes.

## Guardrails

- Ler o codigo antes de opinar sobre arquitetura.
- Preferir `rg`, leitura de manifests, configs, rotas, schemas e arquivos de composicao antes de abrir arquivos aleatorios.
- Sempre aprofundar a descoberta com auto-perguntas antes de chamar algo de entendido.
- Nao chamar algo de padrao arquitetural sem apontar onde ele aparece.
- Nao dizer que uma dependencia e central sem mostrar onde ela entra no runtime.
- Nao dizer que um modulo e morto sem procurar referencias.
- Nao dizer que um bug esta resolvido sem explicar a cadeia causal.
- Nao encerrar na descricao do fluxo sem explicar tambem ownership, contratos, boundaries e propagacao.
- Quando houver mais de um fluxo possivel, separar:
  - `fluxo confirmado`
  - `hipotese ainda nao confirmada`

## O que este skill deve entregar

- explicacao direta e objetiva
- relatorio final de engenharia reversa voltado a transferencia de conhecimento
- guia de onboarding operacional para novos engenheiros
- arquivo visual de arquitetura e fluxos em Mermaid
- raciocinio tecnico por tras da estrutura
- exemplo concreto do repositorio
- grafo ASCII de fluxo ou dependencia quando isso ajudar
- mapa do fluxo ponta a ponta, da entrada inicial ate a saida final
- padroes estruturais encontrados e onde aparecem
- resumo final de alto sinal

## Formato minimo de resposta

1. `Resumo`
2. `Como funciona`
3. `Por que funciona assim`
4. `Padroes encontrados`
5. `Grafo`
6. `Exemplo concreto`
7. `Lacunas ou proximos arquivos a ler`

## Estrutura de saida obrigatoria

Quando este skill produzir documentacao exportavel, ele deve criar uma pasta:

- `reports/<NomeDoProjeto>/`

Dentro dela, deve gerar por padrao estes tres arquivos:

1. `REVERSE-ENGINEERING.md`
2. `ONBOARDING-GUIDE.md`
3. `ARCHITECTURE-GRAPHS.md`

## Idioma dos reports

- Detecte o idioma principal do pedido do usuario antes de escrever os reports.
- Escreva o conteudo dos reports no mesmo idioma do pedido do usuario.
- Preserve os nomes dos arquivos em ingles para manter o padrao do plugin.
- Se o idioma estiver ambiguo ou misto, use o idioma predominante do primeiro pedido.
- Se ainda assim nao ficar claro, use ingles.

### Responsabilidade de cada arquivo

- `REVERSE-ENGINEERING.md`
  - analise principal baseada em evidencia
  - entrypoints
  - fluxos
  - ownership
  - padroes
  - lacunas

- `ONBOARDING-GUIDE.md`
  - leitura guiada
  - tabela `arquivo -> responsabilidade -> quando ler`
  - checklist de onboarding
  - playbooks curtos por objetivo

- `ARCHITECTURE-GRAPHS.md`
  - diagramas Mermaid separados por visao
  - fluxos por harness
  - fluxo principal
  - fluxo de execucao
  - mapa estrutural de componentes e conexoes

Se fizer sentido, `REVERSE-ENGINEERING.md` e `ONBOARDING-GUIDE.md` devem apontar para `ARCHITECTURE-GRAPHS.md` nos trechos em que a visualizacao ajudar.

## Resultado esperado

O resultado esperado deste skill e um relatorio que permita a engenheiros entender:

- como o projeto inicia
- como os fluxos atravessam camadas
- quais sao os modulos centrais
- quais contratos e boundaries organizam o sistema
- quais padroes aparecem de fato
- onde estao os pontos de extensao, risco e acoplamento

E, quando houver export, esse conhecimento deve ficar organizado de forma repetivel dentro de `reports/<NomeDoProjeto>/`.

O objetivo nao e apenas responder uma duvida pontual. O objetivo final e construir conhecimento operacional confiavel sobre como o projeto funciona.

## Heuristicas de investigacao

- Comece por:
  - `package.json`, `turbo.json`, manifests, configs de framework, bootstrap de app, registradores de rota e pontos de composicao
- Para frontend:
  - comece por `app`, `pages`, layouts, providers, services, features, hooks e contracts
- Para backend:
  - comece por bootstrap HTTP, rotas, controllers, presenters, use cases, entities, repositories e adapters
- Para bibliotecas e packages:
  - comece por exports publicos, factories, registries, adapters e testes
- Para incidentes:
  - comece pelo sintoma observavel e caminhe para tras pelo fluxo real

## Perguntas obrigatorias por descoberta

Quando descobrir algo importante, este skill deve tentar responder, com evidencia, perguntas como:

- qual arquivo introduz isso no runtime
- quem chama isso
- quem e chamado por isso
- qual contrato segura essa troca
- onde isso muda de forma, camada ou responsabilidade
- qual parte e regra de negocio e qual parte e detalhe de framework
- onde existem duplicacoes, excecoes ou atalhos
- o que um engenheiro novo precisaria saber para nao interpretar isso errado

## Quando combinar com outras skills

- Use `debug` quando a tarefa exigir isolamento sistematico de bug e verificacao de causa raiz.
- Use `explain-code` quando a prioridade for didatica e analogias, nao mapeamento profundo.
- Use skills arquiteturais especificas quando o repositorio ja tiver um contrato de camada explicito.
