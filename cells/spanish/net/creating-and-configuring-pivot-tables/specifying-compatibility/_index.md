---
title: Especificar la compatibilidad de archivos Excel mediante programación en .NET
linktitle: Especificar la compatibilidad de archivos Excel mediante programación en .NET
second_title: API de procesamiento de Excel Aspose.Cells .NET
description: Aprenda a manipular tablas dinámicas de Excel con Aspose.Cells para .NET, incluidas actualizaciones de datos, configuraciones de compatibilidad y formato de celdas.
weight: 23
url: /es/net/creating-and-configuring-pivot-tables/specifying-compatibility/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Especificar la compatibilidad de archivos Excel mediante programación en .NET

## Introducción

En el mundo actual, impulsado por los datos, la gestión y manipulación de archivos de Excel mediante programación se ha vuelto esencial para muchos desarrolladores. Si trabaja con Excel en .NET, Aspose.Cells es una potente biblioteca que facilita la creación, lectura, modificación y guardado de archivos de Excel. Una característica importante de esta biblioteca le permite especificar la compatibilidad de los archivos de Excel mediante programación. En este tutorial, exploraremos cómo manipular archivos de Excel, centrándonos especialmente en la gestión de la compatibilidad mediante Aspose.Cells para .NET. Al final, comprenderá cómo establecer la compatibilidad de los archivos de Excel, especialmente para las tablas dinámicas, mientras actualiza y administra los datos.

## Prerrequisitos

Antes de sumergirse en la fase de codificación, asegúrese de tener lo siguiente:

1. Conocimientos básicos de C#: dado que escribiremos código en C#, la familiaridad con el lenguaje le ayudará a comprender mejor el tutorial.
2.  Biblioteca Aspose.Cells para .NET: puede descargarla desde[Página de lanzamiento de Aspose Cells](https://releases.aspose.com/cells/net/)Si aún no lo has hecho, considera obtener una prueba gratuita para explorar sus funciones primero.
3. Visual Studio: un IDE donde puedes escribir y probar tu código C# de manera efectiva.
4.  Archivo de Excel de muestra: asegúrese de tener un archivo de Excel de muestra, preferiblemente uno que contenga una tabla dinámica para la demostración. Para nuestro ejemplo, usaremos`sample-pivot-table.xlsx`.

Con estos requisitos previos establecidos, comencemos con el proceso de codificación.

## Importar paquetes

Antes de comenzar a escribir su aplicación, debe incluir los espacios de nombres necesarios en su código para utilizar la biblioteca Aspose.Cells de manera eficaz. A continuación, le indicamos cómo hacerlo.

### Importar el espacio de nombres Aspose.Cells

```csharp
using System.IO;
using System;
using Aspose.Cells;
using Aspose.Cells.Pivot;
using System.Drawing;
```

Esta línea de código garantiza que pueda acceder a todas las clases y métodos dentro de la biblioteca Aspose.Cells.

Ahora, analicemos el proceso en detalle para asegurarnos de que todo esté claro y comprensible.

## Paso 1: Configura tu directorio

Lo primero es lo primero: configure el directorio donde se encuentran sus archivos de Excel. Es importante proporcionar la ruta de archivo correcta.

```csharp
// La ruta al directorio de documentos.
string dataDir = "Your Document Directory";
```

 Aquí, reemplace`"Your Document Directory"`con la ruta real a sus archivos de Excel. Aquí es donde debería estar su archivo de tabla dinámica de muestra.

## Paso 2: Cargue el archivo Excel de origen

A continuación, debemos cargar el archivo Excel que contiene la tabla dinámica de muestra. 

```csharp
// Cargar archivo fuente de Excel que contiene una tabla dinámica de muestra
Workbook wb = new Workbook(dataDir + "sample-pivot-table.xlsx");
```

 En este paso, creamos una instancia del`Workbook` clase, que carga el archivo Excel especificado. 

## Paso 3: Acceda a las hojas de trabajo

Ahora que el libro de trabajo está cargado, debe acceder a la hoja de trabajo que contiene los datos de la tabla dinámica.

```csharp
// Acceda a la primera hoja de cálculo que contiene datos de la tabla dinámica
Worksheet dataSheet = wb.Worksheets[0];
```

Aquí accedemos a la primera hoja de cálculo donde se encuentra la tabla dinámica. También puedes recorrer o especificar otras hojas de cálculo en función de tu estructura de Excel.

## Paso 4: Manipular los datos de la celda

A continuación, modificará algunos valores de celda en la hoja de cálculo. 

### Paso 4.1: Modificar la celda A3

Comencemos accediendo a la celda A3 y estableciendo su valor.

```csharp
// Accede a la celda A3 y establece sus datos
Cells cells = dataSheet.Cells;
Cell cell = cells["A3"];
cell.PutValue("FooBar");
```

Este fragmento de código actualiza la celda A3 con el valor “FooBar”.

### Paso 4.2: Modificar la celda B3 con una cadena larga

Ahora, coloquemos una cadena larga en la celda B3, que excede los límites de caracteres estándar de Excel.

```csharp
// Accede a la celda B3 y establece sus datos
string longStr = "Very long text 1. very long text 2.... [continue your long string]";
cell = cells["B3"];
cell.PutValue(longStr);
```

Este código es importante porque establece sus expectativas con respecto a los límites de datos, especialmente cuando se trabaja con configuraciones de compatibilidad en Excel.

## Paso 5: Verifique la longitud de la celda B3

También es esencial confirmar la longitud de la cadena que ingresamos.

```csharp
// Imprima la longitud de la cadena de la celda B3
Console.WriteLine("Length of original data string: " + cell.StringValue.Length);
```

Esto es sólo para verificación para mostrar cuántos caracteres contiene su celda.

## Paso 6: Establecer otros valores de celda

Ahora accederemos a más celdas y estableceremos algunos valores.

```csharp
// Accede a la celda C3 y establece sus datos
cell = cells["C3"];
cell.PutValue("closed");

// Accede a la celda D3 y establece sus datos
cell = cells["D3"];
cell.PutValue("2016/07/21");
```

Cada uno de estos fragmentos actualiza varias celdas adicionales dentro de la hoja de cálculo.

## Paso 7: Acceda a la tabla dinámica

A continuación, accederá a la segunda hoja de trabajo, que contiene los datos de la tabla dinámica.

```csharp
//Acceda a la segunda hoja de cálculo que contiene la tabla dinámica
Worksheet pivotSheet = wb.Worksheets[1];

// Acceder a la tabla dinámica
PivotTable pivotTable = pivotSheet.PivotTables[0];
```

Este fragmento le permite manipular la tabla dinámica para realizar configuraciones de compatibilidad.

## Paso 8: Establecer compatibilidad para Excel 2003

Es fundamental determinar si su tabla dinámica es compatible con Excel 2003 o no. 

```csharp
// La propiedad IsExcel2003Compatible indica si la tabla dinámica es compatible con Excel2003 al actualizar la tabla dinámica
pivotTable.IsExcel2003Compatible = true;
pivotTable.RefreshData();
pivotTable.CalculateData();
```

 Aquí es donde comienza la verdadera transformación. Al establecer`IsExcel2003Compatible` a`true`, limita la longitud de caracteres a 255 al actualizar.

## Paso 9: Verificar la longitud después de la configuración de compatibilidad

Después de configurar la compatibilidad, veamos cómo afecta a los datos.

```csharp
// Verifique el valor de la celda B5 de la hoja dinámica.
Cell b5 = pivotSheet.Cells["B5"];
Console.WriteLine("Length of cell B5 after setting IsExcel2003Compatible property to True: " + b5.StringValue.Length);
```

Probablemente verá una salida que confirme el efecto de truncamiento si los datos iniciales superan los 255 caracteres.

## Paso 10: Cambiar la configuración de compatibilidad

Ahora, cambiemos la configuración de compatibilidad y verifiquemos nuevamente.

```csharp
//Ahora configure la propiedad IsExcel2003Compatible en falso y actualice nuevamente
pivotTable.IsExcel2003Compatible = false;
pivotTable.RefreshData();
pivotTable.CalculateData();
```

Esto permite que sus datos reflejen su longitud original sin las restricciones anteriores.

## Paso 11: Verifique la longitud nuevamente 

Verifiquemos que los datos ahora reflejan con precisión su longitud real.

```csharp
// Ahora se imprimirá la longitud original de los datos de la celda. Los datos ya no se han truncado.
b5 = pivotSheet.Cells["B5"];
Console.WriteLine("Length of cell B5 after setting IsExcel2003Compatible property to False: " + b5.StringValue.Length);
```

Debería ver que la salida confirma la eliminación del truncamiento.

## Paso 12: Formatear las celdas

Para mejorar la experiencia visual, es posible que desees formatear las celdas. 

```csharp
// Establezca la altura de la fila y el ancho de la columna de la celda B5 y también ajuste su texto
pivotSheet.Cells.SetRowHeight(b5.Row, 100);
pivotSheet.Cells.SetColumnWidth(b5.Column, 65);
Style st = b5.GetStyle();
st.IsTextWrapped = true;
b5.SetStyle(st);
```

Estas líneas de código hacen que los datos sean más fáciles de leer ajustando las dimensiones de la celda y habilitando el ajuste de texto.

## Paso 13: Guardar el libro de trabajo

Por último, guarda tu libro de trabajo con los cambios que has realizado.

```csharp
// Guardar libro de trabajo en formato xlsx
wb.Save(dataDir + "SpecifyCompatibility_out.xlsx", SaveFormat.Xlsx);
```

 Elegir un formato de archivo adecuado es crucial al guardar archivos de Excel.`Xlsx`El formato es ampliamente utilizado y compatible con muchas versiones de Excel.

## Conclusión

¡Felicitaciones! Ya programó la configuración de compatibilidad de archivos de Excel con Aspose.Cells para .NET. Este tutorial describe cada paso, desde la configuración de su entorno hasta la modificación de la configuración de compatibilidad para tablas dinámicas. Si alguna vez trabajó con datos que requerían limitaciones o compatibilidad específicas, esta es una habilidad que no querrá pasar por alto.

## Preguntas frecuentes

### ¿Qué es Aspose.Cells?  
Aspose.Cells es una biblioteca .NET diseñada para ayudar a los desarrolladores a crear, manipular y convertir archivos Excel sin problemas.

### ¿Por qué es importante la compatibilidad con Excel?  
La compatibilidad con Excel es crucial para garantizar que los archivos puedan abrirse y usarse en las versiones previstas de Excel, especialmente si contienen características o formatos no compatibles con versiones anteriores.

### ¿Puedo crear tablas dinámicas mediante programación con Aspose.Cells?  
Sí, puede crear y manipular tablas dinámicas mediante programación utilizando Aspose.Cells. La biblioteca proporciona varios métodos para agregar fuentes de datos, campos y funciones asociadas con las tablas dinámicas.

### ¿Cómo puedo verificar la longitud de una cadena en una celda de Excel?  
Puedes utilizar el`StringValue` propiedad de un`Cell` objeto para obtener el contenido de la celda y luego llamar al`.Length` Propiedad para averiguar la longitud de la cadena.

### ¿Puedo personalizar el formato de celda más allá del alto y ancho de la fila?  
 ¡Por supuesto! Aspose.Cells permite un amplio formato de celdas. Puede cambiar estilos de fuente, colores, bordes, formatos de números y mucho más a través de la`Style` clase.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
