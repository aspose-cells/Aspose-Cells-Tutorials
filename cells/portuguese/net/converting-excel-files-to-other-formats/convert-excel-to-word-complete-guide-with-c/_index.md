---
category: general
date: 2026-05-30
description: Converta Excel para Word rapidamente. Aprenda como exportar dados do
  Excel para um documento Word, salvar o Excel como DOCX e converter gráficos com
  exemplos de código claros.
draft: false
keywords:
- convert excel to word
- export excel data to word document
- how to save excel as docx
- convert excel chart to word
- convert spreadsheet to word document
language: pt
og_description: Converter Excel para Word em C#. Este guia mostra como exportar dados
  do Excel para um documento Word, salvar o Excel como DOCX e incorporar gráficos.
og_title: Converter Excel para Word – Tutorial C# passo a passo
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Convert Excel to Word quickly. Learn how to export Excel data to Word
    document, save Excel as DOCX, and convert charts with clear code examples.
  headline: Convert Excel to Word – Complete Guide with C#
  type: TechArticle
- description: Convert Excel to Word quickly. Learn how to export Excel data to Word
    document, save Excel as DOCX, and convert charts with clear code examples.
  name: Convert Excel to Word – Complete Guide with C#
  steps:
  - name: '**Install** the Aspose.Cells package.'
    text: '**Install** the Aspose.Cells package.'
  - name: '**Load** the Excel workbook (`Workbook workbook = new Workbook("path.xlsx")`).'
    text: '**Load** the Excel workbook (`Workbook workbook = new Workbook("path.xlsx")`).'
  - name: '**Create** a Word document container (`Document doc = new Document()`).'
    text: '**Create** a Word document container (`Document doc = new Document()`).'
  - name: '**Transfer** data—either a whole sheet, a selected range, or a chart—into
      the Word document.'
    text: '**Transfer** data—either a whole sheet, a selected range, or a chart—into
      the Word document.'
  - name: '**Save** the Word file as `.docx`.'
    text: '**Save** the Word file as `.docx`.'
  - name: We grab the first chart from the worksheet.
    text: We grab the first chart from the worksheet.
  - name: '`ToImage` renders it to a PNG stream—no temporary file needed.'
    text: '`ToImage` renders it to a PNG stream—no temporary file needed.'
  - name: '`DocumentBuilder` inserts that image into a fresh Word document.'
    text: '`DocumentBuilder` inserts that image into a fresh Word document.'
  - name: Finally we save the document as `.docx`.
    text: Finally we save the document as `.docx`.
  type: HowTo
tags:
- excel
- word
- csharp
- file-conversion
title: Converter Excel para Word – Guia Completo com C#
url: /pt/net/converting-excel-files-to-other-formats/convert-excel-to-word-complete-guide-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Converter Excel para Word – Guia Completo com C#

Já se perguntou como **converter Excel para Word** sem copiar‑e‑colar manualmente? Você não está sozinho. Seja para enviar um relatório, inserir um gráfico em uma proposta ou simplesmente automatizar uma tarefa entediante, transformar uma planilha em um documento Word pode economizar horas.

Neste tutorial vamos percorrer uma maneira limpa e programática de **exportar dados do Excel para um documento Word**, mostrar **como salvar Excel como DOCX** e ainda abordar **converter gráfico do Excel para Word**. Ao final você terá um trecho reutilizável que funciona com qualquer pasta de trabalho e entenderá o porquê de cada passo.

## O que você vai aprender

- Instalar a biblioteca .NET correta (Aspose.Cells) que torna a conversão Excel‑para‑Word simples.  
- Carregar uma pasta de trabalho Excel do disco e inspecionar seu conteúdo.  
- Exportar uma planilha inteira, um intervalo ou apenas um gráfico para um arquivo Word.  
- Salvar o resultado como um arquivo `.docx`, pronto para distribuição.  
- Armadilhas comuns, dicas de desempenho e como lidar com arquivos grandes.

Sem configuração pesada, sem interop, apenas código C# puro que roda em qualquer lugar onde .NET Core 6+ seja suportado.

## Pré‑requisitos

- .NET 6 SDK ou posterior (você também pode usar .NET Framework 4.7+).  
- Familiaridade básica com C# e pacotes NuGet.  
- O arquivo Excel que você deseja converter (vamos chamá‑lo de `advChart.xlsx`).  
- Uma licença para Aspose.Cells (a avaliação gratuita funciona bem para aprendizado).

Se estiver faltando algo, obtenha agora — caso contrário, vamos mergulhar.

## Converter Excel para Word – Visão geral

Em alto nível o processo se parece com isto:

1. **Instalar** o pacote Aspose.Cells.  
2. **Carregar** a pasta de trabalho Excel (`Workbook workbook = new Workbook("path.xlsx")`).  
3. **Criar** um contêiner de documento Word (`Document doc = new Document()`).  
4. **Transferir** os dados — seja uma planilha inteira, um intervalo selecionado ou um gráfico — para o documento Word.  
5. **Salvar** o arquivo Word como `.docx`.

Cada passo é detalhado abaixo, e você verá por que essa abordagem supera uma simples macro de “copiar‑colar”.

## Passo 1: Instalar a Biblioteca Necessária

Aspose.Cells é uma biblioteca comercial que manipula arquivos Excel sem precisar do Microsoft Office instalado. Ela também fornece um overload prático de `Save` que grava diretamente em formatos Word.

```bash
dotnet add package Aspose.Cells --version 24.9
```

> **Dica de especialista:** Se estiver experimentando localmente, pode pular o registro da licença. Apenas lembre‑se de definir o objeto `License` quando for para produção, caso contrário a saída conterá uma marca d’água.

## Passo 2: Carregar a Pasta de Trabalho Excel

Carregar a pasta de trabalho é simples. O construtor lê o arquivo para a memória, dando acesso a planilhas, células e gráficos.

```csharp
using Aspose.Cells;
using Aspose.Words;   // Needed for the Word document class
using System;

// Step 2: Load the Excel workbook
Workbook workbook = new Workbook(@"C:\Data\advChart.xlsx");

// Optional: Verify that the workbook loaded correctly
Console.WriteLine($"Workbook contains {workbook.Worksheets.Count} worksheet(s).");
```

Por que carregamos a pasta de trabalho primeiro? Porque a rotina de conversão extrai os dados diretamente da representação em memória. Isso evita I/O de disco posterior e permite manipular os dados (por exemplo, ocultar colunas) antes da exportação.

## Passo 3: Exportar Dados do Excel para Documento Word

Agora criaremos um objeto `Document` do Aspose.Words e inseriremos o conteúdo do Excel. Existem várias maneiras de fazer isso, mas a mais flexível é usar o método `Save` com `SaveFormat.Docx`.

```csharp
using Aspose.Words.Saving;

// Step 3: Export Excel data to a Word document
// The Save method automatically converts the workbook to a Word format.
workbook.Save(@"C:\Data\advChart.docx", SaveFormat.Docx);
```

Essa única linha faz o trabalho pesado: converte **todas** as planilhas, incluindo quaisquer gráficos incorporados, em um documento Word. Se precisar apenas de uma planilha específica, use o método `Copy` do objeto `Worksheet` para uma nova pasta de trabalho antes de salvar.

```csharp
// Export only the first worksheet
Worksheet sheet = workbook.Worksheets[0];
Workbook singleSheetWb = new Workbook();
singleSheetWb.Worksheets.AddCopy(sheet);
singleSheetWb.Save(@"C:\Data\singleSheet.docx", SaveFormat.Docx);
```

### Por que escolher `SaveFormat.Docx`?

- **Compatibilidade:** `.docx` é o formato Word moderno, legível pelo Office, Google Docs e LibreOffice.  
- **Tamanho:** É XML compactado, então o arquivo resultante costuma ser menor que os antigos binários `.doc`.  
- **Futuro‑próprio:** A Microsoft está impulsionando `.docx` para todos os novos recursos, então você não encontrará problemas de descontinuação.

## Passo 4: Converter Gráfico do Excel para Word

Às vezes você precisa apenas do gráfico, não da planilha inteira. Aspose.Cells permite extrair um gráfico como imagem e então incorporá‑lo em um documento Word.

```csharp
using System.Drawing.Imaging;

// Assume the chart we want is the first one on the first worksheet
Chart chart = workbook.Worksheets[0].Charts[0];

// Export chart to a PNG stream
using (MemoryStream chartStream = new MemoryStream())
{
    chart.ToImage(chartStream, ImageFormat.Png);
    chartStream.Position = 0; // Reset stream position

    // Create a new Word document
    Document wordDoc = new Document();
    DocumentBuilder builder = new DocumentBuilder(wordDoc);

    // Insert the chart image
    builder.InsertImage(chartStream);

    // Save the Word file
    wordDoc.Save(@"C:\Data\chartOnly.docx", SaveFormat.Docx);
}
```

**O que está acontecendo aqui?**  
1. Capturamos o primeiro gráfico da planilha.  
2. `ToImage` o renderiza para um fluxo PNG — sem necessidade de arquivo temporário.  
3. `DocumentBuilder` insere essa imagem em um novo documento Word.  
4. Finalmente salvamos o documento como `.docx`.

Se houver vários gráficos, basta percorrer `workbook.Worksheets[i].Charts` e repetir a lógica de inserção.

## Passo 5: Como Salvar Excel como DOCX (Casos de Borda)

O simples `workbook.Save(..., SaveFormat.Docx)` funciona na maioria dos cenários, mas há alguns casos de borda que vale a pena observar:

| Situação | Ação recomendada |
|-----------|--------------------|
| Pasta de trabalho muito grande (> 500 MB) | Use `SaveOptions` para aumentar o buffer de memória e habilitar streaming. |
| Necessita apenas de valores, sem fórmulas | Chame `workbook.CalculateFormula()` primeiro, então defina `Options.ConvertFormulaToValue = true`. |
| Quer manter a formatação do Excel | Garanta `Options.PreserveFormatting = true` (padrão). |
| Arquivo Excel protegido por senha | Abra com `new LoadOptions { Password = "pwd" }` antes da conversão. |

Aqui está um exemplo rápido que desabilita a conversão de fórmulas e transmite a saída:

```csharp
var saveOptions = new DocxSaveOptions
{
    PreserveFormatting = true,
    ConvertFormulaToValue = false,
    // Stream the result directly to a file to avoid loading the whole DOCX into RAM
    OutputStream = new FileStream(@"C:\Data\largeWorkbook.docx", FileMode.Create, FileAccess.Write)
};

workbook.Save(saveOptions);
```

## Armadilhas Comuns e Dicas de Especialista

- **Referência Aspose.Words ausente:** O overload `SaveFormat.Docx` está no namespace `Aspose.Words`, não em `Aspose.Cells`. Adicione ambos os pacotes NuGet.  
- **Separadores de caminho incorretos:** Use `@` antes de literais de string ou `Path.Combine` para evitar problemas com `\\` no Windows.  
- **Índice de gráfico fora do intervalo:** Nem toda planilha contém um gráfico. Sempre verifique `worksheet.Charts.Count > 0` antes de acessar `Charts[0]`.  
- **Desempenho:** Converter muitas planilhas de uma vez pode consumir muita memória. Libere objetos `Workbook` intermediários rapidamente ou use blocos `using`.  
- **Avisos de licença:** No modo avaliação, a saída terá uma marca d’água. Registre a licença logo no início da aplicação (`new License().SetLicense("Aspose.Cells.lic")`).  

## Exemplo Completo Funcional

Abaixo está um aplicativo console completo, pronto‑para‑executar, que demonstra **converter excel para word**, **exportar dados do excel para documento word**, **como salvar excel como docx** e **converter gráfico do excel para word**. Sinta‑se à vontade para copiar, colar e modificar.

```csharp
using System;
using System.IO;
using Aspose.Cells;
using Aspose.Words;
using Aspose.Words.Saving;
using Aspose.Words.Drawing;
using Aspose.Words.Drawing.Charts;
using System.Drawing.Imaging;

namespace ExcelToWordDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Install license if you have one (optional for demo)
            // var license = new Aspose.Cells.License();
            // license.SetLicense("Aspose.Cells.lic");

            string excelPath = @"C:\Data\advChart.xlsx";
            string wordPath = @"C:\Data\advChart.docx";
            string chartWordPath = @"C:\Data\chartOnly.docx";

            // 2️⃣ Load the workbook
            Workbook wb = new Workbook(excelPath);
            Console.WriteLine($"Loaded workbook with {wb.Worksheets.Count} sheet(s).");

            // 3️⃣ Convert full workbook to Word (convert excel to word)
            wb.Save(wordPath, SaveFormat.Docx);
            Console.WriteLine($"Workbook saved as Word document: {wordPath}");

            // 4️⃣ Extract first chart and embed into a separate Word file
            if (wb.Worksheets[0].Charts.Count > 0)
            {
                Chart chart = wb.Worksheets[0].Charts[0];
                using (MemoryStream imgStream = new MemoryStream())
                {
                    chart.ToImage(imgStream, ImageFormat.Png);
                    imgStream.Position = 0;

                    Document wordDoc = new Document();
                    DocumentBuilder builder = new DocumentBuilder(wordDoc);
                    builder.InsertImage(imgStream);
                    wordDoc.Save(chartWordPath, SaveFormat.Docx);
                    Console.WriteLine($"Chart extracted to Word: {chartWordPath}");
                }
            }
            else
            {
                Console.WriteLine("No chart found on the first worksheet.");
            }

            // 5️⃣ Optional: Export only the first worksheet
            Worksheet firstSheet = wb.Worksheets[0];
            Workbook singleSheetWb = new Workbook();
            singleSheetWb.Worksheets.AddCopy(firstSheet);
            string single


## O que você deve aprender a seguir?

- [Como Converter Arquivos Excel para DOCX Usando Aspose.Cells para .NET em C#](/cells/english/net/workbook-operations/convert-excel-to-docx-aspose-csharp/)
- [Como Converter Excel para PDF/A Usando Aspose.Cells para .NET (Guia Abrangente)](/cells/english/net/workbook-operations/convert-excel-to-pdf-a-aspose-cells-dotnet/)
- [Como Converter Excel para PowerPoint Usando Aspose.Cells para .NET: Um Guia Completo](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}