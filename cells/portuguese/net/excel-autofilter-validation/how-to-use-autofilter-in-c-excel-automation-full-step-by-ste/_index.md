---
category: general
date: 2026-05-30
description: Como usar AutoFilter na automação de Excel em C#. Aprenda a criar uma
  pasta de trabalho Excel, filtrar linhas por valor e otimizar suas tarefas de planilha.
draft: false
keywords:
- how to use autofilter
- create excel workbook
- filter rows by value
- filter column b
- excel automation c#
language: pt
og_description: Como usar AutoFilter na automação de Excel com C#. Domine a criação
  de pastas de trabalho, filtrando linhas por valor e automatizando planilhas com
  facilidade.
og_title: Como usar o AutoFilter na automação de Excel com C# – Guia completo
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: How to use AutoFilter in C# Excel automation. Learn how to create Excel
    workbook, filter rows by value, and streamline your spreadsheet tasks.
  headline: How to Use AutoFilter in C# Excel Automation – Full Step‑by‑Step Guide
  type: TechArticle
- description: How to use AutoFilter in C# Excel automation. Learn how to create Excel
    workbook, filter rows by value, and streamline your spreadsheet tasks.
  name: How to Use AutoFilter in C# Excel Automation – Full Step‑by‑Step Guide
  steps:
  - name: '**Creating the workbook** – `new Workbook()` gives you a clean file; `Worksheets[0]`
      grabs the default sheet.'
    text: '**Creating the workbook** – `new Workbook()` gives you a clean file; `Worksheets[0]`
      grabs the default sheet.'
  - name: '**Filling sample data** – We write a tiny dataset so you can see the filter
      in action.'
    text: '**Filling sample data** – We write a tiny dataset so you can see the filter
      in action.'
  - name: '**Adding a table** – `ListObjects.Add` converts the range into an Excel
      table, which automatically supports filtering and styling.'
    text: '**Adding a table** – `ListObjects.Add` converts the range into an Excel
      table, which automatically supports filtering and styling.'
  - name: '**Applying AutoFilter** – `table.AutoFilter.Filter(1, "Apple")` tells the
      engine: “Show only rows where the second column (B) equals *Apple*.”'
    text: '**Applying AutoFilter** – `table.AutoFilter.Filter(1, "Apple")` tells the
      engine: “Show only rows where the second column (B) equals *Apple*.”'
  - name: '**Saving files** – Two files are written: one filtered, one with the filter
      removed, proving that `RemoveAutoFilter()` works as expected.'
    text: '**Saving files** – Two files are written: one filtered, one with the filter
      removed, proving that `RemoveAutoFilter()` works as expected.'
  type: HowTo
- questions:
  - answer: Yes. Aspose.Cells can save to both `.xlsx` and `.xls` by changing the
      file extension or using `SaveOptions`.
    question: Does this work with older .xls files?
  - answer: Load the file with `new Workbook("path.xlsx")`, apply the filter, then
      `Save` again.
    question: What if I need to filter *after* the workbook is already saved?
  - answer: 'Absolutely. Use `worksheet.AutoFilter.Range = "A1:C5";` and then `worksheet.AutoFilter.ApplyFilter();`.
      However, tables give you built‑in styling and easier column referencing. ---
      ## Image – Visual Confirmation ![Screenshot showing AutoFilter applied to column
      B in an Excel workbook created with C#'
    question: Can I apply a filter to a *range* that isn’t a table?
  type: FAQPage
tags:
- C#
- Excel
- Automation
title: Como usar o AutoFilter na automação de Excel com C# – Guia completo passo a
  passo
url: /pt/net/excel-autofilter-validation/how-to-use-autofilter-in-c-excel-automation-full-step-by-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Usar AutoFilter em Automação de Excel com C# – Guia Completo

Já se perguntou **como usar AutoFilter** ao gerar arquivos Excel a partir de código C#? Você não está sozinho—muitos desenvolvedores se deparam com esse obstáculo quando precisam ocultar linhas que não correspondem a um determinado critério.  

Neste tutorial vamos percorrer um exemplo concreto e executável que **cria uma pasta de trabalho Excel**, adiciona uma tabela e então **filtra linhas por valor** na coluna B. Ao final, você terá um trecho limpo e reutilizável que pode ser inserido em qualquer projeto C# que precise de automação Excel.

## O Que Você Vai Aprender

- Configurar um projeto C# com a biblioteca Aspose.Cells (ou Microsoft.Office.Interop).  
- **Criar pasta de trabalho Excel** programaticamente e adicionar uma tabela estilizada.  
- Aplicar **AutoFilter** para mostrar apenas linhas onde **a coluna B** seja igual a uma string específica.  
- Remover o filtro completamente, restaurando o conjunto de dados completo.  
- Dicas para lidar com casos de borda, como colunas ausentes ou múltiplos critérios de filtro.

Nenhuma experiência prévia em Excel‑VBA é necessária; apenas um entendimento básico de C# e pacotes NuGet.

---

## Pré‑requisitos

| Requisito | Por que é importante |
|-----------|----------------------|
| .NET 6.0 ou superior (ou .NET Framework 4.7+) | Runtimes modernos oferecem melhor desempenho e gerenciamento de pacotes mais simples. |
| Aspose.Cells for .NET (ou Microsoft.Office.Interop.Excel) instalado via NuGet | Esta biblioteca fornece os objetos `Workbook`, `Worksheet` e `Table` usados no código. |
| Um editor de código (Visual Studio, VS Code, Rider, etc.) | Você precisará compilar e executar o exemplo. |
| Conhecimento básico de C# | O tutorial explica *por que* cada linha existe, não apenas *o que* ela faz. |

Você pode instalar Aspose.Cells com:

```bash
dotnet add package Aspose.Cells
```

---

## Como Usar AutoFilter com Aspose.Cells em C#

A seguir está o programa completo e autocontido. Salve como `Program.cs` em um projeto de console e execute – você obterá `FilteredWorkbook.xlsx` na pasta de saída.

```csharp
using System;
using Aspose.Cells;

namespace ExcelAutoFilterDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // Step 1: Create an Excel workbook and grab the first worksheet
            // -------------------------------------------------
            Workbook workbook = new Workbook();               // creates a new, empty workbook
            Worksheet sheet = workbook.Worksheets[0];         // the default sheet is named "Sheet1"

            // Populate the sheet with sample data (A‑C columns, 5 rows)
            sheet.Cells["A1"].PutValue("ID");
            sheet.Cells["B1"].PutValue("Fruit");
            sheet.Cells["C1"].PutValue("Quantity");

            sheet.Cells["A2"].PutValue(1);
            sheet.Cells["B2"].PutValue("Apple");
            sheet.Cells["C2"].PutValue(10);

            sheet.Cells["A3"].PutValue(2);
            sheet.Cells["B3"].PutValue("Banana");
            sheet.Cells["C3"].PutValue(15);

            sheet.Cells["A4"].PutValue(3);
            sheet.Cells["B4"].PutValue("Apple");
            sheet.Cells["C4"].PutValue(7);

            sheet.Cells["A5"].PutValue(4);
            sheet.Cells["B5"].PutValue("Cherry");
            sheet.Cells["C5"].PutValue(20);

            // -------------------------------------------------
            // Step 2: Convert the range into a ListObject (Excel table)
            // -------------------------------------------------
            // Parameters: firstRow, firstColumn, totalRows, totalColumns, hasHeaders
            int tableIdx = sheet.ListObjects.Add(0, 0, 5, 3, true);
            ListObject table = sheet.ListObjects[tableIdx];
            table.TableStyleType = TableStyleType.TableStyleMedium2; // nice built‑in styling

            // -------------------------------------------------
            // Step 3: Apply an AutoFilter to show only rows where column B = "Apple"
            // -------------------------------------------------
            // The AutoFilter is attached to the table’s range automatically.
            // We target column B (index 1) and set the criteria.
            table.AutoFilter.Filter(1, "Apple"); // 1 = zero‑based column index for B

            // -------------------------------------------------
            // Step 4: Save the filtered workbook to disk
            // -------------------------------------------------
            workbook.Save("FilteredWorkbook.xlsx");

            // -------------------------------------------------
            // Step 5: (Optional) Remove the AutoFilter completely
            // -------------------------------------------------
            // This demonstrates that you can revert to the full dataset without re‑loading.
            table.RemoveAutoFilter();   // clears the filter
            workbook.Save("UnfilteredWorkbook.xlsx");

            Console.WriteLine("Workbook created and filtered successfully.");
        }
    }
}
```

### Como o Código Funciona

1. **Criando a pasta de trabalho** – `new Workbook()` fornece um arquivo limpo; `Worksheets[0]` captura a planilha padrão.  
2. **Preenchendo dados de exemplo** – Escrevemos um pequeno conjunto de dados para que você veja o filtro em ação.  
3. **Adicionando uma tabela** – `ListObjects.Add` converte o intervalo em uma tabela Excel, que suporta filtragem e estilização automaticamente.  
4. **Aplicando AutoFilter** – `table.AutoFilter.Filter(1, "Apple")` diz ao motor: “Mostre apenas linhas onde a segunda coluna (B) seja *Apple*.”  
5. **Salvando arquivos** – Dois arquivos são gravados: um filtrado e outro com o filtro removido, provando que `RemoveAutoFilter()` funciona como esperado.

> **Dica de especialista:** Se precisar filtrar por múltiplos critérios (ex.: “Apple” *ou* “Banana”), use a sobrecarga `Filter(int columnIndex, string criteria1, string criteria2)` ou passe um array de strings.

---

## Filtrando Linhas por Valor – Variações Comuns

Embora o exemplo acima foque em **filtrar a coluna B**, você pode querer filtrar outras colunas ou usar critérios numéricos. Aqui está um cheat sheet rápido:

| Filtro desejado | Trecho de código |
|-----------------|-------------------|
| Correspondência de texto na coluna C | `table.AutoFilter.Filter(2, "Cherry");` |
| Números maiores que 10 na coluna C | `table.AutoFilter.CustomFilter(2, "10", OperatorType.GreaterThan);` |
| Múltiplos valores na coluna B | `table.AutoFilter.Filter(1, new[] { "Apple", "Banana" });` |

**Caso de borda:** Se o cabeçalho da coluna estiver escrito errado ou o índice da coluna estiver fora do intervalo, Aspose.Cells lançará um `ArgumentException`. Evite isso verificando `table.ListColumns.Count` antes de aplicar o filtro.

---

## Removendo o AutoFilter – Quando Resetar

Às vezes você precisa apresentar o conjunto de dados completo novamente (por exemplo, após o usuário limpar uma caixa de pesquisa). Chamar `table.RemoveAutoFilter()` resolve o problema em uma única linha. Se estiver usando Microsoft.Office.Interop, você chamaria `worksheet.AutoFilterMode = false;`.

---

## Recapitulação do Exemplo Completo

Abaixo está o *programa inteiro* novamente, sem comentários para quem prefere uma visão concisa:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        ws.Cells["A1"].PutValue("ID");
        ws.Cells["B1"].PutValue("Fruit");
        ws.Cells["C1"].PutValue("Quantity");

        ws.Cells["A2"].PutValue(1); ws.Cells["B2"].PutValue("Apple");  ws.Cells["C2"].PutValue(10);
        ws.Cells["A3"].PutValue(2); ws.Cells["B3"].PutValue("Banana"); ws.Cells["C3"].PutValue(15);
        ws.Cells["A4"].PutValue(3); ws.Cells["B4"].PutValue("Apple");  ws.Cells["C4"].PutValue(7);
        ws.Cells["A5"].PutValue(4); ws.Cells["B5"].PutValue("Cherry"); ws.Cells["C5"].PutValue(20);

        int idx = ws.ListObjects.Add(0, 0, 5, 3, true);
        ListObject tbl = ws.ListObjects[idx];
        tbl.TableStyleType = TableStyleType.TableStyleMedium2;

        tbl.AutoFilter.Filter(1, "Apple");
        wb.Save("FilteredWorkbook.xlsx");

        tbl.RemoveAutoFilter();
        wb.Save("UnfilteredWorkbook.xlsx");
    }
}
```

Executar isso gera dois arquivos:

- **FilteredWorkbook.xlsx** – apenas linhas com *Apple* visíveis.  
- **UnfilteredWorkbook.xlsx** – os dados originais restaurados.

---

## Perguntas Frequentes

**P: Isso funciona com arquivos .xls antigos?**  
R: Sim. Aspose.Cells pode salvar tanto em `.xlsx` quanto em `.xls` alterando a extensão do arquivo ou usando `SaveOptions`.

**P: E se eu precisar filtrar *após* a pasta de trabalho já estar salva?**  
R: Carregue o arquivo com `new Workbook("caminho.xlsx")`, aplique o filtro e, em seguida, `Save` novamente.

**P: Posso aplicar um filtro a um *intervalo* que não seja uma tabela?**  
R: Absolutamente. Use `worksheet.AutoFilter.Range = "A1:C5";` e então `worksheet.AutoFilter.ApplyFilter();`. Contudo, tabelas fornecem estilização integrada e referência de coluna mais fácil.

---

## Imagem – Confirmação Visual

![Captura de tela mostrando AutoFilter aplicado à coluna B em uma pasta de trabalho Excel criada com C#](/images/autofilter-column-b.png "AutoFilter na coluna B")

*(A imagem ilustra a visualização filtrada onde permanecem apenas as linhas contendo “Apple”.)*

---

## Conclusão

Acabamos de cobrir **como usar AutoFilter** em um cenário de automação Excel conduzido por C#, desde **criar uma pasta de trabalho Excel** até **filtrar linhas por valor** na **coluna B**, e finalmente **remover o filtro** quando não for mais necessário. Os passos principais—inicializar, adicionar uma tabela, aplicar o filtro e limpar—são reutilizáveis em qualquer projeto que precise de **excel automation c#**.

Pronto para o próximo desafio? Experimente:

- Adicionar formatação condicional para destacar linhas filtradas.  
- Exportar os dados filtrados para um CSV para processamento posterior.  
- Combinar múltiplos filtros (ex.: “Apple” *e* quantidade > 8).

Experimente, quebre coisas e depois conserte-as—

## O Que Você Deve Aprender a Seguir?

- [Como Implementar AutoFilter no Excel usando Aspose.Cells para .NET (Guia de Análise de Dados)](/cells/english/net/data-analysis/implement-autofilter-excel-aspose-cells-dotnet/)
- [Como Usar Autofilter Not Contains no Aspose.Cells .NET para Análise de Dados no Excel](/cells/english/net/data-analysis/master-autofilter-not-contains-aspose-cells-net/)
- [Como Implementar Autofilter 'EndsWith' no Aspose.Cells para .NET](/cells/english/net/data-analysis/implement-autofilter-endswith-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}