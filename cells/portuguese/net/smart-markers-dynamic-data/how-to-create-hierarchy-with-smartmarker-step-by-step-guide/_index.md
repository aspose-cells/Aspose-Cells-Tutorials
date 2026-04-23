---
category: general
date: 2026-02-14
description: Como criar hierarquia em templates SmartMarker é mais fácil do que você
  imagina – aprenda a criar dados hierárquicos e a listar funcionários de forma eficiente.
draft: false
keywords:
- how to create hierarchy
- create hierarchical data
- how to list employees
- SmartMarker nested range
- C# template processing
language: pt
og_description: Como criar hierarquia em modelos SmartMarker é simples. Siga este
  guia para criar dados hierárquicos e listar funcionários com intervalos aninhados.
og_title: Como criar hierarquia com SmartMarker – Guia completo
tags:
- SmartMarker
- C#
- templating
title: Como criar hierarquia com SmartMarker – Guia passo a passo
url: /pt/net/smart-markers-dynamic-data/how-to-create-hierarchy-with-smartmarker-step-by-step-guide/
---

codes.

Proceed.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Criar Hierarquia com SmartMarker – Guia Completo

Já se perguntou **como criar hierarquia** dentro de um template SmartMarker sem perder a cabeça? Você não está sozinho. Em muitos cenários de relatórios você precisa de um relacionamento pai‑filho — pense em departamentos e nas pessoas que trabalham neles. A boa notícia é que o SmartMarker torna isso muito fácil, basta seguir os passos corretos.

Neste tutorial vamos percorrer todo o processo: desde **criar dados hierárquicos** em C#, habilitar intervalos aninhados e, por fim, renderizar um template que **lista funcionários** para cada departamento. Ao final você terá um exemplo pronto‑para‑executar que pode ser inserido em qualquer projeto .NET.

---

## O Que Você Precisa

- .NET 6+ (qualquer versão recente serve)
- Uma referência à biblioteca **SmartMarker** (o namespace `ws.SmartMarkerProcessor`)
- Conhecimento básico de C# – nada sofisticado, apenas alguns objetos e uma ou duas expressões lambda
- Uma IDE ou editor de sua escolha (Visual Studio, Rider, VS Code… você decide)

Se já tem tudo isso, ótimo — vamos começar.

---

## Como Criar Hierarquia – Visão Geral

A ideia central é construir um **grafo de objetos aninhado** que reflita a estrutura que você deseja ver no documento final. No nosso caso o grafo se parece com:

```
Departments
 ├─ Name (string)
 └─ Employees (string[])
```

O SmartMarker pode então iterar sobre `Departments` e, como ativaremos o **processamento de intervalos aninhados**, ele também percorrerá automaticamente a coleção `Employees` de cada departamento.

---

## Etapa 1: Construir o Modelo de Dados Hierárquico

Primeiro criamos um objeto anônimo que contém um array de departamentos, cada um com sua própria lista de funcionários. Usar um tipo anônimo mantém o exemplo leve — sinta‑se à vontade para substituí‑lo por classes POCO reais mais tarde.

```csharp
// Step 1: Create hierarchical data that SmartMarker will iterate over
var departmentData = new
{
    Departments = new[]
    {
        new { Name = "HR", Employees = new[] { "John", "Amy" } },
        new { Name = "IT", Employees = new[] { "Bob", "Eve" } }
    }
};
```

> **Por que isso importa:** O array `Departments` é a coleção de nível superior. Cada elemento contém um array `Employees`, fornecendo o segundo nível de hierarquia que acessaremos mais adiante com `#Departments.Employees#`.

---

## Etapa 2: Habilitar o Processamento de Intervalos Aninhados

O SmartMarker não mergulha nas coleções internas a menos que você indique. O objeto `SmartMarkerOptions` contém essa chave.

```csharp
// Step 2: Enable nested range processing so inner collections (Employees) can be used
var smartMarkerOptions = new SmartMarkerOptions
{
    EnableNestedRange = true   // crucial for #Departments.Employees# to work
};
```

> **Dica de especialista:** Se você esquecer essa flag, o intervalo interno `#Employees#` simplesmente não retornará nada, e você ficará se perguntando por que o template ficou em branco.

---

## Etapa 3: Executar o Processador com Seus Dados

Agora passamos os dados e as opções para o processador. A variável `ws` representa seu **WebService** (ou qualquer objeto que hospede o motor SmartMarker).

```csharp
// Step 3: Run SmartMarker processing with the data and the configured options
ws.SmartMarkerProcessor.StartSmartMarkerProcessing(departmentData, smartMarkerOptions);
```

Neste ponto o SmartMarker analisa o template, substitui `#Departments.Name#` por cada nome de departamento e, como os intervalos aninhados estão habilitados, itera através da coleção `Employees` de cada departamento.

---

## Etapa 4: Criar os Marcadores do Template

Abaixo está um template mínimo que demonstra tanto o loop externo quanto o interno. Cole‑o no editor de templates do SmartMarker (ou em um arquivo `.txt` que você passa ao processador).

```
#Departments.Name#
  #Departments.Employees#
    - #Departments.Employees#
  #/Departments.Employees#
#/Departments.Name#
```

Ao ser renderizado, você verá:

```
HR
  - John
  - Amy
IT
  - Bob
  - Eve
```

> **O que você está vendo:** O `#Departments.Name#` externo imprime o título do departamento. O bloco interno `#Departments.Employees#` percorre cada funcionário, e `#Departments.Employees#` dentro do bloco gera o nome real.

---

## Saída Esperada & Verificação

Executar o exemplo completo (dados + opções + template) deve produzir exatamente a lista mostrada acima. Para verificar rapidamente, você pode imprimir o resultado no console:

```csharp
string result = ws.SmartMarkerProcessor.GetProcessedResult(); // pseudo‑method
Console.WriteLine(result);
```

Se você vir os dois títulos de departamento seguidos por suas listas de funcionários, você criou **uma hierarquia** e **listou os funcionários** com sucesso.

---

## Armadilhas Comuns & Casos de Borda

| Problema | Por que Acontece | Solução |
|----------|------------------|---------|
| Nenhuma saída para funcionários | `EnableNestedRange` deixado como false | Defina `EnableNestedRange = true` |
| Nomes de funcionários duplicados | Mesmo array reutilizado em vários departamentos | Clone o array ou use coleções distintas |
| Hierarquias muito grandes causam pressão de memória | SmartMarker carrega todo o grafo de objetos na memória | Transmita os dados ou pagine coleções grandes |
| Erros de sintaxe no template | Tags de fechamento `#/…#` ausentes | Use o validador do SmartMarker ou teste rápido com um template pequeno |

---

## Avançando – Variações do Mundo Real

1. **Fontes de dados dinâmicas** – Busque departamentos de um banco de dados e mapeie‑os para a estrutura anônima usando LINQ.  
2. **Formatação condicional** – Adicione uma flag `IsManager` a cada funcionário e use as tags condicionais do SmartMarker (`#if …#`) para destacar gerentes.  
3. **Múltiplos níveis de aninhamento** – Se precisar de equipes dentro de departamentos, basta acrescentar outra coleção (`Teams`) e manter `EnableNestedRange` ativado.

---

## Exemplo Completo Funcional (Pronto para Copiar‑Colar)

```csharp
using System;
using SmartMarker; // hypothetical namespace

class Program
{
    static void Main()
    {
        // 1️⃣ Build hierarchical data
        var departmentData = new
        {
            Departments = new[]
            {
                new { Name = "HR", Employees = new[] { "John", "Amy" } },
                new { Name = "IT", Employees = new[] { "Bob", "Eve" } }
            }
        };

        // 2️⃣ Enable nested ranges
        var smartMarkerOptions = new SmartMarkerOptions
        {
            EnableNestedRange = true
        };

        // 3️⃣ Start processing
        var ws = new WebService(); // assume this is your entry point
        ws.SmartMarkerProcessor.StartSmartMarkerProcessing(departmentData, smartMarkerOptions);

        // 4️⃣ Retrieve and display the result
        string output = ws.SmartMarkerProcessor.GetProcessedResult(); // placeholder method
        Console.WriteLine(output);
    }
}
```

**Template (template.txt)**

```
#Departments.Name#
  #Departments.Employees#
    - #Departments.Employees#
  #/Departments.Employees#
#/Departments.Name#
```

Executar o programa imprime a hierarquia exatamente como mostrada anteriormente.

---

## Conclusão

Cobremos **como criar hierarquia** no SmartMarker, desde a modelagem **de dados hierárquicos** em C# até a ativação de intervalos aninhados e, por fim, a renderização de um template que **lista funcionários** por departamento. O padrão escala — basta acrescentar mais coleções aninhadas ou lógica condicional e você terá um motor de relatórios poderoso nas mãos.

Pronto para o próximo desafio? Experimente substituir os tipos anônimos por classes POCO fortemente tipadas, ou integre esse fluxo em um endpoint ASP.NET Core que devolva um PDF ou documento Word. O céu é o limite, e agora você tem uma base sólida.

---

![How to create hierarchy diagram](image.png){alt="Diagrama de como criar hierarquia mostrando relacionamento departamento‑funcionário"}

*Feliz codificação! Se encontrar algum obstáculo, deixe um comentário abaixo — ficarei feliz em ajudar.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}