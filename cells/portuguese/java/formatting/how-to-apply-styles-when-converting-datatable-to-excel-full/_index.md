---
category: general
date: 2026-06-21
description: Como aplicar estilos ao converter DataTable para Excel em Java. Aprenda
  a importar DataTable para Excel, adicionar estilos personalizados ao Excel e salvar
  a pasta de trabalho em um arquivo em minutos.
draft: false
keywords:
- how to apply styles
- convert datatable to excel
- save workbook to file
- add custom styles excel
- import datatable to excel
language: pt
og_description: Como aplicar estilos ao converter DataTable para Excel em Java. Este
  guia mostra como importar a DataTable para o Excel, adicionar estilos personalizados
  ao Excel e salvar a pasta de trabalho em um arquivo.
og_title: Como aplicar estilos ao converter DataTable para Excel – Tutorial Java
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: How to apply styles while converting DataTable to Excel in Java. Learn
    to import datatable to excel, add custom styles excel, and save workbook to file
    in minutes.
  headline: How to Apply Styles When Converting DataTable to Excel – Full Java Guide
  type: TechArticle
- description: How to apply styles while converting DataTable to Excel in Java. Learn
    to import datatable to excel, add custom styles excel, and save workbook to file
    in minutes.
  name: How to Apply Styles When Converting DataTable to Excel – Full Java Guide
  steps:
  - name: 5.1 Conditional Formatting Instead of Fixed Styles
    text: If you need to highlight rows where `Score > 90`, you can add a `ConditionalFormattingCollection`
      after the import. This gives you dynamic coloring without hard‑coding extra
      styles.
  - name: 5.2 Merging Cells for Titles
    text: Sometimes a report needs a big title spanning multiple columns. Use `worksheet.getCells().merge(0,
      0, 1, 3)` and then apply a distinct style to that merged region.
  - name: 5.3 Large DataSets – Performance Considerations
    text: When dealing with >100k rows, set `ImportDataTableOptions` to `ImportDataTableOptions.NO_FORMATTING`
      first, then apply styles in a second pass. This avoids the overhead of styling
      each cell during import.
  - name: 5.4 Multi‑Sheet Export
    text: If you have several `DataTable`s, just create additional worksheets via
      `workbook.getWorksheets().add("Sheet2")` and repeat the **import datatable to
      excel** step for each sheet.
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel
- DataTable
title: Como Aplicar Estilos ao Converter DataTable para Excel – Guia Completo em Java
url: /pt/java/formatting/how-to-apply-styles-when-converting-datatable-to-excel-full/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Aplicar Estilos ao Converter DataTable para Excel – Guia Completo em Java

Já se perguntou **como aplicar estilos** quando precisa **converter DataTable para Excel**? Você não está sozinho. Em muitas ferramentas internas extraímos dados de bancos de dados, colocamos em um `DataTable` e então esperamos uma planilha bonita sem nenhum trabalho extra. Spoiler: você precisa dizer à biblioteca *exatamente* o que “bonito” significa.

Neste tutorial vamos percorrer um exemplo completo, pronto‑para‑executar, que mostra **como aplicar estilos** usando Aspose.Cells for Java, importar um `DataTable` para Excel, **adicionar estilos personalizados estilo Excel**, e finalmente **salvar a pasta de trabalho em arquivo**. Ao final, você terá um trecho reutilizável que pode ser inserido em qualquer projeto.

---

## O que Você Precisa

- **Java 17** (ou qualquer JDK recente) – o código funciona também em Java 8+.  
- **Aspose.Cells for Java** JAR (a versão de teste gratuita serve para testes).  
- Uma fonte `DataTable` – vamos simular uma simples, mas você pode substituir por qualquer resultado de consulta real.  
- Uma IDE de sua preferência (IntelliJ, Eclipse, VS Code… você escolhe).

Nenhuma ferramenta de build extra é necessária; um simples `pom.xml` do Maven basta, mas você também pode adicionar o JAR manualmente.

---

## Etapa 1: Configurar o Projeto e as Dependências

Primeiro de tudo—vamos colocar a biblioteca no classpath.

```xml
<!-- pom.xml snippet -->
<dependencies>
    <dependency>
        <groupId>com.aspose</groupId>
        <artifactId>aspose-cells</artifactId>
        <version>24.9</version> <!-- check the latest version -->
    </dependency>
</dependencies>
```

Se você não estiver usando Maven, basta colocar o `aspose-cells-24.9.jar` na pasta `libs` e adicioná‑lo ao caminho de compilação.

> **Dica profissional:** Aspose fornece uma classe `License`. Registre sua licença logo no início, ou você verá marcas d’água no arquivo de saída.

```java
import com.aspose.cells.*;

public class ExcelExporter {
    static {
        try {
            License license = new License();
            license.setLicense("Aspose.Cells.lic"); // place your license file in resources
        } catch (Exception e) {
            System.out.println("License not found – running in evaluation mode.");
        }
    }
    // …rest of the class
}
```

Agora estamos prontos para falar sobre **como aplicar estilos**.

---

## Etapa 2: Criar Estilos Personalizados para Excel

A magia de uma planilha bem polida está nos estilos de célula. Aspose permite definir um objeto `Style`, ajustar fontes, cores, bordas e reutilizá‑lo onde quiser. Abaixo está uma forma compacta de **adicionar estilos personalizados estilo Excel**.

```java
/**
 * Builds an array of two custom styles:
 * 1. Header style – bold, gray background, centered.
 * 2. Data style   – thin borders, left‑aligned.
 */
private static Style[] buildImportStyles(Workbook workbook) {
    // Header style
    Style headerStyle = workbook.createStyle();
    Font headerFont = headerStyle.getFont();
    headerFont.setBold(true);
    headerFont.setColor(Color.getWhite());
    headerStyle.setPattern(BackgroundType.SOLID);
    headerStyle.setBackgroundColor(Color.getGray25());
    headerStyle.setHorizontalAlignment(TextAlignmentType.CENTER);
    headerStyle.setVerticalAlignment(TextAlignmentType.CENTER);

    // Data style
    Style dataStyle = workbook.createStyle();
    dataStyle.setBorder(BorderType.LEFT_BORDER, CellBorderType.THIN, Color.getBlack());
    dataStyle.setBorder(BorderType.RIGHT_BORDER, CellBorderType.THIN, Color.getBlack());
    dataStyle.setBorder(BorderType.TOP_BORDER, CellBorderType.THIN, Color.getBlack());
    dataStyle.setBorder(BorderType.BOTTOM_BORDER, CellBorderType.THIN, Color.getBlack());
    dataStyle.setHorizontalAlignment(TextAlignmentType.LEFT);
    dataStyle.setVerticalAlignment(TextAlignmentType.CENTER);

    return new Style[] { headerStyle, dataStyle };
}
```

Observe como criamos **dois estilos distintos**—um para os cabeçalhos de coluna e outro para as linhas de dados. Você pode estender esse array com quantos estilos precisar; Aspose os aplicará na ordem em que você chamar `importDataTable`.

---

## Etapa 3: Importar DataTable para a Planilha

Agora vem a parte que realmente **importa datatable para excel**. O método `importDataTable` recebe o `DataTable` de origem, um sinalizador para cabeçalhos de coluna, a linha/coluna inicial e o array de estilos que acabamos de montar.

```java
public static void exportDataTableToExcel(DataTable dataTable, String outputPath) throws Exception {
    // 1️⃣ Create a new workbook and grab the first worksheet
    Workbook workbook = new Workbook();
    Worksheet worksheet = workbook.getWorksheets().get(0);

    // 2️⃣ Build the custom styles (header + data)
    Style[] importStyles = buildImportStyles(workbook);

    // 3️⃣ Import the DataTable – start at A1 (0,0), keep column names, apply styles
    worksheet.getCells().importDataTable(dataTable, true, 0, 0, importStyles);

    // 4️⃣ Auto‑fit columns for a tidy look
    worksheet.autoFitColumns();

    // 5️⃣ Finally, **save workbook to file**
    workbook.save(outputPath);
}
```

Uma observação rápida: o argumento `true` indica ao Aspose que deve **preservar os cabeçalhos de coluna**—esse é o caso típico quando você quer um relatório legível. Se definir como `false`, a primeira linha de dados se tornará o cabeçalho.

---

## Etapa 4: Unir Tudo – Um Exemplo Minimalista Funcional

A seguir está um método `main` autônomo que cria um `DataTable` fictício, chama a rotina de exportação e grava `output.xlsx` na pasta `./results`.

```java
import com.aspose.cells.*;
import java.util.*;

public class ExcelExporter {

    // (License block omitted for brevity – see Step 1)

    public static void main(String[] args) throws Exception {
        // Mock a DataTable – replace this with your real DB call
        DataTable dataTable = createSampleDataTable();

        // Define where the Excel file should land
        String outputPath = "results/output.xlsx";

        // Perform the conversion and styling
        exportDataTableToExcel(dataTable, outputPath);

        System.out.println("Excel file generated at: " + outputPath);
    }

    /** Helper that builds a simple DataTable with three columns */
    private static DataTable createSampleDataTable() {
        DataTable dt = new DataTable();
        dt.getColumns().add("ID", CellValueType.INTEGER);
        dt.getColumns().add("Name", CellValueType.STRING);
        dt.getColumns().add("Score", CellValueType.DOUBLE);

        // Add a few rows
        dt.getRows().add(new Object[] {1, "Alice", 85.5});
        dt.getRows().add(new Object[] {2, "Bob", 92.0});
        dt.getRows().add(new Object[] {3, "Charlie", 78.3});
        return dt;
    }

    // (Style builder and export method from Steps 2‑3 go here)
}
```

**Saída esperada:** Abra `output.xlsx` e você verá uma linha de cabeçalho em negrito e cinza, células de dados com bordas finas e colunas dimensionadas automaticamente para caber o conteúdo. Isso demonstra exatamente **como aplicar estilos** para que a planilha pareça profissional.

![How to apply styles in Excel workbook](/images/excel-styles.png){alt="como aplicar estilos em uma pasta de trabalho Excel"}

*(A captura de tela mostra o cabeçalho em negrito cinza e as linhas de dados com bordas finas.)*

---

## Etapa 5: Dicas Avançadas & Casos de Borda

### 5.1 Formatação Condicional em vez de Estilos Fixos  
Se precisar destacar linhas onde `Score > 90`, você pode adicionar um `ConditionalFormattingCollection` após a importação. Isso fornece coloração dinâmica sem codificar estilos extras.

```java
FormatConditionCollection fcc = worksheet.getConditionalFormattings().add();
FormatCondition fc = fcc.addCondition(FormatConditionType.CELL_VALUE, OperatorType.GREATER_THAN, "90");
fc.getStyle().setBackgroundColor(Color.getLightGreen());
```

### 5.2 Mesclar Células para Títulos  
Às vezes um relatório precisa de um título grande que ocupe várias colunas. Use `worksheet.getCells().merge(0, 0, 1, 3)` e então aplique um estilo distinto à região mesclada.

### 5.3 Conjuntos de Dados Grandes – Considerações de Performance  
Ao lidar com >100 k linhas, defina `ImportDataTableOptions` como `ImportDataTableOptions.NO_FORMATTING` primeiro, depois aplique os estilos em uma segunda passagem. Isso evita a sobrecarga de formatar cada célula durante a importação.

### 5.4 Exportação Multi‑Planilha  
Se você tem vários `DataTable`s, basta criar planilhas adicionais via `workbook.getWorksheets().add("Sheet2")` e repetir a etapa **importar datatable para excel** para cada planilha.

---

## Conclusão

Cobremos **como aplicar estilos** do início ao fim: configurando Aspose.Cells, construindo **estilos personalizados estilo Excel**, **importando datatable para excel**, e finalmente **salvando a pasta de trabalho em arquivo**. O código completo está pronto para copiar‑colar, e as dicas extras fornecem um roteiro para relatórios mais sofisticados.

Em seguida, você pode explorar **adicionar estilos personalizados excel** para gráficos, ou experimentar **converter datatable para excel** em um endpoint REST Spring Boot. De qualquer forma, agora você tem uma base sólida para transformar tabelas brutas em planilhas polidas—sem necessidade de formatação manual.

Tem perguntas

## O que Você Deve Aprender a Seguir?

Os tutoriais abaixo abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [How to Apply Styles to Excel Cells Using Aspose.Cells for Java - Complete Guide](/cells/english/java/formatting/apply-styles-excel-aspose-cells-java/)
- [Merge Cells & Apply Styles in Excel using Aspose.Cells for Java - A Complete Guide](/cells/english/java/formatting/merge-cells-apply-styles-aspose-cells-java/)
- [How to Import DataTable into Excel Using Aspose.Cells for .NET (Step-by-Step Guide)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}