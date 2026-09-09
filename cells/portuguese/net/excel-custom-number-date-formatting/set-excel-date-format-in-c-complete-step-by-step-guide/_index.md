---
category: general
date: 2026-02-28
description: Aprenda como definir o formato de data do Excel, ler data/hora do Excel,
  extrair a data do Excel e calcular fórmulas da pasta de trabalho usando Aspose.Cells
  em C#. Exemplo completo e executável.
draft: false
keywords:
- set excel date format
- read excel datetime
- extract date from excel
- calculate workbook formulas
- get datetime cell
language: pt
og_description: Domine a configuração de formato de data no Excel, a leitura de datetime
  no Excel, a extração de datas e o cálculo de fórmulas da planilha com um exemplo
  completo em C#.
og_title: definir formato de data do Excel em C# – Guia completo passo a passo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Definir formato de data do Excel em C# – Guia completo passo a passo
url: /pt/net/excel-custom-number-date-formatting/set-excel-date-format-in-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# definir formato de data no Excel – Guia Completo em C#

Já teve dificuldade em **definir o formato de data no Excel** ao gerar planilhas dinamicamente? Você não está sozinho. Muitos desenvolvedores se deparam com o problema quando a célula exibe uma string bruta em vez de uma data correta, especialmente com datas de era japonesa ou strings de localidade personalizadas.  

Neste tutorial, percorreremos um exemplo real que **define o formato de data no Excel**, depois **lê o datetime do Excel**, **extrai a data do Excel**, e ainda **calcula fórmulas da pasta de trabalho** para que você possa, finalmente, **obter valores de célula datetime** como objetos nativos .NET `DateTime`. Sem referências externas, apenas um trecho autocontido e executável que você pode colar no Visual Studio e ver funcionando instantaneamente.

## O que você precisará

- **Aspose.Cells for .NET** (qualquer versão recente; a API usada aqui funciona com 23.x e superior)  
- .NET 6 ou superior (o código também compila com .NET Framework 4.6+)  
- Um entendimento básico da sintaxe C# – se você consegue escrever `Console.WriteLine`, está pronto.

É isso. Nenhum pacote NuGet extra além do Aspose.Cells, sem necessidade de instalação do Excel.

## Como definir o formato de data no Excel em C#

A primeira coisa que fazemos é informar ao Excel que a célula contém uma data, não apenas texto. Aspose.Cells fornece um ID de formato numérico embutido (`14`) que corresponde ao padrão de data curta da localidade atual.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // Step 2: Write a Japanese era date string into cell A1
        sheet.Cells["A1"].PutValue("Reiwa 2-04-01");

        // Step 3: Apply the standard date number format (ID 14) to A1
        // This tells Excel to treat the cell as a date.
        sheet.Cells["A1"].Style.Number = 14;

        // Step 4: Force Excel to recalculate formulas so the value is parsed
        workbook.CalculateFormula();

        // Step 5: Retrieve the parsed value as a .NET DateTime
        DateTime parsedDate = sheet.Cells["A1"].GetDateTime();

        // Step 6: Show the result – should be 2020‑04‑01
        Console.WriteLine($"Parsed DateTime: {parsedDate:yyyy-MM-dd}");
    }
}
```

> **Dica profissional:** A chamada `CalculateFormula()` é crucial. Sem ela, a célula ainda contém a string bruta, e `GetDateTime()` lançaria uma exceção. Esta linha força o Aspose.Cells a executar seu analisador interno, efetivamente **calculando as fórmulas da pasta de trabalho** para nós.

A saída que você verá ao executar o programa é:

```
Parsed DateTime: 2020-04-01
```

Isso confirma que definimos com sucesso o **formato de data no Excel**, e conseguimos **obter a célula datetime** como um `DateTime` adequado.

## Lendo valores datetime do Excel  

Agora que a data está armazenada corretamente, você pode se perguntar como recuperá‑la depois, talvez de um arquivo existente. O mesmo método `GetDateTime()` funciona em qualquer célula que já possui um formato de data.

```csharp
// Assuming 'sheet' is already loaded from an existing workbook
DateTime existingDate = sheet.Cells["B5"].GetDateTime();
Console.WriteLine($"Cell B5 contains: {existingDate:d}");
```

Se a célula não estiver formatada como data, `GetDateTime()` retorna `DateTime.MinValue`. Por isso sempre **definimos o formato de data no Excel** primeiro.

## Extraindo a data de células do Excel  

Às vezes a célula contém um timestamp completo (data + hora), mas você precisa apenas da parte da data. Você pode truncar o componente de hora usando `.Date` no `DateTime` retornado.

```csharp
DateTime fullStamp = sheet.Cells["C3"].GetDateTime(); // e.g., 2023-07-15 14:30:00
DateTime onlyDate = fullStamp.Date;                  // 2023-07-15 00:00:00
Console.WriteLine($"Date only: {onlyDate:yyyy-MM-dd}");
```

Esta abordagem funciona independentemente do formato numérico subjacente do Excel, contanto que a célula seja reconhecida como data.

## Calculando fórmulas da pasta de trabalho  

E se a data for o resultado de uma fórmula, como `=TODAY()` ou `=DATE(2022,5,10)`? Aspose.Cells avaliará a fórmula quando você chamar `CalculateFormula()`. Depois disso, a célula se comporta exatamente como uma data inserida manualmente.

```csharp
sheet.Cells["D2"].Formula = "=TODAY()";
workbook.CalculateFormula(); // Re‑evaluate the sheet
DateTime today = sheet.Cells["D2"].GetDateTime();
Console.WriteLine($"Today is: {today:yyyy-MM-dd}");
```

Observe que não foi necessário alterar o estilo da célula; o Excel já trata resultados de fórmulas como datas quando a fórmula retorna um número serial que corresponde a uma data.

## Obtendo uma célula datetime de uma pasta de trabalho existente  

Juntando tudo, aqui está uma rotina compacta que você pode inserir em qualquer projeto para abrir um arquivo Excel, garantir que todas as células de data sejam interpretadas corretamente e devolver uma lista de objetos `DateTime`.

```csharp
using System.Collections.Generic;
using Aspose.Cells;

static List<DateTime> ExtractAllDates(string filePath)
{
    Workbook wb = new Workbook(filePath);
    Worksheet ws = wb.Worksheets[0];
    wb.CalculateFormula(); // Make sure formulas are evaluated

    var dates = new List<DateTime>();
    foreach (Cell cell in ws.Cells)
    {
        // Check if the cell has a date number format (ID 14‑22 are common date formats)
        if (cell.GetStyle().Number >= 14 && cell.GetStyle().Number <= 22)
        {
            dates.Add(cell.GetDateTime());
        }
    }
    return dates;
}
```

Executar `ExtractAllDates("Sample.xlsx")` fornecerá todas as datas que foram **definidas com o formato de data no Excel** corretamente na primeira planilha.

## Armadilhas comuns e como evitá‑las  

| Problema | Por que acontece | Correção |
|----------|------------------|----------|
| `GetDateTime()` throws `ArgumentException` | A célula não é reconhecida como data (formato numérico ausente) | Aplique `Style.Number = 14` **antes** de chamar `CalculateFormula()` |
| Date appears as `1900‑01‑00` | O número serial 0 do Excel é interpretado como a época | Garanta que a célula realmente contenha um serial válido (>0) |
| Japanese era strings don’t parse | Aspose.Cells só analisa strings de era após `CalculateFormula()` | Mantenha a string bruta, defina um formato de data e então chame `CalculateFormula()` |
| Time zone shifts | `DateTime` é armazenado sem informação de fuso horário, mas seu aplicativo pode exibir em uma localidade diferente | Use `DateTimeKind.Utc` ou converta explicitamente se necessário |

## Imagem – Resumo Visual  

![exemplo de definição de formato de data no Excel](excel-date-format.png "exemplo de definição de formato de data no Excel")

O diagrama ilustra o fluxo: **escrever string → aplicar formato numérico → recalcular → recuperar DateTime**.

## Conclusão  

Cobrimos tudo o que você precisa para **definir o formato de data no Excel**, **ler datetime do Excel**, **extrair a data do Excel**, **calcular fórmulas da pasta de trabalho**, e finalmente **obter valores de célula datetime** como objetos .NET nativos. O código completo e executável está pronto para copiar‑colar, e as explicações fornecem o “porquê” de cada etapa, permitindo que você adapte o padrão a cenários mais complexos.

### O que vem a seguir?

- **Importação/exportação em massa:** Use o helper `ExtractAllDates` para processar em lote grandes relatórios.  
- **Formatos de data personalizados:** Substitua `Style.Number = 14` por `Style.Custom = "yyyy/mm/dd"` para formatação independente de localidade.  
- **Datas sensíveis a fuso horário:** Combine `DateTimeOffset` com os números seriais do Excel para aplicações globais.

Sinta‑se à vontade para experimentar, adicionar formatação condicional ou inserir as datas em um banco de dados. Se encontrar algum problema, deixe um comentário — feliz codificação!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}