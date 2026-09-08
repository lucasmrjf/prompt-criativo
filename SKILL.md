---
name: prompt-criativo
description: Monta o prompt de geração de imagem (GPT por padrão; serve para Nano Banana, Midjourney) de um criativo estático a partir de copy JÁ PRONTA, da identidade visual do cliente e da foto fornecida. Não escreve copy. Use quando o usuário pedir "prompt pro GPT gerar o criativo", "prompt de imagem do anúncio", "estático pra rodar", para qualquer cliente.
---

# /prompt-criativo

Transforma copy aprovada + identidade do cliente + foto em um prompt de imagem pronto para colar. Nasceu em 07/09/2026 nos estáticos da masterclass do Thomáz (R+), depois de seis criativos validados com o mesmo molde.

## O que esta skill NÃO faz
- Não escreve nem "melhora" copy. Gancho, linha de apoio e CTA chegam prontos, saídos da `/roteiro-anuncio` (Etapa 2, por partes) e já passados pela `/limpa-ia`. Se a copy não existir, parar e rodar a `/roteiro-anuncio` primeiro. Nunca inventar uma frase para preencher o prompt.
- Não inventa paleta, fonte ou logo. Tudo vem da pasta de identidade do cliente.

## Etapa 1 · Insumos (ler antes de escrever)
1. **Cliente:** `clientes/<cliente>/contexto.md` (regras, termos proibidos, compliance) e a pasta `identidade-visual/` do produto ou evento (hex, fonte, logo). Se o produto tem identidade própria (ex.: Obesity & Genomics verde, Endohacking vermelho), usar a do produto, não a da marca-mãe.
2. **Copy pronta:** gancho (até 2 linhas, ~9 palavras), linha de apoio (até 12 palavras, ou nenhuma quando o gancho já fecha a ideia), rodapé fixo (data · hora · quem pode), texto do botão. Regra do Lucas (08/09/2026): estático é gancho e uma frase; o argumento vai na legenda, nunca na imagem. Anotar a linha Bastidores da copy para carregar na entrega.
3. **Foto:** qual arquivo, e o **regime**:
   - `intocada`: a IA não recorta, não recolore, não retoca; só enquadra. Layout dividido (foto no topo ~60% + painel de cor com o texto).
   - `composição livre` (padrão): rosto e corpo ficam como fotografados; a IA pode recortar, estender fundo, aplicar degradê, colocar texto sobre a imagem. Proibir explicitamente o layout dividido para as peças não saírem iguais.
   - `sem foto`: só tipografia sobre a paleta.
4. **Formato:** 1080x1350 (4:5, padrão feed), 1080x1920 (9:16, stories/reels: manter 250 px livres no topo e 340 px na base) ou 1080x1080.
5. **Ferramenta:** GPT por padrão. Instruções em inglês (obedece melhor ao layout), texto da peça em português entre aspas e marcado como verbatim.
6. **Logo:** a IA não reproduz logo. Reservar um canto limpo e aplicar depois (Canva/Figma). Nunca pedir para a IA desenhar logo, brasão ou nome de instituição.

Defaults quando o usuário não disser: 4:5, GPT, composição livre, logo depois.

## Etapa 2 · Montar o prompt (molde)
Blocos, nesta ordem. Trocar só o que está entre colchetes.

```
Create a static ad for Instagram/Facebook, [1080x1350 px (4:5)], built on top of the attached photo.

ABOUT THE PHOTO
[intocada] Do not alter the photo in any way: do not cut the person out, do not change colors, lighting, skin, face, clothes or scenery, no filters, no new person. The only allowed operation is framing it inside its reserved area, keeping the face whole and centered.
[composição livre] The person must stay exactly as photographed: do not retouch, redraw, regenerate or age the face, skin, hair, expression, body or clothes. Everything else is yours: crop, reframe, extend the background, cut the person out onto a new background, add gradients and color grading, place text over the image.

COMPOSITION
[intocada] Two areas: top ~60% the photo, full width, nothing over it; bottom ~40% a solid panel [HEX principal] with all the text. Clean straight transition, no gradient into the photo.
[composição livre] Do NOT use a "photo on top, text below" or "photo on one side, text on the other" layout. Integrate text over or around the photo. You may choose: full-bleed photo with a [HEX principal] gradient rising from the bottom; the person cut out on a [HEX principal] background with subtle grain and the headline partly behind or beside him/her; a tight dramatic crop with the headline stacked on the darker side. Editorial and sober, like [referência de tom do cliente: evento médico premium / escritório de advocacia / marca de luxo], never like a generic online-course ad. No decorative elements: [lista de clichês do nicho a proibir].

COLORS AND TYPE
Palette: [HEX principal], [HEX escuro], [HEX de destaque], [HEX do texto]. Typeface in the style of [fonte da identidade]. All text on an area dark/light enough to read on a phone; add a gradient behind text if needed. Minimum 70 px margin from the edges. [9:16: keep the top 250 px and bottom 340 px free of text.]

TEXT (Brazilian Portuguese, reproduce verbatim, character by character, including accents; do not translate, paraphrase, or add hyphens or dashes)
a) Small label, uppercase, wide letter spacing, [HEX destaque]: "[ETIQUETA]"
b) Headline, semibold, the largest text, two lines: "[LINHA 1]" / "[LINHA 2]" (render the words "[DESTAQUE]" in [HEX destaque])
c) Supporting line, smaller, light weight: "[APOIO]"
d) Footer line, small, uppercase, wide letter spacing: "[RODAPÉ]"
e) A discreet square-cornered button, background [HEX destaque], text [HEX escuro]: "[BOTÃO]"

LOGO
Leave one corner clear of text for the logo, which will be added later. Do not invent any logo, crest or institution name.

FINAL CHECK
The person's face and body are identical to the photo provided. All text readable on a phone. No words other than the ones listed. No spelling mistakes in Portuguese. [Compliance do nicho: ex. "No medication names, no pen injectors, syringes, pills or scales anywhere."]
Export the final image at exactly [1080x1350 px], no borders, no frame, no watermark.
```

## Etapa 3 · Checklist antes de entregar
- Todo texto em português dentro do prompt é idêntico à copy aprovada. Zero travessão, nenhum termo proibido do cliente (`/limpa-ia`).
- Hex e fonte vieram do arquivo de identidade, não de memória.
- Compliance do nicho no FINAL CHECK e na lista de elementos proibidos (médico: nada de remédio, seringa, caneta injetora, balança; advogado: nada de martelo, balança da justiça, toga; nutrição: nada de fita métrica, prato de salada). Sem depoimento, sem "antes e depois".
- Numa série, variar a composição sugerida entre as peças (degradê de base, recorte em fundo sólido, crop fechado) para não sair tudo igual.
- Destaque em cor só num trecho curto do gancho (2 a 4 palavras), o que carrega a dor ou a promessa.

## Etapa 4 · Entrega
1. Prompt em bloco de código, pronto para colar com a foto.
2. Uma linha **Ficha**: cliente · formato · regime da foto · paleta usada · foto (caminho).
3. A linha **Bastidores** da copy (vem da `/roteiro-anuncio`; sem ela, a copy não passou pelo processo).
4. Registrar o prompt (ou só o texto trocável b/c e a Ficha) em `clientes/<cliente>/<produto>/criativos/PROMPTS-<campanha>.md`, um bloco por criativo com status "pendente/aprovado".
5. Duas instruções de uso para o Lucas: conferir texto, rosto e elementos proibidos ao voltar; se só o texto sair errado, pedir "keep the image exactly as is, fix only the text to: …" em vez de gerar de novo.

Nada prolixo: um criativo por resposta, sem recapitular regras que o usuário já sabe.
