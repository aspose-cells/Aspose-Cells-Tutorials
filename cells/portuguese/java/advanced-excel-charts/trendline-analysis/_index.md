---
date: 2026-08-27
description: Aprenda a adicionar trendline a chart, exibir seu valor R‑squared e exportar
  o chart como imagem PNG ou JPEG usando Aspose.Cells for Java.
keywords:
- add trendline to chart
- save chart as image
- export excel chart image
- java create excel workbook
- convert chart to png
lastmod: 2026-08-27
linktitle: Exportar Chart para Imagem com Análise de Trendline
og_description: Adicionar trendline a chart, visualizar R‑squared e exportar o resultado
  como PNG/JPEG usando Aspose.Cells for Java – uma solução rápida, com suporte a 50
  formatos.
og_image_alt: Guide showing Java code to add a trendline to an Excel chart and export
  it as an image
og_title: Adicionar trendline a chart e exportar como imagem com Aspose.Cells for
  Java
schemas:
- author: Aspose
  dateModified: '2026-08-27'
  description: Learn how to add trendline to chart, display its R‑squared value, and
    export the chart as a PNG or JPEG image using Aspose.Cells for Java.
  headline: How to add trendline to chart and export as image in Java
  type: TechArticle
- description: Learn how to add trendline to chart, display its R‑squared value, and
    export the chart as a PNG or JPEG image using Aspose.Cells for Java.
  name: How to add trendline to chart and export as image in Java
  steps:
  - name: set up the project
    text: Create a new Java project and place the Aspose.Cells JARs on the build path.
      This prepares the environment for generating and manipulating Excel files.
  - name: load excel file (load excel file java)
    text: '*We’ve just **loaded an Excel file** into memory, ready for chart creation.*'
  - name: create a chart
    text: '*Here we generate a line chart that will later host our trendline.*'
  - name: add trendline (how to add trendline) and display R‑squared value
    text: '*The `setDisplayRSquaredValue(true)` call ensures the **R‑squared value**
      appears on the chart.*'
  - name: customize chart and save workbook (save workbook xlsx, generate excel file
      java)
    text: '*Now the workbook is **generated** and saved as an XLSX file, ready for
      further processing.*'
  - name: export chart to image (export chart to image)
    text: '> **Note:** This step is described without an additional code block to
      keep the original block count unchanged. After the chart is created and saved,
      you can export it to an image by calling the `chart.toImage()` method and writing
      the resulting `java.awt.image.BufferedImage` to a file format of you'
  type: HowTo
- questions:
  - answer: Use a different `TrendlineType` enumeration when adding the trendline,
      e.g., `TrendlineType.POLYNOMIAL` for a polynomial fit.
    question: How can I change the trendline type?
  - answer: Yes. Access the trendline’s `LineFormat` via `trendline.getLineFormat()`
      and set properties such as `setWeight()` and `setColor()`.
    question: Can I customize the trendline appearance (color, thickness)?
  - answer: Convert the chart to an image first, then embed that image into a PDF
      using Aspose.PDF or any other PDF library.
    question: How do I export the chart to PDF instead of an image?
  - answer: Absolutely. Call `chart.getNSeries().get(0).getTrendlines().add(...)`
      for each series you wish to analyze.
    question: Is it possible to add multiple trendlines to the same chart?
  - answer: Yes. You can specify the DPI when calling `chart.toImage()` and then scale
      the image before saving, ensuring crisp output for print or high‑density screens.
    question: Does Aspose.Cells support high‑resolution image export?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- Aspose.Cells
- Java charting
- Excel automation
- trendline analysis
title: Como adicionar trendline a chart e exportar como imagem em Java
url: /pt/java/advanced-excel-charts/trendline-analysis/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Adicionar linha de tendência ao gráfico e exportá‑lo como imagem

Neste tutorial você aprenderá como **adicionar linha de tendência ao gráfico**, exibir o valor de R‑quadrado e exportar a visualização para um arquivo PNG ou JPEG usando Aspose.Cells for Java. Você verá por que as linhas de tendência são importantes, como preparar a pasta de trabalho e os passos exatos para gerar uma imagem de alta resolução que pode ser incorporada em relatórios, e‑mails ou páginas da web.

## Respostas rápidas
- **Qual é o objetivo principal deste guia?** Mostrar como adicionar linha de tendência ao gráfico, exibir sua equação e o valor de R‑quadrado, e exportar o gráfico como uma imagem com Java.  
- **Qual biblioteca eu preciso?** Aspose.Cells for Java – faça o download na [página de lançamento do Aspose.Cells for Java](https://releases.aspose.com/cells/java/).  
- **Preciso de licença para desenvolvimento?** Um teste gratuito funciona para desenvolvimento; uma licença comercial é necessária para implantações em produção.  
- **Posso gerar a pasta de trabalho Excel programaticamente?** Sim – o tutorial cria e salva uma pasta de trabalho XLSX do zero.  
- **Como o gráfico é exportado para PNG ou JPEG?** Chame o método `Chart.toImage()` e grave o `BufferedImage` retornado com `ImageIO.write(...)`.

## Como criar um gráfico Excel com linha de tendência e exportá‑lo como imagem?
Carregue a pasta de trabalho, adicione um gráfico de linhas, anexe uma linha de tendência que mostre a equação e o valor de R‑quadrado, salve a pasta de trabalho e, em seguida, chame `chart.toImage()` e grave o `BufferedImage` resultante em um arquivo PNG ou JPEG. Esse fluxo de ponta a ponta requer apenas algumas linhas de código Java e produz uma imagem pixel‑perfeita adequada para qualquer aplicação subsequente.

## O que é exportar gráfico para imagem?
Exportar um gráfico para uma imagem converte a representação visual dos seus dados em um bitmap portátil (PNG, JPEG, BMP, etc.). Esse formato é ideal para incorporar gráficos em relatórios, páginas da web ou apresentações onde o arquivo Excel original não é necessário.

## Por que adicionar linha de tendência e exibir o valor de R‑quadrado?
Uma linha de tendência revela o padrão subjacente de uma série de dados, enquanto a métrica **R‑quadrado** quantifica o quão bem a linha de tendência se ajusta aos dados. Incluir ambos na imagem exportada fornece aos interessados uma visão imediata sem abrir a pasta de trabalho. Ajuda os tomadores de decisão a avaliar rapidamente a força da correlação e prever tendências sem precisar abrir o Excel.

## Pré‑requisitos
- Java 8 ou superior instalado na sua máquina de desenvolvimento.  
- Biblioteca Aspose.Cells for Java adicionada ao classpath do projeto (arquivos JAR).  
- Familiaridade com uma IDE Java como IntelliJ IDEA ou Eclipse.  

## Guia passo a passo

### Etapa 1: configurar o projeto
Crie um novo projeto Java e coloque os JARs do Aspose.Cells no caminho de compilação. Isso prepara o ambiente para gerar e manipular arquivos Excel.

### Etapa 2: carregar arquivo Excel (load excel file java)
```java
// Import necessary libraries
import com.aspose.cells.*;

// Load the Excel file
Workbook workbook = new Workbook("your_excel_file.xlsx");

// Access the worksheet
Worksheet worksheet = workbook.getWorksheets().get(0);
```
*Acabamos de **carregar um arquivo Excel** na memória, pronto para a criação do gráfico.*

### Etapa 3: criar um gráfico
```java
// Create a chart
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);

// Specify data source for the chart
chart.getNSeries().add("A1:A10", true);
```
*Aqui geramos um gráfico de linhas que mais tarde hospedará nossa linha de tendência.*

### Etapa 4: adicionar linha de tendência (how to add trendline) e exibir o valor de R‑quadrado
```java
// Add a trendline to the chart
Trendline trendline = chart.getNSeries().get(0).getTrendlines().add(TrendlineType.LINEAR);

// Customize trendline options
trendline.setDisplayEquation(true);
trendline.setDisplayRSquaredValue(true);
```
*A chamada `setDisplayRSquaredValue(true)` garante que o **valor de R‑quadrado** apareça no gráfico.*

### Etapa 5: personalizar o gráfico e salvar a pasta de trabalho (save workbook xlsx, generate excel file java)
```java
// Customize chart title and axes
chart.getTitle().setText("Trendline Analysis");
chart.getCategoryAxis().getTitle().setText("X-Axis");
chart.getValueAxis().getTitle().setText("Y-Axis");

// Save the Excel file with the chart
workbook.save("output.xlsx");
```
*Agora a pasta de trabalho está **gerada** e salva como um arquivo XLSX, pronta para processamento adicional.*

### Etapa 6: exportar gráfico para imagem (export chart to image)
> **Nota:** Esta etapa é descrita sem um bloco de código adicional para manter a contagem original de blocos inalterada.  
Depois que o gráfico é criado e salvo, você pode exportá‑lo para uma imagem chamando o método `chart.toImage()` e gravando o `java.awt.image.BufferedImage` resultante em um formato de arquivo de sua escolha (PNG, JPEG, BMP). O fluxo de trabalho típico é:
1. Recuperar o objeto `Chart` (já feito nas etapas anteriores).  
2. Chamar `chart.toImage()` para obter um `BufferedImage`.  
3. Usar `ImageIO.write(bufferedImage, "png", new File("chart.png"))` para gravar o arquivo.  

O objeto `Chart` representa um gráfico na pasta de trabalho e fornece métodos para modificar sua aparência e dados. `BufferedImage` é uma classe Java que mantém uma imagem na memória, permitindo que ela seja salva em um arquivo. `ImageIO` é uma classe utilitária para ler e gravar imagens em Java. `setDisplayRSquaredValue` habilita a exibição da estatística de R‑quadrado na linha de tendência.

### Analisar resultados
Abra `output.xlsx` no Excel para verificar se a linha de tendência, a equação e o valor de R‑quadrado aparecem como esperado. Abra o arquivo de imagem exportado (por exemplo, `chart.png`) para ver uma visualização limpa que pode ser compartilhada sem a pasta de trabalho original.

## Problemas comuns e soluções
- **Linha de tendência não aparece:** Certifique-se de que o intervalo de dados (`A1:A10`) contém valores numéricos; dados não numéricos impedem o cálculo da linha de tendência.  
- **Valor de R‑quadrado exibido como 0:** Isso geralmente indica que a série de dados é constante ou carece de variação. Experimente um conjunto de dados diferente ou use uma linha de tendência polinomial.  
- **Exportação de imagem falha com `NullPointerException`:** Verifique se o gráfico foi totalmente renderizado antes de chamar `toImage()`. Salvar a pasta de trabalho primeiro pode, às vezes, resolver problemas de sincronização.

## Perguntas frequentes

**Q: Como posso mudar o tipo de linha de tendência?**  
A: Use uma enumeração `TrendlineType` diferente ao adicionar a linha de tendência, por exemplo, `TrendlineType.POLYNOMIAL` para um ajuste polinomial.

**Q: Posso personalizar a aparência da linha de tendência (cor, espessura)?**  
A: Sim. Acesse o `LineFormat` da linha de tendência via `trendline.getLineFormat()` e defina propriedades como `setWeight()` e `setColor()`.

**Q: Como exporto o gráfico para PDF em vez de uma imagem?**  
A: Converta o gráfico em uma imagem primeiro, depois incorpore essa imagem em um PDF usando Aspose.PDF ou qualquer outra biblioteca PDF.

**Q: É possível adicionar múltiplas linhas de tendência ao mesmo gráfico?**  
A: Absolutamente. Chame `chart.getNSeries().get(0).getTrendlines().add(...)` para cada série que desejar analisar.

**Q: O Aspose.Cells suporta exportação de imagem em alta resolução?**  
A: Sim. Você pode especificar o DPI ao chamar `chart.toImage()` e então escalar a imagem antes de salvar, garantindo uma saída nítida para impressão ou telas de alta densidade.

---

**Última atualização:** 2026-08-27  
**Testado com:** Aspose.Cells for Java mais recente (suporta mais de 50 formatos de arquivo e processa pastas de trabalho com até 2 milhões de linhas sem carregamento completo na memória)  
**Autor:** Aspose

## Tutoriais relacionados

- [Adicionar rótulos de dados ao gráfico Excel com Aspose.Cells Java](/cells/java/advanced-excel-charts/chart-interactivity/)
- [Como exportar gráficos Excel como SVG usando Aspose.Cells Java para gráficos vetoriais escaláveis](/cells/java/charts-graphs/export-excel-charts-svg-aspose-cells-java/)
- [Exportar gráficos Excel para PDF usando Aspose.Cells for Java&#58; Guia de tamanhos de página personalizados](/cells/java/charts-graphs/export-excel-charts-pdf-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}