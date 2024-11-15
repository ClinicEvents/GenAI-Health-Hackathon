# Challenge 23: Diagnostic Management of Infection in Febrile Neutropenia Patients


The low positivity rates observed in certain microbiological diagnostic tests for febrile neutropenia highlight the need for cost-effective diagnostic management. Using a dataset of all our neutropenic patients with malignant hematologic disorders, generative AI could assist in developing a diagnostic protocol with prioritized and targeted diagnostic testing to maximize cost-efficiency in infection diagnosis, focusing tests based on the etiological suspicion of bacterial, viral, or fungal infections.

Population: Hematologic patients with febrile neutropenia

Involved Specialties: Infectious diseases, hematology, microbiology

The methodology employed to address this challenge could lead to more efficient use of diagnostic testing in various pathologies.


## Objective

To develop an AI model with a diagnostic protocol that prioritizes and limits diagnostic testing to achieve maximum cost-efficiency in infection diagnosis, based on the suspicion of bacterial, viral, or fungal infection, using a dataset of neutropenic patients with malignant hematologic conditions.

## Expected Outcomes

### Input

Predict the likelihood of each microorganism infection category: bacterial, viral, and fungal. The likelihood for each category should be represented as a floating-point value within the range of 0.0 to 1.0, inclusive, where 0.0 indicates very unlikely and 1.0 indicates very likely.

### Output

```json
{ 
"results": [ 
    { 
    "microorganism_type": "viral", 
    "probability": 0.7
    }, 
    { 
    "microorganism_type": "bacterial", 
    "probability": 0.4
    }, 
    { 
    "microorganism_type": "fungal", 
    "probability": 0.1 
    } 
] 
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

- [BASE23](https://us-west-2.console.aws.amazon.com/s3/buckets/data-clinic-hackathon-2024?region=us-west-2&bucketType=general&prefix=BASE23/&showversions=false) contains:
 	 -	DAT23_01: Free text document: Admission reports
 	 -	DAT23_02: Laboratory data (LAB)
 	 -	DAT23_03: Demographic data (DEMO)
 	 -	DAT23_04: Socioeconomic data (SOCIOECONOMICOS)
- OUT23: Table that allows you to compare with the results obtained.




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




D. Output 

| Variable name      | Description |
| ----------- | ----------- |
| pid      | Patient's unique identificator    |
| sex      | Patient's sex, registered as a categorical value    |
| birth_date      | Patient's birth date    |
| exitus_30d      | Death indicator in the following 30 days to the febrile neutropenia (1 for death, 0 for no death)    |
| exitus_60d      | Death indicator in the following 60 days to the febrile neutropenia (1 for death, 0 for no death)    |
| exitus_date      | Patient's death date    |
| nf_start_date      | Start date for the febrile neutropenia episode  |
| nf_end_date      | End date for the febrile neutropenia episode    |
| outcome_bact_pos      | Indicates if the patient has a positive diagnostic sample for bacteria infection during the febrile neutropenia episode     |
| outcome_virus_pos      | Indicates if the patient has a positive diagnostic sample for viral infection during the febrile neutropenia episode    |
| outcome_fungi_pos      | Indicates if the patient has a positive diagnostic sample for fungal infection during the febrile neutropenia episode    |


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

Sensitivity, Specificity, Positive Predictive Value (PPV), Negative Predictive Value (NPV), Accuracy, F1 Score, AUC-ROC.

## Annex

We have a comprehensive, refined dataset that includes all febrile neutropenia patients, with 4,520 microbiological tests conducted and their results (10% positivity rate), corresponding to 462 episodes of febrile neutropenia in patients with malignant hematologic conditions treated at the hospital from January 2020 to July 2022. This dataset serves as a solid foundation to develop an optimized diagnostic protocol with the support of generative artificial intelligence, prioritizing and limiting diagnostic tests to maximize cost-efficiency in infection detection, based on the etiological suspicion of bacterial, viral, or fungal infection.

**Pathogen and Clinical Sample Classification**
**Bacterial Pathogens**
- Blood Cultures: blood samples used for blood cultures to detect systemic bacterial infections.
Respiratory Tract: includes sputum, bronchoalveolar lavage fluid (BAL), tracheal aspirate, pleural fluid, and nasopharyngeal swab samples. These samples are used to detect bacterial infections in the lower and upper respiratory tract. Specific microorganisms in BAL: Chlamydia pneumoniae, Legionella pneumophila, Mycoplasma pneumoniae.
- Cerebrospinal Fluid: enables detection of microorganisms such as Escherichia coli K1, Haemophilus influenzae, Listeria monocytogenes, Neisseria meningitidis, Streptococcus agalactiae, and Streptococcus pneumoniae.
- Stool: stool samples used for the detection of Campylobacter spp., Salmonella spp., and Shigella spp. / Enteroinvasive E. coli.
- Urine: includes clean-catch and catheterized urine samples.
- Other: includes intra-abdominal fluids, such as peritoneal fluid and biliary tract fluid.
- 
**Viral Pathogens**

- Respiratory Tract: includes bronchoalveolar lavage fluid (BAL) and nasopharyngeal swab samples for detecting respiratory viruses such as adenovirus, coronavirus, SARS-CoV-2, enterovirus, human bocavirus, metapneumovirus, influenza A (H1N12009 and H3N2), influenza A, B, and C, parainfluenza virus (1-4), respiratory syncytial virus, and rhinovirus.
- Cerebrospinal Fluid: enables detection of cytomegalovirus, enterovirus, herpes simplex virus 1 and 2, human herpesvirus 6, human parechovirus, and varicella-zoster virus.
- Stool: detects adenovirus group F (serotypes 40 and 41), norovirus (genotypes G1 and G2), and rotavirus group A.
- Plasma: detects adenovirus, BK virus, cytomegalovirus, Epstein-Barr virus, herpes simplex virus type 1 and 2, human herpesvirus 6, and parvovirus B19 via Rt-PCR.

**Fungal Pathogens**

- Serum: includes fungi such as Pneumocystis jirovecii, Candida spp., Fusarium spp., Histoplasma spp., Cryptococcus neoformans, and Aspergillus fumigatus, detected by 1,3-√ü-D-glucan, cryptococcal antigen, and galactomannan antigen tests.
- Cerebrospinal Fluid: enables detection of Cryptococcus neoformans/gattii.

