# Regra de desempate — projetos na fronteira entre faixas

Vale quando o projeto não cai claramente em uma faixa da planilha de dimensionamento. Não substitui o dimensionamento: resolve só o empate, e sempre deixa rastro para a revisão do responsável.

---

## ⚠ Direção padrão varia por disciplina — não existe regra única

Uma versão anterior deste arquivo assumia que a decisão em caso de fronteira era sempre "subir de faixa". **Isso está errado.** As bench com os POs confirmaram que cada disciplina tem uma direção-padrão diferente:

| Disciplina | Direção padrão em caso de fronteira | Fonte |
|---|---|---|
| **ARQ** | Para **baixo** (nunca abaixo de 6 semanas) | Isabela Lot |
| **Elétrico / Hidráulico** | Para **cima**, a partir de ~160-170m² (valor aproximado, não confirmado com precisão) | Paulinho |
| **Estrutural** | Para **cima** | Julia Lee ("Julee") |
| **GO** | Não se aplica da mesma forma — GO tem só dois pontos-âncora (70m² e 200m²), tratado como interpolação (ver tipo 7 na tabela abaixo) | Planilha oficial |

**Antes de aplicar qualquer passo abaixo, identifique a disciplina e confirme a direção padrão dela na tabela acima.** Os passos 1 a 3 abaixo descrevem *como* ajustar (subir faixa inteira vs. meio-termo), mas a direção de partida (pra cima ou pra baixo) vem desta tabela, não é universal.

---

## Ordem de decisão

Sempre nesta ordem. Só passa para o passo seguinte se o anterior não resolver.

### Passo 1 — Procurar precedente na base

Buscar na base de projetos já dimensionados um caso parecido: mesma disciplina, metragem próxima, mesma condição de terreno e mesmo tipo de edificação.

Se achar, usar o prazo do precedente no lugar da faixa e registrar qual projeto foi usado. Precedente real ganha da faixa, porque a faixa é uma aproximação e o precedente é medição.

Se a base estiver vazia ou não tiver nada comparável, seguir para o passo 2. Não forçar um precedente distante só para ter um.

### Passo 2 — Mover para a faixa na direção padrão da disciplina

Classificar na faixa na direção indicada pela tabela do início do arquivo (acima para Elétrico/Hidráulico/Estrutural; abaixo para ARQ) e registrar o movimento na observação.

### Passo 3 — Meio-termo (0,5 semana) no lugar da faixa inteira

Quando mover a faixa inteira for exagero, adicionar (ou subtrair, dependendo da direção da disciplina) 0,5 semana em vez de mudar de faixa. É alternativa ao passo 2, não acréscimo: nunca aplicar os dois na mesma atividade.

**Decisão confirmada para o Estrutural:** a Julia Lee sugeriu, na bench, usar este meio-termo (+0,5 semana) como padrão em vez de subir a faixa inteira nos casos de fronteira do Estrutural. Essa sugestão foi confirmada como decisão fechada — tratar +0,5 semana como o padrão do Estrutural em casos de fronteira, preferindo o passo 3 ao passo 2 sempre que a condição de margem pequena (até 10% acima do limite) se aplicar.

Também gera registro na observação.

### Passo 4 — Parar e marcar para revisão humana

Nos casos listados em Guardrails. A skill não decide, sinaliza.

---

## Como escolher entre o passo 2 e o passo 3

**Move a faixa inteira quando:**

- o salto custa 0,5 semana ou menos — já é o ajuste mínimo, não há o que economizar
- o projeto atende à faixa correspondente por mais de um critério
- é buraco entre faixas ou limite exato não coberto (tipos 2 e 3 da tabela abaixo), onde não existe dúvida de direção, só falta de cobertura

**Usa meio-termo (0,5 semana) quando as duas condições valerem:**

- o salto para a faixa correspondente custa 1 semana ou mais, **e**
- o projeto encosta nessa faixa por um único critério e por margem pequena

Margem pequena significa até 10% acima (ou abaixo, no caso do ARQ) do limite. Uma casa de 130m² contra o limite de 120m² é margem pequena. Uma de 200m² contra o mesmo limite não é.

---

## Tipos de fronteira conhecidos

| # | Situação | Onde aparece | O que fazer |
|---|---|---|---|
| 1 | Número exato pertence a duas faixas | Móveis do DI: 5 está em `1-5` e em `5-10`; idem 10 e 15. Pranchas de marcenaria e famílias do ARQ/GBE têm o mesmo desenho | Faixa na direção padrão da disciplina, direto |
| 2 | Buraco entre faixas | Modelagem ARQ/GBE salta de `150-300m²` para `400-800m²`; nada cobre 350m² | Faixa acima do buraco, direto (este tipo é sempre "pra cima" porque é sobre cobertura, não sobre direção de arredondamento) |
| 3 | Limite exato não coberto | Estudo preliminar usa `<120m²` e `>120m²`; 120 exato não está em nenhum. Mesmo caso em 200 e 300 | Faixa correspondente na direção padrão da disciplina, direto |
| 4 | Dois critérios da mesma célula discordam | Estudo preliminar: `<120m² ou com planta definida` contra `>120m² ou sem planta definida`. Casa de 150m² com planta definida se encaixa nas duas | Vale o critério que aponta mais alto, depois aplicar o teste do passo 2 contra o 3 |
| 5 | Critérios de natureza diferente na mesma linha | Ex: Estudo preliminar mistura metragem com tipo (`>200m² ou sobrado`). *(A Análise topográfica não entra mais aqui: desde 30/09/2026 só o desnível conta, a área do terreno não.)* | Vale o que aponta mais alto, mesmo teste |
| 6 | Linha sem critério nenhum | Modelagem no Revit, anteprojeto e renderização têm as células de complexidade vazias | Herdar a coluna em que o projeto caiu no Estudo preliminar, e registrar que foi por herança |
| 7 | Sem faixa, só dois pontos | GO tem apenas 70m² e 200m² como âncoras (valor de 70m² tem divergência não resolvida — ver Guardrails) | Interpolar e arredondar para cima em múltiplos de 0,5 |

---

## Guardrails

**Mover de faixa nunca produz "Inviável".** Onde o topo da tabela é `1.5+ ou Inviável` (planejamento de zoneamento) ou `4.5 ou Inviável` (modelagem ARQ/GBE), o movimento para e vira revisão humana. Uma regra automática não recusa lead.

**Máximo duas movimentações por disciplina.** Contam juntas as mudanças de faixa e os acréscimos de 0,5. Na terceira, parar de somar e marcar a disciplina inteira para revisão humana. É isso que impede a bola de neve.

**Teto do estrutural.** A planilha registra que dificilmente um projeto passa de 8 ou 9 semanas. Se o ajuste ultrapassar, parar e sinalizar.

**Elevador no Estrutural não é mais caso de fronteira nem de ajuste — é inviável direto.** Mudança recente registrada na planilha oficial: elevador saiu de "complexidade +1 semana" para "inviável total". Não aplicar nenhum dos passos acima quando o projeto envolver elevador no Estrutural — encaminhar direto para inviabilidade, sem revisão de fronteira.

**Arredondamento não conta duas vezes.** A planilha já arredonda para cima em dois momentos que **não são** movimentação de faixa e não geram observação:

- metragem quebrada dimensionada no limite superior — 300m² dimensiona como 400m²
- soma final quebrada arredondada para cima — 3,5 vira 4

Se a metragem já foi arredondada para cima, não aplicar movimentação de faixa de novo pelo mesmo motivo.

**Freio de bom senso.** A própria planilha comenta, no exemplo da casa de 300m² com todos os complementares, que 6 e 7 semanas pode ser excessivo, e sugere mapear melhor os detalhes antes de somar tudo. Quando o total de uma disciplina passar de 6 semanas só por acúmulo de complementares, preferir o passo 3 ao passo 2 e sinalizar na observação.

---

## Comentário obrigatório

Toda vez que esta regra mexer no dimensionamento — movimentação de faixa, meio-termo, precedente ou parada para revisão — sai um comentário de **duas linhas** no campo de observações da validação.

Primeira linha diz onde mexeu e quanto. Segunda linha diz por quê.

```
[DISCIPLINA] [atividade]: [valor de origem] → [valor final] ([+X ou -X] semana)
Motivo: [qual fronteira e por que a regra decidiu assim, incluindo a direção padrão da disciplina]
```

Exemplos:

```
ARQ estudo preliminar: 2,5 → 2 semanas (-0,5)
Motivo: 195m², perto do limite de 200m²; ARQ arredonda para baixo por padrão (Lot), sem evidência contrária (ex: fachada elaborada) que justificasse manter a faixa de cima.

ELE dimensionamento: 3 → 3,5 semanas (+0,5)
Motivo: 165m², perto do limite de 170m² onde compensa arredondar para cima; Elétrico/Hidráulico arredondam para cima por padrão (Paulinho).

EST tamanho da casa: 5 → 6 semanas (+1)
Motivo: precedente do projeto Guarulhos, 320m² em terreno inclinado, dimensionado em 6 semanas.

ARQ planejamento de zoneamento: parado, sem valor
Motivo: indício de zoneamento especial; a faixa de cima é inviável e a regra não decide inviabilidade.

EST elevador: parado, sem valor
Motivo: elevador é inviável direto no Estrutural (mudança recente), não é caso de fronteira.
```

Um comentário por ajuste, mesmo que sejam vários na mesma disciplina. Sem comentário, a decisão não foi tomada.

Se a regra não mexeu em nada, escrever `Sem ajustes de fronteira.` A ausência precisa ser explícita, do mesmo jeito que os campos vazios do template de validação.

---

## Pontos ainda em aberto

Três coisas que a planilha não resolve e que a skill não deve inventar. Quando o caso encostar em qualquer uma, sinalizar para revisão humana.

- **Metragem mínima do GO.** A planilha oficial registra 70m², mas um áudio da quantificação cita 100m². Ainda "a confirmar" na própria planilha. Projetos entre 70 e 100m² ficam sem chão até isso ser definido.
- **Herança das linhas sem critério.** A regra do tipo 6 é uma inferência: modelagem no Revit, anteprojeto e renderização não dizem por qual critério se classificam. Está sendo assumido que seguem o Estudo preliminar. Precisa de confirmação do time.
- **De onde vem a trava de metragem do GO.** Acima do limite quem barra é o **Instala**, não o GO — isso já está sinalizado como "a confirmar" na própria planilha oficial, mas ainda não foi formalizado. A skill não deve concluir inviabilidade por metragem no GO sozinha.
