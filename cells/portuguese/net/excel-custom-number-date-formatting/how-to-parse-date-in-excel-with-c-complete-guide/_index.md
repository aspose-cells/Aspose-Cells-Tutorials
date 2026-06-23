---
category: general
date: 2026-05-23
description: Como analisar data de uma célula do Excel usando C#. Aprenda truques
  de formatação personalizada de números no Excel, leia a data da célula e aplique
  formatação personalizada para resultados precisos.
draft: false
keywords:
- how to parse date
- custom number format excel
- read date from cell
- format excel cell date
- apply custom format
language: pt
og_description: Como analisar data de uma célula do Excel usando C#. Este tutorial
  mostra como aplicar formato numérico personalizado no Excel, ler a data da célula
  e formatar a data da célula do Excel corretamente.
og_title: Como analisar data no Excel com C# – Guia completo
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: How to parse date from an Excel cell using C#. Learn custom number
    format Excel tricks, read date from cell, and apply custom format for accurate
    results.
  headline: How to Parse Date in Excel with C# – Complete Guide
  type: TechArticle
- description: How to parse date from an Excel cell using C#. Learn custom number
    format Excel tricks, read date from cell, and apply custom format for accurate
    results.
  name: How to Parse Date in Excel with C# – Complete Guide
  steps:
  - name: Why a Custom Format Works
    text: Excel stores dates as serial numbers internally. By applying a locale‑aware
      format, Excel attempts to *interpret* the underlying text according to the pattern.
      The `[$-ja-JP]` prefix forces the Japanese calendar rules, while the rest of
      the pattern maps the characters to year, month, and day.
  - name: 1. Parsing European Dates (e.g., “12/05/2021” in French)
    text: '```csharp firstCell.PutValue("12/05/2021"); // day/month/year Style frStyle
      = workbook.CreateStyle(); frStyle.Custom = "[$-fr-FR]dd/mm/yyyy"; firstCell.SetStyle(frStyle);
      DateTime frDate = firstCell.DateTimeValue; // 2021-05-12 ```'
  - name: 2. When the Cell Already Contains a Serial Date
    text: 'If the source Excel file already stores a true date value, you can skip
      the custom format entirely:'
  - name: 3. Fallback to Manual Parsing
    text: 'Sometimes data is messy (extra spaces, hidden characters). A safe fallback
      is:'
  type: HowTo
tags:
- Excel
- C#
- Date Parsing
title: Como analisar data no Excel com C# – Guia completo
url: /pt/net/excel-custom-number-date-formatting/how-to-parse-date-in-excel-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como analisar data no Excel com C# – Guia Completo

Já se perguntou **como analisar data** armazenada em uma planilha do Excel sem ter que mexer manualmente nas conversões de string? Você não está sozinho. Seja extraindo datas fiscais japonesas, combinações mês‑dia europeias ou qualquer string específica de localidade, obter um `DateTime` confiável em C# pode parecer perseguir um alvo em movimento.  

Neste tutorial, vamos percorrer um exemplo concreto, de ponta a ponta, que **aplica um formato numérico personalizado do Excel** a uma célula de texto, e então **lê a data da célula** como um `DateTime` adequado. Ao final, você saberá exatamente como **formatar data de célula do Excel**, **aplicar formato personalizado**, e evitar as armadilhas comuns que atrapalham a maioria dos desenvolvedores.

## Pré-requisitos

- .NET 6.0 ou posterior (o código funciona com .NET Core, .NET Framework e .NET 5+)
- Uma referência a uma biblioteca de planilhas que suporte manipulação de estilos – o exemplo usa **Aspose.Cells**, mas os conceitos se aplicam ao EPPlus, ClosedXML ou NPOI.
- Conhecimento básico de C# (você tem, certo?)

> **Dica profissional:** Se ainda não tem o Aspose.Cells, você pode obter uma avaliação gratuita no site deles e adicioná-lo via NuGet: `dotnet add package Aspose.Cells`.

## Visão geral da solução

1. **Crie uma pasta de trabalho** e direcione a primeira célula da primeira planilha.  
2. **Insira uma string de data específica de localidade** (japonês no nosso caso).  
3. **Aplique um formato numérico personalizado** que indica ao Excel para tratar a string como data.  
4. **Leia o valor da célula** de volta como um objeto `DateTime`.  

Esse é todo o fluxo – sem análise manual, sem acrobacias de `DateTime.ParseExact`. Vamos mergulhar.

---

## Etapa 1: Configurar a pasta de trabalho e a célula alvo

Primeiro, crie uma nova pasta de trabalho e obtenha a célula com a qual vamos trabalhar. Isso reflete o cenário de “nova pasta de trabalho” que a maioria dos trabalhos de processamento em lote inicia.

```csharp
using Aspose.Cells;

// Create a new workbook
Workbook workbook = new Workbook();

// Get the first worksheet's first cell (A1)
Cell firstCell = workbook.Worksheets[0].Cells[0, 0];
```

> **Por que isso importa:** Inicializar a pasta de trabalho programaticamente garante que controlamos todos os aspectos do arquivo – sem surpresas de formatação ocultas. O objeto `Cell` é nosso ponto de entrada tanto para o conteúdo quanto para o estilo.

---

## Etapa 2: Inserir uma string de data japonesa

O Excel frequentemente recebe datas como texto simples, especialmente quando os dados vêm de sistemas legados. Aqui simulamos isso inserindo uma data da era japonesa diretamente na célula.

```csharp
// Insert a Japanese date string (令和3年5月12日 = May 12, 2021)
firstCell.PutValue("令和3年5月12日");
```

> **Observação de caso extremo:** Se a célula já continha uma data real do Excel (um número serial), você poderia pular a etapa de formato personalizado. Este guia foca no caminho de conversão *texto‑para‑data*.

---

## Etapa 3: Aplicar um formato numérico personalizado que interpreta o texto como data

Agora vem a mágica: dizemos ao Excel para tratar a string usando um padrão **custom number format Excel** que respeita a localidade japonesa. A string de formato `[$-ja-JP]yyyy` extrai o componente do ano, mas você pode estendê-la para mês e dia conforme necessário.

```csharp
// Define a style with a custom number format for Japanese locale
Style style = workbook.CreateStyle();
style.Custom = "[$-ja-JP]yyyy\"年\"m\"月\"d\"日\"";

// Apply the style to the cell
firstCell.SetStyle(style);
```

### Por que um formato personalizado funciona

O Excel armazena datas como números seriais internamente. Ao aplicar um formato sensível à localidade, o Excel tenta *interpretar* o texto subjacente de acordo com o padrão. O prefixo `[$-ja-JP]` impõe as regras do calendário japonês, enquanto o restante do padrão mapeia os caracteres para ano, mês e dia.

> **Alternativa:** Se precisar de uma abordagem mais genérica, você pode usar `[$-en-US]mm/dd/yyyy` para datas no estilo dos EUA, ou qualquer outro código de cultura suportado pelo Windows.

---

## Etapa 4: Recuperar a data analisada como um objeto `DateTime`

Finalmente, solicitamos à célula seu `DateTimeValue`. O Aspose.Cells converte automaticamente o texto formatado em uma instância `DateTime` adequada.

```csharp
// Retrieve the cell value as a DateTime
DateTime parsedDate = firstCell.DateTimeValue;

// Output to console for verification
Console.WriteLine($"Parsed date: {parsedDate:yyyy-MM-dd}");
```

**Saída esperada no console**

```
Parsed date: 2021-05-12
```

> **E se ele retornar `DateTime.MinValue`?** Isso normalmente significa que o formato não corresponde ao conteúdo da célula. Verifique novamente a string de formato personalizado e assegure que o código de localidade corresponde ao idioma de origem.

---

## Bônus: Lidando com outras localidades e variações do mundo real

### 1. Analisando datas europeias (ex.: “12/05/2021” em francês)

```csharp
firstCell.PutValue("12/05/2021"); // day/month/year
Style frStyle = workbook.CreateStyle();
frStyle.Custom = "[$-fr-FR]dd/mm/yyyy";
firstCell.SetStyle(frStyle);
DateTime frDate = firstCell.DateTimeValue; // 2021-05-12
```

### 2. Quando a célula já contém uma data serial

Se o arquivo Excel de origem já armazena um valor de data real, você pode pular o formato personalizado completamente:

```csharp
DateTime existingDate = firstCell.DateTimeValue; // works out‑of‑the‑box
```

### 3. Recurso de análise manual

Às vezes os dados são confusos (espaços extras, caracteres ocultos). Um recurso seguro é:

```csharp
string raw = firstCell.StringValue?.Trim();
if (DateTime.TryParseExact(raw, "yyyy/MM/dd", CultureInfo.InvariantCulture,
                           DateTimeStyles.None, out DateTime fallback))
{
    // use fallback
}
```

Mas a abordagem de **aplicar formato personalizado** geralmente é mais rápida e menos propensa a erros porque aproveita o próprio mecanismo de análise do Excel.

---

## Armadilhas comuns e como evitá‑las

| Armadilha | Sintoma | Correção |
|-----------|---------|----------|
| Código de localidade errado (`[$-ja-JP]` vs `[$-ja]`) | `DateTimeValue` permanece em `1/1/1900` | Verifique a string LCID exata; use `CultureInfo.GetCultureInfo("ja-JP").LCID` para ter certeza. |
| Faltando aspas ao redor do texto estático | Excel trata `"年"` como um placeholder de formato e falha | Envolva caracteres estáticos em aspas duplas, por exemplo, `\"年\"`. |
| Célula já formatada como *Texto* | Formato personalizado ignorado | Limpe o `NumberFormat` da célula primeiro: `firstCell.SetStyle(workbook.CreateStyle());` |
| Usando uma biblioteca que não suporta a propriedade `Custom` | Erro de compilação | Mude para uma biblioteca que exponha formatos numéricos personalizados (Aspose.Cells, EPPlus, ClosedXML). |

---

## Exemplo completo funcionando (pronto para copiar e colar)

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and get target cell
        Workbook workbook = new Workbook();
        Cell firstCell = workbook.Worksheets[0].Cells[0, 0];

        // 2️⃣ Insert Japanese date string
        firstCell.PutValue("令和3年5月12日");

        // 3️⃣ Apply custom number format for Japanese locale
        Style style = workbook.CreateStyle();
        style.Custom = "[$-ja-JP]yyyy\"年\"m\"月\"d\"日\"";
        firstCell.SetStyle(style);

        // 4️⃣ Retrieve parsed DateTime
        DateTime parsedDate = firstCell.DateTimeValue;

        // Verify the result
        Console.WriteLine($"Parsed date: {parsedDate:yyyy-MM-dd}");
        // Expected: Parsed date: 2021-05-12

        // Optional: Save the workbook to see the formatted cell in Excel
        workbook.Save("ParsedDateExample.xlsx");
    }
}
```

Execute o programa, abra `ParsedDateExample.xlsx`, e você verá a célula **A1** exibindo `2021年5月12日` enquanto o valor subjacente é uma data correta do Excel.

---

## Conclusão

Cobriramos **como analisar data** em strings no Excel usando C# ao **aplicar um formato numérico personalizado do Excel** e então **ler a data da célula** como um `DateTime` nativo. Os principais pontos:

- Use um formato personalizado sensível à localidade (`[$-ja-JP]…`) para deixar o Excel fazer o trabalho pesado.  
- Acesse `Cell.DateTimeValue` para obter um `DateTime` limpo sem análise manual.  
- Ajuste a string de formato para outras culturas e sempre verifique com um rápido dump no console.  

A partir daqui você pode **formatar data de célula do Excel** para relatórios, alimentar o `DateTime` em bancos de dados, ou realizar cálculos diretamente no seu aplicativo C#. Experimente diferentes localidades, combine múltiplas células ou até processe em lote planilhas inteiras – os mesmos princípios se aplicam.

Tem um formato de data estranho que você não consegue decifrar? Deixe um comentário e vamos solucionar juntos. Feliz codificação!

## Tutoriais relacionados

- [Formatação personalizada de número e data no Excel](/cells/english/net/excel-custom-number-date-formatting/)
- [Dominando a apresentação de dados no Excel: formatação de número e data personalizada com Aspose.Cells para Java](/cells/english/java/formatting/aspose-cells-java-data-formatting-excel/)
- [Formatação personalizada de número e data no Excel](/cells/german/net/excel-custom-number-date-formatting/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}