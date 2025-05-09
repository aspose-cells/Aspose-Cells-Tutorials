---
"date": "2025-04-05"
"description": "Aprenda a crear gráficos circulares dinámicos con líneas guía usando Aspose.Cells para .NET. Siga esta guía para mejorar sus habilidades de visualización de datos."
"title": "Creación de gráficos circulares con líneas guía en Aspose.Cells .NET&#58; una guía completa"
"url": "/es/net/charts-graphs/create-pie-charts-aspose-cells-net/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Creación de gráficos circulares con líneas guía mediante Aspose.Cells .NET

## Introducción
Mejore la visualización de sus datos creando gráficos circulares más informativos con Aspose.Cells para .NET. Esta guía paso a paso le muestra cómo agregar líneas guía a los segmentos de gráficos circulares, lo que facilita la identificación rápida de las categorías de datos correspondientes. Siguiendo este tutorial, sus visualizaciones serán visualmente atractivas y altamente funcionales.

**Lo que aprenderás:**
- Configuración de Aspose.Cells para .NET en su entorno
- Creación de gráficos circulares de líneas guía personalizados con C#
- Guardar el gráfico como imagen o dentro de un libro de Excel

Asegúrese de tener todo listo para seguir el proceso de manera efectiva.

## Prerrequisitos
Antes de comenzar, asegúrese de cumplir estos requisitos previos:

- **Bibliotecas y versiones**: Instale Aspose.Cells para .NET. Asegúrese de que su proyecto esté configurado con la última versión.
- **Configuración del entorno**:Esta guía asume un entorno .NET compatible con Aspose.Cells.
- **Requisitos previos de conocimiento**Es beneficioso tener familiaridad básica con la programación en C# y las operaciones de Excel.

## Configuración de Aspose.Cells para .NET
Para comenzar, instale Aspose.Cells en su proyecto a través de:

**CLI de .NET**
```bash
dotnet add package Aspose.Cells
```

**Administrador de paquetes**
```powershell
PM> NuGet\Install-Package Aspose.Cells
```

Obtenga una licencia para funcionalidad completa seleccionando entre las siguientes opciones:
- **Prueba gratuita**:Comienza tu prueba gratuita en [Página de descarga de Aspose](https://releases.aspose.com/cells/net/).
- **Licencia temporal**:Obtener una licencia temporal [aquí](https://purchase.aspose.com/temporary-license/).
- **Compra**:Para obtener todas las funciones, compre una licencia [aquí](https://purchase.aspose.com/buy).

Inicialice Aspose.Cells en su proyecto creando una instancia de `Workbook` clase.

## Guía de implementación

### Creación del libro de trabajo y la hoja de trabajo
1. **Inicializar el libro de trabajo**
   Crear un nuevo libro de trabajo en formato XLSX:
   ```csharp
   Workbook workbook = new Workbook(FileFormatType.Xlsx);
   ```

2. **Accediendo a la primera hoja de trabajo**
   Utilice la primera hoja de trabajo para ingresar datos:
   ```csharp
   Worksheet worksheet = workbook.Worksheets[0];
   ```

3. **Agregar datos para un gráfico circular**
   Llene su hoja de cálculo con categorías y valores:
   ```csharp
   worksheet.Cells["A1"].PutValue("Retail");
   // Añadir los nombres de categorías restantes...
   worksheet.Cells["B1"].PutValue(10.4);
   // Añade los valores correspondientes...
   ```

### Cómo agregar un gráfico circular a la hoja de trabajo
1. **Crear el gráfico circular**
   Genere un gráfico circular y agréguelo a la colección de gráficos de su hoja de trabajo:
   ```csharp
   int id = worksheet.Charts.Add(ChartType.Pie, 3, 3, 23, 13);
   ```

2. **Configurar datos de series y categorías**
   Vincula los datos de las series y categorías:
   ```csharp
   Chart chart = worksheet.Charts[id];
   chart.NSeries.Add("B1:B16", true);
   chart.NSeries.CategoryData = "A1:A16";
   ```

3. **Personalizar etiquetas de datos**
   Desactivar la visualización de leyendas, configurar las etiquetas de datos para mostrar los nombres de categorías y los porcentajes:
   ```csharp
   chart.ShowLegend = false;
   DataLabels dataLabels = chart.NSeries[0].DataLabels;
   dataLabels.ShowCategoryName = true;
   dataLabels.ShowPercentage = true;
   dataLabels.Position = LabelPositionType.OutsideEnd;
   ```

### Implementación de líneas guía
1. **Activar líneas guía**
   Habilite las líneas guía para obtener conexiones visuales más claras:
   ```csharp
   chart.NSeries[0].HasLeaderLines = true;
   ```

2. **Ajustar la posición de las etiquetas de datos**
   Garantice la visibilidad ajustando la posición de las etiquetas:
   ```csharp
   int DELTA = 100;
   foreach (var point in chart.NSeries[0].Points)
   {
       int X = point.DataLabels.X;
       if (X > 2000) 
           point.DataLabels.X += DELTA;
       else 
           point.DataLabels.X -= DELTA;
   }
   ```

### Guardar el gráfico y el libro de trabajo
1. **Guardar como imagen**
   Representar el gráfico en un archivo de imagen:
   ```csharp
   ImageOrPrintOptions options = new ImageOrPrintOptions { ImageType = Drawing.ImageType.Png, HorizontalResolution = 200, VerticalResolution = 200 };
   chart.ToImage("output_out.png", options);
   ```

2. **Guardar libro de trabajo**
   Guarde el libro de trabajo para ver el gráfico en Excel:
   ```csharp
   workbook.Save("output_out.xlsx");
   ```

## Aplicaciones prácticas
- **Informes financieros**:Representar claramente las asignaciones presupuestarias.
- **Análisis de marketing**:Visualice datos de participación de mercado de manera efectiva en presentaciones o informes.
- **Análisis de ventas**:Muestra la distribución de ventas entre diferentes regiones/productos con facilidad.

Las posibilidades de integración incluyen la exportación de estas visualizaciones a aplicaciones web o su integración en herramientas de informes automatizados.

## Consideraciones de rendimiento
Al utilizar Aspose.Cells, tenga en cuenta lo siguiente para obtener un rendimiento óptimo:
- Minimiza grandes conjuntos de datos cargados en la memoria a la vez.
- Utilice bucles eficientes y evite cálculos innecesarios dentro de los bucles.
- Limpie periódicamente los recursos, como los objetos del libro de trabajo, para evitar pérdidas de memoria.

## Conclusión
Aprendió a crear gráficos circulares con líneas guía usando Aspose.Cells para .NET. Esta funcionalidad mejora la claridad de sus visualizaciones de datos, haciéndolas más accesibles e impactantes. 

**Próximos pasos:**
Explore más personalizaciones en la apariencia de los gráficos o experimente con otros tipos de gráficos disponibles en Aspose.Cells.

## Sección de preguntas frecuentes
1. **¿Qué es una línea guía en un gráfico circular?**
   Las líneas guía conectan las etiquetas de datos con sus respectivos segmentos, mejorando la legibilidad.

2. **¿Puedo utilizar Aspose.Cells gratis?**
   Sí, puedes comenzar con una prueba gratuita, pero las funciones completas requieren una licencia.

3. **¿Es posible exportar gráficos como imágenes?**
   ¡Por supuesto! Usar `ImageOrPrintOptions` para guardar su gráfico en formatos de imagen como PNG o JPEG.

4. **¿Cómo ajusto manualmente las posiciones de las etiquetas de datos?**
   Modificar las coordenadas X e Y de las etiquetas de datos dentro del bucle de puntos de la serie.

5. **¿Puede Aspose.Cells integrarse con otros sistemas?**
   Sí, se puede utilizar junto con bases de datos, servicios web y más para soluciones de informes automatizados.

## Recursos
- [Documentación de Aspose.Cells](https://reference.aspose.com/cells/net/)
- [Descargar Aspose.Cells](https://releases.aspose.com/cells/net/)
- [Licencia de compra](https://purchase.aspose.com/buy)
- [Prueba gratuita](https://releases.aspose.com/cells/net/)
- [Licencia temporal](https://purchase.aspose.com/temporary-license/)
- [Foro de soporte](https://forum.aspose.com/c/cells/9)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}