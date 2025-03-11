---
title: Gráfico de renderização
linktitle: Gráfico de renderização
second_title: API de processamento do Aspose.Cells .NET Excel
description: Descubra como renderizar gráficos em .NET usando Aspose.Cells. Siga nosso tutorial passo a passo para criar visuais impressionantes sem esforço.
weight: 10
url: /pt/net/chart-rendering-and-conversion/render-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Gráfico de renderização

## Introdução

Os gráficos são um elemento essencial na apresentação e análise de dados, tornando informações complexas facilmente digeríveis. Se você estiver trabalhando com .NET e precisar gerar gráficos programaticamente, o Aspose.Cells é uma biblioteca poderosa que fornece recursos intuitivos e avançados para lidar com arquivos e gráficos do Excel. Neste guia, percorreremos o processo de renderização de um gráfico usando o Aspose.Cells para .NET. Prepare-se para mergulhar neste tutorial detalhado, que foi projetado para ser envolvente e fácil de seguir!

## Pré-requisitos

Antes de pularmos para o código, vamos garantir que você tenha tudo pronto. Aqui está o que você precisa:

1. Ambiente .NET: Certifique-se de ter um ambiente de desenvolvimento .NET configurado. Você pode usar o Visual Studio ou qualquer outro IDE que suporte .NET.
2.  Aspose.Cells para .NET: Você precisa ter a biblioteca Aspose.Cells instalada. Você pode baixá-la em[Página de lançamento do Aspose](https://releases.aspose.com/cells/net/).
3. Conhecimento básico de C#: a familiaridade com a programação em C# ajudará você a entender melhor os exemplos, mas não se preocupe se você for novo — este guia explicará tudo passo a passo!

## Pacotes de importação

O primeiro passo na sua jornada de codificação é importar os pacotes necessários. Abra seu projeto no seu IDE e adicione o seguinte namespace:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Rendering;
```

Esses namespaces fornecerão acesso à funcionalidade oferecida pela biblioteca Aspose.Cells, permitindo que você crie e manipule seus gráficos sem problemas.


Agora que cobrimos os pré-requisitos e importações, vamos mergulhar nos detalhes da renderização de um gráfico! Vamos dividir isso em etapas claras e gerenciáveis.

## Etapa 1: configure seu diretório de saída

Antes de criarmos nossa pasta de trabalho e gráfico, precisamos estabelecer onde nossas saídas serão salvas. Dessa forma, quando nosso gráfico for gerado, você saberá exatamente onde encontrá-lo.

```csharp
string outputDir = "Your Output Directory"; // Especifique o diretório de saída aqui.
```

Certifique-se de substituir "Seu diretório de saída" pelo caminho onde você deseja salvar as imagens do gráfico.

## Etapa 2: Crie uma pasta de trabalho

Em seguida, vamos instanciar uma nova pasta de trabalho. É aqui que toda a mágica acontece!

```csharp
Workbook workbook = new Workbook();
```

 Esta linha cria uma nova instância do`Workbook` classe, que nos permite trabalhar com planilhas e gráficos.

## Etapa 3: Adicionar uma nova planilha

Agora que temos nossa pasta de trabalho, é hora de adicionar uma nova planilha. Pense nas planilhas como páginas diferentes em um caderno, onde você pode manter seus dados organizados.

```csharp
int sheetIndex = workbook.Worksheets.Add();
Worksheet worksheet = workbook.Worksheets[sheetIndex];
```

Aqui, adicionamos uma nova planilha e obtemos uma referência a ela. Você trabalhará com essa planilha para inserir seus dados e gráficos.

## Etapa 4: Insira valores de amostra

Com nossa planilha criada, vamos adicionar alguns dados de amostra às células. Esses dados são os que seu gráfico será baseado, então escolha valores que façam sentido para seu tipo de gráfico!

```csharp
worksheet.Cells["A1"].PutValue(50);
worksheet.Cells["A2"].PutValue(100);
worksheet.Cells["A3"].PutValue(150);
worksheet.Cells["B1"].PutValue(4);
worksheet.Cells["B2"].PutValue(20);
worksheet.Cells["B3"].PutValue(50);
```

Neste snippet, estamos preenchendo as células "A1" a "A3" com alguns valores numéricos e as células "B1" a "B3" com outro conjunto de valores. Sinta-se à vontade para personalizar esses números para atender às suas necessidades!

## Etapa 5: Crie um gráfico

Agora, é hora de criar seu gráfico. Adicionaremos um tipo de gráfico de colunas, que é ótimo para comparar valores.

```csharp
int chartIndex = worksheet.Charts.Add(ChartType.Column, 5, 0, 15, 5);
Aspose.Cells.Charts.Chart chart = worksheet.Charts[chartIndex];
```

Aqui, estamos adicionando um gráfico no local especificado definindo seu layout: o primeiro conjunto de números representa a posição do gráfico na grade.

## Etapa 6: Adicionar séries de dados ao gráfico

Com o gráfico criado, agora precisamos vinculá-lo aos dados que inserimos nas etapas anteriores.

```csharp
chart.NSeries.Add("A1:B3", true);
```

Esta linha conecta a série de dados do gráfico aos valores nas células "A1" a "B3". Isso significa que seu gráfico representará visualmente os dados conforme pretendido.

## Etapa 7: Salve o gráfico como uma imagem

Agora vamos converter nosso gráfico em um formato de imagem, para que ele possa ser facilmente compartilhado e visualizado.

```csharp
chart.ToImage(outputDir + "outputChartRendering.emf", System.Drawing.Imaging.ImageFormat.Emf);
```

Nesta etapa, salvamos o gráfico como uma imagem EMF (Enhanced Metafile) no diretório de saída especificado. Você também pode salvá-lo em diferentes formatos, como BMP ou PNG.

## Etapa 8: converter gráfico em bitmap

Se você preferir trabalhar com bitmaps, veja como converter seu gráfico para um formato Bitmap.

```csharp
System.Drawing.Bitmap bitmap = chart.ToImage();
bitmap.Save(outputDir + "outputChartRendering.bmp", System.Drawing.Imaging.ImageFormat.Bmp);
```

Isso salvará seu gráfico como uma imagem BMP. Lembre-se, os arquivos BMP tendem a ser maiores, mas são de qualidade incrivelmente alta!

## Etapa 9: Renderização com opções avançadas

Também podemos renderizar o gráfico com algumas opções avançadas de imagem para melhor qualidade e resolução. Vamos configurar algumas opções:

```csharp
ImageOrPrintOptions options = new ImageOrPrintOptions()
{
    VerticalResolution = 300,
    HorizontalResolution = 300,
    SmoothingMode = System.Drawing.Drawing2D.SmoothingMode.AntiAlias
};
```

Essas opções ajudam a melhorar a qualidade visual da imagem gerada, especialmente úteis para apresentações ou publicações.

## Etapa 10: converter gráfico em imagem com opções avançadas

Agora vamos converter o gráfico usando as opções avançadas que acabamos de definir.

```csharp
chart.ToImage(outputDir + "outputChartRendering.png", options);
```

Isso salva seu gráfico como um arquivo PNG com configurações de qualidade aprimoradas.

## Etapa 11: Exportando o gráfico para PDF

Por fim, se você quiser um documento refinado e fácil de compartilhar, você pode exportar seu gráfico diretamente para um formato PDF.

```csharp
chart.ToPdf(outputDir + "outputChartRendering.pdf");
```

Esta etapa criará um PDF que contém seu gráfico, tornando-o perfeito para relatórios digitais ou para compartilhamento com colegas.

## Conclusão 

Parabéns! Você renderizou com sucesso um gráfico usando o Aspose.Cells para .NET. Esta biblioteca poderosa simplifica a criação e manipulação de arquivos e gráficos do Excel, tornando seus dados muito mais acessíveis e visualmente atraentes. Não importa se você está preparando relatórios, análises ou apresentações, os gráficos causam um impacto significativo e, com o Aspose, você pode criá-los programaticamente com facilidade.

## Perguntas frequentes

### Que tipos de gráficos posso criar com o Aspose.Cells para .NET?
Você pode criar uma variedade de gráficos, incluindo gráficos de colunas, linhas, pizza e barras, entre outros.

### Posso personalizar a aparência dos gráficos?
Sim, o Aspose.Cells permite ampla personalização, incluindo cores, estilos e elementos de gráfico.

### Existe um teste gratuito disponível?
Absolutamente! Você pode baixar uma versão de teste gratuita em[aqui](https://releases.aspose.com/).

### Onde posso obter suporte para o Aspose.Cells?
 Você pode encontrar suporte e recursos da comunidade em[Fórum de suporte Aspose](https://forum.aspose.com/c/cells/9).

### Preciso de uma licença para usar o Aspose.Cells?
 Sim, é necessária uma licença para uso contínuo além do período de teste, mas você pode solicitar uma licença temporária[aqui](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
