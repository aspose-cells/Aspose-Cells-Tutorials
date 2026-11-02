---
category: general
date: 2026-09-18
description: como duplicar uma tabela dinâmica em Java com Aspose.Cells – copie uma
  tabela dinâmica entre pastas de trabalho de forma rápida e confiável.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to duplicate pivot
- copy range between workbooks
- how to copy pivot
- copy pivot to workbook
- load excel workbook java
language: pt
lastmod: 2026-09-18
og_description: como duplicar uma tabela dinâmica em Java usando Aspose.Cells. Siga
  este tutorial completo para copiar uma tabela dinâmica entre pastas de trabalho
  com código Java limpo.
og_image_alt: Screenshot showing a Java IDE copying a pivot table between two Excel
  workbooks
og_title: Duplicar uma tabela dinâmica em Java – guia passo a passo
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: how to duplicate pivot in Java with Aspose.Cells – copy a pivot table
    between workbooks quickly and reliably.
  headline: How to duplicate pivot in Java using Aspose.Cells
  type: TechArticle
- description: how to duplicate pivot in Java with Aspose.Cells – copy a pivot table
    between workbooks quickly and reliably.
  name: How to duplicate pivot in Java using Aspose.Cells
  steps:
  - name: '**Load the source workbook** – this gives you access to the worksheet that
      holds the pivot.'
    text: '**Load the source workbook** – this gives you access to the worksheet that
      holds the pivot.'
  - name: '**Define the cell area** that encloses the pivot.'
    text: '**Define the cell area** that encloses the pivot.'
  - name: '**Create a destination workbook** – an empty file that will receive the
      copied range.'
    text: '**Create a destination workbook** – an empty file that will receive the
      copied range.'
  - name: '**Copy the range** – Aspose.Cells automatically duplicates the pivot definition.'
    text: '**Copy the range** – Aspose.Cells automatically duplicates the pivot definition.'
  - name: '**Save the destination workbook** – you now have a separate file with the
      same pivot.'
    text: '**Save the destination workbook** – you now have a separate file with the
      same pivot.'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Como duplicar uma tabela dinâmica em Java usando Aspose.Cells
url: /pt/java/excel-pivot-tables/how-to-duplicate-pivot-in-java-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como duplicar uma tabela dinâmica em Java usando Aspose.Cells

Se você precisa **como duplicar uma tabela dinâmica** em uma aplicação Java, este guia mostra as etapas exatas. Ao carregar uma pasta de trabalho Excel, definir a área de células da tabela dinâmica e copiar esse intervalo para uma nova pasta de trabalho, você pode mover uma tabela dinâmica sem perder sua definição ou dados.

Copiar uma tabela dinâmica é uma necessidade comum ao gerar relatórios, arquivar análises ou dividir uma grande pasta de trabalho em partes modulares. Neste tutorial você aprenderá como **copiar intervalo entre pastas de trabalho**, como **carregar pasta de trabalho Excel Java**, e as nuances de **como copiar uma tabela dinâmica** com segurança.

Você terminará com um programa Java pronto‑para‑executar que duplica uma tabela dinâmica de `Source.xlsx` para `PivotCopied.xlsx` usando Aspose.Cells for Java.

## Pré-requisitos

Antes de começar, certifique‑se de que você tem:

* JDK 8 ou mais recente instalado.
* Maven (ou outra ferramenta de build) para gerenciar dependências.
* Aspose.Cells for Java versão 23.10 ou posterior. Adicione a seguinte dependência Maven ao seu `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier> <!-- adjust classifier to your JDK version -->
</dependency>
```

* Uma pasta de trabalho fonte (`Source.xlsx`) que contém uma tabela dinâmica no intervalo **A1:H30**.

## Como duplicar uma tabela dinâmica em Java

A ideia central é simples:

1. **Carregar a pasta de trabalho fonte** – isso lhe dá acesso à planilha que contém a tabela dinâmica.
2. **Definir a área de células** que envolve a tabela dinâmica.
3. **Criar uma pasta de trabalho de destino** – um arquivo vazio que receberá o intervalo copiado.
4. **Copiar o intervalo** – Aspose.Cells duplica automaticamente a definição da tabela dinâmica.
5. **Salvar a pasta de trabalho de destino** – agora você tem um arquivo separado com a mesma tabela dinâmica.

Abaixo está um programa Java completo e executável que segue essas etapas.

```java
package com.example.excelpivot;

import com.aspose.cells.*;

public class DuplicatePivotExample {

    public static void main(String[] args) throws Exception {
        // ---------- Step 1: Load the source workbook ----------
        // Replace the path with the actual location of your source file.
        String srcPath = "YOUR_DIRECTORY/Source.xlsx";
        Workbook srcWorkbook = new Workbook(srcPath);
        // The first worksheet (index 0) contains the pivot table.
        Worksheet srcWorksheet = srcWorkbook.getWorksheets().get(0);

        // ---------- Step 2: Define the cell area that contains the pivot ----------
        // The pivot occupies A1:H30 in the source sheet.
        CellArea srcRange = CellArea.create("A1", "H30");

        // ---------- Step 3: Create a new workbook for the copy ----------
        Workbook destWorkbook = new Workbook();               // creates a blank workbook
        Worksheet destWorksheet = destWorkbook.getWorksheets().get(0);

        // ---------- Step 4: Copy the range (pivot table is duplicated automatically) ----------
        // CopyOptions can be left default; it ensures that all formatting and pivot objects are preserved.
        srcWorksheet.copyRange(srcRange, destWorksheet, "A1", new CopyOptions());

        // ---------- Step 5: Save the destination workbook ----------
        String destPath = "YOUR_DIRECTORY/PivotCopied.xlsx";
        destWorkbook.save(destPath);

        System.out.println("Pivot table duplicated successfully to " + destPath);
    }
}
```

### Por que isso funciona

* **Aspose.Cells** trata uma tabela dinâmica como parte da coleção de células da planilha. Quando você invoca `copyRange`, a biblioteca copia não apenas os valores das células, mas também o cache e a definição subjacentes da tabela dinâmica, de modo que a nova pasta de trabalho contém um duplicado totalmente funcional.
* O objeto `CopyOptions` tem como padrão a preservação de fórmulas, formatos e objetos incorporados. Você pode customizá‑lo (por exemplo, `setCopyColumnWidths(true)`) se precisar de controle extra.

## Copiar intervalo entre pastas de trabalho – visão aprofundada

Embora o exemplo acima copie um único bloco contíguo, `copyRange` pode lidar com qualquer área retangular. Se sua tabela dinâmica abranger intervalos não adjacentes, você pode chamar `copyRange` várias vezes ou usar `Worksheet.copy` para duplicar a planilha inteira.

```java
// Example: copy the whole sheet, preserving all pivots and charts
srcWorksheet.copy(destWorksheet, new CopyOptions());
```

**Dica:** Ao copiar pastas de trabalho grandes, habilite `CopyOptions.setPreserveCellStyle(true)` para evitar duplicação desnecessária de estilos, o que pode melhorar o desempenho.

## Como copiar uma tabela dinâmica para a pasta de trabalho – lidando com múltiplas tabelas dinâmicas

Se a planilha fonte contiver mais de uma tabela dinâmica, você pode iterar sobre as tabelas dinâmicas da planilha e copiar cada uma individualmente:

```java
for (int i = 0; i < srcWorksheet.getPivotTables().getCount(); i++) {
    PivotTable pt = srcWorksheet.getPivotTables().get(i);
    // Determine the range that the pivot occupies
    CellArea pivotArea = pt.getPivotTableArea();
    srcWorksheet.copyRange(pivotArea, destWorksheet, pt.getName() + "!A1", new CopyOptions());
}
```

Essa abordagem garante que cada tabela dinâmica mantenha seu nome e fonte de dados originais.

## Carregar pasta de trabalho Excel Java – armadilhas comuns

* **Separadores de caminho de arquivo:** Use barras (`/`) ou `File.separator` para manter o código independente de plataforma.
* **Licença ausente:** Aspose.Cells funciona em modo de avaliação, mas a saída conterá uma marca d'água. Registre uma licença com `License license = new License(); license.setLicense("Aspose.Total.Java.lic");` antes de carregar a pasta de trabalho para remover a marca d'água.
* **Arquivos grandes:** Para pastas de trabalho maiores que 100 MB, considere usar `WorkbookFactory.create(InputStream, new LoadOptions(LoadFormat.XLSX))` com opções de streaming para reduzir o consumo de memória.

## Recapitulação do exemplo completo de ponta a ponta

Juntando tudo, aqui está o programa final que você pode copiar‑colar em sua IDE:

```java
package com.example.excelpivot;

import com.aspose.cells.*;

public class DuplicatePivotExample {
    public static void main(String[] args) throws Exception {
        // Load license (optional, removes evaluation watermark)
        // License lic = new License();
        // lic.setLicense("Aspose.Total.Java.lic");

        // 1️⃣ Load source workbook
        Workbook srcWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");
        Worksheet srcWorksheet = srcWorkbook.getWorksheets().get(0);

        // 2️⃣ Define pivot range (A1:H30)
        CellArea srcRange = CellArea.create("A1", "H30");

        // 3️⃣ Prepare destination workbook
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.getWorksheets().get(0);

        // 4️⃣ Copy the pivot (Aspose.Cells handles the pivot cache automatically)
        srcWorksheet.copyRange(srcRange, destWorksheet, "A1", new CopyOptions());

        // 5️⃣ Save the result
        destWorkbook.save("YOUR_DIRECTORY/PivotCopied.xlsx");

        System.out.println("Pivot table duplicated successfully.");
    }
}
```

**Saída esperada:** Após a execução, `PivotCopied.xlsx` aparece no diretório especificado. Ao abri‑lo no Excel, ele mostra o mesmo layout da tabela dinâmica, filtros e dados que em `Source.xlsx`. Todos os campos calculados e formatações são preservados.

## Perguntas frequentes

* **Isso funciona com formatos antigos do Excel (.xls)?**  
  Sim. Aspose.Cells detecta automaticamente o formato. Use `new Workbook("file.xls")` e a mesma lógica de cópia se aplica.

* **E se a tabela dinâmica referenciar fontes de dados externas?**  
  A cópia mantém a referência original da fonte de dados. Se o ambiente de destino não puder acessar essa fonte, a tabela dinâmica exibirá erros `#REF!`. Para evitar isso, atualize a tabela dinâmica após a cópia ou altere sua fonte de dados via `PivotTable.setDataSource(...)`.

* **Posso copiar uma tabela dinâmica para um nome de planilha específico?**  
  Absolutamente. Após criar a planilha de destino, renomeie‑a:

  ```java
  destWorksheet.setName("ReportPivot");
  srcWorksheet.copyRange(srcRange, destWorksheet, "A1", new CopyOptions());
  ```

## Conclusão

Agora você sabe **como duplicar tabelas dinâmicas** em Java usando Aspose.Cells, como **copiar intervalo entre pastas de trabalho**, e as melhores práticas para **carregar pasta de trabalho Excel Java**. Seguindo o processo de cinco etapas — carregar, definir, criar destino, copiar e salvar — você pode automatizar a geração de relatórios, arquivar análises ou dividir pastas de trabalho complexas sem perder a funcionalidade da tabela dinâmica.

Em seguida, explore tópicos relacionados como **copiar tabela dinâmica para pasta de trabalho** com múltiplas planilhas, ou integre a tabela dinâmica duplicada em um pipeline maior de processamento de dados usando Apache POI para cenários não‑Aspose. Experimente diferentes configurações de `CopyOptions` para ajustar o desempenho em pastas de trabalho massivas.

Feliz codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Como criar tabelas dinâmicas no Excel usando Aspose.Cells para Java: Um guia abrangente](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Como atualizar a fonte da tabela dinâmica do Excel com Aspose.Cells para Java: Um guia abrangente](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Agrupar campos de tabela dinâmica em pastas de trabalho Excel usando Aspose.Cells para Java - Guia abrangente](/cells/english/java/data-analysis/aspose-cells-java-group-pivot-fields-excel-workbook/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}