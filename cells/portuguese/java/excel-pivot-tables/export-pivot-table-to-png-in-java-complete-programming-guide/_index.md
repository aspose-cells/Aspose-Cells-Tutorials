---
category: general
date: 2026-06-27
description: Exportar tabela dinâmica como imagem do Excel em Java. Aprenda como definir
  o formato PNG, configurar opções e salvar o arquivo em apenas alguns passos.
draft: false
keywords:
- export pivot table
- excel pivot image
- set png format
language: pt
og_description: Exportar a tabela dinâmica como uma imagem de pivô do Excel usando
  Java. Este guia mostra como definir o formato PNG e salvar a imagem com confiança.
og_title: Exportar tabela dinâmica para PNG em Java – Guia passo a passo
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Export pivot table as an Excel pivot image in Java. Learn how to set
    PNG format, configure options, and save the file in just a few steps.
  headline: Export pivot table to PNG in Java – Complete Programming Guide
  type: TechArticle
tags:
- Java
- Aspose.Cells
- Excel Automation
title: Exportar tabela dinâmica para PNG em Java – Guia completo de programação
url: /pt/java/excel-pivot-tables/export-pivot-table-to-png-in-java-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exportar tabela dinâmica para PNG em Java – Guia de Programação Completo

Já precisou **exportar uma tabela dinâmica** de uma pasta de trabalho Excel, mas não sabia como obter um arquivo de imagem limpo? Você não está sozinho — muitos desenvolvedores encontram essa barreira ao criar painéis de relatórios. A boa notícia é que, com algumas linhas de código Java, você pode transformar qualquer tabela dinâmica em uma nítida **imagem de tabela dinâmica do Excel** salva como PNG.  

Neste tutorial vamos percorrer todo o processo: ler a pasta de trabalho, localizar a primeira tabela dinâmica, configurar a exportação para **definir o formato PNG**, e finalmente gravar a imagem no disco. Ao final, você terá um trecho reutilizável que pode ser inserido em qualquer projeto.

## O que você vai aprender

- Como carregar um arquivo Excel com Aspose.Cells (ou Apache POI, se preferir).  
- As chamadas de API exatas necessárias para **exportar tabela dinâmica** como PNG.  
- Por que definir o formato da imagem importa e como **definir o formato PNG** corretamente.  
- Armadilhas comuns — como lidar com múltiplas tabelas dinâmicas ou planilhas ausentes — e como evitá‑las.  
- Um exemplo Java completo, pronto‑para‑executar, que você pode copiar‑colar.

> **Pré‑requisitos**  
> • Java 17 ou superior (o código funciona em versões anteriores, mas 17 é recomendado).  
> • Biblioteca Aspose.Cells for Java (a versão de avaliação funciona perfeitamente).  
> • Familiaridade básica com arquivos Excel e I/O em Java.

---

## Etapa 1: Adicionar a dependência Aspose.Cells

Se você usa Maven, insira a dependência a seguir no seu `pom.xml`. Caso contrário, baixe o JAR no site da Aspose e adicione‑o ao seu classpath.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- latest as of June 2026 -->
</dependency>
```

*Dica:* Mantenha as versões das suas bibliotecas sincronizadas com as notas de lançamento oficiais para evitar bugs inesperados.

## Etapa 2: Carregar a pasta de trabalho e localizar a tabela dinâmica

Primeiro abrimos o arquivo Excel, depois buscamos a primeira tabela dinâmica na primeira planilha. Se a pasta de trabalho não contiver tabelas dinâmicas, encerramos o processo de forma elegante.

```java
import com.aspose.cells.*;

public class PivotTableExporter {

    public static void main(String[] args) {
        try {
            // Load the workbook (replace with your actual path)
            Workbook workbook = new Workbook("C:/data/report.xlsx");

            // Access the first worksheet – you can also loop through all sheets
            Worksheet ws = workbook.getWorksheets().get(0);

            // Verify that the sheet actually contains pivot tables
            if (ws.getPivotTables().getCount() == 0) {
                System.out.println("No pivot tables found on the first sheet.");
                return;
            }

            // Retrieve the first pivot table (this is the target for export)
            PivotTable pivotTable = ws.getPivotTables().get(0);
```

> **Por que esta etapa é importante** – O objeto `PivotTable` é o ponto de entrada para qualquer exportação de imagem. Tentar chamar `toImage` em uma tabela dinâmica inexistente lançará um `NullPointerException`, por isso verificamos a contagem primeiro.

## Etapa 3: Configurar as opções de exportação de imagem (Definir formato PNG)

Agora criamos uma instância de `ImageOrPrintOptions` e **definimos explicitamente o formato PNG**. PNG é sem perdas, o que preserva a nitidez das linhas de grade e das fontes.

```java
            // Step 3: Configure image export options – we want PNG
            ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
            imgOptions.setImageFormat(ImageFormat.PNG);   // <-- set png format
            imgOptions.setOnePagePerSheet(true);          // optional: force single‑page output
            imgOptions.setTransparent(true);              // optional: keep background transparent
```

*Observação:* Se precisar de JPEG, basta substituir `ImageFormat.PNG` por `ImageFormat.JPEG`. O mesmo objeto de opções funciona para ambos.

## Etapa 4: Exportar a tabela dinâmica como arquivo de imagem

Com as opções prontas, chamamos `toImage`. O método grava o arquivo diretamente, sem necessidade de streams adicionais.

```java
            // Step 4: Export the pivot table as an image file
            String outputPath = "C:/exports/pivot.png";
            pivotTable.toImage(outputPath, imgOptions);

            System.out.println("Pivot table exported successfully to: " + outputPath);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

Executar o programa gera um arquivo chamado `pivot.png` que tem exatamente a mesma aparência da tabela dinâmica no Excel. Abra‑o com qualquer visualizador de imagens para conferir.

### Saída esperada

```
Pivot table exported successfully to: C:/exports/pivot.png
```

A imagem resultante corresponderá ao layout exibido na tela, incluindo larguras de coluna, alturas de linha e qualquer formatação condicional que você tenha aplicado.

## Manipulando múltiplas tabelas dinâmicas (Avançado)

E se sua planilha contiver várias tabelas dinâmicas e você quiser apenas uma específica? Você pode percorrer `ws.getPivotTables()` e selecionar pelo nome:

```java
PivotTable target = null;
for (int i = 0; i < ws.getPivotTables().getCount(); i++) {
    PivotTable pt = ws.getPivotTables().get(i);
    if ("SalesByRegion".equals(pt.getName())) {
        target = pt;
        break;
    }
}
if (target == null) {
    System.out.println("Desired pivot table not found.");
    return;
}
target.toImage("C:/exports/sales_by_region.png", imgOptions);
```

*Por que isso é útil*: Em relatórios reais você costuma ter uma tabela dinâmica resumida e outra detalhada. Selecionar pelo nome evita sobrescritas acidentais.

## Armadilhas comuns & Como evitá‑las

| Problema | Sintoma | Solução |
|------|----------|-----|
| **Planilha ausente** | `IndexOutOfBoundsException` ao acessar `ws` | Verifique `workbook.getWorksheets().getCount() > 0` antes de indexar. |
| **Nenhuma tabela dinâmica** | Falha silenciosa ou imagem vazia | Use a verificação `ws.getPivotTables().getCount()` (veja a Etapa 2). |
| **Formato de imagem incorreto** | Saída borrada ou com artefatos | Sempre `setImageFormat(ImageFormat.PNG)` para saída sem perdas; evite JPEG para tabelas com muito texto. |
| **Caminho de arquivo não gravável** | `IOException` em `toImage` | Garanta que o diretório exista (`new File(outputPath).getParentFile().mkdirs()`). |

## Dica de especialista: Exportar para um array de bytes em aplicações web

Se você está construindo um serviço web que devolve o PNG diretamente ao navegador, pode gravar em um `ByteArrayOutputStream` em vez de um arquivo:

```java
ByteArrayOutputStream baos = new ByteArrayOutputStream();
pivotTable.toImage(baos, imgOptions);
byte[] pngBytes = baos.toByteArray();
// Send pngBytes as HTTP response with Content-Type: image/png
```

Isso elimina a necessidade de arquivos temporários e acelera a resposta.

---

## Exemplo completo (Todas as etapas combinadas)

A seguir está o programa completo, pronto‑para‑copiar‑e‑colar, que inclui todas as boas práticas discutidas.

```java
import com.aspose.cells.*;
import java.io.*;

public class PivotTableExporter {

    public static void main(String[] args) {
        // 1️⃣ Load workbook
        Workbook workbook;
        try {
            workbook = new Workbook("C:/data/report.xlsx");
        } catch (Exception e) {
            System.err.println("Failed to load workbook: " + e.getMessage());
            return;
        }

        // 2️⃣ Get first worksheet and ensure a pivot exists
        if (workbook.getWorksheets().getCount() == 0) {
            System.out.println("Workbook contains no worksheets.");
            return;
        }
        Worksheet ws = workbook.getWorksheets().get(0);
        if (ws.getPivotTables().getCount() == 0) {
            System.out.println("No pivot tables on the first sheet.");
            return;
        }
        PivotTable pivotTable = ws.getPivotTables().get(0); // export pivot table

        // 3️⃣ Configure export options – set png format
        ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
        imgOptions.setImageFormat(ImageFormat.PNG); // <-- set png format
        imgOptions.setOnePagePerSheet(true);
        imgOptions.setTransparent(true);

        // 4️⃣ Prepare output directory
        String outDir = "C:/exports";
        new File(outDir).mkdirs(); // create if missing

        // 5️⃣ Export the image
        String outPath = outDir + "/pivot.png";
        try {
            pivotTable.toImage(outPath, imgOptions);
            System.out.println("Pivot table exported successfully to: " + outPath);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

Executar esta classe gerará `pivot.png` dentro de `C:/exports`. Abra o arquivo e você verá uma réplica visual exata da tabela dinâmica original — perfeito para incorporar em relatórios, e‑mails ou páginas web.

![Exported pivot table saved as PNG – example of an excel pivot image](https://example.com/images/pivot-export.png "export pivot table example")

*Texto alternativo da imagem:* **exemplo de exportação de tabela dinâmica mostrando uma imagem PNG de tabela dinâmica do Excel**

---

## Conclusão

Acabamos de mostrar como **exportar tabela dinâmica** do Excel para um PNG de alta qualidade usando Java. Os passos chave são carregar a pasta de trabalho, localizar a tabela dinâmica, configurar `ImageOrPrintOptions` para **definir o formato PNG**, e finalmente chamar `toImage`.  

Com esse conhecimento, você pode automatizar a geração de relatórios, incorporar instantâneos de tabelas dinâmicas em painéis, ou servi‑los diretamente de uma API web. Em seguida, você pode explorar opções de dimensionamento da **imagem de tabela dinâmica do Excel**, adicionar marcas d'água, ou até converter o PNG para PDF para relatórios imprimíveis.  

Tem dúvidas sobre como lidar com pastas de trabalho maiores ou integrar com Spring Boot? Deixe um comentário abaixo, e feliz codificação!

## O que aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [Como Atualizar a Fonte da Tabela Dinâmica do Excel com Aspose.Cells para Java: Um Guia Abrangente](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Automatizar Estilização e Salvamento de Tabela Dinâmica do Excel com Aspose.Cells para Java: Um Guia Abrangente](/cells/english/java/data-analysis/excel-pivot-table-styling-saving-aspose-cells-java/)
- [Manipulação de Tabela Dinâmica do Excel com Aspose.Cells Java: Um Guia Abrangente](/cells/english/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}