---
category: general
date: 2026-09-24
description: Analisar DateTime com o reinado do imperador japonês usando Aspose.Cells
  em C#. Ativar o calendário de eras japonesas, escrever strings de era e recuperar
  valores DateTime precisos.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- Parse DateTime with Japanese Emperor Reign
- Aspose.Cells
- C# date parsing
- Japanese era calendar
- Workbook Settings
- DateTimeValue
language: pt
lastmod: 2026-09-24
og_description: Analisar DateTime com o reinado do imperador japonês usando Aspose.Cells
  em C#. Este tutorial demonstra como habilitar o calendário de eras japonesas, escrever
  strings de era e ler de volta um DateTime correto.
og_image_alt: Screenshot of C# code parsing a Japanese era date with Aspose.Cells
og_title: Analisar DateTime com o reinado do imperador japonês usando Aspose.Cells
  – Guia C#
schemas:
- author: Aspose
  dateModified: '2026-09-24'
  description: Parse DateTime with Japanese Emperor Reign using Aspose.Cells in C#.
    Enable the Japanese era calendar, write era strings, and retrieve accurate DateTime
    values.
  headline: Parse DateTime with Japanese Emperor Reign using Aspose.Cells
  type: TechArticle
- description: Parse DateTime with Japanese Emperor Reign using Aspose.Cells in C#.
    Enable the Japanese era calendar, write era strings, and retrieve accurate DateTime
    values.
  name: Parse DateTime with Japanese Emperor Reign using Aspose.Cells
  steps:
  - name: Multiple era formats
    text: 'Aspose.Cells recognises several era representations:'
  - name: Invalid strings
    text: 'When the string cannot be parsed (e.g., `"令和99年13月40日"`), `DateTimeValue`
      returns `DateTime.MinValue`. You can check for this condition:'
  - name: Disabling the feature
    text: 'If you later need to store raw era strings without conversion, set the
      flag back to `false`:'
  - name: Performance tip
    text: Enabling the era calendar adds a small overhead to every `PutValue` call
      that involves strings. If you only parse a handful of cells, enable the flag
      right before the operation and disable it afterward to minimise impact.
  type: HowTo
tags:
- Aspose.Cells
- C#
- DateTime
- Japanese era
- .NET
title: Analisar DateTime com o reinado do imperador japonês usando Aspose.Cells
url: /pt/net/excel-custom-number-date-formatting/parse-datetime-with-japanese-emperor-reign-using-aspose-cell/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Analisar DateTime com o Reinado do Imperador Japonês usando Aspose.Cells

Se você precisar **analisar DateTime com o Reinado do Imperador Japonês** em uma aplicação .NET, este guia mostra exatamente como fazer isso com Aspose.Cells. Ao habilitar o calendário de eras japonesas, escrever uma string baseada em era e ler o valor `DateTime` resultante, você obtém datas confiáveis e sensíveis à cultura sem manipulação manual de strings.

Trabalhar com datas de eras japonesas é comum em finanças, governo e sistemas legados que ainda armazenam datas como “令和3年5月10日”. Este tutorial cobre o fluxo de trabalho completo, desde a configuração do projeto até a obtenção de um objeto `DateTime` que você pode usar em cálculos, registro ou exibição na UI.

## O que você aprenderá

- Como adicionar o pacote NuGet Aspose.Cells a um projeto C#.  
- Como ativar o **calendário de era japonesa** via `Workbook.Settings`.  
- Como escrever uma string de data de era japonesa em uma célula e deixar o Aspose.Cells analisá‑la automaticamente.  
- Como ler o `DateTime` analisado usando a propriedade `DateTimeValue`.  

**Pré-requisitos**  
- .NET 6.0 ou posterior (o código também funciona com .NET Framework 4.7+).  
- Familiaridade básica com C# e Visual Studio (ou qualquer IDE).  
- Acesso à internet para baixar o pacote Aspose.Cells.

---

## Etapa 1: Instalar Aspose.Cells

Abra a pasta do seu projeto em um terminal ou no Console do Gerenciador de Pacotes NuGet e execute:

```bash
dotnet add package Aspose.Cells
```

Ou, no Visual Studio, clique com o botão direito no projeto → **Manage NuGet Packages** → procure por **Aspose.Cells** e clique em **Install**.  
Isso adiciona o assembly `Aspose.Cells`, que fornece as funcionalidades `Workbook`, `Worksheet` e de análise que precisamos.

## Etapa 2: Habilitar o calendário de era japonesa

O Aspose.Cells desabilita a análise de eras japonesas por padrão. Você deve ativá‑la através da flag `Workbook.Settings.UseJapaneseEraCalendar`.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Create a new workbook instance
        Workbook workbook = new Workbook();

        // Enable parsing of Japanese era dates (e.g., 令和, 平成)
        workbook.Settings.UseJapaneseEraCalendar = true;
```

Definir `UseJapaneseEraCalendar` como `true` indica à biblioteca que ela deve interpretar strings que contêm nomes de eras (`令和`, `平成`, `昭和`, etc.) de acordo com as regras oficiais do calendário japonês.

## Etapa 3: Escrever uma string de data de era japonesa em uma célula

Em seguida, obtenha a primeira planilha e coloque uma string de data de era japonesa na célula **A1**.

```csharp
        // Access the first worksheet (index 0)
        Worksheet sheet = workbook.Worksheets[0];

        // Write the era‑based date string into cell A1
        sheet.Cells["A1"].PutValue("令和3年5月10日");
```

**Por que isso funciona:**  
Quando `UseJapaneseEraCalendar` está ativo, `PutValue` examina a string, detecta o prefixo da era (`令和`) e a converte internamente para o ano gregoriano correspondente (2021). A biblioteca então armazena o valor como um verdadeiro objeto `DateTime`, não apenas como texto.

## Etapa 4: Recuperar o valor `DateTime` analisado

Agora leia o `DateTimeValue` da célula. O Aspose.Cells retorna automaticamente a data gregoriana.

```csharp
        // Retrieve the parsed DateTime from cell A1
        DateTime parsedDate = sheet.Cells["A1"].DateTimeValue;

        // Output the result to the console
        Console.WriteLine($"Parsed Gregorian date: {parsedDate:yyyy-MM-dd}");
    }
}
```

Executando o programa imprime:

```
Parsed Gregorian date: 2021-05-10
```

A saída confirma que **Parse DateTime with Japanese Emperor Reign** converteu corretamente “令和3年5月10日” para 10 de maio de 2021.

## Etapa 5: Lidar com casos extremos e variações comuns

### Vários formatos de era
O Aspose.Cells reconhece várias representações de era:

| Era (Japonês) | Intervalo de anos gregoriano |
|----------------|------------------------------|
| 明治 (Meiji)   | 1868‑1912                    |
| 大正 (Taishō)  | 1912‑1926                    |
| 昭和 (Shōwa)   | 1926‑1989                    |
| 平成 (Heisei)  | 1989‑2019                    |
| 令和 (Reiwa)   | 2019‑present                 |

Se seus dados de origem misturam caracteres de largura total, espaços ou utilizam os kanjis “年”, “月”, “日”, o analisador ainda funciona. Por exemplo, `"平成31年4月30日"` torna‑se `2019-04-30`.

### Strings inválidas
Quando a string não pode ser analisada (ex.: `"令和99年13月40日"`), `DateTimeValue` retorna `DateTime.MinValue`. Você pode verificar essa condição:

```csharp
if (parsedDate == DateTime.MinValue)
{
    Console.WriteLine("The cell does not contain a valid Japanese era date.");
}
```

### Desativando o recurso
Se mais tarde precisar armazenar strings de era brutas sem conversão, defina a flag de volta para `false`:

```csharp
workbook.Settings.UseJapaneseEraCalendar = false;
```

### Dica de desempenho
Habilitar o calendário de era adiciona uma pequena sobrecarga a cada chamada de `PutValue` que envolve strings. Se você analisar apenas algumas células, habilite a flag imediatamente antes da operação e desative‑a depois para minimizar o impacto.

## Exemplo completo e executável

Abaixo está o programa completo que você pode copiar, colar e executar imediatamente.

```csharp
using Aspose.Cells;
using System;

class ParseJapaneseEraDemo
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // 2️⃣ Turn on Japanese era parsing
        workbook.Settings.UseJapaneseEraCalendar = true;

        // 3️⃣ Access the first worksheet
        Worksheet sheet = workbook.Worksheets[0];

        // 4️⃣ Write an era date string into A1
        sheet.Cells["A1"].PutValue("令和3年5月10日");

        // 5️⃣ Retrieve the parsed DateTime
        DateTime parsedDate = sheet.Cells["A1"].DateTimeValue;

        // Verify the result
        Console.WriteLine($"Parsed Gregorian date: {parsedDate:yyyy-MM-dd}");
        // Expected output: Parsed Gregorian date: 2021-05-10
    }
}
```

**Saída esperada**

```
Parsed Gregorian date: 2021-05-10
```

O programa demonstra o fluxo de ponta a ponta para **Parse DateTime with Japanese Emperor Reign** usando Aspose.Cells, desde a criação da planilha até a obtenção de um objeto `DateTime` utilizável.

## Conclusão

Agora você sabe como **Parse DateTime with Japanese Emperor Reign** em C# ao:

1. Instalar o **Aspose.Cells**.  
2. Habilitar o **calendário de era japonesa** via `Workbook.Settings`.  
3. Escrever strings baseadas em era nas células.  
4. Ler o `DateTimeValue` resultante.  

Essa abordagem elimina a lógica de análise manual, respeita os limites oficiais das eras e integra‑se perfeitamente ao código existente de manipulação de datas .NET.

**Próximos passos**  
- Explore outros recursos específicos de cultura do Aspose.Cells, como **análise de datas C#** para calendários Hijri ou Budista Tailandês.  
- Combine esta técnica com **Workbook Settings** como `CalcEngine` para avaliar fórmulas que referenciam datas de era.  
- Use o `DateTime` analisado em relatórios, armazenamento em banco de dados ou componentes de UI que requerem datas gregorianas.

Sinta‑se à vontade para experimentar diferentes strings de era, lidar com entradas inválidas e integrar a solução em pipelines maiores de importação de dados. Feliz codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Parse Japanese Era Dates in Excel – Full Guide for C# Developers](/cells/english/net/data-loading-and-parsing/parse-japanese-era-dates-in-excel-full-guide-for-c-developer/)
- [How to Parse Japanese Dates in C# – Complete Guide](/cells/english/net/data-loading-and-parsing/how-to-parse-japanese-dates-in-c-complete-guide/)
- [How to Implement Date Validation in .NET Using Aspose.Cells: A Comprehensive Guide](/cells/english/net/data-validation/implement-date-validation-net-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}