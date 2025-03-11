---
title: Criar gráfico de linhas
linktitle: Criar gráfico de linhas
second_title: API de processamento do Aspose.Cells .NET Excel
description: Crie gráficos de linha impressionantes usando Aspose.Cells para .NET. Siga nosso guia passo a passo para visualizar seus dados de forma eficaz.
weight: 11
url: /pt/net/manipulating-chart-types/create-line-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar gráfico de linhas

## Introdução

Você está pronto para visualizar seus dados com clareza impressionante? Gráficos de linha são uma maneira fantástica de exibir tendências ao longo do tempo ou a relação entre duas variáveis. Quer você esteja gerenciando dados para um projeto empresarial ou analisando métricas pessoais, a capacidade de criar gráficos de linha programaticamente pode economizar seu tempo e permitir maior flexibilidade. Neste guia, nós o guiaremos por cada etapa da criação de um gráfico de linha usando o Aspose.Cells para .NET. Pronto para mergulhar? Vamos começar!

## Pré-requisitos

Antes de começarmos a criar um gráfico de linhas, vamos garantir que você esteja preparado para acompanhar:

1. Visual Studio: certifique-se de ter o Visual Studio instalado em sua máquina, pois é um dos IDEs mais populares para desenvolvimento .NET.
2.  Biblioteca Aspose.Cells para .NET: Você precisará da biblioteca Aspose.Cells, que pode ser baixada em[aqui](https://releases.aspose.com/cells/net/).
3. Conhecimento básico de C#: A familiaridade com a linguagem de programação C# ajudará você a entender melhor os exemplos e trechos de código.
4. .NET Framework ou .NET Core: uma configuração básica de qualquer framework, pois esta será a base para nossos aplicativos.

Depois de resolver esses pré-requisitos, você estará pronto para criar alguns gráficos!

## Pacotes de importação

Agora que configuramos nosso ambiente, precisamos importar os pacotes necessários em nosso código C#. Assim como você reúne suas ferramentas antes de começar um projeto, importar pacotes é essencial para garantir que você tenha tudo o que precisa.

Veja como fazer:

```csharp
using System;
using System.IO;

using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
using Aspose.Cells.Charts;
```

 Esta linha importa o`Aspose.Cells` namespace, que contém todas as classes e métodos que usaremos para criar nosso gráfico de linhas.

Agora, vamos dividir todo o processo em etapas simples e digeríveis. Cada etapa guiará você pelo fluxo lógico de criação de um gráfico de linhas usando Aspose.Cells for .NET.

## Etapa 1: Configurar o diretório de saída

O primeiro passo é definir onde você quer salvar seu arquivo de saída. É como configurar seu espaço de trabalho antes de começar a colocar a mão na massa. 

```csharp
// Diretório de saída
string outputDir = "Your Output Directory";
```
 Substituir`"Your Output Directory"`com o caminho real onde você deseja salvar o arquivo Excel gerado.

## Etapa 2: Instanciar o objeto Workbook

Em seguida, precisamos criar uma nova instância de workbook. Pense no Workbook como a tela onde sua criatividade fluirá. 

```csharp
// Instanciando um objeto Workbook
Workbook workbook = new Workbook();
```
Esta linha inicializa uma nova pasta de trabalho que conterá todos os seus dados e visuais.

## Etapa 3: Acesse a planilha

Em nossa pasta de trabalho recém-criada, precisamos obter uma referência para a planilha onde inseriremos nossos dados. Se a pasta de trabalho for nossa tela, então a planilha será nossa paleta.

```csharp
// Obtendo a referência da planilha recém-adicionada passando seu índice de planilha
Worksheet worksheet = workbook.Worksheets[0];
```
 Aqui, acessamos a primeira planilha (índice`0`).

## Etapa 4: Adicionar valores de amostra às células

Agora vem a parte divertida! Vamos inserir alguns valores de amostra em nossa planilha. Esses dados servirão como base para nosso gráfico de linhas. 

```csharp
// Adicionar valores de amostra às células
worksheet.Cells["A1"].PutValue(50);
worksheet.Cells["A2"].PutValue(100);
worksheet.Cells["A3"].PutValue(150);
worksheet.Cells["B1"].PutValue(4);
worksheet.Cells["B2"].PutValue(20);
worksheet.Cells["B3"].PutValue(50);
```
Neste snippet, estamos adicionando valores às células nas colunas A e B. A coluna A representa os valores do eixo X, enquanto a coluna B representa os valores do eixo Y.

## Etapa 5: adicione um gráfico de linhas à planilha

Em seguida, vamos introduzir nosso gráfico de linhas na planilha. É aqui que seus dados realmente ganharão vida!

```csharp
// Adicionar um gráfico à planilha
int chartIndex = worksheet.Charts.Add(Aspose.Cells.Charts.ChartType.Line, 5, 0, 25, 10);
```
Aqui, adicionamos um gráfico de linhas no local especificado. Os parâmetros (5, 0, 25, 10) definem a posição e o tamanho do gráfico dentro da planilha.

## Etapa 6: Acesse a nova instância do gráfico

Depois de adicionar nosso gráfico, é hora de colocar as mãos no objeto de gráfico recém-criado. 

```csharp
// Acessando a instância do gráfico recém-adicionado
Aspose.Cells.Charts.Chart chart = worksheet.Charts[chartIndex];
```
Este código nos conecta ao gráfico para que possamos manipulá-lo posteriormente.

## Etapa 7: Adicionar SeriesCollection ao gráfico

Agora precisamos dizer ao nosso gráfico quais dados exibir. É aqui que definimos a fonte de dados para nosso gráfico de linhas adicionando uma SeriesCollection.

```csharp
// Adicionar SeriesCollection (fonte de dados do gráfico) ao gráfico que varia da célula "A1" até "B3"
chart.NSeries.Add("A1:B3", true);
```
Neste exemplo, estamos dizendo ao gráfico para usar os valores nas células A1 a B3.

## Etapa 8: Salve o arquivo Excel

O grand finale! Depois de todo o seu trabalho duro, é hora de salvar o arquivo Excel e ver seu gráfico de linhas em ação.

```csharp
// Salvando o arquivo Excel
workbook.Save(outputDir + "outputHowToCreateLineChart.xlsx");
```
 Esta linha salva sua pasta de trabalho no diretório de saída especificado com o nome`outputHowToCreateLineChart.xlsx`.

## Etapa 9: Executar e verificar

Por fim, agora você pode executar seu código e verificar se o gráfico de linhas foi criado com sucesso no seu diretório de saída! 

```csharp
Console.WriteLine("HowToCreateLineChart executed successfully.");
```
Isso exibirá uma mensagem no seu console, informando que tudo ocorreu sem problemas.

## Conclusão

Criar um gráfico de linhas usando o Aspose.Cells para .NET é uma maneira eficiente de dar vida aos seus dados. Seguindo este guia passo a passo, você pode visualizar facilmente tendências e relacionamentos em seus conjuntos de dados. Seja você um desenvolvedor experiente ou apenas começando, o Aspose.Cells fornece a flexibilidade e o poder para automatizar suas tarefas de visualização de dados. 

## Perguntas frequentes

### O que é Aspose.Cells para .NET?  
Aspose.Cells para .NET é uma biblioteca poderosa projetada para gerenciar e manipular arquivos do Excel programaticamente, permitindo que desenvolvedores criem, editem e convertam planilhas.

### O Aspose.Cells suporta gráficos?  
Sim, o Aspose.Cells oferece amplo suporte para vários tipos de gráficos, incluindo gráficos de linhas, gráficos de pizza, gráficos de barras e muito mais.

### Posso usar o Aspose.Cells gratuitamente?  
Sim, você pode baixar uma versão de teste gratuita para explorar seus recursos. Para uso a longo prazo, considere comprar uma licença.

### Existe um fórum de suporte?  
 Absolutamente! Você pode encontrar respostas e fazer perguntas no[Fórum Aspose.Cells](https://forum.aspose.com/c/cells/9).

### Como faço para comprar uma licença?  
 As licenças podem ser adquiridas facilmente através do[página de compra](https://purchase.aspose.com/buy).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
