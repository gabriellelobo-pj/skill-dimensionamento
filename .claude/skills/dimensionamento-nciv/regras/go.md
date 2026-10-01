# GO

**Fonte:** planilha oficial + bench com Heitor Taniguchi (PO de GO).

**Variável principal: número de disciplinas contratadas.** Ao contrário das outras disciplinas, não é principalmente metragem.

## Faixas

Três etapas. Mínimo ≈ 70m² com todas as disciplinas; máximo ≈ 200m² com todas. Entre os dois pontos, interpolar (tipo 7 de `regra-fronteira-faixas.md`).

| Etapa | Mínimo | Máximo |
|---|---|---|
| Quantificação | 2 semanas | 4 semanas |
| Orçamento | 3 semanas | 4 semanas |
| Planejamento | 2 semanas | 4 semanas |

## Teto de 8 semanas

Teto prático da soma Quantificação + Orçamento + Planejamento: **6-8 semanas** (confirmado pelo Heitor). Soma acima de 8 é sinal de erro na aplicação da regra, não resultado válido.

**Nunca apresente total de GO acima de 8 semanas**, nem na tabela-resumo nem no detalhe da disciplina. A linha do GO mostra `🚩 em revisão — soma das etapas passou do teto de 8 semanas`. Os valores por etapa que estouraram vão só em Observações, marcados como "não válidos", com comentário de duas linhas.

## Pontos de atenção por etapa (planilha oficial)

**Quantificação.** Duas partes: colocar os elementos modelados na EAP proposta e criar regras de extração do que não é modelado mas será quantificado. **Pesa a disciplina, não o tamanho:**
- EST: regras de extração do treinamento, não mudam com o tamanho. Impacto **baixo**.
- Instala: ainda muito manual/automático, segue o método do treinamento. Impacto **baixo**.
- **ARQ "manda" e define o prazo da etapa:** costuma vir modelado com menos informação, itens perdidos garimpados na mão. Impacto **alto**.
- Disciplina modelada por terceiros: **+1 semana**, exceto se vier do Iberque ou do Builder.

**Orçamento.**
- Só pode usar **SINAPI**, que não representa bem alto padrão (serve para baixo e médio). Impacto **crucial**.
- **Instala "manda":** quanto maior, mais itens ruins de orçar. Impacto **alto**.
- Complementares do Instala (fotovoltaico, reuso, PCI etc.) puxam o prazo: **+2 semanas com todas**.
- EST é tranquilo; ARQ dá trabalho mas muda pouco o prazo final. Impacto **baixo**.
- Processo muito manual; uso de IA estudado mas não confirmado em produção.

**Planejamento.**
- Todas as disciplinas pesam praticamente igual.
- Etapa que a equipe **menos domina**: risco reconhecido.
- **Linear:** o prazo cresce proporcional ao tamanho do projeto.
- 4 semanas já é bastante; 6 é considerado muito.

## Pendências "A CONFIRMAR" (não decidir sozinha)

- **Metragem mínima:** a planilha diz 70m², um áudio da quantificação cita 100m². Projetos entre 70 e 100m² ficam sem chão: sinalize.
- **Trava de metragem:** acima do limite quem barra é o **Instala**, não o GO, mas isso não foi formalizado. **Não conclua inviabilidade por metragem no GO.**
- **Etapas frente ao teto:** somando as faixas, o mínimo já dá 7 semanas (~70m²) e o máximo 12 (~200m²), então qualquer projeto acima de ~100m² com as três etapas passa do teto. Não está definido se as etapas se sobrepõem ou se as faixas serão revistas. Até o Heitor confirmar, não compense: todo GO acima de 8 vai para revisão humana.
- Um trecho de áudio inaudível sobre planejamento trazia números não confirmados; não foi usado.
