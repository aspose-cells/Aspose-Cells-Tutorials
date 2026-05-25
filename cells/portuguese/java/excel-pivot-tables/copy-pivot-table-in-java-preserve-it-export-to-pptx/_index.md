---
category: general
date: 2026-03-01
description: Copie a tabela dinâmica em Java preservando o pivô, depois exporte o
  Excel para PPTX, desative o AutoFiltro do Excel e use Smart Marker para arrays JSON
  – guia completo passo a passo.
draft: false
keywords:
- copy pivot table
- preserve pivot table
- use smart marker
- disable excel autofilter
- export excel to pptx
language: pt
og_description: Copiar tabela dinâmica em Java, preservar a definição da tabela dinâmica,
  exportar para PPTX, desativar AutoFilter e usar Smart Marker – guia completo para
  desenvolvedores.
og_title: Copiar Tabela Dinâmica em Java – Preserve‑a, Exporte para PPTX
tags:
- Aspose.Cells
- Java
- Excel Automation
title: Copiar Tabela Dinâmica em Java – Preservá‑la, Exportar para PPTX
url: /pt/java/excel-pivot-tables/copy-pivot-table-in-java-preserve-it-export-to-pptx/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Copiar Tabela Dinâmica em Java – Preservá‑la, Exportar para PPTX

Já precisou **copiar tabela dinâmica** de uma pasta de trabalho para outra sem perder a definição subjacente da tabela dinâmica? Você não é o único coçando a cabeça com isso. Em muitos projetos do mundo real, você acabará movendo dados, e a última coisa que deseja é uma tabela dinâmica quebrada que gera erros em tempo de execução.  

Neste tutorial, percorreremos uma solução completa que não só **copia tabela dinâmica** mas também mostra como **preservar tabela dinâmica** ao copiar, **exportar Excel para PPTX**, **desativar AutoFilter do Excel**, e **usar smart marker** para inserir um array JSON em uma única célula. Ao final, você terá um único programa Java executável que cobre todos os quatro cenários.

## Pré-requisitos

- Java 8 ou superior (o código funciona também com Java 11)  
- Biblioteca Aspose.Cells for Java (versão 23.9 ou posterior) – você pode obtê‑la no Maven Central  
- Familiaridade básica com conceitos do Excel como tabelas dinâmicas, tabelas e caixas de texto  

Se estiver faltando o JAR do Aspose.Cells, adicione isto ao seu `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
</dependency>
```

Agora, vamos mergulhar.

## Etapa 1: Copiar Tabela Dinâmica – Preservando a Definição da Tabela Dinâmica

Quando você simplesmente copia o intervalo de células que contém uma tabela dinâmica, os metadados da tabela dinâmica frequentemente ficam para trás. Aspose.Cells nos oferece uma maneira prática de manter a definição intacta usando `copyRange` com uma instância de `CopyOptions`.

```java
import com.aspose.cells.*;

public class PivotCopyDemo {

    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook that contains the pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/src.xlsx");
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);

        // 2️⃣ Define the range that includes the pivot (A1:G20 is just an example)
        Range pivotRange = sourceSheet.getCells().createRange("A1:G20");

        // 3️⃣ Prepare the destination workbook
        Workbook destWorkbook = new Workbook();
        Worksheet destSheet = destWorkbook.getWorksheets().get(0);

        // 4️⃣ Copy the range – the pivot definition travels with it
        destSheet.getCells().copyRange(pivotRange,
                new CellArea(0, 0, 19, 6), // destination area (rows 0‑19, cols 0‑6)
                new CopyOptions());

        // 5️⃣ Save the result
        destWorkbook.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

**Por que isso funciona:** `CopyOptions` indica ao Aspose.Cells que copie tudo, incluindo o cache da tabela dinâmica e as configurações de campo. Sem ele, você acabará com valores simples e perderá a capacidade de atualizar a tabela dinâmica.

**Caso de borda:** Se a sua tabela dinâmica de origem abranger mais do que o intervalo codificado `A1:G20`, ajuste o intervalo adequadamente ou use `sourceSheet.getPivotTables().get(0).getDataRange()` para obtê‑lo dinamicamente.

![Exemplo de cópia de tabela dinâmica](image.png "Copiar tabela dinâmica em Java")

*Texto alternativo da imagem: diagrama de cópia de tabela dinâmica em Java*

## Etapa 2: Exportar uma Planilha com uma Caixa de Texto Editável para PPTX

Frequentemente você precisa transformar uma planilha Excel em um slide PowerPoint — pense em dashboards semanais que precisam ser apresentados. Aspose.Cells pode salvar diretamente uma planilha como um arquivo PPTX preservando formas como caixas de texto.

```java
import com.aspose.cells.*;

public class ExportToPptxDemo {

    public static void main(String[] args) throws Exception {
        // Load workbook that contains a TextBox shape
        Workbook wb = new Workbook("YOUR_DIRECTORY/textbox.xlsx");

        // Export the first worksheet to PPTX
        wb.save("YOUR_DIRECTORY/output.pptx", SaveFormat.PPTX);

        System.out.println("Worksheet exported to PPTX successfully.");
    }
}
```

**O que está acontecendo:** O método `save` com `SaveFormat.PPTX` converte a planilha inteira, incluindo qualquer TextBox editável, em um slide PowerPoint. O texto dentro da caixa permanece editável ao abrir o PPTX no PowerPoint.

**Dica:** Se você tem várias planilhas e deseja apenas uma específica, chame `wb.getWorksheets().removeAt(index)` nas demais antes de salvar.

## Etapa 3: Desativar AutoFilter do Excel em uma Tabela

AutoFilter é útil para os usuários finais, mas às vezes você precisa desativá‑lo programaticamente — talvez antes de exportar dados ou ao gerar um relatório limpo. Veja como **desativar excel autofilter** em uma tabela do Excel.

```java
import com.aspose.cells.*;

public class DisableAutoFilterDemo {

    public static void main(String[] args) throws Exception {
        Workbook wb = new Workbook("YOUR_DIRECTORY/textbox.xlsx");
        Worksheet sheet = wb.getWorksheets().get(0);

        // Assume the first table in the sheet is the target
        Table table = sheet.getTables().get(0);

        // Turn off the AutoFilter arrows
        table.setShowAutoFilter(false);

        // Save the modified workbook
        wb.save("YOUR_DIRECTORY/noFilter.xlsx");
        System.out.println("AutoFilter disabled and workbook saved.");
    }
}
```

**Por que você pode precisar disso:** Exportar para formatos que não suportam AutoFilter (como CSV ou PDF) pode fazer ícones de filtro aparecerem. Desativá‑lo garante uma saída limpa.

**Armadilha comum:** Se a planilha não possuir tabelas, `getTables().get(0)` lançará uma `IndexOutOfBoundsException`. Sempre verifique `sheet.getTables().size()` primeiro em código de produção.

## Etapa 4: Usar Smart Marker – Inserir um Array JSON como Valor de Uma Única Célula

Smart Marker é o mecanismo de templating da Aspose. Um truque útil é tratar um array JSON inteiro como valor de uma única célula, o que é perfeito para logging ou para passar dados estruturados adiante. Vamos **usar smart marker** para conseguir isso.

```java
import com.aspose.cells.*;

public class SmartMarkerDemo {

    public static void main(String[] args) throws Exception {
        Workbook wb = new Workbook("YOUR_DIRECTORY/textbox.xlsx");

        // Initialise the SmartMarker processor with the workbook
        SmartMarkerProcessor processor = new SmartMarkerProcessor(wb);

        // JSON array we want to embed
        String jsonArray = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":28}]";

        // Configure the processor to treat arrays as a single cell
        processor.setOptions(SmartMarkerOptions.ArrayAsSingle);

        // Apply the marker – assume cell A1 contains the marker ${json}
        processor.apply(jsonArray);

        // Save the result
        wb.save("YOUR_DIRECTORY/smartMarkerResult.xlsx");
        System.out.println("JSON array inserted via Smart Marker.");
    }
}
```

**Como funciona:** O marcador `${json}` na pasta de trabalho é substituído pela string JSON completa porque definimos `ArrayAsSingle`. Sem essa opção, Aspose tentaria expandir cada elemento do array em linhas separadas.

**Variação:** Se precisar que o array seja dividido em linhas, basta omitir `ArrayAsSingle` e deixar o Smart Marker lidar com a expansão automaticamente.

## Exemplo Completo Funcional – Todas as Etapas Combinadas

Abaixo está uma única classe Java que encadeia todas as operações que abordamos. Execute‑a como um método `main` regular; basta ajustar os caminhos de arquivo para corresponder ao seu ambiente.

```java
import com.aspose.cells.*;

public class CompleteExcelAutomation {

    public static void main(String[] args) throws Exception {
        // ----------- Step 1: Copy Pivot Table -----------
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/src.xlsx");
        Worksheet srcSheet = srcWb.getWorksheets

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}