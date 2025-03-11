---
title: Aplicar formato 3D al gráfico
linktitle: Aplicar formato 3D al gráfico
second_title: API de procesamiento de Excel Aspose.Cells .NET
description: Descubra cómo crear gráficos 3D impresionantes en Excel con Aspose.Cells para .NET. Siga nuestra sencilla guía paso a paso.
weight: 10
url: /es/net/advanced-chart-operations/apply-3d-format-to-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aplicar formato 3D al gráfico

## Introducción

En una era en la que la visualización de datos es primordial, la forma en que presentamos nuestros datos va más allá de los gráficos y diagramas básicos. Con herramientas como Aspose.Cells para .NET, puede mejorar sus presentaciones de datos con gráficos 3D sorprendentes que no solo captan la atención, sino que también transmiten la información de manera eficaz. Esta guía lo guiará por los pasos para aplicar un formato 3D a un gráfico con Aspose.Cells, transformando sus datos sin procesar en una presentación atractiva.

## Prerrequisitos

Antes de profundizar en los detalles de la aplicación de un formato 3D a un gráfico, asegurémonos de que tienes todo lo que necesitas.

### Requisitos de software

- Visual Studio: asegúrese de tener instalado Visual Studio para trabajar con aplicaciones .NET.
-  Aspose.Cells para .NET: Si aún no lo ha hecho, descargue e instale Aspose.Cells desde[aquí](https://releases.aspose.com/cells/net/).

### Configuración del entorno de codificación

1. Cree un nuevo proyecto .NET: abra Visual Studio, seleccione “Crear un nuevo proyecto” y elija una aplicación de consola.
2. Agregar referencia de Aspose.Cells: a través del Administrador de paquetes NuGet, agregue Aspose.Cells buscándolo o mediante la Consola del Administrador de paquetes:

```bash
Install-Package Aspose.Cells
```

3. Configurar el directorio de salida: designe un directorio de salida donde se guardarán los archivos generados; esto puede ser tan simple como crear una carpeta en su escritorio.

Ahora que ya está todo configurado, ¡es hora de adentrarnos en el código y crear unos gráficos 3D impresionantes!

## Importar paquetes

Para comenzar, debe importar los espacios de nombres necesarios. Esto le ayudará a acceder a las clases y métodos proporcionados por Aspose.Cells. A continuación, le indicamos cómo hacerlo:

```csharp
using System;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
using Aspose.Cells.Charts;
```

Esta sección dividirá el proceso en pasos manejables, brindándole una comprensión clara de cada etapa.

## Paso 1: Inicialice su libro de trabajo

 Primero, necesitas crear una instancia del`Workbook` Clase. Este objeto servirá como base para su documento de Excel.

```csharp
//Directorio de salida
string outputDir = "Your Document Directory";
Workbook book = new Workbook();
```
 Piensa en esto`Workbook` como un lienzo en blanco, listo para que lo llenes con datos coloridos y visualizaciones impactantes.

## Paso 2: Cambiar el nombre de la primera hoja de trabajo

A continuación, cambiemos el nombre de la primera hoja de cálculo. Esto nos permitirá saber claramente con qué datos estamos trabajando.

```csharp
book.Worksheets[0].Name = "DataSheet";
```

Los nombres deben ser intuitivos. En este caso, lo llamaremos "Hoja de datos" para saber dónde se encuentran nuestros datos.

## Paso 3: Crear datos para el gráfico

Ahora, agregaremos algunos datos a nuestra "Hoja de datos". Completemos la hoja con los valores que utilizará nuestro gráfico.

```csharp
Worksheet dataSheet = book.Worksheets["DataSheet"];
dataSheet.Cells["B1"].PutValue(1);
dataSheet.Cells["B2"].PutValue(2);
dataSheet.Cells["B3"].PutValue(3);
dataSheet.Cells["A1"].PutValue("A");
dataSheet.Cells["A2"].PutValue("B");
dataSheet.Cells["A3"].PutValue("C");
```

Al igual que una receta depende de los ingredientes, la eficacia de su gráfico depende de la calidad y organización de los datos de entrada.

## Paso 4: Configurar una nueva hoja de cálculo de gráficos

Es hora de crear una nueva hoja de cálculo para el gráfico. Esto ayuda a mantener organizada la visualización de datos.

```csharp
Worksheet sheet = book.Worksheets.Add("MyChart");
```

Considere esta hoja de trabajo como su escenario, donde se desarrolla el rendimiento de sus datos.

## Paso 5: Agregar un gráfico

Aquí, agregaremos un gráfico de columnas a la hoja de trabajo recién creada.  

```csharp
ChartCollection charts = sheet.Charts;
int chartSheetIdx = charts.Add(ChartType.Column, 5, 0, 25, 15);
```

Estamos definiendo un espacio para nuestro gráfico y especificando de qué tipo es. Piense en ello como si estuviera seleccionando el tipo de marco para su obra de arte.

## Paso 6: Personalizar la apariencia del gráfico

Ahora, personalicemos la apariencia de nuestro gráfico configurando colores de fondo. 

```csharp
Aspose.Cells.Charts.Chart chart = book.Worksheets["MyChart"].Charts[0];
chart.PlotArea.Area.BackgroundColor = Color.White;
chart.ChartArea.Area.BackgroundColor = Color.White;
chart.PlotArea.Area.ForegroundColor = Color.White;
chart.ChartArea.Area.ForegroundColor = Color.White;
chart.ShowLegend = false;
```

Un fondo blanco limpio a menudo hace que los colores de sus datos se destaquen, mejorando la visibilidad.

## Paso 7: Agregar series de datos al gráfico

Es hora de introducir los datos en nuestro gráfico. Agregaremos una serie de datos de nuestra "Hoja de datos" para asegurarnos de que nuestro gráfico refleje los datos que necesitamos.

```csharp
chart.NSeries.Add("DataSheet!B1:B3", true);
chart.NSeries.CategoryData = "DataSheet!A1:A3";
```

Esto es similar a cuando un chef prepara un plato con ingredientes específicos. ¡Cada dato es importante!

## Paso 8: Acceder y dar formato a la serie de datos

Ahora que tenemos nuestros datos vinculados, tomemos la serie de datos y comencemos a aplicar algunos efectos 3D.

```csharp
Aspose.Cells.Charts.Series ser = chart.NSeries[0];
ShapePropertyCollection spPr = ser.ShapeProperties;
Format3D fmt3d = spPr.Format3D;
```

Nos estamos preparando para agregarle algo de estilo a nuestro plato; piense en ello como un condimento que realza el sabor general.

## Paso 9: Aplicar efectos de bisel 3D

A continuación, agregaremos un efecto de bisel para darle algo de dimensión a nuestro gráfico.

```csharp
Bevel bevel = fmt3d.TopBevel;
bevel.Type = BevelPresetType.Circle;
bevel.Height = 2;
bevel.Width = 5;
```

Al igual que un escultor da forma a una piedra, ¡estamos creando una profundidad que hace que nuestro gráfico cobre vida!

## Paso 10: Personaliza el material de la superficie y la iluminación

¡Hagamos que nuestro gráfico brille! Ajustaremos el material de la superficie y la configuración de la iluminación.

```csharp
fmt3d.SurfaceMaterialType = PresetMaterialType.WarmMatte;
fmt3d.SurfaceLightingType = LightRigType.ThreePoint;
fmt3d.LightingAngle = 20;
```

La iluminación y los materiales adecuados pueden transformar un objeto plano en una imagen cautivadora. Piense en un set de filmación con una iluminación experta para realzar cada escena.

## Paso 11: Toques finales en la apariencia de la serie

Ahora vamos a finalizar el aspecto de nuestra serie de datos ajustando su color.

```csharp
ser.Area.BackgroundColor = Color.Maroon;
ser.Area.ForegroundColor = Color.Maroon;
ser.Border.Color = Color.Maroon;
```

El color adecuado puede evocar determinados sentimientos y reacciones: el granate añade un toque de elegancia y sofisticación.

## Paso 12: Guarda tu libro de trabajo

¡Por fin ha llegado el momento de guardar tu obra maestra! No olvides especificar el destino en el que quieres guardarla.

```csharp
book.Save(outputDir + "outputApplying3DFormat.xlsx");
Console.WriteLine("Applying3DFormat executed successfully.");
```

Guardar tu trabajo es como poner tu arte en una galería; es un momento para apreciar y compartir.

## Conclusión

¡Felicitaciones! Ha creado con éxito un gráfico 3D visualmente atractivo con Aspose.Cells para .NET. Si sigue estos pasos, ahora tendrá una herramienta poderosa para mejorar sus presentaciones de datos, haciéndolas no solo informativas sino también visualmente atractivas. A medida que perfecciona sus gráficos, recuerde que cada visualización es una historia: ¡hágala atractiva, clara e impactante!

## Preguntas frecuentes

### ¿Qué es Aspose.Cells para .NET?
Aspose.Cells para .NET es una potente biblioteca que permite a los desarrolladores manipular documentos de Excel mediante programación, incluida la creación de gráficos y diagramas.

### ¿Puedo personalizar los tipos de gráficos en Aspose.Cells?
¡Sí! Aspose.Cells admite varios tipos de gráficos, como columnas, líneas, circulares y muchos más, que se pueden personalizar fácilmente.

### ¿Hay una prueba gratuita disponible para Aspose.Cells?
 ¡Por supuesto! Puedes descargar una versión de prueba gratuita desde[aquí](https://releases.aspose.com/).

### ¿Puedo aplicar otros efectos a los gráficos además de los formatos 3D?
Sí, puedes aplicar varios efectos como sombras, degradados y diferentes estilos para mejorar tus gráficos más allá del 3D.

### ¿Dónde puedo encontrar soporte para Aspose.Cells?
 Para obtener ayuda, puede visitar el sitio[Foro de Aspose](https://forum.aspose.com/c/cells/9) para asistencia y ayuda de la comunidad.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
