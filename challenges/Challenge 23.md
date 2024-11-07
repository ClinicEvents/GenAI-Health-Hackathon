# Challenge 23: Diagnostic Management of Infection in Febrile Neutropenia Patients


The low positivity rates observed in certain microbiological diagnostic tests for febrile neutropenia highlight the need for cost-effective diagnostic management. Using a dataset of all our neutropenic patients with malignant hematologic disorders, generative AI could assist in developing a diagnostic protocol with prioritized and targeted diagnostic testing to maximize cost-efficiency in infection diagnosis, focusing tests based on the etiological suspicion of bacterial, viral, or fungal infections.
Population: Hematologic patients with febrile neutropenia
Involved Specialties: Infectious diseases, hematology, microbiology

The methodology employed to address this challenge could lead to more efficient use of diagnostic testing in various pathologies.


## Objective

To develop an AI model with a diagnostic protocol that prioritizes and limits diagnostic testing to achieve maximum cost-efficiency in infection diagnosis, based on the suspicion of bacterial, viral, or fungal infection, using a dataset of neutropenic patients with malignant hematologic conditions.


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
1.	BASE23. Contains:
 	 -	DAT23_01: Free text document: Admission reports
 	 -	DAT23_02: Laboratory data (LAB)
 	 -	DAT23_03: Demographic data (DEMO)
 	 -	DAT23_04: Socioeconomic data (SOCIOECONOMICOS)
2.	OUT23 (Write-only backup where the challenge results will be stored).



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

## Evaluation Metrics

Sensitivity, Specificity, Positive Predictive Value (PPV), Negative Predictive Value (NPV), Accuracy, F1 Score, AUC-ROC.

## Output database

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

