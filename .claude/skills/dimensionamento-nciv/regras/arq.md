# Arquitetônico (ARQ)

**Fonte:** Isabela Lot (PO do ARQ e DI), bench + planilha oficial.
**Variáveis principais:** metragem e terreno (ver `gerais.md`: terreno dimensiona o pré-projeto, metragem o resto).

## Faixas (planilha oficial)

| Etapa | Critério | Semanas |
|---|---|---|
| Planejamento de zoneamento (pré-projeto) | Cidade bem documentada / com precedente | 0,5 |
| | Cidade com legislação difícil de achar ou espalhada | 1 |
| | Cidade pequena mal documentada | 1 |
| | Zoneamento especial | 1,5+ ou **inviável** |
| Análise topográfica (pré-projeto) | Terreno plano ou pouco inclinado | 0 |
| | Desnível 1:20 | 0,5 |
| | Desnível até 1:2 | 1 |
| | Desnível >1:1, ou terreno especial (rochoso, leito de rio, mar) | **inviável** |
| Estudo de Viabilidade / Programa de Necessidades | Projeto comum NCiv | 0,5 |
| | Cliente com ideias prontas convencionais | 0,5 |
| | Cliente com ideias prontas mirabolantes | 1 |
| Estudo Preliminar | Metragem <120m² ou com planta definida | 1 |
| | Metragem >120m² ou sem planta definida | 1,5 |
| | Metragem >200m² ou sobrado | 2 |
| | >300m² ou sobrado com subsolo/adicionais (piscina **não** conta) | 2,5 |
| Anteprojeto (modelagem no Revit, já com 0,5 de gordura embutida) | Mesmas 4 faixas do Estudo Preliminar | 2 / 2,5 / 3 / 3,5 |
| Renderização | Mesmas 4 faixas do Estudo Preliminar | 0,5 / 0,5 / 1 / 1 |
| Projeto Legal | Documentação exigida breve | 1 |
| | Documentação normal / casa mediana | 1 |
| | Documentação extensa / casa complexa | 2 |
| | Documentação extra/especial (ex: aclive que exige projeto de movimentação de terra) | 2,5 |

## Decisões da Lot sobre o gabarito (30/09/2026)

A skill superestimava o ARQ em todos os testes, principalmente no pré-projeto.

- **Pré-projeto de projeto comum ≈ 1 semana no total** (zoneamento 0,5 + topografia 0 + viabilidade 0,5). Se passar disso, confira se algum critério foi aplicado sem motivo claro.
- **Zoneamento "bem documentada"** é a **facilidade de achar a legislação**, não o tamanho da cidade. Legislação recente e fácil de acessar (ex: geoportal onde se digita o endereço e sai tudo): **0,5**, mesmo no interior (Ibiúna é bem documentada). Lei difícil de achar, desatualizada ou espalhada em vários documentos: **1**. "Cidade pequena mal documentada" é o caso extremo, "no fim do mundo". Se possível, verifique a legislação da cidade; se não der, use 0,5 e registre em *Suposições*.
- **Análise topográfica: só o desnível importa**, não a área do terreno. Terreno pouco inclinado: 0.
- **Viabilidade:** 0,5 é o padrão. Total 1 só com pedido do cliente muito específico ou difícil, que exige ir mais a fundo (ex: espaço de serralheria).
- **Projeto legal 2,5 ("terreno em aclive")** só para aclive relevante, da ordem de ~6 m de desnível, que exija **projeto de movimentação de terra** (+1 semana; hoje só a Lot sabe fazer). Terreno levemente inclinado é projeto legal normal (**1**). Com **só foto** não dá para saber o desnível: use 1 e registre em *Suposições* que pode subir se o levantamento mostrar desnível relevante.
- **Piscina não muda a faixa do ARQ.** Não soma nada nem empurra para a faixa de cima; o que dimensiona é a metragem.
- **ARQ não tem teto prático.** A regra é tentar aceitar tudo (diferente do EST e do GO).
- **Topografia não influencia o Anteprojeto/Revit** (ter ou não levantamento, ou só imagem/localização). Use só a faixa da planilha (2-3,5 semanas), com ou sem planta prévia detalhada. Não existe faixa separada "com planta prévia".

## Variáveis secundárias

Todas levam a **aprofundar o estudo de viabilidade**:

- **Cidade do lote:** muda legislação e exigências
- **Condomínio:** acrescenta regras além das municipais
- **Proposta muito diferenciada pelo cliente:** quanto mais foge do usual, mais fundo vai a viabilidade. É julgamento caso a caso, sem limiar numérico (decisão confirmada).

## Restrições de escopo

- **Não fazem urbanismo, paisagismo nem implantação de múltiplas edificações/unidades no mesmo terreno** (ex: condomínio com portaria, salão de festas, quadra, academia). Falta know-how de traçado.
- **Recusam projetos "exorbitantes"** (castelos, condomínios, casas milionárias de altíssimo padrão). Critério de viabilidade da planilha.
- **O critério real de inclinação é a necessidade de contenção**, não o grau isolado. Terreno que exige contenção é viabilidade comprometida.
