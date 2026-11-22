# Software FJ · Gestión de clientes, servicios y reservas

Proyecto individual de consola para la Fase 4 de Programación (UNAD). Requiere Python 3.9 o posterior y utiliza exclusivamente la biblioteca estándar.

## Ejecutar en Visual Studio

1. Descomprima el proyecto en una carpeta con permiso de escritura.
2. Con la carga de trabajo de desarrollo de Python instalada, abra la carpeta SoftwareFJ en Visual Studio y seleccione su intérprete Python 3.
3. Desde la terminal de esa carpeta ejecute `python main.py`. En Windows también puede usar `py main.py`. Para ejecutar desde el IDE, establezca main.py como archivo de inicio.
4. Para reproducir los 19 casos y ver el conteo final, elija 6 o ejecute `python main.py --demo`. La demostración utiliza su propio catálogo.

## Operación manual

Registre un cliente C1 y un servicio S1 de tipo sala con tarifa 20000. Cree la reserva R1 para C1 y S1 por 2 horas, con 10 % de descuento y 19 % de impuesto. El total debe ser 42840.00 COP. Confirme R1 y luego procésela. Consulte los registros con la opción 5. Al cerrar, los datos de la sesión se descartan. El archivo software_fj.log conserva eventos, errores y sus trazas.

## Diseño y criterios adoptados

- modelos.py define Entidad y Servicio como clases abstractas. Cliente encapsula nombre, correo y código. Sala, Equipo y Asesoria sobrescriben la validación de horas, la descripción y el costo base. Reserva vincula los objetos y controla sus transiciones.
- gestion.py administra tres listas internas, comprueba códigos únicos por colección y rechaza referencias inexistentes. Una reserva pendiente o confirmada ocupa el servicio. Cancelarla o procesarla lo libera. Una reserva procesada o cancelada es definitiva.
- Una sala se alquila de 1 a 12 horas a tarifa simple. Un equipo admite de 1 a 72 horas y suma 5000 COP por alistamiento. Una asesoría admite de 0.5 a 8 horas y añade 10 % por preparación. Son reglas ilustrativas del proyecto. Use punto decimal para fracciones.
- calcular_costo admite variantes con horas, con horas y descuento, o con horas, descuento e impuesto mediante parámetros opcionales. También admite impuesto por nombre. Se usan importes Decimal y redondeo final a dos decimales.
- main.py aísla cada operación mediante try/except/else/finally. Las excepciones DatoInvalido y OperacionInvalida distinguen problemas de entrada y de negocio. La conversión numérica conserva la causa con raise ... from. Los fallos inesperados también quedan registrados. Si el archivo de eventos no se puede abrir, se informa la causa y el registro continúa en consola.
- La simulación contrasta cada resultado con la clase de error esperada o con el éxito esperado. Incluye una llamada incompleta deliberada para demostrar la recuperación ante un error de programación.
