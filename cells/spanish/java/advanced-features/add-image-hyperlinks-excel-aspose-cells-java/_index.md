---
date: '2026-09-02'
description: Aprenda cómo crear libros de Excel con imágenes clicables usando Aspose.Cells
  para Java, añadiendo hipervínculos a las imágenes para hojas de cálculo interactivas.
keywords:
- create clickable image
- add image hyperlink
- add hyperlink to picture
- interactive excel spreadsheet
- how to add hyperlink
lastmod: '2026-09-02'
og_description: Aprenda cómo crear libros de Excel con imágenes clicables usando Aspose.Cells
  para Java, añadiendo hipervínculos, descripciones emergentes y optimizando el rendimiento
  en solo unas pocas líneas de código.
og_image_alt: 'Developer guide: create clickable image Excel using Aspose.Cells for
  Java'
og_title: Crear imagen clicable en Excel con Aspose.Cells para Java
schemas:
- author: Aspose
  dateModified: '2026-09-02'
  description: Learn how to create clickable image Excel workbooks with Aspose.Cells
    for Java, adding hyperlinks to pictures for interactive spreadsheets.
  headline: Create clickable image Excel using Aspose.Cells for Java
  type: TechArticle
- description: Learn how to create clickable image Excel workbooks with Aspose.Cells
    for Java, adding hyperlinks to pictures for interactive spreadsheets.
  name: Create clickable image Excel using Aspose.Cells for Java
  steps:
  - name: prepare your workbook
    text: We start by creating a new workbook and selecting the first sheet.
  - name: insert a label and adjust cell size
    text: Add a descriptive label and give the cell enough space for the picture.
  - name: add the image
    text: '`Picture` represents an image object placed on a worksheet. *Tip*: Replace
      `"path/to/aspose-logo.jpg"` with the actual path to your image file.'
  - name: configure placement and add the hyperlink
    text: '`Hyperlink` defines a link associated with a cell, shape, or picture, enabling
      navigation when clicked.'
  - name: set a screen tip and save the workbook
    text: Provide a helpful tooltip and write the workbook to disk.
  type: HowTo
- questions:
  - answer: Aspose.Cells for Java.
    question: What library is required?
  - answer: Yes – the API works with both .xls and .xlsx.
    question: Can I use .xlsx files?
  - answer: A trial works for evaluation; a permanent license is required for production.
    question: Do I need a license?
  - answer: About 20 lines to add a clickable image.
    question: How many lines of code?
  - answer: Workbook objects are not thread‑safe; create separate instances per thread.
    question: Is it thread‑safe?
  type: FAQPage
tags:
- create clickable image
- Aspose.Cells
- Java Excel automation
title: Crear imagen clicable en Excel con Aspose.Cells para Java
url: /es/java/advanced-features/add-image-hyperlinks-excel-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear imagen de Excel clicable usando Aspose.Cells para Java

## Introducción

Si deseas **create clickable image Excel** libros de trabajo que permitan a los usuarios saltar a sitios web, documentos u otros recursos con un solo clic, estás en el lugar correcto. En este tutorial veremos cómo Aspose.Cells para Java te permite **add hyperlink Excel picture** objetos, configurar consejos de pantalla y mantener tus hojas de cálculo tanto hermosas como funcionales.

### Qué aprenderás
- Inicializar un libro de trabajo Aspose.Cells en Java.  
- Insertar una imagen y convertirla en un hipervínculo clicable.  
- Métodos clave como `addHyperlink`, `setPlacement` y `setScreenTip`.  
- Mejores prácticas para rendimiento y licenciamiento.

## Respuestas rápidas
- **¿Qué biblioteca se requiere?** Aspose.Cells for Java.  
- **¿Puedo usar archivos .xlsx?** Sí – la API funciona con .xls y .xlsx.  
- **¿Necesito una licencia?** Una prueba funciona para evaluación; se requiere una licencia permanente para producción.  
- **¿Cuántas líneas de código?** Aproximadamente 20 líneas para añadir una imagen clicable.  
- **¿Es seguro para subprocesos?** Los objetos Workbook no son seguros para subprocesos; crea instancias separadas por subproceso.  
- **¿Puedo añadir consejo de pantalla en Excel?** Sí – usa `Hyperlink.setScreenTip()` para mostrar texto útil al pasar el cursor.

## Cómo crear una imagen de Excel clicable con Aspose.Cells para Java

Creas un libro de trabajo de Excel con imagen clicable cargando o creando un `Workbook`, insertando un objeto `Picture`, adjuntando un `Hyperlink` a esa imagen, opcionalmente estableciendo un consejo de pantalla y finalmente guardando el archivo. La API maneja todo el XML de Excel de bajo nivel, por lo que solo escribes unas pocas líneas sencillas de código Java.

### Requisitos previos
- **Aspose.Cells for Java** (v25.3 o posterior).  
- **JDK 8+** instalado.  
- Un IDE (IntelliJ IDEA, Eclipse o NetBeans) y Maven o Gradle para la gestión de dependencias.  

### Bibliotecas requeridas
Add Aspose.Cells to your project:

**Maven**  
```xml
<dependency>
  <groupId>com.aspose</groupId>
  <artifactId>aspose-cells</artifactId>
  <version>25.3</version>
</dependency>
```  

**Gradle**  
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```  

### Obtención de licencia
Aspose.Cells es comercial, pero puedes comenzar con una prueba gratuita o solicitar una licencia temporal:

- Prueba gratuita: Descarga desde [Aspose Downloads](https://releases.aspose.com/cells/java/).  
- Licencia temporal: Solicita a través de la [Temporary License page](https://purchase.aspose.com/temporary-license/).  
- Compra: Para uso a largo plazo, visita [Aspose Purchase](https://purchase.aspose.com/buy).

### Inicialización básica
La clase `Workbook` representa un archivo Excel completo en memoria. La instancias y luego obtienes una referencia a la primera hoja de cálculo. `Worksheet` representa una hoja única dentro del libro.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

// Initialize workbook
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```  

## Implementación paso a paso

### Paso 1: prepara tu libro de trabajo
Comenzamos creando un nuevo libro de trabajo y seleccionando la primera hoja.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```  

### Paso 2: inserta una etiqueta y ajusta el tamaño de la celda
Añade una etiqueta descriptiva y da a la celda suficiente espacio para la imagen.

```java
worksheet.getCells().get("C2").setValue("Image Hyperlink");
worksheet.getCells().setRowHeight(3, 100); // Set row height for C4
worksheet.getCells().setColumnWidth(2, 21); // Adjust column width for C column
```  

### Paso 3: añade la imagen
`Picture` representa un objeto de imagen colocado en una hoja de cálculo.

```java
int index = worksheet.getPictures().add(3, 2, "path/to/aspose-logo.jpg");
```  
*Consejo*: Reemplaza `"path/to/aspose-logo.jpg"` con la ruta real a tu archivo de imagen.

### Paso 4: configura la ubicación y añade el hipervínculo
`Hyperlink` define un enlace asociado a una celda, forma o imagen, habilitando la navegación al hacer clic.

```java
import com.aspose.cells.Picture;
import com.aspose.cells.PlacementType;

Picture pic = worksheet.getPictures().get(index);
pic.setPlacement(PlacementType.FREE_FLOATING);

// Add hyperlink to the picture
pic.addHyperlink("http://www.aspose.com/");
```  

### Paso 5: establece un consejo de pantalla y guarda el libro de trabajo
Proporciona una información sobre herramientas útil y escribe el libro de trabajo en disco.

```java
import com.aspose.cells.Hyperlink;

Hyperlink hlink = pic.getHyperlink();
hlink.setScreenTip("Click to go to Aspose site");

workbook.save("AIHyperlinks_out.xls");
```  

## ¿Por qué añadir una imagen de Excel con hipervínculo?

Insertar una imagen clicable permite convertir elementos de marca, íconos o diagramas en puntos de navegación directos, reduciendo la cantidad de clics necesarios para llegar al contenido relacionado. Este enfoque mejora la eficiencia del usuario en paneles de marketing, manuales técnicos y hojas de cálculo educativas.

## Cómo añadir un consejo de pantalla en Excel

Se añade un consejo de pantalla llamando a `hyperlink.setScreenTip("Your tip here")` en el objeto `Hyperlink` adjunto a la imagen. El consejo aparece cuando el cursor pasa sobre la imagen, proporcionando a los usuarios una guía contextual sin saturar la hoja.

## Consejos de solución de problemas
- **Errores de ruta de imagen** – verifica la ubicación del archivo y asegura que la aplicación tenga permisos de lectura.  
- **Licencia no aplicada** – si la prueba expira, los hipervínculos pueden dejar de funcionar; aplica una licencia válida con `License.setLicense`.  
- **Hipervínculo no clicable** – verifica que el `PlacementType` de la imagen esté configurado como `FREE_FLOATING`.

## Aplicaciones prácticas
Insertar imágenes clicables es útil en muchos escenarios:

1. **Informes de marketing** – enlaza logotipos de marca a páginas de productos.  
2. **Documentación técnica** – adjunta diagramas que abren esquemas detallados.  
3. **Hojas de trabajo educativas** – convierte íconos en accesos directos a videos complementarios.  
4. **Paneles de proyecto** – haz que los íconos de estado abran los rastreadores de tareas relacionados.

## Consideraciones de rendimiento
- Mantén los tamaños de archivo de imagen razonables; las imágenes grandes aumentan el uso de memoria del libro.  
- Elimina objetos no usados (`workbook.dispose()`) al procesar muchos archivos en un bucle.  
- Actualiza a la última versión de Aspose.Cells para mejoras de rendimiento y corrección de errores.

## Conclusión
Ahora sabes cómo añadir un hipervínculo a imágenes en Excel usando Aspose.Cells para Java, lo que te permite **create clickable image Excel** libros de trabajo más ricos e interactivos. Experimenta con diferentes URL, consejos de pantalla y ubicaciones de imágenes para adaptarlos a tus necesidades de informes. A continuación, podrías explorar añadir hipervínculos a formas o automatizar la inserción masiva de imágenes en múltiples hojas.

## Preguntas frecuentes

**Q:** ¿Cuál es el tamaño máximo de imagen soportado por Aspose.Cells para Java?  
**A:** No hay un límite estricto, pero imágenes muy grandes pueden afectar el rendimiento y aumentar el tamaño del archivo.

**Q:** ¿Puedo usar esta función con archivos .xlsx?  
**A:** Sí, la API funciona con los formatos `.xls` y `.xlsx`.

**Q:** ¿Cómo debo manejar excepciones al añadir hipervínculos?  
**A:** Envuelve el código en un bloque try‑catch y registra los detalles de `Exception` para diagnosticar problemas de ruta o licencia.

**Q:** ¿Es posible eliminar un hipervínculo de una imagen después de haberlo añadido?  
**A:** Sí – recupera el objeto `Picture` y llama a `pic.getHyperlink().remove()` o elimina la imagen de la colección.

**Q:** ¿Por qué mi hipervínculo podría no funcionar como se espera?  
**A:** Las causas comunes incluyen una cadena URL incorrecta, falta del prefijo `http://`/`https://`, o una prueba sin licencia que desactiva ciertas funciones.

## Recursos adicionales
- **Documentation:** [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
- **Download:** [Aspose Cells Release](https://releases.aspose.com/cells/java/)  
- **Purchase and trial:** Visita [Aspose Purchase](https://purchase.aspose.com/buy) o [Temporary License Page](https://purchase.aspose.com/temporary-license/) para opciones de licenciamiento.  
- **Support forum:** Para asistencia, consulta el [Aspose Support Forum](https://forum.aspose.com/c/cells/9).

---

**Last updated:** 2026-09-02  
**Tested with:** Aspose.Cells for Java 25.3  
**Author:** Aspose

## Tutoriales relacionados

- [How to Create Hyperlinks in Excel Using Aspose.Cells for Java - A Step‑By‑Step Guide](/cells/java/advanced-features/create-hyperlinks-excel-aspose-cells-java/)
- [How to Style Excel Cells and Add Hyperlinks Using Aspose.Cells for Java](/cells/java/formatting/style-excel-cells-hyperlinks-aspose-cells-java/)
- [Add Image to Excel Comment with Aspose.Cells for Java: A Complete Guide](/cells/java/comments-annotations/add-image-excel-comment-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}