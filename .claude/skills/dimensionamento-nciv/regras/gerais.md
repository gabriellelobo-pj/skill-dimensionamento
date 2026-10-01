# Regras gerais de dimensionamento

Valem para todas as disciplinas. O objetivo é raciocinar na mesma ordem e olhar as mesmas variáveis que um PO olharia.

## Regras de uso

1. **Não invente faixa nem número.** Caso não coberto pelos arquivos de regras: pergunte ao usuário em vez de estimar. Um dimensionamento inventado é pior que nenhum, porque parece calibrado.
2. **Identifique a etapa antes de escolher a variável.** No ARQ a variável principal muda conforme a etapa (ver abaixo).
3. **Percorra as três camadas na ordem:** variável principal, depois variáveis secundárias, depois critérios não-óbvios.
4. **Marque explicitamente o que não conseguiu avaliar.**
5. **Critério não-óbvio não registrado não significa que não exista.** O conhecimento dos POs costuma estar automatizado; na dúvida, sinalize.
6. **Arredondamento em fronteira** fica em `regra-fronteira-faixas.md`.

## Terreno e metragem dimensionam etapas diferentes

O critério mais importante e menos intuitivo. Veio do ARQ, mas afeta como qualquer dimensionamento é montado.

| Variável | O que dimensiona |
|---|---|
| **Terreno** | Viabilidade do projeto e pré-projeto |
| **Metragem** | Todas as demais etapas |

Terreno complicado com metragem pequena pode ter pré-projeto longo e etapas seguintes curtas. Dimensionar o pré-projeto por metragem subestima; dimensionar as etapas seguintes por terreno superestima.

## A metragem é a do card, e ela já inclui a garagem

Use a **área construída do card como está**. Para o NCiv a garagem é área construída, porque é modelada. **Nunca some a garagem por cima** (card diz 100 m² com garagem no térreo: dimensionar com 100 m², não 200 m²). A confusão vem da legislação, onde às vezes a garagem não é área computável; isso não vale aqui. (Lot, 30/09/2026; bate com o gabarito do Elétrico no mesmo caso.)

## Limite das faixas

As faixas vêm da planilha oficial e das bench com os POs, não de regressão sobre o histórico (a base antiga quase não tem área construída nem endereço). A validação continua prospectiva.
