---
"date": "2025-04-08"
"description": "Aprenda a criar e personalizar gráficos de pizza usando Aspose.Cells para Java. Um guia passo a passo com exemplos de código para desenvolvedores."
"title": "Dominando o Aspose.Cells&#58; Crie e personalize gráficos de pizza em Java"
"url": "/pt/java/charts-graphs/create-customize-aspose-cells-pie-chart-java/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}


# Dominando Aspose.Cells: Crie e personalize gráficos de pizza em Java

## Introdução
Criar gráficos visualmente atraentes é um requisito comum ao lidar com visualização de dados no Excel. Seja para apresentar informações demográficas ou analisar tendências de mercado, os gráficos de pizza oferecem uma maneira clara de representar dados proporcionais. No entanto, configurar esses gráficos programaticamente pode ser complexo. Este tutorial orienta você na criação e personalização de um gráfico de pizza Aspose.Cells usando Java, simplificando o processo para desenvolvedores.

**O que você aprenderá:**
- Configure seu ambiente com Aspose.Cells para Java.
- Crie uma nova pasta de trabalho e acesse as células da planilha.
- Preencha dados em células específicas para preparar a criação do gráfico.
- Gere um gráfico de pizza a partir desses dados.
- Personalize a aparência do seu gráfico de pizza, incluindo cores, títulos e legendas.

Antes de começar, certifique-se de ter noções básicas de programação Java e gerenciamento de dependências em Maven ou Gradle. Vamos configurar nosso ambiente!

## Pré-requisitos
Para acompanhar este tutorial, você precisará:
- **Kit de Desenvolvimento Java (JDK)**: Versão 8 ou superior.
- **Ambiente de Desenvolvimento Integrado (IDE)**: Como IntelliJ IDEA ou Eclipse.
- **Gerenciamento de Dependências**: Use Maven ou Gradle para gerenciar suas dependências.

### Bibliotecas e dependências necessárias
Certifique-se de incluir o Aspose.Cells para Java no seu projeto usando Maven ou Gradle.

**Especialista**
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle**
```gradle
implementation 'com.aspose:aspose-cells:25.3'
```

### Etapas de aquisição de licença
Aspose.Cells para Java é uma biblioteca comercial, mas você pode começar com um teste gratuito ou solicitar uma licença temporária. Visite o [página de compra](https://purchase.aspose.com/buy) para explorar opções de licenciamento.

## Configurando Aspose.Cells para Java
Primeiramente, certifique-se de que o ambiente do seu projeto inclua as bibliotecas necessárias, adicionando-as por meio do Maven ou Gradle, conforme mostrado acima. Uma vez incluídas, você pode inicializar o Aspose.Cells:

```java
import com.aspose.cells.Workbook;

// Inicializar uma nova instância da pasta de trabalho
Workbook workbook = new Workbook();
```

## Guia de Implementação

### Criar e configurar uma pasta de trabalho
Criar uma pasta de trabalho é o passo inicial em que você configurará seus dados.

#### Importar bibliotecas
Certifique-se de que essas importações estejam incluídas no topo do seu arquivo:

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

#### Etapa 1: Criar uma instância de pasta de trabalho
```java
// Cria uma instância de pasta de trabalho vazia para trabalhar.
Workbook workbook = new Workbook();
```
Esta etapa inicializa seu arquivo Excel programaticamente, permitindo que você o manipule usando as funcionalidades do Aspose.Cells.

### Acessar ou modificar células da planilha
Em seguida, preencha os dados nas células da planilha que serão usadas para o gráfico de pizza.

#### Etapa 2: Acessar uma planilha e suas células
```java
// Acesse a primeira planilha na pasta de trabalho.
Worksheet worksheet = workbook.getWorksheets().get(0);
Cells cells = worksheet.getCells();

// Coloque valores de amostra usados para um gráfico de pizza em células específicas.
cells.get("C3").putValue("India");
cells.get("C4").putValue("China");
cells.get("C5").parseNumber("United States", true, null);
cells.get("C6").setValue("Russia");
cells.get("C7").setValue("United Kingdom");
cells.get("C8").setValue("Others");

// Coloque valores percentuais de um gráfico de pizza em células específicas.
cells.get("D2").putValue("% of world population");
cells.get("D3").putValue(25);
cells.get("D4").putValue(30);
cells.get("D5").putValue(10);
cells.get("D6").putValue(13);
cells.get("D7").putValue(9);
cells.get("D8").putValue(13);
```
Aqui, você preenche a planilha com dados que representarão diferentes segmentos de um gráfico de pizza.

### Criar um gráfico de pizza

#### Etapa 3: adicione um gráfico de pizza à planilha
```java
// Crie um gráfico de pizza na planilha.
int pieIdx = worksheet.getCharts().add(ChartType.PIE, 1, 6, 15, 14);
Chart pie = worksheet.getCharts().get(pieIdx);
```
Esta etapa adiciona um novo gráfico de pizza à sua planilha em posições e dimensões especificadas.

### Configurar séries e dados do gráfico de pizza

#### Etapa 4: Defina a série para o gráfico
```java
// Configure o intervalo de dados da série para o gráfico.
pie.getNSeries().add("D3:D8", true);
pie.getNSeries().setCategoryData("=Sheet1!$C$3:$C$8");

// Vincule o título do gráfico de pizza a uma célula que contém o texto do título.
pie.getTitle().setLinkedSource("D2");
```
Este código vincula seu intervalo de dados e configura a série para o gráfico de pizza.

### Configurar a legenda do gráfico e a aparência do título

#### Etapa 5: personalize a legenda e o título do gráfico
```java
// Defina a posição da legenda na parte inferior do gráfico.
pie.getLegend().setPosition(LegendPositionType.BOTTOM);

// Defina as propriedades da fonte para o título do gráfico.
pie.getTitle().getFont().setName("Calibri");
pie.getTitle().getFont().setSize(18);
```
Personalizar a aparência melhora a legibilidade e o apelo visual.

### Personalizar cores da série do gráfico

#### Etapa 6: alterar as cores dos segmentos da pizza
```java
import com.aspose.cells.Color;

// Acesse e personalize as cores de segmentos individuais do gráfico de pizza.
Series srs = pie.getNSeries().get(0);
srs.getPoints().get(0).getArea().setForegroundColor(Color.fromArgb(0, 246, 22, 219));
srs.getPoints().get(1).getArea().setForegroundColor(Color.fromArgb(0, 51, 34, 84));
srs.getPoints().get(2).getArea().setForegroundColor(Color.fromArgb(0, 46, 74, 44));
srs.getPoints().get(3).getArea().setForegroundColor(Color.fromArgb(0, 19, 99, 44));
srs.getPoints().get(4).getArea().setForegroundColor(Color.fromArgb(0, 208, 223, 7));
srs.getPoints().get(5).getArea().setForegroundColor(Color.fromArgb(0, 222, 69, 8));
```
Essas configurações personalizam seu gráfico para se ajustar a esquemas de cores específicos.

### Ajustar colunas automaticamente e salvar pasta de trabalho

#### Etapa 7: ajuste as larguras das colunas e salve o arquivo
```java
// Ajustar automaticamente todas as colunas.
worksheet.autoFitColumns();

// Defina o caminho do espaço reservado do diretório de saída para salvar a pasta de trabalho.
String outDir = "YOUR_OUTPUT_DIRECTORY";

// Salve a pasta de trabalho modificada em um arquivo Excel no diretório especificado.
workbook.save(outDir + "/CSOrSColorsPieChart_out.xlsx", SaveFormat.XLSX);
```
Por fim, ajuste automaticamente as colunas e salve sua pasta de trabalho.

## Aplicações práticas
1. **Análise Demográfica**: Use gráficos de pizza para exibir distribuições populacionais em diferentes países ou regiões.
2. **Relatórios de Participação de Mercado**: Ilustrar a participação de mercado de diferentes empresas em um setor.
3. **Alocação Orçamentária**: Visualize como os orçamentos são alocados entre vários departamentos dentro de uma organização.

Esses aplicativos demonstram a versatilidade e a utilidade do Aspose.Cells em cenários do mundo real.

## Considerações de desempenho
Para otimizar o desempenho ao usar Aspose.Cells:
- Minimize o uso de memória descartando objetos que não são mais necessários.
- Use estruturas de dados eficientes para processar grandes conjuntos de dados.
- Crie um perfil do seu aplicativo para identificar gargalos.

adesão às melhores práticas garante aplicativos fluidos e responsivos.

## Conclusão
Este tutorial orientou você nas etapas para criar e personalizar um gráfico de pizza usando o Aspose.Cells em Java. Com esse conhecimento, você poderá aplicar essas técnicas a diversas tarefas de visualização de dados em seus projetos. Para explorar mais a fundo, considere explorar outros tipos de gráficos e opções avançadas de personalização disponíveis com o Aspose.Cells.


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}