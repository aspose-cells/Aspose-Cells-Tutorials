---
category: general
date: 2026-10-20
description: Aprenda a copiar tabelas dinâmicas usando Aspose.Cells em Java. Este
  tutorial mostra como copiar um intervalo para uma nova planilha e duplicar a planilha
  de tabela dinâmica com segurança.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy range to new sheet
- duplicate pivot table sheet
language: pt
lastmod: 2026-10-20
og_description: Como copiar tabela dinâmica com Aspose.Cells em Java. Siga este guia
  para copiar o intervalo para uma nova planilha e duplicar a planilha da tabela dinâmica
  sem perder dados.
og_image_alt: Screenshot showing how to copy pivot table from one worksheet to another
  in a Java program
og_title: Como copiar tabela dinâmica em Java – tutorial completo do Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-10-20'
  description: Learn how to copy pivot table using Aspose.Cells in Java. This tutorial
    shows how to copy range to new sheet and duplicate pivot table sheet safely.
  headline: How to copy pivot table in Java with Aspose.Cells – step‑by‑step guide
  type: TechArticle
- description: Learn how to copy pivot table using Aspose.Cells in Java. This tutorial
    shows how to copy range to new sheet and duplicate pivot table sheet safely.
  name: How to copy pivot table in Java with Aspose.Cells – step‑by‑step guide
  steps:
  - name: Load the workbook that holds the original pivot table.
    text: Load the workbook that holds the original pivot table.
  - name: Identify the exact range that includes the pivot table.
    text: Identify the exact range that includes the pivot table.
  - name: Create a new worksheet that will receive the copied data.
    text: Create a new worksheet that will receive the copied data.
  - name: Use the `Range.copy` method to transfer the range to the new sheet.
    text: Use the `Range.copy` method to transfer the range to the new sheet.
  - name: Save the workbook to a new file.
    text: Save the workbook to a new file.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Como copiar tabela dinâmica em Java com Aspose.Cells – guia passo a passo
url: /pt/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-with-aspose-cells-step-by-st/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como copiar tabela dinâmica em Java com Aspose.Cells – guia passo a passo

Se você precisa **como copiar tabela dinâmica** em uma aplicação Java, este guia o conduzirá pelos passos exatos. Seja construindo um mecanismo de relatórios ou automatizando a migração de dados, você verá como copiar um intervalo para uma nova planilha preservando a definição e os dados da tabela dinâmica.

Copiar uma tabela dinâmica pode parecer arriscado porque o cache subjacente e as configurações de campo frequentemente se perdem. Este tutorial demonstra uma abordagem confiável usando Aspose.Cells, mostra o código completo executável e explica por que cada linha é importante. Ao final, você será capaz de duplicar a planilha da tabela dinâmica em segundos.

## Pré-requisitos

Antes de começar, certifique‑se de que você tem:

* Java 8 ou mais recente instalado.
* Aspose.Cells for Java (versão 23.10 ou posterior) adicionada ao classpath do seu projeto.
* Uma pasta de trabalho de origem (`source.xlsx`) que contém uma tabela dinâmica no intervalo `A1:G20`.
* Familiaridade básica com Java e conceitos do Excel.

Nenhuma biblioteca adicional é necessária; o Aspose.Cells lida com todas as operações do Excel internamente.

## Como copiar tabela dinâmica – estratégia geral

A ideia central é simples:

1. Carregar a pasta de trabalho que contém a tabela dinâmica original.
2. Identificar o intervalo exato que inclui a tabela dinâmica.
3. Criar uma nova planilha que receberá os dados copiados.
4. Usar o método `Range.copy` para transferir o intervalo para a nova planilha.  
   Esse método copia automaticamente o cache da tabela dinâmica, de modo que a tabela permanece funcional.
5. Salvar a pasta de trabalho em um novo arquivo.

Como a operação de cópia funciona ao nível de intervalo, a **planilha duplicada da tabela dinâmica** mantém todas as configurações de campo, filtros e itens calculados.

## Etapa 1: Carregar a pasta de trabalho de origem

```java
// Import Aspose.Cells classes
import com.aspose.cells.*;

public class PivotCopyDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that contains the pivot table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
```

*Por que isso importa*: Carregar a pasta de trabalho fornece acesso às suas planilhas, células e ao cache da tabela dinâmica. O Aspose.Cells lê todo o arquivo para a memória, de modo que as operações subsequentes são rápidas e thread‑safe.

## Etapa 2: Definir o intervalo de origem que contém a tabela dinâmica

```java
        // Locate the first worksheet (index 0) and create a range covering the pivot table
        Range sourceRange = workbook.getWorksheets()
                                    .get(0)               // first sheet
                                    .getCells()
                                    .createRange("A1:G20"); // adjust if your pivot table is larger
```

*Por que isso importa*: A chamada `createRange` informa ao Aspose.Cells exatamente quais células copiar. Incluir toda a área da tabela dinâmica garante que as linhas de cache ocultas também sejam transferidas. Se você omitir alguma parte do cache, a tabela dinâmica copiada aparecerá vazia.

## Etapa 3: Adicionar uma planilha de destino para os dados copiados

```java
        // Add a new worksheet that will hold the duplicated pivot table
        Worksheet destinationSheet = workbook.getWorksheets().add("CopyResult");
```

*Por que isso importa*: Adicionar uma planilha dedicada isola a tabela dinâmica copiada da original, facilitando a comparação de resultados ou o uso da planilha como modelo para processamento adicional.

## Etapa 4: Copiar o intervalo para a planilha de destino (tabela dinâmica preservada)

```java
        // Copy the defined range to cell A1 of the new worksheet
        sourceRange.copy(destinationSheet.getCells().createRange("A1"));
```

*Por que isso importa*: O método `copy` não apenas copia valores e formatação das células, mas também replica o cache da tabela dinâmica. Este é o passo chave que permite **duplicar a planilha da tabela dinâmica** sem perder nenhuma funcionalidade.

## Etapa 5: Salvar a pasta de trabalho com o intervalo copiado

```java
        // Persist the workbook to a new file
        workbook.save("YOUR_DIRECTORY/result.xlsx");
    }
}
```

*Por que isso importa*: Salvar cria um novo arquivo Excel (`result.xlsx`) que contém tanto a original quanto a planilha duplicada da tabela dinâmica. Agora você pode abrir o arquivo no Excel para verificar que a tabela dinâmica funciona exatamente como antes.

## Exemplo completo e executável

Juntando tudo, aqui está o programa completo que você pode copiar‑colar no seu IDE:

```java
import com.aspose.cells.*;

public class PivotCopyDemo {
    public static void main(String[] args) throws Exception {
        // 1. Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // 2. Define the source range that contains the pivot table
        Range sourceRange = workbook.getWorksheets()
                                    .get(0)
                                    .getCells()
                                    .createRange("A1:G20");

        // 3. Add a destination worksheet for the copied data
        Worksheet destinationSheet = workbook.getWorksheets().add("CopyResult");

        // 4. Copy the range to the destination worksheet (pivot table is preserved)
        sourceRange.copy(destinationSheet.getCells().createRange("A1"));

        // 5. Save the workbook with the copied range
        workbook.save("YOUR_DIRECTORY/result.xlsx");
    }
}
```

### Saída esperada

* Ao abrir `result.xlsx` são exibidas duas planilhas:
  * **Sheet1** – os dados originais e a tabela dinâmica.
  * **CopyResult** – uma duplicata exata da tabela dinâmica, totalmente funcional.
* Todos os campos, filtros e itens calculados da tabela dinâmica se comportam identicamente ao da origem.

Se você modificar a tabela dinâmica de origem após a cópia, a planilha duplicada **não** refletirá essas alterações porque o cache foi duplicado no momento da cópia. Esse isolamento costuma ser desejável quando você precisa de um instantâneo do relatório.

## Armadilhas comuns e como evitá‑las

| Problema | Por que acontece | Solução |
|----------|------------------|---------|
| **A tabela dinâmica aparece em branco** | O intervalo copiado omitiu as linhas de cache ocultas. | Certifique‑se de que o intervalo inclui todo o cache (geralmente algumas linhas abaixo da tabela visível). |
| **Nome da planilha de destino já existe** | `add("CopyResult")` lança exceção se o nome já estiver em uso. | Use `workbook.getWorksheets().addUniqueName("CopyResult")` ou verifique `contains` antes de adicionar. |
| **Erros de caminho de arquivo** | `YOUR_DIRECTORY` incorreto gera `FileNotFoundException`. | Use caminhos absolutos ou `Paths.get(...).toAbsolutePath()` do Java para resolver as localizações. |
| **Desempenho lento em pastas de trabalho grandes** | Copiar intervalos massivos inclui células desnecessárias. | Limite o intervalo à área exata da tabela dinâmica ou use `Range.copy` com `CopyOptions` para pular formatação, se não for necessária. |

## Dica avançada: Usando `CopyOptions` para controle mais fino

Se você precisa apenas dos dados da tabela dinâmica e deseja ignorar a formatação das células, pode passar um objeto `CopyOptions`:

```java
CopyOptions options = new CopyOptions();
options.setCopyStyle(false);        // skip styles
options.setCopyMerged(true);        // keep merged cells
sourceRange.copy(destinationSheet.getCells().createRange("A1"), options);
```

Isso reduz o tamanho do arquivo da planilha duplicada e acelera a operação de cópia, especialmente em pastas de trabalho grandes.

## Como copiar intervalo para nova planilha sem perder fórmulas

O exemplo acima já copia fórmulas porque `Range.copy` as preserva por padrão. Se você quiser apenas valores (por exemplo, para congelar o estado atual), defina `options.setPasteType(PasteType.VALUES)`.

```java
CopyOptions opt = new CopyOptions();
opt.setPasteType(PasteType.VALUES);
sourceRange.copy(destinationSheet.getCells().createRange("A1"), opt);
```

Agora a planilha de destino contém valores estáticos, mas a tabela dinâmica ainda funcionará porque seu cache faz parte do intervalo.

## Recapitulação da solução

* **Como copiar tabela dinâmica** – carregue a pasta de trabalho, defina o intervalo exato, adicione uma nova planilha, copie o intervalo e salve.
* O processo também demonstra **copiar intervalo para nova planilha** e como **duplicar a planilha da tabela dinâmica** com segurança.
* Você pode ajustar a cópia com `CopyOptions` para melhorar desempenho ou cenários apenas‑valor.

## Próximos passos e tópicos relacionados

* **Atualizar cache da tabela dinâmica programaticamente** – use `PivotTable.refreshData()` após atualizar os dados de origem.
* **Exportar tabela dinâmica para PDF** – combine esta técnica de cópia com `PdfSaveOptions` para criar relatórios instantâneos.
* **Automatizar duplicação de múltiplas planilhas** – percorra todas as planilhas e aplique a mesma lógica de cópia.

Experimente essas variações para adaptar o padrão ao seu pipeline de relatórios específico. Se encontrar casos extremos, como fontes de dados externas ou pivôs controlados por VBA, a mesma abordagem de cópia de intervalo funciona, mas pode ser necessário copiar também os objetos de conexão subjacentes.

---

*Feliz codificação! Se este tutorial ajudou você a aprender **como copiar tabela dinâmica**, sinta‑se à vontade para compartilhá‑lo com colegas ou contribuir com melhorias.*

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [How to copy range and preserve a pivot table in Java](/cells/english/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/)
- [Create New Workbook in Java – Full Guide to Copy Pivot Table](/cells/english/java/excel-pivot-tables/create-new-workbook-in-java-full-guide-to-copy-pivot-table/)
- [Copy Pivot Table Between Workbooks – Step‑by‑Step Java Guide](/cells/english/java/excel-pivot-tables/copy-pivot-table-between-workbooks-step-by-step-java-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}