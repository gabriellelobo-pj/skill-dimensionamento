# Regra de desempate — projetos na fronteira entre faixas

Vale quando o projeto não cai claramente em uma faixa. Não substitui o dimensionamento: só resolve o empate, e sempre deixa rastro para a revisão do PO.

## Direção padrão por disciplina

Não existe regra única de "subir de faixa". Identifique a disciplina e a direção dela **antes** de qualquer passo. Os passos dizem *como* ajustar; a direção vem desta tabela.

| Disciplina | Direção padrão | Fonte |
|---|---|---|
| **ARQ** | Para **baixo** (nunca abaixo de 6 semanas) | Isabela Lot |
| **ELE / HID** | Para **cima**, a partir de ~160-170m² (valor aproximado, não confirmado com precisão) | Paulinho |
| **EST** | Para **cima** | Julia Lee ("Julee") |
| **GO** | Não se aplica: só dois pontos-âncora (70m² e 200m²), tratado por interpolação (tipo 7) | Planilha oficial |

## Ordem de decisão

Sempre nesta ordem. Só passe ao seguinte se o anterior não resolver.

**Passo 1 — Precedente na base.** Procure caso parecido já dimensionado: mesma disciplina, metragem próxima, mesma condição de terreno e tipo de edificação. Se achar, use o prazo do precedente no lugar da faixa e registre qual projeto foi usado (precedente é medição, faixa é aproximação). Base vazia ou sem nada comparável: passo 2. Não force um precedente distante.

**Passo 2 — Faixa inteira na direção padrão** da disciplina, registrando o movimento na observação.

**Passo 3 — Meio-termo de 0,5 semana** (somar ou subtrair, conforme a direção) em vez da faixa inteira. É alternativa ao passo 2, nunca os dois na mesma atividade. Também gera registro.
**EST (decisão fechada, Julee):** +0,5 é o padrão do EST em fronteira. Prefira o passo 3 ao 2 sempre que a margem for pequena (até 10% acima do limite).

**Passo 4 — Parar e marcar para revisão humana** nos casos dos Guardrails. A skill não decide, sinaliza.

## Passo 2 ou passo 3?

**Faixa inteira quando:**
- o salto custa 0,5 semana ou menos (já é o ajuste mínimo)
- o projeto atende à faixa por mais de um critério
- é buraco entre faixas ou limite exato não coberto (tipos 2 e 3): não há dúvida de direção, só falta de cobertura

**Meio-termo quando as duas condições valem:**
- o salto custa 1 semana ou mais, **e**
- o projeto encosta na faixa por um único critério e por margem pequena

Margem pequena = até 10% acima do limite (ou abaixo, no ARQ). 130m² contra o limite de 120m² é margem pequena; 200m² contra o mesmo limite não é.

## Tipos de fronteira conhecidos

| # | Situação | Onde aparece | O que fazer |
|---|---|---|---|
| 1 | Número exato em duas faixas | Móveis do DI: 5 está em `1-5` e `5-10`; idem 10 e 15. Pranchas de marcenaria e famílias do ARQ/GBE têm o mesmo desenho | Faixa na direção padrão, direto |
| 2 | Buraco entre faixas | Modelagem ARQ/GBE salta de `150-300m²` para `400-800m²`; nada cobre 350m² | Faixa acima do buraco, direto (sempre para cima: é cobertura, não arredondamento) |
| 3 | Limite exato não coberto | Estudo preliminar usa `<120m²` e `>120m²`; 120 exato não está em nenhuma. Idem 200 e 300 | Faixa na direção padrão, direto |
| 4 | Dois critérios da mesma célula discordam | Estudo preliminar: `<120m² ou com planta definida` contra `>120m² ou sem planta definida`; 150m² com planta definida cabe nas duas | Vale o critério mais alto, depois o teste passo 2 × passo 3 |
| 5 | Critérios de natureza diferente na mesma linha | Estudo preliminar mistura metragem com tipo (`>200m² ou sobrado`) | Vale o mais alto, mesmo teste |
| 6 | Linha sem critério | Modelagem no Revit, anteprojeto e renderização têm células de complexidade vazias | Herdar a coluna do Estudo preliminar e registrar que foi por herança |
| 7 | Só dois pontos, sem faixa | GO: âncoras 70m² e 200m² (o 70m² tem divergência, ver `regras/go.md`) | Interpolar e arredondar para cima em múltiplos de 0,5 |

## Guardrails

- **Mover de faixa nunca produz "Inviável".** Onde o topo é `1.5+ ou Inviável` (zoneamento) ou `4.5 ou Inviável` (modelagem ARQ/GBE), o movimento para e vira revisão humana. Regra automática não recusa lead.
- **Máximo duas movimentações por disciplina**, somando mudanças de faixa e acréscimos de 0,5. Na terceira, pare e marque a disciplina inteira para revisão. Isso impede a bola de neve.
- **Teto do EST (8-9 semanas)** e **elevador no EST (inviável direto, sem passo de fronteira):** ver `regras/est.md`.
- **Teto do GO (8 semanas):** ver `regras/go.md`.
- **Arredondamento não conta duas vezes.** Os arredondamentos da planilha (metragem quebrada no limite superior; soma final quebrada para cima, ver `regras/instala.md`) não são movimentação de faixa e não geram observação. Se a metragem já subiu por arredondamento, não mova a faixa de novo pelo mesmo motivo.
- **Freio de bom senso.** A planilha comenta que 6 e 7 semanas (casa de 300m² com todos os complementares) pode ser excessivo. Quando uma disciplina passar de 6 semanas só por acúmulo de complementares, prefira o passo 3 ao 2 e sinalize na observação.

## Comentário obrigatório

Todo ajuste desta regra (faixa, meio-termo, precedente ou parada) gera um comentário de **duas linhas** em Observações: a primeira diz onde mexeu e quanto, a segunda diz por quê.

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
Motivo: elevador é inviável direto no Estrutural, não é caso de fronteira.
```

Um comentário por ajuste, mesmo vários na mesma disciplina. Sem comentário, a decisão não foi tomada. Sem nenhum ajuste, escreva `Sem ajustes de fronteira.` (a ausência precisa ser explícita).

## Em aberto (sinalizar se o caso encostar)

- **Herança das linhas sem critério (tipo 6)** é inferência: assume-se que Revit, anteprojeto e renderização seguem o Estudo preliminar. Falta confirmação do time.
- **Pendências do GO** (metragem mínima 70 × 100m², trava de metragem do Instala): ver `regras/go.md`.
