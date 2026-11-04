---
category: general
date: 2026-10-20
description: Como salvar PDF a partir de uma pasta de trabalho do Excel usando Aspose.Cells,
  expandir intervalos dinâmicos, importar Markdown para o Excel e preservar seletores
  de variação de fonte.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to save pdf
- save workbook as pdf
- markdown to excel
- dynamic range formula
- how to import markdown
language: pt
lastmod: 2026-10-20
og_description: Como salvar PDF a partir de uma pasta de trabalho do Excel com Aspose.Cells,
  usando fórmulas de intervalo dinâmico, preservando seletores de variação de fonte
  e importando Markdown para o Excel.
og_image_alt: Screenshot showing how to save PDF from an Excel workbook with dynamic
  range and Markdown import
og_title: Como salvar PDF de uma pasta de trabalho do Excel – guia completo do Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-10-20'
  description: How to save PDF from an Excel workbook using Aspose.Cells, expand dynamic
    ranges, import Markdown to Excel, and preserve font variation selectors.
  headline: How to save PDF from an Excel workbook with Aspose.Cells
  type: TechArticle
- description: How to save PDF from an Excel workbook using Aspose.Cells, expand dynamic
    ranges, import Markdown to Excel, and preserve font variation selectors.
  name: How to save PDF from an Excel workbook with Aspose.Cells
  steps:
  - name: '**Dynamic range formula** – use the new `EXPAND` function to create a resizable
      range.'
    text: '**Dynamic range formula** – use the new `EXPAND` function to create a resizable
      range.'
  - name: '**Save workbook as PDF** – configure `PdfSaveOptions` so the output keeps
      font variation selectors.'
    text: '**Save workbook as PDF** – configure `PdfSaveOptions` so the output keeps
      font variation selectors.'
  - name: '**Markdown to Excel** – import a Markdown file that may contain Base‑64‑encoded
      images.'
    text: '**Markdown to Excel** – import a Markdown file that may contain Base‑64‑encoded
      images.'
  - name: '**Smart Marker with IF** – generate a report that evaluates a condition
      for each row.'
    text: '**Smart Marker with IF** – generate a report that evaluates a condition
      for each row.'
  - name: '`VarSel.pdf` – a PDF that shows the expanded range `B1:B5` and retains
      any emoji or special glyphs.'
    text: '`VarSel.pdf` – a PDF that shows the expanded range `B1:B5` and retains
      any emoji or special glyphs.'
  - name: '`doc.md` content appears as a regular worksheet, with images rendered in
      the correct cells.'
    text: '`doc.md` content appears as a regular worksheet, with images rendered in
      the correct cells.'
  - name: Column **C** in the final worksheet contains **Pass** for Alice and Charlie
    text: Column **C** in the final worksheet contains **Pass** for Alice and Charlie
  type: HowTo
tags:
- Aspose.Cells
- PDF
- Excel
- Markdown
- Smart Marker
title: Como salvar PDF de uma pasta de trabalho Excel com Aspose.Cells
url: /pt/net/conversion-to-pdf/how-to-save-pdf-from-an-excel-workbook-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como salvar PDF a partir de uma pasta de trabalho Excel com Aspose.Cells

Se você precisa **como salvar PDF** a partir de uma pasta de trabalho Excel, este guia mostra um fluxo de trabalho pronto para produção usando Aspose.Cells para .NET. Você aprenderá a expandir dinamicamente um intervalo, preservar seletores de variação de fonte Unicode ao salvar, importar um documento Markdown diretamente para uma planilha e aplicar lógica de Smart Marker com expressões condicionais.

O tutorial cobre quatro cenários práticos:

1. **Fórmula de intervalo dinâmico** – use a nova função `EXPAND` para criar um intervalo redimensionável.  
2. **Salvar pasta de trabalho como PDF** – configure `PdfSaveOptions` para que a saída mantenha os seletores de variação de fonte.  
3. **Markdown para Excel** – importe um arquivo Markdown que pode conter imagens codificadas em Base‑64.  
4. **Smart Marker com IF** – gere um relatório que avalia uma condição para cada linha.

Você só precisa de uma versão recente do .NET (≥ 4.6) e de uma licença válida do Aspose.Cells. Nenhuma ferramenta externa é necessária.

![Como salvar PDF a partir de uma pasta de trabalho Excel](/images/save-pdf-workbook.png){alt="Como salvar PDF a partir de uma pasta de trabalho Excel usando Aspose.Cells"}

## Pré‑requisitos

- Visual Studio 2022 ou qualquer IDE C#.  
- Aspose.Cells para .NET (pacote NuGet `Aspose.Cells`).  
- Uma pasta chamada `YOUR_DIRECTORY` onde os arquivos gerados serão gravados.  
- Opcional: um arquivo Markdown (`doc.md`) que contém uma tabela e imagens Base‑64.

---

## Usando uma fórmula de intervalo dinâmico com a função EXPAND

Uma **fórmula de intervalo dinâmico** permite referenciar um bloco de células que pode crescer ou diminuir em tempo de execução. A função `EXPAND` introduzida nas versões recentes do Excel é totalmente suportada pelo Aspose.Cells.

```csharp
// Step 1: Create a workbook and populate a simple list
Workbook workbook = new Workbook();
Worksheet sheet = workbook.Worksheets[0];

sheet.Cells["A1"].PutValue(1);
sheet.Cells["A2"].PutValue(2);
sheet.Cells["A3"].PutValue(3);

// Expand A1:A3 to 5 rows and 1 column using EXPAND
sheet.Cells["B1"].Formula = "=EXPAND(A1:A3, 5, 1)";
sheet.Calculate(); // Forces evaluation of the formula
```

**Por que usar EXPAND?**  
Quando o tamanho dos dados de origem muda, você evita ajustar manualmente o intervalo de destino. No exemplo acima, `B1:B5` conterá os valores `1, 2, 3, 0, 0` após o cálculo, preenchendo automaticamente as linhas extras com zeros.

> **Dica profissional:** Se precisar de uma expansão bidimensional, passe os argumentos `rows` e `columns`, por exemplo, `=EXPAND(A1:B2, 10, 5)`.

---

## Como salvar PDF a partir de uma pasta de trabalho com seletores de variação de fonte

Salvar uma pasta de trabalho como PDF é simples, mas preservar **seletores de variação de fonte** (usados para emojis e scripts complexos) requer um pequeno ajuste de opção. Este é o núcleo do requisito **salvar pasta de trabalho como PDF**.

```csharp
// Step 2: Configure PDF options to keep variation selectors
PdfSaveOptions pdfOptions = new PdfSaveOptions
{
    // When true, the PDF keeps Unicode variation selector characters
    FontVariationSelectors = true
};

// Save the workbook that now contains the expanded range
workbook.Save("YOUR_DIRECTORY/VarSel.pdf", pdfOptions);
```

**O que acontece nos bastidores?**  
`PdfSaveOptions.FontVariationSelectors` indica ao renderizador que escreva os pontos de código Unicode originais em vez de removê‑los. O PDF resultante exibe exatamente os glifos que você vê no Excel, o que é essencial para idiomas que dependem desses seletores.

> **Pergunta comum:** *O tamanho do arquivo aumentará?*  
Apenas marginalmente, pois os bytes extras fazem parte do fluxo de texto. O ganho em fidelidade visual supera o impacto no tamanho para a maioria das aplicações.

---

## Markdown para Excel: importando um arquivo Markdown

O recurso **markdown to excel** permite transformar um documento Markdown em uma planilha totalmente preenchida. Aspose.Cells analisa tabelas, listas e até imagens codificadas em Base‑64.

```csharp
// Step 3: Load a Markdown file directly into a new workbook
Workbook markdownWorkbook = new Workbook();
markdownWorkbook.ImportMarkdown("YOUR_DIRECTORY/doc.md");

// The first worksheet now mirrors the Markdown structure
Worksheet mdSheet = markdownWorkbook.Worksheets[0];
```

**Como funciona a importação?**  

| Elemento Markdown | Representação no Excel |
|-------------------|------------------------|
| Linhas de tabela  | Linhas da planilha      |
| Imagens inline (Base‑64) | Objetos de imagem incorporados |
| Cabeçalhos (`#`)  | Valores de célula em negrito com fonte maior |

Se `doc.md` contiver uma tabela como:

```markdown
| Name | Score |
|------|-------|
| Alice | 92 |
| Bob   | 78 |
```

a planilha resultante terá o mesmo layout de duas colunas pronto para processamento adicional.

> **Caso extremo:** Quando o arquivo Markdown contém tabelas malformadas, Aspose.Cells registra um aviso e ignora as linhas problemáticas, permitindo que o restante do documento seja carregado sem interrupção.

---

## Smart Marker com lógica condicional e dados variáveis

Smart Marker é o mecanismo de templating do Aspose.Cells. Ele substitui marcadores como `{Name}` por dados de um `DataTable`. Adicionar uma expressão `IF` permite incorporar texto condicional diretamente no template.

```csharp
// Step 4: Prepare a sheet with Smart Marker tags
Worksheet smSheet = markdownWorkbook.Worksheets[0];
smSheet.Cells["A1"].PutValue("{Name}");
smSheet.Cells["B1"].PutValue("{Score}");
smSheet.Cells["C1"].PutValue("{IF(Score>80,\"Pass\",\"Fail\")}");

// Simulated data source
DataTable scores = GetScoreTable(); // Returns columns Name (string) and Score (int)

// Process the markers – each row becomes a new line in the sheet
smSheet.SmartMarkerProcessor.Process(scores);
```

**Por que usar IF dentro do Smart Marker?**  
Elimina a necessidade de código de pós‑processamento. A expressão `IF(Score>80,"Pass","Fail")` é avaliada por linha, gravando **Pass** para pontuações acima de 80 e **Fail** caso contrário.

> **Dica profissional:** Combine múltiplas condições com `AND`/`OR` dentro da mesma tag `{IF}`, por exemplo, `{IF(Score>80 AND Attendance>90,"Excellent","Review")}`.

---

## Exemplo completo de ponta a ponta

Juntando todas as peças, obtém‑se um programa único e executável:

```csharp
using Aspose.Cells;
using System.Data;

class Program
{
    static void Main()
    {
        // 1️⃣ Dynamic range with EXPAND
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];
        ws.Cells["A1"].PutValue(1);
        ws.Cells["A2"].PutValue(2);
        ws.Cells["A3"].PutValue(3);
        ws.Cells["B1"].Formula = "=EXPAND(A1:A3, 5, 1)";
        ws.Calculate();

        // 2️⃣ Save as PDF while preserving variation selectors
        PdfSaveOptions pdfOpts = new PdfSaveOptions { FontVariationSelectors = true };
        wb.Save("YOUR_DIRECTORY/VarSel.pdf", pdfOpts);

        // 3️⃣ Import Markdown (markdown to excel)
        Workbook mdWb = new Workbook();
        mdWb.ImportMarkdown("YOUR_DIRECTORY/doc.md");
        Worksheet mdWs = mdWb.Worksheets[0];

        // 4️⃣ Smart Marker with IF condition
        mdWs.Cells["A1"].PutValue("{Name}");
        mdWs.Cells["B1"].PutValue("{Score}");
        mdWs.Cells["C1"].PutValue("{IF(Score>80,\"Pass\",\"Fail\")}");

        DataTable scores = GetScoreTable(); // Implement this helper as shown below
        mdWs.SmartMarkerProcessor.Process(scores);

        // Optional: save the final workbook
        mdWb.Save("YOUR_DIRECTORY/FinalReport.xlsx");
    }

    // Helper that creates a sample DataTable
    static DataTable GetScoreTable()
    {
        DataTable dt = new DataTable();
        dt.Columns.Add("Name", typeof(string));
        dt.Columns.Add("Score", typeof(int));

        dt.Rows.Add("Alice", 92);
        dt.Rows.Add("Bob", 78);
        dt.Rows.Add("Charlie", 85);
        return dt;
    }
}
```

**Saída esperada**

1. `VarSel.pdf` – um PDF que mostra o intervalo expandido `B1:B5` e mantém quaisquer emojis ou glifos especiais.  
2. O conteúdo de `doc.md` aparece como uma planilha regular, com imagens renderizadas nas células corretas.  
3. A coluna **C** na planilha final contém **Pass** para Alice e Charlie


## O que você deve aprender a seguir?


Os tutoriais a seguir abordam tópicos estreitamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [How to Save Specific Pages of an Excel File as PDF Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/save-specific-excel-pages-pdf-aspose-cells-net/)
- [Save Excel Workbook as PDF with Custom Fonts using Aspose.Cells for .NET](/cells/english/net/workbook-operations/save-excel-workbook-pdf-custom-fonts-aspose-cells-net/)
- [How to Export PDF from Excel – Complete Guide to Save Workbook as PDF](/cells/english/net/conversion-to-pdf/how-to-export-pdf-from-excel-complete-guide-to-save-workbook/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}