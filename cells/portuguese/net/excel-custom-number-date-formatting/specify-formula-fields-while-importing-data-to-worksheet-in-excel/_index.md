---
title: Especificar campos de fórmula ao importar dados para uma planilha do Excel
linktitle: Especificar campos de fórmula ao importar dados para uma planilha do Excel
second_title: API de processamento do Aspose.Cells .NET Excel
description: Aprenda como importar dados para planilhas do Excel com campos de fórmula especificados usando o Aspose.Cells para .NET neste tutorial detalhado.
weight: 11
url: /pt/net/excel-custom-number-date-formatting/specify-formula-fields-while-importing-data-to-worksheet-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Especificar campos de fórmula ao importar dados para uma planilha do Excel

## Introdução

Quando se trata de manipular arquivos do Excel programaticamente, o Aspose.Cells for .NET é uma ferramenta inestimável. Ele fornece funcionalidade robusta para criar, modificar e manipular planilhas do Excel com facilidade. Um dos recursos interessantes que ele oferece é a capacidade de especificar campos de fórmula ao importar dados para uma planilha do Excel. Imagine que você está trabalhando em um relatório financeiro e precisa calcular totais automaticamente com base na entrada do usuário. Este tutorial o guiará passo a passo para conseguir exatamente isso com uma abordagem limpa e direta.

## Pré-requisitos

Antes de mergulhar no código, vamos garantir que você tenha tudo o que precisa. 

1. Visual Studio ou qualquer ambiente de desenvolvimento integrado (IDE) .NET: certifique-se de ter um IDE adequado para escrever e executar seu código C#.
2.  Aspose.Cells para .NET: Você precisará baixar e referenciar a biblioteca Aspose.Cells em seu projeto. Você pode baixá-la do[Lançamentos da Aspose](https://releases.aspose.com/cells/net/).
3. Conhecimento básico de C#: A familiaridade com C# e conceitos de programação orientada a objetos ajudará você a entender melhor os exemplos.
4. .NET Framework: Este tutorial pressupõe que você esteja usando o .NET Framework 4.5 ou superior.

Depois de resolver os pré-requisitos, vamos prosseguir com a importação de alguns dados para uma planilha do Excel com campos de fórmula especificados.

## Pacotes de importação

Antes de começar a escrever seu código, você precisará importar o namespace Aspose.Cells necessário. Isso normalmente é feito no topo do seu arquivo C#:

```csharp
using Aspose.Cells;
using System;
using System.Collections.Generic;
```

Isso permite que você use as classes e os métodos fornecidos pela biblioteca Aspose.Cells sem precisar prefixá-los com o namespace todas as vezes.

Vamos dividir todo o processo em etapas gerenciáveis:

## Etapa 1: Defina o diretório de saída

Primeiro, você precisa estabelecer onde quer salvar seu arquivo Excel. Veja como você pode fazer isso:

```csharp
static string outputDir = "Your Document Directory"; // especifique seu diretório de documentos aqui
```

 Substituir`"Your Document Directory"` com seu caminho de arquivo real. É aqui que o arquivo Excel gerado será salvo.

## Etapa 2: Crie uma classe definida pelo usuário para itens de dados

Em seguida, definiremos uma classe para estruturar os dados que planejamos importar.

```csharp
class DataItems
{
    public int Number1 { get; set; }
    public int Number2 { get; set; }
    public string Formula1 { get; set; }
    public string Formula2 { get; set; }
}
```

 Esse`DataItems` A classe conterá os números inteiros brutos e as fórmulas que escreveremos na planilha do Excel. 

## Etapa 3: inicializar uma lista para conter itens de dados

 Usaremos uma lista para armazenar várias instâncias do nosso`DataItems` aula.

```csharp
List<DataItems> dis = new List<DataItems>();
```

## Etapa 4: Adicionar itens de dados à lista

Agora, vamos adicionar algumas entradas à nossa lista. Cada entrada conterá dois números e duas fórmulas.

```csharp
// Defina e adicione cada item de dados
DataItems di = new DataItems();
di.Number1 = 2002;
di.Number2 = 3502;
di.Formula1 = "=SUM(A2,B2)";
di.Formula2 = "=HYPERLINK(\"https://www.aspose.com\",\"Site Aspose\")";
dis.Add(di);

// Repita para itens de dados adicionais
```

 Certifique-se de personalizar cada`DataItems` instância com valores e fórmulas exclusivos.

## Etapa 5: Criar pasta de trabalho e planilha do Access

Em seguida, crie a pasta de trabalho e acesse a primeira planilha onde eventualmente importaremos os dados.

```csharp
Workbook wb = new Workbook(); // criar uma nova pasta de trabalho
Worksheet ws = wb.Worksheets[0]; // acesse a primeira planilha
```

## Etapa 6: especifique as opções de importação da tabela

É aqui que a mágica acontece. Você precisa especificar quais campos em seus dados correspondem a fórmulas. 

```csharp
ImportTableOptions opts = new ImportTableOptions();
opts.IsFormulas = new bool[] { false, false, true, true };
```

 Neste exemplo, os dois últimos campos contêm fórmulas, o que é indicado por`true` , enquanto os dois primeiros campos são definidos como`false`.

## Etapa 7: Importar objetos personalizados

Agora que tudo está configurado, vamos importar nossa lista de itens de dados para a planilha.

```csharp
ws.Cells.ImportCustomObjects(dis, 0, 0, opts);
```

Esta linha importa efetivamente os dados começando na célula A1.

## Etapa 8: Calcular fórmulas

Como importamos algumas fórmulas, é essencial calculá-las.

```csharp
wb.CalculateFormula();
```

Este método garante que suas fórmulas sejam avaliadas com base em suas dependências.

## Etapa 9: Ajuste automático de colunas

Para garantir que seus dados sejam exibidos de forma amigável, você pode ajustar automaticamente as colunas com base no conteúdo.

```csharp
ws.AutoFitColumns();
```

Esta etapa otimiza o layout do arquivo Excel. 

## Etapa 10: Salve seu arquivo Excel

Por fim, é hora de salvar o arquivo Excel recém-criado. 

```csharp
wb.Save(outputDir + "outputSpecifyFormulaFieldsWhileImportingDataToWorksheet.xlsx");
```

Certifique-se de que o nome do arquivo de saída seja relevante e descritivo!

## Etapa 11: Verificando a execução

Como uma maneira simples de confirmar se tudo ocorreu corretamente, você pode imprimir uma mensagem.

```csharp
Console.WriteLine("SpecifyFormulaFieldsWhileImportingDataToWorksheet executed successfully.");
```

Isso lhe dá um feedback imediato de que o código funcionou sem problemas.

## Conclusão

aí está! Você importou dados com sucesso para uma planilha do Excel usando o Aspose.Cells para .NET e especificou campos de fórmula. Seguindo essas etapas, você pode aplicar técnicas semelhantes para automatizar tarefas de processamento de dados adaptadas às suas necessidades. Quer você esteja processando números para relatórios ou simplesmente mantendo dados, dominar a arte da manipulação do Excel com o Aspose é uma habilidade que vale a pena ter.

## Perguntas frequentes

### O que é Aspose.Cells?
Aspose.Cells é uma biblioteca .NET projetada para criar, manipular e converter arquivos do Excel programaticamente.

### Como instalo o Aspose.Cells para .NET?
 Você pode baixá-lo do[Lançamentos da Aspose](https://releases.aspose.com/cells/net/) e referencie-o em seu projeto.

### Posso usar o Aspose.Cells gratuitamente?
 Sim, o Aspose oferece um teste gratuito disponível em[este link](https://releases.aspose.com/).

### Onde posso encontrar mais exemplos?
 Exemplos e documentação adicionais podem ser encontrados em[Página de documentação do Aspose](https://reference.aspose.com/cells/net/).

### E se eu tiver problemas ao usar o Aspose?
 Você pode buscar ajuda no fórum de suporte do Aspose[aqui](https://forum.aspose.com/c/cells/9).
 
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
