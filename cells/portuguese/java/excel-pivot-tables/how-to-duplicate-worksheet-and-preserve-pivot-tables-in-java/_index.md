---
category: general
date: 2026-08-17
description: Como duplicar uma planilha em Java usando Aspose.Cells, preservando a
  tabela dinâmica, copiando a tabela dinâmica para uma nova pasta de trabalho e criando
  uma pasta de trabalho a partir de uma planilha.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to duplicate worksheet
- how to copy pivot
- how to preserve pivot
- copy pivot to workbook
- create workbook from sheet
language: pt
lastmod: 2026-08-17
og_description: Como duplicar uma planilha em Java usando Aspose.Cells, preservando
  a tabela dinâmica, copiando a tabela dinâmica para uma nova pasta de trabalho e
  criando uma pasta de trabalho a partir de uma planilha — todos os passos explicados.
og_image_alt: Screenshot of Java code duplicating an Excel worksheet with a pivot
  table using Aspose.Cells
og_title: Como duplicar planilha e manter tabelas dinâmicas – Guia Java
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: How to duplicate worksheet in Java using Aspose.Cells, preserving the
    pivot table, copying pivot to a new workbook, and creating a workbook from a sheet.
  headline: How to duplicate worksheet and preserve pivot tables in Java
  type: TechArticle
- description: How to duplicate worksheet in Java using Aspose.Cells, preserving the
    pivot table, copying pivot to a new workbook, and creating a workbook from a sheet.
  name: How to duplicate worksheet and preserve pivot tables in Java
  steps:
  - name: – Load the workbook that contains the pivot table
    text: '```java import com.aspose.cells.*;'
  - name: – Create a new workbook and duplicate the entire worksheet
    text: '```java // Create an empty destination workbook Workbook destinationWorkbook
      = new Workbook();'
  - name: – Save the new workbook
    text: '```java // Save the duplicated workbook; the pivot remains functional destinationWorkbook.save("YOUR_DIRECTORY/copy_with_pivot.xlsx");
      } } ```'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- Pivot Table
- Workbook
title: Como duplicar a planilha e preservar as tabelas dinâmicas em Java
url: /pt/java/excel-pivot-tables/how-to-duplicate-worksheet-and-preserve-pivot-tables-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como duplicar planilha e preservar tabelas dinâmicas em Java

Como duplicar uma planilha mantendo sua tabela dinâmica intacta é uma necessidade frequente ao automatizar relatórios em Excel. Este guia mostra como copiar a tabela dinâmica para uma nova pasta de trabalho usando Aspose.Cells para Java e também aborda como preservar a tabela dinâmica ao criar uma pasta de trabalho a partir de uma planilha.

Você aprenderá como carregar uma pasta de trabalho existente, duplicar a planilha que contém a tabela dinâmica e salvar o resultado como um novo arquivo. O tutorial pressupõe que você tem um ambiente básico de desenvolvimento Java e uma licença válida do Aspose.Cells (a avaliação gratuita funciona para testes). Nenhuma ferramenta externa é necessária além do JAR do Aspose.Cells.

## Pré-requisitos

Antes de começar, certifique-se de ter:

* Java Development Kit (JDK) 8 ou superior.
* Maven ou Gradle para gerenciar a dependência do Aspose.Cells.
* Um arquivo Excel (`source.xlsx`) que contenha ao menos uma tabela dinâmica na primeira planilha.
* Um diretório onde você possa ler o arquivo de origem e gravar a pasta de trabalho duplicada.

Adicione a dependência do Aspose.Cells ao seu `pom.xml` (Maven) ou `build.gradle` (Gradle). Para Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- use the latest version -->
</dependency>
```

## Como duplicar planilha com uma tabela dinâmica

A operação principal é um processo de três etapas: carregar, copiar e salvar. Cada etapa é explicada abaixo.

### Etapa 1 – Carregar a pasta de trabalho que contém a tabela dinâmica

```java
import com.aspose.cells.*;

public class CopyPivotTable {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that holds the pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet sourceWorksheet = sourceWorkbook.getWorksheets().get(0);
```

*Por que esta etapa importa*: O objeto `Workbook` representa todo o arquivo Excel. Ao recuperar a primeira planilha (`get(0)`), você direciona a planilha que contém a tabela dinâmica que pretende duplicar.

### Etapa 2 – Criar uma nova pasta de trabalho e duplicar a planilha inteira

```java
        // Create an empty destination workbook
        Workbook destinationWorkbook = new Workbook();

        // Duplicate the source worksheet, preserving its pivot table
        destinationWorkbook.getWorksheets().addCopy(sourceWorksheet);
```

`addCopy` clona a planilha **incluindo** todos os objetos incorporados, fórmulas e caches de tabelas dinâmicas. Esta é a maneira recomendada de **como copiar tabela dinâmica** porque a definição da tabela dinâmica e sua fonte de dados são transferidas juntas.

### Etapa 3 – Salvar a nova pasta de trabalho

```java
        // Save the duplicated workbook; the pivot remains functional
        destinationWorkbook.save("YOUR_DIRECTORY/copy_with_pivot.xlsx");
    }
}
```

Após a execução, `copy_with_pivot.xlsx` contém uma cópia exata da planilha original, e a tabela dinâmica funciona sem configuração adicional.

**Resultado esperado**: Abrir `copy_with_pivot.xlsx` no Excel mostra a planilha duplicada com o mesmo layout de tabela dinâmica, filtros e campos calculados do arquivo de origem.

## Como copiar tabela dinâmica para outra pasta de trabalho

Se precisar mover uma tabela dinâmica sem copiar a planilha inteira, você pode extrair o cache da tabela dinâmica e anexá‑lo a uma nova planilha. O trecho a seguir demonstra essa abordagem:

```java
// Assume sourceWorkbook and sourceWorksheet are already loaded
PivotTable pivot = sourceWorksheet.getPivotTables().get(0);

// Create a new workbook and a blank worksheet
Workbook targetWorkbook = new Workbook();
Worksheet targetSheet = targetWorkbook.getWorksheets().add("PivotCopy");

// Import the pivot table definition
targetSheet.getPivotTables().addCopy(pivot);
targetWorkbook.save("YOUR_DIRECTORY/pivot_only_copy.xlsx");
```

Este código responde **como copiar tabela dinâmica** copiando apenas o objeto da tabela dinâmica, não a planilha inteira. O método `addCopy` na coleção `PivotTables` garante que o cache da tabela dinâmica seja duplicado, atendendo aos requisitos de **como preservar tabela dinâmica**.

## Como preservar tabela dinâmica ao criar pasta de trabalho a partir de uma planilha

Às vezes você começa com uma planilha que não pertence a uma pasta de trabalho (por exemplo, gera uma planilha na memória). Para **criar pasta de trabalho a partir de planilha** mantendo a tabela dinâmica, siga estas etapas:

```java
// Create a worksheet in memory
Worksheet tempSheet = new Worksheet();
PivotTable pivot = tempSheet.getPivotTables().add("A1", "B10", "MyPivot");

// Configure the pivot source range, rows, columns, data fields, etc.
// (Omitted for brevity – see Aspose.Cells docs for detailed setup)

// Wrap the worksheet in a new workbook
Workbook newWorkbook = new Workbook();
newWorkbook.getWorksheets().addCopy(tempSheet);
newWorkbook.save("YOUR_DIRECTORY/created_from_sheet.xlsx");
```

Ao adicionar a planilha a um novo `Workbook` depois que a tabela dinâmica estiver totalmente definida, você garante que **como preservar tabela dinâmica** funcione mesmo quando a planilha se originou fora de um arquivo existente.

## Dicas práticas e armadilhas comuns

| Dica | Por que importa |
|-----|----------------|
| Use `addCopy` em vez de `copy` | `addCopy` clona o cache subjacente da tabela dinâmica; um simples `copy` pode perder a conexão com a fonte de dados. |
| Mantenha os arquivos de origem e destino no mesmo sistema de arquivos | Caminhos relativos na fonte de dados da tabela dinâmica são resolvidos corretamente, reduzindo erros de “fonte não encontrada”. |
| Verifique o cache da tabela dinâmica após a cópia | Chame `pivot.refresh()` se os dados de origem mudaram entre a cópia e a operação de salvamento. |
| Libere as pastas de trabalho quando terminar | `sourceWorkbook.dispose();` libera recursos nativos, o que é importante para arquivos grandes. |

## Casos extremos que você pode encontrar

* **Múltiplas planilhas com tabelas dinâmicas interdependentes** – Copie cada planilha individualmente; caches compartilhados são duplicados automaticamente, mas pode ser necessário reatribuir conexões de dados externas.
* **Tabelas dinâmicas baseadas em consultas SQL externas** – Garanta que o ambiente de destino possa acessar o mesmo banco de dados; caso contrário, a tabela dinâmica exibirá erros “#REF!”. 
* **Pastas de trabalho grandes (>100 MB)** – Use `WorkbookSettings.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` para reduzir a pressão de memória durante a operação de cópia.

## Exemplo completo, executável

Abaixo está o programa completo que incorpora todas as etapas discutidas. Salve-o como `CopyPivotTable.java`, ajuste os caminhos dos arquivos e execute-o com sua IDE preferida ou via `javac`/`java`.



## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [How to Create Pivot Tables in Excel Using Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [How to Update Excel Pivot Table Source with Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [How to Implement Slicers in Pivot Tables Using Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-analysis/implement-slicers-pivot-tables-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}