# Challenge 17: Non-structured data extraction from release reports to predict re-admission risk and death during the transactional atention


This challenge aims to use large language models (LLM) to analyze and extract non-structured data from release reports. The reliability and impact of this data in the predictive models will be evaluated to improve safety and efficiency in post-hospital attention.



## Objective

Integrate non-structured data extraction from release reports in machine learning predictive models to evaluate and predict re-admission risk and death during the transactional atention.



## AWS Tools

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
    - DEMO_RAG_with_Kendra
    - DEMO_download_studies_and_upload_to_s3
    - DEMO_s3_read_file
    - DEMO_s3_write_file

## Database
      
The databases that make up this challenge are:
1.	BASE17. Contains:
    - DAT17_01: Free text document: Discharge report
    -	DAT17_02: Demographic data (DEMO)
    -	DAT17_03: Socioeconomic data (SOCIOECONOMICOS)

**Summary of the tables**
DEMO
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

SOCIECONOMICOS
| Name      | Description |
| ----------- | ----------- |
| register_date      | Register date     |
| register_time      | Register time     |
| situ_lab      | Employment status     |
| vive_con      | Co-habitation status. Alone, with family, shared home.   |
| cuida_nomb      | Name of the care giver       |
| id_patient_pseu      | Patient identification number that links the patients between tables       |

**Free text documents**
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




## Evaluation metrics

The performance of the predictive models will be evaluated by metrics: precission, sensibility and specificity, AUC and F1-score. Also the impact of the captured variables will be evaluated via LLM with the relative importance in the models.


## Shared bucket
Participants have an available bucket to store all of the desired documents and use them to develop the challenge.


```
https://us-west-2.console.aws.amazon.com/s3/buckets/shared-clinic-hackathon-2024?region=us-west-2&bucketType=general&tab=objects
```

Members of each group ONLY will have access to the folder with the name of their group. It is advised to check `demos DEMO_s3_read_file` and `DEMO_s3_write_file` to learn how to write and read a file from a bucket. Use the following values in the demos:


```python
BUCKET_NAME = 'shared-clinic-hackathon-2024' 
BUCKET_FILE_LOCATION_AND_NAME = '<nombre_del_grupo>/<nombre_del fichero>' 
# NOTA: 
# - remplazar <nombre_del_grupo> por el nombre del grupo al que usted pertenece  (por ejemplo, Team1) 
# - remplazar <nombre_del fichero> por el nombre del fichero que se desea leer/escribir.
``` 


## Results
The challenge will only be validated if the participants save ALL the needed files to replicate the proposed answer by the members of the group. This implies that if the group integrants needed to modify somo of the files that have been provided with, or they have used external info to solve the challenge, they must include it as a part of the answer.


The files must be stored in the buscket [results-clinic-hackathon-2024](https://us-west-2.console.aws.amazon.com/s3/buckets/results-clinic-hackathon-2024?region=us-west-2&bucketType=general&tab=objects). The files location inside the bucket must be: `<nombre_grupo>/<nombre_reto>/<ficheros_resultados>`. 


It is advised to use demo `DEMO_s3_write_file` to write the files/code of the proposed answer. Use the following values in the demos:


```python
BUCKET_NAME = 'results-clinic-hackathon-2024' 
BUCKET_FILE_LOCATION_AND_NAME = '<nombre_del_grupo>/<nombre_del reto>/<nombre_del fichero>' 
# NOTA: :
# - remplazar <nombre_del_grupo> por el nombre del grupo al que usted pertenece (por ejemplo, Team1)
# - remplazar <nombre_del reto> por el nombre del reto al que corresponde la solución propuesta (por ejemplo, Challenge1)
# - remplazar <nombre_del fichero> por el nombre del fichero que se desea almacenar (por ejemplo, main_code_challenge1.ipynb)
``` 
