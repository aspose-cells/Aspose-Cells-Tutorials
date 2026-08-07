---
category: general
date: 2026-07-03
description: Como gerar relatório preenchendo um modelo do Excel usando Smart Markers.
  Aprenda a criar a planilha de detalhes, usar smart markers e automatizar a inserção
  de dados.
draft: false
keywords:
- how to generate report
- populate excel template
- how to create detail
- create detail sheet
- use smart markers
language: pt
og_description: Como gerar relatório usando Smart Markers em Java. Este guia mostra
  como preencher um modelo Excel, criar uma planilha de detalhes e automatizar relatórios
  mestre‑detalhe.
og_title: Como gerar relatório com marcadores inteligentes do Excel – Tutorial Java
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: How to generate report by populating an Excel template using Smart
    Markers. Learn to create detail sheet, use smart markers and automate data insertion.
  headline: How to Generate Report with Excel Smart Markers – Full Java Guide
  type: TechArticle
- description: How to generate report by populating an Excel template using Smart
    Markers. Learn to create detail sheet, use smart markers and automate data insertion.
  name: How to Generate Report with Excel Smart Markers – Full Java Guide
  steps:
  - name: What the code does, step by step
    text: '| Step | Explanation | |------|-------------| | **Load workbook** | Reads
      the template, preserving all formatting. | | **Insert marker** | Guarantees
      the placeholder exists even if you built the template programmatically. | |
      **Prepare data** | The `Map` key (`"Orders"`) must match the Smart Marker '
  - name: 5.1 Multiple Detail Datasets
    text: 'You can embed several Smart Markers in the same template, e.g., `{{Detail:Customers}}`
      and `{{Detail:Orders}}`. Just add corresponding entries to the `Map`:'
  - name: 5.2 Custom Sheet Names per Row
    text: 'If you need a unique sheet per order (instead of a single detail sheet),
      use the `DetailSheetNewName` pattern with placeholders:'
  - name: 5.3 Handling Large Datasets
    text: 'When dealing with thousands of rows, enable streaming to keep memory usage
      low:'
  - name: 5.4 Formatting Numbers and Dates
    text: Smart Markers respect the cell’s existing format. If column B in the template
      is formatted as **Currency**, the amounts will automatically display with the
      correct symbol. For custom date formats, just set the cell’s number format before
      processing.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel Automation
title: Como gerar relatório com marcadores inteligentes do Excel – Guia completo em
  Java
url: /pt/java/templates-reporting/how-to-generate-report-with-excel-smart-markers-full-java-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Gerar Relatórios com Marcadores Inteligentes do Excel – Guia Completo em Java

Já se perguntou **como gerar relatórios** a partir de um modelo Excel sem escrever milhões de linhas de código de loop? Você não está sozinho. Muitos desenvolvedores encontram dificuldades quando precisam extrair dados de um banco de dados, inseri‑los em uma planilha mestre‑detalhe e ainda manter o layout impecável.  

A boa notícia? Com os **Marcadores Inteligentes** do Aspose.Cells você pode **preencher um modelo Excel** em uma única chamada legível — sem precisar de malabarismos célula por célula. Neste tutorial vamos percorrer todo o processo, desde a preparação do modelo até a gravação do arquivo final, e também vamos mostrar **como criar planilhas de detalhe** dinamicamente.

Ao final deste guia você será capaz de:

* Carregar uma pasta de trabalho pré‑projetada que funciona como sua planilha mestre.  
* Inserir um marcador inteligente que o Aspose substituirá pelos dados reais do pedido.  
* Alimentar um `Map` Java como fonte de dados e configurar as opções de **criar planilha de detalhe**.  
* Executar o processador e obter um relatório mestre‑detalhe polido pronto para ser compartilhado.

> **Dica de especialista:** Se você já tem um modelo que a equipe de negócios adora, não precisará tocar no layout — basta inserir as tags de Marcador Inteligente nas células corretas.

---

## Pré‑requisitos

Antes de mergulharmos no código, certifique‑se de que você tem o seguinte:

| Requisito | Por que é importante |
|-------------|----------------|
| **Aspose.Cells for Java** (versão mais recente) | Fornece o `SmartMarkerProcessor`, `Workbook` e APIs relacionadas. |
| **Java 8+** | O exemplo usa streams e o método de fábrica `Map.of` introduzido no Java 9; ajuste se estiver usando Java 8. |
| **Um modelo Excel** (`template.xlsx`) com uma célula de placeholder para o Marcador Inteligente | Este é o arquivo que você carregará e, posteriormente, salvará como `masterDetail.xlsx`. |
| **Um modelo de dados simples** (por exemplo, classe `Order`) | Fornece ao processador algo concreto para substituir os marcadores. |

Se ainda não tem o Aspose.Cells, obtenha uma avaliação gratuita no site oficial e adicione o JAR ao classpath do seu projeto.

---

## Etapa 1: Configurar o Modelo Excel (populate excel template)

Abra o Excel e crie uma pasta de trabalho chamada `template.xlsx`. Na célula **A1** da primeira planilha, digite a tag do Marcador Inteligente:

```
{{Detail:Orders}}
```

Essa tag indica ao Aspose que a coleção `Orders` deve ser tratada como um conjunto de **detalhe** e que linhas serão geradas para cada item. Salve o arquivo em uma pasta que será referenciada mais tarde, por exemplo, `C:/Reports/`.

> **Por que isso importa:** Ao incorporar o marcador diretamente no modelo, você mantém o design visual separado do código. Designers podem ajustar fontes, cores e fórmulas sem tocar no Java.

---

## Etapa 2: Criar a Estrutura do Projeto Java

Aqui está um trecho mínimo do `pom.xml` Maven que inclui o Aspose.Cells:

```xml
<dependencies>
    <dependency>
        <groupId>com.aspose</groupId>
        <artifactId>aspose-cells</artifactId>
        <version>24.9</version> <!-- Use the latest version -->
    </dependency>
</dependencies>
```

Crie o pacote `com.example.report` e adicione duas classes: `ReportGenerator` (o driver principal) e `Order` (nosso modelo de dados).

```java
package com.example.report;

public class Order {
    public String orderId;
    public String customer;
    public double amount;

    public Order(String orderId, String customer, double amount) {
        this.orderId = orderId;
        this.customer = customer;
        this.amount = amount;
    }

    // Getters are optional for Smart Marker; public fields work fine.
}
```

---

## Etapa 3: Carregar a Pasta de Trabalho e Inserir o Marcador Inteligente (use smart markers)

Agora vamos escrever a lógica central. Observe como o código reflete o snippet original, mas adiciona imports, tratamento de erros e comentários para clareza.

```java
package com.example.report;

import com.aspose.cells.*;
import java.util.*;

public class ReportGenerator {

    public static void main(String[] args) {
        try {
            // 1️⃣ Load the workbook that contains the master sheet
            Workbook wb = new Workbook("C:/Reports/template.xlsx");

            // 2️⃣ Grab the first worksheet (the master)
            Worksheet master = wb.getWorksheets().get(0);

            // 3️⃣ Insert a Smart Marker placeholder if you prefer to do it programmatically.
            //    This is optional because we already placed {{Detail:Orders}} in A1.
            master.getCells().putValue("A1", "{{Detail:Orders}}");

            // 4️⃣ Prepare the data source for the Smart Marker
            Map<String, Object> data = new HashMap<>();
            data.put("Orders", getOrders()); // getOrders() returns List<Order>

            // 5️⃣ Configure Smart Marker options – this is where we **create detail sheet**
            SmartMarkerOptions smOpt = new SmartMarkerOptions();
            smOpt.setDetailSheetNewName("OrderDetail"); // New sheet will be named "OrderDetail"

            // 6️⃣ Process the Smart Marker to generate the master‑detail report
            SmartMarkerProcessor processor = new SmartMarkerProcessor();
            processor.process(master, data, smOpt);

            // 7️⃣ Save the resulting workbook
            wb.save("C:/Reports/masterDetail.xlsx");

            System.out.println("Report generated successfully!");
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    /**
     * Simulates fetching order data from a database or service.
     * In a real‑world scenario replace this with JDBC/ORM calls.
     */
    private static List<Order> getOrders() {
        return Arrays.asList(
            new Order("ORD001", "Acme Corp", 1250.75),
            new Order("ORD002", "Beta Ltd.", 980.00),
            new Order("ORD003", "Gamma Inc.", 432.50)
        );
    }
}
```

### O que o código faz, passo a passo

| Etapa | Explicação |
|------|-------------|
| **Carregar a pasta de trabalho** | Lê o modelo, preservando toda a formatação. |
| **Inserir o marcador** | Garante que o placeholder exista mesmo se você criou o modelo programaticamente. |
| **Preparar os dados** | A chave do `Map` (`"Orders"`) deve coincidir com a tag do Marcador Inteligente (`{{Detail:Orders}}`). |
| **Configurar opções** | `setDetailSheetNewName` instrui o Aspose a criar uma **planilha de detalhe** chamada *OrderDetail*. |
| **Processar** | O `SmartMarkerProcessor` percorre a pasta de trabalho, substitui a tag e gera linhas na nova planilha. |
| **Salvar** | Grava o `masterDetail.xlsx` final no disco. |

> **Por que usar Marcadores Inteligentes?** Eles permitem que você descreva *o que* deseja (uma tabela de pedidos) em vez de *como* percorrer linhas e colunas. A biblioteca cuida da paginação, cópia de estilos e até da recalculação de fórmulas automaticamente.

---

## Etapa 4: Verificar a Saída (how to generate report – verification)

Execute a classe `ReportGenerator`. Após a execução você deverá ver duas planilhas:

1. **Sheet1** – a planilha mestre original (ainda contém `{{Detail:Orders}}`, mas o processador a oculta).  
2. **OrderDetail** – uma nova planilha com uma linha para cada objeto `Order`:

| Order ID | Customer   | Amount |
|----------|------------|--------|
| ORD001   | Acme Corp  | 1250.75|
| ORD002   | Beta Ltd.  | 980.00 |
| ORD003   | Gamma Inc. | 432.50 |

Se você abrir o arquivo no Excel perceberá que larguras de coluna, fontes e quaisquer estilos pré‑aplicados no modelo permanecem intactos. Essa é a beleza de **usar marcadores inteligentes**: eles preservam a apresentação enquanto injetam os dados.

---

## Etapa 5: Variações Comuns & Casos de Borda (populate excel template, how to create detail)

### 5.1 Vários Conjuntos de Detalhe

É possível inserir vários Marcadores Inteligentes no mesmo modelo, por exemplo, `{{Detail:Customers}}` e `{{Detail:Orders}}`. Basta adicionar as entradas correspondentes ao `Map`:

```java
data.put("Customers", getCustomers());
data.put("Orders", getOrders());
```

Cada um gerará sua própria planilha se você definir `DetailSheetNewName` adequadamente.

### 5.2 Nomes de Planilha Personalizados por Linha

Se precisar de uma planilha única por pedido (em vez de uma única planilha de detalhe), use o padrão `DetailSheetNewName` com placeholders:

```java
smOpt.setDetailSheetNewName("Order_{OrderId}");
```

O Aspose substituirá `{OrderId}` pelo valor real de cada linha.

### 5.3 Manipulação de Grandes Conjuntos de Dados

Ao lidar com milhares de linhas, habilite streaming para manter o uso de memória baixo:

```java
WorkbookSettings ws = wb.getSettings();
ws.setMemorySetting(MemorySetting.MEMORY_PREFERENCE);
```

### 5.4 Formatação de Números e Datas

Marcadores Inteligentes respeitam o formato existente da célula. Se a coluna B no modelo estiver formatada como **Currency**, os valores serão exibidos automaticamente com o símbolo correto. Para formatos de data personalizados, basta definir o formato numérico da célula antes do processamento.

---

## Etapa 6: Dicas & Armadilhas (how to create detail, use smart markers)

* **Nunca codifique caminhos de arquivo** em produção. Use um arquivo de configuração ou variável de ambiente.  
* **Sempre feche recursos** se estiver abrindo streams manualmente; a classe `Workbook` implementa `AutoCloseable` nas versões mais recentes.  
* **Fique atento a colisões de nomes** — se já existir uma planilha com o mesmo nome, o Aspose acrescentará um sufixo numérico. Para garantir unicidade, prefixe o nome com um timestamp.  
* **Teste com coleções vazias**. Se `Orders` estiver vazio, o processador ainda cria a planilha, mas a deixa em branco — trate isso posteriormente se não quiser abas desnecessárias.  
* **Depuração de Marcadores Inteligentes**: configure `smOpt.setThrowExceptionOnMissingData(true)` para obter uma exceção clara quando um marcador não corresponder a nenhum campo de dados.

---

![How to generate report using Smart Markers in Java](/images/how-to-generate-report-smart-markers.png "how to generate report")

*Legenda da imagem: O `masterDetail.xlsx` final mostrando a planilha mestre e a planilha **OrderDetail** gerada.*

---

## Conclusão

Acabamos de demonstrar **como gerar relatórios** ao **preencher um modelo Excel** com os Marcadores Inteligentes do Aspose.Cells, e cobrimos tudo o que você precisa para **criar planilhas de detalhe** automaticamente. A abordagem mantém

## O que Você Deve Aprender a Seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [How to Automate Excel Smart Markers with Aspose.Cells for Java](/cells/english/java/automation-batch-processing/aspose-cells-java-smart-markers-excel/)
- [Populate Excel with Data Using Aspose.Cells and Smart Markers](/cells/english/java/cell-operations/populate-excel-aspose-cells-smart-markers/)
- [How to Create Pivot Tables in Excel Using Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}