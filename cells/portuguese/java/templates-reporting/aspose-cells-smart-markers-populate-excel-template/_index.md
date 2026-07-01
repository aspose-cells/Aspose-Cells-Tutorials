---
category: general
date: 2026-06-30
description: Aprenda a usar os Smart Markers do Aspose Cells para preencher um modelo
  Excel e gerar um relatório Excel em Java. Código completo passo a passo incluído.
draft: false
keywords:
- aspose cells smart markers
- populate excel template
- generate excel report
- load and save workbook
language: pt
og_description: Os Smart Markers do Aspose Cells permitem preencher um modelo do Excel
  com dados e gerar um relatório do Excel em Java. Siga este guia para obter uma solução
  completa e executável.
og_title: Aspose Cells Smart Markers – Preencher Modelo do Excel
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Learn how to use Aspose Cells Smart Markers to populate an Excel template
    and generate an Excel report in Java. Full step‑by‑step code included.
  headline: Aspose Cells Smart Markers – Populate Excel Template
  type: TechArticle
- description: Learn how to use Aspose Cells Smart Markers to populate an Excel template
    and generate an Excel report in Java. Full step‑by‑step code included.
  name: Aspose Cells Smart Markers – Populate Excel Template
  steps:
  - name: '**Loads** an existing Excel file that contains a smart‑marker placeholder.'
    text: '**Loads** an existing Excel file that contains a smart‑marker placeholder.'
  - name: '**Defines** a master‑detail template (`${Orders.OrderId}` … `${Orders.Details:DetailRow}`).'
    text: '**Defines** a master‑detail template (`${Orders.OrderId}` … `${Orders.Details:DetailRow}`).'
  - name: '**Creates** a `SmartMarkerProcessor` and a populated data model.'
    text: '**Creates** a `SmartMarkerProcessor` and a populated data model.'
  - name: '**Applies** the processor to the first worksheet.'
    text: '**Applies** the processor to the first worksheet.'
  - name: '**Saves** the workbook to a new file, giving you a ready‑to‑use report.'
    text: '**Saves** the workbook to a new file, giving you a ready‑to‑use report.'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel Automation
- Smart Markers
title: Aspose Cells Smart Markers – Preencher Modelo do Excel
url: /pt/java/templates-reporting/aspose-cells-smart-markers-populate-excel-template/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose Cells Smart Markers – Preencher Modelo Excel

Já se perguntou como **populate excel template** sem escrever loops intermináveis e atribuições célula por célula? A resposta costuma ser **Aspose Cells Smart Markers**, uma forma declarativa de vincular seus objetos Java diretamente a uma pasta de trabalho Excel. Neste tutorial, vamos percorrer o carregamento de uma pasta de trabalho, a definição de um modelo de smart‑marker mestre‑detalhe, alimentá‑lo com um modelo de dados e, finalmente, salvar o resultado como um arquivo **generate excel report** totalmente preenchido.

Pense nisso como uma mala‑direta para planilhas: você projeta o layout uma vez e deixa a biblioteca fazer o trabalho pesado. Chega de chamadas manuais `cell.setValue()`, chega de erros de deslocamento. Pronto para ver em ação?

## O que você vai construir

Até o final deste guia, você terá um programa Java que:

1. **Loads** um arquivo Excel existente que contém um placeholder de smart‑marker.
2. **Defines** um modelo mestre‑detalhe (`${Orders.OrderId}` … `${Orders.Details:DetailRow}`).
3. **Creates** um `SmartMarkerProcessor` e um modelo de dados preenchido.
4. **Applies** o processador à primeira planilha.
5. **Saves** a pasta de trabalho em um novo arquivo, fornecendo um relatório pronto‑para‑usar.

Você também receberá dicas sobre como lidar com grandes conjuntos de dados, várias planilhas e armadilhas comuns.

## Pré-requisitos

- Java 8 ou superior (o código usa a Stream API para brevidade).
- Biblioteca Aspose.Cells for Java (download em [aspose.com/cells/java](https://products.aspose.com/cells/java/)).
- Um arquivo Excel (`input.xlsx`) que contém os placeholders de smart‑marker mostrados abaixo.
- Um entendimento básico de coleções e mapas Java.

Se você não tem algum desses, obtenha agora — caso contrário, vamos mergulhar.

![aspose cells smart markers workflow diagram](image-url-placeholder.png)

## Etapa 1 – Carregar e Salvar Pasta de Trabalho

A primeira coisa que fazemos é **load and save workbook**. Aspose.Cells abstrai o formato de arquivo, de modo que você pode trabalhar com `.xlsx`, `.xls` ou até `.csv` sem mudar uma linha de código.

```java
import com.aspose.cells.*;

public class SmartMarkerDemo {
    public static void main(String[] args) throws Exception {
        // Load the workbook that contains the smart‑marker template
        Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // All processing happens here (see later steps)

        // Save the workbook with the populated data
        wb.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

> **Pro tip:** Se você está lidando com arquivos enormes, considere usar `WorkbookSettings.setMemorySetting(MemorySetting.MEMORY_PREFERENCE);` para manter o uso de memória baixo.

## Etapa 2 – Projetar o Modelo Smart‑Marker

Abra `input.xlsx` no Excel e digite o seguinte em uma célula (geralmente a primeira linha de uma tabela):

```
${Orders.OrderId}
${Orders.Details:DetailRow}
```

- `${Orders.OrderId}` – extrai o campo `OrderId` de cada objeto `Order`.
- `${Orders.Details:DetailRow}` – indica ao Aspose para repetir a linha para cada item na coleção `Details` (mestre‑detalhe).

O sufixo `:DetailRow` é o **detail marker**; ele repete a linha inteira para cada elemento da coleção, ajustando automaticamente os números das linhas.

## Etapa 3 – Criar o SmartMarkerProcessor

O processador é o motor que lê o modelo, combina os marcadores com seus dados e grava o resultado de volta na planilha.

```java
// Step 3: Create a SmartMarkerProcessor instance
SmartMarkerProcessor processor = new SmartMarkerProcessor();
```

Você pode ajustar seu comportamento (por exemplo, habilitar `processor.setOptions(SmartMarkerOptions.REMOVE_EMPTY_ROWS);`) mas os padrões funcionam na maioria dos cenários.

## Etapa 4 – Construir o Modelo de Dados

Aspose espera um `Map<String, Object>` onde a chave corresponde ao nome do marcador (`Orders` no nosso caso). Abaixo está um modelo de dados mínimo, *completo*, que inclui uma lista mestre de pedidos, cada um com uma lista de itens de detalhe.

```java
import java.util.*;

public class DataProvider {
    // Returns a map that Aspose will use to replace the markers
    public static Map<String, Object> getOrderData() {
        List<Order> orders = new ArrayList<>();

        // Sample Order 1
        Order order1 = new Order(1001);
        order1.addDetail(new Detail("Apple", 3, 1.20));
        order1.addDetail(new Detail("Banana", 5, 0.80));
        orders.add(order1);

        // Sample Order 2
        Order order2 = new Order(1002);
        order2.addDetail(new Detail("Orange", 2, 1.50));
        order2.addDetail(new Detail("Grapes", 1, 2.00));
        orders.add(order2);

        // The key must match the marker name in the template
        Map<String, Object> model = new HashMap<>();
        model.put("Orders", orders);
        return model;
    }
}

// --- POJOs used above ----------------------------------------------------
class Order {
    private int orderId;
    private List<Detail> details = new ArrayList<>();

    public Order(int orderId) { this.orderId = orderId; }

    public int getOrderId() { return orderId; }

    public List<Detail> getDetails() { return details; }

    public void addDetail(Detail d) { details.add(d); }
}

class Detail {
    private String product;
    private int quantity;
    private double price;

    public Detail(String product, int quantity, double price) {
        this.product = product;
        this.quantity = quantity;
        this.price = price;
    }

    public String getProduct() { return product; }
    public int getQuantity() { return quantity; }
    public double getPrice() { return price; }
}
```

> **Why a Map?**  
> O motor de smart‑marker usa reflexão para ler os getters de propriedades (`getOrderId()`, `getDetails()`). Ao fornecer um mapa, você pode trocar qualquer grafo de objetos sem reescrever o modelo.

## Etapa 5 – Aplicar o Processador à Planilha

Agora juntamos tudo. O processador escaneia a primeira planilha (índice 0) em busca de marcadores, mescla os dados e expande as linhas conforme necessário.

```java
// Inside main() after loading the workbook
Map<String, Object> dataModel = DataProvider.getOrderData();

// Apply the processor to the first worksheet using the model
processor.apply(wb.getWorksheets().get(0), dataModel);
```

Se o seu modelo estiver em outra planilha, basta mudar o índice (`get(1)`, `get("Sheet2")`, etc.). O processador também funciona em várias planilhas em uma única chamada se você passar o `Workbook` inteiro em vez de um único `Worksheet`.

## Etapa 6 – Verificar a Saída

Execute o programa. Abra `output.xlsx` e você deverá ver algo como:

| OrderId | Product | Quantity | Price |
|--------|---------|----------|-------|
| 1001   | Apple   | 3        | 1.20  |
| 1001   | Banana  | 5        | 0.80  |
| 1002   | Orange  | 2        | 1.50  |
| 1002   | Grapes  | 1        | 2.00  |

Observe como as linhas mestre‑detalhe são geradas automaticamente — sem loops, sem referências manuais de células. Esse é o poder dos **aspose cells smart markers**.

## Tópicos Avançados e Casos Limite

### 1. Manipulação de Grandes Conjuntos de Dados
Quando você precisar gerar um relatório com dezenas de milhares de linhas, habilite streaming:



## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá-lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Como Automatizar Smart Markers do Excel com Aspose.Cells para Java](/cells/english/java/automation-batch-processing/aspose-cells-java-smart-markers-excel/)
- [Domine Aspose.Cells Java: Implemente Smart Markers e Fórmulas para Automação Excel](/cells/english/java/formulas-functions/aspose-cells-java-smart-markers-formulas/)
- [Preencha Excel com Dados Usando Aspose.Cells e Smart Markers](/cells/english/java/cell-operations/populate-excel-aspose-cells-smart-markers/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}