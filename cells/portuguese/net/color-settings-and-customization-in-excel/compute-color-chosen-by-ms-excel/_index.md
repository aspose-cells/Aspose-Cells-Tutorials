---
"description": "Aprenda a calcular a cor escolhida pelo MS Excel usando o Aspose.Cells para .NET. Siga este guia passo a passo para acessar a cor de formatação condicional do Excel programaticamente."
"linktitle": "Calcular a cor escolhida pelo MS Excel programaticamente"
"second_title": "API de processamento do Excel Aspose.Cells .NET"
"title": "Calcular a cor escolhida pelo MS Excel programaticamente"
"url": "/pt/net/color-settings-and-customization-in-excel/compute-color-chosen-by-ms-excel/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Calcular a cor escolhida pelo MS Excel programaticamente

## Introdução
Você já trabalhou com arquivos do Excel e se perguntou como certas cores são selecionadas automaticamente para formatação? Você não está sozinho. A formatação condicional do Excel pode ser um mistério, especialmente ao tentar extrair a cor exata que o Excel atribui. Mas não se preocupe, nós ajudamos você! Neste tutorial, vamos nos aprofundar em como calcular programaticamente a cor escolhida pelo MS Excel usando o Aspose.Cells para .NET. Vamos explicar passo a passo para que você possa acompanhar e aplicar aos seus próprios projetos com facilidade. Vamos começar!
## Pré-requisitos
Antes de mergulhar no código, vamos cobrir o que você precisa para seguir este tutorial:
- Aspose.Cells para .NET instalado. Se você ainda não o tem, você pode [baixe aqui](https://releases.aspose.com/cells/net/).
- Conhecimento prático de C# e .NET framework.
- Um arquivo de exemplo do Excel (Book1.xlsx) com alguma formatação condicional aplicada.
Você também pode experimentar a versão de avaliação gratuita do Aspose.Cells para .NET se ainda não tiver uma licença. Baixe a versão de avaliação [aqui](https://releases.aspose.com/).
## Pacotes de importação
Antes de começarmos a programar, precisamos importar os pacotes necessários para garantir que tudo corra bem. Certifique-se de incluir os seguintes namespaces no seu projeto:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
using System;
```
Essas importações fornecem acesso às principais classes Aspose.Cells e à biblioteca de desenho do sistema nativo do .NET para manipulação de cores.

Agora que temos tudo pronto, vamos dividir essa tarefa em etapas fáceis de entender:
## Etapa 1: Configurar o objeto da pasta de trabalho
A primeira coisa que precisamos fazer é instanciar um `Workbook` objeto e carregar o arquivo Excel com o qual queremos trabalhar. É aqui que a jornada começa!
```csharp
// O caminho para o diretório de documentos.
string dataDir = "Your Document Directory";
// Instanciar um objeto de pasta de trabalho e abrir o arquivo de modelo
Workbook workbook = new Workbook(dataDir + "Book1.xlsx");
```
Nesta etapa, estamos criando uma nova instância do `Workbook` classe de Aspose.Cells. A `Workbook` A classe representa um arquivo do Excel e, ao fornecer o caminho para o nosso arquivo, podemos carregá-lo facilmente para manipulação posterior.
## Etapa 2: Acesse a primeira planilha
Após o carregamento da pasta de trabalho, precisamos acessar a planilha específica da qual queremos extrair a cor. Neste exemplo, trabalharemos com a primeira planilha.
```csharp
// Obtenha a primeira planilha
Worksheet worksheet = workbook.Worksheets[0];
```
Aqui, estamos buscando a primeira planilha na pasta de trabalho usando o `Worksheets[0]` índice. O Aspose.Cells permite que você acesse qualquer planilha no arquivo Excel pelo seu índice ou nome.
## Etapa 3: Selecione a célula de interesse
Em seguida, escolheremos uma célula específica na planilha. Neste tutorial, focaremos na célula "A1", mas você pode selecionar qualquer célula com formatação condicional aplicada.
```csharp
// Obtenha a célula A1
Cell a1 = worksheet.Cells["A1"];
```
Nós usamos o `Cells` propriedade para referenciar uma célula específica pelo seu endereço. Neste caso, estamos selecionando a célula "A1" porque queremos extrair os resultados da formatação condicional aplicados a esta célula.
## Etapa 4: recuperar o resultado da formatação condicional
Agora é onde a mágica acontece! Usaremos Aspose.Cells para obter o resultado da formatação condicional da célula selecionada. É assim que o Excel calcula a formatação dinamicamente, incluindo as cores.
```csharp
// Obter o objeto resultante da formatação condicional
ConditionalFormattingResult cfr1 = a1.GetConditionalFormattingResult();
```
O `GetConditionalFormattingResult()` O método é crucial nesta etapa. Ele retorna um objeto que contém os resultados de qualquer formatação condicional aplicada à célula. É aqui que começamos a explorar as informações de cores que o Excel está usando.
## Etapa 5: Acesse o ColorScaleResult
Depois que tivermos o resultado da formatação condicional, podemos nos aprofundar e acessar a escala de cores que o Excel usou para essa célula específica.
```csharp
// Obter o objeto de cor resultante ColorScale
Color c = cfr1.ColorScaleResult;
```
A formatação condicional no Excel geralmente depende de escalas de cores. Esta linha nos permite extrair a cor resultante que foi aplicada com base nas regras de formatação condicional.
## Etapa 6: Produzir as informações de cor
Por fim, queremos ver a cor aplicada no Excel. Vamos imprimir os detalhes da cor em um formato fácil de entender, incluindo o valor ARGB e o nome.
```csharp
// Leia a cor
Console.WriteLine(c.ToArgb().ToString());
Console.WriteLine(c.Name);
```
O `ToArgb()` método nos dá a cor no formato ARGB (Alfa, Vermelho, Verde, Azul), enquanto o `Name` A propriedade fornece o nome da cor em um formato mais legível. Você pode usar esses detalhes de cor para corresponder a eles em outros aplicativos ou modificar seus arquivos do Excel programaticamente.

## Conclusão
pronto! Seguindo estes passos, você acabou de aprender a calcular programaticamente a cor escolhida pelo MS Excel usando o Aspose.Cells para .NET. Essa abordagem pode ser incrivelmente útil para automatizar tarefas baseadas no Excel, especialmente ao lidar com formatação condicional complexa. Agora, da próxima vez que encontrar uma cor misteriosa no Excel, você saberá exatamente como revelar seus segredos.
## Perguntas frequentes
### Posso aplicar formatação condicional programaticamente usando Aspose.Cells?
Sim, o Aspose.Cells permite que você aplique, modifique e até mesmo remova formatação condicional em arquivos do Excel programaticamente.
### O Aspose.Cells é compatível com todas as versões do Excel?
Com certeza! O Aspose.Cells é compatível com Excel 97-2003 (XLS), Excel 2007-2019/365 (XLSX) e outros formatos, incluindo PDF, HTML e CSV.
### O Aspose.Cells está disponível para outras plataformas além do .NET?
Sim, o Aspose.Cells está disponível para várias plataformas, incluindo Java, C++ e Android via Java.
### Como posso obter uma avaliação gratuita do Aspose.Cells?
Você pode baixar uma versão de avaliação gratuita do Aspose.Cells para .NET em [aqui](https://releases.aspose.com/).
### Como lidar com arquivos grandes do Excel com o Aspose.Cells?
O Aspose.Cells é otimizado para desempenho, mesmo ao lidar com arquivos grandes. Você pode utilizar APIs de streaming para lidar com grandes volumes de dados com eficiência.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}