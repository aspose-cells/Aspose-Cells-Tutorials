---
category: general
date: 2026-08-14
description: Como definir delimitador e salvar como CSV usando Aspose.Cells, limitar
  dígitos, exportar strings CSV e recalcular fórmulas em Java.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set delimiter
- save as csv
- recalculate formulas
- how to export csv
- how to limit digits
language: pt
lastmod: 2026-08-14
og_description: Como definir delimitador e salvar como CSV com Aspose.Cells, limitar
  dígitos, exportar strings CSV e recalcular fórmulas em Java.
og_image_alt: Screenshot of Java code that sets a CSV delimiter and saves an Excel
  workbook as CSV using Aspose.Cells
og_title: Como definir delimitador e salvar como CSV – Guia Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: How to set delimiter and save as CSV using Aspose.Cells, limit digits,
    export CSV strings, and recalculate formulas in Java.
  headline: How to set delimiter and save as CSV with Aspose.Cells
  type: TechArticle
- description: How to set delimiter and save as CSV using Aspose.Cells, limit digits,
    export CSV strings, and recalculate formulas in Java.
  name: How to set delimiter and save as CSV with Aspose.Cells
  steps:
  - name: Why this works
    text: "- `CsvSaveOptions.setDelimiter(char)` tells Aspose.Cells which character
      separates fields. By default it’s a comma, but any character (tab `'\t'`, pipe
      `'|'`, etc.) works. - `setSignificantDigits(int)` limits numeric precision,
      satisfying the **how to limit digits** requirement without manually form"
  - name: When to use this
    text: '- Returning CSV from a REST endpoint (`@RestController` in Spring) - Embedding
      CSV data into an email attachment without writing to disk - Performing quick
      sanity checks during unit tests'
  - name: Why recalculate?
    text: '- Formulas may reference external data or volatile functions (`NOW()`,
      `RAND()`) that need fresh values. - Dynamic‑array formulas (e.g., `=SORT(A1:A10)`)
      are evaluated automatically, but calling `calculateFormula()` guarantees consistency
      across all sheets.'
  - name: Verifying the result
    text: 1. Open `output.csv` in a text editor – you should see a semicolon (`;`)
      separating each column. 2. Confirm that numeric columns display at most five
      significant digits. 3. The console output will print the CSV string generated
      in step 4. 4. Open `japan_updated.xlsx` in Excel – any formulas that pre
  type: HowTo
tags:
- Aspose.Cells
- Java
- CSV export
- Excel automation
title: Como definir delimitador e salvar como CSV com Aspose.Cells
url: /pt/java/excel-import-export/how-to-set-delimiter-and-save-as-csv-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como definir delimitador e salvar como CSV com Aspose.Cells

Se você precisa **definir delimitador** ao exportar dados de uma pasta de trabalho do Excel, este guia mostra uma solução completa, de ponta a ponta, usando Aspose.Cells para Java. Você aprenderá como configurar o delimitador CSV, limitar o número de dígitos significativos, exportar uma string CSV e atualizar fórmulas de matriz dinâmica após carregar uma pasta de trabalho.

O tutorial cobre tudo o que você precisa para executar o código na sua máquina, incluindo o tratamento de calendários especiais, como o reinado do Imperador japonês. Ao final, você será capaz de gerar arquivos CSV precisos, controlar a precisão numérica e garantir que as fórmulas estejam atualizadas.

## Pré‑requisitos

- Java 17 ou superior (o código também compila com JDK 11+)
- Aspose.Cells para Java 23.9 ou mais recente – faça o download no [site da Aspose](https://products.aspose.com/cells/java/)
- Familiaridade básica com Maven ou Gradle para gerenciamento de dependências
- Uma IDE (IntelliJ IDEA, Eclipse, VS Code) ou um editor de texto simples e linha de comando

> **Dica:** Use uma pasta dedicada `libs` ou o Maven Central para manter o JAR do Aspose.Cells no seu classpath. Os exemplos abaixo assumem um projeto Maven.

## Etapa 1: Configurar o projeto Maven

Crie um `pom.xml` com a dependência do Aspose.Cells:

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" 
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 
                             http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>aspose-csv-demo</artifactId>
    <version>1.0.0</version>
    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
    </properties>

    <dependencies>
        <dependency>
            <groupId>com.aspose</groupId>
            <artifactId>aspose-cells</artifactId>
            <version>23.9</version>
            <classifier>jdk17</classifier>
        </dependency>
    </dependencies>
</project>
```

Execute `mvn clean compile` para baixar a biblioteca e verificar se a compilação foi bem‑sucedida.

## Etapa 2: Como definir delimitador e salvar como CSV

O objetivo principal é mudar o delimitador padrão de vírgula para um caractere personalizado (por exemplo, ponto‑e‑vírgula) ao salvar uma pasta de trabalho do Excel como CSV. Aspose.Cells fornece `CsvSaveOptions` para isso.

```java
package com.example;

import com.aspose.cells.*;

public class CsvDelimiterDemo {
    public static void main(String[] args) throws Exception {
        // Load an existing workbook (replace the path with your file)
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Configure CSV save options
        CsvSaveOptions csvOptions = new CsvSaveOptions();
        // Primary requirement: set a custom delimiter
        csvOptions.setDelimiter(';');               // <-- how to set delimiter
        // Optional: limit the number of significant digits
        csvOptions.setSignificantDigits(5);         // <-- how to limit digits

        // Save the workbook as CSV using the configured options
        workbook.save("YOUR_DIRECTORY/output.csv", csvOptions);

        System.out.println("CSV file saved with ';' delimiter and 5‑digit precision.");
    }
}
```

### Por que isso funciona

- `CsvSaveOptions.setDelimiter(char)` informa ao Aspose.Cells qual caractere separa os campos. Por padrão é a vírgula, mas qualquer caractere (tab `'\t'`, pipe `'|'`, etc.) funciona.
- `setSignificantDigits(int)` limita a precisão numérica, atendendo ao requisito **como limitar dígitos** sem formatar cada célula manualmente.

#### Saída esperada

O arquivo `output.csv` conterá linhas como:

```
Name;Amount;Date
Alice;123.46;2024-01-15
Bob;78.90;2024-01-16
```

Observe que os números são arredondados para cinco dígitos significativos (por exemplo, `123.45678` → `123.46`).

## Etapa 3: Como limitar dígitos ao salvar CSV

Se precisar de controle mais rígido sobre a formatação numérica, também pode usar uma instância de `CsvSaveOptions` para especificar uma string de formato numérico personalizada.

```java
CsvSaveOptions csvOptions = new CsvSaveOptions();
csvOptions.setDelimiter(',');                // standard comma delimiter
csvOptions.setNumberFormat("0.####");        // up to 4 decimal places
csvOptions.setSignificantDigits(6);          // overall significant digits
```

- `setNumberFormat` segue os padrões de estilo .NET, que o Aspose.Cells respeita.
- Combinar `setNumberFormat` e `setSignificantDigits` fornece arredondamento previsível em diferentes localidades.

## Etapa 4: Como exportar CSV como string com delimitador personalizado

Às vezes você não quer um arquivo físico; precisa dos dados CSV na memória (por exemplo, para enviar como resposta HTTP). A classe `ExportTableOptions` permite exportar um intervalo como string.

```java
// Export a range (rows 0‑9, columns 0‑4) as a CSV string
ExportTableOptions exportOptions = new ExportTableOptions();
exportOptions.setExportAsString(true);   // return a string instead of a file
exportOptions.setDelimiter(',');         // <-- how to set delimiter for export
exportOptions.setIncludeColumnNames(true);

String csvData = workbook.getWorksheets()
                         .get(0)                     // first worksheet
                         .getCells()
                         .exportDataTableAsString(0, 0, 10, 5, exportOptions);

System.out.println("Exported CSV string:");
System.out.println(csvData);
```

### Quando usar isso

- Retornar CSV de um endpoint REST (`@RestController` no Spring)
- Incorporar dados CSV em um anexo de e‑mail sem gravar no disco
- Realizar verificações rápidas durante testes unitários

## Etapa 5: Como recalcular fórmulas após carregar uma pasta de trabalho

Se sua pasta de trabalho contém fórmulas — especialmente **fórmulas de matriz dinâmica** introduzidas nas versões recentes do Excel — você deve recalculá‑las após carregar o arquivo. Aspose.Cells atualiza automaticamente os resultados de matrizes dinâmicas, mas ainda é necessário chamar `calculateFormula()` para fórmulas regulares.

```java
// Load a workbook that uses the Japanese Emperor calendar (optional step)
LoadOptions loadOptions = new LoadOptions();
loadOptions.setCalendar(CalendarType.JAPANESE_EMPEROR_REIGN);
Workbook japaneseWorkbook = new Workbook("YOUR_DIRECTORY/japan.xlsx", loadOptions);

// Recalculate all formulas in the workbook
japaneseWorkbook.calculateFormula();   // <-- recalculate formulas

// Save the refreshed workbook (preserves the original calendar)
japaneseWorkbook.save("YOUR_DIRECTORY/japan_updated.xlsx");
System.out.println("Formulas recalculated and workbook saved.");
```

### Por que recalcular?

- As fórmulas podem referenciar dados externos ou funções voláteis (`NOW()`, `RAND()`) que precisam de valores atualizados.
- Fórmulas de matriz dinâmica (por exemplo, `=SORT(A1:A10)`) são avaliadas automaticamente, mas chamar `calculateFormula()` garante consistência em todas as planilhas.

## Etapa 6: Exemplo completo de ponta a ponta

Abaixo está uma única classe que demonstra **como definir delimitador**, **salvar como CSV**, **limitar dígitos**, **exportar uma string CSV**, **carregar uma pasta de trabalho com calendário especial** e **recalcular fórmulas**. O código está pronto para copiar e colar no seu projeto.

```java
package com.example;

import com.aspose.cells.*;

public class AsposeCsvFullDemo {
    public static void main(String[] args) throws Exception {
        // -----------------------------------------------------------------
        // 1. Load an existing workbook
        // -----------------------------------------------------------------
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // -----------------------------------------------------------------
        // 2. Configure CSV save options (delimiter + digit limit)
        // -----------------------------------------------------------------
        CsvSaveOptions csvOptions = new CsvSaveOptions();
        csvOptions.setDelimiter(';');          // <-- how to set delimiter
        csvOptions.setSignificantDigits(5);    // <-- how to limit digits

        // -----------------------------------------------------------------
        // 3. Save the workbook as CSV
        // -----------------------------------------------------------------
        workbook.save("YOUR_DIRECTORY/output.csv", csvOptions);
        System.out.println("Saved CSV with ';' delimiter.");

        // -----------------------------------------------------------------
        // 4. Export a range as a CSV string (custom delimiter)
        // -----------------------------------------------------------------
        ExportTableOptions exportOptions = new ExportTableOptions();
        exportOptions.setExportAsString(true);
        exportOptions.setDelimiter(',');       // <-- how to set delimiter for export
        exportOptions.setIncludeColumnNames(true);

        String csvString = workbook.getWorksheets()
                                   .get(0)
                                   .getCells()
                                   .exportDataTableAsString(0, 0, 10, 5, exportOptions);
        System.out.println("CSV string exported:");
        System.out.println(csvString);

        // -----------------------------------------------------------------
        // 5. Load a workbook that uses the Japanese Emperor calendar
        // -----------------------------------------------------------------
        LoadOptions loadOptions = new LoadOptions();
        loadOptions.setCalendar(CalendarType.JAPANESE_EMPEROR_REIGN);
        Workbook japaneseWorkbook = new Workbook("YOUR_DIRECTORY/japan.xlsx", loadOptions);

        // -----------------------------------------------------------------
        // 6. Recalculate formulas (including dynamic‑array formulas)
        // -----------------------------------------------------------------
        japaneseWorkbook.calculateFormula();   // <-- recalculate formulas

        // -----------------------------------------------------------------
        // 7. Save the refreshed workbook
        // -----------------------------------------------------------------
        japaneseWorkbook.save("YOUR_DIRECTORY/japan_updated.xlsx");
        System.out.println("Japanese workbook refreshed and saved.");
    }
}
```

### Verificando o resultado

1. Abra `output.csv` em um editor de texto – você deverá ver um ponto‑e‑vírgula (`;`) separando cada coluna.
2. Confirme que as colunas numéricas exibem no máximo cinco dígitos significativos.
3. A saída no console imprimirá a string CSV gerada na Etapa 4.
4. Abra `japan_updated.xlsx` no Excel – quaisquer fórmulas que antes exibiam `#REF!` ou valores desatualizados agora mostrarão os resultados corretos.

## Armadilhas comuns e como evitá‑las

| Problema | Causa | Solução |
|----------|-------|---------|
| CSV mostra aspas extras | As células contêm vírgulas enquanto o delimitador também é vírgula | Use um delimitador diferente (`;` ou `\t`) via `setDelimiter` |
| Números são arredondados incorretamente | `setSignificantDigits` aplicado após formato numérico personalizado | Aplique `setNumberFormat` **antes** de `setSignificantDigits` |

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [Como carregar e salvar Excel como CSV usando Aspose.Cells para Java: Um guia abrangente](/cells/english/java/workbook-operations/aspose-cells-java-load-save-excel-csv/)
- [Como carregar um arquivo CSV usando Aspose.Cells para Java: Um guia abrangente](/cells/english/java/workbook-operations/load-csv-aspose-cells-java-tutorial/)
- [Como carregar arquivos CSV usando analisadores personalizados em Java com Aspose.Cells](/cells/english/java/import-export/load-csv-files-custom-parsers-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}