# Challenge 24: Differential diagnostic optimization and mental illness symptoms identification using AI with text data


This challenge aims to improve the efficiency and precision of differential diagnostics using clinical text data. Using specific examples, it allows to adjust the diagnostics process in sequential steps, quickly integrate different sources data and analyse them in a flexible way and provide a detailed context to improve the precision and reliability of the AI proposed diagnostics, as well as optimizing the clinical trial selection and the treatment recomendation.

## Objective

Develop an AI model that is able to identify spacific diagnostics like bipolar disorder, schizophrenia, depressive disorder, etc., and transdiagnostic symptoms like imsomnia, irritability, anxyety, etc. from clinical course texts and clinical histories written by health proffessionals.


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
1. BASE24. Contains:
	- DAT24_01: Free text document: Discharge report
	- DAT24_02: Free text document: Emergency discharge report
	- DAT24_03: Free text document: Evolution report
	- DAT24_04: Free text document: Neuropsychologycal report, psychometry
	- DAT24_05: Free text document: TEC report
	- DAT24_06: Free text document: Neuropicture
	- DAT24_07: Lab data (LAB)
	- DAT24_08: Demographic data (DEMO)
	- DAT24_09: Socioeconomic data (SOCIOECONOMICOS)
2.	OUT24 (Write-only backup where the challenge results will be stored).



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

LABORATORIO:
| Name      | Description |
| ----------- | ----------- |
| ou_med      | Medical unit that performas the extraction    |
| extrac_date      | Extraction date   |
| extrac_time      | Extraction time    |
| lab_ref      | Lab reference   |
| lab_desc      | Reference description  |
| result      | Result    |
| units      | Result units    |
| rang      | Normal value range   |
| id_patient_pseu      | Patient identification number that links the patients between tables    |
| id_epis_pseu      | Episode identification number  |





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

-	Precission: Correct diagnostics percentage that are proposed by the model.
-	Recall: Model abilty to identify all of the possible correct diagnostics.
-	F1-score: Combined measurement of precission and recall to avualte the global efficiency of the model.
-	Exactitud: Correct diagnostics percentage between all of the analysed cases.
-	AUC (Area Under Curve): Model capacity measurement to distinguish between different diagnostics classes.
-	Other specified metrics: Capacity to identify transdiagnostic symptoms, diagnostic time reduction, improvement in life quality for the patients.

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
	




