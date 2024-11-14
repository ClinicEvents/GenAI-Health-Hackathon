# Challenge 24: Optimizing Psychiatric Diagnosis and Patient Profiling through AI-Driven Textual Data Extraction and Analysis

Psychiatry faces unique diagnostic challenges, as it relies primarily on subjective data—such as self-reported symptoms and clinical observations—without the objective biomarkers commonly available in other medical fields. Diagnosis and treatment in psychiatry are shaped by multiple interconnected factors, including symptom patterns, genetic predispositions, personal medical history, and responses to previous treatments. Despite the wealth of patient information recorded in clinical settings, much of this data remains unstructured and fragmented, making comprehensive analysis difficult. Integrating these data sources is essential for advancing psychiatry, enabling precise patient profiling, and supporting personalized treatment strategies. Challenge 24 addresses these needs by developing AI-driven systems to systematically extract, organize, and analyze psychiatric data, fostering evidence-based, holistic mental health care.

## Objective

Develop automated systems to extract relevant psychiatric information from unstructured text and organize it into structured datasets.
- Automatically capture sociodemographic data (e.g., gender, age, education level, socioeconomic status, occupation), anthropometric data (e.g., weight, height, BMI), pharmacological treatments (e.g., type, dosage), specific psychiatric diagnoses (e.g., bipolar disorder, schizophrenia, depression), psychiatric symptoms (e.g., insomnia, irritability, anxiety), non-psychiatric comorbidities, personality profiles, clinical specifiers (e.g., rapid cycling, seasonality), and other clinical data.
- Extract data from structured sources (e.g., blood and urine tests) and unstructured data from reports of complementary exams (e.g., neuropsychological assessments, psychometric tests, neuroimaging).

Improvement 1: Identify specific patient profiles based on the extracted data. Use accurate diagnostic, symptomatic, and supplementary data to define patient profiles for applications such as identifying clinical trial candidates, tailoring treatment recommendations, and identifying additional test needs. These systems will enable clinicians to understand patient information holistically and make more informed decisions.

NOTE: More details in Annex A





## Expected Outcomes

### Input 

Text: IR_PSI_CLIN - Neuropsychology and psychometrics reports

Resumen clínico / Resum Clínic 

Paciente varón de 45 años de edad remitido para valoración neuropsicológica en el contexto de participación en un estudio de investigación dentro del Programa de Trastornos Bipolares. Diagnosticado de trastorno bipolar.

Puntuaciones

WAIS-III (puntuaciones escalares):
Vocabulario: 12. Clave números: 09. Búsqueda símbolos: 08. Aritmética: 10. Dígitos: 10. Letras y números: 9.
Estimación CI: 110.
Índice CI velocidad de procesamiento: 92.
Índice CI memoria de trabajo: 96. 
CVLT (puntuaciones tipificadas z):
Curva de aprendizaje: 05-07-06-08-08. Total: 34.
Recuerdo libre inmediato: -2. Recuerdo guiado inmediato: -1 Recuerdo libre demorado: -2. Recuerdo guiado demorado: -2. Reconocimiento: 0. 
Figura compleja de Taylor (puntuaciones típicas): Planificación: 40. Memoria: 23. 
TMT (puntuaciones típicas): TMT-A: 47. TMT-B: 50. 
WCST (puntuaciones directas): Categorías: 5. Errores perseverativos: 17. 
SCWT (puntuación típica): Interferencia: 43 
FLUENCIAS (puntuaciones directas): 
PMR: 28. Categoría animales: 21. 
CPT-II (puntuaciones típicas):
Errores omisión: 111,87. Errores comisión: 60,92. TR: 63,09. TR cambio bloque: 65,54. TR error estandar: 98,01. d': 58,31. ß: 49,71. TR ISI change: 57,69. 

Conclusiones / Conclusions 

Los resultados de la exploración neuropsicológica indican, dentro de un contexto de un nivel intelectual normal, que el paciente presenta importantes dificultades en capacidad mnésica y en atención sostenida. Permanece conservado el rendimiento en el resto de funciones cognitivas evaluadas. En comparación con la anterior valoración (Mayo 2019), se evidencia mejora clínicamente significativa en cálculo mental, funciones ejecutivas y en reconocimiento en recuerdo verbal. 

### Output

```json
{
  "Resumen_clinico": {
    "Paciente": {
      "Sexo": "Masculino",
      "Edad": 45
    },
    "Motivo_exploracion": "Participación en estudio de investigación dentro del Programa de Trastornos Bipolares",
    "Diagnostico": "Trastorno bipolar",
  },
  "Puntuaciones": {
    "WAIS-III": {
      "Vocabulario": 12,
      "Clave_numeros": 9,
      "Busqueda_simbolos": 8,
      "Aritmetica": 10,
      "Digitos": 10,
      "Letras_numeros": 9,
      "Estimacion_CI": 110,
      "Indice_CI_velocidad_procesamiento": 92,
      "Indice_CI_memoria_trabajo": 96
    },
    "CVLT": {
      "Curva_aprendizaje": [5, 7, 6, 8, 8],
      "Total": 34,
      "Recuerdo_libre_inmediato": -2,
      "Recuerdo_guiado_inmediato": -1,
      "Recuerdo_libre_demorado": -2,
      "Recuerdo_guiado_demorado": -2,
      "Reconocimiento": 0
    },
    "Figura_Taylor": {
      "Planificacion": 40,
      "Memoria": 23
    },
    "TMT": {
      "TMT-A": 47,
      "TMT-B": 50
    },
    "WCST": {
      "Categorias": 5,
      "Errores_perseverativos": 17
    },
    "SCWT": {
      "Interferencia": 43
    },
    "Fluencias": {
      "PMR": 28,
      "Categoria_animales": 21
    },
    "CPT-II": {
      "Errores_omision": 111.87,
      "Errores_comision": 60.92,
      "TR": 63.09,
      "TR_cambio_bloque": 65.54,
      "TR_error_estandar": 98.01,
      "d'": 58.31,
      "ß": 49.71,
      "TR_ISI_change": 57.69
    }
  }
  "Conclusiones": {
    "Resumen": "Dificultades importantes en capacidad mnéstica y atención sostenida",
    "Nivel_intelectual": "Normal",
    "Rendimiento_funciones_cognitivas_restantes": "Conservado",
    "Comparacion_anterior": "Mejora en cálculo mental, funciones ejecutivas y reconocimiento en recuerdo verbal"
  },
}
```

NOTE 1: More examples in Annex B


**NOTE 2: Your mentor will provide you with more details on the expected outcome for Improvement 1.**

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
- BASE24. Contains:
	- DAT24_01: Free text document: Discharge report
	- DAT24_02: Free text document: Emergency discharge report
	- DAT24_03: Free text document: Evolution report
	- DAT24_04: Free text document: Neuropsychologycal report, psychometry
	- DAT24_05: Free text document: TEC report
	- DAT24_06: Free text document: Neuropicture
	- DAT24_07: Lab data (LAB)
	- DAT24_08: Demographic data (DEMO)
	- DAT24_09: Socioeconomic data (SOCIOECONOMICOS)


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

{challenge_number }_{challenge_identifier_number} _{report_type } _{id_patient_pseu} _{creation_date} _{counter}.txt

For example:
01_02_INF_VAL_INI_407789453_20211119_29.txt
-	Challenge: 01
-	Challenge identifier number: 02
-	Report type: INF_VAL_INI
-	Id_patient_pseu: 407789453
-	Creation date (YYYYMMDD): 20211119
-	Counter: 29

Source: Electronic Health Records (EHR) from Hospital Clínic de Barcelona – SAP Program.
-	Textual information: Clinical courses and reports.
-	ICD-10 diagnostic codes

### Data Preparation Process

- Data Extraction: Data will be sourced from the Electronic Health Records (EHR) at Hospital Clínic de Barcelona – SAP Program. The textual data will include patients’ clinical courses and reports, along with coded diagnostic information (ICD-10).
- Data Cleaning: The data will be cleaned to remove errors, inconsistencies, and irrelevant information.
- Annotation Requirement: Annotation will ensure each patient is assigned a diagnostic code, prioritizing the most relevant code in cases of multiple diagnoses. Annotation will also enable accurate symptom identification by the model.
- Anonymization: Anonymization techniques, such as pseudonymization and removal of personally identifiable information, will ensure patient privacy and compliance with data protection regulations.
- Integration: Data from various sources will be integrated into a unified format to ensure compatibility and coherence for analysis.

### Output Database

The output database should consist of structured tabular data for each document in an Excel format.
-	Document Organization: Each patient may have multiple associated documents. For the second objective (identification of patient profiles), data extracted from each document related to a single patient should be consolidated into a single file, using an id_patient identifier to merge information across documents.
-	Example of Output Data Structure:
	- Patient ID (id_patient): Unique identifier to link all related data for a single patient.
	- Document Type: Specifies the type of document (e.g., Clinical Course Report, Neuropsychology Report).
	- Extraction Timestamp: Records the date and time of data extraction to capture temporal changes in patient data.
	- Data Fields: Includes all extracted fields (e.g., diagnoses, treatments, symptoms, lab results), organized under specific headings (e.g., sociodemographic, psychiatric history, symptoms, medication, lab findings).
Each Excel sheet entry should represent a document related to a patient, with fields standardized across documents to ensure compatibility for analysis.



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

The evaluation of Challenge 24’s AI-driven data extraction and patient profiling system will be based on its effectiveness in accurately extracting, structuring, and categorizing psychiatric data from clinical records. Given the complexity and variability in psychiatric data, the following metrics have been defined to ensure that both the accuracy and completeness of the model's outputs are rigorously assessed.

Objective 1: Structured Data Extraction
1.	Entity Recognition Accuracy: Measures the model's ability to identify key entities (e.g., diagnoses, symptoms, medications). Metric: Percentage of correctly identified entities.
2.	Entity Classification Accuracy: Evaluates whether the model categorizes extracted entities correctly (e.g., distinguishing symptoms from diagnoses or treatments). Metric: Percentage of entities accurately classified.
3.	Attribute Extraction Completeness: Checks if all relevant details for each entity are extracted (e.g., medication dosage, symptom severity). Metric: Completeness rate of extracted attributes.
4.	Relation Extraction Accuracy: Assesses the accuracy in identifying relationships between entities (e.g., linking treatments to specific diagnoses). Metric: Percentage of correct relationships captured.
5.	Adherence to JSON Format: Ensures the output matches the predefined JSON structure, including correct fields and nesting. Metric: Rate of format compliance.
6.	Free-Text Handling Accuracy: Evaluates the effectiveness in capturing and structuring relevant free-text data. Metric: Percentage of free-text data accurately extracted.
7.	Sensitivity (Recall), Precision, and F1 Score: Measures overall extraction accuracy and completeness.
- Recall: Percentage of all relevant entities captured.
- Precision: Accuracy of each extracted entity.
- F1 Score: Balanced measure of recall and precision.

Objective 2: Patient Profile Identification and Integration
1.	Data Consistency Across Documents: Measures consistency in data extraction across multiple documents for the same patient. Metric: Consistency rate for repeated data points.
2.	Temporal Accuracy: Assesses the accuracy in sequencing time-dependent data (e.g., symptom progression). Metric: Rate of correct temporal sequencing.
3.	Profile Completeness: Checks how well the model consolidates data into comprehensive patient profiles by integrating all relevant data sources. Metric: Completeness rate for required profile elements.
4.	Patient Profile Classification Accuracy: Measures accuracy in assigning patients to specific profiles based on criteria (e.g., diagnosis + treatment history). Metric: Rate of correctly classified profiles.
5.	Inter-Rater Agreement for Manual Validation: Assesses consistency among expert reviewers in manual validation. Metric: Agreement score (e.g., Cohen’s Kappa).



## Annex A

The unstructured free-text data has been extracted from electronic health records from the Hospital Clinic of Barcelona, all of which have been anonymized to ensure patient privacy.

- **Main objective**. Information will be extracted, and the output should be a list of JSON objects following a predefined format by challenge members. Each examination should generate a single JSON object. The format will vary across documents due to the different types of information they contain. Note that while a vast amount of psychiatric information exists, only a subset is present in most records. For example, although over 100 psychiatric symptoms are known, fewer than 20 are typically documented for a given patient.

- **Improvement 1**. The second objective focuses on integrating information from various reports and creating patient profiles based on the comprehensive data. This involves merging extracted data from all available sources, such as clinical courses, neuropsychological assessments, and imaging results, into a cohesive view of each patient’s psychiatric history. Each patient is assigned a unique identifier, and timestamps are used to track data variations over time. Once consolidated, this dataset is analyzed to identify characteristic profiles based on shared diagnostic, symptomatic, and treatment patterns.
	- Data Merging: Consolidate all data related to a single patient across various sources, ensuring data from different reports is accurately associated with the correct patient identifier. Each entry includes a timestamp to account for changes over time.
	- Patient Profiling: Develop a set of profiles that represent different patient archetypes based on conditions, treatment history, and observed outcomes. Profiles are created in order of complexity, starting from basic diagnostic categories and advancing to profiles that consider combinations of specific treatments, cognitive impairments, and other clinical markers.
	- Algorithm Application: Machine learning or rule-based algorithms are used to categorize patients into profiles based on predefined criteria, such as diagnosis, lifetime treatment history, cognitive assessments, and other clinical data points. Profiles may include:
		- Profile 1: Bipolar disorder.
		- Profile 1.1: Bipolar disorder + lifetime lithium treatment.
		- Profile 1.2: Bipolar disorder + lifetime lithium treatment + cognitive impairment.
		- Profile 1.3: Profile 1.2 + lithium levels > 0.7 mEq/L for >1 year.
		- Profile 1.4: Profile 1.3 + 2+ hospital admissions.
		- Profile 1.5: Profile 1.4 + history of ECT.
		- Profile 1.6: Profile 1.5 + age >55 years.
		- Profile 1.7: Profile 1.6 + brain imaging abnormalities (CT/MRI).
	Each profile builds on the previous one, gradually incorporating more detailed clinical markers. This layered approach allows for nuanced categorization, helping clinicians distinguish between patients 	with varying levels of complexity and care needs. This structured profiling enhances the potential for personalized treatment, targeted clinical recommendations, and advanced understanding of complex 	psychiatric cases.

	- Validation: To ensure reliability, each profile is evaluated and refined based on real-world outcomes, with further validation provided by clinical experts.


Hardware and Software Requirements: High-performance servers and specialized software may be required to handle large-scale data processing and support advanced AI models.

Ethical Constraints: Compliance with all current ethical and privacy regulations is essential, ensuring the protection of patient rights at all times.

## Annex B

**Example: Text form (CUR_CLI - Clinical course report)**

PSICOBIOGRAFÍA: Hombre de 45 años. Independiente para las actividades de la vida diaria Divorciado en noviembre de 2017. Vive con familiares. No tiene hijos. Se dedica a la publicidad (agencia propia). Estudiois de periodismo. Buen soporte familiar. Adecuado círculo sociofamiliar.

ANTECEDENTES SOMÁTICO-QUIRÚRGICOS: Niega AMC o antecedentes somático-qx de interés. .
ANTECEDENTES PSIQUIÁTRICOS FAMILIARES:
- Madre con episodios depresivos. Se desconocen otros.

ANTECEDENTES PERSONALES PSIQUIÁTRICOS:
- Primer ingreso en Psiquiatría de 1 días de duración, en el circuito privado, a los 33 años aproximadamente por "depresión engógena". Niega ritmicidad circadiana, niega pérdida de apetito/peso. Seguimiento posterior con el Dr. Serrat. Posterior tractament farmacològic (sospita clomipramina + BZD).
- Segundo ingreso en 2016 por "trastorno depersivo mayor", también el circuito provado por clínica depresiva, iba por la noche y le realizabansueroterapian con clomipramina durante 8 días, sin clara mejoría. - Posteriormente cambia seguimiento con el Dr. Lopez en el ámbito privado y realiza tratamiento con paroxetina + BZD. - Ingreso en HSJDD-Numancia en 08/2018 durante 13 días por un episodio maníaco con síntomas psicóticos (ideación megalomaníaca). 

HABITOS TÓXICOS:
- Tabaquismo activo
- Xantinas: en deteriminados momentos hasta 7 cafés/día
- Alcohol: esporádico
- Cocaína: ocasional en el pasado.
- Niega otros hábitos tóxicos

EXPLORACIÓN PSICOPATOLÓGICA: Vigil y orientado. Cierta disprosexia. Contacto sintónico. Cierta irritabilidad. Discurso fluido y coherente, sin verborrean ni clínica psicótica. Realiza crítica de los síntomas del episodio (hipo)maníaco. Sin déficits cognitivos aparentes. Eutimia, humor reactivo. No otra clínica maniforme ni depresiva. Sueño y orexia preservados. Insight parcial. Juicio crítico preservado.

MEDICACIÓN ACTUAL:
- Olanzapina 10 mg 0-0-1
- Litio 400 mg 1-0-1 y 1/2
- Clonazepam 0,5 mg puntual para acatisia.

JSON Structured Form

```json
{
    "psicobiografia": {
        "sexo": "Hombre",
        "edad": 45,
        "estado_civil": "Divorciado",
        "hijos": "No tiene",
        "convivencia": "Vive con familiares",
        "ocupacion": "Publicidad (agencia propia)",
        "estudios": "Periodismo",
        "soporte_sociofamiliar": "Buen soporte familiar y círculo sociofamiliar adecuado"
    },
    "antecedentes": {
        "somatico_quirurgicos": "Niega AMC o antecedentes somático-quirúrgicos de interés",
        "psiquiatricos_familiares": {
            "madre": "Episodios depresivos"
        },
        "personales_psiquiatricos": [
		{
  
                "evento": "Primer ingreso en psiquiatría",
                "edad": 33,
                "duracion": "1 día",
                "diagnostico": "Depresión endógena",
                "tratamiento": "Clomipramina + BZD",
            },
            {
                "evento": "Segundo ingreso en 2016",
                "diagnostico": "Trastorno depresivo mayor",
                "duracion": "8 días",
                "tratamiento": "Suero terapia con clomipramina",
            },
            {
                "evento": "Ingreso en HSJDD-Numancia",
                "fecha": "08/2018",
                "duracion": "13 días",
                "diagnostico": "Episodio maníaco con síntomas psicóticos",
                "sintomas_psicoticos": "Ideación megalomaníaca"
            }
        ]
    },
    "habitos_toxicos": {
        "tabaquismo": "Activo",
        "xantinas": "Hasta 7 cafés al día en momentos específicos",
        "alcohol": "Esporádico",
        "cocaina": "Consumo ocasional en el pasado",
        "otros": "Niega otros hábitos tóxicos"
    },
    "exploracion_psicopatologica": {
        "conciencia": "Vigil",
        "orientación": "adecuada",
        "atención": "Cierta disprosexia",
        "contacto": "Sintónico",
        "irritabilidad": "leve",
        "discurso": "Fluido y coherente, sin verborrea ni clínica psicótica",
        "cognicion":"Sin déficits cognitivos aparentes",
        "estado_animo": "Eutimia, humor reactivo",
        "sintomas_maniacos": "Ausente",
        "sintomas_depresivos": "Ausente",
        "sueño": "Preservado",
        "orexia": "Preservada",
        "insight": "Parcial",
        "juicio_critico": "Preservado"
    },
    "medicacion_actual": [
        {
            "nombre": "Olanzapina",
            "dosis": "10 mg",
            "frecuencia": "0-0-1"
        },
        {
            "nombre": "Litio",
            "dosis": "400 mg",
            "frecuencia": "1-0-1 y 1/2"
        },
        {
            "nombre": "Clonazepam",
            "dosis": "0.5 mg",
            "frecuencia": "Puntual para acatisia"
        }
    ]
}
```





