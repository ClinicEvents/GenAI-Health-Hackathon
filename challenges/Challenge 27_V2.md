# Challenge 27: Evaluation of LLM Performance in Assessing the Appropriateness of Outpatient Colonoscopy Requests According to Current Guidelines


The digestive endoscopy unit receives an increasing number of outpatient colonoscopy requests each year. Many of these requests are either not correctly indicated, or their prioritization does not align with current recommendations. This growing volume exceeds the unit's operational capacity, leading to extended waitlist times for all patients.
To address this, the proposed challenge aims to individually evaluate outpatient colonoscopy requests, prioritizing or rejecting procedures based on their indications according to the latest clinical guidelines. Currently, requests are received daily in free-text format, and manual evaluation by clinical staff is time-consuming. Automating the process of reading, interpreting, and processing outpatient colonoscopy requests using LLMs (Large Language Models) could streamline this workflow.
Since LLMs are not specifically trained on endoscopy data and may not reflect the latest guidelines, Retrieval-Augmented Generation (RAG) approach could be used to provide the necessary context. 

## Objective

The goal is to create an automated process to read, interpret, and evaluate outpatient colonoscopy requests in free-text format. The system will prioritize or reject procedures based on current clinical guidelines and recommendations.

## Expected Outcomes
The model should be able to determine the values ​​in the output table (output base).



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
- BASE21. Contains:
 	 -	DAT21_01: Free text document: Endoscopy report
 	 -	DAT21_02: Free text document: Endoscopy exploration petitions
 	 -	DAT21_03: Demographic data (DEMO)
 	 -	DAT21_04: Socioeconomic data (SOCIOECONOMICOS)
-OUT21: Table ground truth


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

The model should output the following fields in a tabular format for each request, along with any additional fields specified by the challenge members:
| Name      | Description |
| ----------- | ----------- |
|date_solicitud| date of request (yyyy/mm/dd)|
|id_patient_pseu| patient identifier|
|date_pref| date of preference of the colonoscopy (yyyy/mm/dd)|
|origin| department requesting the colonoscopy|
|zona| area in the city from which the request is made|
|acceptacio| wether the colonoscopy request was accepted (1) or rejected (0)|
|priorization| priorization level of accepted colonoscopies (1 to 5)|
|rebuig| rejection reason of rejected colonoscopies (1 to 7)|
|acceptacio_val| wether the colonoscopy request was accepted (1) or rejected (0): revised requests|
|priorization_val| priorization level of accepted colonoscopies (1 to 5): revised requests|
|rebuig_val| rejection reason of rejected colonoscopies (1 to 7): revised requests|
|notes| anotator comments|



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


## Annex

### Document de context per l’avaluació de l’adequació de les sol·licituds de colonoscòpia ambulatòries

Aquest protocol estableix el coneixement de context necessari perquè un humà i un model de llenguatge siguin capaços d’avaluar l’adequació de les sol·licituds de colonoscòpia ambulatòries i, per tant, prendre una decisió: si s’accepta o es rebutja la prova. Que una sol·licitud de colonoscòpia sigui adequada significa que la sol·licitud s’adapta a un o més dels motius de sol·licitud explicats al present document. En aquest cas s’acceptarà la prova. En cas que la prova s’accepti, cal indicar-ne la prioritat. En cas que la sol·licitud no s’adapti a cap dels motius següents, la prova s’ha de rebutjar i cal indicar el motiu de rebuig. 

**Possibilitats de decisió**

1.	En cas que sigui adequada, la sol·licitud s’acceptarà i caldrà indicar la prioritat de la prova que pot ser:
	- Prioritat 1. Urgent
	- Prioritat 2. Preferent
	- Prioritat 3. Electiva
	- Prioritat 4. Ajornable
	- Prioritat 5. Control programat

Al document de context figura en cada cas quina prioritat s’ha de seguir. En cas que la prova s’adeqüi a dos motius de sol·licitud, es triarà la prioritat més propera a 1.

2. 	Si la colonoscòpia no està indicada es rebutjarà i caldrà especificar un dels 7 motius de rebuig:
	- Rebuig 1. Cribratge oportunista 
	- Rebuig 2. Antecedents familiars de càncer colorectal 
	- Rebuig 3. Vigilància post-polipectomia 
	- Rebuig 4. Vigilància Interval Incorrecte 
	- Rebuig 5. No indicada per edat 
	- Rebuig 6. Manca d’Informació 
	- Rebuig 7. Manca de test de sang en femta

3.	Tota petició sense informació sobre el motiu de la colonoscòpia (sense text o que sigui impossible establir clarament el motiu de la sol·licitud) es rebutjarà per manca d’informació (Rebuig 6).

**Motius adequats de sol·licitud de colonoscòpia**

1. Colonoscòpia per símptomes

La petició de la colonoscòpia es demana per símptomes quan el metge sol·licitant especifiqui que el pacient té algun tipus de símptoma abdominal/digestiu (dolor abdominal, restrenyiment, pèrdua de pes, canvi en el ritme deposicional, distensió, diarrea, anèmia, rectorràgia, melenes, hematoquècia, hemorràgia digestiva, sang amb les deposicions). Qualsevol sol·licitud on s’especifiquin símptomes s’ha d’avaluar segons els criteris d’aquest apartat i no segons els criteris dels altres apartats. 
- Diarrea crònica (diarrea de més de 2 mesos d’evolució) per descartar colitis microscòpica:  (S’accepta amb Prioritat 2). 
- Quan hi hagi una elevada sospita de malaltia inflamatòria intestinal (perquè així s’indiqui a la petició o perquè especifiquin que la petició és per diarrea crònica amb sang o moc i, a més a més, febre, dolor abdominal o pèrdua de pes:  (S’accepta amb Prioritat 1).
- Quan s’especifiqui que l’exploració sigui per aplicar un tractament sobre una lesió ja coneguda (tractament d’angiodisplàsies, proctitis actínica, resecció de lesions ja conegudes, lesions ressecades parcialment, etc): (S’accepta amb Prioritat 1).
- Quan s’especifiqui que el tacte rectal és patològic (massa o lesió palpable per tacte rectal) o bé es palpi una massa a l’exploració abdominal. S’han d’acceptar amb Prioritat 1.

Per acceptar una petició de colonoscòpia per símptomes en altres situacions a les prèvies caldrà que s’especifiqui el resultat del test de sang oculta en femta (TSOFi) (sinònims: TSOF, SOFi, SOF, TSOH, fecatest, sang oculta en femta, sang oculta i similars). Si el resultat del TSOFI no s’especifica a la sol·licitud o es va fer fa més de 6 mesos i era negatiu, es rebutjarà la colonoscòpia (Rebuig 7).

Resultat del TSOFi:
- Positiu: Quan especifiquin que és positiu o que té ≥ 10 µg Hb/g femta o ≥ 50 ng/mL. Tota petició que tingui un TSOFi positiu pel motiu que sigui serà acceptada amb Prioritat 1. Es considerarà negativa amb un punt de tall <10 μg Hb/g femta.
- Negatiu: Quan s’especifiqui que és negatiu o < 10 µg Hb/g femta o < 50 ng/mL. Les peticions per símptomes amb TSOFi negatiu es prioritzaran segons els símptomes.
	- Com a norma general qualsevol indicació de colonoscòpia per símptomes amb TSOFi negatiu serà acceptada amb prioritat 3 excepte les esmentades a continuació.
		- Anèmia ferropènica, estrenyiment, distensió abdominal o canvi en el ritme deposicional en pacient major de 50 anys i sense colonoscòpies prèvies  Prioritat 2. 
		- Rectorràgia (o qualsevol sinònim d’hemorràgia digestiva) en pacient sense colonoscòpia prèvia Prioritat 2. Si les rectorràgies cursen amb anemització llavors serà Prioritat 1.
 
2. Colonoscòpia de vigilància de pòlips o lesions precursores de càncer colorectal

Una colonoscòpia serà de vigilància quan el pacient no tingui cap símptoma digestiu o abdominal i es demani per controlar pòlips ressecats prèviament en una colonoscòpia prèvia o després de la resecció quirúrgica o endoscòpica d’un càncer colorectal. S’entendrà que pòlip i lesió són sinònims.

2.1 Colonoscòpia de vigilància de pòlips
- A partir dels 80 anys no es recomanen colonoscòpies de vigilància de pòlips pel que es rebutjarà la petició (Rebuig 5).

Hi ha tres tipus de lesions ressecats per colonoscòpia que cal vigilar a la resta de pacients:
- Adenoma no avançat: < 10mm i displàsia de baix grau.
- Adenoma avançat: ≥ 10mm, displàsia d’alt grau o component vellós a l’anatomia patològica.
- Lesions serrades: lesió serrada sèssil, serrat tradicional i lesió hiperplàsica excepte els hiperplàsics de recte-sigma de menys de 10mm.
- 
Els intervals de vigilància recomanats són els següents:
- En cas de resecció en fragments d’una lesió sèssil o plana ≥ 20mm es farà la colonoscòpia als 4-6 mesos. 
- No requereixen vigilància: quan la colonoscòpia prèvia sigui normal, tingui < 5 lesions no avançades (suma d’adenomes no avançats i lesions serrades) o únicament identifiqui pòlips hiperplàsics a recte-sigma < 10mm. En aquests casos rebutjarem la petició (Rebuig 3). 
- La resta de lesions requereixen vigilància:
	- Vigilància estàndard (3 anys):
		- Adenoma avançat
		- Suma de lesions (adenomes + serrades) entre 5 i 9 
	- Vigilància intensiva (1 any): 
		- Lesió sèssil o plana (no pediculada) ≥ 20mm extirpada en bloc (no fragmentada)
		- Suma de lesions (adenomes + serrades) ≥ 10
	- Si el pacient havia tingut pòlips en colonoscòpies anteriors però en la darrera colonoscòpia no tenia lesions o tenia lesions que no requereixen vigilància s’ha d’acceptar la colonoscòpia i programar-la en 5 anys.

2.2 Colonoscòpia de vigilància després de cirurgia de càncer colorectal (o tractament endoscòpic de pT1)

- Primera colonoscòpia de vigilància a 1 any de la intervenció prèvia.
- Segona colonoscòpia als 3 anys de la cirurgia (o resecció endoscòpica).
- Després se seguirà cada 5 anys sempre i quan no hi hagi lesions que impliquin una vigilància estàndard o intensiva (veure punt 2.1). Si el pacient té > 80 anys en aquest punt, es rebutjarà atès que no es recomanen colonoscòpies de vigilància (Rebuig 5).
 
Per tant, per prendre les decisions d’acceptació o rebuig i de priorització en cas d’acceptació de la prova, caldrà conèixer la data de quan es va fer la resecció dels pòlips o del càncer colorectal, o bé la data de la darrera colonoscòpia i el seu resultat. Si aquesta informació no figura a la sol·licitud caldrà rebutjar la colonoscòpia (Rebuig 6). 
En la petició hi haurà una data de preferència que l’indicarà el metge sol·licitant. 
- Si la data de preferència s’adequa aproximadament a l’interval de vigilància indicat en aquest document llavors s’acceptarà la petició i es programarà com a Prioritat 5 respectant aquesta data de preferència. 
- Si la data de preferència no s’adequa a l’interval de vigilància indicat o no apareix però el pacient té indicació de colonoscòpia de vigilància en l’any actual llavors s’acceptarà la petició i es programarà com a Prioritat 4. 
- Si la data de preferència no s’adequa a l’interval de vigilància indicat o no apareix i el pacient no té indicació de colonoscòpia de vigilància en l’any actual llavors es rebutjarà l’exploració (Rebuig 4).

Cal recordar per donar un interval de vigilància adequat caldrà que la colonoscòpia inicial sigui de qualitat, és a dir, completa (fins a cec), amb preparació adequada (Boston ≥ 6 punts) i amb resecció de totes les lesions observades (excepte les lesions hiperplàsiques < 10mm de recte-sigma). Si a la petició s’informa que la colonoscòpia prèvia és incompleta, mal preparada o no s’han extirpat totes les lesions caldrà repetir-la amb Prioritat 2. Finalment, si a l’anamnesi s’especifica que la colonoscòpia és de vigilància o control de pòlips però també descriuen símptomes llavors es prioritzarà segons els símptomes (veure apartat 1) colonoscòpia per símptomes). 

3. Colonoscòpia de cribratge de càncer colorectal (CCR)

S’entendrà que la petició de la colonoscòpia és per cribratge quan el metge sol·licitant així ho especifiqui fent ús del terme “cribratge” o un sinònim (“despistatge”, “screening”, etc) i no refereixi cap símptoma digestiu o abdominal. Hi ha diverses situacions possibles: 
- Cribratge oportunista: El cribratge oportunista consisteix en fer una prova per detectar càncer colorectal o lesions precursores de càncer colorectal en un pacient sense símptomes fora del programa de cribratge poblacional. En el nostre medi el cribratge oportunista no s’ha de fer amb colonoscòpia. Es rebutjarà tota petició de colonoscòpia per cribratge oportunista de càncer colorectal (Rebuig 1. Cribratge oportunista) excepte en dues situacions: si s’ha fet prèviament un test de sang oculta en femta i ha resultat positiu, o bé si hi ha antecedents familiars de càncer colorectal que cumpleixin criteris (veure següent punt). Si el test de sang oculta en femta és positiu s’acceptarà la prova amb prioritat 1. Si s’especifica que hi ha antecedents familiars cal veure el següent punt.   
- Cribratge per antecedents familiars: En cas de colonoscòpia de cribratge (sense símptomes) i que en la petició s’especifiquin antecedents familiars de càncer colorectal, únicament s’acceptarà si s’especifica que el pacient té un familiar de primer grau (pares, germans o fills) amb diagnòstic de càncer colorectal abans dels 50 anys, o bé dos o més  familiars de primer grau amb càncer colorectal independentment de l’edat. En aquests casos s’accepta la colonoscòpia si el pacient té més de 40 anys amb Prioritat 4. En els casos en què els antecedents familiars no compleixin els criteris prèviament esmentats es rebutjarà (Rebuig 2). En cas que no s’especifiquin amb detall suficient els antecedents familiars es rebutjarà la prova per manca d’informació (Rebuig 6). En els pacients en què s’hagi realitzat una colonoscòpia de cribratge per antecedents familiars, la vigilància de les successives colonoscòpies s’ha de fer als  5 anys de la prèvia pel que s’acceptaria la prova amb Prioritat 5, sempre i quan no hi hagi lesions que justifiquin un seguiment més intensiu (veure apartat 2.1) o s’hagi fet un TOSFi amb resultat positiu (prioritat 1).  
- En cas que s’especifiqui alguna síndrome hereditària de càncer colorectal (síndrome de Lynch, poliposi adenomatosa familiar, etc) caldrà derivar el malalt a la Clínica d’Alt Risc de càncer colorectal (Rebuig 1).
- A partir dels 80 anys no està indicat realitzar colonoscòpies de cribratge ni de vigilància i únicament s’han d’avaluar les que es demanen per símptomes. En cas de colonoscòpia de cribratge en pacient de 80 anys o més es rebutjarà (Rebuig 5).

4. Altres indicacions
Hi ha altres indicacions que no queden englobades en cap dels grups previs i que s’acceptaran també sense la necessitat de disposar d’un test de sang oculta en femta. 
- Colonoscòpia de control post-diverticulitis. S’han d’acceptar amb prioritat 2 excepte si el pacient s’ha fet una colonoscòpia prèvia en els últims 5 anys completa i ben preparada. En aquests darrers casos s’ha de rebutjar (Rebuig 4).   
- Estudi d’extensió, avaluació resposta o control de malaltia inflamatòria intestinal (malaltia de Crohn o colitis ulcerosa). S’han d’acceptar amb Prioritat 2.
- Tractament o diagnòstic de lesions al colon conegudes per alguna altra exploració (lesió detectada a un escàner, TAC o captació a PET-TC). S’han d’acceptar amb Prioritat 1. 
- Colonoscòpia prèvia a una cirurgia (avaluació pretransplantament hepàtic o renal, previ a cirurgia esofagogàstrica amb possible necessitat de coloplàstia, etc). S’han d’acceptar amb Prioritat 1.
- Protocol “watch & wait” (W&W) de vigilància del càncer de recte. Prioritat 5. 
- Cribratge de displàsia a la malaltia inflamatòria intestinal (malaltia de Crohn o colitis ulcerosa). Prioritat 5. 



















