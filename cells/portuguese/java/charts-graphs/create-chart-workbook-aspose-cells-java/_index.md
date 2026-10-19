---
date: '2026-09-27'
description: Aprenda a criar um arquivo xlsx em Java usando Aspose.Cells, adicionar
  dados ao gráfico e automatizar a criação de gráficos do Excel com configuração Maven
  em apenas alguns passos.
keywords:
- create xlsx file java
- add data to chart
- how to add chart
- create excel workbook java
- automate excel chart creation
lastmod: '2026-09-27'
og_description: Aprenda a criar um arquivo xlsx em Java usando Aspose.Cells, adicionar
  dados ao gráfico e automatizar a criação de gráficos do Excel com configuração Maven
  em apenas alguns passos.
og_image_alt: Guide showing how to create XLSX file in Java and generate charts with
  Aspose.Cells
og_title: Como criar um arquivo xlsx em Java com gráficos Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to create xlsx file java using Aspose.Cells, add data to
    chart, and automate Excel chart creation with Maven setup in just a few steps.
  headline: How to create xlsx file java with Aspose.Cells charts
  type: TechArticle
- questions:
  - answer: Use `worksheet.getCharts().add(ChartType.COLUMN, upperLeftRow, upperLeftColumn,
      lowerRightRow, lowerRightColumn)` for each chart you need, then set each chart’s
      data source individually.
    question: How do I add more than one chart to the same worksheet?
  - answer: Yes—instantiate `Workbook` with the file path (`new Workbook("existing.xlsx")`)
      and then add or edit worksheets and charts as shown above.
    question: Can I modify an existing Excel file instead of creating a new one?
  - answer: Aspose.Cells supports XLS, CSV, PDF, HTML, ODS, and more than 30 additional
      formats, allowing seamless conversion after chart creation.
    question: Which file formats can I export to besides XLSX?
  - answer: Load data in chunks, write each chunk to the worksheet, and call `worksheet.calculateFormula()`
      only after all data is written to minimise CPU overhead.
    question: What is the recommended way to handle very large datasets?
  - answer: Browse the full reference at the [official documentation](https://docs.aspose.com/cells/java/).
    question: Where can I find deeper documentation and code samples?
  type: FAQPage
tags:
- create xlsx
- Aspose.Cells
- Java Excel automation
- chart generation
title: Como criar um arquivo xlsx em Java com gráficos Aspose.Cells
url: /pt/java/charts-graphs/create-chart-workbook-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como criar arquivo xlsx Java com gráficos Aspose.Cells

## Introdução
Criar um workbook **xlsx** programaticamente pode parecer assustador, especialmente quando você precisa automatizar a geração de gráficos. Neste guia você aprenderá como **criar arquivo xlsx Java** usando Aspose.Cells, adicionar dados a um gráfico e salvar o resultado — tudo com código Java claro, passo a passo. Ao final, você poderá incorporar gráficos de colunas dinâmicos em qualquer arquivo Excel sem abrir o próprio Excel.

## Respostas rápidas
- **Qual é a primeira linha de código?** `Workbook workbook = new Workbook();` cria um novo workbook XLSX.  
- **Qual artefato Maven eu preciso?** `com.aspose:aspose-cells` (versão mais recente).  
- **Posso adicionar vários gráficos?** Sim – chame `worksheet.getCharts().add(...)` para cada tipo de gráfico.  
- **Preciso de licença para testes?** Uma licença temporária funciona para avaliação; uma licença comprada remove os limites de avaliação.  
- **Qual versão do Java é necessária?** Java 8 ou superior é totalmente suportado.

## O que é Aspose.Cells para Java?
Aspose.Cells para Java é uma API poderosa que permite criar, editar e converter arquivos Excel sem o Microsoft Office. Ela suporta **50+** formatos de entrada e saída e pode processar workbooks com centenas de planilhas usando menos de 200 MB de memória.

## Como criar arquivo xlsx Java?
`Workbook` representa um workbook Excel na memória. Carregue a biblioteca Aspose.Cells, instancie um `Workbook`, adicione dados, crie um gráfico e, em seguida, salve o arquivo. Todo esse fluxo de trabalho pode ser escrito em menos de dez linhas de Java, proporcionando uma solução rápida e repetível para relatórios automatizados.

## Pré-requisitos
- **Aspose.Cells para Java** – adicione a dependência Maven ou Gradle (veja abaixo).  
- **JDK 8+** – a biblioteca funciona em qualquer runtime Java 8 ou mais recente.  
- **Conhecimento básico de Java** – você deve estar confortável com classes e chamadas de método.

## Configurando Aspose.Cells para Java
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

## Aquisição de Licença
Antes de começar, decida se você precisa de um **teste gratuito** ou de uma **licença comprada**. Uma licença de teste remove a maioria das restrições de recursos, enquanto uma licença completa elimina a marca d'água de avaliação. Obtenha uma licença na [Página de Compra da Aspose](https://purchase.aspose.com/buy) ou solicite uma [Licença Temporária](https://purchase.aspose.com/temporary-license/).

## Inicialização básica
A classe `License` carrega seu arquivo de licença para que todas as chamadas subsequentes da API sejam executadas sem limites de avaliação.  
```java
import com.aspose.cells.Workbook;

public class Main {
    public static void main(String[] args) {
        // Initialize a new Workbook object
        Workbook workbook = new Workbook();
        
        System.out.println("Workbook initialized successfully.");
    }
}
```

## Guia de implementação
A seguir, percorremos cada passo necessário para **criar arquivo xlsx Java** e incorporar um gráfico de colunas.

### 1. Criar novo workbook
`Workbook` é o objeto de nível superior que representa um arquivo Excel na memória.  
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.FileFormatType;

public class WorkbookCreation {
    public static void main(String[] args) {
        String dataDir = "YOUR_DATA_DIRECTORY";
        
        // Create a new workbook in XLSX format
        Workbook workbook = new Workbook(FileFormatType.XLSX);
        System.out.println("New Excel workbook created.");
    }
}
```

### 2. Acessar a primeira planilha
`Worksheet` fornece acesso a células, linhas, colunas e gráficos em uma planilha específica.  
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

public class AccessWorksheet {
    public static void main(String[] args) {
        Workbook workbook = new Workbook();
        
        // Get the first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
        System.out.println("First worksheet accessed.");
    }
}
```

### 3. Adicionar dados para o gráfico
Preencha as células com os valores que você deseja visualizar. Esses dados serão o intervalo de origem para o gráfico.  
```java
import com.aspose.cells.Cells;
import com.aspose.cells.Worksheet;

public class AddData {
    public static void main(String[] args) {
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);
        Cells cells = worksheet.getCells();

        // Populate data for chart
        cells.get("A2").putValue("C1");
cells.get("A3").putValue("C2");
cells.get("A4").putValue("C3");

        cells.get("B1").putValue("T1");
cells.get("B2").putValue(6);
cells.get("B3").putValue(3);
cells.get("B4").putValue(2);

        cells.get("C1").putValue("T2");
cells.get("C2").putValue(7);
cells.get("C3").putValue(2);
cells.get("C4").putValue(5);

        cells.get("D1").putValue("T3");
cells.get("D2").putValue(8);
cells.get("D3").putValue(4);
cells.get("D4").putValue(2);

        System.out.println("Data added for chart creation.");
    }
}
```

### 4. Criar gráfico de colunas
Objetos `Chart` são adicionados à coleção `Charts` de uma planilha. Você pode especificar o tipo de gráfico, o intervalo de dados e a posição.  
```java
import com.aspose.cells.Chart;
import com.aspose.cells.ChartType;
import com.aspose.cells.Worksheet;

public class CreateChart {
    public static void main(String[] args) {
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Add a column chart
        int idx = worksheet.getCharts().add(ChartType.COLUMN, 6, 5, 20, 13);
        Chart ch = worksheet.getCharts().get(idx);

        // Set the data range for the chart
        ch.setChartDataRange("A1:D4", true);
        
        System.out.println("Column chart created successfully.");
    }
}
```

### 5. Salvar workbook
Chame `save` na instância `Workbook`, fornecendo o caminho de destino e o formato desejado (XLSX, PDF, etc.).  
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.SaveFormat;

public class SaveWorkbook {
    public static void main(String[] args) {
        String outDir = "YOUR_OUTPUT_DIRECTORY";
        Workbook workbook = new Workbook();

        // Save the workbook in XLSX format
        workbook.save(outDir + "EWForChartSetup.xlsx", SaveFormat.XLSX);
        
        System.out.println("Workbook saved as 'EWForChartSetup.xlsx'.");
    }
}
```

## Aplicações práticas
- **Relatórios financeiros** – gerar demonstrações de lucros e perdas trimestrais com gráficos de colunas de escala automática.  
- **Análise de vendas** – produzir painéis de vendas por região que são atualizados diariamente a partir de um banco de dados.  
- **Gestão de inventário** – visualizar tendências de estoque ao longo dos meses para acionar alertas de reposição.

## Considerações de desempenho
Aspose.Cells processa workbooks grandes de forma eficiente, transmitindo dados e reutilizando objetos. Para obter os melhores resultados:
- Processar linhas em lotes ao lidar com > 100 000 registros.  
- Reutilizar uma única instância `Workbook` dentro de loops para evitar alocação repetida de memória.  
- Ajustar o tamanho do heap da JVM (`-Xmx2g` ou superior) se você esperar arquivos com centenas de páginas.

## Perguntas frequentes
**Q: Como adiciono mais de um gráfico na mesma planilha?**  
A: Use `worksheet.getCharts().add(ChartType.COLUMN, upperLeftRow, upperLeftColumn, lowerRightRow, lowerRightColumn)` para cada gráfico que precisar, então defina a fonte de dados de cada gráfico individualmente.

**Q: Posso modificar um arquivo Excel existente em vez de criar um novo?**  
A: Sim—instancie `Workbook` com o caminho do arquivo (`new Workbook("existing.xlsx")`) e então adicione ou edite planilhas e gráficos como mostrado acima.

**Q: Para quais formatos de arquivo posso exportar além de XLSX?**  
A: Aspose.Cells suporta XLS, CSV, PDF, HTML, ODS e mais de 30 formatos adicionais, permitindo conversão perfeita após a criação do gráfico.

**Q: Qual é a maneira recomendada de lidar com conjuntos de dados muito grandes?**  
A: Carregue os dados em blocos, escreva cada bloco na planilha e chame `worksheet.calculateFormula()` somente após todos os dados serem escritos para minimizar a sobrecarga de CPU.

**Q: Onde posso encontrar documentação mais detalhada e exemplos de código?**  
A: Navegue a referência completa na [documentação oficial](https://docs.aspose.com/cells/java/).

## Conclusão
Agora você tem uma receita completa e pronta para produção para **criar arquivo xlsx Java**, preenchê‑lo com dados e gerar um gráfico de colunas usando Aspose.Cells. Integre esses trechos em jobs em lote, serviços web ou ferramentas desktop para automatizar relatórios e análises sem nunca abrir o Excel.

---

**Última atualização:** 2026-09-27  
**Testado com:** Aspose.Cells 24.12 for Java  
**Autor:** Aspose

## Tutoriais Relacionados

- [Domine Aspose.Cells em Java: Configurar Workbook e Visualizar Dados com Gráficos](/cells/java/charts-graphs/aspose-cells-java-setup-data-visualization/)
- [Domine Excel com Aspose.Cells Java: Criação de Workbook e Personalização de Gráficos](/cells/java/charts-graphs/aspose-cells-java-workbook-chart-customization/)
- [Adicionar Rótulos de Dados ao Gráfico Excel com Aspose.Cells Java](/cells/java/advanced-excel-charts/chart-interactivity/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}