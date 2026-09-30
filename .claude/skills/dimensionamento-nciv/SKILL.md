---
name: dimensionamento-nciv
description: Dimensiona automaticamente propostas de Concepção do NCiv (ARQ, DI, Estrutural, Elétrico, Hidráulico, GO) a partir dos insumos de um card de lead. Use quando o usuário pedir para dimensionar, validar ou estimar prazo de um projeto/proposta do NCiv, ou mencionar um card com dados de terreno, metragem, disciplinas contratadas e itens especiais (fotovoltaico, piscina, subsolo).
---

# Skill de Dimensionamento Automático — NCiv

Esta skill dimensiona automaticamente propostas de Concepção (ARQ, DI, Estrutural, Elétrico, Hidráulico, GO) a partir dos insumos recebidos no card do lead. O resultado é sempre revisado por um PO humano antes de virar proposta — a skill reduz o tempo de validação, não substitui a revisão.

---

## Antes de dimensionar qualquer coisa

1. Identifique **quais disciplinas foram contratadas** no card (nem todo lead pede todas).
2. Para cada disciplina contratada, consulte `regras-dimensionamento-escopo.md` (nesta mesma pasta) — ele traz a variável principal, as faixas numéricas oficiais e os critérios não-óbvios de cada disciplina.
3. Se o card trouxer link do Drive ou nome de cliente com pasta de insumos de terreno, consulte `insumos-drive.md` (nesta mesma pasta) **antes** de preencher qualquer campo de terreno — ele define como localizar a pasta, o que extrair de cada tipo de arquivo, e o vocabulário permitido para inclinação (nunca invente um número de inclinação a partir de foto).
4. Se o projeto cair perto do limite entre duas faixas de uma disciplina, consulte `regra-fronteira-faixas.md` (nesta mesma pasta) — a direção padrão (subir ou descer a faixa) **varia por disciplina**, não é universal.

## Regra geral, vale para todas as disciplinas

- **Nunca invente número.** Se uma variável não tiver informação suficiente no card, marque como não avaliado e sinalize para o PO — não assuma o caso mais comum.
- **Sempre marque a origem de um dado estimado** (ex: "declive visível, origem: foto" vs. "desnível de 1,8m, origem: levantamento em PDF").
- **Restrições de escopo levam a "inviável", não a um ajuste de prazo.** Ex: elevador no Estrutural, poço no Hidráulico, média tensão no Elétrico — pare e sinalize, não tente dimensionar em semanas.
- **Um comentário de duas linhas** deve acompanhar qualquer ajuste de fronteira (o que mudou + por quê), conforme o padrão definido em `regra-fronteira-faixas.md`.

## Quando parar e sinalizar para revisão humana (não decidir sozinha)

- Terreno especial (rochoso, leito de rio, mar) ou zoneamento especial → planilha trata como inviável, a skill não decide isso
- Qualidade da planta arquitetônica terceirizada parecer comprometida (paredes desalinhadas, medidas inconsistentes) → não avaliável pela skill, sempre manual
- Necessidade de contenção/muro de arrimo → fora de escopo do NCiv, sinalizar terceirização com o Clau
- Divergências entre o que o analista declarou e o que foi encontrado na pasta de insumos
- **GO ultrapassando 8 semanas no total** (soma de Quantificação + Orçamento + Planejamento) → teto prático confirmado pelo Heitor Taniguchi é 6-8 semanas; se a soma das faixas por etapa ultrapassar 8, é sinal de erro de aplicação da regra, não um resultado válido — ver `regras-dimensionamento-escopo.md`
- Qualquer dos guardrails listados em `regra-fronteira-faixas.md` (máximo de 2 movimentações de faixa por disciplina, teto de semanas do Estrutural, etc.)

## Formato da resposta

Toda validação sai **sempre neste formato**, nesta ordem. Quem lê pode ser um PO ou SDR novo: escrever em frases simples, sem sigla ou jargão solto (explicar na primeira vez que aparecer, ex: "muro de arrimo (muro que segura a terra)").

**Status:** uma linha no topo, antes de tudo:
- ✅ Pronto para proposta
- ⚠️ Precisa de revisão do PO
- 🚩 Parado (restrição de escopo ou possível inviabilidade)

**1. Resumo do projeto** — 2-3 linhas: tipo, metragem, cidade, terreno, principais cômodos/itens especiais e disciplinas contratadas.

**2. Pontos de atenção** — riscos do projeto que o PO precisa decidir (restrições de escopo, terreno especial, divergências entre card e pasta). Mais grave primeiro.

**3. Insumos que faltam para validar** (se necessário) — lista do que pedir ao cliente/analista. Inclui a linha `INSUMOS:` / `Faltando:` definida em `insumos-drive.md`.

**4. Dimensionamento por portfólio**
- Começa com uma **tabela-resumo** com o total de semanas de cada disciplina contratada (disciplina não contratada aparece como "não solicitado").
- Depois, uma tabela por disciplina com **cada entrega/etapa e suas semanas** (ex: ARQ → Zoneamento, Análise topográfica, Estudo preliminar…; ELE/HID → base + cada complementar).

**5. Observações** (se necessário), separadas em:
- *Suposições:* tudo que a skill decidiu sem regra explícita (ex: "contei a garagem na metragem"). É o que o PO mais precisa conferir.
- *Ajustes de fronteira:* os comentários de duas linhas de `regra-fronteira-faixas.md`, ou `Sem ajustes de fronteira.`

## Estrutura de arquivos desta skill

```
regras-dimensionamento-escopo.md   → variáveis e faixas numéricas por disciplina (ARQ, DI, EST, ELE, HID, GO)
regra-fronteira-faixas.md          → o que fazer quando o projeto cai entre duas faixas
insumos-drive.md                   → como localizar e ler a pasta de insumos do cliente no Drive
```

À medida que a base de exemplos (projetos reais com input + dimensionamento validado, vindos dos 8 novos testes) for consolidada, ela deve ser adicionada em uma pasta `exemplos/` e referenciada aqui.

## Status

Versão inicial. Ainda pendente: (1) resultado dos 8 novos testes de dimensionamento com o template v3, rodando em projeto separado; (2) confirmação da liderança sobre metragem mínima do GO (70 vs. 100m²) e de onde vem a trava de metragem (Instala vs. GO) — enquanto isso não for resolvido, a skill não deve concluir inviabilidade por metragem no GO sozinha.
