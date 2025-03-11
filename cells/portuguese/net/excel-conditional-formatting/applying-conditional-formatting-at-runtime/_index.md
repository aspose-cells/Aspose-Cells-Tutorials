---
title: Aplicando formatação condicional em tempo de execução no Excel
linktitle: Aplicando formatação condicional em tempo de execução no Excel
second_title: API de processamento do Aspose.Cells .NET Excel
description: Aprenda como aplicar formatação condicional em tempo de execução no Excel com o Aspose.Cells para .NET neste guia abrangente passo a passo.
weight: 11
url: /pt/net/excel-conditional-formatting/applying-conditional-formatting-at-runtime/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aplicando formatação condicional em tempo de execução no Excel

## Introdução

elas são ferramentas poderosas para análise e visualização de dados. Um dos recursos de destaque do Excel é a formatação condicional, que permite que os usuários apliquem estilos de formatação específicos às células com base em seus valores. Isso pode facilitar a identificação de tendências, destacar pontos de dados importantes ou simplesmente tornar os dados mais legíveis. Se você está procurando implementar formatação condicional em seus arquivos do Excel programaticamente, você está no lugar certo! Neste guia, mostraremos como aplicar formatação condicional em tempo de execução usando o Aspose.Cells para .NET.

## Pré-requisitos
Antes de mergulhar no código, vamos garantir que você tenha tudo o que precisa para começar:

1. Visual Studio: Certifique-se de ter o Visual Studio instalado em sua máquina. Você pode usar qualquer versão que suporte desenvolvimento .NET.
2.  Aspose.Cells para .NET: Você precisará ter o Aspose.Cells para .NET instalado. Você pode baixá-lo do[Site Aspose](https://releases.aspose.com/cells/net/).
3. Conhecimento básico de C#: A familiaridade com a programação em C# ajudará você a entender melhor os trechos de código.
4. .NET Framework: certifique-se de que seu projeto esteja direcionado a uma versão compatível do .NET Framework.

Agora que cobrimos os pré-requisitos, vamos para a parte divertida!

## Pacotes de importação
Para começar a usar o Aspose.Cells, você precisará importar os namespaces necessários no seu projeto C#. Veja como você pode fazer isso:

```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

Esses namespaces darão acesso às classes e métodos necessários para manipular arquivos do Excel e aplicar formatação condicional.

Agora, vamos dividir o processo de aplicação da formatação condicional em etapas gerenciáveis.

## Etapa 1: configure seu projeto
Primeiro, você precisa criar um novo projeto C# no Visual Studio. Veja como:

1. Abra o Visual Studio e selecione Arquivo > Novo > Projeto.
2. Escolha Console App (.NET Framework) e dê um nome ao seu projeto.
3. Clique em Criar.

## Etapa 2: Adicionar referência Aspose.Cells
Depois que seu projeto estiver configurado, você precisa adicionar uma referência à biblioteca Aspose.Cells:

1. Clique com o botão direito do mouse no seu projeto no Solution Explorer.
2. Selecione Gerenciar pacotes NuGet.
3. Procure por Aspose.Cells e instale-o.

Isso permitirá que você use todas as funcionalidades fornecidas pela biblioteca Aspose.Cells.

## Etapa 3: Criar um objeto de pasta de trabalho
Em seguida, vamos criar uma nova pasta de trabalho e uma planilha. É aqui que toda a mágica acontece:

```csharp
// O caminho para o diretório de documentos.
string dataDir = "Your Document Directory";
string filePath = dataDir + "Book1.xlsx";

// Instanciando um objeto Workbook
Workbook workbook = new Workbook();
Worksheet sheet = workbook.Worksheets[0];
```

Nesta etapa, definimos o diretório onde nosso arquivo Excel será salvo, criamos uma nova pasta de trabalho e acessamos a primeira planilha.

## Etapa 4: Adicionar formatação condicional
Agora, vamos adicionar alguma formatação condicional. Começaremos criando um objeto de formatação condicional vazio:

```csharp
// Adiciona uma formatação condicional vazia
int index = sheet.ConditionalFormattings.Add();
FormatConditionCollection fcs = sheet.ConditionalFormattings[index];
```

Aqui, estamos adicionando uma nova coleção de formatação condicional à nossa planilha, que conterá nossas regras de formatação.

## Etapa 5: Defina o intervalo de formato
Em seguida, precisamos especificar o intervalo de células ao qual a formatação condicional será aplicada. Digamos que queremos formatar a primeira linha e a segunda coluna:

```csharp
// Define o intervalo de formato condicional.
CellArea ca = new CellArea();
ca.StartRow =0;
ca.EndRow =0;
ca.StartColumn =0;
ca.EndColumn =0;
fcs.AddArea(ca);

ca = new CellArea();
ca.StartRow =1;
ca.EndRow =1;
ca.StartColumn =1;
ca.EndColumn =1;
fcs.AddArea(ca);
```

Neste código, definimos duas áreas para formatação condicional. A primeira área é para a célula em (0,0) e a segunda para (1,1). Sinta-se à vontade para ajustar esses intervalos com base em suas necessidades específicas!

## Etapa 6: Adicionar condições de formatação condicional
Agora é hora de definir as condições para nossa formatação. Digamos que queremos destacar células com base em seus valores:

```csharp
// Adiciona condição.
int conditionIndex = fcs.AddCondition(FormatConditionType.CellValue, OperatorType.Between, "=A2", "100");

// Adiciona condição.
int conditionIndex2 = fcs.AddCondition(FormatConditionType.CellValue, OperatorType.Between, "50", "100");
```

 Nesta etapa, estamos adicionando duas condições: uma para valores entre`A2` e`100` , e outro para valores entre`50` e`100`. Isso permite que você destaque células dinamicamente com base em seus valores.

## Etapa 7: Defina os estilos de formatação
Com nossas condições em vigor, agora podemos definir os estilos de formatação. Vamos mudar a cor de fundo para nossas condições:

```csharp
// Define a cor de fundo.
FormatCondition fc = fcs[conditionIndex];
fc.Style.BackgroundColor = Color.Red;
```

Aqui, estamos definindo a cor de fundo da primeira condição para vermelho. Você pode personalizar isso ainda mais alterando a cor da fonte, bordas e outros estilos conforme necessário!

## Etapa 8: Salve o arquivo Excel
Finalmente, é hora de salvar nosso trabalho! Salvaremos a pasta de trabalho no diretório especificado:

```csharp
// Salvando o arquivo Excel
workbook.Save(dataDir + "output.xls");
```

Esta linha de código salva o arquivo Excel com a formatação condicional aplicada. Certifique-se de verificar o diretório especificado para seu arquivo de saída!

## Conclusão
aí está! Você aplicou com sucesso a formatação condicional em tempo de execução no Excel usando o Aspose.Cells para .NET. Esta biblioteca poderosa facilita a manipulação de arquivos do Excel programaticamente, permitindo que você automatize tarefas tediosas e aprimore suas apresentações de dados. Não importa se você está trabalhando em um projeto pequeno ou em um aplicativo de grande escala, o Aspose.Cells pode ajudar a simplificar seu fluxo de trabalho e melhorar sua produtividade.

## Perguntas frequentes

### O que é Aspose.Cells?
Aspose.Cells é uma biblioteca .NET que permite aos desenvolvedores criar, manipular e converter arquivos do Excel programaticamente.

### Posso usar o Aspose.Cells com outras linguagens de programação?
Sim, o Aspose.Cells está disponível para diversas linguagens de programação, incluindo Java, Python e muito mais.

### Existe um teste gratuito disponível para o Aspose.Cells?
 Sim, você pode baixar uma versão de avaliação gratuita do[Site Aspose](https://releases.aspose.com/).

### Como posso obter suporte para o Aspose.Cells?
 Você pode obter suporte visitando o[Fórum de suporte Aspose](https://forum.aspose.com/c/cells/9).

### Preciso de uma licença para usar o Aspose.Cells?
 Sim, é necessária uma licença para uso comercial, mas você pode solicitar uma licença temporária[aqui](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
