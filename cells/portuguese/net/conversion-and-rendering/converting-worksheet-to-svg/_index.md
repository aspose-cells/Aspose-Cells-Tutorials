---
title: Convertendo planilha para SVG no .NET
linktitle: Convertendo planilha para SVG no .NET
second_title: API de processamento do Aspose.Cells .NET Excel
description: Aprenda como converter uma planilha do Excel para SVG usando Aspose.Cells para .NET com este guia passo a passo. Perfeito para desenvolvedores .NET que buscam renderizar Excel para SVG.
weight: 11
url: /pt/net/conversion-and-rendering/converting-worksheet-to-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Convertendo planilha para SVG no .NET

## Introdução

Se você está procurando converter uma planilha do Excel para o formato SVG, você veio ao lugar certo! Aspose.Cells para .NET é uma ferramenta poderosa que permite aos desenvolvedores manipular arquivos do Excel e convertê-los em vários formatos, incluindo o amplamente suportado SVG (Scalable Vector Graphics). Este tutorial irá guiá-lo através do processo de conversão de uma planilha para um SVG no .NET, dividindo-o passo a passo, para que até mesmo iniciantes possam acompanhar com facilidade.

## Pré-requisitos

Antes de mergulhar no código, vamos ter certeza de que você tem tudo o que precisa:

1.  Aspose.Cells para .NET: Baixe e instale a versão mais recente do Aspose.Cells para .NET em[Aspose.Cells para .NET](https://releases.aspose.com/cells/net/).
2. Ambiente de desenvolvimento .NET: você precisará do Visual Studio ou qualquer outro IDE .NET instalado.
3. Conhecimento básico de C#: É necessário ter familiaridade com C#, mas não se preocupe, explicaremos tudo claramente.
4. Arquivo Excel: tenha um arquivo Excel pronto que você gostaria de converter para o formato SVG.

## Importando Pacotes Necessários

Antes de começar a codificação, certifique-se de incluir os namespaces necessários no topo do seu arquivo C#.

```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Rendering;
```

Esses pacotes são necessários para trabalhar com Aspose.Cells e manipular opções de renderização, como exportação de SVG.

Agora que abordamos o básico, vamos passar para as etapas reais de conversão de uma planilha do Excel em uma imagem SVG.

## Etapa 1: Defina o caminho para o diretório de documentos

A primeira coisa que precisamos é definir o caminho para a pasta onde seu arquivo Excel está localizado. Isso é crucial porque seu código referenciará o diretório para carregar e salvar arquivos.

```csharp
// O caminho para o diretório de documentos
string dataDir = "Your Document Directory";
```

 Certifique-se de substituir`"Your Document Directory"`com o caminho real onde seu arquivo Excel reside.

##  Etapa 2: Carregue o arquivo Excel usando`Workbook`

 Em seguida, precisamos carregar o arquivo Excel em uma instância do`Workbook` classe. A`Workbook` class representa o arquivo Excel inteiro, incluindo todas as planilhas contidas nele.

```csharp
string filePath = dataDir + "Template.xlsx";
Workbook book = new Workbook(filePath);
```

 Aqui,`"Template.xlsx"` é o nome do arquivo Excel com o qual você está trabalhando. Certifique-se de que esse arquivo exista no diretório especificado, caso contrário, você encontrará erros.

## Etapa 3: Defina opções de imagem ou impressão para conversão de SVG

 Antes de convertermos a planilha para o formato SVG, precisamos especificar as opções de imagem. O`ImageOrPrintOptions` classe permite que você controle como a planilha será convertida. Especificamente, precisamos definir o`SaveFormat` para`SVG` e garantir que cada planilha seja convertida em uma única página.

```csharp
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
imgOptions.SaveFormat = SaveFormat.Svg;
imgOptions.OnePagePerSheet = true;
```

 O`SaveFormat.Svg` opção garante que o formato de saída será SVG, enquanto`OnePagePerSheet` garante que cada planilha será renderizada em uma única página.

## Etapa 4: iterar por cada planilha na pasta de trabalho

Agora precisamos fazer um loop por todas as planilhas no arquivo Excel. Cada planilha será convertida individualmente.

```csharp
foreach (Worksheet sheet in book.Worksheets)
{
    // Processaremos cada planilha uma por uma
}
```

Esse loop garante que, não importa quantas planilhas estejam presentes na sua pasta de trabalho, cada uma delas será manipulada.

##  Etapa 5: Crie um`SheetRender` Object for Rendering

 Para cada planilha, criaremos uma`SheetRender` objeto. Este objeto é responsável por converter a planilha para o formato de imagem desejado, que neste caso, é SVG.

```csharp
SheetRender sr = new SheetRender(sheet, imgOptions);
```

 O`SheetRender` objeto recebe dois argumentos: a planilha que você está convertendo e as opções de imagem que você definiu anteriormente.

## Etapa 6: converter a planilha para SVG

 Finalmente, dentro do loop, converteremos cada planilha para o formato SVG. Usamos um loop aninhado para iterar pelas páginas (embora, neste caso, haja apenas uma página por planilha, graças ao`OnePagePerSheet` opção).

```csharp
for (int i = 0; i < sr.PageCount; i++)
{
    // Produza a planilha no formato de imagem Svg
    sr.ToImage(i, filePath + sheet.Name + i + ".out.svg");
}
```

Este código salvará a planilha como um arquivo SVG no mesmo diretório do arquivo Excel. Cada arquivo SVG será nomeado de acordo com o nome da planilha e um número de índice para evitar conflitos de nomenclatura.

## Conclusão

E é isso! Você converteu com sucesso uma planilha do Excel para o formato SVG usando o Aspose.Cells para .NET. Esse processo permite que você mantenha o layout e o design da sua planilha enquanto a torna visível em qualquer navegador ou dispositivo que suporte SVG, que é praticamente todos eles. Não importa se você está trabalhando com arquivos complexos do Excel ou apenas uma tabela simples, esse método garante que seus dados sejam lindamente renderizados em um formato amigável para a web.

## Perguntas frequentes

### O que é SVG e por que devo usá-lo?
SVG (Scalable Vector Graphics) é um formato amigável à web que pode ser dimensionado infinitamente sem perder qualidade. É perfeito para gráficos, diagramas e imagens que precisam ser exibidos em vários tamanhos.

### O Aspose.Cells pode manipular arquivos grandes do Excel para conversão?
Sim, o Aspose.Cells pode manipular com eficiência grandes arquivos do Excel e convertê-los para SVG sem problemas significativos de desempenho.

### Existe um limite para o número de planilhas que posso converter para SVG?
Não, não há limite inerente no Aspose.Cells para converter múltiplas planilhas. A única restrição seria a memória e o desempenho do seu sistema.

### Preciso de uma licença para usar o Aspose.Cells?
 Sim, o Aspose.Cells requer uma licença para uso em produção. Você pode obter uma licença temporária[aqui](https://purchase.aspose.com/temporary-license/) ou explorar o[teste gratuito](https://releases.aspose.com/).

### Posso personalizar a saída SVG?
 Sim, você pode ajustar o`ImageOrPrintOptions` para personalizar vários aspectos da saída SVG, como resolução e escala.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
