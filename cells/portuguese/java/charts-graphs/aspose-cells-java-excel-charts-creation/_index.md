---
date: '2026-04-08'
description: Aprenda a criar um gráfico de linhas com marcadores usando Aspose.Cells
  para Java, adicionar o gráfico à planilha e personalizar gráficos do Excel para
  relatórios automatizados.
keywords:
- line chart with markers
- add chart to worksheet
- automate excel chart creation
- populate data for chart
- export styled chart excel
title: Criar um Gráfico de Linha com Marcadores Usando Aspose.Cells para Java
url: /pt/java/charts-graphs/aspose-cells-java-excel-charts-creation/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Criando e Estilizando Gráficos do Excel com Aspose.Cells Java

## Introdução

No mundo orientado a dados de hoje, um **line chart with markers** é uma das maneiras mais eficazes de visualizar tendências e valores atípicos. Seja construindo relatórios automatizados ou um painel que é atualizado diariamente, poder adicionar programaticamente um line chart with markers a uma planilha economiza inúmeras etapas manuais. Este tutorial orienta você a usar Aspose.Cells para Java para criar, estilizar e exportar tais gráficos, permitindo que você se concentre em insights em vez de ajustes tediosos no Excel.

**O que você aprenderá**
- Inicializar uma pasta de trabalho e preenchê‑la com dados usando Aspose.Cells.  
- **Como adicionar um line chart with markers a uma planilha** e configurar sua aparência.  
- Personalizar cores de séries, marcadores e outras opções de estilo.  
- Salvar a pasta de trabalho como um arquivo Excel que inclui seu gráfico estilizado.

## Respostas Rápidas
- **Qual é a classe principal para iniciar?** `Workbook` inicializa um novo arquivo Excel.  
- **Qual tipo de gráfico cria um line chart with markers?** `ChartType.LINE_WITH_DATA_MARKERS`.  
- **Como definir cores personalizadas para pontos de série?** Use `chart.getNSeries().setColorVaried(true)` e defina cores da área do marcador.  
- **Preciso de uma licença para funcionalidade completa?** Sim, uma licença paga ou temporária do Aspose.Cells remove os limites de avaliação.  
- **Posso exportar o resultado como XLSX?** Absolutamente—`workbook.save("StyledChart.xlsx")` cria um arquivo XLSX.

## Pré-requisitos

Antes de criar e estilizar gráficos usando Aspose.Cells para Java, certifique‑se de que você tem a seguinte configuração:

### Bibliotecas Necessárias
Inclua Aspose.Cells como dependência em seu projeto. Aqui estão as instruções para usuários Maven e Gradle:

**Maven:**
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle:**
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### Requisitos de Configuração do Ambiente
- Java Development Kit (JDK) instalado em seu sistema.  
- Um Ambiente de Desenvolvimento Integrado (IDE) como IntelliJ IDEA ou Eclipse para codificação e testes.

### Pré-requisitos de Conhecimento
É necessário um entendimento básico de programação Java, juntamente com familiaridade com pastas de trabalho Excel e conceitos de gráficos. 

### Aquisição de Licença
Aspose.Cells é um produto comercial que requer licença para funcionalidade completa. Você pode obter um teste gratuito para avaliar seus recursos, solicitar uma licença temporária para testes estendidos ou comprar o produto para uso a longo prazo.

- **Teste Gratuito:** [Download Free Trial](https://releases.aspose.com/cells/java/)  
- **Licença Temporária:** [Solicitar Licença Temporária](https://purchase.aspose.com/temporary-license/)  
- **Compra:** [Comprar Aspose.Cells](https://purchase.aspose.com/buy)

## Configurando Aspose.Cells para Java

Depois de instalar as dependências necessárias, configure seu ambiente de desenvolvimento para usar Aspose.Cells. Comece importando a biblioteca e inicializando um objeto `Workbook` em sua aplicação Java:

```java
import com.aspose.cells.*;

public class SetupAsposeCells {
    public static void main(String[] args) throws Exception {
        // Initialize a new workbook instance
        Workbook workbook = new Workbook();
        
        System.out.println("Workbook initialized successfully!");
    }
}
```

## Guia de Implementação

Nesta seção, vamos dividir a implementação em recursos distintos: Inicialização da Pasta de Trabalho e População de Dados, Criação e Configuração de Gráficos, Personalização de Séries e Salvamento da Pasta de Trabalho.

### Recurso 1: Inicialização da Pasta de Trabalho e População de Dados

**Visão geral:** Este recurso foca em criar uma nova pasta de trabalho, acessar sua primeira planilha e preenchê‑la com dados para a criação do gráfico.

#### Passo 1: Inicializar a Pasta de Trabalho
Comece instanciando um objeto `Workbook`:

```java
import com.aspose.cells.*;

public class FeatureWorkbookInitialization {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

#### Passo 2: Definir Títulos das Colunas e Preencher Dados
Defina os cabeçalhos das colunas e preencha as linhas com dados de exemplo:

```java
        // Set columns title 
        worksheet.getCells().get(0, 0).setValue("X");
        worksheet.getCells().get(0, 1).setValue("Y");

        // Create random data for series 1
        for (int i = 1; i < 21; i++) {
            worksheet.getCells().get(i, 0).setValue(i);
            worksheet.getCells().get(i, 1).setValue(0.8);
        }

        // Create random data for series 2
        for (int i = 21; i < 41; i++) {
            worksheet.getCells().get(i, 0).setValue(i - 20);
            worksheet.getCells().get(i, 1).setValue(0.9);
        }
    }
}
```

### Recurso 2: Criação e Configuração de Gráfico

**Visão geral:** Este recurso demonstra como adicionar um gráfico à planilha da pasta de trabalho, definir seu estilo e configurar propriedades básicas.

#### Passo 3: Adicionar um Gráfico à Planilha
Adicione um line chart with data markers:

```java
import com.aspose.cells.*;

public class FeatureChartCreation {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
        
        // Add chart to the worksheet
        int idx = worksheet.getCharts().add(ChartType.LINE_WITH_DATA_MARKERS, 1, 3, 20, 20);

        // Access and configure the chart
        Chart chart = worksheet.getCharts().get(idx);
        chart.setStyle(3); // Set a predefined style
        chart.setAutoScaling(true);
        chart.getTitle().setText("Sample Chart");
        chart.getCategoryAxis().getTitle().setText("Units");
    }
}
```

### Recurso 3: Configuração e Personalização de Séries

**Visão geral:** Melhore o apelo visual de seus gráficos personalizando as configurações de séries, como cores variadas e estilos de marcadores.

#### Passo 4: Personalizar Configurações de Série
Configure os dados da série, aplique formatação personalizada e ajuste os marcadores:

```java
import com.aspose.cells.*;

public class FeatureSeriesConfiguration {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
        
        // Add series to the chart
        Chart chart = worksheet.getCharts().add(ChartType.LINE_WITH_DATA_MARKERS, 1, 3, 20, 20).get(0);

        int s2_idx = chart.getNSeries().add("A2: A21", true);
        int s3_idx = chart.getNSeries().add("A22: A41", true);

        // Enable varied colors for series points
        chart.getNSeries().setColorVaried(true);

        // Customize first series marker styles and colors
        chart.getNSeries().get(s2_idx).getArea().setFormatting(FormattingType.CUSTOM);
        chart.getNSeries().get(s2_idx).getMarker().getArea().setForegroundColor(Color.getYellow());
        chart.getNSeries().get(s2_idx).getMarker().getBorder().setVisible(false);

        // Set X and Y values for the first series
        chart.getNSeries().get(s2_idx).setXValues("A2: A21");
        chart.getNSeries().get(s2_idx).setValues("B2: B21");

        // Customize second series marker styles and colors
        chart.getNSeries().get(s3_idx).getArea().setFormatting(FormattingType.CUSTOM);
        chart.getNSeries().get(s3_idx).getMarker().getArea().setForegroundColor(Color.getGreen());
        chart.getNSeries().get(s3_idx).getMarker().getBorder().setVisible(false);

        // Set X and Y values for the second series
        chart.getNSeries().get(s3_idx).setXValues("A22: A41");
        chart.getNSeries().get(s3_idx).setValues("B22: B41");
    }
}
```

### Recurso 4: Salvamento da Pasta de Trabalho

**Visão geral:** Finalmente, salve a pasta de trabalho para persistir suas alterações e garantir que o gráfico seja incluído no arquivo Excel.

#### Passo 5: Salvar a Pasta de Trabalho
Salve sua pasta de trabalho com os gráficos recém‑criados:

```java
import com.aspose.cells.*;

public class FeatureWorkbookSaving {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet and add data, chart configuration as per previous steps...
        Worksheet worksheet = workbook.getWorksheets().get(0);
        // (Implementation of adding data and configuring the chart would be here)

        // Save the workbook to an Excel file
        workbook.save("StyledChart.xlsx");
    }
}
```

### Problemas Comuns e Solução de Problemas

- **O gráfico aparece em branco:** Verifique se os intervalos de células usados em `setXValues` e `setValues` referenciam corretamente células preenchidas.  
- **Cores não aplicadas:** Certifique‑se de que `chart.getNSeries().setColorVaried(true)` seja chamado antes de personalizar séries individuais.  
- **Erros de licença:** Uma licença de avaliação pode limitar o número de gráficos; instale uma licença completa para remover restrições.

## Perguntas Frequentes

**P: Posso criar outros tipos de gráfico (por exemplo, barra, pizza) com Aspose.Cells?**  
R: Sim, Aspose.Cells suporta uma ampla variedade de tipos de gráfico; basta substituir `ChartType.LINE_WITH_DATA_MARKERS` pelo valor enum desejado.

**P: Preciso fechar a pasta de trabalho ou liberar recursos?**  
R: A classe `Workbook` gerencia recursos automaticamente, mas você pode chamar `workbook.dispose()` em aplicações de longa duração para liberar memória.

**P: É possível adicionar vários gráficos à mesma planilha?**  
R: Absolutamente—chame `worksheet.getCharts().add(...)` para cada gráfico que desejar inserir.

**P: Como exportar o arquivo como um formato Excel mais antigo (XLS)?**  
R: Use `workbook.save("StyledChart.xls", SaveFormat.EXCEL_97_TO_2003);`.

**P: O gráfico manterá seu estilo ao ser aberto no Microsoft Excel?**  
R: Sim, Aspose.Cells grava objetos de gráfico nativos do Excel, portanto todos os estilos, cores e marcadores aparecem exatamente como definidos.

---

**Última atualização:** 2026-04-08  
**Testado com:** Aspose.Cells 25.3 for Java  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}