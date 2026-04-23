---
category: general
date: 2026-02-14
description: Analise datas de era japonesa no Excel com análise de data personalizada.
  Aprenda como carregar a pasta de trabalho a partir de um arquivo usando load excel
  com opções e evite armadilhas comuns.
draft: false
keywords:
- parse japanese era dates
- load excel with options
- load workbook from file
- custom date parsing excel
language: pt
og_description: Analise datas de eras japonesas no Excel usando Aspose.Cells. Este
  guia mostra como carregar a pasta de trabalho a partir de um arquivo com opções
  personalizadas de análise de datas.
og_title: Analisar datas de eras japonesas – Tutorial C# passo a passo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Analisar datas de eras japonesas no Excel – Guia completo para desenvolvedores
  C#
url: /pt/net/data-loading-and-parsing/parse-japanese-era-dates-in-excel-full-guide-for-c-developer/
---

final output with same structure.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Analisar Datas de Era Japonesa – Tutorial Completo em C#

Já precisou **analisar datas de era japonesa** de uma planilha Excel e se perguntou por que os valores continuam se transformando em números estranhos? Você não está sozinho. Muitos desenvolvedores encontram esse problema quando o analisador padrão `DateTime` não reconhece o estilo “Reiwa 1/04/01” usado nos calendários japoneses.  

Boa notícia: você pode instruir o Aspose.Cells a tratar essas células como datas de era japonesa desde o momento em que **carrega o Excel com opções**. Neste guia, vamos percorrer o carregamento de uma pasta de trabalho a partir de um arquivo, configurar a análise de datas personalizada e verificar se as datas são retornadas exatamente como você espera.

Ao final deste tutorial, você será capaz de:

* Carregar uma pasta de trabalho a partir de um arquivo especificando `DateTimeParsing.JapaneseEra`.
* Acessar valores de células como objetos `DateTime` adequados.
* Lidar com casos extremos, como células vazias ou calendários mistos.
* Estender a abordagem para qualquer cenário **custom date parsing excel** que você possa encontrar.

> **Pré-requisito** – Você precisa da biblioteca Aspose.Cells for .NET (v23.9 ou posterior) e de uma IDE compatível com .NET (Visual Studio, Rider, etc.). Nenhum outro pacote é necessário.

---

## Etapa 1: Configurar Opções de Carregamento de Texto para Análise de Era Japonesa  

A primeira coisa que fazemos é instruir o carregador sobre como interpretar texto que parece uma data de era japonesa. Isso é feito via `TxtLoadOptions` e o enum `DateTimeParsing`.

```csharp
using Aspose.Cells;

// Step 1: Set up load options to understand Japanese era dates
TxtLoadOptions loadOptions = new TxtLoadOptions
{
    // This flag makes the parser treat “R1/04/01” as 2024‑04‑01, etc.
    DateTimeParsing = DateTimeParsing.JapaneseEra
};
```

**Por que isso importa:** Sem a flag `JapaneseEra`, o Aspose.Cells trata a célula como uma string simples, deixando você dividir manualmente o nome da era e convertê-lo. A flag faz o trabalho pesado, mantendo seu código limpo e menos propenso a erros.

---

## Etapa 2: Carregar Pasta de Trabalho a partir de Arquivo Usando as Opções  

Agora realmente abrimos o arquivo Excel. Observe como o objeto `loadOptions` é passado ao construtor `Workbook` — esta é a etapa de **load workbook from file** que respeita nossas regras de análise personalizadas.

```csharp
// Step 2: Load the workbook with the configured options
string filePath = Path.Combine(Environment.CurrentDirectory, "japan_dates.xlsx");
Workbook workbook = new Workbook(filePath, loadOptions);
```

Se o arquivo estiver em outro local (por exemplo, um compartilhamento de rede), basta ajustar `filePath` adequadamente. A parte importante é que a mesma instância `loadOptions` seja usada; caso contrário, a conversão de era japonesa não ocorrerá.

---

## Etapa 3: Acessar as Datas Analisadas  

Com a pasta de trabalho carregada, você pode obter valores de células exatamente como faria com qualquer data normal. A API retorna automaticamente um objeto `DateTime`.

```csharp
// Step 3 (optional): Read a date from the first worksheet, cell A1
Worksheet sheet = workbook.Worksheets[0];
Cell dateCell = sheet.Cells["A1"];

// The Value property is already a DateTime because of our parsing option
DateTime parsedDate = dateCell.DateTimeValue;

// Quick sanity check – print to console
Console.WriteLine($"Parsed date from A1: {parsedDate:yyyy-MM-dd}");
```

**Saída esperada** (supondo que A1 contenha “R1/04/01”):

```
Parsed date from A1: 2024-04-01
```

Se a célula contiver uma data gregoriana como “2023‑12‑31”, o analisador ainda funciona — ele simplesmente retorna a data original sem alterações.

---

## Etapa 4: Verificar Todas as Datas em uma Coluna  

Frequentemente você precisa percorrer uma coluna inteira de datas de era japonesa. Abaixo está um loop compacto que mostra como lidar com células vazias e conteúdo misto de forma elegante.

```csharp
// Step 4: Iterate through column B (index 1) and print each parsed date
int firstRow = 0;
int lastRow = sheet.Cells.MaxDataRow; // last row with data

for (int row = firstRow; row <= lastRow; row++)
{
    Cell cell = sheet.Cells[row, 1]; // column B
    if (cell.Type == CellValueType.IsDateTime)
    {
        Console.WriteLine($"Row {row + 1}: {cell.DateTimeValue:yyyy-MM-dd}");
    }
    else if (!cell.IsNull)
    {
        // Fallback: show raw string for non‑date cells
        Console.WriteLine($"Row {row + 1}: (non‑date) {cell.StringValue}");
    }
}
```

**Dica profissional:** `CellValueType.IsDateTime` é a maneira mais segura de verificar se o analisador teve sucesso. Ele protege você de `InvalidCastException` quando uma célula contém texto inesperado.

---

## Etapa 5: Armadilhas Comuns & Como Lidiar com Elas  

| Problema | Por que acontece | Correção |
|----------|------------------|----------|
| **Células vazias retornam `DateTime.MinValue`** | O analisador trata strings vazias como a data mínima. | Verifique `cell.IsNull` antes de acessar `DateTimeValue`. |
| **Calendários mistos (Japonês + Gregoriano) na mesma coluna** | O analisador lida com ambos, mas pode ser necessário diferenciar para relatórios. | Use `cell.StringValue` para inspecionar o texto original quando `cell.Type` for `IsString`. |
| **Era incorreta (ex.: “H30” para Heisei) após 2019** | Heisei terminou em 2019; datas posteriores devem usar “R”. | Valide o prefixo da era antes de confiar no resultado analisado. |
| **Desempenho reduzido em arquivos grandes** | Carregar com opções personalizadas adiciona uma pequena sobrecarga. | Carregue apenas as planilhas necessárias (`Workbook.LoadOptions.LoadAllWorksheets = false`). |

---

## Etapa 6: Exemplo Completo em Funcionamento  

Juntando tudo, aqui está um aplicativo de console autônomo que você pode copiar‑colar e executar. Ele demonstra **custom date parsing excel** do início ao fim.

```csharp
// FullExample.cs
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Configure load options for Japanese era dates
        TxtLoadOptions loadOptions = new TxtLoadOptions
        {
            DateTimeParsing = DateTimeParsing.JapaneseEra
        };

        // 2️⃣ Load the workbook from file with those options
        string filePath = Path.Combine(Environment.CurrentDirectory, "japan_dates.xlsx");
        if (!File.Exists(filePath))
        {
            Console.WriteLine($"File not found: {filePath}");
            return;
        }

        Workbook workbook = new Workbook(filePath, loadOptions);
        Worksheet sheet = workbook.Worksheets[0];

        // 3️⃣ Read a single cell (A1) – demonstrates automatic parsing
        Cell a1 = sheet.Cells["A1"];
        Console.WriteLine($"A1 raw value: {a1.StringValue}");
        Console.WriteLine($"A1 parsed date: {a1.DateTimeValue:yyyy-MM-dd}");

        // 4️⃣ Loop through column B to show batch parsing
        Console.WriteLine("\n--- Column B Dates ---");
        int lastRow = sheet.Cells.MaxDataRow;
        for (int row = 0; row <= lastRow; row++)
        {
            Cell cell = sheet.Cells[row, 1]; // B column
            if (cell.Type == CellValueType.IsDateTime)
                Console.WriteLine($"Row {row + 1}: {cell.DateTimeValue:yyyy-MM-dd}");
            else if (!cell.IsNull)
                Console.WriteLine($"Row {row + 1}: (non‑date) {cell.StringValue}");
        }

        // 5️⃣ Optional: Save a copy with dates converted to ISO format
        // This shows that the workbook now holds proper DateTime objects.
        workbook.Save("japan_dates_converted.xlsx");
        Console.WriteLine("\nWorkbook saved as japan_dates_converted.xlsx");
    }
}
```

**O que você deve ver** quando `japan_dates.xlsx` contém:

| A | B |
|---|---|
| R1/04/01 | 2023‑12‑31 |
| H30/12/31 | R2/01/01 |
| (blank) | R2/02/15 |

Saída no console:

```
A1 raw value: R1/04/01
A1 parsed date: 2024-04-01

--- Column B Dates ---
Row 1: 2023-12-31
Row 2: 2025-01-01
Row 3: (non-date) 
Row 4: 2025-02-15
Workbook saved as japan_dates_converted.xlsx
```

O arquivo salvo agora armazena células de data corretas, que você pode abrir no Excel e ver a formatação de data usual.

---

## Conclusão  

Acabamos de mostrar como **analisar datas de era japonesa** no Excel configurando `TxtLoadOptions`, **load workbook from file** com essas opções e trabalhando com os valores `DateTime` resultantes. O mesmo padrão — definir flags de análise personalizadas e então carregar a pasta de trabalho — se aplica a qualquer necessidade de **custom date parsing excel**, seja lidando com períodos fiscais, números de semana ISO ou formatos proprietários.

Tem uma era diferente ou uma planilha de calendário misto? Basta trocar `DateTimeParsing.JapaneseEra` por outro valor de enum (por exemplo, `DateTimeParsing.Custom`) e fornecer uma string de formato. A flexibilidade do Aspose.Cells significa que raramente você precisará escrever código de conversão manual novamente.

**Próximos passos** que você pode explorar:

* **Load Excel with options** para arquivos CSV (`CsvLoadOptions`) para lidar com separadores específicos de localidade.
* Use `Workbook.Save` com `SaveFormat.Xlsx` para exportar dados limpos.
* Combine esta abordagem com **Aspose.Slides** ou **Aspose.Words** para pipelines de relatórios.

Experimente, ajuste as opções e deixe a biblioteca fazer o trabalho pesado. Feliz codificação!  

![Captura de tela das datas de era japonesa analisadas em uma janela de console – exemplo de parse japanese era dates](/images/parse-japanese-era-dates.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}