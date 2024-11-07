# Validación GenHack

El Pre-hackaton durará de las 8:00h del dia 5/11/2024 hasta las 20:00h del 6/11/2024 pasada esa hora las cuentas se cerraran y no se podrá acceder, os pedimos que realicéis toda la validación ya que es imprescindible determinar si todo esta correcto antes del evento. En la tabla de continuación, se muestra para cada miembro participante el grupo, challenge y base asignada de validación.

| Participante | Reto | TEAM | BASE name |
|:-:|:-:|:-:|:-:|
| Pau | Challenge01 | Team2 | BASE01 |
| Xavi | Challenge24 | Team1 | BASE24 |
| Petter | Challenge17 | Team0 | BASE17 |
| Santi | Challenge23 | Team6 | BASE23 |
| David | Challenge31 | Team9 | BASE30 |



## Conexión AWS
- Acceder a la cuenta. Revisar el correo. Este indica la URL para acceder a la cuenta de AWS (apartado 3.1 del readme)
- Habilitar los modelos de Bedrock (apartado 3.2.1 del readme)
- Crea un notebook de SageMaker (apartado 3.2.2 del readme)

## Test permisos
- Acceder a bucket [data-clinic-hackathon-2024](https://us-west-2.console.aws.amazon.com/s3/buckets/data-clinic-hackathon-2024?region=us-west-2&bucketType=general&tab=objects).
- Comprobar que ÚNICAMENTE puede ver los ficheros de la base asignada a su reto (mirar en la tabla columna BASE name).
- Lectura de un fichero csv o txt de la carpeta asignada a su reto (mirar en la tabla columna BASE name). Utilizar `DEMO_s3_read_file`.
- Intentar escribir un fichero en la carpeta asignada a su reto (mirar en la tabla columna BASE name). Utilizar `DEMO_s3_write_file`. **No debería dejar hacer esta acción. En el caso que se pueda en el grupo de teams hackaton-2024-preparacion datos**
- Escribir un fichero en la carpeta de su equipo dentro del bucket [shared-clinic-hackathon-2024](https://us-west-2.console.aws.amazon.com/s3/buckets/shared-clinic-hackathon-2024?region=us-west-2&bucketType=general&tab=objects) (mirar en la tabla columna TEAM). Utilizar `DEMO_s3_write_file`.
- Leer el fichero escrito en el punto anterior. Utilizar `DEMO_s3_read_file`.
- Escribir un fichero en la carpeta de su equipo dentro del bucket [results-clinic-hackathon-2024 ](https://us-west-2.console.aws.amazon.com/s3/buckets/results-clinic-hackathon-2024?region=us-west-2&bucketType=general&tab=objects) (mirar en la tabla columna TEAM). Utilizar `DEMO_s3_write_file`.
- Leer el fichero escrito en el punto anterior. Utilizar `DEMO_s3_read_file`.
- Probar de leer/escribir en otras carpetas de los buckets [data-clinic-hackathon-2024](https://us-west-2.console.aws.amazon.com/s3/buckets/data-clinic-hackathon-2024?region=us-west-2&bucketType=general&tab=objects), [shared-clinic-hackathon-2024](https://us-west-2.console.aws.amazon.com/s3/buckets/shared-clinic-hackathon-2024?region=us-west-2&bucketType=general&tab=objects), y [results-clinic-hackathon-2024 ](https://us-west-2.console.aws.amazon.com/s3/buckets/results-clinic-hackathon-2024?region=us-west-2&bucketType=general&tab=objects). **No debería dejar hacer esta acción. En el caso que se pueda escribid en el grupo de teams hackaton-2024-preparacion datos**

## Test de Bedrock
- Seguir el manual `DEMO_bedrock_connection`.

## Test creación RAG
- Seguir el manual `DEMO_RAG_with_KnowledgeBase`.
- Crear un RAG del reto asignado siguiendo la demo: `DEMO_RAG_with_KnowledgeBase`. Hacer preguntas sobre la información que contienen los documentos utilizados como fuente de datos.
- [NO PROBAR] Seguir el manual `DEMO_RAG_with_Kendra`.
- [NO PROBAR]  Crear un RAG del reto asignado siguiendo la demo: `DEMO_RAG_with_Kendra`. Hacer preguntas sobre la información que contienen los documentos utilizados como fuente de datos.
