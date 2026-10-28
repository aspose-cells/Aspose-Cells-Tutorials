---
category: general
date: 2026-10-07
description: Aprenda a duplicar tabelas dinâmicas no Excel usando Java e Aspose.Cells.
  Copie uma tabela dinâmica copiando seu intervalo entre pastas de trabalho rapidamente.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to duplicate pivot
- copy pivot table
- copy excel range
- copy range between workbooks
- how to copy pivot table
language: pt
lastmod: 2026-10-07
og_description: Como duplicar tabelas dinâmicas no Excel usando Java e Aspose.Cells.
  Siga este guia para copiar uma tabela dinâmica copiando seu intervalo entre pastas
  de trabalho.
og_image_alt: Illustration of copying an Excel pivot table from one workbook to another
og_title: Como duplicar tabelas dinâmicas no Excel com Java – tutorial completo
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to duplicate pivot tables in Excel using Java and Aspose.Cells.
    Copy a pivot table by copying its range between workbooks quickly.
  headline: How to duplicate pivot tables in Excel with Java – step‑by‑step guide
  type: TechArticle
- description: Learn how to duplicate pivot tables in Excel using Java and Aspose.Cells.
    Copy a pivot table by copying its range between workbooks quickly.
  name: How to duplicate pivot tables in Excel with Java – step‑by‑step guide
  steps:
  - name: Explanation of each step
    text: '| Step | What the code does | Why it matters for **copy pivot table** |
      |------|-------------------|----------------------------------------| | **1️⃣
      Load source workbook** | `new Workbook(srcPath)` reads `Source.xlsx`. | The
      source file is the only place where the original pivot exists. | | **2️⃣ D'
  - name: 1️⃣ Copying a pivot that spans multiple sheets
    text: 'If the pivot’s source data lives on a different sheet than the pivot itself,
      include both sheets in the copy operation. The simplest approach is to copy
      the entire source sheet first, then copy the pivot sheet:'
  - name: 2️⃣ Dealing with named ranges
    text: 'Aspose.Cells preserves named ranges when you copy a range. However, if
      the destination workbook already contains a name with the same identifier, a
      `CellsException` is thrown. Resolve this by renaming the conflicting name before
      the copy:'
  - name: 3️⃣ Large workbooks and performance
    text: 'Copying very large ranges (hundreds of thousands of rows) can be memory‑intensive.
      Enable **memory optimization**:'
  - name: 4️⃣ Keeping formulas intact
    text: If the source range contains formulas that reference cells outside the copied
      area, those references become broken after the copy. To avoid this, expand the
      range to include all dependent cells, or use `copyRange` with the `CopyOptions`
      flag `CopyOptions.COPY_FORMULA`.
  type: HowTo
tags:
- Excel
- Java
- Aspose.Cells
- PivotTable
- Data manipulation
title: Como duplicar tabelas dinâmicas no Excel com Java – guia passo a passo
url: /pt/java/excel-pivot-tables/how-to-duplicate-pivot-tables-in-excel-with-java-step-by-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como duplicar tabelas dinâmicas no Excel com Java – guia passo a passo

Se você precisa **como duplicar tabelas dinâmicas** em uma pasta de trabalho do Excel, este tutorial mostra uma solução completa e pronta‑para‑executar. Usando Aspose.Cells for Java você pode copiar uma tabela dinâmica junto com seus dados de origem copiando o intervalo subjacente e, em seguida, salvando o resultado como uma nova pasta de trabalho.

Duplicar uma tabela dinâmica costuma ser complicado porque o cache da tabela dinâmica está oculto dentro da planilha. Ao copiar todo o intervalo que contém a tabela dinâmica, o Aspose.Cells recria automaticamente o cache na pasta de trabalho de destino, proporcionando uma cópia totalmente funcional sem necessidade de manipular XML manualmente.

Neste guia você irá:

* Carregar uma pasta de trabalho fonte que contém uma tabela dinâmica.  
* Definir o intervalo exato que contém a tabela dinâmica.  
* Copiar esse intervalo para uma nova pasta de trabalho, preservando a definição da tabela dinâmica.  
* Salvar o novo arquivo e verificar se a tabela dinâmica funciona.  

As etapas funcionam com qualquer versão do Excel suportada pelo Aspose.Cells (2007‑2024) e requerem apenas algumas linhas de código Java.

## Pré-requisitos

| Requisito | Por que é importante |
|-------------|----------------|
| **Java 8 ou superior** | Aspose.Cells foi desenvolvido para Java 8+. |
| **Aspose.Cells for Java** (versão mais recente) | Fornece as APIs `Workbook`, `Range` e `CopyRange` usadas no exemplo. |
| **Pasta de trabalho fonte** com uma tabela dinâmica (ex.: `Source.xlsx`) | A tabela dinâmica que você deseja duplicar. |
| **Permissão de gravação** no diretório de destino | Necessária para salvar `CopyWithPivot.xlsx`. |

Adicione a dependência do Aspose.Cells Maven ao seu `pom.xml` (ou faça o download do JAR manualmente):

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>   <!-- use the latest stable version -->
</dependency>
```

## Como duplicar tabelas dinâmicas – implementação completa

A seguir está um programa Java autônomo que demonstra **como duplicar tabelas dinâmicas** copiando o intervalo que contém a tabela dinâmica. O código inclui tratamento de erros, comentários e uma etapa de verificação.

```java
// File: DuplicatePivot.java
import com.aspose.cells.*;

public class DuplicatePivot {
    public static void main(String[] args) {
        // 1️⃣ Load the source workbook that holds the pivot table.
        String srcPath = "YOUR_DIRECTORY/Source.xlsx";
        Workbook srcWb;
        try {
            srcWb = new Workbook(srcPath);
        } catch (Exception e) {
            System.err.println("Failed to load source workbook: " + e.getMessage());
            return;
        }

        // 2️⃣ Identify the range that encloses the pivot table.
        // Adjust the sheet index (0‑based) and address as needed.
        Worksheet srcSheet = srcWb.getWorksheets().get(0);
        // Example address "A1:G20" – includes the pivot and its data source.
        String pivotRangeAddress = "A1:G20";
        Range srcRange = srcSheet.getCells().createRange(pivotRangeAddress);

        // 3️⃣ Create a destination workbook and copy the identified range.
        Workbook destWb = new Workbook(); // starts with a blank workbook
        Worksheet destSheet = destWb.getWorksheets().get(0);
        try {
            // copyRange copies both values and the internal pivot cache.
            destSheet.getCells().copyRange(srcRange, "A1");
        } catch (Exception e) {
            System.err.println("Failed to copy range: " + e.getMessage());
            return;
        }

        // 4️⃣ (Optional) Refresh the pivot so it reflects the copied data.
        // Aspose.Cells automatically rebuilds the cache, but calling refresh
        // guarantees up‑to‑date results if the source data has changed.
        for (int i = 0; i < destSheet.getPivotTables().getCount(); i++) {
            destSheet.getPivotTables().get(i).refresh();
        }

        // 5️⃣ Save the new workbook that now contains the duplicated pivot.
        String destPath = "YOUR_DIRECTORY/CopyWithPivot.xlsx";
        try {
            destWb.save(destPath);
            System.out.println("Pivot table duplicated successfully to: " + destPath);
        } catch (Exception e) {
            System.err.println("Failed to save destination workbook: " + e.getMessage());
        }
    }
}
```

### Explicação de cada etapa

| Etapa | O que o código faz | Por que é importante para **copiar tabela dinâmica** |
|------|-------------------|----------------------------------------|
| **1️⃣ Carregar pasta de trabalho fonte** | `new Workbook(srcPath)` lê `Source.xlsx`. | O arquivo fonte é o único local onde a tabela dinâmica original existe. |
| **2️⃣ Definir o intervalo** | `createRange("A1:G20")` cria um objeto `Range` que cobre a tabela dinâmica e seus dados. | Uma tabela dinâmica é armazenada junto com seu cache; copiar todo o intervalo garante que o cache seja movido também. |
| **3️⃣ Copiar o intervalo** | `copyRange(srcRange, "A1")` grava o intervalo na planilha de destino. | Este é o núcleo de **copiar intervalo entre pastas de trabalho** – a API lida automaticamente com objetos ocultos. |
| **4️⃣ Atualizar tabela dinâmica** | `pivotTable.refresh()` força a tabela dinâmica a recalcular. | Garante que a tabela dinâmica duplicada mostre os mesmos valores da original, especialmente após modificações. |
| **5️⃣ Salvar pasta de trabalho** | `destWb.save(destPath)` grava o arquivo no disco. | Produz o resultado final de **copiar intervalo do Excel** que você pode abrir no Excel. |

#### Saída esperada

Após executar o programa, abra `CopyWithPivot.xlsx`. Você verá uma planilha que parece idêntica à planilha fonte, e a tabela dinâmica funciona exatamente como a original – você pode expandir linhas, filtrar campos e atualizar os dados sem erros.

## Variações comuns e casos extremos

### 1️⃣ Copiando uma tabela dinâmica que abrange várias planilhas

Se os dados de origem da tabela dinâmica estiverem em uma planilha diferente da própria tabela dinâmica, inclua ambas as planilhas na operação de cópia. A abordagem mais simples é copiar primeiro a planilha fonte inteira e, em seguida, copiar a planilha da tabela dinâmica:

```java
// Copy source data sheet
Workbook temp = new Workbook(); // temporary workbook for the data sheet
temp.getWorksheets().addCopy(srcWb.getWorksheets().get(0));
Workbook dest = new Workbook();
dest.getWorksheets().addCopy(temp.getWorksheets().get(0));

// Then copy the pivot sheet as shown earlier
```

### 2️⃣ Lidando com intervalos nomeados

O Aspose.Cells preserva intervalos nomeados ao copiar um intervalo. Contudo, se a pasta de trabalho de destino já contiver um nome com o mesmo identificador, uma `CellsException` é lançada. Resolva isso renomeando o nome conflitante antes da cópia:

```java
if (destWb.getWorksheets().get(0).getNames().containsKey("MyRange")) {
    destWb.getWorksheets().get(0).getNames().remove("MyRange");
}
```

### 3️⃣ Pastas de trabalho grandes e desempenho

Copiar intervalos muito grandes (centenas de milhares de linhas) pode consumir muita memória. Ative a **otimização de memória**:

```java
LoadOptions loadOptions = new LoadOptions(LoadFormat.XLSX);
loadOptions.setMemorySetting(MemorySetting.MEMORY_PREFERENCE);
Workbook largeSrc = new Workbook(srcPath, loadOptions);
```

### 4️⃣ Mantendo fórmulas intactas

Se o intervalo fonte contém fórmulas que referenciam células fora da área copiada, essas referências ficam quebradas após a cópia. Para evitar isso, expanda o intervalo para incluir todas as células dependentes ou use `copyRange` com a flag `CopyOptions` `CopyOptions.COPY_FORMULA`.

```java
CopyOptions options = new CopyOptions();
options.setCopyFormula(true);
destSheet.getCells().copyRange(srcRange, "A1", options);
```

## Dicas profissionais para um **copiar intervalo entre pastas de trabalho** confiável

* **Sempre use endereços absolutos** (`$A$1:$G$20`) quando a planilha fonte pode ser renomeada.  
* **Atualize após a cópia** – embora o Aspose.Cells reconstrua o cache, chamar `refresh()` elimina avisos ocasionais de cache obsoleto no Excel.  
* **Valide a tabela dinâmica**: após salvar, abra o arquivo programaticamente e chame `pivotTable.validate()` para garantir que não haja referências quebradas.  
* **Compatibilidade de versão**: o código funciona com arquivos Excel 2007‑2024 (`.xlsx`, `.xlsm`). Para arquivos legados `.xls`, defina `LoadOptions.setLoadFormat(LoadFormat.XLS)`.

## Listagem completa do código fonte (pronta para compilar)

```java
import com.aspose.cells.*;

public class DuplicatePivot {
    public static void main(String[] args) {
        // --------------------------------------------------------------------
        // 1️⃣ Carregar pasta de trabalho fonte
        // --------------------------------------------------------------------
        String srcPath = "YOUR_DIRECTORY/Source.xlsx";
        Workbook srcWb;
        try {
            srcWb = new Workbook(srcPath);
        } catch (Exception e) {
            System.err.println("Failed to load source workbook: " + e.getMessage());
            return;
        }

        // --------------------------------------------------------------------
        // 2️⃣ Definir o intervalo que contém a tabela dinâmica
        // --------------------------------------------------------------------
        Worksheet srcSheet = srcWb.getWorksheets().get(0);
        String pivotRangeAddress = "A1:G20"; // adjust to your pivot's actual area
        Range srcRange = srcSheet.getCells().createRange(pivotRangeAddress);

        // --------------------------------------------------------------------
        // 3️⃣ Copiar o intervalo (incluindo a tabela dinâmica) para uma nova pasta de trabalho
        // --------------------------------------------------------------------
        Workbook destWb = new Workbook(); // blank workbook
        Worksheet destSheet = destWb.getWorksheets().get(0);
        try {
            destSheet.getCells().copyRange(srcRange, "A1");
        } catch (Exception e) {
            System.err.println("Failed to copy range: " + e.getMessage());
            return;
        }

        // --------------------------------------------------------------------
        // 4️⃣ Atualizar a tabela dinâmica duplicada (garante valores corretos)
        // --------------------------------------------------------------------
        for (int i = 0; i < destSheet.getPivotTables().getCount(); i++) {
            destSheet


## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Como copiar tabela dinâmica em Java – Guia completo do Aspose.Cells](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-complete-aspose-cells-guide/)
- [Como criar tabelas dinâmicas no Excel usando Aspose.Cells para Java: Um guia abrangente](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Como atualizar a fonte da tabela dinâmica do Excel com Aspose.Cells para Java: Um guia abrangente](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}