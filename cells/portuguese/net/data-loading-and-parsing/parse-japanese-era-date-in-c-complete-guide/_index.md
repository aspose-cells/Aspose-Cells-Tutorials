---
category: general
date: 2026-06-27
description: Aprenda a analisar datas de era japonesa em C# e, em seguida, formatar
  datetime yyyy‑mm‑dd para saída ISO. Código passo a passo, casos limites e dicas.
draft: false
keywords:
- parse japanese era date
- format datetime yyyy-mm-dd
- C# JapaneseCalendar
- CultureInfo date parsing
- .NET DateTime era handling
language: pt
og_description: Analise datas de era japonesa em C# e formate datetime yyyy-mm-dd
  sem esforço. Exemplo completo com explicações e armadilhas.
og_title: Analisar data de era japonesa em C# – Tutorial completo de programação
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Learn how to parse Japanese era date in C# and then format datetime
    yyyy-mm-dd for ISO output. Step‑by‑step code, edge cases, and tips.
  headline: Parse Japanese era date in C# – Complete Guide
  type: TechArticle
- description: Learn how to parse Japanese era date in C# and then format datetime
    yyyy-mm-dd for ISO output. Step‑by‑step code, edge cases, and tips.
  name: Parse Japanese era date in C# – Complete Guide
  steps:
  - name: Multiple Eras
    text: Japan has gone through several eras (Meiji, Taishō, Shōwa, Heisei, Reiwa).
      The `JapaneseCalendar` automatically maps them, so `"H30-12-31"` (Heisei 30)
      becomes `2018-12-31`. Just keep the same parsing logic; the calendar does the
      heavy lifting.
  - name: Invalid Input
    text: 'If a string doesn’t match the expected pattern, `Parse` throws. Use `TryParseExact`
      as shown earlier, or pre‑validate with a regular expression:'
  - name: Time Zones
    text: '`DateTime` objects are “kind‑agnostic” by default. If you need a UTC timestamp,
      call:'
  type: HowTo
tags:
- C#
- .NET
- DateTime
- Localization
title: Analisar data de era japonesa em C# – Guia completo
url: /pt/net/data-loading-and-parsing/parse-japanese-era-date-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Analisar data da era japonesa em C# – Guia Completo

Já precisou **analisar data da era japonesa** em um aplicativo .NET e se perguntou por que o resultado parece errado? Você não está sozinho. Em muitos sistemas legados, as datas chegam no estilo “R3‑04‑01”, e você precisa convertê‑las para uma string **format datetime yyyy-mm-dd** limpa para APIs ou bancos de dados.  

Neste tutorial vamos percorrer passo a passo como fazer isso, explicar por que cada parte importa e mostrar como lidar com os casos limites que costumam pegar os desenvolvedores.

> **Nota:** Todo o código está pronto para copiar‑e‑colar em um console app direcionado ao .NET 6 ou superior.

## O que você vai precisar

- .NET 6 SDK (ou qualquer versão recente)
- Familiaridade básica com C# e o namespace `System.Globalization`
- Uma IDE ou editor – Visual Studio, VS Code, Rider, o que preferir

Nenhum pacote NuGet externo é necessário; tudo está na BCL.

## Etapa 1: Configurar a cultura japonesa com o calendário imperial

Primeiro, precisamos de um `CultureInfo` que conheça o calendário imperial japonês. Por padrão, `ja-JP` usa o calendário gregoriano, então substituímos seu `DateTimeFormat.Calendar` por uma instância de `JapaneseCalendar`.

```csharp
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // Step 1: Create a Japanese culture and switch to the Japanese imperial calendar
        CultureInfo japaneseCulture = new CultureInfo("ja-JP");
        japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();

        // (The rest of the code follows...)
```

> **Por que isso importa:** O `JapaneseCalendar` traduz símbolos de era (como “R” para Reiwa) para o ano gregoriano correto. Sem ele, `DateTime.Parse` lançaria uma `FormatException`.

## Etapa 2: Analisar a string de data baseada em era

Agora podemos passar uma string como `"R3-04-01"` para `DateTime.Parse`. A cultura que configuramos informa ao analisador como interpretar a parte “R3”.

```csharp
        // Step 2: Parse a date string that uses the Japanese era format (e.g., "R3-04-01")
        string eraDate = "R3-04-01";
        DateTime parsedDate = DateTime.Parse(eraDate, japaneseCulture);
```

Se preferir uma abordagem mais segura que evite exceções em entradas inválidas, troque `Parse` por `TryParseExact`:

```csharp
        // Safer alternative with TryParseExact
        if (DateTime.TryParseExact(
                eraDate,
                "ggy-MM-dd",               // ggy = era+year, MM = month, dd = day
                japaneseCulture,
                DateTimeStyles.None,
                out DateTime safeDate))
        {
            parsedDate = safeDate;
        }
        else
        {
            Console.WriteLine("Unable to parse the Japanese era date.");
            return;
        }
```

> **Dica profissional:** A string de formato personalizada `"ggy-MM-dd"` diz ao analisador exatamente o que esperar. “gg” é o designador de era, “y” o ano dentro daquela era.

## Etapa 3: Converter o resultado para ISO 8601 (`format datetime yyyy-mm-dd`)

Por fim, exibimos o `DateTime` em um formato ISO padrão. O especificador de formato `"yyyy-MM-dd"` faz exatamente isso.

```csharp
        // Step 3: Display the parsed date in a standard ISO format
        string isoDate = parsedDate.ToString("yyyy-MM-dd", CultureInfo.InvariantCulture);
        Console.WriteLine(isoDate); // Expected output: 2021-04-01
    }
}
```

Executando o programa, a saída será:

```
2021-04-01
```

Esse é o **format datetime yyyy-mm-dd** que você precisava, pronto para payloads JSON, inserções SQL ou qualquer sistema downstream.

![parse japanese era date example](placeholder.png){alt="exemplo de análise de data da era japonesa"}

## Tratamento de outras eras e casos limites

### Múltiplas Eras

O Japão passou por várias eras (Meiji, Taishō, Shōwa, Heisei, Reiwa). O `JapaneseCalendar` mapeia‑as automaticamente, então `"H30-12-31"` (Heisei 30) torna‑se `2018-12-31`. Basta manter a mesma lógica de análise; o calendário faz o trabalho pesado.

### Entrada inválida

Se uma string não corresponder ao padrão esperado, `Parse` lança exceção. Use `TryParseExact` como mostrado antes, ou pré‑valide com uma expressão regular:

```csharp
bool IsValidEraDate(string input) =>
    System.Text.RegularExpressions.Regex.IsMatch(
        input, @"^[RHS][0-9]+-\d{2}-\d{2}$", System.Text.RegularExpressions.RegexOptions.IgnoreCase);
```

### Fusos horários

Objetos `DateTime` são “agnósticos quanto ao tipo” por padrão. Se precisar de um timestamp UTC, chame:

```csharp
DateTime utc = DateTime.SpecifyKind(parsedDate, DateTimeKind.Utc);
```

Ou use `DateTimeOffset` para total consciência de fuso horário.

## Exemplo completo funcional

Aqui está o trecho completo que você pode inserir em um novo projeto de console:

```csharp
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // Initialize Japanese culture with the imperial calendar
        CultureInfo japaneseCulture = new CultureInfo("ja-JP");
        japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();

        // The era‑based date you want to convert
        string eraDate = "R3-04-01";

        // Try parsing – safer than Parse when input may be malformed
        if (!DateTime.TryParseExact(
                eraDate,
                "ggy-MM-dd",
                japaneseCulture,
                DateTimeStyles.None,
                out DateTime parsedDate))
        {
            Console.WriteLine("Failed to parse the Japanese era date.");
            return;
        }

        // Convert to ISO 8601 (format datetime yyyy-mm-dd)
        string isoDate = parsedDate.ToString("yyyy-MM-dd", CultureInfo.InvariantCulture);
        Console.WriteLine($"Original era date: {eraDate}");
        Console.WriteLine($"Converted ISO date: {isoDate}");
    }
}
```

**Saída esperada no console**

```
Original era date: R3-04-01
Converted ISO date: 2021-04-01
```

## Recapitulação

Cobremos como **analisar datas da era japonesa** ao:

1. Criar um `CultureInfo` para `ja-JP` e substituir o calendário por `JapaneseCalendar`.
2. Usar `DateTime.Parse` ou o mais robusto `TryParseExact` com um formato personalizado.
3. Formatar o `DateTime` resultante com `"yyyy-MM-dd"` para obter o desejado **format datetime yyyy-mm-dd**.

Isso é tudo que você precisa para conectar dados legados de era japonesa a sistemas modernos compatíveis com ISO.

## O que vem a seguir?

- **Processamento em lote:** Percorra um CSV de datas de era e grave strings ISO em um banco de dados.
- **Localização:** Converta datas ISO de volta para o formato de era para exibição na UI (`ToString("ggyy年MM月dd日", japaneseCulture)`).
- **Calendários personalizados:** Explore `TaiwanCalendar` ou `HijriCalendar` para outras necessidades regionais.

Sinta‑se à vontade para experimentar – troque a string de era, teste casos limites ou integre essa lógica em endpoints ASP.NET Core. Se encontrar algum obstáculo, deixe um comentário abaixo; feliz codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [How to Implement Date Validation in .NET Using Aspose.Cells: A Comprehensive Guide](/cells/english/net/data-validation/implement-date-validation-net-aspose-cells/)
- [Change Excel Date System to 1904 using Aspose.Cells .NET](/cells/english/net/calculation-engine/change-excel-date-system-aspose-cells-net/)
- [How to Implement and Format Excel Comments Using Aspose.Cells for .NET: A Step‑By‑Step Guide](/cells/english/net/comments-annotations/implement-format-excel-comments-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}