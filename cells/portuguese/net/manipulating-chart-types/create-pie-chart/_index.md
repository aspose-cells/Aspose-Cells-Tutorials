---
"description": "Aprenda a criar um gráfico de pizza no Excel usando o Aspose.Cells para .NET com este guia passo a passo. Visualize seus dados sem esforço."
"linktitle": "Criar gráfico de pizza"
"second_title": "API de processamento do Excel Aspose.Cells .NET"
"title": "Criar gráfico de pizza"
"url": "/pt/net/manipulating-chart-types/create-pie-chart/"
"weight": 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Criar gráfico de pizza

## Introdução

Criar gráficos é essencial para representar dados visualmente, e gráficos de pizza são uma das maneiras mais populares de ilustrar como as partes formam um todo. Com o Aspose.Cells para .NET, você pode automatizar facilmente a geração de gráficos de pizza em arquivos do Excel. Neste tutorial, vamos nos aprofundar em como criar um gráfico de pizza do zero usando o Aspose.Cells para .NET, com um guia passo a passo para tornar o processo simples e fácil. Seja você iniciante na ferramenta ou buscando aprimorar suas habilidades de automação do Excel, este guia tem tudo o que você precisa!

## Pré-requisitos

Antes de mergulhar no código, certifique-se de ter o seguinte configurado:

1. Biblioteca Aspose.Cells para .NET: Certifique-se de ter o Aspose.Cells instalado em seu projeto. Se ainda não o instalou, você pode baixá-lo em [aqui](https://releases.aspose.com/cells/net/).
2. Ambiente de desenvolvimento .NET: certifique-se de que seu projeto esteja configurado para usar o .NET Framework ou o .NET Core.
3. Conhecimento básico de C#: você deve estar familiarizado com programação em C#, especialmente programação orientada a objetos (POO).

Para usuários avançados, uma licença temporária pode ser aplicada para desbloquear todos os recursos do Aspose.Cells. Você pode solicitar uma em [aqui](https://purchase.aspose.com/temporary-license/).

## Pacotes de importação

Para começar, importe os namespaces e pacotes necessários para este tutorial. Estes incluem operações básicas de E/S e o pacote Aspose.Cells.

```csharp
using System;
using System.IO;

using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
using Aspose.Cells.Charts;
```

## Etapa 1: Criar uma nova pasta de trabalho

Primeiro, precisamos criar uma instância do `Workbook` class, que representa o arquivo do Excel. Uma pasta de trabalho contém várias planilhas e, no nosso exemplo, trabalharemos com duas planilhas — uma para dados e outra para o gráfico de pizza.

```csharp
Workbook workbook = new Workbook();
```

Isso inicializa uma nova pasta de trabalho do Excel. Mas para onde vão os dados? Vamos cuidar disso na próxima etapa.

## Etapa 2: Adicionar dados à planilha

Após a criação da pasta de trabalho, precisamos acessar a primeira planilha e dar um nome a ela. É aqui que inseriremos os dados necessários para o gráfico de pizza.

```csharp
Worksheet sheet = workbook.Worksheets[0];
sheet.Name = "Data";
Cells cells = sheet.Cells;
```

Agora, podemos inserir alguns dados fictícios de vendas representando diferentes regiões:

```csharp
cells["A1"].PutValue("Region");
cells["A2"].PutValue("France");
cells["A3"].PutValue("Germany");
cells["A4"].PutValue("England");
cells["A5"].PutValue("Sweden");
cells["A6"].PutValue("Italy");
cells["A7"].PutValue("Spain");
cells["A8"].PutValue("Portugal");

cells["B1"].PutValue("Sales");
cells["B2"].PutValue(70000);
cells["B3"].PutValue(55000);
cells["B4"].PutValue(30000);
cells["B5"].PutValue(40000);
cells["B6"].PutValue(35000);
cells["B7"].PutValue(32000);
cells["B8"].PutValue(10000);
```

Aqui, estamos adicionando duas colunas: uma para regiões e outra para números de vendas. Esses dados serão representados no gráfico de pizza.

## Etapa 3: Adicionar uma planilha de gráfico

Em seguida, vamos adicionar uma planilha separada para armazenar o gráfico de pizza.

```csharp
int sheetIndex = workbook.Worksheets.Add(SheetType.Chart);
Worksheet chartSheet = workbook.Worksheets[sheetIndex];
chartSheet.Name = "Chart";
```

Esta nova planilha hospedará o gráfico de pizza. Nomeá-lo como "Gráfico" garante que os usuários saibam o que esperar ao abrir o arquivo.

## Etapa 4: Crie o gráfico de pizza

Agora é hora de criar o gráfico propriamente dito. Especificaremos que queremos um gráfico de pizza e definiremos sua posição na planilha.

```csharp
int chartIndex = chartSheet.Charts.Add(Aspose.Cells.Charts.ChartType.Pie, 5, 0, 25, 10);
Aspose.Cells.Charts.Chart chart = chartSheet.Charts[chartIndex];
```

O método `Add()` aceita parâmetros para o tipo de gráfico (neste caso, `ChartType.Pie`) e sua localização na planilha. Os números representam as posições das linhas e colunas.

## Etapa 5: personalize a aparência do gráfico

Um gráfico de pizza não estaria completo sem alguma personalização! Vamos deixar nosso gráfico visualmente atraente ajustando as cores, os rótulos e o título.

### Definir título do gráfico
```csharp
chart.Title.Text = "Sales By Region";
chart.Title.Font.Color = Color.Blue;
chart.Title.Font.IsBold = true;
chart.Title.Font.Size = 12;
```

### Personalizar área de plotagem
```csharp
chart.PlotArea.Area.ForegroundColor = Color.Coral;
chart.PlotArea.Area.FillFormat.SetTwoColorGradient(Color.Yellow, Color.White, GradientStyleType.Vertical, 2);
chart.PlotArea.Border.IsVisible = false;
```

Definimos o preenchimento de gradiente para a área de plotagem e ocultamos a borda para uma aparência mais limpa.

## Etapa 6: Definir dados do gráfico

É hora de vincular o gráfico aos nossos dados. O `NSeries` propriedade do gráfico vincula os números de vendas e regiões ao gráfico de pizza.

```csharp
chart.NSeries.Add("Data!B2:B8", true);
chart.NSeries.CategoryData = "Data!A2:A8";
chart.NSeries.IsColorVaried = true;
```

A primeira linha especifica que estamos usando os dados de vendas das células `B2:B8`. Também informamos ao gráfico para usar os nomes das regiões de `A2:A8` como rótulos de categoria.

## Etapa 7: Adicionar rótulos de dados

Adicionar rótulos diretamente aos segmentos do gráfico pode facilitar a compreensão. Vamos incluir os nomes das regiões e os valores de vendas nas fatias do gráfico de pizza.

```csharp
for (int i = 0; i < chart.NSeries.Count; i++)
{
    DataLabels labels = chart.NSeries[i].DataLabels;
    labels.ShowCategoryName = true;
    labels.ShowValue = true;
    labels.Position = LabelPositionType.InsideBase;
}
```

## Etapa 8: personalizar a área do gráfico e a legenda

Por fim, vamos dar alguns retoques finais à área do gráfico e à legenda. Isso aprimora a apresentação geral do gráfico.

### Área do gráfico
```csharp
ChartArea chartArea = chart.ChartArea;
chartArea.Area.Formatting = FormattingType.Custom;
chartArea.Area.FillFormat.Texture = TextureType.BlueTissuePaper;
```

### Lenda
```csharp
Legend legend = chart.Legend;
legend.Position = LegendPositionType.Left;
legend.Font.IsBold = true;
legend.Border.Color = Color.Blue;
legend.Area.FillFormat.Texture = TextureType.Bouquet;
```

## Etapa 9: Salve a pasta de trabalho

Por fim, salvamos a pasta de trabalho em um arquivo Excel. Você pode especificar o diretório de saída e o nome do arquivo conforme necessário.

```csharp
workbook.Save(outputDir + "outputHowToCreatePieChart.xlsx");
```

## Conclusão

Criar um gráfico de pizza com o Aspose.Cells para .NET é um processo simples e personalizável. Seguindo este guia, você pode gerar um gráfico com aparência profissional que transmite insights valiosos em apenas algumas etapas. Seja para relatórios comerciais ou fins educacionais, dominar a criação de gráficos elevará suas habilidades de automação do Excel. Lembre-se: o Aspose.Cells oferece a flexibilidade necessária para criar arquivos Excel impressionantes e baseados em dados sem esforço.

## Perguntas frequentes

### Posso criar outros tipos de gráficos usando o Aspose.Cells para .NET?
Sim! O Aspose.Cells suporta vários tipos de gráficos, incluindo gráficos de barras, gráficos de linhas e gráficos de dispersão.

### Preciso de uma licença paga para usar o Aspose.Cells para .NET?
Você pode usar a versão gratuita com algumas limitações. Para obter todos os recursos, você precisará de uma licença, que pode ser adquirida [aqui](https://purchase.aspose.com/buy).

### Posso exportar o gráfico para formatos como PDF ou imagens?
Com certeza! O Aspose.Cells permite exportar gráficos para vários formatos, incluindo PDF e PNG.

### É possível estilizar cada fatia de torta com cores diferentes?
Sim, você pode aplicar cores diferentes a cada fatia definindo o `IsColorVaried` propriedade para `true`, conforme mostrado no tutorial.

### Posso automatizar a geração de vários gráficos em uma única pasta de trabalho?
Sim, você pode criar e personalizar quantos gráficos precisar em um único arquivo do Excel.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}