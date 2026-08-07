---
category: general
date: 2026-06-21
description: Crie várias planilhas no Excel usando Java. Aprenda como exportar dados
  para planilhas, usar uma abordagem baseada em modelo no Excel e salvar a pasta de
  trabalho xlsx de forma eficiente.
draft: false
keywords:
- create multiple sheets
- export data to sheets
- template based excel
- save workbook xlsx
- insert index worksheet
language: pt
og_description: Crie várias planilhas no Excel usando Java. Este guia mostra como
  exportar dados para planilhas, aplicar um fluxo de trabalho baseado em modelo no
  Excel e salvar a pasta de trabalho em xlsx.
og_title: Crie várias planilhas no Excel com Java – Passo a passo
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create multiple sheets in Excel using Java. Learn how to export data
    to sheets, use a template based Excel approach, and save workbook xlsx efficiently.
  headline: Create Multiple Sheets in Excel with Java – Complete Template‑Based Guide
  type: TechArticle
tags:
- Java
- Excel
- Aspose.Cells
- Automation
title: Crie várias planilhas no Excel com Java – Guia completo baseado em modelos
url: /pt/java/worksheet-management/create-multiple-sheets-in-excel-with-java-complete-template/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar Várias Planilhas no Excel com Java – Guia Completo Baseado em Modelo

Já precisou **criar várias planilhas** em uma pasta de trabalho do Excel a partir de uma aplicação Java, mas não sabia por onde começar? Você não está sozinho. Seja construindo um mecanismo de relatórios, uma utilidade de exportação de dados, ou apenas tentando automatizar uma tarefa tediosa de planilha, dominar como *exportar dados para planilhas* pode economizar horas de trabalho manual.

Neste tutorial, percorreremos uma solução **Excel baseada em modelo** que permite inserir uma planilha de índice, gerar uma planilha por item de dados e, finalmente, **salvar a workbook xlsx** com uma única chamada de método. Sem enrolação, apenas um exemplo prático, de ponta a ponta, que você pode inserir em seu projeto hoje.

## O que você aprenderá

- Como inicializar uma workbook que conterá **várias planilhas**.
- Usando a sintaxe Smart Marker do Aspose.Cells para repetir planilhas automaticamente.
- Preparando uma fonte de dados (lista de mapas, POJOs ou qualquer coleção) para o modelo.
- Aplicando o modelo com `SmartMarkerProcessor`.
- Salvando o resultado como um arquivo **xlsx**.
- Dicas opcionais para inserir uma planilha de índice e lidar com casos extremos.

*Pré-requisitos*: Java 8+, Maven ou Gradle, e a biblioteca Aspose.Cells for Java (a avaliação gratuita funciona bem para testes). Se você é novo no Aspose, não se preocupe — manteremos as etapas de configuração breves.

---

## Etapa 1: Inicializar a Workbook – O Canvas para **Create Multiple Sheets**

Antes que qualquer planilha apareça, você precisa de uma instância de `Workbook`. Pense nela como uma tela em branco que, mais tarde, conterá cada planilha gerada.

```java
import com.aspose.cells.*;

public class MultiSheetExporter {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an empty workbook that will hold the generated worksheets
        Workbook workbook = new Workbook();
        // ... we'll add more code here later
    }
}
```

> **Por que isso importa:** O objeto `Workbook` abstrai todo o arquivo Excel. Ao começar com uma workbook vazia, você mantém controle total sobre a criação de planilhas, formatação e salvamento final.

---

## Etapa 2: Definir um Marcador **Template Based Excel** – O Blueprint para Cada Planilha

O mecanismo Smart Marker do Aspose.Cells permite incorporar marcadores de posição diretamente em um modelo de string. O marcador especial `${#WorksheetRepeat}` indica ao processador que inicie uma **nova planilha** para cada item na coleção de dados.

```java
// Step 2: Define a Smart Marker template.
// ${#WorksheetRepeat} starts a new worksheet for each item in the data collection.
// ${Index} inserts the current item index, and ${Data} inserts the item value.
String template = "${#WorksheetRepeat}Sheet${Index}\n${Data}";
```

> **Dica profissional:** O caractere `\n` cria uma nova linha após o nome da planilha, de modo que a primeira linha de cada planilha conterá o valor real dos dados. Ajuste o modelo para incluir cabeçalhos, fórmulas ou estilos conforme necessário.

---

## Etapa 3: Preparar sua Fonte de Dados – **Export Data to Sheets** Simplificado

O modelo funciona com qualquer coleção que o Aspose possa iterar. Para este exemplo, usaremos um `List<Map<String,Object>>`, mas você também pode passar facilmente uma lista de POJOs.

```java
// Step 3: Prepare the data source (a list of maps, objects, etc.).
// Replace this with your actual data collection.
List<Map<String, Object>> dataList = getData(); // placeholder for your data
```

Aqui está uma implementação simulada rápida que você pode copiar‑colar durante os testes:

```java
private static List<Map<String, Object>> getData() {
    List<Map<String, Object>> list = new ArrayList<>();
    for (int i = 1; i <= 5; i++) {
        Map<String, Object> row = new HashMap<>();
        row.put("Data", "Row value " + i);
        list.add(row);
    }
    return list;
}
```

> **Por que um mapa?** Usar um mapa fornece pares chave‑valor que correspondem ao marcador `${Data}`. Se preferir POJOs, basta garantir que os nomes dos campos estejam alinhados com seus marcadores.

---

## Etapa 4: Inicializar o **SmartMarkerProcessor** – O Motor por Trás da Mágica

Agora que temos uma workbook e um modelo, precisamos do processador que os unirá.

```java
// Step 4: Initialise the SmartMarkerProcessor with the workbook
SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);
```

O processador lê o modelo, itera sobre `dataList` e cria uma nova planilha para cada entrada. Nenhum loop manual é necessário.

---

## Etapa 5: Aplicar o Modelo – **Insert Index Worksheet** e Gerar Planilhas

Neste ponto, você poderia simplesmente chamar `processor.apply(template, dataList);`. No entanto, muitos usuários também desejam uma **planilha de índice** que liste todos os nomes de planilhas geradas com links clicáveis. Abaixo está uma abordagem de duas etapas:

1. **Gerar as planilhas de dados** usando o modelo.
2. **Criar uma planilha de índice** e preenchê‑la com hyperlinks.

```java
// Step 5a: Apply the template to the data.
// A new worksheet is created for each element in dataList.
processor.apply(template, dataList);

// Step 5b (optional): Insert an index worksheet at the beginning.
Worksheet indexSheet = workbook.getWorksheets().add("Index");
int row = 0;
indexSheet.getCells().setColumnWidth(0, 25);
indexSheet.getCells().setColumnWidth(1, 30);
indexSheet.getCells().setRowHeight(row, 20);
indexSheet.getCells().get(row, 0).setValue("Sheet Name");
indexSheet.getCells().get(row, 1).setValue("Link");

// Loop through generated sheets and add a hyperlink entry.
for (int i = 0; i < dataList.size(); i++) {
    String sheetName = "Sheet" + (i + 1);
    row++;
    indexSheet.getCells().get(row, 0).setValue(sheetName);
    // Create a hyperlink that points to the generated worksheet.
    Hyperlink link = indexSheet.getHyperlinks().add(row, 1, 1, 1,
            "'" + sheetName + "'!A1", "Go to " + sheetName);
    indexSheet.getCells().get(row, 1).setValue("Open");
}
```

> **Explicação:**  
> - O loop constrói uma tabela organizada onde cada linha vincula à sua planilha correspondente.  
> - Usar `Hyperlink.add` garante uma referência clicável dentro do Excel.  
> - Esta etapa demonstra **insert index worksheet** em ação, tornando a navegação fácil para os usuários finais.

---

## Etapa 6: **Save Workbook Xlsx** – Uma Chamada, Pronta para Distribuição

Finalmente, grave a workbook no disco. O método `save` detecta automaticamente o formato do arquivo a partir da extensão.

```java
// Step 6: Save the workbook to a file
workbook.save("YOUR_DIRECTORY/output.xlsx");
System.out.println("Workbook saved successfully!");
```

> **Dica:** Se precisar transmitir o arquivo diretamente para uma resposta HTTP (por exemplo, em um controlador Spring), use `workbook.save(outputStream, SaveFormat.XLSX);` em vez disso.

---

## Exemplo Completo Funcional – Pronto para Copiar‑Colar

Abaixo está o programa completo que reúne todas as peças. Basta substituir `"YOUR_DIRECTORY"` por um caminho real em sua máquina.

```java
import com.aspose.cells.*;
import java.util.*;

public class MultiSheetExporter {
    public static void main(String[] args) throws Exception {
        // Initialise an empty workbook (Step 1)
        Workbook workbook = new Workbook();

        // Define the Smart Marker template (Step 2)
        String template = "${#WorksheetRepeat}Sheet${Index}\n${Data}";

        // Prepare data (Step 3)
        List<Map<String, Object>> dataList = getData();

        // Initialise the processor (Step 4)
        SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);

        // Apply template (Step 5a)
        processor.apply(template, dataList);

        // Optional: Insert an index worksheet (Step 5b)
        Worksheet indexSheet = workbook.getWorksheets().add("Index");
        int row = 0;
        indexSheet.getCells().setColumnWidth(0, 25);
        indexSheet.getCells().setColumnWidth(1, 30);
        indexSheet.getCells().setRowHeight(row, 20);
        indexSheet.getCells().get(row, 0).setValue("Sheet Name");
        indexSheet.getCells().get(row, 1).setValue("Link");

        for (int i = 0; i < dataList.size(); i++) {
            String sheetName = "Sheet" + (i + 1);
            row++;
            indexSheet.getCells().get(row, 0).setValue(sheetName);
            Hyperlink link = indexSheet.getHyperlinks().add(row, 1, 1, 1,
                    "'" + sheetName + "'!A1", "Go to " + sheetName);
            indexSheet.getCells().get(row, 1).setValue("Open");
        }

        // Save the workbook (Step 6)
        workbook.save("YOUR_DIRECTORY/output.xlsx");
        System.out.println("Workbook saved successfully!");
    }

    // Mock data generator
    private static List<Map<String, Object>> getData() {
        List<Map<String, Object>> list = new ArrayList<>();
        for (int i = 1; i <= 5; i++) {
            Map<String, Object> row = new HashMap<>();
            row.put("Data", "Row value " + i);
            list.add(row);
        }
        return list;
    }
}
```

**Saída esperada:**  
- Um arquivo `output.xlsx` contendo seis planilhas (`Index`, `Sheet1` … `Sheet5`).  
- A planilha `Index` lista cada nome de planilha gerada com um link “Open” clicável.  
- Cada `SheetX` contém uma única célula (`A1`) com “Row value X”.

---

## Perguntas Frequentes & Casos Limite

| Pergunta | Resposta |
|----------|----------|
| **Posso usar uma fonte CSV ou JSON em vez de um `List<Map>`?** | Absolutamente. O Smart Marker da Aspose funciona com qualquer coleção `Iterable`. Basta mapear os campos do seu JSON para os nomes dos marcadores. |
| **E se minha lista de dados estiver vazia?** | O processador não criará planilhas adicionais, mas a planilha de índice ainda será adicionada (você pode querer proteger contra isso). |
| **Como adiciono cabeçalhos ou estilos a cada planilha gerada?** | Estenda o modelo: `\"${#WorksheetRepeat}Sheet${Index}\\nHeader1,Header2\\n${Data}\"`. Você também pode aplicar um estilo programaticamente após `apply`. |
| **Existe um limite para o número de planilhas?** | Na prática, o Excel limita a 1.048.576 linhas por planilha; o número de planilhas é limitado apenas pela memória. |
| **Preciso de uma licença para o Aspose.Cells?** | Uma avaliação gratuita funciona para desenvolvimento. Para produção, uma licença remove a marca d'água de avaliação e desbloqueia todos os recursos. |

---

## Conclusão

Agora você tem um fluxo de trabalho sólido para **create multiple sheets** em Java que utiliza uma abordagem **template based Excel**, **exporta dados para planilhas**, opcionalmente **insere uma planilha de índice**, e finalmente **salva a workbook xlsx** com uma única linha de código. Esse padrão escala de forma elegante — de algumas linhas a exportações massivas de dados — mantendo seu código limpo e fácil de manter.

Pronto para o próximo passo? Experimente adicionar formatação condicional, incorporar gráficos ou mesclar o índice com um painel resumido. O mesmo mecanismo Smart Marker pode lidar com esses cenários com apenas alguns marcadores extras.

Se encontrar algum problema, deixe um comentário abaixo ou explore a extensa documentação do Aspose.Cells. Feliz codificação e aproveite a automação dessas planilhas!

## O que Você Deve Aprender a Seguir?

Os tutoriais a seguir abordam tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Criar e Acessar Planilhas Excel, Adicionar Marcadores PDF Usando Aspose.Cells para Java](/cells/english/java/workbook-operations/create-access-excel-sheets-add-pdf-bookmarks-aspose-cells-java/)
- [Exportar Planilhas Excel para Imagens Usando Aspose.Cells para Java - Um Guia Abrangente](/cells/english/java/workbook-operations/export-excel-sheets-images-aspose-cells-java/)
- [Como Criar e Exportar Excel para HTML Usando Aspose.Cells Java | Guia de Operações de Workbook](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}