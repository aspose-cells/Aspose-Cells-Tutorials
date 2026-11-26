---
category: general
date: 2026-11-25
description: Criar exemplo de código Java que gera uma pasta de trabalho Excel usando
  marcadores inteligentes do Aspose.Cells para vincular arrays JSON como valores únicos.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook java
- Aspose.Cells smart marker
- Java JSON to Excel
- setSmartMarkerData
- Excel export Java
language: pt
lastmod: 2026-11-25
og_description: Crie uma planilha Excel em Java com Aspose.Cells para exportar facilmente
  arrays JSON como células individuais. Siga o guia passo a passo.
og_image_alt: Screenshot of an Excel workbook created in Java using Aspose.Cells smart
  markers
og_title: Criar pasta de trabalho Excel Java – Guia de marcador inteligente Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: Create Excel workbook Java code example using Aspose.Cells smart markers
    to bind JSON arrays as single values.
  headline: How to create Excel workbook Java with Aspose.Cells markers
  type: TechArticle
- description: Create Excel workbook Java code example using Aspose.Cells smart markers
    to bind JSON arrays as single values.
  name: How to create Excel workbook Java with Aspose.Cells markers
  steps:
  - name: '**Creates a fresh workbook** – `new Workbook()` gives you an in‑memory
      Excel file with a default sheet.'
    text: '**Creates a fresh workbook** – `new Workbook()` gives you an in‑memory
      Excel file with a default sheet.'
  - name: '**Places a smart marker in cell A1** – `{{jsonArray:ArrayAsSingle}}` tells
      Aspose.Cells to replace the marker with the *entire* array, joined by commas.'
    text: '**Places a smart marker in cell A1** – `{{jsonArray:ArrayAsSingle}}` tells
      Aspose.Cells to replace the marker with the *entire* array, joined by commas.'
  - name: '**Builds a `Map` data source** – The key `"jsonArray"` matches the marker
      name; the value is a `String[]`.'
    text: '**Builds a `Map` data source** – The key `"jsonArray"` matches the marker
      name; the value is a `String[]`.'
  - name: '**Calls `setSmartMarkerData`** – This binds the map to the marker and performs
      the replacement.'
    text: '**Calls `setSmartMarkerData`** – This binds the map to the marker and performs
      the replacement.'
  - name: '**Saves the file** – `workbook.save(...)` writes `JsonSingleValue.xlsx`
      to disk.'
    text: '**Saves the file** – `workbook.save(...)` writes `JsonSingleValue.xlsx`
      to disk.'
  - name: Open `JsonSingleValue.xlsx` in Microsoft Excel, LibreOffice Calc, or Google
      Sheets.
    text: Open `JsonSingleValue.xlsx` in Microsoft Excel, LibreOffice Calc, or Google
      Sheets.
  - name: Confirm that cell **A1** reads `One, Two, Three`.
    text: Confirm that cell **A1** reads `One, Two, Three`.
  - name: Check that no extra rows or columns were added – the smart marker performed
      an in‑place replacement.
    text: Check that no extra rows or columns were added – the smart marker performed
      an in‑place replacement.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Como criar uma pasta de trabalho Excel em Java com marcadores Aspose.Cells
url: /pt/java/templates-reporting/how-to-create-excel-workbook-java-with-aspose-cells-markers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como criar uma pasta de trabalho Excel Java com marcadores Aspose.Cells

Se você precisa **criar uma pasta de trabalho Excel Java** que escreva um array JSON em uma única célula, este tutorial mostra exatamente como fazer. Usando marcadores inteligentes do Aspose.Cells, você pode tratar um array inteiro como um único valor, evitando loops manuais e gravações célula por célula.

Você aprenderá como configurar uma pasta de trabalho, definir um marcador inteligente, vincular uma fonte de dados `Map` que contém um array no estilo JSON e, finalmente, salvar o arquivo. O exemplo funciona com Java 17+, Maven e a biblioteca de avaliação gratuita do Aspose.Cells for Java.

---

![Screenshot of an Excel workbook created in Java using Aspose.Cells smart markers](excel-workbook-java.png){: .center-image alt="Captura de tela de uma pasta de trabalho Excel criada em Java usando marcadores inteligentes do Aspose.Cells"}

## Pré-requisitos

| Requisito | Por que é importante |
|-------------|----------------|
| Java 17 ou superior | Os recursos mais recentes da linguagem e atualizações de segurança |
| Maven 3.6+ | Simplifica o gerenciamento de dependências |
| Aspose.Cells for Java (v23.12 ou mais recente) | Fornece as APIs `Workbook`, `Worksheet` e smart‑marker usadas no exemplo |
| Conhecimento básico de coleções Java | Você criará um `Map<String, Object>` que atua como a fonte de dados |

Adicione a dependência do Aspose.Cells ao seu `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
    <classifier>jdk17</classifier>
</dependency>
```

---

## Criar pasta de trabalho Excel Java – exemplo completo

O programa a seguir é uma solução **completa e executável**. Copie-o para um arquivo chamado `ExcelSmartMarkerDemo.java`, compile e execute.

```java
package com.example.excel;

import com.aspose.cells.*;
import java.util.HashMap;
import java.util.Map;

/**
 * Demonstrates how to create Excel workbook Java using Aspose.Cells smart markers.
 * The smart marker "{{jsonArray:ArrayAsSingle}}" treats the whole array as a single cell value.
 */
public class ExcelSmartMarkerDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();                       // empty workbook
        Worksheet worksheet = workbook.getWorksheets().get(0);    // first (default) sheet

        // Step 2: Define a smart marker that treats a JSON array as a single value
        // The "ArrayAsSingle" option concatenates the array elements with commas.
        String smartMarker = "{{jsonArray:ArrayAsSingle}}";
        worksheet.getCells().get("A1").putValue(smartMarker);

        // Step 3: Prepare the data source – a simple string array
        Map<String, Object> dataSource = new HashMap<>();
        dataSource.put("jsonArray", new String[] { "One", "Two", "Three" });

        // Step 4: Bind the data to the smart marker and save the workbook
        worksheet.getCells().get("A1").setSmartMarkerData(dataSource);
        workbook.save("JsonSingleValue.xlsx");   // workbook saved to project root
        System.out.println("Workbook created successfully.");
    }
}
```

### O que o código faz

1. **Cria uma nova pasta de trabalho** – `new Workbook()` fornece um arquivo Excel em memória com uma planilha padrão.  
2. **Coloca um marcador inteligente na célula A1** – `{{jsonArray:ArrayAsSingle}}` indica ao Aspose.Cells que substitua o marcador pelo *array inteiro*, unido por vírgulas.  
3. **Constrói uma fonte de dados `Map`** – A chave `"jsonArray"` corresponde ao nome do marcador; o valor é um `String[]`.  
4. **Chama `setSmartMarkerData`** – Isso vincula o mapa ao marcador e realiza a substituição.  
5. **Salva o arquivo** – `workbook.save(...)` grava `JsonSingleValue.xlsx` no disco.

Ao abrir o arquivo Excel gerado, a célula **A1** contém:

```
One, Two, Three
```

O array é renderizado como uma única string separada por vírgulas devido à opção `ArrayAsSingle`.

---

## Usando marcadores inteligentes do Aspose.Cells para vincular dados JSON

Os marcadores inteligentes do Aspose.Cells são uma forma poderosa de mapear objetos complexos (incluindo estruturas semelhantes a JSON) diretamente nas planilhas. A sintaxe `{{fieldName:Option}}` funciona como um motor de templates:

* **fieldName** – a chave na sua fonte de dados (`Map`, POJO ou `DataTable`).  
* **Option** – controla como as coleções são tratadas. `ArrayAsSingle` trata toda a coleção como um único valor; outras opções como `Array` expandiriam o array ao longo das linhas.

**Por que usar um marcador inteligente em vez de um loop?**  
Um loop requer cálculos manuais de endereços de células, indexação propensa a erros e código extra para estilização. Marcadores inteligentes permitem escrever marcadores declarativos, manter seu código Java curto e deixar a biblioteca lidar com os detalhes de layout.

---

## Configurando a fonte de dados Java Map

O `Map<String, Object>` é o contêiner de dados mais simples para o Aspose.Cells:

```java
Map<String, Object> dataSource = new HashMap<>();
dataSource.put("jsonArray", new String[] { "One", "Two", "Three" });
```

*A chave (`jsonArray`) deve corresponder exatamente ao nome do marcador.*

Você também pode usar um `List<String>`, um POJO personalizado ou até um `Map` aninhado para estruturas JSON mais complexas. O Aspose.Cells percorrerá o grafo de objetos automaticamente.

**Dica:** Se precisar formatar a string concatenada de forma diferente (por exemplo, usando ponto‑e‑vírgula), pré‑procese o array em Java antes de atribuí‑lo ao mapa:

```java
String joined = String.join(";", new String[] {"One","Two","Three"});
dataSource.put("jsonArray", new String[] { joined });
```

---

## Salvando a pasta de trabalho e verificando a saída

```java
workbook.save("JsonSingleValue.xlsx");
```

O método `save` suporta vários formatos (`.xlsx`, `.xls`, `.csv`, `.pdf`). Para este tutorial, mantemos o formato padrão Excel Open XML.

**Etapas de verificação**

1. Abra `JsonSingleValue.xlsx` no Microsoft Excel, LibreOffice Calc ou Google Sheets.  
2. Confirme que a célula **A1** contém `One, Two, Three`.  
3. Verifique se não foram adicionadas linhas ou colunas extras – o marcador inteligente realizou a substituição no local.

Se a célula mostrar o texto bruto do marcador (`{{jsonArray:ArrayAsSingle}}`), verifique novamente que:

* O nome do marcador corresponde exatamente à chave do mapa (sensível a maiúsculas/minúsculas).  
* `setSmartMarkerData` é chamado **depois** que o marcador é colocado.  
* A versão do Aspose.Cells suporta a opção `ArrayAsSingle` (disponível desde v20.3).

---

## Variações comuns e casos extremos

| Cenário | Ajuste |
|----------|------------|
| **Delimitador diferente** | Use `ArrayAsSingle` junto com um join customizado em Java (veja a dica acima). |
| **Múltiplos arrays em uma planilha** | Coloque marcadores adicionais como `{{anotherArray:ArrayAsSingle}}` em outras células e adicione entradas correspondentes ao mapa. |
| **Objetos JSON aninhados** | Forneça um `Map<String, Object>` aninhado; referencie campos com notação de ponto (`{{parent.child}}`). |
| **Conjuntos de dados grandes** | Para milhares de linhas, prefira a opção `Array` para permitir que o Aspose.Cells expanda as linhas automaticamente, o que |

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Como criar e exportar Excel para HTML usando Aspose.Cells Java | Guia de Operações de Pasta de Trabalho](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Exportar Pasta de Trabalho Excel como Imagem usando Aspose.Cells para Java: Um Guia Passo a Passo](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [Como criar e salvar uma Pasta de Trabalho Excel como SVG usando Aspose.Cells para Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}