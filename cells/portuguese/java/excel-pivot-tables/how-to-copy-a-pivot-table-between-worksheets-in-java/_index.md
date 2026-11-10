---
category: general
date: 2026-10-16
description: Como copiar tabela dinâmica em Java com Aspose.Cells – aprenda a copiar
  intervalo para outra planilha e copiar intervalo entre planilhas de forma eficiente.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy range to another sheet
- copy range between worksheets
language: pt
lastmod: 2026-10-16
og_description: Como copiar tabela dinâmica em Java usando Aspose.Cells. Este tutorial
  mostra como copiar um intervalo para outra planilha e copiar intervalo entre planilhas
  com código completo.
og_image_alt: Diagram illustrating how to copy pivot table from one worksheet to another
  in Java
og_title: Como copiar uma tabela dinâmica entre planilhas em Java – guia passo a passo
schemas:
- author: Aspose
  dateModified: '2026-10-16'
  description: How to copy pivot table in Java with Aspose.Cells – learn to copy range
    to another sheet and copy range between worksheets efficiently.
  headline: How to copy a pivot table between worksheets in Java
  type: TechArticle
- description: How to copy pivot table in Java with Aspose.Cells – learn to copy range
    to another sheet and copy range between worksheets efficiently.
  name: How to copy a pivot table between worksheets in Java
  steps:
  - name: Load the workbook
    text: '```java import com.aspose.cells.*;'
  - name: Locate the source range that contains the pivot table
    text: '```java // The first worksheet (index 0) holds the pivot table. Worksheet
      sourceSheet = workbook.getWorksheets().get(0);'
  - name: Define the destination range on another sheet
    text: '```java // The second worksheet (index 1) will receive the copied pivot
      table. Worksheet destSheet = workbook.getWorksheets().get(1);'
  - name: Copy the source range while preserving the pivot table
    text: '```java // Configure copy options to keep all formatting, formulas, and
      pivot data. CopyOptions copyOptions = new CopyOptions(); copyOptions.setPasteType(PasteType.PASTE_ALL);
      // copies everything copyOptions.setSkipEmptyRows(false); copyOptions.setSkipEmptyColumns(false);'
  - name: Save the workbook and verify the result
    text: '```java // Save the modified workbook to a new file. workbook.save("output.xlsx");
      System.out.println("Pivot table copied successfully."); } } ```'
  type: HowTo
tags:
- Aspose.Cells
- Java
- PivotTable
- Excel automation
title: Como copiar uma tabela dinâmica entre planilhas em Java
url: /pt/java/excel-pivot-tables/how-to-copy-a-pivot-table-between-worksheets-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como copiar uma tabela dinâmica entre planilhas em Java

Se você precisa **como copiar tabela dinâmica** de uma planilha para outra na mesma pasta de trabalho, este guia fornece uma solução completa, pronta‑para‑executar. Você verá como copiar o intervalo de origem que contém a tabela dinâmica, preservar sua funcionalidade e verificar o resultado — tudo usando Aspose.Cells for Java.

Copiar uma tabela dinâmica é uma tarefa comum ao gerar relatórios programaticamente, e fazê‑lo corretamente evita a perda do cache da tabela dinâmica ou a quebra de fórmulas. Ao final deste tutorial, você será capaz de **copiar intervalo para outra planilha** e **copiar intervalo entre planilhas** sem quaisquer etapas manuais.

## O que você aprenderá

* Carregar um arquivo Excel existente com uma tabela dinâmica.
* Definir o intervalo de origem que contém a tabela dinâmica.
* Definir um intervalo de destino em outra planilha.
* Usar `CopyOptions` para manter a tabela dinâmica intacta.
* Verificar se a tabela dinâmica copiada funciona como esperado.

**Pré-requisitos**

* Java 17 ou posterior.
* Aspose.Cells for Java (versão 23.12 ou mais recente).  
* Um arquivo Excel (`input.xlsx`) que contém uma tabela dinâmica na primeira planilha.

---

## Como copiar tabela dinâmica com Aspose.Cells

O núcleo da operação é um processo de quatro etapas: carregar a pasta de trabalho, localizar o intervalo de origem, definir o intervalo de destino e executar a cópia. A seguir, cada etapa é explicada em detalhes.

### Etapa 1: Carregar a pasta de trabalho

```java
import com.aspose.cells.*;

public class CopyPivotTableExample {
    public static void main(String[] args) throws Exception {
        // Load the workbook that contains the original pivot table
        Workbook workbook = new Workbook("input.xlsx");
```

*Por que esta etapa?*  
Carregar a pasta de trabalho traz todo o arquivo para a memória, proporcionando acesso às planilhas, células e ao cache da tabela dinâmica. Aspose.Cells lê o formato do arquivo automaticamente, portanto você não precisa se preocupar com `.xls` vs `.xlsx`.

### Etapa 2: Localizar o intervalo de origem que contém a tabela dinâmica

```java
        // The first worksheet (index 0) holds the pivot table.
        Worksheet sourceSheet = workbook.getWorksheets().get(0);

        // Define the exact area that includes the pivot table.
        // Adjust the address if your pivot table spans a different range.
        Range sourceRange = sourceSheet.getCells().createRange("A1:G20");
```

*Por que esta etapa?*  
Uma tabela dinâmica é armazenada em um bloco de células que também referencia um cache oculto. Ao selecionar o intervalo exato (`A1:G20` neste exemplo), você garante que o cache permaneça vinculado quando o intervalo for copiado.

### Etapa 3: Definir o intervalo de destino em outra planilha

```java
        // The second worksheet (index 1) will receive the copied pivot table.
        Worksheet destSheet = workbook.getWorksheets().get(1);

        // Destination starts at cell A1 of the second sheet.
        Range destRange = destSheet.getCells().createRange("A1");
```

*Por que esta etapa?*  
Escolher um destino em outra planilha permite que você **copie intervalo para outra planilha**. A célula superior‑esquerda (`A1`) é um ponto de partida comum, mas você pode posicioná‑la em qualquer lugar alterando o endereço.

### Etapa 4: Copiar o intervalo de origem preservando a tabela dinâmica

```java
        // Configure copy options to keep all formatting, formulas, and pivot data.
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.PASTE_ALL); // copies everything
        copyOptions.setSkipEmptyRows(false);
        copyOptions.setSkipEmptyColumns(false);

        // Perform the copy operation.
        sourceRange.copy(destRange, copyOptions);
```

*Por que esta etapa?*  
`CopyOptions` controla o que é transferido. Usar `PasteType.PASTE_ALL` garante que a tabela dinâmica, sua formatação e as fórmulas subjacentes sejam duplicadas. Sem essas opções, apenas valores brutos podem ser copiados, quebrando a funcionalidade da tabela dinâmica.

### Etapa 5: Salvar a pasta de trabalho e verificar o resultado

```java
        // Save the modified workbook to a new file.
        workbook.save("output.xlsx");
        System.out.println("Pivot table copied successfully.");
    }
}
```

Abra `output.xlsx` no Excel e confirme que:

* A segunda planilha contém uma tabela dinâmica totalmente funcional, idêntica à original.
* Atualizar a tabela dinâmica atualiza os dados, comprovando que o cache está intacto.

---

## Copiar intervalo para outra planilha usando Java

Se o seu objetivo é simplesmente **copiar intervalo para outra planilha** sem uma tabela dinâmica, o mesmo código funciona com um intervalo de células regular. A única mudança é o endereço de origem. A configuração de `CopyOptions` permanece a mesma, garantindo que fórmulas e formatação sejam preservadas.

```java
// Example: copy a plain data table from Sheet1!B2:D10 to Sheet3!A1
Range plainSource = workbook.getWorksheets().get(0)
                            .getCells().createRange("B2:D10");
Range plainDest = workbook.getWorksheets().get(2)
                          .getCells().createRange("A1");
plainSource.copy(plainDest, copyOptions);
```

Este trecho demonstra a flexibilidade da API tanto para cenários com tabela dinâmica quanto sem tabela dinâmica.

---

## Copiar intervalo entre planilhas sem perder fórmulas

Quando você **copia intervalo entre planilhas**, fórmulas que referenciam outras planilhas podem ficar quebradas se as referências relativas mudarem. Para evitar isso:

1. Use `CopyOptions.setPasteType(PasteType.PASTE_FORMULAS)` se você precisar apenas de fórmulas.
2. Mantenha a planilha de destino na mesma pasta de trabalho para que as referências internas permaneçam válidas.
3. Após a cópia, chame `workbook.calculateFormula();` para forçar um recálculo.

```java
copyOptions.setPasteType(PasteType.PASTE_FORMULAS);
sourceRange.copy(destRange, copyOptions);
workbook.calculateFormula();
```

Essas etapas adicionais garantem que um intervalo copiado se comporte exatamente como o original, mesmo quando abrange várias planilhas.

---

## Dicas profissionais e armadilhas comuns

| Situação | Dica |
|-----------|-----|
| **Cache da tabela dinâmica não atualizando** | Depois de copiar, chame `destSheet.getPivotTables().get(0).refresh();` para atualizar o cache. |
| **Copiando para uma pasta de trabalho diferente** | Use `Workbook destWorkbook = new Workbook();` e então `sourceRange.copy(destWorkbook.getWorksheets().get(0).getCells().createRange("A1"), copyOptions);`. Lembre‑se de copiar o cache da tabela dinâmica separadamente, se necessário. |
| **Tabelas dinâmicas grandes** | Aumente o tamanho do heap Java (`-Xmx2g`) para evitar `OutOfMemoryError` durante a cópia. |
| **Preservando estilos** | Defina `copyOptions.setPasteType(PasteType.PASTE_ALL)`; caso contrário, apenas valores são copiados. |

---

## Saída esperada

Executar o programa completo gera `output.xlsx`. Quando aberto no Excel:

* **Sheet2!A1:G20** exibe a mesma tabela dinâmica que **Sheet1!A1:G20**.
* A lista de campos da tabela dinâmica, rótulos de linhas/colunas e valores de dados correspondem à origem.
* Atualizar a tabela dinâmica atualiza os números, confirmando que o cache está funcional.

O console exibirá:

```
Pivot table copied successfully.
```

---

## Conclusão

Neste tutorial você aprendeu **como copiar tabela dinâmica** de uma planilha para outra usando Aspose.Cells for Java. Ao carregar a pasta de trabalho, selecionar o intervalo de origem correto, definir um destino e configurar `CopyOptions`, você pode copiar de forma confiável **intervalo para outra planilha** e **intervalo entre planilhas** preservando toda a funcionalidade da tabela dinâmica.  

Em seguida, você pode explorar:

* Exportar a tabela dinâmica copiada para PDF ou HTML.
* Automatizar a atualização de tabelas dinâmicas em várias pastas de trabalho.
* Usar `CopyOptions` para copiar apenas elementos específicos (por exemplo, valores, formatos).

Sinta‑se à vontade para experimentar diferentes endereços de intervalo, estruturas de pasta de trabalho ou até mesmo cópias entre pastas de trabalho. Boa codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Como copiar intervalo em Java – Copiar Tabela Dinâmica com Aspose.Cells](/cells/english/java/excel-pivot-tables/how-to-copy-range-in-java-copy-pivot-table-with-aspose-cells/)
- [Como Copiar Tabela Dinâmica em Java – Guia Completo do Aspose.Cells](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-complete-aspose-cells-guide/)
- [Copiar Tabela Dinâmica Excel – Guia Passo a Passo Usando Java](/cells/english/java/excel-pivot-tables/copy-pivot-table-excel-step-by-step-guide-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}