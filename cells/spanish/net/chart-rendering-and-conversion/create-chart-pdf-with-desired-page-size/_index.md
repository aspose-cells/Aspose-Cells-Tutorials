---
title: Crear un gráfico en formato PDF con el tamaño de página deseado
linktitle: Crear un gráfico en formato PDF con el tamaño de página deseado
second_title: API de procesamiento de Excel Aspose.Cells .NET
description: Cree un PDF con su gráfico de Excel usando Aspose.Cells para .NET. Aprenda cómo hacerlo con esta guía paso a paso.
weight: 12
url: /es/net/chart-rendering-and-conversion/create-chart-pdf-with-desired-page-size/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear un gráfico en formato PDF con el tamaño de página deseado

## Introducción

La creación de gráficos visualmente atractivos e informativos es esencial para la representación de datos en varios campos. Ya sea que trabaje con datos de ventas, métricas de rendimiento o cualquier otro tipo de información, tener la capacidad de producir gráficos de alta calidad le brinda profundidad y claridad a sus hallazgos. Si trabaja con aplicaciones .NET, Aspose.Cells es una biblioteca poderosa que facilita el manejo de documentos de Excel y la generación de gráficos. En este tutorial, lo guiaremos a través del proceso de creación de un PDF de un gráfico a partir de un archivo de Excel con el tamaño de página deseado.

## Prerrequisitos

Antes de sumergirte en el código, hay algunos requisitos previos que debes cumplir para garantizar una experiencia fluida:

### Conocimientos básicos de C# y .NET

Necesitará conocimientos básicos de programación en C# y del marco .NET. Esto le ayudará a comprender la estructura del código que encontrará en esta guía.

### Aspose.Cells para .NET

Asegúrese de tener instalado Aspose.Cells para .NET. Puede encontrar todos los detalles en[Documentación de Aspose.Cells](https://reference.aspose.com/cells/net/). 

### Entorno de desarrollo

 Configure su entorno de desarrollo. Puede ser Visual Studio o cualquier otro IDE que admita C#. Descargue e instale la biblioteca Aspose.Cells desde[página de descarga](https://releases.aspose.com/cells/net/).

### Archivo de Excel de muestra

Necesitará un archivo de Excel de muestra que contenga al menos un gráfico. Puede crear un archivo de muestra o descargar uno para utilizarlo en este tutorial.

## Importar paquetes

Para comenzar a trabajar con Aspose.Cells, debe importar los espacios de nombres necesarios en su aplicación C#. A continuación, le indicamos cómo hacerlo:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

using Aspose.Cells.Charts;
```

Estos espacios de nombres le brindan acceso a las clases y métodos necesarios para manipular los libros de Excel y sus contenidos.

Ahora que tenemos todos los requisitos previos resueltos, dividamos el proceso en pasos detallados.

## Paso 1: Configurar los directorios de origen y salida

Para comenzar, debe definir dónde se guardará el PDF de salida y dónde se encuentra el documento Excel de origen.

```csharp
//Directorio de salida
string outputDir = "Your Output Directory";

//Directorio de fuentes
string sourceDir = "Your Document Directory";
```

Asegúrese de reemplazar "Su directorio de salida" y "Su directorio de documentos" con las rutas reales de su sistema. Esto indica dónde guardará Aspose el PDF generado y dónde encontrará el archivo Excel.

## Paso 2: Cargue el archivo Excel de muestra

A continuación, debe cargar el archivo de Excel que contiene el gráfico. A continuación, le indicamos cómo hacerlo:

```csharp
//Cargue el archivo Excel de muestra que contiene el gráfico.
Workbook wb = new Workbook(sourceDir + "sampleCreateChartPDFWithDesiredPageSize.xlsx");
```

 El`Workbook` La clase es fundamental para interactuar con el documento de Excel. Asegúrese de que la ruta apunte correctamente al archivo de Excel; un error aquí impedirá que se ejecute el resto del código.

## Paso 3: Acceda a la primera hoja de trabajo

Una vez cargado el libro de trabajo, el siguiente paso es acceder a la hoja de trabajo que contiene el gráfico deseado.

```csharp
//Acceda a la primera hoja de trabajo.
Worksheet ws = wb.Worksheets[0];
```

 En Aspose.Cells, las hojas de trabajo se indexan a partir de cero, por lo que`Worksheets[0]` se refiere a la primera hoja.

## Paso 4: Acceda al primer gráfico

Ahora, accedamos al gráfico que desea exportar a PDF. Este paso supone que su hoja de cálculo contiene al menos un gráfico.

```csharp
//Acceda al primer gráfico dentro de la hoja de cálculo.
Chart ch = ws.Charts[0];
```

Nuevamente, esto accede al primer gráfico en la hoja de cálculo; asegúrese de que la estructura de su hoja de cálculo se adapte a este enfoque.

## Paso 5: Crea un PDF con el tamaño de página deseado

Finalmente, es momento de crear el PDF a partir del gráfico con un tamaño de página específico. Aquí está la línea mágica de código que lo hace todo:

```csharp
//Cree un gráfico en PDF con el tamaño de página deseado.
ch.ToPdf(outputDir + "outputCreateChartPDFWithDesiredPageSize.pdf", 7, 7, PageLayoutAlignmentType.Center, PageLayoutAlignmentType.Center);
```

En este código:
- El PDF se guardará en el directorio de salida que usted especificó anteriormente.
-  Los números`7, 7` representan el ancho y la altura del tamaño de página deseado, respectivamente.
- PageLayoutAlignmentType.Center garantiza que el gráfico esté centrado en la página.

## Paso 6: Mensaje de confirmación

Para que usted y los demás sepan que todo salió bien, incluya un mensaje de confirmación al final de su código:

```csharp
Console.WriteLine("CreateChartPDFWithDesiredPageSize executed successfully.");
```

Este mensaje aparecerá en la ventana de la consola una vez que se complete el proceso, indicando que su PDF se ha creado sin problemas.

## Conclusión

¡Felicitaciones! Acaba de aprender a aprovechar Aspose.Cells para .NET para crear un PDF a partir de un gráfico contenido en un archivo Excel. Esta potente biblioteca optimiza el proceso de manipulación de documentos Excel y la generación de representaciones visuales de datos, lo que le permite ahorrar horas de formateo manual. Asegúrese de explorar la gran cantidad de otras funciones que ofrece Aspose.Cells más allá de la generación de PDF: ¡nunca se sabe qué puede mejorar aún más sus proyectos!

## Preguntas frecuentes

### ¿Para qué se utiliza Aspose.Cells para .NET?  
Aspose.Cells para .NET se utiliza para crear, editar y convertir documentos de Excel mediante programación en aplicaciones .NET.

### ¿Puedo utilizar Aspose.Cells gratis?  
 Sí, Aspose.Cells ofrece una[prueba gratis](https://releases.aspose.com/) para fines de evaluación.

### ¿Hay alguna manera de extender mi prueba más allá del período inicial?  
 Puedes solicitar una[licencia temporal](https://purchase.aspose.com/temporary-license/) para pruebas extendidas.

### ¿Qué pasa si encuentro problemas o tengo preguntas?  
 Puede buscar ayuda en la comunidad de Aspose en su[foro de soporte](https://forum.aspose.com/c/cells/9).

### ¿Cómo puedo comprar Aspose.Cells?  
 Puedes comprar Aspose.Cells en[Página de compra](https://purchase.aspose.com/buy).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
