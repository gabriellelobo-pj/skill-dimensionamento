---
name: dimensionamento-nciv
description: Dimensiona automaticamente propostas de Concepção do NCiv (ARQ, DI, Estrutural, Elétrico, Hidráulico, GO) a partir dos insumos de um card de lead. Use quando o usuário pedir para dimensionar, validar ou estimar prazo de um projeto/proposta do NCiv, ou mencionar um card com dados de terreno, metragem, disciplinas contratadas e itens especiais (fotovoltaico, piscina, subsolo).
---

# Dimensionamento automático — NCiv

Dimensiona propostas de Concepção a partir do card do lead. Um PO humano sempre revisa o resultado antes de virar proposta. A skill reduz o tempo de validação, não substitui a revisão.

## Quais arquivos ler

1. Identifique as disciplinas contratadas no card (nem todo lead pede todas).
2. Leia sempre `regras/gerais.md`.
3. Leia só o arquivo de cada disciplina contratada:

| Disciplina | Arquivo |
|---|---|
| Arquitetônico (ARQ) | `regras/arq.md` |
| Design de Interiores (DI) | `regras/di.md` |
| Estrutural (EST) | `regras/est.md` |
| Elétrico (ELE) e Hidráulico (HID) | `regras/instala.md` |
| GO | `regras/go.md` |

4. Card com link do Drive ou nome de cliente com pasta de insumos: leia `insumos-drive.md` **antes** de preencher qualquer campo de terreno. Nunca invente um número de inclinação a partir de foto.
5. Projeto perto do limite entre duas faixas: leia `regra-fronteira-faixas.md`. A direção padrão (subir ou descer) **varia por disciplina**.

## Regras gerais

- **Nunca invente número.** Variável sem informação suficiente no card fica como não avaliada e vai para o PO. Não assuma o caso mais comum.
- **Marque a origem de todo dado estimado.** Ex: "declive visível, origem: foto" ou "desnível de 1,8 m, origem: levantamento em PDF".
- **Restrição de escopo leva a "inviável", não a ajuste de prazo.** Ex: elevador no EST, poço no HID, média tensão no ELE. Pare e sinalize, não converta em semanas.
- **Todo ajuste de fronteira leva um comentário de duas linhas** (o que mudou e por quê), no padrão de `regra-fronteira-faixas.md`.

## Quando parar e sinalizar para o PO

A skill não decide sozinha nestes casos:

- Terreno especial (rochoso, leito de rio, mar) ou zoneamento especial. A planilha trata como inviável.
- Planta arquitetônica terceirizada com qualidade duvidosa (paredes desalinhadas, medidas inconsistentes). Não é avaliável pela skill, sempre manual.
- Necessidade de contenção ou muro de arrimo. Fora do escopo do NCiv: sinalizar terceirização com o Clau.
- Divergência entre o que o analista declarou e o que está na pasta de insumos.
- GO com total acima de 8 semanas (regra completa em `regras/go.md`).
- Qualquer guardrail de `regra-fronteira-faixas.md`.

## Formato da resposta

Sempre neste formato e nesta ordem. Quem lê pode ser um PO ou SDR novo: frases simples, sem sigla ou jargão solto. Explique o termo na primeira vez que aparecer, ex: "muro de arrimo (muro que segura a terra)".

**Título:** a primeira linha é sempre `# Projeto [nome do cliente]`, com o campo `Cliente:` do card (ex: `# Projeto Ademir`). O título do chat costuma sair da primeira mensagem; se não sair certo, quem validou renomeia o chat para `Projeto [nome do cliente]`.

**Status:** uma linha logo abaixo do título:
- ✅ Pronto para proposta
- ⚠️ Precisa de revisão do PO
- 🚩 Parado (restrição de escopo ou possível inviabilidade)

**1. Resumo do projeto.** 2-3 linhas: tipo, metragem, cidade, terreno, principais cômodos e itens especiais, disciplinas contratadas.

**2. Pontos de atenção.** Riscos que o PO precisa decidir (restrições de escopo, terreno especial, divergências entre card e pasta). Mais grave primeiro.

**3. Insumos que faltam para validar** (se necessário). O que pedir ao cliente ou analista, incluindo as linhas `INSUMOS:` / `Faltando:` de `insumos-drive.md`.

**4. Dimensionamento por portfólio.**
- Primeiro uma **tabela-resumo** com o total de semanas de cada disciplina contratada. Disciplina não contratada aparece como "não solicitado".
- Depois uma tabela por disciplina com **cada entrega ou etapa e suas semanas** (ex: ARQ com Zoneamento, Análise topográfica, Estudo preliminar…; ELE/HID com a base e cada complementar).

**5. Observações** (se necessário), em duas partes:
- *Suposições:* tudo que a skill decidiu sem regra explícita (ex: "contei a garagem na metragem"). É o que o PO mais precisa conferir.
- *Ajustes de fronteira:* os comentários de duas linhas de `regra-fronteira-faixas.md`, ou `Sem ajustes de fronteira.`

## Arquivos desta skill

```
regras/gerais.md            regras que valem para todas as disciplinas
regras/arq.md, di.md, est.md, instala.md, go.md   faixas e critérios por disciplina
regra-fronteira-faixas.md   o que fazer quando o projeto cai entre duas faixas
insumos-drive.md            como localizar e ler a pasta de insumos do cliente no Drive
fontes.md                   registro das fontes (referência humana, não precisa ler para dimensionar)
```

Quando a base de exemplos validados (projetos reais com input e dimensionamento) estiver consolidada, ela entra numa pasta `exemplos/` referenciada aqui.
