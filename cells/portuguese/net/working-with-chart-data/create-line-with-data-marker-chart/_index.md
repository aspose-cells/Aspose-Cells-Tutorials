---
title: Criar linha com gráfico de marcadores de dados
linktitle: Criar linha com gráfico de marcadores de dados
second_title: API de processamento do Aspose.Cells .NET Excel
description: Aprenda a criar um gráfico de Linha com Marcadores de Dados no Excel usando Aspose.Cells para .NET. Siga este guia passo a passo para gerar e personalizar gráficos facilmente.
weight: 10
url: /pt/net/working-with-chart-data/create-line-with-data-marker-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar linha com gráfico de marcadores de dados

## Introdução

Você já se perguntou como criar gráficos impressionantes no Excel programaticamente? Bem, aperte os cintos, porque hoje vamos mergulhar na criação de um Gráfico de Linha com Marcador de Dados usando o Aspose.Cells para .NET. Este tutorial o guiará por cada etapa, garantindo que você tenha uma compreensão firme da geração de gráficos, mesmo se estiver apenas começando com o Aspose.Cells.

## Pré-requisitos

Antes de começar, certifique-se de que você tem tudo pronto para seguir adiante sem problemas.

1. Aspose.Cells para .NET Library – Você precisará instalar isso. Você pode obtê-lo[aqui](https://releases.aspose.com/cells/net/).
2. .NET Framework – Certifique-se de que seu ambiente de desenvolvimento esteja configurado com a versão mais recente do .NET.
3. IDE (Ambiente de Desenvolvimento Integrado) – Visual Studio é recomendado.
4.  Uma licença Aspose.Cells válida – Se você não tiver uma, pode solicitar uma[licença temporária](https://purchase.aspose.com/temporary-license/) ou confira o deles[teste gratuito](https://releases.aspose.com/).

Pronto para ir? Vamos decompor!

## Importando Pacotes Necessários

Para começar, certifique-se de importar os seguintes namespaces para seu projeto. Eles fornecerão as classes e métodos necessários para criar seu gráfico.

```csharp
using System;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Charts;
using System.Drawing;
```

Depois que você tiver entendido isso, podemos começar a programar!

## Etapa 1: configure sua pasta de trabalho e planilha

Primeiramente, você precisa criar uma nova pasta de trabalho e acessar a primeira planilha.

```csharp
//Diretório de saída
static string outputDir = "Your Document Directory";
		
// Instanciar uma pasta de trabalho
Workbook workbook = new Workbook();

// Acesse a primeira planilha
Worksheet worksheet = workbook.Worksheets[0];
```

Pense na pasta de trabalho como seu arquivo Excel e na planilha como a planilha específica dentro dela. Neste caso, estamos trabalhando com a primeira planilha.

## Etapa 2: preencher a planilha com dados

Agora que temos nossa planilha, vamos preenchê-la com alguns dados. Estamos criando pontos de dados aleatórios para duas séries de valores.

```csharp
// Definir título das colunas
worksheet.Cells[0, 0].Value = "X";
worksheet.Cells[0, 1].Value = "Y";

// Dados aleatórios para gerar o gráfico
Random R = new Random();

// Crie dados aleatórios e salve nas células
for (int i = 1; i < 21; i++)
{
    worksheet.Cells[i, 0].Value = i;
    worksheet.Cells[i, 1].Value = 0.8;
}

for (int i = 21; i < 41; i++)
{
    worksheet.Cells[i, 0].Value = i - 20;
    worksheet.Cells[i, 1].Value = 0.9;
}
```

Aqui, estamos usando números aleatórios para simular dados, mas em aplicações da vida real, você pode preenchê-los com valores reais do seu conjunto de dados.

## Etapa 3: adicione o gráfico à planilha

Em seguida, adicionamos o gráfico à planilha e escolhemos o tipo – neste caso, um gráfico de linhas com marcadores de dados.

```csharp
// Adicionar um gráfico à planilha
int idx = worksheet.Charts.Add(ChartType.LineWithDataMarkers, 1, 3, 20, 20);

// Acesse o gráfico recém-criado
Chart chart = worksheet.Charts[idx];
```

Este snippet adiciona um gráfico de linha com marcadores de dados à planilha, colocando-o em um intervalo específico (1,3 a 20,20). Bem simples, certo?

## Etapa 4: personalize a aparência do gráfico

Depois que o gráfico for criado, você pode estilizá-lo como preferir. Vamos mudar o plano de fundo, o título e o estilo do gráfico.

```csharp
// Definir estilo de gráfico
chart.Style = 3;

// Defina o valor de dimensionamento automático como verdadeiro
chart.AutoScaling = true;

// Definir cor de primeiro plano para branco
chart.PlotArea.Area.ForegroundColor = Color.White;

//Definir propriedades do título do gráfico
chart.Title.Text = "Sample Chart";

// Definir tipo de gráfico
chart.Type = ChartType.LineWithDataMarkers;
```

Aqui, estamos dando ao gráfico uma aparência limpa, definindo um fundo branco, dimensionando automaticamente e dando a ele um título significativo.

## Etapa 5: Definir séries e pontos de dados do gráfico

Agora que nosso gráfico está bom, precisamos definir as séries de dados que serão plotadas.

```csharp
// Definir propriedades do título do eixo da categoria
chart.CategoryAxis.Title.Text = "Units";

// Defina duas séries para o gráfico
int s2_idx = chart.NSeries.Add("A2: A21", true);
int s3_idx = chart.NSeries.Add("A22: A41", true);
```

Essas séries correspondem aos intervalos de pontos de dados que preenchemos anteriormente.

## Etapa 6: adicione cores e personalize os marcadores de série

Vamos tornar este gráfico ainda mais atraente adicionando cores personalizadas aos nossos marcadores de dados.

```csharp
// Personalize a primeira série
chart.NSeries[s2_idx].Marker.Area.ForegroundColor = Color.Yellow;
chart.NSeries[s2_idx].Marker.Border.IsVisible = false;

// Personalize a segunda série
chart.NSeries[s3_idx].Marker.Area.ForegroundColor = Color.Green;
chart.NSeries[s3_idx].Marker.Border.IsVisible = false;
```

Ao personalizar as cores, você torna o gráfico não apenas funcional, mas também visualmente atraente!

## Etapa 7: Defina os valores X e Y para cada série

Por fim, vamos atribuir os valores X e Y para cada uma das nossas séries.

```csharp
// Defina os valores X e Y da primeira série
chart.NSeries[s2_idx].XValues = "A2: A21";
chart.NSeries[s2_idx].Values = "B2: B21";

// Defina os valores X e Y da segunda série
chart.NSeries[s3_idx].XValues = "A22: A41";
chart.NSeries[s3_idx].Values = "B22: B41";
```

Os valores são baseados nos dados que preenchemos na etapa 2.

## Etapa 8: Salve a pasta de trabalho

Agora que tudo está definido, vamos salvar a pasta de trabalho para que possamos ver o gráfico em ação.

```csharp
// Salvar a pasta de trabalho
workbook.Save(outputDir + @"LineWithDataMarkerChart.xlsx", Aspose.Cells.SaveFormat.Xlsx);
```

E é isso! Você acabou de criar um gráfico de linhas com marcadores de dados usando Aspose.Cells for .NET.

## Conclusão

Criar gráficos programaticamente no Excel pode parecer assustador, mas com o Aspose.Cells para .NET, é tão fácil quanto seguir uma receita passo a passo. Da configuração da sua pasta de trabalho à personalização da aparência do gráfico, esta biblioteca poderosa cuida de tudo. Não importa se você está criando relatórios, painéis ou visualizações de dados, o Aspose.Cells permite que você faça isso facilmente.

## Perguntas frequentes

### Posso personalizar ainda mais o gráfico?  
Absolutamente! O Aspose.Cells oferece uma tonelada de opções de personalização, de fontes a linhas de grade e muito mais.

### Preciso de uma licença para usar o Aspose.Cells?  
 Sim, é necessária uma licença para funcionalidade completa. Você pode obter uma[licença temporária](https://purchase.aspose.com/temporary-license/) ou comece com um[teste gratuito](https://releases.aspose.com/).

### Como posso adicionar mais séries de dados?  
 Basta adicionar séries adicionais usando o`NSeries.Add` método, especificando os intervalos de células para os novos dados.

### Posso exportar o gráfico como uma imagem?  
 Sim, você pode exportar gráficos diretamente como imagens usando o`Chart.ToImage` método.

### O Aspose.Cells suporta gráficos 3D?  
Sim, o Aspose.Cells suporta uma ampla variedade de tipos de gráficos, incluindo gráficos 3D.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
