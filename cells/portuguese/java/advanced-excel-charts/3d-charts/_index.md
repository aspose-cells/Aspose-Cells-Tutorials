---
date: 2026-08-21
description: Aprenda como exportar chart como image e criar 3D pie charts em Java
  com Aspose.Cells. Gere 3D bar charts, adicione 3D charts ao Excel e salve workbooks
  como XLSX.
keywords:
- export chart as image
- 3d pie chart java
- 3d bar chart java
- save workbook as xlsx
- add 3d chart excel
lastmod: 2026-08-21
linktitle: Criar 3D Pie Chart Java
og_description: Exportar chart como image e criar 3D pie charts em Java usando Aspose.Cells.
  Guia passo a passo para gerar 3D bar e pie charts, personalizá‑los e salvar workbooks
  como XLSX.
og_image_alt: Developer guide showing how to export a 3D chart as an image with Aspose.Cells
  for Java
og_title: Exportar chart como image e criar 3D pie chart em Java
schemas:
- author: Aspose
  dateModified: '2026-08-21'
  description: Learn how to export chart as image and create 3D pie charts in Java
    with Aspose.Cells. Generate 3D bar charts, add 3D charts to Excel, and save workbooks
    as XLSX.
  headline: How to export chart as image and create 3D pie chart in Java
  type: TechArticle
- questions:
  - answer: Use `chart.getNSeries().add()` for each series range and ensure the chart
      type remains 3‑D (e.g., `ChartType.BAR_3_D` or `ChartType.PIE_3_D`).
    question: How can I add multiple data series to a 3D chart?
  - answer: Yes, you can save the chart as PNG, JPEG, or PDF by calling the appropriate
      `chart.toImage()` overload or `workbook.save()` with an image or PDF format,
      satisfying the **convert chart png** requirement.
    question: Can I export 3D charts created with Aspose.Cells for Java to other formats?
  - answer: Aspose.Cells focuses on static Excel charts. For interactive web‑based
      3‑D visualizations, consider coupling Excel data with JavaScript libraries such
      as Three.js.
    question: Is it possible to create interactive 3D charts with Aspose.Cells for
      Java?
  - answer: Absolutely. Load new data into the worksheet programmatically and refresh
      the chart range; the next time the workbook is opened, the chart reflects the
      updated values.
    question: Can I automate the process of updating data in my 3D charts?
  - answer: 'You can find comprehensive documentation and resources for Aspose.Cells
      for Java at the website: [Aspose.Cells for Java Documentation](https://reference.aspose.com/cells/java/).'
    question: Where can I find more resources and documentation for Aspose.Cells for
      Java?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- export chart as image
- 3d pie chart
- Aspose.Cells Java
- Excel chart automation
title: Como exportar chart como image e criar 3D pie chart em Java
url: /pt/java/advanced-excel-charts/3d-charts/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Criar gráfico de pizza 3D Java

## Introdução aos gráficos 3D

Aspose.Cells for Java é uma poderosa API Java para trabalhar com arquivos Excel, e facilita a **create 3d pie chart** de projetos, bem como visualizações clássicas de barras 3‑D. Neste tutorial você verá exatamente como **export chart as image**, gerar um gráfico de barras 3‑D, adaptar a mesma abordagem para um gráfico de pizza 3‑D, personalizar aparências e, finalmente, **add 3d chart excel** aos seus relatórios. Seja construindo um painel financeiro, uma planilha de desempenho de vendas ou visualizando dados científicos, os passos abaixo lhe darão uma base sólida.

## Respostas rápidas
- **Qual biblioteca eu preciso?** Aspose.Cells for Java (latest version)  
- **Posso gerar um gráfico de barras 3D?** Yes – use `ChartType.BAR_3_D`  
- **Preciso de uma licença?** A valid license removes evaluation limits  
- **Quais versões do Excel são suportadas?** All major versions from 2003 to 2023  
- **É possível exportar o gráfico como imagem?** Yes – call `chart.toImage()` after the chart is created  

## O que são gráficos 3D?
Gráficos 3D adicionam profundidade às visualizações 2D tradicionais, ajudando os espectadores a compreender relações multidimensionais de forma mais intuitiva. Eles são especialmente úteis quando você precisa comparar várias categorias lado a lado, mantendo uma hierarquia visual clara. Ao adicionar uma terceira dimensão, esses gráficos podem destacar diferenças de magnitude que podem ser menos óbvias em representações planas, facilitando a interpretação de dados complexos para as partes interessadas de negócios.

## Por que usar Aspose.Cells for Java para gerar gráfico de barras 3D?
Aspose.Cells for Java oferece mais de 150 tipos de gráficos incorporados e suporta mais de 100 funções do Excel, proporcionando um mecanismo completo que funciona em todas as versões do Excel de 2003 a 2023 sem exigir o Microsoft Office. Isso significa que você pode **generate 3d bar chart** objetos programaticamente com resultados previsíveis e sobrecarga mínima.

## Configurando Aspose.Cells for Java

### Download e instalação
Você pode baixar a biblioteca Aspose.Cells for Java no site oficial. Siga as instruções fornecidas para Maven/Gradle ou adicione o JAR diretamente ao classpath do seu projeto.

### Inicialização da licença
A classe `License` é usada para aplicar sua licença Aspose.Cells e desbloquear a funcionalidade completa.  
```java
// Initialize Aspose.Cells license
License license = new License();
license.setLicense("path_to_license_file.xml");
```

## Criando um gráfico 3D básico

### Importando bibliotecas necessárias
Primeiro, traga as classes necessárias para o escopo:  
```java
import com.aspose.cells.*;
```

### Inicializando uma pasta de trabalho
Crie uma nova pasta de trabalho que hospedará o gráfico:  
```java
Workbook workbook = new Workbook();
```

### Adicionando dados ao gráfico
Preencha a planilha com dados de exemplo que o gráfico referenciará:  
```java
Worksheet worksheet = workbook.getWorksheets().get(0);

// Adding data to cells
worksheet.getCells().get("A1").putValue("Category");
worksheet.getCells().get("A2").putValue("A");
worksheet.getCells().get("A3").putValue("B");
worksheet.getCells().get("A4").putValue("C");

worksheet.getCells().get("B1").putValue("Value");
worksheet.getCells().get("B2").putValue(10);
worksheet.getCells().get("B3").putValue(20);
worksheet.getCells().get("B4").putValue(30);
```

## Como gerar gráfico de barras 3D em Java
Para criar um gráfico de barras 3D, você adiciona um objeto de gráfico à planilha, define seu tipo como `ChartType.BAR_3_D` e então vincula a série de dados às células que contêm seus valores. Após configurar a aparência do gráfico, você pode renderiz‑lo ou exportá‑lo conforme necessário.  
```java
int chartIndex = worksheet.getCharts().add(ChartType.BAR_3_D, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);

// Setting the data range for the chart
chart.getNSeries().add("A2:B4", true);

// Customizing chart attributes
chart.getChartArea().getBorder().setVisible(false);
chart.getChartTitle().setText("3D Bar Chart");
```

## Salvando o gráfico em um arquivo
Finalmente, grave a pasta de trabalho (que agora contém o gráfico 3‑D) no disco. Isso também **save workbook xlsx** no formato padrão do Excel:  
```java
workbook.save("3D_Chart.xlsx");
```

## Como criar gráfico de pizza 3D com Aspose.Cells for Java
Se você precisar de uma visualização no estilo de pizza, o fluxo de trabalho é quase idêntico — apenas o enum `ChartType` muda. Substitua `ChartType.BAR_3_D` por `ChartType.PIE_3_D` ao adicionar o gráfico e aponte a série para o mesmo intervalo de dados. Após o gráfico ser criado, você pode definir um título descritivo, ajustar as cores das fatias e exportar o resultado como imagem. Essa abordagem permite reutilizar o mesmo código de preparação de dados enquanto oferece uma perspectiva visual diferente.  

## Como exportar gráfico como imagem em Java
O método `toImage` do objeto `Chart` salva o gráfico como um arquivo de imagem. Você pode exportar qualquer gráfico 3D para uma imagem raster com uma única chamada: `chart.toImage("myChart.png", ImageFormat.getPng())`. Esse método renderiza o gráfico exatamente como aparece no Excel, preservando a profundidade 3‑D, cores e legendas, e grava a saída no caminho de arquivo especificado. Use PNG para qualidade sem perdas ou JPEG para tamanhos de arquivo menores ao incorporar a imagem em relatórios web.

## Tipos diferentes de gráficos 3D
Aspose.Cells for Java suporta várias variedades de gráficos 3D que você pode **add 3d chart excel** arquivos com:

- **Bar charts** – ideal para comparar categorias.  
- **Pie charts** – mostram contribuições proporcionais (incluindo pizza 3D).  
- **Line charts** – ilustram tendências ao longo do tempo.  
- **Area charts** – enfatizam a magnitude da mudança.

## Personalização avançada de gráficos

### Adicionando títulos e rótulos
Dê contexto ao seu gráfico definindo um título descritivo e rótulos de eixo.

### Ajustando cores e estilos
Use o método `chart.getSeries().get(i).getArea().setForegroundColor(Color.getRGB(...))` para combinar com a identidade visual corporativa.

### Trabalhando com eixos do gráfico
Ajuste fino das escalas dos eixos, intervalos e marcas de graduação para melhorar a legibilidade.

### Adicionando legendas
Habilite legendas com `chart.getLegend().setVisible(true)` para que os espectadores possam identificar cada série de dados.

### Exportando gráficos como imagens
Quando precisar de uma imagem estática para um relatório web, chame `chart.toImage("chart.png", ImageFormat.getPng())`. Isso atende ao caso de uso **convert chart png** sem sair da pasta de trabalho.

## Integração de dados
Aspose.Cells for Java pode extrair dados de bancos de dados, arquivos CSV ou APIs ao vivo. Basta preencher as células da planilha com os dados obtidos antes de vincular o intervalo ao gráfico. Isso mantém seu fluxo de trabalho **add 3d chart excel** dinâmico e atualizado.

## Conclusão
Neste guia, percorremos como **create 3d pie chart** e **create 3d bar chart** projetos do início ao fim — configurando a biblioteca, adicionando dados, gerando um gráfico de barras 3‑D, adaptando os mesmos passos para um gráfico de pizza 3‑D e aplicando estilos avançados. Com Aspose.Cells for Java, você tem uma maneira confiável e independente de versão para incorporar visualizações ricas em 3‑D diretamente em pastas de trabalho Excel e até **export chart as image** para uso em painéis ou relatórios.

## Perguntas frequentes

**Q: Como posso adicionar várias séries de dados a um gráfico 3D?**  
A: Use `chart.getNSeries().add()` para cada intervalo de série e garanta que o tipo de gráfico permaneça 3‑D (por exemplo, `ChartType.BAR_3_D` ou `ChartType.PIE_3_D`).

**Q: Posso exportar gráficos 3D criados com Aspose.Cells for Java para outros formatos?**  
A: Sim, você pode salvar o gráfico como PNG, JPEG ou PDF chamando a sobrecarga apropriada de `chart.toImage()` ou `workbook.save()` com um formato de imagem ou PDF, atendendo ao requisito **convert chart png**.

**Q: É possível criar gráficos 3D interativos com Aspose.Cells for Java?**  
A: Aspose.Cells foca em gráficos estáticos do Excel. Para visualizações 3‑D interativas baseadas na web, considere combinar os dados do Excel com bibliotecas JavaScript como Three.js.

**Q: Posso automatizar o processo de atualização de dados nos meus gráficos 3D?**  
A: Absolutamente. Carregue novos dados na planilha programaticamente e atualize o intervalo do gráfico; na próxima vez que a pasta de trabalho for aberta, o gráfico refletirá os valores atualizados.

**Q: Onde posso encontrar mais recursos e documentação para Aspose.Cells for Java?**  
A: Você pode encontrar documentação abrangente e recursos para Aspose.Cells for Java no site: [Aspose.Cells for Java Documentation](https://reference.aspose.com/cells/java/).

---

**Última atualização:** 2026-08-21  
**Testado com:** Aspose.Cells for Java 24.12 (latest)  
**Autor:** Aspose

## Tutoriais Relacionados

- [Criar gráficos de pizza no Excel usando Aspose.Cells for Java: um guia abrangente](/cells/java/charts-graphs/master-pie-chart-creation-excel-aspose-cells-java/)
- [aspose cells java – criar gráfico Excel com anotações](/cells/java/advanced-excel-charts/chart-annotations/)
- [Adicionar rótulos de dados ao gráfico Excel com Aspose.Cells Java](/cells/java/advanced-excel-charts/chart-interactivity/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}