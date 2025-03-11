---
title: Exportar valores de cadenas HTML de celdas a una tabla de datos en Excel
linktitle: Exportar valores de cadenas HTML de celdas a una tabla de datos en Excel
second_title: API de procesamiento de Excel Aspose.Cells .NET
description: Aprenda a exportar valores de cadena HTML desde celdas de Excel a una DataTable usando Aspose.Cells para .NET en un sencillo tutorial paso a paso.
weight: 11
url: /es/net/excel-data-sorting-exporting/export-html-string-value-of-cells-to-datatable-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exportar valores de cadenas HTML de celdas a una tabla de datos en Excel

## Introducción

Al trabajar con archivos de Excel en un entorno .NET, es posible que necesite extraer información de las celdas, no solo como texto sin formato, sino como cadenas HTML. Esto puede resultar muy útil cuando trabaja con datos de texto enriquecido o cuando desea mantener el formato. En esta guía, le mostraré cómo exportar el valor de la cadena HTML de las celdas a una DataTable mediante Aspose.Cells para .NET. 

## Prerrequisitos

Antes de sumergirnos en el código, asegurémonos de que tienes todo lo que necesitas en su lugar. Aquí tienes una lista de verificación rápida:

1. Conocimientos básicos de C# y .NET: antes de comenzar a codificar, asegúrese de estar familiarizado con la programación en C# y los conceptos básicos del marco .NET.
2.  Aspose.Cells para .NET: Si aún no lo ha hecho, debe instalar Aspose.Cells para .NET. Puede descargar una versión de prueba gratuita desde[aquí](https://releases.aspose.com/).
3. Visual Studio o el IDE de su elección: configure su entorno para escribir código C#. Se recomienda Visual Studio por su amplia gama de funciones y facilidad de uso.
4. Archivo de Excel de muestra: Necesitará un archivo de Excel de muestra (`sampleExportTableAsHtmlString.xlsx`) con el que trabajar. Asegúrese de que esté ubicado en un directorio al que se pueda acceder.
5. Administrador de paquetes NuGet: asegúrese de tener acceso al Administrador de paquetes NuGet en su proyecto para agregar fácilmente la biblioteca Aspose.Cells.

Con estos requisitos previos en regla, ¡manos a la obra con algo de codificación!

## Importar paquetes

Antes de poder empezar a trabajar con Aspose.Cells, debemos importar los paquetes necesarios. Esto suele implicar agregar el paquete NuGet Aspose.Cells a su proyecto. A continuación, le indicamos cómo hacerlo:

### Abrir el Administrador de paquetes NuGet

En Visual Studio, haga clic con el botón derecho en su proyecto en el Explorador de soluciones y seleccione Administrar paquetes NuGet.

### Buscar Aspose.Cells

 En el Administrador de paquetes NuGet, escriba`Aspose.Cells` en la barra de búsqueda.

### Instalar el paquete

Una vez que encuentre Aspose.Cells, haga clic en el botón Instalar. Esto agregará la biblioteca a su proyecto y le permitirá importarla en su código.

### Importar el espacio de nombres

Agregue la siguiente directiva using en la parte superior de su archivo de código:

```csharp
using System;
using System.IO;
using Aspose.Cells;
using System.Data;
```

Ahora que hemos configurado todo, profundicemos en el proceso paso a paso de exportación de valores de cadena HTML desde un archivo Excel a una DataTable. 

## Paso 1: Definir el directorio de origen

Para comenzar, deberá definir el directorio en el que se almacena el archivo de Excel de muestra. Esto es fundamental, ya que le indica a su aplicación dónde encontrar el archivo. Este es el código para ello:

```csharp
string sourceDir = "Your Document Directory";
```

 Asegúrese de reemplazar`"Your Document Directory"` con la ruta real a su archivo Excel.

## Paso 2: Cargue el archivo Excel de muestra

 El siguiente paso es cargar el libro de Excel. Para ello, utilizará el`Workbook` Clase de Aspose.Cells para hacer esto. Aquí se explica cómo cargar el archivo:

```csharp
Workbook wb = new Workbook(sourceDir + "sampleExportTableAsHtmlString.xlsx");
```

Esta simple línea de código inicializa el libro de trabajo y carga el archivo Excel especificado.

## Paso 3: Acceda a la primera hoja de trabajo

Una vez cargado el libro de trabajo, deberá acceder a la hoja de trabajo específica que contiene los datos que le interesan. Por lo general, comenzará con la primera hoja de trabajo:

```csharp
Worksheet ws = wb.Worksheets[0];
```

Aquí, trabajamos con la primera hoja de cálculo (índice 0). Asegúrate de que tus datos estén en la hoja correcta.

## Paso 4: Especificar las opciones de la tabla de exportación

Para controlar cómo se exportan los datos, debe configurar`ExportTableOptions`En este caso, desea asegurarse de que los nombres de las columnas no se exporten y desea que los datos de las celdas se exporten como cadenas HTML:

```csharp
ExportTableOptions opts = new ExportTableOptions();
opts.ExportColumnName = false;
opts.ExportAsHtmlString = true;
```

Esta configuración le permite mantener el formato enriquecido de los datos de su celda al exportar.

## Paso 5: Exportar celdas a DataTable

 Ahora viene la parte crucial, donde realmente se exportan los datos.`ExportDataTable` método, puede extraer los datos de la hoja de cálculo a una`DataTable`A continuación te explicamos cómo hacerlo:

```csharp
DataTable dt = ws.Cells.ExportDataTable(0, 0, 3, 3, opts);
```

Este código exporta un rango específico de celdas (desde la fila 0, columna 0 hasta la fila 3, columna 3) a una DataTable utilizando las opciones especificadas anteriormente.

## Paso 6: Imprima el valor de la cadena HTML

Por último, imprimamos el valor de la cadena HTML de una celda específica en la DataTable para ver lo que hemos logrado exportar. Por ejemplo, si desea imprimir el valor de la tercera fila y la segunda columna, deberá hacer lo siguiente:

```csharp
Console.WriteLine(dt.Rows[2][1].ToString());
```

Esta línea imprime la cadena HTML deseada desde DataTable en la consola. 

## Conclusión 

¡Y ya está! Ha exportado con éxito valores de cadena HTML desde celdas de un archivo Excel a una DataTable utilizando Aspose.Cells para .NET. Esta capacidad no solo enriquece sus habilidades de manipulación de datos, sino que también amplía sus opciones al trabajar con contenido formateado directamente desde archivos Excel. 

## Preguntas frecuentes

### ¿Puedo usar Aspose.Cells para otros formatos de archivo además de Excel?  
Sí, Aspose.Cells es principalmente para Excel, pero Aspose ofrece otras bibliotecas para diferentes formatos.

### ¿Necesito una licencia para Aspose.Cells?  
 Sí, se requiere una licencia válida para el uso en producción. Puede obtener una licencia temporal[aquí](https://purchase.aspose.com/temporary-license/).

### ¿Qué pasa si mi archivo de Excel contiene fórmulas? ¿Se exportarán correctamente?  
Sí, Aspose.Cells puede manejar fórmulas y, al exportarlas, se evaluarán según sus valores resultantes.

### ¿Es posible cambiar las opciones de exportación?  
 ¡Por supuesto! Puedes personalizarlo`ExportTableOptions` para adaptarse a sus necesidades específicas.

### ¿Dónde puedo encontrar documentación más detallada sobre Aspose.Cells?  
 Puede encontrar una amplia documentación[aquí](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
