---
category: general
date: 2026-06-08
description: Analise data de era japonesa em C# usando Aspose.Cells. Aprenda como
  CultureInfo ja-JP e o formato de era japonesa permitem conversão precisa de datas
  no Excel.
draft: false
keywords:
- parse japanese era date
- Aspose.Cells
- CultureInfo ja-JP
- Japanese era format
- Excel date conversion
- C# DateTime parsing
language: pt
og_description: Analise datas de era japonesa em C# rapidamente. Este tutorial mostra
  como CultureInfo ja-JP e Aspose.Cells convertem strings de era em objetos DateTime
  adequados.
og_title: Analisar Data da Era Japonesa em C# – Guia Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Parse Japanese era date in C# using Aspose.Cells. Learn how CultureInfo
    ja-JP and Japanese era format enable accurate Excel date conversion.
  headline: Parse Japanese Era Date in C# with Aspose.Cells – Full Guide
  type: TechArticle
- description: Parse Japanese era date in C# using Aspose.Cells. Learn how CultureInfo
    ja-JP and Japanese era format enable accurate Excel date conversion.
  name: Parse Japanese Era Date in C# with Aspose.Cells – Full Guide
  steps:
  - name: 5.1 Invalid or Empty Strings
    text: '```csharp string maybeDate = workbook.Worksheets[0].Cells["B1"].GetString();
      // could be empty if (string.IsNullOrWhiteSpace(maybeDate)) { Console.WriteLine("Cell
      B1 is empty – skipping."); } else { // Attempt to parse; catch format exceptions
      try { DateTime dt = DateTime.Parse(maybeDate, new Cultur'
  - name: 5.2 Older Eras (Showa, Taisho)
    text: 'The same `CultureInfo ja-JP` works for older eras automatically:'
  - name: 5.3 Using `DateTime.ParseExact` for Strict Validation
    text: 'If you want to enforce the exact Japanese era pattern, use a custom format
      string:'
  type: HowTo
- questions:
  - answer: Yes. As long as the workbook’s `Settings.CultureInfo` is set to `ja-JP`
      *before* you call `GetDateTime()`, Aspose.Cells will interpret the existing
      strings correctly.
    question: Does this work with .xlsx files that already contain era dates?
  - answer: The parsing returns a `DateTime` with `Kind = Unspecified`. If you need
      UTC or local time, apply `DateTime.SpecifyKind` or convert after parsing.
    question: What about time zones?
  - answer: Absolutely. Loop through the desired range and call `GetDateTime()` on
      each cell—just remember to handle exceptions for malformed entries.
    question: Can I parse multiple cells at once?
  type: FAQPage
tags:
- C#
- Excel
- DateTime
- Localization
title: Analisar Data de Era Japonesa em C# com Aspose.Cells – Guia Completo
url: /pt/net/excel-custom-number-date-formatting/parse-japanese-era-date-in-c-with-aspose-cells-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Parse Japanese Era Date in C# with Aspose.Cells – Guia Completo

Já precisou **parse japanese era date** diretamente de uma planilha Excel? Talvez você esteja extraindo dados de um sistema legado que ainda usa “令和3年5月12日” e queira um `DateTime` limpo para gerar relatórios. Neste tutorial vamos percorrer um exemplo completo, pronto‑para‑executar, que converte essas strings no formato de era em datas C# corretas — sem adivinhações.

Usaremos **Aspose.Cells**, a poderosa biblioteca .NET para manipulação de Excel, juntamente com a configuração **CultureInfo ja-JP** que entende as eras japonesas. Ao final, você terá um trecho reutilizável que lida com “令和”, “平成” e até eras mais antigas sem esforço.

## Pré‑requisitos

- .NET 6.0 ou superior (o código também funciona no .NET Framework 4.6+)  
- Aspose.Cells para .NET (você pode obter o pacote de teste gratuito via NuGet: `Install-Package Aspose.Cells`)  
- Familiaridade básica com C# — nada sofisticado, apenas um aplicativo de console serve  
- Uma IDE de sua escolha (Visual Studio, Rider, VS Code, etc.)

É só isso. Nenhum serviço extra, nenhum analisador de terceiros obscuro.

## Etapa 1: Configurar o Projeto e Adicionar Aspose.Cells

Primeiro, crie um novo projeto de console:

```bash
dotnet new console -n JapaneseEraParser
cd JapaneseEraParser
dotnet add package Aspose.Cells
```

Agora abra **Program.cs** e adicione os namespaces necessários:

```csharp
using System;
using System.Globalization;
using Aspose.Cells;
```

> **Dica profissional:** Se você estiver usando o Visual Studio, a IDE sugerirá adicionar as instruções `using` automaticamente após digitar os nomes das classes.

## Etapa 2: Criar uma Pasta de Trabalho e Aplicar a Cultura Japonesa

A chave para **parse japanese era date** corretamente é informar ao Aspose.Cells qual cultura usar. Definir `CultureInfo` para `ja-JP` ativa a análise sensível a eras.

```csharp
// Step 2: Initialize a new workbook and set Japanese culture
Workbook workbook = new Workbook();
workbook.Settings.CultureInfo = new CultureInfo("ja-JP");
```

Por que isso importa? O calendário japonês possui várias eras (por exemplo, *Reiwa* (令和), *Heisei* (平成)). O objeto `CultureInfo` contém um `JapaneseCalendar` que conhece as datas de início de cada era, de modo que qualquer string no formato de era japonesa pode ser interpretada corretamente.

## Etapa 3: Gravar uma String de Data de Era Japonesa em uma Célula

Vamos inserir uma data de era de exemplo na célula **A1**. Sinta‑se à vontade para alterar a string e testar diferentes eras.

```csharp
// Step 3: Put a Japanese era date string into A1
string japaneseDate = "令和3年5月12日"; // Reiwa 3, May 12, 2021
workbook.Worksheets[0].Cells["A1"].PutValue(japaneseDate);
```

Se preferir trabalhar com uma pasta de trabalho existente, você pode carregá‑la com `new Workbook("path/to/file.xlsx")` e pular a etapa de criação.

## Etapa 4: Recuperar o Valor como um Objeto C# DateTime

Agora a mágica acontece. Ao chamar `GetDateTime()`, o Aspose.Cells lê a célula usando a `CultureInfo` previamente definida e devolve um `DateTime` adequado.

```csharp
// Step 4: Parse the cell value into a DateTime
DateTime parsedDate = workbook.Worksheets[0].Cells["A1"].GetDateTime();
Console.WriteLine($"Parsed DateTime: {parsedDate:yyyy-MM-dd}");
```

**Saída esperada**

```
Parsed DateTime: 2021-05-12
```

Esse é todo o fluxo de **parse japanese era date** — quatro linhas concisas de código.

## Etapa 5: Tratamento de Casos Limite e Eras Alternativas

Dados do mundo real nem sempre são limpos. Aqui estão alguns cenários que você pode encontrar e como tratá‑los.

### 5.1 Strings Inválidas ou Vazias

```csharp
string maybeDate = workbook.Worksheets[0].Cells["B1"].GetString(); // could be empty
if (string.IsNullOrWhiteSpace(maybeDate))
{
    Console.WriteLine("Cell B1 is empty – skipping.");
}
else
{
    // Attempt to parse; catch format exceptions
    try
    {
        DateTime dt = DateTime.Parse(maybeDate, new CultureInfo("ja-JP"));
        Console.WriteLine($"B1 parsed as {dt:yyyy-MM-dd}");
    }
    catch (FormatException)
    {
        Console.WriteLine($"Unable to parse '{maybeDate}' as a Japanese era date.");
    }
}
```

### 5.2 Eras Mais Antigas (Showa, Taisho)

O mesmo `CultureInfo ja-JP` funciona automaticamente para eras mais antigas:

```csharp
string showaDate = "昭和45年12月31日"; // Showa 45 = 1970-12-31
DateTime showaParsed = DateTime.Parse(showaDate, new CultureInfo("ja-JP"));
Console.WriteLine(showaParsed.ToString("yyyy-MM-dd")); // 1970-12-31
```

### 5.3 Usando `DateTime.ParseExact` para Validação Rigorosa

Se quiser impor o padrão exato da era japonesa, use uma string de formato personalizada:

```csharp
string pattern = "ggggy年M月d日"; // gggg = era name, y = year in era
DateTime strictDate = DateTime.ParseExact(japaneseDate, pattern, new CultureInfo("ja-JP"));
Console.WriteLine(strictDate); // 2021-05-12 00:00:00
```

Essa abordagem lança um `FormatException` quando a string diverge, o que pode ser útil para verificações de qualidade de dados.

## Exemplo Completo em Funcionamento

Abaixo está o programa completo que você pode copiar‑colar em **Program.cs** e executar.

```csharp
using System;
using System.Globalization;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and set Japanese culture
        Workbook workbook = new Workbook();
        workbook.Settings.CultureInfo = new CultureInfo("ja-JP");

        // 2️⃣ Insert a Japanese era date string
        string japaneseDate = "令和3年5月12日";
        workbook.Worksheets[0].Cells["A1"].PutValue(japaneseDate);

        // 3️⃣ Parse the cell value into DateTime
        DateTime parsedDate = workbook.Worksheets[0].Cells["A1"].GetDateTime();
        Console.WriteLine($"Parsed DateTime: {parsedDate:yyyy-MM-dd}");

        // 4️⃣ Demonstrate handling an older era
        string showaDate = "昭和45年12月31日";
        DateTime showaParsed = DateTime.Parse(showaDate, new CultureInfo("ja-JP"));
        Console.WriteLine($"Showa parsed: {showaParsed:yyyy-MM-dd}");

        // 5️⃣ Strict parsing with ParseExact
        string pattern = "gggy年M月d日";
        try
        {
            DateTime strict = DateTime.ParseExact(japaneseDate, pattern, new CultureInfo("ja-JP"));
            Console.WriteLine($"Strict parse: {strict:yyyy-MM-dd}");
        }
        catch (FormatException ex)
        {
            Console.WriteLine($"Strict parse failed: {ex.Message}");
        }
    }
}
```

Execute com `dotnet run` e você deverá ver:

```
Parsed DateTime: 2021-05-12
Showa parsed: 1970-12-31
Strict parse: 2021-05-12
```

Boom—**parse japanese era date** concluído, e você tem um modelo para qualquer era que encontrar.

![Fluxo de análise de data de era japonesa – mostra criação da planilha, definição de cultura, escrita da célula e chamada GetDateTime](parse-japanese-era-date.png "Diagrama ilustrando como analisar data de era japonesa usando Aspose.Cells e CultureInfo ja-JP")

## Perguntas Frequentes Respondidas

- **Isso funciona com arquivos .xlsx que já contêm datas de era?**  
  Sim. Desde que o `Settings.CultureInfo` da pasta de trabalho esteja definido como `ja-JP` *antes* de chamar `GetDateTime()`, o Aspose.Cells interpretará as strings existentes corretamente.

- **E quanto aos fusos horários?**  
  A análise devolve um `DateTime` com `Kind = Unspecified`. Se precisar de UTC ou horário local, aplique `DateTime.SpecifyKind` ou converta após a análise.

- **Posso analisar várias células de uma vez?**  
  Absolutamente. Percorra o intervalo desejado e chame `GetDateTime()` em cada célula — apenas lembre‑se de tratar exceções para entradas malformadas.

## Conclusão

Cobremos tudo o que você precisa para **parse japanese era date** em C# usando Aspose.Cells e o `CultureInfo ja-JP` embutido. Desde a configuração da pasta de trabalho, gravação de strings no formato de era, recuperação de um `DateTime` limpo, até o tratamento de casos limite como eras antigas e validação rigorosa — este guia oferece uma solução pronta para produção.

Em seguida, você pode explorar **conversão de datas do Excel** para datas numéricas serializadas, ou mergulhar em **análise de DateTime em C#** com calendários personalizados para outras localidades. O mesmo padrão funciona para o calendário budista tailandês, calendário hebraico e mais — basta trocar o `CultureInfo`.

Tem algum caso especial que está lhe dando dor de cabeça? Deixe um comentário e vamos solucionar juntos. Feliz codificação!

## O Que Você Deve Aprender a Seguir?

Os tutoriais abaixo abordam tópicos intimamente relacionados que expandem as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Como Implementar Validação de Data em .NET Usando Aspose.Cells: Um Guia Abrangente](/cells/english/net/data-validation/implement-date-validation-net-aspose-cells/)
- [Alterar o Sistema de Data do Excel para 1904 usando Aspose.Cells .NET](/cells/english/net/calculation-engine/change-excel-date-system-aspose-cells-net/)
- [Converter Excel para PDF com Formatos de Data Personalizados Usando Aspose.Cells para Java](/cells/english/java/workbook-operations/render-excel-custom-date-formats-pdf-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}