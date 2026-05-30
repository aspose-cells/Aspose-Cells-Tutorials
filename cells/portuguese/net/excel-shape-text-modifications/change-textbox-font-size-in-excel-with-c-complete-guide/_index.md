---
category: general
date: 2026-05-30
description: Altere o tamanho da fonte da caixa de texto no Excel usando C#. Aprenda
  a modificar a fonte da caixa de texto do Excel rapidamente com código passo a passo.
draft: false
keywords:
- change textbox font size
- modify excel textbox font
language: pt
og_description: Altere o tamanho da fonte da caixa de texto no Excel usando C#. Este
  guia mostra como modificar a fonte da caixa de texto do Excel de forma segura e
  eficiente.
og_title: Alterar o Tamanho da Fonte da Caixa de Texto no Excel com C# – Tutorial
  Completo
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Change textbox font size in Excel using C#. Learn how to modify excel
    textbox font quickly with step‑by‑step code.
  headline: Change Textbox Font Size in Excel with C# – Complete Guide
  type: TechArticle
- description: Change textbox font size in Excel using C#. Learn how to modify excel
    textbox font quickly with step‑by‑step code.
  name: Change Textbox Font Size in Excel with C# – Complete Guide
  steps:
  - name: Why this matters
    text: Opening the workbook via COM gives us a live object model—meaning any change
      we make reflects instantly in the file. Setting `Visible = false` speeds things
      up and avoids popping windows during automation.
  - name: Why we use `TextFrame2`
    text: '`TextFrame2` is the newer object model introduced with Office 2007. It
      supports advanced typographic features and is generally more reliable than the
      older `TextFrame`. Using it ensures our **change textbox font size** operation
      works across modern Excel versions.'
  - name: 1. Change *all* textboxes on a sheet
    text: '```csharp foreach (Excel.Shape s in xlWorksheet.Shapes) { if (s.Type.HasFlag(Excel.MsoShapeType.msoTextBox))
      { var tr = s.TextFrame2.TextRange; tr.Font.Name = fontName; tr.Font.Size = newSize;
      } } ```'
  - name: 2. Identify a textbox by its **Name** instead of index
    text: 'If you gave your textbox a meaningful name (e.g., “TitleBox”), you can
      fetch it directly:'
  type: HowTo
tags:
- Excel Interop
- C#
- Office Automation
title: Alterar o tamanho da fonte da caixa de texto no Excel com C# – Guia completo
url: /pt/net/excel-shape-text-modifications/change-textbox-font-size-in-excel-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Alterar o Tamanho da Fonte da Caixa de Texto no Excel com C# – Guia Completo

Precisa **alterar o tamanho da fonte da caixa de texto** em uma planilha do Excel usando C#? Você está no lugar certo. Seja gerando relatórios, construindo um painel ou apenas ajustando um modelo, modificar a aparência de uma caixa de texto pode deixar sua planilha muito mais profissional.

Neste tutorial, também **modificaremos a fonte da caixa de texto no Excel** além do tamanho — pense em família da fonte, negrito e até em lidar com múltiplas formas. Ao final, você terá um trecho pronto‑para‑executar que cobre todos os aspectos do processo, desde a abertura da pasta de trabalho até a limpeza dos objetos COM. Sem enrolação, apenas código prático que você pode inserir no seu projeto hoje.

## Pré-requisitos — O Que Você Precisa

| Requirement | Why it matters |
|-------------|----------------|
| **.NET 6+** (or .NET Framework 4.7.2+) | Fornece o compilador e runtime C#. |
| **Microsoft.Office.Interop.Excel** NuGet package | Fornece os tipos COM interop necessários para comunicar-se com o Excel. |
| **Excel installed** (any recent version) | A camada Interop funciona apenas quando o aplicativo Office está presente. |
| **Basic C# knowledge** | Você acompanhará facilmente, mas explicaremos cada linha. |

Se algum desses estiver faltando, pause agora e instale-os; o restante do guia assume que eles estão presentes.

## Etapa 1: Configurar o Projeto e Importar Namespaces

Primeiro, crie um novo aplicativo console (ou integre em um existente) e importe o namespace interop.

```csharp
using System;
using Excel = Microsoft.Office.Interop.Excel;

namespace ExcelTextboxDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll call the helper method that does the heavy lifting.
            ChangeTextboxFontSize(@"C:\Temp\Sample.xlsx", "Sheet1", 0, 14, "Calibri");
        }
    }
}
```

> **Pro tip:** Se você estiver direcionando .NET 6+, adicione o pacote `Microsoft.Office.Interop.Excel` via `dotnet add package Microsoft.Office.Interop.Excel`. Isso garante que o alias `Excel` seja resolvido corretamente.

## Etapa 2: Abrir a Pasta de Trabalho e Obter a Planilha Alvo

Agora precisamos iniciar o Excel, abrir o arquivo e apontar para a planilha que contém a caixa de texto. Envolver isso em um bloco `try/finally` garante que os objetos COM sejam liberados mesmo que algo dê errado.

```csharp
static void ChangeTextboxFontSize(string workbookPath,
                                  string sheetName,
                                  int textboxIndex,
                                  double newSize,
                                  string fontName)
{
    Excel.Application xlApp = null;
    Excel.Workbook xlWorkbook = null;
    Excel.Worksheet xlWorksheet = null;

    try
    {
        xlApp = new Excel.Application
        {
            // Keep Excel hidden; set to true if you want to watch the changes.
            Visible = false,
            DisplayAlerts = false
        };

        xlWorkbook = xlApp.Workbooks.Open(workbookPath);
        xlWorksheet = xlWorkbook.Worksheets[sheetName] as Excel.Worksheet;
        if (xlWorksheet == null)
            throw new ArgumentException($"Worksheet '{sheetName}' not found.");
```

### Por que isso importa

Abrir a pasta de trabalho via COM nos fornece um modelo de objeto ao vivo — ou seja, qualquer alteração que façamos reflete instantaneamente no arquivo. Definir `Visible = false` acelera o processo e evita janelas surgindo durante a automação.

## Etapa 3: Recuperar a Forma da Caixa de Texto

O Excel trata caixas de texto como objetos `Shape` dentro da coleção `Shapes`, e não como uma coleção dedicada `TextBox`. Por isso, o código abaixo parece um pouco diferente do trecho que você pode ter visto online.

```csharp
        // Excel stores all drawing objects (including textboxes) in the Shapes collection.
        Excel.Shapes shapes = xlWorksheet.Shapes;

        // Guard against an out‑of‑range index.
        if (textboxIndex < 0 || textboxIndex >= shapes.Count)
            throw new IndexOutOfRangeException("Textbox index is out of range.");

        // Grab the specific shape; we assume it’s a textbox.
        Excel.Shape textboxShape = shapes.Item(textboxIndex + 1); // COM collections are 1‑based.
        if (!textboxShape.Type.HasFlag(Excel.MsoShapeType.msoTextBox))
            throw new InvalidOperationException("Selected shape is not a textbox.");
```

> **Watch out:** A coleção `Shapes` é baseada em 1, então adicionamos `+1` ao `textboxIndex` baseado em zero que você fornece. Esquecer isso gera erros de “índice fora do intervalo” que podem ser frustrantes de depurar.

## Etapa 4: Alterar o Tamanho da Fonte da Caixa de Texto (e o Nome)

É aqui que finalmente **alteramos o tamanho da fonte da caixa de texto**. A propriedade `TextFrame2` nos dá acesso às opções de formatação de texto rico, que incluem `Font.Name` e `Font.Size`.

```csharp
        // Access the text range inside the textbox.
        Excel.TextRange2 textRange = textboxShape.TextFrame2.TextRange;

        // Change the font name – this also “modifies excel textbox font”.
        textRange.Font.Name = fontName;

        // Change the font size – the core of our tutorial.
        textRange.Font.Size = newSize;

        // Optional: make the text bold for extra emphasis.
        // textRange.Font.Bold = Microsoft.Office.Core.MsoTriState.msoTrue;
```

### Por que usamos `TextFrame2`

`TextFrame2` é o modelo de objeto mais recente introduzido no Office 2007. Ele suporta recursos tipográficos avançados e geralmente é mais confiável que o antigo `TextFrame`. Usá‑lo garante que nossa operação de **alterar o tamanho da fonte da caixa de texto** funcione nas versões modernas do Excel.

## Etapa 5: Salvar, Limpar e Verificar

Depois de ajustar a fonte, precisamos persistir as alterações e liberar todas as referências COM. Pular a limpeza pode deixar processos órfãos do Excel rodando em segundo plano.

```csharp
        // Save the workbook – you can also use SaveAs to create a copy.
        xlWorkbook.Save();

        Console.WriteLine($"Successfully changed textbox font size to {newSize} pt and font to '{fontName}'.");
    }
    catch (Exception ex)
    {
        Console.Error.WriteLine($"Error: {ex.Message}");
    }
    finally
    {
        // Release COM objects in reverse order of creation.
        if (xlWorksheet != null) System.Runtime.InteropServices.Marshal.ReleaseComObject(xlWorksheet);
        if (xlWorkbook != null)
        {
            xlWorkbook.Close(false);
            System.Runtime.InteropServices.Marshal.ReleaseComObject(xlWorkbook);
        }
        if (xlApp != null)
        {
            xlApp.Quit();
            System.Runtime.InteropServices.Marshal.ReleaseComObject(xlApp);
        }

        // Force garbage collection to clean up any remaining RCWs.
        GC.Collect();
        GC.WaitForPendingFinalizers();
    }
}
```

> **Pro tip:** Se precisar **modificar a fonte da caixa de texto no Excel** em várias planilhas, envolva a lógica interna em um loop que itere sobre `Workbook.Worksheets`. Apenas lembre‑se de redefinir `textboxIndex` para cada planilha.

## Lidando com Casos de Borda — Múltiplas Caixas de Texto e Formas Ausentes

Planilhas do mundo real raramente contêm apenas uma caixa de texto. Abaixo estão duas estratégias rápidas que você pode adotar sem reescrever todo o método.

### 1. Alterar *todas* as caixas de texto em uma planilha

```csharp
foreach (Excel.Shape s in xlWorksheet.Shapes)
{
    if (s.Type.HasFlag(Excel.MsoShapeType.msoTextBox))
    {
        var tr = s.TextFrame2.TextRange;
        tr.Font.Name = fontName;
        tr.Font.Size = newSize;
    }
}
```

### 2. Identificar uma caixa de texto pelo seu **Nome** em vez de índice

Se você deu à sua caixa de texto um nome significativo (por exemplo, “TitleBox”), pode obtê‑la diretamente:

```csharp
Excel.Shape namedBox = xlWorksheet.Shapes.Item("TitleBox");
namedBox.TextFrame2.TextRange.Font.Size = newSize;
```

Ambas as abordagens permitem que você **modifique a fonte da caixa de texto no Excel** com precisão, independentemente de como a pasta de trabalho está estruturada.

## Visão Geral Visual (Opcional)

Se você prefere uma pista visual rápida, imagine o diagrama a seguir:

![Screenshot showing Excel worksheet with a highlighted textbox – demonstrates how to change textbox font size](change-textbox-font-size.png)

*Texto alternativo:* *alterar o tamanho da fonte da caixa de texto no Excel – caixa de texto destacada pronta para modificação da fonte.*

## Exemplo Completo Funcional

Juntando tudo, aqui está um único arquivo que você pode copiar‑colar em um projeto console e executar imediatamente (apenas atualize o caminho do arquivo e o nome da planilha).



## O que Você Deve Aprender a Seguir?

- [Alterando o Tamanho da Fonte no Excel](/cells/english/net/working-with-fonts-in-excel/changing-font-size/)
- [Como Personalizar o Tamanho da Fonte em Células do Excel Usando Aspose.Cells .NET | Guia Completo](/cells/english/net/formatting/customize-font-size-excel-aspose-cells-dotnet/)
- [Como Definir Estilos de Fonte no Excel Usando Aspose.Cells para .NET (Guia Passo a Passo)](/cells/english/net/formatting/aspose-cells-dotnet-set-font-styles-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}