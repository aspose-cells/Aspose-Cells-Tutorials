---
title: Remover intervalo nomeado no Excel
linktitle: Remover intervalo nomeado no Excel
second_title: API de processamento do Aspose.Cells .NET Excel
description: Aprenda como remover intervalos nomeados no Excel usando o Aspose.Cells para .NET com instruções detalhadas passo a passo.
weight: 11
url: /pt/net/excel-managing-named-ranges/remove-named-range/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Remover intervalo nomeado no Excel

## Introdução
Excel se tornou um item básico no gerenciamento e análise de dados para muitas pessoas e organizações. Seja você um analista de dados experiente ou simplesmente alguém que gosta de organizar seus dados, dominar o Excel é essencial. Hoje, estamos mergulhando em um recurso específico, mas poderoso: remover intervalos nomeados usando o Aspose.Cells para .NET. Este guia o guiará pelas etapas para fazer isso de forma eficaz. Então, arregace as mangas e vamos começar!

## Pré-requisitos

Antes de começarmos a codificação propriamente dita, há algumas coisas que você precisa ter em mente:

### Configuração do ambiente .NET

Para trabalhar com o Aspose.Cells para .NET perfeitamente, certifique-se de ter o seguinte:

1.  Visual Studio: Baixe e instale o Visual Studio (Community Edition é perfeitamente adequado), que você pode encontrar no[Site do Visual Studio](https://visualstudio.microsoft.com/).
2. .NET Framework: Certifique-se de que você esteja usando uma versão apropriada do .NET Framework. O Aspose.Cells suporta o .NET Framework 4.0 e superior.
3. Biblioteca Aspose.Cells: Você precisa baixar e referenciar a biblioteca Aspose.Cells for .NET em seu aplicativo. Você pode encontrar o pacote para download[aqui](https://releases.aspose.com/cells/net/).

### Noções básicas de C#

Você precisará de um entendimento básico de programação em C#. Isso ajudará você a entender os trechos de código que discutiremos.

### Acesso a arquivos do Excel

Certifique-se de ter um arquivo Excel à mão para experimentar. Se não tiver, você pode criar um rapidamente usando o Microsoft Excel.

## Pacotes de importação

Agora que cobrimos nossos pré-requisitos, vamos importar os pacotes que precisaremos em nosso projeto. Abra o Visual Studio e crie um novo aplicativo de console. Em seguida, inclua o seguinte namespace em seu programa:

```csharp
using System;
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

Esta configuração permite que você aproveite as funcionalidades fornecidas pelo Aspose.Cells para manipular planilhas do Excel facilmente.

## Etapa 1: Configurando o diretório de saída

Primeiro, precisamos definir onde nosso arquivo de saída será salvo. Isso é crucial, pois evita confusões mais tarde sobre onde seus arquivos estão.

```csharp
// Diretório de saída
string outputDir = "Your Document Directory Here\\";
```

 Substituir`"Your Document Directory Here\\"`com o caminho no seu computador onde você deseja salvar o arquivo.

## Etapa 2: Instanciando uma nova pasta de trabalho

Como começar com uma lousa nova? Criando uma nova pasta de trabalho, é claro! Esta pasta de trabalho servirá como nossa tela em branco.

```csharp
// Instanciar uma nova pasta de trabalho.
Workbook workbook = new Workbook();
```

Esta linha de código cria uma nova pasta de trabalho que podemos manipular.

## Etapa 3: Acessando a coleção de planilhas

Cada workbook consiste em uma ou mais planilhas. Para trabalhar em uma planilha específica, precisamos acessar esta coleção.

```csharp
// Obtenha todas as planilhas do livro.
WorksheetCollection worksheets = workbook.Worksheets;
```

Aqui, recuperamos todas as planilhas disponíveis em nossa nova pasta de trabalho.

## Etapa 4: Selecionando a primeira planilha

Em seguida, queremos operar dentro da primeira planilha, o ponto de partida padrão em muitos casos.

```csharp
// Obtenha a primeira planilha na coleção de planilhas.
Worksheet worksheet = workbook.Worksheets[0];
```

Este trecho de código nos permite selecionar a primeira planilha facilmente.

## Etapa 5: Criando intervalos nomeados

Agora, vamos criar um intervalo nomeado, que é uma parte essencial deste tutorial. Isso nos permitirá ilustrar como remover um intervalo nomeado mais tarde.

```csharp
// Crie um intervalo de células.
Range range1 = worksheet.Cells.CreateRange("E12", "I12");

// Dê um nome ao intervalo.
range1.Name = "FirstRange";
```

Aqui, definimos um intervalo das células E12 a I12 e o chamamos de “FirstRange”.

## Etapa 6: Formatando o intervalo nomeado

Para demonstrar o quão versátil o Aspose.Cells pode ser, vamos adicionar alguma formatação ao nosso intervalo nomeado.

```csharp
// Defina a borda do contorno para o intervalo.
range1.SetOutlineBorder(BorderType.TopBorder, CellBorderType.Medium, Color.FromArgb(0, 0, 128));
range1.SetOutlineBorder(BorderType.BottomBorder, CellBorderType.Medium, Color.FromArgb(0, 0, 128));
range1.SetOutlineBorder(BorderType.LeftBorder, CellBorderType.Medium, Color.FromArgb(0, 0, 128));
range1.SetOutlineBorder(BorderType.RightBorder, CellBorderType.Medium, Color.FromArgb(0, 0, 128));
```

Estamos adicionando uma borda média azul marinho ao redor da nossa linha para torná-la visualmente atraente.

## Etapa 7: Inserindo dados no intervalo

Em seguida, podemos preencher nossas células com alguns dados para torná-las funcionais.

```csharp
// Insira alguns dados com algumas formatações em algumas células do intervalo.
range1[0, 0].PutValue("Test");            
range1[0, 4].PutValue(123);
```

Nesta etapa, colocamos a palavra "Teste" na célula E12 e o número 123 na célula I12.

## Etapa 8: Criando outro intervalo nomeado

Para ilustrar melhor nosso ponto, criaremos outro intervalo nomeado semelhante ao primeiro.

```csharp
//Crie outro intervalo de células.
Range range2 = worksheet.Cells.CreateRange("B3", "F3");

// Dê um nome ao intervalo.
range2.Name = "SecondRange";
```

Agora temos outro intervalo nomeado "SecondRange" disponível para uso.

## Etapa 9: Copiando o primeiro intervalo para o segundo intervalo

Vamos demonstrar como usar nosso segundo intervalo copiando dados do primeiro intervalo.

```csharp
// Copie o primeiro intervalo no segundo intervalo.
range2.Copy(range1);
```

Com esta etapa, duplicamos efetivamente os dados de "FirstRange" para "SecondRange".

## Etapa 10: Removendo o intervalo nomeado

Agora, o destaque do nosso tutorial: remover o intervalo nomeado. É aqui que tudo se junta.

```csharp
// Remova o intervalo nomeado anteriormente (range1) com seu conteúdo.
worksheet.Cells.ClearRange(range1.FirstRow, range1.FirstColumn, range1.FirstRow + range1.RowCount - 1, range1.FirstColumn + range1.ColumnCount - 1);
```

Esta linha limpa o conteúdo do intervalo que queremos remover, garantindo que não deixamos nenhum rastro!

## Etapa 11: Excluir o intervalo nomeado da planilha

Uma etapa final importante é remover o intervalo nomeado da coleção de nomes da planilha.

```csharp
worksheets.Names.RemoveAt(0);
```

Isso removerá efetivamente o intervalo nomeado “FirstRange” da pasta de trabalho.

## Etapa 12: Salvando a pasta de trabalho

Por último, mas não menos importante, vamos salvar nosso trabalho. 

```csharp
// Salve o arquivo Excel.
workbook.Save(outputDir + "outputRemoveNamedRange.xlsx");
```

Este comando salva sua pasta de trabalho com as alterações que fizemos — é aqui que todo o seu trabalho duro é preservado!

## Etapa 13: Confirmando a execução bem-sucedida

Para finalizar, você pode querer enviar uma mensagem de sucesso para o console.

```csharp
Console.WriteLine("RemoveNamedRange executed successfully.");
```

Isso notifica você de que toda a operação foi concluída sem problemas!

## Conclusão

Seguindo este guia, você aprendeu a manipular intervalos nomeados no Excel usando o Aspose.Cells para .NET. Você criou intervalos, preencheu-os com dados, copiou seus conteúdos e, por fim, os removeu, garantindo que seu arquivo do Excel permanecesse organizado e limpo. O Excel, assim como um café movimentado, prospera na organização. Então, se você está gerenciando dados para um relatório ou aprimorando sua planilha de orçamento pessoal, dominar intervalos nomeados pode ajudar a elaborar algumas soluções eficientes. 

## Perguntas frequentes

### O que é Aspose.Cells?
Aspose.Cells é uma biblioteca .NET projetada para manipular arquivos do Excel programaticamente.

### Posso remover vários intervalos nomeados de uma só vez?
Sim, você pode percorrer a coleção de intervalos nomeados e removê-los conforme necessário.

### Existe uma versão de teste disponível?
 Sim, você pode baixar uma versão de avaliação gratuita do Aspose.Cells[aqui](https://releases.aspose.com/).

### Quais linguagens de programação o Aspose.Cells suporta?
Ele oferece suporte principalmente a linguagens .NET, como C# e VB.NET, entre outras.

### Onde posso buscar suporte se tiver problemas?
 Você pode visitar o[Fórum de suporte Aspose](https://forum.aspose.com/c/cells/9) para obter ajuda com quaisquer dúvidas.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
