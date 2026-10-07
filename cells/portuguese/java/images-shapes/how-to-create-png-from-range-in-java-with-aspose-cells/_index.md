---
category: general
date: 2026-10-07
description: Aprenda a criar PNG a partir de um intervalo e exportar dados como PNG
  em Java. Este guia mostra como salvar a imagem de um intervalo do Excel usando Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create png from range
- export data as png
- save excel range image
- convert worksheet to png
- save cells as png
language: pt
lastmod: 2026-10-07
og_description: Crie PNG a partir de um intervalo em Java e exporte os dados como
  PNG com Aspose.Cells. Siga este tutorial completo para salvar a imagem do intervalo
  do Excel instantaneamente.
og_image_alt: Screenshot of Java code that creates a PNG from an Excel range
og_title: Criar PNG a partir de um intervalo em Java – guia passo a passo do Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to create PNG from range and export data as PNG in Java.
    This guide shows you how to save Excel range image using Aspose.Cells.
  headline: How to create PNG from range in Java with Aspose.Cells
  type: TechArticle
- description: Learn how to create PNG from range and export data as PNG in Java.
    This guide shows you how to save Excel range image using Aspose.Cells.
  name: How to create PNG from range in Java with Aspose.Cells
  steps:
  - name: Maven dependency
    text: '```xml <dependency> <groupId>com.aspose</groupId> <artifactId>aspose-cells</artifactId>
      <version>23.12</version> </dependency> ```'
  - name: Expected output
    text: '* A file named `PivotImage.png` located in `YOUR_DIRECTORY`. * The image
      shows the exact layout, fonts, colors, and borders from the selected range.
      * If the source range contains a pivot table, the rendered image includes the
      same styling and calculated values as displayed in Excel.'
  - name: Exporting a non‑contiguous range
    text: Aspose.Cells does not render disjoint ranges in a single image. To export
      multiple areas, create separate images for each range and combine them later
      with an image‑processing library (e.g., ImageIO).
  - name: Saving a large worksheet as PNG
    text: 'Rendering an entire sheet that spans thousands of rows can consume significant
      memory. Mitigate this by:'
  - name: Preserving cell formulas
    text: A PNG image is a raster format; formulas are not retained. If downstream
      consumers need the raw data, also export the range as CSV or JSON using `Range.exportDataTable()`.
  - name: Next steps
    text: '* Experiment with different `Resolution` values to balance quality and
      file size. * Use `ImageOrPrintOptions.setTransparent(true)` if you need a PNG
      with a transparent background. * Combine multiple range images into a single
      PDF using `PdfSaveOptions` for multi‑page reports. * Explore exporting to '
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Como criar PNG a partir de um intervalo em Java com Aspose.Cells
url: /pt/java/images-shapes/how-to-create-png-from-range-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como criar PNG a partir de um intervalo em Java com Aspose.Cells

Se você precisa **criar PNG a partir de um intervalo** em uma pasta de trabalho Excel, este tutorial mostra exatamente como fazer isso. Ao final do guia você será capaz de **exportar dados como PNG**, salvar a imagem de um intervalo do Excel e reutilizar o arquivo em relatórios ou páginas da web.

Você verá um programa Java completo e executável que carrega uma pasta de trabalho, seleciona as células desejadas, renderiza-as como PNG e salva o resultado no disco. Nenhuma ferramenta externa é necessária — o Aspose.Cells cuida de tudo internamente.

## O que este tutorial cobre

* Pré‑requisitos e configuração do Maven para Aspose.Cells
* Carregamento de uma pasta de trabalho que contém uma tabela dinâmica ou qualquer intervalo de dados
* Definição do intervalo de células exato que você deseja converter
* Configuração das opções de imagem para saída PNG
* Renderização do intervalo e salvamento do arquivo PNG
* Armadilhas comuns e dicas para imagens de alta qualidade

Depois de concluir estas etapas, você poderá **converter planilha para PNG** para qualquer intervalo, seja uma tabela simples ou um gráfico dinâmico complexo.

## Pré‑requisitos

* Java 17 ou superior (o código compila com JDK 11+)
* Maven 3.6+ (ou Gradle, se preferir)
* Aspose.Cells for Java 23.12 ou mais recente – adicione a dependência mostrada abaixo
* Um arquivo Excel existente (`PivotWithStyle.xlsx`) que contém o intervalo que você deseja capturar

> **Dica profissional:** Se você não tem uma licença, pode solicitar uma chave de avaliação temporária da Aspose. A biblioteca funciona em modo de avaliação sem configuração adicional.

### Dependência Maven

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
</dependency>
```

## Etapa 1: Carregar a pasta de trabalho que contém o intervalo alvo

A primeira operação é abrir o arquivo Excel. O Aspose.Cells lê o arquivo na memória sem exigir o Microsoft Office.

```java
import com.aspose.cells.*;

public class PivotRangeToPng {
    public static void main(String[] args) throws Exception {
        // Load the workbook containing the data you want to export
        Workbook workbook = new Workbook("YOUR_DIRECTORY/PivotWithStyle.xlsx");
```

*Por que isso importa*: Carregar a pasta de trabalho lhe dá acesso às planilhas, células e propriedades de configuração de página necessárias para a renderização.

## Etapa 2: Acessar a planilha que contém o intervalo

A maioria das pastas de trabalho tem uma planilha padrão no índice 0, mas você também pode usar o nome da planilha.

```java
        // Retrieve the first worksheet (index 0)
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

Se seus dados estiverem em outra planilha, substitua `0` pelo índice apropriado ou use `workbook.getWorksheets().get("SheetName")`.

## Etapa 3: Definir o intervalo de células que você deseja converter

Você pode especificar qualquer área retangular usando a notação A1. Neste exemplo capturamos `A1:D15`, que pode ser uma tabela dinâmica ou um bloco de dados regular.

```java
        // Create a range object for cells A1:D15
        Range pivotRange = worksheet.getCells().createRange("A1:D15");
```

*Caso especial*: Quando o intervalo inclui células mescladas, o Aspose.Cells expande automaticamente a imagem para incluir a área mesclada.

## Etapa 4: Preparar as opções de imagem PNG

`ImageOrPrintOptions` permite controlar o formato, a resolução e outros detalhes de renderização. Definir o formato de salvamento como PNG garante qualidade sem perdas.

```java
        // Configure image options – we want a PNG file
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions();
        imageOptions.setSaveFormat(SaveFormat.PNG);
        // Optional: increase DPI for sharper output (default is 96)
        imageOptions.setImageFormat(ImageFormat.getPng());
        imageOptions.setResolution(150); // 150 DPI for clearer text
```

Aumentar o DPI é útil quando as células de origem contêm fontes pequenas ou gráficos detalhados.

## Etapa 5: Limitar a área de renderização ao intervalo selecionado

Ao atribuir o intervalo como área de impressão, o Aspose.Cells renderiza apenas essas células e ignora o restante da planilha.

```java
        // Set the print area so only the defined range is rendered
        worksheet.getPageSetup().setPrintArea(pivotRange.getRefersTo());
```

Se você pular esta etapa, toda a planilha será rasterizada, o que pode desperdiçar memória e gerar uma imagem maior.

## Etapa 6: Renderizar o intervalo e adicionar a imagem à planilha (opcional)

Se quiser incorporar o PNG gerado de volta na pasta de trabalho (para fins de visualização), pode adicioná‑lo como uma imagem. Esta etapa é opcional para cenários de exportação pura.

```java
        // Add the rendered image back to the worksheet at cell (0,0) – optional
        worksheet.getPictures().add(0, 0, imageOptions);
```

*Por que você pode fazer isso*: Alguns fluxos de trabalho exigem que a imagem faça parte da pasta de trabalho antes da distribuição, como a criação de um relatório imprimível que combina células nativas e imagens.

## Etapa 7: Salvar o arquivo PNG no disco

Finalmente, escreva a imagem em um arquivo. O método `save` respeita o formato especificado em `imageOptions`.

```java
        // Save the rendered PNG image to the specified path
        workbook.save("YOUR_DIRECTORY/PivotImage.png", SaveFormat.PNG);
    }
}
```

Quando o programa terminar, `PivotImage.png` conterá uma captura pixel‑perfect das células `A1:D15`.

### Saída esperada

* Um arquivo chamado `PivotImage.png` localizado em `YOUR_DIRECTORY`.
* A imagem mostra o layout exato, fontes, cores e bordas do intervalo selecionado.
* Se o intervalo de origem contiver uma tabela dinâmica, a imagem renderizada inclui o mesmo estilo e valores calculados exibidos no Excel.

## Lidando com cenários comuns

### Exportando um intervalo não contíguo

O Aspose.Cells não renderiza intervalos disjuntos em uma única imagem. Para exportar várias áreas, crie imagens separadas para cada intervalo e combine‑as depois com uma biblioteca de processamento de imagens (por exemplo, ImageIO).

```java
Range first = worksheet.getCells().createRange("A1:B10");
Range second = worksheet.getCells().createRange("D1:E10");
// Render each range individually using the same ImageOrPrintOptions
```

### Salvando uma planilha grande como PNG

Renderizar uma planilha inteira que abrange milhares de linhas pode consumir muita memória. Mitigue isso:

* Reduzindo o DPI (`imageOptions.setResolution(72)`) para um arquivo menor.
* Usando `setPageCount` para limitar o número de páginas renderizadas.
* Exportando uma página imprimível de cada vez via `worksheet.getPageSetup().setPrintArea(...)`.

### Preservando fórmulas das células

Uma imagem PNG é um formato raster; fórmulas não são mantidas. Se consumidores posteriores precisarem dos dados brutos, exporte também o intervalo como CSV ou JSON usando `Range.exportDataTable()`.

## Exemplo completo e executável

Abaixo está a classe Java completa que você pode copiar‑colar no seu IDE. Substitua `YOUR_DIRECTORY` por um caminho absoluto ou relativo na sua máquina.

```java
import com.aspose.cells.*;

public class PivotRangeToPng {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the workbook containing the data
        Workbook workbook = new Workbook("YOUR_DIRECTORY/PivotWithStyle.xlsx");

        // 2️⃣ Access the first worksheet (adjust index or name as needed)
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 3️⃣ Define the exact cell range you want to convert (A1:D15 in this case)
        Range pivotRange = worksheet.getCells().createRange("A1:D15");

        // 4️⃣ Prepare PNG image options – set format and optional resolution
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions();
        imageOptions.setSaveFormat(SaveFormat.PNG);
        imageOptions.setResolution(150); // sharper output

        // 5️⃣ Restrict rendering to the selected range
        worksheet.getPageSetup().setPrintArea(pivotRange.getRefersTo());

        // 6️⃣ (Optional) Add the rendered image back to the worksheet for preview
        worksheet.getPictures().add(0, 0, imageOptions);

        // 7️⃣ Save the PNG file – this creates the final image on disk
        workbook.save("YOUR_DIRECTORY/PivotImage.png", SaveFormat.PNG);
    }
}
```

Execute o programa com `mvn compile exec:java` (ou sua ferramenta de build preferida). Após a execução, abra `PivotImage.png` para verificar o resultado.

## Conclusão

Agora você sabe como **criar PNG a partir de um intervalo** em Java usando Aspose.Cells, efetivamente **exportar dados como PNG** e **salvar imagem de intervalo do Excel** para qualquer cenário de relatório ou compartilhamento. As etapas — carregar a pasta de trabalho, definir o intervalo, configurar as opções de imagem, definir a área de impressão e salvar o arquivo — cobrem todo o fluxo de trabalho para **converter planilha para PNG** e **salvar células como PNG**.

### Próximos passos

* Experimente diferentes valores de `Resolution` para equilibrar qualidade e tamanho do arquivo.
* Use `ImageOrPrintOptions.setTransparent(true)` se precisar de um PNG com fundo transparente.
* Combine várias imagens de intervalo em um único PDF usando `PdfSaveOptions` para relatórios de várias páginas.
* Explore a exportação para outros formatos raster (JPEG, BMP) alterando `setSaveFormat`.

Sinta‑se à vontade para adaptar este padrão a gráficos, tabelas ou até planilhas inteiras. Feliz codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [How to Export an Excel Worksheet to PNG Using Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)
- [Convert Excel to PNG Using Aspose.Cells for Java: A Step‑By‑Step Guide](/cells/english/java/workbook-operations/convert-excel-to-png-aspose-cells-java/)
- [Create Union Range in Excel using Aspose.Cells Java: A Comprehensive Guide](/cells/english/java/range-management/create-union-range-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}