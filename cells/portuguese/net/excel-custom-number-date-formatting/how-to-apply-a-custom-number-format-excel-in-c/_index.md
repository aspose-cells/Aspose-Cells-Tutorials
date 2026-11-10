---
category: general
date: 2026-10-26
description: Aprenda como definir um formato numérico personalizado em um arquivo
  Excel em C# configurando dígitos significativos, criando uma pasta de trabalho Excel
  e salvando-a como um documento XLSX.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- custom number format excel
- set significant digits
- how to set number format
- create excel workbook c#
- save workbook xlsx
language: pt
lastmod: 2026-10-26
og_description: O formato de número personalizado no Excel em C# permite controlar
  os dígitos significativos, criar uma pasta de trabalho do Excel e salvá‑la como
  XLSX. Siga este tutorial completo.
og_image_alt: Excel cell A1 displaying a number formatted with 4 significant digits
  using C#
og_title: Formato numérico personalizado no Excel em C# – guia passo a passo
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to set a custom number format excel file in C# by configuring
    significant digits, creating an Excel workbook, and saving it as an XLSX document.
  headline: How to apply a custom number format excel in C#
  type: TechArticle
- description: Learn how to set a custom number format excel file in C# by configuring
    significant digits, creating an Excel workbook, and saving it as an XLSX document.
  name: How to apply a custom number format excel in C#
  steps:
  - name: Using a custom format string instead of global options
    text: 'If you need a format that applies only to a single range, you can assign
      a format string directly:'
  - name: Applying the setting to an entire column
    text: '```csharp // Apply the same significant‑digit rule to column B ws.Cells.Columns[1].ApplyNumberFormatOptions(
      new NumberFormatOptions { SignificantDigits = 4 }); ```'
  - name: Dealing with negative numbers
    text: 'The global `SignificantDigits` option works uniformly for positive and
      negative numbers. If you want a different display for negatives, combine it
      with a custom format:'
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: Como aplicar um formato numérico personalizado do Excel em C#
url: /pt/net/excel-custom-number-date-formatting/how-to-apply-a-custom-number-format-excel-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como aplicar um formato numérico personalizado no Excel em C#

Se você precisa de um **formato numérico personalizado no Excel** que mostre um número específico de dígitos significativos, este guia mostra exatamente como fazer isso em C#. Você verá como definir dígitos significativos, criar uma pasta de trabalho Excel e salvar o arquivo como XLSX — tudo com poucas linhas de código.

Trabalhar programaticamente com arquivos Excel geralmente exige controlar como os números são exibidos. Usando Aspose.Cells para .NET, você pode definir uma opção global de formato numérico que força cada célula numérica a respeitar uma quantidade determinada de dígitos significativos. Este tutorial cobre todo o fluxo de trabalho, desde a configuração do projeto até a verificação do resultado no Excel.

## Pré‑requisitos

Antes de começar, certifique‑se de que você tem:

* .NET 6.0 ou superior instalado (o código também funciona com .NET Framework 4.7.2+)
* Visual Studio 2022 ou qualquer IDE C# de sua preferência
* O pacote NuGet **Aspose.Cells** (`Install-Package Aspose.Cells`) – uma biblioteca totalmente gerenciada para manipulação de Excel
* Familiaridade básica com a sintaxe C#

## Etapa 1: Criar uma pasta de trabalho Excel em C#

A primeira operação é instanciar um novo objeto `Workbook`. Esse objeto representa todo o arquivo Excel na memória.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook instance
        Workbook wb = new Workbook();

        // The workbook now contains a default worksheet named "Sheet1"
        // You can access it via the Worksheets collection.
        Worksheet ws = wb.Worksheets[0];
```

**Por que isso importa:** `Workbook` é o ponto de entrada para toda operação no Excel. Ao criá‑lo primeiro, você garante um arquivo limpo que pode ser salvo posteriormente como XLSX.

## Etapa 2: Configurar o formato numérico para definir dígitos significativos

Aspose.Cells fornece uma configuração global chamada `NumberFormatOptions`. Ao atribuir `SignificantDigits = 4`, cada célula numérica exibirá até quatro dígitos significativos, a menos que um formato mais específico a sobrescreva.

```csharp
        // Step 2: Set the global number‑format option to 4 significant digits
        WorkbookSettings.SetNumberFormatOptions(
            new NumberFormatOptions { SignificantDigits = 4 });
```

**Por que isso importa:** Usar `SetNumberFormatOptions` permite definir um **formato numérico personalizado no Excel** sem precisar escrever uma string de formato para cada célula. Ele espelha a opção “Dígitos Significativos” que você encontraria na caixa de diálogo *Formatar Células → Número → Personalizado* do Excel.

## Etapa 3: Inserir valores e verificar o formato numérico personalizado

Agora coloque um valor numérico em uma célula. A configuração global aplicará automaticamente a regra de 4 dígitos.

```csharp
        // Step 3: Write a numeric value into cell A1 (row 0, column 0)
        ws.Cells[0, 0].PutValue(123.456789);

        // Optional: Add a label so you can see the effect in Excel
        ws.Cells[0, 1].PutValue("Original value:");
        ws.Cells[0, 2].PutValue(123.456789);
```

Ao abrir o arquivo salvo, a célula **A1** exibirá `123.5` (arredondado para quatro dígitos significativos). O valor original permanece inalterado nos dados subjacentes, o que pode ser confirmado observando a barra de fórmulas.

**Dica para casos extremos:** Se você armazenar um número muito grande como `12345678.9`, a mesma configuração exibirá `1.235E+07` (notação científica) porque o Excel escolhe a representação mais compacta preservando quatro dígitos significativos.

## Etapa 4: Salvar a pasta de trabalho como XLSX

Por fim, persista a pasta de trabalho no disco. O método `Save` escolhe automaticamente o formato do arquivo com base na extensão.

```csharp
        // Step 4: Save the workbook to an XLSX file
        string outputPath = @"C:\Temp\SigDigits.xlsx";
        wb.Save(outputPath);

        // Inform the user
        System.Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**Por que isso importa:** Salvar como **XLSX** (`save workbook xlsx`) garante máxima compatibilidade com versões modernas do Excel, Office 365 e outras ferramentas de planilha.

## Resultado esperado

Abra *C:\Temp\SigDigits.xlsx* no Microsoft Excel. Você deverá ver:

| A          | B               | C               |
|------------|-----------------|-----------------|
| **123.5**  | Valor original: | **123.456789**  |

*Cell A1* mostra o número arredondado para quatro dígitos significativos, enquanto *C1* mantém a precisão total para comparação.

## Variações comuns e como definir formato numérico para células específicas

### Usando uma string de formato personalizada em vez de opções globais

Se precisar de um formato que se aplique apenas a um intervalo único, pode atribuir uma string de formato diretamente:

```csharp
ws.Cells["D1"].PutValue(0.0012345);
Style style = wb.CreateStyle();
style.Custom = "0.####"; // shows up to 4 decimal places, not significant digits
ws.Cells["D1"].SetStyle(style);
```

### Aplicando a configuração a uma coluna inteira

```csharp
// Apply the same significant‑digit rule to column B
ws.Cells.Columns[1].ApplyNumberFormatOptions(
    new NumberFormatOptions { SignificantDigits = 4 });
```

### Lidando com números negativos

A opção global `SignificantDigits` funciona uniformemente para números positivos e negativos. Se quiser uma exibição diferente para negativos, combine-a com um formato personalizado:

```csharp
Style negStyle = wb.CreateStyle();
negStyle.Custom = "#,##0.###;[Red]-#,##0.###";
ws.Cells["E1"].PutValue(-9876.54321);
ws.Cells["E1"].SetStyle(negStyle);
```

## Dicas avançadas e armadilhas

* **Dica avançada:** Defina as opções de formato numérico **antes** de escrever quaisquer dados. Alterar a opção após preencher as células não reformata retroativamente os valores existentes.
* **Cuidado com:** Usar `PutValue` com uma **string** que parece um número (ex.: `"123.45"`). O Excel tratará isso como texto, e o formato personalizado não será aplicado.
* **Observação de desempenho:** Configurações globais são leves, mas aplicar um estilo a milhões de células pode aumentar o uso de memória. Use formatação ao nível de coluna sempre que possível.

## Próximos passos

Agora que você pode **personalizar o formato numérico no Excel** com dígitos significativos, pode explorar:

* **Como definir formato numérico** para datas e moedas usando `Style.Custom`.
* **Criar gráficos** que respeitem seus formatos personalizados.
* **Exportar para CSV** preservando a precisão numérica (`save workbook xlsx` → `wb.Save("file.csv", SaveFormat.Csv)`).

Esses tópicos se baseiam nos mesmos conceitos de `Workbook` e `Worksheet` demonstrados aqui.

---

**Resumo**

Você aprendeu como **personalizar o formato numérico no Excel** configurando `NumberFormatOptions` para **definir dígitos significativos**, criando uma pasta de trabalho Excel em C#, inserindo valores e **salvando a pasta de trabalho como um arquivo XLSX**. O código completo e executável acima mostra cada passo, explica por que cada parte é necessária e oferece dicas para variações comuns. Sinta‑se à vontade para adaptar os trechos ao seu projeto e experimentar outros cenários de formatação.

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [Custom Number Format Excel in C# – Complete Guide](/cells/english/net/excel-custom-number-date-formatting/custom-number-format-excel-in-c-complete-guide/)
- [Create Excel Workbook C# – Limit Significant Digits Excel](/cells/english/net/excel-custom-number-date-formatting/create-excel-workbook-c-limit-significant-digits-excel/)
- [How to apply number format excel with Aspose.Cells](/cells/english/net/excel-custom-number-date-formatting/how-to-apply-number-format-excel-with-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}