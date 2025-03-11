---
title: Aplicar temas no gráfico
linktitle: Aplicar temas no gráfico
second_title: API de processamento do Aspose.Cells .NET Excel
description: Aprenda como aplicar temas a gráficos no Excel usando Aspose.Cells para .NET com nosso guia passo a passo fácil de seguir. Melhore sua apresentação de dados.
weight: 10
url: /pt/net/setting-chart-appearance/apply-themes-in-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aplicar temas no gráfico

## Introdução

Criar gráficos visualmente atraentes no Excel é crucial para comunicar seus dados de forma eficaz. Ao aplicar temas, você pode melhorar a estética de seus gráficos, tornando as informações não apenas acessíveis, mas também envolventes. Neste guia, exploraremos como aplicar temas usando o Aspose.Cells para .NET. Então, pegue seu lanche favorito e vamos mergulhar no mundo criativo dos gráficos!

## Pré-requisitos

Antes de avançarmos para a seção de codificação, há alguns pré-requisitos que você precisa ter em mente.

### Software necessário

1. Visual Studio: Certifique-se de ter o Visual Studio instalado em sua máquina. Ele fornece um ambiente amigável para desenvolver aplicativos .NET.
2. .NET Framework ou .NET Core: Dependendo da sua preferência, você deve ter o .NET Framework ou o .NET Core configurado para acompanhar nosso código.
3.  Aspose.Cells para .NET: Você não pode perder isso! Baixe Aspose.Cells para .NET para começar. Você pode encontrar as DLLs[aqui](https://releases.aspose.com/cells/net/).
4. Conhecimento básico de C#: embora iremos guiá-lo pelo código passo a passo, alguma familiaridade básica com C# certamente ajudará.

## Pacotes de importação

Para trabalhar com Aspose.Cells para .NET, o primeiro passo é importar os pacotes necessários. No seu projeto C#, inclua o seguinte namespace:

```csharp
using System;
using System.IO;

using Aspose.Cells;
using Aspose.Cells.Charts;
```

Agora que cobrimos nossos pré-requisitos, vamos detalhar o processo de aplicação de temas a um gráfico no Excel passo a passo.

## Etapa 1: configure seus diretórios de saída e origem

A primeira coisa que precisamos fazer é estabelecer nosso diretório de saída e diretório de origem. É de lá que você carregará seus arquivos do Excel e onde os arquivos modificados serão salvos.

```csharp
// Diretório de saída
string outputDir = "Your Output Directory";

// Diretório de origem
string sourceDir = "Your Document Directory";
```

 Aqui, substitua`Your Output Directory` e`Your Document Directory` com seus caminhos específicos. Ter esses diretórios claramente definidos simplificará seu fluxo de trabalho e evitará qualquer confusão no futuro.

## Etapa 2: Instanciar a pasta de trabalho

 Em seguida, é hora de abrir o arquivo Excel que contém o gráfico que você deseja modificar. Fazemos isso criando uma instância do`Workbook` classe e carregando nosso arquivo de origem.

```csharp
// Instanciar a pasta de trabalho para abrir o arquivo que contém um gráfico
Workbook workbook = new Workbook(sourceDir + "sampleApplyingThemesInChart.xlsx");
```

 Garantir que`sampleApplyingThemesInChart.xlsx` existe no seu diretório de origem.

## Etapa 3: Acesse a planilha

Agora que configuramos nossa pasta de trabalho, o próximo passo é acessar a planilha específica que contém nosso gráfico. 

```csharp
// Obtenha a primeira planilha
Worksheet worksheet = workbook.Worksheets[0];
```

Neste caso, estamos simplesmente pegando a primeira planilha, o que é suficiente para este exemplo. Se você tiver várias planilhas, você pode especificar o índice ou nome da planilha com base em seus requisitos.

## Etapa 4: Obtenha o gráfico

Com a planilha em mãos, agora podemos acessar o gráfico que pretendemos estilizar.

```csharp
// Obtenha o primeiro gráfico na planilha
Chart chart = worksheet.Charts[0];
```

Aqui estamos buscando o primeiro gráfico. Se sua planilha contiver vários gráficos e você quiser um específico, basta alterar o índice de acordo.

## Etapa 5: aplique preenchimento sólido à série

Antes de aplicar um tema, vamos garantir que nossa série de gráficos tenha um preenchimento sólido. Veja como você pode configurá-lo:

```csharp
// Especifique o tipo do FillFormat para Preenchimento Sólido da primeira série
chart.NSeries[0].Area.FillFormat.FillType = Aspose.Cells.Drawing.FillType.Solid;
```

Esta linha de código garante que a primeira série no gráfico seja definida para usar um preenchimento sólido.

## Etapa 6: Configurar a cor

 Agora que nossa série está pronta, precisamos modificar sua cor. Isso envolve criar uma`CellsColor` objeto e especificando uma cor de tema. Escolheremos um estilo de destaque para este exemplo.

```csharp
//Obter o CellsColor do SolidFill
CellsColor cc = chart.NSeries[0].Area.FillFormat.SolidFill.CellsColor;

// Crie um tema no estilo Accent
cc.ThemeColor = new ThemeColor(ThemeColorType.Accent6, 0.6);
```

Veja o que está acontecendo:
1. Obtemos a cor do preenchimento sólido.
2.  Usando`ThemeColor` , definimos uma cor para nosso preenchimento sólido. Você pode alterar`Accent6` para qualquer outra cor temática, dependendo do que você gosta.

## Etapa 7: Aplique o tema à série

Depois de configurar a cor, é hora de aplicar esse novo tema à nossa série. 

```csharp
// Aplique o tema à série
chart.NSeries[0].Area.FillFormat.SolidFill.CellsColor = cc;
```

Esta linha atualiza efetivamente as cores no gráfico. 

## Etapa 8: Salve a pasta de trabalho

Depois de todo esse trabalho duro, precisamos salvar nossas alterações em um novo arquivo do Excel.

```csharp
// Salvar o arquivo Excel
workbook.Save(outputDir + "outputApplyingThemesInChart.xlsx");
```

Aqui, estamos salvando a pasta de trabalho modificada no diretório de saída que você especificou anteriormente. 

## Etapa 9: Saída de confirmação

Para nos informar que o processo foi executado com sucesso, podemos imprimir uma mensagem de confirmação:

```csharp
Console.WriteLine("ApplyingThemesInChart executed successfully.");
```

Esta linha exibirá uma mensagem no console informando que a tarefa foi concluída.

## Conclusão

Aplicar temas aos seus gráficos no Excel usando o Aspose.Cells para .NET pode transformar completamente a forma como seus dados são visualizados. Isso não só torna seus gráficos esteticamente agradáveis, mas também ajuda a transmitir sua mensagem de forma mais eficaz. Seguindo as etapas descritas neste guia, você pode personalizar facilmente seus gráficos e apresentar seus dados de uma forma que capture a atenção do seu público.

## Perguntas frequentes

### O que é Aspose.Cells?
Aspose.Cells é uma biblioteca poderosa para .NET que permite aos desenvolvedores manipular arquivos do Excel programaticamente.

### Posso experimentar o Aspose.Cells antes de comprar?
 Sim, você pode baixar uma versão de teste gratuita[aqui](https://releases.aspose.com/).

### Que tipos de temas de gráficos posso aplicar?
Aspose.Cells suporta várias cores de tema, incluindo estilos de destaque e outros.

### É possível aplicar temas a vários gráficos?
Absolutamente! Você pode fazer um loop`worksheet.Charts` e aplique temas conforme necessário.

### Onde posso obter suporte para o Aspose.Cells?
 Você pode obter suporte e interagir com uma comunidade de usuários[aqui](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
