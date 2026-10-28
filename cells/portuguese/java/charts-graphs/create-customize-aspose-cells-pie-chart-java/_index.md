---
date: '2026-09-27'
description: Aprenda a criar gráfico de pizza java usando Aspose.Cells. Guia passo
  a passo para personalizar gráfico de pizza do Excel, configurar dependência Maven
  e gerar gráficos profissionais.
keywords:
- create pie chart java
- customize excel pie chart
- maven dependency aspose cells
lastmod: '2026-09-27'
og_description: Crie gráfico de pizza java usando Aspose.Cells para Java. Aprenda
  a personalizar gráfico de pizza do Excel, adicionar dependência Maven e gerar gráficos
  profissionais em minutos.
og_image_alt: Java code generating a customized pie chart in Excel with Aspose.Cells
og_title: Criar gráfico de pizza java com Aspose.Cells – Guia Java Completo
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to create pie chart java using Aspose.Cells. Step‑by‑step
    guide to customize Excel pie chart, set up Maven dependency, and generate professional
    charts.
  headline: How to create pie chart java with Aspose.Cells
  type: TechArticle
- questions:
  - answer: Yes, repeat the chart‑creation steps for each data range; each chart is
      independent.
    question: Can I generate multiple pie charts in the same workbook?
  - answer: It does; set the chart type to `ChartType.PIE_3D` when adding the chart.
    question: Does Aspose.Cells support 3‑D pie charts?
  - answer: Use the `Workbook.setDefaultTheme` method before creating any charts.
    question: How do I apply a custom theme to all charts?
  - answer: Over 30 formats, including XLSX, CSV, PDF, and HTML.
    question: What file formats can I export the workbook to?
  - answer: Yes, a valid license removes evaluation watermarks and unlocks full functionality.
    question: Is a license required for commercial deployment?
  type: FAQPage
tags:
- Aspose.Cells
- Java charting
- Excel automation
- data visualization
title: Como criar gráfico de pizza java com Aspose.Cells
url: /pt/java/charts-graphs/create-customize-aspose-cells-pie-chart-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como criar gráfico de pizza java com Aspose.Cells

## Introdução
Criar um **pie chart** programaticamente muitas vezes parece um quebra-cabeça, especialmente quando você precisa de controle fino sobre cores, legendas e títulos. Neste guia você aprenderá como **create pie chart java** usando Aspose.Cells, e então personalizar o gráfico de pizza do Excel para combinar com sua marca ou estilo de relatório. Percorreremos a configuração do ambiente, o preenchimento de dados, a geração do gráfico e ajustes visuais — tudo sem sair do seu IDE Java.

**O que você aprenderá**
- Adicionar a **Maven dependency Aspose.Cells** ao seu projeto.
- Construir uma pasta de trabalho, preencher células com dados e gerar um gráfico de pizza.
- Aplicar cores personalizadas, títulos e legendas ao gráfico.
- Exportar a pasta de trabalho para um arquivo XLSX pronto para compartilhamento.

Antes de começar, você deve estar confortável com a sintaxe básica de Java e ter o Maven ou Gradle instalado.

## Respostas rápidas
- **Qual biblioteca cria gráficos de pizza em Java?** Aspose.Cells for Java.
- **Preciso de uma licença?** Um teste gratuito funciona para desenvolvimento; uma licença paga é necessária para produção.
- **Quais coordenadas Maven são necessárias?** `com.aspose:aspose-cells:24.10`.
- **Posso mudar as cores das fatias?** Sim, via o método `setAreaColor` em cada série.
- **O gráfico pode ser exportado para XLSX?** Absolutamente — basta chamar `workbook.save("output.xlsx")`.

## O que é um gráfico de pizza no Excel?
Um gráfico de pizza visualiza uma única série de dados como fatias proporcionais de um círculo, facilitando a comparação de partes de um todo. O ângulo de cada fatia corresponde ao seu valor relativo ao total, permitindo uma visão rápida da distribuição entre categorias como participação de mercado, alocação de orçamento ou percentuais demográficos.

## Por que usar Aspose.Cells para criar um gráfico de pizza java?
Aspose.Cells suporta mais de 50 tipos de gráficos e pode lidar com planilhas com até um milhão de linhas sem carregar o arquivo inteiro na memória. Essa vantagem de desempenho permite gerar relatórios grandes em hardware modesto, ao mesmo tempo que oferece controle fino sobre a aparência do gráfico, vinculação de dados e formatos de exportação, tornando‑a uma escolha superior em relação a muitas bibliotecas de código aberto.

## Pré-requisitos
- **Java Development Kit (JDK)** 8 ou mais recente.
- **IDE** como IntelliJ IDEA ou Eclipse.
- **Maven** ou **Gradle** para gerenciamento de dependências.
- Uma **licença de teste ou comprada do Aspose.Cells**.

### Bibliotecas e dependências necessárias
Adicione o artefato Maven do Aspose.Cells ao seu `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

Ou o equivalente no Gradle:

```gradle
implementation 'com.aspose:aspose-cells:25.3'
```

### Etapas para aquisição de licença
Aspose.Cells for Java é comercial, mas você pode começar com um teste gratuito. Visite a [purchase page](https://purchase.aspose.com/buy) para obter uma chave de licença temporária.

## Configurando Aspose.Cells para Java
Primeiro, certifique-se de que a biblioteca está no seu classpath. Após adicionar a dependência, você pode inicializar a API como mostrado abaixo.

```java
import com.aspose.cells.Workbook;

// Initialize a new workbook instance
Workbook workbook = new Workbook();
```

## Guia de implementação

### Criar e configurar uma pasta de trabalho
A classe `Workbook` representa um arquivo Excel completo na memória.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
import com.aspose.cells.Cells;
import com.aspose.cells.ChartType;
import com.aspose.cells.Chart;
import com.aspose.cells.Series;
import com.aspose.cells.Color;
import com.aspose.cells.LegendPositionType;
import com.aspose.cells.SaveFormat;
```

#### Etapa 1: instanciar uma pasta de trabalho
```java
// Creates an empty workbook instance to work with.
Workbook workbook = new Workbook();
```  
Isso cria uma nova pasta de trabalho vazia que você pode começar a preencher imediatamente.

### Acessar ou modificar células da planilha
Um `Worksheet` representa uma única planilha dentro da pasta de trabalho, contendo células, linhas e colunas.  
Você escreverá os dados que alimentam o gráfico de pizza em uma planilha.

#### Etapa 2: obter a primeira planilha e suas células
```java
// Access the first worksheet in the workbook.
Worksheet worksheet = workbook.getWorksheets().get(0);
Cells cells = worksheet.getCells();

// Put sample values used for a pie chart into specific cells.
cells.get("C3").putValue("India");
cells.get("C4").putValue("China");
cells.get("C5").parseNumber("United States", true, null);
cells.get("C6").setValue("Russia");
cells.get("C7").setValue("United Kingdom");
cells.get("C8").setValue("Others");

// Put percentage values for a pie chart into specific cells.
cells.get("D2").putValue("% of world population");
cells.get("D3").putValue(25);
cells.get("D4").putValue(30);
cells.get("D5").putValue(10);
cells.get("D6").putValue(13);
cells.get("D7").putValue(9);
cells.get("D8").putValue(13);
```  
Preencha as células com nomes de categorias e valores que o gráfico consumirá.

### Criar um gráfico de pizza
Objetos `Chart` visualizam dados em uma planilha e suportam vários tipos como pizza, coluna e linha.

#### Etapa 3: adicionar um gráfico de pizza à planilha
```java
// Create a pie chart in the worksheet.
int pieIdx = worksheet.getCharts().add(ChartType.PIE, 1, 6, 15, 14);
Chart pie = worksheet.getCharts().get(pieIdx);
```  

### Configurar séries e dados do gráfico de pizza
`Series` define o intervalo de dados e a formatação de um gráfico, vinculando células da planilha a elementos visuais.

#### Etapa 4: definir as séries para o gráfico
```java
// Configure the series data range for the chart.
pie.getNSeries().add("D3:D8", true);
pie.getNSeries().setCategoryData("=Sheet1!$C$3:$C$8");

// Link the pie chart title to a cell containing the title text.
pie.getTitle().setLinkedSource("D2");
```  

### Configurar aparência da legenda e título do gráfico
Uma `Legend` do gráfico exibe os nomes das séries e cores, ajudando os leitores a identificar cada fatia.

#### Etapa 5: personalizar a legenda e o título do gráfico
```java
// Set legend position at bottom of the chart.
pie.getLegend().setPosition(LegendPositionType.BOTTOM);

// Set font properties for the chart title.
pie.getTitle().getFont().setName("Calibri");
pie.getTitle().getFont().setSize(18);
```  

### Personalizar cores das séries do gráfico
`setAreaColor` define a cor de preenchimento de uma fatia da série do gráfico usando um valor RGB.

#### Etapa 6: alterar cores dos segmentos do pizza
```java
import com.aspose.cells.Color;

// Access and customize colors of individual pie chart segments.
Series srs = pie.getNSeries().get(0);
srs.getPoints().get(0).getArea().setForegroundColor(Color.fromArgb(0, 246, 22, 219));
srs.getPoints().get(1).getArea().setForegroundColor(Color.fromArgb(0, 51, 34, 84));
srs.getPoints().get(2).getArea().setForegroundColor(Color.fromArgb(0, 46, 74, 44));
srs.getPoints().get(3).getArea().setForegroundColor(Color.fromArgb(0, 19, 99, 44));
srs.getPoints().get(4).getArea().setForegroundColor(Color.fromArgb(0, 208, 223, 7));
srs.getPoints().get(5).getArea().setForegroundColor(Color.fromArgb(0, 222, 69, 8));
```  

### Ajustar colunas automaticamente e salvar a pasta de trabalho
`autoFitColumns` ajusta automaticamente a largura das colunas para caber o conteúdo das células.

#### Etapa 7: ajustar larguras das colunas e salvar o arquivo
```java
// Autofit all columns.
worksheet.autoFitColumns();

// Define output directory placeholder path for saving the workbook.
String outDir = "YOUR_OUTPUT_DIRECTORY";

// Save the modified workbook to an Excel file in the specified directory.
workbook.save(outDir + "/CSOrSColorsPieChart_out.xlsx", SaveFormat.XLSX);
```  

## Casos de uso comuns
- **Análise demográfica:** Mostrar a distribuição da população entre regiões.
- **Relatório de participação de mercado:** Visualizar a fatia de cada concorrente de um único olhar.
- **Alocação de orçamento:** Destacar como os fundos são divididos entre departamentos.

## Considerações de desempenho
- Liberar objetos (`workbook.dispose()`) quando não forem mais necessários para liberar memória nativa.
- Para conjuntos de dados massivos, use `WorkbookDesigner` para transmitir dados em vez de carregar tudo de uma vez.
- Perfil com Java Flight Recorder para identificar gargalos na geração de gráficos.

## Perguntas frequentes

**Q: Posso gerar vários gráficos de pizza na mesma pasta de trabalho?**  
A: Sim, repita as etapas de criação de gráfico para cada intervalo de dados; cada gráfico é independente.

**Q: O Aspose.Cells suporta gráficos de pizza 3‑D?**  
A: Sim; defina o tipo de gráfico como `ChartType.PIE_3D` ao adicionar o gráfico.

**Q: Como aplicar um tema personalizado a todos os gráficos?**  
A: Use o método `Workbook.setDefaultTheme` antes de criar quaisquer gráficos.

**Q: Para quais formatos de arquivo posso exportar a pasta de trabalho?**  
A: Mais de 30 formatos, incluindo XLSX, CSV, PDF e HTML.

**Q: É necessária uma licença para implantação comercial?**  
A: Sim, uma licença válida remove marcas d'água de avaliação e desbloqueia toda a funcionalidade.

## Conclusão
Agora você tem uma receita completa, de ponta a ponta, para **create pie chart java** com Aspose.Cells. Seguindo os passos acima, você pode gerar gráficos de pizza do Excel refinados, ajustar cores e títulos, e incorporá‑los em qualquer fluxo de relatório. Explore outros tipos de gráficos — coluna, linha, radar — para ampliar seu conjunto de ferramentas de visualização de dados.

---

**Última atualização:** 2026-09-27  
**Testado com:** Aspose.Cells 24.10 for Java  
**Autor:** Aspose

## Tutoriais relacionados

- [Personalizar rótulos de dados de gráficos do Excel usando Aspose.Cells para Java: Um guia passo a passo](/cells/java/charts-graphs/customize-chart-data-labels-aspose-cells-java/)
- [Criar gráficos dinâmicos do Excel com Aspose.Cells Java: Um guia abrangente para desenvolvedores](/cells/java/charts-graphs/aspose-cells-java-dynamic-excel-charts/)
- [Criar e personalizar pastas de trabalho do Excel usando Aspose.Cells Java: Um guia passo a passo](/cells/java/workbook-operations/create-customize-excel-workbooks-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}