---
"description": "Aprenda a manipular tabelas dinâmicas do Excel com o Aspose.Cells para .NET, incluindo atualizações de dados, configurações de compatibilidade e formatação de células."
"linktitle": "Especificar compatibilidade de arquivo do Excel programaticamente em .NET"
"second_title": "API de processamento do Excel Aspose.Cells .NET"
"title": "Especificar compatibilidade de arquivo do Excel programaticamente em .NET"
"url": "/pt/net/creating-and-configuring-pivot-tables/specifying-compatibility/"
"weight": 23
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Especificar compatibilidade de arquivo do Excel programaticamente em .NET

## Introdução

No mundo atual, orientado a dados, gerenciar e manipular arquivos do Excel programaticamente tornou-se essencial para muitos desenvolvedores. Se você trabalha com o Excel em .NET, o Aspose.Cells é uma biblioteca poderosa que facilita a criação, a leitura, a modificação e o salvamento de arquivos do Excel. Um recurso importante dessa biblioteca permite especificar a compatibilidade de arquivos do Excel programaticamente. Neste tutorial, exploraremos como manipular arquivos do Excel, com foco especial no gerenciamento de compatibilidade usando o Aspose.Cells para .NET. Ao final, você entenderá como definir a compatibilidade de arquivos do Excel, especialmente para tabelas dinâmicas, enquanto atualiza e gerencia dados.

## Pré-requisitos

Antes de mergulhar na fase de codificação, certifique-se de ter o seguinte:

1. Conhecimento básico de C#: Como escreveremos código em C#, a familiaridade com a linguagem ajudará você a entender melhor o tutorial.
2. Biblioteca Aspose.Cells para .NET: Você pode baixá-la do [Página de lançamentos do Aspose Cells](https://releases.aspose.com/cells/net/). Se você ainda não o fez, considere fazer um teste gratuito para explorar seus recursos primeiro.
3. Visual Studio: um IDE onde você pode escrever e testar seu código C# de forma eficaz.
4. Arquivo Excel de exemplo: Certifique-se de ter um arquivo Excel de exemplo, de preferência um que contenha uma tabela dinâmica para a demonstração. Para o nosso exemplo, usaremos `sample-pivot-table.xlsx`.

Com esses pré-requisitos em vigor, vamos começar o processo de codificação.

## Pacotes de importação

Antes de começar a escrever sua aplicação, você precisa incluir os namespaces necessários no seu código para utilizar a biblioteca Aspose.Cells de forma eficaz. Veja como fazer isso.

### Importar namespace Aspose.Cells

```csharp
using System.IO;
using System;
using Aspose.Cells;
using Aspose.Cells.Pivot;
using System.Drawing;
```

Esta linha de código garante que você possa acessar todas as classes e métodos dentro da biblioteca Aspose.Cells.

Agora, vamos detalhar o processo para garantir que tudo esteja claro e compreensível.

## Etapa 1: configure seu diretório

Antes de mais nada, configure o diretório onde seus arquivos do Excel estão localizados. É importante fornecer o caminho correto para o arquivo.

```csharp
// O caminho para o diretório de documentos.
string dataDir = "Your Document Directory";
```

Aqui, substitua `"Your Document Directory"` com o caminho real para seus arquivos do Excel. É aqui que seu arquivo de tabela dinâmica de exemplo deve estar.

## Etapa 2: Carregar o arquivo de origem do Excel

Em seguida, precisamos carregar o arquivo Excel que contém a tabela dinâmica de exemplo. 

```csharp
// Carregar arquivo Excel de origem contendo tabela dinâmica de exemplo
Workbook wb = new Workbook(dataDir + "sample-pivot-table.xlsx");
```

Nesta etapa, criamos uma instância do `Workbook` classe, que carrega o arquivo Excel especificado. 

## Etapa 3: Acesse as planilhas

Agora que a pasta de trabalho foi carregada, você precisa acessar a planilha que contém os dados da tabela dinâmica.

```csharp
// Acesse a primeira planilha que contém dados da tabela dinâmica
Worksheet dataSheet = wb.Worksheets[0];
```

Aqui, acessamos a primeira planilha onde a tabela dinâmica está localizada. Você também pode percorrer ou especificar outras planilhas com base na estrutura do Excel.

## Etapa 4: Manipular dados da célula

Em seguida, você modificará alguns valores de células na planilha. 

### Etapa 4.1: Modificar a célula A3

Vamos começar acessando a célula A3 e definindo seu valor.

```csharp
// Acesse a célula A3 e defina seus dados
Cells cells = dataSheet.Cells;
Cell cell = cells["A3"];
cell.PutValue("FooBar");
```

Este trecho de código atualiza a célula A3 com o valor “FooBar”.

### Etapa 4.2: Modificar a célula B3 com uma string longa

Agora, vamos definir uma sequência longa na célula B3, que exceda os limites de caracteres padrão do Excel.

```csharp
// Acesse a célula B3, defina seus dados
string longStr = "Very long text 1. very long text 2.... [continue your long string]";
cell = cells["B3"];
cell.PutValue(longStr);
```

Este código é importante porque define suas expectativas em relação aos limites de dados, especialmente ao trabalhar com configurações de compatibilidade no Excel.

## Etapa 5: Verifique o comprimento da célula B3

Também é essencial confirmar o comprimento da string que inserimos.

```csharp
// Imprima o comprimento da string da célula B3
Console.WriteLine("Length of original data string: " + cell.StringValue.Length);
```

Isto é apenas para verificação para mostrar quantos caracteres seu celular contém.

## Etapa 6: definir outros valores de célula

Agora vamos acessar mais células e definir alguns valores.

```csharp
// Acesse a célula C3 e defina seus dados
cell = cells["C3"];
cell.PutValue("closed");

// Acesse a célula D3 e defina seus dados
cell = cells["D3"];
cell.PutValue("2016/07/21");
```

Cada um desses trechos atualiza diversas células adicionais na planilha.

## Etapa 7: Acesse a Tabela Dinâmica

Em seguida, você acessará a segunda planilha, que consiste nos dados da tabela dinâmica.

```csharp
// Acesse a segunda planilha que contém a tabela dinâmica
Worksheet pivotSheet = wb.Worksheets[1];

// Acesse a tabela dinâmica
PivotTable pivotTable = pivotSheet.PivotTables[0];
```

Este snippet permite que você manipule a tabela dinâmica para configurações de compatibilidade.

## Etapa 8: Definir compatibilidade para Excel 2003

É crucial definir se sua tabela dinâmica é compatível com o Excel 2003 ou não. 

```csharp
// A propriedade IsExcel2003Compatible informa se a Tabela Dinâmica é compatível com o Excel 2003 ao atualizar a Tabela Dinâmica
pivotTable.IsExcel2003Compatible = true;
pivotTable.RefreshData();
pivotTable.CalculateData();
```

É aqui que começa a verdadeira transformação. Ao definir `IsExcel2003Compatible` para `true`você limita o comprimento de caracteres a 255 ao atualizar.

## Etapa 9: Verifique o comprimento após a configuração de compatibilidade

Depois de definir a compatibilidade, vamos ver como ela afeta os dados.

```csharp
// Verifique o valor da célula B5 da planilha dinâmica.
Cell b5 = pivotSheet.Cells["B5"];
Console.WriteLine("Length of cell B5 after setting IsExcel2003Compatible property to True: " + b5.StringValue.Length);
```

Você provavelmente verá uma saída que confirma o efeito de truncamento se os dados iniciais excederem 255 caracteres.

## Etapa 10: alterar a configuração de compatibilidade

Agora, vamos alterar a configuração de compatibilidade e verificar novamente.

```csharp
// Agora defina a propriedade IsExcel2003Compatible como falsa e atualize novamente
pivotTable.IsExcel2003Compatible = false;
pivotTable.RefreshData();
pivotTable.CalculateData();
```

Isso permite que seus dados reflitam seu comprimento original sem as restrições anteriores.

## Etapa 11: Verifique o comprimento novamente 

Vamos verificar se os dados agora refletem com precisão seu comprimento real.

```csharp
// Agora, ele imprimirá o comprimento original dos dados da célula. Os dados não foram truncados.
b5 = pivotSheet.Cells["B5"];
Console.WriteLine("Length of cell B5 after setting IsExcel2003Compatible property to False: " + b5.StringValue.Length);
```

Você deverá ver que a saída confirma a remoção do truncamento.

## Etapa 12: formatar as células

Para melhorar a experiência visual, você pode formatar as células. 

```csharp
// Defina a altura da linha e a largura da coluna da célula B5 e também quebre seu texto
pivotSheet.Cells.SetRowHeight(b5.Row, 100);
pivotSheet.Cells.SetColumnWidth(b5.Column, 65);
Style st = b5.GetStyle();
st.IsTextWrapped = true;
b5.SetStyle(st);
```

Essas linhas de código facilitam a leitura dos dados ajustando as dimensões das células e permitindo o ajuste de texto.

## Etapa 13: Salvar a pasta de trabalho

Por fim, salve sua pasta de trabalho com as alterações feitas.

```csharp
// Salvar pasta de trabalho em formato xlsx
wb.Save(dataDir + "SpecifyCompatibility_out.xlsx", SaveFormat.Xlsx);
```

A escolha de um formato de arquivo apropriado é crucial ao salvar arquivos do Excel. `Xlsx` O formato é amplamente utilizado e compatível com muitas versões do Excel.

## Conclusão

Parabéns! Você programou as configurações de compatibilidade de arquivos do Excel usando o Aspose.Cells para .NET. Este tutorial descreveu cada etapa, desde a configuração do seu ambiente até a alteração das configurações de compatibilidade para tabelas dinâmicas. Se você já trabalhou com dados que exigiam limitações ou compatibilidade específicas, esta é uma habilidade que você não vai querer ignorar.

## Perguntas frequentes

### O que é Aspose.Cells?  
Aspose.Cells é uma biblioteca .NET projetada para ajudar desenvolvedores a criar, manipular e converter arquivos do Excel sem problemas.

### Por que a compatibilidade do Excel é importante?  
A compatibilidade do Excel é crucial para garantir que os arquivos possam ser abertos e usados nas versões pretendidas do Excel, principalmente se eles contiverem recursos ou formatos não suportados em versões anteriores.

### Posso criar tabelas dinâmicas programadamente com Aspose.Cells?  
Sim, você pode criar e manipular Tabelas Dinâmicas programaticamente usando Aspose.Cells. A biblioteca oferece vários métodos para adicionar fontes de dados, campos e recursos associados a Tabelas Dinâmicas.

### Como posso verificar o comprimento de uma string em uma célula do Excel?  
Você pode usar o `StringValue` propriedade de um `Cell` objeto para obter o conteúdo da célula e então chamar o `.Length` propriedade para descobrir o comprimento da string.

### Posso personalizar a formatação das células além da altura e largura da linha?  
Com certeza! O Aspose.Cells permite uma formatação abrangente de células. Você pode alterar estilos de fonte, cores, bordas, formatos de números e muito mais através do `Style` aula.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}