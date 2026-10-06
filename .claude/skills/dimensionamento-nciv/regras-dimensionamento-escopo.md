# Regras de dimensionamento de escopo — conhecimento tácito dos POs

O que os POs usam para dimensionar escopo, para que o modelo raciocine na mesma ordem e olhe as mesmas variáveis que um PO olharia. As seis disciplinas (ARQ, DI, Estrutural, Elétrico, Hidráulico, GO) têm variáveis e faixas levantadas a partir da planilha de validação oficial (Google Sheets, versão com alterações da Lot) e das bench individuais de cada PO. Há ainda o bloco **ARQ/GBE — Modelagem**, para quando o cliente quer só modelagem de projeto existente (ex: 2D → 3D).

**Índice:** Regras de uso · Regras transversais · ARQ · ARQ/GBE (Modelagem) · DI · Estrutural · Elétrico · Hidráulico · GO · Lacunas · Registro das fontes

---

## Regras de uso (ler antes de dimensionar)

1. **Não inventar faixa nem número.** Caso não coberto aqui → perguntar ao usuário em vez de estimar. Dimensionamento inventado é pior que nenhum, porque parece calibrado.
2. **Identificar a etapa antes de escolher a variável.** No ARQ a variável principal muda conforme a etapa (ver regra transversal abaixo).
3. **Percorrer as três camadas na ordem:** variável principal → variáveis secundárias → critérios não-óbvios.
4. **Marcar explicitamente o que não foi possível avaliar.**
5. **Ausência de critério não-óbvio registrado não significa que não exista** (ver Lacunas, no fim).
6. **Fronteira entre faixas não está aqui** → `regra-fronteira-faixas.md`.

---

## Regras transversais

### Terreno e metragem dimensionam etapas diferentes

O critério mais importante e menos intuitivo do arquivo. Veio do ARQ, mas afeta como qualquer dimensionamento é montado.

| Variável | O que ela dimensiona |
|---|---|
| **Terreno** | Viabilidade do projeto e o pré-projeto |
| **Metragem** | Todas as demais etapas |

Terreno complicado + metragem pequena pode dar pré-projeto longo e etapas seguintes curtas. Dimensionar o pré-projeto por metragem subestima; dimensionar as etapas seguintes por terreno superestima.

### A metragem é a do card, e ela já inclui a garagem

Usar a **área construída escrita no card, como está**. Ela já inclui a garagem (para o NCiv, garagem é área construída, porque é modelada). **Nunca somar a garagem por cima** (ex: card diz 100 m² com garagem no térreo → dimensionar com 100 m², não 200 m²). A confusão vem da legislação, onde às vezes a garagem não é área computável — isso não vale para o dimensionamento. (Confirmado pela Lot em 30/09/2026; bate com o gabarito do Elétrico no mesmo caso.)

---

## Arquitetônico (ARQ)

**Fonte:** Isabela Lot (PO do ARQ e DI) — bench + planilha de validação oficial.
**Variáveis principais:** metragem e terreno.

### Faixas numéricas (planilha oficial)

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
| | >300m² ou sobrado com subsolo/adicionais (piscina **não** conta — ver abaixo) | 2,5 |
| Anteprojeto (modelagem no Revit — já com 0,5 de gordura embutida) | Mesmas 4 faixas acima | 2 / 2,5 / 3 / 3,5 |
| Renderização | Mesmas 4 faixas acima | 0,5 / 0,5 / 1 / 1 |
| Projeto Legal | Documentação exigida breve | 1 |
| | Documentação normal / casa mediana | 1 |
| | Documentação extensa / casa complexa | 2 |
| | Documentação extra/especial (ex: terreno em aclive que exige projeto de movimentação de terra) | 2,5 |

### Decisões da Lot sobre o gabarito (30/09/2026)

Vieram da comparação com a validação da Lot nos testes do template v3 — a skill superestimava o ARQ em todos os casos, principalmente no pré-projeto.

- **Pré-projeto de projeto comum ≈ 1 semana no total** (zoneamento 0,5 + topografia 0 + viabilidade 0,5). Se a soma passar disso, conferir se algum critério foi aplicado sem motivo claro.
- **Zoneamento — "bem documentada" = facilidade de achar a legislação**, não tamanho da cidade.
  - Legislação recente e fácil de acessar (ex: site/geoportal onde se digita o endereço e sai tudo) → **0,5**, mesmo em cidade de interior (ex: Ibiúna é bem documentada).
  - Lei difícil de encontrar, desatualizada ou espalhada em vários documentos → **1**.
  - "Cidade pequena mal documentada" é o caso extremo, "no fim do mundo".
  - Quando possível, **verificar** se a legislação da cidade é fácil de achar; se não der, usar 0,5 e registrar em *Suposições*.
- **Análise topográfica — só o desnível importa, a área do terreno não.** Critérios antigos "terreno >300m²" e ">700m²" foram retirados. Terreno pouco inclinado → 0.
- **Viabilidade:** 0,5 é o padrão; +0,5 (total 1) só com pedido muito específico ou difícil do cliente, que exige ir mais a fundo (ex: um espaço de serralheria).
- **Projeto legal 2,5 ("terreno em aclive")** só para aclive relevante — da ordem de ~6 m de desnível — que exija **projeto de movimentação de terra** (+1 semana; hoje só a Lot sabe fazer). Terreno levemente inclinado → projeto legal normal (**1**). Com **só foto** não dá para saber o desnível: usar 1 e registrar em *Suposições* que pode subir se o levantamento mostrar desnível relevante.
- **Piscina não muda a faixa do ARQ.** Não soma nada nem empurra para a faixa mais alta ("ninguém vai ficar três dias modelando a piscina") — o que dimensiona é a metragem. A Lot tirou a piscina da planilha.
- **Não existe teto prático para o ARQ** — a regra é tentar aceitar tudo (diferente do Estrutural e do GO). Exceção da planilha oficial: **área construída >500 m² → reunião de validação** (não é inviável; dimensionar normalmente e marcar para revisão do PO).
- **Anteprojeto/Revit — confirmado, ponto fechado:** a topografia (ter ou não levantamento, ou só imagem/localização exata) **não influencia**. Seguir só a faixa única da planilha (2-3,5 semanas), haja ou não planta prévia detalhada. Não há faixa separada "com planta prévia".

### Variáveis secundárias

Todas levam à mesma consequência: **aprofundar o estudo de viabilidade**.
- **Cidade do lote** — muda legislação e exigências
- **Condomínio** — camada de regras além da municipal
- **Proposta muito diferenciada pelo cliente** — quanto mais se afasta do usual, mais fundo o estudo de viabilidade. Julgamento caso a caso, sem limiar numérico (decisão confirmada, não é lacuna).

### Critérios não-óbvios / restrições de escopo

- **Não fazem implantação de múltiplas edificações no mesmo terreno** (ex: condomínio com portaria + salão de festas + quadra + academia) — falta de know-how de traçado
- **Recusam projetos "exorbitantes"** (castelos, condomínios, casas milionárias de altíssimo padrão) — critério de viabilidade na planilha oficial
- **Não fazem urbanismo (masterplan), paisagismo, nem implantação de múltiplas unidades no terreno**
- **Critério real de inclinação é a necessidade de contenção**, não o grau isolado (ver Análise topográfica). Desnível 1:1 ou terreno que exige técnicas de contenção → viabilidade comprometida
- **Também na lista de viabilidade da planilha:** falta de insumos para validação, zoneamento especial, tecnologias construtivas ainda não exploradas, projeto executivo de sistema
- **DI não dimensiona pontos hidráulicos e elétricos** — só indicação de posicionamento recomendado

**Modelagem por metragem/pavimento (150-300m² = 2 … >1000m² = 4,5 ou inviável)** é do bloco **ARQ/GBE — Modelagem** (seção abaixo), não da Concepção do ARQ nem do DI. Não usar essas faixas para dimensionar ARQ ou DI de concepção.

---

## ARQ/GBE — Modelagem

**Quando usar:** o cliente quer **modelagem** de um projeto que já existe (ex: passar de 2D para 3D / BIM), não um projeto de concepção. Dimensionar só este bloco, não as etapas de Concepção do ARQ.
**Fonte:** planilha de validação oficial, bloco "Validação de Leads (ARQ/GBE) — por pavimento".

### Faixas numéricas (planilha marca "POR PAVIMENTO")

| Etapa | Critério | Semanas |
|---|---|---|
| Preparação — famílias criadas | 0 famílias | 0 |
| | 1-5 famílias | 2 |
| | 5+ famílias | 2,5 ou **inviável** |
| Preparação — tipos criados pela parametrização | 1-5 tipos | 0,5 |
| | 5-10 tipos | 1 |
| | 10+ tipos | 1,5 |
| Modelagem | 150-300m² | 2 |
| | 400-800m² | 3 |
| | 800-1000m² | 4 |
| | >1000m² | 4,5 ou **inviável** |
| Criação do modelo federado (todos os pavimentos) | 3 pavimentos tipo | 1,5 |
| | 4 pavimentos tipo | 2 |
| | 5+ pavimentos tipo | 2,5 |

- **Premissa da planilha:** "analistas capacitados suficientes para a execução de todos os pavimentos tipos do empreendimento".
- **Mais de um tipo de pavimento — ainda não definido** se as etapas por pavimento rodam em paralelo (conta uma vez, o pavimento mais pesado) ou somam para cada tipo de pavimento. A skill **não decide**: mostra o valor de **um** pavimento (Famílias + Tipos + Modelagem) + modelo federado, explica as duas leituras em *Suposições* e marca ⚠️ para revisão do PO. Com um único pavimento não há ambiguidade.
- **Modelo federado** só tem faixa a partir de 3 pavimentos tipo; com 1-2, não incluir e registrar em *Suposições*.
- **Buraco 300-400m²** → `regra-fronteira-faixas.md` (faixa acima). **Abaixo de 150m²** a planilha não tem faixa → não inventar; perguntar ao PO.

### Viabilidade (planilha oficial)

- **Falta de insumos necessários para validação** → não validar; pedir os insumos.
- Pontos que definem a viabilidade: **quantidade e complexidade de famílias** a desenvolver, **número de tipos de pavimentos** do empreendimento e **metragem**. Topo das faixas (5+ famílias, >1000m²) = "ou inviável" → revisão humana, a skill não recusa sozinha.

---

## Design de Interiores (DI)

**Fonte:** planilha de validação oficial (aba separada do ARQ, mesma PO — Isabela Lot).

### Faixas numéricas — entregas padrão (sempre entram no total)

| Etapa | Critério | Semanas |
|---|---|---|
| Representação geométrica da arquitetura no Revit | 0-50m² | 0,5 |
| | 50-150m² | 1 |
| | >150m² | 1,5 |
| Modelagem dos móveis | 1-5 móveis | 1,5 |
| | 5-10 móveis | 2,5 |
| | 10-15 móveis | 3 |
| | 15+ móveis | 3,5 |
| Paginação | 1 cômodo | 0,5 |
| | 2-4 cômodos ou até 50m² | 0,5 |
| | 5+ cômodos ou >50m² | 1 |
| Pranchas de Marcenaria e Marmoaria | 1-5 móveis | 1 |
| | 5-10 móveis | 1,5 |
| | 10-15 móveis | 2 |
| | 15+ móveis | 2,5 |
| Caderno de Projetos | 1 cômodo | 0,5 |
| | 2-4 cômodos ou até 100m² | 1 |
| | 5+ cômodos ou >100m² | 1 |
| Renderização | 0-50m² | 0,5 |
| | 50-150m² | 0,5 |
| | >150m² | 1 |

### Entregas opcionais — só se o cliente pedir

**Não fazem parte do DI padrão.** Só dimensionar se o card/cliente pedir explicitamente; caso contrário, aparecem na tabela do DI como "não solicitado" e **não somam no total**. Card que não menciona → não incluir (não assumir que o cliente quer).

| Etapa | Critério | Semanas |
|---|---|---|
| Projeto luminotécnico | 1 cômodo | 0,5 |
| | 2-4 cômodos ou até 50m² | 0,5 |
| | 5+ cômodos ou >50m² | 1 |
| Previsão de pontos hidráulicos e elétricos | Se o cliente pedir | +1 semana |

- **Previsão de pontos ≠ dimensionamento.** DI **não dimensiona pontos hidráulicos e elétricos** — só faz uma indicação de posicionamento possível/recomendado. Se o cliente quer pontos dimensionados, é escopo do Elétrico/Hidráulico.

### Viabilidade (planilha oficial)

- **Falta de insumos necessários para validação** → não validar; pedir os insumos.
- **Reforma que envolva demolição ou construção de cômodos** → fora do DI; sinalizar para o PO (é escopo de ARQ, não de interiores).
- **Dimensionamento de pontos hidráulicos e elétricos** → inviável no DI (ver acima).
- **Gargalo de capacitação (crítico, não numérico):** hoje só a Lot sabe fazer DI no Revit (a validação padrão é no Sketchup). Não há processo formal de validação de DI no Revit nem responsável definido para criá-lo após a saída dela para CP.

---

## Estrutural (EST)

**Fonte:** Julia Lee ("Julee", PO do Estrutural) — bench + planilha de validação oficial. (Os dados vieram da Julee, anotados por Gabrielle Lobo durante a conversa.)

### Variáveis principais

Base: **sobrado de 200m² = 5 semanas.** Somar os ajustes a partir dessa base:

| Variável | Faixa | Ajuste |
|---|---|---|
| Tamanho da casa | <50m² | -2 semanas |
| | <150m² | -1 semana |
| | >300m² | +1 semana |
| | >400m² | +2 semanas |
| | >500m² | +3 semanas |
| Complexidade do terreno | Plano | sem alteração |
| | Inclinado | +1 semana |
| | Tão inclinado a criar novo andar | +2 semanas |
| Andares | Sobrado | sem alteração |
| | Mais andares (diferente dos demais) | +1 semana |
| | Prédio (andares parecidos) | análise diferente — ex: Guarulhos, 7 andares, ~9 semanas |
| Complexidade | Solução estrutural muito complexa | +1 semana |
| | Algo que ainda não fizeram | +1 semana |

**Teto prático:** dificilmente um projeto passa de 8-9 semanas.

### Variáveis secundárias

- **Piscina** → **+1 semana**
- **Muro de arrimo** → não é ajuste de prazo, é restrição de escopo (ver abaixo)

### Critérios não-óbvios

Geométricos, só visíveis na planta — nenhum é dedutível de metragem, endereço ou valor de contrato. Sem a planta na entrada, o dimensionamento estrutural fica incompleto por definição:
- **Janelas muito grandes**
- **Paredes que não se alinham entre pavimentos**
- **Pé-direito muito alto**
- **Paredes inclinadas**
- **Encanamento no subsolo** — nunca vem informado nos cards; importante mapear
- **Cômodos maiores que o padrão (~6x6m)** — ex: card recente com "garagem que ocupa o terreno inteiro"
- **Qualidade/origem da planta arquitetônica terceirizada** — plantas de baixa qualidade (paredes desalinhadas, medidas inconsistentes, subsolo menor que o terreno) são **não avaliáveis pela skill**; checagem manual mesmo com a skill implementada

### Restrições de escopo

- **Só concreto armado** como solução estrutural própria (executada internamente).
- **Steel frame, tijolo ecológico e alvenaria estrutural** não são executados internamente, mas podem ser **terceirizados com o engenheiro parceiro Clau**. O dimensionamento desses sistemas não está mapeado aqui: perguntar ao Clau, não usar as faixas de concreto armado.
- **Muro de arrimo nunca foi feito internamente pelo Estrutural do NCiv** — fora do escopo padrão, não ajuste de prazo.
- **Inviáveis (planilha oficial):** pavimentação (nunca aceitam, mesmo com leads de prefeitura/condomínio), reformas, edifícios muito altos, estruturas não convencionais, projetos de contenção de alta complexidade, infraestrutura urbana, projetos com elevador, muro de arrimo.
- **Não recomendado — risco alto:** prédios. Não é inviável, mas o risco é muito grande; recomendação é não aceitar → sinalizar para o PO.
- **⚠ Elevador = inviável total** (mudança recente na planilha oficial: saiu de "complexidade +1 semana"). A planilha ainda tem um texto de referência antigo não corrigido — desconsiderar qualquer menção a elevador como "+1 semana" em versões antigas deste ou de outros documentos.

---

## Elétrico (ELE)

**Fonte:** Paulinho (PO de Hidrossanitário e Elétrico) — bench + planilha de validação oficial.
**Variável principal:** metragem.

### Faixas numéricas (estrutura: Croqui + Predim + Dim + Doc)

| Faixa | Total |
|---|---|
| Base até 200m² | 3 semanas |
| 200-400m² | 5 semanas |
| >600m² | faixa mais aberta / flexível, caso a caso |

**Regra de escala:** acima de 200m², cada 200m² adicionais soma +0,5 semana em cada etapa (Croqui, Predim, Dim, Doc).

### Complementares (cada um soma à base)

| Complementar | Acréscimo |
|---|---|
| Fotovoltaico | +0,5 |
| Cabeamento | **+1** (a maioria não sabe fazer, por isso é maior que os outros) |
| Reuso | +0,5 |
| Climatização | **não soma no Elétrico** — só Hidráulico (confirmado em 30/09/2026) |
| Piscina | **não soma no Elétrico** — só Hidráulico (confirmado em 30/09/2026) |
| Gás | +0,5 |

**Exemplo real (planilha oficial):** casa de 300m² com todos os complementares = **6 semanas** no Elétrico.

### Variável secundária não-óbvia: tipo de aquecimento de água

Não é ter ou não (quase toda casa tem), é o tipo:
- A gás (mais comum) — menor impacto no dimensionamento elétrico
- Elétrico de passagem (ex: chuveiro elétrico tipo Lorenzetti) — maior consumo, exige mais atenção, principalmente em casas menores com pouca folga de carga

Ainda **não está na planilha oficial** — só levantada na bench com o Paulinho.

### Restrições de escopo

- **Não fazem média tensão** (>75kW de carga instalada) — "não sabemos fazer e Francisco não pode assinar"
- **Não fazem instalação de elevador**

### Arredondamentos da planilha (não são regra de fronteira)

- Metragem quebrada dimensiona no limite superior (ex: 300m² é tratado como 400m²)
- Metragem desconhecida do cliente: se for casa térrea, estimar ~200m²
- Soma final quebrada arredonda para cima (ex: 3,5 → 4)
- **Complementares por metragem:** casa de **400m² para cima** → cada complementar soma +0,5 a mais (vale para Elétrico e Hidráulico)

---

## Hidráulico (HID)

**Fonte:** Paulinho (mesmo PO do Elétrico) — bench + planilha de validação oficial.
**Variável principal:** metragem — mesma estrutura e faixas do Elétrico (Croqui + Predim + Dim + Doc; base até 200m² = 3 semanas; 200-400m² = 5 semanas).

### Complementares

Mesma tabela do Elétrico (fotovoltaico +0,5, cabeamento +1, reuso +0,5, gás +0,5), mais **climatização +0,5** e **piscina +0,5**, que no Instala só somam aqui no Hidráulico.

**Exemplo real (planilha oficial):** casa de 300m² com todos os complementares = **7 semanas** no Hidráulico (uma a mais que o Elétrico no mesmo cenário).

### Variável secundária não-óbvia: declive do terreno → estação elevatória (+0,5 semana)

O esgoto escoa por gravidade. Se a casa fica **mais baixa** que o ponto de coleta de esgoto, é preciso projetar uma **estação elevatória de esgoto** (equipamento que bombeia o esgoto para cima, contra a gravidade, até a coleta). Casos reais: o Farage no projeto "Sonho Palpável"; a Bel no "Cuara".

**Impacto no prazo: +0,5 semana.** Ainda não é campo formal do Hidráulico na planilha oficial (a análise topográfica formal só existe na aba de ARQ), mas já está confirmada e numerada aqui.

### Restrições de escopo

- **Não fazem poço** — componentes específicos não existem no builder
- **Não fazem climatização além de multi-split e cassete** — alinhar já na venda, ou não vender esse item

### Restrições que valem para Elétrico e Hidráulico

- **Reforma só é possível com as plantas estruturais, elétricas e hidrossanitárias existentes** — no geral, "reforma" no núcleo significa fazer uma nova casa no mesmo terreno
- **DI + Instala vendidos sozinhos (sem ARQ) sempre deu problema** — se vender assim, o escopo precisa estar muito bem definido em contrato
- **Prédios / edifícios muito altos: não recomendado — risco alto.** Não é todo inviável, mas recomendação é não aceitar → sinalizar para o PO.
- **Residências multifamiliares:** não são sempre inviáveis, mas têm limitações técnicas — fotovoltaico não atende a demanda de energia mais alta; padrão de entrada e hidrômetro são impeditivo técnico, mas o builder resolve

### Decisões confirmadas nos testes do template v3 (30/09/2026)

- **Item "futuro" ou "só preparação"** (ex: preparação para painel solar, para piscina futura): dimensionar **como item completo**, com o acréscimo cheio do complementar. Não existe de fato "preparação" — o cliente executa usando o nosso projeto quando quiser.
- **Garagem:** usar a área do card como está; **nunca somar a garagem por cima** (regra transversal). *Corrigido em 30/09/2026: a versão anterior mandava somar, o que gerou erro de +2 semanas no Elétrico no gabarito.*
- **Fossa séptica não soma prazo** no Hidráulico, mas **registrar na validação** se o projeto usa fossa (útil para o projeto e evita perguntar de novo).
- **Piscina e climatização são só Hidráulico** — não somam no Elétrico, mesmo que o card os cite no escopo do Elétrico.

### Falta levantar

- Incluir formalmente o campo "declive do terreno / necessidade de estação elevatória de esgoto" na planilha oficial do Hidráulico (hoje só documentado aqui).

---

## GO

**Fonte:** planilha de validação oficial + bench com Heitor Tani (PO de GO).
**Variável principal:** **número de disciplinas contratadas** — não principalmente metragem, ao contrário das outras disciplinas.

### Estrutura e faixas numéricas

Três etapas, cada uma com faixa mínima (~70m², todas as disciplinas) e máxima (~200m², todas as disciplinas):

| Etapa | Mínimo | Máximo |
|---|---|---|
| Quantificação | 2 semanas | 4 semanas |
| Orçamento | 3 semanas | 4 semanas |
| Planejamento | 2 semanas | 4 semanas |

**Teto do GO no total:** Quantificação + Orçamento + Planejamento tem teto prático de **6-8 semanas** (confirmado por Heitor Taniguchi). Soma acima de 8 = erro na aplicação da regra, não resultado válido → parar e marcar para revisão humana, com comentário de duas linhas. **Nunca apresentar total de GO acima de 8 semanas** (nem na tabela-resumo, nem no detalhe): mostrar `🚩 em revisão` e colocar os valores por etapa só em Observações, marcados como "não válidos".

### Pontos de atenção por etapa (planilha oficial)

**Quantificação** — duas partes: colocar os elementos modelados na EAP proposta; depois criar regras de extração do que não será modelado mas será quantificado. **O que pesa é a disciplina, não o tamanho:**
- Estrutural: regras de extração ensinadas no treinamento, não muda com tamanho — impacto **baixo**
- Instala: ainda muito manual/automático, segue método do treinamento (deve evoluir, mas não tão cedo) — impacto **baixo**
- **ARQ "manda"**: o mais perigoso, costuma vir modelado com menos informação, itens perdidos garimpados na mão, **define o prazo da etapa** — impacto **alto**
- Disciplina modelada por terceiros (não pela própria equipe): **+1 semana por padrão**, exceto se vier do Iberque ou do Builder

**Orçamento:**
- Só pode usar a **SINAPI** — não representa bem padrão alto, serve para baixo e médio padrão — impacto **crucial**
- **Instala "manda"**: quanto maior o Instala, mais itens associados a orçar, e são itens ruins de orçar — impacto **alto**
- Complementares no Instala (fotovoltaico, reuso, PCI, etc.) puxam o prazo para cima: **+2 semanas com todas**
- Estrutural é tranquilo; ARQ dá trabalho mas não muda muito o prazo final — impacto **baixo**
- Processo hoje muito manual/braçal — já se estudou usar IA, ainda não confirmado em produção

**Planejamento:**
- Ao contrário das outras etapas, **todas as disciplinas pesam praticamente igual**
- É a etapa que a equipe **menos domina** — risco reconhecido
- **Comportamento linear:** prazo cresce proporcional ao tamanho do projeto
- Teto prático: 4 semanas já é bastante; 6 é considerado muito

### Pendências "A CONFIRMAR" na planilha

- **Metragem mínima:** planilha registra 70m², um áudio de quantificação cita 100m². Não definido qual vale.
- **De onde vem a trava de metragem:** acima do limite, quem barra é o **Instala**, não o GO — ainda não formalizado. A skill não conclui inviabilidade por metragem no GO sozinha.
- **Como as etapas se combinam frente ao teto de 8:** somando as faixas, o mínimo já dá 7 semanas (~70m²) e o máximo 12 (~200m²) — qualquer projeto acima de ~100m² com as três etapas ultrapassa o teto. Não está definido se as etapas se sobrepõem (e quanto) ou se as faixas precisam ser revistas. Até confirmar com o Heitor, a skill não compensa sozinha: todo GO acima de 8 vai para revisão humana.
- **Trecho de áudio inaudível** sobre planejamento, com números não confirmados ("...m² é duas semanas, 144, 210, talvez seis") — não transcrito para não inventar número.

---

## Lacunas que valem para todo o arquivo

- **Faixas ainda não calibradas contra o histórico.** A base de projetos passados quase não tem área construída e endereço (2 de 346 projetos com área construída, endereço em nenhum). Os números vêm da planilha oficial e das bench, não de regressão — a validação continua prospectiva.
- **"Todos os critérios são óbvios"**, dito por um especialista, normalmente significa conhecimento automatizado, não compartilhado. Por isso a ausência de critério não-óbvio registrado numa disciplina não prova que ele não exista.

---

## Registro das fontes

| Data | Fonte | Disciplina | O que trouxe |
|---|---|---|---|
| 03/09/2026 | Julia Lee ("Julee") | Estrutural | 5 variáveis principais, estruturas especiais, 4 dificuldades de planta (anotado por Gabrielle Lobo durante a conversa — atribuição corrigida) |
| 03/09/2026 | Isabela Lot | Arquitetônico | Distinção terreno / metragem por etapa, 3 variáveis secundárias |
| 30/09/2026 | Isabela Lot (áudios sobre o gabarito) | Arquitetônico | Pré-projeto ≈ 1 semana; "bem documentada" = facilidade de achar a legislação; topografia só por desnível; projeto legal 2,5 só com movimentação de terra; piscina não muda faixa; sem teto; metragem do card já inclui garagem |
| — | Paulinho | Elétrico / Hidráulico | Tipo de aquecimento de água, declive do terreno, faixas numéricas, complementares |
| — | Julia Lee ("Julee") | Estrutural (bench formal) | Concreto armado, steel frame, encanamento no subsolo, cômodos >6x6m, qualidade de planta terceirizada |
| — | Heitor Tani | GO | Pontos de atenção por etapa, pendências "a confirmar" |
| — | Planilha de validação oficial (Google Sheets, versão com alterações da Lot) | Todas | Faixas numéricas de ARQ, DI, Estrutural, Elétrico, Hidráulico, GO |
| 01/10/2026 | Gabi (otimização) | Todas | Reescrita dos 4 .md para leitura de agente — sem mudança de regra nem de número |
| 06/10/2026 | Planilha de validação oficial (atualizada pelos POs) + Gabi | DI (principal), ARQ, Estrutural, Instala | DI: representação no Revit com corte em 150m²; paginação 0,5/0,5/1; renderização 0,5/0,5/1; luminotécnico 0,5/0,5/1 e **opcional (só se o cliente pedir — Gabi)**; previsão de pontos +1 só se pedir; viabilidade do DI; "Modelagem por metragem" saiu do DI (é ARQ/GBE). ARQ: >500m² → reunião de validação; itens de viabilidade. EST: reformas, elevador e muro de arrimo na lista de inviáveis; prédios não recomendados. Instala: prédios não recomendados; complementares +0,5 a partir de 400m² |
| 06/10/2026 | Planilha de validação oficial + Gabi | ARQ/GBE | Bloco de Modelagem adicionado (famílias, tipos, modelagem por metragem, modelo federado; viabilidade). Usado quando o cliente quer modelagem (ex: 2D → 3D). Soma com vários tipos de pavimento em aberto → PO revisa |
| 06/10/2026 | Planilha de validação oficial | DI | Representação geométrica e Renderização passaram a ser por **metragem** (0-50 / 50-150 / >150m²) em vez de nº de cômodos; semanas iguais |
