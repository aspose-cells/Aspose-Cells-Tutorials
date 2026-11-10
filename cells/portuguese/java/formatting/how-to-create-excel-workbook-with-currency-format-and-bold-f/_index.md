---
category: general
date: 2026-08-20
description: Criar uma pasta de trabalho Excel em Java usando Aspose.Cells, definir
  o formato de moeda, adicionar fonte em negrito e importar a matriz de estilos para
  células estilizadas.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- set currency format
- format cells currency
- how to import style
- add bold font
language: pt
lastmod: 2026-08-20
og_description: Criar uma pasta de trabalho Excel em Java, definir o formato de moeda,
  adicionar fonte em negrito e aprender como importar estilo usando Aspose.Cells.
og_image_alt: Screenshot of an excel workbook created with currency format and bold
  font using Aspose.Cells
og_title: Criar pasta de trabalho Excel com células de moeda estilizadas em Java
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Create excel workbook in Java using Aspose.Cells, set currency format,
    add bold font, and import style array for styled cells.
  headline: How to create excel workbook with currency format and bold font in Java
  type: TechArticle
- description: Create excel workbook in Java using Aspose.Cells, set currency format,
    add bold font, and import style array for styled cells.
  name: How to create excel workbook with currency format and bold font in Java
  steps:
  - name: Initialise the workbook and worksheet
    text: Creating a fresh workbook gives you a clean container for all subsequent
      formatting.
  - name: Build a DataTable with numeric data
    text: A `DataTable` mimics a database table, making it easy to import rows in
      bulk.
  - name: Define a style – currency format and bold font
    text: Here we **set currency format** and **add bold font** to a `Style` object.
  - name: Configure import options to use the style array
    text: Aspose.Cells lets you pass a `Style[]` via `ImportTableOptions`. This is
      the official **how to import style** method.
  - name: Import the DataTable into the worksheet
    text: Now we bring the data into the sheet at cell `A1`, applying the style array
      automatically.
  - name: Save the workbook to disk
    text: Finally, write the in‑memory workbook to a physical file.
  - name: Expected output
    text: 'When you open `DataTableWithStyleArray.xlsx` in Microsoft Excel, you should
      see:'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- Formatting
title: Como criar uma pasta de trabalho do Excel com formato de moeda e fonte em negrito
  em Java
url: /pt/java/formatting/how-to-create-excel-workbook-with-currency-format-and-bold-f/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como criar uma pasta de trabalho Excel com formato de moeda e fonte em negrito em Java

Se você precisa **criar uma pasta de trabalho Excel** programaticamente, este guia mostra exatamente como fazer. Vamos percorrer a criação de uma pasta de trabalho, a aplicação de um formato de moeda, a adição de fonte em negrito e o uso do recurso **como importar estilo** do Aspose.Cells para que cada célula importada tenha aparência consistente.

Ao final, você terá um arquivo `DataTableWithStyleArray.xlsx` pronto‑para‑uso que exibe números como dólares e os destaca em negrito. Nenhuma formatação manual no Excel será necessária.

## Pré‑requisitos

Antes de começar, certifique‑se de que você tem:

- Java 17 ou superior instalado.
- Uma licença do Aspose.Cells for Java (ou uma chave de avaliação gratuita).
- Maven ou Gradle para gerenciar a dependência `aspose-cells`.
- Familiaridade básica com coleções Java e `DataTable`.

```xml
<!-- Maven dependency -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version>
</dependency>
```

> **Dica profissional:** Se você encontrar uma `LicenseException`, coloque seu arquivo de licença no classpath e chame `License license = new License(); license.setLicense("Aspose.Total.Java.lic");` antes de criar a pasta de trabalho.

## Como criar uma pasta de trabalho Excel com células de moeda estilizadas

Esta seção contém os passos principais. Cada passo explica **por que** ele é importante, não apenas **o que** digitar.

### Passo 1: Inicializar a pasta de trabalho e a planilha

Criar uma nova pasta de trabalho fornece um contêiner limpo para toda a formatação subsequente.

```java
// Step 1: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();                     // creates an empty .xlsx file in memory
Worksheet worksheet = workbook.getWorksheets().get(0); // first sheet is index 0
Cells cells = worksheet.getCells();                     // shortcut to work with cells
```

> **Por que:** O objeto `Workbook` representa o arquivo Excel completo. Acessar a primeira `Worksheet` permite que você comece a preencher dados imediatamente.

### Passo 2: Construir um DataTable com dados numéricos

Um `DataTable` imita uma tabela de banco de dados, facilitando a importação de linhas em massa.

```java
// Step 2: Build a DataTable with sample numeric data
DataTable dataTable = new DataTable();
dataTable.getColumns().add("Amount", DataType.DOUBLE); // column type DOUBLE ensures numeric handling
dataTable.getRows().add(new Object[]{1234.56});
dataTable.getRows().add(new Object[]{7890.12});
```

> **Por que:** Usar `DOUBLE` garante que os valores mantenham sua precisão decimal, o que é essencial quando você posteriormente **formatar células como moeda**.

### Passo 3: Definir um estilo – formato de moeda e fonte em negrito

Aqui nós **definimos o formato de moeda** e **adicionamos fonte em negrito** a um objeto `Style`.

```java
// Step 3: Define a style (currency format and bold font) for the imported cells
Style currencyStyle = workbook.createStyle();                // create a reusable style instance
currencyStyle.getNumber().setFormat("$#,##0.00");            // set currency format (e.g., $1,234.56)
currencyStyle.getFont().setBold(true);                      // make the font bold
Style[] styleArray = new Style[] { currencyStyle };          // style array required by ImportTableOptions
```

> **Por que:** A string de formato `Number` `$#,##0.00` indica ao Excel que a célula deve ser tratada como valor monetário, enquanto `setBold(true)` chama a atenção para os números. Colocar o estilo em um array prepara o próximo passo **como importar estilo**.

### Passo 4: Configurar opções de importação para usar o array de estilos

O Aspose.Cells permite passar um `Style[]` via `ImportTableOptions`. Este é o método oficial **como importar estilo**.

```java
// Step 4: Set up import options to use the style array
ImportTableOptions importOptions = new ImportTableOptions();
importOptions.setStyleArray(styleArray); // tells the importer to apply our currencyStyle to every column
```

> **Por que:** Sem `ImportTableOptions`, as células importadas herdariam o estilo padrão, perdendo a formatação de moeda e o negrito que definimos.

### Passo 5: Importar o DataTable para a planilha

Agora trazemos os dados para a planilha na célula `A1`, aplicando o array de estilos automaticamente.

```java
// Step 5: Import the DataTable into the worksheet at A1, applying the style
cells.importDataTable(dataTable, true, "A1", importOptions);
```

- `true` indica que a primeira linha do `DataTable` contém cabeçalhos de coluna.
- `"A1"` é o canto superior‑esquerdo onde a importação começa.

> **Por que:** Importar com o array de estilos garante que cada célula importada receba o estilo **formatar células como moeda** que preparamos anteriormente.

### Passo 6: Salvar a pasta de trabalho no disco

Por fim, gravamos a pasta de trabalho em memória em um arquivo físico.

```java
// Step 6: Save the workbook to a file
String outputPath = "YOUR_DIRECTORY/DataTableWithStyleArray.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to: " + outputPath);
```

> **Por que:** Salvar persiste a formatação, permitindo que você ou processos subsequentes abram o arquivo no Excel com a aparência desejada.

## Código‑fonte completo

Abaixo está a classe Java completa, pronta‑para‑executar. Copie-a para sua IDE, substitua `YOUR_DIRECTORY` por uma pasta existente e execute.

```java
import com.aspose.cells.*;

public class StyleArrayImportTutorial {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);
        Cells cells = worksheet.getCells();

        // Step 2: Build a DataTable with sample numeric data
        DataTable dataTable = new DataTable();
        dataTable.getColumns().add("Amount", DataType.DOUBLE);
        dataTable.getRows().add(new Object[]{1234.56});
        dataTable.getRows().add(new Object[]{7890.12});

        // Step 3: Define a style (currency format and bold font) for the imported cells
        Style currencyStyle = workbook.createStyle();
        currencyStyle.getNumber().setFormat("$#,##0.00");   // set currency format
        currencyStyle.getFont().setBold(true);             // add bold font
        Style[] styleArray = new Style[] { currencyStyle };

        // Step 4: Set up import options to use the style array
        ImportTableOptions importOptions = new ImportTableOptions();
        importOptions.setStyleArray(styleArray);           // how to import style

        // Step 5: Import the DataTable into the worksheet at A1, applying the style
        cells.importDataTable(dataTable, true, "A1", importOptions);

        // Step 6: Save the workbook to a file
        workbook.save("YOUR_DIRECTORY/DataTableWithStyleArray.xlsx");
        System.out.println("Workbook created successfully.");
    }
}
```

### Saída esperada

Ao abrir `DataTableWithStyleArray.xlsx` no Microsoft Excel, você deverá ver:

| Amount |
|--------|
| **$1,234.56** |
| **$7,890.12** |

- Os números são exibidos com um **formato de moeda** (símbolo `$`, duas casas decimais).
- A fonte de ambas as células está **em negrito**, destacando‑as.

## Variações comuns e casos de borda

| Cenário | O que mudar | Motivo |
|----------|----------------|--------|
| **Moeda diferente** | `currencyStyle.getNumber().setFormat("€#,##0.00");` | Use o símbolo do Euro ou qualquer formato específico de localidade. |
| **Múltiplas colunas com estilos diferentes** | Crie vários objetos `Style`, preencha `styleArray` na mesma ordem das colunas. | Cada coluna pode ter seu próprio formato numérico, fonte, plano de fundo, etc. |
| **Conjuntos de dados grandes** | Use `cells.importDataTable(dataTable, false, "A1", importOptions);` e defina `importOptions.setImportDataOptions(ImportDataOptions.DATA_ONLY);` | Melhora o desempenho ao pular linhas de cabeçalho ou metadados desnecessários. |
| **Aplicar estilo após a importação** | Chame `cells.get("A2").setStyle(currencyStyle);` para células individuais. | Útil quando apenas um subconjunto de linhas precisa de formatação especial. |

## Dicas para uso em produção

- **Licenciar cedo**: Registre sua licença Aspose.Cells antes de criar a pasta de trabalho para evitar a marca d'água de avaliação.
- **Segurança de threads**: Instâncias de `Workbook` **não** são seguras para uso simultâneo. Crie uma instância separada por thread se gerar muitos arquivos concorrentes.
- **Gerenciamento de memória**: Para planilhas muito grandes, considere usar a API de streaming do `Workbook` (`Workbook` → `WorkbookDesigner`) para manter o uso de memória baixo.
- **Testes**: Inclua um teste unitário que abra o arquivo salvo com Apache POI e verifique se o número de formato do estilo da célula corresponde a `"$#,##0.00"`.

## Conclusão

Agora você sabe como **criar uma pasta de trabalho Excel** em Java, **definir formato de moeda**, **adicionar fonte em negrito** e usar corretamente **como importar estilo** com `ImportTableOptions` do Aspose.Cells. Esta solução de ponta a ponta elimina etapas manuais no Excel e garante que cada célula importada siga o mesmo estilo **formatar células como moeda**.

Pronto para o próximo desafio? Experimente adicionar formatação condicional, incorporar gráficos ou exportar a pasta de trabalho para PDF — tudo reutilizando a mesma técnica de array de estilos. Boa codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Criar uma pasta de trabalho Excel usando Aspose.Cells em Java: Um Guia Passo a Passo](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [Como criar e formatar células Excel usando Aspose.Cells para Java: Um Guia Passo a Passo](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)
- [Como estilizar células Excel e adicionar hyperlinks usando Aspose.Cells para Java](/cells/english/java/formatting/style-excel-cells-hyperlinks-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}