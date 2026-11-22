---
category: general
date: 2026-11-22
description: Aprenda como incorporar fontes ao salvar o Excel como HTML, permitindo
  a incorporação de fontes para renderização consistente em diferentes navegadores.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to embed fonts
- enable font embedding
- save excel html
- html font embedding
- embed fonts html
language: pt
lastmod: 2026-11-22
og_description: Como incorporar fontes ao salvar o Excel como HTML. Siga este guia
  para habilitar a incorporação de fontes e garantir que suas planilhas tenham a mesma
  aparência em qualquer navegador.
og_image_alt: Screenshot showing an Excel file exported to HTML with embedded fonts
og_title: Como incorporar fontes ao salvar o Excel como HTML – passo a passo
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn how to embed fonts while saving Excel as HTML, enabling font
    embedding for consistent rendering across browsers.
  headline: How to embed fonts when saving Excel as HTML – complete guide
  type: TechArticle
- description: Learn how to embed fonts while saving Excel as HTML, enabling font
    embedding for consistent rendering across browsers.
  name: How to embed fonts when saving Excel as HTML – complete guide
  steps:
  - name: What if the font is not found?
    text: Aspose.Cells can embed only fonts that the JVM can locate. If you receive
      a warning like *“Font not found, falling back to default”*, make sure the font
      file is installed on the operating system or placed in a directory listed in
      the `java.library.path`.
  - name: Does embedding increase file size?
    text: 'Yes. Embedding a full TrueType font can add 30–200 KB to the HTML file,
      depending on the font. If size is a concern, consider:'
  - name: Can I embed multiple fonts?
    text: Absolutely. The library examines every cell style, extracts all referenced
      fonts, and embeds each one when `setEmbedFonts(true)` is active.
  - name: Is the approach compatible with older browsers?
    text: The `@font-face` rule works in all browsers that support CSS 2.1 and later,
      which includes IE 9 +, Chrome, Firefox, Safari, and Edge. For very old browsers
      (IE 8‑), you may need to provide a fallback font family.
  type: HowTo
tags:
- Excel
- HTML
- Font embedding
title: Como incorporar fontes ao salvar o Excel como HTML – guia completo
url: /pt/java/excel-import-export/how-to-embed-fonts-when-saving-excel-as-html-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como incorporar fontes ao salvar Excel como HTML – guia completo

Se você precisa **como incorporar fontes** ao exportar uma pasta de trabalho do Excel para HTML, este guia mostra os passos exatos. Incorporar fontes garante que o arquivo HTML gerado exiba a mesma tipografia da pasta de trabalho original, mesmo em sistemas que não possuam os tipos de letra necessários. Você também aprenderá como **habilitar a incorporação de fontes** usando Aspose.Cells for Java, uma maneira confiável de **salvar Excel HTML** com fidelidade visual completa.

Neste tutorial você irá:

* Configurar um projeto Java com a biblioteca Aspose.Cells.  
* Criar um objeto `HtmlSaveOptions` e ativar **html font embedding**.  
* Salvar a pasta de trabalho como um arquivo HTML que contém os arquivos de fonte necessários.  

Pré‑requisitos:

* Java 8 ou mais recente.  
* Aspose.Cells for Java (recomenda‑se a versão mais recente).  
* Conhecimento básico de Java e manipulação de arquivos Excel.

---

## O que você precisará

| Item | Razão |
|------|--------|
| **Aspose.Cells for Java** | Fornece a classe `HtmlSaveOptions` e o método `setEmbedFonts`. |
| **Uma fonte TrueType ou OpenType** instalada na máquina | A biblioteca pode incorporar apenas fontes que estejam acessíveis à JVM. |
| **Um IDE ou ferramenta de build** (por exemplo, Maven, Gradle ou `javac` simples) | Para compilar e executar o exemplo. |

---

## Etapa 1: Adicionar Aspose.Cells ao seu projeto

Se você usa Maven, adicione a dependência ao `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- use the latest version -->
</dependency>
```

Para Gradle, coloque o seguinte em `build.gradle`:

```gradle
implementation 'com.aspose:aspose-cells:23.12'
```

*Dica profissional:* Mantenha a versão da biblioteca atualizada; lançamentos mais recentes incluem correções de bugs para o tratamento de **embed fonts html**.

---

## Etapa 2: Criar uma pasta de trabalho e preenchê‑la

Abaixo está um programa Java mínimo e autocontido que cria uma pasta de trabalho, escreve algum texto formatado e a prepara para exportação HTML.

```java
import com.aspose.cells.*;

public class ExcelHtmlFontEmbedding {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create a new workbook
        Workbook wb = new Workbook();

        // 2️⃣ Access the first worksheet
        Worksheet sheet = wb.getWorksheets().get(0);
        Cells cells = sheet.getCells();

        // 3️⃣ Put some text in A1 and apply a custom font
        Cell a1 = cells.get("A1");
        a1.putValue("Hello, embedded fonts!");
        Style style = a1.getStyle();
        Font font = style.getFont();
        font.setName("Comic Sans MS");   // any installed font works
        font.setSize(14);
        a1.setStyle(style);

        // 4️⃣ Save as HTML with font embedding (see next step)
        saveWithEmbeddedFonts(wb);
    }

    private static void saveWithEmbeddedFonts(Workbook wb) throws Exception {
        // This method contains the core of **html font embedding**
        HtmlSaveOptions saveOptions = new HtmlSaveOptions();
        // Enable font embedding so the HTML contains the required .ttf files
        saveOptions.setEmbedFonts(true);

        // Optional: specify a folder for the generated assets (fonts, images)
        saveOptions.setExportImagesAsBase64(true); // reduces external files
        String outputPath = "output/embedded.html";

        // Perform the save operation
        wb.save(outputPath, saveOptions);
        System.out.println("Workbook saved with embedded fonts to: " + outputPath);
    }
}
```

**Por que isso funciona:**  
* `HtmlSaveOptions#setEmbedFonts(true)` informa ao Aspose.Cells para incluir os arquivos de fonte usados na pasta de trabalho dentro do HTML gerado.  
* Definir `ExportImagesAsBase64` mantém a saída organizada, mas é opcional.

---

## Etapa 3: Verificar o HTML gerado

Abra `output/embedded.html` em qualquer navegador moderno. Você deverá ver o texto renderizado com *Comic Sans MS* mesmo que a fonte não esteja instalada na máquina do cliente. Para confirmar que a fonte está realmente incorporada, visualize o código‑fonte da página; você encontrará um bloco `<style>` que contém uma regra `@font-face` referenciando um arquivo de fonte codificado em base64.

```html
<style>
@font-face {
    font-family: 'Comic Sans MS';
    src: url(data:font/ttf;base64,AAEAAAARAQAABAA...);
}
...
</style>
```

**Saída esperada:** A página exibe “Hello, embedded fonts!” usando a fonte especificada, e o arquivo HTML contém os dados da fonte incorporada.

---

## Perguntas comuns e casos de borda

### E se a fonte não for encontrada?
Aspose.Cells pode incorporar apenas fontes que a JVM consiga localizar. Se você receber um aviso como *“Font not found, falling back to default”*, certifique‑se de que o arquivo de fonte está instalado no sistema operacional ou colocado em um diretório listado em `java.library.path`.

### A incorporação aumenta o tamanho do arquivo?
Sim. Incorporar uma fonte TrueType completa pode acrescentar de 30 a 200 KB ao arquivo HTML, dependendo da fonte. Se o tamanho for uma preocupação, considere:

* Usar apenas os caracteres que aparecem na pasta de trabalho (Aspose.Cells remove glifos não usados).  
* Selecionar uma fonte web‑safe leve que a maioria dos navegadores já possua.

### Posso incorporar várias fontes?
Absolutamente. A biblioteca examina cada estilo de célula, extrai todas as fontes referenciadas e incorpora cada uma quando `setEmbedFonts(true)` está ativo.

### O método é compatível com navegadores antigos?
A regra `@font-face` funciona em todos os navegadores que suportam CSS 2.1 ou superior, incluindo IE 9 +, Chrome, Firefox, Safari e Edge. Para navegadores muito antigos (IE 8‑), pode ser necessário fornecer uma família de fontes alternativa.

---

## Dicas avançadas para uso em produção

* **Cachear o HTML gerado** – incorporar fontes torna cada exportação mais pesada; armazene o resultado se precisar servi‑lo repetidamente.  
* **Pasta de ativos separada** – em vez de base64, você pode permitir que Aspose.Cells grave os arquivos `.ttf` em uma pasta (`saveOptions.setExportFontFile(true)`). Isso mantém o tamanho do HTML pequeno e permite que os navegadores façam cache dos arquivos de fonte.  
* **Segurança** – nunca incorpore fontes de fontes não confiáveis; elas podem conter dados maliciosos. Use apenas fontes que você controla.

---

## Conclusão

Agora você sabe **como incorporar fontes** ao **salvar Excel HTML** usando Aspose.Cells for Java. Ao habilitar **font embedding**, o HTML gerado contém as regras `@font-face` necessárias, garantindo que sua planilha tenha a mesma aparência em todos os navegadores. Esta técnica resolve o clássico problema de *html font embedding* e é a forma recomendada de **enable font embedding** para qualquer fluxo de conversão de Excel para HTML.

Pronto para o próximo passo? Explore tópicos relacionados como **saving Excel as PDF with embedded fonts**, ou aprenda a **customize CSS output** para páginas web responsivas. Feliz codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Como incorporar fontes ao salvar Excel para HTML com Aspose.Cells para C#](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-when-saving-excel-to-html-with-c/)
- [Como usar wrapcols e incorporar fontes ao salvar Excel para HTML](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-use-wrapcols-and-embed-fonts-saving-excel-to-html/)
- [Como incorporar fontes em HTML ao salvar uma pasta de trabalho](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-in-html-when-saving-a-workbook/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}