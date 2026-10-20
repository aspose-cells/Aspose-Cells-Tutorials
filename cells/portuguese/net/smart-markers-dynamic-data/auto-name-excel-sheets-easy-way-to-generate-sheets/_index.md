---
category: general
date: 2026-02-23
description: Nomeie automaticamente planilhas do Excel e aprenda a gerar planilhas
  automaticamente usando SmartMarkers. Guia passo a passo em C# para pastas de trabalho
  dinâmicas.
draft: false
keywords:
- auto name excel sheets
- how to generate sheets
- Aspose.Cells SmartMarkers
- dynamic worksheet naming
- C# Excel automation
language: pt
og_description: Nomeie planilhas do Excel automaticamente e instantaneamente. Aprenda
  a gerar planilhas com SmartMarkers em C# – exemplo completo e executável.
og_title: Nomear automaticamente planilhas do Excel – tutorial rápido de C#
tags:
- C#
- Excel
- Aspose.Cells
title: Nomear Automaticamente Planilhas do Excel – Forma Fácil de Gerar Planilhas
url: /pt/net/smart-markers-dynamic-data/auto-name-excel-sheets-easy-way-to-generate-sheets/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Nomear Automaticamente Planilhas do Excel – Tutorial Completo em C#

Já se perguntou como **auto name excel sheets** sem escrever um loop que renomeia manualmente cada aba? Você não está sozinho. Em muitos projetos de relatórios a quantidade de planilhas cresce em tempo de execução, e manter os nomes organizados se torna um ponto crítico. A boa notícia? Com os **SmartMarkers** do Aspose.Cells você pode deixar a biblioteca cuidar da nomeação para você, e ainda permite **how to generate sheets** em tempo real.

Neste guia, percorreremos um cenário real: criar uma pasta de trabalho, configurar as opções do SmartMarker para que as planilhas de detalhe sejam nomeadas automaticamente como *Detail*, *Detail1*, *Detail2*, …, e então verificar se as planilhas aparecem como esperado. Ao final, você terá uma solução autônoma, pronta para copiar e colar, que pode adaptar a qualquer projeto que precise de criação dinâmica de planilhas.

---

## O que você precisará

- **.NET 6+** (ou .NET Framework 4.6.2+). O código funciona em qualquer runtime recente.
- **Aspose.Cells for .NET** pacote NuGet – `Install-Package Aspose.Cells`.
- Um projeto básico em C# (Console App, WinForms ou ASP.NET – o mesmo código funciona em qualquer lugar).
- Visual Studio, VS Code ou sua IDE favorita.

Sem interop extra do Excel, sem COM, apenas código gerenciado puro.

---

## Etapa 1: Nomear Automaticamente Planilhas do Excel com SmartMarkers

A primeira coisa que você precisa fazer é informar ao Aspose.Cells qual nome base você deseja para as planilhas de detalhe criadas automaticamente. Isso é feito através da classe `SmartMarkerOptions`.

```csharp
using Aspose.Cells;
using Aspose.Cells.Tables;   // for SmartMarkers
using System;

class Program
{
    static void Main()
    {
        // Create a new workbook that will hold the master sheet.
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];
        ws.Name = "Master";

        // -----------------------------------------------------------
        // Step 1: Configure SmartMarker options – set the base name
        // -----------------------------------------------------------
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
        {
            // This tells SmartMarkers to create sheets named Detail, Detail1, Detail2, …
            DetailSheetNewName = "Detail"
        };
```

**Por que isso importa:** Ao definir `DetailSheetNewName`, você delega a lógica de nomeação à biblioteca. Não é necessário escrever um loop `for` que verifica os nomes das planilhas existentes e incrementa um contador – a API faz isso por você, garantindo nomes únicos mesmo quando a fonte de dados contém dezenas de linhas.

---

## Etapa 2: Preparar a Fonte de Dados

SmartMarkers funcionam com qualquer coleção `IEnumerable`, um `DataTable` ou até mesmo uma lista simples de objetos. Para esta demonstração, usaremos uma lista simples de objetos que representam detalhes de pedidos.

```csharp
        // -----------------------------------------------------------
        // Step 2: Build a sample data source
        // -----------------------------------------------------------
        var orders = new[]
        {
            new { OrderId = 1001, Product = "Laptop", Qty = 2, Price = 1200.00 },
            new { OrderId = 1002, Product = "Mouse",   Qty = 5, Price =  25.99 },
            new { OrderId = 1003, Product = "Keyboard",Qty = 3, Price =  45.50 }
        };
```

**Por que isso importa:** A fonte de dados determina quantas planilhas de detalhe serão geradas. Cada elemento da coleção cria uma nova planilha baseada no modelo SmartMarker que adicionaremos a seguir.

---

## Etapa 3: Inserir um Modelo SmartMarker na Planilha Mestre

Um modelo SmartMarker é apenas uma célula (ou intervalo) que contém marcadores de posição. Quando o método `Apply` é executado, os marcadores são substituídos por dados reais, e para cada linha uma nova planilha é criada.

```csharp
        // -----------------------------------------------------------
        // Step 3: Add a SmartMarker template to the master sheet
        // -----------------------------------------------------------
        // Put a header row
        ws.Cells["A1"].PutValue("Order ID");
        ws.Cells["B1"].PutValue("Product");
        ws.Cells["C1"].PutValue("Quantity");
        ws.Cells["D1"].PutValue("Unit Price");

        // Insert SmartMarker placeholders starting at row 2
        ws.Cells["A2"].PutValue("&=orders.OrderId");
        ws.Cells["B2"].PutValue("&=orders.Product");
        ws.Cells["C2"].PutValue("&=orders.Qty");
        ws.Cells["D2"].PutValue("&=orders.Price");
```

**Por que isso importa:** A sintaxe `&=` indica aos SmartMarkers “pegar o valor da fonte de dados”. Quando `Apply` é executado, o Aspose.Cells copiará essa linha para uma nova planilha para cada item em `orders`, nomeando automaticamente a planilha com base na opção que definimos anteriormente.

---

## Etapa 4: Aplicar Opções do SmartMarker – É Aqui que as Planilhas São Nomeadas Automaticamente

Agora chega o momento em que a biblioteca faz o trabalho pesado. A chamada `Apply` lê o modelo, cria as planilhas de detalhe e as nomeia de acordo com `DetailSheetNewName`.

```csharp
        // -----------------------------------------------------------
        // Step 4: Apply SmartMarker – auto name excel sheets happens here
        // -----------------------------------------------------------
        ws.SmartMarkers.Apply(smartMarkerOptions, new { orders });

        // Save the workbook to verify the result
        wb.Save("AutoNamedSheets.xlsx");
        Console.WriteLine("Workbook saved. Open AutoNamedSheets.xlsx to see the result.");
    }
}
```

**Por que isso importa:** O método `Apply` não apenas preenche os dados, mas também respeita o padrão de nomeação que fornecemos. Se você abrir *AutoNamedSheets.xlsx* verá:

- **Detail** – contém o primeiro pedido.
- **Detail1** – segundo pedido.
- **Detail2** – terceiro pedido.

Nenhuma renomeação manual necessária.

---

## Etapa 5: Verificar o Resultado – Como Gerar Planilhas Corretamente

Depois de executar o programa, abra o arquivo gerado. Você deverá ver três novas planilhas nomeadas exatamente como descrito acima. Isso prova que você aprendeu com sucesso **how to generate sheets** automaticamente.

> **Dica profissional:** Se precisar de um sufixo personalizado (por exemplo, “_Report”), basta definir `DetailSheetNewName = "Detail_Report"` e a biblioteca acrescentará números após a string base.

---

## Casos de Borda & Perguntas Frequentes

### E se o nome base já existir?

Aspose.Cells verifica os nomes de planilhas existentes e acrescenta um número incremental até encontrar um nome único. Portanto, mesmo que já exista uma planilha chamada *Detail* na pasta de trabalho, a próxima planilha gerada será *Detail1*.

### Posso controlar a ordem das planilhas geradas?

Sim. A ordem segue a sequência da fonte de dados. Se precisar de uma ordem específica, ordene a coleção antes de passá‑la para `Apply`.

### É possível gerar planilhas em uma pasta de trabalho diferente?

Absolutamente. Crie uma segunda instância `Workbook`, adicione uma planilha de espaço reservado e chame `Apply` nessa planilha. A mesma lógica de nomeação se aplica.

### Como isso funciona com grandes conjuntos de dados?

SmartMarkers são otimizados para desempenho. Mesmo com milhares de linhas, a biblioteca transmite os dados de forma eficiente. Apenas certifique‑se de que há memória suficiente para o tamanho final da pasta de trabalho.

---

## Exemplo Completo Funcional (Pronto para Copiar‑Colar)

Abaixo está o programa completo que você pode inserir em um novo projeto de console. Nenhuma parte está faltando – tudo, desde as diretivas `using` até a chamada final `Save`, está incluído.

```csharp
using Aspose.Cells;
using Aspose.Cells.Tables;
using System;

class AutoNameExcelSheetsDemo
{
    static void Main()
    {
        // 1️⃣ Create workbook and master worksheet
        Workbook workbook = new Workbook();
        Worksheet master = workbook.Worksheets[0];
        master.Name = "Master";

        // 2️⃣ Set up SmartMarker options – this is the key to auto‑naming
        SmartMarkerOptions options = new SmartMarkerOptions
        {
            DetailSheetNewName = "Detail"   // base name for generated sheets
        };

        // 3️⃣ Sample data source – each element will become a new sheet
        var orders = new[]
        {
            new { OrderId = 1001, Product = "Laptop",   Qty = 2, Price = 1200.00 },
            new { OrderId = 1002, Product = "Mouse",    Qty = 5, Price =  25.99 },
            new { OrderId = 1003, Product = "Keyboard", Qty = 3, Price =  45.50 }
        };

        // 4️⃣ Build a simple template on the master sheet
        master.Cells["A1"].PutValue("Order ID");
        master.Cells["B1"].PutValue("Product");
        master.Cells["C1"].PutValue("Quantity");
        master.Cells["D1"].PutValue("Unit Price");

        master.Cells["A2"].PutValue("&=orders.OrderId");
        master.Cells["B2"].PutValue("&=orders.Product");
        master.Cells["C2"].PutValue("&=orders.Qty");
        master.Cells["D2"].PutValue("&=orders.Price");

        // 5️⃣ Apply SmartMarkers – this auto‑creates and auto‑names the sheets
        master.SmartMarkers.Apply(options, new { orders });

        // 6️⃣ Save and inform the user
        workbook.Save("AutoNamedSheets.xlsx");
        Console.WriteLine("Done! Open AutoNamedSheets.xlsx – you’ll see Detail, Detail1, Detail2 …");
    }
}
```

Execute o programa, abra o *AutoNamedSheets.xlsx* resultante e você verá o recurso de **auto name excel sheets** em ação.

---

## Perguntas Frequentes de Follow‑Up

- **Posso usar isso com um arquivo de modelo existente?**  
  Sim. Carregue a pasta de trabalho com `new Workbook("Template.xlsx")` e aponte `master` para a planilha que contém seus marcadores SmartMarker.

- **E se eu precisar de convenções de nomeação diferentes por tipo de planilha?**  
  Crie múltiplos objetos `SmartMarkerOptions`, cada um com seu próprio `DetailSheetNewName`, e aplique-os a diferentes planilhas mestres.

- **Existe uma forma de suprimir a planilha base (a que contém o modelo)?**  
  Após `Apply`, você pode simplesmente excluir a planilha mestre: `workbook.Worksheets.RemoveAt(0);` – as planilhas de detalhe permanecem intactas.

---

## Conclusão

Agora você sabe **how to auto name excel sheets** usando Aspose.Cells SmartMarkers, e também viu um padrão sólido para **how to generate sheets** dinamicamente em C#. A ideia central é simples: configure `SmartMarkerOptions.DetailSheetNewName`, forneça uma coleção e deixe a biblioteca fazer o resto. Essa abordagem elimina loops repetitivos, garante nomes únicos e escala de forma elegante.

Pronto para o próximo passo? Experimente trocar a fonte de dados por um `Data

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}