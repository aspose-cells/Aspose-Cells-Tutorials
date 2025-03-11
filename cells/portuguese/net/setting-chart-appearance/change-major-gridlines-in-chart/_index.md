---
title: Alterar as principais linhas de grade no gráfico
linktitle: Alterar as principais linhas de grade no gráfico
second_title: API de processamento do Aspose.Cells .NET Excel
description: Aprenda como alterar as principais linhas de grade em gráficos do Excel usando o Aspose.Cells para .NET com nosso guia passo a passo detalhado.
weight: 11
url: /pt/net/setting-chart-appearance/change-major-gridlines-in-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Alterar as principais linhas de grade no gráfico

## Introdução

Criar gráficos visualmente atraentes no Excel é essencial para uma apresentação de dados eficaz. Seja você um analista de dados, um gerente de projeto ou apenas alguém interessado em visualização de dados, entender como personalizar gráficos pode melhorar significativamente seus relatórios. Neste artigo, aprenderemos como alterar as principais linhas de grade em um gráfico do Excel usando a biblioteca Aspose.Cells para .NET.

## Pré-requisitos

Antes de começar, há algumas coisas que você precisa ter em mãos para garantir uma experiência tranquila ao trabalhar com o Aspose.Cells:

- Visual Studio: Certifique-se de ter o Visual Studio instalado no seu computador. É aqui que você escreverá e executará seu código.
-  Aspose.Cells para .NET: Você pode baixar a versão mais recente do Aspose.Cells do[site](https://releases.aspose.com/cells/net/) . Se você quiser experimentar antes de comprar, considere se inscrever em um[teste gratuito](https://releases.aspose.com/).
- Conhecimento básico de C#: A familiaridade com a programação em C# tornará mais fácil acompanhar os exemplos deste tutorial.

Depois que tudo estiver configurado, podemos começar a escrever nosso código!

## Pacotes de importação

Para trabalhar com Aspose.Cells, o primeiro passo é importar os pacotes necessários no seu projeto C#. Abra seu projeto do Visual Studio e inclua as seguintes diretivas using no topo do seu arquivo C#:

```csharp
using Aspose.Cells;
using Aspose.Cells.Charts;
using System.Drawing;
```

Esses pacotes permitem que você acesse as classes e os métodos necessários para criar e modificar pastas de trabalho e gráficos do Excel.

Agora, vamos dividir o processo em etapas detalhadas e fáceis de seguir. Criaremos um gráfico simples com alguns dados e, em seguida, mudaremos a cor de suas principais linhas de grade.

## Etapa 1: Defina seu diretório de saída

A primeira coisa que você vai querer fazer é definir onde você quer salvar o arquivo Excel de saída. Isso é feito especificando um caminho de diretório no seu código:

```csharp
// Diretório de saída
string outputDir = "Your Output Directory"; // Atualize com o caminho desejado
```

 Substituir`"Your Output Directory"` com o caminho real onde você deseja salvar seu arquivo.

## Etapa 2: Instanciar um objeto de pasta de trabalho

 Em seguida, você precisa criar uma nova instância do`Workbook` classe. Este objeto representará seu arquivo Excel, permitindo que você manipule seu conteúdo.

```csharp
// Instanciando um objeto Workbook
Workbook workbook = new Workbook();
```

Esta linha de código inicializa uma nova pasta de trabalho, que fornecerá uma tela em branco para nossa planilha e gráfico.

## Etapa 3: Acesse a planilha

 Após criar a pasta de trabalho, você pode acessar sua planilha padrão. As planilhas em Aspose.Cells são indexadas, então se você quiser a primeira planilha, você se refere a ela pelo índice`0`.

```csharp
// Obtendo a referência da planilha recém-adicionada passando seu índice de planilha
Worksheet worksheet = workbook.Worksheets[0];
```

## Etapa 4: preencher a planilha com dados de amostra

Vamos adicionar alguns valores de amostra nas células da planilha, que servirão como dados para nosso gráfico. Isso é importante porque o gráfico fará referência a esses dados.

```csharp
// Adicionar valores de amostra às células
worksheet.Cells["A1"].PutValue(50);
worksheet.Cells["A2"].PutValue(100);
worksheet.Cells["A3"].PutValue(150);
worksheet.Cells["B1"].PutValue(60);
worksheet.Cells["B2"].PutValue(32);
worksheet.Cells["B3"].PutValue(50);
```

Aqui, inserimos vários valores numéricos em células específicas. As colunas "A" e "B" contêm os pontos de dados que visualizaremos.

## Etapa 5: Adicionar um gráfico à planilha

Com nossos dados no lugar, é hora de criar um gráfico. Adicionaremos um gráfico de colunas que visualiza nosso conjunto de dados.

```csharp
// Adicionar um gráfico à planilha
int chartIndex = worksheet.Charts.Add(Aspose.Cells.Charts.ChartType.Column, 5, 0, 25, 10);
```

Neste código, especificamos o tipo de gráfico (neste caso, um gráfico de colunas) e a posição onde queremos colocá-lo.

## Etapa 6: Acesse a instância do gráfico

 Depois de criar o gráfico, precisamos acessar sua instância para modificar suas propriedades. Isso é feito recuperando-o por meio do`Charts`coleção.

```csharp
// Acessando a instância do gráfico recém-adicionado
Aspose.Cells.Charts.Chart chart = worksheet.Charts[chartIndex];
```

## Etapa 7: Adicionar séries de dados ao gráfico

Agora precisamos vincular nossos dados ao gráfico. Isso envolve especificar as células como a fonte de dados para o gráfico.

```csharp
// Adicionar SeriesCollection (fonte de dados do gráfico) ao gráfico que varia da célula "A1" até "B3"
chart.NSeries.Add("A1:B3", true);
```

Nesta etapa, informamos ao gráfico o intervalo de dados que ele deve visualizar.

## Etapa 8: Personalize a aparência do gráfico

Vamos enfeitar um pouco nosso gráfico mudando as cores da área de plotagem, área do gráfico e coleções de séries. Isso ajudará nosso gráfico a se destacar e melhorar seu apelo visual.

```csharp
// Definir a cor de primeiro plano da área de plotagem
chart.PlotArea.Area.ForegroundColor = Color.Blue;

// Definir a cor de primeiro plano da área do gráfico
chart.ChartArea.Area.ForegroundColor = Color.Yellow;

// Definindo a cor de primeiro plano da área 1st SeriesCollection
chart.NSeries[0].Area.ForegroundColor = Color.Red;

// Definindo a cor de primeiro plano da área do 1º ponto SeriesCollection
chart.NSeries[0].Points[0].Area.ForegroundColor = Color.Cyan;

// Preenchendo a área da 2ª SeriesCollection com um gradiente
chart.NSeries[1].Area.FillFormat.SetOneColorGradient(Color.Lime, 1, Aspose.Cells.Drawing.GradientStyleType.Horizontal, 1);
```

Neste código, definimos várias cores para diferentes partes do gráfico. Personalizar a aparência pode tornar seus dados muito mais envolventes!

## Etapa 9: Alterar as cores das principais linhas de grade

Agora, para o evento principal! Para melhorar a legibilidade, mudaremos a cor das principais linhas de grade ao longo de ambos os eixos do nosso gráfico.

```csharp
// Definir a cor das principais linhas de grade do Eixo de Categoria para prata
chart.CategoryAxis.MajorGridLines.Color = Color.Silver;

// Definir a cor das principais linhas de grade do Value Axis para vermelho
chart.ValueAxis.MajorGridLines.Color = Color.Red;
```

Esses comandos definem as principais linhas de grade para os eixos de categoria e valor para prata e vermelho, respectivamente. Essa diferenciação garante que seus visualizadores possam seguir facilmente as linhas de grade no gráfico.

## Etapa 10: Salve a pasta de trabalho

Após fazer todas as suas modificações, é hora de salvar a pasta de trabalho. Este é o passo final que traz seu esforço à fruição.

```csharp
// Salvando o arquivo Excel
workbook.Save(outputDir + "outputChangingMajorGridlinesInChart.xlsx");
```

Esta linha salva o arquivo Excel recém-criado no diretório de saída especificado com um nome que reflete sua finalidade.

## Etapa 11: Mensagem de confirmação

Por fim, vamos adicionar uma mensagem para confirmar que nossa tarefa foi bem-sucedida:

```csharp
Console.WriteLine("Changing Major Gridlines in Chart executed successfully.");
```

Esta saída simples do console informa que seu programa foi executado corretamente e sem problemas.

## Conclusão

aí está! Você aprendeu com sucesso como alterar as principais linhas de grade em um gráfico usando o Aspose.Cells para .NET. Ao seguir este guia passo a passo, você não apenas manipulou arquivos do Excel programaticamente, mas também melhorou seu apelo visual com personalizações de cores. Sinta-se à vontade para experimentar mais com o Aspose.Cells para aprofundar suas habilidades de apresentação de dados e tornar seus gráficos ainda mais dinâmicos!

## Perguntas frequentes

### O que é Aspose.Cells?  
Aspose.Cells é uma biblioteca .NET projetada para criar, manipular e gerenciar arquivos do Excel programaticamente.

### Posso testar o Aspose.Cells gratuitamente?  
 Sim, você pode se inscrever para um teste gratuito[aqui](https://releases.aspose.com/).

### Como posso alterar outros elementos em um gráfico usando Aspose.Cells?  
 Você pode personalizar várias propriedades do gráfico de forma semelhante acessando os elementos do gráfico por meio do`Chart` classe, como títulos, legendas e rótulos de dados.

### Quais formatos de arquivo o Aspose.Cells suporta?  
O Aspose.Cells suporta vários formatos de arquivo, incluindo XLSX, XLS, CSV e outros.

### Onde posso encontrar documentação para Aspose.Cells?  
 Você pode consultar a documentação detalhada em[Documentação do Aspose.Cells](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
