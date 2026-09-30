# Insumos do terreno na pasta do Drive

Regras para localizar a pasta do cliente, ler o que tem dentro e preencher os campos de terreno da validação.

Ponteiro no `SKILL.md`: ler este arquivo sempre que a validação trouxer link do Drive ou nome de cliente, antes de preencher os campos de terreno.

---

## Passo 1 — Localizar a pasta e listar o conteúdo

Na ordem abaixo. Só passa para o item seguinte se o anterior não resolver.

### 1.1 Abrir o link

O campo `Drive:` da mensagem traz o link da pasta do cliente. É o caminho normal e sempre a primeira tentativa. Não buscar nada antes de tentar o link.

### 1.2 Conferir se é a pasta certa

Abrir o link não é o mesmo que estar no lugar certo. Antes de ler qualquer arquivo, comparar o nome da pasta com o campo `Cliente:` da mensagem.

**Segue em frente quando:**

- o nome da pasta bate com o cliente
- o link caiu numa subpasta do cliente (`Terreno`, `Documentos`, `Fotos`) — subir um nível, confirmar o nome da pasta pai e seguir

**Vai para 1.3 quando:**

- a pasta é de outro cliente
- o link caiu numa pasta genérica, como `Clientes`, ou na raiz do Drive
- o link não abre, expirou ou não tem permissão
- o campo `Drive:` está vazio ou com `não informado`

Nunca ler arquivos de uma pasta cujo dono não foi confirmado.

### 1.3 Buscar a pasta pelo nome do cliente

As pastas são organizadas uma por cliente. Buscar pelo valor do campo `Cliente:`.

A busca precisa tolerar as variações normais: ordem invertida (`Franco, Rodrigo`), ausência de acento, sobrenome abreviado, hífen ou underline no lugar de espaço, nome da empresa em vez do nome da pessoa.

**Mais de uma pasta correspondendo:** não escolher. Registrar as candidatas e sinalizar para o responsável. Ler a pasta do cliente errado é pior que não ler nenhuma.

**Nenhuma pasta correspondendo:** registrar `pasta não localizada` e seguir com o que o analista declarou. Não concluir que o cliente está sem insumos — a pasta pode existir com outro nome.

### 1.4 Registrar quando o link falhou

Se chegou até a busca porque o link não serviu, isso não é detalhe interno: o link da mensagem está errado e alguém precisa corrigir na origem, senão o erro se repete na próxima validação.

```
Link do Drive não serviu: [o que aconteceu]. Pasta localizada pela busca: [nome].
```

### 1.5 Listar, não buscar dentro da pasta

Uma vez confirmada a pasta, enumerar o conteúdo dela e das subpastas. Não usar busca por nome de arquivo nem por tipo: há relato de que a busca do conector não retorna arquivos que não são nativos do Google, o que faria fotos e PDFs sumirem em silêncio, como se a pasta estivesse vazia. Navegar pela pasta contorna isso. Confirmar no teste.

### 1.6 Aprovação

Por padrão o conector pede aprovação a cada ação. Se a skill for rodar em fluxo contínuo, verificar antes a configuração da conta.

---

## Passo 2 — Descartar o que não interessa, sem abrir

As pastas têm gravações de reunião misturadas com os insumos. Elas não entram nesta análise e não devem ser abertas: são pesadas, consomem contexto e não dizem nada sobre o terreno.

Descartar por extensão: `.mp4`, `.mov`, `.avi`, `.m4a`, `.mp3`, `.wav`.

Exceção: se houver **transcrição em texto** da reunião, ela não é gravação e pode ser útil para preencher lacunas de outros campos. Não usar para campos de terreno.

---

## Passo 3 — Classificar o que sobrou

Classificar por extensão e conteúdo, não por nome de arquivo. Nomes como `IMG_2847.jpg` são o caso normal, não a exceção.

| Tipo | Como reconhecer | O que extrair | O que **não** concluir |
|---|---|---|---|
| Foto do terreno | `.jpg`, `.png`, `.heic`, sem estrutura de prancha | Leitura qualitativa (passo 4) | Nenhum valor numérico |
| Levantamento em PDF | PDF com curvas de nível, cotas, quadro de áreas, RN | Cotas, área, perímetro, desnível se estiver escrito | Não inferir declividade medindo a imagem da prancha |
| Levantamento em DXF | `.dxf` | Cotas e polilinhas, se a leitura funcionar | — |
| Levantamento em DWG | `.dwg` | **Nada.** Formato binário, não há texto para extrair | Não tratar como ausente (ver abaixo) |
| Matrícula | PDF de cartório | Área do terreno, dimensões, confrontantes | Não confundir área de matrícula com área útil |
| Croqui | `.jpg` ou PDF desenhado à mão | Disposição pretendida dos cômodos | Nada sobre terreno |
| Planta anterior | PDF ou DWG de projeto | Metragem construída, pavimentos | — |

### DWG presente não é levantamento ausente

Se houver DWG na pasta, o levantamento **existe** — só não é legível por aqui. Isso é diferente de não ter levantamento, e a distinção muda o que o time faz a seguir.

Registrar como: `levantamento existe em DWG, ilegível, pedir DXF ou PDF ao topógrafo`.

Nunca escrever "sem levantamento" quando houver DWG na pasta.

---

## Passo 4 — Regras de leitura de foto

**Foto não mede inclinação.** A planilha classifica topografia em `plano`, `1:20`, `até 1:2` e `maior que 1:1`. São proporções medidas. Nenhuma delas pode sair de uma foto.

**Proibido:** produzir qualquer proporção, porcentagem ou desnível em metros a partir de imagem. Uma estimativa numérica com aparência de medição contamina o dimensionamento e é pior que campo vazio.

**Vocabulário permitido**, e só ele:

- `aparentemente plano`
- `declive visível`
- `declive acentuado`
- `não dá para dizer pela foto`

Sempre acompanhado da marcação de origem (passo 5).

**O que a foto serve para flagrar**, e aqui ela é útil:

- afloramento rochoso
- curso d'água, alagamento, vegetação de várzea
- muro de arrimo ou contenção existente
- construção vizinha colada
- infraestrutura na rua: poste, guia, pavimento
- terreno ocupado quando foi declarado vago

Os três primeiros encostam no critério de inviabilidade da planilha (`rochoso, leito de rio, mar`). Quando aparecerem, **sinalizar para revisão humana**. A skill não declara inviabilidade sozinha, do mesmo jeito que na regra de fronteira.

---

## Passo 5 — Marcar a origem de cada dado

Todo campo de terreno preenchido a partir da pasta leva a origem entre parênteses. Quem revisa precisa saber se o número foi medido ou olhado.

```
Inclinação: declive visível (origem: foto, estimativa visual)
Inclinação: desnível de 1,8m em 24m, cerca de 1:13 (origem: levantamento em PDF)
Área: 293 m² (origem: matrícula)
```

Sem a origem, o dado não entra.

---

## Passo 6 — Conferir contra o que o analista declarou

O campo `Levantamento:` da mensagem é preenchido pelo analista, que pode não ter conferido a pasta.

Se o declarado e o encontrado divergirem, registrar os dois. Não corrigir em silêncio.

```
Divergência: analista declarou "topográfico no Drive", pasta tem só fotos.
```

---

## Passo 7 — O que escrever de volta

Duas linhas, no mesmo padrão da regra de fronteira: a primeira diz o que foi encontrado, a segunda o que falta.

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

Se a pasta não foi localizada ou não abriu, escrever `INSUMOS: pasta não localizada.` A ausência precisa ser explícita, do mesmo jeito que os campos vazios do template.

---

## Quando parar e sinalizar

- mais de uma pasta corresponde ao nome do cliente
- o link do campo `Drive:` não serviu e a pasta teve de ser localizada por busca
- foto sugere terreno especial (rocha, água, várzea)
- divergência entre o declarado e o encontrado
- levantamento existe mas só em DWG
- pasta acessível e completamente vazia de insumos

Nesses casos a skill não decide: registra e passa para o responsável.

---

## Pendente de teste

Três coisas ainda não confirmadas. Enquanto isso, a skill deve tratar cada uma como incerta e não silenciar falha.

- **Leitura de imagem solta.** A documentação lista imagens entre os formatos legíveis, mas também diz que a extração é só de texto. Se funcionar, o passo 4 vale como está. Se não, a foto conta apenas como presença na pasta, e a inclinação fica com o que o analista declarou.
- **Leitura de `.dxf`.** Não testada.
- **Enumeração da pasta.** Confirmar que listar o conteúdo devolve arquivos não nativos do Google. Se a lista vier vazia numa pasta que sabidamente tem fotos, o problema é do conector e não da pasta — não registrar como ausência de insumos.
