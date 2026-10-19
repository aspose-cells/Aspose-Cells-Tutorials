---
category: general
date: 2026-06-27
description: Abra arquivos XLSX em Java rapidamente. Aprenda como ler arquivos Excel
  em Java, carregar a pasta de trabalho do Excel e recalcular todas as fórmulas usando
  o Apache POI.
draft: false
keywords:
- open xlsx file
- recalculate all formulas
- read excel file in java
- how to recalculate excel formulas
- load excel workbook
language: pt
og_description: Abra um arquivo XLSX em Java e aprenda como ler um arquivo Excel em
  Java, carregar a pasta de trabalho Excel e, em seguida, recalcular todas as fórmulas
  com um exemplo claro e executável.
og_title: Abrir arquivo XLSX em Java – Carregamento passo a passo da pasta de trabalho
  e recálculo de fórmulas
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Open XLSX file in Java quickly. Learn how to read Excel file in Java,
    load Excel workbook, and recalculate all formulas using Apache POI.
  headline: Open XLSX File in Java – Complete Guide to Load Workbook & Recalculate
    Formulas
  type: TechArticle
- questions:
  - answer: Not directly. For older binary formats you’d use `HSSFWorkbook` instead
      of `XSSFWorkbook`. The rest of the code (evaluator, saving) stays the same.
    question: Does this work with `.xls` files?
  - answer: POI does not execute VBA macros, but it can preserve them when you write
      the file back. The formulas will still be recalculated.
    question: What if the workbook contains macros?
  - answer: 'Yes—call `evaluator.evaluateAll()` on the sheet object: `evaluator.evaluateAll(sheet);`.
      ## Wrap‑Up We’ve just shown you how to **open XLSX file in Java**, **load Excel
      workbook**, and **recalculate all formulas** in a clean, production‑ready way.
      The example covers *how to recalculate Excel formula'
    question: Can I recalculate only a single sheet?
  type: FAQPage
tags:
- java
- excel
- apache-poi
title: Abrir arquivo XLSX em Java – Guia completo para carregar a pasta de trabalho
  e recalcular fórmulas
url: /pt/java/calculation-engine/open-xlsx-file-in-java-complete-guide-to-load-workbook-recal/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Abrir Arquivo XLSX em Java – Guia Completo para Carregar a Pasta de Trabalho & Recalcular Fórmulas

Já precisou **abrir um arquivo XLSX** em Java, mas não sabia qual biblioteca escolher ou como fazer as fórmulas atualizarem automaticamente? Você não está sozinho. Muitos desenvolvedores esbarram nessa barreira ao tentar *ler um arquivo Excel em Java* para relatórios ou tarefas de migração de dados.

Neste tutorial vamos percorrer uma solução do mundo real: carregar uma pasta de trabalho Excel, **recalcular todas as fórmulas**, e salvar o resultado—sem precisar de planilhas manuais. Ao final, você saberá exatamente *como recalcular fórmulas do Excel* programaticamente e terá um exemplo de código pronto para executar.

## O Que Você Vai Precisar

- Java 8 ou superior (o código funciona em Java 11, 17, etc.)  
- Apache POI 5.x (a biblioteca de fato para manipulação de Excel em Java)  
- Um simples arquivo `dynamic.xlsx` colocado em algum local que você possa referenciar a partir do seu projeto  
- Seu IDE favorito ou um editor de texto simples—não importa, o código é direto  

Se já tem tudo isso, ótimo—vamos começar.

## Abrir Arquivo XLSX em Java – Carregar a Pasta de Trabalho Excel

O primeiro passo é **carregar a pasta de trabalho excel** a partir do disco. Pense nisso como abrir a porta da planilha; sem isso você não vê nenhuma célula ou fórmula dentro.

```java
import java.io.FileInputStream;
import java.io.FileOutputStream;
import org.apache.poi.ss.usermodel.*;
import org.apache.poi.xssf.usermodel.XSSFWorkbook;

/**
 * Demonstrates opening an XLSX file, recalculating formulas, and saving the result.
 */
public class ExcelFormulaRecalc {

    public static void main(String[] args) throws Exception {
        // Path to the file you want to open
        String inputPath = "dynamic.xlsx";

        // Step 1: Load the workbook (open xlsx file)
        try (FileInputStream fis = new FileInputStream(inputPath);
             Workbook workbook = new XSSFWorkbook(fis)) {

            // The workbook is now in memory – ready for further actions
            System.out.println("Workbook loaded successfully.");
```

> **Por que XSSFWorkbook?**  
> `XSSFWorkbook` lida com o formato OOXML moderno `.xlsx`, enquanto `HSSFWorkbook` é para o legado `.xls`. Usar a classe correta garante que você realmente **abra um arquivo XLSX** sem encontrar `InvalidFormatException`.

## Recalcular Todas as Fórmulas na Pasta de Trabalho

Agora que o arquivo está aberto, a próxima pergunta lógica é *“como recalcular fórmulas do Excel?”* A resposta está no `FormulaEvaluator` do POI. Ele percorre todo o grafo da planilha, avaliando cada célula que contém uma fórmula.

```java
            // Step 2: Create a FormulaEvaluator (how to recalculate excel formulas)
            FormulaEvaluator evaluator = workbook.getCreationHelper().createFormulaEvaluator();

            // Step 3: Force POI to evaluate every formula cell (recalculate all formulas)
            evaluator.evaluateAll();

            System.out.println("All formulas have been recalculated.");
```

> **Dica profissional:** Se você precisa atualizar apenas uma única planilha, chame `evaluator.evaluateAll()` nessa planilha em vez de em toda a pasta de trabalho. Isso pode economizar memória em arquivos gigantes.

### Casos Limite & Armadilhas Comuns

| Situação | O Que Observar | Correção Sugerida |
|-----------|-------------------|---------------|
| Pastas de trabalho muito grandes (centenas de MB) | POI pode esgotar a memória heap | Use `SXSSFWorkbook` para escrita em streaming, ou aumente `-Xmx` |
| Células contêm referências externas | POI não consegue resolvê‑las automaticamente | Pré‑popule os dados necessários ou evite links externos |
| Funções personalizadas (UDFs) | POI não sabe como avaliá‑las | Implemente um `UDFFinder` ou ignore essas células |

## Verificar e Salvar a Pasta de Trabalho Atualizada

Recalcular só é útil se você puder ver o resultado. Vamos escrever a pasta de trabalho atualizada de volta ao disco. Você poderia sobrescrever o arquivo original, mas o exemplo abaixo grava em um novo arquivo para manter a segurança.

```java
            // Step 4: Write the updated workbook to a new file
            String outputPath = "dynamic_updated.xlsx";
            try (FileOutputStream fos = new FileOutputStream(outputPath)) {
                workbook.write(fos);
            }

            System.out.println("Updated workbook saved as " + outputPath);
        }
    }
}
```

Executar o programa exibe:

```
Workbook loaded successfully.
All formulas have been recalculated.
Updated workbook saved as dynamic_updated.xlsx
```

Abra `dynamic_updated.xlsx` no Excel e você verá que cada fórmula agora reflete os dados mais recentes—exatamente o que se espera após uma operação manual de **recalcular todas as fórmulas**.

## Lendo Células Específicas (Opcional)

Se o seu objetivo é *ler um arquivo Excel em Java* após a recalculação, você pode obter valores de célula assim:

```java
Sheet sheet = workbook.getSheetAt(0); // first sheet
Row row = sheet.getRow(1); // second row (0‑based)
Cell cell = row.getCell(2); // third column

if (cell.getCellType() == CellType.NUMERIC) {
    double value = cell.getNumericCellValue();
    System.out.println("Recalculated value: " + value);
}
```

Este trecho mostra como extrair um único valor recém‑calculado da pasta de trabalho—útil para alimentar dados a outros componentes Java.

## Recapitulação do Exemplo Completo

Juntando tudo, aqui está o programa completo e autocontido que você pode copiar‑colar em `ExcelFormulaRecalc.java` e executar:

```java
import java.io.FileInputStream;
import java.io.FileOutputStream;
import org.apache.poi.ss.usermodel.*;
import org.apache.poi.xssf.usermodel.XSSFWorkbook;

public class ExcelFormulaRecalc {
    public static void main(String[] args) throws Exception {
        String inputPath = "dynamic.xlsx";
        String outputPath = "dynamic_updated.xlsx";

        try (FileInputStream fis = new FileInputStream(inputPath);
             Workbook workbook = new XSSFWorkbook(fis)) {

            // Load the workbook (open xlsx file)
            System.out.println("Workbook loaded successfully.");

            // Recalculate all formulas (how to recalculate excel formulas)
            FormulaEvaluator evaluator = workbook.getCreationHelper().createFormulaEvaluator();
            evaluator.evaluateAll();
            System.out.println("All formulas have been recalculated.");

            // Optional: read a specific cell after recalculation
            Sheet sheet = workbook.getSheetAt(0);
            Row row = sheet.getRow(1);
            Cell cell = row.getCell(2);
            if (cell != null && cell.getCellType() == CellType.NUMERIC) {
                System.out.println("Recalculated cell value: " + cell.getNumericCellValue());
            }

            // Save the updated workbook
            try (FileOutputStream fos = new FileOutputStream(outputPath)) {
                workbook.write(fos);
            }
            System.out.println("Updated workbook saved as " + outputPath);
        }
    }
}
```

Salve o arquivo, adicione o Apache POI ao classpath do seu projeto (usuários Maven podem incluir a dependência `poi-ooxml`), e execute `java ExcelFormulaRecalc`. Pronto—você **abriu um arquivo XLSX**, **recalculou todas as fórmulas**, e **salvou as alterações**.

![Exemplo de abrir arquivo XLSX em Java](/images/open-xlsx-java.png "abrir arquivo xlsx")

*Texto alternativo da imagem: exemplo de abrir arquivo xlsx em Java mostrando editor de código e saída do console.*

## Perguntas Frequentes

**Q: Isso funciona com arquivos `.xls`?**  
A: Não diretamente. Para formatos binários antigos você usaria `HSSFWorkbook` em vez de `XSSFWorkbook`. O restante do código (avaliador, salvamento) permanece o mesmo.

**Q: E se a pasta de trabalho contiver macros?**  
A: O POI não executa macros VBA, mas pode preservá‑las ao escrever o arquivo de volta. As fórmulas ainda serão recalculadas.

**Q: Posso recalcular apenas uma única planilha?**  
A: Sim—chame `evaluator.evaluateAll()` no objeto da planilha: `evaluator.evaluateAll(sheet);`.

## Conclusão

Acabamos de mostrar como **abrir um arquivo XLSX em Java**, **carregar a pasta de trabalho Excel**, e **recalcular todas as fórmulas** de forma limpa e pronta para produção. O exemplo cobre *como recalcular fórmulas do Excel*, demonstra *ler um arquivo Excel em Java*, e destaca as nuances de *carregar pasta de trabalho excel* tanto para arquivos pequenos quanto grandes.

A seguir, você pode explorar:

- Adicionar estilos ou gráficos com as classes `XSSF` do POI  
- Fazer streaming de grandes pastas de trabalho com `SXSSFWorkbook` para gravações de baixa memória  
- Integrar a solução a um serviço Spring Boot que processa uploads em tempo real  

Experimente, e logo você estará automatizando fluxos de trabalho pesados em Excel como um profissional. Mais dúvidas? Deixe um comentário, e feliz codificação!

## O Que Você Deve Aprender a Seguir?

Os tutoriais abaixo abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [Master Excel File Manipulation Using Aspose.Cells for Java | Workbook Operations Guide](/cells/english/java/workbook-operations/master-excel-manipulation-aspose-cells-java/)
- [Master Excel File Operations in Java Using Aspose.Cells](/cells/english/java/workbook-operations/excel-file-operations-aspose-cells-java/)
- [Master Excel XLSB File Management in Java with Aspose.Cells: Load and Modify DB Connections](/cells/english/java/workbook-operations/excel-xlsb-management-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}