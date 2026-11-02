---
category: general
date: 2026-03-30
description: Aprenda como formatar data ISO enquanto lê valores de data/hora do Excel
  e extrai dados de data/hora do Excel usando Aspose.Cells em C#.
draft: false
keywords:
- format date iso
- read excel datetime
- extract datetime excel
- Aspose.Cells date parsing
- Japanese era dates
language: pt
og_description: formate data ISO a partir de dados do Excel usando Aspose.Cells. Este
  guia mostra como ler data/hora do Excel, extrair valores de data/hora do Excel e
  gerar datas ISO.
og_title: Formatar data ISO do Excel – Tutorial C# passo a passo
tags:
- C#
- Excel
- DateTime
- Aspose.Cells
title: Formatar data ISO a partir do Excel – Guia completo de C#
url: /pt/net/excel-custom-number-date-formatting/format-date-iso-from-excel-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# formatar data iso a partir do Excel – Guia Completo em C#

Já precisou **formatar data iso** ao extrair datas de uma planilha Excel? Talvez você esteja lidando com datas de era japonesa, ou simplesmente queira uma string limpa `yyyy‑MM‑dd` para um payload de API. Neste tutorial você verá exatamente como **ler datetime do Excel** nas células, **extrair datetime Excel** valores, e convertê-los para o formato ISO‑8601 — sem adivinhações.

Vamos percorrer um exemplo real que usa Aspose.Cells, explica por que cada linha importa e mostra a saída final que você pode copiar‑colar em seu projeto. Ao final, você será capaz de lidar com strings de era incomuns como “令和3年5月1日” e gerar uma data ISO padrão, pronta para bancos de dados, JSON ou onde precisar.

## Pré-requisitos

- .NET 6.0 ou posterior (o código funciona também com .NET Framework)
- Aspose.Cells para .NET (versão de avaliação gratuita ou licenciada)
- Familiaridade básica com C# e conceitos de Excel
- Visual Studio ou qualquer editor C# de sua preferência

Nenhum pacote NuGet adicional é necessário além do Aspose.Cells, portanto a configuração é bastante simples.

---

## Etapa 1: Criar um Workbook e Alvo a Primeira Planilha

A primeira coisa que você faz é instanciar um novo objeto `Workbook`. Isso fornece uma representação em memória de um arquivo Excel, que você pode então manipular ou ler.

```csharp
using Aspose.Cells;
using System.Globalization;

// Step 1: Initialize a new workbook and grab the first worksheet
Workbook workbook = new Workbook();                 // creates an empty .xlsx
Worksheet worksheet = workbook.Worksheets[0];      // the default sheet is "Sheet1"
```

*Por que isso importa:*  
Criar o workbook programaticamente permite que você evite lidar com arquivos físicos durante os testes. Também garante que a referência da planilha esteja sempre válida — sem surpresas de referência nula mais tarde ao tentar **ler datetime do Excel** valores.

---

## Etapa 2: Escrever uma String de Data de Era Japonesa em uma Célula

Nosso objetivo é demonstrar a análise de uma data não gregoriana. Vamos colocar a string de era diretamente na célula **A1**.

```csharp
// Step 2: Insert a Japanese era date string into cell A1
worksheet.Cells["A1"].PutValue("令和3年5月1日");
```

*Dica profissional:* Se você estiver extraindo dados de um workbook existente, você pularia a chamada `PutValue` e simplesmente referenciaria a célula que já contém a data. O importante é que a célula contém uma **string** que representa uma data no calendário lunissolar japonês.

---

## Etapa 3: Configurar uma Cultura que Entende o Calendário Lunissolar Japonês

A classe `CultureInfo` do .NET permite especificar como as datas devem ser interpretadas. Ao substituir o calendário gregoriano padrão por `JapaneseLunisolarCalendar`, você fornece ao analisador o contexto necessário.

```csharp
// Step 3: Set up a culture using the Japanese lunisolar calendar
CultureInfo japaneseCulture = new CultureInfo("ja-JP");
japaneseCulture.DateTimeFormat.Calendar = new JapaneseLunisolarCalendar();
```

*Por que fazemos isso:*  
Se você tentar analisar “令和3年5月1日” com a cultura padrão, o .NET lançará uma `FormatException`. Substituir pelo calendário lunissolar informa ao runtime exatamente como mapear “令和3年” (o 3º ano da era Reiwa) para o ano gregoriano 2021.

---

## Etapa 4: Analisar o Valor da Célula como um `DateTime` Usando a Cultura Configurada

Agora vem o coração da operação — transformar aquela string de era em um objeto `DateTime` adequado. Aspose.Cells fornece uma sobrecarga conveniente de `GetDateTime` que aceita um `CultureInfo`.

```csharp
// Step 4: Retrieve the cell value as a DateTime, respecting the Japanese culture
DateTime parsedDate = worksheet.Cells["A1"].GetDateTime(japaneseCulture);
```

*O que está acontecendo nos bastidores:*  
`GetDateTime` lê a string bruta, aplica as regras de calendário da cultura fornecida e retorna um `DateTime` que representa o mesmo instante no calendário gregoriano. Este é o momento em que você **extrai datetime Excel** dados em uma forma que pode ser manipulada no .NET.

---

## Etapa 5: Exibir a Data Analisada no Formato ISO 8601

Finalmente, formatamos o `DateTime` como uma string ISO — `yyyy‑MM‑dd` — que é universalmente aceita por APIs, bancos de dados e frameworks front‑end.

```csharp
// Step 5: Print the date in ISO format (e.g., 2021-05-01)
Console.WriteLine(parsedDate.ToString("yyyy-MM-dd")); // Output: 2021-05-01
```

*Por que ISO?*  
ISO 8601 elimina ambiguidades. “05/01/2021” pode ser 1º de maio ou 5 de janeiro dependendo da localidade. `2021-05-01` é cristalino, e é por isso que **formatamos data iso** em quase todos os cenários de integração.

---

## Exemplo Completo Funcional

Abaixo está o programa completo, pronto‑para‑executar. Copie-o para um projeto de aplicativo console, adicione a referência ao Aspose.Cells e pressione **F5**.

```csharp
using Aspose.Cells;
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and select the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Write a Japanese era date string into cell A1
        worksheet.Cells["A1"].PutValue("令和3年5月1日");

        // 3️⃣ Set up Japanese lunisolar culture
        CultureInfo japaneseCulture = new CultureInfo("ja-JP");
        japaneseCulture.DateTimeFormat.Calendar = new JapaneseLunisolarCalendar();

        // 4️⃣ Parse the cell value as DateTime using the culture
        DateTime parsedDate = worksheet.Cells["A1"].GetDateTime(japaneseCulture);

        // 5️⃣ Output the date in ISO format
        Console.WriteLine(parsedDate.ToString("yyyy-MM-dd")); // 2021-05-01
    }
}
```

**Saída esperada**

```
2021-05-01
```

Execute-o uma vez, e você verá a data formatada em ISO impressa no console. Esse é todo o pipeline de **ler datetime do Excel** até **formatar data iso**.

---

## Lidando com Casos de Borda Comuns

### 1. Células contendo números de data reais do Excel

Às vezes o Excel armazena datas como números seriais (ex., `44204`). Nesse caso, você não precisa de uma cultura; basta chamar `GetDateTime()` sem parâmetros:

```csharp
DateTime serialDate = worksheet.Cells["B2"].GetDateTime(); // B2 holds a numeric date
Console.WriteLine(serialDate.ToString("yyyy-MM-dd"));
```

### 2. Células vazias ou inválidas

Se uma célula estiver vazia ou contiver uma string não analisável, `GetDateTime` lançará uma exceção. Envolva a chamada em um `try/catch` ou verifique `IsDateTime` primeiro:

```csharp
if (worksheet.Cells["C3"].Type == CellValueType.IsDateTime)
{
    DateTime safeDate = worksheet.Cells["C3"].GetDateTime();
    Console.WriteLine(safeDate.ToString("yyyy-MM-dd"));
}
else
{
    Console.WriteLine("Cell C3 does not contain a valid date.");
}
```

### 3. Formatos de Era Diferentes

Outras eras japonesas (Heisei, Showa) seguem o mesmo padrão. O mesmo `JapaneseLunisolarCalendar` as tratará automaticamente, portanto você não precisa de lógica extra — basta fornecer a string.

---

## Dicas Profissionais & Armadilhas

- **Performance:** Ao processar planilhas grandes, reutilize uma única instância de `CultureInfo` em vez de criar uma nova dentro de um loop.
- **Thread Safety:** Objetos `CultureInfo` são somente‑leitura após você definir o calendário, portanto são seguros para compartilhar entre threads.
- **Aspose.Cells Licensing:** Se você estiver usando a versão de avaliação gratuita, lembre‑se de que alguns recursos podem ser limitados após o período de avaliação expirar. A análise de datas mostrada aqui funciona bem tanto em modo de avaliação quanto licenciado.
- **Time Zones:** O `DateTime` que você obtém é **unspecified** (sem fuso horário). Se precisar de UTC, chame `DateTime.SpecifyKind(parsedDate, DateTimeKind.Utc)` ou converta usando `TimeZoneInfo`.

---

## Conclusão

Cobremos tudo o que você precisa para **formatar data iso** a partir de um workbook Excel usando C#. Começando de uma string de era japonesa bruta, nós **lemos datetime do Excel**, configuramos a cultura correta, **extraímos datetime Excel** dados e, finalmente, geramos uma string ISO‑8601 limpa. A abordagem funciona para qualquer representação de data que o Excel possa apresentar, seja um número serial, uma string específica de localidade ou um formato de era tradicional.

Próximos passos? Experimente percorrer uma coluna inteira de datas, gravar os resultados ISO de volta em uma nova planilha, ou enviá‑los diretamente em um payload JSON para um serviço web. Se você estiver curioso sobre outros sistemas de calendário (Hebraico, Islâmico), Aspose.Cells e o `CultureInfo` do .NET tornam esses experimentos igualmente fáceis.

Tem perguntas ou um formato de data complicado que não consegue decifrar? Deixe um comentário abaixo, e feliz codificação!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}