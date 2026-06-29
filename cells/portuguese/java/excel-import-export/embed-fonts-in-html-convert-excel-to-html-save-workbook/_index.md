---
category: general
date: 2026-06-27
description: Incorpore fontes em HTML ao converter Excel para HTML. Aprenda como salvar
  a planilha como HTML com fontes incorporadas usando código Java simples.
draft: false
keywords:
- embed fonts in html
- convert excel to html
- save workbook as html
- Java Excel to HTML conversion
- Aspose.Cells HTML export
language: pt
og_description: Incorpore fontes em HTML ao converter Excel para HTML. Este guia mostra
  como salvar a pasta de trabalho como HTML com fontes incorporadas usando Java.
og_title: Incorporar fontes no HTML – Converter Excel para HTML e salvar a pasta de
  trabalho
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Embed fonts in HTML when you convert Excel to HTML. Learn how to save
    workbook as HTML with embedded fonts using simple Java code.
  headline: Embed Fonts in HTML – Convert Excel to HTML & Save Workbook
  type: TechArticle
- description: Embed fonts in HTML when you convert Excel to HTML. Learn how to save
    workbook as HTML with embedded fonts using simple Java code.
  name: Embed Fonts in HTML – Convert Excel to HTML & Save Workbook
  steps:
  - name: Right‑click the page → “View Page Source”.
    text: Right‑click the page → “View Page Source”.
  - name: 'Search for `@font-face`. You’ll find a CSS rule that contains a `src: url(data:font/ttf;base64,…)`
      line—this is the Base64‑encoded font data.'
    text: 'Search for `@font-face`. You’ll find a CSS rule that contains a `src: url(data:font/ttf;base64,…)`
      line—this is the Base64‑encoded font data.'
  - name: Load or create the workbook.
    text: Load or create the workbook.
  - name: Create `HtmlSaveOptions` and enable `setEmbedFonts(true)`.
    text: Create `HtmlSaveOptions` and enable `setEmbedFonts(true)`.
  - name: Call `Workbook.save` with those options.
    text: Call `Workbook.save` with those options.
  type: HowTo
tags:
- Java
- Aspose.Cells
- HTML
- Excel
title: Incorporar fontes em HTML – Converter Excel para HTML e salvar a pasta de trabalho
url: /pt/java/excel-import-export/embed-fonts-in-html-convert-excel-to-html-save-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Incorporar Fontes em HTML – Converter Excel para HTML e Salvar Pasta de Trabalho

Já precisou **incorporar fontes em HTML** ao *converter Excel para HTML*? Talvez você esteja construindo um portal de relatórios e as fontes web padrão simplesmente não atendam. A boa notícia é que você não precisa se contentar com um visual genérico—Aspose.Cells permite embutir as tipografias exatas que você usou na planilha diretamente no arquivo HTML gerado.

Neste tutorial vamos percorrer um exemplo completo, pronto‑para‑executar em Java que **salva a pasta de trabalho como HTML** com fontes incorporadas, explica por que você faria isso e aponta alguns detalhes que podem surgir. Ao final, você terá uma página HTML autônoma que se parece exatamente com a planilha Excel original, sem glifos ausentes, sem dores de cabeça com CSS externo.

## O que você vai aprender

- Como carregar uma pasta de trabalho Excel existente (ou criar uma do zero) em Java.  
- Como configurar `HtmlSaveOptions` para incorporar as fontes da pasta de trabalho diretamente na saída HTML.  
- Como invocar `Workbook.save` para que o arquivo seja gravado como **HTML com fontes incorporadas**.  
- Dicas para lidar com arquivos de fonte grandes, diretórios de fontes personalizados e solução de problemas comuns.

> **Pré‑requisito:** Você precisa do Aspose.Cells para Java (versão mais recente) no seu classpath e de um runtime Java 8+. Nenhuma outra biblioteca de terceiros é necessária.

---

## Etapa 1: Configurar o Projeto e Importar as Classes Necessárias

Antes de mergulharmos no código, vamos garantir que o ambiente de desenvolvimento esteja pronto. Se você usa Maven, adicione a dependência do Aspose.Cells ao seu `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- Use the newest version available -->
</dependency>
```

Se preferir Gradle, o equivalente é:

```gradle
implementation 'com.aspose:aspose-cells:23.12'
```

> **Dica profissional:** Mantenha a biblioteca atualizada. Novas versões costumam melhorar o tratamento de fontes e reduzir o tamanho dos dados incorporados.

Agora, importe as classes que usaremos:

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.HtmlSaveOptions;
import com.aspose.cells.SaveFormat;
import java.io.File;
```

Essas importações nos dão acesso ao modelo da pasta de trabalho, às opções de exportação HTML e a algumas classes utilitárias.

---

## Etapa 2: Carregar (ou Criar) a Pasta de Trabalho Excel

Você pode carregar um arquivo `.xlsx` existente ou criar uma pasta de trabalho dinamicamente. Para ilustrar, vamos supor que temos um arquivo chamado `Sample.xlsx` na pasta `resources` do projeto.

```java
// Load an existing workbook
String inputPath = "resources/Sample.xlsx";
Workbook wb = new Workbook(inputPath);
```

Se não houver um arquivo de origem, você pode gerar uma pasta de trabalho rapidamente:

```java
// Create a workbook from scratch (optional)
Workbook wb = new Workbook();               // creates a new empty workbook
wb.getWorksheets().get(0).getCells().putValue("A1", "Hello, world!");
```

> **Por que isso importa:** Quando você incorpora fontes, o Aspose.Cells extrai as definições exatas das fontes usadas na pasta de trabalho. Se a pasta contiver fontes personalizadas, elas viajarão com o HTML, garantindo fidelidade visual.

---

## Etapa 3: Configurar HtmlSaveOptions para Incorporar Fontes

Este é o coração do tutorial. Por padrão, `HtmlSaveOptions` gera CSS que referencia fontes do sistema. Para mudar esse comportamento, habilitamos a flag `setEmbedFonts(true)`.

```java
// Step 1: Create HTML save options
HtmlSaveOptions htmlOpts = new HtmlSaveOptions(SaveFormat.HTML);

// Step 2: Enable embedding of fonts in the HTML output
htmlOpts.setEmbedFonts(true);

// (Optional) Reduce the size of embedded fonts by subsetting only used glyphs
htmlOpts.setSubsetFonts(true);
```

### O que as opções fazem

| Opção | Padrão | Efeito quando alterado |
|--------|---------|---------------------|
| `setEmbedFonts(true)` | `false` | Incorpora os arquivos de fonte completos (geralmente como URIs de dados Base64) dentro do HTML gerado. |
| `setSubsetFonts(true)` | `false` | Reduz a fonte incorporada apenas aos caracteres realmente usados, diminuindo drasticamente o tamanho do arquivo. |
| `setFontEmbeddingMode(HtmlSaveOptions.FontEmbeddingMode.EMBED_ALL)` | `EMBED_ALL` | Você pode escolher incorporar apenas fontes específicas se houver restrições de licenciamento. |

> **Caso extremo:** Se a pasta de trabalho usar uma fonte que não está instalada no servidor, o Aspose.Cells recorre a uma fonte padrão do sistema. Para evitar surpresas, certifique‑se de que todas as fontes personalizadas estejam disponíveis no diretório de fontes do runtime Java ou registre‑as manualmente via `FontConfig`.

---

## Etapa 4: Salvar a Pasta de Trabalho como HTML com Fontes Incorporadas

Com as opções definidas, basta chamar `save`. A saída será um único arquivo `.html` que contém os dados da pasta de trabalho **e** os arquivos de fonte codificados diretamente no markup.

```java
// Step 3: Save the workbook as an HTML file with embedded fonts
String outputDir = "output";
new File(outputDir).mkdirs(); // Ensure the folder exists

String outputPath = outputDir + File.separator + "page.html";
wb.save(outputPath, htmlOpts);

System.out.println("HTML file with embedded fonts created at: " + outputPath);
```

Ao abrir `page.html` em qualquer navegador moderno, a página será renderizada com a tipografia exatamente igual à que você viu no Excel—sem arquivos de fonte externos, sem caracteres ausentes.

---

## Etapa 5: Verificar o Resultado e Entender a Saída

Abra o HTML gerado em um navegador (Chrome, Firefox, Edge—qualquer um serve). Você deverá ver a planilha renderizada fielmente. Para confirmar que as fontes realmente foram incorporadas:

1. Clique com o botão direito na página → “Ver código‑fonte da página”.  
2. Procure por `@font-face`. Você encontrará uma regra CSS que contém uma linha `src: url(data:font/ttf;base64,…)`—esse é o dado da fonte codificado em Base64.  

Se isso aparecer, a etapa **incorporar fontes em HTML** foi bem‑sucedida.

### Perguntas Frequentes

- **“Por que o arquivo HTML está maior do que o esperado?”**  
  Incorporar fontes completas pode acrescentar várias centenas de kilobytes. Use `setSubsetFonts(true)` para reduzir o tamanho ou considere converter apenas as planilhas necessárias.

- **“Posso incorporar apenas uma fonte específica?”**  
  Sim. Defina `htmlOpts.setFontEmbeddingMode(HtmlSaveOptions.FontEmbeddingMode.EMBED_SPECIFIED)` e então especifique os nomes das fontes via `htmlOpts.getSpecifiedFontNames().add("MyCustomFont")`.

- **“E se a fonte for licenciada e eu não puder incorporá‑la?”**  
  Desative a flag (`setEmbedFonts(false)`) e forneça um fallback web‑safe via CSS, ou hospede a fonte em um CDN onde você tenha permissão.

---

## Etapa 6: Lidando com Pastas de Trabalho Grandes e Dicas de Performance

Incorporar fontes funciona bem para planilhas modestamente dimensionadas, mas uma pasta com dezenas de fontes personalizadas pode inflar o tamanho do HTML. Aqui vão algumas recomendações orientadas à performance:

- **Subconjunte fontes** (já mostrado) para manter apenas os glifos usados.  
- **Exporte apenas as planilhas necessárias** usando `htmlOpts.setExportActiveWorksheetOnly(true)`.  
- **Comprima o HTML** após a geração (por exemplo, gzip no servidor) para reduzir a latência de rede.  
- **Cache o HTML gerado** se o mesmo arquivo Excel for solicitado com frequência.

---

## Etapa 7: Próximos Passos – Indo Além da Exportação Básica

Agora que você domina **incorporar fontes em HTML**, pode explorar recursos relacionados:

- **Converter Excel para HTML com imagens** (`htmlOpts.setExportImagesAsBase64(true)`).  
- **Gerar PDF em vez de HTML** (`wb.save("output.pdf", SaveFormat.PDF)`).  
- **Criar HTML responsivo** ajustando `htmlOpts.setExportActiveWorksheetOnly` e `htmlOpts.setExportGridLines`.  

Todos esses recursos seguem o mesmo padrão: configure um objeto `*SaveOptions`, ative as flags apropriadas e chame `Workbook.save`.

---

## Conclusão

Você acabou de aprender como **incorporar fontes em HTML** enquanto **converte Excel para HTML** e **salva a pasta de trabalho como HTML** usando Aspose.Cells para Java. Os passos principais são:

1. Carregar ou criar a pasta de trabalho.  
2. Criar `HtmlSaveOptions` e habilitar `setEmbedFonts(true)`.  
3. Chamar `Workbook.save` com essas opções.

O resultado é um único arquivo HTML portátil que se parece exatamente com sua planilha original—sem fontes ausentes, sem arquivos CSS adicionais e sem depender das fontes instaladas no cliente.

Sinta‑se à vontade para experimentar a sub‑conjuntura de fontes, a incorporação seletiva ou até combinar isso com cache no lado do servidor para cenários de alto tráfego. Se encontrar algum detalhe inesperado (como arquivos muito grandes ou glifos ausentes), revise as configurações opcionais que abordamos e ajuste conforme necessário.

Feliz codificação, e aproveite o HTML pixel‑perfect que você pode servir diretamente das suas aplicações Java!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [Converter Excel para HTML em Java usando Aspose.Cells: Um Guia Passo a Passo](/cells/english/java/workbook-operations/convert-excel-html-aspose-cells-java/)
- [Exportar Excel para HTML usando Aspose.Cells para Java: Um Guia Completo](/cells/english/java/workbook-operations/export-excel-to-html-aspose-cells-java/)
- [Exportar Excel para HTML usando IStreamProvider & Aspose.Cells para Java: Um Guia Abrangente](/cells/english/java/workbook-operations/export-excel-html-streamprovider-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}