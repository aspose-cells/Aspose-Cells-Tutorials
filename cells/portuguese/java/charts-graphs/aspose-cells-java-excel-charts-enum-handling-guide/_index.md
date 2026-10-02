---
date: '2026-04-11'
description: Aprenda como exibir a versão do Aspose Cells, carregar uma pasta de trabalho
  Excel em Java e manipular enums de gráficos com Aspose.Cells. Siga exemplos passo
  a passo.
keywords:
- display aspose cells version
- load excel workbook java
- excel chart manipulation
title: Exibir a versão do Aspose Cells e o tratamento de enumeração de gráficos em
  Java
url: /pt/java/charts-graphs/aspose-cells-java-excel-charts-enum-handling-guide/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Exibir Versão do Aspose Cells e Manipulação de Enum de Gráfico em Java

## Introdução

Se você precisa **exibir a versão do Aspose Cells**, carregar uma pasta de trabalho Excel em Java e trabalhar com enums de gráfico, você está no lugar certo. Neste tutorial, percorreremos os passos exatos que você precisa para integrar o Aspose.Cells para Java em seus projetos, extrair dados de gráficos e converter enums baseados em inteiros em strings legíveis. Ao final, você terá uma solução sólida e pronta para produção que pode ser inserida diretamente em sua base de código.

**O que você aprenderá**
- Como exibir a versão do Aspose.Cells.
- Como **carregar uma pasta de trabalho Excel em Java** e acessar dados de gráfico.
- Como converter valores de enum inteiros em seus equivalentes de string.
- Como recuperar os tipos de valor X e Y de um ponto de gráfico.

Vamos começar!

## Respostas Rápidas
- **Como verifico a versão do Aspose.Cells?** Chame `CellsHelper.getVersion()` e imprima o resultado.  
- **Qual coordenada Maven adiciona o Aspose.Cells?** `com.aspose:aspose-cells:25.3`.  
- **Posso carregar uma pasta de trabalho Excel em Java?** Sim—use `new Workbook(filePath)`.  
- **Como os valores de enum são convertidos?** Armazene um `HashMap<Integer, String>` e procure a chave inteira.  
- **Qual método imprime os tipos de valor X/Y?** `pnt.getXValueType()` e `pnt.getYValueType()`.

## O que é “exibir versão do Aspose Cells”?
A frase refere‑se à obtenção da string de versão da biblioteca em tempo de execução. Conhecer a versão exata ajuda na depuração, garante compatibilidade e confirma que sua licença está aplicada à versão pretendida.

## Por que exibir a versão e carregar a pasta de trabalho Excel em Java?
- **Depuração** – Confirma que a biblioteca correta está no classpath.  
- **Conformidade** – Facilita a verificação de que você está usando uma versão licenciada.  
- **Automação** – Permite scripts que se adaptam a diferentes versões da biblioteca sem alterações manuais.  

## Prerequisites

### Bibliotecas e Dependências Necessárias
- **Aspose.Cells for Java** – biblioteca principal para manipulação de Excel.  
- **Java Development Kit (JDK)** – versão 8 ou superior.

### Configuração do Ambiente
- IDE de sua escolha (IntelliJ IDEA, Eclipse, NetBeans).  
- Ferramenta de build: Maven **ou** Gradle (instruções abaixo).

### Conhecimentos Necessários
- Programação Java básica.  
- Familiaridade com conceitos de Excel (planilhas, gráficos) é útil, mas não obrigatória.

## Setting Up Aspose.Cells for Java

### Usando Maven
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Usando Gradle
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### Etapas de Aquisição de Licença
- **Teste Gratuito**: Baixe em [Aspose's Release Page](https://releases.aspose.com/cells/java/).  
- **Licença Temporária**: Obtenha uma licença de curto prazo em [Aspose's Temporary License Page](https://purchase.aspose.com/temporary-license/).  
- **Compra**: Para projetos de longo prazo, compre uma licença através da [Aspose Purchase Page](https://purchase.aspose.com/buy).

### Inicialização e Configuração Básicas
```java
import com.aspose.cells.*;

public class InitializeAsposeCells {
    public static void main(String[] args) {
        // Set the license if available
        License license = new License();
        try {
            license.setLicense("Path_to_License_File");
        } catch (Exception e) {
            System.out.println("Error setting license: " + e.getMessage());
        }

        // Print Aspose.Cells version to confirm setup
        System.out.println("Aspose.Cells for Java Version: " + CellsHelper.getVersion());
    }
}
```

## Guia de Implementação

### Como Exibir a Versão do Aspose Cells
**Visão geral** – Verifique rapidamente a versão da biblioteca em tempo de execução.

#### Passo 1: Importar Pacotes Necessários
```java
import com.aspose.cells.*;
```

#### Passo 2: Criar uma Classe e o Método Main
```java
public class DisplayAsposeCellsVersion {
    public static void main(String[] args) throws Exception {
        // This prints the Aspose.Cells version
        System.out.println("Aspose.Cells for Java Version: " + CellsHelper.getVersion());
    }
}
```

#### Explicação
- `CellsHelper.getVersion()` retorna a string exata da versão da DLL Aspose.Cells que sua aplicação está usando.

### Como Converter Enums Inteiros em Enums de String
**Visão geral** – Transforme valores numéricos de enum (ex., `CellValueType.IS_NUMERIC`) em texto legível.

#### Passo 1: Configurar HashMap para Conversão
```java
import java.util.HashMap;

HashMap<Integer, String> cvTypes = new HashMap<>();
cvTypes.put(CellValueType.IS_NUMERIC, "IsNumeric");
cvTypes.put(CellValueType.IS_STRING, "IsString");
```

#### Passo 2: Converter e Imprimir o Valor do Enum
```java
public class EnumConversion {
    public static void main(String[] args) {
        int exampleEnumValue = CellValueType.IS_NUMERIC;
        System.out.println("Converted Enum Value: " + cvTypes.get(exampleEnumValue));
    }
}
```

#### Explicação
- O mapa `cvTypes` preenche a lacuna entre a constante numérica e um rótulo legível por humanos.

### Como Carregar Pasta de Trabalho Excel em Java e Acessar Dados de Gráfico
**Visão geral** – Abra uma pasta de trabalho existente, localize um gráfico e garanta que seus dados estejam atualizados.

#### Passo 1: Importar Pacotes Necessários
```java
import com.aspose.cells.*;
```

#### Passo 2: Carregar a Pasta de Trabalho e Acessar a Planilha
```java
public class LoadExcelAndAccessChart {
    static String dataDir = "YOUR_DATA_DIRECTORY";

    public static void main(String[] args) throws Exception {
        Workbook wb = new Workbook(dataDir + "/sampleFindTypeOfXandYValuesOfPointsInChartSeries.xlsx");
        Worksheet ws = wb.getWorksheets().get(0);
        Chart ch = ws.getCharts().get(0);
        ch.calculate();
    }
}
```

#### Explicação
- `new Workbook(filePath)` carrega o arquivo na memória.  
- `ch.calculate()` força o gráfico a recalcular quaisquer fórmulas para que os dados lidos estejam atuais.

### Como Recuperar e Imprimir os Tipos de Valor X e Y de um Ponto de Gráfico
**Visão geral** – Extraia o tipo de dado dos valores X e Y de um ponto específico.

#### Passo 1: Configurar HashMap de Conversão de Enum (reutilizar do passo anterior)
```java
HashMap<Integer, String> cvTypes = new HashMap<>();
cvTypes.put(CellValueType.IS_NUMERIC, "IsNumeric");
cvTypes.put(CellValueType.IS_STRING, "IsString");
```

#### Passo 2: Acessar o Ponto do Gráfico e Imprimir os Tipos de Valor
```java
public class RetrieveChartPointTypes {
    static String dataDir = "YOUR_DATA_DIRECTORY";

    public static void main(String[] args) throws Exception {
        Workbook wb = new Workbook(dataDir + "/sampleFindTypeOfXandYValuesOfPointsInChartSeries.xlsx");
        Worksheet ws = wb.getWorksheets().get(0);
        Chart ch = ws.getCharts().get(0);
        ch.calculate();

        ChartPoint pnt = ch.getNSeries().get(0).getPoints().get(0);

        System.out.println("X Value Type: " + cvTypes.get(pnt.getXValueType()));
        System.out.println("Y Value Type: " + cvTypes.get(pnt.getYValueType()));
    }
}
```

#### Explicação
- `pnt.getXValueType()` / `pnt.getYValueType()` retornam constantes inteiras que indicam se o valor é numérico, string, data, etc.  
- O mapa `cvTypes` traduz esses inteiros em texto legível.

## Aplicações Práticas
1. **Relatórios Financeiros** – Gere automaticamente gráficos com tipos de dados verificados para trilhas de auditoria.  
2. **Painéis de Visualização de Dados** – Extraia pontos de gráfico para componentes de UI personalizados.  
3. **Testes Automatizados** – Valide que as séries de gráficos contenham os tipos de dados esperados.  
4. **Inteligência de Negócios** – Alimente metadados de gráficos em pipelines de análise posteriores.  
5. **Ferramentas de Relatórios Personalizadas** – Construa motores de relatório sob medida que necessitam de manipulação precisa de enums.

## Considerações de Desempenho
- **Carregue Apenas as Planilhas Necessárias** – Use `Workbook.getWorksheets().get(index)` ao invés de carregar todas as planilhas ao lidar com arquivos grandes.  
- **Descarte Objetos Rapidamente** – Defina as referências da pasta de trabalho como `null` após o processamento para auxiliar a coleta de lixo.  
- **Processamento em Lote de Arquivos** – Ao lidar com muitas pastas de trabalho, processe-as em lotes para manter o uso de memória previsível.

## Problemas Comuns & Soluções
- **Licença Não Encontrada** – Certifique‑se de que o caminho do arquivo de licença está correto e que o arquivo está incluído na saída da build.  
- **Gráfico Não Calculado** – Sempre chame `chart.calculate()` antes de ler os valores dos pontos.  
- **Mapeamento de Enum Incorreto** – Verifique se você adicionou todas as constantes relevantes de `CellValueType` ao `HashMap`.  

## Perguntas Frequentes

**P: Posso usar este código com Aspose.Cells 24.x?**  
**R:** Sim, a API para recuperação de versão, carregamento de pasta de trabalho e acesso a pontos de gráfico permaneceu estável nas versões recentes.

**P: E se meu gráfico contiver valores de data?**  
**R:** Adicione `CellValueType.IS_DATE_TIME` ao mapa `cvTypes` e mapeie‑o para `"IsDateTime"`.

**P: Preciso de licença para uso de teste?**  
**R:** Uma licença de teste é necessária para funcionalidade completa; sem ela você verá marcas d'água nos arquivos gerados.

**P: Como lidar com múltiplas planilhas?**  
**R:** Itere através de `wb.getWorksheets()` e processe cada objeto `Chart` que encontrar.

**P: Existe uma forma de exportar os dados do gráfico para CSV?**  
**R:** Sim—extraia os valores das séries via `chart.getNSeries().get(i).getValues()` e escreva‑os usando I/O padrão do Java.

---

**Last Updated:** 2026-04-11  
**Tested With:** Aspose.Cells 25.3 for Java  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}