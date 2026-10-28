---
category: general
date: 2026-03-01
description: Aprenda como incorporar fontes em HTML e outros formatos. Tutorial passo
  a passo cobrindo incorporação de fontes em HTML, conversão de Excel para HTML, como
  exportar OLE e conversão de Excel para XPS.
draft: false
keywords:
- how to embed fonts
- embed fonts in html
- convert excel to html
- how to export ole
- convert excel to xps
language: pt
og_description: Como incorporar fontes em exportações HTML, XPS e OLE. Aprenda todo
  o fluxo de trabalho, veja código Java executável e domine a incorporação de fontes
  em HTML para conversões de Excel.
og_title: Como Incorporar Fontes – Tutorial Completo de Java
tags:
- Aspose.Cells
- Java
- Document Export
title: Como Incorporar Fontes – Guia Completo para Exportação em HTML, XPS e OLE
url: /pt/java/ole-objects-embedded-content/how-to-embed-fonts-complete-guide-for-html-xps-and-ole-expor/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Incorporar Fontes – Guia Completo para HTML, XPS e Exportação OLE

Já se perguntou **como incorporar fontes** ao transformar uma pasta de trabalho do Excel em uma página da web ou em um documento imprimível? Você não está sozinho. Muitos desenvolvedores se deparam com um obstáculo quando a saída parece correta na sua máquina, mas falha em outra porque as fontes necessárias estão ausentes.  

Neste tutorial, percorreremos um cenário real usando Aspose.Cells for Java: incorporaremos fontes em HTML, preservaremos os seletores de variação de emoji ao converter para XPS e até manteremos um objeto OLE editável ao exportar para PPTX. Ao final, você terá uma solução robusta, pronta para copiar e colar, que responde a “como incorporar fontes” e também aborda **embed fonts in html**, **convert excel to html**, **how to export ole**, e **convert excel to xps**.

## Pré-requisitos

- Java 17 (ou qualquer JDK recente)  
- Aspose.Cells for Java 25.x ou posterior  
- Uma IDE de desenvolvimento (IntelliJ IDEA, Eclipse ou VS Code)  
- Familiaridade básica com estruturas de dados do Excel  

Não são necessários serviços externos—tudo roda localmente.

## Visão Geral da Solução

1. **Criar uma pasta de trabalho** e usar a função `WRAPCOLS` para transformar um intervalo vertical em um layout de três colunas.  
2. **Salvar a pasta de trabalho como XPS** ativando os seletores de variação de fonte para que os emojis permaneçam intactos.  
3. **Exportar para HTML** com fontes incorporadas, garantindo que a página tenha a mesma aparência em qualquer lugar.  
4. **Exportar uma pasta de trabalho contendo um objeto OLE para PPTX**, preservando a editabilidade.  
5. **Aplicar um modelo Smart Marker** que demonstra a vinculação de dados mestre‑detalhe.  

Cada passo está isolado em sua própria seção H2, facilitando a leitura rápida tanto para mecanismos de busca quanto para assistentes de IA.

![Ilustração de como incorporar fontes](image.png "como incorporar fontes")

*Texto alternativo da imagem: diagrama de como incorporar fontes mostrando o fluxo de trabalho do Excel para HTML, XPS e PPTX.*

---

## Etapa 1 – Criar uma Pasta de Trabalho e Usar WRAPCOLS (Por que Isso Importa para embed fonts in html)

Antes de falarmos sobre incorporação de fontes, precisamos de uma pasta de trabalho que realmente contenha dados. A função `WRAPCOLS` é uma maneira prática de dividir uma única coluna em várias colunas, o que frequentemente torna o HTML final mais legível.

```java
import com.aspose.cells.*;

public class EmbedFontsDemo {
    public static void main(String[] args) throws Exception {
        // Initialize a new workbook
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Populate A2:A10 with sample data
        for (int i = 2; i <= 10; i++) {
            sheet.getCells().get("A" + i).putValue("Item " + (i - 1));
        }

        // Use WRAPCOLS to create a 3‑column block starting at A1
        Cell resultCell = sheet.getCells().get("A1");
        resultCell.setFormula("=WRAPCOLS(A2:A10,3)");
        workbook.calculateFormula();

        System.out.println("WRAPCOLS result: " + resultCell.getStringValue());
        // -----------------------------------------------------------------
        // The rest of the steps are demonstrated after this point.
        // -----------------------------------------------------------------
```

**Por que este passo?**  
A chamada `WRAPCOLS` gera um intervalo de múltiplas colunas que depois aparece no HTML como uma tabela. Quando posteriormente **incorporamos fontes em html**, o estilo da tabela dependerá das fontes que incorporamos, garantindo renderização consistente em todos os navegadores.

---

## Etapa 2 – Salvar a Pasta de Trabalho como XPS Preservando Emoji (convert excel to xps)

Se você precisa de um formato pronto para impressão, XPS é uma escolha sólida. No entanto, documentos modernos frequentemente contêm emojis ou símbolos que utilizam seletores de variação. Ativar `EnableFontVariationSelectors` garante que esses caracteres sobrevivam à conversão.

```java
        // --------------------------------------------------------------
        // Step 2: Save as XPS with font variation selectors enabled
        // --------------------------------------------------------------
        WorkbookSettings settings = workbook.getSettings();
        settings.setEnableFontVariationSelectors(true); // crucial for emoji

        String xpsPath = "output/withVariations.xps";
        workbook.save(xpsPath, SaveFormat.XPS);
        System.out.println("Workbook saved as XPS at: " + xpsPath);
```

**O que você obtém:**  
Um arquivo XPS que exibe qualquer emoji incorporado exatamente como na pasta de trabalho original. Isso atende ao requisito **convert excel to xps** e demonstra que o tratamento de fontes não se limita ao HTML.

---

## Etapa 3 – Exportar para HTML com Fontes Incorporadas (how to embed fonts & embed fonts in html)

Agora chegamos ao núcleo do tutorial: **como incorporar fontes** ao converter Excel para HTML. Aspose.Cells nos permite incorporar as fontes diretamente no arquivo HTML gerado, eliminando a necessidade de arquivos de fonte externos.

```java
        // --------------------------------------------------------------
        // Step 3: Export to HTML with embedded fonts
        // --------------------------------------------------------------
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions();
        htmlOptions.setEmbedFonts(true); // this is the key line for embed fonts in html
        htmlOptions.setExportImagesAsBase64(true); // optional, keeps all assets in one file

        String htmlPath = "output/embeddedFonts.html";
        workbook.save(htmlPath, htmlOptions);
        System.out.println("HTML with embedded fonts saved at: " + htmlPath);
```

**Como funciona:**  
`setEmbedFonts(true)` indica ao renderizador que ele deve ler os arquivos de fonte usados na pasta de trabalho e incorporá‑los como regras `@font-face` codificadas em Base64 dentro da tag `<style>`. O HTML resultante é autônomo, de modo que você pode colocá‑lo em qualquer servidor e as fontes serão renderizadas corretamente — exatamente o que os desenvolvedores procuram quando buscam **how to embed fonts**.

**Trecho de saída esperado (dentro de `embeddedFonts.html`):**

```html
<style>
@font-face{font-family:"Arial";src:url(data:font/ttf;base64,AAEAAA... ) format('truetype');}
</style>
<table>
  <tr><td>Item 1</td><td>Item 4</td><td>Item 7</td></tr>
  <tr><td>Item 2</td><td>Item 5</td><td>Item 8</td></tr>
  <tr><td>Item 3</td><td>Item 6</td><td>Item 9</td></tr>
</table>
```

Observe a regra `@font-face` — esta é a resposta concreta para **embed fonts in html**.

---

## Etapa 4 – Exportar uma Pasta de Trabalho Contendo um Objeto OLE para PPTX (how to export ole)

Muitos relatórios empresariais incorporam documentos Word, PDFs ou outras planilhas Excel como objetos OLE. Ao exportar essa pasta de trabalho para PowerPoint, costuma‑se perder a capacidade de editar esse objeto. Aspose.Cells preserva a editabilidade prontamente.

```java
        // --------------------------------------------------------------
        // Step 4: Export a workbook with an OLE object to PPTX
        // --------------------------------------------------------------
        // Load a workbook that already contains an OLE object.
        Workbook oleWorkbook = new Workbook("input/oleObject.xlsx");

        String pptxPath = "output/oleEditable.pptx";
        oleWorkbook.save(pptxPath, SaveFormat.PPTX);
        System.out.println("PPTX with editable OLE object saved at: " + pptxPath);
```

**Por que isso importa:**  
Se você está procurando **how to export ole**, este trecho mostra a chamada de API exata. O slide resultante do PowerPoint contém o objeto OLE como um componente ativo, de duplo clique para editar — sem necessidade de pós‑processamento adicional.

---

## Etapa 5 – Aplicar um Modelo Smart Marker (master‑detail) e Finalizar a Demonstração

Smart Markers permitem vincular uma fonte de dados (Map, JSON, DataTable) diretamente a um modelo Excel. Aqui está um exemplo mínimo que imprime linhas mestre‑detalhe.

```java
        // --------------------------------------------------------------
        // Step 5: Apply Smart Marker template (master‑detail)
        // --------------------------------------------------------------
        String smartMarkerTemplate = "${Orders.Master:OrderID,Customer}\n${Orders.Detail:Product,Qty,Price}";
        // Simulated data source
        java.util.Map<String, Object> dataSource = new java.util.HashMap<>();
        java.util.List<java.util.Map<String, Object>> master = new java.util.ArrayList<>();
        java.util.Map<String, Object> masterRow = new java.util.HashMap<>();
        masterRow.put("OrderID", 1001);
        masterRow.put("Customer", "Acme Corp");
        master.add(masterRow);
        dataSource.put("Orders.Master", master);

        java.util.List<java.util.Map<String, Object>> detail = new java.util.ArrayList<>();
        java.util.Map<String, Object> detailRow = new java.util.HashMap<>();
        detailRow.put("Product", "Widget");
        detailRow.put("Qty", 5);
        detailRow.put("Price", 9.99);
        detail.add(detailRow);
        dataSource.put("Orders.Detail", detail);

        SmartMarkerProcessor processor = new SmartMarkerProcessor(new Workbook());
        processor.apply(smartMarkerTemplate, dataSource);
        processor.getWorkbook().save("output/smartMarkerResult.xlsx");
        System.out.println("Smart Marker workbook saved.");
    }
}
```

**O que você vê:**  
Uma nova pasta de trabalho (`smartMarkerResult.xlsx`) onde os marcadores de posição do modelo são substituídos pelos dados. Esta etapa não trata diretamente de fontes, mas completa o tutorial ao mostrar um fluxo de trabalho típico de relatórios que frequentemente precede uma exportação **embed fonts in html**.

---

## Armadilhas Comuns & Dicas Profissionais (Garantindo a Incorporação Bem‑sucedida de Fontes)

| Problema | Por que acontece | Correção |
|----------|------------------|----------|
| As fontes estão ausentes no arquivo HTML | A pasta de trabalho usa uma fonte do sistema que não está instalada no servidor. | Use `Workbook.getSettings().setDefaultFont("Arial")` antes de carregar os dados, ou incorpore manualmente os arquivos de fonte necessários. |
| O HTML de saída é enorme | Incorporar muitas fontes grandes aumenta o tamanho do arquivo. | Limite a incorporação apenas às fontes que você realmente usa: `htmlOptions.setFontEmbeddingMode(HtmlFontEmbeddingMode.EmbedSubset)`. |
| Emojis desaparecem após a conversão para XPS | Os seletores de variação são removidos por padrão. | Ative `settings.setEnableFontVariationSelectors(true)` conforme mostrado na Etapa 2. |
| O objeto OLE torna‑se uma imagem estática no PPTX | A pasta de trabalho de origem foi salva com `setSuppressOLEObjects(true)`. | Certifique‑se de **não** suprimir objetos OLE ao salvar para PPTX. |

---

## Verificando os Resultados

1. Abra `embeddedFonts.html` no Chrome/Firefox. A tabela deve ser exibida usando a fonte incorporada (por exemplo, Arial) mesmo que essa fonte não esteja instalada na máquina.  
2. Abra `withVariations.xps` no Visualizador XPS do Windows. Emojis como 👍 devem ser renderizados corretamente.  
3. Abra `oleEditable.pptx` no PowerPoint. Clique duas vezes na forma OLE;

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}