---
category: general
date: 2026-03-01
description: O tutorial de leitura e escrita de Excel em C# mostra como ler o valor
  de uma célula do Excel e gravar data e hora no Excel usando C# e Aspose.Cells em
  alguns passos fáceis.
draft: false
keywords:
- read write excel c#
- read excel cell value
- write datetime to excel
- c# excel interop
- aspnet excel automation
language: pt
og_description: Tutorial de leitura e escrita de Excel em C# explica como ler o valor
  de uma célula do Excel e gravar data e hora no Excel com exemplos de código claros
  e boas práticas.
og_title: Leitura e Escrita de Excel em C# – Guia Passo a Passo
tags:
- C#
- Excel
- Aspose.Cells
title: Ler e Escrever Excel C# – Guia Completo para Ler e Escrever Células do Excel
url: /pt/net/cell-operations/read-write-excel-c-complete-guide-to-reading-and-writing-exc/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Read Write Excel C# – Guia Completo para Ler e Escrever Células do Excel

Já tentou **read write Excel C#** e acabou com uma exceção críptica ou uma data incompatível? Você não está sozinho. Muitos desenvolvedores tropeçam quando precisam extrair uma data de era japonesa de uma planilha e então armazenar um `DateTime` adequado de volta na mesma célula.  

Neste guia vamos percorrer exatamente como **read excel cell value** e **write datetime to excel** usando C# e a poderosa biblioteca Aspose.Cells. Ao final, você terá um exemplo autocontido e executável que pode inserir em qualquer projeto .NET.

## O que você aprenderá

- Como instalar e referenciar Aspose.Cells em um projeto .NET 6+.
- O código exato necessário para obter uma célula que contém uma string de era japonesa como `"R3/5/12"`.
- Como analisar essa string em um `DateTime` usando a cultura `"ja-JP"`.
- Os passos para inserir o `DateTime` resultante de volta na mesma célula da planilha.
- Dicas para lidar com casos extremos, como células vazias ou formatos de era inesperados.  

Nenhuma experiência prévia com interop do Excel é necessária — apenas um entendimento básico de C# e .NET. Vamos começar.

![Screenshot of read write Excel C# operation showing cell B2 before and after conversion](read-write-excel-csharp.png "read write excel c# example")

## Etapa 1: Configurar o Projeto – Fundamentos de Read Write Excel C#  

Antes de mergulharmos no código, precisamos de uma base sólida.

1. **Create a new console app** (ou qualquer projeto .NET) direcionado ao .NET 6 ou posterior:

   ```bash
   dotnet new console -n ExcelEraDemo
   cd ExcelEraDemo
   ```

2. **Add the Aspose.Cells NuGet package**. É uma biblioteca totalmente gerenciada que funciona sem interop COM:

   ```bash
   dotnet add package Aspose.Cells
   ```

3. **Copy an Excel file** (`EraDates.xlsx`) para a raiz do projeto. Esta pasta de trabalho deve conter uma planilha chamada `"Sheet1"` com a célula **B2** contendo um valor como `"R3/5/12"` (Reiwa 3, 12 de maio).

Isso é tudo o que você precisa para a estrutura. O resto do tutorial foca na lógica real de **read excel cell value** e **write datetime to excel**.

## Etapa 2: Ler o Valor da Célula do Excel com C#

Agora que o projeto está pronto, vamos buscar a string da planilha. O trecho a seguir demonstra a cadeia de chamadas exata:

```csharp
using Aspose.Cells;
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // Load the workbook (adjust the path as needed)
        Workbook wb = new Workbook("EraDates.xlsx");
        Worksheet ws = wb.Worksheets["Sheet1"];   // assumes the sheet is named Sheet1

        // Step 2: Get the cell that holds the Japanese era date string
        // B2 contains something like "R3/5/12"
        Cell dateCell = ws.Cells["B2"];  

        // Step 3: Read the string representation from the cell
        string eraDateString = dateCell.StringValue;  

        Console.WriteLine($"Original cell value: {eraDateString}");
        // -------------------------------------------------
        // From here we’ll convert the era string to a DateTime.
        // -------------------------------------------------
    }
}
```

**Por que isso funciona:** `Cell.StringValue` sempre retorna o texto exibido, independentemente do formato numérico subjacente. Isso garante que trabalhemos com a string exata `"R3/5/12"` que o usuário vê.

### Armadilhas Comuns

- **Células vazias** – `StringValue` retorna uma string vazia. Proteja-se contra isso antes de analisar.  
- **Formatos inesperados** – Se a célula contiver `"2023/05/12"` o analisador de era lançará uma exceção; pode ser necessário um fallback.

## Etapa 3: Escrever DateTime no Excel com C#

Com a string de era em mãos, agora a analisamos usando `DateTime.ParseExact`. O formato `"ggyy/MM/dd"` indica ao .NET que espere uma era japonesa (`gg`), um ano de dois dígitos (`yy`) e componentes de mês/dia.

```csharp
        // Step 4: Convert the era date string to a DateTime using the Japanese culture
        DateTime parsedDate;
        try
        {
            parsedDate = DateTime.ParseExact(
                eraDateString,
                "ggyy/MM/dd",
                new CultureInfo("ja-JP"));
        }
        catch (FormatException)
        {
            Console.WriteLine("The cell value does not match the expected Japanese era format.");
            return;
        }

        Console.WriteLine($"Parsed DateTime (UTC): {parsedDate:u}");

        // Step 5: Store the resulting DateTime back into the same cell
        dateCell.PutValue(parsedDate);

        // Optional: Apply a standard date format so Excel shows it nicely
        dateCell.SetStyle(new Style { Number = 14 }); // 14 = "m/d/yyyy"

        // Save the workbook to a new file so we don’t overwrite the original
        wb.Save("EraDates_Converted.xlsx");
        Console.WriteLine("Workbook saved as EraDates_Converted.xlsx");
```

**Por que usamos `PutValue`**: Aspose.Cells detecta automaticamente o tipo .NET e grava o tipo de célula do Excel apropriado. Passar um `DateTime` resulta em uma data verdadeira do Excel, que pode ser formatada ou usada em fórmulas posteriores.

### Casos de Borda e Dicas

- **Fusos horários** – Objetos `DateTime` são armazenados sem informação de zona. Se precisar de UTC, chame `DateTime.SpecifyKind`.  
- **Fallback de cultura** – Se você antecipar outras culturas, envolva a análise em um helper que tente múltiplos objetos `CultureInfo`.  
- **Desempenho** – Ao processar milhares de linhas, reutilize uma única instância de `CultureInfo` em vez de criar uma nova a cada iteração.

## Etapa 4: Exemplo Completo Funcional – Juntando Tudo

Abaixo está o programa completo, pronto‑para‑executar. Copie‑e‑cole em `Program.cs`, certifique-se de que `EraDates.xlsx` esteja ao lado do binário compilado e execute `dotnet run`.

```csharp
using Aspose.Cells;
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // Load workbook
        Workbook wb = new Workbook("EraDates.xlsx");
        Worksheet ws = wb.Worksheets["Sheet1"];   // Change if your sheet has a different name

        // -------------------------------------------------
        // 1️⃣ Read the Japanese era string from B2
        // -------------------------------------------------
        Cell dateCell = ws.Cells["B2"];
        string eraDateString = dateCell.StringValue?.Trim();

        if (string.IsNullOrEmpty(eraDateString))
        {
            Console.WriteLine("Cell B2 is empty. Nothing to convert.");
            return;
        }

        Console.WriteLine($"Original cell value: {eraDateString}");

        // -------------------------------------------------
        // 2️⃣ Parse the era string into a DateTime
        // -------------------------------------------------
        DateTime parsedDate;
        try
        {
            parsedDate = DateTime.ParseExact(
                eraDateString,
                "ggyy/MM/dd",
                new CultureInfo("ja-JP"));
        }
        catch (FormatException)
        {
            Console.WriteLine("The value does not match the expected Japanese era format (ggyy/MM/dd).");
            return;
        }

        Console.WriteLine($"Parsed DateTime: {parsedDate:u}");

        // -------------------------------------------------
        // 3️⃣ Write the DateTime back into the same cell
        // -------------------------------------------------
        dateCell.PutValue(parsedDate);

        // Apply a friendly date format (e.g., 2023/05/12)
        Style style = wb.CreateStyle();
        style.Number = 14; // Built‑in date format
        dateCell.SetStyle(style);

        // Save the updated workbook
        wb.Save("EraDates_Converted.xlsx");
        Console.WriteLine("Conversion complete – saved as EraDates_Converted.xlsx");
    }
}
```

**Saída esperada**

```
Original cell value: R3/5/12
Parsed DateTime: 2021-05-12 00:00:00Z
Conversion complete – saved as EraDates_Converted.xlsx
```

Ao abrir `EraDates_Converted.xlsx`, a célula **B2** agora exibe uma data normal (por exemplo, `5/12/2021`) e pode ser usada em cálculos do Excel como qualquer outro valor de data.

## Dicas Profissionais para Código Robust Read Write Excel C#  

- **Valide antes de escrever** – Use `Cell.IsFormula` ou `Cell.Type` para evitar sobrescrever fórmulas inadvertidamente.  
- **Processamento em lote** – Se precisar converter uma coluna inteira, itere sobre `ws.Cells.Columns[1]` (coluna B) e aplique a mesma lógica.  
- **Segurança de thread** – Objetos Aspose.Cells não são thread‑safe; crie instâncias separadas de `Workbook` por thread ao paralelizar.  
- **Logging** – Para scripts de produção, substitua `Console.WriteLine` por um logger adequado (ex.: Serilog) para capturar falhas de análise.  
- **Testes** – Escreva testes unitários que alimentem strings de era conhecidas em um método helper e verifiquem os valores `DateTime` resultantes.

## Conclusão

Você acabou de dominar **read write Excel C#** aprendendo como **read excel cell value**, analisar uma string de era japonesa e **write datetime to excel** com confiança. O exemplo completo demonstra um fluxo de trabalho limpo e de ponta a ponta que você pode adaptar para operações em massa, diferentes culturas ou até pipelines Excel‑para‑banco de dados.

O que vem a seguir? Tente estender o script para processar uma coluna inteira de datas de era, ou explore as opções de formatação avançada do Aspose.Cells para estilizar as células de saída. Você também pode experimentar outras bibliotecas como EPPlus ou ClosedXML — a maior parte da lógica permanece a mesma, apenas as chamadas de API diferem.

Tem perguntas ou um cenário complicado de Excel? Deixe um comentário abaixo, e feliz codificação!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}