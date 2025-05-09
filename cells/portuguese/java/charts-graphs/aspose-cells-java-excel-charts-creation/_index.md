---
"date": "2025-04-07"
"description": "Aprenda a criar e personalizar gráficos no Excel usando o Aspose.Cells para Java. Automatize a criação de gráficos, aprimore a visualização de dados e economize tempo com este guia detalhado."
"title": "Criação e estilização de gráficos do Excel com Aspose.Cells Java - Um guia completo"
"url": "/pt/java/charts-graphs/aspose-cells-java-excel-charts-creation/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Criação e estilização de gráficos do Excel com Aspose.Cells Java

## Introdução

No mundo atual, orientado por dados, a visualização eficaz de informações é crucial para análises e tomadas de decisão. Muitas vezes, é necessário criar gráficos dinâmicos em pastas de trabalho do Excel programaticamente, especialmente ao lidar com grandes conjuntos de dados ou sistemas de relatórios automatizados. Este tutorial demonstra como usar o Aspose.Cells para Java para criar e personalizar gráficos no Excel de forma integrada. Ao integrar o Aspose.Cells aos seus aplicativos Java, você pode automatizar a criação de gráficos, aprimorar a apresentação de dados e economizar tempo.

**O que você aprenderá:**
- Inicializando uma pasta de trabalho e preenchendo-a com dados usando Aspose.Cells.
- Criação e configuração de gráficos de linhas com marcadores de dados.
- Personalização da aparência e cores das séries para melhor visualização.
- Salvando a pasta de trabalho com o gráfico recém-criado em formato Excel.

Vamos começar discutindo os pré-requisitos necessários para começar.

## Pré-requisitos

Antes de criar e estilizar gráficos usando o Aspose.Cells para Java, certifique-se de ter a seguinte configuração:

### Bibliotecas necessárias
Inclua Aspose.Cells como dependência no seu projeto. Aqui estão as instruções para usuários do Maven e do Gradle:

**Especialista:**
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

### Requisitos de configuração do ambiente
- Java Development Kit (JDK) instalado no seu sistema.
- Um Ambiente de Desenvolvimento Integrado (IDE), como IntelliJ IDEA ou Eclipse, para codificação e testes.

### Pré-requisitos de conhecimento
É necessário um conhecimento básico de programação Java, além de familiaridade com pastas de trabalho do Excel e conceitos de gráficos. 

### Aquisição de Licença
O Aspose.Cells é um produto comercial que requer uma licença para funcionar plenamente. Você pode obter uma avaliação gratuita para avaliar seus recursos, solicitar uma licença temporária para testes mais longos ou comprar o produto para uso de longo prazo.

- **Teste gratuito:** [Baixe a versão de avaliação gratuita](https://releases.aspose.com/cells/java/)
- **Licença temporária:** [Solicitar Licença Temporária](https://purchase.aspose.com/temporary-license/)
- **Comprar:** [Compre Aspose.Cells](https://purchase.aspose.com/buy)

## Configurando Aspose.Cells para Java

Após instalar as dependências necessárias, configure seu ambiente de desenvolvimento para usar Aspose.Cells. Comece importando a biblioteca e inicializando um objeto Workbook em seu aplicativo Java:

```java
import com.aspose.cells.*;

public class SetupAsposeCells {
    public static void main(String[] args) throws Exception {
        // Inicializar uma nova instância da pasta de trabalho
        Workbook workbook = new Workbook();
        
        System.out.println("Workbook initialized successfully!");
    }
}
```

## Guia de Implementação

Nesta seção, dividiremos a implementação em recursos distintos: Inicialização da pasta de trabalho e preenchimento de dados, Criação e configuração de gráficos, Personalização de séries e Salvamento da pasta de trabalho.

### Recurso 1: Inicialização da pasta de trabalho e preenchimento de dados

**Visão geral:** Este recurso se concentra na criação de uma nova pasta de trabalho, acessando sua primeira planilha e preenchê-la com dados para criação de gráficos.

#### Etapa 1: inicializar a pasta de trabalho
Comece instanciando um `Workbook` objeto:

```java
import com.aspose.cells.*;

public class FeatureWorkbookInitialization {
    public static void main(String[] args) throws Exception {
        // Instanciar uma pasta de trabalho
        Workbook workbook = new Workbook();
        
        // Acesse a primeira planilha
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

#### Etapa 2: definir títulos de colunas e preencher dados
Defina os cabeçalhos das colunas e preencha as linhas com dados de amostra:

```java
        // Definir título das colunas 
        worksheet.getCells().get(0, 0).setValue("X");
        worksheet.getCells().get(0, 1).setValue("Y");

        // Crie dados aleatórios para a série 1
        for (int i = 1; i < 21; i++) {
            worksheet.getCells().get(i, 0).setValue(i);
            worksheet.getCells().get(i, 1).setValue(0.8);
        }

        // Crie dados aleatórios para a série 2
        for (int i = 21; i < 41; i++) {
            worksheet.getCells().get(i, 0).setValue(i - 20);
            worksheet.getCells().get(i, 1).setValue(0.9);
        }
    }
}
```

### Recurso 2: Criação e configuração de gráficos

**Visão geral:** Este recurso demonstra como adicionar um gráfico à planilha da pasta de trabalho, definir seu estilo e configurar propriedades básicas.

#### Etapa 3: adicionar um gráfico à planilha
Adicione um gráfico de linhas com marcadores de dados:

```java
import com.aspose.cells.*;

public class FeatureChartCreation {
    public static void main(String[] args) throws Exception {
        // Instanciar uma pasta de trabalho
        Workbook workbook = new Workbook();
        
        // Acesse a primeira planilha
        Worksheet worksheet = workbook.getWorksheets().get(0);
        
        // Adicionar gráfico à planilha
        int idx = worksheet.getCharts().add(ChartType.LINE_WITH_DATA_MARKERS, 1, 3, 20, 20);

        // Acessar e configurar o gráfico
        Chart chart = worksheet.getCharts().get(idx);
        chart.setStyle(3); // Defina um estilo predefinido
        chart.setAutoScaling(true);
        chart.getTitle().setText("Sample Chart");
        chart.getCategoryAxis().getTitle().setText("Units");
    }
}
```

### Recurso 3: Configuração e personalização da série

**Visão geral:** Melhore o apelo visual dos seus gráficos personalizando as configurações da série, como cores variadas e estilos de marcadores.

#### Etapa 4: personalizar as configurações da série
Configure dados de série, aplique formatação personalizada e ajuste marcadores:

```java
import com.aspose.cells.*;

public class FeatureSeriesConfiguration {
    public static void main(String[] args) throws Exception {
        // Instanciar uma pasta de trabalho
        Workbook workbook = new Workbook();
        
        // Acesse a primeira planilha
        Worksheet worksheet = workbook.getWorksheets().get(0);
        
        // Adicionar séries ao gráfico
        Chart chart = worksheet.getCharts().add(ChartType.LINE_WITH_DATA_MARKERS, 1, 3, 20, 20).get(0);

        int s2_idx = chart.getNSeries().add("A2: A21", true);
        int s3_idx = chart.getNSeries().add("A22: A41", true);

        // Habilitar cores variadas para pontos de série
        chart.getNSeries().setColorVaried(true);

        // Personalize os estilos e cores dos marcadores da primeira série
        chart.getNSeries().get(s2_idx).getArea().setFormatting(FormattingType.CUSTOM);
        chart.getNSeries().get(s2_idx).getMarker().getArea().setForegroundColor(Color.getYellow());
        chart.getNSeries().get(s2_idx).getMarker().getBorder().setVisible(false);

        // Defina os valores X e Y para a primeira série
        chart.getNSeries().get(s2_idx).setXValues("A2: A21");
        chart.getNSeries().get(s2_idx).setValues("B2: B21");

        // Personalize os estilos e cores dos marcadores da segunda série
        chart.getNSeries().get(s3_idx).getArea().setFormatting(FormattingType.CUSTOM);
        chart.getNSeries().get(s3_idx).getMarker().getArea().setForegroundColor(Color.getGreen());
        chart.getNSeries().get(s3_idx).getMarker().getBorder().setVisible(false);

        // Defina os valores X e Y para a segunda série
        chart.getNSeries().get(s3_idx).setXValues("A22: A41");
        chart.getNSeries().get(s3_idx).setValues("B22: B41");
    }
}
```

### Recurso 4: Salvamento de pasta de trabalho

**Visão geral:** Por fim, salve a pasta de trabalho para manter suas alterações e garantir que o gráfico seja incluído no arquivo Excel.

#### Etapa 5: Salve a pasta de trabalho
Salve sua pasta de trabalho com os gráficos recém-criados:

```java
import com.aspose.cells.*;

public class FeatureWorkbookSaving {
    public static void main(String[] args) throws Exception {
        // Instanciar uma pasta de trabalho
        Workbook workbook = new Workbook();
        
        // Acesse a primeira planilha e adicione dados, configuração do gráfico conforme as etapas anteriores...
        Worksheet worksheet = workbook.getWorksheets().get(0);
        // (A implementação da adição de dados e configuração do gráfico seria aqui)

        // Salvar a pasta de trabalho em um arquivo Excel
        workbook.save("StyledChart.xlsx");
    }
}
```

**Recomendações de palavras-chave:**
- "Aspose.Cells para Java"
- "Criação de gráficos do Excel com Java"
- "Programação Java para automação do Excel"

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}