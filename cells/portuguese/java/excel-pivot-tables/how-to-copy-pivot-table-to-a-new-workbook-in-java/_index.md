---
category: general
date: 2026-10-26
description: Aprenda como copiar uma tabela dinâmica para uma nova pasta de trabalho
  usando Java, preservando a formatação e a definição da tabela dinâmica ao copiar
  um intervalo do Excel com formatação via Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot
- copy excel range
- create empty workbook
- copy range with formatting
language: pt
lastmod: 2026-10-26
og_description: Copie a tabela dinâmica para uma nova pasta de trabalho em Java com
  Aspose.Cells. Este guia mostra como copiar um intervalo do Excel, preservar a formatação
  e criar uma pasta de trabalho vazia de forma eficiente.
og_image_alt: Screenshot of a Java program that copies a pivot table to a new Excel
  workbook
og_title: Copiar tabela dinâmica para uma nova planilha em Java – guia passo a passo
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to copy pivot table to a new workbook using Java, preserving
    formatting and the pivot definition while you copy excel range with formatting
    via Aspose.Cells.
  headline: How to copy pivot table to a new workbook in Java
  type: TechArticle
- description: Learn how to copy pivot table to a new workbook using Java, preserving
    formatting and the pivot definition while you copy excel range with formatting
    via Aspose.Cells.
  name: How to copy pivot table to a new workbook in Java
  steps:
  - name: Prerequisites
    text: '* Java 17 or later. * Aspose.Cells for Java (version 23.10 or newer). *
      Basic familiarity with Java IDEs (IntelliJ IDEA, Eclipse, etc.).'
  - name: Why this works
    text: '* `new Workbook()` **creates empty workbook** with a default sheet, avoiding
      the need to delete existing data. * `CopyOptions` tells Aspose.Cells to copy
      **pivot table** metadata, not just raw values. The `PASTE_ALL` mode also carries
      cell styles, number formats, and conditional formatting—fulfillin'
  - name: Edge cases to consider
    text: '| Situation | Recommended handling | |----------------------------------------|----------------------|
      | Source workbook has multiple pivots | Copy each pivot’s range separately or
      copy the whole sheet. | | Destination already contains data | Choose a non‑conflicting
      start cell (e.g., "H1") when cal'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Como copiar tabela dinâmica para uma nova pasta de trabalho em Java
url: /pt/java/excel-pivot-tables/how-to-copy-pivot-table-to-a-new-workbook-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como copiar tabela dinâmica para uma nova pasta de trabalho em Java

Se você precisar **copy pivot table** de um arquivo Excel para outro, este guia mostra uma solução completa e executável. Você verá como preservar a definição da tabela dinâmica, manter toda a formatação e evitar armadilhas comuns ao copiar um intervalo do Excel.

Copiar uma tabela dinâmica frequentemente levanta dúvidas como *how to copy pivot* sem quebrar a fonte de dados ou perder estilos. Ao final deste tutorial você terá um programa Java autocontido que cria uma pasta de trabalho vazia, copia o intervalo desejado e salva o resultado com a tabela dinâmica intacta.

## O que você vai alcançar

* Carregue uma pasta de trabalho fonte que contém uma tabela dinâmica.  
* **Create empty workbook** que receberá os dados copiados.  
* **Copy excel range** que inclui a tabela dinâmica, usando opções que mantêm a tabela dinâmica e a formatação.  
* Salve o arquivo de destino e verifique se a tabela dinâmica funciona exatamente como a original.

### Pré-requisitos

* Java 17 ou posterior.  
* Aspose.Cells for Java (versão 23.10 ou mais recente).  
* Familiaridade básica com IDEs Java (IntelliJ IDEA, Eclipse, etc.).  

> **Dica profissional:** Use a licença de avaliação gratuita do Aspose.Cells para testes rápidos; substitua-a por uma licença completa antes do uso em produção.

## Copiar tabela dinâmica para uma nova pasta de trabalho

O primeiro passo é configurar as pastas de trabalho de origem e destino. O destino começa com uma chamada **create empty workbook**, que fornece um arquivo limpo com uma única planilha.

```java
import com.aspose.cells.*;

public class CopyPivotExample {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that holds the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // Create an empty workbook that will receive the copied range
        Workbook destWb = new Workbook();

        // Get the first worksheet from each workbook
        Worksheet srcSheet = srcWb.getWorksheets().get(0);
        Worksheet destSheet = destWb.getWorksheets().get(0);

        // Configure copy options to preserve the pivot table and formatting
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.PASTE_ALL); // ensures pivot and styles are kept

        // Copy the range that contains the pivot table
        srcSheet.getCells().copyRange("A1:D20", destSheet.getCells(), "A1", copyOptions);

        // Save the destination workbook
        destWb.save("YOUR_DIRECTORY/destination.xlsx");
    }
}
```

### Por que isso funciona

* `new Workbook()` **creates empty workbook** com uma planilha padrão, evitando a necessidade de excluir dados existentes.  
* `CopyOptions` informa ao Aspose.Cells para copiar os metadados da **pivot table**, não apenas os valores brutos. O modo `PASTE_ALL` também transporta estilos de célula, formatos numéricos e formatação condicional — atendendo ao requisito de **copy range with formatting**.  
* `copyRange` executa uma operação de **copy excel range** que respeita as estruturas internas da origem, de modo que a tabela dinâmica permanece funcional após a cópia.

## Como copiar tabela dinâmica sem perder a formatação

Se você usar apenas o `CopyOptions` padrão, algumas informações de estilo podem ser omitidas em versões mais antigas do Aspose.Cells. Definir explicitamente o tipo de colagem garante que **copy range with formatting** seja respeitado.

```java
CopyOptions copyOptions = new CopyOptions();
copyOptions.setPasteType(PasteType.PASTE_ALL);          // copy values, formulas, formats
copyOptions.setPasteSpecialType(PasteSpecialType.ALL); // include column widths and row heights
```

Adicionar `setPasteSpecialType` garante que larguras de coluna, alturas de linha e até regras de validação de dados sejam transportadas junto com o intervalo. Isso é especialmente útil quando a tabela dinâmica abrange várias colunas com larguras personalizadas.

## Criar pasta de trabalho vazia antes de copiar

Às vezes, desenvolvedores tentam copiar para uma pasta de trabalho existente que já contém dados. Isso pode causar sobreposição de intervalos ou substituições inesperadas. Começar com uma chamada **create empty workbook** isola a operação:

```java
Workbook destWb = new Workbook(); // fresh file with one sheet
Worksheet destSheet = destWb.getWorksheets().get(0); // reference the clean sheet
```

Se você precisar de mais de uma planilha no destino, pode adicioná‑las após a cópia:

```java
destWb.getWorksheets().add("Summary");
```

## Copiar intervalo do Excel com formatação usando CopyOptions

Além de tabelas dinâmicas, o mesmo padrão funciona para qualquer **copy excel range** que requer preservação de formatação — gráficos, tabelas ou formatos condicionais.

```java
// Example: copy a styled table from A1 to G15
srcSheet.getCells().copyRange("A1:G15", destSheet.getCells(), "A1", copyOptions);
```

A instância `CopyOptions` permanece a mesma, portanto você obtém comportamento consistente em diferentes intervalos.

### Casos limites a considerar

| Situação                              | Manipulação recomendada |
|----------------------------------------|--------------------------|
| A pasta de trabalho de origem tem múltiplas tabelas dinâmicas   | Copie o intervalo de cada tabela dinâmica separadamente ou copie a planilha inteira. |
| O destino já contém dados      | Escolha uma célula inicial não conflitante (por exemplo, "H1") ao chamar `copyRange`. |
| A fonte de dados da tabela dinâmica é externa (por exemplo, BD) | Garanta que a pasta de trabalho de destino aponte para a mesma fonte de dados externa, ou atualize a tabela dinâmica após a cópia. |
| Pasta de trabalho grande ( > 10 MB )             | Aumente o tamanho do heap Java (`-Xmx2g`) para evitar `OutOfMemoryError`. |

## Verificar o resultado

Depois de executar o programa, abra `destination.xlsx`. Você deve ver:

* O mesmo layout da tabela dinâmica que está em `source.xlsx`.  
* Todas as cores de célula, formatos numéricos e larguras de coluna preservados.  
* A fonte de dados da tabela dinâmica ainda aponta para o intervalo de dados original dentro do novo arquivo, de modo que atualizar a tabela dinâmica atualiza os valores corretamente.

Se a tabela dinâmica aparecer como uma tabela estática, verifique novamente se `CopyOptions.setPasteType(PasteType.PASTE_ALL)` está definido. Sem essa opção o Aspose.Cells trata a tabela dinâmica como dados simples.

## Conclusão

Agora você sabe como **copy pivot table** para uma nova pasta de trabalho em Java enquanto preserva formatação, conexões de dados e layout da planilha. A solução completa demonstra como carregar um arquivo fonte, **create empty workbook**, configurar as opções de **copy excel range** e salvar o resultado.  

A partir daqui você pode explorar tópicos relacionados, como **how to copy pivot** entre diferentes planilhas, incorporar gráficos ao lado de tabelas dinâmicas ou automatizar o processamento em lote de várias pastas de trabalho. Experimente as configurações do `CopyOptions` para adequá‑las às suas necessidades específicas de automação e você terá um conjunto robusto de ferramentas para manipular Excel ao seu alcance.

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Criar nova pasta de trabalho em Java – Guia completo para copiar tabela dinâmica](/cells/english/java/excel-pivot-tables/create-new-workbook-in-java-full-guide-to-copy-pivot-table/)
- [Copiar tabela dinâmica entre pastas de trabalho – Guia passo a passo em Java](/cells/english/java/excel-pivot-tables/copy-pivot-table-between-workbooks-step-by-step-java-guide/)
- [Como copiar intervalo e preservar uma tabela dinâmica em Java](/cells/english/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}