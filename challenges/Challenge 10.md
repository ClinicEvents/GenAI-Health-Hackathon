# Challenge 10: LLM comparison against ontologies for the patient's safety improvement with medication use


Ontologies are semantic structures used to formally represent and share knowledge about a certain domain. Knowledge modeling of a determined domain is done via the creation of a formal structure that defines concepts, properties and other entities, as well as relationships that exist between them.
Ontologies allow a semantic representation of a determined domain, favoring the domain comprehension, its flexibility and scalability of the system, the interoperability and the reasoning behind the modeled knowledge.

OntoPharma is a support system for clinical decisions, designed, developed and implemented in Hospital Clinic de Barcelona. OntoPharma has as main goal to generate recommendations that help the professional to take clinical decisions in the medication area. To do this, OntoPharma crosses the patient's clinical information with a medication knowledge database based in ontologies.


## Objective

Generate recommendations to help the professional make clinical decisions in the medication area.

## Expected Outcomes

The report must contain the following:

- **Patient ID.**
- **Patient age**
- **Number of alerts generated due to inappropriate prescription**
- **Drug that triggered each alert**
- **Type of alert**. Specify as: exceeds maximum dose, presence of drug interaction, need for dose adjustment according to renal function, previous adverse reaction to the medication, presence of warning signals, high pharmacotherapeutic complexity, high anticholinergic or sedative burden”
- **Description of the reason for the alert**
- **Recommended action** (if applicable)
- **Relevance of the alert** (if applicable)
- **Pharmacotherapeutic complexity calculation** (if applicable)
- **Anticholinergic burden calculation** (if applicable)"


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
 
SAP Dataset Clinic (BASE10)

- Databases used as data sources.
- Agencia Española del Medicamento y Productos Sanitarios' prescription nomenclator (.xml file)
- CatSalut's safety module for electronic receipts (.xlsx file)
- ABX-dosage database's info (.xlsx file)
- Specific population expert panel's info (cronical patient and newborn patient) (.xlsx and pdf files)
- 100 clinical cases that may contain potentially inappropriate prescriptions
- OntoPharma obtained results. Patient's safety results for medication use will previously be obtained from a test environment (SAP-QAS) and reflected in a file to compare them to LLM results.

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

## Evaluation metrics

The LLM delivered results will be evaluated by an expert panel in the medication field. They will be responsible for:
-	Verification of the accuracy and importance of the LLM generated alerts.
-	Comparison of the LLM generated alerts to an ontologies based model in terms of number, typology and clinical relevance for the patient.

## Annex

The alerts that OntoPharma generates are the following:

**Adult patient:**
-	Exceeded daily dose of a medicine alert.
-	Medicine-medicine interaction alert.  
-	Dose adjustment by kidney function alert.
-	Adverse effect prior to a medicine alert (RAM).
-	Adverse effect created by analytical alteration with certain medication presence alert.
-	High anticholinergic load alert. Applies for > 65 years old patients and Drug Burden Index ≥2 tested anticholinergic load.
-	High pharmacotherapy complexity alert. Applies for > 65 years old patients and Medication Regimen Complexity Index ≥40 tested complexity.




