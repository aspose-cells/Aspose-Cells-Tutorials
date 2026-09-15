---
date: '2026-03-15'
description: Aprenda como dividir nomes em colunas separadas e salvar a planilha xlsx
  usando Aspose.Cells Java em um tutorial passo a passo.
keywords:
- Aspose.Cells Java
- split names columns
- Excel manipulation
- text to columns Java
- Java Excel processing
title: aspose cells java – Dividir Nomes em Colunas
url: /pt/java/cell-operations/aspose-cells-java-split-names-columns/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Dominando **aspose cells java**: Dividir Nomes em Colunas

Bem‑vindo ao nosso tutorial completo de **aspose cells java**. Neste guia você aprenderá **como dividir nomes** que estão armazenados em uma única coluna do Excel em duas colunas separadas — nome próprio e sobrenome — usando o poderoso recurso de texto‑para‑colunas. Seja para limpar uma lista de contatos, preparar dados para importação em um CRM ou simplesmente precisar de uma maneira rápida de reestruturar planilhas, este tutorial mostra exatamente como **salvar workbook xlsx** após a transformação.

## Respostas Rápidas
- **O que este tutorial cobre?** Divisão de strings de nome completo em colunas de nome próprio e sobrenome com Aspose.Cells para Java.  
- **Qual versão da biblioteca é usada?** A versão estável mais recente (a partir de 2026).  
- **Preciso de licença?** Uma avaliação gratuita funciona para desenvolvimento; uma licença comercial é necessária para produção.  
- **Posso dividir usando outros delimitadores?** Sim — basta alterar o separador em `TxtLoadOptions`.  
- **A saída é um arquivo .xlsx?** Absolutamente, a pasta de trabalho é salva no formato XLSX.

## O que é **aspose cells java**?
**Aspose.Cells java** é uma API Java de alto desempenho que permite a desenvolvedores criar, modificar, converter e renderizar arquivos Excel sem precisar do Microsoft Office. Ela suporta todos os principais formatos do Excel e oferece recursos avançados como fórmulas, gráficos e manipulação de dados.

## Por que usar **aspose cells java** para dividir nomes?
- **Zero‑install**: Funciona em qualquer ambiente Java server‑side.  
- **Velocidade**: Processa planilhas grandes mais rápido que a interoperação nativa do Excel.  
- **Precisão**: Controle total sobre delimitadores, intervalos de colunas e formatos de saída.  
- **Confiabilidade**: Sem dependências de COM ou Office, ideal para implantações em nuvem ou contêineres.

## Pré‑requisitos
- Java Development Kit (JDK) 8 ou superior.  
- Uma IDE como IntelliJ IDEA ou Eclipse (opcional, mas recomendada).  
- Maven ou Gradle para gerenciamento de dependências.  

### Configuração Maven
Adicione a dependência Aspose.Cells ao seu `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Configuração Gradle
Adicione a biblioteca ao seu `build.gradle`:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

> **Dica profissional:** Use uma licença temporária do portal Aspose para desbloquear toda a funcionalidade durante o desenvolvimento.

## Implementação Passo a Passo

### Etapa 1: Criar um Workbook e Acessar a Primeira Worksheet
Primeiro, importe as classes principais e instancie uma nova pasta de trabalho. Isso fornece um arquivo Excel limpo pronto para inserção de dados.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
```

```java
String dataDir = "YOUR_DATA_DIRECTORY"; // Define your directory path here

Workbook wb = new Workbook();
Worksheet ws = wb.getWorksheets().get(0);
```

### Etapa 2: Popular a Worksheet com Nomes de Exemplo
Em seguida, adicione algumas strings de nome completo à coluna **A**. Em um projeto real você leria esses valores de um banco de dados ou arquivo CSV.

```java
import com.aspose.cells.Cell;

String outDir = "YOUR_OUTPUT_DIRECTORY"; // Define your output directory path here

ws.getCells().get("A1").putValue("John Teal");
ws.getCells().get("A2").putValue("Peter Graham");
ws.getCells().get("A3").putValue("Brady Cortez");
ws.getCells().get("A4").putValue("Mack Nick");
ws.getCells().get("A5").putValue("Hsu Lee");
```

### Etapa 3: Configurar Text Load Options para Divisão de Colunas
A classe `TxtLoadOptions` informa ao Aspose.Cells como interpretar o texto. Aqui usamos um espaço (`' '`) como delimitador.

```java
import com.aspose.cells.TxtLoadOptions;

TxtLoadOptions opts = new TxtLoadOptions();
opts.setSeparator(' ');
```

### Etapa 4: Dividir o Texto em Duas Colunas
Agora chame `textToColumns()` na área de células que contém os nomes. Os parâmetros `(0, 0, 5, opts)` significam *iniciar na linha 0, coluna 0, processar 5 linhas, usando as opções que acabamos de definir*.

```java
ws.getCells().textToColumns(0, 0, 5, opts);
```

Após esta chamada, a coluna A contém os nomes próprios e a coluna B contém os sobrenomes.

### Etapa 5: Salvar o Workbook como Arquivo XLSX
Por fim, grave a pasta de trabalho modificada no disco. O enum `SaveFormat` garante que o arquivo seja armazenado no moderno formato XLSX.

```java
import com.aspose.cells.SaveFormat;

wb.save(outDir + "outputTextToColumns.xlsx");
```

> **Por que isso importa:** Ao usar **save workbook xlsx**, você garante compatibilidade com as versões mais recentes do Excel, Google Sheets e outras ferramentas de planilha.

## Aplicações Práticas
- **Limpeza de Dados:** Separe rapidamente campos concatenados antes de carregá‑los em pipelines de análise.  
- **Integração com CRM:** Transforme uma lista de contatos plana em uma tabela estruturada para importação.  
- **Sistemas de RH:** Divida nomes completos de funcionários para processamento de folha de pagamento ou benefícios.

## Considerações de Desempenho
Ao trabalhar com milhares de linhas:

1. **Atualizações em Lote:** Use `ws.getCells().setRowHeight()` ou métodos semelhantes em lote para reduzir a sobrecarga.  
2. **Gerenciamento de Memória:** Chame `wb.calculateFormula()` somente quando necessário e descarte objetos grandes prontamente.  
3. **Coleta de Lixo:** Execute a JVM com configurações adequadas de heap (`-Xmx2g` para arquivos grandes) para evitar erros OutOfMemory.

## Problemas Comuns e Soluções
| Problema | Solução |
|----------|---------|
| **Nomes contêm iniciais do meio** (ex.: “John A. Doe”) | Ajuste o separador ou pós‑procese a segunda coluna para extrair o sobrenome. |
| **Células vazias inesperadas** | Verifique se o intervalo de origem (`textToColumns` parâmetros) corresponde ao número real de linhas de dados. |
| **Licença não encontrada** | Coloque o arquivo de licença temporária (`Aspose.Cells.lic`) na raiz do projeto ou defina a licença programaticamente. |

## Perguntas Frequentes

**P: O que é Aspose.Cells Java?**  
R: Uma biblioteca poderosa que permite criar, modificar e converter arquivos Excel programaticamente usando Java.

**P: Posso dividir colunas com delimitadores diferentes de espaços?**  
R: Sim, personalize o separador `TxtLoadOptions` conforme a necessidade dos seus dados.

**P: Como lidar com grandes volumes de dados usando Aspose.Cells?**  
R: Otimize o desempenho gerenciando a memória e minimizando operações na pasta de trabalho, conforme descrito acima.

**P: Existe suporte disponível caso eu encontre problemas?**  
R: Visite o [Aspose Forum](https://forum.aspose.com/c/cells/9) para ajuda da comunidade ou entre em contato diretamente com a equipe de suporte da Aspose.

**P: Em quais formatos o Aspose.Cells pode salvar workbooks?**  
R: Suporta uma ampla gama de formatos Excel, incluindo XLSX, XLS, CSV e mais.

## Recursos

- **Documentação**: [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)
- **Download**: [Aspose.Cells Java Releases](https://releases.aspose.com/cells/java/)
- **Compra**: [Buy Aspose.Cells](https://purchase.aspose.com/buy)
- **Teste Gratuito**: [Try Aspose.Cells for Free](https://releases.aspose.com/cells/java/)
- **Licença Temporária**: [Request a Temporary License](https://purchase.aspose.com/temporary-license/)

Bom desenvolvimento e aproveite todo o poder do **aspose cells java** em seus projetos!

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**Última atualização:** 2026-03-15  
**Testado com:** Aspose.Cells 25.3 for Java  
**Autor:** Aspose