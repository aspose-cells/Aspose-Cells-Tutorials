---
category: general
date: 2026-11-22
description: Aprenda como exportar o Excel como texto e criar um arquivo delimitado
  por tabulação. Este guia mostra como definir a citação de todos os campos e salvar
  o texto da planilha de forma eficiente.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel as text
- quote all fields
- create tab-delimited file
- save spreadsheet text
- export spreadsheet tab-delimited
language: pt
lastmod: 2026-11-22
og_description: Exporte o Excel como texto e crie um arquivo delimitado por tabulação.
  Siga este tutorial passo a passo para colocar aspas em todos os campos e salvar
  o texto da planilha com Java.
og_image_alt: Screenshot showing Java code that exports an Excel workbook as a tab‑delimited
  text file
og_title: Exportar Excel como texto – guia de arquivo delimitado por tabulação
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn how to export Excel as text and create a tab‑delimited file.
    This guide shows setting quote all fields and saving spreadsheet text efficiently.
  headline: How to export Excel as text with tab‑delimited output
  type: TechArticle
- description: Learn how to export Excel as text and create a tab‑delimited file.
    This guide shows setting quote all fields and saving spreadsheet text efficiently.
  name: How to export Excel as text with tab‑delimited output
  steps:
  - name: Prepare the workbook and sample data
    text: Creating a workbook gives you something to export. In a real project you
      would load an existing file with `new Workbook("input.xlsx")`; here we generate
      a tiny sheet so the example runs out‑of‑the‑box.
  - name: Configure export options – delimiter, quoting, and output mode
    text: The core of **export spreadsheet tab‑delimited** lies in `ExportTableOptions`.
      You set the delimiter to a tab (`'\t'`) and enable `setQuoteAllFields(true)`
      so every cell is wrapped in double quotes. This eliminates ambiguity when a
      cell itself contains a tab or newline.
  - name: Save the workbook as a tab‑delimited text file
    text: Now you actually **export excel as text**. The `save` method takes the target
      path and the `ExportOptions` you configured.
  type: HowTo
tags:
- export excel as text
- quote all fields
- tab-delimited file
- spreadsheet export
- Java
title: Como exportar o Excel como texto com saída delimitada por tabulação
url: /pt/java/excel-import-export/how-to-export-excel-as-text-with-tab-delimited-output/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como exportar Excel como texto com saída delimitada por tabulação

Se você precisa **exportar Excel como texto**, este tutorial orienta todo o processo de criação de um arquivo delimitado por tabulação a partir de uma pasta de trabalho. Seja construindo um pipeline de migração de dados ou precisando de um despejo rápido no estilo CSV para processamento posterior, as etapas abaixo permitem que você **salve o texto da planilha** com controle total sobre delimitadores e aspas.

Exportar dados da planilha como texto simples costuma ser mais portátil do que manter o formato nativo `.xlsx`. Neste guia você também aprenderá a **citar todos os campos**, o que garante que valores contendo tabulações, vírgulas ou quebras de linha sejam encapsulados com segurança.

## O que você precisará

Antes de começar, certifique‑se de que tem:

* Java 17 ou superior instalado.  
* A biblioteca Aspose.Cells for Java (o código usa `ExportOptions` e `ExportTableOptions` desta biblioteca). Você pode adicioná‑la via Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
</dependency>
```

* Uma IDE ou um editor de texto simples para compilar e executar o programa Java.

## Exportar Excel como texto – passo a passo

As seções a seguir dividem a tarefa em três etapas lógicas. Cada etapa explica **por que** ela é importante, não apenas **o que** digitar.

### Etapa 1: Preparar a pasta de trabalho e os dados de exemplo

Criar uma pasta de trabalho fornece algo para exportar. Em um projeto real você carregaria um arquivo existente com `new Workbook("input.xlsx")`; aqui geramos uma planilha pequena para que o exemplo funcione imediatamente.

```java
import com.aspose.cells.*;

public class ExportExcelAsText {
    public static void main(String[] args) throws Exception {
        // Load an existing workbook or create a new one
        Workbook wb = new Workbook();
        Worksheet sheet = wb.getWorksheets().get(0);

        // Populate sample data – this will be part of the exported text
        sheet.getCells().get("A1").setValue("Name");
        sheet.getCells().get("B1").setValue("Age");
        sheet.getCells().get("A2").setValue("Alice");
        sheet.getCells().get("B2").setValue(30);
        sheet.getCells().get("A3").setValue("Bob, Jr."); // contains a comma
        sheet.getCells().get("B3").setValue(25);
```

*Por que esta etapa?*  
Uma pasta de trabalho é o objeto fonte para qualquer operação de exportação. Ao adicionar algumas linhas você pode verificar que a opção **citar todos os campos** realmente protege vírgulas e outros caracteres especiais.

### Etapa 2: Configurar as opções de exportação – delimitador, aspas e modo de saída

O núcleo do **exportar planilha delimitada por tabulação** está em `ExportTableOptions`. Você define o delimitador como uma tabulação (`'\t'`) e habilita `setQuoteAllFields(true)` para que cada célula seja envolvida em aspas duplas. Isso elimina ambiguidades quando uma célula contém uma tabulação ou quebra de linha.

```java
        // Step 2: Create table export options and configure delimiter and quoting
        ExportTableOptions tableExportOptions = new ExportTableOptions();
        tableExportOptions.setDelimiter('\t');            // Use a tab as the field separator
        tableExportOptions.setQuoteAllFields(true);      // Quote every field for safety

        // Create overall export options and attach the table options
        ExportOptions exportOptions = new ExportOptions();
        exportOptions.setExportTableOptions(tableExportOptions);
        exportOptions.setExportAsString(true);            // Produce plain‑text output
```

*Por que esta etapa?*  
- **Delimitador** determina como as colunas são separadas. Uma tabulação (`\t`) cria um **arquivo delimitado por tabulação** que muitas ferramentas de processamento de dados aceitam.  
- **Citar todos os campos** garante que, mesmo que uma célula contenha o delimitador, o texto resultante continue analisável.  
- Definir `ExportAsString` indica ao Aspose.Cells que deve gerar uma string em vez de uma pasta de trabalho binária, que é exatamente o que você precisa para **salvar o texto da planilha**.

### Etapa 3: Salvar a pasta de trabalho como um arquivo de texto delimitado por tabulação

Agora você realmente **exporta Excel como texto**. O método `save` recebe o caminho de destino e as `ExportOptions` que você configurou.

```java
        // Step 3: Save the workbook as a tab‑delimited text file
        wb.save("output/table.txt", exportOptions);
    }
}
```

Quando o programa terminar, você encontrará `output/table.txt` contendo:

```
"Name"	"Age"
"Alice"	"30"
"Bob, Jr."	"25"
```

*Por que esta etapa?*  
A chamada `save` grava o **arquivo delimitado por tabulação** no disco, efetivamente **salvando o texto da planilha** em um formato que pode ser aberto pelo Excel, Notepad ou qualquer ferramenta de importação de dados que reconheça tabulações.

## Como citar todos os campos ao exportar Excel como texto

Se você omitir `setQuoteAllFields(true)`, células que contenham tabulações, vírgulas ou quebras de linha quebrarão a estrutura do arquivo de saída. Por exemplo, a linha `Bob, Jr.` seria dividida em duas colunas, corrompendo o conjunto de dados. Sempre habilite a citação quando:

* Seus dados de origem podem conter vírgulas, tabulações ou quebras de linha.  
* Os analisadores posteriores esperam arquivos CSV/TSV citados.  
* Você precisa de uma exportação determinística independentemente do conteúdo das células.

## Criando um arquivo delimitado por tabulação sem Aspose.Cells (opcional)

Se preferir uma solução pura em Java sem bibliotecas de terceiros, você pode percorrer as linhas e gravá‑las manualmente:

```java
try (PrintWriter pw = new PrintWriter(new FileWriter("output/manual.txt"))) {
    for (int r = 0; r < sheet.getCells().getMaxDataRow() + 1; r++) {
        List<String> rowValues = new ArrayList<>();
        for (int c = 0; c < sheet.getCells().getMaxDataColumn() + 1; c++) {
            String value = sheet.getCells().get(r, c).getStringValue();
            // Quote all fields manually
            rowValues.add('"' + value.replace("\"", "\"\"") + '"');
        }
        pw.println(String.join("\t", rowValues));
    }
}
```

Este trecho demonstra a mesma lógica de **exportar planilha delimitada por tabulação**: delimitador de tabulação, citando cada campo e gravando o resultado como texto simples. Contudo, usar Aspose.Cells simplifica o manuseio de pastas de trabalho grandes, preserva a formatação e reduz o código boilerplate.

## Armadilhas comuns e dicas avançadas

| Problema | Por que acontece | Solução |
|----------|------------------|---------|
| **Tabulações ausentes na saída** | Delimitador deixado como vírgula padrão. | Chame explicitamente `setDelimiter('\t')`. |
| **Vírgulas não citadas quebram colunas** | `quoteAllFields` não habilitado. | Use `setQuoteAllFields(true)` ou cite manualmente. |
| **Arquivo não criado** | Diretório de saída não existe. | Garanta que a pasta `output/` exista ou use `Files.createDirectories`. |
| **Problemas de codificação** | Codificação padrão da plataforma pode corromper caracteres não‑ASCII. | Passe `ExportOptions.setEncoding(Encoding.getUTF8())` se necessário. |

## Testando o resultado

Após executar o programa:

1. Abra `output/table.txt` em um editor de texto simples. Você deverá ver cada valor envolto em aspas duplas e as colunas separadas por um único caractere de tabulação.  
2. Importe o arquivo no Excel (`Dados → De Texto/CSV`). Escolha **Tab** como delimitador; o Excel colocará corretamente cada valor citado em sua própria célula.  
3. Verifique que caracteres especiais (vírgulas, quebras de linha etc.) permanecem intactos.

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [how to export excel – Tab‑Delimited Text Guide](/cells/english/net/converting-excel-files-to-other-formats/how-to-export-excel-tab-delimited-text-guide/)
- [Save Excel as Text File with Custom Separator using Aspose.Cells](/cells/english/net/workbook-operations/save-excel-text-custom-separator-aspose-cells-net/)
- [How to save Excel as text with Aspose.Cells – step‑by‑step guide](/cells/english/net/converting-excel-files-to-other-formats/how-to-save-excel-as-text-with-aspose-cells-step-by-step-gui/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}