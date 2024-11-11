# Challenge 29: Hospital Clinic Web

The Hospital Clínic website is one of the most visited non-English-speaking websites globally, a testament to the exceptional expertise of its healthcare professionals and the outstanding quality of its content. This reflects the hospital's status as a leader in the field of medicine, both locally and internationally. However, despite its rich repository of information, the current navigation architecture, based on traditional hyperlink systems, and the limited functionality of its local search engines present significant challenges. These include fragmented information across various sections, difficulty locating specific content, and search results that are either too broad or irrelevant, making it harder for users to access the precise information they need efficiently.
The challenge lies in overcoming these limitations by leveraging the advanced semantic understanding and natural language processing capabilities of modern large language models (LLMs). These models could enable users to interact with the website in a conversational manner, using natural language queries to locate specific information seamlessly. By doing so, the website could provide more accurate, relevant, and user-centered results, dramatically improving the user experience. This approach would transform the website from a static information portal into an intelligent, dynamic platform that enhances user engagement and accessibility, aligning with the hospital's commitment to innovation and excellence in patient care and communication.

## Objective

El objetivo es generar un chatbot poder dar una repuesta al usuario basandonos en la información que contiene la web del HCB

## Expected Outcomes

Generar un chatbot que pueda contestar de forma clara y concisa las preguntas que se le estan realizando por usuario, y que indique donde se encuentra la información solicitada por el usuario.

## Tools

Participants will have the following information/tools to complete the challenge.

- Database:
    - Information about the database.

- Develop:
    - Jupyter Notebook
    - Bedrock
    - Bucket shared

- Manuals. It is recommended to consult the following demos:
    - DEMO_bedrock_connection
    - DEMO_RAG_with_KnowledgeBase
    - DEMO_download_studies_and_upload_to_s3
    - DEMO_s3_read_file
    - DEMO_s3_write_file


**All development must be carried out using the services available on AWS. Moving information outside of the specified tools is NOT allowed.**

Below are details of the most relevant aspects of the tools available to participants.

### Database

Los datos necesarios para hacer el reto se encuentran en la web:

https://www.clinicbarcelona.org/asistencia/

Tened en cuenta que al hacer el RAG supera el tamaño permitido y no se puede hacer un RAG de toda la URL.


### Shared bucket

Participants have access to a shared bucket to store any necessary documents for the challenge.

```
https://us-west-2.console.aws.amazon.com/s3/buckets/shared-clinic-hackathon-2024?region=us-west-2&bucketType=general&tab=objects
```

Each group has access ONLY to the folder named after their group. It is recommended to check the demos `DEMO_s3_read_file` and `DEMO_s3_write_file` to learn how to read and write files from a bucket. Use the following values in the demos:

```python
BUCKET_NAME = 'shared-clinic-hackathon-2024'
BUCKET_FILE_LOCATION_AND_NAME = '<grupo_name>/<file_name>'
# NOTE:
# - replace <grupo_name> by the name of your team  (e.g. Team1)
# - replace <file_name> by the file name you want to read/write.
```

## Results

The challenge will only be considered valid if participants save ALL files necessary to reproduce the solution proposed by the group members. This implies that if the group members modified any provided files or used external information to solve the challenge, these must be included as part of the solution.

Files must be saved in the bucket: [results-clinic-hackathon-2024](https://us-west-2.console.aws.amazon.com/s3/buckets/results-clinic-hackathon-2024?region=us-west-2&bucketType=general&tab=objects). The file location within the bucket (prefixes) must be: `<group_name>/<challenge_name>/<file_name>`.

It is recommended to use the `DEMO_s3_write_file` demo to write the files/code of the proposed solution. Use the following values in the demos:

```python
BUCKET_NAME = 'results-clinic-hackathon-2024'
BUCKET_FILE_LOCATION_AND_NAME = '<group_name>/<challenge_name>/<file_name>'
# NOTA: :
# - replace <group_name> by the name of your team (e.g. Team1)
# - replace <challenge_name>  by the name of the challenge (e.g. Challenge1)
# - replace <file_name> by the name of the file that you want to store (e.g., main_code_challenge1.ipynb)

```
### Evaluation Metrics

- **Tasa de rendimiento**: Número de respuestas correctas dividido por el número de sesiones activas (una respuesta correcta es una respuesta sugerida por el bot y cliqueada por el usuario en caso de múltiples opciones, o abierta instantáneamente en caso de una fuerte coincidencia semántica).
- **Tasa de satisfacción**: Nota media otorgada al evaluar las respuestas del chatbot (para equilibrar con la tasa de evaluación).
- **Tasa de evaluación**: Porcentaje de respuestas acertadas.
- **Número promedio de interacciones**: Se utiliza para evaluar el Índice de esfuerzo del cliente (CES) en el chatbot y debe correlacionarse con el índice de satisfacción. Si este último es muy bajo, es posible que el bot esté involucrando a los usuarios en demasiadas ramas y pasos para satisfacer sus necesidades. En este caso, una solución puede ser corregir los árboles de decisión o la arquitectura de la base de conocimiento.
- **Tasa de falta de respuesta**:La cantidad de veces que el chatbot no ha podido enviar ningún contenido después de una pregunta (debido a la falta de contenido o malentendido).











