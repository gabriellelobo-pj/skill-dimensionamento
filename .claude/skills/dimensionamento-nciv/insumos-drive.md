# Insumos do terreno na pasta do Drive

Como localizar a pasta do cliente, ler o que tem dentro e preencher os campos de terreno da validação. Ler sempre que a validação trouxer link do Drive ou nome de cliente, **antes** de preencher os campos de terreno.

---

## Passo 1 — Localizar a pasta e listar o conteúdo

Na ordem. Só passa ao item seguinte se o anterior não resolver.

**1.1 Abrir o link.** O campo `Drive:` traz o link da pasta do cliente. É sempre a primeira tentativa; não buscar nada antes.

**1.2 Conferir se é a pasta certa** (comparar o nome da pasta com o campo `Cliente:`) antes de ler qualquer arquivo.
- Segue em frente quando: o nome bate com o cliente; ou o link caiu numa subpasta do cliente (`Terreno`, `Documentos`, `Fotos`) — subir um nível, confirmar o nome da pasta pai e seguir.
- Vai para 1.3 quando: a pasta é de outro cliente; o link caiu numa pasta genérica (ex: `Clientes`) ou na raiz do Drive; o link não abre, expirou ou não tem permissão; o campo `Drive:` está vazio ou `não informado`.
- Nunca ler arquivos de uma pasta cujo dono não foi confirmado.

**1.3 Buscar a pasta pelo nome do cliente** (uma pasta por cliente; buscar pelo valor de `Cliente:`). Tolerar variações: ordem invertida (`Franco, Rodrigo`), sem acento, sobrenome abreviado, hífen/underline no lugar de espaço, nome da empresa em vez da pessoa.
- **Mais de uma pasta corresponde:** não escolher. Registrar as candidatas e sinalizar para o responsável (ler a pasta errada é pior que não ler nenhuma).
- **Nenhuma corresponde:** registrar `pasta não localizada` e seguir com o que o analista declarou. Não concluir que o cliente está sem insumos — a pasta pode existir com outro nome.

**1.4 Registrar quando o link falhou.** Se chegou à busca porque o link não serviu, o link da mensagem está errado e precisa ser corrigido na origem (senão o erro se repete na próxima validação):

```
Link do Drive não serviu: [o que aconteceu]. Pasta localizada pela busca: [nome].
```

**1.5 Listar, não buscar dentro da pasta.** Confirmada a pasta, enumerar o conteúdo dela e das subpastas. Não usar busca por nome nem por tipo de arquivo: há relato de que a busca do conector não retorna arquivos não nativos do Google, o que faria fotos e PDFs sumirem em silêncio. Navegar pela pasta contorna isso. Confirmar no teste.

**1.6 Aprovação.** Por padrão o conector pede aprovação a cada ação. Para fluxo contínuo, verificar antes a configuração da conta.

---

## Passo 2 — Descartar sem abrir

Gravações de reunião ficam misturadas com os insumos. Não abrir (pesadas, consomem contexto, não dizem nada sobre o terreno). Descartar por extensão: `.mp4`, `.mov`, `.avi`, `.m4a`, `.mp3`, `.wav`.

Exceção: **transcrição em texto** da reunião não é gravação e pode preencher lacunas de outros campos. Não usar para campos de terreno.

---

## Passo 3 — Classificar o que sobrou

Por extensão e conteúdo, não por nome de arquivo (`IMG_2847.jpg` é o caso normal).

| Tipo | Como reconhecer | O que extrair | O que **não** concluir |
|---|---|---|---|
| Foto do terreno | `.jpg`, `.png`, `.heic`, sem estrutura de prancha | Leitura qualitativa (passo 4) | Nenhum valor numérico |
| Levantamento em PDF | PDF com curvas de nível, cotas, quadro de áreas, RN | Cotas, área, perímetro, desnível se estiver escrito | Não inferir declividade medindo a imagem da prancha |
| Levantamento em DXF | `.dxf` | Cotas e polilinhas, se a leitura funcionar | — |
| Levantamento em DWG | `.dwg` | **Nada.** Formato binário, não há texto para extrair | Não tratar como ausente (ver abaixo) |
| Matrícula | PDF de cartório | Área do terreno, dimensões, confrontantes | Não confundir área de matrícula com área útil |
| Croqui | `.jpg` ou PDF desenhado à mão | Disposição pretendida dos cômodos | Nada sobre terreno |
| Planta anterior | PDF ou DWG de projeto | Metragem construída, pavimentos | — |

**DWG presente ≠ levantamento ausente.** Com DWG na pasta, o levantamento **existe**, só não é legível aqui (a distinção muda o que o time faz a seguir). Registrar: `levantamento existe em DWG, ilegível, pedir DXF ou PDF ao topógrafo`. Nunca escrever "sem levantamento" quando houver DWG.

---

## Passo 4 — Leitura de foto

**Foto não mede inclinação.** A planilha classifica topografia em `plano`, `1:20`, `até 1:2` e `maior que 1:1` — proporções medidas; nenhuma pode sair de foto.

**Proibido:** produzir proporção, porcentagem ou desnível em metros a partir de imagem. Estimativa numérica com cara de medição contamina o dimensionamento e é pior que campo vazio.

**Vocabulário permitido (só este)**, sempre com a marcação de origem (passo 5):
- `aparentemente plano`
- `declive visível`
- `declive acentuado`
- `não dá para dizer pela foto`

**O que a foto serve para flagrar:**
- afloramento rochoso
- curso d'água, alagamento, vegetação de várzea
- muro de arrimo ou contenção existente
- construção vizinha colada
- infraestrutura na rua: poste, guia, pavimento
- terreno ocupado quando foi declarado vago

Os três primeiros encostam no critério de inviabilidade da planilha (`rochoso, leito de rio, mar`) → **sinalizar para revisão humana**. A skill não declara inviabilidade sozinha (igual à regra de fronteira).

---

## Passo 5 — Marcar a origem de cada dado

Todo campo de terreno preenchido a partir da pasta leva a origem entre parênteses (quem revisa precisa saber se foi medido ou olhado). Sem origem, o dado não entra.

```
Inclinação: declive visível (origem: foto, estimativa visual)
Inclinação: desnível de 1,8m em 24m, cerca de 1:13 (origem: levantamento em PDF)
Área: 293 m² (origem: matrícula)
```

---

## Passo 6 — Conferir contra o que o analista declarou

O campo `Levantamento:` é preenchido pelo analista, que pode não ter conferido a pasta. Se declarado e encontrado divergirem, registrar os dois — não corrigir em silêncio.

```
Divergência: analista declarou "topográfico no Drive", pasta tem só fotos.
```

---

## Passo 7 — O que escrever de volta

Duas linhas (mesmo padrão da regra de fronteira): o que foi encontrado, depois o que falta.

```
INSUMOS: [o que a pasta tem, por tipo]
Faltando: [o que a validação exigia e não está lá]
```

Exemplos:

```
INSUMOS: 6 fotos do terreno, matrícula em PDF, levantamento em DWG (ilegível).
Faltando: levantamento em formato legível — pedir DXF ou PDF ao topógrafo.

INSUMOS: pasta acessível, só gravações de reunião.
Faltando: qualquer registro do terreno — nem foto nem levantamento.

INSUMOS: levantamento em PDF com cotas, 4 fotos.
Faltando: nada.
```

Pasta não localizada ou não abriu → `INSUMOS: pasta não localizada.` (ausência explícita, como os campos vazios do template).

---

## Quando parar e sinalizar

A skill não decide; registra e passa para o responsável quando:
- mais de uma pasta corresponde ao nome do cliente
- o link do campo `Drive:` não serviu e a pasta teve de ser localizada por busca
- foto sugere terreno especial (rocha, água, várzea)
- há divergência entre o declarado e o encontrado
- o levantamento existe mas só em DWG
- a pasta está acessível e completamente vazia de insumos

---

## Pendente de teste

Ainda não confirmado. Tratar cada item como incerto e não silenciar falha.

- **Leitura de imagem solta.** A documentação lista imagens entre os formatos legíveis, mas diz que a extração é só de texto. Se funcionar, o passo 4 vale como está. Se não, a foto conta só como presença na pasta e a inclinação fica com o que o analista declarou.
- **Leitura de `.dxf`.** Não testada.
- **Enumeração da pasta.** Confirmar que listar o conteúdo devolve arquivos não nativos do Google. Lista vazia numa pasta que sabidamente tem fotos = problema do conector, não da pasta — não registrar como ausência de insumos.
