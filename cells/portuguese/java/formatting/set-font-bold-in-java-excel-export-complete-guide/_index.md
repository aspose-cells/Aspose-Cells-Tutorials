---
category: general
date: 2026-06-30
description: Defina a fonte em negrito ao importar um DataTable para o Excel usando
  Java. Aprenda o código de formatação condicional, importe o DataTable para o Excel
  e estilize tabelas sem esforço.
draft: false
keywords:
- set font bold
- conditional formatting code
- import datatable excel
- how to import datatable
- import table with styles
language: pt
og_description: Defina a fonte em negrito em Java ao exportar um DataTable para Excel.
  Este guia aborda código de formatação condicional, importação de DataTable para
  Excel e estilização da tabela.
og_title: Definir fonte em negrito na exportação Excel em Java – Tutorial passo a
  passo
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Set font bold while importing a DataTable to Excel using Java. Learn
    conditional formatting code, import datatable excel and style tables effortlessly.
  headline: Set Font Bold in Java Excel Export – Complete Guide
  type: TechArticle
- description: Set font bold while importing a DataTable to Excel using Java. Learn
    conditional formatting code, import datatable excel and style tables effortlessly.
  name: Set Font Bold in Java Excel Export – Complete Guide
  steps:
  - name: '**Create a mock `DataTable`** that mimics data you’d normally pull from
      a database.'
    text: '**Create a mock `DataTable`** that mimics data you’d normally pull from
      a database.'
  - name: '**Generate a `CellStyle` array** where every even column gets a bold font
      – that’s the core of **set font bold**.'
    text: '**Generate a `CellStyle` array** where every even column gets a bold font
      – that’s the core of **set font bold**.'
  - name: '**Grab the first worksheet** from the workbook.'
    text: '**Grab the first worksheet** from the workbook.'
  - name: '**Import the `DataTable`** with column headers, starting at cell `A1`,
      and apply the prepared styles.'
    text: '**Import the `DataTable`** with column headers, starting at cell `A1`,
      and apply the prepared styles.'
  - name: (Optional) **Add a conditional formatting rule** to illustrate the **conditional
      formatting code** keyword.
    text: (Optional) **Add a conditional formatting rule** to illustrate the **conditional
      formatting code** keyword.
  type: HowTo
tags:
- Java
- Excel
- Aspose.Cells
- DataTable
title: Definir Fonte em Negrito na Exportação de Excel em Java – Guia Completo
url: /pt/java/formatting/set-font-bold-in-java-excel-export-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Definir Fonte em Negrito na Exportação Excel em Java – Guia Completo

Já se perguntou **como definir fonte em negrito** para colunas específicas ao **importar datatable excel**? Você não está sozinho. Muitos desenvolvedores encontram dificuldades quando precisam de uma planilha bem formatada sem ajustar manualmente cada célula. A boa notícia? Com algumas linhas de Java você pode importar um `DataTable`, aplicar fontes em negrito e até incluir um pouco de **conditional formatting code** — tudo programaticamente.

Neste tutorial, percorreremos um exemplo completo e executável que mostra **como importar datatable** para uma pasta de trabalho Excel, aplicar **set font bold** em cada coluna de índice par e, opcionalmente, adicionar um formato condicional simples. Ao final, você terá um trecho pronto para execução e uma compreensão clara de **import table with styles** para qualquer projeto.

## Pré-requisitos

- Java 8 ou mais recente (o código funciona também no Java 17)  
- Aspose.Cells for Java (versão de teste gratuita serve) – adicione a dependência Maven ou o JAR ao seu classpath.  
- Familiaridade básica com a conversão `java.sql` `ResultSet` → `DataTable` (vamos simular uma tabela para simplificar).  
- Uma IDE ou uma ferramenta de build como Maven/Gradle.

> **Dica profissional:** Se você estiver usando Maven, adicione isto ao seu `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- check for the latest version -->
</dependency>
```

## Visão Geral da Solução

1. **Criar um `DataTable` simulado** que imita os dados que você normalmente obteria de um banco de dados.  
2. **Gerar um array de `CellStyle`** onde cada coluna par recebe uma fonte em negrito – esse é o núcleo de **set font bold**.  
3. **Obter a primeira planilha** da pasta de trabalho.  
4. **Importar o `DataTable`** com cabeçalhos de coluna, começando na célula `A1`, e aplicar os estilos preparados.  
5. (Opcional) **Adicionar uma regra de formatação condicional** para ilustrar a palavra‑chave **conditional formatting code**.

Cada passo é explicado em linguagem simples, e os blocos de código são totalmente autônomos para que você possa copiar‑colar e executar imediatamente.

---

## Etapa 1: Recuperar ou Construir o DataTable para Importar

Em aplicativos reais, você provavelmente chamaria utilitários de conversão `ResultSet` → `DataTable`. Para este guia, construiremos um `DataTable` simples manualmente para que você possa focar na parte do Excel.

```java
import com.aspose.cells.*;
import java.util.*;

public class ExcelExportDemo {

    /** Creates a sample DataTable with three columns and a few rows. */
    private static DataTable getDataTable() {
        // Define column names
        List<String> columns = Arrays.asList("ID", "Name", "Score");

        // Create the DataTable and add columns
        DataTable table = new DataTable();
        for (String col : columns) {
            table.getColumns().add(col);
        }

        // Populate rows
        Object[][] rows = {
            {1, "Alice", 85},
            {2, "Bob", 92},
            {3, "Charlie", 78},
            {4, "Diana", 88}
        };

        for (Object[] row : rows) {
            DataRow dr = table.getRows().add();
            for (int i = 0; i < row.length; i++) {
                dr.get(i).setValue(row[i]);
            }
        }
        return table;
    }
```

> **Por que isso importa:** Ter um `DataTable` pronto nos permite focar na API **import datatable excel** e na lógica de estilo. O método acima é reutilizável — basta substituir as linhas codificadas por uma consulta ao banco de dados quando for para produção.

---

## Etapa 2: Preparar Estilos – É Aqui que **Set Font Bold**

Agora vamos construir um array de objetos `CellStyle`, um por coluna. A regra é simples: **set font bold** para cada coluna de índice par (0, 2, 4,…). As colunas ímpares permanecem normais.

```java
    /** Creates a CellStyle array where even columns have a bold font. */
    private static CellStyle[] createColumnStyles(Workbook wb, DataTable table) {
        int columnCount = table.getColumns().size();
        CellStyle[] styles = new CellStyle[columnCount];

        for (int i = 0; i < columnCount; i++) {
            // Create a new style instance for the column
            styles[i] = wb.createStyle();

            // Set the font to bold if the column index is even
            Font font = styles[i].getFont();
            font.setBold(i % 2 == 0);   // <-- this line performs the set font bold action
        }
        return styles;
    }
```

### Por Que Usar um Array de Estilos?

- **Desempenho:** Aplicar um estilo por coluna é mais rápido do que estilizar cada célula individualmente.  
- **Consistência:** Cada célula em uma coluna herda a mesma formatação, garantindo uma aparência uniforme.  
- **Escalabilidade:** Adicionar mais colunas posteriormente requer apenas estender o array — sem reescrever código.

---

## Etapa 3: Acessar a Primeira Planilha na Pasta de Trabalho

Aspose.Cells cria uma planilha padrão para nós, mas é uma boa prática obtê‑la explicitamente. Isso também demonstra **how to import datatable** em uma planilha específica.

```java
    /** Retrieves the first worksheet from the workbook. */
    private static Worksheet getFirstWorksheet(Workbook wb) {
        // Worksheets are zero‑based; index 0 is the first sheet.
        return wb.getWorksheets().get(0);
    }
```

---

## Etapa 4: Importar o DataTable com Estilos – A Operação Central **Import Table With Styles**

O método `importDataTable` faz o trabalho pesado. Ele copia os dados, adiciona cabeçalhos de coluna e aplica o array de estilos que construímos anteriormente.

```java
    /** Imports the DataTable into the worksheet, applying column styles. */
    private static void importTableWithStyles(Worksheet sheet, DataTable table, CellStyle[] styles) {
        // Parameters: (DataTable, import column headers?, start row, start column, styles)
        sheet.getCells().importDataTable(table, true, 0, 0, styles);
    }
```

Ao executar o exemplo, você verá **set font bold** aplicado nas colunas `ID` e `Score`, enquanto `Name` permanece normal.

---

## Etapa 5 (Opcional): Adicionar Formatação Condicional – Um Rápido Exemplo de **Conditional Formatting Code**

Se você quiser destacar linhas onde a pontuação excede 90, algumas linhas extras farão o trabalho. Isso demonstra a palavra‑chave **conditional formatting code** sem desviar o fluxo principal.

```java
    /** Adds a simple conditional format that colors scores > 90 in green. */
    private static void addConditionalFormatting(Worksheet sheet) {
        // Define the range: rows 2‑5 (zero‑based), column C (index 2)
        int firstRow = 1;  // row after header
        int lastRow = sheet.getCells().getMaxDataRow();
        int scoreCol = 2;  // zero‑based index for "Score"

        // Build the range string, e.g., "C2:C5"
        String range = new StyleRegion(firstRow, scoreCol, lastRow, scoreCol).getRefersTo();

        // Create a new conditional formatting collection
        FormatConditionCollection fcc = sheet.getConditionalFormattings().add();

        // Add a condition: cell value > 90
        FormatCondition condition = fcc.addCondition(FormatConditionType.CELL_VALUE, OperatorType.GREATER_THAN, "90", null);
        condition.getStyle().setBackgroundColor(Color.getLightGreen());

        // Apply the condition to the range
        fcc.addArea(new CellArea(firstRow, scoreCol, lastRow, scoreCol));
    }
```

> **Nota:** O trecho acima é opcional, mas demonstra como você pode sobrepor **conditional formatting code** sobre a tabela já formatada.

---

## Juntando Tudo – Exemplo Completo e Executável

```java
import com.aspose.cells.*;
import java.util.*;

public class ExcelExportDemo {

    public static void main(String[] args) throws Exception {
        // 1️⃣ Create a new workbook (in‑memory)
        Workbook wb = new Workbook();

        // 2️⃣ Retrieve the DataTable we want to export
        DataTable dataTable = getDataTable();

        // 3️⃣ Prepare column styles – this is where we set font bold
        CellStyle[] columnStyles = createColumnStyles(wb, dataTable);

        // 4️⃣ Grab the first worksheet
        Worksheet sheet = getFirstWorksheet(wb);

        // 5️⃣ Import the table with headers and our styles
        importTableWithStyles(sheet, dataTable, columnStyles);

        // 6️⃣ OPTIONAL: add a conditional formatting rule
        addConditionalFormatting(sheet);

        // 7️⃣ Save the workbook to disk
        String outPath = "StyledDataTable.xlsx";
        wb.save(outPath, SaveFormat.XLSX);
        System.out.println("Workbook saved to " + outPath);
    }

    // ----- Helper methods from earlier sections -----
    private static DataTable getDataTable() {
        List<String> columns = Arrays.asList("ID", "Name", "Score");
        DataTable table = new DataTable();
        for (String col : columns) {
            table.getColumns().add(col);
        }
        Object[][] rows = {
            {1, "Alice", 85},
            {2, "Bob", 92},
            {3, "Charlie", 78},
            {4, "Diana", 88}
        };
        for (Object[] row : rows) {
            DataRow dr = table.getRows().add();
            for (int i = 0; i < row.length; i++) {
                dr.get(i).setValue(row[i]);
            }
        }
        return table;
    }

    private static CellStyle[] createColumnStyles(Workbook wb, DataTable table) {
        int colCount = table.getColumns().size();
        CellStyle[] styles = new CellStyle[colCount];
        for (int i = 0; i < colCount; i++) {
            styles[i] = wb.createStyle();
            Font font = styles[i].getFont();
            font.setBold(i % 2 == 0);   // set font bold for even columns
        }
        return styles;
    }

    private static Worksheet getFirstWorksheet(Workbook wb) {
        return wb.getWorksheets().get(0);
    }

    private static void importTableWithStyles(Worksheet sheet, DataTable table, CellStyle[] styles) {
        sheet.getCells().importDataTable(table, true, 0, 0, styles);
    }

    private static void addConditionalFormatting(Worksheet sheet


## O Que Você Deve Aprender a Seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Automatizar Formatação Condicional no Excel usando Aspose.Cells para Java: Guia Completo](/cells/english/java/formatting/automate-conditional-formatting-excel-aspose-cells-java/)
- [Como Implementar Configurações de Fonte Personalizadas no Aspose.Cells Java para Formatação de Excel](/cells/english/java/formatting/aspose-cells-java-custom-fonts/)
- [Definir Tamanho da Fonte no Excel usando Aspose.Cells Java - Guia Abrangente](/cells/english/java/formatting/aspose-cells-java-set-font-size-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}