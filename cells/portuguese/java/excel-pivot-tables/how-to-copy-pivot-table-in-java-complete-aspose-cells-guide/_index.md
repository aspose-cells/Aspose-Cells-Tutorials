---
category: general
date: 2026-06-08
description: Como copiar tabela dinâmica usando Aspose.Cells em Java. Aprenda a copiar
  intervalos entre pastas de trabalho e preservar tabelas dinâmicas sem esforço.
draft: false
keywords:
- how to copy pivot table
- copy range between workbooks
- how to preserve pivot
- copy pivot table to new workbook
- copy excel sheet with pivot
language: pt
og_description: Como copiar tabela dinâmica em Java com Aspose.Cells. Este tutorial
  mostra como copiar intervalo entre pastas de trabalho e manter a tabela dinâmica
  intacta.
og_title: Como copiar uma Tabela Dinâmica em Java – Guia passo a passo
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: How to copy pivot table using Aspose.Cells in Java. Learn to copy range
    between workbooks and preserve pivot tables effortlessly.
  headline: How to Copy Pivot Table in Java – Complete Aspose.Cells Guide
  type: TechArticle
- description: How to copy pivot table using Aspose.Cells in Java. Learn to copy range
    between workbooks and preserve pivot tables effortlessly.
  name: How to Copy Pivot Table in Java – Complete Aspose.Cells Guide
  steps:
  - name: Set Up Aspose.Cells in Your Project
    text: 'Before you can manipulate Excel files, you need the Aspose.Cells library
      on your classpath. If you use Maven, add the following dependency to your `pom.xml`:'
  - name: Load the Source Workbook
    text: We need a `Workbook` instance that points at the file housing the pivot.
      Replace `YOUR_DIRECTORY/src.xlsx` with the actual path on your machine.
  - name: Define the Pivot’s Enclosing Range
    text: A pivot table lives inside a rectangular block of cells. You can locate
      it manually (e.g., `A1:G20`) or programmatically by inspecting the worksheet’s
      `PivotTables` collection. For this tutorial we’ll hard‑code the range for clarity.
  - name: Create a Blank Destination Workbook
    text: Now we spin up an empty workbook that will receive the copied data.
  - name: Copy the Range and Preserve the Pivot
    text: Here’s where the magic happens. The `copyRange` method accepts a `CopyOptions`
      object, but we don’t need to tweak anything—pivot preservation is enabled out
      of the box.
  - name: Save the Destination Workbook
    text: Finally, write the new file to disk.
  type: HowTo
- questions:
  - answer: Yes. Because we’re copying the entire cell range, styles, conditional
      formatting, and number formats travel with the data.
    question: Does this method also copy the pivot’s formatting?
  - answer: Simply change the third argument of `copyRange` to the desired top‑left
      address, e.g., `"B5"`.
    question: What if I need to copy the pivot to a specific cell other than `A1`?
  - answer: 'Not directly. The pivot cache lives inside the workbook; removing the
      source data will render the pivot unusable. Export the source data to a hidden
      sheet if you want a lightweight copy. --- ## Conclusion You now have a clear,
      end‑to‑end answer to **how to copy pivot table** in Java using Aspose.Cel'
    question: Can I copy a pivot without its source data?
  type: FAQPage
tags:
- Aspose.Cells
- Java
- Excel
- PivotTable
title: Como Copiar Tabela Dinâmica em Java – Guia Completo do Aspose.Cells
url: /pt/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-complete-aspose-cells-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Copiar Tabela Dinâmica em Java – Guia Completo do Aspose.Cells

Já se perguntou **como copiar uma tabela dinâmica** de uma pasta de trabalho Excel para outra usando Java? A boa notícia é que o Aspose.Cells facilita **copiar intervalo entre pastas de trabalho** preservando todos os detalhes da tabela dinâmica.  

Neste tutorial vamos percorrer um exemplo real que não apenas copia a própria tabela dinâmica, mas também mantém os dados subjacentes, a formatação e as fórmulas intactas. Ao final, você saberá exatamente **como preservar a tabela dinâmica**, como mover uma tabela dinâmica para uma nova pasta de trabalho e como evitar armadilhas comuns que atrapalham muitos desenvolvedores.

Vamos cobrir:

* Os pré‑requisitos mínimos (Java 17+, Aspose.Cells for Java 23.9+).  
* Um passo‑a‑passo detalhado do código, com explicações do **porquê** de cada linha.  
* Tratamento de casos extremos para intervalos de tabela dinâmica grandes e fontes de dados externas.  
* Um programa completo, executável, que você pode inserir no seu IDE e rodar hoje.

> **Dica profissional:** Se você já usa Maven ou Gradle, adicionar o Aspose.Cells como dependência é uma única linha—sem necessidade de lidar manualmente com JARs.

---

## Como Copiar Tabela Dinâmica – Visão Geral Passo a Passo

A seguir, uma visão de alto nível do que vamos alcançar:

1. Carregar a pasta de trabalho de origem que contém a tabela dinâmica.  
2. Identificar o intervalo exato de células que envolve a tabela dinâmica.  
3. Criar uma nova pasta de trabalho de destino.  
4. **Copiar o intervalo** para a nova planilha, permitindo que o Aspose.Cells preserve automaticamente a tabela dinâmica.  
5. Salvar o resultado como um novo arquivo.

Cada passo é ilustrado com trechos de código e uma breve justificativa, para que você compreenda a mecânica—not just the mechanics.

![Diagrama ilustrando como uma tabela dinâmica é copiada de uma pasta de trabalho de origem para uma pasta de trabalho de destino enquanto preserva sua estrutura](/images/how-to-copy-pivot-table-diagram.png){: .align-center alt="diagrama de como copiar tabela dinâmica"}

---

### Passo 1: Configurar o Aspose.Cells no Seu Projeto

Antes de manipular arquivos Excel, você precisa da biblioteca Aspose.Cells no classpath. Se usar Maven, adicione a seguinte dependência ao seu `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier>
</dependency>
```

Para Gradle, também é uma linha única:

```gradle
implementation 'com.aspose:aspose-cells:23.9:jdk17'
```

*Por que isso importa:* O Aspose.Cells abstrai os detalhes de baixo nível do OpenXML, oferecendo uma API simples para **copiar tabela dinâmica para nova pasta de trabalho** sem perder nenhum metadado.

---

### Passo 2: Carregar a Pasta de Trabalho de Origem

Precisamos de uma instância `Workbook` que aponte para o arquivo que contém a tabela dinâmica. Substitua `YOUR_DIRECTORY/src.xlsx` pelo caminho real na sua máquina.

```java
// Load the source workbook that contains the pivot table
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/src.xlsx");
```

> **Observação:** O Aspose.Cells detecta automaticamente o formato do arquivo (XLSX, XLS, CSV, etc.), então você não precisa se preocupar com conversão de formato.

---

### Passo 3: Definir o Intervalo que Envolve a Tabela Dinâmica

Uma tabela dinâmica vive dentro de um bloco retangular de células. Você pode localizá‑la manualmente (por exemplo, `A1:G20`) ou programaticamente inspecionando a coleção `PivotTables` da planilha. Para este tutorial, vamos codificar o intervalo para clareza.

```java
// Define the range that encloses the pivot table (e.g., A1:G20)
Range pivotRange = sourceWorkbook.getWorksheets().get(0)
                                 .getCells()
                                 .createRange("A1:G20");
```

*Por que usamos `createRange`*: Ele cria um objeto `Range` leve que pode ser passado para `copyRange`. Esta é a forma mais confiável de **copiar intervalo entre pastas de trabalho** garantindo que as estruturas internas da tabela dinâmica sejam incluídas.

---

### Passo 4: Criar uma Pasta de Trabalho de Destino em Branco

Agora criamos uma pasta de trabalho vazia que receberá os dados copiados.

```java
// Create a new (blank) destination workbook
Workbook destinationWorkbook = new Workbook(); // defaults to a single empty sheet
Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);
```

A pasta de trabalho padrão já contém uma planilha, o que é perfeito para nosso propósito. Se precisar de um nome de planilha específico, você pode renomeá‑la:

```java
destinationSheet.setName("PivotCopy");
```

---

### Passo 5: Copiar o Intervalo e Preservar a Tabela Dinâmica

Aqui é onde a mágica acontece. O método `copyRange` aceita um objeto `CopyOptions`, mas não precisamos ajustar nada— a preservação da tabela dinâmica já vem habilitada por padrão.

```java
// Copy the range to the destination sheet; the pivot table is preserved automatically
destinationSheet.getCells().copyRange(pivotRange, new CopyOptions() {{
    // No additional settings are required – pivot preservation is enabled by default
}}, "A1");
```

*Por que isso funciona:* O Aspose.Cells trata a tabela dinâmica como parte da coleção de células. Quando você invoca `copyRange`, ele replica o cache interno da tabela dinâmica, os campos de dados e o layout, efetivamente **como preservar a tabela dinâmica** sem código adicional.

---

### Passo 6: Salvar a Pasta de Trabalho de Destino

Por fim, grave o novo arquivo no disco.

```java
// Save the destination workbook with the copied pivot table
destinationWorkbook.save("YOUR_DIRECTORY/copied-with-pivot.xlsx");
```

Abra o `copied-with-pivot.xlsx` resultante no Excel e você verá uma réplica exata da tabela dinâmica original, pronta para análises adicionais.

---

## Exemplo Completo Funcionando

A seguir está o programa completo que você pode compilar e executar diretamente. Ele reúne todos os trechos acima, adiciona algumas verificações defensivas e imprime uma mensagem de confirmação amigável.

```java
import com.aspose.cells.*;

public class CopyPivotRange {
    public static void main(String[] args) throws Exception {
        // ---------- 1. Load source workbook ----------
        String srcPath = "YOUR_DIRECTORY/src.xlsx";
        Workbook sourceWorkbook = new Workbook(srcPath);

        // ---------- 2. Identify pivot range ----------
        // You may replace the hard‑coded range with a dynamic lookup if needed.
        Range pivotRange = sourceWorkbook.getWorksheets().get(0)
                                         .getCells()
                                         .createRange("A1:G20");

        // ---------- 3. Create destination workbook ----------
        Workbook destinationWorkbook = new Workbook(); // empty workbook
        Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);
        destinationSheet.setName("PivotCopy");

        // ---------- 4. Copy range (pivot preserved) ----------
        destinationSheet.getCells().copyRange(pivotRange,
                new CopyOptions() {{
                    // No extra options required for pivot preservation.
                }}, "A1");

        // ---------- 5. Save result ----------
        String destPath = "YOUR_DIRECTORY/copied-with-pivot.xlsx";
        destinationWorkbook.save(destPath);

        System.out.println("Pivot table successfully copied!");
        System.out.println("Source:  " + srcPath);
        System.out.println("Destination: " + destPath);
    }
}
```

**Saída esperada ao executar o programa**:

```
Pivot table successfully copied!
Source:  YOUR_DIRECTORY/src.xlsx
Destination: YOUR_DIRECTORY/copied-with-pivot.xlsx
```

Abra o arquivo de destino—sua tabela dinâmica deve estar idêntica à original, completa com segmentações, filtros e campos calculados.

---

## Tratamento de Casos de Borda Comuns

| Situação | O que observar | Solução sugerida |
|-----------|-------------------|---------------|
| **Tabela dinâmica usa fonte de dados externa** (ex.: banco de dados) | A conexão externa não está incorporada na pasta de trabalho, então a cópia pode quebrar o link. | Exporte os dados para uma planilha primeiro, então crie a tabela dinâmica nessa planilha antes de copiar. |
| **Tabela dinâmica muito grande (milhares de linhas)** | `copyRange` pode consumir muita memória. | Aumente o heap da JVM (`-Xmx2g`) ou copie a tabela em blocos menores usando `copyRows`/`copyColumns`. |
| **Múltiplas tabelas dinâmicas na mesma planilha** | Codificar `A1:G20` copia apenas a primeira tabela dinâmica. | Percorra `sourceWorksheet.getPivotTables()` e copie cada `PivotTable.getDataRange()`. |
| **Pasta de trabalho de destino já contém uma planilha com o mesmo nome** | `setName` lançará uma exceção. | Use `Workbook.getWorksheets().add("PivotCopy")` para criar uma planilha com nome exclusivo. |

Essas dicas garantem que **como copiar tabela dinâmica** funcione de forma confiável, mesmo em cenários de produção.

---

## Perguntas Frequentes

**P: Este método também copia a formatação da tabela dinâmica?**  
R: Sim. Como estamos copiando todo o intervalo de células, estilos, formatação condicional e formatos numéricos são transferidos junto.

**P: E se eu precisar copiar a tabela dinâmica para uma célula específica diferente de `A1`?**  
R: Basta alterar o terceiro argumento de `copyRange` para o endereço desejado, por exemplo, `"B5"`.

**P: Posso copiar a tabela dinâmica sem seus dados de origem?**  
R: Não diretamente. O cache da tabela dinâmica reside dentro da pasta de trabalho; remover os dados de origem tornará a tabela inutilizável. Exporte os dados de origem para uma planilha oculta se quiser uma cópia mais leve.

---

## Conclusão

Agora você tem uma resposta clara e de ponta a ponta para **como copiar tabela dinâmica** em Java usando Aspose.Cells. Ao carregar a pasta de trabalho de origem, definir o intervalo da tabela dinâmica e usar `copyRange`, você pode facilmente **copiar intervalo entre pastas de trabalho** garantindo que a tabela dinâmica permaneça intacta.

## O Que Você Deve Aprender a Seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que expandem as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [How to Update Excel Pivot Table Source with Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [How to Create Pivot Tables in Excel Using Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [How to Implement Slicers in Pivot Tables Using Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/implement-slicers-pivot-tables-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}