# Challenge 29: Chatbot for Hospital Clinic website

The Hospital Clínic website is one of the most visited non-English-speaking websites globally, a testament to the exceptional expertise of its healthcare professionals and the outstanding quality of its content. This reflects the hospital's status as a leader in the field of medicine, both locally and internationally. However, despite its rich repository of information, the current navigation architecture, based on traditional hyperlink systems, and the limited functionality of its local search engines present significant challenges. These include fragmented information across various sections, difficulty locating specific content, and search results that are either too broad or irrelevant, making it harder for users to access the precise information they need efficiently.

The challenge lies in overcoming these limitations by leveraging the advanced semantic understanding and natural language processing capabilities of modern large language models (LLMs). These models could enable users to interact with the website in a conversational manner, using natural language queries to locate specific information seamlessly. By doing so, the website could provide more accurate, relevant, and user-centered results, dramatically improving the user experience. This approach would transform the website from a static information portal into an intelligent, dynamic platform that enhances user engagement and accessibility, aligning with the hospital's commitment to innovation and excellence in patient care and communication.

## Objective

The objective is to develop a chatbot capable of answering user inquiries based on information available on the Hospital Clínic de Barcelona (HCB) website.

## Expected Outcomes

### Example 1:
 ```
-- USER -- 
    
   Tinc mal de cap, què em puc prendre? 
  
-- Chatbot --  

En primer lloc, és important saber quin tipus de mal de cap o cefalea tens. Per exemple, existeix la cefalea tensional, la cefalea per esforç físic o la migranya, entre d’altres.  En segon lloc, cal identificar si hi ha desencadenants d’aquesta cefalea. Com l'alteració del ritme del son o la presa d'algun aliment o medicament.  
En tercer lloc, el dolor es pot tractar amb analgèsics com el paracetamol. Si es tracta de cefalea tensional es recomana fer servir tècniques de relaxació. 

Davant d'un primer episodi de cefalea que no marxa amb analgèsics com el paracetamol, o bé davant cefalea repetida que distorsiona les activitats de la vida diària, s'ha de consultar al metge de família. 

És molt important no automedicar-se ni recomanar tractaments a altres pacients, ja que pot ser que no tinguin el mateix tipus de cefalea i, en conseqüència, el tractament sigui diferent. En cas de dubte és recomanable consultar amb un especialista ja que cada cas s'ha d'estudiar en profunditat de manera independent. 


Font de la informació: https://www.clinicbarcelona.org/ca/asistencia/malalties/cefalea 
  ```
 

### Example 2:

```
-- USER -- 

Per què no es pot curar el VIH? 

-- Chatbot --  

Actualment, no hi ha un tractament curatiu per al VIH. La vacuna representa la major esperança per erradicar aquest virus però l’obtenció de vacunes eficaces contra el VIH és encara una gran assignatura pendent.   

Aquesta és una tasca científica complexa a causa dels mecanismes d’adaptació i evasió del VIH a la resposta immunitària i a les dificultats de desenvolupament, aplicació i avaluació dels prototips de vacunes. Fins ara no s’ha obtingut cap vacuna preventiva contra la infecció pel VIH. 

El tractament actual s’anomena antiretroviral i inclou dos o tres fàrmacs en total. És molt eficaç, cal prendre’l tota la vida i és molt important seguir-lo de forma adequada, tal com ho prescrigui l’especialista. 

Els antiretrovirals es toleren bé i en poques ocasions causen efectes secundaris.  


Font de la informació: https://www.clinicbarcelona.org/ca/asistencia/malalties/vih-sida 
```
 

## Tools

Participants will have the following information/tools to complete the challenge.

- Database:
    - Information about the database.

- Develop:
    - Jupyter Notebook
    - Bedrock
    - Bucket shared

- Guides. It is recommended to consult the following demos:
    - DEMO_bedrock_connection
    - DEMO_RAG_with_KnowledgeBase
    - DEMO_download_studies_and_upload_to_s3
    - DEMO_s3_read_file
    - DEMO_s3_write_file


**All development must be carried out using the services available on AWS. Moving information outside of the specified tools is NOT allowed.**

Below are details of the most relevant aspects of the tools available to participants.

### Database

The necessary data to generate the chatbot are in the following web page:

https://www.clinicbarcelona.org/

The chatbot has to use only "Assistance and health" section of the web page.

**NOTE:** If a patient is not found in the databases, the k-anonimization has deleted it.


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

- **Success Rate:** The ratio of correct responses provided by the bot to active sessions. A response is considered correct if the user clicks on the suggested answer among multiple options or opens it immediately if there's a strong semantic match.
- **Satisfaction Rate:** The average rating given by users when evaluating the chatbot's responses. This rate should also be considered alongside the Evaluation Rate to ensure a balanced measure of user satisfaction.
- **Evaluation Rate:** The percentage of responses deemed accurate by users or evaluators.
- **Average Number of Interactions:** This metric reflects the Customer Effort Score (CES) for the chatbot, helping assess the effort users put into finding their answers. It should correlate with the satisfaction rate; if satisfaction is low and interaction count is high, it may indicate that the bot leads users through too many steps or branches to meet their needs. Improving decision trees or knowledge base architecture may be beneficial in such cases..
- **No-Response Rate:** The number of times the chatbot fails to provide any relevant content after a question is asked. This may be due to content gaps or misinterpretations.











