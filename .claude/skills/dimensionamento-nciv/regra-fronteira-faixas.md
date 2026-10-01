# Regra de desempate — projetos na fronteira entre faixas

Vale quando o projeto não cai claramente em uma faixa da planilha de dimensionamento. Não substitui o dimensionamento: resolve só o empate e sempre deixa rastro para a revisão do responsável.

---

## 1. Direção padrão por disciplina (conferir antes de qualquer passo)

Não existe regra única. Uma versão anterior assumia "sempre subir de faixa" — **está errado**. As bench com os POs confirmaram:

| Disciplina | Direção padrão na fronteira | Fonte |
|---|---|---|
| **ARQ** | Para **baixo** (nunca abaixo de 6 semanas) | Isabela Lot |
| **Elétrico / Hidráulico** | Para **cima**, a partir de ~160-170m² (valor aproximado, não confirmado com precisão) | Paulinho |
| **Estrutural** | Para **cima** | Julia Lee ("Julee") |
| **GO** | Não se aplica da mesma forma — só dois pontos-âncora (70m² e 200m²), tratado como interpolação (tipo 7 abaixo) | Planilha oficial |

**Antes de aplicar qualquer passo abaixo, identifique a disciplina e confirme a direção padrão dela nesta tabela.** Os passos dizem *como* ajustar (faixa inteira vs. meio-termo); a direção de partida (pra cima ou pra baixo) vem desta tabela, não é universal.

---

## 2. Ordem de decisão

Sempre nesta ordem. Só passa ao passo seguinte se o anterior não resolver.

**Passo 1 — Precedente na base.** Buscar caso parecido já dimensionado: mesma disciplina, metragem próxima, mesma condição de terreno, mesmo tipo de edificação. Se achar, usar o prazo do precedente no lugar da faixa e registrar qual projeto foi usado (precedente é medição, faixa é aproximação). Base vazia ou sem nada comparável → passo 2. Não forçar precedente distante.

**Passo 2 — Mover para a faixa na direção padrão** (cima para Elétrico/Hidráulico/Estrutural; baixo para ARQ). Registrar na observação.

**Passo 3 — Meio-termo de 0,5 semana** no lugar da faixa inteira (somar ou subtrair conforme a direção da disciplina). É **alternativa** ao passo 2, nunca acréscimo: nunca aplicar os dois na mesma atividade. Registrar na observação.
- **Estrutural — decisão fechada:** +0,5 semana é o padrão em fronteira (sugestão da Julia Lee confirmada). Preferir o passo 3 ao passo 2 sempre que valer a margem pequena (até 10% acima do limite).

**Passo 4 — Parar e marcar para revisão humana** nos casos dos Guardrails (seção 5). A skill não decide, sinaliza.

### Passo 2 ou passo 3?

**Faixa inteira (passo 2) quando qualquer um vale:**
- o salto custa 0,5 semana ou menos (já é o ajuste mínimo)
- o projeto atende à faixa correspondente por mais de um critério
- é buraco entre faixas ou limite exato não coberto (tipos 2 e 3 abaixo) — não há dúvida de direção, só falta de cobertura

**Meio-termo (passo 3) quando as duas valem:**
- o salto para a faixa correspondente custa 1 semana ou mais, **e**
- o projeto encosta nessa faixa por um único critério e por margem pequena

Margem pequena = até 10% acima (ou abaixo, no ARQ) do limite. 130m² contra limite de 120m² é margem pequena; 200m² contra o mesmo limite não é.

---

## 3. Tipos de fronteira conhecidos

| # | Situação | Onde aparece | O que fazer |
|---|---|---|---|
| 1 | Número exato pertence a duas faixas | Móveis do DI: 5 está em `1-5` e em `5-10`; idem 10 e 15. Pranchas de marcenaria e famílias do ARQ/GBE têm o mesmo desenho | Faixa na direção padrão da disciplina, direto |
| 2 | Buraco entre faixas | Modelagem ARQ/GBE salta de `150-300m²` para `400-800m²`; nada cobre 350m² | Faixa acima do buraco, direto (sempre "pra cima": é cobertura, não direção de arredondamento) |
| 3 | Limite exato não coberto | Estudo preliminar usa `<120m²` e `>120m²`; 120 exato não está em nenhum. Mesmo caso em 200 e 300 | Faixa correspondente na direção padrão da disciplina, direto |
| 4 | Dois critérios da mesma célula discordam | Estudo preliminar: `<120m² ou com planta definida` contra `>120m² ou sem planta definida`. Casa de 150m² com planta definida se encaixa nas duas | Vale o critério que aponta mais alto, depois aplicar o teste passo 2 vs. passo 3 |
| 5 | Critérios de natureza diferente na mesma linha | Ex: Estudo preliminar mistura metragem com tipo (`>200m² ou sobrado`). *(Análise topográfica não entra mais aqui: desde 30/09/2026 só o desnível conta, a área do terreno não.)* | Vale o que aponta mais alto, mesmo teste |
| 6 | Linha sem critério nenhum | Modelagem no Revit, anteprojeto e renderização têm as células de complexidade vazias | Herdar a coluna em que o projeto caiu no Estudo preliminar e registrar que foi por herança |
| 7 | Sem faixa, só dois pontos | GO tem apenas 70m² e 200m² como âncoras (70m² tem divergência não resolvida — ver Guardrails) | Interpolar e arredondar para cima em múltiplos de 0,5 |

---

## 4. Comentário obrigatório

Toda vez que esta regra mexer no dimensionamento (movimentação de faixa, meio-termo, precedente ou parada para revisão), sai um comentário de **duas linhas** em Observações: a primeira diz onde mexeu e quanto; a segunda, por quê.

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

- Um comentário por ajuste, mesmo que sejam vários na mesma disciplina. Sem comentário, a decisão não foi tomada.
- Se a regra não mexeu em nada, escrever `Sem ajustes de fronteira.` (ausência explícita, como os campos vazios do template de validação).

---

## 5. Guardrails

- **Mover de faixa nunca produz "Inviável".** Onde o topo da tabela é `1.5+ ou Inviável` (planejamento de zoneamento) ou `4.5 ou Inviável` (modelagem ARQ/GBE), o movimento para e vira revisão humana. Regra automática não recusa lead.
- **Máximo duas movimentações por disciplina**, contando juntas mudanças de faixa e acréscimos de 0,5. Na terceira, parar de somar e marcar a disciplina inteira para revisão humana (impede a bola de neve).
- **Teto do Estrutural:** a planilha registra que dificilmente um projeto passa de 8 ou 9 semanas. Se o ajuste ultrapassar, parar e sinalizar.
- **Elevador no Estrutural é inviável direto, não caso de fronteira nem de ajuste.** Mudança recente na planilha oficial: saiu de "complexidade +1 semana" para "inviável total". Não aplicar nenhum passo acima — encaminhar direto para inviabilidade, sem revisão de fronteira.
- **Arredondamento não conta duas vezes.** A planilha já arredonda para cima em dois momentos que **não são** movimentação de faixa e não geram observação:
  - metragem quebrada dimensionada no limite superior — 300m² dimensiona como 400m²
  - soma final quebrada arredondada para cima — 3,5 vira 4

  Se a metragem já foi arredondada para cima, não aplicar movimentação de faixa de novo pelo mesmo motivo.
- **Freio de bom senso.** A planilha comenta, no exemplo da casa de 300m² com todos os complementares, que 6 e 7 semanas pode ser excessivo, e sugere mapear melhor os detalhes antes de somar tudo. Quando o total de uma disciplina passar de 6 semanas só por acúmulo de complementares, preferir o passo 3 ao passo 2 e sinalizar na observação.

---

## 6. Pontos ainda em aberto

A planilha não resolve e a skill não deve inventar. Caso que encostar em qualquer um → sinalizar para revisão humana.

- **Metragem mínima do GO.** Planilha oficial registra 70m²; um áudio da quantificação cita 100m². Ainda "a confirmar" na planilha. Projetos entre 70 e 100m² ficam sem chão até isso ser definido.
- **Herança das linhas sem critério (tipo 6).** É inferência: modelagem no Revit, anteprojeto e renderização não dizem por qual critério se classificam; assume-se que seguem o Estudo preliminar. Precisa de confirmação do time.
- **De onde vem a trava de metragem do GO.** Acima do limite quem barra é o **Instala**, não o GO — sinalizado como "a confirmar" na planilha, ainda não formalizado. A skill não conclui inviabilidade por metragem no GO sozinha.
