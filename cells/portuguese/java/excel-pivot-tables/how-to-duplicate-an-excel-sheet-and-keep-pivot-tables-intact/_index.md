---
category: general
date: 2026-10-23
description: Aprenda a duplicar uma planilha do Excel em Java preservando as tabelas
  dinâmicas. Este guia também mostra como copiar tabelas dinâmicas, copiar intervalos
  do Excel e copiar uma planilha com dados de tabela dinâmica.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- duplicate excel sheet
- how to copy pivot
- copy excel range
- copy sheet with pivot
- copy pivot to workbook
language: pt
lastmod: 2026-10-23
og_description: Duplique uma planilha do Excel em Java preservando as tabelas dinâmicas.
  Siga este tutorial completo para copiar tabelas dinâmicas, copiar intervalos do
  Excel e copiar uma planilha com dados de tabela dinâmica.
og_image_alt: Screenshot showing a duplicated Excel sheet with pivot tables preserved
og_title: Duplicar uma planilha do Excel com tabelas dinâmicas em Java – guia passo
  a passo
schemas:
- author: Aspose
  dateModified: '2026-10-23'
  description: Learn how to duplicate an Excel sheet in Java while preserving pivot
    tables. This guide also shows how to copy pivot tables, copy Excel ranges, and
    copy a sheet with pivot data.
  headline: How to duplicate an Excel sheet and keep pivot tables intact in Java
  type: TechArticle
- description: Learn how to duplicate an Excel sheet in Java while preserving pivot
    tables. This guide also shows how to copy pivot tables, copy Excel ranges, and
    copy a sheet with pivot data.
  name: How to duplicate an Excel sheet and keep pivot tables intact in Java
  steps:
  - name: Expected output
    text: 'Running the program creates `DuplicatedWithPivot.xlsx` in the target directory.
      Open the file in Excel and you will see:'
  - name: How to copy pivot to another workbook without copying the whole sheet?
    text: If you only need the pivot and its underlying data, copy the range that
      contains both the source data and the pivot, then use `setCopyPivotTable(true)`.
      The same code from **Step 4** applies; just ensure the range covers the data
      source.
  - name: What if the source workbook has multiple worksheets with pivots?
    text: 'Repeat **Step 3** for each worksheet you want to duplicate:'
  - name: Does this work with protected worksheets?
    text: 'Aspose.Cells can copy protected sheets, but you must unprotect them first
      if you need to modify the pivot after copying:'
  - name: Can I copy a pivot table to an existing workbook that already contains a
      sheet with the same name?
    text: 'Yes. Use `addCopy` with a unique name:'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
- Pivot tables
title: Como duplicar uma planilha do Excel e manter as tabelas dinâmicas intactas
  em Java
url: /pt/java/excel-pivot-tables/how-to-duplicate-an-excel-sheet-and-keep-pivot-tables-intact/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como duplicar uma planilha do Excel e manter as tabelas dinâmicas intactas em Java

Se você precisa **duplicar uma planilha do Excel** enquanto mantém todas as tabelas dinâmicas ativas, este guia mostra exatamente como fazer. Você verá uma solução concisa que copia uma planilha, copia um intervalo específico e até copia uma tabela dinâmica para outra pasta de trabalho — tudo em Java puro usando Aspose.Cells.

Duplicar uma planilha do Excel é uma tarefa comum quando você gera relatórios mensais a partir de um modelo ou quando precisa de uma cópia sandbox para testes. O código abaixo funciona com Aspose.Cells 25.11 ou posterior, que introduziu a opção `setCopyPivotTable(true)`.

## O que você precisará

Antes de começar, certifique‑se de que você tem:

- Java 17 (ou qualquer JDK recente) instalado
- Aspose.Cells for Java 25.11 ou mais recente no seu projeto (coordenada Maven `com.aspose:aspose-cells:25.11`)
- Uma pasta de trabalho fonte (`SourceWithPivot.xlsx`) que já contém uma tabela dinâmica
- Uma IDE ou ferramenta de build de sua escolha (IntelliJ IDEA, Eclipse, Maven, Gradle, etc.)

## Etapa 1: Carregar a pasta de trabalho fonte que contém a tabela dinâmica

A primeira operação é abrir a pasta de trabalho que contém a tabela dinâmica que você deseja preservar.

```java
import com.aspose.cells.*;

public class DuplicateExcelSheet {
    public static void main(String[] args) throws Exception {
        // Load the source workbook with the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
```

> **Por que esta etapa importa:** Carregar a pasta de trabalho fonte lhe dá acesso aos objetos de planilha, células e às tabelas dinâmicas incorporadas. Sem isso, você não pode referenciar os dados da tabela dinâmica que planeja copiar.

## Etapa 2: Criar uma pasta de trabalho de destino vazia (ou carregar uma existente)

Você pode começar a partir de uma pasta de trabalho em branco ou abrir um arquivo existente que receberá a planilha duplicada.

```java
        // Create a new, empty destination workbook
        Workbook dstWb = new Workbook();
```

> **Dica:** Se você já tem uma pasta de trabalho de relatório, substitua a linha acima por `new Workbook("ExistingReport.xlsx")` para adicionar a planilha duplicada a ela.

## Etapa 3: Copiar a planilha inteira – a tabela dinâmica é preservada automaticamente

Copiar a planilha inteira é a maneira mais simples de **copiar planilha com tabela dinâmica**. Aspose.Cells copia a definição da tabela dinâmica e seu cache automaticamente.

```java
        // Access the first worksheet (index 0) from the source workbook
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Add a copy of the source worksheet to the destination workbook
        Worksheet dstWs = dstWb.getWorksheets().addCopy(srcWs);
```

> **Por que funciona:** `addCopy` clona a estrutura da planilha, valores das células, estilos e quaisquer tabelas dinâmicas incorporadas. A nova planilha em `dstWb` ficará idêntica à original, incluindo o cache da tabela dinâmica.

## Etapa 4: (Opcional) Copiar apenas um intervalo específico que inclui a tabela dinâmica

Às vezes você não quer a planilha inteira — talvez precise apenas de uma parte que contenha a tabela dinâmica. É aqui que você **copia intervalo do Excel** e solicita explicitamente que a tabela dinâmica seja copiada.

```java
        // Define the source range that covers the pivot table (adjust as needed)
        Range srcRange = srcWs.getCells().createRange("A1:G30");

        // Define the target range in the destination worksheet
        Range dstRange = dstWs.getCells().createRange("A1");

        // Copy the range and tell Aspose.Cells to include the pivot table
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setCopyPivotTable(true); // new option in 25.11
        dstRange.copy(srcRange, copyOptions);
```

> **Como ajuda:** `setCopyPivotTable(true)` força o mecanismo a duplicar a definição da tabela dinâmica mesmo quando você copia um intervalo limitado. Sem essa flag, apenas os dados brutos seriam copiados e a tabela dinâmica seria perdida.

## Etapa 5: Salvar a pasta de trabalho de destino

Por fim, grave o conteúdo duplicado em um novo arquivo.

```java
        // Save the destination workbook to a new file
        dstWb.save("YOUR_DIRECTORY/DuplicatedWithPivot.xlsx");
    }
}
```

### Saída esperada

Executar o programa cria `DuplicatedWithPivot.xlsx` no diretório de destino. Abra o arquivo no Excel e você verá:

- Uma nova planilha chamada `Sheet1 (Copy)` (ou o nome original com “Copy” anexado)
- A tabela dinâmica aparece exatamente como na planilha fonte, totalmente funcional
- Se você usou a cópia de intervalo opcional, apenas as células A1:G30 estarão presentes, mas a tabela dinâmica ainda funciona porque seu cache foi copiado

## Perguntas comuns e casos de borda

### Como copiar a tabela dinâmica para outra pasta de trabalho sem copiar a planilha inteira?

Se você precisar apenas da tabela dinâmica e dos dados subjacentes, copie o intervalo que contém tanto os dados de origem quanto a tabela dinâmica, então use `setCopyPivotTable(true)`. O mesmo código da **Etapa 4** se aplica; apenas garanta que o intervalo cubra a fonte de dados.

### E se a pasta de trabalho fonte tiver várias planilhas com tabelas dinâmicas?

Repita a **Etapa 3** para cada planilha que você quiser duplicar:

```java
for (int i = 0; i < srcWb.getWorksheets().getCount(); i++) {
    Worksheet ws = srcWb.getWorksheets().get(i);
    dstWb.getWorksheets().addCopy(ws);
}
```

### Isso funciona com planilhas protegidas?

Aspose.Cells pode copiar planilhas protegidas, mas você deve desprotegê‑las primeiro se precisar modificar a tabela dinâmica após a cópia:

```java
srcWs.unprotect("password");
dstWs.unprotect("password");
```

### Posso copiar uma tabela dinâmica para uma pasta de trabalho existente que já contém uma planilha com o mesmo nome?

Sim. Use `addCopy` com um nome exclusivo:

```java
Worksheet dstWs = dstWb.getWorksheets().addCopy(srcWs);
dstWs.setName("PivotCopy_" + System.currentTimeMillis());
```

## Dica profissional: verificar o cache da tabela dinâmica

Após a cópia, você pode confirmar programaticamente que o cache da tabela dinâmica existe:

```java
PivotTable pt = dstWs.getPivotTables().get(0);
System.out.println("Pivot cache ID: " + pt.getCacheIndex());
```

Se o ID do cache imprimir um número não‑negativo, a tabela dinâmica foi duplicada com sucesso.

## Conclusão

Agora você sabe como **duplicar uma planilha do Excel** em Java enquanto preserva todas as tabelas dinâmicas, como **copiar tabelas dinâmicas** diretamente, como **copiar intervalo do Excel** que inclui uma tabela dinâmica e como **copiar planilha com tabela dinâmica** ou **copiar tabela dinâmica para pasta de trabalho** usando Aspose.Cells 25.11+. Aplique esses padrões para automatizar a geração de relatórios, criar clones de modelos ou construir ambientes de teste que necessitam de análises idênticas baseadas em tabelas dinâmicas.

Pronto para explorar mais? Experimente exportar a pasta de trabalho duplicada para PDF, ou atualizar programaticamente o cache da tabela dinâmica após a cópia para garantir que os dados mais recentes sejam refletidos. Feliz codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que expandem as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [How to duplicate worksheet and preserve pivot tables in Java](/cells/english/java/excel-pivot-tables/how-to-duplicate-worksheet-and-preserve-pivot-tables-in-java/)
- [How to Copy Pivot Table in Java – Complete Aspose.Cells Guide](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-complete-aspose-cells-guide/)
- [How to copy range and preserve a pivot table in Java](/cells/english/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}