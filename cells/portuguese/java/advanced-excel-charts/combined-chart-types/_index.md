---
date: 2026-09-02
description: Aprenda como exportar gráfico para PNG, adicionar série de dados, combinar
  gráfico de linha e coluna, salvar a pasta de trabalho como XLSX e adicionar legenda
  ao gráfico usando Aspose.Cells for Java.
keywords:
- export chart to png
- combine line and column chart
- save workbook as xlsx
- generate chart image java
lastmod: 2026-09-02
linktitle: Exportar gráfico para PNG e adicionar série de dados para gráfico combinado
og_description: Exportar gráfico para PNG com Aspose.Cells for Java, combinar gráfico
  de linha e coluna, adicionar série de dados e salvar a pasta de trabalho como XLSX
  em um único tutorial.
og_image_alt: Developer guide showing combined line‑column chart export to PNG using
  Aspose.Cells for Java
og_title: Exportar gráfico para PNG e adicionar série de dados para gráfico combinado
schemas:
- author: Aspose
  dateModified: '2026-09-02'
  description: Learn how to export chart to PNG, add data series, combine line column
    chart, save workbook as XLSX and add legend chart using Aspose.Cells for Java.
  headline: Export chart to PNG and add data series for combined chart
  type: TechArticle
- description: Learn how to export chart to PNG, add data series, combine line column
    chart, save workbook as XLSX and add legend chart using Aspose.Cells for Java.
  name: Export chart to PNG and add data series for combined chart
  steps:
  - name: import aspose.cells classes
    text: '`Workbook` is Aspose.Cells’ core object that represents an entire Excel
      file in memory.'
  - name: create a new workbook
    text: '`Worksheet` represents a single sheet inside a `Workbook` and provides
      access to cells, rows, and charts.'
  - name: access the first worksheet
    text: '`Chart` is the object that holds all chart‑related settings, series, and
      rendering options.'
  - name: add a combined chart object to the worksheet
    text: We’ll start with a line chart and later add a column series to achieve a
      **combined line column chart** effect.
  - name: define the data ranges and add data series
    text: '`NSeries` is the collection that stores each data series for a chart. Adding
      a series links a range of cells to the chart. > **Pro tip:** The first parameter
      (`"A1:A5"`) is the range for the first series, and the second (`"B1:B5"`) creates
      a second series that will be combined with the first.'
  - name: set the category (X‑axis) data
    text: '`CategoryAxis` represents the horizontal axis of the chart, controlling
      the labels displayed along the X‑axis.'
  - name: set chart axis labels and title
    text: '`Title` sets the main title of the chart, and `Axis` objects represent
      the X and Y axes.'
  - name: add legend chart and adjust its position
    text: '`Legend` controls the placement and appearance of the series legend in
      the chart.'
  - name: save the workbook as an Excel file (XLSX)
    text: '`Workbook.save` writes the in‑memory workbook to a file in the specified
      format.'
  - name: export chart to PNG
    text: '`Chart.toImage` renders the chart as an image file in the chosen format.
      > The `chart.toImage` method **generates Excel chart** images that can be used
      in web pages, reports, or emails.'
  type: HowTo
- questions:
  - answer: 'Download the JAR from the official site and add it to your project’s
      classpath. The download link is: [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/).'
    question: How do I install Aspose.Cells for Java?
  - answer: Yes, Aspose.Cells supports bar, pie, scatter, area, and many more chart
      types. Refer to the API documentation for the full list.
    question: Can I create other chart types besides line and column?
  - answer: A valid Aspose.Cells license is required for production deployments. A
      free trial is available for evaluation.
    question: Is a license required for production use?
  - answer: Use `chart.getNSeries().get(i).setAreaColor(Color.getRed())` (or similar)
      after adding the series.
    question: How can I change the colors of each series?
  - answer: 'Comprehensive documentation and additional samples are available at the
      Aspose reference site: [Aspose Cells Java reference documentation](https://reference.aspose.com/cells/java/).'
    question: Where can I find more code examples?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- export chart to png
- Aspose.Cells
- Java Excel charts
title: Exportar gráfico para PNG e adicionar série de dados para gráfico combinado
url: /pt/java/advanced-excel-charts/combined-chart-types/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exportar gráfico para PNG e adicionar série de dados para gráfico combinado

Neste tutorial você **adicionará séries de dados** a uma pasta de trabalho Excel, **combinará elementos de gráfico de linha e coluna**, e aprenderá como **exportar o gráfico para PNG** usando Aspose.Cells for Java. Vamos percorrer cada passo — desde a configuração da pasta de trabalho, adicionando o gráfico a uma planilha, personalizando a legenda, até **salvar a pasta de trabalho como XLSX** e gerar uma imagem PNG do gráfico. Ao final, você terá um gráfico combinado pronto para uso que pode ser incorporado em relatórios ou painéis.

## Respostas rápidas
- **Qual biblioteca cria gráficos combinados?** Aspose.Cells for Java.  
- **Como adiciono uma série de dados?** Chame `chart.getNSeries().add(...)` com o intervalo apropriado.  
- **Como posso exportar o gráfico para PNG?** Use `chart.toImage("chart.png", ImageFormat.getPng())`.  
- **Em que formato de arquivo posso salvar a pasta de trabalho?** `.xlsx` padrão (salvar a pasta de trabalho como XLSX).  
- **Preciso de uma licença para produção?** Sim – uma licença válida do Aspose.Cells é necessária para implantações em produção.

## O que é exportar gráfico para PNG no Aspose.Cells?
Exportar um gráfico para PNG cria uma imagem raster do gráfico do Excel que pode ser exibida em páginas da web, relatórios ou e‑mails sem exigir o aplicativo Excel. Esse método captura o layout visual exato, cores e marcadores de dados, produzindo um arquivo de imagem portátil.

## Por que criar um gráfico combinado de linha e coluna?
Um gráfico combinado de linha‑coluna permite exibir diferentes conjuntos de dados com representações visuais distintas (por exemplo, uma série de linha sobre uma série de coluna) em uma única visualização. Essa abordagem é ideal para comparar tendências com totais, destacar correlações ou fornecer insights mais ricos mantendo a pegada visual pequena.

## Pré‑requisitos
- Java Development Kit (JDK) 8 ou superior  
- Biblioteca Aspose.Cells for Java (download no link abaixo)  
- Familiaridade básica com a sintaxe Java e conceitos do Excel  

## Começando

Primeiro, faça o download da biblioteca Aspose.Cells for Java no site oficial:

[Baixar Aspose.Cells for Java](https://releases.aspose.com/cells/java/)

Depois que o JAR for adicionado ao classpath do seu projeto, você pode começar a criar o gráfico.

### Etapa 1: importar classes aspose.cells
`Workbook` é o objeto central do Aspose.Cells que representa um arquivo Excel completo na memória.  
```java
import com.aspose.cells.*;
```

### Etapa 2: criar uma nova pasta de trabalho
`Worksheet` representa uma única planilha dentro de um `Workbook` e fornece acesso a células, linhas e gráficos.  
```java
Workbook workbook = new Workbook();
```

### Etapa 3: acessar a primeira planilha
`Chart` é o objeto que contém todas as configurações relacionadas ao gráfico, séries e opções de renderização.  
```java
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### Etapa 4: adicionar um objeto de gráfico combinado à planilha  
Começaremos com um gráfico de linha e, posteriormente, adicionaremos uma série de coluna para alcançar o efeito de **gráfico combinado de linha e coluna**.  
```java
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 0, 0, 20, 10);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## Adicionando dados ao gráfico

Agora que o contêiner do gráfico existe, precisamos alimentá‑lo com dados.

### Etapa 5: definir os intervalos de dados e adicionar séries de dados
`NSeries` é a coleção que armazena cada série de dados para um gráfico. Adicionar uma série vincula um intervalo de células ao gráfico.  
```java
Cells cells = worksheet.getCells();
chart.getNSeries().add("A1:A5", true);
chart.getNSeries().add("B1:B5", true);
```
> **Dica profissional:** O primeiro parâmetro (`"A1:A5"`) é o intervalo para a primeira série, e o segundo (`"B1:B5"`) cria uma segunda série que será combinada com a primeira.

### Etapa 6: definir os dados da categoria (eixo X)
`CategoryAxis` representa o eixo horizontal do gráfico, controlando os rótulos exibidos ao longo do eixo X.  
```java
chart.getNSeries().setCategoryData("C1:C5");
```

## Personalizando o gráfico

Um bom gráfico conta uma história. Vamos dar a ele títulos, rótulos de eixos e uma legenda clara.

### Etapa 7: definir rótulos dos eixos do gráfico e título
`Title` define o título principal do gráfico, e os objetos `Axis` representam os eixos X e Y.  
```java
chart.getTitle().setText("Combined Chart Example");
chart.getCategoryAxis().getTitle().setText("Categories");
chart.getValueAxis().getTitle().setText("Values");
```

### Etapa 8: adicionar legenda ao gráfico e ajustar sua posição
`Legend` controla a posição e a aparência da legenda das séries no gráfico.  
```java
chart.getLegend().setPosition(LegendPositionType.BOTTOM);
chart.getLegend().setOverlay(true);
```

## Salvando e exportando o gráfico

Depois da personalização, você desejará **salvar a pasta de trabalho como XLSX** e também gerar uma imagem.

### Etapa 9: salvar a pasta de trabalho como um arquivo Excel (XLSX)
`Workbook.save` grava a pasta de trabalho em memória em um arquivo no formato especificado.  
```java
workbook.save("CombinedChart.xlsx");
```

### Etapa 10: exportar o gráfico para PNG
`Chart.toImage` renderiza o gráfico como um arquivo de imagem no formato escolhido.  
```java
chart.toImage("CombinedChart.png", ImageFormat.getPng());
```
> O método `chart.toImage` **gera imagens de gráficos do Excel** que podem ser usadas em páginas da web, relatórios ou e‑mails.

## Problemas comuns e solução de problemas

| Problema | Solução |
|----------|---------|
| **Nenhum dado aparece** | Verifique se os intervalos de células (`A1:A5`, `B1:B5`, `C1:C5`) realmente contêm dados antes de criar o gráfico. |
| **A legenda sobrepõe o gráfico** | Defina `chart.getLegend().setOverlay(false)` ou mova a legenda para uma posição diferente (por exemplo, `RIGHT`). |
| **Arquivo de imagem está em branco** | Certifique‑se de que o gráfico tenha ao menos uma série e que `chart.toImage` seja chamado após todas as personalizações. |
| **Salvar gera uma exceção** | Verifique se você tem permissões de gravação no diretório de destino e se o arquivo não está aberto no Excel. |

## Perguntas frequentes

**Q: Como instalo o Aspose.Cells for Java?**  
A: Baixe o JAR no site oficial e adicione ao classpath do seu projeto. O link de download é: [Baixar Aspose.Cells for Java](https://releases.aspose.com/cells/java/).

**Q: Posso criar outros tipos de gráfico além de linha e coluna?**  
A: Sim, o Aspose.Cells suporta gráficos de barra, pizza, dispersão, área e muitos outros tipos. Consulte a documentação da API para a lista completa.

**Q: É necessária uma licença para uso em produção?**  
A: Uma licença válida do Aspose.Cells é necessária para implantações em produção. Um teste gratuito está disponível para avaliação.

**Q: Como posso mudar as cores de cada série?**  
A: Use `chart.getNSeries().get(i).setAreaColor(Color.getRed())` (ou similar) após adicionar a série.

**Q: Onde posso encontrar mais exemplos de código?**  
A: Documentação abrangente e exemplos adicionais estão disponíveis no site de referência da Aspose: [Documentação de referência do Aspose Cells Java](https://reference.aspose.com/cells/java/).

---

**Última atualização:** 2026-09-02  
**Testado com:** Aspose.Cells for Java versão mais recente  
**Autor:** Aspose

## Tutoriais Relacionados

- [Como adicionar rótulos a gráficos do Excel usando Aspose.Cells for Java](/cells/java/charts-graphs/adding-labels-to-charts-aspose-cells-java-tutorial/)
- [Como criar gráfico Excel com linha de tendência e exportar para imagem usando Aspose.Cells for Java](/cells/java/advanced-excel-charts/trendline-analysis/)
- [Exportar gráficos Excel para PDF usando Aspose.Cells for Java: Guia de tamanhos de página personalizados](/cells/java/charts-graphs/export-excel-charts-pdf-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}