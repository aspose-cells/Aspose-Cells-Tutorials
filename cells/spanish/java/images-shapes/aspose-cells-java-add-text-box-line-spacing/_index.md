---
"date": "2025-04-08"
"description": "Aprenda a usar Aspose.Cells para Java para agregar cuadros de texto y configurar el interlineado en libros de Excel. Mejore las presentaciones de sus libros con formas de texto con estilo."
"title": "Agregar cuadro de texto y establecer interlineado en Excel con Aspose.Cells para Java"
"url": "/es/java/images-shapes/aspose-cells-java-add-text-box-line-spacing/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Agregar un cuadro de texto y establecer el interlineado en Excel usando Aspose.Cells para Java

## Introducción

Crear informes dinámicos de Excel suele requerir un formato de texto personalizado, como añadir cuadros de texto con un interlineado específico. Con Aspose.Cells para Java, esto se vuelve sencillo y eficiente. Este tutorial le guiará para mejorar las presentaciones de su libro de trabajo con Aspose.Cells para Java y añadir formas de texto con estilo.

Al final de esta guía, aprenderá a:
- Cree un nuevo libro de Excel y acceda a sus hojas de cálculo
- Agregar una forma de cuadro de texto a una hoja de cálculo
- Establecer un interlineado personalizado dentro de una forma de texto
- Guarde su libro de trabajo formateado en formato XLSX

Comencemos configurando su entorno.

### Prerrequisitos

Antes de comenzar, asegúrese de tener lo siguiente:
- Kit de desarrollo de Java (JDK) instalado en su máquina
- Un IDE o editor para escribir código Java
- Sistema de compilación Maven o Gradle configurado para administrar dependencias

Será beneficioso tener conocimientos básicos de programación Java y estar familiarizado con las estructuras de archivos de Excel.

## Configuración de Aspose.Cells para Java

Incluya Aspose.Cells en la gestión de dependencias de su proyecto usando Maven o Gradle:

**Experto**

Agregue el siguiente bloque de dependencia a su `pom.xml` archivo:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle**

Incluye esto en tu `build.gradle` archivo:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

A continuación, adquiera una licencia para Aspose.Cells optando por una prueba gratuita, solicitando una licencia temporal o comprando una licencia completa.

### Inicializando Aspose.Cells

Una vez que la biblioteca esté incluida en su proyecto, inicialícela dentro de su aplicación Java:

```java
import com.aspose.cells.Workbook;

public class ExcelDemo {
    public static void main(String[] args) {
        // Inicializar una instancia de Workbook (representa un archivo de Excel)
        Workbook workbook = new Workbook();
        
        System.out.println("Aspose.Cells for Java initialized successfully.");
    }
}
```

## Guía de implementación

### Crear un libro de trabajo y acceder a una hoja de trabajo

Empieza creando un nuevo libro de Excel y accediendo a su primera hoja. Aquí es donde agregarás el cuadro de texto.

#### Descripción general

La creación de un nuevo libro de trabajo proporciona un espacio vacío para agregar datos, formas y formato según sea necesario.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

public class ExcelDemo {
    public static void main(String[] args) {
        // Crear un nuevo libro de trabajo (archivo de Excel)
        Workbook workbook = new Workbook();
        
        // Acceda a la primera hoja de trabajo
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        System.out.println("Workbook and first worksheet accessed.");
    }
}
```

### Agregar cuadro de texto a la hoja de trabajo

A continuación, añade un cuadro de texto a la hoja de cálculo seleccionada. Este cuadro puede contener cualquier texto que necesites.

#### Descripción general

Los cuadros de texto son herramientas versátiles para incluir textos personalizados, como notas o instrucciones, directamente dentro de una hoja de Excel.

```java
import com.aspose.cells.Shape;
import com.aspose.cells.MsoDrawingType;

public class ExcelDemo {
    public static void main(String[] args) {
        // Crear un nuevo libro de trabajo (archivo de Excel)
        Workbook workbook = new Workbook();
        
        // Acceda a la primera hoja de trabajo
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Agregar una forma de cuadro de texto a la hoja de cálculo
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        System.out.println("Text box added.");
    }
}
```

### Establecer texto en forma

Una vez que su cuadro de texto esté listo, configure su contenido y formatee el texto dentro de él.

```java
import com.aspose.cells.Shape;

public class ExcelDemo {
    public static void main(String[] args) {
        // Crear un nuevo libro de trabajo (archivo de Excel)
        Workbook workbook = new Workbook();
        
        // Acceda a la primera hoja de trabajo
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Agregar una forma de cuadro de texto a la hoja de cálculo
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // Establecer el contenido del texto dentro de la forma
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        System.out.println("Text set in shape.");
    }
}
```

### Acceder a párrafos de texto en Shape

Puede acceder a párrafos individuales dentro de un cuadro de texto para aplicar un formato específico.

```java
import com.aspose.cells.TextParagraph;

public class ExcelDemo {
    public static void main(String[] args) {
        // Crear un nuevo libro de trabajo (archivo de Excel)
        Workbook workbook = new Workbook();
        
        // Acceda a la primera hoja de trabajo
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Agregar una forma de cuadro de texto a la hoja de cálculo
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // Establecer el contenido del texto dentro de la forma
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        // Accede al segundo párrafo de la forma
        TextParagraph paragraph = textBox.getTextBody().getTextParagraphs().get(1);
        
        System.out.println("Accessed second paragraph in text box.");
    }
}
```

### Establecer el espaciado entre líneas del párrafo

Personalizar el interlineado puede mejorar la legibilidad. Aquí te explicamos cómo configurarlo:

```java
import com.aspose.cells.LineSpaceSizeType;

public class ExcelDemo {
    public static void main(String[] args) throws Exception {
        // Crear un nuevo libro de trabajo (archivo de Excel)
        Workbook workbook = new Workbook();
        
        // Acceda a la primera hoja de trabajo
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Agregar una forma de cuadro de texto a la hoja de cálculo
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // Establecer el contenido del texto dentro de la forma
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        // Accede al segundo párrafo de la forma
        TextParagraph paragraph = textBox.getTextBody().getTextParagraphs().get(1);

        // Establezca el interlineado en 20 puntos
        paragraph.setLineSpaceSizeType(LineSpaceSizeType.POINTS);
        paragraph.setLineSpace(20); 
        
        // Configurar el espacio antes y después del párrafo
        paragraph.setSpaceAfterSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceAfter(10);
        
        paragraph.setSpaceBeforeSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceBefore(10);

        System.out.println("Line spacing set.");
    }
}
```

### Guardar libro de trabajo

Por último, guarde su libro de trabajo con el cuadro de texto recién agregado y formateado.

```java
import com.aspose.cells.SaveFormat;

public class ExcelDemo {
    public static void main(String[] args) throws Exception {
        // Crear un nuevo libro de trabajo (archivo de Excel)
        Workbook workbook = new Workbook();
        
        // Acceda a la primera hoja de trabajo
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Agregar una forma de cuadro de texto a la hoja de cálculo
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // Establecer el contenido del texto dentro de la forma
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        // Accede al segundo párrafo de la forma
        TextParagraph paragraph = textBox.getTextBody().getTextParagraphs().get(1);

        // Establezca el interlineado en 20 puntos
        paragraph.setLineSpaceSizeType(LineSpaceSizeType.POINTS);
        paragraph.setLineSpace(20); 
        
        // Configurar el espacio antes y después del párrafo
        paragraph.setSpaceAfterSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceAfter(10);
        
        paragraph.setSpaceBeforeSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceBefore(10);

        // Guardar el libro de trabajo
        workbook.save("StyledTextShape.xlsx", SaveFormat.XLSX);
    }
}
```

## Conclusión

Has aprendido a agregar un cuadro de texto y a configurar el interlineado en un libro de Excel con Aspose.Cells para Java. Esto mejora tu capacidad para crear informes dinámicos y visualmente atractivos.

## Recomendaciones de palabras clave
- Aspose.Cells para Java
- "Agregar cuadro de texto en Excel"
- "Establecer el interlineado en Excel"
- Libro de Excel con texto con estilo
- Java y Aspose.Cells


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}