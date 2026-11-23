---
category: general
date: 2026-11-22
description: Aprenda a usar um formato numérico personalizado para formatar uma coluna
  como moeda no Excel usando Java. Defina o formato numérico do Excel rapidamente
  com um estilo simples.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- custom number format
- format column as currency
- set excel number format
- set currency format
- style first column
language: pt
lastmod: 2026-11-22
og_description: Aplique um formato numérico personalizado no Excel com Java. Este
  tutorial mostra como definir o formato numérico do Excel e formatar a primeira coluna
  como moeda.
og_image_alt: Java code snippet that applies a custom number format to an Excel column
og_title: Aplique um formato numérico personalizado no Excel com Java – guia passo
  a passo
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn how to use a custom number format to format a column as currency
    in Excel using Java. Set Excel number format quickly with a simple style.
  headline: How to apply a custom number format in Excel with Java
  type: TechArticle
tags:
- Java
- Excel
- Apache POI
- Spreadsheet Automation
title: Como aplicar um formato numérico personalizado no Excel com Java
url: /pt/java/formatting/how-to-apply-a-custom-number-format-in-excel-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como aplicar um custom number format no Excel com Java

Se você precisa aplicar um **custom number format** a uma coluna em uma planilha Excel, este guia mostra exatamente como fazer isso usando Java. Seja gerando relatórios financeiros ou exportando dados contábeis, formatar a primeira coluna como moeda torna a saída imediatamente legível.

No exemplo abaixo, vamos **format column as currency**, aplicar o estilo à primeira coluna e, em seguida, importar um `DataTable` para a planilha. A mesma abordagem funciona para qualquer formato numérico que você queira exibir.

## O que você aprenderá

* Como criar um **custom number format** com o objeto `Style` do Apache POI.  
* Como **set Excel number format** para uma coluna específica, incluindo o caso de **set currency format**.  
* Como **style first column** ao importar um `DataTable`.  
* Como salvar a pasta de trabalho e verificar se a formatação aparece corretamente.

### Pré-requisitos

* Java 17 ou superior.  
* Apache POI 5.x (a biblioteca que fornece `Workbook`, `Worksheet` e `Style`).  
* Uma implementação de `DataTable` que possa ser iterada como a do exemplo de código.  
* Familiaridade básica com conceitos de Java e Excel.

---

## Etapa 1: Configurar o projeto e importar os dados

Primeiro, adicione o Apache POI ao seu projeto. Se você usa Maven, inclua a dependência a seguir:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>org.apache.poi</groupId>
    <artifactId>poi-ooxml</artifactId>
    <version>5.2.3</version>
</dependency>
```

Em seguida, obtenha os dados de origem como um `DataTable`. Em um cenário real, isso pode vir de uma consulta ao banco de dados, de um arquivo CSV ou de uma resposta de API.

```java
// Step 1: Obtain the source data as a DataTable
DataTable dataTable = getData();   // replace with your own data‑fetching logic
```

> **Dica profissional:** Certifique‑se de que as colunas do `DataTable` tenham os tipos Java corretos (`Integer`, `Double`, etc.) porque o número format só afeta células numéricas.

---

## Etapa 2: Criar um **custom number format** para a primeira coluna

Um **custom number format** indica ao Excel como exibir valores numéricos. Para mostrar valores como moeda, usamos o formato interno `CURRENCY`, mas você também pode definir padrões como `"$#,##0.00"`.

```java
// Step 2: Prepare a Style array – one entry per column in the DataTable
Style[] columnStyles = new Style[dataTable.getColumns().size()];

// Step 3: Create a style for the first column and set it to display values as currency
// wb – existing Workbook instance (e.g., XSSFWorkbook for .xlsx files)
Workbook wb = new XSSFWorkbook();
columnStyles[0] = wb.createCellStyle();               // style first column
columnStyles[0].setDataFormat(
        wb.createDataFormat().getFormat(Style.CustomNumberFormat.CURRENCY));
```

**Por que isso funciona:**  
* `createCellStyle()` retorna um objeto de estilo reutilizável.  
* `setDataFormat()` associa o **set currency format** ao estilo, que o Excel então aplica a cada célula que usa esse estilo.  
* Ao armazenar o estilo em `columnStyles[0]` garantimos que somente a primeira coluna receba a formatação de moeda.

---

## Etapa 3: Importar o `DataTable` aplicando os estilos de coluna

Agora importamos os dados para a planilha. O método `importDataTable` aceita o array de estilos, permitindo que **style first column** e deixando as demais colunas com formatação padrão.

```java
// Step 4: Import the DataTable into the worksheet, applying the column styles
// ws – existing Worksheet instance
Worksheet ws = wb.createSheet("Report");

// true  → import column headers
// 0,0   → start at cell A1
ws.getCells().importDataTable(dataTable, true, 0, 0, columnStyles);
```

A chamada acima **sets Excel number format** apenas para a primeira coluna. Todas as outras colunas herdam o estilo padrão da pasta de trabalho, o que mantém o código simples e eficiente.

---

## Etapa 4: Salvar a pasta de trabalho e verificar o resultado

Finalmente, grave a pasta de trabalho em um arquivo e abra-a no Excel para confirmar que a primeira coluna exibe símbolos de moeda.

```java
// Step 5: Save the workbook to disk
try (FileOutputStream fileOut = new FileOutputStream("FormattedReport.xlsx")) {
    wb.write(fileOut);
}
System.out.println("Workbook saved as FormattedReport.xlsx");
```

**Saída esperada:**  
Ao abrir *FormattedReport.xlsx*, os valores na coluna A aparecem com o símbolo de moeda apropriado (por exemplo, `$1,234.00`). Todas as outras colunas mantêm sua representação numérica original.

---

## Variações comuns e casos de borda

| Situação | Ajuste |
|-----------|------------|
| **Moeda diferente** (por exemplo, Euro) | Substitua `Style.CustomNumberFormat.CURRENCY` por um padrão personalizado: <br>`wb.createDataFormat().getFormat("\"€\"#,##0.00")` |
| **Mais de uma coluna estilizada** | Preencha entradas adicionais em `columnStyles[]` com seus próprios objetos `CellStyle`. |
| **Conjuntos de dados grandes** | Use `importDataTable` em lotes ou faça streaming de linhas para evitar `OutOfMemoryError`. |
| **Separadores específicos de localidade** | Use `java.text.NumberFormat` para gerar um padrão sensível à localidade e passe‑o para `setDataFormat`. |

> **Atenção:** Reutilizar um único objeto `CellStyle` em muitas colunas pode causar formatação inesperada porque o Excel limita o número de estilos distintos por pasta de trabalho. Crie um estilo separado para cada formato exclusivo que você precisar.

---

## Exemplo completo executável

Abaixo está um programa autônomo que demonstra todo o fluxo de trabalho, desde a criação dos dados até a gravação da pasta de trabalho formatada.

```java
import java.io.FileOutputStream;
import java.util.ArrayList;
import java.util.List;

import org.apache.poi.ss.usermodel.*;
import org.apache.poi.xssf.usermodel.XSSFWorkbook;

/* Mock DataTable implementation for demonstration purposes */
class DataTable {
    private final List<String> columns = List.of("Amount", "Description");
    private final List<Object[]> rows = new ArrayList<>();

    public DataTable() {
        rows.add(new Object[]{1234.5, "Consulting"});
        rows.add(new Object[]{5678.9, "Licensing"});
    }

    public List<String> getColumns() { return columns; }
    public List<Object[]> getRows() { return rows; }
}

/* Helper that mimics the importDataTable method used in the original snippet */
class WorksheetHelper {
    private final Sheet sheet;
    private final Workbook wb;

    public WorksheetHelper(Workbook wb, Sheet sheet) {
        this.wb = wb;
        this.sheet = sheet;
    }

    public void importDataTable(DataTable dt, boolean includeHeaders,
                                int startRow, int startCol, Style[] styles) {
        int rowIdx = startRow;
        if (includeHeaders) {
            Row header = sheet.createRow(rowIdx++);
            for (int c = 0; c < dt.getColumns().size(); c++) {
                Cell cell = header.createCell(startCol + c);
                cell.setCellValue(dt.getColumns().get(c));
            }
        }
        for (Object[] rowData : dt.getRows()) {
            Row row = sheet.createRow(rowIdx++);
            for (int c = 0; c < rowData.length; c++) {
                Cell cell = row.createCell(startCol + c);
                Object value = rowData[c];
                if (value instanceof Number) {
                    cell.setCellValue(((Number) value).doubleValue());
                } else {
                    cell.setCellValue(value.toString());
                }
                // Apply custom style if provided
                if (styles != null && c < styles.length && styles[c] != null) {
                    cell.setCellStyle((CellStyle) styles[c]);
                }
            }
        }
    }
}

/* Main class that puts everything together */
public class CustomNumberFormatDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Obtain the source data
        DataTable dataTable = new DataTable();

        // 2️⃣ Create a workbook and a sheet
        Workbook wb = new XSSFWorkbook();
        Sheet ws = wb.createSheet("Report");

        // 3️⃣ Prepare a style array – one entry per column
        Style[] columnStyles = new Style[dataTable.getColumns().size()];

        // 4️⃣ Create a style for the first column (currency)
        CellStyle currencyStyle = wb.createCellStyle();
        DataFormat fmt = wb.createDataFormat();
        currencyStyle.setDataFormat(fmt.getFormat("$#,##0.00"));
        columnStyles[0] = currencyStyle;   // style first column

        // 5️⃣ Import the DataTable, applying the column styles
        WorksheetHelper helper = new WorksheetHelper(wb, ws);
        helper.importDataTable(dataTable, true, 0, 0, columnStyles);

        // 6️⃣ Save the workbook
        try (FileOutputStream out = new FileOutputStream("FormattedReport.xlsx")) {
            wb.write(out);
        }
        System.out.println("Workbook written to FormattedReport.xlsx");
    }
}
```

Executar o programa cria **FormattedReport.xlsx**, onde a coluna A (a coluna “Amount”) é exibida com um **custom number format** que mostra o símbolo de dólar e duas casas decimais.

---

## Conclusão

Agora você sabe como **custom number format** uma planilha Excel a partir do Java, **format column as currency**, e **style first column** ao importar dados. Ao criar um `CellStyle` reutilizável e passá‑lo para `importDataTable`, você pode **set Excel number format** para qualquer coluna sem percorrer cada célula manualmente.

Next, try:

* Usar `setDataFormat` com padrões específicos de localidade para **set currency format**

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Definir Formato Numérico Excel em Java – Guia Completo](/cells/english/java/formatting/set-number-format-excel-in-java-complete-guide/)
- [Aplicar Formato Numérico Excel em Java – Guia Completo Aspose.Cells](/cells/english/java/formatting/apply-number-format-excel-in-java-complete-aspose-cells-guid/)
- [Como criar uma pasta de trabalho Excel com formato de moeda e fonte em negrito em Java](/cells/english/java/formatting/how-to-create-excel-workbook-with-currency-format-and-bold-f/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}