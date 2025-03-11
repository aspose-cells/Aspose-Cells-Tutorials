---
title: Atualizar item de fórmula do Power Query na pasta de trabalho
linktitle: Atualizar item de fórmula do Power Query na pasta de trabalho
second_title: API de processamento do Aspose.Cells .NET Excel
description: Aprenda como atualizar fórmulas do Power Query no Excel com o Aspose.Cells para .NET neste guia passo a passo abrangente.
weight: 27
url: /pt/net/workbook-operations/update-power-query-formula-item/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Atualizar item de fórmula do Power Query na pasta de trabalho

## Introdução
Entender como gerenciar dados de forma eficiente usando o Power Query no Excel é essencial para qualquer analista de dados ou entusiasta do Excel. Se você já precisou atualizar os itens de fórmula em sua pasta de trabalho do Power Query, você está no lugar certo. Este guia foi criado para ajudar você a aprender como usar o Aspose.Cells para .NET para atualizar perfeitamente as fórmulas do Power Query em uma pasta de trabalho do Excel. Com algumas etapas simples, você poderá manipular e otimizar seus dados, garantindo que suas pastas de trabalho permaneçam dinâmicas e centralizadas.
## Pré-requisitos
Antes de começar a analisar o código de exemplo e as etapas, vamos ver o que você precisa:
1. Noções básicas de C# e .NET: A familiaridade com conceitos de programação em C# será benéfica, pois escreveremos algum código.
2.  Instalar Aspose.Cells para .NET: Você precisa ter a biblioteca Aspose.Cells integrada ao seu projeto .NET. Você pode baixá-la[aqui](https://releases.aspose.com/cells/net/).
3. Um arquivo Excel pronto para modificação: certifique-se de ter um arquivo Excel que contenha uma Power Query que você deseja atualizar. Você precisa ter uma pasta de trabalho de exemplo como`SamplePowerQueryFormula.xlsx` à sua disposição.
## Pacotes de importação
Para começar, certifique-se de ter os seguintes namespaces incluídos no seu arquivo C#:
```csharp
using Aspose.Cells.DigitalSignatures;
using Aspose.Cells.QueryTables;
using System;
using System.IO;
```
Isso permitirá que você acesse as funcionalidades fornecidas pela biblioteca Aspose.Cells, principalmente para trabalhar com pastas de trabalho e dados do Power Query.
## Etapa 1: configure seus diretórios de trabalho
Primeiramente, você precisa definir onde seus arquivos de origem e de saída estão localizados. 
```csharp
string SourceDir = "Your Document Directory";
string outputDir = "Your Document Directory";
```
 Nesta etapa, você especifica os caminhos do diretório. Substituir`"Your Document Directory"` com o caminho real onde seus arquivos Excel estão salvos. Isso informa ao programa onde procurar seu arquivo de origem e onde salvar o atualizado.
## Etapa 2: Carregue a pasta de trabalho
Agora que você definiu seus diretórios de trabalho, o próximo passo é carregar seu arquivo Excel no programa.
```csharp
Workbook workbook = new Workbook(SourceDir + "SamplePowerQueryFormula.xlsx");
```
 Aqui, você cria um`Workbook` objeto que carrega o arquivo Excel especificado. O`Workbook` classe faz parte da biblioteca Aspose.Cells e é essencial para qualquer operação que você realizar naquele arquivo Excel.
## Etapa 3: acesse os dados do Power Query
Depois que a pasta de trabalho for carregada, é hora de acessar as fórmulas do Power Query armazenadas nela.
```csharp
DataMashup mashupData = workbook.DataMashup;
```
 Nessa linha, o`DataMashup` propriedade ajuda a acessar as estruturas de dados do Power Query dentro da pasta de trabalho. Esta propriedade lhe dá a capacidade de interagir com vários aspectos dos dados do Power Query contidos no seu arquivo Excel.
## Etapa 4: percorrer as fórmulas do Power Query
Com os dados do Power Query acessíveis, o próximo passo é iterar por cada uma das fórmulas presentes.
```csharp
foreach (PowerQueryFormula formula in mashupData.PowerQueryFormulas)
{
    foreach (PowerQueryFormulaItem item in formula.PowerQueryFormulaItems)
    {
        if (item.Name == "Source")
        {
            item.Value = "Excel.Workbook(File.Contents(\"" + SourceDir + "SamplePowerQueryFormulaSource.xlsx\"), null, true)";
        }
    }
}
```
 É aqui que a mágica acontece. Nós fazemos um loop por cada`PowerQueryFormula` e então através de cada um`PowerQueryFormulaItem` . O`if` A instrução procura o item de fórmula chamado "Source” e atualiza seu valor para ser o caminho do arquivo de origem ao qual você deseja que o Power Query faça referência. Isso permite que você altere dinamicamente de qual arquivo o Power Query extrai dados.
## Etapa 5: Salve a pasta de trabalho atualizada
Depois de atualizar os itens de fórmula necessários, a etapa final é salvar a pasta de trabalho.
```csharp
workbook.Save(outputDir + "SamplePowerQueryFormula_out.xlsx");
```
Esta linha salva a pasta de trabalho modificada em um novo arquivo, preservando o original e permitindo que você trabalhe com a versão atualizada.
## Etapa 6: Mensagem de confirmação
Por fim, é uma boa prática verificar se seu código foi executado corretamente.
```csharp
Console.WriteLine("UpdatePowerQueryFormulaItem executed successfully.");
```
Esta mensagem simples confirmará no console que sua operação foi bem-sucedida, proporcionando um final tranquilo ao processo.
## Conclusão
E aí está! Atualizar itens de fórmula do Power Query no Excel usando o Aspose.Cells para .NET pode ser feito em apenas algumas etapas simples. Seguindo este guia, você pode gerenciar com eficiência suas conexões de dados do Excel e manter suas pastas de trabalho funcionando sem problemas. Seja você um profissional experiente ou apenas começando na manipulação de dados, o Aspose.Cells fornece uma maneira poderosa de automatizar e aprimorar os fluxos de trabalho do Excel. 
## Perguntas frequentes
### Posso usar o Aspose.Cells com qualquer versão do .NET?
O Aspose.Cells é compatível com diversas versões do .NET, incluindo .NET Framework e .NET Core.
### O Aspose.Cells é gratuito?
 O Aspose.Cells oferece um teste gratuito, mas para uso contínuo, é necessária uma licença. Você pode obter uma licença temporária[aqui](https://purchase.aspose.com/temporary-license/).
### se meu arquivo Excel existente não tiver o Power Query?
O processo descrito se concentra na atualização de itens do Power Query, portanto, se seu arquivo não os tiver, você precisará incorporar o Power Queries primeiro.
### Onde posso encontrar mais informações sobre o Aspose.Cells?
 Verifique a documentação para obter orientação e exemplos abrangentes. Visite o[documentação](https://reference.aspose.com/cells/net/).
### Como posso relatar bugs ou problemas com o Aspose.Cells?
Você pode entrar em contato com o fórum de suporte deles para obter assistência sobre quaisquer problemas que encontrar.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
