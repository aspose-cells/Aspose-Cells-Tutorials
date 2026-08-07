---
date: '2026-04-08'
description: Aprenda a gerar gráfico de colunas em Java usando Aspose.Cells, abordando
  criar gráfico em Java, adicionar planilha de gráfico e exportar a pasta de trabalho
  do Excel.
keywords:
- generate column chart
- create chart java
- add chart sheet
- populate excel cells
- set chart title
- export workbook excel
title: Gerar Gráfico de Colunas com o Tutorial Aspose.Cells Java
url: /pt/java/charts-graphs/aspose-cells-java-create-customize-charts/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Gerar Gráfico de Colunas com Aspose.Cells Java

Nas aplicações orientadas por dados de hoje, **gerar um gráfico de colunas** de forma rápida e programática pode transformar números brutos em insights visuais claros. Seja construindo um painel de relatórios, uma ferramenta de análise ou um recurso simples de exportação, Aspose.Cells for Java oferece uma API fluente para **create chart java** projetos sem lidar com a interface do Excel. Neste tutorial você aprenderá como configurar a biblioteca, **populate Excel cells**, adicionar uma **chart sheet**, personalizar o **chart title**, e, finalmente, **export workbook excel** para um arquivo.

## Respostas Rápidas
- **O que significa “generate column chart”?** Cria uma visualização do tipo barra vertical a partir de dados tabulares.  
- **Qual biblioteca é necessária?** Aspose.Cells for Java (versão de avaliação gratuita disponível).  
- **Preciso de uma instalação do Excel?** Não, a biblioteca funciona independentemente do Microsoft Excel.  
- **Posso exportar para formatos além de XLS?** Sim – PDF, PNG, SVG, etc., via `workbook.save()`.  
- **É necessária uma licença para produção?** Sim, é necessária uma licença comprada ou temporária.

## O que é um generate column chart?
Um gráfico de colunas exibe séries de dados como barras verticais, facilitando a comparação de valores entre categorias como regiões, meses ou linhas de produtos. Aspose.Cells permite construir esse gráfico totalmente por código, oferecendo controle total sobre os dados, estilo e formato de saída.

## Por que usar Aspose.Cells para create chart java?
- **Sem interop COM** – funciona em qualquer SO com JVM.  
- **Opções avançadas de estilo** – imagens, gradientes, legendas e fontes personalizadas.  
- **Alto desempenho** – adequado para grandes conjuntos de dados.  
- **Múltiplos formatos de exportação** – XLS, XLSX, PDF, PNG e mais.

## Pré-requisitos
- **Java Development Kit (JDK) 8+** instalado.  
- Conhecimento básico de Java e familiaridade com conceitos do Excel.

### Bibliotecas Necessárias
Adicione Aspose.Cells ao seu projeto usando um dos trechos abaixo.

#### Maven
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

#### Gradle
```gradle
implementation group: 'com.aspose', name: 'aspose-cells', version: '25.3'
```

### Aquisição de Licença
Aspose oferece uma avaliação gratuita e uma licença temporária para testes extensivos.

- **Free Trial**: [Download Gratuito](https://releases.aspose.com/cells/java/)  
- **Temporary License**: [Solicitar Aqui](https://purchase.aspose.com/temporary-license/)

## Configurando Aspose.Cells para Java

Primeiro, crie uma instância `Workbook` – este será a tela para nossos dados e gráfico.

```java
import com.aspose.cells.Workbook;

// Initialize a new Workbook
Workbook workbook = new Workbook();
```

## Guia Passo a Passo

### 1. Criar e Nomear uma Planilha
Armazenaremos os dados brutos em uma planilha chamada **Data**.

```java
import com.aspose.cells.Worksheet;

// Create a new Workbook instance
Workbook workbook = new Workbook();
```

```java
// Access the first worksheet and set its name to "Data"
Worksheet sheet = workbook.getWorksheets().get(0);
sheet.setName("Data");
```

### 2. Preencher Células do Excel
Insira nomes de regiões e valores de vendas que o gráfico de colunas visualizará.

```java
import com.aspose.cells.Cells;

// Get the cells collection from the "Data" sheet
Cells cells = sheet.getCells();
```

```java
// Insert region names and sales figures
cells.get("A1").putValue("Region");
cells.get("B1").putValue("Sale");

String[] regions = {"France", "Germany", "England", "Sweden", "Italy", "Spain", "Portugal"};
int[] sales = {70000, 55000, 30000, 40000, 35000, 32000, 10000};

for (int i = 0; i < regions.length; i++) {
    cells.get("A" + (i+2)).putValue(regions[i]);
    cells.get("B" + (i+2)).putValue(sales[i]);
}
```

### 3. Adicionar Planilha de Gráfico
Separar o gráfico dos dados brutos mantém a planilha organizada.

```java
import com.aspose.cells.SheetType;

// Add a new chart sheet
int sheetIndex = workbook.getWorksheets().add(SheetType.CHART);
Worksheet chartSheet = workbook.getWorksheets().get(sheetIndex);

// Name the worksheet "Chart"
chartSheet.setName("Chart");
```

### 4. Criar um Gráfico de Colunas
Agora realmente **geramos objetos generate column chart**.

```java
import com.aspose.cells.Chart;
import com.aspose.cells.ChartType;

// Add a new column chart to the "Chart" sheet
int chartIndex = chartSheet.getCharts().add(ChartType.COLUMN, 1, 1, 25, 10);
Chart chart = chartSheet.getCharts().get(chartIndex);
```

### 5. Definir Imagem como Preenchimento de Fundo na Área de Plotagem
Uma imagem de fundo pode fazer o gráfico se destacar.

```java
import java.io.FileInputStream;
import com.aspose.cells.Color;

String dataDir = "YOUR_DATA_DIRECTORY";
File file = new FileInputStream(dataDir + "aspose-logo.png");
byte[] data = new byte[(int)file.length()];
file.read(data);

chart.getPlotArea().getArea().getFillFormat().setImageData(data);
chart.getPlotArea().getBorder().setVisible(false);
```

### 6. Definir Título do Gráfico
Personalizar o **set chart title** melhora a legibilidade.

```java
// Configure the chart's title properties
chart.getTitle().setText("Sales By Region");
chart.getTitle().getFont().setColor(Color.getBlue());
chart.getTitle().getFont().setBold(true);
chart.getTitle().getFont().setSize(12);
```

### 7. Configurar Dados da Série e Legenda
Vincule o intervalo de dados ao gráfico e posicione a legenda.

```java
// Set series and category data for the chart
chart.getNSeries().add("Data!B2:B8", true);
chart.getNSeries().setCategoryData("Data!A2:A8");
chart.getNSeries().setColorVaried(true);

// Position the legend at the top of the chart
import com.aspose.cells.Legend;
import com.aspose.cells.LegendPositionType;

Legend legend = chart.getLegend();
legend.setPosition(LegendPositionType.TOP);
```

### 8. Exportar Workbook Excel
Finalmente, **exportar workbook excel** para um arquivo XLS (ou qualquer formato suportado).

```java
String outDir = "YOUR_OUTPUT_DIRECTORY";
workbook.save(outDir + "SPAsBFillInChart_out.xls");
```

## Aplicações Práticas
- **Business Reports** – Auto‑gerar gráficos de vendas para PDFs mensais.  
- **Data Analysis Tools** – Incorporar gráficos dinâmicos em painéis de análise personalizados.  
- **Enterprise Dashboards** – Atualizar imagens de gráficos em tempo real para monitoramento.

## Considerações de Desempenho
- Atualizações em lote de células ao trabalhar com grandes conjuntos de dados para reduzir a sobrecarga.  
- Libere recursos (`workbook.dispose()`) se você processar muitas planilhas em um loop.  

## Problemas Comuns e Soluções
- **Image not showing** – Verifique o caminho do arquivo e se o formato da imagem (PNG, JPEG) é suportado.  
- **Chart appears blank** – Certifique‑se de que as referências de intervalo de dados (`Data!B2:B8`) correspondam às células preenchidas.  
- **Out‑of‑memory errors** – Processar os dados em blocos e chamar `System.gc()` após grandes gravações.

## Perguntas Frequentes

**Q: Como adiciono várias séries a um gráfico de colunas?**  
A: Chame `chart.getNSeries().add()` repetidamente com diferentes intervalos de dados, por exemplo, `"Data!C2:C8"` para uma segunda série.

**Q: Posso alterar os rótulos dos eixos?**  
A: Sim. Use `chart.getCategoryAxis().setTitle("Regions")` e `chart.getValueAxis().setTitle("Sales")`.

**Q: Para quais formatos posso exportar além de XLS?**  
A: Use `workbook.save("chart.pdf")`, `workbook.save("chart.png")`, ou `workbook.save("chart.xlsx")` para PDF, PNG e XLSX respectivamente.

**Q: É necessária uma licença para builds de desenvolvimento?**  
A: Uma avaliação gratuita funciona para avaliação, mas uma licença permanente ou temporária é necessária para implantações em produção.

**Q: Como posso melhorar a velocidade de renderização para milhares de linhas?**  
A: Preencha as células usando `cells.importArray()` e minimize as repinturas do gráfico criando-o após todos os dados serem carregados.

---

**Última Atualização:** 2026-04-08  
**Testado com:** Aspose.Cells 25.3 for Java  
**Autor:** Aspose  

## Recursos

- [Documentação do Aspose.Cells](https://reference.aspose.com/cells/java/)  
- [Baixar Aspose.Cells](https://releases.aspose.com/cells/java/)  
- [Comprar Licença](https://purchase.aspose.com/buy)  
- [Avaliação Gratuita](https://releases.aspose.com/cells/java/)  
- [Solicitar Licença Temporária](https://purchase.aspose.com/temporary-license/)  
- [Fórum de Suporte](https://forum.aspose.com/c/cells/9)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}