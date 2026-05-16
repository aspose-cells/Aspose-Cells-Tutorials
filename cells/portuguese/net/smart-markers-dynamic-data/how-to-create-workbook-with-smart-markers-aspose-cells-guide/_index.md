---
category: general
date: 2026-02-23
description: Como criar uma pasta de trabalho usando Aspose.Cells e adicionar marcadores
  com um array JSON. Aprenda como adicionar marcadores, usar array JSON e marcadores
  inteligentes do Aspose.Cells em minutos.
draft: false
keywords:
- how to create workbook
- how to add markers
- use json array
- smart markers aspose.cells
language: pt
og_description: Como criar uma pasta de trabalho usando Aspose.Cells, adicionar marcadores
  e usar um array JSON. Este guia passo a passo mostra tudo o que você precisa.
og_title: Como criar uma pasta de trabalho com marcadores inteligentes – Aspose.Cells
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Como criar uma pasta de trabalho com marcadores inteligentes – Guia Aspose.Cells
url: /pt/net/smart-markers-dynamic-data/how-to-create-workbook-with-smart-markers-aspose-cells-guide/
---

Trabalho com Marcadores Inteligentes – Guia Aspose.Cells"

Proceed.

Make sure to keep bold formatting.

Translate.

Let's write.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Criar uma Pasta de Trabalho com Marcadores Inteligentes – Guia Aspose.Cells

Já se perguntou **como criar uma pasta de trabalho** que preenche automaticamente os dados a partir de uma fonte JSON? Você não está sozinho—desenvolvedores perguntam constantemente como adicionar marcadores que extraem valores de arrays, especialmente ao trabalhar com Aspose.Cells. A boa notícia? É bem simples depois que você entende o conceito de smart‑marker. Neste tutorial vamos percorrer a criação de uma pasta de trabalho, a adição de marcadores, o uso de um array JSON e a configuração de smart markers no Aspose.Cells para que você possa gerar arquivos Excel dinamicamente.

Vamos cobrir tudo o que você precisa saber: inicializar a pasta de trabalho, construir um `MarkerCollection`, alimentar um array JSON, alternar a flag “ArrayAsSingle” e, finalmente, aplicar os marcadores. Ao final, você terá um programa C# totalmente funcional que produz um arquivo Excel com os valores **A**, **B** e **C** preenchidos automaticamente. Sem serviços externos, apenas a magia pura do Aspose.Cells.

## Pré‑requisitos

- .NET 6.0 ou superior (o código também funciona com .NET Framework 4.6+)
- Pacote NuGet Aspose.Cells for .NET (`Install-Package Aspose.Cells`)
- Noções básicas de sintaxe C# (se você for iniciante, os trechos estão fortemente comentados)
- Visual Studio ou qualquer IDE de sua preferência

Se você já tem tudo isso, ótimo—vamos começar.

## Etapa 1: Como Criar uma Pasta de Trabalho (Inicializar o Arquivo Excel)

A primeira coisa que você precisa é um objeto de pasta de trabalho vazio. Pense nele como uma tela em branco que o Aspose.Cells pintará com dados posteriormente.

```csharp
using System;
using Aspose.Cells;

class SmartMarkerDemo
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();               // creates an empty .xlsx in memory
        Worksheet worksheet = workbook.Worksheets[0];    // reference to the default sheet
```

> **Por que isso importa:** `Workbook` é o ponto de entrada para toda operação no Excel. Sem ele você não pode anexar smart markers nem salvar o arquivo. Criar a pasta de trabalho primeiro também garante um ambiente limpo para as etapas subsequentes.

## Etapa 2: Como Adicionar Marcadores – Inicializar uma Coleção de Marcadores

Smart markers vivem dentro de um `MarkerCollection`. Essa coleção é onde você define os placeholders (os marcadores) e os dados que os substituirão.

```csharp
        // Step 2: Initialise a collection for smart markers
        MarkerCollection smartMarkerCollection = new MarkerCollection();
```

> **Dica profissional:** Você pode reutilizar o mesmo `MarkerCollection` para várias planilhas, mas manter um por planilha facilita a depuração.

## Etapa 3: Usar Array JSON – Adicionar um Marcador com Dados JSON

Agora realmente adicionamos um marcador. O placeholder `{SmartMarker}` será substituído pelo array JSON que fornecemos. O JSON deve ser um array convertido em string, por exemplo, `["A","B","C"]`.

```csharp
        // Step 3: Add a smart marker and provide replacement data (JSON array)
        smartMarkerCollection.Add("{SmartMarker}", "[\"A\",\"B\",\"C\"]");
```

> **Explicação:** O método `Add` recebe dois argumentos: o texto do marcador e a fonte de dados. Aqui a fonte de dados é um array JSON, que o Aspose.Cells pode analisar automaticamente. Este é o núcleo do **use json array** com smart markers.

## Etapa 4: Configurar o Marcador – Tratar o Array como um Valor Único

Por padrão, o Aspose.Cells expande um array JSON em linhas separadas. Se você quiser que todo o array seja tratado como um único valor de célula (útil para listas suspensas ou strings concatenadas), defina a flag `ArrayAsSingle`.

```csharp
        // Step 4: Configure the marker to treat the array as a single value
        smartMarkerCollection["ArrayAsSingle"] = true;
```

> **Quando usar:** Se precisar que o array apareça em uma única célula (ex.: `"A,B,C"`), habilite essa flag. Caso contrário, o Aspose.Cells gravará cada elemento em sua própria linha.

## Etapa 5: Anexar Marcadores à Planilha e Aplicá‑los

Por fim, vincule a coleção de marcadores à planilha e indique ao Aspose.Cells para substituir os placeholders pelos dados reais.

```csharp
        // Step 5: Attach the marker collection to the worksheet and apply it
        worksheet.SmartMarkers.Add(smartMarkerCollection);
        worksheet.SmartMarkers.Apply();

        // Optional: write the placeholder into a cell so you can see the replacement
        worksheet.Cells["A1"].PutValue("{SmartMarker}");

        // Save the workbook to disk
        workbook.Save("SmartMarkerResult.xlsx");
        Console.WriteLine("Workbook created successfully!");
    }
}
```

> **Resultado:** Após executar o programa, `SmartMarkerResult.xlsx` contém o valor **A** (ou o array completo se `ArrayAsSingle` for true) na célula `A1`. Abra o arquivo para verificar.

### Saída Esperada

| A |
|---|
| A |   *(se `ArrayAsSingle` for false, o primeiro elemento preenche a célula)*

Se você definir `ArrayAsSingle = true`, a célula `A1` conterá a string `["A","B","C"]`.

## Etapa 6: Como Adicionar Marcadores – Cenários Avançados (Opcional)

Você pode se perguntar, *e se eu precisar de mais de um marcador?* A resposta é simples: basta chamar `Add` novamente.

```csharp
        smartMarkerCollection.Add("{SecondMarker}", "[{\"Name\":\"John\"},{\"Name\":\"Jane\"}]");
        // You can also control each marker individually:
        smartMarkerCollection["SecondMarker"] = false; // expand into rows
```

> **Por que isso funciona:** Cada marcador opera de forma independente, permitindo combinar “array como único” e “expandir em linhas” na mesma planilha. Essa flexibilidade é uma marca dos **smart markers aspose.cells**.

## Armadilhas Comuns & Como Evitá‑las

| Problema | Por que Acontece | Solução |
|----------|------------------|---------|
| Marcador não substituído | Texto placeholder ausente ou erro de digitação | Garanta que a célula contenha a string exata do marcador (`{SmartMarker}`) |
| JSON não analisado | Sintaxe JSON inválida (faltando aspas) | Use um validador JSON ou escape as aspas duplamente nas strings C# |
| Array expande inesperadamente | `ArrayAsSingle` deixado como `false` padrão | Defina `["ArrayAsSingle"] = true` para o marcador específico |
| Pasta de trabalho salva vazia | `Apply()` não chamado antes de `Save()` | Sempre chame `worksheet.SmartMarkers.Apply()` antes de salvar |

## Exemplo Completo Funcional (Pronto para Copiar‑Colar)

Abaixo está o programa completo que você pode inserir em um aplicativo console. Nenhum arquivo adicional é necessário.

```csharp
using System;
using Aspose.Cells;

class SmartMarkerDemo
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Initialise a collection for smart markers
        MarkerCollection smartMarkerCollection = new MarkerCollection();

        // Add a smart marker and provide replacement data (JSON array)
        smartMarkerCollection.Add("{SmartMarker}", "[\"A\",\"B\",\"C\"]");

        // Configure the marker to treat the array as a single value
        smartMarkerCollection["ArrayAsSingle"] = true;

        // Attach the marker collection to the worksheet and apply it
        worksheet.SmartMarkers.Add(smartMarkerCollection);
        worksheet.SmartMarkers.Apply();

        // Place the marker in a cell so we can see the replacement
        worksheet.Cells["A1"].PutValue("{SmartMarker}");

        // Save the workbook
        workbook.Save("SmartMarkerResult.xlsx");
        Console.WriteLine("Workbook created successfully!");
    }
}
```

Execute o programa, abra `SmartMarkerResult.xlsx` e você verá o array JSON (ou seu primeiro elemento) colocado ordenadamente na célula **A1**.

## Próximos Passos: Expandindo a Solução

Agora que você sabe **como criar uma pasta de trabalho**, **como adicionar marcadores** e **usar json array** com Aspose.Cells, considere estas ideias de continuação:

1. **Múltiplas Planilhas** – Percorra uma lista de planilhas e anexe diferentes coleções de marcadores a cada uma.
2. **JSON Dinâmico** – Recupere JSON de uma API web (`HttpClient`) e alimente‑o diretamente em `smartMarkerCollection.Add`.
3. **Estilizando a Saída** – Após aplicar os marcadores, formate as células (fontes, cores) para deixar o relatório mais polido.
4. **Formatos de Exportação** – Salve a pasta de trabalho como PDF, CSV ou HTML alterando `workbook.Save("file.pdf")`.

Cada um desses tópicos envolve naturalmente **smart markers aspose.cells**, então você estará ampliando os mesmos conceitos centrais que acabou de aprender.

## Conclusão

Percorremos **como criar uma pasta de trabalho** do zero, **como adicionar marcadores** e como **usar json array** com smart markers do Aspose.Cells. O exemplo completo e executável demonstra todo o fluxo de trabalho, desde a inicialização do `Workbook` até a gravação do arquivo final. Ao alternar a flag `ArrayAsSingle` você obtém controle granular sobre como os dados JSON aparecem no Excel, tornando a solução adaptável a uma ampla gama de cenários de relatório.

Teste o código, ajuste o JSON e experimente marcadores adicionais. Quando você dominar esses blocos de construção, gerar relatórios Excel sofisticados se tornará muito fácil. Tem dúvidas ou quer compartilhar um caso de uso interessante? Deixe um comentário abaixo—bom código!

![Diagrama mostrando como criar uma pasta de trabalho com marcadores inteligentes no Aspose.Cells](https://example.com/images/create-workbook-smart-markers.png "como criar pasta de trabalho com marcadores inteligentes Aspose.Cells")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}