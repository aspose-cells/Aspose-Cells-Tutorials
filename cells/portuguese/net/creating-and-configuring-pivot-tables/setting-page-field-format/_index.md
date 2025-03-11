---
title: Configurando o formato do campo de página programaticamente no .NET
linktitle: Configurando o formato do campo de página programaticamente no .NET
second_title: API de processamento do Aspose.Cells .NET Excel
description: Aprenda como definir formatos de campo de página em PivotTables programaticamente usando Aspose.Cells para .NET. Siga nosso tutorial passo a passo para gerenciamento de dados perfeito.
weight: 21
url: /pt/net/creating-and-configuring-pivot-tables/setting-page-field-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Configurando o formato do campo de página programaticamente no .NET

## Introdução
Criar e manipular arquivos do Excel por meio de código pode ser bastante poderoso, especialmente quando você precisa analisar grandes conjuntos de dados. Uma das ferramentas fantásticas em seu arsenal é o Aspose.Cells para .NET, que permite que você interaja programaticamente com arquivos do Excel e crie estruturas de relatórios complexas. Neste tutorial, vamos nos aprofundar em como você pode configurar formatos de campo de página em uma Tabela Dinâmica usando esta biblioteca poderosa. Seja você um desenvolvedor experiente ou um iniciante, ao final deste guia, você terá uma forte compreensão de como operar com Tabelas Dinâmicas e suas várias configurações no .NET.
## Pré-requisitos
Antes de mergulharmos de cabeça na codificação, vamos garantir que você tenha tudo configurado corretamente. Você precisará do seguinte:
- Visual Studio: um ambiente de trabalho onde você pode escrever e executar seu código .NET.
-  Aspose.Cells: Você pode baixar a biblioteca[aqui](https://releases.aspose.com/cells/net/).
- Conhecimento básico de C#: A familiaridade com a programação em C# ajudará você a entender melhor os trechos de código.
-  Arquivo Excel: Tenha um arquivo Excel pronto (como`Book1.xls`) contendo dados adequados para criação de Tabela Dinâmica. 
 Se você ainda não fez isso, faça uma avaliação gratuita do Aspose.Cells[aqui](https://releases.aspose.com/).
## Pacotes de importação
Para começar, você precisará importar os pacotes certos no seu projeto. Comece adicionando referências à biblioteca Aspose.Cells no seu projeto C#. Veja como fazer isso:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
using Aspose.Cells.Pivot;
```
Isso extrairá todas as classes e métodos necessários para manipular arquivos do Excel usando Aspose.Cells.
## Etapa 1: configure seu espaço de trabalho
Comece definindo seu diretório de trabalho onde seus arquivos Excel serão armazenados. Por exemplo, você pode declarar uma variável como esta:
```csharp
string dataDir = "Your Document Directory";
```
## Carregando a pasta de trabalho
Em seguida, precisamos carregar nosso modelo Excel. Este é um passo essencial porque estabelece o contexto para nossas operações:
```csharp
Workbook workbook = new Workbook(dataDir + "Book1.xls");
```
Esta linha carrega a pasta de trabalho existente do diretório especificado.
## Etapa 2: Acesse a planilha
Depois que sua pasta de trabalho for carregada, é hora de acessar a planilha que contém a Tabela Dinâmica ou os dados que você deseja analisar. Veja como você pode fazer isso:
```csharp
Worksheet worksheet = workbook.Worksheets[0];
```
Isso pega a primeira planilha da pasta de trabalho carregada. Você pode modificar facilmente o índice se estiver trabalhando com várias planilhas.
## Etapa 3: Acessando a Tabela Dinâmica
 Continuando, vamos acessar a Tabela Dinâmica em nossa planilha escolhida. Se você estiver usando uma única Tabela Dinâmica, você pode definir seu índice para`0`:
```csharp
int pivotindex = 0;
// Acessando a Tabela Dinâmica
PivotTable pivotTable = worksheet.PivotTables[pivotindex];
```
Este trecho de código seleciona a primeira Tabela Dinâmica na planilha. 
## Etapa 4: Configurando a Tabela Dinâmica
Agora vem a parte emocionante! Vamos configurar a PivotTable para mostrar totais gerais para as linhas:
```csharp
pivotTable.RowGrand = true;
```
Esta linha garante que seu relatório exibirá totais gerais, o que pode ser um resumo útil para análise de dados.
## Etapa 5: Acessar e configurar campos de linha
Em seguida, precisamos acessar os campos de linha da Tabela Dinâmica:
```csharp
Aspose.Cells.Pivot.PivotFieldCollection pivotFields = pivotTable.RowFields;
```
Esta coleção nos permite manipular os campos conforme necessário.
## Configurar o campo da primeira linha
Quer definir tipos específicos de subtotal? Vamos acessar o primeiro campo em nossa coleção e configurá-lo:
```csharp
Aspose.Cells.Pivot.PivotField pivotField = pivotFields[0];
// Definindo subtotais.
pivotField.SetSubtotals(Aspose.Cells.Pivot.PivotFieldSubtotalType.Sum, true);
pivotField.SetSubtotals(Aspose.Cells.Pivot.PivotFieldSubtotalType.Count, true);
```
 Ao habilitar`Sum` e`Count` subtotais, podemos resumir rapidamente os dados em nosso relatório.
## Etapa 6: Definindo opções de classificação automática
Em seguida, vamos colocar alguma classificação inteligente em prática. Dessa forma, sua Tabela Dinâmica organizará os dados em uma ordem significativa:
```csharp
// Configurando opções de classificação automática.
pivotField.IsAutoSort = true;
pivotField.IsAscendSort = true;
pivotField.AutoSortField = -5; // Usando um campo de classificação predefinido.
```
Este trecho de código permite a classificação automática e especifica a ordem crescente. 
## Etapa 7: Definindo opções de apresentação automática
Gostaria de filtrar seus dados ainda mais? A opção AutoShow é útil para mostrar pontos de dados específicos sob condições definidas:
```csharp
// Configurando opções de autoShow.
pivotField.IsAutoShow = true;
pivotField.IsAscendShow = false;
pivotField.AutoShowField = 0; // Especifique o campo para exibição automática.
```
Isso garante que sua Tabela Dinâmica exiba apenas dados relevantes, aumentando a clareza e o foco.
## Etapa 8: salvando seu trabalho
Depois de todas essas configurações, você não vai querer perder seu trabalho! Salve a pasta de trabalho modificada assim:
```csharp
workbook.Save(dataDir + "output.xls");
```
Agora, você pode encontrar o arquivo Excel recém-criado no seu diretório de documentos.
## Conclusão
E aí está! Nós percorremos uma abordagem abrangente e prática para definir formatos de campo de página programaticamente em uma Tabela Dinâmica usando Aspose.Cells para .NET. Com as etapas simples fornecidas, você deve se sentir confiante para modificar seus dados do Excel para atender às suas necessidades de relatórios. É incrível o que você pode conseguir quando combina o poder do C# com o Aspose.Cells.
## Perguntas frequentes
### O que é Aspose.Cells?
Aspose.Cells é uma biblioteca .NET que permite aos desenvolvedores criar, manipular e converter arquivos do Excel programaticamente.
### Como instalo o Aspose.Cells?
 Você pode baixá-lo diretamente do[Site Aspose](https://releases.aspose.com/cells/net/).
### Posso usar o Aspose.Cells sem instalar o Excel?
Sim, o Aspose.Cells é uma biblioteca autônoma que não requer a instalação do Microsoft Excel.
### Onde posso encontrar suporte detalhado?
 Você pode acessar suporte detalhado e fóruns em[Suporte Aspose](https://forum.aspose.com/c/cells/9).
### Como posso obter uma licença temporária?
 Você pode adquirir uma licença temporária em[aqui](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
