# Challenge 32: Optimizing Precision Oncology in the Clinic Comprehensive Cancer Center with Generative AI (OPERA Project)


This project aims to improve the decision-making process for patients with advanced solid tumors before starting systemic therapy. It addresses various challenges that combine the integration of clinical, biological, pathological, and molecular data with alignment to European guidelines and connection to clinical trial networks. 

The first challenge involves creating a comprehensive summary of information extracted from the SAP system, consolidating all relevant data for patients with solid tumors. This information will enable oncologists to perform a more accurate and efficient initial assessment.

Secondly, the project seeks to ensure that this process aligns with European clinical guidelines, allowing oncologists to make therapeutic decisions in accordance with established best practices. Additionally, the project aims to facilitate the identification of patients eligible for clinical trials by creating a direct link between patient information and available clinical trial networks, thus improving access to new treatment options.

Finally, the project explores the development of a scoring model to help clinicians optimize initial decision-making in precision medicine. This model will use advanced analytical tools to suggest therapeutic strategies tailored to individual patient profiles, facilitating personalized treatment. The project is complemented by a Q&A tool that allows users to consult clinical guidelines in natural language, helping clinicians query optimal management based on patient data and available guidelines.



## Objective

The clinical guidelines Q&A aims to ensure that this process aligns with European clinical guidelines, enabling oncologists to make therapeutic decisions in accordance with established best practices.

## Expected Outcomes
To be agreed with the mentor.

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
    - DEMO_RAG_with_Kendra
    - DEMO_download_studies_and_upload_to_s3
    - DEMO_s3_read_file
    - DEMO_s3_write_file


**All development must be carried out using the services available on AWS. Moving information outside of the specified tools is NOT allowed.**

Below are details of the most relevant aspects of the tools available to participants.

### Database

The databases that make up this challenge are:

- [BASE30](https://us-west-2.console.aws.amazon.com/s3/buckets/data-clinic-hackathon-2024?region=us-west-2&bucketType=general&prefix=BASE30/&showversions=false) contains:
  -	DAT30_01: Clinical course
  -	DAT30_02: Demographic data (DEMO)
  -	DAT30_03: Socioeconomic data (SOCIOECONOMICOS)
- OUT30: Table that allows you to compare with the results obtained.


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

**NOTE:** If a patient is not found in the databases, the k-anonimization has deleted it.

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

{challenge_number} _{challenge_identifier_number} _{report_type} _{id_patient_pseu} _{creation_date} _{counter}.txt

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

| Criterion      | Excellent | Adequate | Needs Improvement | Poor |
| ----------- | ----------- | ----------- | ----------- | ----------- |
| Clinical Accuracy      | All information is accurate and clinically relevant.     | Most information is accurate, with minor omissions.     | Several inaccuracies affecting interpretation.     | Incorrect or confusing information, compromising utility. |
| Completeness       | Includes all relevant patient data.     | Includes key data, missing some secondary details.     | Incomplete information, missing critical details.     | Insufficient information for an adequate clinical assessment. |
| Language Clarity       | Language is clear and understandable for any medical reader.     | Understandable, but with some ambiguous terms.     | Several ambiguous terms or clarity issues.     | Confusing language that impedes understanding. |
| Information Relevance       | All information is relevant for diagnosis and treatment.     | Mostly relevant, with some marginal data.     | Partially relevant or disorganized information.     | Irrelevant or disorganized information that confuses. |







