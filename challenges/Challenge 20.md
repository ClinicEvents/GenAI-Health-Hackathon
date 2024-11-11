# Challenge 20: Optimizing Clinical Research Using Artificial Intelligence for Extracting and Analyzing Stroke Patient Data


The main objective of this challenge is to automate the extraction of specific data from medical reports, medical notes, and complementary studies for patients who have experienced a stroke in 2023. These extracted data will be integrated and compared with an existing database (CICAT-Stroke Code Database) containing multiple variables related to the clinical characteristics of the patients. The goal is to enhance the precision and efficiency of collecting relevant clinical data for research and analyzing treatments, risk factors, and neurological outcomes of stroke patients.

This challenge is scalable to any disease and/or specialty. The target population includes patients diagnosed with stroke who have been assessed through the Stroke Code Circuit, covering a range of ages, genders, and medical histories, with a focus on those who have received specific treatments. The project is expected to significantly improve the efficiency and accuracy of clinical data collection and analysis, facilitating research and clinical studies for ischemic stroke patients.



## Objective

Use artificial intelligence to automate the extraction of specific data from medical reports, medical notes, and complementary studies for stroke patients from 2023.


## Expected Outcomes
To be agreed with the mentor.

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

- BASE19. Contains:
  	-	DAT19_01: Free text document: Emergency discharge report
 	 -	DAT19_02: Free text document: Hospital admission report
 	 -	DAT19_03: Free text document: Transport
 	 -	DAT19_04: Free text document: Cranial CT
	  - DAT19_05: Clinical course
 	 - DAT19_06: Free text document: Discharge report
 	 - DAT19_07: Lab data (LAB)
 	 - DAT19_08: Demographic data (DEMO)
 	 - DAT19_09: Socioeconomic data (SOCIOECONOMICOS)
- OUT19: Table that allows you to compare with the results obtained.



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

C. LABORATORIO:
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



D. FREE TEXT DOCUMENTS


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


### Evaluation Metrics

To assess and validate the effectiveness of the data extraction and analysis process, the following metrics will be used:

-	**Extraction accuracy**: measuring the precision with which AI extracts specific variables from medical reports compared to a reference manual extraction.
-	**Data consistency**: assessing the consistency between the extracted data and the existing database to ensure variables match in terms of definition and format.
-	**Processing time**: measuring the time required to extract and process data compared to traditional manual methods.
-	**Data coverage**: evaluating the proportion of medical reports from which complete and relevant information was successfully extracted.
-	**Impact on clinical research**: analyzing the impact of the extracted data on the quality and depth of clinical analysis, including identifying new patterns or trends in the treatment and outcomes of ischemic stroke patients.
