---
category: general
date: 2026-08-04
description: Copiar tabela dinâmica com Aspose.Cells para Java. Aprenda como copiar
  intervalo do Excel, duplicar tabela dinâmica e copiar planilha com tabela dinâmica
  em apenas algumas linhas.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- copy excel range
- copy range java
- duplicate pivot table
- copy worksheet with pivot
language: pt
lastmod: 2026-08-04
og_description: Copiar tabela dinâmica usando Aspose.Cells para Java. Este tutorial
  orienta você a copiar um intervalo do Excel, duplicar uma tabela dinâmica e preservar
  todos os dados em uma nova planilha.
og_image_alt: Screenshot of a Java program that copies a pivot table to a new worksheet
og_title: Copiar tabela dinâmica em Java – tutorial completo do Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Copy pivot table with Aspose.Cells for Java. Learn how to copy excel
    range, duplicate pivot table, and copy worksheet with pivot in just a few lines.
  headline: Copy pivot table in Java – step‑by‑step guide using Aspose.Cells
  type: TechArticle
- description: Copy pivot table with Aspose.Cells for Java. Learn how to copy excel
    range, duplicate pivot table, and copy worksheet with pivot in just a few lines.
  name: Copy pivot table in Java – step‑by‑step guide using Aspose.Cells
  steps:
  - name: '`CopyWithPivot.xlsx` appears in `YOUR_DIRECTORY`.'
    text: '`CopyWithPivot.xlsx` appears in `YOUR_DIRECTORY`.'
  - name: Opening the file in Excel shows a new sheet named **CopySheet**.
    text: Opening the file in Excel shows a new sheet named **CopySheet**.
  - name: '**CopySheet** contains a fully functional pivot table identical to the
      original, ready to refresh.'
    text: '**CopySheet** contains a fully functional pivot table identical to the
      original, ready to refresh.'
  - name: All formatting, filters, and calculated fields are preserved.
    text: All formatting, filters, and calculated fields are preserved.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
- PivotTable
- Data copying
title: Copiar tabela dinâmica em Java – guia passo a passo usando Aspose.Cells
url: /pt/java/excel-pivot-tables/copy-pivot-table-in-java-step-by-step-guide-using-aspose-cel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Copiar tabela dinâmica em Java – guia passo a passo usando Aspose.Cells

Se você precisar **copiar uma tabela dinâmica** de uma planilha para outra em Java, este guia mostra exatamente como fazer isso com Aspose.Cells. Seja gerando relatórios programaticamente ou construindo uma ferramenta de migração de dados, você verá um exemplo completo e executável que preserva a definição e os dados da tabela dinâmica.

Copiar uma tabela dinâmica é mais do que simplesmente copiar um intervalo de células; o cache subjacente e a fonte de dados devem permanecer intactos. Neste tutorial também abordamos como **copiar intervalo excel**, como **duplicar tabela dinâmica** entre planilhas e como **copiar planilha com tabela dinâmica** usando a mesma API.

## Pré-requisitos

Antes de começar, certifique-se de que você tem:

* Java Development Kit (JDK) 8 ou mais recente.
* Maven ou Gradle para gerenciar dependências.
* Aspose.Cells for Java (a versão mais recente, por exemplo, 23.12). Adicione a seguinte coordenada Maven ao seu `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
</dependency>
```

* Uma pasta de trabalho de origem (`Source.xlsx`) que contém uma tabela dinâmica na primeira planilha.

## Como copiar tabela dinâmica em Java com Aspose.Cells

A ideia principal é copiar o *intervalo de origem* que envolve a tabela dinâmica e, em seguida, colá-lo em uma nova planilha. Aspose.Cells copia automaticamente o cache da tabela dinâmica, de modo que a planilha resultante contém uma **tabela dinâmica duplicada** totalmente funcional.

```java
import com.aspose.cells.*;

public class CopyPivotTableDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the workbook that contains the PivotTable
        Workbook workbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");

        // Step 2: Define the source range (including the PivotTable) to be copied
        // The range must cover the entire pivot table area, e.g., A1:G20
        Range sourceRange = workbook.getWorksheets()
                                    .get(0)                 // first worksheet
                                    .getCells()
                                    .createRange("A1:G20");

        // Step 3: Add a new worksheet that will receive the copied range
        Worksheet destinationSheet = workbook.getWorksheets().add("CopySheet");

        // Step 4: Copy the source range to cell A1 of the new worksheet
        sourceRange.copy(destinationSheet.getCells().createRange("A1"));

        // Step 5: Save the workbook with the copied PivotTable intact
        workbook.save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
    }
}
```

### Por que isso funciona

* **A cópia de intervalo inclui o cache da tabela dinâmica** – Aspose.Cells trata uma tabela dinâmica como um objeto especial incorporado ao intervalo de células. Quando você chama `Range.copy`, a biblioteca copia tanto as células visíveis quanto o cache oculto que alimenta a tabela dinâmica.
* **Nenhuma recriação manual necessária** – Você não precisa reconstruir os campos da tabela dinâmica ou a fonte de dados; a duplicata está pronta para atualizar instantaneamente.
* **Funciona com qualquer versão do Excel** – O arquivo gerado segue o padrão Office Open XML (XLSX), portanto o Excel 2007+ pode abri‑lo sem avisos.

## Copiar intervalo excel – reutilizando o mesmo código para dados sem tabela dinâmica

Se você precisar apenas **copiar intervalo excel** sem uma tabela dinâmica, o mesmo padrão se aplica. Basta ajustar o endereço do intervalo para a região que deseja duplicar.

```java
// Example: copy A1:D10 from Sheet1 to Sheet2
Range dataRange = workbook.getWorksheets()
                          .get(0)
                          .getCells()
                          .createRange("A1:D10");
Worksheet sheet2 = workbook.getWorksheets().add("DataCopy");
dataRange.copy(sheet2.getCells().createRange("A1"));
```

O método `copy` preserva fórmulas, formatação e comentários, tornando‑o uma solução universal para qualquer bloco de dados do Excel.

## Duplicar tabela dinâmica em várias planilhas

Às vezes você precisa **duplicar tabela dinâmica** várias vezes — por exemplo, uma por departamento. Percorra as planilhas de destino e reutilize a mesma chamada `sourceRange.copy`:

```java
String[] departments = {"Sales", "Marketing", "Finance"};
for (String dept : departments) {
    Worksheet ws = workbook.getWorksheets().add(dept + "Pivot");
    sourceRange.copy(ws.getCells().createRange("A1"));
}
```

Cada nova planilha contém uma tabela dinâmica independente que pode ser atualizada separadamente. O cache é duplicado, portanto alterações em uma planilha não afetarão as outras.

## Copiar planilha com tabela dinâmica – preservando configurações ao nível da planilha

Se você quiser **copiar planilha com tabela dinâmica** mantendo também a configuração de página, larguras de coluna e intervalos nomeados, use `Worksheet.copy` em vez de copiar um intervalo manualmente. Esse método clona a planilha inteira, incluindo a tabela dinâmica.

```java
Worksheet original = workbook.getWorksheets().get(0);
Worksheet clone = workbook.getWorksheets().addCopy(original);
clone.setName("FullCopy");
workbook.save("YOUR_DIRECTORY/FullCopy.xlsx");
```

`addCopy` é útil quando a planilha contém gráficos, imagens ou estilos personalizados que precisam ser transferidos junto com a tabela dinâmica.

## Armadilhas comuns e como evitá‑las

| Problema | Por que acontece | Solução |
|----------|------------------|---------|
| **Cache da tabela dinâmica perdido após a cópia** | Usar `Cell.copy` em células individuais (em vez de um intervalo) descarta o cache oculto. | Sempre copie o *intervalo inteiro* que envolve a tabela dinâmica, como mostrado na Etapa 2. |
| **Intervalo de origem muito pequeno** | O intervalo não inclui a área de dados da tabela dinâmica, portanto a nova planilha mostra apenas valores estáticos. | Expanda o endereço (por exemplo, `A1:G20`) para cobrir a tabela dinâmica completa, além de quaisquer segmentações ou filtros. |
| **Incompatibilidade de versão da pasta de trabalho de destino** | Salvar como XLS (legado) elimina recursos modernos de tabela dinâmica. | Salve como XLSX (padrão) ou defina explicitamente `SaveFormat.XLSX`. |
| **Fonte de dados externa quebrada** | A tabela dinâmica aponta para uma fonte de dados fora da pasta de trabalho; a cópia não a incorpora. | Use `PivotTable.refreshData()` após a cópia, ou incorpore os dados de origem na mesma pasta de trabalho. |

## Saída esperada

Após executar o programa:

1. `CopyWithPivot.xlsx` aparece em `YOUR_DIRECTORY`.
2. Abrir o arquivo no Excel mostra uma nova planilha chamada **CopySheet**.
3. **CopySheet** contém uma tabela dinâmica totalmente funcional, idêntica à original, pronta para atualizar.
4. Toda a formatação, filtros e campos calculados são preservados.

Se você abrir `FullCopy.xlsx`, verá uma réplica completa da planilha original, incluindo quaisquer gráficos ou imagens que estavam na planilha de origem.

## Recapitulação

* Você aprendeu como **copiar tabela dinâmica** em Java usando Aspose.Cells.
* A mesma abordagem funciona para um simples **copiar intervalo excel** ou cenários de **copy range java**.
* Para operações em massa, você pode **duplicar tabela dinâmica** em várias planilhas.
* Quando precisar de toda a planilha, **copiar planilha com tabela dinâmica** usando `addCopy`.

## Próximos passos

* Explore **PivotTable.refreshData()** para atualizar programaticamente o cache após a cópia.
* Combine a lógica de cópia com **Excel file streaming** para lidar com pastas de trabalho grandes sem carregar tudo na memória.
* Confira o suporte do Aspose.Cells a **pivot slicers** se seus relatórios dependem de filtros interativos.

Sinta‑se à vontade para adaptar o código à estrutura do seu próprio projeto, experimentar diferentes tamanhos de intervalo ou integrá‑lo a um pipeline de processamento de dados maior. Feliz codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Como atualizar a fonte da tabela dinâmica do Excel com Aspose.Cells para Java: um guia abrangente](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Manipulação de Tabela Dinâmica do Excel Aspose Cells Java](/cells/hongkong/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)
- [Criar nova pasta de trabalho Excel – Copiar & Duplicar Tabela Dinâmica](/cells/english/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}