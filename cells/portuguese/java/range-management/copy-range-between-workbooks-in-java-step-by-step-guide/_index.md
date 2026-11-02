---
category: general
date: 2026-08-14
description: Copie intervalo entre pastas de trabalho com Java usando Aspose.Cells.
  Aprenda a copiar a planilha de tabela dinâmica, exportar imagem para PowerPoint
  e remover o AutoFiltro de uma tabela do Excel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy range between workbooks
- copy pivot table workbook
- export picture to powerpoint
- copy excel range to new workbook
- remove autofilter from excel table
language: pt
lastmod: 2026-08-14
og_description: Copiar intervalo entre pastas de trabalho em Java. Este guia mostra
  como copiar a pasta de trabalho da tabela dinâmica, exportar imagem para PowerPoint
  e remover o AutoFiltro da tabela do Excel.
og_image_alt: Screenshot of Java code copying range between workbooks with Aspose.Cells
og_title: Copiar intervalo entre pastas de trabalho em Java – tutorial completo do
  Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Copy range between workbooks with Java using Aspose.Cells. Learn to
    copy pivot table workbook, export picture to PowerPoint and remove AutoFilter
    from Excel table.
  headline: Copy range between workbooks in Java – step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
- PowerPoint export
title: Copiar intervalo entre pastas de trabalho em Java – guia passo a passo
url: /pt/java/range-management/copy-range-between-workbooks-in-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Copiar intervalo entre pastas de trabalho em Java – guia passo a passo

Se você precisa **copiar intervalo entre pastas de trabalho** em Java, o Aspose.Cells oferece uma API limpa que manipula objetos complexos como tabelas dinâmicas e imagens. Este tutorial mostra como **copiar a pasta de trabalho da tabela dinâmica**, **exportar imagem para PowerPoint** e **remover AutoFilter de uma tabela do Excel** mantendo o código fácil de ler e manter.

Você aprenderá a:

* Carregar uma pasta de trabalho de origem e definir o intervalo de origem.  
* Criar uma pasta de trabalho de destino e copiar o intervalo de modo que a tabela dinâmica permaneça intacta.  
* Exportar a primeira imagem da planilha como um objeto editável do PowerPoint.  
* Remover um AutoFilter da primeira tabela do Excel.  
* Carregar uma pasta de trabalho com `SmartMarkerOptions` para tratar arrays JSON como um único valor de célula.

O exemplo usa Aspose.Cells 23.10 para Java, mas os conceitos se aplicam a versões anteriores também.

---

## Pré‑requisitos

| Requisito | Por que é importante |
|-----------|----------------------|
| Java 17 ou superior | Necessário para o runtime mais recente do Aspose.Cells. |
| Aspose.Cells for Java (artefato Maven `com.aspose:aspose-cells`) | Fornece as classes `Workbook`, `Worksheet`, `Range` e relacionadas usadas no código. |
| Um arquivo Excel de origem (`src.xlsx`) que contém uma tabela dinâmica, uma imagem e uma tabela com AutoFilter. | O tutorial manipula esses objetos para demonstrar cada recurso. |

Adicione a dependência Maven ao seu `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

---

## Copiar intervalo entre pastas de trabalho – carregar origem e destino

A primeira etapa é abrir a pasta de trabalho de origem, selecionar o intervalo que contém os dados que você deseja copiar e criar uma pasta de trabalho de destino vazia.

```java
import com.aspose.cells.*;

public class CopyRangeDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that holds the pivot table, picture, and table.
        Workbook sourceWb = new Workbook("YOUR_DIRECTORY/src.xlsx");
        Worksheet sourceWs = sourceWb.getWorksheets().get(0);

        // Define the range that includes the pivot table (A1:G20 in this example).
        Range sourceRange = sourceWs.getCells().createRange("A1:G20");

        // Create a new workbook that will receive the copied range.
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);
        Range destRange = destWs.getCells().createRange("A1");
```

> **Por que isso importa:** Ao usar `Range.copy`, o Aspose.Cells copia não apenas os valores brutos das células, mas também o cache subjacente da tabela dinâmica, mantendo a tabela dinâmica funcional na pasta de trabalho de destino.

---

## Copiar pasta de trabalho da tabela dinâmica ao copiar o intervalo

Agora copie o intervalo definido da pasta de trabalho de origem para a pasta de trabalho de destino. A tabela dinâmica é preservada automaticamente porque o intervalo inclui o cache da tabela dinâmica.

```java
        // Copy the source range to the destination range.
        destRange.copy(sourceRange);

        // Save the intermediate workbook to verify that the pivot table was copied.
        destWb.save("YOUR_DIRECTORY/destination.xlsx");
```

> **Resultado:** Ao abrir `destination.xlsx` você verá o mesmo layout de tabela dinâmica de `src.xlsx`. Nenhum código adicional é necessário para reconstruir o cache da tabela dinâmica.

---

## Exportar imagem para PowerPoint

O Aspose.Cells pode marcar uma imagem para exportação como um objeto editável do PowerPoint. O código a seguir seleciona a primeira imagem na planilha de destino e define a bandeira de exportação.

```java
        // Retrieve the first picture on the destination sheet.
        Shape picture = destWs.getPictures().get(0);

        // Instruct Aspose.Cells to export this picture as a PowerPoint object.
        picture.getPictureFormat().setExportToPptx(true);

        // Optionally, save the workbook as PPTX to see the result.
        destWb.save("YOUR_DIRECTORY/destination.pptx");
```

> **O que você vê:** Ao abrir `destination.pptx` no PowerPoint, a imagem aparece como uma forma nativa que pode ser editada, redimensionada ou animada.

---

## Remover AutoFilter da tabela do Excel

Se a planilha de origem contém uma tabela com AutoFilter, você pode querer limpá‑lo após a cópia. O código abaixo acessa a primeira tabela e remove seu filtro.

```java
        // Access the first table on the destination sheet.
        Table table = destWs.getTables().get(0);

        // Remove the AutoFilter by assigning null.
        table.setAutoFilter(null);

        // Save the final workbook.
        destWb.save("YOUR_DIRECTORY/final_output.xlsx");
```

> **Efeito:** A tabela permanece na pasta de trabalho, mas as setas de filtro suspensas desaparecem, proporcionando uma visualização de dados limpa.

---

## Carregar pasta de trabalho com opções SmartMarker – tratar arrays JSON como um único valor de célula

Ao gerar um relatório a partir de JSON, o Aspose.Cells pode tratar um array inteiro como um único valor de célula. Isso é útil para inserir strings JSON em um modelo sem expandi‑las em várias células.

```java
        // Configure LoadOptions to enable SmartMarker array handling.
        LoadOptions loadOptions = new LoadOptions();
        SmartMarkerOptions smOptions = new SmartMarkerOptions();
        smOptions.setArrayAsSingle(true);
        loadOptions.setSmartMarkerOptions(smOptions);

        // Load a template workbook using the configured options.
        Workbook smartMarkerWb = new Workbook("YOUR_DIRECTORY/template.xlsx", loadOptions);

        // Continue processing (e.g., populate markers) as needed.
        // ...

        // Save the processed workbook.
        smartMarkerWb.save("YOUR_DIRECTORY/template_filled.xlsx");
    }
}
```

> **Por que você pode usar isso:** Se sua carga JSON contém um array que deve aparecer como uma string JSON em uma única célula, `setArrayAsSingle(true)` impede que o Aspose.Cells expanda o array em linhas ou colunas separadas.

---

![Copy range between workbooks in Java – Aspose.Cells code example](copy-range-workbooks.png)

*Texto alternativo da imagem:* **Copy range between workbooks in Java – Aspose.Cells code example** (corresponde à palavra‑chave principal).

---

## Saída esperada

| Nome do arquivo | Contém |
|-----------------|--------|
| `destination.xlsx` | Intervalo copiado com tabela dinâmica funcional. |
| `destination.pptx` | Imagem exportada como forma editável do PowerPoint. |
| `final_output.xlsx` | Tabela sem setas de AutoFilter. |
| `template_filled.xlsx` | Array JSON armazenado como um único valor de célula. |

Abra cada arquivo no aplicativo apropriado (Excel ou PowerPoint) para verificar se as operações foram bem‑sucedidas.

---

## Conclusão

Agora você sabe como **copiar intervalo entre pastas de trabalho** em Java usando Aspose.Cells, preservando uma tabela dinâmica, exportando uma imagem para PowerPoint e removendo um AutoFilter de uma tabela do Excel. O mesmo padrão pode ser estendido para copiar qualquer intervalo do Excel para uma nova pasta de trabalho, manipular arrays JSON com SmartMarker ou encadear transformações adicionais.

Próximos passos que você pode explorar:

* **Copiar intervalo do Excel para nova pasta de trabalho** com várias planilhas.  
* Usar **export picture to PowerPoint** para extração em lote de imagens.  
* Aplicar **remove autofilter from excel table** em pipelines de relatórios maiores.  
* Combinar essas técnicas com Aspose.Slides para automação completa de Excel‑para‑PowerPoint.

Sinta‑se à vontade para experimentar diferentes endereços de intervalo, múltiplas tabelas dinâmicas ou formatos de imagem personalizados. A API do Aspose.Cells foi projetada para flexibilidade programática, permitindo que você adapte os padrões mostrados aqui a qualquer cenário de automação corporativa do Excel.


## O que você deve aprender a seguir?


Os tutoriais a seguir cobrem tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Copy Images Between Sheets in Excel Using Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/images-shapes/copy-images-between-sheets-excel-aspose-cells-java/)
- [Copy Page Setup Settings Between Worksheets in Excel Using Aspose.Cells Java](/cells/english/java/headers-footers/copy-page-setup-excel-aspose-cells-java/)
- [Excel Copy Worksheets Between Workbooks](/cells/english/net/excel-copy-worksheet/excel-copy-worksheets-between-workbooks/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}