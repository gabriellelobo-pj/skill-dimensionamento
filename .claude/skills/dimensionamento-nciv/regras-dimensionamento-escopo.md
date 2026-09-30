# Regras de dimensionamento de escopo — conhecimento tácito dos POs

Este arquivo registra o que os POs usam para dimensionar escopo. O objetivo é que o modelo raciocine na mesma ordem e olhe para as mesmas variáveis que um PO olharia.

**Status:** todas as cinco disciplinas (ARQ, Estrutural, Elétrico, Hidráulico, GO) já têm variáveis e faixas numéricas levantadas, com base na planilha de validação oficial (Google Sheets, versão com alterações da Lot) e nas bench individuais de cada PO.

---

## Regras de uso

Leia esta seção antes de dimensionar qualquer coisa.

1. **Não invente faixa nem número.** Onde este arquivo não cobrir um caso, pergunte ao usuário em vez de estimar. Um dimensionamento inventado é pior que nenhum, porque parece calibrado.
2. **Identifique a etapa antes de escolher a variável.** No arquitetônico a variável principal muda conforme a etapa (ver regra transversal abaixo).
3. **Percorra as três camadas na ordem:** variável principal → variáveis secundárias → critérios não-óbvios.
4. **Marque explicitamente o que você não conseguiu avaliar.**
5. **Ausência de critério não-óbvio registrado não significa que não exista** — ver nota no fim do arquivo.
6. **Regras de arredondamento em fronteira não estão aqui.** Ver `regra-fronteira-faixas.md` para o que fazer quando um projeto cai entre duas faixas.

---

## Regra transversal: terreno e metragem dimensionam etapas diferentes

Este é o critério mais importante do arquivo e o menos intuitivo. Veio do arquitetônico, mas afeta como qualquer dimensionamento deve ser montado.

| Variável | O que ela dimensiona |
|---|---|
| **Terreno** | Viabilidade do projeto e o pré-projeto |
| **Metragem** | Todas as demais etapas |

Consequência prática: um projeto com terreno complicado e metragem pequena pode ter pré-projeto longo e etapas seguintes curtas. Dimensionar o pré-projeto por metragem subestima; dimensionar as etapas seguintes por terreno superestima.

---

## Arquitetônico (ARQ)

**Fonte:** Isabela Lot (PO do ARQ e DI) — bench + planilha de validação oficial.

### Variáveis principais

- **Metragem**
- **Terreno**

### Faixas numéricas (planilha oficial)

| Etapa | Critério | Semanas |
|---|---|---|
| Planejamento de zoneamento (pré-projeto) | Cidade bem documentada / com precedente | 0,5 |
| | Cidade média sem precedente | 1 |
| | Cidade pequena mal documentada | 1 |
| | Zoneamento especial | 1,5+ ou **inviável** |
| Análise topográfica (pré-projeto) | Terreno plano | 0 |
| | Desnível 1:20 ou terreno >300m² | 0,5 |
| | Desnível até 1:2 ou terreno >700m² | 1 |
| | Desnível >1:1, ou terreno especial (rochoso, leito de rio, mar) | **inviável** |
| Estudo de Viabilidade / Programa de Necessidades | Projeto comum NCiv | 0,5 |
| | Cliente com ideias prontas convencionais | 0,5 |
| | Cliente com ideias prontas mirabolantes | 1 |
| Estudo Preliminar | Metragem <120m² ou com planta definida | 1 |
| | Metragem >120m² ou sem planta definida | 1,5 |
| | Metragem >200m² ou sobrado | 2 |
| | >300m² ou sobrado com piscina/subsolo/adicionais | 2,5 |
| Anteprojeto (modelagem no Revit — já com 0,5 de gordura embutida) | Mesmas 4 faixas acima | 2 / 2,5 / 3 / 3,5 |
| Renderização | Mesmas 4 faixas acima | 0,5 / 0,5 / 1 / 1 |
| Projeto Legal | Documentação exigida breve | 1 |
| | Documentação normal / casa mediana | 1 |
| | Documentação extensa / casa complexa | 2 |
| | Documentação extra/especial (ex: terreno em aclive) | 2,5 |

**Confirmado:** a topografia (ter ou não o levantamento, ou só imagem/localização exata) **não influencia** o dimensionamento do Anteprojeto/Revit. Seguir apenas a faixa única da planilha oficial (2-3,5 semanas), independente de haver planta prévia detalhada ou não. Ponto fechado — não há faixa separada para "com planta prévia".

### Variáveis secundárias

Todas apontam para a mesma consequência: **aprofundar o estudo de viabilidade**.

- **Cidade do lote** — muda legislação e exigências aplicáveis
- **Condomínio** — acrescenta camada de regras além da municipal
- **Proposta muito diferenciada pelo cliente** — quanto mais a proposta se afasta do usual, mais fundo o estudo de viabilidade precisa ir

### Critérios não-óbvios / restrições de escopo

- **Não fazem implantação de múltiplas edificações no mesmo terreno** (ex: condomínio com portaria + salão de festas + quadra + academia) — falta de know-how de traçado
- **Recusam projetos "exorbitantes"** (castelos, condomínios, casas milionárias de altíssimo padrão) — listado como critério de viabilidade na planilha oficial
- **Não fazem urbanismo, paisagismo, nem implantação de múltiplas unidades no terreno**
- **Critério real de inclinação é a necessidade de contenção**, não o grau isolado — ver tabela de Análise Topográfica acima; quando o terreno exige técnicas de contenção, entra como caso de viabilidade comprometida
- **DI (Design de Interiores) não dimensiona pontos hidráulicos e elétricos** — só indicação de posicionamento recomendado

### Falta levantar

- Nenhuma pendência aberta. "Proposta muito diferenciada" permanece intencionalmente como julgamento caso a caso, sem limiar numérico — decisão confirmada, não é lacuna.

---

## Design de Interiores (DI)

**Fonte:** planilha de validação oficial (aba separada do ARQ, mesma PO — Isabela Lot).

### Faixas numéricas

| Etapa | Critério | Semanas |
|---|---|---|
| Representação geométrica no Sketchup | 1 cômodo | 0,5 |
| | 2-4 cômodos ou até 100m² | 1 |
| | 5+ cômodos ou >100m² | 1,5 |
| Modelagem dos móveis | 1-5 móveis | 1,5 |
| | 5-10 móveis | 2,5 |
| | 10-15 móveis | 3 |
| | 15+ móveis | 3,5 |
| Paginação | 1 cômodo | 0,5 |
| | 2-4 cômodos ou até 50m² | 1 |
| | 5+ cômodos ou >50m² | 1,5 |
| Modelagem (por metragem) | 150-300m² | 2 |
| | 400-800m² | 3 |
| | 800-1000m² | 4 |
| | >1000m² | 4,5 ou **inviável** |
| Pranchas de Marcenaria e Marmoaria | 1-5 móveis | 1 |
| | 5-10 móveis | 1,5 |
| | 10-15 móveis | 2 |
| | 15+ móveis | 2,5 |
| Projeto luminotécnico | 1 cômodo | 0,5 |
| | 2-4 cômodos ou até 50m² | 1 |
| | 5+ cômodos ou >50m² | 1,5 |
| | Se pedir previsão de pontos hidro/elétrico | +1 semana |
| Caderno de Projetos | 1 cômodo | 0,5 |
| | 2-4 cômodos ou até 100m² | 1 |
| | 5+ cômodos ou >100m² | 1 |
| Renderização | 1 cômodo | 0,5 |
| | 2-4 cômodos | 1 |
| | 5+ cômodos | 1 |

**Restrição importante:** DI **não dimensiona pontos hidráulicos e elétricos** — só pode indicar posicionamento recomendado.

**Gargalo de capacitação (não numérico, mas crítico):** hoje só a Lot sabe fazer DI no Revit (a validação padrão é feita no Sketchup). Não existe processo formal de validação de DI no Revit ainda, e não há responsável definido para criar esse processo após a saída dela para CP.

---

## Estrutural (EST)

**Fonte:** Julia Lee ("Julee", PO do Estrutural) — bench + planilha de validação oficial. (Nota de correção: uma versão anterior deste arquivo atribuía o levantamento inicial do Estrutural a "Gabrielle Lobo" — na verdade os dados vieram da própria Julee, anotados por Gabrielle durante a conversa. Fonte real: Julee.)

### Variáveis principais

Base: **sobrado de 200m² = 5 semanas.** Ajustes somados a partir dessa base:

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

- **Piscina** — acrescenta **+1 semana**
- **Muro de arrimo** — o NCiv **nunca fez** estrutural de muro de arrimo internamente; não é uma variável de ajuste de prazo, é uma restrição de escopo (ver abaixo)

### Critérios não-óbvios

Geométricos, só visíveis olhando a planta — nenhum é dedutível a partir de metragem, endereço ou valor de contrato. Se a entrada não incluir a planta, o dimensionamento estrutural fica incompleto por definição:

- **Janelas muito grandes**
- **Paredes que não se alinham entre pavimentos**
- **Pé-direito muito alto**
- **Paredes inclinadas**
- **Encanamento no subsolo** — nunca vem informado nos cards; considerado importante mapear
- **Cômodos maiores que o padrão (~6x6m)** — ex: card recente com "garagem que ocupa o terreno inteiro"
- **Qualidade/origem da planta arquitetônica quando terceirizada** — plantas terceirizadas de baixa qualidade (paredes desalinhadas, medidas inconsistentes, subsolo menor que o terreno) são consideradas **não avaliáveis pela skill**; permanece como checagem manual mesmo com a skill implementada

### Restrições de escopo

- **Só trabalham com concreto armado** como solução estrutural própria (executada internamente)
- **Steel frame, tijolo ecológico e alvenaria estrutural não são executados internamente**, mas podem ser **terceirizados com o engenheiro parceiro Clau** — o dimensionamento desses sistemas não está mapeado neste arquivo; quem precisar dimensionar deve perguntar diretamente ao Clau, não usar as faixas de concreto armado acima
- **Muro de arrimo nunca foi feito internamente pelo Estrutural do NCiv** — tratar como fora do escopo padrão, não como ajuste de prazo
- **Inviáveis:** pavimentação (nunca aceitam, mesmo com leads de prefeitura/condomínio), edifícios muito altos, estruturas não convencionais, projetos de contenção de alta complexidade, infraestrutura urbana
- **⚠ Mudança recente registrada na planilha oficial:** elevador **saiu** da categoria "complexidade +1 semana" e passou para **inviável total** (não fazem). A planilha ainda mantém um texto de referência antigo que não foi corrigido — ao consultar versões antigas deste ou de outros documentos, desconsiderar qualquer menção a elevador como "+1 semana"

### Falta levantar

- Nenhuma pendência aberta neste momento.

---

## Elétrico (ELE)

**Fonte:** Paulinho (PO de Hidrossanitário e Elétrico) — bench + planilha de validação oficial.

### Variável principal

**Metragem**

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
| Cabeamento | **+1** (a maioria não sabe fazer, por isso o acréscimo é maior que os outros) |
| Reuso | +0,5 |
| Climatização | **não soma no Elétrico** — climatização é só Hidráulico (decisão confirmada em 30/09/2026) |
| Piscina | **não soma no Elétrico** — piscina é só Hidráulico (decisão confirmada em 30/09/2026) |
| Gás | +0,5 |

**Exemplo real (planilha oficial):** casa de 300m² com todos os complementares = **6 semanas** no Elétrico.

### Variável secundária não-óbvia

**Tipo de aquecimento de água** — não é sobre ter ou não (quase toda casa tem), mas o tipo:
- Aquecimento a gás (mais comum) — menor impacto no dimensionamento elétrico
- Aquecimento elétrico de passagem (ex: chuveiro elétrico tipo Lorenzetti) — maior consumo de energia, exige mais atenção, especialmente em casas menores com pouca folga de carga elétrica

Esta variável **não está na planilha oficial** ainda — só foi levantada na bench com o Paulinho. Pode explicar parte da diferença de acurácia observada entre Hidráulico (87%) e Elétrico (71%) nos testes já feitos.

### Restrições de escopo

- **Não fazem média tensão** (>75kW de carga instalada) — "não sabemos fazer e Francisco não pode assinar"
- **Não fazem instalação de elevador**

### Regras gerais de arredondamento (não são regra de fronteira — ver arquivo separado)

- Metragem quebrada dimensiona no limite superior (ex: 300m² é tratado como 400m²)
- Metragem desconhecida do cliente: se for casa térrea, estimar ~200m²
- Soma final quebrada arredonda para cima (ex: 3,5 → 4)

---

## Hidráulico (HID)

**Fonte:** Paulinho (mesmo PO do Elétrico) — bench + planilha de validação oficial.

### Variável principal

**Metragem** — mesma estrutura e mesmas faixas do Elétrico (Croqui + Predim + Dim + Doc; base até 200m² = 3 semanas; 200-400m² = 5 semanas).

### Complementares

Mesma tabela do Elétrico (fotovoltaico +0,5, cabeamento +1, reuso +0,5, gás +0,5), mais **climatização +0,5** e **piscina +0,5**, que no Instala só somam aqui no Hidráulico.

**Exemplo real (planilha oficial):** casa de 300m² com todos os complementares = **7 semanas** no Hidráulico (uma semana a mais que o Elétrico no mesmo cenário).

### Variável secundária não-óbvia

**Declive do terreno** — impacta o Hidráulico porque o esgoto escoa por gravidade. Se a casa fica em um nível **mais baixo** do que o ponto de coleta de esgoto, é necessário projetar uma **estação elevatória de esgoto** (equipamento que bombeia o esgoto para cima, contra a gravidade, até alcançar a coleta). Casos reais em que isso já aconteceu: o Farage precisou fazer isso no projeto "Sonho Palpável"; a Bel precisou no "Cuara".

**Impacto no prazo: +0,5 semana.**

Esta variável **não está na planilha oficial** ainda como campo formal do Hidráulico (a análise topográfica formal só existe na aba de ARQ) — mas já está confirmada e numerada aqui.

### Restrições de escopo

- **Não fazem poço** — componentes específicos não existem no builder
- **Não fazem climatização além de multi-split e cassete** — alinhar isso já na venda, ou simplesmente não vender esse item

### Restrição geral que envolve ambas Elétrico e Hidráulico

- **Reforma só é possível quando já existem as plantas estruturais, elétricas e hidrossanitárias** — no geral, "reforma" no núcleo significa fazer uma nova casa no mesmo terreno
- **DI + Instala vendidos sozinhos (sem ARQ) sempre deu problema** — se for vender assim, o escopo precisa estar muito bem definido em contrato
- **Residências multifamiliares:** não são sempre inviáveis, mas trazem limitações técnicas — fotovoltaico não atende a demanda de energia mais alta; padrão de entrada e hidrômetro são impeditivo técnico, mas o builder resolve

### Decisões confirmadas nos testes (30/09/2026)

Casos que a regra não cobria e foram decididos durante os testes do template v3:

- **Item "futuro" ou "só preparação"** (ex: preparação para painel solar, para piscina futura): dimensionar **como item completo do projeto**, com o acréscimo cheio do complementar. Não existe de fato uma "preparação" — o cliente executa usando o nosso projeto quando quiser.
- **Garagem entra na metragem** do Elétrico e do Hidráulico. Para o Elétrico faz sentido; para o Hidráulico é uma aproximação reconhecidamente ruim, mas ainda não há forma melhor de dimensionar.
- **Fossa séptica não soma prazo** no Hidráulico. Mesmo assim, **registrar na validação** se o projeto usa fossa — é informação útil para o projeto e evita perguntar de novo depois.
- **Piscina e climatização são só Hidráulico** — não somam no Elétrico, mesmo que o card cite esses itens no escopo do Elétrico (ver tabela de complementares do Elétrico).

### Falta levantar

- Incluir formalmente o campo "declive do terreno / necessidade de estação elevatória de esgoto" na planilha oficial do Hidráulico (hoje só está documentado aqui)

---

## GO

**Fonte:** planilha de validação oficial + bench com Heitor Tani (PO de GO).

### Variável principal

**Número de disciplinas contratadas** — não é dimensionado principalmente por metragem, ao contrário das outras disciplinas.

### Estrutura e faixas numéricas

Três etapas, cada uma com faixa mínima (~70m², todas as disciplinas) e máxima (~200m², todas as disciplinas):

| Etapa | Mínimo | Máximo |
|---|---|---|
| Quantificação | 2 semanas | 4 semanas |
| Orçamento | 3 semanas | 4 semanas |
| Planejamento | 2 semanas | 4 semanas |

**Teto do GO no total:** a soma Quantificação + Orçamento + Planejamento tem teto prático de **6-8 semanas** (confirmado por Heitor Taniguchi). Se a soma passar de 8, é sinal de erro na aplicação da regra, não um resultado válido — parar e marcar para revisão humana, com comentário de duas linhas. **Nunca apresentar total de GO acima de 8 semanas como resultado** (nem na tabela-resumo, nem no detalhe da disciplina): mostrar `🚩 em revisão` e colocar os valores por etapa só em Observações, marcados como "não válidos".

### Pontos de atenção por etapa (todos da planilha oficial)

**Quantificação** — dividida em duas partes: colocar os elementos modelados na EAP proposta, depois criar regras de extração do que não será modelado mas será quantificado. Aqui **o que pesa é a disciplina, não o tamanho**:
- Estrutural: regras de extração ensinadas no treinamento, não muda com tamanho — impacto **baixo**
- Instala: ainda muito manual/automático, segue método do treinamento (deve evoluir, mas não tão cedo) — impacto **baixo**
- **ARQ é o que "manda"**: o mais perigoso, costuma vir modelado com menos informação, itens perdidos que precisam ser garimpados na mão, **define o prazo da etapa** — impacto **alto**
- Disciplina modelada por terceiros (não pela própria equipe): **+1 semana por padrão**, exceto se vier do Iberque ou do Builder

**Orçamento:**
- Só pode usar a **SINAPI** para orçar — não representa bem padrão alto, serve para baixo e médio padrão — impacto **crucial**
- **Instala é o que "manda"**: quanto maior o Instala, mais itens associados a orçar, e são itens ruins de orçar — impacto **alto**
- Disciplinas complementares no Instala (fotovoltaico, reuso, PCI, etc.) puxam o prazo pra cima: **+2 semanas com todas**
- Estrutural e ARQ: Estrutural é tranquilo; ARQ dá trabalho mas não muda muito o prazo final — impacto **baixo**
- Processo hoje é muito manual/braçal — já se estudou usar IA, mas ainda não foi confirmado o uso em produção

**Planejamento:**
- Diferente das outras etapas, **todas as disciplinas pesam praticamente igual**
- É a etapa que a equipe **menos domina** — reconhecidamente um risco
- Tem **comportamento linear**: prazo cresce proporcional ao tamanho do projeto
- Teto prático: 4 semanas já é bastante; 6 semanas é considerado muito

### Pendências oficialmente registradas como "A CONFIRMAR" na planilha

- **Divergência de metragem mínima:** a planilha registra 70m² como mínimo, mas um áudio de quantificação cita 100m². Ainda não definido qual vale.
- **De onde vem a trava de metragem:** acima do limite, é o **Instala** que barra o projeto, não o GO propriamente — mas isso ainda não foi formalizado. A skill não deve concluir inviabilidade por metragem no GO sozinha.
- **Como as etapas se combinam frente ao teto de 8 semanas:** somando as faixas acima, o mínimo já dá 7 semanas (~70m²) e o máximo 12 (~200m²) — qualquer projeto acima de ~100m² com as três etapas ultrapassa o teto. Não está definido se as etapas se sobrepõem (e quanto) ou se as faixas por etapa precisam ser revistas. Até confirmar com o Heitor, a skill não compensa sozinha: todo GO acima de 8 vai para revisão humana.
- **Trecho de áudio inaudível** sobre planejamento, com números não confirmados ("...m² é duas semanas, 144, 210, talvez seis") — não foi transcrito para não inventar número.

---

## Lacunas que valem para todo o arquivo

**As faixas ainda não podem ser plenamente calibradas contra o histórico.** A base de projetos passados tem pouquíssimo preenchimento de área construída e endereço (situação registrada em levantamento anterior: 2 de 346 projetos com área construída, endereço em nenhum). Os números usados aqui vêm da planilha oficial e das bench, não de regressão sobre o histórico — a validação continua sendo prospectiva.

**Sobre "todos os critérios são óbvios".** Quando um especialista responde isso, normalmente significa que o conhecimento está automatizado, não que seja compartilhado. Perguntas abstratas do tipo "existem critérios não-óbvios?" não extraem esse tipo de conhecimento. As que funcionam são ancoradas em caso concreto:

- Me dá dois projetos que você dimensionou, um que ficou certo e um que estourou. O que você olhou em cada um?
- Se eu te der só a metragem, você consegue cravar as semanas? Que número você usa de cabeça?
- Quanto muda se tiver piscina? E muro de arrimo?
- Que erro um consultor novo comete quando dimensiona isso sozinho?
- Já teve caso em que a metragem enganou — projeto pequeno que deu muito mais trabalho?

---

## Registro das fontes

| Data | Fonte | Disciplina | O que trouxe |
|---|---|---|---|
| 03/09/2026 | Julia Lee ("Julee") | Estrutural | 5 variáveis principais, estruturas especiais, 4 dificuldades de planta (anotado por Gabrielle Lobo durante a conversa — atribuição corrigida) |
| 03/09/2026 | Isabela Lot | Arquitetônico | Distinção terreno / metragem por etapa, 3 variáveis secundárias |
| — | Paulinho | Elétrico / Hidráulico | Tipo de aquecimento de água, declive do terreno, faixas numéricas, complementares |
| — | Julia Lee ("Julee") | Estrutural (bench formal) | Concreto armado, steel frame, encanamento no subsolo, cômodos >6x6m, qualidade de planta terceirizada |
| — | Heitor Tani | GO | Pontos de atenção por etapa, pendências "a confirmar" |
| — | Planilha de validação oficial (Google Sheets, versão com alterações da Lot) | Todas | Faixas numéricas de ARQ, DI, Estrutural, Elétrico, Hidráulico, GO |
