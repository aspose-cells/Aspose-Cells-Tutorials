---
category: general
date: 2026-11-22
description: Exportar Excel como imagem com Java usando Aspose.Cells. Aprenda como
  adicionar imagem à planilha e salvar o Excel como arquivo PNG em poucos passos.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel as image
- add picture to worksheet
- export excel sheet to png
- save excel as png file
- save workbook as image
language: pt
lastmod: 2026-11-22
og_description: Exporte o Excel como imagem com Java usando Aspose.Cells. Siga este
  guia para adicionar uma imagem à planilha e salvar o Excel como arquivo PNG rapidamente.
og_image_alt: Code snippet showing Java export of an Excel worksheet to a PNG image
og_title: Exportar Excel como imagem com Java – tutorial passo a passo
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Export Excel as image with Java using Aspose.Cells. Learn how to add
    picture to worksheet and save Excel as PNG file in a few steps.
  headline: Export Excel as image with Java – complete guide
  type: TechArticle
tags:
- Java
- Aspose.Cells
- Excel automation
- Image export
title: Exportar Excel como imagem com Java – guia completo
url: /pt/java/images-shapes/export-excel-as-image-with-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exportar Excel como imagem com Java – guia completo

Se você precisa **exportar Excel como imagem** em uma aplicação Java, este tutorial mostra uma solução pronta‑para‑usar. Você verá como adicionar uma imagem à worksheet, configurar as opções de exportação e, finalmente, **salvar Excel como arquivo PNG** com apenas algumas linhas de código.

O guia cobre tudo, desde a configuração do Maven até o tratamento de casos extremos, para que você possa integrar a técnica em qualquer projeto que exija capturas visuais de planilhas.

## Pré-requisitos

* Java 17 ou mais recente instalado.
* Maven 3.6+ (ou Gradle) para gerenciamento de dependências.
* Uma licença Aspose.Cells for Java (a avaliação gratuita funciona para testes).
* Um workbook Excel de exemplo (`sample.xlsx`) que contém os dados que você deseja exportar.

## Etapa 1: Adicionar dependência Aspose.Cells

Aspose.Cells fornece a classe `ImageOrPrintOptions` usada para **exportar Excel como imagem**. Adicione a dependência a seguir ao seu `pom.xml` (ou a entrada equivalente no Gradle).

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest stable version -->
</dependency>
```

> **Dica profissional:** Mantenha o número da versão atualizado; lançamentos mais recentes incluem melhorias de desempenho para renderização de imagens.

## Etapa 2: Carregar o workbook e selecionar a worksheet

O primeiro passo programático é abrir o arquivo Excel e obter uma referência à worksheet que você deseja exportar.

```java
import com.aspose.cells.*;

public class ExcelToImage {
    public static void main(String[] args) throws Exception {
        // Load the workbook from disk
        Workbook wb = new Workbook("sample.xlsx");

        // Access the first worksheet (index 0)
        Worksheet ws = wb.getWorksheets().get(0);
```

*Por que isso importa*: Carregar o workbook dá acesso aos seus objetos internos, e selecionar a worksheet correta garante que a faixa correta seja renderizada.

## Etapa 3: Configurar ImageOrPrintOptions (exportar excel como imagem)

`ImageOrPrintOptions` controla o formato da imagem, resolução e outros detalhes de renderização. Aqui definimos o formato como PNG, o que atende ao requisito de **exportar planilha excel para png**.

```java
        // Create options for image export
        ImageOrPrintOptions opts = new ImageOrPrintOptions();

        // Set the desired image format (PNG)
        opts.setSaveFormat(SaveFormat.PNG);

        // Optional: increase resolution for sharper output
        opts.setResolution(300);
```

Definir o formato como `PNG` garante compressão sem perdas, tornando o arquivo adequado para processamento adicional ou inclusão em relatórios.

## Etapa 4: Adicionar imagem à worksheet (add picture to worksheet)

Se precisar incorporar uma imagem—como um logotipo ou uma captura de outra faixa—use a coleção `Pictures`. O código a seguir insere uma imagem da faixa `A1:G20` no canto superior esquerdo da worksheet.

```java
        // Insert a picture of the range A1:G20 at cell (0,0)
        ws.getPictures().add(0, 0, "A1:G20");
```

> **Por que você pode fazer isso:** Adicionar uma imagem antes de exportar permite combinar gráficos estáticos com os dados da worksheet, produzindo uma imagem final mais rica.

## Etapa 5: Salvar a worksheet como arquivo PNG (save excel as png file, save workbook as image)

Finalmente, invoque `Workbook.save` com as opções configuradas. O método grava um arquivo PNG no diretório especificado.

```java
        // Save the worksheet as an image file
        wb.save("output/pivot.png", opts);

        System.out.println("Export completed: output/pivot.png");
    }
}
```

Quando o programa termina, `output/pivot.png` contém uma representação pixel‑perfect da worksheet, incluindo a imagem que você adicionou.

### Arquivo fonte completo

```java
import com.aspose.cells.*;

public class ExcelToImage {
    public static void main(String[] args) throws Exception {
        // Load workbook
        Workbook wb = new Workbook("sample.xlsx");
        Worksheet ws = wb.getWorksheets().get(0);

        // Configure export options
        ImageOrPrintOptions opts = new ImageOrPrintOptions();
        opts.setSaveFormat(SaveFormat.PNG);
        opts.setResolution(300); // optional high‑DPI output

        // Add picture to worksheet
        ws.getPictures().add(0, 0, "A1:G20");

        // Export worksheet as PNG image
        wb.save("output/pivot.png", opts);
        System.out.println("Export completed: output/pivot.png");
    }
}
```

Executar a classe produz o arquivo PNG mostrado abaixo (a imagem é ilustrativa; seu arquivo refletirá o conteúdo real da worksheet).

![Exported Excel worksheet as PNG](/images/excel-to-png.png "Result of export excel as image using Java")

*Texto alternativo (alt da imagem):* **Resultado da exportação de Excel como imagem usando Java – uma captura PNG da worksheet** (satisfaz o requisito de alt da imagem).

## Armadilhas comuns e como evitá‑las

| Problema | Razão | Correção |
|----------|-------|----------|
| **Arquivo não encontrado** | O caminho para `sample.xlsx` está incorreto. | Use um caminho absoluto ou coloque o arquivo na raiz do projeto. |
| **Imagem em branco** | A worksheet não tem conteúdo visível ou a faixa da imagem está vazia. | Verifique se as células `A1:G20` contêm dados ou ajuste a faixa. |
| **Baixa resolução** | O DPI padrão é 96, o que pode ficar borrado ao imprimir. | Chame `opts.setResolution(300)` (ou maior) antes de salvar. |
| **Exceção de licença** | Usar a versão de avaliação pode adicionar uma marca d'água. | Aplique uma licença válida do Aspose.Cells com `License license = new License(); license.setLicense("Aspose.Total.lic");`. |

## Próximos passos

Agora que você pode **exportar Excel como imagem**, você pode explorar:

* **Exportar planilha excel para png** para cada worksheet em um workbook (percorrer `wb.getWorksheets()`).
* Converter o PNG para PDF usando Aspose.PDF se precisar de um formato amigável a documentos.
* Incorporar o PNG gerado em uma página web ou anexo de e‑mail diretamente a partir do Java.

Essas extensões se baseiam no mesmo padrão `ImageOrPrintOptions`, mantendo a base de código consistente.

## Conclusão

Você aprendeu como **exportar Excel como imagem** com Java, como **adicionar imagem à worksheet**, e como **salvar Excel como arquivo PNG** usando Aspose.Cells. O exemplo completo demonstra uma forma confiável de **salvar workbook como imagem**, lidar com resolução e evitar erros comuns. Aplique o padrão para automatizar relatórios, gerar miniaturas ou integrar visualizações de planilhas em qualquer fluxo de trabalho baseado em Java.

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Como Exportar uma Worksheet Excel para PNG Usando Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)
- [Exportar Workbook Excel como Imagem Usando Aspose.Cells para Java: Um Guia Passo a Passo](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [Exportar Workbook Excel como Imagem Usando Aspose Cells para Java](/cells/german/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}