---
category: general
date: 2026-09-27
description: Criar um intervalo nomeado no Excel usando Aspose.Cells, definir o nome
  da tabela, adicionar intervalo nomeado, criar tabela Excel e detectar erros de nome
  duplicado.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create named range
- set table name
- create excel table
- add named range
- detect duplicate name
language: pt
lastmod: 2026-09-27
og_description: Crie um intervalo nomeado no Excel com Aspose.Cells, depois defina
  o nome da tabela, adicione o intervalo nomeado, crie a tabela do Excel e detecte
  erros de nomes duplicados.
og_image_alt: Screenshot showing how to create a named range in Excel with Aspose.Cells
og_title: Criar um intervalo nomeado e detectar nome duplicado no Excel
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Create a named range in Excel using Aspose.Cells, set table name, add
    named range, create Excel table, and detect duplicate name errors.
  headline: Create a named range and detect duplicate name in Excel
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
title: Criar um intervalo nomeado e detectar nome duplicado no Excel
url: /pt/java/range-management/create-a-named-range-and-detect-duplicate-name-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar um intervalo nomeado e detectar nome duplicado no Excel

Se você precisar **criar um intervalo nomeado** em uma pasta de trabalho do Excel e quiser evitar colisões de nomes, este guia mostra exatamente como fazer isso com Aspose.Cells for Java. Você aprenderá a **adicionar intervalo nomeado**, **criar tabela Excel**, **definir nome da tabela** e **detectar erros de nome duplicado** em um único exemplo autônomo.

Trabalhar com intervalos nomeados é uma necessidade comum ao desenvolver ferramentas de relatório, planilhas de validação de dados ou dashboards dinâmicos. Ao final deste tutorial você terá um programa executável que cria com segurança um intervalo nomeado, constrói uma tabela e lida graciosamente com qualquer exceção de conflito de nome.

## Pré-requisitos

- Java 17 ou superior instalado
- Maven ou Gradle para gerenciamento de dependências
- Aspose.Cells for Java (última versão; coordenada Maven `com.aspose:aspose-cells:23.9` no momento da escrita)
- Familiaridade básica com conceitos do Excel, como planilhas, intervalos e tabelas

## Etapa 1: Criar um intervalo nomeado na pasta de trabalho

O primeiro passo é instanciar um objeto `Workbook` e adicionar um intervalo nomeado que aponta para um bloco específico de células.

```java
import com.aspose.cells.*;

public class NamedRangeDemo {
    public static void main(String[] args) throws Exception {
        // Initialize a new workbook
        Workbook workbook = new Workbook();

        // Get the default first worksheet (named "Sheet1")
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Define a named range called "MyRange" that covers A1:C5
        // This demonstrates the "add named range" operation.
        workbook.getNames().add("MyRange", "'Sheet1'!$A$1:$C$5");
```

**Por que isso importa:**  
Um intervalo nomeado funciona como uma referência reutilizável que fórmulas e tabelas podem usar. adicioná‑lo logo no início garante que as etapas subsequentes possam reutilizar o mesmo identificador sem codificar endereços de célula.

## Etapa 2: Criar tabela Excel que usa o intervalo nomeado

Em seguida, criamos uma tabela estruturada (ListObject) que ocupa a mesma área do intervalo nomeado. Isso ilustra o conceito de **criar tabela Excel**.

```java
        // Create an Excel table (ListObject) that spans the same area as the named range.
        // The parameters (0,0,4,2) represent the top‑left cell (A1) and bottom‑right cell (C5).
        ListObject table = sheet.getListObjects().add(0, 0, 4, 2, true);
```

**Por que isso importa:**  
Tabelas fornecem ordenação, filtragem e estilo integrados. Ao alinhar a tabela com o intervalo nomeado, você mantém o modelo de dados consistente.

## Etapa 3: Definir nome da tabela e tratar um possível conflito

Agora tentamos dar à tabela um nome que coincide com o intervalo nomeado criado anteriormente. Esta etapa demonstra **definir nome da tabela** e intencionalmente gera um conflito de nomes.

```java
        try {
            // Attempt to set the table name to "MyRange".
            // Because a named range with the same identifier already exists,
            // Aspose.Cells will throw an exception.
            table.setName("MyRange"); // <-- conflict expected
        } catch (Exception e) {
            // Step 4: Detect duplicate name and respond appropriately
            System.out.println("Name conflict detected: " + e.getMessage());
        }
```

**Por que isso importa:**  
O Excel não permite que uma tabela e um intervalo nomeado compartilhem o mesmo identificador. Detectar o conflito cedo impede pastas de trabalho corrompidas e facilita a depuração.

## Etapa 4: Detectar nome duplicado e resolvê‑lo

Quando a exceção é capturada, você pode renomear a tabela ou remover o intervalo nomeado em conflito. Abaixo está uma estratégia simples de resolução que renomeia a tabela com um sufixo.

```java
            // Resolve the conflict by appending a numeric suffix
            String baseName = "MyRange";
            int suffix = 1;
            String newName;
            do {
                newName = baseName + "_" + suffix;
                suffix++;
            } while (workbook.getNames().get(newName) != null);

            table.setName(newName);
            System.out.println("Table renamed to: " + newName);
        }

        // Save the workbook to verify the result
        workbook.save("NamedRangeDemo.xlsx");
    }
}
```

**Pontos‑chave da resolução:**

- **detectar nome duplicado** – o bloco `catch` confirma o conflito.
- O laço verifica a coleção de nomes da pasta de trabalho para garantir que o novo identificador seja único.
- Por fim, a pasta de trabalho é salva para que você possa abri‑la no Excel e verificar que a tabela tem um nome distinto enquanto o intervalo nomeado original permanece intacto.

## Exemplo completo e executável

Juntando todas as peças, o programa completo fica assim:

```java
import com.aspose.cells.*;

public class NamedRangeDemo {
    public static void main(String[] args) throws Exception {
        // Initialize workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Add a named range called "MyRange" covering A1:C5
        workbook.getNames().add("MyRange", "'Sheet1'!$A$1:$C$5");

        // Create an Excel table that occupies the same cells
        ListObject table = sheet.getListObjects().add(0, 0, 4, 2, true);

        try {
            // Try to set the table name to the same identifier
            table.setName("MyRange");
        } catch (Exception e) {
            // Detect duplicate name and resolve it
            System.out.println("Name conflict detected: " + e.getMessage());

            String baseName = "MyRange";
            int suffix = 1;
            String newName;
            do {
                newName = baseName + "_" + suffix;
                suffix++;
            } while (workbook.getNames().get(newName) != null);

            table.setName(newName);
            System.out.println("Table renamed to: " + newName);
        }

        // Save the file for inspection
        workbook.save("NamedRangeDemo.xlsx");
    }
}
```

**Saída esperada ao executar o programa:**

```
Name conflict detected: A name with the specified identifier already exists.
Table renamed to: MyRange_1
```

Abrir `NamedRangeDemo.xlsx` no Excel mostrará:

- Um intervalo nomeado **MyRange** que referencia as células A1:C5.
- Uma tabela chamada **MyRange_1** que cobre as mesmas células.
- Nenhum erro de nome ao adicionar fórmulas que referenciam `MyRange`.

## Armadilhas comuns e boas práticas

- **Não reutilize identificadores**: Sempre verifique se um nome já existe antes de atribuí‑lo a uma tabela.  
- **Prefira verificações explícitas**: `workbook.getNames().get("Name")` retorna `null` se o nome estiver livre, o que é mais seguro do que capturar uma exceção genérica.  
- **Mantenha convenções de nomenclatura consistentes**: Usar um prefixo como `tbl_` para tabelas e `rng_` para intervalos reduz a chance de colisões.  
- **Compatibilidade de versão**: O código funciona com Aspose.Cells 23.9 e posteriores; versões anteriores podem ter mensagens de exceção diferentes.

## Conclusão

Agora você sabe como **criar um intervalo nomeado**, **adicionar intervalo nomeado**, **criar tabela Excel**, **definir nome da tabela** e **detectar conflitos de nome duplicado** usando Aspose.Cells for Java. Ao tratar colisões de nomes de forma proativa, você mantém suas pastas de trabalho limpas e seus scripts de automação robustos.

**Próximos passos**

- Explore mais a API **definir nome da tabela** para aplicar opções de estilo.  
- Use o padrão **detectar nome duplicado** ao gerar múltiplas tabelas programaticamente.  
- Combine intervalos nomeados com fórmulas ou validação de dados para relatórios dinâmicos.

Boa codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Criar intervalo nomeado com estilo Excel Aspose Cells Java](/cells/hindi/java/tables-structured-references/create-style-named-range-excel-aspose-cells-java/)
- [Criar intervalo nomeado com estilo Excel Aspose Cells Java](/cells/german/java/tables-structured-references/create-style-named-range-excel-aspose-cells-java/)
- [Criar intervalo nomeado com estilo Excel Aspose Cells Java](/cells/french/java/tables-structured-references/create-style-named-range-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}