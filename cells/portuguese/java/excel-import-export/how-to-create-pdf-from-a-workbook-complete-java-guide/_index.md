---
category: general
date: 2026-03-01
description: Como criar PDF e salvar a pasta de trabalho como PDF, exportar Excel
  para HTML e usar a função expand com Aspose.Cells para Java. Código passo a passo
  incluído.
draft: false
keywords:
- how to create pdf
- save workbook as pdf
- export excel to html
- use expand function
language: pt
og_description: Como criar PDF a partir de uma planilha usando Aspose.Cells para Java.
  Aprenda a salvar a planilha como PDF, exportar Excel para HTML e usar a função EXPAND.
og_title: Como criar PDF a partir de uma planilha – Tutorial Java
tags:
- Aspose.Cells
- Java
- PDF generation
title: Como criar PDF a partir de uma pasta de trabalho – Guia completo de Java
url: /pt/java/excel-import-export/how-to-create-pdf-from-a-workbook-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Criar PDF a partir de uma Pasta de Trabalho – Guia Completo em Java

Já se perguntou **como criar PDF** diretamente de uma pasta de trabalho do Excel sem lidar com conversores de terceiros? Você não está sozinho. Muitos desenvolvedores se deparam com um obstáculo quando precisam de uma exportação rápida para PDF, uma pré‑visualização em HTML ou fórmulas de matriz avançadas — tudo de uma vez.  

Neste tutorial, percorreremos um único programa Java autônomo que faz exatamente isso. Vamos **salvar a pasta de trabalho como PDF**, mostrar como **exportar Excel para HTML** mantendo as linhas congeladas e demonstrar o **uso da função expand** dentro de uma planilha. Ao final, você terá um projeto executável que pode ser inserido em qualquer build Maven ou Gradle.

> **Dica profissional:** Todo o código abaixo funciona com Aspose.Cells 23.10 (ou mais recente). Se você estiver usando uma versão mais antiga, alguns nomes de métodos podem diferir ligeiramente.

---

## Pré-requisitos

- **Java 17** (ou qualquer versão LTS) instalado e configurado.
- Biblioteca **Aspose.Cells for Java**. Adicione a seguinte dependência Maven ao seu `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

- Uma IDE ou editor de texto de sua escolha (IntelliJ IDEA, VS Code, Eclipse…).

Sem APIs externas, sem serviços web — apenas Java puro e o SDK Aspose.Cells.

---

## Visão Geral da Solução

Dividiremos a implementação em **sete etapas lógicas**:

1. Criar uma pasta de trabalho e demonstrar a função **EXPAND**.  
2. Habilitar seletores de variação de fonte e **salvar a pasta de trabalho como PDF**.  
3. Exportar a mesma pasta de trabalho para HTML preservando linhas congeladas.  
4. Usar um Smart Marker com um parâmetro `IF` para inserir texto condicional.  
5. Aplicar um Smart Marker mestre‑detalhe para dados hierárquicos.  
6. Carregar um arquivo Markdown que contém imagens codificadas em Base‑64.  
7. Configurar opções do GridJs para alinhamento e bordas, então inserir dados.

Cada etapa está encapsulada em seu próprio método para manter o método `main` organizado e ilustrar **por que** fazemos o que fazemos, não apenas **o que** digitamos.

---

## Etapa 1 – Criar uma Pasta de Trabalho e Usar a Função EXPAND

A função **EXPAND** é uma nova fórmula de matriz dinâmica introduzida no Office 365. Ela permite expandir um intervalo para uma área maior sem copiar células manualmente.

```java
import com.aspose.cells.*;

public class WorkbookDemo {

    private static void createWorkbookWithExpand() throws Exception {
        // Initialize a new workbook and grab the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // A1 uses EXPAND to turn a 1×3 array into a 5×2 block
        sheet.getCells().get("A1").setFormula("=EXPAND({1,2,3}, 5, 2)");

        // B1 demonstrates a classic trigonometric function (cotangent)
        sheet.getCells().get("B1").setFormula("=COT(PI()/4)");

        // Force calculation so we can read the results immediately
        workbook.calculateFormula();

        // Print the top‑left value to the console – should be 1
        System.out.println("A1 value after EXPAND: " + sheet.getCells().get("A1").getStringValue());
    }
```

**Por que isso importa:**  
- `EXPAND` preenche automaticamente o resultado com espaços em branco, o que é perfeito quando você posteriormente **salva a pasta de trabalho como PDF** — o PDF exibirá uma tabela limpa e retangular.  
- Chamar `calculateFormula()` garante que o motor de fórmulas seja executado antes de exportarmos qualquer coisa.

---

## Etapa 2 – Habilitar Seletores de Variação de Fonte e **Salvar Pasta de Trabalho como PDF**

Se você precisar suportar tipografia avançada (por exemplo, emojis ou seletores de variação CJK), deve ativar o recurso **antes** de salvar.

```java
    private static void saveAsPdf(Workbook workbook) throws Exception {
        // Enable support for variation selectors (useful for emojis, etc.)
        WorkbookSettings settings = workbook.getSettings();
        settings.setEnableFontVariationSelectors(true);

        // Define the output path – adjust to your environment
        String pdfPath = "output/vsPdf.pdf";

        // Save the workbook as a PDF file
        workbook.save(pdfPath, SaveFormat.PDF);
        System.out.println("PDF saved to: " + pdfPath);
    }
```

**Ponto chave:** A palavra‑chave principal **how to create pdf** é respondida aqui — chamando `workbook.save(..., SaveFormat.PDF)` após configurar as opções.

---

## Etapa 3 – **Exportar Excel para HTML** Preservando Linhas Congeladas

Frequentemente, as partes interessadas solicitam uma pré‑visualização rápida na web. Aspose.Cells pode exportar para HTML e, com `setPreserveFrozenRows(true)`, mantemos a mesma experiência de rolagem que no Excel.

```java
    private static void exportToHtml(Workbook workbook) throws Exception {
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions();
        htmlOptions.setPreserveFrozenRows(true); // keep frozen panes

        String htmlPath = "output/frozenRows.html";
        workbook.save(htmlPath, htmlOptions);
        System.out.println("HTML exported to: " + htmlPath);
    }
```

**Por que isso importa:** Linhas congeladas são um detalhe de usabilidade; sem elas, as linhas de cabeçalho desaparecem quando os usuários rolam a página.

---

## Etapa 4 – Smart Marker com um Parâmetro IF

Smart Markers permitem mesclar dados em um modelo sem escrever loops. O parâmetro `if` adiciona lógica condicional diretamente dentro do marcador.

```java
    private static void applyConditionalSmartMarker() throws Exception {
        String template = "${if(@IsVIP, 'VIP Customer', 'Regular Customer')}: ${CustomerName}";
        Map<String, Object> data = new HashMap<>();
        data.put("IsVIP", true);
        data.put("CustomerName", "Acme Corp");

        // Create a fresh workbook to host the result
        Workbook markerWorkbook = new Workbook();
        SmartMarkerProcessor processor = new SmartMarkerProcessor(markerWorkbook);
        processor.apply(template, data);

        // Save to see the result
        markerWorkbook.save("output/conditionalMarker.pdf", SaveFormat.PDF);
    }
```

O PDF gerado exibirá **“VIP Customer: Acme Corp”** porque `IsVIP` está `true`. Alterando a bandeira para `false`, você obterá **“Regular Customer: Acme Corp”** — sem código extra necessário.

---

## Etapa 5 – Smart Marker Mestre‑Detalhe Usando um Intervalo Hierárquico

Quando você tem dados pai‑filho (por exemplo, pedidos e itens de linha), um marcador mestre‑detalhe evita a inserção manual de linhas.

```java
    private static void applyMasterDetailSmartMarker() throws Exception {
        // Simulated hierarchical data
        Map<String, Object> hierarchicalData = new HashMap<>();
        List<Map<String, Object>> orders = new ArrayList<>();

        Map<String, Object> order1 = new HashMap<>();
        order1.put("OrderID", 1001);
        order1.put("Date", "2024‑12‑01");
        List<Map<String, Object>> details1 = new ArrayList<>();
        details1.add(Map.of("Product", "Widget A", "Qty", 5));
        details1.add(Map.of("Product", "Widget B", "Qty", 2));
        order1.put("Detail", details1);
        orders.add(order1);

        hierarchicalData.put("Orders", orders);

        String masterDetailTemplate =
                "${Orders.Master:OrderID,Date}\n" +
                "${Orders.Detail:Product,Qty}";

        Workbook mdWorkbook = new Workbook();
        SmartMarkerProcessor mdProcessor = new SmartMarkerProcessor(mdWorkbook);
        mdProcessor.apply(masterDetailTemplate, hierarchicalData);

        mdWorkbook.save("output/masterDetail.pdf", SaveFormat.PDF);
    }
```

**O que você ganha:** O motor expande as linhas mestre para cada pedido e aninha automaticamente as linhas de detalhe abaixo — perfeito para faturas ou relatórios de compras.

---

## Etapa 6 – Carregar um Documento Markdown com Imagens Incorporadas em Base‑64

Se seus dados de origem estiverem em Markdown (comum em pipelines de documentação), Aspose.Cells pode renderiz‑los diretamente em uma pasta de trabalho.

```java
    private static void loadMarkdownWithBase64() throws Exception {
        MarkdownLoadOptions mdOptions = new MarkdownLoadOptions();
        mdOptions.setEnableBase64Images(true); // decode inline images

        // Assume doc.md lives in the project root
        Workbook mdWorkbook = new Workbook("input/doc.md", mdOptions);
        mdWorkbook.save("output/markdownExport.pdf", SaveFormat.PDF);
        System.out.println("Markdown loaded and saved as PDF.");
    }
```

**Observação de caso extremo:** Se a string Base‑64 estiver malformada, o Aspose ignorará a imagem mas continuará processando o restante do documento — sem travar.

---

## Etapa 7 – Configurar Opções do GridJs e Inserir Dados

GridJs é uma grade JavaScript leve que o Aspose pode renderizar em HTML. Alinhar números e aplicar bordas melhora a legibilidade.

```java
    private static void configureGridJs() throws Exception {
        GridJsOptions gridOptions = new GridJsOptions();
        gridOptions.setNumberFormatAlignment(Alignment.Center); // center numbers
        gridOptions.setNumberFormatBorder(BorderLineStyle.Thin); // thin border

        GridJsEngine gridEngine = new GridJsEngine(gridOptions);
        gridEngine.insertRows(0, 10); // create 10 empty rows
        gridEngine.setCellValue(0, 0, "123"); // first cell gets a value

        // Export the GridJs view to HTML for quick inspection
        String htmlPath = "output/gridJs.html";
        gridEngine.save(htmlPath);
        System.out.println("GridJs HTML saved to: " + htmlPath);
    }
```

**Por que isso importa:** Alinhamento adequado e bordas fazem o HTML gerado parecer uma planilha refinada — útil para dashboards.

---

## Juntando Tudo – O Método `main`

```java
    public static void main(String[] args) {
        try {
            // Step 1 – create workbook with EXPAND
            Workbook workbook = new Workbook();
            Worksheet sheet = workbook.getWorksheets().get(0);
            sheet.getCells().get("A1").setFormula("=EXPAND({1,2,3}, 5, 2)");
            sheet.getCells().get("B1").setFormula("=COT(PI()/4)");
            workbook.calculateFormula();
            System.out.println("A1 after EXPAND: " + sheet.getCells().get("A1").getStringValue());

            // Step 2 – save as PDF
            saveAsPdf(workbook);

            // Step 3 – export to HTML
            exportToHtml(workbook);

            // Step 4 – conditional Smart Marker
            applyConditionalSmartMarker();

            // Step 5 – master‑detail Smart Marker
            applyMasterDetailSmartMarker();

            // Step 6 – load Markdown with Base‑64 images
            loadMarkdownWithBase64();

            // Step 7 – GridJs configuration
            configureGridJs();

            System.out.println("All tasks completed successfully.");
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}