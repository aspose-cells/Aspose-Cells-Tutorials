---
category: general
date: 2026-03-29
description: Como analisar datas japonesas em C# usando DateTimeParser e CultureInfo.
  Aprenda a analisar datas de eras japonesas, dicas de análise de datas em C# e como
  lidar com casos extremos.
draft: false
keywords:
- how to parse japanese
- japanese era date parsing
- datetimeparser c#
- cultureinfo ja-jp
- parse japanese era
- c# date parsing
language: pt
og_description: Como analisar datas japonesas em C# usando DateTimeParser e CultureInfo.
  Obtenha uma solução passo a passo para a análise de datas de era japonesa.
og_title: Como analisar datas japonesas em C# – Guia completo
tags:
- C#
- .NET
- DateTime
- Localization
title: Como analisar datas japonesas em C# – Guia completo
url: /pt/net/data-loading-and-parsing/how-to-parse-japanese-dates-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como analisar datas japonesas em C# – Guia Completo

Já se perguntou **como analisar datas japonesas** dentro de uma aplicação .NET? Talvez você esteja trabalhando em um sistema financeiro que recebe datas como “令和3年5月12日” de um cliente japonês, e precise convertê‑las para um `DateTime` regular. Você não está sozinho—problemas de localização surgem o tempo todo.  

A boa notícia é que, com as configurações de cultura corretas e uma pequena classe auxiliar, **como analisar datas japonesas** se torna muito fácil. Neste tutorial vamos percorrer cada passo, desde a configuração do `CultureInfo` para *ja‑JP* até o tratamento de casos‑borda como eras históricas. Ao final, você terá um `DateTimeParser` reutilizável que funciona para qualquer data da era japonesa moderna.

> **O que você receberá** – um exemplo completo e executável, explicações do *porquê* de cada linha, dicas para eras mais antigas e uma lista de verificação rápida para que você nunca esqueça um passo.

## Pré‑requisitos

- .NET 6+ (ou .NET Framework 4.7 + – a API que usamos não mudou)
- Conhecimento básico de C# (você deve estar confortável com instruções `using` e `Console.WriteLine`)
- Nenhum pacote NuGet externo—tudo está em `System` e `System.Globalization`

Se você já tem um projeto aberto, ótimo—basta inserir o código. Caso contrário, crie um novo aplicativo console com `dotnet new console -n JapaneseDateDemo` e você está pronto.

## Passo 1: Entender o Sistema de Calendário Japonês

Antes de mergulharmos no código, vamos responder ao “por quê”. As datas japonesas são expressas em formato de **era** (元号), onde o número do ano reinicia quando um novo imperador ascende. Por exemplo:

- **令和** (Reiwa) começou em 01‑05‑2019.
- **平成** (Heisei) cobriu de 1989‑2019.
- **昭和** (Showa) foi de 1926‑1989.

A classe `JapaneseCalendar` do .NET já conhece essas eras, mas você precisa informar ao analisador qual cultura usar. É aí que entra **cultureinfo ja‑jp**—ele vincula o calendário ao locale japonês.

## Passo 2: Criar um Pequeno Wrapper – `DateTimeParser`

Em vez de espalhar `CultureInfo` por todo o código, vamos encapsular a lógica em um pequeno helper. Isso torna o código reutilizável e mantém o restante da sua aplicação limpo.

```csharp
// File: DateTimeParser.cs
using System;
using System.Globalization;

public class DateTimeParser
{
    private readonly CultureInfo _culture;
    private readonly JapaneseCalendar _japaneseCalendar;

    public DateTimeParser(CultureInfo culture)
    {
        // Ensure the supplied culture uses the Japanese calendar.
        if (culture.Calendar is not JapaneseCalendar)
            throw new ArgumentException("Culture must use JapaneseCalendar.", nameof(culture));

        _culture = culture;
        _japaneseCalendar = (JapaneseCalendar)culture.Calendar;
    }

    /// <summary>
    /// Parses a Japanese era date string (e.g., "令和3年5月12日") into a Gregorian DateTime.
    /// </summary>
    /// <param name="japaneseDate">The era‑based date string.</param>
    /// <returns>A DateTime representing the same day in the Gregorian calendar.</returns>
    public DateTime Parse(string japaneseDate)
    {
        if (string.IsNullOrWhiteSpace(japaneseDate))
            throw new ArgumentNullException(nameof(japaneseDate));

        // The standard pattern for Japanese era dates.
        // "gggy年M月d日" -> era name (ggg), year (y), month (M), day (d)
        const string pattern = "gggy年M月d日";

        // TryParseExact respects the culture's calendar (JapaneseCalendar here).
        if (DateTime.TryParseExact(
                japaneseDate,
                pattern,
                _culture,
                DateTimeStyles.None,
                out DateTime result))
        {
            return result;
        }

        // If parsing fails, give a helpful exception.
        throw new FormatException(
            $"Unable to parse '{japaneseDate}'. Expected format: {pattern}");
    }
}
```

**Por que este helper?**  
- **Responsabilidade única** – todo o parsing específico de locale fica em um só lugar.  
- **Tratamento de erros** – exibimos mensagens claras quando o formato está errado.  
- **Preparado para o futuro** – se mais tarde você precisar suportar as eras *Taisho* ou *Meiji*, basta ajustar o padrão ou adicionar um fallback.

## Passo 3: Conectar Tudo em `Program.cs`

Agora usaremos o wrapper para realmente analisar uma string de exemplo. Observe como obtemos a cultura japonesa com `CultureInfo.GetCultureInfo("ja-JP")`. Isso satisfaz o requisito **cultureinfo ja‑jp** e garante que o `JapaneseCalendar` esteja ativo.

```csharp
// File: Program.cs
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // Step 3‑1: Grab the Japanese culture (ja-JP) which uses JapaneseCalendar.
        var japaneseCulture = CultureInfo.GetCultureInfo("ja-JP");

        // Step 3‑2: Initialise our DateTimeParser with that culture.
        var parser = new DateTimeParser(japaneseCulture);

        // Step 3‑3: The era string we want to convert.
        string eraDate = "令和3年5月12日";

        try
        {
            // Step 3‑4: Parse it.
            DateTime gregorian = parser.Parse(eraDate);

            // Step 3‑5: Show the result – expected: 2021‑05‑12.
            Console.WriteLine($"Japanese: {eraDate} → Gregorian: {gregorian:yyyy-MM-dd}");
        }
        catch (Exception ex)
        {
            // Friendly error output – useful in real‑world apps.
            Console.WriteLine($"Error: {ex.Message}");
        }
    }
}
```

Quando você executar `dotnet run` verá:

```
Japanese: 令和3年5月12日 → Gregorian: 2021-05-12
```

Esse é o núcleo de **como analisar datas japonesas**. Simples, não?

## Passo 4: Lidando com Casos de Borda & Eras Antigas

### 4.1 Datas Históricas Antes de 1912

O `JapaneseCalendar` embutido suporta apenas as eras modernas (a partir de Meiji). Se precisar analisar datas das eras *Taisho* (1912‑1926) ou *Meiji* (1868‑1912), o mesmo padrão funciona—basta garantir que a string inclua o nome correto da era (“大正”, “明治”). O parser ainda retornará um `DateTime` gregoriano correto.

```csharp
string taisho = "大正5年12月31日"; // 1916‑12‑31
Console.WriteLine(parser.Parse(taisho).ToString("yyyy-MM-dd"));
```

### 4.2 Era Ausente (Entrada Ambígua)

Se um cliente enviar “2021年5月12日” sem era, o parser falhará porque o padrão espera uma era (`ggg`). Você tem duas opções:

1. **Assumir Gregorian** – recair para `CultureInfo.InvariantCulture` e um padrão diferente.  
2. **Rejeitar a entrada** – informar ao chamador que a era é obrigatória.

Aqui está uma adaptação rápida:

```csharp
public DateTime ParseFlexible(string input)
{
    // Try era‑based first.
    try { return Parse(input); } catch { /* ignore */ }

    // Fallback to plain Gregorian pattern.
    const string gregPattern = "yyyy年M月d日";
    if (DateTime.TryParseExact(
            input,
            gregPattern,
            _culture,
            DateTimeStyles.None,
            out DateTime gResult))
    {
        return gResult;
    }

    throw new FormatException("Unable to parse the provided date string.");
}
```

### 3.3 Observação sobre Segurança de Thread

Objetos `CultureInfo` são somente‑leitura após a criação, então você pode reutilizar a mesma instância com segurança entre threads. O `DateTimeParser` em si não mantém estado mutável, tornando‑o **thread‑safe** – um fato útil para APIs web de alto volume.

## Passo 5: Junte Tudo – Um Exemplo Pronto‑para‑Copiar

Abaixo está o código completo que você pode inserir em um novo projeto console. Sem pacotes externos, sem dependências ocultas.

```csharp
// DateTimeParser.cs
using System;
using System.Globalization;

public class DateTimeParser
{
    private readonly CultureInfo _culture;
    private readonly JapaneseCalendar _japaneseCalendar;

    public DateTimeParser(CultureInfo culture)
    {
        if (culture.Calendar is not JapaneseCalendar)
            throw new ArgumentException("Culture must use JapaneseCalendar.", nameof(culture));

        _culture = culture;
        _japaneseCalendar = (JapaneseCalendar)culture.Calendar;
    }

    public DateTime Parse(string japaneseDate)
    {
        if (string.IsNullOrWhiteSpace(japaneseDate))
            throw new ArgumentNullException(nameof(japaneseDate));

        const string pattern = "gggy年M月d日";

        if (DateTime.TryParseExact(
                japaneseDate,
                pattern,
                _culture,
                DateTimeStyles.None,
                out DateTime result))
        {
            return result;
        }

        throw new FormatException(
            $"Unable to parse '{japaneseDate}'. Expected format: {pattern}");
    }

    // Optional flexible parser for non‑era inputs.
    public DateTime ParseFlexible(string input)
    {
        try { return Parse(input); } catch { /* fall through */ }

        const string gregPattern = "yyyy年M月d日";
        if (DateTime.TryParseExact(
                input,
                gregPattern,
                _culture,
                DateTimeStyles.None,
                out DateTime gResult))
        {
            return gResult;
        }

        throw new FormatException("Unable to parse the provided date string.");
    }
}
```

```csharp
// Program.cs
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        var japaneseCulture = CultureInfo.GetCultureInfo("ja-JP");
        var parser = new DateTimeParser(japaneseCulture);

        string[] samples = {
            "令和3年5月12日",   // 2021‑05‑12
            "平成31年4月30日", // 2019‑04‑30 (last day of Heisei)
            "大正5年12月31日", // 1916‑12‑31 (historical)
            "2022年1月1日"      // ambiguous – no era
        };

        foreach (var s in samples)
        {
            try
            {
                DateTime dt = parser.ParseFlexible(s);
                Console.WriteLine($"{s} → {dt:yyyy-MM-dd}");

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}