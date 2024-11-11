# Challenge 21: Structuring Digestive Endoscopy Reports Using Pretrained LLM

The results of digestive endoscopy procedures (gastroscopies and colonoscopies) are documented in natural language in an unstructured format. Structuring the documentation of endoscopy reports could enable data analysis capabilities that would be beneficial for both management and research purposes. Currently, there are no automated tools available that process natural language for analyzing this type of documentation and, certainly, it is not used in clinical practice or for any other type of analysis. Although the information in a digestive endoscopy report is in free-text format, it follows a strong underlying structure since it is generated from a template that the endoscopist then edits to generate the final report. This characteristic could make the task easier for a language model.

## Objective

To generate a large corpus of digestive endoscopy results in a structured format from reports written in natural language using general pretrained LLM.

## Expected Outcomes

The solution proposed by participants should be able to generate a JSON containing the report information in a structured manner.

**Gastroscopy**
- Report example
```txt
GASTROSCOPIA
Sedación y analgesia con propofol y remifentanilo por parte del servicio de Anestesia. 
- ESÓFAGO: cardias a 35m de arcada dentaria. Mucosa de aspecto normal. 
- ESTÓMAGO: mucosa de fundus, cuerpo e incisura de aspecto normal. 
    Antro con discreto eritema y congestión. Se toma biopsia de antro (tubo 1).
- DUODENO: bulbo y segunda porción duodenal de aspecto normal.
- CONCLUSIONES:
Antritis no erosiva. Biopsia de antro.”
```
- Json outcome

```json
{
    "exploration": "gastroscopy",
    "anestesia": {
        "sedative": "propofol",
        "analgesia": "remifentanil"
    },
    "reason": "Dispepsia",
    "result": [
        {
            "section": "esófago",
            "findigs": ["normal", "cardias a 35cm"],
            "procedures": []
        },
        {
            "section": "fundus",
            "findigs": ["normal"],
            "procedures": []
        },
        {
            "section": "cuerpo",
            "findigs": ["normal"],
            "procedures": []
        },
        {
            "section": "incisura",
            "findings": ["normal"],
            "procedures": []
        },
        {
            "section": "antro",
            "findigs": ["antritis"],
            "procedures": ["biopsia"]
        }
    ],
    "conclusiones": ["antritis", “biopsia de antro”]
}
```     
**Colonoscopy**

- Report example

```txt
Aparato:OLYMPUS CF-EZ1500DL; 2100846 Motivo de la exploración: Colonosocpia de control en paciente con polipos adenomatosos. 
Premedicación: Se administra Propofol / Remifentanilo por el Servicio de Anestesia Tipo de Insuflación: Se realiza exploración con CO2 Preparación: Clasificación Boston por segmentos: 3+3+3 Preparación excelente (Clas Boston > 7 con ningún segmento < 2): Mucosa visualizada en su totalidad. 
Ausencia de restos no aspirables.
Extensión exploración: Se explora todo el colon hasta el ciego. 
Exploración: Se explora detenidamente la mucosa colónica, identificando: 
- En colon ascendente pólipo sesil (Paris Is, NICE 2) de 8 mm que se extrae con asa fria en un solo fragmento. En ángulo hepático se identifica pólipo plano elevado (Paris IIa) de aspecto serrado de 12mm que se extrae con asa fria en dos fragmentos y pólipo plano elevado (Paris IIa) de aspecto serrado de 14mm que se extrae con asa fria en múltiples fragmentos. Se recuperan todos para AP en tubo 1. 
- En colon transverso se identifica pólipo plano elevado (Paris IIa) de aspecto serrado de 10mm que se extrae con asa fria en dos fragmentos y se recupera para AP en tubo 2. 
- Orificios diverticulares localizados en todo el marco colónico de predominio en sigma sin signos de inflamación ni hemorragia. Hay fijación de asas que dificultan la progresión a nivel de sigma. 
- Se explora la ampolla rectal por retroversión identificando papilas anales. 
Procedimientos: Se ha realizado polipectomía endoscópica de 4 lesiones. Se recuperan 4 para AP. Orientación diagnóstica: Pólipos en colon x4. Se efectúa polipectomía. Pendiente AP. Diverticulosis. No se observan complicaciones inmediatas después del procedimiento. No obstante, se explica al paciente la actitud a seguir ante la aparición posterior de complicaciones.
```

- Json outcome

```json
{
    "exploration": "colonoscopy",
    "gear": "OLYMPUS CF-EZ1500DL;2100864",
    "reason": "Colonoscopia de control de paciente con pólipos",
    "anestesia": {
        "sedative": "propofol",
        "analgesia": "remifentanil"
    },
    "preparation": {
        "boston": [3, 3, 3],
        "subjective_eval": "excelente"
    },
    "extension": "ciego",
    "result": [
        {
            "section": "ciego",
            "findings": []
        },
        {
            "section": "colon ascendente",
            "findings": [
                {
                    "type": "pólipo",
                    "details": {
                        "size_mm": 8,
                        "location": "colon ascendente",
                        "morphology": "sesil",
                        "aspect": "serrado",
                        "resected": true, 
                        "recovered": true
                    }
                },
                {
                    "type": "pólipo",
                    "details": {
                        "size_mm": 12,
                        "location": "angulo hepático",
                        "morphology": "plano elevado",
                        "aspect": "serrado",
                        "resected": true,
                        "recovered": true
                    }
                },
                {
                    "type": "pólipo",
                    "details": {
                        "size_mm": 14,
                        "location": "ángulo hepático",
                        "morphology": "plano elevado",
                        "aspect": "serrado",
                        "resected": true,
                        "recovered": true
                    }
                }
            ]
        },
        {
            "section": "colon transverso",
            "findings": [
                {
                    "type": "polyp",
                    "details": {
                        "size_mm": 10,
                        "location": "colon transverso",
                        "morphology": "plano elevado",
                        "aspect": "serrado",
                        "resected": true, 
                        "recovered": true
                    }
                }
            ]
        },
        {
            "section": "colon descendente",
            "findings": []
        },
        {
            "section": "sigma",
            "findings": [
                {
                    "type": "divertículos"
                }
            ]
        },
        {
            "section": "recto",
            "findings": [
                {
                    "type": "papilas anales"
                }
            ]
        }
    ],
    "procedures": ["polipectomía"],
    "diagnosis": ["pólipos", "divertículos"],
    "complications": "no complicaciones"
}
``` 


## Tools

Participants will have the following information/tools to complete the challenge.

- Database:
    - Information about the database.

- Develop:
    - Jupyter Notebook
    - Bedrock
    - Shared bucket 

- Guides. It is recommended to consult the following demos:
    - DEMO_bedrock_connection
    - DEMO_RAG_with_KnowledgeBase
    - DEMO_RAG_with_Kendra
    - DEMO_download_studies_and_upload_to_s3
    - DEMO_s3_read_file
    - DEMO_s3_write_file



**All development must be carried out using the services available on AWS. Moving information outside of the specified tools is NOT allowed.**

Below are details of the most relevant aspects of the tools available to participants.


### Database
 
The databases that make up this challenge are:
- BASE21. Contains:
	- DAT21_01: Free-text documents
	- DAT21_02: Requests for endoscopy examinations
	- DAT21_03: Demographic data (DEMO)
	- DAT21_04: Socioeconomic data (SOCIOECONOMICOS)







#### Summary of the tables

A. DEMO

| Name      | Description |
| ----------- | ----------- |
| Sex      | Patient's sex, 1 for male, 2 for female, 3 for other      |
| Birth_date      | Patient's birth date     |
| Civil_status      | Patient's marital status      |
| Natio      | place of residence, nation_dic.txt file      |
| Idiom      | Patient's language   |
| Zip_code      | Postal code      |
| Health_area      | Health area       |
| Employment_situation      | Employment situation       |
| Contact      | Contact person     |
| id_patient_pseu      | Patient identification number that links the patients between tables      |

B. SOCIECONOMICOS

| Name      | Description |
| ----------- | ----------- |
| register_date      | Register date     |
| register_time      | Register time     |
| situ_lab      | Employment status     |
| vive_con      | Co-habitation status. Alone, with family, shared home.   |
| cuida_nomb      | Name of the care giver       |
| id_patient_pseu      | Patient identification number that links the patients between tables       |

C. FREE TEXT DOCUMENTS

The types of reports that we may encounter are:

| Name      | Description |
| ----------- | ----------- |
| INF_VAL_INI      | Starting validation report  |
| EVOL_ANCLD/ INF_EVO      | Evolution report |
| INF_AL_UR      | Emergency discharge report  |
| INF_AL      | Discharge report  |
| INF_AD      | Hospital admission report  |
| INF_TR      | Transport report  |
| TC_CR      | Cranial CT  |
| CUR_CLI      | Clinical course  |
| INF_END      | Endoscopy report  |
| IR_PSI_CLIN      | Neuropsychologycal report, psychometry  |
| IR_PSI_TEC      | TEC reports  |

In the free-text reports the file name is always structured as follows:

{challenge_number}_{challenge_identifier_number}_{report_type}_{id_patient_pseu}_{creation_date}_{counter}.txt

For example:
01_02_INF_VAL_INI_407789453_20211119_29.txt
-	Challenge: 01
-	Challenge identifier number: 02
-	Report type: INF_VAL_INI
-	Id_patient_pseu: 407789453
-	Creation date (YYYYMMDD): 20211119
-	Counter: 29


 


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



## Evaluation Metrics

Once the model is created, it will be evaluated by the challenge members using metrics such as sensitivity (recall), precision, and F1 score. They should compare the ground truth (correct labeled data) with the predicted output (from the model), both of which should be JSON objects. The metric’s evaluation should be performed both automatically with strict exact match for each entity and also manually from domain experts. It is possible that the model extracts equivalent (but not exact) information compared to the correct labeled dataset. This can be performed using a rubric that may look like the following one. 

| Criteria      | Description | Score Range (1-5) |
| ----------- | ----------- | ----------- |
| **Entity Recognition Accuracy**      | How accurately the model identifies entities from the endoscopy reports (e.g., organs, pathologies, procedures). This includes correctly identifying locations like esophagus, stomach, duodenum, etc.  | 1:Significant misidentifications                 5:All entities correctly identified  |
| **Entity Classification**      | Accuracy in categorizing entities under the correct type (e.g., identifying "biopsy" as a procedure, "antrum" as a location).  | 1:Frequent misclassifications                 5:Entities accurately categorized  |
| **Relation Extraction**      | Accuracy in identifying relationships between entities (e.g., biopsy was taken from the antrum, sedation was provided by anesthesia).  | 1:Incorrect or missing relationships                 5:All relationships correctly captured  |
| **Completeness of Extraction**      | How well the model captures all relevant information from the report (i.e., does it miss any key entities or relationships?).  | 1:Many key details missing                5:No key details missed  |
| **Adherence to JSON Format**      | How well the output adheres to the predefined JSON format. It should include all required fields and data in the correct structure.  | 1:Frequent format errors              5:Consistent adherence to JSON format  |
| **Handling of Free-Text Details**      | The model's ability to handle free-text observations that are harder to structure, ensuring they are captured in an accurate and usable way.  | 1: Poor handling of free-text details            5:All free-text details structured appropriately or stored in observations  |
| **Procedure Differentiation**      | How well the model differentiates between gastroscopy and colonoscopy reports, applying the appropriate structure to each.  | 1:Frequent confusion between procedure types                 5:Clear and accurate distinction between gastroscopy and colonoscopy  |

**Hints:**
Dagdelen J, Dunn A, Lee S, et al. Structured information extraction from scientific text with large language models. Nat Commun. 2024;15(1):1418. doi:10.1038/s41467-024-45563-x

