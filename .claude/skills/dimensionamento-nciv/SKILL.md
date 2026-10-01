---
name: dimensionamento-nciv
description: Dimensiona automaticamente propostas de Concepção do NCiv (ARQ, DI, Estrutural, Elétrico, Hidráulico, GO) a partir dos insumos de um card de lead. Use quando o usuário pedir para dimensionar, validar ou estimar prazo de um projeto/proposta do NCiv, ou mencionar um card com dados de terreno, metragem, disciplinas contratadas e itens especiais (fotovoltaico, piscina, subsolo).
---

# Skill de Dimensionamento Automático — NCiv

Dimensiona propostas de Concepção (ARQ, DI, Estrutural, Elétrico, Hidráulico, GO) a partir do card do lead. Um PO humano sempre revisa o resultado antes de virar proposta: a skill reduz o tempo de validação, não substitui a revisão.

## Arquivos desta pasta (ler sob demanda)

| Arquivo | Quando ler |
|---|---|
| `regras-dimensionamento-escopo.md` | Sempre, para cada disciplina contratada: variável principal, faixas oficiais, critérios não-óbvios |
| `insumos-drive.md` | Se o card trouxer link do Drive ou nome de cliente com pasta de insumos — **antes** de preencher qualquer campo de terreno |
| `regra-fronteira-faixas.md` | Se o projeto cair perto do limite entre duas faixas — a direção (subir/descer) **varia por disciplina**, não é universal |

Ainda não existe pasta `exemplos/`. Quando a base de exemplos (projetos reais com input + dimensionamento validado, vindos dos 8 novos testes) for consolidada, ela entra em `exemplos/` e é referenciada aqui.

## Procedimento

1. Identificar **quais disciplinas foram contratadas** no card (nem todo lead pede todas).
2. Se houver Drive/pasta do cliente: seguir `insumos-drive.md` antes de preencher terreno (como localizar a pasta, o que extrair de cada arquivo, vocabulário permitido para inclinação). Nunca inventar número de inclinação a partir de foto.
3. Para cada disciplina contratada: aplicar `regras-dimensionamento-escopo.md`.
4. Caso perto do limite entre faixas: aplicar `regra-fronteira-faixas.md`.
5. Montar a resposta no formato abaixo.

## Regras gerais (todas as disciplinas)

- **Nunca inventar número.** Variável sem informação suficiente no card → marcar como não avaliado e sinalizar para o PO. Não assumir o caso mais comum.
- **Sempre marcar a origem de dado estimado** (ex: "declive visível, origem: foto" vs. "desnível de 1,8m, origem: levantamento em PDF").
- **Restrição de escopo → "inviável", não ajuste de prazo.** Ex: elevador no Estrutural, poço no Hidráulico, média tensão no Elétrico. Parar e sinalizar, não dimensionar em semanas.
- **Todo ajuste de fronteira leva comentário de duas linhas** (o que mudou + por quê), no padrão de `regra-fronteira-faixas.md`.

## Parar e sinalizar para revisão humana (não decidir sozinha)

- Terreno especial (rochoso, leito de rio, mar) ou zoneamento especial → a planilha trata como inviável; a skill não decide isso.
- Planta arquitetônica terceirizada com qualidade aparentemente comprometida (paredes desalinhadas, medidas inconsistentes) → não avaliável pela skill, sempre manual.
- Necessidade de contenção/muro de arrimo → fora de escopo do NCiv; sinalizar terceirização com o Clau.
- Divergência entre o que o analista declarou e o que foi encontrado na pasta de insumos.
- **GO acima de 8 semanas no total** (Quantificação + Orçamento + Planejamento). Teto prático confirmado pelo Heitor Taniguchi: 6-8 semanas; se a soma das faixas por etapa passar de 8, é erro de aplicação da regra, não resultado válido (ver GO em `regras-dimensionamento-escopo.md`). **Nunca apresentar total de GO acima de 8**, nem na tabela-resumo nem no detalhe: a linha do GO mostra `🚩 em revisão — soma das etapas passou do teto de 8 semanas`, e os valores por etapa que causaram o estouro vão só em Observações, marcados como "não válidos".
- Qualquer guardrail de `regra-fronteira-faixas.md` (máximo de 2 movimentações de faixa por disciplina, teto de semanas do Estrutural, etc.).

## Formato da resposta (sempre este, nesta ordem)

Público: pode ser um PO ou SDR novo. Frases simples, sem sigla ou jargão solto — explicar na primeira vez que aparecer (ex: "muro de arrimo (muro que segura a terra)").

**Título:** primeira linha sempre `# Projeto [nome do cliente]`, usando o campo `Cliente:` do card (ex: `# Projeto Ademir`). Serve para identificar a conversa (o título do chat costuma vir da primeira mensagem; se não sair certo, quem validou renomeia o chat para `Projeto [nome do cliente]`).

**Status:** uma linha logo abaixo do título, uma destas:
- ✅ Pronto para proposta
- ⚠️ Precisa de revisão do PO
- 🚩 Parado (restrição de escopo ou possível inviabilidade)

**1. Resumo do projeto** — 2-3 linhas: tipo, metragem, cidade, terreno, principais cômodos/itens especiais e disciplinas contratadas.

**2. Pontos de atenção** — riscos que o PO precisa decidir (restrições de escopo, terreno especial, divergências entre card e pasta). Mais grave primeiro.

**3. Insumos que faltam para validar** (se necessário) — o que pedir ao cliente/analista. Inclui a linha `INSUMOS:` / `Faltando:` definida em `insumos-drive.md`.

**4. Dimensionamento por portfólio**
- Começa com uma **tabela-resumo** com o total de semanas de cada disciplina contratada (disciplina não contratada aparece como "não solicitado").
- Depois, uma tabela por disciplina com **cada entrega/etapa e suas semanas** (ex: ARQ → Zoneamento, Análise topográfica, Estudo preliminar…; ELE/HID → base + cada complementar).

**5. Observações** (se necessário), separadas em:
- *Suposições:* tudo que a skill decidiu sem regra explícita (ex: "contei a garagem na metragem"). É o que o PO mais precisa conferir.
- *Ajustes de fronteira:* os comentários de duas linhas de `regra-fronteira-faixas.md`, ou `Sem ajustes de fronteira.`

## Status da skill

Versão inicial. Pendente: (1) resultado dos 8 novos testes de dimensionamento com o template v3, rodando em projeto separado; (2) confirmação da liderança sobre metragem mínima do GO (70 vs. 100m²) e de onde vem a trava de metragem (Instala vs. GO). Enquanto (2) não for resolvido, a skill não conclui inviabilidade por metragem no GO sozinha.
