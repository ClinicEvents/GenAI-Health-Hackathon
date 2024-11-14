# Challenge 28: Querying a database using natural language

Users accessing data in the hospital are doctors, many of whom lack the training to interact directly with the hospital's database. For this reason, they are provided with a set of tables (views) containing all the necessary information to carry out their studies.

However, there are times when doctors need information that requires combining some of these tables. Requesting an expert to create the needed query can be a slow process, which may limit doctors' responsiveness.

From this need, this challenge was born, aiming to generate a SQL query from natural language to improve the accessibility, responsiveness, and efficiency of the service provided to healthcare personnel.

## Objective

Generate a SQL query from natural language input. Compare the results with the model: nat2sql-DSC.

Improvement 1: the model must be insensitive to misspelling/language in order to filter the data correctly.  

Improvement 2: the model must be able to select tables correctly even if the description/reference is not  explicitly included.

## Expected Outcomes

The solution proposed by participants should be able to generate SQL for the following natural language queries:

- Query 1

```
Give me the patients who had two different episodes and the time difference between those episodes must be less than a week. Include patient, episode and the time difference.
```

- Query 2

```
For patients who have '%esclerosis%lateral%amiotrófica%' diagnosis, give me the highest value measured of "%colesterol total%" during the episode. Include episode, lab description, units and the  highest value measured.
```

- Query 3

```
Patients who had "Calcio" (lab) greater than 11,5 mg/dL during a normal hospital admission. I just want to know for 2023.
```

- Query 4

```
Patients older than 65 years of age who had an admission diagnosis  "%fractura%fémur%". Health care during the episode had to be done by the medical unit whose reference is "A".
```

- Query 5

```
Patients who have been in an “ICU” type of care level, compute the average duration (hours) of the episode duration. Exclude those who have been there less than 24 hours. Moreover, patients must be located in a unit with a reference "X" or "Y". Compute how many patients fulfill these conditions.
```

- Query 6

```
I want to know how many episodes had a "%infarto%agudo%miocardio%ST%" diagnosis for each month in 2023. In these episodes, "Glucosa" had to be measured.
```

- Query 7

```
Compute the PaFi coefficient which is the relation between 'pO2 sangre arterial' (lab) and 'FiO2 mezclador'(rc). Include only patients who had 'G47.%' diagnosis code. Result has to include patient, episode, PaFi, medical unit that requests the measurements, and the extraction date.
```

- Query 8

```
I want to know the time between the beginning of the episode and the first measured "ACR_FIO2" value (rc). During the episode, the patient must be at least once in an "ICU" type of care level. Include the patient, the episode, the value of the first "ACR_FIO2" measured and the difference in hours between the beginning of the episode and the first measurement. Use  subqueries to answer my question.
```

Improvement 1:
```
Patients who had "calci" (lab) greater than 11,5 mg/dl during a normal hospital admission. I just want to know for 2023.
```

NOTE: outcomes must be the same as query 3.


Improvement 2:
```
Patients who had "Calcio" greater than 11,5 mg/dL during a normal hospital admission. I just want to know for 2023.
```

NOTE: outcomes must be the same as query 3.

## Tools

Participants will have access to the following information/tools to complete the challenge:

- Data:

  - Database

- Development:

  - Jupyter Notebook
  - Bedrock
  - Shared bucket 

- Validation:

  - Aurora PostgreSQL
  - Nat2sql-DSC

- Guides. It is recommended to read the following demos:
  - DEMO_bedrock_connection
  - DEMO_nat2sqlDSC

**All development must be carried out using the services available on AWS. Moving information outside of the specified tools is NOT allowed.**

Below are details of the most relevant aspects of the tools available to participants.

### Database

This section details the available tables (views) and their attributes.

**NOTE:** If a patient is not found in the databases, the k-anonimization has deleted it.

#### VIEW: demo_events

Defines patient's attributes. Contains demographic information about the patient.

The attributes of the table are listed below:

<center>

| Name         | Description                                             |
| ------------ | ------------------------------------------------------- |
| patient_ref  | patient identifier                                      |
| birth_date   | birth date                                              |
| sex_atr      | patient gender. NOTE: 1 (male), 2 (female), 3 (other)   |
| natio_ref    | country code corresponding to the patient’s nationality |
| nation_descr | description of the country code                         |

</center>

#### VIEW: episode_events

Records medical events that happen to a patient, such as admission, assessment in the emergency department, among others.

The attributes of the table are listed below:

<center>

| Name        | Description                                                                                                                                                                                                                                                                        |
| ----------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| patient_ref | patient identifier                                                                                                                                                                                                                                                                 |
| episode_ref | episode identifier                                                                                                                                                                                                                                                                 |
| type_ref    | episode type reference. NOTE: AM (outpatient episode), EM (emergency episode), DO (donor), HOSP_IQ (hospitalization episode for surgery), HOSP_RN (hospitalization of a healthy newborn), HOSP (hospitalization episode different from HOSP_IQ and HOSP_RN), EXT_SAMP (external sample), HAH (home hospitalization) |
| start_date  | episode start date                                                                                                                                                                                                                                                                 |
| end_date    | episode end date                                                                                                                                                                                                                                                                   |

</center>

#### VIEW: rc_events

Contains the patient's clinical records. Based on observations and measurements, the doctors could determine the patient's status.

The attributes of the table are listed below:

<center>

| Name           | Description                                                                                                             |
| -------------- | ----------------------------------------------------------------------------------------------------------------------- |
| patient_ref    | patient identifier                                                                                                      |
| episode_ref    | episode identifier                                                                                                      |
| result_date    | measurement date                                                                                                        |
| meas_type_ref  | specifies the measurement method used. NOTE: 0 (manual), 1 (machine, not validated result), 2 (machine, validated result) |
| ou_loc_ref     | code of the patient’s location / physical hospitalization unit                                                          |
| ou_med_ref     | code of the medical organizational unit                                                                                 |
| rc_sap_ref     |clinical record reference                                                                                            |
| descr          | description of the clinical record reference                                                                                 |
| result_num     | numeric result                                                                                                          |
| result_txt     | text result                                                                                                             |
| units          | units                                                                                                                   |
| care_level_ref | care level identifier                                                                                                 |

</center>

#### VIEW: lab_events

Records the results obtained from tests sent to the laboratory.

The attributes of the table are listed below:

<center>

| Name           | Description                                                       |
| -------------- | ----------------------------------------------------------------- |
| patient_ref    | patient identifier                                                |
| episode_ref    | episode identifier                                                |
| extrac_date    | extraction date                                                   |
| result_date    | date of result publication                                        |
| ou_med_ref     | code of the medical organizational unit requesting the extraction |
| lab_sap_ref    |  laboratory parameter reference                                         |
| descr          | description of the laboratory parameter reference                 |
| result_num     | numeric result                                                    |
| result_txt     | text result                                                       |
| units          | units                                                             |
| care_level_ref | care level identifier                                           |

</center>

#### VIEW: care_level_events

Defines the level of care required by a patient during an episode.

The attributes of the table are listed below:

<center>

| Name                | Description                                                                                                                                                                                                                |
| ------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| patient_ref         | patient identifier                                                                                                                                                                                                         |
| episode_ref         | episode identifier                                                                                                                                                                                                         |
| care_level_ref      | care level identifier                                                                                                                                                                                                      |
| start_date          | start date of care level                                                                                                                                                                                                   |
| end_date            | end date of care level                                                                                                                                                                                                     |
| care_level_type_ref | care level type. NOTE: WARD (conventional hospitalization), ICU (intensive care unit), EM (emergency episode), SPEC (special episode), HAH (home hospitalization), PEND. CLAS (pending classification), SHORT (short stay) |

</center>

#### VIEW: mov_events

Records each specific location where the patient was during the episode period.

The attributes of the table are listed below:

<center>

| Name                | Description                                                    |
| ------------------- | -------------------------------------------------------------- |
| patient_ref         | patient identifier                                             |
| episode_ref         | episode identifier                                             |
| start_date          | movement start date                                            |
| end_date            | movement end date                                              |
| place_ref           | patient room/bed code                                          |
| ou_loc_ref          | code of the patient’s location / physical hospitalization unit |
| ou_loc_descr        | description of the physical hospitalization unit               |
| ou_med_ref          | code of the medical organizational unit                        |
| ou_med_descr        | description of the medical organizational unit                 |
| facility_descr      | specifies which facility ou_loc_descr belongs to               |
| care_level_ref      | care level identifier                                          |
| care_level_type_ref | care level type                                                |

</center>

#### VIEW: diag_events

Set of diagnoses determined during an episode.

The attributes of the table are listed below:

<center>

| Name        | Description                                                                                 |
| ----------- | ------------------------------------------------------------------------------------------- |
| patient_ref | patient identifier                                                                          |
| episode_ref | episode identifier                                                                          |
| reg_date    | diagnosis registration date                                                                 |
| diag_ref    | diagnosis reference                                                                         |
| catalog     | indicates the catalog to which the diagnosis belongs                                        |
| code        | diagnosis code                                                                              |
| descr       | diagnosis description                                                                       |
| class_ref   | code indicating the type of diagnosis. NOTE: P (primary diagnosis), S (secondary diagnosis) |
| poa_ref     | code indicating if the diagnosis was present at admission                                   |

</center>

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

### Validation

Participants have access to an Aurora PostgreSQL database and nat2sql-DSC in order to help them in the development of the challenge.

#### Aurora PostgreSQL database

A database simulating the views in Aurora PostgreSQL has been created so that users can query the data and test the generated SQL queries. Users can connect to the database using `pgcli` or `pgAdmin` with the following configuration:

```.env
HOST = datathone-database-2024.cluster-c92ey0eoyy93.us-west-2.rds.amazonaws.com
USER = clinic2024
PASSWORD =  Isi+ArXFSP5kdvO
DATABASE = datathone_datascope
```

NOTE: you can use `pgcli`, `pgAdmin` or `psycopg2` library (python) to connect with Aurora PostgreSQL.

#### Nat2sql-DSC model

`Nat2sql-DSC` is a simple model developed by Clínic Hospital that generates a SQL query from natural language. Users will have access to this service to compare the SQL queries generated by their model with the Clínic model. For more information on how to use 'Nat2sql-DSC', see the demo: `DEMO_nat2sqlDSC`.

NOTE: Improvements 1 and 2 are not included in `Nat2sql-DSC` model available at this event.

Results provided by Nat2sql-DSC model are also included below:

- Query 1

Natural language:

```
Give me the patients who had two different episodes and the time difference between those episodes must be less than a week. Include patient, episode and the time difference.
```

SQL query:

```SQL
WITH episode_pairs AS (
  SELECT
    e1.patient_ref,
    e1.episode_ref AS episode1,
    e2.episode_ref AS episode2,
    e2.start_date - e1.start_date AS time_difference
  FROM
    episode_events e1
  JOIN
    episode_events e2 ON e1.patient_ref = e2.patient_ref
  WHERE
    e1.episode_ref < e2.episode_ref
    AND e2.start_date - e1.start_date BETWEEN INTERVAL '0 days' AND INTERVAL '7 days'
)
SELECT
  patient_ref,
  episode1,
  episode2,
  time_difference
FROM
  episode_pairs
ORDER BY
  patient_ref, episode1, episode2;
```

- Query 2

Natural language:

```
For patients who have '%esclerosis%lateral%amiotrófica%' diagnosis, give me the highest value measured of "%colesterol total%" during the episode. Include episode, lab description, units and the  highest value measured.
```

SQL query:

```SQL
SELECT
    de.episode_ref,
    le.descr AS lab_description,
    le.units,
    MAX(le.result_num) AS highest_value
FROM
    diag_events de
JOIN
    lab_events le ON de.patient_ref = le.patient_ref AND de.episode_ref = le.episode_ref
WHERE
    de.descr ILIKE '%esclerosis%lateral%amiotrófica%'
    AND le.descr ILIKE '%colesterol total%'
GROUP BY
    de.episode_ref,
    le.descr,
    le.units
ORDER BY
    highest_value DESC
```

- Query 3

Natural language:

```
Patients who had a "Calcio" (lab) greater than 11,5 mg/dL during a normal hospital admission. I just want to know by 2023.
```

SQL query:

```SQL
SELECT DISTINCT le.patient_ref
FROM lab_events le
JOIN episode_events ee ON le.patient_ref = ee.patient_ref AND le.episode_ref = ee.episode_ref
WHERE le.descr = 'Calcio'
  AND le.result_num > 11.5
  AND le.units = 'mg/dL'
  AND ee.type_ref = 'HOSP'
  AND EXTRACT(YEAR FROM le.extrac_date) = 2023
  AND le.extrac_date BETWEEN ee.start_date AND COALESCE(ee.end_date, CURRENT_TIMESTAMP);
```

- Query 4

Natural language:

```
Patients older than 65 years of age who had an admission diagnosis  "%fractura%fémur%". Health care during the episode had to be done by medical the unit whose reference is "A".
```

SQL query:

```SQL
SELECT DISTINCT de.patient_ref
FROM demo_events de
JOIN episode_events ee ON de.patient_ref = ee.patient_ref
JOIN diag_events dg ON ee.patient_ref = dg.patient_ref AND ee.episode_ref = dg.episode_ref
JOIN mov_events me ON ee.patient_ref = me.patient_ref AND ee.episode_ref = me.episode_ref
WHERE de.birth_date <= (CURRENT_DATE - INTERVAL '65 years')
  AND LOWER(dg.descr) LIKE '%fractura%fémur%'
  AND me.ou_med_ref = 'A'
  AND ee.start_date = (
    SELECT MIN(start_date)
    FROM episode_events ee2
    WHERE ee2.patient_ref = ee.patient_ref
      AND ee2.episode_ref = ee.episode_ref
  );
```

- Query 5

Natural language:

```
Patients who have been in an “ICU” type of care level, compute the average duration (hours) of th episode duration. Exclude those who have been there less than 24 hours. Moreover, patients must be located in a unit with a reference "X" or "Y". Compute how many patients fulfill these conditions.
```

SQL query:

```SQL
WITH icu_patients AS (
    SELECT DISTINCT cle.patient_ref, cle.episode_ref,
           EXTRACT(EPOCH FROM (ee.end_date - ee.start_date)) / 3600 AS episode_duration_hours
    FROM care_level_events cle
    JOIN episode_events ee ON cle.patient_ref = ee.patient_ref AND cle.episode_ref = ee.episode_ref
    JOIN mov_events me ON cle.patient_ref = me.patient_ref AND cle.episode_ref = me.episode_ref
    WHERE cle.care_level_type_ref = 'ICU'
    AND (me.ou_loc_ref = 'X' OR me.ou_loc_ref = 'Y')
),
filtered_patients AS (
    SELECT *
    FROM icu_patients
    WHERE episode_duration_hours >= 24
)
SELECT
    AVG(episode_duration_hours) AS avg_episode_duration_hours,
    COUNT(DISTINCT patient_ref) AS patient_count
FROM filtered_patients;
```

- Query 6

Natural language:

```
I want to know how many episodes had a "%infarto%agudo%miocardio%ST%" diagnosis for each month in 2023. In these episodes, "Glucosa" had to be measured.
```

SQL query:

```SQL
SELECT
     DATE_TRUNC('month', d.reg_date) AS month,
     COUNT(DISTINCT d.episode_ref) AS episode_count
 FROM
     diag_events d
 JOIN
     lab_events l ON d.patient_ref = l.patient_ref AND d.episode_ref = l.episode_ref
 WHERE
     d.descr ILIKE '%infarto%agudo%miocardio%ST%'
     AND l.descr = 'Glucosa'
     AND EXTRACT(YEAR FROM d.reg_date) = 2023
 GROUP BY
     DATE_TRUNC('month', d.reg_date)
 ORDER BY
     month;
```

- Query 7

Natural language:

```
Compute the PaFi coefficient which is the relation between 'pO2 sangre arterial' (lab) and 'FiO2 mezclador'(rc). Include only patients who had 'G47.%' diagnosis code. Result has to include patient, episode, PaFi, medical unit that requests the measurements, and the extraction date.
```

SQL query:

```SQL
SELECT
    le.patient_ref,
    le.episode_ref,
    le.result_num / rc.result_num AS PaFi,
    le.ou_med_ref,
    le.extrac_date
FROM
    lab_events le
JOIN rc_events rc ON
    le.patient_ref = rc.patient_ref
    AND le.episode_ref = rc.episode_ref
JOIN diag_events de ON
    le.patient_ref = de.patient_ref
    AND le.episode_ref = de.episode_ref
WHERE
    le.descr = 'pO2 sangre arterial'
    AND rc.descr = 'FiO2 mezclador'
    AND de.code LIKE 'G47.%'
    AND le.result_num IS NOT NULL
    AND rc.result_num IS NOT NULL
    AND rc.result_num != 0;
```

- Query 8

Natural language:

```
I want to know the time between the beginning of the episode and the first measured "ACR_FIO2" value (rc). During the episode, the patient must be at least once in an "ICU" type of care level. Include the patient, the episode, the value of the first "ACR_FIO2" measured and the difference in hours between the beginning of the episode and the first measurement. Use  subqueries to answer my question.
```

SQL query:

```SQL
SELECT
    e.patient_ref,
    e.episode_ref,
    first_acr.result_num AS first_acr_fio2,
    EXTRACT(EPOCH FROM (first_acr.result_date - e.start_date)) / 3600 AS hours_difference
FROM
    episode_events e
JOIN
    (SELECT
        patient_ref,
        episode_ref,
        MIN(result_date) AS first_acr_date
    FROM
        rc_events
    WHERE
        rc_sap_ref = 'ACR_FIO2'
    GROUP BY
        patient_ref, episode_ref) first_acr_date
ON
    e.patient_ref = first_acr_date.patient_ref
    AND e.episode_ref = first_acr_date.episode_ref
JOIN
    rc_events first_acr
ON
    first_acr.patient_ref = first_acr_date.patient_ref
    AND first_acr.episode_ref = first_acr_date.episode_ref
    AND first_acr.result_date = first_acr_date.first_acr_date
    AND first_acr.rc_sap_ref = 'ACR_FIO2'
WHERE
    EXISTS (
        SELECT 1
        FROM care_level_events cl
        WHERE cl.patient_ref = e.patient_ref
        AND cl.episode_ref = e.episode_ref
        AND cl.care_level_type_ref = 'ICU'
    )
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
