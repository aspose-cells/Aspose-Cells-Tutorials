---
date: '2026-04-11'
description: Aprenda automação de Excel com Java usando Aspose.Cells. Este tutorial
  mostra como criar uma planilha Excel em Java, preencher dados do Excel em Java e
  salvar o arquivo Excel em Java com gráficos.
keywords:
- excel automation java
- create excel workbook java
- save excel file java
- populate excel data java
- aspose cells java
title: 'Automação de Excel Java: Crie Pastas de Trabalho e Gráficos usando Aspose'
url: /pt/java/charts-graphs/aspose-cells-java-excel-workbook-charts/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Automação de Excel Java: Crie Pastas de Trabalho e Gráficos usando Aspose

## Introdução

Automatizar tarefas do Excel com Java pode economizar horas de trabalho manual, especialmente quando você precisa gerar relatórios, dashboards ou gráficos baseados em dados em tempo real. **Excel automation java** com Aspose.Cells oferece uma API limpa e de alto desempenho que lida com tudo, desde a criação de pastas de trabalho até a estilização avançada de gráficos. Neste tutorial você aprenderá como configurar o Aspose.Cells, **create an Excel workbook java**, preenchê‑lo com dados, adicionar um gráfico, aplicar formatação 3‑D e, finalmente, **save the Excel file java**.

### Respostas Rápidas
- **Qual biblioteca simplifica a automação de Excel em Java?** Aspose.Cells for Java.  
- **Posso adicionar gráficos 3‑D programaticamente?** Sim – a API suporta formatação 3‑D e efeitos de iluminação.  
- **Preciso de uma licença para desenvolvimento?** Uma licença de teste gratuita está disponível; uma licença comercial é necessária para produção.  
- **Quais ferramentas de build Java são suportadas?** Maven e Gradle são totalmente suportados.  
- **Quais formatos de arquivo posso exportar?** XLS, XLSX, CSV, PDF e muitos outros.

## O que é Excel automation java?

Excel automation java refere‑se ao processo de gerar, modificar e salvar pastas de trabalho do Excel programaticamente usando código Java. Ele elimina a edição manual de planilhas, garante consistência e permite integração com outros sistemas, como bancos de dados ou serviços web.

## Por que usar Aspose.Cells para Java?

- **Rich feature set** – from simple cell values to complex charts, pivot tables, and conditional formatting.  
- **No Microsoft Office dependency** – works on any server‑side environment.  
- **High performance** – optimized for large data sets and multi‑threaded scenarios.  
- **Broad format support** – read/write XLS, XLSX, ODS, CSV, PDF, HTML, and more.

## Pré-requisitos

- **Java Development Kit (JDK) 8+**  
- **Maven ou Gradle** para gerenciamento de dependências  
- **Aspose.Cells for Java 25.3 ou posterior** (trial ou licenciado)  

## Configurando Aspose.Cells para Java

Adicione a biblioteca ao seu projeto usando uma das configurações a seguir.

### Maven
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Gradle
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

#### Aquisição de Licença

Solicite uma licença de teste gratuita no site da Aspose, ou compre uma licença completa para uso em produção. Coloque o arquivo de licença no seu projeto e carregue‑o em tempo de execução.

## Inicialização e Configuração Básicas

Uma vez que a dependência esteja resolvida, você pode começar a codificar.

```java
import com.aspose.cells.Workbook;

public class ExcelDemo {
    public static void main(String[] args) throws Exception {
        String dataDir = "YOUR_DATA_DIRECTORY";
        String outDir = "YOUR_OUTPUT_DIRECTORY";

        // Initialize a new Workbook object
        Workbook book = new Workbook();
        System.out.println("Workbook initialized successfully.");
    }
}
```

## Guia Passo a Passo

### Etapa 1: Como criar excel workbook java

Crie uma nova instância de pasta de trabalho que conterá todas as suas planilhas.

```java
import com.aspose.cells.Workbook;
// Initialize a new Workbook object
Workbook book = new Workbook();
```

### Etapa 2: Adicionar planilhas (incluindo uma planilha de gráfico)

```java
import com.aspose.cells.Worksheet;
Worksheet dataSheet = book.getWorksheets().add("DataSheet");
Worksheet chartSheet = book.getWorksheets().add("MyChart");
System.out.println("Worksheets added successfully.");
```

### Etapa 3: Como popular excel data java

Insira dados de exemplo que o gráfico referenciará.

```java
import com.aspose.cells.Cells;
Cells cells = dataSheet.getCells();
cells.get("B1").putValue(1);
cells.get("B2").putValue(2);
cells.get("B3").putValue(3);
cells.get("A1").putValue("A");
cells.get("A2").putValue("B");
cells.get("A3").putValue("C");
System.out.println("Data populated successfully.");
```

### Etapa 4: Adicionar um gráfico de colunas à pasta de trabalho

```java
import com.aspose.cells.Chart;
import com.aspose.cells.ChartCollection;
import com.aspose.cells.ChartType;
ChartCollection charts = chartSheet.getCharts();
charts.add(ChartType.COLUMN, 5, 0, 25, 15);
Chart chart = book.getWorksheets().get(2).getCharts().get(0);
System.out.println("Chart added successfully.");
```

### Etapa 5: Aplicar formatação de cores à área do gráfico

```java
import com.aspose.cells.Color;
chart.getPlotArea().getArea().setBackgroundColor(Color.getWhite());
chart.getChartArea().getArea().setBackgroundColor(Color.getWhite());
chart.getPlotArea().getArea().setForegroundColor(Color.getWhite());
chart.getChartArea().getArea().setForegroundColor(Color.getWhite());
System.out.println("Color formatting applied successfully.");
```

### Etapa 6: Configurar legenda e séries de dados

```java
import com.aspose.cells.Series;
chart.setShowLegend(false);
chart.getNSeries().add("DataSheet!B1:B3", true);
chart.getNSeries().setCategoryData("DataSheet!A1:A3");
Series ser = chart.getNSeries().get(0);
System.out.println("Chart series configured successfully.");
```

### Etapa 7: Aplicar formatação 3D às séries

```java
import com.aspose.cells.Bevel;
import com.aspose.cells.BevelPresetType;
import com.aspose.cells.Format3D;
import com.aspose.cells.LightRigType;
import com.aspose.cells.PresetMaterialType;
import com.aspose.cells.ShapePropertyCollection;
ShapePropertyCollection spPr = ser.getShapeProperties();
Format3D fmt3d = spPr.getFormat3D();

Bevel bevel = fmt3d.getTopBevel();
bevel.setType(BevelPresetType.CIRCLE);
bevel.setHeight(5);
bevel.setWidth(9);
fmt3d.setSurfaceMaterialType(PresetMaterialType.WARM_MATTE);
fmt3d.setSurfaceLightingType(LightRigType.THREE_POINT);
fmt3d.setLightingAngle(20);
System.out.println("3D formatting applied successfully.");
```

### Etapa 8: Definir cores das séries para melhor distinção visual

```java
ser.getArea().setBackgroundColor(Color.getMaroon());
ser.getArea().setForegroundColor(Color.getMaroon());
ser.getBorder().setColor(Color.getMaroon());
System.out.println("Series color formatting applied successfully.");
```

### Etapa 9: Como salvar excel file java

```java
book.save(outDir + "A3DFormat_out.xls");
System.out.println("Workbook saved successfully.");
```

## Aplicações Práticas

- **Financial Reporting** – Generate quarterly statements with dynamic charts. → **Relatórios Financeiros** – Gere demonstrações trimestrais com gráficos dinâmicos.  
- **Data‑Analysis Dashboards** – Build interactive dashboards that refresh automatically. → **Painéis de Análise de Dados** – Crie painéis interativos que são atualizados automaticamente.  
- **Inventory Management** – Export stock levels and trends to Excel for stakeholder review. → **Gestão de Inventário** – Exporte níveis de estoque e tendências para Excel para revisão das partes interessadas.  
- **Project Planning** – Create Gantt‑style charts directly from Java‑based scheduling systems. → **Planejamento de Projetos** – Crie gráficos estilo Gantt diretamente de sistemas de agendamento baseados em Java.

## Dicas de Desempenho para Excel Automation Java

- **Reuse Workbook Objects** when processing multiple sheets to reduce memory churn. → **Reutilizar objetos Workbook** ao processar múltiplas planilhas para reduzir o consumo de memória.  
- **Batch Cell Updates** using `Cells.importArray` for large data sets instead of individual `putValue` calls. → **Atualizações em lote de células** usando `Cells.importArray` para grandes conjuntos de dados em vez de chamadas individuais a `putValue`.  
- **Dispose Resources** by calling `book.dispose()` after saving large files. → **Liberar recursos** chamando `book.dispose()` após salvar arquivos grandes.

## Perguntas Frequentes

**Q: Posso gerar XLSX em vez de XLS?**  
A: Sim – basta mudar a extensão do arquivo em `book.save("output.xlsx")`; Aspose seleciona automaticamente o formato correto.

**Q: É necessária uma licença para desenvolvimento?**  
A: Uma licença de teste gratuita funciona para desenvolvimento e testes. Implantações em produção requerem uma licença adquirida.

**Q: Como adiciono mais tipos de gráfico?**  
A: Use o enum `ChartType` (por exemplo, `ChartType.PIE`, `ChartType.LINE`) ao chamar `charts.add(...)`.

**Q: E se eu precisar proteger a pasta de trabalho?**  
A: Chame `book.getSettings().setPassword("yourPassword")` antes de salvar.

**Q: O Aspose.Cells suporta arquivos com macros?**  
A: Sim – você pode criar ou preservar macros VBA em pastas de trabalho XLSM.

---

**Última atualização:** 2026-04-11  
**Testado com:** Aspose.Cells 25.3 (Java)  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}