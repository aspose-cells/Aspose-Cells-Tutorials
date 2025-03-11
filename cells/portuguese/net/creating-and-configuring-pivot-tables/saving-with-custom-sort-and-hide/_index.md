---
title: Salvando tabelas dinâmicas com classificação e ocultação personalizadas no .NET
linktitle: Salvando tabelas dinâmicas com classificação e ocultação personalizadas no .NET
second_title: API de processamento do Aspose.Cells .NET Excel
description: Aprenda como salvar tabelas dinâmicas com classificação personalizada e ocultação de linhas usando Aspose.Cells para .NET. Guia passo a passo com exemplos práticos incluídos.
weight: 26
url: /pt/net/creating-and-configuring-pivot-tables/saving-with-custom-sort-and-hide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Salvando tabelas dinâmicas com classificação e ocultação personalizadas no .NET

## Introdução
No mundo da análise de dados, as tabelas dinâmicas se destacam como uma das ferramentas mais poderosas para resumir, analisar e apresentar dados em um formato digerível. Se você está trabalhando com .NET e procurando uma maneira direta de manipular tabelas dinâmicas — especificamente, salvá-las com classificação personalizada e ocultar linhas específicas — você está no lugar certo! Hoje, vamos descompactar a técnica de salvar tabelas dinâmicas usando Aspose.Cells para .NET. Este guia o guiará por tudo, desde pré-requisitos até exemplos práticos, garantindo que você esteja equipado para lidar com tarefas semelhantes por conta própria. Então, vamos direto ao assunto!
## Pré-requisitos
Antes de mergulhar nos detalhes da codificação, certifique-se de ter os seguintes pré-requisitos em vigor:
1. Visual Studio: Idealmente, você gostaria de um IDE sólido para lidar com seus projetos .NET. O Visual Studio é uma ótima escolha.
2.  Aspose.Cells para .NET: Você precisará de acesso à biblioteca do Aspose para gerenciar arquivos Excel programaticamente. Você pode[baixe Aspose.Cells para .NET aqui](https://releases.aspose.com/cells/net/).
3. Conhecimento básico de C#: A familiaridade com conceitos básicos de programação e sintaxe em C# tornará o processo mais tranquilo.
4.  Arquivo Excel de exemplo: Usaremos um arquivo de exemplo chamado`PivotTableHideAndSortSample.xlsx`. Certifique-se de ter esse arquivo no diretório de documentos designado.
Depois que seu ambiente de desenvolvimento estiver configurado e seu arquivo de amostra pronto, estará tudo pronto!
## Pacotes de importação
Agora que temos os pré-requisitos verificados, vamos importar os pacotes necessários. No seu arquivo C#, use a seguinte diretiva para incluir Aspose.Cells:
```csharp
using System;
using Aspose.Cells.Pivot;
```
Esta diretiva permite que você acesse as classes e métodos fornecidos pela biblioteca Aspose.Cells. Certifique-se de ter adicionado Aspose.Cells.dll às referências do seu projeto.
## Etapa 1: Configurar a pasta de trabalho
Primeiro, precisamos carregar nossa pasta de trabalho. O seguinte trecho de código faz isso:
```csharp
// Diretórios para arquivos de origem e saída
string sourceDir = "Your Document Directory";
string outputDir = "Your Document Directory";
// Carregue a pasta de trabalho
Workbook workbook = new Workbook(sourceDir + "PivotTableHideAndSortSample.xlsx");
```
 Nesta etapa, você define os diretórios onde seus arquivos de origem e saída são armazenados. O`Workbook` construtor carregará seu arquivo Excel existente, deixando-o pronto para manipulação.
## Etapa 2: Acesse a planilha e a tabela dinâmica
Agora, vamos acessar a planilha específica dentro da pasta de trabalho e selecionar a tabela dinâmica com a qual queremos trabalhar.
```csharp
// Acesse a primeira planilha
Worksheet worksheet = workbook.Worksheets[0];
// Acesse a primeira tabela dinâmica na planilha
var pivotTable = worksheet.PivotTables[0];
```
 Neste trecho,`Worksheets[0]` seleciona a primeira planilha do seu documento Excel e`PivotTables[0]` recupera a primeira tabela dinâmica. Isso permite que você direcione a tabela dinâmica exata que deseja modificar.
## Etapa 3: Classificar linhas da tabela dinâmica
Em seguida, implementaremos a classificação personalizada para organizar nossos dados. Especificamente, classificaremos as pontuações em ordem decrescente.
```csharp
// Classificando o campo da primeira linha em ordem decrescente
PivotField field = pivotTable.RowFields[0];
field.IsAutoSort = true;
field.IsAscendSort = false;  // falso para descendente
field.AutoSortField = 0;     // Classificação com base na primeira coluna
```
 Aqui, estamos usando o`PivotField` para definir os parâmetros de classificação. Isso diz à tabela dinâmica para classificar o campo de linha especificado com base na primeira coluna, e para fazer isso em ordem decrescente. 
## Etapa 4: Atualizar e calcular dados
Depois de aplicar a classificação, é crucial atualizar os dados da tabela dinâmica para garantir que ela reflita nossas modificações.
```csharp
// Atualizar e calcular os dados da tabela dinâmica
pivotTable.RefreshData();
pivotTable.CalculateData();
```
Esta etapa sincroniza a tabela dinâmica com seus dados atuais, aplicando quaisquer alterações de classificação ou filtragem que você tenha feito até agora. Pense nisso como clicar em "atualizar" para ver a nova organização dos seus dados!
## Etapa 5: Ocultar linhas específicas
Agora, vamos ocultar as linhas que contêm pontuações abaixo de um certo limite — digamos, menos de 60. É aqui que podemos filtrar os dados ainda mais.
```csharp
// Especifique a linha inicial para verificar as pontuações
int currentRow = 3;
int rowsUsed = pivotTable.DataBodyRange.EndRow;
// Ocultar linhas com pontuação menor que 60
while (currentRow < rowsUsed)
{
    Cell cell = worksheet.Cells[currentRow, 1]; // Supondo que a pontuação esteja na primeira coluna
    double score = Convert.ToDouble(cell.Value);
    if (score < 60)
    {
        worksheet.Cells.HideRow(currentRow);  // Ocultar a linha se a pontuação for inferior a 60
    }
    currentRow++;
}
```
Neste loop, verificamos cada linha dentro do intervalo do corpo de dados da tabela dinâmica. Se uma pontuação estiver abaixo de 60, ocultamos essa linha. É como limpar seu espaço de trabalho — removendo a desordem que não ajuda você a ver o quadro geral!
## Etapa 6: atualização final e salvar a pasta de trabalho
Antes de encerrar, vamos fazer uma última atualização da tabela dinâmica para garantir que a ocultação de linhas tenha efeito e, em seguida, salvar a pasta de trabalho em um novo arquivo.
```csharp
// Atualize e calcule os dados uma última vez
pivotTable.RefreshData();
pivotTable.CalculateData();
// Salvar a pasta de trabalho modificada
workbook.Save(outputDir + "PivotTableHideAndSort_out.xlsx");
```
Essa atualização final garante que tudo esteja atualizado e, ao salvar a pasta de trabalho, você cria um novo arquivo que reflete todas as alterações que fizemos.
## Etapa 7: Confirme o sucesso
Por fim, imprimiremos uma mensagem de sucesso para confirmar que nossa operação foi concluída sem problemas.
```csharp
Console.WriteLine("PivotTableSortAndHide executed successfully.");
```
Esta linha tem o duplo propósito de confirmar o sucesso e fornecer feedback no seu console, tornando o processo um pouco mais interativo e fácil de usar.
## Conclusão
aí está! Você aprendeu com sucesso como salvar tabelas dinâmicas com funcionalidades personalizadas de classificação e ocultação usando o Aspose.Cells para .NET. Desde carregar sua pasta de trabalho até classificar dados e ocultar detalhes desnecessários, essas etapas fornecem uma abordagem estruturada para gerenciar suas tabelas dinâmicas programaticamente. Quer você esteja analisando dados de vendas, rastreando o desempenho da equipe ou simplesmente organizando informações, dominar essas habilidades com o Aspose.Cells pode economizar um tempo valioso e melhorar seu fluxo de trabalho de análise de dados.
## Perguntas frequentes
### O que é Aspose.Cells para .NET?
Aspose.Cells for .NET é uma biblioteca .NET que permite aos desenvolvedores criar, manipular e converter planilhas do Excel sem depender do Microsoft Excel. É perfeito para automatizar tarefas em documentos do Excel.
### Posso usar o Aspose.Cells sem o Microsoft Office instalado?
Claro! Aspose.Cells é uma biblioteca autônoma, então você não precisa ter o Microsoft Office instalado no seu sistema para trabalhar com arquivos do Excel.
### Como posso obter uma licença temporária para o Aspose.Cells?
 Você pode solicitar uma licença temporária através do[página de licença temporária](https://purchase.aspose.com/temporary-license/).
### Onde posso encontrar suporte para problemas do Aspose.Cells?
 Para quaisquer dúvidas ou problemas, você pode visitar o[Fórum Aspose](https://forum.aspose.com/c/cells/9), onde você encontrará suporte da comunidade e da equipe da Aspose.
### Existe um teste gratuito disponível para o Aspose.Cells?
 Sim! Você pode baixar uma versão de teste gratuita do Aspose.Cells para testar seus recursos antes de fazer uma compra. Visite o[página de teste grátis](https://releases.aspose.com/) para começar.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
