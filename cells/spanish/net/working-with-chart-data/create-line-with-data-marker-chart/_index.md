---
title: Crear gráfico de línea con marcador de datos
linktitle: Crear gráfico de línea con marcador de datos
second_title: API de procesamiento de Excel Aspose.Cells .NET
description: Aprenda a crear un gráfico de líneas con marcadores de datos en Excel con Aspose.Cells para .NET. Siga esta guía paso a paso para generar y personalizar gráficos fácilmente.
weight: 10
url: /es/net/working-with-chart-data/create-line-with-data-marker-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear gráfico de línea con marcador de datos

## Introducción

¿Alguna vez te preguntaste cómo crear gráficos impresionantes en Excel mediante programación? Abróchate el cinturón, porque hoy vamos a sumergirnos en la creación de un gráfico de línea con marcador de datos usando Aspose.Cells para .NET. Este tutorial te guiará a través de cada paso, asegurándote de que tienes un conocimiento sólido de la generación de gráficos, incluso si recién estás comenzando con Aspose.Cells.

## Prerrequisitos

Antes de comenzar, asegúrese de tener todo en su lugar para seguir el proceso sin problemas.

1. Biblioteca Aspose.Cells para .NET: deberá instalarla. Puede descargarla[aquí](https://releases.aspose.com/cells/net/).
2. .NET Framework: asegúrese de que su entorno de desarrollo esté configurado con la última versión de .NET.
3. IDE (Entorno de desarrollo integrado): se recomienda Visual Studio.
4.  Una licencia válida de Aspose.Cells: si no tiene una, puede solicitar una[licencia temporal](https://purchase.aspose.com/temporary-license/) o echa un vistazo a sus[prueba gratis](https://releases.aspose.com/).

¿Listo para empezar? ¡Vamos a desglosarlo!

## Importación de paquetes necesarios

Para comenzar, asegúrese de importar los siguientes espacios de nombres a su proyecto. Estos le proporcionarán las clases y los métodos necesarios para crear su gráfico.

```csharp
using System;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Charts;
using System.Drawing;
```

¡Una vez que tengas eso claro, podemos empezar a codificar!

## Paso 1: Configura tu libro de trabajo y tu hoja de trabajo

Lo primero es lo primero: debes crear un nuevo libro de trabajo y acceder a la primera hoja de trabajo.

```csharp
//Directorio de salida
static string outputDir = "Your Document Directory";
		
// Crear una instancia de un libro de trabajo
Workbook workbook = new Workbook();

// Acceda a la primera hoja de trabajo
Worksheet worksheet = workbook.Worksheets[0];
```

Piense en el libro de trabajo como su archivo de Excel y en la hoja de trabajo como la hoja específica dentro de él. En este caso, estamos trabajando con la primera hoja.

## Paso 2: Rellene la hoja de cálculo con datos

Ahora que tenemos nuestra hoja de cálculo, llenémosla con algunos datos. Crearemos puntos de datos aleatorios para dos series de valores.

```csharp
// Establecer el título de las columnas
worksheet.Cells[0, 0].Value = "X";
worksheet.Cells[0, 1].Value = "Y";

// Datos aleatorios para generar el gráfico
Random R = new Random();

// Crea datos aleatorios y guárdalos en las celdas
for (int i = 1; i < 21; i++)
{
    worksheet.Cells[i, 0].Value = i;
    worksheet.Cells[i, 1].Value = 0.8;
}

for (int i = 21; i < 41; i++)
{
    worksheet.Cells[i, 0].Value = i - 20;
    worksheet.Cells[i, 1].Value = 0.9;
}
```

Aquí usamos números aleatorios para simular datos, pero en aplicaciones de la vida real puedes completarlos con valores reales de tu conjunto de datos.

## Paso 3: Agregue el gráfico a la hoja de trabajo

A continuación, agregamos el gráfico a la hoja de cálculo y elegimos el tipo: en este caso, un gráfico de líneas con marcadores de datos.

```csharp
// Agregar un gráfico a la hoja de trabajo
int idx = worksheet.Charts.Add(ChartType.LineWithDataMarkers, 1, 3, 20, 20);

// Acceda al gráfico recién creado
Chart chart = worksheet.Charts[idx];
```

Este fragmento agrega un gráfico de líneas con marcadores de datos a la hoja de cálculo y los coloca en un rango específico (1,3 a 20,20). Bastante simple, ¿verdad?

## Paso 4: Personaliza la apariencia del gráfico

Una vez creado el gráfico, puedes darle el estilo que desees. Vamos a cambiar el fondo, el título y el estilo del gráfico.

```csharp
// Establecer el estilo del gráfico
chart.Style = 3;

// Establezca el valor de escalamiento automático en verdadero
chart.AutoScaling = true;

// Establecer el color de primer plano en blanco
chart.PlotArea.Area.ForegroundColor = Color.White;

//Establecer las propiedades del título del gráfico
chart.Title.Text = "Sample Chart";

// Establecer el tipo de gráfico
chart.Type = ChartType.LineWithDataMarkers;
```

Aquí, le damos al gráfico un aspecto limpio estableciendo un fondo blanco, escalando automáticamente y dándole un título significativo.

## Paso 5: Definir series y graficar puntos de datos

Ahora que nuestro gráfico se ve bien, necesitamos definir la serie de datos que se trazarán.

```csharp
// Establecer propiedades del título del eje de categorías
chart.CategoryAxis.Title.Text = "Units";

// Definir dos series para el gráfico
int s2_idx = chart.NSeries.Add("A2: A21", true);
int s3_idx = chart.NSeries.Add("A22: A41", true);
```

Estas series corresponden a los rangos de puntos de datos que completamos anteriormente.

## Paso 6: Agregar colores y personalizar los marcadores de serie

Hagamos este gráfico aún más atractivo agregando colores personalizados a nuestros marcadores de datos.

```csharp
// Personaliza la primera serie
chart.NSeries[s2_idx].Marker.Area.ForegroundColor = Color.Yellow;
chart.NSeries[s2_idx].Marker.Border.IsVisible = false;

// Personalizar la segunda serie
chart.NSeries[s3_idx].Marker.Area.ForegroundColor = Color.Green;
chart.NSeries[s3_idx].Marker.Border.IsVisible = false;
```

¡Al personalizar los colores, el gráfico no solo es funcional sino también visualmente atractivo!

## Paso 7: Establezca los valores X e Y para cada serie

Por último, asignemos los valores X e Y para cada una de nuestras series.

```csharp
// Establecer los valores X e Y de la primera serie
chart.NSeries[s2_idx].XValues = "A2: A21";
chart.NSeries[s2_idx].Values = "B2: B21";

// Establecer los valores X e Y de la segunda serie
chart.NSeries[s3_idx].XValues = "A22: A41";
chart.NSeries[s3_idx].Values = "B22: B41";
```

Los valores se basan en los datos que completamos en el paso 2.

## Paso 8: Guardar el libro de trabajo

Ahora que todo está configurado, guardemos el libro de trabajo para que podamos ver el gráfico en acción.

```csharp
// Guardar el libro de trabajo
workbook.Save(outputDir + @"LineWithDataMarkerChart.xlsx", Aspose.Cells.SaveFormat.Xlsx);
```

¡Y eso es todo! Acabas de crear un gráfico de líneas con marcadores de datos utilizando Aspose.Cells para .NET.

## Conclusión

Crear gráficos de forma programada en Excel puede parecer una tarea abrumadora, pero con Aspose.Cells para .NET, es tan fácil como seguir una receta paso a paso. Desde la configuración de su libro de trabajo hasta la personalización de la apariencia del gráfico, esta potente biblioteca se encarga de todo. Ya sea que esté creando informes, paneles o visualizaciones de datos, Aspose.Cells le permite hacerlo en un abrir y cerrar de ojos.

## Preguntas frecuentes

### ¿Puedo personalizar aún más el gráfico?  
¡Por supuesto! Aspose.Cells ofrece un montón de opciones de personalización, desde fuentes hasta cuadrículas y más.

### ¿Necesito una licencia para utilizar Aspose.Cells?  
 Sí, se requiere una licencia para la funcionalidad completa. Puede obtener una[licencia temporal](https://purchase.aspose.com/temporary-license/) o empezar con un[prueba gratis](https://releases.aspose.com/).

### ¿Cómo puedo agregar más series de datos?  
 Simplemente agregue series adicionales usando el`NSeries.Add` método, especificando los rangos de celdas para los nuevos datos.

### ¿Puedo exportar el gráfico como imagen?  
 Sí, puedes exportar gráficos directamente como imágenes usando el`Chart.ToImage` método.

### ¿Aspose.Cells admite gráficos 3D?  
Sí, Aspose.Cells admite una amplia gama de tipos de gráficos, incluidos gráficos 3D.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
