---
category: general
date: 2026-03-18
description: Crie uma nova pasta de trabalho e exporte o Excel para TXT preservando
  a precisão numérica. Aprenda como salvar a planilha como TXT e converter a planilha
  para TXT de forma eficiente.
draft: false
keywords:
- create new workbook
- export excel to txt
- save excel as txt
- save worksheet as txt
- convert worksheet to txt
language: pt
og_description: Crie uma nova pasta de trabalho e exporte o Excel para TXT com precisão.
  Este tutorial mostra como salvar a planilha como TXT e converter a planilha para
  TXT usando C#.
og_title: Criar nova pasta de trabalho – Guia de Exportação do Excel para TXT
tags:
- Aspose.Cells
- C#
- Excel automation
title: Criar nova pasta de trabalho – Exportar Excel para TXT com precisão total
url: /pt/net/converting-excel-files-to-other-formats/create-new-workbook-export-excel-to-txt-with-full-precision/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar nova pasta de trabalho – Exportar Excel para TXT com Precisão Total

Já precisou **criar nova pasta de trabalho** em C# apenas para despejar alguns dados em um arquivo de texto simples? Talvez você esteja extraindo um relatório de um sistema legado e a ferramenta downstream aceite apenas um feed `.txt`. A boa notícia? Você não precisa sacrificar a precisão numérica e, certamente, não precisa criar manualmente strings CSV.

Neste guia, percorreremos todo o processo de **exportar excel para txt**, cobrindo tudo, desde a inicialização da pasta de trabalho até a preservação de zeros à direita quando você **salvar planilha como txt**. Ao final, você terá um trecho pronto‑para‑executar que pode ser inserido em qualquer projeto .NET — sem utilitários extras necessários.

## O que você precisará

- **ASP.NET/ .NET 6+** (o código funciona também no .NET Framework 4.6+)  
- **Aspose.Cells for .NET** – a biblioteca que fornece as classes `Workbook`, `Worksheet` e `TxtSaveOptions`. Você pode obtê‑la no NuGet com `Install-Package Aspose.Cells`.  
- Um entendimento básico de C# (se você está confortável com declarações `using`, está pronto para prosseguir).  

É isso — sem interop do Excel, sem objetos COM e definitivamente sem concatenação manual de strings.

---

## Etapa 1: Inicializar uma Nova Pasta de Trabalho (Palavra‑chave Primária)

A primeira coisa que você precisa fazer é **criar nova pasta de trabalho**. Pense na pasta de trabalho como uma tela em branco onde você colará números, texto ou fórmulas posteriormente.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToTxtDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();                 // <‑‑ creates new workbook
            Worksheet worksheet = workbook.Worksheets[0];       // first sheet (index 0)
```

> **Por que isso importa:** Instanciar `Workbook` sem carregar um arquivo fornece uma página limpa. Você pode então adicionar dados programaticamente, o que é perfeito para cenários de **converter planilha para txt** onde não há um `.xlsx` existente.

---

## Etapa 2: Preencher Células – Mantenha os Zeros à Direita

Um erro comum ao despejar números em texto é perder os zeros à direita (`123.45000` torna‑se `123.45`). Se os sistemas downstream dependem de campos de largura fixa, essa perda pode quebrar tudo.

```csharp
            // Step 2: Write a numeric value that contains trailing zeros
            // PutValue respects the data type; we’ll later tell the saver to keep precision.
            worksheet.Cells[0, 0].PutValue(123.45000);
```

> **Dica profissional:** `PutValue` infere automaticamente o tipo de dado. Se precisar de uma string que pareça um número, use `PutValue("123.45000")` em vez disso.

---

## Etapa 3: Configurar Opções de Salvamento TXT – Preservar a Precisão Numérica

É aqui que a mágica acontece. Ao ativar `PreserveNumericPrecision`, você instrui o Aspose.Cells a gravar o valor exato que inseriu, incluindo quaisquer zeros à direita insignificantes.

```csharp
            // Step 3: Configure TXT save options to keep the original numeric precision
            TxtSaveOptions txtSaveOptions = new TxtSaveOptions(SaveFormat.Txt)
            {
                PreserveNumericPrecision = true   // retain all digits, even trailing zeros
            };
```

> **Por que habilitar isso?** Quando você **salva excel como txt**, o comportamento padrão remove decimais desnecessários. Definir `PreserveNumericPrecision = true` garante que a saída reflita o valor exibido na célula, o que é crítico para relatórios financeiros ou dados científicos.

---

## Etapa 4: Salvar a Planilha como TXT – A Exportação Final

Agora realmente **salvamos a planilha como txt**. Você pode apontar o caminho para qualquer local onde tenha permissão de gravação; o exemplo usa uma pasta relativa chamada `output`.

```csharp
            // Step 4: Save the worksheet as a TXT file using the configured options
            string outputPath = "output/num-preserve.txt";
            worksheet.Save(outputPath, txtSaveOptions);

            Console.WriteLine($"File saved to {outputPath}");
        }
    }
}
```

> **Saída esperada** (`num-preserve.txt`):

```
123.45000
```

Observe que os zeros à direita permanecem intactos — exatamente o que você pediu.

---

## Etapa 5: Verificar o Resultado – Verificação Rápida

Depois que o programa for executado, abra `num-preserve.txt` em qualquer editor de texto. Você deve ver a linha única `123.45000`. Se encontrar `123.45` em vez disso, verifique novamente se `PreserveNumericPrecision` está definido como `true` e se está usando uma versão recente do Aspose.Cells (v23.10+).

---

## Variações Comuns & Casos Limite

### Exportando Múltiplas Células ou Intervalos

Se precisar **exportar excel para txt** de um intervalo inteiro, basta preencher mais células antes de salvar:

```csharp
worksheet.Cells["A1"].PutValue(100);
worksheet.Cells["A2"].PutValue(200.500);
worksheet.Cells["A3"].PutValue(300.00);
```

Por padrão, o Aspose gravará cada célula em uma nova linha. Você também pode alterar o delimitador (tab, vírgula) via `txtSaveOptions.Separator`.

### Convertendo Planilha para TXT com Codificações Diferentes

Às vezes, os sistemas downstream exigem UTF‑8 BOM ou ASCII. Ajuste a codificação assim:

```csharp
txtSaveOptions.Encoding = System.Text.Encoding.UTF8;
```

### Manipulando Pastas de Trabalho Grandes

Ao lidar com planilhas massivas (centenas de milhares de linhas), considere transmitir a saída:

```csharp
txtSaveOptions.EnableCache = true; // writes data in chunks to reduce memory footprint
```

---

## Dicas Profissionais & Armadilhas

- **Não se esqueça de criar o diretório de saída** antes de chamar `Save`, caso contrário você receberá uma `DirectoryNotFoundException`.  
- **Fique atento aos separadores decimais específicos de localidade**. Se o seu ambiente usa vírgulas (`1,23`), defina `txtSaveOptions.DecimalSeparator = '.'` para impor um ponto.  
- **Compatibilidade de versão**: O sinalizador `PreserveNumericPrecision` foi introduzido no Aspose.Cells 20.6. Se você estiver em uma versão mais antiga, o sinalizador não existirá e será necessário formatar a célula como texto antes de salvar.

![Exemplo de criação de nova pasta de trabalho](excel-to-txt.png "Criar nova pasta de trabalho")

*Texto alternativo da imagem: "Criar nova pasta de trabalho e exportar Excel para TXT com precisão numérica preservada"*

---

## Recapitulação – O que Cobrimos

- **Criar nova pasta de trabalho** usando Aspose.Cells.  
- Preencher uma célula com um número que inclui zeros à direita.  
- Definir `TxtSaveOptions.PreserveNumericPrecision = true` para **salvar excel como txt** sem perder a precisão.  
- Gravar o arquivo no disco, verificando que a saída corresponde ao valor original.  

Esse é o fluxo completo de **converter planilha para txt** em menos de 50 linhas de C#.

---

## Próximos Passos & Tópicos Relacionados

Agora que você pode **exportar excel para txt** com precisão perfeita, talvez queira explorar:

- **Exportar para CSV** com delimitadores personalizados (`TxtSaveOptions.Separator`).  
- **Salvar como outros formatos de texto simples** como TSV (`SaveFormat.TabDelimited`).  
- **Processamento em lote** de múltiplas pastas de trabalho em uma pasta usando `Directory.GetFiles`.  
- **Integração com Azure Functions** para conversão sob demanda na nuvem.  

Cada um desses se baseia no mesmo padrão `Workbook` → `Worksheet` → `TxtSaveOptions`, então você se sentirá em casa.

---

### Reflexão Final

Se você acompanhou, agora sabe exatamente como **criar nova pasta de trabalho**, preenchê‑la e **salvar a planilha como txt** mantendo cada dígito decimal que importa. É um pequeno trecho de código, mas resolve um problema surpreendentemente comum quando pipelines legados exigem entradas em texto simples.

Experimente, ajuste as opções e deixe os dados fluírem exatamente como você precisa. Feliz codificação!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}