---
category: general
date: 2026-09-27
description: Criar uma pasta de trabalho Excel em Java, importar dados SQL, definir
  o formato numérico da coluna e salvar a pasta de trabalho como XLSX usando Aspose.Cells
  em Java.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook java
- save workbook as xlsx
- import sql data excel
- add number format excel
- set number format column
language: pt
lastmod: 2026-09-27
og_description: Criar workbook Excel em Java, importar dados SQL, definir o formato
  numérico da coluna e salvar o workbook como XLSX com um exemplo Java totalmente
  funcional.
og_image_alt: Screenshot of a Java program creating an Excel workbook with styled
  numeric columns
og_title: Criar planilha Excel em Java – importar dados SQL e definir formatos numéricos
  das colunas
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Create Excel workbook java, import SQL data, set number format column,
    and save workbook as XLSX using Aspose.Cells in Java.
  headline: Create Excel workbook java and apply column number formats
  type: TechArticle
tags:
- Java
- Aspose.Cells
- Excel automation
- Data import
title: Criar planilha Excel em Java e aplicar formatos numéricos nas colunas
url: /pt/java/formatting/create-excel-workbook-java-and-apply-column-number-formats/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar workbook Excel java e aplicar formatos numéricos nas colunas

Se você precisa **criar workbook Excel java** e estilizar colunas numéricas, este guia mostra exatamente como fazer. Você aprenderá a importar dados SQL para o Excel, definir um formato numérico para cada coluna e **salvar o workbook como XLSX** usando a biblioteca Aspose.Cells.

Trabalhar com planilhas a partir do Java costuma ser fragmentado — desenvolvedores copiam‑e‑colam trechos de código, esquecem de formatar números ou acabam com arquivos CSV em vez de arquivos Excel reais. Este tutorial elimina esse atrito ao fornecer uma solução única, de ponta a ponta, que pode ser inserida em qualquer projeto Java.

Ao final do artigo você será capaz de:

* Conectar‑se a um banco de dados e recuperar um `DataTable` (ou `ResultSet`)  
* Criar um novo workbook com Aspose.Cells  
* Aplicar um estilo consistente de **add number format excel** a todas as colunas  
* **Salvar o workbook como XLSX** em um local de sua escolha  

O único pré‑requisito é um ambiente de desenvolvimento Java (JDK 8+ recomendado) e o JAR do Aspose.Cells for Java no seu classpath.

---

## Pré‑requisitos

| Requisito | Por que é importante |
|-----------|----------------------|
| JDK 8 ou mais recente | Fornece os recursos de linguagem usados no exemplo. |
| Aspose.Cells for Java (versão mais recente) | Manipula a criação, estilização e salvamento do Excel sem precisar do Office instalado. |
| Um banco de dados compatível com JDBC (ex.: MySQL, PostgreSQL) | Fornece os dados SQL que iremos importar. |
| Maven ou Gradle (opcional) | Simplifica o gerenciamento de dependências. |

Adicione o Aspose.Cells ao seu `pom.xml` do Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- use the latest stable version -->
</dependency>
```

Ou faça o download do JAR diretamente do site da Aspose e adicione‑o ao classpath do seu projeto.

---

## Etapa 1: Criar workbook Excel java

O primeiro bloco lógico é instanciar um novo `Workbook`. Esse objeto representa todo o arquivo Excel na memória e dá acesso a planilhas, células e estilos.

```java
// Step 1: Create a new workbook instance
Workbook workbook = new Workbook();
```

Criar o workbook antecipadamente também nos fornece uma fábrica de `Style` que precisaremos mais adiante ao **set number format column**.

---

## Etapa 2: Recuperar dados do SQL (import sql data excel)

A seguir abrimos uma conexão JDBC, executamos uma simples instrução `SELECT` e carregamos o result set em um `DataTable` da Aspose. A classe `DataTable` imita o `DataTable` do .NET e funciona perfeitamente com o método `importDataTable`.

```java
// Step 2: Pull data from a database and fill a DataTable
private static DataTable getDataTableFromDb() throws SQLException {
    // Replace with your actual connection string, user, and password
    String url = "jdbc:mysql://localhost:3306/yourdb";
    String user = "your_user";
    String password = "your_password";

    try (Connection conn = DriverManager.getConnection(url, user, password);
         Statement stmt = conn.createStatement();
         ResultSet rs = stmt.executeQuery("SELECT Id, Amount, CreatedDate FROM Payments")) {

        // Aspose.Cells provides a utility to convert ResultSet → DataTable
        return CellsHelper.getDataTableFromResultSet(rs);
    }
}
```

> **Dica:** Se você já possui um `DataTable` de outra fonte (ex.: parsing de CSV), pode pular o código JDBC e retornar essa tabela diretamente.

---

## Etapa 3: Preparar um estilo reutilizável (add number format excel)

Queremos que toda coluna numérica exiba números com duas casas decimais e separador de milhar. Em vez de estilizar cada célula individualmente, criamos um objeto `Style` uma única vez por coluna e o reutilizamos durante a importação. Essa é a forma mais eficiente de **add number format excel**.

```java
// Step 3: Build a style array – one style per column
private static Style[] buildColumnStyles(Workbook workbook, int columnCount) {
    Style[] styles = new Style[columnCount];
    for (int i = 0; i < columnCount; i++) {
        styles[i] = workbook.createStyle();
        // "0.00" = two decimal places; "#,##0.00" adds thousands separator
        styles[i].setNumber("#,##0.00");
    }
    return styles;
}
```

Você pode adaptar a string de formato (`"#,##0.00"`) para qualquer formato numérico do Excel que precisar. Para datas, use `styles[i].setCustom("mm-dd-yyyy")`, etc.

---

## Etapa 4: Importar o DataTable e aplicar os estilos de coluna

Agora juntamos tudo. A sobrecarga `importDataTable` permite passar o `DataTable`, especificar se a primeira linha deve ser tratada como cabeçalhos de coluna e fornecer o array de estilos. Isso define automaticamente **set number format column** para cada célula na coluna correspondente.

```java
// Step 4: Import data with styles into the first worksheet
private static void importDataWithStyles(Workbook workbook, DataTable dataTable) {
    // Build a style for each column based on the number of columns in the DataTable
    Style[] columnStyles = buildColumnStyles(workbook, dataTable.getColumns().size());

    // Import the DataTable starting at cell A1 (row 0, column 0)
    workbook.getWorksheets().get(0).getCells()
            .importDataTable(dataTable, true, 0, 0, columnStyles);
}
```

Como passamos `true` para o parâmetro `importColumnNames`, a primeira linha da planilha contém os nomes das colunas do `DataTable`. Cada linha subsequente recebe os dados, já formatados de acordo com o estilo que definimos.

---

## Etapa 5: Salvar workbook como xlsx

A etapa final é persistir o workbook em memória em um arquivo físico. O Aspose.Cells suporta vários formatos; usaremos o formato moderno XLSX, que é o esperado pela maioria das aplicações hoje.

```java
// Step 5: Save the workbook to an .xlsx file
private static void saveWorkbook(Workbook workbook, String filePath) throws IOException {
    workbook.save(filePath, com.aspose.cells.SaveFormat.XLSX);
}
```

Você pode alterar `filePath` para qualquer local válido no seu sistema. O método lança `IOException` se o diretório não existir ou se você não tiver permissão de escrita.

---

## Exemplo completo, executável

Juntando todas as peças, obtemos um programa autocontido que pode ser compilado e executado imediatamente.

```java
import com.aspose.cells.*;
import java.sql.*;

public class CreateExcelWorkbookJava {
    public static void main(String[] args) {
        try {
            // 1️⃣ Obtain data from the database
            DataTable dataTable = getDataTableFromDb();

            // 2️⃣ Create a new workbook that will hold the imported data
            Workbook workbook = new Workbook();

            // 3️⃣ Import the DataTable with a numeric style per column
            importDataWithStyles(workbook, dataTable);

            // 4️⃣ Save the workbook as XLSX
            String outputPath = "DataTableWithNumberFormat.xlsx";
            saveWorkbook(workbook, outputPath);

            System.out.println("Workbook created successfully at: " + outputPath);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    // ---- Helper methods (see earlier sections) ----
    private static DataTable getDataTableFromDb() throws SQLException {
        String url = "jdbc:mysql://localhost:3306/yourdb";
        String user = "your_user";
        String password = "your_password";

        try (Connection conn = DriverManager.getConnection(url, user, password);
             Statement stmt = conn.createStatement();
             ResultSet rs = stmt.executeQuery("SELECT Id, Amount, CreatedDate FROM Payments")) {

            return CellsHelper.getDataTableFromResultSet(rs);
        }
    }

    private static Style[] buildColumnStyles(Workbook workbook, int columnCount) {
        Style[] styles = new Style[columnCount];
        for (int i = 0; i < columnCount; i++) {
            styles[i] = workbook.createStyle();
            styles[i].setNumber("#,##0.00"); // two decimals with thousands separator
        }
        return styles;
    }

    private static void importDataWithStyles(Workbook workbook, DataTable dataTable) {
        Style[] columnStyles = buildColumnStyles(workbook, dataTable.getColumns().size());
        workbook.getWorksheets().get(0).getCells()
                .importDataTable(dataTable, true, 0, 0, columnStyles);
    }

    private static void saveWorkbook(Workbook workbook, String filePath) throws IOException {
        workbook.save(filePath, SaveFormat.XLSX);
    }
}
```

### Resultado esperado

Ao executar o programa, um arquivo chamado **DataTableWithNumberFormat.xlsx** será criado no diretório de trabalho. Abra‑o com Microsoft Excel, LibreOffice Calc ou qualquer visualizador compatível com XLSX e você verá:

| Id | Amount | CreatedDate |
|----|--------|-------------|
| 1  | 1,234.56 | 2023‑01‑15 |
| 2  | 78,900.00 | 2023‑02‑20 |
| …  | … | … |

*A coluna **Amount** exibe números com duas casas decimais e separador de milhar, graças ao estilo **add number format excel** que aplicamos.*

---

## Perguntas comuns e tratamento de casos limites

| Pergunta | Resposta |
|----------|----------|
| **E se minha consulta não retornar linhas?** | O `DataTable` ficará vazio, mas ainda conterá as definições de coluna. O workbook terá apenas a linha de cabeçalho, o que costuma ser suficiente para processos subsequentes. |
| **Como aplicar formatos diferentes por coluna?** | Modifique `buildColumnStyles` para inspecionar o nome da coluna ou o tipo de dado e atribuir um formato personalizado (ex.: datas, percentuais). |
| **Posso escrever diretamente em um `ByteArrayOutputStream`?** | Sim. Substitua `workbook.save(filePath, SaveFormat.XLSX);` por


## O que você deve aprender a seguir?


Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [How to Create and Save an Excel Workbook as SVG using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [Create Save Excel Workbook Aspose Cells Java](/cells/hindi/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)
- [Create Save Excel Workbook Aspose Cells Java](/cells/german/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}