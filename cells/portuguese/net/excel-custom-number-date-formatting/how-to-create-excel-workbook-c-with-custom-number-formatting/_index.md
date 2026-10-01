---
category: general
date: 2026-10-01
description: Aprenda a criar uma pasta de trabalho Excel em C#, aplicar formato numérico
  personalizado, definir casas decimais das células e salvar a pasta de trabalho como
  XLSX em um guia completo passo a passo.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook c#
- apply custom number format
- how to format numbers excel
- set cell decimal places
- save workbook as xlsx
language: pt
lastmod: 2026-10-01
og_description: Crie uma pasta de trabalho Excel em C# com formato numérico personalizado,
  defina as casas decimais da célula e salve a pasta de trabalho como XLSX. Siga este
  guia completo para obter saída numérica precisa.
og_image_alt: Screenshot of an Excel sheet showing numbers rounded to four significant
  digits
og_title: Criar pasta de trabalho Excel em C# – formato numérico personalizado e exportação
  XLSX
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to create Excel workbook C# and apply custom number format,
    set cell decimal places, and save workbook as XLSX in a complete step‑by‑step
    guide.
  headline: How to create Excel workbook C# with custom number formatting
  type: TechArticle
- description: Learn how to create Excel workbook C# and apply custom number format,
    set cell decimal places, and save workbook as XLSX in a complete step‑by‑step
    guide.
  name: How to create Excel workbook C# with custom number formatting
  steps:
  - name: Run the program (`dotnet run`).
    text: Run the program (`dotnet run`).
  - name: Open `SigDigits.xlsx`.
    text: Open `SigDigits.xlsx`.
  - name: Confirm that **A1** reads `123.5`.
    text: Confirm that **A1** reads `123.5`.
  - name: If you open the file’s XML (`.xlsx` is a zip archive), you’ll see the custom
      format `"0.######"` stored in the `<c>` element’s `s` attribute.
    text: If you open the file’s XML (`.xlsx` is a zip archive), you’ll see the custom
      format `"0.######"` stored in the `<c>` element’s `s` attribute.
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: Como criar uma pasta de trabalho do Excel em C# com formatação numérica personalizada
url: /pt/net/excel-custom-number-date-formatting/how-to-create-excel-workbook-c-with-custom-number-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como criar Excel workbook C# com formatação numérica personalizada

Se você precisa **criar excel workbook c#** que exiba números exatamente da maneira que deseja, este guia mostra como fazer isso em alguns passos claros. Você aprenderá a aplicar um formato numérico personalizado, definir casas decimais da célula e, finalmente, **salvar workbook como xlsx** para consumo posterior.

Trabalhar com dados numéricos costuma significar equilibrar precisão e legibilidade. Ao final deste tutorial você terá um padrão reutilizável que limita os dígitos exibidos a um número específico de algarismos significativos, preservando o valor original no arquivo. Nenhum script externo é necessário — apenas C# e a biblioteca Aspose.Cells.

## Pré-requisitos

Antes de começar, certifique‑se de que você tem:

* .NET 6.0 SDK ou posterior instalado  
* Visual Studio 2022 (ou qualquer IDE C#)  
* O pacote NuGet **Aspose.Cells for .NET** (`Install-Package Aspose.Cells`) – esta biblioteca fornece as classes `Workbook`, `Worksheet` e `ExportTableOptions` usadas nos exemplos.  

Esses requisitos são mínimos; o mesmo código funciona em .NET Core, .NET Framework e até em Azure Functions.

## Etapa 1: Create Excel workbook C# – initialize the file

A primeira operação é instanciar um novo objeto `Workbook`. Esse objeto representa todo o arquivo Excel na memória e contém automaticamente uma planilha padrão.

```csharp
using Aspose.Cells;

namespace ExcelDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();               // creates an empty .xlsx container
            Worksheet sheet = workbook.Worksheets[0];         // reference to the default sheet
```

**Por que isso importa:**  
Criar a pasta de trabalho antecipadamente fornece uma tela limpa. A planilha padrão (`Worksheets[0]`) está pronta para entrada de dados, de modo que você não precise adicionar uma nova aba a menos que seu cenário exija várias guias.

## Etapa 2: Write a numeric value to a cell

Agora coloque um número de exemplo na célula **A1**. O valor que usamos (`123.456789`) contém mais casas decimais do que queremos exibir finalmente, o que nos permite demonstrar o arredondamento depois.

```csharp
            // Step 2: Write a numeric value to cell A1
            sheet.Cells[0, 0].PutValue(123.456789); // row 0, column 0 = A1
```

**Dica:** `PutValue` detecta automaticamente o tipo de dado, então você não precisa converter o número para string.

## Etapa 3: Apply custom number format – limit visible decimals

Para controlar como o Excel mostra o número, criamos um `Style` com um **custom number format**. O padrão `"0.######"` indica ao Excel que exiba até seis casas decimais, mas omita zeros à direita.

```csharp
            // Step 3: Define a custom number format (up to 6 decimal places) and apply it
            Style customStyle = workbook.CreateStyle();
            customStyle.Custom = "0.######";               // up to 6 decimals, no trailing zeros
            sheet.Cells[0, 0].SetStyle(customStyle);
```

**Como isso funciona:**  
A string de formato segue a sintaxe de formatos personalizados do Excel. `0` força a exibição de um dígito, enquanto `#` exibe um dígito apenas se for significativo. Ao combiná‑los, você obtém uma exibição flexível que ainda respeita a precisão original.

## Etapa 4: Set cell decimal places – using ExportTableOptions

Se precisar **set cell decimal places** para dados exportados (por exemplo, ao converter para um DataTable), o Aspose.Cells permite especificar o número de **significant digits**. Esta etapa garante que o CSV ou DataTable exportado respeite as mesmas regras de arredondamento aplicadas na pasta de trabalho.

```csharp
            // Step 4: Configure export options to limit the output to 4 significant digits
            ExportTableOptions exportOptions = new ExportTableOptions();
            exportOptions.SignificantDigits = 4;           // round to 4 significant figures
```

**Por que usar `SignificantDigits`?**  
Ao contrário de uma contagem fixa de casas decimais, dígitos significativos preservam a magnitude do número enquanto limitam a precisão, o que costuma ser o que analistas esperam ao resumir dados.

## Etapa 5: Export the worksheet data and **save workbook as xlsx**

Por fim, exporte os dados (se precisar de um DataTable) e persista a pasta de trabalho no disco. A chamada `ExportDataTable` respeita as `ExportTableOptions` que configuramos, e `workbook.Save` grava um arquivo XLSX padrão.

```csharp
            // Step 5: Export the worksheet data using the configured options and save the workbook
            sheet.ExportDataTable(sheet.Cells.MaxDisplayRange, true, exportOptions);
            workbook.Save("SigDigits.xlsx");               // saves to the application’s working folder
        }
    }
}
```

**Resultado esperado:**  
Ao abrir *SigDigits.xlsx* no Excel, a célula **A1** mostra `123.5`. O valor subjacente permanece `123.456789`, mas o número exibido segue a regra de 4 dígitos significativos. Se você exportar a planilha para um DataTable, o valor na tabela também será arredondado para `123.5`.

---

## Apply custom number format to additional cells

Se precisar formatar um intervalo em vez de uma única célula, reutilize o objeto `Style`:

```csharp
// Apply the same custom style to B2:C5
Range range = sheet.Cells.CreateRange("B2:C5");
range.ApplyStyle(customStyle, new StyleFlag { NumberFormat = true });
```

**Pro tip:** Reutilizar um objeto de estilo reduz o consumo de memória e garante formatação consistente em toda a planilha.

## How to format numbers Excel using C# – common variations

| Cenário | String de formato | Resultado |
|----------|-------------------|-----------|
| Duas casas decimais fixas | `"0.00"` | `123.46` |
| Moeda (EUA) | `"$#,##0.00"` | `$123.46` |
| Porcentagem com uma casa decimal | `"0.0%"` | `12,346.0%` |
| Notação científica | `"0.00E+00"` | `1.23E+02` |

Escolha o padrão que corresponde aos requisitos do seu relatório. Todos os padrões são compatíveis com a propriedade `Style.Custom` demonstrada anteriormente.

## Set cell decimal places dynamically based on user input

Às vezes a precisão necessária não é conhecida em tempo de compilação. Você pode construir a string de formato em tempo de execução:

```csharp
int decimals = 3; // could come from a UI textbox
string format = "0." + new string('#', decimals);
customStyle.Custom = format;
sheet.Cells["A2"].PutValue(987.654321);
sheet.Cells["A2"].SetStyle(customStyle);
```

**Caso extremo:** Se `decimals` for zero, o formato torna‑se `"0"` (exibição inteira). Sempre valide a entrada do usuário para evitar strings de formato malformadas.

## Save workbook as XLSX – best practices

* **Use absolute paths** ao gravar em um diretório conhecido (`Path.Combine(Environment.CurrentDirectory, "output.xlsx")`).  
* **Dispose** o `Workbook` se você o envolver em uma instrução `using` para liberar recursos não gerenciados rapidamente:

```csharp
using (Workbook wb = new Workbook())
{
    // ...populate workbook...
    wb.Save(Path.Combine(@"C:\Exports", "Report.xlsx"));
}
```

* **Version compatibility:** Aspose.Cells grava arquivos compatíveis com Excel 2010‑2023, de modo que usuários posteriores não encontrarão problemas de formato.

---

## Full working example

Abaixo está o programa completo que você pode copiar, colar e executar imediatamente. Ele inclui todas as diretivas `using` necessárias, comentários e tratamento de erros.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelDemo
{
    class Program
    {
        static void Main()
        {
            try
            {
                // 1️⃣ Create workbook and get the first worksheet
                Workbook workbook = new Workbook();
                Worksheet sheet = workbook.Worksheets[0];

                // 2️⃣ Write a high‑precision number to A1
                sheet.Cells[0, 0].PutValue(123.456789);

                // 3️⃣ Apply a custom number format (up to 6 decimals)
                Style customStyle = workbook.CreateStyle();
                customStyle.Custom = "0.######";
                sheet.Cells[0, 0].SetStyle(customStyle);

                // 4️⃣ Configure export options for 4 significant digits
                ExportTableOptions exportOptions = new ExportTableOptions
                {
                    SignificantDigits = 4
                };

                // 5️⃣ Export data (optional) and save the workbook as XLSX
                sheet.ExportDataTable(sheet.Cells.MaxDisplayRange, true, exportOptions);
                string outputPath = Path.Combine(Environment.CurrentDirectory, "SigDigits.xlsx");
                workbook.Save(outputPath);

                Console.WriteLine($"Workbook saved successfully at: {outputPath}");
                Console.WriteLine("Cell A1 displays: " + sheet.Cells["A1"].StringValue);
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"Error creating workbook: {ex.Message}");
            }
        }
    }
}
```

**Etapas de verificação**

1. Execute o programa (`dotnet run`).  
2. Abra `SigDigits.xlsx`.  
3. Confirme que **A1** lê `123.5`.  
4. Se você abrir o XML do arquivo (`.xlsx` é um arquivo zip), verá o formato personalizado `"0.######"` armazenado no atributo `s` do elemento `<c>`.

---

## Conclusão

Neste tutorial você aprendeu como **create excel workbook c#**, **apply custom number format**, **set cell decimal places** e **save workbook as xlsx** usando Aspose.Cells. A solução demonstra tanto a formatação visual dentro do Excel quanto o arredondamento na exportação de dados através de `ExportTableOptions`.  

A partir daqui você pode:

* Expandir a abordagem para intervalos ou tabelas inteiras.  
* Combinar múltiplos estilos (fontes, bordas) com `StyleFlag`.  
* Automatizar a geração de relatórios percorrendo fontes de dados e aplicando a mesma lógica de formatação.  

Sinta‑se à vontade para experimentar diferentes strings de formato, contagens decimais ou opções de exportação para atender às necessidades específicas de seus relatórios. Boa codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Criar Pasta de Trabalho Excel C# – Aplicar Formato de Moeda e Importar DataTable](/cells/english/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/)
- [Criar Pasta de Trabalho Excel C# – Guia Passo a Passo com Formatação Condicional](/cells/english/net/excel-conditional-formatting/create-excel-workbook-c-step-by-step-guide-with-conditional/)
- [Criar Pasta de Trabalho Excel C# – Adicionar Comentário e Salvar como XLSX](/cells/english/net/excel-comment-annotation/create-excel-workbook-c-add-comment-save-as-xlsx/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}