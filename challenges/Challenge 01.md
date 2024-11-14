# Challenge 01: Clinical History of Pain


This challenge focuses on using generative AI models to improve the collection and management of clinical histories during the initial visit and follow-up for patients in the pain unit. Currently, due to limited time for consultations, there is often not enough time to administer validated questionnaires or engage in in-depth discussions with patients. The integration of generative AI could enable more comprehensive and precise data collection, improving both the quality of the first visit and follow-up. It would also facilitate a more reliable and reproducible monitoring of outcomes and allow for the easy generation of documents for both the patient and their clinical history.

## Objective

Generate a report for the patient and other physicians based on previous clinical courses, imaging tests, and neurophysiological assessments. An initial assessment report or, in the case of follow-up visits, an updated clinical course will be generated for the patient, which will then be uploaded back into the SAP system for continued monitoring.


## Expected Outcomes

Pain medical history report must contain the following:

1. Demographic and Socioeconomic Data:
	- Age: Crucial, as age affects pain presentation and management (older adults, children, adolescents).
	- Sex: Influences prevalence and presentation. Record sex assigned at birth and gender.
	- Educational Level/Health Literacy: Impacts understanding of pain and treatment. Evaluate patient’s ability to obtain, process, and understand basic health information.
	- Employment Status: Assess impact on work capacity and the need for accommodations. Record specific occupation.
	- Marital Status/Social Support: Influences support network. Detail family composition and available support.
	- Socioeconomic Level: Affects access to resources. Include information on income, insurance, and barriers to access.
	- Cultural Background/Beliefs about Pain: Influences pain perception and expression. Record ethnicity, religion, and specific beliefs regarding the cause and meaning of pain.

2. Pain Characteristics:
	- Location: Anatomical precision. Use body diagrams. Document if localized or diffuse.
	- Radiation: Pathway. Differentiate between radicular and referred pain.
	- Quality: Sensory description (e.g., stabbing, burning, dull, pressing, electric, lancinating, throbbing, cramp, constant, intermittent).
	- Intensity: Validated scales (e.g., NRS 0-10, Faces Pain Scale). Consider age and cognitive capacity when selecting a scale.
	- Onset: Date, circumstances, precipitating factors.
	- Duration: Acute or chronic. Specify duration in days, weeks, months, or years.
	- Frequency: Continuous, intermittent, episodic. Quantify frequency (e.g., times per day, week, month).
	- Aggravating Factors: Movements, postures, stress, food, weather, etc.
	- Alleviating Factors: Rest, heat, cold, medications, distraction, etc.
	- Associated Symptoms: Nausea, vomiting, dizziness, sleep disturbances, anxiety, depression, fatigue, numbness, tingling, weakness, stiffness, etc. Detail the nature and severity of each symptom.

3. Diagnoses:
	- Primary Diagnoses: Main condition according to IASP and/or ICD-11. Examples:
		- Chronic Primary Pain:
			- Chronic Primary Generalized Pain (e.g., Fibromyalgia)
			- Chronic Primary Localized Pain (e.g., chronic primary headache, chronic primary shoulder pain, chronic primary knee pain, etc.)
			- Chronic Primary Regional Pain (e.g., Complex Regional Pain Syndrome (CRPS))
			- Other Chronic Primary Pain (e.g., chronic primary visceral pain, chronic postoperative pain syndrome)
		- Chronic Secondary Pain:
			- Chronic Cancer-Related Pain (specify cancer type and pain location)
			- Chronic Pain Secondary to Other Conditions:
				- Chronic Neuropathic Pain (e.g., postherpetic neuralgia, painful diabetic neuropathy, trigeminal neuralgia (if due to injury), carpal tunnel syndrome)
				- Chronic Musculoskeletal Pain (e.g., osteoarthritis, rheumatoid arthritis, chronic low back pain, chronic neck pain, myofascial pain syndrome, spondyloarthritis, osteoporosis, fractures)
				- Chronic Visceral Pain (e.g., irritable bowel syndrome, interstitial cystitis, chronic pancreatitis, endometriosis, pelvic inflammatory disease)
				- Chronic Postoperative or Post-Traumatic Pain (specify surgery or trauma)
				- Other Chronic Pain Causes (e.g., infectious diseases (HIV, herpes zoster), vascular diseases (peripheral artery disease), endocrine diseases (hypothyroidism))
			- Chronic Headache or Orofacial Pain:
				- Chronic Migraine
				- Chronic Tension-Type Headache
				- Chronic Trigeminal Neuralgia (if caused by underlying condition)
				- Chronic Cluster Headache
				- Other Chronic Headaches (e.g., chronic paroxysmal hemicrania, occipital neuralgia)
				- Chronic Orofacial Pain (e.g., temporomandibular disorders, burning mouth syndrome, neuropathic orofacial pain)
	- Secondary Diagnoses: Comorbidities that contribute to pain. Examples: Depression, anxiety, sleep disorders, substance abuse, somatoform disorders, comorbid medical conditions (e.g., diabetes, hypertension, heart disease, lung disease, kidney disease, liver disease, arthritis, cancer).
	- Pain Classification (IASP): Nociceptive, neuropathic, nociplastic, mixed. Specify pain pathophysiology. Examples: Somatic nociceptive pain, visceral nociceptive pain, peripheral neuropathic pain, central neuropathic pain, nociplastic pain.
	- Diagnoses according to DSM-5/ICD-11: Include mental or behavioral disorder diagnoses. Examples: Major depressive disorder, generalized anxiety disorder, post-traumatic stress disorder, panic disorder, obsessive-compulsive disorder, substance use disorder, sleep disorders.

4. Treatments:
	- Pharmacological:
		- Non-Opioid Analgesics (NSAIDs): Name, dose, frequency, duration, side effects, interactions.
		- Opioids: Name, dose (in MME - morphine milligram equivalents), frequency, duration, side effects, monitoring plan (e.g., urine tests), addiction risk assessment (using validated tools), opioid use history, informed consent.
		- Adjunctive Agents: Antidepressants (e.g., amitriptyline, duloxetine), anticonvulsants (e.g., gabapentin, pregabalin), muscle relaxants (e.g., cyclobenzaprine, tizanidine), etc. Name, dose, frequency, duration, side effects, interactions.
	- Non-Pharmacological:
		- Physical Therapy: Type (e.g., strengthening exercises, stretching, aerobic exercises, manual therapy), frequency, duration, specific exercises, progress.
		- Occupational Therapy: Home and work adaptations, assistive devices.
		- Psychological Therapy: Type (e.g., cognitive-behavioral therapy (CBT), acceptance and commitment therapy (ACT), mindfulness), frequency, duration, techniques used, progress.
		- Stress Reduction Interventions: Mindfulness, meditation, yoga, tai chi, relaxation techniques.
		- Acupuncture: Type, frequency, points used.
		- Injections: Type (e.g., nerve block, epidural injections, facet injections, trigger point injections), location, medications used, frequency, treatment response.
		- Surgery: Type, date, outcomes.
		- Implantable Devices: Type (e.g., spinal cord stimulator, dorsal root ganglion stimulator), implantation date, programming, effectiveness.
		- TENS/PENS: Stimulation parameters, usage frequency, effectiveness.
		- Self-Care: Patient strategies. Detail activities (e.g., exercise, stretching, heat/cold application, relaxation techniques), frequency, effectiveness.

5. Functional Assessment:
	- Activities of Daily Living (ADL): Standardized scales or questionnaires (e.g., Barthel Index). Specify activities affected.
	- Instrumental Activities of Daily Living (IADL): Standardized scales or questionnaires (e.g., Lawton and Brody Scale). Specify activities affected.
	- Impact on Work, Relationships, and Leisure: Use validated scales (e.g., Brief Pain Inventory - BPI, WHODAS 2.0). Describe specific impact on each area.
	- Functional Assessment Scales: Examples: Oswestry Disability Index (ODI) for low back pain, Roland Morris Disability Questionnaire (RMDQ) for low back pain, McGill Pain Questionnaire (MPQ), Neck Disability Index (NDI) for cervical pain.

6. Medical History:
	- Medical Conditions: Detail diagnoses, treatments, and management. Include information on chronic illnesses such as diabetes, hypertension, heart disease, lung disease, kidney disease, liver disease, autoimmune diseases, neurological disorders.
	- Allergies: Specify allergen and type of allergic reaction.
	- Substance Abuse History: Type of substance, frequency, duration, previous treatments. Use validated screening tools.
	- Psychiatric History: Diagnoses, treatments, current status. Include mood disorders, anxiety disorders, sleep disorders, personality disorders.
	- Surgical History: Type of surgery, date, outcomes, complications.

7. Psychosocial Assessment:
	- Mood: Use validated scales (e.g., HADS, BDI, PHQ-9). Describe the patient's mood (e.g., depressed, anxious, irritable, apathetic).
	- Social Support: Quantify and qualify available social support. Identify support sources (e.g., family, friends, support groups).
	- Coping Strategies: Adaptive and maladaptive. Describe how the patient emotionally manages pain.
	- Treatment Expectations: Realistic vs. unrealistic. Negotiate therapeutic goals.
	- Beliefs about Pain (Catastrophizing, Kinesiophobia, etc.): Use specific questionnaires (e.g., Pain Catastrophizing Scale - PCS, Tampa Scale of Kinesiophobia - TSK).
	- Impact of Pain on Quality of Life: Use validated scales (e.g., SF-36, EQ-5D). Describe how pain affects different quality of life areas (e.g., physical, emotional, social).

8. Other:
	- Laboratory Tests: Include values, dates, and type of test (e.g., complete blood count, erythrocyte sedimentation rate, C-reactive protein).
	- Imaging Studies: Include reports, dates, and type of study (e.g., X-rays, MRI, CT scan).
	- Electromyography (EMG) / Nerve Conduction Studies: Include reports and dates.
	- Red Flags: Urgent medical evaluation signs (e.g., fever, unexplained weight loss, severe nighttime pain, progressive neurological symptoms).
	- Yellow Flags: Psychosocial factors increasing chronic pain risk (e.g., catastrophizing, kinesiophobia, negative pain beliefs, low mood, stress).
	- Blue Flags: Perceptions about the relationship between work and health that may affect recovery (e.g., belief that work is harmful, low job satisfaction, workplace conflicts).
	- Black Flags: Work-related obstacles that may affect recovery (e.g., company policies, workers' compensation, lack of employer support).
	- Orange Flags: Signs of psychopathology (e.g., depression symptoms, anxiety, PTSD).




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
- [BASE01](https://us-west-2.console.aws.amazon.com/s3/buckets/data-clinic-hackathon-2024?region=us-west-2&bucketType=general&prefix=BASE01/&showversions=false) contains:
	- DAT01_01: Free text document: Initial valuation
	- DAT01_02: Free text document: Evolution
	- DAT01_03: Demographic data (DEMO)
	- DAT01_04: Socioeconomic data (SOCIOECONOMICOS)



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
