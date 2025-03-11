---
title: Adicionar controle TextBox ao gráfico
linktitle: Adicionar controle TextBox ao gráfico
second_title: API de processamento do Aspose.Cells .NET Excel
description: Aprenda como adicionar um TextBox a gráficos no Excel usando Aspose.Cells para .NET. Melhore sua visualização de dados sem esforço.
weight: 12
url: /pt/net/inserting-controls-in-charts/add-textbox-control-to-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Adicionar controle TextBox ao gráfico

## Introdução

Criar gráficos dinâmicos e visualmente atraentes no Excel é uma maneira fantástica de representar dados de forma eficaz. Um recurso bacana que você pode usar é adicionar um TextBox a um gráfico. Com o Aspose.Cells para .NET, essa tarefa se torna fácil e divertida! Neste guia, nós o guiaremos pelo processo de integração de um TextBox ao seu gráfico passo a passo. Seja você um desenvolvedor experiente ou apenas iniciante, este tutorial lhe dará todas as ferramentas necessárias para aprimorar seus gráficos do Excel. Então, você está pronto para mergulhar?

## Pré-requisitos

Antes de começarmos a codificar, há algumas coisas que você deve ter em mente:

- Noções básicas de C#: Uma compreensão fundamental da programação em C# será útil. Não se preocupe; você não precisa ser um especialista, apenas estar confortável navegando pela sintaxe.
-  Biblioteca Aspose.Cells instalada: Certifique-se de ter a biblioteca Aspose.Cells para .NET instalada. Você pode baixá-la em[aqui](https://releases.aspose.com/cells/net/) se você ainda não o fez.
- Visual Studio: É essencial ter familiaridade com o Visual Studio ou qualquer IDE que você prefira usar para o .NET Framework.
- Um arquivo Excel existente: para este exemplo, trabalharemos com um arquivo Excel existente chamado "sampleAddingTextBoxControlInChart.xls". Você pode criar um ou baixar um exemplo.

Agora que temos tudo pronto, vamos para a parte da codificação!

## Pacotes de importação

Primeiro, precisamos importar os namespaces Aspose.Cells necessários para nosso projeto C#. Você pode fazer isso facilmente incluindo as seguintes linhas no topo do seu arquivo de código:

```csharp
using System;
using System.IO;

using Aspose.Cells;
using System.Drawing;
```

## Etapa 1: Defina seus diretórios de origem e saída

Antes de começarmos a trabalhar com o arquivo Excel, é importante definir onde seu arquivo de entrada está localizado e onde você quer salvar o arquivo de saída. Isso ajuda a manter seu projeto organizado.

```csharp
// Diretório de origem
string sourceDir = "Your Document Directory";

// Diretório de saída
string outputDir = "Your Output Directory";
```
 Substituir`"Your Document Directory"` e`"Your Output Directory"` com os caminhos reais no seu sistema.

## Etapa 2: Abra o arquivo Excel existente

Em seguida, precisamos abrir o arquivo Excel que contém o gráfico que queremos modificar. Isso nos permitirá buscar o gráfico e fazer alterações.

```csharp
// Abra o arquivo existente.
Workbook workbook = new Workbook(sourceDir + "sampleAddingTextBoxControlInChart.xls");
```
Esta linha inicializa um novo objeto Workbook com nosso arquivo especificado.

## Etapa 3: Acesse o gráfico na planilha

Como os gráficos no Excel são armazenados em uma planilha, precisamos primeiro acessar a planilha e então obter o gráfico desejado. Para este exemplo, acessaremos o primeiro gráfico na primeira planilha.

```csharp
// Obtenha o gráfico do designer na primeira folha.
Worksheet sheet = workbook.Worksheets[0];
Aspose.Cells.Charts.Chart chart = sheet.Charts[0];
```
Ao alterar o valor do índice, você pode selecionar planilhas ou gráficos diferentes se o seu arquivo tiver mais.

## Etapa 4: adicione uma nova caixa de texto ao gráfico

Agora, estamos prontos para adicionar nossa TextBox. Especificaremos sua posição e tamanho ao criá-la.

```csharp
// Adicione uma nova caixa de texto ao gráfico.
Aspose.Cells.Drawing.TextBox textbox0 = chart.Shapes.AddTextBoxInChart(400, 1100, 350, 2550);
```
Neste comando, os parâmetros definem a localização (x, y) e o tamanho (largura, altura) do TextBox no gráfico. Ajuste esses valores com base em suas necessidades específicas de layout.

## Etapa 5: Defina o texto para a caixa de texto

Depois que o TextBox estiver no lugar, é hora de preenchê-lo com conteúdo. Você pode adicionar qualquer texto que considere necessário para seu gráfico.

```csharp
// Preencha o texto.
textbox0.Text = "Sales By Region";
```
Sinta-se à vontade para substituir "Vendas por região" por qualquer texto relevante para seus dados.

## Etapa 6: ajuste as propriedades da caixa de texto

Agora, vamos fazer com que nossa TextBox fique bonita! Você pode personalizar várias propriedades, como cor da fonte, tamanho e estilo.

```csharp
// Defina a cor da fonte.
textbox0.Font.Color = Color.Maroon; // Mude para a cor desejada

// Defina a fonte como negrito.
textbox0.Font.IsBold = true;

// Defina o tamanho da fonte.
textbox0.Font.Size = 14;

// Defina o atributo de fonte como itálico.
textbox0.Font.IsItalic = true;
```

Cada uma dessas linhas modifica a aparência do texto dentro do seu TextBox, melhorando a visibilidade e o apelo.

## Etapa 7: formatar a aparência da caixa de texto

Também é essencial formatar o fundo e a borda do TextBox. Isso faz com que ele se destaque no gráfico.

```csharp
// Obtenha o formato de preenchimento da caixa de texto.
Aspose.Cells.Drawing.FillFormat fillformat = textbox0.Fill;

// Obtenha o tipo de formato de linha da caixa de texto.
Aspose.Cells.Drawing.LineFormat lineformat = textbox0.Line;

// Defina a espessura da linha.
lineformat.Weight = 2;

// Defina o estilo do traço como sólido.
lineformat.DashStyle = Aspose.Cells.Drawing.MsoLineDashStyle.Solid;
```

Essas opções permitem que você defina o preenchimento de fundo da caixa de texto e personalize sua borda.

## Etapa 8: Salve o arquivo Excel modificado

O último passo é salvar as alterações que você fez em um novo arquivo do Excel. Isso garantirá que seu arquivo original permaneça intocado.

```csharp
// Salve o arquivo Excel.
workbook.Save(outputDir + "outputAddingTextBoxControlInChart.xls");
```
 Substituir`"outputAddingTextBoxControlInChart.xls"` com o nome de arquivo que você preferir.

## Conclusão

Parabéns! Você adicionou com sucesso um controle TextBox a um gráfico usando Aspose.Cells para .NET. Essa mudança simples, mas eficaz, pode tornar seus gráficos mais informativos e visualmente atraentes. A representação de dados é essencial para uma comunicação eficaz e, com ferramentas como o Aspose, você tem o poder de aprimorar essa apresentação com o mínimo de esforço.

## Perguntas frequentes

### O que é Aspose.Cells para .NET?
Aspose.Cells para .NET é uma biblioteca poderosa para criar, manipular e converter arquivos do Excel sem precisar depender do Microsoft Excel.

### Posso adicionar várias caixas de texto a um único gráfico?
Sim! Você pode adicionar quantas TextBoxes precisar repetindo os passos de criação de TextBox com posições diferentes.

### O Aspose.Cells é gratuito?
Aspose.Cells é uma biblioteca paga, mas você pode baixar uma versão de teste gratuita em[aqui](https://releases.aspose.com/).

### Onde posso encontrar mais documentação sobre o Aspose.Cells?
 Você pode acessar documentação abrangente[aqui](https://reference.aspose.com/cells/net/).

### Como obtenho suporte se tiver problemas?
 Você pode buscar assistência através do fórum de suporte do Aspose[aqui](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
