# Insumos do terreno na pasta do Drive

Como localizar a pasta do cliente, ler o que tem dentro e preencher os campos de terreno da validação.

## Passo 1 — Localizar a pasta e listar o conteúdo

Na ordem. Só passe ao item seguinte se o anterior não resolver.

**1.1 Abrir o link.** O campo `Drive:` traz o link da pasta do cliente. É sempre a primeira tentativa; não busque nada antes.

**1.2 Conferir se é a pasta certa.** Antes de ler qualquer arquivo, compare o nome da pasta com o campo `Cliente:`.
- Segue em frente: o nome bate; ou o link caiu numa subpasta do cliente (`Terreno`, `Documentos`, `Fotos`), então suba um nível, confirme o nome da pasta pai e siga.
- Vai para 1.3: pasta de outro cliente; pasta genérica (`Clientes`) ou raiz do Drive; link que não abre, expirou ou sem permissão; campo `Drive:` vazio ou `não informado`.

Nunca leia arquivos de uma pasta cujo dono não foi confirmado.

**1.3 Buscar pelo nome do cliente.** As pastas são uma por cliente; busque pelo campo `Cliente:`, tolerando ordem invertida (`Franco, Rodrigo`), falta de acento, sobrenome abreviado, hífen ou underline no lugar de espaço, nome da empresa em vez da pessoa.
- **Mais de uma pasta corresponde:** não escolha. Registre as candidatas e sinalize. Ler a pasta do cliente errado é pior que não ler nenhuma.
- **Nenhuma corresponde:** registre `pasta não localizada` e siga com o que o analista declarou. Não conclua que o cliente está sem insumos: a pasta pode ter outro nome.

**1.4 Registrar quando o link falhou.** Se a pasta só foi achada pela busca, o link da mensagem está errado e precisa ser corrigido na origem:

```
Link do Drive não serviu: [o que aconteceu]. Pasta localizada pela busca: [nome].
```

**1.5 Listar, não buscar dentro da pasta.** Enumere o conteúdo da pasta e das subpastas. Não use busca por nome nem por tipo de arquivo: há relato de que a busca do conector não retorna arquivos não nativos do Google, e fotos e PDFs sumiriam em silêncio.

**1.6 Aprovação.** Por padrão o conector pede aprovação a cada ação. Para fluxo contínuo, verifique antes a configuração da conta.

## Passo 2 — Descartar gravações sem abrir

Gravações de reunião não entram: são pesadas, consomem contexto e não dizem nada do terreno. Descarte por extensão: `.mp4`, `.mov`, `.avi`, `.m4a`, `.mp3`, `.wav`.

Exceção: **transcrição em texto** da reunião pode ajudar a preencher outros campos, mas não os de terreno.

## Passo 3 — Classificar o que sobrou

Por extensão e conteúdo, não pelo nome (`IMG_2847.jpg` é o caso normal).

| Tipo | Como reconhecer | O que extrair | O que **não** concluir |
|---|---|---|---|
| Foto do terreno | `.jpg`, `.png`, `.heic`, sem estrutura de prancha | Leitura qualitativa (passo 4) | Nenhum valor numérico |
| Levantamento em PDF | Curvas de nível, cotas, quadro de áreas, RN | Cotas, área, perímetro, desnível se estiver escrito | Não inferir declividade medindo a imagem da prancha |
| Levantamento em DXF | `.dxf` | Cotas e polilinhas, se a leitura funcionar | — |
| Levantamento em DWG | `.dwg` | **Nada** (binário, sem texto) | Não tratar como ausente |
| Matrícula | PDF de cartório | Área do terreno, dimensões, confrontantes | Não confundir com área útil |
| Croqui | `.jpg` ou PDF desenhado à mão | Disposição pretendida dos cômodos | Nada sobre terreno |
| Planta anterior | PDF ou DWG de projeto | Metragem construída, pavimentos | — |

**DWG na pasta = levantamento existe**, só não é legível aqui. Registre `levantamento existe em DWG, ilegível, pedir DXF ou PDF ao topógrafo`. Nunca escreva "sem levantamento" com DWG na pasta.

## Passo 4 — Leitura de foto

**Foto não mede inclinação.** A planilha classifica topografia em `plano`, `1:20`, `até 1:2` e `maior que 1:1`, proporções medidas que não saem de foto. **Proibido** tirar proporção, porcentagem ou desnível em metros de imagem: estimativa com cara de medição contamina o dimensionamento e é pior que campo vazio.

**Vocabulário permitido**, só este, sempre com a origem (passo 5):
- `aparentemente plano`
- `declive visível`
- `declive acentuado`
- `não dá para dizer pela foto`

**A foto serve para flagrar:**
- afloramento rochoso
- curso d'água, alagamento, vegetação de várzea
- muro de arrimo ou contenção existente
- construção vizinha colada
- infraestrutura na rua: poste, guia, pavimento
- terreno ocupado quando foi declarado vago

Os três primeiros encostam no critério de inviabilidade (`rochoso, leito de rio, mar`): **sinalize para revisão humana**. A skill não declara inviabilidade sozinha.

## Passo 5 — Marcar a origem de cada dado

Todo campo de terreno vindo da pasta leva a origem entre parênteses. Sem origem, o dado não entra.

```
Inclinação: declive visível (origem: foto, estimativa visual)
Inclinação: desnível de 1,8m em 24m, cerca de 1:13 (origem: levantamento em PDF)
Área: 293 m² (origem: matrícula)
```

## Passo 6 — Conferir contra o que o analista declarou

O campo `Levantamento:` é do analista, que pode não ter conferido a pasta. Se divergir do encontrado, registre os dois; não corrija em silêncio.

```
Divergência: analista declarou "topográfico no Drive", pasta tem só fotos.
```

## Passo 7 — O que escrever de volta

Duas linhas: o que foi encontrado e o que falta.

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

Pasta não localizada ou que não abriu: `INSUMOS: pasta não localizada.` (a ausência precisa ser explícita).

## Quando parar e sinalizar

Registre e passe para o responsável quando:
- mais de uma pasta corresponde ao cliente
- o link do `Drive:` não serviu e a pasta veio da busca
- foto sugere terreno especial (rocha, água, várzea)
- o declarado diverge do encontrado
- o levantamento existe só em DWG
- a pasta está acessível e vazia de insumos

## Ainda não testado (trate como incerto, não silencie falha)

- **Imagem solta:** se a leitura não funcionar, a foto conta só como presença na pasta e a inclinação fica com o que o analista declarou.
- **`.dxf`:** leitura não testada.
- **Listagem da pasta:** se vier vazia numa pasta que sabidamente tem fotos, o problema é do conector, não registre como ausência de insumos.
