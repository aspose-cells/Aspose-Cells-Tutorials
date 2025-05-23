---
"description": "Aprenda a crear un gráfico circular en Excel con Aspose.Cells para .NET con esta guía paso a paso. Visualice sus datos fácilmente."
"linktitle": "Crear un gráfico circular"
"second_title": "API de procesamiento de Excel Aspose.Cells .NET"
"title": "Crear un gráfico circular"
"url": "/es/net/manipulating-chart-types/create-pie-chart/"
"weight": 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Crear un gráfico circular

## Introducción

Crear gráficos es esencial para representar visualmente los datos, y los gráficos circulares son una de las formas más populares de ilustrar cómo las partes conforman un todo. Con Aspose.Cells para .NET, puede automatizar fácilmente la generación de gráficos circulares en archivos de Excel. En este tutorial, profundizaremos en cómo crear un gráfico circular desde cero con Aspose.Cells para .NET, con una guía paso a paso para que el proceso sea sencillo y directo. Tanto si es nuevo en la herramienta como si busca mejorar sus habilidades de automatización de Excel, ¡esta guía lo tiene todo cubierto!

## Prerrequisitos

Antes de sumergirse en el código, asegúrese de tener la siguiente configuración:

1. Biblioteca Aspose.Cells para .NET: Asegúrate de tener Aspose.Cells instalado en tu proyecto. Si aún no lo has instalado, puedes descargarlo desde [aquí](https://releases.aspose.com/cells/net/).
2. Entorno de desarrollo .NET: asegúrese de que su proyecto esté configurado para usar .NET Framework o .NET Core.
3. Conocimientos básicos de C#: Debe sentirse cómodo con la programación en C#, especialmente con la programación orientada a objetos (OOP).

Los usuarios avanzados pueden solicitar una licencia temporal para desbloquear todas las funciones de Aspose.Cells. Pueden solicitarla en [aquí](https://purchase.aspose.com/temporary-license/).

## Importar paquetes

Para comenzar, importe los espacios de nombres y paquetes necesarios para este tutorial. Estos incluyen operaciones básicas de E/S y el paquete Aspose.Cells.

```csharp
using System;
using System.IO;

using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
using Aspose.Cells.Charts;
```

## Paso 1: Crear un nuevo libro de trabajo

Primero, necesitamos crear una instancia del `Workbook` Clase, que representa el archivo de Excel. Un libro contiene varias hojas, y en nuestro ejemplo, trabajaremos con dos: una para los datos y otra para el gráfico circular.

```csharp
Workbook workbook = new Workbook();
```

Esto inicializa un nuevo libro de Excel. Pero ¿dónde se almacenan los datos? Lo explicaremos en el siguiente paso.

## Paso 2: Agregar datos a la hoja de trabajo

Una vez creado el libro, debemos acceder a la primera hoja de cálculo y asignarle un nombre. Aquí ingresaremos los datos necesarios para el gráfico circular.

```csharp
Worksheet sheet = workbook.Worksheets[0];
sheet.Name = "Data";
Cells cells = sheet.Cells;
```

Ahora, podemos ingresar algunos datos de ventas ficticios que representen diferentes regiones:

```csharp
cells["A1"].PutValue("Region");
cells["A2"].PutValue("France");
cells["A3"].PutValue("Germany");
cells["A4"].PutValue("England");
cells["A5"].PutValue("Sweden");
cells["A6"].PutValue("Italy");
cells["A7"].PutValue("Spain");
cells["A8"].PutValue("Portugal");

cells["B1"].PutValue("Sales");
cells["B2"].PutValue(70000);
cells["B3"].PutValue(55000);
cells["B4"].PutValue(30000);
cells["B5"].PutValue(40000);
cells["B6"].PutValue(35000);
cells["B7"].PutValue(32000);
cells["B8"].PutValue(10000);
```

Aquí, añadimos dos columnas: una para las regiones y otra para las cifras de ventas. Estos datos se representarán en el gráfico circular.

## Paso 3: Agregar una hoja de gráficos

A continuación, agreguemos una hoja de trabajo separada para contener el gráfico circular.

```csharp
int sheetIndex = workbook.Worksheets.Add(SheetType.Chart);
Worksheet chartSheet = workbook.Worksheets[sheetIndex];
chartSheet.Name = "Chart";
```

Esta nueva hoja albergará el gráfico circular. Al asignarle un nombre como "Gráfico", se garantiza que los usuarios sepan qué esperar al abrir el archivo.

## Paso 4: Crea el gráfico circular

Ahora es el momento de crear el gráfico. Especificaremos que queremos un gráfico circular y definiremos su posición en la hoja.

```csharp
int chartIndex = chartSheet.Charts.Add(Aspose.Cells.Charts.ChartType.Pie, 5, 0, 25, 10);
Aspose.Cells.Charts.Chart chart = chartSheet.Charts[chartIndex];
```

El método `Add()` acepta parámetros para el tipo de gráfico (en este caso, `ChartType.Pie`) y su ubicación en la hoja de cálculo. Los números representan las posiciones de fila y columna.

## Paso 5: Personaliza la apariencia del gráfico

¡Un gráfico circular no estaría completo sin algo de personalización! Hagamos que nuestro gráfico sea visualmente atractivo modificando los colores, las etiquetas y el título.

### Establecer título del gráfico
```csharp
chart.Title.Text = "Sales By Region";
chart.Title.Font.Color = Color.Blue;
chart.Title.Font.IsBold = true;
chart.Title.Font.Size = 12;
```

### Personalizar el área de la parcela
```csharp
chart.PlotArea.Area.ForegroundColor = Color.Coral;
chart.PlotArea.Area.FillFormat.SetTwoColorGradient(Color.Yellow, Color.White, GradientStyleType.Vertical, 2);
chart.PlotArea.Border.IsVisible = false;
```

Establecemos el relleno degradado para el área del gráfico y ocultamos el borde para una apariencia más limpia.

## Paso 6: Definir los datos del gráfico

Es hora de vincular el gráfico con nuestros datos. `NSeries` La propiedad del gráfico vincula las cifras de ventas y regiones al gráfico circular.

```csharp
chart.NSeries.Add("Data!B2:B8", true);
chart.NSeries.CategoryData = "Data!A2:A8";
chart.NSeries.IsColorVaried = true;
```

La primera línea especifica que estamos utilizando los datos de ventas de las celdas. `B2:B8`También le indicamos al gráfico que utilice los nombres de las regiones de `A2:A8` como etiquetas de categoría.

## Paso 7: Agregar etiquetas de datos

Agregar etiquetas directamente a los segmentos del gráfico facilita su comprensión. Incluyamos los nombres de las regiones y los valores de ventas dentro de los segmentos del gráfico circular.

```csharp
for (int i = 0; i < chart.NSeries.Count; i++)
{
    DataLabels labels = chart.NSeries[i].DataLabels;
    labels.ShowCategoryName = true;
    labels.ShowValue = true;
    labels.Position = LabelPositionType.InsideBase;
}
```

## Paso 8: Personalizar el área del gráfico y la leyenda

Por último, demos los toques finales al área del gráfico y a la leyenda. Esto mejora la presentación general del gráfico.

### Área del gráfico
```csharp
ChartArea chartArea = chart.ChartArea;
chartArea.Area.Formatting = FormattingType.Custom;
chartArea.Area.FillFormat.Texture = TextureType.BlueTissuePaper;
```

### Leyenda
```csharp
Legend legend = chart.Legend;
legend.Position = LegendPositionType.Left;
legend.Font.IsBold = true;
legend.Border.Color = Color.Blue;
legend.Area.FillFormat.Texture = TextureType.Bouquet;
```

## Paso 9: Guardar el libro de trabajo

Finalmente, guardamos el libro en un archivo de Excel. Puede especificar el directorio de salida y el nombre del archivo según sea necesario.

```csharp
workbook.Save(outputDir + "outputHowToCreatePieChart.xlsx");
```

## Conclusión

Crear un gráfico circular con Aspose.Cells para .NET es un proceso sencillo y personalizable. Siguiendo esta guía, podrá generar un gráfico de aspecto profesional que transmita información valiosa en tan solo unos pasos. Ya sea para informes empresariales o con fines educativos, dominar la creación de gráficos mejorará sus habilidades de automatización de Excel. Recuerde que Aspose.Cells le ofrece la flexibilidad necesaria para crear archivos de Excel impactantes y basados en datos sin esfuerzo.

## Preguntas frecuentes

### ¿Puedo crear otros tipos de gráficos utilizando Aspose.Cells para .NET?
¡Sí! Aspose.Cells admite varios tipos de gráficos, como gráficos de barras, gráficos de líneas y diagramas de dispersión.

### ¿Necesito una licencia paga para usar Aspose.Cells para .NET?
Puedes usar la versión gratuita con algunas limitaciones. Para disfrutar de todas las funciones, necesitas una licencia, que puedes comprar. [aquí](https://purchase.aspose.com/buy).

### ¿Puedo exportar el gráfico a formatos como PDF o imágenes?
¡Por supuesto! Aspose.Cells te permite exportar gráficos a varios formatos, incluidos PDF y PNG.

### ¿Es posible darle estilo a cada porción de pastel con diferentes colores?
Sí, puedes aplicar diferentes colores a cada rebanada configurando el `IsColorVaried` propiedad a `true`, como se muestra en el tutorial.

### ¿Puedo automatizar la generación de múltiples gráficos en un solo libro de trabajo?
Sí, puedes crear y personalizar tantos gráficos como necesites dentro de un solo archivo de Excel.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}