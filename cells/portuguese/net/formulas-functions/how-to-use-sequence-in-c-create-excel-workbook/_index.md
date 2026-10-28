---
category: general
date: 2026-07-03
description: Como usar SEQUENCE em C# para gerar números incrementais no Excel. Aprenda
  a criar uma pasta de trabalho Excel em C# e ASP.NET e a gerar um arquivo Excel com
  poucas linhas de código.
draft: false
keywords:
- how to use sequence
- create excel workbook c#
- asp.net create excel file
- generate incremental numbers excel
language: pt
og_description: Como usar SEQUENCE em C# para gerar números incrementais no Excel.
  Guia passo a passo para criar uma pasta de trabalho Excel em C# e ASP.NET e gerar
  arquivo Excel.
og_title: Como usar SEQUENCE em C# – Criar pasta de trabalho do Excel
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: How to use SEQUENCE in C# to generate incremental numbers in Excel.
    Learn to create Excel workbook C# and ASP.NET create Excel file with a few lines
    of code.
  headline: How to Use SEQUENCE in C# – Create Excel Workbook
  type: TechArticle
- description: How to use SEQUENCE in C# to generate incremental numbers in Excel.
    Learn to create Excel workbook C# and ASP.NET create Excel file with a few lines
    of code.
  name: How to Use SEQUENCE in C# – Create Excel Workbook
  steps:
  - name: Why Use SEQUENCE Instead of a Loop?
    text: '- **Performance** – Excel does the math on its own engine, which is highly
      optimized. - **Maintainability** – The formula is self‑documenting; anyone opening
      the sheet instantly knows the intent. - **Dynamic resizing** – Change the `rows`
      argument and the spill range expands automatically.'
  - name: Pro Tip
    text: 'If you need the workbook in memory (e.g., to send it over a web API), use
      a `MemoryStream`:'
  - name: What If the Client Uses an Older Excel Version?
    text: 'Dynamic arrays (including `SEQUENCE`) were introduced in Excel 365/2019.
      If you need backward compatibility, fall back to a manual fill:'
  type: HowTo
- questions:
  - answer: No. `SEQUENCE` is a non‑iterative function; a simple `CalculateFormula()`
      call is enough.
    question: Do I need to enable iterative calculation?
  - answer: 'Change the second argument: `=SEQUENCE(1,5,10,2)` spills across B1:F1.'
    question: What if I want a horizontal spill?
  - answer: Absolutely. For example, `=INDEX(A:A, SEQUENCE(5,1,10,2))` can pull rows
      from another column.
    question: Can I combine SEQUENCE with other functions?
  - answer: The file size impact of a formula is negligible. Only when you start populating
      millions of cells manually does size become an issue.
    question: Is the workbook size a concern?
  type: FAQPage
tags:
- C#
- Excel
- Aspose.Cells
- ASP.NET
title: Como usar SEQUENCE em C# – Criar pasta de trabalho do Excel
url: /pt/net/formulas-functions/how-to-use-sequence-in-c-create-excel-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como usar SEQUENCE em C# – Criar Pasta de Trabalho Excel

Já se perguntou **como usar SEQUENCE** para gerar uma lista de números em uma planilha Excel a partir de C#? Você não está sozinho. Seja construindo um painel de relatórios, alimentando uma grade de dados, ou apenas precisando de uma maneira rápida de gerar IDs, dominar esse truque economiza tempo de lidar com loops.

Neste tutorial, vamos **criar uma pasta de trabalho Excel em C#**, inserir uma fórmula de array dinâmico `SEQUENCE` na célula A1, e obter uma agradável coluna de números incrementais. Também veremos como servir esse arquivo a partir de um controlador ASP.NET—sim, **ASP.NET create Excel file** também será abordado. Ao final, você será capaz de **gerar números incrementais no estilo Excel** com uma única linha de código.

## O que você precisará

- .NET 6+ (o código também funciona no .NET Framework 4.6+)
- O pacote NuGet **Aspose.Cells for .NET** (ou qualquer biblioteca que exponha objetos `Workbook`/`Worksheet`)
- Um projeto básico ASP.NET Core ou MVC se você quiser experimentar a parte de download web

É isso. Nenhum COM interop extra, nenhuma instalação do Office necessária.

---

## Como usar SEQUENCE para gerar números incrementais

A função Excel `SEQUENCE(rows, [columns], [start], [step])` retorna um intervalo **spill**. No nosso caso queremos 5 linhas, 1 coluna, iniciar em 10, passo 2. A fórmula fica assim:

```excel
=SEQUENCE(5,1,10,2)
```

Quando o Excel a avalia, as células A1:A5 conterão **10, 12, 14, 16, 18**. A beleza é que não precisamos escrever nenhum loop em C#—a fórmula faz o trabalho pesado.

Abaixo está o trecho completo em C# que cria uma pasta de trabalho, insere a fórmula, força o cálculo e salva o arquivo.

```csharp
using Aspose.Cells;
using System.IO;

// 1️⃣ Create a new workbook
Workbook workbook = new Workbook();

// 2️⃣ Grab the first worksheet (Aspose creates one by default)
Worksheet sheet = workbook.Worksheets[0];

// 3️⃣ Insert the SEQUENCE formula – this will spill a 5‑row column starting at 10, step 2
sheet.Cells["A1"].Formula = "=SEQUENCE(5,1,10,2)";

// 4️⃣ Force calculation so the spilled range is materialized
workbook.CalculateFormula();

// 5️⃣ Save to disk (you can change the path as needed)
workbook.Save("DynamicArray.xlsx");
```

**Saída esperada** – abra *DynamicArray.xlsx* e você verá:

| A |
|---|
| 10 |
| 12 |
| 14 |
| 16 |
| 18 |

Essa é toda a história de **how to use sequence** em C#. Simples, certo? Mas vamos aprofundar um pouco mais.

### Por que usar SEQUENCE em vez de um loop?

- **Performance** – O Excel faz os cálculos em seu próprio motor, que é altamente otimizado.
- **Maintainability** – A fórmula é auto‑documentável; qualquer pessoa que abra a planilha entende instantaneamente a intenção.
- **Dynamic resizing** – Alterar o argumento `rows` faz com que o intervalo spill se expanda automaticamente.

---

## Criar Pasta de Trabalho Excel C# – Passo a Passo

Se você é novo em **create excel workbook c#**, a lista de verificação a seguir ajuda a evitar armadilhas comuns.

1. **Adicionar o pacote Aspose.Cells**  
   ```bash
   dotnet add package Aspose.Cells
   ```
   (Você também pode usar ClosedXML ou EPPlus, mas a API mostrada corresponde ao código acima.)

2. **Definir uma licença** (opcional para avaliação).  
   ```csharp
   var license = new Aspose.Cells.License();
   license.SetLicense("Aspose.Total.NET.lic");
   ```

3. **Instanciar `Workbook`** – isso fornece uma nova pasta de trabalho em branco.

4. **Referenciar a planilha** – `workbook.Worksheets[0]` é a planilha padrão chamada *Sheet1*.

5. **Aplicar a fórmula SEQUENCE** – como mostrado anteriormente.

6. **Calcular** – `workbook.CalculateFormula()` força o spill; caso contrário o arquivo conteria apenas a fórmula.

7. **Salvar** – você pode gravar no disco, em um `MemoryStream`, ou diretamente em uma resposta HTTP.

### Dica Pro

Se você precisar da pasta de trabalho na memória (por exemplo, para enviá‑la via API web), use um `MemoryStream`:

```csharp
using var ms = new MemoryStream();
workbook.Save(ms, SaveFormat.Xlsx);
byte[] excelBytes = ms.ToArray(); // ready to return or attach
```

---

## ASP.NET Create Excel File – Transmitindo ao Navegador

Agora que sabemos **create excel workbook c#**, vamos integrá‑lo a um controlador ASP.NET Core para que os usuários possam baixar o arquivo instantaneamente.

```csharp
using Aspose.Cells;
using Microsoft.AspNetCore.Mvc;
using System.IO;

[Route("api/[controller]")]
public class ExcelController : ControllerBase
{
    [HttpGet("download")]
    public IActionResult Download()
    {
        // 1️⃣ Build the workbook (same steps as before)
        var workbook = new Workbook();
        var sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].Formula = "=SEQUENCE(5,1,10,2)";
        workbook.CalculateFormula();

        // 2️⃣ Save to a memory stream
        using var ms = new MemoryStream();
        workbook.Save(ms, SaveFormat.Xlsx);
        ms.Position = 0; // reset stream position

        // 3️⃣ Return the file as a download
        const string fileName = "DynamicArray.xlsx";
        return File(ms, 
                    "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet", 
                    fileName);
    }
}
```

Quando um usuário acessa `/api/excel/download`, o navegador solicita o download de *DynamicArray.xlsx*. O arquivo já contém a coluna **generated incremental numbers excel** graças à fórmula `SEQUENCE`.

### E se o cliente usar uma versão mais antiga do Excel?

Arrays dinâmicos (incluindo `SEQUENCE`) foram introduzidos no Excel 365/2019. Se precisar de compatibilidade retroativa, volte para um preenchimento manual:

```csharp
// Alternative for older Excel: write numbers directly
for (int i = 0; i < 5; i++)
{
    sheet.Cells[i, 0].PutValue(10 + i * 2); // column 0 = A
}
```

Esse trecho mostra a abordagem clássica de **generate incremental numbers excel** sem depender da nova função.

---

## Perguntas Frequentes & Casos Limite

- **Preciso habilitar cálculo iterativo?**  
  Não. `SEQUENCE` é uma função não iterativa; uma simples chamada `CalculateFormula()` basta.

- **E se eu quiser um spill horizontal?**  
  Altere o segundo argumento: `=SEQUENCE(1,5,10,2)` espalha de B1 a F1.

- **Posso combinar SEQUENCE com outras funções?**  
  Absolutamente. Por exemplo, `=INDEX(A:A, SEQUENCE(5,1,10,2))` pode extrair linhas de outra coluna.

- **O tamanho da pasta de trabalho é uma preocupação?**  
  O impacto no tamanho do arquivo de uma fórmula é insignificante. Só quando você começa a preencher manualmente milhões de células o tamanho se torna um problema.

---

## Conclusão

Percorremos **how to use sequence** em C# para **create excel workbook c#**, servimos essa pasta de trabalho via **ASP.NET create excel file**, e demonstramos uma forma limpa de **generate incremental numbers excel** sem escrever loops. O principal aprendizado: deixe o próprio motor de arrays dinâmicos do Excel fazer a contagem, e deixe seu código .NET focar na orquestração.

Sinta‑se à vontade para experimentar—troque os argumentos `rows`, `start` ou `step`, faça spill horizontal, ou combine a fórmula com `IF` ou `FILTER` para relatórios mais sofisticados. Quando estiver pronto, tente encadear várias planilhas ou exportar a pasta de trabalho como CSV para sistemas downstream.

Tem uma variação que gostaria de compartilhar? Deixe um comentário abaixo, ou me chame no GitHub. Feliz codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Como criar e configurar pastas de trabalho Excel com Aspose.Cells .NET: Um guia passo a passo](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [Como criar e salvar arquivos Excel com Aspose.Cells para .NET: Um guia completo](/cells/english/net/workbook-operations/create-save-excel-file-aspose-cells-dotnet/)
- [Como criar e estilizar pastas de trabalho Excel usando Aspose.Cells para .NET (Guia 2023)](/cells/english/net/formatting/create-style-excel-workbooks-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}