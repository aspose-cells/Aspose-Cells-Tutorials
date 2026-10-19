---
date: 2026-08-21
description: Aprenda a adicionar dicas de ferramenta, rótulos de dados e alterar o
  tipo de gráfico em gráficos do Excel usando Aspose.Cells for Java – guia passo a
  passo com exemplos interativos.
keywords:
- how to add tooltips
- how to change chart type
- how to add data labels
lastmod: 2026-08-21
linktitle: Alterar Tipo de Gráfico do Excel
og_description: Aprenda a adicionar dicas de ferramenta, rótulos de dados e alterar
  o tipo de gráfico em gráficos do Excel usando Aspose.Cells for Java – guia passo
  a passo com exemplos interativos.
og_image_alt: 'Developer guide: Adding tooltips and data labels to Excel charts with
  Aspose.Cells for Java'
og_title: Como adicionar dicas de ferramenta e rótulos de dados a gráficos do Excel
  em Java
schemas:
- author: Aspose
  dateModified: '2026-08-21'
  description: Learn how to add tooltips, data labels, and change chart type in Excel
    charts using Aspose.Cells for Java – step‑by‑step guide with interactive examples.
  headline: How to add tooltips and data labels to Excel charts in Java
  type: TechArticle
- questions:
  - answer: You need to create a new chart with the desired `ChartType`. Aspose.Cells
      does not provide an in‑place type conversion, so remove the old chart and add
      a new one.
    question: How can I change the chart type after it’s created?
  - answer: Yes. Use the `DataLabel` properties such as `setFontSize`, `setFontColor`,
      and `setBackgroundColor` to style the tooltip text.
    question: Can I customize the appearance of tooltips?
  - answer: Export the workbook to an HTML or XLSX file and use JavaScript on the
      client side to capture click events on chart elements.
    question: How do I handle user interactions in a web application?
  - answer: Visit the [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/)
      for a full list of chart‑related classes and methods.
    question: Where can I find more examples and documentation?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- Aspose.Cells
- Java chart
- Excel interactivity
- tooltips
- data labels
title: Como adicionar dicas de ferramenta e rótulos de dados a gráficos do Excel em
  Java
url: /pt/java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Adicionar rótulos de dados ao gráfico do Excel e alterar o tipo de gráfico – Aspose.Cells Java

Gráficos interativos dão aos seus relatórios do Excel um novo nível de insight, e **como adicionar tooltips** torna a informação instantaneamente legível. Neste tutorial você aprenderá como **adicionar rótulos de dados ao gráfico do Excel**, **alterar o tipo de gráfico**, e criar soluções Java interativas com Aspose.Cells. Também mostraremos como adicionar tooltips e um hyperlink simples de drill‑down para que seu público possa explorar os dados em profundidade.

## Respostas rápidas
- **Qual biblioteca é usada?** Aspose.Cells for Java  
- **Posso alterar o tipo de gráfico?** Sim – basta modificar o enum `ChartType` ao criar o gráfico.  
- **Como adiciono tooltips a um gráfico?** Use a API de rótulo de dados (`setHasDataLabels(true)`) e habilite a exibição de valores.  
- **Drill‑down é suportado?** Você pode anexar hyperlinks a pontos de dados para comportamento básico de drill‑down.  
- **Pré‑requisitos?** IDE Java, Aspose.Cells JAR e um arquivo Excel com dados de exemplo.

## O que é como adicionar tooltips?
**Como adicionar tooltips** refere‑se ao processo de habilitar texto ao passar o mouse que exibe o valor de um ponto de dados ou informações personalizadas em um gráfico do Excel. No Aspose.Cells isso é conseguido através das configurações de rótulo de dados do gráfico. Tooltips ajudam os usuários a entender rapidamente os dados sem sobrecarregar o gráfico, e podem ser personalizados quanto a fonte, cor e formato.

## Por que usar gráficos interativos com Aspose.Cells?
Aspose.Cells suporta **mais de 50 formatos de entrada e saída**—incluindo XLSX, CSV, PDF e HTML—e pode processar pastas de trabalho com **mais de 1 000 planilhas** sem carregar o arquivo inteiro na memória, oferecendo geração rápida de gráficos no lado do servidor para relatórios corporativos. Gráficos interativos também permitem a incorporação de hyperlinks, atualizações dinâmicas de dados e exportação para formatos web‑friendly, tornando‑os ideais para dashboards e portais de relatórios.

## Pré‑requisitos

Antes de começar, certifique‑se de que você tem o seguinte:

- Ambiente de desenvolvimento Java (JDK 8+ recomendado)  
- Biblioteca Aspose.Cells for Java (download na [página de download do Aspose.Cells for Java](https://releases.aspose.com/cells/java/))  
- Uma pasta de trabalho de exemplo (`data.xlsx`) contendo os dados que você deseja visualizar  

## Etapa 1: configurando seu projeto Java

1. Crie um novo projeto Java na sua IDE favorita (IntelliJ IDEA, Eclipse, etc.).  
2. Adicione o Aspose.Cells JAR ao caminho de compilação do seu projeto ou às dependências Maven/Gradle.

## Etapa 2: carregando dados

Para trabalhar com gráficos, primeiro você precisa de uma pasta de trabalho carregada na memória.

A classe `Workbook` representa um arquivo Excel, e `Worksheet` representa uma única planilha dentro desse arquivo.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## Como alterar o tipo de gráfico no Aspose.Cells?

Crie um novo gráfico com o enum `ChartType` desejado; o Aspose.Cells não modifica o tipo de um gráfico existente in‑place, portanto você deve adicionar um novo gráfico do tipo correto e, opcionalmente, remover o antigo. Essa abordagem garante que todas as séries e eixos sejam reconstruídos corretamente para a nova representação visual.

## Etapa 3: criando um gráfico (e alterando seu tipo)

Você pode escolher qualquer tipo de gráfico que se ajuste à sua análise. Abaixo criamos um **gráfico de colunas**, mas você pode facilmente mudar para um gráfico de linhas, pizza ou barras alterando o enum `ChartType`.

O objeto `Chart` fornece métodos para configurar a representação visual dos dados na planilha.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

> **Dica profissional:** Para **alterar o tipo de gráfico do Excel**, substitua `ChartType.COLUMN` por `ChartType.LINE`, `ChartType.PIE`, etc.

## Como adicionar tooltips a um gráfico do Excel?

Carregue seu gráfico, habilite os rótulos de dados e defina a flag `showValue`. O tooltip então exibirá o valor da célula subjacente sempre que o usuário passar o mouse sobre um ponto de dados no arquivo Excel renderizado ou na visualização HTML. Você também pode personalizar a fonte, cor e plano de fundo do tooltip para combinar com o estilo do seu relatório.

A classe `DataLabel` controla a aparência e o conteúdo dos rótulos de dados, que também servem como tooltips.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

## Etapa 4: adicionando interatividade

### 4.1. Adicionando tooltips (add tooltips to chart)

Tooltips aparecem quando o usuário passa o mouse sobre um ponto de dados. O código a seguir habilita rótulos de dados e mostra o valor como tooltip.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

### 4.2. Adicionando rótulos de dados – **add data labels to excel chart**

Rótulos de dados fornecem uma pista visual permanente no próprio gráfico. Você pode exibi‑los como balões para melhor legibilidade.

A classe `DataLabel` controla a aparência dos rótulos em cada série. Ao chamar `setHasDataLabels(true)` e configurar propriedades como `setShowValue(true)`, você incorpora o valor numérico diretamente no gráfico, tornando‑o instantaneamente visível sem qualquer interação. Opções adicionais permitem mostrar nomes de séries, porcentagens ou texto personalizado para um contexto mais rico.

> **Por que adicionar rótulos de dados?** Incluir rótulos de dados diretamente no gráfico elimina a necessidade de o usuário passar o mouse ou adivinhar valores, melhorando a clareza do relatório.

### 4.3. Implementando drill‑down (hyperlink em um ponto de dados)

Uma maneira simples de adicionar capacidade de drill‑down é anexar um hyperlink a um ponto específico. Clicar no ponto abre uma página web com informações detalhadas.

A classe `Hyperlink` anexa um link clicável a um elemento do gráfico, habilitando a navegação de drill‑down.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

## Como adicionar rótulos de dados a um gráfico do Excel?

A classe `DataLabel` controla a aparência dos rótulos em cada série. Ao chamar `setHasDataLabels(true)` e configurar propriedades como `setShowValue(true)`, você incorpora o valor numérico diretamente no gráfico, tornando‑o instantaneamente visível sem qualquer interação. Opções adicionais permitem mostrar nomes de séries, porcentagens ou texto personalizado para um contexto mais rico.

## Etapa 5: salvando a pasta de trabalho

Depois de configurar o gráfico, persista a pasta de trabalho para que os recursos interativos sejam armazenados no arquivo de saída.

Chamar `workbook.save` grava a pasta de trabalho modificada em um arquivo no formato escolhido.

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## Problemas comuns & soluções

| Problema | Solução |
|----------|----------|
| **Tooltips não aparecem** | Certifique‑se de que `setHasDataLabels(true)` seja chamado antes de configurar `setShowValue(true)`. |
| **Hyperlink não é clicável** | Verifique se o formato de saída suporta hyperlinks (por exemplo, XLSX, não CSV). |
| **Tipo de gráfico não muda** | Verifique se você modificou o enum `ChartType` correto ao adicionar o gráfico. |

## Perguntas frequentes

**P: Como posso mudar o tipo de gráfico depois que ele foi criado?**  
R: Você precisa criar um novo gráfico com o `ChartType` desejado. O Aspose.Cells não fornece conversão in‑place, portanto remova o gráfico antigo e adicione um novo.

**P: Posso personalizar a aparência dos tooltips?**  
R: Sim. Use as propriedades da `DataLabel` como `setFontSize`, `setFontColor` e `setBackgroundColor` para estilizar o texto do tooltip.

**P: Como trato interações do usuário em uma aplicação web?**  
R: Exporte a pasta de trabalho para um arquivo HTML ou XLSX e use JavaScript no lado do cliente para capturar eventos de clique nos elementos do gráfico.

**P: Onde posso encontrar mais exemplos e documentação?**  
R: Visite a [Referência da API Aspose.Cells Java](https://reference.aspose.com/cells/java/) para uma lista completa de classes e métodos relacionados a gráficos.

## Conclusão

Agora você sabe como **adicionar rótulos de dados ao gráfico do Excel**, **alterar o tipo de gráfico do Excel**, **criar soluções Java de gráficos interativos**, e enriquecê‑los com tooltips, rótulos de dados e hyperlinks de drill‑down usando Aspose.Cells for Java. Essas melhorias tornam seus relatórios do Excel muito mais envolventes e perspicazes para os usuários finais.

---

**Última atualização:** 2026-08-21  
**Testado com:** Aspose.Cells for Java 24.12  
**Autor:** Aspose

## Tutoriais relacionados

- [Como modificar gráficos e rótulos de dados do Excel usando Aspose.Cells for Java](/cells/java/charts-graphs/aspose-cells-java-modify-excel-charts-data-labels/)
- [Extrair rótulos de eixo de gráfico do Excel usando Aspose.Cells Java: Um guia abrangente](/cells/java/charts-graphs/aspose-cells-java-excel-chart-axis-labels/)
- [Criar gráficos de bolha no Excel usando Aspose.Cells for Java: Um guia passo a passo](/cells/java/charts-graphs/aspose-cells-java-create-bubble-charts/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}