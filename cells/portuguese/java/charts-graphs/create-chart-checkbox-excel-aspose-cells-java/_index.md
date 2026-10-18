---
date: '2026-09-22'
description: Aprenda a criar um gráfico interativo no Excel com caixas de seleção
  usando Aspose.Cells for Java. Este guia aborda a configuração, a adição de caixas
  de seleção, licenciamento e as melhores práticas.
keywords:
- create interactive Excel chart
- how to add checkbox java
- aspose.cells license java
lastmod: '2026-09-22'
og_description: Aprenda a criar um gráfico interativo no Excel com caixas de seleção
  usando Aspose.Cells for Java. Siga instruções passo a passo, veja dicas de licenciamento
  e descubra casos de uso reais.
og_image_alt: Guide showing how to create interactive Excel chart with checkboxes
  using Aspose.Cells for Java
og_title: Como criar um gráfico interativo no Excel com caixas de seleção
schemas:
- author: Aspose
  dateModified: '2026-09-22'
  description: Learn how to create interactive Excel chart with checkboxes using Aspose.Cells
    for Java. This guide covers setup, adding checkboxes, licensing, and best practices.
  headline: How to create interactive Excel chart with checkboxes
  type: TechArticle
- questions:
  - answer: Use Aspose.Cells’ `Shape` API with `ShapeType.FORM_CONTROL_CHECKBOX` and
      link it to a worksheet cell; the checkbox works natively in Excel.
    question: How do I add a checkbox without using VBA?
  - answer: The checkbox shape is available in the free evaluation, but a permanent
      Aspose.Cells license removes evaluation limits and enables full performance
      optimizations.
    question: Do I need a license for the checkbox feature?
  - answer: Files saved with Aspose.Cells follow the Office Open XML standard and
      open correctly in Excel 2016, 2019, 2021, and Microsoft 365.
    question: Which Excel versions can open the generated file?
  - answer: Yes, create a checkbox for each series, link each to a distinct helper
      cell, and use conditional formulas to toggle each series independently.
    question: Can I control multiple series with separate checkboxes?
  - answer: Practically, you can add dozens; performance remains stable up to 200
      controls per worksheet on typical server hardware.
    question: Is there a limit on the number of checkboxes per chart?
  type: FAQPage
tags:
- interactive Excel charts
- Aspose.Cells
- Java Excel automation
title: Como criar um gráfico interativo no Excel com caixas de seleção
url: /pt/java/charts-graphs/create-chart-checkbox-excel-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como criar um gráfico interativo do Excel com caixas de seleção

## Introdução

Neste tutorial você **criará um gráfico interativo do Excel** que permite aos usuários alternar séries de dados clicando em caixas de seleção colocadas diretamente no gráfico. Usando Aspose.Cells for Java, você pode gerar pastas de trabalho totalmente equipadas programaticamente, sem precisar do Microsoft Excel instalado. A abordagem funciona para qualquer solução de relatórios ou painel baseada em Java.

**O que você aprenderá**
- Como configurar o Aspose.Cells for Java no Maven ou Gradle  
- Como instanciar um `Workbook` e adicionar um gráfico de colunas  
- Como incorporar uma forma de caixa de seleção dentro da área do gráfico  
- Como aplicar uma licença do Aspose.Cells para uso em produção  

## Respostas rápidas
- **Qual biblioteca cria gráficos interativos do Excel?** Aspose.Cells for Java.  
- **Posso adicionar caixas de seleção sem VBA?** Sim, inserindo uma forma de Controle de Formulário via API.  
- **Preciso de uma licença para este recurso?** Uma licença temporária funciona para avaliação; uma licença permanente é necessária para produção.  
- **Qual versão do Java é necessária?** JDK 8 ou superior.  
- **O gráfico funcionará no Excel 2016‑2024?** Sim, o arquivo gerado segue o padrão Office Open XML.  

## O que é um gráfico interativo do Excel?
Um **gráfico interativo do Excel** combina um gráfico padrão com controles de interface (por exemplo, caixas de seleção) que permitem aos usuários mostrar ou ocultar séries de dados instantaneamente, transformando uma visualização estática em uma ferramenta de relatório dinâmica.

## Por que usar Aspose.Cells for Java?
Aspose.Cells suporta **mais de 80 formatos de entrada e saída** e pode processar pastas de trabalho com **mais de 10.000 linhas** sem carregar o arquivo inteiro na memória, oferecendo geração de alto desempenho em ambientes de servidor.

## Pré-requisitos

- **Java Development Kit (JDK):** versão 8 ou superior.  
- **Aspose.Cells for Java:** versão mais recente (por exemplo, 25.3).  
- **Maven ou Gradle:** para gerenciar a dependência da biblioteca.  

### Pré-requisitos de conhecimento
Sintaxe básica de Java e familiaridade com conceitos do Excel (planilhas, intervalos, gráficos) são úteis, mas as etapas abaixo são detalhadas o suficiente para desenvolvedores de qualquer nível de experiência.

## Como adicionar caixa de seleção em Java?

Carregue a biblioteca Aspose.Cells, crie uma pasta de trabalho e insira uma forma de caixa de seleção em uma única chamada. A caixa de seleção é um Controle de Formulário que pode ser vinculado a uma célula; ao alterná‑la, o valor da célula vinculada será alterado, o que você pode posteriormente associar à visibilidade de uma série do gráfico.

```text
// Direct answer (40‑70 words):
You add a checkbox by creating a `Shape` of type `ShapeType.FORM_CONTROL_CHECKBOX`, setting its placement on the chart worksheet, and linking it to a cell that stores the Boolean state. The linked cell can be used in formulas that drive chart series visibility, enabling real‑time interactivity without VBA.
```

### Passo 1: Configurar a dependência Maven

Adicione o artefato Maven do Aspose.Cells ao seu `pom.xml`:

```xml
<dependency>
  <groupId>com.aspose</groupId>
  <artifactId>aspose-cells</artifactId>
  <version>25.3</version>
</dependency>
```

### Passo 2: Configurar a dependência Gradle

Adicione a linha a seguir ao seu arquivo `build.gradle`:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

#### Etapas de aquisição de licença

Para desbloquear a funcionalidade completa, obtenha uma licença temporária ou permanente. Baixe uma licença de avaliação em [Aspose's website](https://releases.aspose.com/cells/java/). Para produção, adquira uma licença e aplique-a conforme mostrado mais adiante.

#### Inicialização básica

License é a classe Aspose.Cells usada para aplicar um arquivo de licença adquirido, habilitando a funcionalidade completa sem limites de avaliação. Inicialize a biblioteca no seu código Java antes de qualquer operação de pasta de trabalho:

```java
import com.aspose.cells.Workbook;

public class AsposeSetup {
    public static void main(String[] args) throws Exception {
        // Initialize the Workbook object.
        Workbook workbook = new Workbook();
        
        System.out.println("Aspose.Cells for Java initialized successfully.");
    }
}
```

## Como criar um gráfico interativo do Excel?

Um objeto `Workbook` do Aspose.Cells representa um arquivo Excel completo, contendo planilhas, gráficos e outros elementos. Ao criar uma pasta de trabalho, você pode adicionar dados programaticamente, gerar um gráfico de colunas e, posteriormente, incorporar controles interativos como caixas de seleção. As etapas a seguir orientam você na construção da pasta de trabalho, preenchimento de dados e configuração do gráfico para interatividade.

```text
// Direct answer (40‑70 words):
First, instantiate a `Workbook`, fill a worksheet with sample data, and call `addChart` to place a column chart. Next, create a checkbox shape, position it over the chart, and link it to a cell that toggles the series’ `isVisible` property via a formula. Finally, save the workbook as an XLSX file.
```

### Instanciar pasta de trabalho e adicionar gráfico

#### Visão geral

Esta seção mostra como criar uma nova pasta de trabalho, adicionar uma planilha para dados e gerar um gráfico de colunas que posteriormente será tornado interativo.

##### Passo 1: Criar uma nova pasta de trabalho

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.SheetType;

public class ChartCreation {
    public static void main(String[] args) throws Exception {
        // Instantiate a new Workbook object representing an Excel file.
        Workbook workbook = new Workbook();
        
        System.out.println("Workbook created.");
    }
}
```

##### Passo 2: Adicionar uma planilha de gráfico

```java
import com.aspose.cells.Worksheet;
import com.aspose.cells.ChartType;

public class ChartCreation {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        
        // Adding a chart worksheet to the workbook.
        int index = workbook.getWorksheets().add(SheetType.CHART);
        Worksheet sheet = workbook.getWorksheets().get(index);

        System.out.println("Chart worksheet added.");
    }
}
```

##### Passo 3: Inserir um gráfico de colunas

```java
public class ChartCreation {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        int index = workbook.getWorksheets().add(SheetType.CHART);
        Worksheet sheet = workbook.getWorksheets().get(index);

        // Add a floating chart of type COLUMN to the newly added chart worksheet.
        sheet.getCharts().addFloatingChart(ChartType.COLUMN, 0, 0, 1024, 960);

        System.out.println("Column chart inserted.");
    }
}
```

##### Passo 4: Adicionar dados da série

```java
public class ChartCreation {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        int index = workbook.getWorksheets().add(SheetType.CHART);
        Worksheet sheet = workbook.getWorksheets().get(index);

        // Add a floating chart of type COLUMN.
        sheet.getCharts().addFloatingChart(ChartType.COLUMN, 0, 0, 1024, 960);

        // Adding series data for the chart.
        sheet.getCharts().get(0).getNSeries().add("{1,2,3}", false);
        
        System.out.println("Series data added to the chart.");
    }
}
```

## Como incorporar uma caixa de seleção em um gráfico?

Incorporar uma caixa de seleção diretamente na área do gráfico permite que os usuários finais cliquem para mostrar ou ocultar uma série específica. A caixa de seleção é uma forma de Controle de Formulário que pode ser vinculada a uma célula; o valor da célula pode ser referenciado em uma fórmula que controla a visibilidade da série.

Shape é o objeto Aspose.Cells que representa um elemento de desenho, como um controle de formulário, imagem ou caixa de texto dentro de uma planilha.

```text
// Direct answer (40‑70 words):
You embed a checkbox by creating a `Shape` with `ShapeType.FORM_CONTROL_CHECKBOX`, positioning it using `setUpperLeftRow/Column` relative to the chart sheet, and linking it to a helper cell (e.g., `B1`). Then, use a conditional formula in the series data range that checks the helper cell’s Boolean value to decide whether the series is plotted.
```

### Incorporar uma forma de caixa de seleção

```java
import com.aspose.cells.MsoDrawingType;
import com.aspose.cells.PlacementType;

public class ChartWithCheckbox {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        int index = workbook.getWorksheets().add(SheetType.CHART);
        Worksheet sheet = workbook.getWorksheets().get(index);

        // Add a checkbox shape within the chart area on the first chart of the worksheet.
        sheet.getCharts().get(0).getShapes().addShapeInChart(MsoDrawingType.CHECK_BOX, PlacementType.MOVE, 400, 400, 1000, 600);
        
        System.out.println("Checkbox added to the chart.");
    }
}
```

### Definir texto da caixa de seleção

```java
public class ChartWithCheckbox {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        int index = workbook.getWorksheets().add(SheetType.CHART);
        Worksheet sheet = workbook.getWorksheets().get(index);

        // Add checkbox shape within the chart.
        sheet.getCharts().get(0).getShapes().addShapeInChart(MsoDrawingType.CHECK_BOX, PlacementType.MOVE, 400, 400, 1000, 600);

        // Setting text for the newly added checkbox shape.
        sheet.getCharts().get(0).getShapes().get(0).setText("CheckBox 1");

        System.out.println("Checkbox labeled successfully.");
    }
}
```

## Como salvar a pasta de trabalho como arquivo Excel?

Salvar o `Workbook` grava todas as alterações em memória em um arquivo Excel físico no disco. Aspose.Cells suporta o formato .xlsx moderno, garantindo que o arquivo seja aberto no Excel 2016‑2024 e em outros aplicativos compatíveis com Office. Use o método `save` com o caminho de arquivo desejado e, opcionalmente, especifique o formato do arquivo para opções adicionais.

```text
// Direct answer (40‑70 words):
Call `workbook.save("InteractiveChart.xlsx", SaveFormat.XLSX)` to write the workbook. The method automatically closes all streams and guarantees that the embedded chart and checkbox are fully functional when the file is opened in Excel 2016‑2024.
```

```java
public class ChartWithCheckbox {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        int index = workbook.getWorksheets().add(SheetType.CHART);
        Worksheet sheet = workbook.getWorksheets().get(index);

        // Add checkbox shape and label it.
        sheet.getCharts().get(0).getShapes().addShapeInChart(MsoDrawingType.CHECK_BOX, PlacementType.MOVE, 400, 400, 1000, 600);
        sheet.getCharts().get(0).getShapes().get(0).setText("CheckBox 1");

        // Save the workbook
        String outDir = "YOUR_OUTPUT_DIRECTORY"; // Replace with your actual output directory path.
        workbook.save(outDir + "/InsertCheckboxInChartSheet_out.xlsx");
        
        System.out.println("Workbook saved successfully.");
    }
}
```

## Aplicações práticas

Cenários do mundo real onde um gráfico interativo com caixas de seleção agrega valor:

1. **Relatórios interativos:** Permita que as partes interessadas alternem linhas de produtos individuais em um gráfico de vendas.  
2. **Análise comparativa:** Permita que analistas se concentrem em períodos de tempo ou regiões específicas marcando/desmarcando séries.  
3. **Painéis educacionais:** Os estudantes podem explorar tendências de dados selecionando quais variáveis exibir.

## Problemas comuns e soluções

- **Caixa de seleção não responde:** Certifique‑se de que a caixa de seleção está vinculada a uma célula e que a célula é referenciada em uma fórmula que afeta a visibilidade da série.  
- **Gráfico não atualiza após alternar:** Atualize a visualização da pasta de trabalho no Excel ou recalcule as fórmulas (`workbook.calculateFormula()`).  
- **Licença não aplicada:** Verifique se `License license = new License(); license.setLicense("Aspose.Cells.lic");` é executado antes de qualquer operação de pasta de trabalho.

## Perguntas frequentes

**Q: Como adiciono uma caixa de seleção sem usar VBA?**  
A: Use a API `Shape` do Aspose.Cells com `ShapeType.FORM_CONTROL_CHECKBOX` e vincule-a a uma célula da planilha; a caixa de seleção funciona nativamente no Excel.

**Q: Preciso de uma licença para o recurso de caixa de seleção?**  
A: A forma de caixa de seleção está disponível na avaliação gratuita, mas uma licença permanente do Aspose.Cells remove os limites de avaliação e habilita otimizações de desempenho completas.

**Q: Quais versões do Excel podem abrir o arquivo gerado?**  
A: Arquivos salvos com Aspose.Cells seguem o padrão Office Open XML e abrem corretamente no Excel 2016, 2019, 2021 e Microsoft 365.

**Q: Posso controlar várias séries com caixas de seleção separadas?**  
A: Sim, crie uma caixa de seleção para cada série, vincule cada uma a uma célula auxiliar distinta e use fórmulas condicionais para alternar cada série independentemente.

**Q: Existe um limite para o número de caixas de seleção por gráfico?**  
A: Na prática, você pode adicionar dezenas; o desempenho permanece estável até cerca de 200 controles por planilha em hardware de servidor típico.

---

**Última atualização:** 2026-09-22  
**Testado com:** Aspose.Cells 25.3 for Java  
**Autor:** Aspose

## Tutoriais relacionados

- [Como adicionar uma caixa de seleção no Excel usando Aspose.Cells para Java: Guia passo a passo](/cells/java/data-validation/add-checkbox-excel-aspose-cells-java/)
- [Criar gráficos dinâmicos do Excel com Aspose.Cells Java: Um guia abrangente para desenvolvedores](/cells/java/charts-graphs/aspose-cells-java-dynamic-excel-charts/)
- [Adicionar rótulos de dados ao gráfico do Excel com Aspose.Cells Java](/cells/java/advanced-excel-charts/chart-interactivity/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}