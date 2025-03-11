---
title: Encontre o máximo de linhas e colunas suportadas pelos formatos XLS e XLSX
linktitle: Encontre o máximo de linhas e colunas suportadas pelos formatos XLS e XLSX
second_title: API de processamento do Aspose.Cells .NET Excel
description: Descubra o máximo de linhas e colunas suportadas pelos formatos XLS e XLSX usando o Aspose.Cells para .NET. Maximize seu gerenciamento de dados do Excel com este tutorial abrangente.
weight: 11
url: /pt/net/workbook-settings/find-maximum-supported-rows-columns/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Encontre o máximo de linhas e colunas suportadas pelos formatos XLS e XLSX

## Introdução
No mundo do Excel, gerenciar grandes conjuntos de dados pode ser uma tarefa assustadora, especialmente quando se trata de lidar com o número máximo de linhas e colunas suportadas por diferentes formatos de arquivo. Este tutorial o guiará pelo processo de encontrar o máximo de linhas e colunas suportadas pelos formatos XLS e XLSX usando a biblioteca Aspose.Cells for .NET. Ao final deste artigo, você terá uma compreensão abrangente de como utilizar esta ferramenta poderosa para lidar com suas tarefas relacionadas ao Excel de forma eficiente.
## Pré-requisitos
Antes de começarmos o tutorial, certifique-se de ter os seguintes pré-requisitos:
1. [Estrutura .NET](https://dotnet.microsoft.com/en-us/download) ou[.NET Núcleo](https://dotnet.microsoft.com/en-us/download) instalado no seu sistema.
2. [Aspose.Cells para .NET](https://releases.aspose.com/cells/net/) biblioteca baixada e referenciada em seu projeto.
 Se ainda não o fez, você pode baixar a biblioteca Aspose.Cells for .NET do[site](https://releases.aspose.com/cells/net/) ou instale-o via[NuGet](https://www.nuget.org/packages/Aspose.Cells/).
## Pacotes de importação
Para começar, você precisará importar os pacotes necessários da biblioteca Aspose.Cells for .NET. Adicione as seguintes instruções using no topo do seu arquivo C#:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
## Etapa 1: Encontre o máximo de linhas e colunas suportadas pelo formato XLS
Vamos começar explorando o número máximo de linhas e colunas suportadas pelo formato XLS (Excel 97-2003).
```csharp
// Imprimir mensagem sobre o formato XLS.
Console.WriteLine("Maximum Rows and Columns supported by XLS format.");
// Crie uma pasta de trabalho no formato XLS.
Workbook wb = new Workbook(FileFormatType.Excel97To2003);
// Imprima o máximo de linhas e colunas suportadas pelo formato XLS.
int maxRows = wb.Settings.MaxRow + 1;
int maxCols = wb.Settings.MaxColumn + 1;
Console.WriteLine("Maximum Rows: " + maxRows);
Console.WriteLine("Maximum Columns: " + maxCols);
Console.WriteLine();
```
Nesta etapa, nós:
1. Imprima uma mensagem para indicar que estamos trabalhando com o formato XLS.
2.  Criar um novo`Workbook` instância usando o`FileFormatType.Excel97To2003` enum, que representa o formato XLS.
3.  Recupere o máximo de linhas e colunas suportadas pelo formato XLS usando o`Workbook.Settings.MaxRow` e`Workbook.Settings.MaxColumn`properties, respectivamente. Adicionamos 1 a esses valores para obter os números máximos reais de linhas e colunas (já que são baseados em zero).
4. Imprima o máximo de linhas e colunas no console.
## Etapa 2: Encontre o Máximo de Linhas e Colunas Suportadas pelo Formato XLSX
A seguir, vamos explorar o número máximo de linhas e colunas suportadas pelo formato XLSX (Excel 2007 e posterior).
```csharp
// Imprimir mensagem sobre o formato XLSX.
Console.WriteLine("Maximum Rows and Columns supported by XLSX format.");
// Crie uma pasta de trabalho no formato XLSX.
wb = new Workbook(FileFormatType.Xlsx);
// Imprima o máximo de linhas e colunas suportadas pelo formato XLSX.
maxRows = wb.Settings.MaxRow + 1;
maxCols = wb.Settings.MaxColumn + 1;
Console.WriteLine("Maximum Rows: " + maxRows);
Console.WriteLine("Maximum Columns: " + maxCols);
```
Nesta etapa, nós:
1. Imprima uma mensagem para indicar que estamos trabalhando com o formato XLSX.
2.  Criar um novo`Workbook` instância usando o`FileFormatType.Xlsx` enum, que representa o formato XLSX.
3.  Recupere o máximo de linhas e colunas suportadas pelo formato XLSX usando o`Workbook.Settings.MaxRow` e`Workbook.Settings.MaxColumn`properties, respectivamente. Adicionamos 1 a esses valores para obter os números máximos reais de linhas e colunas (já que são baseados em zero).
4. Imprima o máximo de linhas e colunas no console.
## Etapa 3: Exibir uma mensagem de sucesso
Por fim, vamos exibir uma mensagem de sucesso para indicar que o exemplo "FindMaximumRowsAndColumnsSupportedByXLSAndXLSXFormats" foi executado com sucesso.
```csharp
Console.WriteLine("FindMaximumRowsAndColumnsSupportedByXLSAndXLSXFormats executed successfully.");
```
Esta etapa simplesmente imprime uma mensagem de sucesso no console.
## Conclusão
Neste tutorial, você aprendeu como usar a biblioteca Aspose.Cells for .NET para encontrar o máximo de linhas e colunas suportadas pelos formatos de arquivo XLS e XLSX. Ao entender as limitações desses formatos, você pode planejar e gerenciar melhor seus projetos baseados no Excel, garantindo que seus dados se encaixem nos intervalos suportados.
## Perguntas frequentes
### Qual é o número máximo de linhas suportadas pelo formato XLS?
O número máximo de linhas suportadas pelo formato XLS (Excel 97-2003) é 65.536.
### Qual é o número máximo de colunas suportadas pelo formato XLS?
O número máximo de colunas suportadas pelo formato XLS (Excel 97-2003) é 256.
### Qual é o número máximo de linhas suportadas pelo formato XLSX?
O número máximo de linhas suportadas pelo formato XLSX (Excel 2007 e posterior) é 1.048.576.
### Qual é o número máximo de colunas suportadas pelo formato XLSX?
O número máximo de colunas suportadas pelo formato XLSX (Excel 2007 e posterior) é 16.384.
### Posso usar a biblioteca Aspose.Cells for .NET para trabalhar com outros formatos de arquivo do Excel?
 Sim, a biblioteca Aspose.Cells for .NET suporta uma ampla variedade de formatos de arquivo Excel, incluindo XLS, XLSX, ODS e muito mais. Você pode explorar o[documentação](https://reference.aspose.com/cells/net/) para saber mais sobre os recursos e funcionalidades disponíveis.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
