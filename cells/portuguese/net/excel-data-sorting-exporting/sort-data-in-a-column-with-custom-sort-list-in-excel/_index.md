---
title: Classificar dados em uma coluna com lista de classificação personalizada no Excel
linktitle: Classificar dados em uma coluna com lista de classificação personalizada no Excel
second_title: API de processamento do Aspose.Cells .NET Excel
description: Aprenda a classificar dados no Excel usando uma lista de classificação personalizada com o Aspose.Cells para .NET neste tutorial abrangente.
weight: 10
url: /pt/net/excel-data-sorting-exporting/sort-data-in-a-column-with-custom-sort-list-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Classificar dados em uma coluna com lista de classificação personalizada no Excel

## Introdução

Este tutorial guiará você pelo processo de configuração do seu projeto, carregamento de um arquivo Excel e classificação de dados dentro de um intervalo especificado usando uma ordem de classificação personalizada. Ao seguir este guia, você ganhará experiência prática que pode aprimorar suas habilidades de gerenciamento de dados e usabilidade da biblioteca Aspose.Cells.

## Pré-requisitos

Antes de mergulhar no tutorial, vamos descrever alguns pré-requisitos para garantir uma experiência de aprendizado tranquila.

### Conhecimento básico de C#

Embora o tutorial tenha sido criado para orientar você em cada etapa, ter um conhecimento básico de C# facilitará a compreensão dos conceitos apresentados.

### Ambiente de desenvolvimento .NET

Certifique-se de ter um ambiente de desenvolvimento .NET funcional configurado. Você pode usar o Visual Studio ou qualquer outro IDE que suporte desenvolvimento .NET.

### Pacote Aspose.Cells para .NET NuGet

Você precisa da biblioteca Aspose.Cells para .NET instalada no seu projeto. Você pode adicioná-la facilmente via NuGet Package Manager. 

Veja como fazer:

1. Abra seu projeto no Visual Studio.
2. Vá para "Ferramentas" > "Gerenciador de Pacotes NuGet" > "Gerenciar Pacotes NuGet para Solução".
3.  Procurar`Aspose.Cells` e instale a versão mais recente.

### Arquivo Excel básico para teste

Você precisará de um arquivo Excel de exemplo para trabalhar. Você pode criar um arquivo Excel simples com nomes de países aleatórios e seus códigos.

## Pacotes de importação

Para começar, vamos importar os pacotes necessários para o seu projeto. Aqui está um trecho de como configurar seu código:

```csharp
using System;
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

Com os pacotes importados, estamos prontos para seguir em frente.

## Etapa 1: Defina os diretórios de origem e saída 

O primeiro passo é definir onde seu arquivo de entrada está localizado e onde você quer que a saída (arquivo classificado) seja salva. Você precisa especificar dois caminhos: um para o arquivo Excel de origem e outro para salvar a saída após a classificação.

```csharp
string sourceDir = "Your Document Directory\\";
string outputDir = "Your Document Directory\\";
```

## Etapa 2: Carregue o arquivo de origem do Excel

Em seguida, carregaremos o arquivo Excel que contém os dados que você deseja classificar. Isso é feito criando uma instância do`Workbook` classe e passando o caminho do seu arquivo de origem.

```csharp
Workbook wb = new Workbook(sourceDir + "sampleSortData_CustomSortList.xlsx");
```

## Etapa 3: Acesse a primeira planilha 

Depois que o arquivo for carregado, precisamos acessar a planilha específica que contém os dados que pretendemos classificar. Neste caso, estamos mirando na primeira planilha.

```csharp
Worksheet ws = wb.Worksheets[0];
```

## Etapa 4: especifique a área da célula a ser classificada

 Precisamos determinar o intervalo de células que classificaremos. Neste exemplo, classificaremos as células de A1 a A40. Use o`CellArea.CreateCellArea` método para definir a área da célula.

```csharp
CellArea ca = CellArea.CreateCellArea("A1", "A40");
```

## Etapa 5: Crie uma lista de classificação personalizada

Antes de classificar, precisamos estabelecer os critérios que usaremos para nossa classificação personalizada. Você pode definir uma lista de classificação como uma matriz de strings. A lista de classificação personalizada ditará a ordem da classificação.

```csharp
string[] customSortList = new string[] { "USA,US", "Brazil,BR", "China,CN", "Russia,RU", "Canada,CA" };
```

## Etapa 6: adicione a chave de classificação e execute a classificação

Agora é hora de classificar! Usaremos a classe DataSorter para isso. Crie uma chave para classificação com base em nossa lista personalizada e execute a operação de classificação.

```csharp
wb.DataSorter.AddKey(0, SortOrder.Ascending, customSortList);
wb.DataSorter.Sort(ws.Cells, ca);
```

## Etapa 7: Salve o arquivo de saída do Excel

Após a classificação ser concluída, a última etapa é salvar as alterações em um novo arquivo do Excel. Especifique o nome do arquivo de saída e salve a pasta de trabalho.

```csharp
wb.Save(outputDir + "outputSortData_CustomSortList.xlsx");
```

## Etapa 8: Confirme a execução bem-sucedida

Para garantir que tudo funcionou perfeitamente, você pode imprimir uma mensagem de confirmação no console. Isso ajuda na depuração e lhe dá a satisfação de que a operação foi bem-sucedida.

```csharp
Console.WriteLine("SortDataInColumnWithCustomSortList executed successfully.\r\n");
```

## Conclusão

E aí está! Você classificou com sucesso os dados em uma coluna do Excel usando uma lista de classificação personalizada com o Aspose.Cells para .NET. A classificação ajuda a dar estrutura e clareza aos seus dados, facilitando a análise e a interpretação. Espero que este guia leve suas habilidades para o próximo nível e ajude você a perceber o quão poderoso o Aspose.Cells pode ser para suas tarefas relacionadas ao Excel.

## Perguntas frequentes

### O que é Aspose.Cells para .NET?
Aspose.Cells para .NET é uma biblioteca abrangente que permite manipular arquivos do Excel em aplicativos .NET, incluindo criação, edição e conversão.

### Posso classificar mais de uma coluna usando uma lista de classificação personalizada?
Sim! Você pode adicionar chaves adicionais para classificar por múltiplas colunas, se necessário, basta seguir o mesmo procedimento para cada chave.

### Preciso de conhecimento prévio de C# para usar o Aspose.Cells?
Embora seja útil, você pode acompanhar este tutorial e aprender conforme avança! Ter algum conhecimento básico de C# vai melhorar sua experiência de aprendizado.

### É possível usar uma licença temporária para o Aspose.Cells?
Claro! Você pode adquirir uma licença temporária se quiser testar todos os recursos da biblioteca sem restrições.

### Posso baixar exemplos ou documentação para Aspose.Cells?
 Sim! O Aspose fornece documentação extensa e projetos de amostra que podem ajudar muito você. Confira o[Documentação do Aspose.Cells](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
