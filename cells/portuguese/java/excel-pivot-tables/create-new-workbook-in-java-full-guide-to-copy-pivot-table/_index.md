---
category: general
date: 2026-07-23
description: Crie uma nova pasta de trabalho em Java e aprenda como copiar tabela
  dinâmica, copiar intervalo do Excel e exportar tabela dinâmica com Aspose.Cells
  em minutos.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new workbook
- copy pivot table
- how to copy pivot
- copy excel range
- export pivot table
language: pt
lastmod: 2026-07-23
og_description: Crie uma nova planilha em Java e copie instantaneamente a tabela dinâmica,
  copie o intervalo do Excel e, em seguida, exporte a tabela dinâmica usando Aspose.Cells.
  Siga este tutorial completo.
og_image_alt: Screenshot of Java code copying a pivot table from one workbook to another
og_title: Criar Nova Pasta de Trabalho em Java – Copiar Tabela Dinâmica Passo a Passo
schemas:
- author: Aspose
  dateModified: '2026-07-23'
  description: Create new workbook in Java and learn how to copy pivot table, copy
    excel range, and export pivot table with Aspose.Cells in minutes.
  headline: Create New Workbook in Java – Full Guide to Copy Pivot Table
  type: TechArticle
- questions:
  - answer: You’ll need to copy each relevant range separately, then recreate the
      pivot on the destination sheet using `PivotTable` APIs.
    question: What if the source pivot spans more than one worksheet?
  - answer: Set `sourceRange.setCopyDataOnly(false)` before the copy. This tells Aspose
      to keep the cache but not the underlying source data.
    question: Can I copy only the pivot layout without the data?
  - answer: CSV doesn’t support pivots, but you can export the pivot’s *result* by
      calling `pivotTable.calculate()` and then saving the sheet as CSV.
    question: Is there a way to copy the pivot to a CSV file?
  - answer: Formatting lives in the style collection. After copying, you can call
      `destinationSheet.getCells().applyStyle(sourceSheet.getCells().getStyle())`
      to transfer styles.
    question: Why does the copied pivot lose its formatting?
  type: FAQPage
tags:
- Java
- Aspose.Cells
- Excel Automation
title: Criar Nova Pasta de Trabalho em Java – Guia Completo para Copiar Tabela Dinâmica
url: /pt/java/excel-pivot-tables/create-new-workbook-in-java-full-guide-to-copy-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar Nova Pasta de Trabalho em Java – Guia Completo para Copiar Tabela Dinâmica

Já se perguntou como **create new workbook** em Java enquanto preserva uma tabela dinâmica complexa? Você não é o único a ficar coçando a cabeça com isso. Em muitos aplicativos de relatórios você precisa mover uma tabela dinâmica de um arquivo de origem para uma nova pasta de trabalho, talvez para enviá‑la a um cliente ou para executar cálculos adicionais. A boa notícia? Com algumas linhas de código você pode fazer exatamente isso — sem necessidade de copiar‑colar manualmente.

Neste tutorial vamos percorrer todo o processo: carregar o arquivo de origem, definir o intervalo que contém a tabela dinâmica, **copying the Excel range**, criar uma **new workbook**, e finalmente **exporting the pivot table** para um novo arquivo. Ao final, você terá um programa Java autônomo e executável que responde à pergunta “**how to copy pivot**” sem adivinhações.

## Prerequisites

Antes de começarmos, certifique‑se de que você tem:

- Java 17 ou superior (o código funciona com qualquer JDK recente)
- Biblioteca Aspose.Cells for Java (versão de avaliação gratuita ou licenciada)
- Um exemplo `source.xlsx` que contém uma tabela dinâmica no intervalo `A1:G20`
- Uma IDE ou ferramenta de build (Maven/Gradle) para gerenciar o JAR do Aspose.Cells

Tem tudo isso? Ótimo — vamos começar.

## Step 1: Set Up the Project and Import Aspose.Cells

Primeiro de tudo, você precisa adicionar o Aspose.Cells ao seu projeto. Se você estiver usando Maven, insira esta dependência no seu `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.8</version> <!-- check for the latest version -->
</dependency>
```

Se preferir Gradle, o equivalente é:

```groovy
implementation 'com.aspose:aspose-cells:24.8'
```

Depois que a biblioteca estiver no classpath, importe as classes que você precisará:

```java
import com.aspose.cells.*;
import java.io.IOException;
```

> **Pro tip:** Aspose.Cells é uma biblioteca comercial, mas oferece uma avaliação totalmente funcional de 30 dias que adiciona uma marca d'água ao output — perfeito para testar isso.

## Step 2: Load the Source Workbook

Agora vamos **create new workbook** objetos, mas primeiro precisamos da origem que contém a tabela dinâmica. Esta etapa é a base para qualquer operação de **copy excel range**, pois o objeto de intervalo sabe exatamente quais células (incluindo o cache da tabela dinâmica) transferir.

```java
// Load the source workbook that contains the pivot table
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");

// Grab the first worksheet (index 0) – adjust if your pivot lives elsewhere
Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);
```

Por que não ler o intervalo diretamente? Porque os metadados da tabela dinâmica vivem no cache de pivô da planilha, e o Aspose.Cells agrupa isso automaticamente quando você copia o intervalo.

## Step 3: Define the Range That Holds the Pivot Table

Em muitos arquivos do mundo real a tabela dinâmica ocupa um bloco retangular. Para este exemplo, assumiremos que ela está em `A1:G20`. Você pode, claro, ajustar o endereço para corresponder ao seu layout real.

```java
// Define the exact area that includes the pivot table
Range sourceRange = sourceSheet.getCells().createRange("A1:G20");
```

Se não tiver certeza do endereço exato, pode usar `sourceSheet.getCells().getMaxDataRow()` e `getMaxDataColumn()` para calcular os limites dinamicamente. É um truque útil quando o tamanho da tabela dinâmica muda ao longo do tempo.

## Step 4: **Create New Workbook** and Destination Worksheet

Aqui está o momento em que realmente **create new workbook** que receberá o conteúdo copiado. Pense nisso como a tela em branco onde você colará a tabela dinâmica.

```java
// Create an empty workbook – this is our destination
Workbook destinationWorkbook = new Workbook();

// By default a new workbook comes with one worksheet
Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);
```

Por que começar com uma pasta de trabalho vazia? Isso garante que nenhum estilo oculto ou pivôs anteriores interfiram na cópia, proporcionando um resultado limpo pronto para **export pivot table**.

## Step 5: Copy the Pivot Table (and Its Underlying Range)

Agora o núcleo do tutorial: **copy pivot table**. O Aspose.Cells trata a cópia de um intervalo como uma cópia profunda, ou seja, o cache da tabela dinâmica viaja junto com as células. Por isso essa única linha faz o trabalho pesado.

```java
// Copy the defined range (including the pivot) to the destination sheet at A1
sourceRange.copy(destinationSheet.getCells().createRange("A1"));
```

Se você já se perguntou **how to copy pivot** sem perder sua funcionalidade, esta é a resposta. A planilha de destino agora contém uma tabela dinâmica totalmente funcional que você pode atualizar, modificar ou simplesmente exportar.

### Edge Case: Preserving Refresh Settings

Às vezes a tabela dinâmica de origem está configurada para atualizar ao abrir. Para manter esse comportamento, você pode copiar as opções da tabela dinâmica explicitamente:

```java
// Optional: retain the original pivot's refresh settings
PivotTable srcPivot = sourceSheet.getPivotTables().get(0);
PivotTable destPivot = destinationSheet.getPivotTables().get(0);
destPivot.setRefreshOnFileOpen(srcPivot.isRefreshOnFileOpen());
```

Esse trecho garante que a tabela dinâmica copiada se comporte exatamente como a original.

## Step 6: Save the Destination Workbook – **Export Pivot Table**

Finalmente, nós **export pivot table** salvando a nova pasta de trabalho no disco. Você pode escolher qualquer formato suportado pelo Aspose: XLSX, XLS, CSV, PDF, etc. Para este guia, vamos ficar com XLSX.

```java
// Save the workbook that now contains the copied pivot
destinationWorkbook.save("YOUR_DIRECTORY/copied_with_pivot.xlsx", SaveFormat.XLSX);
```

Se precisar enviar o arquivo por um serviço web, pode escrevê‑lo em um `ByteArrayOutputStream` em vez de um caminho de arquivo — o Aspose torna isso trivial.

## Full Working Example

Juntando tudo, aqui está um programa completo, pronto‑para‑executar. Sinta‑se à vontade para copiar, colar e executar no seu IDE.

```java
import com.aspose.cells.*;

public class CopyPivotExample {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);
        Range sourceRange = sourceSheet.getCells().createRange("A1:G20");

        // 2️⃣ Create a new workbook that will receive the copied range
        Workbook destinationWorkbook = new Workbook();
        Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);

        // 3️⃣ Copy the range (pivot table included) to the destination sheet
        sourceRange.copy(destinationSheet.getCells().createRange("A1"));

        // Optional: Preserve refresh settings if needed
        if (!sourceSheet.getPivotTables().isEmpty()) {
            PivotTable srcPivot = sourceSheet.getPivotTables().get(0);
            PivotTable destPivot = destinationSheet.getPivotTables().get(0);
            destPivot.setRefreshOnFileOpen(srcPivot.isRefreshOnFileOpen());
        }

        // 4️⃣ Save the result – this effectively **export pivot table**
        destinationWorkbook.save("YOUR_DIRECTORY/copied_with_pivot.xlsx", SaveFormat.XLSX);

        System.out.println("Pivot table copied successfully!");
    }
}
```

### Expected Output

Ao executar o programa, o console exibe:

```
Pivot table copied successfully!
```

E o arquivo `copied_with_pivot.xlsx` aparece em `YOUR_DIRECTORY`. Abra‑o no Excel e você verá a tabela dinâmica intacta, pronta para ser atualizada ou editada.

## Common Questions & Troubleshooting

- **What if the source pivot spans more than one worksheet?**  
  Você precisará copiar cada intervalo relevante separadamente, depois recriar a tabela dinâmica na planilha de destino usando as APIs `PivotTable`.

- **Can I copy only the pivot layout without the data?**  
  Defina `sourceRange.setCopyDataOnly(false)` antes da cópia. Isso indica ao Aspose para manter o cache, mas não os dados subjacentes.

- **Is there a way to copy the pivot to a CSV file?**  
  CSV não suporta tabelas dinâmicas, mas você pode exportar o *resultado* da tabela dinâmica chamando `pivotTable.calculate()` e então salvando a planilha como CSV.

- **Why does the copied pivot lose its formatting?**  
  A formatação vive na coleção de estilos. Após a cópia, você pode chamar `destinationSheet.getCells().applyStyle(sourceSheet.getCells().getStyle())` para transferir os estilos.

## Conclusion

Acabamos de mostrar como **create new workbook** em Java, **copy pivot table** e **export pivot table** — tudo com um exemplo de código limpo e reproduzível. Ao definir o exato **copy excel range**, aproveitar a semântica de cópia profunda do Aspose.Cells e preservar configurações opcionais, você pode automatizar praticamente qualquer tarefa de migração de tabelas dinâmicas.

Pronto para o próximo passo? Experimente mudar o formato de saída para PDF ou percorrer vários arquivos de origem para processar em lote dezenas de tabelas dinâmicas. O mesmo padrão se aplica — basta ajustar os caminhos de arquivo e os endereços dos intervalos.

Se encontrar algum problema, deixe um comentário abaixo ou consulte a documentação do Aspose.Cells para manipulação avançada de tabelas dinâmicas. Feliz codificação, e aproveite o tempo que você economizou ao automatizar essas tarefas tediosas de copiar‑colar!

## What Should You Learn Next?

Os tutoriais a seguir abordam tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Como Criar Tabelas Dinâmicas no Excel Usando Aspose.Cells para Java: Um Guia Abrangente](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Como Atualizar a Fonte da Tabela Dinâmica do Excel com Aspose.Cells para Java: Um Guia Abrangente](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Como Criar e Exportar Excel para HTML Usando Aspose.Cells Java | Guia de Operações de Pasta de Trabalho](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}