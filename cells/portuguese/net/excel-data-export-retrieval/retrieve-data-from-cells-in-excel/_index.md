---
title: Recuperar dados de células no Excel
linktitle: Recuperar dados de células no Excel
second_title: API de processamento do Aspose.Cells .NET Excel
description: Aprenda como recuperar dados de células do Excel usando o Aspose.Cells para .NET neste tutorial passo a passo, perfeito para iniciantes e desenvolvedores experientes.
weight: 10
url: /pt/net/excel-data-export-retrieval/retrieve-data-from-cells-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Recuperar dados de células no Excel

## Introdução

Quando se trata de gerenciar dados no Excel, a capacidade de ler e recuperar informações de células é crucial. Aspose.Cells para .NET é uma biblioteca poderosa que permite aos desenvolvedores manipular arquivos do Excel perfeitamente. Neste tutorial, vamos nos aprofundar em como recuperar dados de células em uma pasta de trabalho do Excel usando o Aspose.Cells. Seja você um desenvolvedor experiente ou apenas começando, este guia o guiará pelo processo passo a passo.

## Pré-requisitos

Antes de começarmos a usar o código, há alguns pré-requisitos que você precisa ter em mente:

1. Visual Studio: Certifique-se de ter o Visual Studio instalado em sua máquina. É o IDE que usaremos para escrever e executar nosso código.
2.  Aspose.Cells para .NET: Você precisa ter a biblioteca Aspose.Cells. Você pode baixá-la do[Site Aspose](https://releases.aspose.com/cells/net/).
3. Conhecimento básico de C#: A familiaridade com a programação em C# ajudará você a entender melhor os exemplos.
4. Arquivo Excel: Tenha um arquivo Excel pronto (por exemplo,`book1.xls`) que você usará neste tutorial.

Depois de resolver esses pré-requisitos, podemos começar a explorar como recuperar dados de células do Excel.

## Pacotes de importação

Para começar, você precisa importar os namespaces necessários no seu projeto C#. Isso permitirá que você utilize as classes e métodos fornecidos pelo Aspose.Cells.

```csharp
using System.IO;
using Aspose.Cells;
using System;
```

Com esses namespaces importados, você está pronto para começar a codificar. Vamos dividir o processo em etapas gerenciáveis.

## Etapa 1: configure seu diretório de documentos

O primeiro passo é definir o caminho para o diretório de documentos onde seu arquivo Excel está localizado. Isso é crucial porque diz ao aplicativo onde encontrar o arquivo com o qual você quer trabalhar.


```csharp
// O caminho para o diretório de documentos.
string dataDir = "Your Document Directory";
```

 Substituir`"Your Document Directory"` com o caminho real onde seu`book1.xls` o arquivo é armazenado. Este caminho é onde o Aspose.Cells procurará o arquivo quando você tentar abri-lo.

## Etapa 2: Abra a pasta de trabalho existente

Agora que você configurou o diretório do documento, o próximo passo é abrir a pasta de trabalho (arquivo do Excel) com a qual deseja trabalhar.


```csharp
//Abrindo uma pasta de trabalho existente
Workbook workbook = new Workbook(dataDir + "book1.xls");
```

 Aqui, criamos um`Workbook` objeto passando o caminho completo do arquivo Excel. Esta etapa inicializa a pasta de trabalho e a deixa pronta para recuperação de dados.

## Etapa 3: Acesse a primeira planilha

Após abrir a pasta de trabalho, você vai querer acessar a planilha específica da qual você quer recuperar dados. Neste caso, acessaremos a primeira planilha.


```csharp
// Acessando a primeira planilha
Worksheet worksheet = workbook.Worksheets[0];
```

 O`Worksheets` coleção permite que você acesse diferentes planilhas na pasta de trabalho. O índice`[0]` refere-se à primeira planilha. Se você quiser acessar planilhas subsequentes, você pode alterar o índice de acordo.

## Etapa 4: Loop através das células

Agora que você tem a planilha, é hora de percorrer cada célula para recuperar os dados. É aqui que a mágica acontece!


```csharp
foreach (Cell cell1 in worksheet.Cells)
{
    // Variáveis para armazenar valores de diferentes tipos de dados
    string stringValue;
    double doubleValue;
    bool boolValue;
    DateTime dateTimeValue;

    // Passando o tipo dos dados contidos na célula para avaliação
    switch (cell1.Type)
    {
        // Avaliando o tipo de dados da célula para valor de string
        case CellValueType.IsString:
            stringValue = cell1.StringValue;
            Console.WriteLine("String Value: " + stringValue);
            break;

        // Avaliando o tipo de dados da célula para valor duplo
        case CellValueType.IsNumeric:
            doubleValue = cell1.DoubleValue;
            Console.WriteLine("Double Value: " + doubleValue);
            break;

        //Avaliando o tipo de dados da célula para valor booleano
        case CellValueType.IsBool:
            boolValue = cell1.BoolValue;
            Console.WriteLine("Bool Value: " + boolValue);
            break;

        // Avaliando o tipo de dados da célula para valor de data/hora
        case CellValueType.IsDateTime:
            dateTimeValue = cell1.DateTimeValue;
            Console.WriteLine("DateTime Value: " + dateTimeValue);
            break;

        // Avaliando o tipo de dados desconhecido dos dados da célula
        case CellValueType.IsUnknown:
            stringValue = cell1.StringValue;
            Console.WriteLine("Unknown Value: " + stringValue);
            break;

        // Terminando a verificação de tipo de tipo de dados da célula é nulo
        case CellValueType.IsNull:
            break;
    }
}
```

 Nesta etapa, fazemos um loop em cada célula da planilha. Para cada célula, verificamos seu tipo de dados usando um`switch` declaração. Dependendo do tipo, recuperamos o valor e o imprimimos no console. Aqui está uma análise dos casos:

-  IsString: Se a célula contiver uma string, nós a recuperamos usando`StringValue`.
-  IsNumeric: Para valores numéricos, usamos`DoubleValue`.
-  IsBool: Se a célula contiver um valor booleano, nós o acessamos usando`BoolValue`.
-  IsDateTime: Para valores de data e hora, usamos`DateTimeValue`.
- IsUnknown: Se o tipo de dado for desconhecido, ainda recuperamos a representação da string.
- IsNull: Se a célula estiver vazia, simplesmente a ignoramos.

## Conclusão

Recuperar dados de células do Excel usando o Aspose.Cells para .NET é um processo direto. Seguindo essas etapas, você pode extrair com eficiência vários tipos de dados dos seus arquivos do Excel. Não importa se você está criando uma ferramenta de relatórios, automatizando a entrada de dados ou apenas precisa analisar dados, o Aspose.Cells fornece a flexibilidade e o poder necessários para fazer o trabalho.

## Perguntas frequentes

### O que é Aspose.Cells?  
Aspose.Cells é uma biblioteca .NET que permite aos desenvolvedores criar, manipular e converter arquivos do Excel sem precisar instalar o Microsoft Excel.

### Posso usar o Aspose.Cells gratuitamente?  
 Sim, o Aspose.Cells oferece um teste gratuito que você pode usar para testar seus recursos. Você pode baixá-lo[aqui](https://releases.aspose.com/).

### Que tipos de dados posso recuperar de células do Excel?  
Você pode recuperar vários tipos de dados, incluindo strings, números, booleanos e valores de data/hora.

### Como obtenho suporte para o Aspose.Cells?  
 Você pode obter suporte visitando o[Fórum Aspose](https://forum.aspose.com/c/cells/9) onde você pode fazer perguntas e obter ajuda da comunidade.

### Existe uma licença temporária disponível?  
 Sim, a Aspose oferece uma licença temporária para fins de avaliação. Você pode encontrar mais informações[aqui](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
