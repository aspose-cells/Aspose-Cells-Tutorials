---
category: general
date: 2026-11-25
description: Exportar Excel para SVG com Aspose.Cells em Java – um guia passo a passo
  para salvar Excel como SVG e criar uma imagem vetorial.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to svg
- save excel as svg
- excel to vector image
- convert excel to svg
- export excel as svg
language: pt
lastmod: 2026-11-25
og_description: Exporte Excel para SVG com Aspose.Cells em Java. Aprenda como salvar
  Excel como SVG e gerar imagens vetoriais de alta qualidade em poucas linhas de código.
og_image_alt: Screenshot of an Excel worksheet exported to SVG format
og_title: Exportar Excel para SVG em Java – tutorial completo do Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: Export Excel to SVG with Aspose.Cells in Java – a step‑by‑step guide
    to save Excel as SVG and create a vector image.
  headline: How to export Excel to SVG using Aspose.Cells in Java
  type: TechArticle
- description: Export Excel to SVG with Aspose.Cells in Java – a step‑by‑step guide
    to save Excel as SVG and create a vector image.
  name: How to export Excel to SVG using Aspose.Cells in Java
  steps:
  - name: Load the workbook containing the data
    text: '```java import com.aspose.cells.Workbook;'
  - name: Set up image export options for SVG
    text: '```java import com.aspose.cells.ImageOrPrintOptions; import com.aspose.cells.ImageFormat;'
  - name: Save the workbook as an SVG file
    text: '```java import com.aspose.cells.SaveFormat;'
  - name: What to explore next
    text: '* **Export Excel as PNG or JPEG** – change `exportOptions.setImageFormat(ImageFormat.PNG)`
      for raster output. * **Convert Excel to PDF** – use `PdfSaveOptions` for printable
      documents. * **Batch processing** – combine the above code with a file‑system
      watcher to automatically **convert Excel to SVG*'
  type: HowTo
tags:
- Aspose.Cells
- Java
- SVG
- Excel
title: Como exportar Excel para SVG usando Aspose.Cells em Java
url: /pt/java/excel-import-export/how-to-export-excel-to-svg-using-aspose-cells-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como exportar Excel para SVG usando Aspose.Cells em Java

Se você precisa **exportar Excel para SVG**, este guia mostra como fazer isso com Aspose.Cells para Java. Você aprenderá como **salvar Excel como SVG** e gerar uma **imagem vetorial** de alta qualidade em apenas algumas linhas de código.

Exportar uma pasta de trabalho Excel para um arquivo SVG permite incorporar a planilha em páginas da web, relatórios ou qualquer ambiente que prefira gráficos escaláveis. O formato SVG preserva fontes, cores e bordas das células sem a pixelização que você obtém com imagens rasterizadas.

## Pré‑requisitos

Antes de começar, certifique‑se de que você tem:

* Java 17 ou superior instalado.  
* Uma licença ativa do Aspose.Cells para Java (ou uma chave de avaliação temporária).  
* Um projeto Maven ou Gradle onde você possa adicionar a dependência do Aspose.Cells.

Adicione a biblioteca Aspose.Cells ao seu projeto:

```xml
<!-- Maven -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- Use the latest stable version -->
</dependency>
```

```gradle
// Gradle
implementation 'com.aspose:aspose-cells:24.10'
```

## Exportar Excel para SVG – passo a passo

O processo consiste em três etapas simples: carregar a pasta de trabalho, configurar as opções de exportação SVG e salvar o resultado. Cada etapa é explicada abaixo.

### Etapa 1: Carregar a pasta de trabalho que contém os dados

```java
import com.aspose.cells.Workbook;

public class ExcelToSvgDemo {
    public static void main(String[] args) throws Exception {
        // Load the Excel file you want to convert.
        Workbook workbook = new Workbook("C:/Data/Report.xlsx");
        // Continue with export options...
    }
}
```

**Por que isso importa:**  
`Workbook` é o objeto central no Aspose.Cells. Carregar o arquivo uma única vez lhe dá acesso a todas as planilhas, estilos e objetos incorporados, que o exportador SVG renderizará posteriormente.

### Etapa 2: Configurar as opções de exportação de imagem para SVG

```java
import com.aspose.cells.ImageOrPrintOptions;
import com.aspose.cells.ImageFormat;

ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
exportOptions.setImageFormat(ImageFormat.SVG); // Guarantees a vector output
exportOptions.setOnePagePerSheet(true);       // Export each sheet as a single SVG page
exportOptions.setTransparent(true);           // Preserve transparent backgrounds
```

**Por que isso importa:**  
`ImageOrPrintOptions` permite controlar o formato de saída. Selecionar `ImageFormat.SVG` garante que o resultado seja uma **imagem vetorial** em vez de um bitmap. Habilitar `OnePagePerSheet` evita quebras de página dentro de uma planilha, o que geralmente é desejado quando o SVG será exibido em uma visualização web.

### Etapa 3: Salvar a pasta de trabalho como um arquivo SVG

```java
import com.aspose.cells.SaveFormat;

workbook.save("C:/Output/Report.svg", exportOptions);
System.out.println("Excel workbook successfully exported to SVG.");
```

**Por que isso importa:**  
O método `save` combina a pasta de trabalho carregada com as `exportOptions` configuradas. A chamada grava um arquivo SVG totalmente compatível que pode ser aberto em navegadores, Inkscape ou qualquer editor que suporte vetores.

## Exemplo completo executável

Juntando as três etapas, você obtém um programa autocontido que pode ser compilado e executado imediatamente:

```java
import com.aspose.cells.*;

public class ExportExcelToSvg {
    public static void main(String[] args) throws Exception {
        // 1. Load the workbook
        Workbook workbook = new Workbook("C:/Data/FontVariation.xlsx");

        // 2. Configure SVG export options
        ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
        exportOptions.setImageFormat(ImageFormat.SVG);
        exportOptions.setOnePagePerSheet(true);
        exportOptions.setTransparent(true);

        // 3. Export to SVG
        workbook.save("C:/Output/WithVariationSelectors.svg", exportOptions);
        System.out.println("Export complete: Excel saved as SVG.");
    }
}
```

**Saída esperada**

Ao executar o programa, ele imprime:

```
Export complete: Excel saved as SVG.
```

Você encontrará `WithVariationSelectors.svg` em `C:/Output`. Abrir o arquivo em um navegador mostra a planilha renderizada como gráficos escaláveis, com texto, bordas e cores de célula preservados.

## Variações comuns e casos de borda

| Situação | Ajuste recomendado |
|-----------|------------------------|
| **Múltiplas planilhas** | Percorra `workbook.getWorksheets()` e chame `save` para cada planilha, opcionalmente acrescentando o nome da planilha ao nome do arquivo. |
| **Pastas de trabalho grandes** | Aumente `exportOptions.setRenderThreadCount(int)` para usar renderização paralela, reduzindo o tempo de conversão. |
| **DPI personalizado** | Chame `exportOptions.setHorizontalResolution(int)` e `exportOptions.setVerticalResolution(int)` para controlar a escala do `viewBox` do SVG. |
| **Incorporação de fontes** | Defina `exportOptions.setExportFontAsSVG(true)` para incorporar definições de fonte diretamente no SVG, garantindo fidelidade visual em máquinas sem as fontes originais. |
| **Arquivos protegidos por senha** | Forneça a senha ao carregar: `Workbook workbook = new Workbook("file.xlsx", new LoadOptions(LoadFormat.XLSX) {{ setPassword("pwd"); }});` |

## Dicas profissionais

* **Evite fallback raster** – Se a planilha contém gráficos complexos, verifique se eles aparecem como elementos vetoriais no SVG. Caso contrário, habilite `exportOptions.setExportChartAsSVG(true)`.  
* **Desempenho** – Para conversões em lote, reutilize uma única instância de `ImageOrPrintOptions` em vez de criar uma nova para cada arquivo.  
* **Testes** – Valide o SVG gerado com um validador online (por exemplo, W3C SVG Validator) para detectar marcação malformada logo no início.

## Verificar a conversão

Você pode confirmar programaticamente que o arquivo de saída é realmente um SVG:

```java
import java.nio.file.Files;
import java.nio.file.Paths;

byte[] data = Files.readAllBytes(Paths.get("C:/Output/Report.svg"));
String content = new String(data, "UTF-8");
if (content.contains("<svg")) {
    System.out.println("File is a valid SVG.");
}
```

A presença do elemento raiz `<svg>` indica que a operação **converter Excel para SVG** foi bem‑sucedida.

## Conclusão

Este tutorial demonstrou como **exportar Excel para SVG** usando Aspose.Cells para Java. Ao carregar a pasta de trabalho, configurar `ImageOrPrintOptions` para SVG e chamar `save`, você pode **salvar Excel como SVG** e obter uma conversão limpa de **Excel para imagem vetorial**. A partir daqui, você pode incorporar o SVG em páginas web, incluí‑lo em documentação ou processá‑lo ainda mais com qualquer ferramenta de gráficos vetoriais.

### O que explorar a seguir

* **Exportar Excel como PNG ou JPEG** – altere `exportOptions.setImageFormat(ImageFormat.PNG)` para saída raster.  
* **Converter Excel para PDF** – use `PdfSaveOptions` para documentos imprimíveis.  
* **Processamento em lote** – combine o código acima com um observador de sistema de arquivos para automaticamente **converter Excel para SVG** para cada nova pasta de trabalho em uma pasta.

Sinta‑se à vontade para experimentar as opções e deixar que a flexibilidade do Aspose.Cells transforme seus dados do Excel em qualquer formato visual que você precisar. Feliz codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [How to Export Excel Charts as SVG Using Aspose.Cells Java for Scalable Vector Graphics](/cells/english/java/charts-graphs/export-excel-charts-svg-aspose-cells-java/)
- [How to Create and Save an Excel Workbook as SVG using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [How to Export Excel to SVG – Step‑by‑Step Java Guide](/cells/english/java/excel-import-export/how-to-export-excel-to-svg-step-by-step-java-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}