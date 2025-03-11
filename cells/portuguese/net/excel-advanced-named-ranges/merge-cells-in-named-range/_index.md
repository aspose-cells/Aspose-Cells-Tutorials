---
title: Mesclar células em um intervalo nomeado no Excel
linktitle: Mesclar células em um intervalo nomeado no Excel
second_title: API de processamento do Aspose.Cells .NET Excel
description: Aprenda como mesclar células em um intervalo nomeado usando Aspose.Cells for .NET neste tutorial passo a passo. Descubra como formatar, estilizar e automatizar relatórios do Excel.
weight: 11
url: /pt/net/excel-advanced-named-ranges/merge-cells-in-named-range/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Mesclar células em um intervalo nomeado no Excel

## Introdução

Ao trabalhar com arquivos do Excel programaticamente, uma das tarefas comuns que você pode encontrar é mesclar células dentro de um intervalo nomeado. Não importa se você está automatizando a geração de relatórios, criando painéis ou simplesmente gerenciando grandes conjuntos de dados, mesclar células é uma técnica essencial. Neste tutorial, exploraremos como mesclar células em um intervalo nomeado usando o Aspose.Cells para .NET — uma biblioteca poderosa que permite que os desenvolvedores manipulem arquivos do Excel sem precisar do Microsoft Excel instalado.

## Pré-requisitos

Antes de começar, certifique-se de ter o seguinte pronto:

-  Aspose.Cells para .NET: Você pode baixá-lo do[Página de lançamentos do Aspose.Cells](https://releases.aspose.com/cells/net/).
- .NET Framework instalado na sua máquina.
- Conhecimento básico de C#: familiaridade com conceitos como classes, métodos e objetos ajudará.

## Pacotes de importação

Antes de começarmos a codificar, você precisa importar os namespaces necessários. Esses namespaces darão a você acesso à funcionalidade da biblioteca Aspose.Cells.

```csharp
using System;
using System.IO;
using Aspose.Cells;
```

Com os pré-requisitos e pacotes resolvidos, vamos para a parte divertida: a codificação!

Veja aqui uma análise de como você pode mesclar células em um intervalo nomeado em uma planilha do Excel usando o Aspose.Cells para .NET.

## Etapa 1: Crie uma nova pasta de trabalho

A primeira coisa que precisamos é de uma pasta de trabalho. Uma pasta de trabalho em termos do Excel é o equivalente a um arquivo do Excel. Vamos criar uma.

```csharp
// Instanciar uma nova pasta de trabalho.
Workbook wb1 = new Workbook();
```

Ao inicializar uma nova pasta de trabalho, agora temos um arquivo Excel vazio pronto para ser manipulado. É como começar com uma tela em branco!

## Etapa 2: Acesse a primeira planilha

Cada pasta de trabalho contém planilhas e, neste caso, queremos trabalhar com a primeira. Vamos pegá-la!

```csharp
// Obtenha a primeira planilha na pasta de trabalho.
Worksheet worksheet1 = wb1.Worksheets[0];
```

Pense na planilha como as abas individuais em um arquivo Excel onde os dados reais vivem. Por padrão, estamos acessando a primeira aba.

## Etapa 3: Crie um intervalo de células

Agora que temos nossa planilha, é hora de criar um intervalo. Um intervalo se refere a um bloco de células, que pode abranger várias linhas e colunas.

```csharp
//Crie um intervalo.
Range mrange = worksheet1.Cells.CreateRange("D6", "I12");
```

Aqui, estamos selecionando células de D6 a I12 — um bloco que abrange várias linhas e colunas. Em breve, mesclaremos esse intervalo!

## Etapa 4: Nomeie o intervalo

Nomear um intervalo facilita sua referência posterior, especialmente ao lidar com grandes conjuntos de dados.

```csharp
// Dê um nome ao intervalo.
mrange.Name = "TestRange";
```

Ao nomear esse intervalo "TestRange", podemos recuperá-lo rapidamente mais tarde no código, sem precisar especificar as coordenadas da célula novamente.

## Etapa 5: Mesclar o intervalo de células

Agora, a mágica é mesclar as células dentro do intervalo que acabamos de criar!

```csharp
// Mesclar as células do intervalo.
mrange.Merge();
```

Esta etapa mescla todas as células de D6 a I12 em uma única célula. Perfeito para coisas como títulos ou resumos!

## Etapa 6: recuperar o intervalo nomeado

Depois que as células forem mescladas, podemos querer aplicar alguma formatação. Vamos primeiro recuperar nosso intervalo nomeado.

```csharp
// Obtenha o alcance.
Range range1 = wb1.Worksheets.GetRangeByName("TestRange");
```

Recuperar o intervalo pelo nome nos permite realizar outras operações, como adicionar estilos ou inserir dados.

## Etapa 7: Defina um estilo para as células mescladas

De que serve uma célula mesclada se ela não parece polida? Vamos criar um objeto de estilo para alinhar o texto e aplicar uma cor de fundo.

```csharp
// Defina um objeto de estilo.
Style style = wb1.CreateStyle();

// Defina o alinhamento.
style.HorizontalAlignment = TextAlignmentType.Center;
style.VerticalAlignment = TextAlignmentType.Center;
style.Pattern = BackgroundType.Solid;
style.ForegroundColor = System.Drawing.Color.Aqua;
```

Aqui, estamos alinhando o texto horizontalmente e verticalmente no centro, e definindo uma cor de fundo azul claro (aqua). Elegante, certo?

## Etapa 8: aplique o estilo ao intervalo

Depois de definir o estilo, é hora de aplicá-lo ao intervalo mesclado.

```csharp
// Crie um objeto StyleFlag.
StyleFlag flag = new StyleFlag();

// Ative o atributo de estilo relativo.
flag.HorizontalAlignment = true;
flag.VerticalAlignment = true;
flag.CellShading = true;

// Aplique o estilo ao intervalo.
range1.ApplyStyle(style, flag);
```

 O`StyleFlag` informa ao Aspose.Cells quais propriedades de estilo aplicar — alinhamento, sombreamento, etc. Isso lhe dá controle granular sobre como o estilo é aplicado.

## Etapa 9: Insira dados no intervalo mesclado

O que é um intervalo formatado sem conteúdo? Vamos adicionar algum texto.

```csharp
// Insira dados no intervalo.
range1[0, 0].PutValue("Welcome to Aspose APIs.");
```

Isso coloca o texto "Welcome to Aspose APIs" na primeira célula do nosso intervalo mesclado. Com a célula sendo mesclada, esse texto se estenderá por todas as células de D6 a I12.

## Etapa 10: Salve o arquivo Excel

Por fim, vamos salvar a pasta de trabalho como um arquivo Excel.

```csharp
// Salve o arquivo Excel.
wb1.Save(dataDir + "outputMergeCellsInNamedRange.xlsx");
```

Aqui, a pasta de trabalho é salva com o nome "outputMergeCellsInNamedRange.xlsx" no diretório especificado.

## Conclusão

E aí está! Você mesclou células com sucesso em um intervalo nomeado, aplicou uma formatação bonita e até mesmo inseriu alguns dados — tudo com o Aspose.Cells para .NET. Quer você esteja trabalhando na automação de relatórios, manipulando arquivos do Excel ou apenas aprendendo novas técnicas, este guia passo a passo deve lhe dar a base necessária.

## Perguntas frequentes

### Posso mesclar vários intervalos não contíguos no Aspose.Cells?  
Não, você só pode mesclar células contíguas em Aspose.Cells.

### Posso desfazer uma operação de mesclagem programaticamente?  
 Depois que as células forem mescladas, você pode desfazê-las usando o`UnMerge()` método em Aspose.Cells.

### Mesclar células remove os dados contidos nelas?  
Se houver dados nas células antes da mesclagem, os dados da primeira célula do intervalo serão mantidos.

### Posso aplicar estilos diferentes a células individuais dentro de um intervalo mesclado?  
Não, um intervalo mesclado atua como uma única célula, então você não pode aplicar estilos diferentes a células individuais dentro dele.

### Como faço para acessar uma célula mesclada após a mesclagem?  
Após a mesclagem, você ainda pode acessar a célula mesclada usando as coordenadas do canto superior esquerdo.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
