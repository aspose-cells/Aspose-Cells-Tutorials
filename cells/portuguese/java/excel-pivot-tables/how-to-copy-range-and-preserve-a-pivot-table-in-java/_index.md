---
category: general
date: 2026-09-21
description: Aprenda a copiar intervalos em Java preservando a tabela dinâmica. Este
  guia passo a passo mostra como exportar uma tabela dinâmica com segurança.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy range
- copy pivot table
- preserve pivot table
- export pivot table
- how to preserve pivot
language: pt
lastmod: 2026-09-21
og_description: Como copiar intervalo em Java preservando a tabela dinâmica. Siga
  este guia completo para exportar tabelas dinâmicas com segurança.
og_image_alt: Screenshot of Java code copying a range and preserving a pivot table
og_title: Como copiar intervalo e preservar uma tabela dinâmica em Java
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Learn how to copy range in Java while preserving the pivot table. This
    step‑by‑step guide shows you how to export a pivot table safely.
  headline: How to copy range and preserve a pivot table in Java
  type: TechArticle
- description: Learn how to copy range in Java while preserving the pivot table. This
    step‑by‑step guide shows you how to export a pivot table safely.
  name: How to copy range and preserve a pivot table in Java
  steps:
  - name: Load the source workbook
    text: '```java // Load the source workbook that contains the pivot table Workbook
      srcWb = new Workbook("YOUR_DIRECTORY/Source.xlsx"); Worksheet srcWs = srcWb.getWorksheets().get(0);
      ```'
  - name: Define the range that covers the pivot table
    text: '```java // Define the range covering the pivot table (including its data
      source) Range srcRange = srcWs.getCells().createRange("A1:G20"); ```'
  - name: Create an empty destination workbook
    text: '```java // Create a new, empty destination workbook Workbook destWb = new
      Workbook(); Worksheet destWs = destWb.getWorksheets().get(0); ```'
  - name: Copy the range – the pivot table is preserved
    text: '```java // Copy the defined range to the destination sheet – the pivot
      table is preserved destWs.getCells().copyRange(srcRange, new CellArea("A1",
      "G20")); ```'
  - name: Save the destination workbook
    text: '```java // Save the destination workbook with the copied pivot table destWb.save("YOUR_DIRECTORY/DestWithPivot.xlsx");
      ```'
  - name: Copy pivot table across different workbook versions
    text: Aspose.Cells supports older `.xls` files as well as the newer `.xlsx` format.
      The same code works regardless of the file extension, making it a universal
      solution for **how to preserve pivot** across versions.
  - name: Preserving pivot table when using a filtered source
    text: 'If the source pivot is filtered, the filter state is also copied. Should
      you need to reset filters in the destination, call `PivotTable.refreshData()`
      after copying:'
  - name: Export pivot table as a static snapshot
    text: Sometimes you may want a static copy (values only) rather than a live pivot.
      Replace `copyRange` with `copyRange` followed by `pt.setEnableRefresh(false)`
      to disable further calculations.
  - name: Handling large workbooks
    text: For workbooks with many worksheets, limit the copy operation to the specific
      sheet to reduce memory usage. Use `Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)`
      to fine‑tune performance.
  type: HowTo
tags:
- Java
- Aspose.Cells
- pivot table
- Excel automation
- range copy
title: Como copiar intervalo e preservar uma tabela dinâmica em Java
url: /pt/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como copiar intervalo e preservar uma tabela dinâmica em Java

Se você precisa **como copiar intervalo** que contém uma tabela dinâmica, este guia mostra uma maneira confiável de manter a pivot intacta. Muitos desenvolvedores enfrentam a perda da pivot ao exportar dados, mas a abordagem abaixo permite **copiar tabela dinâmica** sem quebrar sua funcionalidade. Ao final deste tutorial você será capaz de **preservar a estrutura da tabela dinâmica**, **exportar arquivos de tabela dinâmica** e entender **como preservar a pivot** em diferentes cenários.

O exemplo usa Aspose.Cells for Java, uma biblioteca popular para automação de Excel. Nenhuma ferramenta adicional é necessária além de um ambiente padrão de desenvolvimento Java.

## Pré-requisitos

Antes de começar, certifique‑se de que você tem:

* Java 17 (ou superior) instalado.
* Maven ou Gradle para gerenciar dependências.
* Aspose.Cells for Java (versão 23.9 ou mais recente). Adicione a seguinte dependência Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier>
</dependency>
```

* Uma pasta de trabalho fonte (`Source.xlsx`) que contém a tabela dinâmica que você deseja copiar.

## Como copiar intervalo e manter a tabela dinâmica intacta

A ideia central é copiar o **intervalo** que engloba toda a pivot — incluindo sua fonte de dados — usando `copyRange`. Esse método copia tanto os dados brutos quanto a definição da pivot, garantindo que a pasta de trabalho de destino receba uma pivot totalmente funcional.

### Etapa 1: Carregar a pasta de trabalho fonte

```java
// Load the source workbook that contains the pivot table
Workbook srcWb = new Workbook("YOUR_DIRECTORY/Source.xlsx");
Worksheet srcWs = srcWb.getWorksheets().get(0);
```

*Por que esta etapa?*  
Carregar a pasta de trabalho fornece acesso à planilha que hospeda a pivot. A classe `Workbook` abstrai todo o arquivo Excel, enquanto `Worksheet` oferece operações ao nível de célula.

### Etapa 2: Definir o intervalo que cobre a tabela dinâmica

```java
// Define the range covering the pivot table (including its data source)
Range srcRange = srcWs.getCells().createRange("A1:G20");
```

*Por que esta etapa?*  
Uma tabela dinâmica não é uma única célula; ela abrange um bloco que inclui cabeçalhos, linhas de dados e o cache da pivot. Ao especificar um intervalo que contém totalmente a pivot, você garante que `copyRange` também copie o cache subjacente, essencial para o comportamento de **preservar tabela dinâmica**.

### Etapa 3: Criar uma pasta de trabalho de destino vazia

```java
// Create a new, empty destination workbook
Workbook destWb = new Workbook();
Worksheet destWs = destWb.getWorksheets().get(0);
```

*Por que esta etapa?*  
Começar com uma pasta de trabalho limpa evita conflitos acidentais com planilhas ou intervalos nomeados existentes. A pasta de trabalho de destino receberá o intervalo copiado, efetivamente **exportando o conteúdo da tabela dinâmica**.

### Etapa 4: Copiar o intervalo – a tabela dinâmica é preservada

```java
// Copy the defined range to the destination sheet – the pivot table is preserved
destWs.getCells().copyRange(srcRange, new CellArea("A1", "G20"));
```

*Por que esta etapa?*  
`copyRange` realiza uma cópia profunda: valores das células, formatação e metadados da pivot são transferidos. Esta é a operação crítica que permite **copiar tabela dinâmica** sem perder sua funcionalidade. O objeto `CellArea` define onde o intervalo será colocado na planilha de destino.

### Etapa 5: Salvar a pasta de trabalho de destino

```java
// Save the destination workbook with the copied pivot table
destWb.save("YOUR_DIRECTORY/DestWithPivot.xlsx");
```

*Por que esta etapa?*  
Salvar finaliza o processo de **exportar tabela dinâmica**. O arquivo resultante (`DestWithPivot.xlsx`) contém uma pivot totalmente operacional que pode ser aberta no Excel, Google Sheets ou qualquer outro visualizador de planilhas.

## Verificando se a tabela dinâmica foi preservada

Abra `DestWithPivot.xlsx` no Excel e verifique o seguinte:

1. A tabela dinâmica aparece na mesma localização (A1:G20) da fonte.
2. Atualizar a pivot atualiza os dados corretamente, comprovando que o cache foi copiado.
3. Toda a formatação (largura das colunas, formatos numéricos) corresponde ao original.

Se alguma dessas verificações falhar, confirme que o intervalo fonte engloba totalmente a pivot e sua fonte de dados. Um erro comum é selecionar um intervalo que não inclui o cache de dados, o que gera uma pivot quebrada.

## Considerações adicionais

### Copiar tabela dinâmica entre diferentes versões de pasta de trabalho

Aspose.Cells suporta arquivos `.xls` antigos assim como o formato mais recente `.xlsx`. O mesmo código funciona independentemente da extensão do arquivo, tornando‑o uma solução universal para **como preservar a pivot** entre versões.

### Preservar a tabela dinâmica ao usar uma fonte filtrada

Se a pivot fonte estiver filtrada, o estado do filtro também é copiado. Caso precise redefinir filtros no destino, chame `PivotTable.refreshData()` após a cópia:

```java
PivotTable pt = destWs.getPivotTables().get(0);
pt.refreshData();   // Clears filters but keeps the pivot definition
```

### Exportar a tabela dinâmica como instantâneo estático

Às vezes você pode querer uma cópia estática (apenas valores) em vez de uma pivot ativa. Substitua `copyRange` por `copyRange` seguido de `pt.setEnableRefresh(false)` para desativar cálculos posteriores.

```java
destWs.getCells().copyRange(srcRange, new CellArea("A1", "G20"));
PivotTable pt = destWs.getPivotTables().get(0);
pt.setEnableRefresh(false); // Makes the pivot static
```

### Manipulando pastas de trabalho grandes

Para pastas de trabalho com muitas planilhas, limite a operação de cópia à planilha específica para reduzir o uso de memória. Use `Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` para ajustar o desempenho.

## Exemplo completo executável

Abaixo está o programa completo que você pode copiar, colar e executar. Ajuste os caminhos de arquivo para corresponder ao seu ambiente.

```java
import com.aspose.cells.*;

public class CopyPivotRange {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the source workbook that contains the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/Source.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Step 2: Define the range covering the pivot table (including its data source)
        // Adjust the range as needed to fully contain your pivot
        Range srcRange = srcWs.getCells().createRange("A1:G20");

        // Step 3: Create a new, empty destination workbook
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);

        // Step 4: Copy the defined range – the pivot table is preserved
        destWs.getCells().copyRange(srcRange, new CellArea("A1", "G20"));

        // Optional: If you need a static snapshot, disable refresh
        // PivotTable pt = destWs.getPivotTables().get(0);
        // pt.setEnableRefresh(false);

        // Step 5: Save the destination workbook with the copied pivot table
        destWb.save("YOUR_DIRECTORY/DestWithPivot.xlsx");

        System.out.println("Pivot table copied successfully. File saved as DestWithPivot.xlsx");
    }
}
```

**Saída esperada**

```
Pivot table copied successfully. File saved as DestWithPivot.xlsx
```

Ao abrir `DestWithPivot.xlsx`, você deverá ver a tabela dinâmica original totalmente funcional, confirmando que você conseguiu **como copiar intervalo** enquanto **preserva a tabela dinâmica**.

## Armadilhas comuns e dicas de especialista

| Problema | Por que acontece | Solução |
|----------|------------------|--------|
| A pivot aparece, mas mostra erros `#REF!` | O intervalo copiado omitiu a planilha de cache oculta | Expanda o intervalo fonte para incluir todo o cache (geralmente as linhas abaixo da pivot) |
| A pasta de trabalho de destino fica maior que o esperado | `copyRange` também copia formatação | Use `CopyOptions` para excluir formatação se o tamanho for um problema |
| A atualização falha com “Data source not found” | A pasta de trabalho fonte usava conexões de dados externas | Replique a conexão no destino ou copie primeiro a planilha de fonte de dados |

**Dica de especialista:** Sempre execute uma verificação rápida `destWs.getPivotTables().size()` após a cópia. Se o contador for zero, o intervalo não incluiu a definição da pivot e você precisará expandi‑lo.

## Conclusão

Neste tutorial demonstramos **como copiar intervalo** que contém uma tabela dinâmica e garantir que o comportamento de **preservar a tabela dinâmica** permaneça intacto. Ao carregar a pasta de trabalho fonte, definir um intervalo abrangente, usar `copyRange` e salvar o arquivo de destino, você pode exportar dados de tabela dinâmica de forma confiável e responder à pergunta **como preservar a pivot** em projetos Java.

Próximos passos que você pode explorar incluem:

* Automatizar a cópia para múltiplas planilhas (use a palavra‑chave secundária **copy pivot table** em um loop).
* Converter a pasta de trabalho exportada para CSV mantendo os dados brutos (ainda aplicando a lógica de **preservar tabela dinâmica** para a fonte).

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Copy Pivot Table in Java – Preserve It, Export to PPTX](/cells/english/java/excel-pivot-tables/copy-pivot-table-in-java-preserve-it-export-to-pptx/)
- [How to Update Excel Pivot Table Source with Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [How to Export Pivot Table as an Image in C# – Step‑by‑Step Guide](/cells/english/net/pivot-tables/how-to-export-pivot-table-as-an-image-in-c-step-by-step-guid/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}