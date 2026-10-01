# Instala: Elétrico (ELE) e Hidráulico (HID)

**Fonte:** Paulinho (PO de ELE e HID), bench + planilha oficial.

## Base (igual para ELE e HID)

**Variável principal: metragem.** Estrutura: Croqui + Predim + Dim + Doc.

| Faixa | Total |
|---|---|
| Até 200m² | 3 semanas |
| 200-400m² | 5 semanas |
| >600m² | faixa aberta, caso a caso |

**Escala:** acima de 200m², cada 200m² adicionais soma +0,5 semana em cada etapa (Croqui, Predim, Dim, Doc).

**Arredondamento** (não é regra de fronteira):
- Metragem quebrada dimensiona no limite superior (300m² é tratado como 400m²)
- Metragem desconhecida em casa térrea: estimar ~200m²
- Soma final quebrada arredonda para cima (3,5 vira 4)

## Complementares (somam à base)

Some só os complementares pedidos para aquela disciplina no card. Exceção: piscina e climatização pedidas no ELE vão para o HID.

| Complementar | ELE | HID |
|---|---|---|
| Fotovoltaico | +0,5 | +0,5 |
| Cabeamento | **+1** (a maioria não sabe fazer) | +1 |
| Reuso | +0,5 | +0,5 |
| Gás | +0,5 | +0,5 |
| Climatização | **não soma** | +0,5 |
| Piscina | **não soma** | +0,5 |

**Piscina e climatização são só HID**, mesmo que o card cite esses itens no escopo do ELE (decisão de 30/09/2026).

**Exemplo real (planilha):** casa de 300m² com todos os complementares = **6 semanas no ELE** e **7 no HID**.

## Decisões confirmadas nos testes (30/09/2026)

- **Item "futuro" ou "só preparação"** (ex: preparação para painel solar, piscina futura): dimensionar como **item completo**, com o acréscimo cheio. Não existe "preparação": o cliente executa com o nosso projeto quando quiser.
- **Garagem:** já está na metragem do card, nunca somar (ver `gerais.md`).
- **Fossa séptica não soma prazo** no HID, mas **registre na validação** se o projeto usa fossa.

## Variáveis secundárias não-óbvias

Levantadas na bench, ainda fora da planilha oficial.

**ELE: tipo de aquecimento de água.** Quase toda casa tem; o que importa é o tipo:
- A gás (mais comum): menor impacto no ELE
- Elétrico de passagem (ex: chuveiro tipo Lorenzetti): mais consumo, exige atenção, principalmente em casas menores com pouca folga de carga

**HID: declive do terreno: +0,5 semana.** O esgoto escoa por gravidade. Se a casa fica **abaixo** do ponto de coleta, é preciso projetar uma **estação elevatória de esgoto** (equipamento que bombeia o esgoto para cima até a coleta). Já aconteceu no "Sonho Palpável" (Farage) e no "Cuara" (Bel).

## Restrições de escopo

- **ELE: não fazem média tensão** (>75kW de carga instalada): "não sabemos fazer e Francisco não pode assinar"
- **ELE: não fazem instalação de elevador**
- **HID: não fazem poço** (componentes não existem no builder)
- **HID: climatização só multi-split e cassete.** Alinhar na venda ou não vender o item.
- **Reforma** só com plantas estruturais, elétricas e hidrossanitárias existentes. No núcleo, "reforma" costuma ser uma casa nova no mesmo terreno.
- **DI + Instala vendidos sem ARQ sempre deu problema.** Se vender assim, o escopo precisa estar muito bem definido em contrato.
- **Multifamiliar:** nem sempre inviável, mas o fotovoltaico não atende a demanda maior de energia; padrão de entrada e hidrômetro são impeditivo técnico, mas o builder resolve.
