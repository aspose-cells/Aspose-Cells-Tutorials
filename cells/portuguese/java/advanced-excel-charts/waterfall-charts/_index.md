---
date: 2026-09-02
description: Aprenda como criar excel waterfall chart em Java com Aspose.Cells, definir
  o intervalo de dados do gráfico, personalizar rótulos e exportar para XLSX.
keywords:
- create excel waterfall chart
- waterfall chart data labels
- Aspose.Cells Java chart
lastmod: 2026-09-02
linktitle: Gráficos Waterfall
og_description: Criar excel waterfall chart usando Aspose.Cells para Java – definir
  o intervalo de dados do gráfico, adicionar rótulos de dados e exportar para XLSX
  em poucos passos.
og_image_alt: 'Tutorial: create excel waterfall chart with Aspose.Cells Java'
og_title: Criar excel waterfall chart com Aspose.Cells para Java
schemas:
- author: Aspose
  dateModified: '2026-09-02'
  description: Learn how to create excel waterfall chart in Java with Aspose.Cells,
    set the chart data range, customize labels and export to XLSX.
  headline: Create excel waterfall chart with Aspose.Cells for Java
  type: TechArticle
- description: Learn how to create excel waterfall chart in Java with Aspose.Cells,
    set the chart data range, customize labels and export to XLSX.
  name: Create excel waterfall chart with Aspose.Cells for Java
  steps:
  - name: import Aspose.Cells
    text: The `com.aspose.cells` package contains all classes required for Excel manipulation,
      including workbook creation, worksheet handling, and chart generation.
  - name: initialize workbook and worksheet
    text: A **Workbook** represents an Excel file, and a **Worksheet** is a single
      sheet within that file. Creating these objects provides the canvas for both
      raw data and the chart.
  - name: enter data
    text: Column A holds category labels, while column B contains the numeric values
      for the waterfall. This layout matches the typical profit‑and‑loss flow used
      in financial analysis.
  - name: create the waterfall chart
    text: The **Chart** object creates a visual representation; setting its type to
      `ChartType.WATERFALL` configures it as a waterfall chart. Use the `add` method
      to set the chart data range for the series (`"B2:B6"`), and link the category
      axis to `"A2:A6"`.
  - name: save the workbook
    text: Saving the workbook writes the chart and data to the specified file format.
      Call `workbook.save("WaterfallChart.xlsx")` to generate an XLSX file, or change
      the format parameter to export to PDF, CSV, or HTML.
  type: HowTo
- questions:
  - answer: Use the `add` method on the chart’s series, passing the cell range that
      contains your values, e.g., `"B2:B6"`.
    question: How do I set the chart data range for a financial waterfall chart?
  - answer: Yes, call `workbook.save("WaterfallChart.pdf", SaveFormat.PDF);` to generate
      a PDF version.
    question: Can I export the workbook to PDF instead of XLSX?
  - answer: Extend the data range in both the values column and the category column,
      then update the `add` and `setCategoryData` calls accordingly.
    question: What if I need to create a waterfall chart with more categories?
  - answer: Iterate through the `Series` collection and set the `FillFormat` color
      based on each value’s sign; Aspose.Cells lets you apply conditional formatting
      programmatically.
    question: Is there a way to automatically format positive and negative bars?
  - answer: Yes. After modifying cell values, simply re‑save the workbook—the chart
      will reflect the new data automatically.
    question: Does Aspose.Cells support dynamic data updates for charts?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- waterfall chart
- Aspose.Cells
- java excel charts
- excel automation
title: Criar excel waterfall chart com Aspose.Cells para Java
url: /pt/java/advanced-excel-charts/waterfall-charts/
weight: 18
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Gráficos de cascata

## Introdução aos gráficos de cascata usando Aspose.Cells para Java

Neste tutorial você aprenderá a **criar gráfico de cascata no Excel** e a **definir o intervalo de dados do gráfico** com Aspose.Cells para Java. Gráficos de cascata transformam uma série de números positivos e negativos em uma história visual clara, tornando-os ideais para demonstrações financeiras, revisões de desempenho de vendas e qualquer cenário em que você precise ver como itens individuais contribuem para um total.

## Respostas rápidas
- **O que é um gráfico de cascata?** Um visual que mostra como um valor inicial é aumentado e diminuído por uma série de valores intermediários, terminando com um total final.  
- **Qual biblioteca é usada?** Aspose.Cells para Java.  
- **Preciso de uma licença?** Um teste gratuito funciona para desenvolvimento; uma licença comercial é necessária para produção.  
- **Posso salvar o arquivo como XLSX?** Sim – use `workbook.save("FileName.xlsx")`.  
- **É adequado para visualização de dados em Java?** Absolutamente; Aspose.Cells fornece recursos avançados de gráficos sem necessidade do Office instalado.

## O que é um gráfico de cascata?
Um gráfico de cascata exibe contribuições positivas e negativas sequenciais a um valor inicial, ajudando você a entender como cada componente impacta o resultado geral. Ao visualizar ganhos e perdas lado a lado, ele torna fluxos financeiros complexos instantaneamente legíveis.

## Por que usar Aspose.Cells para Java para adicionar um gráfico de cascata?
Aspose.Cells permite gerar gráficos do Excel em qualquer servidor, pipeline CI ou desktop sem precisar do Microsoft Excel. Ele suporta **mais de 15 formatos de saída** (XLSX, PDF, HTML, CSV e mais), processa pastas de trabalho com **mais de 500 linhas** em menos de um segundo e oferece controle programático sobre cada elemento do gráfico — de cores a rótulos de dados.

## Pré‑requisitos

Antes de mergulharmos no código, certifique‑se de que você tem os seguintes pré‑requisitos configurados:

- Aspose.Cells para Java: Você precisará ter o Aspose.Cells para Java instalado. Você pode baixá‑lo na página de lançamentos do Aspose.Cells para Java: [Aspose.Cells for Java releases](https://releases.aspose.com/cells/java/).
- Ambiente de desenvolvimento Java: Garanta que o Java esteja instalado em seu sistema e que uma ferramenta de build (Maven/Gradle) esteja pronta.

Agora, vamos começar a criar o gráfico de cascata passo a passo.

## Como definir o intervalo de dados do gráfico para um gráfico de cascata em Java
Carregue uma nova pasta de trabalho, preencha‑a com dados, adicione um objeto `Chart`, defina o intervalo da série e, finalmente, salve o arquivo. Esse processo é simples: você cria uma pasta de trabalho, preenche células com categorias e valores, cria um gráfico, vincula os intervalos de dados e, então, exporta a pasta de trabalho. O resultado é um gráfico de cascata totalmente funcional pronto para uso em relatórios ou dashboards.

### Etapa 1: importar Aspose.Cells
O pacote `com.aspose.cells` contém todas as classes necessárias para manipulação do Excel, incluindo criação de pastas de trabalho, manipulação de planilhas e geração de gráficos.

### Etapa 2: inicializar pasta de trabalho e planilha
Um **Workbook** representa um arquivo Excel, e um **Worksheet** é uma única aba dentro desse arquivo. Criar esses objetos fornece a base tanto para os dados brutos quanto para o gráfico.

### Etapa 3: inserir dados
A coluna A contém rótulos de categoria, enquanto a coluna B contém os valores numéricos para a cascata. Esse layout corresponde ao fluxo típico de lucro‑e‑prejuízo usado em análises financeiras.

### Etapa 4: criar o gráfico de cascata
O objeto **Chart** cria a representação visual; definir seu tipo como `ChartType.WATERFALL` o configura como um gráfico de cascata. Use o método `add` para definir o intervalo de dados do gráfico para a série (`"B2:B6"`), e vincule o eixo de categorias a `"A2:A6"`.

### Etapa 5: salvar a pasta de trabalho
Salvar a pasta de trabalho grava o gráfico e os dados no formato de arquivo especificado. Chame `workbook.save("WaterfallChart.xlsx")` para gerar um arquivo XLSX, ou altere o parâmetro de formato para exportar para PDF, CSV ou HTML.

## Problemas comuns e soluções

- **O gráfico aparece em branco** – Verifique se as referências de intervalo de dados (`B2:B6` e `A2:A6`) correspondem às células reais que contêm seus valores e categorias.  
- **Valores negativos não são exibidos corretamente** – Certifique‑se de que o tipo da série esteja definido como `ChartType.WATERFALL`; outros tipos de gráfico tratam negativos de forma diferente.  
- **Arquivo não abre no Excel** – Use a versão mais recente do Aspose.Cells e confirme se a extensão do arquivo corresponde ao formato (`.xlsx` para Excel).

## Perguntas frequentes

### Como posso personalizar a aparência do meu gráfico de cascata?
Você pode modificar propriedades como `Chart.getSeries().get(0).getFillFormat().setColor(Color.getRed())` para mudar a cor das barras, habilitar rótulos de dados com `setShowDataLabels(true)` e ajustar os títulos dos eixos através de `getCategoryAxis().setTitle("Stage")`. A referência da API Aspose.Cells fornece uma lista completa de opções personalizáveis.

### Posso criar vários gráficos de cascata na mesma planilha?
Sim. Após adicionar o primeiro gráfico, repita as etapas de criação do gráfico com um intervalo de dados diferente e um novo objeto `Chart`. Cada gráfico é independente e pode ser posicionado em qualquer lugar da planilha.

### O Aspose.Cells é compatível com diferentes ambientes de desenvolvimento Java?
Absolutamente. A biblioteca funciona com Eclipse, IntelliJ IDEA, NetBeans e qualquer sistema de build que suporte Maven ou Gradle. Nenhum plugin adicional é necessário.

### Posso adicionar séries de dados adicionais ao meu gráfico de cascata?
Você pode adicionar mais séries chamando `chart.getNSeries().add("C2:C6", true)` e configurando cada série separadamente. Isso permite comparar múltiplos cenários lado a lado.

### Onde posso encontrar mais recursos e exemplos para Aspose.Cells para Java?
Explore a documentação completa na referência da API Aspose.Cells Java: [Aspose.Cells Java API reference](https://reference.aspose.com/cells/java/).

## FAQ

**P: Como definir o intervalo de dados do gráfico para um gráfico de cascata financeiro?**  
R: Use o método `add` na série do gráfico, passando o intervalo de células que contém seus valores, por exemplo, `"B2:B6"`.

**P: Posso exportar a pasta de trabalho para PDF em vez de XLSX?**  
R: Sim, chame `workbook.save("WaterfallChart.pdf", SaveFormat.PDF);` para gerar uma versão em PDF.

**P: E se eu precisar criar um gráfico de cascata com mais categorias?**  
R: Expanda o intervalo de dados tanto na coluna de valores quanto na coluna de categorias, então atualize as chamadas `add` e `setCategoryData` de acordo.

**P: Existe uma maneira de formatar automaticamente barras positivas e negativas?**  
R: Percorra a coleção `Series` e defina a cor `FillFormat` com base no sinal de cada valor; o Aspose.Cells permite aplicar formatação condicional programaticamente.

**P: O Aspose.Cells suporta atualizações dinâmicas de dados para gráficos?**  
R: Sim. Após modificar os valores das células, basta salvar novamente a pasta de trabalho — o gráfico refletirá os novos dados automaticamente.

---

**Última atualização:** 2026-09-02  
**Testado com:** Aspose.Cells para Java (última versão)  
**Autor:** Aspose  









```java
import com.aspose.cells.*;
```

```java
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```

```java
Cells cells = worksheet.getCells();

// Insert data
cells.get("A1").putValue("Categories");
cells.get("A2").putValue("Start");
cells.get("A3").putValue("Positive Value 1");
cells.get("A4").putValue("Negative Value 1");
cells.get("A5").putValue("Positive Value 2");
cells.get("A6").putValue("End");

cells.get("B1").putValue("Values");
cells.get("B2").putValue(0);
cells.get("B3").putValue(20);
cells.get("B4").putValue(-10);
cells.get("B5").putValue(15);
cells.get("B6").putValue(25);
```

```java
int chartIndex = worksheet.getCharts().add(ChartType.WATERFALL, 5, 0, 15, 5);
Chart waterfallChart = worksheet.getCharts().get(chartIndex);
waterfallChart.getNSeries().add("B2:B6", true);
waterfallChart.getNSeries().setCategoryData("A2:A6");
```

```java
workbook.save("WaterfallChart.xlsx");
```

## Tutoriais relacionados

- [Customize Excel Chart Data Labels Using Aspose.Cells for Java: A Step-by-Step Guide](/cells/java/charts-graphs/customize-chart-data-labels-aspose-cells-java/)
- [Add Data Labels to Excel Chart with Aspose.Cells Java](/cells/java/advanced-excel-charts/chart-interactivity/)
- [How to Create and Export Charts in Java Using Aspose.Cells: A Complete Guide](/cells/java/charts-graphs/aspose-cells-java-create-export-charts/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}