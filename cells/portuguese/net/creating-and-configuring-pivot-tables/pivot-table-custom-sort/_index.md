---
title: Programação personalizada de classificação de tabela dinâmica em .NET
linktitle: Programação personalizada de classificação de tabela dinâmica em .NET
second_title: API de processamento do Aspose.Cells .NET Excel
description: Aprenda a programar tabelas dinâmicas no .NET usando Aspose.Cells. Um guia passo a passo que abrange instalação, configuração, classificação e salvamento de resultados como arquivos Excel e PDF.
weight: 29
url: /pt/net/creating-and-configuring-pivot-tables/pivot-table-custom-sort/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Programação personalizada de classificação de tabela dinâmica em .NET

## Introdução
Quando se trata de trabalhar com o Excel em um ambiente .NET, uma biblioteca se destaca entre as demais: Aspose.Cells. Agora, você não adora quando uma ferramenta permite que você manipule planilhas programaticamente? É exatamente isso que o Aspose.Cells faz! No tutorial de hoje, vamos mergulhar fundo no mundo das Tabelas Dinâmicas e mostrar como implementar a classificação personalizada programaticamente usando esta biblioteca versátil.
## Pré-requisitos
Antes de arregaçarmos as mangas e mergulharmos no código, certifique-se de ter algumas coisas em mãos:
1. Visual Studio: Você precisará de uma versão funcional do Visual Studio. É o playground onde toda a mágica acontece.
2. .NET Framework: Familiaridade com programação .NET é essencial. Seja você um entusiasta do .NET Core ou do .NET Framework, você está pronto para começar.
3.  Biblioteca Aspose.Cells: Você precisa instalar a biblioteca Aspose.Cells. Você pode obtê-la em[Link para download](https://releases.aspose.com/cells/net/) e adicione-o ao seu projeto.
4. Noções básicas sobre tabelas dinâmicas: embora você não precise ser um especialista, um pouco de conhecimento sobre como as tabelas dinâmicas funcionam será benéfico à medida que avançamos neste tutorial.
5.  Arquivo Excel de exemplo: Tenha um arquivo Excel de exemplo chamado`SamplePivotSort.xlsx` pronto em seu diretório de trabalho para testes.
## Pacotes de importação
Depois que você tiver todos os seus pré-requisitos classificados, o primeiro passo é importar os pacotes necessários. Para fazer isso, inclua as seguintes linhas no topo do seu código:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells;
using Aspose.Cells.Pivot;
```
Este pacote fornece todas as funcionalidades necessárias para manipular arquivos do Excel usando o Aspose.Cells.

Certo, vamos para a parte divertida! Vamos dividir o processo de criação de uma Tabela Dinâmica e aplicar classificação personalizada em etapas gerenciáveis.
## Etapa 1: Configurar a pasta de trabalho
Para começar, precisamos configurar nossa pasta de trabalho. Veja como fazer isso:
```csharp
string sourceDir = "Your Document Directory";
string outputDir = "Your Document Directory";
Workbook wb = new Workbook(sourceDir + "SamplePivotSort.xlsx");
```
 Nesta etapa, inicializamos um novo`Workbook` instância com o caminho para nosso arquivo Excel. Isso atua como a tela onde nossa Tabela Dinâmica ganhará vida.
## Etapa 2: Acesse a planilha
Em seguida, precisamos acessar a planilha onde adicionaremos nossa Tabela Dinâmica.
```csharp
Worksheet sheet = wb.Worksheets[0];
PivotTableCollection pivotTables = sheet.PivotTables;
```
 Aqui, pegamos a primeira planilha em nossa pasta de trabalho e chamamos o`PivotTableCollection`. Esta coleção nos permite gerenciar todas as Tabelas Dinâmicas nesta planilha.
## Etapa 3: Crie sua primeira tabela dinâmica
Agora é hora de criar nossa Tabela Dinâmica.
```csharp
int index = pivotTables.Add("=Sheet1!A1:C10", "E3", "PivotTable1");
PivotTable pivotTable = pivotTables[index];
```
Adicionamos uma nova Tabela Dinâmica à nossa planilha, especificando o intervalo de dados e sua localização. "E3" indica onde queremos que nossa Tabela Dinâmica comece. Em seguida, referenciamos essa nova Tabela Dinâmica usando seu índice.
## Etapa 4: Configurar as configurações da tabela dinâmica
Vamos configurar nossa Tabela Dinâmica! Isso significa controlar aspectos como totais gerais e arranjos de campos.
```csharp
pivotTable.RowGrand = false;
pivotTable.ColumnGrand = false;
pivotTable.AddFieldToArea(PivotFieldType.Row,1);
PivotField rowField = pivotTable.RowFields[0];
rowField.IsAutoSort = true;
rowField.IsAscendSort = true;
```
Garantimos que os totais gerais para linhas e colunas não sejam exibidos, o que pode tornar os dados mais limpos. Então, estamos adicionando o primeiro campo à área de linha, permitindo a classificação automática e uma classificação ascendente.
## Etapa 5: Adicionar campos de coluna e dados
Depois que as linhas estiverem definidas, vamos adicionar a coluna e os campos de dados.
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Column,0);
PivotField colField = pivotTable.ColumnFields[0];
colField.NumberFormat = "dd/mm/yyyy";
colField.IsAutoSort = true;
colField.IsAscendSort = true;
```
Adicionamos o segundo campo como uma coluna e o formatamos como uma data. Novamente, habilitamos a classificação automática e a ordem crescente para manter as coisas organizadas. Por fim, precisamos adicionar o terceiro campo à nossa área de dados:
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Data,2);
```
## Etapa 6: Atualizar e calcular a tabela dinâmica
Depois de adicionar todos os campos necessários, vamos garantir que nossa Tabela Dinâmica esteja atualizada e pronta.
```csharp
pivotTable.RefreshData();
pivotTable.CalculateData();
```
Esses métodos atualizam os dados e os recalculam, garantindo que tudo esteja atualizado e exibido corretamente em nossa Tabela Dinâmica.
## Etapa 7: Classificação personalizada com base nos valores do campo de linha
Vamos adicionar um pouco de estilo classificando a Tabela Dinâmica com base em valores específicos, como "Frutos do mar".
```csharp
index = pivotTables.Add("=Sheet1!A1:C10", "E10", "PivotTable2");
pivotTable = pivotTables[index];
```
Estamos repetindo o processo criando outra Tabela Dinâmica e configurando-a similarmente à primeira. Agora podemos personalizá-la ainda mais:
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Row,1);
rowField = pivotTable.RowFields[0];
rowField.IsAutoSort = true;
rowField.IsAscendSort = true;
```
## Etapa 8: Personalização adicional de classificaçãoVamos tentar outro método de classificação com base em uma data específica:
```csharp
// Adicionando outra Tabela Dinâmica para classificar por data
index = pivotTables.Add("=Sheet1!A1:C10", "E18", "PivotTable3");
pivotTable = pivotTables[index];
// Repita as configurações de linha e coluna semelhantes às etapas anteriores
```
Basta repetir o mesmo processo, criando uma terceira Tabela Dinâmica com critérios de classificação adaptados às suas necessidades.
## Etapa 9: Salve a pasta de trabalhoTempo para salvar todo o trabalho duro que fizemos!
```csharp
wb.Save(outputDir + "out.xlsx");
PdfSaveOptions options = new PdfSaveOptions();
options.OnePagePerSheet = true;
wb.Save(outputDir + "out.pdf", options);
```
 Aqui, você salva a pasta de trabalho como um arquivo Excel e um PDF. O`PdfSaveOptions` permite melhor formatação, garantindo que cada folha apareça em uma página separada quando convertida.
## Etapa 10: Finalize. Conclua tudo informando ao usuário que está tudo bem.
```csharp
Console.WriteLine("PivotTableCustomSort executed successfully.");
```
## Conclusão
Agora, você aprendeu como aproveitar o poder do Aspose.Cells para criar e personalizar Tabelas Dinâmicas em seus aplicativos .NET. Da configuração inicial à classificação personalizada, cada etapa se combina para oferecer uma experiência perfeita. Quer você precise apresentar dados de vendas anuais ou rastrear estatísticas de estoque, essas habilidades serão úteis para você!
## Perguntas frequentes
### O que é uma tabela dinâmica?
Uma Tabela Dinâmica é uma ferramenta de processamento de dados no Excel que permite resumir e analisar dados, fornecendo uma maneira flexível de extrair insights facilmente.
### Como instalo o Aspose.Cells?
 Você pode instalá-lo via NuGet no Visual Studio ou baixá-lo diretamente do[Link para download](https://releases.aspose.com/cells/net/).
### Existe uma versão de teste do Aspose.Cells?
 Sim! Você pode experimentar gratuitamente visitando o[Link de teste gratuito](https://releases.aspose.com/).
### Posso classificar vários campos em uma Tabela Dinâmica?
Absolutamente! Você pode adicionar e classificar vários campos com base em seus requisitos.
### Onde posso encontrar suporte para o Aspose.Cells?
 A comunidade é bastante ativa e você pode fazer perguntas no fórum deles[aqui](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
