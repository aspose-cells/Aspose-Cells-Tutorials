---
category: general
date: 2026-07-29
description: Salve uma nova pasta de trabalho em Java ao copiar intervalo entre pastas
  de trabalho. Aprenda a transferir um intervalo do Excel e preservar a formatação
  ao copiar em apenas alguns passos.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save new workbook
- copy range between workbooks
- transfer excel range
- load excel workbook java
- preserve formatting copy
language: pt
lastmod: 2026-07-29
og_description: Salve uma nova pasta de trabalho em Java com Aspose.Cells — aprenda
  a copiar intervalos entre pastas de trabalho preservando a formatação, tudo em um
  guia conciso passo a passo.
og_image_alt: Java code that saves new workbook after transferring an Excel range
og_title: Salvar Nova Pasta de Trabalho em Java – Copiar Intervalo Entre Pastas de
  Trabalho
schemas:
- author: Aspose
  dateModified: '2026-07-29'
  description: Save new workbook in Java while copy range between workbooks. Learn
    to transfer Excel range and preserve formatting copy in just a few steps.
  headline: Save New Workbook in Java – Copy Range Between Workbooks Tutorial
  type: TechArticle
tags:
- Java
- Excel
- Aspose.Cells
- Workbook
- File I/O
title: Salvar Nova Pasta de Trabalho em Java – Tutorial de Copiar Intervalo entre
  Pastas de Trabalho
url: /pt/java/workbook-operations/save-new-workbook-in-java-copy-range-between-workbooks-tutor/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Salvar Nova Pasta de Trabalho em Java – Tutorial de Copiar Intervalo Entre Pastas de Trabalho

Já precisou **save new workbook** depois de mover dados de um arquivo Excel para outro, mas não tinha certeza de como manter o estilo original? Você não está sozinho. Em muitos aplicativos corporativos, precisamos **transfer Excel range** de um modelo para um arquivo gerado pelo usuário, e o truque é garantir que a formatação sobreviva à transferência.

Neste guia, percorreremos um exemplo completo e executável que **load Excel workbook java**‑style usando Aspose.Cells, **copy range between workbooks**, e finalmente **save new workbook** com todas as cores, bordas e formatos numéricos originais intactos. Sem enrolação—apenas o código que você pode inserir em seu projeto hoje.

> **Dica profissional:** Se você já está usando Maven, adicione a dependência Aspose.Cells uma vez e você estará pronto para qualquer tarefa de manipulação de pastas de trabalho.

## Pré-requisitos

- Java 17 (ou qualquer JDK recente)
- Aspose.Cells for Java (versão 23.10 ou mais recente)
- Familiaridade básica com Java I/O
- Dois arquivos Excel: um fonte (`source.xlsx`) contendo os dados que você deseja mover, e um destino vazio (`dest.xlsx`) que será criado pelo código

Agora, vamos mergulhar nos passos.

## Etapa 1 – Load Excel Workbook Java Style

A primeira coisa que fazemos é **load Excel workbook java**‑wise. Aspose.Cells abstrai o formato do arquivo, então você não precisa se preocupar com o XML subjacente.

```java
import com.aspose.cells.*;

public class ExcelRangeTransfer {
    public static void main(String[] args) throws Exception {
        // Load the source workbook (make sure the path is correct)
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        // ------------------------------------------------------------
        // At this point the source workbook is fully loaded in memory.
        // ------------------------------------------------------------
```

*Por que isso importa:* Carregar a pasta de trabalho lhe dá acesso a cada planilha, célula e objeto de estilo. Se você pular esta etapa e tentar copiar diretamente de um fluxo de arquivo, perderá a capacidade de preservar a formatação posteriormente.

## Etapa 2 – Define the Source Range (Preserve Formatting Copy)

Em seguida, identificamos a área exata que queremos mover. No nosso exemplo, o intervalo `A1:G20` contém uma tabela dinâmica e algumas linhas de cabeçalho. Ao criar um objeto `Range` podemos posteriormente instruir o Aspose.Cells a manter cada estilo intacto—esta é a essência de uma **preserve formatting copy**.

```java
        // Grab the first worksheet
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);

        // Define the range that includes the data we want to copy
        // Using createRange ensures we capture formulas, formats, and comments.
        Range sourceRange = sourceSheet.getCells().createRange("A1:G20");
```

*Dica:* Se precisar copiar uma área dinâmica, você pode calcular a última linha/coluna usada com `sourceSheet.getCells().getMaxDataRow()` e montar a string de endereço em tempo real.

## Etapa 3 – Create Destination Workbook (Where We'll Save New Workbook)

Agora criamos uma nova pasta de trabalho que receberá os dados. É aqui que a ação **save new workbook** acontecerá finalmente.

```java
        // Create a brand‑new workbook that will become our destination file
        Workbook destinationWorkbook = new Workbook();

        // Get its first worksheet – this is where we’ll paste the range
        Worksheet destSheet = destinationWorkbook.getWorksheets().get(0);
```

*Por que criamos uma nova:* Começar com uma pasta de trabalho limpa garante que não haja estilos residuais que possam entrar em conflito com o intervalo recebido. Também reduz o tamanho final do arquivo, pois apenas os recursos necessários são salvos.

## Etapa 4 – Copy Range Between Workbooks

Aqui está o coração do tutorial: **copy range between workbooks** enquanto preserva cada detalhe visual. A classe `CopyOptions` nos permite especificar que queremos uma cópia completa, não apenas valores.

```java
        // Set up copy options to keep everything—values, formulas, formats, comments.
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.ALL); // ensures formatting stays

        // Perform the copy. The destination starts at cell A1 (row 0, column 0).
        destSheet.getCells().copyRange(sourceRange, 0, 0, copyOptions);
```

*Pergunta comum:* *E se eu precisar apenas de valores, sem formatação?* Altere `PasteType.ALL` para `PasteType.VALUES` e a formatação será ignorada.

## Etapa 5 – Save New Workbook

Finalmente gravamos o arquivo de destino no disco. Este é o momento em que realmente **save new workbook** e vemos o resultado de nossas etapas anteriores.

```java
        // Persist the destination workbook to the file system
        destinationWorkbook.save("YOUR_DIRECTORY/dest.xlsx");
        System.out.println("Destination workbook saved successfully.");
    }
}
```

Ao abrir `dest.xlsx` você verá exatamente a mesma aparência e sensação do intervalo original `source.xlsx`—cores, bordas e formatos numéricos todos intactos.

---

<img src="excel-copy.png" alt="Código Java que salva nova pasta de trabalho após transferir um intervalo Excel" />

## Exemplo Completo (Todas as Etapas Combinadas)

Abaixo está o programa completo e autocontido. Copie-o para um arquivo chamado `ExcelRangeTransfer.java`, ajuste os caminhos dos arquivos e execute-o com `javac`/`java`.

```java
import com.aspose.cells.*;

public class ExcelRangeTransfer {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // 2️⃣ Get the first worksheet and define the range we want to copy
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);
        Range sourceRange = sourceSheet.getCells().createRange("A1:G20");

        // 3️⃣ Create a fresh destination workbook
        Workbook destinationWorkbook = new Workbook();
        Worksheet destSheet = destinationWorkbook.getWorksheets().get(0);

        // 4️⃣ Copy the defined range – preserving formatting
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.ALL);
        destSheet.getCells().copyRange(sourceRange, 0, 0, copyOptions);

        // 5️⃣ Save new workbook to disk
        destinationWorkbook.save("YOUR_DIRECTORY/dest.xlsx");
        System.out.println("Destination workbook saved successfully.");
    }
}
```

**Saída esperada** ao executar o programa:

```
Destination workbook saved successfully.
```

Abra `dest.xlsx` e você verá a réplica exata de `A1:G20` da fonte, completa com sua formatação original.

## Perguntas Frequentes & Casos Limítrofes

| Question | Answer |
|----------|--------|
| *Can I copy between workbooks that use different Excel versions?* | Yes. Aspose.Cells normalizes the format internally, so a `.xls` source can be copied into a `.xlsx` destination without extra work. |
| *What if the destination already contains data?* | Use `copyRange` with a different start row/column (e.g., `5, 2`) to paste elsewhere, or clear the sheet first with `destSheet.getCells().clearAll()`. |
| *Do formulas stay linked to the original workbook?* | By default they become **relative** to the destination. If you need external references, set `copyOptions.setPasteType(PasteType.FORMULAS)` and handle workbook links manually. |
| *How do I preserve column widths?* | Column widths are part of the format; `PasteType.ALL` already copies them. If you notice discrepancies, call `destSheet.autoFitColumns()` after the copy. |

## Próximos Passos – Indo Além do Básico

Agora que você sabe como **save new workbook**, **copy range between workbooks**, e **preserve formatting copy**, pode querer explorar:

- **Batch processing** – percorrer uma pasta de arquivos fonte e gerar um relatório consolidado.
- **Conditional formatting transfer** – usar `CopyOptions.setPasteType(PasteType.FORMATS)` para focar apenas nos estilos.
- **Streaming API** – para arquivos massivos, a classe `Workbook` oferece um modo de baixa memória que ainda suporta cópia de intervalos.

Cada um desses tópicos se baseia naturalmente nos conceitos abordados aqui, e todos giram em torno da mesma ideia central: manipular arquivos Excel em Java com confiança e precisão.

---

### TL;DR

Começamos com **load excel workbook java**, definimos um **transfer excel range**, usamos **copy range between workbooks** com `CopyOptions` para **preserve formatting copy**, criamos um arquivo novo e, finalmente, **save new workbook**. O resultado é um `dest.xlsx` totalmente funcional que espelha o intervalo da fonte até o último estilo de célula.

Experimente, ajuste o endereço do intervalo e veja quão rápido você pode automatizar tarefas de relatórios Excel em Java. Feliz codificação!

## O Que Você Deve Aprender a Seguir?

Os tutoriais a seguir abordam tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá-lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Como Implementar um Intervalo Nomeado com Escopo de Pasta de Trabalho no Aspose.Cells Java para Gerenciamento Avançado de Dados Excel](/cells/english/java/tables-structured-references/implement-named-range-workbook-scope-aspose-cells-java/)
- [Salvar Pasta de Trabalho Excel com Aspose.Cells para Java – Guia Completo](/cells/english/java/automation-batch-processing/excel-workbook-automation-aspose-cells-java/)
- [Salvar Arquivo Excel Java com Aspose.Cells – Dominando a Automação de Pastas de Trabalho](/cells/english/java/automation-batch-processing/aspose-cells-java-excel-workbook-automation/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}