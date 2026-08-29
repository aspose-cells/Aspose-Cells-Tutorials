---
category: general
date: 2026-08-20
description: Aprenda a exportar Excel para TXT limitando casas decimais, mantendo
  dígitos significativos e salvando a pasta de trabalho como TXT usando Java.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to txt
- limit decimal places
- keep significant digits
- save workbook as txt
language: pt
lastmod: 2026-08-20
og_description: Exportar Excel para TXT com Aspose.Cells. Este guia mostra como limitar
  casas decimais, manter dígitos significativos e salvar a pasta de trabalho como
  TXT em Java.
og_image_alt: Result of export excel to txt showing limited decimal places and kept
  significant digits
og_title: Exportar Excel para TXT em Java – controlar casas decimais e dígitos significativos
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Learn to export Excel to TXT while limiting decimal places, keeping
    significant digits, and saving workbook as TXT using Java.
  headline: How to export Excel to TXT with Aspose.Cells and control decimal precision
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel
- Text export
title: Como exportar Excel para TXT com Aspose.Cells e controlar a precisão decimal
url: /pt/java/excel-import-export/how-to-export-excel-to-txt-with-aspose-cells-and-control-dec/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como exportar Excel para TXT com Aspose.Cells e controlar a precisão decimal

Se você precisa **exportar Excel para TXT** e garantir que a saída respeite um número específico de casas decimais, este guia fornece uma solução completa. Você verá como limitar casas decimais, manter dígitos significativos e **salvar a pasta de trabalho como TXT** usando a biblioteca Aspose.Cells para Java.

O tutorial percorre a criação de uma pasta de trabalho, a inserção de um valor de alta precisão, a configuração das opções de salvamento TXT e a gravação do arquivo no disco. Ao final, você poderá gerar um arquivo de texto que contém exatamente a precisão que você necessita, sem processamento manual posterior.

## O que você precisará

- Java 17 (ou qualquer JDK suportado)
- Aspose.Cells for Java 23.10 ou mais recente
- Uma IDE ou ferramenta de build (Maven/Gradle) para gerenciar dependências
- Permissão de escrita no diretório de saída

## Etapa 1: Criar uma pasta de trabalho e acessar a primeira planilha

Criar uma pasta de trabalho é o primeiro passo quando você deseja **exportar Excel para TXT**. A classe `Workbook` representa o arquivo Excel completo, e `Worksheet` fornece acesso às células.

```java
import com.aspose.cells.*;

public class ExportExcelToTxtDemo {
    public static void main(String[] args) throws Exception {
        // Initialize a new workbook
        Workbook workbook = new Workbook();

        // Get the first worksheet (index 0)
        Worksheet sheet = workbook.getWorksheets().get(0);
```

*Por que isso importa*: O objeto workbook contém todos os dados, estilos e metadados. Começar com uma nova pasta de trabalho garante que nenhuma formatação oculta interfira na exportação de texto.

## Etapa 2: Adicionar um valor numérico e limitar casas decimais

Insira um número que possua muitas casas decimais para que você possa demonstrar como **limitar casas decimais** durante a exportação.

```java
        // Put a high‑precision number into cell A1
        sheet.getCells().putValue("A1", 0.000123456789);
```

*Por que isso importa*: O Excel armazena a precisão total, mas ao exportar posteriormente, você pode querer truncar ou arredondar o valor. A configuração `limit decimal places` tratará isso automaticamente.

## Etapa 3: Configurar as opções de salvamento TXT para manter dígitos significativos

Aspose.Cells fornece `TxtSaveOptions`. Definir `significantDigits` indica ao exportador que mantenha apenas o número necessário de dígitos significativos, ignorando zeros à esquerda.

```java
        // Configure TXT export options
        TxtSaveOptions txtOptions = new TxtSaveOptions();

        // Keep exactly 5 significant digits (e.g., 0.00012346)
        txtOptions.setSignificantDigits(5);
```

*Por que isso importa*: A opção **keep significant digits** garante que o arquivo de saída contenha uma quantidade previsível de precisão, o que é essencial para sistemas downstream que esperam um formato numérico de largura fixa.

## Etapa 4: Salvar a pasta de trabalho como TXT

Finalmente, grave a pasta de trabalho em um arquivo de texto. O método `save` respeita as opções configuradas, de modo que o arquivo resultante conterá a representação decimal limitada.

```java
        // Define the output path (replace with your own directory)
        String outputPath = "output/SignificantDigits.txt";

        // Export the workbook to TXT using the configured options
        workbook.save(outputPath, txtOptions);

        System.out.println("Export completed: " + outputPath);
    }
}
```

*Por que isso importa*: Usar **save workbook as txt** com o `TxtSaveOptions` preparado garante que o arquivo exportado corresponda às restrições de precisão definidas na etapa anterior.

### Conteúdo esperado de `SignificantDigits.txt`

```
0.00012346
```

O valor mostra cinco dígitos significativos (`12346`) após o arredondamento, e os zeros à esquerda são preservados de acordo com o formato TXT.

## Variações e casos extremos

| Cenário | Ajuste |
|----------|------------|
| **Different number of significant digits** | Call `txtOptions.setSignificantDigits(n)` where `n` is 1‑15. |
| **Exporting a range instead of the whole sheet** | Use `txtOptions.setExportRange("A1:B10")` before saving. |
| **Preserving column separators** | Set `txtOptions.setSeparator('\t')` for tab‑delimited output. |
| **Large worksheets** | Increase `txtOptions.setMemorySetting(MemorySetting.MEMORY_PREFERENCES)` to avoid `OutOfMemoryError`. |

## Armadilhas comuns e dicas profissionais

- **Não confunda dígitos significativos com casas decimais**. Zeros à esquerda não são contados como significativos; use `setSignificantDigits` para precisão significativa e `setDecimalPlaces` se precisar de um número fixo de dígitos após o ponto decimal.
- **Sempre especifique um caminho de saída absoluto** ao executar a partir de uma IDE para evitar erros de permissão.
- **Valide o arquivo gerado** com uma chamada simples `java.nio.file.Files.readAllLines(Paths.get(outputPath))` para garantir que o conteúdo corresponda às expectativas antes de enviá‑lo aos processos downstream.

## Código‑fonte completo para referência

```java
import com.aspose.cells.*;

public class ExportExcelToTxtDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Step 2: Insert a high‑precision number (will be limited later)
        sheet.getCells().putValue("A1", 0.000123456789);

        // Step 3: Set TXT options – keep 5 significant digits
        TxtSaveOptions txtOptions = new TxtSaveOptions();
        txtOptions.setSignificantDigits(5);   // keep significant digits

        // Step 4: Save the workbook as TXT
        String outputPath = "output/SignificantDigits.txt";
        workbook.save(outputPath, txtOptions);

        System.out.println("Export completed: " + outputPath);
    }
}
```

Executar o programa produz `SignificantDigits.txt` contendo a única linha `0.00012346`, demonstrando que o processo de **export excel to txt** respeita tanto os requisitos de **limit decimal places** quanto **keep significant digits**.

## Conclusão

Agora você sabe como **exportar Excel para TXT** usando Aspose.Cells para Java enquanto controla a precisão numérica. Configurando `TxtSaveOptions`, você pode **limitar casas decimais**, **manter dígitos significativos** e, de forma confiável, **salvar a pasta de trabalho como txt** sem processamento adicional posterior.

Next, you might explore:

- Exportar várias planilhas para arquivos TXT separados (`save workbook as txt` por planilha)
- Usar `setSeparator` para criar saída compatível com CSV
- Automatizar conversões em lote para grandes conjuntos de dados

Sinta‑se à vontade para experimentar diferentes contagens de dígitos e separadores para atender às necessidades exatas do seu projeto. Feliz codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Como criar e exportar Excel para HTML usando Aspose.Cells Java | Guia de operações de pasta de trabalho](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Salvar Excel como Texto – Guia completo em C# para exportar Excel para TXT](/cells/english/net/converting-excel-files-to-other-formats/save-excel-as-text-complete-c-guide-to-export-excel-to-txt/)
- [Exportar Excel Workbook como Imagem Usando Aspose.Cells para Java&#58; Um Guia Passo a Passo](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}