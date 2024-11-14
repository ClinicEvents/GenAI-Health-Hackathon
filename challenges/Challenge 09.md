# Challenge 09: Personalized Delivery of Nutrition Tips for Prehabilitation Patients


This project focuses on the evaluation of artificial intelligence tools that personalize educational content for patients with specific needs or limitations, especially for patients included in surgical prehabilitation programs. The main objective is to explore how these tools adapt explanations and educational material based on changes in the patient's profile, aiming to improve patient empowerment for self-management of their health.

In the current context, providing personalized and understandable education for each patient is an essential component in the management of chronic diseases and pre-surgical preparation. However, educational content is often tailored to basic patient’s profiles, without considering the specific characteristics of each patient, which may limit the effectiveness of these interventions. 

This challenge seeks to overcome this limitation by using technology that adjusts educational content to the unique patient's nutritional status, target surgery, sociodemographic data, comorbidities and frailty scale.
This project aims to evaluate the linguistic quality, integrity of the content, and the adaptation of educational material to the real needs of patients, ensuring that the explanations are clear, complete, and factual.

## Objective

Evaluate the performance of artificial intelligence tools to extract the patient's nutritional status from the transcription of the conversation between the patient and the nutritionist during the face-to-face appointment in the outpatient’s clinic, and generate personalized nutrition tips. 


## Expected outcomes

### Input

Nutricionista: Bon dia! Avui revisarem algunes dades per avaluar el teu estat nutricional. Comencem amb els valors registrats a la teva història clínica. 
Veig que tens una hemoglobina de 15.4 g/dL. Com et sents últimament, has notat fatiga o cansament?
Pacient: No, em sento bé.

Nutricionista: D'acord. També tens els nivells d'albúmina a 45.0 g/L i prealbúmina a nan g/L. Els metges han comentat alguna cosa sobre aquests valors?
Pacient: Sí, m’han dit que estic una mica baix en aquests valors.

Nutricionista: Bé, passem a calcular el teu IMC. Segons la teva alçada i pes, l’índex de massa corporal és 22.5 kg/m². Et sembla correcte el pes que tenim registrat?
Pacient: Sí, sembla correcte.

Nutricionista: Ara prendré el perímetre del bessó, que és de 36.5 cm, i la força del hand-grip que és de 65.0 kg. Com et sents amb la teva força actual?
Pacient: Crec que està bé.

Nutricionista: Finalment, m'agradaria saber si tens alguna condició que afecti la ingesta o absorció d’aliments, com per exemple nàusees, anorèxia o altres problemes.
Pacient: No, no tinc problemes.

Nutricionista: Molt bé, i prens algun suplement nutricional? Aquí tinc registrat Checked.
Pacient: Sí, prenc un suplement energètic i proteic.

Nutricionista: Gràcies per la informació, farem un seguiment properament. Cuida't!

### Output 1: outpatient’s clinic

-	emoglobina 	7.6
-	Albúmina	37
-	Prealbúmina	0.088
-	Índex de massa corporal (IMC) (Kg/m2)	20.4
-	Perímetre bessó (cm)	29.8
-	Hand-grip dominant (Kg)	39
-	Estat nutricional	
-	Pateix condicions que dificultin l'ingesta i/o l'absorció? (choice=No)	Unchecked
-	Pateix condicions que dificultin l'ingesta i/o l'absorció? (choice=Anorèxia)	Checked
-	Pateix condicions que dificultin l'ingesta i/o l'absorció? (choice=Nàusees / Vòmits)	Unchecked
-	Pateix condicions que dificultin l'ingesta i/o l'absorció? (choice=Dispèpsia)	Unchecked
-	Pateix condicions que dificultin l'ingesta i/o l'absorció? (choice=Diarrea)	Unchecked
-	Pateix condicions que dificultin l'ingesta i/o l'absorció? (choice=Disfàgia)	Unchecked
-	Pateix condicions que dificultin l'ingesta i/o l'absorció? (choice=Mucositis)	Unchecked
-	Pateix condicions que dificultin l'ingesta i/o l'absorció? (choice=Dolor / Distensió abdominal)	Unchecked
-	Pateix condicions que dificultin l'ingesta i/o l'absorció? (choice=Insuficiència pancreàtica)	Unchecked
-	Suplements nutricionals (choice=Enriquiment proteic amb aliments)	Unchecked
-	Suplements nutricionals (choice=Mòdul proteic)	Unchecked
-	Suplements nutricionals (choice=Suplement hiperproteic)	Unchecked
-	Suplements nutricionals (choice=Suplement energètic)	Unchecked
-	Suplements nutricionals (choice=Suplement energètic i proteic)	Checked
-	Suplements nutricionals (choice=Suplement inmunomodulador la setmana abans de la cirurgia)	Unchecked
-	Suplements nutricionals (choice=No necessita)	Unchecked
-	Dosi de suplement nutricional	2/dia
-	Dosi mòdul nutricional	No aplica

### Output 2: personalized nutrition tips
PARA EMPEZAR	
Conseguir o mantener un buen estado nutricional antes de la cirugía contribuye a disminuir las complicaciones, el tiempo de ingreso y a mejorar la recuperación. 
Durante los siguientes días recibirás recomendaciones para seguir una alimentación saludable enriquecida con proteínas. 
En caso de presentar síntomas digestivos (vómitos, diarreas, dolor abdominal, etc.) estas recomendaciones se adaptarán de forma individualizada consulte con su nutricionista.

ENRIQUECE TU ALIMENTACIÓN CON PROTEÍNAS	Incluye en todas las comidas algún alimento rico en proteínas como: pescado, huevo, pollo, carne, legumbres, yogur, leche, queso y frutos secos. Existen en el mercado productos enriquecidos en proteínas, introdúcelos en tu día a día. 
Estas recomendaciones de enriquecimiento proteico las debes seguir temporalmente hasta la intervención quirúrgica.
¿Cuáles son los alimentos aconsejables más ricos en proteínas?
-	Leche, yogures, kéfir, quesos (tiernos o frescos, tipo requesón o mató) 
-	Pescados blanco y azul. Mariscos
-	Huevos 
-	Pollo, pavo, conejo (sin piel ni grasa). Ternera y lomo de cerdo limitar a 1-2 veces/semanas. 
-	Fiambre de pavo, jamón serrano, jamón cocido (consumir de forma moderada)
-	Legumbres 
-	Frutos secos 
-	Soja y derivados (texturizado de soja, tofu, tempeh, bebida de soja) 
-	Derivados lácteos o vegetales ricos en proteínas: yogur, leche o batido de soja enriquecidos con proteínas.

VERDURAS, HORTALIZAS
Se aconseja un consumo mínimo de dos raciones diarias. Consúmelas crudas o cocidas, como plato principal o de guarnición. Prefiere las de temporada por ser más baratas, sabrosas y nutritivas.

FRUTAS	
Se aconseja un consumo de tres raciones diarias. Las puedes tomar de postre, en el desayuno, para merendar o incluirlas como ingrediente en una receta. Siempre es mejor comer la fruta entera y no en zumo. Prefiere las de temporada por ser más baratas, sabrosas y nutritivas.

¿CÓMO ENRIQUEZCO MI DIETA CON PROTEÍNAS?	
Aquí tienes ingredientes para añadir a platos habituales y complementarlos sin aumentar el volumen.	"¿Cómo enriquezco mi dieta con proteínas? Aquí tienes ingredientes para añadir a platos habituales y complementarlos sin aumentar el volumen. 
-	LÁCTEOS: Añade leche en polvo, queso fresco o bajo en grasa, queso en polvo o rallado en preparaciones de salsas, sopas, purés, cremas y batidos.
-	HUEVOS: Añade claras cocidas o huevo entero en sopas, cremas, arroz, pasta, leche.
-	FRUTOS SECOS: Almendras, piñones, pistachos, nueces, avellanas, cacahuete desgrasado... añádelos picados, triturados o en polvo en yogures, batidos, cremas, sopas, guisos, salsas, postres. 
-	SOJA, TOFU: Añade texturizado de soja o tofu en cremas, sopas y purés.

CEREALES INTEGRALES	
Los productos integrales son más nutritivos y aportan más fibra que las versiones de harina refinada por lo que son más aconsejables. Escoge la opción integral de pan, cereales, pasta y/o arroz.

LEGUMBRES	
Procura alcanzar las 2 ó 3 raciones semanales. Son la fuente de proteína vegetal por excelencia y contienen fibra, hidratos de carbono complejos y múltiples micronutrientes. Las puedes comer en una ensalada, en estofado, purés, en humus, etc.

PESCADOS, HUEVOS Y PRODUCTOS CÁRNICOS	
Consume pescado tanto blanco como azul, al menos tres veces a la semana. Toma 3 ó 4 huevos a la semana. Selecciona con mayor frecuencia carnes blancas (pollo o pavo sin piel y/o conejo) que carnes rojas, embutidos u otras carnes procesadas (hamburguesas, albóndigas, salchichas…).

SNACKS Y PREPARACIONES RICAS EN PROTEÍNAS	
¡Fáciles de preparar y saludables! Procura tomarlas entre horas o después de hacer ejercicio físico.	
Aquí tienes opciones de snacks y preparaciones ricas en proteínas:
-	Batido de plátano, bebida de soja y avellanas 
-	Batido de leche con queso fresco y fruta (fresas, melocotón o plátano…) 
-	Batido de tofu con naranja, mango y almendras 
-	Batido de yogur con leche en polvo y frutos secos 
-	Rollitos de jamón cocido con queso fresco o de queso tierno con humus 
-	Tortilla de dos claras y una yema con: jamón cocido o queso o atún o salmón ahumado reducidos en sal 
-	Yogur de soja (sin azúcares añadidos) con plátano y nueces picadas
-	Sándwich de pavo con huevo duro y un poco de mayonesa  

GRASAS	
Utiliza siempre aceite de oliva virgen, es una grasa saludable. Se puede utilizar tanto para aliñar como para cocinar ya que aguanta bien las temperaturas.

FRUTOS SECOS	
Inclúyelos varios días a la semana, entre horas, con el desayuno o como parte de un plato principal. Se deben consumir crudos o tostados, no fritos ni salados.

PRODUCTOS ULTRAPROCESADOS	
Evita consumir de forma habitual alimentos procesados como platos precocinados, embutidos y bollería por su alto contenido en aditivos, grasas saturadas, sal y azúcares.

SAL	
Reduce la sal añadida y condimenta con hierbas aromáticas, especias y limón para dar sabor. Modera el consumo de alimentos salados tipo: enlatados, conservas, chips y alimentos precocinados.

BEBIDAS	
El agua debe ser siempre la bebida de elección. Limita el consumo de bebidas azucaradas y evita el consumo de cualquier bebida alcohólica (vino, cava, cerveza, bebidas de alta graduación).

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

Transcripts ([BASE09](https://us-west-2.console.aws.amazon.com/s3/buckets/data-clinic-hackathon-2024?region=us-west-2&bucketType=general&prefix=BASE09/&showversions=false))

Source: AI-generated (ChatGPT 4o) patient-nutritionist conversations from tabular data. 

Content: Text files for each row in the tabular data. 

- **Nutritional profile (tabular data)**

Source: REDCap project of the surgical prehabilitation unit. 
Content: Hemoglobin, Albumin, Prealbumin, Body Mass Index (BMI) (Kg/m2), Calf circumference (cm), Dominant Hand-grip (Kg), Nutritional status (categorical), conditions that hinder intake and/or absorption (categorical), Nutritional supplements (categorical), Nutritional supplement dose (categorical), Nutritional module dose (categorical).

- **Sociodemographic and clinical data (tabular data)**

Source: REDCap project of the surgical prehabilitation unit. 
Content: assigned nutritional profile by the nutritionist (categorical), gender (categorical), Age (years), Target Surgery (categorical), educational status (categorical), living alone (Binary), dependency to attend the visits (Binary), marital status (Categorial), professional status (Categorial), transport (Categorial), season of the year (Categorial), Area of residence (Categorial), Oncologic Surgery (Binary), Neoadjuvant therapy (Binary), ASA (Categorial), comorbidities (Categorial), polypharmacy (Binary), Hemoglobin optimization (Categorial), Smoking status (Categorial), CSHA Frailty Scale (Categorial). 

- **Educational material per nutritional profile**
  
Source: specialized professionals (nutritionists) in simple text format. 
Content: Educational tips (text) prepared by the nutritionist according to the three patient educational profiles (Generic, Overweight, Low in residues).


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

**Performance analysis of extracting tabular data from text (evaluation)**
Assess the accuracy of the AI tools in correctly extracting the patient's nutritional status from the transcription of the conversations.
Metrics: accuracy, structural Fidelity, and error types.
Application: Measure the percentage of correctly extracted values compared to ground truth, assess how closely the extracted tables match the original structure, and analyze Common errors to understand the tool's limitations.

**Concordance Analysis (Validation)**
Compare the quality of the content generated by the AI tools with and without considering as context the manually created content by healthcare professionals.
Metrics: Assessment form (Appendix I).
Application: Assess the ability to enhance the profile-specific educational content generated by specialized professionals (nutritionists), ensuring that it is coherent, clear, relevant, and feasible for each patient according to their specific characteristics, and measure the linguistic quality and integrity of the content.

## Annex
```
AI-Enhanced Educational Content Evaluation Form
Patient Profile Information
Patient ID: ___________________
1. Coherence
Does the content flow logically from one point to the next?
[ ] 1 - Very incoherent
[ ] 2 - Somewhat incoherent
[ ] 3 - Neutral
[ ] 4 - Mostly coherent
[ ] 5 - Very coherent
Comments: ______________________________________________________
Does the content align with the professional’s original message?
[ ] 1 - Not aligned at all
[ ] 2 - Slightly misaligned
[ ] 3 - Neutral
[ ] 4 - Mostly aligned
[ ] 5 - Perfectly aligned
Comments: ______________________________________________________
2. Clarity
Is the information presented in a way that is easy for the patient to understand?
[ ] 1 - Very unclear
[ ] 2 - Somewhat unclear
[ ] 3 - Neutral
[ ] 4 - Mostly clear
[ ] 5 - Very clear
Comments: ______________________________________________________
Is the language free from jargon or overly complex terminology?
[ ] 1 - Too technical
[ ] 2 - Mostly technical
[ ] 3 - Neutral
[ ] 4 - Mostly simple
[ ] 5 - Very simple
Comments: ______________________________________________________
3. Relevance
Does the content address the patient’s specific health conditions and goals?
[ ] 1 - Very irrelevant
[ ] 2 - Somewhat irrelevant
[ ] 3 - Neutral
[ ] 4 - Mostly relevant
[ ] 5 - Very relevant
Comments: ______________________________________________________
Are the recommendations in line with current nutritional guidelines?
[ ] 1 - Not aligned
[ ] 2 - Somewhat aligned
[ ] 3 - Neutral
[ ] 4 - Mostly aligned
[ ] 5 - Perfectly aligned
Comments: ______________________________________________________
4. Feasibility
Are the recommendations realistic for the patient’s lifestyle and preferences?
[ ] 1 - Very unrealistic
[ ] 2 - Somewhat unrealistic
[ ] 3 - Neutral
[ ] 4 - Mostly realistic
[ ] 5 - Very realistic
Comments: ______________________________________________________
Are the recommendations actionable and easy to implement?
[ ] 1 - Very hard to implement
[ ] 2 - Somewhat hard to implement
[ ] 3 - Neutral
[ ] 4 - Mostly easy to implement
[ ] 5 - Very easy to implement
Comments: ______________________________________________________
5. Linguistic Quality and Integrity
Fluency: Does the content read naturally, without grammatical or syntactical errors?
[ ] 1 - Very poor fluency
[ ] 2 - Somewhat fluent
[ ] 3 - Neutral
[ ] 4 - Mostly fluent
[ ] 5 - Very fluent
Comments: ______________________________________________________
Brevity: Is the content concise, providing necessary information without unnecessary detail?
[ ] 1 - Too verbose
[ ] 2 - Somewhat verbose
[ ] 3 - Neutral
[ ] 4 - Mostly concise
[ ] 5 - Very concise
Comments: ______________________________________________________
Factual Accuracy: Is the content factually correct, with no misinformation about nutritional science or patient care?
[ ] 1 - Very inaccurate
[ ] 2 - Somewhat inaccurate
[ ] 3 - Neutral
[ ] 4 - Mostly accurate
[ ] 5 - Perfectly accurate
Comments: ______________________________________________________
Overall Coherence: Does the content maintain clarity and a cohesive message throughout?
[ ] 1 - Very incoherent
[ ] 2 - Somewhat coherent
[ ] 3 - Neutral
[ ] 4 - Mostly coherent
[ ] 5 - Very coherent
Comments: ______________________________________________________
6. Overall Satisfaction
Overall, how satisfied are you with the AI’s ability to enhance the educational content?
[ ] 1 - Very dissatisfied
[ ] 2 - Somewhat dissatisfied
[ ] 3 - Neutral
[ ] 4 - Mostly satisfied
[ ] 5 - Very satisfied
Comments: ______________________________________________________
7. Additional Feedback
What aspects of the AI-enhanced content were most helpful?________________________________________
What specific improvements would you suggest for the AI tool?________________________________________

```








