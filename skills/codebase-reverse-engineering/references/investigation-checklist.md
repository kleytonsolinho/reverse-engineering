# Investigation Checklist

Use esta checklist antes de concluir qualquer analise.

## 1. Pergunta operacional

- Qual pergunta real precisa ser respondida?
- O objetivo e explicar arquitetura, achar entrypoint, seguir fluxo ou depurar bug?
- O recorte esta claro: feature, modulo, request, tela, job, comando ou incidente?

## 2. Bootstrap e entrypoints

- Li os manifests principais?
- Li os arquivos de bootstrap relevantes?
- Identifiquei por onde esse fluxo entra em runtime?
- Separei entrypoint confirmado de entrypoint apenas suspeito?

## 3. Fluxo real

- Quem recebe a entrada?
- Quem valida?
- Quem transforma?
- Quem orquestra?
- Quem chama integracoes externas?
- Quem persiste, renderiza ou publica?

## 4. Auto-perguntas profundas

- Para cada regra descoberta, perguntei de onde ela nasce?
- Perguntei quem depende dela e quem quebraria se ela mudasse?
- Perguntei se ela vale para todo o sistema ou so para esse fluxo?
- Procurei excecoes, contradicoes ou forks dessa regra?
- Procurei o contrato, boundary ou adapter que sustenta esse comportamento?
- Continuei investigando ate parar de achar novas perguntas relevantes?

## 5. Evidencia concreta

- Tenho arquivos especificos para sustentar cada afirmacao importante?
- Tenho simbolos, imports, chamadas, rotas, schemas ou configs que provam o fluxo?
- Estou descrevendo o que li ou completando lacunas por intuicao?

## 6. Estrutura

- Quais camadas realmente aparecem no codigo?
- Qual a direcao de dependencia entre elas?
- Existem contratos, interfaces, adapters, factories ou registries?
- Onde o framework termina e onde a regra de negocio comeca?

## 7. Causalidade tecnica

- Se estou falando de bug, segui o sintoma ate a origem?
- Se estou falando de arquitetura, expliquei o porque estrutural com base no codigo?
- Marquei claramente o que e `fluxo confirmado` e o que e `hipotese ainda nao confirmada`?

## 8. Fechamento

- A resposta termina como relatorio de engenharia reversa util para outros engenheiros?
- A resposta cobre fluxo ponta a ponta, padroes encontrados e lacunas restantes?
- Se houver export, a estrutura `reports/<NomeDoProjeto>/` foi criada?
- Os tres arquivos padrao foram gerados quando aplicavel?
- Tudo o que estou afirmando esta confirmado no codigo lido?
- Se nao estiver, eu disse explicitamente que nao confirmei?
