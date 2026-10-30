---
category: general
date: 2026-08-04
description: Criar tabela Excel em Java e aprender como desativar o autofiltro, definir
  o intervalo de células e salvar a planilha como xlsx com um exemplo de código completo.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel table
- turn off autofilter
- define cell range
- save workbook as xlsx
- disable autofilter in excel
language: pt
lastmod: 2026-08-04
og_description: Crie uma tabela Excel em Java, desative o autofiltro, defina o intervalo
  de células e salve a planilha como xlsx. Siga este tutorial completo para dominar
  a automação do Excel.
og_image_alt: Image showing how to create excel table without autofilter using Java
og_title: Criar tabela Excel em Java – tutorial completo do código
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Create excel table in Java and learn how to turn off autofilter, define
    cell range, and save workbook as xlsx with a complete code example.
  headline: Create excel table in Java – step‑by‑step guide
  type: TechArticle
- description: Create excel table in Java and learn how to turn off autofilter, define
    cell range, and save workbook as xlsx with a complete code example.
  name: Create excel table in Java – step‑by‑step guide
  steps:
  - name: Define cell range for the table
    text: Next, you must specify the exact area that will become the table. The **define
      cell range** step tells Aspose.Cells which rows and columns to include.
  - name: Add the table and enable its default AutoFilter
    text: Now you add a `ListObject` (the Aspose.Cells representation of an Excel
      table). By default, a new table includes an AutoFilter dropdown for each column.
  - name: Turn off autofilter for the table
    text: If you want a clean table without filter dropdowns, you must **turn off
      autofilter** (or **disable autofilter in excel**). The API call is straightforward.
  - name: Save workbook as xlsx file
    text: Finally, persist the workbook to disk. The **save workbook as xlsx** call
      writes a standard Office Open XML file that any modern spreadsheet program can
      open.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Criar tabela Excel em Java – guia passo a passo
url: /pt/java/tables-structured-references/create-excel-table-in-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar tabela Excel em Java – guia passo a passo

Se você precisa **criar tabela excel** em Java, este tutorial mostra exatamente como fazer isso. Você aprenderá a **definir intervalo de células**, **desativar autofilter** e **salvar a pasta de trabalho como xlsx** com um único programa executável.

O exemplo usa a biblioteca Aspose.Cells for Java, que fornece uma API de alto nível para automação do Excel. Nenhuma dependência adicional é necessária além do JAR do Aspose.Cells. Ao final do guia, você terá uma solução autônoma que pode ser inserida em qualquer projeto Java.

## O que você vai construir

* Um novo workbook contendo uma planilha.  
* Uma tabela (ListObject) que abrange um **intervalo de células** específico (A1:D5).  
* O AutoFilter da tabela desativado **off** (ou seja, **disable autofilter in excel**).  
* O workbook salvo como um arquivo **xlsx** no disco.

## Pré-requisitos

* Java 8 ou superior instalado.  
* Aspose.Cells for Java (download do site oficial ou adicione via Maven).  
* Familiaridade básica com a sintaxe Java e IDEs como IntelliJ IDEA ou Eclipse.

---

## Como criar tabela excel sem autofilter em Java

O primeiro passo importante é instanciar um `Workbook` e obter a planilha padrão. Isso fornece uma tela limpa onde você pode colocar uma tabela.

```java
import com.aspose.cells.*;

public class CreateExcelTable {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

**Por que isso importa:**  
Um `Workbook` representa o arquivo Excel completo. A primeira planilha (`get(0)`) é criada automaticamente, portanto você não precisa adicionar uma manualmente. Começar com uma planilha nova garante que nenhum dado residual interfira na tabela que você criará.

### Definir intervalo de células para a tabela

Em seguida, você deve especificar a área exata que se tornará a tabela. O passo de **definir intervalo de células** informa ao Aspose.Cells quais linhas e colunas incluir.

```java
        // Step 2: Define the cell range that will become the table (A1:D5)
        CellArea tableRange = CellArea.createCellArea("A1", "D5");
```

**Por que isso importa:**  
`CellArea` codifica os cantos superior‑esquerdo e inferior‑direito do intervalo. Ao usar `"A1"` e `"D5"` você cria um bloco de 5 linhas × 4 colunas, que é o tamanho típico para uma tabela de dados simples.

### Adicionar a tabela e habilitar seu AutoFilter padrão

Agora você adiciona um `ListObject` (a representação Aspose.Cells de uma tabela Excel). Por padrão, uma nova tabela inclui um dropdown AutoFilter para cada coluna.

```java
        // Step 3: Add a table (ListObject) to the worksheet and enable its AutoFilter
        ListObject table = worksheet.getListObjects().add("MyTable", tableRange, true);
        table.setShowAutoFilter(true); // AutoFilter is turned on by default
```

**Por que isso importa:**  
Habilitar `setShowAutoFilter(true)` reflete o comportamento padrão do Excel, tornando a tabela imediatamente filtrável. Este passo é opcional, mas esclarece o estado antes de desativá-lo.

### Desativar autofilter para a tabela

Se você deseja uma tabela limpa sem dropdowns de filtro, deve **desativar autofilter** (ou **disable autofilter in excel**). A chamada da API é simples.

```java
        // Step 4: Disable the AutoFilter for the table
        table.setShowAutoFilter(false);
```

**Por que isso importa:**  
Desativar o AutoFilter melhora a legibilidade quando a tabela é usada para relatórios ou impressão. Também reduz a desordem da UI para os usuários finais que não precisam de filtragem interativa.

### Salvar workbook como arquivo xlsx

Finalmente, persista o workbook no disco. A chamada **save workbook as xlsx** grava um arquivo Office Open XML padrão que qualquer programa de planilha moderno pode abrir.

```java
        // Step 5: Save the workbook to a file
        workbook.save("TableNoAutoFilter.xlsx", SaveFormat.XLSX);
    }
}
```

**Por que isso importa:**  
Escolher o formato `XLSX` garante compatibilidade com Excel 2007+ e com serviços em nuvem como Google Sheets. O nome do arquivo `TableNoAutoFilter.xlsx` reflete claramente que o AutoFilter foi desativado.

---

## Recapitulação do código-fonte completo

Juntando todos os trechos, obtém-se um programa completo e executável:

```java
import com.aspose.cells.*;

public class CreateExcelTable {
    public static void main(String[] args) throws Exception {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Define the cell range that will become the table (A1:D5)
        CellArea tableRange = CellArea.createCellArea("A1", "D5");

        // Add a table (ListObject) to the worksheet and enable its AutoFilter
        ListObject table = worksheet.getListObjects().add("MyTable", tableRange, true);
        table.setShowAutoFilter(true); // AutoFilter is on by default

        // Disable the AutoFilter for the table
        table.setShowAutoFilter(false);

        // Save the workbook to a file (xlsx format)
        workbook.save("TableNoAutoFilter.xlsx", SaveFormat.XLSX);
    }
}
```

**Resultado esperado:**  
Ao abrir `TableNoAutoFilter.xlsx` no Microsoft Excel, você verá uma tabela chamada **MyTable** cobrindo as células A1:D5. Nenhuma seta de filtro aparece nos cabeçalhos das colunas, confirmando que o passo de **turn off autofilter** foi bem-sucedido.

## Perguntas comuns e casos extremos

| Question | Answer |
|----------|--------|
| *Posso adicionar dados antes de criar a tabela?* | Sim. Preencha as células no intervalo definido primeiro; a tabela incluirá automaticamente os dados. |
| *E se a planilha já contiver dados?* | Escolha um **intervalo de células** diferente que não sobreponha o conteúdo existente, ou limpe a área com `worksheet.getCells().clear(A1, D5)`. |
| *É possível manter o AutoFilter apenas em algumas colunas?* | Aspose.Cells não suporta alternar o AutoFilter por coluna; você deve mantê-lo ativado para toda a tabela ou desativá-lo completamente. |
| *Como altero o estilo da tabela?* | Use `table.setTableStyleType( TableStyleType.TABLE_STYLE_MEDIUM_2 );` antes de salvar. |
| *Isso funcionará em versões antigas do Excel (xls)?* | Salve com `SaveFormat.XLS` em vez de `XLSX`, mas observe que alguns recursos mais recentes (como ListObject) podem ser limitados. |

**Dica profissional:** Sempre chame `workbook.save(..., SaveFormat.XLSX)` depois de concluir todas as modificações da tabela. Salvar várias vezes pode aumentar o tamanho do arquivo desnecessariamente.

## Próximos passos

Agora que você sabe como **criar tabela excel**, **definir intervalo de células**, **desativar autofilter** e **salvar workbook como xlsx**, pode estender a solução:

* **Adicionar fórmulas** às colunas calculadas usando `table.getListColumns().get(i).setFormula("=SUM(...)")`.  
* **Aplicar formatação condicional** para destacar linhas que atendam a certos critérios.  
* **Exportar o workbook para PDF** com `workbook.save("Table.pdf", SaveFormat.PDF)` para fins de relatório.  

Cada um desses tópicos se baseia nos conceitos centrais abordados neste tutorial e demonstra ainda como **disable autofilter in excel** quando necessário.

## Conclusão

Agora você tem um exemplo completo e pronto para produção que mostra como **criar tabela excel** em Java, **definir intervalo de células**, **desativar autofilter** e **salvar workbook como xlsx**. Seguindo o código passo a passo e as explicações, você pode integrar a criação de tabelas Excel em qualquer aplicação Java e controlar o comportamento do AutoFilter programaticamente. Feliz codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá-lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Como criar e salvar uma pasta de trabalho Excel como SVG usando Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [Criar e salvar pasta de trabalho Excel Aspose Cells Java](/cells/hindi/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)
- [Criar e salvar pasta de trabalho Excel Aspose Cells Java](/cells/german/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}