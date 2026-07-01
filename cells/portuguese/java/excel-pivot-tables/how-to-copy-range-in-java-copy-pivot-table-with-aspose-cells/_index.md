---
category: general
date: 2026-06-30
description: Como copiar intervalo em Java usando Aspose.Cells – duplicar intervalo
  do Excel, copiar tabela dinâmica e carregar a pasta de trabalho do Excel de forma
  eficiente.
draft: false
keywords:
- how to copy range
- copy pivot table
- pivot table to sheet
- duplicate excel range
- load excel workbook
language: pt
og_description: Como copiar intervalo em Java com Aspose.Cells. Aprenda a duplicar
  intervalo do Excel, copiar tabela dinâmica e carregar a pasta de trabalho do Excel
  em minutos.
og_title: Como copiar intervalo em Java – Guia passo a passo
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: How to copy range in Java using Aspose.Cells – duplicate Excel range,
    copy pivot table, and load Excel workbook efficiently.
  headline: How to copy range in Java – Copy Pivot Table with Aspose.Cells
  type: TechArticle
- description: How to copy range in Java using Aspose.Cells – duplicate Excel range,
    copy pivot table, and load Excel workbook efficiently.
  name: How to copy range in Java – Copy Pivot Table with Aspose.Cells
  steps:
  - name: Expected Output
    text: 'When you execute `CopyPivotDemo`, the console prints:'
  - name: What if the source workbook has multiple worksheets?
    text: You can loop through `sourceWorkbook.getWorksheets()` and copy each relevant
      range. Just be careful to maintain the same sheet names in the destination if
      you need to preserve references.
  - name: Does the copied pivot retain its data source?
    text: Yes. Aspose.Cells copies the pivot cache along with the range, so the destination
      workbook still points to the original data source within the same file. If you
      later move the data to a different sheet, you may need to refresh the pivot
      manually.
  - name: How to copy a pivot that uses an external data source?
    text: When the pivot’s data source is an external file, you’ll have to embed that
      data into the destination workbook first (e.g., copy the source data range)
      before copying the pivot. Otherwise the pivot will show “#REF!” errors.
  - name: Can I copy the pivot without the surrounding data?
    text: Absolutely. Just adjust `pivotRange` to cover only the pivot’s cells (usually
      the top‑left corner plus the data area). You can also use `sourceSheet.getPivotTables().get(0).getPivotTableArea()`
      to retrieve the exact range programmatically.
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel Automation
title: Como copiar intervalo em Java – Copiar Tabela Dinâmica com Aspose.Cells
url: /pt/java/excel-pivot-tables/how-to-copy-range-in-java-copy-pivot-table-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como copiar intervalo em Java – Copiar Tabela Dinâmica com Aspose.Cells

Já se perguntou **como copiar intervalo** de uma pasta de trabalho Excel para outra sem perder a integridade da tabela dinâmica? Você não está sozinho. Em muitos pipelines de relatórios, a necessidade de *duplicar intervalo Excel* preservando a lógica da tabela dinâmica é uma dor de cabeça diária. Felizmente, o Aspose.Cells para Java torna isso simples, e neste tutorial vamos percorrer um exemplo completo e executável que também mostra como **carregar pasta de trabalho Excel**, copiar uma tabela dinâmica e salvar o resultado.

Ao final deste guia você terá um programa Java autônomo que:

* Carrega uma pasta de trabalho existente (`load excel workbook`);
* Define as células exatas que contêm a tabela dinâmica;
* Copia essa **tabela dinâmica para planilha** em uma nova pasta de trabalho;
* Salva o novo arquivo, pronto para processamento posterior.

Sem scripts externos, sem etapas manuais — apenas código puro.

## O que você precisará

Antes de mergulharmos, certifique‑se de que você tem:

* Java 8 ou superior (o código também funciona com Java 11+);
* Biblioteca Aspose.Cells para Java (você pode obtê‑la no Maven Central);
* Dois arquivos Excel de exemplo – um fonte com uma tabela dinâmica (`source.xlsx`) e uma pasta de destino onde você escreverá `copy-pivot.xlsx`.

É só isso. Não são necessários truques de IDE sofisticados; qualquer editor de texto mais `javac` serve.

## Etapa 1: Configurar o projeto e importar Aspose.Cells

Primeiro de tudo — vamos colocar a biblioteca no projeto. Se você usa Maven, adicione esta dependência ao seu `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- check for the latest version -->
</dependency>
```

Se não estiver usando Maven, faça o download do JAR no site da Aspose e adicione‑o ao seu classpath. Depois de resolvido isso, crie uma nova classe Java chamada `CopyPivotDemo`.

```java
package com.example.excel;

import com.aspose.cells.*;

public class CopyPivotDemo {
    public static void main(String[] args) throws Exception {
        // The implementation will go here.
    }
}
```

> **Dica profissional:** Mantenha sua pasta `src/main/java` organizada e dê à classe um nome significativo; isso facilita a manutenção futura.

## Etapa 2: Carregar a pasta de trabalho fonte (`load excel workbook`)

Agora vamos realmente **load excel workbook** que contém a tabela dinâmica que queremos copiar. O construtor `Workbook` recebe um caminho de arquivo, então verifique se o caminho está correto.

```java
// Step 2: Load the source workbook
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");

// Grab the first worksheet (index 0)
Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);
```

Por que escolhemos a primeira planilha? Na maioria dos casos simples a tabela dinâmica está na primeira aba, mas você pode mudar o índice ou usar o nome da planilha, se necessário. Essa flexibilidade é um dos motivos pelos quais o Aspose.Cells se destaca.

## Etapa 3: Definir o intervalo que contém a tabela dinâmica

Uma tabela dinâmica geralmente abrange um bloco de células. Vamos supor que ela ocupe `A1:G20`. Você pode ajustar o endereço para corresponder aos seus dados reais.

```java
// Step 3: Define the range that includes the pivot table
Range pivotRange = sourceSheet.getCells().createRange("A1:G20");
```

Se não tiver certeza do endereço exato, abra a pasta de trabalho no Excel, selecione toda a tabela dinâmica e olhe na caixa de nome. Lembre‑se, **duplicate excel range** funciona melhor quando você aponta exatamente para a área — sem linhas extras, sem colunas faltando.

## Etapa 4: Criar uma nova pasta de trabalho para o destino

Precisamos de uma pasta de trabalho nova que receberá o intervalo copiado. É aqui que **copy pivot table** será enviado para uma nova planilha.

```java
// Step 4: Create a new workbook to receive the copied range
Workbook destinationWorkbook = new Workbook(); // starts with a default empty sheet
Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);
```

Neste ponto a pasta de trabalho de destino está vazia, mas o Aspose.Cells adiciona automaticamente uma planilha padrão, que usaremos como alvo.

## Etapa 5: Copiar o intervalo – Tabela Dinâmica permanece intacta

Aqui está a linha mágica que **copy pivot table** mantendo todas as conexões internas vivas.

```java
// Step 5: Copy the range (pivot table stays intact) to the destination sheet
destinationSheet.getCells().copy(pivotRange,
        destinationSheet.getCells().createRange("A1"));
```

O método `copy` recebe dois argumentos: o `Range` de origem e o `Range` de destino. Ao iniciar o destino em `A1`, colocamos a tabela dinâmica exatamente onde estava na fonte. O Aspose.Cells copia o cache subjacente da tabela dinâmica, de modo que a nova pasta de trabalho ainda sabe como atualizar a tabela.

## Etapa 6: Salvar a pasta de trabalho resultante

Por fim, grave o novo arquivo no disco. Você pode escolher qualquer formato suportado pelo Aspose (`.xlsx`, `.xls`, `.csv`, etc.). Vamos ficar com `.xlsx`.

```java
// Step 6: Save the resulting workbook
destinationWorkbook.save("YOUR_DIRECTORY/copy-pivot.xlsx");
System.out.println("Pivot table successfully copied to copy-pivot.xlsx");
```

Execute o programa e você deverá ver uma nova pasta de trabalho com o mesmo layout da tabela dinâmica. Abra‑a no Excel — se tudo correu bem, você poderá atualizar a tabela dinâmica sem erros.

### Saída esperada

Ao executar `CopyPivotDemo`, o console exibe:

```
Pivot table successfully copied to copy-pivot.xlsx
```

Abrindo `copy-pivot.xlsx` revela uma planilha que parece idêntica à área da tabela dinâmica da fonte, e a **pivot table to sheet** funciona exatamente como a original.

## Exemplo completo em funcionamento

Abaixo está a classe Java completa, pronta para ser executada, que reúne todas as etapas. Copie‑e‑cole no seu IDE, ajuste os caminhos dos arquivos e execute.

```java
package com.example.excel;

import com.aspose.cells.*;

public class CopyPivotDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook (load excel workbook)
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);

        // 2️⃣ Define the range that contains the pivot table
        // Adjust the address if your pivot occupies a different area
        Range pivotRange = sourceSheet.getCells().createRange("A1:G20");

        // 3️⃣ Create a fresh workbook for the destination
        Workbook destinationWorkbook = new Workbook(); // empty workbook
        Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);

        // 4️⃣ Copy the range – the pivot table stays intact
        destinationSheet.getCells().copy(pivotRange,
                destinationSheet.getCells().createRange("A1"));

        // 5️⃣ Save the new workbook
        destinationWorkbook.save("YOUR_DIRECTORY/copy-pivot.xlsx");

        System.out.println("Pivot table successfully copied to copy-pivot.xlsx");
    }
}
```

> **Observação:** Se sua tabela dinâmica se estender por mais de uma planilha, repita a etapa de cópia para cada planilha relevante, ou use `Workbook.copy` para clonar planilhas inteiras.

## Perguntas frequentes e casos de borda

### E se a pasta de trabalho fonte tiver várias planilhas?

Você pode percorrer `sourceWorkbook.getWorksheets()` e copiar cada intervalo relevante. Apenas tome cuidado para manter os mesmos nomes de planilha no destino, se precisar preservar referências.

### A tabela dinâmica copiada mantém sua fonte de dados?

Sim. O Aspose.Cells copia o cache da tabela dinâmica junto com o intervalo, de modo que a pasta de trabalho de destino ainda aponta para a fonte de dados original dentro do mesmo arquivo. Se você mover os dados para outra planilha depois, talvez seja necessário atualizar a tabela manualmente.

### Como copiar uma tabela dinâmica que usa fonte de dados externa?

Quando a fonte de dados da tabela dinâmica é um arquivo externo, você precisará incorporar esses dados na pasta de trabalho de destino primeiro (por exemplo, copiar o intervalo de dados fonte) antes de copiar a tabela dinâmica. Caso contrário, a tabela mostrará erros “#REF!”.

### Posso copiar a tabela dinâmica sem os dados ao redor?

Com certeza. Basta ajustar `pivotRange` para cobrir apenas as células da tabela dinâmica (geralmente o canto superior‑esquerdo mais a área de dados). Você também pode usar `sourceSheet.getPivotTables().get(0).getPivotTableArea()` para obter o intervalo exato programaticamente.

## Dicas para projetos reais

* **Processamento em lote:** Se precisar duplicar dezenas de pastas de trabalho, encapsule o código acima em um método e chame‑o dentro de um loop que itere sobre um diretório.
* **Desempenho:** Para arquivos grandes, reutilize uma única instância de `Workbook` e chame `Workbook.calculateFormula()` somente após todas as cópias concluírem.
* **Tratamento de erros:** Envolva a lógica de cópia em blocos try‑catch e registre `Exception.getMessage()`; o Aspose lança `CellsException` para intervalos inválidos.

## Conclusão

Acabamos de cobrir **how to copy range** em Java usando Aspose.Cells, mostrando como **duplicate excel range**, **copy pivot table** e **load excel workbook** tudo em um programa organizado. As etapas são diretas, o código é totalmente executável, e a abordagem escala de uma demonstração de uma única planilha a trabalhos em lote de nível empresarial.

Pronto para o próximo desafio? Tente exportar a tabela dinâmica copiada para PDF, ou atualizá‑la programaticamente após adicionar novos dados. Ambas as tarefas se baseiam na mesma fundação que apresentamos aqui, então você estará bem preparado para enfrentá‑las.

Tem dúvidas ou quer compartilhar suas próprias adaptações? Deixe um comentário abaixo — feliz codificação! 

![Diagram illustrating how a range with a pivot table is copied from one workbook to another](https://example.com/images/how-to-copy-range-diagram.png "how to copy range diagram")


## O que você deve aprender a seguir?


Os tutoriais a seguir abordam tópicos estreitamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [How to Implement a Named Range with Workbook Scope in Aspose.Cells Java for Enhanced Excel Data Management](/cells/english/java/tables-structured-references/implement-named-range-workbook-scope-aspose-cells-java/)
- [How to Copy Multiple Columns in Excel Using Aspose.Cells Java: A Complete Guide](/cells/english/java/range-management/copy-multiple-columns-excel-aspose-cells-java/)
- [Excel Aspose Cells Dotnet Copy Range Data](/cells/hindi/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}