---
category: general
date: 2026-06-21
description: Salvar a pasta de trabalho como XLSX usando SmartMarkerProcessor para
  gerar XLSX a partir de JSON e preencher facilmente o Excel com dados JSON.
draft: false
keywords:
- save workbook as xlsx
- generate xlsx from json
- populate excel from json
language: pt
og_description: Salve a pasta de trabalho como XLSX com um único trecho de código
  Java. Aprenda como gerar XLSX a partir de JSON e preencher o Excel a partir de JSON
  usando SmartMarker.
og_title: Salvar Pasta de Trabalho como XLSX – Gerar XLSX a partir de JSON
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Save workbook as XLSX using SmartMarkerProcessor to generate XLSX from
    JSON and easily populate Excel from JSON data.
  headline: Save Workbook as XLSX – Generate XLSX from JSON
  type: TechArticle
- description: Save workbook as XLSX using SmartMarkerProcessor to generate XLSX from
    JSON and easily populate Excel from JSON data.
  name: Save Workbook as XLSX – Generate XLSX from JSON
  steps:
  - name: Expected Result
    text: 'After you run the program, open `output.xlsx`. You’ll see a sheet named
      **Sheet1** with two rows of data:'
  - name: Customizing the Template
    text: 'If you’d rather control column order or add a header row, create a tiny
      template before running the code:'
  - name: 1. Nested JSON Objects
    text: SmartMarker can dive into nested structures using dot notation (`${jsonArray.Address.City}`).
      Just ensure your JSON string reflects that hierarchy.
  - name: 2. Large Datasets
    text: 'When dealing with thousands of rows, disable workbook calculation before
      processing:'
  - name: 3. Data Types
    text: 'Dates, numbers, and booleans are inferred automatically, but you can force
      a format:'
  - name: 4. Multiple Placeholders
    text: You can feed several JSON arrays into the same workbook by using distinct
      placeholder names (`${orders}`, `${customers}`) and calling `processor.apply`
      for each.
  type: HowTo
- questions:
  - answer: No. The library is self‑contained; just add the JAR (or Maven dependency)
      and you’re ready to **save workbook as xlsx**.
    question: Do I need to install anything besides the Aspose Cells JAR?
  - answer: 'Absolutely. Replace `workbook.save("output.xlsx", SaveFormat.XLSX);`
      with: ```java try (FileOutputStream out = new FileOutputStream("output.xlsx"))
      { workbook.save(out, SaveFormat.XLSX); } ```'
    question: Can I write directly to a stream instead of a file?
  - answer: 'Use the `SmartMarkerProcessor.setCustomFieldNames` method to map JSON
      keys to placeholder names. ## Conclusion We’ve covered everything you need to
      **save workbook as xlsx** while **generating XLSX from JSON** and **populating
      Excel from JSON** using Aspose Cells’ SmartMarker. The short program show'
    question: What if my JSON keys don’t match Excel column names?
  type: FAQPage
tags:
- Aspose.Cells
- Java
- Excel Automation
title: Salvar Pasta de Trabalho como XLSX – Gerar XLSX a partir de JSON
url: /pt/java/excel-import-export/save-workbook-as-xlsx-generate-xlsx-from-json/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Salvar Pasta de Trabalho como XLSX – Gerar XLSX a partir de JSON

Já precisou **salvar pasta de trabalho como xlsx** mas só tinha dados JSON à mão? Você não é o único a encontrar essa barreira. Seja consumindo respostas de API, lendo um arquivo de configuração ou apenas experimentando relatórios Excel orientados a dados, transformar JSON em uma planilha organizada é uma demanda frequente.

Neste guia vamos percorrer um exemplo completo, pronto‑para‑executar em Java que **gera XLSX a partir de JSON** e mostra exatamente como **popular Excel a partir de JSON** usando o processador SmartMarker do Aspose Cells. Sem referências vagas—apenas código que você pode copiar, colar e executar.

## O que você vai precisar

- Java 17 (ou qualquer JDK recente)  
- Biblioteca Aspose Cells for Java (a versão de avaliação gratuita funciona)  
- Um IDE simples ou uma ferramenta de build de linha de comando (Maven/Gradle)  
- O trecho JSON que será inserido na pasta de trabalho  

É só isso—sem serviços extras, sem etapas ocultas. Vamos lá.

## Salvar Pasta de Trabalho como XLSX – Processo Completo

Abaixo está o programa inteiro, desde a importação da biblioteca até a persistência do arquivo no disco. Preste atenção aos comentários; eles explicam **por que** cada linha é importante, não apenas **o que** ela faz.

```java
// ---------------------------------------------------------------
// Save Workbook as XLSX – Complete Java Example
// ---------------------------------------------------------------
import com.aspose.cells.*;
import com.google.gson.JsonArray; // For parsing raw JSON string

public class JsonToExcelDemo {

    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook that will receive the data
        Workbook workbook = new Workbook();

        // Step 2: Initialize the SmartMarker processor for the workbook
        SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);

        // Step 3: Enable the flag to treat an array as a single record.
        // This tells SmartMarker to iterate over each element in the JSON array.
        processor.setArrayAsSingle(true);

        // Step 4: Prepare the JSON array source.
        // In a real‑world scenario you might read this from a file or API.
        String json = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":25}]";

        // Step 5: Apply the JSON data to the SmartMarker using the placeholder ${jsonArray}
        // The JsonArray class from Aspose wraps the raw string so SmartMarker can understand it.
        processor.apply("${jsonArray}", new JsonArray(json));

        // OPTIONAL: Save the workbook to see the result.
        // This is the line that actually **save workbook as xlsx**.
        workbook.save("output.xlsx", SaveFormat.XLSX);

        System.out.println("Workbook saved successfully as output.xlsx");
    }
}
```

> **Dica:** Se você estiver usando Maven, adicione as seguintes dependências ao seu `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- check for the latest version -->
</dependency>
<dependency>
    <groupId>com.google.code.gson</groupId>
    <artifactId>gson</artifactId>
    <version>2.10.1</version>
</dependency>
```

### Resultado Esperado

Depois de executar o programa, abra `output.xlsx`. Você verá uma planilha chamada **Sheet1** com duas linhas de dados:

| Name | Age |
|------|-----|
| John | 30  |
| Anna | 25  |

Essa é toda a experiência de **popular excel a partir de json** em menos de 30 linhas de Java.

![save workbook as xlsx example](example.png)

*Texto alternativo da imagem: “exemplo de salvar pasta de trabalho como xlsx”*

## Gerar XLSX a partir de JSON – Como o SmartMarker Funciona

SmartMarker é essencialmente um motor de templates para Excel. Ao colocar `${jsonArray}` em qualquer célula (ou intervalo) de uma pasta de trabalho em branco, você indica ao processador “substitua este placeholder pelos dados do array JSON”. Quando `processor.apply` é executado, ele:

1. Analisa o JSON em uma coleção de registros.  
2. Mapeia cada propriedade (`Name`, `Age`) para uma coluna com base no contexto do placeholder.  
3. Insere linhas automaticamente, tratando os tipos de dados para você.

Como chamamos `processor.setArrayAsSingle(true)`, o array inteiro é tratado como um único conjunto lógico de registros, que é o padrão mais comum ao **gerar XLSX a partir de JSON**.

### Personalizando o Template

Se preferir controlar a ordem das colunas ou adicionar uma linha de cabeçalho, crie um pequeno template antes de executar o código:

| A            | B   |
|--------------|-----|
| **Name**     | **Age** |
| ${jsonArray.Name} | ${jsonArray.Age} |

Salve isso como `template.xlsx` e carregue-o em vez de uma pasta de trabalho vazia:

```java
Workbook workbook = new Workbook("template.xlsx");
```

O restante das etapas permanece idêntico, e a saída manterá a linha de cabeçalho que você definiu.

## Popular Excel a partir de JSON – Casos de Borda & Dicas

### 1. Objetos JSON Aninhados  
SmartMarker pode percorrer estruturas aninhadas usando notação de ponto (`${jsonArray.Address.City}`). Apenas certifique‑se de que sua string JSON reflita essa hierarquia.

### 2. Grandes Conjuntos de Dados  
Ao lidar com milhares de linhas, desative o cálculo da pasta de trabalho antes do processamento:

```java
workbook.getSettings().setCalculateFormula(false);
```

Reative após a gravação para manter o desempenho ágil.

### 3. Tipos de Dados  
Datas, números e booleanos são inferidos automaticamente, mas você pode forçar um formato:

```java
processor.apply("${jsonArray.BirthDate}", new JsonArray(json));
workbook.getWorksheets().get(0).getCells().get("C2").setNumberFormat("mm/dd/yyyy");
```

### 4. Múltiplos Placeholders  
É possível inserir vários arrays JSON na mesma pasta de trabalho usando nomes de placeholder distintos (`${orders}`, `${customers}`) e chamando `processor.apply` para cada um.

## Perguntas Frequentes Respondidas

**Q: Preciso instalar algo além do JAR do Aspose Cells?**  
A: Não. A biblioteca é autônoma; basta adicionar o JAR (ou a dependência Maven) e você está pronto para **salvar pasta de trabalho como xlsx**.

**Q: Posso escrever diretamente em um stream em vez de um arquivo?**  
A: Claro. Substitua `workbook.save("output.xlsx", SaveFormat.XLSX);` por:

```java
try (FileOutputStream out = new FileOutputStream("output.xlsx")) {
    workbook.save(out, SaveFormat.XLSX);
}
```

**Q: E se minhas chaves JSON não coincidirem com os nomes das colunas do Excel?**  
A: Use o método `SmartMarkerProcessor.setCustomFieldNames` para mapear chaves JSON para nomes de placeholders.

## Conclusão

Cobremos tudo o que você precisa para **salvar pasta de trabalho como xlsx** enquanto **gera XLSX a partir de JSON** e **popula Excel a partir de JSON** usando o SmartMarker do Aspose Cells. O pequeno programa demonstra todo o ciclo de vida: criar uma pasta de trabalho, configurar o SmartMarker, alimentar um array JSON e, finalmente, persistir o arquivo.

Em seguida, experimente estender o template com fórmulas, estilos ou múltiplas planilhas—cada um desses conceitos se baseia diretamente na fundação que você acabou de dominar. Se encontrar algum detalhe inesperado, revisitar a seção “Casos de Borda & Dicas” costuma esclarecer a situação.

Boa codificação, e que suas planilhas estejam sempre tão limpas quanto seu JSON!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [How to Save XLSX Files Using Aspose.Cells for .NET: A Step‑by‑Step Guide](/cells/english/net/workbook-operations/save-xlsx-files-aspose-cells-dotnet/)
- [How to Save Excel Workbook in Java Using Aspose.Cells](/cells/english/java/automation-batch-processing/excel-automation-java-aspose-cells-guide/)
- [How to Create and Save an Excel Workbook as SVG using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}