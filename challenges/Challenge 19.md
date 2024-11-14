# Challenge 19: AI implementation for personal therapeutic advise for stroke patients


The project aims to produce AI generated advise and evaluation for stroke patients through interactive visualizations like dashboards and KPI(Key Performance Indicators).
This challenge focuses stroke patients, but it can be extrapolated to any illness or specialty.
The target population includes patients that have been released after an hospital stay caused by an stroke. These patients can have additional diagnostics like high blood pressure, diabetes and dyslipidemia, and the project will focus on customizing the therapeutic advise for these specific cases.

This challenge has potential to transform the way therapeutic advises are made, using AI to improve accuracy and efficiency in clinical data evaluation and the generation of clinical guides and internal protocols based recommendations. Furthermore, interactive visualization will ease the comprehension and implementation of the recommendations, helping to improve the clinical results and patient's prognosis.



## Objective

Use AI to analyze the release reports of stroke patients and their complementary studies (blood and image testing), to provide individual therapeutic recommendations based on clinical guides and Stroke Unit's internal protocols.

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
- [BASE19](https://us-west-2.console.aws.amazon.com/s3/buckets/data-clinic-hackathon-2024?region=us-west-2&bucketType=general&prefix=BASE19/&showversions=false) contains:
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
| Natio      | place of residence, ES: Spanish, OT: Other     |
| Idiom      | Patient's language, ES: Spanish, OT: Other    |
| Health_area      | Health area       |
| Employment_situation*      | Employment status       |
| Contact*      | Contact person     |
| id_patient_pseu      | Patient identification number that links the patients between tables      |

*NOTE: Check Dictionaries file for the description of the value

B. SOCIECONOMICOS

| Name      | Description |
| ----------- | ----------- |
| register_date      | Register date     |
| register_time      | Register time     |
| situ_lab*      | Employment status     |
| vive_con*      | Co-habitation status. Alone, with family, shared home.   |
| cuida_nomb      | Name of the care giver       |
| id_patient_pseu      | Patient identification number that links the patients between tables       |

*NOTE: Check Dictionaries file for the description of the value

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

**NOTE:** If a patient is not found in the databases, the k-anonimization has deleted it.

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
## Evaluation Metrics

-	**Data Extraction Accuracy**: measuring the accuracy with which AI extracts relevant information from hospital discharge reports compared to a manual reference extraction.
-	**Consistency of recommendations**: assessing the agreement between AI-generated recommendations and clinical guidelines/internal protocols.
-	**Processing time**: measuring the time needed to extract, process, and analyze data, compared to traditional manual methods.
-	**Impact on clinical decision-making**: analyzing the impact of AI-generated recommendations on therapeutic decisions and the improvement of patients' clinical outcomes.
-	**Visualization usability**: assessing the usability and comprehensibility of dashboards and KPIs for medical staff through surveys and direct feedback.
