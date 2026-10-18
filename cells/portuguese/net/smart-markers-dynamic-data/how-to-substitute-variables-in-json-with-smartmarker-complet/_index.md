---
category: general
date: 2026-03-29
description: Como substituir variáveis em JSON usando SmartMarker – aprenda a usar
  a expressão if, aplicar lógica condicional, multiplicar valores e gerar JSON sem
  esforço.
draft: false
keywords:
- how to substitute variables
- use if expression
- how to apply conditional
- how to multiply values
- how to generate json
language: pt
og_description: Como substituir variáveis em JSON usando SmartMarker. Descubra como
  usar expressão if, aplicar lógica condicional, multiplicar valores e gerar JSON
  em minutos.
og_title: Como Substituir Variáveis em JSON com SmartMarker – Passo a Passo
tags:
- C#
- SmartMarker
- JSON templating
title: Como Substituir Variáveis em JSON com SmartMarker – Guia Completo
url: /pt/net/smart-markers-dynamic-data/how-to-substitute-variables-in-json-with-smartmarker-complet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Substituir Variáveis em JSON com SmartMarker – Guia Completo

Já se perguntou **como substituir variáveis** dentro de um payload JSON sem escrever um parser personalizado? Você não está sozinho. Em muitos cenários de integração—pense em faturas, motores de precificação ou arquivos de configuração dinâmicos—você precisa injetar valores em tempo de execução, aplicar condicionais simples e, talvez, fazer uma multiplicação rápida. Este tutorial mostra exatamente **como substituir variáveis** usando a biblioteca SmartMarker, tudo mantendo o JSON limpo e legível.

Vamos percorrer um exemplo do mundo real que cobre **uso de expressão if**, **como aplicar condicional**, **como multiplicar valores**, e **como gerar json** dinamicamente. Ao final, você terá um trecho de C# pronto‑para‑executar que pode ser inserido em qualquer projeto .NET.

## O Que Você Vai Aprender

- Configurar `SmartMarkerOptions` para armazenar variáveis reutilizáveis.  
- Escrever um template JSON que contém uma expressão `if` para lógica condicional.  
- Multiplicar um valor por uma variável dentro do template.  
- Processar o template com `SmartMarkerProcessor` e obter a string JSON final.  
- Solucionar armadilhas comuns, como variáveis ausentes ou expressões malformadas.

Sem serviços externos, sem dependências pesadas—apenas C# puro e o pacote NuGet SmartMarker.

---

## Como Substituir Variáveis – Visão Geral Passo a Passo

Abaixo está uma visão de alto nível do fluxo de trabalho. Pense nele como um pipeline onde seu template JSON bruto entra à esquerda, o motor SmartMarker faz sua mágica, e o JSON totalmente renderizado sai à direita.

![Diagrama mostrando como substituir variáveis em JSON](https://example.com/images/smartmarker-flow.png "Como substituir variáveis em JSON")

*Texto alternativo da imagem: Diagrama mostrando como substituir variáveis em JSON.*

---

## Passo 1: Instalar e Importar SmartMarker

Antes de começar, certifique‑se de que o pacote SmartMarker está referenciado no seu projeto. Se você estiver usando a .NET CLI, execute:

```bash
dotnet add package SmartMarker
```

Em seguida, adicione as diretivas `using` necessárias no topo do seu arquivo C#:

```csharp
using SmartMarker;
using SmartMarker.Models;
using System;
```

> **Dica profissional:** A versão mais recente (a partir de março 2026) é 2.4.1. Ela suporta .NET 6 e posteriores, mas funciona perfeitamente também com .NET Framework 4.7.

---

## Passo 2: Criar Opções do SmartMarker e Definir Variáveis

Agora criaremos uma instância de `SmartMarkerOptions` que armazenará todas as variáveis que queremos reutilizar no template. É aqui que respondemos à pergunta **como substituir variáveis**—as variáveis atuam como marcadores que o SmartMarker substituirá depois.

```csharp
// Step 2: Create SmartMarker options to hold variables used in the template
var smartMarkerOptions = new SmartMarkerOptions();

// Define a variable (Rate) that we’ll reference later in the JSON expression
smartMarkerOptions.Variables["Rate"] = 0.08; // 8% commission rate
```

Por que armazenar a taxa em `Variables` ao invés de codificá‑la? Porque você pode obter esse número de um banco de dados, de um arquivo de configuração ou de uma entrada do usuário. Mantê‑la nas opções torna o template reutilizável e testável.

---

## Passo 3: Escrever o Template JSON com uma Expressão `if`

É aqui que a palavra‑chave **uso de expressão if** brilha. O SmartMarker permite que você incorpore lógica condicional diretamente dentro da string JSON. A sintaxe se parece um pouco com um nome de propriedade, mas o SmartMarker a trata como uma diretiva.

```csharp
// Step 3: Prepare the JSON data with a conditional field that uses the variable
string jsonTemplate = @"{
    ""Amount"": 1000,
    ""if(Amount>500)"": ""${Amount * Rate}""
}";
```

Observe a chave `if(Amount>500)`. O SmartMarker avalia a expressão `Amount>500`; se for verdadeira, o valor correspondente (`${Amount * Rate}`) é inserido na saída. A sintaxe `${...}` é o motor de *substituição de variáveis*—aqui **como multiplicar valores** (`Amount * Rate`) antes de injetar o resultado.

---

## Passo 4: Processar o Template e Recuperar o JSON Final

Com as opções e o template prontos, entregamos tudo ao processador. O método `ProcessJson` analisa o template, aplica a condição, realiza a multiplicação e devolve uma string JSON limpa.

```csharp
// Step 4: Process the JSON with SmartMarker, applying the variable substitution
string resultJson = ws.SmartMarkerProcessor.ProcessJson(jsonTemplate, smartMarkerOptions);
Console.WriteLine(resultJson);
```

Executar o trecho imprime:

```json
{
  "Amount": 1000,
  "Result": "80"
}
```

**O que aconteceu?**  
- `Amount` é 1000, o que satisfaz `Amount>500`.  
- SmartMarker avalia `${Amount * Rate}` → `1000 * 0.08 = 80`.  
- A chave condicional original (`if(Amount>500)`) é substituída por um nome de propriedade limpo (`Result`). Por padrão o SmartMarker usa `"Result"`, mas você pode customizar (mais detalhes adiante).

Se você mudar `Amount` para `400`, a saída se torna:

```json
{
  "Amount": 400
}
```

O bloco condicional desaparece porque a expressão avaliou para `false`. Essa é a essência de **como aplicar condicional** em JSON.

---

## Passo 5: Customizar o Nome da Propriedade de Saída (Opcional)

Às vezes você não quer a chave genérica `"Result"`. O SmartMarker permite especificar um nome customizado usando a opção `RenameIfExpression`:

```csharp
smartMarkerOptions.RenameIfExpression = "Discount";
string customResult = ws.SmartMarkerProcessor.ProcessJson(jsonTemplate, smartMarkerOptions);
Console.WriteLine(customResult);
```

Saída:

```json
{
  "Amount": 1000,
  "Discount": "80"
}
```

Agora o valor condicional é armazenado sob um nome de propriedade mais significativo—perfeito para serviços downstream que esperam um campo específico.

---

## Armadilhas Comuns e Como Evitá‑las

| Problema | Por Que Acontece | Solução |
|----------|------------------|---------|
| Variável não encontrada | Você referenciou uma variável que não está em `smartMarkerOptions.Variables`. | Verifique a ortografia e assegure‑se de que a variável foi adicionada antes do processamento. |
| Sintaxe `if` inválida | Falta de parênteses ou operador errado (`>`, `<`, `==`). | Siga exatamente o padrão `if(<expressão>)`; o SmartMarker suporta apenas comparações numéricas simples. |
| JSON fica malformado | Deixar uma vírgula extra após o bloco condicional. | Deixe o SmartMarker remover; mantenha o template original sintaticamente correto. |
| Formato de número inesperado | O resultado aparece como string `"80"` ao invés de número. | Converta ou faça parse depois, ou use `${(Amount * Rate):N0}` para formatação numérica. |

---

## Exemplo Completo (Pronto para Copiar e Colar)

Abaixo está o programa completo que você pode compilar e executar. Ele demonstra **como gerar json** com variáveis dinâmicas, condicionais e aritmética—tudo em menos de 30 linhas.

```csharp
using System;
using SmartMarker;
using SmartMarker.Models;

class Program
{
    static void Main()
    {
        // 1️⃣ Create SmartMarker options and define a reusable variable
        var smartMarkerOptions = new SmartMarkerOptions();
        smartMarkerOptions.Variables["Rate"] = 0.08; // 8% commission
        smartMarkerOptions.RenameIfExpression = "Discount"; // optional custom name

        // 2️⃣ JSON template with an if expression and multiplication
        string jsonTemplate = @"{
            ""Amount"": 1000,
            ""if(Amount>500)"": ""${Amount * Rate}""
        }";

        // 3️⃣ Process the template
        string output = ws.SmartMarkerProcessor.ProcessJson(jsonTemplate, smartMarkerOptions);

        // 4️⃣ Show the result
        Console.WriteLine("Generated JSON:");
        Console.WriteLine(output);
    }
}
```

**Saída esperada no console**

```
Generated JSON:
{
  "Amount": 1000,
  "Discount": "80"
}
```

Sinta‑se à vontade para mudar `Amount` e testar o ramo condicional, ou ajustar `Rate` para ver diferentes cálculos de desconto.

---

## Expandindo o Padrão – Mais Cenários “Como Fazer”

- **Como substituir variáveis** a partir de um arquivo de configuração: carregue um `Dictionary<string, object>` de `appsettings.json` e alimente `smartMarkerOptions.Variables`.  
- **Como usar expressão if** para múltiplas condições: encadeie como `"if(Amount>500 && CustomerType=='VIP')"`—o SmartMarker suporta AND/OR lógicos.  
- **Como aplicar formatação condicional**: use `${Amount:0.00}` dentro da expressão para controlar casas decimais.  
- **Como multiplicar valores** com matemática mais complexa: `${(Amount - Discount) * TaxRate}` funciona da mesma forma.  
- **Como gerar json** para objetos aninhados: coloque o bloco condicional dentro de outro objeto JSON, e o SmartMarker preservará a hierarquia.

---

## Conclusão

Cobremos **como substituir variáveis** em JSON usando SmartMarker, demonstramos **uso de expressão if** para inclusão condicional, explicamos **como aplicar condicional**, mostramos **como multiplicar valores** dentro de um template e, finalmente, ilustramos **como gerar json** pronto para consumo downstream. A abordagem é leve, não requer motor de template externo e se encaixa perfeitamente em qualquer base de código C#.

Experimente—ajuste as variáveis, adicione mais condições ou encapsule tudo em uma classe helper para reutilização em toda a solução. Quando precisar produzir JSON dinâmico rapidamente, o SmartMarker é uma opção sólida e pronta para produção.

---

**Próximos passos**

- Aprofunde‑se nos recursos avançados do SmartMarker, como loops (`foreach`) e funções customizadas.  
- Combine esta técnica com endpoints ASP.NET Core para servir APIs JSON dinâmicas.  
- Explore outras bibliotecas de templating (ex.: Handlebars.NET) para comparação, especialmente se precisar de sintaxe mais rica.

Tem perguntas ou um caso de uso específico que está te dando dor de cabeça? Deixe um comentário abaixo e vamos solucionar juntos. Feliz codificação!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}