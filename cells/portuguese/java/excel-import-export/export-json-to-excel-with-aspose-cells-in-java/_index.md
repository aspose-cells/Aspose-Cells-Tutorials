---
category: general
date: 2026-09-18
description: Exportar JSON para Excel usando Aspose.Cells em Java. Aprenda a inserir
  JSON no Excel, converter JSON para Excel e salvar a pasta de trabalho como XLSX.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export json to excel
- insert json into excel
- how to insert json
- convert json to excel
- save workbook as xlsx
language: pt
lastmod: 2026-09-18
og_description: Exportar JSON para Excel usando Aspose.Cells para Java. Tutorial passo
  a passo mostra como inserir JSON no Excel, converter JSON para Excel e salvar a
  pasta de trabalho como XLSX.
og_image_alt: Aspose.Cells Java code inserting JSON array into a single Excel cell
og_title: Exportar JSON para Excel com Aspose.Cells – Guia Java
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Export JSON to Excel using Aspose.Cells in Java. Learn to insert JSON
    into Excel, convert JSON to Excel, and save workbook as XLSX.
  headline: Export JSON to Excel with Aspose.Cells in Java
  type: TechArticle
- description: Export JSON to Excel using Aspose.Cells in Java. Learn to insert JSON
    into Excel, convert JSON to Excel, and save workbook as XLSX.
  name: Export JSON to Excel with Aspose.Cells in Java
  steps:
  - name: Prepare your development environment.
    text: Prepare your development environment.
  - name: Define the JSON data source.
    text: Define the JSON data source.
  - name: Create a workbook and worksheet.
    text: Create a workbook and worksheet.
  - name: Insert JSON into Excel using a Smart Marker.
    text: Insert JSON into Excel using a Smart Marker.
  - name: Process the Smart Marker so the JSON appears in a single cell.
    text: Process the Smart Marker so the JSON appears in a single cell.
  - name: Save the workbook as an XLSX file.
    text: Save the workbook as an XLSX file.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Exportar JSON para Excel com Aspose.Cells em Java
url: /pt/java/excel-import-export/export-json-to-excel-with-aspose-cells-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exportar JSON para Excel com Aspose.Cells em Java

Se você precisa **exportar JSON para Excel**, este guia mostra uma solução completa usando Aspose.Cells para Java. Você verá exatamente como inserir JSON no Excel, converter JSON para Excel e, finalmente, **salvar a pasta de trabalho como XLSX** sem sair do seu IDE.

Trabalhar com dados JSON é comum ao criar APIs, painéis de relatórios ou ferramentas de migração de dados. Em vez de copiar‑colar manualmente, a abordagem abaixo automatiza todo o pipeline para que você possa gerar arquivos Excel programaticamente.

## Exportar JSON para Excel – guia passo a passo

As seções a seguir conduzem você por cada etapa necessária:

1. Prepare seu ambiente de desenvolvimento.  
2. Defina a fonte de dados JSON.  
3. Crie uma pasta de trabalho e uma planilha.  
4. Insira JSON no Excel usando um Smart Marker.  
5. Processe o Smart Marker para que o JSON apareça em uma única célula.  
6. Salve a pasta de trabalho como um arquivo XLSX.

Ao final deste tutorial você terá um programa Java executável que produz um arquivo `JsonExport.xlsx` contendo o array JSON na célula **A1**.

## Pré‑requisitos

- Java Development Kit 8 ou superior.  
- Maven ou Gradle para gerenciar dependências.  
- Aspose.Cells para Java (a versão mais recente no momento da escrita, 24.10).  
- Conhecimento básico de sintaxe Java e formato JSON.

> **Pro tip:** Aspose.Cells é uma biblioteca comercial, mas uma licença de avaliação gratuita funciona para desenvolvimento e testes.

## Etapa 1: Configurar seu projeto Java

Adicione a dependência Aspose.Cells ao seu `pom.xml` (Maven) ou `build.gradle` (Gradle).

**Maven**

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version>
</dependency>
```

**Gradle**

```groovy
implementation 'com.aspose:aspose-cells:24.10'
```

Depois que a dependência for resolvida, você pode importar as classes necessárias:

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
import com.aspose.cells.SmartMarkerException;
```

## Etapa 2: Definir a fonte de dados JSON

A string JSON representa um array de objetos. Em um projeto real você pode ler isso de um arquivo, de um endpoint REST ou de um banco de dados. Para ilustração, incorporamos o JSON diretamente no código.

```java
// Step 2: Define the JSON data source (an array of objects)
String jsonData = "[{\"Name\":\"John\",\"Score\":85},{\"Name\":\"Anna\",\"Score\":92}]";
```

**Por que isso importa:** Aspose.Cells pode tratar um array JSON como uma única célula quando você usa a opção `ArrayAsSingle`. Isso evita a necessidade de dividir o array em linhas e colunas, o que é ideal para exportar cargas JSON brutas.

## Etapa 3: Criar uma pasta de trabalho e obter a primeira planilha

Um objeto `Workbook` representa o arquivo Excel completo. A primeira planilha (índice 0) é onde colocaremos o JSON.

```java
// Step 3: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```

**Explicação:** Instanciar `Workbook` sem parâmetros cria uma pasta de trabalho vazia com uma planilha padrão. Você pode adicionar mais planilhas posteriormente, se seu cenário exigir múltiplos conjuntos de dados.

## Etapa 4: Inserir JSON no Excel usando um Smart Marker

Smart Markers são marcadores de posição que o Aspose.Cells substitui por dados em tempo de execução. O marcador `&=jsonArray(ArrayAsSingle)` indica ao motor que escreva todo o array JSON em uma única célula.

```java
// Step 4: Insert a Smart Marker that tells Aspose.Cells to treat the JSON array as a single cell
worksheet.getCells().putValue(0, 0, "&=jsonArray(ArrayAsSingle)");
```

**Por que usar um Smart Marker?** Ele abstrai a lógica de vinculação de dados, permitindo que você se concentre no formato de origem (JSON) em vez de manipular células de baixo nível.

## Etapa 5: Associar o nome do Smart Marker aos dados JSON

É necessário vincular o identificador do marcador (`jsonArray`) à string JSON real.

```java
// Step 5: Associate the Smart Marker name with the JSON data
workbook.getSmartMarkers().setDataSource("jsonArray", jsonData);
```

**Observação:** O método `setDataSource` aceita qualquer objeto que o motor de Smart Marker possa serializar, incluindo strings JSON, coleções Java ou DataTables.

## Etapa 6: Processar os Smart Markers para que o array JSON seja escrito na célula

Chamar `processSmartMarkers()` aciona a substituição do marcador pelo JSON vinculado.

```java
// Step 6: Process the Smart Markers so the JSON array is written into the cell
workbook.processSmartMarkers();
```

Se o JSON estiver malformado, o Aspose.Cells lançará uma `SmartMarkerException`. Envolva a chamada em um bloco try‑catch para maior robustez em produção.

## Etapa 7: Salvar a pasta de trabalho como um arquivo XLSX

Por fim, grave a pasta de trabalho no disco. A extensão do arquivo determina o formato de saída; usar `.xlsx` garante o formato moderno Office Open XML.

```java
// Step 7: Save the workbook to a file
String outputPath = "YOUR_DIRECTORY/JsonExport.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to " + outputPath);
```

**Resultado:** Abrir `JsonExport.xlsx` mostra o array JSON exatamente como aparece em `jsonData`, localizado na célula **A1**.

## Exemplo completo executável

Abaixo está uma classe Java autônoma que você pode copiar, colar e executar.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
import com.aspose.cells.SmartMarkerException;

/**
 * Demonstrates how to export JSON to Excel using Aspose.Cells.
 * The program inserts a JSON array into a single cell and saves the workbook as XLSX.
 */
public class JsonToExcelExporter {
    public static void main(String[] args) {
        // 1. Define the JSON data source (an array of objects)
        String jsonData = "[{\"Name\":\"John\",\"Score\":85},{\"Name\":\"Anna\",\"Score\":92}]";

        try {
            // 2. Create a new workbook and obtain the first worksheet
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.getWorksheets().get(0);

            // 3. Insert a Smart Marker that treats the JSON array as a single cell
            worksheet.getCells().putValue(0, 0, "&=jsonArray(ArrayAsSingle)");

            // 4. Bind the Smart Marker name to the JSON string
            workbook.getSmartMarkers().setDataSource("jsonArray", jsonData);

            // 5. Process Smart Markers – this writes the JSON into cell A1
            workbook.processSmartMarkers();

            // 6. Save the workbook as an XLSX file
            String outputPath = "JsonExport.xlsx";
            workbook.save(outputPath);
            System.out.println("Workbook saved to " + outputPath);
        } catch (SmartMarkerException e) {
            System.err.println("Error processing Smart Markers: " + e.getMessage());
        } catch (Exception e) {
            System.err.println("Unexpected error: " + e.getMessage());
        }
    }
}
```

### Saída esperada

Ao executar o programa, ele imprime:

```
Workbook saved to JsonExport.xlsx
```

Abrindo **JsonExport.xlsx** mostra a célula **A1** contendo:

```
[{"Name":"John","Score":85},{"Name":"Anna","Score":92}]
```

## Variações comuns e casos de borda

| Situação | Como adaptar o código |
|----------|------------------------|
| **Carga JSON grande** ( > 1 MB) | Aumente o tamanho do heap JVM (`-Xmx2g`) para evitar `OutOfMemoryError`. |
| **Múltiplos objetos JSON** que precisam de linhas separadas | Use `ArrayAsRows` em vez de `ArrayAsSingle` e mapeie o marcador para uma coleção de POJOs. |
| **Salvar como CSV** | Substitua `workbook.save(outputPath)` por `workbook.save(outputPath, com.aspose.cells.SaveFormat.CSV);`. |
| **Adicionar uma linha de cabeçalho** | Escreva uma string estática em `worksheet.getCells().putValue(0, 0, "JSON Payload");` antes de inserir o Smart Marker. |
| **Usar um diretório diferente** | Certifique‑se de que o diretório exista ou crie‑o com `new java.io.File(dir).mkdirs();`. |

## Dicas para uso em produção

- **Valide o JSON** antes de passá‑lo ao Aspose.Cells para evitar exceções em tempo de execução.  
- **Use try‑with‑resources** para quaisquer streams que você abrir ao ler JSON de fontes externas.  
- **Bloqueie a pasta de trabalho** se múltiplas threads puderem escrever no mesmo arquivo simultaneamente.  
- **Registro de licença**: chame `com.aspose.cells.License license = new com.aspose.cells.License(); license.setLicense("Aspose.Cells.lic");` na inicialização da aplicação.

## Próximos passos

Agora que você pode **exportar JSON para Excel**, considere explorar capacidades relacionadas:

- **Inserir JSON no Excel** com formatação: aplique estilos de célula após processar o Smart Marker.  
- **Converter JSON para tabelas Excel**: mapeie objetos JSON para linhas e colunas

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [Import JSON Data into Excel Using Aspose.Cells Java&#58; A Comprehensive Guide](/cells/english/java/import-export/import-json-data-excel-aspose-cells-java/)
- [How to Insert Multiple Rows into Excel Using Aspose.Cells for Java](/cells/english/java/cell-operations/excel-automation-aspose-cells-java-insert-multiple-rows/)
- [How to Insert Images into Excel Using Java and Aspose.Cells](/cells/english/java/images-shapes/insert-image-into-excel-java-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}