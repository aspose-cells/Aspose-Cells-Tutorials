---
category: general
date: 2026-08-20
description: Crie marcadores inteligentes de planilhas em Java usando Aspose.Cells
  e controle a nomeação da planilha de detalhes com SmartMarkerOptions.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create worksheets smart markers
- Aspose.Cells Java
- smart marker options
- duplicate sheet names
- detail sheet naming
language: pt
lastmod: 2026-08-20
og_description: Crie marcadores inteligentes de planilhas em Java com Aspose.Cells.
  Aprenda como nomear planilhas de detalhes dinamicamente usando SmartMarkerOptions.
og_image_alt: create worksheets smart markers example diagram
og_title: Criar marcadores inteligentes para planilhas – Guia Java com Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Create worksheets smart markers in Java using Aspose.Cells and control
    detail sheet naming with SmartMarkerOptions.
  headline: How to create worksheets smart markers with Aspose.Cells
  type: TechArticle
- description: Create worksheets smart markers in Java using Aspose.Cells and control
    detail sheet naming with SmartMarkerOptions.
  name: How to create worksheets smart markers with Aspose.Cells
  steps:
  - name: Set up the Maven project and add Aspose.Cells
    text: 'Create a new Maven module (or Gradle project) and add the Aspose.Cells
      dependency:'
  - name: Load the master workbook that contains smart markers
    text: '```java import com.aspose.cells.*;'
  - name: Configure SmartMarkerOptions for custom detail sheet names
    text: '```java // Define naming pattern for detail sheets. SmartMarkerOptions
      smartMarkerOptions = new SmartMarkerOptions(); // {0} is automatically replaced
      by the row index (starting at 1). smartMarkerOptions.setDetailSheetNewName("DetailSheet_{0}");
      ```'
  - name: Build a DataTable that matches the smart marker fields
    text: '```java // Build a simple DataTable with two columns. DataTable data =
      new DataTable(); data.getColumns().add("Id", DataType.INTEGER); data.getColumns().add("Value",
      DataType.STRING); // Add sample rows. data.getRows().add(new Object[] { 1, "A"
      }); data.getRows().add(new Object[] { 2, "B" }); ```'
  - name: Apply the data to the smart markers with the naming options
    text: '```java // Apply the data to the first worksheet (index 0). workbook.getWorksheets().get(0).getSmartMarkers().apply(data,
      smartMarkerOptions); ```'
  - name: Save the workbook and verify the result
    text: '```java // Save the expanded workbook. workbook.save("YOUR_DIRECTORY/MasterDetailDuplicatedNames.xlsx");
      } } ```'
  - name: Multiple master sheets
    text: 'If your template contains more than one master sheet, iterate over each
      sheet’s smart markers:'
  - name: Custom naming beyond the row index
    text: 'You can embed any data column into the sheet name by using placeholders
      like `{ColumnName}`:'
  - name: Preventing overly long sheet names
    text: 'Excel limits sheet names to 31 characters. If your naming pattern risks
      exceeding this limit, truncate or hash the value:'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Smart Markers
- Excel Automation
title: Como criar marcadores inteligentes em planilhas com Aspose.Cells
url: /pt/java/templates-reporting/how-to-create-worksheets-smart-markers-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como criar marcadores inteligentes de planilhas com Aspose.Cells

Se você precisar **criar marcadores inteligentes de planilhas** em uma workbook Java, este guia mostra os passos exatos para fazê‑lo com Aspose.Cells. Você verá como configurar `SmartMarkerOptions` para que cada planilha de detalhe receba um nome único e previsível.

Gerar relatórios Excel que expandem um modelo mestre‑detalhe é uma necessidade comum em finanças, inventário e sistemas de relatórios. Usar marcadores inteligentes elimina a duplicação manual de planilhas e permite que você se concentre nos dados em vez da infraestrutura.

## O que você aprenderá

* Como carregar uma workbook mestre que contém marcadores inteligentes.  
* Como definir `SmartMarkerOptions` para controlar a nomeação das planilhas de detalhe geradas.  
* Como fornecer um `DataTable` com dados de exemplo e aplicá‑lo aos marcadores inteligentes.  
* Como salvar o resultado para que cada planilha de detalhe tenha um nome distinto, evitando nomes de planilha duplicados.

**Pré-requisitos**  
* Java 17 ou superior (o código também compila com JDK 8+).  
* Aspose.Cells for Java 23.9 ou mais recente – a biblioteca fornece as classes `Workbook`, `SmartMarkerOptions` e relacionadas.  
* Uma IDE como IntelliJ IDEA, Eclipse ou VS Code.

Conceitos secundários que você encontrará incluem **Aspose.Cells Java**, **smart marker options** e o tratamento de **duplicate sheet names** quando o modelo é expandido.

## Criar marcadores inteligentes de planilhas – guia passo a passo

As seções a seguir dividem o processo em etapas discretas e reutilizáveis. Cada etapa inclui um trecho de código, uma explicação do porquê é importante e dicas práticas para evitar armadilhas comuns.

### Etapa 1: Configurar o projeto Maven e adicionar Aspose.Cells

Crie um novo módulo Maven (ou projeto Gradle) e adicione a dependência Aspose.Cells:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
</dependency>
```

**Por que esta etapa é importante** – A biblioteca fornece a classe `Workbook` que lê e grava arquivos Excel, além do mecanismo smart‑marker que expande seu modelo automaticamente. Sem a dependência correta, o compilador não consegue resolver as chamadas de API usadas posteriormente.

> **Dica profissional:** Se você trabalha atrás de um proxy corporativo, configure o `settings.xml` do Maven para buscar o repositório Aspose de forma segura.

### Etapa 2: Carregar a workbook mestre que contém marcadores inteligentes

Carregue a workbook mestre que contém marcadores inteligentes:

```java
import com.aspose.cells.*;

public class DuplicateDetailSheetNames {
    public static void main(String[] args) throws Exception {
        // Load the template that holds the smart marker tags.
        Workbook workbook = new Workbook("YOUR_DIRECTORY/MasterDetailTemplate.xlsx");
```

**Por que esta etapa é importante** – A workbook mestre define o layout, fórmulas e tags de espaço reservado (`«SmartMarker»`) que o mecanismo substituirá. Carregar o arquivo uma única vez mantém o uso de memória baixo e permite reutilizar a mesma workbook para vários conjuntos de dados.

### Etapa 3: Configurar SmartMarkerOptions para nomes personalizados de planilhas de detalhe

Configure o SmartMarkerOptions para nomes personalizados de planilhas de detalhe:

```java
        // Define naming pattern for detail sheets.
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions();
        // {0} is automatically replaced by the row index (starting at 1).
        smartMarkerOptions.setDetailSheetNewName("DetailSheet_{0}");
```

**Por que esta etapa é importante** – Por padrão, Aspose.Cells cria planilhas de detalhe com nomes genéricos como “DetailSheet”. Quando o modelo é expandido para muitas linhas, esses nomes entram em conflito, levando a **duplicate sheet names** e a uma exceção em tempo de execução. O padrão `"DetailSheet_{0}"` garante um nome único por linha, resolvendo o problema de duplicação.

### Etapa 4: Construir um DataTable que corresponda aos campos do marcador inteligente

Construa um DataTable que corresponda aos campos do marcador inteligente:

```java
        // Build a simple DataTable with two columns.
        DataTable data = new DataTable();
        data.getColumns().add("Id", DataType.INTEGER);
        data.getColumns().add("Value", DataType.STRING);
        // Add sample rows.
        data.getRows().add(new Object[] { 1, "A" });
        data.getRows().add(new Object[] { 2, "B" });
```

**Por que esta etapa é importante** – O `DataTable` fornece os valores reais que substituem os espaços reservados dos marcadores inteligentes. Os nomes das colunas devem corresponder aos nomes dos marcadores no modelo; caso contrário, o mecanismo ignora a substituição silenciosamente.

> **Erro comum:** Usar um nome de coluna que difere em maiúsculas/minúsculas (por exemplo, “id” vs “Id”) leva à falta de dados nas planilhas geradas.

### Etapa 5: Aplicar os dados aos marcadores inteligentes com as opções de nomeação

Aplique os dados aos marcadores inteligentes com as opções de nomeação:

```java
        // Apply the data to the first worksheet (index 0).
        workbook.getWorksheets().get(0).getSmartMarkers().apply(data, smartMarkerOptions);
```

**Por que esta etapa é importante** – O método `apply` aciona o mecanismo smart‑marker. Ele lê cada linha, cria uma nova planilha de detalhe usando o padrão de nomeação de `SmartMarkerOptions` e preenche a planilha com os dados da linha. Essa única chamada substitui dezenas de linhas de clonagem manual de planilhas e preenchimento de células.

### Etapa 6: Salvar a workbook e verificar o resultado

Salve a workbook e verifique o resultado:

```java
        // Save the expanded workbook.
        workbook.save("YOUR_DIRECTORY/MasterDetailDuplicatedNames.xlsx");
    }
}
```

Após a execução, abra `MasterDetailDuplicatedNames.xlsx`. Você deverá ver:

* A planilha mestre original inalterada.  
* Duas novas planilhas nomeadas `DetailSheet_1` e `DetailSheet_2`.  
* Cada planilha de detalhe contém os valores da linha correspondente do `DataTable`.

**Por que esta etapa é importante** – Persistir a workbook finaliza a expansão dos marcadores inteligentes. O arquivo agora pode ser enviado a sistemas downstream, anexado a e‑mails ou aberto no Excel para análise adicional.

## Tratamento de casos extremos e variações

### Várias planilhas mestre

Se o seu modelo contiver mais de uma planilha mestre, itere sobre os marcadores inteligentes de cada planilha:

```java
for (int i = 0; i < workbook.getWorksheets().getCount(); i++) {
    workbook.getWorksheets().get(i).getSmartMarkers().apply(data, smartMarkerOptions);
}
```

### Nomeação personalizada além do índice da linha

Você pode incorporar qualquer coluna de dados no nome da planilha usando espaços reservados como `{ColumnName}`:

```java
smartMarkerOptions.setDetailSheetNewName("Order_{OrderId}");
```

Certifique-se de que a coluna `OrderId` exista no `DataTable` fornecido.

### Prevenindo nomes de planilha excessivamente longos

O Excel limita os nomes de planilha a 31 caracteres. Se o seu padrão de nomeação correr o risco de exceder esse limite, trunque ou faça hash do valor:

```java
String pattern = "Detail_{0}_{1}";
smartMarkerOptions.setDetailSheetNewName(pattern);
```

Em seguida, pós‑procese o nome gerado com `StringUtils.abbreviate` antes de passá‑lo ao Aspose.

## Exemplo completo executável

Abaixo está o arquivo de código-fonte completo que você pode copiar, ajustar os caminhos de arquivo e executar diretamente:

```java
import com.aspose.cells.*;

public class DuplicateDetailSheetNames {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the master workbook that contains smart markers
        Workbook workbook = new Workbook("YOUR_DIRECTORY/MasterDetailTemplate.xlsx");

        // 2️⃣ Define how detail sheets will be named when they are created
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions();
        // {0} is replaced by the row index (starting at 1)
        smartMarkerOptions.setDetailSheetNewName("DetailSheet_{0}");

        // 3️⃣ Prepare sample data to populate the smart markers
        DataTable data = new DataTable();
        data.getColumns().add("Id", DataType.INTEGER);
        data.getColumns().add("Value", DataType.STRING);
        data.getRows().add(new Object[] { 1, "A" });
        data.getRows().add(new Object[] { 2, "B" });

        // 4️⃣ Apply the data to the smart markers using the naming options
        workbook.getWorksheets().get(0).getSmartMarkers().apply(data, smartMarkerOptions);

        // 5️⃣ Save the workbook – each detail sheet now has a unique name
        workbook.save("YOUR_DIRECTORY/MasterDetailDuplicatedNames.xlsx");
    }
}
```

**Saída esperada**  

* `MasterDetailDuplicatedNames.xlsx` contém:

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Mastering Aspose.Cells Java: Utilize Smart Markers for Dynamic Data in Worksheets](/cells/english/java/worksheet-management/aspose-cells-java-smart-markers-worksheets/)
- [Create Dynamic Charts with Smart Markers in Aspose.Cells for Java | Step-by-Step Guide](/cells/english/java/charts-graphs/dynamic-charts-smart-markers-aspose-cells-java/)
- [Aspose Cells Java Smart Markers Worksheets](/cells/german/java/worksheet-management/aspose-cells-java-smart-markers-worksheets/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}