# openday_edem
OpenDay EDEM Ejercicio

## Instrucciones para Crear un Bucket en AWS usando la Consola Web

A continuación, se describen los pasos para crear un bucket en AWS S3 utilizando la consola web de AWS.

### Prerrequisitos

1. **Cuenta de AWS**: Asegúrate de tener una cuenta activa en AWS usando las credenciales dadas.
2. **Acceso a la Consola Web**: Inicia sesión en la consola web de AWS en [https://nw-pedronieto-sandbox.signin.aws.amazon.com/console](https://nw-pedronieto-sandbox.signin.aws.amazon.com/console).
### Pasos para Crear un Bucket

1. **Acceder al Servicio S3**:
   - Una vez que hayas iniciado sesión en la consola de AWS, busca "S3" en la barra de búsqueda superior y selecciona el servicio **S3**.

2. **Crear un Nuevo Bucket**:
   - Haz clic en el botón **Create bucket** (Crear bucket).

3. **Configurar el Nombre del Bucket**:
   - En el campo **Bucket name**, ingresa un nombre único para tu bucket. Por ejemplo: `nombre-alumno-openday`.
   - Nota: El nombre debe ser único a nivel global y no puede contener espacios ni caracteres especiales.

4. **Seleccionar la Región**:
   - En la sección **AWS Region**, selecciona la región donde deseas crear el bucket (por ejemplo, 'eu-west-1`).

5. **Configurar Opciones Adicionales**:
   - Puedes dejar las configuraciones predeterminadas para las opciones adicionales, como el control de acceso público y el cifrado. Asegúrate de revisar estas configuraciones según tus necesidades.

6. **Crear el Bucket**:
   - Haz clic en el botón **Create bucket** (Crear bucket) al final de la página.

7. **Verificar el Bucket**:
   - Una vez creado, serás redirigido a la lista de buckets. Busca el nombre de tu bucket en la lista para confirmar que se creó correctamente.


¡Listo! Ahora tienes un bucket creado en AWS S3 usando la consola web.

## Segundo paso Vamos a crear una web

Si quieres crear tu propia pagina web te doy un posible prompt para pedirselo a chatgpt, si no puedes coger el que he dejado de ejemplo:

```bash
Genera una página web de una tienda de móviles en html con las siguientes funcionalidades:

Diseño más moderno y limpio.
Animaciones más suaves y sutiles.
Iconos de carrito en botones.
Scroll suave para navegación.
Imagen destacada en el header.
URLs limpias y más consistencia visual.
Optimizado para responsive.

```
Una vez que lo tengáis guardad el contenido como 

index.html

Y subidlo a vuestro bucket de S3, para ello seguid estos pasos:
1. **Acceder al Bucket**:
   - En la consola de S3, haz clic en el nombre del bucket que acabas de crear.
2. **Subir Archivos**:
3. Haz clic en el botón **Upload** (Subir).
4. Selecciona el archivo `index.html` que has creado y haz clic en **Next** (Siguiente).
5. Una vez subido, selecciona el archivo y pulsa el botón de "open" para abrirlo.


## Tercer paso

Ahora vamos a crear una lambda que reaccione a la subida de un archivo a nuestro bucket, para ello vamos a crear una lambda que se ejecute cada vez que subamos un archivo a nuestro bucket.

1. **Acceder al Servicio Lambda**:
   - En la consola de AWS, busca "Lambda" en la barra de búsqueda superior y selecciona el servicio **Lambda**.
2. **Crear una Nueva Función Lambda**:
3. Haz clic en el botón **Create function** (Crear función).
4. Selecciona **Author from scratch** (Crear desde cero).
5. Asigna un nombre a la función, por ejemplo: `nombre_alumno_lambda`.
6. Selecciona el **Runtime** (entorno de ejecución) que prefieras, por ejemplo: `Python 3.x`.
7. Crear un nuevo rol de ejecución con permisos básicos de Lambda.
8. Crear un Trigger de tipo S3 
9. Selecciona el bucket que has creado anteriormente.
10. Selecciona el evento `All object create events` (Todos los eventos de creación de objetos).
11. Haz clic en **Add** (Agregar) para añadir el trigger.
12. Vete a la opción de código y pega este código:
```python
import json
import logging

def lambda_handler(event, context):
    logging.getLogger().setLevel(logging.INFO)
    logging.info('Loading function')
    logging.info(event)
    logging.info(context)
    # TODO implement
    return {
        'statusCode': 200,
        'body': json.dumps('Hello from Lambda!')
    }
```
13. Haz clic en **Deploy** (Desplegar) para guardar los cambios.
14. **Probar la Función Lambda**:
    - Puedes probar la función Lambda haciendo clic en el botón **Test** (Probar) y creando un evento de prueba. Asegúrate de que la función se ejecute correctamente y registre los eventos en CloudWatch.
15. **Verificar los Logs**:
    - Ve a la consola de CloudWatch y selecciona **Logs** (Registros) para ver los registros generados por tu función Lambda. Busca el grupo de registros correspondiente a tu función Lambda y revisa los logs para asegurarte de que la función se ejecute correctamente.

## Cuarto paso

Vamos a probar!! Ahora sube un archivo a tu bucket y comprueba que se ha ejecutado la lambda, para ello ve a la consola de CloudWatch y selecciona **Logs** (Registros) para ver los registros generados por tu función Lambda. Busca el grupo de registros correspondiente a tu función Lambda y revisa los logs para asegurarte de que la función se ejecute correctamente.
