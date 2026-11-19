---
category: general
date: 2026-11-19
description: Defina o formato numérico da célula em C# e aprenda a aplicar o formato
  de data do Excel para datas da era japonesa, possibilitando uma conversão confiável
  de datas do Excel em C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set cell number format
- apply excel date format
- c# excel date conversion
- japanese era date excel
- aspose.cells date handling
language: pt
lastmod: 2026-11-19
og_description: Defina o formato numérico da célula em C# e aplique o formato de data
  do Excel às datas da era japonesa. Siga este guia completo para uma conversão precisa
  de datas do Excel em C#.
og_image_alt: Screenshot showing a C# code editor with set cell number format applied
  to an Excel cell
og_title: Defina o formato numérico da célula e converta datas japonesas em C# – guia
  passo a passo
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Set cell number format in C# and learn how to apply Excel date format
    for Japanese era dates, enabling reliable C# Excel date conversion.
  headline: Set cell number format and convert Japanese dates in C#
  type: TechArticle
- description: Set cell number format in C# and learn how to apply Excel date format
    for Japanese era dates, enabling reliable C# Excel date conversion.
  name: Set cell number format and convert Japanese dates in C#
  steps:
  - name: Why this works
    text: '* `Style.Number = 14` maps to Excel’s *Short Date* format (`mm/dd/yyyy`
      by default). * When the cell contains a Japanese era string like `R3/04/01`,
      Aspose.Cells’ internal parser recognises the era and converts it to the corresponding
      Gregorian serial number during `CalculateFormula()`. * After the '
  - name: When to use a custom format
    text: '* Reports intended for Japanese audiences. * When you need to preserve
      the original era information for legal documents. * In dashboards where both
      Gregorian and era dates are shown side‑by‑side.'
  - name: Full end‑to‑end example
    text: Below is a self‑contained program that demonstrates both the Gregorian and
      era outputs in one run.
  - name: Edge cases & common pitfalls
    text: '| Situation | What to watch for | Fix / Recommendation | |----------------------------------------|------------------------------------------------------|----------------------------------------------------------|
      | Empty or malformed era string | `PutValue` stores the literal text; conversion
      fails'
  - name: Automation tip
    text: 'If you need to process a large range of era dates (e.g., column A contains
      many Japanese dates), wrap the conversion logic in a loop:'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
- Date conversion
title: Definir o formato numérico da célula e converter datas japonesas em C#
url: /pt/net/excel-custom-number-date-formatting/set-cell-number-format-and-convert-japanese-dates-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Definir formato numérico da célula e converter datas japonesas em C#

Se você precisar **definir formato numérico da célula** em um projeto de automação Excel em C#, este guia mostra como **aplicar formato de data do Excel** e realizar **conversão de data Excel em C#** para datas de era japonesa. Você obterá um exemplo completo e executável que converte uma string da era Reiwa (por exemplo, `R3/04/01`) na data gregoriana `2021‑04‑01`.

## O que você aprenderá

* Como criar uma pasta de trabalho e acessar sua primeira planilha.  
* Como **definir formato numérico da célula** para que o Excel trate o valor como uma data.  
* Como **aplicar formato de data do Excel** que reconhece strings de era japonesa.  
* Como disparar **conversão de data Excel em C#** recalculando fórmulas.  
* Saída esperada e dicas de solução de problemas para casos extremos.

**Pré-requisitos**

* .NET 6 ou posterior (o código também funciona com .NET Framework 4.6+).  
* Aspose.Cells para .NET 2024 ou mais recente – instale via NuGet: `dotnet add package Aspose.Cells`.  
* Familiaridade básica com C# e manipulação de datas no Excel.

> **Dica profissional:** Aspose.Cells funciona sem o Microsoft Office instalado, tornando‑o ideal para automação no lado do servidor.

## Definir formato numérico da célula com Aspose.Cells em C#

O primeiro passo é informar ao Excel que a célula contém uma data. O Excel armazena datas como números seriais, portanto precisamos aplicar um formato numérico de data interno (ID 14) à célula alvo.

```csharp
using System;
using Aspose.Cells;

class JapaneseEraDateDemo
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // 2️⃣ Insert a Japanese era date string (Reiwa 3) into cell A1
        sheet.Cells["A1"].PutValue("R3/04/01");

        // 3️⃣ **Set cell number format** – use built‑in date format ID 14
        //    This tells Excel to treat the string as a date value.
        sheet.Cells["A1"].Style.Number = 14;

        // 4️⃣ Recalculate formulas so the internal date engine converts the era.
        workbook.CalculateFormula();

        // 5️⃣ Output the converted Gregorian date.
        Console.WriteLine(sheet.Cells["A1"].StringValue); // → 2021-04-01
    }
}
```

### Por que isso funciona

* `Style.Number = 14` corresponde ao formato *Data Curta* do Excel (`mm/dd/yyyy` por padrão).  
* Quando a célula contém uma string de era japonesa como `R3/04/01`, o analisador interno do Aspose.Cells reconhece a era e a converte para o número serial gregoriano correspondente durante `CalculateFormula()`.  
* Após o cálculo, `StringValue` retorna a data gregoriana formatada.

## Aplicar formato de data do Excel para datas de era japonesa

Se você quiser que a célula exiba a era japonesa em vez da data gregoriana, pode usar um formato numérico personalizado que inclua o código da era. Isso demonstra a capacidade de **aplicar formato de data do Excel**.

```csharp
// Apply a custom format that forces the Japanese era display
sheet.Cells["A1"].Style.Custom = "[$-ja-JP]ggge\"年\"m\"月\"d\"日\"";

// Recalculate to apply the custom format
workbook.CalculateFormula();

// Output the era‑styled string
Console.WriteLine(sheet.Cells["A1"].StringValue); // → R3年04月01日
```

* `[$-ja-JP]` força a localidade japonesa.  
* `ggg` representa o nome da era (por exemplo, `R` para Reiwa).  
* Adicionar caracteres literais (`年`, `月`, `日`) cria um layout de data japonês familiar.

### Quando usar um formato personalizado

* Relatórios destinados a públicos japoneses.  
* Quando for necessário preservar a informação original da era para documentos legais.  
* Em painéis onde datas gregorianas e de era são exibidas lado a lado.

## Conversão de data Excel em C# – lidando com eras japonesas

O processo de **conversão de data Excel em C#** pode ser dividido em três partes lógicas:

1. **Analisar a string da era** – Aspose.Cells reconhece automaticamente `R` (Reiwa), `H` (Heisei), `S` (Showa), etc.  
2. **Converter para um número serial** – O Excel armazena datas como dias desde 30‑12‑1899.  
3. **Formatar o número serial** – seja com um formato interno (ID 14) ou um formato japonês personalizado.

### Exemplo completo de ponta a ponta

Abaixo está um programa autônomo que demonstra tanto a saída gregoriana quanto a de era em uma única execução.

```csharp
using System;
using Aspose.Cells;

class JapaneseEraConversion
{
    static void Main()
    {
        // Create workbook and worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        // Input: Reiwa 3 (2021) – can be any era string
        ws.Cells["A1"].PutValue("R3/04/01");

        // ---- Part 1: Gregorian output ----
        ws.Cells["A1"].Style.Number = 14;      // built‑in short date
        wb.CalculateFormula();                // forces conversion
        string gregorian = ws.Cells["A1"].StringValue;
        Console.WriteLine($"Gregorian: {gregorian}"); // 2021-04-01

        // ---- Part 2: Japanese era output ----
        ws.Cells["B1"].PutValue("R3/04/01");   // repeat input for clarity
        ws.Cells["B1"].Style.Custom = "[$-ja-JP]ggge\"年\"m\"月\"d\"日\"";
        wb.CalculateFormula();
        string era = ws.Cells["B1"].StringValue;
        Console.WriteLine($"Japanese era: {era}"); // R3年04月01日
    }
}
```

**Saída esperada no console**

```
Gregorian: 2021-04-01
Japanese era: R3年04月01日
```

### Casos extremos e armadilhas comuns

| Situação                              | O que observar                                   | Correção / Recomendação                                   |
|---------------------------------------|--------------------------------------------------|-----------------------------------------------------------|
| String de era vazia ou malformada    | `PutValue` armazena o texto literal; a conversão falha | Valide a entrada com uma expressão regular antes de gravar na célula. |
| Incompatibilidade de localidade       | O formato personalizado mostra dígitos ocidentais em vez de caracteres japoneses | Garanta que o formato `Custom` inclua `[$-ja-JP]` ou defina `Workbook.Settings.CultureInfo` para `ja-JP`. |
| A pasta de trabalho contém fórmulas que referenciam a célula de data | A recalculação pode sobrescrever os resultados das fórmulas | Chame `CalculateFormula` **depois** de todas as etapas de formatação, ou use `Workbook.CalculateFormula(FormulaCalculationOptions.IgnoreError)` se precisar ignorar erros. |
| Uso de versões antigas do Aspose.Cells | O suporte a eras japonesas foi adicionado no 3º trimestre de 2022 | Atualize para o pacote NuGet mais recente.                     |

## Testando a solução

1. **Execute o programa** a partir do Visual Studio ou `dotnet run`.  
2. Verifique se o console exibe a data gregoriana `2021‑04‑01` e a string de era `R3年04月01日`.  
3. Abra a pasta de trabalho gerada (se você adicionar `wb.Save("Demo.xlsx");`) no Microsoft Excel para ver a mesma formatação aplicada às células.

### Dica de automação

Se precisar processar um grande intervalo de datas de era (por exemplo, a coluna A contém muitas datas japonesas), envolva a lógica de conversão em um loop:

```csharp
for (int row = 0; row < ws.Cells.MaxDataRow + 1; row++)
{
    var cell = ws.Cells[row, 0]; // column A
    cell.Style.Number = 14;
}
wb.CalculateFormula();
```

Essa abordagem mantém a operação de **definir formato numérico da célula** rápida e eficiente em memória.

## Conclusão

Agora você sabe como **definir formato numérico da célula** em C# usando Aspose.Cells, como **aplicar formato de data do Excel** para strings de era japonesa e como realizar uma **conversão de data Excel em C#** confiável da era para datas gregorianas. O código completo e executável demonstra ambas as saídas e destaca casos extremos comuns.  

**Próximos passos**

* Explore outros IDs de formatos internos

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [definir formato de data do Excel em C# – Guia completo passo a passo](/cells/english/net/excel-custom-number-date-formatting/set-excel-date-format-in-c-complete-step-by-step-guide/)
- [Como aplicar formato numérico no Excel com Aspose.Cells](/cells/english/net/excel-custom-number-date-formatting/how-to-apply-number-format-excel-with-aspose-cells/)
- [Como aplicar um formato numérico personalizado no Excel em C#](/cells/english/net/excel-custom-number-date-formatting/how-to-apply-a-custom-number-format-excel-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}